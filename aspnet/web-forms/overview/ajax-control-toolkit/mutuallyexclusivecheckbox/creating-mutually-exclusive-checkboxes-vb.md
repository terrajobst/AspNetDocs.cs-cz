---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Vytváření vzájemně se vylučujících zaškrtávacích políček (VB) | Microsoft Docs
author: wenz
description: 'Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka. Došlo k nevýhodě, i když: je vybráno jedno přepínač ve skupině,...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554010"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="b7777-104">Vytvoření vzájemně se vylučujících zaškrtávacích políček (VB)</span><span class="sxs-lookup"><span data-stu-id="b7777-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>

<span data-ttu-id="b7777-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b7777-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b7777-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b7777-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="b7777-107">Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka.</span><span class="sxs-lookup"><span data-stu-id="b7777-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="b7777-108">Došlo k nevýhodě, i když: Když vyberete jeden přepínač ve skupině, není možné zrušit kontrolu všech přepínačů.</span><span class="sxs-lookup"><span data-stu-id="b7777-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="b7777-109">Zaškrtávací políčka je možné kdykoli zrušit, ale vzájemně se nevylučují.</span><span class="sxs-lookup"><span data-stu-id="b7777-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="b7777-110">Tento kurz nabízí nejlepší z obou přístupů: zaškrtávací políčka, která se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="b7777-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="b7777-111">Přehled</span><span class="sxs-lookup"><span data-stu-id="b7777-111">Overview</span></span>

<span data-ttu-id="b7777-112">Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka.</span><span class="sxs-lookup"><span data-stu-id="b7777-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="b7777-113">Došlo k nevýhodě, i když: Když vyberete jeden přepínač ve skupině, není možné zrušit kontrolu všech přepínačů.</span><span class="sxs-lookup"><span data-stu-id="b7777-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="b7777-114">Zaškrtávací políčka je možné kdykoli zrušit, ale vzájemně se nevylučují.</span><span class="sxs-lookup"><span data-stu-id="b7777-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="b7777-115">Tento kurz nabízí nejlepší z obou přístupů: zaškrtávací políčka, která se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="b7777-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="b7777-116">Kroky</span><span class="sxs-lookup"><span data-stu-id="b7777-116">Steps</span></span>

<span data-ttu-id="b7777-117">Sada ASP.NET AJAX Control Toolkit obsahuje MutuallyExclusiveCheckBox a Extender.</span><span class="sxs-lookup"><span data-stu-id="b7777-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="b7777-118">To umožňuje programátorům přiřadit libovolné zaškrtávací políčko k názvu skupiny (`Key` atribut).</span><span class="sxs-lookup"><span data-stu-id="b7777-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="b7777-119">Všechna zaškrtávací políčka v rámci stejné skupiny se dají vybrat jenom jednou.</span><span class="sxs-lookup"><span data-stu-id="b7777-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="b7777-120">Začněte tím, že na nové stránce ASP.NET vložíte dvě zaškrtávací políčka.</span><span class="sxs-lookup"><span data-stu-id="b7777-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="b7777-121">Může to být více, ale dva z nich jsou dostačující k předvedení principu:</span><span class="sxs-lookup"><span data-stu-id="b7777-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="b7777-122">Pro obě zaškrtávací políčka musí být ovládací prvek MutuallyExclusiveCheckBoxExtender vložen na stránku.</span><span class="sxs-lookup"><span data-stu-id="b7777-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="b7777-123">Oba atributy klíče musí mít stejnou hodnotu, stejně jako atributy hodnoty prvků přepínače HTML musí být identické, aby se shodovaly s tím, do které skupiny patří.</span><span class="sxs-lookup"><span data-stu-id="b7777-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="b7777-124">Vlastnost vlastnost TargetControlID prvku objektu Extender odkazuje na ID zaškrtávacího políčka.</span><span class="sxs-lookup"><span data-stu-id="b7777-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="b7777-125">Nakonec zahrňte ASP.NET AJAX `ScriptManager`, který je vyžadován všemi prvky sady ASP.NET AJAX Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="b7777-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="b7777-126">Uložte a spusťte stránku: můžete zaškrtnout a zrušit zaškrtnutí obou políček, avšak současně by nebylo možné zaškrtnout obě zaškrtávací políčka.</span><span class="sxs-lookup"><span data-stu-id="b7777-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="b7777-127">[![může být současně zaškrtnuto pouze jedno zaškrtávací políčko.](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b7777-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="b7777-128">Současně může být zaškrtnuto pouze jedno zaškrtávací políčko ([kliknutím zobrazíte obrázek v plné velikosti).](creating-mutually-exclusive-checkboxes-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b7777-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b7777-129">Předchozí</span><span class="sxs-lookup"><span data-stu-id="b7777-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
