---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: Animace v závislosti na podmínce (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Zda je animace...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 583ebdbf109beb74b9a425020477183067bbb79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607024"
---
# <a name="animation-depending-on-a-condition-vb"></a>Animace závislá na podmínce (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Zda je animace spuštěna, nebo ne, může také záviset na stavu ve formě některého kódu JavaScriptu.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Zda je animace spuštěna, nebo ne, může také záviset na stavu ve formě některého kódu JavaScriptu.

## <a name="steps"></a>Uvedené

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

Pak přidejte `AnimationExtender` na stránku a poskytněte `ID`, atribut `TargetControlID` a povinný `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

V uzlu `<Animations>` pomocí `<OnLoad>` spustit animace, jakmile se stránka kompletně načetla. Místo jedné z běžných animací se `<Condition>` element přesune do hry. Kód jazyka JavaScript poskytnutý jako hodnota atributu `ConditionScript` se spustí za běhu. Pokud se vyhodnotí jako true, spustí se animace, jinak ne. Následující kód poskytuje dvě animace, každý z nich je spuštěn v 50% případů po náhodném provedení. Vzhledem k tomu, že v `<OnLoad>`může existovat pouze jedna animace, jsou tyto dvě `<Condition>` animace spojeny společně pomocí elementu `<Sequence>`:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

Všimněte si, že znaménko menší než (`<`) v atributu `ConditionScript` musí mít řídicí znak (). Spouštíte-li tento skript, buď žádná animace neběží, nebo jeden z těchto dvou testů nebo obojí.

[![je panel bez změny velikosti, takže se druhá animace spustí, první z nich se nezměnila.](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

Panel se vypustil bez změny velikosti, takže se druhá animace spustí poprvé ([kliknutím zobrazíte obrázek v plné velikosti).](animation-depending-on-a-condition-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](executing-several-animations-after-each-other-vb.md)
> [Další](picking-one-animation-out-of-a-list-vb.md)
