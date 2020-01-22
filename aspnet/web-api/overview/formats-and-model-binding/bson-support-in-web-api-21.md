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
# <a name="bson-support-in-aspnet-web-api-21"></a>Podpora BSON v rozhraní ASP.NET Web API 2,1

o [Jan Wasson](https://github.com/MikeWasson)

V tomto tématu se dozvíte, jak používat BSON v řadiči webového rozhraní API (na straně serveru) a v klientské aplikaci .NET. Webové rozhraní API 2,1 zavádí podporu pro BSON. 

## <a name="what-is-bson"></a>Co je BSON?

[Bson](http://bsonspec.org/) je binární serializace formátu. "BSON" je zkratka "Binary JSON", ale BSON a JSON jsou serializovány velmi jinak. BSON je typu "JSON", protože objekty jsou reprezentovány jako páry název-hodnota, podobně jako JSON. Na rozdíl od formátu JSON jsou číselné datové typy uloženy jako bajty, nikoli řetězce.

BSON byla navržena jako odlehčená, snadná a rychlá pro kódování a dekódování.

- BSON má srovnatelné velikosti až JSON. V závislosti na datech může být datová část BSON menší nebo větší než datová část JSON. Pro serializaci binárních dat, jako je například soubor obrázku, je BSON menší než JSON, protože binární data nejsou zakódovaná ve formátu base64.
- Dokumenty BSON se snadno prohledávají, protože prvky mají předponu pole length, takže analyzátor může přeskočit prvky bez jejich dekódování.
- Kódování a dekódování jsou efektivní, protože číselné datové typy jsou uloženy jako čísla, nikoli jako řetězce.

Nativním klientům, jako jsou klientské aplikace .NET, můžou využívat BSON místo textových formátů, jako je JSON nebo XML. Pro klienty prohlížeče pravděpodobně budete chtít s JSON, protože JavaScript může přímo převést datovou část JSON.

Naštěstí webové rozhraní API využívá [vyjednávání obsahu](content-negotiation.md), takže vaše rozhraní API může podporovat oba formáty a nechat si klienta zvolit.

## <a name="enabling-bson-on-the-server"></a>Povolení BSON na serveru

V konfiguraci webového rozhraní API přidejte **BsonMediaTypeFormatter** do kolekce formátovacích souborů.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

Když teď klient požaduje "Application/bson", webové rozhraní API použije formátovací modul BSON.

Pokud chcete přidružit BSON k ostatním typům médií, přidejte je do kolekce SupportedMediaTypes. Následující kód přidá "application/vnd. contoso" do podporovaných typů médií:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>Příklad relace HTTP

V tomto příkladu použijeme následující třídu modelu a jednoduchý kontroler webového rozhraní API:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

Klient může odeslat následující požadavek HTTP:

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

Tady je odpověď:

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

Zde jsem nahradili binární data &quot;.&quot; znaky. Následující snímek obrazovky z Fiddler zobrazuje nezpracované šestnáctkové hodnoty.

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>Použití BSON s HttpClient

Klientské aplikace .NET můžou používat formátovací modul BSON s **HttpClient**. Další informace o **HttpClient**najdete v tématu [volání webového rozhraní API z klienta .NET](../advanced/calling-a-web-api-from-a-net-client.md).

Následující kód odešle požadavek GET, který přijme BSON, a poté deserializaci datové části BSON v odpovědi.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

Pro vyžádání BSON ze serveru nastavte hlavičku Accept na "Application/bson":

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

Chcete-li deserializovat tělo odpovědi, použijte **BsonMediaTypeFormatter**. Tento formátovací modul není ve výchozí kolekci formátování, takže je nutné ho zadat při čtení těla odpovědi:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

Další příklad ukazuje, jak odeslat požadavek POST, který obsahuje BSON.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

Většina tohoto kódu je stejná jako v předchozím příkladu. Ale v metodě **PostAsync** zadejte **BsonMediaTypeFormatter** jako formátovací modul:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>Serializace primitivních typů nejvyšší úrovně

Každý dokument BSON je seznam párů klíč/hodnota. Specifikace BSON nedefinuje syntaxi pro serializaci jedné nezpracované hodnoty, jako je například celé číslo nebo řetězec.

Chcete-li toto omezení obejít, **BsonMediaTypeFormatter** považuje primitivní typy za zvláštní případ. Před serializací převede hodnotu na dvojici klíč/hodnota s klíčem "value". Předpokládejme například, že váš kontroler rozhraní API vrací celé číslo:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

Před serializací se formátovací modul BSON převede na následující pár klíč/hodnota:

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

Při deserializaci, formátovací modul převede data zpět na původní hodnotu. Nicméně pokud vaše webové rozhraní API vrátí nezpracované hodnoty, budou se v takovém případě muset vycházet z klientů, kteří používají jiný analyzátor BSON. Obecně byste měli zvážit vracení strukturovaných dat místo nezpracovaných hodnot.

## <a name="additional-resources"></a>Další materiály a zdroje informací

[Ukázka BSON webového rozhraní API](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[Formátovací moduly médií](media-formatters.md)
