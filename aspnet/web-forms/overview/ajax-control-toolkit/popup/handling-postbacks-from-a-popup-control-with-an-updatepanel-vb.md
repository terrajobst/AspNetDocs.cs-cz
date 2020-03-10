---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: Zpracování zpětného volání z překryvného ovládacího prvku s ovládacím prvkem UpdatePanel (VB) | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Zvláštní péče je nutné vzít v potaz...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: dd045ae56696c7944df98cf805ba812fde1bb4ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612894"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a>Zpracování postbacků ovládacího prvku PopupControl ovládacím prvkem UpdatePanel (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)

> PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Zvláštní péči je nutné provést, pokud dojde k postbacku v takovém překryvném okně.

## <a name="overview"></a>Přehled

PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Zvláštní péči je nutné provést, pokud dojde k postbacku v takovém překryvném okně.

## <a name="steps"></a>Kroky

Při použití `PopupControl` s postbackem může `UpdatePanel` zabránit aktualizaci stránky způsobenou postbackem. Následující kód definuje několik důležitých prvků:

- Ovládací prvek `ScriptManager`, aby sada nástrojů ASP.NET AJAX Control
- Dva `TextBox` ovládací prvky, které spustí místní nabídku
- Ovládací prvek `Panel`, který bude sloužit jako místní nabídka
- V rámci tohoto panelu je ovládací prvek `Calendar` vložený v rámci ovládacího prvku `UpdatePanel`
- Dva `PopupControlExtender` ovládací prvky, které přiřadí panel k textovým polím

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

Všimněte si, že atribut `OnSelectionChanged` ovládacího prvku `Calendar` je nastaven. Takže když uživatel vybere datum v kalendáři, dojde k postbacku a spustí se `c1_SelectionChanged()` metoda na straně serveru. V rámci této metody musí být aktuální datum načteno a zapsáno zpět do textového pole.

Tato syntaxe je následující: první ze všech musí být vygenerován objekt proxy pro `PopupControlExtender` na stránce. ASP.NET AJAX Control Toolkit nabízí metodu `GetProxyForCurrentPopup()`. Objekt, který vrací tato metoda, podporuje metodu `Commit()`, která pošle hodnotu zpět do ovládacího prvku, který aktivoval místní nabídku (nikoli ovládací prvek, který aktivoval volání metody!). Následující kód poskytuje vybrané datum jako argument metody `Commit()`, což způsobí, že kód zapíše vybrané datum zpět do textového pole:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

Když teď kliknete na datum kalendáře, zobrazí se vybrané datum v přidruženém textovém poli a vytvoří se ovládací prvek pro výběr data, který se teď dá najít na mnoha webech.

[![kalendáři se zobrazí, když uživatel klikne do textového pole.](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)

Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png)

[![kliknutí na datum vloží do textového pole.](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)

Kliknutím na datum se vloží do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](using-multiple-popup-controls-vb.md)
> [Další](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)
