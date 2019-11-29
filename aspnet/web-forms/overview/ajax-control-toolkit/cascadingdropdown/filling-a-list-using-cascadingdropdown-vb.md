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
# <a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="d9bf8-103">Vyplnění seznamu ovládacím prvkem CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="d9bf8-103">Filling a List Using CascadingDropDown (VB)</span></span>

<span data-ttu-id="d9bf8-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d9bf8-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d9bf8-105">[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d9bf8-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="d9bf8-106">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="d9bf8-107">(Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="d9bf8-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="d9bf8-108">Overview</span></span>

<span data-ttu-id="d9bf8-109">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="d9bf8-110">(Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="d9bf8-111">Uvedené</span><span class="sxs-lookup"><span data-stu-id="d9bf8-111">Steps</span></span>

<span data-ttu-id="d9bf8-112">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="d9bf8-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="d9bf8-113">Pak je vyžadován ovládací prvek DropDownList:</span><span class="sxs-lookup"><span data-stu-id="d9bf8-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="d9bf8-114">Pro tento seznam se přidá CascadingDropDown Extended.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="d9bf8-115">Pošle asynchronní požadavek webové službě, která pak vrátí seznam položek, které se mají zobrazit v seznamu.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="d9bf8-116">Aby to fungovalo, musí být nastavené následující atributy CascadingDropDown:</span><span class="sxs-lookup"><span data-stu-id="d9bf8-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="d9bf8-117">`ServicePath`: adresa URL webové služby, která doručuje položky seznamu.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="d9bf8-118">`ServiceMethod`: Webová metoda doručování položek seznamu</span><span class="sxs-lookup"><span data-stu-id="d9bf8-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="d9bf8-119">`TargetControlID`: ID rozevíracího seznamu</span><span class="sxs-lookup"><span data-stu-id="d9bf8-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="d9bf8-120">`Category`: informace o kategorii, které se odešlou do webové metody při volání</span><span class="sxs-lookup"><span data-stu-id="d9bf8-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="d9bf8-121">`PromptText`: text zobrazený při asynchronním načítání dat seznamu ze serveru</span><span class="sxs-lookup"><span data-stu-id="d9bf8-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="d9bf8-122">Zde je značka pro prvek `CascadingDropDown`.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="d9bf8-123">Jediným rozdílem mezi C# a VB je název přidružené webové služby:</span><span class="sxs-lookup"><span data-stu-id="d9bf8-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="d9bf8-124">Kód jazyka JavaScript přicházející z `CascadingDropDown` rozšiřuje volání metody webové služby s následující signaturou:</span><span class="sxs-lookup"><span data-stu-id="d9bf8-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="d9bf8-125">Proto je důležité, aby metoda vrátila pole typu `CascadingDropDownNameValue` (definovaném pomocí sady nástrojů ASP.NET AJAX Control Toolkit).</span><span class="sxs-lookup"><span data-stu-id="d9bf8-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="d9bf8-126">V konstruktoru `CascadingDropDownNameValue` nejprve zadat text položky seznamu a pak její hodnotu, stejně jako `<option value="VALUE">NAME</option>` by v HTML.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="d9bf8-127">Tady je několik ukázkových dat:</span><span class="sxs-lookup"><span data-stu-id="d9bf8-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="d9bf8-128">Načtení stránky v prohlížeči aktivuje seznam, který bude vyplněn třemi dodavateli.</span><span class="sxs-lookup"><span data-stu-id="d9bf8-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="d9bf8-129">[![vyplní seznam automaticky.](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d9bf8-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="d9bf8-130">Seznam se vyplní automaticky ([kliknutím zobrazíte obrázek v plné velikosti).](filling-a-list-using-cascadingdropdown-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d9bf8-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d9bf8-131">[Předchozí](using-auto-postback-with-cascadingdropdown-cs.md)
> [Další](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d9bf8-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
