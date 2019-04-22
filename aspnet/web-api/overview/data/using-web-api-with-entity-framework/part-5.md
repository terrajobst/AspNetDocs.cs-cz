---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Vytvoření objektů pro přenos dat (DTO) | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 1af29955e8040c34840d4c77fc2006f59d2324dd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395274"
---
# <a name="create-data-transfer-objects-dtos"></a>Vytvoření objektů pro přenos dat (DTO)

podle [Mike Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

Pravé teď naše webové rozhraní API zveřejňuje entity databáze do klienta. Klient obdrží data, která mapuje přímo na databázových tabulek. Nicméně, který není vždy vhodné. Někdy budete chtít změnit tvar data, která odesíláte do klienta. Například můžete chtít:

- Odeberte cyklické odkazy (viz předchozí část).
- Skryjte určité vlastnosti, které klienti neměl zobrazit.
- Vynechte některé vlastnosti, aby bylo možné zmenšit velikost datové části.
- Sloučení grafů objektů, které obsahují vnořené objekty, aby se daly vhodnější pro klienty.
- Vyhněte se "over-pass-the účtování" ohrožení zabezpečení. (Viz [ověření modelu](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) diskuzi o navýšení účtování.)
- Oddělte vrstvě služby z vrstvy vaší databáze.

Chcete-li to provést, můžete definovat *objekt pro přenos dat* (DTO). Objekt DTO je objekt, který definuje, jak data se odešlou přes síť. Podívejme se, jak to funguje s entitou knihy. Ve složce modely přidejte dvě DTO třídy:

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDTO` Třída zahrnuje všechny vlastnosti z knihy modelu, s výjimkou, že `AuthorName` je řetězec, který bude obsahovat jméno autora. `BookDTO` Třída obsahuje podmnožinu vlastností z `BookDetailDTO`.

Tyto dvě metody GET v dalším kroku nahraďte `BooksController` třídy s verzemi, které vracejí DTO. Použijeme LINQ **vyberte** příkaz Převést ze seznamu entit na DTO.

[!code-csharp[Main](part-5/samples/sample2.cs)]

Tady je SQL vygeneroval nový `GetBooks` metody. Uvidíte, že překládá EF LINQ **vyberte** do příkazu SQL SELECT.

[!code-sql[Main](part-5/samples/sample3.sql)]

Nakonec upravte `PostBook` metoda vrátí objekt DTO.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> V tomto kurzu převádíme na DTO ručně v kódu. Další možností je použít knihovnu jako [AutoMapper](http://automapper.org/) , která zpracovává server převod automaticky.
> 
> [!div class="step-by-step"]
> [Předchozí](part-4.md)
> [další](part-6.md)
