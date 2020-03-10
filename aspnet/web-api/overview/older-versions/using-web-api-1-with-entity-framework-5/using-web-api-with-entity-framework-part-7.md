---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7\. část: vytvoření hlavní stránky | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598677"
---
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="69f6b-102">7\. část: vytvoření hlavní stránky</span><span class="sxs-lookup"><span data-stu-id="69f6b-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="69f6b-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="69f6b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="69f6b-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="69f6b-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="69f6b-105">Vytvoření hlavní stránky</span><span class="sxs-lookup"><span data-stu-id="69f6b-105">Creating the Main Page</span></span>

<span data-ttu-id="69f6b-106">V této části vytvoříte hlavní stránku aplikace.</span><span class="sxs-lookup"><span data-stu-id="69f6b-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="69f6b-107">Tato stránka bude složitější než stránka pro správu, takže se k ní přiblížíme několika kroky.</span><span class="sxs-lookup"><span data-stu-id="69f6b-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="69f6b-108">V takovém případě uvidíte několik pokročilejších technik vyseknutí. js.</span><span class="sxs-lookup"><span data-stu-id="69f6b-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="69f6b-109">Toto je základní rozložení stránky:</span><span class="sxs-lookup"><span data-stu-id="69f6b-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="69f6b-110">"Products" uchovává pole produktů.</span><span class="sxs-lookup"><span data-stu-id="69f6b-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="69f6b-111">"Košík" obsahuje pole produktů s množstvím.</span><span class="sxs-lookup"><span data-stu-id="69f6b-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="69f6b-112">Kliknutím na Přidat do košíku aktualizujete košík.</span><span class="sxs-lookup"><span data-stu-id="69f6b-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="69f6b-113">"Orders" obsahuje pole ID objednávek.</span><span class="sxs-lookup"><span data-stu-id="69f6b-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="69f6b-114">"Details" obsahuje podrobnosti objednávky, což je pole položek (produkty s množstvím).</span><span class="sxs-lookup"><span data-stu-id="69f6b-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="69f6b-115">Začneme definováním základního rozložení ve formátu HTML bez vazby dat nebo skriptu.</span><span class="sxs-lookup"><span data-stu-id="69f6b-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="69f6b-116">Otevřete soubor views/Home/index. cshtml a nahraďte celý obsah následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="69f6b-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="69f6b-117">Dále přidejte oddíl skripty a vytvořte prázdný model zobrazení:</span><span class="sxs-lookup"><span data-stu-id="69f6b-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="69f6b-118">V závislosti na návrhu, který jsme si vyznamenali dříve, náš model zobrazení potřebuje observables pro produkty, košík, objednávky a podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="69f6b-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="69f6b-119">Do objektu `AppViewModel` přidejte následující proměnné:</span><span class="sxs-lookup"><span data-stu-id="69f6b-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="69f6b-120">Uživatelé mohou přidat položky ze seznamu produktů do košíku a odebrat položky z košíku.</span><span class="sxs-lookup"><span data-stu-id="69f6b-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="69f6b-121">Pokud chcete tyto funkce zapouzdřit, vytvoříme další třídu zobrazení-model reprezentující produkt.</span><span class="sxs-lookup"><span data-stu-id="69f6b-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="69f6b-122">Přidejte následující kód pro `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="69f6b-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="69f6b-123">Třída `ProductViewModel` obsahuje dvě funkce, které se používají k přesunu produktu do a ze vozíku: `addItemToCart` na vozík přidá jednu jednotku produktu a `removeAllFromCart` odstraní všechna množství produktu.</span><span class="sxs-lookup"><span data-stu-id="69f6b-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="69f6b-124">Uživatelé můžou vybrat existující objednávku a získat podrobnosti o objednávce.</span><span class="sxs-lookup"><span data-stu-id="69f6b-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="69f6b-125">Tuto funkci zapouzdří do jiného zobrazení – model:</span><span class="sxs-lookup"><span data-stu-id="69f6b-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="69f6b-126">`OrderDetailsViewModel` je inicializována s objednávkou a načítá podrobnosti o objednávce odesláním požadavku AJAX na server.</span><span class="sxs-lookup"><span data-stu-id="69f6b-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="69f6b-127">Všimněte si také, že vlastnost `total` v `OrderDetailsViewModel`.</span><span class="sxs-lookup"><span data-stu-id="69f6b-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="69f6b-128">Tato vlastnost je speciální druh, který je k pozorovateli, který se používá jako [vypočítaná](http://knockoutjs.com/documentation/computedObservables.html).</span><span class="sxs-lookup"><span data-stu-id="69f6b-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="69f6b-129">Jak název implikuje, vypočítaná pozorovatel umožňuje vytvořit datovou vazby k vypočítané hodnotě&#8212;v tomto případě celková cena za objednávku.</span><span class="sxs-lookup"><span data-stu-id="69f6b-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="69f6b-130">Pak přidejte tyto funkce do `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="69f6b-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="69f6b-131">`resetCart` odebere všechny položky z košíku.</span><span class="sxs-lookup"><span data-stu-id="69f6b-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="69f6b-132">`getDetails` Získá podrobnosti o objednávce (vložením nového `OrderDetailsViewModel` do seznamu `details`).</span><span class="sxs-lookup"><span data-stu-id="69f6b-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="69f6b-133">`createOrder` vytvoří nové pořadí a vyprázdní košík.</span><span class="sxs-lookup"><span data-stu-id="69f6b-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="69f6b-134">Nakonec inicializujte model zobrazení tak, že provedete požadavky AJAX na produkty a objednávky:</span><span class="sxs-lookup"><span data-stu-id="69f6b-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="69f6b-135">OK, to je velké množství kódu, ale sestavili jsme ho krok za krokem, takže snad návrh je jasný.</span><span class="sxs-lookup"><span data-stu-id="69f6b-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="69f6b-136">Nyní můžeme do kódu HTML přidat několik vazeb vyseknutí. js.</span><span class="sxs-lookup"><span data-stu-id="69f6b-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="69f6b-137">**Produkty**</span><span class="sxs-lookup"><span data-stu-id="69f6b-137">**Products**</span></span>

<span data-ttu-id="69f6b-138">Tady jsou vazby pro seznam produktů:</span><span class="sxs-lookup"><span data-stu-id="69f6b-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="69f6b-139">Tato iterace přechází přes pole Products a zobrazí název a cenu.</span><span class="sxs-lookup"><span data-stu-id="69f6b-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="69f6b-140">Tlačítko Přidat do objednávky je viditelné pouze v případě, že je uživatel přihlášen.</span><span class="sxs-lookup"><span data-stu-id="69f6b-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="69f6b-141">Tlačítko "Přidat k objednávce" volá `addItemToCart` instance `ProductViewModel` pro daný produkt.</span><span class="sxs-lookup"><span data-stu-id="69f6b-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="69f6b-142">Tím se ukazuje dobrá funkce vyseknutí. js: když model zobrazení obsahuje další modely zobrazení, můžete vazby použít na vnitřní model.</span><span class="sxs-lookup"><span data-stu-id="69f6b-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="69f6b-143">V tomto příkladu jsou vazby v rámci `foreach` aplikovány na každou z `ProductViewModel` instancí.</span><span class="sxs-lookup"><span data-stu-id="69f6b-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="69f6b-144">Tento přístup je mnohem čistší než všechny funkce do jediného modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69f6b-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="69f6b-145">**Nákupního**</span><span class="sxs-lookup"><span data-stu-id="69f6b-145">**Cart**</span></span>

<span data-ttu-id="69f6b-146">Tady jsou vazby pro košík:</span><span class="sxs-lookup"><span data-stu-id="69f6b-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="69f6b-147">Tato iterace prochází přes pole vozíku a zobrazuje název, cenu a množství.</span><span class="sxs-lookup"><span data-stu-id="69f6b-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="69f6b-148">Všimněte si, že odkaz odebrat a tlačítko vytvořit objednávku jsou svázané s funkcemi zobrazení modelu.</span><span class="sxs-lookup"><span data-stu-id="69f6b-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="69f6b-149">**Fakt**</span><span class="sxs-lookup"><span data-stu-id="69f6b-149">**Orders**</span></span>

<span data-ttu-id="69f6b-150">Tady jsou vazby pro seznam objednávky:</span><span class="sxs-lookup"><span data-stu-id="69f6b-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="69f6b-151">Tato iterace projde objednávkami a zobrazí ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="69f6b-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="69f6b-152">Událost Click na odkazu je svázána s funkcí `getDetails`.</span><span class="sxs-lookup"><span data-stu-id="69f6b-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="69f6b-153">**Podrobnosti objednávky**</span><span class="sxs-lookup"><span data-stu-id="69f6b-153">**Order Details**</span></span>

<span data-ttu-id="69f6b-154">Tady jsou vazby pro podrobnosti objednávky:</span><span class="sxs-lookup"><span data-stu-id="69f6b-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="69f6b-155">Tím se prochází nad položkami v objednávce a zobrazuje produkt, cenu a množství.</span><span class="sxs-lookup"><span data-stu-id="69f6b-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="69f6b-156">Okolní div je viditelné pouze v případě, že pole podrobností obsahuje jednu nebo více položek.</span><span class="sxs-lookup"><span data-stu-id="69f6b-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="69f6b-157">Závěr</span><span class="sxs-lookup"><span data-stu-id="69f6b-157">Conclusion</span></span>

<span data-ttu-id="69f6b-158">V tomto kurzu jste vytvořili aplikaci, která používá Entity Framework ke komunikaci s databází a webové rozhraní API ASP.NET k zajištění rozhraní, které se nachází na datové vrstvě jako veřejné.</span><span class="sxs-lookup"><span data-stu-id="69f6b-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="69f6b-159">ASP.NET MVC 4 používáme k vykreslování stránek HTML a vyseknutí. js plus jQuery k poskytnutí dynamické interakce bez nutnosti opětovného načtení stránky.</span><span class="sxs-lookup"><span data-stu-id="69f6b-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="69f6b-160">Další zdroje informací:</span><span class="sxs-lookup"><span data-stu-id="69f6b-160">Additional resources:</span></span>

- [<span data-ttu-id="69f6b-161">Mapa obsahu ASP.NET Data Access</span><span class="sxs-lookup"><span data-stu-id="69f6b-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="69f6b-162">Centrum pro vývojáře Entity Framework</span><span class="sxs-lookup"><span data-stu-id="69f6b-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="69f6b-163">Předchozí</span><span class="sxs-lookup"><span data-stu-id="69f6b-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
