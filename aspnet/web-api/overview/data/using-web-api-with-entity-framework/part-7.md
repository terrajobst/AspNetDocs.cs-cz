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
# <a name="create-the-view-ui"></a><span data-ttu-id="971fc-102">Vytvoření zobrazení (uživatelského rozhraní)</span><span class="sxs-lookup"><span data-stu-id="971fc-102">Create the View (UI)</span></span>

<span data-ttu-id="971fc-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="971fc-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="971fc-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="971fc-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="971fc-105">V této části začnete definovat HTML pro aplikaci a přidáte datovou vazbu mezi HTML a model zobrazení.</span><span class="sxs-lookup"><span data-stu-id="971fc-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="971fc-106">Otevřete soubor views/Home/index. cshtml.</span><span class="sxs-lookup"><span data-stu-id="971fc-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="971fc-107">Celý obsah tohoto souboru nahraďte následujícím souborem.</span><span class="sxs-lookup"><span data-stu-id="971fc-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="971fc-108">Většina `div`ch prvků je k dispozici pro styl [bootstrap](http://getbootstrap.com/) .</span><span class="sxs-lookup"><span data-stu-id="971fc-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="971fc-109">Důležité prvky jsou ty s atributy `data-bind`.</span><span class="sxs-lookup"><span data-stu-id="971fc-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="971fc-110">Tento atribut propojuje jazyk HTML s modelem zobrazení.</span><span class="sxs-lookup"><span data-stu-id="971fc-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="971fc-111">Příklad:</span><span class="sxs-lookup"><span data-stu-id="971fc-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="971fc-112">V tomto příkladu &quot;`text`&quot; vazba způsobí, že element `<p>` zobrazí hodnotu vlastnosti `error` z modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="971fc-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="971fc-113">Odvolání tohoto `error` bylo deklarováno jako `ko.observable`:</span><span class="sxs-lookup"><span data-stu-id="971fc-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="971fc-114">Pokaždé, když je nová hodnota přiřazena `error`, vyseknutí aktualizuje text v elementu `<p>`.</span><span class="sxs-lookup"><span data-stu-id="971fc-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="971fc-115">Vazba `foreach` oznamuje vyseknutí k procházení obsahu pole `books`.</span><span class="sxs-lookup"><span data-stu-id="971fc-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="971fc-116">Pro každou položku v poli vytvoří vykrojení nový prvek &lt;li&gt;.</span><span class="sxs-lookup"><span data-stu-id="971fc-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="971fc-117">Vazby v kontextu `foreach` odkazují na vlastnosti položky pole.</span><span class="sxs-lookup"><span data-stu-id="971fc-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="971fc-118">Příklad:</span><span class="sxs-lookup"><span data-stu-id="971fc-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="971fc-119">Zde `text` vazba přečte vlastnost Author každé knihy.</span><span class="sxs-lookup"><span data-stu-id="971fc-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="971fc-120">Pokud aplikaci spustíte nyní, mělo by to vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="971fc-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="971fc-121">Po načtení stránky se seznam knih načte asynchronně.</span><span class="sxs-lookup"><span data-stu-id="971fc-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="971fc-122">V současné době nejsou odkazy &quot;podrobností&quot; funkční.</span><span class="sxs-lookup"><span data-stu-id="971fc-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="971fc-123">Tuto funkci přidáme v další části.</span><span class="sxs-lookup"><span data-stu-id="971fc-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="971fc-124">[Předchozí](part-6.md)
> [Další](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="971fc-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
