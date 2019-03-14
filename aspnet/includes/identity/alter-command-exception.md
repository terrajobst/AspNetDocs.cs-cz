---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57796030"
---
> Některé příkazy nejsou podporovány, pokud aplikace používá jako své úložiště dat Identity SQLite. Vzhledem k omezením v databázovém stroji `Alter` příkazy vyvolání následující výjimky:
>
> "System.NotSupportedException: SQLite nepodporuje tuto operaci migrace." 
>
> Jako alternativní řešení spusťte migrace Code First v databázi, a změnit v tabulkách.
