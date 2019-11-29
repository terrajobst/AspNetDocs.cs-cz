---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: Provádění několika animací současně (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje spustit sever...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575364"
---
# <a name="executing-several-animations-at-the-same-time-c"></a>Provádění několika animací současně (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje paralelní spuštění několika animací.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Umožňuje paralelní spuštění několika animací.

## <a name="steps"></a>Uvedené

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla. Obecně `<OnLoad>` akceptuje pouze jednu animaci. Rozhraní animace umožňuje připojit několik animací k jednomu pomocí elementu `<Parallel>`. Všechny animace v rámci `<Parallel>` jsou spouštěny ve stejnou dobu.

Zde je možné označení pro ovládací prvek `AnimationExtender`, podrobné změny a změna velikosti panelu ve stejnou dobu:

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

A skutečně: když spustíte tento skript, panel se zobrazí a pak se změní velikost (víc než při cestě k jeho šířce a poloviční výška) a rozchází se současně.

[![panelu se dozvíte a mění velikost (včetně jeho obsahu), a to díky modulu vykreslování v prohlížeči).](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)

Na panelu se dozvíte, jak změnit velikost (včetně jejího obsahu), a to díky modulu vykreslování v prohlížeči ([kliknutím zobrazíte obrázek v plné velikosti).](executing-several-animations-at-the-same-time-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](adding-animation-to-a-control-cs.md)
> [Další](executing-several-animations-after-each-other-cs.md)
