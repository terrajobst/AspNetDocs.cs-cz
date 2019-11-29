---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: Manipulace s DropShadow vlastnostmi z klientského kódu (C#) | Microsoft Docs
author: wenz
description: Přizpůsobení rozhraní pro úpravy prvku DataList
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574101"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="9a606-103">Změna vlastností ovládacího prvku DropShadow klientským kódem (C#)</span><span class="sxs-lookup"><span data-stu-id="9a606-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>

<span data-ttu-id="9a606-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9a606-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9a606-105">[Stažení kódu](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="9a606-105">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="9a606-106">Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín.</span><span class="sxs-lookup"><span data-stu-id="9a606-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="9a606-107">Vlastnosti tohoto zařízení lze také změnit pomocí kódu JavaScriptu klienta.</span><span class="sxs-lookup"><span data-stu-id="9a606-107">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="9a606-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="9a606-108">Overview</span></span>

<span data-ttu-id="9a606-109">Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín.</span><span class="sxs-lookup"><span data-stu-id="9a606-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="9a606-110">Vlastnosti tohoto zařízení lze také změnit pomocí kódu JavaScriptu klienta.</span><span class="sxs-lookup"><span data-stu-id="9a606-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="9a606-111">Uvedené</span><span class="sxs-lookup"><span data-stu-id="9a606-111">Steps</span></span>

<span data-ttu-id="9a606-112">Kód začíná panelem obsahujícím některé řádky textu:</span><span class="sxs-lookup"><span data-stu-id="9a606-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="9a606-113">Přidružená Třída CSS dává panelu na skvělé barvy pozadí:</span><span class="sxs-lookup"><span data-stu-id="9a606-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="9a606-114">Přidá se `DropShadowExtender`, aby se panel rozšířil na efekt vrženého stínu, což je neprůhlednost nastavené na 50%:</span><span class="sxs-lookup"><span data-stu-id="9a606-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="9a606-115">Pak ovládací prvek ASP.NET AJAX `ScriptManager` umožňuje, aby sada nástrojů pracovala:</span><span class="sxs-lookup"><span data-stu-id="9a606-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="9a606-116">Další panel obsahuje dva odkazy JavaScriptu pro nastavení neprůhlednosti vrženého stínu: odkaz minus snižuje průhlednost stínu, a proto se ho zvyšuje propojení.</span><span class="sxs-lookup"><span data-stu-id="9a606-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="9a606-117">Funkce jazyka JavaScript `changeOpacity()` musí nejprve najít ovládací prvek `DropShadowExtender` na stránce.</span><span class="sxs-lookup"><span data-stu-id="9a606-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="9a606-118">ASP.NET AJAX definuje metodu `$find()` pro přesně danou úlohu.</span><span class="sxs-lookup"><span data-stu-id="9a606-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="9a606-119">Pak metoda `get_Opacity()` načte aktuální neprůhlednost, metoda `set_Opacity()` ji nastaví.</span><span class="sxs-lookup"><span data-stu-id="9a606-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="9a606-120">Kód jazyka JavaScript pak vloží aktuální hodnotu neprůhlednosti v prvku `<label>`:</span><span class="sxs-lookup"><span data-stu-id="9a606-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

<span data-ttu-id="9a606-121">[![změna neprůhlednosti na straně klienta](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9a606-121">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="9a606-122">Neprůhlednost se mění na straně klienta ([kliknutím zobrazíte obrázek v plné velikosti).](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="9a606-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9a606-123">[Předchozí](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [Další](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9a606-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
