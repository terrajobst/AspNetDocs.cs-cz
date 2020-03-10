---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Volání webového rozhraní API z klienta .NET (C#) – ASP.NET 4. x
author: MikeWasson
description: V tomto kurzu se dozvíte, jak volat webové rozhraní API z aplikace .NET 4. x.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: ab3ba71839123e848dffaa59871f9dac8c1a88d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622617"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="6005a-103">Volání webového rozhraní API z klienta .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="6005a-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="6005a-104">[Jan Wasson](https://github.com/MikeWasson) a [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6005a-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="6005a-105">[Stažení dokončeného projektu](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="6005a-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="6005a-106">[Pokyny ke stažení](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="6005a-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="6005a-107">V tomto kurzu se dozvíte, jak volat webové rozhraní API z aplikace .NET pomocí [System .NET. http. HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="6005a-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="6005a-108">V tomto kurzu se napíše klientská aplikace, která využívá následující webové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="6005a-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="6005a-109">Akce</span><span class="sxs-lookup"><span data-stu-id="6005a-109">Action</span></span> | <span data-ttu-id="6005a-110">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="6005a-110">HTTP method</span></span> | <span data-ttu-id="6005a-111">Relativní identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="6005a-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6005a-112">Získat produkt podle ID</span><span class="sxs-lookup"><span data-stu-id="6005a-112">Get a product by ID</span></span> | <span data-ttu-id="6005a-113">GET</span><span class="sxs-lookup"><span data-stu-id="6005a-113">GET</span></span> | <span data-ttu-id="6005a-114">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="6005a-114">/api/products/*id*</span></span> |
| <span data-ttu-id="6005a-115">Vytvořit nový produkt</span><span class="sxs-lookup"><span data-stu-id="6005a-115">Create a new product</span></span> | <span data-ttu-id="6005a-116">POST</span><span class="sxs-lookup"><span data-stu-id="6005a-116">POST</span></span> | <span data-ttu-id="6005a-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="6005a-117">/api/products</span></span> |
| <span data-ttu-id="6005a-118">Aktualizace produktu</span><span class="sxs-lookup"><span data-stu-id="6005a-118">Update a product</span></span> | <span data-ttu-id="6005a-119">PUT</span><span class="sxs-lookup"><span data-stu-id="6005a-119">PUT</span></span> | <span data-ttu-id="6005a-120">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="6005a-120">/api/products/*id*</span></span> |
| <span data-ttu-id="6005a-121">Odstranění produktu</span><span class="sxs-lookup"><span data-stu-id="6005a-121">Delete a product</span></span> | <span data-ttu-id="6005a-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="6005a-122">DELETE</span></span> | <span data-ttu-id="6005a-123">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="6005a-123">/api/products/*id*</span></span> |

<span data-ttu-id="6005a-124">Informace o tom, jak implementovat toto rozhraní API s webovým rozhraním API ASP.NET, najdete v tématu [Vytvoření webového rozhraní API, které podporuje operace CRUD](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="6005a-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="6005a-125">Pro zjednodušení je klientská aplikace v tomto kurzu pro konzolovou aplikaci systému Windows.</span><span class="sxs-lookup"><span data-stu-id="6005a-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="6005a-126">**HttpClient** se také podporuje pro aplikace Windows Phone a Windows Store.</span><span class="sxs-lookup"><span data-stu-id="6005a-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="6005a-127">Další informace najdete v tématu [Zápis kódu klienta webového rozhraní API pro více platforem pomocí přenosných knihoven](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6005a-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="6005a-128">Vytvoření konzolové aplikace</span><span class="sxs-lookup"><span data-stu-id="6005a-128">Create the Console Application</span></span>

<span data-ttu-id="6005a-129">V aplikaci Visual Studio vytvořte novou konzolovou aplikaci pro Windows s názvem **HttpClientSample** a vložte ji do následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="6005a-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="6005a-130">Předchozí kód je kompletní klientská aplikace.</span><span class="sxs-lookup"><span data-stu-id="6005a-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="6005a-131">`RunAsync` běží a blokuje až do dokončení.</span><span class="sxs-lookup"><span data-stu-id="6005a-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="6005a-132">Většina metod **HttpClient** je asynchronní, protože provádí v/v sítě.</span><span class="sxs-lookup"><span data-stu-id="6005a-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="6005a-133">Všechny asynchronní úlohy jsou prováděny v rámci `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="6005a-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="6005a-134">Obvykle aplikace neblokuje hlavní vlákno, ale tato aplikace nepovoluje žádnou interakci.</span><span class="sxs-lookup"><span data-stu-id="6005a-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="6005a-135">Instalace klientských knihoven webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6005a-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="6005a-136">Pomocí Správce balíčků NuGet nainstalujte balíček klientské knihovny webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6005a-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="6005a-137">V nabídce **nástroje** vyberte **správce balíčků NuGet** > **konzolu Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="6005a-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="6005a-138">V konzole správce balíčků (PMC) zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="6005a-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="6005a-139">Předchozí příkaz přidá do projektu následující balíčky NuGet:</span><span class="sxs-lookup"><span data-stu-id="6005a-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="6005a-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="6005a-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="6005a-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="6005a-141">Newtonsoft.Json</span></span>

<span data-ttu-id="6005a-142">Netwonsoft. JSON (označované také jako Json.NET) je oblíbený vysoce výkonný rozhraní JSON pro rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="6005a-142">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="6005a-143">Přidat třídu modelu</span><span class="sxs-lookup"><span data-stu-id="6005a-143">Add a Model Class</span></span>

<span data-ttu-id="6005a-144">Projděte si třídu `Product`:</span><span class="sxs-lookup"><span data-stu-id="6005a-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="6005a-145">Tato třída se shoduje s datovým modelem používaným webovým rozhraním API.</span><span class="sxs-lookup"><span data-stu-id="6005a-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="6005a-146">Aplikace může použít **HttpClient** ke čtení instance `Product` z odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="6005a-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="6005a-147">Aplikace nemusí zapisovat žádný kód deserializace.</span><span class="sxs-lookup"><span data-stu-id="6005a-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="6005a-148">Vytvoření a inicializace HttpClient</span><span class="sxs-lookup"><span data-stu-id="6005a-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="6005a-149">Prověřte vlastnost Static **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="6005a-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="6005a-150">**HttpClient** má být vytvořena instance jednou a znovu použita po celou dobu životnosti aplikace.</span><span class="sxs-lookup"><span data-stu-id="6005a-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="6005a-151">Následující podmínky mohou způsobit chyby **SocketException** :</span><span class="sxs-lookup"><span data-stu-id="6005a-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="6005a-152">Vytváří se nová instance **HttpClient** na žádost.</span><span class="sxs-lookup"><span data-stu-id="6005a-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="6005a-153">Server v případě vysoké zátěže.</span><span class="sxs-lookup"><span data-stu-id="6005a-153">Server under heavy load.</span></span>

<span data-ttu-id="6005a-154">Vytvoření nové instance **HttpClient** na žádost může vyčerpat dostupné sokety.</span><span class="sxs-lookup"><span data-stu-id="6005a-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="6005a-155">Následující kód Inicializuje instanci **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="6005a-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="6005a-156">Předchozí kód:</span><span class="sxs-lookup"><span data-stu-id="6005a-156">The preceding code:</span></span>

* <span data-ttu-id="6005a-157">Nastaví základní identifikátor URI pro požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="6005a-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="6005a-158">Změňte číslo portu na port použitý v serverové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6005a-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="6005a-159">Aplikace nebude fungovat, pokud se nepoužije port pro serverovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6005a-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="6005a-160">Nastaví hlavičku Accept na "Application/JSON".</span><span class="sxs-lookup"><span data-stu-id="6005a-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="6005a-161">Nastavení této hlavičky oznamuje serveru, aby odesílal data ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="6005a-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="6005a-162">Odeslat požadavek GET k načtení prostředku</span><span class="sxs-lookup"><span data-stu-id="6005a-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="6005a-163">Následující kód odešle požadavek GET na produkt:</span><span class="sxs-lookup"><span data-stu-id="6005a-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="6005a-164">Metoda **GetAsync** ODEŠLE požadavek HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="6005a-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="6005a-165">Po dokončení metody vrátí **HttpResponseMessage** , který obsahuje odpověď HTTP.</span><span class="sxs-lookup"><span data-stu-id="6005a-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="6005a-166">Pokud je stavový kód v odpovědi kód úspěšnosti, tělo odpovědi obsahuje reprezentaci kódu Product.</span><span class="sxs-lookup"><span data-stu-id="6005a-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="6005a-167">Zavolejte **ReadAsAsync** k deserializaci datové části JSON do instance `Product`.</span><span class="sxs-lookup"><span data-stu-id="6005a-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="6005a-168">Metoda **ReadAsAsync** je asynchronní, protože tělo odpovědi může být libovolně velké.</span><span class="sxs-lookup"><span data-stu-id="6005a-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="6005a-169">**HttpClient** nevyvolá výjimku, pokud odpověď HTTP obsahuje kód chyby.</span><span class="sxs-lookup"><span data-stu-id="6005a-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="6005a-170">Místo toho má vlastnost **IsSuccessStatusCode** **hodnotu false** , pokud je stav kód chyby.</span><span class="sxs-lookup"><span data-stu-id="6005a-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="6005a-171">Pokud dáváte přednost považovat kódy chyb HTTP jako výjimky, zavolejte [HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) objektu Response.</span><span class="sxs-lookup"><span data-stu-id="6005a-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="6005a-172">`EnsureSuccessStatusCode` vyvolá výjimku, pokud stavový kód spadá mimo rozsah 200&ndash;299.</span><span class="sxs-lookup"><span data-stu-id="6005a-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="6005a-173">Všimněte si, že **HttpClient** může vyvolat výjimky z jiných důvodů &mdash; například, pokud vyprší časový limit požadavku.</span><span class="sxs-lookup"><span data-stu-id="6005a-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="6005a-174">Formátovací moduly typu Media k deserializaci</span><span class="sxs-lookup"><span data-stu-id="6005a-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="6005a-175">Pokud je **ReadAsAsync** volán bez parametrů, používá výchozí sadu *formátovacích modulů médií* pro čtení těla odpovědi.</span><span class="sxs-lookup"><span data-stu-id="6005a-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="6005a-176">Výchozí formátovací moduly podporují data zakódovaná JSON, XML a Form-URL.</span><span class="sxs-lookup"><span data-stu-id="6005a-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="6005a-177">Namísto použití výchozích formátovacích modulů můžete zadat seznam formátovacích modulů do metody **ReadAsAsync** .</span><span class="sxs-lookup"><span data-stu-id="6005a-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="6005a-178">Použití seznamu formátovacích modulů je užitečné, pokud máte vlastní formátovací modul typu média:</span><span class="sxs-lookup"><span data-stu-id="6005a-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="6005a-179">Další informace najdete v tématu [Formátování médií ve webovém rozhraní API 2 pro ASP.NET](../formats-and-model-binding/media-formatters.md) .</span><span class="sxs-lookup"><span data-stu-id="6005a-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="6005a-180">Odeslání požadavku POST k vytvoření prostředku</span><span class="sxs-lookup"><span data-stu-id="6005a-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="6005a-181">Následující kód odešle požadavek POST, který obsahuje instanci `Product` ve formátu JSON:</span><span class="sxs-lookup"><span data-stu-id="6005a-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="6005a-182">Metoda **PostAsJsonAsync** :</span><span class="sxs-lookup"><span data-stu-id="6005a-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="6005a-183">Serializace objektu do formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="6005a-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="6005a-184">Odešle datovou část JSON v žádosti POST.</span><span class="sxs-lookup"><span data-stu-id="6005a-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="6005a-185">Pokud je požadavek úspěšný:</span><span class="sxs-lookup"><span data-stu-id="6005a-185">If the request succeeds:</span></span>

* <span data-ttu-id="6005a-186">Měla by vrátit odpověď 201 (vytvořeno).</span><span class="sxs-lookup"><span data-stu-id="6005a-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="6005a-187">Odpověď by měla obsahovat adresu URL vytvořených prostředků v hlavičce umístění.</span><span class="sxs-lookup"><span data-stu-id="6005a-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="6005a-188">Odeslání žádosti o vložení za účelem aktualizace prostředku</span><span class="sxs-lookup"><span data-stu-id="6005a-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="6005a-189">Následující kód odešle požadavek PUT k aktualizaci produktu:</span><span class="sxs-lookup"><span data-stu-id="6005a-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="6005a-190">Metoda **PutAsJsonAsync** funguje jako **PostAsJsonAsync**s tím rozdílem, že ODEŠLE požadavek PUT namísto post.</span><span class="sxs-lookup"><span data-stu-id="6005a-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="6005a-191">Odeslání žádosti o odstranění k odstranění prostředku</span><span class="sxs-lookup"><span data-stu-id="6005a-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="6005a-192">Následující kód pošle žádost o odstranění produktu:</span><span class="sxs-lookup"><span data-stu-id="6005a-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="6005a-193">Podobně jako GET, žádost o odstranění neobsahuje tělo žádosti.</span><span class="sxs-lookup"><span data-stu-id="6005a-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="6005a-194">Pomocí DELETE není nutné zadávat formát JSON nebo XML.</span><span class="sxs-lookup"><span data-stu-id="6005a-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="6005a-195">Test ukázky</span><span class="sxs-lookup"><span data-stu-id="6005a-195">Test the sample</span></span>

<span data-ttu-id="6005a-196">Testování klientské aplikace:</span><span class="sxs-lookup"><span data-stu-id="6005a-196">To test the client app:</span></span>

1. <span data-ttu-id="6005a-197">[Stáhněte](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) a spusťte serverovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6005a-197">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="6005a-198">[Pokyny ke stažení](/aspnet/core/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="6005a-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="6005a-199">Ověřte, že aplikace serveru pracuje.</span><span class="sxs-lookup"><span data-stu-id="6005a-199">Verify the server app is working.</span></span> <span data-ttu-id="6005a-200">Například `http://localhost:64195/api/products` by měl vracet seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="6005a-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="6005a-201">Nastavte základní identifikátor URI pro požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="6005a-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="6005a-202">Změňte číslo portu na port použitý v serverové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6005a-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="6005a-203">Spusťte klientskou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6005a-203">Run the client app.</span></span> <span data-ttu-id="6005a-204">Vytvoří se následující výstup:</span><span class="sxs-lookup"><span data-stu-id="6005a-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
