---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: Změna animace pomocí kódu na straně klienta (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace může také...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598215"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="ac0a1-104">Změna animace klientským kódem (C#)</span><span class="sxs-lookup"><span data-stu-id="ac0a1-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="ac0a1-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ac0a1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ac0a1-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ac0a1-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="ac0a1-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ac0a1-108">Animaci lze také změnit pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-108">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="ac0a1-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="ac0a1-109">Overview</span></span>

<span data-ttu-id="ac0a1-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ac0a1-111">Animaci lze také změnit pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="ac0a1-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="ac0a1-112">Steps</span></span>

<span data-ttu-id="ac0a1-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="ac0a1-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="ac0a1-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="ac0a1-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="ac0a1-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="ac0a1-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="ac0a1-116">Skutečná animace se spustí tlačítkem HTML:</span><span class="sxs-lookup"><span data-stu-id="ac0a1-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="ac0a1-117">Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="ac0a1-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="ac0a1-118">Všimněte si, že v ovládacím prvku `AnimationExtender` není žádný `<Animations>` uzel.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="ac0a1-119">Vlastní kód JavaScriptu slouží k poskytnutí animací pro použití s ovládacím prvkem.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="ac0a1-120">Stejně jako u rozhraní API serveru `AnimationExtender`neexistuje jednoduchý způsob, jak přiřadit animaci k tomuto zařízení.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="ac0a1-121">Nicméně modul pro rozšiřování vystavuje několik metod pro čtení a zápis animací zaregistrovaných v různých událostech (`OnClick`, `OnLoad`a tak dále).</span><span class="sxs-lookup"><span data-stu-id="ac0a1-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="ac0a1-122">Zde je několik příkladů:</span><span class="sxs-lookup"><span data-stu-id="ac0a1-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="ac0a1-123">Formát návratové hodnoty funkcí `get_*()` a formát argumentu pro funkce `set_*()` je řetězec JSON, který poskytuje objekt reprezentující, co by byl kód XML.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="ac0a1-124">V současné době neexistuje způsob, jak objekt předat, ale je možné číst objekt z dané animace (`get_OnXXXBehavior()` metody).</span><span class="sxs-lookup"><span data-stu-id="ac0a1-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="ac0a1-125">Tady je řetězec JSON (bez uvozovek a formátovaného textu) představující animaci, která se aktivovala tlačítkem, ale animování panelu změnou velikosti a postupným postupným postupným navýšení.</span><span class="sxs-lookup"><span data-stu-id="ac0a1-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="ac0a1-126">Následující kód jazyka JavaScript přiřadí tento znak JSON ke `OnClick` animaci aktuálního a spustí ho:</span><span class="sxs-lookup"><span data-stu-id="ac0a1-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

<span data-ttu-id="ac0a1-127">[![se animace spouští okamžitě bez kliknutí myší (a s velmi malým označením).](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ac0a1-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="ac0a1-128">Animace se spustí okamžitě, bez kliknutí myší (a s velmi malým označením) ([kliknutím zobrazíte obrázek v plné velikosti).](changing-an-animation-using-client-side-code-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ac0a1-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ac0a1-129">[Předchozí](executing-animations-using-client-side-code-cs.md)
> [Další](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ac0a1-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
