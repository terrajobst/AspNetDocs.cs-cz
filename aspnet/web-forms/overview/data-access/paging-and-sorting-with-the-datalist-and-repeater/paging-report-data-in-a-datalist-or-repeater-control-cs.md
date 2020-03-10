---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
title: Stránkování dat sestavy v ovládacím prvku DataList nebo Repeater (C#) | Microsoft Docs
author: rick-anderson
description: I když prvek DataList ani Repeater nenabízí podporu automatického stránkování nebo řazení, v tomto kurzu se dozvíte, jak přidat podporu stránkování do prvku DataList nebo Repeater,...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: e8e0809b-25c4-4c3b-8d12-9a17048148ae
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 16686c7e41926698c0da9c60d3cf26e858f5daca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78620636"
---
# <a name="paging-report-data-in-a-datalist-or-repeater-control-c"></a>Stránkování dat sestavy ovládacími prvky DataList nebo Repeater (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_CS.exe) nebo [Stáhnout PDF](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial44cs1.pdf)

> I když prvek DataList ani Repeater nenabízí automatickou podporu stránkování nebo řazení, tento kurz ukazuje, jak přidat podporu stránkování do prvku DataList nebo Repeater, což umožňuje mnohem flexibilnější rozhraní pro zobrazení stránkování a dat.

## <a name="introduction"></a>Úvod

Stránkování a řazení jsou dvě velmi běžné funkce při zobrazování dat v online aplikaci. Například při hledání ASP.NET knih v online knihkupectví mohou existovat stovky takových knih, ale v sestavě se seznamem výsledků hledání se zobrazí pouze deset shod na jednu stránku. Kromě toho je možné výsledky seřadit podle názvu, ceny, počtu stránek, jména autora atd. Jak jsme probrali v kurzu [stránkování a řazení dat sestavy](../paging-and-sorting/paging-and-sorting-report-data-cs.md) , ovládací prvky GridView, DetailsView a FormView poskytují integrovanou podporu stránkování, kterou lze povolit při zaškrtnutí políčka. Prvek GridView také zahrnuje podporu řazení.

Prvek DataList ani Repeater však nenabízí podporu automatického stránkování ani řazení. V tomto kurzu podíváme se, jak přidat podporu stránkování do prvku DataList nebo Repeater. Je nutné ručně vytvořit rozhraní stránkování, zobrazit příslušnou stránku záznamů a zapamatovat si stránku navštívené napříč zpětnými voláními. I když to trvá více času a kódu než u prvku GridView, DetailsView nebo FormView, prvky DataList a Repeater umožňují mnohem pružnější rozhraní pro zobrazení stránkování a dat.

> [!NOTE]
> Tento kurz se zaměřuje výhradně na stránkování. V dalším kurzu budeme věnovat pozornost přidávání možností řazení.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>Krok 1: Přidání webových stránek kurzu stránkování a seřazení

Před zahájením tohoto kurzu si nejdřív počkejte, než se přidá stránky ASP.NET, které budeme potřebovat pro tento kurz a druhý. Začněte vytvořením nové složky v projektu s názvem `PagingSortingDataListRepeater`. V dalším kroku přidejte do této složky následující pět ASP.NET stránek a všechny je nakonfigurované tak, aby používaly stránku předlohy `Site.master`:

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`

![Vytvořte složku PagingSortingDataListRepeater a přidejte stránky ASP.NET kurzu.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**Obrázek 1**: vytvoření složky pro `PagingSortingDataListRepeater` a přidání ASP.NETových stránek kurzu

Potom otevřete stránku `Default.aspx` a přetáhněte uživatelský ovládací prvek `SectionLevelTutorialListing.ascx` ze složky `UserControls` na návrhovou plochu. Tento uživatelský ovládací prvek, který jsme vytvořili v kurzu [hlavní stránky a navigace na webu](../introduction/master-pages-and-site-navigation-cs.md) , vytvoří výčet mapy lokality a v aktuálním oddílu zobrazí v seznamu s odrážkami kurzy.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image4.png))

Aby se v seznamu s odrážkami zobrazovaly kurzy stránkování a řazení, vytvoříme, že je musíme přidat k mapě webu. Otevřete soubor `Web.sitemap` a přidejte následující kód po úpravách a odstraňování pomocí značek uzlu mapy webu DataList:

[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample1.xml)]

![Aktualizovat mapu webu tak, aby obsahovala nové stránky ASP.NET](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)

**Obrázek 3**: aktualizace mapy webu tak, aby obsahovala nové stránky ASP.NET

## <a name="a-review-of-paging"></a>Kontrola stránkování

V předchozích kurzech jsme viděli, jak procházet data v ovládacích prvcích GridView, DetailsView a FormView. Tyto tři ovládací prvky nabízejí jednoduchou formu stránkování s názvem *výchozí stránkování* , které lze implementovat pouhým zaškrtnutím možnosti Povolit stránkování v inteligentní značce ovládacího prvku. Při výchozím stránkování se při každém vyžádání stránky dat buď na první stránce navštíví, nebo když uživatel přejde na jinou stránku dat, ovládací prvek GridView, DetailsView nebo FormView znovu vyžádá *všechna* data z prvku ObjectDataSource. Pak vystřihá konkrétní sadu záznamů, které se zobrazí podle požadovaného indexu stránky a počtu záznamů, které se mají zobrazit na stránce. Podrobněji jsme probrali výchozí stránkování v kurzu [stránkování a řazení dat sestavy](../paging-and-sorting/paging-and-sorting-report-data-cs.md) .

Vzhledem k tomu, že výchozí stránkování znovu vyžádá všechny záznamy pro každou stránku, není praktické při stránkování po dostatečně velkých objemech dat. Představte si třeba stránkování prostřednictvím 50 000 záznamů s velikostí stránky 10. Pokaždé, když se uživatel přesune na novou stránku, musí se z databáze načíst všechny záznamy 50 000, i když se zobrazí jenom deset z nich.

*Vlastní stránkování* řeší problémy s výkonem výchozích stránkování tím, že z požadované stránky zobrazí jenom přesnou podmnožinu záznamů. Při implementaci vlastního stránkování je nutné zapsat dotaz SQL, který bude efektivně vracet pouze správnou sadu záznamů. Zjistili jsme, jak tento dotaz vytvořit pomocí SQL Server 2005 s novými [`ROW_NUMBER()` klíčovým slovem](http://www.4guysfromrolla.com/webtech/010406-1.shtml) pro [efektivní stránkování prostřednictvím velkých objemů dat](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) .

Chcete-li implementovat výchozí stránkování v ovládacím prvku DataList nebo Repeater, můžeme použít [třídu`PagedDataSource`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx) jako obálku kolem `ProductsDataTable`, jejichž obsah je právě stránkovaný. Třída `PagedDataSource` má vlastnost `DataSource`, kterou lze přiřadit k jakémukoli vyčíslitelnému objektu a [`PageSize`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx) a [`CurrentPageIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx) vlastností, které určují, kolik záznamů má být zobrazeno na stránce a v indexu aktuální stránky. Po nastavení těchto vlastností lze `PagedDataSource` použít jako zdroj dat libovolného webového ovládacího prvku dat. `PagedDataSource`při výčtu vrátí pouze příslušnou podmnožinu záznamů své vnitřní `DataSource` na základě vlastností `PageSize` a `CurrentPageIndex`. Obrázek 4 znázorňuje funkčnost `PagedDataSource` třídy.

![PagedDataSource zalomí Vyčíslitelného objektu pomocí stránkovaného rozhraní.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image6.png)

**Obrázek 4**: `PagedDataSource` zabalí vyčíslitelné objekt s použitím stránkovaného rozhraní.

Objekt `PagedDataSource` lze vytvořit a nakonfigurovat přímo z vrstvy obchodní logiky a vázat na prvek DataList nebo Repeater prostřednictvím prvku ObjectDataSource, nebo jej lze vytvořit a nakonfigurovat přímo ve třídě ASP.NET stránky s kódem na pozadí. Je-li použit druhý přístup, je nutné použít prvek ObjectDataSource a místo toho navazovat stránkovaná data na prvky DataList nebo Repeater programově.

Objekt `PagedDataSource` obsahuje také vlastnosti pro podporu vlastního stránkování. Můžeme však obejít použití `PagedDataSource` pro vlastní stránkování, protože již máme metody knihoven BLL ve třídě `ProductsBLL` navržené pro vlastní stránkování, které vrací přesné záznamy k zobrazení.

V tomto kurzu se podíváme na implementaci výchozího stránkování v prvku DataList přidáním nové metody do třídy `ProductsBLL`, která vrací vhodně nakonfigurovaný `PagedDataSource` objekt. V dalším kurzu uvidíme, jak používat vlastní stránkování.

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>Krok 2: přidání výchozí metody stránkování do vrstvy obchodní logiky

Třída `ProductsBLL` v současnosti obsahuje metodu pro vrácení všech informací o produktu `GetProducts()` a jednu pro vrácení konkrétní podmnožiny produktů v počátečním indexu `GetProductsPaged(startRowIndex, maximumRows)`. S výchozím stránkováním ovládací prvky GridView, DetailsView a FormView používají metodu `GetProducts()` k načtení všech produktů, ale pak používají `PagedDataSource` interně k zobrazení pouze správné podmnožiny záznamů. Chcete-li replikovat tuto funkci s ovládacími prvky DataList a Repeater, můžeme v knihoven BLL vytvořit novou metodu, která napodobuje toto chování.

Přidejte metodu do třídy `ProductsBLL` s názvem `GetProductsAsPagedDataSource`, která přijímá dva vstupní parametry typu Integer:

- `pageIndex` index zobrazované stránky, indexované na nulu a
- `pageSize` počet záznamů, které se mají zobrazit na stránce.

`GetProductsAsPagedDataSource` spustí načtením *všech* záznamů z `GetProducts()`. Potom vytvoří objekt `PagedDataSource`, nastaví jeho `CurrentPageIndex` a `PageSize` vlastnosti na hodnoty předaných `pageIndex` a `pageSize` parametrů. Metoda se dokončí vrácením tohoto nakonfigurovaného `PagedDataSource`:

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>Krok 3: zobrazení informací o produktu v prvku DataList pomocí výchozí stránkování

Pomocí metody `GetProductsAsPagedDataSource` přidané do `ProductsBLL` třídy teď můžeme vytvořit prvek DataList nebo Repeater, který poskytuje výchozí stránkování. Začněte otevřením stránky `Paging.aspx` ve složce `PagingSortingDataListRepeater` a přetažením prvku DataList z panelu nástrojů do návrháře, nastavením vlastnosti `ID` prvku DataList na `ProductsDefaultPaging`. Z inteligentní značky DataList a vytvořte nový prvek ObjectDataSource s názvem `ProductsDefaultPagingDataSource` a nakonfigurujte jej tak, aby načítat data pomocí metody `GetProductsAsPagedDataSource`.

[![vytvořit prvek ObjectDataSource a nakonfigurovat jej pro použití metody GetProductsAsPagedDataSource ()](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**Obrázek 5**: Vytvoření prvku ObjectDataSource a jeho konfigurace pro použití metody `GetProductsAsPagedDataSource` `()` ([kliknutím zobrazíte obrázek v plné velikosti](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image9.png))

Nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné).

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**Obrázek 6**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))

Vzhledem k tomu, že metoda `GetProductsAsPagedDataSource` očekává dva vstupní parametry, Průvodce vás vyzve ke zdroji těchto hodnot parametrů.

Hodnoty indexu stránky a velikosti stránky musí být zapamatovatelné napříč zpětnými odesláními. Mohou být uloženy ve stavu zobrazení, uloženy do řetězce dotazu QueryString, uloženy v proměnných relace nebo zachovány pomocí nějaké jiné techniky. Pro účely tohoto kurzu použijeme dotaz QueryString, který má výhodu povolit záložku konkrétní stránky dat.

Konkrétně použijte pole QueryString pageIndex a pageSize pro parametry `pageIndex` a `pageSize` v uvedeném pořadí (viz obrázek 7). Chvíli počkejte, než nastavíte výchozí hodnoty pro tyto parametry, protože hodnoty QueryString nebudou k dispozici, když uživatel poprvé navštíví tuto stránku. Pro `pageIndex`nastavte výchozí hodnotu na 0 (která bude zobrazovat první stránku dat) a výchozí hodnotu `pageSize` s na 4.

[![použít řetězec QueryString jako zdroj pro parametry pageIndex a pageSize](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**Obrázek 7**: použijte řetězec QueryString jako zdroj pro parametry `pageIndex` a `pageSize` ([kliknutím zobrazíte obrázek v plné velikosti).](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image15.png)

Po nakonfigurování prvku ObjectDataSource aplikace Visual Studio automaticky vytvoří `ItemTemplate` pro prvek DataList. Přizpůsobte `ItemTemplate` tak, aby se zobrazil jenom název produktu, kategorie a dodavatel. Nastavte také vlastnost `RepeatColumns` prvku DataList na hodnotu 2, její `Width` na 100% a její `ItemStyle` s `Width` na 50%. Tato nastavení šířky budou pro tyto dva sloupce obsahovat stejné mezery.

Po provedení těchto změn by značka DataList a ObjectDataSource s vypadala podobně jako v následujícím příkladu:

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

> [!NOTE]
> Vzhledem k tomu, že v tomto kurzu neprovádíme žádné funkce Update nebo DELETE, můžete zakázat stav zobrazení DataList s, aby se snížila velikost vykreslené stránky.

Při počáteční návštěvě této stránky v prohlížeči nejsou k dispozici parametry `pageIndex` ani `pageSize` QueryString. Proto se použijí výchozí hodnoty 0 a 4. Jak ukazuje obrázek 8, výsledkem je prvek DataList, který zobrazuje první čtyři produkty.

[Zobrazí se ![prvních čtyř produktů.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)

**Obrázek 8**: Seznam prvních čtyř produktů ([kliknutím zobrazíte obrázek v plné velikosti](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image18.png))

Bez rozhraní stránkování teď neexistuje žádný jednoduchý způsob, jak uživatel přejít na druhou stránku dat. V kroku 4 vytvoříme rozhraní stránkování. V současné době může být stránkování provedeno pouze přímým určením kritérií stránkování v řetězci dotazu. Chcete-li například zobrazit druhou stránku, změňte adresu URL v adresním řádku prohlížeče z `Paging.aspx` na `Paging.aspx?pageIndex=2` a stiskněte klávesu ENTER. To způsobí zobrazení druhé stránky dat (viz obrázek 9).

[![se zobrazí druhá stránka dat](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)

**Obrázek 9**: zobrazí se druhá stránka dat ([kliknutím zobrazíte obrázek v plné velikosti).](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)

## <a name="step-4-creating-the-paging-interface"></a>Krok 4: vytvoření rozhraní stránkování

Existuje řada různých rozhraní stránkování, která lze implementovat. Ovládací prvky GridView, DetailsView a FormView poskytují čtyři různá rozhraní pro výběr mezi:

- **Dále můžou předchozí** uživatelé přesunout jednu stránku současně na další nebo předchozí.
- **Další, předchozí, první, poslední,** kromě tlačítek Další a předchozí, toto rozhraní zahrnuje první a poslední tlačítko pro přechod na velmi první nebo velmi poslední stránku.
- **Číselný** seznam čísel stránek ve stránkovacím rozhraní, které uživateli umožňuje rychle přejít na konkrétní stránku.
- **Číselná, první, poslední,** kromě čísel číselných stránek obsahuje tlačítka pro přechod na velmi první nebo velmi poslední stránku.

Pro prvky DataList a Repeater zodpovídáme za rozhodování o stránkování rozhraní a jeho implementaci. To zahrnuje vytvoření potřebných webových ovládacích prvků na stránce a zobrazení požadované stránky při kliknutí na tlačítko rozhraní stránkování. Kromě toho může být potřeba zakázat některé ovládací prvky rozhraní stránkování. Například při zobrazení první stránky dat pomocí následujícího, předchozího, prvního rozhraní bude zakázáno první i předchozí tlačítko.

Pro tento kurz použijte k použití následujícího, předchozího, prvního, posledního rozhraní. Přidejte na stránku čtyři webové ovládací prvky tlačítka a nastavte jejich `ID` s na `FirstPage`, `PrevPage`, `NextPage`a `LastPage`. Nastavte vlastnosti `Text` na nejdříve &lt;&lt; první, &lt; předchozí, další &gt;a poslední &gt;&gt;.

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample4.aspx)]

Dále vytvořte obslužnou rutinu události `Click` pro každé z těchto tlačítek. Za chvíli přidáme kód potřebný k zobrazení požadované stránky.

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>Pamatuje si celkový počet záznamů, které se Stránkují.

Bez ohledu na zvolené rozhraní stránkování musíme vypočítat a zapamatovat si celkový počet záznamů, které jsou stránkou. Celkový počet řádků (ve spojení s velikostí stránky) určuje, kolik z celkových stránek dat je zpracováváno stránkou, což určuje, které ovládací prvky rozhraní pro stránkování jsou přidány nebo jsou povoleny. V dalším, předchozím, prvním, posledním rozhraní, které sestavíme, se počet stránek používá dvěma způsoby:

- Chcete-li zjistit, zda se zobrazuje poslední stránka, v takovém případě je tlačítko Další a poslední vypnuté.
- Pokud uživatel klikne na poslední tlačítko, potřebujeme ho zawhisky na poslední stránku, jejíž index je menší než počet stránek.

Počet stránek se počítá jako strop celkového počtu řádků dělený velikostí stránky. Pokud například máme stránkování přes 79 záznamů se čtyřmi záznamy na stránku, bude počet stránek 20 (horní mez 79/4). Pokud používáme rozhraní číselného stránkování, tyto informace informují o tom, kolik tlačítek číselné stránky se má zobrazit. Pokud má naše rozhraní stránkování další nebo poslední tlačítka, počet stránek se používá k určení, kdy se má zakázat tlačítko Další nebo poslední.

Pokud stránkovací rozhraní obsahuje tlačítko poslední, je nezbytné, aby celkový počet záznamů, které jsou na straně sebe, byly předávány napříč zpětnými odesláními, aby při kliknutí na poslední tlačítko bylo možné určit poslední index stránky. Pokud to chcete usnadnit, vytvořte vlastnost `TotalRowCount` ve třídě ASP.NET stránky s kódem na pozadí, která ukládá jeho hodnotu do stavu zobrazení:

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

Kromě `TotalRowCount`můžete vytvořit vlastnosti na úrovni stránky jen pro čtení a získat tak snadný přístup k indexu stránky, velikosti stránky a počtu stránek:

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample6.cs)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>Určení celkového počtu záznamů, které se Stránkují

Objekt `PagedDataSource` vrácený z metody ObjectDataSource `Select()` v rámci něj obsahuje *všechny* záznamy produktů, a to i v případě, že je v prvku DataList zobrazena pouze jeho podmnožina. Vlastnost `PagedDataSource` s [`Count`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx) vrací pouze počet položek, které budou zobrazeny v prvku DataList; [vlastnost`DataSourceCount`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx) vrátí celkový počet položek v rámci `PagedDataSource`. Proto je potřeba přiřadit vlastnost ASP.NET Page s `TotalRowCount` hodnotu vlastnosti `DataSourceCount` `PagedDataSource` s.

K tomu je potřeba vytvořit obslužnou rutinu události pro `Selected` události ObjectDataSource s. V `Selected` obslužná rutina události máme přístup k návratové hodnotě metody ObjectDataSource s `Select()` v tomto případě `PagedDataSource`.

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

## <a name="displaying-the-requested-page-of-data"></a>Zobrazení požadované stránky dat

Když uživatel klikne na jedno z tlačítek ve stránkovacím rozhraní, musíme zobrazit požadovanou stránku dat. Vzhledem k tomu, že parametry stránkování jsou zadány pomocí řetězce dotazu QueryString, aby se zobrazila požadovaná stránka dat `Response.Redirect(url)`, aby prohlížeč uživatelů znovu požadoval stránku `Paging.aspx` s příslušnými parametry stránkování. Pokud například chcete zobrazit druhou stránku dat, přesměrujte uživatele na `Paging.aspx?pageIndex=1`.

Chcete-li to usnadnit, vytvořte `RedirectUser(sendUserToPageIndex)` metodu, která přesměruje uživatele na `Paging.aspx?pageIndex=sendUserToPageIndex`. Pak zavolejte tuto metodu ze čtyř tlačítek `Click` obslužných rutin událostí. V obslužné rutině události `FirstPage` `Click` zavolejte `RedirectUser(0)`, aby se odesílaly na první stránku; v obslužné rutině události `Click` `PrevPage` použijte `PageIndex - 1` jako index stránky; a tak dále.

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample8.cs)]

S kompletními obslužnými rutinami události `Click` se záznamy DataList s dají stránkovat kliknutím na tlačítka. Vyzkoušejte si to prosím chvilku!

## <a name="disabling-paging-interface-controls"></a>Zakázání ovládacích prvků rozhraní stránkování

V současné době jsou všechna čtyři tlačítka povolena bez ohledu na zobrazovanou stránku. Chceme však zakázat první a předchozí tlačítka při zobrazení první stránky dat a tlačítka Další a poslední při zobrazení poslední stránky. Objekt `PagedDataSource` vrácený metodou ObjectDataSource `Select()` obsahuje vlastnosti [`IsFirstPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx) a [`IsLastPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx) , které můžeme prostudovat, abyste zjistili, zda zobrazujeme první nebo poslední stránku dat.

Do obslužné rutiny události `Selected` ObjectDataSource s přidejte následující:

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

V takovém případě budou při prohlížení první stránky vypnutá tlačítka první a předchozí, zatímco tlačítko Další a poslední bude při zobrazení poslední stránky zakázané.

Přizpůsobte rozhraní stránkování tím, že Informujte uživatele o tom, jakou stránku nyní právě prohlížíte, a kolik jich má celkový počet stránek. Přidejte ovládací prvek web popisku na stránku a nastavte jeho vlastnost `ID` na hodnotu `CurrentPageNumber`. Nastavte jeho vlastnost `Text` v obslužné rutině ovládacího prvku ObjectDataSource s, tak, aby obsahovalo aktuální prohlíženou stránku (`PageIndex + 1`) a celkový počet stránek (`PageCount`).

[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample10.cs)]

Obrázek 10 ukazuje `Paging.aspx` při prvním navštívení. Vzhledem k tomu, že je dotaz QueryString prázdný, zobrazí se ve výchozím nastavení DataList prvních čtyř produktů; tlačítka první a předchozí jsou zakázaná. Kliknutím na další zobrazíte další čtyři záznamy (viz obrázek 11); tlačítka první a předchozí jsou nyní povolena.

[![zobrazení první stránky dat](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image22.png)

**Obrázek 10**: zobrazí se první stránka dat ([kliknutím zobrazíte obrázek v plné velikosti).](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)

[![se zobrazí druhá stránka dat](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)

**Obrázek 11**: zobrazí se druhá stránka dat ([kliknutím zobrazíte obrázek v plné velikosti).](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)

> [!NOTE]
> Stránkovací rozhraní lze dále rozšířit tím, že uživateli umožníte určit, kolik stránek se má zobrazit na stránce. Můžete například přidat DropDownList možnosti pro výpis velikosti stránky, jako je 5, 10, 25, 50 a vše. Po výběru velikosti stránky musí být uživatel přesměrován zpět na `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`. Odejdu z tohoto vylepšení jako cvičení pro čtenáře.

## <a name="using-custom-paging"></a>Použití vlastního stránkování

Stránky DataList prostřednictvím svých dat s využitím neefektivních výchozích technik stránkování. Když je stránkování po dostatečně velkých objemech dat, je nezbytné, aby se použilo vlastní stránkování. I když se podrobnosti implementace mírně liší, koncepce za implementací vlastního stránkování v prvku DataList jsou stejné jako výchozí stránkování. Pomocí vlastního stránkování použijte metodu `ProductBLL` třídy s `GetProductsPaged` (místo `GetProductsAsPagedDataSource`). Jak je popsáno v kurzu [efektivní stránkování prostřednictvím velkých objemů dat](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) , `GetProductsPaged` musí být předán index počátečního řádku a maximální počet řádků, které se mají vrátit. Tyto parametry lze uchovávat pomocí řetězce dotazu, stejně jako `pageIndex` a parametry `pageSize` používané ve výchozím stránkování.

Vzhledem k tomu, že neexistují `PagedDataSource` s vlastním stránkováním, je potřeba použít alternativní techniky k určení celkového počtu záznamů, které jsou stránkovaná, a to, jestli se má znovu zobrazit první nebo poslední stránka dat. Metoda `TotalNumberOfProducts()` ve třídě `ProductsBLL` vrátí celkový počet produktů, které jsou stránkou. Chcete-li zjistit, zda je zobrazena první stránka dat, Projděte si index počátečního řádku, pokud je nula, a pak se zobrazí první stránka. Poslední stránka je zobrazena, pokud je index počátečního řádku plus maximální počet vrácených řádků větší nebo roven celkovému počtu záznamů, které jsou stránkou.

V dalším kurzu budeme prozkoumat implementaci vlastního stránkování podrobněji.

## <a name="summary"></a>Souhrn

I když prvek DataList ani Repeater nenabízí podporu stránkování, která se nachází v ovládacích prvcích GridView, DetailsView a FormView, může být tato funkce přičtena s minimálním úsilím. Nejjednodušší způsob, jak implementovat výchozí stránkování, je zabalit celou sadu produktů v rámci `PagedDataSource` a potom navazovat `PagedDataSource` na DataList nebo Repeater. V tomto kurzu jsme přidali metodu `GetProductsAsPagedDataSource` do `ProductsBLL` třídy, která vrátí `PagedDataSource`. Třída `ProductsBLL` již obsahuje metody potřebné pro vlastní stránkování `GetProductsPaged` a `TotalNumberOfProducts`.

Při načítání přesné sady záznamů, které se mají zobrazit pro vlastní stránkování nebo pro všechny záznamy v `PagedDataSource` pro výchozí stránkování, je také potřeba ručně přidat rozhraní stránkování. Pro tento kurz jsme vytvořili další, předchozí, první a poslední rozhraní se čtyřmi webovými ovládacími prvky tlačítka. Také ovládací prvek popisek zobrazující číslo aktuální stránky a celkový počet stránek byl přidán.

V dalším kurzu uvidíte, jak přidat podporu řazení do prvku DataList a Repeater. Také se dozvíte, jak vytvořit prvek DataList, který může být stránkovaný i seřazený (s příklady pomocí výchozího a vlastního stránkování).

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Liz Shulok, Ken Pespisa a Bernadette Leigh. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](sorting-data-in-a-datalist-or-repeater-control-cs.md)
