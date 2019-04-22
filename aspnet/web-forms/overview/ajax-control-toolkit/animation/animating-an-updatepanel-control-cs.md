---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Animace ovládacího prvku UpdatePanel (C#) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Pro obsah...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 36d1166e1bd2b4c97b3cf3dd0bc3a7e8010a9443
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393688"
---
# <a name="animating-an-updatepanel-control-c"></a>Animace ovládacího prvku UpdatePanel (C#)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Obsah prvku UpdatePanel existuje speciální rozšiřujícího objektu, která se spoléhá na rozhraní .NET framework animace: UpdatePanelAnimation. Tento kurz ukazuje, jak nastavit tyto animace ovládacího prvku UpdatePanel.


## <a name="overview"></a>Přehled

Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Pro obsah `UpdatePanel`, speciální rozšiřující objekt existuje, která se spoléhá na rozhraní .NET framework animace: `UpdatePanelAnimation`. Tento kurz ukazuje, jak nastavit tyto animace pro `UpdatePanel`.

## <a name="steps"></a>Kroky

Prvním krokem je jako obvykle zahrnují `ScriptManager` na stránce tak, aby je načtena knihovna ASP.NET AJAX a Control Toolkit je možné:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

Animace v tomto scénáři se použijí pro ASP.NET `Wizard` webový ovládací prvek umístěný v `UpdatePanel`. Tři kroky (libovolný) obsahují dostatek možnosti k aktivaci zpětného odeslání:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

Pro značky `UpdatePanelAnimationExtender` je velmi podobný značky použité pro ovládací prvek `AnimationExtender`. V `TargetControlID` atribut zajišťuje `ID` z `UpdatePanel` pro animaci; v rámci `UpdatePanelAnimationExtender` ovládací prvek, `<Animations>` element obsahuje kód XML pro animace. Nicméně je jedním z rozdílů: Objem událostí a obslužných rutin událostí je omezená ve srovnání s `AnimationExtender`. Pro `UpdatePanels`, pouze dva z nich neexistuje:

- `<OnUpdated>` Pokud byl aktualizován prvku UpdatePanel
- `<OnUpdating>` Aktualizuje se při spuštění prvku UpdatePanel

V tomto scénáři, nový obsah `UpdatePanel` (po zpětném volání) se má vyblednout. To je nezbytné zápis, který:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

Nyní pokaždé, když se vyvolá se v rámci prvku UpdatePanel zpětné volání, nový obsah na panelu fade plynule.


[![V dalším kroku průvodce se pozvolného](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

V dalším kroku průvodce se pozvolného ([kliknutím ji zobrazíte obrázek v plné velikosti](animating-an-updatepanel-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Předchozí](changing-an-animation-using-client-side-code-cs.md)
> [další](dynamically-controlling-updatepanel-animations-cs.md)
