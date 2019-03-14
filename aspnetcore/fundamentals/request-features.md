---
title: Požadavky na funkce v ASP.NET Core
author: ardalis
description: Další informace o podrobnosti implementace web server týkající se požadavků HTTP a odpovědí, které jsou definovány v rozhraní ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: fundamentals/request-features
ms.openlocfilehash: d0f3ae521d1f314dd04cb581d9a921da4719273d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067990"
---
# <a name="request-features-in-aspnet-core"></a><span data-ttu-id="e0d7f-103">Požadavky na funkce v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e0d7f-103">Request Features in ASP.NET Core</span></span>

<span data-ttu-id="e0d7f-104">Podle [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="e0d7f-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="e0d7f-105">Implementační detaily webového serveru související s HTTP požadavky a odpověďmi jsou definovány v rozhraních.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-105">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="e0d7f-106">Tato rozhraní jsou používány implementací serveru a middleware pro vytvoření a úprava kanálu hostování vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-106">These interfaces are used by server implementations and middleware to create and modify the application's hosting pipeline.</span></span>

## <a name="feature-interfaces"></a><span data-ttu-id="e0d7f-107">Funkce rozhraní</span><span class="sxs-lookup"><span data-stu-id="e0d7f-107">Feature interfaces</span></span>

<span data-ttu-id="e0d7f-108">Definuje počet rozhraní funkce protokolu HTTP v ASP.NET Core `Microsoft.AspNetCore.Http.Features` servery které se používají k identifikaci funkce podporují.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-108">ASP.NET Core defines a number of HTTP feature interfaces in `Microsoft.AspNetCore.Http.Features` which are used by servers to identify the features they support.</span></span> <span data-ttu-id="e0d7f-109">Následující funkce rozhraní zpracování požadavků a vrácení odpovědi:</span><span class="sxs-lookup"><span data-stu-id="e0d7f-109">The following feature interfaces handle requests and return responses:</span></span>

<span data-ttu-id="e0d7f-110">`IHttpRequestFeature` Definuje strukturu požadavek HTTP, včetně protokolu, cesta, řetězec dotazu, záhlaví a text.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-110">`IHttpRequestFeature` Defines the structure of an HTTP request, including the protocol, path, query string, headers, and body.</span></span>

<span data-ttu-id="e0d7f-111">`IHttpResponseFeature` Definuje strukturu odpověď HTTP včetně kódů, záhlaví a text odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-111">`IHttpResponseFeature` Defines the structure of an HTTP response, including the status code, headers, and body of the response.</span></span>

<span data-ttu-id="e0d7f-112">`IHttpAuthenticationFeature` Definuje podporu pro identifikaci uživatelů na základě `ClaimsPrincipal` a určení obslužnou rutinu ověřování.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-112">`IHttpAuthenticationFeature` Defines support for identifying users based on a `ClaimsPrincipal` and specifying an authentication handler.</span></span>

<span data-ttu-id="e0d7f-113">`IHttpUpgradeFeature` Definuje podporu pro [HTTP upgrady](https://tools.ietf.org/html/rfc2616.html#section-14.42), které umožňují klientovi k určení, které další protokoly se chtěli používat, pokud chce přepnout protokolů serveru.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-113">`IHttpUpgradeFeature` Defines support for [HTTP Upgrades](https://tools.ietf.org/html/rfc2616.html#section-14.42), which allow the client to specify which additional protocols it would like to use if the server wishes to switch protocols.</span></span>

<span data-ttu-id="e0d7f-114">`IHttpBufferingFeature` Definuje metody pro zakázání ukládání do vyrovnávací paměti požadavky a/nebo odpovědí.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-114">`IHttpBufferingFeature` Defines methods for disabling buffering of requests and/or responses.</span></span>

<span data-ttu-id="e0d7f-115">`IHttpConnectionFeature` Definuje vlastnosti pro místní a vzdálené adresy a porty.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-115">`IHttpConnectionFeature` Defines properties for local and remote addresses and ports.</span></span>

<span data-ttu-id="e0d7f-116">`IHttpRequestLifetimeFeature` Definuje podporu pro přerušení připojení nebo zjišťování, pokud žádost se ukončila předčasně ukončen, například po odpojení klienta.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-116">`IHttpRequestLifetimeFeature` Defines support for aborting connections, or detecting if a request has been terminated prematurely, such as by a client disconnect.</span></span>

<span data-ttu-id="e0d7f-117">`IHttpSendFileFeature` Definuje metody pro asynchronní odesílání souborů.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-117">`IHttpSendFileFeature` Defines a method for sending files asynchronously.</span></span>

<span data-ttu-id="e0d7f-118">`IHttpWebSocketFeature` Definuje rozhraní API pro podporu webové sokety.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-118">`IHttpWebSocketFeature` Defines an API for supporting web sockets.</span></span>

<span data-ttu-id="e0d7f-119">`IHttpRequestIdentifierFeature` Přidá vlastnost, která je možné implementovat k jednoznačné identifikaci požadavků.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-119">`IHttpRequestIdentifierFeature` Adds a property that can be implemented to uniquely identify requests.</span></span>

<span data-ttu-id="e0d7f-120">`ISessionFeature` Definuje `ISessionFactory` a `ISession` abstrakce pro podporu uživatelských relací.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-120">`ISessionFeature` Defines `ISessionFactory` and `ISession` abstractions for supporting user sessions.</span></span>

<span data-ttu-id="e0d7f-121">`ITlsConnectionFeature` Definuje rozhraní API pro načítání klientské certifikáty.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-121">`ITlsConnectionFeature` Defines an API for retrieving client certificates.</span></span>

<span data-ttu-id="e0d7f-122">`ITlsTokenBindingFeature` Definuje metody pro práci s parametry token vazby protokolu TLS.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-122">`ITlsTokenBindingFeature` Defines methods for working with TLS token binding parameters.</span></span>

> [!NOTE]
> <span data-ttu-id="e0d7f-123">`ISessionFeature` není funkce serveru, ale implementuje ho `SessionMiddleware` (naleznete v tématu [Správa stavu aplikace](app-state.md)).</span><span class="sxs-lookup"><span data-stu-id="e0d7f-123">`ISessionFeature` isn't a server feature, but is implemented by the `SessionMiddleware` (see [Managing Application State](app-state.md)).</span></span>

## <a name="feature-collections"></a><span data-ttu-id="e0d7f-124">Kolekce funkcí</span><span class="sxs-lookup"><span data-stu-id="e0d7f-124">Feature collections</span></span>

<span data-ttu-id="e0d7f-125">`Features` Vlastnost `HttpContext` poskytuje rozhraní pro získání a nastavení k dispozici funkce protokolu HTTP pro aktuální požadavek.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-125">The `Features` property of `HttpContext` provides an interface for getting and setting the available HTTP features for the current request.</span></span> <span data-ttu-id="e0d7f-126">Protože kolekce funkcí proměnlivé i v rámci kontextu požadavku, middleware je možné změnit kolekci a přidání podpory pro další funkce.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-126">Since the feature collection is mutable even within the context of a request, middleware can be used to modify the collection and add support for additional features.</span></span>

## <a name="middleware-and-request-features"></a><span data-ttu-id="e0d7f-127">Middleware a žádosti o funkce</span><span class="sxs-lookup"><span data-stu-id="e0d7f-127">Middleware and request features</span></span>

<span data-ttu-id="e0d7f-128">I když servery zodpovědná za vytvoření kolekce funkcí, middleware lze do této kolekce přidat i využívat funkce z kolekce.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-128">While servers are responsible for creating the feature collection, middleware can both add to this collection and consume features from the collection.</span></span> <span data-ttu-id="e0d7f-129">Například `StaticFileMiddleware` přistupuje `IHttpSendFileFeature` funkce.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-129">For example, the `StaticFileMiddleware` accesses the `IHttpSendFileFeature` feature.</span></span> <span data-ttu-id="e0d7f-130">Pokud funkci existuje, se používá k odesílání požadovaných statických souborů z jeho fyzickou cestu.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-130">If the feature exists, it's used to send the requested static file from its physical path.</span></span> <span data-ttu-id="e0d7f-131">V opačném případě pomalejší alternativní metoda se používá k odeslání souboru.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-131">Otherwise, a slower alternative method is used to send the file.</span></span> <span data-ttu-id="e0d7f-132">Pokud je k dispozici, `IHttpSendFileFeature` umožňuje operačního systému k otevření souboru a provádění kopie režimu jádra s přímým přístupem k síťové kartě.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-132">When available, the `IHttpSendFileFeature` allows the operating system to open the file and perform a direct kernel mode copy to the network card.</span></span>

<span data-ttu-id="e0d7f-133">Kromě toho middleware lze přidat do kolekce funkce stanovené serveru.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-133">Additionally, middleware can add to the feature collection established by the server.</span></span> <span data-ttu-id="e0d7f-134">Existující funkce lze nahradit i middlewaru umožňuje middleware pro rozšíření funkcí serveru.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-134">Existing features can even be replaced by middleware, allowing the middleware to augment the functionality of the server.</span></span> <span data-ttu-id="e0d7f-135">Funkce přidané do kolekce jsou k dispozici okamžitě na další middleware nebo základní samotná aplikace později v kanálu požadavku.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-135">Features added to the collection are available immediately to other middleware or the underlying application itself later in the request pipeline.</span></span>

<span data-ttu-id="e0d7f-136">Díky kombinaci implementace vlastního serveru a vylepšení pro konkrétní middleware, lze sestavit přesnou sadu funkcí, které aplikace vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-136">By combining custom server implementations and specific middleware enhancements, the precise set of features an application requires can be constructed.</span></span> <span data-ttu-id="e0d7f-137">To umožňuje chybějící funkce přidávané bez nutnosti provádění změn na serveru a zajišťuje jsou přístupné jenom minimální množství funkcí, tedy omezení útoku surface oblasti a zlepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-137">This allows missing features to be added without requiring a change in server, and ensures only the minimal amount of features are exposed, thus limiting attack surface area and improving performance.</span></span>

## <a name="summary"></a><span data-ttu-id="e0d7f-138">Souhrn</span><span class="sxs-lookup"><span data-stu-id="e0d7f-138">Summary</span></span>

<span data-ttu-id="e0d7f-139">Funkce rozhraní definují určité funkce protokolu HTTP, které můžou podporovat daného požadavku.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-139">Feature interfaces define specific HTTP features that a given request may support.</span></span> <span data-ttu-id="e0d7f-140">Servery definovat kolekce funkcí a počáteční sadu funkcí podporovaných tímto serverem, ale ke zvýšení tyto funkce můžete použít middlewaru.</span><span class="sxs-lookup"><span data-stu-id="e0d7f-140">Servers define collections of features, and the initial set of features supported by that server, but middleware can be used to enhance these features.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0d7f-141">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="e0d7f-141">Additional resources</span></span>

* [<span data-ttu-id="e0d7f-142">Servery</span><span class="sxs-lookup"><span data-stu-id="e0d7f-142">Servers</span></span>](xref:fundamentals/servers/index)
* [<span data-ttu-id="e0d7f-143">Middleware</span><span class="sxs-lookup"><span data-stu-id="e0d7f-143">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="e0d7f-144">Otevřené webové rozhraní pro .NET (OWIN)</span><span class="sxs-lookup"><span data-stu-id="e0d7f-144">Open Web Interface for .NET (OWIN)</span></span>](xref:fundamentals/owin)
