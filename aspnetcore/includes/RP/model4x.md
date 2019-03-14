---
ms.openlocfilehash: d875717d480fe234ac5a328493fcec6a268e37a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070492"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>Vygenerované uživatelské rozhraní Video modelu

* Spusťte následující příkaz z příkazového řádku (v adresáři projektu, který obsahuje *Program.cs*, *Startup.cs*, a *.csproj* soubory):

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

Pokud dojde k chybě:
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

Otevřete příkazové okno k adresáři projektu (adresář, který obsahuje *Program.cs*, *Startup.cs*, a *.csproj* soubory).
