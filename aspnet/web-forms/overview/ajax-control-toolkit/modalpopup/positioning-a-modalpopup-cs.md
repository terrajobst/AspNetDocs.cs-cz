---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: Umístění ovládacího prvku modalpopup (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613223"
---
# <a name="positioning-a-modalpopup-c"></a>Umístění ovládacího prvku ModalPopup (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)

> Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.

## <a name="overview"></a>Přehled

Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.

## <a name="steps"></a>Kroky

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, `ScriptManager`. ovládací prvek musí být umístěn kdekoli na stránce (ale v prvku `<form>`):

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

Dále přidejte panel, který slouží jako modální automaticky otevírané okno. Tlačítko slouží k zavření automaticky otevíraného okna:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

Pokaždé, když se zobrazí místní nabídka, je umístěna na určitém místě na stránce. Pro tuto úlohu je vytvořena funkce JavaScriptu na straně klienta. Nejprve se pokusí o přístup k panelu. V případě úspěchu se pozice panelu nastaví pomocí CSS a JavaScriptu (Změna pozice místní nabídky na). `ModalPopupExtender` ovládací prvek se ale také pokusí umístit automaticky otevírané okno. Proto kód JavaScriptu opakovaně umístí automaticky otevírané okno, každou desetinu sekundy.

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

Jak vidíte, návratová hodnota metody `setTimeout()` JavaScriptu je uložena v globální proměnné. To umožňuje zastavit opakované umístění místní nabídky na vyžádání pomocí `clearTimeout()` metody:

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

Vše, co zbývá udělat, je to, aby prohlížeč tyto funkce vyvolal, kdykoli to bude vhodné. Funkce `movePanel()` JavaScriptu musí být volána při kliknutí na tlačítko, které aktivuje panel:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

A funkce `stopMoving()` přijde do hry, když se zavře automaticky otevírané okno, může se aktivovat v ovládacím prvku `ModalPopupExtender`:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

[![modální překryvné okno se zobrazí na určené pozici.](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)

Modální místní nabídka se zobrazí na určené pozici ([kliknutím zobrazíte obrázek v plné velikosti).](positioning-a-modalpopup-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](handling-postbacks-from-a-modalpopup-cs.md)
> [Další](launching-a-modal-popup-window-from-server-code-vb.md)
