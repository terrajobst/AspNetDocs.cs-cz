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
# <a name="display-item-details"></a><span data-ttu-id="03a8e-102">Zobrazení podrobností o položkách</span><span class="sxs-lookup"><span data-stu-id="03a8e-102">Display Item Details</span></span>

<span data-ttu-id="03a8e-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="03a8e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="03a8e-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="03a8e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="03a8e-105">V této části přidáte možnost Zobrazit podrobnosti pro každou knihu.</span><span class="sxs-lookup"><span data-stu-id="03a8e-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="03a8e-106">V App. js přidejte následující kód do modelu zobrazení:</span><span class="sxs-lookup"><span data-stu-id="03a8e-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="03a8e-107">V zobrazeních/Home/index. cshtml přidejte element vázání dat na odkaz Podrobnosti:</span><span class="sxs-lookup"><span data-stu-id="03a8e-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="03a8e-108">Tím se naváže obslužná rutina Click pro &lt;&gt; elementu na funkci `getBookDetail` v modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03a8e-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="03a8e-109">Ve stejném souboru nahraďte následující označení:</span><span class="sxs-lookup"><span data-stu-id="03a8e-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="03a8e-110">tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="03a8e-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="03a8e-111">Tento kód vytvoří tabulku, která je vázána na data na vlastnosti `detail` pozorovatelný v modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03a8e-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="03a8e-112">Syntaxe&lt;!--Ko--&gt;&quot; umožňuje zahrnout vazby vykrojení mimo prvek modelu DOM.</span><span class="sxs-lookup"><span data-stu-id="03a8e-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="03a8e-113">V tomto případě `if` vazba způsobí, že se tento oddíl označení zobrazí pouze v případě, že `details` není null.</span><span class="sxs-lookup"><span data-stu-id="03a8e-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="03a8e-114">Když teď aplikaci spustíte a kliknete na jednu z &quot;podrobností&quot;ch odkazů, aplikace zobrazí podrobnosti o knize.</span><span class="sxs-lookup"><span data-stu-id="03a8e-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="03a8e-115">[Předchozí](part-7.md)
> [Další](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="03a8e-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>
