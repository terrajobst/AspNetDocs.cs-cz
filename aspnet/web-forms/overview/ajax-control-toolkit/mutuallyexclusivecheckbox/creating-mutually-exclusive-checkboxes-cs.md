---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: Vytváření vzájemně se vylučujícíchC#zaškrtávacích políček () | Microsoft Docs
author: wenz
description: 'Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka. Došlo k nevýhodě, i když: je vybráno jedno přepínač ve skupině,...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606504"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a>Vytvoření vzájemně se vylučujících zaškrtávacích políček (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)

> Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka. Došlo k nevýhodě, i když: Když vyberete jeden přepínač ve skupině, není možné zrušit kontrolu všech přepínačů. Zaškrtávací políčka je možné kdykoli zrušit, ale vzájemně se nevylučují. Tento kurz nabízí nejlepší z obou přístupů: zaškrtávací políčka, která se vzájemně vylučují.

## <a name="overview"></a>Přehled

Je-li možné vybrat pouze jednu ze sad možností, jsou obvykle použity přepínací tlačítka. Došlo k nevýhodě, i když: Když vyberete jeden přepínač ve skupině, není možné zrušit kontrolu všech přepínačů. Zaškrtávací políčka je možné kdykoli zrušit, ale vzájemně se nevylučují. Tento kurz nabízí nejlepší z obou přístupů: zaškrtávací políčka, která se vzájemně vylučují.

## <a name="steps"></a>Uvedené

Sada ASP.NET AJAX Control Toolkit obsahuje MutuallyExclusiveCheckBox a Extender. To umožňuje programátorům přiřadit libovolné zaškrtávací políčko k názvu skupiny (`Key` atribut). Všechna zaškrtávací políčka v rámci stejné skupiny se dají vybrat jenom jednou.

Začněte tím, že na nové stránce ASP.NET vložíte dvě zaškrtávací políčka. Může to být více, ale dva z nich jsou dostačující k předvedení principu:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

Pro obě zaškrtávací políčka musí být ovládací prvek MutuallyExclusiveCheckBoxExtender vložen na stránku. Oba atributy klíče musí mít stejnou hodnotu, stejně jako atributy hodnoty prvků přepínače HTML musí být identické, aby se shodovaly s tím, do které skupiny patří. Vlastnost vlastnost TargetControlID prvku objektu Extender odkazuje na ID zaškrtávacího políčka.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

Nakonec zahrňte ASP.NET AJAX `ScriptManager`, který je vyžadován všemi prvky sady ASP.NET AJAX Control Toolkit:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

Uložte a spusťte stránku: můžete zaškrtnout a zrušit zaškrtnutí obou políček, avšak současně by nebylo možné zaškrtnout obě zaškrtávací políčka.

[![může být současně zaškrtnuto pouze jedno zaškrtávací políčko.](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)

Současně může být zaškrtnuto pouze jedno zaškrtávací políčko ([kliknutím zobrazíte obrázek v plné velikosti).](creating-mutually-exclusive-checkboxes-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](creating-mutually-exclusive-checkboxes-vb.md)
