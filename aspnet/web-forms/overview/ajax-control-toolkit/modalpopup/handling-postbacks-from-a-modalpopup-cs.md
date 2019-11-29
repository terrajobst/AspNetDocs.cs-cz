---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: Zpracování zpětného odeslání z ovládacího prvku modalpopup (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Zvláštní péči je potřeba vzít v případě POS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599101"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a><span data-ttu-id="703ab-104">Zpracování postbacků z ovládacího prvku ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="703ab-104">Handling Postbacks from a ModalPopup (C#)</span></span>

<span data-ttu-id="703ab-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="703ab-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="703ab-106">[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="703ab-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span></span>

> <span data-ttu-id="703ab-107">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="703ab-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="703ab-108">Při vytváření zpětného volání z místní nabídky je potřeba věnovat zvláštní péči.</span><span class="sxs-lookup"><span data-stu-id="703ab-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="703ab-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="703ab-109">Overview</span></span>

<span data-ttu-id="703ab-110">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="703ab-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="703ab-111">Při vytváření zpětného volání z místní nabídky je potřeba věnovat zvláštní péči.</span><span class="sxs-lookup"><span data-stu-id="703ab-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="703ab-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="703ab-112">Steps</span></span>

<span data-ttu-id="703ab-113">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="703ab-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="703ab-114">Dále přidejte panel, který slouží jako modální automaticky otevírané okno.</span><span class="sxs-lookup"><span data-stu-id="703ab-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="703ab-115">Tam může uživatel zadat jméno a e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="703ab-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="703ab-116">Tlačítko slouží k zavření automaticky otevíraného okna a uložení informací.</span><span class="sxs-lookup"><span data-stu-id="703ab-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="703ab-117">Všimněte si, že atribut `OnClick` je nastaven tak, aby při kliknutí na toto tlačítko vznikl postback:</span><span class="sxs-lookup"><span data-stu-id="703ab-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="703ab-118">Samotná stránka se skládá ze dvou popisků pro přesně stejné informace: jméno a e-mailová adresa.</span><span class="sxs-lookup"><span data-stu-id="703ab-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="703ab-119">Tlačítko slouží k aktivaci modální překryvné nabídky:</span><span class="sxs-lookup"><span data-stu-id="703ab-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

<span data-ttu-id="703ab-120">Chcete-li, aby se místní nabídka zobrazila, přidejte ovládací prvek `ModalPopupExtender`.</span><span class="sxs-lookup"><span data-stu-id="703ab-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="703ab-121">Nastavte atribut `PopupControlID` na ID panelu a `TargetControlID` na ID tlačítka:</span><span class="sxs-lookup"><span data-stu-id="703ab-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

<span data-ttu-id="703ab-122">Nyní, když se klikne na tlačítko `Save` v modálním překryvném okně, je provedena metoda `SaveData()` na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="703ab-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="703ab-123">V takovém případě můžete zadaná data uložit do úložiště dat.</span><span class="sxs-lookup"><span data-stu-id="703ab-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="703ab-124">V zájmu jednoduchosti jsou nová data pouze výstupem v popisku:</span><span class="sxs-lookup"><span data-stu-id="703ab-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

<span data-ttu-id="703ab-125">Také ovládací prvky TextBox v modálním překryvném okně by měly být vyplněny aktuálním jménem a e-mailem.</span><span class="sxs-lookup"><span data-stu-id="703ab-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="703ab-126">To je však nutné pouze v případě, že nedojde k postbacku.</span><span class="sxs-lookup"><span data-stu-id="703ab-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="703ab-127">Pokud dojde k postbacku, funkce ASP.NET ViewState automaticky vyplní textová pole odpovídajícími hodnotami.</span><span class="sxs-lookup"><span data-stu-id="703ab-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

<span data-ttu-id="703ab-128">[![modálního automaticky otevíraného okna způsobí postback.](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="703ab-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="703ab-129">Modální překryvné okno způsobí postback ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-modalpopup-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="703ab-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="703ab-130">[Předchozí](using-modalpopup-with-a-repeater-control-cs.md)
> [Další](positioning-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="703ab-130">[Previous](using-modalpopup-with-a-repeater-control-cs.md)
[Next](positioning-a-modalpopup-cs.md)</span></span>
