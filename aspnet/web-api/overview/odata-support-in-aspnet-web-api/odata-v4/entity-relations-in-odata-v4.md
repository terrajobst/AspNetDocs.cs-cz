---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: Vztahy mezi entitami v OData v4 pomocí webového rozhraní API ASP.NET 2,2 | Microsoft Docs
author: MikeWasson
description: 'Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele. Pomocí OData můžou klienti přejít přes...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598691"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>Vztahy mezi entitami v OData v4 pomocí webového rozhraní API ASP.NET 2,2

o [Jan Wasson](https://github.com/MikeWasson)

> Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele. Pomocí OData můžou klienti přejít na vztahy mezi entitami. Pro daný produkt můžete najít dodavatele. Můžete také vytvořit nebo odebrat relace. Můžete například nastavit dodavatele produktu.
>
> V tomto kurzu se dozvíte, jak podporovat tyto operace v OData v4 pomocí webového rozhraní API ASP.NET. Kurz sestaví v kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
> - Webové rozhraní API 2,1
> - OData v4
> - Visual Studio 2013 (Stáhněte si Visual Studio 2017 [tady](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - Entity Framework 6
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>Verze kurzů
>
> Informace o OData verze 3 najdete v tématu [Podpora vztahů mezi entitami v OData V3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).

## <a name="add-a-supplier-entity"></a>Přidat entitu dodavatele

> [!NOTE]
> Kurz sestaví v kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md).

Nejdřív potřebujeme související entitu. Do složky modely přidejte třídu s názvem `Supplier`.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

Přidejte vlastnost navigace do `Product` třídy:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

Přidejte do `ProductsContext` třídy novou **negenerickými** , aby Entity Framework zahrnovala tabulku dodavatelů v databázi.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

V WebApiConfig.cs přidejte sadu entit&quot; &quot;dodavatelé k modelu Entity Data Model:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>Přidat řadič dodavatelů

Přidejte třídu `SuppliersController` do složky Controllers.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

Neukazuje, jak přidat operace CRUD pro tento kontroler. Postup je stejný jako u kontroleru produktů (viz [Vytvoření koncového bodu OData v4](create-an-odata-v4-endpoint.md)).

## <a name="getting-related-entities"></a>Získávání souvisejících entit

Pokud chcete získat dodavatele pro určitý produkt, klient odešle požadavek GET:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

Pro podporu tohoto požadavku přidejte následující metodu do třídy `ProductsController`:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

Tato metoda používá výchozí konvenci pojmenování.

- Název metody: GetX, kde X je navigační vlastnost.
- Název parametru: *klíč*

Pokud budete postupovat podle těchto zásad vytváření názvů, webové rozhraní API automaticky mapuje požadavek HTTP na metodu kontroleru.

Příklad požadavku HTTP:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

Příklad odpovědi HTTP:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>Získání související kolekce

V předchozím příkladu má produkt jednoho dodavatele. Navigační vlastnost může také vracet kolekci. Následující kód získá produkty pro dodavatele:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

V tomto případě metoda vrátí **IQueryable** místo **SingleResult&lt;t&gt;**

Příklad požadavku HTTP:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

Příklad odpovědi HTTP:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>Vytvoření relace mezi entitami

OData podporuje vytváření nebo odebírání vztahů mezi dvěma stávajícími entitami. V terminologii OData v4 je vztah &quot;odkazem&quot;. (V OData V3 se vztah nazýval *propojení*. Rozdíly v protokolu nejsou pro tento kurz důležité.)

Odkaz má svůj vlastní identifikátor URI s `/Entity/NavigationProperty/$ref`formuláře. Tady je například identifikátor URI, který řeší odkaz mezi produktem a jeho dodavatelem:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

Chcete-li přidat relaci, klient pošle požadavek POST nebo PUT na tuto adresu.

- Vloží, pokud je navigační vlastnost jediná entita, například `Product.Supplier`.
- PŘÍSPĚVEK, pokud je navigační vlastnost kolekce, například `Supplier.Products`.

Tělo požadavku obsahuje identifikátor URI druhé entity ve vztahu. Tady je příklad žádosti:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

V tomto příkladu klient odešle požadavek PUT do `/Products(6)/Supplier/$ref`, což je $ref URI pro `Supplier` produktu s ID = 6. Pokud je požadavek úspěšný, odešle Server odpověď 204 (bez obsahu):

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

Zde je metoda kontroleru pro přidání vztahu k `Product`:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

Parametr *navigationProperty* určuje, který vztah má být nastaven. (Pokud je v entitě více než jedna vlastnost navigace, můžete přidat další příkazy `case`.)

Parametr *propojení* obsahuje identifikátor URI dodavatele. Webové rozhraní API automaticky analyzuje tělo žádosti a získá hodnotu pro tento parametr.

K vyhledání dodavatele potřebujeme ID (nebo klíč), které je součástí parametru *propojení* . K tomu použijte následující pomocnou metodu:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

V podstatě Tato metoda používá knihovnu OData k rozdělení cesty identifikátoru URI na segmenty, vyhledá segment, který obsahuje klíč, a převede klíč na správný typ.

## <a name="deleting-a-relationship-between-entities"></a>Odstranění relace mezi entitami

Pokud chcete odstranit relaci, klient pošle požadavek HTTP DELETE na $ref URI:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

Tady je metoda kontroleru pro odstranění vztahu mezi produktem a dodavatelem:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

V takovém případě je `Product.Supplier` &quot;1&quot; konec relace 1: n, takže můžete relaci odebrat pouze nastavením `Product.Supplier` na `null`.

V &quot;mnoho&quot; konci relace musí klient určit, kterou související entitu chcete odebrat. K tomu klient pošle identifikátor URI související entity v řetězci dotazu žádosti. Pokud například chcete odebrat "produkt 1" z "dodavatel 1":

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

Pro podporu tohoto webového rozhraní API musíme do metody `DeleteRef` zahrnout další parametr. Tady je metoda kontroleru pro odebrání produktu z relace `Supplier.Products`.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

Parametr *Key* je klíč pro dodavatele a parametr *relatedKey* je klíč, který produkt odebere ze vztahu `Products`. Všimněte si, že webové rozhraní API automaticky získá klíč z řetězce dotazu.
