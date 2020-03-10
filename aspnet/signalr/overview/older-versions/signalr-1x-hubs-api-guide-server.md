---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: Průvodce rozhraním API pro centra ASP.NET Signales – Server (Signal 1. x) | Microsoft Docs
author: bradygaster
description: Tento dokument popisuje, jak programovat serverovou stranu rozhraní API centra ASP.NET pro Signal verze 1,1 s ukázkami kódu demonstratin...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579637"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="29d7d-103">Průvodce rozhraním API pro centra ASP.NET Signal-Server (signál 1. x)</span><span class="sxs-lookup"><span data-stu-id="29d7d-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>

<span data-ttu-id="29d7d-104">autorem [Fletcher](https://github.com/pfletcher), který [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="29d7d-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="29d7d-105">Tento dokument popisuje, jak programovat serverovou stranu rozhraní API centra ASP.NET pro Signal verze 1,1 s ukázkami kódu, které demonstrují běžné možnosti.</span><span class="sxs-lookup"><span data-stu-id="29d7d-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="29d7d-106">Rozhraní API pro centra signalizace vám umožní provádět Vzdálená volání procedur (RPC) ze serveru pro připojené klienty a klienty na server.</span><span class="sxs-lookup"><span data-stu-id="29d7d-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="29d7d-107">V kódu serveru můžete definovat metody, které mohou být volány klienty, a volat metody, které jsou spouštěny v klientovi.</span><span class="sxs-lookup"><span data-stu-id="29d7d-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="29d7d-108">V kódu klienta definujete metody, které mohou být volány ze serveru, a voláte metody, které jsou spuštěny na serveru.</span><span class="sxs-lookup"><span data-stu-id="29d7d-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="29d7d-109">Signalizace postará o všechny instalace klienta na server za vás.</span><span class="sxs-lookup"><span data-stu-id="29d7d-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="29d7d-110">Nástroj Signal také nabízí nižší úroveň rozhraní API označované jako trvalá připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="29d7d-111">Úvod do nástroje pro signalizaci, centra a trvalá připojení nebo v kurzu, který ukazuje, jak sestavit kompletní aplikaci signalizace, najdete v tématu [signaler-Začínáme](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="29d7d-112">Přehled</span><span class="sxs-lookup"><span data-stu-id="29d7d-112">Overview</span></span>

<span data-ttu-id="29d7d-113">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="29d7d-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="29d7d-114">Jak zaregistrovat trasu signalizace a nakonfigurovat možnosti signalizace</span><span class="sxs-lookup"><span data-stu-id="29d7d-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="29d7d-115">Adresa URL/SignalR</span><span class="sxs-lookup"><span data-stu-id="29d7d-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="29d7d-116">Konfigurace možností signalizace</span><span class="sxs-lookup"><span data-stu-id="29d7d-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="29d7d-117">Jak vytvořit a používat třídy centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="29d7d-118">Doba života objektu centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="29d7d-119">Ve stylu CamelCase – velká a malá písmena názvů hub v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="29d7d-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="29d7d-120">Více Center</span><span class="sxs-lookup"><span data-stu-id="29d7d-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="29d7d-121">Jak definovat metody ve třídě centra, které můžou klienti volat</span><span class="sxs-lookup"><span data-stu-id="29d7d-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="29d7d-122">Ve stylu CamelCase – velká a malá písmena názvů metod v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="29d7d-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="29d7d-123">Kdy spustit asynchronně</span><span class="sxs-lookup"><span data-stu-id="29d7d-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="29d7d-124">Definování přetížení</span><span class="sxs-lookup"><span data-stu-id="29d7d-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="29d7d-125">Volání metod klienta z třídy hub</span><span class="sxs-lookup"><span data-stu-id="29d7d-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="29d7d-126">Výběr klientů, kteří budou přijímat RPC</span><span class="sxs-lookup"><span data-stu-id="29d7d-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="29d7d-127">Žádné ověřování v době kompilace pro názvy metod</span><span class="sxs-lookup"><span data-stu-id="29d7d-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="29d7d-128">Porovnávání názvů metod bez rozlišení velkých a malých písmen</span><span class="sxs-lookup"><span data-stu-id="29d7d-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="29d7d-129">Asynchronní spuštění</span><span class="sxs-lookup"><span data-stu-id="29d7d-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="29d7d-130">Správa členství ve skupinách z třídy hub</span><span class="sxs-lookup"><span data-stu-id="29d7d-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="29d7d-131">Asynchronní provádění metod Add a Remove</span><span class="sxs-lookup"><span data-stu-id="29d7d-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="29d7d-132">Trvalost členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="29d7d-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="29d7d-133">Skupiny s jedním uživatelem</span><span class="sxs-lookup"><span data-stu-id="29d7d-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="29d7d-134">Postup zpracování událostí životního cyklu připojení ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="29d7d-135">Když se připojí, odpojí se a OnReconnected se zavolají.</span><span class="sxs-lookup"><span data-stu-id="29d7d-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="29d7d-136">Stav volajícího není naplněný.</span><span class="sxs-lookup"><span data-stu-id="29d7d-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="29d7d-137">Jak získat informace o klientovi z kontextové vlastnosti</span><span class="sxs-lookup"><span data-stu-id="29d7d-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="29d7d-138">Postup předání stavu mezi klienty a třídou centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="29d7d-139">Jak zpracovávat chyby ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="29d7d-140">Jak volat klientské metody a spravovat skupiny mimo třídu centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="29d7d-141">Volání metod klienta</span><span class="sxs-lookup"><span data-stu-id="29d7d-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="29d7d-142">Správa členství ve skupinách</span><span class="sxs-lookup"><span data-stu-id="29d7d-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="29d7d-143">Jak povolit trasování</span><span class="sxs-lookup"><span data-stu-id="29d7d-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="29d7d-144">Postup přizpůsobení kanálu Center</span><span class="sxs-lookup"><span data-stu-id="29d7d-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="29d7d-145">Dokumentaci k programům pro klienty naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="29d7d-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="29d7d-146">Průvodce rozhraním API pro centra signálů – JavaScriptový klient</span><span class="sxs-lookup"><span data-stu-id="29d7d-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="29d7d-147">Průvodce rozhraním API pro centra signálů – klient .NET</span><span class="sxs-lookup"><span data-stu-id="29d7d-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="29d7d-148">Odkazy na referenční témata rozhraní API odkazují na verzi rozhraní API .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="29d7d-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="29d7d-149">Pokud používáte .NET 4, přečtěte si téma věnované [verzi rozhraní API rozhraní .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="29d7d-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="29d7d-150">Jak zaregistrovat trasu signalizace a nakonfigurovat možnosti signalizace</span><span class="sxs-lookup"><span data-stu-id="29d7d-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="29d7d-151">Chcete-li definovat trasu, kterou budou klienti používat pro připojení k vašemu rozbočovači, zavolejte metodu [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="29d7d-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="29d7d-152">`MapHubs` je [metoda rozšíření](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) pro třídu `System.Web.Routing.RouteCollection`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="29d7d-153">Následující příklad ukazuje, jak definovat trasu centra signalizace v souboru *Global. asax* .</span><span class="sxs-lookup"><span data-stu-id="29d7d-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="29d7d-154">Pokud přidáváte funkce signalizace do aplikace ASP.NET MVC, ujistěte se, že je před ostatními trasa přidána trasa signálu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="29d7d-155">Další informace najdete v tématu [kurz: Začínáme s nástrojem Signal and MVC 4](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="29d7d-156">Adresa URL/SignalR</span><span class="sxs-lookup"><span data-stu-id="29d7d-156">The /signalr URL</span></span>

<span data-ttu-id="29d7d-157">Ve výchozím nastavení je adresa URL trasy, kterou budou klienti používat pro připojení k vašemu centru, "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="29d7d-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="29d7d-158">(Nezaměňujte tuto adresu URL s adresou URL "/SignalR/Hubs", která je pro automaticky generovaný soubor JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="29d7d-159">Další informace o vygenerovaném proxy serveru najdete v tématu [Průvodce rozhraním API pro centra signalizace – JavaScriptový klient – vygenerovaný proxy server a co pro vás](index.md).)</span><span class="sxs-lookup"><span data-stu-id="29d7d-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="29d7d-160">Mohou nastat mimořádné okolnosti, které tuto základní adresu URL nedají použít pro signál. máte například složku v projektu s názvem *signaler* a nechcete změnit název.</span><span class="sxs-lookup"><span data-stu-id="29d7d-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="29d7d-161">V takovém případě můžete změnit základní adresu URL, jak je znázorněno v následujících příkladech (nahraďte "/SignalR" v ukázkovém kódu požadovanou adresou URL).</span><span class="sxs-lookup"><span data-stu-id="29d7d-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="29d7d-162">**Kód serveru, který určuje adresu URL**</span><span class="sxs-lookup"><span data-stu-id="29d7d-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="29d7d-163">**JavaScript – kód klienta, který určuje adresu URL (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="29d7d-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="29d7d-164">**JavaScriptový kód klienta, který určuje adresu URL (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="29d7d-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="29d7d-165">**Kód klienta .NET, který určuje adresu URL**</span><span class="sxs-lookup"><span data-stu-id="29d7d-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="29d7d-166">Konfigurace možností signalizace</span><span class="sxs-lookup"><span data-stu-id="29d7d-166">Configuring SignalR Options</span></span>

<span data-ttu-id="29d7d-167">Přetížení metody `MapHubs` umožňují zadat vlastní adresu URL, vlastní překladač závislosti a následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="29d7d-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="29d7d-168">Povolí volání mezi doménami z klientů prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="29d7d-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="29d7d-169">V případě, že prohlížeč načítá stránku z `http://contoso.com`, připojení k signalizaci je ve stejné doméně, v `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="29d7d-170">Pokud stránka z `http://contoso.com` vytvoří připojení k `http://fabrikam.com/signalr`, což je připojení mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="29d7d-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="29d7d-171">Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázaná.</span><span class="sxs-lookup"><span data-stu-id="29d7d-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="29d7d-172">Další informace najdete v tématu [Průvodce rozhraním API pro centra signálů ASP.NET – klient JavaScriptu – jak navázat připojení mezi doménami](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="29d7d-173">Povolte podrobné chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="29d7d-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="29d7d-174">Pokud dojde k chybám, je výchozím chováním signalizace odeslání do klientů oznamovací zpráva bez podrobností o tom, co se stalo.</span><span class="sxs-lookup"><span data-stu-id="29d7d-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="29d7d-175">Odeslání podrobných informací o chybách klientům se nedoporučuje v produkčním prostředí, protože uživatelé se zlými úmysly můžou používat informace v útocích proti vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="29d7d-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="29d7d-176">Při řešení potíží můžete tuto možnost použít k dočasnému povolení více informativních zpráv o chybách.</span><span class="sxs-lookup"><span data-stu-id="29d7d-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="29d7d-177">Zakáže automaticky generované soubory proxy JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="29d7d-178">Ve výchozím nastavení je soubor JavaScriptu s proxy pro vaše třídy centra vygenerovaný jako odpověď na adresu URL "/SignalR/Hubs".</span><span class="sxs-lookup"><span data-stu-id="29d7d-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="29d7d-179">Pokud nechcete používat proxy servery JavaScript, nebo pokud chcete tento soubor vygenerovat ručně a můžete se podívat na fyzický soubor ve vašich klientech, můžete tuto možnost použít k zakázání generování proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="29d7d-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="29d7d-180">Další informace najdete v tématu [Průvodce rozhraním API pro centra signálů – klient JavaScript – jak vytvořit fyzický soubor pro proxy vygenerovaný signálem](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="29d7d-181">Následující příklad ukazuje, jak zadat adresu URL připojení signálů a tyto možnosti ve volání metody `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="29d7d-182">Chcete-li zadat vlastní adresu URL, nahraďte text "/SignalR" v příkladu adresou URL, kterou chcete použít.</span><span class="sxs-lookup"><span data-stu-id="29d7d-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="29d7d-183">Jak vytvořit a používat třídy centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-183">How to create and use Hub classes</span></span>

<span data-ttu-id="29d7d-184">Chcete-li vytvořit centrum, vytvořte třídu, která je odvozena z [Microsoft. ASPNET. signaler. hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="29d7d-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="29d7d-185">Následující příklad ukazuje jednoduchou třídu centra pro aplikaci chatu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="29d7d-186">V tomto příkladu může připojený klient volat metodu `NewContosoChatMessage` a v případě, že je přijatá data, se budou všesměrově vysílat všem připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="29d7d-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="29d7d-187">Doba života objektu centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-187">Hub object lifetime</span></span>

<span data-ttu-id="29d7d-188">Nemusíte vytvářet instanci třídy centra ani volat své metody z vlastního kódu na serveru; To je vše, co pro vás prochází kanálem pro centra signalizace.</span><span class="sxs-lookup"><span data-stu-id="29d7d-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="29d7d-189">Signál vytvoří novou instanci třídy centra pokaždé, když potřebuje zpracovat operaci centra, například když se klient připojí, odpojí nebo provede volání metody serveru.</span><span class="sxs-lookup"><span data-stu-id="29d7d-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="29d7d-190">Vzhledem k tomu, že instance třídy centra jsou přechodné, nemůžete je použít pro zachování stavu z jednoho volání metody do dalšího.</span><span class="sxs-lookup"><span data-stu-id="29d7d-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="29d7d-191">Pokaždé, když server obdrží volání metody z klienta, zpracuje nová instance třídy hub zprávu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="29d7d-192">Chcete-li zachovat stav prostřednictvím více připojení a volání metod, použijte jinou metodu, jako je například databáze nebo statickou proměnnou na třídě centra, nebo jinou třídu, která není odvozena z `Hub`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="29d7d-193">Pokud uchováváte data v paměti pomocí metody, jako je statická proměnná na třídě centra, data budou ztracena při recyklování domény aplikace.</span><span class="sxs-lookup"><span data-stu-id="29d7d-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="29d7d-194">Pokud chcete odesílat zprávy klientům z vlastního kódu, který se spouští mimo třídu centra, nemůžete to provést vytvořením instance instance třídy centra, ale můžete to provést tak, že získáte odkaz na objekt kontextu signálu pro vaši třídu centra.</span><span class="sxs-lookup"><span data-stu-id="29d7d-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="29d7d-195">Další informace najdete v tématu [jak volat klientské metody a spravovat skupiny mimo třídu centra](#callfromoutsidehub) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="29d7d-196">Ve stylu CamelCase – velká a malá písmena názvů hub v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="29d7d-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="29d7d-197">Ve výchozím nastavení klienti JavaScriptu odkazují na centra pomocí verze ve stylu CamelCase-použita názvu třídy.</span><span class="sxs-lookup"><span data-stu-id="29d7d-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="29d7d-198">Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="29d7d-199">Předchozí příklad by se odkazoval jako `contosoChatHub` v kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="29d7d-200">**Server**</span><span class="sxs-lookup"><span data-stu-id="29d7d-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="29d7d-201">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="29d7d-202">Pokud chcete zadat jiný název, který budou klienti používat, přidejte atribut `HubName`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="29d7d-203">Použijete-li atribut `HubName`, nebudete mít v klientech jazyka JavaScript ve stylu CamelCase případnou změnu názvu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="29d7d-204">**Server**</span><span class="sxs-lookup"><span data-stu-id="29d7d-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="29d7d-205">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="29d7d-206">Více Center</span><span class="sxs-lookup"><span data-stu-id="29d7d-206">Multiple Hubs</span></span>

<span data-ttu-id="29d7d-207">V aplikaci můžete definovat více tříd rozbočovačů.</span><span class="sxs-lookup"><span data-stu-id="29d7d-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="29d7d-208">Když to uděláte, připojení se sdílí, ale skupiny se oddělují:</span><span class="sxs-lookup"><span data-stu-id="29d7d-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="29d7d-209">Všichni klienti budou používat stejnou adresu URL k navázání připojení k signalizaci pomocí služby (/SignalR nebo vlastní adresy URL, pokud jste ji zadali), a toto připojení se používá pro všechna centra definovaná službou.</span><span class="sxs-lookup"><span data-stu-id="29d7d-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="29d7d-210">V porovnání s definováním všech funkcí centra v jedné třídě neexistuje rozdíl mezi výkonem pro více Center.</span><span class="sxs-lookup"><span data-stu-id="29d7d-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="29d7d-211">Všechna centra získají stejné informace požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="29d7d-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="29d7d-212">Vzhledem k tomu, že všechna centra sdílejí stejné připojení, jediné informace o požadavku HTTP, které server získá, jsou součástí původní žádosti HTTP, která vytváří připojení k signalizaci.</span><span class="sxs-lookup"><span data-stu-id="29d7d-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="29d7d-213">Pokud použijete požadavek na připojení k předávání informací z klienta na server zadáním řetězce dotazu, nemůžete do různých Center zadávat různé řetězce dotazů.</span><span class="sxs-lookup"><span data-stu-id="29d7d-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="29d7d-214">Všechna centra dostanou stejné informace.</span><span class="sxs-lookup"><span data-stu-id="29d7d-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="29d7d-215">Vygenerovaný soubor proxy JavaScript bude obsahovat proxy pro všechna centra v jednom souboru.</span><span class="sxs-lookup"><span data-stu-id="29d7d-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="29d7d-216">Informace o proxy serverech JavaScript najdete v tématu [Průvodce rozhraním API pro centra signalizace – JavaScriptový klient – vygenerovaný proxy server a co pro vás dělá](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="29d7d-217">Skupiny se definují v rámci Center.</span><span class="sxs-lookup"><span data-stu-id="29d7d-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="29d7d-218">V nástroji Signal můžete definovat pojmenované skupiny pro všesměrové vysílání pro submnožiny připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="29d7d-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="29d7d-219">Skupiny se uchovávají samostatně pro každé centrum.</span><span class="sxs-lookup"><span data-stu-id="29d7d-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="29d7d-220">Například skupina s názvem "Administrators" by zahrnovala jednu sadu klientů pro třídu `ContosoChatHub` a stejný název skupiny by odkazoval na jinou sadu klientů pro třídu `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="29d7d-221">Jak definovat metody ve třídě centra, které můžou klienti volat</span><span class="sxs-lookup"><span data-stu-id="29d7d-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="29d7d-222">K vystavení metody na rozbočovači, který chcete volat z klienta, deklarujte veřejnou metodu, jak je znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="29d7d-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="29d7d-223">Můžete zadat návratový typ a parametry, včetně složitých typů a polí, stejně jako v libovolné C# metodě.</span><span class="sxs-lookup"><span data-stu-id="29d7d-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="29d7d-224">Všechna data, která se zobrazí v parametrech nebo se vrátí volajícímu, se přenáší mezi klientem a serverem pomocí JSON a signalizace zpracovává vazbu složitých objektů a polí objektů automaticky.</span><span class="sxs-lookup"><span data-stu-id="29d7d-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="29d7d-225">Ve stylu CamelCase – velká a malá písmena názvů metod v klientech JavaScript</span><span class="sxs-lookup"><span data-stu-id="29d7d-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="29d7d-226">Ve výchozím nastavení klienti JavaScriptu odkazují na metody centra pomocí verze ve stylu CamelCase-použita názvu metody.</span><span class="sxs-lookup"><span data-stu-id="29d7d-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="29d7d-227">Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="29d7d-228">**Server**</span><span class="sxs-lookup"><span data-stu-id="29d7d-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="29d7d-229">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="29d7d-230">Pokud chcete zadat jiný název, který budou klienti používat, přidejte atribut `HubMethodName`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="29d7d-231">**Server**</span><span class="sxs-lookup"><span data-stu-id="29d7d-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="29d7d-232">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="29d7d-233">Kdy spustit asynchronně</span><span class="sxs-lookup"><span data-stu-id="29d7d-233">When to execute asynchronously</span></span>

<span data-ttu-id="29d7d-234">Pokud bude metoda dlouhodobě spuštěna nebo bude muset dělat práci, která by vyžadovala čekání, jako je například vyhledávání databáze nebo volání webové služby, udělejte asynchronní metodu tak, že vrátíte [úlohu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (místo `void` Return) nebo objekt [&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) objektu (místo `T` návratového typu).</span><span class="sxs-lookup"><span data-stu-id="29d7d-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="29d7d-235">Při vrácení objektu `Task` z metody čeká signál, aby se `Task` dokončil, a poté pošle nezabalený výsledek zpátky klientovi, takže nedochází k žádnému rozdílu ve způsobu, jakým je volání metody v klientovi nijak zakódovat.</span><span class="sxs-lookup"><span data-stu-id="29d7d-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="29d7d-236">Když se metoda rozbočovače stane asynchronním, vyhnete se tak blokování připojení při použití přenosu protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="29d7d-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="29d7d-237">Když se metoda rozbočovače provádí synchronně a přenos je WebSocket, následné vyvolání metod v centru od stejného klienta se zablokuje, dokud se nedokončí metoda centra.</span><span class="sxs-lookup"><span data-stu-id="29d7d-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="29d7d-238">Následující příklad ukazuje stejný kód pro spuštění synchronně nebo asynchronně, následovaný kódem JavaScriptu klienta, který funguje pro volání buď verze.</span><span class="sxs-lookup"><span data-stu-id="29d7d-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="29d7d-239">**Synchronizace**</span><span class="sxs-lookup"><span data-stu-id="29d7d-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="29d7d-240">**Asynchronní – ASP.NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="29d7d-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="29d7d-241">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="29d7d-242">Další informace o použití asynchronních metod v ASP.NET 4,5 najdete v tématu [Použití asynchronních metod v ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="29d7d-243">Definování přetížení</span><span class="sxs-lookup"><span data-stu-id="29d7d-243">Defining Overloads</span></span>

<span data-ttu-id="29d7d-244">Pokud chcete definovat přetížení pro metodu, počet parametrů v každém přetížení musí být jiný.</span><span class="sxs-lookup"><span data-stu-id="29d7d-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="29d7d-245">Pokud odlišujete přetížení pouhým zadáním různých typů parametrů, vaše třída centra se zkompiluje, ale služba Signaler vyvolá výjimku za běhu, když se klienti pokusí zavolat jedno z přetížení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="29d7d-246">Volání metod klienta z třídy hub</span><span class="sxs-lookup"><span data-stu-id="29d7d-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="29d7d-247">Chcete-li volat metody klienta ze serveru, použijte vlastnost `Clients` v metodě ve třídě hub.</span><span class="sxs-lookup"><span data-stu-id="29d7d-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="29d7d-248">Následující příklad ukazuje serverový kód, který volá `addNewMessageToPage` na všech připojených klientech, a klientský kód, který definuje metodu v klientovi jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="29d7d-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="29d7d-249">**Server**</span><span class="sxs-lookup"><span data-stu-id="29d7d-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="29d7d-250">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="29d7d-251">Z metody klienta nelze získat návratovou hodnotu. syntaxe, jako je `int x = Clients.All.add(1,1)`, nefunguje.</span><span class="sxs-lookup"><span data-stu-id="29d7d-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="29d7d-252">Můžete zadat komplexní typy a pole pro parametry.</span><span class="sxs-lookup"><span data-stu-id="29d7d-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="29d7d-253">Následující příklad předá klientovi komplexní typ v parametru metody.</span><span class="sxs-lookup"><span data-stu-id="29d7d-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="29d7d-254">**Serverový kód, který volá metodu klienta využívající složitý objekt**</span><span class="sxs-lookup"><span data-stu-id="29d7d-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="29d7d-255">**Kód serveru, který definuje komplexní objekt**</span><span class="sxs-lookup"><span data-stu-id="29d7d-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="29d7d-256">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="29d7d-257">Výběr klientů, kteří budou přijímat RPC</span><span class="sxs-lookup"><span data-stu-id="29d7d-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="29d7d-258">Vlastnost klienti vrátí objekt [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) , který poskytuje několik možností určení klientů, kteří budou přijímat RPC:</span><span class="sxs-lookup"><span data-stu-id="29d7d-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="29d7d-259">Všichni připojení klienti.</span><span class="sxs-lookup"><span data-stu-id="29d7d-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="29d7d-260">Pouze volající klient.</span><span class="sxs-lookup"><span data-stu-id="29d7d-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="29d7d-261">Všichni klienti s výjimkou volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="29d7d-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="29d7d-262">Konkrétní klient identifikovaný IDENTIFIKÁTORem připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="29d7d-263">Tento příklad volá `addContosoChatMessageToPage` na volajícím klientovi a má stejný účinek jako použití `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="29d7d-264">Všichni připojení klienti s výjimkou určených klientů identifikovaných IDENTIFIKÁTORem připojení</span><span class="sxs-lookup"><span data-stu-id="29d7d-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="29d7d-265">Všichni připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="29d7d-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="29d7d-266">Všechny připojené klienty v zadané skupině s výjimkou určených klientů identifikovaných podle ID připojení</span><span class="sxs-lookup"><span data-stu-id="29d7d-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="29d7d-267">Všichni připojení klienti v zadané skupině s výjimkou volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="29d7d-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="29d7d-268">Žádné ověřování v době kompilace pro názvy metod</span><span class="sxs-lookup"><span data-stu-id="29d7d-268">No compile-time validation for method names</span></span>

<span data-ttu-id="29d7d-269">Název metody, který zadáte, je interpretován jako dynamický objekt, což znamená, že pro něj není k dispozici žádná technologie IntelliSense nebo kompilace.</span><span class="sxs-lookup"><span data-stu-id="29d7d-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="29d7d-270">Výraz je vyhodnocen v době běhu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="29d7d-271">Když se spustí volání metody, Signal pošle klientovi název metody a hodnoty parametrů, a pokud má klient metodu, která odpovídá názvu, je tato metoda volána a hodnoty parametrů jsou předány.</span><span class="sxs-lookup"><span data-stu-id="29d7d-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="29d7d-272">Pokud není v klientovi nalezena žádná vyhovující metoda, není vyvolána žádná chyba.</span><span class="sxs-lookup"><span data-stu-id="29d7d-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="29d7d-273">Informace o formátu dat, která signalizace přenáší klientovi na pozadí při volání metody klienta, najdete v tématu [Úvod do nástroje Signal](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="29d7d-274">Porovnávání názvů metod bez rozlišení velkých a malých písmen</span><span class="sxs-lookup"><span data-stu-id="29d7d-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="29d7d-275">Porovnávání názvů metod nerozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="29d7d-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="29d7d-276">Například `Clients.All.addContosoChatMessageToPage` na serveru spustí `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`nebo `addContosoChatMessageToPage` na klientovi.</span><span class="sxs-lookup"><span data-stu-id="29d7d-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="29d7d-277">Asynchronní spuštění</span><span class="sxs-lookup"><span data-stu-id="29d7d-277">Asynchronous execution</span></span>

<span data-ttu-id="29d7d-278">Volanou metodu provádí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="29d7d-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="29d7d-279">Jakýkoli kód, který přichází po volání metody do klienta, se spustí okamžitě bez čekání na dokončení přenosu dat do klientů, pokud nezadáte, že následující řádky kódu by měly čekat na dokončení metody.</span><span class="sxs-lookup"><span data-stu-id="29d7d-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="29d7d-280">Následující příklady kódu ukazují, jak postupně spouštět dvě metody klienta, jednu pomocí kódu, který funguje v rozhraní .NET 4,5, a jeden pomocí kódu, který funguje v rozhraní .NET 4.</span><span class="sxs-lookup"><span data-stu-id="29d7d-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="29d7d-281">**Příklad .NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="29d7d-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="29d7d-282">**Příklad .NET 4**</span><span class="sxs-lookup"><span data-stu-id="29d7d-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="29d7d-283">Použijete-li `await` nebo `ContinueWith` počkat na dokončení metody klienta před provedením dalšího řádku kódu, neznamená to, že klienti budou zprávu před spuštěním dalšího řádku kódu zobrazovat.</span><span class="sxs-lookup"><span data-stu-id="29d7d-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="29d7d-284">"Dokončování" volání metody klienta znamená, že Signal dokončil vše potřebné k odeslání zprávy.</span><span class="sxs-lookup"><span data-stu-id="29d7d-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="29d7d-285">Pokud potřebujete ověření, že klienti obdrželi zprávu, musíte tento mechanismus programovat sami.</span><span class="sxs-lookup"><span data-stu-id="29d7d-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="29d7d-286">Například můžete kód metody `MessageReceived` v centru a v metodě `addContosoChatMessageToPage` na klientovi, kterou byste mohli volat `MessageReceived` po jakékoli práci, kterou potřebujete udělat na klientovi.</span><span class="sxs-lookup"><span data-stu-id="29d7d-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="29d7d-287">V `MessageReceived` v centru můžete provádět práci, která závisí na skutečném příjmu a zpracování původního volání metody.</span><span class="sxs-lookup"><span data-stu-id="29d7d-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="29d7d-288">Jak použít řetězcovou proměnnou jako název metody</span><span class="sxs-lookup"><span data-stu-id="29d7d-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="29d7d-289">Pokud chcete vyvolat metodu klienta pomocí proměnné řetězce jako název metody, přetypujte `Clients.All` (nebo `Clients.Others`, `Clients.Caller`atd.) na `IClientProxy` a pak zavolejte metodu [Invoke (MethodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="29d7d-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="29d7d-290">Správa členství ve skupinách z třídy hub</span><span class="sxs-lookup"><span data-stu-id="29d7d-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="29d7d-291">Skupiny v nástroji Signal poskytují metodu pro vysílání zpráv pro zadané podmnožiny připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="29d7d-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="29d7d-292">Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin.</span><span class="sxs-lookup"><span data-stu-id="29d7d-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="29d7d-293">Chcete-li spravovat členství ve skupině, použijte metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) a [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) poskytované vlastností `Groups` třídy hub.</span><span class="sxs-lookup"><span data-stu-id="29d7d-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="29d7d-294">Následující příklad ukazuje metody `Groups.Add` a `Groups.Remove` používané v metodách centra, které jsou volány klientským kódem, následovaný kódem jazyka JavaScript, který je volá.</span><span class="sxs-lookup"><span data-stu-id="29d7d-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="29d7d-295">**Server**</span><span class="sxs-lookup"><span data-stu-id="29d7d-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="29d7d-296">**Klient jazyka JavaScript pomocí vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="29d7d-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="29d7d-297">Nemusíte explicitně vytvářet skupiny.</span><span class="sxs-lookup"><span data-stu-id="29d7d-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="29d7d-298">V důsledku toho se skupina automaticky vytvoří při prvním zadání názvu při volání `Groups.Add`a odstraní se, když odeberete Poslední připojení z jeho členství.</span><span class="sxs-lookup"><span data-stu-id="29d7d-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="29d7d-299">Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin.</span><span class="sxs-lookup"><span data-stu-id="29d7d-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="29d7d-300">Signal odesílá zprávy klientům a skupinám na základě [modelu Pub/sub](http://en.wikipedia.org/wiki/Publish/subscribe)a server neudržuje seznamy skupin nebo členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="29d7d-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="29d7d-301">To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, všechny stavy, které tento signál udržuje, musí být šířeny do nového uzlu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="29d7d-302">Asynchronní provádění metod Add a Remove</span><span class="sxs-lookup"><span data-stu-id="29d7d-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="29d7d-303">Metody `Groups.Add` a `Groups.Remove` provádějí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="29d7d-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="29d7d-304">Chcete-li přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, je nutné zajistit, aby byla metoda `Groups.Add` dokončena jako první.</span><span class="sxs-lookup"><span data-stu-id="29d7d-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="29d7d-305">Následující příklady kódu ukazují, jak to provést, pomocí kódu, který funguje v rozhraní .NET 4,5 a jeden pomocí kódu, který funguje v rozhraní .NET 4.</span><span class="sxs-lookup"><span data-stu-id="29d7d-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="29d7d-306">**Příklad .NET 4,5**</span><span class="sxs-lookup"><span data-stu-id="29d7d-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="29d7d-307">**Příklad .NET 4**</span><span class="sxs-lookup"><span data-stu-id="29d7d-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="29d7d-308">Trvalost členství ve skupině</span><span class="sxs-lookup"><span data-stu-id="29d7d-308">Group membership persistence</span></span>

<span data-ttu-id="29d7d-309">Signál sleduje připojení, ne uživatele, takže pokud chcete, aby byl uživatel ve stejné skupině pokaždé, když uživatel vytvoří připojení, je nutné volat `Groups.Add` pokaždé, když uživatel vytvoří nové připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="29d7d-310">Po dočasné ztrátě připojení občas může signál obnovit připojení automaticky.</span><span class="sxs-lookup"><span data-stu-id="29d7d-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="29d7d-311">V takovém případě odesílatel obnovuje stejné připojení, nevytváří nové připojení, takže se automaticky obnoví členství klienta ve skupině.</span><span class="sxs-lookup"><span data-stu-id="29d7d-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="29d7d-312">To je možné i v případě, že dočasné přerušení je výsledkem restartování nebo selhání serveru, protože stav připojení pro každého klienta, včetně členství ve skupinách, je Trip klientovi.</span><span class="sxs-lookup"><span data-stu-id="29d7d-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="29d7d-313">Pokud dojde k výpadku serveru a jeho nahrazením novým serverem před vypršením časového limitu připojení, může se klient automaticky znovu připojit k novému serveru a znovu zaregistrovat do skupin, které je členem.</span><span class="sxs-lookup"><span data-stu-id="29d7d-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="29d7d-314">Pokud se připojení nedá obnovit automaticky po ztrátě připojení, nebo když vypršel časový limit připojení, nebo když se klient odpojí (například když se v prohlížeči přejde na novou stránku), ztratí se členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="29d7d-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="29d7d-315">Až se uživatel příště připojí, vytvoří se nové připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="29d7d-316">Aby se zachovalo členství ve skupině, když stejný uživatel vytváří nové připojení, musí vaše aplikace sledovat přidružení uživatelů a skupin a obnovovat členství ve skupině pokaždé, když uživatel vytvoří nové připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="29d7d-317">Další informace o připojení a opětovném připojení najdete v tématu [postup zpracování událostí životního cyklu připojení v třídě centra](#connectionlifetime) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="29d7d-318">Skupiny s jedním uživatelem</span><span class="sxs-lookup"><span data-stu-id="29d7d-318">Single-user groups</span></span>

<span data-ttu-id="29d7d-319">Aplikace, které používají signál, obvykle musí sledovat přidružení mezi uživateli a připojení, aby věděli, který uživatel odeslal zprávu a kteří uživatelé by měli zprávu přijímat.</span><span class="sxs-lookup"><span data-stu-id="29d7d-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="29d7d-320">Skupiny se používají v jednom ze dvou běžně používaných vzorů.</span><span class="sxs-lookup"><span data-stu-id="29d7d-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="29d7d-321">Skupiny s jedním uživatelem.</span><span class="sxs-lookup"><span data-stu-id="29d7d-321">Single-user groups.</span></span>

    <span data-ttu-id="29d7d-322">Můžete zadat uživatelské jméno jako název skupiny a při každém připojení nebo opětovném připojení uživatele přidat aktuální ID připojení ke skupině.</span><span class="sxs-lookup"><span data-stu-id="29d7d-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="29d7d-323">K odesílání zpráv uživateli, který jste odeslali do skupiny.</span><span class="sxs-lookup"><span data-stu-id="29d7d-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="29d7d-324">Nevýhodou této metody je, že skupina neposkytuje způsob, jak zjistit, jestli je uživatel online nebo offline.</span><span class="sxs-lookup"><span data-stu-id="29d7d-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="29d7d-325">Sledujte přidružení mezi uživatelskými jmény a identifikátory připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="29d7d-326">Můžete uložit přidružení mezi jednotlivými uživatelskými jmény a jedním nebo více ID připojení ve slovníku nebo databázi a při každém připojení nebo odpojení uživatele aktualizovat uložená data.</span><span class="sxs-lookup"><span data-stu-id="29d7d-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="29d7d-327">K odesílání zpráv uživateli zadejte ID připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="29d7d-328">Nevýhodou této metody je, že má více paměti.</span><span class="sxs-lookup"><span data-stu-id="29d7d-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="29d7d-329">Postup zpracování událostí životního cyklu připojení ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="29d7d-330">Typickými důvody pro zpracování událostí životního cyklu připojení je sledovat, zda je uživatel připojen nebo nikoli, a sledovat přidružení mezi uživatelskými jmény a identifikátory připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="29d7d-331">Chcete-li spustit vlastní kód, když se klienti připojují nebo odpojí, přepište `OnConnected`, `OnDisconnected`a `OnReconnected` virtuální metody třídy hub, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="29d7d-332">Když se připojí, odpojí se a OnReconnected se zavolají.</span><span class="sxs-lookup"><span data-stu-id="29d7d-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="29d7d-333">Pokaždé, když prohlížeč přejde na novou stránku, je nutné vytvořit nové připojení, což znamená, že signál spustí metodu `OnDisconnected` následovanou metodou `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="29d7d-334">Při navázání nového připojení se signálem vždy vytvoří nové ID připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="29d7d-335">Metoda `OnReconnected` se volá, když se dokončí dočasná přerušení připojení, na které se může signál automaticky zotavit, například když se kabel dočasně odpojí a znovu připojí před vypršením časového limitu připojení. Metoda `OnDisconnected` je volána, když je klient odpojen a uživatel se nemůže automaticky znovu připojit, například když prohlížeč přejde na novou stránku.</span><span class="sxs-lookup"><span data-stu-id="29d7d-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="29d7d-336">Proto je možné posloupnost událostí pro daného klienta `OnConnected`, `OnReconnected``OnDisconnected`; nebo `OnConnected``OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="29d7d-337">Pro dané připojení se nezobrazí `OnConnected`sekvence, `OnDisconnected``OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="29d7d-338">Metoda `OnDisconnected` se v některých scénářích nevolá, například když dojde k výpadku serveru nebo pokud se doména aplikace recykluje.</span><span class="sxs-lookup"><span data-stu-id="29d7d-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="29d7d-339">Když je na řádku nebo v doméně aplikace dokončená recyklace jiného serveru, můžou se někteří klienti moci znovu připojit a spustit událost `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="29d7d-340">Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení v nástroji Signal](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="29d7d-341">Stav volajícího není naplněný.</span><span class="sxs-lookup"><span data-stu-id="29d7d-341">Caller state not populated</span></span>

<span data-ttu-id="29d7d-342">Metody obslužné rutiny události doby života připojení jsou volány ze serveru, což znamená, že všechny stavy, které umístíte do objektu `state` v klientovi, nebudou naplněny do vlastnosti `Caller` na serveru.</span><span class="sxs-lookup"><span data-stu-id="29d7d-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="29d7d-343">Informace o objektu `state` a vlastnosti `Caller` naleznete v tématu [jak předat stav mezi klienty a třídou centra](#passstate) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="29d7d-344">Jak získat informace o klientovi z kontextové vlastnosti</span><span class="sxs-lookup"><span data-stu-id="29d7d-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="29d7d-345">Chcete-li získat informace o klientovi, použijte vlastnost `Context` třídy centra.</span><span class="sxs-lookup"><span data-stu-id="29d7d-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="29d7d-346">Vlastnost `Context` vrátí objekt [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) , který poskytuje přístup k následujícím informacím:</span><span class="sxs-lookup"><span data-stu-id="29d7d-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="29d7d-347">ID připojení volajícího klienta.</span><span class="sxs-lookup"><span data-stu-id="29d7d-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="29d7d-348">ID připojení je identifikátor GUID, který je přiřazený signálem (hodnotu nemůžete zadat ve svém vlastním kódu).</span><span class="sxs-lookup"><span data-stu-id="29d7d-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="29d7d-349">Pro každé připojení existuje jedno ID připojení a stejné ID připojení se používá pro všechna centra, pokud máte ve své aplikaci více rozbočovačů.</span><span class="sxs-lookup"><span data-stu-id="29d7d-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="29d7d-350">Data hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="29d7d-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="29d7d-351">Můžete také získat hlavičku protokolu HTTP z `Context.Headers`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="29d7d-352">Důvodem pro více odkazů na stejnou věc je, že nejprve byl vytvořen `Context.Headers`, byla vlastnost `Context.Request` přidána později a `Context.Headers` byla zachována z důvodu zpětné kompatibility.</span><span class="sxs-lookup"><span data-stu-id="29d7d-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="29d7d-353">Dotaz na data řetězce.</span><span class="sxs-lookup"><span data-stu-id="29d7d-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="29d7d-354">Můžete také získat data řetězce dotazu z `Context.QueryString`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="29d7d-355">Řetězec dotazu, který získáte v této vlastnosti, je ten, který se použil s požadavkem HTTP, který vytvořil připojení k signalizaci.</span><span class="sxs-lookup"><span data-stu-id="29d7d-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="29d7d-356">Můžete přidat parametry řetězce dotazu do klienta nakonfigurováním připojení, což je pohodlný způsob, jak předat data o klientovi z klienta na server.</span><span class="sxs-lookup"><span data-stu-id="29d7d-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="29d7d-357">Následující příklad ukazuje jeden ze způsobů, jak přidat řetězec dotazu v klientovi jazyka JavaScript při použití vygenerovaného proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="29d7d-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="29d7d-358">Další informace o nastavení parametrů řetězce dotazu najdete v příručkách k rozhraní API pro klienty [JavaScriptu](index.md) a [.NET](index.md) .</span><span class="sxs-lookup"><span data-stu-id="29d7d-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="29d7d-359">Metodu přenosu, která se používá pro připojení v datech řetězce dotazu, můžete najít spolu s jinými hodnotami, které interně používají signály:</span><span class="sxs-lookup"><span data-stu-id="29d7d-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="29d7d-360">Hodnota `transportMethod` bude "WebSockets", "serverSentEvents", "foreverFrame" nebo "longPolling".</span><span class="sxs-lookup"><span data-stu-id="29d7d-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="29d7d-361">Všimněte si, že pokud zaškrtnete tuto hodnotu v metodě obslužné rutiny události `OnConnected`, může v některých scénářích zpočátku získat přenosovou hodnotu, která není koncovým vysjednaným způsobem přenosu pro připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="29d7d-362">V takovém případě metoda vyvolá výjimku a bude volána později po navázání finální metody přenosu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="29d7d-363">Soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="29d7d-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="29d7d-364">Soubory cookie můžete také získat z `Context.RequestCookies`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="29d7d-365">Informace o uživateli.</span><span class="sxs-lookup"><span data-stu-id="29d7d-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="29d7d-366">Objekt HttpContext pro požadavek:</span><span class="sxs-lookup"><span data-stu-id="29d7d-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="29d7d-367">Místo `HttpContext.Current` k získání `HttpContext` objektu pro připojení k signalizaci použijte tuto metodu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="29d7d-368">Postup předání stavu mezi klienty a třídou centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="29d7d-369">Klient proxy serveru poskytuje objekt `state`, ve kterém můžete ukládat data, která chcete přenést na server, pomocí jednotlivých volání metody.</span><span class="sxs-lookup"><span data-stu-id="29d7d-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="29d7d-370">Na serveru můžete získat přístup k těmto datům ve vlastnosti `Clients.Caller` v metodách centra, které jsou volány klienty.</span><span class="sxs-lookup"><span data-stu-id="29d7d-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="29d7d-371">Vlastnost `Clients.Caller` není vyplněna pro metody obslužné rutiny události doby života připojení `OnConnected`, `OnDisconnected`a `OnReconnected`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="29d7d-372">Vytváření a aktualizace dat v objektu `state` a vlastnost `Clients.Caller` funguje v obou směrech.</span><span class="sxs-lookup"><span data-stu-id="29d7d-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="29d7d-373">Hodnoty na serveru můžete aktualizovat a předávat je zpátky klientovi.</span><span class="sxs-lookup"><span data-stu-id="29d7d-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="29d7d-374">Následující příklad ukazuje kód klienta JavaScriptu, který ukládá stav pro přenos do serveru při každém volání metody.</span><span class="sxs-lookup"><span data-stu-id="29d7d-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="29d7d-375">Následující příklad ukazuje ekvivalentní kód v klientovi .NET.</span><span class="sxs-lookup"><span data-stu-id="29d7d-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="29d7d-376">Ve třídě centra máte přístup k těmto datům ve vlastnosti `Clients.Caller`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="29d7d-377">Následující příklad ukazuje kód, který načte stav uvedený v předchozím příkladu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="29d7d-378">Tento mechanismus pro trvalý stav není určený pro velké objemy dat, protože vše, co vložíte do vlastnosti `state` nebo `Clients.Caller`, je Round-Trip s každým voláním metody.</span><span class="sxs-lookup"><span data-stu-id="29d7d-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="29d7d-379">Je vhodný pro menší položky, jako jsou uživatelská jména nebo čítače.</span><span class="sxs-lookup"><span data-stu-id="29d7d-379">It's useful for smaller items such as user names or counters.</span></span>

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="29d7d-380">Jak zpracovávat chyby ve třídě centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="29d7d-381">Chcete-li zpracovat chyby, ke kterým dochází v metodách vaší třídy centra, použijte jednu nebo obě následující metody:</span><span class="sxs-lookup"><span data-stu-id="29d7d-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="29d7d-382">Zabalte kód metody v blocích try-catch a Zaprotokolujte objekt výjimky.</span><span class="sxs-lookup"><span data-stu-id="29d7d-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="29d7d-383">Pro účely ladění můžete výjimku odeslat klientovi, ale z bezpečnostních důvodů, které odesílají podrobné informace klientům v produkčním prostředí, se nedoporučuje.</span><span class="sxs-lookup"><span data-stu-id="29d7d-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="29d7d-384">Vytvořte modul kanálu centra, který zpracovává metodu [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="29d7d-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="29d7d-385">Následující příklad ukazuje modul kanálu, který protokoluje chyby, následovaný kódem v Global. asax, který vloží modul do kanálu rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="29d7d-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="29d7d-386">Další informace o modulech kanálu centra najdete v tématu [Postup přizpůsobení kanálu centra](#hubpipeline) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="29d7d-387">Jak povolit trasování</span><span class="sxs-lookup"><span data-stu-id="29d7d-387">How to enable tracing</span></span>

<span data-ttu-id="29d7d-388">Chcete-li povolit trasování na straně serveru, přidejte do souboru Web. config prvek System. Diagnostics, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="29d7d-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="29d7d-389">Při spuštění aplikace v aplikaci Visual Studio můžete zobrazit protokoly v okně **výstup** .</span><span class="sxs-lookup"><span data-stu-id="29d7d-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="29d7d-390">Jak volat klientské metody a spravovat skupiny mimo třídu centra</span><span class="sxs-lookup"><span data-stu-id="29d7d-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="29d7d-391">Chcete-li volat metody klienta z jiné třídy než vaší třídy centra, získejte odkaz na objekt kontextu signálu pro centrum a použijte jej ke volání metod v klientovi nebo správě skupin.</span><span class="sxs-lookup"><span data-stu-id="29d7d-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="29d7d-392">Následující vzorová `StockTicker` Třída získá objekt kontextu, uloží ho do instance třídy, uloží instanci třídy do statické vlastnosti a použije kontext z instance třídy singleton k volání metody `updateStockPrice` na klientech, kteří jsou připojení k centru s názvem `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="29d7d-393">Pokud je třeba v dlouhodobém objektu použít kontext vícekrát, získejte odkaz a uložte ho místo pokaždé, když ho budete potřebovat znovu.</span><span class="sxs-lookup"><span data-stu-id="29d7d-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="29d7d-394">Když se kontext získá, zajistíte tak, že signál klientům pošle zprávy ve stejném pořadí, ve kterém vaše metody rozbočovače provedou vyvolání metod klienta.</span><span class="sxs-lookup"><span data-stu-id="29d7d-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="29d7d-395">Kurz, ve kterém se dozvíte, jak používat kontext signalizace pro centrum, najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal](index.md).</span><span class="sxs-lookup"><span data-stu-id="29d7d-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="29d7d-396">Volání metod klienta</span><span class="sxs-lookup"><span data-stu-id="29d7d-396">Calling client methods</span></span>

<span data-ttu-id="29d7d-397">Můžete určit, kteří klienti obdrží RPC, ale máte méně možností než při volání z třídy centra.</span><span class="sxs-lookup"><span data-stu-id="29d7d-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="29d7d-398">Důvodem je, že kontext není přidružen ke konkrétnímu volání z klienta, takže žádné metody, které vyžadují znalosti aktuálního ID připojení, například `Clients.Others`nebo `Clients.Caller`nebo `Clients.OthersInGroup`, nejsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="29d7d-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="29d7d-399">K dispozici jsou následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="29d7d-399">The following options are available:</span></span>

- <span data-ttu-id="29d7d-400">Všichni připojení klienti.</span><span class="sxs-lookup"><span data-stu-id="29d7d-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="29d7d-401">Konkrétní klient identifikovaný IDENTIFIKÁTORem připojení.</span><span class="sxs-lookup"><span data-stu-id="29d7d-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="29d7d-402">Všichni připojení klienti s výjimkou určených klientů identifikovaných IDENTIFIKÁTORem připojení</span><span class="sxs-lookup"><span data-stu-id="29d7d-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="29d7d-403">Všichni připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="29d7d-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="29d7d-404">Všechny připojené klienty v zadané skupině s výjimkou určených klientů identifikovaných podle ID připojení</span><span class="sxs-lookup"><span data-stu-id="29d7d-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="29d7d-405">Pokud voláte do nehub třídy z metod ve třídě centra, můžete předat aktuální ID připojení a použít ho pomocí `Clients.Client`, `Clients.AllExcept`nebo `Clients.Group` pro simulaci `Clients.Caller`, `Clients.Others`nebo `Clients.OthersInGroup`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="29d7d-406">V následujícím příkladu třída `MoveShapeHub` předá ID připojení ke třídě `Broadcaster`, aby třída `Broadcaster` mohla simulovat `Clients.Others`.</span><span class="sxs-lookup"><span data-stu-id="29d7d-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="29d7d-407">Správa členství ve skupinách</span><span class="sxs-lookup"><span data-stu-id="29d7d-407">Managing group membership</span></span>

<span data-ttu-id="29d7d-408">Pro správu skupin máte stejné možnosti jako v rámci třídy centra.</span><span class="sxs-lookup"><span data-stu-id="29d7d-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="29d7d-409">Přidání klienta do skupiny</span><span class="sxs-lookup"><span data-stu-id="29d7d-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="29d7d-410">Odebrání klienta ze skupiny</span><span class="sxs-lookup"><span data-stu-id="29d7d-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="29d7d-411">Postup přizpůsobení kanálu Center</span><span class="sxs-lookup"><span data-stu-id="29d7d-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="29d7d-412">Signaler umožňuje vložit do kanálu rozbočovače vlastní kód.</span><span class="sxs-lookup"><span data-stu-id="29d7d-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="29d7d-413">Následující příklad ukazuje vlastní modul kanálů rozbočovače, který protokoluje každé volání příchozí metody přijaté z klienta a odchozí volání metody vyvolané na klientovi:</span><span class="sxs-lookup"><span data-stu-id="29d7d-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="29d7d-414">Následující kód v souboru *Global. asax* registruje modul, který se má spustit v kanálu centra:</span><span class="sxs-lookup"><span data-stu-id="29d7d-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="29d7d-415">Existuje mnoho různých metod, které lze přepsat.</span><span class="sxs-lookup"><span data-stu-id="29d7d-415">There are many different methods that you can override.</span></span> <span data-ttu-id="29d7d-416">Úplný seznam naleznete v tématu [metody HubPipelineModule](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="29d7d-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
