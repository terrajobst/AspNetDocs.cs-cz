---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: Použití postbacků s ovládacím prvkem ReorderList (VB) | Dokumentace Microsoftu
author: wenz
description: Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení. Pokaždé, když je pořadí v seznamu změníte, po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 22c7eecb841ff67196d21e6efeeda63a3456c5cb
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409080"
---
# <a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="a208e-104">Použití postbacků s ovládacím prvkem ReorderList (VB)</span><span class="sxs-lookup"><span data-stu-id="a208e-104">Using Postbacks with ReorderList (VB)</span></span>

<span data-ttu-id="a208e-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a208e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a208e-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a208e-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="a208e-107">Ovládacím prvkem ReorderList ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="a208e-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="a208e-108">Pokaždé, když je pořadí v seznamu změníte, zpětné volání informuje server změny.</span><span class="sxs-lookup"><span data-stu-id="a208e-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="a208e-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="a208e-109">Overview</span></span>

<span data-ttu-id="a208e-110">`ReorderList` Ovládacího prvku AJAX Control Toolkit poskytuje seznam, který může být přeuspořádány uživatelem pomocí přetažení.</span><span class="sxs-lookup"><span data-stu-id="a208e-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="a208e-111">Pokaždé, když je pořadí v seznamu změníte, zpětné volání informuje server změny.</span><span class="sxs-lookup"><span data-stu-id="a208e-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="a208e-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="a208e-112">Steps</span></span>

<span data-ttu-id="a208e-113">Existuje několik datových zdrojů pro `ReorderList` ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a208e-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="a208e-114">Jeden má používat `XmlDataSource` ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="a208e-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="a208e-115">Vázat tento XML tak, aby `ReorderList` postbacků ovládacího prvku a povolit, následující atributy musí být nastavena:</span><span class="sxs-lookup"><span data-stu-id="a208e-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- `DataSourceID`<span data-ttu-id="a208e-116">: ID zdroje dat</span><span class="sxs-lookup"><span data-stu-id="a208e-116">: The ID of the data source</span></span>
- `SortOrderField`<span data-ttu-id="a208e-117">: Vlastnost, která má řadit podle</span><span class="sxs-lookup"><span data-stu-id="a208e-117">: The property to sort by</span></span>
- `AllowReorder`<span data-ttu-id="a208e-118">: Jestli se má povolit uživatelům změnit uspořádání seznamu elementů</span><span class="sxs-lookup"><span data-stu-id="a208e-118">: Whether to allow the user to reorder the list elements</span></span>
- `PostBackOnReorder`<span data-ttu-id="a208e-119">: Jestli chcete vytvořit zpětné volání pokaždé, když je změnit jejich uspořádání seznamu</span><span class="sxs-lookup"><span data-stu-id="a208e-119">: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="a208e-120">Tady je odpovídající značky ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="a208e-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="a208e-121">V rámci `ReorderList` ovládacího prvku, konkrétní data ze zdroje dat, může být vázaný pomocí `Eval()` metody:</span><span class="sxs-lookup"><span data-stu-id="a208e-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="a208e-122">Na libovolné pozici na stránce popisek bude obsahovat informace, kdy poslední změny pořadí došlo k chybě:</span><span class="sxs-lookup"><span data-stu-id="a208e-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="a208e-123">Tento popisek je vyplněna text v kódu na straně serveru, zpracování zpětného volání:</span><span class="sxs-lookup"><span data-stu-id="a208e-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="a208e-124">Nakonec, aby bylo možné aktivovat funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit na stránce:</span><span class="sxs-lookup"><span data-stu-id="a208e-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


[![E<span data-ttu-id="a208e-125">Změna uspořádání ACH aktivuje zpětné volání]</span><span class="sxs-lookup"><span data-stu-id="a208e-125">ach reordering triggers a postback]</span></span>(using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

<span data-ttu-id="a208e-126">Každá změna uspořádání aktivuje zpětné volání ([kliknutím ji zobrazíte obrázek v plné velikosti](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a208e-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a208e-127">[Předchozí](drag-and-drop-via-reorderlist-cs.md)
> [další](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a208e-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
