---
uid: webhooks/diagnostics/logging
title: Protokolování webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Postup při protokolování webhooků ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: a05b32c4a8f9577bcf6170bd19a9e440b1aeb75b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457580"
---
# <a name="aspnet-webhooks-logging"></a>Protokolování webhooků ASP.NET

Microsoft ASP.NET webhooků používá protokolování jako způsob, jakým se hlásí problémy a problémy. Ve výchozím nastavení jsou protokoly zapisovány pomocí [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) , kde je lze spravovaných pomocí [posluchačů trasování](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) jako jakýkoli jiný datový proud protokolu.

Když nasadíte webovou aplikaci jako webovou aplikaci Azure, protokoly se automaticky vybírají a dají se spravovat společně s jakýmkoli jiným protokolováním [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) . Podrobnosti najdete [v tématu Povolení protokolování diagnostiky pro webové aplikace v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Kromě toho je možné protokoly získat přímo ze sady Visual Studio, jak je popsáno v tématu [řešení potíží s webovou aplikací v Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="redirecting-logs"></a>Přesměrování protokolů

Místo psaní protokolů do [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)je možné poskytnout alternativní implementaci protokolování, která se může protokolovat přímo do Správce protokolů, jako je [Log4Net](http://logging.apache.org/log4net/) a [nLOG](http://nlog-project.org/). Jednoduše Poskytněte implementaci [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) a zaregistrujte ji s modulem injektáže závislosti dle vašeho výběru a vystaví se Microsoft ASP.NET webhookech. Podrobnosti najdete [v článku vkládání závislostí ve webovém rozhraní API 2 ASP.NET](https://www.asp.net/web-api/overview/advanced/dependency-injection) .
