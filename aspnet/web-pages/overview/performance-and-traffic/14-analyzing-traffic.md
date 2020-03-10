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
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="efc1a-103">Sledování informací návštěvníka (analýza) pro web ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="efc1a-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="efc1a-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="efc1a-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="efc1a-105">Tento článek popisuje, jak pomocí pomocníka přidat na stránky na webu ASP.NET Web Pages (Razor) Web Analytics.</span><span class="sxs-lookup"><span data-stu-id="efc1a-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="efc1a-106">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="efc1a-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="efc1a-107">Jak odesílat informace o provozu vašeho webu do poskytovatele analýz</span><span class="sxs-lookup"><span data-stu-id="efc1a-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="efc1a-108">Jedná se o funkce ASP.NET programování, které jsou představené v článku:</span><span class="sxs-lookup"><span data-stu-id="efc1a-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="efc1a-109">Pomocná rutina `Analytics`</span><span class="sxs-lookup"><span data-stu-id="efc1a-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="efc1a-110">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="efc1a-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="efc1a-111">Webové stránky ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="efc1a-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="efc1a-112">Knihovna webových pomocníků ASP.NET (balíček NuGet)</span><span class="sxs-lookup"><span data-stu-id="efc1a-112">ASP.NET Web Helpers Library (NuGet package)</span></span>

<span data-ttu-id="efc1a-113">Analýza je obecný termín pro technologie, které měří provoz na vašem webu, abyste mohli pochopit, jak uživatelé web používají.</span><span class="sxs-lookup"><span data-stu-id="efc1a-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="efc1a-114">K dispozici je řada analytických služeb, včetně služeb Google, Yahoo, StatCounter a dalších.</span><span class="sxs-lookup"><span data-stu-id="efc1a-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="efc1a-115">Způsob analýzy funguje tak, že se zaregistrujete k účtu pomocí poskytovatele analýz, kde zaregistrujete lokalitu, kterou chcete sledovat. Poskytovatel vám pošle fragment kódu JavaScriptu, který obsahuje ID nebo sledovací kód pro váš účet.</span><span class="sxs-lookup"><span data-stu-id="efc1a-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="efc1a-116">Přidáte fragment kódu jazyka JavaScript do webových stránek na webu, který chcete sledovat. (Fragment analýzy obvykle přidáte na stránku zápatí nebo rozložení nebo na jiný kód HTML, který se zobrazí na každé stránce webu.) Když uživatelé požadují stránku, která obsahuje jeden z těchto fragmentů kódu JavaScriptu, fragment kódu pošle informace o aktuální stránce poskytovateli Analytics, který zaznamenává různé podrobnosti o stránce.</span><span class="sxs-lookup"><span data-stu-id="efc1a-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="efc1a-117">Pokud si chcete prohlédnout statistiku lokality, přihlaste se na web poskytovatele analýz.</span><span class="sxs-lookup"><span data-stu-id="efc1a-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="efc1a-118">Pak můžete zobrazit nejrůznější sestavy o webu, například:</span><span class="sxs-lookup"><span data-stu-id="efc1a-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="efc1a-119">Počet zobrazení stránky pro jednotlivé stránky.</span><span class="sxs-lookup"><span data-stu-id="efc1a-119">The number of page views for individual pages.</span></span> <span data-ttu-id="efc1a-120">Tím se dozvíte, kolik lidí web navštěvuje a které stránky na webu jsou nejoblíbenější.</span><span class="sxs-lookup"><span data-stu-id="efc1a-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="efc1a-121">Jak dlouho tráví lidé na konkrétních stránkách.</span><span class="sxs-lookup"><span data-stu-id="efc1a-121">How long people spend on specific pages.</span></span> <span data-ttu-id="efc1a-122">To vám může sdělit, jak vaše domovská stránka zachovává zájem lidí.</span><span class="sxs-lookup"><span data-stu-id="efc1a-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="efc1a-123">Jaké weby byly na pracovišti předtím, než navštívily vaši lokalitu.</span><span class="sxs-lookup"><span data-stu-id="efc1a-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="efc1a-124">To vám pomůže pochopit, jestli přenosy pocházejí z odkazů, hledání a tak dále.</span><span class="sxs-lookup"><span data-stu-id="efc1a-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="efc1a-125">Když lidé navštíví web a jak dlouho se budou zabývat.</span><span class="sxs-lookup"><span data-stu-id="efc1a-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="efc1a-126">Do kterých zemí vaše Návštěvníci patří.</span><span class="sxs-lookup"><span data-stu-id="efc1a-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="efc1a-127">Jaké prohlížeče a operační systémy vaše návštěvníci používají.</span><span class="sxs-lookup"><span data-stu-id="efc1a-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="efc1a-129">Použití pomocníka k přidávání analýz na stránku</span><span class="sxs-lookup"><span data-stu-id="efc1a-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="efc1a-130">Webové stránky ASP.NET obsahují několik analytických pomocníků (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`a `Analytics.GetStatCounterHtml`), které usnadňují správu fragmentů JavaScriptu používaných pro analýzy.</span><span class="sxs-lookup"><span data-stu-id="efc1a-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="efc1a-131">Místo toho, abyste zjistili, jak a kam vložit kód JavaScriptu, stačí přidat pomocníka na stránku.</span><span class="sxs-lookup"><span data-stu-id="efc1a-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="efc1a-132">Jediné informace, které potřebujete zadat, jsou název vašeho účtu, ID nebo sledovací kód.</span><span class="sxs-lookup"><span data-stu-id="efc1a-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="efc1a-133">(Pro StatCounter musíte také zadat několik dalších hodnot.)</span><span class="sxs-lookup"><span data-stu-id="efc1a-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="efc1a-134">V tomto postupu vytvoříte stránku rozložení, která používá pomocníka `GetGoogleHtml`.</span><span class="sxs-lookup"><span data-stu-id="efc1a-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="efc1a-135">Pokud už máte účet s některým z dalších zprostředkovatelů analýz, můžete místo toho použít tento účet a v případě potřeby provádět drobné úpravy.</span><span class="sxs-lookup"><span data-stu-id="efc1a-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="efc1a-136">Při vytváření účtu Analytics zaregistrujete adresu URL webu, který chcete sledovat.</span><span class="sxs-lookup"><span data-stu-id="efc1a-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="efc1a-137">Pokud testujete všechno v místním počítači, nebudete sledovat skutečný provoz (jediný provoz je vám), takže nebudete moct nahrávat a zobrazovat statistiku lokality.</span><span class="sxs-lookup"><span data-stu-id="efc1a-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="efc1a-138">Tento postup ale ukazuje, jak přidat pomocníka Analytics na stránku.</span><span class="sxs-lookup"><span data-stu-id="efc1a-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="efc1a-139">Při publikování webu bude živý web odesílat informace vašemu poskytovateli Analytics.</span><span class="sxs-lookup"><span data-stu-id="efc1a-139">When you publish your site, the live site will send information to your analytics provider.</span></span>

1. <span data-ttu-id="efc1a-140">Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.</span><span class="sxs-lookup"><span data-stu-id="efc1a-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="efc1a-141">Vytvořte účet s Google Analytics a zaznamenejte název účtu.</span><span class="sxs-lookup"><span data-stu-id="efc1a-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="efc1a-142">Vytvořte stránku rozložení s názvem *Analytics. cshtml* a přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="efc1a-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="efc1a-143">Volání do pomocné rutiny `Analytics` je nutné umístit v těle webové stránky (před značku `</body>`).</span><span class="sxs-lookup"><span data-stu-id="efc1a-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="efc1a-144">V opačném případě se skript nespustí v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="efc1a-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="efc1a-145">Pokud používáte jiného poskytovatele analýz, použijte místo toho některého z následujících pomocníků:</span><span class="sxs-lookup"><span data-stu-id="efc1a-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="efc1a-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="efc1a-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="efc1a-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="efc1a-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="efc1a-148">Nahraďte `myaccount` názvem účtu, ID nebo sledovacího kódu, který jste vytvořili v kroku 1.</span><span class="sxs-lookup"><span data-stu-id="efc1a-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="efc1a-149">Spusťte stránku v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="efc1a-149">Run the page in the browser.</span></span> <span data-ttu-id="efc1a-150">(Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .)</span><span class="sxs-lookup"><span data-stu-id="efc1a-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="efc1a-151">V prohlížeči zobrazte zdroj stránky.</span><span class="sxs-lookup"><span data-stu-id="efc1a-151">In the browser, view the page source.</span></span> <span data-ttu-id="efc1a-152">Zobrazí se vám vykreslený analytický kód:</span><span class="sxs-lookup"><span data-stu-id="efc1a-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="efc1a-153">Přihlaste se k webu Google Analytics a Projděte si statistiku vašeho webu.</span><span class="sxs-lookup"><span data-stu-id="efc1a-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="efc1a-154">Pokud spouštíte stránku na živém webu, zobrazí se položka, která zaznamená návštěvu na stránce.</span><span class="sxs-lookup"><span data-stu-id="efc1a-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="efc1a-155">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="efc1a-155">Additional Resources</span></span>

- [<span data-ttu-id="efc1a-156">Web Google Analytics</span><span class="sxs-lookup"><span data-stu-id="efc1a-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="efc1a-157">Web Yahoo! Web Analytics</span><span class="sxs-lookup"><span data-stu-id="efc1a-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="efc1a-158">StatCounter lokalita</span><span class="sxs-lookup"><span data-stu-id="efc1a-158">StatCounter site</span></span>](http://statcounter.com/)
