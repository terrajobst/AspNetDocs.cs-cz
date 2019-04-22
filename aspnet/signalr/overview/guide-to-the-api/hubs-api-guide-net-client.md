---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: Funkce SignalR technologie ASP.NET pokyny k rozhraní API Center – klient .NET (C#) | Dokumentace Microsoftu
author: bradygaster
description: Tento dokument obsahuje úvod k používání rozhraní API rozbočovače pro funkci SignalR verze 2 v rozhraní .NET klientů, jako jsou Windows Store (WinRT), WPF, Silverlight a nevýhody...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 473c8dd14d639fb9f4ff9e11a4c3ffa2b1a3a81e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59396028"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="d5e24-103">Funkce SignalR technologie ASP.NET pokyny k rozhraní API Center – klient .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="d5e24-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>


[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d5e24-104">Tento dokument obsahuje úvod k používání rozhraní API rozbočovače pro funkci SignalR verze 2 v rozhraní .NET klientů, jako jsou Windows Store (WinRT), WPF, Silverlight a konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="d5e24-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="d5e24-105">Rozhraní API pro rozbočovače SignalR umožňuje vytvářet vzdálených volání procedur (RPC) ze serveru pro připojené klienty a z klientů k serveru.</span><span class="sxs-lookup"><span data-stu-id="d5e24-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="d5e24-106">V serverovém kódu můžete definovat metody, které mohou být volány klientů a volat metody, které běží na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d5e24-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="d5e24-107">V klientském kódu můžete definovat metody, které lze volat ze serveru a volání metody, které běží na serveru.</span><span class="sxs-lookup"><span data-stu-id="d5e24-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="d5e24-108">Funkce SignalR postará za vás zajistí funkčnost systému klient server.</span><span class="sxs-lookup"><span data-stu-id="d5e24-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="d5e24-109">Funkce SignalR také nabízí nižší úrovně rozhraní API volá trvalé připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="d5e24-110">Úvod do SignalR, rozbočovačů a trvalá připojení, nebo kurz, který ukazuje, jak sestavit kompletní aplikace SignalR, přečtěte si téma [SignalR – Začínáme](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="d5e24-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d5e24-111">Verze softwaru použitým v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="d5e24-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="d5e24-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d5e24-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="d5e24-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d5e24-113">.NET 4.5</span></span>
> - <span data-ttu-id="d5e24-114">Funkce SignalR verze 2</span><span class="sxs-lookup"><span data-stu-id="d5e24-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="d5e24-115">Předchozích verzích tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="d5e24-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="d5e24-116">Informace o předchozích verzích systému SignalR naleznete v tématu [starší verze funkce SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="d5e24-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="d5e24-117">Otázky a komentáře</span><span class="sxs-lookup"><span data-stu-id="d5e24-117">Questions and comments</span></span>
>
> <span data-ttu-id="d5e24-118">Napište prosím zpětnou vazbu o tom, jak vám líbilo v tomto kurzu a co můžeme zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="d5e24-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d5e24-119">Pokud máte nějaké otázky, které přímo nesouvisejí, najdete v tomto kurzu, můžete je publikovat [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="d5e24-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="d5e24-120">Přehled</span><span class="sxs-lookup"><span data-stu-id="d5e24-120">Overview</span></span>

<span data-ttu-id="d5e24-121">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="d5e24-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="d5e24-122">Instalace klienta</span><span class="sxs-lookup"><span data-stu-id="d5e24-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="d5e24-123">Postup vytvoření připojení</span><span class="sxs-lookup"><span data-stu-id="d5e24-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="d5e24-124">Připojení mezi doménami z klienty prostředí Silverlight</span><span class="sxs-lookup"><span data-stu-id="d5e24-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="d5e24-125">Postup konfigurace připojení</span><span class="sxs-lookup"><span data-stu-id="d5e24-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="d5e24-126">Jak nastavit maximální počet souběžných připojení v klientech WPF</span><span class="sxs-lookup"><span data-stu-id="d5e24-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="d5e24-127">Určení parametrů řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="d5e24-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="d5e24-128">Jak určit metodu přenosu</span><span class="sxs-lookup"><span data-stu-id="d5e24-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="d5e24-129">Jak zadat hlavičky protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="d5e24-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="d5e24-130">Určení klientských certifikátů</span><span class="sxs-lookup"><span data-stu-id="d5e24-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="d5e24-131">Jak vytvořit proxy server rozbočovače</span><span class="sxs-lookup"><span data-stu-id="d5e24-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="d5e24-132">Definování metody na straně klienta, která může volat na serveru</span><span class="sxs-lookup"><span data-stu-id="d5e24-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="d5e24-133">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="d5e24-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="d5e24-134">Metody s parametry, určující typy parametrů</span><span class="sxs-lookup"><span data-stu-id="d5e24-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="d5e24-135">Metody s parametry, dynamických objektů pro parametry</span><span class="sxs-lookup"><span data-stu-id="d5e24-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="d5e24-136">Jak odebrat obslužnou rutinu</span><span class="sxs-lookup"><span data-stu-id="d5e24-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="d5e24-137">Volání metody serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="d5e24-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="d5e24-138">Zpracování událostí doby platnosti</span><span class="sxs-lookup"><span data-stu-id="d5e24-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="d5e24-139">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="d5e24-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="d5e24-140">Jak povolit protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="d5e24-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="d5e24-141">WPF, Silverlight a Konzolová aplikace ukázky kódu pro metody klienta, které můžete volat na serveru</span><span class="sxs-lookup"><span data-stu-id="d5e24-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="d5e24-142">Ukázka .NET klientské projekty naleznete v následujících zdrojích:</span><span class="sxs-lookup"><span data-stu-id="d5e24-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="d5e24-143">[gustavo armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) na webu GitHub.com (příklady WinRT, Silverlight, konzoly aplikace).</span><span class="sxs-lookup"><span data-stu-id="d5e24-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="d5e24-144">[DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) na webu GitHub.com (např. WPF).</span><span class="sxs-lookup"><span data-stu-id="d5e24-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="d5e24-145">[Funkce SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) na webu GitHub.com (např. aplikace konzoly).</span><span class="sxs-lookup"><span data-stu-id="d5e24-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="d5e24-146">Dokumentace o tom, jak program na serveru nebo klientů JavaScript naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="d5e24-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="d5e24-147">Pokyny k rozhraní API Center SignalR – Server</span><span class="sxs-lookup"><span data-stu-id="d5e24-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="d5e24-148">Pokyny k rozhraní API Center SignalR – javascriptový klient</span><span class="sxs-lookup"><span data-stu-id="d5e24-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="d5e24-149">Odkazy na témata, Reference k rozhraní API se API verze rozhraní .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d5e24-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="d5e24-150">Pokud používáte .NET 4, přečtěte si téma [verze .NET 4 témat API](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="d5e24-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="d5e24-151">Instalace klienta</span><span class="sxs-lookup"><span data-stu-id="d5e24-151">Client setup</span></span>

<span data-ttu-id="d5e24-152">Nainstalujte [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) balíčku NuGet (ne [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) balíček).</span><span class="sxs-lookup"><span data-stu-id="d5e24-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="d5e24-153">Tento balíček podporuje WinRT, Silverlight, WPF, konzolovou aplikaci a klienti Windows Phone, .NET 4 a .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d5e24-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="d5e24-154">Pokud verze funkce signalr, která máte na straně klienta se liší od verze, které máte na serveru, SignalR často je možné přizpůsobit pro rozdíl.</span><span class="sxs-lookup"><span data-stu-id="d5e24-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="d5e24-155">Například server se systémem SignalR verze 2 bude podporovat klienty, kteří mají nainstalované 1.1.x, stejně jako klienti, kteří mají verzi 2 nainstalované.</span><span class="sxs-lookup"><span data-stu-id="d5e24-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="d5e24-156">Pokud je příliš velký rozdíl mezi verzí na serveru a verze na klientovi, nebo pokud klient je novější než server, vyvolá funkce SignalR `InvalidOperationException` výjimky, když se klient pokusí navázat připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="d5e24-157">Chybová zpráva "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span><span class="sxs-lookup"><span data-stu-id="d5e24-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="d5e24-158">Postup vytvoření připojení</span><span class="sxs-lookup"><span data-stu-id="d5e24-158">How to establish a connection</span></span>

<span data-ttu-id="d5e24-159">Předtím, než můžete navázat spojení, je nutné vytvořit `HubConnection` objektů a vytvořit proxy.</span><span class="sxs-lookup"><span data-stu-id="d5e24-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="d5e24-160">K navázání připojení, zavolejte `Start` metodu `HubConnection` objektu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="d5e24-161">Pro klienty jazyka JavaScript, je nutné provést registraci aspoň jednu obslužnou rutinu události před voláním `Start` metoda k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="d5e24-162">To není nutné pro klienty .NET.</span><span class="sxs-lookup"><span data-stu-id="d5e24-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="d5e24-163">Pro klienty jazyka JavaScript, vygenerovaném kódu proxy automaticky vytvoří proxy pro všechna centra, které existují na serveru a registraci obslužné rutiny je způsob, jak naznačit které rozbočovače klienta chce využít.</span><span class="sxs-lookup"><span data-stu-id="d5e24-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="d5e24-164">Ale pro klienta .NET vytvořit proxy servery Hub ručně, tak SignalR předpokládá, že budete používat libovolné centrum, kterou vytvoříte pro proxy server.</span><span class="sxs-lookup"><span data-stu-id="d5e24-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="d5e24-165">Vzorový kód používá výchozí "/ signalr" adresa URL k připojení do služby SignalR.</span><span class="sxs-lookup"><span data-stu-id="d5e24-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="d5e24-166">Informace o tom, jak určit různé základní adresu URL najdete v tématu [ASP.NET pokyny k rozhraní API Center SignalR - Server - /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="d5e24-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="d5e24-167">`Start` Metoda provedena asynchronně.</span><span class="sxs-lookup"><span data-stu-id="d5e24-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="d5e24-168">Ujistěte se, že následující řádky kódu není můžete spustit až po vytvoření připojení, použijte `await` v technologii ASP.NET 4.5 asynchronní metodu nebo `.Wait()` v synchronní metodě.</span><span class="sxs-lookup"><span data-stu-id="d5e24-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="d5e24-169">Nepoužívejte `.Wait()` v klientovi WinRT.</span><span class="sxs-lookup"><span data-stu-id="d5e24-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="d5e24-170">Připojení mezi doménami z klienty prostředí Silverlight</span><span class="sxs-lookup"><span data-stu-id="d5e24-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="d5e24-171">Informace o tom, jak povolit připojení mezi doménami z klienty prostředí Silverlight naleznete v tématu [zpřístupnění služby k dispozici napříč hranicemi domén](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="d5e24-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="d5e24-172">Postup konfigurace připojení</span><span class="sxs-lookup"><span data-stu-id="d5e24-172">How to configure the connection</span></span>

<span data-ttu-id="d5e24-173">Než vytvoříte připojení, můžete určit kterékoli z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="d5e24-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="d5e24-174">Limit souběžných připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="d5e24-175">Parametry řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-175">Query string parameters.</span></span>
- <span data-ttu-id="d5e24-176">Metoda přenosu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-176">The transport method.</span></span>
- <span data-ttu-id="d5e24-177">Hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="d5e24-177">HTTP headers.</span></span>
- <span data-ttu-id="d5e24-178">Klientské certifikáty.</span><span class="sxs-lookup"><span data-stu-id="d5e24-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="d5e24-179">Jak nastavit maximální počet souběžných připojení v klientech WPF</span><span class="sxs-lookup"><span data-stu-id="d5e24-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="d5e24-180">V WPF klienty bude pravděpodobně zvýšit maximální počet souběžných připojení z jeho výchozí hodnotu 2.</span><span class="sxs-lookup"><span data-stu-id="d5e24-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="d5e24-181">Doporučená hodnota je 10.</span><span class="sxs-lookup"><span data-stu-id="d5e24-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="d5e24-182">Další informace najdete v tématu [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5e24-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="d5e24-183">Určení parametrů řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="d5e24-183">How to specify query string parameters</span></span>

<span data-ttu-id="d5e24-184">Pokud chcete odesílat data do serveru, když se klient připojí, můžete přidat parametry řetězce dotazu do objekt připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="d5e24-185">Následující příklad ukazuje, jak nastavit parametr řetězce dotazu v klientském kódu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="d5e24-186">Následující příklad znázorňuje způsob čtení parametru řetězce dotazu v serverovém kódu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="d5e24-187">Jak určit metodu přenosu</span><span class="sxs-lookup"><span data-stu-id="d5e24-187">How to specify the transport method</span></span>

<span data-ttu-id="d5e24-188">Jako součást procesu připojování klienta SignalR obvykle vyjedná se serverem a určit nejlepší přenos, který je podporovaný server i klient.</span><span class="sxs-lookup"><span data-stu-id="d5e24-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="d5e24-189">Pokud již víte, jaké přenosu, kterou chcete použít, můžete obejít tento proces vyjednávání.</span><span class="sxs-lookup"><span data-stu-id="d5e24-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="d5e24-190">K určení metodu přenosu, předejte objekt transport metodě Start.</span><span class="sxs-lookup"><span data-stu-id="d5e24-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="d5e24-191">Následující příklad ukazuje, jak zadat metodu přenosu v klientském kódu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="d5e24-192">[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) obor názvů obsahuje následující třídy, které můžete použít k určení přenos.</span><span class="sxs-lookup"><span data-stu-id="d5e24-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="d5e24-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="d5e24-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="d5e24-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="d5e24-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="d5e24-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (dostupné pouze v případě serverů i klientů pomocí rozhraní .NET 4.5.)</span><span class="sxs-lookup"><span data-stu-id="d5e24-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="d5e24-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (automaticky vybere nejlepší přenos, který podporuje klient i server.</span><span class="sxs-lookup"><span data-stu-id="d5e24-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="d5e24-197">Toto je výchozí přenos.</span><span class="sxs-lookup"><span data-stu-id="d5e24-197">This is the default transport.</span></span> <span data-ttu-id="d5e24-198">Tuto hodnotu na předání `Start` metoda má stejný účinek jako ne vyhovující co.)</span><span class="sxs-lookup"><span data-stu-id="d5e24-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="d5e24-199">Přenos ForeverFrame není zahrnuta v tomto seznamu, protože se používá pouze pomocí prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="d5e24-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="d5e24-200">Informace o tom, jak zkontrolovat metodu přenosu v serverovém kódu najdete v tématu [ASP.NET pokyny k rozhraní API Center SignalR - Server - jak získat informace o klientovi z kontextové vlastnosti](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="d5e24-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="d5e24-201">Další informace o přenosy a náhrad najdete v tématu [Úvod ke knihovně SignalR – přenosy a náhrad](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="d5e24-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="d5e24-202">Jak zadat hlavičky protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="d5e24-202">How to specify HTTP headers</span></span>

<span data-ttu-id="d5e24-203">K nastavení hlavičky protokolu HTTP, použijte `Headers` vlastnost na objekt připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="d5e24-204">Následující příklad ukazuje, jak přidat hlavičku protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="d5e24-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="d5e24-205">Určení klientských certifikátů</span><span class="sxs-lookup"><span data-stu-id="d5e24-205">How to specify client certificates</span></span>

<span data-ttu-id="d5e24-206">Chcete-li přidat klientské certifikáty, použijte `AddClientCertificate` metodu na objekt připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="d5e24-207">Jak vytvořit proxy server rozbočovače</span><span class="sxs-lookup"><span data-stu-id="d5e24-207">How to create the Hub proxy</span></span>

<span data-ttu-id="d5e24-208">Aby bylo možné definovat metody na straně klienta, která centrum může volat ze serveru a volání metod rozbočovače na serveru, vytvořit proxy server rozbočovače voláním `CreateHubProxy` na objekt připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="d5e24-209">Řetězec předáním `CreateHubProxy` je název třídy rozbočovače nebo název určený `HubName` atribut, pokud bylo použito na serveru.</span><span class="sxs-lookup"><span data-stu-id="d5e24-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="d5e24-210">Shoda názvů nerozlišuje.</span><span class="sxs-lookup"><span data-stu-id="d5e24-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="d5e24-211">**Třída rozbočovače na serveru**</span><span class="sxs-lookup"><span data-stu-id="d5e24-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="d5e24-212">**Vytvořit proxy klienta pro rozbočovač třídu**</span><span class="sxs-lookup"><span data-stu-id="d5e24-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="d5e24-213">Pokud uspořádání vaší třídy centra s `HubName` atribut, použijte tento název.</span><span class="sxs-lookup"><span data-stu-id="d5e24-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="d5e24-214">**Třída rozbočovače na serveru**</span><span class="sxs-lookup"><span data-stu-id="d5e24-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="d5e24-215">**Vytvořit proxy klienta pro rozbočovač třídu**</span><span class="sxs-lookup"><span data-stu-id="d5e24-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="d5e24-216">Při volání `HubConnection.CreateHubProxy` víckrát se stejným `hubName`, získáte stejné mezipaměti `IHubProxy` objektu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="d5e24-217">Definování metody na straně klienta, která může volat na serveru</span><span class="sxs-lookup"><span data-stu-id="d5e24-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="d5e24-218">Chcete-li definovat metodu, která může volat na serveru, používat proxy server, na `On` metody pro registraci obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="d5e24-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="d5e24-219">Shoda názvu metody je velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="d5e24-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="d5e24-220">Například `Clients.All.UpdateStockPrice` na serveru spustí `updateStockPrice`, `updatestockprice`, nebo `UpdateStockPrice` na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d5e24-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="d5e24-221">Různé klientské platformy mají různé požadavky na jak psát kód, metoda pro aktualizaci uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="d5e24-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="d5e24-222">Příklady uvedené jsou pro klienty WinRT (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="d5e24-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="d5e24-223">WPF, Silverlight a příklady aplikací konzoly jsou k dispozici v [samostatné části dále v tomto tématu](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="d5e24-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="d5e24-224">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="d5e24-224">Methods without parameters</span></span>

<span data-ttu-id="d5e24-225">Pokud metoda, že zpracování nemá žádné parametry, použijte přetížení obecné `On` metody:</span><span class="sxs-lookup"><span data-stu-id="d5e24-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="d5e24-226">**Volání metody bez parametrů kódu serveru**</span><span class="sxs-lookup"><span data-stu-id="d5e24-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="d5e24-227">**WinRT klientský kód pro metodu volat ze serveru bez parametrů ([WPF a Silverlight příklady dále v tomto tématu](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="d5e24-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="d5e24-228">Metody s parametry, určující typy parametrů</span><span class="sxs-lookup"><span data-stu-id="d5e24-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="d5e24-229">Pokud jste zpracování metody obsahuje parametry, zadejte typy parametrů jako obecné typy `On` metody.</span><span class="sxs-lookup"><span data-stu-id="d5e24-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="d5e24-230">Existují přetížení obecné `On` metoda vám umožní určit až na 8 parametry (4 ve Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="d5e24-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="d5e24-231">V následujícím příkladu je jeden parametr odeslán `UpdateStockPrice` metody.</span><span class="sxs-lookup"><span data-stu-id="d5e24-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="d5e24-232">**Volání metody s parametrem kódu serveru**</span><span class="sxs-lookup"><span data-stu-id="d5e24-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="d5e24-233">**Třída akcie použitý pro parametr**</span><span class="sxs-lookup"><span data-stu-id="d5e24-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="d5e24-234">**WinRT klientský kód pro metodu volat ze serveru s parametrem ([WPF a Silverlight příklady dále v tomto tématu](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="d5e24-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="d5e24-235">Metody s parametry, dynamických objektů pro parametry</span><span class="sxs-lookup"><span data-stu-id="d5e24-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="d5e24-236">Jako alternativu k zadání parametrů jako obecné typy `On` metodu, můžete zadat parametry jako dynamické objekty:</span><span class="sxs-lookup"><span data-stu-id="d5e24-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="d5e24-237">**Volání metody s parametrem kódu serveru**</span><span class="sxs-lookup"><span data-stu-id="d5e24-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="d5e24-238">**Třída akcie použitý pro parametr**</span><span class="sxs-lookup"><span data-stu-id="d5e24-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="d5e24-239">**WinRT klientský kód pro metodu volat ze serveru s parametrem, pomocí dynamického objektu pro parametr ([WPF a Silverlight příklady dále v tomto tématu](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="d5e24-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="d5e24-240">Jak odebrat obslužnou rutinu</span><span class="sxs-lookup"><span data-stu-id="d5e24-240">How to remove a handler</span></span>

<span data-ttu-id="d5e24-241">Chcete-li odebrat obslužnou rutinu, zavolejte jeho `Dispose` metoda.</span><span class="sxs-lookup"><span data-stu-id="d5e24-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="d5e24-242">**Klientský kód pro metodu volat ze serveru**</span><span class="sxs-lookup"><span data-stu-id="d5e24-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="d5e24-243">**Klientský kód odebrat obslužnou rutinu**</span><span class="sxs-lookup"><span data-stu-id="d5e24-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="d5e24-244">Volání metody serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="d5e24-244">How to call server methods from the client</span></span>

<span data-ttu-id="d5e24-245">Chcete-li volat metodu na serveru, použijte `Invoke` metodu na proxy server rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="d5e24-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="d5e24-246">Pokud metoda server nemá žádnou návratovou hodnotu, použijte přetížení obecné `Invoke` metody.</span><span class="sxs-lookup"><span data-stu-id="d5e24-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="d5e24-247">**Serverový kód pro metodu, která nemá žádnou návratovou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="d5e24-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="d5e24-248">**Klientský kód volá metodu, která nemá žádnou návratovou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="d5e24-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="d5e24-249">Pokud metoda serveru má návratovou hodnotu, určit návratový typ jako generický typ `Invoke` metody.</span><span class="sxs-lookup"><span data-stu-id="d5e24-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="d5e24-250">**Serverový kód pro metodu, nemá návratovou hodnotu, která přebírá parametr komplexního typu**</span><span class="sxs-lookup"><span data-stu-id="d5e24-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="d5e24-251">**Třída akcie použitý pro parametr a vrátí hodnotu**</span><span class="sxs-lookup"><span data-stu-id="d5e24-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="d5e24-252">**Klientský kód volá metodu, nemá návratovou hodnotu, která přebírá parametr komplexního typu, v asynchronní metodě technologie ASP.NET 4.5**</span><span class="sxs-lookup"><span data-stu-id="d5e24-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="d5e24-253">**Klientský kód volá metodu, nemá návratovou hodnotu, která přebírá parametr komplexního typu, v synchronní metodě**</span><span class="sxs-lookup"><span data-stu-id="d5e24-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="d5e24-254">`Invoke` Metoda asynchronně provede a vrátí `Task` objektu.</span><span class="sxs-lookup"><span data-stu-id="d5e24-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="d5e24-255">Pokud nezadáte `await` nebo `.Wait()`, dalším řádku kódu se provedou předtím, než metody, která je zapotřebí vyvolat neskončí.</span><span class="sxs-lookup"><span data-stu-id="d5e24-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="d5e24-256">Zpracování událostí doby platnosti</span><span class="sxs-lookup"><span data-stu-id="d5e24-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="d5e24-257">Funkce SignalR poskytuje následující připojení události doby života, které dokáže zpracovat:</span><span class="sxs-lookup"><span data-stu-id="d5e24-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="d5e24-258">`Received`: Vyvoláno, když je veškerá data přijatá v připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="d5e24-259">Poskytuje přijatá data.</span><span class="sxs-lookup"><span data-stu-id="d5e24-259">Provides the received data.</span></span>
- <span data-ttu-id="d5e24-260">`ConnectionSlow`: Vyvoláno, když klient zjistí pomalý nebo často vyřazení připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="d5e24-261">`Reconnecting`: Vyvolá se při přenosu začne znovu obnovovat.</span><span class="sxs-lookup"><span data-stu-id="d5e24-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="d5e24-262">`Reconnected`: Vyvolá se při přenosu má připojen.</span><span class="sxs-lookup"><span data-stu-id="d5e24-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="d5e24-263">`StateChanged`: Vyvolá se při změně stavu připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="d5e24-264">Poskytuje stav starý a nový stav.</span><span class="sxs-lookup"><span data-stu-id="d5e24-264">Provides the old state and the new state.</span></span> <span data-ttu-id="d5e24-265">Informace o připojení najdete v části hodnoty stavu [ConnectionState výčet](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="d5e24-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="d5e24-266">`Closed`: Vyvolá se při připojení se odpojil.</span><span class="sxs-lookup"><span data-stu-id="d5e24-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="d5e24-267">Například pokud chcete zobrazit varovné zprávy o chybách, které nejsou závažné, ale způsobit problémy s přerušovaným připojením, například jako pomalost nebo častému odstranění připojení, zpracování `ConnectionSlow` událostí.</span><span class="sxs-lookup"><span data-stu-id="d5e24-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="d5e24-268">Další informace najdete v tématu [principy a zpracování událostí doby platnosti v knihovně SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="d5e24-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="d5e24-269">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="d5e24-269">How to handle errors</span></span>

<span data-ttu-id="d5e24-270">Pokud není explicitně povolit podrobné chybové zprávy na serveru, obsahuje objekt výjimky, která vrací SignalR po chybě minimální informace o této chybě.</span><span class="sxs-lookup"><span data-stu-id="d5e24-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="d5e24-271">Například, pokud je volání `newContosoChatMessage` selže, chybová zpráva v objektu chyba obsahuje "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" podrobné chybové zprávy pro klienty v produkčním prostředí se nedoporučuje z bezpečnostních důvodů, ale pokud chcete povolit podrobné chybové zprávy pro odesílání na serveru pro účely odstraňování potíží, použijte následující kód.</span><span class="sxs-lookup"><span data-stu-id="d5e24-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="d5e24-272">Zpracování chyb, které vyvolává SignalR, můžete přidat obslužnou rutinu pro `Error` události u objektu připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="d5e24-273">Zpracování chyb z volání metod, zabalte kód v bloku try-catch.</span><span class="sxs-lookup"><span data-stu-id="d5e24-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="d5e24-274">Jak povolit protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="d5e24-274">How to enable client-side logging</span></span>

<span data-ttu-id="d5e24-275">Chcete-li povolit protokolování na straně klienta, nastavte `TraceLevel` a `TraceWriter` vlastnosti objektu připojení.</span><span class="sxs-lookup"><span data-stu-id="d5e24-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="d5e24-276">WPF, Silverlight a Konzolová aplikace ukázky kódu pro metody klienta, které můžete volat na serveru</span><span class="sxs-lookup"><span data-stu-id="d5e24-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="d5e24-277">Ukázky kódu je uvedeno výše pro definování metody klienta, které můžete volat serveru platí pro klienty WinRT.</span><span class="sxs-lookup"><span data-stu-id="d5e24-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="d5e24-278">Následující ukázky ukazují ekvivalentní kód pro WPF, Silverlight a klienty aplikace konzoly.</span><span class="sxs-lookup"><span data-stu-id="d5e24-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="d5e24-279">Metody bez parametrů</span><span class="sxs-lookup"><span data-stu-id="d5e24-279">Methods without parameters</span></span>

<span data-ttu-id="d5e24-280">**WPF klientský kód pro metodu s názvem ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="d5e24-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="d5e24-281">**Kód klienta programu Silverlight pro metodu s názvem ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="d5e24-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="d5e24-282">**Konzole application klientský kód pro metodu s názvem ze serveru bez parametrů**</span><span class="sxs-lookup"><span data-stu-id="d5e24-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="d5e24-283">Metody s parametry, určující typy parametrů</span><span class="sxs-lookup"><span data-stu-id="d5e24-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="d5e24-284">**WPF klientský kód pro metodu volat ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="d5e24-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="d5e24-285">**Kód klienta programu Silverlight pro metodu volat ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="d5e24-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="d5e24-286">**Kód klienta konzolové aplikace pro metodu volat ze serveru s parametrem**</span><span class="sxs-lookup"><span data-stu-id="d5e24-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="d5e24-287">Metody s parametry, dynamických objektů pro parametry</span><span class="sxs-lookup"><span data-stu-id="d5e24-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="d5e24-288">**WPF klientský kód pro metodu volat ze serveru s parametrem, pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="d5e24-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="d5e24-289">**Kód klienta programu Silverlight pro metodu volat ze serveru s parametrem, pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="d5e24-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="d5e24-290">**Kód klienta konzolové aplikace pro metodu volat ze serveru s parametrem, pomocí dynamického objektu pro parametr**</span><span class="sxs-lookup"><span data-stu-id="d5e24-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
