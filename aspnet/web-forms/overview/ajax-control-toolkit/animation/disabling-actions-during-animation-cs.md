---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: Zakázání akcí během animace (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Také podporuje akci...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: e91205ad2f9e6ee1fdd869ceb7587c3a82754772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536265"
---
# <a name="disabling-actions-during-animation-c"></a>Zakázání akcí během animace (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Podporuje také akce, jako je kliknutí myší. Pokud se ale po kliknutí myší spustí animace, je žádoucí zakázat kliknutí myší během animace.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Podporuje také akce, jako je kliknutí myší. Pokud se ale po kliknutí myší spustí animace, je žádoucí zakázat kliknutí myší během animace.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

Animace se použije na tlačítko HTML jako toto:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

Všimněte si, že se místo webového ovládacího prvku používá ovládací prvek HTML, protože nechcete, aby tlačítko vytvořilo postback. Stačí spustit animaci na straně klienta pro nás.

Pak přidejte `AnimationExtender` na stránku a zadejte `ID`, atribut `TargetControlID` a povinný `runat="server"`:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

V uzlu `<Animations>` je `<OnClick>` pravého prvku pro zpracování kliknutí myší. Tlačítko však může být kliknuto i během animace. Element `<EnableAction>` se může postarat. Nastavení `Enabled="false"` zakáže tlačítko v rámci animace. Vzhledem k tomu, že používáme několik jednotlivých animací (zakážete tlačítko a skutečné animace), `<Parallel>` element je nutný k vzájemnému připevnění jednotlivých animací. Toto je kompletní označení pro `AnimationExtender`:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

Je také možné znovu povolit tlačítko po animaci, a to pomocí následujícího elementu XML na konci seznamu:

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

V daném scénáři to však nebude k dispozici, protože tlačítko zmizí a na konci animace není vidět.

[![tlačítko je po spuštění animace zakázané.](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)

Tlačítko je zakázáno, jakmile se spustí animace ([kliknutím zobrazíte obrázek v plné velikosti).](disabling-actions-during-animation-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](animating-in-response-to-user-interaction-cs.md)
> [Další](triggering-an-animation-in-another-control-cs.md)
