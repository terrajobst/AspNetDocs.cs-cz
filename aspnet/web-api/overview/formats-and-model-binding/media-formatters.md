---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: Formátovací moduly médií ve rozhraní ASP.NET Web API 2 – ASP.NET 4.x
author: MikeWasson
description: Ukazuje, jak Podpora formátů dalšího média v rozhraní ASP.NET Web API pro ASP.NET 4.x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418765"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="ec507-103">Formátovací moduly médií ve rozhraní ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="ec507-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="ec507-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ec507-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ec507-105">Tento kurz ukazuje, jak Podpora formátů dalšího média v rozhraní ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="ec507-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="ec507-106">Typy médií Internet</span><span class="sxs-lookup"><span data-stu-id="ec507-106">Internet Media Types</span></span>

<span data-ttu-id="ec507-107">Typ média, taky jako typ MIME, identifikuje formát část data.</span><span class="sxs-lookup"><span data-stu-id="ec507-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="ec507-108">V protokolu HTTP popisují typy médií formátu těla zprávy.</span><span class="sxs-lookup"><span data-stu-id="ec507-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="ec507-109">Typ média se skládá z dvou řetězců, typ a podtyp.</span><span class="sxs-lookup"><span data-stu-id="ec507-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="ec507-110">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ec507-110">For example:</span></span>

- <span data-ttu-id="ec507-111">text/html</span><span class="sxs-lookup"><span data-stu-id="ec507-111">text/html</span></span>
- <span data-ttu-id="ec507-112">Image/png</span><span class="sxs-lookup"><span data-stu-id="ec507-112">image/png</span></span>
- <span data-ttu-id="ec507-113">application/json</span><span class="sxs-lookup"><span data-stu-id="ec507-113">application/json</span></span>

<span data-ttu-id="ec507-114">Pokud zpráva HTTP obsahuje obsah entity, Hlavička Content-Type určuje formát těla zprávy.</span><span class="sxs-lookup"><span data-stu-id="ec507-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="ec507-115">To informuje příjemce, jak analyzovat obsah textu zprávy.</span><span class="sxs-lookup"><span data-stu-id="ec507-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="ec507-116">Například pokud odpověď HTTP obsahuje obrázek PNG, odpověď může obsahovat tato záhlaví.</span><span class="sxs-lookup"><span data-stu-id="ec507-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="ec507-117">Když klient odešle zprávu požadavku, může obsahovat hlavičku Accept.</span><span class="sxs-lookup"><span data-stu-id="ec507-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="ec507-118">Hlavička Accept říká, že server, klient typy médií, které chce ze serveru.</span><span class="sxs-lookup"><span data-stu-id="ec507-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="ec507-119">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ec507-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="ec507-120">Toto záhlaví říká serveru, vyžaduje klient HTML, XHTML a XML.</span><span class="sxs-lookup"><span data-stu-id="ec507-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="ec507-121">Typ média určuje, jak webové rozhraní API serializuje a deserializuje tělo zprávy HTTP.</span><span class="sxs-lookup"><span data-stu-id="ec507-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="ec507-122">Webové rozhraní API obsahuje integrovanou podporu XML, JSON, BSON a data formuláře kódovaná a může podporovat další média typy zápisem *formátovací modul médií*.</span><span class="sxs-lookup"><span data-stu-id="ec507-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="ec507-123">Pokud chcete vytvořit formátovací modul médií, odvození od některého z těchto tříd:</span><span class="sxs-lookup"><span data-stu-id="ec507-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="ec507-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec507-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="ec507-125">Tato třída používá asynchronní čtení a zápis metody.</span><span class="sxs-lookup"><span data-stu-id="ec507-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="ec507-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec507-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="ec507-127">Tato třída je odvozena z **objekt MediaTypeFormatter** , ale používá metody synchronního čtení/zápisu.</span><span class="sxs-lookup"><span data-stu-id="ec507-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="ec507-128">Odvozování z **BufferedMediaTypeFormatter** je jednodušší, protože neexistuje žádný asynchronní kód, ale také to znamená volající vlákno může přerušováno během vstupně-výstupních operací.</span><span class="sxs-lookup"><span data-stu-id="ec507-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="ec507-129">Příklad: Vytváření médií formátovacího modulu sdíleného svazku clusteru</span><span class="sxs-lookup"><span data-stu-id="ec507-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="ec507-130">Následující příklad ukazuje formátovací modul typu média, která může serializovat objekt produktu do formátu hodnot oddělených čárkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="ec507-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="ec507-131">Tento příklad používá produkt typ definovaný v tomto kurzu [této operace CRUD podporuje vytvoření webového rozhraní API](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span><span class="sxs-lookup"><span data-stu-id="ec507-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="ec507-132">Tady je definice objektu produktu:</span><span class="sxs-lookup"><span data-stu-id="ec507-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="ec507-133">Chcete-li implementovat formátovací modul sdíleného svazku clusteru, definovat třídu, která je odvozena z **BufferedMediaTypeFormatter**:</span><span class="sxs-lookup"><span data-stu-id="ec507-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="ec507-134">V konstruktoru přidejte typy médií podporovanými formátovacím podporuje.</span><span class="sxs-lookup"><span data-stu-id="ec507-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="ec507-135">V tomto příkladu podporuje formátovací modul typu média jeden &quot;text/csv&quot;:</span><span class="sxs-lookup"><span data-stu-id="ec507-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="ec507-136">Přepsat **CanWriteType** indikace toho, jakého typu formátování může serializovat:</span><span class="sxs-lookup"><span data-stu-id="ec507-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="ec507-137">V tomto příkladu může serializovat formátování jednoho `Product` objekty a kolekce `Product` objekty.</span><span class="sxs-lookup"><span data-stu-id="ec507-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="ec507-138">Podobně, přepsat **CanReadType** indikace toho, jakého typu formátování může deserializovat.</span><span class="sxs-lookup"><span data-stu-id="ec507-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="ec507-139">V tomto příkladu formátovací modul nepodporuje deserializace, takže metoda jednoduše vrací **false**.</span><span class="sxs-lookup"><span data-stu-id="ec507-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="ec507-140">Nakonec přepsání **WriteToStream** metody.</span><span class="sxs-lookup"><span data-stu-id="ec507-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="ec507-141">Tato metoda serializuje typu pomocí zápisu do datového proudu.</span><span class="sxs-lookup"><span data-stu-id="ec507-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="ec507-142">Pokud vaše formátovací modul podporuje deserializace, také přepsat **ReadFromStream** metody.</span><span class="sxs-lookup"><span data-stu-id="ec507-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="ec507-143">Přidání formátovací modul médií do kanálu webové rozhraní API</span><span class="sxs-lookup"><span data-stu-id="ec507-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="ec507-144">Chcete-li přidat typy médií formátovacího modulu do kanálu webové rozhraní API, použijte **formátovací moduly** vlastnost **HttpConfiguration** objektu.</span><span class="sxs-lookup"><span data-stu-id="ec507-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="ec507-145">Kódování znaků</span><span class="sxs-lookup"><span data-stu-id="ec507-145">Character Encodings</span></span>

<span data-ttu-id="ec507-146">Formátovací modul médií může volitelně podporovat více kódování znaků, například UTF-8 nebo ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="ec507-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="ec507-147">V konstruktoru, přidejte jeden nebo více [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) typy mají **SupportedEncodings** kolekce.</span><span class="sxs-lookup"><span data-stu-id="ec507-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="ec507-148">Dejte výchozí kódování první.</span><span class="sxs-lookup"><span data-stu-id="ec507-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="ec507-149">V **WriteToStream** a **ReadFromStream** volání metody, [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) vybrat kódování upřednostňované znak.</span><span class="sxs-lookup"><span data-stu-id="ec507-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="ec507-150">Tato metoda odpovídá záhlaví požadavku na seznam podporovaných kódování.</span><span class="sxs-lookup"><span data-stu-id="ec507-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="ec507-151">Pomocí vráceného **kódování** při čtení nebo zápisu z datového proudu:</span><span class="sxs-lookup"><span data-stu-id="ec507-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
