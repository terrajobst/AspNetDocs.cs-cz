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
# <a name="media-formatters-in-aspnet-web-api-2"></a>Formátovací moduly médií v ASP.NET webovém rozhraní API 2

o [Jan Wasson](https://github.com/MikeWasson)

V tomto kurzu se dozvíte, jak ve webovém rozhraní API ASP.NET podporovat další formáty médií.

## <a name="internet-media-types"></a>Typy internetových médií

Typ média, označovaný také jako typ MIME, určuje formát částí dat. V části HTTP typy médií popisují formát textu zprávy. Typ média se skládá ze dvou řetězců, typu a podtypu. Příklad:

- text/html
- image/png
- application/json

V případě, že zpráva HTTP obsahuje tělo entity, určuje záhlaví Content-Type formát textu zprávy. Příjemce zobrazí informace o tom, jak analyzovat obsah textu zprávy.

Například pokud odpověď HTTP obsahuje obrázek PNG, odpověď může obsahovat následující záhlaví.

[!code-console[Main](media-formatters/samples/sample1.cmd)]

Když klient odešle zprávu s požadavkem, může obsahovat hlavičku Accept. Hlavička Accept označuje server, který typ média chce klient ze serveru. Příklad:

[!code-console[Main](media-formatters/samples/sample2.cmd)]

Tato hlavička oznamuje serveru, který chce klient buď HTML, XHTML nebo XML.

Typ média určuje, jak webové rozhraní API serializace a deserializace tělo zprávy HTTP. Webové rozhraní API obsahuje integrovanou podporu pro data XML, JSON, BSON a form-urlencoded. další typy médií můžete podpořit napsáním *formátovacího modulu médií*.

Chcete-li vytvořit formátovací modul médií, odvozujte z jedné z těchto tříd:

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx). Tato třída používá asynchronní metody čtení a zápisu.
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx). Tato třída je odvozena z **MediaTypeFormatter** , ale používá synchronní metody čtení/zápisu.

Odvození od **BufferedMediaTypeFormatter** je jednodušší, protože není k dispozici žádný asynchronní kód, ale také to znamená, že volající vlákno může během vstupně-výstupních operací zablokovat.

## <a name="example-creating-a-csv-media-formatter"></a>Příklad: vytvoření formátovacího modulu média sdíleného svazku clusteru

Následující příklad ukazuje formátovací modul typu média, který může serializovat objekt produktu do formátu hodnot oddělených čárkami (CSV). V tomto příkladu se používá typ produktu definovaný v kurzu [vytváření webového rozhraní API, které podporuje operace CRUD](../older-versions/creating-a-web-api-that-supports-crud-operations.md). Tady je definice objektu produktu:

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

Chcete-li implementovat formátovací modul CSV, Definujte třídu, která je odvozena z **BufferedMediaTypeFormatter**:

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

V konstruktoru přidejte typy médií, které formátovací modul podporuje. V tomto příkladu formátovací modul podporuje jeden typ média &quot;text/CSV&quot;:

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

Přepište metodu **CanWriteType** a určete, které typy může formátovací modul serializovat:

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

V tomto příkladu formátovací modul může serializovat jeden `Product` objektů i kolekce objektů `Product`.

Podobně přepište metodu **CanReadType** , aby označovala typy, které může formátovací modul deserializovat. V tomto příkladu formátovací modul nepodporuje deserializaci, takže metoda jednoduše vrátí **hodnotu false**.

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

Nakonec přepište metodu **WriteToStream** . Tato metoda zaserializace typ zápisem do datového proudu. Pokud formátovací modul podporuje deserializaci, přepište také metodu **ReadFromStream** .

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>Přidání formátovacího modulu médií do kanálu webového rozhraní API

Chcete-li přidat formátovací modul typu média do kanálu webového rozhraní API, použijte vlastnost **formátovací** moduly v objektu **HttpConfiguration** .

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>Kódování znaků

V případě potřeby může formátovací modul médií podporovat více kódování znaků, jako je UTF-8 nebo ISO 8859-1.

V konstruktoru přidejte jeden nebo více typů [System. text. Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) do kolekce **SupportedEncodings** . Nejprve vložte výchozí kódování.

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

V metodách **WriteToStream** a **ReadFromStream** volejte [MediaTypeFormatter. SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) pro výběr upřednostňovaného kódování znaků. Tato metoda odpovídá hlavičkám požadavku na seznam podporovaných kódování. Při čtení nebo zápisu z datového proudu použít vrácené **kódování** :

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
