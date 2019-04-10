---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: Použití ovládacího prvku TextBoxWatermark s validačních ovládacích prvků (C#) | Dokumentace Microsoftu
author: wenz
description: Ovládacího prvku TextBoxWatermark v sadou nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby text se zobrazí v poli. Když uživatel klikne do pole, to jsem...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: f833868d9dbf51a9714b9bbe6730a24badc169d0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59391010"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="64142-104">Použití ovládacího prvku TextBoxWatermark s validačními ovládacími prvky (C#)</span><span class="sxs-lookup"><span data-stu-id="64142-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>

<span data-ttu-id="64142-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="64142-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="64142-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="64142-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="64142-107">Ovládacího prvku TextBoxWatermark v sadou nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby text se zobrazí v poli.</span><span class="sxs-lookup"><span data-stu-id="64142-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="64142-108">Když uživatel klikne do pole, je prázdný.</span><span class="sxs-lookup"><span data-stu-id="64142-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="64142-109">Pokud uživatel ponechá pole bez nutnosti zadávat text, zobrazí se předem vyplněných text.</span><span class="sxs-lookup"><span data-stu-id="64142-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="64142-110">To může kolidovat s ASP.NET validačních ovládacích prvků na stejné stránce, ale může tyto problémy překonat.</span><span class="sxs-lookup"><span data-stu-id="64142-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>


## <a name="overview"></a><span data-ttu-id="64142-111">Přehled</span><span class="sxs-lookup"><span data-stu-id="64142-111">Overview</span></span>

<span data-ttu-id="64142-112">`TextBoxWatermark` Ovládacího prvku AJAX Control Toolkit rozšiřuje textové pole tak, aby text se zobrazí v poli.</span><span class="sxs-lookup"><span data-stu-id="64142-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="64142-113">Když uživatel klikne do pole, je prázdný.</span><span class="sxs-lookup"><span data-stu-id="64142-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="64142-114">Pokud uživatel ponechá pole bez nutnosti zadávat text, zobrazí se předem vyplněných text.</span><span class="sxs-lookup"><span data-stu-id="64142-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="64142-115">To může kolidovat s ASP.NET validačních ovládacích prvků na stejné stránce, ale může tyto problémy překonat.</span><span class="sxs-lookup"><span data-stu-id="64142-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="64142-116">Kroky</span><span class="sxs-lookup"><span data-stu-id="64142-116">Steps</span></span>

<span data-ttu-id="64142-117">Základní nastavení vzorku je následující: `TextBox` ovládací prvek je horní mezí, použití `TextBoxWatermarkExtender` ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="64142-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="64142-118">Tlačítko aktivuje zpětného odeslání a bude možné později použít k aktivaci validačních ovládacích prvků na stránce.</span><span class="sxs-lookup"><span data-stu-id="64142-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="64142-119">Navíc `ScriptManager` ovládací prvek je potřebné k inicializaci technologie ASP.NET AJAX:</span><span class="sxs-lookup"><span data-stu-id="64142-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="64142-120">Teď přidejte `RequiredFieldValidator` ovládací prvek, který kontroluje, zda je text v poli při odeslání formuláře.</span><span class="sxs-lookup"><span data-stu-id="64142-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="64142-121">`InitialValue` Validátoru musí být nastavena na stejnou hodnotu, která se používá v `TextBoxWatermarkExtender` ovládacího prvku: Když se odešle formulář, beze změny textové pole hodnotu hodnoty meze v rámci něj:</span><span class="sxs-lookup"><span data-stu-id="64142-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="64142-122">Je ale jeden problém s tímto přístupem: Pokud klient zakáže jazyka JavaScript, pole textu není proto předem s vodoznakového textu `RequiredFieldValidator` neaktivuje chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="64142-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="64142-123">Proto sekundy `RequiredFieldValidator` ovládací prvek je vyžadován, který vyhledává prázdné textové pole (vynechání `InitialValue` atributu).</span><span class="sxs-lookup"><span data-stu-id="64142-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="64142-124">Jelikož obě validátory používat `Display` = `"Dynamic"`, koncovému uživateli nelze rozlišit z vizuálního vzhledu, která dvě validátorů se vyvolala; místo toho to vypadá, došlo jenom jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="64142-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="64142-125">Nakonec přidejte nějaký kód na straně serveru do výstupního text v poli, pokud nebyl nalezen žádný validátor vydané chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="64142-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]


[![T<span data-ttu-id="64142-126">he program pro ověření, že neexistuje žádný text v poli si bude stěžovat]</span><span class="sxs-lookup"><span data-stu-id="64142-126">he validator complains that there is no text in the field]</span></span>(using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

<span data-ttu-id="64142-127">Validátor si bude stěžovat na, že neexistuje žádný text v poli ([kliknutím ji zobrazíte obrázek v plné velikosti](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="64142-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="64142-128">[Předchozí](using-textboxwatermark-in-a-formview-cs.md)
> [další](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="64142-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>
