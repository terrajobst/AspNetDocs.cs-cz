---
ms.openlocfilehash: 282871e5db197dfb4226cc02918f2d6ba1135c04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072322"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a>Ukázky rozšiřitelnosti Middleware ASP.NET Core

Tento příklad ukazuje použití metody [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) a [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) s 3. stran kontejner vkládání závislostí, [jednoduché Injector](https://simpleinjector.org). Tato ukázka demonstruje funkce popsané v [Middleware aktivace s kontejnerem jiného výrobce v ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).
