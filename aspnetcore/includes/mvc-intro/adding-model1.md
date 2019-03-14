---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070291"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="7de2e-101">Přidání modelu pro aplikace ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="7de2e-101">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="7de2e-102">Podle [Rick Anderson](https://twitter.com/RickAndMSFT) a [Petr Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7de2e-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="7de2e-103">V této části přidáte některé třídy pro správu filmy v databázi.</span><span class="sxs-lookup"><span data-stu-id="7de2e-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="7de2e-104">Tyto třídy bude "**M**odelu" součástí **M**VC aplikace.</span><span class="sxs-lookup"><span data-stu-id="7de2e-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="7de2e-105">Použití těchto tříd s [Entity Framework Core](/ef/core) (EF Core) pro práci s databází.</span><span class="sxs-lookup"><span data-stu-id="7de2e-105">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="7de2e-106">EF Core je objektově relační mapování (ORM) platforma, která zjednodušuje kód přístupu k datům, který musíte napsat.</span><span class="sxs-lookup"><span data-stu-id="7de2e-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="7de2e-107">[EF Core podporuje mnoho databázových strojů](/ef/core/providers/).</span><span class="sxs-lookup"><span data-stu-id="7de2e-107">[EF Core supports many database engines](/ef/core/providers/).</span></span>

<span data-ttu-id="7de2e-108">Tříd modelu, které vytvoříte jsou označovány jako POCO třídy (od "prostý staré CLR objekty"), protože nemají žádné závislosti na EF Core.</span><span class="sxs-lookup"><span data-stu-id="7de2e-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="7de2e-109">Právě definují vlastnosti data, která se uloží v databázi.</span><span class="sxs-lookup"><span data-stu-id="7de2e-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="7de2e-110">V tomto kurzu budete psát tříd modelu nejprve a databáze se vytvoří EF Core.</span><span class="sxs-lookup"><span data-stu-id="7de2e-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="7de2e-111">Alternativní není součástí tohoto přístupu je k vytvoření tříd modelu z databáze již existuje.</span><span class="sxs-lookup"><span data-stu-id="7de2e-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="7de2e-112">Informace o tento přístup, najdete v části [ASP.NET Core – existující databáze](/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="7de2e-112">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="7de2e-113">Přidejte třídu modelu dat</span><span class="sxs-lookup"><span data-stu-id="7de2e-113">Add a data model class</span></span>
