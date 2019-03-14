---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075607"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a>Úlohy na pozadí ASP.NET Core vzorku (obecný hostitele)

Tento příklad ukazuje použití metody [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice). Tato ukázka demonstruje funkce popsané v [úloh s hostovanými službami v ASP.NET Core na pozadí](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) tématu.

Při spuštění ukázky [Visual Studio Code](https://code.visualstudio.com/), nastavte **konzoly** hodnota konfigurace konzoly v *.vscode/launch.json* buď `externalTerminal` nebo `integratedTerminal`. Použití `internalConsole` není kompatibilní s konzoly stisk klávesy vstup, který aplikace používá k zařazení do fronty na pozadí pracovní položky.
