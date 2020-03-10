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
# <a name="content-negotiation-in-aspnet-web-api"></a>Vyjednávání obsahu ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento článek popisuje, jak webové rozhraní API ASP.NET implementuje vyjednávání obsahu pro ASP.NET 4. x.

Specifikace HTTP (RFC 2616) definuje vyjednávání obsahu jako "proces výběru nejlepší reprezentace pro danou odpověď, pokud jsou k dispozici více reprezentují." Primárním mechanismem pro vyjednávání obsahu v HTTP jsou tyto hlavičky požadavků:

- **Přijmout:** Které typy médií jsou přijatelné pro odpověď, jako je například Application/JSON, Application/XML nebo vlastní typ média, jako je například &quot;application/vnd. example + XML&quot;
- **Přijmout – charset:** Které znakové sady jsou přijatelné, například UTF-8 nebo ISO 8859-1.
- **Přijmout – kódování:** Které kódování obsahu jsou přijatelné, například gzip.
- **Přijmout – jazyk:** Preferovaný přirozený jazyk, například "en-US".

Server se také může podívat na jiné části požadavku HTTP. Pokud například požadavek obsahuje hlavičku X-with, která označuje požadavek AJAX, server může být ve výchozím nastavení JSON, pokud není k dispozici hlavička Accept.

V tomto článku se podíváme na to, jak webové rozhraní API používá hlavičky Accept a Accept-Charset. (V současnosti není k dispozici žádná integrovaná podpora pro Accept-Encoding nebo Accept-Language.)

## <a name="serialization"></a>Serializace

Pokud kontroler webového rozhraní API vrátí prostředek jako typ CLR, kanál tuto vrácenou hodnotu zavolá a zapíše ho do těla odpovědi HTTP.

Zvažte například následující akci kontroleru:

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

Klient může tuto žádost HTTP odeslat:

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

V reakci může server odeslat:

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

V tomto příkladu si klient vyžádal buď JSON, JavaScript, nebo "cokoli" (\*/\*). Server odpověděl pomocí reprezentace JSON objektu `Product`. Všimněte si, že hlavička Content-Type v odpovědi je nastavená na &quot;Application/JSON&quot;.

Kontroler může také vracet objekt **HttpResponseMessage** . Chcete-li určit objekt CLR pro tělo odpovědi, zavolejte metodu rozšíření **CreateResponse** :

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

Tato možnost nabízí větší kontrolu nad podrobnostmi odpovědi. Můžete nastavit stavový kód, přidat hlavičky HTTP a tak dále.

Objekt, který serializaci prostředku, se nazývá *formátovací modul média*. Formátovací moduly médií jsou odvozeny od třídy **MediaTypeFormatter** . Webové rozhraní API poskytuje formátovací moduly médií pro XML a JSON a můžete vytvořit vlastní formátovací moduly pro podporu jiných typů médií. Informace o zápisu vlastního formátovacího modulu najdete v tématu [Formátování médií](media-formatters.md).

## <a name="how-content-negotiation-works"></a>Jak funguje vyjednávání obsahu

Nejprve kanál získá službu **IContentNegotiator** z objektu **HttpConfiguration** . Také získá seznam formátovacích modulů médií z kolekce **HttpConfiguration. formátovacích** rutin.

Dále kanál volá **IContentNegotiator. Negotiate**a předává:

- Typ objektu, který se má serializovat
- Kolekce formátovacích modulů médií
- Požadavek HTTP

Metoda **Negotiate** vrátí dvě části informací:

- Který formátovací modul použít
- Typ média pro odpověď

Pokud není nalezen žádný formátovací modul, metoda **Negotiate** vrátí **hodnotu null**a klient obdrží chybu protokolu HTTP 406 (není přijatelné).

Následující kód ukazuje, jak může řadič přímo vyvolat vyjednávání obsahu:

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

Tento kód je ekvivalentní k tomu, co kanál automaticky dělá.

## <a name="default-content-negotiator"></a>Výchozí Negociační obsahu

Třída **DefaultContentNegotiator** poskytuje výchozí implementaci **IContentNegotiator**. Pro výběr formátovacího modulu používá několik kritérií.

Nejprve musí být formátovací modul schopný serializovat typ. To se ověřuje voláním **MediaTypeFormatter. CanWriteType**.

V dalším kroku se prozkoumá vyjednávání obsahu u každého formátovacího modulu a vyhodnotí, jak dobře odpovídá požadavku HTTP. Pro vyhodnocení shody vyhledává vyjednávání obsahu dvě věci formátování:

- Kolekce **SupportedMediaTypes** , která obsahuje seznam podporovaných typů médií. Nástroj pro vyjednávání obsahu se pokusí spárovat tento seznam s hlavičkou Accept žádosti. Všimněte si, že hlavička Accept může zahrnovat rozsahy. Například "text/jednoduchá" je shoda pro text/\* nebo \*/\*.
- Kolekce **MediaTypeMappings** , která obsahuje seznam objektů **MediaTypeMapping** . Třída **MediaTypeMapping** poskytuje obecný způsob, jak porovnat požadavky HTTP s typy médií. Například může namapovat vlastní hlavičku HTTP na konkrétní typ média.

Je-li k dispozici více shod, odpovídá nejvyšší faktor kvality služby WINS. Příklad:

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

V tomto příkladu má Application/JSON předpokládaný faktor kvality 1,0, takže se upřednostňuje přes Application/XML.

Pokud se nenaleznou žádné shody, vyzkouší se kolize obsahu u typu média těla žádosti, pokud existuje. Pokud například požadavek obsahuje data JSON, vyhledá Negociační modul pro obsah formátování JSON.

Pokud se stále neshodují, probíhají pouze první formátovací modul, který může serializovat typ.

## <a name="selecting-a-character-encoding"></a>Výběr kódování znaků

Po výběru formátovacího modulu se vybírá nejlepší kódování znaků tím, že se na formátovací modul vyhledá vlastnost **SupportedEncodings** a v žádosti se porovná s hlavičkou Accept-Charset (pokud existuje).
