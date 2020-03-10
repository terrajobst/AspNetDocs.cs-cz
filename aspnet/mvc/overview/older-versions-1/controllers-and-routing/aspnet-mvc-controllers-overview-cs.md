---
uid: mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
title: ASP.NET kontroler MVC –C#přehled () | Microsoft Docs
author: StephenWalther
description: V tomto kurzu vás Stephen Walther seznámí s řadiči pro ASP.NET MVC. Naučíte se vytvářet nové řadiče a vracet různé typy zdrojů akcí...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: b985c49a-3668-455c-a366-f85f6bc64b12
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a287b37742400a17c2ed53cfd00bfb053b4f3d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544112"
---
# <a name="aspnet-mvc-controller-overview-c"></a><span data-ttu-id="fe212-104">ASP.NET MVC – přehled kontrolerů (C#)</span><span class="sxs-lookup"><span data-stu-id="fe212-104">ASP.NET MVC Controller Overview (C#)</span></span>

<span data-ttu-id="fe212-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="fe212-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="fe212-106">V tomto kurzu vás Stephen Walther seznámí s řadiči pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fe212-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="fe212-107">Naučíte se vytvářet nové řadiče a vracet různé typy výsledků akcí.</span><span class="sxs-lookup"><span data-stu-id="fe212-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="fe212-108">V tomto kurzu se seznámíte s tématem řadičů ASP.NET MVC, akcemi kontrol a výsledků akcí.</span><span class="sxs-lookup"><span data-stu-id="fe212-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="fe212-109">Po dokončení tohoto kurzu budete rozumět tomu, jak se řadiče používají k řízení způsobu, jakým návštěvník komunikuje s webem ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fe212-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="fe212-110">Principy řadičů</span><span class="sxs-lookup"><span data-stu-id="fe212-110">Understanding Controllers</span></span>

<span data-ttu-id="fe212-111">Řadiče MVC zodpovídají za reakci na požadavky vytvořené na webu ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fe212-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="fe212-112">Každá žádost prohlížeče je namapovaná na konkrétní kontroler.</span><span class="sxs-lookup"><span data-stu-id="fe212-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="fe212-113">Představte si například, že na adresní řádek v prohlížeči zadáte následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="fe212-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="fe212-114">V tomto případě je vyvolán kontroler s názvem ProductController.</span><span class="sxs-lookup"><span data-stu-id="fe212-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="fe212-115">ProductController zodpovídá za generování odpovědi na požadavek prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="fe212-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="fe212-116">Kontroler může například vrátit konkrétní zobrazení zpět do prohlížeče nebo může správce přesměrovat uživatele na jiný kontroler.</span><span class="sxs-lookup"><span data-stu-id="fe212-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="fe212-117">Výpis 1 obsahuje jednoduchý řadič s názvem ProductController.</span><span class="sxs-lookup"><span data-stu-id="fe212-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="fe212-118">**Listing1 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="fe212-118">**Listing1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample1.cs)]

<span data-ttu-id="fe212-119">Jak vidíte z výpisu 1, kontroler je pouze třída (Visual Basic .NET nebo C# třída).</span><span class="sxs-lookup"><span data-stu-id="fe212-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="fe212-120">Kontrolér je třída, která je odvozena od třídy Base System. Web. Mvc. Controller.</span><span class="sxs-lookup"><span data-stu-id="fe212-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="fe212-121">Vzhledem k tomu, že kontroler dědí z této základní třídy, kontroler zdědí několik užitečných metod (v průběhu chvilky probereme tyto metody).</span><span class="sxs-lookup"><span data-stu-id="fe212-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="fe212-122">Principy akcí kontroleru</span><span class="sxs-lookup"><span data-stu-id="fe212-122">Understanding Controller Actions</span></span>

<span data-ttu-id="fe212-123">Kontroler zveřejňuje akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-123">A controller exposes controller actions.</span></span> <span data-ttu-id="fe212-124">Akce je metoda na řadiči, který se volá při zadání konkrétní adresy URL v adresním řádku prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="fe212-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="fe212-125">Představte si například, že vytvoříte požadavek na následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="fe212-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="fe212-126">V tomto případě je metoda index () volána na třídu ProductController.</span><span class="sxs-lookup"><span data-stu-id="fe212-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="fe212-127">Metoda index () je příkladem akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="fe212-128">Akce kontroleru musí být veřejnou metodou třídy Controller.</span><span class="sxs-lookup"><span data-stu-id="fe212-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="fe212-129">C#metody jsou ve výchozím nastavení soukromé metody.</span><span class="sxs-lookup"><span data-stu-id="fe212-129">C# methods, by default, are private methods.</span></span> <span data-ttu-id="fe212-130">Mějte na paměti, že všechny veřejné metody, které přidáte do třídy Controller, se vystaví jako akce kontroleru automaticky (musíte být opatrní, protože akci kontroleru může vyvolat kdokoli v hlavním panelu jednoduše zadáním správné adresy URL do adresního řádku prohlížeče).</span><span class="sxs-lookup"><span data-stu-id="fe212-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="fe212-131">K dispozici jsou některé další požadavky, které musí splnit akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="fe212-132">Metoda použitá jako akce kontroleru nemůže být přetížena.</span><span class="sxs-lookup"><span data-stu-id="fe212-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="fe212-133">Kromě toho nemůže být akce kontroleru statickou metodou.</span><span class="sxs-lookup"><span data-stu-id="fe212-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="fe212-134">Kromě toho můžete jako akci kontroleru použít jenom tuto metodu.</span><span class="sxs-lookup"><span data-stu-id="fe212-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="fe212-135">Porozumění výsledkům akcí</span><span class="sxs-lookup"><span data-stu-id="fe212-135">Understanding Action Results</span></span>

<span data-ttu-id="fe212-136">Akce kontroleru vrátí něco označovaného jako *výsledek akce*.</span><span class="sxs-lookup"><span data-stu-id="fe212-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="fe212-137">Výsledkem akce je to, co se akce kontroleru vrátí v reakci na požadavek prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="fe212-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="fe212-138">Rozhraní ASP.NET MVC podporuje několik typů výsledků akcí, včetně:</span><span class="sxs-lookup"><span data-stu-id="fe212-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="fe212-139">ViewResult – reprezentuje HTML a značky.</span><span class="sxs-lookup"><span data-stu-id="fe212-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="fe212-140">EmptyResult – nepředstavuje žádný výsledek.</span><span class="sxs-lookup"><span data-stu-id="fe212-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="fe212-141">RedirectResult – představuje přesměrování na novou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="fe212-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="fe212-142">JsonResult – představuje výsledek JavaScript Object Notation, který lze použít v aplikaci AJAX.</span><span class="sxs-lookup"><span data-stu-id="fe212-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="fe212-143">JavaScriptResult – představuje skript JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="fe212-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="fe212-144">ContentResult – představuje výsledek textu.</span><span class="sxs-lookup"><span data-stu-id="fe212-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="fe212-145">FileContentResult – představuje soubor ke stažení (s binárním obsahem).</span><span class="sxs-lookup"><span data-stu-id="fe212-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="fe212-146">FilePathResult – představuje soubor ke stažení (s cestou).</span><span class="sxs-lookup"><span data-stu-id="fe212-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="fe212-147">FileStreamResult – představuje soubor ke stažení (s datovým proudem souboru).</span><span class="sxs-lookup"><span data-stu-id="fe212-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="fe212-148">Všechny tyto výsledky akce dědí ze základní třídy ActionResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="fe212-149">Ve většině případů akce kontroleru vrátí ViewResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="fe212-150">Například akce řadiče indexu v seznamu 2 vrátí hodnotu ViewResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="fe212-151">**Výpis 2 – Controllers\BookController.cs**</span><span class="sxs-lookup"><span data-stu-id="fe212-151">**Listing 2 - Controllers\BookController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample2.cs)]

<span data-ttu-id="fe212-152">Když akce vrátí ViewResult, do prohlížeče se vrátí HTML.</span><span class="sxs-lookup"><span data-stu-id="fe212-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="fe212-153">Metoda index () v seznamu 2 vrátí zobrazení s názvem index do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="fe212-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="fe212-154">Všimněte si, že akce index () v seznamu 2 nevrací ViewResult ().</span><span class="sxs-lookup"><span data-stu-id="fe212-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="fe212-155">Místo toho je volána metoda View () základní třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="fe212-156">Za normálních okolností nevrátíte výsledek akce přímo.</span><span class="sxs-lookup"><span data-stu-id="fe212-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="fe212-157">Místo toho zavoláte jednu z následujících metod základní třídy Controller:</span><span class="sxs-lookup"><span data-stu-id="fe212-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="fe212-158">Zobrazit – vrátí výsledek akce ViewResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="fe212-159">Redirect – vrátí výsledek akce RedirectResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="fe212-160">RedirectToAction – vrátí výsledek akce RedirectToRouteResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="fe212-161">Metodu RedirectToRoute – vrátí výsledek akce RedirectToRouteResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="fe212-162">JSON – vrátí výsledek akce JsonResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="fe212-163">JavaScriptResult – vrátí JavaScriptResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="fe212-164">Content – vrátí výsledek ContentResult akce.</span><span class="sxs-lookup"><span data-stu-id="fe212-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="fe212-165">File-vrátí FileContentResult, FilePathResult nebo FileStreamResult v závislosti na parametrech předaných metodě.</span><span class="sxs-lookup"><span data-stu-id="fe212-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="fe212-166">Takže pokud chcete vrátit zobrazení do prohlížeče, zavolejte metodu View ().</span><span class="sxs-lookup"><span data-stu-id="fe212-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="fe212-167">Pokud chcete uživatele přesměrovat z jedné akce kontroleru na jiný, zavoláte metodu RedirectToAction ().</span><span class="sxs-lookup"><span data-stu-id="fe212-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="fe212-168">Například akce podrobnosti () v seznamu 3 buď zobrazí zobrazení nebo přesměruje uživatele na akci index () v závislosti na tom, zda parametr ID má hodnotu.</span><span class="sxs-lookup"><span data-stu-id="fe212-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="fe212-169">**Výpis 3 – CustomerController.cs**</span><span class="sxs-lookup"><span data-stu-id="fe212-169">**Listing 3 - CustomerController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample3.cs)]

<span data-ttu-id="fe212-170">Výsledek akce ContentResult je zvláštní.</span><span class="sxs-lookup"><span data-stu-id="fe212-170">The ContentResult action result is special.</span></span> <span data-ttu-id="fe212-171">Výsledek akce ContentResult můžete použít k vrácení výsledku akce jako prostý text.</span><span class="sxs-lookup"><span data-stu-id="fe212-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="fe212-172">Například metoda index () v seznamu 4 vrátí zprávu jako prostý text a ne jako HTML.</span><span class="sxs-lookup"><span data-stu-id="fe212-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="fe212-173">**Výpis 4 – Controllers\StatusController.cs**</span><span class="sxs-lookup"><span data-stu-id="fe212-173">**Listing 4 - Controllers\StatusController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample4.cs)]

<span data-ttu-id="fe212-174">Při vyvolání akce StatusController. index () se zobrazení nevrátí.</span><span class="sxs-lookup"><span data-stu-id="fe212-174">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="fe212-175">Místo toho je nezpracovaný text "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="fe212-175">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="fe212-176">se vrátí do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="fe212-176">is returned to the browser.</span></span>

<span data-ttu-id="fe212-177">Pokud akce kontroleru vrátí výsledek, který není výsledkem akce – například datum nebo celé číslo, pak je výsledek zabalen do ContentResult automaticky.</span><span class="sxs-lookup"><span data-stu-id="fe212-177">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="fe212-178">Například při vyvolání akce index () WorkController v seznamu 5 se datum vrátí jako ContentResult automaticky.</span><span class="sxs-lookup"><span data-stu-id="fe212-178">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="fe212-179">**Výpis 5 – WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="fe212-179">**Listing 5 - WorkController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample5.cs)]

<span data-ttu-id="fe212-180">Akce index () v výpisu 5 vrátí objekt DateTime.</span><span class="sxs-lookup"><span data-stu-id="fe212-180">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="fe212-181">Rozhraní ASP.NET MVC převede objekt DateTime na řetězec a automaticky zabalí hodnotu DateTime do ContentResult.</span><span class="sxs-lookup"><span data-stu-id="fe212-181">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="fe212-182">Prohlížeč obdrží jako prostý text Datum a čas.</span><span class="sxs-lookup"><span data-stu-id="fe212-182">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="fe212-183">Souhrn</span><span class="sxs-lookup"><span data-stu-id="fe212-183">Summary</span></span>

<span data-ttu-id="fe212-184">Účelem tohoto kurzu je předvést vás koncepty řadičů ASP.NET MVC, akcí kontrol a výsledků akcí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-184">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="fe212-185">V první části jste se dozvěděli, jak přidat nové řadiče do projektu ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="fe212-185">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="fe212-186">V dalším kroku jste zjistili, jak se veřejné metody kontroleru zveřejňují jako akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-186">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="fe212-187">Nakonec jsme probrali různé typy výsledků akcí, které je možné vrátit z akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-187">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="fe212-188">Konkrétně jsme probrali, jak vrátit ViewResult, RedirectToActionResult a ContentResult z akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="fe212-188">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fe212-189">[Předchozí](creating-an-action-vb.md)
> [Další](creating-custom-routes-cs.md)</span><span class="sxs-lookup"><span data-stu-id="fe212-189">[Previous](creating-an-action-vb.md)
[Next](creating-custom-routes-cs.md)</span></span>
