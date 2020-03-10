---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Použití nabídky hovermenu s ovládacím prvkem Repeater (C#) | Microsoft Docs
author: wenz
description: 'Ovládací prvek nabídky hovermenu v sadě nástrojů AJAX Control Toolkit poskytuje jednoduchý překryvný efekt: když ukazatel myši najede na prvek, zobrazí se automaticky otevírané okno...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578125"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="05357-103">Použití nabídky HoverMenu s ovládacím prvkem Repeater (C#)</span><span class="sxs-lookup"><span data-stu-id="05357-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="05357-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="05357-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="05357-105">[Stažení kódu](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="05357-105">[Download Code](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="05357-106">Ovládací prvek nabídky hovermenu v sadě nástrojů AJAX Control Toolkit poskytuje jednoduchý překryvný efekt: když ukazatel myši najede myší na prvek, zobrazí se místní nabídka na zadané pozici.</span><span class="sxs-lookup"><span data-stu-id="05357-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="05357-107">Tento ovládací prvek lze také použít v rámci Repeater.</span><span class="sxs-lookup"><span data-stu-id="05357-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="05357-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="05357-108">Overview</span></span>

<span data-ttu-id="05357-109">Ovládací prvek `HoverMenu` v sadě nástrojů AJAX Control Toolkit poskytuje jednoduchý překryvný efekt: když ukazatel myši najede myší na prvek, zobrazí se místní nabídka na zadané pozici.</span><span class="sxs-lookup"><span data-stu-id="05357-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="05357-110">Tento ovládací prvek lze také použít v rámci Repeater.</span><span class="sxs-lookup"><span data-stu-id="05357-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="05357-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="05357-111">Steps</span></span>

<span data-ttu-id="05357-112">Nejdříve je vyžadován zdroj dat.</span><span class="sxs-lookup"><span data-stu-id="05357-112">First of all, a data source is required.</span></span> <span data-ttu-id="05357-113">V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express.</span><span class="sxs-lookup"><span data-stu-id="05357-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="05357-114">Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="05357-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="05357-115">Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="05357-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="05357-116">Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.</span><span class="sxs-lookup"><span data-stu-id="05357-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="05357-117">V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="05357-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="05357-118">Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="05357-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="05357-119">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="05357-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="05357-120">Pak přidejte zdroj dat na stránku.</span><span class="sxs-lookup"><span data-stu-id="05357-120">Then, add a data source to the page.</span></span> <span data-ttu-id="05357-121">Aby bylo možné použít omezené množství dat, vyberte pouze prvních pět záznamů v tabulce dodavatelů databáze AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="05357-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="05357-122">Pokud k vytvoření zdroje dat používáte pomocníka sady Visual Studio, pamatujte, že chyba v aktuální verzi neprefixuje název tabulky (`Vendor`) s `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="05357-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="05357-123">Následující kód ukazuje správnou syntaxi:</span><span class="sxs-lookup"><span data-stu-id="05357-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="05357-124">Dále přidejte panel, který slouží jako modální automaticky otevíraná okna:</span><span class="sxs-lookup"><span data-stu-id="05357-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="05357-125">Nyní `HoverMenuExtender` přichází do hry.</span><span class="sxs-lookup"><span data-stu-id="05357-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="05357-126">Aby každý prvek ve zdroji dat získá svou vlastní místní nabídku, musí být tento ovládací prvek vložen do oddílu `<ItemTemplate>` Repeater.</span><span class="sxs-lookup"><span data-stu-id="05357-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="05357-127">Zde je značka:</span><span class="sxs-lookup"><span data-stu-id="05357-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="05357-128">Po zpoždění 50 milisekund (`PopDelay` atribut) teď každá položka ve zdroji dat zobrazuje automaticky otevírané okno vpravo (`PopupPosition` atribut).</span><span class="sxs-lookup"><span data-stu-id="05357-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="05357-129">[![se vedle každé položky v poli Repeater zobrazí nabídka s efektem přechodu](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="05357-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="05357-130">Vedle každé položky v poli Repeater se zobrazí nabídka přechodu ([kliknutím zobrazíte obrázek v plné velikosti).](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="05357-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="05357-131">Next</span><span class="sxs-lookup"><span data-stu-id="05357-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
