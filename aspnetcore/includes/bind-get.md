---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074236"
---
> [!WARNING]
> Z bezpečnostních důvodů musíte výslovný souhlas se vazba `GET` požadovat data na stránce Vlastnosti modelu. Ověření vstupu uživatele před mapování na vlastnosti. K přidání na `GET` vazby je užitečné, když adresování scénáře, které jsou závislé na řetězec nebo trasy hodnoty dotazu.
>
> Vytvořit vazbu vlastnosti `GET` nastavit požadavky [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) atributu `SupportsGet` vlastnost `true`: `[BindProperty(SupportsGet = true)]`
