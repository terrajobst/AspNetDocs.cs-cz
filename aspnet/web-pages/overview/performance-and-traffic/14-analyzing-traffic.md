---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: Sledování informací návštěvníka (analýza) pro web ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Až se vám váš web bude líbit, možná budete chtít analyzovat provoz vašeho webu.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525184"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>Sledování informací návštěvníka (analýza) pro web ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje, jak pomocí pomocníka přidat na stránky na webu ASP.NET Web Pages (Razor) Web Analytics.
> 
> Naučíte se:
> 
> - Jak odesílat informace o provozu vašeho webu do poskytovatele analýz
> 
> Jedná se o funkce ASP.NET programování, které jsou představené v článku:
> 
> - Pomocná rutina `Analytics`
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - Knihovna webových pomocníků ASP.NET (balíček NuGet)

Analýza je obecný termín pro technologie, které měří provoz na vašem webu, abyste mohli pochopit, jak uživatelé web používají. K dispozici je řada analytických služeb, včetně služeb Google, Yahoo, StatCounter a dalších.

Způsob analýzy funguje tak, že se zaregistrujete k účtu pomocí poskytovatele analýz, kde zaregistrujete lokalitu, kterou chcete sledovat. Poskytovatel vám pošle fragment kódu JavaScriptu, který obsahuje ID nebo sledovací kód pro váš účet. Přidáte fragment kódu jazyka JavaScript do webových stránek na webu, který chcete sledovat. (Fragment analýzy obvykle přidáte na stránku zápatí nebo rozložení nebo na jiný kód HTML, který se zobrazí na každé stránce webu.) Když uživatelé požadují stránku, která obsahuje jeden z těchto fragmentů kódu JavaScriptu, fragment kódu pošle informace o aktuální stránce poskytovateli Analytics, který zaznamenává různé podrobnosti o stránce.

Pokud si chcete prohlédnout statistiku lokality, přihlaste se na web poskytovatele analýz. Pak můžete zobrazit nejrůznější sestavy o webu, například:

- Počet zobrazení stránky pro jednotlivé stránky. Tím se dozvíte, kolik lidí web navštěvuje a které stránky na webu jsou nejoblíbenější.
- Jak dlouho tráví lidé na konkrétních stránkách. To vám může sdělit, jak vaše domovská stránka zachovává zájem lidí.
- Jaké weby byly na pracovišti předtím, než navštívily vaši lokalitu. To vám pomůže pochopit, jestli přenosy pocházejí z odkazů, hledání a tak dále.
- Když lidé navštíví web a jak dlouho se budou zabývat.
- Do kterých zemí vaše Návštěvníci patří.
- Jaké prohlížeče a operační systémy vaše návštěvníci používají.

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>Použití pomocníka k přidávání analýz na stránku

Webové stránky ASP.NET obsahují několik analytických pomocníků (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`a `Analytics.GetStatCounterHtml`), které usnadňují správu fragmentů JavaScriptu používaných pro analýzy. Místo toho, abyste zjistili, jak a kam vložit kód JavaScriptu, stačí přidat pomocníka na stránku. Jediné informace, které potřebujete zadat, jsou název vašeho účtu, ID nebo sledovací kód. (Pro StatCounter musíte také zadat několik dalších hodnot.)

V tomto postupu vytvoříte stránku rozložení, která používá pomocníka `GetGoogleHtml`. Pokud už máte účet s některým z dalších zprostředkovatelů analýz, můžete místo toho použít tento účet a v případě potřeby provádět drobné úpravy.

> [!NOTE]
> Při vytváření účtu Analytics zaregistrujete adresu URL webu, který chcete sledovat. Pokud testujete všechno v místním počítači, nebudete sledovat skutečný provoz (jediný provoz je vám), takže nebudete moct nahrávat a zobrazovat statistiku lokality. Tento postup ale ukazuje, jak přidat pomocníka Analytics na stránku. Při publikování webu bude živý web odesílat informace vašemu poskytovateli Analytics.

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.
2. Vytvořte účet s Google Analytics a zaznamenejte název účtu.
3. Vytvořte stránku rozložení s názvem *Analytics. cshtml* a přidejte následující kód:

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > Volání do pomocné rutiny `Analytics` je nutné umístit v těle webové stránky (před značku `</body>`). V opačném případě se skript nespustí v prohlížeči.

    Pokud používáte jiného poskytovatele analýz, použijte místo toho některého z následujících pomocníků:

    - (Yahoo) `@Analytics.GetYahooHtml("myaccount")`
    - (StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`
4. Nahraďte `myaccount` názvem účtu, ID nebo sledovacího kódu, který jste vytvořili v kroku 1.
5. Spusťte stránku v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .)
6. V prohlížeči zobrazte zdroj stránky. Zobrazí se vám vykreslený analytický kód:

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. Přihlaste se k webu Google Analytics a Projděte si statistiku vašeho webu. Pokud spouštíte stránku na živém webu, zobrazí se položka, která zaznamená návštěvu na stránce.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

- [Web Google Analytics](https://www.google.com/analytics/)
- [Web Yahoo! Web Analytics](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter lokalita](http://statcounter.com/)
