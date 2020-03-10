---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: Provádění několika animací současně (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit sever...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598117"
---
# <a name="executing-several-animations-at-the-same-time-c"></a><span data-ttu-id="a126c-104">Provádění několika animací současně (C#)</span><span class="sxs-lookup"><span data-stu-id="a126c-104">Executing Several Animations at The Same Time (C#)</span></span>

<span data-ttu-id="a126c-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a126c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a126c-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a126c-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span></span>

> <span data-ttu-id="a126c-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a126c-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a126c-108">Umožňuje paralelní spuštění několika animací.</span><span class="sxs-lookup"><span data-stu-id="a126c-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="a126c-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="a126c-109">Overview</span></span>

<span data-ttu-id="a126c-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a126c-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a126c-111">Umožňuje paralelní spuštění několika animací.</span><span class="sxs-lookup"><span data-stu-id="a126c-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="a126c-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="a126c-112">Steps</span></span>

<span data-ttu-id="a126c-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="a126c-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

<span data-ttu-id="a126c-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="a126c-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

<span data-ttu-id="a126c-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="a126c-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

<span data-ttu-id="a126c-116">Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="a126c-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

<span data-ttu-id="a126c-117">V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla.</span><span class="sxs-lookup"><span data-stu-id="a126c-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="a126c-118">Obecně `<OnLoad>` akceptuje pouze jednu animaci.</span><span class="sxs-lookup"><span data-stu-id="a126c-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="a126c-119">Rozhraní animace umožňuje připojit několik animací k jednomu pomocí elementu `<Parallel>`.</span><span class="sxs-lookup"><span data-stu-id="a126c-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="a126c-120">Všechny animace v rámci `<Parallel>` jsou spouštěny ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="a126c-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="a126c-121">Zde je možné označení pro ovládací prvek `AnimationExtender`, podrobné změny a změna velikosti panelu ve stejnou dobu:</span><span class="sxs-lookup"><span data-stu-id="a126c-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

<span data-ttu-id="a126c-122">A skutečně: když spustíte tento skript, panel se zobrazí a pak se změní velikost (víc než při cestě k jeho šířce a poloviční výška) a rozchází se současně.</span><span class="sxs-lookup"><span data-stu-id="a126c-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="a126c-123">[![panelu se dozvíte a mění velikost (včetně jeho obsahu), a to díky modulu vykreslování v prohlížeči).](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a126c-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span></span>

<span data-ttu-id="a126c-124">Na panelu se dozvíte, jak změnit velikost (včetně jejího obsahu), a to díky modulu vykreslování v prohlížeči ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-at-the-same-time-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a126c-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a126c-125">[Předchozí](adding-animation-to-a-control-cs.md)
> [Další](executing-several-animations-after-each-other-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a126c-125">[Previous](adding-animation-to-a-control-cs.md)
[Next](executing-several-animations-after-each-other-cs.md)</span></span>
