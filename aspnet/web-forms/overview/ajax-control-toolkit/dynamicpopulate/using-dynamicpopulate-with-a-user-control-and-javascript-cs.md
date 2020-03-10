---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
title: Použití ovládacího prvku DynamicPopulate s uživatelským ovládacím prvkem a JavaScriptem (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 38ac8250-8854-444c-b9ab-8998faa41c5a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: a0e6d04a5f62ab558aceb8302d94d3bf2dc8a39f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613706"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-c"></a>Použití ovládacího prvku DynamicPopulate s uživatelským ovládacím prvkem a JavaScriptem (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)

> Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky. Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta. Zvláštní péči je však nutné vzít v případě, že se v uživatelském ovládacím prvku nachází zařízení.

## <a name="overview"></a>Přehled

Ovládací prvek `DynamicPopulate` v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky. Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta. Zvláštní péči je však nutné vzít v případě, že se v uživatelském ovládacím prvku nachází zařízení.

## <a name="steps"></a>Kroky

Nejprve potřebujete webovou službu ASP.NET, která implementuje metodu volanou ovládacím prvkem `DynamicPopulateExtender`. Webová služba implementuje metodu `getDate()`, která očekává jeden argument typu String, nazvaný `contextKey`, protože ovládací prvek `DynamicPopulate` odesílá jednu část informací o kontextu s každým voláním webové služby. Zde je kód (soubor `DynamicPopulate.cs.asmx`), který načte aktuální datum v jednom ze tří formátů:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample1.aspx)]

V dalším kroku vytvořte nový uživatelský ovládací prvek (`.ascx` soubor) označený následující deklarací v prvním řádku:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample2.aspx)]

&lt;`label`&gt; prvek bude použit k zobrazení dat přicházejících ze serveru.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample3.aspx)]

V souboru uživatelského ovládacího prvku budeme používat tři přepínače, přičemž každý z nich představuje jeden ze tří možných formátů data, které webová služba podporuje. Když uživatel klikne na jeden z přepínačů, prohlížeč spustí kód JavaScriptu, který vypadá takto:

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample4.ps1)]

Tento kód přistupuje k `DynamicPopulateExtender` (nedělejte si starosti s neobvyklým ID, bude popsaný později) a aktivuje dynamické naplnění dat. V kontextu aktuálního přepínače `this.value` odkazuje na jeho hodnotu, která je `format1`, `format2` nebo `format3` přesně to, co Webová metoda očekává.

V uživatelském ovládacím prvku již chybí jediná věc `DynamicPopulateExtender` ovládací prvek, který propojuje přepínače s webovou službou.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample5.aspx)]

Znovu si můžete všimnout nezvyklého ID použitého v ovládacím prvku: `mcd1$myDate` místo `myDate`. Dříve se kód jazyka JavaScript použil `mcd1_dpe1` pro přístup k `DynamicPopulateExtender` namísto `dpe1`. Tato strategie pojmenovávání je zvláštní požadavek při použití `DynamicPopulateExtender` v rámci uživatelského ovládacího prvku. Kromě toho je nutné vložit uživatelský ovládací prvek tak, aby všechno fungoval. Vytvořte novou stránku ASP.NET a zaregistrujte předponu značky pro uživatelský ovládací prvek, který jste právě implementovali:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample6.aspx)]

Potom do nové stránky přidejte ovládací prvek ASP.NET AJAX `ScriptManager`:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample7.aspx)]

Nakonec přidejte uživatelský ovládací prvek na stránku. Je nutné nastavit jeho atribut `ID` (a `runat="server"`, samozřejmě), ale musíte ho také nastavit na konkrétní název: `mcd1`, protože se jedná o předponu použitou v uživatelském ovládacím prvku pro přístup pomocí JavaScriptu.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample8.aspx)]

A to je vše! Stránka se chová podle očekávání: uživatel klikne na jeden z přepínačů, ovládací prvek v sadě nástrojů volá webovou službu a zobrazí aktuální datum v požadovaném formátu.

[![, že se přepínače nacházejí v uživatelském ovládacím prvku](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)

Přepínače se nacházejí v uživatelském ovládacím prvku ([kliknutím zobrazíte obrázek v plné velikosti).](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](dynamically-populating-a-control-using-javascript-code-cs.md)
> [Další](dynamically-populating-a-control-vb.md)
