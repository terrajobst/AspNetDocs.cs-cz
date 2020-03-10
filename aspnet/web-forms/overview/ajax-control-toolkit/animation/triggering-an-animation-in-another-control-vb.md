---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: Aktivace animace v jiném ovládacím prvku (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Obecně se spouští...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536069"
---
# <a name="triggering-an-animation-in-another-control-vb"></a>Aktivace animace jiného ovládacího prvku (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Obecně se spouští animace pomocí interakce uživatele se stejným ovládacím prvkem. Je však také možné pracovat s jedním ovládacím prvkem a následně animacem jiného ovládacího prvku.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Obecně se spouští animace pomocí interakce uživatele se stejným ovládacím prvkem. Je však také možné pracovat s jedním ovládacím prvkem a následně animacem jiného ovládacího prvku.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

Aby bylo možné začít animovat panel, je použito tlačítko HTML. Všimněte si, že `<input type="button" />` je výhodnější pro `<asp:Button />`, protože nepožadujeme postback, když uživatel na toto tlačítko klikne.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server"`. Je důležité nastavit `TargetControlID` na ID tlačítka (element, který aktivuje animaci), nikoli na ID panelu (element je animovaný).

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

V uzlu `<Animations>` umístěte animace obvyklým způsobem. Aby bylo možné změnit panel, nikoli tlačítko, nastavte atribut `AnimationTarget` pro všechny elementy animace v rámci `AnimationExtender`. Hodnota pro `AnimationTarget` je ID panelu kurzu. Tímto způsobem se animace vyskytují s panelem, nikoli s tlačítkem aktivovat. Tady je `AnimationExtender` značky pro tento scénář:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

Všimněte si speciálního pořadí, ve kterém se jednotlivé animace zobrazí. Nejprve se tlačítko po spuštění animace deaktivuje. Vzhledem k tomu, že v elementu `<EnableAction>` není žádný atribut `AnimationTarget`, tato animace se aplikuje na ovládací prvek původce: tlačítko. Následující dva kroky animace je třeba provést paralelně (`<Parallel>` element). Oba mají své `AnimationTarget` atributy nastavené na `"Panel1"`, takže animován panel, ne tlačítko.

[![kliknutí myší na tlačítko spustí animaci panelu](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

Kliknutím na tlačítko myši na tlačítko se spustí animace panelu ([kliknutím zobrazíte obrázek v plné velikosti).](triggering-an-animation-in-another-control-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](disabling-actions-during-animation-vb.md)
> [Další](modifying-animations-from-the-server-side-vb.md)
