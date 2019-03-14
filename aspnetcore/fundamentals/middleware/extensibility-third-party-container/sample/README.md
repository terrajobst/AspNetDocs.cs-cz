---
ms.openlocfilehash: 282871e5db197dfb4226cc02918f2d6ba1135c04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072322"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a><span data-ttu-id="30f4e-101">Ukázky rozšiřitelnosti Middleware ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="30f4e-101">ASP.NET Core Middleware Extensibility Sample</span></span>

<span data-ttu-id="30f4e-102">Tento příklad ukazuje použití metody [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) a [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) s 3. stran kontejner vkládání závislostí, [jednoduché Injector](https://simpleinjector.org).</span><span class="sxs-lookup"><span data-stu-id="30f4e-102">This sample illustrates the use of [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) and [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) with a 3rd party dependency injection container, [Simple Injector](https://simpleinjector.org).</span></span> <span data-ttu-id="30f4e-103">Tato ukázka demonstruje funkce popsané v [Middleware aktivace s kontejnerem jiného výrobce v ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).</span><span class="sxs-lookup"><span data-stu-id="30f4e-103">This sample demonstrates the features described in [Middleware activation with a third-party container in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container).</span></span>
