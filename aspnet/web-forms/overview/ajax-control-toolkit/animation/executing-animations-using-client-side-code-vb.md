---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: Spouštění animací pomocí kódu na straně klienta (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Spuštění animace...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575489"
---
# <a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="1ad78-104">Spuštění animací klientským kódem (VB)</span><span class="sxs-lookup"><span data-stu-id="1ad78-104">Executing Animations Using Client-Side Code (VB)</span></span>

<span data-ttu-id="1ad78-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1ad78-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1ad78-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1ad78-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="1ad78-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="1ad78-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1ad78-108">Spuštění animace se může také aktivovat pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="1ad78-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="1ad78-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="1ad78-109">Overview</span></span>

<span data-ttu-id="1ad78-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="1ad78-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1ad78-111">Spuštění animace se může také aktivovat pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="1ad78-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="1ad78-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="1ad78-112">Steps</span></span>

<span data-ttu-id="1ad78-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="1ad78-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="1ad78-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="1ad78-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="1ad78-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="1ad78-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="1ad78-116">Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="1ad78-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="1ad78-117">V uzlu `<Animations>` pomocí `<OnClick>` spustit animace, jakmile uživatel klikne na panel.</span><span class="sxs-lookup"><span data-stu-id="1ad78-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="1ad78-118">Přidejte dvě animace, které se mají spustit paralelně:</span><span class="sxs-lookup"><span data-stu-id="1ad78-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="1ad78-119">Pro účely ukázky je tato animace (a jakákoli jiná animace vytvořená pomocí sady Control Toolkit) spouštěna pomocí kódu jazyka JavaScript po spuštění stránky.</span><span class="sxs-lookup"><span data-stu-id="1ad78-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="1ad78-120">Nejdřív potřebujeme přístup k ovládacímu prvku `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="1ad78-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="1ad78-121">Knihovna ASP.NET AJAX poskytuje funkci `$find()` pro tuto úlohu:</span><span class="sxs-lookup"><span data-stu-id="1ad78-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="1ad78-122">Ovládací prvek `AnimationExtender` zpřístupňuje bohatá rozhraní API, včetně metod s názvy shodnými s obslužnými rutinami událostí použitými v kódu XML: `OnClick()`, `OnLoad()`a tak dále.</span><span class="sxs-lookup"><span data-stu-id="1ad78-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="1ad78-123">Například volání metody `OnClick()` spustí animaci v rámci elementu `<OnClick>` ovládacího prvku `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="1ad78-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="1ad78-124">Zde je kompletní kód JavaScriptu na straně klienta, který emuluje kliknutí na panel po úplném načtení stránky, Všimněte si, že se používá název funkce `pageLoad()`, který je volán ASP.NET AJAX po načtení stránky a všech zahrnutých knihoven JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="1ad78-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

<span data-ttu-id="1ad78-125">[![se animace spustí hned bez kliknutí myší.](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1ad78-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="1ad78-126">Animace se spustí okamžitě bez kliknutí myší ([kliknutím zobrazíte obrázek v plné velikosti).](executing-animations-using-client-side-code-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1ad78-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ad78-127">[Předchozí](modifying-animations-from-the-server-side-vb.md)
> [Další](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1ad78-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
