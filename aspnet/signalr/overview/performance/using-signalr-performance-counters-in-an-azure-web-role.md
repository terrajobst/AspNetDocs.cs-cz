---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Použití čítačů výkonu signalizace ve webové roli Azure | Microsoft Docs
author: guardrex
description: Jak nainstalovat a používat čítače výkonu signálů ve webové roli Azure
keywords: ASP. NET, signaler, čítač výkonu, Webová role Azure
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 969a2ce43a7cb8d649555daf282f900401c0c914
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578979"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="6607c-104">Použití čítačů výkonu signalizace ve webové roli Azure</span><span class="sxs-lookup"><span data-stu-id="6607c-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="6607c-105">Od [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="6607c-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="6607c-106">Čítače výkonu signálu se používají ke sledování výkonu vaší aplikace ve webové roli Azure.</span><span class="sxs-lookup"><span data-stu-id="6607c-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="6607c-107">Čítače jsou zachyceny Diagnostika Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6607c-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="6607c-108">Čítače výkonu signálu do Azure nainstalujete pomocí nástroje *Signal. exe*, který se používá pro samostatné i místní aplikace.</span><span class="sxs-lookup"><span data-stu-id="6607c-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="6607c-109">Vzhledem k tomu, že role Azure jsou přechodné, nakonfigurujete aplikaci, která bude instalovat a registrovat čítače výkonu signálu při spuštění.</span><span class="sxs-lookup"><span data-stu-id="6607c-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6607c-110">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="6607c-110">Prerequisites</span></span>

* <span data-ttu-id="6607c-111">Visual Studio 2015 nebo [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="6607c-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="6607c-112">Poznámka [k sadě Microsoft Azure SDK pro Visual Studio](https://azure.microsoft.com/downloads/) **: po instalaci sady SDK restartujte počítač.**</span><span class="sxs-lookup"><span data-stu-id="6607c-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="6607c-113">Předplatné Microsoft Azure: Pokud si chcete zaregistrovat bezplatný zkušební účet Azure, podívejte se na [bezplatnou zkušební verzi Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6607c-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="6607c-114">Vytvoření aplikace webové role Azure, která zpřístupňuje čítače výkonu signálů</span><span class="sxs-lookup"><span data-stu-id="6607c-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="6607c-115">Otevřete sadu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6607c-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="6607c-116">V aplikaci Visual Studio vyberte **soubor** > **Nový** > **projekt**.</span><span class="sxs-lookup"><span data-stu-id="6607c-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="6607c-117">V dialogovém okně **Nový projekt** vyberte na levé straně kategorii **cloudu**  **C# Visual** > a pak vyberte šablonu **cloudové služby Azure** .</span><span class="sxs-lookup"><span data-stu-id="6607c-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="6607c-118">Pojmenujte aplikaci **SignalRPerfCounters** a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6607c-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![Nová cloudová aplikace](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="6607c-120">Pokud nevidíte kategorii **cloudové** šablony nebo šablonu **cloudové služby Azure** , musíte nainstalovat **vývojovou úlohu Azure** pro Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6607c-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="6607c-121">Kliknutím na odkaz **otevřít instalační program pro Visual Studio** v levé dolní části dialogového okna **nový projekt** otevřete instalační program pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6607c-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="6607c-122">Vyberte úlohu **vývoje Azure** a pak kliknutím na tlačítko **změnit** spusťte instalaci úlohy.</span><span class="sxs-lookup"><span data-stu-id="6607c-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Úlohy vývoje Azure v Instalační program pro Visual Studio](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="6607c-124">V dialogovém okně **nová Microsoft Azure cloudová služba** vyberte **Webová role ASP.NET** a kliknutím na tlačítko > přidejte do projektu roli.</span><span class="sxs-lookup"><span data-stu-id="6607c-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="6607c-125">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6607c-125">Select **OK**.</span></span>

   ![Přidat webovou roli ASP.NET](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="6607c-127">V dialogovém okně **Nová webová aplikace v ASP.NET – WebRole1** vyberte šablonu **MVC** a pak vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6607c-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![Přidat MVC a webové rozhraní API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="6607c-129">V **Průzkumník řešení**otevřete soubor *Diagnostics. wadcfgx* pod **WebRole1**.</span><span class="sxs-lookup"><span data-stu-id="6607c-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![Průzkumník řešení Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="6607c-131">Nahraďte obsah souboru následující konfigurací a uložte soubor:</span><span class="sxs-lookup"><span data-stu-id="6607c-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="6607c-132">Otevřete **konzolu Správce balíčků** z **nástrojů** > **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6607c-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="6607c-133">Zadáním následujících příkazů nainstalujte nejnovější verzi nástroje Signaler a balíček nástrojů pro signalizaci:</span><span class="sxs-lookup"><span data-stu-id="6607c-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="6607c-134">Nakonfigurujte aplikaci tak, aby při spuštění nebo recyklaci do instance role instalovala čítače výkonu signálu.</span><span class="sxs-lookup"><span data-stu-id="6607c-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="6607c-135">V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **WebRole1** a vyberte **Přidat** > **Nová složka**.</span><span class="sxs-lookup"><span data-stu-id="6607c-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="6607c-136">Pojmenujte nové *spuštění*složky.</span><span class="sxs-lookup"><span data-stu-id="6607c-136">Name the new folder *Startup*.</span></span>

   ![Přidat složku po spuštění](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="6607c-138">Zkopírujte soubor *Signal. exe* (přidaný do balíčku **Microsoft. ASPNET. signaler. util** ) z \<složky projektu >/SignalRPerfCounters/Packages/Microsoft.ASPNET.SignalR.utils.\<verze >/Tools do složky *po spuštění* , kterou jste vytvořili v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="6607c-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="6607c-139">V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku *po spuštění* a vyberte **Přidat** > **existující položku**.</span><span class="sxs-lookup"><span data-stu-id="6607c-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="6607c-140">V dialogovém okně, které se zobrazí, vyberte možnost *signaler. exe* a vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6607c-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![Přidat Signal. exe do projektu](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="6607c-142">Pravým tlačítkem myši klikněte na složku *po spuštění* , kterou jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="6607c-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="6607c-143">Vyberte **přidat** > **novou položku**.</span><span class="sxs-lookup"><span data-stu-id="6607c-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="6607c-144">Vyberte uzel **Obecné** , vyberte **textový soubor**a pojmenujte novou položku *SignalRPerfCounterInstall. cmd*.</span><span class="sxs-lookup"><span data-stu-id="6607c-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="6607c-145">Tento soubor příkazů nainstaluje do webové role čítače výkonu signálu.</span><span class="sxs-lookup"><span data-stu-id="6607c-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![Vytvořit instalační dávkový soubor čítače výkonu signál](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="6607c-147">Když Visual Studio vytvoří soubor *SignalRPerfCounterInstall. cmd* , automaticky se otevře v hlavním okně.</span><span class="sxs-lookup"><span data-stu-id="6607c-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="6607c-148">Obsah souboru nahraďte následujícím skriptem a pak soubor uložte a zavřete.</span><span class="sxs-lookup"><span data-stu-id="6607c-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="6607c-149">Tento skript provede *signál. exe*, který přidá čítače výkonu signalizace do instance role.</span><span class="sxs-lookup"><span data-stu-id="6607c-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="6607c-150">V **Průzkumník řešení**vyberte soubor *signaler. exe* .</span><span class="sxs-lookup"><span data-stu-id="6607c-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="6607c-151">Ve **vlastnostech**souboru nastavte **Kopírovat do výstupního adresáře** na **Kopírovat vždy**.</span><span class="sxs-lookup"><span data-stu-id="6607c-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![Nastavit kopírovat do výstupního adresáře na vždycky kopírovat](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="6607c-153">Opakujte předchozí krok pro soubor *SignalRPerfCounterInstall. cmd* .</span><span class="sxs-lookup"><span data-stu-id="6607c-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="6607c-154">Klikněte pravým tlačítkem myši na soubor *SignalRPerfCounterInstall. cmd* a vyberte možnost **otevřít v programu**.</span><span class="sxs-lookup"><span data-stu-id="6607c-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="6607c-155">V dialogovém okně, které se zobrazí, vyberte **binární editor** a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6607c-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![Otevřít v binárním editoru](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="6607c-157">V binárním editoru vyberte v souboru všechny úvodní bajty a odstraňte je.</span><span class="sxs-lookup"><span data-stu-id="6607c-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="6607c-158">Uložte soubor a zavřete ho.</span><span class="sxs-lookup"><span data-stu-id="6607c-158">Save and close the file.</span></span>

    ![Odstranit úvodní bajty](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="6607c-160">Otevřete *ServiceDefinition. csdef* a přidejte úlohu po spuštění, která při spuštění služby spustí soubor *SignalrPerfCounterInstall. cmd* :</span><span class="sxs-lookup"><span data-stu-id="6607c-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="6607c-161">Otevřete `Views/Shared/_Layout.cshtml` a z konce souboru odeberte skript sady jQuery.</span><span class="sxs-lookup"><span data-stu-id="6607c-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="6607c-162">Přidejte klienta JavaScriptu, který nepřetržitě zavolá metodu `increment` na serveru.</span><span class="sxs-lookup"><span data-stu-id="6607c-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="6607c-163">Otevřete `Views/Home/Index.cshtml` a nahraďte obsah následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="6607c-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="6607c-164">Vytvořte novou složku v projektu **WebRole1** s názvem *Centers*.</span><span class="sxs-lookup"><span data-stu-id="6607c-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="6607c-165">Klikněte pravým tlačítkem na složku *Centers* v **Průzkumník řešení** a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="6607c-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="6607c-166">V dialogovém okně **Přidat novou položku** vyberte kategorii **signalizace** **webového** > a pak vyberte šablonu položky **třídy centra (v2) pro rozbočovače signálu** .</span><span class="sxs-lookup"><span data-stu-id="6607c-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="6607c-167">Zadejte název nového centra *MyHub.cs* a vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6607c-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![Přidání třídy centra signalizace do složky Center v dialogovém okně Přidat novou položku](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="6607c-169">*MyHub.cs* se automaticky otevře v hlavním okně.</span><span class="sxs-lookup"><span data-stu-id="6607c-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="6607c-170">Nahraďte obsah následujícím kódem a pak soubor uložte a zavřete:</span><span class="sxs-lookup"><span data-stu-id="6607c-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="6607c-171">*[Crank. exe](signalr-connection-density-testing-with-crank.md)* je nástroj pro testování hustoty připojení, který je k dispozici v základu signálu.</span><span class="sxs-lookup"><span data-stu-id="6607c-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="6607c-172">Vzhledem k tomu, že Crank vyžaduje trvalé připojení, přidejte ho do svého webu pro použití při testování.</span><span class="sxs-lookup"><span data-stu-id="6607c-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="6607c-173">Přidejte novou složku do projektu **WebRole1** s názvem *PersistentConnections*.</span><span class="sxs-lookup"><span data-stu-id="6607c-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="6607c-174">Klikněte pravým tlačítkem na tuto složku a vyberte **přidat** > **třídy**.</span><span class="sxs-lookup"><span data-stu-id="6607c-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="6607c-175">Pojmenujte nový soubor třídy *MyPersistentConnections.cs* a vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6607c-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="6607c-176">Visual Studio otevře soubor *MyPersistentConnections.cs* v hlavním okně.</span><span class="sxs-lookup"><span data-stu-id="6607c-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="6607c-177">Nahraďte obsah následujícím kódem a pak soubor uložte a zavřete:</span><span class="sxs-lookup"><span data-stu-id="6607c-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="6607c-178">Pomocí třídy `Startup` se objekty signalizace spouštějí při spuštění OWIN.</span><span class="sxs-lookup"><span data-stu-id="6607c-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="6607c-179">Otevřete nebo vytvořte *Startup.cs* a nahraďte obsah následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="6607c-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="6607c-180">V kódu výše atribut `OwinStartup` označuje tuto třídu jako počáteční OWIN.</span><span class="sxs-lookup"><span data-stu-id="6607c-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="6607c-181">Metoda `Configuration` spustí signál.</span><span class="sxs-lookup"><span data-stu-id="6607c-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="6607c-182">Otestujte aplikaci v Microsoft Azure Emulator stisknutím klávesy **F5**.</span><span class="sxs-lookup"><span data-stu-id="6607c-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6607c-183">Pokud narazíte na **FileLoadException** na **MapSignalR**, změňte přesměrování vazby v *souboru Web. config* na následující:</span><span class="sxs-lookup"><span data-stu-id="6607c-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="6607c-184">Počkejte asi jednu minutu.</span><span class="sxs-lookup"><span data-stu-id="6607c-184">Wait about one minute.</span></span> <span data-ttu-id="6607c-185">V aplikaci Visual Studio otevřete okno nástroje Průzkumník cloudu (**zobrazit** > **Průzkumník cloudu**) a rozbalte cestu `(Local)/Storage Accounts/(Development)/Tables`.</span><span class="sxs-lookup"><span data-stu-id="6607c-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="6607c-186">Dvakrát klikněte na **WADPerformanceCountersTable**.</span><span class="sxs-lookup"><span data-stu-id="6607c-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="6607c-187">V datech tabulky by se měly zobrazit čítače signalizace.</span><span class="sxs-lookup"><span data-stu-id="6607c-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="6607c-188">Pokud tabulku nevidíte, možná budete muset znovu zadat přihlašovací údaje Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6607c-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="6607c-189">Možná budete muset vybrat tlačítko **aktualizovat** , aby se zobrazila tabulka v **Průzkumníku cloudu** , nebo kliknutím na tlačítko **aktualizovat** v okně Otevřít tabulku zobrazit data v tabulce.</span><span class="sxs-lookup"><span data-stu-id="6607c-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Výběr tabulky čítače výkonu WAD v Průzkumníkovi cloudu sady Visual Studio](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![Zobrazuje se počítadla shromážděná v tabulce čítače výkonu WAD.](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="6607c-192">Pokud chcete otestovat aplikaci v cloudu, aktualizujte soubor **ServiceConfiguration. Cloud. cscfg** a nastavte `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` na platný připojovací řetězec Azure Storage účtu.</span><span class="sxs-lookup"><span data-stu-id="6607c-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="6607c-193">Nasaďte aplikaci do svého předplatného Azure.</span><span class="sxs-lookup"><span data-stu-id="6607c-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="6607c-194">Podrobnosti o tom, jak nasadit aplikaci do Azure, najdete v tématu [jak vytvořit a nasadit cloudovou službu](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="6607c-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="6607c-195">Počkejte několik minut.</span><span class="sxs-lookup"><span data-stu-id="6607c-195">Wait a few minutes.</span></span> <span data-ttu-id="6607c-196">V **Průzkumníku cloudu**vyhledejte účet úložiště, který jste nakonfigurovali výše, a vyhledejte v něm tabulku `WADPerformanceCountersTable`.</span><span class="sxs-lookup"><span data-stu-id="6607c-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="6607c-197">V datech tabulky by se měly zobrazit čítače signalizace.</span><span class="sxs-lookup"><span data-stu-id="6607c-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="6607c-198">Pokud tabulku nevidíte, možná budete muset znovu zadat přihlašovací údaje Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6607c-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="6607c-199">Možná budete muset vybrat tlačítko **aktualizovat** , aby se zobrazila tabulka v **Průzkumníku cloudu** , nebo kliknutím na tlačítko **aktualizovat** v okně Otevřít tabulku zobrazit data v tabulce.</span><span class="sxs-lookup"><span data-stu-id="6607c-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="6607c-200">Pro původní obsah použitý v tomto kurzu se speciálním obsahem myslíme na [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) .</span><span class="sxs-lookup"><span data-stu-id="6607c-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
