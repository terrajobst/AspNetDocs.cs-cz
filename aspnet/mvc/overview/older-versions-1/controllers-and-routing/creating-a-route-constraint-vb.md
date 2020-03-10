---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: Vytvoření omezení trasy (VB) | Microsoft Docs
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak se požadavky prohlížeče shodují s trasami vytvořením omezení trasy pomocí regulárních výrazů.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 205742dd8f866c8828008c8aac7ab3f98b173ceb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601386"
---
# <a name="creating-a-route-constraint-vb"></a><span data-ttu-id="177e9-103">Vytvoření omezení trasy (VB)</span><span class="sxs-lookup"><span data-stu-id="177e9-103">Creating a Route Constraint (VB)</span></span>

<span data-ttu-id="177e9-104">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="177e9-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="177e9-105">V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak se požadavky prohlížeče shodují s trasami vytvořením omezení trasy pomocí regulárních výrazů.</span><span class="sxs-lookup"><span data-stu-id="177e9-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="177e9-106">Omezení tras použijete k omezení požadavků prohlížeče, které odpovídají konkrétní trase.</span><span class="sxs-lookup"><span data-stu-id="177e9-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="177e9-107">K určení omezení trasy můžete použít regulární výraz.</span><span class="sxs-lookup"><span data-stu-id="177e9-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="177e9-108">Představte si například, že jste v souboru Global. asax definovali trasu v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="177e9-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="177e9-109">**Výpis 1 – Global. asax. vb**</span><span class="sxs-lookup"><span data-stu-id="177e9-109">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="177e9-110">Výpis 1 obsahuje trasu s názvem produkt.</span><span class="sxs-lookup"><span data-stu-id="177e9-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="177e9-111">Můžete použít trasu produktu k mapování požadavků prohlížeče na ProductController obsaženou v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="177e9-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="177e9-112">**Výpis 2 – Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="177e9-112">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="177e9-113">Všimněte si, že akce podrobnosti () vystavená produktovým adaptérem přijímá jeden parametr s názvem productId.</span><span class="sxs-lookup"><span data-stu-id="177e9-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="177e9-114">Tento parametr je celočíselným parametrem.</span><span class="sxs-lookup"><span data-stu-id="177e9-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="177e9-115">Trasa definovaná v seznamu 1 bude odpovídat všem následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="177e9-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="177e9-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="177e9-116">/Product/23</span></span>
- <span data-ttu-id="177e9-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="177e9-117">/Product/7</span></span>

<span data-ttu-id="177e9-118">Tato trasa bohužel bude taky odpovídat následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="177e9-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="177e9-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="177e9-119">/Product/blah</span></span>
- <span data-ttu-id="177e9-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="177e9-120">/Product/apple</span></span>

<span data-ttu-id="177e9-121">Vzhledem k tomu, že akce Details () očekává parametr typu Integer, vytvoření požadavku, který obsahuje něco jiného než celočíselné hodnoty způsobí chybu.</span><span class="sxs-lookup"><span data-stu-id="177e9-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="177e9-122">Pokud například zadáte adresu URL/Product/Apple do prohlížeče, zobrazí se chybová stránka na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="177e9-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="177e9-123">[![dialogového okna Nový projekt](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="177e9-123">[![The New Project dialog box](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span></span>

<span data-ttu-id="177e9-124">**Obrázek 01**: zobrazení rozbalené stránky ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-route-constraint-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="177e9-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-vb/_static/image2.png))</span></span>

<span data-ttu-id="177e9-125">Co opravdu chcete udělat, odpovídá jenom adresám URL, které obsahují správné celé číslo productId.</span><span class="sxs-lookup"><span data-stu-id="177e9-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="177e9-126">Omezení můžete použít při definování trasy, která bude omezovat adresy URL, které odpovídají trase.</span><span class="sxs-lookup"><span data-stu-id="177e9-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="177e9-127">Upravená trasa produktu v seznamu 3 obsahuje omezení regulárního výrazu, které odpovídá pouze celým číslům.</span><span class="sxs-lookup"><span data-stu-id="177e9-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="177e9-128">**Výpis 3 – Global. asax. vb**</span><span class="sxs-lookup"><span data-stu-id="177e9-128">**Listing 3 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="177e9-129">Regulární výraz \D + odpovídá jednomu nebo více celým číslům.</span><span class="sxs-lookup"><span data-stu-id="177e9-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="177e9-130">Toto omezení způsobí, že trasa produktu bude odpovídat následujícím adresám URL:</span><span class="sxs-lookup"><span data-stu-id="177e9-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="177e9-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="177e9-131">/Product/3</span></span>
- <span data-ttu-id="177e9-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="177e9-132">/Product/8999</span></span>

<span data-ttu-id="177e9-133">Ale ne následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="177e9-133">But not the following URLs:</span></span>

- <span data-ttu-id="177e9-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="177e9-134">/Product/apple</span></span>
- <span data-ttu-id="177e9-135">/Product</span><span class="sxs-lookup"><span data-stu-id="177e9-135">/Product</span></span>

<span data-ttu-id="177e9-136">Tyto požadavky prohlížeče budou zpracovány jinou trasou, nebo pokud nejsou k dispozici žádné vyhovující trasy, nebude možné *najít prostředek* , který se vrátí.</span><span class="sxs-lookup"><span data-stu-id="177e9-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="177e9-137">[Předchozí](creating-custom-routes-vb.md)
> [Další](creating-a-custom-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="177e9-137">[Previous](creating-custom-routes-vb.md)
[Next](creating-a-custom-route-constraint-vb.md)</span></span>
