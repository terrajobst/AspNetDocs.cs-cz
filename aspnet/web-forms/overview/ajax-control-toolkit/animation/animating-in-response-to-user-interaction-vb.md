---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: Animace v reakci na interakci uživatele (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace můžou mít hvězdičku...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607027"
---
# <a name="animating-in-response-to-user-interaction-vb"></a>Animace v reakci na interakci uživatele (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace mohou být spouštěny automaticky nebo mohou být aktivovány interakcí uživatele, například kliknutím myší.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace mohou být spouštěny automaticky nebo mohou být aktivovány interakcí uživatele, například kliknutím myší.

## <a name="steps"></a>Uvedené

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

V uzlu `<Animations>` existuje pět způsobů, jak spustit animaci prostřednictvím interakce s uživatelem (chybějící element je `<OnLoad>`, který je proveden po úplném načtení celé stránky):

- `<OnClick>` (kliknutí myší na ovládací prvek)
- `<OnHoverOut>` (myš opustí ovládací prvek)
- `<OnHoverOver>` (najetí myší nad ovládací prvek, zastavení `<OnHoverOut>` animace)
- `<OnMouseOut>` (opustí ovládací prvek myší)
- `<OnMouseOver>` (najetí myší na ovládací prvek, nezastavení `<OnMouseOut>` animace)

V tomto scénáři se používá `<OnClick>`. Když uživatel klikne na panel, změní se jeho velikost a zároveň se vykreslí.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

[![kliknutí myší se spustí animace](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)

Po kliknutí myší se spustí animace ([kliknutím zobrazíte obrázek v plné velikosti).](animating-in-response-to-user-interaction-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](picking-one-animation-out-of-a-list-vb.md)
> [Další](disabling-actions-during-animation-vb.md)
