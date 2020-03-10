---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Hostování OWIN v roli pracovního procesu Azure | Microsoft Docs
author: MikeWasson
description: V tomto kurzu se dozvíte, jak můžete OWIN sebe samostatně hostovat do role pracovního procesu Microsoft Azure. Open Web Interface for .NET (OWIN) definuje abstrakci mezi webovým serverem .NET...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584614"
---
# <a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="9e80f-104">Hostování specifikace OWIN v rolích pracovního procesu v Azure</span><span class="sxs-lookup"><span data-stu-id="9e80f-104">Host OWIN in an Azure Worker Role</span></span>

<span data-ttu-id="9e80f-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9e80f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="9e80f-106">V tomto kurzu se dozvíte, jak můžete OWIN sebe samostatně hostovat do role pracovního procesu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9e80f-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
>
> <span data-ttu-id="9e80f-107">[Open Web Interface for .NET](http://owin.org/) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="9e80f-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="9e80f-108">OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS – například v rámci role pracovního procesu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e80f-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="9e80f-109">V tomto kurzu se naučíte, jak sami hostovat aplikace OWIN v rámci role pracovního procesu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9e80f-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="9e80f-110">Další informace o rolích pracovního procesu najdete v tématu [modely spouštění Azure](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span><span class="sxs-lookup"><span data-stu-id="9e80f-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9e80f-111">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="9e80f-111">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="9e80f-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9e80f-112">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [<span data-ttu-id="9e80f-113">Sada Azure SDK pro .NET 2,3</span><span class="sxs-lookup"><span data-stu-id="9e80f-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="9e80f-114">Microsoft. Owin. SelfHost 2.1.0</span><span class="sxs-lookup"><span data-stu-id="9e80f-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="9e80f-115">Vytvoření projektu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9e80f-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="9e80f-116">Spusťte aplikaci Visual Studio s oprávněními správce.</span><span class="sxs-lookup"><span data-stu-id="9e80f-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="9e80f-117">K místnímu ladění aplikace pomocí emulátoru služby COMPUTE Azure jsou nutná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="9e80f-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="9e80f-118">V nabídce **soubor** klikněte na příkaz **Nový**a potom na **projekt**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="9e80f-119">Z **nainstalovaných šablon**v části C#vizuál klikněte na **Cloud** a pak klikněte na **cloudová služba Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="9e80f-120">Pojmenujte projekt "soubor azureapp" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="9e80f-121">V dialogovém okně **Nová cloudová služba Microsoft Azure** poklikejte na **role pracovního procesu**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="9e80f-122">Ponechte výchozí název ("WorkerRole1").</span><span class="sxs-lookup"><span data-stu-id="9e80f-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="9e80f-123">Tento krok přidá do řešení pracovní roli.</span><span class="sxs-lookup"><span data-stu-id="9e80f-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="9e80f-124">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="9e80f-125">Vytvořené řešení sady Visual Studio obsahuje dva projekty:</span><span class="sxs-lookup"><span data-stu-id="9e80f-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="9e80f-126">&quot;soubor azureapp&quot; definuje role a konfiguraci pro aplikaci Azure.</span><span class="sxs-lookup"><span data-stu-id="9e80f-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="9e80f-127">&quot;WorkerRole1&quot; obsahuje kód role pracovního procesu.</span><span class="sxs-lookup"><span data-stu-id="9e80f-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="9e80f-128">Obecně platí, že aplikace Azure může obsahovat více rolí, i když tento kurz používá jedinou roli.</span><span class="sxs-lookup"><span data-stu-id="9e80f-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="9e80f-129">Přidání balíčků pro samoobslužné hostování OWIN</span><span class="sxs-lookup"><span data-stu-id="9e80f-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="9e80f-130">V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-130">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="9e80f-131">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="9e80f-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="9e80f-132">Přidat koncový bod HTTP</span><span class="sxs-lookup"><span data-stu-id="9e80f-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="9e80f-133">V Průzkumník řešení rozbalte projekt soubor azureapp.</span><span class="sxs-lookup"><span data-stu-id="9e80f-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="9e80f-134">Rozbalte uzel role, klikněte pravým tlačítkem na WorkerRole1 a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="9e80f-135">Klikněte na **koncové body**a pak klikněte na **přidat koncový bod**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="9e80f-136">V rozevíracím seznamu **protokol** vyberte http.</span><span class="sxs-lookup"><span data-stu-id="9e80f-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="9e80f-137">Do **veřejného portu** a **privátního portu**zadejte 80.</span><span class="sxs-lookup"><span data-stu-id="9e80f-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="9e80f-138">Tato čísla portů se mohou lišit.</span><span class="sxs-lookup"><span data-stu-id="9e80f-138">These port numbers can be different.</span></span> <span data-ttu-id="9e80f-139">Veřejný port je používán klienty při odesílání žádosti do role.</span><span class="sxs-lookup"><span data-stu-id="9e80f-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="9e80f-140">Vytvoření třídy pro spuštění OWIN</span><span class="sxs-lookup"><span data-stu-id="9e80f-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="9e80f-141">V Průzkumník řešení klikněte pravým tlačítkem na projekt WorkerRole1 a výběrem **přidat** / **třídu** přidejte novou třídu.</span><span class="sxs-lookup"><span data-stu-id="9e80f-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="9e80f-142">Pojmenujte `Startup`třídy.</span><span class="sxs-lookup"><span data-stu-id="9e80f-142">Name the class `Startup`.</span></span>

<span data-ttu-id="9e80f-143">Celý často používaný kód nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="9e80f-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="9e80f-144">Metoda rozšíření `UseWelcomePage` přidá do aplikace jednoduchou stránku HTML, aby bylo možné ověřit, zda lokalita funguje.</span><span class="sxs-lookup"><span data-stu-id="9e80f-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="9e80f-145">Spustit hostitele OWIN</span><span class="sxs-lookup"><span data-stu-id="9e80f-145">Start the OWIN Host</span></span>

<span data-ttu-id="9e80f-146">Otevřete soubor WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="9e80f-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="9e80f-147">Tato třída definuje kód, který se spustí při spuštění a zastavení role pracovního procesu.</span><span class="sxs-lookup"><span data-stu-id="9e80f-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="9e80f-148">Přidejte následující příkaz using:</span><span class="sxs-lookup"><span data-stu-id="9e80f-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="9e80f-149">Přidejte člena **IDisposable** do třídy `WorkerRole`:</span><span class="sxs-lookup"><span data-stu-id="9e80f-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="9e80f-150">Do `OnStart` metody přidejte následující kód pro spuštění hostitele:</span><span class="sxs-lookup"><span data-stu-id="9e80f-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="9e80f-151">Metoda **WebApp. Start** SPUSTÍ hostitele Owin.</span><span class="sxs-lookup"><span data-stu-id="9e80f-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="9e80f-152">Název třídy `Startup` je parametr typu metody.</span><span class="sxs-lookup"><span data-stu-id="9e80f-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="9e80f-153">Podle konvence hostitel zavolá metodu `Configure` této třídy.</span><span class="sxs-lookup"><span data-stu-id="9e80f-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="9e80f-154">Přepište `OnStop` k Dispose instance *\_aplikace* :</span><span class="sxs-lookup"><span data-stu-id="9e80f-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="9e80f-155">Zde je kompletní kód pro WorkerRole.cs:</span><span class="sxs-lookup"><span data-stu-id="9e80f-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="9e80f-156">Sestavte řešení a stisknutím klávesy F5 spusťte aplikaci místně v emulátoru služby COMPUTE Azure.</span><span class="sxs-lookup"><span data-stu-id="9e80f-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="9e80f-157">V závislosti na nastavení brány firewall možná budete muset emulátor zapnout přes bránu firewall.</span><span class="sxs-lookup"><span data-stu-id="9e80f-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="9e80f-158">Emulátor služby COMPUTE přiřadí koncovému bodu místní IP adresu.</span><span class="sxs-lookup"><span data-stu-id="9e80f-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="9e80f-159">IP adresu najdete v uživatelském rozhraní emulátoru Compute.</span><span class="sxs-lookup"><span data-stu-id="9e80f-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="9e80f-160">Klikněte pravým tlačítkem myši na ikonu emulátoru v oznamovací oblasti na hlavním panelu a vyberte **Zobrazit uživatelské rozhraní emulátoru COMPUTE**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="9e80f-161">Vyhledejte IP adresu v části nasazení služeb, nasazení [ID], Podrobnosti služby.</span><span class="sxs-lookup"><span data-stu-id="9e80f-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="9e80f-162">Otevřete webový prohlížeč a přejděte na adresu http:\/\/*adresa*, kde *adresa* je IP adresa přiřazená emulátorem COMPUTE; například `http://127.0.0.1:80`.</span><span class="sxs-lookup"><span data-stu-id="9e80f-162">Open a web browser and navigate to http:\/\/*address*, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="9e80f-163">Měla by se zobrazit úvodní stránka OWIN:</span><span class="sxs-lookup"><span data-stu-id="9e80f-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="9e80f-164">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="9e80f-164">Deploy to Azure</span></span>

<span data-ttu-id="9e80f-165">Pro tento krok musíte mít účet Azure.</span><span class="sxs-lookup"><span data-stu-id="9e80f-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="9e80f-166">Pokud ho ještě nemáte, můžete si během několika minut vytvořit bezplatný zkušební účet.</span><span class="sxs-lookup"><span data-stu-id="9e80f-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9e80f-167">Podrobnosti najdete v tématu [Microsoft Azure bezplatné zkušební verze](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9e80f-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="9e80f-168">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt soubor azureapp.</span><span class="sxs-lookup"><span data-stu-id="9e80f-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="9e80f-169">Vyberte **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="9e80f-170">Pokud nejste přihlášení ke svému účtu Azure, klikněte na **Přihlásit**se.</span><span class="sxs-lookup"><span data-stu-id="9e80f-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="9e80f-171">Po přihlášení vyberte předplatné a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="9e80f-172">Zadejte název cloudové služby a vyberte oblast.</span><span class="sxs-lookup"><span data-stu-id="9e80f-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="9e80f-173">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="9e80f-174">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="9e80f-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="9e80f-175">V okně Protokol aktivit Azure se zobrazuje průběh nasazení.</span><span class="sxs-lookup"><span data-stu-id="9e80f-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="9e80f-176">Po nasazení aplikace přejděte na adresu `http://appname.cloudapp.net/`, kde *AppName* je název vaší cloudové služby.</span><span class="sxs-lookup"><span data-stu-id="9e80f-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e80f-177">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="9e80f-177">Additional Resources</span></span>

- [<span data-ttu-id="9e80f-178">Přehled projektu Katana</span><span class="sxs-lookup"><span data-stu-id="9e80f-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="9e80f-179">Projekt Katana na GitHubu</span><span class="sxs-lookup"><span data-stu-id="9e80f-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
