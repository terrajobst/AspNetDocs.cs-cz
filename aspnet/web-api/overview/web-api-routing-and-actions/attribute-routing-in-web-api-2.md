---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Směrování atributů ve webovém rozhraní API 2 pro ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554983"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="a2aea-102">Směrování atributů ve webovém rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a2aea-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="a2aea-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a2aea-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a2aea-104">*Směrování* je způsob, jakým webové rozhraní API odpovídá na akci pomocí identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="a2aea-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="a2aea-105">Webové rozhraní API 2 podporuje nový typ směrování, kterému se říká *Směrování atributů*.</span><span class="sxs-lookup"><span data-stu-id="a2aea-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="a2aea-106">Jak název naznačuje, směrování atributů používá atributy k definování tras.</span><span class="sxs-lookup"><span data-stu-id="a2aea-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="a2aea-107">Směrování atributů nabízí větší kontrolu nad identifikátory URI ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a2aea-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="a2aea-108">Můžete například snadno vytvořit identifikátory URI, které popisují hierarchie prostředků.</span><span class="sxs-lookup"><span data-stu-id="a2aea-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="a2aea-109">Dřívější styl směrování s názvem směrování na základě konvence je stále plně podporovaný.</span><span class="sxs-lookup"><span data-stu-id="a2aea-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="a2aea-110">Ve skutečnosti můžete obě techniky kombinovat do stejného projektu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="a2aea-111">V tomto tématu se dozvíte, jak povolit směrování atributů a popisuje různé možnosti pro směrování atributů.</span><span class="sxs-lookup"><span data-stu-id="a2aea-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="a2aea-112">Ucelený kurz, který používá směrování atributů, najdete v tématu [vytvoření REST API s směrováním atributů ve webovém rozhraní API 2](create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="a2aea-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2aea-113">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="a2aea-113">Prerequisites</span></span>

<span data-ttu-id="a2aea-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Komunita, edice Professional nebo Enterprise</span><span class="sxs-lookup"><span data-stu-id="a2aea-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="a2aea-115">Případně můžete pomocí Správce balíčků NuGet nainstalovat potřebné balíčky.</span><span class="sxs-lookup"><span data-stu-id="a2aea-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="a2aea-116">V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="a2aea-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="a2aea-117">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="a2aea-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="a2aea-118">Proč směrování atributů?</span><span class="sxs-lookup"><span data-stu-id="a2aea-118">Why Attribute Routing?</span></span>

<span data-ttu-id="a2aea-119">První vydání webového rozhraní API používalo směrování *založené na konvencích* .</span><span class="sxs-lookup"><span data-stu-id="a2aea-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="a2aea-120">V tomto typu směrování definujete jednu nebo více šablon směrování, které jsou v podstatě parametrizované řetězce.</span><span class="sxs-lookup"><span data-stu-id="a2aea-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="a2aea-121">Když rozhraní obdrží požadavek, odpovídá identifikátoru URI proti šabloně trasy.</span><span class="sxs-lookup"><span data-stu-id="a2aea-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="a2aea-122">(Další informace o směrování založeném na konvencích najdete v tématu [směrování ve webovém rozhraní API ASP.NET](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="a2aea-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="a2aea-123">Jednou z výhod směrování založeného na konvenci je, že šablony jsou definovány na jednom místě a pravidla směrování se používají konzistentně napříč všemi řadiči.</span><span class="sxs-lookup"><span data-stu-id="a2aea-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="a2aea-124">Směrování založené na konvenci bohužel obtížně podporuje určité vzory identifikátorů URI, které jsou běžné v rozhraních RESTful API.</span><span class="sxs-lookup"><span data-stu-id="a2aea-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="a2aea-125">Například prostředky často obsahují podřízené prostředky: zákazníci mají objednávky, filmy mají aktéry, v knihách jsou autoři a tak dále.</span><span class="sxs-lookup"><span data-stu-id="a2aea-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="a2aea-126">Je přirozené vytvořit identifikátory URI, které odráží tyto relace:</span><span class="sxs-lookup"><span data-stu-id="a2aea-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="a2aea-127">Tento typ identifikátoru URI je obtížné vytvořit pomocí směrování založeného na konvencích.</span><span class="sxs-lookup"><span data-stu-id="a2aea-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="a2aea-128">I když je to možné, výsledky se nemůžou škálovat dobře, pokud máte mnoho řadičů nebo typů prostředků.</span><span class="sxs-lookup"><span data-stu-id="a2aea-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="a2aea-129">Při směrování atributů je jednoduché definovat trasu pro tento identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="a2aea-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="a2aea-130">Jednoduše přidáte atribut do akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="a2aea-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="a2aea-131">Tady je několik dalších vzorů, které směrování atributů usnadňuje.</span><span class="sxs-lookup"><span data-stu-id="a2aea-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="a2aea-132">**Správa verzí rozhraní API**</span><span class="sxs-lookup"><span data-stu-id="a2aea-132">**API versioning**</span></span>

<span data-ttu-id="a2aea-133">V tomto příkladu se "/API/v1/Products" směruje na jiný kontroler než "/API/v2/Products".</span><span class="sxs-lookup"><span data-stu-id="a2aea-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="a2aea-134">**Přetížené segmenty identifikátorů URI**</span><span class="sxs-lookup"><span data-stu-id="a2aea-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="a2aea-135">V tomto příkladu je "1" číslo objednávky, ale "čeká" se mapuje na kolekci.</span><span class="sxs-lookup"><span data-stu-id="a2aea-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="a2aea-136">**Více typů parametrů**</span><span class="sxs-lookup"><span data-stu-id="a2aea-136">**Multiple parameter types**</span></span>

<span data-ttu-id="a2aea-137">V tomto příkladu je "1" číslo objednávky, ale "2013/06/16" Určuje datum.</span><span class="sxs-lookup"><span data-stu-id="a2aea-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="a2aea-138">Povolení směrování atributů</span><span class="sxs-lookup"><span data-stu-id="a2aea-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="a2aea-139">Chcete-li povolit směrování atributů, zavolejte **MapHttpAttributeRoutes** během konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a2aea-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="a2aea-140">Tato metoda rozšíření je definována v třídě **System. Web. http. HttpConfigurationExtensions** .</span><span class="sxs-lookup"><span data-stu-id="a2aea-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="a2aea-141">Směrování atributů se dá kombinovat s směrováním [založeným na konvencích](routing-in-aspnet-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="a2aea-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="a2aea-142">Chcete-li definovat trasy založené na konvencích, zavolejte metodu **MapHttpRoute** .</span><span class="sxs-lookup"><span data-stu-id="a2aea-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="a2aea-143">Další informace o konfiguraci webového rozhraní API najdete v tématu [Konfigurace webového rozhraní API 2 pro ASP.NET](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="a2aea-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="a2aea-144">Poznámka: migrace z webového rozhraní API 1</span><span class="sxs-lookup"><span data-stu-id="a2aea-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="a2aea-145">Před webovým rozhraním API 2 šablony projektu webového rozhraní API vygenerovaly kód takto:</span><span class="sxs-lookup"><span data-stu-id="a2aea-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="a2aea-146">Pokud je povoleno směrování atributů, bude tento kód generovat výjimku.</span><span class="sxs-lookup"><span data-stu-id="a2aea-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="a2aea-147">Pokud upgradujete existující projekt webového rozhraní API tak, aby používal směrování atributů, nezapomeňte aktualizovat konfigurační kód následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a2aea-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="a2aea-148">Další informace najdete v tématu [Konfigurace webového rozhraní API s hostováním ASP.NET](../advanced/configuring-aspnet-web-api.md#webhost).</span><span class="sxs-lookup"><span data-stu-id="a2aea-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="a2aea-149">Přidání atributů trasy</span><span class="sxs-lookup"><span data-stu-id="a2aea-149">Adding Route Attributes</span></span>

<span data-ttu-id="a2aea-150">Tady je příklad trasy definované pomocí atributu:</span><span class="sxs-lookup"><span data-stu-id="a2aea-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="a2aea-151">Řetězec &quot;Customers/{customerId}/Orders&quot; je šablona identifikátoru URI pro trasu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="a2aea-152">Webové rozhraní API se pokusí spárovat identifikátor URI žádosti se šablonou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="a2aea-153">V tomto příkladu jsou "Customers" a "Orders" segmenty literálů a "{customerId}" je parametr proměnné.</span><span class="sxs-lookup"><span data-stu-id="a2aea-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="a2aea-154">Následující identifikátory URI by odpovídaly této šabloně:</span><span class="sxs-lookup"><span data-stu-id="a2aea-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="a2aea-155">Můžete omezit porovnání pomocí [omezení](#constraints), která jsou popsána dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="a2aea-156">Všimněte si, že parametr &quot;{customerId}&quot; v šabloně trasy odpovídá názvu parametru *customerId* v metodě.</span><span class="sxs-lookup"><span data-stu-id="a2aea-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="a2aea-157">Když webové rozhraní API vyvolá akci kontroleru, pokusí se vytvořit vazby parametrů trasy.</span><span class="sxs-lookup"><span data-stu-id="a2aea-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="a2aea-158">Například pokud je identifikátor URI `http://example.com/customers/1/orders`, webové rozhraní API se pokusí o navázání hodnoty "1" na parametr *customerId* v akci.</span><span class="sxs-lookup"><span data-stu-id="a2aea-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="a2aea-159">Šablona identifikátoru URI může mít několik parametrů:</span><span class="sxs-lookup"><span data-stu-id="a2aea-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="a2aea-160">Všechny metody kontroleru, které nemají atribut směrování, používají směrování na základě konvence.</span><span class="sxs-lookup"><span data-stu-id="a2aea-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="a2aea-161">Tímto způsobem můžete zkombinovat oba typy směrování do stejného projektu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a2aea-162">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="a2aea-162">HTTP Methods</span></span>

<span data-ttu-id="a2aea-163">Webové rozhraní API také vybere akce založené na metodě HTTP žádosti (GET, POST atd.).</span><span class="sxs-lookup"><span data-stu-id="a2aea-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="a2aea-164">Ve výchozím nastavení hledá webové rozhraní API porovnávání bez rozlišení velkých a malých písmen na začátku názvu metody kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a2aea-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="a2aea-165">Například metoda kontroleru s názvem `PutCustomers` odpovídá požadavku HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="a2aea-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="a2aea-166">Tuto konvenci můžete přepsat tak, že upravení metodu s následujícími atributy:</span><span class="sxs-lookup"><span data-stu-id="a2aea-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="a2aea-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="a2aea-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="a2aea-168">**HttpGet**</span><span class="sxs-lookup"><span data-stu-id="a2aea-168">**[HttpGet]**</span></span>
- <span data-ttu-id="a2aea-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="a2aea-169">**[HttpHead]**</span></span>
- <span data-ttu-id="a2aea-170">**[HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="a2aea-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="a2aea-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="a2aea-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="a2aea-172">**HTTPPOST**</span><span class="sxs-lookup"><span data-stu-id="a2aea-172">**[HttpPost]**</span></span>
- <span data-ttu-id="a2aea-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="a2aea-173">**[HttpPut]**</span></span>

<span data-ttu-id="a2aea-174">Následující příklad mapuje metodu CreateBook na požadavky HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a2aea-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="a2aea-175">Pro všechny ostatní metody HTTP, včetně nestandardních metod, použijte atribut **AcceptVerbs** , který převezme seznam metod http.</span><span class="sxs-lookup"><span data-stu-id="a2aea-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="a2aea-176">Předpony tras</span><span class="sxs-lookup"><span data-stu-id="a2aea-176">Route Prefixes</span></span>

<span data-ttu-id="a2aea-177">Trasy v řadiči jsou často spouštěny se stejnou předponou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="a2aea-178">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a2aea-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="a2aea-179">Společnou předponu pro celý kontroler můžete nastavit pomocí atributu **[RoutePrefix]** :</span><span class="sxs-lookup"><span data-stu-id="a2aea-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="a2aea-180">K přepsání předpony trasy použijte vlnovku (~) na atributu method:</span><span class="sxs-lookup"><span data-stu-id="a2aea-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="a2aea-181">Předpona trasy může zahrnovat parametry:</span><span class="sxs-lookup"><span data-stu-id="a2aea-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="a2aea-182">Omezení trasy</span><span class="sxs-lookup"><span data-stu-id="a2aea-182">Route Constraints</span></span>

<span data-ttu-id="a2aea-183">Omezení tras vám umožňují omezit způsob párování parametrů v šabloně směrování.</span><span class="sxs-lookup"><span data-stu-id="a2aea-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="a2aea-184">Obecná syntaxe je &quot;{Parameter: Constraint}&quot;.</span><span class="sxs-lookup"><span data-stu-id="a2aea-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="a2aea-185">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a2aea-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="a2aea-186">V tomto případě se první trasa vybere jenom v případě, že ID &quot;&quot; segmentu identifikátoru URI je celé číslo.</span><span class="sxs-lookup"><span data-stu-id="a2aea-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="a2aea-187">V opačném případě bude zvolena Druhá trasa.</span><span class="sxs-lookup"><span data-stu-id="a2aea-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="a2aea-188">V následující tabulce jsou uvedena omezení, která jsou podporována.</span><span class="sxs-lookup"><span data-stu-id="a2aea-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="a2aea-189">Jedinečn</span><span class="sxs-lookup"><span data-stu-id="a2aea-189">Constraint</span></span> | <span data-ttu-id="a2aea-190">Popis</span><span class="sxs-lookup"><span data-stu-id="a2aea-190">Description</span></span> | <span data-ttu-id="a2aea-191">Příklad</span><span class="sxs-lookup"><span data-stu-id="a2aea-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a2aea-192">Rozšířená</span><span class="sxs-lookup"><span data-stu-id="a2aea-192">alpha</span></span> | <span data-ttu-id="a2aea-193">Odpovídá znakům na velká a malá písmena latinky (a – z, A – Z).</span><span class="sxs-lookup"><span data-stu-id="a2aea-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="a2aea-194">{x:alpha}</span><span class="sxs-lookup"><span data-stu-id="a2aea-194">{x:alpha}</span></span> |
| <span data-ttu-id="a2aea-195">bool</span><span class="sxs-lookup"><span data-stu-id="a2aea-195">bool</span></span> | <span data-ttu-id="a2aea-196">Odpovídá logické hodnotě.</span><span class="sxs-lookup"><span data-stu-id="a2aea-196">Matches a Boolean value.</span></span> | <span data-ttu-id="a2aea-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="a2aea-197">{x:bool}</span></span> |
| <span data-ttu-id="a2aea-198">datetime</span><span class="sxs-lookup"><span data-stu-id="a2aea-198">datetime</span></span> | <span data-ttu-id="a2aea-199">Odpovídá hodnotě **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="a2aea-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="a2aea-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="a2aea-200">{x:datetime}</span></span> |
| <span data-ttu-id="a2aea-201">decimal</span><span class="sxs-lookup"><span data-stu-id="a2aea-201">decimal</span></span> | <span data-ttu-id="a2aea-202">Odpovídá desítkové hodnotě.</span><span class="sxs-lookup"><span data-stu-id="a2aea-202">Matches a decimal value.</span></span> | <span data-ttu-id="a2aea-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="a2aea-203">{x:decimal}</span></span> |
| <span data-ttu-id="a2aea-204">double</span><span class="sxs-lookup"><span data-stu-id="a2aea-204">double</span></span> | <span data-ttu-id="a2aea-205">Odpovídá hodnotě 64, což je hodnota s plovoucí desetinnou čárkou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="a2aea-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="a2aea-206">{x:double}</span></span> |
| <span data-ttu-id="a2aea-207">float</span><span class="sxs-lookup"><span data-stu-id="a2aea-207">float</span></span> | <span data-ttu-id="a2aea-208">Odpovídá hodnotě 32, což je hodnota s plovoucí desetinnou čárkou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="a2aea-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="a2aea-209">{x:float}</span></span> |
| <span data-ttu-id="a2aea-210">guid</span><span class="sxs-lookup"><span data-stu-id="a2aea-210">guid</span></span> | <span data-ttu-id="a2aea-211">Odpovídá hodnotě identifikátoru GUID.</span><span class="sxs-lookup"><span data-stu-id="a2aea-211">Matches a GUID value.</span></span> | <span data-ttu-id="a2aea-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="a2aea-212">{x:guid}</span></span> |
| <span data-ttu-id="a2aea-213">int</span><span class="sxs-lookup"><span data-stu-id="a2aea-213">int</span></span> | <span data-ttu-id="a2aea-214">Vyhledá shodu s celočíselnou hodnotou 32.</span><span class="sxs-lookup"><span data-stu-id="a2aea-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="a2aea-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="a2aea-215">{x:int}</span></span> |
| <span data-ttu-id="a2aea-216">length</span><span class="sxs-lookup"><span data-stu-id="a2aea-216">length</span></span> | <span data-ttu-id="a2aea-217">Odpovídá řetězci se zadanou délkou nebo v zadaném rozsahu délek.</span><span class="sxs-lookup"><span data-stu-id="a2aea-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="a2aea-218">{x:Length (6)} {x:Length (1; 20)}</span><span class="sxs-lookup"><span data-stu-id="a2aea-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="a2aea-219">long</span><span class="sxs-lookup"><span data-stu-id="a2aea-219">long</span></span> | <span data-ttu-id="a2aea-220">Vyhledá shodu s celočíselnou hodnotou 64.</span><span class="sxs-lookup"><span data-stu-id="a2aea-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="a2aea-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="a2aea-221">{x:long}</span></span> |
| <span data-ttu-id="a2aea-222">max</span><span class="sxs-lookup"><span data-stu-id="a2aea-222">max</span></span> | <span data-ttu-id="a2aea-223">Odpovídá celému číslu s maximální hodnotou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="a2aea-224">{x:max (10)}</span><span class="sxs-lookup"><span data-stu-id="a2aea-224">{x:max(10)}</span></span> |
| <span data-ttu-id="a2aea-225">MaxLength</span><span class="sxs-lookup"><span data-stu-id="a2aea-225">maxlength</span></span> | <span data-ttu-id="a2aea-226">Odpovídá řetězci s maximální délkou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="a2aea-227">{x:MaxLength (10)}</span><span class="sxs-lookup"><span data-stu-id="a2aea-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="a2aea-228">min</span><span class="sxs-lookup"><span data-stu-id="a2aea-228">min</span></span> | <span data-ttu-id="a2aea-229">Odpovídá celému číslu s minimální hodnotou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="a2aea-230">{x:min (10)}</span><span class="sxs-lookup"><span data-stu-id="a2aea-230">{x:min(10)}</span></span> |
| <span data-ttu-id="a2aea-231">minLength</span><span class="sxs-lookup"><span data-stu-id="a2aea-231">minlength</span></span> | <span data-ttu-id="a2aea-232">Odpovídá řetězci s minimální délkou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="a2aea-233">{x:minLength (10)}</span><span class="sxs-lookup"><span data-stu-id="a2aea-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="a2aea-234">range</span><span class="sxs-lookup"><span data-stu-id="a2aea-234">range</span></span> | <span data-ttu-id="a2aea-235">Odpovídá celému číslu v rámci rozsahu hodnot.</span><span class="sxs-lookup"><span data-stu-id="a2aea-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="a2aea-236">{x:Range (10, 50)}</span><span class="sxs-lookup"><span data-stu-id="a2aea-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="a2aea-237">regulární</span><span class="sxs-lookup"><span data-stu-id="a2aea-237">regex</span></span> | <span data-ttu-id="a2aea-238">Odpovídá regulárnímu výrazu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-238">Matches a regular expression.</span></span> | <span data-ttu-id="a2aea-239">{x:Regex (^ \d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="a2aea-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="a2aea-240">Všimněte si, že některá omezení, například &quot;minimální&quot;, přijímají argumenty v závorkách.</span><span class="sxs-lookup"><span data-stu-id="a2aea-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="a2aea-241">U parametru můžete použít více omezení oddělených dvojtečkou.</span><span class="sxs-lookup"><span data-stu-id="a2aea-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="a2aea-242">Vlastní omezení trasy</span><span class="sxs-lookup"><span data-stu-id="a2aea-242">Custom Route Constraints</span></span>

<span data-ttu-id="a2aea-243">Můžete vytvořit vlastní omezení trasy implementací rozhraní **IHttpRouteConstraint** .</span><span class="sxs-lookup"><span data-stu-id="a2aea-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="a2aea-244">Například následující omezení omezuje parametr na celočíselnou hodnotu, která není nulová.</span><span class="sxs-lookup"><span data-stu-id="a2aea-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="a2aea-245">Následující kód ukazuje, jak toto omezení zaregistrovat:</span><span class="sxs-lookup"><span data-stu-id="a2aea-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="a2aea-246">Nyní můžete omezení použít ve svých trasách:</span><span class="sxs-lookup"><span data-stu-id="a2aea-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="a2aea-247">Můžete také nahradit celou třídu **DefaultInlineConstraintResolver** implementací rozhraní **IInlineConstraintResolver** .</span><span class="sxs-lookup"><span data-stu-id="a2aea-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="a2aea-248">Tím se nahradí všechna předdefinovaná omezení, pokud vaše implementace **IInlineConstraintResolver** konkrétně nepřidá.</span><span class="sxs-lookup"><span data-stu-id="a2aea-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="a2aea-249">Volitelné parametry identifikátoru URI a výchozí hodnoty</span><span class="sxs-lookup"><span data-stu-id="a2aea-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="a2aea-250">Parametr URI můžete nastavit jako volitelný přidáním otazníku do parametru Route.</span><span class="sxs-lookup"><span data-stu-id="a2aea-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="a2aea-251">Pokud je parametr trasy volitelný, je nutné definovat výchozí hodnotu parametru metody.</span><span class="sxs-lookup"><span data-stu-id="a2aea-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="a2aea-252">V tomto příkladu `/api/books/locale/1033` a `/api/books/locale` vrací stejný prostředek.</span><span class="sxs-lookup"><span data-stu-id="a2aea-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="a2aea-253">Případně můžete zadat výchozí hodnotu v rámci šablony trasy následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a2aea-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="a2aea-254">To je skoro stejné jako v předchozím příkladu, ale existuje mírné rozdíly v chování při použití výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a2aea-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="a2aea-255">V prvním příkladu ("{LCID: int?}") je výchozí hodnota 1033 přiřazena přímo k parametru metody, takže parametr bude mít tuto přesnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="a2aea-256">V druhém příkladu ("{LCID: int = 1033}") je výchozí hodnota "1033" prostřednictvím procesu vytváření vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="a2aea-257">Výchozí model-Binder převede "1033" na číselnou hodnotu 1033.</span><span class="sxs-lookup"><span data-stu-id="a2aea-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="a2aea-258">Mohli byste se ale připojit k vlastnímu pořadači modelů, který může dělat něco jiného.</span><span class="sxs-lookup"><span data-stu-id="a2aea-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="a2aea-259">(Ve většině případů platí, že pokud ve vašem kanálu nemáte vlastní pořadače modelů, budou tyto dva formuláře ekvivalentní.)</span><span class="sxs-lookup"><span data-stu-id="a2aea-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="a2aea-260">Názvy tras</span><span class="sxs-lookup"><span data-stu-id="a2aea-260">Route Names</span></span>

<span data-ttu-id="a2aea-261">Ve webovém rozhraní API má každá trasa název.</span><span class="sxs-lookup"><span data-stu-id="a2aea-261">In Web API, every route has a name.</span></span> <span data-ttu-id="a2aea-262">Názvy tras jsou užitečné pro generování odkazů, abyste mohli zahrnout odkaz do odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="a2aea-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="a2aea-263">Chcete-li zadat název trasy, nastavte vlastnost **název** u atributu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="a2aea-264">Následující příklad ukazuje, jak nastavit název trasy a také jak použít název trasy při generování propojení.</span><span class="sxs-lookup"><span data-stu-id="a2aea-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="a2aea-265">Pořadí směrování</span><span class="sxs-lookup"><span data-stu-id="a2aea-265">Route Order</span></span>

<span data-ttu-id="a2aea-266">Když se architektura pokusí vyhledat identifikátor URI s trasou, vyhodnotí trasy v určitém pořadí.</span><span class="sxs-lookup"><span data-stu-id="a2aea-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="a2aea-267">Chcete-li zadat pořadí, nastavte vlastnost **Order** v atributu Route.</span><span class="sxs-lookup"><span data-stu-id="a2aea-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="a2aea-268">Nižší hodnoty jsou vyhodnocovány jako první.</span><span class="sxs-lookup"><span data-stu-id="a2aea-268">Lower values are evaluated first.</span></span> <span data-ttu-id="a2aea-269">Výchozí hodnota pořadí je nula.</span><span class="sxs-lookup"><span data-stu-id="a2aea-269">The default order value is zero.</span></span>

<span data-ttu-id="a2aea-270">Tady je způsob, jakým je stanoveno celkové řazení:</span><span class="sxs-lookup"><span data-stu-id="a2aea-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="a2aea-271">Porovnejte vlastnost **Order** atributu Route.</span><span class="sxs-lookup"><span data-stu-id="a2aea-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="a2aea-272">Podívejte se na každý segment identifikátoru URI v šabloně trasy.</span><span class="sxs-lookup"><span data-stu-id="a2aea-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="a2aea-273">Pro každý segment seřazením následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a2aea-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="a2aea-274">Segmenty literálu.</span><span class="sxs-lookup"><span data-stu-id="a2aea-274">Literal segments.</span></span>
    2. <span data-ttu-id="a2aea-275">Parametry směrování s omezeními.</span><span class="sxs-lookup"><span data-stu-id="a2aea-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="a2aea-276">Parametry trasy bez omezení.</span><span class="sxs-lookup"><span data-stu-id="a2aea-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="a2aea-277">Segmenty parametrů se zástupnými znaky s omezeními.</span><span class="sxs-lookup"><span data-stu-id="a2aea-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="a2aea-278">Segmenty parametrů zástupného znaku bez omezení.</span><span class="sxs-lookup"><span data-stu-id="a2aea-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="a2aea-279">V případě propojení se trasy seřadí podle ordinálního porovnávání řetězců bez rozlišení velkých a malých písmen ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) šablony trasy.</span><span class="sxs-lookup"><span data-stu-id="a2aea-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="a2aea-280">Tady je příklad.</span><span class="sxs-lookup"><span data-stu-id="a2aea-280">Here is an example.</span></span> <span data-ttu-id="a2aea-281">Předpokládejme, že definujete následující kontroler:</span><span class="sxs-lookup"><span data-stu-id="a2aea-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="a2aea-282">Tyto trasy jsou seřazené následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="a2aea-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="a2aea-283">objednávky/podrobnosti</span><span class="sxs-lookup"><span data-stu-id="a2aea-283">orders/details</span></span>
2. <span data-ttu-id="a2aea-284">objednávky/{ID}</span><span class="sxs-lookup"><span data-stu-id="a2aea-284">orders/{id}</span></span>
3. <span data-ttu-id="a2aea-285">objednávky/{Customer}</span><span class="sxs-lookup"><span data-stu-id="a2aea-285">orders/{customerName}</span></span>
4. <span data-ttu-id="a2aea-286">objednávky/{\*datum}</span><span class="sxs-lookup"><span data-stu-id="a2aea-286">orders/{\*date}</span></span>
5. <span data-ttu-id="a2aea-287">objednávky/čeká na vyřízení</span><span class="sxs-lookup"><span data-stu-id="a2aea-287">orders/pending</span></span>

<span data-ttu-id="a2aea-288">Všimněte si, že "Details" je segment literálu a zobrazí se před "{ID}", ale "čeká" se zobrazí jako poslední, protože vlastnost **Order** je 1.</span><span class="sxs-lookup"><span data-stu-id="a2aea-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="a2aea-289">(Tento příklad předpokládá, že nejsou k dispozici žádní zákazníci s názvem "Details" nebo "pending".</span><span class="sxs-lookup"><span data-stu-id="a2aea-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="a2aea-290">Obecně se pokuste vyhnout dvojznačným trasám.</span><span class="sxs-lookup"><span data-stu-id="a2aea-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="a2aea-291">V tomto příkladu je lepší šablonou směrování pro `GetByCustomer` "Customers/{Customer}").</span><span class="sxs-lookup"><span data-stu-id="a2aea-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
