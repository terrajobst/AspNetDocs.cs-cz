---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: Provádění několika animací po sobě (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit sever...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598131"
---
# <a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="72364-104">Postupné provedení několika animací (VB)</span><span class="sxs-lookup"><span data-stu-id="72364-104">Executing Several Animations after Each Other (VB)</span></span>

<span data-ttu-id="72364-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="72364-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="72364-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="72364-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="72364-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="72364-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="72364-108">Umožňuje spustit několik animací za sebou.</span><span class="sxs-lookup"><span data-stu-id="72364-108">It allows to run several animations one after the other.</span></span>

## <a name="overview"></a><span data-ttu-id="72364-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="72364-109">Overview</span></span>

<span data-ttu-id="72364-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="72364-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="72364-111">Umožňuje spustit několik animací za sebou.</span><span class="sxs-lookup"><span data-stu-id="72364-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="72364-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="72364-112">Steps</span></span>

<span data-ttu-id="72364-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="72364-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="72364-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="72364-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="72364-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="72364-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="72364-116">Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="72364-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="72364-117">V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla.</span><span class="sxs-lookup"><span data-stu-id="72364-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="72364-118">Obecně `<OnLoad>` akceptuje pouze jednu animaci.</span><span class="sxs-lookup"><span data-stu-id="72364-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="72364-119">Rozhraní animace umožňuje připojit několik animací k jednomu pomocí elementu `<Sequence>`.</span><span class="sxs-lookup"><span data-stu-id="72364-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="72364-120">Všechny animace v rámci `<Sequence>` jsou spouštěny jednou po druhém.</span><span class="sxs-lookup"><span data-stu-id="72364-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="72364-121">Zde je možné označení pro ovládací prvek `AnimationExtender`, nejprve panel Rozšiřte a poté zmenšete jeho výšku:</span><span class="sxs-lookup"><span data-stu-id="72364-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="72364-122">Když spustíte tento skript, panel se nejprve rozšíří a pak zmenší.</span><span class="sxs-lookup"><span data-stu-id="72364-122">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="72364-123">[![první šířka se zvyšuje.](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="72364-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="72364-124">Nejprve se zvětší Šířka ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-after-each-other-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="72364-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>

<span data-ttu-id="72364-125">[![pak se výška zmenší.](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="72364-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="72364-126">Pak se výška zmenší ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-after-each-other-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="72364-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="72364-127">[Předchozí](executing-several-animations-at-the-same-time-vb.md)
> [Další](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="72364-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
