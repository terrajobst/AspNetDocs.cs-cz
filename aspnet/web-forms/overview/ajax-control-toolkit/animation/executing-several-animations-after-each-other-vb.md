---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: Postupné provedení několika animací (VB) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Umožňuje spustit severa...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 53984f03cf01caab859f44fdc018b1598ed62def
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59383041"
---
# <a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="ad9d3-104">Postupné provedení několika animací (VB)</span><span class="sxs-lookup"><span data-stu-id="ad9d3-104">Executing Several Animations after Each Other (VB)</span></span>

<span data-ttu-id="ad9d3-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ad9d3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ad9d3-106">[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ad9d3-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="ad9d3-107">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ad9d3-108">Umožňuje spuštění několika animací jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-108">It allows to run several animations one after the other.</span></span>


## <a name="overview"></a><span data-ttu-id="ad9d3-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="ad9d3-109">Overview</span></span>

<span data-ttu-id="ad9d3-110">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ad9d3-111">Umožňuje spuštění několika animací jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="ad9d3-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="ad9d3-112">Steps</span></span>

<span data-ttu-id="ad9d3-113">Za prvé, zahrnout `ScriptManager` na stránce; potom technologie ASP.NET AJAX je načíst knihovnu, což umožňuje použití Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="ad9d3-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="ad9d3-114">Animace se použijí pro panel text, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="ad9d3-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="ad9d3-115">V přidružené třídy šablony stylů CSS pro panel definovat barvu pozadí nice a také nastavit Pevná šířka panelu:</span><span class="sxs-lookup"><span data-stu-id="ad9d3-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="ad9d3-116">Pak přidejte `AnimationExtender` na stránku, poskytování `ID`, `TargetControlID` atribut a povinný údaj `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="ad9d3-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="ad9d3-117">V rámci `<Animations>` uzlu, použijte `<OnLoad>` ke spuštění animací, jakmile úplným načtením stránky.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="ad9d3-118">Obecně platí `<OnLoad>` přijímá pouze jeden animace.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="ad9d3-119">Animace framework umožňuje připojit k několika animací do jednoho pomocí `<Sequence>` elementu.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="ad9d3-120">Všechny animace v rámci `<Sequence>` jsou spuštěný jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="ad9d3-121">Tady je možné značky `AnimationExtender` ovládací prvek, nejprve Příprava panelu širší a zmenšení výšku:</span><span class="sxs-lookup"><span data-stu-id="ad9d3-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="ad9d3-122">Při spuštění tohoto skriptu panelu první získá širší a potom menší.</span><span class="sxs-lookup"><span data-stu-id="ad9d3-122">When you run this script, the panel first gets wider and then smaller.</span></span>


<span data-ttu-id="ad9d3-123">[![Nejprve je vyšší šířku](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ad9d3-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="ad9d3-124">Nejprve je vyšší šířku ([kliknutím ji zobrazíte obrázek v plné velikosti](executing-several-animations-after-each-other-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ad9d3-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>


<span data-ttu-id="ad9d3-125">[![Pak je snížení výšky](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ad9d3-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="ad9d3-126">Pak se sníží výška ([kliknutím ji zobrazíte obrázek v plné velikosti](executing-several-animations-after-each-other-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ad9d3-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ad9d3-127">[Předchozí](executing-several-animations-at-the-same-time-vb.md)
> [další](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ad9d3-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
