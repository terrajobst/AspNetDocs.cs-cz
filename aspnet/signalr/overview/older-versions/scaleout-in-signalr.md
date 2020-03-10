---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: Úvod do horizontálního navýšení kapacity v nástroji Signal 1. x | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 04/29/2013
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9bad72d31a0ebc491910ebb128b3b3a7fb537958
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536566"
---
# <a name="introduction-to-scaleout-in-signalr-1x"></a>Úvod do škálování aplikace SignalR 1.x

[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Obecně existují dva způsoby škálování webové aplikace: *horizontální navýšení* kapacity a *horizontální*navýšení kapacity.

- Horizontální navýšení kapacity prostřednictvím většího serveru (nebo většího virtuálního počítače) s větším množstvím paměti RAM, procesorů atd.
- Horizontální navýšení kapacity znamená přidání dalších serverů pro zpracování zatížení.

Problém s horizontálním škálováním je, že rychle vysáhnete velikost počítače. Kromě toho je nutné horizontální navýšení kapacity. Při horizontálním navýšení kapacity ale klienti můžou směrovat na různé servery. Klient, který je připojen k jednomu serveru, nebude přijímat zprávy odesílané z jiného serveru.

![](scaleout-in-signalr/_static/image1.png)

Jedním z řešení je přeposílání zpráv mezi servery pomocí komponenty s názvem *plán*. Když je povolený plán, každá instance aplikace odesílá zprávy do plánu pro replánování a znovu je přenáší do ostatních instancí aplikace. (V elektronikě je skupina pro replán typu "Parallel Connectors". Pomocí analogie naplánuje se signál k naplánování několika serverů.)

![](scaleout-in-signalr/_static/image2.png)

Signal v současné době poskytuje tři řídicí plány:

- **Azure Service Bus**. Service Bus je infrastruktura zasílání zpráv, která umožňuje komponentám posílání zpráv volně přizpůsobovat.
- **Redis**. Redis je úložiště hodnot klíč-hodnota v paměti. Redis podporuje vzor publikování/odběru ("pub/sub") pro posílání zpráv.
- **SQL Server**. SQL Server pro naplánování zapisuje zprávy do tabulek SQL. Plán pro použití Service Broker pro efektivní zasílání zpráv používá. Ale funguje i v případě, že Service Broker není povolená.

Pokud nasadíte aplikaci do Azure, zvažte použití Azure Service Busho plánu. Pokud nasazujete na vlastní serverovou farmu, zvažte SQL Server nebo Redis.

Následující témata obsahují podrobné kurzy pro každé schéma:

- [Škálování aplikace SignalR službou Azure Service Bus](scaleout-with-windows-azure-service-bus.md)
- [Šklálování aplikace SignalR službou Redis](scaleout-with-redis.md)
- [Šklálování aplikace SignalR SQL Serverem](scaleout-with-sql-server.md)

## <a name="implementation"></a>Implementace

V nástroji Signal se každá zpráva odesílá prostřednictvím sběrnice zpráv. Sběrnice zpráv implementuje rozhraní [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) , které poskytuje abstrakci pro publikování/odběr. Plán funguje tak, že nahradí výchozí **IMessageBus** sběrnicí, která je navržena pro tento plán. Například sběrnice zpráv pro Redis je [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)a k posílání a přijímání zpráv používá mechanismus Redis [Pub/sub](http://redis.io/topics/pubsub) .

Každá instance serveru se připojuje k vašemu schématu prostřednictvím sběrnice. Když se pošle zpráva, přejde do plánu pro replánování a znovu ho pošle na každý server. Když server získá zprávu z příkazového schématu, umístí zprávu do místní mezipaměti. Server pak doručuje zprávy klientům z místní mezipaměti.

Pro každé připojení klienta je průběh čtení streamu zprávy sledován pomocí kurzoru. (Kurzor představuje pozici v datovém proudu zpráv.) Pokud se klient odpojí a pak znovu připojí, požádá o sběrnici všechny zprávy, které dorazily po hodnotě kurzoru klienta. K tomu dochází, když připojení používá [dlouhé cyklické dotazování](../getting-started/introduction-to-signalr.md#transports). Po dokončení dlouhé žádosti o dotazování klient otevře nové připojení a požádá o zprávy, které dorazily po kurzoru.

Mechanismus kurzoru funguje i v případě, že je klient směrován na jiný server při opětovném připojení. Replánování ví o všech serverech a nezáleží na tom, ke kterému serveru se klient připojuje.

## <a name="limitations"></a>Omezení

Při použití schématu pro replánování je maximální propustnost zpráv nižší než v případě, že klienti komunikují přímo na jednom uzlu serveru. Důvodem je, že příkaz replán přepošle každou zprávu na každý uzel, takže se může stát, že by se plán znovu stal kritickým bodem. Bez ohledu na to, jestli se jedná o problém, závisí na aplikaci. Tady je například několik typických scénářů signalizace:

- [Všesměrové vysílání serveru](tutorial-server-broadcast-with-aspnet-signalr.md) (např. burzovní modul): v tomto scénáři dobře funguje plán, protože server řídí rychlost odesílání zpráv.
- [Klient-klient](tutorial-getting-started-with-signalr.md) (např. chat): v tomto scénáři může být plán opětovného použití kritický, pokud se počet zpráv škáluje s počtem klientů. To znamená, že pokud se rychlost zpráv postupně zvětšuje při připojování více klientů.
- [Vysoká frekvence v reálném](tutorial-high-frequency-realtime-with-signalr.md) čase (například hry v reálném čase): pro tento scénář se nedoporučuje použití schématu pro replánování.

## <a name="enabling-tracing-for-signalr-scaleout"></a>Povolení trasování pro škálování signálu

Chcete-li povolit trasování pro nové plány, přidejte následující části do souboru Web. config v kořenovém elementu **Konfigurace** :

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
