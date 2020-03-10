---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: Vytvoření koncového bodu OData v4 pomocí webového rozhraní API ASP.NET 2,2 | Microsoft Docs
author: MikeWasson
description: Protokol OData (Open Data Protocol) je protokol pro přístup k datům pro web. OData poskytuje jednotný způsob dotazování a manipulace s datovými sadami prostřednictvím operací CRUD...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598733"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="cca6c-104">Vytvoření koncového bodu OData v4 pomocí webového rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cca6c-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="cca6c-105">Protokol OData (Open Data Protocol) je protokol pro přístup k datům pro web.</span><span class="sxs-lookup"><span data-stu-id="cca6c-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="cca6c-106">OData poskytuje jednotný způsob dotazování a manipulace s datovými sadami prostřednictvím operací CRUD (vytvoření, čtení, aktualizace a odstranění).</span><span class="sxs-lookup"><span data-stu-id="cca6c-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="cca6c-107">Webové rozhraní API ASP.NET podporuje V3 i v4 protokolu.</span><span class="sxs-lookup"><span data-stu-id="cca6c-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="cca6c-108">Můžete dokonce i koncový bod v4, který běží souběžně s koncovým bodem v3.</span><span class="sxs-lookup"><span data-stu-id="cca6c-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="cca6c-109">V tomto kurzu se dozvíte, jak vytvořit koncový bod OData v4, který podporuje operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="cca6c-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cca6c-110">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="cca6c-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="cca6c-111">Webové rozhraní API 5,2</span><span class="sxs-lookup"><span data-stu-id="cca6c-111">Web API 5.2</span></span>
> - <span data-ttu-id="cca6c-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="cca6c-112">OData v4</span></span>
> - <span data-ttu-id="cca6c-113">Visual Studio 2017 ( [tady si můžete](https://visualstudio.microsoft.com/downloads/)stáhnout visual Studio 2017)</span><span class="sxs-lookup"><span data-stu-id="cca6c-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="cca6c-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="cca6c-114">Entity Framework 6</span></span>
> - <span data-ttu-id="cca6c-115">.NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="cca6c-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="cca6c-116">Verze kurzů</span><span class="sxs-lookup"><span data-stu-id="cca6c-116">Tutorial versions</span></span>
>
> <span data-ttu-id="cca6c-117">Informace o OData verze 3 najdete v tématu [Vytvoření koncového bodu OData V3](../odata-v3/creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="cca6c-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="cca6c-118">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cca6c-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="cca6c-119">V aplikaci Visual Studio v nabídce **soubor** vyberte **Nový** &gt; **projekt**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="cca6c-120">Rozbalte položku **nainstalované** &gt;  **C# Visual** &gt; **Web**a vyberte šablonu **Webová aplikace ASP.NET (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="cca6c-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="cca6c-121">Pojmenujte projekt &quot;ProductService&quot;.</span><span class="sxs-lookup"><span data-stu-id="cca6c-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="cca6c-122">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-122">Select **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="cca6c-123">Vyberte **prázdnou** šablonu.</span><span class="sxs-lookup"><span data-stu-id="cca6c-123">Select the **Empty** template.</span></span> <span data-ttu-id="cca6c-124">V části **Přidat složky a základní reference pro:** vyberte **webové rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="cca6c-125">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="cca6c-126">Instalace balíčků OData</span><span class="sxs-lookup"><span data-stu-id="cca6c-126">Install the OData packages</span></span>

<span data-ttu-id="cca6c-127">V nabídce **nástroje** vyberte **správce balíčků NuGet** &gt; **konzolu Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="cca6c-128">V okně konzoly Správce balíčků zadejte:</span><span class="sxs-lookup"><span data-stu-id="cca6c-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="cca6c-129">Tento příkaz nainstaluje nejnovější balíčky NuGet pro OData.</span><span class="sxs-lookup"><span data-stu-id="cca6c-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="cca6c-130">Přidejte třídu modelu</span><span class="sxs-lookup"><span data-stu-id="cca6c-130">Add a model class</span></span>

<span data-ttu-id="cca6c-131">*Model* je objekt, který představuje datovou entitu v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="cca6c-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="cca6c-132">V Průzkumník řešení klikněte pravým tlačítkem na složku modely.</span><span class="sxs-lookup"><span data-stu-id="cca6c-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="cca6c-133">V místní nabídce vyberte **přidat** &gt; **třídy**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="cca6c-134">Podle konvence jsou třídy modelu umístěny do složky modelů, ale nemusíte postupovat podle této konvence ve svých vlastních projektech.</span><span class="sxs-lookup"><span data-stu-id="cca6c-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>

<span data-ttu-id="cca6c-135">Pojmenujte `Product`třídy.</span><span class="sxs-lookup"><span data-stu-id="cca6c-135">Name the class `Product`.</span></span> <span data-ttu-id="cca6c-136">V souboru Product.cs nahraďte často používaný kód následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="cca6c-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="cca6c-137">Vlastnost `Id` je klíč entity.</span><span class="sxs-lookup"><span data-stu-id="cca6c-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="cca6c-138">Klienti můžou zadávat dotazy na entity podle klíče.</span><span class="sxs-lookup"><span data-stu-id="cca6c-138">Clients can query entities by key.</span></span> <span data-ttu-id="cca6c-139">Chcete-li například získat produkt s ID 5, je identifikátor URI `/Products(5)`.</span><span class="sxs-lookup"><span data-stu-id="cca6c-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="cca6c-140">Vlastnost `Id` bude také primárním klíčem v back-endové databázi.</span><span class="sxs-lookup"><span data-stu-id="cca6c-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="cca6c-141">Povolit Entity Framework</span><span class="sxs-lookup"><span data-stu-id="cca6c-141">Enable Entity Framework</span></span>

<span data-ttu-id="cca6c-142">V tomto kurzu použijeme Entity Framework (EF) Code First k vytvoření back-endové databáze.</span><span class="sxs-lookup"><span data-stu-id="cca6c-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="cca6c-143">Rozhraní Web API OData nevyžaduje EF.</span><span class="sxs-lookup"><span data-stu-id="cca6c-143">Web API OData does not require EF.</span></span> <span data-ttu-id="cca6c-144">Použijte jakoukoli vrstvu přístupu k datům, která dokáže překládat databázové entity do modelů.</span><span class="sxs-lookup"><span data-stu-id="cca6c-144">Use any data-access layer that can translate database entities into models.</span></span>

<span data-ttu-id="cca6c-145">Nejdřív nainstalujte balíček NuGet pro EF.</span><span class="sxs-lookup"><span data-stu-id="cca6c-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="cca6c-146">V nabídce **nástroje** vyberte **správce balíčků NuGet** &gt; **konzolu Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="cca6c-147">V okně konzoly Správce balíčků zadejte:</span><span class="sxs-lookup"><span data-stu-id="cca6c-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="cca6c-148">Otevřete soubor Web. config a přidejte následující oddíl do **konfiguračního** elementu za prvek **configSections** .</span><span class="sxs-lookup"><span data-stu-id="cca6c-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="cca6c-149">Toto nastavení přidá připojovací řetězec pro databázi LocalDB.</span><span class="sxs-lookup"><span data-stu-id="cca6c-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="cca6c-150">Tato databáze se použije, když aplikaci spouštíte místně.</span><span class="sxs-lookup"><span data-stu-id="cca6c-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="cca6c-151">Dále do složky modely přidejte třídu s názvem `ProductsContext`:</span><span class="sxs-lookup"><span data-stu-id="cca6c-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="cca6c-152">V konstruktoru `"name=ProductsContext"` poskytuje název připojovacího řetězce.</span><span class="sxs-lookup"><span data-stu-id="cca6c-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="cca6c-153">Konfigurace koncového bodu OData</span><span class="sxs-lookup"><span data-stu-id="cca6c-153">Configure the OData endpoint</span></span>

<span data-ttu-id="cca6c-154">Otevřete soubor App\_Start/WebApiConfig. cs.</span><span class="sxs-lookup"><span data-stu-id="cca6c-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="cca6c-155">Přidejte následující příkazy **using** :</span><span class="sxs-lookup"><span data-stu-id="cca6c-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="cca6c-156">Pak do metody **registru** přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="cca6c-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="cca6c-157">Tento kód provede dvě věci:</span><span class="sxs-lookup"><span data-stu-id="cca6c-157">This code does two things:</span></span>

- <span data-ttu-id="cca6c-158">Vytvoří model EDM (Entity Data Model) (EDM).</span><span class="sxs-lookup"><span data-stu-id="cca6c-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="cca6c-159">Přidá trasu.</span><span class="sxs-lookup"><span data-stu-id="cca6c-159">Adds a route.</span></span>

<span data-ttu-id="cca6c-160">EDM je abstraktní model dat.</span><span class="sxs-lookup"><span data-stu-id="cca6c-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="cca6c-161">Model EDM slouží k vytvoření dokumentu metadat služby.</span><span class="sxs-lookup"><span data-stu-id="cca6c-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="cca6c-162">Třída **ODataConventionModelBuilder** vytvoří EDM pomocí výchozích konvencí pojmenování.</span><span class="sxs-lookup"><span data-stu-id="cca6c-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="cca6c-163">Tento přístup vyžaduje nejméně kód.</span><span class="sxs-lookup"><span data-stu-id="cca6c-163">This approach requires the least code.</span></span> <span data-ttu-id="cca6c-164">Pokud chcete mít větší kontrolu nad modelem EDM, můžete pomocí třídy **ODataModelBuilder** vytvořit EDM přidáním vlastností, klíčů a vlastností navigace explicitně.</span><span class="sxs-lookup"><span data-stu-id="cca6c-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="cca6c-165">*Trasa* oznamuje webovému rozhraní API, jak SMĚROVAT požadavky HTTP na koncový bod.</span><span class="sxs-lookup"><span data-stu-id="cca6c-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="cca6c-166">Chcete-li vytvořit trasu OData v4, zavolejte metodu rozšíření **MapODataServiceRoute** .</span><span class="sxs-lookup"><span data-stu-id="cca6c-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="cca6c-167">Pokud má vaše aplikace více koncových bodů OData, vytvořte pro každou z nich samostatnou trasu.</span><span class="sxs-lookup"><span data-stu-id="cca6c-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="cca6c-168">Udělte každé trase jedinečný název a předponu trasy.</span><span class="sxs-lookup"><span data-stu-id="cca6c-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="cca6c-169">Přidat kontroler OData</span><span class="sxs-lookup"><span data-stu-id="cca6c-169">Add the OData controller</span></span>

<span data-ttu-id="cca6c-170">*Kontroler* je třída, která zpracovává požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="cca6c-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="cca6c-171">Pro každou sadu entit ve službě OData vytvoříte samostatný kontroler.</span><span class="sxs-lookup"><span data-stu-id="cca6c-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="cca6c-172">V tomto kurzu vytvoříte pro entitu `Product` jeden kontroler.</span><span class="sxs-lookup"><span data-stu-id="cca6c-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="cca6c-173">V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers a vyberte **přidat** &gt; **třídu**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="cca6c-174">Pojmenujte `ProductsController`třídy.</span><span class="sxs-lookup"><span data-stu-id="cca6c-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="cca6c-175">Verze tohoto kurzu pro OData V3 používá rozhraní **Add controllering** .</span><span class="sxs-lookup"><span data-stu-id="cca6c-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="cca6c-176">V současné době neexistuje pro OData v4 žádné generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cca6c-176">Currently, there is no scaffolding for OData v4.</span></span>

<span data-ttu-id="cca6c-177">Pomocí následujícího kódu nahraďte často používaný kód v ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="cca6c-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="cca6c-178">Řadič používá třídu `ProductsContext` pro přístup k databázi pomocí EF.</span><span class="sxs-lookup"><span data-stu-id="cca6c-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="cca6c-179">Všimněte si, že kontroler přepisuje metodu **Dispose** pro uvolnění **ProductsContext**.</span><span class="sxs-lookup"><span data-stu-id="cca6c-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="cca6c-180">Toto je výchozí bod pro kontroler.</span><span class="sxs-lookup"><span data-stu-id="cca6c-180">This is the starting point for the controller.</span></span> <span data-ttu-id="cca6c-181">Dále přidáme metody pro všechny operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="cca6c-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="cca6c-182">Dotazování sady entit</span><span class="sxs-lookup"><span data-stu-id="cca6c-182">Query the entity set</span></span>

<span data-ttu-id="cca6c-183">Přidejte následující metody pro `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="cca6c-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="cca6c-184">Verze `Get` metody bez parametrů vrací celou kolekci Products.</span><span class="sxs-lookup"><span data-stu-id="cca6c-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="cca6c-185">Metoda `Get` s parametrem *Key* vyhledává produkt podle jeho klíče (v tomto případě vlastnost `Id`).</span><span class="sxs-lookup"><span data-stu-id="cca6c-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="cca6c-186">Atribut **[EnableQuery]** umožňuje klientům upravit dotaz pomocí možností dotazu, jako je $filter, $sort a $Page.</span><span class="sxs-lookup"><span data-stu-id="cca6c-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="cca6c-187">Další informace najdete v tématu [Podpora možností dotazů OData](../supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="cca6c-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="cca6c-188">Přidat entitu do sady entit</span><span class="sxs-lookup"><span data-stu-id="cca6c-188">Add an entity to the entity set</span></span>

<span data-ttu-id="cca6c-189">Chcete-li povolit klientům přidat do databáze nový produkt, přidejte následující metodu pro `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="cca6c-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="cca6c-190">Aktualizace entity</span><span class="sxs-lookup"><span data-stu-id="cca6c-190">Update an entity</span></span>

<span data-ttu-id="cca6c-191">OData podporuje dvě odlišná sémantika pro aktualizaci entity, opravy a vložení.</span><span class="sxs-lookup"><span data-stu-id="cca6c-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="cca6c-192">Oprava provede částečnou aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="cca6c-192">PATCH performs a partial update.</span></span> <span data-ttu-id="cca6c-193">Klient Určuje pouze vlastnosti, které se mají aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="cca6c-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="cca6c-194">PUT nahradí celou entitu.</span><span class="sxs-lookup"><span data-stu-id="cca6c-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="cca6c-195">Nevýhodou PUT je, že klient musí odesílat hodnoty všech vlastností v entitě, včetně hodnot, které se nemění.</span><span class="sxs-lookup"><span data-stu-id="cca6c-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="cca6c-196">[Specifikace OData](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) uvádí, že oprava je upřednostňovaná.</span><span class="sxs-lookup"><span data-stu-id="cca6c-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="cca6c-197">V každém případě je zde uveden kód pro metodu PATCH i PUT:</span><span class="sxs-lookup"><span data-stu-id="cca6c-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="cca6c-198">V případě opravy používá kontroler **&gt;typu rozdíl&lt;t** ke sledování změn.</span><span class="sxs-lookup"><span data-stu-id="cca6c-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="cca6c-199">Odstranění entity</span><span class="sxs-lookup"><span data-stu-id="cca6c-199">Delete an entity</span></span>

<span data-ttu-id="cca6c-200">Chcete-li povolit klientům odstranit produkt z databáze nástroje, přidejte následující metodu pro `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="cca6c-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
