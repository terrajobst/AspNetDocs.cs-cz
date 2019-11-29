---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: Umístění ovládacího prvku modalpopup (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: fb79a08a339588ed8adc4b4236911819ea9286b4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598971"
---
# <a name="positioning-a-modalpopup-vb"></a>Umístění ovládacího prvku ModalPopup (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)

> Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.

## <a name="overview"></a>Přehled

Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Ovládací prvek však nenabízí integrovanou funkci pro umístění místní nabídky.

## <a name="steps"></a>Uvedené

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, `ScriptManager`. ovládací prvek musí být umístěn kdekoli na stránce (ale v prvku `<form>`):

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

Dále přidejte panel, který slouží jako modální automaticky otevírané okno. Tlačítko slouží k zavření automaticky otevíraného okna:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

Pokaždé, když se zobrazí místní nabídka, je umístěna na určitém místě na stránce. Pro tuto úlohu je vytvořena funkce JavaScriptu na straně klienta. Nejprve se pokusí o přístup k panelu. V případě úspěchu se pozice panelu nastaví pomocí CSS a JavaScriptu (Změna pozice místní nabídky na). `ModalPopupExtender` ovládací prvek se ale také pokusí umístit automaticky otevírané okno. Proto kód JavaScriptu opakovaně umístí automaticky otevírané okno, každou desetinu sekundy.

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

Jak vidíte, návratová hodnota metody `setTimeout()` JavaScriptu je uložena v globální proměnné. To umožňuje zastavit opakované umístění místní nabídky na vyžádání pomocí `clearTimeout()` metody:

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

Vše, co zbývá udělat, je to, aby prohlížeč tyto funkce vyvolal, kdykoli to bude vhodné. Funkce `movePanel()` JavaScriptu musí být volána při kliknutí na tlačítko, které aktivuje panel:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

A funkce `stopMoving()` přijde do hry, když se zavře automaticky otevírané okno, může se aktivovat v ovládacím prvku `ModalPopupExtender`:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]

[![modální překryvné okno se zobrazí na určené pozici.](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)

Modální místní nabídka se zobrazí na určené pozici ([kliknutím zobrazíte obrázek v plné velikosti).](positioning-a-modalpopup-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](handling-postbacks-from-a-modalpopup-vb.md)
