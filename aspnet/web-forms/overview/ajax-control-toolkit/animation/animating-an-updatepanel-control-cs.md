---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Animace ovládacího prvku UpdatePanel (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536377"
---
# <a name="animating-an-updatepanel-control-c"></a>Animace ovládacího prvku UpdatePanel (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah ovládacího prvku UpdatePanel existuje speciální rozšířený objekt, který spoléhá na rámec animace: UpdatePanelAnimation. V tomto kurzu se dozvíte, jak nastavit takovou animaci pro UpdatePanel.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Pro obsah `UpdatePanel`existuje speciální rozšířený objekt, který spoléhá na rámec animace: `UpdatePanelAnimation`. V tomto kurzu se dozvíte, jak nastavit takovou animaci pro `UpdatePanel`.

## <a name="steps"></a>Kroky

Prvním krokem je obvykle zahrnutí `ScriptManager` do stránky, aby byla načtena knihovna ASP.NET AJAX a bylo možné použít ovládací sadu Toolkit:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

Animace v tomto scénáři bude použita na ASP.NET `Wizard` webový ovládací prvek umístěný v `UpdatePanel`. Tři (libovolné) kroky poskytují dostatek možností pro aktivaci zpětného volání:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

Označení potřebné pro ovládací prvek `UpdatePanelAnimationExtender` je poměrně podobné označení používanému pro `AnimationExtender`. V atributu `TargetControlID` poskytujeme `ID` `UpdatePanel` k animaci; v rámci ovládacího prvku `UpdatePanelAnimationExtender` prvek `<Animations>` obsahuje kód XML pro animace (y). Existuje však jeden rozdíl: množství událostí a obslužných rutin událostí je omezeno na porovnání s `AnimationExtender`. Pro `UpdatePanels`existují jenom dva z nich:

- `<OnUpdated>` při aktualizaci prvku UpdatePanel
- `<OnUpdating>` při zahájení aktualizace ovládacího prvku UpdatePanel

V tomto scénáři se nový obsah `UpdatePanel` (po zpětném vystavení) rozzvolna. Toto je nezbytné označení pro:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

Nyní, když dojde k postbacku v rámci prvku UpdatePanel, je nový obsah panelu plynule rozzvolna.

[![je další krok v průvodci slábnutí](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

V dalším kroku průvodce se[nezobrazuje (Kliknutím zobrazíte obrázek v plné velikosti).](animating-an-updatepanel-control-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](changing-an-animation-using-client-side-code-cs.md)
> [Další](dynamically-controlling-updatepanel-animations-cs.md)
