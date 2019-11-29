---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: Aktivace animace v jiném ovládacím prvku (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Obecně se spouští...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575034"
---
# <a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="50a9e-104">Aktivace animace jiného ovládacího prvku (VB)</span><span class="sxs-lookup"><span data-stu-id="50a9e-104">Triggering an Animation in another Control (VB)</span></span>

<span data-ttu-id="50a9e-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="50a9e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="50a9e-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="50a9e-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="50a9e-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="50a9e-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="50a9e-108">Obecně se spouští animace pomocí interakce uživatele se stejným ovládacím prvkem.</span><span class="sxs-lookup"><span data-stu-id="50a9e-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="50a9e-109">Je však také možné pracovat s jedním ovládacím prvkem a následně animacem jiného ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="50a9e-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="50a9e-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="50a9e-110">Overview</span></span>

<span data-ttu-id="50a9e-111">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="50a9e-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="50a9e-112">Obecně se spouští animace pomocí interakce uživatele se stejným ovládacím prvkem.</span><span class="sxs-lookup"><span data-stu-id="50a9e-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="50a9e-113">Je však také možné pracovat s jedním ovládacím prvkem a následně animacem jiného ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="50a9e-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="50a9e-114">Uvedené</span><span class="sxs-lookup"><span data-stu-id="50a9e-114">Steps</span></span>

<span data-ttu-id="50a9e-115">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="50a9e-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="50a9e-116">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="50a9e-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="50a9e-117">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="50a9e-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="50a9e-118">Aby bylo možné začít animovat panel, je použito tlačítko HTML.</span><span class="sxs-lookup"><span data-stu-id="50a9e-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="50a9e-119">Všimněte si, že `<input type="button" />` je výhodnější pro `<asp:Button />`, protože nepožadujeme postback, když uživatel na toto tlačítko klikne.</span><span class="sxs-lookup"><span data-stu-id="50a9e-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="50a9e-120">Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server"`.</span><span class="sxs-lookup"><span data-stu-id="50a9e-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="50a9e-121">Je důležité nastavit `TargetControlID` na ID tlačítka (element, který aktivuje animaci), nikoli na ID panelu (element je animovaný).</span><span class="sxs-lookup"><span data-stu-id="50a9e-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="50a9e-122">V uzlu `<Animations>` umístěte animace obvyklým způsobem.</span><span class="sxs-lookup"><span data-stu-id="50a9e-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="50a9e-123">Aby bylo možné změnit panel, nikoli tlačítko, nastavte atribut `AnimationTarget` pro všechny elementy animace v rámci `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="50a9e-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="50a9e-124">Hodnota pro `AnimationTarget` je ID panelu kurzu.</span><span class="sxs-lookup"><span data-stu-id="50a9e-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="50a9e-125">Tímto způsobem se animace vyskytují s panelem, nikoli s tlačítkem aktivovat.</span><span class="sxs-lookup"><span data-stu-id="50a9e-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="50a9e-126">Tady je `AnimationExtender` značky pro tento scénář:</span><span class="sxs-lookup"><span data-stu-id="50a9e-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="50a9e-127">Všimněte si speciálního pořadí, ve kterém se jednotlivé animace zobrazí.</span><span class="sxs-lookup"><span data-stu-id="50a9e-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="50a9e-128">Nejprve se tlačítko po spuštění animace deaktivuje.</span><span class="sxs-lookup"><span data-stu-id="50a9e-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="50a9e-129">Vzhledem k tomu, že v elementu `<EnableAction>` není žádný atribut `AnimationTarget`, tato animace se aplikuje na ovládací prvek původce: tlačítko.</span><span class="sxs-lookup"><span data-stu-id="50a9e-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="50a9e-130">Následující dva kroky animace je třeba provést paralelně (`<Parallel>` element).</span><span class="sxs-lookup"><span data-stu-id="50a9e-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="50a9e-131">Oba mají své `AnimationTarget` atributy nastavené na `"Panel1"`, takže animován panel, ne tlačítko.</span><span class="sxs-lookup"><span data-stu-id="50a9e-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="50a9e-132">[![kliknutí myší na tlačítko spustí animaci panelu](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="50a9e-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="50a9e-133">Kliknutím na tlačítko myši na tlačítko se spustí animace panelu ([kliknutím zobrazíte obrázek v plné velikosti).](triggering-an-animation-in-another-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="50a9e-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="50a9e-134">[Předchozí](disabling-actions-during-animation-vb.md)
> [Další](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="50a9e-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
