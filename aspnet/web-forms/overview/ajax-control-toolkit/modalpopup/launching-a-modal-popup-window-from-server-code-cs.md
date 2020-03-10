---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: Spuštění modálního překryvného okna ze serverovéhoC#kódu () | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Některé scénáře ale vyžadují tuto t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: fec0ce2cdd24333f65201301718440e1a09d930e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613293"
---
# <a name="launching-a-modal-popup-window-from-server-code-c"></a>Spuštění okna modální místní nabídky serverovým kódem (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)

> Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Některé scénáře však vyžadují, aby bylo otevření modální nabídky na straně serveru spuštěno.

## <a name="overview"></a>Přehled

Ovládací prvek ovládacího prvku modalpopup v sadě nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální nabídku pomocí prostředků na straně klienta. Některé scénáře však vyžadují, aby bylo otevření modální nabídky na straně serveru spuštěno.

## <a name="steps"></a>Kroky

Nejprve je třeba webový ovládací prvek ASP.NET tlačítka, který ukazuje, jak funguje ovládací prvek ovládacího prvku modalpopup. Přidejte takové tlačítko do&gt; elementu &lt;formuláře na nové stránce:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

Pak budete potřebovat označení pro místní nabídku, kterou chcete vytvořit. Definujte ho jako ovládací prvek `<asp:Panel>` a ujistěte se, že obsahuje ovládací prvek tlačítko. Ovládací prvek ovládacího prvku modalpopup nabízí funkci, aby toto tlačítko zavřelo překryvné okno; jinak neexistuje žádný snadný způsob, jak to umožnit, aby zmizel.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

Dále přidejte ovládací prvek ovládacího prvku modalpopup z ASP.NET AJAX Toolkit na stránku. Nastavte vlastnosti pro tlačítko, které načte ovládací prvek, tlačítko, které zmizí, a ID skutečné překryvné nabídky.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

Stejně jako všechny webové stránky založené na ASP.NET AJAX; Správce skriptů je nutný k načtení nezbytných knihoven JavaScriptu pro různé cílové prohlížeče:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

Spusťte příklad v prohlížeči. Po kliknutí na tlačítko se zobrazí modální okno. Aby bylo možné dosáhnout stejného účinku pomocí kódu na straně serveru, je vyžadováno nové tlačítko:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

Jak vidíte, kliknutí na tlačítko vygeneruje postback a spustí metodu `ServerButton_Click()` na serveru. V této metodě je funkce JavaScriptu, která se nazývá `launchModal()`, prováděna přesně, funkce JavaScriptu se spustí po načtení stránky:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

Úkolem `launchModal()` je zobrazit ovládacího prvku modalpopup. Funkce `launchModal()` je provedena po načtení kompletní stránky HTML. V tomto okamžiku ale rozhraní ASP.NET AJAX ještě není zcela načteno. Proto funkce `launchModal()` pouze nastaví proměnnou, kterou musí být ovládací prvek ovládacího prvku modalpopup zobrazen později v:

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

Funkce `pageLoad()` JavaScriptu je speciální funkce, která se spustí po plném načtení ASP.NET AJAX. Proto přidáme kód do této funkce pro zobrazení ovládacího prvku ovládacího prvku modalpopup, ale pouze v případě, že byla volána `launchModal()` před:

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

Funkce `$find()` hledá pojmenovaný element na stránce a jako parametr očekává ID na straně serveru. Proto `$find("mpe")` vrátí reprezentaci klienta ovládacího prvku ovládacího prvku modalpopup; jeho metoda `show()` umožňuje zobrazit automaticky otevírané okno.

[![modálnímu překryvnému okně se zobrazí při kliknutí na jedno z tlačítek.](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)

Modální automaticky otevírané okno se zobrazí, když se klikne na jedno z tlačítek ([kliknutím zobrazíte obrázek v plné velikosti).](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](using-modalpopup-with-a-repeater-control-cs.md)
