---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: Zakázání akcí během animace (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Také podporuje akci...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536237"
---
# <a name="disabling-actions-during-animation-vb"></a>Zakázání akcí během animace (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Podporuje také akce, jako je kliknutí myší. Pokud se ale po kliknutí myší spustí animace, je žádoucí zakázat kliknutí myší během animace.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Podporuje také akce, jako je kliknutí myší. Pokud se ale po kliknutí myší spustí animace, je žádoucí zakázat kliknutí myší během animace.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

Animace se použije na tlačítko HTML jako toto:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

Všimněte si, že se místo webového ovládacího prvku používá ovládací prvek HTML, protože nechcete, aby tlačítko vytvořilo postback. Stačí spustit animaci na straně klienta pro nás.

Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

V uzlu `<Animations>` je `<OnClick>` pravého prvku pro zpracování kliknutí myší. Tlačítko však může být kliknuto i během animace. Element `<EnableAction>` se může postarat. Nastavení `Enabled="false"` zakáže tlačítko v rámci animace. Vzhledem k tomu, že používáme několik jednotlivých animací (zakážete tlačítko a skutečné animace), `<Parallel>` element je nutný k vzájemnému připevnění jednotlivých animací. Toto je kompletní označení pro `AnimationExtender`:

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

Je také možné znovu povolit tlačítko po animaci, a to pomocí následujícího elementu XML na konci seznamu:

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

V daném scénáři to však nebude k dispozici, protože tlačítko zmizí a na konci animace není vidět.

[![tlačítko je po spuštění animace zakázané.](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

Tlačítko je zakázáno, jakmile se spustí animace ([kliknutím zobrazíte obrázek v plné velikosti).](disabling-actions-during-animation-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](animating-in-response-to-user-interaction-vb.md)
> [Další](triggering-an-animation-in-another-control-vb.md)
