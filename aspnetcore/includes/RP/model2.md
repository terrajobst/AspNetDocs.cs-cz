---
ms.openlocfilehash: 055a7b0b97f31b2e0e5b36134151a52e9ab45c5c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073252"
---
<a name="dc"></a>
### 

Přidejte následující `RazorPagesMovieContext` třídu *modely* složky:  

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Data/RazorPagesMovieContext.cs)]

Předchozí kód vytvoří `DbSet` vlastnost sady entit. V terminologii Entity Framework obvykle sadu entit odpovídá databázové tabulky a entity odpovídající řádek v tabulce.

<a name="cs"></a>

### <a name="add-a-database-connection-string"></a>Přidat připojovací řetězec databáze

Přidat připojovací řetězec pro *appsettings.json* souboru:

[!code-json[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings_SQLite.json?highlight=8-10)]

### <a name="add-required-nuget-packages"></a>Přidat požadované balíčky NuGet

Spusťte následující příkaz rozhraní příkazového řádku .NET Core pro přidání SQLite a CodeGeneration.Design do projektu:

```console
dotnet add package Microsoft.EntityFrameworkCore.SQLite
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet add package Microsoft.EntityFrameworkCore.Design

```

`Microsoft.VisualStudio.Web.CodeGeneration.Design` Balíčky jsou požadovány pro generování uživatelského rozhraní.

<a name="reg"></a>

### <a name="register-the-database-context"></a>Zaregistrujte kontext databáze

Přidejte následující `using` příkazů v horní části *Startup.cs*:

```csharp
using RazorPagesMovie.Models;
using Microsoft.EntityFrameworkCore;
```

Zaregistrujte kontext databáze s [injektáž závislostí](xref:fundamentals/dependency-injection) kontejneru v `Startup.ConfigureServices`.

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Startup.cs?name=snippet_UseSqlite&highlight=11-12)]

Sestavte projekt jako kontrolu chyb.
