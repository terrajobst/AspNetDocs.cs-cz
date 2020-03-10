---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
title: Vytvoření vlastního uživatelského rozhraní pro řazení (VB) | Microsoft Docs
author: rick-anderson
description: Když zobrazujete dlouhý seznam seřazených dat, může být velmi užitečné seskupovat související data zavedením oddělovacích řádků. V tomto kurzu si ukážeme, jak vytv...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: f3897a74-cc6a-4032-8f68-465f155e296a
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 66127630560141cd795beb15f525a7fba85f3993
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78619922"
---
# <a name="creating-a-customized-sorting-user-interface-vb"></a>Vytvoření vlastního uživatelského rozhraní pro řazení (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_VB.exe) nebo [Stáhnout PDF](creating-a-customized-sorting-user-interface-vb/_static/datatutorial27vb1.pdf)

> Když zobrazujete dlouhý seznam seřazených dat, může být velmi užitečné seskupovat související data zavedením oddělovacích řádků. V tomto kurzu se dozvíte, jak vytvořit takové uživatelské rozhraní pro řazení.

## <a name="introduction"></a>Úvod

Při zobrazení dlouhého seznamu seřazených dat, kde je v seřazeném sloupci pouze několik různých hodnot, může koncový uživatel zjistit, že je obtížné nerozlišuje, pokud přesně dojde k hranicím rozdílů. V databázi je například 81 produktů, ale pouze devět různých možností kategorií (osm jedinečných kategorií plus `NULL` možnost). Vezměte v úvahu případ uživatele, který má zájem o prověření produktů spadajících pod kategorii rybích plodů. Na stránce, která obsahuje seznam *všech* produktů v jednom prvku GridView, může uživatel podle svých nejlepších tipů seřadit výsledky podle kategorií, které dohromady seskupí všechny produkty z mořského moře. Po seřazení podle kategorií pak uživatel musí seznam prohledat a vyhledat, kde jsou produkty v produktech seskupené na začátku a na konci. Vzhledem k tomu, že se výsledky řadí abecedně podle názvu kategorie hledání produktů z mořských plodů, není obtížné, ale stále je potřeba, abyste pečlivě prohledali seznam položek v mřížce.

Aby bylo možné zvýraznit hranice mezi seřazenými skupinami, mnoho webů používá uživatelské rozhraní, které mezi těmito skupinami přidává oddělovač. Oddělovače jako ty, které jsou znázorněny na obrázku 1, umožňují uživateli rychleji najít konkrétní skupinu a identifikovat její hranice a také zjistit, jaké samostatné skupiny v datech existují.

[![je každá skupina kategorií jasně identifikovaná.](creating-a-customized-sorting-user-interface-vb/_static/image2.png)](creating-a-customized-sorting-user-interface-vb/_static/image1.png)

**Obrázek 1**: jasně se identifikují jednotlivé skupiny kategorií ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-customized-sorting-user-interface-vb/_static/image3.png)).

V tomto kurzu se dozvíte, jak vytvořit takové uživatelské rozhraní pro řazení.

## <a name="step-1-creating-a-standard-sortable-gridview"></a>Krok 1: vytvoření standardního, seřaditelné GridView

Předtím, než se podíváme, jak rozšířit prvek GridView, aby poskytovalo vylepšené rozhraní pro řazení, je nejdříve potřeba vytvořit standardní, řazený prvek GridView, který obsahuje seznam produktů. Začněte tím, že otevřete stránku `CustomSortingUI.aspx` ve složce `PagingAndSorting`. Přidejte prvek GridView na stránku, nastavte jeho vlastnost `ID` na `ProductList`a navažte jej na nový prvek ObjectDataSource. Nakonfigurujte prvek ObjectDataSource tak, aby pro výběr záznamů používal metodu `ProductsBLL` třídy s `GetProducts()`.

Dále nakonfigurujte prvek GridView tak, že obsahuje pouze `ProductName`, `CategoryName`, `SupplierName`a `UnitPrice` BoundFields a ukončený třídě CheckBoxField podporována. Nakonec nakonfigurujte prvek GridView tak, aby podporoval řazení, zaškrtnutím políčka Povolit řazení v inteligentní značce GridView s (nebo nastavením jeho vlastnosti `AllowSorting` na `true`). Po provedení těchto dodatků na stránce `CustomSortingUI.aspx` by deklarativní označení mělo vypadat podobně jako následující:

[!code-aspx[Main](creating-a-customized-sorting-user-interface-vb/samples/sample1.aspx)]

Chvíli si můžete prohlédnout v prohlížeči. Obrázek 2 znázorňuje řazený prvek GridView, pokud jsou jeho data seřazená podle kategorie v abecedním pořadí.

[![seřaditelné údaje prvku GridView seřazené podle kategorie](creating-a-customized-sorting-user-interface-vb/_static/image5.png)](creating-a-customized-sorting-user-interface-vb/_static/image4.png)

**Obrázek 2**: seřaditelné data GridView s jsou seřazená podle kategorií ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-customized-sorting-user-interface-vb/_static/image6.png)

## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>Krok 2: zkoumání techniků pro přidání oddělovacích řádků

S obecným řazením prvku GridView, který je kompletní, je možné přidat oddělovací řádky do prvku GridView před každou jedinečnou seřazenou skupinu. Ale jak mohou být tyto řádky vloženy do prvku GridView? V podstatě potřebujeme iterovat řádky GridView s, určit, kde rozdíly nastávají mezi hodnotami v seřazeném sloupci, a pak přidat příslušný oddělovací řádek. Při zvažování tohoto problému se jeví jako přirozené, že toto řešení je někde v obslužné rutině ovládacího prvku GridView s `RowDataBound`. Jak jsme probrali v kurzu pro [data na základě vlastního formátování](../custom-formatting/custom-formatting-based-upon-data-vb.md) , tato obslužná rutina se běžně používá při použití formátování na úrovni řádků na základě dat řádku s. Nicméně obslužná rutina události `RowDataBound` zde není řešení, protože řádky nelze do prvku GridView přidat programově z této obslužné rutiny události. Kolekce GridView `Rows`, ve skutečnosti je určena jen pro čtení.

Chcete-li přidat další řádky do prvku GridView, máme tři možnosti:

- Přidejte tyto řádky oddělovače metadat do skutečných dat, která jsou svázána s prvku GridView.
- Po svázání prvku GridView s daty přidejte další `TableRow` instance do kolekce ovládacích prvků GridView.
- Vytvoření vlastního serverového ovládacího prvku, který rozšiřuje ovládací prvek GridView a přepisuje tyto metody zodpovědné za vytváření struktury GridView.

Vytvoření vlastního serverového ovládacího prvku by představovalo nejlepší přístup, pokud byla tato funkce nutná na mnoho webových stránek nebo napříč několika weby. Nicméně by to znamenalo poměrně bitovou část kódu a důkladně prozkoumání hloubky interních pracovních prvků GridView. Proto tuto možnost tohoto kurzu nepovažujeme.

Další dvě možnosti přidávají oddělovací řádky do skutečných dat svázaných s ovládacím prvkem GridView a manipulaci s kolekcí ovládacích prvků GridView s po provázání útoku na problém, a to jinak.

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>Přidání řádků do dat vázaných na prvek GridView.

Když je prvek GridView svázán se zdrojem dat, vytvoří `GridViewRow` pro každý záznam vrácený zdrojem dat. Proto můžeme vložit oddělovací řádky do zdroje dat před jeho vytvořením do prvku GridView. Tento koncept znázorňuje obrázek 3.

![Jedna technika zahrnuje Přidání oddělovacích řádků do zdroje dat.](creating-a-customized-sorting-user-interface-vb/_static/image7.png)

**Obrázek 3**: jedna technika zahrnuje Přidání oddělovacích řádků do zdroje dat.

Používám záznamy oddělovačů termínů v uvozovkách, protože neexistují žádné speciální záznamy oddělovače; místo toho je nutné označit, že konkrétní záznam ve zdroji dat slouží jako oddělovač, nikoli normální datový řádek. V našem příkladu jsme znovu navážeme instanci `ProductsDataTable` na prvek GridView, který se skládá z `ProductRows`. Záznam můžete označit jako oddělovací řádek tím, že nastavíte jeho vlastnost `CategoryID` na `-1` (protože taková hodnota nepatří do normálního stavu).

K využití této techniky potřebujeme provést následující kroky:

1. Programově načte data pro svázání s prvku GridView (instance `ProductsDataTable`)
2. Seřazení dat na základě `SortExpression` a `SortDirection` vlastností prvků GridView.
3. Iterujte pomocí `ProductsRows` v `ProductsDataTable`a vyhledejte, kde se rozdíly v seřazeném sloupci naleží.
4. V každé hranici skupiny zasuňte záznam oddělovače `ProductsRow` instanci do objektu DataTable, což má `CategoryID` nastavenou na `-1` (nebo jakékoli označení bylo rozhodnuto, že označí záznam jako záznam oddělovače).
5. Po vložení oddělovacích řádků programově Navažte data na prvek GridView.

Kromě těchto pěti kroků je také potřeba poskytnout obslužnou rutinu události pro `RowDataBound` událost GridView. V tomto případě zkontrolujeme každé `DataRow` a určíme, jestli se jednalo o oddělovací řádek, jehož `CategoryID` nastavení bylo `-1`. V takovém případě je pravděpodobné, že budete chtít upravit jeho formátování nebo text zobrazený v buňkách.

Použití této techniky pro vložení hranic skupiny řazení vyžaduje trochu větší práci, než je uvedeno výše, protože je třeba zadat také obslužnou rutinu události `Sorting` události GridView. a sledovat `SortExpression` a `SortDirection` hodnoty.

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>Manipulace s kolekcí ovládacích prvků GridView s, jakmile byla svázána s daty

Místo odeslání dat před jejich navázáním na prvek GridView můžeme přidat oddělovací řádky *poté, co* byla data svázána s ovládacím prvek GridView. Proces vázání dat sestaví hierarchii ovládacího prvku GridView s, která ve skutečnosti je jednoduše `Table` instance složená z kolekce řádků, z nichž každá je tvořena kolekcí buněk. Konkrétně kolekce ovládacích prvků GridView s obsahuje objekt `Table` ve svém kořenu, `GridViewRow` (která je odvozena od třídy `TableRow`) pro každý záznam v `DataSource` vázaný na prvek GridView a objekt `TableCell` v každé instanci `GridViewRow` pro každé datové pole v `DataSource`.

Chcete-li přidat oddělovací řádky mezi každou skupinu řazení, můžeme tuto hierarchii ovládacích prvků po vytvoření přímo manipulovat. Můžeme si být jistí, že hierarchie ovládacích prvků GridView s byla vytvořena pro poslední čas podle času vykreslování stránky. Proto tento přístup přepíše metodu `Page` třídy s `Render`, při které je poslední hierarchie ovládacího prvku GridView s aktualizována tak, aby obsahovala potřebné oddělovací řádky. Obrázek 4 znázorňuje tento proces.

[![alternativním technika pracuje s hierarchií ovládacího prvku GridView.](creating-a-customized-sorting-user-interface-vb/_static/image9.png)](creating-a-customized-sorting-user-interface-vb/_static/image8.png)

**Obrázek 4**: alternativní technika pracuje s hierarchií ovládacího prvku GridView s ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-customized-sorting-user-interface-vb/_static/image10.png)).

Pro účely tohoto kurzu použijeme tento druhý postup k přizpůsobení prostředí pro řazení uživatelů.

> [!NOTE]
> Kód I m prezentující v tomto kurzu vychází z příkladu uvedeného v záznamu blogu [Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) s, který [hraje bit pomocí seskupení řazení GridView](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx).

## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>Krok 3: Přidání oddělovacích řádků do hierarchie ovládacího prvku GridView.

Vzhledem k tomu, že chcete přidat oddělovací řádky do hierarchie ovládacího prvku GridView. poté, co byla její hierarchie ovládacího prvku vytvořena a vytvořena pro poslední stránku na této stránce, chceme tento postup doplnit na konci životního cyklu stránky, ale před skutečným prvkem GridView c hierarchie ojů byla vykreslena do kódu HTML. Nejnovější možný bod, ve kterém můžeme dosáhnout, je `Page` třídy s `Render` události, kterou můžeme přepsat v naší třídě s kódem na pozadí pomocí následující signatury metody:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample2.vb)]

Při vyvolání původní metody `Render` `Page` třídy s `base.Render(writer)` všechny ovládací prvky na stránce budou vykresleny, generování značek na základě jejich hierarchie ovládacích prvků. Proto je nutné, aby oba volali `base.Render(writer)`, aby se stránka vykreslila a před voláním `base.Render(writer)`spolupracujeme s hierarchií ovládacího prvku GridView., takže řádky oddělovače byly přidány do hierarchie ovládacího prvku GridView s před jejich vykreslením.

Aby bylo možné vložit záhlaví skupin pro řazení, nejdřív je potřeba zajistit, aby si uživatel vyžádal, aby se data seřadila. Ve výchozím nastavení nejsou setříděny obsahy prvku GridView, a proto není nutné zadávat záhlaví skupin řazení.

> [!NOTE]
> Chcete-li, aby byl ovládací prvek GridView seřazen podle konkrétního sloupce při prvním načtení stránky, zavolejte metodu GridView s `Sort` na první stránce na webu (ale ne při následném postbacku). Chcete-li toho dosáhnout, přidejte toto volání do obslužné rutiny události `Page_Load` v rámci `if (!Page.IsPostBack)` podmíněný. Další informace o metodě `Sort` najdete v tématu informace o kurzu [stránkování a řazení dat sestavy](paging-and-sorting-report-data-vb.md) .

Za předpokladu, že data byla seřazena, je dalším úkolem, jak určit sloupec, podle kterého byla data seřazena, a následně vyhledat řádky, které hledají rozdíly v těchto hodnotách sloupce. Následující kód zajišťuje řazení dat a vyhledá sloupec, podle kterého byla data seřazena:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample3.vb)]

Pokud prvek GridView již má být seřazen, vlastnost GridView s `SortExpression` nebude nastavena. Proto chceme přidat oddělovací řádky pouze v případě, že má tato vlastnost nějakou hodnotu. V takovém případě je potřeba určit index sloupce, podle kterého se data seřadila. To se provádí smyčkou pomocí `Columns` kolekce GridView. vyhledá sloupec, jehož vlastnost `SortExpression` se rovná vlastnosti GridView s `SortExpression`. Kromě indexu sloupce je také k dispozici vlastnost `HeaderText`, která se používá při zobrazení oddělovacích řádků.

Pomocí indexu sloupce, podle kterého jsou data seřazena, je posledním krokem vytvoření výčtu řádků prvku GridView. U každého řádku potřebujeme určit, jestli se hodnota seřazeného sloupce liší od předchozí hodnoty seřazeného sloupce s předchozími řádky. V takovém případě musíme vložit novou instanci `GridViewRow` do hierarchie ovládacích prvků. Toho je možné dosáhnout pomocí následujícího kódu:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample4.vb)]

Tento kód začíná programově odkazující na objekt `Table`, který se nachází v kořenovém adresáři hierarchie ovládacího prvku GridView s a vytváří řetězcovou proměnnou s názvem `lastValue`. `lastValue` slouží k porovnání aktuální hodnoty seřazeného sloupce s předchozími hodnotami řádku s. V dalším kroku je vyhodnocena kolekce `Rows` prvku GridView a pro každý řádek je hodnota seřazeného sloupce uložena v proměnné `currentValue`.

> [!NOTE]
> Chcete-li určit hodnotu konkrétního sloupce s seřazenými řádky, použijte vlastnost `Text` buňky. To funguje dobře pro BoundFields, ale nebude fungovat podle potřeby pro TemplateField, CheckBoxFields a tak dále. Podíváme se, jak brzy připravujeme alternativní pole GridView.

Proměnné `currentValue` a `lastValue` jsou pak porovnány. Pokud se liší, je nutné přidat nový řádek oddělovače do hierarchie ovládacích prvků. Toho je možné dosáhnout určením indexu `GridViewRow` v kolekci `Table` objektů `Rows`, vytvořením nových `GridViewRow` a `TableCell` instancí a následným přidáním `TableCell` a `GridViewRow` do hierarchie ovládacích prvků.

Všimněte si, že oddělovací řádka s jedinou `TableCell` je formátována tak, aby byla rozložena k celé šířce prvku GridView, je formátována pomocí `SortHeaderRowStyle` třídy šablony stylů CSS a má vlastnost `Text` tak, aby zobrazila název skupiny řazení (například kategorie) a hodnotu skupiny (například nápoje). Nakonec se `lastValue` aktualizuje na hodnotu `currentValue`.

Třída CSS použitá k formátování řádku záhlaví skupiny řazení `SortHeaderRowStyle` musí být zadána v souboru `Styles.css`. Nebojte se použít jakékoli odvolání nastavení stylu. Použil (a) jsem následující:

[!code-css[Main](creating-a-customized-sorting-user-interface-vb/samples/sample5.css)]

Pomocí aktuálního kódu přiřadí rozhraní řazení záhlaví skupin řazení při řazení podle libovolného vlastnost BoundField (viz obrázek 5, který zobrazuje snímek obrazovky při řazení podle dodavatele). Ale při řazení podle jiného typu pole (například třídě CheckBoxField podporována nebo TemplateField) se záhlaví skupiny řazení nikde, které se mají najít (viz obrázek 6).

[![rozhraní řazení zahrnuje záhlaví skupin při řazení podle BoundFields](creating-a-customized-sorting-user-interface-vb/_static/image12.png)](creating-a-customized-sorting-user-interface-vb/_static/image11.png)

**Obrázek 5**: rozhraní řazení zahrnuje záhlaví skupin při řazení podle BoundFields ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-customized-sorting-user-interface-vb/_static/image13.png)

[![při řazení třídě CheckBoxField podporována chybí záhlaví skupiny řazení](creating-a-customized-sorting-user-interface-vb/_static/image15.png)](creating-a-customized-sorting-user-interface-vb/_static/image14.png)

**Obrázek 6**: při řazení třídě CheckBoxField podporována chybí záhlaví skupiny řazení ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-customized-sorting-user-interface-vb/_static/image16.png)).

Důvod, proč chybí záhlaví skupiny řazení při řazení podle třídě CheckBoxField podporována, je, že kód aktuálně používá pouze vlastnost `Text` `TableCell` s k určení hodnoty seřazeného sloupce pro každý řádek. Pro CheckBoxFields je vlastnost `Text` `TableCell` s prázdným řetězcem. místo toho je tato hodnota k dispozici prostřednictvím webového ovládacího prvku CheckBox, který se nachází v kolekci `TableCell` s `Controls`.

Abychom mohli zpracovávat jiné typy polí než BoundFields, musíme rozšířit kód, kde je přiřazena proměnná `currentValue` pro kontrolu existence zaškrtávacího políčka v kolekci `TableCell` s `Controls`. Místo použití `currentValue = gvr.Cells(sortColumnIndex).Text`nahraďte tento kód následujícím kódem:

[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample6.vb)]

Tento kód prověřuje seřazený sloupec `TableCell` pro aktuální řádek k určení, zda existují ovládací prvky v kolekci `Controls`. Pokud existují a prvním ovládacím prvkem zaškrtávací políčko, je proměnná `currentValue` v závislosti na vlastnosti `Checked` CheckBoxs nastavena na hodnotu yes nebo No. V opačném případě se hodnota převezme z vlastnosti `TableCell` s `Text`. Tuto logiku lze replikovat pro zpracování řazení pro jakékoli pole TemplateField, která mohou existovat v prvku GridView.

S výše uvedeným kódem jsou nyní k dispozici záhlaví skupin pro řazení při řazení podle třídě CheckBoxField podporovánach ukončených (viz obrázek 7).

[![se při řazení třídě CheckBoxField podporována k dispozici záhlaví skupin řazení.](creating-a-customized-sorting-user-interface-vb/_static/image18.png)](creating-a-customized-sorting-user-interface-vb/_static/image17.png)

**Obrázek 7**: při řazení třídě CheckBoxField podporována jsou teď k dispozici záhlaví skupin pro řazení ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-customized-sorting-user-interface-vb/_static/image19.png)

> [!NOTE]
> Pokud máte produkty s `NULL` hodnotami databáze pro pole `CategoryID`, `SupplierID`nebo `UnitPrice`, budou se tyto hodnoty ve výchozím nastavení zobrazovat jako prázdné řetězce v prvku GridView, což znamená, že text oddělovače pro tyto produkty s `NULL` hodnotami se načtou jako kategorie: (to znamená, že za kategorií: nápoje nejsou žádné názvy). Pokud chcete zobrazit hodnotu, můžete buď nastavit [vlastnost BoundFields`NullDisplayText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx) na text, který chcete zobrazit, nebo můžete přidat podmíněný příkaz do metody Render při přiřazování `currentValue` k vlastnosti `Text` oddělovače řádků.

## <a name="summary"></a>Souhrn

Prvek GridView nezahrnuje mnoho předdefinovaných možností pro přizpůsobení rozhraní řazení. Nicméně s bitovou úrovní kódu na nízké úrovni je možné upravit hierarchii ovládacího prvku GridView s a vytvořit přizpůsobené rozhraní. V tomto kurzu jsme viděli, jak přidat řádek oddělovače skupiny řazení pro řazený prvek GridView, který snadněji identifikuje samostatné skupiny a tyto skupiny. Další příklady přizpůsobených rozhraní řazení najdete v části [Scott Guthrie](https://weblogs.asp.net/scottgu/) s [pár ASP.NET 2,0 GridView – tipy a položky blogu s triky pro řazení](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx) .

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](sorting-custom-paged-data-vb.md)
