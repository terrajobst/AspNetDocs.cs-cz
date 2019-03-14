---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077476"
---
# <a name="aspnet-core-response-caching-sample"></a>Ukázku ukládání do mezipaměti odpovědi ASP.NET Core

Tato ukázka ilustruje použití ASP.NET Core [Middleware pro ukládání do mezipaměti odpovědí](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).

Aplikace odpoví indexovou stránku, včetně `Cache-Control` záhlaví konfigurace chování ukládání do mezipaměti. Aplikace také nastaví `Vary` záhlaví postup při konfiguraci mezipaměti pro obsluhu odpovědi pouze tehdy, pokud `Accept-Encoding` odpovídá záhlaví následné žádosti z původního požadavku.

Při spuštění ukázky, Index stránky se načítají z mezipaměti pro ukládání a uložit do mezipaměti po dobu až 10 sekund.
