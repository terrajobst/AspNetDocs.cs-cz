---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: Zpracování postbacků extenderu Popupcontrol bez ovládacího prvku UpdatePanel (VB) ovládacího | Dokumentace Microsoftu
author: wenz
description: Zařízení extender PopupControl v sadou nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevíraného okna, když se aktivuje jiný ovládací prvek. Zpětné volání při výskytu v su...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: c46f00c42f9b06d0224bcae03f51be8a73099974
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409340"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="6d9f7-104">Zpracování postbacků ovládacího prvku PopupControl bez ovládacího prvku UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="6d9f7-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="6d9f7-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6d9f7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6d9f7-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6d9f7-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="6d9f7-107">Zařízení extender PopupControl v sadou nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevíraného okna, když se aktivuje jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="6d9f7-108">Když zpětného odeslání dojde k takové panelu a na stránce se několika panely je obtížné určit, se kliklo panelu.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="6d9f7-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="6d9f7-109">Overview</span></span>

<span data-ttu-id="6d9f7-110">Zařízení extender PopupControl v sadou nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevíraného okna, když se aktivuje jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="6d9f7-111">Když zpětného odeslání dojde k takové panelu a na stránce se několika panely je obtížné určit, se kliklo panelu.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="6d9f7-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="6d9f7-112">Steps</span></span>

<span data-ttu-id="6d9f7-113">Při použití `PopupControl` s zpětné volání, ale bez nutnosti `UpdatePanel` na stránce Control Toolkit nenabízí způsob, jak určit, který klient prvek spustil automaticky otevírané okno, které pak způsobil zpětné volání.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="6d9f7-114">Ale triku poskytuje řešení pro tento scénář.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="6d9f7-115">Za prvé, tady je základní nastavení: dvě textová pole, které obě aktivovat stejné místní nabídky kalendář.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="6d9f7-116">Dvě `PopupControlExtenders` textová pole a automaticky otevírané okno pohromadě.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="6d9f7-117">Základní myšlenka spočívá v přidání skrytého pole v &lt; `form` &gt; element, který obsahuje textové pole, které spustí automaticky otevírané okno:</span><span class="sxs-lookup"><span data-stu-id="6d9f7-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="6d9f7-118">Při načtení stránky kódu jazyka JavaScript přidá obslužnou rutinu události do obou polí: Pokaždé, když uživatel klikne na textové pole, jeho název je zapsán do skryté pole formuláře:</span><span class="sxs-lookup"><span data-stu-id="6d9f7-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="6d9f7-119">V kódu na straně serveru musí přečíst hodnotu skrytého pole.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="6d9f7-120">Protože jsou triviální k manipulaci s skrytých polí ve formuláři, vyžaduje se seznamu povolených IP adres přístup k ověření skryté hodnoty.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="6d9f7-121">Jakmile byl identifikován správný textového pole, se do něj zapíše datum z kalendáře.</span><span class="sxs-lookup"><span data-stu-id="6d9f7-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]


[![T<span data-ttu-id="6d9f7-122">má kalendář se zobrazí, když uživatel klikne do textového pole]</span><span class="sxs-lookup"><span data-stu-id="6d9f7-122">he Calendar appears when the user clicks into the textbox]</span></span>(handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)

<span data-ttu-id="6d9f7-123">Když uživatel klikne do textového pole, zobrazí se v kalendáři ([kliknutím ji zobrazíte obrázek v plné velikosti](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6d9f7-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>


[![C<span data-ttu-id="6d9f7-124">licking k datu umístí ho do textového pole]</span><span class="sxs-lookup"><span data-stu-id="6d9f7-124">licking on a date puts it in the textbox]</span></span>(handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)

<span data-ttu-id="6d9f7-125">Kliknutím na datum umístí ho do textového pole ([kliknutím ji zobrazíte obrázek v plné velikosti](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6d9f7-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6d9f7-126">Předchozí</span><span class="sxs-lookup"><span data-stu-id="6d9f7-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
