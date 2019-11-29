---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
title: Dotazování na data pomocí ovládacího prvku SqlDataSource (VB) | Microsoft Docs
author: rick-anderson
description: V předchozích kurzech jsme použili ovládací prvek ObjectDataSource k úplnému oddělení prezentační vrstvy z vrstvy přístupu k datům. Začíná na tomto tutor...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: b12f752d-3502-40a4-b695-fc7b7d08cfd3
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 199ddb46e877c3a0937672d33241a240660684da
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606066"
---
# <a name="querying-data-with-the-sqldatasource-control-vb"></a>Dotazování na data ovládacím prvkem SqlDataSource(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_VB.exe) nebo [Stáhnout PDF](querying-data-with-the-sqldatasource-control-vb/_static/datatutorial47vb1.pdf)

> V předchozích kurzech jsme použili ovládací prvek ObjectDataSource k úplnému oddělení prezentační vrstvy z vrstvy přístupu k datům. Od tohoto kurzu se dozvíte, jak lze ovládací prvek SqlDataSource použít pro jednoduché aplikace, které nevyžadují takovou striktní oddělení prezentace a přístup k datům.

## <a name="introduction"></a>Úvod

Všechny kurzy, které jsme doposud prozkoumali, používaly vrstvenou architekturu skládající se z prezentační, obchodní logiky a vrstev přístupu k datům. Vrstva přístupu k datům (DAL) byla vytvořena v prvním kurzu ([Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-vb.md)) a vrstvy obchodní logiky v druhé ([Vytvoření vrstvy obchodní logiky](../introduction/creating-a-business-logic-layer-vb.md)). Počínaje kurzem [zobrazení dat s](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) popisem ObjectDataSource jsme viděli, jak používat ASP.NET 2,0 s novým ovládacím prvkem ObjectDataSource pro deklarativní rozhraní s architekturou z prezentační vrstvy.

I když všechny kurzy, které doposud používaly architekturu pro práci s daty, také umožňují přístup k datům databáze, jejich vkládání, aktualizace a odstraňování dat přímo ze stránky ASP.NET a jejich obejití. Tím umístíte konkrétní databázové dotazy a obchodní logiku přímo do webové stránky. Pro dostatečně velké nebo složité aplikace, navrhování, implementaci a používání vrstvených architektur je v případě úspěchu, aktualizace a udržovatelnosti aplikace velmi důležité. Vývoj robustní architektury však může být zbytečný při vytváření více než jedna z nich, jednorázových aplikací.

ASP.NET 2,0 poskytuje pět vestavěných ovládacích prvků zdroje dat [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)a [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx). Třída SqlDataSource se dá použít pro přístup k datům a jejich úpravu přímo z relační databáze, včetně Microsoft SQL Server, Microsoft Access, Oracle, MySQL a dalších. V tomto kurzu a dalších třech prozkoumáme, jak pracovat s ovládacím prvkem SqlDataSource, prozkoumat způsob dotazování a filtrování dat databáze a jak používat SqlDataSource k vkládání, aktualizaci a odstraňování dat.

![ASP.NET 2,0 zahrnuje pět vestavěných ovládacích prvků zdroje dat.](querying-data-with-the-sqldatasource-control-vb/_static/image1.gif)

**Obrázek 1**: ASP.NET 2,0 zahrnuje pět vestavěných ovládacích prvků zdroje dat.

## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>Porovnání prvku ObjectDataSource a SqlDataSource

Koncepční ovládací prvky ObjectDataSource i SqlDataSource jsou jednoduše proxy na data. Jak je popsáno v kurzu [zobrazení dat s](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) využitím prvku ObjectDataSource, prvek ObjectDataSource obsahuje vlastnosti, které určují typ objektu, který poskytuje data a metody k vyvolání pro výběr, vložení, aktualizaci a odstranění dat z podkladového typu objektu. Po nakonfigurování vlastností ObjectDataSource s lze ovládací prvek data web, jako je například GridView, DetailsView nebo DataList, svázat s ovládacím prvkem, pomocí `Select()`ObjectDataSource s, `Insert()`, `Delete()`a `Update()` metody pro interakci s podkladovou architekturou.

Třída SqlDataSource poskytuje stejné funkce, ale funguje na relační databázi, nikoli v knihovně objektů. Ve třídě SqlDataSource je nutné zadat připojovací řetězec databáze a ad-hoc dotazy SQL nebo uložené procedury, které mají být provedeny pro vložení, aktualizaci, odstranění a načtení dat. Metody `Select()`SqlDataSource, `Insert()`, `Update()`a `Delete()`, se při vyvolání připojí k zadané databázi a vydávají odpovídající dotaz SQL. Jak znázorňuje následující obrázek, tyto metody grunt práci s připojením k databázi, vydávají dotaz a vracejí výsledky.

![Třída SqlDataSource slouží jako proxy k databázi.](querying-data-with-the-sqldatasource-control-vb/_static/image2.gif)

**Obrázek 2**: třída SqlDataSource slouží jako proxy databáze.

> [!NOTE]
> V tomto kurzu se zaměříme na načítání dat z databáze. V kurzu [vložení, aktualizace a odstranění dat pomocí ovládacího prvku SqlDataSource](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md) uvidíte, jak nakonfigurovat SqlDataSource pro podporu vložení, aktualizace a odstranění.

## <a name="the-sqldatasource-and-accessdatasource-controls"></a>Ovládací prvky SqlDataSource a AccessDataSource

Kromě ovládacího prvku SqlDataSource ASP.NET 2,0 také obsahuje ovládací prvek AccessDataSource. Tyto dva různé ovládací prvky zavedou mnoho vývojářů, kteří jsou noví v ASP.NET 2,0, což má za následek, že ovládací prvek AccessDataSource je navržený tak, aby fungoval výhradně s přístupem k aplikaci Microsoft Access s ovládacím prvkem SqlDataSource Microsoft SQL Server navrženým I když je prvek AccessDataSource navržený tak, aby fungoval konkrétně s přístupem k aplikaci Microsoft Access, ovládací prvek SqlDataSource *funguje s relační databází, ke které* lze přistupovat prostřednictvím rozhraní .NET. To zahrnuje všechna úložiště dat kompatibilní s OleDb nebo rozhraním ODBC, jako jsou Microsoft SQL Server, Microsoft Access, Oracle, Informix, MySQL a PostgreSQL, a to i mezi mnoha ostatními.

Jediným rozdílem mezi ovládacími prvky AccessDataSource a SqlDataSource je způsob, jakým jsou zadány informace o připojení databáze. Ovládací prvek AccessDataSource potřebuje pouze cestu k souboru databáze aplikace Access. Třída SqlDataSource na druhé straně vyžaduje úplný připojovací řetězec.

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>Krok 1: vytvoření webových stránek SqlDataSource

Předtím, než začneme zkoumat, jak pracovat přímo s daty databáze pomocí ovládacího prvku SqlDataSource, si nejdřív chvíli počkejte, než vytvoříte stránky ASP.NET v našem projektu webu, který budeme potřebovat pro tento kurz a další tři. Začněte přidáním nové složky s názvem `SqlDataSource`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`

![Přidání stránek ASP.NET pro kurzy týkající se SqlDataSource](querying-data-with-the-sqldatasource-control-vb/_static/image3.gif)

**Obrázek 3**: přidání stránek ASP.NET pro kurzy týkající se SqlDataSource

Podobně jako v ostatních složkách `Default.aspx` ve složce `SqlDataSource` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](querying-data-with-the-sqldatasource-control-vb/_static/image5.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image4.gif)

**Obrázek 4**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](querying-data-with-the-sqldatasource-control-vb/_static/image6.gif))

Nakonec tyto čtyři stránky přidejte jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značku po přidání vlastních tlačítek do prvku DataList a Repeater `<siteMapNode>`:

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample1.sql)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro kurzy pro úpravy, vkládání a odstraňování.

![Mapa webu teď obsahuje položky pro kurzy SqlDataSource](querying-data-with-the-sqldatasource-control-vb/_static/image7.gif)

**Obrázek 5**: Mapa webu teď obsahuje položky pro kurzy SqlDataSource.

## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>Krok 2: Přidání a konfigurace ovládacího prvku SqlDataSource

Začněte tím, že otevřete stránku `Querying.aspx` ve složce `SqlDataSource` a přepnete na zobrazení Návrh. Přetáhněte ovládací prvek SqlDataSource ze sady nástrojů do návrháře a nastavte jeho `ID` na `ProductsDataSource`. Stejně jako v prvku ObjectDataSource, třída SqlDataSource nevytvoří žádný Vykreslený výstup, a proto se zobrazí jako šedé pole na návrhové ploše. Chcete-li konfigurovat SqlDataSource, klikněte na odkaz konfigurace zdroje dat z inteligentní značky SqlDataSource s.

![Klikněte na odkaz konfigurace zdroje dat z inteligentní značky SqlDataSource s.](querying-data-with-the-sqldatasource-control-vb/_static/image8.gif)

**Obrázek 6**: klikněte na odkaz konfigurace zdroje dat ze inteligentní značky SqlDataSource s.

Tím se zobrazí průvodce pro ovládací prvek SqlDataSource s konfigurací zdroje dat. I když se postup Průvodce s liší od ovládacího prvku ObjectDataSource s, je konečný cíl stejný, aby poskytoval podrobné informace o tom, jak načíst, vkládat, aktualizovat a odstraňovat data prostřednictvím zdroje dat. Pro SqlDataSource to zahrnuje určení podkladové databáze, která se má použít, a poskytnutí příkazů SQL ad hoc nebo uložených procedur.

První krok průvodce vás vyzve k zadání databáze. Rozevírací seznam obsahuje tyto databáze nacházející se ve složce Web Application `App_Data` a ty, které byly přidány do uzlu datová připojení v Průzkumník serveru. Vzhledem k tomu, že jsme už přidali připojovací řetězec pro databázi `NORTHWIND.MDF` do složky `App_Data` do našeho souboru projektu s `Web.config`, rozevírací seznam obsahuje odkaz na tento připojovací řetězec `NORTHWINDConnectionString`. V rozevíracím seznamu vyberte tuto položku a klikněte na další.

![Z rozevíracího seznamu vyberte NORTHWINDConnectionString.](querying-data-with-the-sqldatasource-control-vb/_static/image9.gif)

**Obrázek 7**: volba `NORTHWINDConnectionString` v rozevíracím seznamu

Po výběru databáze Průvodce požádá, aby dotaz vrátil data. Můžeme buď zadat sloupce tabulky nebo zobrazení, které se mají vrátit, nebo můžete zadat vlastní příkaz SQL nebo zadat uloženou proceduru. Mezi touto volbou můžete přepínat pomocí příkazu zadat vlastní příkaz SQL nebo uloženou proceduru a určit sloupce z tabulky nebo přepínačů zobrazení.

> [!NOTE]
> V tomto prvním příkladu použijte možnost zadat sloupce z tabulky nebo zobrazení. Později v tomto kurzu se vrátíme k Průvodci a prozkoumejte možnost zadat vlastní příkaz SQL nebo uloženou proceduru.

Na obrázku 8 se zobrazí obrazovka konfigurovat příkaz pro výběr, pokud je vybrán přepínač zadat sloupce z tabulky nebo zobrazení. Rozevírací seznam obsahuje sadu tabulek a zobrazení v databázi Northwind s vybranými sloupci tabulky nebo zobrazení v následujícím seznamu zaškrtávacích políček. V tomto příkladu můžete pomocí tabulky `Products` vracet sloupce `ProductID`, `ProductName`a `UnitPrice`. Jak ukazuje obrázek 8, po provedení těchto výběrů zobrazí průvodce Výsledný příkaz SQL `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`.

![Vrátit data z tabulky Products](querying-data-with-the-sqldatasource-control-vb/_static/image10.gif)

**Obrázek 8**: návratová Data z `Products` tabulky

Jakmile nakonfigurujete Průvodce tak, aby vracel sloupce `ProductID`, `ProductName`a `UnitPrice` z tabulky `Products`, klikněte na tlačítko Další. Tato poslední obrazovka nabízí příležitost k prohlédnutí výsledků dotazu nakonfigurovaného z předchozího kroku. Kliknutí na tlačítko Test Query spustí nakonfigurovaný příkaz `SELECT` a zobrazí výsledky v mřížce.

![Kliknutím na tlačítko Test dotazu si můžete prohlédnout svůj dotaz SELECT.](querying-data-with-the-sqldatasource-control-vb/_static/image11.gif)

**Obrázek 9**: kliknutím na tlačítko Test dotazu si můžete prohlédnout `SELECT` dotaz

Průvodce dokončíte kliknutím na tlačítko Dokončit.

Podobně jako v prvku ObjectDataSource, průvodce setřídě SqlDataSource pouze přiřazuje hodnoty vlastnostím ovládacího prvku, konkrétně [`ConnectionString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx) a [`SelectCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx) vlastností. Po dokončení průvodce by deklarativní označení ovládacího prvku SqlDataSource mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample2.aspx)]

Vlastnost `ConnectionString` poskytuje informace o tom, jak se připojit k databázi. Této vlastnosti může být přiřazena úplná, pevně zakódovaná hodnota připojovacího řetězce nebo může ukazovat na připojovací řetězec v `Web.config`. Chcete-li odkazovat na hodnotu připojovacího řetězce v souboru Web. config, použijte syntaxi `<%$ expressionPrefix:expressionValue %>`. *ExpressionPrefix* je obvykle connectionStrings a *expressionValue* je název řetězce připojení v [části`<connectionStrings>`](https://msdn.microsoft.com/library/bf7sd233.aspx)`Web.config`. Syntaxe se však dá použít k odkazování `<appSettings>` prvků nebo obsahu ze souborů prostředků. Další informace o této syntaxi najdete v tématu [Přehled výrazů ASP.NET](https://msdn.microsoft.com/library/d5bd1tad.aspx) .

Vlastnost `SelectCommand` Určuje příkaz SQL ad hoc nebo uloženou proceduru, která má být provedena pro vrácení dat.

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>Krok 3: Přidání webového ovládacího prvku data a jeho svázání na třídě SqlDataSource

Jakmile je třída SqlDataSource nakonfigurována, může být svázána s datovým ovládacím prvkem webového ovládacího prvku, jako je například GridView nebo DetailsView. Pro tento kurz se zobrazí data v prvku GridView. Z panelu nástrojů přetáhněte prvek GridView na stránku a navažte jej na `ProductsDataSource` SqlDataSource tím, že v rozevíracím seznamu v inteligentní značce GridView. vyberete zdroj dat.

[![přidání prvku GridView a jeho svázání s ovládacím prvkem SqlDataSource](querying-data-with-the-sqldatasource-control-vb/_static/image13.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image12.gif)

**Obrázek 10**: Přidání prvku GridView a jeho svázání s ovládacím prvkem SqlDataSource ([kliknutím zobrazíte obrázek v plné velikosti](querying-data-with-the-sqldatasource-control-vb/_static/image14.gif))

Jakmile vyberete ovládací prvek SqlDataSource z rozevíracího seznamu v inteligentní značce GridView s, Visual Studio automaticky přidá vlastnost BoundField nebo třídě CheckBoxField podporována do prvku GridView pro každý sloupec vrácený ovládacím prvkem zdroje dat. Vzhledem k tomu, že třída SqlDataSource vrátí tři databázové sloupce `ProductID`, `ProductName`a `UnitPrice` existují tři pole v prvku GridView.

Chvíli počkejte, než se nakonfiguruje ovládací prvek GridView s třemi BoundFieldsy. Změňte vlastnost `ProductName` pole s `HeaderText` na název produktu a `UnitPrice` pole s na Price. Naformátujte také pole `UnitPrice` jako měnu. Po provedení těchto úprav by deklarativní značky GridViewu měly vypadat podobně jako následující:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample3.aspx)]

Navštivte tuto stránku v prohlížeči. Jak ukazuje obrázek 11, GridView zobrazí seznam jednotlivých produktů `ProductID`, `ProductName`a `UnitPrice`.

[![prvek GridView zobrazuje jednotlivé hodnoty produktů ProductID, NázevVýrobku a UnitPrice.](querying-data-with-the-sqldatasource-control-vb/_static/image16.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image15.gif)

**Obrázek 11**: prvek GridView zobrazuje jednotlivé produkty `ProductID`, `ProductName`a `UnitPrice` hodnoty ([kliknutím zobrazíte obrázek v plné velikosti).](querying-data-with-the-sqldatasource-control-vb/_static/image17.gif)

Když je stránka navštívena, prvek GridView Vyvolá svou metodu správy zdrojů dat s `Select()`. Když jsme používali ovládací prvek ObjectDataSource, tato metoda se nazývá `ProductsBLL` třídy s `GetProducts()`. Ve třídě SqlDataSource však metoda `Select()` naváže připojení k zadané databázi a vydá `SelectCommand` (`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`, v tomto příkladu). Třída SqlDataSource vrátí svůj výsledek, který prvek GridView vytvoří, a vytvoří řádek v prvku GridView pro každý vrácený záznam databáze.

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>Vestavěné funkce webového ovládacího prvku a ovládací prvek SqlDataSource

Obecně platí, že funkce, které jsou součástí ovládacího prvku data web Controls stránkování, řazení, úpravy, odstranění, vložení a tak dále, jsou specifické pro webový ovládací prvek dat a nejsou závislé na použitém ovládacím prvku zdroje dat. To znamená, že GridView může využít integrované stránkování, řazení, úpravy a odstranění, zda je svázána s prvkem ObjectDataSource nebo SqlDataSource. Některé funkce webového ovládacího prvku jsou však citlivé na používané ovládací prvky zdroje dat nebo na konfiguraci správy zdrojů dat.

Například v kurzu [efektivního stránkování po velkých objemech dat](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) jsme probrali, jak ve výchozím nastavení logika stránkování pro datové ovládací prvky data naively vrátí *všechny* záznamy z podkladového zdroje dat a potom zobrazí jenom příslušnou podmnožinu záznamů, která má daný index stránky, a počet záznamů, které se mají zobrazit na stránce. Tento model je vysoce neefektivní při stránkování prostřednictvím dostatečně velkých sad výsledků. Prvek ObjectDataSource je možné nakonfigurovat tak, aby podporoval vlastní stránkování, které vrací pouze přesné podmnožiny záznamů, které se mají zobrazit. Ovládací prvek SqlDataSource ale nemá vlastnosti pro implementaci vlastního stránkování.

Další Subtlety se stránkováním a řazením se projeví na třídě SqlDataSource. Ve výchozím nastavení mohou být data vrácená ze sady SqlDataSource stránkovaná nebo seřazena prostřednictvím prvku GridView. To provedete tak, že zaškrtnete možnosti Povolit stránkování a Povolit řazení v inteligentní značce GridView s v `Querying.aspx` a ověříte, že funguje podle očekávání.

Řazení a stránkování funguje, protože třída SqlDataSource načítá databázová data do volně typované datové sady. Celkový počet záznamů vrácených dotazem: základní aspekt implementace stránkování lze zjistit z datové sady. Kromě toho je možné výsledky datové sady seřadit pomocí objektu DataView. Tyto možnosti jsou automaticky používány třídou SqlDataSource při žádosti GridView na stránkovaná nebo seřazená data.

Třída SqlDataSource může být nakonfigurována tak, aby vracela objekt DataReader, a ne datovou sadu změnou jeho [`DataSourceMode` vlastností](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx) z `DataSet` (výchozí) na `DataReader`. Použití objektu DataReader může být upřednostňováno v situacích při předávání výsledků z objektu SqlDataSource s existujícímu kódu, který očekává objekt DataReader. Vzhledem k tomu, že datačtecí objekty výrazně zjednodušují objekty než datové sady, nabízejí lepší výkon. Pokud tuto změnu provedete, webové ovládací prvky dat ale nemusí ani seřadit ani stránku, protože třída SqlDataSource nemůže zjistit, kolik záznamů je vráceno dotazem, ani DataReader nenabízí žádné techniky pro řazení vrácených dat.

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>Krok 4: použití vlastního příkazu SQL nebo uložené procedury

Při konfiguraci ovládacího prvku SqlDataSource lze dotaz, který se použije k vrácení dat, zadat v jednom ze dvou přístupů jako na vlastní příkaz SQL nebo uloženou proceduru nebo jako sloupce z existující tabulky nebo zobrazení. V kroku 2 jsme prozkoumali výběr sloupců z `Products` tabulky. Pojďme se podívat na použití vlastního příkazu SQL.

Přidejte další ovládací prvek GridView na stránku `Querying.aspx` a vyberte možnost vytvořit nový zdroj dat z rozevíracího seznamu v inteligentní značce. Dále určete, že data budou načítána z databáze. tím se vytvoří nový ovládací prvek SqlDataSource. Pojmenujte `ProductsWithCategoryInfoDataSource`ovládacího prvku.

![Vytvořit nový ovládací prvek SqlDataSource s názvem ProductsWithCategoryInfoDataSource](querying-data-with-the-sqldatasource-control-vb/_static/image18.gif)

**Obrázek 12**: vytvoření nového ovládacího prvku SqlDataSource s názvem `ProductsWithCategoryInfoDataSource`

Na další obrazovce se zobrazí výzva k zadání databáze. Stejně jako na obrázku 7 jsme v rozevíracím seznamu vybrali `NORTHWINDConnectionString` a kliknete na další. Na obrazovce konfigurace příkazu SELECT zvolte přepínač zadat vlastní příkaz SQL nebo uložený postup a klikněte na tlačítko Další. Tím se zobrazí obrazovka definovat vlastní příkazy nebo uložené procedury, která nabízí karty označené jako SELECT, UPDATE, INSERT a DELETE. Na každé kartě můžete zadat vlastní příkaz SQL do textového pole nebo zvolit uloženou proceduru z rozevíracího seznamu. V tomto kurzu se podíváme na zadání vlastního příkazu SQL. Další kurz obsahuje příklad, který používá uloženou proceduru.

![Zadejte vlastní příkaz SQL nebo vyberte uloženou proceduru.](querying-data-with-the-sqldatasource-control-vb/_static/image19.gif)

**Obrázek 13**: zadejte vlastní příkaz SQL nebo vyberte uloženou proceduru.

Vlastní příkaz SQL lze zadat ručně do textového pole nebo lze vytvořit graficky kliknutím na tlačítko Tvůrce dotazů. Z Tvůrce dotazů nebo textového pole použijte následující dotaz k vrácení polí `ProductID` a `ProductName` z tabulky `Products` pomocí `JOIN` k načtení `CategoryName` produktů z `Categories` tabulky:

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample4.sql)]

![Dotaz můžete graficky sestavit pomocí Tvůrce dotazů](querying-data-with-the-sqldatasource-control-vb/_static/image20.gif)

**Obrázek 14**: dotaz můžete graficky sestavit pomocí Tvůrce dotazů

Po zadání dotazu klikněte na tlačítko Další a pokračujte na obrazovku test Query. Kliknutím na Dokončit dokončete Průvodce SqlDataSource.

Po dokončení průvodce bude do prvku GridView přidána tři BoundFieldsy, které zobrazují sloupce `ProductID`, `ProductName`a `CategoryName`, které byly vráceny z dotazu a výsledkem je následující deklarativní označení:

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample5.aspx)]

[![se v prvku GridView zobrazuje každé ID produktu, název a přiřazená kategorie s názvem.](querying-data-with-the-sqldatasource-control-vb/_static/image22.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image21.gif)

**Obrázek 15**: prvek GridView zobrazuje každé ID produktu, název a přiřazený název kategorie ([kliknutím zobrazíte obrázek v plné velikosti).](querying-data-with-the-sqldatasource-control-vb/_static/image23.gif)

## <a name="summary"></a>Přehled

V tomto kurzu jsme viděli, jak zadávat dotazy a zobrazovat data pomocí ovládacího prvku SqlDataSource. Podobně jako prvek ObjectDataSource, třída SqlDataSource slouží jako proxy a poskytuje deklarativní přístup pro přístup k datům. Jeho vlastnosti určují databázi, ke které se má připojit, a dotaz SQL `SELECT`, který se má provést. dá se zadat pomocí okno Vlastnosti nebo pomocí Průvodce konfigurací zdroje dat.

Příklady dotazů `SELECT`, které jsme prozkoumali v tomto kurzu, vrátily všechny záznamy ze zadaného dotazu. Ovládací prvek SqlDataSource však může obsahovat klauzuli `WHERE` s parametry, jejichž hodnoty jsou přiřazeny programově nebo automaticky načteny ze zadaného zdroje. Podíváme se, jak vytvořit a používat parametrizované dotazy v dalším kurzu.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přístup k datům relační databáze](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource – Přehled ovládacího prvku](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [Kurzy rychlý Start ASP.NET: ovládací prvek SqlDataSource](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [`<connectionStrings>` element Web. config](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [Odkaz na připojovací řetězec databáze](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Zuzana Connery, Bernadette Leigh a David Suru. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)
> [Další](using-parameterized-queries-with-the-sqldatasource-vb.md)
