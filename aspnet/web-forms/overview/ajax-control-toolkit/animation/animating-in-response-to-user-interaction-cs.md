---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: Animace v reakci na interakci uživatele (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace můžou mít hvězdičku...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614371"
---
# <a name="animating-in-response-to-user-interaction-c"></a>Animace v reakci na interakci uživatele (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace mohou být spouštěny automaticky nebo mohou být aktivovány interakcí uživatele, například kliknutím myší.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace mohou být spouštěny automaticky nebo mohou být aktivovány interakcí uživatele, například kliknutím myší.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

V uzlu `<Animations>` existuje pět způsobů, jak spustit animaci prostřednictvím interakce s uživatelem (chybějící element je `<OnLoad>`, který je proveden po úplném načtení celé stránky):

- `<OnClick>` (kliknutí myší na ovládací prvek)
- `<OnHoverOut>` (myš opustí ovládací prvek)
- `<OnHoverOver>` (najetí myší nad ovládací prvek, zastavení `<OnHoverOut>` animace)
- `<OnMouseOut>` (opustí ovládací prvek myší)
- `<OnMouseOver>` (najetí myší na ovládací prvek, nezastavení `<OnMouseOut>` animace)

V tomto scénáři se používá `<OnClick>`. Když uživatel klikne na panel, změní se jeho velikost a zároveň se vykreslí.

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

[![kliknutí myší se spustí animace](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

Po kliknutí myší se spustí animace ([kliknutím zobrazíte obrázek v plné velikosti).](animating-in-response-to-user-interaction-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](picking-one-animation-out-of-a-list-cs.md)
> [Další](disabling-actions-during-animation-cs.md)
