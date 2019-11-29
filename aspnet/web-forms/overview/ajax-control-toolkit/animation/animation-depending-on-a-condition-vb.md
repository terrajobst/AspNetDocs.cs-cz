---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: Animace v závislosti na podmínce (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Zda je animace...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 583ebdbf109beb74b9a425020477183067bbb79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607024"
---
# <a name="animation-depending-on-a-condition-vb"></a><span data-ttu-id="475cd-104">Animace závislá na podmínce (VB)</span><span class="sxs-lookup"><span data-stu-id="475cd-104">Animation Depending On a Condition (VB)</span></span>

<span data-ttu-id="475cd-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="475cd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="475cd-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="475cd-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span></span>

> <span data-ttu-id="475cd-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="475cd-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="475cd-108">Zda je animace spuštěna, nebo ne, může také záviset na stavu ve formě některého kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="475cd-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="475cd-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="475cd-109">Overview</span></span>

<span data-ttu-id="475cd-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="475cd-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="475cd-111">Zda je animace spuštěna, nebo ne, může také záviset na stavu ve formě některého kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="475cd-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="475cd-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="475cd-112">Steps</span></span>

<span data-ttu-id="475cd-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="475cd-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

<span data-ttu-id="475cd-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="475cd-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

<span data-ttu-id="475cd-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="475cd-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

<span data-ttu-id="475cd-116">Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="475cd-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

<span data-ttu-id="475cd-117">V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla.</span><span class="sxs-lookup"><span data-stu-id="475cd-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="475cd-118">Místo jedné z běžných animací se `<Condition>` element přesune do hry.</span><span class="sxs-lookup"><span data-stu-id="475cd-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="475cd-119">Kód jazyka JavaScript poskytnutý jako hodnota atributu `ConditionScript` se spustí za běhu.</span><span class="sxs-lookup"><span data-stu-id="475cd-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="475cd-120">Pokud se vyhodnotí jako true, spustí se animace, jinak ne.</span><span class="sxs-lookup"><span data-stu-id="475cd-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="475cd-121">Následující kód poskytuje dvě animace, každý z nich je spuštěn v 50% případů po náhodném provedení.</span><span class="sxs-lookup"><span data-stu-id="475cd-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="475cd-122">Vzhledem k tomu, že v `<OnLoad>`může existovat pouze jedna animace, jsou tyto dvě `<Condition>` animace spojeny společně pomocí elementu `<Sequence>`:</span><span class="sxs-lookup"><span data-stu-id="475cd-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

<span data-ttu-id="475cd-123">Všimněte si, že znaménko menší než (`<`) v atributu `ConditionScript` musí mít řídicí znak ().</span><span class="sxs-lookup"><span data-stu-id="475cd-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="475cd-124">Spouštíte-li tento skript, buď žádná animace neběží, nebo jeden z těchto dvou testů nebo obojí.</span><span class="sxs-lookup"><span data-stu-id="475cd-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>

<span data-ttu-id="475cd-125">[![je panel bez změny velikosti, takže se druhá animace spustí, první z nich se nezměnila.](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="475cd-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span></span>

<span data-ttu-id="475cd-126">Panel se vypustil bez změny velikosti, takže se druhá animace spustí poprvé ([kliknutím zobrazíte obrázek v plné velikosti).](animation-depending-on-a-condition-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="475cd-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="475cd-127">[Předchozí](executing-several-animations-after-each-other-vb.md)
> [Další](picking-one-animation-out-of-a-list-vb.md)</span><span class="sxs-lookup"><span data-stu-id="475cd-127">[Previous](executing-several-animations-after-each-other-vb.md)
[Next](picking-one-animation-out-of-a-list-vb.md)</span></span>
