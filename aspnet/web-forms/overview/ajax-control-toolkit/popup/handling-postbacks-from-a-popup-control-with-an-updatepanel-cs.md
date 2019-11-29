---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: Zpracování zpětného volání z překryvného ovládacího prvku s ovládacímC#prvkem UpdatePanel () | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Zvláštní péče je nutné vzít v potaz...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606274"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>Zpracování postbacků ovládacího prvku PopupControl ovládacím prvkem UpdatePanel (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Zvláštní péči je nutné provést, pokud dojde k postbacku v takovém překryvném okně.

## <a name="overview"></a>Přehled

PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Zvláštní péči je nutné provést, pokud dojde k postbacku v takovém překryvném okně.

## <a name="steps"></a>Uvedené

Při použití `PopupControl` s postbackem může `UpdatePanel` zabránit aktualizaci stránky způsobenou postbackem. Následující kód definuje několik důležitých prvků:

- Ovládací prvek `ScriptManager`, aby sada nástrojů ASP.NET AJAX Control
- Dva `TextBox` ovládací prvky, které spustí místní nabídku
- Ovládací prvek `Panel`, který bude sloužit jako místní nabídka
- V rámci tohoto panelu je ovládací prvek `Calendar` vložený v rámci ovládacího prvku `UpdatePanel`
- Dva `PopupControlExtender` ovládací prvky, které přiřadí panel k textovým polím

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

Všimněte si, že atribut `OnSelectionChanged` ovládacího prvku `Calendar` je nastaven. Takže když uživatel vybere datum v kalendáři, dojde k postbacku a spustí se `c1_SelectionChanged()` metoda na straně serveru. V rámci této metody musí být aktuální datum načteno a zapsáno zpět do textového pole.

Tato syntaxe je následující: první ze všech musí být vygenerován objekt proxy pro `PopupControlExtender` na stránce. ASP.NET AJAX Control Toolkit nabízí metodu `GetProxyForCurrentPopup()`. Objekt, který vrací tato metoda, podporuje metodu `Commit()`, která pošle hodnotu zpět do ovládacího prvku, který aktivoval místní nabídku (nikoli ovládací prvek, který aktivoval volání metody!). Následující kód poskytuje vybrané datum jako argument metody `Commit()`, což způsobí, že kód zapíše vybrané datum zpět do textového pole:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

Když teď kliknete na datum kalendáře, zobrazí se vybrané datum v přidruženém textovém poli a vytvoří se ovládací prvek pro výběr data, který se teď dá najít na mnoha webech.

[![kalendáři se zobrazí, když uživatel klikne do textového pole.](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png)

[![kliknutí na datum vloží do textového pole.](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

Kliknutím na datum se vloží do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](using-multiple-popup-controls-cs.md)
> [Další](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
