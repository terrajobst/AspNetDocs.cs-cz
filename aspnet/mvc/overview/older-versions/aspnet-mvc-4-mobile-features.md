---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 – mobilní funkce | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu je teď verze MVC 5 tohoto kurzu s ukázkami kódu v nasazení mobilní webové aplikace ASP.NET MVC 5 na webech Azure.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 907a16946c93761cd543135b0b226c8696b041f0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594297"
---
# <a name="aspnet-mvc-4-mobile-features"></a>Funkce mobilní architektury ASP.NET MVC 4

Od [Rick Anderson]((https://twitter.com/RickAndMSFT))

> V tomto kurzu je teď verze MVC 5 tohoto kurzu s ukázkami kódu v [Nasazení mobilní webové aplikace ASP.NET MVC 5 na webech Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).

V tomto kurzu se naučíte základy práce s mobilními funkcemi ve webové aplikaci ASP.NET MVC 4. Pro tento kurz můžete použít [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) nebo Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer nebo souboru vwd&quot;). Pokud již máte, můžete použít profesionální verzi sady Visual Studio.

Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže.

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (doporučeno) nebo Visual Studio Web Developer Express SP1. Visual Studio 2012 obsahuje ASP.NET MVC 4. Pokud používáte aplikaci Visual Web Developer 2010, je nutné nainstalovat [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).

Budete také potřebovat emulátor mobilního prohlížeče. Bude fungovat kterýkoli z následujících postupů:

- [Emulátor pro Windows 7 Phone](https://msdn.microsoft.com/library/ff402563(VS.92).aspx). (Jedná se o emulátor, který se používá ve většině snímků obrazovky v tomto kurzu.)
- Změňte řetězec uživatelského agenta tak, aby emuluje iPhone. Podívejte se na [tuto](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) položku blogu.
- [Emulátor mobilního emulátoru Opera](http://www.opera.com/developer/tools/mobile/)
- [Apple Safari](http://www.apple.com/safari/download/) s uživatelským agentem nastaveným na iPhone. Pokyny, jak nastavit agenta uživatele v Safari na "iPhone", najdete v článku [jak umožnit Safari předstírat se](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) na blogu David ALISON v IE.

Projekty sady Visual Studio C# se zdrojovým kódem jsou k dispozici pro toto téma:

- [Stažení projektu Starter](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [Stažení dokončeného projektu](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>Co sestavíte

Pro tento kurz přidáte mobilní funkce do jednoduché aplikace výpisu konferencí, která je k dispozici v [počátečním projektu](https://go.microsoft.com/fwlink/?LinkId=228307). Na následujícím snímku obrazovky vidíte stránku značek dokončené aplikace, jak je vidět v [emulátoru telefonu pro Windows 7](https://msdn.microsoft.com/library/ff402563(VS.92).aspx). Pokud chcete zjednodušit vstup z klávesnice, přečtěte si téma [mapování klávesnice pro Windows Phone emulátor](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) .

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

K vývoji mobilní aplikace můžete použít Internet Explorer verze 9 nebo 10, FireFox nebo Chrome nastavením [řetězce uživatelského agenta](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/). Následující obrázek znázorňuje dokončený kurz pomocí aplikace Internet Explorer emulující iPhone. K ladění aplikace můžete použít nástroje pro vývojáře v aplikaci Internet Explorer F-12 a [Nástroj Fiddler](http://www.fiddler2.com/fiddler2/) .

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>Dovednosti, se kterými se naučíte

Tady je seznam toho, co se naučíte:

- Jak šablony ASP.NET MVC 4 používají atribut HTML5 `viewport` a adaptivní vykreslování pro zlepšení zobrazení na mobilních zařízeních.
- Vytváření zobrazení specifických pro mobilní zařízení.
- Jak vytvořit přepínač zobrazení, který uživatelům umožňuje přepínat mezi mobilním zobrazením a zobrazením plochy aplikace.

### <a name="getting-started"></a>Začínáme

Stáhněte si aplikaci pro výpis konference pro počáteční projekt pomocí následujícího odkazu: [Stáhnout](https://go.microsoft.com/fwlink/?LinkId=228307). Pak v Průzkumníkovi Windows klikněte pravým tlačítkem na soubor *MvcMobile. zip* a zvolte **vlastnosti**. V dialogovém okně **vlastnosti MvcMobile. zip** vyberte tlačítko **odblokování** . (Odblokování zabraňuje upozornění zabezpečení, které se vyskytne při pokusu o použití souboru *. zip* , který jste stáhli z webu.)

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

Klikněte pravým tlačítkem na soubor *MvcMobile. zip* a vyberte **Rozbalit vše pro rozbalení** souboru. V aplikaci Visual Studio otevřete soubor *MvcMobile. sln* .

Stisknutím kombinace kláves CTRL + F5 spusťte aplikaci, která se zobrazí v prohlížeči na ploše. Spusťte emulátor mobilního prohlížeče, zkopírujte adresu URL pro aplikaci konference do emulátoru a potom klikněte na odkaz **Procházet podle značky** . Pokud používáte emulátor Windows Phone, klikněte na panelu Adresa URL a stisknutím klávesy Pause získáte přístup k klávesnici. Následující obrázek ukazuje zobrazení *AllTags* (výběr možnosti **Procházet podle značky**).

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

Zobrazení je velmi čitelné na mobilním zařízení. Klikněte na odkaz ASP.NET.

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

Zobrazení značek ASP.NET je velmi zbytečné. Například sloupec **data** je velmi obtížné přečíst. Později v tomto kurzu vytvoříte verzi zobrazení *AllTags* , která je určená konkrétně pro mobilní prohlížeče a která umožní čtení zobrazení.

Poznámka: v současné době existuje chyba v modulu ukládání do mezipaměti pro mobilní zařízení. V případě produkčních aplikací je nutné nainstalovat [opravený balíček DisplayMode](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) zrnkos. Podrobnosti o opravě najdete v tématu věnovaném [chybě ukládání do mezipaměti pro mobilní služby ASP.NET MVC 4](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) .

## <a name="css-media-queries"></a>Dotazy na média CSS

[Dotazy na média CSS](http://www.w3.org/TR/css3-mediaqueries/) jsou rozšíření šablon stylů CSS pro typy médií. Umožňují vytvářet pravidla, která přepisují výchozí pravidla CSS pro konkrétní prohlížeče (uživatelské agenty). Běžné pravidlo pro šablonu stylů CSS, které cílí na mobilní prohlížeče, definuje maximální velikost obrazovky. Soubor *Content\Site.CSS* , který se vytvoří při vytvoření nového ASP.NET projektu MVC 4, obsahuje následující multimediální dotaz:

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

Pokud je okno prohlížeče 850 pixelů na šířku nebo méně, budou použita pravidla šablony stylů CSS v tomto bloku média. Pomocí multimediálních dotazů šablon stylů CSS můžete poskytnout lepší zobrazení obsahu HTML v malých prohlížečích (například v mobilních prohlížečích) než výchozí pravidla šablon stylů CSS, která jsou navržena pro širší zobrazení desktopových prohlížečů.

## <a name="the-viewport-meta-tag"></a>Meta značka zobrazení

Většina mobilních prohlížečů definuje šířku okna virtuálního prohlížeče ( *zobrazení*), která je mnohem větší než skutečná šířka mobilního zařízení. To umožňuje mobilním prohlížečům umístit celou webovou stránku do virtuálního zobrazení. Uživatelé se pak můžou přiblížit k zajímavému obsahu. Pokud však nastavíte šířku zobrazení na skutečnou šířku zařízení, není nutné žádné přiblížení, protože obsah se vejde do mobilního prohlížeče.

Zobrazení `<meta>` značka v souboru rozložení ASP.NET MVC 4 nastaví zobrazení na šířku zařízení. Následující řádek ukazuje zobrazení `<meta>` značku v souboru rozložení ASP.NET MVC 4.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>Zkoumání efektu dotazů na média CSS a značky meta zobrazení

V editoru otevřete soubor *Views\Shared\\_Layout. cshtml* a odkomentujte `<meta>` značku zobrazení. Následující kód ukazuje řádek s komentářem.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

Otevřete soubor *MvcMobile\Content\Site.CSS* v editoru a změňte maximální šířku dotazu na média na nula pixelů. Tím zabráníte použití pravidel CSS v mobilních prohlížečích. Upravený multimediální dotaz se zobrazuje na následujícím řádku:

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

Uložte změny a přejděte do aplikace konference v emulátoru mobilního prohlížeče. Malý text na následujícím obrázku je výsledkem odebrání zobrazení `<meta>` značku. Bez zobrazení `<meta>` značku, prohlížeč se přiblíží k výchozí šířce zobrazení (850 pixelů nebo širší pro většinu mobilních prohlížečů).

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

Vrátit zpět změny – Odkomentujte zobrazení `<meta>` značku v souboru rozložení a obnovte dotaz média na 850 pixelů v souboru *site. CSS* . Uložte změny a aktualizujte mobilní prohlížeč, aby se ověřilo, že se obnovilo mobilní zobrazení.

Zobrazení `<meta>` značka a dotaz na média CSS nejsou specifické pro ASP.NET MVC 4 a můžete využít výhod těchto funkcí v jakékoli webové aplikaci. Jsou však nyní integrovány do souborů, které jsou generovány při vytváření nového projektu ASP.NET MVC 4.

Další informace o zobrazení `<meta>` značky naleznete v části se [dvěma zobrazeními – druhá část](http://www.quirksmode.org/mobile/viewports2.html).

V další části se dozvíte, jak poskytnout zobrazení specifická pro mobilní prohlížeče.

## <a name="overriding-views-layouts-and-partial-views"></a>Přepsání zobrazení, rozložení a částečných zobrazení

Významnou novou funkcí v ASP.NET MVC 4 je jednoduchý mechanismus, který umožňuje potlačit libovolné zobrazení (včetně rozložení a částečných zobrazení) pro mobilní prohlížeče obecně, pro jednotlivé mobilní prohlížeče nebo pro všechny konkrétní prohlížeče. Chcete-li poskytnout zobrazení pro konkrétní mobilní zařízení, můžete zkopírovat soubor zobrazení a přidat *. Mobilní* na název souboru. Chcete-li například vytvořit zobrazení mobilního *indexu* , zkopírujte *Views\Home\Index.cshtml* do *Views\Home\Index.Mobile.cshtml*.

V této části vytvoříte soubor rozložení specifický pro mobilní zařízení.

Spusťte kopírování *Views\Shared\\_Layout. cshtml* do *Views\Shared\\_Layout. Mobile. cshtml*. Otevřete *\_layout. Mobile. cshtml* a změňte název z **konference MVC4** na **konferenci (mobilní)** .

V každém volání `Html.ActionLink` odeberte "Procházet podle" v každém odkazu *ActionLink*. Následující kód ukazuje část hotový text v souboru rozložení pro mobilní zařízení.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

Zkopírujte soubor *Views\Home\AllTags.cshtml* do *Views\Home\AllTags.Mobile.cshtml*. Otevřete nový soubor a změňte `<h2>` element z "Tags" na "Tags" (M) ":

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

Přejděte na stránku značky pomocí klasického prohlížeče a pomocí emulátoru v mobilním prohlížeči. Emulátor mobilního prohlížeče zobrazuje dvě změny, které jste provedli.

[![p2m_layoutTags. Mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

Naproti tomu se zobrazení plochy nezměnilo.

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>Zobrazení specifická pro prohlížeč

Kromě zobrazení specifických pro mobilní zařízení a pro stolní počítače můžete vytvořit zobrazení pro jednotlivé prohlížeče. Můžete například vytvořit zobrazení, která jsou speciálně pro prohlížeč iPhone. V této části vytvoříte rozložení pro iPhone Browser a verzi iPhone *AllTags* zobrazení.

Otevřete soubor *Global. asax* a přidejte následující kód do metody `Application_Start`.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

Tento kód definuje nový režim zobrazení s názvem iPhone, který se bude shodovat s každým příchozím požadavkem. Pokud příchozí požadavek odpovídá definované hodnotě (tj. Pokud uživatelský agent obsahuje řetězec "iPhone"), ASP.NET MVC bude hledat zobrazení, jejichž název obsahuje příponu "iPhone".

V kódu klikněte pravým tlačítkem myši `DefaultDisplayMode`, zvolte možnost **vyřešit**a pak zvolte možnost `using System.Web.WebPages;`. Tím se přidá odkaz na obor názvů `System.Web.WebPages`, kde jsou definovány typy `DisplayModes` a `DefaultDisplayMode`.

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

Alternativně můžete ručně přidat následující řádek do oddílu `using` souboru.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

Úplný obsah souboru *Global. asax* je uveden níže.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

Uložte změny. Zkopírujte soubor *MvcMobile\Views\Shared\\_Layout. Mobile. cshtml* do *MvcMobile\Views\Shared\\_Layout. iPhone. cshtml*. Otevřete nový soubor a potom změňte nadpis `h1` z `Conference (Mobile)` na `Conference (iPhone)`.

Zkopírujte soubor *MvcMobile\Views\Home\AllTags.Mobile.cshtml* do *MvcMobile\Views\Home\AllTags.iPhone.cshtml*. V novém souboru změňte `<h2>` element z "Tags (M)" na "Tags (iPhone)".

Spusťte aplikaci. Spusťte emulátor mobilního prohlížeče, ujistěte se, že je jeho uživatelský agent nastavený na "iPhone", a přejděte do zobrazení *AllTags* . Na následujícím snímku obrazovky vidíte zobrazení *AllTags* vygenerované v prohlížeči [Safari](http://www.apple.com/safari/download/) . Safari pro Windows si můžete stáhnout [tady](https://support.apple.com/kb/DL1531).

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

V této části jsme viděli, jak vytvořit mobilní rozložení a zobrazení a jak vytvářet rozložení a zobrazení pro konkrétní zařízení, jako je iPhone. V další části se dozvíte, jak využít jQuery Mobile pro působivější mobilní zobrazení.

## <a name="using-jquery-mobile"></a>Použití jQuery Mobile

Knihovna [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) poskytuje rozhraní pro uživatelské rozhraní, které funguje ve všech hlavních mobilních prohlížečích. jQuery Mobile používá *progresivní rozšíření* pro mobilní prohlížeče, které podporují šablony stylů CSS a JavaScript. Progresivní navýšení umožňuje všem prohlížečům zobrazit základní obsah webové stránky a zároveň umožnit výkonnějším prohlížečům a zařízením lepší zobrazení. Soubory jazyka JavaScript a CSS, které jsou součástí funkce jQuery Mobile Style, obsahují mnoho prvků, které odpovídají mobilním prohlížečům bez jakýchkoli změn kódu.

V této části nainstalujete balíček NuGet *jQuery. Mobile. Mvc* , který nainstaluje jQuery Mobile a widget pro přepínač zobrazení.

Chcete-li začít, odstraňte *sdílené\\_Layout. Mobile. cshtml* a *shared\\_Layout soubory. iPhone. cshtml* , které jste vytvořili dříve.

Přejmenujte soubory *Views\Home\AllTags.Mobile.cshtml* a *Views\Home\AllTags.iPhone.cshtml* na *Views\Home\AllTags.iPhone.cshtml.Hide* a *Views\Home\AllTags.Mobile.cshtml.Hide*. Vzhledem k tomu, že soubory již nemají příponu *. cshtml* , nebudou použity modulem runtime ASP.NET MVC k vykreslení zobrazení *AllTags* .

Nainstalujte balíček NuGet *jQuery. Mobile. Mvc* tímto způsobem:

1. V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. V **konzole správce balíčků**zadejte `Install-Package jQuery.Mobile.MVC -version 1.0.0`

Následující obrázek ukazuje soubory přidané a změněné do projektu MvcMobile pomocí balíčku NuGet jQuery. Mobile. MVC. Přidané soubory mají za název souboru doplněny [Add]. V imagi se nezobrazuje soubory GIF a PNG přidané do složky *Content\images* .

![](aspnet-mvc-4-mobile-features/_static/image21.png)

Balíček NuGet jQuery. Mobile. MVC nainstaluje následující:

- *Aplikace\_souboru Start\BundleMobileConfig.cs* , který je potřeba pro odkazování na přidané soubory JAVASCRIPTU a šablony pro jQuery. Musíte postupovat podle následujících pokynů a odkazovat na mobilní sadu definovanou v tomto souboru.
- soubory v mobilní ŠABLONĚ.
- Widget kontroleru `ViewSwitcher` (*Controllers\ViewSwitcherController.cs*).
- soubory JavaScriptu pro mobilní zařízení
- Soubor rozložení s mobilním stylem jQuery (*Views\Shared\\_Layout. Mobile. cshtml*).
- Částečné zobrazení s přepínačem zobrazení *(MvcMobile\Views\Shared\\_ViewSwitcher. cshtml*), které poskytuje odkaz v horní části každé stránky pro přepínání z desktopového zobrazení do mobilního zobrazení a naopak.
- Několik souborů obrázků<em>. png</em> a <em>. gif</em> ve složce <em>Content\images</em>

Otevřete soubor *Global. asax* a přidejte následující kód jako poslední řádek metody `Application_Start`.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

Následující kód ukazuje kompletní soubor *Global. asax* .

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> Pokud používáte Internet Explorer 9 a `BundleMobileConfig` řádek výše ve žlutém zvýraznění, klikněte na tlačítko [zobrazení kompatibility](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Obrázek tlačítka zobrazení kompatibility (vypnuto)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Obrázek tlačítka pro zobrazení kompatibility (vypnuto)") v IE, aby se ikona změnila z ![obrázku](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Obrázek tlačítka pro zobrazení kompatibility (vypnuto)") v osnově tlačítka zobrazení kompatibility (zapnuto) na plný barevný obrázek tlačítka kompatibilního zobrazení ![(zapnuto](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Obrázek tlačítka zobrazení kompatibility (zapnuto)")). Případně můžete tento kurz zobrazit v prohlížeči FireFox nebo Chrome.

Otevřete soubor *MvcMobile\Views\Shared\\_Layout. Mobile. cshtml* a přidejte následující značku přímo po `Html.Partial` volání:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

Úplný soubor *MvcMobile\Views\Shared\\_Layout. Mobile. cshtml* je zobrazený níže:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

Sestavte aplikaci a v emulátoru mobilního prohlížeče přejděte do zobrazení *AllTags* . Zobrazí se následující:

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> Kód specifický pro mobilní zařízení můžete ladit [nastavením řetězce uživatelského agenta](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) pro IE nebo Chrome na iPhone a pak pomocí vývojářských nástrojů F-12. Pokud v mobilním prohlížeči nejsou odkazy na **domovskou stránku**, **mluvčí**, **značku**a **kalendářních dat** , je pravděpodobné, že odkazy na skripty jQuery a soubory CSS nejsou správné.

Kromě změny stylu se zobrazí zobrazení **mobilního zobrazení** a odkaz, který vám umožní přepnout z mobilního zobrazení do desktopového zobrazení. Klikněte na odkaz **zobrazení plochy** a zobrazí se zobrazení plocha.

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

Zobrazení plochy neposkytuje způsob, jak přímo přejít zpět do mobilního zobrazení. Nyní ji opravíte. Otevřete soubor *Views\Shared\\_Layout. cshtml* . Hned pod elementem `body` stránky přidejte následující kód, který vykresluje widget pro přepínač zobrazení:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

Aktualizujte zobrazení *AllTags* v mobilním prohlížeči. Teď můžete přecházet mezi zobrazeními počítačů a mobilních zařízení.

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> Poznámka k ladění: následující kód můžete přidat na konec Views\Shared\\_ViewSwitcher. cshtml pro usnadnění ladění zobrazení při použití prohlížeče řetězce uživatelského agenta nastaveného na mobilní zařízení.
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> a přidáním následujícího nadpisu do souboru *Views\Shared\\_Layout. cshtml* .
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

Přejděte na stránku *AllTags* v desktopovém prohlížeči. Widget pro přepínání zobrazení není zobrazený v desktopovém prohlížeči, protože je přidaný jenom na stránku rozložení pro mobilní zařízení. Později v tomto kurzu uvidíte, jak můžete přidat widget pro přepínání zobrazení do zobrazení plochy.

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>Vylepšení seznamu mluvčích

V mobilním prohlížeči vyberte odkaz **reproduktory** . Vzhledem k tomu, že není k dispozici mobilní zobrazení (*AllSpeakers. Mobile. cshtml*), je výchozí zobrazení mluvčího (*AllSpeakers. cshtml*) vykresleno pomocí zobrazení rozložení pro mobilní zařízení ( *\_layout. Mobile. cshtml*).

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

Můžete globálně zakázat výchozí (nemobilní) zobrazení z vykreslování v mobilním rozložení nastavením `RequireConsistentDisplayMode` na `true` v *zobrazeních\\_ViewStart souboru. cshtml* , například takto:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

Pokud je `RequireConsistentDisplayMode` nastaveno na `true`, je mobilní rozložení (<em>\_layout. Mobile. cshtml</em>) použito pouze pro mobilní zobrazení. (To znamená, že soubor zobrazení má formu <em>* * viewName</em><em>. Mobile. cshtml</em>.) možná budete chtít nastavit `RequireConsistentDisplayMode`, aby `true`, pokud vaše mobilní rozložení nefunguje dobře s nemobilními zobrazeními. Následující snímek obrazovky ukazuje, jak se stránka <em>mluvčí</em> vykreslí, když je `RequireConsistentDisplayMode` nastavená na `true`.

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

Režim konzistentního zobrazení můžete zakázat v zobrazení nastavením `RequireConsistentDisplayMode` na `false` v souboru zobrazení. Následující značky v sadě souborů *Views\Home\AllSpeakers.cshtml* `RequireConsistentDisplayMode` `false`:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>Vytvoření zobrazení mobilního mluvčího

Jak jste viděli, je zobrazení *mluvčích* čitelné, ale odkazy jsou malé a v mobilním zařízení je obtížné klepnout. V této části vytvoříte zobrazení *mluvčích* specifických pro mobilní zařízení, které vypadá jako moderní mobilní aplikace – zobrazuje velké, snadno ovladatelné odkazy a obsahuje vyhledávací pole pro rychlé vyhledání mluvčích.

Zkopírujte *AllSpeakers. cshtml* do *AllSpeakers. Mobile. cshtml*. Otevřete soubor *AllSpeakers. Mobile. cshtml* a odeberte `<h2>` element záhlaví.

Ve značce `<ul>` přidejte atribut `data-role` a nastavte jeho hodnotu na `listview`. Podobně jako u jiných [atributů`data-*`](http://html5doctor.com/html5-custom-data-attributes/)`data-role="listview"` usnadňuje klepnutí na velké položky seznamu. To znamená, že hotový kód vypadá takto:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

Aktualizujte si mobilní prohlížeč. Aktualizované zobrazení vypadá takto:

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

I když se mobilní zobrazení zlepšilo, je obtížné přejít na dlouhý seznam mluvčích. Chcete-li tento problém vyřešit, přidejte do značky `<ul>` atribut `data-filter` a nastavte jej na `true`. Následující kód ukazuje `ul` označení.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

Následující obrázek znázorňuje pole vyhledávací filtr v horní části stránky, které je výsledkem atributu `data-filter`.

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

Při zadávání jednotlivých písmen do vyhledávacího pole se v okně pro hledání zobrazí mobilní filtry, jak je znázorněno na obrázku níže.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>Vylepšení seznamu značek

Podobně jako u výchozího zobrazení *mluvčích* je zobrazení *značek* čitelné, ale odkazy jsou malé a obtížné klepnout na mobilní zařízení. V této části opravíte zobrazení *značek* stejným způsobem jako v zobrazení *mluvčích* .

Odeberte &quot;skryjte&quot; příponu souboru *Views\Home\AllTags.Mobile.cshtml.Hide* , aby se název *Views\Home\AllTags.Mobile.cshtml*. Otevřete přejmenovaný soubor a odeberte `<h2>` element.

Do značky `<ul>` přidejte atributy `data-role` a `data-filter`, jak je znázorněno zde:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

Následující obrázek ukazuje filtrování stránky na `J`písmen.

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>Vylepšení seznamu kalendářních dat

Můžete vylepšit zobrazení *dat* , jako jste vylepšili *reproduktory* a zobrazení *značek* , aby bylo možné je snadněji používat na mobilním zařízení.

Zkopírujte soubor *Views\Home\AllDates.cshtml* do *Views\Home\AllDates.Mobile.cshtml*. Otevřete nový soubor a odeberte `<h2>` element.

Přidejte `data-role="listview"` do značky `<ul>`, například takto:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

Následující obrázek ukazuje, jak stránka **data** vypadá jako atribut `data-role` na místě.

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Obsah souboru *Views\Home\AllDates.Mobile.cshtml* nahraďte následujícím kódem:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

Tento kód seskupuje všechny relace podle dnů. Vytvoří oddělovač seznamu pro každý nový den a zobrazí všechny relace pro každý den v rámci oddělovače. Jak to vypadá, když tento kód spouští:

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>Vylepšení zobrazení relace

V této části vytvoříte zobrazení relací specifických pro mobilní zařízení. Změny, které provedeme, budou složitější než v jiných zobrazeních, která jsme vytvořili.

V mobilním prohlížeči klepněte na tlačítko **mluvčího** a potom do vyhledávacího pole zadejte `Sc`.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

Klepněte na odkaz **Scott Hanselman** .

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

Jak vidíte, zobrazení je obtížné přečíst v mobilním prohlížeči. Sloupec data je těžké přečíst a sloupec značky je mimo zobrazení. Pokud to chcete opravit, zkopírujte *Views\Home\SessionsTable.cshtml* do *Views\Home\SessionsTable.Mobile.cshtml*a potom nahraďte obsah souboru následujícím kódem:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

Kód odstraní sloupce místnost a značky a zformátuje název, mluvčí a datum svisle tak, aby byly všechny tyto informace čitelné v mobilním prohlížeči. Obrázek níže odráží změny kódu.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>Vylepšení zobrazení SessionByCode

Nakonec vytvoříte zobrazení *SessionByCode* pro mobilní zařízení. V mobilním prohlížeči klepněte na tlačítko **mluvčího** a potom do vyhledávacího pole zadejte `Sc`.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

Klepněte na odkaz **Scott Hanselman** . Zobrazí se relace Scott Hanselman.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

Vyberte si **Přehled odkazu na lásku v MS web Stack** .

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

Výchozí zobrazení desktopu je v pořádku, ale můžete ho vylepšit.

Zkopírujte *Views\Home\SessionByCode.cshtml* do *Views\Home\SessionByCode.Mobile.cshtml* a nahraďte obsah souboru *Views\Home\SessionByCode.Mobile.cshtml* následujícím kódem:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

Nový kód používá atribut `data-role` ke zlepšení rozložení zobrazení.

Aktualizujte si mobilní prohlížeč. Následující obrázek odráží změny kódu, které jste právě provedli:

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup a revize

Tento kurz přináší nové mobilní funkce ASP.NET MVC 4 Developer Preview. K mobilním funkcím patří:

- Možnost přepsat rozložení, zobrazení a částečná zobrazení globálně i pro jednotlivá zobrazení.
- Kontrola rozložení a vynucení částečného přepsání pomocí vlastnosti `RequireConsistentDisplayMode`.
- Widget pro přepínač zobrazení pro mobilní zobrazení, než se dá zobrazit také v zobrazeních plochy.
- Podpora pro podporu konkrétních prohlížečů, jako je například prohlížeč iPhone.

## <a name="see-also"></a>Viz také

- [mobilní web jQuery](http://jquerymobile.com) .
- [Přehled nástroje jQuery Mobile](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [Osvědčené postupy pro mobilní webové aplikace s doporučením W3C](http://www.w3.org/TR/mwabp/)
- [Doporučení společnosti W3C pro dotazy na média](http://www.w3.org/TR/css3-mediaqueries/)
