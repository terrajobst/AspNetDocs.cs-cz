---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Škálování signálu pomocí Redis (Signaler 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536559"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="17149-102">Škálování aplikace SignalR službou Redis (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="17149-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>

<span data-ttu-id="17149-103">[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="17149-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="17149-104">V tomto kurzu použijete [Redis](http://redis.io/) k distribuci zpráv v aplikaci signalizace, která je nasazená ve dvou samostatných INSTANCÍCH služby IIS.</span><span class="sxs-lookup"><span data-stu-id="17149-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="17149-105">Redis je úložiště hodnot klíč-hodnota v paměti.</span><span class="sxs-lookup"><span data-stu-id="17149-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="17149-106">Podporuje také systém zasílání zpráv s modelem publikování/odběru.</span><span class="sxs-lookup"><span data-stu-id="17149-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="17149-107">Redis pro vyřízení signálu používá funkci Pub/sub k posílání zpráv na jiné servery.</span><span class="sxs-lookup"><span data-stu-id="17149-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="17149-108">Pro tento kurz budete používat tři servery:</span><span class="sxs-lookup"><span data-stu-id="17149-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="17149-109">Dva servery se systémem Windows, které použijete k nasazení aplikace Signal.</span><span class="sxs-lookup"><span data-stu-id="17149-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="17149-110">Jeden server se systémem Linux, který použijete ke spuštění Redis.</span><span class="sxs-lookup"><span data-stu-id="17149-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="17149-111">Pro snímky obrazovky v tomto kurzu jsem používal Ubuntu 12,04 TLS.</span><span class="sxs-lookup"><span data-stu-id="17149-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="17149-112">Pokud nemáte tři fyzické servery k použití, můžete vytvořit virtuální počítače v prostředí Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="17149-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="17149-113">Další možností je vytvořit virtuální počítače v Azure.</span><span class="sxs-lookup"><span data-stu-id="17149-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="17149-114">I když tento kurz používá oficiální implementaci Redis, existuje taky [Port Windows Redis](https://github.com/MSOpenTech/redis) z MSOpenTech.</span><span class="sxs-lookup"><span data-stu-id="17149-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="17149-115">Nastavení a konfigurace se liší, ale v opačném případě se jedná o stejné kroky.</span><span class="sxs-lookup"><span data-stu-id="17149-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="17149-116">Škálování signálu pomocí Redis nepodporuje clustery Redis.</span><span class="sxs-lookup"><span data-stu-id="17149-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="17149-117">Přehled</span><span class="sxs-lookup"><span data-stu-id="17149-117">Overview</span></span>

<span data-ttu-id="17149-118">Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="17149-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="17149-119">Nainstalujte Redis a spusťte server Redis.</span><span class="sxs-lookup"><span data-stu-id="17149-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="17149-120">Přidejte tyto balíčky NuGet do vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="17149-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="17149-121">Microsoft. AspNet. Signaler</span><span class="sxs-lookup"><span data-stu-id="17149-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="17149-122">Microsoft. AspNet. Signaler. Redis</span><span class="sxs-lookup"><span data-stu-id="17149-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="17149-123">Vytvořte aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="17149-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="17149-124">Přidejte následující kód do Global. asax ke konfiguraci rozhraní pro naplánování:</span><span class="sxs-lookup"><span data-stu-id="17149-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="17149-125">Ubuntu na Hyper-V</span><span class="sxs-lookup"><span data-stu-id="17149-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="17149-126">Pomocí technologie Windows Hyper-V můžete snadno vytvořit virtuální počítač s Ubuntu na Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="17149-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="17149-127">Stáhněte si Ubuntu ISO z [http://www.ubuntu.com](http://www.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="17149-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="17149-128">V Hyper-V přidejte nový virtuální počítač.</span><span class="sxs-lookup"><span data-stu-id="17149-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="17149-129">V kroku **připojit virtuální pevný disk** vyberte možnost **vytvořit virtuální pevný disk**.</span><span class="sxs-lookup"><span data-stu-id="17149-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="17149-130">V kroku **Možnosti instalace** vyberte **soubor obrázku (. ISO)** , klikněte na tlačítko **Procházet**a přejděte do Ubuntu instalace ISO.</span><span class="sxs-lookup"><span data-stu-id="17149-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="17149-131">Nainstalovat Redis</span><span class="sxs-lookup"><span data-stu-id="17149-131">Install Redis</span></span>

<span data-ttu-id="17149-132">Podle pokynů v části [http://redis.io/download](http://redis.io/download) Stáhněte a sestavte Redis.</span><span class="sxs-lookup"><span data-stu-id="17149-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="17149-133">Tím se vytvoří binární soubory Redis v adresáři `src`.</span><span class="sxs-lookup"><span data-stu-id="17149-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="17149-134">Ve výchozím nastavení Redis nevyžaduje heslo.</span><span class="sxs-lookup"><span data-stu-id="17149-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="17149-135">Chcete-li nastavit heslo, upravte soubor `redis.conf`, který je umístěn v kořenovém adresáři zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="17149-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="17149-136">(Před úpravou! vytvořte záložní kopii souboru) Přidejte následující direktivu pro `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="17149-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="17149-137">Nyní spusťte server Redis:</span><span class="sxs-lookup"><span data-stu-id="17149-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="17149-138">Otevřete port 6379, což je výchozí port, na kterém Redis naslouchá.</span><span class="sxs-lookup"><span data-stu-id="17149-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="17149-139">(V konfiguračním souboru můžete změnit číslo portu.)</span><span class="sxs-lookup"><span data-stu-id="17149-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="17149-140">Vytvoření aplikace Signal</span><span class="sxs-lookup"><span data-stu-id="17149-140">Create the SignalR Application</span></span>

<span data-ttu-id="17149-141">Pomocí některého z těchto kurzů vytvořte aplikaci signalizace:</span><span class="sxs-lookup"><span data-stu-id="17149-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="17149-142">Začínáme se signálem</span><span class="sxs-lookup"><span data-stu-id="17149-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="17149-143">Začínáme s nástrojem Signal a MVC 4</span><span class="sxs-lookup"><span data-stu-id="17149-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="17149-144">V dalším kroku změníme aplikaci Chat, aby podporovala horizontální navýšení kapacity pomocí Redis.</span><span class="sxs-lookup"><span data-stu-id="17149-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="17149-145">Nejprve do svého projektu přidejte balíček NuGet. Redis NuGet.</span><span class="sxs-lookup"><span data-stu-id="17149-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="17149-146">V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="17149-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="17149-147">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="17149-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="17149-148">Potom otevřete soubor Global. asax.</span><span class="sxs-lookup"><span data-stu-id="17149-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="17149-149">Do **aplikace\_začátek** metody přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="17149-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="17149-150">"Server" je název serveru, na kterém běží Redis.</span><span class="sxs-lookup"><span data-stu-id="17149-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="17149-151">*port* je číslo portu.</span><span class="sxs-lookup"><span data-stu-id="17149-151">*port* is the port number</span></span>
- <span data-ttu-id="17149-152">heslo je heslo, které jste definovali v souboru Redis. conf.</span><span class="sxs-lookup"><span data-stu-id="17149-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="17149-153">"AppName" je libovolný řetězec.</span><span class="sxs-lookup"><span data-stu-id="17149-153">"AppName" is any string.</span></span> <span data-ttu-id="17149-154">Signal vytvoří Redis kanál pro publikování a podkanál s tímto názvem.</span><span class="sxs-lookup"><span data-stu-id="17149-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="17149-155">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17149-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="17149-156">Nasazení a spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="17149-156">Deploy and Run the Application</span></span>

<span data-ttu-id="17149-157">Připraví instance Windows serveru pro nasazení aplikace Signal.</span><span class="sxs-lookup"><span data-stu-id="17149-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="17149-158">Přidejte roli IIS.</span><span class="sxs-lookup"><span data-stu-id="17149-158">Add the IIS role.</span></span> <span data-ttu-id="17149-159">Zahrňte funkce pro vývoj aplikací, včetně protokolu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="17149-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="17149-160">Zahrňte také službu správy (v seznamu "nástroje pro správu").</span><span class="sxs-lookup"><span data-stu-id="17149-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="17149-161">**Nainstalujte Nasazení webu 3,0.**</span><span class="sxs-lookup"><span data-stu-id="17149-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="17149-162">Spustíte-li správce služby IIS, zobrazí se výzva k instalaci webové platformy společnosti Microsoft nebo můžete [instalační program stáhnout](https://go.microsoft.com/fwlink/?LinkId=255386).</span><span class="sxs-lookup"><span data-stu-id="17149-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="17149-163">V instalačním programu platformy vyhledejte Nasazení webu a nainstalujte Nasazení webu 3,0</span><span class="sxs-lookup"><span data-stu-id="17149-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="17149-164">Ověřte, zda je spuštěna služba webové správy.</span><span class="sxs-lookup"><span data-stu-id="17149-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="17149-165">V takovém případě službu spusťte.</span><span class="sxs-lookup"><span data-stu-id="17149-165">If not, start the service.</span></span> <span data-ttu-id="17149-166">(Pokud se služba webové správy nezobrazuje v seznamu služeb systému Windows, ujistěte se, že jste nainstalovali službu správy při přidání role služby IIS.)</span><span class="sxs-lookup"><span data-stu-id="17149-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="17149-167">Ve výchozím nastavení služba webové správy naslouchá na portu TCP 8172.</span><span class="sxs-lookup"><span data-stu-id="17149-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="17149-168">V bráně Windows Firewall vytvořte nové příchozí pravidlo povolující přenosy TCP na portu 8172.</span><span class="sxs-lookup"><span data-stu-id="17149-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="17149-169">Další informace najdete v tématu [Konfigurace pravidel brány firewall](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="17149-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="17149-170">(Pokud virtuální počítače hostují v Azure, můžete to provést přímo v Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="17149-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="17149-171">Přečtěte si téma [nastavení koncových bodů na virtuální počítač](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="17149-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="17149-172">Nyní jste připraveni nasadit projekt sady Visual Studio z vývojového počítače na server.</span><span class="sxs-lookup"><span data-stu-id="17149-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="17149-173">V Průzkumník řešení klikněte pravým tlačítkem na řešení a pak klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="17149-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="17149-174">Podrobnější dokumentaci k nasazení webu najdete v tématu [Mapa obsahu nasazení webu pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="17149-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="17149-175">Pokud nasadíte aplikaci na dva servery, můžete každou instanci otevřít v samostatném okně prohlížeče a podívat se, že každý z nich obdrží zprávy signálu.</span><span class="sxs-lookup"><span data-stu-id="17149-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="17149-176">(Samozřejmě v produkčním prostředí budou dva servery za nástroj pro vyrovnávání zatížení.)</span><span class="sxs-lookup"><span data-stu-id="17149-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="17149-177">Pokud jste zajímá zprávy, které se odesílají do Redis, můžete použít klienta **Redis-CLI** , který se instaluje s Redis.</span><span class="sxs-lookup"><span data-stu-id="17149-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
