---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: Povolení operací CRUD ve webovém rozhraní API ASP.NET 1 – ASP.NET 4. x
author: MikeWasson
description: V tomto kurzu se dozvíte, jak podporovat operace CRUD ve službě HTTP pomocí webového rozhraní API ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556201"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a>Povolení operací CRUD ve webovém rozhraní API ASP.NET 1

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> V tomto kurzu se dozvíte, jak podporovat operace CRUD ve službě HTTP pomocí webového rozhraní API ASP.NET pro ASP.NET 4. x.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Visual Studio 2012
> - Webové rozhraní API 1 (funguje taky s webovým rozhraním API 2)

CRUD představuje &quot;vytváření, čtení, aktualizace a odstraňování&quot; což jsou čtyři základní databázové operace. Mnohé služby HTTP také modelují operace CRUD prostřednictvím rozhraní API REST nebo REST.

V tomto kurzu vytvoříte velmi jednoduché webové rozhraní API pro správu seznamu produktů. Každý produkt bude obsahovat název, cenu a kategorii (například &quot;Toys&quot; nebo &quot;hardware&quot;) a ID produktu.

Rozhraní API pro produkty zpřístupňuje následující metody.

| Akce | Metoda HTTP | Relativní identifikátor URI |
| --- | --- | --- |
| Získat seznam všech produktů | GET | /api/products |
| Získat produkt podle ID | GET | *ID* /API/Products/ |
| Získat produkt podle kategorie | GET | /API/Products? kategorie =*kategorie* |
| Vytvořit nový produkt | POST | /api/products |
| Aktualizace produktu | PUT | *ID* /API/Products/ |
| Odstranění produktu | DELETE | *ID* /API/Products/ |

Všimněte si, že některé identifikátory URI zahrnují ID produktu v cestě. Pokud například chcete získat produkt, jehož ID je 28, klient odešle požadavek GET na `http://hostname/api/products/28`.

### <a name="resources"></a>Zdroje

Rozhraní API pro produkty definuje identifikátory URI pro dva typy prostředků:

| Prostředek | URI |
| --- | --- |
| Seznam všech produktů. | /api/products |
| Jednotlivý produkt. | *ID* /API/Products/ |

### <a name="methods"></a>Metody

Čtyři hlavní metody HTTP (GET, PUT, POST a DELETE) lze namapovat na operace CRUD následujícím způsobem:

- GET načte reprezentace prostředku na zadaném identifikátoru URI. GET by neměl mít na serveru žádné vedlejší účinky.
- VLOŽÍ aktualizace prostředku se zadaným identifikátorem URI. Příkaz PUT lze použít také k vytvoření nového prostředku v zadaném identifikátoru URI, pokud server umožňuje klientům zadat nové identifikátory URI. V tomto kurzu rozhraní API nebude podporovat vytváření prostřednictvím PUT.
- POST vytvoří nový prostředek. Server přiřadí identifikátor URI pro nový objekt a vrátí tento identifikátor URI jako součást zprávy s odpovědí.
- ODSTRANĚNÍ odstraní prostředek se zadaným identifikátorem URI.

Poznámka: metoda PUT nahrazuje celou entitu produktu. To znamená, že klient očekává odeslání úplné reprezentace aktualizovaného produktu. Pokud chcete podporovat částečné aktualizace, je vhodnější metoda opravy. Tento kurz neimplementuje opravu.

## <a name="create-a-new-web-api-project"></a>Vytvoření nového projektu webového rozhraní API

Začněte spuštěním sady Visual Studio a na **úvodní** stránce vyberte **Nový projekt** . Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**. Pojmenujte projekt &quot;ProductStore&quot; a klikněte na tlačítko **OK**.

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte **webové rozhraní API** a klikněte na **OK**.

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>Přidání modelu

*Model* je objekt, který představuje data v aplikaci. Ve webovém rozhraní API ASP.NET můžete jako modely použít objekty CLR silného typu a automaticky je serializovat do XML nebo JSON pro klienta.

Pro rozhraní ProductStore API se naše data skládají z produktů, takže vytvoříme novou třídu s názvem `Product`.

Pokud Průzkumník řešení ještě není vidět, klikněte na nabídku **zobrazení** a vyberte možnost **Průzkumník řešení**. V Průzkumník řešení klikněte pravým tlačítkem na složku **modely** . V místní nabídce vyberte **Přidat**a pak vyberte **Třída**. Pojmenujte třídu &quot;&quot;produktu.

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

Do třídy `Product` přidejte následující vlastnosti.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>Přidání úložiště

Musíme Uložit kolekci produktů. Je vhodné oddělit kolekci od implementace naší služby. Tímto způsobem můžeme změnit záložní úložiště bez přepsání třídy služby. Tento typ návrhu se nazývá vzor *úložiště* . Začněte definováním obecného rozhraní pro úložiště.

V Průzkumník řešení klikněte pravým tlačítkem na složku **modely** . Vyberte **Přidat**a pak vyberte **Nová položka**.

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte C# uzel. V C#části vyberte **kód**. V seznamu šablon kódu vyberte **rozhraní**. Název rozhraní &quot;IProductRepository&quot;.

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

Přidejte následující implementaci:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

Nyní do složky modely přidejte další třídu s názvem &quot;ProductRepository.&quot; Tato třída bude implementovat rozhraní `IProductRepository`. Přidejte následující implementaci:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

Úložiště uchovává seznam v místní paměti. V tomto kurzu je to v pořádku, ale v reálné aplikaci byste data ukládali externě, buď do databáze, nebo do cloudového úložiště. Vzor úložiště vám usnadní pozdější změnu implementace.

## <a name="adding-a-web-api-controller"></a>Přidání kontroleru webového rozhraní API

Pokud jste pracovali s ASP.NET MVC, už jste obeznámeni s řadiči. Ve webovém rozhraní API ASP.NET je *kontroler* třída, která zpracovává požadavky HTTP od klienta. Průvodce vytvořením nového projektu při vytváření projektu vytvořil dva řadiče. Pokud je chcete zobrazit, rozbalte složku řadiče v Průzkumník řešení.

- HomeController je tradiční kontroler ASP.NET MVC. Zodpovídá za obsluhu stránek HTML webu a přímo se nevztahuje k našemu webovému rozhraní API.
- ValuesController je ukázkový kontroler WebAPI.

Pokračujte a odstraňte ValuesController tak, že kliknete pravým tlačítkem na soubor v Průzkumník řešení a vyberete **Odstranit.** Nyní přidejte nový kontroler, a to takto:

V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat** a pak vybrat **kontroler**.

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

V průvodci **přidáním kontroleru** pojmenujte kontrolér &quot;ProductsController&quot;. V rozevíracím seznamu **Šablona** vyberte **prázdný kontroler rozhraní API**. Pak klikněte na **Přidat**.

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> Ovladače není nutné vkládat do složky s názvem Controllers. Název složky není důležitý. je to jednoduše pohodlný způsob, jak uspořádat zdrojové soubory.

Průvodce **přidáním kontroleru** vytvoří ve složce Controllers soubor s názvem ProductsController.cs. Pokud tento soubor ještě není otevřený, otevřete ho tak, že na něj dvakrát kliknete. Přidejte následující příkaz **using** :

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

Přidejte pole, které obsahuje instanci **IProductRepository** .

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> Volání `new ProductRepository()` v kontroleru není nejlepším návrhem, protože tento kontroler přiřazuje konkrétní implementaci `IProductRepository`. Lepší přístup najdete v tématu [použití překladače závislostí webového rozhraní API](../advanced/dependency-injection.md).

## <a name="getting-a-resource"></a>Získání prostředku

Rozhraní ProductStore API zveřejňuje několik &quot;číst&quot; akcí jako metody GET protokolu HTTP. Každá akce bude odpovídat metodě ve třídě `ProductsController`.

| Akce | Metoda HTTP | Relativní identifikátor URI |
| --- | --- | --- |
| Získat seznam všech produktů | GET | /api/products |
| Získat produkt podle ID | GET | *ID* /API/Products/ |
| Získat produkt podle kategorie | GET | /API/Products? kategorie =*kategorie* |

Chcete-li získat seznam všech produktů, přidejte tuto metodu do třídy `ProductsController`:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

Název metody začíná na &quot;získat&quot;, tak podle konvence, kterou mapuje na požadavky GET. Vzhledem k tomu, že metoda nemá žádné parametry, je namapována na identifikátor URI, který neobsahuje *&quot;id&quot;* segmentu v cestě.

Chcete-li získat produkt podle ID, přidejte tuto metodu do třídy `ProductsController`:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

Tento název metody také začíná &quot;získat&quot;, ale metoda má parametr s názvem *ID*. Tento parametr je namapován na &quot;ID&quot; segmentu cesty identifikátoru URI. Rozhraní Web API pro ASP.NET automaticky převede ID na správný datový typ (**int**) pro parametr.

Metoda getproduct vyvolá výjimku typu **HttpResponseException** , pokud *ID* je neplatné. Tato výjimka bude přeložena rozhraním do chyby 404 (Nenalezeno).

Nakonec přidejte metodu pro vyhledání produktů podle kategorie:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

Pokud má identifikátor URI žádosti řetězec dotazu, webové rozhraní API se pokusí porovnat parametry dotazu s parametry v metodě kontroleru. Proto se identifikátor URI ve formátu "API/Products? kategorie =*Category*" namapuje na tuto metodu.

## <a name="creating-a-resource"></a>Vytvoření prostředku

Dále přidáme metodu do třídy `ProductsController` pro vytvoření nového produktu. Tady je jednoduchá implementace metody:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

Všimněte si, že tato metoda má dvě věci:

- Název metody začíná &quot;post...&quot;. Pokud chcete vytvořit nový produkt, klient odešle požadavek HTTP POST.
- Metoda přijímá parametr typu produkt. V rozhraní Web API jsou parametry se složitými typy deserializovány z textu žádosti. Očekáváme proto, že klient pošle serializovanou reprezentaci objektu produktu ve formátu XML nebo JSON.

Tato implementace bude fungovat, ale není poměrně kompletní. V ideálním případě chceme, aby odpověď protokolu HTTP zahrnovala tyto věci:

- **Kód odpovědi:** Ve výchozím nastavení rozhraní Web API nastaví stavový kód odpovědi na 200 (OK). Pokud je v závislosti na protokolu HTTP/1.1 výsledkem žádosti POST vytvoření prostředku, server by měl odpovědět na stav 201 (vytvořeno).
- **Umístění:** Když server vytvoří prostředek, měl by obsahovat identifikátor URI nového prostředku v hlavičce umístění odpovědi.

Webové rozhraní API pro ASP.NET usnadňuje zpracování zprávy s odpovědí HTTP. Tady je vylepšená implementace:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

Všimněte si, že návratový typ metody je nyní **HttpResponseMessage**. Vrácením **HttpResponseMessage** namísto produktu můžeme řídit podrobnosti zprávy s odpovědí HTTP, včetně stavového kódu a hlavičky umístění.

Metoda **CreateResponse** vytvoří **HttpResponseMessage** a automaticky zapíše serializovanou reprezentaci objektu produktu do těla zprávy odpovědi.

> [!NOTE]
> Tento příklad neověřuje `Product`. Informace o ověřování modelu najdete v tématu [ověřování modelu v ASP.NET webovém rozhraní API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).

## <a name="updating-a-resource"></a>Aktualizace prostředku

Aktualizace produktu pomocí PUT je jednoduchá:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

Název metody začíná na &quot;PUT...&quot;, takže webové rozhraní API odpovídá na vložení požadavků. Metoda přijímá dva parametry, ID produktu a aktualizovaný produkt. Parametr *ID* je pořízen z cesty identifikátoru URI a parametr *produktu* je deserializovaný z textu žádosti. Ve výchozím nastavení přebírá rozhraní Web API ASP.NET jednoduché typy parametrů z trasy a komplexní typy z textu žádosti.

## <a name="deleting-a-resource"></a>Odstranění prostředku

Chcete-li odstranit prostředek, definujte "Delete..." Metoda.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

Pokud je žádost o odstranění úspěšná, může vrátit stav 200 (OK) s tělem entity, které popisuje stav. stav 202 (přijato), pokud odstranění stále čeká na vyřízení; nebo stav 204 (žádný obsah) bez těla entity V takovém případě má `DeleteProduct` metoda `void` návratový typ, takže webové rozhraní API ASP.NET automaticky přeloží tento kód stavu 204 (žádný obsah).
