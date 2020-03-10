---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: Zpracování zpětného odeslání z ovládacího prvku modalpopup (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Zvláštní péči je potřeba vzít v případě POS...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554059"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a>Zpracování postbacků z ovládacího prvku ModalPopup (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)

> Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Při vytváření zpětného volání z místní nabídky je potřeba věnovat zvláštní péči.

## <a name="overview"></a>Přehled

Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Při vytváření zpětného volání z místní nabídky je potřeba věnovat zvláštní péči.

## <a name="steps"></a>Kroky

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

Dále přidejte panel, který slouží jako modální automaticky otevírané okno. Tam může uživatel zadat jméno a e-mailovou adresu. Tlačítko slouží k zavření automaticky otevíraného okna a uložení informací. Všimněte si, že atribut `OnClick` je nastaven tak, aby při kliknutí na toto tlačítko vznikl postback:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

Samotná stránka se skládá ze dvou popisků pro přesně stejné informace: jméno a e-mailová adresa. Tlačítko slouží k aktivaci modální překryvné nabídky:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

Chcete-li, aby se místní nabídka zobrazila, přidejte ovládací prvek `ModalPopupExtender`. Nastavte atribut `PopupControlID` na ID panelu a `TargetControlID` na ID tlačítka:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

Nyní, když se klikne na tlačítko `Save` v modálním překryvném okně, je provedena metoda `SaveData()` na straně serveru. V takovém případě můžete zadaná data uložit do úložiště dat. V zájmu jednoduchosti jsou nová data pouze výstupem v popisku:

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

Také ovládací prvky TextBox v modálním překryvném okně by měly být vyplněny aktuálním jménem a e-mailem. To je však nutné pouze v případě, že nedojde k postbacku. Pokud dojde k postbacku, funkce ASP.NET ViewState automaticky vyplní textová pole odpovídajícími hodnotami.

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

[![modálního automaticky otevíraného okna způsobí postback.](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)

Modální překryvné okno způsobí postback ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-modalpopup-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-modalpopup-with-a-repeater-control-cs.md)
> [Další](positioning-a-modalpopup-cs.md)
