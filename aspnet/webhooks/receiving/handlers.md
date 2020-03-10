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
# <a name="aspnet-webhooks-handlers"></a>Obslužné rutiny webhooků ASP.NET

Po ověření požadavků webhooků přijímačem Webhooku je možné ho zpracovat pomocí uživatelského kódu. Zde jsou uvedené *obslužné rutiny* . Obslužné rutiny jsou odvozeny z rozhraní [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) , ale obvykle používá třídu [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) namísto odvození přímo z rozhraní.

Požadavek Webhooku může být zpracován jedním nebo více obslužnými rutinami. Obslužné rutiny jsou volány v pořadí podle jejich příslušné vlastnosti *Order* z nejnižší na nejvyšší, kde pořadí je jednoduché celé číslo (navržené v rozmezí od 1 do 100):

![Diagram vlastnosti pořadí obslužné rutiny Webhooku](_static/Handlers.png)

Obslužná rutina může volitelně nastavit vlastnost *Response* na WebHookHandlerContext, která způsobí, že se zpracování zastaví a odpověď se pošle zpátky jako odpověď HTTP na Webhook. V případě výše se obslužná rutina C nevolá, protože má vyšší pořadí než B a B nastavuje odpověď.

Nastavení odpovědi je obvykle relevantní pouze pro Webhooky, kde odpověď může přenášet informace zpět do původního rozhraní API. To je například případ s Webhooky časové rezervy, kde je odpověď odeslána zpátky do kanálu, ze kterého pochází Webhook. Obslužné rutiny mohou nastavit vlastnost přijímače, pokud chtějí přijímat pouze Webhooky z tohoto konkrétního přijímače. Pokud nenastaví přijímač, který se bude volat pro všechny z nich.

Jednou z dalších běžných použití odpovědi je použití odpovědi *410* , která značí, že Webhook již není aktivní a žádné další požadavky by se neměly odesílat.

Ve výchozím nastavení bude obslužná rutina volána všemi přijímači Webhooku. Pokud je však vlastnost *příjemce* nastavena na název obslužné rutiny, pak bude tato obslužná rutina přijímat pouze žádosti Webhooku od tohoto příjemce.

## <a name="processing-a-webhook"></a>Zpracování Webhooku

Když je volána obslužná rutina, získá [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) obsahující informace o požadavku Webhooku. Data, obvykle tělo požadavku HTTP, jsou k dispozici z vlastnosti *data* .

Typ dat je typicky data formuláře JSON nebo HTML, ale pokud je to potřeba, můžete přetypovat na konkrétnější typ. Například vlastní Webhooky vygenerované Webhooky ASP.NET je možné přetypovat na typ [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) následujícím způsobem:

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

  ## <a name="queued-processing"></a>Zpracování ve frontě

Většina odesílatelů Webhooku pošle Webhook znovu, pokud odpověď nebude vygenerována během několiky sekund. To znamená, že vaše obslužná rutina musí dokončit zpracování v tomto časovém rámci, aby ji nebylo možné volat znovu.

Pokud zpracování trvá déle nebo je lépe zpracováváno samostatně, můžete [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) použít k odeslání požadavku Webhooku do fronty, například [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).

Osnova implementace [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) je k dispozici zde:

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
