---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: Sbalení a rozbalení panelu z JavaScriptu (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu možnost sbalení obsahu a jeho rozšíření...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599369"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a><span data-ttu-id="4d457-103">Sbalení a rozbalení panelu JavaScriptem (VB)</span><span class="sxs-lookup"><span data-stu-id="4d457-103">Collapsing and Expanding a Panel from JavaScript (VB)</span></span>

<span data-ttu-id="4d457-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4d457-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4d457-105">[Stažení kódu](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4d457-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span></span>

> <span data-ttu-id="4d457-106">Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu schopnost sbalit svůj obsah a znovu ho rozbalit.</span><span class="sxs-lookup"><span data-stu-id="4d457-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="4d457-107">Tyto dvě akce lze také aktivovat z vlastního kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="4d457-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="4d457-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="4d457-108">Overview</span></span>

<span data-ttu-id="4d457-109">Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu schopnost sbalit svůj obsah a znovu ho rozbalit.</span><span class="sxs-lookup"><span data-stu-id="4d457-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="4d457-110">Tyto dvě akce lze také aktivovat z vlastního kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="4d457-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="4d457-111">Uvedené</span><span class="sxs-lookup"><span data-stu-id="4d457-111">Steps</span></span>

<span data-ttu-id="4d457-112">Nejprve vytvořte novou stránku ASP.NET a zahrňte `ScriptManager` do jednoho `<form>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4d457-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="4d457-113">Načte knihovnu ASP.NET AJAX, která je požadována pro sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="4d457-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="4d457-114">Pak vytvořte panel s nějakým textem, aby bylo možné zobrazit efekt sbalení/rozbalení:</span><span class="sxs-lookup"><span data-stu-id="4d457-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="4d457-115">Jak vidíte, panel odkazuje na třídu šablony stylů CSS, která je zde zobrazena (a v podstatě definuje barvu pozadí a šířku panelu):</span><span class="sxs-lookup"><span data-stu-id="4d457-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

<span data-ttu-id="4d457-116">Ovládací prvek `CollapsiblePanelExtender` vyžaduje atribut `TargetControlID`, aby sada nástrojů věděla, který panel má sbalit nebo rozbalit na vyžádání:</span><span class="sxs-lookup"><span data-stu-id="4d457-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

<span data-ttu-id="4d457-117">V současné době bohužel rozšíření nezveřejňuje konkrétní rozhraní API pro sbalení nebo rozbalení panelu, ale některé nedokumentované metody budou dělat.</span><span class="sxs-lookup"><span data-stu-id="4d457-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="4d457-118">Nejprve na stránku přidejte tři tlačítka HTML, která pak spustí JavaScript na straně klienta pro sbalení nebo rozbalení obsahu panelu:</span><span class="sxs-lookup"><span data-stu-id="4d457-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="4d457-119">V kódu JavaScriptu na straně klienta (spuštěný s `<script type="text/javascript">`) je nutné použít metodu `$find()` pro přístup k `CollapsiblePanelExtender`.</span><span class="sxs-lookup"><span data-stu-id="4d457-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="4d457-120">`$find("cpe")` vrátí odkaz na něj.</span><span class="sxs-lookup"><span data-stu-id="4d457-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="4d457-121">V takovém případě vyřeší konkrétní metody úkol na ruce.</span><span class="sxs-lookup"><span data-stu-id="4d457-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="4d457-122">Metoda pro otevření (rozšíření) panel se nazývá `_doOpen()`; Následující kód implementuje funkci `doOpen()` volanou při kliknutí na první tlačítko:</span><span class="sxs-lookup"><span data-stu-id="4d457-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

<span data-ttu-id="4d457-123">Pro zavření nebo sbalení panelu musí být spuštěna metoda `_doClose()`.</span><span class="sxs-lookup"><span data-stu-id="4d457-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="4d457-124">Takže když uživatel klikne na druhé tlačítko, volá se následující JavaScriptový kód:</span><span class="sxs-lookup"><span data-stu-id="4d457-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

<span data-ttu-id="4d457-125">Třetí tlačítko přepíná stav panelu: ze sbalené na rozbalené a naopak.</span><span class="sxs-lookup"><span data-stu-id="4d457-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="4d457-126">`CollapsiblePanelExtender` zpřístupňuje metodu `toggle()`, která přesně používá: vrátí stav panelu.</span><span class="sxs-lookup"><span data-stu-id="4d457-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="4d457-127">Existuje však i další přístup (který je interně používán metodou `toggle()`): `get_Collapsed()` metoda `CollapsiblePanelExtender()` oznamuje, zda je panel sbalený nebo nikoli.</span><span class="sxs-lookup"><span data-stu-id="4d457-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="4d457-128">V závislosti na vrácené hodnotě této funkce je panel pak buď rozbalený (`_doOpen()` metoda) nebo sbalená (`_doClose()`) metoda:</span><span class="sxs-lookup"><span data-stu-id="4d457-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

<span data-ttu-id="4d457-129">[![třetí tlačítko změní stav panelu: ze sbalené na rozbalené a zpátky](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4d457-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="4d457-130">Třetí tlačítko změní stav panelu: ze sbaleného na rozšířené a zpět ([kliknutím zobrazíte obrázek v plné velikosti](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="4d457-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4d457-131">Předchozí</span><span class="sxs-lookup"><span data-stu-id="4d457-131">Previous</span></span>](collapsing-and-expanding-a-panel-from-javascript-cs.md)
