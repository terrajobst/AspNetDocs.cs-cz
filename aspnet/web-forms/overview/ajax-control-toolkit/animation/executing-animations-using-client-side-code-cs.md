---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: Spouštění animací pomocí kódu na straně klienta (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Spuštění animace...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b6ba1553b9c8c51d5d6ae1679e53f9cc1d17b769
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598180"
---
# <a name="executing-animations-using-client-side-code-c"></a>Spuštění animací klientským kódem (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Spuštění animace se může také aktivovat pomocí vlastního kódu JavaScriptu na straně klienta.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Spuštění animace se může také aktivovat pomocí vlastního kódu JavaScriptu na straně klienta.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

V uzlu `<Animations>` pomocí `<OnClick>` spustit animace, jakmile uživatel klikne na panel. Přidejte dvě animace, které se mají spustit paralelně:

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

Pro účely ukázky je tato animace (a jakákoli jiná animace vytvořená pomocí sady Control Toolkit) spouštěna pomocí kódu jazyka JavaScript po spuštění stránky. Nejdřív potřebujeme přístup k ovládacímu prvku `AnimationExtender`. Knihovna ASP.NET AJAX poskytuje funkci `$find()` pro tuto úlohu:

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

Ovládací prvek `AnimationExtender` zpřístupňuje bohatá rozhraní API, včetně metod s názvy shodnými s obslužnými rutinami událostí použitými v kódu XML: `OnClick()`, `OnLoad()`a tak dále. Například volání metody `OnClick()` spustí animaci v rámci elementu `<OnClick>` ovládacího prvku `AnimationExtender`:

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

Zde je kompletní kód JavaScriptu na straně klienta, který emuluje kliknutí na panel po úplném načtení stránky, Všimněte si, že se používá název funkce `pageLoad()`, který je volán ASP.NET AJAX po načtení stránky a všech zahrnutých knihoven JavaScriptu.

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

[![se animace spustí hned bez kliknutí myší.](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)

Animace se spustí okamžitě bez kliknutí myší ([kliknutím zobrazíte obrázek v plné velikosti).](executing-animations-using-client-side-code-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](modifying-animations-from-the-server-side-cs.md)
> [Další](changing-an-animation-using-client-side-code-cs.md)
