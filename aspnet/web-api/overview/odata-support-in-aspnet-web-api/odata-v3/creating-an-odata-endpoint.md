---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Vytvoření koncového bodu OData V3 s webovým rozhraním API 2 | Microsoft Docs
author: MikeWasson
description: Protokol OData (Open Data Protocol) je protokol pro přístup k datům pro web. OData poskytuje jednotný způsob strukturování dat, dotazování na data a manipulaci s daty...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556411"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>Vytvoření koncového bodu OData V3 pomocí webového rozhraní API 2

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> Protokol OData ( [Open Data Protocol](http://www.odata.org/) ) je protokol pro přístup k datům pro web. OData poskytuje jednotný způsob strukturování dat, dotazování na data a manipulaci s datovou sadou prostřednictvím operací CRUD (vytvoření, čtení, aktualizace a odstranění). OData podporuje formáty AtomPub (XML) i JSON. OData také definuje způsob, jak vystavit metadata o datech. Klienti můžou metadata použít ke zjištění informací o typu a vztahů pro datovou sadu.
>
> Webové rozhraní API pro ASP.NET usnadňuje vytvoření koncového bodu OData pro datovou sadu. Můžete přesně řídit, které operace OData koncový bod podporuje. Můžete hostovat více koncových bodů OData spolu s koncovými body mimo OData. Máte plnou kontrolu nad datovým modelem, koncovou obchodní logikou a datovou vrstvou.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Webové rozhraní API 2
> - OData verze 3
> - Entity Framework 6
> - [Proxy Fiddler webového ladění (volitelné)](http://www.fiddler2.com)
>
> V [aktualizaci ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650)byla přidána podpora rozhraní Web API OData. Tento kurz ale používá generování uživatelského rozhraní, které bylo přidáno v Visual Studio 2013.

V tomto kurzu vytvoříte jednoduchý koncový bod OData, ke kterému se můžou klienti dotazovat. Také vytvoříte C# klienta pro koncový bod. Po dokončení tohoto kurzu se v další sadě kurzů ukáže, jak přidat další funkce, včetně vztahů mezi entitami, akcemi a $expand/$select.

- [Vytvoření projektu sady Visual Studio](#create-project)
- [Přidání modelu entity](#add-model)
- [Přidat kontroler OData](#add-controller)
- [Přidání modelu EDM a trasy](#edm)
- [Dosazení databáze (volitelné)](#seed-db)
- [Zkoumání koncového bodu OData](#explore)
- [Formáty serializace OData](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>Vytvoření projektu sady Visual Studio

V tomto kurzu vytvoříte koncový bod OData, který podporuje základní operace CRUD. Koncový bod zveřejní jeden prostředek, seznam produktů. Novější kurzy budou přidávat další funkce.

Spusťte Visual Studio a na úvodní stránce vyberte **Nový projekt** . Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel vizuál C# . V **části C#vizuál** vyberte **Web**. Vyberte šablonu **webové aplikace ASP.NET** .

![](creating-an-odata-endpoint/_static/image1.png)

V dialogovém okně **Nový projekt ASP.NET** vyberte **prázdnou** šablonu. V části &quot;přidat složky a základní reference pro...&quot;zaškrtněte **webové rozhraní API**. Klikněte na tlačítko **OK**.

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>Přidání modelu entity

*Model* je objekt, který představuje data v aplikaci. Pro tento kurz potřebujeme model, který reprezentuje produkt. Model odpovídá našemu typu entity OData.

V Průzkumník řešení klikněte pravým tlačítkem na složku modely. V místní nabídce vyberte **Přidat** a pak vyberte **Třída**.

![](creating-an-odata-endpoint/_static/image3.png)

V dialogovém okně **Přidat novou** položku pojmenujte třídu &quot;&quot;produktu.

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> Podle konvence jsou třídy modelu umístěny do složky modely. Nemusíte postupovat podle této konvence ve svých vlastních projektech, ale použijeme ji pro tento kurz.

Do souboru Product.cs přidejte následující definici třídy:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

Vlastnost ID bude klíč entity. Klienti můžou zadávat dotazy na produkty podle ID. Toto pole by také představovalo primární klíč v back-endové databázi.

Sestavte projekt hned teď. V dalším kroku použijeme některé generování uživatelského rozhraní sady Visual Studio, které používá reflexi k nalezení typu produktu.

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>Přidat kontroler OData

*Kontroler* je třída, která zpracovává požadavky HTTP. Pro každou sadu entit v rámci služby OData definujete samostatný kontroler. V tomto kurzu vytvoříme jeden kontroler.

V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat** a pak vybrat **kontroler**.

![](creating-an-odata-endpoint/_static/image5.png)

V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte &quot;kontroler webového rozhraní API 2 OData s akcemi pomocí Entity Framework&quot;.

![](creating-an-odata-endpoint/_static/image6.png)

V dialogovém okně **Přidat řadič** pojmenujte kontroler "ProductsController". Vyberte &quot;použít akce asynchronního kontroleru&quot; CheckBox. V rozevíracím seznamu **model** vyberte třídu produktu.

![](creating-an-odata-endpoint/_static/image7.png)

Klikněte na tlačítko **nový kontext dat...** . Ponechte výchozí název typu datového kontextu a klikněte na **Přidat**.

![](creating-an-odata-endpoint/_static/image8.png)

Kliknutím na Přidat v dialogovém okně Přidat řadič přidejte kontroler.

![](creating-an-odata-endpoint/_static/image9.png)

Poznámka: Pokud se zobrazí chybová zpráva s oznámením &quot;došlo k chybě při získávání typu...&quot;, ujistěte se, že jste po přidání třídy produktu vytvořili projekt sady Visual Studio. Generování uživatelského rozhraní používá reflexi k nalezení třídy.

![](creating-an-odata-endpoint/_static/image10.png)

Generování uživatelského rozhraní do projektu přidá dva soubory kódu:

- Products.cs definuje kontroler webového rozhraní API, který implementuje koncový bod OData.
- ProductServiceContext.cs poskytuje metody pro dotazování podkladové databáze pomocí Entity Framework.

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>Přidání modelu EDM a trasy

V Průzkumník řešení rozbalte složku App\_Start Folder a otevřete soubor s názvem WebApiConfig.cs. Tato třída obsahuje konfigurační kód pro webové rozhraní API. Nahraďte tento kód následujícím kódem:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

Tento kód provede dvě věci:

- Vytvoří model EDM (Entity Data Model) (EDM) pro koncový bod OData.
- Přidá trasu pro koncový bod.

EDM je abstraktní model dat. Model EDM slouží k vytvoření dokumentu metadat a definování identifikátorů URI pro službu. **ODataConventionModelBuilder** vytvoří EDM pomocí sady výchozích konvencí pojmenování EDM. Tento přístup vyžaduje nejméně kód. Pokud chcete mít větší kontrolu nad modelem EDM, můžete pomocí třídy **ODataModelBuilder** vytvořit EDM přidáním vlastností, klíčů a vlastností navigace explicitně.

Metoda **EntitySet** přidá sadu entit do modelu EDM:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

Řetězec "Products" definuje název sady entit. Název kontroleru se musí shodovat s názvem sady entit. V tomto kurzu se sada entit nazývá "Products" a kontroler má název `ProductsController`. Pokud jste pojmenovali sadu entit "ProductSet", pojmenujete `ProductSetController`kontroleru. Všimněte si, že koncový bod může mít několik sad entit. Pro každou sadu entit volejte **&gt;EntitySet&lt;t** a pak definujte odpovídající kontroler.

Metoda **MapODataRoute** přidá trasu pro koncový bod OData.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

První parametr je popisný název trasy. Klienti vaší služby tento název nevidí. Druhým parametrem je předpona identifikátoru URI pro koncový bod. V tomto kódu je identifikátor URI pro sadu entit Products http://<em>hostname</em>/OData/Products. Vaše aplikace může mít více než jeden koncový bod OData. Pro každý koncový bod zavolejte <strong>MapODataRoute</strong> a zadejte jedinečný název trasy a jedinečnou PŘEDPONu identifikátoru URI.

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>Dosazení databáze (volitelné)

V tomto kroku použijete Entity Framework k osazení databáze s některými testovacími daty. Tento krok je nepovinný, ale umožňuje hned testovat koncový bod OData.

V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

Tím se přidá složka s názvem migrace a soubor kódu s názvem Configuration.cs.

![](creating-an-odata-endpoint/_static/image12.png)

Otevřete tento soubor a přidejte následující kód do metody `Configuration.Seed`.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

V okně konzoly Správce balíčků zadejte následující příkazy:

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

Tyto příkazy generují kód, který vytvoří databázi a následně spustí tento kód.

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>Zkoumání koncového bodu OData

V této části použijeme [proxy Fiddler webového ladění](http://www.fiddler2.com) k odeslání požadavků do koncového bodu a kontrole zpráv odpovědí. To vám pomůže pochopit možnosti koncového bodu OData.

V aplikaci Visual Studio stiskněte klávesu F5 pro spuštění ladění. Ve výchozím nastavení Visual Studio otevře váš prohlížeč na `http://localhost:*port*`, kde *port* je číslo portu nakonfigurované v nastavení projektu.

V nastavení projektu můžete změnit číslo portu. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**. V okně Vlastnosti vyberte **Web**. Do pole **Adresa URL projektu**zadejte číslo portu.

### <a name="service-document"></a>Dokument služby

*Dokument služby* obsahuje seznam sad entit pro koncový bod OData. Chcete-li získat dokument služby, odešlete požadavek GET do kořenového identifikátoru URI služby.

Pomocí Fiddler na kartě **skladatele** zadejte následující identifikátor URI: `http://localhost:port/odata/`, kde *port* je číslo portu.

![](creating-an-odata-endpoint/_static/image13.png)

Klikněte na tlačítko **Provést**. Fiddler odešle do vaší aplikace požadavek HTTP GET. V seznamu webové relace by se měla zobrazit odpověď. Pokud vše funguje, bude stavový kód 200.

![](creating-an-odata-endpoint/_static/image14.png)

Dvojitým kliknutím na odpověď v seznamu webové relace zobrazíte podrobnosti zprávy s odpovědí na kartě kontroly.

![](creating-an-odata-endpoint/_static/image15.png)

Zpráva s nezpracovanými odpověďmi HTTP by měla vypadat nějak takto:

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

Ve výchozím nastavení webový rozhraní API vrátí dokument služby ve formátu AtomPub. Pro vyžádání JSON přidejte do požadavku HTTP následující hlavičku:

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

Nyní odpověď HTTP obsahuje datovou část JSON:

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>Dokument metadat služby

*Dokument metadat služby* popisuje datový model služby pomocí jazyka XML nazývaného jazyk CSDL (konceptuální schéma Definition Language). Dokument metadat zobrazuje strukturu dat ve službě a lze jej použít k vygenerování kódu klienta.

Chcete-li získat dokument metadat, odešlete požadavek GET na `http://localhost:port/odata/$metadata`. Tady je metadata pro koncový bod zobrazený v tomto kurzu.

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>Sada entit

Chcete-li získat sadu entit Products, odešlete požadavek GET na `http://localhost:port/odata/Products`.

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>Entita

Pokud chcete získat jednotlivý produkt, pošlete požadavek GET na `http://localhost:port/odata/Products(1)`, kde "1" je ID produktu.

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>Formáty serializace OData

OData podporuje několik formátů serializace:

- Publikování atomů (XML)
- JSON "Light" (představený v OData V3)
- JSON "Verbose" (OData v2)

Ve výchozím nastavení používá webové rozhraní API AtomPubJSON formát "Light".

Chcete-li získat formát AtomPub, nastavte hlavičku Accept na "Application/Atom + XML". Tady je příklad těla odpovědi:

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

Můžete se podívat na jednu zjevnou nevýhodu formátu Atom: je to mnohem více podrobných podrobností než ve formátu JSON. Pokud však máte klienta, který rozumí AtomPub, může klient preferovat tento formát přes JSON.

Tady je verze Light v rámci formátu JSON stejné entity:

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

Světlý formát JSON byl představen ve verzi 3 protokolu OData. Z důvodu zpětné kompatibility může klient požádat o starší formát JSON "Verbose". Pokud chcete požádat o podrobný formát JSON, nastavte hlavičku Accept na `application/json;odata=verbose`. Zde je podrobná verze:

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

V tomto formátu jsou další metadata v těle odpovědi, což může výrazně prodloužit nároky na celou relaci. Také přidá úroveň dereference po zabalení objektu ve vlastnosti s názvem "d".

## <a name="next-steps"></a>Další kroky

- [Přidání vztahů mezi entitami](working-with-entity-relations.md)
- [Přidat akce OData](odata-actions.md)
- [Volání služby OData z klienta .NET](calling-an-odata-service-from-a-net-client.md)
