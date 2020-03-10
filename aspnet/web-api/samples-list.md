---
uid: web-api/samples-list
title: Seznam ukázek webového rozhraní API – ASP.NET 4. x
author: rick-anderson
description: Seznam ukázek ASP.NET webového rozhraní API pro ASP.NET 4. x
ms.author: riande
ms.date: 09/18/2012
ms.custom: seoapril2019
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 24368fc80e7fc3c840f1f1f9accf13fa15a06c1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598460"
---
# <a name="web-api-samples-list"></a>Seznam ukázek webového rozhraní API

## <a name="httpclient-samples"></a>Ukázky HttpClient

**Ukázka překladu bingu** | [vs 2012 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

Ukazuje, jak volat [službu Microsoft Translator](https://msdn.microsoft.com/library/ff512419.aspx) pomocí třídy **HttpClient** . Rozhraní Microsoft Translator Service API vyžaduje token OAuth, který se aplikace získá odesláním žádosti na server tokenu Azure pro každý požadavek na službu překladatele. Výsledek ze serveru tokenu je podáván do žádosti odeslané službě překladu. Před spuštěním této ukázky musíte získat [klíč aplikace z Azure Marketplace](https://msdn.microsoft.com/library/hh454950.aspx) a vyplnit informace v ukázkové třídě AccessTokenMessageHandler.

**Ukázka mapy Google** | [podrobný popis](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [vs 2012 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

Používá **HttpClient** ke stažení mapy Redmond, WA z [Google Maps API](https://developers.google.com/maps/), uloží ho jako místní soubor a otevře výchozí prohlížeč obrázků.

**Ukázka klienta twitteru** | [detailní popis](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) | [vs 2012 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)

Ukazuje, jak napsat jednoduchého klienta Twitteru pomocí **HttpClient**. Ukázka používá **HttpMessageHandler** k vložení ověřovacích informací OAuth do odchozího **zprávy HttpRequestMessage**. Výsledek z Twitteru se načte pomocí JSON.NET. Před spuštěním této ukázky musíte získat [klíč aplikace z Twitteru](https://dev.twitter.com/)a vyplnit informace v ukázkové třídě OAuthMessageHandler.

**Ukázka Světové banky** | [detailní popis](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [vs 2010 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [vs 2012 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)

Ukazuje, jak načíst data z webu data World Bank pomocí JSON.NET k analýze výsledku.

## <a name="web-api-samples"></a>Ukázky webového rozhraní API

**Začínáme s webovým rozhraním API ASP.NET** | [vs 2012 source](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)

Ukazuje, jak vytvořit základní webové rozhraní API, které podporuje požadavky HTTP GET. Obsahuje zdrojový kód kurzu [prvního webového rozhraní API ASP.NET](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).

**Scénáře JavaScript Web API pro ASP.NET – komentáře** | [vs 2012 source](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

Ukazuje, jak používat webové rozhraní API ASP.NET k vytváření webových rozhraní API, která podporují klienty prohlížeče a dají se snadno volat pomocí jQuery.

**Správce kontaktů** | [vs 2010 zdroj](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

Tato ukázka používá webové rozhraní API ASP.NET k vytvoření jednoduché aplikace Správce kontaktů. Aplikace se skládá z webového rozhraní API Contact Manageru, které používá aplikace ASP.NET MVC a aplikace Windows Phone k zobrazení a správě seznamu kontaktů.

**Ukázka dávkování** | [podrobný popis](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [vs 2012 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

Ukazuje, jak implementovat dávkování HTTP v rámci ASP.NET. Dávkování se skládá z vložení více požadavků HTTP v rámci jedné části těla entity MIME, která se pak pošle na server jako HTTP POST. Žádosti jsou zpracovávány jednotlivě a odpovědi jsou vloženy do jiného textu entity, který je vrácen klientovi.

**Ukázka řadiče obsahu** | [detailní popis](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [vs 2010](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) source | [vs 2012 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

Ukazuje, jak číst a zapisovat entity požadavků a odpovědí asynchronně pomocí datových proudů. Vzorový kontroler má dvě akce: akci PUT, která čte tělo entity požadavku asynchronně a ukládá je do místního souboru a akci GET, která vrací obsah místního souboru.

**Ukázka překladače vlastního sestavení** | [vs 2012 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

Ukazuje, jak upravit webové rozhraní API ASP.NET, aby podporovalo zjišťování řadičů z dynamicky načteného sestavení knihovny. Ukázka implementuje vlastní **IAssembliesResolver** , který volá výchozí implementaci a pak přidá sestavení knihovny do výchozích výsledků.

**Ukázka formátování vlastního typu média** | [podrobný popis](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [vs 2010 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

Ukazuje, jak vytvořit vlastní formátovací modul typu média pomocí základní třídy **BufferedMediaTypeFormatter** . Tato základní třída je určena pro formátovací moduly, které primárně používají synchronní operace čtení a zápisu. Kromě zobrazení formátovacího modulu typu média Ukázka ukazuje, jak ho připojit tak, že ho zaregistrujete jako součást **HttpConfiguration** pro vaši aplikaci. Všimněte si, že je také možné použít třídu **MediaTypeFormatter** Base přímo pro formátovací moduly, které primárně používají asynchronní operace čtení a zápisu.

**Ukázka vazby vlastního parametru** | [podrobný popis](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [vs 2010 source](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

Ukazuje, jak přizpůsobit proces vazby parametrů, což je proces, který určuje, jak jsou informace z požadavku svázány s parametry akce. V této ukázce má domovský adaptér čtyři akce:

1. BindPrincipal ukazuje, jak navazovat parametr IPrincipal z vlastního obecného objektu zabezpečení, nikoli ze zprávy HTTP GET;
2. BindCustomComplexTypeFromUriOrBody ukazuje, jak vytvořit váže parametr komplexního typu, který se může nacházet buď z textu zprávy, nebo z identifikátoru URI požadavku zprávy HTTP POST;
3. BindCustomComplexTypeFromUriWithRenamedProperty ukazuje, jak vytvořit navázání parametru komplexního typu s přejmenovanou vlastností, která pochází z identifikátoru URI požadavku zprávy HTTP POST;
4. PostMultipleParametersFromBody ukazuje, jak navazovat více parametrů z těla zprávy POST;

**Ukázka nahrávání souborů** | [podrobný popis](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [vs 2012 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

Ukazuje, jak nahrát soubory do **ApiController** pomocí nahrávání souboru MIME s více částmi a jak nastavit oznámení o průběhu pomocí **HttpClient** pomocí **ProgressNotificationHandler**. Kontroler načte obsah souboru HTML do asynchronního načtení a zapíše jednu nebo více částí těla do místního souboru. Odpověď obsahuje informace o nahraném souboru (nebo souborech).

**Ukázka odeslání souboru do úložiště objektů BLOB v Azure** | [podrobný popis](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [vs 2012 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

Tato ukázka se podobá ukázce nahrávání souborů, ale místo uložení nahraných souborů na místní disk asynchronně nahrává soubory do [úložiště objektů BLOB v Azure](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs) pomocí [sady Windows Azure SDK pro .NET](https://www.windowsazure.com/develop/net/). Poskytuje také mechanismus pro výpis objektů blobů aktuálně přítomných v [kontejneru Azure Blob Storage](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs). Můžete vyzkoušet ukázku spuštěnou pro **Azure Storage emulátor** , který je součástí sady Azure SDK. Pokud máte [účet Azure Storage](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs), můžete ho spustit i na reálné službě úložiště.

**Ukázka kanálu obslužných rutin zpráv Http** | [detailní popis](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [vs 2010 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)

Ukazuje, jak nasměrovat instance **HttpMessageHandler** jak na klienta (**HttpClient**), tak na serveru (ASP.NET Web API). V ukázce se stejná obslužná rutina používá jak na klientovi, tak i na serveru. I když je pravděpodobné, že se přesná stejná obslužná rutina spustí na obou místech, objektový model je stejný na straně klienta a serveru.

**Ukázka nahrávání JSON** | [zdroj vs 2012](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

Ukazuje, jak nahrát a stáhnout JSON z **ApiController**a z něj. Ukázka používá minimální **ApiController** a přistupuje k nim pomocí **HttpClient**.

**Ukázka hybridní webové** aplikace | [podrobný popis](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [vs 2012 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)

Ukazuje, jak přistupovat k několika vzdáleným webům asynchronně z akce **ApiController** . Pokaždé, když je akce dosažena, požadavky se provádějí asynchronně, takže nejsou blokována žádná vlákna.

**Ukázka trasování paměti** | [detailní popis](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [vs 2010 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

Tento ukázkový projekt vytvoří balíček NuGet, který nainstaluje vlastní Zapisovací modul trasování v paměti do ASP.NET webových aplikací API.

**MongoDB Sample** | [detailed description](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [vs 2012 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)

Ukazuje, jak používat MongoDB jako trvalé úložiště pro **ApiController**pomocí vzoru úložiště.

**Ukázka procesorů textu odpovědi** | [vs 2012 zdroj](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

Ukazuje, jak zkopírovat entitu odpovědi (tj. tělo odpovědi HTTP) do místního souboru před tím, než se přenáší klientovi a provede se asynchronní zpracování tohoto souboru. Ukázka implementuje **HttpMessageHandler** , který zabalí entitu Response s použitím samotného zápisu do výstupu jako normálního a do místního souboru.

**Nahrát ukázku XDocument** | [podrobný popis](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [vs 2012 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)

Ukazuje, jak nahrát XDocument do **ApiController** pomocí **PushStreamContent** a **HttpClient**.

**Ukázka ověření** | [zdroj vs 2010](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

Ukazuje, jak můžete pomocí atributů ověřování v modelech v ASP.NET WebAPI ověřit obsah požadavku HTTP. Ukazuje, jak označit vlastnosti jako povinné, jak použít jak atributy definované rozhraním, tak i vlastní ověřovací atributy k přidání poznámky k modelu a jak vracet chybové odpovědi pro neplatné stavy modelu.

**Ukázka webového formuláře** | [podrobný popis](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [vs 2010 source](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)

Zobrazuje ApiController přidaný do projektu webových formulářů.

**[Ukázka RestBugs](https://github.com/howarddierking/RestBugs)**

RestBugs je jednoduchá aplikace pro sledování chyb, která ukazuje, jak používat webové rozhraní API ASP.NET a novou knihovnu klienta HTTP k vytvoření systému založeného na médiích. Ukázka zahrnuje implementace klienta i serveru pomocí webového rozhraní API ASP.NET. Server používá vlastní formátovací modul Razor ke generování reprezentace prostředků. Ukázka také poskytuje server Node. js pro ilustraci výhod, které pocházejí z použití návrhu pomocí a k oddělit klienty a servery.
