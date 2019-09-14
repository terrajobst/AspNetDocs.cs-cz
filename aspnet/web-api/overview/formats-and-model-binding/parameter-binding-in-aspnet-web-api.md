---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: Vazba parametrů ve webovém rozhraní API ASP.NET – ASP.NET 4. x
author: MikeWasson
description: Popisuje, jak rozhraní Web API váže parametry a jak přizpůsobit proces vazby v ASP.NET 4. x.
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5386532ab581e023d93d16a5d4107e07f40b986f
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985824"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="d8b82-103">Vazba parametrů ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d8b82-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="d8b82-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d8b82-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="d8b82-105">Tento článek popisuje, jak rozhraní Web API váže parametry a jak můžete přizpůsobit proces vazby.</span><span class="sxs-lookup"><span data-stu-id="d8b82-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="d8b82-106">Když webové rozhraní API volá metodu na řadiči, musí nastavit hodnoty pro parametry, což je proces s názvem *vazba*.</span><span class="sxs-lookup"><span data-stu-id="d8b82-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span>

<span data-ttu-id="d8b82-107">Ve výchozím nastavení používá webové rozhraní API následující pravidla pro svázání parametrů:</span><span class="sxs-lookup"><span data-stu-id="d8b82-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="d8b82-108">Pokud je parametr "jednoduchý" typ, webové rozhraní API se pokusí získat hodnotu z identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="d8b82-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="d8b82-109">Mezi jednoduché typy patří [primitivní typy](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) rozhraní .NET (**int**, **bool**, **Double**a tak dále), plus **TimeSpan**, **DateTime**, **GUID**, **Decimal**a **String**a *navíc* libovolný typ s typem. převaděč, který může být převeden z řetězce.</span><span class="sxs-lookup"><span data-stu-id="d8b82-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="d8b82-110">(Další informace o převaděčích typů později.)</span><span class="sxs-lookup"><span data-stu-id="d8b82-110">(More about type converters later.)</span></span>
- <span data-ttu-id="d8b82-111">Pro komplexní typy se webové rozhraní API pokusí přečíst hodnotu z těla zprávy pomocí [formátovacího modulu typu média](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="d8b82-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="d8b82-112">Příkladem je příklad typické metody řadiče webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="d8b82-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="d8b82-113">Parametr *ID* je &quot;jednoduchý&quot; typ, takže se webové rozhraní API pokusí získat hodnotu z identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="d8b82-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="d8b82-114">Parametr *Item* je komplexní typ, takže webové rozhraní API používá ke čtení hodnoty z textu žádosti formátovací modul typu Media.</span><span class="sxs-lookup"><span data-stu-id="d8b82-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="d8b82-115">Pokud chcete získat hodnotu z identifikátoru URI, webové rozhraní API bude hledat v řetězci směrování dat a v řetězci dotazu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="d8b82-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="d8b82-116">Data trasy se naplní, když systém směrování analyzuje identifikátor URI a odpovídá na trasu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="d8b82-117">Další informace najdete v tématu [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="d8b82-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="d8b82-118">Ve zbývající části tohoto článku si ukážeme, jak můžete přizpůsobit proces vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="d8b82-119">U komplexních typů však zvažte použití formátovacích formátovacích typů médií, kdykoli je to možné.</span><span class="sxs-lookup"><span data-stu-id="d8b82-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="d8b82-120">Klíčovým principem protokolu HTTP je odeslání prostředků do těla zprávy pomocí vyjednávání obsahu pro určení reprezentace prostředku.</span><span class="sxs-lookup"><span data-stu-id="d8b82-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="d8b82-121">Formátovací moduly typu média byly navrženy pro přesně tento účel.</span><span class="sxs-lookup"><span data-stu-id="d8b82-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="d8b82-122">Použití [FromUri]</span><span class="sxs-lookup"><span data-stu-id="d8b82-122">Using [FromUri]</span></span>

<span data-ttu-id="d8b82-123">Chcete-li vynutit, aby webové rozhraní API četlo komplexní typ z identifikátoru URI, přidejte do parametru atribut **[FromUri]** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="d8b82-124">Následující příklad definuje `GeoPoint` typ spolu s metodou kontroleru, která `GeoPoint` získá z identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="d8b82-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="d8b82-125">Klient může do řetězce dotazu umístit hodnoty zeměpisné šířky a délky a webové rozhraní API je bude používat k sestavení `GeoPoint`.</span><span class="sxs-lookup"><span data-stu-id="d8b82-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="d8b82-126">Příklad:</span><span class="sxs-lookup"><span data-stu-id="d8b82-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="d8b82-127">Použití [FromBody]</span><span class="sxs-lookup"><span data-stu-id="d8b82-127">Using [FromBody]</span></span>

<span data-ttu-id="d8b82-128">Chcete-li vynutit, aby webové rozhraní API četlo jednoduchý typ z těla žádosti, přidejte do parametru atribut **[FromBody]** :</span><span class="sxs-lookup"><span data-stu-id="d8b82-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="d8b82-129">V tomto příkladu webové rozhraní API použije ke čtení hodnoty *názvu* z textu žádosti formátovací modul typu Media.</span><span class="sxs-lookup"><span data-stu-id="d8b82-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="d8b82-130">Tady je příklad žádosti klienta.</span><span class="sxs-lookup"><span data-stu-id="d8b82-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="d8b82-131">Když parametr obsahuje [FromBody], webové rozhraní API použije hlavičku Content-Type k výběru formátovacího modulu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="d8b82-132">V tomto příkladu je typem &quot;obsahu Application/JSON&quot; a tělo požadavku je nezpracovaný řetězec JSON (ne objekt JSON).</span><span class="sxs-lookup"><span data-stu-id="d8b82-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="d8b82-133">Čtení z textu zprávy může mít maximálně jeden parametr.</span><span class="sxs-lookup"><span data-stu-id="d8b82-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="d8b82-134">Takže to nebude fungovat:</span><span class="sxs-lookup"><span data-stu-id="d8b82-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="d8b82-135">Důvodem pro toto pravidlo je, že text požadavku může být uložený v nebufferovém datovém proudu, který se dá číst jenom jednou.</span><span class="sxs-lookup"><span data-stu-id="d8b82-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="d8b82-136">Převaděče typů</span><span class="sxs-lookup"><span data-stu-id="d8b82-136">Type Converters</span></span>

<span data-ttu-id="d8b82-137">Webové rozhraní API můžete považovat za jednoduchý typ (takže se webové rozhraní API pokusí vytvořit vazby z identifikátoru URI) vytvořením **třídy TypeConverter** a zadáním převodu řetězce.</span><span class="sxs-lookup"><span data-stu-id="d8b82-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="d8b82-138">Následující kód ukazuje `GeoPoint` třídu reprezentující zeměpisný bod a **třídu TypeConverter** , která je převedena z řetězců na `GeoPoint` instance.</span><span class="sxs-lookup"><span data-stu-id="d8b82-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="d8b82-139">Třída je upravena pomocí atributu **[TypeConverter]** pro určení převaděče typu. `GeoPoint`</span><span class="sxs-lookup"><span data-stu-id="d8b82-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="d8b82-140">(Tento příklad byl nechte inspirovat na blogovém příspěvku Jan Stallion, [jak vytvořit vazby k vlastním objektům v podpisech akcí v MVC/WebApi](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span><span class="sxs-lookup"><span data-stu-id="d8b82-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="d8b82-141">Teď bude webové rozhraní API `GeoPoint` považovat za jednoduchý typ, což znamená, že se `GeoPoint` pokusí vytvořit vazby parametrů z identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="d8b82-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="d8b82-142">Do parametru není nutné zahrnout **[FromUri]** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="d8b82-143">Klient může metodu vyvolat pomocí identifikátoru URI, například:</span><span class="sxs-lookup"><span data-stu-id="d8b82-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="d8b82-144">Pořadače modelů</span><span class="sxs-lookup"><span data-stu-id="d8b82-144">Model Binders</span></span>

<span data-ttu-id="d8b82-145">Pružnější možnost než konvertor typu je vytvoření vlastního pořadače modelů.</span><span class="sxs-lookup"><span data-stu-id="d8b82-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="d8b82-146">Pomocí pořadače modelů máte přístup k takovým akcím, jako je požadavek HTTP, popis akce a nezpracované hodnoty z dat směrování.</span><span class="sxs-lookup"><span data-stu-id="d8b82-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="d8b82-147">Chcete-li vytvořit pořadač modelů, implementujte rozhraní **IModelBinder** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="d8b82-148">Toto rozhraní definuje jedinou metodu **BindModel**:</span><span class="sxs-lookup"><span data-stu-id="d8b82-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="d8b82-149">Tady je modelový pořadač pro `GeoPoint` objekty.</span><span class="sxs-lookup"><span data-stu-id="d8b82-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="d8b82-150">Pořadač modelů získá nezpracované vstupní hodnoty od *poskytovatele hodnot*.</span><span class="sxs-lookup"><span data-stu-id="d8b82-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="d8b82-151">Tento návrh odděluje dvě různé funkce:</span><span class="sxs-lookup"><span data-stu-id="d8b82-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="d8b82-152">Zprostředkovatel hodnoty převezme požadavek HTTP a naplní slovník párů klíč-hodnota.</span><span class="sxs-lookup"><span data-stu-id="d8b82-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="d8b82-153">Pořadač modelů používá tento slovník k naplnění modelu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="d8b82-154">Výchozí zprostředkovatel hodnoty ve webovém rozhraní API získává hodnoty z dat směrování a řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="d8b82-155">Například pokud je `http://localhost/api/values/1?location=48,-122`identifikátor URI, zprostředkovatel hodnoty vytvoří následující páry klíč-hodnota:</span><span class="sxs-lookup"><span data-stu-id="d8b82-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="d8b82-156">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="d8b82-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="d8b82-157">umístění = &quot;48 122&quot;</span><span class="sxs-lookup"><span data-stu-id="d8b82-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="d8b82-158">(Předpokládáme výchozí šablonu směrování, která je &quot;API/{Controller}/{ID}&quot;.)</span><span class="sxs-lookup"><span data-stu-id="d8b82-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="d8b82-159">Název parametru, který se má vytvořit, je uložený ve vlastnosti **ModelBindingContext. model** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="d8b82-160">Pořadač modelů vyhledá klíč s touto hodnotou ve slovníku.</span><span class="sxs-lookup"><span data-stu-id="d8b82-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="d8b82-161">Pokud hodnota existuje a může být převedena `GeoPoint`na, pořadač modelů přiřadí vázanou hodnotu vlastnosti **ModelBindingContext. model** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="d8b82-162">Všimněte si, že pořadač modelů není omezený na jednoduchý převod typu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="d8b82-163">V tomto příkladu pořadač modelů nejprve vyhledá tabulku známých umístění a pokud se to nepovede, používá převod typu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="d8b82-164">**Nastavení pořadače modelů**</span><span class="sxs-lookup"><span data-stu-id="d8b82-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="d8b82-165">Existuje několik způsobů, jak nastavit pořadač modelů.</span><span class="sxs-lookup"><span data-stu-id="d8b82-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="d8b82-166">Nejprve můžete k parametru přidat atribut **[ModelBinder]** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="d8b82-167">K typu můžete také přidat atribut **[ModelBinder]** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="d8b82-168">Webové rozhraní API bude používat zadaný modelový pořadač pro všechny parametry tohoto typu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="d8b82-169">Nakonec můžete přidat poskytovatele modelového pořadače do **HttpConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="d8b82-170">Poskytovatel pořadače modelů je jednoduše třída továrny, která vytváří pořadač modelů.</span><span class="sxs-lookup"><span data-stu-id="d8b82-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="d8b82-171">Zprostředkovatele můžete vytvořit odvozením z třídy [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d8b82-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="d8b82-172">Pokud však pořadač modelů zpracovává jeden typ, je snazší použít vestavěný **SimpleModelBinderProvider**, která je navržena pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="d8b82-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="d8b82-173">Následující kód ukazuje, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="d8b82-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="d8b82-174">U poskytovatele vázání modelů stále potřebujete přidat do parametru atribut **[ModelBinder]** , aby bylo možné sdělit webovému rozhraní API, že by měl používat pořadač modelů a nikoli formátování mediálního typu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="d8b82-175">Nyní ale není nutné zadávat typ pořadače modelů v atributu:</span><span class="sxs-lookup"><span data-stu-id="d8b82-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="d8b82-176">Zprostředkovatelé hodnot</span><span class="sxs-lookup"><span data-stu-id="d8b82-176">Value Providers</span></span>

<span data-ttu-id="d8b82-177">Uvedli jsem, že pořadač modelů Získá hodnoty od poskytovatele hodnot.</span><span class="sxs-lookup"><span data-stu-id="d8b82-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="d8b82-178">Chcete-li napsat vlastního zprostředkovatele hodnoty, implementujte rozhraní **IValueProvider** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="d8b82-179">Tady je příklad, který načte hodnoty z souborů cookie v žádosti:</span><span class="sxs-lookup"><span data-stu-id="d8b82-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="d8b82-180">Také je nutné vytvořit továrnu poskytovatele hodnot odvozenou od třídy **ValueProviderFactory** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="d8b82-181">Přidejte objekt pro vytváření zprostředkovatele hodnoty do **HttpConfiguration** následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="d8b82-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="d8b82-182">Webové rozhraní API vytvoří všechny poskytovatele hodnot, takže když pořadač modelu volá **ValueProvider. GetValue**, modelový pořadač obdrží hodnotu od prvního poskytovatele hodnoty, který je schopný ho vytvořit.</span><span class="sxs-lookup"><span data-stu-id="d8b82-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="d8b82-183">Alternativně můžete nastavit objekt pro vytváření zprostředkovatele hodnoty na úrovni parametru pomocí atributu **ValueProvider** následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d8b82-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="d8b82-184">To oznamuje webovému rozhraní API použití vazby modelu se zadaným objektem pro vytváření zprostředkovatelů hodnot a nepoužívá žádné jiné registrované zprostředkovatele registrovaných hodnot.</span><span class="sxs-lookup"><span data-stu-id="d8b82-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="d8b82-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="d8b82-185">HttpParameterBinding</span></span>

<span data-ttu-id="d8b82-186">Pořadače modelů jsou konkrétní instancí obecnější mechanismu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="d8b82-187">Pokud se podíváte na atribut **[ModelBinder]** , uvidíte, že je odvozen z abstraktní třídy **ParameterBindingAttribute** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="d8b82-188">Tato třída definuje jedinou metodu **GetBinding**, která vrací objekt **HttpParameterBinding** :</span><span class="sxs-lookup"><span data-stu-id="d8b82-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="d8b82-189">**HttpParameterBinding** zodpovídá za vazbu parametru na hodnotu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="d8b82-190">V případě **[ModelBinder]** vrátí atribut implementaci **HttpParameterBinding** , která používá **IModelBinder** k provedení skutečné vazby.</span><span class="sxs-lookup"><span data-stu-id="d8b82-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="d8b82-191">Můžete také implementovat vlastní **HttpParameterBinding**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="d8b82-192">Předpokládejme například, že chcete v žádosti získat značky ETag `if-match` a `if-none-match` Headers.</span><span class="sxs-lookup"><span data-stu-id="d8b82-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="d8b82-193">Začneme definováním třídy, která bude představovat značky ETag.</span><span class="sxs-lookup"><span data-stu-id="d8b82-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="d8b82-194">Také definujeme výčet, který označuje, jestli se má z `if-match` hlavičky `if-none-match` nebo hlavičky získat ETag.</span><span class="sxs-lookup"><span data-stu-id="d8b82-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="d8b82-195">Zde je **HttpParameterBinding** , který získá značku ETag z požadované hlavičky a váže ji k parametru typu ETag:</span><span class="sxs-lookup"><span data-stu-id="d8b82-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="d8b82-196">Metoda **ExecuteBindingAsync** provede vazbu.</span><span class="sxs-lookup"><span data-stu-id="d8b82-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="d8b82-197">V rámci této metody přidejte hodnotu vázaného parametru do **ActionArgument** slovníku v **HttpActionContext**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="d8b82-198">Pokud vaše metoda **ExecuteBindingAsync** přečte tělo zprávy s požadavkem, přepište vlastnost **WillReadBody** na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="d8b82-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="d8b82-199">Text požadavku může být datový proud bez vyrovnávací paměti, který se dá číst jenom jednou, takže webové rozhraní API vynutilo pravidlo, které může přečíst tělo zprávy na maximálně jedné vazbě.</span><span class="sxs-lookup"><span data-stu-id="d8b82-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="d8b82-200">Chcete-li použít vlastní **HttpParameterBinding**, můžete definovat atribut, který je odvozen z **ParameterBindingAttribute**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="d8b82-201">V `ETagParameterBinding`případě definujeme dva atributy, jeden pro `if-match` záhlaví a jeden pro `if-none-match` záhlaví.</span><span class="sxs-lookup"><span data-stu-id="d8b82-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="d8b82-202">Obě jsou odvozeny od abstraktní základní třídy.</span><span class="sxs-lookup"><span data-stu-id="d8b82-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="d8b82-203">Zde je metoda kontroleru, která používá `[IfNoneMatch]` atribut.</span><span class="sxs-lookup"><span data-stu-id="d8b82-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="d8b82-204">Kromě **ParameterBindingAttribute**existuje další zavěšení pro přidání vlastní **HttpParameterBinding**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="d8b82-205">V objektu **HttpConfiguration** je vlastnost **ParameterBindingRules** kolekcí anonymních funkcí typu (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**).</span><span class="sxs-lookup"><span data-stu-id="d8b82-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="d8b82-206">Například můžete přidat pravidlo, které obsahuje `ETagParameterBinding` libovolný parametr ETag metody Get s: `if-none-match`</span><span class="sxs-lookup"><span data-stu-id="d8b82-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="d8b82-207">Funkce by měla vracet `null` pro parametry, kde vazba není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="d8b82-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="d8b82-208">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="d8b82-208">IActionValueBinder</span></span>

<span data-ttu-id="d8b82-209">Celý proces vázání parametrů je řízen službou, kterou může připojit **IActionValueBinder**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="d8b82-210">Výchozí implementace **IActionValueBinder** provádí následující akce:</span><span class="sxs-lookup"><span data-stu-id="d8b82-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="d8b82-211">Vyhledejte v parametru **ParameterBindingAttribute** .</span><span class="sxs-lookup"><span data-stu-id="d8b82-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="d8b82-212">To zahrnuje **[FromBody]** , **[FromUri]** a **[ModelBinder]** , nebo vlastní atributy.</span><span class="sxs-lookup"><span data-stu-id="d8b82-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="d8b82-213">V opačném případě vyhledejte **HttpConfiguration. ParameterBindingRules** pro funkci, která vrací **HttpParameterBinding**s hodnotou jinou než null.</span><span class="sxs-lookup"><span data-stu-id="d8b82-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="d8b82-214">Jinak použijte výchozí pravidla, která jsme popsali dříve.</span><span class="sxs-lookup"><span data-stu-id="d8b82-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="d8b82-215">Pokud je typ parametru "jednoduchý" nebo má konvertor typu, vazba z identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="d8b82-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="d8b82-216">Jedná se o ekvivalent pro vložení atributu **[FromUri]** v parametru.</span><span class="sxs-lookup"><span data-stu-id="d8b82-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="d8b82-217">V opačném případě se pokuste načíst parametr z textu zprávy.</span><span class="sxs-lookup"><span data-stu-id="d8b82-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="d8b82-218">Jedná se o ekvivalent umístění **[FromBody]** v parametru.</span><span class="sxs-lookup"><span data-stu-id="d8b82-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="d8b82-219">Pokud jste chtěli, můžete nahradit celou službu **IActionValueBinder** vlastní implementací.</span><span class="sxs-lookup"><span data-stu-id="d8b82-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8b82-220">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="d8b82-220">Additional Resources</span></span>

[<span data-ttu-id="d8b82-221">Ukázka vazby vlastního parametru</span><span class="sxs-lookup"><span data-stu-id="d8b82-221">Custom Parameter Binding Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

<span data-ttu-id="d8b82-222">Jan kout zapsal dobrý seriál blogových příspěvků o vazbě parametru webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="d8b82-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="d8b82-223">Způsob vazby parametrů webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="d8b82-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="d8b82-224">Vazba parametrů stylu MVC pro webové rozhraní API</span><span class="sxs-lookup"><span data-stu-id="d8b82-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="d8b82-225">Vytvoření vazby na vlastní objekty v podpisech akcí v MVC nebo webovém rozhraní API</span><span class="sxs-lookup"><span data-stu-id="d8b82-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="d8b82-226">Postup vytvoření vlastního zprostředkovatele hodnoty ve webovém rozhraní API</span><span class="sxs-lookup"><span data-stu-id="d8b82-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="d8b82-227">Vazba parametrů webového rozhraní API v digestoři</span><span class="sxs-lookup"><span data-stu-id="d8b82-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
