---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Volání webového rozhraní API z klienta .NET (C#) | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 11/24/2017
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 0c360f580285967c8fab8d33ccbb9557a7316ee1
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423134"
---
<a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="2c901-102">Volání webového rozhraní API z klienta .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="2c901-102">Call a Web API From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="2c901-103">podle [Mike Wasson](https://github.com/MikeWasson) a [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2c901-103">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="2c901-104">[Stáhnout dokončený projekt](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="2c901-104">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="2c901-105">[Pokyny ke stažení](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="2c901-105">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="2c901-106">Tento kurz ukazuje postupy při zavolání webového rozhraní API z aplikace .NET pomocí [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="2c901-106">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="2c901-107">V tomto kurzu je zapsán klientskou aplikaci, že následující webové rozhraní API, který využívá:</span><span class="sxs-lookup"><span data-stu-id="2c901-107">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="2c901-108">Akce</span><span class="sxs-lookup"><span data-stu-id="2c901-108">Action</span></span> | <span data-ttu-id="2c901-109">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="2c901-109">HTTP method</span></span> | <span data-ttu-id="2c901-110">Relativní identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="2c901-110">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c901-111">Získání produktu podle ID</span><span class="sxs-lookup"><span data-stu-id="2c901-111">Get a product by ID</span></span> | <span data-ttu-id="2c901-112">GET</span><span class="sxs-lookup"><span data-stu-id="2c901-112">GET</span></span> | <span data-ttu-id="2c901-113">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="2c901-113">/api/products/*id*</span></span> |
| <span data-ttu-id="2c901-114">Vytvořit nový produkt</span><span class="sxs-lookup"><span data-stu-id="2c901-114">Create a new product</span></span> | <span data-ttu-id="2c901-115">POST</span><span class="sxs-lookup"><span data-stu-id="2c901-115">POST</span></span> | <span data-ttu-id="2c901-116">/ api/produkty</span><span class="sxs-lookup"><span data-stu-id="2c901-116">/api/products</span></span> |
| <span data-ttu-id="2c901-117">Aktualizace produktu</span><span class="sxs-lookup"><span data-stu-id="2c901-117">Update a product</span></span> | <span data-ttu-id="2c901-118">PUT</span><span class="sxs-lookup"><span data-stu-id="2c901-118">PUT</span></span> | <span data-ttu-id="2c901-119">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="2c901-119">/api/products/*id*</span></span> |
| <span data-ttu-id="2c901-120">Odstranit produkt</span><span class="sxs-lookup"><span data-stu-id="2c901-120">Delete a product</span></span> | <span data-ttu-id="2c901-121">DELETE</span><span class="sxs-lookup"><span data-stu-id="2c901-121">DELETE</span></span> | <span data-ttu-id="2c901-122">/ webové rozhraníAPI/produkty/*id*</span><span class="sxs-lookup"><span data-stu-id="2c901-122">/api/products/*id*</span></span> |

<span data-ttu-id="2c901-123">Další postup implementace tohoto rozhraní API s rozhraním ASP.NET Web API najdete v tématu [této operace CRUD podporuje vytvoření webového rozhraní API](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="2c901-123">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="2c901-124">Pro jednoduchost klientská aplikace v tomto kurzu je konzolová aplikace Windows.</span><span class="sxs-lookup"><span data-stu-id="2c901-124">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="2c901-125">**HttpClient** je také podporována pro aplikace pro Windows Phone a Windows Store.</span><span class="sxs-lookup"><span data-stu-id="2c901-125">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="2c901-126">Další informace najdete v tématu [psaní webové rozhraní API klienta kódu pro více platforem, pomocí přenosné knihovny](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="2c901-126">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="2c901-127">Vytvoření konzolové aplikace</span><span class="sxs-lookup"><span data-stu-id="2c901-127">Create the Console Application</span></span>

<span data-ttu-id="2c901-128">V sadě Visual Studio vytvořte novou konzolovou aplikaci s Windows s názvem **HttpClientSample** a vložte následující kód:</span><span class="sxs-lookup"><span data-stu-id="2c901-128">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="2c901-129">Předchozí kód je kompletní klientské aplikace.</span><span class="sxs-lookup"><span data-stu-id="2c901-129">The preceding code is the complete client app.</span></span>

<span data-ttu-id="2c901-130">`RunAsync` spuštění a blokuje, dokud se nedokončí.</span><span class="sxs-lookup"><span data-stu-id="2c901-130">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="2c901-131">Většina **HttpClient** metody jsou asynchronní, protože jejich provádění v / v sítě.</span><span class="sxs-lookup"><span data-stu-id="2c901-131">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="2c901-132">Všechny asynchronní úlohy dokončení uvnitř `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="2c901-132">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="2c901-133">Obvykle aplikace nebrání v hlavním vlákně, ale tuto aplikaci neumožňuje zásahu.</span><span class="sxs-lookup"><span data-stu-id="2c901-133">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="2c901-134">Instalace webové rozhraní API klientské knihovny</span><span class="sxs-lookup"><span data-stu-id="2c901-134">Install the Web API Client Libraries</span></span>

<span data-ttu-id="2c901-135">Použití Správce balíčků NuGet nainstalujte balíček webové rozhraní API klientské knihovny.</span><span class="sxs-lookup"><span data-stu-id="2c901-135">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="2c901-136">Z **nástroje** nabídce vyberte možnost **Správce balíčků NuGet** > **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="2c901-136">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="2c901-137">V balíčku správce konzoly (konzolu PMC), zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="2c901-137">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="2c901-138">Ve výstupu předchozího příkazu přidá následující balíčky NuGet do projektu:</span><span class="sxs-lookup"><span data-stu-id="2c901-138">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="2c901-139">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="2c901-139">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="2c901-140">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="2c901-140">Newtonsoft.Json</span></span>

<span data-ttu-id="2c901-141">Json.NET je oblíbená architektura výkonné JSON pro .NET.</span><span class="sxs-lookup"><span data-stu-id="2c901-141">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="2c901-142">Přidejte třídu modelu</span><span class="sxs-lookup"><span data-stu-id="2c901-142">Add a Model Class</span></span>

<span data-ttu-id="2c901-143">Zkontrolujte `Product` třídy:</span><span class="sxs-lookup"><span data-stu-id="2c901-143">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="2c901-144">Tato třída odpovídá datového modelu používají webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2c901-144">This class matches the data model used by the web API.</span></span> <span data-ttu-id="2c901-145">Můžete použít aplikaci **HttpClient** ke čtení `Product` instanci z odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c901-145">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="2c901-146">Aplikace nebude muset psát kód deserializace.</span><span class="sxs-lookup"><span data-stu-id="2c901-146">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="2c901-147">Vytváření a inicializace HttpClient</span><span class="sxs-lookup"><span data-stu-id="2c901-147">Create and Initialize HttpClient</span></span>

<span data-ttu-id="2c901-148">Prozkoumejte statické **HttpClient** vlastnost:</span><span class="sxs-lookup"><span data-stu-id="2c901-148">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="2c901-149">**HttpClient** by se měly vytvořit jednou a opětovně používat v rámci životnosti aplikace.</span><span class="sxs-lookup"><span data-stu-id="2c901-149">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="2c901-150">Následující podmínky mohou způsobit **socketexception –** chyby:</span><span class="sxs-lookup"><span data-stu-id="2c901-150">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="2c901-151">Vytvoření nového **HttpClient** instance pro každý požadavek.</span><span class="sxs-lookup"><span data-stu-id="2c901-151">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="2c901-152">Server v případě velkého zatížení.</span><span class="sxs-lookup"><span data-stu-id="2c901-152">Server under heavy load.</span></span>

<span data-ttu-id="2c901-153">Vytvoření nového **HttpClient** instance pro každý požadavek lze vyčerpání dostupných soketů.</span><span class="sxs-lookup"><span data-stu-id="2c901-153">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="2c901-154">V následujícím kódu inicializuje **HttpClient** instance:</span><span class="sxs-lookup"><span data-stu-id="2c901-154">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="2c901-155">Předchozí kód:</span><span class="sxs-lookup"><span data-stu-id="2c901-155">The preceding code:</span></span>

* <span data-ttu-id="2c901-156">Nastaví základní identifikátor URI pro požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c901-156">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="2c901-157">Změňte číslo portu na port v serveru aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2c901-157">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="2c901-158">Aplikace nebude fungovat, pokud se používá port pro serverovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2c901-158">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="2c901-159">Nastaví hlavičku Accept na "application/json".</span><span class="sxs-lookup"><span data-stu-id="2c901-159">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="2c901-160">Nastavení této hlavičky určuje server k odesílání dat ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="2c901-160">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="2c901-161">Odeslat požadavek GET na načtení prostředku</span><span class="sxs-lookup"><span data-stu-id="2c901-161">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="2c901-162">Následující kód odešle požadavek GET pro produkt:</span><span class="sxs-lookup"><span data-stu-id="2c901-162">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="2c901-163">**GetAsync** metoda odešle požadavek HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="2c901-163">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="2c901-164">Když dokončení metody, vrátí **objekt HttpResponseMessage** , který obsahuje odpověď HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c901-164">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="2c901-165">Pokud stavový kód odpovědi na kód úspěchu, tělo odpovědi obsahuje reprezentaci JSON produktu.</span><span class="sxs-lookup"><span data-stu-id="2c901-165">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="2c901-166">Volání **ReadAsAsync** datovou část JSON k deserializaci `Product` instance.</span><span class="sxs-lookup"><span data-stu-id="2c901-166">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="2c901-167">**ReadAsAsync** metoda je asynchronní, protože tělo odpovědi může být libovolně velké.</span><span class="sxs-lookup"><span data-stu-id="2c901-167">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="2c901-168">**HttpClient** nevyvolá výjimku, pokud odpověď HTTP, která obsahuje kód chyby.</span><span class="sxs-lookup"><span data-stu-id="2c901-168">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="2c901-169">Místo toho **IsSuccessStatusCode** vlastnost je **false** -li stav nastaven chybový kód.</span><span class="sxs-lookup"><span data-stu-id="2c901-169">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="2c901-170">Pokud chcete přistupovat ke všem chybových kódech HTTP jako výjimky, volání [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) v objektu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="2c901-170">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="2c901-171">`EnsureSuccessStatusCode` vyvolá výjimku, pokud se stavovým kódem spadá mimo rozsah 200&ndash;299.</span><span class="sxs-lookup"><span data-stu-id="2c901-171">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="2c901-172">Všimněte si, že **HttpClient** může vyvolat výjimky z jiných důvodů &mdash; například, pokud vyprší časový limit žádosti.</span><span class="sxs-lookup"><span data-stu-id="2c901-172">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="2c901-173">Formátovací moduly typu médií k deserializaci</span><span class="sxs-lookup"><span data-stu-id="2c901-173">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="2c901-174">Když **ReadAsAsync** je volána bez parametrů, použije výchozí sadu *formátovací moduly médií* ke čtení textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="2c901-174">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="2c901-175">Výchozí formátování Podpora JSON, XML a data formuláře kódovaná adresy url.</span><span class="sxs-lookup"><span data-stu-id="2c901-175">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="2c901-176">Místo použití výchozí formátování, můžete zadat seznam formátovacích modulů k **ReadAsAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="2c901-176">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="2c901-177">Použití seznam formátovacích modulů je užitečné, pokud máte vlastní typ média formátování:</span><span class="sxs-lookup"><span data-stu-id="2c901-177">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="2c901-178">Další informace najdete v tématu [formátovací moduly médií ve ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="2c901-178">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="2c901-179">Odeslání požadavku POST vytvořit prostředek</span><span class="sxs-lookup"><span data-stu-id="2c901-179">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="2c901-180">Následující kód odešle požadavek POST, který obsahuje `Product` instance ve formátu JSON:</span><span class="sxs-lookup"><span data-stu-id="2c901-180">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="2c901-181">**PostAsJsonAsync** metody:</span><span class="sxs-lookup"><span data-stu-id="2c901-181">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="2c901-182">Serializuje objekt do formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="2c901-182">Serializes an object to JSON.</span></span>
* <span data-ttu-id="2c901-183">Odešle datové části JSON v požadavku POST.</span><span class="sxs-lookup"><span data-stu-id="2c901-183">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="2c901-184">Pokud je žádost úspěšná:</span><span class="sxs-lookup"><span data-stu-id="2c901-184">If the request succeeds:</span></span>

* <span data-ttu-id="2c901-185">Měla by vrátit odpověď 201 (vytvořeno).</span><span class="sxs-lookup"><span data-stu-id="2c901-185">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="2c901-186">Má odpověď obsahovat adresu URL vytvořené prostředky v hlavičce Location.</span><span class="sxs-lookup"><span data-stu-id="2c901-186">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="2c901-187">Odesílání požadavek PUT pro aktualizace prostředku</span><span class="sxs-lookup"><span data-stu-id="2c901-187">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="2c901-188">Následující kód odešle požadavek PUT pro aktualizaci produktu:</span><span class="sxs-lookup"><span data-stu-id="2c901-188">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="2c901-189">**PutAsJsonAsync** metoda se dá použít jako **PostAsJsonAsync**, s tím rozdílem, že odešle žádost PUT místo příspěvku.</span><span class="sxs-lookup"><span data-stu-id="2c901-189">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="2c901-190">Odesílání požadavku na odstranění odstranění prostředku</span><span class="sxs-lookup"><span data-stu-id="2c901-190">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="2c901-191">Následující kód odešle žádost o odstranění se odstranit produkt:</span><span class="sxs-lookup"><span data-stu-id="2c901-191">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="2c901-192">Třeba GET žádost o odstranění nemá tělo požadavku.</span><span class="sxs-lookup"><span data-stu-id="2c901-192">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="2c901-193">Není nutné zadat ve formátu JSON nebo XML DELETE.</span><span class="sxs-lookup"><span data-stu-id="2c901-193">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="2c901-194">Testování ukázky</span><span class="sxs-lookup"><span data-stu-id="2c901-194">Test the sample</span></span>

<span data-ttu-id="2c901-195">Testování aplikace klienta:</span><span class="sxs-lookup"><span data-stu-id="2c901-195">To test the client app:</span></span>

1. <span data-ttu-id="2c901-196">[Stáhněte si](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) a spusťte serverovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2c901-196">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="2c901-197">[Pokyny ke stažení](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="2c901-197">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="2c901-198">Ověřte, že server aplikace funguje.</span><span class="sxs-lookup"><span data-stu-id="2c901-198">Verify the server app is working.</span></span> <span data-ttu-id="2c901-199">Například `http://localhost:64195/api/products` by měla vrátit seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="2c901-199">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="2c901-200">Nastaví základní identifikátor URI pro požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c901-200">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="2c901-201">Změňte číslo portu na port v serveru aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2c901-201">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="2c901-202">Spuštění klientské aplikace.</span><span class="sxs-lookup"><span data-stu-id="2c901-202">Run the client app.</span></span> <span data-ttu-id="2c901-203">Následující výstup je vytvořen:</span><span class="sxs-lookup"><span data-stu-id="2c901-203">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
