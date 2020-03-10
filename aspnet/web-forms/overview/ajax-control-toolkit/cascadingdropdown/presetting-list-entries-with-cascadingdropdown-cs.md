---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: Přednastavení položek seznamu pomocí CascadingDropDown (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bb4a51092534e6fddbd40f868c53c58d12eef2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597900"
---
# <a name="presetting-list-entries-with-cascadingdropdown-c"></a>Předvedení položek seznamu ovládacím prvkem CascadingDropDown (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)

> Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. S malým počtem kódů je možné, že po dynamickém načtení dat je vybrán seznam element seznamu.

## <a name="overview"></a>Přehled

Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) S malým počtem kódů je možné, že po dynamickém načtení dat je vybrán seznam element seznamu.

## <a name="steps"></a>Kroky

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

Pak je vyžadován ovládací prvek DropDownList:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

Pro tento seznam se přidá CascadingDropDown Extended, který poskytuje adresu URL a informace o metodě webové služby:

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

CascadingDropDown pak asynchronně volá webovou službu s následující signaturou metody:

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

Metoda vrátí pole typu hodnota CascadingDropDown. Konstruktor typu očekává nejprve titulek položky seznamu a pak hodnotu (atribut `value` HTML). Pokud je třetí argument nastaven na hodnotu true, prvek seznamu se automaticky vybere v prohlížeči.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

Načtení stránky v prohlížeči vyplní rozevírací seznam třemi dodavateli, přičemž vybraný druhý bude předem.

[![seznam je vyplněný a automaticky vybraný.](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)

Seznam se vyplní a automaticky vybere ([kliknutím zobrazíte obrázek v plné velikosti).](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-cascadingdropdown-with-a-database-cs.md)
> [Další](using-auto-postback-with-cascadingdropdown-cs.md)
