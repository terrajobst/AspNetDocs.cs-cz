---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: Přidání animace do ovládacího prvku (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. V tomto kurzu se dozvíte, jak...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598299"
---
# <a name="adding-animation-to-a-control-vb"></a>Přidání animace k ovládacímu prvku (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. V tomto kurzu se dozvíte, jak nastavit takovou animaci.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. V tomto kurzu se dozvíte, jak nastavit takovou animaci.

## <a name="steps"></a>Kroky

Prvním krokem je obvykle zahrnutí `ScriptManager` do stránky, aby byla načtena knihovna ASP.NET AJAX a bylo možné použít ovládací sadu Toolkit:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

Animace v tomto scénáři se použije na panel textu, který vypadá nějak takto:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

Přidružená Třída CSS pro panel definuje barvu pozadí a šířku:

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

V dalším kroku potřebujeme `AnimationExtender`. Po poskytnutí `ID` a obvyklých `runat="server"`musí být atribut `TargetControlID` nastaven na řízení pro animaci v našem případě, panel:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

Celá animace se aplikuje deklarativně pomocí syntaxe XML, ale v současné době není plně podporovaná IntelliSense sady Visual Studio. Kořenový uzel je `<Animations>;` v rámci tohoto uzlu, jsou povoleny různé události, které určují, kdy se mají tyto animace (y) použít:

- `OnClick` (kliknutí myší)
- `OnHoverOut` (když myš opustí ovládací prvek)
- `OnHoverOver` (když ukazatel myši setrvá na ovládacím prvku, zastaví se animace `OnHoverOut`).
- `OnLoad` (při načtení stránky)
- `OnMouseOut` (když myš opustí ovládací prvek)
- `OnMouseOver` (když ukazatel myši setrvá na ovládacím prvku, nezastaví se `OnMouseOut` animace).

Rozhraní obsahuje sadu animací, každý z nich reprezentované vlastním prvkem XML. Tady je výběr:

- `<Color>` (změna barvy)
- `<FadeIn>` (stromeček)
- `<FadeOut>` (stromeček)
- `<Property>` (Změna vlastnosti ovládacího prvku)
- `<Pulse>` (PULSATING)
- `<Resize>` (Změna velikosti)
- `<Scale>` (proporcionálně se mění velikost)

V tomto příkladu je panel vymizet. Animace musí trvat 1,5 sekund (`Duration` atribut), přičemž se zobrazí 24 snímků (kroky animace) za sekundu (atribut`Fps`). Zde je kompletní označení pro ovládací prvek `AnimationExtender`:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

Když spustíte tento skript, panel se zobrazí a zmizí v jednom a půl sekundách.

[![panelu se dozvíte](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

Panel se zobrazuje na více instancí ([kliknutím zobrazíte obrázek v plné velikosti).](adding-animation-to-a-control-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](dynamically-controlling-updatepanel-animations-cs.md)
> [Další](executing-several-animations-at-the-same-time-vb.md)
