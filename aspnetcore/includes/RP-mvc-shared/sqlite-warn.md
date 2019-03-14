---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073108"
---

> [!NOTE]
> EF Core SQLite zprostředkovatel nepodporuje mnoho operací změny schématu. Například přidáním sloupce se podporuje, ale odebráním sloupce se nepodporuje. Pokud chcete odebrat sloupec, je vytvořen migrace `ef migrations add` úspěšný příkaz ale `ef database update` příkaz selže. Některé z těchto omezení je možné překonat ručně napsáním kódu migrace provést opětovné sestavení tabulky. Tabulka opětovné sestavení zahrnuje:

>* Přejmenování existující tabulce.
>* Vytváří se nová tabulka.
>* Kopírování dat z původní tabulky do nové tabulky.
>* Odstranit staré tabulky.

Další informace naleznete v následujících materiálech:
> * [Omezení poskytovatele pro databázi SQLite EF Core](/ef/core/providers/sqlite/limitations)
> * [Přizpůsobení migrace kódu](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [Předvyplnění dat](/ef/core/modeling/data-seeding)