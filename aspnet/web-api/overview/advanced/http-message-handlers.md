---
uid: web-api/overview/advanced/http-message-handlers
title: Obslužné rutiny zpráv HTTP v rozhraní ASP.NET Web API – ASP.NET 4.x
author: MikeWasson
description: Přehled obslužné rutiny zpráv HTTP v rozhraní ASP.NET Web API pro ASP.NET 4.x
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 308d2e3dd21917e7656f7ffe889dc965d9275d74
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392102"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="6d89d-103">Obslužné rutiny zpráv HTTP v rozhraní ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6d89d-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="6d89d-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6d89d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="6d89d-105">A *obslužná rutina zprávy* je třída, která přijme požadavek HTTP a vrátí odpověď HTTP.</span><span class="sxs-lookup"><span data-stu-id="6d89d-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="6d89d-106">Obslužné rutiny zpráv jsou odvozeny od abstraktní **objekt HttpMessageHandler** třídy.</span><span class="sxs-lookup"><span data-stu-id="6d89d-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="6d89d-107">Řada obslužné rutiny zpráv jsou obvykle zřetězen dohromady.</span><span class="sxs-lookup"><span data-stu-id="6d89d-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="6d89d-108">První obslužná rutina požadavku HTTP, provádí nějaké zpracování a poskytuje k další obslužná rutina požadavku.</span><span class="sxs-lookup"><span data-stu-id="6d89d-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="6d89d-109">V určitém okamžiku odpovědi se vytvoří a vrátí řetězem.</span><span class="sxs-lookup"><span data-stu-id="6d89d-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="6d89d-110">Tento model se nazývá *delegování* obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="6d89d-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="6d89d-111">Obslužné rutiny zpráv na straně serveru</span><span class="sxs-lookup"><span data-stu-id="6d89d-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="6d89d-112">Na straně serveru používá kanál rozhraní Web API některé vestavěné zprávy obslužné rutiny:</span><span class="sxs-lookup"><span data-stu-id="6d89d-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="6d89d-113">**HttpServer** získá požadavku od hostitele.</span><span class="sxs-lookup"><span data-stu-id="6d89d-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="6d89d-114">**HttpRoutingDispatcher** odešle požadavek na základě trasy.</span><span class="sxs-lookup"><span data-stu-id="6d89d-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="6d89d-115">**HttpControllerDispatcher** odešle požadavek do kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6d89d-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="6d89d-116">Vlastní obslužné rutiny můžete přidat do kanálu.</span><span class="sxs-lookup"><span data-stu-id="6d89d-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="6d89d-117">Obslužné rutiny zpráv jsou vhodné pro vyskytující aspekty, které pracují na úrovni protokolu HTTP zprávy (spíše než akce kontroleru).</span><span class="sxs-lookup"><span data-stu-id="6d89d-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="6d89d-118">Například může být obslužné rutiny zpráv:</span><span class="sxs-lookup"><span data-stu-id="6d89d-118">For example, a message handler might:</span></span>

- <span data-ttu-id="6d89d-119">Číst nebo upravovat hlavičky žádosti.</span><span class="sxs-lookup"><span data-stu-id="6d89d-119">Read or modify request headers.</span></span>
- <span data-ttu-id="6d89d-120">Přidání hlavičky odpovědi do odpovědi.</span><span class="sxs-lookup"><span data-stu-id="6d89d-120">Add a response header to responses.</span></span>
- <span data-ttu-id="6d89d-121">Ověření požadavků dřív, než dorazí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="6d89d-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="6d89d-122">Tento diagram znázorňuje dvě vlastní obslužné rutiny, které jsou vloženy do kanálu:</span><span class="sxs-lookup"><span data-stu-id="6d89d-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="6d89d-123">Na straně klienta používá HttpClient také obslužné rutiny zpráv.</span><span class="sxs-lookup"><span data-stu-id="6d89d-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="6d89d-124">Další informace najdete v tématu [obslužné rutiny zpráv HttpClient](httpclient-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="6d89d-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="6d89d-125">Obslužné rutiny vlastních zpráv</span><span class="sxs-lookup"><span data-stu-id="6d89d-125">Custom Message Handlers</span></span>

<span data-ttu-id="6d89d-126">Zápis obslužné rutiny vlastních zpráv, jsou odvozeny z **System.Net.Http.DelegatingHandler** a přepsat **SendAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="6d89d-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="6d89d-127">Tato metoda má následující podpis:</span><span class="sxs-lookup"><span data-stu-id="6d89d-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="6d89d-128">Tato metoda přebírá **HttpRequestMessage** jako vstup a asynchronně vrátí **objekt HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="6d89d-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="6d89d-129">Obvyklá implementace provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="6d89d-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="6d89d-130">Zpracování zprávy s požadavkem.</span><span class="sxs-lookup"><span data-stu-id="6d89d-130">Process the request message.</span></span>
2. <span data-ttu-id="6d89d-131">Volání `base.SendAsync` odešlete žádost na vnitřní obslužnou rutinu.</span><span class="sxs-lookup"><span data-stu-id="6d89d-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="6d89d-132">Vnitřní obslužná rutina vrátí zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="6d89d-132">The inner handler returns a response message.</span></span> <span data-ttu-id="6d89d-133">(Tento krok je asynchronní.)</span><span class="sxs-lookup"><span data-stu-id="6d89d-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="6d89d-134">Zpracování odpovědi a vrátí řízení volajícímu.</span><span class="sxs-lookup"><span data-stu-id="6d89d-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="6d89d-135">Zde je příklad jednoduchého dotazu:</span><span class="sxs-lookup"><span data-stu-id="6d89d-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="6d89d-136">Volání `base.SendAsync` je asynchronní.</span><span class="sxs-lookup"><span data-stu-id="6d89d-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="6d89d-137">Pokud obslužná rutina nemá žádnou práci po tomto volání, použijte **await** – klíčové slovo, jak je znázorněno.</span><span class="sxs-lookup"><span data-stu-id="6d89d-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>


<span data-ttu-id="6d89d-138">Delegující obslužné rutiny můžete také přeskočit vnitřní obslužná rutina a vytvořit odpověď přímo:</span><span class="sxs-lookup"><span data-stu-id="6d89d-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="6d89d-139">Pokud delegování obslužná rutina vytvoří odpověď bez volání `base.SendAsync`, přeskočí požadavku rest z kanálu.</span><span class="sxs-lookup"><span data-stu-id="6d89d-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="6d89d-140">To může být užitečné pro obslužnou rutinu, která ověří žádost (vytvoření chybová odpověď).</span><span class="sxs-lookup"><span data-stu-id="6d89d-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="6d89d-141">Přidání obslužné rutiny do kanálu</span><span class="sxs-lookup"><span data-stu-id="6d89d-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="6d89d-142">Pro přidání obslužné rutiny zpráv na straně serveru, přidejte obslužné rutiny **HttpConfiguration.MessageHandlers** kolekce.</span><span class="sxs-lookup"><span data-stu-id="6d89d-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="6d89d-143">Pokud jste použili k vytvoření projektu šablony "Aplikace pro Web ASP.NET MVC 4", můžete k tomu tento uvnitř **WebApiConfig** třídy:</span><span class="sxs-lookup"><span data-stu-id="6d89d-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="6d89d-144">Jsou volány obslužné rutiny zpráv ve stejném pořadí, ve kterém se zobrazují v **MessageHandlers** kolekce.</span><span class="sxs-lookup"><span data-stu-id="6d89d-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="6d89d-145">Vzhledem k tomu, že jsou vnořené, v opačném směru přenáší zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="6d89d-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="6d89d-146">To znamená že poslední obslužnou rutinou je první získá zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="6d89d-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="6d89d-147">Všimněte si, že není nutné nastavit vnitřní obslužných rutin; rozhraní Web API se automaticky připojí obslužné rutiny zpráv.</span><span class="sxs-lookup"><span data-stu-id="6d89d-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="6d89d-148">Pokud jste [s vlastním hostováním](../older-versions/self-host-a-web-api.md), vytvořte instanci **HttpSelfHostConfiguration** třídu a přidejte obslužné rutiny pro **MessageHandlers** kolekce.</span><span class="sxs-lookup"><span data-stu-id="6d89d-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="6d89d-149">Nyní Pojďme se podívat na několik příkladů obslužné rutiny vlastních zpráv.</span><span class="sxs-lookup"><span data-stu-id="6d89d-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="6d89d-150">Příklad: X-HTTP-Method-Override</span><span class="sxs-lookup"><span data-stu-id="6d89d-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="6d89d-151">X-HTTP-Method-Override je nestandardní hlavičku HTTP.</span><span class="sxs-lookup"><span data-stu-id="6d89d-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="6d89d-152">Je určená pro klienty, kteří nemůže odesílat určité typy požadavků HTTP, jako je například PUT nebo DELETE.</span><span class="sxs-lookup"><span data-stu-id="6d89d-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="6d89d-153">Místo toho klient odešle požadavek POST a nastaví hlavičku X-HTTP-Method-Override na požadovanou metodu.</span><span class="sxs-lookup"><span data-stu-id="6d89d-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="6d89d-154">Příklad:</span><span class="sxs-lookup"><span data-stu-id="6d89d-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="6d89d-155">Tady je popisovač zpráv, který přidává podporu pro X-HTTP-Method-Override:</span><span class="sxs-lookup"><span data-stu-id="6d89d-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="6d89d-156">V **SendAsync** metody obslužné rutiny kontroluje, zda je požadavek POST zprávy s požadavkem, a určuje, zda obsahuje hlavičku X-HTTP-Method-Override.</span><span class="sxs-lookup"><span data-stu-id="6d89d-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="6d89d-157">Pokud ano, ověří hodnotu hlavičky a potom upraví metoda žádosti.</span><span class="sxs-lookup"><span data-stu-id="6d89d-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="6d89d-158">A konečně, obslužná rutina zavolá `base.SendAsync` předat další obslužné rutiny zprávy.</span><span class="sxs-lookup"><span data-stu-id="6d89d-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="6d89d-159">Když požadavek dosáhne **HttpControllerDispatcher** třídy **HttpControllerDispatcher** bude směrovat žádosti založené na metodě aktualizace žádosti.</span><span class="sxs-lookup"><span data-stu-id="6d89d-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="6d89d-160">Příklad: Přidání vlastní hlavičky odpovědi</span><span class="sxs-lookup"><span data-stu-id="6d89d-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="6d89d-161">Tady je popisovač zpráv, který přidá vlastní hlavičku každou zprávu s odpovědí:</span><span class="sxs-lookup"><span data-stu-id="6d89d-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="6d89d-162">Nejprve, obslužná rutina zavolá `base.SendAsync` k předání požadavku na vnitřní popisovač zprávy.</span><span class="sxs-lookup"><span data-stu-id="6d89d-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="6d89d-163">Vnitřní obslužná rutina vrátí zprávu odpovědi, ale nepracuje tak asynchronně pomocí **úloh&lt;T&gt;**  objektu.</span><span class="sxs-lookup"><span data-stu-id="6d89d-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="6d89d-164">Zprávy s odpovědí není k dispozici, dokud `base.SendAsync` se dokončí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="6d89d-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="6d89d-165">V tomto příkladu **await** – klíčové slovo a provádí práci asynchronně po `SendAsync` dokončí.</span><span class="sxs-lookup"><span data-stu-id="6d89d-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="6d89d-166">Pokud se zaměřujete na rozhraní .NET Framework 4.0, použijte **úloh**&lt;T&gt;**. ContinueWith** metody:</span><span class="sxs-lookup"><span data-stu-id="6d89d-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="6d89d-167">Příklad: Vyhledání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6d89d-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="6d89d-168">Některé webové služby, aby klienti obsahovat klíč rozhraní API v žádosti.</span><span class="sxs-lookup"><span data-stu-id="6d89d-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="6d89d-169">Následující příklad ukazuje, jak zkontrolovat požadavky na platný klíč rozhraní API obslužné rutiny zpráv:</span><span class="sxs-lookup"><span data-stu-id="6d89d-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="6d89d-170">Tato obslužná rutina hledá klíče rozhraní API v řetězci dotazu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="6d89d-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="6d89d-171">(V tomto příkladu předpokládáme, že klíč je statický řetězec.</span><span class="sxs-lookup"><span data-stu-id="6d89d-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="6d89d-172">Skutečná implementace by pravděpodobně používat složitější ověřování.) Pokud řetězec dotazu obsahuje klíč, obslužná rutina předá žádost vnitřní obslužná rutina.</span><span class="sxs-lookup"><span data-stu-id="6d89d-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="6d89d-173">Pokud požadavek nemá platný klíč, obslužná rutina vytvoří zprávu odpovědi se stavem 403, zakázáno.</span><span class="sxs-lookup"><span data-stu-id="6d89d-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="6d89d-174">V tomto případě obslužná rutina nevolá `base.SendAsync`, takže vnitřní obslužná rutina nikdy obdrží požadavek ani neprovádí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="6d89d-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="6d89d-175">Proto kontroleru můžete předpokládá, že všechny žádosti přicházející platný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6d89d-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="6d89d-176">Klíč rozhraní API se vztahuje pouze na určité akce kontroleru, vezměte v úvahu místo obslužné rutiny zpráv filtru akce.</span><span class="sxs-lookup"><span data-stu-id="6d89d-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="6d89d-177">Filtry akcí se spustí po URI směrování se provádí.</span><span class="sxs-lookup"><span data-stu-id="6d89d-177">Action filters run after URI routing is performed.</span></span>


## <a name="per-route-message-handlers"></a><span data-ttu-id="6d89d-178">Obslužné rutiny zpráv za trasy</span><span class="sxs-lookup"><span data-stu-id="6d89d-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="6d89d-179">Obslužné rutiny ve **HttpConfiguration.MessageHandlers** kolekce platí globálně.</span><span class="sxs-lookup"><span data-stu-id="6d89d-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="6d89d-180">Alternativně můžete přidat obslužné rutiny zpráv na konkrétní postup při definování trasy:</span><span class="sxs-lookup"><span data-stu-id="6d89d-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="6d89d-181">V tomto příkladu, pokud identifikátor URI požadavku odpovídá "Route2" požadavek je odeslána `MessageHandler2`.</span><span class="sxs-lookup"><span data-stu-id="6d89d-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="6d89d-182">Následující diagram znázorňuje kanál pro tyto dvě trasy:</span><span class="sxs-lookup"><span data-stu-id="6d89d-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="6d89d-183">Všimněte si, že `MessageHandler2` nahradí výchozí **HttpControllerDispatcher**.</span><span class="sxs-lookup"><span data-stu-id="6d89d-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="6d89d-184">V tomto příkladu `MessageHandler2` vytvoří odpovědi a požadavky, které odpovídají "Route2" nikdy přejít na kontroler.</span><span class="sxs-lookup"><span data-stu-id="6d89d-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="6d89d-185">Tímto způsobem můžete nahradit celý mechanismus kontroleru webového rozhraní API s vlastní koncový bod.</span><span class="sxs-lookup"><span data-stu-id="6d89d-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="6d89d-186">Alternativně můžete delegovat obslužné rutiny zpráv-route **HttpControllerDispatcher**, která pak odešle zprávu do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="6d89d-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="6d89d-187">Následující kód ukazuje postup při konfiguraci této trasy:</span><span class="sxs-lookup"><span data-stu-id="6d89d-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
