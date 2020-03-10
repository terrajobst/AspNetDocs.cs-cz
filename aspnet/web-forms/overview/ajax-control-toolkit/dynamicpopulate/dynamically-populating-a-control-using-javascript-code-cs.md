---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: Dynamické naplnění ovládacího prvku pomocí kóduC#jazyka JavaScript () | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 24dc358427dec3ffcba16d00041c9a2db657e7e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535740"
---
# <a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="227d7-103">Dynamické naplnění ovládacího prvku javascriptovým kódem (C#)</span><span class="sxs-lookup"><span data-stu-id="227d7-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>

<span data-ttu-id="227d7-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="227d7-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="227d7-105">[Stažení kódu](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="227d7-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="227d7-106">Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky.</span><span class="sxs-lookup"><span data-stu-id="227d7-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="227d7-107">Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="227d7-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="227d7-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="227d7-108">Overview</span></span>

<span data-ttu-id="227d7-109">Ovládací prvek `DynamicPopulate` v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky.</span><span class="sxs-lookup"><span data-stu-id="227d7-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="227d7-110">Je také možné aktivovat plnění pomocí vlastního kódu JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="227d7-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="227d7-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="227d7-111">Steps</span></span>

<span data-ttu-id="227d7-112">Nejprve potřebujete webovou službu ASP.NET, která implementuje metodu volanou ovládacím prvkem `DynamicPopulateExtender`.</span><span class="sxs-lookup"><span data-stu-id="227d7-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="227d7-113">Webová služba implementuje metodu `getDate()`, která očekává jeden argument typu String, nazvaný `contextKey`, protože ovládací prvek `DynamicPopulate` odesílá jednu část informací o kontextu s každým voláním webové služby.</span><span class="sxs-lookup"><span data-stu-id="227d7-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="227d7-114">Zde je kód (soubor `DynamicPopulate.cs.asmx`), který načte aktuální datum v jednom ze tří formátů:</span><span class="sxs-lookup"><span data-stu-id="227d7-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="227d7-115">V dalším kroku vytvořte nový web ASP.NET a začněte s ovládacím prvkem ASP.NET AJAX ScriptManager:</span><span class="sxs-lookup"><span data-stu-id="227d7-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="227d7-116">Pak přidejte ovládací prvek popisek (například pomocí ovládacího prvku HTML se stejným názvem nebo ovládacího prvku `<asp:Label />` Web), který bude později zobrazovat výsledek volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="227d7-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="227d7-117">Dále zahrňte ovládací prvek `DynamicPopulateExtender` a poskytněte informace o webové službě, cílový ovládací prvek, ale ne název ovládacího prvku, který aktivuje tuto populaci, a to pomocí vlastního JavaScriptu!</span><span class="sxs-lookup"><span data-stu-id="227d7-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="227d7-118">Nyní do části JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="227d7-118">Now to the JavaScript part.</span></span> <span data-ttu-id="227d7-119">Funkce `$find()` definovaná knihovnou ASP.NET AJAX vrací odkaz na objekty na straně serveru sady nástrojů ASP.NET AJAX Control Toolkit, jako je například `DynamicPopulateExtender`.</span><span class="sxs-lookup"><span data-stu-id="227d7-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="227d7-120">V aktuálním souboru `$find("dpe")` vrátí odkaz na jeden ovládací prvek `DynamicPopulateExtender` na stránce.</span><span class="sxs-lookup"><span data-stu-id="227d7-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="227d7-121">Zpřístupňuje metodu nazvanou `populate()`, která aktivuje proces dynamického naplnění.</span><span class="sxs-lookup"><span data-stu-id="227d7-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="227d7-122">Metoda `populate()` vyžaduje jeden argument: kontextový klíč, který bude sloužit jako argument webové metody `getDate()`.</span><span class="sxs-lookup"><span data-stu-id="227d7-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="227d7-123">Například `$find("dpe").populate("format1")` by popisek naplnil aktuální datum ve formátu měsíc-den v roce.</span><span class="sxs-lookup"><span data-stu-id="227d7-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="227d7-124">Aby byla ukázka pružnější, uživatel teď může zvolit několik formátů data.</span><span class="sxs-lookup"><span data-stu-id="227d7-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="227d7-125">Pro každý z nich je zobrazen přepínač.</span><span class="sxs-lookup"><span data-stu-id="227d7-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="227d7-126">Jakmile uživatel klikne na přepínač, kód jazyka JavaScript dynamicky naplní popisek na vybraný formát data.</span><span class="sxs-lookup"><span data-stu-id="227d7-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="227d7-127">Tady jsou tato Rádiová tlačítka:</span><span class="sxs-lookup"><span data-stu-id="227d7-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="227d7-128">Všimněte si, že v kontextu přepínače, výraz jazyka JavaScript `this.value` odkazuje na hodnotu aktuálního tlačítka, které se stane přesně stejnými informacemi, se kterou může metoda `getDate()` pracovat.</span><span class="sxs-lookup"><span data-stu-id="227d7-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>

<span data-ttu-id="227d7-129">[![kliknutí na tlačítko načte datum ze serveru ve formátu zadaném](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="227d7-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="227d7-130">Kliknutím na tlačítko načtete datum ze serveru v zadaném formátu ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="227d7-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="227d7-131">[Předchozí](dynamically-populating-a-control-cs.md)
> [Další](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="227d7-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>
