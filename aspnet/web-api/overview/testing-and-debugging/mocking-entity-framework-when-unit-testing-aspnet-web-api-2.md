---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Napodobení Entity Framework při testování částí ASP.NET webového rozhraní API 2 | Microsoft Docs
author: Rick-Anderson
description: Tyto doprovodné materiály a aplikace ukazují, jak vytvořit testy částí pro aplikaci webového rozhraní API 2, která používá Entity Framework. Ukazuje, jak změnit...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555088"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="3ca3b-104">Napodobování Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3ca3b-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="3ca3b-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3ca3b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="3ca3b-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="3ca3b-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="3ca3b-107">Tyto doprovodné materiály a aplikace ukazují, jak vytvořit testy částí pro aplikaci webového rozhraní API 2, která používá Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="3ca3b-108">Ukazuje, jak upravit vygenerovaný řadič, aby bylo možné předat objekt kontextu pro testování a jak vytvořit objekty testu, které pracují s Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="3ca3b-109">Úvod do testování částí s webovým rozhraním API v ASP.NET najdete v tématu [testování částí s webovým rozhraním API 2 pro ASP.NET](unit-testing-with-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="3ca3b-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="3ca3b-110">V tomto kurzu se předpokládá, že jste obeznámeni se základními koncepty webového rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="3ca3b-111">Úvodní kurz najdete v tématu [Začínáme s webovým rozhraním API 2 pro ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="3ca3b-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3ca3b-112">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="3ca3b-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="3ca3b-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3ca3b-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="3ca3b-114">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="3ca3b-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="3ca3b-115">V tomto tématu</span><span class="sxs-lookup"><span data-stu-id="3ca3b-115">In this topic</span></span>

<span data-ttu-id="3ca3b-116">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="3ca3b-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="3ca3b-117">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3ca3b-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="3ca3b-118">Stáhnout kód</span><span class="sxs-lookup"><span data-stu-id="3ca3b-118">Download code</span></span>](#download)
- [<span data-ttu-id="3ca3b-119">Vytvořit aplikaci s projektem testování částí</span><span class="sxs-lookup"><span data-stu-id="3ca3b-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="3ca3b-120">Vytvoření třídy modelu</span><span class="sxs-lookup"><span data-stu-id="3ca3b-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="3ca3b-121">Přidání kontroleru</span><span class="sxs-lookup"><span data-stu-id="3ca3b-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="3ca3b-122">Přidat vkládání závislostí</span><span class="sxs-lookup"><span data-stu-id="3ca3b-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="3ca3b-123">Nainstalovat balíčky NuGet do projektu testů</span><span class="sxs-lookup"><span data-stu-id="3ca3b-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="3ca3b-124">Vytvořit kontext testu</span><span class="sxs-lookup"><span data-stu-id="3ca3b-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="3ca3b-125">Vytváření testů</span><span class="sxs-lookup"><span data-stu-id="3ca3b-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="3ca3b-126">Spustit testy</span><span class="sxs-lookup"><span data-stu-id="3ca3b-126">Run tests</span></span>](#runtests)

<span data-ttu-id="3ca3b-127">Pokud jste již dokončili kroky při [testování částí s webovým rozhraním API 2 pro ASP.NET](unit-testing-with-aspnet-web-api.md), můžete přejít k části [Přidání kontroleru](#controller).</span><span class="sxs-lookup"><span data-stu-id="3ca3b-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="3ca3b-128">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="3ca3b-128">Prerequisites</span></span>

<span data-ttu-id="3ca3b-129">Visual Studio 2017 Community, Professional nebo Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="3ca3b-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="3ca3b-130">Stažení kódu</span><span class="sxs-lookup"><span data-stu-id="3ca3b-130">Download code</span></span>

<span data-ttu-id="3ca3b-131">Stáhněte [dokončený projekt](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span><span class="sxs-lookup"><span data-stu-id="3ca3b-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="3ca3b-132">Projekt ke stažení obsahuje kód jednotkového testu pro toto téma a téma [testování částí ASP.NET webového rozhraní API 2](unit-testing-with-aspnet-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="3ca3b-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="3ca3b-133">Vytvořit aplikaci s projektem testování částí</span><span class="sxs-lookup"><span data-stu-id="3ca3b-133">Create application with unit test project</span></span>

<span data-ttu-id="3ca3b-134">Můžete buď vytvořit projekt testování částí při vytváření aplikace, nebo přidat projekt testování částí do existující aplikace.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="3ca3b-135">V tomto kurzu se dozvíte, jak vytvořit projekt testování částí při vytváření aplikace.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="3ca3b-136">Vytvořte novou webovou aplikaci v ASP.NET s názvem **StoreApp**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="3ca3b-137">V okně Nová okna projektu ASP.NET vyberte **prázdnou** šablonu a přidejte složky a základní odkazy pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="3ca3b-138">Vyberte možnost **Přidat testy jednotek** .</span><span class="sxs-lookup"><span data-stu-id="3ca3b-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="3ca3b-139">Projekt testu jednotek je automaticky pojmenován **StoreApp. Tests**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="3ca3b-140">Tento název můžete zachovat.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-140">You can keep this name.</span></span>

![vytvořit projekt testu jednotek](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="3ca3b-142">Po vytvoření aplikace uvidíte, že obsahuje dva projekty – **StoreApp** a **StoreApp. Tests**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="3ca3b-143">Vytvoření třídy modelu</span><span class="sxs-lookup"><span data-stu-id="3ca3b-143">Create the model class</span></span>

<span data-ttu-id="3ca3b-144">V projektu StoreApp přidejte soubor třídy do složky **modely** s názvem **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="3ca3b-145">Obsah souboru nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="3ca3b-146">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="3ca3b-147">Přidání kontroleru</span><span class="sxs-lookup"><span data-stu-id="3ca3b-147">Add the controller</span></span>

<span data-ttu-id="3ca3b-148">Klikněte pravým tlačítkem na složku řadiče a vyberte **Přidat** a **Nová vygenerovaná položka**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="3ca3b-149">Pomocí Entity Framework vyberte kontroler webového rozhraní API 2 s akcemi.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![Přidat nový kontroler](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="3ca3b-151">Nastavte následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="3ca3b-151">Set the following values:</span></span>

- <span data-ttu-id="3ca3b-152">Název kontroleru: **ProductController**</span><span class="sxs-lookup"><span data-stu-id="3ca3b-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="3ca3b-153">Třída modelu: **produkt**</span><span class="sxs-lookup"><span data-stu-id="3ca3b-153">Model class: **Product**</span></span>
- <span data-ttu-id="3ca3b-154">Třída kontextu dat: [vybrat **nový kontext dat** , který vyplní hodnoty zobrazené níže]</span><span class="sxs-lookup"><span data-stu-id="3ca3b-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![zadat kontroler](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="3ca3b-156">Kliknutím na **Přidat** vytvořte kontroler s automaticky generovaným kódem.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="3ca3b-157">Kód obsahuje metody pro vytváření, načítání, aktualizaci a odstraňování instancí třídy produktu.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="3ca3b-158">Následující kód ukazuje metodu pro přidání produktu.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="3ca3b-159">Všimněte si, že metoda vrací instanci třídy **IHttpActionResult**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="3ca3b-160">IHttpActionResult je jednou z nových funkcí webového rozhraní API 2 a zjednodušuje vývoj testů jednotek.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="3ca3b-161">V další části budete přizpůsobovat generovaný kód pro usnadnění předávání testovacích objektů do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="3ca3b-162">Přidat vkládání závislostí</span><span class="sxs-lookup"><span data-stu-id="3ca3b-162">Add dependency injection</span></span>

<span data-ttu-id="3ca3b-163">V současné době je třída ProductController pevně kódovaná pro použití instance třídy StoreAppContext.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="3ca3b-164">K úpravě aplikace a odstranění této pevně zakódované závislosti použijete vzor nazvaný injektáže závislosti.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="3ca3b-165">Přerušením této závislosti můžete předat objekt objektu k testování.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="3ca3b-166">Klikněte pravým tlačítkem na složku **modely** a přidejte nové rozhraní s názvem **IStoreAppContext**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="3ca3b-167">Nahraďte kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="3ca3b-168">Otevřete soubor StoreAppContext.cs a udělejte následující zvýrazněné změny.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="3ca3b-169">Důležité změny, které se mají poznamenat:</span><span class="sxs-lookup"><span data-stu-id="3ca3b-169">The important changes to note are:</span></span>

- <span data-ttu-id="3ca3b-170">Třída StoreAppContext implementuje rozhraní IStoreAppContext.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="3ca3b-171">Metoda MarkAsModified je implementovaná.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="3ca3b-172">Otevřete soubor ProductController.cs.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="3ca3b-173">Změňte existující kód tak, aby odpovídal zvýrazněnému kódu.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="3ca3b-174">Tyto změny ruší závislost na StoreAppContext a povolují ostatním třídám předat jiný objekt pro třídu kontextu.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="3ca3b-175">Tato změna vám umožní předat kontext testu během testování částí.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="3ca3b-176">V ProductController je potřeba udělat ještě jednu změnu.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="3ca3b-177">V metodě **PutProduct** nahraďte řádek, který nastaví stav entity na hodnotu změněno, voláním metody MarkAsModified.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="3ca3b-178">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-178">Build the solution.</span></span>

<span data-ttu-id="3ca3b-179">Nyní jste připraveni k nastavení testovacího projektu.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="3ca3b-180">Nainstalovat balíčky NuGet do projektu testů</span><span class="sxs-lookup"><span data-stu-id="3ca3b-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="3ca3b-181">Použijete-li prázdnou šablonu k vytvoření aplikace, projekt testu jednotek (StoreApp. Tests) neobsahuje žádné nainstalované balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="3ca3b-182">Jiné šablony, jako je například šablona webového rozhraní API, obsahují některé balíčky NuGet v projektu testování částí.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="3ca3b-183">Pro tento kurz musíte zahrnout balíček Entity Framework a balíček Microsoft ASP.NET Web API 2 Core do projektu testů.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="3ca3b-184">Klikněte pravým tlačítkem na projekt StoreApp. Tests a vyberte možnost **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="3ca3b-185">Chcete-li přidat balíčky do projektu, je nutné vybrat projekt StoreApp. Tests.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![spravovat balíčky](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="3ca3b-187">V online balíčcích vyhledejte a nainstalujte balíček EntityFramework (verze 6,0 nebo novější).</span><span class="sxs-lookup"><span data-stu-id="3ca3b-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="3ca3b-188">Pokud se zdá, že balíček EntityFramework je již nainstalován, jste pravděpodobně vybrali projekt StoreApp namísto projektu StoreApp. Tests.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![Přidat Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="3ca3b-190">Najděte a nainstalujte balíček Microsoft ASP.NET webového rozhraní API 2 Core.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![nainstalovat balíček webového rozhraní API Core](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="3ca3b-192">Zavřete okno Spravovat balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="3ca3b-193">Vytvořit kontext testu</span><span class="sxs-lookup"><span data-stu-id="3ca3b-193">Create test context</span></span>

<span data-ttu-id="3ca3b-194">Do testovacího projektu přidejte třídu s názvem **TestDbSet** .</span><span class="sxs-lookup"><span data-stu-id="3ca3b-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="3ca3b-195">Tato třída slouží jako základní třída pro sadu testovacích dat.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="3ca3b-196">Nahraďte kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="3ca3b-197">Přidejte třídu s názvem **TestProductDbSet** do testovacího projektu, který obsahuje následující kód.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="3ca3b-198">Přidejte třídu s názvem **TestStoreAppContext** a nahraďte existující kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="3ca3b-199">Vytváření testů</span><span class="sxs-lookup"><span data-stu-id="3ca3b-199">Create tests</span></span>

<span data-ttu-id="3ca3b-200">Ve výchozím nastavení obsahuje projekt testů prázdný testovací soubor s názvem **UnitTest1.cs**.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="3ca3b-201">Tento soubor zobrazuje atributy, které použijete k vytvoření testovacích metod.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="3ca3b-202">Pro tento kurz můžete tento soubor odstranit, protože budete přidávat novou testovací třídu.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="3ca3b-203">Do testovacího projektu přidejte třídu s názvem **TestProductController** .</span><span class="sxs-lookup"><span data-stu-id="3ca3b-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="3ca3b-204">Nahraďte kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="3ca3b-205">Spouštění testů</span><span class="sxs-lookup"><span data-stu-id="3ca3b-205">Run tests</span></span>

<span data-ttu-id="3ca3b-206">Nyní jste připraveni spustit testy.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-206">You are now ready to run the tests.</span></span> <span data-ttu-id="3ca3b-207">Všechny metody, které jsou označeny atributem **TestMethod** , budou testovány.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="3ca3b-208">Z položky nabídky **test** spusťte testy.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-208">From the **Test** menu item, run the tests.</span></span>

![Provádění testů](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="3ca3b-210">Otevřete okno **Průzkumník testů** a Všimněte si výsledků testů.</span><span class="sxs-lookup"><span data-stu-id="3ca3b-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![výsledky testu](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
