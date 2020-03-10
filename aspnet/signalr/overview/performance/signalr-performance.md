---
uid: signalr/overview/performance/signalr-performance
title: Výkon signálu | Microsoft Docs
author: bradygaster
description: Výkon aplikace SignalR
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558322"
---
# <a name="signalr-performance"></a>Výkon aplikace SignalR

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak navrhnout, změřit a zvýšit výkon v aplikaci signalizace.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

    **Kód serveru .NET v Startup.cs pro snížení výchozí velikosti vyrovnávací paměti zpráv**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**Nastavení konfigurace služby IIS**

- **Maximální počet souběžných požadavků na aplikaci**: zvýšení počtu souběžných požadavků služby IIS bude zvyšovat prostředky serveru, které jsou k dispozici pro poskytování požadavků. Výchozí hodnota je 5000; Chcete-li toto nastavení zvýšit, spusťte v příkazovém řádku se zvýšenými oprávněními následující příkazy:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: Jedná se o maximální počet požadavků, které fronty http. sys pro fond aplikací využívají. Když je fronta plná, nové požadavky obdrží odpověď 503 "služba není dostupná". Výchozí hodnota je 1000.

    Zkrácením délky fronty pro pracovní proces ve fondu aplikací, který je hostitelem vaší aplikace, bude mít za následek zachování paměťových prostředků. Další informace najdete v tématu [Správa, optimalizace a konfigurace fondů aplikací](https://technet.microsoft.com/library/cc745955.aspx).

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

<a id="scaleout_metrics"></a>

**Metriky škálování**

Následující metriky měří provoz a chyby generované poskytovatelem škálování. **Proud** v tomto kontextu je jednotka škálování používaná poskytovatelem škálování. Toto je tabulka, pokud se používá SQL Server, pokud se používá Service Bus a předplatné, pokud se používá Redis. Každý datový proud zajišťuje seřazené operace čtení a zápisu; jeden datový proud je potenciálním kritickým bodem škálování, takže počet datových proudů se může zvýšit, aby se snížila jeho kritická místa. Pokud se používá víc datových proudů, bude signál automaticky distribuovat (horizontálních oddílů) zprávy napříč těmito proudy způsobem, který zajistí, aby se zprávy odesílané z libovolného připojení dostaly v daném pořadí.

Nastavení [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) řídí délku fronty pro odesílání na škálování udržované signálem. Nastavením hodnoty na hodnotu větší než 0 budou všechny zprávy ve frontě pro odesílání odesílány postupně po nakonfigurované naplánování zasílání zpráv. Pokud velikost fronty překročí nakonfigurovanou délku, následné výzvy k odeslání selžou okamžitě s chybou [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) , dokud počet zpráv ve frontě nebude menší, než je nastavení znovu. Zařazení do fronty je ve výchozím nastavení zakázáno, protože implementované plány pro kontrolu mají obvykle vlastní frontu nebo řízení toku. V případě SQL Server sdružování připojení efektivně omezuje počet odeslaných v jednom okamžiku.

Ve výchozím nastavení se pro SQL Server a Redis používá jenom jeden datový proud, pro Service Bus se používá pět datových proudů a zařazení do fronty je zakázané, ale tato nastavení se dají změnit pomocí konfigurace na SQL Server a Service Bus:

**Kód serveru .NET pro konfiguraci počtu tabulek a délky fronty pro SQL Serverho naplánování**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**Kód serveru .NET pro konfiguraci počtu témat a délky fronty pro Service Busho naplánování**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

Datový proud **vyrovnávací paměti** je ten, který přešel do chybového stavu. Pokud je datový proud v chybném stavu, všechny zprávy odeslané do plánu pro replánování selžou okamžitě, dokud datový proud přestane selhat. **Délka fronty pro odesílání** je počet zpráv, které byly publikovány, ale nebyly dosud odeslány.

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

- Paměť .NET CLR\\počet bajtů ve všech haldách (pro W3wp)

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

- Zámky a vlákna .NET CLR\\Počet aktuálních logických vláken
- Zámky a vlákna .NET CLR\\Počet aktuálních fyzických vláken

<a id="otherresources"></a>

## <a name="other-resources"></a>Další prostředky

Další informace o sledování a ladění výkonu ASP.NET najdete v následujících tématech:

- [Přehled výkonu ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [Použití vláken ASP.NET ve službě IIS 7,5, IIS 7,0 a IIS 6,0](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; – element (nastavení webu)](https://msdn.microsoft.com/library/dd560842.aspx)
