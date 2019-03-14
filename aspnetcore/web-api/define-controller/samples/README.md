---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066073"
---
# <a name="aspnet-core-web-api-controller-sample"></a>Ukázka Kontroleru rozhraní API ASP.NET Core Web

Tato ukázková aplikace se skládá z následující projekty:

- **WebApiSample.Api.22*: Projekt ASP.NET Core 2.2 cílí na .NET Core 2.2.
- **WebApiSample.Api.21**: Projekt ASP.NET Core 2.1 cílí na .NET Core 2.1.
- **WebApiSample.Api.Pre21**: Projekt ASP.NET Core 2.0, která cílí na .NET Core 2.0.
- **WebApiSample.DataAccess**: Knihovna tříd .NET Standard 2.0, který slouží jako vrstvě přístupu k datům pro 2 projekty webového rozhraní API.

Tato ukázka ilustruje variace vytvoření kontroleru webového rozhraní API:

- [Odvodit třídu z ControllerBase](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [Třída s atributem ApiControllerAttribute opatřit poznámkami](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
