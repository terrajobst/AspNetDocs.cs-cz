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
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="1a141-103">Průvodce rozhraním API pro centra ASP.NET Signaler –C#klient .NET ()</span><span class="sxs-lookup"><span data-stu-id="1a141-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="1a141-104">V tomto dokumentu najdete Úvod k používání rozhraní API centra pro službu Signal verze 2 v klientech rozhraní .NET, jako je Windows Store (WinRT), WPF, Silverlight a konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1a141-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="1a141-105">Rozhraní API pro centra signalizace vám umožní provádět Vzdálená volání procedur (RPC) ze serveru pro připojené klienty a klienty na server.</span><span class="sxs-lookup"><span data-stu-id="1a141-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="1a141-106">V kódu serveru můžete definovat metody, které mohou být volány klienty, a volat metody, které jsou spouštěny v klientovi.</span><span class="sxs-lookup"><span data-stu-id="1a141-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="1a141-107">V kódu klienta definujete metody, které mohou být volány ze serveru, a voláte metody, které jsou spuštěny na serveru.</span><span class="sxs-lookup"><span data-stu-id="1a141-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="1a141-108">Signalizace postará o všechny instalace klienta na server za vás.</span><span class="sxs-lookup"><span data-stu-id="1a141-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="1a141-109">Nástroj Signal také nabízí nižší úroveň rozhraní API označované jako trvalá připojení.</span><span class="sxs-lookup"><span data-stu-id="1a141-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="1a141-110">Úvod do nástroje pro signalizaci, centra a trvalá připojení nebo v kurzu, který ukazuje, jak sestavit kompletní aplikaci signalizace, najdete v tématu [signaler-Začínáme](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="1a141-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="1a141-111">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="1a141-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="1a141-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1a141-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="1a141-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1a141-113">.NET 4.5</span></span>
> - <span data-ttu-id="1a141-114">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="1a141-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="1a141-115">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="1a141-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="1a141-116">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="1a141-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="1a141-117">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="1a141-117">Questions and comments</span></span>
>
> <span data-ttu-id="1a141-118">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="1a141-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="1a141-119">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="1a141-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="1a141-120">Přehled</span><span class="sxs-lookup"><span data-stu-id="1a141-120">Overview</span></span>

<span data-ttu-id="1a141-121">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="1a141-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="1a141-122">Instalace klienta</span><span class="sxs-lookup"><span data-stu-id="1a141-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="1a141-123">Jak navázat připojení</span><span class="sxs-lookup"><span data-stu-id="1a141-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="1a141-124">Připojení mezi doménami z klientů Silverlight</span><span class="sxs-lookup"><span data-stu-id="1a141-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="1a141-125">Konfigurace připojení</span><span class="sxs-lookup"><span data-stu-id="1a141-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="1a141-126">Nastavení maximálního počtu souběžných připojení v klientech WPF</span><span class="sxs-lookup"><span data-stu-id="1a141-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="1a141-127">Určení parametrů řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="1a141-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="1a141-128">Určení způsobu přenosu</span><span class="sxs-lookup"><span data-stu-id="1a141-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="1a141-129">Určení hlaviček protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="1a141-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="1a141-130">Určení klientských certifikátů</span><span class="sxs-lookup"><span data-stu-id="1a141-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="1a141-131">Postup vytvoření centrálního proxy serveru</span><span class="sxs-lookup"><span data-stu-id="1a141-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="1a141-132">Jak definovat metody v klientovi, které může server volat</span><span class="sxs-lookup"><span data-stu-id="1a141-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="1a141-133">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="1a141-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="1a141-134">Metody s parametry, které určují typy parametrů</span><span class="sxs-lookup"><span data-stu-id="1a141-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="1a141-135">Metody s parametry, které určují dynamické objekty pro parametry</span><span class="sxs-lookup"><span data-stu-id="1a141-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="1a141-136">Postup odebrání obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="1a141-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="1a141-137">Postup volání metod serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="1a141-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="1a141-138">Postup zpracování událostí životního cyklu připojení</span><span class="sxs-lookup"><span data-stu-id="1a141-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="1a141-139">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="1a141-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="1a141-140">Postup povolení protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="1a141-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="1a141-141">Ukázky kódu aplikace WPF, Silverlight a konzolových aplikací pro metody klienta, které může server volat</span><span class="sxs-lookup"><span data-stu-id="1a141-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="1a141-142">Ukázkové klientské projekty rozhraní .NET najdete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="1a141-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="1a141-143">[Gustavo-armenta/signaler – ukázky](https://github.com/gustavo-armenta/SignalR-Samples) v GitHub.com (WinRT, Silverlight, příklady konzolových aplikací).</span><span class="sxs-lookup"><span data-stu-id="1a141-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="1a141-144">[DamianEdwards/signaler-MoveShapeDemo/MoveShape. Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (příklad WPF)</span><span class="sxs-lookup"><span data-stu-id="1a141-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="1a141-145">[Signaler/Microsoft. ASPNET. signale. Client. Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (příklad aplikace konzoly).</span><span class="sxs-lookup"><span data-stu-id="1a141-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="1a141-146">Dokumentaci k programování klientů serveru nebo JavaScriptu najdete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="1a141-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="1a141-147">Průvodce rozhraním API pro centra signálů – Server</span><span class="sxs-lookup"><span data-stu-id="1a141-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="1a141-148">Průvodce rozhraním API pro centra signálů – JavaScriptový klient</span><span class="sxs-lookup"><span data-stu-id="1a141-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="1a141-149">Odkazy na referenční témata rozhraní API odkazují na verzi rozhraní API .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="1a141-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="1a141-150">Pokud používáte .NET 4, přečtěte si téma věnované [verzi rozhraní API rozhraní .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="1a141-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="1a141-151">Instalace klienta</span><span class="sxs-lookup"><span data-stu-id="1a141-151">Client setup</span></span>

<span data-ttu-id="1a141-152">Nainstalujte balíček NuGet [Microsoft. ASPNET. Signal. Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) (ne balíček [Microsoft. ASPNET. signaler](http://nuget.org/packages/microsoft.aspnet.signalr) ).</span><span class="sxs-lookup"><span data-stu-id="1a141-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="1a141-153">Tento balíček podporuje klienty WinRT, Silverlight, WPF, konzolová aplikace a Windows Phone pro rozhraní .NET 4 i .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="1a141-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="1a141-154">Pokud je verze nástroje Signal, kterou jste na klientovi, odlišná od verze, kterou máte na serveru, je často možné, že se k rozdílu přizpůsobuje signál.</span><span class="sxs-lookup"><span data-stu-id="1a141-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="1a141-155">Například server, na kterém je spuštěný Signal, verze 2, bude podporovat klienty, kteří mají nainstalované verze 1.1. x, a taky klienty, kteří mají nainstalovanou verzi 2.</span><span class="sxs-lookup"><span data-stu-id="1a141-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="1a141-156">Pokud je rozdíl mezi verzí na serveru a verzí v klientovi moc velký nebo pokud je klient novější než server, Signal vyvolá výjimku `InvalidOperationException`, když se klient pokusí navázat připojení.</span><span class="sxs-lookup"><span data-stu-id="1a141-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="1a141-157">Chybová zpráva je "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span><span class="sxs-lookup"><span data-stu-id="1a141-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="1a141-158">Jak navázat připojení</span><span class="sxs-lookup"><span data-stu-id="1a141-158">How to establish a connection</span></span>

<span data-ttu-id="1a141-159">Než budete moct navázat připojení, musíte vytvořit objekt `HubConnection` a vytvořit proxy.</span><span class="sxs-lookup"><span data-stu-id="1a141-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="1a141-160">Chcete-li vytvořit připojení, zavolejte metodu `Start` u objektu `HubConnection`.</span><span class="sxs-lookup"><span data-stu-id="1a141-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="1a141-161">Pro klienty jazyka JavaScript musíte zaregistrovat alespoň jednu obslužnou rutinu události před voláním metody `Start` pro navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="1a141-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="1a141-162">Není to nutné pro klienty rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="1a141-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="1a141-163">V případě klientů v jazyce JavaScript vygenerovaný kód proxy automaticky vytvoří proxy pro všechna centra, která existují na serveru, a registruje obslužnou rutinu, jak označíte, která centra vaše klienti mají použít.</span><span class="sxs-lookup"><span data-stu-id="1a141-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="1a141-164">Ale u klienta .NET vytvoříte proxy rozbočovače ručně, takže signál předpokládá, že budete používat libovolné centrum, pro které vytvoříte proxy server.</span><span class="sxs-lookup"><span data-stu-id="1a141-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="1a141-165">Vzorový kód pro připojení ke službě signalizace používá výchozí adresu URL "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="1a141-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="1a141-166">Informace o tom, jak zadat jinou základní adresu URL, najdete v tématu [Průvodce rozhraním API pro centra ASP.NET Signal-Server-adresa URL/SignalR](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="1a141-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="1a141-167">Metoda `Start` se spouští asynchronně.</span><span class="sxs-lookup"><span data-stu-id="1a141-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="1a141-168">Chcete-li zajistit, že následné řádky kódu nebudou vykonány až po navázání spojení, použijte `await` v asynchronní metodě ASP.NET 4,5 nebo `.Wait()` v synchronní metodě.</span><span class="sxs-lookup"><span data-stu-id="1a141-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="1a141-169">Nepoužívejte `.Wait()` v klientovi WinRT.</span><span class="sxs-lookup"><span data-stu-id="1a141-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="1a141-170">Připojení mezi doménami z klientů Silverlight</span><span class="sxs-lookup"><span data-stu-id="1a141-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="1a141-171">Informace o tom, jak povolit mezidoménová připojení z klientů programu Silverlight, najdete v tématu [zajištění dostupnosti služby napříč hranicemi domén](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="1a141-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="1a141-172">Konfigurace připojení</span><span class="sxs-lookup"><span data-stu-id="1a141-172">How to configure the connection</span></span>

<span data-ttu-id="1a141-173">Před navázáním připojení můžete zadat některou z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="1a141-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="1a141-174">Omezení počtu souběžných připojení.</span><span class="sxs-lookup"><span data-stu-id="1a141-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="1a141-175">Parametry řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="1a141-175">Query string parameters.</span></span>
- <span data-ttu-id="1a141-176">Způsob přenosu.</span><span class="sxs-lookup"><span data-stu-id="1a141-176">The transport method.</span></span>
- <span data-ttu-id="1a141-177">Hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a141-177">HTTP headers.</span></span>
- <span data-ttu-id="1a141-178">Klientské certifikáty.</span><span class="sxs-lookup"><span data-stu-id="1a141-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="1a141-179">Nastavení maximálního počtu souběžných připojení v klientech WPF</span><span class="sxs-lookup"><span data-stu-id="1a141-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="1a141-180">V klientech WPF možná budete muset zvýšit maximální počet souběžných připojení od výchozí hodnoty 2.</span><span class="sxs-lookup"><span data-stu-id="1a141-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="1a141-181">Doporučená hodnota je 10.</span><span class="sxs-lookup"><span data-stu-id="1a141-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="1a141-182">Další informace najdete v tématu [Třída ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a141-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="1a141-183">Určení parametrů řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="1a141-183">How to specify query string parameters</span></span>

<span data-ttu-id="1a141-184">Pokud chcete při připojení klienta odesílat data na server, můžete do objektu připojení přidat parametry řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="1a141-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="1a141-185">Následující příklad ukazuje, jak nastavit parametr řetězce dotazu v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="1a141-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="1a141-186">Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="1a141-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="1a141-187">Určení způsobu přenosu</span><span class="sxs-lookup"><span data-stu-id="1a141-187">How to specify the transport method</span></span>

<span data-ttu-id="1a141-188">V rámci procesu připojování klient signalizace obvykle vyjednává se serverem, aby bylo možné určit nejlepší přenos, který je podporovaný oběma servery i klientem.</span><span class="sxs-lookup"><span data-stu-id="1a141-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="1a141-189">Pokud už víte, kterou přenos chcete použít, můžete tento proces vyjednávání obejít.</span><span class="sxs-lookup"><span data-stu-id="1a141-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="1a141-190">Chcete-li určit metodu transportu, předejte objekt přenosu do metody Start.</span><span class="sxs-lookup"><span data-stu-id="1a141-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="1a141-191">Následující příklad ukazuje, jak určit metodu přenosu v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="1a141-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="1a141-192">Obor názvů [Microsoft. ASPNET. Signal. Client. Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) obsahuje následující třídy, které lze použít k určení přenosu.</span><span class="sxs-lookup"><span data-stu-id="1a141-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="1a141-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="1a141-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="1a141-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="1a141-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="1a141-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (k dispozici pouze v případě, že server i klient používají .NET 4,5)</span><span class="sxs-lookup"><span data-stu-id="1a141-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="1a141-196">Automatický [přenos](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (automaticky zvolí nejlepší přenos, který je podporován klientem i serverem.</span><span class="sxs-lookup"><span data-stu-id="1a141-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="1a141-197">Toto je výchozí přenos.</span><span class="sxs-lookup"><span data-stu-id="1a141-197">This is the default transport.</span></span> <span data-ttu-id="1a141-198">Předání do metody `Start` má stejný účinek, jako by neprošlo cokoli.)</span><span class="sxs-lookup"><span data-stu-id="1a141-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="1a141-199">Přenos ForeverFrame není v tomto seznamu zahrnutý, protože ho používají jenom prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="1a141-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="1a141-200">Informace o tom, jak zjistit způsob přenosu v serverovém kódu, najdete v tématu [Průvodce rozhraním API centra ASP.NET Signal-Server – jak z kontextové vlastnosti získat informace o klientovi](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="1a141-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="1a141-201">Další informace o přenosech a náhradních přenosech najdete v tématu [Úvod k signalizaci a záložním přenosům](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="1a141-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="1a141-202">Určení hlaviček protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="1a141-202">How to specify HTTP headers</span></span>

<span data-ttu-id="1a141-203">K nastavení hlaviček protokolu HTTP použijte vlastnost `Headers` objektu Connection.</span><span class="sxs-lookup"><span data-stu-id="1a141-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="1a141-204">Následující příklad ukazuje, jak přidat hlavičku HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a141-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="1a141-205">Určení klientských certifikátů</span><span class="sxs-lookup"><span data-stu-id="1a141-205">How to specify client certificates</span></span>

<span data-ttu-id="1a141-206">Chcete-li přidat klientské certifikáty, použijte metodu `AddClientCertificate` objektu Connection.</span><span class="sxs-lookup"><span data-stu-id="1a141-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="1a141-207">Postup vytvoření centrálního proxy serveru</span><span class="sxs-lookup"><span data-stu-id="1a141-207">How to create the Hub proxy</span></span>

<span data-ttu-id="1a141-208">Chcete-li definovat metody v klientovi, které může centrum volat ze serveru, a vyvolat metody v centru na serveru, vytvořte proxy serveru pro centrum voláním `CreateHubProxy` na objektu Connection.</span><span class="sxs-lookup"><span data-stu-id="1a141-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="1a141-209">Řetězec, který předáte do `CreateHubProxy`, je název vaší třídy centra nebo název určený atributem `HubName`, pokud se na serveru použila jedna.</span><span class="sxs-lookup"><span data-stu-id="1a141-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="1a141-210">Shoda názvů nerozlišuje malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="1a141-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="1a141-211">**Třída centra na serveru**</span><span class="sxs-lookup"><span data-stu-id="1a141-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="1a141-212">**Vytvoření klientského proxy serveru pro třídu centra**</span><span class="sxs-lookup"><span data-stu-id="1a141-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="1a141-213">Pokud třídu centra seřadíte pomocí atributu `HubName`, použijte tento název.</span><span class="sxs-lookup"><span data-stu-id="1a141-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="1a141-214">**Třída centra na serveru**</span><span class="sxs-lookup"><span data-stu-id="1a141-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="1a141-215">**Vytvoření klientského proxy serveru pro třídu centra**</span><span class="sxs-lookup"><span data-stu-id="1a141-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="1a141-216">Pokud zavoláte `HubConnection.CreateHubProxy` vícekrát se stejným `hubName`, dostanete stejný objekt `IHubProxy` v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="1a141-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="1a141-217">Jak definovat metody v klientovi, které může server volat</span><span class="sxs-lookup"><span data-stu-id="1a141-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="1a141-218">Chcete-li definovat metodu, kterou může server volat, použijte metodu `On` proxy k registraci obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="1a141-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="1a141-219">Porovnávání názvů metod nerozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="1a141-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="1a141-220">Například `Clients.All.UpdateStockPrice` na serveru spustí `updateStockPrice`, `updatestockprice`nebo `UpdateStockPrice` na klientovi.</span><span class="sxs-lookup"><span data-stu-id="1a141-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="1a141-221">Různé klientské platformy mají různé požadavky na způsob psaní kódu metody pro aktualizaci uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="1a141-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="1a141-222">Uvedené příklady jsou pro klienty WinRT (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="1a141-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="1a141-223">Příklady WPF, Silverlight a konzolových aplikací jsou k dispozici v [samostatném oddílu dále v tomto tématu](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="1a141-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="1a141-224">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="1a141-224">Methods without parameters</span></span>

<span data-ttu-id="1a141-225">Pokud metoda, kterou právě zpracováváte, nemá parametry, použijte neobecné přetížení metody `On`:</span><span class="sxs-lookup"><span data-stu-id="1a141-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="1a141-226">**Serverový kód, který volá metodu klienta bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="1a141-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="1a141-227">**Klientský kód WinRT pro metodu volanou ze serveru bez parametrů ([viz příklady WPF a Silverlight dále v tomto tématu](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="1a141-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="1a141-228">Metody s parametry, které určují typy parametrů</span><span class="sxs-lookup"><span data-stu-id="1a141-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="1a141-229">Pokud má zpracovávaná metoda parametry, zadejte typy parametrů jako obecné typy metody `On`.</span><span class="sxs-lookup"><span data-stu-id="1a141-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="1a141-230">Existují obecná přetížení metody `On`, která vám umožní zadat až 8 parametrů (4 v Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="1a141-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="1a141-231">V následujícím příkladu je jeden parametr odeslán do metody `UpdateStockPrice`.</span><span class="sxs-lookup"><span data-stu-id="1a141-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="1a141-232">**Serverový kód, který volá metodu klienta s parametrem**</span><span class="sxs-lookup"><span data-stu-id="1a141-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="1a141-233">**Třída akcie použitá pro parametr**</span><span class="sxs-lookup"><span data-stu-id="1a141-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="1a141-234">**Klientský kód WinRT pro metodu volanou ze serveru s parametrem ([viz příklady WPF a Silverlight dále v tomto tématu](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="1a141-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="1a141-235">Metody s parametry, které určují dynamické objekty pro parametry</span><span class="sxs-lookup"><span data-stu-id="1a141-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="1a141-236">Jako alternativu k určení parametrů jako obecných typů `On` metody můžete zadat parametry jako dynamické objekty:</span><span class="sxs-lookup"><span data-stu-id="1a141-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="1a141-237">**Serverový kód, který volá metodu klienta s parametrem**</span><span class="sxs-lookup"><span data-stu-id="1a141-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="1a141-238">**Třída akcie použitá pro parametr**</span><span class="sxs-lookup"><span data-stu-id="1a141-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="1a141-239">**Klientský kód WinRT pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr ([viz příklady WPF a Silverlight dále v tomto tématu](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="1a141-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="1a141-240">Postup odebrání obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="1a141-240">How to remove a handler</span></span>

<span data-ttu-id="1a141-241">Chcete-li odebrat obslužnou rutinu, zavolejte metodu `Dispose`.</span><span class="sxs-lookup"><span data-stu-id="1a141-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="1a141-242">**Klientský kód pro metodu volanou ze serveru**</span><span class="sxs-lookup"><span data-stu-id="1a141-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="1a141-243">**Klientský kód pro odebrání obslužné rutiny**</span><span class="sxs-lookup"><span data-stu-id="1a141-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="1a141-244">Postup volání metod serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="1a141-244">How to call server methods from the client</span></span>

<span data-ttu-id="1a141-245">Chcete-li volat metodu na serveru, použijte metodu `Invoke` na serveru proxy centra.</span><span class="sxs-lookup"><span data-stu-id="1a141-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="1a141-246">Pokud metoda serveru nemá žádnou návratovou hodnotu, použijte neobecné přetížení metody `Invoke`.</span><span class="sxs-lookup"><span data-stu-id="1a141-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="1a141-247">**Serverový kód pro metodu, která nemá žádnou návratovou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="1a141-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="1a141-248">**Klientský kód volá metodu, která nemá žádnou návratovou hodnotu.**</span><span class="sxs-lookup"><span data-stu-id="1a141-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="1a141-249">Pokud má metoda serveru návratovou hodnotu, zadejte návratový typ jako obecný typ metody `Invoke`.</span><span class="sxs-lookup"><span data-stu-id="1a141-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="1a141-250">**Serverový kód pro metodu, která má návratovou hodnotu a má parametr komplexního typu**</span><span class="sxs-lookup"><span data-stu-id="1a141-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="1a141-251">**Třída akcie použitá pro parametr a návratovou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="1a141-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="1a141-252">**Klientský kód volá metodu, která má návratovou hodnotu a přebírá parametr komplexního typu v asynchronní metodě ASP.NET 4,5.**</span><span class="sxs-lookup"><span data-stu-id="1a141-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="1a141-253">**Klientský kód, který volá metodu, která má návratovou hodnotu a přebírá parametr komplexního typu, v synchronní metodě**</span><span class="sxs-lookup"><span data-stu-id="1a141-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="1a141-254">Metoda `Invoke` se spustí asynchronně a vrátí objekt `Task`.</span><span class="sxs-lookup"><span data-stu-id="1a141-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="1a141-255">Pokud nezadáte `await` nebo `.Wait()`, bude další řádek kódu proveden před tím, než byla vyvolaná metoda dokončena.</span><span class="sxs-lookup"><span data-stu-id="1a141-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="1a141-256">Postup zpracování událostí životního cyklu připojení</span><span class="sxs-lookup"><span data-stu-id="1a141-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="1a141-257">Signál poskytuje následující události doby života připojení, které můžete zpracovat:</span><span class="sxs-lookup"><span data-stu-id="1a141-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="1a141-258">`Received`: Vyvolá se, když jsou v připojení přijata nějaká data.</span><span class="sxs-lookup"><span data-stu-id="1a141-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="1a141-259">Poskytuje přijatá data.</span><span class="sxs-lookup"><span data-stu-id="1a141-259">Provides the received data.</span></span>
- <span data-ttu-id="1a141-260">`ConnectionSlow`: Vyvolá se, když klient zjistí pomalé nebo často vyřazování připojení.</span><span class="sxs-lookup"><span data-stu-id="1a141-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="1a141-261">`Reconnecting`: Vyvolá se, když se zahájí opětovné připojení podkladového přenosu.</span><span class="sxs-lookup"><span data-stu-id="1a141-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="1a141-262">`Reconnected`: Vyvolá se, když se znovu připojí příslušný přenos.</span><span class="sxs-lookup"><span data-stu-id="1a141-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="1a141-263">`StateChanged`: Vyvolá se při změně stavu připojení.</span><span class="sxs-lookup"><span data-stu-id="1a141-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="1a141-264">Poskytuje starý stav a nový stav.</span><span class="sxs-lookup"><span data-stu-id="1a141-264">Provides the old state and the new state.</span></span> <span data-ttu-id="1a141-265">Informace o hodnotách stavu připojení naleznete v tématu [vlastnost ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="1a141-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="1a141-266">`Closed`: Vyvolá se, když se připojení odpojilo.</span><span class="sxs-lookup"><span data-stu-id="1a141-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="1a141-267">Například pokud chcete zobrazovat upozornění na chyby, které nejsou závažné, ale způsobují přerušované problémy s připojením, například pomalé nebo časté připojení, zpracujte událost `ConnectionSlow`.</span><span class="sxs-lookup"><span data-stu-id="1a141-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="1a141-268">Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení v nástroji Signal](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="1a141-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="1a141-269">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="1a141-269">How to handle errors</span></span>

<span data-ttu-id="1a141-270">Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který Signal vrátí po chybě, obsahuje minimální informace o chybě.</span><span class="sxs-lookup"><span data-stu-id="1a141-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="1a141-271">Například pokud se volání `newContosoChatMessage` nepovede, chybová zpráva v objektu Error obsahuje "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" odesílání podrobných chybových zpráv klientům v produkčním prostředí se z bezpečnostních důvodů nedoporučuje, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.</span><span class="sxs-lookup"><span data-stu-id="1a141-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="1a141-272">Chcete-li zpracovat chyby, které signalizace vyvolá, můžete přidat obslužnou rutinu pro událost `Error` objektu Connection.</span><span class="sxs-lookup"><span data-stu-id="1a141-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="1a141-273">Chcete-li zpracovat chyby z vyvolání metod, zabalte kód do bloku try-catch.</span><span class="sxs-lookup"><span data-stu-id="1a141-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="1a141-274">Postup povolení protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="1a141-274">How to enable client-side logging</span></span>

<span data-ttu-id="1a141-275">Pokud chcete povolit protokolování na straně klienta, nastavte `TraceLevel` a vlastnosti `TraceWriter` objektu připojení.</span><span class="sxs-lookup"><span data-stu-id="1a141-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="1a141-276">Ukázky kódu aplikace WPF, Silverlight a konzolových aplikací pro metody klienta, které může server volat</span><span class="sxs-lookup"><span data-stu-id="1a141-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="1a141-277">Ukázky kódu uvedené dříve pro definování metod klienta, které může server volat, se vztahují na klienty WinRT.</span><span class="sxs-lookup"><span data-stu-id="1a141-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="1a141-278">Následující ukázky znázorňují ekvivalentní kód pro klienty WPF, Silverlight a konzolových aplikací.</span><span class="sxs-lookup"><span data-stu-id="1a141-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="1a141-279">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="1a141-279">Methods without parameters</span></span>

<span data-ttu-id="1a141-280">**Kód klienta WPF pro metodu volanou ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="1a141-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="1a141-281">**Kód klienta Silverlight pro metodu volanou ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="1a141-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="1a141-282">**Klientský kód konzolové aplikace pro metodu volanou ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="1a141-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="1a141-283">Metody s parametry, které určují typy parametrů</span><span class="sxs-lookup"><span data-stu-id="1a141-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="1a141-284">**Kód klienta WPF pro metodu volanou ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="1a141-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="1a141-285">**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="1a141-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="1a141-286">**Klientský kód konzolové aplikace pro metodu volanou ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="1a141-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="1a141-287">Metody s parametry, které určují dynamické objekty pro parametry</span><span class="sxs-lookup"><span data-stu-id="1a141-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="1a141-288">**Kód klienta WPF pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="1a141-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="1a141-289">**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="1a141-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="1a141-290">**Klientský kód konzolové aplikace pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="1a141-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
