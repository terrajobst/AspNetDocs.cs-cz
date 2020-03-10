---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: Zpracování zpětných volání z ovládacího prvku modalpopup (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Zvláštní péči je potřeba vzít v případě POS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621525"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="27e25-104">Zpracování postbacků z ovládacího prvku ModalPopup (VB)</span><span class="sxs-lookup"><span data-stu-id="27e25-104">Handling Postbacks from a ModalPopup (VB)</span></span>

<span data-ttu-id="27e25-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="27e25-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="27e25-106">[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="27e25-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="27e25-107">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="27e25-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="27e25-108">Při vytváření zpětného volání z místní nabídky je potřeba věnovat zvláštní péči.</span><span class="sxs-lookup"><span data-stu-id="27e25-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="27e25-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="27e25-109">Overview</span></span>

<span data-ttu-id="27e25-110">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="27e25-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="27e25-111">Při vytváření zpětného volání z místní nabídky je potřeba věnovat zvláštní péči.</span><span class="sxs-lookup"><span data-stu-id="27e25-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="27e25-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="27e25-112">Steps</span></span>

<span data-ttu-id="27e25-113">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="27e25-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="27e25-114">Dále přidejte panel, který slouží jako modální automaticky otevírané okno.</span><span class="sxs-lookup"><span data-stu-id="27e25-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="27e25-115">Tam může uživatel zadat jméno a e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="27e25-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="27e25-116">Tlačítko slouží k zavření automaticky otevíraného okna a uložení informací.</span><span class="sxs-lookup"><span data-stu-id="27e25-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="27e25-117">Všimněte si, že atribut `OnClick` je nastaven tak, aby při kliknutí na toto tlačítko vznikl postback:</span><span class="sxs-lookup"><span data-stu-id="27e25-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="27e25-118">Samotná stránka se skládá ze dvou popisků pro přesně stejné informace: jméno a e-mailová adresa.</span><span class="sxs-lookup"><span data-stu-id="27e25-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="27e25-119">Tlačítko slouží k aktivaci modální překryvné nabídky:</span><span class="sxs-lookup"><span data-stu-id="27e25-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="27e25-120">Chcete-li, aby se místní nabídka zobrazila, přidejte ovládací prvek `ModalPopupExtender`.</span><span class="sxs-lookup"><span data-stu-id="27e25-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="27e25-121">Nastavte atribut `PopupControlID` na ID panelu a `TargetControlID` na ID tlačítka:</span><span class="sxs-lookup"><span data-stu-id="27e25-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="27e25-122">Nyní, když se klikne na tlačítko `Save` v modálním překryvném okně, je provedena metoda `SaveData()` na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="27e25-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="27e25-123">V takovém případě můžete zadaná data uložit do úložiště dat.</span><span class="sxs-lookup"><span data-stu-id="27e25-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="27e25-124">V zájmu jednoduchosti jsou nová data pouze výstupem v popisku:</span><span class="sxs-lookup"><span data-stu-id="27e25-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="27e25-125">Také ovládací prvky TextBox v modálním překryvném okně by měly být vyplněny aktuálním jménem a e-mailem.</span><span class="sxs-lookup"><span data-stu-id="27e25-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="27e25-126">To je však nutné pouze v případě, že nedojde k postbacku.</span><span class="sxs-lookup"><span data-stu-id="27e25-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="27e25-127">Pokud dojde k postbacku, funkce ASP.NET ViewState automaticky vyplní textová pole odpovídajícími hodnotami.</span><span class="sxs-lookup"><span data-stu-id="27e25-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

<span data-ttu-id="27e25-128">[![modálního automaticky otevíraného okna způsobí postback.](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="27e25-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="27e25-129">Modální překryvné okno způsobí postback ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-modalpopup-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="27e25-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="27e25-130">[Předchozí](using-modalpopup-with-a-repeater-control-vb.md)
> [Další](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="27e25-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>
