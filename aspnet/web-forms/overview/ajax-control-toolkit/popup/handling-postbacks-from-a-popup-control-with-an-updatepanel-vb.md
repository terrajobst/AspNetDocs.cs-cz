---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: Zpracování zpětného volání z překryvného ovládacího prvku s ovládacím prvkem UpdatePanel (VB) | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Zvláštní péče je nutné vzít v potaz...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: dd045ae56696c7944df98cf805ba812fde1bb4ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612894"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a><span data-ttu-id="c688b-104">Zpracování postbacků ovládacího prvku PopupControl ovládacím prvkem UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="c688b-104">Handling Postbacks from A Popup Control With an UpdatePanel (VB)</span></span>

<span data-ttu-id="c688b-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c688b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c688b-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c688b-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span></span>

> <span data-ttu-id="c688b-107">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="c688b-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="c688b-108">Zvláštní péči je nutné provést, pokud dojde k postbacku v takovém překryvném okně.</span><span class="sxs-lookup"><span data-stu-id="c688b-108">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="overview"></a><span data-ttu-id="c688b-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="c688b-109">Overview</span></span>

<span data-ttu-id="c688b-110">PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="c688b-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="c688b-111">Zvláštní péči je nutné provést, pokud dojde k postbacku v takovém překryvném okně.</span><span class="sxs-lookup"><span data-stu-id="c688b-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="c688b-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="c688b-112">Steps</span></span>

<span data-ttu-id="c688b-113">Při použití `PopupControl` s postbackem může `UpdatePanel` zabránit aktualizaci stránky způsobenou postbackem.</span><span class="sxs-lookup"><span data-stu-id="c688b-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="c688b-114">Následující kód definuje několik důležitých prvků:</span><span class="sxs-lookup"><span data-stu-id="c688b-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="c688b-115">Ovládací prvek `ScriptManager`, aby sada nástrojů ASP.NET AJAX Control</span><span class="sxs-lookup"><span data-stu-id="c688b-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="c688b-116">Dva `TextBox` ovládací prvky, které spustí místní nabídku</span><span class="sxs-lookup"><span data-stu-id="c688b-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="c688b-117">Ovládací prvek `Panel`, který bude sloužit jako místní nabídka</span><span class="sxs-lookup"><span data-stu-id="c688b-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="c688b-118">V rámci tohoto panelu je ovládací prvek `Calendar` vložený v rámci ovládacího prvku `UpdatePanel`</span><span class="sxs-lookup"><span data-stu-id="c688b-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="c688b-119">Dva `PopupControlExtender` ovládací prvky, které přiřadí panel k textovým polím</span><span class="sxs-lookup"><span data-stu-id="c688b-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="c688b-120">Všimněte si, že atribut `OnSelectionChanged` ovládacího prvku `Calendar` je nastaven.</span><span class="sxs-lookup"><span data-stu-id="c688b-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="c688b-121">Takže když uživatel vybere datum v kalendáři, dojde k postbacku a spustí se `c1_SelectionChanged()` metoda na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="c688b-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="c688b-122">V rámci této metody musí být aktuální datum načteno a zapsáno zpět do textového pole.</span><span class="sxs-lookup"><span data-stu-id="c688b-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="c688b-123">Tato syntaxe je následující: první ze všech musí být vygenerován objekt proxy pro `PopupControlExtender` na stránce.</span><span class="sxs-lookup"><span data-stu-id="c688b-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="c688b-124">ASP.NET AJAX Control Toolkit nabízí metodu `GetProxyForCurrentPopup()`.</span><span class="sxs-lookup"><span data-stu-id="c688b-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="c688b-125">Objekt, který vrací tato metoda, podporuje metodu `Commit()`, která pošle hodnotu zpět do ovládacího prvku, který aktivoval místní nabídku (nikoli ovládací prvek, který aktivoval volání metody!).</span><span class="sxs-lookup"><span data-stu-id="c688b-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="c688b-126">Následující kód poskytuje vybrané datum jako argument metody `Commit()`, což způsobí, že kód zapíše vybrané datum zpět do textového pole:</span><span class="sxs-lookup"><span data-stu-id="c688b-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="c688b-127">Když teď kliknete na datum kalendáře, zobrazí se vybrané datum v přidruženém textovém poli a vytvoří se ovládací prvek pro výběr data, který se teď dá najít na mnoha webech.</span><span class="sxs-lookup"><span data-stu-id="c688b-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>

<span data-ttu-id="c688b-128">[![kalendáři se zobrazí, když uživatel klikne do textového pole.](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c688b-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="c688b-129">Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c688b-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="c688b-130">[![kliknutí na datum vloží do textového pole.](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c688b-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="c688b-131">Kliknutím na datum se vloží do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="c688b-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c688b-132">[Předchozí](using-multiple-popup-controls-vb.md)
> [Další](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c688b-132">[Previous](using-multiple-popup-controls-vb.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span></span>
