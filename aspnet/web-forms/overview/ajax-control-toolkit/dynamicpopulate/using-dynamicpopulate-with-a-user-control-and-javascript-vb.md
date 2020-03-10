---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: Použití ovládacího prvku DynamicPopulate s uživatelským ovládacím prvkem a jazykem JavaScript (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613671"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="0e4a0-103">Použití ovládacího prvku DynamicPopulate s uživatelským ovládacím prvkem a JavaScriptem (VB)</span><span class="sxs-lookup"><span data-stu-id="0e4a0-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>

<span data-ttu-id="0e4a0-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0e4a0-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0e4a0-105">[Stažení kódu](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0e4a0-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="0e4a0-106">Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="0e4a0-107">Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="0e4a0-108">Zvláštní péči je však nutné vzít v případě, že se v uživatelském ovládacím prvku nachází zařízení.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="0e4a0-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="0e4a0-109">Overview</span></span>

<span data-ttu-id="0e4a0-110">Ovládací prvek `DynamicPopulate` v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="0e4a0-111">Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="0e4a0-112">Zvláštní péči je však nutné vzít v případě, že se v uživatelském ovládacím prvku nachází zařízení.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="0e4a0-113">Kroky</span><span class="sxs-lookup"><span data-stu-id="0e4a0-113">Steps</span></span>

<span data-ttu-id="0e4a0-114">Nejprve potřebujete webovou službu ASP.NET, která implementuje metodu volanou ovládacím prvkem `DynamicPopulateExtender`.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="0e4a0-115">Webová služba implementuje metodu `getDate()`, která očekává jeden argument typu String, nazvaný `contextKey`, protože ovládací prvek `DynamicPopulate` odesílá jednu část informací o kontextu s každým voláním webové služby.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="0e4a0-116">Zde je kód (soubory `DynamicPopulate.vb.asmx`), který načte aktuální datum v jednom ze tří formátů:</span><span class="sxs-lookup"><span data-stu-id="0e4a0-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="0e4a0-117">V dalším kroku vytvořte nový uživatelský ovládací prvek (`.ascx` soubor) označený následující deklarací v prvním řádku:</span><span class="sxs-lookup"><span data-stu-id="0e4a0-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="0e4a0-118">&lt;`label`&gt; prvek bude použit k zobrazení dat přicházejících ze serveru.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="0e4a0-119">V souboru uživatelského ovládacího prvku budeme používat tři přepínače, přičemž každý z nich představuje jeden ze tří možných formátů data, které webová služba podporuje.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="0e4a0-120">Když uživatel klikne na jeden z přepínačů, prohlížeč spustí kód JavaScriptu, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="0e4a0-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="0e4a0-121">Tento kód přistupuje k `DynamicPopulateExtender` (nedělejte si starosti s neobvyklým ID, bude popsaný později) a aktivuje dynamické naplnění dat.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="0e4a0-122">V kontextu aktuálního přepínače `this.value` odkazuje na jeho hodnotu, která je `format1`, `format2` nebo `format3` přesně to, co Webová metoda očekává.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="0e4a0-123">V uživatelském ovládacím prvku již chybí jediná věc `DynamicPopulateExtender` ovládací prvek, který propojuje přepínače s webovou službou.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="0e4a0-124">Znovu si můžete všimnout nezvyklého ID použitého v ovládacím prvku: `mcd1$myDate` místo `myDate`.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="0e4a0-125">Dříve se kód jazyka JavaScript použil `mcd1_dpe1` pro přístup k `DynamicPopulateExtender` namísto `dpe1`. Tato strategie pojmenovávání je zvláštní požadavek při použití `DynamicPopulateExtender` v rámci uživatelského ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="0e4a0-126">Kromě toho je nutné vložit uživatelský ovládací prvek tak, aby všechno fungoval.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="0e4a0-127">Vytvořte novou stránku ASP.NET a zaregistrujte předponu značky pro uživatelský ovládací prvek, který jste právě implementovali:</span><span class="sxs-lookup"><span data-stu-id="0e4a0-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="0e4a0-128">Potom do nové stránky přidejte ovládací prvek ASP.NET AJAX `ScriptManager`:</span><span class="sxs-lookup"><span data-stu-id="0e4a0-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="0e4a0-129">Nakonec přidejte uživatelský ovládací prvek na stránku.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="0e4a0-130">Je nutné nastavit jeho atribut `ID` (a `runat="server"`, samozřejmě), ale musíte ho také nastavit na konkrétní název: `mcd1`, protože se jedná o předponu použitou v uživatelském ovládacím prvku pro přístup pomocí JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="0e4a0-131">A to je vše!</span><span class="sxs-lookup"><span data-stu-id="0e4a0-131">And that's it!</span></span> <span data-ttu-id="0e4a0-132">Stránka se chová podle očekávání: uživatel klikne na jeden z přepínačů, ovládací prvek v sadě nástrojů volá webovou službu a zobrazí aktuální datum v požadovaném formátu.</span><span class="sxs-lookup"><span data-stu-id="0e4a0-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="0e4a0-133">[![, že se přepínače nacházejí v uživatelském ovládacím prvku](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0e4a0-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="0e4a0-134">Přepínače se nacházejí v uživatelském ovládacím prvku ([kliknutím zobrazíte obrázek v plné velikosti).](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0e4a0-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0e4a0-135">Předchozí</span><span class="sxs-lookup"><span data-stu-id="0e4a0-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
