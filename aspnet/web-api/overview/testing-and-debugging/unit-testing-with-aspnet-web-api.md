---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: Testování částí ASP.NET webového rozhraní API 2 | Microsoft Docs
author: Rick-Anderson
description: Tyto doprovodné materiály a aplikace ukazují, jak vytvořit jednoduché testy částí pro aplikaci webového rozhraní API 2. Tento kurz ukazuje, jak zahrnout proj test jednotek...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554969"
---
# <a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="28b52-104">Testování částí ASP.NET webového rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="28b52-104">Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="28b52-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="28b52-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="28b52-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="28b52-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="28b52-107">Tyto doprovodné materiály a aplikace ukazují, jak vytvořit jednoduché testy částí pro aplikaci webového rozhraní API 2.</span><span class="sxs-lookup"><span data-stu-id="28b52-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="28b52-108">V tomto kurzu se dozvíte, jak zahrnout projekt testování částí do řešení a zapsat testovací metody, které kontrolují vrácené hodnoty z metody kontroleru.</span><span class="sxs-lookup"><span data-stu-id="28b52-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
>
> <span data-ttu-id="28b52-109">V tomto kurzu se předpokládá, že jste obeznámeni se základními koncepty webového rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="28b52-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="28b52-110">Úvodní kurz najdete v tématu [Začínáme s webovým rozhraním API 2 pro ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="28b52-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> <span data-ttu-id="28b52-111">Testování částí v tomto tématu se úmyslně omezí na jednoduché scénáře dat.</span><span class="sxs-lookup"><span data-stu-id="28b52-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="28b52-112">V případě testování částí pokročilejších scénářů dat naleznete informace v tématu napodobování [Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="28b52-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="28b52-113">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="28b52-113">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="28b52-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="28b52-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="28b52-115">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="28b52-115">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="28b52-116">V tomto tématu</span><span class="sxs-lookup"><span data-stu-id="28b52-116">In this topic</span></span>

<span data-ttu-id="28b52-117">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="28b52-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="28b52-118">Požadavky</span><span class="sxs-lookup"><span data-stu-id="28b52-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="28b52-119">Stáhnout kód</span><span class="sxs-lookup"><span data-stu-id="28b52-119">Download code</span></span>](#download)
- [<span data-ttu-id="28b52-120">Vytvořit aplikaci s projektem testování částí</span><span class="sxs-lookup"><span data-stu-id="28b52-120">Create application with unit test project</span></span>](#appwithunittest)
    - [<span data-ttu-id="28b52-121">Přidat projekt testu jednotek při vytváření aplikace</span><span class="sxs-lookup"><span data-stu-id="28b52-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="28b52-122">Přidat projekt testu jednotek do existující aplikace</span><span class="sxs-lookup"><span data-stu-id="28b52-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="28b52-123">Nastavení aplikace webového rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="28b52-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="28b52-124">Nainstalovat balíčky NuGet do projektu testů</span><span class="sxs-lookup"><span data-stu-id="28b52-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="28b52-125">Vytváření testů</span><span class="sxs-lookup"><span data-stu-id="28b52-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="28b52-126">Spustit testy</span><span class="sxs-lookup"><span data-stu-id="28b52-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="28b52-127">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="28b52-127">Prerequisites</span></span>

<span data-ttu-id="28b52-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Komunita, edice Professional nebo Enterprise</span><span class="sxs-lookup"><span data-stu-id="28b52-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="28b52-129">Stažení kódu</span><span class="sxs-lookup"><span data-stu-id="28b52-129">Download code</span></span>

<span data-ttu-id="28b52-130">Stáhněte [dokončený projekt](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span><span class="sxs-lookup"><span data-stu-id="28b52-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="28b52-131">Projekt ke stažení obsahuje kód jednotkového testu pro toto téma a pro napodobení [Entity Framework při testování částí webového rozhraní API ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) .</span><span class="sxs-lookup"><span data-stu-id="28b52-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="28b52-132">Vytvořit aplikaci s projektem testování částí</span><span class="sxs-lookup"><span data-stu-id="28b52-132">Create application with unit test project</span></span>

<span data-ttu-id="28b52-133">Můžete buď vytvořit projekt testování částí při vytváření aplikace, nebo přidat projekt testování částí do existující aplikace.</span><span class="sxs-lookup"><span data-stu-id="28b52-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="28b52-134">Tento kurz ukazuje obě metody pro vytvoření projektu testování částí.</span><span class="sxs-lookup"><span data-stu-id="28b52-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="28b52-135">Pokud chcete postupovat podle tohoto kurzu, můžete použít libovolný přístup.</span><span class="sxs-lookup"><span data-stu-id="28b52-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="28b52-136">Přidat projekt testu jednotek při vytváření aplikace</span><span class="sxs-lookup"><span data-stu-id="28b52-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="28b52-137">Vytvořte novou webovou aplikaci v ASP.NET s názvem **StoreApp**.</span><span class="sxs-lookup"><span data-stu-id="28b52-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![vytvořit projekt](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="28b52-139">V okně Nová okna projektu ASP.NET vyberte **prázdnou** šablonu a přidejte složky a základní odkazy pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="28b52-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="28b52-140">Vyberte možnost **Přidat testy jednotek** .</span><span class="sxs-lookup"><span data-stu-id="28b52-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="28b52-141">Projekt testu jednotek je automaticky pojmenován **StoreApp. Tests**.</span><span class="sxs-lookup"><span data-stu-id="28b52-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="28b52-142">Tento název můžete zachovat.</span><span class="sxs-lookup"><span data-stu-id="28b52-142">You can keep this name.</span></span>

![vytvořit projekt testu jednotek](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="28b52-144">Po vytvoření aplikace se zobrazí, že obsahuje dva projekty.</span><span class="sxs-lookup"><span data-stu-id="28b52-144">After creating the application, you will see it contains two projects.</span></span>

![dva projekty](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="28b52-146">Přidat projekt testu jednotek do existující aplikace</span><span class="sxs-lookup"><span data-stu-id="28b52-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="28b52-147">Pokud jste při vytváření aplikace nevytvořili projekt testu jednotek, můžete ho kdykoli přidat.</span><span class="sxs-lookup"><span data-stu-id="28b52-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="28b52-148">Předpokládejme například, že již máte aplikaci s názvem StoreApp a chcete přidat jednotkové testy.</span><span class="sxs-lookup"><span data-stu-id="28b52-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="28b52-149">Chcete-li přidat projekt testování částí, klikněte pravým tlačítkem na řešení a vyberte možnost **Přidat** a **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="28b52-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![Přidat nový projekt do řešení](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="28b52-151">V levém podokně vyberte **test** a pro typ projektu vyberte **projekt testování částí** .</span><span class="sxs-lookup"><span data-stu-id="28b52-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="28b52-152">Pojmenujte projekt **StoreApp. Tests**.</span><span class="sxs-lookup"><span data-stu-id="28b52-152">Name the project **StoreApp.Tests**.</span></span>

![Přidat projekt testu jednotek](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="28b52-154">Ve vašem řešení se zobrazí projekt testování částí.</span><span class="sxs-lookup"><span data-stu-id="28b52-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="28b52-155">V projektu testování jednotky přidejte odkaz na projekt do původního projektu.</span><span class="sxs-lookup"><span data-stu-id="28b52-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="28b52-156">Nastavení aplikace webového rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="28b52-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="28b52-157">V projektu StoreApp přidejte soubor třídy do složky **modely** s názvem **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="28b52-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="28b52-158">Obsah souboru nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="28b52-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="28b52-159">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="28b52-159">Build the solution.</span></span>

<span data-ttu-id="28b52-160">Klikněte pravým tlačítkem na složku řadiče a vyberte **Přidat** a **Nová vygenerovaná položka**.</span><span class="sxs-lookup"><span data-stu-id="28b52-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="28b52-161">Vyberte **kontroler webového rozhraní API 2 – prázdné**.</span><span class="sxs-lookup"><span data-stu-id="28b52-161">Select **Web API 2 Controller - Empty**.</span></span>

![Přidat nový kontroler](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="28b52-163">Nastavte název kontroleru na **SimpleProductController**a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="28b52-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![zadat kontroler](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="28b52-165">Nahraďte existující kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="28b52-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="28b52-166">Pro zjednodušení tohoto příkladu jsou data uložena v seznamu, nikoli v databázi.</span><span class="sxs-lookup"><span data-stu-id="28b52-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="28b52-167">Seznam definovaný v této třídě představuje produkční data.</span><span class="sxs-lookup"><span data-stu-id="28b52-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="28b52-168">Všimněte si, že kontroler zahrnuje konstruktor, který přebírá jako parametr seznam objektů produktu.</span><span class="sxs-lookup"><span data-stu-id="28b52-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="28b52-169">Tento konstruktor umožňuje předat testovací data při testování jednotky.</span><span class="sxs-lookup"><span data-stu-id="28b52-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="28b52-170">Kontroler také obsahuje dvě **asynchronní** metody pro ilustraci asynchronních metod testování částí.</span><span class="sxs-lookup"><span data-stu-id="28b52-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="28b52-171">Tyto asynchronní metody byly implementovány voláním **Task. FromResult** pro minimalizaci nadbytečného kódu, ale obvykle by metody zahrnovaly operace náročné na prostředky.</span><span class="sxs-lookup"><span data-stu-id="28b52-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="28b52-172">Metoda getproduct vrátí instanci rozhraní **IHttpActionResult** .</span><span class="sxs-lookup"><span data-stu-id="28b52-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="28b52-173">IHttpActionResult je jednou z nových funkcí webového rozhraní API 2 a zjednodušuje vývoj testů jednotek.</span><span class="sxs-lookup"><span data-stu-id="28b52-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="28b52-174">Třídy, které implementují rozhraní IHttpActionResult, se nacházejí v oboru názvů [System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) .</span><span class="sxs-lookup"><span data-stu-id="28b52-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="28b52-175">Tyto třídy reprezentují možné odezvy z požadavku akce a odpovídají stavovým kódům HTTP.</span><span class="sxs-lookup"><span data-stu-id="28b52-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="28b52-176">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="28b52-176">Build the solution.</span></span>

<span data-ttu-id="28b52-177">Nyní jste připraveni k nastavení testovacího projektu.</span><span class="sxs-lookup"><span data-stu-id="28b52-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="28b52-178">Nainstalovat balíčky NuGet do projektu testů</span><span class="sxs-lookup"><span data-stu-id="28b52-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="28b52-179">Použijete-li prázdnou šablonu k vytvoření aplikace, projekt testu jednotek (StoreApp. Tests) neobsahuje žádné nainstalované balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="28b52-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="28b52-180">Jiné šablony, jako je například šablona webového rozhraní API, obsahují některé balíčky NuGet v projektu testování částí.</span><span class="sxs-lookup"><span data-stu-id="28b52-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="28b52-181">Pro tento kurz musíte do testovacího projektu zahrnout balíček Microsoft ASP.NET Web API 2 Core.</span><span class="sxs-lookup"><span data-stu-id="28b52-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="28b52-182">Klikněte pravým tlačítkem na projekt StoreApp. Tests a vyberte možnost **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="28b52-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="28b52-183">Chcete-li přidat balíčky do projektu, je nutné vybrat projekt StoreApp. Tests.</span><span class="sxs-lookup"><span data-stu-id="28b52-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![spravovat balíčky](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="28b52-185">Najděte a nainstalujte balíček Microsoft ASP.NET webového rozhraní API 2 Core.</span><span class="sxs-lookup"><span data-stu-id="28b52-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![nainstalovat balíček webového rozhraní API Core](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="28b52-187">Zavřete okno Spravovat balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="28b52-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="28b52-188">Vytváření testů</span><span class="sxs-lookup"><span data-stu-id="28b52-188">Create tests</span></span>

<span data-ttu-id="28b52-189">Ve výchozím nastavení obsahuje projekt testů prázdný testovací soubor s názvem UnitTest1.cs.</span><span class="sxs-lookup"><span data-stu-id="28b52-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="28b52-190">Tento soubor zobrazuje atributy, které použijete k vytvoření testovacích metod.</span><span class="sxs-lookup"><span data-stu-id="28b52-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="28b52-191">Pro testování částí můžete použít tento soubor nebo vytvořit vlastní soubor.</span><span class="sxs-lookup"><span data-stu-id="28b52-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="28b52-193">Pro tento kurz vytvoříte vlastní testovací třídu.</span><span class="sxs-lookup"><span data-stu-id="28b52-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="28b52-194">Soubor UnitTest1.cs můžete odstranit.</span><span class="sxs-lookup"><span data-stu-id="28b52-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="28b52-195">Přidejte třídu s názvem **TestSimpleProductController.cs**a nahraďte kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="28b52-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="28b52-196">Spouštění testů</span><span class="sxs-lookup"><span data-stu-id="28b52-196">Run tests</span></span>

<span data-ttu-id="28b52-197">Nyní jste připraveni spustit testy.</span><span class="sxs-lookup"><span data-stu-id="28b52-197">You are now ready to run the tests.</span></span> <span data-ttu-id="28b52-198">Všechny metody, které jsou označeny atributem **TestMethod** , budou testovány.</span><span class="sxs-lookup"><span data-stu-id="28b52-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="28b52-199">Z položky nabídky **test** spusťte testy.</span><span class="sxs-lookup"><span data-stu-id="28b52-199">From the **Test** menu item, run the tests.</span></span>

![Provádění testů](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="28b52-201">Otevřete okno **Průzkumník testů** a Všimněte si výsledků testů.</span><span class="sxs-lookup"><span data-stu-id="28b52-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![výsledky testu](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="28b52-203">Souhrn</span><span class="sxs-lookup"><span data-stu-id="28b52-203">Summary</span></span>

<span data-ttu-id="28b52-204">Dokončili jste tento kurz.</span><span class="sxs-lookup"><span data-stu-id="28b52-204">You have completed this tutorial.</span></span> <span data-ttu-id="28b52-205">Data v tomto kurzu se záměrně zjednodušila a zaměřuje se na podmínky testování částí.</span><span class="sxs-lookup"><span data-stu-id="28b52-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="28b52-206">V případě testování částí pokročilejších scénářů dat naleznete informace v tématu napodobování [Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="28b52-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
