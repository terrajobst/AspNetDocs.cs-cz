---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: Začínáme s webovým rozhraním API ASP.NETC#() – ASP.NET 4. x
author: MikeWasson
description: Kurz s kódem. Pomocí webového rozhraní API ASP.NET můžete vytvořit webové rozhraní API, které vrátí seznam produktů.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 2717d93f47be9d4a6548731d8deeca312b25f39f
ms.sourcegitcommit: 9e3ca74997a67c18589729d4b7303799905473eb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/11/2020
ms.locfileid: "79084051"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="09178-104">Začínáme s webovým rozhraním API 2C#() pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="09178-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="09178-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="09178-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="09178-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="09178-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="09178-107">V tomto kurzu použijete webové rozhraní API ASP.NET k vytvoření webového rozhraní API, které vrátí seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="09178-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="09178-108">HTTP není pouze pro obsluhu webových stránek.</span><span class="sxs-lookup"><span data-stu-id="09178-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="09178-109">HTTP je také výkonná platforma pro vytváření rozhraní API, která zveřejňují služby a data.</span><span class="sxs-lookup"><span data-stu-id="09178-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="09178-110">HTTP je jednoduché, flexibilní a všudypřítomný.</span><span class="sxs-lookup"><span data-stu-id="09178-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="09178-111">Skoro libovolná platforma, na kterou si můžete představit, má knihovnu HTTP, takže služby HTTP mohou dosáhnout široké škály klientů, včetně prohlížečů, mobilních zařízení a tradičních aplikací klasické pracovní plochy.</span><span class="sxs-lookup"><span data-stu-id="09178-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="09178-112">Webové rozhraní API ASP.NET je rozhraní pro vytváření webových rozhraní API nad .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="09178-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="09178-113">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="09178-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="09178-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="09178-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="09178-115">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="09178-115">Web API 2</span></span>

<span data-ttu-id="09178-116">Novější verzi tohoto kurzu najdete v tématu [Vytvoření webového rozhraní API s ASP.NET Core a sadou Visual Studio pro Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) .</span><span class="sxs-lookup"><span data-stu-id="09178-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="09178-117">Vytvoření projektu webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="09178-117">Create a Web API Project</span></span>

<span data-ttu-id="09178-118">V tomto kurzu použijete webové rozhraní API ASP.NET k vytvoření webového rozhraní API, které vrátí seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="09178-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="09178-119">Webová stránka front-end používá jQuery k zobrazení výsledků.</span><span class="sxs-lookup"><span data-stu-id="09178-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="09178-120">Spusťte Visual Studio a na **úvodní** stránce vyberte **Nový projekt** .</span><span class="sxs-lookup"><span data-stu-id="09178-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="09178-121">Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.</span><span class="sxs-lookup"><span data-stu-id="09178-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="09178-122">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** .</span><span class="sxs-lookup"><span data-stu-id="09178-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="09178-123">V **části C#vizuál** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="09178-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="09178-124">V seznamu šablon projektu vyberte **ASP.NET webová aplikace**.</span><span class="sxs-lookup"><span data-stu-id="09178-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="09178-125">Pojmenujte projekt "ProductsApp" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="09178-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="09178-126">V dialogovém okně **Nový projekt ASP.NET** vyberte **prázdnou** šablonu.</span><span class="sxs-lookup"><span data-stu-id="09178-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="09178-127">V části &quot;přidat složky a základní reference pro&quot;zaškrtněte **webové rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="09178-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="09178-128">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="09178-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="09178-129">Můžete také vytvořit projekt webového rozhraní API pomocí šablony &quot;Web API&quot;.</span><span class="sxs-lookup"><span data-stu-id="09178-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="09178-130">Šablona webového rozhraní API používá ASP.NET MVC k poskytnutí stránek s nápovědě k rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="09178-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="09178-131">Používám prázdnou šablonu pro tento kurz, protože chci zobrazit webové rozhraní API bez MVC.</span><span class="sxs-lookup"><span data-stu-id="09178-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="09178-132">Obecně platí, že k používání webového rozhraní API nemusíte znát ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="09178-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="09178-133">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="09178-133">Adding a Model</span></span>

<span data-ttu-id="09178-134">*Model* je objekt, který představuje data v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="09178-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="09178-135">Webové rozhraní API ASP.NET může model automaticky serializovat do formátu JSON, XML nebo jiného formátu a pak zapsat Serializovaná data do těla zprávy odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="09178-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="09178-136">Pokud klient může číst formát serializace, může objekt deserializovat.</span><span class="sxs-lookup"><span data-stu-id="09178-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="09178-137">Většina klientů může analyzovat kód XML nebo JSON.</span><span class="sxs-lookup"><span data-stu-id="09178-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="09178-138">Kromě toho může klient určit, který formát chce, nastavením hlavičky Accept ve zprávě požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="09178-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="09178-139">Pojďme začít vytvořením jednoduchého modelu, který představuje produkt.</span><span class="sxs-lookup"><span data-stu-id="09178-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="09178-140">Pokud Průzkumník řešení ještě není vidět, klikněte na nabídku **zobrazení** a vyberte možnost **Průzkumník řešení**.</span><span class="sxs-lookup"><span data-stu-id="09178-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="09178-141">V Průzkumník řešení klikněte pravým tlačítkem na složku modely.</span><span class="sxs-lookup"><span data-stu-id="09178-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="09178-142">V místní nabídce vyberte **Přidat** a pak vyberte **Třída**.</span><span class="sxs-lookup"><span data-stu-id="09178-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="09178-143">Pojmenujte třídu &quot;&quot;produktu.</span><span class="sxs-lookup"><span data-stu-id="09178-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="09178-144">Do třídy `Product` přidejte následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="09178-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="09178-145">Přidání kontroleru</span><span class="sxs-lookup"><span data-stu-id="09178-145">Adding a Controller</span></span>

<span data-ttu-id="09178-146">Ve webovém rozhraní API je *kontroler* objekt, který zpracovává požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="09178-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="09178-147">Přidáme kontroler, který může vracet buď seznam produktů, nebo jeden produkt určený IDENTIFIKÁTORem.</span><span class="sxs-lookup"><span data-stu-id="09178-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="09178-148">Pokud jste použili ASP.NET MVC, už jste obeznámeni s řadiči.</span><span class="sxs-lookup"><span data-stu-id="09178-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="09178-149">Řadiče webového rozhraní API se podobají řadičům MVC, ale dědí třídu **ApiController** namísto třídy **Controller** .</span><span class="sxs-lookup"><span data-stu-id="09178-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="09178-150">V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="09178-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="09178-151">Vyberte **Přidat** a pak vybrat **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="09178-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="09178-152">V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte možnost **KONTROLER webového rozhraní API – prázdné**.</span><span class="sxs-lookup"><span data-stu-id="09178-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="09178-153">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="09178-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="09178-154">V dialogovém okně **Přidat řadič** pojmenujte kontrolér &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="09178-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="09178-155">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="09178-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="09178-156">Generování uživatelského rozhraní vytvoří ve složce Controllers soubor s názvem ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="09178-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="09178-157">Řadiče nemusíte vkládat do složky s názvem Controllers.</span><span class="sxs-lookup"><span data-stu-id="09178-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="09178-158">Název složky je pouze pohodlný způsob, jak uspořádat zdrojové soubory.</span><span class="sxs-lookup"><span data-stu-id="09178-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="09178-159">Pokud tento soubor ještě není otevřený, otevřete ho tak, že na něj dvakrát kliknete.</span><span class="sxs-lookup"><span data-stu-id="09178-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="09178-160">Nahraďte kód v tomto souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="09178-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="09178-161">Aby byl příklad jednoduchý, produkty jsou uloženy v pevném poli uvnitř třídy Controller.</span><span class="sxs-lookup"><span data-stu-id="09178-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="09178-162">Samozřejmě můžete v reálné aplikaci zadat dotaz na databázi nebo použít jiný externí zdroj dat.</span><span class="sxs-lookup"><span data-stu-id="09178-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="09178-163">Kontroler definuje dvě metody, které vracejí produkty:</span><span class="sxs-lookup"><span data-stu-id="09178-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="09178-164">Metoda `GetAllProducts` vrátí celý seznam produktů jako typ **&gt;&lt;typu produktu IEnumerable** .</span><span class="sxs-lookup"><span data-stu-id="09178-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="09178-165">Metoda `GetProduct` vyhledá jeden produkt podle jeho ID.</span><span class="sxs-lookup"><span data-stu-id="09178-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="09178-166">A to je vše!</span><span class="sxs-lookup"><span data-stu-id="09178-166">That's it!</span></span> <span data-ttu-id="09178-167">Máte funkční webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="09178-167">You have a working web API.</span></span> <span data-ttu-id="09178-168">Každá metoda na kontroleru odpovídá jednomu nebo více identifikátorům URI:</span><span class="sxs-lookup"><span data-stu-id="09178-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="09178-169">Metoda kontroleru</span><span class="sxs-lookup"><span data-stu-id="09178-169">Controller Method</span></span> | <span data-ttu-id="09178-170">URI</span><span class="sxs-lookup"><span data-stu-id="09178-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="09178-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="09178-171">GetAllProducts</span></span> | <span data-ttu-id="09178-172">/api/products</span><span class="sxs-lookup"><span data-stu-id="09178-172">/api/products</span></span> |
| <span data-ttu-id="09178-173">Getproduct</span><span class="sxs-lookup"><span data-stu-id="09178-173">GetProduct</span></span> | <span data-ttu-id="09178-174">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="09178-174">/api/products/*id*</span></span> |

<span data-ttu-id="09178-175">Pro metodu `GetProduct` je *ID* v identifikátoru URI zástupný symbol.</span><span class="sxs-lookup"><span data-stu-id="09178-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="09178-176">Chcete-li například získat produkt s ID 5, je identifikátor URI `api/products/5`.</span><span class="sxs-lookup"><span data-stu-id="09178-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="09178-177">Další informace o tom, jak webové rozhraní API směruje požadavky HTTP na metody kontroleru, najdete v tématu [směrování ve webovém rozhraní api ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="09178-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="09178-178">Volání webového rozhraní API pomocí JavaScriptu a jQuery</span><span class="sxs-lookup"><span data-stu-id="09178-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="09178-179">V této části přidáme stránku HTML, která pro volání webového rozhraní API používá AJAX.</span><span class="sxs-lookup"><span data-stu-id="09178-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="09178-180">Pomocí jQuery provedeme volání AJAX a také aktualizujeme stránku s výsledky.</span><span class="sxs-lookup"><span data-stu-id="09178-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="09178-181">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost **Přidat**a pak vyberte možnost **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="09178-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="09178-182">V dialogovém okně **Přidat novou položku** vyberte v části **vizuál C#** uzel **Web** a pak vyberte položku **stránky HTML** .</span><span class="sxs-lookup"><span data-stu-id="09178-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="09178-183">Pojmenujte stránku &quot;index. html&quot;.</span><span class="sxs-lookup"><span data-stu-id="09178-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="09178-184">Nahraďte vše v tomto souboru následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="09178-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="09178-185">Existuje několik způsobů, jak získat jQuery.</span><span class="sxs-lookup"><span data-stu-id="09178-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="09178-186">V tomto příkladu jsem použil [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span><span class="sxs-lookup"><span data-stu-id="09178-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="09178-187">Můžete si ho také stáhnout z [http://jquery.com/](http://jquery.com/)a šablona projektu ASP.NET "webové rozhraní API" zahrnuje také jQuery.</span><span class="sxs-lookup"><span data-stu-id="09178-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="09178-188">Získání seznamu produktů</span><span class="sxs-lookup"><span data-stu-id="09178-188">Getting a List of Products</span></span>

<span data-ttu-id="09178-189">Pokud chcete získat seznam produktů, odešlete požadavek HTTP GET na &quot;/API/Products&quot;.</span><span class="sxs-lookup"><span data-stu-id="09178-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="09178-190">Funkce jQuery [getjson](http://api.jquery.com/jQuery.getJSON/) pošle požadavek AJAX.</span><span class="sxs-lookup"><span data-stu-id="09178-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="09178-191">Odpověď obsahuje pole objektů JSON.</span><span class="sxs-lookup"><span data-stu-id="09178-191">The response contains array of JSON objects.</span></span> <span data-ttu-id="09178-192">Funkce `done` určuje zpětné volání, které je voláno, pokud je požadavek úspěšný.</span><span class="sxs-lookup"><span data-stu-id="09178-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="09178-193">Ve zpětném volání aktualizujeme model DOM informacemi o produktu.</span><span class="sxs-lookup"><span data-stu-id="09178-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="09178-194">Získání produktu podle ID</span><span class="sxs-lookup"><span data-stu-id="09178-194">Getting a Product By ID</span></span>

<span data-ttu-id="09178-195">Pokud chcete získat produkt podle ID, odešlete požadavek HTTP GET na &quot;*ID* /API/Products/&quot;, kde *ID* je ID produktu.</span><span class="sxs-lookup"><span data-stu-id="09178-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="09178-196">Pořád budeme volat `getJSON` k odeslání požadavku AJAX, ale tentokrát vložíme ID do identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="09178-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="09178-197">Odpověď z tohoto požadavku je reprezentace jediného produktu ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="09178-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="09178-198">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="09178-198">Running the Application</span></span>

<span data-ttu-id="09178-199">Stisknutím klávesy F5 spusťte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="09178-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="09178-200">Webová stránka by měla vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="09178-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="09178-201">Pokud chcete získat produkt podle ID, zadejte ID a klikněte na Hledat:</span><span class="sxs-lookup"><span data-stu-id="09178-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="09178-202">Pokud zadáte neplatné ID, server vrátí chybu protokolu HTTP:</span><span class="sxs-lookup"><span data-stu-id="09178-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="09178-203">Použití nástroje F12 k zobrazení žádosti a odpovědi HTTP</span><span class="sxs-lookup"><span data-stu-id="09178-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="09178-204">Když pracujete se službou HTTP, může být velmi užitečné, abyste zobrazili zprávy s požadavkem a odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="09178-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and response messages.</span></span> <span data-ttu-id="09178-205">To můžete provést pomocí vývojářských nástrojů F12 v aplikaci Internet Explorer 9.</span><span class="sxs-lookup"><span data-stu-id="09178-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="09178-206">V aplikaci Internet Explorer 9 otevřete stisknutím klávesy **F12** nástroje.</span><span class="sxs-lookup"><span data-stu-id="09178-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="09178-207">Klikněte na kartu **síť** a potom stiskněte **Spustit zachytávání**.</span><span class="sxs-lookup"><span data-stu-id="09178-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="09178-208">Nyní se vraťte na webovou stránku a stisknutím klávesy **F5** znovu načtěte webovou stránku.</span><span class="sxs-lookup"><span data-stu-id="09178-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="09178-209">Internet Explorer bude zachytit přenos HTTP mezi prohlížečem a webovým serverem.</span><span class="sxs-lookup"><span data-stu-id="09178-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="09178-210">V souhrnném zobrazení se zobrazuje veškerá síťová komunikace pro stránku:</span><span class="sxs-lookup"><span data-stu-id="09178-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="09178-211">Vyhledejte položku relativního identifikátoru URI "API/Products/".</span><span class="sxs-lookup"><span data-stu-id="09178-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="09178-212">Vyberte tuto položku a klikněte na **Přejít k podrobnému zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="09178-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="09178-213">V podrobném zobrazení jsou k dispozici karty pro zobrazení požadavků a hlaviček odpovědí.</span><span class="sxs-lookup"><span data-stu-id="09178-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="09178-214">Pokud například kliknete na kartu **hlavičky žádosti** , vidíte, že klient požádal o &quot;aplikace/JSON&quot; v hlavičce Accept.</span><span class="sxs-lookup"><span data-stu-id="09178-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="09178-215">Pokud kliknete na kartu tělo odpovědi, uvidíte, jak se seznam produktů serializován do formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="09178-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="09178-216">Jiné prohlížeče mají podobné funkce.</span><span class="sxs-lookup"><span data-stu-id="09178-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="09178-217">Dalším užitečným nástrojem je [Fiddler](http://www.fiddler2.com/fiddler2/), webový ladicí proxy server.</span><span class="sxs-lookup"><span data-stu-id="09178-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="09178-218">Fiddler můžete použít k zobrazení provozu protokolu HTTP a také k vytvoření požadavků HTTP, které vám umožní plnou kontrolu hlaviček protokolu HTTP v žádosti.</span><span class="sxs-lookup"><span data-stu-id="09178-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="09178-219">Podívejte se na tuto aplikaci spuštěnou v Azure</span><span class="sxs-lookup"><span data-stu-id="09178-219">See this App Running on Azure</span></span>

<span data-ttu-id="09178-220">Chcete zobrazit dokončený web běžící jako živá webová aplikace?</span><span class="sxs-lookup"><span data-stu-id="09178-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="09178-221">Úplnou verzi aplikace můžete nasadit do svého účtu Azure pouhým kliknutím na následující tlačítko.</span><span class="sxs-lookup"><span data-stu-id="09178-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="09178-222">K nasazení tohoto řešení do Azure potřebujete účet Azure.</span><span class="sxs-lookup"><span data-stu-id="09178-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="09178-223">Pokud ještě nemáte účet, máte následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="09178-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="09178-224">[Otevřete si bezplatný účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.</span><span class="sxs-lookup"><span data-stu-id="09178-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="09178-225">[Aktivujte výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) – vaše předplatné MSDN vám každý měsíc dává kredity, které můžete použít pro placené služby Azure.</span><span class="sxs-lookup"><span data-stu-id="09178-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09178-226">Další kroky</span><span class="sxs-lookup"><span data-stu-id="09178-226">Next Steps</span></span>

- <span data-ttu-id="09178-227">Úplnější příklad služby HTTP, která podporuje akce POST, PUT a DELETE a zápisy do databáze, najdete v tématu [použití webového rozhraní API 2 s Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span><span class="sxs-lookup"><span data-stu-id="09178-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="09178-228">Další informace o vytváření kapalinových a reagujících webových aplikací nad službou HTTP najdete v tématu [aplikace ASP.NET Single Page](../../../single-page-application/index.md).</span><span class="sxs-lookup"><span data-stu-id="09178-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="09178-229">Informace o tom, jak nasadit webový projekt aplikace Visual Studio do Azure App Service, najdete [v tématu Vytvoření webové aplikace v ASP.NET v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="09178-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
