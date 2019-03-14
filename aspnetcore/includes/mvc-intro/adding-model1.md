---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070291"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a>Přidání modelu pro aplikace ASP.NET Core MVC

Podle [Rick Anderson](https://twitter.com/RickAndMSFT) a [Petr Dykstra](https://github.com/tdykstra)

V této části přidáte některé třídy pro správu filmy v databázi. Tyto třídy bude "**M**odelu" součástí **M**VC aplikace.

Použití těchto tříd s [Entity Framework Core](/ef/core) (EF Core) pro práci s databází. EF Core je objektově relační mapování (ORM) platforma, která zjednodušuje kód přístupu k datům, který musíte napsat. [EF Core podporuje mnoho databázových strojů](/ef/core/providers/).

Tříd modelu, které vytvoříte jsou označovány jako POCO třídy (od "prostý staré CLR objekty"), protože nemají žádné závislosti na EF Core. Právě definují vlastnosti data, která se uloží v databázi.

V tomto kurzu budete psát tříd modelu nejprve a databáze se vytvoří EF Core. Alternativní není součástí tohoto přístupu je k vytvoření tříd modelu z databáze již existuje. Informace o tento přístup, najdete v části [ASP.NET Core – existující databáze](/ef/core/get-started/aspnetcore/existing-db).

## <a name="add-a-data-model-class"></a>Přidejte třídu modelu dat
