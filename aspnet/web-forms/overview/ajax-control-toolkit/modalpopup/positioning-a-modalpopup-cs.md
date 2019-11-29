---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: Umístění ovládacího prvku modalpopup (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599027"
---
# <a name="positioning-a-modalpopup-c"></a><span data-ttu-id="2cfdc-104">Umístění ovládacího prvku ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="2cfdc-104">Positioning a ModalPopup (C#)</span></span>

<span data-ttu-id="2cfdc-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2cfdc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2cfdc-106">[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="2cfdc-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span></span>

> <span data-ttu-id="2cfdc-107">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="2cfdc-108">Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-108">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="2cfdc-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="2cfdc-109">Overview</span></span>

<span data-ttu-id="2cfdc-110">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="2cfdc-111">Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="2cfdc-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="2cfdc-112">Steps</span></span>

<span data-ttu-id="2cfdc-113">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, `ScriptManager`.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="2cfdc-114">ovládací prvek musí být umístěn kdekoli na stránce (ale v prvku `<form>`):</span><span class="sxs-lookup"><span data-stu-id="2cfdc-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="2cfdc-115">Dále přidejte panel, který slouží jako modální automaticky otevírané okno.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="2cfdc-116">Tlačítko slouží k zavření automaticky otevíraného okna:</span><span class="sxs-lookup"><span data-stu-id="2cfdc-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="2cfdc-117">Pokaždé, když se zobrazí místní nabídka, je umístěna na určitém místě na stránce.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="2cfdc-118">Pro tuto úlohu je vytvořena funkce JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="2cfdc-119">Nejprve se pokusí o přístup k panelu.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-119">It first tries to access the panel.</span></span> <span data-ttu-id="2cfdc-120">V případě úspěchu se pozice panelu nastaví pomocí CSS a JavaScriptu (Změna pozice místní nabídky na).</span><span class="sxs-lookup"><span data-stu-id="2cfdc-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="2cfdc-121">`ModalPopupExtender` ovládací prvek se ale také pokusí umístit automaticky otevírané okno.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="2cfdc-122">Proto kód JavaScriptu opakovaně umístí automaticky otevírané okno, každou desetinu sekundy.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

<span data-ttu-id="2cfdc-123">Jak vidíte, návratová hodnota metody `setTimeout()` JavaScriptu je uložena v globální proměnné.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="2cfdc-124">To umožňuje zastavit opakované umístění místní nabídky na vyžádání pomocí `clearTimeout()` metody:</span><span class="sxs-lookup"><span data-stu-id="2cfdc-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

<span data-ttu-id="2cfdc-125">Vše, co zbývá udělat, je to, aby prohlížeč tyto funkce vyvolal, kdykoli to bude vhodné.</span><span class="sxs-lookup"><span data-stu-id="2cfdc-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="2cfdc-126">Funkce `movePanel()` JavaScriptu musí být volána při kliknutí na tlačítko, které aktivuje panel:</span><span class="sxs-lookup"><span data-stu-id="2cfdc-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

<span data-ttu-id="2cfdc-127">A funkce `stopMoving()` přijde do hry, když se zavře automaticky otevírané okno, může se aktivovat v ovládacím prvku `ModalPopupExtender`:</span><span class="sxs-lookup"><span data-stu-id="2cfdc-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

<span data-ttu-id="2cfdc-128">[![modální překryvné okno se zobrazí na určené pozici.](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2cfdc-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="2cfdc-129">Modální místní nabídka se zobrazí na určené pozici ([kliknutím zobrazíte obrázek v plné velikosti).](positioning-a-modalpopup-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2cfdc-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2cfdc-130">[Předchozí](handling-postbacks-from-a-modalpopup-cs.md)
> [Další](launching-a-modal-popup-window-from-server-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2cfdc-130">[Previous](handling-postbacks-from-a-modalpopup-cs.md)
[Next](launching-a-modal-popup-window-from-server-code-vb.md)</span></span>
