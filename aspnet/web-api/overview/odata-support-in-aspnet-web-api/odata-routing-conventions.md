---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: Konvence směrování v ASP.NET Web API 2 OData-ASP.NET 4. x
author: MikeWasson
description: Popisuje konvence směrování, které webové rozhraní API 2 v ASP.NET 4. x používá pro koncové body OData.
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63df4a82cd8df92631485b2544117844cfd0ca56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614714"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a>Konvence směrování v ASP.NET webového rozhraní API 2 OData

o [Jan Wasson](https://github.com/MikeWasson)

> Tento článek popisuje konvence směrování, které webové rozhraní API 2 v ASP.NET 4. x používá pro koncové body OData.

Když webové rozhraní API načte požadavek OData, namapuje požadavek na název kontroleru a název akce. Mapování je založeno na metodě HTTP a identifikátoru URI. Například `GET /odata/Products(1)` Maps `ProductsController.GetProduct`.

V části 1 tohoto článku jsou popsány předdefinované konvence směrování OData. Tyto konvence jsou určené konkrétně pro koncové body OData a nahrazují výchozí systém směrování webového rozhraní API. (Nahrazení proběhne při volání **MapODataRoute**.)

V části 2 jsem ukazuje, jak přidat vlastní konvence směrování. Předdefinované konvence aktuálně nezahrnují celý rozsah identifikátorů URI OData, ale můžete je roztáhnout, abyste mohli zpracovávat další případy.

- [Předdefinované konvence směrování](#conventions)
- [Vlastní konvence směrování](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>Předdefinované konvence směrování

Než popíšete konvence směrování OData ve webovém rozhraní API, je užitečné pochopit identifikátory URI OData. [Identifikátor URI OData](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) se skládá z těchto:

- Kořen služby
- Cesta prostředku
- Možnosti proxy

![](odata-routing-conventions/_static/image1.png)

V případě směrování je důležitou součástí cesta prostředku. Cesta prostředku je rozdělena na segmenty. Například `/Products(1)/Supplier` má tři segmenty:

- `Products` odkazuje na sadu entit s názvem "Products".
- `1` je klíč entity, který vybere jednu entitu ze sady.
- `Supplier` je navigační vlastnost, která vybere související entitu.

Proto tato cesta vybere dodavatele produktu 1.

> [!NOTE]
> Segmenty cesty OData neodpovídají vždy segmentům identifikátoru URI. Například "1" se považuje za segment cesty.

**Názvy řadičů.** Název kontroleru je vždycky odvozený od sady entit v kořenovém adresáři cesty prostředku. Pokud je například cesta prostředku `/Products(1)/Supplier`, webové rozhraní API vyhledá kontroler s názvem `ProductsController`.

**Názvy akcí.** Názvy akcí jsou odvozeny z segmentů cesty a modelu Entity Data Model (EDM), jak je uvedeno v následujících tabulkách. V některých případech máte dvě možnosti pro název akce. Například "Get" nebo &quot;GetProducts&quot;.

**Dotazování entit**

| Žádost | Příklad identifikátoru URI | Název akce | Ukázková akce |
| --- | --- | --- | --- |
| ZÍSKAT/EntitySet | /Products | Getentityset nebo Get | GetProducts |
| ZÍSKAT/EntitySet (klíč) | /Products (1) | GetEntityType nebo Get | Getproduct |
| ZÍSKAT/EntitySet (Key)/cast | /Products (1)/Models.Book | GetEntityType nebo Get | Kniha |

Další informace najdete v tématu [Vytvoření koncového bodu OData jen pro čtení](odata-v3/creating-an-odata-endpoint.md).

**Vytváření, aktualizace a odstraňování entit**

| Žádost | Příklad identifikátoru URI | Název akce | Ukázková akce |
| --- | --- | --- | --- |
| PŘÍSPĚVEK/EntitySet | /Products | PostEntityType nebo post | PostProduct |
| PUT/EntitySet (klíč) | /Products (1) | PutEntityType nebo PUT | PutProduct |
| Vložte/EntitySet (Key)/cast | /Products (1)/Models.Book | PutEntityType nebo PUT | PutBook |
| PATCH/EntitySet (klíč) | /Products (1) | PatchEntityType nebo patch | PatchProduct |
| PATCH/EntitySet (klíč)/cast | /Products (1)/Models.Book | PatchEntityType nebo patch | PatchBook |
| DELETE/EntitySet (klíč) | /Products (1) | DeleteEntityType nebo DELETE | DeleteProduct |
| Odstranit/EntitySet (Key)/cast | /Products (1)/Models.Book | DeleteEntityType nebo DELETE | DeleteBook |

**Dotazování na vlastnost navigace**

| Žádost | Příklad identifikátoru URI | Název akce | Ukázková akce |
| --- | --- | --- | --- |
| ZÍSKAT/EntitySet (Key)/Navigation | /Products (1)/Supplier | GetNavigationFromEntityType nebo getnavigation | GetSupplierFromProduct |
| ZÍSKAT/EntitySet (Key)/cast/Navigation | /Products (1)/Models.Book/Author | GetNavigationFromEntityType nebo getnavigation | GetAuthorFromBook |

Další informace najdete v tématu [práce s relacemi entit](odata-v3/working-with-entity-relations.md).

**Vytváření a odstraňování odkazů**

| Žádost | Příklad identifikátoru URI | Název akce |
| --- | --- | --- |
| POST/EntitySet (Key)/$links/Navigation | /Products (1)/$links/Supplier | CreateLink |
| PUT/EntitySet (Key)/$links/Navigation | /Products (1)/$links/Supplier | CreateLink |
| DELETE/EntitySet (Key)/$links/Navigation | /Products (1)/$links/Supplier | DeleteLink fungují |
| DELETE/EntitySet (Key)/$links/Navigation (relatedKey) | /Products/(1)/$links/Suppliers (1) | DeleteLink fungují |

Další informace najdete v tématu [práce s relacemi entit](odata-v3/working-with-entity-relations.md).

**Vlastnosti**

*Vyžaduje webové rozhraní API 2.*

| Žádost | Příklad identifikátoru URI | Název akce | Ukázková akce |
| --- | --- | --- | --- |
| ZÍSKAT/EntitySet (Key)/Property | /Products (1)/Name | GetPropertyFromEntityType nebo GetProperty | GetNameFromProduct |
| ZÍSKAT/EntitySet (Key)/cast/Property | /Products (1)/Models.Book/Author | GetPropertyFromEntityType nebo GetProperty | GetTitleFromBook |

**Akce**

| Žádost | Příklad identifikátoru URI | Název akce | Ukázková akce |
| --- | --- | --- | --- |
| POST/EntitySet (klíč) za akci | /Products (1)/Rate | ActionNameOnEntityType nebo Action | RateOnProduct |
| POST/EntitySet (klíč)/cast/Action | /Products (1)/Models.Book/CheckOut | ActionNameOnEntityType nebo Action | CheckOutOnBook |

Další informace najdete v tématu [Akce OData](odata-v3/odata-actions.md).

**Signatury metod**

Tady je několik pravidel pro signatury metod:

- Pokud cesta obsahuje klíč, musí mít tato akce parametr s názvem *Key*.
- Pokud cesta obsahuje klíč do vlastnosti navigace, měla by mít tato akce parametr s názvem *relatedKey*.
- Vyupraví *klíč* a *relatedKey* parametry pomocí parametru **[FromODataUri]** .
- Žádosti POST a PUT přebírají parametr typu entity.
- Požadavky PATCH přebírají parametr typu **Delta&lt;t&gt;** , kde *t* je typ entity.

Tady je příklad, který ukazuje signatury metod pro všechny integrované konvence směrování OData.

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>Vlastní konvence směrování

Předdefinované konvence v současné době nezahrnují všechny možné identifikátory URI OData. Nové konvence můžete přidat implementací rozhraní **IODataRoutingConvention** . Toto rozhraní má dvě metody:

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController** vrátí název kontroleru.
- **SelectAction** vrátí název akce.

U obou metod by tato metoda měla vracet hodnotu null, pokud úmluva na tento požadavek neplatí.

Parametr **ODataPath** představuje analyzovanou cestu prostředku OData. Obsahuje seznam instancí **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** , jeden pro každý segment cesty prostředku. **ODataPathSegment** je abstraktní třída; každý typ segmentu je reprezentován třídou, která je odvozena z **ODataPathSegment**.

Vlastnost **ODataPath. TemplatePath** je řetězec, který představuje zřetězení všech segmentů cesty. Například pokud je identifikátor URI `/Products(1)/Supplier`, šablona cesty je &quot;~/EntitySet/Key/Navigation&quot;. Všimněte si, že segmenty neodpovídají přímo segmentům identifikátoru URI. Například klíč entity (1) je reprezentován jako vlastní **ODataPathSegment**.

Obvykle implementace **IODataRoutingConvention** provádí následující:

1. Porovnejte šablonu cesty, abyste viděli, jestli se tato konvence vztahuje na aktuální požadavek. Pokud se nepoužívá, vrátí hodnotu null.
2. Pokud se konvence používá, použijte vlastnosti instancí **ODataPathSegment** k odvození názvů kontroléru a akce.
3. V případě akcí přidejte do slovníku směrování libovolné hodnoty, které by měly být svázány s parametry akce (obvykle klíče entit).

Pojďme se podívat na konkrétní příklad. Předdefinované konvence směrování nepodporují indexování do kolekce navigace. Jinými slovy, neexistuje žádná konvence pro identifikátory URI, například následující:

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

Tady je vlastní konvence směrování pro zpracování tohoto typu dotazu.

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

Poznámky:

1. Je odvozen z **EntitySetRoutingConvention**, protože metoda **SelectController** v této třídě je vhodná pro tuto novou konvenci směrování. To znamená, že nemusíte znovu implementovat **SelectController**.
2. Konvence se vztahuje pouze na požadavky GET a pouze v případě, že je šablona cesty &quot;~/EntitySet/Key/Navigation/Key&quot;.
3. Název akce je &quot;získat&quot;{EntityType}, kde *{EntityType}* je typ kolekce navigace. Například &quot;getdodavatel&quot;. Můžete použít libovolnou konvenci pojmenování, &#8212; kterou byste chtěli udělat, abyste se ujistili, že se akce kontroleru shodují.
4. Akce přijímá dva parametry s názvem *Key* a *relatedKey*. (Seznam některých předdefinovaných názvů parametrů naleznete v tématu [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)

Dalším krokem je přidání nové konvence do seznamu konvencí směrování. K tomu dojde během konfigurace, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

Tady je několik dalších vzorových konvencí směrování, které jsou užitečné pro studii:

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

A samozřejmě samotné webové rozhraní API je open source, takže si můžete prohlédnout [zdrojový kód](http://aspnetwebstack.codeplex.com/) pro předdefinované konvence směrování. Ty jsou definované v oboru názvů **System. Web. http. OData. Routing. Conventions** .
