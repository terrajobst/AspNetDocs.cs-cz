---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: Animace v závislosti na podmínce (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Zda je animace...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599859"
---
# <a name="animation-depending-on-a-condition-c"></a>Animace závislá na podmínce (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Zda je animace spuštěna, nebo ne, může také záviset na stavu ve formě některého kódu JavaScriptu.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Zda je animace spuštěna, nebo ne, může také záviset na stavu ve formě některého kódu JavaScriptu.

## <a name="steps"></a>Uvedené

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla. Místo jedné z běžných animací se `<Condition>` element přesune do hry. Kód jazyka JavaScript poskytnutý jako hodnota atributu `ConditionScript` se spustí za běhu. Pokud se vyhodnotí jako true, spustí se animace, jinak ne. Následující kód poskytuje dvě animace, každý z nich je spuštěn v 50% případů po náhodném provedení. Vzhledem k tomu, že v `<OnLoad>`může existovat pouze jedna animace, jsou tyto dvě `<Condition>` animace spojeny společně pomocí elementu `<Sequence>`:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

Všimněte si, že znaménko menší než (`<`) v atributu `ConditionScript` musí mít řídicí znak (). Spouštíte-li tento skript, buď žádná animace neběží, nebo jeden z těchto dvou testů nebo obojí.

[![je panel bez změny velikosti, takže se druhá animace spustí, první z nich se nezměnila.](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

Panel se vypustil bez změny velikosti, takže se druhá animace spustí poprvé ([kliknutím zobrazíte obrázek v plné velikosti).](animation-depending-on-a-condition-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](executing-several-animations-after-each-other-cs.md)
> [Další](picking-one-animation-out-of-a-list-cs.md)
