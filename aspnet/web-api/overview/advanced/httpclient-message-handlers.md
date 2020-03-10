---
uid: web-api/overview/advanced/httpclient-message-handlers
title: Obslužné rutiny zpráv HttpClient ve ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Vytváření vlastních obslužných rutin zpráv pro webové rozhraní API ASP.NET v ASP.NET 4. x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557643"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="fd9cc-103">Obslužné rutiny zpráv HttpClient ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fd9cc-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="fd9cc-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fd9cc-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fd9cc-105">*Obslužná rutina zprávy* je třída, která přijme požadavek HTTP a vrátí odpověď HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="fd9cc-106">Obvykle je řada obslužných rutin zpráv zřetězena dohromady.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="fd9cc-107">První obslužná rutina přijme požadavek HTTP, provede nějaké zpracování a udělí požadavek Další obslužné rutině.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="fd9cc-108">V určitém okamžiku se odpověď vytvoří a zálohuje řetězec.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="fd9cc-109">Tento model se nazývá *delegování* obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="fd9cc-110">Na straně klienta třída **HttpClient** používá ke zpracování požadavků obslužnou rutinu zprávy.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="fd9cc-111">Výchozí obslužná rutina je **HttpClientHandler**, která odesílá požadavek přes síť a získá odpověď ze serveru.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="fd9cc-112">Do kanálu klienta můžete vložit vlastní obslužné rutiny zpráv:</span><span class="sxs-lookup"><span data-stu-id="fd9cc-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="fd9cc-113">Webové rozhraní API ASP.NET také používá obslužné rutiny zpráv na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="fd9cc-114">Další informace najdete v tématu [obslužné rutiny zpráv HTTP](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="fd9cc-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="fd9cc-115">Vlastní obslužné rutiny zpráv</span><span class="sxs-lookup"><span data-stu-id="fd9cc-115">Custom Message Handlers</span></span>

<span data-ttu-id="fd9cc-116">Chcete-li napsat vlastní obslužnou rutinu zpráv, odvodit ze **System .NET. http. DelegatingHandler** a přepsat metodu **SendAsync** .</span><span class="sxs-lookup"><span data-stu-id="fd9cc-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="fd9cc-117">Tady je podpis této metody:</span><span class="sxs-lookup"><span data-stu-id="fd9cc-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="fd9cc-118">Metoda přebírá **zprávy HttpRequestMessage** jako vstup a asynchronně vrátí **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="fd9cc-119">Typická implementace provede následující:</span><span class="sxs-lookup"><span data-stu-id="fd9cc-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="fd9cc-120">Zpracování zprávy s požadavkem.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-120">Process the request message.</span></span>
2. <span data-ttu-id="fd9cc-121">Zavolejte `base.SendAsync` k odeslání požadavku vnitřní obslužné rutině.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="fd9cc-122">Vnitřní obslužná rutina vrátí zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-122">The inner handler returns a response message.</span></span> <span data-ttu-id="fd9cc-123">(Tento krok je asynchronní.)</span><span class="sxs-lookup"><span data-stu-id="fd9cc-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="fd9cc-124">Zpracujte odpověď a vraťte ji volajícímu.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="fd9cc-125">Následující příklad ukazuje popisovač zprávy, který přidá vlastní hlavičku do odchozího požadavku:</span><span class="sxs-lookup"><span data-stu-id="fd9cc-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="fd9cc-126">Volání `base.SendAsync` je asynchronní.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="fd9cc-127">Pokud obslužná rutina po tomto volání funguje, použijte klíčové slovo **await** pro pokračování v provádění po dokončení metody.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="fd9cc-128">Následující příklad ukazuje obslužnou rutinu, která protokoluje kódy chyb.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="fd9cc-129">Samotné protokolování není velice zajímavé, ale tento příklad ukazuje, jak získat odpověď v rámci obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="fd9cc-130">Přidání obslužných rutin zpráv do kanálu klienta</span><span class="sxs-lookup"><span data-stu-id="fd9cc-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="fd9cc-131">Chcete-li přidat vlastní obslužné rutiny do **HttpClient**, použijte metodu **HttpClientFactory. Create** :</span><span class="sxs-lookup"><span data-stu-id="fd9cc-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="fd9cc-132">Obslužné rutiny zpráv jsou volány v pořadí, které je předáváte do metody **Create** .</span><span class="sxs-lookup"><span data-stu-id="fd9cc-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="fd9cc-133">Vzhledem k tomu, že obslužné rutiny jsou vnořené, zpráva odpovědi se přenáší do druhého směru.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="fd9cc-134">To znamená, že poslední obslužná rutina je první, aby zobrazila zprávu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="fd9cc-134">That is, the last handler is the first to get the response message.</span></span>
