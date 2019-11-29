---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: Povolení operací CRUD ve webovém rozhraní API ASP.NET 1 – ASP.NET 4. x
author: MikeWasson
description: V tomto kurzu se dozvíte, jak podporovat operace CRUD ve službě HTTP pomocí webového rozhraní API ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600341"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="189f6-103">Povolení operací CRUD ve webovém rozhraní API ASP.NET 1</span><span class="sxs-lookup"><span data-stu-id="189f6-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="189f6-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="189f6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="189f6-105">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="189f6-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="189f6-106">V tomto kurzu se dozvíte, jak podporovat operace CRUD ve službě HTTP pomocí webového rozhraní API ASP.NET pro ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="189f6-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="189f6-107">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="189f6-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="189f6-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="189f6-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="189f6-109">Webové rozhraní API 1 (funguje taky s webovým rozhraním API 2)</span><span class="sxs-lookup"><span data-stu-id="189f6-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="189f6-110">CRUD představuje &quot;vytváření, čtení, aktualizace a odstraňování&quot; což jsou čtyři základní databázové operace.</span><span class="sxs-lookup"><span data-stu-id="189f6-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="189f6-111">Mnohé služby HTTP také modelují operace CRUD prostřednictvím rozhraní API REST nebo REST.</span><span class="sxs-lookup"><span data-stu-id="189f6-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="189f6-112">V tomto kurzu vytvoříte velmi jednoduché webové rozhraní API pro správu seznamu produktů.</span><span class="sxs-lookup"><span data-stu-id="189f6-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="189f6-113">Každý produkt bude obsahovat název, cenu a kategorii (například &quot;Toys&quot; nebo &quot;hardware&quot;) a ID produktu.</span><span class="sxs-lookup"><span data-stu-id="189f6-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="189f6-114">Rozhraní API pro produkty zpřístupňuje následující metody.</span><span class="sxs-lookup"><span data-stu-id="189f6-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="189f6-115">Akce</span><span class="sxs-lookup"><span data-stu-id="189f6-115">Action</span></span> | <span data-ttu-id="189f6-116">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="189f6-116">HTTP method</span></span> | <span data-ttu-id="189f6-117">Relativní identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="189f6-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="189f6-118">Získat seznam všech produktů</span><span class="sxs-lookup"><span data-stu-id="189f6-118">Get a list of all products</span></span> | <span data-ttu-id="189f6-119">GET</span><span class="sxs-lookup"><span data-stu-id="189f6-119">GET</span></span> | <span data-ttu-id="189f6-120">/api/products</span><span class="sxs-lookup"><span data-stu-id="189f6-120">/api/products</span></span> |
| <span data-ttu-id="189f6-121">Získat produkt podle ID</span><span class="sxs-lookup"><span data-stu-id="189f6-121">Get a product by ID</span></span> | <span data-ttu-id="189f6-122">GET</span><span class="sxs-lookup"><span data-stu-id="189f6-122">GET</span></span> | <span data-ttu-id="189f6-123">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="189f6-123">/api/products/*id*</span></span> |
| <span data-ttu-id="189f6-124">Získat produkt podle kategorie</span><span class="sxs-lookup"><span data-stu-id="189f6-124">Get a product by category</span></span> | <span data-ttu-id="189f6-125">GET</span><span class="sxs-lookup"><span data-stu-id="189f6-125">GET</span></span> | <span data-ttu-id="189f6-126">/API/Products? kategorie =*kategorie*</span><span class="sxs-lookup"><span data-stu-id="189f6-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="189f6-127">Vytvořit nový produkt</span><span class="sxs-lookup"><span data-stu-id="189f6-127">Create a new product</span></span> | <span data-ttu-id="189f6-128">POST</span><span class="sxs-lookup"><span data-stu-id="189f6-128">POST</span></span> | <span data-ttu-id="189f6-129">/api/products</span><span class="sxs-lookup"><span data-stu-id="189f6-129">/api/products</span></span> |
| <span data-ttu-id="189f6-130">Aktualizace produktu</span><span class="sxs-lookup"><span data-stu-id="189f6-130">Update a product</span></span> | <span data-ttu-id="189f6-131">PŘEVÉST</span><span class="sxs-lookup"><span data-stu-id="189f6-131">PUT</span></span> | <span data-ttu-id="189f6-132">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="189f6-132">/api/products/*id*</span></span> |
| <span data-ttu-id="189f6-133">Odstranění produktu</span><span class="sxs-lookup"><span data-stu-id="189f6-133">Delete a product</span></span> | <span data-ttu-id="189f6-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="189f6-134">DELETE</span></span> | <span data-ttu-id="189f6-135">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="189f6-135">/api/products/*id*</span></span> |

<span data-ttu-id="189f6-136">Všimněte si, že některé identifikátory URI zahrnují ID produktu v cestě.</span><span class="sxs-lookup"><span data-stu-id="189f6-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="189f6-137">Pokud například chcete získat produkt, jehož ID je 28, klient odešle požadavek GET na `http://hostname/api/products/28`.</span><span class="sxs-lookup"><span data-stu-id="189f6-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="189f6-138">Prostředky</span><span class="sxs-lookup"><span data-stu-id="189f6-138">Resources</span></span>

<span data-ttu-id="189f6-139">Rozhraní API pro produkty definuje identifikátory URI pro dva typy prostředků:</span><span class="sxs-lookup"><span data-stu-id="189f6-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="189f6-140">Prostředek</span><span class="sxs-lookup"><span data-stu-id="189f6-140">Resource</span></span> | <span data-ttu-id="189f6-141">URI</span><span class="sxs-lookup"><span data-stu-id="189f6-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="189f6-142">Seznam všech produktů.</span><span class="sxs-lookup"><span data-stu-id="189f6-142">The list of all the products.</span></span> | <span data-ttu-id="189f6-143">/api/products</span><span class="sxs-lookup"><span data-stu-id="189f6-143">/api/products</span></span> |
| <span data-ttu-id="189f6-144">Jednotlivý produkt.</span><span class="sxs-lookup"><span data-stu-id="189f6-144">An individual product.</span></span> | <span data-ttu-id="189f6-145">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="189f6-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="189f6-146">Metody</span><span class="sxs-lookup"><span data-stu-id="189f6-146">Methods</span></span>

<span data-ttu-id="189f6-147">Čtyři hlavní metody HTTP (GET, PUT, POST a DELETE) lze namapovat na operace CRUD následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="189f6-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="189f6-148">GET načte reprezentace prostředku na zadaném identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="189f6-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="189f6-149">GET by neměl mít na serveru žádné vedlejší účinky.</span><span class="sxs-lookup"><span data-stu-id="189f6-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="189f6-150">VLOŽÍ aktualizace prostředku se zadaným identifikátorem URI.</span><span class="sxs-lookup"><span data-stu-id="189f6-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="189f6-151">Příkaz PUT lze použít také k vytvoření nového prostředku v zadaném identifikátoru URI, pokud server umožňuje klientům zadat nové identifikátory URI.</span><span class="sxs-lookup"><span data-stu-id="189f6-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="189f6-152">V tomto kurzu rozhraní API nebude podporovat vytváření prostřednictvím PUT.</span><span class="sxs-lookup"><span data-stu-id="189f6-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="189f6-153">POST vytvoří nový prostředek.</span><span class="sxs-lookup"><span data-stu-id="189f6-153">POST creates a new resource.</span></span> <span data-ttu-id="189f6-154">Server přiřadí identifikátor URI pro nový objekt a vrátí tento identifikátor URI jako součást zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="189f6-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="189f6-155">ODSTRANĚNÍ odstraní prostředek se zadaným identifikátorem URI.</span><span class="sxs-lookup"><span data-stu-id="189f6-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="189f6-156">Poznámka: metoda PUT nahrazuje celou entitu produktu.</span><span class="sxs-lookup"><span data-stu-id="189f6-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="189f6-157">To znamená, že klient očekává odeslání úplné reprezentace aktualizovaného produktu.</span><span class="sxs-lookup"><span data-stu-id="189f6-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="189f6-158">Pokud chcete podporovat částečné aktualizace, je vhodnější metoda opravy.</span><span class="sxs-lookup"><span data-stu-id="189f6-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="189f6-159">Tento kurz neimplementuje opravu.</span><span class="sxs-lookup"><span data-stu-id="189f6-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="189f6-160">Vytvoření nového projektu webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="189f6-160">Create a New Web API Project</span></span>

<span data-ttu-id="189f6-161">Začněte spuštěním sady Visual Studio a na **úvodní** stránce vyberte **Nový projekt** .</span><span class="sxs-lookup"><span data-stu-id="189f6-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="189f6-162">Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.</span><span class="sxs-lookup"><span data-stu-id="189f6-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="189f6-163">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** .</span><span class="sxs-lookup"><span data-stu-id="189f6-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="189f6-164">V **části C#vizuál** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="189f6-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="189f6-165">V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="189f6-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="189f6-166">Pojmenujte projekt &quot;ProductStore&quot; a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="189f6-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="189f6-167">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte **webové rozhraní API** a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="189f6-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="189f6-168">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="189f6-168">Adding a Model</span></span>

<span data-ttu-id="189f6-169">*Model* je objekt, který představuje data v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="189f6-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="189f6-170">Ve webovém rozhraní API ASP.NET můžete jako modely použít objekty CLR silného typu a automaticky je serializovat do XML nebo JSON pro klienta.</span><span class="sxs-lookup"><span data-stu-id="189f6-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="189f6-171">Pro rozhraní ProductStore API se naše data skládají z produktů, takže vytvoříme novou třídu s názvem `Product`.</span><span class="sxs-lookup"><span data-stu-id="189f6-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="189f6-172">Pokud Průzkumník řešení ještě není vidět, klikněte na nabídku **zobrazení** a vyberte možnost **Průzkumník řešení**.</span><span class="sxs-lookup"><span data-stu-id="189f6-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="189f6-173">V Průzkumník řešení klikněte pravým tlačítkem na složku **modely** .</span><span class="sxs-lookup"><span data-stu-id="189f6-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="189f6-174">V místní nabídce vyberte **Přidat**a pak vyberte **Třída**.</span><span class="sxs-lookup"><span data-stu-id="189f6-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="189f6-175">Pojmenujte třídu &quot;&quot;produktu.</span><span class="sxs-lookup"><span data-stu-id="189f6-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="189f6-176">Do třídy `Product` přidejte následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="189f6-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="189f6-177">Přidání úložiště</span><span class="sxs-lookup"><span data-stu-id="189f6-177">Adding a Repository</span></span>

<span data-ttu-id="189f6-178">Musíme Uložit kolekci produktů.</span><span class="sxs-lookup"><span data-stu-id="189f6-178">We need to store a collection of products.</span></span> <span data-ttu-id="189f6-179">Je vhodné oddělit kolekci od implementace naší služby.</span><span class="sxs-lookup"><span data-stu-id="189f6-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="189f6-180">Tímto způsobem můžeme změnit záložní úložiště bez přepsání třídy služby.</span><span class="sxs-lookup"><span data-stu-id="189f6-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="189f6-181">Tento typ návrhu se nazývá vzor *úložiště* .</span><span class="sxs-lookup"><span data-stu-id="189f6-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="189f6-182">Začněte definováním obecného rozhraní pro úložiště.</span><span class="sxs-lookup"><span data-stu-id="189f6-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="189f6-183">V Průzkumník řešení klikněte pravým tlačítkem na složku **modely** .</span><span class="sxs-lookup"><span data-stu-id="189f6-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="189f6-184">Vyberte **Přidat**a pak vyberte **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="189f6-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="189f6-185">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte C# uzel.</span><span class="sxs-lookup"><span data-stu-id="189f6-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="189f6-186">V C#části vyberte **kód**.</span><span class="sxs-lookup"><span data-stu-id="189f6-186">Under C#, select **Code**.</span></span> <span data-ttu-id="189f6-187">V seznamu šablon kódu vyberte **rozhraní**.</span><span class="sxs-lookup"><span data-stu-id="189f6-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="189f6-188">Název rozhraní &quot;IProductRepository&quot;.</span><span class="sxs-lookup"><span data-stu-id="189f6-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="189f6-189">Přidejte následující implementaci:</span><span class="sxs-lookup"><span data-stu-id="189f6-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="189f6-190">Nyní do složky modely přidejte další třídu s názvem &quot;ProductRepository.&quot; Tato třída bude implementovat rozhraní `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="189f6-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="189f6-191">Přidejte následující implementaci:</span><span class="sxs-lookup"><span data-stu-id="189f6-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="189f6-192">Úložiště uchovává seznam v místní paměti.</span><span class="sxs-lookup"><span data-stu-id="189f6-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="189f6-193">V tomto kurzu je to v pořádku, ale v reálné aplikaci byste data ukládali externě, buď do databáze, nebo do cloudového úložiště.</span><span class="sxs-lookup"><span data-stu-id="189f6-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="189f6-194">Vzor úložiště vám usnadní pozdější změnu implementace.</span><span class="sxs-lookup"><span data-stu-id="189f6-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="189f6-195">Přidání kontroleru webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="189f6-195">Adding a Web API Controller</span></span>

<span data-ttu-id="189f6-196">Pokud jste pracovali s ASP.NET MVC, už jste obeznámeni s řadiči.</span><span class="sxs-lookup"><span data-stu-id="189f6-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="189f6-197">Ve webovém rozhraní API ASP.NET je *kontroler* třída, která zpracovává požadavky HTTP od klienta.</span><span class="sxs-lookup"><span data-stu-id="189f6-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="189f6-198">Průvodce vytvořením nového projektu při vytváření projektu vytvořil dva řadiče.</span><span class="sxs-lookup"><span data-stu-id="189f6-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="189f6-199">Pokud je chcete zobrazit, rozbalte složku řadiče v Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="189f6-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="189f6-200">HomeController je tradiční kontroler ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="189f6-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="189f6-201">Zodpovídá za obsluhu stránek HTML webu a přímo se nevztahuje k našemu webovému rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="189f6-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="189f6-202">ValuesController je ukázkový kontroler WebAPI.</span><span class="sxs-lookup"><span data-stu-id="189f6-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="189f6-203">Pokračujte a odstraňte ValuesController tak, že kliknete pravým tlačítkem na soubor v Průzkumník řešení a vyberete **Odstranit.**</span><span class="sxs-lookup"><span data-stu-id="189f6-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="189f6-204">Nyní přidejte nový kontroler, a to takto:</span><span class="sxs-lookup"><span data-stu-id="189f6-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="189f6-205">V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="189f6-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="189f6-206">Vyberte **Přidat** a pak vybrat **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="189f6-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="189f6-207">V průvodci **přidáním kontroleru** pojmenujte kontrolér &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="189f6-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="189f6-208">V rozevíracím seznamu **Šablona** vyberte **prázdný kontroler rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="189f6-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="189f6-209">Pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="189f6-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="189f6-210">Ovladače není nutné vkládat do složky s názvem Controllers.</span><span class="sxs-lookup"><span data-stu-id="189f6-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="189f6-211">Název složky není důležitý. je to jednoduše pohodlný způsob, jak uspořádat zdrojové soubory.</span><span class="sxs-lookup"><span data-stu-id="189f6-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="189f6-212">Průvodce **přidáním kontroleru** vytvoří ve složce Controllers soubor s názvem ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="189f6-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="189f6-213">Pokud tento soubor ještě není otevřený, otevřete ho tak, že na něj dvakrát kliknete.</span><span class="sxs-lookup"><span data-stu-id="189f6-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="189f6-214">Přidejte následující příkaz **using** :</span><span class="sxs-lookup"><span data-stu-id="189f6-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="189f6-215">Přidejte pole, které obsahuje instanci **IProductRepository** .</span><span class="sxs-lookup"><span data-stu-id="189f6-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="189f6-216">Volání `new ProductRepository()` v kontroleru není nejlepším návrhem, protože tento kontroler přiřazuje konkrétní implementaci `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="189f6-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="189f6-217">Lepší přístup najdete v tématu [použití překladače závislostí webového rozhraní API](../advanced/dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="189f6-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="189f6-218">Získání prostředku</span><span class="sxs-lookup"><span data-stu-id="189f6-218">Getting a Resource</span></span>

<span data-ttu-id="189f6-219">Rozhraní ProductStore API zveřejňuje několik &quot;číst&quot; akcí jako metody GET protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="189f6-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="189f6-220">Každá akce bude odpovídat metodě ve třídě `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="189f6-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="189f6-221">Akce</span><span class="sxs-lookup"><span data-stu-id="189f6-221">Action</span></span> | <span data-ttu-id="189f6-222">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="189f6-222">HTTP method</span></span> | <span data-ttu-id="189f6-223">Relativní identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="189f6-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="189f6-224">Získat seznam všech produktů</span><span class="sxs-lookup"><span data-stu-id="189f6-224">Get a list of all products</span></span> | <span data-ttu-id="189f6-225">GET</span><span class="sxs-lookup"><span data-stu-id="189f6-225">GET</span></span> | <span data-ttu-id="189f6-226">/api/products</span><span class="sxs-lookup"><span data-stu-id="189f6-226">/api/products</span></span> |
| <span data-ttu-id="189f6-227">Získat produkt podle ID</span><span class="sxs-lookup"><span data-stu-id="189f6-227">Get a product by ID</span></span> | <span data-ttu-id="189f6-228">GET</span><span class="sxs-lookup"><span data-stu-id="189f6-228">GET</span></span> | <span data-ttu-id="189f6-229">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="189f6-229">/api/products/*id*</span></span> |
| <span data-ttu-id="189f6-230">Získat produkt podle kategorie</span><span class="sxs-lookup"><span data-stu-id="189f6-230">Get a product by category</span></span> | <span data-ttu-id="189f6-231">GET</span><span class="sxs-lookup"><span data-stu-id="189f6-231">GET</span></span> | <span data-ttu-id="189f6-232">/API/Products? kategorie =*kategorie*</span><span class="sxs-lookup"><span data-stu-id="189f6-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="189f6-233">Chcete-li získat seznam všech produktů, přidejte tuto metodu do třídy `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="189f6-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="189f6-234">Název metody začíná na &quot;získat&quot;, tak podle konvence, kterou mapuje na požadavky GET.</span><span class="sxs-lookup"><span data-stu-id="189f6-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="189f6-235">Vzhledem k tomu, že metoda nemá žádné parametry, je namapována na identifikátor URI, který neobsahuje *&quot;id&quot;* segmentu v cestě.</span><span class="sxs-lookup"><span data-stu-id="189f6-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="189f6-236">Chcete-li získat produkt podle ID, přidejte tuto metodu do třídy `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="189f6-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="189f6-237">Tento název metody také začíná &quot;získat&quot;, ale metoda má parametr s názvem *ID*. Tento parametr je namapován na &quot;ID&quot; segmentu cesty identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="189f6-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="189f6-238">Rozhraní Web API pro ASP.NET automaticky převede ID na správný datový typ (**int**) pro parametr.</span><span class="sxs-lookup"><span data-stu-id="189f6-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="189f6-239">Metoda getproduct vyvolá výjimku typu **HttpResponseException** , pokud *ID* je neplatné.</span><span class="sxs-lookup"><span data-stu-id="189f6-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="189f6-240">Tato výjimka bude přeložena rozhraním do chyby 404 (Nenalezeno).</span><span class="sxs-lookup"><span data-stu-id="189f6-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="189f6-241">Nakonec přidejte metodu pro vyhledání produktů podle kategorie:</span><span class="sxs-lookup"><span data-stu-id="189f6-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="189f6-242">Pokud má identifikátor URI žádosti řetězec dotazu, webové rozhraní API se pokusí porovnat parametry dotazu s parametry v metodě kontroleru.</span><span class="sxs-lookup"><span data-stu-id="189f6-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="189f6-243">Proto se identifikátor URI ve formátu "API/Products? kategorie =*Category*" namapuje na tuto metodu.</span><span class="sxs-lookup"><span data-stu-id="189f6-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="189f6-244">Vytvoření prostředku</span><span class="sxs-lookup"><span data-stu-id="189f6-244">Creating a Resource</span></span>

<span data-ttu-id="189f6-245">Dále přidáme metodu do třídy `ProductsController` pro vytvoření nového produktu.</span><span class="sxs-lookup"><span data-stu-id="189f6-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="189f6-246">Tady je jednoduchá implementace metody:</span><span class="sxs-lookup"><span data-stu-id="189f6-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="189f6-247">Všimněte si, že tato metoda má dvě věci:</span><span class="sxs-lookup"><span data-stu-id="189f6-247">Note two things about this method:</span></span>

- <span data-ttu-id="189f6-248">Název metody začíná &quot;post...&quot;.</span><span class="sxs-lookup"><span data-stu-id="189f6-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="189f6-249">Pokud chcete vytvořit nový produkt, klient odešle požadavek HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="189f6-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="189f6-250">Metoda přijímá parametr typu produkt.</span><span class="sxs-lookup"><span data-stu-id="189f6-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="189f6-251">V rozhraní Web API jsou parametry se složitými typy deserializovány z textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="189f6-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="189f6-252">Očekáváme proto, že klient pošle serializovanou reprezentaci objektu produktu ve formátu XML nebo JSON.</span><span class="sxs-lookup"><span data-stu-id="189f6-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="189f6-253">Tato implementace bude fungovat, ale není poměrně kompletní.</span><span class="sxs-lookup"><span data-stu-id="189f6-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="189f6-254">V ideálním případě chceme, aby odpověď protokolu HTTP zahrnovala tyto věci:</span><span class="sxs-lookup"><span data-stu-id="189f6-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="189f6-255">**Kód odpovědi:** Ve výchozím nastavení rozhraní Web API nastaví stavový kód odpovědi na 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="189f6-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="189f6-256">Pokud je v závislosti na protokolu HTTP/1.1 výsledkem žádosti POST vytvoření prostředku, server by měl odpovědět na stav 201 (vytvořeno).</span><span class="sxs-lookup"><span data-stu-id="189f6-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="189f6-257">**Umístění:** Když server vytvoří prostředek, měl by obsahovat identifikátor URI nového prostředku v hlavičce umístění odpovědi.</span><span class="sxs-lookup"><span data-stu-id="189f6-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="189f6-258">Webové rozhraní API pro ASP.NET usnadňuje zpracování zprávy s odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="189f6-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="189f6-259">Tady je vylepšená implementace:</span><span class="sxs-lookup"><span data-stu-id="189f6-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="189f6-260">Všimněte si, že návratový typ metody je nyní **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="189f6-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="189f6-261">Vrácením **HttpResponseMessage** namísto produktu můžeme řídit podrobnosti zprávy s odpovědí HTTP, včetně stavového kódu a hlavičky umístění.</span><span class="sxs-lookup"><span data-stu-id="189f6-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="189f6-262">Metoda **CreateResponse** vytvoří **HttpResponseMessage** a automaticky zapíše serializovanou reprezentaci objektu produktu do těla zprávy odpovědi.</span><span class="sxs-lookup"><span data-stu-id="189f6-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="189f6-263">Tento příklad neověřuje `Product`.</span><span class="sxs-lookup"><span data-stu-id="189f6-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="189f6-264">Informace o ověřování modelu najdete v tématu [ověřování modelu v ASP.NET webovém rozhraní API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="189f6-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="189f6-265">Aktualizace prostředku</span><span class="sxs-lookup"><span data-stu-id="189f6-265">Updating a Resource</span></span>

<span data-ttu-id="189f6-266">Aktualizace produktu pomocí PUT je jednoduchá:</span><span class="sxs-lookup"><span data-stu-id="189f6-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="189f6-267">Název metody začíná na &quot;PUT...&quot;, takže webové rozhraní API odpovídá na vložení požadavků.</span><span class="sxs-lookup"><span data-stu-id="189f6-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="189f6-268">Metoda přijímá dva parametry, ID produktu a aktualizovaný produkt.</span><span class="sxs-lookup"><span data-stu-id="189f6-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="189f6-269">Parametr *ID* je pořízen z cesty identifikátoru URI a parametr *produktu* je deserializovaný z textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="189f6-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="189f6-270">Ve výchozím nastavení přebírá rozhraní Web API ASP.NET jednoduché typy parametrů z trasy a komplexní typy z textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="189f6-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="189f6-271">Odstranění prostředku</span><span class="sxs-lookup"><span data-stu-id="189f6-271">Deleting a Resource</span></span>

<span data-ttu-id="189f6-272">Chcete-li odstranit prostředek, definujte "Delete..." Metoda.</span><span class="sxs-lookup"><span data-stu-id="189f6-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="189f6-273">Pokud je žádost o odstranění úspěšná, může vrátit stav 200 (OK) s tělem entity, které popisuje stav. stav 202 (přijato), pokud odstranění stále čeká na vyřízení; nebo stav 204 (žádný obsah) bez těla entity</span><span class="sxs-lookup"><span data-stu-id="189f6-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="189f6-274">V takovém případě má `DeleteProduct` metoda `void` návratový typ, takže webové rozhraní API ASP.NET automaticky přeloží tento kód stavu 204 (žádný obsah).</span><span class="sxs-lookup"><span data-stu-id="189f6-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
