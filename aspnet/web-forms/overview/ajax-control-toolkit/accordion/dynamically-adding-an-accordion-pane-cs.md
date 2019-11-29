---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: Dynamické Přidání podokna pro přiznávání (C#) | Microsoft Docs
author: wenz
description: Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607250"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="17901-104">Dynamické Přidání podokna pro přiznávání (C#)</span><span class="sxs-lookup"><span data-stu-id="17901-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="17901-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="17901-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="17901-106">[Stažení kódu](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="17901-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="17901-107">Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou.</span><span class="sxs-lookup"><span data-stu-id="17901-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="17901-108">Panely jsou obvykle deklarovány v rámci samotné stránky, ale kód na straně serveru lze použít k dosažení stejného výsledku.</span><span class="sxs-lookup"><span data-stu-id="17901-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="17901-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="17901-109">Overview</span></span>

<span data-ttu-id="17901-110">Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou.</span><span class="sxs-lookup"><span data-stu-id="17901-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="17901-111">Panely jsou obvykle deklarovány v rámci samotné stránky, ale kód na straně serveru lze použít k dosažení stejného výsledku.</span><span class="sxs-lookup"><span data-stu-id="17901-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="17901-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="17901-112">Steps</span></span>

<span data-ttu-id="17901-113">Řízení přiznávání zveřejňuje všechny důležité vlastnosti kódu na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="17901-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="17901-114">Mimo jiné vlastnost `Panes` uděluje přístup ke kolekci podoken, která tvoří danou přiznávání.</span><span class="sxs-lookup"><span data-stu-id="17901-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="17901-115">Každé podokno je typu `AccordionPane`.</span><span class="sxs-lookup"><span data-stu-id="17901-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="17901-116">Proto je triviální vytvořit takové podokno:</span><span class="sxs-lookup"><span data-stu-id="17901-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="17901-117">Vlastnost `HeaderContainer` `AccordionPane` poskytuje přístup k ovládacím prvkům ASP.NET v části záhlaví v podokně; vlastnost `ContentContainer` `AccordionPane` má pro oddíl Content v podokně stejný obsah.</span><span class="sxs-lookup"><span data-stu-id="17901-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="17901-118">To umožňuje ASP.NET kódu přidávat obsah do podoken:</span><span class="sxs-lookup"><span data-stu-id="17901-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="17901-119">Nakonec je třeba přidat podokna do `Panes` kolekce přiznávání:</span><span class="sxs-lookup"><span data-stu-id="17901-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="17901-120">Tady je kompletní kód na straně serveru, který do ovládacího prvku pro řízení přihlašování přičítá dvě podokna:</span><span class="sxs-lookup"><span data-stu-id="17901-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="17901-121">Jediným chybějícím prvkem je samotné přiznávání, které závisí na přítomnosti ovládacího prvku ASP.NET `ScriptManager`:</span><span class="sxs-lookup"><span data-stu-id="17901-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="17901-122">Chcete-li dokončit příklad, dvě třídy CSS, na které se odkazuje v ovládacím prvku pro přiznávání, poskytují informace o stylu prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="17901-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

<span data-ttu-id="17901-123">[![data v přiznávání dynamicky přidal kód na straně serveru.](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="17901-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="17901-124">Data v přiznávání se dynamicky přidala přes kód na straně serveru ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-adding-an-accordion-pane-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="17901-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="17901-125">[Předchozí](databinding-to-an-accordion-cs.md)
> [Další](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="17901-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
