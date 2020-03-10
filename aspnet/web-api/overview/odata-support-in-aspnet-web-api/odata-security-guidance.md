---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Bezpečnostní pokyny pro ASP.NET Web API 2 OData-ASP.NET 4. x
author: MikeWasson
description: Popisuje bezpečnostní problémy, které je potřeba vzít v úvahu při vystavení datové sady prostřednictvím OData pro webové rozhraní API 2 pro ASP.NET ve ASP.NET 4. x.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556495"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="bd87d-103">Pokyny k zabezpečení ASP.NET webového rozhraní API 2 OData</span><span class="sxs-lookup"><span data-stu-id="bd87d-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="bd87d-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bd87d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bd87d-105">Toto téma popisuje některé problémy se zabezpečením, které byste měli zvážit při vystavení datové sady prostřednictvím OData pro webové rozhraní API 2 pro ASP.NET ve ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="bd87d-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="bd87d-106">Zabezpečení EDM</span><span class="sxs-lookup"><span data-stu-id="bd87d-106">EDM Security</span></span>

<span data-ttu-id="bd87d-107">Sémantika dotazu je založena na modelu Entity Data Model (EDM), nikoli na podkladových typech modelů.</span><span class="sxs-lookup"><span data-stu-id="bd87d-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="bd87d-108">Z datového modelu EDM můžete vyloučit vlastnost, která nebude viditelná pro dotaz.</span><span class="sxs-lookup"><span data-stu-id="bd87d-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="bd87d-109">Předpokládejme například, že váš model zahrnuje typ zaměstnance s vlastností mzdy.</span><span class="sxs-lookup"><span data-stu-id="bd87d-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="bd87d-110">Tuto vlastnost můžete chtít vyloučit z modelu EDM, aby bylo možné ji skrýt od klientů.</span><span class="sxs-lookup"><span data-stu-id="bd87d-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="bd87d-111">Existují dva způsoby, jak vyloučit vlastnost z modelu EDM.</span><span class="sxs-lookup"><span data-stu-id="bd87d-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="bd87d-112">Můžete nastavit atribut **[IgnoreDataMember]** u vlastnosti v třídě modelu:</span><span class="sxs-lookup"><span data-stu-id="bd87d-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="bd87d-113">Můžete také odebrat vlastnost z modelu EDM programově:</span><span class="sxs-lookup"><span data-stu-id="bd87d-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="bd87d-114">Zabezpečení dotazů</span><span class="sxs-lookup"><span data-stu-id="bd87d-114">Query Security</span></span>

<span data-ttu-id="bd87d-115">Zlomyslný nebo Naive klient může vytvořit dotaz, který trvá příliš dlouho, než se spustí.</span><span class="sxs-lookup"><span data-stu-id="bd87d-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="bd87d-116">V nejhorším případě to může mít za následek nerušený přístup k vaší službě.</span><span class="sxs-lookup"><span data-stu-id="bd87d-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="bd87d-117">Atribut **[Queryable]** je filtr akcí, který analyzuje, ověřuje a aplikuje dotaz.</span><span class="sxs-lookup"><span data-stu-id="bd87d-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="bd87d-118">Filtr převede možnosti dotazu na výraz LINQ.</span><span class="sxs-lookup"><span data-stu-id="bd87d-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="bd87d-119">Když řadič OData vrátí typ **IQueryable** , poskytovatel **IQueryable** LINQ Převede výraz LINQ na dotaz.</span><span class="sxs-lookup"><span data-stu-id="bd87d-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="bd87d-120">Proto výkon závisí na poskytovateli LINQ, který se používá, a také na konkrétní vlastnosti datové sady nebo schématu databáze.</span><span class="sxs-lookup"><span data-stu-id="bd87d-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="bd87d-121">Další informace o použití možností dotazů OData ve webovém rozhraní API ASP.NET najdete v tématu [Podpora možností dotazů OData](supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="bd87d-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="bd87d-122">Pokud víte, že všichni klienti jsou důvěryhodní (například v podnikovém prostředí), nebo pokud je vaše datová sada malá, nemusí se jednat o problém s výkonem dotazů.</span><span class="sxs-lookup"><span data-stu-id="bd87d-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="bd87d-123">V opačném případě byste měli zvážit následující doporučení.</span><span class="sxs-lookup"><span data-stu-id="bd87d-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="bd87d-124">Otestujte službu pomocí různých dotazů a profilujte databázi.</span><span class="sxs-lookup"><span data-stu-id="bd87d-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="bd87d-125">Povolte stránkování řízené serverem, aby nedošlo k vrácení velkých datových sad v jednom dotazu.</span><span class="sxs-lookup"><span data-stu-id="bd87d-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="bd87d-126">Další informace najdete v tématu [stránkování řízené serverem](supporting-odata-query-options.md#server-paging).</span><span class="sxs-lookup"><span data-stu-id="bd87d-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="bd87d-127">Potřebujete $filter a $orderby?</span><span class="sxs-lookup"><span data-stu-id="bd87d-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="bd87d-128">Některé aplikace mohou umožňovat stránkování klienta pomocí $top a $skip, ale zakazují další možnosti dotazu.</span><span class="sxs-lookup"><span data-stu-id="bd87d-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="bd87d-129">Zvažte omezení $orderby na vlastnosti v clusterovaných indexech.</span><span class="sxs-lookup"><span data-stu-id="bd87d-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="bd87d-130">Řazení velkých objemů dat bez clusterovaných indexů je pomalé.</span><span class="sxs-lookup"><span data-stu-id="bd87d-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="bd87d-131">Maximální počet uzlů: vlastnost **MaxNodeCount** v **[Queryable]** nastaví maximální počet uzlů povolených ve stromu syntaxe $Filter.</span><span class="sxs-lookup"><span data-stu-id="bd87d-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="bd87d-132">Výchozí hodnota je 100, ale možná budete chtít nastavit nižší hodnotu, protože velký počet uzlů může být pro zkompilování pomalé.</span><span class="sxs-lookup"><span data-stu-id="bd87d-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="bd87d-133">To platí zejména v případě, že používáte LINQ to Objects (tj. dotazy LINQ na kolekci v paměti, bez použití zprostředkujícího poskytovatele LINQ).</span><span class="sxs-lookup"><span data-stu-id="bd87d-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="bd87d-134">Zvažte zakázání funkcí any () a All (), protože tyto funkce mohou být pomalé.</span><span class="sxs-lookup"><span data-stu-id="bd87d-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="bd87d-135">Pokud některé vlastnosti řetězce obsahují velké řetězce&#8212;, například popis produktu nebo záznam&#8212;blogu, zvažte zakázání funkcí řetězce.</span><span class="sxs-lookup"><span data-stu-id="bd87d-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="bd87d-136">Zvažte možnost zakázat filtrování u vlastností navigace.</span><span class="sxs-lookup"><span data-stu-id="bd87d-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="bd87d-137">Filtrování vlastností navigace může mít za následek spojení, což může být pomalé v závislosti na schématu databáze.</span><span class="sxs-lookup"><span data-stu-id="bd87d-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="bd87d-138">Následující kód ukazuje validátor dotazů, který brání filtrování vlastností navigace.</span><span class="sxs-lookup"><span data-stu-id="bd87d-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="bd87d-139">Další informace o validátorech dotazů naleznete v tématu [ověření dotazu](supporting-odata-query-options.md#query-validation).</span><span class="sxs-lookup"><span data-stu-id="bd87d-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="bd87d-140">Zvažte omezení $filterch dotazů zápisem ověřovacího modulu, který je přizpůsoben pro vaši databázi.</span><span class="sxs-lookup"><span data-stu-id="bd87d-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="bd87d-141">Zvažte například tyto dva dotazy:</span><span class="sxs-lookup"><span data-stu-id="bd87d-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="bd87d-142">Všechny filmy s objekty actor, jejichž příjmení začíná znakem A.</span><span class="sxs-lookup"><span data-stu-id="bd87d-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="bd87d-143">Všechny filmy vydané v 1994.</span><span class="sxs-lookup"><span data-stu-id="bd87d-143">All movies released in 1994.</span></span>

    <span data-ttu-id="bd87d-144">V případě, že filmy nejsou indexovány aktéry, může první dotaz vyžadovat, aby databázový stroj prohledal celý seznam filmů.</span><span class="sxs-lookup"><span data-stu-id="bd87d-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="bd87d-145">Vzhledem k tomu, že druhý dotaz může být přijatelný, předpokládá se, že filmy jsou indexovány v roce vydání.</span><span class="sxs-lookup"><span data-stu-id="bd87d-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="bd87d-146">Následující kód ukazuje validátor, který umožňuje filtrování vlastností "ReleaseYear" a "title", ale žádné další vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="bd87d-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="bd87d-147">Obecně zvažte, které $filter funkce potřebujete.</span><span class="sxs-lookup"><span data-stu-id="bd87d-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="bd87d-148">Pokud klienti nepotřebují úplné expresivity $filter, můžete povolené funkce omezit.</span><span class="sxs-lookup"><span data-stu-id="bd87d-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
