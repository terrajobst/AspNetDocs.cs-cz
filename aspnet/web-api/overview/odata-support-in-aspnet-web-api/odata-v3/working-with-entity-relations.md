---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Podpora vztahů mezi entitami v OData V3 s webovým rozhraním API 2 | Microsoft Docs
author: MikeWasson
description: 'Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele. Pomocí OData můžou klienti přejít přes...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600316"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a>Podpora vztahů mezi entitami v OData V3 pomocí webového rozhraní API 2

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele. Pomocí OData můžou klienti přejít na vztahy mezi entitami. Pro daný produkt můžete najít dodavatele. Můžete také vytvořit nebo odebrat relace. Můžete například nastavit dodavatele produktu.
> 
> V tomto kurzu se dozvíte, jak tyto operace podporovat v ASP.NET webovém rozhraní API. Kurz sestaví na kurzu [Vytvoření koncového bodu OData V3 pomocí webového rozhraní API 2](creating-an-odata-endpoint.md).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové rozhraní API 2
> - OData verze 3
> - Entity Framework 6

## <a name="add-a-supplier-entity"></a>Přidat entitu dodavatele

Nejdřív musíme do našeho informačního kanálu OData přidat nový typ entity. Přidáme třídu `Supplier`.

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

Tato třída používá řetězec pro klíč entity. V praxi může být méně častější než použití celočíselného klíče. Je ale vhodné vidět, jak OData zpracovává jiné typy klíčů Kromě celých čísel.

V dalším kroku vytvoříme relaci přidáním vlastnosti `Supplier` do `Product` třídy:

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

Přidejte novou **negenerickými** do třídy `ProductServiceContext`, aby Entity Framework v databázi zahrnovala tabulku `Supplier`.

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

Do WebApiConfig.cs přidejte do modelu EDM entitu "dodavatelé":

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a>Navigační vlastnosti

Pokud chcete získat dodavatele pro určitý produkt, klient odešle požadavek GET:

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

Zde je pro typ `Product` navigační vlastnost "dodavatel". V tomto případě `Supplier` odkazuje na jednu položku, ale navigační vlastnost může také vracet kolekci (vztah 1: n nebo m:n).

Pro podporu tohoto požadavku přidejte následující metodu do třídy `ProductsController`:

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

Parametr *Key* je klíč produktu. Metoda vrátí související entitu&#8212;v tomto případě instance `Supplier`. Název metody a název parametru jsou důležité. Obecně platí, že pokud je navigační vlastnost pojmenována "X", je nutné přidat metodu s názvem "GetX". Metoda musí přijmout parametr s názvem "*Key*", který odpovídá datovému typu nadřazeného klíče.

Je také důležité zahrnout do parametru *Key* atribut **[FromOdataUri]** . Tento atribut oznamuje webovému rozhraní API použití pravidel syntaxe OData při analýze klíče z identifikátoru URI požadavku.

## <a name="creating-and-deleting-links"></a>Vytváření a odstraňování odkazů

OData podporuje vytváření nebo odebírání vztahů mezi dvěma entitami. V terminologii OData je vztah "odkaz". Každý odkaz má identifikátor URI s formulářem *entity*/$Links/*entity*. Například odkaz z produktu na dodavatel vypadá takto:

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

Chcete-li vytvořit nový odkaz, klient odešle požadavek POST do identifikátoru URI odkazu. Tělo požadavku je identifikátor URI cílové entity. Předpokládejme například, že je k dispozici dodavatel s klíčem "CTSO". Pokud chcete vytvořit odkaz z "Product (1)" na "dodavatel (' CTSO ')", klient odešle požadavek podobný následujícímu:

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

Chcete-li odstranit odkaz, klient pošle požadavek na odstranění identifikátoru URI odkazu.

**Vytváření odkazů**

Chcete-li povolit klientovi vytváření odkazů na dodavatele produktů, přidejte následující kód do třídy `ProductsController`:

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

Tato metoda přijímá tři parametry:

- *klíč*: klíč k nadřazené entitě (produkt)
- *navigationProperty*: název vlastnosti navigace. V tomto příkladu je jedinou platnou navigační vlastností "dodavatel".
- *odkaz*: identifikátor URI OData související entity. Tato hodnota je pořízena z textu žádosti. Identifikátor URI odkazu může být například "`http://localhost/odata/Suppliers('CTSO')`, což znamená dodavatel s ID =" CTSO ".

Metoda používá odkaz k vyhledání dodavatele. Pokud je nalezen shodný dodavatel, metoda nastaví vlastnost `Product.Supplier` a uloží výsledek do databáze.

Závažná součást analyzuje identifikátor URI odkazu. V podstatě potřebujete simulovat výsledek odeslání žádosti o získání na tento identifikátor URI. Následující pomocná metoda ukazuje, jak to provést. Metoda vyvolá proces směrování webového rozhraní API a vrátí zpět instanci **ODataPath** , která představuje analyzovanou cestu OData. U identifikátoru URI odkazu by měl být jeden z segmentů klíč entity. (Pokud ne, klient odeslal chybný identifikátor URI.)

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

**Odstraňování odkazů**

Chcete-li odstranit odkaz, přidejte následující kód do třídy `ProductsController`:

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

V tomto příkladu je navigační vlastnost jedinou entitou `Supplier`. Pokud je navigační vlastnost kolekce, identifikátor URI pro odstranění odkazu musí obsahovat klíč pro související entitu. Příklad:

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

Tato žádost odebere objednávku 1 od zákazníka 1. V takovém případě bude mít metoda DeleteLink fungují následující signaturu:

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

Parametr *relatedKey* poskytuje klíč pro související entitu. Takže v metodě `DeleteLink` vyhledejte primární entitu pomocí parametru *Key* , vyhledejte související entitu pomocí parametru *relatedKey* a pak odeberte přidružení. V závislosti na datovém modelu možná budete muset implementovat obě verze `DeleteLink`. Webové rozhraní API bude volat správnou verzi na základě identifikátoru URI požadavku.
