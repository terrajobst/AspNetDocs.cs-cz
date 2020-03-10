---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: Zpracování zpětného volání z překryvného ovládacího prvku bez prvku UpdatePanel (VB) | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Když dojde k postbacku v Su...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553982"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="a54c8-104">Zpracování postbacků ovládacího prvku PopupControl bez ovládacího prvku UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="a54c8-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="a54c8-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a54c8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a54c8-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a54c8-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="a54c8-107">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="a54c8-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a54c8-108">Pokud dojde k postbacku na takovém panelu a na stránce je několik panelů, je obtížné určit, na který panel byl kliknuto.</span><span class="sxs-lookup"><span data-stu-id="a54c8-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="a54c8-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="a54c8-109">Overview</span></span>

<span data-ttu-id="a54c8-110">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="a54c8-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a54c8-111">Pokud dojde k postbacku na takovém panelu a na stránce je několik panelů, je obtížné určit, na který panel byl kliknuto.</span><span class="sxs-lookup"><span data-stu-id="a54c8-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="a54c8-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="a54c8-112">Steps</span></span>

<span data-ttu-id="a54c8-113">Při použití `PopupControl` s zpětným voláním, ale bez `UpdatePanel` na stránce, sada nástrojů Control Toolkit nenabízí způsob, jak určit, který prvek klienta aktivoval automaticky otevírané okno, které způsobilo zpětné odeslání.</span><span class="sxs-lookup"><span data-stu-id="a54c8-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="a54c8-114">Malý štych ale poskytuje alternativní řešení pro tento scénář.</span><span class="sxs-lookup"><span data-stu-id="a54c8-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="a54c8-115">První ze všech, zde je základní nastavení: dvě textová pole, která obě spustí stejnou místní nabídku, kalendář.</span><span class="sxs-lookup"><span data-stu-id="a54c8-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="a54c8-116">Dva `PopupControlExtenders` přenášet textová pole a automaticky otevíraná okna.</span><span class="sxs-lookup"><span data-stu-id="a54c8-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="a54c8-117">Základní nápad je přidat skryté pole formuláře do &lt;`form`&gt; elementu, který obsahuje textové pole, ve kterém se spustila automaticky otevíraná okna:</span><span class="sxs-lookup"><span data-stu-id="a54c8-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="a54c8-118">Při načtení stránky kód JavaScriptu přidá obslužnou rutinu události do obou textových polí: vždy, když uživatel klikne na textové pole, jeho název se zapíše do skrytého pole formuláře:</span><span class="sxs-lookup"><span data-stu-id="a54c8-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="a54c8-119">V kódu na straně serveru musí být hodnota skrytého pole přečtena.</span><span class="sxs-lookup"><span data-stu-id="a54c8-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="a54c8-120">Vzhledem k tomu, že skrytá pole formuláře jsou triviální pro manipulaci, je požadován přístup povolený k ověření skryté hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a54c8-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="a54c8-121">Po identifikaci správného textového pole se do něj zapíše datum z kalendáře.</span><span class="sxs-lookup"><span data-stu-id="a54c8-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

<span data-ttu-id="a54c8-122">[![kalendáři se zobrazí, když uživatel klikne do textového pole.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a54c8-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="a54c8-123">Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a54c8-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="a54c8-124">[![kliknutí na datum vloží do textového pole.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="a54c8-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="a54c8-125">Kliknutím na datum se vloží do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="a54c8-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a54c8-126">Předchozí</span><span class="sxs-lookup"><span data-stu-id="a54c8-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
