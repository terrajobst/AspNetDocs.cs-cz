---
uid: signalr/overview/performance/scaleout-with-sql-server
title: Škálování signálu pomocí SQL Server | Microsoft Docs
author: bradygaster
description: Verze softwaru používané v tomto tématu Visual Studio 2013 k předchozím verzím tohoto tématu v předchozích verzích rozhraní .NET 4,5 Signaler verze 2, kde najdete informace o dřívějších verzích...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579182"
---
# <a name="signalr-scaleout-with-sql-server"></a>Šklálování aplikace SignalR SQL Serverem

[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Signal – verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

V tomto kurzu použijete SQL Server k distribuci zpráv v aplikaci signalizace, která je nasazená ve dvou samostatných instancích služby IIS. Můžete také spustit tento kurz na jednom testovacím počítači, ale chcete-li získat úplný efekt, je nutné nasadit aplikaci signalizace na dva nebo více serverů. Je také nutné nainstalovat SQL Server na jednom ze serverů nebo na samostatném vyhrazeném serveru. Další možností je spustit kurz s použitím virtuálních počítačů v Azure.

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>Předpoklady

Microsoft SQL Server 2005 nebo novější. Replánování podporuje desktopové i serverové edice SQL Server. Nepodporuje SQL Server Compact edici ani Azure SQL Database. (Pokud je vaše aplikace hostovaná v Azure, zvažte místo toho Service Bus.)

## <a name="overview"></a>Přehled

Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.

1. Vytvořte novou prázdnou databázi. Při replánování se vytvoří potřebné tabulky v této databázi.
2. Přidejte tyto balíčky NuGet do vaší aplikace:

    - [Microsoft. AspNet. Signaler](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. AspNet. Signaler. SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. Vytvořte aplikaci signalizace.
4. Přidáním následujícího kódu do Startup.cs nakonfigurujte schéma pro replánování:

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   Tento kód nakonfiguruje pro replánování výchozí hodnoty pro [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) a [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx). Informace o změně těchto hodnot najdete v tématu [výkon signalizace: metriky škálování](signalr-performance.md#scaleout_metrics).

## <a name="configure-the-database"></a>Konfigurace databáze

Rozhodněte, zda aplikace bude pro přístup k databázi používat ověřování systému Windows nebo ověřování SQL Server. Bez ohledu na to, že uživatel databáze má oprávnění k přihlášení, vytváření schémat a vytváření tabulek.

Vytvořte novou databázi pro plán, který chcete použít. Databázi můžete dát libovolný název. V databázi nemusíte vytvářet žádné tabulky. pro replánování se vytvoří potřebné tabulky.

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Povolit Service Broker

Doporučuje se povolit Service Broker pro databázi pro naplánování. Service Broker poskytuje nativní podporu pro zasílání zpráv a frontu v SQL Server, která umožňuje, aby se aktualizace dostávala efektivněji. (Bez Service Broker ale funguje i bez.)

Chcete-li ověřit, zda je povolena Service Broker, je nutné zadat dotaz na sloupec **is\_Broker\_Enabled** v zobrazení katalogu **Sys. databases** .

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Pokud chcete povolit Service Broker, použijte následující dotaz SQL:

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> Pokud se zobrazí dotaz zablokování, ujistěte se, že neexistují žádné aplikace připojené k databázi.

Pokud jste povolili trasování, trasování zobrazí také, zda je povoleno Service Broker.

## <a name="create-a-signalr-application"></a>Vytvoření aplikace Signal

Pomocí některého z těchto kurzů vytvořte aplikaci signalizace:

- [Začínáme se signálem 2,0](../getting-started/tutorial-getting-started-with-signalr.md)
- [Začínáme s nástrojem Signal 2,0 a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

Dále upravíte aplikaci Chat, aby podporovala horizontální navýšení kapacity SQL Server. Nejprve do svého projektu přidejte balíček NuGet. SqlServer. V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

Pak otevřete soubor Startup.cs. Do metody **Configure** přidejte následující kód:

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>Nasazení a spuštění aplikace

Připraví instance Windows serveru pro nasazení aplikace Signal.

Přidejte roli IIS. Zahrňte funkce pro vývoj aplikací, včetně protokolu WebSocket.

![](scaleout-with-sql-server/_static/image4.png)

Zahrňte také službu správy (v seznamu "nástroje pro správu").

![](scaleout-with-sql-server/_static/image5.png)

**Nainstalujte Nasazení webu 3,0.** Spustíte-li správce služby IIS, zobrazí se výzva k instalaci webové platformy společnosti Microsoft nebo můžete [instalační program stáhnout](https://go.microsoft.com/fwlink/?LinkId=255386). V instalačním programu platformy vyhledejte Nasazení webu a nainstalujte Nasazení webu 3,0

![](scaleout-with-sql-server/_static/image6.png)

Ověřte, zda je spuštěna služba webové správy. V takovém případě službu spusťte. (Pokud se služba webové správy nezobrazuje v seznamu služeb systému Windows, ujistěte se, že jste nainstalovali službu správy při přidání role služby IIS.)

Nakonec otevřete port 8172 pro protokol TCP. Toto je port, který používá nástroj Nasazení webu Tool.

Nyní jste připraveni nasadit projekt sady Visual Studio z vývojového počítače na server. V Průzkumník řešení klikněte pravým tlačítkem na řešení a pak klikněte na **publikovat**.

Podrobnější dokumentaci k nasazení webu najdete v tématu [Mapa obsahu nasazení webu pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).

Pokud nasadíte aplikaci na dva servery, můžete každou instanci otevřít v samostatném okně prohlížeče a podívat se, že každý z nich obdrží zprávy signálu. (Samozřejmě v produkčním prostředí budou dva servery za nástroj pro vyrovnávání zatížení.)

![](scaleout-with-sql-server/_static/image7.png)

Po spuštění aplikace vidíte, že tento signál automaticky vytvořil tabulky v databázi nástroje:

![](scaleout-with-sql-server/_static/image8.png)

Signalizace spravuje tabulky. Pokud je vaše aplikace nasazena, neodstraňujte řádky, upravujte tabulku a tak dále.
