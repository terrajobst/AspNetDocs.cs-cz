---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 'Kurz: chat v reálném čase s nástrojem Signal 2 a MVC 5 | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se dozvíte, jak pomocí ASP.NET signalizace 2 vytvořit aplikaci chatu v reálném čase. Přidáte signalizaci do aplikace MVC 5.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600474"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="98dd4-104">Kurz: chat v reálném čase s nástrojem Signal 2 a MVC 5</span><span class="sxs-lookup"><span data-stu-id="98dd4-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="98dd4-105">V tomto kurzu se dozvíte, jak pomocí ASP.NET signalizace 2 vytvořit aplikaci chatu v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="98dd4-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="98dd4-106">Přidáte signalizaci do aplikace MVC 5 a vytvoříte zobrazení chatu pro odesílání a zobrazování zpráv.</span><span class="sxs-lookup"><span data-stu-id="98dd4-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="98dd4-107">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="98dd4-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98dd4-108">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="98dd4-108">Set up the project</span></span>
> * <span data-ttu-id="98dd4-109">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="98dd4-109">Run the sample</span></span>
> * <span data-ttu-id="98dd4-110">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="98dd4-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="98dd4-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="98dd4-111">Prerequisites</span></span>

* <span data-ttu-id="98dd4-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) s úlohou **vývoje ASP.NET a webu** .</span><span class="sxs-lookup"><span data-stu-id="98dd4-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="98dd4-113">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="98dd4-113">Set up the Project</span></span>

<span data-ttu-id="98dd4-114">V této části se dozvíte, jak pomocí sady Visual Studio 2017 a nástroje Signal 2 vytvořit prázdnou aplikaci ASP.NET MVC 5, přidat knihovnu signálů a vytvořit aplikaci Chat.</span><span class="sxs-lookup"><span data-stu-id="98dd4-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="98dd4-115">V aplikaci Visual Studio vytvořte aplikaci C# ASP.NET, která cílí na .NET Framework 4,5, pojmenujte ji SignalRChat a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="98dd4-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![Vytvoření webu](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="98dd4-117">V **New ASP.NET Web Application – SignalRMvcChat**vyberte **MVC** a pak vyberte **změnit ověřování**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="98dd4-118">V nabídce **změnit ověřování**vyberte **bez ověřování** a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![Vyberte bez ověřování.](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="98dd4-120">V **New ASP.NET webová aplikace – SignalRMvcChat**vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="98dd4-121">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="98dd4-122">V **příkaz Přidat novou položku-SignalRChat**vyberte možnost **nainstalováno** \*\* > C# > \*\* webového \*\* > a\*\* vyberte položku **centrum signalizace (v2)** .</span><span class="sxs-lookup"><span data-stu-id="98dd4-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="98dd4-123">Pojmenujte třídu *ChatHub* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="98dd4-124">Tento krok vytvoří soubor třídy *ChatHub.cs* a přidá sadu souborů skriptu a odkazy na sestavení, které podporují signalizaci do projektu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="98dd4-125">Nahraďte kód v novém souboru třídy *ChatHub.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="98dd4-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="98dd4-126">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **třídu**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="98dd4-127">Pojmenujte nové *spuštění* třídy a přidejte je do projektu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="98dd4-128">Nahraďte kód v souboru třídy *Startup.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="98dd4-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="98dd4-129">V **Průzkumník řešení**vyberte možnost **řadiče** > **HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="98dd4-130">Přidejte tuto metodu do *HomeController.cs*.</span><span class="sxs-lookup"><span data-stu-id="98dd4-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="98dd4-131">Tato metoda vrátí zobrazení **chatu** , které vytvoříte v pozdějším kroku.</span><span class="sxs-lookup"><span data-stu-id="98dd4-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="98dd4-132">V **Průzkumník řešení**klikněte pravým tlačítkem na **zobrazení** > **Domů**a vyberte **Přidat** >  **zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="98dd4-133">V části **Přidat zobrazení**pojmenujte nové zobrazení **chat** a vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="98dd4-134">Obsah **chat. cshtml** nahraďte tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="98dd4-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="98dd4-135">V **Průzkumník řešení**rozbalte položku **skripty**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="98dd4-136">Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="98dd4-137">Správce balíčků možná nainstaloval novější verzi skriptů nástroje Signaler.</span><span class="sxs-lookup"><span data-stu-id="98dd4-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="98dd4-138">Ověřte, zda odkazy skriptu v bloku kódu odpovídají verzím souborů skriptu v projektu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="98dd4-139">Odkazy skriptu z původního bloku kódu:</span><span class="sxs-lookup"><span data-stu-id="98dd4-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="98dd4-140">Pokud se neshodují, aktualizujte soubor *. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="98dd4-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="98dd4-141">V řádku nabídek vyberte **soubor** > **Uložit vše**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="98dd4-142">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="98dd4-142">Run the Sample</span></span>

1. <span data-ttu-id="98dd4-143">Na panelu nástrojů zapněte **ladění skriptů** a pak výběrem tlačítka Přehrát spusťte ukázku v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="98dd4-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="98dd4-145">Po otevření prohlížeče zadejte název vaší identity chatu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="98dd4-146">Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.</span><span class="sxs-lookup"><span data-stu-id="98dd4-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="98dd4-147">V každém prohlížeči zadejte jedinečný název.</span><span class="sxs-lookup"><span data-stu-id="98dd4-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="98dd4-148">Nyní přidejte komentář a vyberte **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="98dd4-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="98dd4-149">Tento postup opakujte v ostatních prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="98dd4-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="98dd4-150">Komentáře se zobrazí v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="98dd4-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="98dd4-151">Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru.</span><span class="sxs-lookup"><span data-stu-id="98dd4-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="98dd4-152">Centrum vysílá komentáře všem aktuálním uživatelům.</span><span class="sxs-lookup"><span data-stu-id="98dd4-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="98dd4-153">Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.</span><span class="sxs-lookup"><span data-stu-id="98dd4-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="98dd4-154">Podívejte se, jak aplikace chat běží ve třech různých prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="98dd4-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="98dd4-155">Když Anand a Zuzana odesílají zprávy, všechny prohlížeče se aktualizují v reálném čase:</span><span class="sxs-lookup"><span data-stu-id="98dd4-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Všechny tři prohlížeče zobrazují stejnou historii chatu.](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="98dd4-157">V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="98dd4-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="98dd4-158">K dispozici je soubor skriptu s názvem *centra* , který knihovna signálů generuje za běhu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="98dd4-159">Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="98dd4-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![automaticky vygenerovaný skript Centers v uzlu dokumenty skriptu](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="98dd4-161">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="98dd4-161">Examine the Code</span></span>

<span data-ttu-id="98dd4-162">Chatovací aplikace signalizace ukazuje dva základní úlohy vývoje signálu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="98dd4-163">Ukazuje, jak vytvořit centrum.</span><span class="sxs-lookup"><span data-stu-id="98dd4-163">It shows you how to create a hub.</span></span> <span data-ttu-id="98dd4-164">Server používá toto centrum jako hlavní objekt koordinace.</span><span class="sxs-lookup"><span data-stu-id="98dd4-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="98dd4-165">Centrum používá ke posílání a přijímání zpráv knihovnu jQuery nástroje Signal.</span><span class="sxs-lookup"><span data-stu-id="98dd4-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="98dd4-166">Rozbočovače signálů v ChatHub.cs</span><span class="sxs-lookup"><span data-stu-id="98dd4-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="98dd4-167">V ukázce kódu je třída `ChatHub` odvozena od `Microsoft.AspNet.SignalR.Hub` třídy.</span><span class="sxs-lookup"><span data-stu-id="98dd4-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="98dd4-168">Odvození od `Hub` třídy je užitečný způsob, jak vytvořit aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="98dd4-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="98dd4-169">Veřejné metody můžete vytvořit na třídě centra a potom k těmto metodám přistupovat voláním ze skriptů na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="98dd4-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="98dd4-170">V kódu chatu klienti volají metodu `ChatHub.Send` k odeslání nové zprávy.</span><span class="sxs-lookup"><span data-stu-id="98dd4-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="98dd4-171">Centrum pak pošle zprávu všem klientům voláním `Clients.All.addNewMessageToPage`.</span><span class="sxs-lookup"><span data-stu-id="98dd4-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="98dd4-172">Metoda `Send` ukazuje několik konceptů centra:</span><span class="sxs-lookup"><span data-stu-id="98dd4-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="98dd4-173">Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.</span><span class="sxs-lookup"><span data-stu-id="98dd4-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="98dd4-174">`Microsoft.AspNet.SignalR.Hub.Clients` dynamickou vlastnost můžete použít ke komunikaci se všemi klienty připojenými k tomuto centru.</span><span class="sxs-lookup"><span data-stu-id="98dd4-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="98dd4-175">Chcete-li aktualizovat klienty, zavolejte na klienta funkci (například funkce `addNewMessageToPage`).</span><span class="sxs-lookup"><span data-stu-id="98dd4-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="98dd4-176">Signál a jQuery chat. cshtml</span><span class="sxs-lookup"><span data-stu-id="98dd4-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="98dd4-177">Soubor zobrazení *chat. cshtml* v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace.</span><span class="sxs-lookup"><span data-stu-id="98dd4-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="98dd4-178">Kód provede mnoho důležitých úloh.</span><span class="sxs-lookup"><span data-stu-id="98dd4-178">The code carries out many important tasks.</span></span> <span data-ttu-id="98dd4-179">Vytvoří odkaz na automaticky vygenerovaný proxy server pro centrum, deklaruje funkci, kterou může server volat, aby zavolal obsah do klientů, a spustí připojení k odesílání zpráv do centra.</span><span class="sxs-lookup"><span data-stu-id="98dd4-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="98dd4-180">V jazyce JavaScript je odkaz na třídu serveru a jeho členy v camelCase.</span><span class="sxs-lookup"><span data-stu-id="98dd4-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="98dd4-181">Ukázka kódu odkazuje na C# třídu `ChatHub` v jazyce JavaScript jako `chatHub`.</span><span class="sxs-lookup"><span data-stu-id="98dd4-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="98dd4-182">V tomto bloku kódu vytvoříte ve skriptu funkci zpětného volání.</span><span class="sxs-lookup"><span data-stu-id="98dd4-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="98dd4-183">Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi.</span><span class="sxs-lookup"><span data-stu-id="98dd4-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="98dd4-184">Volitelné volání funkce `htmlEncode` ukazuje způsob, jak HTML kódovat obsah zprávy před jeho zobrazením na stránce.</span><span class="sxs-lookup"><span data-stu-id="98dd4-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="98dd4-185">Je to způsob, jak zabránit vkládání skriptu.</span><span class="sxs-lookup"><span data-stu-id="98dd4-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="98dd4-186">Tento kód otevře připojení k centru.</span><span class="sxs-lookup"><span data-stu-id="98dd4-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="98dd4-187">Tento přístup zajišťuje, že navážete připojení, než se spustí obslužná rutina události.</span><span class="sxs-lookup"><span data-stu-id="98dd4-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="98dd4-188">Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce konverzace.</span><span class="sxs-lookup"><span data-stu-id="98dd4-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="98dd4-189">Získat kód</span><span class="sxs-lookup"><span data-stu-id="98dd4-189">Get the code</span></span>

[<span data-ttu-id="98dd4-190">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="98dd4-190">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="98dd4-191">Další materiály a zdroje informací</span><span class="sxs-lookup"><span data-stu-id="98dd4-191">Additional resources</span></span>

<span data-ttu-id="98dd4-192">Další informace o signalizaci naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="98dd4-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="98dd4-193">Projekt signálu</span><span class="sxs-lookup"><span data-stu-id="98dd4-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="98dd4-194">GitHub a ukázky signálů</span><span class="sxs-lookup"><span data-stu-id="98dd4-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="98dd4-195">Wiki signálu</span><span class="sxs-lookup"><span data-stu-id="98dd4-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="98dd4-196">Další kroky</span><span class="sxs-lookup"><span data-stu-id="98dd4-196">Next steps</span></span>

<span data-ttu-id="98dd4-197">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="98dd4-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98dd4-198">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="98dd4-198">Set up the project</span></span>
> * <span data-ttu-id="98dd4-199">Byla spuštěna ukázka</span><span class="sxs-lookup"><span data-stu-id="98dd4-199">Ran the sample</span></span>
> * <span data-ttu-id="98dd4-200">Zkontrolování kódu</span><span class="sxs-lookup"><span data-stu-id="98dd4-200">Examined the code</span></span>

<span data-ttu-id="98dd4-201">V dalším článku se dozvíte, jak vytvořit webovou aplikaci, která používá signál ASP.NET 2 k poskytování funkcí vysoké frekvence zasílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="98dd4-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="98dd4-202">Webová aplikace s vysokou frekvencí zasílání zpráv</span><span class="sxs-lookup"><span data-stu-id="98dd4-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)