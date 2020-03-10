---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Škálování signálu pomocí Azure Service Bus | Microsoft Docs
author: bradygaster
description: Verze softwaru používané v tomto tématu Visual Studio 2013 v předchozích verzích tohoto tématu v části Signaler 4,5 verze 2 tohoto tématu, pro verzi Signaler 1. x tohoto tématu,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579175"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="74c0b-103">Škálování aplikace SignalR službou Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="74c0b-103">SignalR Scaleout with Azure Service Bus</span></span>

<span data-ttu-id="74c0b-104">[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="74c0b-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="74c0b-105">V tomto kurzu nasadíte aplikaci signalizace do webové role Windows Azure pomocí Service Busho opětovného plánování pro distribuci zpráv do každé instance role.</span><span class="sxs-lookup"><span data-stu-id="74c0b-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="74c0b-106">(Můžete také použít Service Bus pro naplánování pomocí [Web Apps v Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span><span class="sxs-lookup"><span data-stu-id="74c0b-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="74c0b-107">Požadavky:</span><span class="sxs-lookup"><span data-stu-id="74c0b-107">Prerequisites:</span></span>

- <span data-ttu-id="74c0b-108">Účet služby Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="74c0b-108">A Windows Azure account.</span></span>
- <span data-ttu-id="74c0b-109">[Sada Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="74c0b-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="74c0b-110">Visual Studio 2012 nebo 2013.</span><span class="sxs-lookup"><span data-stu-id="74c0b-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="74c0b-111">[Pro Service Bus systému Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)verze 1,1 je služba replánování Service Bus taky kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="74c0b-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="74c0b-112">Není ale kompatibilní s verzí 1,0 Service Bus pro Windows Server.</span><span class="sxs-lookup"><span data-stu-id="74c0b-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="74c0b-113">Ceny</span><span class="sxs-lookup"><span data-stu-id="74c0b-113">Pricing</span></span>

<span data-ttu-id="74c0b-114">Service Bus pro nové plánování používá témata k posílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="74c0b-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="74c0b-115">Nejnovější informace o cenách najdete v tématu [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="74c0b-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="74c0b-116">V době psaní tohoto textu můžete odesílat 1 000 000 zpráv za měsíc za méně než $1.</span><span class="sxs-lookup"><span data-stu-id="74c0b-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="74c0b-117">Metoda replánování pošle zprávu služby Service Bus pro každé vyvolání metody centra signalizace.</span><span class="sxs-lookup"><span data-stu-id="74c0b-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="74c0b-118">K dispozici jsou také některé řídicí zprávy pro připojení, odpojení, spojování nebo opouštíní skupin a tak dále.</span><span class="sxs-lookup"><span data-stu-id="74c0b-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="74c0b-119">Ve většině aplikací se většina přenosů zpráv bude vyvoláním metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="74c0b-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="74c0b-120">Přehled</span><span class="sxs-lookup"><span data-stu-id="74c0b-120">Overview</span></span>

<span data-ttu-id="74c0b-121">Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="74c0b-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="74c0b-122">K vytvoření nového oboru názvů Service Bus použijte Azure Portal Windows.</span><span class="sxs-lookup"><span data-stu-id="74c0b-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="74c0b-123">Přidejte tyto balíčky NuGet do vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="74c0b-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="74c0b-124">Microsoft. AspNet. Signaler</span><span class="sxs-lookup"><span data-stu-id="74c0b-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="74c0b-125">[Microsoft. ASPNET. Signal. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) nebo [Microsoft. ASPNET. Signal. ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="74c0b-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="74c0b-126">Vytvořte aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="74c0b-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="74c0b-127">Přidáním následujícího kódu do Startup.cs nakonfigurujte schéma pro replánování:</span><span class="sxs-lookup"><span data-stu-id="74c0b-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="74c0b-128">Tento kód nakonfiguruje pro replánování výchozí hodnoty pro [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) a [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span><span class="sxs-lookup"><span data-stu-id="74c0b-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="74c0b-129">Informace o změně těchto hodnot najdete v tématu [výkon signalizace: metriky škálování](signalr-performance.md#scaleout_metrics).</span><span class="sxs-lookup"><span data-stu-id="74c0b-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="74c0b-130">Pro každou aplikaci vyberte jinou hodnotu "soubor YourAppName".</span><span class="sxs-lookup"><span data-stu-id="74c0b-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="74c0b-131">Nepoužívejte stejnou hodnotu napříč více aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="74c0b-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="74c0b-132">Vytvoření služeb Azure</span><span class="sxs-lookup"><span data-stu-id="74c0b-132">Create the Azure Services</span></span>

<span data-ttu-id="74c0b-133">Vytvořte cloudovou službu, jak je popsáno v tématu [jak vytvořit a nasadit cloudovou službu](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="74c0b-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="74c0b-134">Postupujte podle kroků v části Postup: vytvoření cloudové služby pomocí příkazu rychle vytvořit.</span><span class="sxs-lookup"><span data-stu-id="74c0b-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="74c0b-135">Pro tento kurz nemusíte nahrávat certifikát.</span><span class="sxs-lookup"><span data-stu-id="74c0b-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="74c0b-136">Vytvořte nový obor názvů Service Bus, jak je popsáno v [tématu Jak používat Service Bus témata/předplatná](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="74c0b-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="74c0b-137">Postupujte podle kroků v části "Vytvoření oboru názvů služby".</span><span class="sxs-lookup"><span data-stu-id="74c0b-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="74c0b-138">Ujistěte se, že jste vybrali stejnou oblast pro cloudovou službu a obor názvů Service Bus.</span><span class="sxs-lookup"><span data-stu-id="74c0b-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="74c0b-139">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74c0b-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="74c0b-140">Spusťte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74c0b-140">Start Visual Studio.</span></span> <span data-ttu-id="74c0b-141">V nabídce **Soubor** klikněte na **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="74c0b-142">V dialogovém okně **Nový projekt** rozbalte položku **vizuál C#** .</span><span class="sxs-lookup"><span data-stu-id="74c0b-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="74c0b-143">V části **Nainstalované šablony**vyberte **Cloud** a potom vyberte **cloudová služba Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="74c0b-144">Ponechte výchozí .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="74c0b-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="74c0b-145">Pojmenujte aplikaci ChatService a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="74c0b-146">V dialogovém okně **Nová cloudová služba Microsoft Azure** vyberte ASP.NET webová role.</span><span class="sxs-lookup"><span data-stu-id="74c0b-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="74c0b-147">Kliknutím na tlačítko se šipkou doprava ( **&gt;** ) přidáte roli do svého řešení.</span><span class="sxs-lookup"><span data-stu-id="74c0b-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="74c0b-148">Najeďte myší na novou roli, aby se ikona tužky zobrazila.</span><span class="sxs-lookup"><span data-stu-id="74c0b-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="74c0b-149">Kliknutím na tuto ikonu přejmenujete roli.</span><span class="sxs-lookup"><span data-stu-id="74c0b-149">Click this icon to rename the role.</span></span> <span data-ttu-id="74c0b-150">Pojmenujte roli "SignalRChat" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="74c0b-151">V dialogovém okně **Nový projekt ASP.NET** vyberte **MVC**a klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="74c0b-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="74c0b-152">Průvodce projektem vytvoří dva projekty:</span><span class="sxs-lookup"><span data-stu-id="74c0b-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="74c0b-153">ChatService: Tento projekt je aplikace systému Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="74c0b-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="74c0b-154">Definuje role Azure a další možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="74c0b-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="74c0b-155">SignalRChat: Tento projekt je váš projekt ASP.NET MVC 5.</span><span class="sxs-lookup"><span data-stu-id="74c0b-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="74c0b-156">Vytvoření aplikace pro chat signálu</span><span class="sxs-lookup"><span data-stu-id="74c0b-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="74c0b-157">Chcete-li vytvořit aplikaci Chat, postupujte podle kroků v kurzu [Začínáme s nástrojem signaler a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="74c0b-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="74c0b-158">K instalaci požadovaných knihoven použijte NuGet.</span><span class="sxs-lookup"><span data-stu-id="74c0b-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="74c0b-159">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-159">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="74c0b-160">V okně **konzoly Správce balíčků** zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="74c0b-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="74c0b-161">Použijte možnost `-ProjectName` k instalaci balíčků do projektu ASP.NET MVC místo do projektu Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="74c0b-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="74c0b-162">Konfigurovat plán</span><span class="sxs-lookup"><span data-stu-id="74c0b-162">Configure the Backplane</span></span>

<span data-ttu-id="74c0b-163">Do souboru Startup.cs vaší aplikace přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="74c0b-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="74c0b-164">Nyní potřebujete získat připojovací řetězec služby Service Bus.</span><span class="sxs-lookup"><span data-stu-id="74c0b-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="74c0b-165">V Azure Portal vyberte obor názvů služby Service Bus, který jste vytvořili, a klikněte na ikonu přístupového klíče.</span><span class="sxs-lookup"><span data-stu-id="74c0b-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="74c0b-166">Zkopírujte připojovací řetězec do schránky a vložte ho do proměnné *ConnectionString* .</span><span class="sxs-lookup"><span data-stu-id="74c0b-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="74c0b-167">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="74c0b-167">Deploy to Azure</span></span>

<span data-ttu-id="74c0b-168">V Průzkumník řešení rozbalte složku **role** v projektu ChatService.</span><span class="sxs-lookup"><span data-stu-id="74c0b-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="74c0b-169">Klikněte pravým tlačítkem na roli SignalRChat a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="74c0b-170">Vyberte kartu **Konfigurace** . V části **instance** vyberte 2.</span><span class="sxs-lookup"><span data-stu-id="74c0b-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="74c0b-171">Velikost virtuálního počítače taky můžete nastavit na **velmi malou**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="74c0b-172">Uložte změny.</span><span class="sxs-lookup"><span data-stu-id="74c0b-172">Save the changes.</span></span>

<span data-ttu-id="74c0b-173">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt ChatService.</span><span class="sxs-lookup"><span data-stu-id="74c0b-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="74c0b-174">Vyberte **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="74c0b-175">Pokud publikujete do Windows Azure poprvé, musíte si stáhnout svoje přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="74c0b-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="74c0b-176">V průvodci **publikování** klikněte na Přihlásit se a stáhněte přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="74c0b-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="74c0b-177">Zobrazí se výzva, abyste se přihlásili k Windows Azure Portal a stáhli soubor nastavení publikování.</span><span class="sxs-lookup"><span data-stu-id="74c0b-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="74c0b-178">Klikněte na **importovat** a vyberte soubor nastavení publikování, který jste stáhli.</span><span class="sxs-lookup"><span data-stu-id="74c0b-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="74c0b-179">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-179">Click **Next**.</span></span> <span data-ttu-id="74c0b-180">V dialogovém okně **publikovat nastavení** v části **cloudová služba**Vyberte cloudovou službu, kterou jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="74c0b-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="74c0b-181">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="74c0b-181">Click **Publish**.</span></span> <span data-ttu-id="74c0b-182">Nasazení aplikace a spuštění virtuálních počítačů může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="74c0b-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="74c0b-183">Nyní když spouštíte aplikaci Chat, instance rolí komunikují prostřednictvím Azure Service Bus pomocí Service Busho tématu.</span><span class="sxs-lookup"><span data-stu-id="74c0b-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="74c0b-184">Téma je fronta zpráv, která umožňuje více odběratelů.</span><span class="sxs-lookup"><span data-stu-id="74c0b-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="74c0b-185">Znovu naplánování automaticky vytvoří téma a odběry.</span><span class="sxs-lookup"><span data-stu-id="74c0b-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="74c0b-186">Chcete-li zobrazit odběry a aktivity zprávy, otevřete Azure Portal, vyberte obor názvů Service Bus a klikněte na tlačítko "témata".</span><span class="sxs-lookup"><span data-stu-id="74c0b-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="74c0b-187">Zobrazení aktivity zprávy na řídicím panelu může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="74c0b-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="74c0b-188">Návěstí řídí dobu života tématu.</span><span class="sxs-lookup"><span data-stu-id="74c0b-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="74c0b-189">Pokud je vaše aplikace nasazena, nepokoušejte se ručně odstranit témata nebo změnit nastavení v tématu.</span><span class="sxs-lookup"><span data-stu-id="74c0b-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="74c0b-190">Řešení potíží</span><span class="sxs-lookup"><span data-stu-id="74c0b-190">Troubleshooting</span></span>

<span data-ttu-id="74c0b-191">**System. InvalidOperationException "jedinou podporovanou IsolationLevel je" IsolationLevel. serializovatelný ".**</span><span class="sxs-lookup"><span data-stu-id="74c0b-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="74c0b-192">K této chybě může dojít, pokud je úroveň transakce pro operaci nastavena na jinou hodnotu než `Serializable`.</span><span class="sxs-lookup"><span data-stu-id="74c0b-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="74c0b-193">Ověřte, že se neprovádí žádné operace s jinými úrovněmi transakce.</span><span class="sxs-lookup"><span data-stu-id="74c0b-193">Verify that no operations are being performed with other transaction levels.</span></span>
