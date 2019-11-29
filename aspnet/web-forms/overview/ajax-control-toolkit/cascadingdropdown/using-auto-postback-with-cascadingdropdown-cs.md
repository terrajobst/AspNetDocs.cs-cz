---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: Použití automatického zpětného odeslání s CascadingDropDownC#() | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574507"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="ddcd6-103">Použití funkce Auto-Postback v ovládacím prvku CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="ddcd6-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>

<span data-ttu-id="ddcd6-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ddcd6-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ddcd6-105">[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ddcd6-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="ddcd6-106">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="ddcd6-107">Nicméně při použití ovládacího prvku CascadingDropDown, ASP. Funkce automatického odeslání ovládacího prvku pro ovládací prvek DropDownList nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebný) postback sám.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="ddcd6-108">S nějakým kódem JavaScriptu, je možné se tomuto efektu vyhnout.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="ddcd6-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="ddcd6-109">Overview</span></span>

<span data-ttu-id="ddcd6-110">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="ddcd6-111">(Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) Nicméně při použití ovládacího prvku CascadingDropDown, ASP. Funkce automatického odeslání ovládacího prvku pro ovládací prvek DropDownList nefunguje, protože asynchronní načítání dat do seznamu generuje (nepotřebný) postback sám.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="ddcd6-112">S nějakým kódem JavaScriptu, je možné se tomuto efektu vyhnout.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="ddcd6-113">Uvedené</span><span class="sxs-lookup"><span data-stu-id="ddcd6-113">Steps</span></span>

<span data-ttu-id="ddcd6-114">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v &lt;`form`elementu &gt;):</span><span class="sxs-lookup"><span data-stu-id="ddcd6-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="ddcd6-115">Pak je vyžadován ovládací prvek DropDownList:</span><span class="sxs-lookup"><span data-stu-id="ddcd6-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="ddcd6-116">Pro tento seznam se přidá CascadingDropDown Extended, který poskytuje adresu URL a informace o metodě webové služby:</span><span class="sxs-lookup"><span data-stu-id="ddcd6-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="ddcd6-117">CascadingDropDown pak asynchronně volá webovou službu s následující signaturou metody:</span><span class="sxs-lookup"><span data-stu-id="ddcd6-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="ddcd6-118">Metoda vrátí pole typu hodnota CascadingDropDown.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="ddcd6-119">Konstruktor typu očekává nejprve titulek položky seznamu a pak hodnotu (atribut `value` HTML).</span><span class="sxs-lookup"><span data-stu-id="ddcd6-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="ddcd6-120">Načtení stránky v prohlížeči vyplní rozevírací seznam třemi dodavateli, přičemž vybraný druhý bude předem.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="ddcd6-121">ASP.NET definuje také metodu `__doPostBack()` JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="ddcd6-122">Po načtení stránky je toto volání JavaScriptu přidáno do rozevíracího seznamu, ale pouze v případě, že jsou v něm prvky.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="ddcd6-123">Pokud v seznamu nejsou žádné prvky, ovládací sada nástrojů je aktuálně načítá, takže kód jazyka JavaScript používá časový limit a opakuje pokus za půl sekundy.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="ddcd6-124">Tímto způsobem se spustí postback pouze v případě, že se v seznamu skutečně nacházejí nějaké prvky a uživatel vybere položku.</span><span class="sxs-lookup"><span data-stu-id="ddcd6-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="ddcd6-125">[![výběru prvku seznamu způsobí postback.](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ddcd6-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="ddcd6-126">Výběr prvku seznamu způsobí postback ([kliknutím zobrazíte obrázek v plné velikosti).](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ddcd6-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ddcd6-127">[Předchozí](presetting-list-entries-with-cascadingdropdown-cs.md)
> [Další](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ddcd6-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>
