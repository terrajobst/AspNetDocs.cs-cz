---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: Naplnění seznamu pomocí CascadingDropDownC#() | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614210"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a>Vyplnění seznamu ovládacím prvkem CascadingDropDown (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)

> Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.

## <a name="overview"></a>Přehled

Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.

## <a name="steps"></a>Kroky

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

Pak je vyžadován ovládací prvek DropDownList:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

Pro tento seznam se přidá CascadingDropDown Extended. Pošle asynchronní požadavek webové službě, která pak vrátí seznam položek, které se mají zobrazit v seznamu. Aby to fungovalo, musí být nastavené následující atributy CascadingDropDown:

- `ServicePath`: adresa URL webové služby, která doručuje položky seznamu.
- `ServiceMethod`: Webová metoda doručování položek seznamu
- `TargetControlID`: ID rozevíracího seznamu
- `Category`: informace o kategorii, které se odešlou do webové metody při volání
- `PromptText`: text zobrazený při asynchronním načítání dat seznamu ze serveru

Zde je značka pro prvek `CascadingDropDown`. Jediným rozdílem mezi C# a VB je název přidružené webové služby:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

Kód jazyka JavaScript přicházející z `CascadingDropDown` rozšiřuje volání metody webové služby s následující signaturou:

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

Proto je důležité, aby metoda vrátila pole typu `CascadingDropDownNameValue` (definovaném pomocí sady nástrojů ASP.NET AJAX Control Toolkit). V konstruktoru `CascadingDropDownNameValue` nejprve zadat text položky seznamu a pak její hodnotu, stejně jako `<option value="VALUE">NAME</option>` by v HTML. Tady je několik ukázkových dat:

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

Načtení stránky v prohlížeči aktivuje seznam, který bude vyplněn třemi dodavateli.

[![vyplní seznam automaticky.](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)

Seznam se vyplní automaticky ([kliknutím zobrazíte obrázek v plné velikosti).](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](using-cascadingdropdown-with-a-database-cs.md)
