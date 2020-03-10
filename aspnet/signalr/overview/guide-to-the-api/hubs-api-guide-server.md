---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: Průvodce rozhraním API pro centra ASP.NET Signal-C#Server () | Microsoft Docs
author: bradygaster
description: Tento dokument popisuje, jak programovat serverovou stranu rozhraní API centra ASP.NET pro Signal verze 2 s ukázkami kódu, které demonstrují...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536748"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="01a7e-103">Průvodce rozhraním API pro centra ASP.NET Signal-C#Server ()</span><span class="sxs-lookup"><span data-stu-id="01a7e-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="01a7e-104">autorem [Fletcher](https://github.com/pfletcher), který [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="01a7e-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="01a7e-105">Tento dokument popisuje, jak programovat serverovou stranu rozhraní API centra ASP.NET pro Signal verze 2 s ukázkami kódu, které demonstrují běžné možnosti.</span><span class="sxs-lookup"><span data-stu-id="01a7e-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="01a7e-106">Rozhraní API pro centra signalizace vám umožní provádět Vzdálená volání procedur (RPC) ze serveru pro připojené klienty a klienty na server.</span><span class="sxs-lookup"><span data-stu-id="01a7e-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="01a7e-107">V kódu serveru můžete definovat metody, které mohou být volány klienty, a volat metody, které jsou spouštěny v klientovi.</span><span class="sxs-lookup"><span data-stu-id="01a7e-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="01a7e-108">V kódu klienta definujete metody, které mohou být volány ze serveru, a voláte metody, které jsou spuštěny na serveru.</span><span class="sxs-lookup"><span data-stu-id="01a7e-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="01a7e-109">Signalizace postará o všechny instalace klienta na server za vás.</span><span class="sxs-lookup"><span data-stu-id="01a7e-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="01a7e-110">Nástroj Signal také nabízí nižší úroveň rozhraní API označované jako trvalá připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="01a7e-111">Úvod do nástroje pro signalizaci, centra a trvalá připojení najdete v tématu [Úvod do nástroje Signal 2](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="01a7e-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="01a7e-112">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="01a7e-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="01a7e-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="01a7e-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="01a7e-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="01a7e-114">.NET 4.5</span></span>
> - <span data-ttu-id="01a7e-115">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="01a7e-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="01a7e-116">Verze tématu</span><span class="sxs-lookup"><span data-stu-id="01a7e-116">Topic versions</span></span>
> 
> <span data-ttu-id="01a7e-117">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="01a7e-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="01a7e-118">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="01a7e-118">Questions and comments</span></span>
> 
> <span data-ttu-id="01a7e-119">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="01a7e-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="01a7e-120">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="01a7e-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="01a7e-121">Přehled</span><span class="sxs-lookup"><span data-stu-id="01a7e-121">Overview</span></span>

<span data-ttu-id="01a7e-122">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="01a7e-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="01a7e-123">Registrace middlewaru signálu</span><span class="sxs-lookup"><span data-stu-id="01a7e-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="01a7e-124">Adresa URL/SignalR</span><span class="sxs-lookup"><span data-stu-id="01a7e-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="01a7e-125">Konfigurace možností signalizace</span><span class="sxs-lookup"><span data-stu-id="01a7e-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="01a7e-126">Jak vytvořit a používat třídy centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="01a7e-127">Doba života objektu centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="01a7e-128">Ve stylu CamelCase – velká a malá písmena názvů hub v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="01a7e-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="01a7e-129">Více Center</span><span class="sxs-lookup"><span data-stu-id="01a7e-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="01a7e-130">Rozbočovače silného typu</span><span class="sxs-lookup"><span data-stu-id="01a7e-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="01a7e-131">Jak definovat metody ve třídě centra, které můžou klienti volat</span><span class="sxs-lookup"><span data-stu-id="01a7e-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="01a7e-132">Ve stylu CamelCase – velká a malá písmena názvů metod v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="01a7e-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="01a7e-133">Kdy spustit asynchronně</span><span class="sxs-lookup"><span data-stu-id="01a7e-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="01a7e-134">Definování přetížení</span><span class="sxs-lookup"><span data-stu-id="01a7e-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="01a7e-135">Vytváření sestav o průběhu z volání metod centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="01a7e-136">Volání metod klienta z třídy hub</span><span class="sxs-lookup"><span data-stu-id="01a7e-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="01a7e-137">Výběr klientů, kteří budou přijímat RPC</span><span class="sxs-lookup"><span data-stu-id="01a7e-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="01a7e-138">Žádné ověřování v době kompilace pro názvy metod</span><span class="sxs-lookup"><span data-stu-id="01a7e-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="01a7e-139">Porovnávání názvů metod bez rozlišení velkých a malých písmen</span><span class="sxs-lookup"><span data-stu-id="01a7e-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="01a7e-140">Asynchronní spuštění</span><span class="sxs-lookup"><span data-stu-id="01a7e-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="01a7e-141">Správa členství ve skupinách z třídy hub</span><span class="sxs-lookup"><span data-stu-id="01a7e-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="01a7e-142">Asynchronní provádění metod Add a Remove</span><span class="sxs-lookup"><span data-stu-id="01a7e-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="01a7e-143">Trvalost členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="01a7e-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="01a7e-144">Skupiny s jedním uživatelem</span><span class="sxs-lookup"><span data-stu-id="01a7e-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="01a7e-145">Postup zpracování událostí životního cyklu připojení ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="01a7e-146">Když se připojí, odpojí se a OnReconnected se zavolají.</span><span class="sxs-lookup"><span data-stu-id="01a7e-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="01a7e-147">Stav volajícího není naplněný.</span><span class="sxs-lookup"><span data-stu-id="01a7e-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="01a7e-148">Jak získat informace o klientovi z kontextové vlastnosti</span><span class="sxs-lookup"><span data-stu-id="01a7e-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="01a7e-149">Postup předání stavu mezi klienty a třídou centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="01a7e-150">Jak zpracovávat chyby ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="01a7e-151">Jak volat klientské metody a spravovat skupiny mimo třídu centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="01a7e-152">Volání metod klienta</span><span class="sxs-lookup"><span data-stu-id="01a7e-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="01a7e-153">Správa členství ve skupinách</span><span class="sxs-lookup"><span data-stu-id="01a7e-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="01a7e-154">Jak povolit trasování</span><span class="sxs-lookup"><span data-stu-id="01a7e-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="01a7e-155">Postup přizpůsobení kanálu Center</span><span class="sxs-lookup"><span data-stu-id="01a7e-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="01a7e-156">Dokumentaci k programům pro klienty naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="01a7e-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="01a7e-157">Průvodce rozhraním API pro centra signálů – JavaScriptový klient</span><span class="sxs-lookup"><span data-stu-id="01a7e-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="01a7e-158">Průvodce rozhraním API pro centra signálů – klient .NET</span><span class="sxs-lookup"><span data-stu-id="01a7e-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="01a7e-159">Součásti serveru pro Signal 2 jsou k dispozici pouze v rozhraní .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="01a7e-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="01a7e-160">Servery, na kterých běží .NET 4,0, musí používat signál v1. x.</span><span class="sxs-lookup"><span data-stu-id="01a7e-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="01a7e-161">Registrace middlewaru signálu</span><span class="sxs-lookup"><span data-stu-id="01a7e-161">How to register SignalR middleware</span></span>

<span data-ttu-id="01a7e-162">Chcete-li definovat trasu, kterou budou klienti používat pro připojení k vašemu rozbočovači, zavolejte metodu `MapSignalR` při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="01a7e-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="01a7e-163">`MapSignalR` je [metoda rozšíření](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) pro třídu `OwinExtensions`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="01a7e-164">Následující příklad ukazuje, jak definovat trasu centra signalizace pomocí třídy OWIN Startup.</span><span class="sxs-lookup"><span data-stu-id="01a7e-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="01a7e-165">Pokud přidáváte funkce signalizace do aplikace ASP.NET MVC, ujistěte se, že je před ostatními trasa přidána trasa signálu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="01a7e-166">Další informace najdete v tématu [kurz: Začínáme pomocí nástroje Signal 2 a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="01a7e-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="01a7e-167">Adresa URL/SignalR</span><span class="sxs-lookup"><span data-stu-id="01a7e-167">The /signalr URL</span></span>

<span data-ttu-id="01a7e-168">Ve výchozím nastavení je adresa URL trasy, kterou budou klienti používat pro připojení k vašemu centru, "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="01a7e-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="01a7e-169">(Nezaměňujte tuto adresu URL s adresou URL "/SignalR/Hubs", která je pro automaticky generovaný soubor JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="01a7e-170">Další informace o vygenerovaném proxy serveru najdete v tématu [Průvodce rozhraním API pro centra signalizace – JavaScriptový klient – vygenerovaný proxy server a co pro vás](hubs-api-guide-javascript-client.md#genproxy).)</span><span class="sxs-lookup"><span data-stu-id="01a7e-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="01a7e-171">Mohou nastat mimořádné okolnosti, které tuto základní adresu URL nedají použít pro signál. máte například složku v projektu s názvem *signaler* a nechcete změnit název.</span><span class="sxs-lookup"><span data-stu-id="01a7e-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="01a7e-172">V takovém případě můžete změnit základní adresu URL, jak je znázorněno v následujících příkladech (nahraďte "/SignalR" v ukázkovém kódu požadovanou adresou URL).</span><span class="sxs-lookup"><span data-stu-id="01a7e-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="01a7e-173">**Kód serveru, který určuje adresu URL**</span><span class="sxs-lookup"><span data-stu-id="01a7e-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="01a7e-174">**JavaScript – kód klienta, který určuje adresu URL (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="01a7e-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="01a7e-175">**JavaScriptový kód klienta, který určuje adresu URL (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="01a7e-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="01a7e-176">**Kód klienta .NET, který určuje adresu URL**</span><span class="sxs-lookup"><span data-stu-id="01a7e-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="01a7e-177">Konfigurace možností signalizace</span><span class="sxs-lookup"><span data-stu-id="01a7e-177">Configuring SignalR Options</span></span>

<span data-ttu-id="01a7e-178">Přetížení metody `MapSignalR` umožňují zadat vlastní adresu URL, vlastní překladač závislosti a následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="01a7e-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="01a7e-179">Povolí volání mezi doménami pomocí CORS nebo JSONP z prohlížečů klientů.</span><span class="sxs-lookup"><span data-stu-id="01a7e-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="01a7e-180">V případě, že prohlížeč načítá stránku z `http://contoso.com`, připojení k signalizaci je ve stejné doméně, v `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="01a7e-181">Pokud stránka z `http://contoso.com` vytvoří připojení k `http://fabrikam.com/signalr`, což je připojení mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="01a7e-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="01a7e-182">Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázaná.</span><span class="sxs-lookup"><span data-stu-id="01a7e-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="01a7e-183">Další informace najdete v tématu [Průvodce rozhraním API pro centra signálů ASP.NET – klient JavaScriptu – jak navázat připojení mezi doménami](hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="01a7e-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="01a7e-184">Povolte podrobné chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="01a7e-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="01a7e-185">Pokud dojde k chybám, je výchozím chováním signalizace odeslání do klientů oznamovací zpráva bez podrobností o tom, co se stalo.</span><span class="sxs-lookup"><span data-stu-id="01a7e-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="01a7e-186">Odeslání podrobných informací o chybách klientům se nedoporučuje v produkčním prostředí, protože uživatelé se zlými úmysly můžou používat informace v útocích proti vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="01a7e-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="01a7e-187">Při řešení potíží můžete tuto možnost použít k dočasnému povolení více informativních zpráv o chybách.</span><span class="sxs-lookup"><span data-stu-id="01a7e-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="01a7e-188">Zakáže automaticky generované soubory proxy JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="01a7e-189">Ve výchozím nastavení je soubor JavaScriptu s proxy pro vaše třídy centra vygenerovaný jako odpověď na adresu URL "/SignalR/Hubs".</span><span class="sxs-lookup"><span data-stu-id="01a7e-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="01a7e-190">Pokud nechcete používat proxy servery JavaScript, nebo pokud chcete tento soubor vygenerovat ručně a můžete se podívat na fyzický soubor ve vašich klientech, můžete tuto možnost použít k zakázání generování proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="01a7e-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="01a7e-191">Další informace najdete v tématu [Průvodce rozhraním API pro centra signálů – klient JavaScript – jak vytvořit fyzický soubor pro proxy vygenerovaný signálem](hubs-api-guide-javascript-client.md#manualproxy).</span><span class="sxs-lookup"><span data-stu-id="01a7e-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="01a7e-192">Následující příklad ukazuje, jak zadat adresu URL připojení signálů a tyto možnosti ve volání metody `MapSignalR`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="01a7e-193">Chcete-li zadat vlastní adresu URL, nahraďte text "/SignalR" v příkladu adresou URL, kterou chcete použít.</span><span class="sxs-lookup"><span data-stu-id="01a7e-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="01a7e-194">Jak vytvořit a používat třídy centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-194">How to create and use Hub classes</span></span>

<span data-ttu-id="01a7e-195">Chcete-li vytvořit centrum, vytvořte třídu, která je odvozena z [Microsoft. ASPNET. signaler. hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="01a7e-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="01a7e-196">Následující příklad ukazuje jednoduchou třídu centra pro aplikaci chatu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="01a7e-197">V tomto příkladu může připojený klient volat metodu `NewContosoChatMessage` a v případě, že je přijatá data, se budou všesměrově vysílat všem připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="01a7e-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="01a7e-198">Doba života objektu centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-198">Hub object lifetime</span></span>

<span data-ttu-id="01a7e-199">Nemusíte vytvářet instanci třídy centra ani volat své metody z vlastního kódu na serveru; To je vše, co pro vás prochází kanálem pro centra signalizace.</span><span class="sxs-lookup"><span data-stu-id="01a7e-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="01a7e-200">Signál vytvoří novou instanci třídy centra pokaždé, když potřebuje zpracovat operaci centra, například když se klient připojí, odpojí nebo provede volání metody serveru.</span><span class="sxs-lookup"><span data-stu-id="01a7e-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="01a7e-201">Vzhledem k tomu, že instance třídy centra jsou přechodné, nemůžete je použít pro zachování stavu z jednoho volání metody do dalšího.</span><span class="sxs-lookup"><span data-stu-id="01a7e-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="01a7e-202">Pokaždé, když server obdrží volání metody z klienta, zpracuje nová instance třídy hub zprávu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="01a7e-203">Chcete-li zachovat stav prostřednictvím více připojení a volání metod, použijte jinou metodu, jako je například databáze nebo statickou proměnnou na třídě centra, nebo jinou třídu, která není odvozena z `Hub`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="01a7e-204">Pokud uchováváte data v paměti pomocí metody, jako je statická proměnná na třídě centra, data budou ztracena při recyklování domény aplikace.</span><span class="sxs-lookup"><span data-stu-id="01a7e-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="01a7e-205">Pokud chcete odesílat zprávy klientům z vlastního kódu, který se spouští mimo třídu centra, nemůžete to provést vytvořením instance instance třídy centra, ale můžete to provést tak, že získáte odkaz na objekt kontextu signálu pro vaši třídu centra.</span><span class="sxs-lookup"><span data-stu-id="01a7e-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="01a7e-206">Další informace najdete v tématu [jak volat klientské metody a spravovat skupiny mimo třídu centra](#callfromoutsidehub) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="01a7e-207">Ve stylu CamelCase – velká a malá písmena názvů hub v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="01a7e-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="01a7e-208">Ve výchozím nastavení klienti JavaScriptu odkazují na centra pomocí verze ve stylu CamelCase-použita názvu třídy.</span><span class="sxs-lookup"><span data-stu-id="01a7e-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="01a7e-209">Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="01a7e-210">Předchozí příklad by se odkazoval jako `contosoChatHub` v kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="01a7e-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="01a7e-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="01a7e-212">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="01a7e-213">Pokud chcete zadat jiný název, který budou klienti používat, přidejte atribut `HubName`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="01a7e-214">Použijete-li atribut `HubName`, nebudete mít v klientech jazyka JavaScript ve stylu CamelCase případnou změnu názvu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="01a7e-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="01a7e-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="01a7e-216">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="01a7e-217">Více Center</span><span class="sxs-lookup"><span data-stu-id="01a7e-217">Multiple Hubs</span></span>

<span data-ttu-id="01a7e-218">V aplikaci můžete definovat více tříd rozbočovačů.</span><span class="sxs-lookup"><span data-stu-id="01a7e-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="01a7e-219">Když to uděláte, připojení se sdílí, ale skupiny se oddělují:</span><span class="sxs-lookup"><span data-stu-id="01a7e-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="01a7e-220">Všichni klienti budou používat stejnou adresu URL k navázání připojení k signalizaci pomocí služby (/SignalR nebo vlastní adresy URL, pokud jste ji zadali), a toto připojení se používá pro všechna centra definovaná službou.</span><span class="sxs-lookup"><span data-stu-id="01a7e-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="01a7e-221">V porovnání s definováním všech funkcí centra v jedné třídě neexistuje rozdíl mezi výkonem pro více Center.</span><span class="sxs-lookup"><span data-stu-id="01a7e-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="01a7e-222">Všechna centra získají stejné informace požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="01a7e-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="01a7e-223">Vzhledem k tomu, že všechna centra sdílejí stejné připojení, jediné informace o požadavku HTTP, které server získá, jsou součástí původní žádosti HTTP, která vytváří připojení k signalizaci.</span><span class="sxs-lookup"><span data-stu-id="01a7e-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="01a7e-224">Pokud použijete požadavek na připojení k předávání informací z klienta na server zadáním řetězce dotazu, nemůžete do různých Center zadávat různé řetězce dotazů.</span><span class="sxs-lookup"><span data-stu-id="01a7e-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="01a7e-225">Všechna centra dostanou stejné informace.</span><span class="sxs-lookup"><span data-stu-id="01a7e-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="01a7e-226">Vygenerovaný soubor proxy JavaScript bude obsahovat proxy pro všechna centra v jednom souboru.</span><span class="sxs-lookup"><span data-stu-id="01a7e-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="01a7e-227">Informace o proxy serverech JavaScript najdete v tématu [Průvodce rozhraním API pro centra signalizace – JavaScriptový klient – vygenerovaný proxy server a co pro vás dělá](hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="01a7e-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="01a7e-228">Skupiny se definují v rámci Center.</span><span class="sxs-lookup"><span data-stu-id="01a7e-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="01a7e-229">V nástroji Signal můžete definovat pojmenované skupiny pro všesměrové vysílání pro submnožiny připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="01a7e-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="01a7e-230">Skupiny se uchovávají samostatně pro každé centrum.</span><span class="sxs-lookup"><span data-stu-id="01a7e-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="01a7e-231">Například skupina s názvem "Administrators" by zahrnovala jednu sadu klientů pro třídu `ContosoChatHub` a stejný název skupiny by odkazoval na jinou sadu klientů pro třídu `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="01a7e-232">Rozbočovače silného typu</span><span class="sxs-lookup"><span data-stu-id="01a7e-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="01a7e-233">Chcete-li definovat rozhraní pro vaše metody rozbočovače, na které může klient odkazovat (a povolit technologii IntelliSense v metodách vašeho rozbočovače), odvodit své centrum od `Hub<T>` (představeno v Signaler 2,1) místo `Hub`:</span><span class="sxs-lookup"><span data-stu-id="01a7e-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="01a7e-234">Jak definovat metody ve třídě centra, které můžou klienti volat</span><span class="sxs-lookup"><span data-stu-id="01a7e-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="01a7e-235">K vystavení metody na rozbočovači, který chcete volat z klienta, deklarujte veřejnou metodu, jak je znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="01a7e-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="01a7e-236">Můžete zadat návratový typ a parametry, včetně složitých typů a polí, stejně jako v libovolné C# metodě.</span><span class="sxs-lookup"><span data-stu-id="01a7e-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="01a7e-237">Všechna data, která se zobrazí v parametrech nebo se vrátí volajícímu, se přenáší mezi klientem a serverem pomocí JSON a signalizace zpracovává vazbu složitých objektů a polí objektů automaticky.</span><span class="sxs-lookup"><span data-stu-id="01a7e-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="01a7e-238">Ve stylu CamelCase – velká a malá písmena názvů metod v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="01a7e-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="01a7e-239">Ve výchozím nastavení klienti JavaScriptu odkazují na metody centra pomocí verze ve stylu CamelCase-použita názvu metody.</span><span class="sxs-lookup"><span data-stu-id="01a7e-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="01a7e-240">Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="01a7e-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="01a7e-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="01a7e-242">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="01a7e-243">Pokud chcete zadat jiný název, který budou klienti používat, přidejte atribut `HubMethodName`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="01a7e-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="01a7e-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="01a7e-245">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="01a7e-246">Kdy spustit asynchronně</span><span class="sxs-lookup"><span data-stu-id="01a7e-246">When to execute asynchronously</span></span>

<span data-ttu-id="01a7e-247">Pokud bude metoda dlouhodobě spuštěna nebo bude muset dělat práci, která by vyžadovala čekání, jako je například vyhledávání databáze nebo volání webové služby, udělejte asynchronní metodu tak, že vrátíte [úlohu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (místo `void` Return) nebo objekt [&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) objektu (místo `T` návratového typu).</span><span class="sxs-lookup"><span data-stu-id="01a7e-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="01a7e-248">Při vrácení objektu `Task` z metody čeká signál, aby se `Task` dokončil, a poté pošle nezabalený výsledek zpátky klientovi, takže nedochází k žádnému rozdílu ve způsobu, jakým je volání metody v klientovi nijak zakódovat.</span><span class="sxs-lookup"><span data-stu-id="01a7e-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="01a7e-249">Když se metoda rozbočovače stane asynchronním, vyhnete se tak blokování připojení při použití přenosu protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="01a7e-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="01a7e-250">Když se metoda rozbočovače provádí synchronně a přenos je WebSocket, následné vyvolání metod v centru od stejného klienta se zablokuje, dokud se nedokončí metoda centra.</span><span class="sxs-lookup"><span data-stu-id="01a7e-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="01a7e-251">Následující příklad ukazuje stejný kód pro spuštění synchronně nebo asynchronně, následovaný kódem JavaScriptu klienta, který funguje pro volání buď verze.</span><span class="sxs-lookup"><span data-stu-id="01a7e-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="01a7e-252">**Synchronizace**</span><span class="sxs-lookup"><span data-stu-id="01a7e-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="01a7e-253">**Asynchronně**</span><span class="sxs-lookup"><span data-stu-id="01a7e-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="01a7e-254">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="01a7e-255">Další informace o použití asynchronních metod v ASP.NET 4,5 najdete v tématu [Použití asynchronních metod v ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="01a7e-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="01a7e-256">Definování přetížení</span><span class="sxs-lookup"><span data-stu-id="01a7e-256">Defining Overloads</span></span>

<span data-ttu-id="01a7e-257">Pokud chcete definovat přetížení pro metodu, počet parametrů v každém přetížení musí být jiný.</span><span class="sxs-lookup"><span data-stu-id="01a7e-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="01a7e-258">Pokud odlišujete přetížení pouhým zadáním různých typů parametrů, vaše třída centra se zkompiluje, ale služba Signaler vyvolá výjimku za běhu, když se klienti pokusí zavolat jedno z přetížení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="01a7e-259">Vytváření sestav o průběhu z volání metod centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="01a7e-260">Signal 2,1 přidává podporu pro [vzor vytváření sestav o průběhu](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) představený v .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="01a7e-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="01a7e-261">K implementaci vytváření sestav průběhu definujte parametr `IProgress<T>` pro metodu rozbočovače, ke které má klient přístup:</span><span class="sxs-lookup"><span data-stu-id="01a7e-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="01a7e-262">Při psaní dlouhotrvající metody serveru je důležité použít asynchronní programovací model, jako je například Async/await, namísto blokování vlákna centra.</span><span class="sxs-lookup"><span data-stu-id="01a7e-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="01a7e-263">Volání metod klienta z třídy hub</span><span class="sxs-lookup"><span data-stu-id="01a7e-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="01a7e-264">Chcete-li volat metody klienta ze serveru, použijte vlastnost `Clients` v metodě ve třídě hub.</span><span class="sxs-lookup"><span data-stu-id="01a7e-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="01a7e-265">Následující příklad ukazuje serverový kód, který volá `addNewMessageToPage` na všech připojených klientech, a klientský kód, který definuje metodu v klientovi jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="01a7e-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="01a7e-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="01a7e-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="01a7e-267">Vyvolání metody klienta je asynchronní operace a vrací `Task`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="01a7e-268">Použít `await`:</span><span class="sxs-lookup"><span data-stu-id="01a7e-268">Use `await`:</span></span>

* <span data-ttu-id="01a7e-269">Pro zajištění, že se zpráva pošle bez chyby.</span><span class="sxs-lookup"><span data-stu-id="01a7e-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="01a7e-270">Pro povolení zachycení a zpracování chyb v bloku try-catch.</span><span class="sxs-lookup"><span data-stu-id="01a7e-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="01a7e-271">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="01a7e-272">Z metody klienta nelze získat návratovou hodnotu. syntaxe, jako je `int x = Clients.All.add(1,1)`, nefunguje.</span><span class="sxs-lookup"><span data-stu-id="01a7e-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="01a7e-273">Můžete zadat komplexní typy a pole pro parametry.</span><span class="sxs-lookup"><span data-stu-id="01a7e-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="01a7e-274">Následující příklad předá klientovi komplexní typ v parametru metody.</span><span class="sxs-lookup"><span data-stu-id="01a7e-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="01a7e-275">**Serverový kód, který volá metodu klienta využívající složitý objekt**</span><span class="sxs-lookup"><span data-stu-id="01a7e-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="01a7e-276">**Kód serveru, který definuje komplexní objekt**</span><span class="sxs-lookup"><span data-stu-id="01a7e-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="01a7e-277">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="01a7e-278">Výběr klientů, kteří budou přijímat RPC</span><span class="sxs-lookup"><span data-stu-id="01a7e-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="01a7e-279">Vlastnost klienti vrátí objekt [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) , který poskytuje několik možností určení klientů, kteří budou přijímat RPC:</span><span class="sxs-lookup"><span data-stu-id="01a7e-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="01a7e-280">Všichni připojení klienti.</span><span class="sxs-lookup"><span data-stu-id="01a7e-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="01a7e-281">Pouze volající klient.</span><span class="sxs-lookup"><span data-stu-id="01a7e-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="01a7e-282">Všichni klienti s výjimkou volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="01a7e-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="01a7e-283">Konkrétní klient identifikovaný IDENTIFIKÁTORem připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="01a7e-284">Tento příklad volá `addContosoChatMessageToPage` na volajícím klientovi a má stejný účinek jako použití `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="01a7e-285">Všichni připojení klienti s výjimkou určených klientů identifikovaných IDENTIFIKÁTORem připojení</span><span class="sxs-lookup"><span data-stu-id="01a7e-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="01a7e-286">Všichni připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="01a7e-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="01a7e-287">Všechny připojené klienty v zadané skupině s výjimkou určených klientů identifikovaných podle ID připojení</span><span class="sxs-lookup"><span data-stu-id="01a7e-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="01a7e-288">Všichni připojení klienti v zadané skupině s výjimkou volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="01a7e-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="01a7e-289">Konkrétní uživatel identifikovaný identifikátorem userId.</span><span class="sxs-lookup"><span data-stu-id="01a7e-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="01a7e-290">Ve výchozím nastavení je to `IPrincipal.Identity.Name`, ale můžete ho změnit [registrací implementace IUserIdProvider s globálním hostitelem](mapping-users-to-connections.md#IUserIdProvider).</span><span class="sxs-lookup"><span data-stu-id="01a7e-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="01a7e-291">Všichni klienti a skupiny v seznamu ID připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="01a7e-292">Seznam skupin.</span><span class="sxs-lookup"><span data-stu-id="01a7e-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="01a7e-293">Uživatel podle jména</span><span class="sxs-lookup"><span data-stu-id="01a7e-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="01a7e-294">Seznam uživatelských jmen (představených v nástroji Signal 2,1).</span><span class="sxs-lookup"><span data-stu-id="01a7e-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="01a7e-295">Žádné ověřování v době kompilace pro názvy metod</span><span class="sxs-lookup"><span data-stu-id="01a7e-295">No compile-time validation for method names</span></span>

<span data-ttu-id="01a7e-296">Název metody, který zadáte, je interpretován jako dynamický objekt, což znamená, že pro něj není k dispozici žádná technologie IntelliSense nebo kompilace.</span><span class="sxs-lookup"><span data-stu-id="01a7e-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="01a7e-297">Výraz je vyhodnocen v době běhu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="01a7e-298">Když se spustí volání metody, Signal pošle klientovi název metody a hodnoty parametrů, a pokud má klient metodu, která odpovídá názvu, je tato metoda volána a hodnoty parametrů jsou předány.</span><span class="sxs-lookup"><span data-stu-id="01a7e-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="01a7e-299">Pokud není v klientovi nalezena žádná vyhovující metoda, není vyvolána žádná chyba.</span><span class="sxs-lookup"><span data-stu-id="01a7e-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="01a7e-300">Informace o formátu dat, která signalizace přenáší klientovi na pozadí při volání metody klienta, najdete v tématu [Úvod do nástroje Signal](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="01a7e-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="01a7e-301">Porovnávání názvů metod bez rozlišení velkých a malých písmen</span><span class="sxs-lookup"><span data-stu-id="01a7e-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="01a7e-302">Porovnávání názvů metod nerozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="01a7e-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="01a7e-303">Například `Clients.All.addContosoChatMessageToPage` na serveru spustí `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`nebo `addContosoChatMessageToPage` na klientovi.</span><span class="sxs-lookup"><span data-stu-id="01a7e-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="01a7e-304">Asynchronní spuštění</span><span class="sxs-lookup"><span data-stu-id="01a7e-304">Asynchronous execution</span></span>

<span data-ttu-id="01a7e-305">Volanou metodu provádí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="01a7e-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="01a7e-306">Jakýkoli kód, který přichází po volání metody do klienta, se spustí okamžitě bez čekání na dokončení přenosu dat do klientů, pokud nezadáte, že následující řádky kódu by měly čekat na dokončení metody.</span><span class="sxs-lookup"><span data-stu-id="01a7e-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="01a7e-307">Následující příklad kódu ukazuje, jak postupně provést dvě metody klienta.</span><span class="sxs-lookup"><span data-stu-id="01a7e-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="01a7e-308">**Použití operátoru Await (.NET 4,5)**</span><span class="sxs-lookup"><span data-stu-id="01a7e-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="01a7e-309">Použijete-li `await` pro čekání na dokončení metody klienta před spuštěním dalšího řádku kódu, neznamená to, že klienti zprávu obdrží, před provedením dalšího řádku kódu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="01a7e-310">"Dokončování" volání metody klienta znamená, že Signal dokončil vše potřebné k odeslání zprávy.</span><span class="sxs-lookup"><span data-stu-id="01a7e-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="01a7e-311">Pokud potřebujete ověření, že klienti obdrželi zprávu, musíte tento mechanismus programovat sami.</span><span class="sxs-lookup"><span data-stu-id="01a7e-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="01a7e-312">Například můžete kód metody `MessageReceived` v centru a v metodě `addContosoChatMessageToPage` na klientovi, kterou byste mohli volat `MessageReceived` po jakékoli práci, kterou potřebujete udělat na klientovi.</span><span class="sxs-lookup"><span data-stu-id="01a7e-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="01a7e-313">V `MessageReceived` v centru můžete provádět práci, která závisí na skutečném příjmu a zpracování původního volání metody.</span><span class="sxs-lookup"><span data-stu-id="01a7e-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="01a7e-314">Jak použít řetězcovou proměnnou jako název metody</span><span class="sxs-lookup"><span data-stu-id="01a7e-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="01a7e-315">Pokud chcete vyvolat metodu klienta pomocí proměnné řetězce jako název metody, přetypujte `Clients.All` (nebo `Clients.Others`, `Clients.Caller`atd.) na `IClientProxy` a pak zavolejte metodu [Invoke (MethodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="01a7e-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="01a7e-316">Správa členství ve skupinách z třídy hub</span><span class="sxs-lookup"><span data-stu-id="01a7e-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="01a7e-317">Skupiny v nástroji Signal poskytují metodu pro vysílání zpráv pro zadané podmnožiny připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="01a7e-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="01a7e-318">Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin.</span><span class="sxs-lookup"><span data-stu-id="01a7e-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="01a7e-319">Chcete-li spravovat členství ve skupině, použijte metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) a [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) poskytované vlastností `Groups` třídy hub.</span><span class="sxs-lookup"><span data-stu-id="01a7e-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="01a7e-320">Následující příklad ukazuje metody `Groups.Add` a `Groups.Remove` používané v metodách centra, které jsou volány klientským kódem, následovaný kódem jazyka JavaScript, který je volá.</span><span class="sxs-lookup"><span data-stu-id="01a7e-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="01a7e-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="01a7e-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="01a7e-322">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="01a7e-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="01a7e-323">Nemusíte explicitně vytvářet skupiny.</span><span class="sxs-lookup"><span data-stu-id="01a7e-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="01a7e-324">V důsledku toho se skupina automaticky vytvoří při prvním zadání názvu při volání `Groups.Add`a odstraní se, když odeberete Poslední připojení z jeho členství.</span><span class="sxs-lookup"><span data-stu-id="01a7e-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="01a7e-325">Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin.</span><span class="sxs-lookup"><span data-stu-id="01a7e-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="01a7e-326">Signal odesílá zprávy klientům a skupinám na základě [modelu Pub/sub](http://en.wikipedia.org/wiki/Publish/subscribe)a server neudržuje seznamy skupin nebo členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="01a7e-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="01a7e-327">To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, všechny stavy, které tento signál udržuje, musí být šířeny do nového uzlu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="01a7e-328">Asynchronní provádění metod Add a Remove</span><span class="sxs-lookup"><span data-stu-id="01a7e-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="01a7e-329">Metody `Groups.Add` a `Groups.Remove` provádějí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="01a7e-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="01a7e-330">Chcete-li přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, je nutné zajistit, aby byla metoda `Groups.Add` dokončena jako první.</span><span class="sxs-lookup"><span data-stu-id="01a7e-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="01a7e-331">Následující příklad kódu ukazuje, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="01a7e-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="01a7e-332">**Přidání klienta do skupiny a následné odeslání zprávy klientovi**</span><span class="sxs-lookup"><span data-stu-id="01a7e-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="01a7e-333">Trvalost členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="01a7e-333">Group membership persistence</span></span>

<span data-ttu-id="01a7e-334">Signál sleduje připojení, ne uživatele, takže pokud chcete, aby byl uživatel ve stejné skupině pokaždé, když uživatel vytvoří připojení, je nutné volat `Groups.Add` pokaždé, když uživatel vytvoří nové připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="01a7e-335">Po dočasné ztrátě připojení občas může signál obnovit připojení automaticky.</span><span class="sxs-lookup"><span data-stu-id="01a7e-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="01a7e-336">V takovém případě odesílatel obnovuje stejné připojení, nevytváří nové připojení, takže se automaticky obnoví členství klienta ve skupině.</span><span class="sxs-lookup"><span data-stu-id="01a7e-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="01a7e-337">To je možné i v případě, že dočasné přerušení je výsledkem restartování nebo selhání serveru, protože stav připojení pro každého klienta, včetně členství ve skupinách, je Trip klientovi.</span><span class="sxs-lookup"><span data-stu-id="01a7e-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="01a7e-338">Pokud dojde k výpadku serveru a jeho nahrazením novým serverem před vypršením časového limitu připojení, může se klient automaticky znovu připojit k novému serveru a znovu zaregistrovat do skupin, které je členem.</span><span class="sxs-lookup"><span data-stu-id="01a7e-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="01a7e-339">Pokud se připojení nedá obnovit automaticky po ztrátě připojení, nebo když vypršel časový limit připojení, nebo když se klient odpojí (například když se v prohlížeči přejde na novou stránku), ztratí se členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="01a7e-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="01a7e-340">Až se uživatel příště připojí, vytvoří se nové připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="01a7e-341">Aby se zachovalo členství ve skupině, když stejný uživatel vytváří nové připojení, musí vaše aplikace sledovat přidružení uživatelů a skupin a obnovovat členství ve skupině pokaždé, když uživatel vytvoří nové připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="01a7e-342">Další informace o připojení a opětovném připojení najdete v tématu [postup zpracování událostí životního cyklu připojení v třídě centra](#connectionlifetime) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="01a7e-343">Skupiny s jedním uživatelem</span><span class="sxs-lookup"><span data-stu-id="01a7e-343">Single-user groups</span></span>

<span data-ttu-id="01a7e-344">Aplikace, které používají signál, obvykle musí sledovat přidružení mezi uživateli a připojení, aby věděli, který uživatel odeslal zprávu a kteří uživatelé by měli zprávu přijímat.</span><span class="sxs-lookup"><span data-stu-id="01a7e-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="01a7e-345">Skupiny se používají v jednom ze dvou běžně používaných vzorů.</span><span class="sxs-lookup"><span data-stu-id="01a7e-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="01a7e-346">Skupiny s jedním uživatelem.</span><span class="sxs-lookup"><span data-stu-id="01a7e-346">Single-user groups.</span></span>

    <span data-ttu-id="01a7e-347">Můžete zadat uživatelské jméno jako název skupiny a při každém připojení nebo opětovném připojení uživatele přidat aktuální ID připojení ke skupině.</span><span class="sxs-lookup"><span data-stu-id="01a7e-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="01a7e-348">K odesílání zpráv uživateli, který jste odeslali do skupiny.</span><span class="sxs-lookup"><span data-stu-id="01a7e-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="01a7e-349">Nevýhodou této metody je, že skupina neposkytuje způsob, jak zjistit, jestli je uživatel online nebo offline.</span><span class="sxs-lookup"><span data-stu-id="01a7e-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="01a7e-350">Sledujte přidružení mezi uživatelskými jmény a identifikátory připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="01a7e-351">Můžete uložit přidružení mezi jednotlivými uživatelskými jmény a jedním nebo více ID připojení ve slovníku nebo databázi a při každém připojení nebo odpojení uživatele aktualizovat uložená data.</span><span class="sxs-lookup"><span data-stu-id="01a7e-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="01a7e-352">K odesílání zpráv uživateli zadejte ID připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="01a7e-353">Nevýhodou této metody je, že má více paměti.</span><span class="sxs-lookup"><span data-stu-id="01a7e-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="01a7e-354">Postup zpracování událostí životního cyklu připojení ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="01a7e-355">Typickými důvody pro zpracování událostí životního cyklu připojení je sledovat, zda je uživatel připojen nebo nikoli, a sledovat přidružení mezi uživatelskými jmény a identifikátory připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="01a7e-356">Chcete-li spustit vlastní kód, když se klienti připojují nebo odpojí, přepište `OnConnected`, `OnDisconnected`a `OnReconnected` virtuální metody třídy hub, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="01a7e-357">Když se připojí, odpojí se a OnReconnected se zavolají.</span><span class="sxs-lookup"><span data-stu-id="01a7e-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="01a7e-358">Pokaždé, když prohlížeč přejde na novou stránku, je nutné vytvořit nové připojení, což znamená, že signál spustí metodu `OnDisconnected` následovanou metodou `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="01a7e-359">Při navázání nového připojení se signálem vždy vytvoří nové ID připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="01a7e-360">Metoda `OnReconnected` se volá, když se dokončí dočasná přerušení připojení, na které se může signál automaticky zotavit, například když se kabel dočasně odpojí a znovu připojí před vypršením časového limitu připojení. Metoda `OnDisconnected` je volána, když je klient odpojen a uživatel se nemůže automaticky znovu připojit, například když prohlížeč přejde na novou stránku.</span><span class="sxs-lookup"><span data-stu-id="01a7e-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="01a7e-361">Proto je možné posloupnost událostí pro daného klienta `OnConnected`, `OnReconnected``OnDisconnected`; nebo `OnConnected``OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="01a7e-362">Pro dané připojení se nezobrazí `OnConnected`sekvence, `OnDisconnected``OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="01a7e-363">Metoda `OnDisconnected` se v některých scénářích nevolá, například když dojde k výpadku serveru nebo pokud se doména aplikace recykluje.</span><span class="sxs-lookup"><span data-stu-id="01a7e-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="01a7e-364">Když je na řádku nebo v doméně aplikace dokončená recyklace jiného serveru, můžou se někteří klienti moci znovu připojit a spustit událost `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="01a7e-365">Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení v nástroji Signal](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="01a7e-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="01a7e-366">Stav volajícího není naplněný.</span><span class="sxs-lookup"><span data-stu-id="01a7e-366">Caller state not populated</span></span>

<span data-ttu-id="01a7e-367">Metody obslužné rutiny události doby života připojení jsou volány ze serveru, což znamená, že všechny stavy, které umístíte do objektu `state` v klientovi, nebudou naplněny do vlastnosti `Caller` na serveru.</span><span class="sxs-lookup"><span data-stu-id="01a7e-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="01a7e-368">Informace o objektu `state` a vlastnosti `Caller` naleznete v tématu [jak předat stav mezi klienty a třídou centra](#passstate) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="01a7e-369">Jak získat informace o klientovi z kontextové vlastnosti</span><span class="sxs-lookup"><span data-stu-id="01a7e-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="01a7e-370">Chcete-li získat informace o klientovi, použijte vlastnost `Context` třídy centra.</span><span class="sxs-lookup"><span data-stu-id="01a7e-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="01a7e-371">Vlastnost `Context` vrátí objekt [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) , který poskytuje přístup k následujícím informacím:</span><span class="sxs-lookup"><span data-stu-id="01a7e-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="01a7e-372">ID připojení volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="01a7e-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="01a7e-373">ID připojení je identifikátor GUID, který je přiřazený signálem (hodnotu nemůžete zadat ve svém vlastním kódu).</span><span class="sxs-lookup"><span data-stu-id="01a7e-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="01a7e-374">Pro každé připojení existuje jedno ID připojení a stejné ID připojení se používá pro všechna centra, pokud máte ve své aplikaci více rozbočovačů.</span><span class="sxs-lookup"><span data-stu-id="01a7e-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="01a7e-375">Data hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="01a7e-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="01a7e-376">Můžete také získat hlavičku protokolu HTTP z `Context.Headers`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="01a7e-377">Důvodem pro více odkazů na stejnou věc je, že nejprve byl vytvořen `Context.Headers`, byla vlastnost `Context.Request` přidána později a `Context.Headers` byla zachována z důvodu zpětné kompatibility.</span><span class="sxs-lookup"><span data-stu-id="01a7e-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="01a7e-378">Dotaz na data řetězce.</span><span class="sxs-lookup"><span data-stu-id="01a7e-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="01a7e-379">Můžete také získat data řetězce dotazu z `Context.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="01a7e-380">Řetězec dotazu, který získáte v této vlastnosti, je ten, který se použil s požadavkem HTTP, který vytvořil připojení k signalizaci.</span><span class="sxs-lookup"><span data-stu-id="01a7e-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="01a7e-381">Můžete přidat parametry řetězce dotazu do klienta nakonfigurováním připojení, což je pohodlný způsob, jak předat data o klientovi z klienta na server.</span><span class="sxs-lookup"><span data-stu-id="01a7e-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="01a7e-382">Následující příklad ukazuje jeden ze způsobů, jak přidat řetězec dotazu v klientovi jazyka JavaScript při použití vygenerovaného proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="01a7e-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="01a7e-383">Další informace o nastavení parametrů řetězce dotazu najdete v příručkách k rozhraní API pro klienty [JavaScriptu](hubs-api-guide-javascript-client.md) a [.NET](hubs-api-guide-net-client.md) .</span><span class="sxs-lookup"><span data-stu-id="01a7e-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="01a7e-384">Metodu přenosu, která se používá pro připojení v datech řetězce dotazu, můžete najít spolu s jinými hodnotami, které interně používají signály:</span><span class="sxs-lookup"><span data-stu-id="01a7e-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="01a7e-385">Hodnota `transportMethod` bude "WebSockets", "serverSentEvents", "foreverFrame" nebo "longPolling".</span><span class="sxs-lookup"><span data-stu-id="01a7e-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="01a7e-386">Všimněte si, že pokud zaškrtnete tuto hodnotu v metodě obslužné rutiny události `OnConnected`, může v některých scénářích zpočátku získat přenosovou hodnotu, která není koncovým vysjednaným způsobem přenosu pro připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="01a7e-387">V takovém případě metoda vyvolá výjimku a bude volána později po navázání finální metody přenosu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="01a7e-388">Soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="01a7e-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="01a7e-389">Soubory cookie můžete také získat z `Context.RequestCookies`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="01a7e-390">Informace o uživateli.</span><span class="sxs-lookup"><span data-stu-id="01a7e-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="01a7e-391">Objekt HttpContext pro požadavek:</span><span class="sxs-lookup"><span data-stu-id="01a7e-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="01a7e-392">Místo `HttpContext.Current` k získání `HttpContext` objektu pro připojení k signalizaci použijte tuto metodu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="01a7e-393">Postup předání stavu mezi klienty a třídou centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="01a7e-394">Klient proxy serveru poskytuje objekt `state`, ve kterém můžete ukládat data, která chcete přenést na server, pomocí jednotlivých volání metody.</span><span class="sxs-lookup"><span data-stu-id="01a7e-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="01a7e-395">Na serveru můžete získat přístup k těmto datům ve vlastnosti `Clients.Caller` v metodách centra, které jsou volány klienty.</span><span class="sxs-lookup"><span data-stu-id="01a7e-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="01a7e-396">Vlastnost `Clients.Caller` není vyplněna pro metody obslužné rutiny události doby života připojení `OnConnected`, `OnDisconnected`a `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="01a7e-397">Vytváření a aktualizace dat v objektu `state` a vlastnost `Clients.Caller` funguje v obou směrech.</span><span class="sxs-lookup"><span data-stu-id="01a7e-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="01a7e-398">Hodnoty na serveru můžete aktualizovat a předávat je zpátky klientovi.</span><span class="sxs-lookup"><span data-stu-id="01a7e-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="01a7e-399">Následující příklad ukazuje kód klienta JavaScriptu, který ukládá stav pro přenos do serveru při každém volání metody.</span><span class="sxs-lookup"><span data-stu-id="01a7e-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="01a7e-400">Následující příklad ukazuje ekvivalentní kód v klientovi .NET.</span><span class="sxs-lookup"><span data-stu-id="01a7e-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="01a7e-401">Ve třídě centra máte přístup k těmto datům ve vlastnosti `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="01a7e-402">Následující příklad ukazuje kód, který načte stav uvedený v předchozím příkladu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="01a7e-403">Tento mechanismus pro trvalý stav není určený pro velké objemy dat, protože vše, co vložíte do vlastnosti `state` nebo `Clients.Caller`, je Round-Trip s každým voláním metody.</span><span class="sxs-lookup"><span data-stu-id="01a7e-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="01a7e-404">Je vhodný pro menší položky, jako jsou uživatelská jména nebo čítače.</span><span class="sxs-lookup"><span data-stu-id="01a7e-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="01a7e-405">V VB.NET nebo v rozbočovači se silným typem se k objektu stavu volajícího nelze dostat prostřednictvím `Clients.Caller`; místo toho použijte `Clients.CallerState` (představené v nástroji Signal 2,1):</span><span class="sxs-lookup"><span data-stu-id="01a7e-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="01a7e-406">**Použití CallerState vC#**</span><span class="sxs-lookup"><span data-stu-id="01a7e-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="01a7e-407">**Použití CallerState v Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="01a7e-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="01a7e-408">Jak zpracovávat chyby ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="01a7e-409">Chcete-li zpracovat chyby, ke kterým dochází v metodách vaší třídy rozbočovače, nejprve zkontrolujte, že je třeba pozorovat všechny výjimky z asynchronních operací (například vyvolání metod klienta) pomocí `await`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="01a7e-410">Pak použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="01a7e-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="01a7e-411">Zabalte kód metody v blocích try-catch a Zaprotokolujte objekt výjimky.</span><span class="sxs-lookup"><span data-stu-id="01a7e-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="01a7e-412">Pro účely ladění můžete výjimku odeslat klientovi, ale z bezpečnostních důvodů, které odesílají podrobné informace klientům v produkčním prostředí, se nedoporučuje.</span><span class="sxs-lookup"><span data-stu-id="01a7e-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="01a7e-413">Vytvořte modul kanálu centra, který zpracovává metodu [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="01a7e-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="01a7e-414">Následující příklad ukazuje modul kanálu, který protokoluje chyby, následovaný kódem v Startup.cs, který tento modul vloží do kanálu rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="01a7e-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="01a7e-415">Použijte třídu `HubException` (představená v Signal 2).</span><span class="sxs-lookup"><span data-stu-id="01a7e-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="01a7e-416">Tuto chybu je možné vyvolat z jakéhokoli vyvolání centra.</span><span class="sxs-lookup"><span data-stu-id="01a7e-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="01a7e-417">Konstruktor `HubError` přijímá zprávu řetězce a objekt pro ukládání dalších dat o chybách.</span><span class="sxs-lookup"><span data-stu-id="01a7e-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="01a7e-418">Nástroj Signal vygeneruje výjimku automaticky a pošle ji klientovi, kde bude použit k zamítnutí nebo selhání volání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="01a7e-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="01a7e-419">Následující ukázky kódu ukazují, jak vyvolat `HubException` během vyvolání centra a jak zpracovat výjimku v klientech JavaScript a .NET.</span><span class="sxs-lookup"><span data-stu-id="01a7e-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="01a7e-420">**Kód serveru, který demonstruje třídu HubException**</span><span class="sxs-lookup"><span data-stu-id="01a7e-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="01a7e-421">**Kód klienta JavaScriptu, který demonstruje odezvu na vyvolání HubException v centru**</span><span class="sxs-lookup"><span data-stu-id="01a7e-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="01a7e-422">**Kód klienta .NET, který demonstruje odezvu na vyvolání HubException v centru**</span><span class="sxs-lookup"><span data-stu-id="01a7e-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="01a7e-423">Další informace o modulech kanálu centra najdete v tématu [Postup přizpůsobení kanálu centra](#hubpipeline) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="01a7e-424">Jak povolit trasování</span><span class="sxs-lookup"><span data-stu-id="01a7e-424">How to enable tracing</span></span>

<span data-ttu-id="01a7e-425">Chcete-li povolit trasování na straně serveru, přidejte do souboru Web. config prvek System. Diagnostics, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="01a7e-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="01a7e-426">Při spuštění aplikace v aplikaci Visual Studio můžete zobrazit protokoly v okně **výstup** .</span><span class="sxs-lookup"><span data-stu-id="01a7e-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="01a7e-427">Jak volat klientské metody a spravovat skupiny mimo třídu centra</span><span class="sxs-lookup"><span data-stu-id="01a7e-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="01a7e-428">Chcete-li volat metody klienta z jiné třídy než vaší třídy centra, získejte odkaz na objekt kontextu signálu pro centrum a použijte jej ke volání metod v klientovi nebo správě skupin.</span><span class="sxs-lookup"><span data-stu-id="01a7e-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="01a7e-429">Následující vzorová `StockTicker` Třída získá objekt kontextu, uloží ho do instance třídy, uloží instanci třídy do statické vlastnosti a použije kontext z instance třídy singleton k volání metody `updateStockPrice` na klientech, kteří jsou připojení k centru s názvem `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="01a7e-430">Pokud je třeba v dlouhodobém objektu použít kontext vícekrát, získejte odkaz a uložte ho místo pokaždé, když ho budete potřebovat znovu.</span><span class="sxs-lookup"><span data-stu-id="01a7e-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="01a7e-431">Když se kontext získá, zajistíte tak, že signál klientům pošle zprávy ve stejném pořadí, ve kterém vaše metody rozbočovače provedou vyvolání metod klienta.</span><span class="sxs-lookup"><span data-stu-id="01a7e-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="01a7e-432">Kurz, ve kterém se dozvíte, jak používat kontext signalizace pro centrum, najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal](../getting-started/tutorial-server-broadcast-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="01a7e-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="01a7e-433">Volání metod klienta</span><span class="sxs-lookup"><span data-stu-id="01a7e-433">Calling client methods</span></span>

<span data-ttu-id="01a7e-434">Můžete určit, kteří klienti obdrží RPC, ale máte méně možností než při volání z třídy centra.</span><span class="sxs-lookup"><span data-stu-id="01a7e-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="01a7e-435">Důvodem je, že kontext není přidružen ke konkrétnímu volání z klienta, takže žádné metody, které vyžadují znalosti aktuálního ID připojení, například `Clients.Others`nebo `Clients.Caller`nebo `Clients.OthersInGroup`, nejsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="01a7e-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="01a7e-436">K dispozici jsou následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="01a7e-436">The following options are available:</span></span>

- <span data-ttu-id="01a7e-437">Všichni připojení klienti.</span><span class="sxs-lookup"><span data-stu-id="01a7e-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="01a7e-438">Konkrétní klient identifikovaný IDENTIFIKÁTORem připojení.</span><span class="sxs-lookup"><span data-stu-id="01a7e-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="01a7e-439">Všichni připojení klienti s výjimkou určených klientů identifikovaných IDENTIFIKÁTORem připojení</span><span class="sxs-lookup"><span data-stu-id="01a7e-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="01a7e-440">Všichni připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="01a7e-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="01a7e-441">Všechny připojené klienty v zadané skupině s výjimkou určených klientů identifikovaných podle ID připojení</span><span class="sxs-lookup"><span data-stu-id="01a7e-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="01a7e-442">Pokud voláte do nehub třídy z metod ve třídě centra, můžete předat aktuální ID připojení a použít ho pomocí `Clients.Client`, `Clients.AllExcept`nebo `Clients.Group` pro simulaci `Clients.Caller`, `Clients.Others`nebo `Clients.OthersInGroup`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="01a7e-443">V následujícím příkladu třída `MoveShapeHub` předá ID připojení ke třídě `Broadcaster`, aby třída `Broadcaster` mohla simulovat `Clients.Others`.</span><span class="sxs-lookup"><span data-stu-id="01a7e-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="01a7e-444">Správa členství ve skupinách</span><span class="sxs-lookup"><span data-stu-id="01a7e-444">Managing group membership</span></span>

<span data-ttu-id="01a7e-445">Pro správu skupin máte stejné možnosti jako v rámci třídy centra.</span><span class="sxs-lookup"><span data-stu-id="01a7e-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="01a7e-446">Přidání klienta do skupiny</span><span class="sxs-lookup"><span data-stu-id="01a7e-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="01a7e-447">Odebrání klienta ze skupiny</span><span class="sxs-lookup"><span data-stu-id="01a7e-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="01a7e-448">Postup přizpůsobení kanálu Center</span><span class="sxs-lookup"><span data-stu-id="01a7e-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="01a7e-449">Signaler umožňuje vložit do kanálu rozbočovače vlastní kód.</span><span class="sxs-lookup"><span data-stu-id="01a7e-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="01a7e-450">Následující příklad ukazuje vlastní modul kanálů rozbočovače, který protokoluje každé volání příchozí metody přijaté z klienta a odchozí volání metody vyvolané na klientovi:</span><span class="sxs-lookup"><span data-stu-id="01a7e-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="01a7e-451">Následující kód v souboru *Startup.cs* registruje modul, který se má spustit v kanálu centra:</span><span class="sxs-lookup"><span data-stu-id="01a7e-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="01a7e-452">Existuje mnoho různých metod, které lze přepsat.</span><span class="sxs-lookup"><span data-stu-id="01a7e-452">There are many different methods that you can override.</span></span> <span data-ttu-id="01a7e-453">Úplný seznam naleznete v tématu [metody HubPipelineModule](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="01a7e-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
