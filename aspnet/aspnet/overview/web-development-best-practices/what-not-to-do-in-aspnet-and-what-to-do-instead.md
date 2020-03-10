---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: Co dělat v ASP.NET a co dělat místo | Microsoft Docs
author: Rick-Anderson
description: Toto téma popisuje několik běžných chyb, které uživatelé provedou v rámci ASP.NET webových projektů. Poskytuje doporučení k tomu, abyste se vyhnuli těmto commo...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616989"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="5442b-104">Co nedělat v ASP.NET a jak to udělat správně</span><span class="sxs-lookup"><span data-stu-id="5442b-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="5442b-105">Toto téma popisuje několik běžných chyb, které uživatelé provedou v rámci ASP.NET webových projektů.</span><span class="sxs-lookup"><span data-stu-id="5442b-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="5442b-106">Poskytuje doporučení k tomu, co byste měli udělat, abyste se vyhnuli těmto běžným chybám.</span><span class="sxs-lookup"><span data-stu-id="5442b-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="5442b-107">Je založen na [prezentaci](http://vimeo.com/68390507) , kterou **Damian Edwards** na konferenci norských vývojářů.</span><span class="sxs-lookup"><span data-stu-id="5442b-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="5442b-108">Právní omezení</span><span class="sxs-lookup"><span data-stu-id="5442b-108">Disclaimer</span></span>

<span data-ttu-id="5442b-109">Toto téma není určené jako kompletní příručka, která zajišťuje zabezpečení a efektivitu aplikace.</span><span class="sxs-lookup"><span data-stu-id="5442b-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="5442b-110">Stále je nutné dodržovat osvědčené postupy pro zabezpečení a výkon, které nejsou popsanými v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="5442b-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="5442b-111">Navrhuje jenom to, jak se vyhnout běžným chybám souvisejícím s třídami a procesy .NET.</span><span class="sxs-lookup"><span data-stu-id="5442b-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="5442b-112">Přehled</span><span class="sxs-lookup"><span data-stu-id="5442b-112">Overview</span></span>

<span data-ttu-id="5442b-113">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="5442b-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="5442b-114">Dodržování standardů</span><span class="sxs-lookup"><span data-stu-id="5442b-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="5442b-115">Adaptéry ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="5442b-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="5442b-116">Vlastnosti stylu u ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="5442b-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="5442b-117">Zpětná volání stránek a ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="5442b-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="5442b-118">Detekce schopností prohlížeče</span><span class="sxs-lookup"><span data-stu-id="5442b-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="5442b-119">Zabezpečení</span><span class="sxs-lookup"><span data-stu-id="5442b-119">Security</span></span>](#security)

    - [<span data-ttu-id="5442b-120">Žádost o ověření</span><span class="sxs-lookup"><span data-stu-id="5442b-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="5442b-121">Ověřování a relace bez souborů cookie</span><span class="sxs-lookup"><span data-stu-id="5442b-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="5442b-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="5442b-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="5442b-123">Střední důvěryhodnost</span><span class="sxs-lookup"><span data-stu-id="5442b-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="5442b-124">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="5442b-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="5442b-125">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="5442b-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="5442b-126">Spolehlivost a výkon</span><span class="sxs-lookup"><span data-stu-id="5442b-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="5442b-127">PreSendRequestHeaders a PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="5442b-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="5442b-128">Asynchronní události stránky s webovými formuláři</span><span class="sxs-lookup"><span data-stu-id="5442b-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="5442b-129">Práce s požárem a zapomenoutm</span><span class="sxs-lookup"><span data-stu-id="5442b-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="5442b-130">Tělo entity žádosti</span><span class="sxs-lookup"><span data-stu-id="5442b-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="5442b-131">Response. Redirect a Response. end</span><span class="sxs-lookup"><span data-stu-id="5442b-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="5442b-132">EnableViewState a ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="5442b-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="5442b-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="5442b-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="5442b-134">Dlouho běžící požadavky (> 110 sekund)</span><span class="sxs-lookup"><span data-stu-id="5442b-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="5442b-135">Dodržování standardů</span><span class="sxs-lookup"><span data-stu-id="5442b-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="5442b-136">Adaptéry ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="5442b-136">Control adapters</span></span>

<span data-ttu-id="5442b-137">Doporučení: Ukončete používání adaptérů ovládacích prvků pro adaptivní vykreslování a místo toho používejte dotazy na média CSS a standardy HTML kompatibilní s normami.</span><span class="sxs-lookup"><span data-stu-id="5442b-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="5442b-138">Ovládací prvky adaptérů byly představeny v rozhraní .NET 2,0 pro vykreslování kódu prezentace, který byl přizpůsoben pro různá zařízení a prostředí.</span><span class="sxs-lookup"><span data-stu-id="5442b-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="5442b-139">Nyní lze adaptivní vykreslování provést pomocí šablon stylů CSS a HTML.</span><span class="sxs-lookup"><span data-stu-id="5442b-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="5442b-140">Měli byste ukončit používání adaptérů ovládacích prvků a převést všechny existující adaptéry na šablony stylů CSS a HTML.</span><span class="sxs-lookup"><span data-stu-id="5442b-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="5442b-141">Další informace najdete v tématech [dotazy na média](http://www.w3.org/TR/css3-mediaqueries/) a [Postupy: Přidání mobilních stránek do webových formulářů ASP.NET/aplikace MVC](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="5442b-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="5442b-142">Vlastnosti stylu u ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="5442b-142">Style properties on controls</span></span>

<span data-ttu-id="5442b-143">Doporučení: zastaví nastavení hodnot stylu v označení ovládacího prvku a místo toho nastaví hodnoty formátování v šablonách stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="5442b-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="5442b-144">Ovládací prvky webového serveru obsahují desítky vlastností, které lze použít k nastavení vlastností vloženého stylu.</span><span class="sxs-lookup"><span data-stu-id="5442b-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="5442b-145">Například vlastnost ForeColor nastavuje barvu textu ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="5442b-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="5442b-146">Stejný efekt můžete dosáhnout efektivněji prostřednictvím šablon stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="5442b-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="5442b-147">Šablony stylů umožňují centralizovat hodnoty stylu a vyhnout se nastavování těchto hodnot v celé aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5442b-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="5442b-148">Následující příklad ukazuje třídu šablony stylů CSS, která nastaví text na červenou.</span><span class="sxs-lookup"><span data-stu-id="5442b-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="5442b-149">Následující příklad ukazuje, jak dynamicky použít třídu CSS.</span><span class="sxs-lookup"><span data-stu-id="5442b-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="5442b-150">Zpětná volání stránek a ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="5442b-150">Page and control callbacks</span></span>

<span data-ttu-id="5442b-151">Doporučení: Ukončete používání zpětných volání stránek a ovládacích prvků a místo toho použijte některý z následujících postupů: AJAX, UpdatePanel, MVC Methods, Web API nebo Signal.</span><span class="sxs-lookup"><span data-stu-id="5442b-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="5442b-152">V dřívějších verzích ASP.NET metody zpětného volání stránky a ovládacího prvku umožňují aktualizovat část webové stránky bez aktualizace celé stránky.</span><span class="sxs-lookup"><span data-stu-id="5442b-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="5442b-153">Teď můžete provádět aktualizace na částečnou stránku prostřednictvím [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [webového rozhraní API](../../../web-api/index.md) nebo [signalizace](../../../signalr/index.md).</span><span class="sxs-lookup"><span data-stu-id="5442b-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="5442b-154">Metody zpětného volání byste měli přestat používat, protože mohou způsobovat problémy s popisnými adresami URL a směrováním.</span><span class="sxs-lookup"><span data-stu-id="5442b-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="5442b-155">Ve výchozím nastavení ovládací prvky nepovolují metody zpětného volání, ale pokud jste tuto funkci povolili v ovládacím prvku, měli byste je zakázat.</span><span class="sxs-lookup"><span data-stu-id="5442b-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="5442b-156">Detekce schopností prohlížeče</span><span class="sxs-lookup"><span data-stu-id="5442b-156">Browser capability detection</span></span>

<span data-ttu-id="5442b-157">Doporučení: Zastavte používání statického zjišťování schopností prohlížeče a místo toho použijte detekci dynamické funkce.</span><span class="sxs-lookup"><span data-stu-id="5442b-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="5442b-158">V dřívějších verzích ASP.NET byly podporované funkce pro každý prohlížeč uloženy v souboru XML.</span><span class="sxs-lookup"><span data-stu-id="5442b-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="5442b-159">Rozpoznání podpory funkcí prostřednictvím statického vyhledávání není nejlepší přístup.</span><span class="sxs-lookup"><span data-stu-id="5442b-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="5442b-160">Nyní můžete pomocí rozhraní pro detekci funkcí, jako je například [modernizr](http://modernizr.com/), dynamicky zjišťovat podporované funkce prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="5442b-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="5442b-161">Detekce funkcí Určuje podporu tím, že se pokusí použít metodu nebo vlastnost a pak zkontroluje, jestli prohlížeč vyrobí požadovaný výsledek.</span><span class="sxs-lookup"><span data-stu-id="5442b-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="5442b-162">Ve výchozím nastavení je modernizr součástí šablon webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="5442b-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="5442b-163">Zabezpečení</span><span class="sxs-lookup"><span data-stu-id="5442b-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="5442b-164">Žádost o ověření</span><span class="sxs-lookup"><span data-stu-id="5442b-164">Request validation</span></span>

<span data-ttu-id="5442b-165">Doporučení: ověření vstupu uživatele a kódování výstupu pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="5442b-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="5442b-166">Ověření žádosti je funkce ASP.NET, která kontroluje každou žádost a zastaví žádost, pokud se najde zjištěná hrozba.</span><span class="sxs-lookup"><span data-stu-id="5442b-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="5442b-167">Nezáleží na žádosti o ověření pro zabezpečení vaší aplikace proti útokům prostřednictvím skriptování napříč weby.</span><span class="sxs-lookup"><span data-stu-id="5442b-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="5442b-168">Místo toho ověřte všechny vstupy uživatelů a zakódovat výstup.</span><span class="sxs-lookup"><span data-stu-id="5442b-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="5442b-169">V některých omezených případech můžete použít regulární výrazy k ověření vstupu, ale ve složitějších případech byste měli ověřit vstup uživatele pomocí tříd .NET, které určují, jestli hodnota odpovídá povoleným hodnotám.</span><span class="sxs-lookup"><span data-stu-id="5442b-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="5442b-170">Následující příklad ukazuje, jak použít statickou metodu v třídě URI k určení, zda je identifikátor URI, který je poskytnut uživatelem, platný.</span><span class="sxs-lookup"><span data-stu-id="5442b-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="5442b-171">Chcete-li ale dostatečně ověřit identifikátor URI, měli byste také zkontrolovat, zda určuje `http` nebo `https`.</span><span class="sxs-lookup"><span data-stu-id="5442b-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="5442b-172">Následující příklad používá metody instance k ověření, že identifikátor URI je platný.</span><span class="sxs-lookup"><span data-stu-id="5442b-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="5442b-173">Před vykreslením vstupu uživatele jako HTML nebo vložením vstupu uživatele do dotazu SQL zakódovat hodnoty, abyste zajistili, že není zahrnutý škodlivý kód.</span><span class="sxs-lookup"><span data-stu-id="5442b-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="5442b-174">Můžete kódovat hodnotu v kódu HTML pomocí syntaxe &lt;%:%&gt;, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="5442b-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="5442b-175">Nebo v syntaxe Razor můžete kódovat HTML ve formátu @, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="5442b-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="5442b-176">Následující příklad ukazuje, jak HTML kódovat hodnotu v kódu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="5442b-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="5442b-177">Pro bezpečné kódování hodnoty pro příkazy SQL použijte parametry příkazu, jako je například [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="5442b-178">Ověřování a relace bez souborů cookie</span><span class="sxs-lookup"><span data-stu-id="5442b-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="5442b-179">Doporučení: vyžadovat soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="5442b-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="5442b-180">Předávání ověřovacích informací v řetězci dotazu není zabezpečené.</span><span class="sxs-lookup"><span data-stu-id="5442b-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="5442b-181">Proto vyžaduje soubory cookie, pokud vaše aplikace zahrnuje ověřování.</span><span class="sxs-lookup"><span data-stu-id="5442b-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="5442b-182">Pokud soubor cookie ukládá citlivé informace, zvažte vyžadování protokolu SSL pro soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="5442b-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="5442b-183">Následující příklad ukazuje, jak zadat v souboru Web. config, který ověřování pomocí formulářů vyžaduje soubor cookie přenesený přes protokol SSL.</span><span class="sxs-lookup"><span data-stu-id="5442b-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="5442b-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="5442b-184">EnableViewStateMac</span></span>

<span data-ttu-id="5442b-185">Doporučení: nikdy Nenastaveno na false.</span><span class="sxs-lookup"><span data-stu-id="5442b-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="5442b-186">Ve výchozím nastavení je EnableViewStateMac nastaveno na hodnotu true (pravda).</span><span class="sxs-lookup"><span data-stu-id="5442b-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="5442b-187">I v případě, že vaše aplikace nepoužívá stav zobrazení, nenastavujte EnableViewStateMac na hodnotu false.</span><span class="sxs-lookup"><span data-stu-id="5442b-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="5442b-188">Nastavením hodnoty false dojde k tomu, že vaše aplikace bude zranitelná pro skriptování mezi weby.</span><span class="sxs-lookup"><span data-stu-id="5442b-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="5442b-189">Od ASP.NET 4.5.2 modul runtime vynutil **enableViewStateMAC = true**.</span><span class="sxs-lookup"><span data-stu-id="5442b-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="5442b-190">I v případě, že nastavíte hodnotu false, modul runtime tuto hodnotu ignoruje a pokračuje s hodnotou nastavenou na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="5442b-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="5442b-191">Další informace najdete v tématu [ASP.NET 4.5.2 a enableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="5442b-192">Následující příklad ukazuje, jak nastavit EnableViewStateMac na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="5442b-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="5442b-193">Tuto hodnotu nemusíte ve skutečnosti nastavovat na hodnotu true, protože je ve výchozím nastavení true.</span><span class="sxs-lookup"><span data-stu-id="5442b-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="5442b-194">Pokud jste ale na libovolné stránce aplikace nastavili na false hodnotu false, musíte tuto hodnotu hned opravit.</span><span class="sxs-lookup"><span data-stu-id="5442b-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="5442b-195">Střední důvěryhodnost</span><span class="sxs-lookup"><span data-stu-id="5442b-195">Medium trust</span></span>

<span data-ttu-id="5442b-196">Doporučení: nezávisle na středním vztahu důvěryhodnosti (nebo jakékoli jiné úrovni důvěryhodnosti) jako hranice zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="5442b-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="5442b-197">Při částečném vztahu důvěryhodnosti není vaše aplikace dostatečně chráněná a neměla by se používat.</span><span class="sxs-lookup"><span data-stu-id="5442b-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="5442b-198">Místo toho použijte úplný vztah důvěryhodnosti a izolujte nedůvěryhodné aplikace v samostatných fondech aplikací.</span><span class="sxs-lookup"><span data-stu-id="5442b-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="5442b-199">Spusťte také každý fond aplikací v rámci jedinečné identity.</span><span class="sxs-lookup"><span data-stu-id="5442b-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="5442b-200">Další informace najdete v tématu [ASP.NET s částečným vztahem důvěryhodnosti nezaručuje izolaci aplikace](https://support.microsoft.com/kb/2698981).</span><span class="sxs-lookup"><span data-stu-id="5442b-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="5442b-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="5442b-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="5442b-202">Doporučení: Nepovolujte nastavení zabezpečení ve &lt;appSettings&gt; elementu.</span><span class="sxs-lookup"><span data-stu-id="5442b-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="5442b-203">Element appSettings obsahuje mnoho hodnot, které jsou požadovány pro aktualizace zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="5442b-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="5442b-204">Tyto hodnoty byste neměli měnit ani zakazovat.</span><span class="sxs-lookup"><span data-stu-id="5442b-204">You should not change or disable these values.</span></span> <span data-ttu-id="5442b-205">Pokud je nutné tyto hodnoty při nasazení aktualizace zakázat, ihned po dokončení nasazení znovu povolte.</span><span class="sxs-lookup"><span data-stu-id="5442b-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="5442b-206">Podrobnosti naleznete v tématu [ASP.NET appSettings element](https://msdn.microsoft.com/library/hh975440.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="5442b-207">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="5442b-207">UrlPathEncode</span></span>

<span data-ttu-id="5442b-208">Doporučení: místo toho použijte [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) .</span><span class="sxs-lookup"><span data-stu-id="5442b-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="5442b-209">Metoda UrlPathEncode byla přidána do .NET Framework za účelem vyřešení velmi specifického problému s kompatibilitou prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="5442b-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="5442b-210">Nemá dostatečně zakódovat adresu URL a nechrání aplikaci před skriptováním mezi weby.</span><span class="sxs-lookup"><span data-stu-id="5442b-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="5442b-211">Nikdy ji nepoužívejte ve své aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5442b-211">You should never use it in your application.</span></span> <span data-ttu-id="5442b-212">Místo toho použijte [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="5442b-213">Následující příklad ukazuje, jak předat kódované adresy URL jako parametr řetězce dotazu pro ovládací prvek hypertextového odkazu.</span><span class="sxs-lookup"><span data-stu-id="5442b-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="5442b-214">Spolehlivost a výkon</span><span class="sxs-lookup"><span data-stu-id="5442b-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="5442b-215">PreSendRequestHeaders a PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="5442b-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="5442b-216">Doporučení: Nepoužívejte tyto události se spravovanými moduly.</span><span class="sxs-lookup"><span data-stu-id="5442b-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="5442b-217">Místo toho napíšete nativní modul IIS, který provede požadovanou úlohu.</span><span class="sxs-lookup"><span data-stu-id="5442b-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="5442b-218">Viz [vytváření modulů HTTP v nativním kódu](https://msdn.microsoft.com/library/ms693629.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="5442b-219">Události [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) a [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) můžete použít s nativními moduly IIS.</span><span class="sxs-lookup"><span data-stu-id="5442b-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="5442b-220">Nepoužívejte `PreSendRequestHeaders` a `PreSendRequestContent` se spravovanými moduly, které implementují `IHttpModule`.</span><span class="sxs-lookup"><span data-stu-id="5442b-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="5442b-221">Nastavení těchto vlastností může způsobit problémy s asynchronními požadavky.</span><span class="sxs-lookup"><span data-stu-id="5442b-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="5442b-222">Kombinace požadavků na směrování (ARR) a WebSockets aplikace může vést k narušení přístupu, které by mohly způsobit selhání W3wp.</span><span class="sxs-lookup"><span data-stu-id="5442b-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="5442b-223">Například iiscore! W3_CONTEXT_BASE:: GetIsLastNotification + 68 v souboru iiscore. dll způsobil výjimku narušení přístupu (0xC0000005).</span><span class="sxs-lookup"><span data-stu-id="5442b-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="5442b-224">Asynchronní události stránky s webovými formuláři</span><span class="sxs-lookup"><span data-stu-id="5442b-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="5442b-225">Doporučení: ve webových formulářích Vyhněte se zápisu asynchronních metod void pro události životního cyklu stránky a místo toho použijte [Page. RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) pro asynchronní kód.</span><span class="sxs-lookup"><span data-stu-id="5442b-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="5442b-226">Když označíte událost stránky pomocí **Async** a **void**, nemůžete určit, kdy byl asynchronní kód dokončen.</span><span class="sxs-lookup"><span data-stu-id="5442b-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="5442b-227">Místo toho použijte Page. RegisterAsyncTask ke spuštění asynchronního kódu způsobem, který umožňuje sledovat jeho dokončení.</span><span class="sxs-lookup"><span data-stu-id="5442b-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="5442b-228">Následující příklad ukazuje obslužnou rutinu kliknutí na tlačítko, která obsahuje asynchronní kód.</span><span class="sxs-lookup"><span data-stu-id="5442b-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="5442b-229">Tento příklad zahrnuje asynchronní čtení řetězcové hodnoty, která je poskytována pouze jako zjednodušený příklad asynchronní úlohy a nikoli jako doporučený postup.</span><span class="sxs-lookup"><span data-stu-id="5442b-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="5442b-230">Používáte-li asynchronní úlohy, nastavte cílové rozhraní HTTP runtime na 4,5 (nebo novější) v souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="5442b-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="5442b-231">Nastavení cílové architektury na 4,5 zapne nový kontext synchronizace, který byl přidán v rozhraní .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="5442b-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="5442b-232">Tato hodnota je nastavena ve výchozím nastavení v nových projektech v aplikaci Visual Studio, ale není nastavena, pokud pracujete s existujícím projektem.</span><span class="sxs-lookup"><span data-stu-id="5442b-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="5442b-233">Práce s požárem a zapomenoutm</span><span class="sxs-lookup"><span data-stu-id="5442b-233">Fire-and-forget work</span></span>

<span data-ttu-id="5442b-234">Doporučení: při zpracování žádosti v rámci ASP.NET se vyhnete spouštění práce s požárem a nedovolenými událostmi (například volání metody fondu vláken. QueueUserWorkItem nebo vytvoření časovače, který opakovaně volá delegáta).</span><span class="sxs-lookup"><span data-stu-id="5442b-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="5442b-235">Pokud vaše aplikace funguje s požárem a zapomenutím, která běží v rámci ASP.NET, může se aplikace dostat do synchronizace. Doména aplikace může být kdykoli zničena, což znamená, že váš probíhající proces již nemusí odpovídat aktuálnímu stavu aplikace.</span><span class="sxs-lookup"><span data-stu-id="5442b-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="5442b-236">Tento typ práce byste měli přesunout mimo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5442b-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="5442b-237">K provedení průběžné práce můžete použít webové úlohy, služby systému Windows nebo roli pracovního procesu v Azure a spustit tento kód z jiného procesu.</span><span class="sxs-lookup"><span data-stu-id="5442b-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="5442b-238">Pokud musíte tuto práci provést v rámci ASP.NET, můžete přidat balíček NuGet s názvem [webbackground](http://www.nuget.org/packages/webbackgrounder) a spustit kód.</span><span class="sxs-lookup"><span data-stu-id="5442b-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="5442b-239">Tělo entity žádosti</span><span class="sxs-lookup"><span data-stu-id="5442b-239">Request entity body</span></span>

<span data-ttu-id="5442b-240">Doporučení: Vyhněte se čtení požadavku. Form nebo Request. InputStream před událostí Execute obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="5442b-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="5442b-241">Nejdříve byste měli číst z Request. Form nebo Request. InputStream během události Execute obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="5442b-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="5442b-242">V MVC je kontroler obslužná rutina a událost Execute při spuštění metody Action.</span><span class="sxs-lookup"><span data-stu-id="5442b-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="5442b-243">Ve webových formulářích je stránka obslužná rutina a událost Execute, když je aktivována událost Page. init.</span><span class="sxs-lookup"><span data-stu-id="5442b-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="5442b-244">Pokud si přečtete tělo entity požadavku dříve, než je událost Execute, budete mít vliv na zpracování žádosti.</span><span class="sxs-lookup"><span data-stu-id="5442b-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="5442b-245">Pokud potřebujete číst tělo entity požadavku před událostí Execute, použijte buď [Request. GetBufferlessInputStream není](https://msdn.microsoft.com/library/ff406798.aspx) , nebo [Request. GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="5442b-246">Pokud používáte GetBufferlessInputStream není, získáte z požadavku nezpracovaný datový proud a Předpokládejme zodpovědnost za zpracování celého požadavku.</span><span class="sxs-lookup"><span data-stu-id="5442b-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="5442b-247">Po volání GetBufferlessInputStream není nejsou požadavky Request. Form a Request. InputStream k dispozici, protože nebyly vyplněny ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5442b-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="5442b-248">Když použijete GetBufferedInputStream, dostanete kopii datového proudu z požadavku.</span><span class="sxs-lookup"><span data-stu-id="5442b-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="5442b-249">Request. Form a Request. InputStream jsou stále k dispozici později v žádosti, protože ASP.NET naplní další kopii.</span><span class="sxs-lookup"><span data-stu-id="5442b-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="5442b-250">Response. Redirect a Response. end</span><span class="sxs-lookup"><span data-stu-id="5442b-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="5442b-251">Doporučení: Pamatujte na rozdíly ve způsobu zpracování vlákna po volání metody [Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="5442b-252">Metoda [Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) volá metodu Response. end.</span><span class="sxs-lookup"><span data-stu-id="5442b-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="5442b-253">V synchronním procesu volání Request. Redirect způsobí okamžité přerušení aktuálního vlákna.</span><span class="sxs-lookup"><span data-stu-id="5442b-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="5442b-254">Nicméně v asynchronním procesu volání metody Response. Redirect neukončí aktuální vlákno, takže provádění kódu pro požadavek bude pokračovat.</span><span class="sxs-lookup"><span data-stu-id="5442b-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="5442b-255">V asynchronním procesu je nutné vrátit úlohu z metody pro zastavení provádění kódu.</span><span class="sxs-lookup"><span data-stu-id="5442b-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="5442b-256">V projektu MVC byste neměli volat Response. Redirect.</span><span class="sxs-lookup"><span data-stu-id="5442b-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="5442b-257">Místo toho vraťte RedirectResult.</span><span class="sxs-lookup"><span data-stu-id="5442b-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="5442b-258">EnableViewState a ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="5442b-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="5442b-259">Doporučení: použijte ViewStateMode namísto EnableViewState k poskytnutí podrobné kontroly nad tím, které ovládací prvky používají stav zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5442b-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="5442b-260">Nastavíte-li atribut EnableViewState na hodnotu false v direktivě stránky, je stav zobrazení zakázán pro všechny ovládací prvky na stránce a nelze jej povolit.</span><span class="sxs-lookup"><span data-stu-id="5442b-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="5442b-261">Pokud chcete povolit stav zobrazení pouze pro určité ovládací prvky na stránce, nastavte ViewStateMode na hodnotu zakázáno pro stránku.</span><span class="sxs-lookup"><span data-stu-id="5442b-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="5442b-262">Potom nastavte ViewStateMode na Enabled pouze ovládací prvky, které skutečně potřebují stav zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5442b-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="5442b-263">Když povolíte stav zobrazení jenom pro ovládací prvky, které ho potřebují, můžete zmenšit velikost stavu zobrazení webových stránek.</span><span class="sxs-lookup"><span data-stu-id="5442b-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="5442b-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="5442b-264">SqlMembershipProvider</span></span>

<span data-ttu-id="5442b-265">Doporučení: použijte univerzální poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="5442b-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="5442b-266">V aktuálních šablonách projektu byl SqlMembershipProvider nahrazen [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), který je k dispozici jako balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="5442b-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="5442b-267">Pokud používáte SqlMembershipProvider v projektu, který byl vytvořen pomocí starší verze šablon, měli byste přepnout na Universal Providers.</span><span class="sxs-lookup"><span data-stu-id="5442b-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="5442b-268">Univerzální poskytovatelé pracují se všemi databázemi, které jsou podporovány nástrojem Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="5442b-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="5442b-269">Další informace najdete v tématu [představujeme ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span><span class="sxs-lookup"><span data-stu-id="5442b-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="5442b-270">Dlouho běžící požadavky (> 110 sekund)</span><span class="sxs-lookup"><span data-stu-id="5442b-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="5442b-271">Doporučení: pro připojené klienty použijte [objekty WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) nebo [Signal](../../../signalr/index.md) a použijte asynchronní vstupně-výstupní operace.</span><span class="sxs-lookup"><span data-stu-id="5442b-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="5442b-272">Dlouhotrvající požadavky mohou způsobit nepředvídatelné výsledky a špatný výkon ve vaší webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5442b-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="5442b-273">Výchozí nastavení časového limitu pro požadavek je 110 sekund.</span><span class="sxs-lookup"><span data-stu-id="5442b-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="5442b-274">Pokud používáte stav relace s dlouho běžícím požadavkem, ASP.NET uvolní zámek objektu Session po 110 sekundách.</span><span class="sxs-lookup"><span data-stu-id="5442b-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="5442b-275">Vaše aplikace ale může být uprostřed operace s objektem relace, když se zámek uvolní a operace se nemusí dokončit úspěšně.</span><span class="sxs-lookup"><span data-stu-id="5442b-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="5442b-276">Pokud je druhá žádost od uživatele zablokovaná, zatímco je spuštěný první požadavek, druhý požadavek může získat přístup k objektu Session v nekonzistentním stavu.</span><span class="sxs-lookup"><span data-stu-id="5442b-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="5442b-277">Pokud vaše aplikace zahrnuje blokující (nebo synchronní) vstupně-výstupní operace, aplikace přestane reagovat.</span><span class="sxs-lookup"><span data-stu-id="5442b-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="5442b-278">Chcete-li zvýšit výkon, použijte asynchronní vstupně-výstupní operace v .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5442b-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="5442b-279">K připojení klientů k serveru taky použijte objekty WebSockets nebo Signal.</span><span class="sxs-lookup"><span data-stu-id="5442b-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="5442b-280">Tyto funkce jsou navržené tak, aby efektivně zpracovávala dlouhotrvající požadavky.</span><span class="sxs-lookup"><span data-stu-id="5442b-280">These features are designed to efficiently handle long-running requests.</span></span>
