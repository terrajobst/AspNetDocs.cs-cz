---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: Profilování a ladění aplikace ASP.NET MVC pomocí nakoukněte | Microsoft Docs
author: Rick-Anderson
description: Nakoukněte je prosperující a rostoucí rodina Open Source balíčků NuGet, které poskytují podrobné informace o výkonu, ladění a diagnostických informacích pro ASP.NET a...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457658"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="4d1d4-103">Profil aplikace ASP.NET MVC a její ladění pomocí balíčku Glimpse</span><span class="sxs-lookup"><span data-stu-id="4d1d4-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>

<span data-ttu-id="4d1d4-104">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4d1d4-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="4d1d4-105">Nakoukněte je prosperující a rostoucí rodina Open Source balíčků NuGet, které poskytují podrobné informace o výkonu, ladění a diagnostikě pro aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="4d1d4-106">Je triviální pro instalaci, odlehčenou, extrémně rychlou a zobrazení klíčových metrik výkonu v dolní části každé stránky.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="4d1d4-107">Umožňuje přejít k podrobnostem aplikace v případě, že potřebujete zjistit, co se na serveru chystá.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="4d1d4-108">Nakoukněte poskytuje spoustu užitečných informací, které doporučujeme využít v rámci vašeho vývojového cyklu, včetně vašeho testovacího prostředí Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="4d1d4-109">Zatímco [Fiddler](http://www.telerik.com/fiddler) a [vývojové nástroje F-12](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) poskytují zobrazení na straně klienta, nakoukněte poskytuje podrobné zobrazení ze serveru.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="4d1d4-110">Tento kurz se zaměřuje na použití balíčků nakoukněte ASP.NET MVC a EF, ale k dispozici je spousta dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="4d1d4-111">Kde je to možné, připojte se k odpovídajícím [nakouknětem dokumentům](http://getglimpse.com/Docs/) , které můžu udržovat.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="4d1d4-112">Nakoukněte je open source projekt, takže můžete přispívat ke zdrojovému kódu a dokumentům.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>

- [<span data-ttu-id="4d1d4-113">Instalace nakoukněte</span><span class="sxs-lookup"><span data-stu-id="4d1d4-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="4d1d4-114">Povolit nakoukněte pro localhost</span><span class="sxs-lookup"><span data-stu-id="4d1d4-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="4d1d4-115">Karta Časová osa</span><span class="sxs-lookup"><span data-stu-id="4d1d4-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="4d1d4-116">Vazby modelu</span><span class="sxs-lookup"><span data-stu-id="4d1d4-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="4d1d4-117">Tras</span><span class="sxs-lookup"><span data-stu-id="4d1d4-117">Routes</span></span>](#route)
- [<span data-ttu-id="4d1d4-118">Používání nakoukněte v Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d4-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="4d1d4-119">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="4d1d4-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="4d1d4-120">Instalace nakoukněte</span><span class="sxs-lookup"><span data-stu-id="4d1d4-120">Installing Glimpse</span></span>

<span data-ttu-id="4d1d4-121">Nakoukněte můžete nainstalovat z konzoly Správce balíčků NuGet nebo z konzoly **Správa balíčků NuGet** .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="4d1d4-122">V této ukázce nainstalujete balíčky Mvc5 a EF6:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![instalace nakoukněte z NuGet DLG](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="4d1d4-124">Hledání *nakoukněte. EF*</span><span class="sxs-lookup"><span data-stu-id="4d1d4-124">Search for *Glimpse.EF*</span></span>

![Nakoukněte. EF z instalačního dialogu NuGet](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="4d1d4-126">Když vyberete **nainstalované balíčky**, uvidíte, že jsou nainstalované závislé moduly nakoukněte:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![Instalované balíčky nakoukněte z DLg](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="4d1d4-128">Následující příkazy instalují moduly nakoukněte MVC5 a EF6 z konzoly Správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="4d1d4-129">Povolit nakoukněte pro localhost</span><span class="sxs-lookup"><span data-stu-id="4d1d4-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="4d1d4-130">Přejděte na http://localhost:&lt;p. #&gt;/Glimpse.axd a klikněte na tlačítko <strong>zapnout nakoukněte</strong> .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![Stránka AXD nakoukněte](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="4d1d4-132">Pokud máte zobrazený panel Oblíbené položky, můžete přetáhnout nakoukněte tlačítka a přidat je jako Bookmarklets:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![IE s nakoukněte Bookmarklets](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="4d1d4-134">Teď můžete aplikaci Procházet a v dolní části stránky se zobrazí **zobrazení hlavice** (HUD).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![Stránka správce kontaktů s HUD](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="4d1d4-136">[Stránka NAKOUKNĚTE HUD](http://getglimpse.com/Docs/Heads-up-Display) detailuje informace o časování zobrazené výše.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="4d1d4-137">Nenáročné údaje o výkonu, které HUD zobrazí, vám může upozorňovat na problém okamžitě – předtím, než se dostanete ke zkušebnímu cyklu.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="4d1d4-138">Kliknutím na &quot;g&quot; v pravém dolním rohu se zobrazí panel nakoukněte:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![Panel nakoukněte](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="4d1d4-140">Na obrázku výše je vybrána [karta spuštění](http://getglimpse.com/Docs/Execution-Tab) , která zobrazuje časové údaje o akcích a filtrech v kanálu.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="4d1d4-141">V průběhu fáze 6 kanálu se můžete podívat na svůj [časovač filtru stop watch](http://www.nuget.org/packages/StopWatch/) .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="4d1d4-142">I když je časově náročný časovač schopen poskytnout užitečná data o profilech a časováních, nezjistí veškerý čas strávený při autorizaci a vygenerování zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="4d1d4-143">Můžete si přečíst informace o mém časovači v [profilu a čas, kdy vaše aplikace ASP.NET MVC vše navede do Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="4d1d4-144">Stránka [karty](http://getglimpse.com/Docs/Tabs) obsahuje odkazy na podrobné informace o jednotlivých kartách.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="4d1d4-145">Karta Časová osa</span><span class="sxs-lookup"><span data-stu-id="4d1d4-145">The Timeline tab</span></span>

<span data-ttu-id="4d1d4-146">Změnil (a) jsem si nezpracovaný [kurz Dykstra EF 6/MVC 5](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) s následující změnou kódu na řadič instruktorů:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="4d1d4-147">Výše uvedený kód umožňuje mně předat řetězec dotazu (`eager`) k řízení Eager nebo explicitního načítání dat.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="4d1d4-148">Na následujícím obrázku je použit explicitní načítání a na stránce časování se zobrazí všechny zápisy, které jsou načteny v metodě `Index` Action:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![explicitní načítání](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="4d1d4-150">V následujícím kódu je zadán Eager a každý zápis je načten po volání zobrazení `Index`:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![Eager je zadaný.](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="4d1d4-152">Když najedete myší na časový segment, získáte podrobné informace o časování:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-152">You can hover over a time segment to get detailed timing information:</span></span>

![Pokud chcete zobrazit podrobné časování, najeďte myší.](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="4d1d4-154">Vazba modelu</span><span class="sxs-lookup"><span data-stu-id="4d1d4-154">Model Binding</span></span>

<span data-ttu-id="4d1d4-155">[Karta vazba modelu](http://getglimpse.com/Docs/Model-Binding-Tab) poskytuje spoustu informací, které vám pomohou pochopit, jak jsou proměnné formuláře svázané a proč některé nejsou vázané na to, co by očekávalo.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="4d1d4-156">Následující obrázek ukazuje **?**</span><span class="sxs-lookup"><span data-stu-id="4d1d4-156">The image below shows the **?**</span></span> <span data-ttu-id="4d1d4-157">ikona, na kterou můžete kliknout a získat tak stránku s nápovědu nakoukněte pro tuto funkci.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![zobrazení vazby modelu nakoukněte](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="4d1d4-159">Trasy</span><span class="sxs-lookup"><span data-stu-id="4d1d4-159">Routes</span></span>

 <span data-ttu-id="4d1d4-160">Karta trasy nakoukněte vám může přispět k ladění a pochopení směrování.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="4d1d4-161">Na následujícím obrázku je vybraná trasa k produktu (a zobrazuje se v nakoukněte konvenci zeleně).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="4d1d4-162">Zobrazuje se taky ![vybraný název produktu](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) omezení tras, oblasti a datové tokeny.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="4d1d4-163">Další informace najdete v tématu [nakoukněte trasy](http://getglimpse.com/Docs/Routes-Tab) a [směrování atributů v ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="4d1d4-164">Používání nakoukněte v Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d4-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="4d1d4-165">Výchozí zásady zabezpečení nakoukněte povolují, aby se data nakoukněte zobrazovala jenom z místního hostitele.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="4d1d4-166">Tuto zásadu zabezpečení můžete změnit, abyste mohli tato data zobrazit na vzdáleném serveru (například v Azure Web App).</span><span class="sxs-lookup"><span data-stu-id="4d1d4-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="4d1d4-167">V případě testovacích prostředí v Azure přidejte zvýrazněné označení do dolní části souboru *Web. config* a povolte nakoukněte:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.config* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="4d1d4-168">Tato změna samostatně umožňuje všem uživatelům zobrazit data nakoukněte ve vzdálené lokalitě.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="4d1d4-169">Zvažte přidání značky výše k publikačnímu profilu, takže se nasadí jenom použité, když použijete tento profil publikování (například Azure test Profile). K omezení dat nakoukněte přidáme roli `canViewGlimpseData` a povolíte uživatelům v této roli jenom zobrazení dat nakoukněte.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-169">Consider adding the markup above to a publish profile so it's only deployed an applied when you use that publish profile (for example, your Azure test profile.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="4d1d4-170">Odstraňte komentáře ze souboru *GlimpseSecurityPolicy.cs* a změňte volání [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) z `Administrator` na roli `canViewGlimpseData`:</span><span class="sxs-lookup"><span data-stu-id="4d1d4-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="4d1d4-171">Zabezpečení: rozsáhlá data, která poskytuje nakoukněte, by mohla vystavit zabezpečení vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="4d1d4-172">Společnost Microsoft neprovedla audit zabezpečení nakoukněte pro použití v aplikacích v produkci.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>

<span data-ttu-id="4d1d4-173">Informace o přidávání rolí najdete v kurzu [nasazení webové aplikace ASP.NET MVC 5 pomocí členství, protokolu OAuth a SQL Database do kurzu Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) .</span><span class="sxs-lookup"><span data-stu-id="4d1d4-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="4d1d4-174">Další materiály a zdroje informací</span><span class="sxs-lookup"><span data-stu-id="4d1d4-174">Additional Resources</span></span>

- [<span data-ttu-id="4d1d4-175">Nasazení zabezpečené aplikace ASP.NET MVC 5 s členstvím, protokolem OAuth a SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d4-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="4d1d4-176">[Konfigurace nakoukněte](http://getglimpse.com/Docs/Configuration) – Stránka s dokumentem týkající se konfigurace karet, zásad modulu runtime, protokolování a dalších.</span><span class="sxs-lookup"><span data-stu-id="4d1d4-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
