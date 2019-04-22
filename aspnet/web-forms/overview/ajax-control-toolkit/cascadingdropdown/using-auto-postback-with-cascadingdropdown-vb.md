---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: Použití funkce Auto-Postback ovládacím prvkem CascadingDropDown (VB) | Dokumentace Microsoftu
author: wenz
description: Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 433756839532393b36935df8f237e93706b4f18c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59383152"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a><span data-ttu-id="cbd2d-103">Použití funkce Auto-Postback v ovládacím prvku CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="cbd2d-103">Using Auto-Postback with CascadingDropDown (VB)</span></span>

<span data-ttu-id="cbd2d-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cbd2d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cbd2d-105">[Stáhněte si kód](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="cbd2d-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span></span>

> <span data-ttu-id="cbd2d-106">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="cbd2d-107">Ale při použití ovládacího prvku CascadingDropDown ASP. Prvek DropDownList NET AutoPostBack funkce nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebné) zpětné volání, samotného.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="cbd2d-108">Pomocí kódu jazyka JavaScript se můžete vyhnout tomuto chování.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-108">With some JavaScript code, this effect can be avoided.</span></span>


## <a name="overview"></a><span data-ttu-id="cbd2d-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="cbd2d-109">Overview</span></span>

<span data-ttu-id="cbd2d-110">Sada nástrojů AJAX Control Toolkit ovládacího prvku CascadingDropDown rozšiřuje ovládací prvek DropDownList tak, aby se změny v jedné DropDownList zatížení související hodnoty v jiném DropDownList.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="cbd2d-111">(Například jeden seznam obsahuje seznam nám stavy a dalším seznamu je pak vyplněna hlavních měst v tomto stavu.) Ale při použití ovládacího prvku CascadingDropDown ASP. Prvek DropDownList NET AutoPostBack funkce nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebné) zpětné volání, samotného.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="cbd2d-112">Pomocí kódu jazyka JavaScript se můžete vyhnout tomuto chování.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="cbd2d-113">Kroky</span><span class="sxs-lookup"><span data-stu-id="cbd2d-113">Steps</span></span>

<span data-ttu-id="cbd2d-114">K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci &lt; `form` &gt; element):</span><span class="sxs-lookup"><span data-stu-id="cbd2d-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="cbd2d-115">Ovládací prvek DropDownList je pak potřeba:</span><span class="sxs-lookup"><span data-stu-id="cbd2d-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="cbd2d-116">Pro tento seznam se přidá rozšíření CascadingDropDown poskytuje adresu URL a metoda informace o webových službách:</span><span class="sxs-lookup"><span data-stu-id="cbd2d-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="cbd2d-117">Zařízení extender CascadingDropDown pak asynchronně volá webové služby s využitím následující podpis metody:</span><span class="sxs-lookup"><span data-stu-id="cbd2d-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="cbd2d-118">Metoda vrátí pole typu hodnota CascadingDropDown.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="cbd2d-119">Konstruktor typu očekává, že nejprve titulek položky seznamu a pak hodnotu (HTML `value` atributu).</span><span class="sxs-lookup"><span data-stu-id="cbd2d-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="cbd2d-120">Načítání stránky v prohlížeči vyplní rozevíracího seznamu, s třemi dodavateli, druhý se předem vybrali.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="cbd2d-121">Také definuje ASP.NET `__doPostBack()` metodu JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="cbd2d-122">Po načtení stránky toto volání JavaScript se přidá do rozevíracího seznamu, pouze pokud je ale prvky v ní.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="cbd2d-123">Pokud v seznamu nejsou žádné elementy, Control Toolkit je aktuálně se načítá, tak, aby kód jazyka JavaScript používá vypršení časového limitu a pokusí se znovu za půl sekundy.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

<span data-ttu-id="cbd2d-124">Tímto způsobem, zpětné volání je pouze spuštěn, když v seznamu nejsou ve skutečnosti elementy a uživatel vybere záznam.</span><span class="sxs-lookup"><span data-stu-id="cbd2d-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>


<span data-ttu-id="cbd2d-125">[![Výběr prvku seznamu vyvolá zpětné volání](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cbd2d-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="cbd2d-126">Výběr prvku seznamu vyvolá zpětné volání ([kliknutím ji zobrazíte obrázek v plné velikosti](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cbd2d-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="cbd2d-127">Předchozí</span><span class="sxs-lookup"><span data-stu-id="cbd2d-127">Previous</span></span>](presetting-list-entries-with-cascadingdropdown-vb.md)
