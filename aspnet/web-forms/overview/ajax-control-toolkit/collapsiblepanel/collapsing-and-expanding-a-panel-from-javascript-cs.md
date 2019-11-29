---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: Sbalení a rozbalení panelu z JavaScriptu (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu možnost sbalení obsahu a jeho rozšíření...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: bed14d82394d28336493bec10e31ddb4d411a192
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599431"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a>Sbalení a rozbalení panelu JavaScriptem (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)

> Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu schopnost sbalit svůj obsah a znovu ho rozbalit. Tyto dvě akce lze také aktivovat z vlastního kódu JavaScriptu.

## <a name="overview"></a>Přehled

Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu schopnost sbalit svůj obsah a znovu ho rozbalit. Tyto dvě akce lze také aktivovat z vlastního kódu JavaScriptu.

## <a name="steps"></a>Uvedené

Nejprve vytvořte novou stránku ASP.NET a zahrňte `ScriptManager` do jednoho `<form>` elementu. Načte knihovnu ASP.NET AJAX, která je požadována pro sadu nástrojů Control Toolkit:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

Pak vytvořte panel s nějakým textem, aby bylo možné zobrazit efekt sbalení/rozbalení:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

Jak vidíte, panel odkazuje na třídu šablony stylů CSS, která je zde zobrazena (a v podstatě definuje barvu pozadí a šířku panelu):

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

Ovládací prvek `CollapsiblePanelExtender` vyžaduje atribut `TargetControlID`, aby sada nástrojů věděla, který panel má sbalit nebo rozbalit na vyžádání:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

V současné době bohužel rozšíření nezveřejňuje konkrétní rozhraní API pro sbalení nebo rozbalení panelu, ale některé nedokumentované metody budou dělat. Nejprve na stránku přidejte tři tlačítka HTML, která pak spustí JavaScript na straně klienta pro sbalení nebo rozbalení obsahu panelu:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

V kódu JavaScriptu na straně klienta (spuštěný s `<script type="text/javascript">`) je nutné použít metodu `$find()` pro přístup k `CollapsiblePanelExtender`. `$find("cpe")` vrátí odkaz na něj. V takovém případě vyřeší konkrétní metody úkol na ruce.

Metoda pro otevření (rozšíření) panel se nazývá `_doOpen()`; Následující kód implementuje funkci `doOpen()` volanou při kliknutí na první tlačítko:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

Pro zavření nebo sbalení panelu musí být spuštěna metoda `_doClose()`. Takže když uživatel klikne na druhé tlačítko, volá se následující JavaScriptový kód:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

Třetí tlačítko přepíná stav panelu: ze sbalené na rozbalené a naopak. `CollapsiblePanelExtender` zpřístupňuje metodu `toggle()`, která přesně používá: vrátí stav panelu. Existuje však i další přístup (který je interně používán metodou `toggle()`): `get_Collapsed()` metoda `CollapsiblePanelExtender()` oznamuje, zda je panel sbalený nebo nikoli. V závislosti na vrácené hodnotě této funkce je panel pak buď rozbalený (`_doOpen()` metoda) nebo sbalená (`_doClose()`) metoda:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]

[![třetí tlačítko změní stav panelu: ze sbalené na rozbalené a zpátky](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)

Třetí tlačítko změní stav panelu: ze sbaleného na rozšířené a zpět ([kliknutím zobrazíte obrázek v plné velikosti](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [Next](collapsing-and-expanding-a-panel-from-javascript-vb.md)
