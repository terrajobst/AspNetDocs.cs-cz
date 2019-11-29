---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: Použití ovládacího prvku textboxwatermark s ovládacími prvkyC#ověřování () | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku textboxwatermark v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text. Když uživatel klikne do pole, i...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: bc9498b1c5ba2f38b90706c9200ffa813a945fa9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74610872"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="6676c-104">Použití ovládacího prvku TextBoxWatermark s validačními ovládacími prvky (C#)</span><span class="sxs-lookup"><span data-stu-id="6676c-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>

<span data-ttu-id="6676c-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6676c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6676c-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6676c-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="6676c-107">Ovládací prvek ovládacího prvku textboxwatermark v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text.</span><span class="sxs-lookup"><span data-stu-id="6676c-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="6676c-108">Když uživatel klikne na pole, bude vyprázdněn.</span><span class="sxs-lookup"><span data-stu-id="6676c-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="6676c-109">Pokud uživatel opustí pole bez zadání textu, předem vyplněný text se zobrazí znovu.</span><span class="sxs-lookup"><span data-stu-id="6676c-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="6676c-110">To může kolidovat s ovládacími prvky ověřování ASP.NET na stejné stránce, ale tyto problémy se můžou překonat.</span><span class="sxs-lookup"><span data-stu-id="6676c-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="6676c-111">Přehled</span><span class="sxs-lookup"><span data-stu-id="6676c-111">Overview</span></span>

<span data-ttu-id="6676c-112">Ovládací prvek `TextBoxWatermark` v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text.</span><span class="sxs-lookup"><span data-stu-id="6676c-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="6676c-113">Když uživatel klikne na pole, bude vyprázdněn.</span><span class="sxs-lookup"><span data-stu-id="6676c-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="6676c-114">Pokud uživatel opustí pole bez zadání textu, předem vyplněný text se zobrazí znovu.</span><span class="sxs-lookup"><span data-stu-id="6676c-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="6676c-115">To může kolidovat s ovládacími prvky ověřování ASP.NET na stejné stránce, ale tyto problémy se můžou překonat.</span><span class="sxs-lookup"><span data-stu-id="6676c-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="6676c-116">Uvedené</span><span class="sxs-lookup"><span data-stu-id="6676c-116">Steps</span></span>

<span data-ttu-id="6676c-117">Základní nastavení ukázky je následující: ovládací prvek `TextBox` má vodoznak pomocí ovládacího prvku `TextBoxWatermarkExtender`.</span><span class="sxs-lookup"><span data-stu-id="6676c-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="6676c-118">Tlačítko aktivuje postback a později bude použito ke spuštění ovládacích prvků ověřování na stránce.</span><span class="sxs-lookup"><span data-stu-id="6676c-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="6676c-119">Pro inicializaci ASP.NET AJAX je také vyžadován ovládací prvek `ScriptManager`:</span><span class="sxs-lookup"><span data-stu-id="6676c-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="6676c-120">Nyní přidejte ovládací prvek `RequiredFieldValidator`, který zkontroluje, zda je v poli při odeslání formuláře text.</span><span class="sxs-lookup"><span data-stu-id="6676c-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="6676c-121">Vlastnost `InitialValue` validátoru musí být nastavena na stejnou hodnotu, která se používá v ovládacím prvku `TextBoxWatermarkExtender`: při odeslání formuláře je hodnota nezměněného textového pole hodnotou meze v této podobě:</span><span class="sxs-lookup"><span data-stu-id="6676c-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="6676c-122">Existuje však jeden problém s tímto přístupem: Pokud klient zakáže JavaScript, textové pole není předem vyplněno textem vodoznaku, proto `RequiredFieldValidator` nespustí chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="6676c-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="6676c-123">Proto je vyžadován druhý `RequiredFieldValidator` ovládací prvek, který kontroluje prázdné textové pole (s vynecháním `InitialValue` atributu).</span><span class="sxs-lookup"><span data-stu-id="6676c-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="6676c-124">Vzhledem k tomu, že oba validátory používají `Display`=`"Dynamic"`, nemůže koncový uživatel rozlišovat od vizuálního vzhledu, který vyvolaly dva validátory. místo toho se zdá, že existovala pouze jedna z nich.</span><span class="sxs-lookup"><span data-stu-id="6676c-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="6676c-125">Nakonec přidejte nějaký kód na straně serveru pro výstup textu do pole, pokud žádný validátor nevystavil chybovou zprávu:</span><span class="sxs-lookup"><span data-stu-id="6676c-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="6676c-126">[![stížnosti validátoru, že v poli není žádný text](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6676c-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="6676c-127">Validátor vyplatí, že v poli není žádný text ([kliknutím zobrazíte obrázek v plné velikosti).](using-textboxwatermark-with-validation-controls-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6676c-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6676c-128">[Předchozí](using-textboxwatermark-in-a-formview-cs.md)
> [Další](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6676c-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>
