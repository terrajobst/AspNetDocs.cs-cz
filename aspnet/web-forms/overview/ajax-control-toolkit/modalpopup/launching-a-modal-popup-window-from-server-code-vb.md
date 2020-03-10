---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: Spuštění modálního překryvného okna ze serverového kódu (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Některé scénáře ale vyžadují tuto t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 1368a78d35ac6461bbc2e852e468f42eef2c0d2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613272"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a><span data-ttu-id="1627b-104">Spuštění okna modální místní nabídky serverovým kódem (VB)</span><span class="sxs-lookup"><span data-stu-id="1627b-104">Launching a Modal Popup Window from Server Code (VB)</span></span>

<span data-ttu-id="1627b-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1627b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1627b-106">[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1627b-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span></span>

> <span data-ttu-id="1627b-107">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="1627b-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="1627b-108">Některé scénáře však vyžadují, aby bylo otevření modální nabídky na straně serveru spuštěno.</span><span class="sxs-lookup"><span data-stu-id="1627b-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="1627b-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="1627b-109">Overview</span></span>

<span data-ttu-id="1627b-110">Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="1627b-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="1627b-111">Některé scénáře však vyžadují, aby bylo otevření modální nabídky na straně serveru spuštěno.</span><span class="sxs-lookup"><span data-stu-id="1627b-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="1627b-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="1627b-112">Steps</span></span>

<span data-ttu-id="1627b-113">Nejprve je třeba webový ovládací prvek ASP.NET tlačítka, který ukazuje, jak funguje ovládací prvek ovládacího prvku modalpopup.</span><span class="sxs-lookup"><span data-stu-id="1627b-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="1627b-114">Přidejte takové tlačítko do&gt; elementu &lt;formuláře na nové stránce:</span><span class="sxs-lookup"><span data-stu-id="1627b-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

<span data-ttu-id="1627b-115">Pak budete potřebovat označení pro místní nabídku, kterou chcete vytvořit.</span><span class="sxs-lookup"><span data-stu-id="1627b-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="1627b-116">Definujte ho jako ovládací prvek `<asp:Panel>` a ujistěte se, že obsahuje ovládací prvek tlačítko.</span><span class="sxs-lookup"><span data-stu-id="1627b-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="1627b-117">Ovládací prvek ovládacího prvku modalpopup nabízí funkci, aby toto tlačítko zavřelo překryvné okno; jinak neexistuje žádný snadný způsob, jak to umožnit, aby zmizel.</span><span class="sxs-lookup"><span data-stu-id="1627b-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

<span data-ttu-id="1627b-118">Dále přidejte ovládací prvek ovládacího prvku modalpopup z ASP.NET AJAX Toolkit na stránku.</span><span class="sxs-lookup"><span data-stu-id="1627b-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="1627b-119">Nastavte vlastnosti pro tlačítko, které načte ovládací prvek, tlačítko, které zmizí, a ID skutečné překryvné nabídky.</span><span class="sxs-lookup"><span data-stu-id="1627b-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

<span data-ttu-id="1627b-120">Stejně jako všechny webové stránky založené na ASP.NET AJAX; Správce skriptů je nutný k načtení nezbytných knihoven JavaScriptu pro různé cílové prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="1627b-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

<span data-ttu-id="1627b-121">Spusťte příklad v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="1627b-121">Run the example in the browser.</span></span> <span data-ttu-id="1627b-122">Po kliknutí na tlačítko se zobrazí modální okno.</span><span class="sxs-lookup"><span data-stu-id="1627b-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="1627b-123">Aby bylo možné dosáhnout stejného účinku pomocí kódu na straně serveru, je vyžadováno nové tlačítko:</span><span class="sxs-lookup"><span data-stu-id="1627b-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

<span data-ttu-id="1627b-124">Jak vidíte, kliknutí na tlačítko vygeneruje postback a spustí metodu `ServerButton_Click()` na serveru.</span><span class="sxs-lookup"><span data-stu-id="1627b-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="1627b-125">V této metodě je funkce JavaScriptu, která se nazývá `launchModal()`, prováděna přesně, funkce JavaScriptu se spustí po načtení stránky:</span><span class="sxs-lookup"><span data-stu-id="1627b-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

<span data-ttu-id="1627b-126">Úkolem `launchModal()` je zobrazit ovládacího prvku modalpopup.</span><span class="sxs-lookup"><span data-stu-id="1627b-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="1627b-127">Funkce `launchModal()` je provedena po načtení kompletní stránky HTML.</span><span class="sxs-lookup"><span data-stu-id="1627b-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="1627b-128">V tomto okamžiku ale rozhraní ASP.NET AJAX ještě není zcela načteno.</span><span class="sxs-lookup"><span data-stu-id="1627b-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="1627b-129">Proto funkce `launchModal()` pouze nastaví proměnnou, kterou musí být ovládací prvek ovládacího prvku modalpopup zobrazen později v:</span><span class="sxs-lookup"><span data-stu-id="1627b-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

<span data-ttu-id="1627b-130">Funkce `pageLoad()` JavaScriptu je speciální funkce, která se spustí po plném načtení ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="1627b-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="1627b-131">Proto přidáme kód do této funkce pro zobrazení ovládacího prvku ovládacího prvku modalpopup, ale pouze v případě, že byla volána `launchModal()` před:</span><span class="sxs-lookup"><span data-stu-id="1627b-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

<span data-ttu-id="1627b-132">Funkce `$find()` hledá pojmenovaný element na stránce a jako parametr očekává ID na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="1627b-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="1627b-133">Proto `$find("mpe")` vrátí reprezentaci klienta ovládacího prvku ovládacího prvku modalpopup; jeho metoda `show()` umožňuje zobrazit automaticky otevírané okno.</span><span class="sxs-lookup"><span data-stu-id="1627b-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="1627b-134">[![modálnímu překryvnému okně se zobrazí při kliknutí na jedno z tlačítek.](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1627b-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="1627b-135">Modální automaticky otevírané okno se zobrazí, když se klikne na jedno z tlačítek ([kliknutím zobrazíte obrázek v plné velikosti).](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1627b-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1627b-136">[Předchozí](positioning-a-modalpopup-cs.md)
> [Další](using-modalpopup-with-a-repeater-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1627b-136">[Previous](positioning-a-modalpopup-cs.md)
[Next](using-modalpopup-with-a-repeater-control-vb.md)</span></span>
