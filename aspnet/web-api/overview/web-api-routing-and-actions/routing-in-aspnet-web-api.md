---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Směrování ve webovém rozhraní API ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557608"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="56222-102">Směrování v rozhraní ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="56222-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="56222-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="56222-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="56222-104">Tento článek popisuje, jak webové rozhraní API ASP.NET směruje požadavky HTTP na řadiče.</span><span class="sxs-lookup"><span data-stu-id="56222-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="56222-105">Pokud jste obeznámeni s ASP.NET MVC, směrování webového rozhraní API se velmi podobá směrování MVC.</span><span class="sxs-lookup"><span data-stu-id="56222-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="56222-106">Hlavní rozdíl spočívá v tom, že webové rozhraní API používá příkaz HTTP, nikoli cestu identifikátoru URI, k výběru akce.</span><span class="sxs-lookup"><span data-stu-id="56222-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="56222-107">Ve webovém rozhraní API můžete také použít směrování ve stylu MVC.</span><span class="sxs-lookup"><span data-stu-id="56222-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="56222-108">Tento článek nepředpokládá žádné znalosti ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="56222-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="56222-109">Směrovací tabulky</span><span class="sxs-lookup"><span data-stu-id="56222-109">Routing Tables</span></span>

<span data-ttu-id="56222-110">Ve webovém rozhraní API ASP.NET je *kontroler* třída, která zpracovává požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="56222-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="56222-111">Veřejné metody kontroleru se nazývají *metody akcí* nebo pouhými *akcemi*.</span><span class="sxs-lookup"><span data-stu-id="56222-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="56222-112">Když rozhraní Web API Framework obdrží požadavek, směruje požadavek na akci.</span><span class="sxs-lookup"><span data-stu-id="56222-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="56222-113">K určení, která akce se má vyvolat, používá rozhraní *směrovací tabulku*.</span><span class="sxs-lookup"><span data-stu-id="56222-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="56222-114">Šablona projektu sady Visual Studio pro webové rozhraní API vytvoří výchozí trasu:</span><span class="sxs-lookup"><span data-stu-id="56222-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="56222-115">Tato trasa je definována v souboru *WebApiConfig.cs* , který je umístěn v *aplikaci\_spouštěcí* adresář:</span><span class="sxs-lookup"><span data-stu-id="56222-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="56222-116">Další informace o třídě `WebApiConfig` najdete v tématu [Konfigurace webového rozhraní API ASP.NET](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="56222-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="56222-117">Pokud webové rozhraní API sami hostte, musíte nastavit směrovací tabulku přímo na objekt `HttpSelfHostConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="56222-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="56222-118">Další informace najdete v tématu věnovaném [samoobslužnému hostování webového rozhraní API](../older-versions/self-host-a-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="56222-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="56222-119">Každá položka v tabulce směrování obsahuje *šablonu směrování*.</span><span class="sxs-lookup"><span data-stu-id="56222-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="56222-120">Výchozí šablona trasy pro webové rozhraní API je &quot;API/{Controller}/{ID}&quot;.</span><span class="sxs-lookup"><span data-stu-id="56222-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="56222-121">V této šabloně &quot;rozhraní API&quot; je segment cesty literálu a {Controller} a {ID} jsou zástupné proměnné.</span><span class="sxs-lookup"><span data-stu-id="56222-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="56222-122">Když rozhraní Web API přijme požadavek HTTP, pokusí se porovnat identifikátor URI s jednou ze šablon směrování ve směrovací tabulce.</span><span class="sxs-lookup"><span data-stu-id="56222-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="56222-123">Pokud neodpovídá žádná trasa, klient obdrží chybu 404.</span><span class="sxs-lookup"><span data-stu-id="56222-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="56222-124">Například následující identifikátory URI odpovídají výchozí trase:</span><span class="sxs-lookup"><span data-stu-id="56222-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="56222-125">/api/contacts</span><span class="sxs-lookup"><span data-stu-id="56222-125">/api/contacts</span></span>
- <span data-ttu-id="56222-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="56222-126">/api/contacts/1</span></span>
- <span data-ttu-id="56222-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="56222-127">/api/products/gizmo1</span></span>

<span data-ttu-id="56222-128">Následující identifikátor URI se však neshoduje, protože nemá&quot; segment &quot;rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="56222-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="56222-129">/contacts/1</span><span class="sxs-lookup"><span data-stu-id="56222-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="56222-130">Důvodem použití rozhraní API v trase je zamezení kolizí s směrováním ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="56222-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="56222-131">Tímto způsobem můžete mít &quot;/Contacts&quot; přejít na kontroler MVC a &quot;/API/Contacts&quot; přejít na kontroler webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="56222-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="56222-132">Samozřejmě, pokud se vám tato konvence nelíbí, můžete změnit výchozí směrovací tabulku.</span><span class="sxs-lookup"><span data-stu-id="56222-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="56222-133">Po nalezení vyhovující trasy webové rozhraní API vybere kontroler a akci:</span><span class="sxs-lookup"><span data-stu-id="56222-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="56222-134">Pokud chcete najít kontroler, webové rozhraní API přidá&quot; kontroleru &quot;k hodnotě proměnné *{Controller}* .</span><span class="sxs-lookup"><span data-stu-id="56222-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="56222-135">Pokud chcete najít akci, webové rozhraní API prohlíží příkaz HTTP a pak vyhledá akci, jejíž název začíná tímto názvem příkazu HTTP.</span><span class="sxs-lookup"><span data-stu-id="56222-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="56222-136">Například s požadavkem GET webové rozhraní API vyhledá akci s předponou &quot;získat&quot;, například &quot;GetContact&quot; nebo &quot;GetAllContacts&quot;.</span><span class="sxs-lookup"><span data-stu-id="56222-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="56222-137">Tato konvence se vztahuje pouze na příkazy GET, POST, PUT, DELETE, HEAD, OPTIONS a PATCH.</span><span class="sxs-lookup"><span data-stu-id="56222-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="56222-138">Můžete povolit jiné příkazy HTTP pomocí atributů na řadiči.</span><span class="sxs-lookup"><span data-stu-id="56222-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="56222-139">Později se zobrazí příklad.</span><span class="sxs-lookup"><span data-stu-id="56222-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="56222-140">Jiné zástupné proměnné v šabloně směrování, jako je například *{ID},* jsou namapovány na parametry akce.</span><span class="sxs-lookup"><span data-stu-id="56222-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="56222-141">Pojďme se podívat na příklad.</span><span class="sxs-lookup"><span data-stu-id="56222-141">Let's look at an example.</span></span> <span data-ttu-id="56222-142">Předpokládejme, že definujete následující kontroler:</span><span class="sxs-lookup"><span data-stu-id="56222-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="56222-143">Tady jsou některé možné požadavky HTTP spolu s akcí, která se vyvolá pro každou z těchto možností:</span><span class="sxs-lookup"><span data-stu-id="56222-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="56222-144">Příkaz HTTP</span><span class="sxs-lookup"><span data-stu-id="56222-144">HTTP Verb</span></span> | <span data-ttu-id="56222-145">Cesta URI</span><span class="sxs-lookup"><span data-stu-id="56222-145">URI Path</span></span> | <span data-ttu-id="56222-146">Akce</span><span class="sxs-lookup"><span data-stu-id="56222-146">Action</span></span> | <span data-ttu-id="56222-147">Parametr</span><span class="sxs-lookup"><span data-stu-id="56222-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="56222-148">GET</span><span class="sxs-lookup"><span data-stu-id="56222-148">GET</span></span> | <span data-ttu-id="56222-149">rozhraní API/produkty</span><span class="sxs-lookup"><span data-stu-id="56222-149">api/products</span></span> | <span data-ttu-id="56222-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="56222-150">GetAllProducts</span></span> | <span data-ttu-id="56222-151">*nTato*</span><span class="sxs-lookup"><span data-stu-id="56222-151">*(none)*</span></span> |
| <span data-ttu-id="56222-152">GET</span><span class="sxs-lookup"><span data-stu-id="56222-152">GET</span></span> | <span data-ttu-id="56222-153">API/Products/4</span><span class="sxs-lookup"><span data-stu-id="56222-153">api/products/4</span></span> | <span data-ttu-id="56222-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="56222-154">GetProductById</span></span> | <span data-ttu-id="56222-155">4</span><span class="sxs-lookup"><span data-stu-id="56222-155">4</span></span> |
| <span data-ttu-id="56222-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="56222-156">DELETE</span></span> | <span data-ttu-id="56222-157">API/Products/4</span><span class="sxs-lookup"><span data-stu-id="56222-157">api/products/4</span></span> | <span data-ttu-id="56222-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="56222-158">DeleteProduct</span></span> | <span data-ttu-id="56222-159">4</span><span class="sxs-lookup"><span data-stu-id="56222-159">4</span></span> |
| <span data-ttu-id="56222-160">POST</span><span class="sxs-lookup"><span data-stu-id="56222-160">POST</span></span> | <span data-ttu-id="56222-161">rozhraní API/produkty</span><span class="sxs-lookup"><span data-stu-id="56222-161">api/products</span></span> | <span data-ttu-id="56222-162">*(žádná shoda)*</span><span class="sxs-lookup"><span data-stu-id="56222-162">*(no match)*</span></span> |  |

<span data-ttu-id="56222-163">Všimněte si, že segment *{ID}* identifikátoru URI, pokud je k dispozici, je namapován na parametr *ID* akce.</span><span class="sxs-lookup"><span data-stu-id="56222-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="56222-164">V tomto příkladu kontroler definuje dvě metody GET, jednu s parametrem *ID* a jednu bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="56222-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="56222-165">Také si všimněte, že požadavek POST selže, protože kontroler nedefinuje metodu &quot;post...&quot;.</span><span class="sxs-lookup"><span data-stu-id="56222-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="56222-166">Variace směrování</span><span class="sxs-lookup"><span data-stu-id="56222-166">Routing Variations</span></span>

<span data-ttu-id="56222-167">Předchozí část popisuje základní mechanismus směrování pro webové rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="56222-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="56222-168">Tato část popisuje některé variace.</span><span class="sxs-lookup"><span data-stu-id="56222-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="56222-169">Příkazy protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="56222-169">HTTP verbs</span></span>

<span data-ttu-id="56222-170">Namísto použití zásad vytváření názvů pro příkazy HTTP můžete explicitně zadat příkaz HTTP pro akci tím, že upravení metodu Action s jedním z následujících atributů:</span><span class="sxs-lookup"><span data-stu-id="56222-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="56222-171">V následujícím příkladu je metoda `FindProduct` namapována na požadavky GET:</span><span class="sxs-lookup"><span data-stu-id="56222-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="56222-172">Pro povolení více příkazů HTTP pro akci nebo pro jiné operace HTTP než GET, PUT, POST, DELETE, HEAD, OPTIONS a PATCH použijte atribut `[AcceptVerbs]`, který přebírá seznam příkazů HTTP.</span><span class="sxs-lookup"><span data-stu-id="56222-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="56222-173">Směrování podle názvu akce</span><span class="sxs-lookup"><span data-stu-id="56222-173">Routing by Action Name</span></span>

<span data-ttu-id="56222-174">S výchozí šablonou směrování používá webové rozhraní API k výběru akce příkaz HTTP.</span><span class="sxs-lookup"><span data-stu-id="56222-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="56222-175">Můžete ale také vytvořit trasu, kde je název akce zahrnutý v identifikátoru URI:</span><span class="sxs-lookup"><span data-stu-id="56222-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="56222-176">V této šabloně trasy parametr *{Action}* pojmenuje metodu Action na kontroleru.</span><span class="sxs-lookup"><span data-stu-id="56222-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="56222-177">Pomocí tohoto stylu směrování určete povolené příkazy HTTP pomocí atributů.</span><span class="sxs-lookup"><span data-stu-id="56222-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="56222-178">Předpokládejme například, že řadič má následující metodu:</span><span class="sxs-lookup"><span data-stu-id="56222-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="56222-179">V takovém případě se požadavek GET pro "API/Products/Details/1" namapuje na metodu `Details`.</span><span class="sxs-lookup"><span data-stu-id="56222-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="56222-180">Tento styl směrování se podobá ASP.NET MVC a může být vhodný pro rozhraní API ve stylu RPC.</span><span class="sxs-lookup"><span data-stu-id="56222-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="56222-181">Název akce můžete přepsat pomocí atributu `[ActionName]`.</span><span class="sxs-lookup"><span data-stu-id="56222-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="56222-182">V následujícím příkladu jsou k dispozici dvě akce, které se mapují na &quot;rozhraní API/Products/Miniatura/*ID*. Jedna podporuje GET a druhá podporuje POST:</span><span class="sxs-lookup"><span data-stu-id="56222-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="56222-183">Bez akcí</span><span class="sxs-lookup"><span data-stu-id="56222-183">Non-Actions</span></span>

<span data-ttu-id="56222-184">Chcete-li zabránit metodě v tom, aby se vyvolala jako akce, použijte atribut `[NonAction]`.</span><span class="sxs-lookup"><span data-stu-id="56222-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="56222-185">Tato signály signalizují rozhraní, že metoda není akcí, i když by jinak odpovídala pravidlům směrování.</span><span class="sxs-lookup"><span data-stu-id="56222-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="56222-186">Další čtení</span><span class="sxs-lookup"><span data-stu-id="56222-186">Further Reading</span></span>

<span data-ttu-id="56222-187">Toto téma nabízí podrobný pohled na směrování.</span><span class="sxs-lookup"><span data-stu-id="56222-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="56222-188">Další podrobnosti najdete v tématu [Směrování a výběr akcí](routing-and-action-selection.md), který přesně popisuje, jak architektura odpovídá identifikátoru URI ke směrování, vybere kontroler a pak vybere akci, která se má vyvolat.</span><span class="sxs-lookup"><span data-stu-id="56222-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
