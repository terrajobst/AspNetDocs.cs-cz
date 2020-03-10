---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: Vazba na přiznávání (VB) | Microsoft Docs
author: wenz
description: Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bfb31940c0395c7ed1d5d471fb8fb686b66c59ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614518"
---
# <a name="databinding-to-an-accordion-vb"></a><span data-ttu-id="d2d5b-104">Datová vazba ovládacího prvku Accordion (VB)</span><span class="sxs-lookup"><span data-stu-id="d2d5b-104">Databinding to an Accordion (VB)</span></span>

<span data-ttu-id="d2d5b-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d2d5b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d2d5b-106">[Stažení kódu](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d2d5b-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span></span>

> <span data-ttu-id="d2d5b-107">Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="d2d5b-108">Panely jsou obvykle deklarovány v rámci samotné stránky, ale vazba na zdroj dat nabízí větší flexibilitu.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="d2d5b-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="d2d5b-109">Overview</span></span>

<span data-ttu-id="d2d5b-110">Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="d2d5b-111">Panely jsou obvykle deklarovány v rámci samotné stránky, ale vazba na zdroj dat nabízí větší flexibilitu.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="d2d5b-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="d2d5b-112">Steps</span></span>

<span data-ttu-id="d2d5b-113">Nejdříve je vyžadován zdroj dat.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-113">First of all, a data source is required.</span></span> <span data-ttu-id="d2d5b-114">V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="d2d5b-115">Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="d2d5b-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="d2d5b-116">Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="d2d5b-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="d2d5b-117">Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="d2d5b-118">V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="d2d5b-119">Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="d2d5b-120">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="d2d5b-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

<span data-ttu-id="d2d5b-121">Pak přidejte zdroj dat na stránku.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-121">Then, add a data source to the page.</span></span> <span data-ttu-id="d2d5b-122">Aby bylo možné použít omezené množství dat, vyberte pouze prvních pět záznamů v tabulce dodavatelů databáze AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="d2d5b-123">Pokud k vytvoření zdroje dat používáte pomocníka sady Visual Studio, pamatujte, že chyba v aktuální verzi neprefixuje název tabulky (`Vendor`) s `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="d2d5b-124">Následující kód ukazuje správnou syntaxi:</span><span class="sxs-lookup"><span data-stu-id="d2d5b-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

<span data-ttu-id="d2d5b-125">Zapamatujte si název (ID) zdroje dat.</span><span class="sxs-lookup"><span data-stu-id="d2d5b-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="d2d5b-126">Tato velmi identifikace musí být použita ve vlastnosti `DataSourceID` ovládacího prvku pro přiznávání:</span><span class="sxs-lookup"><span data-stu-id="d2d5b-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

<span data-ttu-id="d2d5b-127">V rámci řízení přiznávání můžete poskytnout šablony pro různé části ovládacího prvku, včetně hlavičky (`<HeaderTemplate>`) a obsahu (`<ContentTemplate>`).</span><span class="sxs-lookup"><span data-stu-id="d2d5b-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="d2d5b-128">V rámci těchto elementů stačí výstup dat ze zdroje dat pomocí metody `DataBinder.Eval()`:</span><span class="sxs-lookup"><span data-stu-id="d2d5b-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

<span data-ttu-id="d2d5b-129">Po načtení stránky musí být zdroj dat vázán na toto souhlasu s tímto kódem na straně serveru:</span><span class="sxs-lookup"><span data-stu-id="d2d5b-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

<span data-ttu-id="d2d5b-130">Chcete-li uzavřít tuto ukázku, je nutné definovat dvě třídy šablony stylů CSS, na které se odkazuje v řízení přiznávání (ve vlastnostech `HeaderCssClass` a `ContentCssClass`).</span><span class="sxs-lookup"><span data-stu-id="d2d5b-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="d2d5b-131">Do části `<head>` stránky vložte následující kód:</span><span class="sxs-lookup"><span data-stu-id="d2d5b-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]

<span data-ttu-id="d2d5b-132">[![se data v přiznávání nacházejí přímo ze zdroje dat.](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d2d5b-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span></span>

<span data-ttu-id="d2d5b-133">Data v přiznávání přicházejí přímo ze zdroje dat ([kliknutím zobrazíte obrázek v plné velikosti).](databinding-to-an-accordion-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d2d5b-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2d5b-134">[Předchozí](dynamically-adding-an-accordion-pane-cs.md)
> [Další](dynamically-adding-an-accordion-pane-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d2d5b-134">[Previous](dynamically-adding-an-accordion-pane-cs.md)
[Next](dynamically-adding-an-accordion-pane-vb.md)</span></span>
