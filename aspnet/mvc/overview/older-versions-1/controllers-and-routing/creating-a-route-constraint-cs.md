---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: Vytváření omezení trasy (C#) | Microsoft Docs
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak se požadavky prohlížeče shodují s trasami vytvořením omezení trasy pomocí regulárních výrazů.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582010"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="a8097-103">Vytvoření omezení trasy (C#)</span><span class="sxs-lookup"><span data-stu-id="a8097-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="a8097-104">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a8097-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="a8097-105">V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak se požadavky prohlížeče shodují s trasami vytvořením omezení trasy pomocí regulárních výrazů.</span><span class="sxs-lookup"><span data-stu-id="a8097-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="a8097-106">Omezení tras použijete k omezení požadavků prohlížeče, které odpovídají konkrétní trase.</span><span class="sxs-lookup"><span data-stu-id="a8097-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="a8097-107">K určení omezení trasy můžete použít regulární výraz.</span><span class="sxs-lookup"><span data-stu-id="a8097-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="a8097-108">Představte si například, že jste v souboru Global. asax definovali trasu v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="a8097-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="a8097-109">**Výpis 1 – Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="a8097-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="a8097-110">Výpis 1 obsahuje trasu s názvem produkt.</span><span class="sxs-lookup"><span data-stu-id="a8097-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="a8097-111">Můžete použít trasu produktu k mapování požadavků prohlížeče na ProductController obsaženou v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="a8097-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="a8097-112">**Výpis 2 – Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="a8097-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="a8097-113">Všimněte si, že akce podrobnosti () vystavená produktovým adaptérem přijímá jeden parametr s názvem productId.</span><span class="sxs-lookup"><span data-stu-id="a8097-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="a8097-114">Tento parametr je celočíselným parametrem.</span><span class="sxs-lookup"><span data-stu-id="a8097-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="a8097-115">Trasa definovaná v seznamu 1 bude odpovídat všem následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="a8097-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="a8097-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="a8097-116">/Product/23</span></span>
- <span data-ttu-id="a8097-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="a8097-117">/Product/7</span></span>

<span data-ttu-id="a8097-118">Tato trasa bohužel bude taky odpovídat následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="a8097-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="a8097-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="a8097-119">/Product/blah</span></span>
- <span data-ttu-id="a8097-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="a8097-120">/Product/apple</span></span>

<span data-ttu-id="a8097-121">Vzhledem k tomu, že akce Details () očekává parametr typu Integer, vytvoření požadavku, který obsahuje něco jiného než celočíselné hodnoty způsobí chybu.</span><span class="sxs-lookup"><span data-stu-id="a8097-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="a8097-122">Pokud například zadáte adresu URL/Product/Apple do prohlížeče, zobrazí se chybová stránka na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="a8097-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="a8097-123">[![dialogového okna Nový projekt](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a8097-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="a8097-124">**Obrázek 01**: zobrazení rozbalené stránky ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-route-constraint-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="a8097-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>

<span data-ttu-id="a8097-125">Co opravdu chcete udělat, odpovídá jenom adresám URL, které obsahují správné celé číslo productId.</span><span class="sxs-lookup"><span data-stu-id="a8097-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="a8097-126">Omezení můžete použít při definování trasy, která bude omezovat adresy URL, které odpovídají trase.</span><span class="sxs-lookup"><span data-stu-id="a8097-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="a8097-127">Upravená trasa produktu v seznamu 3 obsahuje omezení regulárního výrazu, které odpovídá pouze celým číslům.</span><span class="sxs-lookup"><span data-stu-id="a8097-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="a8097-128">**Výpis 3 – Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="a8097-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="a8097-129">Regulární výraz \D + odpovídá jednomu nebo více celým číslům.</span><span class="sxs-lookup"><span data-stu-id="a8097-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="a8097-130">Toto omezení způsobí, že trasa produktu bude odpovídat následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="a8097-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="a8097-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="a8097-131">/Product/3</span></span>
- <span data-ttu-id="a8097-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="a8097-132">/Product/8999</span></span>

<span data-ttu-id="a8097-133">Ale ne následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="a8097-133">But not the following URLs:</span></span>

- <span data-ttu-id="a8097-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="a8097-134">/Product/apple</span></span>
- <span data-ttu-id="a8097-135">/Product</span><span class="sxs-lookup"><span data-stu-id="a8097-135">/Product</span></span>

- <span data-ttu-id="a8097-136">Tyto požadavky prohlížeče budou zpracovány jinou trasou, nebo pokud nejsou k dispozici žádné vyhovující trasy, nebude možné *najít prostředek* , který se vrátí.</span><span class="sxs-lookup"><span data-stu-id="a8097-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a8097-137">[Předchozí](creating-custom-routes-cs.md)
> [Další](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a8097-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
