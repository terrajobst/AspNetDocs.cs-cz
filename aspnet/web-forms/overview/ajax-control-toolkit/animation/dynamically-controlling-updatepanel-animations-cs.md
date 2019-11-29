---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: Dynamické řízení animací UpdatePanel (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606803"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="cafdc-104">Dynamické řízení animací ovládacím prvkem UpdatePanel (C#)</span><span class="sxs-lookup"><span data-stu-id="cafdc-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>

<span data-ttu-id="cafdc-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cafdc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cafdc-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="cafdc-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="cafdc-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="cafdc-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cafdc-108">Pro obsah ovládacího prvku UpdatePanel existuje speciální rozšířený objekt, který spoléhá na rámec animace: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="cafdc-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="cafdc-109">Může také spolupracovat s triggery UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="cafdc-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="cafdc-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="cafdc-110">Overview</span></span>

<span data-ttu-id="cafdc-111">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="cafdc-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cafdc-112">Pro obsah `UpdatePanel`existuje speciální rozšířený objekt, který spoléhá na rámec animace: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="cafdc-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="cafdc-113">Může taky spolupracovat s triggery `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="cafdc-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="cafdc-114">Uvedené</span><span class="sxs-lookup"><span data-stu-id="cafdc-114">Steps</span></span>

<span data-ttu-id="cafdc-115">Prvním krokem je obvykle zahrnutí `ScriptManager` do stránky, aby byla načtena knihovna ASP.NET AJAX a bylo možné použít ovládací sadu Toolkit:</span><span class="sxs-lookup"><span data-stu-id="cafdc-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="cafdc-116">Animace v tomto scénáři se použije na zobrazení aktuálního času.</span><span class="sxs-lookup"><span data-stu-id="cafdc-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="cafdc-117">Tyto informace lze zapsat do popisku pomocí `Page_Load()` metody, nebo (pro účely zjednodušení) je použit následující vložený kód:</span><span class="sxs-lookup"><span data-stu-id="cafdc-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="cafdc-118">Také tlačítko pro aktivaci aktualizace času je vytvořeno:</span><span class="sxs-lookup"><span data-stu-id="cafdc-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="cafdc-119">Tento kód je pak vložen do oddílu `<ContentTemplate>` `UpdatePanel` elementu.</span><span class="sxs-lookup"><span data-stu-id="cafdc-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="cafdc-120">Atribut `UpdateMode` panelu musí být nastaven na hodnotu `"Conditional"`, protože triggery mohou aktualizovat pouze triggery obsahu panelu.</span><span class="sxs-lookup"><span data-stu-id="cafdc-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="cafdc-121">V části `<Triggers>` `UpdatePanel`je vytvořen Trigger asynchronního postbacku a svázán s událostí `Click` tlačítka.</span><span class="sxs-lookup"><span data-stu-id="cafdc-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="cafdc-122">Proto pokud uživatel klikne na tlačítko, `UpdatePanel` se aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="cafdc-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="cafdc-123">Zde je značka pro ovládací prvek `UpdatePanel`:</span><span class="sxs-lookup"><span data-stu-id="cafdc-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="cafdc-124">Nakonec je třeba nakonfigurovat `UpdatePanelAnimationExtender`: nastavte atribut `TargetControlID` na ID panelu a definujte animaci v rámci tohoto zařízení.</span><span class="sxs-lookup"><span data-stu-id="cafdc-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="cafdc-125">Je to v dobrém smyslu, což na aktualizovaném čase vytvoří skvělé vizuální zdůraznění.</span><span class="sxs-lookup"><span data-stu-id="cafdc-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="cafdc-126">Značky zařízení může vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="cafdc-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="cafdc-127">Spusťte soubor v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="cafdc-127">Run the file in the browser.</span></span> <span data-ttu-id="cafdc-128">Kdykoliv kliknete na tlačítko, aktuální čas se zobrazí na panelu, vždy se bude zobrazovat po dobu trvání jedné sekundy.</span><span class="sxs-lookup"><span data-stu-id="cafdc-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="cafdc-129">[![aktuální čas je v čase](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cafdc-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="cafdc-130">Aktuální čas je v čase ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-controlling-updatepanel-animations-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="cafdc-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cafdc-131">[Předchozí](animating-an-updatepanel-control-cs.md)
> [Další](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cafdc-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>
