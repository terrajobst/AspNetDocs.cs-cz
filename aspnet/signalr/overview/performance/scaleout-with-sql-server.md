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
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="87e9c-103">Šklálování aplikace SignalR SQL Serverem</span><span class="sxs-lookup"><span data-stu-id="87e9c-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="87e9c-104">[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="87e9c-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="87e9c-105">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="87e9c-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="87e9c-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="87e9c-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="87e9c-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="87e9c-107">.NET 4.5</span></span>
> - <span data-ttu-id="87e9c-108">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="87e9c-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="87e9c-109">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="87e9c-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="87e9c-110">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="87e9c-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="87e9c-111">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="87e9c-111">Questions and comments</span></span>
>
> <span data-ttu-id="87e9c-112">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="87e9c-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="87e9c-113">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="87e9c-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="87e9c-114">V tomto kurzu použijete SQL Server k distribuci zpráv v aplikaci signalizace, která je nasazená ve dvou samostatných instancích služby IIS.</span><span class="sxs-lookup"><span data-stu-id="87e9c-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="87e9c-115">Můžete také spustit tento kurz na jednom testovacím počítači, ale chcete-li získat úplný efekt, je nutné nasadit aplikaci signalizace na dva nebo více serverů.</span><span class="sxs-lookup"><span data-stu-id="87e9c-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="87e9c-116">Je také nutné nainstalovat SQL Server na jednom ze serverů nebo na samostatném vyhrazeném serveru.</span><span class="sxs-lookup"><span data-stu-id="87e9c-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="87e9c-117">Další možností je spustit kurz s použitím virtuálních počítačů v Azure.</span><span class="sxs-lookup"><span data-stu-id="87e9c-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="87e9c-118">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="87e9c-118">Prerequisites</span></span>

<span data-ttu-id="87e9c-119">Microsoft SQL Server 2005 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="87e9c-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="87e9c-120">Replánování podporuje desktopové i serverové edice SQL Server.</span><span class="sxs-lookup"><span data-stu-id="87e9c-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="87e9c-121">Nepodporuje SQL Server Compact edici ani Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="87e9c-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="87e9c-122">(Pokud je vaše aplikace hostovaná v Azure, zvažte místo toho Service Bus.)</span><span class="sxs-lookup"><span data-stu-id="87e9c-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="87e9c-123">Přehled</span><span class="sxs-lookup"><span data-stu-id="87e9c-123">Overview</span></span>

<span data-ttu-id="87e9c-124">Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="87e9c-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="87e9c-125">Vytvořte novou prázdnou databázi.</span><span class="sxs-lookup"><span data-stu-id="87e9c-125">Create a new empty database.</span></span> <span data-ttu-id="87e9c-126">Při replánování se vytvoří potřebné tabulky v této databázi.</span><span class="sxs-lookup"><span data-stu-id="87e9c-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="87e9c-127">Přidejte tyto balíčky NuGet do vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="87e9c-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="87e9c-128">Microsoft. AspNet. Signaler</span><span class="sxs-lookup"><span data-stu-id="87e9c-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="87e9c-129">Microsoft. AspNet. Signaler. SqlServer</span><span class="sxs-lookup"><span data-stu-id="87e9c-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="87e9c-130">Vytvořte aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="87e9c-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="87e9c-131">Přidáním následujícího kódu do Startup.cs nakonfigurujte schéma pro replánování:</span><span class="sxs-lookup"><span data-stu-id="87e9c-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="87e9c-132">Tento kód nakonfiguruje pro replánování výchozí hodnoty pro [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) a [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span><span class="sxs-lookup"><span data-stu-id="87e9c-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="87e9c-133">Informace o změně těchto hodnot najdete v tématu [výkon signalizace: metriky škálování](signalr-performance.md#scaleout_metrics).</span><span class="sxs-lookup"><span data-stu-id="87e9c-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="87e9c-134">Konfigurace databáze</span><span class="sxs-lookup"><span data-stu-id="87e9c-134">Configure the Database</span></span>

<span data-ttu-id="87e9c-135">Rozhodněte, zda aplikace bude pro přístup k databázi používat ověřování systému Windows nebo ověřování SQL Server.</span><span class="sxs-lookup"><span data-stu-id="87e9c-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="87e9c-136">Bez ohledu na to, že uživatel databáze má oprávnění k přihlášení, vytváření schémat a vytváření tabulek.</span><span class="sxs-lookup"><span data-stu-id="87e9c-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="87e9c-137">Vytvořte novou databázi pro plán, který chcete použít.</span><span class="sxs-lookup"><span data-stu-id="87e9c-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="87e9c-138">Databázi můžete dát libovolný název.</span><span class="sxs-lookup"><span data-stu-id="87e9c-138">You can give the database any name.</span></span> <span data-ttu-id="87e9c-139">V databázi nemusíte vytvářet žádné tabulky. pro replánování se vytvoří potřebné tabulky.</span><span class="sxs-lookup"><span data-stu-id="87e9c-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="87e9c-140">Povolit Service Broker</span><span class="sxs-lookup"><span data-stu-id="87e9c-140">Enable Service Broker</span></span>

<span data-ttu-id="87e9c-141">Doporučuje se povolit Service Broker pro databázi pro naplánování.</span><span class="sxs-lookup"><span data-stu-id="87e9c-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="87e9c-142">Service Broker poskytuje nativní podporu pro zasílání zpráv a frontu v SQL Server, která umožňuje, aby se aktualizace dostávala efektivněji.</span><span class="sxs-lookup"><span data-stu-id="87e9c-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="87e9c-143">(Bez Service Broker ale funguje i bez.)</span><span class="sxs-lookup"><span data-stu-id="87e9c-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="87e9c-144">Chcete-li ověřit, zda je povolena Service Broker, je nutné zadat dotaz na sloupec **is\_Broker\_Enabled** v zobrazení katalogu **Sys. databases** .</span><span class="sxs-lookup"><span data-stu-id="87e9c-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="87e9c-145">Pokud chcete povolit Service Broker, použijte následující dotaz SQL:</span><span class="sxs-lookup"><span data-stu-id="87e9c-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="87e9c-146">Pokud se zobrazí dotaz zablokování, ujistěte se, že neexistují žádné aplikace připojené k databázi.</span><span class="sxs-lookup"><span data-stu-id="87e9c-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="87e9c-147">Pokud jste povolili trasování, trasování zobrazí také, zda je povoleno Service Broker.</span><span class="sxs-lookup"><span data-stu-id="87e9c-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="87e9c-148">Vytvoření aplikace Signal</span><span class="sxs-lookup"><span data-stu-id="87e9c-148">Create a SignalR Application</span></span>

<span data-ttu-id="87e9c-149">Pomocí některého z těchto kurzů vytvořte aplikaci signalizace:</span><span class="sxs-lookup"><span data-stu-id="87e9c-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="87e9c-150">Začínáme se signálem 2,0</span><span class="sxs-lookup"><span data-stu-id="87e9c-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="87e9c-151">Začínáme s nástrojem Signal 2,0 a MVC 5</span><span class="sxs-lookup"><span data-stu-id="87e9c-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="87e9c-152">Dále upravíte aplikaci Chat, aby podporovala horizontální navýšení kapacity SQL Server.</span><span class="sxs-lookup"><span data-stu-id="87e9c-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="87e9c-153">Nejprve do svého projektu přidejte balíček NuGet. SqlServer.</span><span class="sxs-lookup"><span data-stu-id="87e9c-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="87e9c-154">V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="87e9c-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="87e9c-155">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="87e9c-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="87e9c-156">Pak otevřete soubor Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="87e9c-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="87e9c-157">Do metody **Configure** přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="87e9c-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="87e9c-158">Nasazení a spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="87e9c-158">Deploy and Run the Application</span></span>

<span data-ttu-id="87e9c-159">Připraví instance Windows serveru pro nasazení aplikace Signal.</span><span class="sxs-lookup"><span data-stu-id="87e9c-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="87e9c-160">Přidejte roli IIS.</span><span class="sxs-lookup"><span data-stu-id="87e9c-160">Add the IIS role.</span></span> <span data-ttu-id="87e9c-161">Zahrňte funkce pro vývoj aplikací, včetně protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="87e9c-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="87e9c-162">Zahrňte také službu správy (v seznamu "nástroje pro správu").</span><span class="sxs-lookup"><span data-stu-id="87e9c-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="87e9c-163">**Nainstalujte Nasazení webu 3,0.**</span><span class="sxs-lookup"><span data-stu-id="87e9c-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="87e9c-164">Spustíte-li správce služby IIS, zobrazí se výzva k instalaci webové platformy společnosti Microsoft nebo můžete [instalační program stáhnout](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="87e9c-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="87e9c-165">V instalačním programu platformy vyhledejte Nasazení webu a nainstalujte Nasazení webu 3,0</span><span class="sxs-lookup"><span data-stu-id="87e9c-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="87e9c-166">Ověřte, zda je spuštěna služba webové správy.</span><span class="sxs-lookup"><span data-stu-id="87e9c-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="87e9c-167">V takovém případě službu spusťte.</span><span class="sxs-lookup"><span data-stu-id="87e9c-167">If not, start the service.</span></span> <span data-ttu-id="87e9c-168">(Pokud se služba webové správy nezobrazuje v seznamu služeb systému Windows, ujistěte se, že jste nainstalovali službu správy při přidání role služby IIS.)</span><span class="sxs-lookup"><span data-stu-id="87e9c-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="87e9c-169">Nakonec otevřete port 8172 pro protokol TCP.</span><span class="sxs-lookup"><span data-stu-id="87e9c-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="87e9c-170">Toto je port, který používá nástroj Nasazení webu Tool.</span><span class="sxs-lookup"><span data-stu-id="87e9c-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="87e9c-171">Nyní jste připraveni nasadit projekt sady Visual Studio z vývojového počítače na server.</span><span class="sxs-lookup"><span data-stu-id="87e9c-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="87e9c-172">V Průzkumník řešení klikněte pravým tlačítkem na řešení a pak klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="87e9c-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="87e9c-173">Podrobnější dokumentaci k nasazení webu najdete v tématu [Mapa obsahu nasazení webu pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="87e9c-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="87e9c-174">Pokud nasadíte aplikaci na dva servery, můžete každou instanci otevřít v samostatném okně prohlížeče a podívat se, že každý z nich obdrží zprávy signálu.</span><span class="sxs-lookup"><span data-stu-id="87e9c-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="87e9c-175">(Samozřejmě v produkčním prostředí budou dva servery za nástroj pro vyrovnávání zatížení.)</span><span class="sxs-lookup"><span data-stu-id="87e9c-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="87e9c-176">Po spuštění aplikace vidíte, že tento signál automaticky vytvořil tabulky v databázi nástroje:</span><span class="sxs-lookup"><span data-stu-id="87e9c-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="87e9c-177">Signalizace spravuje tabulky.</span><span class="sxs-lookup"><span data-stu-id="87e9c-177">SignalR manages the tables.</span></span> <span data-ttu-id="87e9c-178">Pokud je vaše aplikace nasazena, neodstraňujte řádky, upravujte tabulku a tak dále.</span><span class="sxs-lookup"><span data-stu-id="87e9c-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
