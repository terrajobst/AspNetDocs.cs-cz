---
uid: signalr/overview/older-versions/handling-connection-lifetime-events
title: Porozumění a zpracování událostí životního cyklu připojení v nástroji Signal 1. x | Microsoft Docs
author: bradygaster
description: Tento článek popisuje, jak používat události vystavené rozhraním API centra.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: e608e263-264d-448b-b0eb-6eeb77713b22
msc.legacyurl: /signalr/overview/older-versions/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 2fb671e730a1d41c07b350bf1d64ac1d0b1be55c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536902"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr-1x"></a>Porozumění a zpracování událostí životního cyklu připojení v nástroji Signal 1. x

autorem [Fletcher](https://github.com/pfletcher), který [Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek poskytuje přehled o připojení signálů, opětovném připojení a událostech odpojení, které můžete zpracovávat, a nastavení časových limitů a udržení, které můžete konfigurovat.
> 
> V článku se předpokládá, že už máte nějaké znalosti událostí pro signalizaci a životnost připojení. Úvod do signalizace najdete v části [signaler – přehled-Začínáme](index.md). Seznam událostí životního cyklu připojení najdete v následujících zdrojích informací:
> 
> - [Postup zpracování událostí životního cyklu připojení ve třídě centra](index.md)
> - [Postup zpracování událostí životního cyklu připojení v klientech JavaScript](index.md)
> - [Postup zpracování událostí životního cyklu připojení v klientech rozhraní .NET](index.md)

## <a name="overview"></a>Přehled

Tento článek obsahuje následující oddíly:

- [Terminologie a scénáře platnosti připojení](#terminology)

    - [Připojení k signalizaci, přenosová připojení a fyzická připojení](#signalrvstransport)
    - [Scénáře odpojení přenosu](#transportdisconnect)
    - [Scénáře odpojení klienta](#clientdisconnect)
    - [Scénáře odpojení serveru](#serverdisconnect)
- [Nastavení časového limitu a kontroly naživu](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [Hodnota DisconnectTimeout](#disconnecttimeout)
    - [Udržení](#keepalive)
    - [Postup změny nastavení časových limitů a kontroly udržení](#changetimeout)
- [Upozornění uživatele na odpojení](#notifydisconnect)
- [Postup nepřetržitého opětovného připojení](#continuousreconnect)
- [Odpojení klienta v serverovém kódu](#disconnectclientfromserver)

Odkazy na referenční témata rozhraní API odkazují na verzi rozhraní API .NET 4,5. Pokud používáte .NET 4, přečtěte si téma věnované [verzi rozhraní API rozhraní .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>Terminologie a scénáře platnosti připojení

Obslužná rutina události `OnReconnected` v centru signalizace se dá provést přímo po `OnConnected`, ale ne po `OnDisconnected` pro daného klienta. Důvodem, proč můžete mít opětovné připojení bez odpojení je, že existuje několik způsobů, jak se v nástroji Signal používá slovo "připojení".

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>Připojení k signalizaci, přenosová připojení a fyzická připojení

Tento článek se rozlišuje mezi *připojeními k signalizaci*, *přenosovým připojením*a *fyzickými připojeními*:

- **Připojení k signalizaci** odkazuje na logický vztah mezi klientem a adresou URL serveru, který je udržován rozhraním API pro signalizaci a jednoznačně identifikovaný identifikátorem připojení. Data o tomto vztahu jsou spravována pomocí nástroje Signal a slouží k navázání transportního připojení. Ukončení relace a signalizace vyřadí data, když klient volá metodu `Stop` nebo se dosáhne časového limitu, když se signál pokusí znovu vytvořit ztracené připojení přenosu.
- **Přenosové připojení** odkazuje na logický vztah mezi klientem a serverem, který se uchovává v jednom ze čtyř přenosových rozhraní API: WebSockets, server-odesílají události, snímek navždy nebo dlouhé cyklické dotazování. Signál používá transportní rozhraní API k vytvoření transportního připojení a transportní rozhraní API závisí na existenci fyzického síťového připojení pro vytvoření přenosového připojení. Přenosové připojení končí, když ho signál ukončí nebo když transportní rozhraní API zjistí, že fyzické připojení je přerušené.
- **Fyzické připojení** odkazuje na fyzické síťové odkazy – dráty, bezdrátové signály, směrovače atd., které usnadňují komunikaci mezi klientským počítačem a serverovým počítačem. Aby bylo možné navázat spojení s připojením, musí být fyzické připojení přítomné a musí se navázat přenosové připojení, aby bylo možné navázat připojení k signalizaci. Přerušení fyzického připojení ale vždy okamžitě ukončí přenosové připojení nebo připojení k signalizaci, jak bude vysvětleno dále v tomto tématu.

V následujícím diagramu je připojení k signalizaci reprezentované rozhraním API centra a vrstvou PersistentConnection API Signal, přenosové připojení je reprezentované vrstvou přenosů a fyzické připojení je reprezentované řádky mezi serverem. a klienti.

![Diagram architektury Signal](handling-connection-lifetime-events/_static/image1.png)

Při volání metody `Start` v klientovi signalizace poskytujete klientský kód pro signalizaci s veškerými informacemi, které potřebuje, aby bylo možné navázat fyzické připojení k serveru. Kód klienta signalizace používá tyto informace k vytvoření požadavku HTTP a navázání fyzického připojení, které používá jednu ze čtyř metod přenosu. Pokud není přenosové připojení úspěšné nebo dojde k chybě serveru, připojení k signalizaci se okamžitě neprojeví, protože klient má stále informace, které potřebuje k automatickému opětovnému vytvoření nového transportního připojení ke stejné adrese URL signálu. V tomto scénáři není k dispozici žádný zásah z uživatelské aplikace, a pokud klientský kód Signale vytvoří nové přenosové připojení, nespustí nové připojení k signalizaci. Kontinuita připojení k signalizaci se odrazí ve skutečnosti, že ID připojení, které je vytvořeno při volání metody `Start`, se nezmění.

Obslužná rutina události `OnReconnected` v centru se spustí, když se po ztrátě automaticky znovu naváže připojení přenosu. Obslužná rutina události `OnDisconnected` se spouští na konci připojení k signalizaci. Připojení k signalizaci může končit některým z následujících způsobů:

- Pokud klient volá metodu `Stop`, pošle se na server zpráva o zastavení a klient i server ukončí připojení k signalizaci okamžitě.
- Po ztrátě připojení mezi klientem a serverem se klient pokusí znovu připojit a Server počká, až se klient znovu připojí. Pokud se pokusy o opětovné připojení nezdařily a časové období odpojení skončí, klient i server ukončí připojení k signalizaci. Klient se ukončí pokus o opětovné připojení a server uvolní jeho reprezentaci připojení k signalizaci.
- Pokud klient přestane běžet, aniž by bylo pravděpodobné, že by volal metodu `Stop`, Server počká, až se znovu připojí, a pak ukončí připojení k signalizaci po uplynutí časového limitu odpojení.
- Pokud je server zastavený, klient se pokusí znovu připojit (znovu vytvořit připojení přenosu) a po uplynutí časového limitu odpojení ukončí připojení k signalizaci.

Pokud nedochází k žádným problémům s připojením a uživatelská aplikace ukončí připojení k signalizaci voláním metody `Stop`, připojení k signalizaci a přenosové připojení začíná a končí ve stejnou dobu. V následujících částech jsou podrobněji popsány další informace o dalších scénářích.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>Scénáře odpojení přenosu

Fyzické připojení může být pomalé nebo mohlo dojít k přerušení připojení. V závislosti na faktorech, jako je délka přerušení, může být přenosové připojení vyřazeno. Signalizace se pak pokusí znovu vytvořit připojení přenosu. V některých případech rozhraní API pro přenos připojení zjistí přerušení a uvolní přenos připojení a signál se okamžitě vyhledá, že připojení bylo ztraceno. V jiných scénářích není rozhraní API pro přenos spojení ani signál, že by bylo připojení ztraceno. U všech přenosů s výjimkou dlouhého cyklického dotazování používá klient signalizace funkci s názvem *naživu* , aby zkontrolovala ztrátu připojení, kterou transportní rozhraní API nemůže detekovat. Informace o dlouhých připojeních pro cyklické dotazování najdete v části [nastavení časového limitu a možnosti](#timeoutkeepalive) kontroly pro připojení dále v tomto tématu.

Když je připojení neaktivní, server pravidelně odešle klientovi paket kontroly stavu. Od data, kdy je tento článek napsán, je výchozí frekvence každých 10 sekund. Díky naslouchání těmto paketům můžou klienti zjistit, jestli došlo k potížím s připojením. Pokud v případě, že se po krátké době neobdrží paket kontroly a času, klient předpokládá, že dochází k problémům s připojením, jako je například zpomalení nebo přerušení. Pokud se udržení naživu ještě nepřijme po delší době, klient předpokládá, že připojení bylo vyřazené, a začne se pokoušet o opětovné připojení.

Následující diagram znázorňuje události klienta a serveru, které jsou vyvolány v typickém scénáři, pokud dochází k problémům s fyzickým připojením, které nejsou okamžitě rozpoznány transportním rozhraním API. Diagram se vztahuje na následující okolnosti:

- Přenos je WebSockets, navždy Frame nebo události odesílané serverem.
- Ve fyzickém síťovém připojení dochází k různým dobám přerušení.
- Rozhraní API pro přenos se nedozvědělo o přerušení, takže signalizace spoléhá na funkce naživu.

![Odpojení přenosu](handling-connection-lifetime-events/_static/image2.png)

Pokud klient přejde do režimu opětovného připojení, ale nemůže vytvořit přenosové připojení v rámci časového limitu odpojení, server ukončí připojení k signalizaci. Pokud k tomu dojde, Server provede `OnDisconnected` metodu centra a zařadí do fronty zprávu o odpojení, která se odešle klientovi v případě, že se klient připojí k pozdějšímu připojení. Pokud se klient pak znovu připojí, obdrží příkaz pro odpojení a zavolá metodu `Stop`. V tomto scénáři se `OnReconnected` nespustí, když se klient znovu připojí a `OnDisconnected` se nespustí, když klient volá `Stop`. Tento scénář je znázorněn na následujícím obrázku.

![Přerušení přenosu – časový limit serveru](handling-connection-lifetime-events/_static/image3.png)

Události doby života připojení signálů, které mohou být vyvolány na straně klienta, jsou následující:

- `ConnectionSlow` událost klienta.

    Vyvolá se v případě, že před přijetím poslední zprávy nebo potvrzením platnosti byl přijat přednastavený podíl časového limitu kontroly udržení. Výchozí časový limit pro dobu kontroly stavu (udržení) je 2/3 časového limitu udržení naživu. Časový limit kontroly udržení je 20 sekund, takže se zobrazí upozornění přibližně o 13 sekundách.

    Ve výchozím nastavení server odesílá příkazy pro ověření stavu kontrolního seznamu každých 10 sekund a klient zkontroluje, jestli se na každých 2 sekundách (jedna třetina rozdílu mezi hodnotou časového limitu kontroly stavu kontroly a hodnotou časového limitu kontroly stavu) kontroluje.

    Pokud se transportní rozhraní API dozvědělo o odpojení, může být signál upozorněn na odpojení před úspěšným časovým limitem časového limitu kontroly udržení platnosti. V takovém případě by se událost `ConnectionSlow` nevyvolala a signál by přešel přímo k události `Reconnecting`.
- `Reconnecting` událost klienta.

    Vyvolá se, když (a) Transportní rozhraní API zjistí ztrátu připojení, nebo (b) vypršel časový limit kontroly udržení dat, který uplynul od poslední zprávy, nebo byl přijat příkaz pro ověření naživu. Kód klienta signalizace se začne pokoušet znovu připojit. Tuto událost můžete zpracovat, pokud chcete, aby aplikace probrala určitou akci, když dojde ke ztrátě připojení přenosu. Výchozí časový limit pro udržení naživu je v současné době 20 sekund.

    Pokud se Váš klientský kód pokusí zavolat metodu rozbočovače, zatímco je signál v režimu opětovného připojení, signál se pokusí odeslat příkaz. Ve většině případů tyto pokusy selžou, ale v některých případech se může stát, že budou úspěšné. Pro události odeslané serverem, navždy a dlouhé cyklické dotazování používá Signal dva komunikační kanály, které klient používá k posílání zpráv a k tomu, které používá k přijímání zpráv. Kanál použitý k přijetí je trvale otevřený a je ten, který je uzavřený při přerušení fyzického připojení. Kanál použitý k odeslání zůstává dostupný, takže pokud se obnoví fyzické připojení, může být volání metody z klienta na server úspěšné, než se znovu naváže kanál pro příjem. Návratová hodnota nebude přijata, dokud signál znovu neotevře kanál použitý k přijetí.
- `Reconnected` událost klienta.

    Vyvolá se v případě, že je přenosové připojení znovu navázáno. V centru se spustí obslužná rutina události `OnReconnected`.
- `Closed` událost klienta (událost`disconnected` v JavaScriptu).

    Je aktivována, když časový limit pro odpojení vyprší, když se kód klienta nástroje Signal pokusí znovu připojit po ztrátě připojení přenosu. Výchozí časový limit pro odpojení je 30 sekund. (Tato událost je vyvolána také v případě, že je připojení ukončeno, protože je volána metoda `Stop`.)

Přerušení připojení přenosu, která nejsou zjištěna transportním rozhraním API, a nedělejte prodlevu přijímání příkazů pro ověření platnosti paketů kontroly a času na serveru déle, než je časový limit pro dobu nečinnosti, nemusí způsobit vyvolání všech událostí životního cyklu připojení.

Některá síťová prostředí úmyslně zavřou nečinná připojení a další funkce paketů kontroly stavu, které jim umožňují zabránit tomu, aby tyto sítě věděly, že se připojení k signalizaci používá. V extrémních případech nemusí být výchozí frekvence příkazů pro ověření stavu připojení k síti k dispozici, aby se zabránilo uzavřeným připojením. V takovém případě můžete nakonfigurovat, aby bylo možné odesílat příkazy pro ověřování paketů kontroly a častější odesílání. Další informace najdete v části [nastavení časového limitu a možnosti](#timeoutkeepalive) kontroly pro otevření v tomto tématu.

> [!NOTE] 
> 
> [!IMPORTANT]
> Posloupnost událostí popsaných zde není zaručena. Signalní je pokaždé, když se každý pokus o vyzvednutí událostí životního cyklu připojení předvídatelným způsobem podle tohoto schématu, ale existuje mnoho variant síťových událostí a mnoha způsobů, kterými se podřídí komunikační architektury, jako jsou třeba transportní rozhraní API. Například událost `Reconnected` nemusí být vyvolána, když se klient znovu připojí, nebo se může spustit obslužná rutina `OnConnected` na serveru, když se pokus o navázání spojení nezdařil. V tomto tématu jsou popsány pouze efekty, které by obvykle byly vyprodukovány pomocí určitých typických okolností.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>Scénáře odpojení klienta

V klientském prohlížeči je kód klienta signalizace, který udržuje připojení k signalizaci, spuštěn v kontextu JavaScriptu webové stránky. To je důvod, proč musí připojení k signalizaci končit při přechodu z jedné stránky na jiný a to je důvod, proč máte k dispozici více připojení s více identifikátory připojení, pokud se připojujete z více oken prohlížeče nebo karet. Když uživatel zavře okno nebo kartu prohlížeče nebo přejde na novou stránku nebo aktualizuje stránku, okamžitě se ukončí připojení k signalizaci, protože klientský kód signalizace zpracovává událost prohlížeče a zavolá metodu `Stop`. V těchto scénářích nebo na jakékoli klientské platformě, když vaše aplikace volá metodu `Stop`, obslužná rutina události `OnDisconnected` se okamžitě spustí na serveru a klient vyvolá událost `Closed` (událost je pojmenována `disconnected` v JavaScriptu).

Pokud klientská aplikace nebo počítač, který je spuštěný v případě havárie nebo přejde do režimu spánku (například když uživatel zavírá notebook), neoznamuje server informace o tom, co se stalo. Pokud je server ví, může dojít ke ztrátě klienta z důvodu přerušení připojení a klient se může pokusit o opětovné připojení. Proto se v těchto scénářích Server počká, aby klient mohl znovu připojit, a `OnDisconnected` se nespustí, dokud nevyprší časový limit odpojení (přibližně 30 sekund ve výchozím nastavení). Tento scénář je znázorněn na následujícím obrázku.

![Selhání klientského počítače](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>Scénáře odpojení serveru

Když server přejde do režimu offline, dojde k chybě, recyklace domény aplikace atd.--výsledek může být podobný ztrátě připojení, nebo transportní rozhraní API a odesilatele může okamžitě zjistit, že se server nachází, a signál se může pokusit znovu připojit bez vyvolání události `ConnectionSlow`. Pokud se klient přepne do režimu opětovného připojení a pokud se server obnoví nebo restartuje nebo se nový server přepne do online režimu před vypršením časového limitu odpojení, klient se znovu připojí k obnovenému nebo novému serveru. V takovém případě připojení k signalizaci pokračuje na klientovi a vyvolá se `Reconnected` událost. Na prvním serveru se `OnDisconnected` nikdy neprovede a na novém serveru se `OnReconnected` spustí, i když `OnConnected` pro tohoto klienta na tomto serveru spuštěný. (Účinek je stejný, pokud se klient znovu připojí ke stejnému serveru po restartování nebo recyklaci domény aplikace, protože když se server restartuje, nemá žádná paměť předchozí aktivity připojení.) Následující diagram předpokládá, že transportní rozhraní API se okamžitě dozvědělo o ztraceném připojení, takže se událost `ConnectionSlow` neaktivuje.

![Selhání serveru a opětovné připojení](handling-connection-lifetime-events/_static/image5.png)

Pokud se server v rámci časového limitu odpojení nestane dostupný, ukončí se připojení k signalizaci. V tomto scénáři je v klientovi vyvolána událost `Closed` (`disconnected` v klientech JavaScript), ale `OnDisconnected` na serveru nikdy není volána. Následující diagram předpokládá, že transportní rozhraní API neví o ztracených připojeních, takže se detekuje funkcí kontroly naživu a `ConnectionSlow` událostmi.

![Selhání serveru a časový limit](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Nastavení časového limitu a kontroly naživu

Výchozí hodnoty `ConnectionTimeout`, `DisconnectTimeout`a `KeepAlive` jsou vhodné pro většinu scénářů, ale můžou se změnit, pokud vaše prostředí má speciální požadavky. Pokud například vaše síťové prostředí ukončí připojení, která jsou nečinná po dobu 5 sekund, možná budete muset snížit hodnotu kontroly stavu.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>connectionTimeout

Toto nastavení představuje dobu, po kterou může být připojení přenosu otevřeno a čeká na odpověď před zavřením a otevřením nového připojení. Výchozí hodnota je 110 sekund.

Toto nastavení platí pouze v případě, že funkce kontroly naživu je zakázána, což obvykle platí pouze pro přenos dlouhého cyklického dotazování. Následující diagram znázorňuje účinek tohoto nastavení při dlouhodobém připojení přenosu s dotazem.

![Přenosové připojení dlouhého cyklického dotazování](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>Hodnota DisconnectTimeout

Toto nastavení představuje dobu, po kterou se má čekat po ztrátě připojení přenosu, než se vyvolala událost `Disconnected`. Výchozí hodnota je 30 sekund. Když nastavíte `DisconnectTimeout`, `KeepAlive` se automaticky nastaví na 1/3 hodnoty `DisconnectTimeout`.

<a id="keepalive"></a>

### <a name="keepalive"></a>Udržení

Toto nastavení představuje dobu, po kterou se má čekat před odesláním paketu kontroly a času přes nečinné připojení. Výchozí hodnota je 10 sekund. Tato hodnota nesmí být větší než 1/3 hodnoty `DisconnectTimeout`.

Chcete-li nastavit `DisconnectTimeout` i `KeepAlive`, nastavte `KeepAlive` po `DisconnectTimeout`. V opačném případě bude nastavení `KeepAlive` přepsáno, pokud `DisconnectTimeout` automaticky nastaví `KeepAlive` na 1/3 z hodnoty časového limitu.

Pokud chcete zakázat funkci udržení naživu, nastavte `KeepAlive` na null. Funkce kontroly naživu je pro přenos dlouhého cyklického dotazování automaticky zakázaná.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>Postup změny nastavení časových limitů a kontroly udržení

Chcete-li změnit výchozí hodnoty pro tato nastavení, nastavte je v `Application_Start` v souboru *Global. asax* , jak je znázorněno v následujícím příkladu. Hodnoty uvedené v ukázkovém kódu jsou stejné jako výchozí hodnoty.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>Upozornění uživatele na odpojení

V některých aplikacích může být vhodné zobrazit uživateli při potížích s připojením zprávu. Máte několik možností, jak a kdy to udělat. Následující ukázky kódu jsou pro klienta jazyka JavaScript pomocí vygenerovaného proxy serveru.

- Zpracujte událost `connectionSlow`, aby se zobrazila zpráva, jakmile signál ví o problémech s připojením, než se přejde do režimu opětovného připojení.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- Zpracujte událost `reconnecting`, aby zobrazila zprávu, když signál zná informace o odpojení a přechází do režimu opětovného připojení.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- Zpracuje událost `disconnected`, aby zobrazila zprávu, když vypršel časový limit pokusu o opětovné připojení. V tomto scénáři jediným způsobem, jak znovu navázat spojení se serverem, je restartování připojení k signalizaci voláním metody `Start`, která vytvoří nové ID připojení. Následující ukázka kódu používá příznak k tomu, abyste se ujistili, že budete vydávat oznámení až po vypršení časového limitu opětovného připojení, ne po normálním ukončení připojení k signalizaci, které bylo způsobené voláním metody `Stop`.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>Postup nepřetržitého opětovného připojení

V některých aplikacích můžete chtít automaticky znovu vytvořit připojení po jeho ztrátě a časový limit pokusu o opětovné připojení vypršel. To lze provést voláním metody `Start` z obslužné rutiny události `Closed` (`disconnected` obslužné rutiny události v klientech jazyka JavaScript). Možná budete chtít počkat časový interval před voláním `Start`, abyste se vyhnuli příliš často, když je server nebo fyzické připojení nedostupné. Následující ukázka kódu je pro JavaScriptový klient využívající vygenerovaný proxy server.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

Možným problémem v mobilních klientech je to, že při pokusech o nepřetržité opětovné připojení, když je server nebo fyzické připojení dostupné, by mohlo dojít k zbytečnému vyprázdnění baterie.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>Odpojení klienta v serverovém kódu

Signal verze 1.1.1 nemá integrované serverové rozhraní API pro odpojení klientů. V budoucnu jsou k dispozici [plány pro přidání této funkce](https://github.com/SignalR/SignalR/issues/2101). Nejjednodušší způsob, jak odpojit klienta ze serveru, je v aktuálním vydání signalizace implementace metody odpojení na straně klienta a volání této metody ze serveru. Následující ukázka kódu ukazuje metodu odpojení pro klienta jazyka JavaScript pomocí vygenerovaného proxy serveru.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> Zabezpečení – ani tato metoda odpojení klientů ani navržený integrovaný rozhraní API bude řešit scénář napadených klientů, na kterých běží škodlivý kód, protože se klienti mohou znovu připojit nebo by napadený kód mohl odebrat metodu `stopClient` nebo změnit jejich chování. Příslušné místo pro implementaci stavové ochrany DOS (Denial of Service) není v architektuře ani ve vrstvě serveru, ale spíše v infrastruktuře front-endu.
