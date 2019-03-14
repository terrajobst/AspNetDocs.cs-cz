---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072868"
---
<span data-ttu-id="d32ce-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Přidejte následující vlastnosti pro `Movie` třídy:</span><span class="sxs-lookup"><span data-stu-id="d32ce-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="d32ce-102">`Movie` Třída obsahuje:</span><span class="sxs-lookup"><span data-stu-id="d32ce-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="d32ce-103">`ID` Pole vyžaduje databázi pro primární klíč.</span><span class="sxs-lookup"><span data-stu-id="d32ce-103">The `ID` field is required by the database for the primary key.</span></span>
* <span data-ttu-id="d32ce-104">`[DataType(DataType.Date)]`:  [Datový typ](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) atribut určuje typ dat (datum).</span><span class="sxs-lookup"><span data-stu-id="d32ce-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date).</span></span> <span data-ttu-id="d32ce-105">Pomocí tohoto atributu:</span><span class="sxs-lookup"><span data-stu-id="d32ce-105">With this attribute:</span></span>

  * <span data-ttu-id="d32ce-106">Uživatel není nutné zadávat informace o čase v poli datum.</span><span class="sxs-lookup"><span data-stu-id="d32ce-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="d32ce-107">Pouze datum je zobrazený, není čas informace.</span><span class="sxs-lookup"><span data-stu-id="d32ce-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="d32ce-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) jsou popsané v pozdějších kurzech.</span><span class="sxs-lookup"><span data-stu-id="d32ce-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>