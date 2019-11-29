---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: Použití ovládacího prvku posuvník s automatickým zpětným voláním (VB) | Microsoft Docs
author: wenz
description: Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Je možné vytvořit posuvník pro autopost...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598560"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="008df-104">Použití ovládacího prvku posuvník s automatickým zpětným voláním (VB)</span><span class="sxs-lookup"><span data-stu-id="008df-104">Using the Slider Control With Auto-Postback (VB)</span></span>

<span data-ttu-id="008df-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="008df-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="008df-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="008df-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="008df-107">Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši.</span><span class="sxs-lookup"><span data-stu-id="008df-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="008df-108">Po změně hodnoty je možné provést automatické odeslání posuvníku.</span><span class="sxs-lookup"><span data-stu-id="008df-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="008df-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="008df-109">Overview</span></span>

<span data-ttu-id="008df-110">Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši.</span><span class="sxs-lookup"><span data-stu-id="008df-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="008df-111">Po změně hodnoty je možné provést automatické odeslání posuvníku.</span><span class="sxs-lookup"><span data-stu-id="008df-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="008df-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="008df-112">Steps</span></span>

<span data-ttu-id="008df-113">Aby se posuvník mohl automaticky předávat po změně, musí být v obou textových polích atribut `AutoPostBack="true"`: textové pole, které se stane samotným jezdcem, a textové pole, které obsahuje pozici posuvníku.</span><span class="sxs-lookup"><span data-stu-id="008df-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="008df-114">Zde je povinná značka pro:</span><span class="sxs-lookup"><span data-stu-id="008df-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="008df-115">Ovládací prvek `SliderExtender` z ovládací sady nástrojů ASP.NET AJAX přiřadí funkci posuvníku dvěma textovým polím:</span><span class="sxs-lookup"><span data-stu-id="008df-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="008df-116">Další element Label bude později použit k informování uživatele o zpětném volání:</span><span class="sxs-lookup"><span data-stu-id="008df-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="008df-117">Nakonec ovládací prvek `ScriptManager` ASP.NET AJAX načte požadovaný JavaScript, který bude ovládací sada nástrojů fungovat:</span><span class="sxs-lookup"><span data-stu-id="008df-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="008df-118">Nyní se posuvník účtuje zpátky. na straně serveru může být tato událost zachycena a následně provedena na:</span><span class="sxs-lookup"><span data-stu-id="008df-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

<span data-ttu-id="008df-119">[![přesunutí posuvníku aktivuje postback.](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="008df-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="008df-120">Přesunutí posuvníku aktivuje postback ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-slider-control-with-auto-postback-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="008df-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>

<span data-ttu-id="008df-121">[![později se datum této změny zapíše do popisku.](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="008df-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="008df-122">Následně se datum této změny zapíše do popisku ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-slider-control-with-auto-postback-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="008df-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="008df-123">[Předchozí](databinding-the-slider-control-cs.md)
> [Další](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="008df-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
