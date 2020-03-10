---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Pomocník pro Twitter s webovými stránkami ASP.NET | Microsoft Docs
author: Rick-Anderson
description: Toto téma a aplikace ukazují, jak přidat pomocníka pro Twitter do projektu WebMatrix 3. Obsahuje pomocný kód pro Twitter a ukazuje, jak zavolat pomoc...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638556"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="8e6b9-104">Pomocná rutina Twitteru na webových stránkách ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8e6b9-104">Twitter Helper with ASP.NET Web Pages</span></span>

<span data-ttu-id="8e6b9-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8e6b9-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e6b9-106">Pomocníky pro Twitter jsou zastaralé.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="8e6b9-107">Nejnovější nástroje pro zapojení do Twitteru pro weby najdete v tématu [Přehled Twitteru pro websites](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span><span class="sxs-lookup"><span data-stu-id="8e6b9-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="8e6b9-108">Toto téma a aplikace ukazují, jak přidat pomocníka pro Twitter do projektu WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="8e6b9-109">Obsahuje pomocný kód pro Twitter a ukazuje, jak volat pomocné metody.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="8e6b9-110">Tento kód pro soubor Twitter. cshtml vyvinula aplikace **Tian pan** od Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8e6b9-111">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="8e6b9-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="8e6b9-112">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="8e6b9-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="8e6b9-113">Tento kurz funguje také s ASP.NET webovými stránkami 2.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="introduction"></a><span data-ttu-id="8e6b9-114">Úvod</span><span class="sxs-lookup"><span data-stu-id="8e6b9-114">Introduction</span></span>

<span data-ttu-id="8e6b9-115">Toto téma ukazuje, jak přidat pomocníka pro Twitter do vaší aplikace a použít syntaxe Razor pro volání pomocných metod.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="8e6b9-116">Pomocník pro Twitter usnadňuje začleňování tlačítek a widgetů Twitteru do vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="8e6b9-117">Pokud chcete použít pomůcku Twitteru, například časovou osu uživatele nebo výsledky hledání pro hashtag, musíte nejdřív vytvořit [widget na Twitteru](https://twitter.com/settings/widgets).</span><span class="sxs-lookup"><span data-stu-id="8e6b9-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="8e6b9-118">Po vytvoření widgetu se zobrazí ID widgetu. Toto ID widgetu předáte jako parametr při volání pomocných metod, které znázorňují widget.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="8e6b9-119">Toto téma bylo napsáno pro verzi 1,1 rozhraní API pro Twitter.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="8e6b9-120">Přímým přidáním pomocníka pro Twitter do projektu můžete kód pomocné rutiny aktualizovat, pokud se změní rozhraní API pro Twitter.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="8e6b9-121">Informace o instalaci WebMatrixu najdete v tématu [představení ASP.NET webových stránek 2-Začínáme](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8e6b9-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="8e6b9-122">Přidat pomocníka pro Twitter do projektu</span><span class="sxs-lookup"><span data-stu-id="8e6b9-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="8e6b9-123">Pokud chcete přidat pomocníka pro Twitter, nejdřív přidejte do projektu složku s názvem **App\_Code** .</span><span class="sxs-lookup"><span data-stu-id="8e6b9-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="8e6b9-124">Pak vytvořte soubor s názvem **Twitter. cshtml**.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-124">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code složka](twitter-helper/_static/image1.png)

<span data-ttu-id="8e6b9-126">Nahraďte výchozí kód v Twitter. cshtml následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="8e6b9-127">Volání metod Twitteru z webových stránek</span><span class="sxs-lookup"><span data-stu-id="8e6b9-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="8e6b9-128">Následující příklad ukazuje způsob použití pomocných metod Twitteru ze stránky v projektu.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="8e6b9-129">V projektu budete chtít nahradit hodnoty parametrů hodnotami, které jsou relevantní pro vaše potřeby.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="8e6b9-130">Pomocí poskytnutých ID widgetů můžete prozkoumat, jak metody fungují, ale budete chtít vygenerovat vlastní widgety pro váš projekt.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="8e6b9-131">Ne všechny parametry uvedené níže jsou povinné.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="8e6b9-132">Volitelné parametry slouží k přizpůsobení způsobu zobrazení tlačítka nebo pomůcky.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="8e6b9-133">Například tlačítko sledovat vyžaduje pouze zadání uživatelského jména, ale tento příklad ukazuje, jak zahrnout Počet sledujících a jak určit velikost tlačítka a jazyk.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="8e6b9-134">Zobrazení výsledků</span><span class="sxs-lookup"><span data-stu-id="8e6b9-134">See the results</span></span>

<span data-ttu-id="8e6b9-135">Výše uvedený kód vytváří následující tlačítka a widgety.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="8e6b9-136">Tato tlačítka a widgety jsou plně funkční, nikoli snímky obrazovky.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="8e6b9-137">Tlačítko sledovat se zobrazí v španělštině, protože parametr Language byl nastaven na **ES**.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="8e6b9-138">Tlačítko sledovat</span><span class="sxs-lookup"><span data-stu-id="8e6b9-138">Follow Button</span></span>

<span data-ttu-id="8e6b9-139">[Sledovat @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="8e6b9-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="8e6b9-140">Tlačítko pro možnost pro.</span><span class="sxs-lookup"><span data-stu-id="8e6b9-140">Tweet Button</span></span>

<span data-ttu-id="8e6b9-141">[`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>` ve](https://twitter.com/share) stejném</span><span class="sxs-lookup"><span data-stu-id="8e6b9-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="8e6b9-142">Časová osa uživatele (profil)</span><span class="sxs-lookup"><span data-stu-id="8e6b9-142">User Timeline (Profile)</span></span>

<span data-ttu-id="8e6b9-143">[Tweety podle @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="8e6b9-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="8e6b9-144">Oblíbené položky</span><span class="sxs-lookup"><span data-stu-id="8e6b9-144">Favorites</span></span>

<span data-ttu-id="8e6b9-145">[Oblíbené tweety podle @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="8e6b9-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="8e6b9-146">Seznam</span><span class="sxs-lookup"><span data-stu-id="8e6b9-146">List</span></span>

<span data-ttu-id="8e6b9-147">[Tweety z @Microsoft/MS\_\_pásma příjemce](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="8e6b9-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="8e6b9-148">Hledání</span><span class="sxs-lookup"><span data-stu-id="8e6b9-148">Search</span></span>

<span data-ttu-id="8e6b9-149">[Tweety o &quot;#asp .net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="8e6b9-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
