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
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="c260d-104">Přetažení ovládacím prvkem ReorderList (C#)</span><span class="sxs-lookup"><span data-stu-id="c260d-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="c260d-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c260d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c260d-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c260d-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="c260d-107">Ovládací prvek ReorderList v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="c260d-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="c260d-108">Aktuální pořadí seznamu musí být na serveru trvalé.</span><span class="sxs-lookup"><span data-stu-id="c260d-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="c260d-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="c260d-109">Overview</span></span>

<span data-ttu-id="c260d-110">Ovládací prvek `ReorderList` v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="c260d-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="c260d-111">Aktuální pořadí seznamu musí být na serveru trvalé.</span><span class="sxs-lookup"><span data-stu-id="c260d-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="c260d-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="c260d-112">Steps</span></span>

<span data-ttu-id="c260d-113">Ovládací prvek `ReorderList` podporuje vazby dat z databáze na seznam.</span><span class="sxs-lookup"><span data-stu-id="c260d-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="c260d-114">Nejlepší z nich také podporuje zápis změn v pořadí elementu seznamu zpátky do úložiště dat.</span><span class="sxs-lookup"><span data-stu-id="c260d-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="c260d-115">V této ukázce se jako úložiště dat používá edice Microsoft SQL Server 2005 Express.</span><span class="sxs-lookup"><span data-stu-id="c260d-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="c260d-116">Databáze je volitelná (a bezplatná) součást instalace sady Visual Studio, včetně verze Express Edition.</span><span class="sxs-lookup"><span data-stu-id="c260d-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="c260d-117">Je také k dispozici jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="c260d-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="c260d-118">V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="c260d-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="c260d-119">Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="c260d-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="c260d-120">Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="c260d-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="c260d-121">Připojte se k serveru, dvakrát klikněte na `Databases` a vytvořte novou databázi (klikněte pravým tlačítkem myši a vyberte `New Database`) s názvem `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="c260d-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="c260d-122">V této databázi vytvořte novou tabulku s názvem `AJAX` s následujícími čtyřmi sloupci:</span><span class="sxs-lookup"><span data-stu-id="c260d-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="c260d-123">`id` (primární klíč, celé číslo, identita, NOT NULL)</span><span class="sxs-lookup"><span data-stu-id="c260d-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="c260d-124">`char` (char (1); NULL)</span><span class="sxs-lookup"><span data-stu-id="c260d-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="c260d-125">`description` (varchar (50); NULL)</span><span class="sxs-lookup"><span data-stu-id="c260d-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="c260d-126">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="c260d-126">`position` (int, NULL)</span></span>

<span data-ttu-id="c260d-127">[![rozložení tabulky jazyka AJAX](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c260d-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="c260d-128">Rozložení tabulky jazyka AJAX ([kliknutím zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c260d-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="c260d-129">V dalším kroku vyplňte tabulku několika hodnotami.</span><span class="sxs-lookup"><span data-stu-id="c260d-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="c260d-130">Všimněte si, že `position` sloupec obsahuje pořadí řazení prvků.</span><span class="sxs-lookup"><span data-stu-id="c260d-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="c260d-131">[![počátečních dat v tabulce AJAX](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c260d-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="c260d-132">Počáteční data v tabulce AJAX ([kliknutím zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c260d-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="c260d-133">Další krok vyžaduje vygenerování `SqlDataSource` ovládacího prvku pro komunikaci s novou databází a její tabulkou.</span><span class="sxs-lookup"><span data-stu-id="c260d-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="c260d-134">Zdroj dat musí podporovat příkazy SQL `SELECT` a `UPDATE`.</span><span class="sxs-lookup"><span data-stu-id="c260d-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="c260d-135">Když je pořadí prvků seznamu později změněno, ovládací prvek `ReorderList` automaticky odesílá dvě hodnoty do příkazu `Update` zdroje dat: novou pozici a ID prvku.</span><span class="sxs-lookup"><span data-stu-id="c260d-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="c260d-136">Proto zdroj dat potřebuje část `<UpdateParameters>` pro tyto dvě hodnoty:</span><span class="sxs-lookup"><span data-stu-id="c260d-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="c260d-137">`ReorderList` ovládací prvek musí nastavit následující atributy:</span><span class="sxs-lookup"><span data-stu-id="c260d-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="c260d-138">`AllowReorder`: zda lze změnit uspořádání položek seznamu</span><span class="sxs-lookup"><span data-stu-id="c260d-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="c260d-139">`DataSourceID`: ID zdroje dat</span><span class="sxs-lookup"><span data-stu-id="c260d-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="c260d-140">`DataKeyField`: název sloupce primárního klíče ve zdroji dat</span><span class="sxs-lookup"><span data-stu-id="c260d-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="c260d-141">`SortOrderField`: sloupec zdroj dat, který poskytuje pořadí řazení pro položky seznamu</span><span class="sxs-lookup"><span data-stu-id="c260d-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="c260d-142">V sekcích `<DragHandleTemplate>` a `<ItemTemplate>` lze rozložení seznamu vyladit.</span><span class="sxs-lookup"><span data-stu-id="c260d-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="c260d-143">Vázání dat je také možné pomocí metody `Eval()`, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="c260d-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="c260d-144">Následující informace stylu CSS (odkazováno v sekci `<DragHandleTemplate>` ovládacího prvku `ReorderList`) zajistí, že se ukazatel myši při umístění ukazatele myši na úchyt změní správně:</span><span class="sxs-lookup"><span data-stu-id="c260d-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="c260d-145">Nakonec ovládací prvek `ScriptManager` inicializuje ASP.NET AJAX pro stránku:</span><span class="sxs-lookup"><span data-stu-id="c260d-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="c260d-146">Spusťte tento příklad v prohlížeči a přeuspořádejte položky seznamu na bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="c260d-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="c260d-147">Pak znovu načtěte stránku a nebo se podívejte na databázi.</span><span class="sxs-lookup"><span data-stu-id="c260d-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="c260d-148">Změněné pozice byly zachovány a jsou také vyjádřeny hodnotami ve sloupci `position` v databázi a všechny bez kódu, a to pouze pomocí značek.</span><span class="sxs-lookup"><span data-stu-id="c260d-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="c260d-149">[![se data v databázi mění podle pořadí nové položky seznamu](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c260d-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="c260d-150">Data v databázi se mění podle pořadí nové položky seznamu ([kliknutím zobrazíte obrázek v plné velikosti).](drag-and-drop-via-reorderlist-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="c260d-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c260d-151">[Předchozí](using-postbacks-with-reorderlist-cs.md)
> [Další](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c260d-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
