---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: Přidání animace do ovládacího prvku (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. V tomto kurzu se dozvíte, jak...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607121"
---
# <a name="adding-animation-to-a-control-c"></a><span data-ttu-id="80559-104">Přidání animace k ovládacímu prvku (C#)</span><span class="sxs-lookup"><span data-stu-id="80559-104">Adding Animation to a Control (C#)</span></span>

<span data-ttu-id="80559-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="80559-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="80559-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="80559-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="80559-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="80559-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="80559-108">V tomto kurzu se dozvíte, jak nastavit takovou animaci.</span><span class="sxs-lookup"><span data-stu-id="80559-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="80559-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="80559-109">Overview</span></span>

<span data-ttu-id="80559-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="80559-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="80559-111">V tomto kurzu se dozvíte, jak nastavit takovou animaci.</span><span class="sxs-lookup"><span data-stu-id="80559-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="80559-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="80559-112">Steps</span></span>

<span data-ttu-id="80559-113">Prvním krokem je obvykle zahrnutí `ScriptManager` do stránky, aby byla načtena knihovna ASP.NET AJAX a bylo možné použít ovládací sadu Toolkit:</span><span class="sxs-lookup"><span data-stu-id="80559-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="80559-114">Animace v tomto scénáři se použije na panel textu, který vypadá nějak takto:</span><span class="sxs-lookup"><span data-stu-id="80559-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="80559-115">Přidružená Třída CSS pro panel definuje barvu pozadí a šířku:</span><span class="sxs-lookup"><span data-stu-id="80559-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="80559-116">V dalším kroku potřebujeme `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="80559-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="80559-117">Po poskytnutí `ID` a obvyklých `runat="server"`musí být atribut `TargetControlID` nastaven na řízení pro animaci v našem případě, panel:</span><span class="sxs-lookup"><span data-stu-id="80559-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="80559-118">Celá animace se aplikuje deklarativně pomocí syntaxe XML, ale v současné době není plně podporovaná IntelliSense sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80559-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="80559-119">Kořenový uzel je `<Animations>;` v rámci tohoto uzlu, jsou povoleny různé události, které určují, kdy se mají tyto animace (y) použít:</span><span class="sxs-lookup"><span data-stu-id="80559-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="80559-120">`OnClick` (kliknutí myší)</span><span class="sxs-lookup"><span data-stu-id="80559-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="80559-121">`OnHoverOut` (když myš opustí ovládací prvek)</span><span class="sxs-lookup"><span data-stu-id="80559-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="80559-122">`OnHoverOver` (když ukazatel myši setrvá na ovládacím prvku, zastaví se animace `OnHoverOut`).</span><span class="sxs-lookup"><span data-stu-id="80559-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="80559-123">`OnLoad` (při načtení stránky)</span><span class="sxs-lookup"><span data-stu-id="80559-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="80559-124">`OnMouseOut` (když myš opustí ovládací prvek)</span><span class="sxs-lookup"><span data-stu-id="80559-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="80559-125">`OnMouseOver` (když ukazatel myši setrvá na ovládacím prvku, nezastaví se `OnMouseOut` animace).</span><span class="sxs-lookup"><span data-stu-id="80559-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="80559-126">Rozhraní obsahuje sadu animací, každý z nich reprezentované vlastním prvkem XML.</span><span class="sxs-lookup"><span data-stu-id="80559-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="80559-127">Tady je výběr:</span><span class="sxs-lookup"><span data-stu-id="80559-127">Here is a selection:</span></span>

- <span data-ttu-id="80559-128">`<Color>` (změna barvy)</span><span class="sxs-lookup"><span data-stu-id="80559-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="80559-129">`<FadeIn>` (stromeček)</span><span class="sxs-lookup"><span data-stu-id="80559-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="80559-130">`<FadeOut>` (stromeček)</span><span class="sxs-lookup"><span data-stu-id="80559-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="80559-131">`<Property>` (Změna vlastnosti ovládacího prvku)</span><span class="sxs-lookup"><span data-stu-id="80559-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="80559-132">`<Pulse>` (PULSATING)</span><span class="sxs-lookup"><span data-stu-id="80559-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="80559-133">`<Resize>` (Změna velikosti)</span><span class="sxs-lookup"><span data-stu-id="80559-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="80559-134">`<Scale>` (proporcionálně se mění velikost)</span><span class="sxs-lookup"><span data-stu-id="80559-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="80559-135">V tomto příkladu je panel vymizet. Animace musí trvat 1,5 sekund (`Duration` atribut), přičemž se zobrazí 24 snímků (kroky animace) za sekundu (atribut`Fps`).</span><span class="sxs-lookup"><span data-stu-id="80559-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="80559-136">Zde je kompletní označení pro ovládací prvek `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="80559-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="80559-137">Když spustíte tento skript, panel se zobrazí a zmizí v jednom a půl sekundách.</span><span class="sxs-lookup"><span data-stu-id="80559-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="80559-138">[![panelu se dozvíte](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="80559-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="80559-139">Panel se zobrazuje na více instancí ([kliknutím zobrazíte obrázek v plné velikosti).](adding-animation-to-a-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="80559-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="80559-140">Next</span><span class="sxs-lookup"><span data-stu-id="80559-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
