---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: Dynamické řízení animací UpdatePanel (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 97a52bd75fdf63ad62282afd9df772f0a9e4f931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536153"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a>Dynamické řízení animací ovládacím prvkem UpdatePanel (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah ovládacího prvku UpdatePanel existuje speciální rozšířený objekt, který spoléhá na rámec animace: UpdatePanelAnimation. Může také spolupracovat s triggery UpdatePanel.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah `UpdatePanel`existuje speciální rozšířený objekt, který spoléhá na rámec animace: `UpdatePanelAnimation`. Může taky spolupracovat s triggery `UpdatePanel`.

## <a name="steps"></a>Kroky

Prvním krokem je obvykle zahrnutí `ScriptManager` do stránky, aby byla načtena knihovna ASP.NET AJAX a bylo možné použít ovládací sadu Toolkit:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

Animace v tomto scénáři se použije na zobrazení aktuálního času. Tyto informace lze zapsat do popisku pomocí `Page_Load()` metody, nebo (pro účely zjednodušení) je použit následující vložený kód:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

Také tlačítko pro aktivaci aktualizace času je vytvořeno:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

Tento kód je pak vložen do oddílu `<ContentTemplate>` `UpdatePanel` elementu. Atribut `UpdateMode` panelu musí být nastaven na hodnotu `"Conditional"`, protože triggery mohou aktualizovat pouze triggery obsahu panelu. V části `<Triggers>` `UpdatePanel`je vytvořen Trigger asynchronního postbacku a svázán s událostí `Click` tlačítka. Proto pokud uživatel klikne na tlačítko, `UpdatePanel` se aktualizuje. Zde je značka pro ovládací prvek `UpdatePanel`:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

Nakonec je třeba nakonfigurovat `UpdatePanelAnimationExtender`: nastavte atribut `TargetControlID` na ID panelu a definujte animaci v rámci tohoto zařízení. Je to v dobrém smyslu, což na aktualizovaném čase vytvoří skvělé vizuální zdůraznění. Značky zařízení může vypadat takto:

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

Spusťte soubor v prohlížeči. Kdykoliv kliknete na tlačítko, aktuální čas se zobrazí na panelu, vždy se bude zobrazovat po dobu trvání jedné sekundy.

[![aktuální čas je v čase](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)

Aktuální čas je v čase ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-controlling-updatepanel-animations-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](animating-an-updatepanel-control-vb.md)
