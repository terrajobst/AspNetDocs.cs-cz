---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Doprovodné materiály zabezpečení pro ASP.NET Web API 2 OData – ASP.NET 4.x
author: MikeWasson
description: Popisuje problémy se zabezpečením vzít v úvahu při zpřístupňování datovou sadu prostřednictvím prostředí OData pro ASP.NET Web API 2 technologie ASP.NET 4.x.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393506"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="cd82f-103">Doprovodné materiály zabezpečení pro ASP.NET Web API 2 OData</span><span class="sxs-lookup"><span data-stu-id="cd82f-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="cd82f-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cd82f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="cd82f-105">Toto téma popisuje některé problémy se zabezpečením, které byste měli zvážit při zpřístupňování datovou sadu prostřednictvím prostředí OData pro ASP.NET Web API 2 technologie ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="cd82f-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="cd82f-106">Zabezpečení EDM</span><span class="sxs-lookup"><span data-stu-id="cd82f-106">EDM Security</span></span>

<span data-ttu-id="cd82f-107">Sémantiku dotazů jsou založeny na entity data model (EDM), nikoli základní typy modelů.</span><span class="sxs-lookup"><span data-stu-id="cd82f-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="cd82f-108">Může být z modelu EDM vyloučena určitá vlastnost a nebude viditelná pro dotaz.</span><span class="sxs-lookup"><span data-stu-id="cd82f-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="cd82f-109">Předpokládejme například, že váš model obsahuje typ zaměstnance s vlastností Salary.</span><span class="sxs-lookup"><span data-stu-id="cd82f-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="cd82f-110">Můžete chtít vyloučit tuto vlastnost z modelu EDM skrýt od klientů.</span><span class="sxs-lookup"><span data-stu-id="cd82f-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="cd82f-111">Existují dva způsoby, jak být vyloučena určitá vlastnost z modelu EDM.</span><span class="sxs-lookup"><span data-stu-id="cd82f-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="cd82f-112">Můžete nastavit **[IgnoreDataMember]** atribut na vlastnost ve třídě modelu:</span><span class="sxs-lookup"><span data-stu-id="cd82f-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="cd82f-113">Můžete také odebrat vlastnost z modelu EDM prostřednictvím kódu programu:</span><span class="sxs-lookup"><span data-stu-id="cd82f-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="cd82f-114">Zabezpečení dotazu</span><span class="sxs-lookup"><span data-stu-id="cd82f-114">Query Security</span></span>

<span data-ttu-id="cd82f-115">Škodlivý nebo naivní klienta může být schopen vytvořit dotaz, který trvá velmi dlouho ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="cd82f-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="cd82f-116">V nejhorším případě může to narušit přístup k službě.</span><span class="sxs-lookup"><span data-stu-id="cd82f-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="cd82f-117">**[Queryable]** je atribut filtru akce, které analyzuje, ověří a použije dotaz.</span><span class="sxs-lookup"><span data-stu-id="cd82f-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="cd82f-118">Filtr převede možnosti dotazu výrazu LINQ.</span><span class="sxs-lookup"><span data-stu-id="cd82f-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="cd82f-119">Při vrácení kontroler OData **IQueryable** typ, **IQueryable** zprostředkovatele LINQ Převede výraz LINQ dotaz.</span><span class="sxs-lookup"><span data-stu-id="cd82f-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="cd82f-120">Výkon proto závisí na zprostředkovatele LINQ, který se používá a také na konkrétní charakteristiky schéma datové sady nebo databáze.</span><span class="sxs-lookup"><span data-stu-id="cd82f-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="cd82f-121">Další informace o použití možnosti dotazu OData v rozhraní ASP.NET Web API najdete v tématu [podporuje možnosti dotazu OData](supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="cd82f-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="cd82f-122">Pokud víte, že všichni klienti jsou důvěryhodné (například v podnikovém prostředí), nebo pokud vaše datová sada je malá, výkon dotazů, nemusí být problém.</span><span class="sxs-lookup"><span data-stu-id="cd82f-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="cd82f-123">V opačném případě byste měli zvážit následující doporučení.</span><span class="sxs-lookup"><span data-stu-id="cd82f-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="cd82f-124">Testování služby s různé dotazy a Profilovat databáze.</span><span class="sxs-lookup"><span data-stu-id="cd82f-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="cd82f-125">Povolte stránkování řízených serverem, aby se zabránilo vrácení velké sady dat v jednom dotazu.</span><span class="sxs-lookup"><span data-stu-id="cd82f-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="cd82f-126">Další informace najdete v tématu [stránkování Server-Driven](supporting-odata-query-options.md#server-paging).</span><span class="sxs-lookup"><span data-stu-id="cd82f-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="cd82f-127">Je třeba $filter a $orderby?</span><span class="sxs-lookup"><span data-stu-id="cd82f-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="cd82f-128">Některé aplikace může dovolit klientským stránkování, $top a $skip, ale zakázat další možnosti dotazu.</span><span class="sxs-lookup"><span data-stu-id="cd82f-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="cd82f-129">Zvažte omezení $orderby na vlastnosti v clusterovaném indexu.</span><span class="sxs-lookup"><span data-stu-id="cd82f-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="cd82f-130">Řazení velkých dat bez clusterovaného indexu je pomalé.</span><span class="sxs-lookup"><span data-stu-id="cd82f-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="cd82f-131">Maximální počet uzlů: **MaxNodeCount** vlastnost **[Queryable]** Nastaví maximální počtu uzlů, které jsou povoleny ve stromu syntaxe $filter.</span><span class="sxs-lookup"><span data-stu-id="cd82f-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="cd82f-132">Výchozí hodnota je 100, ale můžete chtít nastavit nižší hodnotu, protože velký počet uzlů, může trvat dlouho. kompilace.</span><span class="sxs-lookup"><span data-stu-id="cd82f-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="cd82f-133">To platí zejména pokud používáte LINQ to Objects (například LINQ dotazy na kolekce v paměti, ale bez použití zprostředkující zprostředkovatele LINQ).</span><span class="sxs-lookup"><span data-stu-id="cd82f-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="cd82f-134">Zvažte zakázání funkce metoda any() a all(), protože to může být pomalé.</span><span class="sxs-lookup"><span data-stu-id="cd82f-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="cd82f-135">Pokud jakékoli vlastnosti řetězce obsahují dlouhých řetězců&#8212;například popis produktu nebo blogu&#8212;zvažte zakázání funkce řetězec.</span><span class="sxs-lookup"><span data-stu-id="cd82f-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="cd82f-136">Zvažte zákaz filtrování na navigační vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="cd82f-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="cd82f-137">Filtrování na navigační vlastnosti může mít za následek spojení, což může být pomalé, v závislosti na schématu databáze.</span><span class="sxs-lookup"><span data-stu-id="cd82f-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="cd82f-138">Následující kód ukazuje validátor dotazu, který zabraňuje filtrování na navigační vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="cd82f-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="cd82f-139">Další informace o dotazu validátory najdete v tématu [dotaz ověření](supporting-odata-query-options.md#query-validation).</span><span class="sxs-lookup"><span data-stu-id="cd82f-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="cd82f-140">Zvažte omezení $filter dotazy napsáním validátor, který je přizpůsobený pro vaši databázi.</span><span class="sxs-lookup"><span data-stu-id="cd82f-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="cd82f-141">Představte si třeba tyto dva dotazy:</span><span class="sxs-lookup"><span data-stu-id="cd82f-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="cd82f-142">Všechna videa pomocí objektů actor, jejichž příjmení začíná "A".</span><span class="sxs-lookup"><span data-stu-id="cd82f-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="cd82f-143">Všechny filmy vydána v roce 1994.</span><span class="sxs-lookup"><span data-stu-id="cd82f-143">All movies released in 1994.</span></span>

    <span data-ttu-id="cd82f-144">Pokud filmy jsou indexovány pomocí objektů actor, první dotaz může vyžadovat databázový stroj kontrolovat celý seznam videa.</span><span class="sxs-lookup"><span data-stu-id="cd82f-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="cd82f-145">Zatímco druhý dotaz může být přijatelný, předpokládá filmy jsou indexovány pomocí rok vydání.</span><span class="sxs-lookup"><span data-stu-id="cd82f-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="cd82f-146">Následující kód ukazuje validátor umožňuje filtrování podle vlastnosti "ReleaseYear" a "Title", ale žádné jiné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="cd82f-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="cd82f-147">Obecně platí zvažte možnost $filter funkcích, které potřebujete.</span><span class="sxs-lookup"><span data-stu-id="cd82f-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="cd82f-148">Pokud vaši klienti nepotřebují úplné expresivity $filter, můžete omezit povolené funkce.</span><span class="sxs-lookup"><span data-stu-id="cd82f-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
