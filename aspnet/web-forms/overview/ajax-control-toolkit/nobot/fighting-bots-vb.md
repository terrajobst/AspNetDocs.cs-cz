---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: Boj roboty (VB) | Microsoft Docs
author: wenz
description: Automatizované roboty sádry Weblogs a další weby s nevyžádanými zprávami, odesílání formulářů komentářů bez zásahu uživatele. Ovládací prvek NoBot v ASP.NET AJAX con...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: a8ca71b96cb84c97b1a60ae6a3d1a129cd1b0b10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627391"
---
# <a name="fighting-bots-vb"></a><span data-ttu-id="2d8a7-104">Boj s roboty (VB)</span><span class="sxs-lookup"><span data-stu-id="2d8a7-104">Fighting Bots (VB)</span></span>

<span data-ttu-id="2d8a7-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2d8a7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2d8a7-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2d8a7-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span></span>

> <span data-ttu-id="2d8a7-107">Automatizované roboty sádry Weblogs a další weby s nevyžádanými zprávami, odesílání formulářů komentářů bez zásahu uživatele.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="2d8a7-108">Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může přispět k boji s těmito robotyy.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="overview"></a><span data-ttu-id="2d8a7-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="2d8a7-109">Overview</span></span>

<span data-ttu-id="2d8a7-110">Automatizované roboty sádry Weblogs a další weby s nevyžádanými zprávami, odesílání formulářů komentářů bez zásahu uživatele.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="2d8a7-111">Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může přispět k boji s těmito robotyy.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="2d8a7-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="2d8a7-112">Steps</span></span>

<span data-ttu-id="2d8a7-113">Jedním z běžných způsobů, jak předpovědět roboty, je použití CAPTCHAs plně automatizovaného testu veřejné Turing testování, které sděluje počítačům a Člověkům.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="2d8a7-114">Test Turing byl původně testem, který někdo potřebuje k rozhodnutí, jestli je komunikační partner člověk nebo počítač.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="2d8a7-115">Na webu se CAPTCHA obvykle skládá z obrázku s některými dedeformovanými písmeny.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="2d8a7-116">Nápad je, že písmena na obrázku může přečíst jenom člověk, zatímco algoritmy optického rozpoznávání se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="2d8a7-117">Tento přístup má několik výhod a nevýhody, ale diskuze nad rámec tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="2d8a7-118">V ovládacím prvku ASP.NET AJAX Control Toolkit je však ovládací prvek, který poskytuje podobný přístup: `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="2d8a7-119">Je snazší je překonat než CAPTCHA, ale je velmi snadné použít a tarify na webech, jako jsou Blogy, kde se považují za úspěch, pokud dojde k překonání většiny nevyžádaných zpráv, které může ovládací prvek `NoBot` provádět.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="2d8a7-120">`NoBot` zachycuje postback aktuálního webového formuláře ASP.NET, pokud je splněna alespoň jedna z těchto podmínek:</span><span class="sxs-lookup"><span data-stu-id="2d8a7-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="2d8a7-121">Prohlížeč nedokáže vyřešit skládanku JavaScriptu (například při deaktivaci JavaScriptu).</span><span class="sxs-lookup"><span data-stu-id="2d8a7-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="2d8a7-122">Uživatel odeslal formulář do funkce Fast.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="2d8a7-123">IP adresa klienta odeslala formulář příliš často v určitém časovém období.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="2d8a7-124">Aby bylo možné kontrolovat tyto podmínky, ovládací prvek `NoBot` vyžaduje tyto atributy (všechny nepovinné):</span><span class="sxs-lookup"><span data-stu-id="2d8a7-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="2d8a7-125">`ResponseMinimumDelaySeconds` minimální doba v sekundách mezi zpětnými odesláními</span><span class="sxs-lookup"><span data-stu-id="2d8a7-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="2d8a7-126">`CutoffWindowSeconds` Délka časového intervalu, ve kterém se zpětná volání z jedné IP adresy měří</span><span class="sxs-lookup"><span data-stu-id="2d8a7-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="2d8a7-127">`CutoffMaximumInstances` maximální dobu v sekundách za časový interval</span><span class="sxs-lookup"><span data-stu-id="2d8a7-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="2d8a7-128">Následující značka vyžaduje, aby mezi zpětnými odesláními a v intervalu 30 sekund uplynula alespoň dvě sekundy:</span><span class="sxs-lookup"><span data-stu-id="2d8a7-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

<span data-ttu-id="2d8a7-129">Pak jako obvykle nezapomeňte zahrnout `ScriptManager` do stránky, aby se načetla knihovna AJAX ASP.NET a mohla by se používat ovládací sada Toolkit:</span><span class="sxs-lookup"><span data-stu-id="2d8a7-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

<span data-ttu-id="2d8a7-130">Vzhledem k tomu, že většina kontrol `NoBot` probíhá na straně serveru, je nutné zkontrolovat výsledek těchto ověření.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="2d8a7-131">To lze provést voláním metody `IsValid()` `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="2d8a7-132">Má jeden argument (jako `out` parametr/`ByRef` parametr), který je typu `NoBotState`.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="2d8a7-133">Jeho řetězcová reprezentace obsahuje důvod, kdy se ověření nepovede, a `Valid` jinak.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="2d8a7-134">Následující kód vytvoří výstup zprávy podle výsledku `NoBot`:</span><span class="sxs-lookup"><span data-stu-id="2d8a7-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

<span data-ttu-id="2d8a7-135">Nakonec potřebujete formulář pro odeslání a označení prvku pro výstup zprávy a Vy jste hotovi.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

<span data-ttu-id="2d8a7-136">Když spustíte tento skript a deaktivujete JavaScript nebo odešlete formulář během prvních dvou sekund nebo formulář odešlete do třiceti sekund, zobrazí se chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="2d8a7-137">Tento ovládací prvek se však dá použít i v takovém případě, protože k aktivaci JavaScriptu má jenom asi 90-95% uživatelů, takže 5-10% uživatelů selže `NoBot`testu.</span><span class="sxs-lookup"><span data-stu-id="2d8a7-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>

<span data-ttu-id="2d8a7-138">[![tato chybová zpráva mohla být způsobená robotem.](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2d8a7-138">[![This error message could have been caused by a bot](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span></span>

<span data-ttu-id="2d8a7-139">Tato chybová zpráva mohla být způsobena robotem ([kliknutím zobrazíte obrázek v plné velikosti).](fighting-bots-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2d8a7-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2d8a7-140">Předchozí</span><span class="sxs-lookup"><span data-stu-id="2d8a7-140">Previous</span></span>](fighting-bots-cs.md)
