---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: Horizontální navýšení signálu pomocí Azure Service Bus (Signal 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558413"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="ceccc-102">Škálování aplikace SignalR službou Azure Service Bus (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="ceccc-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="ceccc-103">[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ceccc-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="ceccc-104">V tomto kurzu nasadíte aplikaci signalizace do webové role Windows Azure pomocí Service Busho opětovného plánování pro distribuci zpráv do každé instance role.</span><span class="sxs-lookup"><span data-stu-id="ceccc-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="ceccc-105">Požadavky:</span><span class="sxs-lookup"><span data-stu-id="ceccc-105">Prerequisites:</span></span>

- <span data-ttu-id="ceccc-106">Účet služby Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="ceccc-106">A Windows Azure account.</span></span>
- <span data-ttu-id="ceccc-107">[Sada Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ceccc-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="ceccc-108">Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="ceccc-108">Visual Studio 2012.</span></span>

<span data-ttu-id="ceccc-109">[Pro Service Bus systému Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)verze 1,1 je služba replánování Service Bus taky kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="ceccc-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="ceccc-110">Není ale kompatibilní s verzí 1,0 Service Bus pro Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ceccc-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="ceccc-111">Ceny</span><span class="sxs-lookup"><span data-stu-id="ceccc-111">Pricing</span></span>

<span data-ttu-id="ceccc-112">Service Bus pro nové plánování používá témata k posílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="ceccc-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="ceccc-113">Nejnovější informace o cenách najdete v tématu [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="ceccc-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="ceccc-114">V době psaní tohoto textu můžete odesílat 1 000 000 zpráv za měsíc za méně než $1.</span><span class="sxs-lookup"><span data-stu-id="ceccc-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="ceccc-115">Metoda replánování pošle zprávu služby Service Bus pro každé vyvolání metody centra signalizace.</span><span class="sxs-lookup"><span data-stu-id="ceccc-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="ceccc-116">K dispozici jsou také některé řídicí zprávy pro připojení, odpojení, spojování nebo opouštíní skupin a tak dále.</span><span class="sxs-lookup"><span data-stu-id="ceccc-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="ceccc-117">Ve většině aplikací se většina přenosů zpráv bude vyvoláním metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="ceccc-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="ceccc-118">Přehled</span><span class="sxs-lookup"><span data-stu-id="ceccc-118">Overview</span></span>

<span data-ttu-id="ceccc-119">Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.</span><span class="sxs-lookup"><span data-stu-id="ceccc-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="ceccc-120">K vytvoření nového oboru názvů Service Bus použijte Azure Portal Windows.</span><span class="sxs-lookup"><span data-stu-id="ceccc-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="ceccc-121">Přidejte tyto balíčky NuGet do vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="ceccc-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="ceccc-122">Microsoft. AspNet. Signaler</span><span class="sxs-lookup"><span data-stu-id="ceccc-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="ceccc-123">Microsoft. AspNet. Signaler. ServiceBus</span><span class="sxs-lookup"><span data-stu-id="ceccc-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="ceccc-124">Vytvořte aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="ceccc-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="ceccc-125">Přidejte následující kód do Global. asax ke konfiguraci rozhraní pro naplánování:</span><span class="sxs-lookup"><span data-stu-id="ceccc-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="ceccc-126">Pro každou aplikaci vyberte jinou hodnotu "soubor YourAppName".</span><span class="sxs-lookup"><span data-stu-id="ceccc-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="ceccc-127">Nepoužívejte stejnou hodnotu napříč více aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="ceccc-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="ceccc-128">Vytvoření služeb Azure</span><span class="sxs-lookup"><span data-stu-id="ceccc-128">Create the Azure Services</span></span>

<span data-ttu-id="ceccc-129">Vytvořte cloudovou službu, jak je popsáno v tématu [jak vytvořit a nasadit cloudovou službu](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="ceccc-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="ceccc-130">Postupujte podle kroků v části Postup: vytvoření cloudové služby pomocí příkazu rychle vytvořit.</span><span class="sxs-lookup"><span data-stu-id="ceccc-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="ceccc-131">Pro tento kurz nemusíte nahrávat certifikát.</span><span class="sxs-lookup"><span data-stu-id="ceccc-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="ceccc-132">Vytvořte nový obor názvů Service Bus, jak je popsáno v [tématu Jak používat Service Bus témata/předplatná](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="ceccc-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="ceccc-133">Postupujte podle kroků v části "Vytvoření oboru názvů služby".</span><span class="sxs-lookup"><span data-stu-id="ceccc-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="ceccc-134">Ujistěte se, že jste vybrali stejnou oblast pro cloudovou službu a obor názvů Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ceccc-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="ceccc-135">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ceccc-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="ceccc-136">Spusťte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ceccc-136">Start Visual Studio.</span></span> <span data-ttu-id="ceccc-137">V nabídce **Soubor** klikněte na **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="ceccc-138">V dialogovém okně **Nový projekt** rozbalte položku **vizuál C#** .</span><span class="sxs-lookup"><span data-stu-id="ceccc-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="ceccc-139">V části **Nainstalované šablony**vyberte **Cloud** a potom vyberte **cloudová služba Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="ceccc-140">Ponechte výchozí .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="ceccc-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="ceccc-141">Pojmenujte aplikaci ChatService a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="ceccc-142">V dialogovém okně **Nová cloudová služba Microsoft Azure** vyberte webová role ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="ceccc-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="ceccc-143">Kliknutím na tlačítko se šipkou doprava ( **&gt;** ) přidáte roli do svého řešení.</span><span class="sxs-lookup"><span data-stu-id="ceccc-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="ceccc-144">Najeďte myší na novou roli, aby se ikona tužky zobrazila.</span><span class="sxs-lookup"><span data-stu-id="ceccc-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="ceccc-145">Kliknutím na tuto ikonu přejmenujete roli.</span><span class="sxs-lookup"><span data-stu-id="ceccc-145">Click this icon to rename the role.</span></span> <span data-ttu-id="ceccc-146">Pojmenujte roli "SignalRChat" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="ceccc-147">V průvodci **vytvořením nového projektu ASP.NET MVC 4** vyberte **internetovou aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="ceccc-148">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-148">Click **OK**.</span></span> <span data-ttu-id="ceccc-149">Průvodce projektem vytvoří dva projekty:</span><span class="sxs-lookup"><span data-stu-id="ceccc-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="ceccc-150">ChatService: Tento projekt je aplikace systému Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="ceccc-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="ceccc-151">Definuje role Azure a další možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ceccc-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="ceccc-152">SignalRChat: Tento projekt je váš projekt ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="ceccc-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="ceccc-153">Vytvoření aplikace pro chat signálu</span><span class="sxs-lookup"><span data-stu-id="ceccc-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="ceccc-154">Chcete-li vytvořit aplikaci Chat, postupujte podle kroků v kurzu [Začínáme s nástrojem Signal and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="ceccc-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="ceccc-155">K instalaci požadovaných knihoven použijte NuGet.</span><span class="sxs-lookup"><span data-stu-id="ceccc-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="ceccc-156">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ceccc-157">V okně **konzoly Správce balíčků** zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="ceccc-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="ceccc-158">Použijte možnost `-ProjectName` k instalaci balíčků do projektu ASP.NET MVC místo do projektu Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="ceccc-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="ceccc-159">Konfigurovat plán</span><span class="sxs-lookup"><span data-stu-id="ceccc-159">Configure the Backplane</span></span>

<span data-ttu-id="ceccc-160">Do souboru Global. asax vaší aplikace přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="ceccc-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="ceccc-161">Nyní potřebujete získat připojovací řetězec služby Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ceccc-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="ceccc-162">V Azure Portal vyberte obor názvů služby Service Bus, který jste vytvořili, a klikněte na ikonu přístupového klíče.</span><span class="sxs-lookup"><span data-stu-id="ceccc-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="ceccc-163">Zkopírujte připojovací řetězec do schránky a vložte ho do proměnné *ConnectionString* .</span><span class="sxs-lookup"><span data-stu-id="ceccc-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="ceccc-164">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="ceccc-164">Deploy to Azure</span></span>

<span data-ttu-id="ceccc-165">V Průzkumník řešení rozbalte složku **role** v projektu ChatService.</span><span class="sxs-lookup"><span data-stu-id="ceccc-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="ceccc-166">Klikněte pravým tlačítkem na roli SignalRChat a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="ceccc-167">Vyberte kartu **Konfigurace** . V části **instance** vyberte 2.</span><span class="sxs-lookup"><span data-stu-id="ceccc-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="ceccc-168">Velikost virtuálního počítače taky můžete nastavit na **velmi malou**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="ceccc-169">Uložte změny.</span><span class="sxs-lookup"><span data-stu-id="ceccc-169">Save the changes.</span></span>

<span data-ttu-id="ceccc-170">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt ChatService.</span><span class="sxs-lookup"><span data-stu-id="ceccc-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="ceccc-171">Vyberte **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="ceccc-172">Pokud publikujete do Windows Azure poprvé, musíte si stáhnout svoje přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="ceccc-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="ceccc-173">V průvodci **publikování** klikněte na Přihlásit se a stáhněte přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="ceccc-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="ceccc-174">Zobrazí se výzva, abyste se přihlásili k Windows Azure Portal a stáhli soubor nastavení publikování.</span><span class="sxs-lookup"><span data-stu-id="ceccc-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="ceccc-175">Klikněte na **importovat** a vyberte soubor nastavení publikování, který jste stáhli.</span><span class="sxs-lookup"><span data-stu-id="ceccc-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="ceccc-176">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-176">Click **Next**.</span></span> <span data-ttu-id="ceccc-177">V dialogovém okně **publikovat nastavení** v části **cloudová služba**Vyberte cloudovou službu, kterou jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="ceccc-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="ceccc-178">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="ceccc-178">Click **Publish**.</span></span> <span data-ttu-id="ceccc-179">Nasazení aplikace a spuštění virtuálních počítačů může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="ceccc-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="ceccc-180">Nyní když spouštíte aplikaci Chat, instance rolí komunikují prostřednictvím Azure Service Bus pomocí Service Busho tématu.</span><span class="sxs-lookup"><span data-stu-id="ceccc-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="ceccc-181">Téma je fronta zpráv, která umožňuje více odběratelů.</span><span class="sxs-lookup"><span data-stu-id="ceccc-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="ceccc-182">Znovu naplánování automaticky vytvoří téma a odběry.</span><span class="sxs-lookup"><span data-stu-id="ceccc-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="ceccc-183">Chcete-li zobrazit odběry a aktivity zprávy, otevřete Azure Portal, vyberte obor názvů Service Bus a klikněte na tlačítko "témata".</span><span class="sxs-lookup"><span data-stu-id="ceccc-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="ceccc-184">Zobrazení aktivity zprávy na řídicím panelu může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="ceccc-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="ceccc-185">Návěstí řídí dobu života tématu.</span><span class="sxs-lookup"><span data-stu-id="ceccc-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="ceccc-186">Pokud je vaše aplikace nasazena, nepokoušejte se ručně odstranit témata nebo změnit nastavení v tématu.</span><span class="sxs-lookup"><span data-stu-id="ceccc-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
