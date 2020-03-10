---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: Průvodce rozhraním API pro centra ASP.NET Signaler –C#klient .NET () | Microsoft Docs
author: bradygaster
description: V tomto dokumentu najdete Úvod k používání rozhraní API centra pro službu Signal verze 2 v klientech rozhraní .NET, jako je Windows Store (WinRT), WPF, Silverlight a nevýhody...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578790"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>Průvodce rozhraním API pro centra ASP.NET Signaler –C#klient .NET ()

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> V tomto dokumentu najdete Úvod k používání rozhraní API centra pro službu Signal verze 2 v klientech rozhraní .NET, jako je Windows Store (WinRT), WPF, Silverlight a konzolové aplikace.
>
> Rozhraní API pro centra signalizace vám umožní provádět Vzdálená volání procedur (RPC) ze serveru pro připojené klienty a klienty na server. V kódu serveru můžete definovat metody, které mohou být volány klienty, a volat metody, které jsou spouštěny v klientovi. V kódu klienta definujete metody, které mohou být volány ze serveru, a voláte metody, které jsou spuštěny na serveru. Signalizace postará o všechny instalace klienta na server za vás.
>
> Nástroj Signal také nabízí nižší úroveň rozhraní API označované jako trvalá připojení. Úvod do nástroje pro signalizaci, centra a trvalá připojení nebo v kurzu, který ukazuje, jak sestavit kompletní aplikaci signalizace, najdete v tématu [signaler-Začínáme](../getting-started/index.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - Signal – verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Tento dokument obsahuje následující části:

- [Instalace klienta](#clientsetup)
- [Jak navázat připojení](#establishconnection)

    - [Připojení mezi doménami z klientů Silverlight](#slcrossdomain)
- [Konfigurace připojení](#configureconnection)

    - [Nastavení maximálního počtu souběžných připojení v klientech WPF](#maxconnections)
    - [Určení parametrů řetězce dotazu](#querystring)
    - [Určení způsobu přenosu](#transport)
    - [Určení hlaviček protokolu HTTP](#httpheaders)
    - [Určení klientských certifikátů](#clientcertificate)
- [Postup vytvoření centrálního proxy serveru](#proxy)
- [Jak definovat metody v klientovi, které může server volat](#callclient)

    - [Metody bez parametrů](#clientmethodswithoutparms)
    - [Metody s parametry, které určují typy parametrů](#clientmethodswithparmtypes)
    - [Metody s parametry, které určují dynamické objekty pro parametry](#clientmethodswithdynamparms)
    - [Postup odebrání obslužné rutiny](#removehandler)
- [Postup volání metod serveru z klienta](#callserver)
- [Postup zpracování událostí životního cyklu připojení](#connectionlifetime)
- [Zpracování chyb](#handleerrors)
- [Postup povolení protokolování na straně klienta](#logging)
- [Ukázky kódu aplikace WPF, Silverlight a konzolových aplikací pro metody klienta, které může server volat](#wpfsl)

Ukázkové klientské projekty rozhraní .NET najdete v následujících zdrojích informací:

- [Gustavo-armenta/signaler – ukázky](https://github.com/gustavo-armenta/SignalR-Samples) v GitHub.com (WinRT, Silverlight, příklady konzolových aplikací).
- [DamianEdwards/signaler-MoveShapeDemo/MoveShape. Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (příklad WPF)
- [Signaler/Microsoft. ASPNET. signale. Client. Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (příklad aplikace konzoly).

Dokumentaci k programování klientů serveru nebo JavaScriptu najdete v následujících zdrojích informací:

- [Průvodce rozhraním API pro centra signálů – Server](hubs-api-guide-server.md)
- [Průvodce rozhraním API pro centra signálů – JavaScriptový klient](hubs-api-guide-javascript-client.md)

Odkazy na referenční témata rozhraní API odkazují na verzi rozhraní API .NET 4,5. Pokud používáte .NET 4, přečtěte si téma věnované [verzi rozhraní API rozhraní .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="clientsetup"></a>

## <a name="client-setup"></a>Instalace klienta

Nainstalujte balíček NuGet [Microsoft. ASPNET. Signal. Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) (ne balíček [Microsoft. ASPNET. signaler](http://nuget.org/packages/microsoft.aspnet.signalr) ). Tento balíček podporuje klienty WinRT, Silverlight, WPF, konzolová aplikace a Windows Phone pro rozhraní .NET 4 i .NET 4,5.

Pokud je verze nástroje Signal, kterou jste na klientovi, odlišná od verze, kterou máte na serveru, je často možné, že se k rozdílu přizpůsobuje signál. Například server, na kterém je spuštěný Signal, verze 2, bude podporovat klienty, kteří mají nainstalované verze 1.1. x, a taky klienty, kteří mají nainstalovanou verzi 2. Pokud je rozdíl mezi verzí na serveru a verzí v klientovi moc velký nebo pokud je klient novější než server, Signal vyvolá výjimku `InvalidOperationException`, když se klient pokusí navázat připojení. Chybová zpráva je "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Jak navázat připojení

Než budete moct navázat připojení, musíte vytvořit objekt `HubConnection` a vytvořit proxy. Chcete-li vytvořit připojení, zavolejte metodu `Start` u objektu `HubConnection`.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> Pro klienty jazyka JavaScript musíte zaregistrovat alespoň jednu obslužnou rutinu události před voláním metody `Start` pro navázání připojení. Není to nutné pro klienty rozhraní .NET. V případě klientů v jazyce JavaScript vygenerovaný kód proxy automaticky vytvoří proxy pro všechna centra, která existují na serveru, a registruje obslužnou rutinu, jak označíte, která centra vaše klienti mají použít. Ale u klienta .NET vytvoříte proxy rozbočovače ručně, takže signál předpokládá, že budete používat libovolné centrum, pro které vytvoříte proxy server.

Vzorový kód pro připojení ke službě signalizace používá výchozí adresu URL "/SignalR". Informace o tom, jak zadat jinou základní adresu URL, najdete v tématu [Průvodce rozhraním API pro centra ASP.NET Signal-Server-adresa URL/SignalR](hubs-api-guide-server.md#signalrurl).

Metoda `Start` se spouští asynchronně. Chcete-li zajistit, že následné řádky kódu nebudou vykonány až po navázání spojení, použijte `await` v asynchronní metodě ASP.NET 4,5 nebo `.Wait()` v synchronní metodě. Nepoužívejte `.Wait()` v klientovi WinRT.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Připojení mezi doménami z klientů Silverlight

Informace o tom, jak povolit mezidoménová připojení z klientů programu Silverlight, najdete v tématu [zajištění dostupnosti služby napříč hranicemi domén](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Konfigurace připojení

Před navázáním připojení můžete zadat některou z následujících možností:

- Omezení počtu souběžných připojení.
- Parametry řetězce dotazu.
- Způsob přenosu.
- Hlavičky protokolu HTTP.
- Klientské certifikáty.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>Nastavení maximálního počtu souběžných připojení v klientech WPF

V klientech WPF možná budete muset zvýšit maximální počet souběžných připojení od výchozí hodnoty 2. Doporučená hodnota je 10.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

Další informace najdete v tématu [Třída ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Určení parametrů řetězce dotazu

Pokud chcete při připojení klienta odesílat data na server, můžete do objektu připojení přidat parametry řetězce dotazu. Následující příklad ukazuje, jak nastavit parametr řetězce dotazu v kódu klienta.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Určení způsobu přenosu

V rámci procesu připojování klient signalizace obvykle vyjednává se serverem, aby bylo možné určit nejlepší přenos, který je podporovaný oběma servery i klientem. Pokud už víte, kterou přenos chcete použít, můžete tento proces vyjednávání obejít. Chcete-li určit metodu transportu, předejte objekt přenosu do metody Start. Následující příklad ukazuje, jak určit metodu přenosu v kódu klienta.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

Obor názvů [Microsoft. ASPNET. Signal. Client. Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) obsahuje následující třídy, které lze použít k určení přenosu.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (k dispozici pouze v případě, že server i klient používají .NET 4,5)
- Automatický [přenos](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (automaticky zvolí nejlepší přenos, který je podporován klientem i serverem. Toto je výchozí přenos. Předání do metody `Start` má stejný účinek, jako by neprošlo cokoli.)

Přenos ForeverFrame není v tomto seznamu zahrnutý, protože ho používají jenom prohlížeče.

Informace o tom, jak zjistit způsob přenosu v serverovém kódu, najdete v tématu [Průvodce rozhraním API centra ASP.NET Signal-Server – jak z kontextové vlastnosti získat informace o klientovi](hubs-api-guide-server.md#contextproperty). Další informace o přenosech a náhradních přenosech najdete v tématu [Úvod k signalizaci a záložním přenosům](../getting-started/introduction-to-signalr.md#transports).

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>Určení hlaviček protokolu HTTP

K nastavení hlaviček protokolu HTTP použijte vlastnost `Headers` objektu Connection. Následující příklad ukazuje, jak přidat hlavičku HTTP.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>Určení klientských certifikátů

Chcete-li přidat klientské certifikáty, použijte metodu `AddClientCertificate` objektu Connection.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Postup vytvoření centrálního proxy serveru

Chcete-li definovat metody v klientovi, které může centrum volat ze serveru, a vyvolat metody v centru na serveru, vytvořte proxy serveru pro centrum voláním `CreateHubProxy` na objektu Connection. Řetězec, který předáte do `CreateHubProxy`, je název vaší třídy centra nebo název určený atributem `HubName`, pokud se na serveru použila jedna. Shoda názvů nerozlišuje malá a velká písmena.

**Třída centra na serveru**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Vytvoření klientského proxy serveru pro třídu centra**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

Pokud třídu centra seřadíte pomocí atributu `HubName`, použijte tento název.

**Třída centra na serveru**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**Vytvoření klientského proxy serveru pro třídu centra**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

Pokud zavoláte `HubConnection.CreateHubProxy` vícekrát se stejným `hubName`, dostanete stejný objekt `IHubProxy` v mezipaměti.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Jak definovat metody v klientovi, které může server volat

Chcete-li definovat metodu, kterou může server volat, použijte metodu `On` proxy k registraci obslužné rutiny události.

Porovnávání názvů metod nerozlišuje velká a malá písmena. Například `Clients.All.UpdateStockPrice` na serveru spustí `updateStockPrice`, `updatestockprice`nebo `UpdateStockPrice` na klientovi.

Různé klientské platformy mají různé požadavky na způsob psaní kódu metody pro aktualizaci uživatelského rozhraní. Uvedené příklady jsou pro klienty WinRT (Windows Store .NET). Příklady WPF, Silverlight a konzolových aplikací jsou k dispozici v [samostatném oddílu dále v tomto tématu](#wpfsl).

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Metody bez parametrů

Pokud metoda, kterou právě zpracováváte, nemá parametry, použijte neobecné přetížení metody `On`:

**Serverový kód, který volá metodu klienta bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**Klientský kód WinRT pro metodu volanou ze serveru bez parametrů ([viz příklady WPF a Silverlight dále v tomto tématu](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Metody s parametry, které určují typy parametrů

Pokud má zpracovávaná metoda parametry, zadejte typy parametrů jako obecné typy metody `On`. Existují obecná přetížení metody `On`, která vám umožní zadat až 8 parametrů (4 v Windows Phone 7). V následujícím příkladu je jeden parametr odeslán do metody `UpdateStockPrice`.

**Serverový kód, který volá metodu klienta s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**Třída akcie použitá pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**Klientský kód WinRT pro metodu volanou ze serveru s parametrem ([viz příklady WPF a Silverlight dále v tomto tématu](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Metody s parametry, které určují dynamické objekty pro parametry

Jako alternativu k určení parametrů jako obecných typů `On` metody můžete zadat parametry jako dynamické objekty:

**Serverový kód, který volá metodu klienta s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**Třída akcie použitá pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**Klientský kód WinRT pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr ([viz příklady WPF a Silverlight dále v tomto tématu](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>Postup odebrání obslužné rutiny

Chcete-li odebrat obslužnou rutinu, zavolejte metodu `Dispose`.

**Klientský kód pro metodu volanou ze serveru**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**Klientský kód pro odebrání obslužné rutiny**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Postup volání metod serveru z klienta

Chcete-li volat metodu na serveru, použijte metodu `Invoke` na serveru proxy centra.

Pokud metoda serveru nemá žádnou návratovou hodnotu, použijte neobecné přetížení metody `Invoke`.

**Serverový kód pro metodu, která nemá žádnou návratovou hodnotu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**Klientský kód volá metodu, která nemá žádnou návratovou hodnotu.**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Pokud má metoda serveru návratovou hodnotu, zadejte návratový typ jako obecný typ metody `Invoke`.

**Serverový kód pro metodu, která má návratovou hodnotu a má parametr komplexního typu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**Třída akcie použitá pro parametr a návratovou hodnotu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**Klientský kód volá metodu, která má návratovou hodnotu a přebírá parametr komplexního typu v asynchronní metodě ASP.NET 4,5.**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Klientský kód, který volá metodu, která má návratovou hodnotu a přebírá parametr komplexního typu, v synchronní metodě**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

Metoda `Invoke` se spustí asynchronně a vrátí objekt `Task`. Pokud nezadáte `await` nebo `.Wait()`, bude další řádek kódu proveden před tím, než byla vyvolaná metoda dokončena.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Postup zpracování událostí životního cyklu připojení

Signál poskytuje následující události doby života připojení, které můžete zpracovat:

- `Received`: Vyvolá se, když jsou v připojení přijata nějaká data. Poskytuje přijatá data.
- `ConnectionSlow`: Vyvolá se, když klient zjistí pomalé nebo často vyřazování připojení.
- `Reconnecting`: Vyvolá se, když se zahájí opětovné připojení podkladového přenosu.
- `Reconnected`: Vyvolá se, když se znovu připojí příslušný přenos.
- `StateChanged`: Vyvolá se při změně stavu připojení. Poskytuje starý stav a nový stav. Informace o hodnotách stavu připojení naleznete v tématu [vlastnost ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).
- `Closed`: Vyvolá se, když se připojení odpojilo.

Například pokud chcete zobrazovat upozornění na chyby, které nejsou závažné, ale způsobují přerušované problémy s připojením, například pomalé nebo časté připojení, zpracujte událost `ConnectionSlow`.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení v nástroji Signal](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Zpracování chyb

Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který Signal vrátí po chybě, obsahuje minimální informace o chybě. Například pokud se volání `newContosoChatMessage` nepovede, chybová zpráva v objektu Error obsahuje "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" odesílání podrobných chybových zpráv klientům v produkčním prostředí se z bezpečnostních důvodů nedoporučuje, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

Chcete-li zpracovat chyby, které signalizace vyvolá, můžete přidat obslužnou rutinu pro událost `Error` objektu Connection.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

Chcete-li zpracovat chyby z vyvolání metod, zabalte kód do bloku try-catch.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Postup povolení protokolování na straně klienta

Pokud chcete povolit protokolování na straně klienta, nastavte `TraceLevel` a vlastnosti `TraceWriter` objektu připojení.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>Ukázky kódu aplikace WPF, Silverlight a konzolových aplikací pro metody klienta, které může server volat

Ukázky kódu uvedené dříve pro definování metod klienta, které může server volat, se vztahují na klienty WinRT. Následující ukázky znázorňují ekvivalentní kód pro klienty WPF, Silverlight a konzolových aplikací.

### <a name="methods-without-parameters"></a>Metody bez parametrů

**Kód klienta WPF pro metodu volanou ze serveru bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Kód klienta Silverlight pro metodu volanou ze serveru bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Klientský kód konzolové aplikace pro metodu volanou ze serveru bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Metody s parametry, které určují typy parametrů

**Kód klienta WPF pro metodu volanou ze serveru s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Klientský kód konzolové aplikace pro metodu volanou ze serveru s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Metody s parametry, které určují dynamické objekty pro parametry

**Kód klienta WPF pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Klientský kód konzolové aplikace pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
