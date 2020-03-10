---
uid: webhooks/receiving/handlers
title: Obslužné rutiny webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Jak zpracovávat požadavky v webhookech ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637870"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="c7318-103">Obslužné rutiny webhooků ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c7318-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="c7318-104">Po ověření požadavků webhooků přijímačem Webhooku je možné ho zpracovat pomocí uživatelského kódu.</span><span class="sxs-lookup"><span data-stu-id="c7318-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="c7318-105">Zde jsou uvedené *obslužné rutiny* .</span><span class="sxs-lookup"><span data-stu-id="c7318-105">This is where *handlers* come in.</span></span> <span data-ttu-id="c7318-106">Obslužné rutiny jsou odvozeny z rozhraní [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) , ale obvykle používá třídu [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) namísto odvození přímo z rozhraní.</span><span class="sxs-lookup"><span data-stu-id="c7318-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="c7318-107">Požadavek Webhooku může být zpracován jedním nebo více obslužnými rutinami.</span><span class="sxs-lookup"><span data-stu-id="c7318-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="c7318-108">Obslužné rutiny jsou volány v pořadí podle jejich příslušné vlastnosti *Order* z nejnižší na nejvyšší, kde pořadí je jednoduché celé číslo (navržené v rozmezí od 1 do 100):</span><span class="sxs-lookup"><span data-stu-id="c7318-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![Diagram vlastnosti pořadí obslužné rutiny Webhooku](_static/Handlers.png)

<span data-ttu-id="c7318-110">Obslužná rutina může volitelně nastavit vlastnost *Response* na WebHookHandlerContext, která způsobí, že se zpracování zastaví a odpověď se pošle zpátky jako odpověď HTTP na Webhook.</span><span class="sxs-lookup"><span data-stu-id="c7318-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="c7318-111">V případě výše se obslužná rutina C nevolá, protože má vyšší pořadí než B a B nastavuje odpověď.</span><span class="sxs-lookup"><span data-stu-id="c7318-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="c7318-112">Nastavení odpovědi je obvykle relevantní pouze pro Webhooky, kde odpověď může přenášet informace zpět do původního rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="c7318-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="c7318-113">To je například případ s Webhooky časové rezervy, kde je odpověď odeslána zpátky do kanálu, ze kterého pochází Webhook.</span><span class="sxs-lookup"><span data-stu-id="c7318-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="c7318-114">Obslužné rutiny mohou nastavit vlastnost přijímače, pokud chtějí přijímat pouze Webhooky z tohoto konkrétního přijímače.</span><span class="sxs-lookup"><span data-stu-id="c7318-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="c7318-115">Pokud nenastaví přijímač, který se bude volat pro všechny z nich.</span><span class="sxs-lookup"><span data-stu-id="c7318-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="c7318-116">Jednou z dalších běžných použití odpovědi je použití odpovědi *410* , která značí, že Webhook již není aktivní a žádné další požadavky by se neměly odesílat.</span><span class="sxs-lookup"><span data-stu-id="c7318-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="c7318-117">Ve výchozím nastavení bude obslužná rutina volána všemi přijímači Webhooku.</span><span class="sxs-lookup"><span data-stu-id="c7318-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="c7318-118">Pokud je však vlastnost *příjemce* nastavena na název obslužné rutiny, pak bude tato obslužná rutina přijímat pouze žádosti Webhooku od tohoto příjemce.</span><span class="sxs-lookup"><span data-stu-id="c7318-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="c7318-119">Zpracování Webhooku</span><span class="sxs-lookup"><span data-stu-id="c7318-119">Processing a WebHook</span></span>

<span data-ttu-id="c7318-120">Když je volána obslužná rutina, získá [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) obsahující informace o požadavku Webhooku.</span><span class="sxs-lookup"><span data-stu-id="c7318-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="c7318-121">Data, obvykle tělo požadavku HTTP, jsou k dispozici z vlastnosti *data* .</span><span class="sxs-lookup"><span data-stu-id="c7318-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="c7318-122">Typ dat je typicky data formuláře JSON nebo HTML, ale pokud je to potřeba, můžete přetypovat na konkrétnější typ.</span><span class="sxs-lookup"><span data-stu-id="c7318-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="c7318-123">Například vlastní Webhooky vygenerované Webhooky ASP.NET je možné přetypovat na typ [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="c7318-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="c7318-124">Zpracování ve frontě</span><span class="sxs-lookup"><span data-stu-id="c7318-124">Queued Processing</span></span>

<span data-ttu-id="c7318-125">Většina odesílatelů Webhooku pošle Webhook znovu, pokud odpověď nebude vygenerována během několiky sekund.</span><span class="sxs-lookup"><span data-stu-id="c7318-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="c7318-126">To znamená, že vaše obslužná rutina musí dokončit zpracování v tomto časovém rámci, aby ji nebylo možné volat znovu.</span><span class="sxs-lookup"><span data-stu-id="c7318-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="c7318-127">Pokud zpracování trvá déle nebo je lépe zpracováváno samostatně, můžete [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) použít k odeslání požadavku Webhooku do fronty, například [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7318-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="c7318-128">Osnova implementace [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) je k dispozici zde:</span><span class="sxs-lookup"><span data-stu-id="c7318-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
