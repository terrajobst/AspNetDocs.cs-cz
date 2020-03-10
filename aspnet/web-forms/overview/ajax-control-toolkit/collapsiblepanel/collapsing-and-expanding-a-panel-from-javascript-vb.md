---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: Sbalení a rozbalení panelu z JavaScriptu (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu možnost sbalení obsahu a jeho rozšíření...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535845"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>Sbalení a rozbalení panelu JavaScriptem (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu schopnost sbalit svůj obsah a znovu ho rozbalit. Tyto dvě akce lze také aktivovat z vlastního kódu JavaScriptu.

## <a name="overview"></a>Přehled

Ovládací prvek CollapsiblePanel v ASP.NET AJAX Control Toolkit rozšiřuje panel a poskytuje mu schopnost sbalit svůj obsah a znovu ho rozbalit. Tyto dvě akce lze také aktivovat z vlastního kódu JavaScriptu.

## <a name="steps"></a>Kroky

Nejprve vytvořte novou stránku ASP.NET a zahrňte `ScriptManager` do jednoho `<form>` elementu. Načte knihovnu ASP.NET AJAX, která je požadována pro sadu nástrojů Control Toolkit:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

Pak vytvořte panel s nějakým textem, aby bylo možné zobrazit efekt sbalení/rozbalení:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

Jak vidíte, panel odkazuje na třídu šablony stylů CSS, která je zde zobrazena (a v podstatě definuje barvu pozadí a šířku panelu):

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

Ovládací prvek `CollapsiblePanelExtender` vyžaduje atribut `TargetControlID`, aby sada nástrojů věděla, který panel má sbalit nebo rozbalit na vyžádání:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

V současné době bohužel rozšíření nezveřejňuje konkrétní rozhraní API pro sbalení nebo rozbalení panelu, ale některé nedokumentované metody budou dělat. Nejprve na stránku přidejte tři tlačítka HTML, která pak spustí JavaScript na straně klienta pro sbalení nebo rozbalení obsahu panelu:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

V kódu JavaScriptu na straně klienta (spuštěný s `<script type="text/javascript">`) je nutné použít metodu `$find()` pro přístup k `CollapsiblePanelExtender`. `$find("cpe")` vrátí odkaz na něj. V takovém případě vyřeší konkrétní metody úkol na ruce.

Metoda pro otevření (rozšíření) panel se nazývá `_doOpen()`; Následující kód implementuje funkci `doOpen()` volanou při kliknutí na první tlačítko:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

Pro zavření nebo sbalení panelu musí být spuštěna metoda `_doClose()`. Takže když uživatel klikne na druhé tlačítko, volá se následující JavaScriptový kód:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

Třetí tlačítko přepíná stav panelu: ze sbalené na rozbalené a naopak. `CollapsiblePanelExtender` zpřístupňuje metodu `toggle()`, která přesně používá: vrátí stav panelu. Existuje však i další přístup (který je interně používán metodou `toggle()`): `get_Collapsed()` metoda `CollapsiblePanelExtender()` oznamuje, zda je panel sbalený nebo nikoli. V závislosti na vrácené hodnotě této funkce je panel pak buď rozbalený (`_doOpen()` metoda) nebo sbalená (`_doClose()`) metoda:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

[![třetí tlačítko změní stav panelu: ze sbalené na rozbalené a zpátky](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

Třetí tlačítko změní stav panelu: ze sbaleného na rozšířené a zpět ([kliknutím zobrazíte obrázek v plné velikosti](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [Předchozí](collapsing-and-expanding-a-panel-from-javascript-cs.md)
