---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: Výběr jedné animace ze seznamu (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Rozhraní také lze povolit...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2bc203d694792716bbf4f7d7b8d152c589bf99b1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597970"
---
# <a name="picking-one-animation-out-of-a-list-c"></a><span data-ttu-id="78ab6-104">Výběr jedné animace ze seznamu (C#)</span><span class="sxs-lookup"><span data-stu-id="78ab6-104">Picking One Animation Out Of a List (C#)</span></span>

<span data-ttu-id="78ab6-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="78ab6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="78ab6-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="78ab6-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span></span>

> <span data-ttu-id="78ab6-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="78ab6-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="78ab6-108">Rozhraní také umožňuje programátorovi vybrat jednu animaci ze seznamu animací v závislosti na vyhodnocení kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="78ab6-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="78ab6-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="78ab6-109">Overview</span></span>

<span data-ttu-id="78ab6-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="78ab6-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="78ab6-111">Rozhraní také umožňuje programátorovi vybrat jednu animaci ze seznamu animací v závislosti na vyhodnocení kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="78ab6-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="78ab6-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="78ab6-112">Steps</span></span>

<span data-ttu-id="78ab6-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="78ab6-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

<span data-ttu-id="78ab6-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="78ab6-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

<span data-ttu-id="78ab6-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="78ab6-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

<span data-ttu-id="78ab6-116">Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="78ab6-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

<span data-ttu-id="78ab6-117">V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla.</span><span class="sxs-lookup"><span data-stu-id="78ab6-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="78ab6-118">Místo jedné z běžných animací se `<Case>` element přesune do hry.</span><span class="sxs-lookup"><span data-stu-id="78ab6-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="78ab6-119">Hodnota jeho atributu SelectScript je vyhodnocena. Vrácená hodnota musí být číselná.</span><span class="sxs-lookup"><span data-stu-id="78ab6-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="78ab6-120">V závislosti na tomto počtu se spustí jedna z podanimačních animací v &lt;případu&gt;.</span><span class="sxs-lookup"><span data-stu-id="78ab6-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="78ab6-121">Pokud je například SelectScript vyhodnocena jako 2, sada nástrojů Control Toolkit spustí třetí animaci v &lt;případu&gt; (počítání začíná 0).</span><span class="sxs-lookup"><span data-stu-id="78ab6-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="78ab6-122">Následující kód definuje tři podanimace: mění velikost šířky, mění velikost výšky a slábnutí. Kód jazyka JavaScript (`Math.floor(3 * Math.random())`) pak vybere číslo mezi 0 a 2, aby se spouštěla jedna ze tří animací:</span><span class="sxs-lookup"><span data-stu-id="78ab6-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

<span data-ttu-id="78ab6-123">[![jeden z možných tří animací: panel bude širší](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="78ab6-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span></span>

<span data-ttu-id="78ab6-124">Jedním z možných tří animací: panel bude širší ([kliknutím zobrazíte obrázek v plné velikosti](picking-one-animation-out-of-a-list-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="78ab6-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="78ab6-125">[Předchozí](animation-depending-on-a-condition-cs.md)
> [Další](animating-in-response-to-user-interaction-cs.md)</span><span class="sxs-lookup"><span data-stu-id="78ab6-125">[Previous](animation-depending-on-a-condition-cs.md)
[Next](animating-in-response-to-user-interaction-cs.md)</span></span>
