---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Vytvořit objekty Přenos dat (DTO) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445755"
---
# <a name="create-data-transfer-objects-dtos"></a>Vytvoření objektů pro přenos dat (DTO)

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

Teď naše webové rozhraní API zpřístupňuje entity databáze klientovi. Klient obdrží data, která se mapují přímo k tabulkám databáze. To však není vždy dobrý nápad. Někdy budete chtít změnit tvar dat odesílaných klientovi. Můžete například potřebovat:

- Odebrat cyklické odkazy (viz předchozí část).
- Skryjte konkrétní vlastnosti, které klienti nemají zobrazovat.
- Vynechejte některé vlastnosti, aby se snížila velikost datové části.
- Ploché grafy objektů obsahující vnořené objekty, aby byly lépe praktické pro klienty.
- Vyhněte se chybám při "přeúčtování". (Viz [ověření modelu](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) pro diskuzi o převzetí služeb při selhání.)
- Oddělit vrstvu služby od vaší databázové vrstvy.

K tomu můžete definovat *objekt pro přenos dat* (DTO). DTO je objekt, který definuje, jak budou data odesílána přes síť. Pojďme se podívat, jak to funguje s entitou Book. Ve složce modely přidejte dvě třídy DTO:

[!code-csharp[Main](part-5/samples/sample1.cs)]

Třída `BookDetailDto` zahrnuje všechny vlastnosti z modelu knihy, s výjimkou toho, že `AuthorName` je řetězec, který bude obsahovat jméno autora. Třída `BookDto` obsahuje podmnožinu vlastností z `BookDetailDto`.

Dále nahraďte dvě metody GET ve třídě `BooksController`, s verzemi, které vracejí DTO. Použijeme příkaz LINQ **Select** pro převod z entit z knihy na DTO.

[!code-csharp[Main](part-5/samples/sample2.cs)]

Zde je příkaz SQL generovaný novou `GetBooks` metodou. Vidíte, že EF překládá výraz LINQ **Select** do příkazu SQL SELECT.

[!code-sql[Main](part-5/samples/sample3.sql)]

Nakonec upravte metodu `PostBook` tak, aby vracela hodnotu DTO.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> V tomto kurzu převádíme ručně na DTO v kódu. Další možností je použít knihovnu, jako je automatické [mapovače](http://automapper.org/) , která automaticky zpracovává převod.
> 
> [!div class="step-by-step"]
> [Předchozí](part-4.md)
> [Další](part-6.md)
