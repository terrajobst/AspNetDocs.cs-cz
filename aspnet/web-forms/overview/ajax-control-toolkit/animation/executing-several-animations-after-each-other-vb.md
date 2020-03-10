---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: Provádění několika animací po sobě (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit sever...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598131"
---
# <a name="executing-several-animations-after-each-other-vb"></a>Postupné provedení několika animací (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit několik animací za sebou.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit několik animací za sebou.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla. Obecně `<OnLoad>` akceptuje pouze jednu animaci. Rozhraní animace umožňuje připojit několik animací k jednomu pomocí elementu `<Sequence>`. Všechny animace v rámci `<Sequence>` jsou spouštěny jednou po druhém. Zde je možné označení pro ovládací prvek `AnimationExtender`, nejprve panel Rozšiřte a poté zmenšete jeho výšku:

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

Když spustíte tento skript, panel se nejprve rozšíří a pak zmenší.

[![první šířka se zvyšuje.](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)

Nejprve se zvětší Šířka ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-after-each-other-vb/_static/image3.png)

[![pak se výška zmenší.](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)

Pak se výška zmenší ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-after-each-other-vb/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](executing-several-animations-at-the-same-time-vb.md)
> [Další](animation-depending-on-a-condition-vb.md)
