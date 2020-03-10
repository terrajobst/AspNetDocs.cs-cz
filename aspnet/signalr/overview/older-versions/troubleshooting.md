---
uid: signalr/overview/older-versions/troubleshooting
title: Poradce při potížích (Signaler 1. x) | Microsoft Docs
author: bradygaster
description: Tento článek popisuje běžné problémy s vývojem aplikací pro signalizaci.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579602"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="950c0-103">Řešení potíží s knihovnou SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="950c0-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="950c0-104">Po [Fletcheru](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="950c0-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="950c0-105">Tento dokument popisuje běžné problémy s odstraňováním potíží s nástrojem Signal.</span><span class="sxs-lookup"><span data-stu-id="950c0-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="950c0-106">Tento dokument obsahuje následující oddíly.</span><span class="sxs-lookup"><span data-stu-id="950c0-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="950c0-107">Volající metody mezi klientem a serverem selžou</span><span class="sxs-lookup"><span data-stu-id="950c0-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="950c0-108">Další problémy s připojením</span><span class="sxs-lookup"><span data-stu-id="950c0-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="950c0-109">Kompilace a chyby na straně serveru</span><span class="sxs-lookup"><span data-stu-id="950c0-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="950c0-110">Problémy se sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="950c0-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="950c0-111">Problémy s Internetová informační služba</span><span class="sxs-lookup"><span data-stu-id="950c0-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="950c0-112">Problémy s Azure</span><span class="sxs-lookup"><span data-stu-id="950c0-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="950c0-113">Volající metody mezi klientem a serverem selžou</span><span class="sxs-lookup"><span data-stu-id="950c0-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="950c0-114">Tato část popisuje možné příčiny selhání volání metody mezi klientem a serverem bez smysluplné chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="950c0-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="950c0-115">V aplikaci signalizace nemá server žádné informace o metodách, které klient implementuje; Když server vyvolá metodu klienta, je do klienta zaslána data názvu metody a parametru a metoda je provedena pouze v případě, že existuje ve formátu, který je zadán serverem.</span><span class="sxs-lookup"><span data-stu-id="950c0-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="950c0-116">Pokud se v klientovi nenajde žádná vyhovující metoda, nic se nestane a na serveru se nevyvolá žádná chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="950c0-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="950c0-117">Chcete-li dále prozkoumat klientské metody, které nejsou volány, můžete zapnout protokolování před voláním metody Start na rozbočovači, aby bylo možné zjistit, jaká volání pocházejí ze serveru.</span><span class="sxs-lookup"><span data-stu-id="950c0-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="950c0-118">Chcete-li povolit protokolování v aplikaci JavaScriptu, přečtěte si téma [Jak povolit protokolování na straně klienta (verze klienta JavaScript)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="950c0-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="950c0-119">Chcete-li povolit protokolování v klientské aplikaci .NET, přečtěte si téma [Jak povolit protokolování na straně klienta (verze klienta rozhraní .NET)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span><span class="sxs-lookup"><span data-stu-id="950c0-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="950c0-120">Nesprávně napsaná metoda, nesprávný podpis metody nebo nesprávný název centra</span><span class="sxs-lookup"><span data-stu-id="950c0-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="950c0-121">Pokud se název nebo signatura volané metody přesně neshoduje s odpovídající metodou na klientovi, volání se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="950c0-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="950c0-122">Ověřte, že název metody, který je volán serverem, odpovídá názvu metody v klientovi.</span><span class="sxs-lookup"><span data-stu-id="950c0-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="950c0-123">Také signál vytvoří rozbočovač proxy pomocí metod ve stylu CamelCase-použita, jak je to vhodné v JavaScriptu, takže metoda nazvaná `SendMessage` na serveru by se volala `sendMessage` na klientském proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="950c0-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="950c0-124">Použijete-li v kódu na straně serveru atribut `HubName`, ověřte, zda se používá název, který se shoduje s názvem použitým k vytvoření centra na klientovi.</span><span class="sxs-lookup"><span data-stu-id="950c0-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="950c0-125">Pokud nepoužijete atribut `HubName`, ověřte, zda je název centra v jazyce JavaScript ve stylu CamelCase-použita, jako je například chatHub namísto ChatHub.</span><span class="sxs-lookup"><span data-stu-id="950c0-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="950c0-126">Duplicitní název metody na klientovi</span><span class="sxs-lookup"><span data-stu-id="950c0-126">Duplicate method name on client</span></span>

<span data-ttu-id="950c0-127">Ověřte, že v klientovi nemáte duplicitní metodu, která se liší pouze velikostí písmen.</span><span class="sxs-lookup"><span data-stu-id="950c0-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="950c0-128">Pokud má vaše klientská aplikace metodu nazvanou `sendMessage`, ověřte také, že není k dispozici také metoda s názvem `SendMessage`.</span><span class="sxs-lookup"><span data-stu-id="950c0-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="950c0-129">Na klientovi chybí analyzátor JSON.</span><span class="sxs-lookup"><span data-stu-id="950c0-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="950c0-130">Návěstí vyžaduje, aby byl k dispozici analyzátor JSON pro serializaci volání mezi serverem a klientem.</span><span class="sxs-lookup"><span data-stu-id="950c0-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="950c0-131">Pokud váš klient nemá integrovaný analyzátor JSON (například Internet Explorer 7), budete ho muset zahrnout do aplikace.</span><span class="sxs-lookup"><span data-stu-id="950c0-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="950c0-132">Analyzátor JSON si můžete stáhnout [tady](http://nuget.org/packages/json2).</span><span class="sxs-lookup"><span data-stu-id="950c0-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="950c0-133">Kombinace centra a PersistentConnection syntaxe</span><span class="sxs-lookup"><span data-stu-id="950c0-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="950c0-134">Nástroj Signal používá dva komunikační modely: centra a PersistentConnections.</span><span class="sxs-lookup"><span data-stu-id="950c0-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="950c0-135">Syntaxe pro volání těchto dvou modelů komunikace je odlišná v kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="950c0-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="950c0-136">Pokud jste do svého serverového kódu přidali centrum, ověřte, že veškerý kód klienta používá správnou syntaxi centra.</span><span class="sxs-lookup"><span data-stu-id="950c0-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="950c0-137">**JavaScriptový kód klienta, který vytvoří PersistentConnection v klientovi JavaScriptu**</span><span class="sxs-lookup"><span data-stu-id="950c0-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="950c0-138">**JavaScriptový kód klienta, který vytvoří rozbočovač proxy v klientovi JavaScriptu**</span><span class="sxs-lookup"><span data-stu-id="950c0-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="950c0-139">**C#kód serveru, který mapuje trasu na PersistentConnection**</span><span class="sxs-lookup"><span data-stu-id="950c0-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="950c0-140">**C#serverový kód, který mapuje trasu na rozbočovač nebo na více Center v případě, že máte více aplikací**</span><span class="sxs-lookup"><span data-stu-id="950c0-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="950c0-141">Připojení začalo před přidáním předplatných.</span><span class="sxs-lookup"><span data-stu-id="950c0-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="950c0-142">Pokud se připojení k rozbočovači spustí před tím, než se do proxy serveru přidají metody, které je možné volat ze serveru, nebudou se přijímat zprávy.</span><span class="sxs-lookup"><span data-stu-id="950c0-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="950c0-143">Následující kód jazyka JavaScript nebude správně spustit centrum:</span><span class="sxs-lookup"><span data-stu-id="950c0-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="950c0-144">**Nesprávný kód klienta JavaScriptu, který nepovoluje příjem zpráv centra**</span><span class="sxs-lookup"><span data-stu-id="950c0-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="950c0-145">Místo toho přidejte předplatná metody před voláním Start:</span><span class="sxs-lookup"><span data-stu-id="950c0-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="950c0-146">**Kód klienta JavaScriptu, který správně přidá odběry do centra**</span><span class="sxs-lookup"><span data-stu-id="950c0-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="950c0-147">Chybí název metody na proxy hub.</span><span class="sxs-lookup"><span data-stu-id="950c0-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="950c0-148">Ověřte, zda je metoda definovaná na serveru přihlášena k odběru klienta.</span><span class="sxs-lookup"><span data-stu-id="950c0-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="950c0-149">I když Server definuje metodu, musí být stále přidaný do klientského proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="950c0-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="950c0-150">Metody lze do proxy serveru klienta přidat následujícími způsoby (Všimněte si, že metoda je přidána do `client`ho člena centra, nikoli přímo do centra):</span><span class="sxs-lookup"><span data-stu-id="950c0-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="950c0-151">**JavaScriptový kód klienta, který přidává metody do proxy serveru hub**</span><span class="sxs-lookup"><span data-stu-id="950c0-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="950c0-152">Metody centra nebo centra nejsou deklarované jako veřejné.</span><span class="sxs-lookup"><span data-stu-id="950c0-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="950c0-153">Aby bylo možné v klientovi zobrazit, musí být implementace a metody centra deklarovány jako `public`.</span><span class="sxs-lookup"><span data-stu-id="950c0-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="950c0-154">Přístup k centru z jiné aplikace</span><span class="sxs-lookup"><span data-stu-id="950c0-154">Accessing hub from a different application</span></span>

<span data-ttu-id="950c0-155">K centrům signálu se dá dostat jenom prostřednictvím aplikací, které implementují klienty signalizace.</span><span class="sxs-lookup"><span data-stu-id="950c0-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="950c0-156">Signál nemůže spolupracovat s jinými komunikačními knihovnami (jako jsou webové služby SOAP nebo WCF). Pokud není pro vaši cílovou platformu k dispozici žádný klient signalizace, nebudete moct přímo získat přístup ke koncovému bodu serveru.</span><span class="sxs-lookup"><span data-stu-id="950c0-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="950c0-157">Ruční serializace dat</span><span class="sxs-lookup"><span data-stu-id="950c0-157">Manually serializing data</span></span>

<span data-ttu-id="950c0-158">Signál k serializaci parametrů metody automaticky použije kód JSON – nemusíte to dělat sami.</span><span class="sxs-lookup"><span data-stu-id="950c0-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="950c0-159">Metoda vzdáleného rozbočovače se neprovádí u klienta v operaci odpojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="950c0-160">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="950c0-160">This behavior is by design.</span></span> <span data-ttu-id="950c0-161">Když je volána `OnDisconnected`, centrum již zadalo `Disconnected` stav, který neumožňuje volání dalších metod centra.</span><span class="sxs-lookup"><span data-stu-id="950c0-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="950c0-162">**C#kód serveru, který správně spustí kód v události odpojení**</span><span class="sxs-lookup"><span data-stu-id="950c0-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="950c0-163">Byl dosažen limit připojení</span><span class="sxs-lookup"><span data-stu-id="950c0-163">Connection limit reached</span></span>

<span data-ttu-id="950c0-164">Při použití plné verze služby IIS na klientském operačním systému, jako je Windows 7, se zavede limit 10 připojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="950c0-165">Pokud používáte klientský operační systém, použijte místo toho IIS Express k tomu, abyste se vyhnuli tomuto omezení.</span><span class="sxs-lookup"><span data-stu-id="950c0-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="950c0-166">Připojení mezi doménami není správně nastavené.</span><span class="sxs-lookup"><span data-stu-id="950c0-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="950c0-167">Pokud připojení mezi doménami (připojení, pro které není adresa URL signalizace ve stejné doméně jako hostující stránka), není nastavené správně, připojení může selhat bez chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="950c0-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="950c0-168">Informace o tom, jak povolit mezidoménovou komunikaci, najdete v tématu [jak vytvořit připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="950c0-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="950c0-169">Připojení pomocí protokolu NTLM (Active Directory) nefunguje v klientu .NET.</span><span class="sxs-lookup"><span data-stu-id="950c0-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="950c0-170">Připojení v klientské aplikaci .NET, které používá zabezpečení domény, může selhat, pokud připojení není správně nakonfigurováno.</span><span class="sxs-lookup"><span data-stu-id="950c0-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="950c0-171">Chcete-li použít signalizaci v prostředí domény, nastavte požadovanou vlastnost připojení následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="950c0-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="950c0-172">**C#kód klienta, který implementuje přihlašovací údaje pro připojení**</span><span class="sxs-lookup"><span data-stu-id="950c0-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="950c0-173">Další problémy s připojením</span><span class="sxs-lookup"><span data-stu-id="950c0-173">Other connection issues</span></span>

<span data-ttu-id="950c0-174">Tato část popisuje příčiny a řešení konkrétních symptomů a chybových zpráv, ke kterým dojde během připojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="950c0-175">Chyba "spuštění musí být voláno před odesláním dat".</span><span class="sxs-lookup"><span data-stu-id="950c0-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="950c0-176">K této chybě obvykle dochází, pokud kód odkazuje na objekty signálu před spuštěním připojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="950c0-177">Wireup pro obslužné rutiny a podobně jako volání metod definovaných na serveru se musí přidat po dokončení připojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="950c0-178">Všimněte si, že volání `Start` je asynchronní, takže kód po volání může být proveden před jeho dokončením.</span><span class="sxs-lookup"><span data-stu-id="950c0-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="950c0-179">Nejlepším způsobem, jak přidat obslužné rutiny po úplném spuštění připojení, je umístit je do funkce zpětného volání, která je předána jako parametr metodě start:</span><span class="sxs-lookup"><span data-stu-id="950c0-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="950c0-180">**JavaScriptový kód klienta, který správně přidává obslužné rutiny událostí, které odkazují na objekty signálu**</span><span class="sxs-lookup"><span data-stu-id="950c0-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="950c0-181">Tato chyba se zobrazí také v případě, že se připojení zastaví, zatímco jsou pořád odkazovány na objekty signálů.</span><span class="sxs-lookup"><span data-stu-id="950c0-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="950c0-182">Chyba "301 přesunutí trvalá" nebo "302 přesunuta"</span><span class="sxs-lookup"><span data-stu-id="950c0-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="950c0-183">Tato chyba se může zobrazit, pokud projekt obsahuje složku s názvem Signal, která bude v konfliktu s automaticky vytvořeným proxy serverem.</span><span class="sxs-lookup"><span data-stu-id="950c0-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="950c0-184">Chcete-li se této chybě vyhnout, nepoužívejte ve své aplikaci složku s názvem `SignalR` nebo vypněte automatické generování proxy.</span><span class="sxs-lookup"><span data-stu-id="950c0-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="950c0-185">Další podrobnosti najdete u [vygenerovaného proxy serveru a o tom, co vám dělá](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) .</span><span class="sxs-lookup"><span data-stu-id="950c0-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="950c0-186">Chyba "403 zakázáno" v klientovi .NET nebo Silverlight</span><span class="sxs-lookup"><span data-stu-id="950c0-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="950c0-187">K této chybě může dojít v prostředích mezi doménami, kde není správně povolená komunikace mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="950c0-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="950c0-188">Informace o tom, jak povolit mezidoménovou komunikaci, najdete v tématu [jak vytvořit připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span><span class="sxs-lookup"><span data-stu-id="950c0-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="950c0-189">Chcete-li vytvořit připojení mezi doménami v klientovi Silverlight, Projděte si téma [připojení mezi doménami od klientů programu Silverlight](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span><span class="sxs-lookup"><span data-stu-id="950c0-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="950c0-190">Chyba "404 nenalezen"</span><span class="sxs-lookup"><span data-stu-id="950c0-190">"404 Not Found" error</span></span>

<span data-ttu-id="950c0-191">Tento problém má několik příčin.</span><span class="sxs-lookup"><span data-stu-id="950c0-191">There are several causes for this issue.</span></span> <span data-ttu-id="950c0-192">Ověřte všechny tyto skutečnosti:</span><span class="sxs-lookup"><span data-stu-id="950c0-192">Verify all of the following:</span></span>

- <span data-ttu-id="950c0-193">**Odkaz na adresu proxy serveru centra není správně naformátován:** K této chybě obvykle dochází v případě, že odkaz na vygenerovanou adresu proxy serveru není správně naformátován.</span><span class="sxs-lookup"><span data-stu-id="950c0-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="950c0-194">Ověřte, zda je odkaz na adresu centra správně vytvořen.</span><span class="sxs-lookup"><span data-stu-id="950c0-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="950c0-195">Podrobnosti najdete v tématu [postup odkazování dynamicky vygenerovaného proxy serveru](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) .</span><span class="sxs-lookup"><span data-stu-id="950c0-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="950c0-196">**Přidávání tras do aplikace před přidáním trasy centra:** Pokud vaše aplikace používá jiné trasy, ověřte, zda je první přidaná trasa voláním `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="950c0-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="950c0-197">"500 interní chyba serveru"</span><span class="sxs-lookup"><span data-stu-id="950c0-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="950c0-198">Toto je velmi obecná chyba, která může mít nejrůznější příčiny.</span><span class="sxs-lookup"><span data-stu-id="950c0-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="950c0-199">Podrobnosti o chybě by se měly zobrazit v protokolu událostí serveru, nebo se dají najít prostřednictvím ladění serveru.</span><span class="sxs-lookup"><span data-stu-id="950c0-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="950c0-200">Podrobnější informace o chybách lze získat zapnutím podrobných chyb na serveru.</span><span class="sxs-lookup"><span data-stu-id="950c0-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="950c0-201">Další informace najdete v tématu [jak zpracovávat chyby ve třídě centra](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span><span class="sxs-lookup"><span data-stu-id="950c0-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="950c0-202">"TypeError: &lt;hubType&gt; není definováno" Chyba</span><span class="sxs-lookup"><span data-stu-id="950c0-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="950c0-203">Tato chyba bude mít za následek nesprávné provedení volání `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="950c0-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="950c0-204">Další informace najdete v tématu [jak zaregistrovat trasu signalizace a nakonfigurovat možnosti signalizace](../guide-to-the-api/hubs-api-guide-server.md#route) .</span><span class="sxs-lookup"><span data-stu-id="950c0-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="950c0-205">JsonSerializationException byl neošetřený uživatelským kódem.</span><span class="sxs-lookup"><span data-stu-id="950c0-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="950c0-206">Ověřte, zda parametry, které odesíláte do vašich metod, neobsahují neserializovatelné typy (například popisovače souborů nebo připojení k databázi).</span><span class="sxs-lookup"><span data-stu-id="950c0-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="950c0-207">Pokud potřebujete použít členy na objektu na straně serveru, který nechcete odesílat klientovi (buď z důvodu zabezpečení, nebo z důvodů serializace), použijte atribut `JSONIgnore`.</span><span class="sxs-lookup"><span data-stu-id="950c0-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="950c0-208">Chyba protokolu: Neznámá přenosová chyba</span><span class="sxs-lookup"><span data-stu-id="950c0-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="950c0-209">K této chybě může dojít, pokud klient nepodporuje přenos, který signál používá.</span><span class="sxs-lookup"><span data-stu-id="950c0-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="950c0-210">Informace o tom, které prohlížeče se dají používat se signálem, najdete v tématu [přenosové a záložní](../getting-started/introduction-to-signalr.md#transports) verze.</span><span class="sxs-lookup"><span data-stu-id="950c0-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="950c0-211">"Generování proxy serveru centra JavaScript bylo zakázáno."</span><span class="sxs-lookup"><span data-stu-id="950c0-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="950c0-212">K této chybě dojde, pokud je nastavena `DisableJavaScriptProxies` a zároveň zahrnuje odkaz na dynamicky generovaný proxy server v `signalr/hubs`.</span><span class="sxs-lookup"><span data-stu-id="950c0-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="950c0-213">Další informace o ručním vytvoření proxy serveru najdete v tématu [vygenerované proxy a k čemu](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="950c0-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="950c0-214">"ID připojení má nesprávný formát" nebo "při aktivním připojení k signalizaci se nemůže změnit identita uživatele"</span><span class="sxs-lookup"><span data-stu-id="950c0-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="950c0-215">Tato chyba se může zobrazit, pokud se používá ověřování a klient se odhlásí před zastavením připojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="950c0-216">Řešením je zastavit připojení k signalizaci před protokolováním klienta.</span><span class="sxs-lookup"><span data-stu-id="950c0-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="950c0-217">"Nezachycená Chyba: signál: jQuery nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="950c0-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="950c0-218">Ujistěte se prosím, že se na jQuery odkazuje před souborem Signal. js.</span><span class="sxs-lookup"><span data-stu-id="950c0-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="950c0-219">Klient pro signalizaci JavaScriptu vyžaduje, aby se spustilo jQuery.</span><span class="sxs-lookup"><span data-stu-id="950c0-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="950c0-220">Ověřte, zda je odkaz na jQuery správný, zda použitá cesta je platná a zda odkaz na jQuery je před odkazem na signál.</span><span class="sxs-lookup"><span data-stu-id="950c0-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="950c0-221">"Nezachycené TypeError: nejde načíst vlastnost&lt;vlastnost&gt;nedefinovaného".</span><span class="sxs-lookup"><span data-stu-id="950c0-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="950c0-222">Tato chyba je způsobena tím, že není správně odkazována na jQuery nebo na proxy centra.</span><span class="sxs-lookup"><span data-stu-id="950c0-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="950c0-223">Ověřte, zda je váš odkaz na jQuery a proxy rozbočovačů správný, zda použitá cesta je platná a zda odkaz na jQuery je před odkazem na proxy centra.</span><span class="sxs-lookup"><span data-stu-id="950c0-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="950c0-224">Výchozí odkaz na proxy centra by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="950c0-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="950c0-225">**Kód HTML na straně klienta, který správně odkazuje na proxy centra**</span><span class="sxs-lookup"><span data-stu-id="950c0-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="950c0-226">Chyba "RuntimeBinderException byl neošetřený uživatelským kódem"</span><span class="sxs-lookup"><span data-stu-id="950c0-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="950c0-227">K této chybě může dojít, pokud je použito nesprávné přetížení `Hub.On`.</span><span class="sxs-lookup"><span data-stu-id="950c0-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="950c0-228">Pokud má metoda návratovou hodnotu, musí být návratový typ zadán jako parametr obecného typu:</span><span class="sxs-lookup"><span data-stu-id="950c0-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="950c0-229">**Metoda definovaná na klientovi (bez vygenerovaného proxy serveru)**</span><span class="sxs-lookup"><span data-stu-id="950c0-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="950c0-230">ID připojení je nekonzistentní nebo se mezi načtenými stránkami narušuje přerušení připojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="950c0-231">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="950c0-231">This behavior is by design.</span></span> <span data-ttu-id="950c0-232">Vzhledem k tomu, že je objekt centra hostovaný v objektu stránky, je při aktualizaci stránky tento rozbočovač zničen.</span><span class="sxs-lookup"><span data-stu-id="950c0-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="950c0-233">Vícestránkové aplikace musí udržovat přidružení mezi uživateli a identifikátory připojení, aby byly konzistentní mezi načítáním stránek.</span><span class="sxs-lookup"><span data-stu-id="950c0-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="950c0-234">ID připojení mohou být uložena na serveru buď v objektu `ConcurrentDictionary`, nebo v databázi.</span><span class="sxs-lookup"><span data-stu-id="950c0-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="950c0-235">Chyba "hodnota nemůže mít hodnotu null"</span><span class="sxs-lookup"><span data-stu-id="950c0-235">"Value cannot be null" error</span></span>

<span data-ttu-id="950c0-236">Metody na straně serveru s nepovinnými parametry se v současné době nepodporují. Pokud je nepovinný parametr vynechán, metoda se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="950c0-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="950c0-237">Další informace najdete v tématu [volitelné parametry](https://github.com/SignalR/SignalR/issues/324).</span><span class="sxs-lookup"><span data-stu-id="950c0-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="950c0-238">"Firefox nemůže navázat připojení k serveru na adrese &lt;adresa&gt;" Chyba v Firebug</span><span class="sxs-lookup"><span data-stu-id="950c0-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="950c0-239">Tato chybová zpráva se může zobrazit v Firebug v případě, že se vyjednávání protokolu WebSocket nezdaří a místo toho se použije další přenos.</span><span class="sxs-lookup"><span data-stu-id="950c0-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="950c0-240">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="950c0-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="950c0-241">"Vzdálený certifikát je neplatný podle ověřovací procedury" Chyba v klientské aplikaci .NET</span><span class="sxs-lookup"><span data-stu-id="950c0-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="950c0-242">Pokud váš server vyžaduje vlastní klientské certifikáty, můžete k připojení přidat certifikátu x509 před tím, než se žádost dovede.</span><span class="sxs-lookup"><span data-stu-id="950c0-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="950c0-243">Přidejte certifikát k připojení pomocí `Connection.AddClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="950c0-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="950c0-244">Po vypršení časového limitu připojení se uvolní.</span><span class="sxs-lookup"><span data-stu-id="950c0-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="950c0-245">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="950c0-245">This behavior is by design.</span></span> <span data-ttu-id="950c0-246">Přihlašovací údaje pro ověřování nelze upravovat, pokud je připojení aktivní; Chcete-li aktualizovat přihlašovací údaje, je nutné připojení zastavit a restartovat.</span><span class="sxs-lookup"><span data-stu-id="950c0-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="950c0-247">V případě, že se používá jQuery Mobile, se v připojení volá dvakrát.</span><span class="sxs-lookup"><span data-stu-id="950c0-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="950c0-248">funkce `initializePage` jQuery Mobile vynutí opětovné spuštění skriptů na každé stránce, čímž se vytvoří druhé připojení.</span><span class="sxs-lookup"><span data-stu-id="950c0-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="950c0-249">Mezi řešení tohoto problému patří:</span><span class="sxs-lookup"><span data-stu-id="950c0-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="950c0-250">Přidejte odkaz na jQuery Mobile před souborem JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="950c0-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="950c0-251">Zakažte funkci `initializePage` nastavením `$.mobile.autoInitializePage = false`.</span><span class="sxs-lookup"><span data-stu-id="950c0-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="950c0-252">Než začnete s připojením, počkejte, než se dokončí inicializace stránky.</span><span class="sxs-lookup"><span data-stu-id="950c0-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="950c0-253">Zprávy jsou v aplikacích Silverlight zpožděny pomocí událostí odeslaných serverem.</span><span class="sxs-lookup"><span data-stu-id="950c0-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="950c0-254">Zprávy jsou zpožděny při použití událostí odeslaných serverem v programu Silverlight.</span><span class="sxs-lookup"><span data-stu-id="950c0-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="950c0-255">Pokud chcete vynutit použití dlouhého cyklického dotazování, použijte při spuštění připojení následující:</span><span class="sxs-lookup"><span data-stu-id="950c0-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="950c0-256">"Oprávnění bylo odepřeno pomocí protokolu rámců navždy</span><span class="sxs-lookup"><span data-stu-id="950c0-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="950c0-257">Jedná se o známý problém, který je [zde](https://github.com/SignalR/SignalR/issues/1963)popsán.</span><span class="sxs-lookup"><span data-stu-id="950c0-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="950c0-258">Tento příznak se může zobrazit pomocí nejnovější knihovny JQuery. alternativním řešením je downgrade aplikace na JQuery 1.8.2.</span><span class="sxs-lookup"><span data-stu-id="950c0-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="950c0-259">Kompilace a chyby na straně serveru</span><span class="sxs-lookup"><span data-stu-id="950c0-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="950c0-260">Následující část obsahuje možná řešení pro kompilátor a chyby běhového prostředí na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="950c0-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="950c0-261">Odkaz na instanci centra je null.</span><span class="sxs-lookup"><span data-stu-id="950c0-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="950c0-262">Vzhledem k tomu, že je instance centra pro každé připojení vytvořená, nemůžete ve svém kódu vytvořit instanci rozbočovače sami.</span><span class="sxs-lookup"><span data-stu-id="950c0-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="950c0-263">Chcete-li volat metody na rozbočovači vně samotného centra, přečtěte si téma [jak volat klientské metody a spravovat skupiny z vně třídy centra](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) pro získání odkazu na kontext centra.</span><span class="sxs-lookup"><span data-stu-id="950c0-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="950c0-264">HTTPContext. Current. Session má hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="950c0-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="950c0-265">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="950c0-265">This behavior is by design.</span></span> <span data-ttu-id="950c0-266">Signál nepodporuje stav relace ASP.NET, protože povolení stavu relace by přerušilo duplexní zasílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="950c0-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="950c0-267">Žádná vhodná metoda pro přepsání</span><span class="sxs-lookup"><span data-stu-id="950c0-267">No suitable method to override</span></span>

<span data-ttu-id="950c0-268">Tato chyba se může zobrazit, pokud používáte kód ze starší dokumentace nebo blogů.</span><span class="sxs-lookup"><span data-stu-id="950c0-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="950c0-269">Ověřte, že neodkazují na názvy metod, které byly změněny nebo zastaralé (například `OnConnectedAsync`).</span><span class="sxs-lookup"><span data-stu-id="950c0-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="950c0-270">HostContextExtensions. WebSocketServerUrl má hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="950c0-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="950c0-271">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="950c0-271">This behavior is by design.</span></span> <span data-ttu-id="950c0-272">Tento člen je zastaralý a neměl by se používat.</span><span class="sxs-lookup"><span data-stu-id="950c0-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="950c0-273">"Trasa s názvem" Signal. Hubs "je již v kolekci tras"</span><span class="sxs-lookup"><span data-stu-id="950c0-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="950c0-274">Tato chyba se zobrazí, pokud vaše aplikace `MapHubs` volá dvakrát.</span><span class="sxs-lookup"><span data-stu-id="950c0-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="950c0-275">Některé příklady aplikací volají `MapHubs` přímo v souboru globální aplikace. jiné provádí volání v obálkové třídě.</span><span class="sxs-lookup"><span data-stu-id="950c0-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="950c0-276">Ujistěte se, že aplikace neprovádí obojí.</span><span class="sxs-lookup"><span data-stu-id="950c0-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="950c0-277">Problémy se sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="950c0-277">Visual Studio issues</span></span>

<span data-ttu-id="950c0-278">Tato část popisuje problémy zjištěné v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="950c0-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="950c0-279">Uzel dokumenty skriptu se nezobrazuje v Průzkumník řešení</span><span class="sxs-lookup"><span data-stu-id="950c0-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="950c0-280">Některé z našich kurzů vás přesměrují na uzel dokumenty skriptů v Průzkumník řešení při ladění.</span><span class="sxs-lookup"><span data-stu-id="950c0-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="950c0-281">Tento uzel je vytvořen ladicím programem jazyka JavaScript a zobrazí se pouze při ladění klientů prohlížeče v aplikaci Internet Explorer. Pokud se použije Chrome nebo Firefox, uzel se nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="950c0-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="950c0-282">Ladicí program JavaScriptu se také nespustí, pokud je spuštěn jiný klientský ladicí program, jako je například ladicí program Silverlight.</span><span class="sxs-lookup"><span data-stu-id="950c0-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="950c0-283">Návěstí nefunguje v systému Visual Studio 2008 nebo starším.</span><span class="sxs-lookup"><span data-stu-id="950c0-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="950c0-284">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="950c0-284">This behavior is by design.</span></span> <span data-ttu-id="950c0-285">Signál vyžaduje .NET Framework 4 nebo novější; To vyžaduje, aby byly aplikace signálů vyvinuty v aplikaci Visual Studio 2010 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="950c0-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="950c0-286">Problémy služby IIS</span><span class="sxs-lookup"><span data-stu-id="950c0-286">IIS issues</span></span>

<span data-ttu-id="950c0-287">Tato část obsahuje problémy s Internetová informační služba.</span><span class="sxs-lookup"><span data-stu-id="950c0-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="950c0-288">Selhání webu po volání MapHubs</span><span class="sxs-lookup"><span data-stu-id="950c0-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="950c0-289">Tento problém byl opraven v nejnovější verzi nástroje Signaler.</span><span class="sxs-lookup"><span data-stu-id="950c0-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="950c0-290">Ověřte, že používáte nejnovější vydanou verzi nástroje Signal tím, že svou instalaci aktualizujete pomocí NuGet.</span><span class="sxs-lookup"><span data-stu-id="950c0-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="950c0-291">Problémy s Azure</span><span class="sxs-lookup"><span data-stu-id="950c0-291">Azure issues</span></span>

<span data-ttu-id="950c0-292">Tato část obsahuje problémy s Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="950c0-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="950c0-293">Po změně názvů témat se zprávy nepřijaly prostřednictvím Azure replánování.</span><span class="sxs-lookup"><span data-stu-id="950c0-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="950c0-294">Témata používaná v Azure back-Plan nejsou zamýšlená jako uživatelsky konfigurovatelné.</span><span class="sxs-lookup"><span data-stu-id="950c0-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
