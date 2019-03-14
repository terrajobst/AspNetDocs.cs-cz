---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075607"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="14ef6-101">Úlohy na pozadí ASP.NET Core vzorku (obecný hostitele)</span><span class="sxs-lookup"><span data-stu-id="14ef6-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="14ef6-102">Tento příklad ukazuje použití metody [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span><span class="sxs-lookup"><span data-stu-id="14ef6-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="14ef6-103">Tato ukázka demonstruje funkce popsané v [úloh s hostovanými službami v ASP.NET Core na pozadí](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) tématu.</span><span class="sxs-lookup"><span data-stu-id="14ef6-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="14ef6-104">Při spuštění ukázky [Visual Studio Code](https://code.visualstudio.com/), nastavte **konzoly** hodnota konfigurace konzoly v *.vscode/launch.json* buď `externalTerminal` nebo `integratedTerminal`.</span><span class="sxs-lookup"><span data-stu-id="14ef6-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="14ef6-105">Použití `internalConsole` není kompatibilní s konzoly stisk klávesy vstup, který aplikace používá k zařazení do fronty na pozadí pracovní položky.</span><span class="sxs-lookup"><span data-stu-id="14ef6-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
