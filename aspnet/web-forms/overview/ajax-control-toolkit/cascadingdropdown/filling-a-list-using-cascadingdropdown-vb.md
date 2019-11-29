---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: Naplnění seznamu pomocí CascadingDropDown (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 8dd9ef8a4bdf705ba4451b7fd240e4de8618221c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599566"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a>Vyplnění seznamu ovládacím prvkem CascadingDropDown (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.

## <a name="overview"></a>Přehled

Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.

## <a name="steps"></a>Uvedené

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

Pak je vyžadován ovládací prvek DropDownList:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

Pro tento seznam se přidá CascadingDropDown Extended. Pošle asynchronní požadavek webové službě, která pak vrátí seznam položek, které se mají zobrazit v seznamu. Aby to fungovalo, musí být nastavené následující atributy CascadingDropDown:

- `ServicePath`: adresa URL webové služby, která doručuje položky seznamu.
- `ServiceMethod`: Webová metoda doručování položek seznamu
- `TargetControlID`: ID rozevíracího seznamu
- `Category`: informace o kategorii, které se odešlou do webové metody při volání
- `PromptText`: text zobrazený při asynchronním načítání dat seznamu ze serveru

Zde je značka pro prvek `CascadingDropDown`. Jediným rozdílem mezi C# a VB je název přidružené webové služby:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

Kód jazyka JavaScript přicházející z `CascadingDropDown` rozšiřuje volání metody webové služby s následující signaturou:

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

Proto je důležité, aby metoda vrátila pole typu `CascadingDropDownNameValue` (definovaném pomocí sady nástrojů ASP.NET AJAX Control Toolkit). V konstruktoru `CascadingDropDownNameValue` nejprve zadat text položky seznamu a pak její hodnotu, stejně jako `<option value="VALUE">NAME</option>` by v HTML. Tady je několik ukázkových dat:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

Načtení stránky v prohlížeči aktivuje seznam, který bude vyplněn třemi dodavateli.

[![vyplní seznam automaticky.](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

Seznam se vyplní automaticky ([kliknutím zobrazíte obrázek v plné velikosti).](filling-a-list-using-cascadingdropdown-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-auto-postback-with-cascadingdropdown-cs.md)
> [Další](using-cascadingdropdown-with-a-database-vb.md)
