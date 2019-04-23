---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: Podpora možností dotazů OData v rozhraní ASP.NET Web API 2 – ASP.NET 4.x
author: MikeWasson
description: Přehled s příklady kódu zobrazuje podpůrné možnosti dotazu OData v ASP.NET Web API 2 pro ASP.NET 4.x.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 428e4942e42436585049c1e84cd7b07a4a79c0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59411563"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="0ffc0-103">Podpora možností dotazů OData v rozhraní ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="0ffc0-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="0ffc0-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0ffc0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0ffc0-105">Tento přehled s příklady kódu ukazuje podpůrné možnosti dotazu OData v ASP.NET Web API 2 technologie ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="0ffc0-106">OData definuje parametry, které lze použít k úpravě dotazu OData.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="0ffc0-107">Klient odešle tyto parametry v řetězci dotazu identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="0ffc0-108">Například pokud chcete výsledky seřadit, klient použije parametr $orderby:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="0ffc0-109">Specifikace prostředí OData volá tyto parametry *možnosti dotazu*.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="0ffc0-110">Možnosti dotazu OData pro každý kontroler rozhraní Web API můžete povolit ve vašem projektu &#8212; kontroleru nemusí být koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="0ffc0-111">To umožňuje pohodlný způsob, jak přidat funkce, jako je filtrování a řazení do libovolné aplikace webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="0ffc0-112">Před povolením možnosti dotazu, přečtěte si prosím téma [doprovodné materiály zabezpečení OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="0ffc0-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="0ffc0-113">Povolení možnosti dotazu OData</span><span class="sxs-lookup"><span data-stu-id="0ffc0-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="0ffc0-114">Příklady dotazů</span><span class="sxs-lookup"><span data-stu-id="0ffc0-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="0ffc0-115">Stránkování řízené serverem</span><span class="sxs-lookup"><span data-stu-id="0ffc0-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="0ffc0-116">Omezení možnosti dotazu</span><span class="sxs-lookup"><span data-stu-id="0ffc0-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="0ffc0-117">Přímo vyvoláním možnosti dotazu</span><span class="sxs-lookup"><span data-stu-id="0ffc0-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="0ffc0-118">Ověření dotazů</span><span class="sxs-lookup"><span data-stu-id="0ffc0-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="0ffc0-119">Povolení možnosti dotazu OData</span><span class="sxs-lookup"><span data-stu-id="0ffc0-119">Enabling OData Query Options</span></span>

<span data-ttu-id="0ffc0-120">Webové rozhraní API podporuje následující možnosti dotazu OData:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="0ffc0-121">Možnost</span><span class="sxs-lookup"><span data-stu-id="0ffc0-121">Option</span></span> | <span data-ttu-id="0ffc0-122">Popis</span><span class="sxs-lookup"><span data-stu-id="0ffc0-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ffc0-123">$expand</span><span class="sxs-lookup"><span data-stu-id="0ffc0-123">$expand</span></span> | <span data-ttu-id="0ffc0-124">Rozbalí vložené související entity.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="0ffc0-125">$filter</span><span class="sxs-lookup"><span data-stu-id="0ffc0-125">$filter</span></span> | <span data-ttu-id="0ffc0-126">Filtrování výsledků na základě logické podmínky.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="0ffc0-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="0ffc0-127">$inlinecount</span></span> | <span data-ttu-id="0ffc0-128">Informuje server zahrnout celkový počet odpovídajících entit v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="0ffc0-129">(Užitečné pro stránkování na straně serveru.)</span><span class="sxs-lookup"><span data-stu-id="0ffc0-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="0ffc0-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="0ffc0-130">$orderby</span></span> | <span data-ttu-id="0ffc0-131">Seřadí výsledky.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-131">Sorts the results.</span></span> |
| <span data-ttu-id="0ffc0-132">$select</span><span class="sxs-lookup"><span data-stu-id="0ffc0-132">$select</span></span> | <span data-ttu-id="0ffc0-133">Vybere vlastnosti, které chcete zahrnout do odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="0ffc0-134">$skip</span><span class="sxs-lookup"><span data-stu-id="0ffc0-134">$skip</span></span> | <span data-ttu-id="0ffc0-135">Přeskočí prvních n výsledků.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-135">Skips the first n results.</span></span> |
| <span data-ttu-id="0ffc0-136">$top</span><span class="sxs-lookup"><span data-stu-id="0ffc0-136">$top</span></span> | <span data-ttu-id="0ffc0-137">Vrací jenom prvních n výsledků.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="0ffc0-138">Pokud chcete použít možnosti dotazu OData, musíte je povolit explicitně.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="0ffc0-139">Můžete povolit globálně pro celou aplikaci nebo je povolit pro konkrétní řadiče nebo konkrétní akce.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="0ffc0-140">Chcete-li povolit možnosti dotazu OData globálně, zavolejte **EnableQuerySupport** na **HttpConfiguration** třída při spuštění:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="0ffc0-141">**EnableQuerySupport** metoda umožňuje využívat možnosti dotazu globálně pro všechny akce kontroleru, který vrátí **IQueryable** typu.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="0ffc0-142">Pokud nechcete, aby možnosti dotazu, které jsou povolené pro celou aplikaci, můžete povolit je pro konkrétní ovladač akcí tak, že přidáte **[Queryable]** atributu na metodu akce.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="0ffc0-143">Příklady dotazů</span><span class="sxs-lookup"><span data-stu-id="0ffc0-143">Example Queries</span></span>

<span data-ttu-id="0ffc0-144">Tato část uvádí typy dotazů, které je možné pomocí možností dotazu OData.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="0ffc0-145">Pro konkrétní podrobnosti o parametrech dotazů najdete v dokumentaci OData na [www.odata.org](http://www.odata.org/).</span><span class="sxs-lookup"><span data-stu-id="0ffc0-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="0ffc0-146">Informace o $rozbalte a $select, naleznete v tématu [pomocí $select $expand a $value v ASP.NET Web API OData](using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="0ffc0-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="0ffc0-147">**Stránkování řízené klienta**</span><span class="sxs-lookup"><span data-stu-id="0ffc0-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="0ffc0-148">Pro velká entita sady klient může chtít omezit počet výsledků.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="0ffc0-149">Klient může například zobrazovat 10 položek současně s "Další" odkazy, chcete-li získat další stránky výsledků.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="0ffc0-150">Klient použije k tomu možnosti $top a $skip.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="0ffc0-151">Možnost $top poskytuje maximální počet vrácených položek a možnost $skip poskytuje počet položek pro přeskočení.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="0ffc0-152">Předchozí příklad načte položky 21 až 30.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="0ffc0-153">**Filtrování**</span><span class="sxs-lookup"><span data-stu-id="0ffc0-153">**Filtering**</span></span>

<span data-ttu-id="0ffc0-154">Možnost $filter umožňuje klientovi filtrování výsledků s použitím logického výrazu.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="0ffc0-155">Filtr výrazy jsou velmi výkonné; patří mezi ně aritmetické a logické operátory, řetězce funkce a funkce data.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="0ffc0-156">Vrátí všechny produkty s kategorií rovno "Toys".</span><span class="sxs-lookup"><span data-stu-id="0ffc0-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="0ffc0-157">`http://localhost/Products?$filter=Category` EQ 'Toys.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="0ffc0-158">Vrátí všechny produkty s cenou menší než 10.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="0ffc0-159">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="0ffc0-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="0ffc0-160">Logické operátory: Vrátit všechny produkty, kde cena > = 5 a cena < = 15.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="0ffc0-161">`http://localhost/Products?$filter=Price` ge 5 a cena le 15</span><span class="sxs-lookup"><span data-stu-id="0ffc0-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="0ffc0-162">Řetězcové funkce: Vrátí všechny produkty s "zz" v názvu.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="0ffc0-163">Datové funkce: Vrátí všechny produkty s ReleaseDate po 2005.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="0ffc0-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span><span class="sxs-lookup"><span data-stu-id="0ffc0-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="0ffc0-165">**Řazení**</span><span class="sxs-lookup"><span data-stu-id="0ffc0-165">**Sorting**</span></span>

<span data-ttu-id="0ffc0-166">Chcete-li seřadit výsledky, použijte filtr $orderby.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="0ffc0-167">Seřadit podle cena.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="0ffc0-168">Seřadit podle: cena v sestupném pořadí (nejvyšší k nejnižší).</span><span class="sxs-lookup"><span data-stu-id="0ffc0-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="0ffc0-169">Seřadit podle kategorie a pak řazení podle ceny v sestupném pořadí v rámci kategorie.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="0ffc0-170">Stránkování řízené serverem</span><span class="sxs-lookup"><span data-stu-id="0ffc0-170">Server-Driven Paging</span></span>

<span data-ttu-id="0ffc0-171">Pokud databáze obsahuje milióny záznamů, které nechcete posílat je všechny v jedné datové části.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="0ffc0-172">Chcete-li tomu zabránit, serveru můžete omezit počet položek, které odešle v jedné odezvě.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="0ffc0-173">Chcete-li povolit stránkování na straně serveru, nastavte **PageSize** vlastnost **Queryable** atribut.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="0ffc0-174">Hodnota je maximální počet vrácených položek.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="0ffc0-175">Pokud váš kontroler vrací formátu OData, text odpovědi bude obsahovat odkaz na další stránku dat:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="0ffc0-176">Klienta můžete použít tento odkaz k načtení další stránky.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="0ffc0-177">Informace o tom celkový počet položek v sadě výsledků, můžete klienta nastavit možnost dotazu $inlinecount s hodnotou "allpages".</span><span class="sxs-lookup"><span data-stu-id="0ffc0-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="0ffc0-178">Hodnota "allpages" informuje server zahrnout celkový počet v odpovědi:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="0ffc0-179">Odkazy na další stránky i vložený počet, který vyžadují formátu OData.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="0ffc0-180">Důvodem je, že OData definuje zvláštní pole v těle odpovědi pro uložení odkazu a počet.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>


<span data-ttu-id="0ffc0-181">Protokolu OData formátů, je stále možné podporovat další stránky odkazy a vložený počet, obalením výsledky dotazu v **PageResult&lt;T&gt;**  objektu.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="0ffc0-182">To ale vyžaduje trochu další kód.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-182">However, it requires a bit more code.</span></span> <span data-ttu-id="0ffc0-183">Tady je příklad:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="0ffc0-184">Tady je příklad odpověď JSON:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="0ffc0-185">Omezení možnosti dotazu</span><span class="sxs-lookup"><span data-stu-id="0ffc0-185">Limiting the Query Options</span></span>

<span data-ttu-id="0ffc0-186">Možnosti dotazu dát klientům spoustu kontrolu nad dotaz, který běží na serveru.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="0ffc0-187">V některých případech můžete chtít omezit dostupné možnosti z důvodů zabezpečení nebo výkon.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="0ffc0-188">**[Queryable]** atribut má některé integrované vlastnosti pro toto.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="0ffc0-189">Zde je několik příkladů:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-189">Here are some examples.</span></span>

<span data-ttu-id="0ffc0-190">Povolit pouze $skip a $top, pro podporu stránkování a nic jiného:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="0ffc0-191">Povolit řazení jenom podle určité vlastnosti, aby se zabránilo řazení na vlastnosti, které nejsou indexovány v databázi:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="0ffc0-192">Povolit funkci logické "eq", ale žádné logické funkce:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="0ffc0-193">Nejsou povoleny všechny aritmetické operátory:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="0ffc0-194">Můžete omezit možnosti globálně tak, že vytváří **položce QueryableAttribute** instance a předá se **EnableQuerySupport** funkce:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="0ffc0-195">Přímo vyvoláním možnosti dotazu</span><span class="sxs-lookup"><span data-stu-id="0ffc0-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="0ffc0-196">Namísto použití **[Queryable]** atribut, možnosti dotazu můžete vyvolat přímo ve vašem řadiči.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="0ffc0-197">Chcete-li to provést, přidejte **ODataQueryOptions** parametru k metodě kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="0ffc0-198">V takovém případě nepotřebujete **[Queryable]** atribut.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="0ffc0-199">Naplní webového rozhraní API **ODataQueryOptions** řetězec dotazu z identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="0ffc0-200">Použije dotaz, předejte **IQueryable** k **volat metodu** metoda.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="0ffc0-201">Metoda vrátí jiný **IQueryable**.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="0ffc0-202">Pro pokročilé scénáře, pokud nemáte **IQueryable** poskytovatele dotazů, můžete zkontrolovat **ODataQueryOptions** a překládat možnosti dotazu do jiného formátu.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="0ffc0-203">(Například najdete v příspěvku blogu RaghuRam Nadiminti [dotazů překladu OData na HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), kde najdete také [ukázka](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span><span class="sxs-lookup"><span data-stu-id="0ffc0-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="0ffc0-204">Ověření dotazů</span><span class="sxs-lookup"><span data-stu-id="0ffc0-204">Query Validation</span></span>

<span data-ttu-id="0ffc0-205">**[Queryable]** atribut ověří dotaz před jeho provedením.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="0ffc0-206">Krok ověření se provádí v **QueryableAttribute.ValidateQuery** metody.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="0ffc0-207">Můžete také přizpůsobit proces ověření.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-207">You can also customize the validation process.</span></span>

<span data-ttu-id="0ffc0-208">Viz také [doprovodné materiály zabezpečení OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="0ffc0-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="0ffc0-209">Nejprve přepsání jeden validátoru tříd, který je definovaný v **Web.Http.OData.Query.Validators** oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="0ffc0-210">Například následující třídu validátora zakáže možnost "desc" pro možnost $orderby.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="0ffc0-211">Podtřídy **[Queryable]** atribut přepsání **ValidateQuery** metody.</span><span class="sxs-lookup"><span data-stu-id="0ffc0-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="0ffc0-212">Potom nastavte vlastní atribut buď globálně nebo na řadič:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="0ffc0-213">Pokud používáte **ODataQueryOptions** přímo, nastavte ověřovací modul na možnostech:</span><span class="sxs-lookup"><span data-stu-id="0ffc0-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
