---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: Použití automatického zpětného odeslání s CascadingDropDown (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535922"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a>Použití funkce Auto-Postback v ovládacím prvku CascadingDropDown (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)

> Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. Nicméně při použití ovládacího prvku CascadingDropDown, ASP. Funkce automatického odeslání ovládacího prvku pro ovládací prvek DropDownList nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebný) postback sám. S nějakým kódem JavaScriptu, je možné se tomuto efektu vyhnout.

## <a name="overview"></a>Přehled

Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) Nicméně při použití ovládacího prvku CascadingDropDown, ASP. Funkce automatického odeslání ovládacího prvku pro ovládací prvek DropDownList nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebný) postback sám. S nějakým kódem JavaScriptu, je možné se tomuto efektu vyhnout.

## <a name="steps"></a>Kroky

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v &lt;`form`elementu &gt;):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

Pak je vyžadován ovládací prvek DropDownList:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

Pro tento seznam se přidá CascadingDropDown Extended, který poskytuje adresu URL a informace o metodě webové služby:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

CascadingDropDown pak asynchronně volá webovou službu s následující signaturou metody:

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

Metoda vrátí pole typu hodnota CascadingDropDown. Konstruktor typu očekává nejprve titulek položky seznamu a pak hodnotu (atribut `value` HTML).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

Načtení stránky v prohlížeči vyplní rozevírací seznam třemi dodavateli, přičemž vybraný druhý bude předem. ASP.NET definuje také metodu `__doPostBack()` JavaScriptu. Po načtení stránky je toto volání JavaScriptu přidáno do rozevíracího seznamu, ale pouze v případě, že jsou v něm prvky. Pokud v seznamu nejsou žádné prvky, ovládací sada nástrojů je aktuálně načítá, takže kód jazyka JavaScript používá časový limit a opakuje pokus za půl sekundy.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

Tímto způsobem se spustí postback pouze v případě, že se v seznamu skutečně nacházejí nějaké prvky a uživatel vybere položku.

[![výběru prvku seznamu způsobí postback.](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)

Výběr prvku seznamu způsobí postback ([kliknutím zobrazíte obrázek v plné velikosti).](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](presetting-list-entries-with-cascadingdropdown-vb.md)
