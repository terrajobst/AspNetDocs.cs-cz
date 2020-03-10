---
uid: signalr/overview/older-versions/signalr-performance
title: Výkon signálu (Signaler 1. x) | Microsoft Docs
author: bradygaster
description: Výkon aplikace SignalR
ms.author: bradyg
ms.date: 07/03/2013
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 915fd822caae9bbcb0a688c6dd7a5b2bda12c9df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579609"
---
# <a name="signalr-performance-signalr-1x"></a>Výkon aplikace SignalR (SignalR 1.x)

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak navrhnout, změřit a zvýšit výkon v aplikaci signalizace.

Nedávný prezentační výkon a škálování signálu najdete v tématu [škálování webu v reálném čase pomocí ASP.NET signálu](https://channel9.msdn.com/Events/Build/2013/3-502).

Toto téma obsahuje následující oddíly:

- [Aspekty návrhu](#design)
- [Ladění serveru signálu pro výkon](#tuning)
- [Řešení potíží s výkonem](#troubleshooting)
- [Použití čítačů výkonu signalizace](#perfcounters)
- [Používání dalších čítačů výkonu](#othercounters)
- [Další zdroje informací](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>Na co dát pozor při navrhování

Tato část popisuje vzory, které je možné implementovat během návrhu aplikace pro signalizaci, aby se zajistilo, že výkon nebude bráněno vygenerováním zbytečných síťových přenosů.

### <a name="throttling-message-frequency"></a>Frekvence omezování zpráv

I v aplikaci, která odesílá zprávy s vysokou frekvencí (například herní aplikace v reálném čase), nemusí většina aplikací odesílat více než několik zpráv za sekundu. Chcete-li snížit množství provozu, který každý z nich vygeneruje, je možné implementovat smyčku zpráv, která zařadí do fronty a odesílá zprávy s výjimkou pevné sazby (to znamená, že až v okamžiku, kdy jsou v této době zprávy, bude odesláno až do určitého počtu zpráv). terval k odeslání). Ukázková aplikace, která omezuje zprávy na určitou míru (od klienta i serveru), najdete v části [vysoká frekvence v reálném čase pomocí nástroje Signal](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).

### <a name="reducing-message-size"></a>Zmenšení velikosti zprávy

Můžete zmenšit velikost zprávy signálu tím, že zmenšíte velikost serializovaných objektů. Pokud v kódu serveru odesíláte objekt, který obsahuje vlastnosti, které není nutné přenést, zabraňte serializaci těchto vlastností pomocí atributu `JsonIgnore`. Názvy vlastností jsou také uloženy ve zprávě; názvy vlastností lze zkrátit pomocí atributu `JsonProperty`. Následující příklad kódu ukazuje, jak vyloučit vlastnost ze zasílání klientovi a jak zkrátit názvy vlastností:

**Kód serveru .NET, který ukazuje atribut JsonIgnore pro vyloučení dat z odeslání do klienta, a atribut JsonProperty pro snížení velikosti zprávy**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

Aby se zachovala čitelnost a udržovatelnost v kódu klienta, zkrácené názvy vlastností lze po přijetí zprávy přemapovat na názvy, které jsou v názvu. Následující příklad kódu ukazuje jeden z možných způsobů, jak přemapování zkrácených názvů na delší, definováním kontraktu zprávy (mapování) a použitím funkce `reMap` pro použití této smlouvy na optimalizované třídě zpráv:

**Kód JavaScriptu na straně klienta, který přemapuje názvy zkrácených vlastností na názvy, které lze číst lidmi**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

Názvy mohou být zkráceny ve zprávách od klienta k serveru, a to pomocí stejné metody.

Snížení výkonu paměti (tj. množství paměti využitého pro zprávu) objektu Message může také zlepšit výkon. Pokud například není potřeba plný rozsah `int`, můžete místo toho použít `short` nebo `byte`.

Vzhledem k tomu, že se zprávy ukládají do sběrnice zpráv v paměti serveru, zmenšení velikosti zpráv může také řešit problémy s pamětí serveru.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>Ladění serveru signálu pro výkon

Následující nastavení konfigurace můžete použít k vyladění serveru pro lepší výkon v aplikaci signalizace. Obecné informace o tom, jak zlepšit výkon v aplikaci ASP.NET, najdete v tématu [zlepšení výkonu ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).

**Nastavení konfigurace signálu**

- **DefaultMessageBufferSize**: ve výchozím nastavení zachovává signál zprávy 1000 v paměti na jedno centrum a připojení. Pokud se používají velké zprávy, může to způsobit problémy paměti, které je možné zmírnit snížením této hodnoty. Toto nastavení lze nastavit v obslužné rutině události `Application_Start` v aplikaci ASP.NET nebo v metodě `Configuration` třídy spouštění OWIN v samoobslužné aplikaci. Následující příklad ukazuje, jak tuto hodnotu omezit, aby se snížilo nároky na paměť aplikace, aby se snížila velikost využité paměti serveru:

    **Kód .NET serveru v Global. asax pro snížení výchozí velikosti vyrovnávací paměti zpráv**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**Nastavení konfigurace služby IIS**

- **Maximální počet souběžných požadavků na aplikaci**: zvýšení počtu souběžných požadavků služby IIS bude zvyšovat prostředky serveru, které jsou k dispozici pro poskytování požadavků. Výchozí hodnota je 5000; Chcete-li toto nastavení zvýšit, spusťte v příkazovém řádku se zvýšenými oprávněními následující příkazy:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

**Nastavení konfigurace ASP.NET**

Tato část obsahuje nastavení konfigurace, která se dají nastavit v souboru `aspnet.config`. Tento soubor se nachází v jednom ze dvou umístění v závislosti na platformě:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

Nastavení ASP.NET, která mohou zlepšit výkon signálu, zahrnují následující:

- **Maximální počet souběžných požadavků na procesor**: zvýšení tohoto nastavení může zmírnit kritická místa výkonu. Chcete-li toto nastavení zvýšit, přidejte do souboru `aspnet.config` následující nastavení konfigurace:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **Limit fronty požadavků**: Pokud celkový počet připojení překročí nastavení `maxConcurrentRequestsPerCPU`, ASP.NET spustí omezování požadavků pomocí fronty. Pokud chcete zvětšit velikost fronty, můžete nastavení `requestQueueLimit` zvýšit. Provedete to tak, že do uzlu `processModel` v `config/machine.config` přidáte následující nastavení konfigurace (místo `aspnet.config`):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>Řešení potíží s výkonem

Tato část popisuje způsoby, jak najít kritická místa výkonu ve vaší aplikaci.

### <a name="verifying-that-websocket-is-being-used"></a>Ověřuje se, jestli se používá protokol WebSocket.

I když může nástroj pro komunikaci mezi klientem a serverem používat nejrůznější přenos, nabízí WebSocket značnou výhodu výkonu a měla by se používat v případě, že ho podporuje klient a Server. Pokud chcete zjistit, jestli váš klient a server splňují požadavky na WebSocket, přečtěte si téma [přenosy a záložní](../getting-started/introduction-to-signalr.md#transports)služby. Chcete-li zjistit, jaký přenos se v aplikaci používá, můžete použít nástroje pro vývojáře v prohlížeči a prohlédnout si protokoly, abyste zjistili, jaký přenos se pro připojení používá. Informace o používání nástrojů pro vývoj v prohlížeči v Internet Exploreru a Chrome najdete v tématu [přenosy a záložní](../getting-started/introduction-to-signalr.md#transports)prvky.

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>Použití čítačů výkonu signalizace

Tato část popisuje, jak povolit a používat čítače výkonu signálů, které najdete v balíčku `Microsoft.AspNet.SignalR.Utils`.

### <a name="installing-signalrexe"></a>Instalace signalizace. exe

Čítače výkonu lze přidat k serveru pomocí nástroje s názvem Signal. exe. K instalaci tohoto nástroje použijte následující postup:

1. V aplikaci Visual Studio vyberte **nástroje** > **správce balíčků NuGet** > **Spravovat balíčky NuGet pro řešení** .
2. Vyhledejte **signál. utils**a vyberte nainstalovat.

    ![](signalr-performance/_static/image1.png)
3. Přijměte licenční smlouvu pro instalaci balíčku.
4. Signál. exe bude nainstalován do `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.

### <a name="installing-performance-counters-with-signalrexe"></a>Instalace čítačů výkonu pomocí nástroje Signaler. exe

Chcete-li nainstalovat čítače výkonu signálu, spusťte příkaz Signal. exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

Chcete-li odebrat čítače výkonu signálu, spusťte příkaz Signal. exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>Čítače výkonu signálu

Balíček nástroje nainstaluje následující čítače výkonu. Čítače "celkem" měří počet událostí od posledního fondu aplikací nebo restartování serveru.

**Metriky připojení**

Následující metriky měří události životnosti připojení, ke kterým dojde. Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení](../guide-to-the-api/handling-connection-lifetime-events.md).

- **Připojení připojena**
- **Připojení se znovu připojila.**
- **Odpojená připojení**
- **Aktuální připojení**

**Metriky zpráv**

Následující metriky měří přenos zpráv generovaných signálem.

- **Počet přijatých zpráv o připojení**
- **Odeslané zprávy o připojení celkem**
- **Přijaté zprávy o připojení za sekundu**
- **Odeslané zprávy o připojení za sekundu**

**Metriky sběrnice zpráv**

Následující metriky měří provoz prostřednictvím interní sběrnice zpráv signálem, fronty, ve které jsou umístěny všechny příchozí a odchozí zprávy signálu. Zpráva se **publikuje** při odeslání nebo vysílání. **Předplatitelem** v tomto kontextu je předplatné ze sběrnice zpráv. hodnota by měla být rovna počtu klientů a samotnému serveru. **Přidělený pracovník** je komponenta, která odesílá data do aktivních připojení. **zaneprázdněný pracovní proces** je jedním z nich, který aktivně posílá zprávu.

- **Přijaté zprávy sběrnice zpráv celkem**
- **Přijaté zprávy sběrnice zpráv/s**
- **Publikované zprávy sběrnice zpráv celkem**
- **Publikované zprávy sběrnice zpráv/s**
- **Předplatitelé sběrnice zpráv aktuální**
- **Předplatitelé sběrnice zpráv celkem**
- **Předplatitelé sběrnice zpráv/s**
- **Pracovníci přidělení sběrnice zpráv**
- **Zaneprázdněné pracovní procesy sběrnice zpráv**
- **Aktuální témata sběrnice zpráv**

**Metriky chyb**

Následující metriky měří chyby vygenerované přenosem zpráv signálem. K chybám **rozlišení centra** dochází v případě, že nelze přeložit centrum nebo metodu centra. Chyby při **vyvolání centra** jsou výjimky vyvolané při vyvolání metody rozbočovače. Chyby **přenosu** jsou chyby připojení vyvolané během žádosti nebo odpovědi HTTP.

- **Chyby: celkem**
- **Chyby: vše/s**
- **Chyby: celkové rozlišení centra**
- **Chyby: řešení centra/s**
- **Chyby: vyvolání centra celkem**
- **Chyby: vyvolání centra/s**
- **Chyby: celkový přenos**
- **Chyby: přenos za sekundu**

**Metriky škálování**

Následující metriky měří provoz a chyby generované poskytovatelem škálování. **Proud** v tomto kontextu je jednotka škálování používaná poskytovatelem škálování. Toto je tabulka, pokud se používá SQL Server, pokud se používá Service Bus a předplatné, pokud se používá Redis. Ve výchozím nastavení se používá pouze jeden datový proud, ale lze ho zvýšit prostřednictvím konfigurace SQL Server a Service Bus. Datový proud **vyrovnávací paměti** je ten, který přešel do chybového stavu. Pokud je datový proud v chybném stavu, všechny zprávy odeslané do plánu pro replánování selžou okamžitě, dokud datový proud přestane selhat. **Délka fronty pro odesílání** je počet zpráv, které byly publikovány, ale nebyly dosud odeslány.

- **Přijaté zprávy ve sběrnici pro škálování/s**
- **Proudy škálování celkem**
- **Otevřené proudy škálování**
- **Vyrovnávací paměť streamování pro horizontální navýšení kapacity**
- **Celkový počet chyb při škálování**
- **Chyby horizontálního navýšení kapacity/s**
- **Délka fronty pro odesílání pro škálování**

Další informace o tom, jak se tyto čítače měří, najdete v tématu [škálování signálu pomocí Azure Service Bus](scaleout-with-windows-azure-service-bus.md).

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>Používání dalších čítačů výkonu

Následující čítače výkonu mohou být užitečné také při monitorování výkonu aplikace.

**Rezident**

- Paměť .NET CLR počet bajtů ve všech haldách (pro W3wp)

**ASP.NET**

- ASP. NET\Requests – aktuální
- ASP. NET\Queued
- ASP. NET\Rejected

**VČETNĚ**

- Čas procesoru Information\Processor

**PROTOKOL TCP/IP**

- TCPv6/připojení navázáno
- TCPv4/připojení navázáno

**Webová služba**

- Připojení k webu Service\Current
- Připojení k webu Service\Maximum

**Dělení na vlákna**

- LocksAndThreads .NET CLR\# aktuálních logických vláken
- LocksAnd vláken .NET CLR\# aktuálních fyzických vláken

<a id="otherresources"></a>

## <a name="other-resources"></a>Další prostředky

Další informace o sledování a ladění výkonu ASP.NET najdete v následujících tématech:

- [Přehled výkonu ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [Použití vláken ASP.NET ve službě IIS 7,5, IIS 7,0 a IIS 6,0](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; – element (nastavení webu)](https://msdn.microsoft.com/library/dd560842.aspx)
