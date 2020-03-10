---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: Průvodce rozhraním API rozbočovače 1. x – klient JavaScriptu | Microsoft Docs
author: bradygaster
description: V tomto dokumentu najdete Úvod k používání rozhraní API centra pro Signal verze 1,1 v klientech JavaScript, jako jsou prohlížeče a Windows Store (WinJS) APPLIC...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 24850fe5229490bf600e09ad4718abb575a845fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536440"
---
# <a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="c388a-103">Pokyny k rozhraní API center SignalR 1.x – javascriptový klient</span><span class="sxs-lookup"><span data-stu-id="c388a-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>

<span data-ttu-id="c388a-104">autorem [Fletcher](https://github.com/pfletcher), který [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c388a-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c388a-105">V tomto dokumentu najdete Úvod k používání rozhraní API centra pro Signal verze 1,1 v klientech JavaScript, jako jsou prohlížeče a aplikace Windows Store (WinJS).</span><span class="sxs-lookup"><span data-stu-id="c388a-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="c388a-106">Rozhraní API pro centra signalizace vám umožní provádět Vzdálená volání procedur (RPC) ze serveru pro připojené klienty a klienty na server.</span><span class="sxs-lookup"><span data-stu-id="c388a-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="c388a-107">V kódu serveru můžete definovat metody, které mohou být volány klienty, a volat metody, které jsou spouštěny v klientovi.</span><span class="sxs-lookup"><span data-stu-id="c388a-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="c388a-108">V kódu klienta definujete metody, které mohou být volány ze serveru, a voláte metody, které jsou spuštěny na serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="c388a-109">Signalizace postará o všechny instalace klienta na server za vás.</span><span class="sxs-lookup"><span data-stu-id="c388a-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="c388a-110">Nástroj Signal také nabízí nižší úroveň rozhraní API označované jako trvalá připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="c388a-111">Úvod do nástroje pro signalizaci, centra a trvalá připojení nebo v kurzu, který ukazuje, jak sestavit kompletní aplikaci signalizace, najdete v tématu [signaler-Začínáme](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="c388a-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="c388a-112">Přehled</span><span class="sxs-lookup"><span data-stu-id="c388a-112">Overview</span></span>

<span data-ttu-id="c388a-113">Tento dokument obsahuje následující části:</span><span class="sxs-lookup"><span data-stu-id="c388a-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="c388a-114">Vygenerovaný proxy server a k čemu</span><span class="sxs-lookup"><span data-stu-id="c388a-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="c388a-115">Kdy použít generovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="c388a-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="c388a-116">Instalace klienta</span><span class="sxs-lookup"><span data-stu-id="c388a-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="c388a-117">Postup odkazu na dynamicky generovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="c388a-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="c388a-118">Jak vytvořit fyzický soubor pro proxy vygenerovaný signálem</span><span class="sxs-lookup"><span data-stu-id="c388a-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="c388a-119">Jak navázat připojení</span><span class="sxs-lookup"><span data-stu-id="c388a-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="c388a-120">$. Connection. hub je stejný objekt, který vytváří $. hubConnection ().</span><span class="sxs-lookup"><span data-stu-id="c388a-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="c388a-121">Asynchronní provádění metody Start</span><span class="sxs-lookup"><span data-stu-id="c388a-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="c388a-122">Jak navázat připojení mezi doménami</span><span class="sxs-lookup"><span data-stu-id="c388a-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="c388a-123">Konfigurace připojení</span><span class="sxs-lookup"><span data-stu-id="c388a-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="c388a-124">Určení parametrů řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="c388a-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="c388a-125">Určení způsobu přenosu</span><span class="sxs-lookup"><span data-stu-id="c388a-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="c388a-126">Jak získat proxy pro třídu centra</span><span class="sxs-lookup"><span data-stu-id="c388a-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="c388a-127">Jak definovat metody v klientovi, které může server volat</span><span class="sxs-lookup"><span data-stu-id="c388a-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="c388a-128">Postup volání metod serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="c388a-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="c388a-129">Postup zpracování událostí životního cyklu připojení</span><span class="sxs-lookup"><span data-stu-id="c388a-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="c388a-130">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="c388a-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="c388a-131">Postup povolení protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="c388a-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="c388a-132">Dokumentaci k programování serveru nebo klientů rozhraní .NET najdete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="c388a-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="c388a-133">Průvodce rozhraním API pro centra signálů – Server</span><span class="sxs-lookup"><span data-stu-id="c388a-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="c388a-134">Průvodce rozhraním API pro centra signálů – klient .NET</span><span class="sxs-lookup"><span data-stu-id="c388a-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="c388a-135">Odkazy na referenční témata rozhraní API odkazují na verzi rozhraní API .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="c388a-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="c388a-136">Pokud používáte .NET 4, přečtěte si téma věnované [verzi rozhraní API rozhraní .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="c388a-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="c388a-137">Vygenerovaný proxy server a k čemu</span><span class="sxs-lookup"><span data-stu-id="c388a-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="c388a-138">Můžete programovat klienta JavaScriptu ke komunikaci se službou signalizace s nebo bez proxy serveru, který vygeneroval signál.</span><span class="sxs-lookup"><span data-stu-id="c388a-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="c388a-139">K čemu je proxy pro vás jednodušší syntaxe kódu, který používáte k připojení, zápisu metod, které server volá, a volání metod na serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="c388a-140">Při psaní kódu pro volání metod serveru, vygenerovaný proxy vám umožní použít syntaxi, která vypadá jako při provádění místní funkce: můžete napsat `serverMethod(arg1, arg2)` místo `invoke('serverMethod', arg1, arg2)`.</span><span class="sxs-lookup"><span data-stu-id="c388a-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="c388a-141">Syntaxe vygenerovaného proxy serveru také umožňuje okamžitou a srozumitelnou chybu na straně klienta, pokud zadáte chybné zadání názvu metody serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="c388a-142">A pokud ručně vytvoříte soubor, který definuje proxy, můžete také získat podporu technologie IntelliSense pro psaní kódu, který volá metody serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="c388a-143">Předpokládejme například, že máte na serveru následující třídu centra:</span><span class="sxs-lookup"><span data-stu-id="c388a-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="c388a-144">Následující příklady kódu ukazují, jaký kód jazyka JavaScript vypadá za vyvolání metody `NewContosoChatMessage` na serveru a přijímání vyvolání `addContosoChatMessageToPage` metody ze serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="c388a-145">**S vygenerovaným proxy serverem**</span><span class="sxs-lookup"><span data-stu-id="c388a-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="c388a-146">**Bez vygenerovaného proxy**</span><span class="sxs-lookup"><span data-stu-id="c388a-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="c388a-147">Kdy použít generovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="c388a-147">When to use the generated proxy</span></span>

<span data-ttu-id="c388a-148">Pokud chcete registrovat více obslužných rutin událostí pro metodu klienta, kterou server volá, nemůžete použít vygenerovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="c388a-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="c388a-149">V opačném případě můžete zvolit používání vygenerovaného proxy serveru nebo ne na základě předvolby kódování.</span><span class="sxs-lookup"><span data-stu-id="c388a-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="c388a-150">Pokud se rozhodnete, že ji nepoužíváte, nemusíte odkazovat na adresu URL "signaler/Hubs" v prvku `script` ve vašem klientském kódu.</span><span class="sxs-lookup"><span data-stu-id="c388a-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="c388a-151">Instalace klienta</span><span class="sxs-lookup"><span data-stu-id="c388a-151">Client setup</span></span>

<span data-ttu-id="c388a-152">JavaScriptový klient vyžaduje odkazy na jQuery a základní soubor JavaScriptu pro signál.</span><span class="sxs-lookup"><span data-stu-id="c388a-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="c388a-153">Verze jQuery musí být 1.6.4 nebo hlavní novější verze, jako je například 1.7.2, 1.8.2 nebo 1.9.1.</span><span class="sxs-lookup"><span data-stu-id="c388a-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="c388a-154">Pokud se rozhodnete použít vygenerovaný proxy server, budete také potřebovat odkaz na soubor JavaScriptu proxy vygenerovaný signálem.</span><span class="sxs-lookup"><span data-stu-id="c388a-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="c388a-155">Následující příklad ukazuje, jak odkazy mohou vypadat jako na stránce HTML, která používá vygenerovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="c388a-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="c388a-156">Tyto odkazy musí být zahrnuté v tomto pořadí: jQuery First, Signal Core po tomto případě a proxy signalizace jako poslední.</span><span class="sxs-lookup"><span data-stu-id="c388a-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="c388a-157">Postup odkazu na dynamicky generovaný proxy server</span><span class="sxs-lookup"><span data-stu-id="c388a-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="c388a-158">V předchozím příkladu odkazuje odkaz na proxy server vygenerovaný signálem k dynamickému generování kódu JavaScriptu, nikoli fyzického souboru.</span><span class="sxs-lookup"><span data-stu-id="c388a-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="c388a-159">Návěstí vytvoří kód JavaScriptu pro proxy a zachová ho klientovi v reakci na adresu URL "/SignalR/Hubs".</span><span class="sxs-lookup"><span data-stu-id="c388a-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="c388a-160">Pokud jste zadali jinou základní adresu URL pro připojení k signalizaci na serveru v metodě `MapHubs`, adresa URL dynamicky generovaného souboru proxy je vaše vlastní adresa URL s připojeným "/Hubs".</span><span class="sxs-lookup"><span data-stu-id="c388a-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="c388a-161">Pro klienty se systémem Windows 8 (Windows Store) v jazyce JavaScript použijte místo dynamicky generovaného souboru fyzický proxy soubor.</span><span class="sxs-lookup"><span data-stu-id="c388a-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="c388a-162">Další informace najdete v části [Postup vytvoření fyzického souboru pro proxy vygenerovaný signálem](#manualproxy) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="c388a-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="c388a-163">V zobrazení ASP.NET MVC 4 Razor použijte vlnovku pro odkaz na kořen aplikace v referenčním souboru proxy:</span><span class="sxs-lookup"><span data-stu-id="c388a-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="c388a-164">Další informace o použití signalizace v MVC 4 najdete v tématu [Začínáme s nástrojem Signal a MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="c388a-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="c388a-165">V zobrazení ASP.NET MVC 3 Razor použijte `Url.Content` pro referenci proxy souboru:</span><span class="sxs-lookup"><span data-stu-id="c388a-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="c388a-166">V aplikaci webových formulářů ASP.NET použijte `ResolveClientUrl` pro odkaz na soubor proxy a zaregistrujte ho prostřednictvím ovládacího prvku ScriptManager pomocí relativní cesty ke kořenu aplikace (počínaje vlnovkou tildy):</span><span class="sxs-lookup"><span data-stu-id="c388a-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="c388a-167">Jako obecné pravidlo použijte stejnou metodu pro zadání adresy URL "/SignalR/Hubs", kterou používáte pro soubory CSS nebo JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c388a-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="c388a-168">Pokud zadáte adresu URL bez použití tildy, v některých případech bude vaše aplikace správně fungovat při testování v aplikaci Visual Studio pomocí IIS Express, ale při nasazení na plnou službu IIS dojde k chybě 404.</span><span class="sxs-lookup"><span data-stu-id="c388a-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="c388a-169">Další informace naleznete v tématu **řešení odkazů na prostředky kořenové úrovně** ve [webových serverech v aplikaci Visual Studio pro webové projekty ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="c388a-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="c388a-170">Při spuštění webového projektu v aplikaci Visual Studio 2012 v režimu ladění a pokud jako prohlížeč používáte Internet Explorer, můžete zobrazit soubor proxy v **Průzkumník řešení** v části **dokumenty skriptu**, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="c388a-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![JavaScriptový soubor generovaný v JavaScriptu v Průzkumník řešení](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="c388a-172">Pokud chcete zobrazit obsah souboru, poklikejte na **rozbočovače**.</span><span class="sxs-lookup"><span data-stu-id="c388a-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="c388a-173">Pokud nepoužíváte sadu Visual Studio 2012 a Internet Explorer nebo pokud nejste v režimu ladění, můžete obsah souboru získat také tak, že přejdete na adresu URL/signalR/hubs.</span><span class="sxs-lookup"><span data-stu-id="c388a-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="c388a-174">Například pokud vaše lokalita běží na `http://localhost:56699`, v prohlížeči se podívejte na `http://localhost:56699/SignalR/hubs`.</span><span class="sxs-lookup"><span data-stu-id="c388a-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="c388a-175">Jak vytvořit fyzický soubor pro proxy vygenerovaný signálem</span><span class="sxs-lookup"><span data-stu-id="c388a-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="c388a-176">Jako alternativu k dynamicky vygenerovanému proxy serveru můžete vytvořit fyzický soubor, který má kód proxy a odkazovat na tento soubor.</span><span class="sxs-lookup"><span data-stu-id="c388a-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="c388a-177">To může být vhodné pro kontrolu nad ukládáním do mezipaměti nebo sdružování nebo pro získání IntelliSense při kódování volání do metod serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="c388a-178">Chcete-li vytvořit soubor proxy, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="c388a-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="c388a-179">Nainstalujte balíček NuGet [Microsoft. ASPNET. signaler. util](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) .</span><span class="sxs-lookup"><span data-stu-id="c388a-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="c388a-180">Otevřete příkazový řádek a přejděte do složky *nástroje* , která obsahuje soubor Signal. exe.</span><span class="sxs-lookup"><span data-stu-id="c388a-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="c388a-181">Složka nástroje je v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="c388a-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="c388a-182">Zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="c388a-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="c388a-183">Cesta k souboru *. dll* je obvykle složka *bin* ve složce projektu.</span><span class="sxs-lookup"><span data-stu-id="c388a-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="c388a-184">Tento příkaz vytvoří soubor s názvem *Server. js* ve stejné složce jako *Signal. exe*.</span><span class="sxs-lookup"><span data-stu-id="c388a-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="c388a-185">Vložte soubor *Server. js* do příslušné složky v projektu, přejmenujte jej podle potřeby pro vaši aplikaci a přidejte odkaz na něj místo odkazu "signál/rozbočovačé".</span><span class="sxs-lookup"><span data-stu-id="c388a-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="c388a-186">Jak navázat připojení</span><span class="sxs-lookup"><span data-stu-id="c388a-186">How to establish a connection</span></span>

<span data-ttu-id="c388a-187">Než budete moct navázat připojení, musíte vytvořit objekt připojení, vytvořit proxy server a zaregistrovat obslužné rutiny událostí pro metody, které je možné volat ze serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="c388a-188">Když jsou nastaveny obslužné rutiny proxy a událostí, navažte připojení voláním metody `start`.</span><span class="sxs-lookup"><span data-stu-id="c388a-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="c388a-189">Pokud používáte generovaný proxy server, nemusíte vytvářet objekt připojení ve vlastním kódu, protože vygenerovaný kód proxy to udělá za vás.</span><span class="sxs-lookup"><span data-stu-id="c388a-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="c388a-190">**Navázat připojení (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="c388a-191">**Navázat připojení (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="c388a-192">Vzorový kód pro připojení ke službě signalizace používá výchozí adresu URL "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="c388a-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="c388a-193">Informace o tom, jak zadat jinou základní adresu URL, najdete v tématu [Průvodce rozhraním API pro centra ASP.NET Signal-Server-adresa URL/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="c388a-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="c388a-194">Normálně zaregistrujete obslužné rutiny události před voláním metody `start` pro navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="c388a-195">Pokud chcete registrovat některé obslužné rutiny události po navázání připojení, můžete to provést, ale před voláním metody `start` je nutné zaregistrovat alespoň jednu obslužnou rutinu události.</span><span class="sxs-lookup"><span data-stu-id="c388a-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="c388a-196">Jedním z důvodů je, že v aplikaci může být mnoho Center, ale pokud se k jednomu z nich budete chtít používat jenom jednu z nich, nebudete chtít aktivovat `OnConnected` událost na každém centru.</span><span class="sxs-lookup"><span data-stu-id="c388a-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="c388a-197">Když je připojení navázáno, přítomnost metody klienta v proxy serveru rozbočovače je tím, co oznamuje signalizaci, aby aktivoval událost `OnConnected`.</span><span class="sxs-lookup"><span data-stu-id="c388a-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="c388a-198">Pokud nezaregistrujete žádné obslužné rutiny událostí před voláním metody `start`, budete moci vyvolat metody v centru, ale metoda `OnConnected` centra nebude volána a žádné metody klienta nebudou vyvolány ze serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="c388a-199">$. Connection. hub je stejný objekt, který vytváří $. hubConnection ().</span><span class="sxs-lookup"><span data-stu-id="c388a-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="c388a-200">Jak vidíte v příkladech, při použití generovaného proxy serveru `$.connection.hub` odkazuje na objekt připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="c388a-201">Jedná se o stejný objekt, který získáte voláním `$.hubConnection()`, když nepoužíváte generovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="c388a-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="c388a-202">Generovaný kód proxy vytvoří připojení za vás spuštěním následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="c388a-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Vytvoření připojení ve vygenerovaném souboru proxy](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="c388a-204">Pokud používáte vygenerovaný proxy server, můžete s `$.connection.hub` provádět cokoli, co můžete dělat s objektem připojení, když nepoužíváte vygenerovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="c388a-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="c388a-205">Asynchronní provádění metody Start</span><span class="sxs-lookup"><span data-stu-id="c388a-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="c388a-206">Metoda `start` se spouští asynchronně.</span><span class="sxs-lookup"><span data-stu-id="c388a-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="c388a-207">Vrací [odložený objekt jQuery](http://api.jquery.com/category/deferred-object/), což znamená, že můžete přidat funkce zpětného volání voláním metod, jako jsou `pipe`, `done`a `fail`.</span><span class="sxs-lookup"><span data-stu-id="c388a-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="c388a-208">Pokud máte kód, který chcete spustit po navázání spojení, jako je například volání metody serveru, vložte tento kód do funkce zpětného volání nebo jej zavolejte z funkce zpětného volání.</span><span class="sxs-lookup"><span data-stu-id="c388a-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="c388a-209">Metoda zpětného volání `.done` se spustí po navázání připojení a po jakémkoli kódu, který máte v metodě obslužné rutiny události `OnConnected` na serveru, se dokončí provádění.</span><span class="sxs-lookup"><span data-stu-id="c388a-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="c388a-210">Pokud vložíte příkaz "nyní připojeno" z předchozího příkladu jako další řádek kódu po volání metody `start` (ne ve zpětném volání `.done`), bude řádek `console.log` spuštěn před navázáním připojení, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="c388a-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Špatný způsob, jak napsat kód, který se spustí po navázání připojení](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="c388a-212">Jak navázat připojení mezi doménami</span><span class="sxs-lookup"><span data-stu-id="c388a-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="c388a-213">V případě, že prohlížeč načítá stránku z `http://contoso.com`, připojení k signalizaci je ve stejné doméně, v `http://contoso.com/signalr`.</span><span class="sxs-lookup"><span data-stu-id="c388a-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="c388a-214">Pokud stránka z `http://contoso.com` vytvoří připojení k `http://fabrikam.com/signalr`, což je připojení mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="c388a-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="c388a-215">Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázaná.</span><span class="sxs-lookup"><span data-stu-id="c388a-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="c388a-216">Pokud chcete vytvořit připojení mezi doménami, ujistěte se, že jsou na serveru povolená připojení mezi doménami, a při vytváření objektu připojení zadejte adresu URL připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="c388a-217">Signál bude používat vhodnou technologii pro připojení mezi doménami, jako třeba [JSONP](http://en.wikipedia.org/wiki/JSONP) nebo [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="c388a-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="c388a-218">Na serveru povolte připojení mezi doménami výběrem této možnosti při volání metody `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="c388a-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="c388a-219">Na straně klienta zadejte adresu URL při vytváření objektu připojení (bez vygenerovaného proxy serveru) nebo před voláním metody Start (s vygenerovaným proxy serverem).</span><span class="sxs-lookup"><span data-stu-id="c388a-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="c388a-220">**Kód klienta, který určuje připojení mezi doménami (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="c388a-221">**Kód klienta, který určuje připojení mezi doménami (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="c388a-222">Pokud použijete konstruktor `$.hubConnection`, nemusíte do adresy URL zahrnout `signalr`, protože se přidá automaticky (Pokud nezadáte `useDefaultUrl` jako `false`).</span><span class="sxs-lookup"><span data-stu-id="c388a-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="c388a-223">Můžete vytvořit více připojení k různým koncovým bodům.</span><span class="sxs-lookup"><span data-stu-id="c388a-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="c388a-224">Ve vašem kódu nenastavujte `jQuery.support.cors` na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="c388a-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![Nenastavujte jQuery. support. Cors na hodnotu true](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="c388a-226">Návěstí zpracovává použití JSONP nebo CORS.</span><span class="sxs-lookup"><span data-stu-id="c388a-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="c388a-227">Nastavením `jQuery.support.cors` na hodnotu true zakážete JSONP, protože to způsobuje, že signál bude předpokládat, že prohlížeč podporuje CORS.</span><span class="sxs-lookup"><span data-stu-id="c388a-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="c388a-228">Pokud se připojujete k adrese URL místního hostitele, Internet Explorer 10 ji nepovažuje za připojení mezi doménami, takže aplikace bude fungovat místně s IE 10, a to i v případě, že jste na serveru nepovolili připojení mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="c388a-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="c388a-229">Informace o použití připojení mezi doménami s Internet Explorerem 9 najdete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span><span class="sxs-lookup"><span data-stu-id="c388a-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="c388a-230">Informace o použití připojení mezi doménami s Chrome najdete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span><span class="sxs-lookup"><span data-stu-id="c388a-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="c388a-231">Vzorový kód pro připojení ke službě signalizace používá výchozí adresu URL "/SignalR".</span><span class="sxs-lookup"><span data-stu-id="c388a-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="c388a-232">Informace o tom, jak zadat jinou základní adresu URL, najdete v tématu [Průvodce rozhraním API pro centra ASP.NET Signal-Server-adresa URL/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="c388a-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="c388a-233">Konfigurace připojení</span><span class="sxs-lookup"><span data-stu-id="c388a-233">How to configure the connection</span></span>

<span data-ttu-id="c388a-234">Před navázáním připojení můžete zadat parametry řetězce dotazu nebo zadat metodu přenosu.</span><span class="sxs-lookup"><span data-stu-id="c388a-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="c388a-235">Určení parametrů řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="c388a-235">How to specify query string parameters</span></span>

<span data-ttu-id="c388a-236">Pokud chcete při připojení klienta odesílat data na server, můžete do objektu připojení přidat parametry řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="c388a-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="c388a-237">Následující příklady ukazují, jak nastavit parametr řetězce dotazu v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="c388a-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="c388a-238">**Před voláním metody Start (s vygenerovaným proxy serverem) nastavte hodnotu řetězce dotazu.**</span><span class="sxs-lookup"><span data-stu-id="c388a-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="c388a-239">**Před voláním metody Start (bez vygenerovaného proxy serveru) nastavte hodnotu řetězce dotazu.**</span><span class="sxs-lookup"><span data-stu-id="c388a-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="c388a-240">Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="c388a-241">Určení způsobu přenosu</span><span class="sxs-lookup"><span data-stu-id="c388a-241">How to specify the transport method</span></span>

<span data-ttu-id="c388a-242">V rámci procesu připojování klient signalizace obvykle vyjednává se serverem, aby bylo možné určit nejlepší přenos, který je podporovaný oběma servery i klientem.</span><span class="sxs-lookup"><span data-stu-id="c388a-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="c388a-243">Pokud již víte, který přenos chcete použít, můžete tento proces vyjednávání obejít zadáním metody přenosu při volání metody `start`.</span><span class="sxs-lookup"><span data-stu-id="c388a-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="c388a-244">**Kód klienta, který určuje způsob přenosu (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="c388a-245">**Kód klienta, který určuje způsob přenosu (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="c388a-246">Jako alternativu můžete zadat více metod přenosu v pořadí, ve kterém chcete, aby je Signal mohl vyzkoušet:</span><span class="sxs-lookup"><span data-stu-id="c388a-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="c388a-247">**Kód klienta, který určuje vlastní záložní schéma přenosu (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="c388a-248">**Kód klienta, který určuje vlastní záložní schéma přenosu (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="c388a-249">K určení metody přenosu můžete použít následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="c388a-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="c388a-250">WebSockets</span><span class="sxs-lookup"><span data-stu-id="c388a-250">"webSockets"</span></span>
- <span data-ttu-id="c388a-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="c388a-251">"foreverFrame"</span></span>
- <span data-ttu-id="c388a-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="c388a-252">"serverSentEvents"</span></span>
- <span data-ttu-id="c388a-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="c388a-253">"longPolling"</span></span>

<span data-ttu-id="c388a-254">Následující příklady ukazují, jak zjistit, která metoda přenosu je používána připojením.</span><span class="sxs-lookup"><span data-stu-id="c388a-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="c388a-255">**Kód klienta, který zobrazuje přenosovou metodu používanou připojením (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="c388a-256">**Kód klienta, který zobrazuje přenosovou metodu používanou připojením (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="c388a-257">Informace o tom, jak zjistit způsob přenosu v serverovém kódu, najdete v tématu [Průvodce rozhraním API centra ASP.NET Signal-Server – jak z kontextové vlastnosti získat informace o klientovi](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="c388a-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="c388a-258">Další informace o přenosech a náhradních přenosech najdete v tématu [Úvod k signalizaci a záložním přenosům](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="c388a-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="c388a-259">Jak získat proxy pro třídu centra</span><span class="sxs-lookup"><span data-stu-id="c388a-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="c388a-260">Každý objekt připojení, který vytvoříte, zapouzdřuje informace o připojení ke službě signalizace, která obsahuje jednu nebo více tříd centra.</span><span class="sxs-lookup"><span data-stu-id="c388a-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="c388a-261">Aby bylo možné komunikovat s třídou centra, použijte proxy objekt, který můžete vytvořit sami (Pokud nepoužíváte generovaný proxy server), nebo který je vygenerován za vás.</span><span class="sxs-lookup"><span data-stu-id="c388a-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="c388a-262">Na straně klienta je názvem proxy verze ve stylu CamelCase-použita s názvem třídy centra.</span><span class="sxs-lookup"><span data-stu-id="c388a-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="c388a-263">Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="c388a-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="c388a-264">**Třída centra na serveru**</span><span class="sxs-lookup"><span data-stu-id="c388a-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="c388a-265">**Získat odkaz na vygenerovaný klientský proxy server pro centrum**</span><span class="sxs-lookup"><span data-stu-id="c388a-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="c388a-266">**Vytvoření klientského proxy serveru pro třídu centra (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="c388a-267">Pokud třídu centra seřadíte pomocí atributu `HubName`, použijte přesný název bez změny velikosti písmen.</span><span class="sxs-lookup"><span data-stu-id="c388a-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="c388a-268">**Třída centra na serveru s atributem HubName**</span><span class="sxs-lookup"><span data-stu-id="c388a-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="c388a-269">**Získat odkaz na vygenerovaný klientský proxy server pro centrum**</span><span class="sxs-lookup"><span data-stu-id="c388a-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="c388a-270">**Vytvoření klientského proxy serveru pro třídu centra (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="c388a-271">Jak definovat metody v klientovi, které může server volat</span><span class="sxs-lookup"><span data-stu-id="c388a-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="c388a-272">Chcete-li definovat metodu, kterou může server volat z centra, přidejte obslužnou rutinu události do proxy serveru centra pomocí vlastnosti `client` generovaného proxy serveru nebo volejte metodu `on`, pokud nepoužíváte generovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="c388a-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="c388a-273">Parametry mohou být složité objekty.</span><span class="sxs-lookup"><span data-stu-id="c388a-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="c388a-274">Přidejte obslužnou rutinu události před voláním metody `start` k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="c388a-275">(Pokud chcete přidat obslužné rutiny událostí po volání metody `start`, přečtěte si poznámku v tématu [jak navázat připojení](#establishconnection) dříve v tomto dokumentu a použít syntaxi zobrazenou pro definování metody bez použití vygenerovaného proxy serveru.)</span><span class="sxs-lookup"><span data-stu-id="c388a-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="c388a-276">Porovnávání názvů metod nerozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="c388a-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="c388a-277">Například `Clients.All.addContosoChatMessageToPage` na serveru spustí `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`nebo `addcontosochatmessagetopage` na klientovi.</span><span class="sxs-lookup"><span data-stu-id="c388a-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="c388a-278">**Definovat metodu na klientovi (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="c388a-279">**Alternativní způsob definování metody v klientovi (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="c388a-280">**Definovat metodu na klientovi (bez vygenerovaného proxy serveru nebo při přidání po volání metody Start)**</span><span class="sxs-lookup"><span data-stu-id="c388a-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="c388a-281">**Serverový kód, který volá metodu klienta**</span><span class="sxs-lookup"><span data-stu-id="c388a-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="c388a-282">Následující příklady zahrnují komplexní objekt jako parametr metody.</span><span class="sxs-lookup"><span data-stu-id="c388a-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="c388a-283">**Metoda define pro klienta, který přebírá složitý objekt (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="c388a-284">**Definovat metodu u klienta, který přebírá složitý objekt (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="c388a-285">**Kód serveru, který definuje komplexní objekt**</span><span class="sxs-lookup"><span data-stu-id="c388a-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="c388a-286">**Serverový kód, který volá metodu klienta pomocí složitého objektu**</span><span class="sxs-lookup"><span data-stu-id="c388a-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="c388a-287">Postup volání metod serveru z klienta</span><span class="sxs-lookup"><span data-stu-id="c388a-287">How to call server methods from the client</span></span>

<span data-ttu-id="c388a-288">Chcete-li volat metodu serveru z klienta, použijte vlastnost `server` vygenerovaného proxy serveru nebo metody `invoke` na serveru proxy centra, pokud nepoužíváte generovaný proxy server.</span><span class="sxs-lookup"><span data-stu-id="c388a-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="c388a-289">Návratová hodnota nebo parametry mohou být složité objekty.</span><span class="sxs-lookup"><span data-stu-id="c388a-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="c388a-290">Předejte ve stylu CamelCase verzi názvu metody v centru.</span><span class="sxs-lookup"><span data-stu-id="c388a-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="c388a-291">Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="c388a-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="c388a-292">Následující příklady ukazují, jak zavolat metodu serveru, která nemá návratovou hodnotu a jak zavolat metodu serveru, která má návratovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="c388a-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="c388a-293">**Metoda serveru bez atributu HubMethodName**</span><span class="sxs-lookup"><span data-stu-id="c388a-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="c388a-294">**Serverový kód, který definuje složitý objekt předaný do parametru**</span><span class="sxs-lookup"><span data-stu-id="c388a-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="c388a-295">**Kód klienta, který vyvolá metodu serveru (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="c388a-296">**Kód klienta, který vyvolá metodu serveru (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="c388a-297">Pokud jste upravili metodu centra s atributem `HubMethodName`, použijte tento název bez změny velikosti písmen.</span><span class="sxs-lookup"><span data-stu-id="c388a-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="c388a-298">**Metoda serveru** s atributem HubMethodName</span><span class="sxs-lookup"><span data-stu-id="c388a-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="c388a-299">**Kód klienta, který vyvolá metodu serveru (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="c388a-300">**Kód klienta, který vyvolá metodu serveru (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="c388a-301">Předchozí příklady ukazují, jak zavolat metodu serveru, která nemá žádnou návratovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="c388a-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="c388a-302">Následující příklady ukazují, jak zavolat metodu serveru, která má návratovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="c388a-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="c388a-303">**Serverový kód pro metodu, která má návratovou hodnotu**</span><span class="sxs-lookup"><span data-stu-id="c388a-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="c388a-304">**Skladová Třída použitá pro** návratovou hodnotu</span><span class="sxs-lookup"><span data-stu-id="c388a-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="c388a-305">**Kód klienta, který vyvolá metodu serveru (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="c388a-306">**Kód klienta, který vyvolá metodu serveru (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="c388a-307">Postup zpracování událostí životního cyklu připojení</span><span class="sxs-lookup"><span data-stu-id="c388a-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="c388a-308">Signál poskytuje následující události doby života připojení, které můžete zpracovat:</span><span class="sxs-lookup"><span data-stu-id="c388a-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="c388a-309">`starting`: je aktivována před odesláním dat prostřednictvím připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="c388a-310">`received`: Vyvolá se, když jsou v připojení přijata nějaká data.</span><span class="sxs-lookup"><span data-stu-id="c388a-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="c388a-311">Poskytuje přijatá data.</span><span class="sxs-lookup"><span data-stu-id="c388a-311">Provides the received data.</span></span>
- <span data-ttu-id="c388a-312">`connectionSlow`: Vyvolá se, když klient zjistí pomalé nebo často vyřazování připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="c388a-313">`reconnecting`: Vyvolá se, když se zahájí opětovné připojení podkladového přenosu.</span><span class="sxs-lookup"><span data-stu-id="c388a-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="c388a-314">`reconnected`: Vyvolá se, když se znovu připojí příslušný přenos.</span><span class="sxs-lookup"><span data-stu-id="c388a-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="c388a-315">`stateChanged`: Vyvolá se při změně stavu připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="c388a-316">Poskytuje starý stav a nový stav (připojení, připojení, opětovné připojení nebo odpojení).</span><span class="sxs-lookup"><span data-stu-id="c388a-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="c388a-317">`disconnected`: Vyvolá se, když se připojení odpojilo.</span><span class="sxs-lookup"><span data-stu-id="c388a-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="c388a-318">Například pokud chcete zobrazovat upozornění, pokud dojde k problémům s připojením, které by mohly způsobit znatelné zpoždění, zpracujte událost `connectionSlow`.</span><span class="sxs-lookup"><span data-stu-id="c388a-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="c388a-319">**Zpracování události connectionSlow (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="c388a-320">**Zpracování události connectionSlow (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="c388a-321">Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení v nástroji Signal](index.md).</span><span class="sxs-lookup"><span data-stu-id="c388a-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="c388a-322">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="c388a-322">How to handle errors</span></span>

<span data-ttu-id="c388a-323">Klient služby Signal JavaScript poskytuje `error` událost, pro kterou můžete přidat obslužnou rutinu pro.</span><span class="sxs-lookup"><span data-stu-id="c388a-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="c388a-324">Můžete také použít metodu selhání k přidání obslužné rutiny pro chyby, které jsou výsledkem vyvolání metody serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="c388a-325">Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který Signal vrátí po chybě, obsahuje minimální informace o chybě.</span><span class="sxs-lookup"><span data-stu-id="c388a-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="c388a-326">Například pokud se volání `newContosoChatMessage` nepovede, chybová zpráva v objektu Error obsahuje "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" odesílání podrobných chybových zpráv klientům v produkčním prostředí se z bezpečnostních důvodů nedoporučuje, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.</span><span class="sxs-lookup"><span data-stu-id="c388a-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="c388a-327">Následující příklad ukazuje, jak přidat obslužnou rutinu pro událost Error.</span><span class="sxs-lookup"><span data-stu-id="c388a-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="c388a-328">**Přidání obslužné rutiny chyb (s vygenerovaným proxy serverem)**</span><span class="sxs-lookup"><span data-stu-id="c388a-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="c388a-329">**Přidání obslužné rutiny chyb (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="c388a-330">Následující příklad ukazuje, jak zpracovat chybu z vyvolání metody.</span><span class="sxs-lookup"><span data-stu-id="c388a-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="c388a-331">**Zpracování chyby z vyvolání metody (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="c388a-332">**Zpracování chyby od vyvolání metody (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="c388a-333">Pokud se volání metody nezdařilo, je vyvolána také událost `error`, takže váš kód v obslužné rutině metody `error` a ve zpětném volání metody `.fail` by se spustil.</span><span class="sxs-lookup"><span data-stu-id="c388a-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="c388a-334">Postup povolení protokolování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="c388a-334">How to enable client-side logging</span></span>

<span data-ttu-id="c388a-335">Chcete-li povolit protokolování na straně klienta pro připojení, nastavte vlastnost `logging` objektu Connection před voláním metody `start` k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="c388a-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="c388a-336">**Povolit protokolování (u generovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="c388a-337">**Povolit protokolování (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="c388a-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="c388a-338">Protokoly zobrazíte tak, že otevřete vývojářské nástroje v prohlížeči a přejdete na kartu konzola. Kurz, který obsahuje podrobné pokyny a snímky obrazovky, které ukazují, jak to udělat, najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal – povolení protokolování](index.md).</span><span class="sxs-lookup"><span data-stu-id="c388a-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
