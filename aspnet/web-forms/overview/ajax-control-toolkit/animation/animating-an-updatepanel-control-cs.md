---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Animace ovládacího prvku UpdatePanel (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599904"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="039e7-104">Animace ovládacího prvku UpdatePanel (C#)</span><span class="sxs-lookup"><span data-stu-id="039e7-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="039e7-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="039e7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="039e7-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="039e7-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="039e7-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="039e7-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="039e7-108">Pro obsah ovládacího prvku UpdatePanel existuje speciální rozšířený objekt, který spoléhá na rámec animace: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="039e7-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="039e7-109">V tomto kurzu se dozvíte, jak nastavit takovou animaci pro UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="039e7-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="039e7-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="039e7-110">Overview</span></span>

<span data-ttu-id="039e7-111">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="039e7-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="039e7-112">Pro obsah `UpdatePanel`existuje speciální rozšířený objekt, který spoléhá na rámec animace: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="039e7-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="039e7-113">V tomto kurzu se dozvíte, jak nastavit takovou animaci pro `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="039e7-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="039e7-114">Uvedené</span><span class="sxs-lookup"><span data-stu-id="039e7-114">Steps</span></span>

<span data-ttu-id="039e7-115">Prvním krokem je obvykle zahrnutí `ScriptManager` do stránky, aby byla načtena knihovna ASP.NET AJAX a bylo možné použít ovládací sadu Toolkit:</span><span class="sxs-lookup"><span data-stu-id="039e7-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="039e7-116">Animace v tomto scénáři bude použita na ASP.NET `Wizard` webový ovládací prvek umístěný v `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="039e7-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="039e7-117">Tři (libovolné) kroky poskytují dostatek možností pro aktivaci zpětného volání:</span><span class="sxs-lookup"><span data-stu-id="039e7-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="039e7-118">Označení potřebné pro ovládací prvek `UpdatePanelAnimationExtender` je poměrně podobné označení používanému pro `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="039e7-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="039e7-119">V atributu `TargetControlID` poskytujeme `ID` `UpdatePanel` k animaci; v rámci ovládacího prvku `UpdatePanelAnimationExtender` prvek `<Animations>` obsahuje kód XML pro animace (y).</span><span class="sxs-lookup"><span data-stu-id="039e7-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="039e7-120">Existuje však jeden rozdíl: množství událostí a obslužných rutin událostí je omezeno na porovnání s `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="039e7-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="039e7-121">Pro `UpdatePanels`existují jenom dva z nich:</span><span class="sxs-lookup"><span data-stu-id="039e7-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="039e7-122">`<OnUpdated>` při aktualizaci prvku UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="039e7-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="039e7-123">`<OnUpdating>` při zahájení aktualizace ovládacího prvku UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="039e7-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="039e7-124">V tomto scénáři se nový obsah `UpdatePanel` (po zpětném vystavení) rozzvolna.</span><span class="sxs-lookup"><span data-stu-id="039e7-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="039e7-125">Toto je nezbytné označení pro:</span><span class="sxs-lookup"><span data-stu-id="039e7-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="039e7-126">Nyní, když dojde k postbacku v rámci prvku UpdatePanel, je nový obsah panelu plynule rozzvolna.</span><span class="sxs-lookup"><span data-stu-id="039e7-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="039e7-127">[![je další krok v průvodci slábnutí](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="039e7-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="039e7-128">V dalším kroku průvodce se[nezobrazuje (Kliknutím zobrazíte obrázek v plné velikosti).](animating-an-updatepanel-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="039e7-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="039e7-129">[Předchozí](changing-an-animation-using-client-side-code-cs.md)
> [Další](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="039e7-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
