---
title: Hostování v technologii ASP.NET Core SignalR produkčního prostředí a škálování
author: bradygaster
description: Zjistěte, jak se vyhnout výkonu a škálování problémů v aplikacích, které používají funkce SignalR technologie ASP.NET Core.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/28/2018
uid: signalr/scale
ms.openlocfilehash: 4ac4509acc89d0091a3757c7cfbc9981614f29ad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069946"
---
# <a name="aspnet-core-signalr-hosting-and-scaling"></a><span data-ttu-id="7c948-103">Hostování v technologii ASP.NET Core SignalR a škálování</span><span class="sxs-lookup"><span data-stu-id="7c948-103">ASP.NET Core SignalR hosting and scaling</span></span>

<span data-ttu-id="7c948-104">Podle [Andrew Stanton sestry](https://twitter.com/anurse), [Brady Gaster](https://twitter.com/bradygaster), a [Petr Dykstra](https://github.com/tdykstra),</span><span class="sxs-lookup"><span data-stu-id="7c948-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse), [Brady Gaster](https://twitter.com/bradygaster), and [Tom Dykstra](https://github.com/tdykstra),</span></span>

<span data-ttu-id="7c948-105">Tento článek vysvětluje, hostování a škálování důležité informace týkající se vysokým provozem aplikací, které používají funkce SignalR technologie ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7c948-105">This article explains hosting and scaling considerations for high-traffic apps that use ASP.NET Core SignalR.</span></span>

## <a name="tcp-connection-resources"></a><span data-ttu-id="7c948-106">Prostředky připojení TCP</span><span class="sxs-lookup"><span data-stu-id="7c948-106">TCP connection resources</span></span>

<span data-ttu-id="7c948-107">Počet souběžných připojení TCP, která podporuje webový server je omezený.</span><span class="sxs-lookup"><span data-stu-id="7c948-107">The number of concurrent TCP connections that a web server can support is limited.</span></span> <span data-ttu-id="7c948-108">Standardní HTTP používají *dočasné* připojení.</span><span class="sxs-lookup"><span data-stu-id="7c948-108">Standard HTTP clients use *ephemeral* connections.</span></span> <span data-ttu-id="7c948-109">Tato připojení lze uzavřít, když klient přejde nečinnosti a později znovu otevřít.</span><span class="sxs-lookup"><span data-stu-id="7c948-109">These connections can be closed when the client goes idle and reopened later.</span></span> <span data-ttu-id="7c948-110">Na druhé straně připojení SignalR je *trvalé*.</span><span class="sxs-lookup"><span data-stu-id="7c948-110">On the other hand, a SignalR connection is *persistent*.</span></span> <span data-ttu-id="7c948-111">Připojení SignalR zůstávají otevřené i v při, klient přejde nečinnosti.</span><span class="sxs-lookup"><span data-stu-id="7c948-111">SignalR connections stay open even when the client goes idle.</span></span> <span data-ttu-id="7c948-112">V aplikace s vysokým provozem, který poskytuje mnoho klientů může způsobit tyto trvalá připojení serverů k dosažení maximálního počtu připojení.</span><span class="sxs-lookup"><span data-stu-id="7c948-112">In a high-traffic app that serves many clients, these persistent connections can cause servers to hit their maximum number of connections.</span></span>

<span data-ttu-id="7c948-113">Trvalá připojení také využívat některé další paměť, ke sledování jednotlivých připojení.</span><span class="sxs-lookup"><span data-stu-id="7c948-113">Persistent connections also consume some additional memory, to track each connection.</span></span>

<span data-ttu-id="7c948-114">Zátěž související připojení prostředků systémem SignalR může ovlivnit jiné webové aplikace, které jsou hostovány na stejném serveru.</span><span class="sxs-lookup"><span data-stu-id="7c948-114">The heavy use of connection-related resources by SignalR can affect other web apps that are hosted on the same server.</span></span> <span data-ttu-id="7c948-115">Když SignalR otevře a obsahuje poslední dostupné připojení TCP, jiné webové aplikace na stejném serveru také mít žádná další připojení, která je jim dostupná.</span><span class="sxs-lookup"><span data-stu-id="7c948-115">When SignalR opens and holds the last available TCP connections, other web apps on the same server also have no more connections available to them.</span></span>

<span data-ttu-id="7c948-116">Pokud serveru připojení, uvidíte soketu náhodných chyb a chyb resetování připojení.</span><span class="sxs-lookup"><span data-stu-id="7c948-116">If a server runs out of connections, you'll see random socket errors and connection reset errors.</span></span> <span data-ttu-id="7c948-117">Příklad:</span><span class="sxs-lookup"><span data-stu-id="7c948-117">For example:</span></span>

```
An attempt was made to access a socket in a way forbidden by its access permissions...
```

<span data-ttu-id="7c948-118">Zabránit používání prostředků SignalR příčinou chyb v jiných webových aplikací, běžet na různých serverech než vaše webové aplikace SignalR.</span><span class="sxs-lookup"><span data-stu-id="7c948-118">To keep SignalR resource usage from causing errors in other web apps, run SignalR on different servers than your other web apps.</span></span>

<span data-ttu-id="7c948-119">Zabránit používání prostředků SignalR příčinou chyb v aplikaci s knihovnou SignalR, horizontální navýšení kapacity na omezit počet připojení, která je na serveru pro zpracování.</span><span class="sxs-lookup"><span data-stu-id="7c948-119">To keep SignalR resource usage from causing errors in a SignalR app, scale out to limit the number of connections a server has to handle.</span></span>

## <a name="scale-out"></a><span data-ttu-id="7c948-120">Škálování na více systémů</span><span class="sxs-lookup"><span data-stu-id="7c948-120">Scale out</span></span>

<span data-ttu-id="7c948-121">Aplikaci, která využívá funkce SignalR musí udržovat přehled o všech jeho připojení vytváří problémy u serverové farmy.</span><span class="sxs-lookup"><span data-stu-id="7c948-121">An app that uses SignalR needs to keep track of all its connections, which creates problems for a server farm.</span></span> <span data-ttu-id="7c948-122">Přidání serveru a načte nová připojení, které nemusíte vědět ostatní servery.</span><span class="sxs-lookup"><span data-stu-id="7c948-122">Add a server, and it gets new connections that the other servers don't know about.</span></span> <span data-ttu-id="7c948-123">SignalR na každém serveru v následujícím diagramu je třeba vědět o připojení na jiných serverech.</span><span class="sxs-lookup"><span data-stu-id="7c948-123">For example, SignalR on each server in the following diagram is unaware of the connections on the other servers.</span></span> <span data-ttu-id="7c948-124">Když chce, aby funkce SignalR technologie jeden ze serverů pro odeslání zprávy na všechny klienty, zprávy pouze přejde na klienty připojené k tomuto serveru.</span><span class="sxs-lookup"><span data-stu-id="7c948-124">When SignalR on one of the servers wants to send a message to all clients, the message only goes to the clients connected to that server.</span></span>

![Bez propojovací rozhraní škálování SignalR](scale/_static/scale-no-backplane.png)

<span data-ttu-id="7c948-126">Možnosti pro řešení tohoto problému jsou [služby Azure SignalR](#azure-signalr-service) a [Redis propojovací rozhraní systému](#redis-backplane).</span><span class="sxs-lookup"><span data-stu-id="7c948-126">The options for solving this problem are the [Azure SignalR Service](#azure-signalr-service) and [Redis backplane](#redis-backplane).</span></span>

## <a name="azure-signalr-service"></a><span data-ttu-id="7c948-127">Služba Azure SignalR</span><span class="sxs-lookup"><span data-stu-id="7c948-127">Azure SignalR Service</span></span>

<span data-ttu-id="7c948-128">Služby Azure SignalR je proxy server, nikoli propojovacího rozhraní.</span><span class="sxs-lookup"><span data-stu-id="7c948-128">The Azure SignalR Service is a proxy rather than a backplane.</span></span> <span data-ttu-id="7c948-129">Pokaždé, když klient zahájí připojení k serveru, se klient přesměruje k připojení ke službě.</span><span class="sxs-lookup"><span data-stu-id="7c948-129">Each time a client initiates a connection to the server, the client is redirected to connect to the service.</span></span> <span data-ttu-id="7c948-130">Tento proces je znázorněn v následujícím diagramu:</span><span class="sxs-lookup"><span data-stu-id="7c948-130">That process is illustrated in the following diagram:</span></span>

![Připojení ke službě Azure SignalR](scale/_static/azure-signalr-service-one-connection.png)

<span data-ttu-id="7c948-132">Výsledkem je, že služba spravuje všechna připojení klientů, zatímco každý server potřebuje pouze malý konstantní počet připojení ke službě, jak je znázorněno v následujícím diagramu:</span><span class="sxs-lookup"><span data-stu-id="7c948-132">The result is that the service manages all of the client connections, while each server needs only a small constant number of connections to the service, as shown in the following diagram:</span></span>

![Klienti se připojí ke službě, servery připojené ke službě](scale/_static/azure-signalr-service-multiple-connections.png)

<span data-ttu-id="7c948-134">Tento přístup pro horizontální navýšení kapacity má několik výhod oproti alternativní Redis propojovací rozhraní systému:</span><span class="sxs-lookup"><span data-stu-id="7c948-134">This approach to scale-out has several advantages over the Redis backplane alternative:</span></span>

* <span data-ttu-id="7c948-135">Rychlé relace, označované také jako [spřažení klienta](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity), není vyžadováno, protože klienti budou přesměrovaní okamžitě ke službě Azure SignalR, když se připojují.</span><span class="sxs-lookup"><span data-stu-id="7c948-135">Sticky sessions, also known as [client affinity](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity), is not required, because clients are immediately redirected to the Azure SignalR Service when they connect.</span></span>
* <span data-ttu-id="7c948-136">SignalR, které aplikace můžete horizontálně navýšit kapacitu podle počtu zpráv odeslaných, zatímco služby Azure SignalR automaticky škáluje, aby zpracování libovolný počet připojení.</span><span class="sxs-lookup"><span data-stu-id="7c948-136">A SignalR app can scale out based on the number of messages sent, while the Azure SignalR Service automatically scales to handle any number of connections.</span></span> <span data-ttu-id="7c948-137">Například může být tisíců klientů, ale pokud pouze několik zpráv za sekundu se odesílají, nebudete muset horizontální navýšení kapacity na několik serverů stačí pro zpracování připojení sami aplikace SignalR.</span><span class="sxs-lookup"><span data-stu-id="7c948-137">For example, there could be thousands of clients, but if only a few messages per second are sent, the SignalR app won't need to scale out to multiple servers just to handle the connections themselves.</span></span>
* <span data-ttu-id="7c948-138">Aplikace s knihovnou SignalR nepoužije podstatně více připojení prostředků než webové aplikace bez SignalR.</span><span class="sxs-lookup"><span data-stu-id="7c948-138">A SignalR app won't use significantly more connection resources than a web app without SignalR.</span></span>

<span data-ttu-id="7c948-139">Z těchto důvodů doporučujeme, abyste službě Azure SignalR pro všechny funkce SignalR technologie ASP.NET Core aplikací hostovaných v Azure, včetně služby App Service, virtuální počítače a kontejnery.</span><span class="sxs-lookup"><span data-stu-id="7c948-139">For these reasons, we recommend the Azure SignalR Service for all ASP.NET Core SignalR apps hosted on Azure, including App Service, VMs, and containers.</span></span>

<span data-ttu-id="7c948-140">Další informace najdete v článku [dokumentace ke službě Azure SignalR](/azure/azure-signalr/signalr-overview).</span><span class="sxs-lookup"><span data-stu-id="7c948-140">For more information see the [Azure SignalR Service documentation](/azure/azure-signalr/signalr-overview).</span></span>

## <a name="redis-backplane"></a><span data-ttu-id="7c948-141">Propojovací rozhraní Redis</span><span class="sxs-lookup"><span data-stu-id="7c948-141">Redis backplane</span></span>

<span data-ttu-id="7c948-142">[Redis](https://redis.io/) je párů klíč hodnota v paměti, podporující systému zasílání zpráv s modelem publikování a přihlášení k odběru.</span><span class="sxs-lookup"><span data-stu-id="7c948-142">[Redis](https://redis.io/) is an in-memory key-value store that supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="7c948-143">Propojovací rozhraní systému SignalR Redis používá funkci pub/sub pro předávání zpráv na jiné servery.</span><span class="sxs-lookup"><span data-stu-id="7c948-143">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span> <span data-ttu-id="7c948-144">Když se klient připojí, informace o připojení je předán do propojovacího rozhraní.</span><span class="sxs-lookup"><span data-stu-id="7c948-144">When a client makes a connection, the connection information is passed to the backplane.</span></span> <span data-ttu-id="7c948-145">Když chce, aby server pro odeslání zprávy na všechny klienty, odešle do propojovacího rozhraní.</span><span class="sxs-lookup"><span data-stu-id="7c948-145">When a server wants to send a message to all clients, it sends to the backplane.</span></span> <span data-ttu-id="7c948-146">Propojovacího rozhraní zná všechny připojené klienty a které servery, které jsou uvedené na.</span><span class="sxs-lookup"><span data-stu-id="7c948-146">The backplane knows all connected clients and which servers they're on.</span></span> <span data-ttu-id="7c948-147">Odešle zprávu pro všechny klienty přes jejich příslušné servery.</span><span class="sxs-lookup"><span data-stu-id="7c948-147">It sends the message to all clients via their respective servers.</span></span> <span data-ttu-id="7c948-148">Tento proces je znázorněn v následujícím diagramu:</span><span class="sxs-lookup"><span data-stu-id="7c948-148">This process is illustrated in the following diagram:</span></span>

![Redis propojovací rozhraní systému, zpráv odesílaných z jednoho serveru na všechny klienty](scale/_static/redis-backplane.png)

<span data-ttu-id="7c948-150">Propojovací rozhraní systému Redis je doporučený postup škálování na víc systémů pro aplikace hostované na vlastní infrastrukturu.</span><span class="sxs-lookup"><span data-stu-id="7c948-150">The Redis backplane is the recommended scale-out approach for apps hosted on your own infrastructure.</span></span> <span data-ttu-id="7c948-151">Službě Azure SignalR není vhodným řešením pro použití v produkčním prostředí pomocí místních aplikací kvůli latenci připojení mezi datovým centrem a datového centra Azure.</span><span class="sxs-lookup"><span data-stu-id="7c948-151">Azure SignalR Service isn't a practical option for production use with on-premises apps due to connection latency between your data center and an Azure data center.</span></span>

<span data-ttu-id="7c948-152">Nevýhody pro propojovací rozhraní systému Redis přináší výhody služby Azure SignalR jste si předtím poznamenali:</span><span class="sxs-lookup"><span data-stu-id="7c948-152">The Azure SignalR Service advantages noted earlier are disadvantages for the Redis backplane:</span></span>

* <span data-ttu-id="7c948-153">Rychlé relace, označované také jako [spřažení klienta](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity), je povinný.</span><span class="sxs-lookup"><span data-stu-id="7c948-153">Sticky sessions, also known as [client affinity](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity), is required.</span></span> <span data-ttu-id="7c948-154">Po připojení se zahájí na serveru, má připojení zůstat na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="7c948-154">Once a connection is initiated on a server, the connection has to stay on that server.</span></span>
* <span data-ttu-id="7c948-155">I v případě, že jsou odesílány zprávy několik, musí aplikace SignalR horizontální navýšení kapacity na základě počtu klientů.</span><span class="sxs-lookup"><span data-stu-id="7c948-155">A SignalR app must scale out based on number of clients even if few messages are being sent.</span></span>
* <span data-ttu-id="7c948-156">Aplikace SignalR používá výrazně více prostředků, připojení než webové aplikace bez SignalR.</span><span class="sxs-lookup"><span data-stu-id="7c948-156">A SignalR app uses significantly more connection resources than a web app without SignalR.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c948-157">Další kroky</span><span class="sxs-lookup"><span data-stu-id="7c948-157">Next steps</span></span>

<span data-ttu-id="7c948-158">Další informace naleznete v následujících materiálech:</span><span class="sxs-lookup"><span data-stu-id="7c948-158">For more information, see the following resources:</span></span>

* [<span data-ttu-id="7c948-159">Dokumentace ke službě Azure SignalR služby</span><span class="sxs-lookup"><span data-stu-id="7c948-159">Azure SignalR Service documentation</span></span>](/azure/azure-signalr/signalr-overview)
* [<span data-ttu-id="7c948-160">Nastavit propojovací rozhraní Redis</span><span class="sxs-lookup"><span data-stu-id="7c948-160">Set up a Redis backplane</span></span>](xref:signalr/redis-backplane)