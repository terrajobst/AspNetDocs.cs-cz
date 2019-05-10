---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: Dynamické přidání podokna ovládacího prvku Accordion (C#) | Dokumentace Microsoftu
author: wenz
description: Ovládacího prvku Accordion sadou nástrojů AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarované w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 7134c95845ec7f22b5216e10b50ab8f81cd24806
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131250"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="8ab3e-104">Dynamické přidání podokna ovládacího prvku Accordion (C#)</span><span class="sxs-lookup"><span data-stu-id="8ab3e-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="8ab3e-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8ab3e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8ab3e-106">[Stáhněte si kód](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8ab3e-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="8ab3e-107">Ovládacího prvku Accordion sadou nástrojů AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="8ab3e-108">Panely jsou obvykle deklarované v rámci samotné stránky, ale kód na straně serveru slouží k dosažení stejného výsledku.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="8ab3e-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="8ab3e-109">Overview</span></span>

<span data-ttu-id="8ab3e-110">Ovládacího prvku Accordion sadou nástrojů AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="8ab3e-111">Panely jsou obvykle deklarované v rámci samotné stránky, ale kód na straně serveru slouží k dosažení stejného výsledku.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="8ab3e-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="8ab3e-112">Steps</span></span>

<span data-ttu-id="8ab3e-113">Ovládací prvek Accordion poskytuje všechny důležité vlastnosti do kódu na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="8ab3e-114">Mimo jiné `Panes` vlastnost uděluje přístup ke kolekci podoken, které tvoří prvku typu Accordion.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="8ab3e-115">Každé podokno je typu `AccordionPane`.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="8ab3e-116">Proto je jednoduché vytvořit takové podokno:</span><span class="sxs-lookup"><span data-stu-id="8ab3e-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="8ab3e-117">`HeaderContainer` Vlastnost `AccordionPane` poskytuje přístup k ovládacím prvkům technologie ASP.NET v záhlaví podokna; `ContentContainer` vlastnost `AccordionPane` dělá to samé pro části obsahu podokna.</span><span class="sxs-lookup"><span data-stu-id="8ab3e-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="8ab3e-118">To umožňuje kódu ASP.NET k přidání obsahu do podokna:</span><span class="sxs-lookup"><span data-stu-id="8ab3e-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="8ab3e-119">Nakonec pane(s) musí být přidané do `Panes` kolekce prvku typu Accordion:</span><span class="sxs-lookup"><span data-stu-id="8ab3e-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="8ab3e-120">Tady je kompletní kód na straně serveru, který přidá dvě podokna ovládacího prvku Accordion:</span><span class="sxs-lookup"><span data-stu-id="8ab3e-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="8ab3e-121">Pouze chybí element je prvku typu Accordion samostatně, což závisí na přítomnosti technologie ASP.NET `ScriptManager` ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="8ab3e-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="8ab3e-122">K dokončení příkladu, dvě šablony stylů CSS třídy odkazuje v ovládacím prvku typu Accordion poskytují informace o stylu prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="8ab3e-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

<span data-ttu-id="8ab3e-123">[![Data prvku typu accordion dynamicky přidal kód na straně serveru](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8ab3e-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="8ab3e-124">Data prvku typu accordion dynamicky přidal kód na straně serveru ([kliknutím ji zobrazíte obrázek v plné velikosti](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8ab3e-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8ab3e-125">[Předchozí](databinding-to-an-accordion-cs.md)
> [další](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8ab3e-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
