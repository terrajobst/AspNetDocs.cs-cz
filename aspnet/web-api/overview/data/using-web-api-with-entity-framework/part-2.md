---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: Přidání modelů a řadičů | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557538"
---
# <a name="add-models-and-controllers"></a>Přidání modelů a kontrolerů

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části přidáte třídy modelů, které definují entity databáze. Pak přidáte řadiče webového rozhraní API, které u těchto entit provádějí operace CRUD.

## <a name="add-model-classes"></a>Přidat třídy modelu

V tomto kurzu vytvoříme databázi pomocí přístupu Code First k Entity Framework (EF). Pomocí Code First zapisujete C# třídy, které odpovídají tabulkám databáze, a EF vytvoří databázi. (Další informace najdete v tématu [Entity Framework vývojové přístupy](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)

Začneme definováním našich doménových objektů jako POCOs (objekty CLR ve starém Old). Vytvoříme následující POCOs:

- Autor
- Book

V Průzkumník řešení klikněte pravým tlačítkem na složku modely. Vyberte **Přidat**a pak vybrat **třídu**. Pojmenujte `Author`třídy.

![](part-2/_static/image1.png)

Nahraďte celý často používaný kód v Author.cs následujícím kódem.

[!code-csharp[Main](part-2/samples/sample1.cs)]

Přidejte další třídu s názvem `Book`s následujícím kódem.

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework použijí tyto modely k vytváření databázových tabulek. U každého modelu se vlastnost `Id` stane sloupcem primárního klíče tabulky databáze.

V třídě Book `AuthorId` definuje cizí klíč do tabulky `Author`. (Pro zjednodušení jsem předpokládáme, že každá kniha má jednoho autora.) Třída Book také obsahuje navigační vlastnost se souvisejícím `Author`. Navigační vlastnost slouží k přístupu k souvisejícímu `Author` v kódu. Vyberu si další informace o navigačních vlastnostech v části 4, [zpracování vztahů mezi entitami](part-4.md).

## <a name="add-web-api-controllers"></a>Přidat řadiče webového rozhraní API

V této části přidáme řadiče webového rozhraní API, které podporují operace CRUD (vytváření, čtení, aktualizace a odstraňování). Řadiče budou používat Entity Framework ke komunikaci s databázovou vrstvou.

Nejprve můžete odstranit soubory Controllers/ValuesController. cs. Tento soubor obsahuje ukázkový kontroler webového rozhraní API, ale pro tento kurz ho nepotřebujete.

![](part-2/_static/image2.png)

V dalším kroku Sestavte projekt. Lešení webového rozhraní API používá reflexi k nalezení tříd modelu, takže potřebuje zkompilované sestavení.

V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat**a pak vybrat **kontroler**.

![](part-2/_static/image3.png)

V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte jako kontroler webové rozhraní API 2 akce pomocí Entity Framework. Klikněte na **Přidat**.

![](part-2/_static/image4.png)

V dialogovém okně **Přidat řadič** proveďte následující:

1. V rozevíracím seznamu **třída modelu** vyberte třídu `Author`. (Pokud ji nevidíte v rozevíracím seznamu, ujistěte se, že jste projekt sestavili.)
2. Podívejte se na použití akcí asynchronního kontroleru.
3. Ponechte název kontroleru &quot;AuthorsController&quot;.
4. Klikněte na tlačítko plus (+) vedle pole **Třída datového kontextu**.

![](part-2/_static/image5.png)

V dialogu **nový kontext dat** ponechte výchozí název a klikněte na **Přidat**.

![](part-2/_static/image6.png)

Kliknutím na tlačítko **Přidat** dokončete dialog **Přidat řadič** . Dialogové okno přidá do projektu dvě třídy:

- `AuthorsController` definuje kontroler webového rozhraní API. Kontroler implementuje REST API, které klienti používají k provádění operací CRUD v seznamu autorů.
- `BookServiceContext` spravuje objekty entit za běhu, což zahrnuje vyplnění objektů daty z databáze, sledování změn a uchování dat v databázi. Dědí z `DbContext`.

![](part-2/_static/image7.png)

V tomto okamžiku Sestavte projekt znovu. Teď Projděte stejný postup, abyste přidali kontroler rozhraní API pro `Book` entit. Tentokrát vyberte `Book` pro třídu modelu a vyberte existující třídu `BookServiceContext` třídy datového kontextu. (Nevytvářet nový kontext dat.) Kliknutím na **Přidat** přidejte kontroler.

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [Předchozí](part-1.md)
> [Další](part-3.md)
