---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Volání webového rozhraní API z klienta .NET (C#) – ASP.NET 4. x
author: MikeWasson
description: V tomto kurzu se dozvíte, jak volat webové rozhraní API z aplikace .NET 4. x.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: ab3ba71839123e848dffaa59871f9dac8c1a88d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622617"
---
# <a name="call-a-web-api-from-a-net-client-c"></a>Volání webového rozhraní API z klienta .NET (C#)

[Jan Wasson](https://github.com/MikeWasson) a [Rick Anderson](https://twitter.com/RickAndMSFT)

[Stažení dokončeného projektu](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample). [Pokyny ke stažení](/aspnet/core/tutorials/#how-to-download-a-sample). 

V tomto kurzu se dozvíte, jak volat webové rozhraní API z aplikace .NET pomocí [System .NET. http. HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)

V tomto kurzu se napíše klientská aplikace, která využívá následující webové rozhraní API:

| Akce | Metoda HTTP | Relativní identifikátor URI |
| --- | --- | --- |
| Získat produkt podle ID | GET | *ID* /API/Products/ |
| Vytvořit nový produkt | POST | /api/products |
| Aktualizace produktu | PUT | *ID* /API/Products/ |
| Odstranění produktu | DELETE | *ID* /API/Products/ |

Informace o tom, jak implementovat toto rozhraní API s webovým rozhraním API ASP.NET, najdete v tématu [Vytvoření webového rozhraní API, které podporuje operace CRUD](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).

Pro zjednodušení je klientská aplikace v tomto kurzu pro konzolovou aplikaci systému Windows. **HttpClient** se také podporuje pro aplikace Windows Phone a Windows Store. Další informace najdete v tématu [Zápis kódu klienta webového rozhraní API pro více platforem pomocí přenosných knihoven](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) .

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>Vytvoření konzolové aplikace

V aplikaci Visual Studio vytvořte novou konzolovou aplikaci pro Windows s názvem **HttpClientSample** a vložte ji do následujícího kódu:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

Předchozí kód je kompletní klientská aplikace.

`RunAsync` běží a blokuje až do dokončení. Většina metod **HttpClient** je asynchronní, protože provádí v/v sítě. Všechny asynchronní úlohy jsou prováděny v rámci `RunAsync`. Obvykle aplikace neblokuje hlavní vlákno, ale tato aplikace nepovoluje žádnou interakci.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>Instalace klientských knihoven webového rozhraní API

Pomocí Správce balíčků NuGet nainstalujte balíček klientské knihovny webového rozhraní API.

V nabídce **nástroje** vyberte **správce balíčků NuGet** > **konzolu Správce balíčků**. V konzole správce balíčků (PMC) zadejte následující příkaz:

`Install-Package Microsoft.AspNet.WebApi.Client`

Předchozí příkaz přidá do projektu následující balíčky NuGet:

* Microsoft.AspNet.WebApi.Client
* Newtonsoft.Json

Netwonsoft. JSON (označované také jako Json.NET) je oblíbený vysoce výkonný rozhraní JSON pro rozhraní .NET.

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>Přidat třídu modelu

Projděte si třídu `Product`:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

Tato třída se shoduje s datovým modelem používaným webovým rozhraním API. Aplikace může použít **HttpClient** ke čtení instance `Product` z odpovědi HTTP. Aplikace nemusí zapisovat žádný kód deserializace.

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>Vytvoření a inicializace HttpClient

Prověřte vlastnost Static **HttpClient** :

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**HttpClient** má být vytvořena instance jednou a znovu použita po celou dobu životnosti aplikace. Následující podmínky mohou způsobit chyby **SocketException** :

* Vytváří se nová instance **HttpClient** na žádost.
* Server v případě vysoké zátěže.

Vytvoření nové instance **HttpClient** na žádost může vyčerpat dostupné sokety.

Následující kód Inicializuje instanci **HttpClient** :

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

Předchozí kód:

* Nastaví základní identifikátor URI pro požadavky HTTP. Změňte číslo portu na port použitý v serverové aplikaci. Aplikace nebude fungovat, pokud se nepoužije port pro serverovou aplikaci.
* Nastaví hlavičku Accept na "Application/JSON". Nastavení této hlavičky oznamuje serveru, aby odesílal data ve formátu JSON.

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>Odeslat požadavek GET k načtení prostředku

Následující kód odešle požadavek GET na produkt:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

Metoda **GetAsync** ODEŠLE požadavek HTTP GET. Po dokončení metody vrátí **HttpResponseMessage** , který obsahuje odpověď HTTP. Pokud je stavový kód v odpovědi kód úspěšnosti, tělo odpovědi obsahuje reprezentaci kódu Product. Zavolejte **ReadAsAsync** k deserializaci datové části JSON do instance `Product`. Metoda **ReadAsAsync** je asynchronní, protože tělo odpovědi může být libovolně velké.

**HttpClient** nevyvolá výjimku, pokud odpověď HTTP obsahuje kód chyby. Místo toho má vlastnost **IsSuccessStatusCode** **hodnotu false** , pokud je stav kód chyby. Pokud dáváte přednost považovat kódy chyb HTTP jako výjimky, zavolejte [HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) objektu Response. `EnsureSuccessStatusCode` vyvolá výjimku, pokud stavový kód spadá mimo rozsah 200&ndash;299. Všimněte si, že **HttpClient** může vyvolat výjimky z jiných důvodů &mdash; například, pokud vyprší časový limit požadavku.

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>Formátovací moduly typu Media k deserializaci

Pokud je **ReadAsAsync** volán bez parametrů, používá výchozí sadu *formátovacích modulů médií* pro čtení těla odpovědi. Výchozí formátovací moduly podporují data zakódovaná JSON, XML a Form-URL.

Namísto použití výchozích formátovacích modulů můžete zadat seznam formátovacích modulů do metody **ReadAsAsync** .  Použití seznamu formátovacích modulů je užitečné, pokud máte vlastní formátovací modul typu média:

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

Další informace najdete v tématu [Formátování médií ve webovém rozhraní API 2 pro ASP.NET](../formats-and-model-binding/media-formatters.md) .

## <a name="sending-a-post-request-to-create-a-resource"></a>Odeslání požadavku POST k vytvoření prostředku

Následující kód odešle požadavek POST, který obsahuje instanci `Product` ve formátu JSON:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

Metoda **PostAsJsonAsync** :

* Serializace objektu do formátu JSON.
* Odešle datovou část JSON v žádosti POST.

Pokud je požadavek úspěšný:

* Měla by vrátit odpověď 201 (vytvořeno).
* Odpověď by měla obsahovat adresu URL vytvořených prostředků v hlavičce umístění.

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>Odeslání žádosti o vložení za účelem aktualizace prostředku

Následující kód odešle požadavek PUT k aktualizaci produktu:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

Metoda **PutAsJsonAsync** funguje jako **PostAsJsonAsync**s tím rozdílem, že ODEŠLE požadavek PUT namísto post.

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>Odeslání žádosti o odstranění k odstranění prostředku

Následující kód pošle žádost o odstranění produktu:

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

Podobně jako GET, žádost o odstranění neobsahuje tělo žádosti. Pomocí DELETE není nutné zadávat formát JSON nebo XML.

## <a name="test-the-sample"></a>Test ukázky

Testování klientské aplikace:

1. [Stáhněte](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) a spusťte serverovou aplikaci. [Pokyny ke stažení](/aspnet/core/#how-to-download-a-sample). Ověřte, že aplikace serveru pracuje. Například `http://localhost:64195/api/products` by měl vracet seznam produktů.
2. Nastavte základní identifikátor URI pro požadavky HTTP. Změňte číslo portu na port použitý v serverové aplikaci.
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. Spusťte klientskou aplikaci. Vytvoří se následující výstup:

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
