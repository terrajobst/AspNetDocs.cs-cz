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
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="45061-104">Vykreslování webů ASP.NET Web Pages (Razor) pro mobilní zařízení</span><span class="sxs-lookup"><span data-stu-id="45061-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="45061-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="45061-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="45061-106">Tento článek popisuje, jak vytvářet stránky na webu ASP.NET Web Pages (Razor), který se bude na mobilních zařízeních správně vykreslovat.</span><span class="sxs-lookup"><span data-stu-id="45061-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="45061-107">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="45061-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="45061-108">Použití zásad vytváření názvů k určení toho, že stránka je navržená speciálně pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="45061-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="45061-109">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="45061-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="45061-110">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="45061-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="45061-111">Tento kurz funguje také s ASP.NET webovými stránkami 2.</span><span class="sxs-lookup"><span data-stu-id="45061-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="45061-112">Webové stránky ASP.NET umožňují vytvářet vlastní displeje pro vykreslování obsahu na mobilních nebo jiných zařízeních.</span><span class="sxs-lookup"><span data-stu-id="45061-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="45061-113">Nejjednodušší způsob, jak vytvořit stránku specifickou pro konkrétní zařízení na webu ASP.NET Web Pages, je použití vzoru pro pojmenovávání souborů, jako je tento: *filename. Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="45061-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="45061-114">Můžete vytvořit dvě verze stránky (například jeden s názvem *MyFile. cshtml* a jeden název *MyFile. Mobile. cshtml*).</span><span class="sxs-lookup"><span data-stu-id="45061-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="45061-115">V době běhu, když mobilní zařízení požaduje *soubor MyFile. cshtml*, ASP.NET vykreslí obsah ze *soubor MyFile. Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="45061-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="45061-116">V opačném případě je *soubor MyFile. cshtml* vykreslen.</span><span class="sxs-lookup"><span data-stu-id="45061-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="45061-117">Následující příklad ukazuje, jak povolit mobilní vykreslování přidáním stránky obsahu pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="45061-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="45061-118">*Page1. cshtml* obsahuje obsah plus navigační panel.</span><span class="sxs-lookup"><span data-stu-id="45061-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="45061-119">*Page1. Mobile. cshtml* obsahuje stejný obsah, ale nenechává postranní panel.</span><span class="sxs-lookup"><span data-stu-id="45061-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="45061-120">Na webu webové stránky ASP.NET vytvořte soubor s názvem *Page1. cshtml* a nahraďte aktuální obsah následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="45061-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="45061-121">Vytvořte soubor s názvem *Page1. Mobile. cshtml* a nahraďte stávající obsah následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="45061-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="45061-122">Všimněte si, že mobilní verze stránky vynechává navigační oddíl pro lepší vykreslování na menších obrazovkách.</span><span class="sxs-lookup"><span data-stu-id="45061-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="45061-123">Spusťte desktopový prohlížeč a přejděte na *Page1. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="45061-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="45061-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="45061-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="45061-125">Spusťte mobilní prohlížeč (nebo emulátor mobilního zařízení) a přejděte na *Page1. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="45061-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="45061-126">(Všimněte si, že nezahrnujete *. Mobile.*</span><span class="sxs-lookup"><span data-stu-id="45061-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="45061-127">jako součást adresy URL.) I když je požadavek na *Page1. cshtml*, ASP.NET vykresluje *Page1. Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="45061-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="45061-129">Chcete-li testovat mobilní stránky, můžete použít simulátor mobilního zařízení, který běží na stolním počítači.</span><span class="sxs-lookup"><span data-stu-id="45061-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="45061-130">Tento nástroj umožňuje testovat webové stránky, které by vypadaly na mobilních zařízeních (obvykle s mnohem menší oblastí zobrazení).</span><span class="sxs-lookup"><span data-stu-id="45061-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="45061-131">Jedním z příkladů simulátoru je [doplněk přepínačů uživatelského agenta](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) pro Mozilla Firefox, který umožňuje emulovat různé mobilní prohlížeče z desktopové verze Firefox.</span><span class="sxs-lookup"><span data-stu-id="45061-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="45061-132">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="45061-132">Additional Resources</span></span>

<span data-ttu-id="45061-133">[Emulátor Windows Phone](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="45061-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
