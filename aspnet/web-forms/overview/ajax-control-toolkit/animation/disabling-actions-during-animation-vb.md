---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: Zakázání akcí během animace (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Také podporuje akci...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536237"
---
# <a name="disabling-actions-during-animation-vb"></a><span data-ttu-id="e6aca-104">Zakázání akcí během animace (VB)</span><span class="sxs-lookup"><span data-stu-id="e6aca-104">Disabling Actions during Animation (VB)</span></span>

<span data-ttu-id="e6aca-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e6aca-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e6aca-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e6aca-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span></span>

> <span data-ttu-id="e6aca-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="e6aca-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e6aca-108">Podporuje také akce, jako je kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="e6aca-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="e6aca-109">Pokud se ale po kliknutí myší spustí animace, je žádoucí zakázat kliknutí myší během animace.</span><span class="sxs-lookup"><span data-stu-id="e6aca-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="e6aca-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="e6aca-110">Overview</span></span>

<span data-ttu-id="e6aca-111">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="e6aca-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e6aca-112">Podporuje také akce, jako je kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="e6aca-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="e6aca-113">Pokud se ale po kliknutí myší spustí animace, je žádoucí zakázat kliknutí myší během animace.</span><span class="sxs-lookup"><span data-stu-id="e6aca-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="e6aca-114">Kroky</span><span class="sxs-lookup"><span data-stu-id="e6aca-114">Steps</span></span>

<span data-ttu-id="e6aca-115">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="e6aca-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

<span data-ttu-id="e6aca-116">Animace se použije na tlačítko HTML jako toto:</span><span class="sxs-lookup"><span data-stu-id="e6aca-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

<span data-ttu-id="e6aca-117">Všimněte si, že se místo webového ovládacího prvku používá ovládací prvek HTML, protože nechcete, aby tlačítko vytvořilo postback. Stačí spustit animaci na straně klienta pro nás.</span><span class="sxs-lookup"><span data-stu-id="e6aca-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="e6aca-118">Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="e6aca-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

<span data-ttu-id="e6aca-119">V uzlu `<Animations>` je `<OnClick>` pravého prvku pro zpracování kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="e6aca-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="e6aca-120">Tlačítko však může být kliknuto i během animace.</span><span class="sxs-lookup"><span data-stu-id="e6aca-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="e6aca-121">Element `<EnableAction>` se může postarat.</span><span class="sxs-lookup"><span data-stu-id="e6aca-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="e6aca-122">Nastavení `Enabled="false"` zakáže tlačítko v rámci animace.</span><span class="sxs-lookup"><span data-stu-id="e6aca-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="e6aca-123">Vzhledem k tomu, že používáme několik jednotlivých animací (zakážete tlačítko a skutečné animace), `<Parallel>` element je nutný k vzájemnému připevnění jednotlivých animací.</span><span class="sxs-lookup"><span data-stu-id="e6aca-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="e6aca-124">Toto je kompletní označení pro `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="e6aca-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

<span data-ttu-id="e6aca-125">Je také možné znovu povolit tlačítko po animaci, a to pomocí následujícího elementu XML na konci seznamu:</span><span class="sxs-lookup"><span data-stu-id="e6aca-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

<span data-ttu-id="e6aca-126">V daném scénáři to však nebude k dispozici, protože tlačítko zmizí a na konci animace není vidět.</span><span class="sxs-lookup"><span data-stu-id="e6aca-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="e6aca-127">[![tlačítko je po spuštění animace zakázané.](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e6aca-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span></span>

<span data-ttu-id="e6aca-128">Tlačítko je zakázáno, jakmile se spustí animace ([kliknutím zobrazíte obrázek v plné velikosti).](disabling-actions-during-animation-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e6aca-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e6aca-129">[Předchozí](animating-in-response-to-user-interaction-vb.md)
> [Další](triggering-an-animation-in-another-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e6aca-129">[Previous](animating-in-response-to-user-interaction-vb.md)
[Next](triggering-an-animation-in-another-control-vb.md)</span></span>
