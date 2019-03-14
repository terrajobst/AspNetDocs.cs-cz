---
ms.openlocfilehash: b6f39dd0dedb38961eb021cde355f7ec83283195
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066073"
---
# <a name="aspnet-core-web-api-controller-sample"></a><span data-ttu-id="2635e-101">Ukázka Kontroleru rozhraní API ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="2635e-101">ASP.NET Core Web API Controller Sample</span></span>

<span data-ttu-id="2635e-102">Tato ukázková aplikace se skládá z následující projekty:</span><span class="sxs-lookup"><span data-stu-id="2635e-102">This sample app consists of the following projects:</span></span>

- <span data-ttu-id="2635e-103">\**WebApiSample.Api.22*: Projekt ASP.NET Core 2.2 cílí na .NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="2635e-103">\**WebApiSample.Api.22*: An ASP.NET Core 2.2 project targeting .NET Core 2.2.</span></span>
- <span data-ttu-id="2635e-104">**WebApiSample.Api.21**: Projekt ASP.NET Core 2.1 cílí na .NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="2635e-104">**WebApiSample.Api.21**: An ASP.NET Core 2.1 project targeting .NET Core 2.1.</span></span>
- <span data-ttu-id="2635e-105">**WebApiSample.Api.Pre21**: Projekt ASP.NET Core 2.0, která cílí na .NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="2635e-105">**WebApiSample.Api.Pre21**: An ASP.NET Core 2.0 project targeting .NET Core 2.0.</span></span>
- <span data-ttu-id="2635e-106">**WebApiSample.DataAccess**: Knihovna tříd .NET Standard 2.0, který slouží jako vrstvě přístupu k datům pro 2 projekty webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2635e-106">**WebApiSample.DataAccess**: A .NET Standard 2.0 class library serving as a data access tier for the 2 Web API projects.</span></span>

<span data-ttu-id="2635e-107">Tato ukázka ilustruje variace vytvoření kontroleru webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="2635e-107">This sample illustrates variations of Web API controller creation:</span></span>

- [<span data-ttu-id="2635e-108">Odvodit třídu z ControllerBase</span><span class="sxs-lookup"><span data-stu-id="2635e-108">Derive class from ControllerBase</span></span>](https://docs.microsoft.com/aspnet/core/web-api#derive-class-from-controllerbase)
- [<span data-ttu-id="2635e-109">Třída s atributem ApiControllerAttribute opatřit poznámkami</span><span class="sxs-lookup"><span data-stu-id="2635e-109">Annotate class with ApiControllerAttribute</span></span>](https://docs.microsoft.com/aspnet/core/web-api#annotate-class-with-apicontrollerattribute)
