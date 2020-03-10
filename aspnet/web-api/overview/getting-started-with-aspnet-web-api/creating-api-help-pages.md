---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: Vytváření stránek s nápovědu pro ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Tento kurz s kódem ukazuje, jak vytvořit stránky s nápovědu pro ASP.NET webové rozhraní API v ASP.NET 4. x.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556873"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="ff464-103">Vytváření stránek s nápovědu pro webové rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ff464-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="ff464-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ff464-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ff464-105">Tento kurz s kódem ukazuje, jak vytvořit stránky s nápovědu pro ASP.NET webové rozhraní API v ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="ff464-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="ff464-106">Při vytváření webového rozhraní API je často užitečné vytvořit stránku s přehledem, aby ostatní vývojáři věděli, jak vaše rozhraní API volat.</span><span class="sxs-lookup"><span data-stu-id="ff464-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="ff464-107">Můžete vytvořit veškerou dokumentaci ručně, ale je lepší ji vygenerovat co nejvíce.</span><span class="sxs-lookup"><span data-stu-id="ff464-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="ff464-108">Pro usnadnění tohoto úkolu poskytuje webové rozhraní API ASP.NET knihovnu pro automatické generování stránek s podporou v době běhu.</span><span class="sxs-lookup"><span data-stu-id="ff464-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="ff464-109">Vytváření stránek s nápovědě k rozhraní API</span><span class="sxs-lookup"><span data-stu-id="ff464-109">Creating API Help Pages</span></span>

<span data-ttu-id="ff464-110">Nainstalujte [aktualizaci ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="ff464-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="ff464-111">Tato aktualizace integruje stránky s nápovědě do šablony projektu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="ff464-112">Dále vytvořte nový projekt ASP.NET MVC 4 a vyberte šablonu projektu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="ff464-113">Šablona projektu vytvoří ukázkový kontroler rozhraní API s názvem `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="ff464-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="ff464-114">Šablona také vytvoří stránky s nápovědě k rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-114">The template also creates the API help pages.</span></span> <span data-ttu-id="ff464-115">Všechny soubory kódu pro stránku s nápovědu jsou umístěny do složky oblasti projektu.</span><span class="sxs-lookup"><span data-stu-id="ff464-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="ff464-116">Po spuštění aplikace obsahuje Domovská stránka odkaz na stránku s informacemi o rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="ff464-117">Z domovské stránky je relativní cesta/help.</span><span class="sxs-lookup"><span data-stu-id="ff464-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="ff464-118">Tento odkaz vás přesune na stránku souhrnu rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="ff464-119">Zobrazení MVC pro tuto stránku je definováno v oblasti/HelpPage/zobrazení/help/index. cshtml.</span><span class="sxs-lookup"><span data-stu-id="ff464-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="ff464-120">Tuto stránku můžete upravit a upravit tak rozložení, Úvod, nadpis, styly a tak dále.</span><span class="sxs-lookup"><span data-stu-id="ff464-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="ff464-121">Hlavní část stránky je tabulka rozhraní API seskupená podle kontroleru.</span><span class="sxs-lookup"><span data-stu-id="ff464-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="ff464-122">Položky tabulky jsou generovány dynamicky pomocí rozhraní **IApiExplorer** .</span><span class="sxs-lookup"><span data-stu-id="ff464-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="ff464-123">(Další informace o tomto rozhraní se dozvíte později.) Pokud přidáte nový kontroler rozhraní API, tabulka se automaticky aktualizuje v době běhu.</span><span class="sxs-lookup"><span data-stu-id="ff464-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="ff464-124">Sloupec "rozhraní API" obsahuje seznam metod HTTP a relativního identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="ff464-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="ff464-125">Sloupec Description (popis) obsahuje dokumentaci pro každé rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="ff464-126">Zpočátku je dokumentace pouze zástupný text.</span><span class="sxs-lookup"><span data-stu-id="ff464-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="ff464-127">V další části si ukážeme, jak přidat dokumentaci z komentářů XML.</span><span class="sxs-lookup"><span data-stu-id="ff464-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="ff464-128">Každé rozhraní API má odkaz na stránku s podrobnějšími informacemi, včetně příkladů požadavků a těl odpovědí.</span><span class="sxs-lookup"><span data-stu-id="ff464-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="ff464-129">Přidání stránek s nápovědě do existujícího projektu</span><span class="sxs-lookup"><span data-stu-id="ff464-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="ff464-130">Stránky s přehledem můžete přidat do existujícího projektu webového rozhraní API pomocí Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="ff464-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="ff464-131">Tato možnost je užitečná, když začínáte s jinou šablonou projektu než s šablonou Web API.</span><span class="sxs-lookup"><span data-stu-id="ff464-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="ff464-132">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="ff464-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="ff464-133">V okně [konzoly Správce balíčků](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) zadejte jeden z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="ff464-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="ff464-134">Pro **C#** aplikaci: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="ff464-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="ff464-135">Pro **Visual Basic** aplikaci: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="ff464-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="ff464-136">Existují dva balíčky, jeden pro C# a jeden pro Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="ff464-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="ff464-137">Ujistěte se, že použijete ten, který odpovídá vašemu projektu.</span><span class="sxs-lookup"><span data-stu-id="ff464-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="ff464-138">Tento příkaz nainstaluje potřebná sestavení a přidá zobrazení MVC pro stránky s nápovědu (umístěné ve složce oblasti/HelpPage).</span><span class="sxs-lookup"><span data-stu-id="ff464-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="ff464-139">Musíte ručně přidat odkaz na stránku s usnadněním.</span><span class="sxs-lookup"><span data-stu-id="ff464-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="ff464-140">Identifikátor URI je/help.</span><span class="sxs-lookup"><span data-stu-id="ff464-140">The URI is /Help.</span></span> <span data-ttu-id="ff464-141">Chcete-li vytvořit odkaz v zobrazení Razor, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="ff464-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="ff464-142">Také nezapomeňte zaregistrovat oblasti.</span><span class="sxs-lookup"><span data-stu-id="ff464-142">Also, make sure to register areas.</span></span> <span data-ttu-id="ff464-143">V souboru Global. asax přidejte následující kód do **aplikace\_Start** , pokud tam ještě není:</span><span class="sxs-lookup"><span data-stu-id="ff464-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="ff464-144">Přidání dokumentace k rozhraní API</span><span class="sxs-lookup"><span data-stu-id="ff464-144">Adding API Documentation</span></span>

<span data-ttu-id="ff464-145">Ve výchozím nastavení mají stránky pro nápovědu zástupné řetězce pro dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="ff464-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="ff464-146">Pomocí dokumentačních [komentářů XML](https://msdn.microsoft.com/library/b2s063f7.aspx) můžete vytvořit dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="ff464-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="ff464-147">Pokud chcete tuto funkci povolit, otevřete soubor oblasti souborů/HelpPage/App\_spusťte/HelpPageConfig. cs a odkomentujte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="ff464-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="ff464-148">Teď povolte dokumentaci XML.</span><span class="sxs-lookup"><span data-stu-id="ff464-148">Now enable XML documentation.</span></span> <span data-ttu-id="ff464-149">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="ff464-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="ff464-150">Vyberte stránku **sestavení** .</span><span class="sxs-lookup"><span data-stu-id="ff464-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="ff464-151">V části **výstup**ověřte **soubor dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="ff464-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="ff464-152">Do pole pro úpravy zadejte "App\_data/XmlDocument. XML".</span><span class="sxs-lookup"><span data-stu-id="ff464-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="ff464-153">V dalším kroku otevřete kód pro `ValuesController` kontroler rozhraní API, který je definovaný v/Controllers/ValuesController.cs.</span><span class="sxs-lookup"><span data-stu-id="ff464-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="ff464-154">Přidejte do metod kontroleru nějaké dokumentační komentáře.</span><span class="sxs-lookup"><span data-stu-id="ff464-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="ff464-155">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ff464-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="ff464-156">Tip: Pokud umístíte blikající kurzor na řádek nad metodu a zadáte tři lomítka, Visual Studio automaticky vloží prvky XML.</span><span class="sxs-lookup"><span data-stu-id="ff464-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="ff464-157">Pak můžete vyplnit prázdné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="ff464-157">Then you can fill in the blanks.</span></span>

<span data-ttu-id="ff464-158">Nyní Sestavte a spusťte aplikaci znovu a přejděte na stránku s nápovědě.</span><span class="sxs-lookup"><span data-stu-id="ff464-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="ff464-159">V tabulce rozhraní API by se měly zobrazit řetězce dokumentace.</span><span class="sxs-lookup"><span data-stu-id="ff464-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="ff464-160">Stránka Help čte řetězce ze souboru XML v době běhu.</span><span class="sxs-lookup"><span data-stu-id="ff464-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="ff464-161">(Při nasazení aplikace nezapomeňte nasadit soubor XML.)</span><span class="sxs-lookup"><span data-stu-id="ff464-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="ff464-162">Pod kapotou</span><span class="sxs-lookup"><span data-stu-id="ff464-162">Under the Hood</span></span>

<span data-ttu-id="ff464-163">Stránky s usnadněním jsou postaveny nad třídou **ApiExplorer** , která je součástí rozhraní Web API Framework.</span><span class="sxs-lookup"><span data-stu-id="ff464-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="ff464-164">Třída **ApiExplorer** poskytuje nezpracovaný materiál pro vytvoření stránky s nápovědu.</span><span class="sxs-lookup"><span data-stu-id="ff464-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="ff464-165">Pro každé rozhraní API obsahuje **ApiExplorer** **ApiDescription** , který popisuje rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="ff464-166">Pro tento účel je "rozhraní API" definováno jako kombinace metody HTTP a relativního identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="ff464-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="ff464-167">Tady jsou například některá odlišná rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="ff464-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="ff464-168">ZÍSKAT/api/Products</span><span class="sxs-lookup"><span data-stu-id="ff464-168">GET /api/Products</span></span>
- <span data-ttu-id="ff464-169">ZÍSKAT/api/Products/{id}</span><span class="sxs-lookup"><span data-stu-id="ff464-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="ff464-170">PŘÍSPĚVEK/api/Products</span><span class="sxs-lookup"><span data-stu-id="ff464-170">POST /api/Products</span></span>

<span data-ttu-id="ff464-171">Pokud akce kontroleru podporuje více metod HTTP, **ApiExplorer** považuje každou metodu za odlišné rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="ff464-172">Chcete-li skrýt rozhraní API z **ApiExplorer**, přidejte do akce atribut **ApiExplorerSettings** a nastavte *IgnoreApi* na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="ff464-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="ff464-173">Tento atribut můžete také přidat do kontroleru pro vyloučení celého kontroleru.</span><span class="sxs-lookup"><span data-stu-id="ff464-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="ff464-174">Třída ApiExplorer získává řetězce dokumentace z rozhraní **IDocumentationProvider** .</span><span class="sxs-lookup"><span data-stu-id="ff464-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="ff464-175">Jak bylo uvedeno dříve, knihovna stránky pro usnadnění poskytuje **IDocumentationProvider** , který získává dokumentaci z dokumentů XML dokumentace.</span><span class="sxs-lookup"><span data-stu-id="ff464-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="ff464-176">Kód je umístěný v/Areas/HelpPage/XmlDocumentationProvider.cs.</span><span class="sxs-lookup"><span data-stu-id="ff464-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="ff464-177">Dokumentaci z jiného zdroje můžete získat tak, že napíšete vlastní **IDocumentationProvider**.</span><span class="sxs-lookup"><span data-stu-id="ff464-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="ff464-178">Pro jeho vedení volejte metodu rozšíření **SetDocumentationProvider** definovanou v **HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="ff464-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="ff464-179">**ApiExplorer** automaticky volá rozhraní **IDocumentationProvider** , aby získala dokumentační řetězce pro každé rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ff464-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="ff464-180">Ukládá je do vlastnosti **dokumentace** objektů **ApiDescription** a **ApiParameterDescription** .</span><span class="sxs-lookup"><span data-stu-id="ff464-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff464-181">Další kroky</span><span class="sxs-lookup"><span data-stu-id="ff464-181">Next Steps</span></span>

<span data-ttu-id="ff464-182">Nejste omezeni na stránky s technickou pomocí, které jsou zde uvedeny.</span><span class="sxs-lookup"><span data-stu-id="ff464-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="ff464-183">**ApiExplorer** se ve skutečnosti neomezí na vytváření stránek s nápovědě.</span><span class="sxs-lookup"><span data-stu-id="ff464-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="ff464-184">Yao Huang – vypsalo jsme některé skvělé blogové příspěvky, které vám pomohou se zamyslet ze svého boxu:</span><span class="sxs-lookup"><span data-stu-id="ff464-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="ff464-185">Přidání jednoduchého testovacího klienta na stránku ASP.NET webové rozhraní API</span><span class="sxs-lookup"><span data-stu-id="ff464-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="ff464-186">Stránka podpory webového rozhraní API pro ASP.NET funguje na samoobslužných službách</span><span class="sxs-lookup"><span data-stu-id="ff464-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="ff464-187">Generování stránky s nápovědu (nebo klienta) v době návrhu pro webové rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ff464-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="ff464-188">Pokročilá přizpůsobení stránky s technickou nastavením</span><span class="sxs-lookup"><span data-stu-id="ff464-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
