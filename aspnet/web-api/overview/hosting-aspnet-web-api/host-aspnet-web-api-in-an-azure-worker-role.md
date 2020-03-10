---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Hostování ASP.NET webového rozhraní API 2 v roli pracovního procesu Azure – ASP.NET 4. x
author: MikeWasson
description: 'Kurz: hostování webového rozhraní API ASP.NET v roli pracovního procesu Azure pomocí OWIN k samoobslužnému hostování rozhraní Web API Framework.'
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556628"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="b4c57-103">Hostování ASP.NET webového rozhraní API 2 v roli pracovního procesu Azure</span><span class="sxs-lookup"><span data-stu-id="b4c57-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="b4c57-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b4c57-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b4c57-105">V tomto kurzu se dozvíte, jak hostovat webové rozhraní API ASP.NET v roli pracovního procesu Azure pomocí OWIN k samoobslužnému hostování rozhraní Web API.</span><span class="sxs-lookup"><span data-stu-id="b4c57-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="b4c57-106">[Open Web Interface for .NET](http://owin.org/) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="b4c57-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="b4c57-107">OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS – například v rámci role pracovního procesu Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c57-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="b4c57-108">V tomto kurzu použijete balíček Microsoft. Owin. Host. HttpListener, který poskytuje server HTTP, který se používá k samoobslužnému hostování aplikací OWIN.</span><span class="sxs-lookup"><span data-stu-id="b4c57-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b4c57-109">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="b4c57-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="b4c57-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b4c57-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="b4c57-111">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="b4c57-111">Web API 2</span></span>
> - [<span data-ttu-id="b4c57-112">Sada Azure SDK pro .NET 2,3</span><span class="sxs-lookup"><span data-stu-id="b4c57-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="b4c57-113">Vytvoření projektu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b4c57-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="b4c57-114">Spusťte aplikaci Visual Studio s oprávněními správce.</span><span class="sxs-lookup"><span data-stu-id="b4c57-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="b4c57-115">K místnímu ladění aplikace pomocí emulátoru služby COMPUTE Azure jsou nutná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="b4c57-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="b4c57-116">V nabídce **soubor** klikněte na příkaz **Nový**a potom na **projekt**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="b4c57-117">Z **nainstalovaných šablon**v části C#vizuál klikněte na **Cloud** a pak klikněte na **cloudová služba Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="b4c57-118">Pojmenujte projekt "soubor azureapp" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="b4c57-119">V dialogovém okně **Nová cloudová služba Microsoft Azure** poklikejte na **role pracovního procesu**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="b4c57-120">Ponechte výchozí název ("WorkerRole1").</span><span class="sxs-lookup"><span data-stu-id="b4c57-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="b4c57-121">Tento krok přidá do řešení pracovní roli.</span><span class="sxs-lookup"><span data-stu-id="b4c57-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="b4c57-122">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="b4c57-123">Vytvořené řešení sady Visual Studio obsahuje dva projekty:</span><span class="sxs-lookup"><span data-stu-id="b4c57-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="b4c57-124">&quot;soubor azureapp&quot; definuje role a konfiguraci pro aplikaci Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c57-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="b4c57-125">&quot;WorkerRole1&quot; obsahuje kód role pracovního procesu.</span><span class="sxs-lookup"><span data-stu-id="b4c57-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="b4c57-126">Obecně platí, že aplikace Azure může obsahovat více rolí, i když tento kurz používá jedinou roli.</span><span class="sxs-lookup"><span data-stu-id="b4c57-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="b4c57-127">Přidat webové rozhraní API a balíčky OWIN</span><span class="sxs-lookup"><span data-stu-id="b4c57-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="b4c57-128">V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="b4c57-129">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="b4c57-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="b4c57-130">Přidat koncový bod HTTP</span><span class="sxs-lookup"><span data-stu-id="b4c57-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="b4c57-131">V Průzkumník řešení rozbalte projekt soubor azureapp.</span><span class="sxs-lookup"><span data-stu-id="b4c57-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="b4c57-132">Rozbalte uzel role, klikněte pravým tlačítkem na WorkerRole1 a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="b4c57-133">Klikněte na **koncové body**a pak klikněte na **přidat koncový bod**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="b4c57-134">V rozevíracím seznamu **protokol** vyberte http.</span><span class="sxs-lookup"><span data-stu-id="b4c57-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="b4c57-135">Do **veřejného portu** a **privátního portu**zadejte 80.</span><span class="sxs-lookup"><span data-stu-id="b4c57-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="b4c57-136">Tato čísla portů se mohou lišit.</span><span class="sxs-lookup"><span data-stu-id="b4c57-136">These port numbers can be different.</span></span> <span data-ttu-id="b4c57-137">Veřejný port je používán klienty při odesílání žádosti do role.</span><span class="sxs-lookup"><span data-stu-id="b4c57-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="b4c57-138">Konfigurace webového rozhraní API pro samoobslužné hostování</span><span class="sxs-lookup"><span data-stu-id="b4c57-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="b4c57-139">V Průzkumník řešení klikněte pravým tlačítkem na projekt WorkerRole1 a výběrem **přidat** / **třídu** přidejte novou třídu.</span><span class="sxs-lookup"><span data-stu-id="b4c57-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="b4c57-140">Pojmenujte `Startup`třídy.</span><span class="sxs-lookup"><span data-stu-id="b4c57-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="b4c57-141">Celý často používaný kód nahraďte tímto souborem:</span><span class="sxs-lookup"><span data-stu-id="b4c57-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="b4c57-142">Přidat kontroler webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="b4c57-142">Add a Web API Controller</span></span>

<span data-ttu-id="b4c57-143">Dále přidejte třídu kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="b4c57-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="b4c57-144">Klikněte pravým tlačítkem na projekt WorkerRole1 a vyberte **přidat** / **třídy**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="b4c57-145">Pojmenujte třídu TestController.</span><span class="sxs-lookup"><span data-stu-id="b4c57-145">Name the class TestController.</span></span> <span data-ttu-id="b4c57-146">Celý často používaný kód nahraďte tímto souborem:</span><span class="sxs-lookup"><span data-stu-id="b4c57-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="b4c57-147">Pro zjednodušení tento kontroler jenom definuje dvě metody GET, které vracejí prostý text.</span><span class="sxs-lookup"><span data-stu-id="b4c57-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="b4c57-148">Spustit hostitele OWIN</span><span class="sxs-lookup"><span data-stu-id="b4c57-148">Start the OWIN Host</span></span>

<span data-ttu-id="b4c57-149">Otevřete soubor WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="b4c57-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="b4c57-150">Tato třída definuje kód, který se spustí při spuštění a zastavení role pracovního procesu.</span><span class="sxs-lookup"><span data-stu-id="b4c57-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="b4c57-151">Přidejte následující příkaz using:</span><span class="sxs-lookup"><span data-stu-id="b4c57-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="b4c57-152">Přidejte člena **IDisposable** do třídy `WorkerRole`:</span><span class="sxs-lookup"><span data-stu-id="b4c57-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="b4c57-153">Do `OnStart` metody přidejte následující kód pro spuštění hostitele:</span><span class="sxs-lookup"><span data-stu-id="b4c57-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="b4c57-154">Metoda **WebApp. Start** SPUSTÍ hostitele Owin.</span><span class="sxs-lookup"><span data-stu-id="b4c57-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="b4c57-155">Název třídy `Startup` je parametr typu metody.</span><span class="sxs-lookup"><span data-stu-id="b4c57-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="b4c57-156">Podle konvence hostitel zavolá metodu `Configure` této třídy.</span><span class="sxs-lookup"><span data-stu-id="b4c57-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="b4c57-157">Přepište `OnStop` k Dispose instance *\_aplikace* :</span><span class="sxs-lookup"><span data-stu-id="b4c57-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="b4c57-158">Zde je kompletní kód pro WorkerRole.cs:</span><span class="sxs-lookup"><span data-stu-id="b4c57-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="b4c57-159">Sestavte řešení a stisknutím klávesy F5 spusťte aplikaci místně v emulátoru služby COMPUTE Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c57-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="b4c57-160">V závislosti na nastavení brány firewall možná budete muset emulátor zapnout přes bránu firewall.</span><span class="sxs-lookup"><span data-stu-id="b4c57-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="b4c57-161">Pokud získáte výjimku, jak je vidět níže, přečtěte si [Tento Blogový příspěvek](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) , kde najdete alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="b4c57-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="b4c57-162">Nepovedlo se načíst soubor nebo sestavení Microsoft. Owin, Version = 2.0.2.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 nebo jedna z jejích závislostí.</span><span class="sxs-lookup"><span data-stu-id="b4c57-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="b4c57-163">Nalezená definice manifestu sestavení neodpovídá odkazu na sestavení.</span><span class="sxs-lookup"><span data-stu-id="b4c57-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="b4c57-164">(Výjimka z HRESULT: 0x80131040)</span><span class="sxs-lookup"><span data-stu-id="b4c57-164">(Exception from HRESULT: 0x80131040)"</span></span>

<span data-ttu-id="b4c57-165">Emulátor služby COMPUTE přiřadí koncovému bodu místní IP adresu.</span><span class="sxs-lookup"><span data-stu-id="b4c57-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="b4c57-166">IP adresu najdete v uživatelském rozhraní emulátoru Compute.</span><span class="sxs-lookup"><span data-stu-id="b4c57-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="b4c57-167">Klikněte pravým tlačítkem myši na ikonu emulátoru v oznamovací oblasti na hlavním panelu a vyberte **Zobrazit uživatelské rozhraní emulátoru COMPUTE**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="b4c57-168">Vyhledejte IP adresu v části nasazení služeb, nasazení [ID], Podrobnosti služby.</span><span class="sxs-lookup"><span data-stu-id="b4c57-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="b4c57-169">Otevřete webový prohlížeč a přejděte na<em>adresu http:///Test/1</em>, kde <em>adresa</em> je IP adresa přiřazená emulátorem COMPUTE; například `http://127.0.0.1:80/test/1`.</span><span class="sxs-lookup"><span data-stu-id="b4c57-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="b4c57-170">Měla by se zobrazit odpověď z kontroleru webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="b4c57-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="b4c57-171">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="b4c57-171">Deploy to Azure</span></span>

<span data-ttu-id="b4c57-172">Pro tento krok musíte mít účet Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c57-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="b4c57-173">Pokud ho ještě nemáte, můžete si během několika minut vytvořit bezplatný zkušební účet.</span><span class="sxs-lookup"><span data-stu-id="b4c57-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b4c57-174">Podrobnosti najdete v tématu [Microsoft Azure bezplatné zkušební verze](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b4c57-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="b4c57-175">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt soubor azureapp.</span><span class="sxs-lookup"><span data-stu-id="b4c57-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="b4c57-176">Vyberte **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="b4c57-177">Pokud nejste přihlášení ke svému účtu Azure, klikněte na **Přihlásit**se.</span><span class="sxs-lookup"><span data-stu-id="b4c57-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="b4c57-178">Po přihlášení vyberte předplatné a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="b4c57-179">Zadejte název cloudové služby a vyberte oblast.</span><span class="sxs-lookup"><span data-stu-id="b4c57-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="b4c57-180">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="b4c57-181">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="b4c57-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="b4c57-182">V okně Protokol aktivit Azure se zobrazuje průběh nasazení.</span><span class="sxs-lookup"><span data-stu-id="b4c57-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="b4c57-183">Po nasazení aplikace přejděte na http://appname.cloudapp.net/test/1.</span><span class="sxs-lookup"><span data-stu-id="b4c57-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="b4c57-184">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="b4c57-184">Additional Resources</span></span>

- [<span data-ttu-id="b4c57-185">Přehled projektu Katana</span><span class="sxs-lookup"><span data-stu-id="b4c57-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="b4c57-186">Projekt Katana na GitHubu</span><span class="sxs-lookup"><span data-stu-id="b4c57-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
