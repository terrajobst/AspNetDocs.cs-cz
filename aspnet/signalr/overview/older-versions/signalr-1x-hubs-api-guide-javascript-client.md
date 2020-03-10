---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: Průvodce rozhraním API rozbočovače 1. x – klient JavaScriptu | Microsoft Docs
author: bradygaster
description: V tomto dokumentu najdete Úvod k používání rozhraní API centra pro Signal verze 1,1 v klientech JavaScript, jako jsou prohlížeče a Windows Store (WinJS) APPLIC...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 24850fe5229490bf600e09ad4718abb575a845fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536440"
---
# <a name="signalr-1x-hubs-api-guide---javascript-client"></a>Pokyny k rozhraní API center SignalR 1.x – javascriptový klient

autorem [Fletcher](https://github.com/pfletcher), který [Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> V tomto dokumentu najdete Úvod k používání rozhraní API centra pro Signal verze 1,1 v klientech JavaScript, jako jsou prohlížeče a aplikace Windows Store (WinJS).
> 
> Rozhraní API pro centra signalizace vám umožní provádět Vzdálená volání procedur (RPC) ze serveru pro připojené klienty a klienty na server. V kódu serveru můžete definovat metody, které mohou být volány klienty, a volat metody, které jsou spouštěny v klientovi. V kódu klienta definujete metody, které mohou být volány ze serveru, a voláte metody, které jsou spuštěny na serveru. Signalizace postará o všechny instalace klienta na server za vás.
> 
> Nástroj Signal také nabízí nižší úroveň rozhraní API označované jako trvalá připojení. Úvod do nástroje pro signalizaci, centra a trvalá připojení nebo v kurzu, který ukazuje, jak sestavit kompletní aplikaci signalizace, najdete v tématu [signaler-Začínáme](../getting-started/index.md).

## <a name="overview"></a>Přehled

Tento dokument obsahuje následující části:

- [Vygenerovaný proxy server a k čemu](#genproxy)

    - [Kdy použít generovaný proxy server](#cantusegenproxy)
- [Instalace klienta](#clientsetup)

    - [Postup odkazu na dynamicky generovaný proxy server](#dynamicproxy)
    - [Jak vytvořit fyzický soubor pro proxy vygenerovaný signálem](#manualproxy)
- [Jak navázat připojení](#establishconnection)

    - [$. Connection. hub je stejný objekt, který vytváří $. hubConnection ().](#connequivalence)
    - [Asynchronní provádění metody Start](#asyncstart)
- [Jak navázat připojení mezi doménami](#crossdomain)
- [Konfigurace připojení](#configureconnection)

    - [Určení parametrů řetězce dotazu](#querystring)
    - [Určení způsobu přenosu](#transport)
- [Jak získat proxy pro třídu centra](#getproxy)
- [Jak definovat metody v klientovi, které může server volat](#callclient)
- [Postup volání metod serveru z klienta](#callserver)
- [Postup zpracování událostí životního cyklu připojení](#connectionlifetime)
- [Zpracování chyb](#handleerrors)
- [Postup povolení protokolování na straně klienta](#logging)

Dokumentaci k programování serveru nebo klientů rozhraní .NET najdete v následujících zdrojích informací:

- [Průvodce rozhraním API pro centra signálů – Server](../guide-to-the-api/hubs-api-guide-server.md)
- [Průvodce rozhraním API pro centra signálů – klient .NET](../guide-to-the-api/hubs-api-guide-net-client.md)

Odkazy na referenční témata rozhraní API odkazují na verzi rozhraní API .NET 4,5. Pokud používáte .NET 4, přečtěte si téma věnované [verzi rozhraní API rozhraní .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>Vygenerovaný proxy server a k čemu

Můžete programovat klienta JavaScriptu ke komunikaci se službou signalizace s nebo bez proxy serveru, který vygeneroval signál. K čemu je proxy pro vás jednodušší syntaxe kódu, který používáte k připojení, zápisu metod, které server volá, a volání metod na serveru.

Při psaní kódu pro volání metod serveru, vygenerovaný proxy vám umožní použít syntaxi, která vypadá jako při provádění místní funkce: můžete napsat `serverMethod(arg1, arg2)` místo `invoke('serverMethod', arg1, arg2)`. Syntaxe vygenerovaného proxy serveru také umožňuje okamžitou a srozumitelnou chybu na straně klienta, pokud zadáte chybné zadání názvu metody serveru. A pokud ručně vytvoříte soubor, který definuje proxy, můžete také získat podporu technologie IntelliSense pro psaní kódu, který volá metody serveru.

Předpokládejme například, že máte na serveru následující třídu centra:

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

Následující příklady kódu ukazují, jaký kód jazyka JavaScript vypadá za vyvolání metody `NewContosoChatMessage` na serveru a přijímání vyvolání `addContosoChatMessageToPage` metody ze serveru.

**S vygenerovaným proxy serverem**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**Bez vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>Kdy použít generovaný proxy server

Pokud chcete registrovat více obslužných rutin událostí pro metodu klienta, kterou server volá, nemůžete použít vygenerovaný proxy server. V opačném případě můžete zvolit používání vygenerovaného proxy serveru nebo ne na základě předvolby kódování. Pokud se rozhodnete, že ji nepoužíváte, nemusíte odkazovat na adresu URL "signaler/Hubs" v prvku `script` ve vašem klientském kódu.

<a id="clientsetup"></a>

## <a name="client-setup"></a>Instalace klienta

JavaScriptový klient vyžaduje odkazy na jQuery a základní soubor JavaScriptu pro signál. Verze jQuery musí být 1.6.4 nebo hlavní novější verze, jako je například 1.7.2, 1.8.2 nebo 1.9.1. Pokud se rozhodnete použít vygenerovaný proxy server, budete také potřebovat odkaz na soubor JavaScriptu proxy vygenerovaný signálem. Následující příklad ukazuje, jak odkazy mohou vypadat jako na stránce HTML, která používá vygenerovaný proxy server.

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

Tyto odkazy musí být zahrnuté v tomto pořadí: jQuery First, Signal Core po tomto případě a proxy signalizace jako poslední.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>Postup odkazu na dynamicky generovaný proxy server

V předchozím příkladu odkazuje odkaz na proxy server vygenerovaný signálem k dynamickému generování kódu JavaScriptu, nikoli fyzického souboru. Návěstí vytvoří kód JavaScriptu pro proxy a zachová ho klientovi v reakci na adresu URL "/SignalR/Hubs". Pokud jste zadali jinou základní adresu URL pro připojení k signalizaci na serveru v metodě `MapHubs`, adresa URL dynamicky generovaného souboru proxy je vaše vlastní adresa URL s připojeným "/Hubs".

> [!NOTE]
> Pro klienty se systémem Windows 8 (Windows Store) v jazyce JavaScript použijte místo dynamicky generovaného souboru fyzický proxy soubor. Další informace najdete v části [Postup vytvoření fyzického souboru pro proxy vygenerovaný signálem](#manualproxy) dále v tomto tématu.

V zobrazení ASP.NET MVC 4 Razor použijte vlnovku pro odkaz na kořen aplikace v referenčním souboru proxy:

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

Další informace o použití signalizace v MVC 4 najdete v tématu [Začínáme s nástrojem Signal a MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).

V zobrazení ASP.NET MVC 3 Razor použijte `Url.Content` pro referenci proxy souboru:

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

V aplikaci webových formulářů ASP.NET použijte `ResolveClientUrl` pro odkaz na soubor proxy a zaregistrujte ho prostřednictvím ovládacího prvku ScriptManager pomocí relativní cesty ke kořenu aplikace (počínaje vlnovkou tildy):

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

Jako obecné pravidlo použijte stejnou metodu pro zadání adresy URL "/SignalR/Hubs", kterou používáte pro soubory CSS nebo JavaScript. Pokud zadáte adresu URL bez použití tildy, v některých případech bude vaše aplikace správně fungovat při testování v aplikaci Visual Studio pomocí IIS Express, ale při nasazení na plnou službu IIS dojde k chybě 404. Další informace naleznete v tématu **řešení odkazů na prostředky kořenové úrovně** ve [webových serverech v aplikaci Visual Studio pro webové projekty ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx) na webu MSDN.

Při spuštění webového projektu v aplikaci Visual Studio 2012 v režimu ladění a pokud jako prohlížeč používáte Internet Explorer, můžete zobrazit soubor proxy v **Průzkumník řešení** v části **dokumenty skriptu**, jak je znázorněno na následujícím obrázku.

![JavaScriptový soubor generovaný v JavaScriptu v Průzkumník řešení](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

Pokud chcete zobrazit obsah souboru, poklikejte na **rozbočovače**. Pokud nepoužíváte sadu Visual Studio 2012 a Internet Explorer nebo pokud nejste v režimu ladění, můžete obsah souboru získat také tak, že přejdete na adresu URL/signalR/hubs. Například pokud vaše lokalita běží na `http://localhost:56699`, v prohlížeči se podívejte na `http://localhost:56699/SignalR/hubs`.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>Jak vytvořit fyzický soubor pro proxy vygenerovaný signálem

Jako alternativu k dynamicky vygenerovanému proxy serveru můžete vytvořit fyzický soubor, který má kód proxy a odkazovat na tento soubor. To může být vhodné pro kontrolu nad ukládáním do mezipaměti nebo sdružování nebo pro získání IntelliSense při kódování volání do metod serveru.

Chcete-li vytvořit soubor proxy, proveďte následující kroky:

1. Nainstalujte balíček NuGet [Microsoft. ASPNET. signaler. util](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) .
2. Otevřete příkazový řádek a přejděte do složky *nástroje* , která obsahuje soubor Signal. exe. Složka nástroje je v následujícím umístění:

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. Zadejte následující příkaz:

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    Cesta k souboru *. dll* je obvykle složka *bin* ve složce projektu.

    Tento příkaz vytvoří soubor s názvem *Server. js* ve stejné složce jako *Signal. exe*.
4. Vložte soubor *Server. js* do příslušné složky v projektu, přejmenujte jej podle potřeby pro vaši aplikaci a přidejte odkaz na něj místo odkazu "signál/rozbočovačé".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Jak navázat připojení

Než budete moct navázat připojení, musíte vytvořit objekt připojení, vytvořit proxy server a zaregistrovat obslužné rutiny událostí pro metody, které je možné volat ze serveru. Když jsou nastaveny obslužné rutiny proxy a událostí, navažte připojení voláním metody `start`.

Pokud používáte generovaný proxy server, nemusíte vytvářet objekt připojení ve vlastním kódu, protože vygenerovaný kód proxy to udělá za vás.

<a id="nogenconnection"></a>

**Navázat připojení (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**Navázat připojení (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

Vzorový kód pro připojení ke službě signalizace používá výchozí adresu URL "/SignalR". Informace o tom, jak zadat jinou základní adresu URL, najdete v tématu [Průvodce rozhraním API pro centra ASP.NET Signal-Server-adresa URL/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).

> [!NOTE]
> Normálně zaregistrujete obslužné rutiny události před voláním metody `start` pro navázání připojení. Pokud chcete registrovat některé obslužné rutiny události po navázání připojení, můžete to provést, ale před voláním metody `start` je nutné zaregistrovat alespoň jednu obslužnou rutinu události. Jedním z důvodů je, že v aplikaci může být mnoho Center, ale pokud se k jednomu z nich budete chtít používat jenom jednu z nich, nebudete chtít aktivovat `OnConnected` událost na každém centru. Když je připojení navázáno, přítomnost metody klienta v proxy serveru rozbočovače je tím, co oznamuje signalizaci, aby aktivoval událost `OnConnected`. Pokud nezaregistrujete žádné obslužné rutiny událostí před voláním metody `start`, budete moci vyvolat metody v centru, ale metoda `OnConnected` centra nebude volána a žádné metody klienta nebudou vyvolány ze serveru.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$. Connection. hub je stejný objekt, který vytváří $. hubConnection ().

Jak vidíte v příkladech, při použití generovaného proxy serveru `$.connection.hub` odkazuje na objekt připojení. Jedná se o stejný objekt, který získáte voláním `$.hubConnection()`, když nepoužíváte generovaný proxy server. Generovaný kód proxy vytvoří připojení za vás spuštěním následujícího příkazu:

![Vytvoření připojení ve vygenerovaném souboru proxy](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

Pokud používáte vygenerovaný proxy server, můžete s `$.connection.hub` provádět cokoli, co můžete dělat s objektem připojení, když nepoužíváte vygenerovaný proxy server.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>Asynchronní provádění metody Start

Metoda `start` se spouští asynchronně. Vrací [odložený objekt jQuery](http://api.jquery.com/category/deferred-object/), což znamená, že můžete přidat funkce zpětného volání voláním metod, jako jsou `pipe`, `done`a `fail`. Pokud máte kód, který chcete spustit po navázání spojení, jako je například volání metody serveru, vložte tento kód do funkce zpětného volání nebo jej zavolejte z funkce zpětného volání. Metoda zpětného volání `.done` se spustí po navázání připojení a po jakémkoli kódu, který máte v metodě obslužné rutiny události `OnConnected` na serveru, se dokončí provádění.

Pokud vložíte příkaz "nyní připojeno" z předchozího příkladu jako další řádek kódu po volání metody `start` (ne ve zpětném volání `.done`), bude řádek `console.log` spuštěn před navázáním připojení, jak je znázorněno v následujícím příkladu:

![Špatný způsob, jak napsat kód, který se spustí po navázání připojení](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>Jak navázat připojení mezi doménami

V případě, že prohlížeč načítá stránku z `http://contoso.com`, připojení k signalizaci je ve stejné doméně, v `http://contoso.com/signalr`. Pokud stránka z `http://contoso.com` vytvoří připojení k `http://fabrikam.com/signalr`, což je připojení mezi doménami. Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázaná. Pokud chcete vytvořit připojení mezi doménami, ujistěte se, že jsou na serveru povolená připojení mezi doménami, a při vytváření objektu připojení zadejte adresu URL připojení. Signál bude používat vhodnou technologii pro připojení mezi doménami, jako třeba [JSONP](http://en.wikipedia.org/wiki/JSONP) nebo [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).

Na serveru povolte připojení mezi doménami výběrem této možnosti při volání metody `MapHubs`.

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

Na straně klienta zadejte adresu URL při vytváření objektu připojení (bez vygenerovaného proxy serveru) nebo před voláním metody Start (s vygenerovaným proxy serverem).

**Kód klienta, který určuje připojení mezi doménami (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

**Kód klienta, který určuje připojení mezi doménami (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

Pokud použijete konstruktor `$.hubConnection`, nemusíte do adresy URL zahrnout `signalr`, protože se přidá automaticky (Pokud nezadáte `useDefaultUrl` jako `false`).

Můžete vytvořit více připojení k různým koncovým bodům.

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - Ve vašem kódu nenastavujte `jQuery.support.cors` na hodnotu true.
> 
>     ![Nenastavujte jQuery. support. Cors na hodnotu true](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     Návěstí zpracovává použití JSONP nebo CORS. Nastavením `jQuery.support.cors` na hodnotu true zakážete JSONP, protože to způsobuje, že signál bude předpokládat, že prohlížeč podporuje CORS.
> - Pokud se připojujete k adrese URL místního hostitele, Internet Explorer 10 ji nepovažuje za připojení mezi doménami, takže aplikace bude fungovat místně s IE 10, a to i v případě, že jste na serveru nepovolili připojení mezi doménami.
> - Informace o použití připojení mezi doménami s Internet Explorerem 9 najdete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).
> - Informace o použití připojení mezi doménami s Chrome najdete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).
> - Vzorový kód pro připojení ke službě signalizace používá výchozí adresu URL "/SignalR". Informace o tom, jak zadat jinou základní adresu URL, najdete v tématu [Průvodce rozhraním API pro centra ASP.NET Signal-Server-adresa URL/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Konfigurace připojení

Před navázáním připojení můžete zadat parametry řetězce dotazu nebo zadat metodu přenosu.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Určení parametrů řetězce dotazu

Pokud chcete při připojení klienta odesílat data na server, můžete do objektu připojení přidat parametry řetězce dotazu. Následující příklady ukazují, jak nastavit parametr řetězce dotazu v kódu klienta.

**Před voláním metody Start (s vygenerovaným proxy serverem) nastavte hodnotu řetězce dotazu.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

**Před voláním metody Start (bez vygenerovaného proxy serveru) nastavte hodnotu řetězce dotazu.**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Určení způsobu přenosu

V rámci procesu připojování klient signalizace obvykle vyjednává se serverem, aby bylo možné určit nejlepší přenos, který je podporovaný oběma servery i klientem. Pokud již víte, který přenos chcete použít, můžete tento proces vyjednávání obejít zadáním metody přenosu při volání metody `start`.

**Kód klienta, který určuje způsob přenosu (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**Kód klienta, který určuje způsob přenosu (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

Jako alternativu můžete zadat více metod přenosu v pořadí, ve kterém chcete, aby je Signal mohl vyzkoušet:

**Kód klienta, který určuje vlastní záložní schéma přenosu (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

**Kód klienta, který určuje vlastní záložní schéma přenosu (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

K určení metody přenosu můžete použít následující hodnoty:

- WebSockets
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

Následující příklady ukazují, jak zjistit, která metoda přenosu je používána připojením.

**Kód klienta, který zobrazuje přenosovou metodu používanou připojením (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

**Kód klienta, který zobrazuje přenosovou metodu používanou připojením (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

Informace o tom, jak zjistit způsob přenosu v serverovém kódu, najdete v tématu [Průvodce rozhraním API centra ASP.NET Signal-Server – jak z kontextové vlastnosti získat informace o klientovi](../guide-to-the-api/hubs-api-guide-server.md#contextproperty). Další informace o přenosech a náhradních přenosech najdete v tématu [Úvod k signalizaci a záložním přenosům](../getting-started/introduction-to-signalr.md#transports).

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>Jak získat proxy pro třídu centra

Každý objekt připojení, který vytvoříte, zapouzdřuje informace o připojení ke službě signalizace, která obsahuje jednu nebo více tříd centra. Aby bylo možné komunikovat s třídou centra, použijte proxy objekt, který můžete vytvořit sami (Pokud nepoužíváte generovaný proxy server), nebo který je vygenerován za vás.

Na straně klienta je názvem proxy verze ve stylu CamelCase-použita s názvem třídy centra. Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.

**Třída centra na serveru**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

**Získat odkaz na vygenerovaný klientský proxy server pro centrum**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

**Vytvoření klientského proxy serveru pro třídu centra (bez vygenerovaného proxy serveru)**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

Pokud třídu centra seřadíte pomocí atributu `HubName`, použijte přesný název bez změny velikosti písmen.

**Třída centra na serveru s atributem HubName**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

**Získat odkaz na vygenerovaný klientský proxy server pro centrum**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

**Vytvoření klientského proxy serveru pro třídu centra (bez vygenerovaného proxy serveru)**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Jak definovat metody v klientovi, které může server volat

Chcete-li definovat metodu, kterou může server volat z centra, přidejte obslužnou rutinu události do proxy serveru centra pomocí vlastnosti `client` generovaného proxy serveru nebo volejte metodu `on`, pokud nepoužíváte generovaný proxy server. Parametry mohou být složité objekty.

Přidejte obslužnou rutinu události před voláním metody `start` k navázání připojení. (Pokud chcete přidat obslužné rutiny událostí po volání metody `start`, přečtěte si poznámku v tématu [jak navázat připojení](#establishconnection) dříve v tomto dokumentu a použít syntaxi zobrazenou pro definování metody bez použití vygenerovaného proxy serveru.)

Porovnávání názvů metod nerozlišuje velká a malá písmena. Například `Clients.All.addContosoChatMessageToPage` na serveru spustí `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`nebo `addcontosochatmessagetopage` na klientovi.

**Definovat metodu na klientovi (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

**Alternativní způsob definování metody v klientovi (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

**Definovat metodu na klientovi (bez vygenerovaného proxy serveru nebo při přidání po volání metody Start)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

**Serverový kód, který volá metodu klienta**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

Následující příklady zahrnují komplexní objekt jako parametr metody.

**Metoda define pro klienta, který přebírá složitý objekt (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

**Definovat metodu u klienta, který přebírá složitý objekt (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

**Kód serveru, který definuje komplexní objekt**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

**Serverový kód, který volá metodu klienta pomocí složitého objektu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Postup volání metod serveru z klienta

Chcete-li volat metodu serveru z klienta, použijte vlastnost `server` vygenerovaného proxy serveru nebo metody `invoke` na serveru proxy centra, pokud nepoužíváte generovaný proxy server. Návratová hodnota nebo parametry mohou být složité objekty.

Předejte ve stylu CamelCase verzi názvu metody v centru. Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.

Následující příklady ukazují, jak zavolat metodu serveru, která nemá návratovou hodnotu a jak zavolat metodu serveru, která má návratovou hodnotu.

**Metoda serveru bez atributu HubMethodName**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

**Serverový kód, který definuje složitý objekt předaný do parametru**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

**Kód klienta, který vyvolá metodu serveru (u generovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

**Kód klienta, který vyvolá metodu serveru (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

Pokud jste upravili metodu centra s atributem `HubMethodName`, použijte tento název bez změny velikosti písmen.

**Metoda serveru** s atributem HubMethodName

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

**Kód klienta, který vyvolá metodu serveru (u generovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

**Kód klienta, který vyvolá metodu serveru (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

Předchozí příklady ukazují, jak zavolat metodu serveru, která nemá žádnou návratovou hodnotu. Následující příklady ukazují, jak zavolat metodu serveru, která má návratovou hodnotu.

**Serverový kód pro metodu, která má návratovou hodnotu**

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

**Skladová Třída použitá pro** návratovou hodnotu

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

**Kód klienta, který vyvolá metodu serveru (u generovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

**Kód klienta, který vyvolá metodu serveru (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Postup zpracování událostí životního cyklu připojení

Signál poskytuje následující události doby života připojení, které můžete zpracovat:

- `starting`: je aktivována před odesláním dat prostřednictvím připojení.
- `received`: Vyvolá se, když jsou v připojení přijata nějaká data. Poskytuje přijatá data.
- `connectionSlow`: Vyvolá se, když klient zjistí pomalé nebo často vyřazování připojení.
- `reconnecting`: Vyvolá se, když se zahájí opětovné připojení podkladového přenosu.
- `reconnected`: Vyvolá se, když se znovu připojí příslušný přenos.
- `stateChanged`: Vyvolá se při změně stavu připojení. Poskytuje starý stav a nový stav (připojení, připojení, opětovné připojení nebo odpojení).
- `disconnected`: Vyvolá se, když se připojení odpojilo.

Například pokud chcete zobrazovat upozornění, pokud dojde k problémům s připojením, které by mohly způsobit znatelné zpoždění, zpracujte událost `connectionSlow`.

**Zpracování události connectionSlow (u generovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

**Zpracování události connectionSlow (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení v nástroji Signal](index.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Zpracování chyb

Klient služby Signal JavaScript poskytuje `error` událost, pro kterou můžete přidat obslužnou rutinu pro. Můžete také použít metodu selhání k přidání obslužné rutiny pro chyby, které jsou výsledkem vyvolání metody serveru.

Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který Signal vrátí po chybě, obsahuje minimální informace o chybě. Například pokud se volání `newContosoChatMessage` nepovede, chybová zpráva v objektu Error obsahuje "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" odesílání podrobných chybových zpráv klientům v produkčním prostředí se z bezpečnostních důvodů nedoporučuje, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

Následující příklad ukazuje, jak přidat obslužnou rutinu pro událost Error.

**Přidání obslužné rutiny chyb (s vygenerovaným proxy serverem)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

**Přidání obslužné rutiny chyb (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

Následující příklad ukazuje, jak zpracovat chybu z vyvolání metody.

**Zpracování chyby z vyvolání metody (u generovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

**Zpracování chyby od vyvolání metody (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

Pokud se volání metody nezdařilo, je vyvolána také událost `error`, takže váš kód v obslužné rutině metody `error` a ve zpětném volání metody `.fail` by se spustil.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Postup povolení protokolování na straně klienta

Chcete-li povolit protokolování na straně klienta pro připojení, nastavte vlastnost `logging` objektu Connection před voláním metody `start` k navázání připojení.

**Povolit protokolování (u generovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

**Povolit protokolování (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

Protokoly zobrazíte tak, že otevřete vývojářské nástroje v prohlížeči a přejdete na kartu konzola. Kurz, který obsahuje podrobné pokyny a snímky obrazovky, které ukazují, jak to udělat, najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal – povolení protokolování](index.md).
