---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Zobrazit podrobnosti položky | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557321"
---
# <a name="display-item-details"></a>Zobrazení podrobností o položkách

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části přidáte možnost Zobrazit podrobnosti pro každou knihu. V App. js přidejte následující kód do modelu zobrazení:

[!code-javascript[Main](part-8/samples/sample1.js)]

V zobrazeních/Home/index. cshtml přidejte element vázání dat na odkaz Podrobnosti:

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

Tím se naváže obslužná rutina Click pro &lt;&gt; elementu na funkci `getBookDetail` v modelu zobrazení.

Ve stejném souboru nahraďte následující označení:

[!code-html[Main](part-8/samples/sample3.html)]

tímto kódem:

[!code-html[Main](part-8/samples/sample4.html)]

Tento kód vytvoří tabulku, která je vázána na data na vlastnosti `detail` pozorovatelný v modelu zobrazení.

Syntaxe&lt;!--Ko--&gt;&quot; umožňuje zahrnout vazby vykrojení mimo prvek modelu DOM. V tomto případě `if` vazba způsobí, že se tento oddíl označení zobrazí pouze v případě, že `details` není null.

[!code-html[Main](part-8/samples/sample5.html)]

Když teď aplikaci spustíte a kliknete na jednu z &quot;podrobností&quot;ch odkazů, aplikace zobrazí podrobnosti o knize.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [Předchozí](part-7.md)
> [Další](part-9.md)
