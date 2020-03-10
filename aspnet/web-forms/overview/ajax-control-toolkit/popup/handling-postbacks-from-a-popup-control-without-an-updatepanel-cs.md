---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: Zpracování zpětného volání z překryvného ovládacího prvku bez prvkuC#UpdatePanel () | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Když dojde k postbacku v Su...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612740"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>Zpracování postbacků ovládacího prvku PopupControl bez ovládacího prvku UpdatePanel (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Pokud dojde k postbacku na takovém panelu a na stránce je několik panelů, je obtížné určit, na který panel byl kliknuto.

## <a name="overview"></a>Přehled

PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Pokud dojde k postbacku na takovém panelu a na stránce je několik panelů, je obtížné určit, na který panel byl kliknuto.

## <a name="steps"></a>Kroky

Při použití `PopupControl` s zpětným voláním, ale bez `UpdatePanel` na stránce, sada nástrojů Control Toolkit nenabízí způsob, jak určit, který prvek klienta aktivoval automaticky otevírané okno, které způsobilo zpětné odeslání. Malý štych ale poskytuje alternativní řešení pro tento scénář.

První ze všech, zde je základní nastavení: dvě textová pole, která obě spustí stejnou místní nabídku, kalendář. Dva `PopupControlExtenders` přenášet textová pole a automaticky otevíraná okna.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

Základní nápad je přidat skryté pole formuláře do &lt;`form`&gt; elementu, který obsahuje textové pole, ve kterém se spustila automaticky otevíraná okna:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

Při načtení stránky kód JavaScriptu přidá obslužnou rutinu události do obou textových polí: vždy, když uživatel klikne na textové pole, jeho název se zapíše do skrytého pole formuláře:

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

V kódu na straně serveru musí být hodnota skrytého pole přečtena. Vzhledem k tomu, že skrytá pole formuláře jsou triviální pro manipulaci, je požadován přístup povolený k ověření skryté hodnoty. Po identifikaci správného textového pole se do něj zapíše datum z kalendáře.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[![kalendáři se zobrazí, když uživatel klikne do textového pole.](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)

[![kliknutí na datum vloží do textového pole.](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

Kliknutím na datum se vloží do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [Další](using-multiple-popup-controls-vb.md)
