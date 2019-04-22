---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: Zpracování postbacků extenderu Popupcontrol ovládacím prvkem UpdatePanel (VB) | Dokumentace Microsoftu
author: wenz
description: Zařízení extender PopupControl v sadou nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevíraného okna, když se aktivuje jiný ovládací prvek. Zvláštní pozornost je třeba vzít...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 3c4b58e864ca99aa30444fbb3244bfa4ffb4c336
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59379037"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a><span data-ttu-id="a3119-104">Zpracování postbacků ovládacího prvku PopupControl ovládacím prvkem UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="a3119-104">Handling Postbacks from A Popup Control With an UpdatePanel (VB)</span></span>

<span data-ttu-id="a3119-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a3119-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a3119-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a3119-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span></span>

> <span data-ttu-id="a3119-107">Zařízení extender PopupControl v sadou nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevíraného okna, když se aktivuje jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="a3119-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a3119-108">Zvláštní pozornost musí být provedeny, když dojde k takové rozbalené postbacku.</span><span class="sxs-lookup"><span data-stu-id="a3119-108">Special care has to be taken when a postback occurs within such a popup.</span></span>


## <a name="overview"></a><span data-ttu-id="a3119-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="a3119-109">Overview</span></span>

<span data-ttu-id="a3119-110">Zařízení extender PopupControl v sadou nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevíraného okna, když se aktivuje jiný ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="a3119-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a3119-111">Zvláštní pozornost musí být provedeny, když dojde k takové rozbalené postbacku.</span><span class="sxs-lookup"><span data-stu-id="a3119-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="a3119-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="a3119-112">Steps</span></span>

<span data-ttu-id="a3119-113">Při použití `PopupControl` s zpětné volání, `UpdatePanel` může zabránit aktualizace stránky způsobené zpětné volání.</span><span class="sxs-lookup"><span data-stu-id="a3119-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="a3119-114">Následující kód definuje několik důležité elementy:</span><span class="sxs-lookup"><span data-stu-id="a3119-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="a3119-115">A `ScriptManager` tak, aby funguje technologie ASP.NET AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="a3119-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="a3119-116">Dvě `TextBox` ovládací prvky, které aktivují obě automaticky otevíraného okna</span><span class="sxs-lookup"><span data-stu-id="a3119-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="a3119-117">A `Panel` ovládací prvek, který bude sloužit jako automaticky otevíraného okna</span><span class="sxs-lookup"><span data-stu-id="a3119-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="a3119-118">V rámci panelu `Calendar` ovládací prvek se vloží v rámci `UpdatePanel` ovládacího prvku</span><span class="sxs-lookup"><span data-stu-id="a3119-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="a3119-119">Dvě `PopupControlExtender` ovládací prvky, které přiřadit do textových polí panelu</span><span class="sxs-lookup"><span data-stu-id="a3119-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="a3119-120">Všimněte si, že `OnSelectionChanged` atribut `Calendar` nastavit ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="a3119-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="a3119-121">Takže když uživatel vybere datum v kalendáři, dojde k zpětné volání a metody na straně serveru `c1_SelectionChanged()` provádí.</span><span class="sxs-lookup"><span data-stu-id="a3119-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="a3119-122">V rámci této metody musí načíst aktuální datum a zapíše zpět do textového pole.</span><span class="sxs-lookup"><span data-stu-id="a3119-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="a3119-123">Syntaxe, která vypadá takto: Za prvé, proxy pro objekt `PopupControlExtender` na stránce je nutné vygenerovat.</span><span class="sxs-lookup"><span data-stu-id="a3119-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="a3119-124">ASP.NET AJAX Control Toolkit nabízí `GetProxyForCurrentPopup()` metody.</span><span class="sxs-lookup"><span data-stu-id="a3119-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="a3119-125">Objekt, vrátí tato metoda podporuje `Commit()` metodu, která odešle hodnotu zpět na ovládací prvek, který aktivuje místní nabídka (ne ovládací prvek, která aktivuje volání metody!).</span><span class="sxs-lookup"><span data-stu-id="a3119-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="a3119-126">Následující kód obsahuje vybrané datum jako argument pro `Commit()` metody způsobí kódu ke zpětnému zápisu vybraného data do textového pole:</span><span class="sxs-lookup"><span data-stu-id="a3119-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="a3119-127">Nyní pokaždé, když kliknete na datum kalendáře přidružené textového pole, se zobrazí vybrané datum vytvoření ovládacího prvku pro výběr data, která aktuálně najdete na počet webů.</span><span class="sxs-lookup"><span data-stu-id="a3119-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>


<span data-ttu-id="a3119-128">[![Když uživatel klikne do textového pole, zobrazí se v kalendáři](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a3119-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="a3119-129">Když uživatel klikne do textového pole, zobrazí se v kalendáři ([kliknutím ji zobrazíte obrázek v plné velikosti](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a3119-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span></span>


<span data-ttu-id="a3119-130">[![Kliknutím na datum umístí ho do textového pole](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="a3119-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="a3119-131">Kliknutím na datum umístí ho do textového pole ([kliknutím ji zobrazíte obrázek v plné velikosti](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="a3119-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a3119-132">[Předchozí](using-multiple-popup-controls-vb.md)
> [další](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a3119-132">[Previous](using-multiple-popup-controls-vb.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span></span>
