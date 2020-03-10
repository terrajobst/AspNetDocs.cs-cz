---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: Vztahy mezi entitami v OData v4 pomocí webového rozhraní API ASP.NET 2,2 | Microsoft Docs
author: MikeWasson
description: 'Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele. Pomocí OData můžou klienti přejít přes...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598691"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="f2155-104">Vztahy mezi entitami v OData v4 pomocí webového rozhraní API ASP.NET 2,2</span><span class="sxs-lookup"><span data-stu-id="f2155-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="f2155-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f2155-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="f2155-106">Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele.</span><span class="sxs-lookup"><span data-stu-id="f2155-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="f2155-107">Pomocí OData můžou klienti přejít na vztahy mezi entitami.</span><span class="sxs-lookup"><span data-stu-id="f2155-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="f2155-108">Pro daný produkt můžete najít dodavatele.</span><span class="sxs-lookup"><span data-stu-id="f2155-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="f2155-109">Můžete také vytvořit nebo odebrat relace.</span><span class="sxs-lookup"><span data-stu-id="f2155-109">You can also create or remove relationships.</span></span> <span data-ttu-id="f2155-110">Můžete například nastavit dodavatele produktu.</span><span class="sxs-lookup"><span data-stu-id="f2155-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="f2155-111">V tomto kurzu se dozvíte, jak podporovat tyto operace v OData v4 pomocí webového rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f2155-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="f2155-112">Kurz sestaví v kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f2155-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f2155-113">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="f2155-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="f2155-114">Webové rozhraní API 2,1</span><span class="sxs-lookup"><span data-stu-id="f2155-114">Web API 2.1</span></span>
> - <span data-ttu-id="f2155-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="f2155-115">OData v4</span></span>
> - <span data-ttu-id="f2155-116">Visual Studio 2013 (Stáhněte si Visual Studio 2017 [tady](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="f2155-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="f2155-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="f2155-117">Entity Framework 6</span></span>
> - <span data-ttu-id="f2155-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f2155-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="f2155-119">Verze kurzů</span><span class="sxs-lookup"><span data-stu-id="f2155-119">Tutorial versions</span></span>
>
> <span data-ttu-id="f2155-120">Informace o OData verze 3 najdete v tématu [Podpora vztahů mezi entitami v OData V3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span><span class="sxs-lookup"><span data-stu-id="f2155-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="f2155-121">Přidat entitu dodavatele</span><span class="sxs-lookup"><span data-stu-id="f2155-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="f2155-122">Kurz sestaví v kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f2155-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="f2155-123">Nejdřív potřebujeme související entitu.</span><span class="sxs-lookup"><span data-stu-id="f2155-123">First, we need a related entity.</span></span> <span data-ttu-id="f2155-124">Do složky modely přidejte třídu s názvem `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="f2155-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="f2155-125">Přidejte vlastnost navigace do `Product` třídy:</span><span class="sxs-lookup"><span data-stu-id="f2155-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="f2155-126">Přidejte do `ProductsContext` třídy novou **negenerickými** , aby Entity Framework zahrnovala tabulku dodavatelů v databázi.</span><span class="sxs-lookup"><span data-stu-id="f2155-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="f2155-127">V WebApiConfig.cs přidejte sadu entit&quot; &quot;dodavatelé k modelu Entity Data Model:</span><span class="sxs-lookup"><span data-stu-id="f2155-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="f2155-128">Přidat řadič dodavatelů</span><span class="sxs-lookup"><span data-stu-id="f2155-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="f2155-129">Přidejte třídu `SuppliersController` do složky Controllers.</span><span class="sxs-lookup"><span data-stu-id="f2155-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="f2155-130">Neukazuje, jak přidat operace CRUD pro tento kontroler.</span><span class="sxs-lookup"><span data-stu-id="f2155-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="f2155-131">Postup je stejný jako u kontroleru produktů (viz [Vytvoření koncového bodu OData v4](create-an-odata-v4-endpoint.md)).</span><span class="sxs-lookup"><span data-stu-id="f2155-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="f2155-132">Získávání souvisejících entit</span><span class="sxs-lookup"><span data-stu-id="f2155-132">Getting Related Entities</span></span>

<span data-ttu-id="f2155-133">Pokud chcete získat dodavatele pro určitý produkt, klient odešle požadavek GET:</span><span class="sxs-lookup"><span data-stu-id="f2155-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="f2155-134">Pro podporu tohoto požadavku přidejte následující metodu do třídy `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="f2155-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="f2155-135">Tato metoda používá výchozí konvenci pojmenování.</span><span class="sxs-lookup"><span data-stu-id="f2155-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="f2155-136">Název metody: GetX, kde X je navigační vlastnost.</span><span class="sxs-lookup"><span data-stu-id="f2155-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="f2155-137">Název parametru: *klíč*</span><span class="sxs-lookup"><span data-stu-id="f2155-137">Parameter name: *key*</span></span>

<span data-ttu-id="f2155-138">Pokud budete postupovat podle těchto zásad vytváření názvů, webové rozhraní API automaticky mapuje požadavek HTTP na metodu kontroleru.</span><span class="sxs-lookup"><span data-stu-id="f2155-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="f2155-139">Příklad požadavku HTTP:</span><span class="sxs-lookup"><span data-stu-id="f2155-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="f2155-140">Příklad odpovědi HTTP:</span><span class="sxs-lookup"><span data-stu-id="f2155-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="f2155-141">Získání související kolekce</span><span class="sxs-lookup"><span data-stu-id="f2155-141">Getting a related collection</span></span>

<span data-ttu-id="f2155-142">V předchozím příkladu má produkt jednoho dodavatele.</span><span class="sxs-lookup"><span data-stu-id="f2155-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="f2155-143">Navigační vlastnost může také vracet kolekci.</span><span class="sxs-lookup"><span data-stu-id="f2155-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="f2155-144">Následující kód získá produkty pro dodavatele:</span><span class="sxs-lookup"><span data-stu-id="f2155-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="f2155-145">V tomto případě metoda vrátí **IQueryable** místo **SingleResult&lt;t&gt;**</span><span class="sxs-lookup"><span data-stu-id="f2155-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="f2155-146">Příklad požadavku HTTP:</span><span class="sxs-lookup"><span data-stu-id="f2155-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="f2155-147">Příklad odpovědi HTTP:</span><span class="sxs-lookup"><span data-stu-id="f2155-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="f2155-148">Vytvoření relace mezi entitami</span><span class="sxs-lookup"><span data-stu-id="f2155-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="f2155-149">OData podporuje vytváření nebo odebírání vztahů mezi dvěma stávajícími entitami.</span><span class="sxs-lookup"><span data-stu-id="f2155-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="f2155-150">V terminologii OData v4 je vztah &quot;odkazem&quot;.</span><span class="sxs-lookup"><span data-stu-id="f2155-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="f2155-151">(V OData V3 se vztah nazýval *propojení*.</span><span class="sxs-lookup"><span data-stu-id="f2155-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="f2155-152">Rozdíly v protokolu nejsou pro tento kurz důležité.)</span><span class="sxs-lookup"><span data-stu-id="f2155-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="f2155-153">Odkaz má svůj vlastní identifikátor URI s `/Entity/NavigationProperty/$ref`formuláře.</span><span class="sxs-lookup"><span data-stu-id="f2155-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="f2155-154">Tady je například identifikátor URI, který řeší odkaz mezi produktem a jeho dodavatelem:</span><span class="sxs-lookup"><span data-stu-id="f2155-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="f2155-155">Chcete-li přidat relaci, klient pošle požadavek POST nebo PUT na tuto adresu.</span><span class="sxs-lookup"><span data-stu-id="f2155-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="f2155-156">Vloží, pokud je navigační vlastnost jediná entita, například `Product.Supplier`.</span><span class="sxs-lookup"><span data-stu-id="f2155-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="f2155-157">PŘÍSPĚVEK, pokud je navigační vlastnost kolekce, například `Supplier.Products`.</span><span class="sxs-lookup"><span data-stu-id="f2155-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="f2155-158">Tělo požadavku obsahuje identifikátor URI druhé entity ve vztahu.</span><span class="sxs-lookup"><span data-stu-id="f2155-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="f2155-159">Tady je příklad žádosti:</span><span class="sxs-lookup"><span data-stu-id="f2155-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="f2155-160">V tomto příkladu klient odešle požadavek PUT do `/Products(6)/Supplier/$ref`, což je $ref URI pro `Supplier` produktu s ID = 6.</span><span class="sxs-lookup"><span data-stu-id="f2155-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="f2155-161">Pokud je požadavek úspěšný, odešle Server odpověď 204 (bez obsahu):</span><span class="sxs-lookup"><span data-stu-id="f2155-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="f2155-162">Zde je metoda kontroleru pro přidání vztahu k `Product`:</span><span class="sxs-lookup"><span data-stu-id="f2155-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="f2155-163">Parametr *navigationProperty* určuje, který vztah má být nastaven.</span><span class="sxs-lookup"><span data-stu-id="f2155-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="f2155-164">(Pokud je v entitě více než jedna vlastnost navigace, můžete přidat další příkazy `case`.)</span><span class="sxs-lookup"><span data-stu-id="f2155-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="f2155-165">Parametr *propojení* obsahuje identifikátor URI dodavatele.</span><span class="sxs-lookup"><span data-stu-id="f2155-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="f2155-166">Webové rozhraní API automaticky analyzuje tělo žádosti a získá hodnotu pro tento parametr.</span><span class="sxs-lookup"><span data-stu-id="f2155-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="f2155-167">K vyhledání dodavatele potřebujeme ID (nebo klíč), které je součástí parametru *propojení* .</span><span class="sxs-lookup"><span data-stu-id="f2155-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="f2155-168">K tomu použijte následující pomocnou metodu:</span><span class="sxs-lookup"><span data-stu-id="f2155-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="f2155-169">V podstatě Tato metoda používá knihovnu OData k rozdělení cesty identifikátoru URI na segmenty, vyhledá segment, který obsahuje klíč, a převede klíč na správný typ.</span><span class="sxs-lookup"><span data-stu-id="f2155-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="f2155-170">Odstranění relace mezi entitami</span><span class="sxs-lookup"><span data-stu-id="f2155-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="f2155-171">Pokud chcete odstranit relaci, klient pošle požadavek HTTP DELETE na $ref URI:</span><span class="sxs-lookup"><span data-stu-id="f2155-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="f2155-172">Tady je metoda kontroleru pro odstranění vztahu mezi produktem a dodavatelem:</span><span class="sxs-lookup"><span data-stu-id="f2155-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="f2155-173">V takovém případě je `Product.Supplier` &quot;1&quot; konec relace 1: n, takže můžete relaci odebrat pouze nastavením `Product.Supplier` na `null`.</span><span class="sxs-lookup"><span data-stu-id="f2155-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="f2155-174">V &quot;mnoho&quot; konci relace musí klient určit, kterou související entitu chcete odebrat.</span><span class="sxs-lookup"><span data-stu-id="f2155-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="f2155-175">K tomu klient pošle identifikátor URI související entity v řetězci dotazu žádosti.</span><span class="sxs-lookup"><span data-stu-id="f2155-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="f2155-176">Pokud například chcete odebrat "produkt 1" z "dodavatel 1":</span><span class="sxs-lookup"><span data-stu-id="f2155-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="f2155-177">Pro podporu tohoto webového rozhraní API musíme do metody `DeleteRef` zahrnout další parametr.</span><span class="sxs-lookup"><span data-stu-id="f2155-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="f2155-178">Tady je metoda kontroleru pro odebrání produktu z relace `Supplier.Products`.</span><span class="sxs-lookup"><span data-stu-id="f2155-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="f2155-179">Parametr *Key* je klíč pro dodavatele a parametr *relatedKey* je klíč, který produkt odebere ze vztahu `Products`.</span><span class="sxs-lookup"><span data-stu-id="f2155-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="f2155-180">Všimněte si, že webové rozhraní API automaticky získá klíč z řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="f2155-180">Note that Web API automatically gets the key from the query string.</span></span>
