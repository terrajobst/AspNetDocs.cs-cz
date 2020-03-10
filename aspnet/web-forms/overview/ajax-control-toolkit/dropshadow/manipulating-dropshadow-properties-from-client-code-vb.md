---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Manipulace s DropShadow vlastnostmi z klientského kódu (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Vlastnosti tohoto zařízení lze také změnit pomocí JavaScrip klienta...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613797"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a>Změna vlastností ovládacího prvku DropShadow klientským kódem (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)

> Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Vlastnosti tohoto zařízení lze také změnit pomocí kódu JavaScriptu klienta.

## <a name="overview"></a>Přehled

Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Vlastnosti tohoto zařízení lze také změnit pomocí kódu JavaScriptu klienta.

## <a name="steps"></a>Kroky

Kód začíná panelem obsahujícím některé řádky textu:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

Přidružená Třída CSS dává panelu na skvělé barvy pozadí:

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

Přidá se `DropShadowExtender`, aby se panel rozšířil na efekt vrženého stínu, což je neprůhlednost nastavené na 50%:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

Pak ovládací prvek ASP.NET AJAX `ScriptManager` umožňuje, aby sada nástrojů pracovala:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

Další panel obsahuje dva odkazy JavaScriptu pro nastavení neprůhlednosti vrženého stínu: odkaz minus snižuje průhlednost stínu, a proto se ho zvyšuje propojení.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

Funkce jazyka JavaScript `changeOpacity()` musí nejprve najít ovládací prvek `DropShadowExtender` na stránce. ASP.NET AJAX definuje metodu `$find()` pro přesně danou úlohu. Pak metoda `get_Opacity()` načte aktuální neprůhlednost, metoda `set_Opacity()` ji nastaví. Kód jazyka JavaScript pak vloží aktuální hodnotu neprůhlednosti v prvku `<label>`:

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

[![změna neprůhlednosti na straně klienta](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

Neprůhlednost se mění na straně klienta ([kliknutím zobrazíte obrázek v plné velikosti).](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](adjusting-the-z-index-of-a-dropshadow-vb.md)
