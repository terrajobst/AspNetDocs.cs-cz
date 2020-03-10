---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: Použití ovládacího prvku posuvník s automatickým zpětnýmC#voláním () | Microsoft Docs
author: wenz
description: Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Je možné vytvořit posuvník pro autopost...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553618"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a>Použití ovládacího prvku posuvník s automatickým zpětnýmC#voláním ()

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)

> Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Po změně hodnoty je možné provést automatické odeslání posuvníku.

## <a name="overview"></a>Přehled

Posuvník v ovládacím prvku AJAX Control Toolkit poskytuje grafický posuvník, který lze ovládat pomocí myši. Po změně hodnoty je možné provést automatické odeslání posuvníku.

## <a name="steps"></a>Kroky

Aby se posuvník mohl automaticky předávat po změně, musí být v obou textových polích atribut `AutoPostBack="true"`: textové pole, které se stane samotným jezdcem, a textové pole, které obsahuje pozici posuvníku. Zde je povinná značka pro:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

Ovládací prvek `SliderExtender` z ovládací sady nástrojů ASP.NET AJAX přiřadí funkci posuvníku dvěma textovým polím:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

Další element Label bude později použit k informování uživatele o zpětném volání:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

Nakonec ovládací prvek `ScriptManager` ASP.NET AJAX načte požadovaný JavaScript, který bude ovládací sada nástrojů fungovat:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

Nyní se posuvník účtuje zpátky. na straně serveru může být tato událost zachycena a následně provedena na:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

[![přesunutí posuvníku aktivuje postback.](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)

Přesunutí posuvníku aktivuje postback ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-slider-control-with-auto-postback-cs/_static/image3.png)

[![později se datum této změny zapíše do popisku.](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)

Následně se datum této změny zapíše do popisku ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-slider-control-with-auto-postback-cs/_static/image6.png)

> [!div class="step-by-step"]
> [Next](databinding-the-slider-control-cs.md)
