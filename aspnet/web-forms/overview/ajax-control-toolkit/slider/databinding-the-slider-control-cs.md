---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: Vazba ovládacího prvku posuvník (C#) | Microsoft Docs
author: wenz
description: Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Je možné vytvořit vazby aktuální Positio...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ef547573f17f3265ad72717d3d3bbc622fd6894e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553716"
---
# <a name="databinding-the-slider-control-c"></a><span data-ttu-id="e0a6a-104">Svázání posuvníku s daty (C#)</span><span class="sxs-lookup"><span data-stu-id="e0a6a-104">Databinding the Slider Control (C#)</span></span>

<span data-ttu-id="e0a6a-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e0a6a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e0a6a-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e0a6a-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span></span>

> <span data-ttu-id="e0a6a-107">Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="e0a6a-108">Je možné vytvořit navázání aktuální pozice posuvníku na jiný ovládací prvek ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="overview"></a><span data-ttu-id="e0a6a-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="e0a6a-109">Overview</span></span>

<span data-ttu-id="e0a6a-110">Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="e0a6a-111">Je možné vytvořit navázání aktuální pozice posuvníku na jiný ovládací prvek ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="e0a6a-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="e0a6a-112">Steps</span></span>

<span data-ttu-id="e0a6a-113">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="e0a6a-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

<span data-ttu-id="e0a6a-114">Dále do stránky přidejte dva ovládací prvky `TextBox`.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="e0a6a-115">Jedna z nich se transformuje na grafický posuvník a druhá bude mít polohu posuvníku.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

<span data-ttu-id="e0a6a-116">Dalším krokem je již poslední krok.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-116">The next step is already the final step.</span></span> <span data-ttu-id="e0a6a-117">Ovládací prvek `SliderExtender` z ASP.NET AJAX Control Toolkit vytvoří posuvník od prvního textového pole a při změně pozice posuvníku automaticky aktualizuje druhé textové pole.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="e0a6a-118">Aby to fungovalo, musí být atribut `SliderExtender``TargetControlID` nastaven na ID prvního textového pole; atribut `BoundControlID` musí být nastaven na ID druhého textového pole.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

<span data-ttu-id="e0a6a-119">Jak vidíte v prohlížeči, datová vazba funguje v obou směrech: zadání nové hodnoty do textového pole aktualizuje polohu posuvníku.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="e0a6a-120">Pokud nastavíte druhé textové pole jen pro čtení, můžete do textového pole přidat slabou ochranu, aby byl uživatel těžší ručně aktualizovat hodnotu v této části.</span><span class="sxs-lookup"><span data-stu-id="e0a6a-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>

<span data-ttu-id="e0a6a-121">[![posuvník a textové pole jsou synchronizované](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e0a6a-121">[![Slider and text box are in sync](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="e0a6a-122">Posuvník a textové pole jsou synchronizované ([kliknutím zobrazíte obrázek v plné velikosti).](databinding-the-slider-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e0a6a-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e0a6a-123">[Předchozí](using-the-slider-control-with-auto-postback-cs.md)
> [Další](using-the-slider-control-with-auto-postback-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e0a6a-123">[Previous](using-the-slider-control-with-auto-postback-cs.md)
[Next](using-the-slider-control-with-auto-postback-vb.md)</span></span>
