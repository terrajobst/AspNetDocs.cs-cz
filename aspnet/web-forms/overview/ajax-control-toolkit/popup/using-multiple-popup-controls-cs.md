---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: Použití několika překryvných ovládacíchC#prvků () | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Je také možné použít m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611665"
---
# <a name="using-multiple-popup-controls-c"></a><span data-ttu-id="ee9a8-104">Použití několika překryvných ovládacích prvků (C#)</span><span class="sxs-lookup"><span data-stu-id="ee9a8-104">Using Multiple Popup Controls (C#)</span></span>

<span data-ttu-id="ee9a8-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ee9a8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ee9a8-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ee9a8-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="ee9a8-107">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="ee9a8-108">Je také možné použít více než jeden ovládací prvek místní nabídky na jedné stránce.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="ee9a8-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="ee9a8-109">Overview</span></span>

<span data-ttu-id="ee9a8-110">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="ee9a8-111">Je také možné použít více než jeden ovládací prvek místní nabídky na jedné stránce.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="ee9a8-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="ee9a8-112">Steps</span></span>

<span data-ttu-id="ee9a8-113">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="ee9a8-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="ee9a8-114">Dále přidejte panel, který slouží jako místní nabídka.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="ee9a8-115">V aktuálním scénáři panel obsahuje ovládací prvek `Calendar`.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="ee9a8-116">Aby se zabránilo aktualizaci stránky způsobené postbacky v kalendáři, je panel umístěn v ovládacím prvku `UpdatePanel`:</span><span class="sxs-lookup"><span data-stu-id="ee9a8-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="ee9a8-117">Stránka obsahuje také dvě textová pole.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-117">The page also contains two text boxes.</span></span> <span data-ttu-id="ee9a8-118">Pro každé textové pole se po aktivaci textového pole zobrazí místní nabídka kalendáře.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="ee9a8-119">Teď rozšíříte každé ze dvou textových polí `PopupControlExtender`.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="ee9a8-120">Atribut `TargetControlID` poskytuje ID ovládacího prvku svázaného s ovládacím prvkem.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="ee9a8-121">Atribut `PopupControlID` obsahuje ID překryvného panelu.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="ee9a8-122">V takovém případě mají oba ovládací panely stejné panely, ale také je možné použít různé panely.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="ee9a8-123">Když teď kliknete na textové pole, zobrazí se pod polem kalendář, který vám umožní vybrat datum.</span><span class="sxs-lookup"><span data-stu-id="ee9a8-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="ee9a8-124">(Získání vybraného data zpět do textových polí bude pokryto v jiném kurzu.)</span><span class="sxs-lookup"><span data-stu-id="ee9a8-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="ee9a8-125">[![kalendáři se zobrazí, když uživatel klikne do textového pole.](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ee9a8-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="ee9a8-126">Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](using-multiple-popup-controls-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ee9a8-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ee9a8-127">Next</span><span class="sxs-lookup"><span data-stu-id="ee9a8-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
