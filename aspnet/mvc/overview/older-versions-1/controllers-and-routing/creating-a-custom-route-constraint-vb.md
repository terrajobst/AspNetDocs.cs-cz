---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: Vytvoření vlastního omezení trasy (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther ukazuje, jak můžete vytvořit vlastní omezení trasy. Implementujeme jednoduché vlastní omezení, které brání tomu, aby se trasa shodovala s...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601407"
---
# <a name="creating-a-custom-route-constraint-vb"></a><span data-ttu-id="35853-104">Vytvoření vlastního omezení trasy (VB)</span><span class="sxs-lookup"><span data-stu-id="35853-104">Creating a Custom Route Constraint (VB)</span></span>

<span data-ttu-id="35853-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="35853-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="35853-106">Stephen Walther ukazuje, jak můžete vytvořit vlastní omezení trasy.</span><span class="sxs-lookup"><span data-stu-id="35853-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="35853-107">Implementujeme jednoduché vlastní omezení, které zabrání tomu, aby se trasa shodovala s tím, jak se ze vzdáleného počítače provede požadavek prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="35853-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="35853-108">Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní omezení trasy.</span><span class="sxs-lookup"><span data-stu-id="35853-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="35853-109">Vlastní omezení trasy vám umožní zabránit tomu, aby se trasa shodovala, pokud se neshoduje nějaká vlastní podmínka.</span><span class="sxs-lookup"><span data-stu-id="35853-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="35853-110">V tomto kurzu vytvoříme omezení trasy localhost.</span><span class="sxs-lookup"><span data-stu-id="35853-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="35853-111">Omezení trasy localhost se shoduje pouze s požadavky provedenými z místního počítače.</span><span class="sxs-lookup"><span data-stu-id="35853-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="35853-112">Vzdálené požadavky přes Internet se neshodují.</span><span class="sxs-lookup"><span data-stu-id="35853-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="35853-113">Vlastní omezení trasy implementujete implementací rozhraní omezení IRouteConstraint.</span><span class="sxs-lookup"><span data-stu-id="35853-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="35853-114">Toto je extrémně jednoduché rozhraní, které popisuje jedinou metodu:</span><span class="sxs-lookup"><span data-stu-id="35853-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="35853-115">Metoda vrací logickou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="35853-115">The method returns a Boolean value.</span></span> <span data-ttu-id="35853-116">Pokud vrátíte hodnotu false, trasa přidružená k omezení nebude odpovídat požadavku prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="35853-116">If you return False, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="35853-117">Omezení localhost je obsaženo v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="35853-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="35853-118">**Výpis 1 – LocalhostConstraint. vb**</span><span class="sxs-lookup"><span data-stu-id="35853-118">**Listing 1 - LocalhostConstraint.vb**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="35853-119">Omezení v výpisu 1 využívá vlastnost místní vystavenou třídou HttpRequest.</span><span class="sxs-lookup"><span data-stu-id="35853-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="35853-120">Tato vlastnost vrátí hodnotu true, pokud je IP adresa požadavku buď 127.0.0.1, nebo pokud je IP adresa požadavku shodná s IP adresou serveru.</span><span class="sxs-lookup"><span data-stu-id="35853-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="35853-121">Použijete vlastní omezení v rámci trasy definované v souboru Global. asax.</span><span class="sxs-lookup"><span data-stu-id="35853-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="35853-122">Soubor Global. asax v seznamu 2 používá omezení localhost k tomu, aby nikdo nemohl požádat o stránku správce, pokud nevytvoří požadavek z místního serveru.</span><span class="sxs-lookup"><span data-stu-id="35853-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="35853-123">Například požadavek na/Admin/DeleteAll selže při provedení ze vzdáleného serveru.</span><span class="sxs-lookup"><span data-stu-id="35853-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="35853-124">**Výpis 2 – Global. asax**</span><span class="sxs-lookup"><span data-stu-id="35853-124">**Listing 2 - Global.asax**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="35853-125">V definici trasy správce se používá omezení localhost.</span><span class="sxs-lookup"><span data-stu-id="35853-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="35853-126">Tato trasa nebude odpovídat požadavku vzdáleného prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="35853-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="35853-127">Upozorňujeme však, že jiné trasy definované v Global. asax mohou odpovídat stejné žádosti.</span><span class="sxs-lookup"><span data-stu-id="35853-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="35853-128">Je důležité pochopit, že omezení brání konkrétní trase v porovnání s požadavkem, a ne všechny trasy definované v souboru Global. asax.</span><span class="sxs-lookup"><span data-stu-id="35853-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="35853-129">Všimněte si, že výchozí trasa byla zakomentována ze souboru Global. asax v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="35853-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="35853-130">Pokud zahrnete výchozí trasu, bude výchozí trasa odpovídat požadavkům pro kontroler správce.</span><span class="sxs-lookup"><span data-stu-id="35853-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="35853-131">V takovém případě mohou vzdálení uživatelé i přesto vyvolat akce kontroleru správce, i když jejich požadavky by neodpovídaly trase správce.</span><span class="sxs-lookup"><span data-stu-id="35853-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="35853-132">Předchozí</span><span class="sxs-lookup"><span data-stu-id="35853-132">Previous</span></span>](creating-a-route-constraint-vb.md)
