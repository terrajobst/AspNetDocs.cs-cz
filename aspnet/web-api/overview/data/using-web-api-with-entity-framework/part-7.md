---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Vytvořit zobrazení (uživatelské rozhraní) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557300"
---
# <a name="create-the-view-ui"></a>Vytvoření zobrazení (uživatelského rozhraní)

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části začnete definovat HTML pro aplikaci a přidáte datovou vazbu mezi HTML a model zobrazení.

Otevřete soubor views/Home/index. cshtml. Celý obsah tohoto souboru nahraďte následujícím souborem.

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

Většina `div`ch prvků je k dispozici pro styl [bootstrap](http://getbootstrap.com/) . Důležité prvky jsou ty s atributy `data-bind`. Tento atribut propojuje jazyk HTML s modelem zobrazení.

Příklad:

[!code-html[Main](part-7/samples/sample2.html)]

V tomto příkladu &quot;`text`&quot; vazba způsobí, že element `<p>` zobrazí hodnotu vlastnosti `error` z modelu zobrazení. Odvolání tohoto `error` bylo deklarováno jako `ko.observable`:

[!code-javascript[Main](part-7/samples/sample3.js)]

Pokaždé, když je nová hodnota přiřazena `error`, vyseknutí aktualizuje text v elementu `<p>`.

Vazba `foreach` oznamuje vyseknutí k procházení obsahu pole `books`. Pro každou položku v poli vytvoří vykrojení nový prvek &lt;li&gt;. Vazby v kontextu `foreach` odkazují na vlastnosti položky pole. Příklad:

[!code-html[Main](part-7/samples/sample4.html)]

Zde `text` vazba přečte vlastnost Author každé knihy.

Pokud aplikaci spustíte nyní, mělo by to vypadat takto:

![](part-7/_static/image1.png)

Po načtení stránky se seznam knih načte asynchronně. V současné době nejsou odkazy &quot;podrobností&quot; funkční. Tuto funkci přidáme v další části.

> [!div class="step-by-step"]
> [Předchozí](part-6.md)
> [Další](part-8.md)
