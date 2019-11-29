---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
title: Dávková aktualizaceC#() | Microsoft Docs
author: rick-anderson
description: Naučte se aktualizovat více databázových záznamů v rámci jedné operace. Ve vrstvě uživatelského rozhraní sestavíme prvek GridView, ve kterém je každý řádek upravitelný. V datech...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4e849bcc-c557-4bc3-937e-f7453ee87265
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
msc.type: authoredcontent
ms.openlocfilehash: baaaf37c47cc57d90ea579a5c20949bf8cfc7a3c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583619"
---
# <a name="batch-updating-c"></a>Dávkové aktualizace (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_CS.zip) nebo [stažení PDF](batch-updating-cs/_static/datatutorial64cs1.pdf)

> Naučte se aktualizovat více databázových záznamů v rámci jedné operace. Ve vrstvě uživatelského rozhraní sestavíme prvek GridView, ve kterém je každý řádek upravitelný. Ve vrstvě přístupu k datům zabalíme operace více aktualizací v rámci transakce, aby se zajistilo, že všechny aktualizace budou úspěšné nebo že se vrátí zpět všechny aktualizace.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](wrapping-database-modifications-within-a-transaction-cs.md) jsme viděli, jak vrstvu pro přístup k datům rozšíříte tak, aby přidala podporu pro databázové transakce. Transakce databáze zaručují, že řada příkazů pro úpravu dat bude považována za jednu atomickou operaci, která zajistí, že všechny úpravy selžou nebo budou úspěšné. Díky tomu, že tato funkce nižší úrovně přecházejí ze své míry, jsme připraveni na vytvoření rozhraní pro úpravu dat Batch.

V tomto kurzu sestavíme GridView, kde je každý řádek upravitelný (viz obrázek 1). Vzhledem k tomu, že se jednotlivé řádky vykreslují ve svém rozhraní pro úpravy, neexistuje žádný sloupec, který by měl mít tlačítka pro úpravy, aktualizaci a zrušení. Místo toho existují dvě tlačítka pro aktualizaci produktů na stránce, na které se po kliknutí zobrazí výčet řádků GridView a aktualizace databáze.

[![každý řádek v prvku GridView je upravitelný](batch-updating-cs/_static/image1.gif)](batch-updating-cs/_static/image1.png)

**Obrázek 1**: každý řádek v prvku GridView je upravitelný ([kliknutím zobrazíte obrázek v plné velikosti).](batch-updating-cs/_static/image2.png)

Pojďme začít!

> [!NOTE]
> V kurzu [provádění dávkových aktualizací](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md) jsme vytvořili rozhraní Batch pro úpravu pomocí ovládacího prvku DataList. Tento kurz se liší od předchozí verze v, který používá prvek GridView a dávková aktualizace se provádí v rámci transakce. Po dokončení tohoto kurzu se můžete vrátit k předchozímu kurzu a aktualizovat ho, aby používaly funkce související s transakční transakce přidané v předchozím kurzu.

## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>Prozkoumání kroků pro úpravy všech řádků GridView

Jak je popsáno v kurzu [vložení, aktualizace a odstranění dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) , GridView nabízí integrovanou podporu pro úpravu svých podkladových dat na jednotlivých řádcích. V interním prvku GridView poznámky k řádku, který je upravitelný pomocí jeho [vlastnosti`EditIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx). Vzhledem k tomu, že prvek GridView je svázán se zdrojem dat, kontroluje každý řádek, aby bylo vidět, zda index řádku odpovídá hodnotě `EditIndex`. V takovém případě se pole s řádky vykreslují pomocí rozhraní pro úpravy. Pro BoundFields rozhraní pro úpravy je textové pole, jehož vlastnost `Text` je přiřazena hodnota datového pole zadaného vlastností vlastnost BoundField s `DataField`. U TemplateField jsou `EditItemTemplate` použity místo `ItemTemplate`.

Pokud uživatel klikne na tlačítko pro úpravy řádku, odvoláte, aby se pracovní postup úpravy spustil. Tím dojde k postbacku, nastaví vlastnost GridView `EditIndex` na indexovaná řádková řádku a znovu sváže data s mřížkou. Při kliknutí na tlačítko Storno řádku se při postbacku `EditIndex` nastaví na hodnotu `-1` před tím, než se data znovu naváže k mřížce. Vzhledem k tomu, že řádky GridView s začínají indexování nulou, nastavení `EditIndex` pro `-1` má vliv na zobrazení prvku GridView v režimu jen pro čtení.

Vlastnost `EditIndex` pracuje dobře u úprav pro jednotlivé řádky, ale není navržena pro dávkové úpravy. Aby bylo možné celý prvek GridView upravovat, musíme mít každý řádek vykreslený pomocí rozhraní pro úpravy. Nejjednodušší způsob, jak to provést, je vytvořit, kde je každé upravitelné pole implementováno jako TemplateField s jeho rozhraním pro úpravy definované v `ItemTemplate`.

V několika dalších krocích vytvoříme kompletně upravitelnou GridView. V kroku 1 začneme vytvořením prvku GridView a jeho prvku ObjectDataSource a převedeme své BoundFields a třídě CheckBoxField podporována na TemplateFields. V krocích 2 a 3 přesunete rozhraní pro úpravy z vlastností TemplateField `EditItemTemplate` s na jejich `ItemTemplate` s.

## <a name="step-1-displaying-product-information"></a>Krok 1: zobrazení informací o produktu

Předtím, než se obáváme o vytvoření prvku GridView, kde jsou řádky editovatelné, nechte začít pouhým zobrazením informací o produktu. Otevřete stránku `BatchUpdate.aspx` ve složce `BatchData` a přetáhněte prvek GridView z panelu nástrojů do návrháře. Nastavte `ID` prvku GridView s `ProductsGrid` a ze své inteligentní značky vyberte možnost svázání s novým prvkem ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby načetl jeho data z metody `ProductsBLL` třídy s `GetProducts`.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLL](batch-updating-cs/_static/image2.gif)](batch-updating-cs/_static/image3.png)

**Obrázek 2**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](batch-updating-cs/_static/image4.png))

[![načíst data produktu pomocí metody GetProducts](batch-updating-cs/_static/image3.gif)](batch-updating-cs/_static/image5.png)

**Obrázek 3**: načtení dat produktu pomocí metody `GetProducts` ([kliknutím zobrazíte obrázek v plné velikosti](batch-updating-cs/_static/image6.png))

Podobně jako v prvku GridView jsou funkce úprav ObjectDataSource s navrženy pro práci na jednotlivých řádcích. Aby bylo možné aktualizovat sadu záznamů, je nutné zapsat bitovou kopii kódu do třídy ASP.NET stránky s kódem na pozadí, která data zabalí a předává je do knihoven BLL. Proto nastavte rozevírací seznamy v rámci karet ObjectDataSource s aktualizace, vložit a odstranit na (žádné). Kliknutím na Dokončit dokončete průvodce.

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](batch-updating-cs/_static/image4.gif)](batch-updating-cs/_static/image7.png)

**Obrázek 4**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti).](batch-updating-cs/_static/image8.png)

Po dokončení Průvodce konfigurací zdroje dat by deklarativní označení ObjectDataSource s mělo vypadat takto:

[!code-aspx[Main](batch-updating-cs/samples/sample1.aspx)]

Dokončení Průvodce konfigurací zdroje dat také způsobí, že Visual Studio vytvoří BoundFields a třídě CheckBoxField podporována pro pole dat produktu v prvku GridView. V tomto kurzu umožníte uživateli zobrazit a upravit jenom název produktu, kategorii, cenu a ukončený stav. Odeberte všechna pole s výjimkou `ProductName`, `CategoryName`, `UnitPrice`a `Discontinued` a přejmenujte `HeaderText` vlastnosti prvních tří polí na produkt, kategorii a cenu. Nakonec zaškrtněte políčka Povolit stránkování a Povolit řazení v inteligentní značce GridView s.

V tomto okamžiku má prvek GridView tři BoundFields (`ProductName`, `CategoryName`a `UnitPrice`) a třídě CheckBoxField podporována (`Discontinued`). Musíme převést tato čtyři pole na pole TemplateField a pak přesunout rozhraní pro úpravy z `EditItemTemplate` TemplateField s na jeho `ItemTemplate`.

> [!NOTE]
> Prozkoumali jsme vytváření a přizpůsobení vlastností TemplateField v kurzu [přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) . Provedeme vás kroky převodu BoundFields a třídě CheckBoxField podporována na TemplateFields a definování jejich rozhraní pro úpravy ve svých `ItemTemplate`ech, ale pokud se dostanete k zablokování nebo potřebujete aktualizační program, nemusíte váhají, abyste se mohli vrátit k předchozímu kurzu.

Z inteligentní značky GridView s klikněte na odkaz Upravit sloupce a otevřete dialogové okno pole. Potom vyberte jednotlivá pole a klikněte na tlačítko převést toto pole na odkaz TemplateField.

![Převést existující BoundFields a třídě CheckBoxField podporována na TemplateField](batch-updating-cs/_static/image5.gif)

**Obrázek 5**: převod existujících BoundFields a třídě CheckBoxField podporována na TemplateField

Teď, když je každé pole TemplateField, jsme připraveni přesunout rozhraní pro úpravy z `EditItemTemplate` s na `ItemTemplate` s.

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>Krok 2: vytvoření rozhraní pro úpravy`ProductName`,`UnitPrice`a`Discontinued`

Vytváření `ProductName`, `UnitPrice`a `Discontinued`ch editačních rozhraní jsou témata tohoto kroku a jsou poměrně jednoduchá, protože každé rozhraní je již definováno v `EditItemTemplate`TemplateField. Vytvoření rozhraní pro úpravy `CategoryName` je trochu důležitější, protože musíme vytvořit DropDownList příslušných kategorií. Toto `CategoryName` pro úpravu rozhraní se používá v kroku 3.

Pojďme začít s `ProductName` TemplateField. Klikněte na odkaz Upravit šablony z inteligentní značky GridView s a přejděte k podrobnostem `ProductName` TemplateField s `EditItemTemplate`. Vyberte textové pole, zkopírujte ho do schránky a vložte ho do `ProductName` TemplateField `ItemTemplate`. Změňte vlastnost TextBox s `ID` na `ProductName`.

Dále přidejte RequiredFieldValidator do `ItemTemplate`, abyste zajistili, že uživatel zadá hodnotu pro každý název produktu. Nastavte vlastnost `ControlToValidate` na NázevVýrobku. vlastnost `ErrorMessage` na ni musíte zadat název produktu. a vlastnost `Text` pro \*. Po provedení těchto přidání do `ItemTemplate`by vaše obrazovka měla vypadat podobně jako na obrázku 6.

[![NázevVýrobku TemplateField nyní obsahuje textové pole a RequiredFieldValidator](batch-updating-cs/_static/image6.gif)](batch-updating-cs/_static/image9.png)

**Obrázek 6**: `ProductName` TemplateField teď obsahuje textové pole a RequiredFieldValidator ([kliknutím zobrazíte obrázek v plné velikosti).](batch-updating-cs/_static/image10.png)

Pro rozhraní `UnitPrice` pro úpravy Začněte tím, že zkopírujete textové pole z `EditItemTemplate` do `ItemTemplate`. Dále umístěte do textového pole $ před a nastavte jeho vlastnost `ID` na hodnotu UnitPrice a vlastnost `Columns` na hodnotu 8.

Přidejte také CompareValidator do `ItemTemplate` `UnitPrice` s, abyste zajistili, že hodnota zadaná uživatelem je platná hodnota měny větší nebo rovna $0,00. Nastavte vlastnost validátoru `ControlToValidate` na hodnotu UnitPrice. vlastnost `ErrorMessage` na hodnotu, kterou musíte zadat platnou hodnotu měny. Vynechejte prosím všechny symboly měn., vlastnost `Text` \*, jeho vlastnost `Type` na `Currency`, jeho vlastnost `Operator` `GreaterThanEqual`a jeho vlastnost `ValueToCompare` na hodnotu 0.

[![přidat CompareValidator, aby se zajistilo, že zadaná cena je nezáporná hodnota měny.](batch-updating-cs/_static/image7.gif)](batch-updating-cs/_static/image11.png)

**Obrázek 7**: přidejte CompareValidator, abyste zajistili, že zadaná cena je nezáporná hodnota měny ([kliknutím zobrazíte obrázek v plné velikosti).](batch-updating-cs/_static/image12.png)

Pro `Discontinued` TemplateField můžete použít zaškrtávací políčko již definované v `ItemTemplate`. Jednoduše nastavte jeho `ID` na ukončeno a jeho vlastnost `Enabled` na `true`.

## <a name="step-3-creating-thecategorynameediting-interface"></a>Krok 3: vytvoření rozhraní pro úpravy`CategoryName`

Rozhraní pro úpravy v `CategoryName` TemplateField s `EditItemTemplate` obsahuje textové pole, které zobrazuje hodnotu `CategoryName` dat. Musíme to nahradit ovládacím prvkem DropDownList, který obsahuje seznam možných kategorií.

> [!NOTE]
> V kurzu [přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) je podrobnější a kompletní diskuzi o přizpůsobení šablony, která obsahuje DropDownList, a to na rozdíl od textového pole. I když jsou tyto kroky dokončené, zobrazí se tersely. Podrobnější pohled na vytváření a konfiguraci ovládacích prvků kategorie DropDownList najdete v kurzu [přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) .

Přetáhněte objekt DropDownList z panelu nástrojů na `CategoryName` TemplateField s `ItemTemplate`a nastavte jeho `ID` na `Categories`. V tomto okamžiku by byl obvykle definován zdroj dat DropDownList s pomocí inteligentní značky a vytvoření nového prvku ObjectDataSource. To však přidá prvek ObjectDataSource v rámci `ItemTemplate`, což způsobí, že bude vytvořena instance ObjectDataSource pro každý řádek prvku GridView. Místo toho je možné vytvořit prvek ObjectDataSource mimo prvky GridView s prvky TemplateField. Ukončete úpravu šablony a přetáhněte prvek ObjectDataSource z panelu nástrojů do návrháře pod `ProductsDataSource` ObjectDataSource. Pojmenujte novou `CategoriesDataSource` ObjectDataSource a nakonfigurujte ji tak, aby používala metodu `GetCategories` `CategoriesBLL` třídy s.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu CategoriesBLL](batch-updating-cs/_static/image8.gif)](batch-updating-cs/_static/image13.png)

**Obrázek 8**: Konfigurace prvku ObjectDataSource, aby používal třídu `CategoriesBLL` ([kliknutím zobrazíte obrázek v plné velikosti](batch-updating-cs/_static/image14.png))

[![načíst data kategorie pomocí metody GetCategories](batch-updating-cs/_static/image9.gif)](batch-updating-cs/_static/image15.png)

**Obrázek 9**: načtení dat kategorie pomocí metody `GetCategories` ([kliknutím zobrazíte obrázek v plné velikosti](batch-updating-cs/_static/image16.png))

Vzhledem k tomu, že je tento prvek ObjectDataSource použit pouze k načtení dat, nastavte rozevírací seznamy na kartách aktualizovat a odstranit na hodnotu (žádné). Kliknutím na Dokončit dokončete průvodce.

[![nastavení rozevíracích seznamů na kartách aktualizovat a odstranit na (žádné)](batch-updating-cs/_static/image10.gif)](batch-updating-cs/_static/image17.png)

**Obrázek 10**: nastavení rozevíracích seznamů na kartách aktualizovat a odstranit na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti).](batch-updating-cs/_static/image18.png)

Po dokončení průvodce by deklarativní označení `CategoriesDataSource` s mělo vypadat takto:

[!code-aspx[Main](batch-updating-cs/samples/sample2.aspx)]

Po vytvoření a konfiguraci `CategoriesDataSource` se vraťte do `CategoryName` TemplateField `ItemTemplate` a v inteligentní značce DropDownList klikněte na odkaz zvolit zdroj dat. V Průvodci konfigurací zdroje dat vyberte v prvním rozevíracím seznamu možnost `CategoriesDataSource` a zvolte, že chcete `CategoryName` použít pro zobrazení a `CategoryID` jako hodnotu.

[![vazby ovládacího prvkem DropDownList na CategoriesDataSource](batch-updating-cs/_static/image11.gif)](batch-updating-cs/_static/image19.png)

**Obrázek 11**: Svázání ovládacího prvkem DropDownList s `CategoriesDataSource`em ([kliknutím zobrazíte obrázek v plné velikosti](batch-updating-cs/_static/image20.png))

V tomto okamžiku `Categories` DropDownList zobrazí seznam všech kategorií, ale zatím nevybere odpovídající kategorii pro produkt vázaný na řádek GridView. Abychom to dosáhli, je potřeba nastavit `Categories` DropDownList s `SelectedValue` na hodnotu `CategoryID` produktu s produktem. Klikněte na odkaz Upravit datové vazby z inteligentní značky DropDownList s a přidružte vlastnost `SelectedValue` k datovému poli `CategoryID`, jak je znázorněno na obrázku 12.

![Vytvořit vazby hodnoty KódKategorie produktu s vlastností DropDownList s SelectedValue](batch-updating-cs/_static/image12.gif)

**Obrázek 12**: svázání hodnoty `CategoryID` produktů s vlastností DropDownList s `SelectedValue`

Jeden poslední problém zůstává: Pokud produkt nemá `CategoryID` zadanou hodnotu, výsledkem příkazu DataBinding na `SelectedValue` bude výjimka. Důvodem je skutečnost, že ovládací prvek DropDownList obsahuje pouze položky pro kategorie a nenabízí možnost pro tyto produkty, které mají `NULL` hodnotu databáze pro `CategoryID`. Chcete-li tento problém napravit, nastavte vlastnost `AppendDataBoundItems` DropDownList na `true` a přidejte novou položku do ovládacího prvků DropDownList, vynechejte vlastnost `Value` z deklarativní syntaxe. Proto se ujistěte, že deklarativní syntaxe `Categories` DropDownList s vypadá takto:

[!code-aspx[Main](batch-updating-cs/samples/sample3.aspx)]

Všimněte si, jak `<asp:ListItem Value="">` – vybrat jeden – má jeho `Value` atribut explicitně nastaven na prázdný řetězec. Přečtěte si kurz [přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) pro podrobnější diskuzi o tom, proč je tato další položka DropDownList potřebná pro zpracování `NULL`ho případu a proč je nutné přiřadit vlastnost `Value` prázdnému řetězci.

> [!NOTE]
> Tady je potenciální problém s výkonem a škálovatelností, které je potřeba zmínit. Vzhledem k tomu, že každý řádek má ovládací prvek DropDownList, který používá `CategoriesDataSource` jako zdroj dat, metoda `CategoriesBLL` třídy `GetCategories` se zavolá *n* krát na stránku, kde *n* je počet řádků v prvku GridView. Tato *n* volání `GetCategories` mají za následek *n* dotazů na databázi. Tento dopad na databázi může být slabší ukládáním do mezipaměti vrácených kategorií, a to buď v mezipaměti pro požadavky, nebo přes vrstvu ukládání do mezipaměti s využitím závislosti mezipaměti SQL nebo velmi krátké doby platnosti. Další informace o možnosti ukládání do mezipaměti pro jednotlivé požadavky najdete v tématu [`HttpContext.Items` úložiště mezipaměti pro žádosti](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx).

## <a name="step-4-completing-the-editing-interface"></a>Krok 4: dokončení rozhraní pro úpravy

Provedli jsme několik změn v šablonách GridView, aniž by bylo nutné se pozastavit, aby se zobrazil náš pokrok. Chvilku si můžete prohlédnout v prohlížeči. Jak ukazuje obrázek 13, jednotlivé řádky jsou vykresleny pomocí `ItemTemplate`, který obsahuje rozhraní pro úpravu buňky s buňkami.

[![každý řádek prvku GridView je upravitelný](batch-updating-cs/_static/image13.gif)](batch-updating-cs/_static/image21.png)

**Obrázek 13**: každý řádek prvku GridView je upravitelný ([kliknutím zobrazíte obrázek v plné velikosti](batch-updating-cs/_static/image22.png)).

K dispozici je několik menších potíží s formátováním, které by se v této fázi měli postarat. Nejdříve si všimněte, že hodnota `UnitPrice` obsahuje čtyři desetinná místa. Chcete-li tento problém vyřešit, vraťte se do `UnitPrice` TemplateField s `ItemTemplate` a z inteligentní značky TextBox s klikněte na odkaz Upravit datové vazby. Dále určete, že vlastnost `Text` má být formátována jako číslo.

![Naformátovat vlastnost text jako číslo](batch-updating-cs/_static/image14.gif)

**Obrázek 14**: naformátování vlastnosti `Text` jako čísla

Za druhé zařaďte zaškrtávací políčko ve sloupci `Discontinued` (místo toho, aby se zarovnalo doleva). Klikněte na Upravit sloupce z inteligentní značky GridView s a vyberte `Discontinued` TemplateField ze seznamu polí v levém dolním rohu. Přejděte k podrobnostem `ItemStyle` a nastavte vlastnost `HorizontalAlign` na střed, jak je znázorněno na obrázku 15.

![Vycentrovat zaškrtávací políčko, které je ukončeno](batch-updating-cs/_static/image15.gif)

**Obrázek 15**: prostřední zaškrtávací políčko `Discontinued`

Dále do stránky přidejte ovládací prvek ovládací souhrnu ověření a nastavte jeho vlastnost `ShowMessageBox` na `true` a jeho vlastnost `ShowSummary` na `false`. Přidejte také webové ovládací prvky tlačítko, které při kliknutí aktualizují změny uživatele. Konkrétně přidejte dvě webové ovládací prvky tlačítko, jednu nad prvek GridView a jednu nad ním, nastavením obou ovládacích prvků `Text` vlastnosti pro aktualizaci produktů.

Vzhledem k tomu, že rozhraní pro úpravy GridView s je definované ve svých TemplateFieldch `ItemTemplate` s, `EditItemTemplate` s je nadbytečný a může být odstraněno.

Po provedení výše zmíněných změn formátování, přidání ovládacích prvků tlačítko a odebrání zbytečných `EditItemTemplate` s, by vaše deklarativní syntaxe stránky měla vypadat takto:

[!code-aspx[Main](batch-updating-cs/samples/sample4.aspx)]

Obrázek 16 znázorňuje tuto stránku při prohlížení přes prohlížeč po přidání webového ovládacího prvku tlačítka a provedené změny formátování.

[![stránka teď obsahuje dvě tlačítka pro aktualizaci produktů.](batch-updating-cs/_static/image16.gif)](batch-updating-cs/_static/image23.png)

**Obrázek 16**: stránka teď obsahuje dvě tlačítka pro aktualizaci produktů ([kliknutím zobrazíte obrázek v plné velikosti).](batch-updating-cs/_static/image24.png)

## <a name="step-5-updating-the-products"></a>Krok 5: aktualizace produktů

Když uživatel navštíví tuto stránku, provede změny a potom klikněte na jedno z těchto dvou tlačítek pro aktualizaci produktů. V tomto bodě musíme nějakým způsobem Uložit uživatelem zadané hodnoty pro každý řádek do instance `ProductsDataTable` a pak předat metodu knihoven BLL, která pak předává tuto `ProductsDataTable` instanci do metody DAL s `UpdateWithTransaction`. Metoda `UpdateWithTransaction`, kterou jsme vytvořili v [předchozím kurzu](wrapping-database-modifications-within-a-transaction-cs.md), zajišťuje, že dávka změn bude aktualizována jako atomická operace.

Vytvořte metodu s názvem `BatchUpdate` v `BatchUpdate.aspx.cs` a přidejte následující kód:

[!code-csharp[Main](batch-updating-cs/samples/sample5.cs)]

Tato metoda začíná tím, že získá všechny produkty zpátky v `ProductsDataTable` prostřednictvím volání metody `GetProducts` knihoven BLL s. Potom vytvoří výčet [`Rows` kolekce](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)`ProductGrid` GridView. Kolekce `Rows` obsahuje [instanci`GridViewRow`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx) pro každý řádek zobrazený v prvku GridView. Vzhledem k tomu, že se zobrazuje maximálně deset řádků na stránce, nebude mít `Rows` kolekce GridViews více než deset položek.

Pro každý řádek je `ProductID` převzata z kolekce `DataKeys` a v `ProductsDataTable`je vybrána příslušná `ProductsRow`. Na čtyři vstupní ovládací prvky TemplateField jsou programově odkazovány a jejich hodnoty jsou přiřazeny vlastnostem `ProductsRow` instance s. Po použití hodnot jednotlivých řádků GridView a k aktualizaci `ProductsDataTable`je předána metodě knihoven BLL s `UpdateWithTransaction`, která, jak jsme viděli v předchozím kurzu, jednoduše zavolá do metody DAL s `UpdateWithTransaction`.

Algoritmus dávkové aktualizace použitý pro účely tohoto kurzu aktualizuje každý řádek v `ProductsDataTable`, který odpovídá řádku v prvku GridView, bez ohledu na to, zda byly informace o produktu změněny. I když tyto nevidomé aktualizace většinou nedochází k problémům s výkonem, můžou vést k nadbytečným záznamům, pokud převedete změny auditování v tabulce databáze. Zpět v kurzu [provádění dávkových aktualizací](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md) jsme prozkoumali, že služba Batch aktualizuje rozhraní pomocí prvku DataList a přidala kód, který by aktualizoval pouze ty záznamy, které byly ve skutečnosti změněny uživatelem. Využijte techniky od [aktualizace služby Batch](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md) k aktualizaci kódu v tomto kurzu, pokud je to potřeba.

> [!NOTE]
> Při navázání zdroje dat na prvek GridView pomocí inteligentní značky Visual Studio automaticky přiřadí hodnoty primárního klíče zdroje dat k vlastnosti GridView `DataKeyNames`. Pokud jste prvek ObjectDataSource nevytvořili v prvku GridView pomocí inteligentní značky GridView s, jak je uvedeno v kroku 1, bude nutné ručně nastavit vlastnost GridView `DataKeyNames` na ProductID, aby bylo možné získat přístup k hodnotě `ProductID` pro každý řádek prostřednictvím kolekce `DataKeys`.

Kód používaný v `BatchUpdate` je podobný tomu, který se používá v metodách `UpdateProduct` knihoven BLL s, hlavní rozdíl spočívá v tom, že v `UpdateProduct`ch metodách je z architektury načtena pouze jedna instance `ProductRow`. Kód, který přiřazuje vlastnosti `ProductRow`, je stejný mezi metodami `UpdateProducts` a kódem v rámci `foreach` smyčky v `BatchUpdate`, jako je to celkový vzor.

K dokončení tohoto kurzu musíme mít při kliknutí na tlačítko Aktualizovat produkty vyvolanou metodu `BatchUpdate`. Vytvořte obslužné rutiny události pro `Click` události těchto dvou ovládacích prvků tlačítko a přidejte následující kód do obslužných rutin událostí:

[!code-csharp[Main](batch-updating-cs/samples/sample6.cs)]

Nejprve bude provedeno volání `BatchUpdate`. V dalším kroku se `ClientScript property` použít k vložení JavaScriptu, který zobrazí MessageBox, který čte produkty, které byly aktualizovány.

Vyzkoušejte si test tohoto kódu minutou. Navštivte `BatchUpdate.aspx` v prohlížeči, upravte počet řádků a klikněte na jedno z tlačítek pro aktualizaci produktů. Za předpokladu, že nejsou k dispozici žádné chyby ověřování, měli byste vidět MessageBox, který čte produkty. K ověření atomické aktualizace zvažte přidání omezení náhodného `CHECK`, jako je, které nepovoluje `UnitPrice` hodnoty 1234,56. Pak z `BatchUpdate.aspx`upravte několik záznamů a nezapomeňte nastavit jednu z `UnitPrice` hodnoty produktu na zakázanou hodnotu (1234,56). To by mělo mít za následek chybu, když kliknete na aktualizovat produkty s ostatními změnami během této dávkové operace zpátky na původní hodnoty.

## <a name="an-alternativebatchupdatemethod"></a>Alternativní metoda`BatchUpdate`

Metoda `BatchUpdate`, kterou jsme právě zkontrolovali, načte *všechny* produkty z metody `GetProducts` knihoven BLL s a pak aktualizuje pouze ty záznamy, které se zobrazí v prvku GridView. Tento přístup je ideální, pokud GridView nepoužívá stránkování, ale pokud k tomu dojde, může to být stovky, tisíce nebo desítky tisíců produktů, ale pouze deset řádků v prvku GridView. V takovém případě jsou všechny produkty z databáze pouze pro úpravu 10 z nich méně, než je ideální.

Pro tyto typy situací zvažte místo toho použití následující metody `BatchUpdateAlternate`:

[!code-csharp[Main](batch-updating-cs/samples/sample7.cs)]

`BatchMethodAlternate` spustí vytvořením nového prázdného `ProductsDataTable` s názvem `products`. Pak kroky prostřednictvím kolekce `Rows` GridView. a pro každý řádek získá konkrétní informace o produktu pomocí metody `GetProductByProductID(productID)` knihoven BLL s. Načtená `ProductsRow` instance má své vlastnosti aktualizované stejným způsobem jako `BatchUpdate`, ale po aktualizaci řádku, který je importován do `products``ProductsDataTable` prostřednictvím [metody`ImportRow(DataRow)`](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)DataTable s.

Po dokončení smyčky `foreach` `products` obsahuje jednu instanci `ProductsRow` pro každý řádek v prvku GridView. Vzhledem k tomu, že se každá z `ProductsRow` instancí přidala do `products` (místo aktualizace), pokud je do metody `UpdateWithTransaction` znovu předána, `ProductsTableAdapter` se pokusí vložit každý záznam do databáze. Místo toho je potřeba určit, že se všechny tyto řádky změnily (nepřidalo se).

To lze provést přidáním nové metody do knihoven BLL s názvem `UpdateProductsWithTransaction`. `UpdateProductsWithTransaction`, zobrazené níže, nastaví `RowState` každé z `ProductsRow` instancí v `ProductsDataTable` na `Modified` a pak předá `ProductsDataTable` metodě DAL s `UpdateWithTransaction`.

[!code-csharp[Main](batch-updating-cs/samples/sample8.cs)]

## <a name="summary"></a>Přehled

Prvek GridView poskytuje integrované možnosti pro úpravu pro jednotlivé řádky, ale neobsahuje podporu pro vytváření plně upravitelných rozhraní. Jak jsme viděli v tomto kurzu, taková rozhraní jsou možná, ale vyžaduje práci. Chcete-li vytvořit prvek GridView, kde je každý řádek upravitelný, je nutné převést pole GridView s na TemplateFields a definovat rozhraní pro úpravy v rámci `ItemTemplate` s. Kromě toho musí být na stránku přidány webové ovládací prvky tlačítka aktualizovat všechny typy, oddělené od prvku GridView. Tato tlačítka `Click` obslužných rutin událostí musí vytvořit výčet `Rows` kolekce GridView, uložit změny v `ProductsDataTable`a předat aktualizované informace do příslušné metody knihoven BLL.

V dalším kurzu se dozvíte, jak vytvořit rozhraní pro odstranění dávky. Konkrétně jednotlivé řádky prvku GridView budou obsahovat zaškrtávací políčko a místo toho, aby obsahovali tlačítka aktualizovat všechny typy, budou k dispozici tlačítka pro odstranění vybraných řádků.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Teresa Murphy a David Suru. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](wrapping-database-modifications-within-a-transaction-cs.md)
> [Další](batch-deleting-cs.md)
