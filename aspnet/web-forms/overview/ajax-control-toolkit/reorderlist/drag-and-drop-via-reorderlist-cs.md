---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: Přetahování přes ReorderList (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek ReorderList v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení. Aktuální pořadí seznamu bude...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fc6d55a290cbb58bea36d8145d814e337bbd931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553828"
---
# <a name="drag-and-drop-via-reorderlist-c"></a>Přetažení ovládacím prvkem ReorderList (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> Ovládací prvek ReorderList v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení. Aktuální pořadí seznamu musí být na serveru trvalé.

## <a name="overview"></a>Přehled

Ovládací prvek `ReorderList` v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení. Aktuální pořadí seznamu musí být na serveru trvalé.

## <a name="steps"></a>Kroky

Ovládací prvek `ReorderList` podporuje vazby dat z databáze na seznam. Nejlepší z nich také podporuje zápis změn v pořadí elementu seznamu zpátky do úložiště dat.

V této ukázce se jako úložiště dat používá edice Microsoft SQL Server 2005 Express. Databáze je volitelná (a bezplatná) součást instalace sady Visual Studio, včetně verze Express Edition. Je také k dispozici jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení. Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.

Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ). Připojte se k serveru, dvakrát klikněte na `Databases` a vytvořte novou databázi (klikněte pravým tlačítkem myši a vyberte `New Database`) s názvem `Tutorials`.

V této databázi vytvořte novou tabulku s názvem `AJAX` s následujícími čtyřmi sloupci:

- `id` (primární klíč, celé číslo, identita, NOT NULL)
- `char` (char (1); NULL)
- `description` (varchar (50); NULL)
- `position` (int, NULL)

[![rozložení tabulky jazyka AJAX](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

Rozložení tabulky jazyka AJAX ([kliknutím zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image3.png))

V dalším kroku vyplňte tabulku několika hodnotami. Všimněte si, že `position` sloupec obsahuje pořadí řazení prvků.

[![počátečních dat v tabulce AJAX](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

Počáteční data v tabulce AJAX ([kliknutím zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image6.png))

Další krok vyžaduje vygenerování `SqlDataSource` ovládacího prvku pro komunikaci s novou databází a její tabulkou. Zdroj dat musí podporovat příkazy SQL `SELECT` a `UPDATE`. Když je pořadí prvků seznamu později změněno, ovládací prvek `ReorderList` automaticky odesílá dvě hodnoty do příkazu `Update` zdroje dat: novou pozici a ID prvku. Proto zdroj dat potřebuje část `<UpdateParameters>` pro tyto dvě hodnoty:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` ovládací prvek musí nastavit následující atributy:

- `AllowReorder`: zda lze změnit uspořádání položek seznamu
- `DataSourceID`: ID zdroje dat
- `DataKeyField`: název sloupce primárního klíče ve zdroji dat
- `SortOrderField`: sloupec zdroj dat, který poskytuje pořadí řazení pro položky seznamu

V sekcích `<DragHandleTemplate>` a `<ItemTemplate>` lze rozložení seznamu vyladit. Vázání dat je také možné pomocí metody `Eval()`, jak je vidět tady:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

Následující informace stylu CSS (odkazováno v sekci `<DragHandleTemplate>` ovládacího prvku `ReorderList`) zajistí, že se ukazatel myši při umístění ukazatele myši na úchyt změní správně:

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

Nakonec ovládací prvek `ScriptManager` inicializuje ASP.NET AJAX pro stránku:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

Spusťte tento příklad v prohlížeči a přeuspořádejte položky seznamu na bitovou kopii. Pak znovu načtěte stránku a nebo se podívejte na databázi. Změněné pozice byly zachovány a jsou také vyjádřeny hodnotami ve sloupci `position` v databázi a všechny bez kódu, a to pouze pomocí značek.

[![se data v databázi mění podle pořadí nové položky seznamu](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

Data v databázi se mění podle pořadí nové položky seznamu ([kliknutím zobrazíte obrázek v plné velikosti).](drag-and-drop-via-reorderlist-cs/_static/image9.png)

> [!div class="step-by-step"]
> [Předchozí](using-postbacks-with-reorderlist-cs.md)
> [Další](using-postbacks-with-reorderlist-vb.md)
