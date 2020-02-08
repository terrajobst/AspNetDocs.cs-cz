---
uid: single-page-application/overview/templates/hottowel-template
title: Hot navrhování ručníků Template | Microsoft Docs
author: madskristensen
description: Šablona HotTowel
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075057"
---
# <a name="hot-towel-template"></a><span data-ttu-id="fcedc-103">Šablona Hot Towel</span><span class="sxs-lookup"><span data-stu-id="fcedc-103">Hot Towel template</span></span>

<span data-ttu-id="fcedc-104">od [Madse Kristensena](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="fcedc-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="fcedc-105">Hot navrhování ručníků se šablona MVC zapisuje Jan Papa</span><span class="sxs-lookup"><span data-stu-id="fcedc-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="fcedc-106">Vyberte verzi, kterou chcete stáhnout:</span><span class="sxs-lookup"><span data-stu-id="fcedc-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="fcedc-107">Šablona MVC Hot navrhování ručníků pro Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="fcedc-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="fcedc-108">Šablona MVC Hot navrhování ručníků pro Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="fcedc-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="fcedc-109">Hot navrhování ručníků: vzhledem k tomu, že nechcete, aby bylo možné přejít na zabezpečené ověřování pro hesla bez použití!</span><span class="sxs-lookup"><span data-stu-id="fcedc-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>

<span data-ttu-id="fcedc-110">Chcete sestavit SPA, ale nemůžete se rozhodnout, kde začít?</span><span class="sxs-lookup"><span data-stu-id="fcedc-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="fcedc-111">Používejte horké navrhování ručníků a v sekundách budete mít zabezpečené a všechny nástroje, které potřebujete k sestavení na počítači!.</span><span class="sxs-lookup"><span data-stu-id="fcedc-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="fcedc-112">Hot navrhování ručníků vytvoří skvělý výchozí bod pro vytváření jednostránkové aplikace (SPA) s ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fcedc-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="fcedc-113">V tomto poli poskytuje modulární strukturu pro váš kód, zobrazení navigace, datovou vazbu, bohatou správu dat a jednoduché, ale elegantní styly.</span><span class="sxs-lookup"><span data-stu-id="fcedc-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="fcedc-114">Hot navrhování ručníků poskytuje vše, co potřebujete k vytvoření zabezpečeného hesla, takže se můžete soustředit na svou aplikaci, ne na instalace.</span><span class="sxs-lookup"><span data-stu-id="fcedc-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="fcedc-115">Přečtěte si další informace o vytváření zabezpečeného hesla z [Jan Papa videa, výukových kurzů a Pluralsight kurzů](http://johnpapa.net/spa?vsix).</span><span class="sxs-lookup"><span data-stu-id="fcedc-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>

## <a name="application-structure"></a><span data-ttu-id="fcedc-116">Struktura aplikace</span><span class="sxs-lookup"><span data-stu-id="fcedc-116">Application Structure</span></span>

<span data-ttu-id="fcedc-117">Hot navrhování ručníků SPA poskytuje složku aplikace, která obsahuje JavaScript a soubory HTML, které definují vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="fcedc-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="fcedc-118">Ve složce aplikace:</span><span class="sxs-lookup"><span data-stu-id="fcedc-118">Inside the App folder:</span></span>

- <span data-ttu-id="fcedc-119">durandal</span><span class="sxs-lookup"><span data-stu-id="fcedc-119">durandal</span></span>
- <span data-ttu-id="fcedc-120">services</span><span class="sxs-lookup"><span data-stu-id="fcedc-120">services</span></span>
- <span data-ttu-id="fcedc-121">viewmodels</span><span class="sxs-lookup"><span data-stu-id="fcedc-121">viewmodels</span></span>
- <span data-ttu-id="fcedc-122">views</span><span class="sxs-lookup"><span data-stu-id="fcedc-122">views</span></span>

<span data-ttu-id="fcedc-123">Složka aplikace obsahuje kolekci modulů.</span><span class="sxs-lookup"><span data-stu-id="fcedc-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="fcedc-124">Tyto moduly zapouzdřují funkce a deklaruje závislosti na dalších modulech.</span><span class="sxs-lookup"><span data-stu-id="fcedc-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="fcedc-125">Složka zobrazení obsahuje HTML pro vaši aplikaci a složka ViewModels obsahuje logiku prezentace pro zobrazení (společný vzor MVVM).</span><span class="sxs-lookup"><span data-stu-id="fcedc-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="fcedc-126">Složka služby je ideální pro uchovávání všech běžných služeb, které vaše aplikace může potřebovat, jako je například načtení dat HTTP nebo interakce místního úložiště.</span><span class="sxs-lookup"><span data-stu-id="fcedc-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="fcedc-127">Je běžné, že více ViewModels opakovaně používá kód z modulů služby.</span><span class="sxs-lookup"><span data-stu-id="fcedc-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="fcedc-128">Struktura aplikace na straně serveru ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="fcedc-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="fcedc-129">Horká navrhování ručníků se staví na známé a výkonné struktuře ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fcedc-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="fcedc-130">Začátek aplikace\_</span><span class="sxs-lookup"><span data-stu-id="fcedc-130">App\_Start</span></span>
- <span data-ttu-id="fcedc-131">Obsah</span><span class="sxs-lookup"><span data-stu-id="fcedc-131">Content</span></span>
- <span data-ttu-id="fcedc-132">Kontrolery</span><span class="sxs-lookup"><span data-stu-id="fcedc-132">Controllers</span></span>
- <span data-ttu-id="fcedc-133">Modely</span><span class="sxs-lookup"><span data-stu-id="fcedc-133">Models</span></span>
- <span data-ttu-id="fcedc-134">Scripts</span><span class="sxs-lookup"><span data-stu-id="fcedc-134">Scripts</span></span>
- <span data-ttu-id="fcedc-135">Zobrazení</span><span class="sxs-lookup"><span data-stu-id="fcedc-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="fcedc-136">Doporučené knihovny</span><span class="sxs-lookup"><span data-stu-id="fcedc-136">Featured Libraries</span></span>

- <span data-ttu-id="fcedc-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="fcedc-137">ASP.NET MVC</span></span>
- <span data-ttu-id="fcedc-138">Webové rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fcedc-138">ASP.NET Web API</span></span>
- <span data-ttu-id="fcedc-139">ASP.NET Web Optimization – sdružování a minifikace</span><span class="sxs-lookup"><span data-stu-id="fcedc-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="fcedc-140">[Breeze. js](http://Breezejs.com) – Správa dat ve bohatě</span><span class="sxs-lookup"><span data-stu-id="fcedc-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="fcedc-141">[Durandal. js](http://Durandaljs.com) – navigace a zobrazení – kompozice</span><span class="sxs-lookup"><span data-stu-id="fcedc-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="fcedc-142">[Vyseknutí. js](http://Knockoutjs.com) – datové vazby</span><span class="sxs-lookup"><span data-stu-id="fcedc-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="fcedc-143">[Vyžadování modularity. js](http://requirejs.org) s využitím AMD a optimalizace</span><span class="sxs-lookup"><span data-stu-id="fcedc-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="fcedc-144">[Informační zpráva. js](http://jpapa.me/c7toastr) – překryvné zprávy</span><span class="sxs-lookup"><span data-stu-id="fcedc-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="fcedc-145">Spuštění [Twitteru](https://twitter.github.com/bootstrap/) – robustní styly CSS</span><span class="sxs-lookup"><span data-stu-id="fcedc-145">[Twitter Bootstrap](https://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="fcedc-146">Instalace prostřednictvím šablony zabezpečeného hesla sady Visual Studio 2012 Hot navrhování ručníků</span><span class="sxs-lookup"><span data-stu-id="fcedc-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="fcedc-147">Hot navrhování ručníků se dá nainstalovat jako šablona sady Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="fcedc-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="fcedc-148">Stačí kliknout na `File` | `New Project` a zvolit `ASP.NET MVC 4 Web Application`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="fcedc-149">Pak vyberte šablonu Hot navrhování ručníků Page a spusťte ji!</span><span class="sxs-lookup"><span data-stu-id="fcedc-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="fcedc-150">Instalace prostřednictvím balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="fcedc-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="fcedc-151">Hot navrhování ručníků je také balíček NuGet, který rozšiřuje existující prázdný projekt ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fcedc-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="fcedc-152">Stačí jenom nainstalovat pomocí NuGet a pak spustit.</span><span class="sxs-lookup"><span data-stu-id="fcedc-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="fcedc-153">Jak na Hot navrhování ručníků vytvořit?</span><span class="sxs-lookup"><span data-stu-id="fcedc-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="fcedc-154">Stačí začít přidávat kód!</span><span class="sxs-lookup"><span data-stu-id="fcedc-154">Simply start adding code!</span></span>

1. <span data-ttu-id="fcedc-155">Přidejte vlastní kód na straně serveru, nejlépe Entity Framework a WebAPI (což skutečně září Breeze. js).</span><span class="sxs-lookup"><span data-stu-id="fcedc-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="fcedc-156">Přidat zobrazení do složky `App/views`</span><span class="sxs-lookup"><span data-stu-id="fcedc-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="fcedc-157">Přidat ViewModels do složky `App/viewmodels`</span><span class="sxs-lookup"><span data-stu-id="fcedc-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="fcedc-158">Přidání datových vazeb HTML a vykrojení do nových zobrazení</span><span class="sxs-lookup"><span data-stu-id="fcedc-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="fcedc-159">Aktualizovat navigační trasy v `shell.js`</span><span class="sxs-lookup"><span data-stu-id="fcedc-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="fcedc-160">Návod pro HTML/JavaScript</span><span class="sxs-lookup"><span data-stu-id="fcedc-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="fcedc-161">Views/HotTowel/index.cshtml</span><span class="sxs-lookup"><span data-stu-id="fcedc-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="fcedc-162">index. cshtml je počáteční trasa a zobrazení pro aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="fcedc-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="fcedc-163">Obsahuje všechny standardní metaznačky, odkazy CSS a reference JavaScriptu, které byste očekávali.</span><span class="sxs-lookup"><span data-stu-id="fcedc-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="fcedc-164">Tělo obsahuje jednu `<div>`, kde se při vyžádání umístí veškerý obsah (vaše zobrazení).</span><span class="sxs-lookup"><span data-stu-id="fcedc-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="fcedc-165">`@Scripts.Render` používá pro spuštění úvodního bodu pro kód aplikace, který je obsažen v souboru `main.js`, požadavek. js.</span><span class="sxs-lookup"><span data-stu-id="fcedc-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="fcedc-166">K dispozici je úvodní obrazovka, která ukazuje, jak během načítání aplikace vytvořit úvodní obrazovku.</span><span class="sxs-lookup"><span data-stu-id="fcedc-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="fcedc-167">App/main.js</span><span class="sxs-lookup"><span data-stu-id="fcedc-167">App/main.js</span></span>

<span data-ttu-id="fcedc-168">`main.js` soubor obsahuje kód, který se spustí hned po načtení vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="fcedc-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="fcedc-169">Tady je místo, kde chcete definovat vaše navigační trasy, nastavit zobrazení pro spuštění a provádět libovolné instalační a zaváděcí operace, jako je například vytváření dat aplikace.</span><span class="sxs-lookup"><span data-stu-id="fcedc-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="fcedc-170">`main.js` soubor definuje několik modulů durandal, které pomůžou aplikaci začít spouštět.</span><span class="sxs-lookup"><span data-stu-id="fcedc-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="fcedc-171">Příkaz define pomáhá vyhodnotit závislosti modulů, aby byly k dispozici pro funkci.</span><span class="sxs-lookup"><span data-stu-id="fcedc-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="fcedc-172">Nejprve jsou povoleny ladicí zprávy, které odesílají zprávy o událostech, které aplikace provádí v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="fcedc-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="fcedc-173">Aplikace. Start Code instruuje durandal Framework pro spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="fcedc-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="fcedc-174">Konvence jsou nastaveny tak, aby durandal ví, že všechna zobrazení a ViewModels jsou obsaženy ve stejných pojmenovaných složkách v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="fcedc-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="fcedc-175">Nakonec `app.setRoot` načte `shell` pomocí předdefinované animace `entrance`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="fcedc-176">Zobrazení</span><span class="sxs-lookup"><span data-stu-id="fcedc-176">Views</span></span>

<span data-ttu-id="fcedc-177">Zobrazení se nacházejí ve složce `App/views`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="fcedc-178">shell.html</span><span class="sxs-lookup"><span data-stu-id="fcedc-178">shell.html</span></span>

<span data-ttu-id="fcedc-179">`shell.html` obsahuje rozložení předlohy pro váš kód HTML.</span><span class="sxs-lookup"><span data-stu-id="fcedc-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="fcedc-180">Všechna ostatní zobrazení se budou skládat někam do zobrazení `shell`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="fcedc-181">Hot navrhování ručníků poskytuje `shell` se třemi takovými oblastmi: záhlaví, oblast obsahu a zápatí.</span><span class="sxs-lookup"><span data-stu-id="fcedc-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="fcedc-182">Každá z těchto oblastí je načtena s obsahem, který je v případě potřeby v jiných zobrazeních.</span><span class="sxs-lookup"><span data-stu-id="fcedc-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="fcedc-183">Vazby `compose` pro záhlaví a zápatí jsou pevně kódované v Hot navrhování ručníků, aby odkazovaly na zobrazení `nav` a `footer`, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="fcedc-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="fcedc-184">Vazba pro psaní oddílu `#content` je vázána na aktivní položku modulu `router`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="fcedc-185">Jinými slovy, když kliknete na navigační odkaz, v této oblasti se načte odpovídající zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fcedc-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="fcedc-186">nav.html</span><span class="sxs-lookup"><span data-stu-id="fcedc-186">nav.html</span></span>

<span data-ttu-id="fcedc-187">`nav.html` obsahuje navigační odkazy pro SPA.</span><span class="sxs-lookup"><span data-stu-id="fcedc-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="fcedc-188">Zde lze umístit strukturu nabídky, například.</span><span class="sxs-lookup"><span data-stu-id="fcedc-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="fcedc-189">Často se jedná o datovou vazbu (pomocí vykrojení) do modulu `router` pro zobrazení navigace, kterou jste definovali v `shell.js`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="fcedc-190">Vyseknutí vyhledá atributy vazby dat a váže je na `shell` ViewModel, aby zobrazila navigační trasy a zobrazila ProgressBar (pomocí služby Twitter Bootstrap), pokud je modul `router` uprostřed přechodu z jednoho zobrazení na jiný (viz `router.isNavigating`).</span><span class="sxs-lookup"><span data-stu-id="fcedc-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="fcedc-191">Home. html a details. html</span><span class="sxs-lookup"><span data-stu-id="fcedc-191">home.html and details.html</span></span>

<span data-ttu-id="fcedc-192">Tato zobrazení obsahují HTML pro vlastní zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fcedc-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="fcedc-193">Pokud se klikne na odkaz `home` v nabídce zobrazení `nav`, bude zobrazení `home` umístěno v oblasti obsahu `shell` zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fcedc-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="fcedc-194">Tato zobrazení lze rozšířit nebo nahradit vlastními zobrazeními.</span><span class="sxs-lookup"><span data-stu-id="fcedc-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="fcedc-195">footer.html</span><span class="sxs-lookup"><span data-stu-id="fcedc-195">footer.html</span></span>

<span data-ttu-id="fcedc-196">`footer.html` obsahuje kód HTML, který se zobrazí v zápatí, v dolní části `shell` zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fcedc-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="fcedc-197">ViewModels</span><span class="sxs-lookup"><span data-stu-id="fcedc-197">ViewModels</span></span>

<span data-ttu-id="fcedc-198">ViewModels se nachází ve složce `App/viewmodels`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="fcedc-199">shell.js</span><span class="sxs-lookup"><span data-stu-id="fcedc-199">shell.js</span></span>

<span data-ttu-id="fcedc-200">`shell` ViewModel obsahuje vlastnosti a funkce, které jsou vázány na zobrazení `shell`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="fcedc-201">Často je to místo, kde se nacházejí navigační vazby nabídky (viz logika `router.mapNav`).</span><span class="sxs-lookup"><span data-stu-id="fcedc-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="fcedc-202">Home. js a details. js</span><span class="sxs-lookup"><span data-stu-id="fcedc-202">home.js and details.js</span></span>

<span data-ttu-id="fcedc-203">Tyto ViewModels obsahují vlastnosti a funkce, které jsou vázány na zobrazení `home`.</span><span class="sxs-lookup"><span data-stu-id="fcedc-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="fcedc-204">obsahuje také logiku prezentace pro zobrazení a je připevněn mezi daty a zobrazením.</span><span class="sxs-lookup"><span data-stu-id="fcedc-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="fcedc-205">Služby</span><span class="sxs-lookup"><span data-stu-id="fcedc-205">Services</span></span>

<span data-ttu-id="fcedc-206">Služby se nacházejí ve složce App/Services.</span><span class="sxs-lookup"><span data-stu-id="fcedc-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="fcedc-207">V ideálním případě by bylo možné umístit budoucí služby, jako je například modul DataService, který je zodpovědný za získání a odeslání vzdálených dat.</span><span class="sxs-lookup"><span data-stu-id="fcedc-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="fcedc-208">logger.js</span><span class="sxs-lookup"><span data-stu-id="fcedc-208">logger.js</span></span>

<span data-ttu-id="fcedc-209">Hot navrhování ručníků poskytuje modul `logger` ve složce služby.</span><span class="sxs-lookup"><span data-stu-id="fcedc-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="fcedc-210">Modul `logger` je ideální pro protokolování zpráv do konzoly a uživatele v překryvném okně informační zprávy.</span><span class="sxs-lookup"><span data-stu-id="fcedc-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
