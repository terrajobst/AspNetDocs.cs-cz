---
uid: signalr/overview/performance/scaleout-with-redis
title: Škálování signálu pomocí Redis | Microsoft Docs
author: bradygaster
description: Verze softwaru používané v tomto tématu Visual Studio 2013 k předchozím verzím tohoto tématu v předchozích verzích rozhraní .NET 4,5 Signaler verze 2, kde najdete informace o dřívějších verzích...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579224"
---
# <a name="signalr-scaleout-with-redis"></a><span data-ttu-id="ba056-103">Šklálování aplikace SignalR službou Redis</span><span class="sxs-lookup"><span data-stu-id="ba056-103">SignalR Scaleout with Redis</span></span>

<span data-ttu-id="ba056-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ba056-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="ba056-105">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="ba056-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="ba056-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ba056-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="ba056-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ba056-107">.NET 4.5</span></span>
> - <span data-ttu-id="ba056-108">Signaler verze 2,4</span><span class="sxs-lookup"><span data-stu-id="ba056-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="ba056-109">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="ba056-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="ba056-110">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="ba056-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ba056-111">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="ba056-111">Questions and comments</span></span>
>
> <span data-ttu-id="ba056-112">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="ba056-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ba056-113">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="ba056-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="ba056-114">V tomto kurzu použijete [Redis](http://redis.io/) k distribuci zpráv v aplikaci signalizace, která je nasazená ve dvou samostatných INSTANCÍCH služby IIS.</span><span class="sxs-lookup"><span data-stu-id="ba056-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="ba056-115">Redis je úložiště hodnot klíč-hodnota v paměti.</span><span class="sxs-lookup"><span data-stu-id="ba056-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="ba056-116">Podporuje také systém zasílání zpráv s modelem publikování/odběru.</span><span class="sxs-lookup"><span data-stu-id="ba056-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="ba056-117">Redis pro vyřízení signálu používá funkci Pub/sub k posílání zpráv na jiné servery.</span><span class="sxs-lookup"><span data-stu-id="ba056-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="ba056-118">Pro tento kurz budete používat tři servery:</span><span class="sxs-lookup"><span data-stu-id="ba056-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="ba056-119">Dva servery se systémem Windows, které použijete k nasazení aplikace Signal.</span><span class="sxs-lookup"><span data-stu-id="ba056-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="ba056-120">Jeden server se systémem Linux, který použijete ke spuštění Redis.</span><span class="sxs-lookup"><span data-stu-id="ba056-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="ba056-121">Pro snímky obrazovky v tomto kurzu jsem používal Ubuntu 12,04 TLS.</span><span class="sxs-lookup"><span data-stu-id="ba056-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="ba056-122">Pokud nemáte tři fyzické servery k použití, můžete vytvořit virtuální počítače v prostředí Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ba056-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="ba056-123">Další možností je vytvořit virtuální počítače v Azure.</span><span class="sxs-lookup"><span data-stu-id="ba056-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="ba056-124">I když tento kurz používá oficiální implementaci Redis, existuje taky [Port Windows Redis](https://github.com/MSOpenTech/redis) z MSOpenTech.</span><span class="sxs-lookup"><span data-stu-id="ba056-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="ba056-125">Nastavení a konfigurace se liší, ale v opačném případě se jedná o stejné kroky.</span><span class="sxs-lookup"><span data-stu-id="ba056-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ba056-126">Škálování signálu pomocí Redis nepodporuje clustery Redis.</span><span class="sxs-lookup"><span data-stu-id="ba056-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="ba056-127">Přehled</span><span class="sxs-lookup"><span data-stu-id="ba056-127">Overview</span></span>

<span data-ttu-id="ba056-128">Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="ba056-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="ba056-129">Nainstalujte Redis a spusťte server Redis.</span><span class="sxs-lookup"><span data-stu-id="ba056-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="ba056-130">Přidejte tyto balíčky NuGet do vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="ba056-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="ba056-131">Microsoft. AspNet. Signaler</span><span class="sxs-lookup"><span data-stu-id="ba056-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="ba056-132">Microsoft. AspNet. Signaler. StackExchangeRedis</span><span class="sxs-lookup"><span data-stu-id="ba056-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="ba056-133">Vytvořte aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="ba056-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="ba056-134">Přidáním následujícího kódu do Startup.cs nakonfigurujte schéma pro replánování:</span><span class="sxs-lookup"><span data-stu-id="ba056-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="ba056-135">Ubuntu na Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ba056-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="ba056-136">Pomocí technologie Windows Hyper-V můžete snadno vytvořit virtuální počítač s Ubuntu na Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="ba056-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="ba056-137">Stáhněte si Ubuntu ISO z [http://www.ubuntu.com](http://www.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="ba056-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="ba056-138">V Hyper-V přidejte nový virtuální počítač.</span><span class="sxs-lookup"><span data-stu-id="ba056-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="ba056-139">V kroku **připojit virtuální pevný disk** vyberte možnost **vytvořit virtuální pevný disk**.</span><span class="sxs-lookup"><span data-stu-id="ba056-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="ba056-140">V kroku **Možnosti instalace** vyberte **soubor obrázku (. ISO)** , klikněte na tlačítko **Procházet**a přejděte do Ubuntu instalace ISO.</span><span class="sxs-lookup"><span data-stu-id="ba056-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="ba056-141">Nainstalovat Redis</span><span class="sxs-lookup"><span data-stu-id="ba056-141">Install Redis</span></span>

<span data-ttu-id="ba056-142">Podle pokynů v části [http://redis.io/download](http://redis.io/download) Stáhněte a sestavte Redis.</span><span class="sxs-lookup"><span data-stu-id="ba056-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="ba056-143">Tím se vytvoří binární soubory Redis v adresáři `src`.</span><span class="sxs-lookup"><span data-stu-id="ba056-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="ba056-144">Ve výchozím nastavení Redis nevyžaduje heslo.</span><span class="sxs-lookup"><span data-stu-id="ba056-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="ba056-145">Chcete-li nastavit heslo, upravte soubor `redis.conf`, který je umístěn v kořenovém adresáři zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="ba056-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="ba056-146">(Před úpravou! vytvořte záložní kopii souboru) Přidejte následující direktivu pro `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="ba056-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="ba056-147">Nyní spusťte server Redis:</span><span class="sxs-lookup"><span data-stu-id="ba056-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="ba056-148">Otevřete port 6379, což je výchozí port, na kterém Redis naslouchá.</span><span class="sxs-lookup"><span data-stu-id="ba056-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="ba056-149">(V konfiguračním souboru můžete změnit číslo portu.)</span><span class="sxs-lookup"><span data-stu-id="ba056-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="ba056-150">Vytvoření aplikace Signal</span><span class="sxs-lookup"><span data-stu-id="ba056-150">Create the SignalR Application</span></span>

<span data-ttu-id="ba056-151">Pomocí některého z těchto kurzů vytvořte aplikaci signalizace:</span><span class="sxs-lookup"><span data-stu-id="ba056-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="ba056-152">Začínáme se signálem 2,0</span><span class="sxs-lookup"><span data-stu-id="ba056-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="ba056-153">Začínáme s nástrojem Signal 2,0 a MVC 5</span><span class="sxs-lookup"><span data-stu-id="ba056-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="ba056-154">V dalším kroku změníme aplikaci Chat, aby podporovala horizontální navýšení kapacity pomocí Redis.</span><span class="sxs-lookup"><span data-stu-id="ba056-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="ba056-155">Nejprve do svého projektu přidejte balíček NuGet `Microsoft.AspNet.SignalR.StackExchangeRedis`.</span><span class="sxs-lookup"><span data-stu-id="ba056-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="ba056-156">V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="ba056-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ba056-157">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="ba056-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="ba056-158">Pak otevřete soubor Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="ba056-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="ba056-159">Do metody **Konfigurace** přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="ba056-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="ba056-160">"Server" je název serveru, na kterém běží Redis.</span><span class="sxs-lookup"><span data-stu-id="ba056-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="ba056-161">*port* je číslo portu.</span><span class="sxs-lookup"><span data-stu-id="ba056-161">*port* is the port number</span></span>
- <span data-ttu-id="ba056-162">heslo je heslo, které jste definovali v souboru Redis. conf.</span><span class="sxs-lookup"><span data-stu-id="ba056-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="ba056-163">"AppName" je libovolný řetězec.</span><span class="sxs-lookup"><span data-stu-id="ba056-163">"AppName" is any string.</span></span> <span data-ttu-id="ba056-164">Signal vytvoří Redis kanál pro publikování a podkanál s tímto názvem.</span><span class="sxs-lookup"><span data-stu-id="ba056-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="ba056-165">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ba056-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="ba056-166">Nasazení a spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="ba056-166">Deploy and Run the Application</span></span>

<span data-ttu-id="ba056-167">Připraví instance Windows serveru pro nasazení aplikace Signal.</span><span class="sxs-lookup"><span data-stu-id="ba056-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="ba056-168">Přidejte roli IIS.</span><span class="sxs-lookup"><span data-stu-id="ba056-168">Add the IIS role.</span></span> <span data-ttu-id="ba056-169">Zahrňte funkce pro vývoj aplikací, včetně protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="ba056-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="ba056-170">Zahrňte také službu správy (v seznamu "nástroje pro správu").</span><span class="sxs-lookup"><span data-stu-id="ba056-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="ba056-171">**Nainstalujte Nasazení webu 3,0.**</span><span class="sxs-lookup"><span data-stu-id="ba056-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="ba056-172">Spustíte-li správce služby IIS, zobrazí se výzva k instalaci webové platformy společnosti Microsoft nebo můžete [instalační program stáhnout](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="ba056-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="ba056-173">V instalačním programu platformy vyhledejte Nasazení webu a nainstalujte Nasazení webu 3,0</span><span class="sxs-lookup"><span data-stu-id="ba056-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="ba056-174">Ověřte, zda je spuštěna služba webové správy.</span><span class="sxs-lookup"><span data-stu-id="ba056-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="ba056-175">V takovém případě službu spusťte.</span><span class="sxs-lookup"><span data-stu-id="ba056-175">If not, start the service.</span></span> <span data-ttu-id="ba056-176">(Pokud se služba webové správy nezobrazuje v seznamu služeb systému Windows, ujistěte se, že jste nainstalovali službu správy při přidání role služby IIS.)</span><span class="sxs-lookup"><span data-stu-id="ba056-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="ba056-177">Ve výchozím nastavení služba webové správy naslouchá na portu TCP 8172.</span><span class="sxs-lookup"><span data-stu-id="ba056-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="ba056-178">V bráně Windows Firewall vytvořte nové příchozí pravidlo povolující přenosy TCP na portu 8172.</span><span class="sxs-lookup"><span data-stu-id="ba056-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="ba056-179">Další informace najdete v tématu [Konfigurace pravidel brány firewall](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="ba056-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="ba056-180">(Pokud virtuální počítače hostují v Azure, můžete to provést přímo v Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ba056-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="ba056-181">Přečtěte si téma [nastavení koncových bodů na virtuální počítač](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="ba056-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="ba056-182">Nyní jste připraveni nasadit projekt sady Visual Studio z vývojového počítače na server.</span><span class="sxs-lookup"><span data-stu-id="ba056-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="ba056-183">V Průzkumník řešení klikněte pravým tlačítkem na řešení a pak klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="ba056-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="ba056-184">Podrobnější dokumentaci k nasazení webu najdete v tématu [Mapa obsahu nasazení webu pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="ba056-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="ba056-185">Pokud nasadíte aplikaci na dva servery, můžete každou instanci otevřít v samostatném okně prohlížeče a podívat se, že každý z nich obdrží zprávy signálu.</span><span class="sxs-lookup"><span data-stu-id="ba056-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="ba056-186">(Samozřejmě v produkčním prostředí budou dva servery za nástroj pro vyrovnávání zatížení.)</span><span class="sxs-lookup"><span data-stu-id="ba056-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="ba056-187">Pokud jste zajímá zprávy, které se odesílají do Redis, můžete použít klienta **Redis-CLI** , který se instaluje s Redis.</span><span class="sxs-lookup"><span data-stu-id="ba056-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
