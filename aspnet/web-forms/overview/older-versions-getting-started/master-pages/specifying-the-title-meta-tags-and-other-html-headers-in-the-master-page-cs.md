---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
title: Zadání názvu, meta značek a dalších záhlaví HTML na stránce předlohy (C#) | Microsoft Docs
author: rick-anderson
description: Vyhledává různé techniky pro definování různých prvků &lt;hlavní&gt; na stránce předlohy ze stránky obsahu.
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 0aa1c84f-c9e2-4699-b009-0e28643ecbc6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: a4ec96a5b90f664655d554c064f9d50e76ad2d58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587106"
---
# <a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-c"></a>Zadání názvu, metaznaček a dalších hlaviček HTML na stránce předlohy (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_CS.pdf)

> Vyhledává různé techniky pro definování různých prvků &lt;hlavní&gt; na stránce předlohy ze stránky obsahu.

## <a name="introduction"></a>Úvod

Nové stránky předlohy vytvořené v aplikaci Visual Studio 2008 mají ve výchozím nastavení dva ovládací prvky ContentPlaceHolder: jednu s názvem Head a umístěnou v prvku `<head>`; a jeden s názvem `ContentPlaceHolder1`umístěný v rámci webového formuláře. Účelem `ContentPlaceHolder1` je definovat oblast ve webovém formuláři, kterou lze přizpůsobit na základě stránky. `head` ContentPlaceHolder umožňuje stránkám přidat vlastní obsah do části `<head>`. (Tyto dva prvky ContentPlaceHolder lze změnit nebo odebrat a další prvky ContentPlaceHolder mohou být přidány do stránky předlohy. Naše stránka předlohy, `Site.master`, má v současné době čtyři ovládací prvky ContentPlaceHolder.)

Prvek HTML `<head>` slouží jako úložiště pro informace o dokumentu webové stránky, který není součástí samotného dokumentu. To zahrnuje informace, jako je název webové stránky, meta-informace používané vyhledávacími weby nebo interními prohledávacími moduly a odkazy na externí prostředky, jako jsou informační kanály RSS, JavaScript a soubory CSS. Některé z těchto informací můžou být relevantní pro všechny stránky na webu. Například můžete chtít globálně importovat stejná pravidla šablony stylů CSS a soubory JavaScriptu pro každou stránku ASP.NET. Existují však části `<head>` element, které jsou specifické pro stránku. Nadpis stránky je základní příklad.

V tomto kurzu se podíváme na to, jak na stránce předlohy a na svých stránkách obsahu definovat globální značku a `<head>` pro konkrétní stránku.

## <a name="examining-the-master-pagesheadsection"></a>Prozkoumání`<head>`sekce stránky předlohy

Výchozí soubor hlavní stránky vytvořený pomocí sady Visual Studio 2008 obsahuje následující značky v jeho `<head>` části:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample1.aspx)]

Všimněte si, že `<head>` element obsahuje atribut `runat="server"`, který označuje, že se jedná o serverový ovládací prvek (spíše než statické HTML). Všechny stránky ASP.NET jsou odvozeny z [třídy`Page`](https://msdn.microsoft.com/library/system.web.ui.page.aspx), která je umístěna v oboru názvů `System.Web.UI`. Tato třída obsahuje vlastnost `Header`, která poskytuje přístup k oblasti `<head>` stránky. Pomocí [vlastnosti`Header`](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx) můžeme nastavit nadpis stránky pro ASP.NET nebo přidat další značky do vykresleného `<head>` oddílu. Je to možné a pak pro přizpůsobení prvku `<head>` stránky obsahu vytvořením bitu kódu v obslužné rutině události `Page_Load` stránky. Podíváme se, jak programově nastavit nadpis stránky v kroku 1.

Značka zobrazená ve výše uvedeném elementu `<head>` také obsahuje ovládací prvek ContentPlaceHolder s názvem Head. Tento ovládací prvek ContentPlaceHolder není nezbytný, protože stránky obsahu mohou programově přidat vlastní obsah do prvku `<head>`. Je však užitečné v situacích, kdy stránka obsahu vyžaduje přidání statického kódu do prvku `<head>`, protože statické označení lze přidat deklarativně k odpovídajícímu ovládacímu prvku obsahu, nikoli programově.

Kromě prvku `<title>` a elementu Head ContentPlaceHolder by `<head>` element stránky předlohy měl obsahovat všechny značky `<head>`na úrovni, které jsou společné pro všechny stránky. Na našem webu všechny stránky používají pravidla CSS definovaná v souboru `Styles.css`. V důsledku toho jsme aktualizovali `<head>` element v kurzu [*vytváření rozložení v rámci webu pomocí stránek předlohy*](creating-a-site-wide-layout-using-master-pages-cs.md) pro zahrnutí odpovídajícího `<link>` elementu. `Site.master` je uvedeno v aktuálním `<head>` značkách hlavní stránky hlavního serveru.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>Krok 1: nastavení názvu stránky obsahu

Název webové stránky je zadán prostřednictvím elementu `<title>`. Je důležité nastavit název každé stránky na odpovídající hodnotu. Při návštěvě stránky se její název zobrazí v záhlaví prohlížeče. Při vytváření záložek stránky používají prohlížeče jako navrhovaný název záložky název stránky. Mnoho vyhledávačů navíc zobrazuje název stránky při zobrazení výsledků hledání.

> [!NOTE]
> Ve výchozím nastavení sada Visual Studio nastavuje prvek `<title>` na stránce předlohy na "bez názvu stránky". Podobně nové stránky ASP.NET mají svou `<title>` nastavenou na bez názvu stránky. Vzhledem k tomu, že se dá snadno zapomenout nastavit nadpis stránky na odpovídající hodnotu, je na internetu celá řada stránek s názvem "stránka bez názvu". Vyhledávání na webových stránkách Google s tímto názvem vrátí zhruba 2 460 000 výsledků. I společnost Microsoft je náchylná k publikování webových stránek s názvem "stránka bez názvu". V době psaní tohoto textu je hledání Google oznámeno 236 takových webových stránek v doméně Microsoft.com.

ASP.NET stránka může zadat její název jedním z následujících způsobů:

- Vložením hodnoty přímo do prvku `<title>`
- Použití atributu `Title` v direktivě `<%@ Page %>`
- Programově se nastavuje vlastnost `Title` stránky pomocí kódu, jako je `Page.Title="title"` nebo `Page.Header.Title="title"`.

Stránky obsahu nemají element `<title>`, jak je definováno na stránce předlohy. Pokud tedy chcete nastavit název stránky obsahu, můžete buď použít atribut `Title` direktivu `<%@ Page %>`, nebo ho nastavit programově.

### <a name="setting-the-pages-title-declaratively"></a>Deklarativní nastavení názvu stránky

Název stránky obsahu lze deklarativně nastavit pomocí atributu `Title` [direktivy`<%@ Page %>`](https://msdn.microsoft.com/library/ydy4x04a.aspx). Tuto vlastnost lze nastavit přímo úpravou direktivy `<%@ Page %>` nebo prostřednictvím okno Vlastnosti. Pojďme se podívat na oba přístupy.

V zobrazení zdroj vyhledejte direktivu `<%@ Page %>`, která je v horní části deklarativního označení stránky. Direktiva `<%@ Page %>` pro `Default.aspx` následující:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample3.aspx)]

Direktiva `<%@ Page %>` určuje atributy specifické pro stránku používané modulem ASP.NET při analýze a kompilování stránky. To zahrnuje soubor hlavní stránky, umístění jeho souboru kódu a jeho nadpis, mimo jiné informace.

Ve výchozím nastavení se při vytváření nové stránky obsahu v sadě Visual Studio nastaví atribut `Title` na stránku bez názvu. Umožňuje změnit atribut `Default.aspx``Title` ze stránky bez názvu na "kurzy pro hlavní stránku" a pak zobrazit stránku pomocí prohlížeče. Obrázek 1 zobrazuje záhlaví prohlížeče, které odráží nový nadpis stránky.

![Záhlaví prohlížeče teď zobrazuje &quot;výukových programů hlavní stránky&quot; místo &quot;bez názvu stránky&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image1.png)

**Obrázek 01**: v záhlaví prohlížeče se nyní zobrazují "kurzy stránky předlohy" místo "stránka bez názvu".

Název stránky může být také nastaven z okno Vlastnosti. Z okno Vlastnosti v rozevíracím seznamu vyberte dokument, aby se načetly vlastnosti na úrovni stránky, které obsahují vlastnost `Title`. Obrázek 2 ukazuje okno Vlastnosti po `Title` nastavení na "kurzy stránky předlohy".

![Název můžete nakonfigurovat také z okna Vlastnosti.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image2.png)

**Obrázek 02**: název můžete nakonfigurovat také z okna Vlastnosti.

### <a name="setting-the-pages-title-programmatically"></a>Programové nastavení názvu stránky

Kód `<head runat="server">` stránky předlohy je přeložen do instance [`HtmlHead` třídy](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx) , když je stránka vykreslena modulem ASP.NET. Třída `HtmlHead` má [vlastnost`Title`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx) , jejíž hodnota se odrazí v elementu vykresleného `<title>`. Tato vlastnost je přístupná z třídy kódu na pozadí stránky ASP.NET prostřednictvím `Page.Header.Title`; k této vlastnosti lze také přistupovat prostřednictvím `Page.Title`.

Chcete-li nastavit název stránky programově, přejděte na třídu kódu na pozadí `About.aspx` stránky a vytvořte obslužnou rutinu události pro událost `Load` stránky. Dále nastavte nadpis stránky na "kurzy stránky předlohy:: about:: *Date*", kde *Datum* je aktuální datum. Po přidání tohoto kódu by obslužná rutina události `Page_Load` měla vypadat nějak takto:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample4.cs)]

Obrázek 3 ukazuje záhlaví prohlížeče při návštěvě stránky `About.aspx`.

![Název stránky je programově nastavený a obsahuje aktuální datum.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image3.png)

**Obrázek 03**: název stránky je programově nastavený a obsahuje aktuální datum.

## <a name="step-2-automatically-assigning-a-page-title"></a>Krok 2: automatické přiřazení nadpisu stránky

Jak jsme viděli v kroku 1, nadpis stránky se dá nastavit deklarativně nebo programově. Pokud zapomenete explicitně změnit název na něco výstižnější, stránka bude mít výchozí název "bez názvu stránky". V ideálním případě se nadpis stránky nastaví automaticky pro nás v případě, že explicitně neurčíte jeho hodnotu. Například pokud je v modulu runtime nadpis stránky "bez názvu stránky", můžeme chtít, aby se název automaticky aktualizoval tak, aby byl stejný jako název souboru stránky ASP.NET. Dobrá zpráva je, že při práci s trochu dopředu je možné automaticky přiřadit název.

Všechny webové stránky ASP.NET jsou odvozeny z třídy `Page` v oboru názvů `System.Web.UI`. Třída `Page` definuje minimální funkčnost potřebnou stránkou ASP.NET a zpřístupňuje základní vlastnosti, jako jsou `IsPostBack`, `IsValid`, `Request`a `Response`, mezi mnoho dalších. Často, každá stránka webové aplikace vyžaduje další funkce nebo funkce. Běžným způsobem, jak to zajistit, je vytvořit vlastní třídu základní stránky. Vlastní třída základní stránky je třída, kterou vytvoříte, která je odvozena od třídy `Page` a obsahuje další funkce. Po vytvoření této základní třídy můžete mít ASP.NET stránky odvozené od ní (spíše než `Page` třídy), což nabízí rozšířenou funkci na stránky ASP.NET.

V tomto kroku vytvoříme základní stránku, která automaticky nastaví název stránky na název ASP.NET stránky, pokud název není jinak explicitně nastavený. Krok 3 se zabývá nastavením nadpisu stránky v závislosti na mapě webu.

> [!NOTE]
> Důkladné hodnocení vytváření a používání vlastních tříd základní stránky je nad rámec této série kurzů. Další informace najdete v tématu [vlastní základní třída pro třídy kódu na pozadí stránek ASP.NET](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx).

### <a name="creating-the-base-page-class"></a>Vytvoření třídy základní stránky

Naším prvním úkolem je vytvořit třídu základní stránky, což je třída, která rozšiřuje třídu `Page`. Začněte přidáním `App_Code` složky do projektu tak, že kliknete pravým tlačítkem myši na název projektu v Průzkumník řešení, zvolíte Přidat složku ASP.NET a pak vyberete `App_Code`. Potom klikněte pravým tlačítkem myši na složku `App_Code` a přidejte novou třídu s názvem `BasePage.cs`. Obrázek 4 ukazuje Průzkumník řešení po přidání `App_Code` složky a `BasePage.cs` třídy.

![Přidat složku App_Code a třídu s názvem BasePage](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image4.png)

**Obrázek 04**: přidejte složku `App_Code` a třídu s názvem `BasePage`

> [!NOTE]
> Visual Studio podporuje dva režimy řízení projektů: projekty webu a projekty webových aplikací. `App_Code` složka je navržena pro použití s modelem projektu webu. Pokud používáte model projektu webové aplikace, umístěte třídu `BasePage.cs` do složky s názvem něco jiného než `App_Code`, například `Classes`. Další informace o tomto tématu najdete v tématu [migrace webového projektu do projektu webové aplikace](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx).

Vzhledem k tomu, že vlastní základní stránka slouží jako základní třída pro třídy kódu na pozadí ASP.NET Pages, je nutné rozšířenou třídu `Page`.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample5.cs)]

Pokaždé, když se na stránku ASP.NET požadavek pokračuje prostřednictvím řady fází, ukončené na požadované stránce se vykreslují do HTML. Můžete klepnout do fáze přepsáním `OnEvent` metody `Page` třídy. Pro naši základní stránku automaticky nastavíme název, pokud nebyl explicitně zadán ve fázi `LoadComplete` (to, jak jste se mohli uhodnout, nastane po `Load` fázi).

Chcete-li to provést, přepište metodu `OnLoadComplete` a zadejte následující kód:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample6.cs)]

Metoda `OnLoadComplete` začíná určením, zda nebyla dosud explicitně nastavena vlastnost `Title`. Pokud je vlastnost `Title` `null`, prázdný řetězec nebo má hodnotu "bez názvu stránky", je přiřazena k názvu souboru požadované stránky ASP.NET. Fyzická cesta k požadované stránce ASP.NET-`C:\MySites\Tutorial03\Login.aspx`, například je přístupná prostřednictvím vlastnosti `Request.PhysicalPath`. Metoda `Path.GetFileNameWithoutExtension` slouží k vypsání pouze části názvu souboru a tento název souboru je pak přiřazen vlastnosti `Page.Title`.

> [!NOTE]
> Dám se pozvat k vylepšení této logiky za účelem zlepšení formátu názvu. Například pokud je název souboru stránky `Company-Products.aspx`, výše uvedený kód vytvoří název "společnost-Products", ale v ideálním případě by se pomlčka nahradila mezerou, jako v "produkty společnosti". Zvažte také přidání místa vždy, když dojde ke změně velikosti písmen. To znamená, že zvažte přidání kódu, který transformuje název souboru `OurBusinessHours.aspx` na název naší pracovní doby.

### <a name="having-the-content-pages-inherit-the-base-page-class"></a>Stránka obsahu zdědí třídu základní stránky.

Teď je potřeba aktualizovat stránky ASP.NET na našem webu tak, aby se místo `Page` třídy odvodily od vlastní základní stránky (`BasePage`). Chcete-li to dosáhnout, přejděte na každou třídu s kódem na pozadí a změňte deklaraci třídy z:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample7.cs)]

Komu:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample8.cs)]

Po jeho provedení navštivte web prostřednictvím prohlížeče. Pokud navštívíte stránku, jejíž název je explicitně nastavený, například `Default.aspx` nebo `About.aspx`, použije se explicitně zadaný název. Pokud ale navštívíte stránku, jejíž název nebyl změněn z výchozí ("stránka bez názvu"), třída základní stránky nastaví název názvu stránky.

Obrázek 5 zobrazuje stránku `MultipleContentPlaceHolders.aspx` při prohlížení v prohlížeči. Všimněte si, že nadpis je přesně název souboru stránky (menší přípona), "MultipleContentPlaceHolders".

[![Pokud název není explicitně zadaný, automaticky se použije název souboru stránky.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image5.png)

**Obrázek 05**: Pokud název není explicitně zadaný, automaticky se použije název souboru stránky ([kliknutím zobrazíte obrázek v plné velikosti).](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image7.png)

## <a name="step-3-basing-the-page-title-on-the-site-map"></a>Krok 3: založení názvu stránky na mapě webu

ASP.NET nabízí robustní rozhraní mapy webu, které umožňuje vývojářům stránek definovat hierarchickou mapu webu v externím zdroji (například soubor XML nebo databázová tabulka) spolu s webovými ovládacími prvky pro zobrazení informací o mapě webu (například SiteMapPath, Ovládací prvky menu a TreeView).

Ke struktuře mapy webu lze také přistupovat programově ze třídy kódu na pozadí stránky ASP.NET. Tímto způsobem můžeme automaticky nastavit nadpis stránky na název odpovídajícího uzlu na mapě webu. Pojďme vylepšit třídu `BasePage` vytvořenou v kroku 2 tak, aby tuto funkci nabízí. Nejdřív ale musíme vytvořit mapu webu pro náš web.

> [!NOTE]
> V tomto kurzu se předpokládá, že čtenář už je obeznámený s ASP. SÍŤOVÉ funkce mapy webu. Další informace o používání mapy webu najdete v části Moje řady článků s více částmi a [zkoumání ASP. Navigace na pracovišti](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)sítě.

### <a name="creating-the-site-map"></a>Vytváření mapy webu

Systém mapy webu je sestaven základem [modelem poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), který odděluje rozhraní API mapy webu od logiky, která serializace informace o mapě lokality mezi pamětí a trvalým úložištěm. .NET Framework se dodává se [třídou`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx), která je výchozím poskytovatelem mapy webu. V takovém případě `XmlSiteMapProvider` jako úložiště map webů používá soubor XML. Pojďme tohoto poskytovatele použít k definování mapy webu.

Začněte vytvořením souboru mapy webu v kořenové složce webu s názvem `Web.sitemap`. Chcete-li to provést, klikněte pravým tlačítkem myši na název webu v Průzkumník řešení, zvolte možnost Přidat novou položku a vyberte šablonu mapy webu. Zajistěte, aby byl soubor pojmenován `Web.sitemap` a klikněte na tlačítko Přidat.

[![přidat soubor s názvem Web. sitemap do kořenové složky webu](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image8.png)

**Obrázek 6**: Přidání souboru s názvem `Web.sitemap` do kořenové složky webu ([kliknutím zobrazíte obrázek v plné velikosti](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image10.png))

Do souboru `Web.sitemap` přidejte následující kód XML:

[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample9.xml)]

Tento kód XML definuje hierarchickou strukturu mapy webu znázorněnou na obrázku 7.

![Mapa webu se v současné době skládá ze tří uzlů mapy webu.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image11.png)

**Obrázek 07**: Mapa webu se v současné době skládá ze tří uzlů mapy webu.

Strukturu mapy webu budeme aktualizovat v budoucích kurzech, protože přidáváme nové příklady.

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>Aktualizace stránky předlohy tak, aby zahrnovala navigační webové ovládací prvky

Teď, když máme nadefinovanou mapu webu, můžeme aktualizovat stránku předlohy tak, aby zahrnovala webové ovládací prvky navigace. Konkrétně přidejte ovládací prvek ListView do levého sloupce v části lekce, která vykreslí Neseřazený seznam s položkou seznamu pro každý uzel definovaný na mapě webu.

> [!NOTE]
> Ovládací prvek ListView je pro ASP.NET verze 3,5 nový. Pokud používáte předchozí verzi ASP.NET, místo toho použijte ovládací prvek Repeater. Další informace o ovládacím prvku ListView naleznete v tématu [Using ASP.NET 3.5 ListView a Datapageer Controls](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx).

Začněte odebráním existujícího označení neuspořádaného seznamu z části lekce. V dalším kroku přetáhněte ovládací prvek ListView z panelu nástrojů a přetáhněte ho pod nadpis lekce. Ovládací prvek ListView je umístěn v části data v sadě nástrojů spolu s dalšími ovládacími prvky zobrazení: GridView, DetailsView a FormView. Nastavte vlastnost ID prvku ListView na hodnotu `LessonsList`.

V Průvodci konfigurací zdroje dat vyberte možnost navázání objektu ListView k novému ovládacímu prvku SiteMapDataSource s názvem `LessonsDataSource`. Ovládací prvek SiteMapDataSource vrátí hierarchickou strukturu z mapového systému lokality.

[![navázání ovládacího prvku SiteMapDataSource k ovládacímu prvku ListView LessonsList](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image12.png)

**Obrázek 08**: Svázání ovládacího prvku SiteMapDataSource s ovládacím prvkem `LessonsList` ListView ([kliknutím zobrazíte obrázek v plné velikosti](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image14.png))

Po vytvoření ovládacího prvku SiteMapDataSource musíme šablony ListView definovat tak, aby vykreslovat neuspořádaný seznam s položkou seznamu pro každý uzel vrácený ovládacím prvkem SiteMapDataSource. To lze provést pomocí následujícího kódu šablony:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample10.aspx)]

`LayoutTemplate` generuje označení pro neuspořádaný seznam (`<ul>...</ul>`), zatímco `ItemTemplate` vykreslí každou položku vrácenou funkcí SiteMapDataSource jako položku seznamu (`<li>`), která obsahuje odkaz na konkrétní lekci.

Po konfiguraci šablon ListView navštivte web. Jak ukazuje obrázek 9, část lekce obsahuje jednu položku s odrážkou, Domovská stránka. Kde jsou informace o a používání více lekcí ovládacích prvků ContentPlaceHolder? Vlastnost SiteMapDataSource je navržena tak, aby vracela hierarchickou sadu dat, ale ovládací prvek ListView může zobrazit pouze jednu úroveň hierarchie. V důsledku toho se zobrazí pouze první úroveň uzlů mapy webu vrácených pomocí ovládacího panelu SiteMapDataSource.

[![část s informacemi o lekci obsahuje jednu položku seznamu.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image15.png)

**Obrázek 09**: oddíl lekce obsahuje jednu položku seznamu ([kliknutím zobrazíte obrázek v plné velikosti).](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image17.png)

Pokud chcete zobrazit více úrovní, můžeme v rámci `ItemTemplate`vnořit více ListView. Tato technika se prozkoumala na [ *stránkách předlohy a* v kurzu navigace na webu](../../data-access/introduction/master-pages-and-site-navigation-cs.md) v části Moje [práce s řadami kurzů dat](../../data-access/index.md). Pro tuto řadu kurzů ale naše mapa webu bude obsahovat jenom dvě úrovně: domů (nejvyšší úroveň); a každou lekci jako podřízenou položku domů. Místo toho, abychom mohli vytvořit vnořenou vlastnost ListView, můžeme místo toho dát ovládacímu prvku SiteMapDataSource pokyn, aby nevrátil počáteční uzel, nastavením jeho [vlastnosti`ShowStartingNode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) na hodnotu `false`. Čistým účinkem je, že se SiteMapDataSource spustí vrácením druhé vrstvy uzlů mapy webu.

Při této změně ListView zobrazuje položky odrážek pro o a použití více lekcí ovládacích prvků ContentPlaceHolder, ale vynechává položku odrážek pro domovskou stránku. Chcete-li tento problém napravit, můžeme explicitně přidat odrážku pro domovskou položku v `LayoutTemplate`:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample11.aspx)]

Když nakonfigurujete prvek SiteMapDataSource tak, aby vynechal počáteční uzel a explicitně přidalo domovskou odrážku položky, v části lekce se teď zobrazí zamýšlený výstup.

[![část lekce obsahuje položku odrážky pro domovskou stránku a každý podřízený uzel.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image18.png)

**Obrázek 10**: oddíl lekce obsahuje položku odrážky pro domov a každý podřízený uzel ([kliknutím zobrazíte obrázek v plné velikosti).](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image20.png)

### <a name="setting-the-title-based-on-the-site-map"></a>Nastavení názvu na základě mapy webu

Díky mapě webu můžeme aktualizovat naši třídu `BasePage` tak, aby používala název zadaný na mapě webu. Stejně jako v kroku 2 chceme použít název uzlu mapa webu pouze v případě, že název stránky nebyl explicitně nastaven vývojářem stránky. Pokud požadovaná stránka nemá explicitně nastaven nadpis stránky a nebyla nalezena na mapě webu, pak se vrátíme k použití názvu souboru požadované stránky (menšího rozšíření), jak jsme to provedli v kroku 2. Obrázek 11 znázorňuje tento rozhodovací proces.

![V případě nepřítomnosti explicitně nastaveného nadpisu stránky se použije název příslušného uzlu mapy webu.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image21.png)

**Obrázek 11**: v případě neexistence explicitně nastaveného názvu stránky je použit název příslušného uzlu mapy webu.

Aktualizujte metodu `OnLoadComplete` třídy `BasePage` tak, aby obsahovala následující kód:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample12.cs)]

Stejně jako dřív se metoda `OnLoadComplete` spustí tím, že určí, zda byl nadpis stránky explicitně nastaven. Pokud je `Page.Title` `null`, prázdný řetězec nebo je přiřazena hodnota "bez názvu stránky", kód automaticky přiřadí hodnotu `Page.Title`.

Chcete-li určit název, který se má použít, kód začíná odkazem na [vlastnost`CurrentNode`](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx) [třídy`SiteMap`](https://msdn.microsoft.com/library/system.web.sitemap.aspx). `CurrentNode` vrátí instanci [`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) v mapě webu, která odpovídá aktuálně požadované stránce. Za předpokladu, že je aktuálně požadovaná stránka nalezena v mapě webu, je vlastnost `Title` `SiteMapNode`přiřazena k názvu stránky. Pokud není aktuálně požadovaná stránka na mapě webu, `CurrentNode` vrátí `null` a jako název se použije název souboru požadované stránky (jak bylo provedeno v kroku 2).

Obrázek 12 zobrazuje stránku `MultipleContentPlaceHolders.aspx` při prohlížení v prohlížeči. Vzhledem k tomu, že název této stránky není explicitně nastaven, použije se místo toho název příslušného uzlu mapy webu.

![Název stránky MultipleContentPlaceHolders. aspx se načte z mapy webu.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image22.png)

**Obrázek 12**: název stránky `MultipleContentPlaceHolders.aspx` se načte z mapy webu.

## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>Krok 4: Přidání dalších značek specifických pro stránku do oddílu`<head>`

Kroky 1, 2 a 3 se prohlédly při přizpůsobení `<title>`ho prvku na základě stránky. Kromě `<title>`oddíl `<head>` může obsahovat `<meta>` prvky a `<link>` elementy. Jak bylo uvedeno výše v tomto kurzu, `Site.master``<head>` oddíl obsahuje `<link>` prvek `Styles.css`. Vzhledem k tomu, že tento element `<link>` je definován v rámci stránky předlohy, je obsažen v části `<head>` pro všechny stránky obsahu. Ale jak se chystám přidat `<meta>` a `<link>` prvky na stránku na základě stránky?

Nejjednodušší způsob, jak do oddílu `<head>` přidat obsah specifický pro stránku, je vytvoření ovládacího prvku ContentPlaceHolder na stránce předlohy. Již máme takové prvky ContentPlaceHolder (s názvem `head`). Proto chcete-li přidat vlastní kód `<head>`, vytvořte na stránce odpovídající ovládací prvek obsahu a vložte značku do něj.

Pro ilustraci Přidání vlastního kódu `<head>` na stránku, přiřadíme element `<meta>` Description na naši aktuální sadu stránek obsahu. Element Description `<meta>` poskytuje stručný popis webové stránky. Většina vyhledávacích modulů při zobrazení výsledků hledání zahrnuje tyto informace v některém formuláři.

Element Description `<meta>` má následující tvar:

[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample13.html)]

Chcete-li přidat tento kód na stránku obsahu, přidejte výše uvedený text do ovládacího prvku Content, který je namapován na hlavní ovládací prvek head stránky předlohy. Například pro definování prvku `<meta>` Description pro `Default.aspx`přidejte následující kód:

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample14.aspx)]

Vzhledem k tomu, že Head ContentPlaceHolder není v těle stránky HTML, značka přidaná do ovládacího prvku obsahu se nezobrazí v zobrazení Návrh. Chcete-li zobrazit prvek popis `<meta>` navštívit `Default.aspx` prostřednictvím prohlížeče. Po načtení stránky zobrazte zdroj a Všimněte si, že část `<head>` obsahuje značku určenou v ovládacím prvku Content.

Počkejte, než se doplňte prvky `<meta>` Description do `About.aspx`, `MultipleContentPlaceHolders.aspx`a `Login.aspx`.

### <a name="programmatically-adding-markup-to-theheadregion"></a>Programové přidávání značek do`<head>`oblasti

Hlavní ovládací prvek ContentPlaceHolder umožňuje deklarativní Přidání vlastního kódu do `<head>` oblasti hlavní stránky. Vlastní značky se taky dají přidat prostřednictvím kódu programu. Odvolání, že vlastnost `Header` třídy `Page` vrací instanci `HtmlHead` definovanou na stránce předlohy (`<head runat="server">`).

Schopnost programově přidávat obsah do `<head>` oblasti je užitečná, když je obsah, který se má přidat, dynamický. Možná je to na základě uživatele, který navštívil stránku. pravděpodobně je načítán z databáze. Bez ohledu na důvod můžete přidat obsah do `HtmlHead` přidáním ovládacích prvků do kolekce ovládacích prvků, například takto:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample15.cs)]

Výše uvedený kód přidá prvek klíčová slova `<meta>` do oblasti `<head>`, která poskytuje seznam klíčových slov s oddělovači, které popisují tuto stránku. Všimněte si, že pokud chcete přidat značku `<meta>`, vytvoříte instanci [`HtmlMeta`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx) , nastavíte její vlastnosti `Name` a `Content` a přidáte ji do `Header`kolekce `Controls`. Podobně pokud chcete programově přidat `<link>` element, vytvořte objekt [`HtmlLink`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx) , nastavte jeho vlastnosti a pak ho přidejte do kolekce `Controls` `Header`.

> [!NOTE]
> Chcete-li přidat libovolný kód, vytvořte instanci [`LiteralControl`](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx) , nastavte její vlastnost `Text` a pak ji přidejte do kolekce `Controls` `Header`.

## <a name="summary"></a>Souhrn

V tomto kurzu jsme se vyhledali různými způsoby, jak přidat `<head>` označení oblasti na stránce. Hlavní stránka by měla zahrnovat `HtmlHead` instanci (`<head runat="server">`) s ovládacím prvky ContentPlaceHolder. Instance `HtmlHead` umožňuje stránkám obsahu programově přistupovat k oblasti `<head>` a deklarativně a programově nastavit nadpis stránky. ovládací prvek ContentPlaceHolder umožňuje přidat vlastní kód do oddílu `<head>` deklarativně prostřednictvím ovládacího prvku obsahu.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Dynamické nastavení nadpisu stránky v ASP.NET](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [Prozkoumává se ASP. SÍŤ – navigace na webu](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Používání značek Meta HTML](http://searchenginewatch.com/showPage.html?page=2167931)
- [Stránky předlohy v ASP.NET](http://www.odetocode.com/articles/419.aspx)
- [Používání ovládacích prvků ListView a DataPager v ASP.NET 3.5](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [Použití vlastní základní třídy pro třídy kódu na pozadí ASP.NET stránek](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Zack Novotný a Banerjee. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](multiple-contentplaceholders-and-default-content-cs.md)
> [Další](urls-in-master-pages-cs.md)
