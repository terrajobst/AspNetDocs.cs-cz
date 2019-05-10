---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: Dynamické řízení animací ovládacím prvkem UpdatePanel (VB) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Pro obsah...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 136e265f36a49a1d3ed41d2a998c395fd2c4fd32
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128731"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="882b0-104">Dynamické řízení animací ovládacím prvkem UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="882b0-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>

<span data-ttu-id="882b0-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="882b0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="882b0-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="882b0-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="882b0-107">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="882b0-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="882b0-108">Obsah prvku UpdatePanel existuje speciální rozšiřujícího objektu, která se spoléhá na rozhraní .NET framework animace: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="882b0-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="882b0-109">Můžete taky fungují společně s aktivačních událostí UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="882b0-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="882b0-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="882b0-110">Overview</span></span>

<span data-ttu-id="882b0-111">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="882b0-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="882b0-112">Pro obsah `UpdatePanel`, speciální rozšiřující objekt existuje, která se spoléhá na rozhraní .NET framework animace: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="882b0-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="882b0-113">Můžete také pracovat společně s `UpdatePanel` aktivační události.</span><span class="sxs-lookup"><span data-stu-id="882b0-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="882b0-114">Kroky</span><span class="sxs-lookup"><span data-stu-id="882b0-114">Steps</span></span>

<span data-ttu-id="882b0-115">Prvním krokem je jako obvykle zahrnují `ScriptManager` na stránce tak, aby je načtena knihovna ASP.NET AJAX a Control Toolkit je možné:</span><span class="sxs-lookup"><span data-stu-id="882b0-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="882b0-116">Animace v tomto scénáři se použijí k zobrazení aktuálního času.</span><span class="sxs-lookup"><span data-stu-id="882b0-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="882b0-117">Tyto informace lze zapsat do label using `Page_Load()` metodu, nebo (z důvodu zjednodušení) se používá následující vloženého kódu:</span><span class="sxs-lookup"><span data-stu-id="882b0-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="882b0-118">Kromě toho se vytvoří tlačítko aktivovat aktualizaci čas:</span><span class="sxs-lookup"><span data-stu-id="882b0-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="882b0-119">Tento kód pak přejde do `<ContentTemplate>` část `UpdatePanel` elementu.</span><span class="sxs-lookup"><span data-stu-id="882b0-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="882b0-120">Na panelu `UpdateMode` atribut musí být nastaven na `"Conditional"`, protože pouze aktivačních událostí může aktualizovat obsah panelu.</span><span class="sxs-lookup"><span data-stu-id="882b0-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="882b0-121">V `<Triggers>` část `UpdatePanel`, je vytvořen a vázané na aktivační událost asynchronní postback `Click` událost tlačítka.</span><span class="sxs-lookup"><span data-stu-id="882b0-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="882b0-122">Proto, když uživatel klikne na tlačítko, `UpdatePanel` je aktualizováno.</span><span class="sxs-lookup"><span data-stu-id="882b0-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="882b0-123">Tady je zápis `UpdatePanel` ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="882b0-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="882b0-124">Nakonec `UpdatePanelAnimationExtender` musí být nakonfigurované: Nastavte `TargetControlID` atribut ID panelu a definovat animace v rámci zařízení extender.</span><span class="sxs-lookup"><span data-stu-id="882b0-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="882b0-125">Pozvolného v díky smysl, která vytvoří nice visual důraz na čas aktualizace.</span><span class="sxs-lookup"><span data-stu-id="882b0-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="882b0-126">Vaše zařízení extender značky pak může vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="882b0-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="882b0-127">Spusťte soubor v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="882b0-127">Run the file in the browser.</span></span> <span data-ttu-id="882b0-128">Pokaždé, když kliknete na tlačítko, aktuální čas je uveden v panelu vždy pozvolného po dobu trvání jedné sekundy.</span><span class="sxs-lookup"><span data-stu-id="882b0-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="882b0-129">[![Aktuální čas je pozvolného](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="882b0-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="882b0-130">Aktuální čas je pozvolného ([kliknutím ji zobrazíte obrázek v plné velikosti](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="882b0-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="882b0-131">Předchozí</span><span class="sxs-lookup"><span data-stu-id="882b0-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
