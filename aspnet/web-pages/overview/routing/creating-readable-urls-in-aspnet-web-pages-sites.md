---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: Vytváření čitelných adres URL na webech ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje směrování na webu ASP.NET Web Pages (Razor) a jak vám to umožňuje používat adresy URL, které jsou čitelnější a lepší pro SEO. Co budete...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628392"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="73813-104">Vytváření čitelných adres URL na webech ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="73813-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="73813-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="73813-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="73813-106">Tento článek popisuje směrování na webu ASP.NET Web Pages (Razor) a jak vám to umožňuje používat adresy URL, které jsou čitelnější a lepší pro SEO.</span><span class="sxs-lookup"><span data-stu-id="73813-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="73813-107">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="73813-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="73813-108">Jak ASP.NET využívá směrování, abyste mohli používat čitelnější a prohledávatelné adresy URL.</span><span class="sxs-lookup"><span data-stu-id="73813-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="73813-109">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="73813-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="73813-110">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="73813-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="73813-111">Tento kurz funguje také s ASP.NET webovými stránkami 2.</span><span class="sxs-lookup"><span data-stu-id="73813-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="73813-112">O směrování</span><span class="sxs-lookup"><span data-stu-id="73813-112">About Routing</span></span>

<span data-ttu-id="73813-113">Adresy URL stránek na webu mohou mít dopad na to, jak dobře web funguje.</span><span class="sxs-lookup"><span data-stu-id="73813-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="73813-114">Adresa URL, která je &quot;uživatelsky přívětivá&quot; může usnadnit používání webu uživateli.</span><span class="sxs-lookup"><span data-stu-id="73813-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="73813-115">Může také pomáhat s optimalizací vyhledávání na webu (SEO).</span><span class="sxs-lookup"><span data-stu-id="73813-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="73813-116">ASP.NET weby zahrnují možnost používat popisné adresy URL automaticky.</span><span class="sxs-lookup"><span data-stu-id="73813-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="73813-117">ASP.NET umožňuje vytvářet smysluplné adresy URL, které popisují akce uživatelů místo pouhého nasměrování na soubor na serveru.</span><span class="sxs-lookup"><span data-stu-id="73813-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="73813-118">Vezměte v úvahu tyto adresy URL fiktivního blogu:</span><span class="sxs-lookup"><span data-stu-id="73813-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="73813-119">Porovnejte tyto adresy URL s těmito adresami:</span><span class="sxs-lookup"><span data-stu-id="73813-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="73813-120">V první dvojici by uživatel musel mít jistotu, že se blog zobrazuje pomocí stránky *blog. cshtml* , a pak by musel sestavit řetězec dotazu, který získá správnou kategorii nebo rozsah kalendářních dat.</span><span class="sxs-lookup"><span data-stu-id="73813-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="73813-121">Druhá sada příkladů je mnohem snazší pochopit a vytvořit.</span><span class="sxs-lookup"><span data-stu-id="73813-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="73813-122">Adresy URL pro první příklad také odkazují přímo na konkrétní soubor (*blog. cshtml*).</span><span class="sxs-lookup"><span data-stu-id="73813-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="73813-123">Pokud z nějakého důvodu byl blog přesunut do jiné složky na serveru nebo pokud byl blog přepsaný na jinou stránku, odkazy by byly nesprávné.</span><span class="sxs-lookup"><span data-stu-id="73813-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="73813-124">Druhá sada adres URL neukazuje na konkrétní stránku, takže i v případě změny nebo implementace blogu budou adresy URL stále platné.</span><span class="sxs-lookup"><span data-stu-id="73813-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="73813-125">Na webových stránkách ASP.NET můžete vytvořit adresy URL příjemnější, jako jsou ty ve výše uvedených příkladech, protože ASP.NET používá *Směrování*.</span><span class="sxs-lookup"><span data-stu-id="73813-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="73813-126">Směrování vytvoří logické mapování z adresy URL na stránku (nebo stránky), která může splnit požadavek.</span><span class="sxs-lookup"><span data-stu-id="73813-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="73813-127">Vzhledem k tomu, že mapování je logické (nefyzické, pro určitý soubor), směrování poskytuje skvělou flexibilitu při definování adres URL pro váš web.</span><span class="sxs-lookup"><span data-stu-id="73813-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="73813-128">Jak funguje směrování</span><span class="sxs-lookup"><span data-stu-id="73813-128">How Routing Works</span></span>

<span data-ttu-id="73813-129">Když ASP.NET zpracuje požadavek, přečte adresu URL, která určí, jak se má směrovat.</span><span class="sxs-lookup"><span data-stu-id="73813-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="73813-130">ASP.NET se snaží porovnat jednotlivé segmenty adresy URL s soubory na disku, a to směrem zleva doprava.</span><span class="sxs-lookup"><span data-stu-id="73813-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="73813-131">Pokud se vyskytne shoda, vše zbývající na adrese URL se předává stránce jako *informace o cestě*.</span><span class="sxs-lookup"><span data-stu-id="73813-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="73813-132">Představte si, že někdo vytvoří žádost pomocí této adresy URL:</span><span class="sxs-lookup"><span data-stu-id="73813-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="73813-133">Hledání bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="73813-133">The search goes like this:</span></span>

1. <span data-ttu-id="73813-134">Existuje soubor s cestou a názvem */a/b/c.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="73813-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="73813-135">Pokud ano, spusťte tuto stránku a nepředá do ní žádné informace.</span><span class="sxs-lookup"><span data-stu-id="73813-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="73813-136">V opačném případě...</span><span class="sxs-lookup"><span data-stu-id="73813-136">Otherwise ...</span></span>
2. <span data-ttu-id="73813-137">Existuje soubor s cestou a názvem */a/b.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="73813-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="73813-138">Pokud ano, spusťte tuto stránku a předejte jí hodnotu `c`.</span><span class="sxs-lookup"><span data-stu-id="73813-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="73813-139">V opačném případě...</span><span class="sxs-lookup"><span data-stu-id="73813-139">Otherwise …</span></span>
3. <span data-ttu-id="73813-140">Existuje soubor s cestou a názvem */a.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="73813-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="73813-141">Pokud ano, spusťte tuto stránku a předejte jí hodnotu `b/c`.</span><span class="sxs-lookup"><span data-stu-id="73813-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="73813-142">Pokud hledání nenalezlo přesné shody souborů *. cshtml* v zadaných složkách, ASP.NET pokračuje v hledání těchto souborů:</span><span class="sxs-lookup"><span data-stu-id="73813-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="73813-143">*/a/b/c/default.cshtml* (žádné informace o cestě).</span><span class="sxs-lookup"><span data-stu-id="73813-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="73813-144">*/a/b/c/index.cshtml* (žádné informace o cestě).</span><span class="sxs-lookup"><span data-stu-id="73813-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="73813-145">Aby bylo jasné, požadavky na konkrétní stránky (tj. požadavky, které obsahují příponu názvu souboru *. cshtml* ) fungují stejně jako ty, které byste očekávali.</span><span class="sxs-lookup"><span data-stu-id="73813-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="73813-146">Žádost, jako je `http://www.contoso.com/a/b.cshtml`, spustí stránku *b. cshtml* pouze přesně.</span><span class="sxs-lookup"><span data-stu-id="73813-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="73813-147">V rámci stránky můžete získat informace o cestě prostřednictvím vlastnosti `UrlData` stránky, což je slovník.</span><span class="sxs-lookup"><span data-stu-id="73813-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="73813-148">Představte si, že máte soubor s názvem *ViewCustomers. cshtml* a váš web získá tuto žádost:</span><span class="sxs-lookup"><span data-stu-id="73813-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="73813-149">Jak je popsáno v předchozích pravidlech, požadavek přejde na vaši stránku.</span><span class="sxs-lookup"><span data-stu-id="73813-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="73813-150">Uvnitř stránky můžete použít kód podobný následujícímu k získání a zobrazení informací o cestě (v tomto případě hodnota &quot;1000&quot;):</span><span class="sxs-lookup"><span data-stu-id="73813-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="73813-151">Vzhledem k tomu, že směrování nezahrnuje úplné názvy souborů, může dojít k nejednoznačnosti, pokud máte stránky se stejným názvem, ale s různými příponami názvu souboru (například *MyPage. cshtml* a *MyPage. html*).</span><span class="sxs-lookup"><span data-stu-id="73813-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="73813-152">Aby se zabránilo problémům se směrováním, je vhodné zajistit, aby ve vaší lokalitě nebyly stránky, jejichž názvy se liší pouze v jejich příponách.</span><span class="sxs-lookup"><span data-stu-id="73813-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="73813-153">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="73813-153">Additional Resources</span></span>

<span data-ttu-id="73813-154">[WebMatrix – adresy URL, UrlData a směrování pro SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span><span class="sxs-lookup"><span data-stu-id="73813-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="73813-155">Tento záznam blogu pomocí Jan slaného záznamu vám poskytne další podrobnosti o tom, jak funguje směrování na webových stránkách ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="73813-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
