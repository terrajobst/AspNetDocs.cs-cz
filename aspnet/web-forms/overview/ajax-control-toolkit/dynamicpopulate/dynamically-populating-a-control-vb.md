---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: Dynamické naplnění ovládacího prvku (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599403"
---
# <a name="dynamically-populating-a-control-vb"></a>Dynamické naplnění ovládacího prvku (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)

> Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky.

## <a name="overview"></a>Přehled

Ovládací prvek `DynamicPopulate` v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky. V tomto kurzu se dozvíte, jak tuto sadu nastavit.

## <a name="steps"></a>Uvedené

Nejprve potřebujete webovou službu ASP.NET, která implementuje metodu volanou `DynamicPopulate`. Třída webové služby vyžaduje atribut `ScriptService`, který je definován v rámci `Microsoft.Web.Script.Services`; v opačném případě ASP.NET AJAX nemůže vytvořit proxy server JavaScriptu na straně klienta pro webovou službu, která je zase požadována `DynamicPopulate`.

Metoda web musí očekávat jeden argument typu String s názvem `contextKey`, protože ovládací prvek `DynamicPopulate` odesílá jednu část informací o kontextu pro každé volání webové služby. Následující webová služba vrátí aktuální datum ve formátu reprezentovaném argumentem `contextKey`:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

Webová služba se pak uloží jako `DynamicPopulate.vb.asmx`. Alternativně můžete implementovat metodu `getDate()` jako metodu stránky na stránce vlastní ASP.NET s ovládacím prvkem `DynamicPopulate`.

V dalším kroku vytvořte nový soubor ASP.NET. Jako vždy je prvním krokem vložení `ScriptManager` do aktuální stránky, aby se načetla knihovna AJAX ASP.NET a aby sada nástrojů Control Toolkit fungovala takto:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

Pak přidejte ovládací prvek popisek (například pomocí ovládacího prvku HTML se stejným názvem nebo &lt;`asp:Label` /&gt; webového ovládacího prvku), který bude později zobrazovat výsledek volání webové služby.

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

Tlačítko HTML (jako ovládací prvek HTML, protože nepotřebujeme postback na server), se pak použije k aktivaci dynamického naplnění:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

Nakonec potřebujeme `DynamicPopulateExtender` řízení k vytváření kabelů. Budou nastaveny následující atributy (Kromě zjevných `ID` a `runat`=`"server"`):

- `TargetControlID`, kam se má vložit výsledek z volání webové služby
- `ServicePath` cesta k webové službě (vynechejte, pokud chcete použít metodu stránky)
- `ServiceMethod` název metody web nebo metody stránky
- `ContextKey` informace o kontextu, které se mají odeslat webové službě
- `PopulateTriggerControlID` element, který aktivuje volání webové služby
- `ClearContentsDuringUpdate`, jestli se má při volání webové služby vyprázdnit cílový element

Jak vidíte, ovládací prvek vyžaduje některé informace, ale vše na místo je poměrně přímé. Zde je značka ovládacího prvku `DynamicPopulateExtender` v aktuálním scénáři:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

Spusťte stránku ASP.NET v prohlížeči a klikněte na tlačítko. zobrazí se aktuální datum ve formátu měsíc-den v roce.

[![kliknutí na tlačítko načte datum ze serveru.](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)

Kliknutím na tlačítko se načte datum ze serveru ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-populating-a-control-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [Další](dynamically-populating-a-control-using-javascript-code-vb.md)
