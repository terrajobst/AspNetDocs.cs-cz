---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: Použití ovládacího prvku textboxwatermark s ovládacími prvky ověřování (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku textboxwatermark v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text. Když uživatel klikne do pole, i...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597240"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>Použití ovládacího prvku TextBoxWatermark s validačními ovládacími prvky (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> Ovládací prvek ovládacího prvku textboxwatermark v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text. Když uživatel klikne na pole, bude vyprázdněn. Pokud uživatel opustí pole bez zadání textu, předem vyplněný text se zobrazí znovu. To může kolidovat s ovládacími prvky ověřování ASP.NET na stejné stránce, ale tyto problémy se můžou překonat.

## <a name="overview"></a>Přehled

Ovládací prvek `TextBoxWatermark` v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text. Když uživatel klikne na pole, bude vyprázdněn. Pokud uživatel opustí pole bez zadání textu, předem vyplněný text se zobrazí znovu. To může kolidovat s ovládacími prvky ověřování ASP.NET na stejné stránce, ale tyto problémy se můžou překonat.

## <a name="steps"></a>Uvedené

Základní nastavení ukázky je následující: ovládací prvek `TextBox` má vodoznak pomocí ovládacího prvku `TextBoxWatermarkExtender`. Tlačítko aktivuje postback a později bude použito ke spuštění ovládacích prvků ověřování na stránce. Pro inicializaci ASP.NET AJAX je také vyžadován ovládací prvek `ScriptManager`:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

Nyní přidejte ovládací prvek `RequiredFieldValidator`, který zkontroluje, zda je v poli při odeslání formuláře text. Vlastnost `InitialValue` validátoru musí být nastavena na stejnou hodnotu, která se používá v ovládacím prvku `TextBoxWatermarkExtender`: při odeslání formuláře je hodnota nezměněného textového pole hodnotou meze v této podobě:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

Existuje však jeden problém s tímto přístupem: Pokud klient zakáže JavaScript, textové pole není předem vyplněno textem vodoznaku, proto `RequiredFieldValidator` nespustí chybovou zprávu. Proto je vyžadován druhý `RequiredFieldValidator` ovládací prvek, který kontroluje prázdné textové pole (s vynecháním `InitialValue` atributu).

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

Vzhledem k tomu, že oba validátory používají `Display`=`"Dynamic"`, nemůže koncový uživatel rozlišovat od vizuálního vzhledu, který vyvolaly dva validátory. místo toho se zdá, že existovala pouze jedna z nich.

Nakonec přidejte nějaký kód na straně serveru pro výstup textu do pole, pokud žádný validátor nevystavil chybovou zprávu:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

[![stížnosti validátoru, že v poli není žádný text](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

Validátor vyplatí, že v poli není žádný text ([kliknutím zobrazíte obrázek v plné velikosti).](using-textboxwatermark-with-validation-controls-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-textboxwatermark-in-a-formview-vb.md)
