---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Serializace JSON a XML ve ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Popisuje formátovací moduly JSON a XML ve webovém rozhraní API ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557468"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="075f0-103">JSON a serializace XML ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="075f0-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="075f0-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="075f0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="075f0-105">Tento článek popisuje formátování JSON a XML ve webovém rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="075f0-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="075f0-106">Ve webovém rozhraní API ASP.NET je *modul formátování mediálního typu* objekt, který může:</span><span class="sxs-lookup"><span data-stu-id="075f0-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="075f0-107">Čtení objektů CLR z těla zprávy HTTP</span><span class="sxs-lookup"><span data-stu-id="075f0-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="075f0-108">Zápis objektů CLR do těla zprávy HTTP</span><span class="sxs-lookup"><span data-stu-id="075f0-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="075f0-109">Webové rozhraní API poskytuje formátovací moduly typu média pro JSON i XML.</span><span class="sxs-lookup"><span data-stu-id="075f0-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="075f0-110">Rozhraní vloží tyto formátovací moduly do kanálu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="075f0-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="075f0-111">Klienti můžou v hlavičce Accept požadavku HTTP požadovat buď JSON, nebo XML.</span><span class="sxs-lookup"><span data-stu-id="075f0-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="075f0-112">Obsah</span><span class="sxs-lookup"><span data-stu-id="075f0-112">Contents</span></span>

- [<span data-ttu-id="075f0-113">Formátovací modul typu médium JSON</span><span class="sxs-lookup"><span data-stu-id="075f0-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="075f0-114">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="075f0-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="075f0-115">Datech</span><span class="sxs-lookup"><span data-stu-id="075f0-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="075f0-116">Odsazení</span><span class="sxs-lookup"><span data-stu-id="075f0-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="075f0-117">Ve stylu CamelCase velká a malá písmena</span><span class="sxs-lookup"><span data-stu-id="075f0-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="075f0-118">Anonymní a slabě typované objekty</span><span class="sxs-lookup"><span data-stu-id="075f0-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="075f0-119">Formátovací modul XML typu média</span><span class="sxs-lookup"><span data-stu-id="075f0-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="075f0-120">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="075f0-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="075f0-121">Datech</span><span class="sxs-lookup"><span data-stu-id="075f0-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="075f0-122">Odsazení</span><span class="sxs-lookup"><span data-stu-id="075f0-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="075f0-123">Nastavení serializátorů XML pro jednotlivé typy</span><span class="sxs-lookup"><span data-stu-id="075f0-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="075f0-124">Odebrání formátovacího modulu JSON nebo XML</span><span class="sxs-lookup"><span data-stu-id="075f0-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="075f0-125">Zpracování cyklických odkazů na objekty</span><span class="sxs-lookup"><span data-stu-id="075f0-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="075f0-126">Testování serializace objektu</span><span class="sxs-lookup"><span data-stu-id="075f0-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="075f0-127">Formátovací modul typu médium JSON</span><span class="sxs-lookup"><span data-stu-id="075f0-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="075f0-128">Formátování JSON je poskytováno třídou **JsonMediaTypeFormatter** .</span><span class="sxs-lookup"><span data-stu-id="075f0-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="075f0-129">Ve výchozím nastavení používá **JsonMediaTypeFormatter** k provedení serializaci knihovnu [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json) .</span><span class="sxs-lookup"><span data-stu-id="075f0-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="075f0-130">Json.NET je open source projekt třetí strany.</span><span class="sxs-lookup"><span data-stu-id="075f0-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="075f0-131">Pokud dáváte přednost, můžete třídu **JsonMediaTypeFormatter** nakonfigurovat tak, aby používala **DataContractJsonSerializer** namísto JSON.NET.</span><span class="sxs-lookup"><span data-stu-id="075f0-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="075f0-132">Provedete to tak, že nastavíte vlastnost **UseDataContractJsonSerializer** na **hodnotu true**:</span><span class="sxs-lookup"><span data-stu-id="075f0-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="075f0-133">Serializace JSON</span><span class="sxs-lookup"><span data-stu-id="075f0-133">JSON Serialization</span></span>

<span data-ttu-id="075f0-134">Tato část popisuje některá konkrétní chování formátovacího modulu JSON s použitím výchozího serializátoru [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json) .</span><span class="sxs-lookup"><span data-stu-id="075f0-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="075f0-135">Nejedná se o komplexní dokumentaci knihovny Json.NET. Další informace najdete v [dokumentaci k JSON.NET](http://james.newtonking.com/projects/json/help/).</span><span class="sxs-lookup"><span data-stu-id="075f0-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="075f0-136">Co získám serializaci?</span><span class="sxs-lookup"><span data-stu-id="075f0-136">What Gets Serialized?</span></span>

<span data-ttu-id="075f0-137">Ve výchozím nastavení jsou všechny veřejné vlastnosti a pole zahrnuté v serializovaném formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="075f0-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="075f0-138">Chcete-li vypustit vlastnost nebo pole, seupravte je pomocí atributu **JsonIgnore** .</span><span class="sxs-lookup"><span data-stu-id="075f0-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="075f0-139">Pokud dáváte přednost &quot;výslovný&quot; přístup, seřazením třídy pomocí atributu **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="075f0-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="075f0-140">Pokud je tento atribut přítomen, jsou členy ignorovány, pokud nemají **DataMember**.</span><span class="sxs-lookup"><span data-stu-id="075f0-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="075f0-141">Můžete také použít **DataMember** k serializaci privátních členů.</span><span class="sxs-lookup"><span data-stu-id="075f0-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="075f0-142">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="075f0-142">Read-Only Properties</span></span>

<span data-ttu-id="075f0-143">Ve výchozím nastavení jsou serializovány vlastnosti jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="075f0-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="075f0-144">Kalendářní data</span><span class="sxs-lookup"><span data-stu-id="075f0-144">Dates</span></span>

<span data-ttu-id="075f0-145">Ve výchozím nastavení Json.NET zapisuje data ve formátu [ISO 8601](http://www.w3.org/TR/NOTE-datetime) .</span><span class="sxs-lookup"><span data-stu-id="075f0-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="075f0-146">Data v UTC (koordinovaný světový čas) se napíší příponou "Z".</span><span class="sxs-lookup"><span data-stu-id="075f0-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="075f0-147">Kalendářní data v místním čase zahrnují posun časového pásma.</span><span class="sxs-lookup"><span data-stu-id="075f0-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="075f0-148">Příklad:</span><span class="sxs-lookup"><span data-stu-id="075f0-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="075f0-149">Ve výchozím nastavení Json.NET zachovává časové pásmo.</span><span class="sxs-lookup"><span data-stu-id="075f0-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="075f0-150">To můžete přepsat nastavením vlastnosti DateTimeZoneHandling:</span><span class="sxs-lookup"><span data-stu-id="075f0-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="075f0-151">Pokud raději použijete [formát data JSON od společnosti Microsoft](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) místo ISO 8601, nastavte vlastnost **DateFormatHandling** v nastavení serializátoru:</span><span class="sxs-lookup"><span data-stu-id="075f0-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="075f0-152">Odsazení</span><span class="sxs-lookup"><span data-stu-id="075f0-152">Indenting</span></span>

<span data-ttu-id="075f0-153">Pro zápis odsazeného JSON nastavte nastavení **formátování** na **formátování. odsazené**:</span><span class="sxs-lookup"><span data-stu-id="075f0-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="075f0-154">Ve stylu CamelCase velká a malá písmena</span><span class="sxs-lookup"><span data-stu-id="075f0-154">Camel Casing</span></span>

<span data-ttu-id="075f0-155">Pro zápis názvů vlastností JSON s ve stylu camelcasemi velkými písmeny bez změny datového modelu nastavte **CamelCasePropertyNamesContractResolver** na serializátoru:</span><span class="sxs-lookup"><span data-stu-id="075f0-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="075f0-156">Anonymní a slabě typované objekty</span><span class="sxs-lookup"><span data-stu-id="075f0-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="075f0-157">Metoda akce může vracet anonymní objekt a serializovat ho do formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="075f0-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="075f0-158">Příklad:</span><span class="sxs-lookup"><span data-stu-id="075f0-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="075f0-159">Tělo zprávy odpovědi bude obsahovat následující kód JSON:</span><span class="sxs-lookup"><span data-stu-id="075f0-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="075f0-160">Pokud vaše webové rozhraní API obdrží volně strukturované objekty JSON od klientů, můžete text žádosti deserializovat do typu **Newtonsoft. JSON. Linq. JObject** .</span><span class="sxs-lookup"><span data-stu-id="075f0-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="075f0-161">Je ale obvykle lepší používat datové objekty silného typu.</span><span class="sxs-lookup"><span data-stu-id="075f0-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="075f0-162">Pak nemusíte data analyzovat sami a získáte výhody ověřování modelu.</span><span class="sxs-lookup"><span data-stu-id="075f0-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="075f0-163">Serializátor XML nepodporuje anonymní typy nebo **JObject** instance.</span><span class="sxs-lookup"><span data-stu-id="075f0-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="075f0-164">Pokud používáte tyto funkce pro data JSON, měli byste z kanálu odebrat formátovací modul XML, jak je popsáno dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="075f0-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="075f0-165">Formátovací modul XML typu média</span><span class="sxs-lookup"><span data-stu-id="075f0-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="075f0-166">Formátování XML je zajištěno třídou **XmlMediaTypeFormatter** .</span><span class="sxs-lookup"><span data-stu-id="075f0-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="075f0-167">Ve výchozím nastavení **XmlMediaTypeFormatter** používá třídu **DataContractSerializer** k provedení serializace.</span><span class="sxs-lookup"><span data-stu-id="075f0-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="075f0-168">Pokud chcete, můžete **XmlMediaTypeFormatter** nakonfigurovat tak, aby používal **XmlSerializer** namísto **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="075f0-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="075f0-169">Provedete to tak, že nastavíte vlastnost **useXmlSerializer** na **hodnotu true**:</span><span class="sxs-lookup"><span data-stu-id="075f0-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="075f0-170">Třída **XmlSerializer** podporuje užší sadu typů než **DataContractSerializer**, ale poskytuje větší kontrolu nad výsledným XML.</span><span class="sxs-lookup"><span data-stu-id="075f0-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="075f0-171">Pokud potřebujete odpovídat existujícímu schématu XML, zvažte použití **XmlSerializer** .</span><span class="sxs-lookup"><span data-stu-id="075f0-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="075f0-172">Serializace XML</span><span class="sxs-lookup"><span data-stu-id="075f0-172">XML Serialization</span></span>

<span data-ttu-id="075f0-173">Tato část popisuje některá konkrétní chování formátovacího modulu XML s použitím výchozí třídy **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="075f0-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="075f0-174">Ve výchozím nastavení se třída DataContractSerializer chová takto:</span><span class="sxs-lookup"><span data-stu-id="075f0-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="075f0-175">Všechny veřejné vlastnosti pro čtení i zápis a pole jsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="075f0-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="075f0-176">Chcete-li vypustit vlastnost nebo pole, seupravte je pomocí atributu **IgnoreDataMember** .</span><span class="sxs-lookup"><span data-stu-id="075f0-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="075f0-177">Soukromé a chráněné členy nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="075f0-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="075f0-178">Vlastnosti jen pro čtení nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="075f0-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="075f0-179">(Obsah vlastnosti kolekce jen pro čtení je však serializován.)</span><span class="sxs-lookup"><span data-stu-id="075f0-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="075f0-180">Názvy tříd a členů jsou zapsány v XML přesně tak, jak jsou uvedeny v deklaraci třídy.</span><span class="sxs-lookup"><span data-stu-id="075f0-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="075f0-181">Použije se výchozí obor názvů XML.</span><span class="sxs-lookup"><span data-stu-id="075f0-181">A default XML namespace is used.</span></span>

<span data-ttu-id="075f0-182">Pokud potřebujete větší kontrolu nad serializací, můžete třídu vytřídit pomocí atributu **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="075f0-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="075f0-183">Pokud je tento atribut přítomen, třída je serializována následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="075f0-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="075f0-184">&quot;opt&quot; přístup: vlastnosti a pole nejsou ve výchozím nastavení serializovány.</span><span class="sxs-lookup"><span data-stu-id="075f0-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="075f0-185">Chcete-li serializovat vlastnost nebo pole, seupravte je pomocí atributu **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="075f0-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="075f0-186">Chcete-li serializovat soukromý nebo chráněný člen, jej seupravte pomocí atributu **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="075f0-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="075f0-187">Vlastnosti jen pro čtení nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="075f0-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="075f0-188">Chcete-li změnit způsob, jakým se v XML zobrazí název třídy, nastavte parametr *Name* v atributu **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="075f0-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="075f0-189">Chcete-li změnit způsob, jakým se název člena zobrazí v XML, nastavte parametr *Name* v atributu **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="075f0-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="075f0-190">Chcete-li změnit obor názvů XML, nastavte parametr *Namespace* ve třídě **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="075f0-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="075f0-191">Vlastnosti jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="075f0-191">Read-Only Properties</span></span>

<span data-ttu-id="075f0-192">Vlastnosti jen pro čtení nejsou serializovány.</span><span class="sxs-lookup"><span data-stu-id="075f0-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="075f0-193">Pokud má vlastnost jen pro čtení záložní privátní pole, můžete označit soukromé pole atributem **DataMember** .</span><span class="sxs-lookup"><span data-stu-id="075f0-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="075f0-194">Tento přístup vyžaduje pro třídu atribut **DataContract** .</span><span class="sxs-lookup"><span data-stu-id="075f0-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="075f0-195">Kalendářní data</span><span class="sxs-lookup"><span data-stu-id="075f0-195">Dates</span></span>

<span data-ttu-id="075f0-196">Data jsou zapsána ve formátu ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="075f0-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="075f0-197">Například &quot;2012-05-23T20:21:37.9116538 Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="075f0-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="075f0-198">Odsazení</span><span class="sxs-lookup"><span data-stu-id="075f0-198">Indenting</span></span>

<span data-ttu-id="075f0-199">Chcete-li zapsat odsazený kód XML, nastavte vlastnost **odsazení** na **hodnotu true**:</span><span class="sxs-lookup"><span data-stu-id="075f0-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="075f0-200">Nastavení serializátorů XML pro jednotlivé typy</span><span class="sxs-lookup"><span data-stu-id="075f0-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="075f0-201">Můžete nastavit různé serializace XML pro různé typy CLR.</span><span class="sxs-lookup"><span data-stu-id="075f0-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="075f0-202">Například můžete mít konkrétní datový objekt, který vyžaduje **XmlSerializer** pro zpětnou kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="075f0-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="075f0-203">Pro tento objekt lze použít **XmlSerializer** a nadále používat **DataContractSerializer** pro jiné typy.</span><span class="sxs-lookup"><span data-stu-id="075f0-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="075f0-204">Chcete-li nastavit serializátor XML pro konkrétní typ, zavolejte **SetSerializer**.</span><span class="sxs-lookup"><span data-stu-id="075f0-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="075f0-205">Můžete určit **XmlSerializer** nebo libovolný objekt, který je odvozen z **XmlObjectSerializer**.</span><span class="sxs-lookup"><span data-stu-id="075f0-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="075f0-206">Odebrání formátovacího modulu JSON nebo XML</span><span class="sxs-lookup"><span data-stu-id="075f0-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="075f0-207">Můžete odebrat formátovací modul JSON nebo formátovací modul XML ze seznamu formátovacích modulů, pokud je nechcete používat.</span><span class="sxs-lookup"><span data-stu-id="075f0-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="075f0-208">Hlavní důvody k tomu jsou tyto:</span><span class="sxs-lookup"><span data-stu-id="075f0-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="075f0-209">Omezení odezvy webového rozhraní API na konkrétní typ média.</span><span class="sxs-lookup"><span data-stu-id="075f0-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="075f0-210">Například se můžete rozhodnout podporovat pouze odpovědi JSON a odstranit formátovací modul XML.</span><span class="sxs-lookup"><span data-stu-id="075f0-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="075f0-211">Chcete-li výchozí formátovací modul nahradit vlastním formátovacím modulem.</span><span class="sxs-lookup"><span data-stu-id="075f0-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="075f0-212">Můžete například nahradit formátovací modul JSON vlastní implementací formátovacího modulu JSON.</span><span class="sxs-lookup"><span data-stu-id="075f0-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="075f0-213">Následující kód ukazuje, jak odebrat výchozí formátovací moduly.</span><span class="sxs-lookup"><span data-stu-id="075f0-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="075f0-214">Tuto metodu zavolejte z vaší **aplikace\_metoda Start** definované v Global. asax.</span><span class="sxs-lookup"><span data-stu-id="075f0-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="075f0-215">Zpracování cyklických odkazů na objekty</span><span class="sxs-lookup"><span data-stu-id="075f0-215">Handling Circular Object References</span></span>

<span data-ttu-id="075f0-216">Ve výchozím nastavení zapisují formátovací moduly JSON a XML všechny objekty jako hodnoty.</span><span class="sxs-lookup"><span data-stu-id="075f0-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="075f0-217">Pokud dvě vlastnosti odkazují na stejný objekt, nebo pokud je stejný objekt v kolekci dvakrát zobrazen, formátovací modul tento objekt pozastaví dvakrát.</span><span class="sxs-lookup"><span data-stu-id="075f0-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="075f0-218">Jedná se o konkrétní problém, pokud graf objektu obsahuje cykly, protože serializátor vyvolá výjimku, když detekuje smyčku v grafu.</span><span class="sxs-lookup"><span data-stu-id="075f0-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="075f0-219">Vezměte v úvahu následující objektové modely a kontroléry.</span><span class="sxs-lookup"><span data-stu-id="075f0-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="075f0-220">Vyvolání této akce způsobí, že formátovací modul vyvolal výjimku, která se přeloží na odpověď na stavový kód 500 (interní chyba serveru) na klienta.</span><span class="sxs-lookup"><span data-stu-id="075f0-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="075f0-221">Chcete-li zachovat odkazy na objekty ve formátu JSON, přidejte následující kód do metody **Application\_Start** v souboru Global. asax:</span><span class="sxs-lookup"><span data-stu-id="075f0-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="075f0-222">Nyní akce kontroleru vrátí JSON, která vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="075f0-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="075f0-223">Všimněte si, že serializátor přidá vlastnost &quot;$id&quot; do obou objektů.</span><span class="sxs-lookup"><span data-stu-id="075f0-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="075f0-224">Také zjistí, že vlastnost zaměstnanec. Department vytvoří smyčku, takže nahradí hodnotu odkazem na objekt: {&quot;$ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="075f0-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="075f0-225">Odkazy na objekty nejsou ve formátu JSON standardní.</span><span class="sxs-lookup"><span data-stu-id="075f0-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="075f0-226">Před použitím této funkce zvažte, zda budou vaši klienti moci analyzovat výsledky.</span><span class="sxs-lookup"><span data-stu-id="075f0-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="075f0-227">Může být vhodnější jednoduše odebrat cykly z grafu.</span><span class="sxs-lookup"><span data-stu-id="075f0-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="075f0-228">Například odkaz od zaměstnance zpátky do oddělení není v tomto příkladu skutečně potřeba.</span><span class="sxs-lookup"><span data-stu-id="075f0-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="075f0-229">Chcete-li zachovat odkazy na objekty v XML, máte dvě možnosti.</span><span class="sxs-lookup"><span data-stu-id="075f0-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="075f0-230">Jednodušší možností je přidat `[DataContract(IsReference=true)]` do třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="075f0-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="075f0-231">Parametr *IsReference* povoluje odkazy na objekty.</span><span class="sxs-lookup"><span data-stu-id="075f0-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="075f0-232">Pamatujte, že **DataContract** zpřístupňuje serializaci, takže budete muset také přidat atributy **DataMember** do vlastností:</span><span class="sxs-lookup"><span data-stu-id="075f0-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="075f0-233">Modul formátování nyní vytvoří jazyk XML podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="075f0-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="075f0-234">Pokud se chcete vyhnout atributům třídy modelu, existuje další možnost: Vytvořte novou instanci **DataContractSerializer** specifickou pro typ a nastavte *preserveObjectReferences* na **hodnotu true** v konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="075f0-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="075f0-235">Pak nastavte tuto instanci jako serializátor pro typ ve formátovacím modulu XML typu médium.</span><span class="sxs-lookup"><span data-stu-id="075f0-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="075f0-236">Následující kód ukazuje, jak to provést:</span><span class="sxs-lookup"><span data-stu-id="075f0-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="075f0-237">Testování serializace objektu</span><span class="sxs-lookup"><span data-stu-id="075f0-237">Testing Object Serialization</span></span>

<span data-ttu-id="075f0-238">Při návrhu webového rozhraní API je vhodné otestovat, jak budou datové objekty serializovány.</span><span class="sxs-lookup"><span data-stu-id="075f0-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="075f0-239">Můžete to udělat bez vytvoření kontroleru nebo vyvolání akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="075f0-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
