---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074236"
---
> [!WARNING]
> <span data-ttu-id="7a508-101">Z bezpečnostních důvodů musíte výslovný souhlas se vazba `GET` požadovat data na stránce Vlastnosti modelu.</span><span class="sxs-lookup"><span data-stu-id="7a508-101">For security reasons, you must opt in to binding `GET` request data to page model properties.</span></span> <span data-ttu-id="7a508-102">Ověření vstupu uživatele před mapování na vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="7a508-102">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="7a508-103">K přidání na `GET` vazby je užitečné, když adresování scénáře, které jsou závislé na řetězec nebo trasy hodnoty dotazu.</span><span class="sxs-lookup"><span data-stu-id="7a508-103">Opting in to `GET` binding is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="7a508-104">Vytvořit vazbu vlastnosti `GET` nastavit požadavky [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) atributu `SupportsGet` vlastnost `true`: `[BindProperty(SupportsGet = true)]`</span><span class="sxs-lookup"><span data-stu-id="7a508-104">To bind a property on `GET` requests, set the [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>
