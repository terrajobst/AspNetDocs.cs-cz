---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073108"
---

> [!NOTE]
> <span data-ttu-id="59039-101">EF Core SQLite zprostředkovatel nepodporuje mnoho operací změny schématu.</span><span class="sxs-lookup"><span data-stu-id="59039-101">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="59039-102">Například přidáním sloupce se podporuje, ale odebráním sloupce se nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="59039-102">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="59039-103">Pokud chcete odebrat sloupec, je vytvořen migrace `ef migrations add` úspěšný příkaz ale `ef database update` příkaz selže.</span><span class="sxs-lookup"><span data-stu-id="59039-103">If a migration is created to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="59039-104">Některé z těchto omezení je možné překonat ručně napsáním kódu migrace provést opětovné sestavení tabulky.</span><span class="sxs-lookup"><span data-stu-id="59039-104">Some of these limitations can be overcome by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="59039-105">Tabulka opětovné sestavení zahrnuje:</span><span class="sxs-lookup"><span data-stu-id="59039-105">A table rebuild involves:</span></span>

>* <span data-ttu-id="59039-106">Přejmenování existující tabulce.</span><span class="sxs-lookup"><span data-stu-id="59039-106">Renaming the existing table.</span></span>
>* <span data-ttu-id="59039-107">Vytváří se nová tabulka.</span><span class="sxs-lookup"><span data-stu-id="59039-107">Creating a new table.</span></span>
>* <span data-ttu-id="59039-108">Kopírování dat z původní tabulky do nové tabulky.</span><span class="sxs-lookup"><span data-stu-id="59039-108">Copying data from the old table to the new table.</span></span>
>* <span data-ttu-id="59039-109">Odstranit staré tabulky.</span><span class="sxs-lookup"><span data-stu-id="59039-109">Dropping the old table.</span></span>

<span data-ttu-id="59039-110">Další informace naleznete v následujících materiálech:</span><span class="sxs-lookup"><span data-stu-id="59039-110">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="59039-111">Omezení poskytovatele pro databázi SQLite EF Core</span><span class="sxs-lookup"><span data-stu-id="59039-111">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="59039-112">Přizpůsobení migrace kódu</span><span class="sxs-lookup"><span data-stu-id="59039-112">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="59039-113">Předvyplnění dat</span><span class="sxs-lookup"><span data-stu-id="59039-113">Data seeding</span></span>](/ef/core/modeling/data-seeding)