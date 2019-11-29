---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: Přednastavení položek seznamu pomocí CascadingDropDown (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599554"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a><span data-ttu-id="d1d3f-103">Předvedení položek seznamu ovládacím prvkem CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="d1d3f-103">Presetting List Entries with CascadingDropDown (VB)</span></span>

<span data-ttu-id="d1d3f-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d1d3f-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d1d3f-105">[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d1d3f-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span></span>

> <span data-ttu-id="d1d3f-106">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="d1d3f-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="d1d3f-107">S malým počtem kódů je možné, že po dynamickém načtení dat je vybrán seznam element seznamu.</span><span class="sxs-lookup"><span data-stu-id="d1d3f-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="d1d3f-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="d1d3f-108">Overview</span></span>

<span data-ttu-id="d1d3f-109">Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList.</span><span class="sxs-lookup"><span data-stu-id="d1d3f-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="d1d3f-110">(Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) S malým počtem kódů je možné, že po dynamickém načtení dat je vybrán seznam element seznamu.</span><span class="sxs-lookup"><span data-stu-id="d1d3f-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="d1d3f-111">Uvedené</span><span class="sxs-lookup"><span data-stu-id="d1d3f-111">Steps</span></span>

<span data-ttu-id="d1d3f-112">Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):</span><span class="sxs-lookup"><span data-stu-id="d1d3f-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="d1d3f-113">Pak je vyžadován ovládací prvek DropDownList:</span><span class="sxs-lookup"><span data-stu-id="d1d3f-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="d1d3f-114">Pro tento seznam se přidá CascadingDropDown Extended, který poskytuje adresu URL a informace o metodě webové služby:</span><span class="sxs-lookup"><span data-stu-id="d1d3f-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="d1d3f-115">CascadingDropDown pak asynchronně volá webovou službu s následující signaturou metody:</span><span class="sxs-lookup"><span data-stu-id="d1d3f-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="d1d3f-116">Metoda vrátí pole typu hodnota CascadingDropDown.</span><span class="sxs-lookup"><span data-stu-id="d1d3f-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="d1d3f-117">Konstruktor typu očekává nejprve titulek položky seznamu a pak hodnotu (atribut `value` HTML).</span><span class="sxs-lookup"><span data-stu-id="d1d3f-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="d1d3f-118">Pokud je třetí argument nastaven na hodnotu true, prvek seznamu se automaticky vybere v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="d1d3f-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="d1d3f-119">Načtení stránky v prohlížeči vyplní rozevírací seznam třemi dodavateli, přičemž vybraný druhý bude předem.</span><span class="sxs-lookup"><span data-stu-id="d1d3f-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="d1d3f-120">[![seznam je vyplněný a automaticky vybraný.](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d1d3f-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="d1d3f-121">Seznam se vyplní a automaticky vybere ([kliknutím zobrazíte obrázek v plné velikosti).](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d1d3f-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d1d3f-122">[Předchozí](using-cascadingdropdown-with-a-database-vb.md)
> [Další](using-auto-postback-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d1d3f-122">[Previous](using-cascadingdropdown-with-a-database-vb.md)
[Next](using-auto-postback-with-cascadingdropdown-vb.md)</span></span>
