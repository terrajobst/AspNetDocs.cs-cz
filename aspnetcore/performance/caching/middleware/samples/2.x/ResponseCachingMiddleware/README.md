---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077476"
---
# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="76bea-101">Ukázku ukládání do mezipaměti odpovědi ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="76bea-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="76bea-102">Tato ukázka ilustruje použití ASP.NET Core [Middleware pro ukládání do mezipaměti odpovědí](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span><span class="sxs-lookup"><span data-stu-id="76bea-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="76bea-103">Aplikace odpoví indexovou stránku, včetně `Cache-Control` záhlaví konfigurace chování ukládání do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="76bea-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="76bea-104">Aplikace také nastaví `Vary` záhlaví postup při konfiguraci mezipaměti pro obsluhu odpovědi pouze tehdy, pokud `Accept-Encoding` odpovídá záhlaví následné žádosti z původního požadavku.</span><span class="sxs-lookup"><span data-stu-id="76bea-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="76bea-105">Při spuštění ukázky, Index stránky se načítají z mezipaměti pro ukládání a uložit do mezipaměti po dobu až 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="76bea-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>
