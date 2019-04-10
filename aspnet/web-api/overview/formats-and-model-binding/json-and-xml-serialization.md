---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Serializace JSON a XML v rozhraní ASP.NET Web API – ASP.NET 4.x
author: MikeWasson
description: Popisuje formátování JSON a XML v rozhraní ASP.NET Web API pro ASP.NET 4.x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: a9e7ed63a55c146976e0221214e722f3a2292fee
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408274"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="2afa3-103">Serializace JSON a XML v rozhraní ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2afa3-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="2afa3-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2afa3-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2afa3-105">Tento článek popisuje formátování JSON a XML v rozhraní ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="2afa3-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="2afa3-106">V rozhraní ASP.NET Web API *formátovací modul typu média* je objekt, který můžete:</span><span class="sxs-lookup"><span data-stu-id="2afa3-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="2afa3-107">Tělo zprávy objekty CLR pro čtení z protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="2afa3-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="2afa3-108">Zápis objektů CLR do textu zprávy HTTP</span><span class="sxs-lookup"><span data-stu-id="2afa3-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="2afa3-109">Webové rozhraní API poskytuje formátovacích modulů typů médií pro JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="2afa3-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="2afa3-110">Rámci těchto formátování vloží do kanálu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="2afa3-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="2afa3-111">Klienti mohou požadovat JSON nebo XML v hlavičce Accept požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="2afa3-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="2afa3-112">Obsah</span><span class="sxs-lookup"><span data-stu-id="2afa3-112">Contents</span></span>

- [<span data-ttu-id="2afa3-113">Formátovací modul typu média JSON</span><span class="sxs-lookup"><span data-stu-id="2afa3-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="2afa3-114">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="2afa3-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="2afa3-115">Kalendářní data</span><span class="sxs-lookup"><span data-stu-id="2afa3-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="2afa3-116">Odsazení</span><span class="sxs-lookup"><span data-stu-id="2afa3-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="2afa3-117">CamelCase</span><span class="sxs-lookup"><span data-stu-id="2afa3-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="2afa3-118">Anonymní a slabě typované objekty</span><span class="sxs-lookup"><span data-stu-id="2afa3-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="2afa3-119">Formátovací modul typu média XML</span><span class="sxs-lookup"><span data-stu-id="2afa3-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="2afa3-120">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="2afa3-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="2afa3-121">Kalendářní data</span><span class="sxs-lookup"><span data-stu-id="2afa3-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="2afa3-122">Odsazení</span><span class="sxs-lookup"><span data-stu-id="2afa3-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="2afa3-123">Nastavení na typ XML Serializátorů</span><span class="sxs-lookup"><span data-stu-id="2afa3-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="2afa3-124">Odebrání formátovací modul XML nebo JSON</span><span class="sxs-lookup"><span data-stu-id="2afa3-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="2afa3-125">Zpracování objektu cyklické odkazy</span><span class="sxs-lookup"><span data-stu-id="2afa3-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="2afa3-126">Testování serializaci objektů</span><span class="sxs-lookup"><span data-stu-id="2afa3-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="2afa3-127">Formátovací modul typu média JSON</span><span class="sxs-lookup"><span data-stu-id="2afa3-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="2afa3-128">Formátování JSON je poskytován **JsonMediaTypeFormatter** třídy.</span><span class="sxs-lookup"><span data-stu-id="2afa3-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="2afa3-129">Ve výchozím nastavení **JsonMediaTypeFormatter** používá [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) knihovny provést serializace.</span><span class="sxs-lookup"><span data-stu-id="2afa3-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="2afa3-130">Json.NET je projekt otevřít zdroj třetích stran.</span><span class="sxs-lookup"><span data-stu-id="2afa3-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="2afa3-131">Pokud dáváte přednost, můžete nakonfigurovat **JsonMediaTypeFormatter** třídu použít **DataContractJsonSerializer** místo Json.NET.</span><span class="sxs-lookup"><span data-stu-id="2afa3-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="2afa3-132">Chcete-li to provést, nastavte **UseDataContractJsonSerializer** vlastnost **true**:</span><span class="sxs-lookup"><span data-stu-id="2afa3-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="2afa3-133">Serializace JSON</span><span class="sxs-lookup"><span data-stu-id="2afa3-133">JSON Serialization</span></span>

<span data-ttu-id="2afa3-134">Tato část popisuje některé konkrétní chování formátovací modul JSON pomocí výchozího [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializátor.</span><span class="sxs-lookup"><span data-stu-id="2afa3-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="2afa3-135">To neměl být úplnou dokumentaci Json.NET knihovny; Další informace najdete v tématu [Json.NET dokumentaci](http://james.newtonking.com/projects/json/help/).</span><span class="sxs-lookup"><span data-stu-id="2afa3-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="2afa3-136">Získá serializován co?</span><span class="sxs-lookup"><span data-stu-id="2afa3-136">What Gets Serialized?</span></span>

<span data-ttu-id="2afa3-137">Ve výchozím nastavení všechny veřejné vlastnosti a pole jsou součástí serializovaná JSON.</span><span class="sxs-lookup"><span data-stu-id="2afa3-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="2afa3-138">Pokud chcete vynechat, nechte vlastnost nebo pole, uspořádání ji **JsonIgnore** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="2afa3-139">Pokud chcete &quot;vyjádřit výslovný souhlas&quot; přístup, uspořádání třídy s **kontraktu dat DataContract** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="2afa3-140">Pokud tento atribut je k dispozici, členové jsou ignorovány, pokud nemají **DataMember**.</span><span class="sxs-lookup"><span data-stu-id="2afa3-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="2afa3-141">Můžete také použít **DataMember** k serializaci soukromé členy.</span><span class="sxs-lookup"><span data-stu-id="2afa3-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="2afa3-142">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="2afa3-142">Read-Only Properties</span></span>

<span data-ttu-id="2afa3-143">Ve výchozím nastavení se serializovat vlastnosti jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="2afa3-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="2afa3-144">Kalendářní data</span><span class="sxs-lookup"><span data-stu-id="2afa3-144">Dates</span></span>

<span data-ttu-id="2afa3-145">Ve výchozím nastavení, Json.NET zapisuje data při [ISO 8601](http://www.w3.org/TR/NOTE-datetime) formátu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="2afa3-146">Data ve standardu UTC (Coordinated Universal Time) jsou zapsány s příponou "Z".</span><span class="sxs-lookup"><span data-stu-id="2afa3-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="2afa3-147">Data v místním čase zahrnují posun časového pásma.</span><span class="sxs-lookup"><span data-stu-id="2afa3-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="2afa3-148">Příklad:</span><span class="sxs-lookup"><span data-stu-id="2afa3-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="2afa3-149">Ve výchozím nastavení zachovává Json.NET časové pásmo.</span><span class="sxs-lookup"><span data-stu-id="2afa3-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="2afa3-150">Toto můžete přepsat tak, že nastavíte vlastnost DateTimeZoneHandling:</span><span class="sxs-lookup"><span data-stu-id="2afa3-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="2afa3-151">Pokud byste radši chtěli použít [formát data Microsoft JSON](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) namísto formátu ISO 8601, nastavte **DateFormatHandling** vlastnost pro nastavení serializátoru:</span><span class="sxs-lookup"><span data-stu-id="2afa3-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="2afa3-152">Odsazení</span><span class="sxs-lookup"><span data-stu-id="2afa3-152">Indenting</span></span>

<span data-ttu-id="2afa3-153">Chcete-li zapsat odsazený JSON, nastavte **formátování** nastavení **Formatting.Indented**:</span><span class="sxs-lookup"><span data-stu-id="2afa3-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="2afa3-154">CamelCase</span><span class="sxs-lookup"><span data-stu-id="2afa3-154">Camel Casing</span></span>

<span data-ttu-id="2afa3-155">Chcete-li zapsat názvy vlastností JSON s camelCase, beze změny datového modelu, nastavte **CamelCasePropertyNamesContractResolver** na serializátoru:</span><span class="sxs-lookup"><span data-stu-id="2afa3-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="2afa3-156">Anonymní a slabě typované objekty</span><span class="sxs-lookup"><span data-stu-id="2afa3-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="2afa3-157">Metody akce můžete vrátit anonymní objekt a serializaci do formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="2afa3-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="2afa3-158">Příklad:</span><span class="sxs-lookup"><span data-stu-id="2afa3-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="2afa3-159">Tělo zprávy odpovědi bude obsahovat následující JSON:</span><span class="sxs-lookup"><span data-stu-id="2afa3-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="2afa3-160">Pokud vaše webové rozhraní API přijímá volně strukturovaná objekty JSON od klientů, při deserializaci v textu žádosti **Newtonsoft.Json.Linq.JObject** typu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="2afa3-161">Je však obvykle vhodnější použít objekty dat silného typu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="2afa3-162">Pak není nutné analyzovat data, a získáte výhody ověření modelu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="2afa3-163">Serializátor XML nepodporuje anonymní typy nebo **JObject** instancí.</span><span class="sxs-lookup"><span data-stu-id="2afa3-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="2afa3-164">Pokud použijete tyto funkce pro vaše data JSON, měli byste odebrat formátovací modul XML z kanálu, jak je popsáno dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="2afa3-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="2afa3-165">Formátovací modul typu média XML</span><span class="sxs-lookup"><span data-stu-id="2afa3-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="2afa3-166">Formát XML je poskytován **XmlMediaTypeFormatter** třídy.</span><span class="sxs-lookup"><span data-stu-id="2afa3-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="2afa3-167">Ve výchozím nastavení **XmlMediaTypeFormatter** používá **DataContractSerializer** pro provádění serializace.</span><span class="sxs-lookup"><span data-stu-id="2afa3-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="2afa3-168">Pokud dáváte přednost, můžete nakonfigurovat **XmlMediaTypeFormatter** používat **XmlSerializer** místo **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="2afa3-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="2afa3-169">Chcete-li to provést, nastavte **UseXmlSerializer** vlastnost **true**:</span><span class="sxs-lookup"><span data-stu-id="2afa3-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="2afa3-170">**XmlSerializer** třída podporuje užší sadu typů než **DataContractSerializer**, ale dává větší kontrolu nad výsledného kódu XML.</span><span class="sxs-lookup"><span data-stu-id="2afa3-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="2afa3-171">Zvažte použití **XmlSerializer** potřebujete odpovídat stávajícím schématu XML.</span><span class="sxs-lookup"><span data-stu-id="2afa3-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="2afa3-172">Serializace XML</span><span class="sxs-lookup"><span data-stu-id="2afa3-172">XML Serialization</span></span>

<span data-ttu-id="2afa3-173">Tato část popisuje některé konkrétní chování formátovací modul XML pomocí výchozího **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="2afa3-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="2afa3-174">Ve výchozím objektu DataContractSerializer chová takto:</span><span class="sxs-lookup"><span data-stu-id="2afa3-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="2afa3-175">Všechny vlastnosti veřejné čtení a zápis a pole se serializují.</span><span class="sxs-lookup"><span data-stu-id="2afa3-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="2afa3-176">Pokud chcete vynechat, nechte vlastnost nebo pole, uspořádání ji **IgnoreDataMember** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="2afa3-177">Soukromé a chráněné členy nejsou serializována.</span><span class="sxs-lookup"><span data-stu-id="2afa3-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="2afa3-178">Vlastnosti jen pro čtení nejsou serializována.</span><span class="sxs-lookup"><span data-stu-id="2afa3-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="2afa3-179">(Ale obsah vlastnosti kolekce jen pro čtení se serializují.)</span><span class="sxs-lookup"><span data-stu-id="2afa3-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="2afa3-180">Názvy tříd a členů jsou zapsány v souboru XML, přesně tak, jak jsou uvedeny v deklaraci třídy.</span><span class="sxs-lookup"><span data-stu-id="2afa3-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="2afa3-181">Výchozí obor názvů XML se používá.</span><span class="sxs-lookup"><span data-stu-id="2afa3-181">A default XML namespace is used.</span></span>

<span data-ttu-id="2afa3-182">Pokud potřebujete větší kontrolu nad serializace, můžete uspořádání třídy s **kontraktu dat DataContract** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="2afa3-183">Když tento atribut je k dispozici, je třída serializované následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2afa3-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="2afa3-184">&quot;Vyjádřit výslovný souhlas&quot; přístup: Pole a vlastnosti nejsou serializované ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="2afa3-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="2afa3-185">K serializaci vlastnost nebo pole, uspořádání ji **DataMember** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="2afa3-186">K serializaci soukromého nebo chráněného členu, uspořádání ji **DataMember** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="2afa3-187">Vlastnosti jen pro čtení nejsou serializována.</span><span class="sxs-lookup"><span data-stu-id="2afa3-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="2afa3-188">Chcete-li změnit, jak se zobrazí název třídy v souboru XML, nastavte *název* parametr **kontraktu dat DataContract** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="2afa3-189">Chcete-li změnit, jak se zobrazí název členu v souboru XML, nastavte *název* parametr **DataMember** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="2afa3-190">Chcete-li změnit obor názvů XML, nastavte *Namespace* parametr **kontraktu dat DataContract** třídy.</span><span class="sxs-lookup"><span data-stu-id="2afa3-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="2afa3-191">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="2afa3-191">Read-Only Properties</span></span>

<span data-ttu-id="2afa3-192">Vlastnosti jen pro čtení nejsou serializována.</span><span class="sxs-lookup"><span data-stu-id="2afa3-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="2afa3-193">Pokud je vlastnost jen pro čtení privátní pole zálohování, můžete označit privátní pole s **DataMember** atribut.</span><span class="sxs-lookup"><span data-stu-id="2afa3-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="2afa3-194">Tento přístup vyžaduje **kontraktu dat DataContract** pomocí atributu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="2afa3-195">Kalendářní data</span><span class="sxs-lookup"><span data-stu-id="2afa3-195">Dates</span></span>

<span data-ttu-id="2afa3-196">Data jsou napsané ve formátu ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="2afa3-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="2afa3-197">Například &quot;2012-05-23T20:21:37.9116538Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="2afa3-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="2afa3-198">Odsazení</span><span class="sxs-lookup"><span data-stu-id="2afa3-198">Indenting</span></span>

<span data-ttu-id="2afa3-199">Chcete-li zapsat odsazený XML, nastavte **odsazení** vlastnost **true**:</span><span class="sxs-lookup"><span data-stu-id="2afa3-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="2afa3-200">Nastavení na typ XML Serializátorů</span><span class="sxs-lookup"><span data-stu-id="2afa3-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="2afa3-201">Můžete nastavit různé serializátory XML pro různé typy CLR.</span><span class="sxs-lookup"><span data-stu-id="2afa3-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="2afa3-202">Například můžete mít určitý datový objekt, který vyžaduje **XmlSerializer** z důvodu zpětné kompatibility.</span><span class="sxs-lookup"><span data-stu-id="2afa3-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="2afa3-203">Můžete použít **XmlSerializer** pro tento objekt a dál používat **DataContractSerializer** u jiných typů.</span><span class="sxs-lookup"><span data-stu-id="2afa3-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="2afa3-204">Chcete-li nastavit serializátor XML pro určitý typ, zavolejte **SetSerializer**.</span><span class="sxs-lookup"><span data-stu-id="2afa3-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="2afa3-205">Můžete zadat **XmlSerializer** nebo libovolný objekt, který je odvozen od **XmlObjectSerializer**.</span><span class="sxs-lookup"><span data-stu-id="2afa3-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="2afa3-206">Odebrání formátovací modul XML nebo JSON</span><span class="sxs-lookup"><span data-stu-id="2afa3-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="2afa3-207">Formátování JSON nebo formátovací modul XML můžete odebrat z seznam formátovacích modulů, pokud nechcete k jejich použití.</span><span class="sxs-lookup"><span data-stu-id="2afa3-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="2afa3-208">Hlavní důvody k tomu jsou:</span><span class="sxs-lookup"><span data-stu-id="2afa3-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="2afa3-209">Chcete-li omezit vaše webové rozhraní API odpovědi na určitý typ média.</span><span class="sxs-lookup"><span data-stu-id="2afa3-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="2afa3-210">Například můžete rozhodnout pro podporu pouze odpověďmi ve formátu JSON a odebrat formátovací modul XML.</span><span class="sxs-lookup"><span data-stu-id="2afa3-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="2afa3-211">Nahradit výchozí formátování pomocí vlastního formátovacího modulu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="2afa3-212">Může například nahradit vlastní implementaci formátování JSON formátování JSON.</span><span class="sxs-lookup"><span data-stu-id="2afa3-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="2afa3-213">Následující kód ukazuje, jak odebrat výchozí formátování.</span><span class="sxs-lookup"><span data-stu-id="2afa3-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="2afa3-214">Volání z vaší **aplikace\_Start** metoda, definována v souboru Global.asax.</span><span class="sxs-lookup"><span data-stu-id="2afa3-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="2afa3-215">Zpracování objektu cyklické odkazy</span><span class="sxs-lookup"><span data-stu-id="2afa3-215">Handling Circular Object References</span></span>

<span data-ttu-id="2afa3-216">Ve výchozím nastavení formátování JSON a XML zápis všech objektů jako hodnoty.</span><span class="sxs-lookup"><span data-stu-id="2afa3-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="2afa3-217">Pokud dvě vlastnosti odkazují na stejný objekt nebo pokud se zobrazí na stejný objekt v kolekci dvakrát, formátovací modul se serializovat objekt dvakrát.</span><span class="sxs-lookup"><span data-stu-id="2afa3-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="2afa3-218">Totiž konkrétního problému. Pokud váš graf objektu obsahuje cykly, serializátoru, který vyvolá výjimku, když zjistí smyčku v grafu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="2afa3-219">Vezměte v úvahu následující objektové modely a kontroleru.</span><span class="sxs-lookup"><span data-stu-id="2afa3-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="2afa3-220">Vyvolání tato akce způsobí, že formátovací modul k vyvolání výjimky, která se přeloží na stavový kód 500 (vnitřní chyba serveru) odpověď klientovi.</span><span class="sxs-lookup"><span data-stu-id="2afa3-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="2afa3-221">Pokud chcete zachovat odkazy na objekty ve formátu JSON, přidejte následující kód k **aplikace\_Start** metody v souboru Global.asax:</span><span class="sxs-lookup"><span data-stu-id="2afa3-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="2afa3-222">Nyní akce kontroleru vrátí JSON, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="2afa3-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="2afa3-223">Všimněte si, že serializátor přidá &quot;$id&quot; vlastnost na oba objekty.</span><span class="sxs-lookup"><span data-stu-id="2afa3-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="2afa3-224">Navíc rozpozná, že vlastnost Employee.Department vytvoří smyčku, takže nahradí hodnotu odkazu na objekt: {&quot;$ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="2afa3-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="2afa3-225">Odkazy na objekty nejsou standardní ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="2afa3-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="2afa3-226">Před použitím této funkce, zvažte, jestli vaši klienti budou moci analyzovat výsledky.</span><span class="sxs-lookup"><span data-stu-id="2afa3-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="2afa3-227">Může být lepší jednoduše odstranit z grafu cykly.</span><span class="sxs-lookup"><span data-stu-id="2afa3-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="2afa3-228">Například odkaz z zaměstnance zpět do oddělení, není v tomto příkladu skutečně nutná.</span><span class="sxs-lookup"><span data-stu-id="2afa3-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>


<span data-ttu-id="2afa3-229">Pokud chcete zachovat odkazy na objekty ve formátu XML, máte dvě možnosti.</span><span class="sxs-lookup"><span data-stu-id="2afa3-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="2afa3-230">Jednodušší možností je přidat `[DataContract(IsReference=true)]` do vaší třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="2afa3-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="2afa3-231">*IsReference* parametr povoluje odkazy na objekty.</span><span class="sxs-lookup"><span data-stu-id="2afa3-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="2afa3-232">Nezapomeňte, že **kontraktu dat DataContract** díky serializace vyjádřit výslovný souhlas, takže budete muset přidat **DataMember** atributy vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="2afa3-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="2afa3-233">Nyní vytvoří formátovací modul XML, podobně jako následující:</span><span class="sxs-lookup"><span data-stu-id="2afa3-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="2afa3-234">Pokud chcete se vyhnout atributy v třídě modelu, existuje další možnost: Vytvořit nový typ konkrétní **DataContractSerializer** instance a nastavte *preserveObjectReferences* k **true** v konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="2afa3-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="2afa3-235">Nastavte tuto instanci jako serializátor-type na formátovací modul typu média XML.</span><span class="sxs-lookup"><span data-stu-id="2afa3-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="2afa3-236">Následující kód ukazuje, jak to provést toto:</span><span class="sxs-lookup"><span data-stu-id="2afa3-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="2afa3-237">Testování serializaci objektů</span><span class="sxs-lookup"><span data-stu-id="2afa3-237">Testing Object Serialization</span></span>

<span data-ttu-id="2afa3-238">Při návrhu webového rozhraní API, je užitečné pro testování, jak bude serializována datové objekty.</span><span class="sxs-lookup"><span data-stu-id="2afa3-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="2afa3-239">Můžete to provést bez vytvoření kontroleru nebo vyvolání akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="2afa3-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
