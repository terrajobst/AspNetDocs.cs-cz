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
# <a name="signalr-performance-signalr-1x"></a><span data-ttu-id="e99d4-103">Výkon aplikace SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="e99d4-103">SignalR Performance (SignalR 1.x)</span></span>

<span data-ttu-id="e99d4-104">Po [Fletcheru](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="e99d4-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="e99d4-105">Toto téma popisuje, jak navrhnout, změřit a zvýšit výkon v aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="e99d4-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>

<span data-ttu-id="e99d4-106">Nedávný prezentační výkon a škálování signálu najdete v tématu [škálování webu v reálném čase pomocí ASP.NET signálu](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="e99d4-106">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="e99d4-107">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="e99d4-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="e99d4-108">Aspekty návrhu</span><span class="sxs-lookup"><span data-stu-id="e99d4-108">Design considerations</span></span>](#design)
- [<span data-ttu-id="e99d4-109">Ladění serveru signálu pro výkon</span><span class="sxs-lookup"><span data-stu-id="e99d4-109">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="e99d4-110">Řešení potíží s výkonem</span><span class="sxs-lookup"><span data-stu-id="e99d4-110">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="e99d4-111">Použití čítačů výkonu signalizace</span><span class="sxs-lookup"><span data-stu-id="e99d4-111">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="e99d4-112">Používání dalších čítačů výkonu</span><span class="sxs-lookup"><span data-stu-id="e99d4-112">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="e99d4-113">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="e99d4-113">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="e99d4-114">Na co dát pozor při navrhování</span><span class="sxs-lookup"><span data-stu-id="e99d4-114">Design considerations</span></span>

<span data-ttu-id="e99d4-115">Tato část popisuje vzory, které je možné implementovat během návrhu aplikace pro signalizaci, aby se zajistilo, že výkon nebude bráněno vygenerováním zbytečných síťových přenosů.</span><span class="sxs-lookup"><span data-stu-id="e99d4-115">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="e99d4-116">Frekvence omezování zpráv</span><span class="sxs-lookup"><span data-stu-id="e99d4-116">Throttling message frequency</span></span>

<span data-ttu-id="e99d4-117">I v aplikaci, která odesílá zprávy s vysokou frekvencí (například herní aplikace v reálném čase), nemusí většina aplikací odesílat více než několik zpráv za sekundu.</span><span class="sxs-lookup"><span data-stu-id="e99d4-117">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="e99d4-118">Chcete-li snížit množství provozu, který každý z nich vygeneruje, je možné implementovat smyčku zpráv, která zařadí do fronty a odesílá zprávy s výjimkou pevné sazby (to znamená, že až v okamžiku, kdy jsou v této době zprávy, bude odesláno až do určitého počtu zpráv). terval k odeslání).</span><span class="sxs-lookup"><span data-stu-id="e99d4-118">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="e99d4-119">Ukázková aplikace, která omezuje zprávy na určitou míru (od klienta i serveru), najdete v části [vysoká frekvence v reálném čase pomocí nástroje Signal](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="e99d4-119">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="e99d4-120">Zmenšení velikosti zprávy</span><span class="sxs-lookup"><span data-stu-id="e99d4-120">Reducing message size</span></span>

<span data-ttu-id="e99d4-121">Můžete zmenšit velikost zprávy signálu tím, že zmenšíte velikost serializovaných objektů.</span><span class="sxs-lookup"><span data-stu-id="e99d4-121">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="e99d4-122">Pokud v kódu serveru odesíláte objekt, který obsahuje vlastnosti, které není nutné přenést, zabraňte serializaci těchto vlastností pomocí atributu `JsonIgnore`.</span><span class="sxs-lookup"><span data-stu-id="e99d4-122">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="e99d4-123">Názvy vlastností jsou také uloženy ve zprávě; názvy vlastností lze zkrátit pomocí atributu `JsonProperty`.</span><span class="sxs-lookup"><span data-stu-id="e99d4-123">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="e99d4-124">Následující příklad kódu ukazuje, jak vyloučit vlastnost ze zasílání klientovi a jak zkrátit názvy vlastností:</span><span class="sxs-lookup"><span data-stu-id="e99d4-124">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="e99d4-125">**Kód serveru .NET, který ukazuje atribut JsonIgnore pro vyloučení dat z odeslání do klienta, a atribut JsonProperty pro snížení velikosti zprávy**</span><span class="sxs-lookup"><span data-stu-id="e99d4-125">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="e99d4-126">Aby se zachovala čitelnost a udržovatelnost v kódu klienta, zkrácené názvy vlastností lze po přijetí zprávy přemapovat na názvy, které jsou v názvu.</span><span class="sxs-lookup"><span data-stu-id="e99d4-126">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="e99d4-127">Následující příklad kódu ukazuje jeden z možných způsobů, jak přemapování zkrácených názvů na delší, definováním kontraktu zprávy (mapování) a použitím funkce `reMap` pro použití této smlouvy na optimalizované třídě zpráv:</span><span class="sxs-lookup"><span data-stu-id="e99d4-127">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="e99d4-128">**Kód JavaScriptu na straně klienta, který přemapuje názvy zkrácených vlastností na názvy, které lze číst lidmi**</span><span class="sxs-lookup"><span data-stu-id="e99d4-128">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="e99d4-129">Názvy mohou být zkráceny ve zprávách od klienta k serveru, a to pomocí stejné metody.</span><span class="sxs-lookup"><span data-stu-id="e99d4-129">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="e99d4-130">Snížení výkonu paměti (tj. množství paměti využitého pro zprávu) objektu Message může také zlepšit výkon.</span><span class="sxs-lookup"><span data-stu-id="e99d4-130">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="e99d4-131">Pokud například není potřeba plný rozsah `int`, můžete místo toho použít `short` nebo `byte`.</span><span class="sxs-lookup"><span data-stu-id="e99d4-131">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="e99d4-132">Vzhledem k tomu, že se zprávy ukládají do sběrnice zpráv v paměti serveru, zmenšení velikosti zpráv může také řešit problémy s pamětí serveru.</span><span class="sxs-lookup"><span data-stu-id="e99d4-132">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="e99d4-133">Ladění serveru signálu pro výkon</span><span class="sxs-lookup"><span data-stu-id="e99d4-133">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="e99d4-134">Následující nastavení konfigurace můžete použít k vyladění serveru pro lepší výkon v aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="e99d4-134">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="e99d4-135">Obecné informace o tom, jak zlepšit výkon v aplikaci ASP.NET, najdete v tématu [zlepšení výkonu ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="e99d4-135">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="e99d4-136">**Nastavení konfigurace signálu**</span><span class="sxs-lookup"><span data-stu-id="e99d4-136">**SignalR configuration settings**</span></span>

- <span data-ttu-id="e99d4-137">**DefaultMessageBufferSize**: ve výchozím nastavení zachovává signál zprávy 1000 v paměti na jedno centrum a připojení.</span><span class="sxs-lookup"><span data-stu-id="e99d4-137">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="e99d4-138">Pokud se používají velké zprávy, může to způsobit problémy paměti, které je možné zmírnit snížením této hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e99d4-138">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="e99d4-139">Toto nastavení lze nastavit v obslužné rutině události `Application_Start` v aplikaci ASP.NET nebo v metodě `Configuration` třídy spouštění OWIN v samoobslužné aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e99d4-139">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="e99d4-140">Následující příklad ukazuje, jak tuto hodnotu omezit, aby se snížilo nároky na paměť aplikace, aby se snížila velikost využité paměti serveru:</span><span class="sxs-lookup"><span data-stu-id="e99d4-140">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="e99d4-141">**Kód .NET serveru v Global. asax pro snížení výchozí velikosti vyrovnávací paměti zpráv**</span><span class="sxs-lookup"><span data-stu-id="e99d4-141">**.NET server code in Global.asax for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="e99d4-142">**Nastavení konfigurace služby IIS**</span><span class="sxs-lookup"><span data-stu-id="e99d4-142">**IIS configuration settings**</span></span>

- <span data-ttu-id="e99d4-143">**Maximální počet souběžných požadavků na aplikaci**: zvýšení počtu souběžných požadavků služby IIS bude zvyšovat prostředky serveru, které jsou k dispozici pro poskytování požadavků.</span><span class="sxs-lookup"><span data-stu-id="e99d4-143">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="e99d4-144">Výchozí hodnota je 5000; Chcete-li toto nastavení zvýšit, spusťte v příkazovém řádku se zvýšenými oprávněními následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="e99d4-144">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

<span data-ttu-id="e99d4-145">**Nastavení konfigurace ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="e99d4-145">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="e99d4-146">Tato část obsahuje nastavení konfigurace, která se dají nastavit v souboru `aspnet.config`.</span><span class="sxs-lookup"><span data-stu-id="e99d4-146">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="e99d4-147">Tento soubor se nachází v jednom ze dvou umístění v závislosti na platformě:</span><span class="sxs-lookup"><span data-stu-id="e99d4-147">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="e99d4-148">Nastavení ASP.NET, která mohou zlepšit výkon signálu, zahrnují následující:</span><span class="sxs-lookup"><span data-stu-id="e99d4-148">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="e99d4-149">**Maximální počet souběžných požadavků na procesor**: zvýšení tohoto nastavení může zmírnit kritická místa výkonu.</span><span class="sxs-lookup"><span data-stu-id="e99d4-149">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="e99d4-150">Chcete-li toto nastavení zvýšit, přidejte do souboru `aspnet.config` následující nastavení konfigurace:</span><span class="sxs-lookup"><span data-stu-id="e99d4-150">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="e99d4-151">**Limit fronty požadavků**: Pokud celkový počet připojení překročí nastavení `maxConcurrentRequestsPerCPU`, ASP.NET spustí omezování požadavků pomocí fronty.</span><span class="sxs-lookup"><span data-stu-id="e99d4-151">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="e99d4-152">Pokud chcete zvětšit velikost fronty, můžete nastavení `requestQueueLimit` zvýšit.</span><span class="sxs-lookup"><span data-stu-id="e99d4-152">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="e99d4-153">Provedete to tak, že do uzlu `processModel` v `config/machine.config` přidáte následující nastavení konfigurace (místo `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="e99d4-153">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="e99d4-154">Řešení potíží s výkonem</span><span class="sxs-lookup"><span data-stu-id="e99d4-154">Troubleshooting performance issues</span></span>

<span data-ttu-id="e99d4-155">Tato část popisuje způsoby, jak najít kritická místa výkonu ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e99d4-155">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="e99d4-156">Ověřuje se, jestli se používá protokol WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e99d4-156">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="e99d4-157">I když může nástroj pro komunikaci mezi klientem a serverem používat nejrůznější přenos, nabízí WebSocket značnou výhodu výkonu a měla by se používat v případě, že ho podporuje klient a Server.</span><span class="sxs-lookup"><span data-stu-id="e99d4-157">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="e99d4-158">Pokud chcete zjistit, jestli váš klient a server splňují požadavky na WebSocket, přečtěte si téma [přenosy a záložní](../getting-started/introduction-to-signalr.md#transports)služby.</span><span class="sxs-lookup"><span data-stu-id="e99d4-158">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="e99d4-159">Chcete-li zjistit, jaký přenos se v aplikaci používá, můžete použít nástroje pro vývojáře v prohlížeči a prohlédnout si protokoly, abyste zjistili, jaký přenos se pro připojení používá.</span><span class="sxs-lookup"><span data-stu-id="e99d4-159">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="e99d4-160">Informace o používání nástrojů pro vývoj v prohlížeči v Internet Exploreru a Chrome najdete v tématu [přenosy a záložní](../getting-started/introduction-to-signalr.md#transports)prvky.</span><span class="sxs-lookup"><span data-stu-id="e99d4-160">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="e99d4-161">Použití čítačů výkonu signalizace</span><span class="sxs-lookup"><span data-stu-id="e99d4-161">Using SignalR performance counters</span></span>

<span data-ttu-id="e99d4-162">Tato část popisuje, jak povolit a používat čítače výkonu signálů, které najdete v balíčku `Microsoft.AspNet.SignalR.Utils`.</span><span class="sxs-lookup"><span data-stu-id="e99d4-162">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="e99d4-163">Instalace signalizace. exe</span><span class="sxs-lookup"><span data-stu-id="e99d4-163">Installing signalr.exe</span></span>

<span data-ttu-id="e99d4-164">Čítače výkonu lze přidat k serveru pomocí nástroje s názvem Signal. exe.</span><span class="sxs-lookup"><span data-stu-id="e99d4-164">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="e99d4-165">K instalaci tohoto nástroje použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="e99d4-165">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="e99d4-166">V aplikaci Visual Studio vyberte **nástroje** > **správce balíčků NuGet** > **Spravovat balíčky NuGet pro řešení** .</span><span class="sxs-lookup"><span data-stu-id="e99d4-166">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="e99d4-167">Vyhledejte **signál. utils**a vyberte nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="e99d4-167">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="e99d4-168">Přijměte licenční smlouvu pro instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="e99d4-168">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="e99d4-169">Signál. exe bude nainstalován do `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span><span class="sxs-lookup"><span data-stu-id="e99d4-169">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="e99d4-170">Instalace čítačů výkonu pomocí nástroje Signaler. exe</span><span class="sxs-lookup"><span data-stu-id="e99d4-170">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="e99d4-171">Chcete-li nainstalovat čítače výkonu signálu, spusťte příkaz Signal. exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:</span><span class="sxs-lookup"><span data-stu-id="e99d4-171">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="e99d4-172">Chcete-li odebrat čítače výkonu signálu, spusťte příkaz Signal. exe v příkazovém řádku se zvýšenými oprávněními s následujícím parametrem:</span><span class="sxs-lookup"><span data-stu-id="e99d4-172">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="e99d4-173">Čítače výkonu signálu</span><span class="sxs-lookup"><span data-stu-id="e99d4-173">SignalR Performance counters</span></span>

<span data-ttu-id="e99d4-174">Balíček nástroje nainstaluje následující čítače výkonu.</span><span class="sxs-lookup"><span data-stu-id="e99d4-174">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="e99d4-175">Čítače "celkem" měří počet událostí od posledního fondu aplikací nebo restartování serveru.</span><span class="sxs-lookup"><span data-stu-id="e99d4-175">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="e99d4-176">**Metriky připojení**</span><span class="sxs-lookup"><span data-stu-id="e99d4-176">**Connection metrics**</span></span>

<span data-ttu-id="e99d4-177">Následující metriky měří události životnosti připojení, ke kterým dojde.</span><span class="sxs-lookup"><span data-stu-id="e99d4-177">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="e99d4-178">Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="e99d4-178">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="e99d4-179">**Připojení připojena**</span><span class="sxs-lookup"><span data-stu-id="e99d4-179">**Connections Connected**</span></span>
- <span data-ttu-id="e99d4-180">**Připojení se znovu připojila.**</span><span class="sxs-lookup"><span data-stu-id="e99d4-180">**Connections Reconnected**</span></span>
- <span data-ttu-id="e99d4-181">**Odpojená připojení**</span><span class="sxs-lookup"><span data-stu-id="e99d4-181">**Connections Disconnected**</span></span>
- <span data-ttu-id="e99d4-182">**Aktuální připojení**</span><span class="sxs-lookup"><span data-stu-id="e99d4-182">**Connections Current**</span></span>

<span data-ttu-id="e99d4-183">**Metriky zpráv**</span><span class="sxs-lookup"><span data-stu-id="e99d4-183">**Message metrics**</span></span>

<span data-ttu-id="e99d4-184">Následující metriky měří přenos zpráv generovaných signálem.</span><span class="sxs-lookup"><span data-stu-id="e99d4-184">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="e99d4-185">**Počet přijatých zpráv o připojení**</span><span class="sxs-lookup"><span data-stu-id="e99d4-185">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="e99d4-186">**Odeslané zprávy o připojení celkem**</span><span class="sxs-lookup"><span data-stu-id="e99d4-186">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="e99d4-187">**Přijaté zprávy o připojení za sekundu**</span><span class="sxs-lookup"><span data-stu-id="e99d4-187">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="e99d4-188">**Odeslané zprávy o připojení za sekundu**</span><span class="sxs-lookup"><span data-stu-id="e99d4-188">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="e99d4-189">**Metriky sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="e99d4-189">**Message bus metrics**</span></span>

<span data-ttu-id="e99d4-190">Následující metriky měří provoz prostřednictvím interní sběrnice zpráv signálem, fronty, ve které jsou umístěny všechny příchozí a odchozí zprávy signálu.</span><span class="sxs-lookup"><span data-stu-id="e99d4-190">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="e99d4-191">Zpráva se **publikuje** při odeslání nebo vysílání.</span><span class="sxs-lookup"><span data-stu-id="e99d4-191">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="e99d4-192">**Předplatitelem** v tomto kontextu je předplatné ze sběrnice zpráv. hodnota by měla být rovna počtu klientů a samotnému serveru.</span><span class="sxs-lookup"><span data-stu-id="e99d4-192">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="e99d4-193">**Přidělený pracovník** je komponenta, která odesílá data do aktivních připojení. **zaneprázdněný pracovní proces** je jedním z nich, který aktivně posílá zprávu.</span><span class="sxs-lookup"><span data-stu-id="e99d4-193">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="e99d4-194">**Přijaté zprávy sběrnice zpráv celkem**</span><span class="sxs-lookup"><span data-stu-id="e99d4-194">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="e99d4-195">**Přijaté zprávy sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-195">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="e99d4-196">**Publikované zprávy sběrnice zpráv celkem**</span><span class="sxs-lookup"><span data-stu-id="e99d4-196">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="e99d4-197">**Publikované zprávy sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-197">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="e99d4-198">**Předplatitelé sběrnice zpráv aktuální**</span><span class="sxs-lookup"><span data-stu-id="e99d4-198">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="e99d4-199">**Předplatitelé sběrnice zpráv celkem**</span><span class="sxs-lookup"><span data-stu-id="e99d4-199">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="e99d4-200">**Předplatitelé sběrnice zpráv/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-200">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="e99d4-201">**Pracovníci přidělení sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="e99d4-201">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="e99d4-202">**Zaneprázdněné pracovní procesy sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="e99d4-202">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="e99d4-203">**Aktuální témata sběrnice zpráv**</span><span class="sxs-lookup"><span data-stu-id="e99d4-203">**Message Bus Topics Current**</span></span>

<span data-ttu-id="e99d4-204">**Metriky chyb**</span><span class="sxs-lookup"><span data-stu-id="e99d4-204">**Error metrics**</span></span>

<span data-ttu-id="e99d4-205">Následující metriky měří chyby vygenerované přenosem zpráv signálem.</span><span class="sxs-lookup"><span data-stu-id="e99d4-205">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="e99d4-206">K chybám **rozlišení centra** dochází v případě, že nelze přeložit centrum nebo metodu centra.</span><span class="sxs-lookup"><span data-stu-id="e99d4-206">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="e99d4-207">Chyby při **vyvolání centra** jsou výjimky vyvolané při vyvolání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="e99d4-207">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="e99d4-208">Chyby **přenosu** jsou chyby připojení vyvolané během žádosti nebo odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="e99d4-208">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="e99d4-209">**Chyby: celkem**</span><span class="sxs-lookup"><span data-stu-id="e99d4-209">**Errors: All Total**</span></span>
- <span data-ttu-id="e99d4-210">**Chyby: vše/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-210">**Errors: All/Sec**</span></span>
- <span data-ttu-id="e99d4-211">**Chyby: celkové rozlišení centra**</span><span class="sxs-lookup"><span data-stu-id="e99d4-211">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="e99d4-212">**Chyby: řešení centra/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-212">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="e99d4-213">**Chyby: vyvolání centra celkem**</span><span class="sxs-lookup"><span data-stu-id="e99d4-213">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="e99d4-214">**Chyby: vyvolání centra/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-214">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="e99d4-215">**Chyby: celkový přenos**</span><span class="sxs-lookup"><span data-stu-id="e99d4-215">**Errors: Transport Total**</span></span>
- <span data-ttu-id="e99d4-216">**Chyby: přenos za sekundu**</span><span class="sxs-lookup"><span data-stu-id="e99d4-216">**Errors: Transport/Sec**</span></span>

<span data-ttu-id="e99d4-217">**Metriky škálování**</span><span class="sxs-lookup"><span data-stu-id="e99d4-217">**Scaleout metrics**</span></span>

<span data-ttu-id="e99d4-218">Následující metriky měří provoz a chyby generované poskytovatelem škálování.</span><span class="sxs-lookup"><span data-stu-id="e99d4-218">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="e99d4-219">**Proud** v tomto kontextu je jednotka škálování používaná poskytovatelem škálování. Toto je tabulka, pokud se používá SQL Server, pokud se používá Service Bus a předplatné, pokud se používá Redis.</span><span class="sxs-lookup"><span data-stu-id="e99d4-219">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="e99d4-220">Ve výchozím nastavení se používá pouze jeden datový proud, ale lze ho zvýšit prostřednictvím konfigurace SQL Server a Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e99d4-220">By default, only one stream is used, but this can be increased through configuration on SQL Server and Service Bus.</span></span> <span data-ttu-id="e99d4-221">Datový proud **vyrovnávací paměti** je ten, který přešel do chybového stavu. Pokud je datový proud v chybném stavu, všechny zprávy odeslané do plánu pro replánování selžou okamžitě, dokud datový proud přestane selhat.</span><span class="sxs-lookup"><span data-stu-id="e99d4-221">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="e99d4-222">**Délka fronty pro odesílání** je počet zpráv, které byly publikovány, ale nebyly dosud odeslány.</span><span class="sxs-lookup"><span data-stu-id="e99d4-222">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="e99d4-223">**Přijaté zprávy ve sběrnici pro škálování/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-223">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="e99d4-224">**Proudy škálování celkem**</span><span class="sxs-lookup"><span data-stu-id="e99d4-224">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="e99d4-225">**Otevřené proudy škálování**</span><span class="sxs-lookup"><span data-stu-id="e99d4-225">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="e99d4-226">**Vyrovnávací paměť streamování pro horizontální navýšení kapacity**</span><span class="sxs-lookup"><span data-stu-id="e99d4-226">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="e99d4-227">**Celkový počet chyb při škálování**</span><span class="sxs-lookup"><span data-stu-id="e99d4-227">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="e99d4-228">**Chyby horizontálního navýšení kapacity/s**</span><span class="sxs-lookup"><span data-stu-id="e99d4-228">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="e99d4-229">**Délka fronty pro odesílání pro škálování**</span><span class="sxs-lookup"><span data-stu-id="e99d4-229">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="e99d4-230">Další informace o tom, jak se tyto čítače měří, najdete v tématu [škálování signálu pomocí Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="e99d4-230">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="e99d4-231">Používání dalších čítačů výkonu</span><span class="sxs-lookup"><span data-stu-id="e99d4-231">Using other performance counters</span></span>

<span data-ttu-id="e99d4-232">Následující čítače výkonu mohou být užitečné také při monitorování výkonu aplikace.</span><span class="sxs-lookup"><span data-stu-id="e99d4-232">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="e99d4-233">**Rezident**</span><span class="sxs-lookup"><span data-stu-id="e99d4-233">**Memory**</span></span>

- <span data-ttu-id="e99d4-234">Paměť .NET CLR počet bajtů ve všech haldách (pro W3wp)</span><span class="sxs-lookup"><span data-stu-id="e99d4-234">.NET CLR Memory# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="e99d4-235">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="e99d4-235">**ASP.NET**</span></span>

- <span data-ttu-id="e99d4-236">ASP. NET\Requests – aktuální</span><span class="sxs-lookup"><span data-stu-id="e99d4-236">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="e99d4-237">ASP. NET\Queued</span><span class="sxs-lookup"><span data-stu-id="e99d4-237">ASP.NET\Queued</span></span>
- <span data-ttu-id="e99d4-238">ASP. NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="e99d4-238">ASP.NET\Rejected</span></span>

<span data-ttu-id="e99d4-239">**VČETNĚ**</span><span class="sxs-lookup"><span data-stu-id="e99d4-239">**CPU**</span></span>

- <span data-ttu-id="e99d4-240">Čas procesoru Information\Processor</span><span class="sxs-lookup"><span data-stu-id="e99d4-240">Processor Information\Processor Time</span></span>

<span data-ttu-id="e99d4-241">**PROTOKOL TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="e99d4-241">**TCP/IP**</span></span>

- <span data-ttu-id="e99d4-242">TCPv6/připojení navázáno</span><span class="sxs-lookup"><span data-stu-id="e99d4-242">TCPv6/Connections Established</span></span>
- <span data-ttu-id="e99d4-243">TCPv4/připojení navázáno</span><span class="sxs-lookup"><span data-stu-id="e99d4-243">TCPv4/Connections Established</span></span>

<span data-ttu-id="e99d4-244">**Webová služba**</span><span class="sxs-lookup"><span data-stu-id="e99d4-244">**Web Service**</span></span>

- <span data-ttu-id="e99d4-245">Připojení k webu Service\Current</span><span class="sxs-lookup"><span data-stu-id="e99d4-245">Web Service\Current Connections</span></span>
- <span data-ttu-id="e99d4-246">Připojení k webu Service\Maximum</span><span class="sxs-lookup"><span data-stu-id="e99d4-246">Web Service\Maximum Connections</span></span>

<span data-ttu-id="e99d4-247">**Dělení na vlákna**</span><span class="sxs-lookup"><span data-stu-id="e99d4-247">**Threading**</span></span>

- <span data-ttu-id="e99d4-248">LocksAndThreads .NET CLR\# aktuálních logických vláken</span><span class="sxs-lookup"><span data-stu-id="e99d4-248">.NET CLR LocksAndThreads\# of current logical Threads</span></span>
- <span data-ttu-id="e99d4-249">LocksAnd vláken .NET CLR\# aktuálních fyzických vláken</span><span class="sxs-lookup"><span data-stu-id="e99d4-249">.NET CLR LocksAnd Threads\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="e99d4-250">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="e99d4-250">Other Resources</span></span>

<span data-ttu-id="e99d4-251">Další informace o sledování a ladění výkonu ASP.NET najdete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="e99d4-251">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="e99d4-252">[Přehled výkonu ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="e99d4-252">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="e99d4-253">Použití vláken ASP.NET ve službě IIS 7,5, IIS 7,0 a IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="e99d4-253">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="e99d4-254">&lt;applicationPool&gt; – element (nastavení webu)</span><span class="sxs-lookup"><span data-stu-id="e99d4-254">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
