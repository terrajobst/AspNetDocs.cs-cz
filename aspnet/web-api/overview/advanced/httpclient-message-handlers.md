---
uid: web-api/overview/advanced/httpclient-message-handlers
title: Obslužné rutiny zpráv HttpClient v rozhraní ASP.NET Web API – ASP.NET 4.x
author: MikeWasson
description: Vytvoření obslužné rutiny vlastních zpráv pro ASP.NET Web API v ASP.NET 4.x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115445"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="dd7a4-103">Obslužné rutiny zpráv HttpClient ve webovém rozhraní API technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dd7a4-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="dd7a4-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dd7a4-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="dd7a4-105">A *obslužná rutina zprávy* je třída, která přijme požadavek HTTP a vrátí odpověď HTTP.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="dd7a4-106">Řada obslužné rutiny zpráv jsou obvykle zřetězen dohromady.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="dd7a4-107">První obslužná rutina požadavku HTTP, provádí nějaké zpracování a poskytuje k další obslužná rutina požadavku.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="dd7a4-108">V určitém okamžiku odpovědi se vytvoří a vrátí řetězem.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="dd7a4-109">Tento model se nazývá *delegování* obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="dd7a4-110">Na straně klienta **HttpClient** třída používá obslužné rutiny zpráv pro zpracování žádostí.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="dd7a4-111">Je výchozí obslužnou rutinu **HttpClientHandler**, který odešle požadavek v síti a získá odpověď ze serveru.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="dd7a4-112">Obslužné rutiny vlastních zpráv můžete vložit do kanálu klienta:</span><span class="sxs-lookup"><span data-stu-id="dd7a4-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="dd7a4-113">Rozhraní ASP.NET Web API také používá obslužné rutiny zpráv na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="dd7a4-114">Další informace najdete v tématu [obslužné rutiny zpráv HTTP](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="dd7a4-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="dd7a4-115">Obslužné rutiny vlastních zpráv</span><span class="sxs-lookup"><span data-stu-id="dd7a4-115">Custom Message Handlers</span></span>

<span data-ttu-id="dd7a4-116">Zápis obslužné rutiny vlastních zpráv, jsou odvozeny z **System.Net.Http.DelegatingHandler** a přepsat **SendAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="dd7a4-117">Následuje podpis metody:</span><span class="sxs-lookup"><span data-stu-id="dd7a4-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="dd7a4-118">Tato metoda přebírá **HttpRequestMessage** jako vstup a asynchronně vrátí **objekt HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="dd7a4-119">Obvyklá implementace provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="dd7a4-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="dd7a4-120">Zpracování zprávy s požadavkem.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-120">Process the request message.</span></span>
2. <span data-ttu-id="dd7a4-121">Volání `base.SendAsync` odešlete žádost na vnitřní obslužnou rutinu.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="dd7a4-122">Vnitřní obslužná rutina vrátí zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-122">The inner handler returns a response message.</span></span> <span data-ttu-id="dd7a4-123">(Tento krok je asynchronní.)</span><span class="sxs-lookup"><span data-stu-id="dd7a4-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="dd7a4-124">Zpracování odpovědi a vrátí řízení volajícímu.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="dd7a4-125">Následující příklad ukazuje popisovač zpráv, který přidá vlastní hlavičku na odchozí žádost:</span><span class="sxs-lookup"><span data-stu-id="dd7a4-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="dd7a4-126">Volání `base.SendAsync` je asynchronní.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="dd7a4-127">Pokud obslužná rutina nemá žádnou práci po tomto volání, použijte **await** – klíčové slovo pokračování provádění po dokončení metody.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="dd7a4-128">Následující příklad ukazuje obslužnou rutinu, která protokoluje kódy chyb.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="dd7a4-129">Protokolování samotný není moc zajímavý, ale tento příklad ukazuje, jak získat odpovědi uvnitř obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="dd7a4-130">Přidání obslužných rutin zpráv do kanálu klienta</span><span class="sxs-lookup"><span data-stu-id="dd7a4-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="dd7a4-131">Chcete-li přidat vlastní obslužné rutiny pro **HttpClient**, použijte **HttpClientFactory.Create** metody:</span><span class="sxs-lookup"><span data-stu-id="dd7a4-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="dd7a4-132">Obslužné rutiny zpráv jsou volány v pořadí, ve kterém můžete předat je do **vytvořit** metody.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="dd7a4-133">Vzhledem k tomu, že jsou vnořené obslužných rutin, v opačném směru přenáší zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="dd7a4-134">To znamená že poslední obslužnou rutinou je první získá zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="dd7a4-134">That is, the last handler is the first to get the response message.</span></span>
