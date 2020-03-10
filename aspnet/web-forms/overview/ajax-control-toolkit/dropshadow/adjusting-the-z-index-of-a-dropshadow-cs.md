---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: Úprava indexu Z-v DropShadow (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Tento stín je však někdy v konfliktu s jinými ovládacími prvky pro insta...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613881"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="5df28-104">Úprava indexu Z ovládacího prvku DropShadow (C#)</span><span class="sxs-lookup"><span data-stu-id="5df28-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>

<span data-ttu-id="5df28-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5df28-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5df28-106">[Stažení kódu](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5df28-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="5df28-107">Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín.</span><span class="sxs-lookup"><span data-stu-id="5df28-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="5df28-108">Tento stín je však někdy v konfliktu s jinými ovládacími prvky, například ovládací prvek nabídky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5df28-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="5df28-109">Když se položka nabídky objeví, zobrazí se za stínem.</span><span class="sxs-lookup"><span data-stu-id="5df28-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="5df28-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="5df28-110">Overview</span></span>

<span data-ttu-id="5df28-111">Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín.</span><span class="sxs-lookup"><span data-stu-id="5df28-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="5df28-112">Tento stín je však někdy v konfliktu s jinými ovládacími prvky, například ovládací prvek nabídky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5df28-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="5df28-113">Když se položka nabídky objeví, zobrazí se za stínem.</span><span class="sxs-lookup"><span data-stu-id="5df28-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="5df28-114">Kroky</span><span class="sxs-lookup"><span data-stu-id="5df28-114">Steps</span></span>

<span data-ttu-id="5df28-115">Kód se zahájí pomocí samotného panelu, který obsahuje dostatek textu, aby panel obsahoval dostatek textu, aby bylo možné tento efekt zobrazit:</span><span class="sxs-lookup"><span data-stu-id="5df28-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="5df28-116">Další panel je umístěn přímo před `panelShadow` panel.</span><span class="sxs-lookup"><span data-stu-id="5df28-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="5df28-117">Obsahuje nabídku s vodorovnou orientací, aby se zobrazovaly položky nabídky (nebo místo toho: v rámci) `dropShadow` panel):</span><span class="sxs-lookup"><span data-stu-id="5df28-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="5df28-118">Pak se přidá `DropShadowExtender`, aby se rozšířil panel `panelShadow` s efektem vrženého stínu:</span><span class="sxs-lookup"><span data-stu-id="5df28-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="5df28-119">Nakonec ovládací prvek `ScriptManager` AJAX ASP.NET umožňuje, aby sada nástrojů pracovala:</span><span class="sxs-lookup"><span data-stu-id="5df28-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="5df28-120">Když spustíte tento skript, položky nabídky se zobrazí pod panelem.</span><span class="sxs-lookup"><span data-stu-id="5df28-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="5df28-121">Nabídka však používá třídu CSS `panel`, kde stačí definovat dvě věci, aby se prvky zobrazovaly před druhým panelem:</span><span class="sxs-lookup"><span data-stu-id="5df28-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="5df28-122">Relativní umístění</span><span class="sxs-lookup"><span data-stu-id="5df28-122">Relative positioning</span></span>
- <span data-ttu-id="5df28-123">Kladný z-index</span><span class="sxs-lookup"><span data-stu-id="5df28-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="5df28-124">Ovládací prvek `DropShadowExtender` pak není v konfliktu s ovládacím prvkem nabídky.</span><span class="sxs-lookup"><span data-stu-id="5df28-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="5df28-125">[![před: položka nabídky není viditelná.](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5df28-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="5df28-126">Před: položka nabídky není zobrazená ([kliknutím zobrazíte obrázek v plné velikosti).](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5df28-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>

<span data-ttu-id="5df28-127">[![po: zobrazí se položka nabídky.](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5df28-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="5df28-128">Po: zobrazí se položka nabídky ([kliknutím zobrazíte obrázek v plné velikosti](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="5df28-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5df28-129">Next</span><span class="sxs-lookup"><span data-stu-id="5df28-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
