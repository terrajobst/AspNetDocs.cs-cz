---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: Ověřování pomocí vrstvy služby (C#) | Microsoft Docs
author: StephenWalther
description: Naučte se, jak přesunout logiku ověřování z akcí kontroleru a do samostatné vrstvy služby. V tomto kurzu Stephen Walther vysvětluje, jak vás...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: da1a1c9cc79a452eb0d7597810e86f7bcf6cd179
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542859"
---
# <a name="validating-with-a-service-layer-c"></a><span data-ttu-id="22864-104">Ověřování vrstvou služby (C#)</span><span class="sxs-lookup"><span data-stu-id="22864-104">Validating with a Service Layer (C#)</span></span>

<span data-ttu-id="22864-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="22864-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="22864-106">Naučte se, jak přesunout logiku ověřování z akcí kontroleru a do samostatné vrstvy služby.</span><span class="sxs-lookup"><span data-stu-id="22864-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="22864-107">V tomto kurzu Stephen Walther vysvětluje, jak můžete udržovat ostré oddělení potíží tím, že izolujete vrstvu služby od vrstvy řadiče.</span><span class="sxs-lookup"><span data-stu-id="22864-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>

<span data-ttu-id="22864-108">Cílem tohoto kurzu je popsat jednu metodu provádění ověřování v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="22864-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="22864-109">V tomto kurzu se naučíte přesunout logiku ověřování z vašich řadičů a do samostatné vrstvy služby.</span><span class="sxs-lookup"><span data-stu-id="22864-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="22864-110">Oddělení obav</span><span class="sxs-lookup"><span data-stu-id="22864-110">Separating Concerns</span></span>

<span data-ttu-id="22864-111">Při sestavování aplikace ASP.NET MVC byste neměli umístit logiku databáze do akcí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22864-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="22864-112">Kombinování databáze a logiky kontroleru usnadňuje údržbu vaší aplikace v průběhu času.</span><span class="sxs-lookup"><span data-stu-id="22864-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="22864-113">Doporučení je, abyste všechny své databázové logiky umístili do samostatné vrstvy úložiště.</span><span class="sxs-lookup"><span data-stu-id="22864-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="22864-114">Například výpis 1 obsahuje jednoduché úložiště s názvem ProductRepository.</span><span class="sxs-lookup"><span data-stu-id="22864-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="22864-115">Úložiště produktu obsahuje veškerý kód pro přístup k datům pro aplikaci.</span><span class="sxs-lookup"><span data-stu-id="22864-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="22864-116">Výpis zahrnuje také rozhraní IProductRepository, které implementuje úložiště produktu.</span><span class="sxs-lookup"><span data-stu-id="22864-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="22864-117">**Výpis 1 – Models\ProductRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="22864-117">**Listing 1 -- Models\ProductRepository.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

<span data-ttu-id="22864-118">Kontroler v seznamu 2 používá vrstvu úložiště v akcích index () a Create ().</span><span class="sxs-lookup"><span data-stu-id="22864-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="22864-119">Všimněte si, že tento kontroler neobsahuje žádnou databázovou logiku.</span><span class="sxs-lookup"><span data-stu-id="22864-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="22864-120">Vytvoření vrstvy úložiště vám umožní udržovat čisté oddělení obav.</span><span class="sxs-lookup"><span data-stu-id="22864-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="22864-121">Řadiče jsou zodpovědné za logiku řízení toku aplikace a úložiště zodpovídá za logiku přístupu k datům.</span><span class="sxs-lookup"><span data-stu-id="22864-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="22864-122">**Výpis 2 – Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="22864-122">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="22864-123">Vytvoření vrstvy služby</span><span class="sxs-lookup"><span data-stu-id="22864-123">Creating a Service Layer</span></span>

<span data-ttu-id="22864-124">Takže logika řízení toku aplikace patří do řadiče a logika přístupu k datům patří do úložiště.</span><span class="sxs-lookup"><span data-stu-id="22864-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="22864-125">V takovém případě, kam umístíte logiku ověřování?</span><span class="sxs-lookup"><span data-stu-id="22864-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="22864-126">Jednou z možností je umístit logiku ověřování ve *vrstvě služeb*.</span><span class="sxs-lookup"><span data-stu-id="22864-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="22864-127">Vrstva služeb je další vrstva v aplikaci ASP.NET MVC, která řeší komunikaci mezi řadičem a vrstvou úložiště.</span><span class="sxs-lookup"><span data-stu-id="22864-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="22864-128">Vrstva služby obsahuje obchodní logiku.</span><span class="sxs-lookup"><span data-stu-id="22864-128">The service layer contains business logic.</span></span> <span data-ttu-id="22864-129">Konkrétně obsahuje logiku ověřování.</span><span class="sxs-lookup"><span data-stu-id="22864-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="22864-130">Například vrstva produktové služby v seznamu 3 má metodu CreateProduct ().</span><span class="sxs-lookup"><span data-stu-id="22864-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="22864-131">Metoda CreateProduct () volá metodu ValidateProduct () pro ověření nového produktu před předáním produktu do úložiště produktu.</span><span class="sxs-lookup"><span data-stu-id="22864-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="22864-132">**Výpis 3 – Models\ProductService.cs**</span><span class="sxs-lookup"><span data-stu-id="22864-132">**Listing 3 - Models\ProductService.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

<span data-ttu-id="22864-133">V seznamu 4 byl aktualizován produkt, aby místo vrstvy úložiště používal vrstvu služby.</span><span class="sxs-lookup"><span data-stu-id="22864-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="22864-134">Vrstva kontroleru mluví do vrstvy služeb.</span><span class="sxs-lookup"><span data-stu-id="22864-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="22864-135">Vrstva služby mluví s vrstvou úložiště.</span><span class="sxs-lookup"><span data-stu-id="22864-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="22864-136">Každá vrstva má samostatnou zodpovědnost.</span><span class="sxs-lookup"><span data-stu-id="22864-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="22864-137">**Výpis 4 – Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="22864-137">**Listing 4 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

<span data-ttu-id="22864-138">Všimněte si, že Produktová služba je vytvořena v konstruktoru produktového kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22864-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="22864-139">Po vytvoření produktové služby je slovník stavu modelu předán službě.</span><span class="sxs-lookup"><span data-stu-id="22864-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="22864-140">Produktová služba používá stav modelu k předání chybových zpráv ověřování zpět do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22864-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="22864-141">Oddělení vrstvy služby</span><span class="sxs-lookup"><span data-stu-id="22864-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="22864-142">Nepovedlo se nám izolovat řadiče a vrstvy služeb v jednom ohledu.</span><span class="sxs-lookup"><span data-stu-id="22864-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="22864-143">Vrstva řadiče a služeb komunikuje přes stav modelu.</span><span class="sxs-lookup"><span data-stu-id="22864-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="22864-144">Jinými slovy, vrstva služby má závislost na konkrétní funkci architektury ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="22864-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="22864-145">Doporučujeme izolovat vrstvu služby z naší vrstvy řadiče co nejvíce.</span><span class="sxs-lookup"><span data-stu-id="22864-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="22864-146">Teoreticky byste měli být schopni používat vrstvu služby s jakýmkoli typem aplikace, a ne pouze aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="22864-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="22864-147">V budoucnu můžeme například pro naši aplikaci vytvořit front-end pro WPF.</span><span class="sxs-lookup"><span data-stu-id="22864-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="22864-148">Měli bychom najít způsob, jak z naší vrstvy služby odebrat závislost na stav modelu ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="22864-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="22864-149">V seznamu 5 se vrstva služby aktualizovala tak, aby už nepoužívala stav modelu.</span><span class="sxs-lookup"><span data-stu-id="22864-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="22864-150">Místo toho používá libovolnou třídu, která implementuje rozhraní IValidationDictionary.</span><span class="sxs-lookup"><span data-stu-id="22864-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="22864-151">**Výpis 5-Models\ProductService.cs (oddělené)**</span><span class="sxs-lookup"><span data-stu-id="22864-151">**Listing 5 - Models\ProductService.cs (decoupled)**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

<span data-ttu-id="22864-152">Rozhraní IValidationDictionary je definováno v výpisu 6.</span><span class="sxs-lookup"><span data-stu-id="22864-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="22864-153">Toto jednoduché rozhraní má jedinou metodu a jedinou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="22864-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="22864-154">**Výpis 6 – Models\IValidationDictionary.cs**</span><span class="sxs-lookup"><span data-stu-id="22864-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

<span data-ttu-id="22864-155">Třída v seznamu 7 s názvem třídy ModelStateWrapper implementuje rozhraní IValidationDictionary.</span><span class="sxs-lookup"><span data-stu-id="22864-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="22864-156">Můžete vytvořit instanci třídy ModelStateWrapper předáním slovníku stavu modelu do konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="22864-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="22864-157">**Výpis 7 – Models\ModelStateWrapper.cs**</span><span class="sxs-lookup"><span data-stu-id="22864-157">**Listing 7 - Models\ModelStateWrapper.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

<span data-ttu-id="22864-158">Nakonec aktualizovaný kontroler v seznamu 8 používá ModelStateWrapper při vytváření vrstvy služby ve svém konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="22864-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="22864-159">**Výpis 8 – Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="22864-159">**Listing 8 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

<span data-ttu-id="22864-160">Použití rozhraní IValidationDictionary a třídy ModelStateWrapper nám umožňuje zcela izolovat naši vrstvu služeb od naší vrstvy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22864-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="22864-161">Vrstva služby již není závislá na stavu modelu.</span><span class="sxs-lookup"><span data-stu-id="22864-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="22864-162">Můžete předat libovolnou třídu, která implementuje rozhraní IValidationDictionary, do vrstvy služby.</span><span class="sxs-lookup"><span data-stu-id="22864-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="22864-163">Například aplikace WPF může implementovat rozhraní IValidationDictionary s jednoduchou třídou kolekce.</span><span class="sxs-lookup"><span data-stu-id="22864-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="22864-164">Souhrn</span><span class="sxs-lookup"><span data-stu-id="22864-164">Summary</span></span>

<span data-ttu-id="22864-165">Cílem tohoto kurzu bylo projednat jeden přístup k provádění ověřování v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="22864-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="22864-166">V tomto kurzu jste zjistili, jak přesunout veškerou logiku ověřování z vašich řadičů do samostatné vrstvy služby.</span><span class="sxs-lookup"><span data-stu-id="22864-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="22864-167">Zjistili jste také, jak izolovat vrstvu služby z vaší vrstvy kontroleru vytvořením třídy ModelStateWrapper.</span><span class="sxs-lookup"><span data-stu-id="22864-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22864-168">[Předchozí](validating-with-the-idataerrorinfo-interface-cs.md)
> [Další](validation-with-the-data-annotation-validators-cs.md)</span><span class="sxs-lookup"><span data-stu-id="22864-168">[Previous](validating-with-the-idataerrorinfo-interface-cs.md)
[Next](validation-with-the-data-annotation-validators-cs.md)</span></span>
