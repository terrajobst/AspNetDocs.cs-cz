---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: Přidat novou položku do databáze | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557286"
---
# <a name="add-a-new-item-to-the-database"></a>Přidání nové položky do databáze

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části přidáte uživatelům možnost vytvořit novou knihu. V App. js přidejte následující kód do modelu zobrazení:

[!code-javascript[Main](part-9/samples/sample1.js)]

V indexu. cshtml nahraďte následující kód:

[!code-html[Main](part-9/samples/sample2.html)]

Za:

[!code-html[Main](part-9/samples/sample3.html)]

Tento kód vytvoří formulář pro odeslání nového autora. Hodnoty pro rozevírací seznam autora jsou vázány na data `authors` lze v modelu zobrazení zobrazit jako pozorovatelný. Pro jiné vstupy formuláře jsou hodnoty vázány na data s vlastností `newBook` modelu zobrazení.

Obslužná rutina odeslání ve formuláři je svázána s funkcí `addBook`:

[!code-html[Main](part-9/samples/sample4.html)]

Funkce `addBook` přečte aktuální hodnoty vstupů vázaných na data pro vytvoření objektu JSON. Pak odešle objekt JSON do `/api/books`.

> [!div class="step-by-step"]
> [Předchozí](part-8.md)
> [Další](part-10.md)
