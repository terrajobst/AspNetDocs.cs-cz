---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Směrování atributů ve webovém rozhraní API 2 pro ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554983"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>Směrování atributů ve webovém rozhraní API 2 ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

*Směrování* je způsob, jakým webové rozhraní API odpovídá na akci pomocí identifikátoru URI. Webové rozhraní API 2 podporuje nový typ směrování, kterému se říká *Směrování atributů*. Jak název naznačuje, směrování atributů používá atributy k definování tras. Směrování atributů nabízí větší kontrolu nad identifikátory URI ve webovém rozhraní API. Můžete například snadno vytvořit identifikátory URI, které popisují hierarchie prostředků.

Dřívější styl směrování s názvem směrování na základě konvence je stále plně podporovaný. Ve skutečnosti můžete obě techniky kombinovat do stejného projektu.

V tomto tématu se dozvíte, jak povolit směrování atributů a popisuje různé možnosti pro směrování atributů. Ucelený kurz, který používá směrování atributů, najdete v tématu [vytvoření REST API s směrováním atributů ve webovém rozhraní API 2](create-a-rest-api-with-attribute-routing.md).

## <a name="prerequisites"></a>Předpoklady

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Komunita, edice Professional nebo Enterprise

Případně můžete pomocí Správce balíčků NuGet nainstalovat potřebné balíčky. V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>Proč směrování atributů?

První vydání webového rozhraní API používalo směrování *založené na konvencích* . V tomto typu směrování definujete jednu nebo více šablon směrování, které jsou v podstatě parametrizované řetězce. Když rozhraní obdrží požadavek, odpovídá identifikátoru URI proti šabloně trasy. (Další informace o směrování založeném na konvencích najdete v tématu [směrování ve webovém rozhraní API ASP.NET](routing-in-aspnet-web-api.md).

Jednou z výhod směrování založeného na konvenci je, že šablony jsou definovány na jednom místě a pravidla směrování se používají konzistentně napříč všemi řadiči. Směrování založené na konvenci bohužel obtížně podporuje určité vzory identifikátorů URI, které jsou běžné v rozhraních RESTful API. Například prostředky často obsahují podřízené prostředky: zákazníci mají objednávky, filmy mají aktéry, v knihách jsou autoři a tak dále. Je přirozené vytvořit identifikátory URI, které odráží tyto relace:

`/customers/1/orders`

Tento typ identifikátoru URI je obtížné vytvořit pomocí směrování založeného na konvencích. I když je to možné, výsledky se nemůžou škálovat dobře, pokud máte mnoho řadičů nebo typů prostředků.

Při směrování atributů je jednoduché definovat trasu pro tento identifikátor URI. Jednoduše přidáte atribut do akce kontroleru:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

Tady je několik dalších vzorů, které směrování atributů usnadňuje.

**Správa verzí rozhraní API**

V tomto příkladu se "/API/v1/Products" směruje na jiný kontroler než "/API/v2/Products".

`/api/v1/products`
`/api/v2/products`

**Přetížené segmenty identifikátorů URI**

V tomto příkladu je "1" číslo objednávky, ale "čeká" se mapuje na kolekci.

`/orders/1`
`/orders/pending`

**Více typů parametrů**

V tomto příkladu je "1" číslo objednávky, ale "2013/06/16" Určuje datum.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>Povolení směrování atributů

Chcete-li povolit směrování atributů, zavolejte **MapHttpAttributeRoutes** během konfigurace. Tato metoda rozšíření je definována v třídě **System. Web. http. HttpConfigurationExtensions** .

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

Směrování atributů se dá kombinovat s směrováním [založeným na konvencích](routing-in-aspnet-web-api.md) . Chcete-li definovat trasy založené na konvencích, zavolejte metodu **MapHttpRoute** .

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Další informace o konfiguraci webového rozhraní API najdete v tématu [Konfigurace webového rozhraní API 2 pro ASP.NET](../advanced/configuring-aspnet-web-api.md).

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>Poznámka: migrace z webového rozhraní API 1

Před webovým rozhraním API 2 šablony projektu webového rozhraní API vygenerovaly kód takto:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

Pokud je povoleno směrování atributů, bude tento kód generovat výjimku. Pokud upgradujete existující projekt webového rozhraní API tak, aby používal směrování atributů, nezapomeňte aktualizovat konfigurační kód následujícím způsobem:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> Další informace najdete v tématu [Konfigurace webového rozhraní API s hostováním ASP.NET](../advanced/configuring-aspnet-web-api.md#webhost).

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>Přidání atributů trasy

Tady je příklad trasy definované pomocí atributu:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

Řetězec &quot;Customers/{customerId}/Orders&quot; je šablona identifikátoru URI pro trasu. Webové rozhraní API se pokusí spárovat identifikátor URI žádosti se šablonou. V tomto příkladu jsou "Customers" a "Orders" segmenty literálů a "{customerId}" je parametr proměnné. Následující identifikátory URI by odpovídaly této šabloně:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

Můžete omezit porovnání pomocí [omezení](#constraints), která jsou popsána dále v tomto tématu.

Všimněte si, že parametr &quot;{customerId}&quot; v šabloně trasy odpovídá názvu parametru *customerId* v metodě. Když webové rozhraní API vyvolá akci kontroleru, pokusí se vytvořit vazby parametrů trasy. Například pokud je identifikátor URI `http://example.com/customers/1/orders`, webové rozhraní API se pokusí o navázání hodnoty "1" na parametr *customerId* v akci.

Šablona identifikátoru URI může mít několik parametrů:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

Všechny metody kontroleru, které nemají atribut směrování, používají směrování na základě konvence. Tímto způsobem můžete zkombinovat oba typy směrování do stejného projektu.

## <a name="http-methods"></a>Metody HTTP

Webové rozhraní API také vybere akce založené na metodě HTTP žádosti (GET, POST atd.). Ve výchozím nastavení hledá webové rozhraní API porovnávání bez rozlišení velkých a malých písmen na začátku názvu metody kontroleru. Například metoda kontroleru s názvem `PutCustomers` odpovídá požadavku HTTP PUT.

Tuto konvenci můžete přepsat tak, že upravení metodu s následujícími atributy:

- **[HttpDelete]**
- **HttpGet**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **HTTPPOST**
- **[HttpPut]**

Následující příklad mapuje metodu CreateBook na požadavky HTTP POST.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

Pro všechny ostatní metody HTTP, včetně nestandardních metod, použijte atribut **AcceptVerbs** , který převezme seznam metod http.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>Předpony tras

Trasy v řadiči jsou často spouštěny se stejnou předponou. Příklad:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

Společnou předponu pro celý kontroler můžete nastavit pomocí atributu **[RoutePrefix]** :

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

K přepsání předpony trasy použijte vlnovku (~) na atributu method:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

Předpona trasy může zahrnovat parametry:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>Omezení trasy

Omezení tras vám umožňují omezit způsob párování parametrů v šabloně směrování. Obecná syntaxe je &quot;{Parameter: Constraint}&quot;. Příklad:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

V tomto případě se první trasa vybere jenom v případě, že ID &quot;&quot; segmentu identifikátoru URI je celé číslo. V opačném případě bude zvolena Druhá trasa.

V následující tabulce jsou uvedena omezení, která jsou podporována.

| Jedinečn | Popis | Příklad |
| --- | --- | --- |
| Rozšířená | Odpovídá znakům na velká a malá písmena latinky (a – z, A – Z). | {x:alpha} |
| bool | Odpovídá logické hodnotě. | {x:bool} |
| datetime | Odpovídá hodnotě **DateTime** . | {x:datetime} |
| decimal | Odpovídá desítkové hodnotě. | {x:decimal} |
| double | Odpovídá hodnotě 64, což je hodnota s plovoucí desetinnou čárkou. | {x:double} |
| float | Odpovídá hodnotě 32, což je hodnota s plovoucí desetinnou čárkou. | {x:float} |
| guid | Odpovídá hodnotě identifikátoru GUID. | {x:guid} |
| int | Vyhledá shodu s celočíselnou hodnotou 32. | {x:int} |
| length | Odpovídá řetězci se zadanou délkou nebo v zadaném rozsahu délek. | {x:Length (6)} {x:Length (1; 20)} |
| long | Vyhledá shodu s celočíselnou hodnotou 64. | {x:long} |
| max | Odpovídá celému číslu s maximální hodnotou. | {x:max (10)} |
| MaxLength | Odpovídá řetězci s maximální délkou. | {x:MaxLength (10)} |
| min | Odpovídá celému číslu s minimální hodnotou. | {x:min (10)} |
| minLength | Odpovídá řetězci s minimální délkou. | {x:minLength (10)} |
| range | Odpovídá celému číslu v rámci rozsahu hodnot. | {x:Range (10, 50)} |
| regulární | Odpovídá regulárnímu výrazu. | {x:Regex (^ \d{3}-\d{3}-\d{4}$)} |

Všimněte si, že některá omezení, například &quot;minimální&quot;, přijímají argumenty v závorkách. U parametru můžete použít více omezení oddělených dvojtečkou.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>Vlastní omezení trasy

Můžete vytvořit vlastní omezení trasy implementací rozhraní **IHttpRouteConstraint** . Například následující omezení omezuje parametr na celočíselnou hodnotu, která není nulová.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

Následující kód ukazuje, jak toto omezení zaregistrovat:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

Nyní můžete omezení použít ve svých trasách:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

Můžete také nahradit celou třídu **DefaultInlineConstraintResolver** implementací rozhraní **IInlineConstraintResolver** . Tím se nahradí všechna předdefinovaná omezení, pokud vaše implementace **IInlineConstraintResolver** konkrétně nepřidá.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>Volitelné parametry identifikátoru URI a výchozí hodnoty

Parametr URI můžete nastavit jako volitelný přidáním otazníku do parametru Route. Pokud je parametr trasy volitelný, je nutné definovat výchozí hodnotu parametru metody.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

V tomto příkladu `/api/books/locale/1033` a `/api/books/locale` vrací stejný prostředek.

Případně můžete zadat výchozí hodnotu v rámci šablony trasy následujícím způsobem:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

To je skoro stejné jako v předchozím příkladu, ale existuje mírné rozdíly v chování při použití výchozí hodnoty.

- V prvním příkladu ("{LCID: int?}") je výchozí hodnota 1033 přiřazena přímo k parametru metody, takže parametr bude mít tuto přesnou hodnotu.
- V druhém příkladu ("{LCID: int = 1033}") je výchozí hodnota "1033" prostřednictvím procesu vytváření vazby modelu. Výchozí model-Binder převede "1033" na číselnou hodnotu 1033. Mohli byste se ale připojit k vlastnímu pořadači modelů, který může dělat něco jiného.

(Ve většině případů platí, že pokud ve vašem kanálu nemáte vlastní pořadače modelů, budou tyto dva formuláře ekvivalentní.)

<a id="route-names"></a>
## <a name="route-names"></a>Názvy tras

Ve webovém rozhraní API má každá trasa název. Názvy tras jsou užitečné pro generování odkazů, abyste mohli zahrnout odkaz do odpovědi HTTP.

Chcete-li zadat název trasy, nastavte vlastnost **název** u atributu. Následující příklad ukazuje, jak nastavit název trasy a také jak použít název trasy při generování propojení.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>Pořadí směrování

Když se architektura pokusí vyhledat identifikátor URI s trasou, vyhodnotí trasy v určitém pořadí. Chcete-li zadat pořadí, nastavte vlastnost **Order** v atributu Route. Nižší hodnoty jsou vyhodnocovány jako první. Výchozí hodnota pořadí je nula.

Tady je způsob, jakým je stanoveno celkové řazení:

1. Porovnejte vlastnost **Order** atributu Route.
2. Podívejte se na každý segment identifikátoru URI v šabloně trasy. Pro každý segment seřazením následujícím způsobem:

    1. Segmenty literálu.
    2. Parametry směrování s omezeními.
    3. Parametry trasy bez omezení.
    4. Segmenty parametrů se zástupnými znaky s omezeními.
    5. Segmenty parametrů zástupného znaku bez omezení.
3. V případě propojení se trasy seřadí podle ordinálního porovnávání řetězců bez rozlišení velkých a malých písmen ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) šablony trasy.

Tady je příklad. Předpokládejme, že definujete následující kontroler:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

Tyto trasy jsou seřazené následujícím způsobem.

1. objednávky/podrobnosti
2. objednávky/{ID}
3. objednávky/{Customer}
4. objednávky/{\*datum}
5. objednávky/čeká na vyřízení

Všimněte si, že "Details" je segment literálu a zobrazí se před "{ID}", ale "čeká" se zobrazí jako poslední, protože vlastnost **Order** je 1. (Tento příklad předpokládá, že nejsou k dispozici žádní zákazníci s názvem "Details" nebo "pending". Obecně se pokuste vyhnout dvojznačným trasám. V tomto příkladu je lepší šablonou směrování pro `GetByCustomer` "Customers/{Customer}").
