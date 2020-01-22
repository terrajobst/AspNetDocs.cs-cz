---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: Podpora BSON v rozhraní ASP.NET Web API 2,1 – ASP.NET 4. x
author: MikeWasson
description: ukazuje, jak používat BSON v řadiči webového rozhraní API (na straně serveru) a v klientské aplikaci .NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519324"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="39e51-103">Podpora BSON v rozhraní ASP.NET Web API 2,1</span><span class="sxs-lookup"><span data-stu-id="39e51-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="39e51-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="39e51-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="39e51-105">V tomto tématu se dozvíte, jak používat BSON v řadiči webového rozhraní API (na straně serveru) a v klientské aplikaci .NET.</span><span class="sxs-lookup"><span data-stu-id="39e51-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="39e51-106">Webové rozhraní API 2,1 zavádí podporu pro BSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="39e51-107">Co je BSON?</span><span class="sxs-lookup"><span data-stu-id="39e51-107">What is BSON?</span></span>

<span data-ttu-id="39e51-108">[Bson](http://bsonspec.org/) je binární serializace formátu.</span><span class="sxs-lookup"><span data-stu-id="39e51-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="39e51-109">"BSON" je zkratka "Binary JSON", ale BSON a JSON jsou serializovány velmi jinak.</span><span class="sxs-lookup"><span data-stu-id="39e51-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="39e51-110">BSON je typu "JSON", protože objekty jsou reprezentovány jako páry název-hodnota, podobně jako JSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="39e51-111">Na rozdíl od formátu JSON jsou číselné datové typy uloženy jako bajty, nikoli řetězce.</span><span class="sxs-lookup"><span data-stu-id="39e51-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="39e51-112">BSON byla navržena jako odlehčená, snadná a rychlá pro kódování a dekódování.</span><span class="sxs-lookup"><span data-stu-id="39e51-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="39e51-113">BSON má srovnatelné velikosti až JSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="39e51-114">V závislosti na datech může být datová část BSON menší nebo větší než datová část JSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="39e51-115">Pro serializaci binárních dat, jako je například soubor obrázku, je BSON menší než JSON, protože binární data nejsou zakódovaná ve formátu base64.</span><span class="sxs-lookup"><span data-stu-id="39e51-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="39e51-116">Dokumenty BSON se snadno prohledávají, protože prvky mají předponu pole length, takže analyzátor může přeskočit prvky bez jejich dekódování.</span><span class="sxs-lookup"><span data-stu-id="39e51-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="39e51-117">Kódování a dekódování jsou efektivní, protože číselné datové typy jsou uloženy jako čísla, nikoli jako řetězce.</span><span class="sxs-lookup"><span data-stu-id="39e51-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="39e51-118">Nativním klientům, jako jsou klientské aplikace .NET, můžou využívat BSON místo textových formátů, jako je JSON nebo XML.</span><span class="sxs-lookup"><span data-stu-id="39e51-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="39e51-119">Pro klienty prohlížeče pravděpodobně budete chtít s JSON, protože JavaScript může přímo převést datovou část JSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="39e51-120">Naštěstí webové rozhraní API využívá [vyjednávání obsahu](content-negotiation.md), takže vaše rozhraní API může podporovat oba formáty a nechat si klienta zvolit.</span><span class="sxs-lookup"><span data-stu-id="39e51-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="39e51-121">Povolení BSON na serveru</span><span class="sxs-lookup"><span data-stu-id="39e51-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="39e51-122">V konfiguraci webového rozhraní API přidejte **BsonMediaTypeFormatter** do kolekce formátovacích souborů.</span><span class="sxs-lookup"><span data-stu-id="39e51-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="39e51-123">Když teď klient požaduje "Application/bson", webové rozhraní API použije formátovací modul BSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="39e51-124">Pokud chcete přidružit BSON k ostatním typům médií, přidejte je do kolekce SupportedMediaTypes.</span><span class="sxs-lookup"><span data-stu-id="39e51-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="39e51-125">Následující kód přidá "application/vnd. contoso" do podporovaných typů médií:</span><span class="sxs-lookup"><span data-stu-id="39e51-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="39e51-126">Příklad relace HTTP</span><span class="sxs-lookup"><span data-stu-id="39e51-126">Example HTTP Session</span></span>

<span data-ttu-id="39e51-127">V tomto příkladu použijeme následující třídu modelu a jednoduchý kontroler webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="39e51-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="39e51-128">Klient může odeslat následující požadavek HTTP:</span><span class="sxs-lookup"><span data-stu-id="39e51-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="39e51-129">Tady je odpověď:</span><span class="sxs-lookup"><span data-stu-id="39e51-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="39e51-130">Zde jsem nahradili binární data &quot;.&quot; znaky.</span><span class="sxs-lookup"><span data-stu-id="39e51-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="39e51-131">Následující snímek obrazovky z Fiddler zobrazuje nezpracované šestnáctkové hodnoty.</span><span class="sxs-lookup"><span data-stu-id="39e51-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="39e51-132">Použití BSON s HttpClient</span><span class="sxs-lookup"><span data-stu-id="39e51-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="39e51-133">Klientské aplikace .NET můžou používat formátovací modul BSON s **HttpClient**.</span><span class="sxs-lookup"><span data-stu-id="39e51-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="39e51-134">Další informace o **HttpClient**najdete v tématu [volání webového rozhraní API z klienta .NET](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="39e51-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="39e51-135">Následující kód odešle požadavek GET, který přijme BSON, a poté deserializaci datové části BSON v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="39e51-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="39e51-136">Pro vyžádání BSON ze serveru nastavte hlavičku Accept na "Application/bson":</span><span class="sxs-lookup"><span data-stu-id="39e51-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="39e51-137">Chcete-li deserializovat tělo odpovědi, použijte **BsonMediaTypeFormatter**.</span><span class="sxs-lookup"><span data-stu-id="39e51-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="39e51-138">Tento formátovací modul není ve výchozí kolekci formátování, takže je nutné ho zadat při čtení těla odpovědi:</span><span class="sxs-lookup"><span data-stu-id="39e51-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="39e51-139">Další příklad ukazuje, jak odeslat požadavek POST, který obsahuje BSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="39e51-140">Většina tohoto kódu je stejná jako v předchozím příkladu.</span><span class="sxs-lookup"><span data-stu-id="39e51-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="39e51-141">Ale v metodě **PostAsync** zadejte **BsonMediaTypeFormatter** jako formátovací modul:</span><span class="sxs-lookup"><span data-stu-id="39e51-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="39e51-142">Serializace primitivních typů nejvyšší úrovně</span><span class="sxs-lookup"><span data-stu-id="39e51-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="39e51-143">Každý dokument BSON je seznam párů klíč/hodnota. Specifikace BSON nedefinuje syntaxi pro serializaci jedné nezpracované hodnoty, jako je například celé číslo nebo řetězec.</span><span class="sxs-lookup"><span data-stu-id="39e51-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="39e51-144">Chcete-li toto omezení obejít, **BsonMediaTypeFormatter** považuje primitivní typy za zvláštní případ.</span><span class="sxs-lookup"><span data-stu-id="39e51-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="39e51-145">Před serializací převede hodnotu na dvojici klíč/hodnota s klíčem "value".</span><span class="sxs-lookup"><span data-stu-id="39e51-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="39e51-146">Předpokládejme například, že váš kontroler rozhraní API vrací celé číslo:</span><span class="sxs-lookup"><span data-stu-id="39e51-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="39e51-147">Před serializací se formátovací modul BSON převede na následující pár klíč/hodnota:</span><span class="sxs-lookup"><span data-stu-id="39e51-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="39e51-148">Při deserializaci, formátovací modul převede data zpět na původní hodnotu.</span><span class="sxs-lookup"><span data-stu-id="39e51-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="39e51-149">Nicméně pokud vaše webové rozhraní API vrátí nezpracované hodnoty, budou se v takovém případě muset vycházet z klientů, kteří používají jiný analyzátor BSON.</span><span class="sxs-lookup"><span data-stu-id="39e51-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="39e51-150">Obecně byste měli zvážit vracení strukturovaných dat místo nezpracovaných hodnot.</span><span class="sxs-lookup"><span data-stu-id="39e51-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39e51-151">Další materiály a zdroje informací</span><span class="sxs-lookup"><span data-stu-id="39e51-151">Additional Resources</span></span>

[<span data-ttu-id="39e51-152">Ukázka BSON webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="39e51-152">Web API BSON Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[<span data-ttu-id="39e51-153">Formátovací moduly médií</span><span class="sxs-lookup"><span data-stu-id="39e51-153">Media Formatters</span></span>](media-formatters.md)
