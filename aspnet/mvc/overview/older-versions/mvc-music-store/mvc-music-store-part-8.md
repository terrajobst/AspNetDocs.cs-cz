---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 'Část 8: nákupní košík s aktualizacemi AJAX | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 8 pokrývá nákupní košík s aktualizacemi AJAX.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539254"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="af506-104">8\. část: Nákupní košík s aktualizacemi Ajax</span><span class="sxs-lookup"><span data-stu-id="af506-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="af506-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="af506-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="af506-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="af506-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="af506-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="af506-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="af506-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="af506-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="af506-109">Část 8 pokrývá nákupní košík s aktualizacemi AJAX.</span><span class="sxs-lookup"><span data-stu-id="af506-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>

<span data-ttu-id="af506-110">Uživatelům umožníme umístit alba do svého košíku bez registrace, ale budou se muset zaregistrovat jako hosté, aby se dokončila rezervace.</span><span class="sxs-lookup"><span data-stu-id="af506-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="af506-111">Proces nákupu a rezervace se rozdělí na dva řadiče: kontroler ShoppingCart, který umožňuje anonymně přidávat položky na košík a kontroler rezervace, který zpracovává proces rezervace.</span><span class="sxs-lookup"><span data-stu-id="af506-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="af506-112">V této části začneme s nákupním košíkem a pak sestavíme proces registrace v následující části.</span><span class="sxs-lookup"><span data-stu-id="af506-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="af506-113">Přidání tříd modelu košíku, objednávky a OrderDetail</span><span class="sxs-lookup"><span data-stu-id="af506-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="af506-114">Na základě nákupních košíků a procesů rezervace se budou využívat některé nové třídy.</span><span class="sxs-lookup"><span data-stu-id="af506-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="af506-115">Klikněte pravým tlačítkem na složku modely a přidejte třídu košíku (Cart.cs) s následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="af506-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="af506-116">Tato třída je poměrně podobná ostatním, co jsme doposud používali, s výjimkou atributu [key] pro vlastnost RecordId.</span><span class="sxs-lookup"><span data-stu-id="af506-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="af506-117">Položky z košíku budou mít identifikátor řetězce s názvem CartID, který umožní anonymní nákupy, ale tabulka obsahuje primární klíč s názvem RecordId.</span><span class="sxs-lookup"><span data-stu-id="af506-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="af506-118">Podle konvence Entity Framework jako první očekává, že primární klíč pro tabulku s názvem košík bude buď CartId, nebo ID, ale můžeme ho snadno přepsat prostřednictvím poznámek nebo kódu, pokud chceme.</span><span class="sxs-lookup"><span data-stu-id="af506-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="af506-119">Toto je příklad toho, jak můžeme použít jednoduché konvence v Entity Framework kódu jako první, když se na nás líbí, ale neomezujeme je, když ne.</span><span class="sxs-lookup"><span data-stu-id="af506-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="af506-120">Dále přidejte třídu Order (Order.cs) s následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="af506-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="af506-121">Tato třída sleduje informace o souhrnu a doručení pro objednávku.</span><span class="sxs-lookup"><span data-stu-id="af506-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="af506-122">**Ještě nebude zkompilován**, protože má vlastnost navigace OrderDetails, která závisí na třídě, kterou jsme ještě nevytvořili.</span><span class="sxs-lookup"><span data-stu-id="af506-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="af506-123">Pojďme to teď opravit přidáním třídy s názvem OrderDetail.cs a přidáním následujícího kódu.</span><span class="sxs-lookup"><span data-stu-id="af506-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="af506-124">Provedeme jednu poslední aktualizaci třídy MusicStoreEntities, aby zahrnovala DbSets, které zveřejňují tyto nové třídy modelu, včetně Negenerickými&lt;interpretu&gt;.</span><span class="sxs-lookup"><span data-stu-id="af506-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="af506-125">Aktualizovaná třída MusicStoreEntities se zobrazuje níže.</span><span class="sxs-lookup"><span data-stu-id="af506-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="af506-126">Správa obchodní logiky nákupního košíku</span><span class="sxs-lookup"><span data-stu-id="af506-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="af506-127">V dalším kroku vytvoříme třídu ShoppingCart ve složce modely.</span><span class="sxs-lookup"><span data-stu-id="af506-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="af506-128">Model ShoppingCart zpracovává přístup k datům v tabulce košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="af506-129">Kromě toho zpracuje obchodní logiku pro přidání a odebrání položek z nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="af506-130">Vzhledem k tomu, že nechcete vyžadovat, aby se uživatelé k účtu přihlásili pouze za účelem přidání položek do nákupního košíku, přiřadíme uživatelům dočasný jedinečný identifikátor (pomocí identifikátoru GUID nebo globálně jedinečného identifikátoru) při přístupu k nákupnímu košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="af506-131">Toto ID uložíme pomocí třídy ASP.NET session.</span><span class="sxs-lookup"><span data-stu-id="af506-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="af506-132">*Poznámka: relace ASP.NET je vhodným místem pro ukládání informací specifických pro uživatele, jejichž platnost vyprší po opuštění lokality. I když by zneužití stavu relace mohlo mít dopad na výkon na větších lokalitách, používá naše světlo dobře funkční pro demonstrační účely.*</span><span class="sxs-lookup"><span data-stu-id="af506-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="af506-133">Třída ShoppingCart zpřístupňuje následující metody:</span><span class="sxs-lookup"><span data-stu-id="af506-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="af506-134">**AddToCart** převezme album jako parametr a přidá ho do košíku uživatele.</span><span class="sxs-lookup"><span data-stu-id="af506-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="af506-135">Vzhledem k tomu, že tabulka košíku sleduje množství pro každé album, obsahuje logiku pro vytvoření nového řádku, pokud je to potřeba, nebo jenom zvýšit množství, pokud už si uživatel objednal jednu kopii alba.</span><span class="sxs-lookup"><span data-stu-id="af506-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="af506-136">**RemoveFromCart** převezme ID alba a odebere ho z košíku uživatele.</span><span class="sxs-lookup"><span data-stu-id="af506-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="af506-137">Pokud má uživatel ve svém košíku jenom jednu kopii alba, řádek se odebere.</span><span class="sxs-lookup"><span data-stu-id="af506-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="af506-138">**EmptyCart** odebere všechny položky z nákupního košíku uživatele.</span><span class="sxs-lookup"><span data-stu-id="af506-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="af506-139">**GetCartItems** načte seznam CartItems pro zobrazení nebo zpracování.</span><span class="sxs-lookup"><span data-stu-id="af506-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="af506-140">**GetCount** načte celkový počet alb, které má uživatel v rámci svého nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="af506-141">**Gettotal** vypočítá celkové náklady na všechny položky v košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="af506-142">**CreateOrder** převede nákupní košík na objednávku během fáze rezervace.</span><span class="sxs-lookup"><span data-stu-id="af506-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="af506-143">**Getkošík** je statická metoda, která umožňuje našim řadičům získat objekt košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="af506-144">Používá metodu **GetCartId** ke zpracování čtení CartId z uživatelské relace.</span><span class="sxs-lookup"><span data-stu-id="af506-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="af506-145">Metoda GetCartId vyžaduje HttpContextBase, aby mohla číst CartId uživatele z uživatelské relace.</span><span class="sxs-lookup"><span data-stu-id="af506-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="af506-146">Tady je kompletní **Třída ShoppingCart**:</span><span class="sxs-lookup"><span data-stu-id="af506-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="af506-147">ViewModels</span><span class="sxs-lookup"><span data-stu-id="af506-147">ViewModels</span></span>

<span data-ttu-id="af506-148">Náš řadič nákupního košíku bude muset sdělit některé komplexní informace, které se nemapují čistě na naše objekty modelu.</span><span class="sxs-lookup"><span data-stu-id="af506-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="af506-149">Nechceme upravovat naše modely, abychom mohli přizpůsobit naše zobrazení; Třídy modelu by měly představovat naši doménu, nikoli uživatelské rozhraní.</span><span class="sxs-lookup"><span data-stu-id="af506-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="af506-150">Jedním z řešení by bylo předat informace do našich zobrazení pomocí třídy ViewBag, stejně jako v informacích rozevíracího seznamu Správce úložiště, ale předáním velkého množství informací prostřednictvím ViewBag je obtížné spravovat.</span><span class="sxs-lookup"><span data-stu-id="af506-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="af506-151">K tomuto řešení slouží vzor *ViewModel* .</span><span class="sxs-lookup"><span data-stu-id="af506-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="af506-152">Při použití tohoto modelu vytvoříme třídy silného typu, které jsou optimalizované pro naše konkrétní scénáře zobrazení a které zveřejňují vlastnosti pro dynamické hodnoty/obsah, které jsou potřebné pro naše šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af506-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="af506-153">Naše třídy kontroleru pak mohou naplnit a předávat tyto třídy optimalizované pro zobrazení do naší šablony zobrazení, která se má použít.</span><span class="sxs-lookup"><span data-stu-id="af506-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="af506-154">To umožňuje v šablonách zobrazení používat technologii IntelliSense pro ověřování, kontrolu doby kompilace a editory.</span><span class="sxs-lookup"><span data-stu-id="af506-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="af506-155">Vytvoříme dva modely zobrazení pro použití v našem řadiči nákupního košíku: ShoppingCartViewModel bude obsahovat obsah nákupního košíku uživatele a ShoppingCartRemoveViewModel se použije k zobrazení informací o potvrzení, když uživatel nějakou dobu odstraní. z jejich košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="af506-156">Pojďme vytvořit novou složku ViewModels v kořenovém adresáři našeho projektu, abychom zachovali věci uspořádané.</span><span class="sxs-lookup"><span data-stu-id="af506-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="af506-157">Klikněte pravým tlačítkem na projekt, vyberte přidat/nová složka.</span><span class="sxs-lookup"><span data-stu-id="af506-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="af506-158">Pojmenujte složku ViewModels.</span><span class="sxs-lookup"><span data-stu-id="af506-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="af506-159">Dále přidejte třídu ShoppingCartViewModel do složky ViewModels.</span><span class="sxs-lookup"><span data-stu-id="af506-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="af506-160">Má dvě vlastnosti: seznam položek košíku a Desítková hodnota pro uchování celkové ceny pro všechny položky v košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="af506-161">Nyní přidejte ShoppingCartRemoveViewModel do složky ViewModels s následujícími čtyřmi vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="af506-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="af506-162">Řadič nákupního košíku</span><span class="sxs-lookup"><span data-stu-id="af506-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="af506-163">Řadič nákupního košíku má tři hlavní účely: Přidání položek do košíku, odebrání položek z košíku a zobrazení položek na vozíku.</span><span class="sxs-lookup"><span data-stu-id="af506-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="af506-164">Využije tři třídy, které jsme právě vytvořili: ShoppingCartViewModel, ShoppingCartRemoveViewModel a ShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="af506-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="af506-165">Stejně jako v případě StoreController a StoreManagerController přidáme pole pro uložení instance MusicStoreEntities.</span><span class="sxs-lookup"><span data-stu-id="af506-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="af506-166">Přidejte do projektu nový řadič nákupního košíku pomocí prázdné šablony kontroleru.</span><span class="sxs-lookup"><span data-stu-id="af506-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="af506-167">Tady je kompletní kontroler ShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="af506-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="af506-168">Akce index a přidat řadič by měly vypadat velmi dobře.</span><span class="sxs-lookup"><span data-stu-id="af506-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="af506-169">Akce kontroleru odebrat a CartSummary zpracovávají dva zvláštní případy, které probereme v následující části.</span><span class="sxs-lookup"><span data-stu-id="af506-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="af506-170">Aktualizace AJAX pomocí jQuery</span><span class="sxs-lookup"><span data-stu-id="af506-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="af506-171">Dál vytvoříme stránku indexu nákupního košíku, která se silně zapíše do ShoppingCartViewModel a použije šablonu zobrazení seznamu pomocí stejné metody jako předtím.</span><span class="sxs-lookup"><span data-stu-id="af506-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="af506-172">Ale namísto použití HTML. ActionLink k odebrání položek z košíku použijeme jQuery pro všechny odkazy v tomto zobrazení, které mají třídu HTML RemoveLink, na událost Click.</span><span class="sxs-lookup"><span data-stu-id="af506-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="af506-173">Namísto publikování formuláře tato obslužná rutina události Click provede zpětné volání AJAX na naši akci RemoveFromCart Controller.</span><span class="sxs-lookup"><span data-stu-id="af506-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="af506-174">RemoveFromCart vrátí serializovaný výsledek JSON, který naše zpětné volání jQuery analyzuje a provede čtyři rychlé aktualizace stránky pomocí jQuery:</span><span class="sxs-lookup"><span data-stu-id="af506-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="af506-175">Odebere odstraněné album ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="af506-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="af506-176">Aktualizuje počet košíků v hlavičce.</span><span class="sxs-lookup"><span data-stu-id="af506-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="af506-177">Zobrazí zprávu aktualizace pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="af506-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="af506-178">Aktualizuje celkovou cenu za košík.</span><span class="sxs-lookup"><span data-stu-id="af506-178">Updates the cart total price</span></span>

<span data-ttu-id="af506-179">Vzhledem k tomu, že je scénář odebrání zpracováván pomocí zpětného volání AJAX v rámci zobrazení indexu, nepotřebujeme další pohled na RemoveFromCart akci.</span><span class="sxs-lookup"><span data-stu-id="af506-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="af506-180">Zde je kompletní kód pro zobrazení/ShoppingCart/Index:</span><span class="sxs-lookup"><span data-stu-id="af506-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="af506-181">Aby bylo možné tento test provést, musíme do nákupního košíku přidat položky.</span><span class="sxs-lookup"><span data-stu-id="af506-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="af506-182">Naše zobrazení **podrobností o Storu** aktualizujeme tak, aby obsahovalo tlačítko Přidat do košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="af506-183">V tom, že jsme v něm, můžeme přidat další informace o albu, které jsme přidali od poslední aktualizace tohoto zobrazení: Žánr, Interpret, cena a obrázek alba.</span><span class="sxs-lookup"><span data-stu-id="af506-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="af506-184">Aktualizovaný kód zobrazení podrobností úložiště se zobrazí, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="af506-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="af506-185">Nyní můžeme kliknout na obchod a testovat přidávání a odebírání alb z a do nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="af506-186">Spusťte aplikaci a přejděte do indexu úložiště.</span><span class="sxs-lookup"><span data-stu-id="af506-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="af506-187">Potom kliknutím na Žánr zobrazíte seznam alb.</span><span class="sxs-lookup"><span data-stu-id="af506-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="af506-188">Po kliknutí na název alba se teď zobrazí naše aktualizované zobrazení podrobností o albu, včetně tlačítka Přidat do košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="af506-189">Kliknutím na tlačítko Přidat do košíku se zobrazí zobrazení indexu nákupního košíku v seznamu souhrnu nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="af506-190">Po načtení nákupního košíku můžete kliknutím na odkaz odebrat z košíku Zobrazit aktualizaci AJAX do nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="af506-191">Sestavili jsme pracovní nákupní košík, který umožňuje neregistrovaným uživatelům přidávat položky do košíku.</span><span class="sxs-lookup"><span data-stu-id="af506-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="af506-192">V následující části jim umožníme registrovat a dokončit proces registrace.</span><span class="sxs-lookup"><span data-stu-id="af506-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="af506-193">[Předchozí](mvc-music-store-part-7.md)
> [Další](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="af506-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
