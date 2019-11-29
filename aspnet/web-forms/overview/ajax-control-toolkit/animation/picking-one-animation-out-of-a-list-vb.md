---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: Výběr jedné animace ze seznamu (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Rozhraní také lze povolit...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 694416532b558291ff6ab57a442058b53d6167e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606756"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a>Výběr jedné animace ze seznamu (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Rozhraní také umožňuje programátorovi vybrat jednu animaci ze seznamu animací v závislosti na vyhodnocení kódu JavaScriptu.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Rozhraní také umožňuje programátorovi vybrat jednu animaci ze seznamu animací v závislosti na vyhodnocení kódu JavaScriptu.

## <a name="steps"></a>Uvedené

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla. Místo jedné z běžných animací se `<Case>` element přesune do hry. Hodnota jeho atributu SelectScript je vyhodnocena. Vrácená hodnota musí být číselná. V závislosti na tomto počtu se spustí jedna z podanimačních animací v &lt;případu&gt;. Pokud je například SelectScript vyhodnocena jako 2, sada nástrojů Control Toolkit spustí třetí animaci v &lt;případu&gt; (počítání začíná 0).

Následující kód definuje tři podanimace: mění velikost šířky, mění velikost výšky a slábnutí. Kód jazyka JavaScript (`Math.floor(3 * Math.random())`) pak vybere číslo mezi 0 a 2, aby se spouštěla jedna ze tří animací:

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]

[![jeden z možných tří animací: panel bude širší](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)

Jedním z možných tří animací: panel bude širší ([kliknutím zobrazíte obrázek v plné velikosti](picking-one-animation-out-of-a-list-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Předchozí](animation-depending-on-a-condition-vb.md)
> [Další](animating-in-response-to-user-interaction-vb.md)
