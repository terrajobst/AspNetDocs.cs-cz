---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 'Část 5: vytvoření dynamického uživatelského rozhraní s vykrojení. js | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600000"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="b150a-102">Část 5: vytvoření dynamického uživatelského rozhraní pomocí vykrojení. js</span><span class="sxs-lookup"><span data-stu-id="b150a-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="b150a-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b150a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b150a-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="b150a-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="b150a-105">Vytvoření dynamického uživatelského rozhraní s knihovnou Knockout.js</span><span class="sxs-lookup"><span data-stu-id="b150a-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="b150a-106">V této části použijeme vyseknutí. js k přidání funkcí do zobrazení správce.</span><span class="sxs-lookup"><span data-stu-id="b150a-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="b150a-107">[Vykrojení. js](http://knockoutjs.com/) je knihovna JavaScriptu, která usnadňuje navázání ovládacích prvků HTML na data.</span><span class="sxs-lookup"><span data-stu-id="b150a-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="b150a-108">Vyseknutí. js používá vzor Model-View-ViewModel (MVVM).</span><span class="sxs-lookup"><span data-stu-id="b150a-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="b150a-109">*Model* je reprezentace dat v obchodní doméně (v našem případě produktů a objednávek) na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="b150a-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="b150a-110">*Zobrazení* je prezentační vrstva (HTML).</span><span class="sxs-lookup"><span data-stu-id="b150a-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="b150a-111">*Model zobrazení* je JavaScriptový objekt, který uchovává data modelu.</span><span class="sxs-lookup"><span data-stu-id="b150a-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="b150a-112">Model zobrazení je abstrakcí kódu uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="b150a-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="b150a-113">Neobsahuje žádné znalosti reprezentace HTML.</span><span class="sxs-lookup"><span data-stu-id="b150a-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="b150a-114">Místo toho představuje abstraktní funkce zobrazení, jako je například seznam položek.</span><span class="sxs-lookup"><span data-stu-id="b150a-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="b150a-115">Zobrazení je vázáno na data na model zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b150a-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="b150a-116">Aktualizace zobrazení – model se automaticky projeví v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b150a-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="b150a-117">Model zobrazení také získává události ze zobrazení, například kliknutí na tlačítko a provádí operace v modelu, například vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="b150a-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="b150a-118">Nejdřív definujeme model zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b150a-118">First we'll define the view-model.</span></span> <span data-ttu-id="b150a-119">Následně navážeme značku HTML na model zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b150a-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="b150a-120">Do správce. cshtml přidejte následující oddíl Razor:</span><span class="sxs-lookup"><span data-stu-id="b150a-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="b150a-121">Tuto část můžete přidat kdekoli v souboru.</span><span class="sxs-lookup"><span data-stu-id="b150a-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="b150a-122">Po vykreslení zobrazení se část zobrazí v dolní části stránky HTML hned před uzavírací &lt;značka&gt;/body.</span><span class="sxs-lookup"><span data-stu-id="b150a-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="b150a-123">Všechny skripty pro tuto stránku se přejdou do značky skriptu označené komentářem:</span><span class="sxs-lookup"><span data-stu-id="b150a-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="b150a-124">Nejprve definujte třídu zobrazení-model:</span><span class="sxs-lookup"><span data-stu-id="b150a-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="b150a-125">**Ko. observableArray** je speciální druh objektu v vykrojení, který se nazývá *pozorovatelný*.</span><span class="sxs-lookup"><span data-stu-id="b150a-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="b150a-126">Z [dokumentace k vyseknutí. js](http://knockoutjs.com/documentation/observables.html): pozorovatelný je objekt JavaScriptu, který může upozornit předplatitele na změny.</span><span class="sxs-lookup"><span data-stu-id="b150a-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="b150a-127">Když je obsah pozorovatelované změny, zobrazení se automaticky aktualizuje tak, aby odpovídalo.</span><span class="sxs-lookup"><span data-stu-id="b150a-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="b150a-128">Chcete-li naplnit `products` pole, proveďte požadavek AJAX na webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="b150a-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="b150a-129">Odvoláme, že jsme uložili základní identifikátor URI pro rozhraní API v kontejneru zobrazení (viz [část 4](using-web-api-with-entity-framework-part-4.md) tohoto kurzu).</span><span class="sxs-lookup"><span data-stu-id="b150a-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="b150a-130">Dále přidejte funkce do zobrazení-model pro vytváření, aktualizaci a odstraňování produktů.</span><span class="sxs-lookup"><span data-stu-id="b150a-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="b150a-131">Tyto funkce odesílají volání AJAX do webového rozhraní API a výsledky se používají k aktualizaci modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b150a-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="b150a-132">Teď nejdůležitější část: když je model DOM plně načtený, zavolejte funkci **Ko. applyBindings** a předejte novou instanci `ProductsViewModel`:</span><span class="sxs-lookup"><span data-stu-id="b150a-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="b150a-133">Metoda **Ko. applyBindings** aktivuje vykrojení a vodiče v zobrazení modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b150a-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="b150a-134">Teď, když máme model zobrazení, můžeme vytvořit vazby.</span><span class="sxs-lookup"><span data-stu-id="b150a-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="b150a-135">V vykrojení. js to provedete přidáním atributů `data-bind` do elementů jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="b150a-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="b150a-136">Chcete-li například svázat seznam HTML s polem, použijte `foreach` vazby:</span><span class="sxs-lookup"><span data-stu-id="b150a-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="b150a-137">Vazba `foreach` projde pole a vytvoří podřízené prvky pro každý objekt v poli.</span><span class="sxs-lookup"><span data-stu-id="b150a-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="b150a-138">Vazby podřízených elementů mohou odkazovat na vlastnosti objektů Array.</span><span class="sxs-lookup"><span data-stu-id="b150a-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="b150a-139">Přidejte následující vazby do seznamu "aktualizace produktů":</span><span class="sxs-lookup"><span data-stu-id="b150a-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="b150a-140">Element `<li>` se vyskytuje v rámci rozsahu vazby **foreach** .</span><span class="sxs-lookup"><span data-stu-id="b150a-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="b150a-141">To znamená, že vykrojení vykreslí prvek jednou pro každý produkt v poli `products`.</span><span class="sxs-lookup"><span data-stu-id="b150a-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="b150a-142">Všechny vazby v rámci elementu `<li>` odkazují na tuto instanci produktu.</span><span class="sxs-lookup"><span data-stu-id="b150a-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="b150a-143">`$data.Name` například odkazuje na vlastnost `Name` v produktu.</span><span class="sxs-lookup"><span data-stu-id="b150a-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="b150a-144">Chcete-li nastavit hodnoty textových vstupů, použijte `value` vazby.</span><span class="sxs-lookup"><span data-stu-id="b150a-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="b150a-145">Tlačítka jsou svázána s funkcemi v zobrazení model pomocí `click` vazby.</span><span class="sxs-lookup"><span data-stu-id="b150a-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="b150a-146">Instance produktu je předána do každé funkce jako parametr.</span><span class="sxs-lookup"><span data-stu-id="b150a-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="b150a-147">Další informace naleznete v [dokumentaci vyseknutí. js](http://knockoutjs.com/documentation/observables.html) s dobrým popisem různých vazeb.</span><span class="sxs-lookup"><span data-stu-id="b150a-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="b150a-148">Dále přidejte vazbu pro událost **odeslání** ve formuláři přidat produkt:</span><span class="sxs-lookup"><span data-stu-id="b150a-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="b150a-149">Tato vazba volá funkci `create` v modelu zobrazení-model pro vytvoření nového produktu.</span><span class="sxs-lookup"><span data-stu-id="b150a-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="b150a-150">Tady je kompletní kód pro zobrazení Správce:</span><span class="sxs-lookup"><span data-stu-id="b150a-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="b150a-151">Spusťte aplikaci, přihlaste se pomocí účtu správce a klikněte na odkaz admin (správce).</span><span class="sxs-lookup"><span data-stu-id="b150a-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="b150a-152">Měl by se zobrazit seznam produktů a může vytvářet, aktualizovat nebo odstraňovat produkty.</span><span class="sxs-lookup"><span data-stu-id="b150a-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b150a-153">[Předchozí](using-web-api-with-entity-framework-part-4.md)
> [Další](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="b150a-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
