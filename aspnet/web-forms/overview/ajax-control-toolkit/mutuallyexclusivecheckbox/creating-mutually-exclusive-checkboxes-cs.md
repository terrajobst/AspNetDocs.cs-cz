---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: Vytváření vzájemně se vylučujícíchC#zaškrtávacích políček () | Microsoft Docs
author: wenz
description: 'Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka. Došlo k nevýhodě, i když: je vybráno jedno přepínač ve skupině,...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606504"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a><span data-ttu-id="e5342-104">Vytvoření vzájemně se vylučujících zaškrtávacích políček (C#)</span><span class="sxs-lookup"><span data-stu-id="e5342-104">Creating Mutually Exclusive Checkboxes (C#)</span></span>

<span data-ttu-id="e5342-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e5342-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e5342-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e5342-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span></span>

> <span data-ttu-id="e5342-107">Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka.</span><span class="sxs-lookup"><span data-stu-id="e5342-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="e5342-108">Došlo k nevýhodě, i když: Když vyberete jeden přepínač ve skupině, není možné zrušit kontrolu všech přepínačů.</span><span class="sxs-lookup"><span data-stu-id="e5342-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="e5342-109">Zaškrtávací políčka je možné kdykoli zrušit, ale vzájemně se nevylučují.</span><span class="sxs-lookup"><span data-stu-id="e5342-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="e5342-110">Tento kurz nabízí nejlepší z obou přístupů: zaškrtávací políčka, která se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="e5342-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="e5342-111">Přehled</span><span class="sxs-lookup"><span data-stu-id="e5342-111">Overview</span></span>

<span data-ttu-id="e5342-112">Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka.</span><span class="sxs-lookup"><span data-stu-id="e5342-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="e5342-113">Došlo k nevýhodě, i když: Když vyberete jeden přepínač ve skupině, není možné zrušit kontrolu všech přepínačů.</span><span class="sxs-lookup"><span data-stu-id="e5342-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="e5342-114">Zaškrtávací políčka je možné kdykoli zrušit, ale vzájemně se nevylučují.</span><span class="sxs-lookup"><span data-stu-id="e5342-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="e5342-115">Tento kurz nabízí nejlepší z obou přístupů: zaškrtávací políčka, která se vzájemně vylučují.</span><span class="sxs-lookup"><span data-stu-id="e5342-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="e5342-116">Uvedené</span><span class="sxs-lookup"><span data-stu-id="e5342-116">Steps</span></span>

<span data-ttu-id="e5342-117">Sada ASP.NET AJAX Control Toolkit obsahuje MutuallyExclusiveCheckBox a Extender.</span><span class="sxs-lookup"><span data-stu-id="e5342-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="e5342-118">To umožňuje programátorům přiřadit libovolné zaškrtávací políčko k názvu skupiny (`Key` atribut).</span><span class="sxs-lookup"><span data-stu-id="e5342-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="e5342-119">Všechna zaškrtávací políčka v rámci stejné skupiny se dají vybrat jenom jednou.</span><span class="sxs-lookup"><span data-stu-id="e5342-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="e5342-120">Začněte tím, že na nové stránce ASP.NET vložíte dvě zaškrtávací políčka.</span><span class="sxs-lookup"><span data-stu-id="e5342-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="e5342-121">Může to být více, ale dva z nich jsou dostačující k předvedení principu:</span><span class="sxs-lookup"><span data-stu-id="e5342-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

<span data-ttu-id="e5342-122">Pro obě zaškrtávací políčka musí být ovládací prvek MutuallyExclusiveCheckBoxExtender vložen na stránku.</span><span class="sxs-lookup"><span data-stu-id="e5342-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="e5342-123">Oba atributy klíče musí mít stejnou hodnotu, stejně jako atributy hodnoty prvků přepínače HTML musí být identické, aby se shodovaly s tím, do které skupiny patří.</span><span class="sxs-lookup"><span data-stu-id="e5342-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="e5342-124">Vlastnost vlastnost TargetControlID prvku objektu Extender odkazuje na ID zaškrtávacího políčka.</span><span class="sxs-lookup"><span data-stu-id="e5342-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

<span data-ttu-id="e5342-125">Nakonec zahrňte ASP.NET AJAX `ScriptManager`, který je vyžadován všemi prvky sady ASP.NET AJAX Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="e5342-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

<span data-ttu-id="e5342-126">Uložte a spusťte stránku: můžete zaškrtnout a zrušit zaškrtnutí obou políček, avšak současně by nebylo možné zaškrtnout obě zaškrtávací políčka.</span><span class="sxs-lookup"><span data-stu-id="e5342-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="e5342-127">[![může být současně zaškrtnuto pouze jedno zaškrtávací políčko.](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e5342-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span></span>

<span data-ttu-id="e5342-128">Současně může být zaškrtnuto pouze jedno zaškrtávací políčko ([kliknutím zobrazíte obrázek v plné velikosti).](creating-mutually-exclusive-checkboxes-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e5342-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e5342-129">Next</span><span class="sxs-lookup"><span data-stu-id="e5342-129">Next</span></span>](creating-mutually-exclusive-checkboxes-vb.md)
