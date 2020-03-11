---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: Přehled zobrazení ASP.NET MVC (VB) | Microsoft Docs
author: StephenWalther
description: Co je zobrazení ASP.NET MVC a jak se liší od stránky HTML? V tomto kurzu Stephen Walther představuje zobrazení a ukazuje, jak můžete t...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f02728ed248f29b09d654e509977ed43889cbb83
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541305"
---
# <a name="aspnet-mvc-views-overview-vb"></a>ASP.NET MVC – přehled zobrazení (VB)

od [Stephen Walther](https://github.com/StephenWalther)

> Co je zobrazení ASP.NET MVC a jak se liší od stránky HTML? V tomto kurzu vám Stephen Walther představuje zobrazení a ukazuje, jak můžete využít výhod zobrazení dat a pomocníků HTML v rámci zobrazení.

Účelem tohoto kurzu je poskytnout stručný úvod do ASP.NETch zobrazení MVC, zobrazit data a pomocníky HTML. Na konci tohoto kurzu byste měli pochopit, jak vytvářet nová zobrazení, předávat data z kontroleru do zobrazení a používat pomocníky HTML pro generování obsahu v zobrazení.

## <a name="understanding-views"></a>Porozumění zobrazením

Na rozdíl od ASP.NET nebo Active Server stránek nezahrnuje ASP.NET MVC cokoli, co přímo odpovídá stránce. V aplikaci ASP.NET MVC není na disku žádná stránka, která by odpovídala cestě v adrese URL, kterou zadáte do panelu Adresa v prohlížeči. Nejbližší věc stránky v aplikaci ASP.NET MVC se říká *zobrazení*.

V aplikaci ASP.NET MVC jsou příchozí požadavky prohlížeče namapovány na akce kontroleru. Akce kontroleru může vrátit zobrazení. Akce kontroleru ale může provést nějaký jiný typ akce, například přesměrování na jinou akci kontroleru.

Výpis 1 obsahuje jednoduchý řadič s názvem HomeController. HomeController zpřístupňuje dvě akce kontroleru s názvem index () a podrobnosti ().

**Výpis 1 – HomeController. vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

Můžete vyvolat první akci, akci index () zadáním následující adresy URL do adresního řádku prohlížeče:

/Home/Index

Druhou akci, akci podrobnosti () můžete vyvolat tak, že do svého prohlížeče zadáte tuto adresu:

/Home/Details

Akce index () vrátí zobrazení. Většina akcí, které vytvoříte, budou vracet zobrazení. Akce však může vracet jiné typy výsledků akce. Například akce podrobnosti () vrátí RedirectToActionResult, který přesměruje příchozí požadavek do akce index ().

Akce index () obsahuje následující jeden řádek kódu:

Zobrazit ()

Tento řádek kódu vrátí zobrazení, které se musí nacházet na následujícím umístění na webovém serveru:

\Views\Home\Index.aspx

Cesta k zobrazení je odvozena z názvu kontroleru a názvu akce kontroleru.

Pokud budete chtít, můžete být pro zobrazení explicitní. Následující řádek kódu vrátí zobrazení s názvem Fred:

Zobrazení (Fred)

Při spuštění tohoto řádku kódu se vrátí zobrazení z následující cesty:

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> Pokud máte v úmyslu vytvořit testy jednotek pro aplikaci ASP.NET MVC, je vhodné, abyste měli explicitní informace o názvech zobrazení. Tímto způsobem můžete vytvořit testování částí a ověřit tak, že se očekávané zobrazení vrátilo pomocí akce kontroleru.

## <a name="adding-content-to-a-view"></a>Přidání obsahu do zobrazení

Zobrazení je standardní dokument HTML (X) HTML, který může obsahovat skripty. Pomocí skriptů můžete přidat dynamický obsah do zobrazení.

Například zobrazení v seznamu 2 zobrazí aktuální datum a čas.

**Výpis 2 – \Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

Všimněte si, že tělo stránky HTML v seznamu 2 obsahuje následující skript:

&lt;% Response. Write (DateTime. Now)%&gt;

Pomocí oddělovačů skriptů &lt;% a%&gt; označíte začátek a konec skriptu. Tento skript je napsán v jazyce Visual Basic. Zobrazí aktuální datum a čas voláním metody Response. Write () pro vykreslení obsahu do prohlížeče. Oddělovače skriptů &lt;% a%&gt; lze použít ke spuštění jednoho nebo více příkazů.

Vzhledem k tomu, že zavoláte Response. Write () tak často, společnost Microsoft poskytuje zástupce pro volání metody Response. Write (). Zobrazení v seznamu 3 používá oddělovače &lt;% = a%&gt; jako zástupce pro volání metody Response. Write ().

**Výpis 3 – Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

K vygenerování dynamického obsahu v zobrazení můžete použít libovolný jazyk rozhraní .NET. Za normálních okolností můžete použít buď Visual Basic .NET C# , nebo můžete zapisovat řadiče a zobrazení.

## <a name="using-html-helpers-to-generate-view-content"></a>Použití pomocníků HTML ke generování obsahu zobrazení

Aby bylo snazší přidávat obsah do zobrazení, můžete využít něco jako *pomocníka HTML*. Pomocný objekt HTML je obvykle metoda, která generuje řetězec. Můžete použít pomocníky HTML k vygenerování standardních HTML prvků, jako jsou textová pole, odkazy, rozevírací seznamy a seznam polí.

Například zobrazení v seznamu 4 využívá tři pomocníky HTML – BeginForm (), textové pole () a heslo () – pro vygenerování přihlašovacího formuláře (viz obrázek 1).

**Výpis 4 – \Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

[![dialogového okna Nový projekt](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**Obrázek 01**: standardní přihlašovací formulář ([kliknutím zobrazíte obrázek v plné velikosti](asp-net-mvc-views-overview-vb/_static/image2.png))

Všechny metody pomocníka HTML jsou volány ve vlastnosti HTML zobrazení. Například můžete vykreslit textové pole voláním metody HTML. TextBox ().

Všimněte si, že používáte oddělovače skriptů &lt;% = a%&gt; při volání pomocníků HTML. TextBox () a HTML. Password (). Tyto pomocníky jednoduše vrátí řetězec. Pro vykreslení řetězce do prohlížeče je nutné zavolat Response. Write ().

Použití pomocných metod jazyka HTML je volitelné. Díky omezení množství HTML a skriptu, který je potřeba napsat, zjednoduší život. Zobrazení v seznamu 5 vykreslí přesně stejný tvar jako zobrazení v seznamu 4 bez použití pomocníků HTML.

**Výpis 5 – \Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

Máte také možnost vytvořit si vlastní pomocníky HTML. Můžete například vytvořit pomocnou metodu GridView (), která zobrazí sadu záznamů databáze v tabulce HTML automaticky. Prozkoumáme toto téma v kurzu **vytváření vlastních pomocníků HTML**.

## <a name="using-view-data-to-pass-data-to-a-view"></a>Použití zobrazení dat k předání dat do zobrazení

Pomocí zobrazení dat můžete předávat data z kontroleru do zobrazení. Představte si zobrazení dat, jako je balíček, který odešlete prostřednictvím e-mailu. Všechna data předaná z kontroleru do zobrazení se musí odeslat pomocí tohoto balíčku. Například kontroler v výpisu 6 přidá zprávu pro zobrazení dat.

**Výpis 6 – ProductController. vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

Vlastnost Controller ViewData představuje kolekci párů název-hodnota. V výpisu 6 metoda index () přidá položku do kolekce zobrazení dat s názvem Zpráva s hodnotou Hello World!. Když je zobrazení vráceno metodou index (), zobrazení dat se automaticky předává do zobrazení.

Zobrazení v seznamu 7 načte zprávu z dat zobrazení a vykreslí zprávu do prohlížeče.

**Výpis 7 – \Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

Všimněte si, že zobrazení při vykreslování zprávy využívá pomocnou metodu HTML. Encode () HTML. Pomocný kód HTML. Encode () HTML kóduje speciální znaky, například &lt; a &gt; do znaků, které jsou bezpečné pro zobrazení na webové stránce. Kdykoli vykreslíte obsah, který uživatel odešle na web, měli byste zakódovat obsah a zabránit tak útokům prostřednictvím injektáže JavaScriptu.

(Vzhledem k tomu, že jsme v ProductController vytvořili zprávu dodržovali, nemusíme ji opravdu kódovat. Je však dobrým zvykem při zobrazování obsahu načteného z zobrazení dat načtených v zobrazení, vždy při volání metody HTML. Encode ().)

V seznamu 7 jsme využili výhod zobrazení dat k předání jednoduché zprávy řetězce z řadiče do zobrazení. Pomocí zobrazení dat můžete také předat další typy dat, jako je například kolekce záznamů databáze, z kontroleru do zobrazení. Například pokud chcete zobrazit obsah tabulky databáze produktů v zobrazení, pak byste měli předat kolekci záznamů databáze v zobrazení dat.

Máte také možnost předat data zobrazení silného typu z kontroleru do zobrazení. Toto téma se zabývá v kurzu, který popisuje **zobrazení dat a zobrazení silného typu**.

## <a name="summary"></a>Souhrn

V tomto kurzu najdete stručný úvod k ASP.NET zobrazením MVC, zobrazení dat a pomocníkům HTML. V první části jste se dozvěděli, jak přidat nová zobrazení do projektu. Zjistili jste, že musíte přidat zobrazení do pravé složky, abyste ho mohli zavolat z konkrétního kontroleru. Dále jsme probrali téma nápovědy HTML. Zjistili jste, jak vám pomocník HTML umožňuje snadno vygenerovat standardní obsah HTML. Nakonec jste zjistili, jak využít výhod zobrazení dat k předávání dat z kontroleru do zobrazení.

> [!div class="step-by-step"]
> [Předchozí](passing-data-to-view-master-pages-cs.md)
> [Další](creating-custom-html-helpers-vb.md)
