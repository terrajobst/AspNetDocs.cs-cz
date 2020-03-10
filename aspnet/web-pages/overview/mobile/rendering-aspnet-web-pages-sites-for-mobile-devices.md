---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: Vykreslování webů ASP.NET Web Pages (Razor) pro mobilní zařízení | Microsoft Docs
author: Rick-Anderson
description: 'Tento článek popisuje, jak vytvářet stránky na webu ASP.NET Web Pages (Razor), který se bude na mobilních zařízeních správně vykreslovat. Co se naučíte: jak vás...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563565"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>Vykreslování webů ASP.NET Web Pages (Razor) pro mobilní zařízení

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje, jak vytvářet stránky na webu ASP.NET Web Pages (Razor), který se bude na mobilních zařízeních správně vykreslovat.
> 
> Naučíte se:
> 
> - Použití zásad vytváření názvů k určení toho, že stránka je navržená speciálně pro mobilní zařízení.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

Webové stránky ASP.NET umožňují vytvářet vlastní displeje pro vykreslování obsahu na mobilních nebo jiných zařízeních.

Nejjednodušší způsob, jak vytvořit stránku specifickou pro konkrétní zařízení na webu ASP.NET Web Pages, je použití vzoru pro pojmenovávání souborů, jako je tento: *filename. Mobile. cshtml*. Můžete vytvořit dvě verze stránky (například jeden s názvem *MyFile. cshtml* a jeden název *MyFile. Mobile. cshtml*). V době běhu, když mobilní zařízení požaduje *soubor MyFile. cshtml*, ASP.NET vykreslí obsah ze *soubor MyFile. Mobile. cshtml*. V opačném případě je *soubor MyFile. cshtml* vykreslen.

Následující příklad ukazuje, jak povolit mobilní vykreslování přidáním stránky obsahu pro mobilní zařízení. *Page1. cshtml* obsahuje obsah plus navigační panel. *Page1. Mobile. cshtml* obsahuje stejný obsah, ale nenechává postranní panel.

1. Na webu webové stránky ASP.NET vytvořte soubor s názvem *Page1. cshtml* a nahraďte aktuální obsah následujícím kódem.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. Vytvořte soubor s názvem *Page1. Mobile. cshtml* a nahraďte stávající obsah následujícím kódem. Všimněte si, že mobilní verze stránky vynechává navigační oddíl pro lepší vykreslování na menších obrazovkách.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. Spusťte desktopový prohlížeč a přejděte na *Page1. cshtml*. ![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. Spusťte mobilní prohlížeč (nebo emulátor mobilního zařízení) a přejděte na *Page1. cshtml*. (Všimněte si, že nezahrnujete *. Mobile.* jako součást adresy URL.) I když je požadavek na *Page1. cshtml*, ASP.NET vykresluje *Page1. Mobile. cshtml*.

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> Chcete-li testovat mobilní stránky, můžete použít simulátor mobilního zařízení, který běží na stolním počítači. Tento nástroj umožňuje testovat webové stránky, které by vypadaly na mobilních zařízeních (obvykle s mnohem menší oblastí zobrazení). Jedním z příkladů simulátoru je [doplněk přepínačů uživatelského agenta](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) pro Mozilla Firefox, který umožňuje emulovat různé mobilní prohlížeče z desktopové verze Firefox.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[Emulátor Windows Phone](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
