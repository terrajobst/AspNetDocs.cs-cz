---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: Vyjednávání obsahu v ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Popisuje, jak webové rozhraní API ASP.NET implementuje vyjednávání obsahu protokolu HTTP pro ASP.NET 4. x.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622267"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="3c566-103">Vyjednávání obsahu ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3c566-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="3c566-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3c566-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3c566-105">Tento článek popisuje, jak webové rozhraní API ASP.NET implementuje vyjednávání obsahu pro ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="3c566-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="3c566-106">Specifikace HTTP (RFC 2616) definuje vyjednávání obsahu jako "proces výběru nejlepší reprezentace pro danou odpověď, pokud jsou k dispozici více reprezentují."</span><span class="sxs-lookup"><span data-stu-id="3c566-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="3c566-107">Primárním mechanismem pro vyjednávání obsahu v HTTP jsou tyto hlavičky požadavků:</span><span class="sxs-lookup"><span data-stu-id="3c566-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="3c566-108">**Přijmout:** Které typy médií jsou přijatelné pro odpověď, jako je například Application/JSON, Application/XML nebo vlastní typ média, jako je například &quot;application/vnd. example + XML&quot;</span><span class="sxs-lookup"><span data-stu-id="3c566-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="3c566-109">**Přijmout – charset:** Které znakové sady jsou přijatelné, například UTF-8 nebo ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="3c566-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="3c566-110">**Přijmout – kódování:** Které kódování obsahu jsou přijatelné, například gzip.</span><span class="sxs-lookup"><span data-stu-id="3c566-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="3c566-111">**Přijmout – jazyk:** Preferovaný přirozený jazyk, například "en-US".</span><span class="sxs-lookup"><span data-stu-id="3c566-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="3c566-112">Server se také může podívat na jiné části požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c566-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="3c566-113">Pokud například požadavek obsahuje hlavičku X-with, která označuje požadavek AJAX, server může být ve výchozím nastavení JSON, pokud není k dispozici hlavička Accept.</span><span class="sxs-lookup"><span data-stu-id="3c566-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="3c566-114">V tomto článku se podíváme na to, jak webové rozhraní API používá hlavičky Accept a Accept-Charset.</span><span class="sxs-lookup"><span data-stu-id="3c566-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="3c566-115">(V současnosti není k dispozici žádná integrovaná podpora pro Accept-Encoding nebo Accept-Language.)</span><span class="sxs-lookup"><span data-stu-id="3c566-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="3c566-116">Serializace</span><span class="sxs-lookup"><span data-stu-id="3c566-116">Serialization</span></span>

<span data-ttu-id="3c566-117">Pokud kontroler webového rozhraní API vrátí prostředek jako typ CLR, kanál tuto vrácenou hodnotu zavolá a zapíše ho do těla odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c566-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="3c566-118">Zvažte například následující akci kontroleru:</span><span class="sxs-lookup"><span data-stu-id="3c566-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="3c566-119">Klient může tuto žádost HTTP odeslat:</span><span class="sxs-lookup"><span data-stu-id="3c566-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="3c566-120">V reakci může server odeslat:</span><span class="sxs-lookup"><span data-stu-id="3c566-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="3c566-121">V tomto příkladu si klient vyžádal buď JSON, JavaScript, nebo "cokoli" (\*/\*).</span><span class="sxs-lookup"><span data-stu-id="3c566-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="3c566-122">Server odpověděl pomocí reprezentace JSON objektu `Product`.</span><span class="sxs-lookup"><span data-stu-id="3c566-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="3c566-123">Všimněte si, že hlavička Content-Type v odpovědi je nastavená na &quot;Application/JSON&quot;.</span><span class="sxs-lookup"><span data-stu-id="3c566-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="3c566-124">Kontroler může také vracet objekt **HttpResponseMessage** .</span><span class="sxs-lookup"><span data-stu-id="3c566-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="3c566-125">Chcete-li určit objekt CLR pro tělo odpovědi, zavolejte metodu rozšíření **CreateResponse** :</span><span class="sxs-lookup"><span data-stu-id="3c566-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="3c566-126">Tato možnost nabízí větší kontrolu nad podrobnostmi odpovědi.</span><span class="sxs-lookup"><span data-stu-id="3c566-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="3c566-127">Můžete nastavit stavový kód, přidat hlavičky HTTP a tak dále.</span><span class="sxs-lookup"><span data-stu-id="3c566-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="3c566-128">Objekt, který serializaci prostředku, se nazývá *formátovací modul média*.</span><span class="sxs-lookup"><span data-stu-id="3c566-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="3c566-129">Formátovací moduly médií jsou odvozeny od třídy **MediaTypeFormatter** .</span><span class="sxs-lookup"><span data-stu-id="3c566-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="3c566-130">Webové rozhraní API poskytuje formátovací moduly médií pro XML a JSON a můžete vytvořit vlastní formátovací moduly pro podporu jiných typů médií.</span><span class="sxs-lookup"><span data-stu-id="3c566-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="3c566-131">Informace o zápisu vlastního formátovacího modulu najdete v tématu [Formátování médií](media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="3c566-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="3c566-132">Jak funguje vyjednávání obsahu</span><span class="sxs-lookup"><span data-stu-id="3c566-132">How Content Negotiation Works</span></span>

<span data-ttu-id="3c566-133">Nejprve kanál získá službu **IContentNegotiator** z objektu **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="3c566-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="3c566-134">Také získá seznam formátovacích modulů médií z kolekce **HttpConfiguration. formátovacích** rutin.</span><span class="sxs-lookup"><span data-stu-id="3c566-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="3c566-135">Dále kanál volá **IContentNegotiator. Negotiate**a předává:</span><span class="sxs-lookup"><span data-stu-id="3c566-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="3c566-136">Typ objektu, který se má serializovat</span><span class="sxs-lookup"><span data-stu-id="3c566-136">The type of object to serialize</span></span>
- <span data-ttu-id="3c566-137">Kolekce formátovacích modulů médií</span><span class="sxs-lookup"><span data-stu-id="3c566-137">The collection of media formatters</span></span>
- <span data-ttu-id="3c566-138">Požadavek HTTP</span><span class="sxs-lookup"><span data-stu-id="3c566-138">The HTTP request</span></span>

<span data-ttu-id="3c566-139">Metoda **Negotiate** vrátí dvě části informací:</span><span class="sxs-lookup"><span data-stu-id="3c566-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="3c566-140">Který formátovací modul použít</span><span class="sxs-lookup"><span data-stu-id="3c566-140">Which formatter to use</span></span>
- <span data-ttu-id="3c566-141">Typ média pro odpověď</span><span class="sxs-lookup"><span data-stu-id="3c566-141">The media type for the response</span></span>

<span data-ttu-id="3c566-142">Pokud není nalezen žádný formátovací modul, metoda **Negotiate** vrátí **hodnotu null**a klient obdrží chybu protokolu HTTP 406 (není přijatelné).</span><span class="sxs-lookup"><span data-stu-id="3c566-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="3c566-143">Následující kód ukazuje, jak může řadič přímo vyvolat vyjednávání obsahu:</span><span class="sxs-lookup"><span data-stu-id="3c566-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="3c566-144">Tento kód je ekvivalentní k tomu, co kanál automaticky dělá.</span><span class="sxs-lookup"><span data-stu-id="3c566-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="3c566-145">Výchozí Negociační obsahu</span><span class="sxs-lookup"><span data-stu-id="3c566-145">Default Content Negotiator</span></span>

<span data-ttu-id="3c566-146">Třída **DefaultContentNegotiator** poskytuje výchozí implementaci **IContentNegotiator**.</span><span class="sxs-lookup"><span data-stu-id="3c566-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="3c566-147">Pro výběr formátovacího modulu používá několik kritérií.</span><span class="sxs-lookup"><span data-stu-id="3c566-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="3c566-148">Nejprve musí být formátovací modul schopný serializovat typ.</span><span class="sxs-lookup"><span data-stu-id="3c566-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="3c566-149">To se ověřuje voláním **MediaTypeFormatter. CanWriteType**.</span><span class="sxs-lookup"><span data-stu-id="3c566-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="3c566-150">V dalším kroku se prozkoumá vyjednávání obsahu u každého formátovacího modulu a vyhodnotí, jak dobře odpovídá požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c566-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="3c566-151">Pro vyhodnocení shody vyhledává vyjednávání obsahu dvě věci formátování:</span><span class="sxs-lookup"><span data-stu-id="3c566-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="3c566-152">Kolekce **SupportedMediaTypes** , která obsahuje seznam podporovaných typů médií.</span><span class="sxs-lookup"><span data-stu-id="3c566-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="3c566-153">Nástroj pro vyjednávání obsahu se pokusí spárovat tento seznam s hlavičkou Accept žádosti.</span><span class="sxs-lookup"><span data-stu-id="3c566-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="3c566-154">Všimněte si, že hlavička Accept může zahrnovat rozsahy.</span><span class="sxs-lookup"><span data-stu-id="3c566-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="3c566-155">Například "text/jednoduchá" je shoda pro text/\* nebo \*/\*.</span><span class="sxs-lookup"><span data-stu-id="3c566-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="3c566-156">Kolekce **MediaTypeMappings** , která obsahuje seznam objektů **MediaTypeMapping** .</span><span class="sxs-lookup"><span data-stu-id="3c566-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="3c566-157">Třída **MediaTypeMapping** poskytuje obecný způsob, jak porovnat požadavky HTTP s typy médií.</span><span class="sxs-lookup"><span data-stu-id="3c566-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="3c566-158">Například může namapovat vlastní hlavičku HTTP na konkrétní typ média.</span><span class="sxs-lookup"><span data-stu-id="3c566-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="3c566-159">Je-li k dispozici více shod, odpovídá nejvyšší faktor kvality služby WINS.</span><span class="sxs-lookup"><span data-stu-id="3c566-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="3c566-160">Příklad:</span><span class="sxs-lookup"><span data-stu-id="3c566-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="3c566-161">V tomto příkladu má Application/JSON předpokládaný faktor kvality 1,0, takže se upřednostňuje přes Application/XML.</span><span class="sxs-lookup"><span data-stu-id="3c566-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="3c566-162">Pokud se nenaleznou žádné shody, vyzkouší se kolize obsahu u typu média těla žádosti, pokud existuje.</span><span class="sxs-lookup"><span data-stu-id="3c566-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="3c566-163">Pokud například požadavek obsahuje data JSON, vyhledá Negociační modul pro obsah formátování JSON.</span><span class="sxs-lookup"><span data-stu-id="3c566-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="3c566-164">Pokud se stále neshodují, probíhají pouze první formátovací modul, který může serializovat typ.</span><span class="sxs-lookup"><span data-stu-id="3c566-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="3c566-165">Výběr kódování znaků</span><span class="sxs-lookup"><span data-stu-id="3c566-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="3c566-166">Po výběru formátovacího modulu se vybírá nejlepší kódování znaků tím, že se na formátovací modul vyhledá vlastnost **SupportedEncodings** a v žádosti se porovná s hlavičkou Accept-Charset (pokud existuje).</span><span class="sxs-lookup"><span data-stu-id="3c566-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
