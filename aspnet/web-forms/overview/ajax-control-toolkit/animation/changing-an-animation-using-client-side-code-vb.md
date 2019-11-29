---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: Změna animace pomocí kódu na straně klienta (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace může také...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: cce0a5a901f71edd40eada59ac7eeba93222e2b3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606922"
---
# <a name="changing-an-animation-using-client-side-code-vb"></a>Změna animace klientským kódem (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animaci lze také změnit pomocí vlastního kódu JavaScriptu na straně klienta.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animaci lze také změnit pomocí vlastního kódu JavaScriptu na straně klienta.

## <a name="steps"></a>Uvedené

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

Skutečná animace se spustí tlačítkem HTML:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

Všimněte si, že v ovládacím prvku `AnimationExtender` není žádný `<Animations>` uzel. Vlastní kód JavaScriptu slouží k poskytnutí animací pro použití s ovládacím prvkem.

Stejně jako u rozhraní API serveru `AnimationExtender`neexistuje jednoduchý způsob, jak přiřadit animaci k tomuto zařízení. Nicméně modul pro rozšiřování vystavuje několik metod pro čtení a zápis animací zaregistrovaných v různých událostech (`OnClick`, `OnLoad`a tak dále). Následuje několik příkladů:

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

Formát návratové hodnoty funkcí `get_*()` a formát argumentu pro funkce `set_*()` je řetězec JSON, který poskytuje objekt reprezentující, co by byl kód XML. V současné době neexistuje způsob, jak objekt předat, ale je možné číst objekt z dané animace (`get_OnXXXBehavior()` metody).

Tady je řetězec JSON (bez uvozovek a formátovaného textu) představující animaci, která se aktivovala tlačítkem, ale animování panelu změnou velikosti a postupným postupným postupným navýšení.

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

Následující kód jazyka JavaScript přiřadí tento znak JSON ke `OnClick` animaci aktuálního a spustí ho:

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]

[![se animace spouští okamžitě bez kliknutí myší (a s velmi malým označením).](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)

Animace se spustí okamžitě, bez kliknutí myší (a s velmi malým označením) ([kliknutím zobrazíte obrázek v plné velikosti).](changing-an-animation-using-client-side-code-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](executing-animations-using-client-side-code-vb.md)
> [Další](animating-an-updatepanel-control-vb.md)
