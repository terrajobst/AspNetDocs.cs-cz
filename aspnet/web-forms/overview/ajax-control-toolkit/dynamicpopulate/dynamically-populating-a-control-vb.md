---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: Dynamické naplnění ovládacího prvku (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599403"
---
# <a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="8c382-103">Dynamické naplnění ovládacího prvku (VB)</span><span class="sxs-lookup"><span data-stu-id="8c382-103">Dynamically Populating a Control (VB)</span></span>

<span data-ttu-id="8c382-104">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8c382-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8c382-105">[Stažení kódu](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8c382-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="8c382-106">Ovládací prvek ovládacího prvku DynamicPopulate v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky.</span><span class="sxs-lookup"><span data-stu-id="8c382-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="8c382-107">Přehled</span><span class="sxs-lookup"><span data-stu-id="8c382-107">Overview</span></span>

<span data-ttu-id="8c382-108">Ovládací prvek `DynamicPopulate` v ASP.NET AJAX Control Toolkit volá webovou službu (nebo metodu stránky) a vyplní výslednou hodnotu do cílového ovládacího prvku na stránce bez obnovení stránky.</span><span class="sxs-lookup"><span data-stu-id="8c382-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="8c382-109">V tomto kurzu se dozvíte, jak tuto sadu nastavit.</span><span class="sxs-lookup"><span data-stu-id="8c382-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="8c382-110">Uvedené</span><span class="sxs-lookup"><span data-stu-id="8c382-110">Steps</span></span>

<span data-ttu-id="8c382-111">Nejprve potřebujete webovou službu ASP.NET, která implementuje metodu volanou `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="8c382-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="8c382-112">Třída webové služby vyžaduje atribut `ScriptService`, který je definován v rámci `Microsoft.Web.Script.Services`; v opačném případě ASP.NET AJAX nemůže vytvořit proxy server JavaScriptu na straně klienta pro webovou službu, která je zase požadována `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="8c382-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="8c382-113">Metoda web musí očekávat jeden argument typu String s názvem `contextKey`, protože ovládací prvek `DynamicPopulate` odesílá jednu část informací o kontextu pro každé volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="8c382-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="8c382-114">Následující webová služba vrátí aktuální datum ve formátu reprezentovaném argumentem `contextKey`:</span><span class="sxs-lookup"><span data-stu-id="8c382-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="8c382-115">Webová služba se pak uloží jako `DynamicPopulate.vb.asmx`.</span><span class="sxs-lookup"><span data-stu-id="8c382-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="8c382-116">Alternativně můžete implementovat metodu `getDate()` jako metodu stránky na stránce vlastní ASP.NET s ovládacím prvkem `DynamicPopulate`.</span><span class="sxs-lookup"><span data-stu-id="8c382-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="8c382-117">V dalším kroku vytvořte nový soubor ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8c382-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="8c382-118">Jako vždy je prvním krokem vložení `ScriptManager` do aktuální stránky, aby se načetla knihovna AJAX ASP.NET a aby sada nástrojů Control Toolkit fungovala takto:</span><span class="sxs-lookup"><span data-stu-id="8c382-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="8c382-119">Pak přidejte ovládací prvek popisek (například pomocí ovládacího prvku HTML se stejným názvem nebo &lt;`asp:Label` /&gt; webového ovládacího prvku), který bude později zobrazovat výsledek volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="8c382-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="8c382-120">Tlačítko HTML (jako ovládací prvek HTML, protože nepotřebujeme postback na server), se pak použije k aktivaci dynamického naplnění:</span><span class="sxs-lookup"><span data-stu-id="8c382-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="8c382-121">Nakonec potřebujeme `DynamicPopulateExtender` řízení k vytváření kabelů.</span><span class="sxs-lookup"><span data-stu-id="8c382-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="8c382-122">Budou nastaveny následující atributy (Kromě zjevných `ID` a `runat`=`"server"`):</span><span class="sxs-lookup"><span data-stu-id="8c382-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="8c382-123">`TargetControlID`, kam se má vložit výsledek z volání webové služby</span><span class="sxs-lookup"><span data-stu-id="8c382-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="8c382-124">`ServicePath` cesta k webové službě (vynechejte, pokud chcete použít metodu stránky)</span><span class="sxs-lookup"><span data-stu-id="8c382-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="8c382-125">`ServiceMethod` název metody web nebo metody stránky</span><span class="sxs-lookup"><span data-stu-id="8c382-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="8c382-126">`ContextKey` informace o kontextu, které se mají odeslat webové službě</span><span class="sxs-lookup"><span data-stu-id="8c382-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="8c382-127">`PopulateTriggerControlID` element, který aktivuje volání webové služby</span><span class="sxs-lookup"><span data-stu-id="8c382-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="8c382-128">`ClearContentsDuringUpdate`, jestli se má při volání webové služby vyprázdnit cílový element</span><span class="sxs-lookup"><span data-stu-id="8c382-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="8c382-129">Jak vidíte, ovládací prvek vyžaduje některé informace, ale vše na místo je poměrně přímé.</span><span class="sxs-lookup"><span data-stu-id="8c382-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="8c382-130">Zde je značka ovládacího prvku `DynamicPopulateExtender` v aktuálním scénáři:</span><span class="sxs-lookup"><span data-stu-id="8c382-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="8c382-131">Spusťte stránku ASP.NET v prohlížeči a klikněte na tlačítko. zobrazí se aktuální datum ve formátu měsíc-den v roce.</span><span class="sxs-lookup"><span data-stu-id="8c382-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="8c382-132">[![kliknutí na tlačítko načte datum ze serveru.](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8c382-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="8c382-133">Kliknutím na tlačítko se načte datum ze serveru ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-populating-a-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8c382-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8c382-134">[Předchozí](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [Další](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8c382-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
