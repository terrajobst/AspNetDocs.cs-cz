---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
title: Hlavní a podrobnosti pomocí seznamu hlavních záznamů s odrážkami s podrobnostmi DataList (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu zkomprimujete sestavu se dvěma stránkami a podrobnostmi pro předchozí kurz na jednu stránku, kde se zobrazí seznam názvů kategorií na t...
ms.author: riande
ms.date: 10/17/2006
ms.assetid: ee20742f-6fb7-49a0-a009-058fe363aacb
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 81d72c666925e89729464e7ea696bde8d323e277
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74641715"
---
# <a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb"></a>Zobrazení hlavních záznamů / podrobností v seznamu hlavních záznamů s odrážkami a podrobnostmi v prvku DataList (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_VB.exe) nebo [Stáhnout PDF](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/datatutorial35vb1.pdf)

> V tomto kurzu zkomprimujete sestavu se dvěma stránkami a podrobnostmi o předchozím kurzu na jednu stránku, kde se zobrazí seznam názvů kategorií na levé straně obrazovky a produkty vybrané kategorie na pravé straně obrazovky.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](master-detail-filtering-acess-two-pages-datalist-vb.md) jsme se vyhledali tak, jak oddělit hlavní a podrobné sestavy na dvou stránkách. Na stránce předlohy jsme použili ovládací prvek Repeater k vykreslení seznamu kategorií s odrážkami. Název každé kategorie byl hypertextový odkaz, který při kliknutí na ni převezme uživatele na stránku podrobností, kde se ve dvou sloupcích DataList ukázaly tyto produkty patřící do vybrané kategorie.

V tomto kurzu zkomprimujeme dvoustranný kurz na jednu stránku a zobrazí se seznam názvů kategorií na levé straně obrazovky s odrážkami s každým názvem kategorie vykresleným jako LinkButton. Kliknutí na jednu z kategorií název LinkButtons vyvolává zpětné odeslání a váže vybrané produkty kategorie s na dva sloupce DataList na pravé straně obrazovky. Kromě zobrazení jednotlivých kategorií s názvem opakuje na levé straně počet produktů, které jsou pro danou kategorii k dispozici (viz obrázek 1).

[![kategorie s název a celkový počet produktů se zobrazí vlevo.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image1.png)

**Obrázek 1**: na levé straně se zobrazí název kategorie a celkový počet produktů ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image3.png)

## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>Krok 1: zobrazení opakovače v levé části obrazovky

Pro účely tohoto kurzu musíme zobrazit seznam kategorií s odrážkami vlevo od vybraných produktů kategorií. Obsah webové stránky lze umístit pomocí standardních značek odstavců HTML, nekoncových mezer, `<table>` s a tak dále, nebo prostřednictvím kaskádových stylů CSS. Všechny naše kurzy doposud používaly techniky CSS k umístění. Při sestavování uživatelského rozhraní navigace na naší stránce předlohy na [stránkách předlohy a](../introduction/master-pages-and-site-navigation-vb.md) v kurzu navigace na webu jsme použili *absolutní umístění*, které indikuje přesný Posun pixelů pro navigační seznam a hlavní obsah. Alternativně lze šablonu stylů CSS použít k umístění jednoho prvku vpravo nebo vlevo od druhého až po *plovoucí*. Seznam kategorií s odrážkami se zobrazuje vlevo od vybraných produktů kategorie s použitím plovoucího opakovače vlevo od prvku DataList.

Otevřete stránku `CategoriesAndProducts.aspx` ze složky `DataListRepeaterFiltering` a přidejte ji do stránky Repeater a DataList. Nastavte `ID` opakování na `Categories` a DataList s na `CategoryProducts`. Přejít do zobrazení zdroje a umístit ovládací prvky Repeater a DataList do jejich vlastních prvků `<div>`. To znamená, že se nejdříve vloží Repeat do prvku `<div>` a poté prvek DataList ve svém vlastním prvku `<div>` přímo za Repeat. Vaše značka v tomto okamžiku by měla vypadat nějak takto:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample1.aspx)]

Pro obtékání opakovače vlevo od prvku DataList je nutné použít atribut `float` stylu CSS, například:

[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample2.html)]

`float: left;` obtéká první prvek `<div>` nalevo od druhého prvku. Nastavení `width` a `padding-right` označují první `<div>` `width` a velikost odsazení mezi `<div>`m obsahem prvku a jeho pravým okrajem. Další informace o plovoucích prvcích v šablonách stylů CSS najdete v [Floatutorial](http://css.maxdesign.com.au/floatutorial/).

Namísto určení nastavení stylu přímo pomocí prvního `<p>` atributu `style` elementu, nechte místo toho vytvořit novou třídu CSS v `Styles.css` s názvem `FloatLeft`:

[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample3.css)]

Pak můžeme `<div>` nahradit `<div class="FloatLeft">`.

Po přidání třídy šablony stylů CSS a konfiguraci značek na stránce `CategoriesAndProducts.aspx` přejdete do návrháře. Měl by se vidět, že se má na začátku v prvku DataList zobrazit obdélník, který se zobrazí vlevo (i když se teď právě zobrazují jako šedá pole, protože jsme ještě předtím nakonfigurovali své zdroje dat nebo šablony).

[![, že se opakuje vlevo od prvku DataList](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image4.png)

**Obrázek 2**: Repeater se odpluje nalevo od prvku DataList ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image6.png)

## <a name="step-2-determining-the-number-of-products-for-each-category"></a>Krok 2: určení počtu produktů pro jednotlivé kategorie

S úplným označením Repeat a DataList s doplňováním kódu jsme znovu připraveni vytvořit vazby dat kategorie k ovládacímu prvku Repeater. Seznam kategorií s odrážkami na obrázku 1 ale navíc také potřebuje zobrazit počet produktů přidružených k této kategorii. Pro přístup k těmto informacím můžeme buď:

- **Určete tyto informace ze třídy ASP.NET stránky s kódem na pozadí.** S ohledem na konkrétní *`categoryID`* můžeme určit počet přidružených produktů voláním metody `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)`. Tato metoda vrátí objekt `ProductsDataTable`, jehož vlastnost `Count` určuje, kolik `ProductsRow` existuje, což je počet produktů pro zadanou *`categoryID`* . Můžeme vytvořit obslužnou rutinu události `ItemDataBound` pro Repeater, která pro každou kategorii, která je svázána s argumentem Repeater, volá metodu `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)` a obsahuje její počet ve výstupu.
- **Aktualizujte `CategoriesDataTable` v zadané datové sadě tak, aby zahrnovaly sloupec `NumberOfProducts`.** Pak můžeme aktualizovat metodu `GetCategories()` v `CategoriesDataTable` tak, aby obsahovala tyto informace, nebo můžete také opustit `GetCategories()` jako a vytvořit novou `CategoriesDataTable` metodu nazvanou `GetCategoriesAndNumberOfProducts()`.

Pojďme prozkoumat oba tyto postupy. Prvním přístupem je jednodušší implementovat, protože nepotřebujeme aktualizovat vrstvu přístupu k datům. ale vyžaduje více komunikace s databází. Volání metody `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)` v obslužné rutině události `ItemDataBound` přidá další volání databáze pro každou kategorii zobrazenou v OPAKOVAČI. V této technice je k dispozici volání databáze *n* + 1, kde *n* je počet kategorií zobrazených v poli Repeater. Při druhém přístupu se počet produktů vrátí s informacemi o jednotlivých kategoriích z metody `CategoriesBLL` třídy s `GetCategories()` (nebo `GetCategoriesAndNumberOfProducts()`), a výsledkem je pouze jedna cesta k databázi.

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>Určení počtu produktů v obslužné rutině události ItemDataBound

Určení počtu produktů pro každou kategorii v `ItemDataBound` obslužná rutina události Repeater, nevyžaduje žádné úpravy existující vrstvy přístupu k datům. Všechny úpravy lze provádět přímo na stránce `CategoriesAndProducts.aspx`. Začněte přidáním nového prvku ObjectDataSource s názvem `CategoriesDataSource` prostřednictvím inteligentní značky Repeater. Dále nakonfigurujte `CategoriesDataSource` ObjectDataSource tak, aby bylo načteno jeho data z metody `GetCategories()` `CategoriesBLL` třídy s.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal metodu CategoriesBLL třídy s GetCategories ()](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image7.png)

**Obrázek 3**: Konfigurace prvku ObjectDataSource pro použití `GetCategories()` metody `CategoriesBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image9.png))

V případě, že je třeba kliknout na každou položku v `Categories` Repeat, je nutné kliknout na možnost a při kliknutí na `CategoryProducts` DataList zobrazit tyto produkty pro vybranou kategorii. To se dá udělat tak, že každý z kategorií vytvoří hypertextový odkaz, propojí zpátky na stejnou stránku (`CategoriesAndProducts.aspx`), ale předává `CategoryID` přes QueryString, podobně jako jsme viděli v předchozím kurzu. Výhodou tohoto přístupu je, že stránka, která zobrazuje konkrétní kategorie produktů, může být záložkou a indexována vyhledávacím modulem.

Případně můžeme vytvořit každou kategorii a LinkButton, což je přístup, který budeme používat pro tento kurz. LinkButton vykreslí v prohlížeči uživatele jako hypertextový odkaz, ale při kliknutí vyvolá zpětné odeslání. Při zpětném volání se musí prvek DataList s ObjectDataSource aktualizovat, aby se zobrazily tyto produkty patřící do vybrané kategorie. Pro tento kurz, použití hypertextového odkazu, je vhodnější než použití LinkButton; v některých případech ale může být použití možnosti LinkButton výhodnější. I když by byl přístup k hypertextovým odkazům ideální pro tento příklad, místo toho se dá prozkoumat pomocí odkazu LinkButton. Jak vidíte, použití odkazu na čísle zavádí některé výzvy, které by jinak nevznikly hypertextovým odkazem. Proto použití položky LinkButton v tomto kurzu zvýrazní tyto výzvy a pomůže vám nabídnout řešení pro tyto scénáře, kde můžeme místo hypertextového odkazu použít LinkButton.

> [!NOTE]
> Doporučujeme, abyste tento kurz opakovali pomocí ovládacího prvku hypertextový odkaz nebo elementu `<a>` místo prvku LinkButton.

Následující kód ukazuje deklarativní syntaxi pro Repeater a ObjectDataSource. Všimněte si, že šablony Repeater vykreslují seznam s odrážkami s každou položkou jako LinkButton:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample4.aspx)]

> [!NOTE]
> Pro účely tohoto kurzu musí mít Repeater povolený stav zobrazení (Všimněte si opomenutí `EnableViewState="False"` z deklarativní syntaxe s opakováním). V kroku 3 vytvoříme obslužnou rutinu události pro událost Repeater `ItemCommand`, ve které budeme aktualizovat kolekci `SelectParameters` DataList s ObjectDataSource s. `ItemCommand`Repeat se ale neaktivuje, pokud je stav zobrazení zakázaný. Podívejte [se na stumper otázky ASP.NET](http://scottonwriting.net/sowblog/posts/1263.aspx) a [její řešení](http://scottonwriting.net/sowBlog/posts/1268.aspx) , kde najdete další informace o tom, proč je potřeba povolit stav zobrazení `ItemCommand` události Repeater.

LinkButton s hodnotou vlastnosti `ID` `ViewCategory` nemá nastavenou vlastnost `Text`. Pokud jsme chtěli zobrazit název kategorie, nastavili jsme vlastnost text deklarativně prostřednictvím syntaxe datových vazeb, například takto:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample5.aspx)]

Chceme ale zobrazit *Jak název kategorie s, tak počet* produktů, které patří do této kategorie. Tyto informace lze načíst z obslužné rutiny události Repeater `ItemDataBound` tím, že zavoláte metodu `GetCategoriesByProductID(categoryID)` `ProductBLL` třídy s a určíte, kolik záznamů je vráceno ve výsledném `ProductsDataTable`, jak ukazuje následující kód:

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample6.vb)]

Začneme tím, že zajistíme, že budeme znovu pracovat s datovou položkou (jejíž `ItemType` je `Item` nebo `AlternatingItem`), a pak odkazuje na `CategoriesRow` instanci, která je právě svázaná s aktuálním `RepeaterItem`. Dále určíme počet produktů pro tuto kategorii vytvořením instance třídy `ProductsBLL`, voláním její metody `GetCategoriesByProductID(categoryID)` a určením počtu vrácených záznamů pomocí vlastnosti `Count`. Nakonec `ViewCategory` LinkButton v šabloně ItemTemplate odkazuje na odkaz a jeho vlastnost `Text` je nastavena na *CategoryName* (*NumberOfProductsInCategory*), kde *NumberOfProductsInCategory* je formátováno jako číslo s nulovými desetinnými místy.

> [!NOTE]
> Alternativně jsme mohli přidat *funkci formátování* do třídy ASP.NET stránky s kódem na pozadí, která přijímá kategorie s `CategoryName` a `CategoryID` hodnoty a vrátí `CategoryName` zřetězené s počtem produktů v kategorii (podle určení voláním metody `GetCategoriesByProductID(categoryID)`). Výsledky takové funkce formátování mohou být deklarativně přiřazeny vlastnosti text LinkButton s, což nahrazuje nutnost obslužné rutiny události `ItemDataBound`. Další informace o používání funkcí formátování naleznete [v tématu použití templatefields v ovládacím prvku GridView](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) nebo [formátování prvku DataList a Repeater na základě kurzů dat](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md) .

Po přidání této obslužné rutiny události chvíli počkejte, než se stránka otestuje v prohlížeči. Všimněte si, že je každá kategorie uvedená v seznamu s odrážkami, zobrazuje název kategorie a počet produktů přidružených k této kategorii (viz obrázek 4).

[![se zobrazí všechny kategorie s názvem a počet produktů.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image10.png)

**Obrázek 4**: zobrazí se všechny kategorie s názvem a počet produktů ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image12.png)).

## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>Aktualizace`CategoriesDataTable`a`CategoriesTableAdapter`, aby obsahovaly počet produktů pro každou kategorii

Místo určení počtu produktů pro každou kategorii v rámci vazby na Repeater můžete tento proces zjednodušit úpravou `CategoriesDataTable` a `CategoriesTableAdapter` ve vrstvě přístupu k datům tak, aby tyto informace byly nativně zahrnuty. Abychom to dosáhli, je nutné přidat nový sloupec, který `CategoriesDataTable` k uložení počtu přidružených produktů. Chcete-li přidat nový sloupec do objektu DataTable, otevřete typovou datovou sadu (`App_Code\DAL\Northwind.xsd`), klikněte pravým tlačítkem myši na objekt DataTable, který chcete upravit, a vyberte možnost Přidat/sloupec. Přidat nový sloupec do `CategoriesDataTable` (viz obrázek 5).

[![přidat nový sloupec do CategoriesDataSource](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image13.png)

**Obrázek 5**: Přidání nového sloupce do `CategoriesDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image15.png))

Tím se přidá nový sloupec s názvem `Column1`, který můžete změnit pouhým zadáním jiného názvu. Přejmenujte tento nový sloupec na `NumberOfProducts`. Dále je potřeba nakonfigurovat tyto vlastnosti sloupce. Klikněte na nový sloupec a přejděte na okno Vlastnosti. Změňte vlastnost `DataType` sloupců z `System.String` na `System.Int32` a nastavte vlastnost `ReadOnly` na `True`, jak je znázorněno na obrázku 6.

![Nastavte vlastnosti DataType a ReadOnly nového sloupce.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image16.png)

**Obrázek 6**: nastavení vlastností `DataType` a `ReadOnly` nového sloupce

I když `CategoriesDataTable` nyní má sloupec `NumberOfProducts`, není jeho hodnota nastavena žádným z odpovídajících dotazů TableAdapter s. Metodu `GetCategories()` můžeme aktualizovat, aby vracela tyto informace, pokud chceme tyto informace vracet při každém načtení informací o kategoriích. Pokud ale potřebujeme jen přidružit počet přidružených produktů pro kategorie ve vzácných instancích (například jenom v tomto kurzu), můžeme ponechat `GetCategories()` tak, jak jsou, a vytvořit novou metodu, která vrátí tyto informace. Pojďme použít tento druhý přístup a vytvořit novou metodu s názvem `GetCategoriesAndNumberOfProducts()`.

Chcete-li přidat tuto novou metodu `GetCategoriesAndNumberOfProducts()`, klikněte pravým tlačítkem myši na `CategoriesTableAdapter` a vyberte možnost Nový dotaz. Tím se zobrazí Průvodce konfigurací dotazu TableAdapter, který jsme v předchozích kurzech používali mnohokrát. V případě této metody spusťte Průvodce tak, že je uvedeno, že dotaz používá příkaz SQL ad hoc, který vrací řádky.

[![vytvořit metodu pomocí ad-hoc příkazu SQL](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image17.png)

**Obrázek 7**: vytvoření metody pomocí ad-hoc příkazu SQL ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image19.png))

[![příkaz jazyka SQL vrátí řádky](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image20.png)

**Obrázek 8**: příkaz jazyka SQL vrací řádky ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image22.png))

Další obrazovka průvodce vás vyzve, aby se dotaz použil. Pokud chcete vrátit jednotlivé kategorie `CategoryID`, `CategoryName`a `Description`, spolu s počtem produktů přidružených k této kategorii, použijte následující příkaz `SELECT`:

[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample7.sql)]

[![zadejte dotaz, který se má použít.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image23.png)

**Obrázek 9**: určení dotazu, který se má použít ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image25.png))

Všimněte si, že poddotaz, který vypočítá počet produktů přidružených k této kategorii, má alias `NumberOfProducts`. Tato shoda názvů způsobí, že hodnota vrácená tímto poddotazem bude přidružena k sloupci `CategoriesDataTable` s `NumberOfProducts`.

Po zadání tohoto dotazu je posledním krokem výběr názvu nové metody. Pro naplnění objektu DataTable použijte `FillWithNumberOfProducts` a `GetCategoriesAndNumberOfProducts` a vraťte se ke vzorům DataTable.

[![název nové metody FillWithNumberOfProducts a GetCategoriesAndNumberOfProducts pro TableAdapter s](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image26.png)

**Obrázek 10**: pojmenujte nové metody TableAdapter s `FillWithNumberOfProducts` a `GetCategoriesAndNumberOfProducts` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image28.png)

V tomto okamžiku byla vrstva přístupu k datům rozšířena tak, aby obsahovala počet produktů na kategorii. Vzhledem k tomu, že všechny naše prezentační vrstvy směrují všechna volání na DAL prostřednictvím samostatné vrstvy obchodní logiky, musíme do `CategoriesBLL` třídy přidat odpovídající metodu `GetCategoriesAndNumberOfProducts`:

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample8.vb)]

Po dokončení a knihoven BLLi jsme připraveni tato data navážet do `Categories`ového opakovače v `CategoriesAndProducts.aspx`! Pokud jste již vytvořili prvek ObjectDataSource pro příkaz Repeater z části určení počtu produktů v sekci obslužné rutiny události `ItemDataBound`, odstraňte tento prvek ObjectDataSource a odeberte nastavení vlastnosti Repeater s `DataSourceID`; také odvedení události Repeater `ItemDataBound` z obslužné rutiny události odebráním syntaxe `Handles Categories.OnItemDataBound` ve třídě kódu na pozadí ASP.NET.

Pomocí návratového znaku zpět v původním stavu přidejte nový prvek ObjectDataSource s názvem `CategoriesDataSource` prostřednictvím inteligentní značky Repeater. Nakonfigurujte prvek ObjectDataSource tak, aby používal třídu `CategoriesBLL`, ale místo toho, aby používal metodu `GetCategories()`, mělo by místo toho použít `GetCategoriesAndNumberOfProducts()` (viz obrázek 11).

[![nakonfigurovat prvek ObjectDataSource na použití metody GetCategoriesAndNumberOfProducts](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image29.png)

**Obrázek 11**: Konfigurace prvku ObjectDataSource pro použití metody `GetCategoriesAndNumberOfProducts` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image31.png))

Dále aktualizujte `ItemTemplate` tak, aby vlastnost LinkButton s `Text` byla deklarativně přiřazena pomocí syntaxe DataBinding a obsahovala datová pole `CategoryName` a `NumberOfProducts`. Dokončení deklarativních značek pro Repeater a `CategoriesDataSource` ObjectDataSource následuje:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample9.aspx)]

Výstup vykreslený aktualizací hodnoty DAL za účelem zahrnutí sloupce `NumberOfProducts` je stejný jako při použití přístupu k obslužné rutině události `ItemDataBound` (vraťte se zpátky na obrázek 4, kde se zobrazí snímek obrazovky s názvem kategorie a počet produktů).

## <a name="step-3-displaying-the-selected-category-s-products"></a>Krok 3: zobrazení vybraných produktů kategorií s

V tomto okamžiku má `Categories` Repeater zobrazení seznamu kategorií spolu s počtem produktů v jednotlivých kategoriích. Repeater používá LinkButton pro každou kategorii, která při kliknutí způsobí postback, ve kterém je potřeba zobrazit tyto produkty pro vybranou kategorii v `CategoryProducts` DataList.

Jedna z nich čelí, jak má prvek DataList zobrazit pouze ty produkty pro vybranou kategorii. V seznamu [a podrobnostech pomocí selektivního hlavního prvku GridView s kurzem podrobností DetailsView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) jsme viděli, jak vytvořit prvek GridView, jehož řádky by se daly vybrat, s vybranými podrobnostmi o řádcích zobrazenými v ovládacím prvku DetailsView na stejné stránce. Prvek GridView s ObjectDataSource vrátil informace o všech produktech pomocí metody `GetProducts()` `ProductsBLL` s, zatímco ovládací prvek DetailsView s ObjectDataSource načetl informace o vybraném produktu pomocí metody `GetProductsByProductID(productID)`. Hodnota parametru *`productID`* byla k dispozici deklarativně tak, že ji přidružíte k hodnotě vlastnosti GridView s `SelectedValue`. Tento příkaz bohužel nemá vlastnost `SelectedValue` a nemůže sloužit jako zdroj parametru.

> [!NOTE]
> Toto je jeden z těchto výzev, které se zobrazí při použití prvku LinkButton v rámci Repeater. Použili jsme hypertextový odkaz k předání `CategoryID` prostřednictvím řetězce dotazu, můžeme použít toto pole QueryString jako zdroj hodnoty parametru s.

Předtím, než se obáváme o nedostatku `SelectedValue` vlastnosti pro Repeater, ale můžeme nejdřív navazovat vazby prvku DataList na prvek ObjectDataSource a zadat jeho `ItemTemplate`.

Z inteligentní značky DataList s Přihlaste se k přidání nového prvku ObjectDataSource s názvem `CategoryProductsDataSource` a nakonfigurujte ho tak, aby používal metodu `GetProductsByCategoryID(categoryID)` `ProductsBLL` třídy s. Vzhledem k tomu, že DataList v tomto kurzu nabízí rozhraní jen pro čtení, můžete nastavit rozevírací seznamy na kartách vložení, aktualizace a odstranění na (žádné).

[![nakonfigurovat prvek ObjectDataSource tak, aby používal metodu ProductsBLL třídy s GetProductsByCategoryID (KódKategorie)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image32.png)

**Obrázek 12**: Konfigurace prvku ObjectDataSource pro použití `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)` metoda ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image34.png))

Vzhledem k tomu, že metoda `GetProductsByCategoryID(categoryID)` očekává vstupní parametr ( *`categoryID`* ), Průvodce konfigurací zdroje dat nám umožňuje zadat parametr s parametrem source. Měly by se tyto kategorie vypisovat v prvku GridView nebo v prvku DataList, ale v rozevíracím seznamu zdroj parametrů se nastaví ovládací prvek a vlastnosti ControlID na `ID` webového ovládacího prvku data. Vzhledem k tomu, že u Repeater chybí vlastnost `SelectedValue`, nemůže být použit jako zdroj parametru. Pokud zkontrolujete, zjistíte, že rozevírací seznam ControlID obsahuje pouze jeden ovládací prvek `ID``CategoryProducts`, `ID` prvku DataList.

Prozatím nastavte rozevírací seznam zdroj parametrů na žádný. Pokud kliknete na položku LinkButton v poli Repeater, ukončíme programově přiřazení této hodnoty parametru.

[![nespecifikovat zdroj parametru pro parametr KódKategorie](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image35.png)

**Obrázek 13**: nezadávejte zdrojový parametr pro parametr *`categoryID`* ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image37.png)).

Po dokončení Průvodce konfigurací zdroje dat aplikace Visual Studio automaticky vygeneruje `ItemTemplate`DataList s. Nahraďte tento výchozí `ItemTemplate` šablonou, kterou jsme použili v předchozím kurzu. také nastavte vlastnost `RepeatColumns` DataList na 2. Po provedení těchto změn by deklarativní označení pro prvek DataList a jeho přidružené prvky ObjectDataSource mělo vypadat takto:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample10.aspx)]

V současné době není parametr `CategoryProductsDataSource` ObjectDataSource s *`categoryID`* nikdy nastaven, takže při zobrazení stránky se nezobrazí žádné produkty. To, co musíme udělat, je tato hodnota parametru nastavená na základě `CategoryID` kategorie kliknutí v poli Repeater. Tím se dokončí dvě výzvy: nejdřív určíme, kdy se na LinkButton `ItemTemplate` kliklo. a za druhé, jak můžeme určit `CategoryID` odpovídající kategorie, jejíž LinkButton byl kliknuto?

Prvek LinkButton, jako je tlačítko a ovládací prvky obrázkové, má událost `Click` a [událost`Command`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx). Událost `Click` je navržena tak, aby jednoduše poznamenala, že jste klikli na LinkButton. Někdy ale kromě toho, že jste klikli na položku LinkButton, ale také potřebujete předat nějaké další informace obslužné rutině události. Pokud se jedná o tento případ, vlastnosti LinkButton [`CommandName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx) a [`CommandArgument`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx) lze přiřadit k této dodatečné informaci. Pak při kliknutí na LinkButton se událost `Command` aktivuje (namísto události `Click`) a obslužná rutina události je předána hodnotami vlastností `CommandName` a `CommandArgument`.

Když je událost `Command` vyvolána v rámci šablony v Repeater, [událost repeater`ItemCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx) se aktivuje a předává se `CommandName` a `CommandArgument` hodnoty kliknutí na položku LinkButton (nebo tlačítko nebo obrázkové). Proto je potřeba provést následující akce, aby bylo možné určit, kdy došlo ke kliknutí na položku LinkButton kategorie v OPAKOVAČI:

1. Nastavte vlastnost `CommandName` prvku LinkButton v poli Repeater s `ItemTemplate` na určitou hodnotu (používá se ListProducts). Nastavením této `CommandName` hodnoty je při kliknutí na LinkButton aktivována událost `Command` LinkButton s.
2. Nastavte vlastnost LinkButton s `CommandArgument` na hodnotu `CategoryID`aktuální položky.
3. Vytvořte obslužnou rutinu události pro událost `ItemCommand` opakování. V obslužné rutině události nastavte `CategoryProductsDataSource` ObjectDataSource s `CategoryID` parametr na hodnotu `CommandArgument`předaného.

Následující `ItemTemplate` značky pro Repeater kategorií implementuje kroky 1 a 2. Všimněte si, jak je přiřazena hodnota `CommandArgument` datové položce s `CategoryID` pomocí syntaxe DataBinding:

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample11.aspx)]

Pokaždé, když se vytvoří obslužná rutina události `ItemCommand`, je obezřetná vždy, když chcete, aby se automaticky zkontrolovala hodnota příchozí `CommandName`, protože *jakákoli* `Command` událost vyvolaná *jakýmkoli* tlačítkem, LinkButton nebo obrázkové v rámci Repeater způsobí, že se událost `ItemCommand` aktivuje. V současné době máme jenom jednu takovou položku LinkButton. v budoucnu bychom (nebo jiný vývojář v našem týmu) mohli přidat další webové ovládací prvky tlačítek do tohoto opakovače, který po kliknutí vyvolá stejnou `ItemCommand` obslužnou rutinu události. Proto se nejlépe ujistěte, že jste zkontrolovali vlastnost `CommandName` a chcete pokračovat v programové logice, pokud se shoduje s očekávanou hodnotou.

Po zajistěte, aby se předaná hodnota `CommandName` rovna ListProducts, obslužná rutina události poté přiřadí parametr `CategoryProductsDataSource` ObjectDataSource s `CategoryID` k hodnotě předaného `CommandArgument`. Tato změna `SelectParameters` ObjectDataSource a automaticky způsobí, že prvek DataList se znovu sváže se zdrojem dat a zobrazí produkty pro nově vybranou kategorii.

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample12.vb)]

S těmito dodatky jsme náš kurz dokončili. Vyzkoušejte si chvilku, abyste ho otestovali v prohlížeči. Obrázek 14 zobrazuje obrazovku při první návštěvě stránky. Vzhledem k tomu, že se kategorie ještě vybrala, nezobrazí se žádné produkty. Kliknutím na kategorii, jako je například výroba, se zobrazí tyto produkty v kategorii produkt v zobrazení se dvěma sloupci (viz obrázek 15).

[Při první návštěvě stránky se nezobrazují ![žádné produkty.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image38.png)

**Obrázek 14**: při první návštěvě stránky nejsou zobrazeny žádné produkty ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image40.png)).

[![kliknutí na kategorii výroba zobrazí seznam vyhovujících produktů napravo.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image41.png)

**Obrázek 15**: kliknutím na kategorii výroba zobrazíte seznam vyhovujících produktů vpravo ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image43.png)

## <a name="summary"></a>Přehled

Jak jsme viděli v tomto kurzu a předchozí sestavy hlavní/podrobnosti je možné rozložit na dvě stránky nebo konsolidovat na jednu z nich. Zobrazení sestavy hlavní/podrobnosti na jedné stránce ale zavádí některé problémy s tím, jak nejlépe rozložení hlavního a podrobného záznamu na stránce. V seznamu *a podrobnostech pomocí selektivního hlavního prvku GridView s podrobným* kurzem k podrobnostem se zobrazí záznamy podrobností nad hlavními záznamy; v tomto kurzu jsme pomocí techniků CSS nastavili hlavní záznamy na levou stranu podrobností.

Společně s zobrazením sestav hlavních a podrobností jsme také pomohli prozkoumat, jak načíst počet produktů přidružených ke každé kategorii a jak provádět logiku na straně serveru při kliknutí na LinkButton (nebo tlačítko nebo obrázkové) v rámci Repeater.

V tomto kurzu se dokončí naše zkoumání sestav hlavní/podrobnosti s prvky DataList a Repeater. Naše další sada kurzů vám ukáže, jak přidat do ovládacího prvku DataList možnosti úprav a odstranění.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Floatutorial](http://css.maxdesign.com.au/floatutorial/) kurz pro plovoucí prvky CSS pomocí šablon stylů CSS
- [Šablony stylů CSS](http://www.brainjar.com/css/positioning/) – Další informace o umísťování elementů pomocí šablon stylů CSS
- [Rozložení obsahu pomocí jazyka HTML](http://www.w3schools.com/html/html_layout.asp) pomocí `<table>` s a dalších prvků HTML pro umístění

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor potenciálních zákazníků pro tento kurz byl Zack Novotný. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-detail-filtering-acess-two-pages-datalist-vb.md)
