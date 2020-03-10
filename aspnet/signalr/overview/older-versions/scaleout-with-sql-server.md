---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: Horizontální navýšení signálu pomocí SQL Server (Signal 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536468"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a>Škálování aplikace SignalR SQL Serverem (SignalR 1.x)

[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

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
4. Přidejte následující kód do Global. asax ke konfiguraci rozhraní pro naplánování: 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

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

- [Začínáme se signálem](../getting-started/tutorial-getting-started-with-signalr.md)
- [Začínáme s nástrojem Signal a MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)

Dále upravíte aplikaci Chat, aby podporovala horizontální navýšení kapacity SQL Server. Nejprve do svého projektu přidejte balíček NuGet. SqlServer. V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

Potom otevřete soubor Global. asax. Do **aplikace\_začátek** metody přidejte následující kód:

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
