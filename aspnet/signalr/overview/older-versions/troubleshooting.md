---
uid: signalr/overview/older-versions/troubleshooting
title: Poradce při potížích (Signaler 1. x) | Microsoft Docs
author: bradygaster
description: Tento článek popisuje běžné problémy s vývojem aplikací pro signalizaci.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579602"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>Řešení potíží s knihovnou SignalR (SignalR 1.x)

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument popisuje běžné problémy s odstraňováním potíží s nástrojem Signal.

Tento dokument obsahuje následující oddíly.

- [Volající metody mezi klientem a serverem selžou](#connection)
- [Další problémy s připojením](#other)
- [Kompilace a chyby na straně serveru](#server)
- [Problémy se sady Visual Studio](#vs)
- [Problémy s Internetová informační služba](#iis)
- [Problémy s Azure](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>Volající metody mezi klientem a serverem selžou

Tato část popisuje možné příčiny selhání volání metody mezi klientem a serverem bez smysluplné chybové zprávy. V aplikaci signalizace nemá server žádné informace o metodách, které klient implementuje; Když server vyvolá metodu klienta, je do klienta zaslána data názvu metody a parametru a metoda je provedena pouze v případě, že existuje ve formátu, který je zadán serverem. Pokud se v klientovi nenajde žádná vyhovující metoda, nic se nestane a na serveru se nevyvolá žádná chybová zpráva.

Chcete-li dále prozkoumat klientské metody, které nejsou volány, můžete zapnout protokolování před voláním metody Start na rozbočovači, aby bylo možné zjistit, jaká volání pocházejí ze serveru. Chcete-li povolit protokolování v aplikaci JavaScriptu, přečtěte si téma [Jak povolit protokolování na straně klienta (verze klienta JavaScript)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging). Chcete-li povolit protokolování v klientské aplikaci .NET, přečtěte si téma [Jak povolit protokolování na straně klienta (verze klienta rozhraní .NET)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>Nesprávně napsaná metoda, nesprávný podpis metody nebo nesprávný název centra

Pokud se název nebo signatura volané metody přesně neshoduje s odpovídající metodou na klientovi, volání se nezdaří. Ověřte, že název metody, který je volán serverem, odpovídá názvu metody v klientovi. Také signál vytvoří rozbočovač proxy pomocí metod ve stylu CamelCase-použita, jak je to vhodné v JavaScriptu, takže metoda nazvaná `SendMessage` na serveru by se volala `sendMessage` na klientském proxy serveru. Použijete-li v kódu na straně serveru atribut `HubName`, ověřte, zda se používá název, který se shoduje s názvem použitým k vytvoření centra na klientovi. Pokud nepoužijete atribut `HubName`, ověřte, zda je název centra v jazyce JavaScript ve stylu CamelCase-použita, jako je například chatHub namísto ChatHub.

### <a name="duplicate-method-name-on-client"></a>Duplicitní název metody na klientovi

Ověřte, že v klientovi nemáte duplicitní metodu, která se liší pouze velikostí písmen. Pokud má vaše klientská aplikace metodu nazvanou `sendMessage`, ověřte také, že není k dispozici také metoda s názvem `SendMessage`.

### <a name="missing-json-parser-on-the-client"></a>Na klientovi chybí analyzátor JSON.

Návěstí vyžaduje, aby byl k dispozici analyzátor JSON pro serializaci volání mezi serverem a klientem. Pokud váš klient nemá integrovaný analyzátor JSON (například Internet Explorer 7), budete ho muset zahrnout do aplikace. Analyzátor JSON si můžete stáhnout [tady](http://nuget.org/packages/json2).

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Kombinace centra a PersistentConnection syntaxe

Nástroj Signal používá dva komunikační modely: centra a PersistentConnections. Syntaxe pro volání těchto dvou modelů komunikace je odlišná v kódu klienta. Pokud jste do svého serverového kódu přidali centrum, ověřte, že veškerý kód klienta používá správnou syntaxi centra.

**JavaScriptový kód klienta, který vytvoří PersistentConnection v klientovi JavaScriptu**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**JavaScriptový kód klienta, který vytvoří rozbočovač proxy v klientovi JavaScriptu**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C#kód serveru, který mapuje trasu na PersistentConnection**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C#serverový kód, který mapuje trasu na rozbočovač nebo na více Center v případě, že máte více aplikací**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>Připojení začalo před přidáním předplatných.

Pokud se připojení k rozbočovači spustí před tím, než se do proxy serveru přidají metody, které je možné volat ze serveru, nebudou se přijímat zprávy. Následující kód jazyka JavaScript nebude správně spustit centrum:

**Nesprávný kód klienta JavaScriptu, který nepovoluje příjem zpráv centra**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

Místo toho přidejte předplatná metody před voláním Start:

**Kód klienta JavaScriptu, který správně přidá odběry do centra**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>Chybí název metody na proxy hub.

Ověřte, zda je metoda definovaná na serveru přihlášena k odběru klienta. I když Server definuje metodu, musí být stále přidaný do klientského proxy serveru. Metody lze do proxy serveru klienta přidat následujícími způsoby (Všimněte si, že metoda je přidána do `client`ho člena centra, nikoli přímo do centra):

**JavaScriptový kód klienta, který přidává metody do proxy serveru hub**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>Metody centra nebo centra nejsou deklarované jako veřejné.

Aby bylo možné v klientovi zobrazit, musí být implementace a metody centra deklarovány jako `public`.

### <a name="accessing-hub-from-a-different-application"></a>Přístup k centru z jiné aplikace

K centrům signálu se dá dostat jenom prostřednictvím aplikací, které implementují klienty signalizace. Signál nemůže spolupracovat s jinými komunikačními knihovnami (jako jsou webové služby SOAP nebo WCF). Pokud není pro vaši cílovou platformu k dispozici žádný klient signalizace, nebudete moct přímo získat přístup ke koncovému bodu serveru.

### <a name="manually-serializing-data"></a>Ruční serializace dat

Signál k serializaci parametrů metody automaticky použije kód JSON – nemusíte to dělat sami.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>Metoda vzdáleného rozbočovače se neprovádí u klienta v operaci odpojení.

Toto chování je záměrné. Když je volána `OnDisconnected`, centrum již zadalo `Disconnected` stav, který neumožňuje volání dalších metod centra.

**C#kód serveru, který správně spustí kód v události odpojení**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>Byl dosažen limit připojení

Při použití plné verze služby IIS na klientském operačním systému, jako je Windows 7, se zavede limit 10 připojení. Pokud používáte klientský operační systém, použijte místo toho IIS Express k tomu, abyste se vyhnuli tomuto omezení.

### <a name="cross-domain-connection-not-set-up-properly"></a>Připojení mezi doménami není správně nastavené.

Pokud připojení mezi doménami (připojení, pro které není adresa URL signalizace ve stejné doméně jako hostující stránka), není nastavené správně, připojení může selhat bez chybové zprávy. Informace o tom, jak povolit mezidoménovou komunikaci, najdete v tématu [jak vytvořit připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>Připojení pomocí protokolu NTLM (Active Directory) nefunguje v klientu .NET.

Připojení v klientské aplikaci .NET, které používá zabezpečení domény, může selhat, pokud připojení není správně nakonfigurováno. Chcete-li použít signalizaci v prostředí domény, nastavte požadovanou vlastnost připojení následujícím způsobem:

**C#kód klienta, který implementuje přihlašovací údaje pro připojení**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>Další problémy s připojením

Tato část popisuje příčiny a řešení konkrétních symptomů a chybových zpráv, ke kterým dojde během připojení.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>Chyba "spuštění musí být voláno před odesláním dat".

K této chybě obvykle dochází, pokud kód odkazuje na objekty signálu před spuštěním připojení. Wireup pro obslužné rutiny a podobně jako volání metod definovaných na serveru se musí přidat po dokončení připojení. Všimněte si, že volání `Start` je asynchronní, takže kód po volání může být proveden před jeho dokončením. Nejlepším způsobem, jak přidat obslužné rutiny po úplném spuštění připojení, je umístit je do funkce zpětného volání, která je předána jako parametr metodě start:

**JavaScriptový kód klienta, který správně přidává obslužné rutiny událostí, které odkazují na objekty signálu**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

Tato chyba se zobrazí také v případě, že se připojení zastaví, zatímco jsou pořád odkazovány na objekty signálů.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>Chyba "301 přesunutí trvalá" nebo "302 přesunuta"

Tato chyba se může zobrazit, pokud projekt obsahuje složku s názvem Signal, která bude v konfliktu s automaticky vytvořeným proxy serverem. Chcete-li se této chybě vyhnout, nepoužívejte ve své aplikaci složku s názvem `SignalR` nebo vypněte automatické generování proxy. Další podrobnosti najdete u [vygenerovaného proxy serveru a o tom, co vám dělá](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) .

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>Chyba "403 zakázáno" v klientovi .NET nebo Silverlight

K této chybě může dojít v prostředích mezi doménami, kde není správně povolená komunikace mezi doménami. Informace o tom, jak povolit mezidoménovou komunikaci, najdete v tématu [jak vytvořit připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain). Chcete-li vytvořit připojení mezi doménami v klientovi Silverlight, Projděte si téma [připojení mezi doménami od klientů programu Silverlight](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).

### <a name="404-not-found-error"></a>Chyba "404 nenalezen"

Tento problém má několik příčin. Ověřte všechny tyto skutečnosti:

- **Odkaz na adresu proxy serveru centra není správně naformátován:** K této chybě obvykle dochází v případě, že odkaz na vygenerovanou adresu proxy serveru není správně naformátován. Ověřte, zda je odkaz na adresu centra správně vytvořen. Podrobnosti najdete v tématu [postup odkazování dynamicky vygenerovaného proxy serveru](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) .
- **Přidávání tras do aplikace před přidáním trasy centra:** Pokud vaše aplikace používá jiné trasy, ověřte, zda je první přidaná trasa voláním `MapHubs`.

### <a name="500-internal-server-error"></a>"500 interní chyba serveru"

Toto je velmi obecná chyba, která může mít nejrůznější příčiny. Podrobnosti o chybě by se měly zobrazit v protokolu událostí serveru, nebo se dají najít prostřednictvím ladění serveru. Podrobnější informace o chybách lze získat zapnutím podrobných chyb na serveru. Další informace najdete v tématu [jak zpracovávat chyby ve třídě centra](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType&gt; není definováno" Chyba

Tato chyba bude mít za následek nesprávné provedení volání `MapHubs`. Další informace najdete v tématu [jak zaregistrovat trasu signalizace a nakonfigurovat možnosti signalizace](../guide-to-the-api/hubs-api-guide-server.md#route) .

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException byl neošetřený uživatelským kódem.

Ověřte, zda parametry, které odesíláte do vašich metod, neobsahují neserializovatelné typy (například popisovače souborů nebo připojení k databázi). Pokud potřebujete použít členy na objektu na straně serveru, který nechcete odesílat klientovi (buď z důvodu zabezpečení, nebo z důvodů serializace), použijte atribut `JSONIgnore`.

### <a name="protocol-error-unknown-transport-error"></a>Chyba protokolu: Neznámá přenosová chyba

K této chybě může dojít, pokud klient nepodporuje přenos, který signál používá. Informace o tom, které prohlížeče se dají používat se signálem, najdete v tématu [přenosové a záložní](../getting-started/introduction-to-signalr.md#transports) verze.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"Generování proxy serveru centra JavaScript bylo zakázáno."

K této chybě dojde, pokud je nastavena `DisableJavaScriptProxies` a zároveň zahrnuje odkaz na dynamicky generovaný proxy server v `signalr/hubs`. Další informace o ručním vytvoření proxy serveru najdete v tématu [vygenerované proxy a k čemu](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"ID připojení má nesprávný formát" nebo "při aktivním připojení k signalizaci se nemůže změnit identita uživatele"

Tato chyba se může zobrazit, pokud se používá ověřování a klient se odhlásí před zastavením připojení. Řešením je zastavit připojení k signalizaci před protokolováním klienta.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"Nezachycená Chyba: signál: jQuery nebyl nalezen. Ujistěte se prosím, že se na jQuery odkazuje před souborem Signal. js.

Klient pro signalizaci JavaScriptu vyžaduje, aby se spustilo jQuery. Ověřte, zda je odkaz na jQuery správný, zda použitá cesta je platná a zda odkaz na jQuery je před odkazem na signál.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"Nezachycené TypeError: nejde načíst vlastnost&lt;vlastnost&gt;nedefinovaného".

Tato chyba je způsobena tím, že není správně odkazována na jQuery nebo na proxy centra. Ověřte, zda je váš odkaz na jQuery a proxy rozbočovačů správný, zda použitá cesta je platná a zda odkaz na jQuery je před odkazem na proxy centra. Výchozí odkaz na proxy centra by měl vypadat takto:

**Kód HTML na straně klienta, který správně odkazuje na proxy centra**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>Chyba "RuntimeBinderException byl neošetřený uživatelským kódem"

K této chybě může dojít, pokud je použito nesprávné přetížení `Hub.On`. Pokud má metoda návratovou hodnotu, musí být návratový typ zadán jako parametr obecného typu:

**Metoda definovaná na klientovi (bez vygenerovaného proxy serveru)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>ID připojení je nekonzistentní nebo se mezi načtenými stránkami narušuje přerušení připojení.

Toto chování je záměrné. Vzhledem k tomu, že je objekt centra hostovaný v objektu stránky, je při aktualizaci stránky tento rozbočovač zničen. Vícestránkové aplikace musí udržovat přidružení mezi uživateli a identifikátory připojení, aby byly konzistentní mezi načítáním stránek. ID připojení mohou být uložena na serveru buď v objektu `ConcurrentDictionary`, nebo v databázi.

### <a name="value-cannot-be-null-error"></a>Chyba "hodnota nemůže mít hodnotu null"

Metody na straně serveru s nepovinnými parametry se v současné době nepodporují. Pokud je nepovinný parametr vynechán, metoda se nezdaří. Další informace najdete v tématu [volitelné parametry](https://github.com/SignalR/SignalR/issues/324).

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox nemůže navázat připojení k serveru na adrese &lt;adresa&gt;" Chyba v Firebug

Tato chybová zpráva se může zobrazit v Firebug v případě, že se vyjednávání protokolu WebSocket nezdaří a místo toho se použije další přenos. Toto chování je záměrné.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>"Vzdálený certifikát je neplatný podle ověřovací procedury" Chyba v klientské aplikaci .NET

Pokud váš server vyžaduje vlastní klientské certifikáty, můžete k připojení přidat certifikátu x509 před tím, než se žádost dovede. Přidejte certifikát k připojení pomocí `Connection.AddClientCertificate`.

### <a name="connection-drops-after-authentication-times-out"></a>Po vypršení časového limitu připojení se uvolní.

Toto chování je záměrné. Přihlašovací údaje pro ověřování nelze upravovat, pokud je připojení aktivní; Chcete-li aktualizovat přihlašovací údaje, je nutné připojení zastavit a restartovat.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>V případě, že se používá jQuery Mobile, se v připojení volá dvakrát.

funkce `initializePage` jQuery Mobile vynutí opětovné spuštění skriptů na každé stránce, čímž se vytvoří druhé připojení. Mezi řešení tohoto problému patří:

- Přidejte odkaz na jQuery Mobile před souborem JavaScriptu.
- Zakažte funkci `initializePage` nastavením `$.mobile.autoInitializePage = false`.
- Než začnete s připojením, počkejte, než se dokončí inicializace stránky.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>Zprávy jsou v aplikacích Silverlight zpožděny pomocí událostí odeslaných serverem.

Zprávy jsou zpožděny při použití událostí odeslaných serverem v programu Silverlight. Pokud chcete vynutit použití dlouhého cyklického dotazování, použijte při spuštění připojení následující:

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>"Oprávnění bylo odepřeno pomocí protokolu rámců navždy

Jedná se o známý problém, který je [zde](https://github.com/SignalR/SignalR/issues/1963)popsán. Tento příznak se může zobrazit pomocí nejnovější knihovny JQuery. alternativním řešením je downgrade aplikace na JQuery 1.8.2.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>Kompilace a chyby na straně serveru

 Následující část obsahuje možná řešení pro kompilátor a chyby běhového prostředí na straně serveru. 

### <a name="reference-to-hub-instance-is-null"></a>Odkaz na instanci centra je null.

Vzhledem k tomu, že je instance centra pro každé připojení vytvořená, nemůžete ve svém kódu vytvořit instanci rozbočovače sami. Chcete-li volat metody na rozbočovači vně samotného centra, přečtěte si téma [jak volat klientské metody a spravovat skupiny z vně třídy centra](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) pro získání odkazu na kontext centra.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext. Current. Session má hodnotu null.

Toto chování je záměrné. Signál nepodporuje stav relace ASP.NET, protože povolení stavu relace by přerušilo duplexní zasílání zpráv.

### <a name="no-suitable-method-to-override"></a>Žádná vhodná metoda pro přepsání

Tato chyba se může zobrazit, pokud používáte kód ze starší dokumentace nebo blogů. Ověřte, že neodkazují na názvy metod, které byly změněny nebo zastaralé (například `OnConnectedAsync`).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions. WebSocketServerUrl má hodnotu null.

Toto chování je záměrné. Tento člen je zastaralý a neměl by se používat.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"Trasa s názvem" Signal. Hubs "je již v kolekci tras"

Tato chyba se zobrazí, pokud vaše aplikace `MapHubs` volá dvakrát. Některé příklady aplikací volají `MapHubs` přímo v souboru globální aplikace. jiné provádí volání v obálkové třídě. Ujistěte se, že aplikace neprovádí obojí.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Problémy se sady Visual Studio

Tato část popisuje problémy zjištěné v aplikaci Visual Studio.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>Uzel dokumenty skriptu se nezobrazuje v Průzkumník řešení

Některé z našich kurzů vás přesměrují na uzel dokumenty skriptů v Průzkumník řešení při ladění. Tento uzel je vytvořen ladicím programem jazyka JavaScript a zobrazí se pouze při ladění klientů prohlížeče v aplikaci Internet Explorer. Pokud se použije Chrome nebo Firefox, uzel se nezobrazí. Ladicí program JavaScriptu se také nespustí, pokud je spuštěn jiný klientský ladicí program, jako je například ladicí program Silverlight.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>Návěstí nefunguje v systému Visual Studio 2008 nebo starším.

Toto chování je záměrné. Signál vyžaduje .NET Framework 4 nebo novější; To vyžaduje, aby byly aplikace signálů vyvinuty v aplikaci Visual Studio 2010 nebo novější.

<a id="iis"></a>

## <a name="iis-issues"></a>Problémy služby IIS

Tato část obsahuje problémy s Internetová informační služba.

### <a name="web-site-crashes-after-maphubs-call"></a>Selhání webu po volání MapHubs

Tento problém byl opraven v nejnovější verzi nástroje Signaler. Ověřte, že používáte nejnovější vydanou verzi nástroje Signal tím, že svou instalaci aktualizujete pomocí NuGet.

<a id="azure"></a>

## <a name="azure-issues"></a>Problémy s Azure

Tato část obsahuje problémy s Microsoft Azure.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>Po změně názvů témat se zprávy nepřijaly prostřednictvím Azure replánování.

Témata používaná v Azure back-Plan nejsou zamýšlená jako uživatelsky konfigurovatelné.
