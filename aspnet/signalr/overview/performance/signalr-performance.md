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
# <a name="signalr-performance"></a><span data-ttu-id="5fa62-103">Výkon aplikace SignalR</span><span class="sxs-lookup"><span data-stu-id="5fa62-103">SignalR Performance</span></span>

<span data-ttu-id="5fa62-104">Po [Fletcheru](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="5fa62-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5fa62-105">Toto téma popisuje, jak navrhnout, změřit a zvýšit výkon v aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="5fa62-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="5fa62-106">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="5fa62-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="5fa62-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5fa62-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="5fa62-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5fa62-108">.NET 4.5</span></span>
> - <span data-ttu-id="5fa62-109">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="5fa62-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="5fa62-110">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="5fa62-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="5fa62-111">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="5fa62-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="5fa62-112">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="5fa62-112">Questions and comments</span></span>
>
> <span data-ttu-id="5fa62-113">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="5fa62-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5fa62-114">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="5fa62-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="5fa62-115">Nedávný prezentační výkon a škálování signálu najdete v tématu [škálování webu v reálném čase pomocí ASP.NET signálu](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="5fa62-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="5fa62-116">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="5fa62-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="5fa62-117">Aspekty návrhu</span><span class="sxs-lookup"><span data-stu-id="5fa62-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="5fa62-118">Ladění serveru signálu pro výkon</span><span class="sxs-lookup"><span data-stu-id="5fa62-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="5fa62-119">Řešení potíží s výkonem</span><span class="sxs-lookup"><span data-stu-id="5fa62-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="5fa62-120">Použití čítačů výkonu signalizace</span><span class="sxs-lookup"><span data-stu-id="5fa62-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="5fa62-121">Používání dalších čítačů výkonu</span><span class="sxs-lookup"><span data-stu-id="5fa62-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="5fa62-122">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="5fa62-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="5fa62-123">Na co dát pozor při navrhování</span><span class="sxs-lookup"><span data-stu-id="5fa62-123">Design considerations</span></span>

<span data-ttu-id="5fa62-124">Tato část popisuje vzory, které je možné implementovat během návrhu aplikace pro signalizaci, aby se zajistilo, že výkon nebude bráněno vygenerováním zbytečných síťových přenosů.</span><span class="sxs-lookup"><span data-stu-id="5fa62-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="5fa62-125">Frekvence omezování zpráv</span><span class="sxs-lookup"><span data-stu-id="5fa62-125">Throttling message frequency</span></span>

<span data-ttu-id="5fa62-126">I v aplikaci, která odesílá zprávy s vysokou frekvencí (například herní aplikace v reálném čase), nemusí většina aplikací odesílat více než několik zpráv za sekundu.</span><span class="sxs-lookup"><span data-stu-id="5fa62-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="5fa62-127">Chcete-li snížit množství provozu, který každý z nich vygeneruje, je možné implementovat smyčku zpráv, která zařadí do fronty a odesílá zprávy s výjimkou pevné sazby (to znamená, že až v okamžiku, kdy jsou v této době zprávy, bude odesláno až do určitého počtu zpráv). terval k odeslání).</span><span class="sxs-lookup"><span data-stu-id="5fa62-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="5fa62-128">Ukázková aplikace, která omezuje zprávy na určitou míru (od klienta i serveru), najdete v části [vysoká frekvence v reálném čase pomocí nástroje Signal](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="5fa62-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="5fa62-129">Zmenšení velikosti zprávy</span><span class="sxs-lookup"><span data-stu-id="5fa62-129">Reducing message size</span></span>

<span data-ttu-id="5fa62-130">Můžete zmenšit velikost zprávy signálu tím, že zmenšíte velikost serializovaných objektů.</span><span class="sxs-lookup"><span data-stu-id="5fa62-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="5fa62-131">Pokud v kódu serveru odesíláte objekt, který obsahuje vlastnosti, které není nutné přenést, zabraňte serializaci těchto vlastností pomocí atributu `JsonIgnore`.</span><span class="sxs-lookup"><span data-stu-id="5fa62-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="5fa62-132">Názvy vlastností jsou také uloženy ve zprávě; názvy vlastností lze zkrátit pomocí atributu `JsonProperty`.</span><span class="sxs-lookup"><span data-stu-id="5fa62-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="5fa62-133">Následující příklad kódu ukazuje, jak vyloučit vlastnost ze zasílání klientovi a jak zkrátit názvy vlastností:</span><span class="sxs-lookup"><span data-stu-id="5fa62-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="5fa62-134">**Kód serveru .NET, který ukazuje atribut JsonIgnore pro vyloučení dat z odeslání do klienta, a atribut JsonProperty pro snížení velikosti zprávy**</span><span class="sxs-lookup"><span data-stu-id="5fa62-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="5fa62-135">Aby se zachovala čitelnost a udržovatelnost v kódu klienta, zkrácené názvy vlastností lze po přijetí zprávy přemapovat na názvy, které jsou v názvu.</span><span class="sxs-lookup"><span data-stu-id="5fa62-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="5fa62-136">Následující příklad kódu ukazuje jeden z možných způsobů, jak přemapování zkrácených názvů na delší, definováním kontraktu zprávy (mapování) a použitím funkce `reMap` pro použití této smlouvy na optimalizované třídě zpráv:</span><span class="sxs-lookup"><span data-stu-id="5fa62-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="5fa62-137">**Kód JavaScriptu na straně klienta, který přemapuje názvy zkrácených vlastností na názvy, které lze číst lidmi**</span><span class="sxs-lookup"><span data-stu-id="5fa62-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="5fa62-138">Názvy mohou být zkráceny ve zprávách od klienta k serveru, a to pomocí stejné metody.</span><span class="sxs-lookup"><span data-stu-id="5fa62-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="5fa62-139">Snížení výkonu paměti (tj. množství paměti využitého pro zprávu) objektu Message může také zlepšit výkon.</span><span class="sxs-lookup"><span data-stu-id="5fa62-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="5fa62-140">Pokud například není potřeba plný rozsah `int`, můžete místo toho použít `short` nebo `byte`.</span><span class="sxs-lookup"><span data-stu-id="5fa62-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="5fa62-141">Vzhledem k tomu, že se zprávy ukládají do sběrnice zpráv v paměti serveru, zmenšení velikosti zpráv může také řešit problémy s pamětí serveru.</span><span class="sxs-lookup"><span data-stu-id="5fa62-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="5fa62-142">Ladění serveru signálu pro výkon</span><span class="sxs-lookup"><span data-stu-id="5fa62-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="5fa62-143">Následující nastavení konfigurace můžete použít k vyladění serveru pro lepší výkon v aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="5fa62-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="5fa62-144">Obecné informace o tom, jak zlepšit výkon v aplikaci ASP.NET, najdete v tématu [zlepšení výkonu ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fa62-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="5fa62-145">**Nastavení konfigurace signálu**</span><span class="sxs-lookup"><span data-stu-id="5fa62-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="5fa62-146">**DefaultMessageBufferSize**: ve výchozím nastavení zachovává signál zprávy 1000 v paměti na jedno centrum a připojení.</span><span class="sxs-lookup"><span data-stu-id="5fa62-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="5fa62-147">Pokud se používají velké zprávy, může to způsobit problémy paměti, které je možné zmírnit snížením této hodnoty.</span><span class="sxs-lookup"><span data-stu-id="5fa62-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="5fa62-148">Toto nastavení lze nastavit v obslužné rutině události `Application_Start` v aplikaci ASP.NET nebo v metodě `Configuration` třídy spouštění OWIN v samoobslužné aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5fa62-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="5fa62-149">Následující příklad ukazuje, jak tuto hodnotu omezit, aby se snížilo nároky na paměť aplikace, aby se snížila velikost využité paměti serveru:</span><span class="sxs-lookup"><span data-stu-id="5fa62-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="5fa62-150">**Kód serveru .NET v Startup.cs pro snížení výchozí velikosti vyrovnávací paměti zpráv**</span><span class="sxs-lookup"><span data-stu-id="5fa62-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="5fa62-151">**Nastavení konfigurace služby IIS**</span><span class="sxs-lookup"><span data-stu-id="5fa62-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="5fa62-152">**Maximální počet souběžných požadavků na aplikaci**: zvýšení počtu souběžných požadavků služby IIS bude zvyšovat prostředky serveru, které jsou k dispozici pro poskytování požadavků.</span><span class="sxs-lookup"><span data-stu-id="5fa62-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="5fa62-153">Výchozí hodnota je 5000; Chcete-li toto nastavení zvýšit, spusťte v příkazovém řádku se zvýšenými oprávněními následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="5fa62-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="5fa62-154">**ApplicationPool QueueLength**: Jedná se o maximální počet požadavků, které fronty http. sys pro fond aplikací využívají.</span><span class="sxs-lookup"><span data-stu-id="5fa62-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="5fa62-155">Když je fronta plná, nové požadavky obdrží odpověď 503 "služba není dostupná".</span><span class="sxs-lookup"><span data-stu-id="5fa62-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="5fa62-156">Výchozí hodnota je 1000.</span><span class="sxs-lookup"><span data-stu-id="5fa62-156">The default value is 1000.</span></span>

    <span data-ttu-id="5fa62-157">Zkrácením délky fronty pro pracovní proces ve fondu aplikací, který je hostitelem vaší aplikace, bude mít za následek zachování paměťových prostředků.</span><span class="sxs-lookup"><span data-stu-id="5fa62-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="5fa62-158">Další informace najdete v tématu [Správa, optimalizace a konfigurace fondů aplikací](https://technet.microsoft.com/library/cc745955.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fa62-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="5fa62-159">**Nastavení konfigurace ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="5fa62-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="5fa62-160">Tato část obsahuje nastavení konfigurace, která se dají nastavit v souboru `aspnet.config`.</span><span class="sxs-lookup"><span data-stu-id="5fa62-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="5fa62-161">Tento soubor se nachází v jednom ze dvou umístění v závislosti na platformě:</span><span class="sxs-lookup"><span data-stu-id="5fa62-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="5fa62-162">Nastavení ASP.NET, která mohou zlepšit výkon signálu, zahrnují následující:</span><span class="sxs-lookup"><span data-stu-id="5fa62-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="5fa62-163">**Maximální počet souběžných požadavků na procesor**: zvýšení tohoto nastavení může zmírnit kritická místa výkonu.</span><span class="sxs-lookup"><span data-stu-id="5fa62-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="5fa62-164">Chcete-li toto nastavení zvýšit, přidejte do souboru `aspnet.config` následující nastavení konfigurace:</span><span class="sxs-lookup"><span data-stu-id="5fa62-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="5fa62-165">**Limit fronty požadavků**: Pokud celkový počet připojení překročí nastavení `maxConcurrentRequestsPerCPU`, ASP.NET spustí omezování požadavků pomocí fronty.</span><span class="sxs-lookup"><span data-stu-id="5fa62-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="5fa62-166">Pokud chcete zvětšit velikost fronty, můžete nastavení `requestQueueLimit` zvýšit.</span><span class="sxs-lookup"><span data-stu-id="5fa62-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="5fa62-167">Provedete to tak, že do uzlu `processModel` v `config/machine.config` přidáte následující nastavení konfigurace (místo `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="5fa62-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="5fa62-168">Řešení potíží s výkonem</span><span class="sxs-lookup"><span data-stu-id="5fa62-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="5fa62-169">Tato část popisuje způsoby, jak najít kritická místa výkonu ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5fa62-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="5fa62-170">Ověřuje se, jestli se používá protokol WebSocket.</span><span class="sxs-lookup"><span data-stu-id="5fa62-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="5fa62-171">I když může nástroj pro komunikaci mezi klientem a serverem používat nejrůznější přenos, nabízí WebSocket značnou výhodu výkonu a měla by se používat v případě, že ho podporuje klient a Server.</span><span class="sxs-lookup"><span data-stu-id="5fa62-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="5fa62-172">Pokud chcete zjistit, jestli váš klient a server splňují požadavky na WebSocket, přečtěte si téma [přenosy a záložní](../getting-started/introduction-to-signalr.md#transports)služby.</span><span class="sxs-lookup"><span data-stu-id="5fa62-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="5fa62-173">Chcete-li zjistit, jaký přenos se v aplikaci používá, můžete použít nástroje pro vývojáře v prohlížeči a prohlédnout si protokoly, abyste zjistili, jaký přenos se pro připojení používá.</span><span class="sxs-lookup"><span data-stu-id="5fa62-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="5fa62-174">Informace o používání nástrojů pro vývoj v prohlížeči v Internet Exploreru a Chrome najdete v tématu [přenosy a záložní](../getting-started/introduction-to-signalr.md#transports)prvky.</span><span class="sxs-lookup"><span data-stu-id="5fa62-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="5fa62-175">Použití čítačů výkonu signalizace</span><span class="sxs-lookup"><span data-stu-id="5fa62-175">Using SignalR performance counters</span></span>

<span data-ttu-id="5fa62-176">Tato část popisuje, jak povolit a používat čítače výkonu signálů, které najdete v balíčku `Microsoft.AspNet.SignalR.Utils`.</span><span class="sxs-lookup"><span data-stu-id="5fa62-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="5fa62-177">Instalace signalizace. exe</span><span class="sxs-lookup"><span data-stu-id="5fa62-177">Installing signalr.exe</span></span>

<span data-ttu-id="5fa62-178">Čítače výkonu lze přidat k serveru pomocí nástroje s názvem Signal. exe.</span><span class="sxs-lookup"><span data-stu-id="5fa62-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="5fa62-179">K instalaci tohoto nástroje použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="5fa62-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="5fa62-180">V aplikaci Visual Studio vyberte **nástroje** > **správce balíčků NuGet** > **Spravovat balíčky NuGet pro řešení** .</span><span class="sxs-lookup"><span data-stu-id="5fa62-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="5fa62-181">Vyhledejte **signál. utils**a vyberte nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="5fa62-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="5fa62-182">Přijměte licenční smlouvu pro instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="5fa62-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="5fa62-183">Signál. exe bude nainstalován do `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span><span class="sxs-lookup"><span data-stu-id="5fa62-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="5fa62-184">Instalace čítačů výkonu pomocí nástroje Signaler. exe</span><span class="sxs-lookup"><span data-stu-id="5fa62-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="5fa62-185">Chcete-li nainstalovat čítače výkonu signálu, spusťte příkaz Signal. exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:</span><span class="sxs-lookup"><span data-stu-id="5fa62-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="5fa62-186">Chcete-li odebrat čítače výkonu signálu, spusťte příkaz Signal. exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:</span><span class="sxs-lookup"><span data-stu-id="5fa62-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="5fa62-187">Čítače výkonu signálu</span><span class="sxs-lookup"><span data-stu-id="5fa62-187">SignalR Performance counters</span></span>

<span data-ttu-id="5fa62-188">Balíček nástroje nainstaluje následující čítače výkonu.</span><span class="sxs-lookup"><span data-stu-id="5fa62-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="5fa62-189">Čítače "celkem" měří počet událostí od posledního fondu aplikací nebo restartování serveru.</span><span class="sxs-lookup"><span data-stu-id="5fa62-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="5fa62-190">**Metriky připojení**</span><span class="sxs-lookup"><span data-stu-id="5fa62-190">**Connection metrics**</span></span>

<span data-ttu-id="5fa62-191">Následující metriky měří události životnosti připojení, ke kterým dojde.</span><span class="sxs-lookup"><span data-stu-id="5fa62-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="5fa62-192">Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="5fa62-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="5fa62-193">**Připojení připojena**</span><span class="sxs-lookup"><span data-stu-id="5fa62-193">**Connections Connected**</span></span>
- <span data-ttu-id="5fa62-194">**Připojení se znovu připojila.**</span><span class="sxs-lookup"><span data-stu-id="5fa62-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="5fa62-195">**Odpojená připojení**</span><span class="sxs-lookup"><span data-stu-id="5fa62-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="5fa62-196">**Aktuální připojení**</span><span class="sxs-lookup"><span data-stu-id="5fa62-196">**Connections Current**</span></span>

<span data-ttu-id="5fa62-197">**Metriky zpráv**</span><span class="sxs-lookup"><span data-stu-id="5fa62-197">**Message metrics**</span></span>

<span data-ttu-id="5fa62-198">Následující metriky měří přenos zpráv generovaných signálem.</span><span class="sxs-lookup"><span data-stu-id="5fa62-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="5fa62-199">**Počet přijatých zpráv o připojení**</span><span class="sxs-lookup"><span data-stu-id="5fa62-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="5fa62-200">**Odeslané zprávy o připojení celkem**</span><span class="sxs-lookup"><span data-stu-id="5fa62-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="5fa62-201">**Přijaté zprávy o připojení za sekundu**</span><span class="sxs-lookup"><span data-stu-id="5fa62-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="5fa62-202">**Odeslané zprávy o připojení za sekundu**</span><span class="sxs-lookup"><span data-stu-id="5fa62-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="5fa62-203">**Metriky sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="5fa62-203">**Message bus metrics**</span></span>

<span data-ttu-id="5fa62-204">Následující metriky měří provoz prostřednictvím interní sběrnice zpráv signálem, fronty, ve které jsou umístěny všechny příchozí a odchozí zprávy signálu.</span><span class="sxs-lookup"><span data-stu-id="5fa62-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="5fa62-205">Zpráva se **publikuje** při odeslání nebo vysílání.</span><span class="sxs-lookup"><span data-stu-id="5fa62-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="5fa62-206">**Předplatitelem** v tomto kontextu je předplatné ze sběrnice zpráv. hodnota by měla být rovna počtu klientů a samotnému serveru.</span><span class="sxs-lookup"><span data-stu-id="5fa62-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="5fa62-207">**Přidělený pracovník** je komponenta, která odesílá data do aktivních připojení. **zaneprázdněný pracovní proces** je jedním z nich, který aktivně posílá zprávu.</span><span class="sxs-lookup"><span data-stu-id="5fa62-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="5fa62-208">**Přijaté zprávy sběrnice zpráv celkem**</span><span class="sxs-lookup"><span data-stu-id="5fa62-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="5fa62-209">**Přijaté zprávy sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="5fa62-210">**Publikované zprávy sběrnice zpráv celkem**</span><span class="sxs-lookup"><span data-stu-id="5fa62-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="5fa62-211">**Publikované zprávy sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="5fa62-212">**Předplatitelé sběrnice zpráv aktuální**</span><span class="sxs-lookup"><span data-stu-id="5fa62-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="5fa62-213">**Předplatitelé sběrnice zpráv celkem**</span><span class="sxs-lookup"><span data-stu-id="5fa62-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="5fa62-214">**Předplatitelé sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="5fa62-215">**Pracovníci přidělení sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="5fa62-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="5fa62-216">**Zaneprázdněné pracovní procesy sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="5fa62-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="5fa62-217">**Aktuální témata sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="5fa62-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="5fa62-218">**Metriky chyb**</span><span class="sxs-lookup"><span data-stu-id="5fa62-218">**Error metrics**</span></span>

<span data-ttu-id="5fa62-219">Následující metriky měří chyby vygenerované přenosem zpráv signálem.</span><span class="sxs-lookup"><span data-stu-id="5fa62-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="5fa62-220">K chybám **rozlišení centra** dochází v případě, že nelze přeložit centrum nebo metodu centra.</span><span class="sxs-lookup"><span data-stu-id="5fa62-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="5fa62-221">Chyby při **vyvolání centra** jsou výjimky vyvolané při vyvolání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="5fa62-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="5fa62-222">Chyby **přenosu** jsou chyby připojení vyvolané během žádosti nebo odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="5fa62-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="5fa62-223">**Chyby: celkem**</span><span class="sxs-lookup"><span data-stu-id="5fa62-223">**Errors: All Total**</span></span>
- <span data-ttu-id="5fa62-224">**Chyby: vše/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="5fa62-225">**Chyby: celkové rozlišení centra**</span><span class="sxs-lookup"><span data-stu-id="5fa62-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="5fa62-226">**Chyby: řešení centra/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="5fa62-227">**Chyby: vyvolání centra celkem**</span><span class="sxs-lookup"><span data-stu-id="5fa62-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="5fa62-228">**Chyby: vyvolání centra/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="5fa62-229">**Chyby: celkový přenos**</span><span class="sxs-lookup"><span data-stu-id="5fa62-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="5fa62-230">**Chyby: přenos za sekundu**</span><span class="sxs-lookup"><span data-stu-id="5fa62-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="5fa62-231">**Metriky škálování**</span><span class="sxs-lookup"><span data-stu-id="5fa62-231">**Scaleout metrics**</span></span>

<span data-ttu-id="5fa62-232">Následující metriky měří provoz a chyby generované poskytovatelem škálování.</span><span class="sxs-lookup"><span data-stu-id="5fa62-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="5fa62-233">**Proud** v tomto kontextu je jednotka škálování používaná poskytovatelem škálování. Toto je tabulka, pokud se používá SQL Server, pokud se používá Service Bus a předplatné, pokud se používá Redis.</span><span class="sxs-lookup"><span data-stu-id="5fa62-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="5fa62-234">Každý datový proud zajišťuje seřazené operace čtení a zápisu; jeden datový proud je potenciálním kritickým bodem škálování, takže počet datových proudů se může zvýšit, aby se snížila jeho kritická místa.</span><span class="sxs-lookup"><span data-stu-id="5fa62-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="5fa62-235">Pokud se používá víc datových proudů, bude signál automaticky distribuovat (horizontálních oddílů) zprávy napříč těmito proudy způsobem, který zajistí, aby se zprávy odesílané z libovolného připojení dostaly v daném pořadí.</span><span class="sxs-lookup"><span data-stu-id="5fa62-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="5fa62-236">Nastavení [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) řídí délku fronty pro odesílání na škálování udržované signálem.</span><span class="sxs-lookup"><span data-stu-id="5fa62-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="5fa62-237">Nastavením hodnoty na hodnotu větší než 0 budou všechny zprávy ve frontě pro odesílání odesílány postupně po nakonfigurované naplánování zasílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="5fa62-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="5fa62-238">Pokud velikost fronty překročí nakonfigurovanou délku, následné výzvy k odeslání selžou okamžitě s chybou [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) , dokud počet zpráv ve frontě nebude menší, než je nastavení znovu.</span><span class="sxs-lookup"><span data-stu-id="5fa62-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="5fa62-239">Zařazení do fronty je ve výchozím nastavení zakázáno, protože implementované plány pro kontrolu mají obvykle vlastní frontu nebo řízení toku.</span><span class="sxs-lookup"><span data-stu-id="5fa62-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="5fa62-240">V případě SQL Server sdružování připojení efektivně omezuje počet odeslaných v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="5fa62-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="5fa62-241">Ve výchozím nastavení se pro SQL Server a Redis používá jenom jeden datový proud, pro Service Bus se používá pět datových proudů a zařazení do fronty je zakázané, ale tato nastavení se dají změnit pomocí konfigurace na SQL Server a Service Bus:</span><span class="sxs-lookup"><span data-stu-id="5fa62-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="5fa62-242">**Kód serveru .NET pro konfiguraci počtu tabulek a délky fronty pro SQL Serverho naplánování**</span><span class="sxs-lookup"><span data-stu-id="5fa62-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="5fa62-243">**Kód serveru .NET pro konfiguraci počtu témat a délky fronty pro Service Busho naplánování**</span><span class="sxs-lookup"><span data-stu-id="5fa62-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="5fa62-244">Datový proud **vyrovnávací paměti** je ten, který přešel do chybového stavu. Pokud je datový proud v chybném stavu, všechny zprávy odeslané do plánu pro replánování selžou okamžitě, dokud datový proud přestane selhat.</span><span class="sxs-lookup"><span data-stu-id="5fa62-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="5fa62-245">**Délka fronty pro odesílání** je počet zpráv, které byly publikovány, ale nebyly dosud odeslány.</span><span class="sxs-lookup"><span data-stu-id="5fa62-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="5fa62-246">**Přijaté zprávy ve sběrnici pro škálování/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="5fa62-247">**Proudy škálování celkem**</span><span class="sxs-lookup"><span data-stu-id="5fa62-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="5fa62-248">**Otevřené proudy škálování**</span><span class="sxs-lookup"><span data-stu-id="5fa62-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="5fa62-249">**Vyrovnávací paměť streamování pro horizontální navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="5fa62-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="5fa62-250">**Celkový počet chyb při škálování**</span><span class="sxs-lookup"><span data-stu-id="5fa62-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="5fa62-251">**Chyby horizontálního navýšení kapacity/s**</span><span class="sxs-lookup"><span data-stu-id="5fa62-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="5fa62-252">**Délka fronty pro odesílání pro škálování**</span><span class="sxs-lookup"><span data-stu-id="5fa62-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="5fa62-253">Další informace o tom, jak se tyto čítače měří, najdete v tématu [škálování signálu pomocí Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="5fa62-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="5fa62-254">Používání dalších čítačů výkonu</span><span class="sxs-lookup"><span data-stu-id="5fa62-254">Using other performance counters</span></span>

<span data-ttu-id="5fa62-255">Následující čítače výkonu mohou být užitečné také při monitorování výkonu aplikace.</span><span class="sxs-lookup"><span data-stu-id="5fa62-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="5fa62-256">**Rezident**</span><span class="sxs-lookup"><span data-stu-id="5fa62-256">**Memory**</span></span>

- <span data-ttu-id="5fa62-257">Paměť .NET CLR\\počet bajtů ve všech haldách (pro W3wp)</span><span class="sxs-lookup"><span data-stu-id="5fa62-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="5fa62-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="5fa62-258">**ASP.NET**</span></span>

- <span data-ttu-id="5fa62-259">ASP. NET\Requests – aktuální</span><span class="sxs-lookup"><span data-stu-id="5fa62-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="5fa62-260">ASP. NET\Queued</span><span class="sxs-lookup"><span data-stu-id="5fa62-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="5fa62-261">ASP. NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="5fa62-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="5fa62-262">**VČETNĚ**</span><span class="sxs-lookup"><span data-stu-id="5fa62-262">**CPU**</span></span>

- <span data-ttu-id="5fa62-263">Čas procesoru Information\Processor</span><span class="sxs-lookup"><span data-stu-id="5fa62-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="5fa62-264">**PROTOKOL TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="5fa62-264">**TCP/IP**</span></span>

- <span data-ttu-id="5fa62-265">TCPv6/připojení navázáno</span><span class="sxs-lookup"><span data-stu-id="5fa62-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="5fa62-266">TCPv4/připojení navázáno</span><span class="sxs-lookup"><span data-stu-id="5fa62-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="5fa62-267">**Webová služba**</span><span class="sxs-lookup"><span data-stu-id="5fa62-267">**Web Service**</span></span>

- <span data-ttu-id="5fa62-268">Připojení k webu Service\Current</span><span class="sxs-lookup"><span data-stu-id="5fa62-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="5fa62-269">Připojení k webu Service\Maximum</span><span class="sxs-lookup"><span data-stu-id="5fa62-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="5fa62-270">**Dělení na vlákna**</span><span class="sxs-lookup"><span data-stu-id="5fa62-270">**Threading**</span></span>

- <span data-ttu-id="5fa62-271">Zámky a vlákna .NET CLR\\Počet aktuálních logických vláken</span><span class="sxs-lookup"><span data-stu-id="5fa62-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="5fa62-272">Zámky a vlákna .NET CLR\\Počet aktuálních fyzických vláken</span><span class="sxs-lookup"><span data-stu-id="5fa62-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="5fa62-273">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="5fa62-273">Other Resources</span></span>

<span data-ttu-id="5fa62-274">Další informace o sledování a ladění výkonu ASP.NET najdete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="5fa62-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="5fa62-275">[Přehled výkonu ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="5fa62-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="5fa62-276">Použití vláken ASP.NET ve službě IIS 7,5, IIS 7,0 a IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="5fa62-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="5fa62-277">&lt;applicationPool&gt; – element (nastavení webu)</span><span class="sxs-lookup"><span data-stu-id="5fa62-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
