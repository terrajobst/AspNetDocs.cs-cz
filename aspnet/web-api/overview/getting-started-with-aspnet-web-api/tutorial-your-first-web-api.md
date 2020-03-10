---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: Začínáme s webovým rozhraním API ASP.NETC#() – ASP.NET 4. x
author: MikeWasson
description: Kurz s kódem. Pomocí webového rozhraní API ASP.NET můžete vytvořit webové rozhraní API, které vrátí seznam produktů.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556796"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a>Začínáme s webovým rozhraním API 2C#() pro ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

V tomto kurzu použijete webové rozhraní API ASP.NET k vytvoření webového rozhraní API, které vrátí seznam produktů.

HTTP není pouze pro obsluhu webových stránek. HTTP je také výkonná platforma pro vytváření rozhraní API, která zveřejňují služby a data. HTTP je jednoduché, flexibilní a všudypřítomný. Skoro libovolná platforma, na kterou si můžete představit, má knihovnu HTTP, takže služby HTTP mohou dosáhnout široké škály klientů, včetně prohlížečů, mobilních zařízení a tradičních aplikací klasické pracovní plochy.

Webové rozhraní API ASP.NET je rozhraní pro vytváření webových rozhraní API nad .NET Framework. 

## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu

- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- Webové rozhraní API 2

Novější verzi tohoto kurzu najdete v tématu [Vytvoření webového rozhraní API s ASP.NET Core a sadou Visual Studio pro Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) .

## <a name="create-a-web-api-project"></a>Vytvoření projektu webového rozhraní API

V tomto kurzu použijete webové rozhraní API ASP.NET k vytvoření webového rozhraní API, které vrátí seznam produktů. Webová stránka front-end používá jQuery k zobrazení výsledků.

![](tutorial-your-first-web-api/_static/image1.png)

Spusťte Visual Studio a na **úvodní** stránce vyberte **Nový projekt** . Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace**. Pojmenujte projekt "ProductsApp" a klikněte na tlačítko **OK**.

![](tutorial-your-first-web-api/_static/image2.png)

V dialogovém okně **Nový projekt ASP.NET** vyberte **prázdnou** šablonu. V části &quot;přidat složky a základní reference pro&quot;zaškrtněte **webové rozhraní API**. Klikněte na tlačítko **OK**.

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> Můžete také vytvořit projekt webového rozhraní API pomocí šablony &quot;Web API&quot;. Šablona webového rozhraní API používá ASP.NET MVC k poskytnutí stránek s nápovědě k rozhraní API. Používám prázdnou šablonu pro tento kurz, protože chci zobrazit webové rozhraní API bez MVC. Obecně platí, že k používání webového rozhraní API nemusíte znát ASP.NET MVC.

## <a name="adding-a-model"></a>Přidání modelu

*Model* je objekt, který představuje data v aplikaci. Webové rozhraní API ASP.NET může model automaticky serializovat do formátu JSON, XML nebo jiného formátu a pak zapsat Serializovaná data do těla zprávy odpovědi HTTP. Pokud klient může číst formát serializace, může objekt deserializovat. Většina klientů může analyzovat kód XML nebo JSON. Kromě toho může klient určit, který formát chce, nastavením hlavičky Accept ve zprávě požadavku HTTP.

Pojďme začít vytvořením jednoduchého modelu, který představuje produkt.

Pokud Průzkumník řešení ještě není vidět, klikněte na nabídku **zobrazení** a vyberte možnost **Průzkumník řešení**. V Průzkumník řešení klikněte pravým tlačítkem na složku modely. V místní nabídce vyberte **Přidat** a pak vyberte **Třída**.

![](tutorial-your-first-web-api/_static/image4.png)

Pojmenujte třídu &quot;&quot;produktu. Do třídy `Product` přidejte následující vlastnosti.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>Přidání kontroleru

Ve webovém rozhraní API je *kontroler* objekt, který zpracovává požadavky HTTP. Přidáme kontroler, který může vracet buď seznam produktů, nebo jeden produkt určený IDENTIFIKÁTORem.

> [!NOTE]
> Pokud jste použili ASP.NET MVC, už jste obeznámeni s řadiči. Řadiče webového rozhraní API se podobají řadičům MVC, ale dědí třídu **ApiController** namísto třídy **Controller** .

V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat** a pak vybrat **kontroler**.

![](tutorial-your-first-web-api/_static/image5.png)

V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte možnost **KONTROLER webového rozhraní API – prázdné**. Klikněte na **Přidat**.

![](tutorial-your-first-web-api/_static/image6.png)

V dialogovém okně **Přidat řadič** pojmenujte kontrolér &quot;ProductsController&quot;. Klikněte na **Přidat**.

![](tutorial-your-first-web-api/_static/image7.png)

Generování uživatelského rozhraní vytvoří ve složce Controllers soubor s názvem ProductsController.cs.

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> Řadiče nemusíte vkládat do složky s názvem Controllers. Název složky je pouze pohodlný způsob, jak uspořádat zdrojové soubory.

Pokud tento soubor ještě není otevřený, otevřete ho tak, že na něj dvakrát kliknete. Nahraďte kód v tomto souboru následujícím kódem:

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

Aby byl příklad jednoduchý, produkty jsou uloženy v pevném poli uvnitř třídy Controller. Samozřejmě můžete v reálné aplikaci zadat dotaz na databázi nebo použít jiný externí zdroj dat.

Kontroler definuje dvě metody, které vracejí produkty:

- Metoda `GetAllProducts` vrátí celý seznam produktů jako typ **&gt;&lt;typu produktu IEnumerable** .
- Metoda `GetProduct` vyhledá jeden produkt podle jeho ID.

A to je vše! Máte funkční webové rozhraní API. Každá metoda na kontroleru odpovídá jednomu nebo více identifikátorům URI:

| Metoda kontroleru | URI |
| --- | --- |
| GetAllProducts | /api/products |
| Getproduct | *ID* /API/Products/ |

Pro metodu `GetProduct` je *ID* v identifikátoru URI zástupný symbol. Chcete-li například získat produkt s ID 5, je identifikátor URI `api/products/5`.

Další informace o tom, jak webové rozhraní API směruje požadavky HTTP na metody kontroleru, najdete v tématu [směrování ve webovém rozhraní api ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>Volání webového rozhraní API pomocí JavaScriptu a jQuery

V této části přidáme stránku HTML, která pro volání webového rozhraní API používá AJAX. Pomocí jQuery provedeme volání AJAX a také aktualizujeme stránku s výsledky.

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost **Přidat**a pak vyberte možnost **Nová položka**.

![](tutorial-your-first-web-api/_static/image9.png)

V dialogovém okně **Přidat novou položku** vyberte v části **vizuál C#** uzel **Web** a pak vyberte položku **stránky HTML** . Pojmenujte stránku &quot;index. html&quot;.

![](tutorial-your-first-web-api/_static/image10.png)

Nahraďte vše v tomto souboru následujícím způsobem:

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

Existuje několik způsobů, jak získat jQuery. V tomto příkladu jsem použil [Microsoft Ajax CDN](../../../ajax/cdn/overview.md). Můžete si ho také stáhnout z [http://jquery.com/](http://jquery.com/)a šablona projektu ASP.NET "webové rozhraní API" zahrnuje také jQuery.

### <a name="getting-a-list-of-products"></a>Získání seznamu produktů

Pokud chcete získat seznam produktů, odešlete požadavek HTTP GET na &quot;/API/Products&quot;.

Funkce jQuery [getjson](http://api.jquery.com/jQuery.getJSON/) pošle požadavek AJAX. Pro odpověď obsahuje pole objektů JSON. Funkce `done` určuje zpětné volání, které je voláno, pokud je požadavek úspěšný. Ve zpětném volání aktualizujeme model DOM informacemi o produktu.

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>Získání produktu podle ID

Pokud chcete získat produkt podle ID, odešlete požadavek HTTP GET na &quot;*ID* /API/Products/&quot;, kde *ID* je ID produktu.

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

Pořád budeme volat `getJSON` k odeslání požadavku AJAX, ale tentokrát vložíme ID do identifikátoru URI požadavku. Odpověď z tohoto požadavku je reprezentace jediného produktu ve formátu JSON.

## <a name="running-the-application"></a>Spuštění aplikace

Stisknutím klávesy F5 spusťte ladění aplikace. Webová stránka by měla vypadat takto:

![](tutorial-your-first-web-api/_static/image11.png)

Pokud chcete získat produkt podle ID, zadejte ID a klikněte na Hledat:

![](tutorial-your-first-web-api/_static/image12.png)

Pokud zadáte neplatné ID, server vrátí chybu protokolu HTTP:

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>Použití nástroje F12 k zobrazení žádosti a odpovědi HTTP

Když pracujete se službou HTTP, může být velmi užitečné zobrazit žádosti HTTP a požadovat zprávy. To můžete provést pomocí vývojářských nástrojů F12 v aplikaci Internet Explorer 9. V aplikaci Internet Explorer 9 otevřete stisknutím klávesy **F12** nástroje. Klikněte na kartu **síť** a potom stiskněte **Spustit zachytávání**. Nyní se vraťte na webovou stránku a stisknutím klávesy **F5** znovu načtěte webovou stránku. Internet Explorer bude zachytit přenos HTTP mezi prohlížečem a webovým serverem. V souhrnném zobrazení se zobrazuje veškerá síťová komunikace pro stránku:

![](tutorial-your-first-web-api/_static/image14.png)

Vyhledejte položku relativního identifikátoru URI "API/Products/". Vyberte tuto položku a klikněte na **Přejít k podrobnému zobrazení**. V podrobném zobrazení jsou k dispozici karty pro zobrazení požadavků a hlaviček odpovědí. Pokud například kliknete na kartu **hlavičky žádosti** , vidíte, že klient požádal o &quot;aplikace/JSON&quot; v hlavičce Accept.

![](tutorial-your-first-web-api/_static/image15.png)

Pokud kliknete na kartu tělo odpovědi, uvidíte, jak se seznam produktů serializován do formátu JSON. Jiné prohlížeče mají podobné funkce. Dalším užitečným nástrojem je [Fiddler](http://www.fiddler2.com/fiddler2/), webový ladicí proxy server. Fiddler můžete použít k zobrazení provozu protokolu HTTP a také k vytvoření požadavků HTTP, které vám umožní plnou kontrolu hlaviček protokolu HTTP v žádosti.

## <a name="see-this-app-running-on-azure"></a>Podívejte se na tuto aplikaci spuštěnou v Azure

Chcete zobrazit dokončený web běžící jako živá webová aplikace? Úplnou verzi aplikace můžete nasadit do svého účtu Azure pouhým kliknutím na následující tlačítko.

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

K nasazení tohoto řešení do Azure potřebujete účet Azure. Pokud ještě nemáte účet, máte následující možnosti:

- [Otevřete si bezplatný účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.
- [Aktivujte výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) – vaše předplatné MSDN vám každý měsíc dává kredity, které můžete použít pro placené služby Azure.

## <a name="next-steps"></a>Další kroky

- Úplnější příklad služby HTTP, která podporuje akce POST, PUT a DELETE a zápisy do databáze, najdete v tématu [použití webového rozhraní API 2 s Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).
- Další informace o vytváření kapalinových a reagujících webových aplikací nad službou HTTP najdete v tématu [aplikace ASP.NET Single Page](../../../single-page-application/index.md).
- Informace o tom, jak nasadit webový projekt aplikace Visual Studio do Azure App Service, najdete [v tématu Vytvoření webové aplikace v ASP.NET v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).
