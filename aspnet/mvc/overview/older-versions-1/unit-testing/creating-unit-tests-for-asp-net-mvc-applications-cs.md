---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: Vytváření testů jednotek pro aplikace ASP.NET MVC (C#) | Microsoft Docs
author: StephenWalther
description: Naučte se vytvářet testy jednotek pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí Parti...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623940"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="5a3e6-104">Vytváření testů jednotek pro aplikace ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="5a3e6-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>

<span data-ttu-id="5a3e6-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="5a3e6-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="5a3e6-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="5a3e6-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="5a3e6-107">Naučte se vytvářet testy jednotek pro akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="5a3e6-108">V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí konkrétní zobrazení, vrátí konkrétní sadu dat nebo vrátí jiný typ výsledku akce.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>

<span data-ttu-id="5a3e6-109">Cílem tohoto kurzu je Ukázat, jak můžete napsat testy jednotek pro řadiče v aplikacích ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="5a3e6-110">Probereme, jak sestavit tři různé typy testů jednotek.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="5a3e6-111">Zjistíte, jak otestovat zobrazení vrácené akcí kontroleru, jak otestovat zobrazení dat vrácených akcí kontroleru a jak otestovat, jestli jedna akce kontroleru vás přesměruje na druhou akci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="5a3e6-112">Vytváření kontroleru v rámci testu</span><span class="sxs-lookup"><span data-stu-id="5a3e6-112">Creating the Controller under Test</span></span>

<span data-ttu-id="5a3e6-113">Pojďme začít vytvořením kontroleru, který chcete otestovat.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="5a3e6-114">Kontroler s názvem `ProductController`je obsažený v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="5a3e6-115">**Výpis 1 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="5a3e6-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="5a3e6-116">`ProductController` obsahuje dvě metody akcí s názvem `Index()` a `Details()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="5a3e6-117">Obě metody akcí vrací zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-117">Both action methods return a view.</span></span> <span data-ttu-id="5a3e6-118">Všimněte si, že akce `Details()` přijímá parametr s názvem ID.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="5a3e6-119">Testování zobrazení vráceného řadičem</span><span class="sxs-lookup"><span data-stu-id="5a3e6-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="5a3e6-120">Představte si, že chceme testovat, zda `ProductController` vrátí pravé zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="5a3e6-121">Chceme zajistit, aby při vyvolání `ProductController.Details()` akce se zobrazilo zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="5a3e6-122">Třída testu v seznamu 2 obsahuje test jednotky pro testování zobrazení vráceného akcí `ProductController.Details()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="5a3e6-123">**Výpis 2 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="5a3e6-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="5a3e6-124">Třída v seznamu 2 obsahuje testovací metodu s názvem `TestDetailsView()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="5a3e6-125">Tato metoda obsahuje tři řádky kódu.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-125">This method contains three lines of code.</span></span> <span data-ttu-id="5a3e6-126">První řádek kódu vytvoří novou instanci třídy `ProductController`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="5a3e6-127">Druhý řádek kódu vyvolá metodu `Details()` akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="5a3e6-128">Nakonec poslední řádek kódu ověří, zda zobrazení vrácené akcí `Details()` je zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="5a3e6-129">Vlastnost `ViewResult.ViewName` představuje název zobrazení vráceného řadičem.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="5a3e6-130">Jedno velké upozornění na testování této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-130">One big warning about testing this property.</span></span> <span data-ttu-id="5a3e6-131">Existují dva způsoby, jak může kontroler vrátit zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="5a3e6-132">Kontroler může explicitně vrátit zobrazení takto:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="5a3e6-133">Případně můžete název zobrazení odvodit z názvu akce řadiče, jako je tato:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="5a3e6-134">Tato akce kontroleru také vrátí zobrazení s názvem `Details`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="5a3e6-135">Název zobrazení je ale odvozený od názvu akce.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="5a3e6-136">Chcete-li otestovat název zobrazení, je nutné explicitně vrátit název zobrazení z akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="5a3e6-137">Test jednotky můžete spustit v seznamu 2 zadáním kombinace kláves **CTRL-R,** nebo kliknutím na tlačítko **Spustit všechny testy v řešení** (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="5a3e6-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="5a3e6-138">Pokud se test projde, zobrazí se okno Výsledky testů na obrázku 2.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>

<span data-ttu-id="5a3e6-139">[![spustit všechny testy v řešení](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5a3e6-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="5a3e6-140">**Obrázek 01**: spuštění všech testů v řešení ([kliknutím zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5a3e6-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>

<span data-ttu-id="5a3e6-141">[![úspěch!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5a3e6-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="5a3e6-142">**Obrázek 02**: úspěch!</span><span class="sxs-lookup"><span data-stu-id="5a3e6-142">**Figure 02**: Success!</span></span> <span data-ttu-id="5a3e6-143">([Kliknutím zobrazíte obrázek v plné velikosti.](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5a3e6-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>

## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="5a3e6-144">Testování zobrazení dat vrácených řadičem</span><span class="sxs-lookup"><span data-stu-id="5a3e6-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="5a3e6-145">Kontroler MVC předává data do zobrazení pomocí objektu s názvem *`View Data`* .</span><span class="sxs-lookup"><span data-stu-id="5a3e6-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="5a3e6-146">Představte si například, že chcete zobrazit podrobnosti o konkrétním produktu při vyvolání akce `ProductController Details()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="5a3e6-147">V takovém případě můžete vytvořit instanci `Product` třídy (definované v modelu) a předat instanci do zobrazení `Details` tím, že využijete `View Data`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="5a3e6-148">Upravený `ProductController` v seznamu 3 obsahuje aktualizovanou `Details()` akci, která vrátí produkt.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="5a3e6-149">**Výpis 3 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="5a3e6-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="5a3e6-150">Nejprve akce `Details()` vytvoří novou instanci třídy `Product`, která představuje přenosný počítač.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="5a3e6-151">Dále instance třídy `Product` je předána jako druhý parametr metodě `View()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="5a3e6-152">Můžete napsat testy jednotek k otestování, zda jsou očekávaná data obsažena v zobrazení dat.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="5a3e6-153">Testování částí v seznamu 4 testuje, zda je při volání metody `ProductController Details()` akce vrácen produkt představující přenosný počítač.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="5a3e6-154">**Výpis 4 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="5a3e6-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="5a3e6-155">V výpisu 4 `TestDetailsView()` metoda Testuje data zobrazení vrácená voláním metody `Details()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="5a3e6-156">`ViewData` je vystavena jako vlastnost `ViewResult` vrácená voláním metody `Details()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="5a3e6-157">Vlastnost `ViewData.Model` obsahuje produkt předaný do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="5a3e6-158">Test jednoduše ověří, že produkt obsažený v zobrazení dat má název přenosného počítače.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="5a3e6-159">Testování výsledku akce vráceného řadičem</span><span class="sxs-lookup"><span data-stu-id="5a3e6-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="5a3e6-160">Složitější akce kontroleru může vracet různé typy výsledků akce v závislosti na hodnotách parametrů předaných do akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="5a3e6-161">Akce kontroleru může vracet různé typy výsledků akce včetně `ViewResult`, `RedirectToRouteResult`nebo `JsonResult`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="5a3e6-162">Například upravená akce `Details()` v seznamu 5 vrátí zobrazení `Details` při předání platného ID produktu do akce.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="5a3e6-163">Pokud předáte neplatné ID produktu – ID s hodnotou menší než 1 –, budete přesměrováni na `Index()` akci.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="5a3e6-164">**Výpis 5 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="5a3e6-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="5a3e6-165">Chování `Details()` akce můžete otestovat pomocí testu jednotek v seznamu 6.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="5a3e6-166">Testování částí v seznamu 6 ověřuje, že jste přesměrováni do zobrazení `Index`, když je ID s hodnotou-1 předáno metodě `Details()`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="5a3e6-167">**Výpis 6 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="5a3e6-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="5a3e6-168">Když zavoláte metodu `RedirectToAction()` v akci kontroleru, akce kontroleru vrátí `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="5a3e6-169">Test ověří, zda `RedirectToRouteResult` přesměruje uživatele na akci kontroleru s názvem `Index`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="5a3e6-170">Souhrn</span><span class="sxs-lookup"><span data-stu-id="5a3e6-170">Summary</span></span>

<span data-ttu-id="5a3e6-171">V tomto kurzu jste zjistili, jak sestavit testy jednotek pro akce kontroleru MVC.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="5a3e6-172">Nejprve jste zjistili, jak ověřit, zda je vráceno správné zobrazení pomocí akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="5a3e6-173">Zjistili jste, jak použít vlastnost `ViewResult.ViewName` k ověření názvu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="5a3e6-174">Dále jsme zkoumali, jak můžete testovat obsah `View Data`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="5a3e6-175">Zjistili jste, jak ověřit, zda byl po volání akce kontroleru vrácen správný produkt v `View Data`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="5a3e6-176">Nakonec jsme probrali, jak můžete testovat, zda jsou z akce kontroleru vráceny různé typy výsledků akce.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="5a3e6-177">Zjistili jste, jak otestovat, zda kontroler vrací `ViewResult` nebo `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5a3e6-178">Next</span><span class="sxs-lookup"><span data-stu-id="5a3e6-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
