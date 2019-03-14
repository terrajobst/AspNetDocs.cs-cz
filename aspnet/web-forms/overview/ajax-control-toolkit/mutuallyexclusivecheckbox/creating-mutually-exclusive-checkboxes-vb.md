---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Vytvoření vzájemně se vylučujících zaškrtávacích políček (VB) | Dokumentace Microsoftu
author: wenz
description: 'Když je možné vybrat jenom jednu sadu možností, přepínače se obvykle používají. Existuje navracení, i když: Jednou jednu skupinu je přepínač vybrán...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd338b622779b64dd59f9cf6f3e2365ef5cb3ffb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072289"
---
<a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="8bb68-104">Vytvoření vzájemně se vylučujících zaškrtávacích políček (VB)</span><span class="sxs-lookup"><span data-stu-id="8bb68-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>
====================
<span data-ttu-id="8bb68-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8bb68-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8bb68-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8bb68-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="8bb68-107">Když je možné vybrat jenom jednu sadu možností, přepínače se obvykle používají.</span><span class="sxs-lookup"><span data-stu-id="8bb68-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="8bb68-108">Existuje navracení, i když: Po výběru jedné přepínací tlačítka ve skupině není možné zrušit zaškrtnutí všech přepínačů.</span><span class="sxs-lookup"><span data-stu-id="8bb68-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="8bb68-109">Zaškrtávací políčka v každém okamžiku může nezaškrtnuté, ale nejsou vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="8bb68-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="8bb68-110">Tento kurz nabízí to nejlepší z obou přístupů: zaškrtávací políčka, které se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="8bb68-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>


## <a name="overview"></a><span data-ttu-id="8bb68-111">Přehled</span><span class="sxs-lookup"><span data-stu-id="8bb68-111">Overview</span></span>

<span data-ttu-id="8bb68-112">Když je možné vybrat jenom jednu sadu možností, přepínače se obvykle používají.</span><span class="sxs-lookup"><span data-stu-id="8bb68-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="8bb68-113">Existuje navracení, i když: Po výběru jedné přepínací tlačítka ve skupině není možné zrušit zaškrtnutí všech přepínačů.</span><span class="sxs-lookup"><span data-stu-id="8bb68-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="8bb68-114">Zaškrtávací políčka v každém okamžiku může nezaškrtnuté, ale nejsou vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="8bb68-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="8bb68-115">Tento kurz nabízí to nejlepší z obou přístupů: zaškrtávací políčka, které se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="8bb68-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="8bb68-116">Kroky</span><span class="sxs-lookup"><span data-stu-id="8bb68-116">Steps</span></span>

<span data-ttu-id="8bb68-117">ASP.NET AJAX Control Toolkit obsahuje MutuallyExclusiveCheckBox zařízení extender.</span><span class="sxs-lookup"><span data-stu-id="8bb68-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="8bb68-118">To umožňuje programátorům přiřadit libovolný zaškrtávací políčko na název skupiny (`Key` atributu).</span><span class="sxs-lookup"><span data-stu-id="8bb68-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="8bb68-119">Ze všech políček v rámci stejné skupiny může najednou vybrat pouze jeden.</span><span class="sxs-lookup"><span data-stu-id="8bb68-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="8bb68-120">Začněme se umísťování dvě zaškrtávací políčka na novou stránku ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8bb68-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="8bb68-121">Může existovat více, ale dva z nich stačí k předvedení se zásadou:</span><span class="sxs-lookup"><span data-stu-id="8bb68-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="8bb68-122">U obou políček MutuallyExclusiveCheckBoxExtender ovládací prvek je třeba umístit na stránce.</span><span class="sxs-lookup"><span data-stu-id="8bb68-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="8bb68-123">Oba atributy klíč musí mít stejnou hodnotu, stejně jako hodnota, kterou atributy prvků HTML tlačítko přepínače musí být stejný jako označují skupiny, do kterých patří.</span><span class="sxs-lookup"><span data-stu-id="8bb68-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="8bb68-124">Vlastnost TargetControlID rozšiřujícího objektu, který odkazuje na Identifikátor zaškrtávacího políčka.</span><span class="sxs-lookup"><span data-stu-id="8bb68-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="8bb68-125">A konečně, zahrnují technologie ASP.NET AJAX `ScriptManager` kterou všechny prvky technologie ASP.NET AJAX Control Toolkit vyžaduje:</span><span class="sxs-lookup"><span data-stu-id="8bb68-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="8bb68-126">Uložte a spusťte: Můžete zkontrolovat a zrušit zaškrtnutí obou políček, ale současně může obě políčka kontrolovat.</span><span class="sxs-lookup"><span data-stu-id="8bb68-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>


<span data-ttu-id="8bb68-127">[![Najednou lze zkontrolovat pouze jeden checkbox](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8bb68-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="8bb68-128">Pouze jeden checkbox můžete zkontrolovat v čase ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8bb68-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8bb68-129">Předchozí</span><span class="sxs-lookup"><span data-stu-id="8bb68-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)