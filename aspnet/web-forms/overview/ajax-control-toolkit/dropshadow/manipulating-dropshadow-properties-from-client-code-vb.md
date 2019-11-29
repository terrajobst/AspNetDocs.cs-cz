---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Manipulace s DropShadow vlastnostmi z klientského kódu (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Vlastnosti tohoto zařízení lze také změnit pomocí JavaScrip klienta...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574042"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="bfb2a-104">Změna vlastností ovládacího prvku DropShadow klientským kódem (VB)</span><span class="sxs-lookup"><span data-stu-id="bfb2a-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="bfb2a-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="bfb2a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="bfb2a-106">[Stažení kódu](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="bfb2a-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="bfb2a-107">Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="bfb2a-108">Vlastnosti tohoto zařízení lze také změnit pomocí kódu JavaScriptu klienta.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-108">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="bfb2a-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="bfb2a-109">Overview</span></span>

<span data-ttu-id="bfb2a-110">Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="bfb2a-111">Vlastnosti tohoto zařízení lze také změnit pomocí kódu JavaScriptu klienta.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="bfb2a-112">Uvedené</span><span class="sxs-lookup"><span data-stu-id="bfb2a-112">Steps</span></span>

<span data-ttu-id="bfb2a-113">Kód začíná panelem obsahujícím některé řádky textu:</span><span class="sxs-lookup"><span data-stu-id="bfb2a-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="bfb2a-114">Přidružená Třída CSS dává panelu na skvělé barvy pozadí:</span><span class="sxs-lookup"><span data-stu-id="bfb2a-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="bfb2a-115">Přidá se `DropShadowExtender`, aby se panel rozšířil na efekt vrženého stínu, což je neprůhlednost nastavené na 50%:</span><span class="sxs-lookup"><span data-stu-id="bfb2a-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="bfb2a-116">Pak ovládací prvek ASP.NET AJAX `ScriptManager` umožňuje, aby sada nástrojů pracovala:</span><span class="sxs-lookup"><span data-stu-id="bfb2a-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="bfb2a-117">Další panel obsahuje dva odkazy JavaScriptu pro nastavení neprůhlednosti vrženého stínu: odkaz minus snižuje průhlednost stínu, a proto se ho zvyšuje propojení.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="bfb2a-118">Funkce jazyka JavaScript `changeOpacity()` musí nejprve najít ovládací prvek `DropShadowExtender` na stránce.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="bfb2a-119">ASP.NET AJAX definuje metodu `$find()` pro přesně danou úlohu.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="bfb2a-120">Pak metoda `get_Opacity()` načte aktuální neprůhlednost, metoda `set_Opacity()` ji nastaví.</span><span class="sxs-lookup"><span data-stu-id="bfb2a-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="bfb2a-121">Kód jazyka JavaScript pak vloží aktuální hodnotu neprůhlednosti v prvku `<label>`:</span><span class="sxs-lookup"><span data-stu-id="bfb2a-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

<span data-ttu-id="bfb2a-122">[![změna neprůhlednosti na straně klienta](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bfb2a-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="bfb2a-123">Neprůhlednost se mění na straně klienta ([kliknutím zobrazíte obrázek v plné velikosti).](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="bfb2a-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bfb2a-124">Předchozí</span><span class="sxs-lookup"><span data-stu-id="bfb2a-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
