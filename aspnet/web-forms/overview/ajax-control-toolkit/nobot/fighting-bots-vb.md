---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: Boj s roboty (VB) | Dokumentace Microsoftu
author: wenz
description: Automatizované robotů sádra webové protokoly a další weby s nevyžádanou poštou, odesílání formulářů komentář bez nutnosti zásahu uživatele. Ovládací prvek NoBot v Con technologie ASP.NET AJAX...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: 8b2a2d2d72bfcf3ce8b3b345fda0bad5a37818ee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066553"
---
<a name="fighting-bots-vb"></a><span data-ttu-id="ab781-104">Boj s roboty (VB)</span><span class="sxs-lookup"><span data-stu-id="ab781-104">Fighting Bots (VB)</span></span>
====================
<span data-ttu-id="ab781-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ab781-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ab781-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ab781-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span></span>

> <span data-ttu-id="ab781-107">Automatizované robotů sádra webové protokoly a další weby s nevyžádanou poštou, odesílání formulářů komentář bez nutnosti zásahu uživatele.</span><span class="sxs-lookup"><span data-stu-id="ab781-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="ab781-108">Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může pomoct bojují těchto robotů.</span><span class="sxs-lookup"><span data-stu-id="ab781-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>


## <a name="overview"></a><span data-ttu-id="ab781-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="ab781-109">Overview</span></span>

<span data-ttu-id="ab781-110">Automatizované robotů sádra webové protokoly a další weby s nevyžádanou poštou, odesílání formulářů komentář bez nutnosti zásahu uživatele.</span><span class="sxs-lookup"><span data-stu-id="ab781-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="ab781-111">Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může pomoct bojují těchto robotů.</span><span class="sxs-lookup"><span data-stu-id="ab781-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="ab781-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="ab781-112">Steps</span></span>

<span data-ttu-id="ab781-113">Jeden běžný postup, se kterými porazíte robotů je použití CAPTCHAs zcela automatizovat veřejné Turing test zjistit počítače a od sebe lidí.</span><span class="sxs-lookup"><span data-stu-id="ab781-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="ab781-114">Turing test byl původně test kde někdo museli rozhodovat, jestli je partnerem komunikace člověk nebo počítač.</span><span class="sxs-lookup"><span data-stu-id="ab781-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="ab781-115">Na webu testu CAPTCHA obvykle obsahuje bitovou kopii s některé zkreslený písmena v něm.</span><span class="sxs-lookup"><span data-stu-id="ab781-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="ab781-116">Cílem je, že může číst pouze lidských písmena v imagi, zatímco OCR algoritmy se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="ab781-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="ab781-117">Existuje několik výhod a nevýhod tohoto přístupu diskusi o to je však nad rámec tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="ab781-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="ab781-118">Je však ovládacího prvku v ASP.NET AJAX Control Toolkit, který nabízí podobný přístup: `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="ab781-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="ab781-119">Je snazší překonat než testu CAPTCHA, ale je velmi snadno používá a tarify velmi dobře ve službě websites jako blogy, kde bude považován za úspěšné Pokud většinu nevyžádané pošty pokusy jsou zrušena, což `NoBot` ovládacího prvku můžete provést.</span><span class="sxs-lookup"><span data-stu-id="ab781-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="ab781-120">`NoBot` zachycuje postback aktuální webové formuláře ASP.NET, pokud je splněna alespoň jedna z těchto podmínek:</span><span class="sxs-lookup"><span data-stu-id="ab781-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="ab781-121">Prohlížeči nepodaří vyřešit díl stavebnice JavaScript (například při deaktivaci JavaScript)</span><span class="sxs-lookup"><span data-stu-id="ab781-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="ab781-122">Formulář pro rychlé odeslané uživatele</span><span class="sxs-lookup"><span data-stu-id="ab781-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="ab781-123">IP adresa klienta odeslání formuláře příliš často v určitou dobu.</span><span class="sxs-lookup"><span data-stu-id="ab781-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="ab781-124">Za účelem ověření pro tyto podmínky `NoBot` ovládací prvek požaduje tyto atributy (všechny z nich volitelný):</span><span class="sxs-lookup"><span data-stu-id="ab781-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="ab781-125">`ResponseMinimumDelaySeconds` minimální velikost sady sekund mezi jednotlivými zpětnými odesláními</span><span class="sxs-lookup"><span data-stu-id="ab781-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="ab781-126">`CutoffWindowSeconds` Délka Časový interval, ve kterém jsou postbacků extenderu jedna IP adresa míry</span><span class="sxs-lookup"><span data-stu-id="ab781-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="ab781-127">`CutoffMaximumInstances` maximální velikost sady sekund na časový interval</span><span class="sxs-lookup"><span data-stu-id="ab781-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="ab781-128">Následující kód požadavky tohoto aspoň 2 sekundy uplynout mezi jednotlivými zpětnými odesláními a, které existují pouze pět zpětného odeslání nebo nižší v rámci intervalu 30 sekund:</span><span class="sxs-lookup"><span data-stu-id="ab781-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

<span data-ttu-id="ab781-129">Potom jako obvykle, nezapomeňte zahrnout `ScriptManager` na stránce tak, aby je načtena knihovna ASP.NET AJAX a Control Toolkit je možné:</span><span class="sxs-lookup"><span data-stu-id="ab781-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

<span data-ttu-id="ab781-130">Protože většina kontrol `NoBot` dělá dojít na straně serveru, je potřeba zkontrolovat výsledek tyto ověření.</span><span class="sxs-lookup"><span data-stu-id="ab781-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="ab781-131">To lze provést zavoláním `NoBot`společnosti `IsValid()` metody.</span><span class="sxs-lookup"><span data-stu-id="ab781-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="ab781-132">Má jeden argument (jako `out` parametr /`ByRef` parametrů) typu `NoBotState`.</span><span class="sxs-lookup"><span data-stu-id="ab781-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="ab781-133">Řetězcové vyjádření obsahuje příčinu selhání kontroly a `Valid` jinak.</span><span class="sxs-lookup"><span data-stu-id="ab781-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="ab781-134">Následující kód vracel zprávu podle `NoBot`je výsledek:</span><span class="sxs-lookup"><span data-stu-id="ab781-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

<span data-ttu-id="ab781-135">Nakonec musíte formuláře pro odeslání a prvku popisku na výstup zprávu, a vy budete hotovi!</span><span class="sxs-lookup"><span data-stu-id="ab781-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

<span data-ttu-id="ab781-136">Při spouštění tohoto skriptu a deaktivovat JavaScript nebo odesláním formuláře v prvních dvou sekund nebo odesláním formuláře sedminásobně během 30 sekund, zobrazí se chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="ab781-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="ab781-137">Ale pomocí tohoto ovládacího prvku obezřetně, protože pouze 90 95 % uživatelé mít JavaScript aktivovat, proto se nezdaří % 5 až 10 uživatelů `NoBot`v testu.</span><span class="sxs-lookup"><span data-stu-id="ab781-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>


<span data-ttu-id="ab781-138">[![Tato chybová zpráva by mohla být způsobena robota](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ab781-138">[![This error message could have been caused by a bot](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span></span>

<span data-ttu-id="ab781-139">Tato chybová zpráva by mohla být způsobena robota ([kliknutím ji zobrazíte obrázek v plné velikosti](fighting-bots-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ab781-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ab781-140">Předchozí</span><span class="sxs-lookup"><span data-stu-id="ab781-140">Previous</span></span>](fighting-bots-cs.md)