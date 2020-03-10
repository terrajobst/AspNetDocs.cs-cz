---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: Vytvoření ovládacího prvku hodnocení (VB) | Microsoft Docs
author: wenz
description: Mnoho webů, od elektronického obchodování po komunitní weby, nabízí svým uživatelům hodnocení článků nebo položek. To obvykle vyžaduje určité úsilí při psaní kódu, ale máme...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 08e245edfe73db4e3896db51151e5d7a0fa9697c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612194"
---
# <a name="creating-a-rating-control-vb"></a><span data-ttu-id="af941-104">Vytvoření ovládacího prvku Rating (VB)</span><span class="sxs-lookup"><span data-stu-id="af941-104">Creating a Rating Control (VB)</span></span>

<span data-ttu-id="af941-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="af941-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="af941-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="af941-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)</span></span>

> <span data-ttu-id="af941-107">Mnoho webů, od elektronického obchodování po komunitní weby, nabízí svým uživatelům hodnocení článků nebo položek.</span><span class="sxs-lookup"><span data-stu-id="af941-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="af941-108">To obvykle vyžaduje určité úsilí při psaní kódu, ale máme k dispozici sadu nástrojů Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="af941-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="af941-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="af941-109">Overview</span></span>

<span data-ttu-id="af941-110">Mnoho webů, od elektronického obchodování po komunitní weby, nabízí svým uživatelům hodnocení článků nebo položek.</span><span class="sxs-lookup"><span data-stu-id="af941-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="af941-111">To obvykle vyžaduje určité úsilí při psaní kódu, ale máme k dispozici sadu nástrojů Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="af941-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="af941-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="af941-112">Steps</span></span>

<span data-ttu-id="af941-113">Nejdřív potřebujete (aspoň) dva druhy imagí: jednu pro vyplněnou položku hodnocení a jednu pro prázdnou položku hodnocení.</span><span class="sxs-lookup"><span data-stu-id="af941-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="af941-114">Položka hodnocení je obvykle hvězdička nebo smajlík.</span><span class="sxs-lookup"><span data-stu-id="af941-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="af941-115">V tomto scénáři najdete tři soubory, smajlík. png a prázdné. png a Smiley-Done. png jako součást souborů ke stažení zdrojového kódu pro účely tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="af941-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="af941-116">Pak vytvořte nový soubor ASP.NET a začněte přidáním ovládacího prvku `ScriptManager`:</span><span class="sxs-lookup"><span data-stu-id="af941-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

<span data-ttu-id="af941-117">Pak přidejte ovládací prvek `Rating` z ovládací sady nástrojů AJAX pro ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="af941-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="af941-118">Pro tento příklad je nutné nastavit následující atributy:</span><span class="sxs-lookup"><span data-stu-id="af941-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="af941-119">`CurrentRating` počáteční hodnocení, které se má použít</span><span class="sxs-lookup"><span data-stu-id="af941-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="af941-120">`MaxRating` maximální hodnocení.</span><span class="sxs-lookup"><span data-stu-id="af941-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="af941-121">`EmptyStarCssClass` třídy šablony stylů CSS, která se má použít, pokud je položka hodnocení (hvězda) prázdná</span><span class="sxs-lookup"><span data-stu-id="af941-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="af941-122">`FilledStarCssClass` třídy šablony stylů CSS, která se má použít, když se vyplní položka hodnocení (hvězda)</span><span class="sxs-lookup"><span data-stu-id="af941-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="af941-123">`StarCssClass` třídy CSS, která se má použít pro viditelné staty</span><span class="sxs-lookup"><span data-stu-id="af941-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="af941-124">`WaitingStarCssClass` třídy šablony stylů CSS, která se má použít, když se na server pošle hodnocení hvězdičkami zpátky</span><span class="sxs-lookup"><span data-stu-id="af941-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="af941-125">A zde je značka, která vytvoří ovládací prvek hodnocení s pěti položkami (Smileys), z nichž není původně vyplněna žádná hodnota:</span><span class="sxs-lookup"><span data-stu-id="af941-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

<span data-ttu-id="af941-126">Tři odkazované třídy CSS teď potřebují zobrazit vhodné soubory obrázků, které je snadné použít CSS:</span><span class="sxs-lookup"><span data-stu-id="af941-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

<span data-ttu-id="af941-127">Ujistěte se, že zadáváte šířku a výšku tří imagí. v opačném případě se může zobrazit bitová kopie.</span><span class="sxs-lookup"><span data-stu-id="af941-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="af941-128">Nakonec by se měl výsledek hodnocení zobrazit uživateli (nebo alespoň v databázi).</span><span class="sxs-lookup"><span data-stu-id="af941-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="af941-129">Přidejte tedy popisek pro výstup textové zprávy a tlačítko Odeslat pro odeslání zpět formuláře hodnocení na server:</span><span class="sxs-lookup"><span data-stu-id="af941-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

<span data-ttu-id="af941-130">V kódu na straně serveru přihlaste k ovládacímu prvku hodnocení prostřednictvím jeho `ID` a potom přejděte k jeho vlastnosti `CurrentRating`, která představuje počet vybraných položek hodnocení. v našem příkladu je to hodnota mezi 0 a 5.</span><span class="sxs-lookup"><span data-stu-id="af941-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

<span data-ttu-id="af941-131">Uložte stránku a načtěte ji do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="af941-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="af941-132">Když najedete myší na položky hodnocení (počáteční prázdné), dojde k efektu JavaScriptu: hodnocení se změní.</span><span class="sxs-lookup"><span data-stu-id="af941-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="af941-133">Když kliknete na sadu hvězdiček, aktuální hodnocení se zachová.</span><span class="sxs-lookup"><span data-stu-id="af941-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="af941-134">Nakonec při odeslání formuláře výstup kódu na straně serveru vypíše vybrané hodnocení.</span><span class="sxs-lookup"><span data-stu-id="af941-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="af941-135">[![vytvoření systému hodnocení s minimálním kódem](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="af941-135">[![Creating a rating system with minimal code](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="af941-136">Vytvoření systému hodnocení s minimálním kódem ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-rating-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="af941-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="af941-137">Předchozí</span><span class="sxs-lookup"><span data-stu-id="af941-137">Previous</span></span>](creating-a-rating-control-cs.md)
