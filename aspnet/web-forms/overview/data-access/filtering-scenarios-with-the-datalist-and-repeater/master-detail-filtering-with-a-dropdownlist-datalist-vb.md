---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: Filtrování seznamu a podrobností s ovládacím prvkem DropDownList (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se zobrazuje, jak zobrazit hlavní a podrobné sestavy na jedné webové stránce pomocí DropDownList k zobrazení záznamů "Master" a prvku DataList pro displ...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 537f8e76bc0cbfa759a014b63ae5f68b5d3ca64d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74629883"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>Filtrování hlavních záznamů / podrobností ovládacím prvkem DropDownList (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) nebo [Stáhnout PDF](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)

> V tomto kurzu se zobrazuje, jak zobrazit hlavní a podrobné sestavy na jedné webové stránce pomocí DropDownList pro zobrazení "hlavních" záznamů a prvku DataList pro zobrazení podrobností.

## <a name="introduction"></a>Úvod

Sestava hlavní/podrobnosti, kterou jsme nejprve vytvořili pomocí prvku GridView v předchozím [filtru hlavního/podrobného filtrování s](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) kurzem DropDownList, začíná zobrazením některé sady "hlavních" záznamů. Uživatel pak může přejít k podrobnostem jednoho ze vzorových záznamů, takže zobrazí podrobnosti o tomto hlavním záznamu. Hlavní a podrobné sestavy jsou ideální volbou pro vizualizaci vztahů 1: n a pro zobrazení podrobných informací z zvláště "nejrůznějších" tabulek (ty, které mají velké množství sloupců). Prozkoumali jsme, jak implementovat hlavní a podrobné sestavy pomocí ovládacích prvků GridView a DetailsView v předchozích kurzech. V tomto kurzu a dalších dvou prověříme tyto koncepty, ale místo toho se zaměřte na použití ovládacího prvku DataList a Repeater.

V tomto kurzu se podíváme na použití ovládacího prvku DropDownList k tomu, aby obsahovalo "hlavní" záznamy a záznamy podrobností zobrazených v prvku DataList.

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>Krok 1: Přidání webových stránek kurzu hlavního/podrobného kurzu

Než začnete s tímto kurzem, nejdřív se podíváme na přidání složky a ASP.NET stránek, které budeme potřebovat pro tento kurz, a dalších dvou operací se sestavou hlavních a podrobných sestav pomocí ovládacích prvků DataList a Repeater. Začněte vytvořením nové složky v projektu s názvem `DataListRepeaterFiltering`. V dalším kroku přidejte do této složky následující pět ASP.NET stránek a všechny je nakonfigurované tak, aby používaly stránku předlohy `Site.master`:

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`

![Vytvořte složku DataListRepeaterFiltering a přidejte stránky ASP.NET kurzu.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

**Obrázek 1**: vytvoření složky pro `DataListRepeaterFiltering` a přidání ASP.NETových stránek kurzu

Potom otevřete stránku `Default.aspx` a přetáhněte uživatelský ovládací prvek `SectionLevelTutorialListing.ascx` ze složky `UserControls` na návrhovou plochu. Tento uživatelský ovládací prvek, který jsme vytvořili v kurzu [hlavní stránky a navigace na webu](../introduction/master-pages-and-site-navigation-vb.md) , vytvoří výčet mapy lokality a zobrazí kurzy z aktuální části v seznamu s odrážkami.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))

Aby se v seznamu s odrážkami zobrazovaly hlavní a podrobné kurzy, vytvoříme je, abychom je mohli přidat k mapě webu. Otevřete soubor `Web.sitemap` a přidejte následující kód za "zobrazení dat pomocí značek DataList a Repeater" značky uzlu mapy webu:

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]

![Aktualizovat mapu webu tak, aby obsahovala nové stránky ASP.NET](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

**Obrázek 3**: aktualizace mapy webu tak, aby obsahovala nové stránky ASP.NET

## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>Krok 2: zobrazení kategorií v DropDownList

V naší sestavě Master/Detail se zobrazí seznam kategorií v DropDownList a na stránce v prvku DataList se zobrazí níže zobrazené produkty vybrané položky seznamu. První úkol je před námi a pak má mít kategorie zobrazené v DropDownList. Začněte otevřením stránky `FilterByDropDownList.aspx` ve složce `DataListRepeaterFiltering` a přetažením ovládacího prvku DropDownList z panelu nástrojů do návrháře stránky. Dále nastavte vlastnost `ID` ovládacího prvku DropDownList na hodnotu `Categories`. Klikněte na odkaz zvolit zdroj dat z inteligentní značky DropDownList a vytvořte nový prvek ObjectDataSource s názvem `CategoriesDataSource`.

[![přidat nový prvek ObjectDataSource s názvem CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)

**Obrázek 4**: Přidání nového prvku ObjectDataSource s názvem `CategoriesDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))

Nakonfigurujte nový prvek ObjectDataSource tak, že vyvolá metodu `GetCategories()` `CategoriesBLL` třídy. Po nakonfigurování prvku ObjectDataSource je stále potřeba určit, jaké pole zdroje dat by se mělo zobrazit v DropDownList a který má být přidružen jako hodnota pro každou položku seznamu. Má pole `CategoryName` jako hodnotu zobrazení a `CategoryID` jako hodnotu pro každou položku seznamu.

[![mají DropDownList zobrazit pole CategoryName a jako hodnotu použít CategoryID.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)

**Obrázek 5**: DropDownList zobrazí pole `CategoryName` a jako hodnotu použije `CategoryID` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png)

V tuto chvíli máme ovládací prvek DropDownList, který je naplněný záznamy z `Categories` tabulky (vše bylo dokončeno přibližně po dobu šesti sekund). Obrázek 6 znázorňuje náš průběh, pokud je zobrazený v prohlížeči.

[![rozevíracího seznamu pro aktuální kategorie](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)

**Obrázek 6**: rozevírací seznam pro aktuální kategorie ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))

## <a name="step-2-adding-the-products-datalist"></a>Krok 2: Přidání prvku DataList pro produkty

Posledním krokem v naší sestavě Master/Detail je seznam produktů přidružených k vybrané kategorii. K tomu je nutné přidat prvek DataList na stránku a vytvořit nový prvek ObjectDataSource s názvem `ProductsByCategoryDataSource`. Mít ovládací prvek `ProductsByCategoryDataSource` načíst jeho data z metody `GetProductsByCategoryID(categoryID)` `ProductsBLL` třídy. Vzhledem k tomu, že tato sestava hlavní/podrobnosti je jen pro čtení, vyberte možnost (žádná) na kartách vložení, aktualizace a odstranění.

[![vybrat metodu GetProductsByCategoryID (KódKategorie)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)

**Obrázek 7**: vyberte metodu `GetProductsByCategoryID(categoryID)` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png)).

Po kliknutí na tlačítko Další Průvodce ObjectDataSource vyzve pro zdroj hodnoty pro *`categoryID`* parametr metody `GetProductsByCategoryID(categoryID)`. Chcete-li použít hodnotu vybrané `categories` položku DropDownList, nastavte zdroj parametru jako ovládací prvek a vlastnosti ControlID k `Categories`.

[![nastavit parametr categoryID na hodnotu kategorie DropDownList](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)

**Obrázek 8**: nastavte parametr *`categoryID`* na hodnotu `Categories` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png)

Po dokončení Průvodce konfigurací zdroje dat bude Visual Studio automaticky generovat `ItemTemplate` pro prvek DataList, který zobrazuje název a hodnotu jednotlivých datových polí. Vylepšete prvek DataList, aby místo toho používal `ItemTemplate`, který zobrazuje pouze název produktu, kategorii, dodavatel, množství na jednotku a cenu spolu s `SeparatorTemplate`, který vkládá `<hr>` prvek mezi jednotlivými položkami. Nyní používám `ItemTemplate` z příkladu v [zobrazení dat pomocí kurzu ovládací prvky DataList a Repeater](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) , ale můžete použít jakýkoli kód šablony, který vyhledáte na základě vizuálního odvolání.

Po provedení těchto změn by váš prvek DataList a jeho značky ObjectDataSource měly vypadat podobně jako následující:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

Chvíli si Projděte náš pokrok v prohlížeči. Při první návštěvě stránky se zobrazí tyto produkty patřící do vybrané kategorie (nápoje) (jak je znázorněno na obrázku 9), ale změna ovládacího prvkem DropDownList neaktualizuje data. Důvodem je, že k aktualizaci prvku DataList musí dojít k postbacku. Chcete-li to dosáhnout, můžeme buď nastavit vlastnost `AutoPostBack` ovládacího prvku DropDownList na `true` nebo přidat webové ovládací prvky tlačítka na stránku. V tomto kurzu se mi rozhodlo nastavit vlastnost `AutoPostBack` ovládacího prvku DropDownList na hodnotu `true`.

Obrázky 9 a 10 ilustrují sestavu hlavní/podrobnosti v akci.

[![při první návštěvě stránky se zobrazí nápojové produkty.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)

**Obrázek 9**: když poprvé navštívíte stránku, zobrazí se nápojové produkty ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png)).

[![výběru nového produktu (vytváře) automaticky vyvolá PostBack, aktualizuje se DataList.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)

**Obrázek 10**: výběr nového produktu (vytvořeného) automaticky způsobí postback, aktualizaci prvku DataList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png)).

## <a name="adding-a----choose-a-category----list-item"></a>Přidání položky seznamu "--zvolit kategorii"

Při první návštěvě `FilterByDropDownList.aspx` stránky je ve výchozím nastavení vybrána položka první položka seznamu (nápoje) kategorie, která zobrazuje nápoje v prvku DataList. V rámci *filtrování hlavní/podrobnosti pomocí kurzu DropDownList* jsme přidali možnost "--zvolit kategorii" na ovládacím prvkem DropDownList, která byla vybrána ve výchozím nastavení, a pokud je vybrána, zobrazí se *všechny* produkty v databázi. Takový přístup je spravovatelný při výpisu produktů v prvku GridView, protože každý produktový řádek zabral malou plochu obrazovky. U prvku DataList ale všechny informace o produktu spotřebovávají mnohem větší blok obrazovky. Pojďme stále přidat možnost--zvolit kategorii a vybrat ji ve výchozím nastavení, ale místo toho, aby zobrazovala všechny produkty, je možné ji nakonfigurovat tak, aby se zobrazily žádné produkty.

Chcete-li přidat novou položku seznamu do ovládacího prvků DropDownList, přejděte na okno Vlastnosti a klikněte na tlačítko se třemi tečkami ve vlastnosti `Items`. Přidejte novou položku seznamu s `Text` "--zvolit kategorii--" a `Value` `0`.

![Přidat](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

**Obrázek 11**: Přidání položky seznamu "--zvolit kategorii"

Alternativně můžete přidat položku seznamu přidáním následujícího kódu do ovládacího prvkem DropDownList:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

Kromě toho je potřeba nastavit `AppendDataBoundItems` ovládacího prvku DropDownList na `true`, protože pokud je nastaven na `false` (výchozí), pokud jsou kategorie svázány s ovládacím prvkem DropDownList z prvku ObjectDataSource, budou přepsány jakékoli ručně přidané položky seznamu.

![Nastavte vlastnost AppendDataBoundItems na hodnotu true.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

**Obrázek 12**: nastavte vlastnost `AppendDataBoundItems` na hodnotu true.

Důvodem je, že `0` hodnoty pro "--zvolit kategorii –" položka seznamu je, protože v systému nejsou žádné kategorie s hodnotou `0`, a proto nebudou vráceny žádné záznamy produktů, pokud je vybrána položka seznamu "--zvolit kategorii". Potvrďte to tak, že chvíli navštívíte stránku prostřednictvím prohlížeče. Jak ukazuje obrázek 13, při počátečním zobrazení stránky se vybere položka seznamu "--zvolit kategorii--" a nezobrazí se žádné produkty.

[![, když](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)

**Obrázek 13**: když je vybraná položka seznamu "--zvolit kategorii--", nezobrazí se žádné produkty ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png)

Pokud místo toho chcete zobrazit *všechny* produkty v případě, že je vybrána možnost--zvolit kategorii--, použijte místo toho hodnotu `-1`. Čtečka bystří tento postup vrátí zpět v rámci *filtrování hlavního/podrobného filtru pomocí kurzu DropDownList* . Aktualizovali jsme `GetProductsByCategoryID(categoryID)` metodu `ProductsBLL` třídy, takže pokud byla předána hodnota *`categoryID`* `-1`, všechny záznamy produktů byly vráceny.

## <a name="summary"></a>Přehled

Při zobrazení hierarchicky souvisejících dat často pomáhá prezentovat data pomocí hlavních a podrobných sestav, od kterých může uživatel začít perusing data z horní části hierarchie a přejít k podrobnostem. V tomto kurzu jsme prozkoumali vytvoření jednoduché sestavy hlavní/podrobnosti zobrazující produkty vybrané kategorie. To bylo provedeno pomocí ovládacího prvku DropDownList pro seznam kategorií a DataList pro produkty patřící do vybrané kategorie.

V dalším kurzu se podíváme na oddělení hlavních a podrobných záznamů na dvou stránkách. Na první stránce se zobrazí seznam "Master" záznamů s odkazem na zobrazení podrobností. Kliknutím na odkaz zobrazíte uživatele na druhou stránku, kde se zobrazí podrobnosti vybraného hlavního záznamu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Randy Schmidt. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [Další](master-detail-filtering-acess-two-pages-datalist-vb.md)
