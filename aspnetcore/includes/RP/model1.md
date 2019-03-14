---
ms.openlocfilehash: 934db70fe49ba9a5330b25596dc694e0ac50c04e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069994"
---
Podle [Rick Anderson](https://twitter.com/RickAndMSFT)

V této části přidáte třídy pro správu filmy v databázi. Použití těchto tříd s [Entity Framework Core](/ef/core) (EF Core) pro práci s databází. EF Core je objektově relační mapování (ORM) platforma, která zjednodušuje kód přístupu k datům, který musíte napsat.

Tříd modelu, které vytvoříte jsou označovány jako POCO třídy (od "prostý staré CLR objekty"), protože nemají žádné závislosti na EF Core. Definují vlastnosti data, která jsou uložena v databázi.

V tomto kurzu nejprve napsat tříd modelu a EF Core vytvoří databázi. Alternativní není součástí tohoto přístupu je [generování tříd modelu z existující databáze](/ef/core/get-started/aspnetcore/existing-db).

[Zobrazení nebo stažení](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) vzorku.
