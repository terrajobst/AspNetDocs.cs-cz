---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: Povolení operací CRUD v ASP.NET Web API 1 – ASP.NET 4.x
author: MikeWasson
description: Kurz ukazuje, jak podporovat operace CRUD v rámci protokolu HTTP služby pomocí rozhraní ASP.NET Web API pro ASP.NET 4.x.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: 3c2a41482b7f9b60a8864b853df23ab5991b6da7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108732"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="81a08-103">Povolení operací CRUD v ASP.NET Web API 1</span><span class="sxs-lookup"><span data-stu-id="81a08-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="81a08-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="81a08-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="81a08-105">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="81a08-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="81a08-106">Tento kurz ukazuje, jak podporovat operace CRUD v rámci protokolu HTTP služby pomocí rozhraní ASP.NET Web API pro ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="81a08-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="81a08-107">V tomto kurzu použili verze softwaru</span><span class="sxs-lookup"><span data-stu-id="81a08-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="81a08-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="81a08-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="81a08-109">Webové rozhraní API 1 (také funguje s webovým rozhraním API 2)</span><span class="sxs-lookup"><span data-stu-id="81a08-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="81a08-110">Zastupuje CRUD &quot;vytvoření, čtení, aktualizace a odstraňování,&quot; jsou čtyři základní databázových operací.</span><span class="sxs-lookup"><span data-stu-id="81a08-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="81a08-111">Mnoho služeb HTTP taky model operace CRUD prostřednictvím REST nebo jako REST API.</span><span class="sxs-lookup"><span data-stu-id="81a08-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="81a08-112">V tomto kurzu vytvoříte velmi jednoduché webové rozhraní API ke správě seznamu produktů.</span><span class="sxs-lookup"><span data-stu-id="81a08-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="81a08-113">Každý produkt bude obsahovat název, cena a kategorie (například &quot;toys&quot; nebo &quot;hardwaru&quot;), plus ID produktu.</span><span class="sxs-lookup"><span data-stu-id="81a08-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="81a08-114">Produkty rozhraní API bude vystavovat následující metody.</span><span class="sxs-lookup"><span data-stu-id="81a08-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="81a08-115">Akce</span><span class="sxs-lookup"><span data-stu-id="81a08-115">Action</span></span> | <span data-ttu-id="81a08-116">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="81a08-116">HTTP method</span></span> | <span data-ttu-id="81a08-117">Relativní identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="81a08-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="81a08-118">Získání seznamu všech produktů</span><span class="sxs-lookup"><span data-stu-id="81a08-118">Get a list of all products</span></span> | <span data-ttu-id="81a08-119">GET</span><span class="sxs-lookup"><span data-stu-id="81a08-119">GET</span></span> | <span data-ttu-id="81a08-120">/ api/produkty</span><span class="sxs-lookup"><span data-stu-id="81a08-120">/api/products</span></span> |
| <span data-ttu-id="81a08-121">Získání produktu podle ID</span><span class="sxs-lookup"><span data-stu-id="81a08-121">Get a product by ID</span></span> | <span data-ttu-id="81a08-122">GET</span><span class="sxs-lookup"><span data-stu-id="81a08-122">GET</span></span> | <span data-ttu-id="81a08-123">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="81a08-123">/api/products/*id*</span></span> |
| <span data-ttu-id="81a08-124">Získání produktu podle kategorie</span><span class="sxs-lookup"><span data-stu-id="81a08-124">Get a product by category</span></span> | <span data-ttu-id="81a08-125">GET</span><span class="sxs-lookup"><span data-stu-id="81a08-125">GET</span></span> | <span data-ttu-id="81a08-126">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="81a08-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="81a08-127">Vytvořit nový produkt</span><span class="sxs-lookup"><span data-stu-id="81a08-127">Create a new product</span></span> | <span data-ttu-id="81a08-128">POST</span><span class="sxs-lookup"><span data-stu-id="81a08-128">POST</span></span> | <span data-ttu-id="81a08-129">/ api/produkty</span><span class="sxs-lookup"><span data-stu-id="81a08-129">/api/products</span></span> |
| <span data-ttu-id="81a08-130">Aktualizace produktu</span><span class="sxs-lookup"><span data-stu-id="81a08-130">Update a product</span></span> | <span data-ttu-id="81a08-131">PUT</span><span class="sxs-lookup"><span data-stu-id="81a08-131">PUT</span></span> | <span data-ttu-id="81a08-132">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="81a08-132">/api/products/*id*</span></span> |
| <span data-ttu-id="81a08-133">Odstranit produkt</span><span class="sxs-lookup"><span data-stu-id="81a08-133">Delete a product</span></span> | <span data-ttu-id="81a08-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="81a08-134">DELETE</span></span> | <span data-ttu-id="81a08-135">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="81a08-135">/api/products/*id*</span></span> |

<span data-ttu-id="81a08-136">Všimněte si, že některé identifikátory URI obsahovat číslo product ID v cestě.</span><span class="sxs-lookup"><span data-stu-id="81a08-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="81a08-137">Pokud chcete získat produktů, jehož ID je 28, klient odešle požadavek GET `http://hostname/api/products/28`.</span><span class="sxs-lookup"><span data-stu-id="81a08-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="81a08-138">Prostředky</span><span class="sxs-lookup"><span data-stu-id="81a08-138">Resources</span></span>

<span data-ttu-id="81a08-139">Produkty API definuje identifikátory URI pro dva typy prostředků:</span><span class="sxs-lookup"><span data-stu-id="81a08-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="81a08-140">Resource</span><span class="sxs-lookup"><span data-stu-id="81a08-140">Resource</span></span> | <span data-ttu-id="81a08-141">Identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="81a08-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="81a08-142">Seznam všech produktů.</span><span class="sxs-lookup"><span data-stu-id="81a08-142">The list of all the products.</span></span> | <span data-ttu-id="81a08-143">/ api/produkty</span><span class="sxs-lookup"><span data-stu-id="81a08-143">/api/products</span></span> |
| <span data-ttu-id="81a08-144">Jednotlivé produkty.</span><span class="sxs-lookup"><span data-stu-id="81a08-144">An individual product.</span></span> | <span data-ttu-id="81a08-145">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="81a08-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="81a08-146">Metody</span><span class="sxs-lookup"><span data-stu-id="81a08-146">Methods</span></span>

<span data-ttu-id="81a08-147">Čtyři hlavní metody HTTP (GET, PUT, POST a DELETE) lze mapovat na operace CRUD následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="81a08-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="81a08-148">GET načte reprezentaci prostředku na zadaný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="81a08-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="81a08-149">GET by měl mít žádné vedlejší účinky na serveru.</span><span class="sxs-lookup"><span data-stu-id="81a08-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="81a08-150">PUT aktualizuje prostředek na zadaný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="81a08-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="81a08-151">PUT také umožňuje vytvořit nový prostředek na zadaný identifikátor URI, pokud server umožňuje klientům k určení nové identifikátory URI.</span><span class="sxs-lookup"><span data-stu-id="81a08-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="81a08-152">Pro účely tohoto kurzu nebude podporovat rozhraní API pro vytváření PUT.</span><span class="sxs-lookup"><span data-stu-id="81a08-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="81a08-153">POST vytvoří nový prostředek.</span><span class="sxs-lookup"><span data-stu-id="81a08-153">POST creates a new resource.</span></span> <span data-ttu-id="81a08-154">Server přiřadí identifikátor URI pro nový objekt a vrátí tento identifikátor URI jako část zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="81a08-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="81a08-155">Odstranit Odstraní prostředek na zadaný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="81a08-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="81a08-156">Poznámka: Metoda PUT nahradí entitu celého produktu.</span><span class="sxs-lookup"><span data-stu-id="81a08-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="81a08-157">To znamená Klient by měl odeslat úplnou reprezentaci aktualizace produktu.</span><span class="sxs-lookup"><span data-stu-id="81a08-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="81a08-158">Pokud chcete zajistit podporu částečné aktualizace, je upřednostňovanou metodu PATCH.</span><span class="sxs-lookup"><span data-stu-id="81a08-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="81a08-159">Tento kurz neimplementuje opravy.</span><span class="sxs-lookup"><span data-stu-id="81a08-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="81a08-160">Vytvořte nový projekt webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="81a08-160">Create a New Web API Project</span></span>

<span data-ttu-id="81a08-161">Začněte tím, že spustíte Visual Studio a vyberte **nový projekt** z **Start** stránky.</span><span class="sxs-lookup"><span data-stu-id="81a08-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="81a08-162">Nebo z **souboru** nabídce vyberte možnost **nový** a potom **projektu**.</span><span class="sxs-lookup"><span data-stu-id="81a08-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="81a08-163">V **šablony** vyberte **nainstalované šablony** a rozbalte **Visual C#** uzlu.</span><span class="sxs-lookup"><span data-stu-id="81a08-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="81a08-164">V části **Visual C#** vyberte **webové**.</span><span class="sxs-lookup"><span data-stu-id="81a08-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="81a08-165">V seznamu šablon projektu vyberte **webové aplikace ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="81a08-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="81a08-166">Pojmenujte projekt &quot;ProductStore&quot; a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="81a08-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="81a08-167">V **nového projektu ASP.NET MVC 4** dialogového okna, vyberte **webového rozhraní API** a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="81a08-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="81a08-168">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="81a08-168">Adding a Model</span></span>

<span data-ttu-id="81a08-169">A *modelu* je objekt, který představuje data ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="81a08-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="81a08-170">V rozhraní ASP.NET Web API objektů se silným typem CLR slouží jako modelů a jejich bude automaticky serializovat do XML nebo JSON pro klienta.</span><span class="sxs-lookup"><span data-stu-id="81a08-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="81a08-171">Pro rozhraní API ProductStore naše data se skládá z produktů, takže vytvoříme novou třídu s názvem `Product`.</span><span class="sxs-lookup"><span data-stu-id="81a08-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="81a08-172">Pokud již není Průzkumník řešení viditelný, klikněte na tlačítko **zobrazení** nabídky a vybereme **Průzkumníka řešení**.</span><span class="sxs-lookup"><span data-stu-id="81a08-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="81a08-173">V Průzkumníku řešení klikněte pravým tlačítkem myši **modely** složky.</span><span class="sxs-lookup"><span data-stu-id="81a08-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="81a08-174">V místní nabídce vyberte **přidat**a pak vyberte **třídy**.</span><span class="sxs-lookup"><span data-stu-id="81a08-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="81a08-175">Název třídy &quot;produktu&quot;.</span><span class="sxs-lookup"><span data-stu-id="81a08-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="81a08-176">Přidejte následující vlastnosti pro `Product` třídy.</span><span class="sxs-lookup"><span data-stu-id="81a08-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="81a08-177">Přidání úložiště</span><span class="sxs-lookup"><span data-stu-id="81a08-177">Adding a Repository</span></span>

<span data-ttu-id="81a08-178">Potřebujeme k uložení kolekce produktů.</span><span class="sxs-lookup"><span data-stu-id="81a08-178">We need to store a collection of products.</span></span> <span data-ttu-id="81a08-179">Je vhodné oddělit kolekce z naší implementaci služby.</span><span class="sxs-lookup"><span data-stu-id="81a08-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="81a08-180">Tímto způsobem můžeme změnit záložní úložiště bez přepsání třídu služby.</span><span class="sxs-lookup"><span data-stu-id="81a08-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="81a08-181">Tento typ návrhu se nazývá *úložiště* vzor.</span><span class="sxs-lookup"><span data-stu-id="81a08-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="81a08-182">Začněte tím, že definování obecné rozhraní pro úložiště.</span><span class="sxs-lookup"><span data-stu-id="81a08-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="81a08-183">V Průzkumníku řešení klikněte pravým tlačítkem myši **modely** složky.</span><span class="sxs-lookup"><span data-stu-id="81a08-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="81a08-184">Vyberte **přidat**a pak vyberte **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="81a08-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="81a08-185">V **šablony** vyberte **nainstalované šablony** a rozbalte uzel jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="81a08-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="81a08-186">V jazyce C# vyberte **kód**.</span><span class="sxs-lookup"><span data-stu-id="81a08-186">Under C#, select **Code**.</span></span> <span data-ttu-id="81a08-187">Vyberte v seznamu šablon kódu **rozhraní**.</span><span class="sxs-lookup"><span data-stu-id="81a08-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="81a08-188">Název rozhraní &quot;IProductRepository&quot;.</span><span class="sxs-lookup"><span data-stu-id="81a08-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="81a08-189">Přidejte následující implementaci:</span><span class="sxs-lookup"><span data-stu-id="81a08-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="81a08-190">Nyní přidejte další třídu ke složce modelů s názvem &quot;ProductRepository.&quot; Tato třída implementuje `IProductRepository` rozhraní.</span><span class="sxs-lookup"><span data-stu-id="81a08-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="81a08-191">Přidejte následující implementaci:</span><span class="sxs-lookup"><span data-stu-id="81a08-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="81a08-192">Úložiště zajišťuje seznamu místní paměti.</span><span class="sxs-lookup"><span data-stu-id="81a08-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="81a08-193">Tento kurz je v pořádku, ale v reálné aplikaci bude ukládat data externě, buď databázi nebo v cloudovém úložišti.</span><span class="sxs-lookup"><span data-stu-id="81a08-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="81a08-194">Vzor úložiště vám usnadní změňte implementaci později.</span><span class="sxs-lookup"><span data-stu-id="81a08-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="81a08-195">Přidání Kontroleru webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="81a08-195">Adding a Web API Controller</span></span>

<span data-ttu-id="81a08-196">Pokud jste už pracovali s ASP.NET MVC, pak jste již obeznámeni s řadiči.</span><span class="sxs-lookup"><span data-stu-id="81a08-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="81a08-197">V rozhraní ASP.NET Web API *řadič* je třída, která zpracovává požadavky HTTP od klienta.</span><span class="sxs-lookup"><span data-stu-id="81a08-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="81a08-198">Průvodce novým projektem vytvoří dva řadiče za vás při vytváření projektu.</span><span class="sxs-lookup"><span data-stu-id="81a08-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="81a08-199">Neuvidíte, rozbalte složku řadiče v Průzkumníku řešení.</span><span class="sxs-lookup"><span data-stu-id="81a08-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="81a08-200">HomeController je tradiční kontroler ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="81a08-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="81a08-201">Zodpovídá za poskytování stránky HTML pro web a přímo nesouvisí s naší webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="81a08-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="81a08-202">Kontroleru ValuesController se příklad řadiče WebAPI.</span><span class="sxs-lookup"><span data-stu-id="81a08-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="81a08-203">Pokračujte a odstranit kontroleru ValuesController, tak, že kliknete pravým tlačítkem soubor v Průzkumníku řešení a vyberete **odstranit.**</span><span class="sxs-lookup"><span data-stu-id="81a08-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="81a08-204">Nyní přidejte nový kontroler, následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="81a08-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="81a08-205">V **Průzkumníka řešení**, klikněte pravým tlačítkem na složku řadiče.</span><span class="sxs-lookup"><span data-stu-id="81a08-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="81a08-206">Vyberte **přidat** a pak vyberte **řadič**.</span><span class="sxs-lookup"><span data-stu-id="81a08-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="81a08-207">V **přidat kontroler** průvodce, názvu kontroleru &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="81a08-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="81a08-208">V **šablony** rozevíracího seznamu vyberte **prázdný kontroler API**.</span><span class="sxs-lookup"><span data-stu-id="81a08-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="81a08-209">Pak klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="81a08-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="81a08-210">Není nutné převést vaše řadiče do složky s názvem řadiče.</span><span class="sxs-lookup"><span data-stu-id="81a08-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="81a08-211">Název složky není důležité. je jednoduše pohodlný způsob, jak uspořádat zdrojové soubory.</span><span class="sxs-lookup"><span data-stu-id="81a08-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="81a08-212">**Přidat kontroler** průvodce vytvořit soubor s názvem ProductsController.cs ve složce řadiče.</span><span class="sxs-lookup"><span data-stu-id="81a08-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="81a08-213">Pokud tento soubor ještě není otevřený, klikněte dvakrát na soubor otevřete.</span><span class="sxs-lookup"><span data-stu-id="81a08-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="81a08-214">Přidejte následující **pomocí** – příkaz:</span><span class="sxs-lookup"><span data-stu-id="81a08-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="81a08-215">Přidat pole, která obsahuje **IProductRepository** instance.</span><span class="sxs-lookup"><span data-stu-id="81a08-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="81a08-216">Volání `new ProductRepository()` v řadiči není optimální, protože propojuje kontroleru pro konkrétní implementaci `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="81a08-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="81a08-217">Lepším řešením, naleznete v tématu [použitím překladač závislostí webové rozhraní API](../advanced/dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="81a08-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="81a08-218">Získání prostředku</span><span class="sxs-lookup"><span data-stu-id="81a08-218">Getting a Resource</span></span>

<span data-ttu-id="81a08-219">Rozhraní API ProductStore bude vystavovat několik &quot;čtení&quot; akce jako metody GET protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="81a08-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="81a08-220">Každá akce, které budou odpovídat na metodu v `ProductsController` třídy.</span><span class="sxs-lookup"><span data-stu-id="81a08-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="81a08-221">Akce</span><span class="sxs-lookup"><span data-stu-id="81a08-221">Action</span></span> | <span data-ttu-id="81a08-222">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="81a08-222">HTTP method</span></span> | <span data-ttu-id="81a08-223">Relativní identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="81a08-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="81a08-224">Získání seznamu všech produktů</span><span class="sxs-lookup"><span data-stu-id="81a08-224">Get a list of all products</span></span> | <span data-ttu-id="81a08-225">GET</span><span class="sxs-lookup"><span data-stu-id="81a08-225">GET</span></span> | <span data-ttu-id="81a08-226">/ api/produkty</span><span class="sxs-lookup"><span data-stu-id="81a08-226">/api/products</span></span> |
| <span data-ttu-id="81a08-227">Získání produktu podle ID</span><span class="sxs-lookup"><span data-stu-id="81a08-227">Get a product by ID</span></span> | <span data-ttu-id="81a08-228">GET</span><span class="sxs-lookup"><span data-stu-id="81a08-228">GET</span></span> | <span data-ttu-id="81a08-229">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="81a08-229">/api/products/*id*</span></span> |
| <span data-ttu-id="81a08-230">Získání produktu podle kategorie</span><span class="sxs-lookup"><span data-stu-id="81a08-230">Get a product by category</span></span> | <span data-ttu-id="81a08-231">GET</span><span class="sxs-lookup"><span data-stu-id="81a08-231">GET</span></span> | <span data-ttu-id="81a08-232">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="81a08-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="81a08-233">Pokud chcete získat seznam všech produktů, přidejte tuto metodu za účelem `ProductsController` třídy:</span><span class="sxs-lookup"><span data-stu-id="81a08-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="81a08-234">Název metody, který začíná &quot;získat&quot;, takže podle konvence je namapován na požadavky GET.</span><span class="sxs-lookup"><span data-stu-id="81a08-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="81a08-235">Navíc vzhledem k tomu, že metoda nemá žádné parametry, mapuje se na identifikátor URI, který neobsahuje *&quot;id&quot;* segment v cestě.</span><span class="sxs-lookup"><span data-stu-id="81a08-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="81a08-236">Chcete-li získat produktů podle ID, přidejte tuto metodu za účelem `ProductsController` třídy:</span><span class="sxs-lookup"><span data-stu-id="81a08-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="81a08-237">Tento název metody také začíná &quot;získat&quot;, ale metoda nemá parametr pojmenovaný *id*. Tento parametr je namapována na &quot;id&quot; segment cesty identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="81a08-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="81a08-238">ID rozhraní ASP.NET Web API automaticky převede na správného datového typu (**int**) pro parametr.</span><span class="sxs-lookup"><span data-stu-id="81a08-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="81a08-239">Metoda GetProduct vyvolá výjimku typu **HttpResponseException** Pokud *id* není platný.</span><span class="sxs-lookup"><span data-stu-id="81a08-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="81a08-240">Tato výjimka bude fungovat v rámci rozhraní chybu 404 (Nenalezeno).</span><span class="sxs-lookup"><span data-stu-id="81a08-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="81a08-241">Nakonec přidejte metodu k vyhledat produkty podle kategorie:</span><span class="sxs-lookup"><span data-stu-id="81a08-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="81a08-242">Pokud identifikátor URI požadavku obsahuje řetězce dotazu, se pokusí odpovídat parametrům dotazu k parametrům metody kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="81a08-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="81a08-243">Proto se identifikátor URI ve tvaru "rozhraní api a produktů? kategorie =*kategorie*" se namapuje do této metody.</span><span class="sxs-lookup"><span data-stu-id="81a08-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="81a08-244">Vytvoření prostředku</span><span class="sxs-lookup"><span data-stu-id="81a08-244">Creating a Resource</span></span>

<span data-ttu-id="81a08-245">V dalším kroku přidáme metodu `ProductsController` třídy za účelem vytvoření nového produktu.</span><span class="sxs-lookup"><span data-stu-id="81a08-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="81a08-246">Tady je jednoduchý implementace metody:</span><span class="sxs-lookup"><span data-stu-id="81a08-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="81a08-247">Mějte na paměti o této metodě dvě věci:</span><span class="sxs-lookup"><span data-stu-id="81a08-247">Note two things about this method:</span></span>

- <span data-ttu-id="81a08-248">Název metody, který začíná &quot;příspěvek... &quot;.</span><span class="sxs-lookup"><span data-stu-id="81a08-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="81a08-249">Pokud chcete vytvořit nový produkt, klient odešle požadavek HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="81a08-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="81a08-250">Tato metoda přebírá parametr typu produktu.</span><span class="sxs-lookup"><span data-stu-id="81a08-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="81a08-251">V rozhraní Web API parametry s komplexní typy jsou v daném kontextu deserializovat tělo požadavku.</span><span class="sxs-lookup"><span data-stu-id="81a08-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="81a08-252">Proto Očekáváme, že klientovi umožní odeslat serializovaná reprezentace objektu produktu ve formátu XML nebo JSON.</span><span class="sxs-lookup"><span data-stu-id="81a08-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="81a08-253">Tato implementace bude fungovat, ale není úplně kompletní.</span><span class="sxs-lookup"><span data-stu-id="81a08-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="81a08-254">V ideálním případě by rádi bychom odpověď HTTP, patří:</span><span class="sxs-lookup"><span data-stu-id="81a08-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="81a08-255">**Kód odpovědi:** Ve výchozím nastavení rozhraní webového rozhraní API nastaví stavový kód odpovědi 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="81a08-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="81a08-256">Ale podle protokolu HTTP/1.1, když požadavek POST má za následek vytvoření prostředku, server by měl odpovídat se stavem 201 (vytvořeno).</span><span class="sxs-lookup"><span data-stu-id="81a08-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="81a08-257">**Umístění:** Když na serveru se vytvoří prostředek, měl by obsahovat identifikátor URI nového prostředku v hlavičce umístění odpovědi.</span><span class="sxs-lookup"><span data-stu-id="81a08-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="81a08-258">Rozhraní ASP.NET Web API usnadňuje zpracování zprávy s odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="81a08-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="81a08-259">Tady je lepší implementace:</span><span class="sxs-lookup"><span data-stu-id="81a08-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="81a08-260">Všimněte si, že je návratový typ metody teď **objekt HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="81a08-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="81a08-261">Vrácením **objekt HttpResponseMessage** místo produktu, jsme můžete řídit podrobnosti zprávy s odpovědí HTTP, včetně stavový kód a hlavičku Location.</span><span class="sxs-lookup"><span data-stu-id="81a08-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="81a08-262">**CreateResponse** metoda vytvoří **objekt HttpResponseMessage** a automaticky zapisuje do těla serializovaná reprezentace objektu Product fo zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="81a08-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="81a08-263">V tomto příkladu neověřuje, `Product`.</span><span class="sxs-lookup"><span data-stu-id="81a08-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="81a08-264">Informace o ověření modelu naleznete v tématu [ověření modelu v rozhraní ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="81a08-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="81a08-265">Aktualizuje se prostředek</span><span class="sxs-lookup"><span data-stu-id="81a08-265">Updating a Resource</span></span>

<span data-ttu-id="81a08-266">Aktualizace produktu pomocí PUT je jednoduchý:</span><span class="sxs-lookup"><span data-stu-id="81a08-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="81a08-267">Název metody, který začíná &quot;vložit... &quot;, takže webového rozhraní API patřil k žádosti PUT.</span><span class="sxs-lookup"><span data-stu-id="81a08-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="81a08-268">Tato metoda přebírá dva parametry, ID produktu a aktualizace produktu.</span><span class="sxs-lookup"><span data-stu-id="81a08-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="81a08-269">*Id* parametr je převzata z cesty identifikátoru URI a *produktu* parametru se v daném kontextu deserializovat tělo požadavku.</span><span class="sxs-lookup"><span data-stu-id="81a08-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="81a08-270">Ve výchozím nastavení použije rozhraní ASP.NET Web API jednoduché typy parametrů z trasy a komplexní typy z textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="81a08-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="81a08-271">Odstranění prostředku</span><span class="sxs-lookup"><span data-stu-id="81a08-271">Deleting a Resource</span></span>

<span data-ttu-id="81a08-272">Chcete-li odstranit prostředek, definujte "Odstranit..." Metoda.</span><span class="sxs-lookup"><span data-stu-id="81a08-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="81a08-273">Pokud je žádost o odstranění úspěšné, může vrátit stav 200 (OK) s – obsah entity, která popisuje stav; Stav 202 (přijato), pokud se odstranění je stále čeká na; stav nebo 204 (žádný obsah) se žádný obsah entity.</span><span class="sxs-lookup"><span data-stu-id="81a08-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="81a08-274">V takovém případě `DeleteProduct` metoda má `void` návratový typ, takže rozhraní ASP.NET Web API automaticky to převede do stavu kód 204 (žádný obsah).</span><span class="sxs-lookup"><span data-stu-id="81a08-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
