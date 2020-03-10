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
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="dc06d-102">Škálování aplikace SignalR SQL Serverem (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="dc06d-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>

<span data-ttu-id="dc06d-103">[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="dc06d-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="dc06d-104">V tomto kurzu použijete SQL Server k distribuci zpráv v aplikaci signalizace, která je nasazená ve dvou samostatných instancích služby IIS.</span><span class="sxs-lookup"><span data-stu-id="dc06d-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="dc06d-105">Můžete také spustit tento kurz na jednom testovacím počítači, ale chcete-li získat úplný efekt, je nutné nasadit aplikaci signalizace na dva nebo více serverů.</span><span class="sxs-lookup"><span data-stu-id="dc06d-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="dc06d-106">Je také nutné nainstalovat SQL Server na jednom ze serverů nebo na samostatném vyhrazeném serveru.</span><span class="sxs-lookup"><span data-stu-id="dc06d-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="dc06d-107">Další možností je spustit kurz s použitím virtuálních počítačů v Azure.</span><span class="sxs-lookup"><span data-stu-id="dc06d-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="dc06d-108">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="dc06d-108">Prerequisites</span></span>

<span data-ttu-id="dc06d-109">Microsoft SQL Server 2005 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="dc06d-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="dc06d-110">Replánování podporuje desktopové i serverové edice SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dc06d-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="dc06d-111">Nepodporuje SQL Server Compact edici ani Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="dc06d-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="dc06d-112">(Pokud je vaše aplikace hostovaná v Azure, zvažte místo toho Service Bus.)</span><span class="sxs-lookup"><span data-stu-id="dc06d-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="dc06d-113">Přehled</span><span class="sxs-lookup"><span data-stu-id="dc06d-113">Overview</span></span>

<span data-ttu-id="dc06d-114">Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="dc06d-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="dc06d-115">Vytvořte novou prázdnou databázi.</span><span class="sxs-lookup"><span data-stu-id="dc06d-115">Create a new empty database.</span></span> <span data-ttu-id="dc06d-116">Při replánování se vytvoří potřebné tabulky v této databázi.</span><span class="sxs-lookup"><span data-stu-id="dc06d-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="dc06d-117">Přidejte tyto balíčky NuGet do vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="dc06d-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="dc06d-118">Microsoft. AspNet. Signaler</span><span class="sxs-lookup"><span data-stu-id="dc06d-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="dc06d-119">Microsoft. AspNet. Signaler. SqlServer</span><span class="sxs-lookup"><span data-stu-id="dc06d-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="dc06d-120">Vytvořte aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="dc06d-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="dc06d-121">Přidejte následující kód do Global. asax ke konfiguraci rozhraní pro naplánování:</span><span class="sxs-lookup"><span data-stu-id="dc06d-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="dc06d-122">Konfigurace databáze</span><span class="sxs-lookup"><span data-stu-id="dc06d-122">Configure the Database</span></span>

<span data-ttu-id="dc06d-123">Rozhodněte, zda aplikace bude pro přístup k databázi používat ověřování systému Windows nebo ověřování SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dc06d-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="dc06d-124">Bez ohledu na to, že uživatel databáze má oprávnění k přihlášení, vytváření schémat a vytváření tabulek.</span><span class="sxs-lookup"><span data-stu-id="dc06d-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="dc06d-125">Vytvořte novou databázi pro plán, který chcete použít.</span><span class="sxs-lookup"><span data-stu-id="dc06d-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="dc06d-126">Databázi můžete dát libovolný název.</span><span class="sxs-lookup"><span data-stu-id="dc06d-126">You can give the database any name.</span></span> <span data-ttu-id="dc06d-127">V databázi nemusíte vytvářet žádné tabulky. pro replánování se vytvoří potřebné tabulky.</span><span class="sxs-lookup"><span data-stu-id="dc06d-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="dc06d-128">Povolit Service Broker</span><span class="sxs-lookup"><span data-stu-id="dc06d-128">Enable Service Broker</span></span>

<span data-ttu-id="dc06d-129">Doporučuje se povolit Service Broker pro databázi pro naplánování.</span><span class="sxs-lookup"><span data-stu-id="dc06d-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="dc06d-130">Service Broker poskytuje nativní podporu pro zasílání zpráv a frontu v SQL Server, která umožňuje, aby se aktualizace dostávala efektivněji.</span><span class="sxs-lookup"><span data-stu-id="dc06d-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="dc06d-131">(Bez Service Broker ale funguje i bez.)</span><span class="sxs-lookup"><span data-stu-id="dc06d-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="dc06d-132">Chcete-li ověřit, zda je povolena Service Broker, je nutné zadat dotaz na sloupec **is\_Broker\_Enabled** v zobrazení katalogu **Sys. databases** .</span><span class="sxs-lookup"><span data-stu-id="dc06d-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="dc06d-133">Pokud chcete povolit Service Broker, použijte následující dotaz SQL:</span><span class="sxs-lookup"><span data-stu-id="dc06d-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="dc06d-134">Pokud se zobrazí dotaz zablokování, ujistěte se, že neexistují žádné aplikace připojené k databázi.</span><span class="sxs-lookup"><span data-stu-id="dc06d-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="dc06d-135">Pokud jste povolili trasování, trasování zobrazí také, zda je povoleno Service Broker.</span><span class="sxs-lookup"><span data-stu-id="dc06d-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="dc06d-136">Vytvoření aplikace Signal</span><span class="sxs-lookup"><span data-stu-id="dc06d-136">Create a SignalR Application</span></span>

<span data-ttu-id="dc06d-137">Pomocí některého z těchto kurzů vytvořte aplikaci signalizace:</span><span class="sxs-lookup"><span data-stu-id="dc06d-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="dc06d-138">Začínáme se signálem</span><span class="sxs-lookup"><span data-stu-id="dc06d-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="dc06d-139">Začínáme s nástrojem Signal a MVC 4</span><span class="sxs-lookup"><span data-stu-id="dc06d-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="dc06d-140">Dále upravíte aplikaci Chat, aby podporovala horizontální navýšení kapacity SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dc06d-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="dc06d-141">Nejprve do svého projektu přidejte balíček NuGet. SqlServer.</span><span class="sxs-lookup"><span data-stu-id="dc06d-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="dc06d-142">V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="dc06d-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="dc06d-143">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="dc06d-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="dc06d-144">Potom otevřete soubor Global. asax.</span><span class="sxs-lookup"><span data-stu-id="dc06d-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="dc06d-145">Do **aplikace\_začátek** metody přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="dc06d-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="dc06d-146">Nasazení a spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="dc06d-146">Deploy and Run the Application</span></span>

<span data-ttu-id="dc06d-147">Připraví instance Windows serveru pro nasazení aplikace Signal.</span><span class="sxs-lookup"><span data-stu-id="dc06d-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="dc06d-148">Přidejte roli IIS.</span><span class="sxs-lookup"><span data-stu-id="dc06d-148">Add the IIS role.</span></span> <span data-ttu-id="dc06d-149">Zahrňte funkce pro vývoj aplikací, včetně protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="dc06d-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="dc06d-150">Zahrňte také službu správy (v seznamu "nástroje pro správu").</span><span class="sxs-lookup"><span data-stu-id="dc06d-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="dc06d-151">**Nainstalujte Nasazení webu 3,0.**</span><span class="sxs-lookup"><span data-stu-id="dc06d-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="dc06d-152">Spustíte-li správce služby IIS, zobrazí se výzva k instalaci webové platformy společnosti Microsoft nebo můžete [instalační program stáhnout](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="dc06d-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="dc06d-153">V instalačním programu platformy vyhledejte Nasazení webu a nainstalujte Nasazení webu 3,0</span><span class="sxs-lookup"><span data-stu-id="dc06d-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="dc06d-154">Ověřte, zda je spuštěna služba webové správy.</span><span class="sxs-lookup"><span data-stu-id="dc06d-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="dc06d-155">V takovém případě službu spusťte.</span><span class="sxs-lookup"><span data-stu-id="dc06d-155">If not, start the service.</span></span> <span data-ttu-id="dc06d-156">(Pokud se služba webové správy nezobrazuje v seznamu služeb systému Windows, ujistěte se, že jste nainstalovali službu správy při přidání role služby IIS.)</span><span class="sxs-lookup"><span data-stu-id="dc06d-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="dc06d-157">Nakonec otevřete port 8172 pro protokol TCP.</span><span class="sxs-lookup"><span data-stu-id="dc06d-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="dc06d-158">Toto je port, který používá nástroj Nasazení webu Tool.</span><span class="sxs-lookup"><span data-stu-id="dc06d-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="dc06d-159">Nyní jste připraveni nasadit projekt sady Visual Studio z vývojového počítače na server.</span><span class="sxs-lookup"><span data-stu-id="dc06d-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="dc06d-160">V Průzkumník řešení klikněte pravým tlačítkem na řešení a pak klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="dc06d-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="dc06d-161">Podrobnější dokumentaci k nasazení webu najdete v tématu [Mapa obsahu nasazení webu pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="dc06d-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="dc06d-162">Pokud nasadíte aplikaci na dva servery, můžete každou instanci otevřít v samostatném okně prohlížeče a podívat se, že každý z nich obdrží zprávy signálu.</span><span class="sxs-lookup"><span data-stu-id="dc06d-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="dc06d-163">(Samozřejmě v produkčním prostředí budou dva servery za nástroj pro vyrovnávání zatížení.)</span><span class="sxs-lookup"><span data-stu-id="dc06d-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="dc06d-164">Po spuštění aplikace vidíte, že tento signál automaticky vytvořil tabulky v databázi nástroje:</span><span class="sxs-lookup"><span data-stu-id="dc06d-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="dc06d-165">Signalizace spravuje tabulky.</span><span class="sxs-lookup"><span data-stu-id="dc06d-165">SignalR manages the tables.</span></span> <span data-ttu-id="dc06d-166">Pokud je vaše aplikace nasazena, neodstraňujte řádky, upravujte tabulku a tak dále.</span><span class="sxs-lookup"><span data-stu-id="dc06d-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
