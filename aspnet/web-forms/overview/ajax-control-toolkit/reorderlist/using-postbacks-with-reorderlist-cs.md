---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: Použití zpětného volání s ReorderListC#() | Microsoft Docs
author: wenz
description: Ovládací prvek ReorderList v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení. Pokaždé, když je přeobjednán seznam, a...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611400"
---
# <a name="using-postbacks-with-reorderlist-c"></a>Použití postbacků s ovládacím prvkem ReorderList (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> Ovládací prvek ReorderList v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení. Pokaždé, když je seznam seřazený, zpětné volání sdělí serveru změny.

## <a name="overview"></a>Přehled

Ovládací prvek `ReorderList` v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení. Pokaždé, když je seznam seřazený, zpětné volání sdělí serveru změny.

## <a name="steps"></a>Uvedené

K dispozici je několik možných zdrojů dat pro ovládací prvek `ReorderList`. Jedním z nich je použití ovládacího prvku `XmlDataSource`:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

Aby bylo možné vytvořit vazby tohoto XML k ovládacímu prvku `ReorderList` a povolit zpětná volání, musí být nastaveny následující atributy:

- `DataSourceID`: ID zdroje dat
- `SortOrderField`: vlastnost, podle které se má řadit
- `AllowReorder`: Určuje, zda má uživatel změnit pořadí prvků seznamu.
- `PostBackOnReorder`: bez ohledu na to, jestli se má vytvořit postback při změně uspořádání seznamu

Toto je vhodný kód pro ovládací prvek:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

V rámci ovládacího prvku `ReorderList` mohou být konkrétní data ze zdroje dat vázána pomocí `Eval()` metody:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

Na libovolné pozici na stránce bude popisek obsahovat informace, když došlo k poslední změně pořadí:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

Tento popisek je vyplněn textem v kódu na straně serveru, který zpracovává postback:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

Nakonec, aby bylo možné aktivovat funkci ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn na stránce:

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

[![každé změnu pořadí spustí postback.](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

Každé přeřazení aktivuje postback ([kliknutím zobrazíte obrázek v plné velikosti).](using-postbacks-with-reorderlist-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](drag-and-drop-via-reorderlist-cs.md)
