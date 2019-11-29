---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: Aktivace animace v jiném ovládacím prvku (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Obecně se spouští...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: e0a1f8986047da04db6fde8e54b6fd0ac6ee2603
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599603"
---
# <a name="triggering-an-animation-in-another-control-c"></a>Aktivace animace jiného ovládacího prvku (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Obecně se spouští animace pomocí interakce uživatele se stejným ovládacím prvkem. Je však také možné pracovat s jedním ovládacím prvkem a následně animacem jiného ovládacího prvku.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Obecně se spouští animace pomocí interakce uživatele se stejným ovládacím prvkem. Je však také možné pracovat s jedním ovládacím prvkem a následně animacem jiného ovládacího prvku.

## <a name="steps"></a>Uvedené

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

Aby bylo možné začít animovat panel, je použito tlačítko HTML. Všimněte si, že `<input type="button" />` je výhodnější pro `<asp:Button />`, protože nepožadujeme postback, když uživatel na toto tlačítko klikne.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server"`. Je důležité nastavit `TargetControlID` na ID tlačítka (element, který aktivuje animaci), nikoli na ID panelu (element je animovaný).

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

V uzlu `<Animations>` umístěte animace obvyklým způsobem. Aby bylo možné změnit panel, nikoli tlačítko, nastavte atribut `AnimationTarget` pro všechny elementy animace v rámci `AnimationExtender`. Hodnota pro `AnimationTarget` je ID panelu kurzu. Tímto způsobem se animace vyskytují s panelem, nikoli s tlačítkem aktivovat. Tady je `AnimationExtender` značky pro tento scénář:

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

Všimněte si speciálního pořadí, ve kterém se jednotlivé animace zobrazí. Nejprve se tlačítko po spuštění animace deaktivuje. Vzhledem k tomu, že v elementu `<EnableAction>` není žádný atribut `AnimationTarget`, tato animace se aplikuje na ovládací prvek původce: tlačítko. Následující dva kroky animace je třeba provést paralelně (`<Parallel>` element). Oba mají své `AnimationTarget` atributy nastavené na `"Panel1"`, takže animován panel, ne tlačítko.

[![kliknutí myší na tlačítko spustí animaci panelu](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)

Kliknutím na tlačítko myši na tlačítko se spustí animace panelu ([kliknutím zobrazíte obrázek v plné velikosti).](triggering-an-animation-in-another-control-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](disabling-actions-during-animation-cs.md)
> [Další](modifying-animations-from-the-server-side-cs.md)
