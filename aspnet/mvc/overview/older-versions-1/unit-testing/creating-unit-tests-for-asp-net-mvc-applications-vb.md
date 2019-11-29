---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: Vytváření testů jednotek pro aplikace ASP.NET MVC (VB) | Microsoft Docs
author: StephenWalther
description: Naučte se vytvářet testy jednotek pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí Parti...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: 643faddaf6f9cd075131e8e5a9cccb303e355ceb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594694"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a><span data-ttu-id="27139-104">Vytváření testů jednotek pro aplikace ASP.NET MVC (VB)</span><span class="sxs-lookup"><span data-stu-id="27139-104">Creating Unit Tests for ASP.NET MVC Applications (VB)</span></span>

<span data-ttu-id="27139-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="27139-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="27139-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="27139-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> <span data-ttu-id="27139-107">Naučte se vytvářet testy jednotek pro akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="27139-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="27139-108">V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí konkrétní zobrazení, vrátí konkrétní sadu dat nebo vrátí jiný typ výsledku akce.</span><span class="sxs-lookup"><span data-stu-id="27139-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>

<span data-ttu-id="27139-109">Cílem tohoto kurzu je Ukázat, jak můžete napsat testy jednotek pro řadiče v aplikacích ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="27139-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="27139-110">Probereme, jak sestavit tři různé typy testů jednotek.</span><span class="sxs-lookup"><span data-stu-id="27139-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="27139-111">Zjistíte, jak otestovat zobrazení vrácené akcí kontroleru, jak otestovat zobrazení dat vrácených akcí kontroleru a jak otestovat, jestli jedna akce kontroleru vás přesměruje na druhou akci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="27139-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="27139-112">Vytváření kontroleru v rámci testu</span><span class="sxs-lookup"><span data-stu-id="27139-112">Creating the Controller under Test</span></span>

<span data-ttu-id="27139-113">Pojďme začít vytvořením kontroleru, který chcete otestovat.</span><span class="sxs-lookup"><span data-stu-id="27139-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="27139-114">Kontroler s názvem `ProductController`je obsažený v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="27139-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="27139-115">**Výpis 1 – `ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="27139-115">**Listing 1 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

<span data-ttu-id="27139-116">`ProductController` obsahuje dvě metody akcí s názvem `Index()` a `Details()`.</span><span class="sxs-lookup"><span data-stu-id="27139-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="27139-117">Obě metody akcí vrací zobrazení.</span><span class="sxs-lookup"><span data-stu-id="27139-117">Both action methods return a view.</span></span> <span data-ttu-id="27139-118">Všimněte si, že akce `Details()` přijímá parametr s názvem ID.</span><span class="sxs-lookup"><span data-stu-id="27139-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="27139-119">Testování zobrazení vráceného řadičem</span><span class="sxs-lookup"><span data-stu-id="27139-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="27139-120">Představte si, že chceme testovat, zda `ProductController` vrátí pravé zobrazení.</span><span class="sxs-lookup"><span data-stu-id="27139-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="27139-121">Chceme zajistit, aby při vyvolání `ProductController.Details()` akce se zobrazilo zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="27139-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="27139-122">Třída testu v seznamu 2 obsahuje test jednotky pro testování zobrazení vráceného akcí `ProductController.Details()`.</span><span class="sxs-lookup"><span data-stu-id="27139-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="27139-123">**Výpis 2 – `ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="27139-123">**Listing 2 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

<span data-ttu-id="27139-124">Třída v seznamu 2 obsahuje testovací metodu s názvem `TestDetailsView()`.</span><span class="sxs-lookup"><span data-stu-id="27139-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="27139-125">Tato metoda obsahuje tři řádky kódu.</span><span class="sxs-lookup"><span data-stu-id="27139-125">This method contains three lines of code.</span></span> <span data-ttu-id="27139-126">První řádek kódu vytvoří novou instanci třídy `ProductController`.</span><span class="sxs-lookup"><span data-stu-id="27139-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="27139-127">Druhý řádek kódu vyvolá metodu `Details()` akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="27139-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="27139-128">Nakonec poslední řádek kódu ověří, zda zobrazení vrácené akcí `Details()` je zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="27139-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="27139-129">Vlastnost `ViewResult.ViewName` představuje název zobrazení vráceného řadičem.</span><span class="sxs-lookup"><span data-stu-id="27139-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="27139-130">Jedno velké upozornění na testování této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="27139-130">One big warning about testing this property.</span></span> <span data-ttu-id="27139-131">Existují dva způsoby, jak může kontroler vrátit zobrazení.</span><span class="sxs-lookup"><span data-stu-id="27139-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="27139-132">Kontroler může explicitně vrátit zobrazení takto:</span><span class="sxs-lookup"><span data-stu-id="27139-132">A controller can explicitly return a view like this:</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

<span data-ttu-id="27139-133">Případně můžete název zobrazení odvodit z názvu akce řadiče, jako je tato:</span><span class="sxs-lookup"><span data-stu-id="27139-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

<span data-ttu-id="27139-134">Tato akce kontroleru také vrátí zobrazení s názvem `Details`.</span><span class="sxs-lookup"><span data-stu-id="27139-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="27139-135">Název zobrazení je ale odvozený od názvu akce.</span><span class="sxs-lookup"><span data-stu-id="27139-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="27139-136">Chcete-li otestovat název zobrazení, je nutné explicitně vrátit název zobrazení z akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="27139-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="27139-137">Test jednotky můžete spustit v seznamu 2 zadáním kombinace kláves **CTRL-R,** nebo kliknutím na tlačítko **Spustit všechny testy v řešení** (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="27139-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="27139-138">Pokud se test projde, zobrazí se okno Výsledky testů na obrázku 2.</span><span class="sxs-lookup"><span data-stu-id="27139-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>

<span data-ttu-id="27139-139">[![spustit všechny testy v řešení](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="27139-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)</span></span>

<span data-ttu-id="27139-140">**Obrázek 01**: spuštění všech testů v řešení ([kliknutím zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="27139-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))</span></span>

<span data-ttu-id="27139-141">[![úspěch!](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="27139-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)</span></span>

<span data-ttu-id="27139-142">**Obrázek 02**: úspěch!</span><span class="sxs-lookup"><span data-stu-id="27139-142">**Figure 02**: Success!</span></span> <span data-ttu-id="27139-143">([Kliknutím zobrazíte obrázek v plné velikosti.](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="27139-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))</span></span>

## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="27139-144">Testování zobrazení dat vrácených řadičem</span><span class="sxs-lookup"><span data-stu-id="27139-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="27139-145">Kontroler MVC předává data do zobrazení pomocí objektu s názvem *`View Data`* .</span><span class="sxs-lookup"><span data-stu-id="27139-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="27139-146">Představte si například, že chcete zobrazit podrobnosti o konkrétním produktu při vyvolání akce `ProductController Details()`.</span><span class="sxs-lookup"><span data-stu-id="27139-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="27139-147">V takovém případě můžete vytvořit instanci `Product` třídy (definované v modelu) a předat instanci do zobrazení `Details` tím, že využijete `View Data`.</span><span class="sxs-lookup"><span data-stu-id="27139-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="27139-148">Upravený `ProductController` v seznamu 3 obsahuje aktualizovanou `Details()` akci, která vrátí produkt.</span><span class="sxs-lookup"><span data-stu-id="27139-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="27139-149">**Výpis 3 – `ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="27139-149">**Listing 3 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

<span data-ttu-id="27139-150">Nejprve akce `Details()` vytvoří novou instanci třídy `Product`, která představuje přenosný počítač.</span><span class="sxs-lookup"><span data-stu-id="27139-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="27139-151">Dále instance třídy `Product` je předána jako druhý parametr metodě `View()`.</span><span class="sxs-lookup"><span data-stu-id="27139-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="27139-152">Můžete napsat testy jednotek k otestování, zda jsou očekávaná data obsažena v zobrazení dat.</span><span class="sxs-lookup"><span data-stu-id="27139-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="27139-153">Testování částí v seznamu 4 testuje, zda je při volání metody `ProductController Details()` akce vrácen produkt představující přenosný počítač.</span><span class="sxs-lookup"><span data-stu-id="27139-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="27139-154">**Výpis 4 – `ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="27139-154">**Listing 4 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

<span data-ttu-id="27139-155">V výpisu 4 `TestDetailsView()` metoda Testuje data zobrazení vrácená voláním metody `Details()`.</span><span class="sxs-lookup"><span data-stu-id="27139-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="27139-156">`ViewData` je vystavena jako vlastnost `ViewResult` vrácená voláním metody `Details()`.</span><span class="sxs-lookup"><span data-stu-id="27139-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="27139-157">Vlastnost `ViewData.Model` obsahuje produkt předaný do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="27139-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="27139-158">Test jednoduše ověří, že produkt obsažený v zobrazení dat má název přenosného počítače.</span><span class="sxs-lookup"><span data-stu-id="27139-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="27139-159">Testování výsledku akce vráceného řadičem</span><span class="sxs-lookup"><span data-stu-id="27139-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="27139-160">Složitější akce kontroleru může vracet různé typy výsledků akce v závislosti na hodnotách parametrů předaných do akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="27139-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="27139-161">Akce kontroleru může vracet různé typy výsledků akce včetně `ViewResult`, `RedirectToRouteResult`nebo `JsonResult`.</span><span class="sxs-lookup"><span data-stu-id="27139-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="27139-162">Například upravená akce `Details()` v seznamu 5 vrátí zobrazení `Details` při předání platného ID produktu do akce.</span><span class="sxs-lookup"><span data-stu-id="27139-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="27139-163">Pokud předáte neplatné ID produktu – ID s hodnotou menší než 1 –, budete přesměrováni na `Index()` akci.</span><span class="sxs-lookup"><span data-stu-id="27139-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="27139-164">**Výpis 5 – `ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="27139-164">**Listing 5 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

<span data-ttu-id="27139-165">Chování `Details()` akce můžete otestovat pomocí testu jednotek v seznamu 6.</span><span class="sxs-lookup"><span data-stu-id="27139-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="27139-166">Testování částí v seznamu 6 ověřuje, že jste přesměrováni do zobrazení `Index`, když je ID s hodnotou-1 předáno metodě `Details()`.</span><span class="sxs-lookup"><span data-stu-id="27139-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="27139-167">**Výpis 6 – `ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="27139-167">**Listing 6 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

<span data-ttu-id="27139-168">Když zavoláte metodu `RedirectToAction()` v akci kontroleru, akce kontroleru vrátí `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="27139-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="27139-169">Test ověří, zda `RedirectToRouteResult` přesměruje uživatele na akci kontroleru s názvem `Index`.</span><span class="sxs-lookup"><span data-stu-id="27139-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="27139-170">Přehled</span><span class="sxs-lookup"><span data-stu-id="27139-170">Summary</span></span>

<span data-ttu-id="27139-171">V tomto kurzu jste zjistili, jak sestavit testy jednotek pro akce kontroleru MVC.</span><span class="sxs-lookup"><span data-stu-id="27139-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="27139-172">Nejprve jste zjistili, jak ověřit, zda je vráceno správné zobrazení pomocí akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="27139-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="27139-173">Zjistili jste, jak použít vlastnost `ViewResult.ViewName` k ověření názvu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="27139-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="27139-174">Dále jsme zkoumali, jak můžete testovat obsah `View Data`.</span><span class="sxs-lookup"><span data-stu-id="27139-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="27139-175">Zjistili jste, jak ověřit, zda byl po volání akce kontroleru vrácen správný produkt v `View Data`.</span><span class="sxs-lookup"><span data-stu-id="27139-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="27139-176">Nakonec jsme probrali, jak můžete testovat, zda jsou z akce kontroleru vráceny různé typy výsledků akce.</span><span class="sxs-lookup"><span data-stu-id="27139-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="27139-177">Zjistili jste, jak otestovat, zda kontroler vrací `ViewResult` nebo `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="27139-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="27139-178">Předchozí</span><span class="sxs-lookup"><span data-stu-id="27139-178">Previous</span></span>](creating-unit-tests-for-asp-net-mvc-applications-cs.md)
