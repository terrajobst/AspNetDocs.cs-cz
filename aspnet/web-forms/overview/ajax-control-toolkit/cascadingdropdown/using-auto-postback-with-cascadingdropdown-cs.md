---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: Použití automatického zpětného odeslání s CascadingDropDownC#() | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574507"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a>Použití funkce Auto-Postback v ovládacím prvku CascadingDropDown (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)

> Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. Nicméně při použití ovládacího prvku CascadingDropDown, ASP. Funkce automatického odeslání ovládacího prvku pro ovládací prvek DropDownList nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebný) postback sám. S nějakým kódem JavaScriptu, je možné se tomuto efektu vyhnout.

## <a name="overview"></a>Přehled

Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) Nicméně při použití ovládacího prvku CascadingDropDown, ASP. Funkce automatického odeslání ovládacího prvku pro ovládací prvek DropDownList nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebný) postback sám. S nějakým kódem JavaScriptu, je možné se tomuto efektu vyhnout.

## <a name="steps"></a>Uvedené

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v &lt;`form`elementu &gt;):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

Pak je vyžadován ovládací prvek DropDownList:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

Pro tento seznam se přidá CascadingDropDown Extended, který poskytuje adresu URL a informace o metodě webové služby:

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

CascadingDropDown pak asynchronně volá webovou službu s následující signaturou metody:

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

Metoda vrátí pole typu hodnota CascadingDropDown. Konstruktor typu očekává nejprve titulek položky seznamu a pak hodnotu (atribut `value` HTML).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

Načtení stránky v prohlížeči vyplní rozevírací seznam třemi dodavateli, přičemž vybraný druhý bude předem. ASP.NET definuje také metodu `__doPostBack()` JavaScriptu. Po načtení stránky je toto volání JavaScriptu přidáno do rozevíracího seznamu, ale pouze v případě, že jsou v něm prvky. Pokud v seznamu nejsou žádné prvky, ovládací sada nástrojů je aktuálně načítá, takže kód jazyka JavaScript používá časový limit a opakuje pokus za půl sekundy.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

Tímto způsobem se spustí postback pouze v případě, že se v seznamu skutečně nacházejí nějaké prvky a uživatel vybere položku.

[![výběru prvku seznamu způsobí postback.](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)

Výběr prvku seznamu způsobí postback ([kliknutím zobrazíte obrázek v plné velikosti).](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](presetting-list-entries-with-cascadingdropdown-cs.md)
> [Další](filling-a-list-using-cascadingdropdown-vb.md)
