---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: Zobrazit podrobnosti o položkách | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389047"
---
# <a name="display-item-details"></a><span data-ttu-id="7dcfb-102">Zobrazení podrobností o položkách</span><span class="sxs-lookup"><span data-stu-id="7dcfb-102">Display Item Details</span></span>

<span data-ttu-id="7dcfb-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7dcfb-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7dcfb-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="7dcfb-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="7dcfb-105">V této části přidáte možnost, chcete-li zobrazit podrobnosti pro jednotlivé knihy.</span><span class="sxs-lookup"><span data-stu-id="7dcfb-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="7dcfb-106">V app.js přidejte následující kód k zobrazení modelu:</span><span class="sxs-lookup"><span data-stu-id="7dcfb-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="7dcfb-107">V Views/Home/Index.cshtml přidejte odkaz na podrobnosti o prvek svázat data:</span><span class="sxs-lookup"><span data-stu-id="7dcfb-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="7dcfb-108">Tím je vytvořena vazba obslužné rutiny kliknutí pro &lt;&gt; elementu `getBookDetail` funkce na model zobrazení.</span><span class="sxs-lookup"><span data-stu-id="7dcfb-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="7dcfb-109">Ve stejném souboru nahraďte následujícím mark-up:</span><span class="sxs-lookup"><span data-stu-id="7dcfb-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="7dcfb-110">tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="7dcfb-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="7dcfb-111">Tento kód vytvoří tabulku, která je vázán na data vlastnosti `detail` pozorovatelných v modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="7dcfb-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="7dcfb-112">"&lt;!--Ko –&gt; &quot; syntaxe umožňuje zahrnout Knockout vazby mimo prvek modelu DOM.</span><span class="sxs-lookup"><span data-stu-id="7dcfb-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="7dcfb-113">V takovém případě `if` vazby způsobí, že v této části kódu, který se má zobrazit pouze tehdy, když `details` je jiná než null.</span><span class="sxs-lookup"><span data-stu-id="7dcfb-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="7dcfb-114">Když teď spusťte aplikaci a klikněte na některou &quot;podrobností&quot; odkazy, aplikace se zobrazí podrobnosti adresáře.</span><span class="sxs-lookup"><span data-stu-id="7dcfb-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="7dcfb-115">[Předchozí](part-7.md)
> [další](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="7dcfb-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
