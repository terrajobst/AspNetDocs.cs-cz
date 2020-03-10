---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Použití jazyka AJAX k doručování dynamických aktualizací | Microsoft Docs
author: microsoft
description: Krok 10 implementuje podporu pro přihlášené uživatele, aby ODPOVĚDĚLi na svůj zájem o účast na večeři s využitím přístupu založeného na AJAX, který je integrovaný v podrobnostech na večeři...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600847"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="a7f17-103">Použití jazyka AJAX k dynamickým aktualizacím</span><span class="sxs-lookup"><span data-stu-id="a7f17-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="a7f17-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a7f17-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="a7f17-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="a7f17-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="a7f17-106">Toto je krok 10 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="a7f17-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="a7f17-107">Krok 10 implementuje podporu pro přihlášené uživatele, aby ODPOVĚDĚLi na svůj zájem o účast na večeři s využitím přístupu založeného na AJAX, který je integrovaný na stránce s podrobnostmi o večeři.</span><span class="sxs-lookup"><span data-stu-id="a7f17-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="a7f17-108">Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.</span><span class="sxs-lookup"><span data-stu-id="a7f17-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="a7f17-109">NerdDinner krok 10: AJAX povolující protokoly RSVP</span><span class="sxs-lookup"><span data-stu-id="a7f17-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="a7f17-110">Pojďme teď pro přihlášené uživatele implementovat podporu, která zaznamená svůj zájem o účast na večeři.</span><span class="sxs-lookup"><span data-stu-id="a7f17-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="a7f17-111">Povolíme to s využitím přístupu založeného na AJAX, který je integrovaný na stránce s podrobnostmi o večeři.</span><span class="sxs-lookup"><span data-stu-id="a7f17-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="a7f17-112">Označuje, zda uživatel používá protokol RSVP.</span><span class="sxs-lookup"><span data-stu-id="a7f17-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="a7f17-113">Uživatelé můžou navštívit adresu URL */Dinners/Details/[ID*] a zobrazit podrobnosti o konkrétní večeři:</span><span class="sxs-lookup"><span data-stu-id="a7f17-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="a7f17-114">Metoda akce Details () je implementována takto:</span><span class="sxs-lookup"><span data-stu-id="a7f17-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="a7f17-115">Náš první krok pro implementaci podpory protokolu RSVP bude přidat pomocnou metodu "IsUserRegistered (uživatelské jméno)" do našeho objektu večeře (v rámci předchozí třídy Dinner.cs, kterou jsme vytvořili dříve).</span><span class="sxs-lookup"><span data-stu-id="a7f17-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="a7f17-116">Tato pomocná metoda vrátí hodnotu true nebo false v závislosti na tom, zda uživatel aktuálně hlásí odpověď pro večeři:</span><span class="sxs-lookup"><span data-stu-id="a7f17-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="a7f17-117">Potom můžeme do naší šablony zobrazení Details. aspx přidat následující kód, který zobrazí příslušnou zprávu s oznámením, že je uživatel zaregistrován nebo není pro událost:</span><span class="sxs-lookup"><span data-stu-id="a7f17-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="a7f17-118">A teď když uživatel navštíví večeři, na který se zaregistruje, zobrazí se tato zpráva:</span><span class="sxs-lookup"><span data-stu-id="a7f17-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="a7f17-119">A když navštívíte večeři, že nejsou zaregistrovaní, uvidí následující zprávu:</span><span class="sxs-lookup"><span data-stu-id="a7f17-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="a7f17-120">Implementace metody akce registru</span><span class="sxs-lookup"><span data-stu-id="a7f17-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="a7f17-121">Pojďme teď přidat funkce potřebné k tomu, aby uživatelé mohli na stránce s podrobnostmi povolit zasílání zpráv na večeři.</span><span class="sxs-lookup"><span data-stu-id="a7f17-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="a7f17-122">Pokud to chcete provést, vytvoříme novou třídu "RSVPController" tak, že kliknete pravým tlačítkem na adresář \Controllers a kliknete na příkaz nabídky přidat&gt;Controller.</span><span class="sxs-lookup"><span data-stu-id="a7f17-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="a7f17-123">Implementujeme metodu "Register" v rámci nové třídy RSVPController, která jako argument převezme ID pro večeři, načte příslušný objekt večeře, zkontroluje, jestli je přihlášený uživatel aktuálně v seznamu uživatelů, kteří si ho zaregistrovali, a pokud nepřidá objekt RSVP pro ně:</span><span class="sxs-lookup"><span data-stu-id="a7f17-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="a7f17-124">Všimněte si, jak vracíme jednoduchý řetězec jako výstup metody Action.</span><span class="sxs-lookup"><span data-stu-id="a7f17-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="a7f17-125">Tuto zprávu jsme mohli vložit do šablony zobrazení – ale vzhledem k tomu, že je to malé, budeme jenom používat pomocnou metodu Content () pro základní třídu kontroleru a vrátíte zprávu s řetězcem, jako je výše.</span><span class="sxs-lookup"><span data-stu-id="a7f17-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="a7f17-126">Volání metody akce RSVPForEvent pomocí jazyka AJAX</span><span class="sxs-lookup"><span data-stu-id="a7f17-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="a7f17-127">Použijeme AJAX k vyvolání metody akce registrace z našeho zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="a7f17-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="a7f17-128">Implementace je poměrně jednoduchá.</span><span class="sxs-lookup"><span data-stu-id="a7f17-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="a7f17-129">Nejprve přidáme dva odkazy knihovny skriptu:</span><span class="sxs-lookup"><span data-stu-id="a7f17-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="a7f17-130">První knihovna odkazuje na základní knihovnu skriptů ASP.NET AJAX na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="a7f17-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="a7f17-131">Tento soubor má přibližně 24k velikost (komprimovaná) a obsahuje základní funkce AJAX na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="a7f17-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="a7f17-132">Druhá knihovna obsahuje funkce nástrojů, které se integrují s vestavěnými podpůrnými metodami AJAX v ASP.NET MVC (které budeme brzy používat).</span><span class="sxs-lookup"><span data-stu-id="a7f17-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="a7f17-133">Pak můžeme aktualizovat kód šablony zobrazení, který jsme přidali dříve, takže místo výstupu "Nejste pro tuto událost zaregistrováni", ale vygenerujeme odkaz, který po vložení vyvolá volání AJAX, které vyvolá naši metodu RSVPForEvent akce na našem řadiči protokolu RSVP. a zaprotokoluje uživatele:</span><span class="sxs-lookup"><span data-stu-id="a7f17-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="a7f17-134">Použitá pomocná metoda AJAX. ActionLink () je vestavěná do ASP.NET MVC a je podobná jako pomocná metoda HTML. ActionLink () s tím rozdílem, že místo provedení standardní navigace vytvoří odkaz AJAX na metodu Action při kliknutí na odkaz.</span><span class="sxs-lookup"><span data-stu-id="a7f17-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="a7f17-135">Nad tím voláme metodu akce Register v řadiči "RSVP" a předáte DinnerID jako parametr "ID".</span><span class="sxs-lookup"><span data-stu-id="a7f17-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="a7f17-136">Konečný parametr AjaxOptions, který předáváme, znamená, že chceme převzít obsah vrácený z metody Action a aktualizovat element HTML &lt;div&gt; na stránce, jejíž ID je "rsvpmsg".</span><span class="sxs-lookup"><span data-stu-id="a7f17-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="a7f17-137">A teď když uživatel přejde na večeři, ke kterému ještě nejsou zaregistrované, uvidí pro něj odkaz na protokol RSVP:</span><span class="sxs-lookup"><span data-stu-id="a7f17-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="a7f17-138">Pokud kliknete na odkaz "protokol RSVP pro tuto událost", provedou volání metody Register na řadiči protokolu RSVP volání AJAX a když se dokončí, zobrazí se aktualizovaná zpráva podobná následující:</span><span class="sxs-lookup"><span data-stu-id="a7f17-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="a7f17-139">Šířka pásma sítě a provoz v rámci tohoto volání AJAX jsou skutečně odlehčené.</span><span class="sxs-lookup"><span data-stu-id="a7f17-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="a7f17-140">Když uživatel klikne na odkaz protokol RSVP pro tuto událost, pošle se malý požadavek na síť HTTP POST na adresu URL */Dinners/Register/1* , která vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="a7f17-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="a7f17-141">A odpověď z naší metody akce registrace je jednoduše:</span><span class="sxs-lookup"><span data-stu-id="a7f17-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="a7f17-142">Toto zjednodušené volání je rychlé a bude fungovat i přes pomalou síť.</span><span class="sxs-lookup"><span data-stu-id="a7f17-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="a7f17-143">Přidání animace jQuery</span><span class="sxs-lookup"><span data-stu-id="a7f17-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="a7f17-144">Funkce AJAX, které jsme implementovali, funguje dobře a rychle.</span><span class="sxs-lookup"><span data-stu-id="a7f17-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="a7f17-145">Někdy k tomu může dojít, když si uživatel nemusí všimnout, že odkaz na protokol RSVP byl nahrazen novým textem.</span><span class="sxs-lookup"><span data-stu-id="a7f17-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="a7f17-146">Pokud chcete, aby byl výsledek trochu jasnější, můžeme přidat jednoduchou animaci, která upozorní na zprávu aktualizace.</span><span class="sxs-lookup"><span data-stu-id="a7f17-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="a7f17-147">Výchozí šablona projektu ASP.NET MVC zahrnuje jQuery – vynikající (a velmi oblíbenou) knihovnu JavaScript open source, která je také podporována společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7f17-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="a7f17-148">jQuery poskytuje řadu funkcí, včetně skvělé knihovny pro výběr a efekty HTML modelu HTML.</span><span class="sxs-lookup"><span data-stu-id="a7f17-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="a7f17-149">Pokud chcete použít jQuery, nejdřív na něj přidáte odkaz na skript.</span><span class="sxs-lookup"><span data-stu-id="a7f17-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="a7f17-150">Vzhledem k tomu, že budeme používat jQuery v rámci celé řady míst v rámci našeho webu, přidáme odkaz na skript do souboru hlavní stránky site. Master, aby ho všechny stránky mohli používat.</span><span class="sxs-lookup"><span data-stu-id="a7f17-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="a7f17-151">*Tip: Ujistěte se, že máte nainstalovanou opravu hotfix technologie JavaScript IntelliSense pro VS 2008 SP1, která umožňuje bohatší podporu technologie IntelliSense pro soubory JavaScriptu (včetně jQuery). Můžete si ho stáhnout z: http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="a7f17-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="a7f17-152">Kód napsaný pomocí JQuery často používá globální metodu "$ ()" jazyka JavaScript, která načítá jeden nebo více elementů jazyka HTML pomocí selektoru šablon stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="a7f17-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="a7f17-153">Například *$ ("#rsvpmsg")* vybere libovolný prvek HTML s ID rsvpmsg, zatímco *$ (". něco")* by vybralo všechny prvky s názvem "text" třídy CSS.</span><span class="sxs-lookup"><span data-stu-id="a7f17-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="a7f17-154">Můžete také zapisovat pokročilejší dotazy, jako je "návrat všech zkontrolovaných přepínačů" pomocí dotazu na selektor, jako je: *$ ("vstup [@type= Radio] [@checked]")* .</span><span class="sxs-lookup"><span data-stu-id="a7f17-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="a7f17-155">Po vybrání prvků můžete volat metody, které mají být vyvolány, jako jejich skrývání: *$ ("#rsvpmsg"). Hide ();*</span><span class="sxs-lookup"><span data-stu-id="a7f17-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="a7f17-156">Pro náš scénář protokolu RSVP definujeme jednoduchou funkci JavaScriptu s názvem "AnimateRSVPMessage", která vybere&gt; &lt;div a animuje velikost jejího textového obsahu.</span><span class="sxs-lookup"><span data-stu-id="a7f17-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="a7f17-157">Následující kód začíná textem malý a pak způsobí, že se zvýší v časovém rozmezí 400 milisekund:</span><span class="sxs-lookup"><span data-stu-id="a7f17-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="a7f17-158">Tuto funkci JavaScriptu pak můžeme natočit po úspěšném dokončení volání AJAX tím, že předáte svůj název do pomocné metody AJAX. ActionLink () (přes vlastnost události AjaxOptions "úspěch"):</span><span class="sxs-lookup"><span data-stu-id="a7f17-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="a7f17-159">A teď, když se klikne na odkaz "RSVP pro tuto událost" a naše volání jazyka AJAX se úspěšně dokončí, bude zpráva o obsahu, která se pošle zpátky, animovat a bude růst velká:</span><span class="sxs-lookup"><span data-stu-id="a7f17-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="a7f17-160">Kromě poskytování události "úspěch" objekt AjaxOptions zpřístupňuje události při zahájení, selhání a dokončení, které lze zpracovat (spolu s celou řadou dalších vlastností a užitečnými možnostmi).</span><span class="sxs-lookup"><span data-stu-id="a7f17-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="a7f17-161">Vyčištění – Refaktorovat částečné zobrazení protokolu RSVP</span><span class="sxs-lookup"><span data-stu-id="a7f17-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="a7f17-162">Naše šablona zobrazení podrobností začíná mít za chvilku, což znamená, že se bude porozumět trochu obtížnější.</span><span class="sxs-lookup"><span data-stu-id="a7f17-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="a7f17-163">Pro zlepšení čitelnosti kódu se dokončí vytvořením částečného zobrazení – RSVPStatus. ascx – které zapouzdřuje všechny kódy zobrazení protokolu RSVP pro naši stránku podrobností.</span><span class="sxs-lookup"><span data-stu-id="a7f17-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="a7f17-164">To můžeme udělat tak, že kliknete pravým tlačítkem na složku \Views\Dinners a pak zvolíte příkaz nabídky zobrazení pro přidání&gt;.</span><span class="sxs-lookup"><span data-stu-id="a7f17-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="a7f17-165">Podíváme se, že bude mít objekt večeře jako svůj ViewModel silně typovaného typu.</span><span class="sxs-lookup"><span data-stu-id="a7f17-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="a7f17-166">Pak můžeme obsah protokolu RSVP zkopírovat a vložit z našeho zobrazení Details. aspx.</span><span class="sxs-lookup"><span data-stu-id="a7f17-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="a7f17-167">Až to uděláte, vytvoříme také další částečné zobrazení – EditAndDeleteLinks. ascx – zapouzdřuje náš kód zobrazení odkazu pro úpravy a odstranění.</span><span class="sxs-lookup"><span data-stu-id="a7f17-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="a7f17-168">Také ponecháme objekt večeře jako svůj ViewModel silně typovaného typu a zkopírujete nebo vložíte logiku upravit a odstranit z našich zobrazení Details. aspx.</span><span class="sxs-lookup"><span data-stu-id="a7f17-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="a7f17-169">Šablona zobrazení podrobností teď může do dolní části Přidat dvě volání metody HTML. RenderPartial ():</span><span class="sxs-lookup"><span data-stu-id="a7f17-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="a7f17-170">To způsobuje, že by měl čistič kódu číst a udržovat.</span><span class="sxs-lookup"><span data-stu-id="a7f17-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="a7f17-171">Další krok</span><span class="sxs-lookup"><span data-stu-id="a7f17-171">Next Step</span></span>

<span data-ttu-id="a7f17-172">Teď se podíváme na to, jak můžeme ještě dál používat AJAX a přidat do naší aplikace podporu interaktivního mapování.</span><span class="sxs-lookup"><span data-stu-id="a7f17-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a7f17-173">[Předchozí](secure-applications-using-authentication-and-authorization.md)
> [Další](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="a7f17-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
