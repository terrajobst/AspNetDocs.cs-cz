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
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="f0a07-103">Vyplnění seznamu ovládacím prvkem CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="f0a07-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="f0a07-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f0a07-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f0a07-105">[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f0a07-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="f0a07-106">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="f0a07-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f0a07-107">(Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="f0a07-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="f0a07-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="f0a07-108">Overview</span></span>

<span data-ttu-id="f0a07-109">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="f0a07-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f0a07-110">(Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) První výzvou, kterou je třeba vyřešit, je ve skutečnosti vyplnit rozevírací seznam pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="f0a07-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="f0a07-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="f0a07-111">Steps</span></span>

<span data-ttu-id="f0a07-112">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="f0a07-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="f0a07-113">Pak je vyžadován ovládací prvek DropDownList:</span><span class="sxs-lookup"><span data-stu-id="f0a07-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="f0a07-114">Pro tento seznam se přidá CascadingDropDown Extended.</span><span class="sxs-lookup"><span data-stu-id="f0a07-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="f0a07-115">Pošle asynchronní požadavek webové službě, která pak vrátí seznam položek, které se mají zobrazit v seznamu.</span><span class="sxs-lookup"><span data-stu-id="f0a07-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="f0a07-116">Aby to fungovalo, musí být nastavené následující atributy CascadingDropDown:</span><span class="sxs-lookup"><span data-stu-id="f0a07-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="f0a07-117">`ServicePath`: adresa URL webové služby, která doručuje položky seznamu.</span><span class="sxs-lookup"><span data-stu-id="f0a07-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="f0a07-118">`ServiceMethod`: Webová metoda doručování položek seznamu</span><span class="sxs-lookup"><span data-stu-id="f0a07-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="f0a07-119">`TargetControlID`: ID rozevíracího seznamu</span><span class="sxs-lookup"><span data-stu-id="f0a07-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="f0a07-120">`Category`: informace o kategorii, které se odešlou do webové metody při volání</span><span class="sxs-lookup"><span data-stu-id="f0a07-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="f0a07-121">`PromptText`: text zobrazený při asynchronním načítání dat seznamu ze serveru</span><span class="sxs-lookup"><span data-stu-id="f0a07-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="f0a07-122">Zde je značka pro prvek `CascadingDropDown`.</span><span class="sxs-lookup"><span data-stu-id="f0a07-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="f0a07-123">Jediným rozdílem mezi C# a VB je název přidružené webové služby:</span><span class="sxs-lookup"><span data-stu-id="f0a07-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="f0a07-124">Kód jazyka JavaScript přicházející z `CascadingDropDown` rozšiřuje volání metody webové služby s následující signaturou:</span><span class="sxs-lookup"><span data-stu-id="f0a07-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="f0a07-125">Proto je důležité, aby metoda vrátila pole typu `CascadingDropDownNameValue` (definovaném pomocí sady nástrojů ASP.NET AJAX Control Toolkit).</span><span class="sxs-lookup"><span data-stu-id="f0a07-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="f0a07-126">V konstruktoru `CascadingDropDownNameValue` nejprve zadat text položky seznamu a pak její hodnotu, stejně jako `<option value="VALUE">NAME</option>` by v HTML.</span><span class="sxs-lookup"><span data-stu-id="f0a07-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="f0a07-127">Tady je několik ukázkových dat:</span><span class="sxs-lookup"><span data-stu-id="f0a07-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="f0a07-128">Načtení stránky v prohlížeči aktivuje seznam, který bude vyplněn třemi dodavateli.</span><span class="sxs-lookup"><span data-stu-id="f0a07-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="f0a07-129">[![vyplní seznam automaticky.](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f0a07-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="f0a07-130">Seznam se vyplní automaticky ([kliknutím zobrazíte obrázek v plné velikosti).](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f0a07-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f0a07-131">Next</span><span class="sxs-lookup"><span data-stu-id="f0a07-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
