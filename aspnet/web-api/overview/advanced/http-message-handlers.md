---
uid: web-api/overview/advanced/http-message-handlers
title: Obslužné rutiny zpráv HTTP ve webovém rozhraní API ASP.NET – ASP.NET 4. x
author: MikeWasson
description: Přehled obslužných rutin zpráv HTTP ve webovém rozhraní API ASP.NET pro ASP.NET 4. x
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622582"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="bd5ec-103">Obslužné rutiny zpráv HTTP ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bd5ec-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="bd5ec-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bd5ec-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bd5ec-105">*Obslužná rutina zprávy* je třída, která přijme požadavek HTTP a vrátí odpověď HTTP.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="bd5ec-106">Obslužné rutiny zpráv jsou odvozeny od abstraktní třídy **HttpMessageHandler** .</span><span class="sxs-lookup"><span data-stu-id="bd5ec-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="bd5ec-107">Obvykle je řada obslužných rutin zpráv zřetězena dohromady.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="bd5ec-108">První obslužná rutina přijme požadavek HTTP, provede nějaké zpracování a udělí požadavek Další obslužné rutině.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="bd5ec-109">V určitém okamžiku se odpověď vytvoří a zálohuje řetězec.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="bd5ec-110">Tento model se nazývá *delegování* obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="bd5ec-111">Obslužné rutiny zpráv na straně serveru</span><span class="sxs-lookup"><span data-stu-id="bd5ec-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="bd5ec-112">Kanál webového rozhraní API na straně serveru používá některé integrované obslužné rutiny zpráv:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="bd5ec-113">**HttpServer** Získá požadavek od hostitele.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="bd5ec-114">**HttpRoutingDispatcher** odesílá požadavek na základě trasy.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="bd5ec-115">**HttpControllerDispatcher** odešle požadavek na kontroler webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="bd5ec-116">Do kanálu můžete přidat vlastní obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="bd5ec-117">Obslužné rutiny zpráv jsou vhodné pro průřezové problémy, které fungují na úrovni zpráv HTTP (místo akcí kontroleru).</span><span class="sxs-lookup"><span data-stu-id="bd5ec-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="bd5ec-118">Například obslužná rutina zprávy může:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-118">For example, a message handler might:</span></span>

- <span data-ttu-id="bd5ec-119">Čtení nebo úpravy hlaviček požadavků.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-119">Read or modify request headers.</span></span>
- <span data-ttu-id="bd5ec-120">Přidejte hlavičku odpovědi na odpovědi.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-120">Add a response header to responses.</span></span>
- <span data-ttu-id="bd5ec-121">Ověřte žádosti předtím, než se dostanou k řadiči.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="bd5ec-122">Tento diagram znázorňuje dva vlastní obslužné rutiny vložené do kanálu:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="bd5ec-123">Na straně klienta HttpClient také používá obslužné rutiny zpráv.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="bd5ec-124">Další informace najdete v tématu [obslužné rutiny zpráv HttpClient](httpclient-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="bd5ec-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="bd5ec-125">Vlastní obslužné rutiny zpráv</span><span class="sxs-lookup"><span data-stu-id="bd5ec-125">Custom Message Handlers</span></span>

<span data-ttu-id="bd5ec-126">Chcete-li napsat vlastní obslužnou rutinu zpráv, odvodit ze **System .NET. http. DelegatingHandler** a přepsat metodu **SendAsync** .</span><span class="sxs-lookup"><span data-stu-id="bd5ec-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="bd5ec-127">Tato metoda má následující signaturu:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="bd5ec-128">Metoda přebírá **zprávy HttpRequestMessage** jako vstup a asynchronně vrátí **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="bd5ec-129">Typická implementace provede následující:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="bd5ec-130">Zpracování zprávy s požadavkem.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-130">Process the request message.</span></span>
2. <span data-ttu-id="bd5ec-131">Zavolejte `base.SendAsync` k odeslání požadavku vnitřní obslužné rutině.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="bd5ec-132">Vnitřní obslužná rutina vrátí zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-132">The inner handler returns a response message.</span></span> <span data-ttu-id="bd5ec-133">(Tento krok je asynchronní.)</span><span class="sxs-lookup"><span data-stu-id="bd5ec-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="bd5ec-134">Zpracujte odpověď a vraťte ji volajícímu.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="bd5ec-135">Tady je triviální příklad:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="bd5ec-136">Volání `base.SendAsync` je asynchronní.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="bd5ec-137">Pokud obslužná rutina po tomto volání funguje, použijte klíčové slovo **await** , jak je znázorněno.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="bd5ec-138">Delegování obslužné rutiny může také přeskočit vnitřní obslužnou rutinu a přímo vytvořit odpověď:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="bd5ec-139">Pokud obslužná rutina delegování vytvoří odpověď bez volání `base.SendAsync`, požadavek přeskočí zbytek kanálu.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="bd5ec-140">To může být užitečné pro obslužnou rutinu, která ověřuje požadavek (vytvoření chybové odpovědi).</span><span class="sxs-lookup"><span data-stu-id="bd5ec-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="bd5ec-141">Přidání obslužné rutiny do kanálu</span><span class="sxs-lookup"><span data-stu-id="bd5ec-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="bd5ec-142">Chcete-li přidat obslužnou rutinu zprávy na straně serveru, přidejte obslužnou rutinu do kolekce **HttpConfiguration. MessageHandlers** .</span><span class="sxs-lookup"><span data-stu-id="bd5ec-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="bd5ec-143">Pokud jste k vytvoření projektu použili šablonu webová aplikace ASP.NET MVC 4, můžete to provést uvnitř třídy **WebApiConfig** :</span><span class="sxs-lookup"><span data-stu-id="bd5ec-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="bd5ec-144">Obslužné rutiny zpráv jsou volány ve stejném pořadí, v jakém jsou uvedeny v kolekci **MessageHandlers** .</span><span class="sxs-lookup"><span data-stu-id="bd5ec-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="bd5ec-145">Vzhledem k tomu, že jsou vnořené, bude zpráva odpovědi přenášena v jiném směru.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="bd5ec-146">To znamená, že poslední obslužná rutina je první, aby zobrazila zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="bd5ec-147">Všimněte si, že nemusíte nastavovat vnitřní obslužné rutiny; rozhraní Web API Framework automaticky propojuje obslužné rutiny zpráv.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="bd5ec-148">Pokud provádíte [samoobslužné hostování](../older-versions/self-host-a-web-api.md), vytvořte instanci třídy **HttpSelfHostConfiguration** a přidejte obslužné rutiny do kolekce **MessageHandlers** .</span><span class="sxs-lookup"><span data-stu-id="bd5ec-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="bd5ec-149">Teď se podívejme na některé příklady vlastních obslužných rutin zpráv.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="bd5ec-150">Příklad: X-HTTP-Method – přepsat</span><span class="sxs-lookup"><span data-stu-id="bd5ec-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="bd5ec-151">X-HTTP-Method-override je nestandardní hlavička HTTP.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="bd5ec-152">Je určená pro klienty, kteří nemůžou odesílat určité typy požadavků HTTP, jako je třeba PUT nebo DELETE.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="bd5ec-153">Místo toho klient odešle požadavek POST a nastaví hlavičku X-HTTP-Method-override na požadovanou metodu.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="bd5ec-154">Příklad:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="bd5ec-155">Tady je obslužná rutina zprávy, která přidává podporu pro X-HTTP-Method-override:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="bd5ec-156">V metodě **SendAsync** obslužná rutina kontroluje, zda je zpráva požadavku POST, a zda obsahuje hlavičku X-http-Method – přepsat.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="bd5ec-157">Pokud ano, ověří hodnotu v hlavičce a pak upraví metodu žádosti.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="bd5ec-158">Nakonec obslužná rutina volá `base.SendAsync` k předání zprávy do další obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="bd5ec-159">Když požadavek dosáhne třídy **HttpControllerDispatcher** , **HttpControllerDispatcher** bude směrovat požadavek na základě aktualizované metody žádosti.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="bd5ec-160">Příklad: Přidání vlastní hlavičky odpovědi</span><span class="sxs-lookup"><span data-stu-id="bd5ec-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="bd5ec-161">Tady je obslužná rutina zprávy, která přidá vlastní hlavičku do každé zprávy odpovědi:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="bd5ec-162">Za prvé obslužná rutina volá `base.SendAsync`, aby odeslala požadavek do vnitřní obslužné rutiny zpráv.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="bd5ec-163">Vnitřní obslužná rutina vrátí zprávu odpovědi, ale provede asynchronní použití objektu **Task&lt;t&gt;** Object.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="bd5ec-164">Zpráva s odpovědí není k dispozici, dokud se `base.SendAsync` nedokončí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="bd5ec-165">Tento příklad používá klíčové slovo **await** k asynchronnímu zpracování práce po dokončení `SendAsync`.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="bd5ec-166">Pokud cílíte .NET Framework 4,0, použijte&gt;**úlohy**&lt;t **. Metoda ContinueWith** :</span><span class="sxs-lookup"><span data-stu-id="bd5ec-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="bd5ec-167">Příklad: Kontrola klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="bd5ec-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="bd5ec-168">Některé webové služby vyžadují, aby klienti do své žádosti zahrnuli klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="bd5ec-169">Následující příklad ukazuje, jak může obslužná rutina zprávy kontrolovat žádosti o platný klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="bd5ec-170">Tato obslužná rutina hledá klíč rozhraní API v řetězci dotazu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="bd5ec-171">(V tomto příkladu předpokládáme, že klíč je statický řetězec.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="bd5ec-172">Skutečná implementace by pravděpodobně použila složitější ověřování.) Pokud řetězec dotazu obsahuje klíč, obslužná rutina předá požadavek vnitřní obslužné rutině.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="bd5ec-173">Pokud požadavek nemá platný klíč, obslužná rutina vytvoří zprávu odpovědi se stavem 403, zakázáno.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="bd5ec-174">V tomto případě obslužná rutina nevolá `base.SendAsync`, takže vnitřní obslužná rutina nikdy neobdrží požadavek ani neprovádí kontroler.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="bd5ec-175">Proto může kontroler předpokládat, že všechny příchozí požadavky mají platný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="bd5ec-176">Pokud se klíč rozhraní API vztahuje pouze na určité akce kontroleru, zvažte použití filtru akcí namísto obslužné rutiny zprávy.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="bd5ec-177">Filtry akcí se spustí po provedení směrování identifikátorů URI.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="bd5ec-178">Obslužné rutiny zpráv pro směrování</span><span class="sxs-lookup"><span data-stu-id="bd5ec-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="bd5ec-179">Obslužné rutiny v kolekci **HttpConfiguration. MessageHandlers** platí globálně.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="bd5ec-180">Případně můžete při definování trasy přidat do konkrétní trasy obslužnou rutinu zpráv:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="bd5ec-181">Pokud v tomto příkladu identifikátor URI žádosti odpovídá "Route2", požadavek se odešle na `MessageHandler2`.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="bd5ec-182">Následující diagram znázorňuje kanál těchto dvou tras:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="bd5ec-183">Všimněte si, že `MessageHandler2` nahradí výchozí **HttpControllerDispatcher**.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="bd5ec-184">V tomto příkladu `MessageHandler2` vytvoří odpověď a požadavky, které odpovídají "Route2" nikdy nejdou na kontroler.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="bd5ec-185">To vám umožní nahradit celý mechanizmus kontroleru webového rozhraní API vlastním koncovým bodem.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="bd5ec-186">Alternativně může obslužná rutina zprávy pro směrování delegovat na **HttpControllerDispatcher**, která pak odesílá do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="bd5ec-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="bd5ec-187">Následující kód ukazuje, jak nakonfigurovat tuto trasu:</span><span class="sxs-lookup"><span data-stu-id="bd5ec-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
