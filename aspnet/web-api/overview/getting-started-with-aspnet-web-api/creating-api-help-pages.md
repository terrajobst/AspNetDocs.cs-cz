---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: Vytváření stránek nápovědy pro rozhraní ASP.NET Web API – ASP.NET 4.x
author: MikeWasson
description: V tomto kurzu se kód ukazuje, jak vytvořit stránky nápovědy pro ASP.NET Web API v ASP.NET 4.x.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: e3f6a9b8a6835b034a075d580cd9a33136969990
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395010"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="2a794-103">Vytváření stránek nápovědy pro rozhraní ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2a794-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="2a794-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2a794-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2a794-105">V tomto kurzu se kód ukazuje, jak vytvořit stránky nápovědy pro ASP.NET Web API v ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="2a794-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="2a794-106">Při vytváření webového rozhraní API, často je užitečné vytvořit stránku nápovědy, tak, aby ostatní vývojáři vědět, jak volat rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="2a794-107">Dokumentace může vytvořit ručně, ale je lepší automaticky vytvořit co největší míře.</span><span class="sxs-lookup"><span data-stu-id="2a794-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="2a794-108">Pro usnadnění tohoto úkolu, rozhraní ASP.NET Web API poskytuje knihovnu pro automatické generování stránek nápovědy v době běhu.</span><span class="sxs-lookup"><span data-stu-id="2a794-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="2a794-109">Vytváření stránek nápovědy k rozhraní API</span><span class="sxs-lookup"><span data-stu-id="2a794-109">Creating API Help Pages</span></span>

<span data-ttu-id="2a794-110">Nainstalujte [ASP.NET a Web Tools 2012.2 aktualizace](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="2a794-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="2a794-111">Tato aktualizace stránky nápovědy integruje šablony projektu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="2a794-112">Dále vytvořte nový projekt ASP.NET MVC 4 a vyberte šablonu projektu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="2a794-113">Šablona projektu vytvoří řadič ukázkové rozhraní API s názvem `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="2a794-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="2a794-114">Šablona vytvoří také stránek nápovědy rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-114">The template also creates the API help pages.</span></span> <span data-ttu-id="2a794-115">Všechny soubory kódu stránky s nápovědou jsou umístěny ve složce oblasti projektu.</span><span class="sxs-lookup"><span data-stu-id="2a794-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="2a794-116">Při spuštění aplikace na domovské stránce obsahuje odkaz na stránku nápovědy na rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="2a794-117">Z domovské stránky je relativní cesta/help.</span><span class="sxs-lookup"><span data-stu-id="2a794-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="2a794-118">Tento odkaz vám přináší na souhrnnou stránku rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="2a794-119">Pro tuto stránku zobrazení MVC je definována v Areas/HelpPage/Views/Help/Index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="2a794-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="2a794-120">Můžete upravit této stránky můžete upravit rozložení, úvod, název, styly a tak dále.</span><span class="sxs-lookup"><span data-stu-id="2a794-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="2a794-121">Hlavní části stránky je tabulka rozhraní API, seskupené podle kontroleru.</span><span class="sxs-lookup"><span data-stu-id="2a794-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="2a794-122">Položky tabulky generuje dynamicky pomocí **IApiExplorer** rozhraní.</span><span class="sxs-lookup"><span data-stu-id="2a794-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="2a794-123">(I více zabývat toto rozhraní později.) Pokud chcete přidat nový kontroler API, se automaticky aktualizuje v tabulce v době běhu.</span><span class="sxs-lookup"><span data-stu-id="2a794-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="2a794-124">Sloupce "Rozhraní API" seznam metodu HTTP a relativní identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="2a794-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="2a794-125">Ve sloupci "Popis" obsahuje dokumentaci pro každé rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="2a794-126">Na začátku dokumentace je jen zástupný text.</span><span class="sxs-lookup"><span data-stu-id="2a794-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="2a794-127">V další části můžu ukážeme, jak přidat dokumentace ke službě z komentářů XML.</span><span class="sxs-lookup"><span data-stu-id="2a794-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="2a794-128">Každé rozhraní API obsahuje odkaz na stránku se podrobnější informace, včetně příklad těla požadavku a odpovědi.</span><span class="sxs-lookup"><span data-stu-id="2a794-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="2a794-129">Přidání stránky nápovědy k existujícímu projektu</span><span class="sxs-lookup"><span data-stu-id="2a794-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="2a794-130">Stránky nápovědy k existujícímu projektu webového rozhraní API můžete přidat pomocí Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="2a794-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="2a794-131">Tato možnost je užitečná, že spusťte ze šablony jiný projekt než má šablona "Webového rozhraní API".</span><span class="sxs-lookup"><span data-stu-id="2a794-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="2a794-132">Z **nástroje** nabídce vyberte možnost **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="2a794-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="2a794-133">V [Konzola správce balíčků](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) okno, zadejte jeden z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="2a794-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="2a794-134">Pro **jazyka C#** aplikace: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="2a794-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="2a794-135">Pro **jazyka Visual Basic** aplikace: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="2a794-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="2a794-136">Existují dva balíčky, jeden pro jazyk C# a jeden pro jazyk Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="2a794-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="2a794-137">Ujistěte se, že chcete používat ten, který odpovídá projektu.</span><span class="sxs-lookup"><span data-stu-id="2a794-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="2a794-138">Tento příkaz nainstaluje potřebná sestavení a přidá zobrazení MVC pro stránky nápovědy (umístěný ve složce plochy/HelpPage).</span><span class="sxs-lookup"><span data-stu-id="2a794-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="2a794-139">Bude potřeba ručně přidat odkaz na stránku nápovědy.</span><span class="sxs-lookup"><span data-stu-id="2a794-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="2a794-140">Identifikátor URI je/help.</span><span class="sxs-lookup"><span data-stu-id="2a794-140">The URI is /Help.</span></span> <span data-ttu-id="2a794-141">Pokud chcete vytvořit odkaz v zobrazení razor, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="2a794-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="2a794-142">Také ujistěte se, že k registraci oblasti.</span><span class="sxs-lookup"><span data-stu-id="2a794-142">Also, make sure to register areas.</span></span> <span data-ttu-id="2a794-143">V souboru Global.asax přidejte následující kód, který **aplikace\_Start** metodu, pokud tam není již:</span><span class="sxs-lookup"><span data-stu-id="2a794-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="2a794-144">Přidání dokumentace k rozhraní API</span><span class="sxs-lookup"><span data-stu-id="2a794-144">Adding API Documentation</span></span>

<span data-ttu-id="2a794-145">Ve výchozím nastavení, v nápovědě stránky obsahují zástupný text řetězce pro dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="2a794-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="2a794-146">Můžete použít [dokumentační komentáře XML](https://msdn.microsoft.com/library/b2s063f7.aspx) vytvořit v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="2a794-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="2a794-147">Chcete-li tuto funkci povolit, otevřete soubor oblasti nebo HelpPage/aplikace\_Start/HelpPageConfig.cs a zrušte komentář u následujícího řádku:</span><span class="sxs-lookup"><span data-stu-id="2a794-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="2a794-148">Nyní povolte dokumentace XML.</span><span class="sxs-lookup"><span data-stu-id="2a794-148">Now enable XML documentation.</span></span> <span data-ttu-id="2a794-149">V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="2a794-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="2a794-150">Vyberte **sestavení** stránky.</span><span class="sxs-lookup"><span data-stu-id="2a794-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="2a794-151">V části **výstup**, zkontrolujte **soubor dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="2a794-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="2a794-152">Do textového pole zadejte "aplikace\_Data/XmlDocument.xml".</span><span class="sxs-lookup"><span data-stu-id="2a794-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="2a794-153">Dále otevřete kód `ValuesController` kontroleru rozhraní API, která je definována v /Controllers/ValuesController.cs.</span><span class="sxs-lookup"><span data-stu-id="2a794-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="2a794-154">Přidáte nějaké komentáře k dokumentaci pro metody kontroleru.</span><span class="sxs-lookup"><span data-stu-id="2a794-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="2a794-155">Příklad:</span><span class="sxs-lookup"><span data-stu-id="2a794-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="2a794-156">Tip: Pokud umístění blikající kurzor na řádek nad metodu a zadejte tři lomítka, sada Visual Studio automaticky vloží elementů XML.</span><span class="sxs-lookup"><span data-stu-id="2a794-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="2a794-157">Potom můžete vyplnit prázdné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="2a794-157">Then you can fill in the blanks.</span></span>


<span data-ttu-id="2a794-158">Nyní vytvářet a spusťte aplikaci znovu a přejděte na stránky nápovědy.</span><span class="sxs-lookup"><span data-stu-id="2a794-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="2a794-159">Dokumentace ke službě řetězce by se zobrazit v tabulce rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="2a794-160">Na stránce nápovědy přečte řetězce ze souboru XML v době běhu.</span><span class="sxs-lookup"><span data-stu-id="2a794-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="2a794-161">(Když nasadíte aplikaci, ujistěte se, že k nasazení souboru XML.)</span><span class="sxs-lookup"><span data-stu-id="2a794-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="2a794-162">Pohled pod kapotu</span><span class="sxs-lookup"><span data-stu-id="2a794-162">Under the Hood</span></span>

<span data-ttu-id="2a794-163">Stránky nápovědy jsou zabudovány nad **ApiExplorer** třídu, která je součástí rozhraní Web API.</span><span class="sxs-lookup"><span data-stu-id="2a794-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="2a794-164">**ApiExplorer** třída poskytuje suroviny pro vytvoření stránky nápovědy.</span><span class="sxs-lookup"><span data-stu-id="2a794-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="2a794-165">Pro každé rozhraní API **ApiExplorer** obsahuje **ApiDescription** popisující rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="2a794-166">V tomto případě "API" je definován jako kombinace relativní URI a metodou HTTP.</span><span class="sxs-lookup"><span data-stu-id="2a794-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="2a794-167">Například tady jsou některé různá rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="2a794-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="2a794-168">ZÍSKAT /api/Products</span><span class="sxs-lookup"><span data-stu-id="2a794-168">GET /api/Products</span></span>
- <span data-ttu-id="2a794-169">ZÍSKAT/webové rozhraní API/produkty / {id}</span><span class="sxs-lookup"><span data-stu-id="2a794-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="2a794-170">Publikovat/api/produkty</span><span class="sxs-lookup"><span data-stu-id="2a794-170">POST /api/Products</span></span>

<span data-ttu-id="2a794-171">Pokud je akce kontroleru podporuje více metod HTTP, **ApiExplorer** považuje každá metoda různých rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="2a794-172">Skrýt rozhraní API z **ApiExplorer**, přidejte **ApiExplorerSettings** akce a nastavte atribut *IgnoreApi* na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="2a794-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="2a794-173">Můžete také přidat tento atribut na řadič, vyloučit celý kontroler.</span><span class="sxs-lookup"><span data-stu-id="2a794-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="2a794-174">Třída ApiExplorer získá dokumentaci řetězců z **IDocumentationProvider** rozhraní.</span><span class="sxs-lookup"><span data-stu-id="2a794-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="2a794-175">Jak jste viděli již dříve, poskytuje knihovna stránky nápovědy **IDocumentationProvider** , který získá dokumentaci z řetězců dokumentaci XML.</span><span class="sxs-lookup"><span data-stu-id="2a794-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="2a794-176">Kód se nachází v /Areas/HelpPage/XmlDocumentationProvider.cs.</span><span class="sxs-lookup"><span data-stu-id="2a794-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="2a794-177">Můžete získat dokumentaci z jiného zdroje napsáním vlastní **IDocumentationProvider**.</span><span class="sxs-lookup"><span data-stu-id="2a794-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="2a794-178">Chcete-li ji nastavit, zavolejte **SetDocumentationProvider** metody rozšíření definované v **HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="2a794-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="2a794-179">**ApiExplorer** automaticky zavolá **IDocumentationProvider** rozhraní pro získání dokumentace řetězce pro každé rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2a794-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="2a794-180">Ukládá je v **dokumentaci** vlastnost **ApiDescription** a **ApiParameterDescription** objekty.</span><span class="sxs-lookup"><span data-stu-id="2a794-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a794-181">Další kroky</span><span class="sxs-lookup"><span data-stu-id="2a794-181">Next Steps</span></span>

<span data-ttu-id="2a794-182">Nejste omezeni na stránky nápovědy je vidět tady.</span><span class="sxs-lookup"><span data-stu-id="2a794-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="2a794-183">Ve skutečnosti **ApiExplorer** není omezena pouze na vytváření stránek nápovědy.</span><span class="sxs-lookup"><span data-stu-id="2a794-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="2a794-184">Ty Huang Yao zapsala si že některé skvělé příspěvky najdete, vám uvažujete úprav:</span><span class="sxs-lookup"><span data-stu-id="2a794-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="2a794-185">Přidání jednoduchého testovacího klienta stránka nápovědy k ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2a794-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="2a794-186">Vytváření technologie ASP.NET webové rozhraní API pomáhají stránky pracovat na služby v místním prostředí</span><span class="sxs-lookup"><span data-stu-id="2a794-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="2a794-187">Vytvoření v době návrhu nápovědy stránky (nebo klienta) pro rozhraní ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2a794-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="2a794-188">Rozšířená přizpůsobení stránce nápovědy</span><span class="sxs-lookup"><span data-stu-id="2a794-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
