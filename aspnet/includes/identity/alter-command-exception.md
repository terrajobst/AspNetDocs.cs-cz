---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57796030"
---
> <span data-ttu-id="b9940-101">Některé příkazy nejsou podporovány, pokud aplikace používá jako své úložiště dat Identity SQLite.</span><span class="sxs-lookup"><span data-stu-id="b9940-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="b9940-102">Vzhledem k omezením v databázovém stroji `Alter` příkazy vyvolání následující výjimky:</span><span class="sxs-lookup"><span data-stu-id="b9940-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="b9940-103">"System.NotSupportedException: SQLite nepodporuje tuto operaci migrace."</span><span class="sxs-lookup"><span data-stu-id="b9940-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="b9940-104">Jako alternativní řešení spusťte migrace Code First v databázi, a změnit v tabulkách.</span><span class="sxs-lookup"><span data-stu-id="b9940-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
