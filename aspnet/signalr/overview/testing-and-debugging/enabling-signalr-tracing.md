---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: Povolování trasování signálů | Microsoft Docs
author: bradygaster
description: Tento dokument popisuje, jak povolit a nakonfigurovat trasování pro servery a klienty signalizace. Trasování umožňuje zobrazit diagnostické informace o událostech...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578832"
---
# <a name="enabling-signalr-tracing"></a>Povolení trasování knihovnou SignalR

tím, že [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument popisuje, jak povolit a nakonfigurovat trasování pro servery a klienty signalizace. Trasování umožňuje zobrazit diagnostické informace o událostech v aplikaci signalizace.
>
> Toto téma bylo původně napsáno nadFletcherm.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - Signal – verze 2
>
>
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

Pokud je povoleno trasování, aplikace signalizace vytvoří položky protokolu pro události. Události můžete protokolovat z klienta i serveru. Trasování v protokolu serveru protokoluje připojení, poskytovatele škálování a události sběrnice zpráv. Trasování v klientském počítači protokoluje události připojení. V nástroji Signal 2,1 a později trasování klienta protokoluje úplný obsah zpráv o voláních centra.

## <a name="contents"></a>Obsah

- [Povolení trasování na serveru](#server)

    - [Protokolování událostí serveru do textových souborů](#server_text)
    - [Protokolování událostí serveru do protokolu událostí](#server_eventlog)
- [Povolení trasování v klientu .NET (desktopové aplikace pro Windows)](#net_client)

    - [Protokolování událostí klienta plochy do konzoly](#desktop_console)
    - [Protokolování událostí klienta plochy do textového souboru](#desktop_text)
- [Povolení trasování v klientech Windows Phone 8](#phone)

    - [Protokolování událostí klienta Windows Phone do uživatelského rozhraní](#phone_ui)
    - [Protokolování událostí klienta Windows Phone do konzoly ladění](#phone_debug)
- [Povolení trasování v klientovi JavaScriptu](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>Povolení trasování na serveru

V závislosti na typu projektu povolíte trasování na serveru v konfiguračním souboru aplikace (soubor App. config nebo Web. config). Určíte, které kategorie událostí chcete protokolovat. V konfiguračním souboru můžete také určit, zda chcete protokolovat události do textového souboru, do protokolu událostí systému Windows nebo do vlastního protokolu pomocí implementace [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).

Kategorie událostí serveru obsahují následující řazení zpráv:

| Zdroj | Zprávy |
| --- | --- |
| Signál. SqlMessageBus | Nastavení poskytovatele škálování sběrnice zpráv SQL, operace databáze, chyba a události časového limitu |
| Signál. ServiceBusMessageBus | Vytváření a předplatné, chyby a události zasílání zpráv v tématu zprostředkovatel škálování služby Service Bus |
| Signál. RedisMessageBus | Připojení, odpojení a chybové události poskytovatele škálování Redis |
| Signál. ScaleoutMessageBus | Události zasílání zpráv ve škálování |
| SignalR.Transports.WebSocketTransport | Přenosové připojení protokolu WebSocket, odpojení, zasílání zpráv a chybové události |
| SignalR.Transports.ServerSentEventsTransport | ServerSentEvents přenosu, odpojení, zasílání zpráv a chybové události |
| SignalR.Transports.ForeverFrameTransport | ForeverFrame přenosu, odpojení, zasílání zpráv a chybové události |
| Signalizace. Transports. LongPollingTransport | LongPolling přenosu, odpojení, zasílání zpráv a chybové události |
| Signalizace. Transports. TransportHeartBeat | Přenosové připojení, odpojení a události udržení naživu |
| Signál. ReflectedHubDescriptorProvider | Události zjišťování centra |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>Protokolování událostí serveru do textových souborů

Následující kód ukazuje, jak povolit trasování pro každou kategorii události. Tato ukázka nakonfiguruje aplikaci tak, aby protokoloval události do textových souborů.

**Kód serveru XML pro povolení trasování**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

V kódu výše položka `SignalRSwitch` určuje parametr [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) , který se používá pro události odeslané do určeného protokolu. V tomto případě je nastavená na `Verbose` to znamená, že se zaznamenávají všechny zprávy ladění a trasování.

Následující výstup zobrazuje položky ze souboru `transports.log.txt` pro aplikaci pomocí výše uvedeného konfiguračního souboru. Zobrazuje nové připojení, odebrané připojení a události prezenčního signálu přenosu.

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>Protokolování událostí serveru do protokolu událostí

Chcete-li protokolovat události do protokolu událostí místo textového souboru, změňte hodnoty položek v uzlu `sharedListeners`. Následující kód ukazuje, jak protokolovat události serveru do protokolu událostí:

**Kód serveru XML pro protokolování událostí do protokolu událostí**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

Události jsou protokolovány v aplikačním protokolu a jsou k dispozici prostřednictvím Prohlížeč událostí, jak je znázorněno níže:

![Prohlížeč událostí zobrazení protokolů signálu](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> Pokud používáte protokol událostí, nastavte hodnotu **TraceLevel** na **chybu** , aby se zachoval počet zpráv, které lze spravovat.

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>Povolení trasování v klientu .NET (desktopové aplikace pro Windows)

Klient rozhraní .NET může protokolovat události do konzoly, textového souboru nebo do vlastního protokolu pomocí implementace [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).

Chcete-li povolit protokolování v klientovi .NET, nastavte vlastnost `TraceLevel` připojení na hodnotu [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) a vlastnost `TraceWriter` na platnou instanci [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) .

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>Protokolování událostí klienta plochy do konzoly

Následující C# kód ukazuje, jak protokolovat události v klientovi .NET do konzoly nástroje:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>Protokolování událostí klienta plochy do textového souboru

Následující C# kód ukazuje, jak protokolovat události v klientovi .NET do textového souboru:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

Následující výstup zobrazuje položky ze souboru `ClientLog.txt` pro aplikaci pomocí výše uvedeného konfiguračního souboru. Zobrazuje se klient, který se připojuje k serveru, a centrum vyvolá metodu klienta nazvanou `addMessage`:

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>Povolení trasování v klientech Windows Phone 8

Aplikace Signal pro aplikace Windows Phone používají stejný klient .NET jako desktopové aplikace, ale [Konzola. out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) a zápis do souboru pomocí [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) nejsou k dispozici. Místo toho je nutné vytvořit vlastní implementaci objektu [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) pro trasování.

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>Protokolování událostí klienta Windows Phone do uživatelského rozhraní

[Základ signálu](https://github.com/SignalR/SignalR/archive/master.zip) obsahuje vzorový Windows Phone, který zapisuje výstup trasování do [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) pomocí vlastní implementace [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) s názvem `TextBlockWriter`. Tuto třídu lze najít v projektu **Samples/Microsoft. ASPNET. signaler. Client. WP8. Samples** . Při vytváření instance `TextBlockWriter`předejte aktuální [Třída SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) , kde vytvoří [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) pro použití pro výstup trasování:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

Výstup trasování se pak zapíše do nového [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) vytvořeného v [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) , které jste předali:

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>Protokolování událostí klienta Windows Phone do konzoly ladění

Chcete-li odeslat výstup do konzoly ladění namísto uživatelského rozhraní, vytvořte implementaci objektu [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) , který zapisuje do okna ladění a přiřaďte ho k vlastnosti [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) vašeho připojení:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

Informace o trasování budou následně zapsány do okna ladění v aplikaci Visual Studio:

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>Povolení trasování v klientovi JavaScriptu

Chcete-li povolit protokolování na straně klienta pro připojení, nastavte vlastnost `logging` objektu Connection před voláním metody `start` k navázání připojení.

**JavaScriptový kód klienta pro povolení trasování do konzoly prohlížeče (s vygenerovaným proxy serverem)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**JavaScriptový kód klienta pro povolení trasování do konzoly prohlížeče (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

Když je trasování povoleno, klient jazyka JavaScript protokoluje události do konzoly prohlížeče. Přístup ke konzole prohlížeče najdete v tématu [monitorování přenosů](../getting-started/introduction-to-signalr.md#MonitoringTransports).

Na následujícím snímku obrazovky vidíte klienta jazyka JavaScript s povoleným trasováním. Zobrazuje události připojení a volání centra v konzole prohlížeče:

![Události trasování signálu v konzole prohlížeče](enabling-signalr-tracing/_static/image4.png)
