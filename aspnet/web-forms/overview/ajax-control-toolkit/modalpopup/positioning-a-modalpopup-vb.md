---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: Umístění ovládacího prvku modalpopup (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: fb79a08a339588ed8adc4b4236911819ea9286b4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598971"
---
# <a name="positioning-a-modalpopup-vb"></a><span data-ttu-id="8fc6a-104">Umístění ovládacího prvku ModalPopup (VB)</span><span class="sxs-lookup"><span data-stu-id="8fc6a-104">Positioning a ModalPopup (VB)</span></span>

<span data-ttu-id="8fc6a-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8fc6a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8fc6a-106">[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8fc6a-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span></span>

> <span data-ttu-id="8fc6a-107">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="8fc6a-108">Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-108">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="8fc6a-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="8fc6a-109">Overview</span></span>

<span data-ttu-id="8fc6a-110">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="8fc6a-111">Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="8fc6a-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="8fc6a-112">Steps</span></span>

<span data-ttu-id="8fc6a-113">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, `ScriptManager`.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="8fc6a-114">ovládací prvek musí být umístěn kdekoli na stránce (ale v prvku `<form>`):</span><span class="sxs-lookup"><span data-stu-id="8fc6a-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="8fc6a-115">Dále přidejte panel, který slouží jako modální automaticky otevírané okno.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="8fc6a-116">Tlačítko slouží k zavření automaticky otevíraného okna:</span><span class="sxs-lookup"><span data-stu-id="8fc6a-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="8fc6a-117">Pokaždé, když se zobrazí místní nabídka, je umístěna na určitém místě na stránce.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="8fc6a-118">Pro tuto úlohu je vytvořena funkce JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="8fc6a-119">Nejprve se pokusí o přístup k panelu.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-119">It first tries to access the panel.</span></span> <span data-ttu-id="8fc6a-120">V případě úspěchu se pozice panelu nastaví pomocí CSS a JavaScriptu (Změna pozice místní nabídky na).</span><span class="sxs-lookup"><span data-stu-id="8fc6a-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="8fc6a-121">`ModalPopupExtender` ovládací prvek se ale také pokusí umístit automaticky otevírané okno.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="8fc6a-122">Proto kód JavaScriptu opakovaně umístí automaticky otevírané okno, každou desetinu sekundy.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

<span data-ttu-id="8fc6a-123">Jak vidíte, návratová hodnota metody `setTimeout()` JavaScriptu je uložena v globální proměnné.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="8fc6a-124">To umožňuje zastavit opakované umístění místní nabídky na vyžádání pomocí `clearTimeout()` metody:</span><span class="sxs-lookup"><span data-stu-id="8fc6a-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

<span data-ttu-id="8fc6a-125">Vše, co zbývá udělat, je to, aby prohlížeč tyto funkce vyvolal, kdykoli to bude vhodné.</span><span class="sxs-lookup"><span data-stu-id="8fc6a-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="8fc6a-126">Funkce `movePanel()` JavaScriptu musí být volána při kliknutí na tlačítko, které aktivuje panel:</span><span class="sxs-lookup"><span data-stu-id="8fc6a-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

<span data-ttu-id="8fc6a-127">A funkce `stopMoving()` přijde do hry, když se zavře automaticky otevírané okno, může se aktivovat v ovládacím prvku `ModalPopupExtender`:</span><span class="sxs-lookup"><span data-stu-id="8fc6a-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]

<span data-ttu-id="8fc6a-128">[![modální překryvné okno se zobrazí na určené pozici.](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8fc6a-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="8fc6a-129">Modální místní nabídka se zobrazí na určené pozici ([kliknutím zobrazíte obrázek v plné velikosti).](positioning-a-modalpopup-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8fc6a-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8fc6a-130">Předchozí</span><span class="sxs-lookup"><span data-stu-id="8fc6a-130">Previous</span></span>](handling-postbacks-from-a-modalpopup-vb.md)
