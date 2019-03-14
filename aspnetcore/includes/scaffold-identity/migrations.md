---
ms.openlocfilehash: 4d6b6309e6e15c364542b5d3ae296d53c6ea4358
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069838"
---
Generovaný kód Identity databáze vyžaduje [migrace Entity Framework Core](/ef/core/managing-schemas/migrations/). Vytvoření migrace a aktualizaci databáze. Například spusťte následující příkazy:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

V sadě Visual Studio **Konzola správce balíčků**:

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[Rozhraní příkazového řádku .NET Core](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

Pro parametr name "CreateIdentitySchema" `Add-Migration` příkaz je volitelný. `"CreateIdentitySchema"` Popisuje migraci.
