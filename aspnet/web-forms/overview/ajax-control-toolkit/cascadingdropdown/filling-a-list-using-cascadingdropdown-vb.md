---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: Vyplnění seznamu ovládacím prvkem CascadingDropDown (VB) pomocí | Dokumentace Microsoftu
author: wenz
description: Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: ad716222335e8b6f2484953296cc263119718105
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075259"
---
<a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="1ccd7-103">Vyplnění seznamu ovládacím prvkem CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="1ccd7-103">Filling a List Using CascadingDropDown (VB)</span></span>
====================
<span data-ttu-id="1ccd7-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1ccd7-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1ccd7-105">[Stáhněte si kód](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1ccd7-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="1ccd7-106">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="1ccd7-107">(Například jeden seznam obsahuje seznam nám stavy a dalším seznamu je pak vyplněna hlavních měst v tomto stavu.) První výzva k řešení je pro skutečné vyplnění rozevíracího seznamu pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="1ccd7-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="1ccd7-108">Overview</span></span>

<span data-ttu-id="1ccd7-109">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="1ccd7-110">(Například jeden seznam obsahuje seznam nám stavy a dalším seznamu je pak vyplněna hlavních měst v tomto stavu.) První výzva k řešení je pro skutečné vyplnění rozevíracího seznamu pomocí tohoto ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="1ccd7-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="1ccd7-111">Steps</span></span>

<span data-ttu-id="1ccd7-112">K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci `<form>` element):</span><span class="sxs-lookup"><span data-stu-id="1ccd7-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="1ccd7-113">Ovládací prvek DropDownList je pak potřeba:</span><span class="sxs-lookup"><span data-stu-id="1ccd7-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="1ccd7-114">Pro tento seznam je přidán CascadingDropDown rozšíření.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="1ccd7-115">Asynchronní požadavek se odešle do webové služby, která pak vrátí seznam položek, které lze zobrazit v seznamu.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="1ccd7-116">Aby to fungovalo nutné nastavit následující atributy CascadingDropDown:</span><span class="sxs-lookup"><span data-stu-id="1ccd7-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="1ccd7-117">`ServicePath`: Adresa URL webové služby doručování položky seznamu</span><span class="sxs-lookup"><span data-stu-id="1ccd7-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="1ccd7-118">`ServiceMethod`: Metodu webové zajištění položky seznamu</span><span class="sxs-lookup"><span data-stu-id="1ccd7-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="1ccd7-119">`TargetControlID`: ID seznamu, rozevíracího seznamu</span><span class="sxs-lookup"><span data-stu-id="1ccd7-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="1ccd7-120">`Category`: Informace o kategoriích, které je odeslána do webové metody při volání</span><span class="sxs-lookup"><span data-stu-id="1ccd7-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="1ccd7-121">`PromptText`: Text zobrazovaný v případě asynchronní načítání seznamu data ze serveru</span><span class="sxs-lookup"><span data-stu-id="1ccd7-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="1ccd7-122">Tady je zápis `CascadingDropDown` elementu.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="1ccd7-123">Jediným rozdílem mezi C# a VB je název přidružené webové služby:</span><span class="sxs-lookup"><span data-stu-id="1ccd7-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="1ccd7-124">Z kódu jazyka JavaScript `CascadingDropDown` volání rozšiřující metody webové služby s následující signaturou:</span><span class="sxs-lookup"><span data-stu-id="1ccd7-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="1ccd7-125">Proto je důležitým aspektem je, že metoda musí vracet pole typu `CascadingDropDownNameValue` (definované technologie ASP.NET AJAX Control Toolkit).</span><span class="sxs-lookup"><span data-stu-id="1ccd7-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="1ccd7-126">V `CascadingDropDownNameValue` konstruktoru, první text položky seznamu a pak její hodnotu musí být zadaná, stejně jako `<option value="VALUE">NAME</option>` byste udělali ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-126">In the `CascadingDropDownNameValue` contructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="1ccd7-127">Tady je ukázková data:</span><span class="sxs-lookup"><span data-stu-id="1ccd7-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="1ccd7-128">Načítání stránky v prohlížeči se aktivuje seznamu tankujeme tři dodavatelů.</span><span class="sxs-lookup"><span data-stu-id="1ccd7-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="1ccd7-129">[![V seznamu se vyplní automaticky](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1ccd7-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="1ccd7-130">V seznamu se vyplní automaticky ([kliknutím ji zobrazíte obrázek v plné velikosti](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1ccd7-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ccd7-131">[Předchozí](using-auto-postback-with-cascadingdropdown-cs.md)
> [další](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1ccd7-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
