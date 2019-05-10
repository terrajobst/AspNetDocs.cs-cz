---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: Vyplnění seznamu ovládacím prvkem použití ovládacího prvku CascadingDropDown (C#) | Dokumentace Microsoftu
author: wenz
description: Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 31319e0ad15825acead2b7e8b619985272fb8eaa
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131460"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="ae25f-103">Vyplnění seznamu ovládacím prvkem CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="ae25f-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="ae25f-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ae25f-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ae25f-105">[Stáhněte si kód](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ae25f-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="ae25f-106">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="ae25f-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="ae25f-107">(Například jeden seznam obsahuje seznam nám stavy a dalším seznamu je pak vyplněna hlavních měst v tomto stavu.) První výzva k řešení je pro skutečné vyplnění rozevíracího seznamu pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="ae25f-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="ae25f-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="ae25f-108">Overview</span></span>

<span data-ttu-id="ae25f-109">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="ae25f-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="ae25f-110">(Například jeden seznam obsahuje seznam nám stavy a dalším seznamu je pak vyplněna hlavních měst v tomto stavu.) První výzva k řešení je pro skutečné vyplnění rozevíracího seznamu pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="ae25f-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="ae25f-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="ae25f-111">Steps</span></span>

<span data-ttu-id="ae25f-112">K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci `<form>` element):</span><span class="sxs-lookup"><span data-stu-id="ae25f-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="ae25f-113">Ovládací prvek DropDownList je pak potřeba:</span><span class="sxs-lookup"><span data-stu-id="ae25f-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="ae25f-114">Pro tento seznam je přidán CascadingDropDown rozšíření.</span><span class="sxs-lookup"><span data-stu-id="ae25f-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="ae25f-115">Asynchronní požadavek se odešle do webové služby, která pak vrátí seznam položek, které lze zobrazit v seznamu.</span><span class="sxs-lookup"><span data-stu-id="ae25f-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="ae25f-116">Aby to fungovalo nutné nastavit následující atributy CascadingDropDown:</span><span class="sxs-lookup"><span data-stu-id="ae25f-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="ae25f-117">`ServicePath`: Adresa URL webové služby doručování položky seznamu</span><span class="sxs-lookup"><span data-stu-id="ae25f-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="ae25f-118">`ServiceMethod`: Metodu webové zajištění položky seznamu</span><span class="sxs-lookup"><span data-stu-id="ae25f-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="ae25f-119">`TargetControlID`: ID seznamu, rozevíracího seznamu</span><span class="sxs-lookup"><span data-stu-id="ae25f-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="ae25f-120">`Category`: Informace o kategoriích, které je odeslána do webové metody při volání</span><span class="sxs-lookup"><span data-stu-id="ae25f-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="ae25f-121">`PromptText`: Text zobrazovaný v případě asynchronní načítání seznamu data ze serveru</span><span class="sxs-lookup"><span data-stu-id="ae25f-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="ae25f-122">Tady je zápis `CascadingDropDown` elementu.</span><span class="sxs-lookup"><span data-stu-id="ae25f-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="ae25f-123">Jediným rozdílem mezi C# a VB je název přidružené webové služby:</span><span class="sxs-lookup"><span data-stu-id="ae25f-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="ae25f-124">Z kódu jazyka JavaScript `CascadingDropDown` volání rozšiřující metody webové služby s následující signaturou:</span><span class="sxs-lookup"><span data-stu-id="ae25f-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="ae25f-125">Proto je důležitým aspektem je, že metoda musí vracet pole typu `CascadingDropDownNameValue` (definované technologie ASP.NET AJAX Control Toolkit).</span><span class="sxs-lookup"><span data-stu-id="ae25f-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="ae25f-126">V `CascadingDropDownNameValue` konstruktoru, první text položky seznamu a pak její hodnotu musí být zadaná, stejně jako `<option value="VALUE">NAME</option>` byste udělali ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="ae25f-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="ae25f-127">Tady je ukázková data:</span><span class="sxs-lookup"><span data-stu-id="ae25f-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="ae25f-128">Načítání stránky v prohlížeči se aktivuje seznamu tankujeme tři dodavatelů.</span><span class="sxs-lookup"><span data-stu-id="ae25f-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="ae25f-129">[![V seznamu se vyplní automaticky](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ae25f-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="ae25f-130">V seznamu se vyplní automaticky ([kliknutím ji zobrazíte obrázek v plné velikosti](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ae25f-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ae25f-131">Next</span><span class="sxs-lookup"><span data-stu-id="ae25f-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
