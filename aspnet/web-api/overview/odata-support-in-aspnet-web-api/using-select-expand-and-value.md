---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: Pomocí $select $expand a $value v ASP.NET Web API 2 OData – ASP.NET 4.x
author: MikeWasson
description: Přehled a ukázky kódu $ rozbalit, $select, a $value možnosti v OData Web API 2 ASP.NET 4.x.
ms.author: riande
ms.date: 10/11/2013
ms.custom: seoapril2019
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: 8b5d3e87c679a31f1908aa648219ae5c6b701a1f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400695"
---
# <a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="9ec14-103">Pomocí $select $expand a $value v ASP.NET Web API 2 OData</span><span class="sxs-lookup"><span data-stu-id="9ec14-103">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="9ec14-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9ec14-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9ec14-105">Přehled a ukázky kódu $ rozbalit, $select, a $value možnosti v OData Web API 2 ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="9ec14-105">Overview and code samples for the $expand, $select, and $value options in OData Web API 2 for ASP.NET 4.x.</span></span> <span data-ttu-id="9ec14-106">Tyto možnosti umožňují klienta pro řízení reprezentaci, který získá zpět ze serveru.</span><span class="sxs-lookup"><span data-stu-id="9ec14-106">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="9ec14-107">**$expand** způsobí, že související entity, které být zahrnuty vložené v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9ec14-107">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="9ec14-108">**$select** vybere podmnožinu vlastnosti, které chcete zahrnout do odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9ec14-108">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="9ec14-109">**$value** získá nezpracovanou hodnotu vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9ec14-109">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="9ec14-110">Příklad schématu</span><span class="sxs-lookup"><span data-stu-id="9ec14-110">Example Schema</span></span>

<span data-ttu-id="9ec14-111">Pro účely tohoto článku používám služby OData, který definuje tři entity: Produktu, dodavatel a kategorie.</span><span class="sxs-lookup"><span data-stu-id="9ec14-111">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="9ec14-112">Každý produkt má jednu kategorii a jednoho dodavatele.</span><span class="sxs-lookup"><span data-stu-id="9ec14-112">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="9ec14-113">Tady jsou třídy C#, které definují modely entity:</span><span class="sxs-lookup"><span data-stu-id="9ec14-113">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="9ec14-114">Všimněte si, že `Product` třídy definuje vlastnosti navigace `Supplier` a `Category`.</span><span class="sxs-lookup"><span data-stu-id="9ec14-114">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="9ec14-115">`Category` Třída definuje vlastnost navigace pro produkty v jednotlivých kategoriích.</span><span class="sxs-lookup"><span data-stu-id="9ec14-115">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="9ec14-116">Chcete-li vytvořit koncový bod OData pro toto schéma, použijte generování uživatelského rozhraní sady Visual Studio 2013, jak je popsáno v [vytváření koncového bodu OData v rozhraní ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="9ec14-116">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="9ec14-117">Přidejte samostatný řadiče pro produkt, kategorie a dodavateli.</span><span class="sxs-lookup"><span data-stu-id="9ec14-117">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="9ec14-118">Povolení $rozbalte a $select</span><span class="sxs-lookup"><span data-stu-id="9ec14-118">Enabling $expand and $select</span></span>

<span data-ttu-id="9ec14-119">V sadě Visual Studio 2013 generování uživatelského rozhraní Web API OData vytvoří kontroler, který automaticky podporuje $expand a $select.</span><span class="sxs-lookup"><span data-stu-id="9ec14-119">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="9ec14-120">Pro srovnání, tady jsou požadavky na podporu $rozbalte a $select v kontroleru.</span><span class="sxs-lookup"><span data-stu-id="9ec14-120">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="9ec14-121">Pro kolekce, kontroler společnosti `Get` metoda musí vracet **IQueryable**.</span><span class="sxs-lookup"><span data-stu-id="9ec14-121">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="9ec14-122">Pro jednotlivé entity, vrátí **SingleResult&lt;T&gt;**, kde T je **IQueryable** obsahující žádnou nebo jednu entitu.</span><span class="sxs-lookup"><span data-stu-id="9ec14-122">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="9ec14-123">Navíc uspořádání vašich `Get` metody s **[Queryable]** atributu, jak je znázorněno v předchozích fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="9ec14-123">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="9ec14-124">Můžete také volat **EnableQuerySupport** na **HttpConfiguration** při spuštění.</span><span class="sxs-lookup"><span data-stu-id="9ec14-124">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="9ec14-125">(Další informace najdete v tématu [povolení možnosti dotazu OData](supporting-odata-query-options.md#enable).)</span><span class="sxs-lookup"><span data-stu-id="9ec14-125">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="9ec14-126">Rozbalte položku pomocí $</span><span class="sxs-lookup"><span data-stu-id="9ec14-126">Using $expand</span></span>

<span data-ttu-id="9ec14-127">Když odešlete dotaz OData entitu nebo kolekci, výchozí odpověď neobsahuje související entity.</span><span class="sxs-lookup"><span data-stu-id="9ec14-127">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="9ec14-128">Tady je příklad, výchozí odpověď pro sadu entit kategorií:</span><span class="sxs-lookup"><span data-stu-id="9ec14-128">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="9ec14-129">Jak je vidět, odpověď neobsahuje žádné produkty, i v případě, že má entita kategorie produktů navigační odkaz.</span><span class="sxs-lookup"><span data-stu-id="9ec14-129">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="9ec14-130">Však může klient použít $rozbalte zobrazíte seznam produktů pro každou kategorii.</span><span class="sxs-lookup"><span data-stu-id="9ec14-130">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="9ec14-131">Možnost rozbalování na $ přejde v řetězci dotazu požadavku:</span><span class="sxs-lookup"><span data-stu-id="9ec14-131">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="9ec14-132">Server teď bude obsahovat produktů pro každou kategorii, vložený v kategorii.</span><span class="sxs-lookup"><span data-stu-id="9ec14-132">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="9ec14-133">Tady je datové části odpovědi:</span><span class="sxs-lookup"><span data-stu-id="9ec14-133">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="9ec14-134">Všimněte si, že každá položka v poli "value" obsahuje seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="9ec14-134">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="9ec14-135">$Expand možnost přijímá čárkami oddělený seznam navigačních vlastností pro rozbalení.</span><span class="sxs-lookup"><span data-stu-id="9ec14-135">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="9ec14-136">Následující požadavek rozšíří kategorii a dodavatele, produktu.</span><span class="sxs-lookup"><span data-stu-id="9ec14-136">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="9ec14-137">Tady je text odpovědi:</span><span class="sxs-lookup"><span data-stu-id="9ec14-137">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="9ec14-138">Můžete rozbalit více než jednu úroveň navigační vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9ec14-138">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="9ec14-139">Následující příklad obsahuje všechny produkty pro kategorii a také dodavatel pro jednotlivé produkty.</span><span class="sxs-lookup"><span data-stu-id="9ec14-139">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="9ec14-140">Tady je text odpovědi:</span><span class="sxs-lookup"><span data-stu-id="9ec14-140">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="9ec14-141">Ve výchozím omezení webového rozhraní API hloubku maximální rozšíření na 2.</span><span class="sxs-lookup"><span data-stu-id="9ec14-141">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="9ec14-142">Klient, který brání v odesílání složité požadavky, jako je `$expand=Orders/OrderDetails/Product/Supplier/Region`, který může být neefektivní pro dotazování a vytvořit velké odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9ec14-142">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="9ec14-143">Chcete-li přepsat výchozí hodnotu, nastavte **MaxExpansionDepth** vlastnost na **[Queryable]** atribut.</span><span class="sxs-lookup"><span data-stu-id="9ec14-143">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="9ec14-144">Další informace o $rozšířit možnosti, najdete v části [rozbalte možností dotazu systému ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) v oficiální dokumentaci OData.</span><span class="sxs-lookup"><span data-stu-id="9ec14-144">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="9ec14-145">Pomocí $select</span><span class="sxs-lookup"><span data-stu-id="9ec14-145">Using $select</span></span>

<span data-ttu-id="9ec14-146">Možnost $select určuje podmnožinu vlastností, které budou obsahovat v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9ec14-146">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="9ec14-147">Například pokud chcete získat název a ceny jednotlivých produktů, použijte následující dotaz:</span><span class="sxs-lookup"><span data-stu-id="9ec14-147">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="9ec14-148">Tady je text odpovědi:</span><span class="sxs-lookup"><span data-stu-id="9ec14-148">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="9ec14-149">Můžete kombinovat $select a $expand ve stejném dotazu.</span><span class="sxs-lookup"><span data-stu-id="9ec14-149">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="9ec14-150">Ujistěte se, že mají být zahrnuty vlastnost rozšířené možnosti $select.</span><span class="sxs-lookup"><span data-stu-id="9ec14-150">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="9ec14-151">Například následující požadavek získá název produktu a dodavateli.</span><span class="sxs-lookup"><span data-stu-id="9ec14-151">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="9ec14-152">Tady je text odpovědi:</span><span class="sxs-lookup"><span data-stu-id="9ec14-152">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="9ec14-153">Můžete také vybrat vlastnosti v rámci rozšířené vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9ec14-153">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="9ec14-154">Následující požadavek rozšiřuje produktů a vybere název kategorie a název produktu.</span><span class="sxs-lookup"><span data-stu-id="9ec14-154">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="9ec14-155">Tady je text odpovědi:</span><span class="sxs-lookup"><span data-stu-id="9ec14-155">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="9ec14-156">Další informace o možnosti $select, naleznete v tématu [vyberte možností dotazu systému ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) v oficiální dokumentaci OData.</span><span class="sxs-lookup"><span data-stu-id="9ec14-156">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="9ec14-157">Načtení jednotlivých vlastností entity ($value)</span><span class="sxs-lookup"><span data-stu-id="9ec14-157">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="9ec14-158">Existují dva způsoby, jak klient OData Chcete-li získat jednotlivé vlastnost z entity.</span><span class="sxs-lookup"><span data-stu-id="9ec14-158">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="9ec14-159">Klienta můžete získat hodnotu ve formátu OData nebo získat nezpracované hodnoty vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9ec14-159">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="9ec14-160">Následující požadavek získá vlastnost ve formátu OData.</span><span class="sxs-lookup"><span data-stu-id="9ec14-160">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="9ec14-161">Tady je příklad odpovědi ve formátu JSON:</span><span class="sxs-lookup"><span data-stu-id="9ec14-161">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="9ec14-162">Nezpracovaná hodnota vlastnosti získáte připojte k identifikátoru URI $value:</span><span class="sxs-lookup"><span data-stu-id="9ec14-162">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="9ec14-163">Tady je tato odpověď.</span><span class="sxs-lookup"><span data-stu-id="9ec14-163">Here is the response.</span></span> <span data-ttu-id="9ec14-164">Všimněte si, že typ obsahu není "text/plain" JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec14-164">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="9ec14-165">Pro podporu těchto dotazů v řadiče OData, přidejte metodu s názvem `GetProperty`, kde `Property` je název vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9ec14-165">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="9ec14-166">Například metoda GET pro vlastnost název pojmenován `GetName`.</span><span class="sxs-lookup"><span data-stu-id="9ec14-166">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="9ec14-167">Metoda by měla vrátit hodnota dané vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="9ec14-167">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
