---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: Zobrazit datové položky a podrobnosti | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,7 a Microsoft Visual Studio 2017
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641111"
---
# <a name="display-data-items-and-details"></a><span data-ttu-id="d65ea-103">Zobrazení datových položek a podrobností</span><span class="sxs-lookup"><span data-stu-id="d65ea-103">Display data items and details</span></span>

<span data-ttu-id="d65ea-104">od [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="d65ea-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="d65ea-105">V této sérii kurzů se naučíte, jak vytvářet aplikace webových formulářů v ASP.NET pomocí ASP.NET 4,7 a Microsoft Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d65ea-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="d65ea-106">V tomto kurzu se dozvíte, jak zobrazit položky dat a podrobnosti o datových položkách pomocí webových formulářů ASP.NET a Entity Framework Code First.</span><span class="sxs-lookup"><span data-stu-id="d65ea-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="d65ea-107">Tento kurz sestaví na předchozím kurzu "uživatelské rozhraní a navigace" jako součást série kurzů Wingtip Toys.</span><span class="sxs-lookup"><span data-stu-id="d65ea-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="d65ea-108">Po dokončení tohoto kurzu uvidíte produkty na stránce *ProductsList. aspx* a v podrobnostech o produktu na stránce *ProductDetails. aspx* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="d65ea-109">Dozvíte se, jak provést tyto akce:</span><span class="sxs-lookup"><span data-stu-id="d65ea-109">You'll learn how to:</span></span>

- <span data-ttu-id="d65ea-110">Přidání ovládacího prvku data pro zobrazení produktů z databáze</span><span class="sxs-lookup"><span data-stu-id="d65ea-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="d65ea-111">Propojit ovládací prvek dat s vybranými daty</span><span class="sxs-lookup"><span data-stu-id="d65ea-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="d65ea-112">Přidání ovládacího prvku data pro zobrazení podrobností o produktu z databáze</span><span class="sxs-lookup"><span data-stu-id="d65ea-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="d65ea-113">Načte hodnotu z řetězce dotazu a pomocí této hodnoty omezí data načítaná z databáze.</span><span class="sxs-lookup"><span data-stu-id="d65ea-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="d65ea-114">Funkce, které jsou představené v tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="d65ea-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="d65ea-115">Vazby modelu</span><span class="sxs-lookup"><span data-stu-id="d65ea-115">Model binding</span></span>
- <span data-ttu-id="d65ea-116">Zprostředkovatelé hodnot</span><span class="sxs-lookup"><span data-stu-id="d65ea-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="d65ea-117">Přidání ovládacího prvku data</span><span class="sxs-lookup"><span data-stu-id="d65ea-117">Add a data control</span></span>

<span data-ttu-id="d65ea-118">K vytvoření vazby dat na serverový ovládací prvek můžete použít několik různých možností.</span><span class="sxs-lookup"><span data-stu-id="d65ea-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="d65ea-119">Mezi nejběžnější patří:</span><span class="sxs-lookup"><span data-stu-id="d65ea-119">The most common include:</span></span>

* <span data-ttu-id="d65ea-120">Přidání ovládacího prvku zdroje dat</span><span class="sxs-lookup"><span data-stu-id="d65ea-120">Adding a data source control</span></span>
* <span data-ttu-id="d65ea-121">Ruční přidání kódu</span><span class="sxs-lookup"><span data-stu-id="d65ea-121">Adding code by hand</span></span>
* <span data-ttu-id="d65ea-122">Použití vazby modelu</span><span class="sxs-lookup"><span data-stu-id="d65ea-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="d65ea-123">Použití ovládacího prvku zdroje dat pro svázání dat</span><span class="sxs-lookup"><span data-stu-id="d65ea-123">Use a data source control to bind data</span></span>

<span data-ttu-id="d65ea-124">Přidání ovládacího prvku zdroje dat umožňuje propojit ovládací prvek zdroje dat s ovládacím prvkem, který zobrazuje data.</span><span class="sxs-lookup"><span data-stu-id="d65ea-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="d65ea-125">Pomocí tohoto přístupu můžete deklarativně namísto programově propojit serverové ovládací prvky se zdroji dat.</span><span class="sxs-lookup"><span data-stu-id="d65ea-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="d65ea-126">Kódování dat pomocí ručního vytvoření vazby dat</span><span class="sxs-lookup"><span data-stu-id="d65ea-126">Code by hand to bind data</span></span>

<span data-ttu-id="d65ea-127">Kódování podle rukou zahrnuje:</span><span class="sxs-lookup"><span data-stu-id="d65ea-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="d65ea-128">Čtení hodnoty</span><span class="sxs-lookup"><span data-stu-id="d65ea-128">Reading a value</span></span>
2. <span data-ttu-id="d65ea-129">Kontroluje se, jestli je null.</span><span class="sxs-lookup"><span data-stu-id="d65ea-129">Checking if it's null</span></span>
3. <span data-ttu-id="d65ea-130">Převod na odpovídající typ</span><span class="sxs-lookup"><span data-stu-id="d65ea-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="d65ea-131">Kontrola úspěšnosti převodu</span><span class="sxs-lookup"><span data-stu-id="d65ea-131">Checking conversion success</span></span>
5. <span data-ttu-id="d65ea-132">Použití hodnoty v dotazu</span><span class="sxs-lookup"><span data-stu-id="d65ea-132">Using the value in the query</span></span> 

<span data-ttu-id="d65ea-133">Tento přístup vám umožní mít plnou kontrolu nad logikou přístupu k datům.</span><span class="sxs-lookup"><span data-stu-id="d65ea-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="d65ea-134">Použití vazby modelu pro svázání dat</span><span class="sxs-lookup"><span data-stu-id="d65ea-134">Use model binding to bind data</span></span>

<span data-ttu-id="d65ea-135">Vazba modelu umožňuje vytvořit vazbu výsledků s mnohem menším kódem a poskytuje možnost opakovaného použití funkcí v celé aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d65ea-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="d65ea-136">Zjednodušuje práci s logikou přístupu k datům, a přitom stále poskytuje bohatou datovou vazbu na datovou strukturu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="d65ea-137">Zobrazit produkty</span><span class="sxs-lookup"><span data-stu-id="d65ea-137">Display products</span></span>

<span data-ttu-id="d65ea-138">V tomto kurzu použijete vazbu modelu pro svázání dat.</span><span class="sxs-lookup"><span data-stu-id="d65ea-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="d65ea-139">Chcete-li nakonfigurovat ovládací prvek data na použití vazby modelu pro výběr dat, nastavte vlastnost `SelectMethod` ovládacího prvku na název metody v kódu stránky.</span><span class="sxs-lookup"><span data-stu-id="d65ea-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="d65ea-140">Ovládací prvek data volá metodu v příslušnou dobu životního cyklu stránky a automaticky vytvoří vazby vrácených dat.</span><span class="sxs-lookup"><span data-stu-id="d65ea-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="d65ea-141">Není nutné explicitně volat metodu `DataBind`.</span><span class="sxs-lookup"><span data-stu-id="d65ea-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="d65ea-142">V **Průzkumník řešení**otevřete *ProductList. aspx*.</span><span class="sxs-lookup"><span data-stu-id="d65ea-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="d65ea-143">Nahraďte existující kód tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="d65ea-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="d65ea-144">Tento kód používá ovládací prvek **ListView** s názvem `productList` k zobrazení produktů.</span><span class="sxs-lookup"><span data-stu-id="d65ea-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="d65ea-145">Pomocí šablon a stylů definujete způsob, jakým ovládací prvek **ListView** zobrazuje data.</span><span class="sxs-lookup"><span data-stu-id="d65ea-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="d65ea-146">Je vhodný pro data v jakékoli opakující se struktuře.</span><span class="sxs-lookup"><span data-stu-id="d65ea-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="d65ea-147">I když tento příklad **ListView** jednoduše zobrazuje data databáze, můžete také bez kódu povolit uživatelům upravovat, vkládat a odstraňovat data a řadit a stránkovat data.</span><span class="sxs-lookup"><span data-stu-id="d65ea-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="d65ea-148">Nastavením vlastnosti `ItemType` v ovládacím prvku **ListView** je k dispozici výraz datové vazby `Item` a ovládací prvek se zapíše do silného typu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="d65ea-149">Jak je uvedeno v předchozím kurzu, můžete vybrat Podrobnosti objektu položky pomocí technologie IntelliSense, například zadání `ProductName`:</span><span class="sxs-lookup"><span data-stu-id="d65ea-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![Zobrazení datových položek a podrobností – IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="d65ea-151">K určení `SelectMethod` hodnoty používáte také vazbu modelu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="d65ea-152">Tato hodnota (`GetProducts`) odpovídá metodě, kterou přidáte do kódu za účelem zobrazení produktů v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="d65ea-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="d65ea-153">Přidat kód pro zobrazení produktů</span><span class="sxs-lookup"><span data-stu-id="d65ea-153">Add code to display products</span></span>

<span data-ttu-id="d65ea-154">V tomto kroku přidáte kód k naplnění ovládacího prvku **ListView** daty produktu z databáze.</span><span class="sxs-lookup"><span data-stu-id="d65ea-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="d65ea-155">Kód podporuje zobrazování všech produktů a jednotlivých kategorií produktů.</span><span class="sxs-lookup"><span data-stu-id="d65ea-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="d65ea-156">V **Průzkumník řešení**klikněte pravým tlačítkem na *ProductList. aspx* a pak vyberte **Zobrazit kód**.</span><span class="sxs-lookup"><span data-stu-id="d65ea-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="d65ea-157">Nahraďte existující kód v souboru *ProductList.aspx.cs* tímto způsobem:</span><span class="sxs-lookup"><span data-stu-id="d65ea-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="d65ea-158">Tento kód ukazuje metodu `GetProducts`, kterou ovládací prvek **ListView** `ItemType` vlastností na stránce *ProductList. aspx* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="d65ea-159">Chcete-li omezit výsledky na určitou kategorii databáze, kód nastaví `categoryId` hodnotu z hodnoty řetězce dotazu předané na stránku *ProductList. aspx* , když je stránka *ProductList. aspx* přesměrována na.</span><span class="sxs-lookup"><span data-stu-id="d65ea-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="d65ea-160">Třída `QueryStringAttribute` v oboru názvů `System.Web.ModelBinding` slouží k načtení hodnoty proměnné řetězce dotazu `id`.</span><span class="sxs-lookup"><span data-stu-id="d65ea-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="d65ea-161">Tím se dá pokyn k vytvoření vazby modelu k pokusu o vazbu hodnoty z řetězce dotazu k parametru `categoryId` v době běhu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="d65ea-162">Pokud je do stránky předána platná kategorie jako řetězec dotazu, výsledky dotazu jsou omezeny na tyto produkty v databázi, které odpovídají hodnotě `categoryId`.</span><span class="sxs-lookup"><span data-stu-id="d65ea-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="d65ea-163">Pokud je například adresa URL stránky *ProductsList. aspx* následující:</span><span class="sxs-lookup"><span data-stu-id="d65ea-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="d65ea-164">Na stránce se zobrazí pouze produkty, u kterých se `categoryId` rovná `1`.</span><span class="sxs-lookup"><span data-stu-id="d65ea-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="d65ea-165">Pokud je zavolána stránka *ProductList. aspx* , jsou zobrazeny všechny produkty, pokud není zadán řetězec dotazu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="d65ea-166">Zdroje hodnot těchto metod jsou označovány jako *Zprostředkovatelé hodnot* (například *QueryString*) a atributy parametrů, které určují, který zprostředkovatel hodnot použít se označuje jako *atributy zprostředkovatele hodnoty* (například `id`).</span><span class="sxs-lookup"><span data-stu-id="d65ea-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="d65ea-167">ASP.NET zahrnuje zprostředkovatele hodnot a odpovídající atributy pro všechny typické zdroje vstupu uživatele v aplikaci webových formulářů, jako je řetězec dotazu, soubory cookie, hodnoty formulářů, ovládací prvky, stav zobrazení, stav relace a vlastnosti profilu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="d65ea-168">Můžete také napsat vlastní zprostředkovatele hodnot.</span><span class="sxs-lookup"><span data-stu-id="d65ea-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="d65ea-169">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="d65ea-169">Run the application</span></span>

<span data-ttu-id="d65ea-170">Spusťte aplikaci nyní, chcete-li zobrazit všechny produkty nebo produkty kategorie.</span><span class="sxs-lookup"><span data-stu-id="d65ea-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="d65ea-171">Spusťte aplikaci stisknutím klávesy **F5** v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d65ea-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="d65ea-172">Prohlížeč otevře a zobrazí stránku *Default. aspx* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="d65ea-173">V navigační nabídce kategorie produktů vyberte **automobily** .</span><span class="sxs-lookup"><span data-stu-id="d65ea-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="d65ea-174">Zobrazí se stránka *ProductList. aspx* zobrazující pouze produkty kategorie **automobilů** .</span><span class="sxs-lookup"><span data-stu-id="d65ea-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="d65ea-175">Později v tomto kurzu zobrazíte podrobnosti o produktu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-175">Later in this tutorial, you'll display product details.</span></span>  

    ![Zobrazení datových položek a podrobností – automobily](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="d65ea-177">V navigační nabídce v horní části vyberte **produkty** .</span><span class="sxs-lookup"><span data-stu-id="d65ea-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="d65ea-178">Znovu se zobrazí stránka *ProductList. aspx* , tentokrát ale zobrazí celý seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="d65ea-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![Zobrazení datových položek a podrobností – produkty](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="d65ea-180">Zavřete prohlížeč a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d65ea-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="d65ea-181">Přidání ovládacího prvku data pro zobrazení podrobností o produktu</span><span class="sxs-lookup"><span data-stu-id="d65ea-181">Add a data control to display product details</span></span>

<span data-ttu-id="d65ea-182">V dalším kroku upravíte značky na stránce *ProductDetails. aspx* , kterou jste přidali v předchozím kurzu, abyste zobrazili konkrétní informace o produktu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="d65ea-183">V **Průzkumník řešení**otevřete *ProductDetails. aspx*.</span><span class="sxs-lookup"><span data-stu-id="d65ea-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="d65ea-184">Nahraďte existující kód tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="d65ea-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="d65ea-185">Tento kód používá ovládací prvek **FormView** k zobrazení konkrétních podrobností o produktu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="d65ea-186">Tento kód používá metody, jako jsou metody použité k zobrazení dat na stránce *ProductList. aspx* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="d65ea-187">Ovládací prvek **FormView** slouží k zobrazení jednoho záznamu v čase ze zdroje dat.</span><span class="sxs-lookup"><span data-stu-id="d65ea-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="d65ea-188">Při použití ovládacího prvku **FormView** vytvoříte šablony pro zobrazení a úpravy hodnot vázaných na data.</span><span class="sxs-lookup"><span data-stu-id="d65ea-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="d65ea-189">Tyto šablony obsahují ovládací prvky, výrazy vazby a formátování, které definují vzhled a funkce formuláře.</span><span class="sxs-lookup"><span data-stu-id="d65ea-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="d65ea-190">Připojení předchozí značky k databázi vyžaduje další kód.</span><span class="sxs-lookup"><span data-stu-id="d65ea-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="d65ea-191">V **Průzkumník řešení**klikněte pravým tlačítkem na *ProductDetails. aspx* a pak klikněte na **Zobrazit kód**.</span><span class="sxs-lookup"><span data-stu-id="d65ea-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="d65ea-192">Zobrazí se soubor *ProductDetails.aspx.cs* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="d65ea-193">Nahraďte existující kód tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="d65ea-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="d65ea-194">Tento kód kontroluje hodnotu řetězce dotazu "`productID`".</span><span class="sxs-lookup"><span data-stu-id="d65ea-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="d65ea-195">Pokud se najde platná hodnota řetězce dotazu, zobrazí se shodný produkt.</span><span class="sxs-lookup"><span data-stu-id="d65ea-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="d65ea-196">Pokud se řetězec dotazu nenajde nebo jeho hodnota není platná, nezobrazí se žádný produkt.</span><span class="sxs-lookup"><span data-stu-id="d65ea-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="d65ea-197">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="d65ea-197">Run the application</span></span>

<span data-ttu-id="d65ea-198">Nyní můžete spustit aplikaci, abyste viděli jednotlivé produkty zobrazené na základě ID produktu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="d65ea-199">Spusťte aplikaci stisknutím klávesy **F5** v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d65ea-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="d65ea-200">Prohlížeč otevře a zobrazí stránku *Default. aspx* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="d65ea-201">V nabídce navigace v kategorii vyberte **lodě** .</span><span class="sxs-lookup"><span data-stu-id="d65ea-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="d65ea-202">Zobrazí se stránka *ProductList. aspx* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="d65ea-203">Vyberte **papírový člun** ze seznamu produktů.</span><span class="sxs-lookup"><span data-stu-id="d65ea-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="d65ea-204">Zobrazí se stránka *ProductDetails. aspx* .</span><span class="sxs-lookup"><span data-stu-id="d65ea-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![Zobrazení datových položek a podrobností – produkty](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="d65ea-206">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="d65ea-206">Close the browser.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d65ea-207">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="d65ea-207">Additional resources</span></span>

[<span data-ttu-id="d65ea-208">Načítání a zobrazování dat s vazbami modelů a webovými formuláři</span><span class="sxs-lookup"><span data-stu-id="d65ea-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="d65ea-209">Další kroky</span><span class="sxs-lookup"><span data-stu-id="d65ea-209">Next steps</span></span>

<span data-ttu-id="d65ea-210">V tomto kurzu jste přidali značky a kód pro zobrazení produktů a podrobností o produktu.</span><span class="sxs-lookup"><span data-stu-id="d65ea-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="d65ea-211">Seznámili jste se s datovými ovládacími prvky silného typu, vazbou modelů a poskytovateli hodnot.</span><span class="sxs-lookup"><span data-stu-id="d65ea-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="d65ea-212">V dalším kurzu přidáte nákupní košík do ukázkové aplikace Wingtip Toys.</span><span class="sxs-lookup"><span data-stu-id="d65ea-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="d65ea-213">[Předchozí](ui_and_navigation.md)
> [Další](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="d65ea-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
