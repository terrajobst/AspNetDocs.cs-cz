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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553562"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a>Použití ovládacího prvku posuvník s automatickým zpětným voláním (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)

> Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Po změně hodnoty je možné provést automatické odeslání posuvníku.

## <a name="overview"></a>Přehled

Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Po změně hodnoty je možné provést automatické odeslání posuvníku.

## <a name="steps"></a>Kroky

Aby se posuvník mohl automaticky předávat po změně, musí být v obou textových polích atribut `AutoPostBack="true"`: textové pole, které se stane samotným jezdcem, a textové pole, které obsahuje pozici posuvníku. Zde je povinná značka pro:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

Ovládací prvek `SliderExtender` z ovládací sady nástrojů ASP.NET AJAX přiřadí funkci posuvníku dvěma textovým polím:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

Další element Label bude později použit k informování uživatele o zpětném volání:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

Nakonec ovládací prvek `ScriptManager` ASP.NET AJAX načte požadovaný JavaScript, který bude ovládací sada nástrojů fungovat:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

Nyní se posuvník účtuje zpátky. na straně serveru může být tato událost zachycena a následně provedena na:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

[![přesunutí posuvníku aktivuje postback.](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)

Přesunutí posuvníku aktivuje postback ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-slider-control-with-auto-postback-vb/_static/image3.png)

[![později se datum této změny zapíše do popisku.](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)

Následně se datum této změny zapíše do popisku ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-slider-control-with-auto-postback-vb/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](databinding-the-slider-control-cs.md)
> [Další](databinding-the-slider-control-vb.md)
