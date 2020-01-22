---
uid: signalr/overview/getting-started/introduction-to-signalr
title: Úvod do signalizace | Microsoft Docs
author: bradygaster
description: Tento článek popisuje, co je signalizace a některá z řešení, která byla navržena pro vytvoření.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519398"
---
# <a name="introduction-to-signalr"></a>Úvod ke knihovně SignalR

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek popisuje, co je signalizace a některá z řešení, která byla navržena pro vytvoření. 
> 
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
> 
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).

## <a name="what-is-signalr"></a>Co je signál?

ASP.NET Signal je knihovna pro vývojáře v ASP.NET, která zjednodušuje proces přidávání webových funkcí v reálném čase do aplikací. Webová funkce v reálném čase je možnost, aby server nabízel obsah nabízeného oznámení připojeným klientům hned, jakmile bude k dispozici, místo toho, aby server čekal na vyžádání nových dat klientem.

Pomocí signálu lze do aplikace ASP.NET přidat libovolný druh webové funkce v reálném čase. I když se chat často používá jako příklad, můžete si udělat spoustu dalších. Pokaždé, když uživatel aktualizuje webovou stránku, aby zobrazil nová data, nebo pokud stránka implementuje [dlouhé cyklické dotazování](http://en.wikipedia.org/wiki/Push_technology#Long_polling) pro načtení nových dat, je kandidátem na použití signalizace. Mezi příklady patří řídicí panely a monitorovací aplikace, aplikace pro spolupráci (například současná úprava dokumentů), aktualizace průběhu úloh a formuláře v reálném čase.

Signal také umožňuje zcela nové typy webových aplikací, které vyžadují aktualizace s vysokou frekvencí ze serveru, například hraní her v reálném čase.

Signalizace poskytuje jednoduché rozhraní API pro vytváření vzdálených procedur vzdáleného volání procedur (RPC), které volají funkce JavaScriptu v klientských prohlížečích (a dalších klientských platformách) z kódu .NET na straně serveru. Návěstí obsahuje také rozhraní API pro správu připojení (například události připojení a odpojení) a seskupování připojení.

![Vyvolání metod pomocí signalizace](introduction-to-signalr/_static/image1.png)

Služba SignalR automaticky řeší správu připojení a dovoluje vám vysílat zprávy pro všechny připojené klienty najednou, jako v chatovací místnosti. Můžete také odesílat zprávy konkrétním klientům. Připojení mezi klientem a serverem je trvalé, na rozdíl od klasického připojení HTTP, které se při každé komunikaci obnovuje.

Signalizace podporuje funkci nabízeného oznámení "serveru, při které kód serveru může volat klientský kód v prohlížeči pomocí vzdáleného volání procedur (RPC), nikoli model požadavků, který je v současnosti společný na webu.

Aplikace pro signalizaci se můžou škálovat na tisíce klientů pomocí integrovaných a poskytovatelů škálování na více instancí třetích stran.

Mezi předdefinované zprostředkovatele patří:
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

Mezi poskytovatelé třetích stran patří:
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

Signalizace je open source, který je přístupný prostřednictvím [GitHubu](https://github.com/signalr).

## <a name="signalr-and-websocket"></a>Signál a WebSocket

Nástroj Signal používá novou dopravu protokolu WebSocket, pokud je k dispozici, a v případě potřeby se vrátí do starších přenosů. I když byste mohli aplikaci opravdu psát pomocí protokolu WebSocket přímo, pomocí nástroje Signaler znamená, že je pro vás již provedeno mnoho dalších funkcí, které byste museli implementovat. Nejdůležitější to znamená, že můžete kód aplikace využít k tomu, abyste mohli využívat WebSocket, aniž byste se museli starat o vytvoření samostatné cesty kódu pro starší klienty. Signalizace vás také chrání před tím, než se nemusíte starat o aktualizace WebSocket, protože byl signál aktualizován tak, aby podporoval změny v podkladovém přenosu, a poskytuje tak jednotné rozhraní pro různé verze protokolu WebSocket.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>Přenosová a záložní

Signalizace je abstrakcí přes některé z přenosů, které jsou potřeba k tomu, aby fungovaly v reálném čase mezi klientem a serverem. Připojení k signalizaci začíná jako HTTP a pak se převýší na připojení protokolu WebSocket, pokud je k dispozici. WebSocket je ideální přenos pro signál, protože zajišťuje nejúčinnější využití paměti serveru, má nejnižší latenci a má nejvíce základní funkce (například plně duplexní komunikaci mezi klientem a serverem), ale má i nejpřísnější z nich. požadavky: WebSocket vyžaduje, aby server používal Windows Server 2012 nebo Windows 8 a .NET Framework 4,5. Pokud tyto požadavky nejsou splněné, pokusí se signál k vytvoření připojení použít jiné přenosy.

### <a name="html-5-transports"></a>Přenosy HTML 5

Tato přenosová rychlost závisí na podpoře [HTML 5](http://en.wikipedia.org/wiki/HTML5). Pokud prohlížeč klienta nepodporuje standard HTML 5, budou použity starší přenosy.

- **WebSocket** (Pokud server i prohlížeč uvádí, že můžou podporovat WebSocket). Jediný přenos, který vytváří skutečné obousměrné připojení mezi klientem a serverem, je WebSocket. Ale WebSocket má i nejpřísnější požadavky. je plně podporovaný jenom v nejnovějších verzích Microsoft Internet Exploreru, Google Chrome a Mozilla Firefox a má jenom částečnou implementaci v jiných prohlížečích, jako je třeba Opera a Safari.
- **Server odeslal události**, označované také jako EventSource (Pokud prohlížeč podporuje události odeslané serverem, které jsou v podstatě všechny prohlížeče kromě aplikace Internet Explorer.)

### <a name="comet-transports"></a>Comet transporty

Následující přenosy jsou založené na modelu webové aplikace [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) , ve kterém prohlížeč nebo jiný klient udržuje dlouhotrvající požadavek HTTP, který může server použít k zápisu dat do klienta bez nutnosti vyžádání klienta.

- **Snímek navždy** (jenom pro Internet Explorer). Navždy Frame vytvoří skrytý prvek IFrame, který vytvoří požadavek na koncový bod na serveru, který není úplný. Server pak průběžně odesílá skript klientovi, který je okamžitě spuštěn, a poskytuje jednosměrné připojení ze serveru k klientovi. Připojení od klienta k serveru používá samostatné připojení ze serveru ke klientskému připojení a podobně jako standardní požadavek HTTP, vytvoří se nové připojení pro každou část dat, která se musí odeslat.
- **Dlouhé cyklické dotazování AJAX** Při dlouhém cyklickém dotazování se nevytváří trvalé připojení, ale místo toho se server dotazuje s požadavkem, který zůstane otevřený, dokud server neodpoví. v tomto okamžiku se připojení zavře a nové připojení se vyžádá hned. To může způsobit určitou latenci při resetování připojení.

Další informace o tom, jaké přenosy jsou podporovány v rámci jakých konfigurací, najdete v tématu [podporované platformy](supported-platforms.md).

### <a name="transport-selection-process"></a>Proces výběru přenosu

V následujícím seznamu jsou uvedeny kroky, které nástroj Signal používá k rozhodnutí, který přenos se má použít.

1. Pokud je prohlížeč Internet Explorer 8 nebo starší, je použito dlouhé dotazování.
2. Pokud je nakonfigurováno JSONP (to znamená, že parametr `jsonp` je nastaven na hodnotu `true` při spuštění připojení), bude použito dlouhé cyklické dotazování.
3. Pokud se provádí připojení mezi doménami (tj. Pokud koncový bod návěstí není ve stejné doméně jako hostující stránka), použije se WebSocket, pokud se splní následující kritéria:

   - Klient podporuje CORS (sdílení prostředků mezi zdroji). Podrobnosti o tom, které klienty podporují CORS, najdete v tématu [CORS na adrese caniuse.com](http://www.caniuse.com/CORS).
   - Klient podporuje WebSocket.
   - Server podporuje WebSocket.

     Pokud některá z těchto kritérií nejsou splněná, použije se dlouhé cyklické dotazování. Další informace o připojeních mezi doménami najdete v tématu [jak vytvořit připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).
4. Pokud není nakonfigurované JSONP a připojení není mezi doménami, bude se používat protokol WebSocket, pokud ho podporuje klient i server.
5. Pokud klient nebo server nepodporují WebSocket, používají se události odeslané serverem, pokud je k dispozici.
6. Pokud nejsou události odeslané serverem k dispozici, bude proveden pokus o spuštění navždy.
7. Pokud se rámec navždy nezdařil, je použito dlouhé cyklické dotazování.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>Monitorování přenosů

Způsob, jakým se aplikace používá, můžete určit tak, že povolíte protokolování v centru a otevřete okno konzoly v prohlížeči.

Pokud chcete povolit protokolování událostí vašeho centra v prohlížeči, přidejte do své klientské aplikace následující příkaz:

`$.connection.hub.logging = true;`

- V Internet Exploreru otevřete nástroje pro vývojáře stisknutím klávesy F12 a klikněte na kartu konzola.

    ![Konzola v aplikaci Microsoft Internet Explorer](introduction-to-signalr/_static/image2.png)
- V Chrome otevřete konzolu stisknutím kombinace kláves Ctrl + Shift + J.

    ![Konzola v Google Chrome](introduction-to-signalr/_static/image3.png)

Otevřete-li konzolu nástroje a protokolování povoleno, budete moci zjistit, který přenos je používán signálem.

![Konzola v Internet Exploreru, která zobrazuje přenos protokolu WebSocket](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>Určení přenosu

Vyjednávání přenosu trvá určitou dobu a prostředky klienta a serveru. Pokud jsou funkce klienta známé, pak je možné zadat přenos při spuštění připojení klienta. Následující fragment kódu ukazuje spuštění připojení pomocí přenosu dlouhého cyklického dotazování AJAX, jak by bylo známo, že klient nepodporoval žádný jiný protokol:

`connection.start({ transport: 'longPolling' });`

Záložní pořadí můžete určit, pokud chcete, aby klient vyzkoušel konkrétní přenosy v daném pořadí. Následující fragment kódu ukazuje vyzkoušení protokolu WebSocket a nedaří se mu, přejít přímo na dlouhé cyklické dotazování.

`connection.start({ transport: ['webSockets','longPolling'] });`

Řetězcové konstanty pro určení přenosů jsou definovány takto:

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>Připojení a rozbočovače

Rozhraní API pro signalizaci obsahuje dva modely pro komunikaci mezi klienty a servery: trvalá připojení a rozbočovače.

Připojení představuje jednoduchý koncový bod pro odesílání, seskupené nebo všesměrové zprávy o jednom příjemci. Rozhraní API trvalého připojení (reprezentované třídou PersistentConnection ve službě .NET code) dává vývojáři přímý přístup k komunikačnímu protokolu nižší úrovně, který signál zpřístupňuje. Použití komunikačního modelu připojení bude známé vývojářům, kteří používali rozhraní API založená na připojeních, jako je například Windows Communication Foundation.

Rozbočovač je více kanálů vysoké úrovně postavených na rozhraní API pro připojení, které umožňuje klientovi a serveru volat metody navzájem přímo. Nástroj Signal zpracovává odesílání přes hranice počítačů, jako by to bylo, že pokud je to Magic, umožňuje klientům volat metody na serveru stejně jako místní metody a naopak. Použití komunikačního modelu hub bude známé vývojářům, kteří používali vzdálená rozhraní API pro vyvolání, jako je například Vzdálená komunikace rozhraní .NET. Použití centra také umožňuje předat parametry silného typu metodám a povolit vazbu modelu.

### <a name="architecture-diagram"></a>Diagram architektury

Následující diagram znázorňuje vztah mezi centry, trvalými připojeními a základními technologiemi používanými pro přenos.

![Diagram architektury signalizace znázorňující rozhraní API, přenosy a klienty](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>Jak fungují centra

Když kód na straně serveru volá metodu na klientovi, pošle se paket přes aktivní přenos, který obsahuje název a parametry metody, která se má volat (když se objekt pošle jako parametr metody, je serializovaný pomocí JSON). Klient pak bude odpovídat názvu metody na metody definované v kódu na straně klienta. Pokud existuje shoda, metoda klienta bude provedena pomocí deserializovaných dat parametrů.

Volání metody lze monitorovat pomocí nástrojů, jako je [Fiddler.](http://fiddler2.com/) Následující obrázek znázorňuje volání metody odeslané ze serveru signalizace do klienta webového prohlížeče v podokně protokoly v Fiddler. Volání metody je odesíláno z rozbočovače s názvem `MoveShapeHub`a metoda, která je vyvolána, se nazývá `updateShape`.

![Zobrazení protokolu Fiddler zobrazujícího přenos signálu](introduction-to-signalr/_static/image6.png)

V tomto příkladu je název centra identifikovaný pomocí parametru `H`; název metody je identifikován parametrem `M` a data, která jsou odesílána do metody, jsou určena parametrem `A`. Aplikace, která vygenerovala tuto zprávu, se vytvoří v kurzu s [vysokou frekvencí v reálném čase](tutorial-high-frequency-realtime-with-signalr.md) .

### <a name="choosing-a-communication-model"></a>Výběr komunikačního modelu

Většina aplikací by měla používat rozhraní API centra. Rozhraní API pro připojení lze použít v následujících případech:

- Je nutné zadat formát skutečné odesílané zprávy.
- Vývojář preferuje práci s modelem zasílání zpráv a odesílání a nikoli s modelem vzdáleného vyvolání.
- Existující aplikace, která používá model zasílání zpráv, je přenášena na použití signalizace.
