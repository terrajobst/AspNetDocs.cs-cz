---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: Použití několika překryvných ovládacích prvků (VB) | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Je také možné použít m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: e1f4ff64e9fdf48ea63b75c97acd53a64b5ab5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612530"
---
# <a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="3756d-104">Použití několika překryvných ovládacích prvků (VB)</span><span class="sxs-lookup"><span data-stu-id="3756d-104">Using Multiple Popup Controls (VB)</span></span>

<span data-ttu-id="3756d-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3756d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3756d-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="3756d-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="3756d-107">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="3756d-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="3756d-108">Je také možné použít více než jeden ovládací prvek místní nabídky na jedné stránce.</span><span class="sxs-lookup"><span data-stu-id="3756d-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="3756d-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="3756d-109">Overview</span></span>

<span data-ttu-id="3756d-110">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="3756d-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="3756d-111">Je také možné použít více než jeden ovládací prvek místní nabídky na jedné stránce.</span><span class="sxs-lookup"><span data-stu-id="3756d-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="3756d-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="3756d-112">Steps</span></span>

<span data-ttu-id="3756d-113">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="3756d-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="3756d-114">Dále přidejte panel, který slouží jako místní nabídka.</span><span class="sxs-lookup"><span data-stu-id="3756d-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="3756d-115">V aktuálním scénáři panel obsahuje ovládací prvek `Calendar`.</span><span class="sxs-lookup"><span data-stu-id="3756d-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="3756d-116">Aby se zabránilo aktualizaci stránky způsobené postbacky v kalendáři, je panel umístěn v ovládacím prvku `UpdatePanel`:</span><span class="sxs-lookup"><span data-stu-id="3756d-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="3756d-117">Stránka obsahuje také dvě textová pole.</span><span class="sxs-lookup"><span data-stu-id="3756d-117">The page also contains two text boxes.</span></span> <span data-ttu-id="3756d-118">Pro každé textové pole se po aktivaci textového pole zobrazí místní nabídka kalendáře.</span><span class="sxs-lookup"><span data-stu-id="3756d-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="3756d-119">Teď rozšíříte každé ze dvou textových polí `PopupControlExtender`.</span><span class="sxs-lookup"><span data-stu-id="3756d-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="3756d-120">Atribut `TargetControlID` poskytuje ID ovládacího prvku svázaného s ovládacím prvkem.</span><span class="sxs-lookup"><span data-stu-id="3756d-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="3756d-121">Atribut `PopupControlID` obsahuje ID překryvného panelu.</span><span class="sxs-lookup"><span data-stu-id="3756d-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="3756d-122">V takovém případě mají oba ovládací panely stejné panely, ale také je možné použít různé panely.</span><span class="sxs-lookup"><span data-stu-id="3756d-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="3756d-123">Když teď kliknete na textové pole, zobrazí se pod polem kalendář, který vám umožní vybrat datum.</span><span class="sxs-lookup"><span data-stu-id="3756d-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="3756d-124">(Získání vybraného data zpět do textových polí bude pokryto v jiném kurzu.)</span><span class="sxs-lookup"><span data-stu-id="3756d-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="3756d-125">[![kalendáři se zobrazí, když uživatel klikne do textového pole.](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3756d-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="3756d-126">Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](using-multiple-popup-controls-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3756d-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3756d-127">[Předchozí](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [Další](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3756d-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
