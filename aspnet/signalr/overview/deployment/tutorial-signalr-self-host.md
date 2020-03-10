---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 'Kurz: samoobslužný signál pro hostování | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se dozvíte, jak vytvořit server s nástrojem Signal-Host 2 a jak se k němu připojit pomocí JavaScriptového klienta. Verze softwaru používané v kurzu V...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558679"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="3e7be-104">Kurz: SignalR v místním prostředí</span><span class="sxs-lookup"><span data-stu-id="3e7be-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="3e7be-105">Po [Fletcheru](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="3e7be-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="3e7be-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="3e7be-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> <span data-ttu-id="3e7be-107">V tomto kurzu se dozvíte, jak vytvořit server s nástrojem Signal-Host 2 a jak se k němu připojit pomocí JavaScriptového klienta.</span><span class="sxs-lookup"><span data-stu-id="3e7be-107">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3e7be-108">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="3e7be-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="3e7be-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3e7be-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="3e7be-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3e7be-110">.NET 4.5</span></span>
> - <span data-ttu-id="3e7be-111">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="3e7be-111">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="3e7be-112">Pomocí sady Visual Studio 2012 s tímto kurzem</span><span class="sxs-lookup"><span data-stu-id="3e7be-112">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="3e7be-113">Chcete-li použít Visual Studio 2012 s tímto kurzem, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="3e7be-113">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="3e7be-114">Aktualizujte [Správce balíčků](http://docs.nuget.org/docs/start-here/installing-nuget) na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="3e7be-114">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="3e7be-115">Nainstalujte [instalační program webové platformy](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e7be-115">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="3e7be-116">V instalačním programu webové platformy vyhledejte a nainstalujte **ASP.NET and Web Tools 2013,1 pro Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-116">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="3e7be-117">Tím se nainstaluje šablony sady Visual Studio pro třídy signalizace, jako je například **centrum**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-117">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="3e7be-118">Některé šablony (například **Třída Owin Startup**) nebudou k dispozici. pro tyto soubory použijte místo toho soubor třídy.</span><span class="sxs-lookup"><span data-stu-id="3e7be-118">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="3e7be-119">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="3e7be-119">Questions and comments</span></span>
>
> <span data-ttu-id="3e7be-120">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="3e7be-120">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="3e7be-121">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="3e7be-121">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="3e7be-122">Přehled</span><span class="sxs-lookup"><span data-stu-id="3e7be-122">Overview</span></span>

<span data-ttu-id="3e7be-123">Server signalizace je obvykle hostován v aplikaci ASP.NET ve službě IIS, ale může být také v místním prostředí (například v konzolové aplikaci nebo ve službě Windows) pomocí knihovny pro samoobslužné hostování.</span><span class="sxs-lookup"><span data-stu-id="3e7be-123">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="3e7be-124">Tato knihovna, stejně jako všechny signály 2, je postavená na OWIN ([Open Web Interface for .NET](http://owin.org)).</span><span class="sxs-lookup"><span data-stu-id="3e7be-124">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="3e7be-125">OWIN definuje abstrakci mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="3e7be-125">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="3e7be-126">OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS.</span><span class="sxs-lookup"><span data-stu-id="3e7be-126">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="3e7be-127">Důvody pro nehostování ve službě IIS zahrnují:</span><span class="sxs-lookup"><span data-stu-id="3e7be-127">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="3e7be-128">Prostředí, ve kterých služba IIS není k dispozici nebo je žádoucí, jako je například existující serverová farma bez služby IIS.</span><span class="sxs-lookup"><span data-stu-id="3e7be-128">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="3e7be-129">Nároky na výkon služby IIS je třeba vyhnout.</span><span class="sxs-lookup"><span data-stu-id="3e7be-129">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="3e7be-130">Funkce signalizace se přidá do existující aplikace, která běží ve službě Windows, v roli pracovního procesu Azure nebo v jiném procesu.</span><span class="sxs-lookup"><span data-stu-id="3e7be-130">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="3e7be-131">Pokud je řešení vyvíjené jako samostatný hostitel z důvodů výkonu, doporučuje se také otestovat aplikaci hostovanou službou IIS, aby se zjistilo zvýhodnění výkonu.</span><span class="sxs-lookup"><span data-stu-id="3e7be-131">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="3e7be-132">Tento kurz obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="3e7be-132">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="3e7be-133">Vytvoření serveru</span><span class="sxs-lookup"><span data-stu-id="3e7be-133">Creating the server</span></span>](#server)
- [<span data-ttu-id="3e7be-134">Přístup k serveru pomocí JavaScriptového klienta</span><span class="sxs-lookup"><span data-stu-id="3e7be-134">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="3e7be-135">Vytvoření serveru</span><span class="sxs-lookup"><span data-stu-id="3e7be-135">Creating the server</span></span>

<span data-ttu-id="3e7be-136">V tomto kurzu vytvoříte Server, který je hostovaný v konzolové aplikaci, ale server se může hostovat v jakémkoli procesu, jako je například služba systému Windows nebo role pracovního procesu Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7be-136">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="3e7be-137">Vzorový kód pro hostování serveru signalizace ve službě systému Windows najdete v tématu [signál pro samoobslužné hostování ve službě systému Windows](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span><span class="sxs-lookup"><span data-stu-id="3e7be-137">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="3e7be-138">Otevřete Visual Studio 2013 s oprávněními správce.</span><span class="sxs-lookup"><span data-stu-id="3e7be-138">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="3e7be-139">Vyberte **soubor**, **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-139">Select **File**, **New Project**.</span></span> <span data-ttu-id="3e7be-140">V uzlu  **C# vizuálu** v podokně **šablony** vyberte možnost **Windows** a vyberte šablonu **Konzolová aplikace** .</span><span class="sxs-lookup"><span data-stu-id="3e7be-140">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="3e7be-141">Pojmenujte nový projekt "SignalRSelfHost" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-141">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="3e7be-142">Otevřete konzolu Správce balíčků NuGet výběrem **nástrojů** > **správce balíčků NuGet** > **konzole správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-142">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="3e7be-143">V konzole správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="3e7be-143">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="3e7be-144">Tento příkaz přidá do projektu knihovny pro samoobslužné hostování Signal 2.</span><span class="sxs-lookup"><span data-stu-id="3e7be-144">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="3e7be-145">V konzole správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="3e7be-145">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="3e7be-146">Tento příkaz přidá do projektu knihovnu Microsoft. Owin. Cors.</span><span class="sxs-lookup"><span data-stu-id="3e7be-146">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="3e7be-147">Tato knihovna se bude používat pro podporu mezi doménami, která je nutná pro aplikace, které hostuje signál a klienta webové stránky v různých doménách.</span><span class="sxs-lookup"><span data-stu-id="3e7be-147">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="3e7be-148">Vzhledem k tomu, že budete hostovat server signálu a webového klienta na různých portech, znamená to, že pro komunikaci mezi těmito součástmi musí být povolena mezidoménová služba.</span><span class="sxs-lookup"><span data-stu-id="3e7be-148">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="3e7be-149">Obsah Program.cs nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="3e7be-149">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="3e7be-150">Výše uvedený kód zahrnuje tři třídy:</span><span class="sxs-lookup"><span data-stu-id="3e7be-150">The above code includes three classes:</span></span>

    - <span data-ttu-id="3e7be-151">**Program**, včetně metody **Main** definující primární cestu provádění.</span><span class="sxs-lookup"><span data-stu-id="3e7be-151">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="3e7be-152">V této metodě se webová aplikace typu **spuštění** spouští na zadané adrese URL (`http://localhost:8080`).</span><span class="sxs-lookup"><span data-stu-id="3e7be-152">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="3e7be-153">Pokud je na koncovém bodu vyžadováno zabezpečení, může být implementován protokol SSL.</span><span class="sxs-lookup"><span data-stu-id="3e7be-153">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="3e7be-154">Další informace najdete v tématu [Postup: Konfigurace portu s certifikátem SSL](https://msdn.microsoft.com/library/ms733791.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3e7be-154">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="3e7be-155">**Po spuštění**třída obsahující konfiguraci serveru signalizace (jediná konfigurace, kterou tento kurz používá, je volání `UseCors`) a volání `MapSignalR`, které vytváří trasy pro všechny objekty hub v projektu.</span><span class="sxs-lookup"><span data-stu-id="3e7be-155">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="3e7be-156">**MyHub**, třída centra signálů, kterou aplikace bude poskytovat klientům.</span><span class="sxs-lookup"><span data-stu-id="3e7be-156">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="3e7be-157">Tato třída má jedinou metodu, kterou klienti budou **volat, aby**vysílaly zprávu všem ostatním připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="3e7be-157">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="3e7be-158">Zkompilujte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="3e7be-158">Compile and run the application.</span></span> <span data-ttu-id="3e7be-159">Adresa, na které je spuštěn server, by měla být zobrazena v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="3e7be-159">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="3e7be-160">Pokud spuštění selže s výjimkou `System.Reflection.TargetInvocationException was unhandled`, bude nutné restartovat aplikaci Visual Studio s oprávněními správce.</span><span class="sxs-lookup"><span data-stu-id="3e7be-160">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="3e7be-161">Než budete pokračovat k další části, zastavte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="3e7be-161">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="3e7be-162">Přístup k serveru pomocí JavaScriptového klienta</span><span class="sxs-lookup"><span data-stu-id="3e7be-162">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="3e7be-163">V této části použijete stejného klienta JavaScriptu v [kurzu Začínáme](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="3e7be-163">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="3e7be-164">Klientovi provedeme jenom jednu změnu, která bude explicitně definovat adresu URL centra.</span><span class="sxs-lookup"><span data-stu-id="3e7be-164">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="3e7be-165">V případě samoobslužné aplikace nemusí být server nutně na stejné adrese jako adresa URL připojení (z důvodu reverzních proxy serverů a nástrojů pro vyrovnávání zatížení), takže adresu URL je potřeba definovat explicitně.</span><span class="sxs-lookup"><span data-stu-id="3e7be-165">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="3e7be-166">V **Průzkumník řešení**klikněte pravým tlačítkem na řešení a vyberte **Přidat**, **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-166">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="3e7be-167">Vyberte uzel **Web** a vyberte šablonu **webové aplikace ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="3e7be-167">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="3e7be-168">Pojmenujte projekt "JavascriptClient" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-168">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="3e7be-169">Vyberte **prázdnou** šablonu a nechejte zbývající možnosti nevybrané.</span><span class="sxs-lookup"><span data-stu-id="3e7be-169">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="3e7be-170">Vyberte **vytvořit projekt**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-170">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="3e7be-171">V konzole správce balíčků vyberte projekt "JavascriptClient" v rozevíracím seznamu **výchozí projekt** a spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="3e7be-171">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="3e7be-172">Tento příkaz nainstaluje do klienta knihovny pro signalizaci a JQuery, které budete potřebovat.</span><span class="sxs-lookup"><span data-stu-id="3e7be-172">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="3e7be-173">Klikněte pravým tlačítkem na projekt a vyberte **Přidat**, **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-173">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="3e7be-174">Vyberte uzel **Web** a vyberte stránku HTML.</span><span class="sxs-lookup"><span data-stu-id="3e7be-174">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="3e7be-175">Pojmenujte stránku **Default. html**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-175">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="3e7be-176">Obsah nové stránky HTML nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="3e7be-176">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="3e7be-177">Ověřte, zda odkazy na skript zde odpovídají skriptům ve složce Scripts v projektu.</span><span class="sxs-lookup"><span data-stu-id="3e7be-177">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="3e7be-178">Následující kód (zvýrazněný výše v ukázce kódu výše) je přidání, které jste provedli pro klienta použitého v kurzu získání vloženého textu (kromě upgradu kódu na Signal verze 2 Beta).</span><span class="sxs-lookup"><span data-stu-id="3e7be-178">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="3e7be-179">Tento řádek kódu explicitně nastavuje základní adresu URL pro signál na serveru.</span><span class="sxs-lookup"><span data-stu-id="3e7be-179">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="3e7be-180">Klikněte pravým tlačítkem na řešení a vyberte **nastavit projekty po spuštění...** . Vyberte přepínač **více projektů po spuštění** a nastavte **akci** u obou projektů na **Spustit**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-180">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="3e7be-181">Klikněte pravým tlačítkem na Default. html a vyberte **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="3e7be-181">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="3e7be-182">Spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="3e7be-182">Run the application.</span></span> <span data-ttu-id="3e7be-183">Spustí se server a stránka.</span><span class="sxs-lookup"><span data-stu-id="3e7be-183">The server and page will launch.</span></span> <span data-ttu-id="3e7be-184">Pokud se stránka načte před spuštěním serveru, může být nutné znovu načíst webovou stránku (nebo v ladicím programu vybrat možnost **pokračovat** ).</span><span class="sxs-lookup"><span data-stu-id="3e7be-184">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="3e7be-185">Po zobrazení výzvy zadejte v prohlížeči uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="3e7be-185">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="3e7be-186">Zkopírujte adresu URL stránky do jiné karty nebo okna prohlížeče a zadejte jiné uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="3e7be-186">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="3e7be-187">Můžete odesílat zprávy z jednoho podokna prohlížeče do druhé, jako v kurzu Začínáme.</span><span class="sxs-lookup"><span data-stu-id="3e7be-187">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>
