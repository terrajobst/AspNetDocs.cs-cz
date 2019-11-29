---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: Animace v reakci na interakci uživatele (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace můžou mít hvězdičku...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607027"
---
# <a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="7b1bd-104">Animace v reakci na interakci uživatele (VB)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-104">Animating in Response To User Interaction (VB)</span></span>

<span data-ttu-id="7b1bd-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7b1bd-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="7b1bd-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="7b1bd-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7b1bd-108">Animace mohou být spouštěny automaticky nebo mohou být aktivovány interakcí uživatele, například kliknutím myší.</span><span class="sxs-lookup"><span data-stu-id="7b1bd-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="7b1bd-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="7b1bd-109">Overview</span></span>

<span data-ttu-id="7b1bd-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="7b1bd-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7b1bd-111">Animace mohou být spouštěny automaticky nebo mohou být aktivovány interakcí uživatele, například kliknutím myší.</span><span class="sxs-lookup"><span data-stu-id="7b1bd-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="7b1bd-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="7b1bd-112">Steps</span></span>

<span data-ttu-id="7b1bd-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="7b1bd-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="7b1bd-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="7b1bd-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="7b1bd-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="7b1bd-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="7b1bd-116">Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="7b1bd-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="7b1bd-117">V uzlu `<Animations>` existuje pět způsobů, jak spustit animaci prostřednictvím interakce s uživatelem (chybějící element je `<OnLoad>`, který je proveden po úplném načtení celé stránky):</span><span class="sxs-lookup"><span data-stu-id="7b1bd-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="7b1bd-118">`<OnClick>` (kliknutí myší na ovládací prvek)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="7b1bd-119">`<OnHoverOut>` (myš opustí ovládací prvek)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="7b1bd-120">`<OnHoverOver>` (najetí myší nad ovládací prvek, zastavení `<OnHoverOut>` animace)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="7b1bd-121">`<OnMouseOut>` (opustí ovládací prvek myší)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="7b1bd-122">`<OnMouseOver>` (najetí myší na ovládací prvek, nezastavení `<OnMouseOut>` animace)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="7b1bd-123">V tomto scénáři se používá `<OnClick>`.</span><span class="sxs-lookup"><span data-stu-id="7b1bd-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="7b1bd-124">Když uživatel klikne na panel, změní se jeho velikost a zároveň se vykreslí.</span><span class="sxs-lookup"><span data-stu-id="7b1bd-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

<span data-ttu-id="7b1bd-125">[![kliknutí myší se spustí animace](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="7b1bd-126">Po kliknutí myší se spustí animace ([kliknutím zobrazíte obrázek v plné velikosti).](animating-in-response-to-user-interaction-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7b1bd-127">[Předchozí](picking-one-animation-out-of-a-list-vb.md)
> [Další](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7b1bd-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
