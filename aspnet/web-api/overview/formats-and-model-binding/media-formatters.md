---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: Formátovací moduly médií v ASP.NET webového rozhraní API 2 – ASP.NET 4. x
author: MikeWasson
description: Ukazuje, jak podporovat další formáty médií ve webovém rozhraní API ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557251"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="cf0d4-103">Formátovací moduly médií v ASP.NET webovém rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="cf0d4-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="cf0d4-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cf0d4-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="cf0d4-105">V tomto kurzu se dozvíte, jak ve webovém rozhraní API ASP.NET podporovat další formáty médií.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="cf0d4-106">Typy internetových médií</span><span class="sxs-lookup"><span data-stu-id="cf0d4-106">Internet Media Types</span></span>

<span data-ttu-id="cf0d4-107">Typ média, označovaný také jako typ MIME, určuje formát částí dat.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="cf0d4-108">V části HTTP typy médií popisují formát textu zprávy.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="cf0d4-109">Typ média se skládá ze dvou řetězců, typu a podtypu.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="cf0d4-110">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cf0d4-110">For example:</span></span>

- <span data-ttu-id="cf0d4-111">text/html</span><span class="sxs-lookup"><span data-stu-id="cf0d4-111">text/html</span></span>
- <span data-ttu-id="cf0d4-112">image/png</span><span class="sxs-lookup"><span data-stu-id="cf0d4-112">image/png</span></span>
- <span data-ttu-id="cf0d4-113">application/json</span><span class="sxs-lookup"><span data-stu-id="cf0d4-113">application/json</span></span>

<span data-ttu-id="cf0d4-114">V případě, že zpráva HTTP obsahuje tělo entity, určuje záhlaví Content-Type formát textu zprávy.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="cf0d4-115">Příjemce zobrazí informace o tom, jak analyzovat obsah textu zprávy.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="cf0d4-116">Například pokud odpověď HTTP obsahuje obrázek PNG, odpověď může obsahovat následující záhlaví.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="cf0d4-117">Když klient odešle zprávu s požadavkem, může obsahovat hlavičku Accept.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="cf0d4-118">Hlavička Accept označuje server, který typ média chce klient ze serveru.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="cf0d4-119">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cf0d4-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="cf0d4-120">Tato hlavička oznamuje serveru, který chce klient buď HTML, XHTML nebo XML.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="cf0d4-121">Typ média určuje, jak webové rozhraní API serializace a deserializace tělo zprávy HTTP.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="cf0d4-122">Webové rozhraní API obsahuje integrovanou podporu pro data XML, JSON, BSON a form-urlencoded. další typy médií můžete podpořit napsáním *formátovacího modulu médií*.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="cf0d4-123">Chcete-li vytvořit formátovací modul médií, odvozujte z jedné z těchto tříd:</span><span class="sxs-lookup"><span data-stu-id="cf0d4-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="cf0d4-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf0d4-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="cf0d4-125">Tato třída používá asynchronní metody čtení a zápisu.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="cf0d4-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf0d4-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="cf0d4-127">Tato třída je odvozena z **MediaTypeFormatter** , ale používá synchronní metody čtení/zápisu.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="cf0d4-128">Odvození od **BufferedMediaTypeFormatter** je jednodušší, protože není k dispozici žádný asynchronní kód, ale také to znamená, že volající vlákno může během vstupně-výstupních operací zablokovat.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="cf0d4-129">Příklad: vytvoření formátovacího modulu média sdíleného svazku clusteru</span><span class="sxs-lookup"><span data-stu-id="cf0d4-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="cf0d4-130">Následující příklad ukazuje formátovací modul typu média, který může serializovat objekt produktu do formátu hodnot oddělených čárkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="cf0d4-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="cf0d4-131">V tomto příkladu se používá typ produktu definovaný v kurzu [vytváření webového rozhraní API, které podporuje operace CRUD](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span><span class="sxs-lookup"><span data-stu-id="cf0d4-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="cf0d4-132">Tady je definice objektu produktu:</span><span class="sxs-lookup"><span data-stu-id="cf0d4-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="cf0d4-133">Chcete-li implementovat formátovací modul CSV, Definujte třídu, která je odvozena z **BufferedMediaTypeFormatter**:</span><span class="sxs-lookup"><span data-stu-id="cf0d4-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="cf0d4-134">V konstruktoru přidejte typy médií, které formátovací modul podporuje.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="cf0d4-135">V tomto příkladu formátovací modul podporuje jeden typ média &quot;text/CSV&quot;:</span><span class="sxs-lookup"><span data-stu-id="cf0d4-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="cf0d4-136">Přepište metodu **CanWriteType** a určete, které typy může formátovací modul serializovat:</span><span class="sxs-lookup"><span data-stu-id="cf0d4-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="cf0d4-137">V tomto příkladu formátovací modul může serializovat jeden `Product` objektů i kolekce objektů `Product`.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="cf0d4-138">Podobně přepište metodu **CanReadType** , aby označovala typy, které může formátovací modul deserializovat.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="cf0d4-139">V tomto příkladu formátovací modul nepodporuje deserializaci, takže metoda jednoduše vrátí **hodnotu false**.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="cf0d4-140">Nakonec přepište metodu **WriteToStream** .</span><span class="sxs-lookup"><span data-stu-id="cf0d4-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="cf0d4-141">Tato metoda zaserializace typ zápisem do datového proudu.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="cf0d4-142">Pokud formátovací modul podporuje deserializaci, přepište také metodu **ReadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="cf0d4-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="cf0d4-143">Přidání formátovacího modulu médií do kanálu webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="cf0d4-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="cf0d4-144">Chcete-li přidat formátovací modul typu média do kanálu webového rozhraní API, použijte vlastnost **formátovací** moduly v objektu **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="cf0d4-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="cf0d4-145">Kódování znaků</span><span class="sxs-lookup"><span data-stu-id="cf0d4-145">Character Encodings</span></span>

<span data-ttu-id="cf0d4-146">V případě potřeby může formátovací modul médií podporovat více kódování znaků, jako je UTF-8 nebo ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="cf0d4-147">V konstruktoru přidejte jeden nebo více typů [System. text. Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) do kolekce **SupportedEncodings** .</span><span class="sxs-lookup"><span data-stu-id="cf0d4-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="cf0d4-148">Nejprve vložte výchozí kódování.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="cf0d4-149">V metodách **WriteToStream** a **ReadFromStream** volejte [MediaTypeFormatter. SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) pro výběr upřednostňovaného kódování znaků.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="cf0d4-150">Tato metoda odpovídá hlavičkám požadavku na seznam podporovaných kódování.</span><span class="sxs-lookup"><span data-stu-id="cf0d4-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="cf0d4-151">Při čtení nebo zápisu z datového proudu použít vrácené **kódování** :</span><span class="sxs-lookup"><span data-stu-id="cf0d4-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
