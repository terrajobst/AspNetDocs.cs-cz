---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: Přetahování přes ReorderList (VB) | Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 3f7c5749053d8bf587467fb1939fca05ce2872a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553919"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="ea09d-103">Přetažení ovládacím prvkem ReorderList (VB)</span><span class="sxs-lookup"><span data-stu-id="ea09d-103">Drag and Drop via ReorderList (VB)</span></span>

<span data-ttu-id="ea09d-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ea09d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ea09d-105">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ea09d-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="ea09d-106">Ovládací prvek ReorderList v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="ea09d-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="ea09d-107">Aktuální pořadí seznamu musí být na serveru trvalé.</span><span class="sxs-lookup"><span data-stu-id="ea09d-107">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="ea09d-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="ea09d-108">Overview</span></span>

<span data-ttu-id="ea09d-109">Ovládací prvek `ReorderList` v sadě nástrojů AJAX Control Toolkit poskytuje seznam, který lze přeuspořádat uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="ea09d-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="ea09d-110">Aktuální pořadí seznamu musí být na serveru trvalé.</span><span class="sxs-lookup"><span data-stu-id="ea09d-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="ea09d-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="ea09d-111">Steps</span></span>

<span data-ttu-id="ea09d-112">Ovládací prvek `ReorderList` podporuje vazby dat z databáze na seznam.</span><span class="sxs-lookup"><span data-stu-id="ea09d-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="ea09d-113">Nejlepší z nich také podporuje zápis změn v pořadí elementu seznamu zpátky do úložiště dat.</span><span class="sxs-lookup"><span data-stu-id="ea09d-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="ea09d-114">V této ukázce se jako úložiště dat používá edice Microsoft SQL Server 2005 Express.</span><span class="sxs-lookup"><span data-stu-id="ea09d-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="ea09d-115">Databáze je volitelná (a bezplatná) součást instalace sady Visual Studio, včetně verze Express Edition.</span><span class="sxs-lookup"><span data-stu-id="ea09d-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="ea09d-116">Je také k dispozici jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="ea09d-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="ea09d-117">V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="ea09d-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="ea09d-118">Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="ea09d-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="ea09d-119">Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="ea09d-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="ea09d-120">Připojte se k serveru, dvakrát klikněte na `Databases` a vytvořte novou databázi (klikněte pravým tlačítkem myši a vyberte `New Database`) s názvem `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="ea09d-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="ea09d-121">V této databázi vytvořte novou tabulku s názvem `AJAX` s následujícími čtyřmi sloupci:</span><span class="sxs-lookup"><span data-stu-id="ea09d-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="ea09d-122">`id` (primární klíč, celé číslo, identita, NOT NULL)</span><span class="sxs-lookup"><span data-stu-id="ea09d-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="ea09d-123">`char` (char (1); NULL)</span><span class="sxs-lookup"><span data-stu-id="ea09d-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="ea09d-124">`description` (varchar (50); NULL)</span><span class="sxs-lookup"><span data-stu-id="ea09d-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="ea09d-125">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="ea09d-125">`position` (int, NULL)</span></span>

<span data-ttu-id="ea09d-126">[![rozložení tabulky jazyka AJAX](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ea09d-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="ea09d-127">Rozložení tabulky jazyka AJAX ([kliknutím zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ea09d-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>

<span data-ttu-id="ea09d-128">V dalším kroku vyplňte tabulku několika hodnotami.</span><span class="sxs-lookup"><span data-stu-id="ea09d-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="ea09d-129">Všimněte si, že `position` sloupec obsahuje pořadí řazení prvků.</span><span class="sxs-lookup"><span data-stu-id="ea09d-129">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="ea09d-130">[![počátečních dat v tabulce AJAX](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ea09d-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="ea09d-131">Počáteční data v tabulce AJAX ([kliknutím zobrazíte obrázek v plné velikosti](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ea09d-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>

<span data-ttu-id="ea09d-132">Další krok vyžaduje vygenerování `SqlDataSource` ovládacího prvku pro komunikaci s novou databází a její tabulkou.</span><span class="sxs-lookup"><span data-stu-id="ea09d-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="ea09d-133">Zdroj dat musí podporovat příkazy SQL `SELECT` a `UPDATE`.</span><span class="sxs-lookup"><span data-stu-id="ea09d-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="ea09d-134">Když je pořadí prvků seznamu později změněno, ovládací prvek `ReorderList` automaticky odesílá dvě hodnoty do příkazu `Update` zdroje dat: novou pozici a ID prvku.</span><span class="sxs-lookup"><span data-stu-id="ea09d-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="ea09d-135">Proto zdroj dat potřebuje část `<UpdateParameters>` pro tyto dvě hodnoty:</span><span class="sxs-lookup"><span data-stu-id="ea09d-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="ea09d-136">`ReorderList` ovládací prvek musí nastavit následující atributy:</span><span class="sxs-lookup"><span data-stu-id="ea09d-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="ea09d-137">`AllowReorder`: zda lze změnit uspořádání položek seznamu</span><span class="sxs-lookup"><span data-stu-id="ea09d-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="ea09d-138">`DataSourceID`: ID zdroje dat</span><span class="sxs-lookup"><span data-stu-id="ea09d-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="ea09d-139">`DataKeyField`: název sloupce primárního klíče ve zdroji dat</span><span class="sxs-lookup"><span data-stu-id="ea09d-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="ea09d-140">`SortOrderField`: sloupec zdroj dat, který poskytuje pořadí řazení pro položky seznamu</span><span class="sxs-lookup"><span data-stu-id="ea09d-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="ea09d-141">V sekcích `<DragHandleTemplate>` a `<ItemTemplate>` lze rozložení seznamu vyladit.</span><span class="sxs-lookup"><span data-stu-id="ea09d-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="ea09d-142">Vázání dat je také možné pomocí metody `Eval()`, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="ea09d-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="ea09d-143">Následující informace stylu CSS (odkazováno v sekci `<DragHandleTemplate>` ovládacího prvku `ReorderList`) zajistí, že se ukazatel myši při umístění ukazatele myši na úchyt změní správně:</span><span class="sxs-lookup"><span data-stu-id="ea09d-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="ea09d-144">Nakonec ovládací prvek `ScriptManager` inicializuje ASP.NET AJAX pro stránku:</span><span class="sxs-lookup"><span data-stu-id="ea09d-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="ea09d-145">Spusťte tento příklad v prohlížeči a přeuspořádejte položky seznamu na bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="ea09d-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="ea09d-146">Pak znovu načtěte stránku a nebo se podívejte na databázi.</span><span class="sxs-lookup"><span data-stu-id="ea09d-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="ea09d-147">Změněné pozice byly zachovány a jsou také vyjádřeny hodnotami ve sloupci `position` v databázi a všechny bez kódu, a to pouze pomocí značek.</span><span class="sxs-lookup"><span data-stu-id="ea09d-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="ea09d-148">[![se data v databázi mění podle pořadí nové položky seznamu](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ea09d-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="ea09d-149">Data v databázi se mění podle pořadí nové položky seznamu ([kliknutím zobrazíte obrázek v plné velikosti).](drag-and-drop-via-reorderlist-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="ea09d-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ea09d-150">Předchozí</span><span class="sxs-lookup"><span data-stu-id="ea09d-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
