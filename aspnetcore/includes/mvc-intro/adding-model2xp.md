---
ms.openlocfilehash: 0084d8c6bc5d16eaa1c3fa36d8aabb2aa31e1283
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067453"
---
<a name="cli"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="532f1-101">Provést počáteční migraci</span><span class="sxs-lookup"><span data-stu-id="532f1-101">Perform initial migration</span></span>

<span data-ttu-id="532f1-102">Z příkazového řádku spusťte následující příkazy rozhraní příkazového řádku .NET Core:</span><span class="sxs-lookup"><span data-stu-id="532f1-102">From the command line, run the following .NET Core CLI commands:</span></span>

```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

<span data-ttu-id="532f1-103">`dotnet ef migrations add InitialCreate` Příkaz vygeneruje kód pro vytvoření schématu počáteční databáze.</span><span class="sxs-lookup"><span data-stu-id="532f1-103">The `dotnet ef migrations add InitialCreate` command generates code to create the initial database schema.</span></span> <span data-ttu-id="532f1-104">Schéma je založen na zadaném v modelu `DbContext` (v *Models/MvcMovieContext.cs* souboru).</span><span class="sxs-lookup"><span data-stu-id="532f1-104">The schema is based on the model specified in the `DbContext` (In the *Models/MvcMovieContext.cs* file).</span></span> <span data-ttu-id="532f1-105">`Initial` Argument se používá k pojmenování migrace.</span><span class="sxs-lookup"><span data-stu-id="532f1-105">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="532f1-106">Můžete použít libovolný název, ale podle konvence zvolte název, který popisuje migraci.</span><span class="sxs-lookup"><span data-stu-id="532f1-106">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="532f1-107">Zobrazit [Úvod do migrace](xref:data/ef-mvc/migrations#introduction-to-migrations) Další informace.</span><span class="sxs-lookup"><span data-stu-id="532f1-107">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="532f1-108">`dotnet ef database update` Příkaz spustí `Up` metodu *migrace /\<časové razítko > _InitialCreate.cs* soubor, který vytvoří databázi.</span><span class="sxs-lookup"><span data-stu-id="532f1-108">The `dotnet ef database update` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file, which creates the database.</span></span>
