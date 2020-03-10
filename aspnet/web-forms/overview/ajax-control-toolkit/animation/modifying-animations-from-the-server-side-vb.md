---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: Úprava animací ze strany serveru (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace také mohou...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597998"
---
# <a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="abb95-104">Změna animací ze strany serveru (VB)</span><span class="sxs-lookup"><span data-stu-id="abb95-104">Modifying Animations From The Server Side (VB)</span></span>

<span data-ttu-id="abb95-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="abb95-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="abb95-106">[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="abb95-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="abb95-107">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="abb95-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="abb95-108">Animace se taky můžou změnit na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="abb95-108">The animations may also be changed on the server-side</span></span>

## <a name="overview"></a><span data-ttu-id="abb95-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="abb95-109">Overview</span></span>

<span data-ttu-id="abb95-110">Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="abb95-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="abb95-111">Animace se taky můžou změnit na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="abb95-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="abb95-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="abb95-112">Steps</span></span>

<span data-ttu-id="abb95-113">Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="abb95-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="abb95-114">Animace se použije na panel textu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="abb95-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="abb95-115">V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:</span><span class="sxs-lookup"><span data-stu-id="abb95-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="abb95-116">Zbytek kódu se spouští na straně serveru a nepoužívá značky; místo toho používá kód k vytvoření `AnimationExtender`ho ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="abb95-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="abb95-117">Sada Control Toolkit ale v současné době neposkytuje přístup rozhraní API k vytváření jednotlivých animací.</span><span class="sxs-lookup"><span data-stu-id="abb95-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="abb95-118">Je však možné nastavit vlastnost animací `AnimationExtender`na řetězec obsahující značku XML použitou při deklarativním přiřazení animací.</span><span class="sxs-lookup"><span data-stu-id="abb95-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="abb95-119">Chcete-li vytvořit XML, které nesmí obsahovat prvek `<Animations>` můžete použít podporu XML .NET Framework nebo, jak je uvedeno v následujícím kódu, pouze zadat řetězec:</span><span class="sxs-lookup"><span data-stu-id="abb95-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="abb95-120">Nakonec přidejte ovládací prvek `AnimationExtender` do aktuální stránky v rámci `<form runat="server">` elementu a ujistěte se, že je animace zahrnutá a spuštěná:</span><span class="sxs-lookup"><span data-stu-id="abb95-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

<span data-ttu-id="abb95-121">[![je animace vytvořena pomocí kódu/VB na straně C#serveru](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="abb95-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="abb95-122">Animace je vytvořena pomocí/vb kódu na straně C#serveru ([kliknutím zobrazíte obrázek v plné velikosti).](modifying-animations-from-the-server-side-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="abb95-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="abb95-123">[Předchozí](triggering-an-animation-in-another-control-vb.md)
> [Další](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="abb95-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
