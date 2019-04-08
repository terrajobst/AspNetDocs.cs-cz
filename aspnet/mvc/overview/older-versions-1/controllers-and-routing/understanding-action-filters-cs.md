---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: Principy filtrů akcí (C#) | Dokumentace Microsoftu
author: microsoft
description: Cílem tohoto kurzu je vysvětlit filtrů akce. Filtr akce je atribut, který můžete použít na akce kontroleru--nebo celý kontroler...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c7706d8252d5a0271f1b9243fa8eb282f722654
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076387"
---
<a name="understanding-action-filters-c"></a><span data-ttu-id="abfde-104">Principy filtrů akcí (C#)</span><span class="sxs-lookup"><span data-stu-id="abfde-104">Understanding Action Filters (C#)</span></span>
====================
<span data-ttu-id="abfde-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="abfde-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="abfde-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="abfde-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="abfde-107">Cílem tohoto kurzu je vysvětlit filtrů akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="abfde-108">Filtr akce je atribut, který můžete použít na akce kontroleru--nebo celý kontroler –, který mění způsob, jakým provedením akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>


## <a name="understanding-action-filters"></a><span data-ttu-id="abfde-109">Principy filtrů akcí</span><span class="sxs-lookup"><span data-stu-id="abfde-109">Understanding Action Filters</span></span>

<span data-ttu-id="abfde-110">Cílem tohoto kurzu je vysvětlit filtrů akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="abfde-111">Filtr akce je atribut, který můžete použít na akce kontroleru--nebo celý kontroler –, který mění způsob, jakým provedením akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="abfde-112">Architektura ASP.NET MVC zahrnuje několik filtrů akce:</span><span class="sxs-lookup"><span data-stu-id="abfde-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="abfde-113">OutputCache – tento filtr akce ukládá do mezipaměti výstupu akce kontroleru pro určenou dobu.</span><span class="sxs-lookup"><span data-stu-id="abfde-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="abfde-114">HandleError – tento filtr akce zpracovává chyby, na které se vyvolá, když se spustí akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="abfde-115">Povolit – tento filtr akce umožňuje omezit přístup na konkrétní uživatele nebo roli.</span><span class="sxs-lookup"><span data-stu-id="abfde-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="abfde-116">Můžete také vytvořit vlastní filtry vlastní akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="abfde-117">Můžete například chtít vytvořit filtr vlastních akcí kvůli implementaci vlastního ověřovacího systému.</span><span class="sxs-lookup"><span data-stu-id="abfde-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="abfde-118">Nebo můžete chtít vytvořit filtr akce, která upravuje zobrazení dat vrácených akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="abfde-119">V tomto kurzu se dozvíte, jak vytvořit filtr akce od základů.</span><span class="sxs-lookup"><span data-stu-id="abfde-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="abfde-120">Vytvoříme protokolu filtru akce, která protokoluje různé fáze zpracování akce v okně Výstup Visual Studia.</span><span class="sxs-lookup"><span data-stu-id="abfde-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="abfde-121">Pomocí filtru akce</span><span class="sxs-lookup"><span data-stu-id="abfde-121">Using an Action Filter</span></span>

<span data-ttu-id="abfde-122">Filtr akce je atribut.</span><span class="sxs-lookup"><span data-stu-id="abfde-122">An action filter is an attribute.</span></span> <span data-ttu-id="abfde-123">Většina filtrů akce můžete použít k akci individuální řadiče nebo celý kontroler.</span><span class="sxs-lookup"><span data-stu-id="abfde-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="abfde-124">Například kontroler dat v informacích 1 zpřístupňuje akci s názvem `Index()` , který vrací aktuální čas.</span><span class="sxs-lookup"><span data-stu-id="abfde-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="abfde-125">Tato akce je doplněn `OutputCache` filtru akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="abfde-126">Tento filtr způsobí, že hodnota vrácená akce, která má být uložené v mezipaměti 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="abfde-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="abfde-127">**Výpis 1 – `Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="abfde-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="abfde-128">Pokud opakovaně vyvoláte `Index()` akce zadáním adresy URL/Data/Index do adresního řádku prohlížeče a při aktualizaci tlačítko více než jednou, zobrazí se stejnou dobu 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="abfde-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="abfde-129">Výstup `Index()` akce se uloží do mezipaměti po dobu 10 sekund (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="abfde-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>


<span data-ttu-id="abfde-130">[![Čas v mezipaměti](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="abfde-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="abfde-131">**Obrázek 01**: V mezipaměti Doba ([kliknutím ji zobrazíte obrázek v plné velikosti](understanding-action-filters-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="abfde-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>


<span data-ttu-id="abfde-132">V jedné akce filtru – výpis 1 `OutputCache` filtr akce – platí pro `Index()` metoda.</span><span class="sxs-lookup"><span data-stu-id="abfde-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="abfde-133">Pokud potřebujete, můžete provést několik filtrů akce u stejné akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="abfde-134">Například můžete chtít použít i `OutputCache` a `HandleError` filtrů Akce na stejnou akci.</span><span class="sxs-lookup"><span data-stu-id="abfde-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="abfde-135">V informacích 1 `OutputCache` filtr akce `Index()` akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="abfde-136">Můžete také použít tento atribut `DataController` třídu.</span><span class="sxs-lookup"><span data-stu-id="abfde-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="abfde-137">V takovém případě výsledek vrácený z jakékoli akce kontroleru vystavené by do mezipaměti 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="abfde-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="abfde-138">Různé typy filtrů</span><span class="sxs-lookup"><span data-stu-id="abfde-138">The Different Types of Filters</span></span>

<span data-ttu-id="abfde-139">Architektura ASP.NET MVC podporuje čtyři typy filtrů:</span><span class="sxs-lookup"><span data-stu-id="abfde-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="abfde-140">Filtry autorizace – implementuje `IAuthorizationFilter` atribut.</span><span class="sxs-lookup"><span data-stu-id="abfde-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="abfde-141">Filtry akcí – implementuje `IActionFilter` atribut.</span><span class="sxs-lookup"><span data-stu-id="abfde-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="abfde-142">Výsledek filtry – implementuje `IResultFilter` atribut.</span><span class="sxs-lookup"><span data-stu-id="abfde-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="abfde-143">Filtry výjimek – implementuje `IExceptionFilter` atribut.</span><span class="sxs-lookup"><span data-stu-id="abfde-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="abfde-144">Filtry jsou spuštěny v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="abfde-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="abfde-145">Například filtry autorizace se vždy spouští se před filtrů Akce a filtry výjimek jsou provedeny vždy po každý jiný typ filtru.</span><span class="sxs-lookup"><span data-stu-id="abfde-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="abfde-146">Filtry autorizace se používají k implementaci ověřování a autorizaci pro akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="abfde-147">Například filtr Authorize je příkladem filtr autorizace.</span><span class="sxs-lookup"><span data-stu-id="abfde-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="abfde-148">Filtry akcí obsahují logiku, která se spustí před a po spuštění akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="abfde-149">Filtr akce, můžete použít například upravit data zobrazení, která vrací akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="abfde-150">Filtry výsledků obsahují logiku, která se spustí před a po zobrazení výsledků spuštění.</span><span class="sxs-lookup"><span data-stu-id="abfde-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="abfde-151">Například můžete chtít změnit zobrazení výsledků klikněte pravým tlačítkem myši předtím, než je zobrazení vykresleno do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="abfde-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="abfde-152">Filtry výjimek jsou poslední typ filtru pro spuštění.</span><span class="sxs-lookup"><span data-stu-id="abfde-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="abfde-153">Zpracování chyb vyvolaných akce kontroleru nebo výsledky akce kontroleru můžete použít filtr výjimek.</span><span class="sxs-lookup"><span data-stu-id="abfde-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="abfde-154">Filtry výjimek můžete použít také k protokolování chyb.</span><span class="sxs-lookup"><span data-stu-id="abfde-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="abfde-155">Každý jiný typ filtru je proveden v určitém pořadí.</span><span class="sxs-lookup"><span data-stu-id="abfde-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="abfde-156">Pokud chcete řídit pořadí provedení filtrů stejného typu můžete nastavit vlastnost pořadí filtru.</span><span class="sxs-lookup"><span data-stu-id="abfde-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="abfde-157">Základní třída pro všechny filtry akce je `System.Web.Mvc.FilterAttribute` třídy.</span><span class="sxs-lookup"><span data-stu-id="abfde-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="abfde-158">Pokud chcete implementovat konkrétní typ filtru, je nutné vytvořit třídu, která dědí ze základní třídy filtr a implementuje jednu nebo více `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, nebo `IExceptionFilter` rozhraní.</span><span class="sxs-lookup"><span data-stu-id="abfde-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="abfde-159">Základní třídy ActionFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="abfde-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="abfde-160">Aby bylo snazší pro vás k implementaci filtr vlastních akcí, rozhraní ASP.NET MVC zahrnuje základní `ActionFilterAttribute` třídy.</span><span class="sxs-lookup"><span data-stu-id="abfde-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="abfde-161">Tato třída implementuje oba `IActionFilter` a `IResultFilter` rozhraní a dědí z `Filter` třídy.</span><span class="sxs-lookup"><span data-stu-id="abfde-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="abfde-162">Terminologie tady není zcela v souladu.</span><span class="sxs-lookup"><span data-stu-id="abfde-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="abfde-163">Technicky je o třídu odvozenou od třídy ActionFilterAttribute filtru akce a výsledku filtru.</span><span class="sxs-lookup"><span data-stu-id="abfde-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="abfde-164">V tom smyslu přijít o provedené, ale filtr akcí aplikace word se používá k odkazování na libovolný typ filtru v rozhraní ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="abfde-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="abfde-165">Základní `ActionFilterAttribute` třída má následující metody, které můžete přepsat:</span><span class="sxs-lookup"><span data-stu-id="abfde-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="abfde-166">OnActionExecuting – tato metoda je volána před provedením akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="abfde-167">OnActionExecuted – tato metoda je volána po provedení akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="abfde-168">OnResultExecuting – tato metoda je volána před provedením výsledku akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="abfde-169">OnResultExecuted – tato metoda je volána po provedení výsledku akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="abfde-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="abfde-170">V další části uvidíme, jak můžete implementovat, každá z těchto různých metod.</span><span class="sxs-lookup"><span data-stu-id="abfde-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="abfde-171">Vytvoření filtru protokolu akcí</span><span class="sxs-lookup"><span data-stu-id="abfde-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="abfde-172">Aby bylo možné ukazují, jak se dají vytvářet filtr vlastních akcí, vytvoříme vlastní akce filtr, který se zaznamená v jednotlivých fázích zpracování akce kontroleru v okně Výstup Visual Studia.</span><span class="sxs-lookup"><span data-stu-id="abfde-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="abfde-173">Naše `LogActionFilter` je obsažen v informacích 2.</span><span class="sxs-lookup"><span data-stu-id="abfde-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="abfde-174">**Výpis 2 – `ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="abfde-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="abfde-175">V informacích 2 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, a `OnResultExecuted()` volání metody `Log()` metody.</span><span class="sxs-lookup"><span data-stu-id="abfde-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="abfde-176">Název metody a aktuální data trasy, která je předána `Log()` metody.</span><span class="sxs-lookup"><span data-stu-id="abfde-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="abfde-177">`Log()` Metoda zapíše zprávu do okna výstup Visual Studia (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="abfde-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>


<span data-ttu-id="abfde-178">[![Zápis v okně Výstup Visual Studia](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="abfde-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="abfde-179">**Obrázek 02**: Zápis v okně Výstup Visual Studia ([kliknutím ji zobrazíte obrázek v plné velikosti](understanding-action-filters-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="abfde-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>


<span data-ttu-id="abfde-180">Kontroler Home v informacích 3 znázorňuje, jak je možné použít filtr protokolu akcí do třídy celý kontroler.</span><span class="sxs-lookup"><span data-stu-id="abfde-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="abfde-181">Vždy, když některou z akcí, které jsou vystavené kontroler Home jsou vyvolány – buď `Index()` metoda nebo `About()` metoda – fáze zpracování akce se Zaprotokolují v okně Výstup Visual Studia.</span><span class="sxs-lookup"><span data-stu-id="abfde-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="abfde-182">**Výpis 3 – `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="abfde-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="abfde-183">Souhrn</span><span class="sxs-lookup"><span data-stu-id="abfde-183">Summary</span></span>

<span data-ttu-id="abfde-184">V tomto kurzu jste se seznámili s ASP.NET MVC filtrů akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="abfde-185">Jste se dozvěděli o čtyři typy filtrů: filtry autorizace, filtry akce, filtry výsledků a filtry výjimek.</span><span class="sxs-lookup"><span data-stu-id="abfde-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="abfde-186">Také jste se naučili o základní `ActionFilterAttribute` třídy.</span><span class="sxs-lookup"><span data-stu-id="abfde-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="abfde-187">Nakonec jste zjistili, jak implementovat jednoduchého filtru akce.</span><span class="sxs-lookup"><span data-stu-id="abfde-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="abfde-188">Vytvořili jsme filtr protokolu akce, která protokoluje v jednotlivých fázích zpracování akce kontroleru v okně Výstup Visual Studia.</span><span class="sxs-lookup"><span data-stu-id="abfde-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="abfde-189">[Předchozí](asp-net-mvc-routing-overview-cs.md)
> [další](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="abfde-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>