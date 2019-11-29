---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
title: Vložení nového záznamu ze zápatí prvku GridView (VB) | Microsoft Docs
author: rick-anderson
description: I když ovládací prvek GridView neposkytuje integrovanou podporu pro vkládání nového záznamu dat, v tomto kurzu se dozvíte, jak rozšířit prvek GridView tak, aby zahrnoval...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 528acc48-f20c-4b4e-aa16-4cc02f068ebb
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 67ef370a90bc843f5c2da80bb43c8ef8de216b51
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74631944"
---
# <a name="inserting-a-new-record-from-the-gridviews-footer-vb"></a>Vložení nového záznamu ze zápatí prvku GridView (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_VB.exe) nebo [Stáhnout PDF](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/datatutorial53vb1.pdf)

> I když ovládací prvek GridView neposkytuje integrovanou podporu pro vkládání nového záznamu dat, v tomto kurzu se dozvíte, jak rozšířit prvek GridView tak, aby zahrnoval rozhraní pro vložení.

## <a name="introduction"></a>Úvod

Jak je popsáno v tématu [Přehled vložení, aktualizace a odstranění dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) , jednotlivé webové ovládací prvky GridView, DetailsView a FormView obsahují integrované možnosti změny dat. Při použití s deklarativními ovládacími prvky zdroje dat lze tyto tři webové ovládací prvky rychle a snadno nakonfigurovat pro úpravu dat a ve scénářích, aniž byste museli psát jediný řádek kódu. Bohužel pouze ovládací prvky DetailsView a FormView poskytují integrované možnosti vkládání, úprav a odstraňování. Prvek GridView nabízí pouze úpravu a odstraňování podpory. Nicméně s malým pravoúhlým odmašťování můžeme ovládací prvek GridView rozšířit tak, aby zahrnoval rozhraní pro vložení.

Při přidávání možností vkládání do prvku GridView zodpovídáme za rozhodování o tom, jak se přidávají nové záznamy, vytvoří se rozhraní pro vložení a napíše se kód pro vložení nového záznamu. V tomto kurzu se podíváme na přidání rozhraní pro vložení do řádku zápatí GridView s (viz obrázek 1). Buňka zápatí pro každý sloupec obsahuje příslušný prvek uživatelského rozhraní pro shromažďování dat (textové pole pro název produktu, DropDownList pro dodavatele atd.). Pro tlačítko Přidat potřebujeme také sloupec, který po kliknutí způsobí zpětné odeslání a vložení nového záznamu do tabulky `Products` pomocí hodnot zadaných v řádku zápatí.

[![řádku zápatí poskytuje rozhraní pro přidávání nových produktů.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.png)

**Obrázek 1**: řádek zápatí poskytuje rozhraní pro přidání nových produktů ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.png)

## <a name="step-1-displaying-product-information-in-a-gridview"></a>Krok 1: zobrazení informací o produktu v prvku GridView

Předtím, než se budeme věnovat dodržovali vytváření rozhraní pro vložení do zápatí GridView s, se nejprve nezapomeňte zaměřit na přidání prvku GridView na stránku, která obsahuje seznam produktů v databázi. Začněte otevřením stránky `InsertThroughFooter.aspx` ve složce `EnhancedGridView` a přetažením prvku GridView z panelu nástrojů do návrháře, nastavením vlastnosti `ID` prvku GridView s `Products`. Dále použijte inteligentní značku GridView s pro svázání s novým prvkem ObjectDataSource s názvem `ProductsDataSource`.

[![vytvořit nový prvek ObjectDataSource s názvem ProductsDataSource](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.png)

**Obrázek 2**: vytvoření nového prvku ObjectDataSource s názvem `ProductsDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.png))

Nakonfigurujte prvek ObjectDataSource pro použití metody `GetProducts()` `ProductsBLL` třídy s k načtení informací o produktu. V tomto kurzu se zaměřujeme výhradně na přidávání možností vkládání a nedělejte si starosti s úpravami a odstraňováním. Proto se ujistěte, že rozevírací seznam na kartě Vložení je nastaven na `AddProduct()` a že rozevírací seznamy na kartách aktualizovat a odstranit jsou nastaveny na hodnotu (žádné).

[![namapovat metodu AddProduct na metodu ObjectDataSource s Insert ()](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.png)

**Obrázek 3**: namapujte metodu `AddProduct` na metodu `Insert()` ObjectDataSource s ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.png)

[![nastavení rozevíracích seznamů aktualizovat a odstranit na (žádné)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.png)

**Obrázek 4**: nastavení rozevíracích seznamů aktualizovat a odstranit na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.png))

Po dokončení Průvodce přidáním zdroje dat v prvku ObjectDataSource pro sadu Visual Studio automaticky přidá pole do prvku GridView pro každé z odpovídajících datových polí. Prozatím ponechte všechna pole přidaná v aplikaci Visual Studio. Později v tomto kurzu se vrátíme a odebereme některá pole, jejichž hodnoty není potřeba zadat při přidávání nového záznamu.

Vzhledem k tomu, že databáze obsahuje blízko až 80 produktů, bude nutné, aby se uživatel přesunul do dolní části webové stránky, aby bylo možné přidat nový záznam. Proto umožníme stránkování, aby bylo vkládání rozhraní lépe viditelné a dostupné. Chcete-li zapnout stránkování, stačí zaškrtnout políčko Povolit stránkování z inteligentní značky GridView.

V tomto okamžiku by deklarativní označení GridView a ObjectDataSource s měly vypadat podobně jako následující:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample1.aspx)]

[![všechna pole dat produktu se zobrazují ve stránkovém prvku GridView.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.png)

**Obrázek 5**: všechna pole dat produktu se zobrazují v stránkovaném prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.png)

## <a name="step-2-adding-a-footer-row"></a>Krok 2: Přidání řádku zápatí

Spolu s jeho řádky záhlaví a dat obsahuje prvek GridView řádek zápatí. Řádky záhlaví a zápatí se zobrazí v závislosti na hodnotách [`ShowHeader`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showheader.aspx) a [`ShowFooter`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showfooter.aspx) vlastností prvku GridView. Chcete-li zobrazit řádek zápatí, jednoduše nastavte vlastnost `ShowFooter` na hodnotu `True`. Jak ukazuje obrázek 6, nastavení vlastnosti `ShowFooter` na `True` přidá do mřížky řádek zápatí.

[![pro zobrazení řádku zápatí nastavte ShowFooter na hodnotu true.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.png)

**Obrázek 6**: Chcete-li zobrazit řádek zápatí, nastavte `ShowFooter` na `True` ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.png)

Všimněte si, že řádek zápatí má tmavě červenou barvu pozadí. Důvodem je motiv DataWebControls, který jsme vytvořili a použili na všechny stránky zpátky v kurzu [zobrazení dat s](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) využitím prvku ObjectDataSource. Konkrétně soubor `GridView.skin` konfiguruje vlastnost `FooterStyle`, která používá třídu `FooterStyle` šablony stylů CSS. Třída `FooterStyle` je definována v `Styles.css` následujícím způsobem:

[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample2.css)]

> [!NOTE]
> V předchozích kurzech jsme prozkoumali pomocí řádku zápatí GridView. V případě potřeby se vraťte k [zobrazení souhrnných informací v](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) kurzu pro aktualizační program v části zápatí prvku GridView.

Po nastavení vlastnosti `ShowFooter` na `True`chvíli počkejte, než se výstup zobrazí v prohlížeči. V současné době se v řádku zápatí neobsahují žádné textové ani webové ovládací prvky. V kroku 3 Upravme zápatí pro každé pole GridView tak, aby obsahovalo příslušné rozhraní pro vložení.

[![prázdného řádku zápatí se zobrazí nad ovládacími prvky rozhraní stránkování.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image13.png)

**Obrázek 7**: prázdný řádek zápatí se zobrazí nad ovládacími prvky rozhraní stránkování ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image14.png)

## <a name="step-3-customizing-the-footer-row"></a>Krok 3: přizpůsobení řádku zápatí

Zpět v kurzu [použití templatefields v kurzu ovládacího prvku GridView](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) jsme viděli, jak významně přizpůsobit zobrazení konkrétního sloupce GridView pomocí templatefields (na rozdíl od BoundFields nebo CheckBoxFields); v [části přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) jsme se vyhledali pomocí vlastností templatefields k přizpůsobení rozhraní pro úpravy v prvku GridView. Odvolání, že TemplateField se skládá z několika šablon, které definují kombinaci značek, webových ovládacích prvků a syntaxe datových vazeb použitých pro určité typy řádků. `ItemTemplate`například určuje šablonu použitou pro řádky jen pro čtení, zatímco `EditItemTemplate` definuje šablonu pro upravitelný řádek.

Společně s `ItemTemplate` a `EditItemTemplate`pole TemplateField také obsahuje `FooterTemplate`, které určuje obsah pro řádek zápatí. Proto můžeme přidat webové ovládací prvky, které jsou potřeba pro každé pole vkládání rozhraní do `FooterTemplate`. Chcete-li začít, převeďte všechna pole v prvku GridView na TemplateFields. To lze provést kliknutím na odkaz Upravit sloupce v inteligentní značce GridView s, výběrem každého pole v levém dolním rohu a kliknutím na tlačítko převést toto pole na odkaz TemplateField.

![Převést každé pole na TemplateField](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.gif)

**Obrázek 8**: převod každého pole na TemplateField

Kliknutím na tlačítko převést toto pole na TemplateField dojde k zapínání aktuálního typu pole do ekvivalentní hodnoty TemplateField. Například každá vlastnost BoundField je nahrazena vlastností TemplateField s `ItemTemplate`, která obsahuje popisek, který zobrazuje příslušné datové pole a `EditItemTemplate`, které zobrazuje datové pole v textovém poli. `ProductName` vlastnost BoundField byl převeden na následující značky TemplateField:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample3.aspx)]

Podobně `Discontinued` třídě CheckBoxField podporována byl převeden na TemplateField, jehož `ItemTemplate` a `EditItemTemplate` obsahují webový ovládací prvek CheckBox (s políčkem `ItemTemplate` s zakázáním). Vlastnost BoundField `ProductID` jen pro čtení bylo převedeno na TemplateField s ovládacím prvkem popisek v `ItemTemplate` a `EditItemTemplate`. V krátkém případě převod existujícího pole GridView na TemplateField je rychlý a snadný způsob, jak přepnout na více přizpůsobitelného TemplateField, aniž by došlo ke ztrátě všech existujících funkcí polí.

Vzhledem k tomu, že komponenta GridView, kterou jsme provedli, jsme si nemuseli upravovat podporu, nebojte se `EditItemTemplate` z každého pole TemplateField a opouštíte jenom `ItemTemplate`. Po provedení tohoto postupu by deklarativní označení GridView s mělo vypadat takto:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample4.aspx)]

Teď, když se každé pole GridView převede na TemplateField, můžeme do každého pole s `FooterTemplate`zadat příslušné rozhraní pro vložení. Některá pole nebudou mít rozhraní pro vložení (`ProductID`, například). ostatní se budou lišit ve webových ovládacích prvcích používaných ke shromažďování nových informací o produktech.

Chcete-li vytvořit rozhraní pro úpravy, vyberte odkaz Upravit šablony z inteligentní značky GridView. Pak v rozevíracím seznamu vyberte odpovídající pole `FooterTemplate` a přetáhněte příslušný ovládací prvek z panelu nástrojů do návrháře.

[![do každého pole s šablona FooterTemplate přidejte příslušné rozhraní pro vložení.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image15.png)

**Obrázek 9**: Přidejte příslušné rozhraní pro vložení do každého pole s `FooterTemplate` ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image16.png)

Následující seznam s odrážkami vypíše pole GridView a určí rozhraní pro vložení, které se má přidat:

- `ProductID` žádné.
- `ProductName` přidejte textové pole a nastavte jeho `ID` na `NewProductName`. Přidejte ovládací prvek RequiredFieldValidator a zajistěte, aby uživatel zadal hodnotu pro nový název produktu.
- `SupplierID` žádné.
- `CategoryID` žádné.
- `QuantityPerUnit` přidejte textové pole a nastavte jeho `ID` na `NewQuantityPerUnit`.
- `UnitPrice` přidat textové pole s názvem `NewUnitPrice` a CompareValidator, které zajistí, že zadaná hodnota je hodnota měny větší nebo rovna nule.
- `UnitsInStock` použít textové pole, jehož `ID` je nastavené na `NewUnitsInStock`. Zahrňte CompareValidator, který zajistí, že zadaná hodnota je celočíselná hodnota větší nebo rovna nule.
- `UnitsOnOrder` použít textové pole, jehož `ID` je nastavené na `NewUnitsOnOrder`. Zahrňte CompareValidator, který zajistí, že zadaná hodnota je celočíselná hodnota větší nebo rovna nule.
- `ReorderLevel` použít textové pole, jehož `ID` je nastavené na `NewReorderLevel`. Zahrňte CompareValidator, který zajistí, že zadaná hodnota je celočíselná hodnota větší nebo rovna nule.
- `Discontinued` přidejte zaškrtávací políčko a nastavte jeho `ID` na `NewDiscontinued`.
- `CategoryName` přidejte objekt DropDownList a nastavte jeho `ID` na `NewCategoryID`. Navažte ji na nový prvek ObjectDataSource s názvem `CategoriesDataSource` a nakonfigurujte ho tak, aby používal metodu `GetCategories()` `CategoriesBLL` třídy s. Mít `ListItem` DropDownList s, zobrazí `CategoryName` data pole, a to jako jejich hodnoty pomocí pole `CategoryID` data.
- `SupplierName` přidejte objekt DropDownList a nastavte jeho `ID` na `NewSupplierID`. Navažte ji na nový prvek ObjectDataSource s názvem `SuppliersDataSource` a nakonfigurujte ho tak, aby používal metodu `GetSuppliers()` `SuppliersBLL` třídy s. Mít `ListItem` DropDownList s, zobrazí `CompanyName` data pole, a to jako jejich hodnoty pomocí pole `SupplierID` data.

Pro každé ovládací prvky ověřování zrušte zaškrtnutí vlastnosti `ForeColor` tak, aby se místo výchozí červené hodnoty popředí `FooterStyle` třídy CSS Class s používala bílá barva popředí. Pro podrobný popis také použijte vlastnost `ErrorMessage`, ale nastavte vlastnost `Text` na hvězdičku. Chcete-li zabránit tomu, aby text ovládacího prvku ověřování způsobil přebalení rozhraní vložení na dva řádky, nastavte vlastnost `FooterStyle` s `Wrap` na hodnotu false pro každý `FooterTemplate` s, který používá ovládací prvek ověřování. Nakonec přidejte ovládací prvek ovládací souhrnu ověření pod prvek GridView a nastavte jeho vlastnost `ShowMessageBox` na `True` a jeho vlastnost `ShowSummary` na `False`.

Když přidáváte nový produkt, musíme zadat `CategoryID` a `SupplierID`. Tyto informace jsou zachyceny prostřednictvím ovládacích prvků DropDownList v buňkách zápatí pro pole `CategoryName` a `SupplierName`. Rozhodli jste se použít tato pole na rozdíl od `CategoryID` a `SupplierID` TemplateFields, protože v řádcích s daty gridu se uživatel pravděpodobně lépe zajímá, aby zobrazil názvy kategorií a dodavatelů, nikoli jejich hodnoty ID. Vzhledem k tomu, že hodnoty `CategoryID` a `SupplierID` jsou nyní zaznamenávány do `CategoryName` a `SupplierName` pole pro vkládání rozhraní, můžeme odebrat `CategoryID` a `SupplierID` TemplateFields z prvku GridView.

Obdobně se `ProductID` nepoužívá při přidávání nového produktu, takže je možné také odebrat `ProductID` TemplateField. Ale nechte pole `ProductID` v mřížce. Kromě textových polí, DropDownList, zaškrtávacích políček a ověřovacích ovládacích prvků, které tvoří rozhraní pro vložení, budete potřebovat také tlačítko Přidat, které po kliknutí provede logiku pro přidání nového produktu do databáze. V kroku 4 přidáme tlačítko Přidat do rozhraní pro vložení v `ProductID` TemplateField s `FooterTemplate`.

Nebojte se zlepšit vzhled různých polí GridView. Například můžete chtít naformátovat `UnitPrice` hodnoty jako měnu, Zarovnat pole `UnitsInStock`, `UnitsOnOrder`a `ReorderLevel` a aktualizovat `HeaderText` hodnoty pro pole TemplateField.

Po vytvoření slew pro vkládání rozhraní v `FooterTemplate` s, odebrání `SupplierID`a `CategoryID` TemplateFields a zlepšení estetickosti mřížky prostřednictvím formátování a zarovnání TemplateFields by vaše deklarativní značky GridViewu měly vypadat podobně jako následující:

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample5.aspx)]

Při prohlížení v prohlížeči teď řádek zápatí prvku GridView. obsahuje dokončené rozhraní vložení (viz obrázek 10). V tomto okamžiku vložení rozhraní nezahrnuje prostředek pro uživatele, který indikuje, že zadal data pro nový produkt a chce do databáze vložit nový záznam. I když jsme ještě zjistili, jak se data zadaná do zápatí budou překládat do nového záznamu v databázi `Products`. V kroku 4 se podíváme na to, jak zahrnout tlačítko Přidat do rozhraní pro vkládání a jak spustit kód při zpětném volání, když se na něj klikne. Krok 5 ukazuje, jak vložit nový záznam pomocí dat z zápatí.

[![zápatí prvku GridView poskytuje rozhraní pro přidání nového záznamu.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image17.png)

**Obrázek 10**: zápatí prvku GridView poskytuje rozhraní pro přidání nového záznamu ([kliknutím zobrazíte obrázek v plné velikosti](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image18.png)).

## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>Krok 4: zahrnutí tlačítka Přidat do rozhraní pro vložení

Do rozhraní pro vkládání musíme vložit tlačítko Přidat, protože rozhraní pro vložení řádku zápatí v tuto chvíli neobsahuje prostředky pro uživatele, aby označovali, že dokončili zadávání informací o novém produktu. To může být umístěno v jednom z existujících `FooterTemplate` s nebo do mřížky pro tento účel přidat nový sloupec. Pro tento kurz přidejte tlačítko Přidat do `ProductID` TemplateField `FooterTemplate`.

V návrháři klikněte na odkaz Upravit šablony v inteligentní značce GridView s a pak v rozevíracím seznamu zvolte `ProductID` pole s `FooterTemplate`. Přidejte webový ovládací prvek tlačítko (nebo objekt LinkButton nebo obrázkové, pokud dáváte přednost) k šabloně, nastavení jeho ID na hodnotu `AddProduct`, jeho `CommandName` pro vložení a jeho vlastnost `Text` k přidání, jak je znázorněno na obrázku 11.

[![umístit tlačítko Přidat do pole ProductID TemplateField s šablona FooterTemplate](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image19.png)

**Obrázek 11**: Vložte tlačítko přidat do `ProductID` TemplateField s `FooterTemplate` ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image20.png)

Až budete mít tlačítko Přidat, otestujte stránku v prohlížeči. Všimněte si, že když kliknete na tlačítko Přidat s neplatnými daty v rozhraní pro vložení, zpětné volání je krátké a ovládací prvek ovládací souhrnu ověření indikuje neplatná data (viz obrázek 12). Po zadání příslušných dat se kliknutím na tlačítko Přidat vyvolá postback. Do databáze se ale nepřidá žádný záznam. Abychom mohli vkládat, budete muset napsat bitovou kopii kódu.

[![tlačítko Přidat s zpětným voláním je krátké, pokud v rozhraní pro vkládání nejsou platná data.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image21.png)

**Obrázek 12**: v případě, že je v rozhraní pro vkládání neplatné nějaké údaje ([kliknutím zobrazíte obrázek v plné velikosti](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image22.png)), je tlačítko Přidat a zpět v případě neplatných.

> [!NOTE]
> Ovládací prvky ověřování v rozhraní vložení nebyly přiřazeny ke skupině ověření. To funguje, pokud je rozhraní pro vkládání jedinou sadou ověřovacích ovládacích prvků na stránce. Pokud jsou však na stránce k dispozici další ovládací prvky ověřování (například ovládací prvky ověřování v rozhraní pro úpravy gridu), měla by být ovládacím prvkům pro vložení rozhraní a tlačítku Přidat `ValidationGroup` vlastností přiřazena stejná hodnota, aby bylo možné tyto ovládací prvky přidružit ke konkrétní skupině ověření. Další informace o dělení ověřovacích ovládacích prvků a tlačítek na stránce do ověřovacích skupin naleznete v tématu [deprotínající ovládací prvky ověřování v ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx) .

## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>Krok 5: vložení nového záznamu do`Products`tabulky

Při použití vestavěných funkcí úprav ovládacího prvku GridView, prvek GridView automaticky zpracuje veškerou práci potřebnou k aktualizaci. Zejména při kliknutí na tlačítko Aktualizovat kopíruje hodnoty zadané z rozhraní pro úpravy do parametrů v kolekci ObjectDataSource `UpdateParameters` Collection a zahájí aktualizaci vyvoláním metody ObjectDataSource s `Update()`. Vzhledem k tomu, že prvek GridView neposkytuje integrovanou funkcionalitu pro vkládání, je nutné implementovat kód, který volá metodu ObjectDataSource s `Insert()` a kopíruje hodnoty z rozhraní pro vložení do kolekce ObjectDataSource s `InsertParameters`.

Tato logika vložení by měla být provedena po kliknutí na tlačítko Přidat. Jak je popsáno v kurzu [přidávání a reagování na tlačítka v](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb.md) prvku GridView, je kliknutí na tlačítko, LinkButton nebo obrázkové v prvku GridView, událost GridView `RowCommand`, která se aktivuje při zpětném volání. Tato událost aktivuje, zda bylo tlačítko, LinkButton nebo obrázkové přidáno explicitně, například tlačítko Přidat v řádku zápatí, nebo zda bylo automaticky přidáno prvek GridView (například LinkButtons v horní části každého sloupce, pokud je vybrána možnost Povolit řazení), nebo LinkButtons v rozhraní stránkování, pokud je vybráno možnost Povolit stránkování).

Proto pokud chcete reagovat na uživatele kliknutím na tlačítko Přidat, musíme vytvořit obslužnou rutinu události pro `RowCommand` událost GridView. Vzhledem k tomu, že se tato událost aktivuje *vždy, když se* klikne na tlačítko, LinkButton nebo obrázkové v prvku GridView, je důležité, abyste pokračovali pouze s logikou vložení, pokud vlastnost `CommandName` předaná do obslužné rutiny události mapuje na `CommandName` hodnotu tlačítka Přidat (vložit). Kromě toho by měl být také pokračovat pouze v případě, že ovládací prvky ověřování vykazují platná data. Chcete-li to přizpůsobit, vytvořte obslužnou rutinu události pro událost `RowCommand` s následujícím kódem:

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample6.vb)]

> [!NOTE]
> Může dojít k zajímání, proč obslužná rutina události kontroluje vlastnost `Page.IsValid`. Po všech nebudete moct postback potlačit, pokud v rozhraní pro vkládání nejsou k dispozici neplatná data? Tento předpoklad je správný, dokud uživatel nezakázal JavaScript nebo neučinil kroky pro obcházení logiky ověřování na straně klienta. V krátkém případě by se jedna neměla spoléhat výhradně na ověřování na straně klienta; před prací s daty by měla být vždy provedena kontrolu platnosti na straně serveru.

V kroku 1 jsme vytvořili `ProductsDataSource` ObjectDataSource tak, že jeho `Insert()` metoda je namapována na `AddProduct` metodu `ProductsBLL` třídy s. Pro vložení nového záznamu do tabulky `Products` můžeme jednoduše vyvolat metodu `Insert()` ObjectDataSource s:

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample7.vb)]

Nyní, když byla vyvolána metoda `Insert()`, vše zůstává ke zkopírování hodnot z rozhraní pro vložení do parametrů předaných metodě `AddProduct` `ProductsBLL` třídy s. Jak jsme se vrátili při [zkoumání událostí spojených s kurzem vložení, aktualizace a odstranění](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) , můžete to provést prostřednictvím události ObjectDataSource `Inserting`. V `Inserting` události potřebujeme programově odkazovat na ovládací prvky z řádku zápatí `Products` GridView s a přiřadit jejich hodnoty do kolekce `e.InputParameters`. Pokud uživatel vynechá hodnotu, třeba když necháte pole `ReorderLevel` prázdné pole, je nutné zadat, aby byla hodnota vložená do databáze `NULL`. Vzhledem k tomu, že metoda `AddProducts` akceptuje typy s možnou hodnotou null pro pole databáze s možnou hodnotou null, stačí použít typ s možnou hodnotou null a nastavit jeho hodnotu na `Nothing` v případě vynechání vstupu uživatele.

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample8.vb)]

Když je obslužná rutina události `Inserting` dokončená, dají se do tabulky databáze `Products` přidat nové záznamy přes řádek zápatí GridView. Pokračujte a zkuste přidat několik nových produktů.

## <a name="enhancing-and-customizing-the-add-operation"></a>Vylepšení a přizpůsobení operace přidání

V současné době kliknutím na tlačítko Přidat přidáte nový záznam do tabulky databáze, ale neposkytnete žádný druh vizuální zpětné vazby, který záznam úspěšně přidal. V ideálním případě by okno popisek webového ovládacího prvku nebo upozornění na straně klienta informovalo uživatele o tom, že jejich vložení bylo úspěšné. Tuto funkci mám jako cvičení pro čtenáře.

Prvek GridView použitý v tomto kurzu nepoužívá pro uvedené produkty žádné pořadí řazení, ani neumožňuje koncovému uživateli data seřadit. V důsledku toho jsou záznamy seřazeny tak, jak jsou v databázi, podle jejich primárního pole klíče. Vzhledem k tomu, že každý nový záznam má `ProductID` hodnotu větší než poslední, pokaždé, když se přidá nový produkt, se směruje na konec mřížky. Proto může být vhodné po přidání nového záznamu automaticky odeslat uživatele na poslední stránku prvku GridView. To lze provést přidáním následujícího řádku kódu po volání `ProductsDataSource.Insert()` v obslužné rutině události `RowCommand` pro indikaci, že uživatel musí být odeslán na poslední stránku po vytvoření vazby dat na prvek GridView:

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample9.vb)]

`SendUserToLastPage` je logická proměnná na úrovni stránky, která má zpočátku přiřazenou hodnotu `False`. V obslužné rutině `DataBound` ovládacího prvku GridView, pokud je `SendUserToLastPage` false, je vlastnost `PageIndex` aktualizována tak, aby odesílala uživatele na poslední stránku.

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample10.vb)]

Důvod, proč je nastavena vlastnost `PageIndex` v obslužné rutině události `DataBound` (na rozdíl od obslužné rutiny události `RowCommand`) je, že když obslužná rutina události `RowCommand` aktivuje, je to proto, že jsme ještě do tabulky `Products`ch databází přidali nový záznam. Proto v obslužné rutině události `RowCommand` poslední index stránky (`PageCount - 1`) představuje poslední index stránky *před* přidáním nového produktu. Pro většinu přidávaných produktů je poslední index stránky stejný po přidání nového produktu. Pokud ale přidaný produkt vede k novému indexu poslední stránky, pokud jsme `PageIndex` v obslužné rutině události `RowCommand` nesprávně aktualizovali pak budeme považovat za druhý na poslední stránku (poslední index stránky před přidáním nového produktu), a to na rozdíl od nového indexu poslední stránky. Vzhledem k tomu, že se obslužná rutina události `DataBound` aktivuje poté, co se přidá nový produkt a data se předají do mřížky, nastavím vlastnost `PageIndex`, že máme znovu napravo správné indexu poslední stránky.

Nakonec je ovládací prvek GridView použitý v tomto kurzu poměrně velký v důsledku počtu polí, která musí být shromažďována pro přidání nového produktu. Vzhledem k této šířce může být upřednostňováno svislé rozložení ovládacího prvku DetailsView s. Celkovou šířku prvku GridView s lze snížit shromažďováním menšího počtu vstupů. Možná nepotřebujeme při přidávání nového produktu shromažďovat pole `UnitsOnOrder`, `UnitsInStock`a `ReorderLevel`. v takovém případě je možné tato pole odebrat z prvku GridView.

Pro úpravu shromažďovaných dat můžeme použít jeden ze dvou přístupů:

- Pokračujte v použití metody `AddProduct`, která očekává hodnoty pro pole `UnitsOnOrder`, `UnitsInStock`a `ReorderLevel`. V obslužné rutině události `Inserting` poskytují pevně zakódované výchozí hodnoty, které se použijí pro tyto vstupy, které byly odebrány z rozhraní pro vložení.
- Vytvořte nové přetížení metody `AddProduct` ve třídě `ProductsBLL`, která nepřijímá vstupy pro pole `UnitsOnOrder`, `UnitsInStock`a `ReorderLevel`. Pak na stránce ASP.NET nakonfigurujte prvek ObjectDataSource tak, aby používal toto nové přetížení.

Obě možnosti budou fungovat i stejně. V minulých kurzech jsme použili druhou možnost a vytvořením několika přetížení pro metodu `ProductsBLL` třídy s `UpdateProduct`.

## <a name="summary"></a>Přehled

V prvku GridView chybí vestavěné možnosti vkládání nalezené v ovládacím prvku DetailsView a FormView, ale s mikroúsilím je možné přidat rozhraní vložení do řádku zápatí. Chcete-li zobrazit řádek zápatí v prvku GridView, stačí nastavit jeho vlastnost `ShowFooter` na hodnotu `True`. Obsah řádku zápatí lze přizpůsobit pro každé pole tak, že převede pole na TemplateField a přidáte rozhraní pro vložení do `FooterTemplate`. Jak jsme viděli v tomto kurzu, `FooterTemplate` mohou obsahovat tlačítka, textová pole, DropDownList, zaškrtávací políčka a ovládací prvky zdroje dat pro vyplnění datových ovládacích prvků řízených daty (například DropDownList) a ověřovací ovládací prvky. Společně s ovládacími prvky pro shromažďování vstupu uživatele, je třeba přidat tlačítko Přidat, LinkButton nebo obrázkové.

Po kliknutí na tlačítko Přidat je vyvolána metoda ObjectDataSource s `Insert()` k zahájení vkládání pracovního postupu. Prvek ObjectDataSource pak zavolá nakonfigurovanou metodu Insert (metoda `ProductsBLL` třídy s `AddProduct` v tomto kurzu). Před vyvoláním metody Insert je nutné zkopírovat hodnoty z rozhraní GridView s `InsertParameters` do kolekce ObjectDataSource s. To lze provést programově odkazování na webové ovládací prvky rozhraní v prvku ObjectDataSource s `Inserting` obslužné rutiny události.

V tomto kurzu se dokončí náš pohled na techniky pro vylepšení vzhledu prvků GridView. Další sada kurzů bude kontrolovat, jak pracovat s binárními daty, jako jsou obrázky, soubory PDF, dokumenty aplikace Word atd. a webové ovládací prvky dat.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Bernadette Leigh. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](adding-a-gridview-column-of-checkboxes-vb.md)
