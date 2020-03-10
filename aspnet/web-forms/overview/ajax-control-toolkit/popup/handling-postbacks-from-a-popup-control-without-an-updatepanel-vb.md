---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: Zpracování zpětného volání z překryvného ovládacího prvku bez prvku UpdatePanel (VB) | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Když dojde k postbacku v Su...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553982"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a>Zpracování postbacků ovládacího prvku PopupControl bez ovládacího prvku UpdatePanel (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)

> PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Pokud dojde k postbacku na takovém panelu a na stránce je několik panelů, je obtížné určit, na který panel byl kliknuto.

## <a name="overview"></a>Přehled

PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Pokud dojde k postbacku na takovém panelu a na stránce je několik panelů, je obtížné určit, na který panel byl kliknuto.

## <a name="steps"></a>Kroky

Při použití `PopupControl` s zpětným voláním, ale bez `UpdatePanel` na stránce, sada nástrojů Control Toolkit nenabízí způsob, jak určit, který prvek klienta aktivoval automaticky otevírané okno, které způsobilo zpětné odeslání. Malý štych ale poskytuje alternativní řešení pro tento scénář.

První ze všech, zde je základní nastavení: dvě textová pole, která obě spustí stejnou místní nabídku, kalendář. Dva `PopupControlExtenders` přenášet textová pole a automaticky otevíraná okna.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

Základní nápad je přidat skryté pole formuláře do &lt;`form`&gt; elementu, který obsahuje textové pole, ve kterém se spustila automaticky otevíraná okna:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

Při načtení stránky kód JavaScriptu přidá obslužnou rutinu události do obou textových polí: vždy, když uživatel klikne na textové pole, jeho název se zapíše do skrytého pole formuláře:

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

V kódu na straně serveru musí být hodnota skrytého pole přečtena. Vzhledem k tomu, že skrytá pole formuláře jsou triviální pro manipulaci, je požadován přístup povolený k ověření skryté hodnoty. Po identifikaci správného textového pole se do něj zapíše datum z kalendáře.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

[![kalendáři se zobrazí, když uživatel klikne do textového pole.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)

Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png)

[![kliknutí na datum vloží do textového pole.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)

Kliknutím na datum se vloží do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
