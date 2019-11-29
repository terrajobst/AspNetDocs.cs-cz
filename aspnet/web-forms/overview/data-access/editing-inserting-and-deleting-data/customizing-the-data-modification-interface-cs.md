---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs
title: Přizpůsobení rozhraní pro úpravu dat (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na postup přizpůsobení rozhraní upravitelného prvku GridView tím, že nahradíte standardní textové pole a zaškrtávací políčko pomocí alternujících prvků...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 22e99600-8d18-4a94-a20e-a3a62bb63798
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: af68d1a0b744a2c1fd9d21a8bf6165bafa4de683
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74624231"
---
# <a name="customizing-the-data-modification-interface-c"></a>Přizpůsobení rozhraní pro úpravu dat (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_CS.exe) nebo [Stáhnout PDF](customizing-the-data-modification-interface-cs/_static/datatutorial20cs1.pdf)

> V tomto kurzu se podíváme na postup přizpůsobení rozhraní upravitelného prvku GridView tím, že nahradíte standardní textové ovládací prvky a ovládací prvky CheckBox s alternativním zadáním.

## <a name="introduction"></a>Úvod

BoundFields a CheckBoxFields, které používají ovládací prvky GridView a DetailsView, zjednodušují proces úpravy dat z důvodu jejich schopnosti vykreslovat rozhraní jen pro čtení, upravitelná a vložená rozhraní. Tato rozhraní lze vykreslit bez nutnosti přidávat další deklarativní označení nebo kód. Rozhraní vlastnost BoundField a třídě CheckBoxField podporována ale nemají v reálných scénářích často potřebnou možnost úprav. Aby bylo možné přizpůsobit upravitelné nebo vkládané rozhraní v prvku GridView nebo DetailsView, je nutné místo toho použít TemplateField.

V [předchozím kurzu](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) jsme viděli, jak přizpůsobit rozhraní pro úpravu dat přidáním ověřovacích webových ovládacích prvků. V tomto kurzu se podíváme na to, jak přizpůsobit skutečné webové ovládací prvky pro shromažďování dat, které nahradí standardní textové pole vlastnost BoundField a třídě CheckBoxField podporována a ovládací prvky CheckBox s alternativním vstupním webovým ovládacím prvkům. Konkrétně sestavíme upravitelný prvek GridView, který umožňuje aktualizovat název, kategorii, dodavatele a zastavený stav produktu. Při úpravách konkrétního řádku se pole kategorie a dodavatel vykreslí jako DropDownList, které obsahují sadu dostupných kategorií a dodavatelů, ze kterých si můžete vybrat. Kromě toho nahradíme výchozí zaškrtávací políčko třídě CheckBoxField podporována ovládacím prvkem RadioButtonList, který nabízí dvě možnosti: "aktivní" a "ukončeno".

[![rozhraní pro úpravy prvku GridView obsahuje DropDownList a RadioButton](customizing-the-data-modification-interface-cs/_static/image2.png)](customizing-the-data-modification-interface-cs/_static/image1.png)

**Obrázek 1**: rozhraní pro úpravy ovládacího prvku GridView zahrnuje DropDownList a RadioButton ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-data-modification-interface-cs/_static/image3.png)

## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>Krok 1: vytvoření příslušného přetížení`UpdateProduct`

V tomto kurzu vytvoříme upravitelný prvek GridView, který umožňuje úpravu názvu, kategorie, dodavatele a ukončeného stavu produktu. Proto musíme `UpdateProduct` přetížení, které přijímá pět vstupních parametrů těchto čtyř hodnot produktu a `ProductID`. Stejně jako v předchozích přetíženích to bude:

1. Načíst informace o produktu z databáze pro zadanou `ProductID`,
2. Aktualizujte pole `ProductName`, `CategoryID`, `SupplierID`a `Discontinued` a
3. Odešlete žádost o aktualizaci na DAL prostřednictvím metody `Update()` TableAdapter.

Pro zkrácení se pro toto konkrétní přetížení přestala kontrolovat obchodní pravidlo, že produkt označený jako vyřazený není jediným produktem, který nabízí jeho dodavatel. Nebojte se přidat v případě, že dáváte přednost nebo, v ideálním případě refaktorujte logiku pro samostatnou metodu.

Následující kód ukazuje nové přetížení `UpdateProduct` ve třídě `ProductsBLL`:

[!code-csharp[Main](customizing-the-data-modification-interface-cs/samples/sample1.cs)]

## <a name="step-2-crafting-the-editable-gridview"></a>Krok 2: vytvoření upravitelného prvku GridView

S přidaným přetížením `UpdateProduct` jsme připraveni vytvořit náš upravitelný prvek GridView. Otevřete stránku `CustomizedUI.aspx` ve složce `EditInsertDelete` a přidejte ovládací prvek GridView do návrháře. Dále vytvořte nový prvek ObjectDataSource z inteligentní značky prvku GridView. Nakonfigurujte prvek ObjectDataSource pro načtení informací o produktu prostřednictvím metody `GetProducts()` `ProductBLL` třídy a k aktualizaci dat produktu pomocí `UpdateProduct` přetížení, které jsme právě vytvořili. Z rozevíracích seznamů na kartách vložit a odstranit vyberte (žádné).

[![nakonfigurovat prvek ObjectDataSource na použití právě vytvořeného přetížení UpdateProduct](customizing-the-data-modification-interface-cs/_static/image5.png)](customizing-the-data-modification-interface-cs/_static/image4.png)

**Obrázek 2**: Konfigurace prvku ObjectDataSource pro použití právě vytvořeného přetížení `UpdateProduct` ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image6.png))

Jak jsme viděli v kurzech pro úpravu dat, deklarativní syntaxe prvku ObjectDataSource vytvořeného v aplikaci Visual Studio přiřadí vlastnost `OldValuesParameterFormatString` k `original_{0}`. To samozřejmě nebude fungovat s naší vrstvou obchodní logiky, protože naše metody neočekávají původní `ProductID` hodnota, která se má předat. Proto vzhledem k tomu, že jsme provedli v předchozích kurzech, chvíli počkejte, než odeberete toto přiřazení vlastnosti z deklarativní syntaxe, nebo místo toho nastavte hodnotu této vlastnosti na `{0}`.

Po této změně by deklarativní označení prvku ObjectDataSource mělo vypadat takto:

[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample2.aspx)]

Všimněte si, že vlastnost `OldValuesParameterFormatString` byla odebrána a že `Parameter` v kolekci `UpdateParameters` pro každý ze vstupních parametrů, který očekával náš `UpdateProduct` přetížení.

I když je prvek ObjectDataSource nakonfigurován tak, aby aktualizoval pouze podmnožinu hodnot produktů, prvek GridView aktuálně zobrazuje *všechna* pole produktu. Pro úpravu prvku GridView chvíli počkejte, aby:

- Zahrnuje to jenom `ProductName`, `SupplierName`, `CategoryName` BoundFields a `Discontinued` třídě CheckBoxField podporována.
- Pole `CategoryName` a `SupplierName`, která se mají zobrazit před (vlevo od) `Discontinued` třídě CheckBoxField podporována
- Vlastnost `HeaderText` `CategoryName` a `SupplierName` BoundFields je nastavená na kategorie a dodavatel (v uvedeném pořadí).
- Podpora úprav je povolena (zaškrtněte políčko Povolit úpravy v inteligentní značce prvku GridView)

Po těchto změnách bude Návrhář vypadat podobně jako obrázek 3 s deklarativní syntaxí prvku GridView zobrazenou níže.

[![odebrat nepotřebná pole z prvku GridView.](customizing-the-data-modification-interface-cs/_static/image8.png)](customizing-the-data-modification-interface-cs/_static/image7.png)

**Obrázek 3**: Odebrání nepotřebných polí z prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image9.png))

[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample3.aspx)]

V tomto okamžiku je chování prvku GridView jen pro čtení dokončeno. Při prohlížení dat se každý produkt vykresluje jako řádek v prvku GridView a zobrazuje název produktu, kategorii, dodavatele a ukončený stav.

[![rozhraní pouze pro čtení prvku GridView je dokončeno.](customizing-the-data-modification-interface-cs/_static/image11.png)](customizing-the-data-modification-interface-cs/_static/image10.png)

**Obrázek 4**: rozhraní pouze pro čtení prvku GridView je dokončeno ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image12.png)).

> [!NOTE]
> Jak je popsáno v článku [kurz vkládání, aktualizace a odstraňování dat](an-overview-of-inserting-updating-and-deleting-data-cs.md), je důležité, aby byl povolen stav zobrazení GridView. (výchozí chování). Pokud nastavíte vlastnost `EnableViewState` prvku GridView s na hodnotu `false`, spustíte riziko, že neúmyslně odstraní nebo upraví záznamy v souběžných uživatelích. Viz [Upozornění: problém souběžnosti s ASP.NET 2,0 gridviews/DetailsView/formviews, které podporují úpravy a/nebo odstraňování a jejichž stav zobrazení je zakázán](http://scottonwriting.net/sowblog/posts/10054.aspx) pro další informace.

## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>Krok 3: použití ovládacího prvkem DropDownList pro rozhraní pro úpravy kategorie a dodavatele

Odvolat, že objekt `ProductsRow` obsahuje vlastnosti `CategoryID`, `CategoryName`, `SupplierID`a `SupplierName`, které poskytují skutečné hodnoty ID cizího klíče v tabulce databáze `Products` a odpovídající `Name` hodnoty v tabulkách `Categories` a `Suppliers`. `CategoryID` `ProductRow`a `SupplierID` lze číst z a zapisovat do, zatímco vlastnosti `CategoryName` a `SupplierName` jsou označeny jen pro čtení.

V důsledku stavu jen pro čtení `CategoryName` a `SupplierName` vlastností `ReadOnly` měla odpovídající BoundFields vlastnost nastavenou na `true`, aby se tyto hodnoty při úpravě řádku neměnily. I když můžeme nastavit vlastnost `ReadOnly` na hodnotu `false`a vykreslit `CategoryName` a `SupplierName` BoundFields jako textová pole během úprav, takový přístup bude mít za následek výjimku, když se uživatel pokusí produkt aktualizovat, protože neexistuje žádné `UpdateProduct` přetížení, které přebírá `CategoryName` a `SupplierName` vstupy. Ve skutečnosti nechci vytvořit takové přetížení ze dvou důvodů:

- `Products` tabulka neobsahuje pole `SupplierName` nebo `CategoryName`, ale `SupplierID` a `CategoryID`. Proto chceme, aby naše metoda předala tyto konkrétní hodnoty ID, nikoli hodnoty jejich vyhledávací tabulky.
- Vyžadování uživatele k zadání názvu dodavatele nebo kategorie je menší než ideální, protože vyžaduje, aby uživatel znal dostupné kategorie a dodavatelé a jejich správné pravopisné názvy.

V polích dodavatel a kategorie by se měla zobrazovat jména kategorií a dodavatelů v režimu jen pro čtení (stejně jako v současné době) a v rozevíracím seznamu odpovídajících možností při úpravách. Pomocí rozevíracího seznamu může koncový uživatel rychle zjistit, jaké kategorie a dodavatelé jsou k dispozici pro výběr, a může snadněji vytvořit jejich výběr.

Pro poskytnutí tohoto chování musíme převést `SupplierName` a `CategoryName` BoundFields na TemplateFields, jejichž `ItemTemplate` emituje `SupplierName` a `CategoryName` hodnoty a jejichž `EditItemTemplate` používá ovládací prvek DropDownList k vypsání dostupných kategorií a dodavatelů.

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>Přidání`Categories`a`Suppliers`DropDownList

Začněte převodem `SupplierName` a `CategoryName` BoundFields na TemplateFields pomocí: kliknutí na odkaz Upravit sloupce z inteligentní značky GridView; Výběr vlastnost BoundField ze seznamu vlevo dole; a kliknutím na odkaz převést toto pole na TemplateField. Proces převodu vytvoří TemplateField pomocí `ItemTemplate` a `EditItemTemplate`, jak je znázorněno v deklarativní syntaxi níže:

[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample4.aspx)]

Vzhledem k tomu, že vlastnost BoundField byla označena jako jen pro čtení, obsahují `ItemTemplate` i `EditItemTemplate` webový ovládací prvek popisku, jehož vlastnost `Text` je svázána s příslušným datovým polem (`CategoryName`v syntaxi výše). Musíme upravit `EditItemTemplate`a nahradit webový ovládací prvek popisek ovládacím prvkem DropDownList.

Jak jsme viděli v předchozích kurzech, šablonu lze upravit pomocí návrháře nebo přímo z deklarativní syntaxe. Pokud ho chcete upravit pomocí návrháře, klikněte na odkaz Upravit šablony z inteligentní značky GridViewu a vyberte možnost pracovat s `EditItemTemplate`pole kategorie. Odeberte ovládací prvek web Label a nahraďte ho ovládacím prvkem DropDownList a nastavte vlastnost ID ovládacího prvku DropDownList na `Categories`.

[![odebrat TexBox a přidat DropDownList do EditItemTemplate](customizing-the-data-modification-interface-cs/_static/image14.png)](customizing-the-data-modification-interface-cs/_static/image13.png)

**Obrázek 5**: odebrání TexBox a přidání ovládacího prvkem DropDownList do `EditItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image15.png))

Dál je potřeba naplnit DropDownList pomocí dostupných kategorií. Klikněte na odkaz zvolit zdroj dat z inteligentní značky DropDownList a vyberte možnost vytvořit nový prvek ObjectDataSource s názvem `CategoriesDataSource`.

[![vytvořit nový ovládací prvek ObjectDataSource s názvem CategoriesDataSource](customizing-the-data-modification-interface-cs/_static/image17.png)](customizing-the-data-modification-interface-cs/_static/image16.png)

**Obrázek 6**: vytvoření nového ovládacího prvku ObjectDataSource s názvem `CategoriesDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image18.png))

Chcete-li, aby byl tento prvek ObjectDataSource vrácen do všech kategorií, připojte jej k metodě `GetCategories()` `CategoriesBLL` třídy.

[![sváže prvek ObjectDataSource s metodou GetCategories () CategoriesBLL.](customizing-the-data-modification-interface-cs/_static/image20.png)](customizing-the-data-modification-interface-cs/_static/image19.png)

**Obrázek 7**: Svázání prvku ObjectDataSource s metodou `GetCategories()` `CategoriesBLL`([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image21.png))

Nakonec nakonfigurujte nastavení ovládacího prvku DropDownList tak, aby pole `CategoryName` bylo zobrazeno v každé `ListItem` DropDownList s polem `CategoryID`, které se používá jako hodnota.

[![mít zobrazené pole CategoryName a KódKategorie použité jako hodnota](customizing-the-data-modification-interface-cs/_static/image23.png)](customizing-the-data-modification-interface-cs/_static/image22.png)

**Obrázek 8**: je zobrazeno pole `CategoryName` a `CategoryID` použito jako hodnota ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-data-modification-interface-cs/_static/image24.png)

Po provedení těchto změn deklarativní značky pro `EditItemTemplate` v `CategoryName` TemplateField budou zahrnovat ovládací prvek DropDownList i ObjectDataSource:

[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample5.aspx)]

> [!NOTE]
> Pro DropDownList v `EditItemTemplate` musí být povolený stav zobrazení. Brzy přidáme syntaxi datové vazby do deklarativní syntaxe ovládacího prvku DropDownList a příkazů DataBinding, jako je `Eval()` a `Bind()` se může vyskytovat pouze v ovládacích prvcích, jejichž stav zobrazení je povolen.

Zopakováním těchto kroků přidáte DropDownList s názvem `Suppliers` do `EditItemTemplate``SupplierName` TemplateField. To zahrnuje přidání ovládacího prvku DropDownList do `EditItemTemplate` a vytvoření jiného prvku ObjectDataSource. Prvek ObjectDataSource `Suppliers` DropDownList je však třeba nakonfigurovat tak, aby vyvolal metodu `GetSuppliers()` `SuppliersBLL` třídy. Kromě toho nakonfigurujte `Suppliers` DropDownList pro zobrazení pole `CompanyName` a použijte pole `SupplierID` jako hodnotu pro jeho `ListItem` s.

Po přidání ovládacích prvků DropDownList do dvou `EditItemTemplate` s načtěte stránku v prohlížeči a klikněte na tlačítko Upravit pro produkt Cajun pro sezónu Anton. Jak ukazuje obrázek 9, kategorie a sloupce dodavatelů produktu se vykreslují jako rozevírací seznamy obsahující dostupné kategorie a dodavatele, ze kterých si můžete vybrat. Všimněte si ale, že *první* položky v obou rozevíracích seznamech jsou ve výchozím nastavení vybrané (nápoje pro kategorii a exotické kapaliny jako dodavatel), a to i v případě, že je Cajun období systému Anton je koření dodávané novými Orleansy Cajun.

[![je první položka v rozevíracích seznamech standardně vybraná.](customizing-the-data-modification-interface-cs/_static/image26.png)](customizing-the-data-modification-interface-cs/_static/image25.png)

**Obrázek 9**: ve výchozím nastavení je vybraná první položka v rozevíracích seznamech ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-data-modification-interface-cs/_static/image27.png)

Pokud navíc kliknete na tlačítko Aktualizovat, zjistíte, že hodnoty `CategoryID` a `SupplierID` produktu jsou nastaveny na `NULL`. Obě tato nežádoucí chování jsou způsobena tím, že DropDownList v `EditItemTemplate` s nejsou vázány na žádná datová pole z podkladových dat produktu.

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>Svázání DropDownList s datovými poli`CategoryID`a`SupplierID`

Aby se rozevírací seznamy pro kategorie a dodavatele upravovaného produktu nastavily na příslušné hodnoty a aby se tyto hodnoty po kliknutí na aktualizovat vrátily zpátky do `UpdateProduct` metody knihoven BLL, potřebujeme vytvořit vazbu `SelectedValue`ch vlastností DropDownList na `CategoryID` a `SupplierID` datových polí pomocí obousměrné datové vazby. Chcete-li toho dosáhnout pomocí `Categories` DropDownList, můžete přidat `SelectedValue='<%# Bind("CategoryID") %>'` přímo do deklarativní syntaxe.

Alternativně můžete nastavit datové vazby ovládacího prvku DropDownList úpravou šablony prostřednictvím návrháře a kliknutím na odkaz Upravit datové vazby z inteligentní značky DropDownList. Dále určete, že vlastnost `SelectedValue` by měla být vázána na `CategoryID` pole pomocí obousměrné datové vazby (viz obrázek 10). Opakujte buď deklarativní, nebo proces návrháře, abyste navázali datové pole `SupplierID` na `Suppliers` DropDownList.

[![vytvořit vazbu KódKategorie s vlastností SelectedValue ovládacího prvku pro zobrazení dat pomocí obousměrné datové vazby](customizing-the-data-modification-interface-cs/_static/image29.png)](customizing-the-data-modification-interface-cs/_static/image28.png)

**Obrázek 10**: vytvoření vazby `CategoryID` k vlastnosti ovládacího `SelectedValue` prvku DropDownList pomocí obousměrné datové vazby ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image30.png))

Jakmile se vazby použijí na `SelectedValue` vlastnosti dvou DropDownList, budou se ve výchozím nastavení pro aktuální hodnoty produktu automaticky upravovat sloupce kategorie a dodavatelé upravovaného produktu. Po kliknutí na možnost aktualizovat budou hodnoty `CategoryID` a `SupplierID` vybrané položky rozevíracího seznamu předány metodě `UpdateProduct`. Obrázek 11 znázorňuje kurz po přidání příkazů DataBinding. Všimněte si, že vybrané položky rozevíracího seznamu pro Cajun pro Anton jsou správně koření a nové Orleans Cajun.

[![aktuální kategorie a hodnoty dodavatele upravovaného produktu, které jsou ve výchozím nastavení vybrané.](customizing-the-data-modification-interface-cs/_static/image32.png)](customizing-the-data-modification-interface-cs/_static/image31.png)

**Obrázek 11**: ve výchozím nastavení je vybrána aktuální kategorie a hodnoty dodavatele upravovaného produktu ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-data-modification-interface-cs/_static/image33.png)

## <a name="handlingnullvalues"></a>Zpracování hodnot`NULL`

Sloupce `CategoryID` a `SupplierID` v tabulce `Products` lze `NULL`, ale ovládací prvky DropDownList v `EditItemTemplate` neobsahují položku seznamu, která představuje `NULL` hodnotu. To má dvě důsledky:

- Uživatel nemůže použít naše rozhraní ke změně kategorie nebo dodavatele produktu z ne`NULL` hodnoty na `NULL` jednu.
- Pokud má produkt `NULL` `CategoryID` nebo `SupplierID`, kliknutí na tlačítko Upravit bude mít za následek výjimku. Důvodem je, že hodnota `NULL` vrácená pomocí `CategoryID` (nebo `SupplierID`) v příkazu `Bind()` není mapována na hodnotu v DropDownList (objekt DropDownList vyvolá výjimku, pokud je vlastnost `SelectedValue` nastavena na hodnotu, která *není* v kolekci položek seznamu).

Aby bylo možné podporovat `NULL` `CategoryID` a `SupplierID` hodnoty, musíme do každého DropDownList přidat další `ListItem`, které reprezentují `NULL` hodnota. V kurzu zobrazení [hlavního/podrobného filtru](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) v rámci DropDownList jsme viděli, jak přidat další `ListItem` k vlastnosti DropDownList vázaného na data, která se zabývá nastavením vlastnosti `AppendDataBoundItems` ovládacího prvku dropdownlist na `true` a ručním přidáním dalších `ListItem`. V tomto předchozím kurzu ale Přidali jsme `ListItem` s `Value` `-1`. Logika datové vazby v ASP.NET však automaticky převede prázdný řetězec na `NULL` hodnotu a naopak. Proto pro tento kurz chceme, aby `ListItem``Value` jako prázdný řetězec.

Začněte nastavením vlastnosti `AppendDataBoundItems` ovládacího prvek DropDownList na hodnotu `true`. Dále přidejte `NULL` `ListItem` přidáním následujícího elementu `<asp:ListItem>` do každého DropDownList, aby deklarativní označení vypadalo takto:

[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample6.aspx)]

Rozhodli jste se jako textovou hodnotu pro tento `ListItem`použít "(žádný)", ale pokud chcete, můžete ho změnit na i prázdný řetězec.

> [!NOTE]
> Jak jsme viděli v rámci *filtrování hlavního/podrobného dotazu pomocí ovládacího prvku DropDownList* , `ListItem` s lze přidat do ovládacího prvku DropDownList prostřednictvím návrháře kliknutím na vlastnost `Items` ovládacího prvku dropdownlist v okno vlastnosti (která zobrazí Editor kolekce `ListItem`). Nezapomeňte však přidat `ListItem` `NULL` pro tento kurz pomocí deklarativní syntaxe. Použijete-li Editor kolekce `ListItem`, vygenerovaná deklarativní syntaxe vynechá nastavení `Value` zcela v případě, že je přiřazen prázdný řetězec, čímž se vytvoří deklarativní označení jako: `<asp:ListItem>(None)</asp:ListItem>`. I když to může vypadat neškodně, chybějící hodnota způsobí, že DropDownList použije hodnotu vlastnosti `Text` na svém místě. To znamená, že pokud je vybrána tato `NULL` `ListItem`, dojde k pokusu o přiřazení hodnoty "(None)" `CategoryID`, což bude mít za následek výjimku. Když explicitně nastavíte `Value=""`, `CategoryID` se při výběru `NULL` `ListItem` přiřadí hodnota `NULL`.

Opakujte tyto kroky pro DropDownList pro dodavatele.

Pomocí tohoto dalšího `ListItem`rozhraní pro úpravy teď může přiřazovat `NULL` hodnoty k `CategoryID`ům a `SupplierID`ým polím produktu, jak je znázorněno na obrázku 12.

[![zvolit (žádný) pro přiřazení hodnoty NULL pro kategorii nebo dodavatele produktu](customizing-the-data-modification-interface-cs/_static/image35.png)](customizing-the-data-modification-interface-cs/_static/image34.png)

**Obrázek 12**: vyberte (žádný) pro přiřazení hodnoty `NULL` pro kategorii nebo dodavatele produktu ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-data-modification-interface-cs/_static/image36.png)

## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>Krok 4: použití RadioButton pro stav ukončeno

V současné době je datové pole `Discontinued` Products vyjádřeno pomocí třídě CheckBoxField podporována, které vykreslí zakázané zaškrtávací políčko pro řádky, které jsou jen pro čtení, a políčko povoleno pro upravovaný řádek. I když je toto uživatelské rozhraní často vhodné, můžeme v případě potřeby upravit pomocí TemplateField. Pro účely tohoto kurzu změňte třídě CheckBoxField podporována na TemplateField, který používá ovládací prvek RadioButtonList se dvěma možnostmi "aktivní" a "ukončené", ze kterého může uživatel zadat `Discontinued` hodnotu produktu.

Začněte převodem `Discontinued` třídě CheckBoxField podporována na TemplateField, čímž se vytvoří TemplateField pomocí `ItemTemplate` a `EditItemTemplate`. Obě šablony obsahují zaškrtávací políčko s vlastností `Checked` vázanými na datové pole `Discontinued`, jediný rozdíl mezi dvěma tím, že je vlastnost `Enabled` políčka `ItemTemplate`nastavena na `false`.

Nahraďte zaškrtávací políčko v `ItemTemplate` i `EditItemTemplate` ovládacím prvkem RadioButtonList, nastavením vlastností `ID` obou RadioButtonList na `DiscontinuedChoice`. Dále určete, že ovládací prvky RadioButtonList by měly obsahovat dva přepínače, jeden označený "aktivní" s hodnotou "false" a jeden označený "ukončen" s hodnotou "true". Chcete-li to provést, můžete buď zadat `<asp:ListItem>` prvky přímo prostřednictvím deklarativní syntaxe nebo použít Editor kolekce `ListItem` z návrháře. Obrázek 13 ukazuje `ListItem` Editor kolekce po zadání dvou přepínačů přepínačů.

[![přidat](customizing-the-data-modification-interface-cs/_static/image38.png)](customizing-the-data-modification-interface-cs/_static/image37.png)

**Obrázek 13**: Přidání možností "aktivní" a "zastaveno" na RadioButtonList ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image39.png))

Vzhledem k tomu, že se RadioButtonList v `ItemTemplate` neměl upravovat, nastavte jeho vlastnost `Enabled` na `false`, a ponechte vlastnost `Enabled` na `true` (výchozí) pro RadioButtonList v `EditItemTemplate`. Tím se přestanou přepínací tlačítka v neupravovaném řádku zobrazovat jako jen pro čtení, ale umožní uživateli změnit hodnoty RadioButton pro upravený řádek.

Pořád potřebujeme přiřadit vlastnosti `SelectedValue` ovládacího prvku RadioButtonList, aby se na základě `Discontinued`ho datového pole produktu vybral odpovídající přepínač. Stejně jako u DropDownList, které byly přezkoumány dříve v tomto kurzu, lze tuto syntaxi datové vazby přidat přímo do deklarativního kódu nebo prostřednictvím odkazu upravit datové vazby v inteligentních značkách RadioButtonList.

Po přidání dvou RadioButtonList a jejich konfiguraci by deklarativní označení `Discontinued` TemplateField mělo vypadat takto:

[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample7.aspx)]

S těmito změnami byl sloupec `Discontinued` transformované ze seznamu zaškrtávacích políček na seznam párů přepínačů (viz obrázek 14). Když upravujete produkt, je vybraný příslušný přepínač a stav zastaveno (zastaveno) produktu můžete aktualizovat tak, že vyberete druhý přepínač a kliknete na tlačítko Aktualizovat.

[![zaškrtávací políčka, která byla zastavena, byla nahrazena dvojicemi přepínačů.](customizing-the-data-modification-interface-cs/_static/image41.png)](customizing-the-data-modification-interface-cs/_static/image40.png)

**Obrázek 14**: zaškrtávací políčka ukončená byly nahrazena dvojicemi přepínačů ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-data-modification-interface-cs/_static/image42.png)).

> [!NOTE]
> Vzhledem k tomu, že sloupec `Discontinued` v databázi `Products` nemůže mít `NULL` hodnoty, nemusíte si dělat starosti se zachytáváním `NULL` informací v rozhraní. Pokud ale `Discontinued` sloupec může obsahovat `NULL` hodnoty, chtěli bychom do seznamu přidat třetí přepínač s jeho `Value` nastavenou na prázdný řetězec (`Value=""`), stejně jako u ovládacích prvků DropDownList kategorie a dodavatele.

## <a name="summary"></a>Přehled

I když vlastnost BoundField a třídě CheckBoxField podporována automaticky vykreslují rozhraní jen pro čtení, úpravy a vkládání, nemají možnost přizpůsobení. Často ale budeme muset přizpůsobit rozhraní pro úpravy nebo vložení, možná přidáte ovládací prvky pro ověřování (jak jsme viděli v předchozím kurzu) nebo přizpůsobení uživatelského rozhraní shromažďování dat (jak jsme viděli v tomto kurzu). Přizpůsobení rozhraní pomocí TemplateField lze sčítat v následujících krocích:

1. Přidat TemplateField nebo převést existující vlastnost BoundField nebo třídě CheckBoxField podporována na TemplateField
2. Rozšíření rozhraní podle potřeby
3. Svázání odpovídajících datových polí s nově přidanými webovými ovládacími prvky pomocí obousměrné datové sady

Kromě používání vestavěných webových ovládacích prvků ASP.NET můžete také přizpůsobit šablony TemplateField pomocí vlastních, kompilovaných serverových ovládacích prvků a uživatelských ovládacích prvků.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)
> [Další](implementing-optimistic-concurrency-cs.md)
