---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: Dynamické naplnění ovládacího prvku pomocí kódu jazyka JavaScript (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613762"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a>Dynamické naplnění ovládacího prvku javascriptovým kódem (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky. Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta.

## <a name="overview"></a>Přehled

Ovládací prvek `DynamicPopulate` v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky. Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta.

## <a name="steps"></a>Kroky

Nejprve potřebujete webovou službu ASP.NET, která implementuje metodu volanou ovládacím prvkem `DynamicPopulateExtender`. Webová služba implementuje metodu `getDate()`, která očekává jeden argument typu String, nazvaný `contextKey`, protože ovládací prvek `DynamicPopulate` odesílá jednu část informací o kontextu s každým voláním webové služby. Zde je kód (soubor `DynamicPopulate.vb.asmx`), který načte aktuální datum v jednom ze tří formátů:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

V dalším kroku vytvořte nový web ASP.NET a začněte s ovládacím prvkem ASP.NET AJAX ScriptManager:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

Pak přidejte ovládací prvek popisek (například pomocí ovládacího prvku HTML se stejným názvem nebo ovládacího prvku `<asp:Label />` Web), který bude později zobrazovat výsledek volání webové služby.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

Dále zahrňte ovládací prvek `DynamicPopulateExtender` a poskytněte informace o webové službě, cílový ovládací prvek, ale ne název ovládacího prvku, který aktivuje tuto populaci, a to pomocí vlastního JavaScriptu!

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

Nyní do části JavaScriptu. Funkce `$find()` definovaná knihovnou ASP.NET AJAX vrací odkaz na objekty na straně serveru sady nástrojů ASP.NET AJAX Control Toolkit, jako je například `DynamicPopulateExtender`. V aktuálním souboru `$find("dpe")` vrátí odkaz na jeden ovládací prvek `DynamicPopulateExtender` na stránce. Zpřístupňuje metodu nazvanou `populate()`, která aktivuje proces dynamického naplnění. Metoda `populate()` vyžaduje jeden argument: kontextový klíč, který bude sloužit jako argument webové metody `getDate()`. Například `$find("dpe").populate("format1")` by popisek naplnil aktuální datum ve formátu měsíc-den v roce.

Aby byla ukázka pružnější, uživatel teď může zvolit několik formátů data. Pro každý z nich je zobrazen přepínač. Jakmile uživatel klikne na přepínač, kód jazyka JavaScript dynamicky naplní popisek na vybraný formát data. Tady jsou tato Rádiová tlačítka:

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

Všimněte si, že v kontextu přepínače, výraz jazyka JavaScript `this.value` odkazuje na hodnotu aktuálního tlačítka, které se stane přesně stejnými informacemi, se kterou může metoda `getDate()` pracovat.

[![kliknutí na tlačítko načte datum ze serveru ve formátu zadaném](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

Kliknutím na tlačítko načtete datum ze serveru v zadaném formátu ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](dynamically-populating-a-control-vb.md)
> [Další](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
