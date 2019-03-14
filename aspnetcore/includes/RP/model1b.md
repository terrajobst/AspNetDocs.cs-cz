---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072868"
---
<!-- THIS INCLUDE USED BY MVC AND RP --> Přidejte následující vlastnosti pro `Movie` třídy:

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

`Movie` Třída obsahuje:

* `ID` Pole vyžaduje databázi pro primární klíč.
* `[DataType(DataType.Date)]`:  [Datový typ](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) atribut určuje typ dat (datum). Pomocí tohoto atributu:

  * Uživatel není nutné zadávat informace o čase v poli datum.
  * Pouze datum je zobrazený, není čas informace.

[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) jsou popsané v pozdějších kurzech.