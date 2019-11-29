---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Vytvoření číselného ovládacího prvku nahoru/dolů pomocí back-endu webovéC#služby () | Microsoft Docs
author: wenz
description: Místo toho, aby uživatel zadalo zadat hodnotu do zaškrtávacího políčka, by se měl v systému Windows a jiných operačních systémech jednat o další ovládací prvek c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598884"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="e12d4-103">Vytvoření ovládacího prvku Numeric Up/Down webovou službou typu back-end (C#)</span><span class="sxs-lookup"><span data-stu-id="e12d4-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>

<span data-ttu-id="e12d4-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e12d4-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e12d4-105">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e12d4-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="e12d4-106">Místo toho, aby uživatel zadalo zadat hodnotu do zaškrtávacího políčka, může být číselná hodnota ovládacího prvku (která existuje v systému Windows a dalších operačních systémech), a to pohodlnější.</span><span class="sxs-lookup"><span data-stu-id="e12d4-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="e12d4-107">Ve výchozím nastavení ovládací prvek NumericUpDown vždycky zvyšuje nebo snižuje hodnotu o 1, ale webová služba prokáže větší flexibilitu.</span><span class="sxs-lookup"><span data-stu-id="e12d4-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="e12d4-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="e12d4-108">Overview</span></span>

<span data-ttu-id="e12d4-109">Místo toho, aby uživatel zadalo zadat hodnotu do zaškrtávacího políčka, může být číselná hodnota ovládacího prvku (která existuje v systému Windows a dalších operačních systémech), a to pohodlnější.</span><span class="sxs-lookup"><span data-stu-id="e12d4-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="e12d4-110">Ve výchozím nastavení `NumericUpDown` ovládací prvek vždy zvyšuje nebo snižuje hodnotu o 1, ale webová služba prokáže větší flexibilitu.</span><span class="sxs-lookup"><span data-stu-id="e12d4-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="e12d4-111">Uvedené</span><span class="sxs-lookup"><span data-stu-id="e12d4-111">Steps</span></span>

<span data-ttu-id="e12d4-112">ASP.NET AJAX Control Toolkit obsahuje rozšíření `NumericUpDown`, které do textového pole automaticky přidá dvě tlačítka: jednu pro zvýšení své hodnoty, jednu pro snížení její hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e12d4-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="e12d4-113">Nicméně ovládací prvek podporuje také volání webové služby (nebo volání metody stránky).</span><span class="sxs-lookup"><span data-stu-id="e12d4-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="e12d4-114">Při každém kliknutí na tlačítko nahoru nebo dolů se kód JavaScriptu připojí k webovému serveru a spustí metodu.</span><span class="sxs-lookup"><span data-stu-id="e12d4-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="e12d4-115">Signatura metody je následující:</span><span class="sxs-lookup"><span data-stu-id="e12d4-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="e12d4-116">Argument `current` je aktuální hodnota v textovém poli; atribut `tag` jsou další kontextová data, která lze nastavit jako vlastnost zařízení `NumericUpDown` (ale není vyžadováno).</span><span class="sxs-lookup"><span data-stu-id="e12d4-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="e12d4-117">V této ukázce má číselný ovládací prvek číselníku jenom hodnoty, které mají dvě mocniny: 1, 2, 4, 8, 16, 32, 64 a tak dále.</span><span class="sxs-lookup"><span data-stu-id="e12d4-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="e12d4-118">Proto metoda, která se spustí, když chce uživatel zvýšit hodnotu, musí mít dvojnásobek staré hodnoty; Druhá metoda musí rozdělit hodnotu dvěma.</span><span class="sxs-lookup"><span data-stu-id="e12d4-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="e12d4-119">Takže tady je kompletní webová služba:</span><span class="sxs-lookup"><span data-stu-id="e12d4-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="e12d4-120">Nakonec vytvořte novou stránku ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e12d4-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="e12d4-121">V obvyklých případech potřebujete `ScriptManager` ovládací prvek, ovládací prvek `TextBox` a ovládací prvek `NumericUpDownExtender`.</span><span class="sxs-lookup"><span data-stu-id="e12d4-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="e12d4-122">V takovém případě je nutné zadat informace o webové službě:</span><span class="sxs-lookup"><span data-stu-id="e12d4-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="e12d4-123">`ServiceDownMethod` název metody webové metody nebo stránky</span><span class="sxs-lookup"><span data-stu-id="e12d4-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="e12d4-124">`ServiceDownPath` cesta k webové službě s metodou služby Down; vynechat, pokud používáte metodu stránky</span><span class="sxs-lookup"><span data-stu-id="e12d4-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="e12d4-125">`ServiceUpMethod` název metody webové metody nebo metody stránky</span><span class="sxs-lookup"><span data-stu-id="e12d4-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="e12d4-126">cesta `ServiceUpPath` k webové službě s metodou up Service; vynechat, pokud používáte metodu stránky</span><span class="sxs-lookup"><span data-stu-id="e12d4-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="e12d4-127">Zde je kompletní kód pro stránku:</span><span class="sxs-lookup"><span data-stu-id="e12d4-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="e12d4-128">Pokud spouštíte stránku, Všimněte si, jak se hodnota v textovém poli vždy zdvojnásobí po kliknutí na horní tlačítko a po kliknutí na tlačítko dolů se zmenší.</span><span class="sxs-lookup"><span data-stu-id="e12d4-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>

<span data-ttu-id="e12d4-129">[![pouze čísla, která jsou mocninou 2.](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e12d4-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="e12d4-130">Zobrazí se pouze čísla, která jsou mocninou 2 ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e12d4-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e12d4-131">Next</span><span class="sxs-lookup"><span data-stu-id="e12d4-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
