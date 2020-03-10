---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 'Kurz: chat v reálném čase s nástrojem Signal 2 | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se naučíte používat funkci SignalR k vytvoření aplikace pro chatování v reálném čase. Přidáte signál do prázdné webové aplikace v ASP.NET.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536979"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="6268e-104">Kurz: chat v reálném čase s nástrojem Signal 2</span><span class="sxs-lookup"><span data-stu-id="6268e-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="6268e-105">V tomto kurzu se dozvíte, jak pomocí signalizace vytvořit aplikaci Chat v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="6268e-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="6268e-106">Přidáte signál do prázdné webové aplikace v ASP.NET a vytvoříte stránku HTML pro odesílání a zobrazování zpráv.</span><span class="sxs-lookup"><span data-stu-id="6268e-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="6268e-107">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="6268e-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6268e-108">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="6268e-108">Set up the project</span></span>
> * <span data-ttu-id="6268e-109">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="6268e-109">Run the sample</span></span>
> * <span data-ttu-id="6268e-110">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="6268e-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="6268e-111">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="6268e-111">Prerequisites</span></span>

* <span data-ttu-id="6268e-112">Sada [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) se sadou funkcí **Vývoj pro ASP.NET a web**.</span><span class="sxs-lookup"><span data-stu-id="6268e-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="6268e-113">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="6268e-113">Set up the Project</span></span>

<span data-ttu-id="6268e-114">V této části se dozvíte, jak použít Visual Studio 2017 a Signal 2 k vytvoření prázdné webové aplikace v ASP.NET, přidání signálu a vytvoření aplikace chatu.</span><span class="sxs-lookup"><span data-stu-id="6268e-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="6268e-115">V aplikaci Visual Studio vytvořte webovou aplikaci v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6268e-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Vytvoření webu](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="6268e-117">V okně **Nový projekt ASP.NET – SignalRChat** ponechte vybrané **prázdné** a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6268e-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="6268e-118">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="6268e-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="6268e-119">V **příkaz Přidat novou položku-SignalRChat**vyberte možnost **nainstalováno** \*\* > C# > \*\* webového \*\* > a\*\* vyberte položku **centrum signalizace (v2)** .</span><span class="sxs-lookup"><span data-stu-id="6268e-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="6268e-120">Pojmenujte třídu *ChatHub* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="6268e-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="6268e-121">Tento krok vytvoří soubor třídy *ChatHub.cs* a přidá sadu souborů skriptu a odkazy na sestavení, které podporují signalizaci do projektu.</span><span class="sxs-lookup"><span data-stu-id="6268e-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="6268e-122">Nahraďte kód v novém souboru třídy *ChatHub.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="6268e-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="6268e-123">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="6268e-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="6268e-124">V **položce Přidat novou položku – SignalRChat** vyberte **nainstalované** > **Visual C#**  > **Web** a pak vyberte **třídu pro spuštění Owin**.</span><span class="sxs-lookup"><span data-stu-id="6268e-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="6268e-125">Pojmenujte *spouštěcí* třídu a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="6268e-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="6268e-126">Nahraďte výchozí kód ve *spouštěcí* třídě tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="6268e-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="6268e-127">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **stránku HTML**.</span><span class="sxs-lookup"><span data-stu-id="6268e-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="6268e-128">Pojmenujte nový *index* stránky a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6268e-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="6268e-129">V **Průzkumník řešení**klikněte pravým tlačítkem na stránku HTML, kterou jste vytvořili, a vyberte **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="6268e-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="6268e-130">Nahraďte výchozí kód na stránce HTML tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="6268e-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="6268e-131">V **Průzkumník řešení**rozbalte položku **skripty**.</span><span class="sxs-lookup"><span data-stu-id="6268e-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="6268e-132">Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.</span><span class="sxs-lookup"><span data-stu-id="6268e-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6268e-133">Správce balíčků možná nainstaloval novější verzi skriptů nástroje Signaler.</span><span class="sxs-lookup"><span data-stu-id="6268e-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="6268e-134">Ověřte, zda odkazy skriptu v bloku kódu odpovídají verzím souborů skriptu v projektu.</span><span class="sxs-lookup"><span data-stu-id="6268e-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="6268e-135">Odkazy skriptu z původního bloku kódu:</span><span class="sxs-lookup"><span data-stu-id="6268e-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="6268e-136">Pokud se neshodují, aktualizujte soubor *. html* .</span><span class="sxs-lookup"><span data-stu-id="6268e-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="6268e-137">V řádku nabídek vyberte **soubor** > **Uložit vše**.</span><span class="sxs-lookup"><span data-stu-id="6268e-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="6268e-138">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="6268e-138">Run the Sample</span></span>

1. <span data-ttu-id="6268e-139">Na panelu nástrojů zapněte **ladění skriptů** a pak výběrem tlačítka Přehrát spusťte ukázku v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="6268e-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="6268e-141">Po otevření prohlížeče zadejte název vaší identity chatu.</span><span class="sxs-lookup"><span data-stu-id="6268e-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="6268e-142">Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.</span><span class="sxs-lookup"><span data-stu-id="6268e-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="6268e-143">V každém prohlížeči zadejte jedinečný název.</span><span class="sxs-lookup"><span data-stu-id="6268e-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="6268e-144">Nyní přidejte komentář a vyberte **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="6268e-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="6268e-145">Tento postup opakujte v ostatních prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="6268e-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="6268e-146">Komentáře se zobrazí v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="6268e-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6268e-147">Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru.</span><span class="sxs-lookup"><span data-stu-id="6268e-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="6268e-148">Centrum vysílá komentáře všem aktuálním uživatelům.</span><span class="sxs-lookup"><span data-stu-id="6268e-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="6268e-149">Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.</span><span class="sxs-lookup"><span data-stu-id="6268e-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="6268e-150">Podívejte se, jak aplikace chat běží ve třech různých prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="6268e-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="6268e-151">Když Anand a Zuzana odesílají zprávy, všechny prohlížeče se aktualizují v reálném čase:</span><span class="sxs-lookup"><span data-stu-id="6268e-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Všechny tři prohlížeče zobrazují stejnou historii chatu.](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="6268e-153">V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6268e-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="6268e-154">K dispozici je soubor skriptu s názvem *centra* , který knihovna signálů generuje za běhu.</span><span class="sxs-lookup"><span data-stu-id="6268e-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="6268e-155">Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="6268e-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![automaticky vygenerovaný skript Centers v uzlu dokumenty skriptu](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="6268e-157">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="6268e-157">Examine the Code</span></span>

<span data-ttu-id="6268e-158">Aplikace SignalRChat ukazuje dva základní úlohy vývoje signálu.</span><span class="sxs-lookup"><span data-stu-id="6268e-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="6268e-159">Ukazuje, jak vytvořit centrum.</span><span class="sxs-lookup"><span data-stu-id="6268e-159">It shows you how to create a hub.</span></span> <span data-ttu-id="6268e-160">Server používá toto centrum jako hlavní objekt koordinace.</span><span class="sxs-lookup"><span data-stu-id="6268e-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="6268e-161">Centrum používá ke posílání a přijímání zpráv knihovnu jQuery nástroje Signal.</span><span class="sxs-lookup"><span data-stu-id="6268e-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="6268e-162">Rozbočovače signálů v ChatHub.cs</span><span class="sxs-lookup"><span data-stu-id="6268e-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="6268e-163">Ve výše uvedeném příkladu kódu je třída `ChatHub` odvozena od `Microsoft.AspNet.SignalR.Hub` třídy.</span><span class="sxs-lookup"><span data-stu-id="6268e-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="6268e-164">Odvození od `Hub` třídy je užitečný způsob, jak vytvořit aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="6268e-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="6268e-165">Veřejné metody můžete vytvořit na třídě centra a pak je použít tak, že je zavoláte ze skriptů na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="6268e-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="6268e-166">V kódu chatu klienti volají metodu `ChatHub.Send` k odeslání nové zprávy.</span><span class="sxs-lookup"><span data-stu-id="6268e-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="6268e-167">Centrum pak pošle zprávu všem klientům voláním `Clients.All.broadcastMessage`.</span><span class="sxs-lookup"><span data-stu-id="6268e-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="6268e-168">Metoda `Send` ukazuje několik konceptů centra:</span><span class="sxs-lookup"><span data-stu-id="6268e-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="6268e-169">Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.</span><span class="sxs-lookup"><span data-stu-id="6268e-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="6268e-170">`Microsoft.AspNet.SignalR.Hub.Clients` dynamickou vlastnost můžete použít ke komunikaci se všemi klienty připojenými k tomuto centru.</span><span class="sxs-lookup"><span data-stu-id="6268e-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="6268e-171">Chcete-li aktualizovat klienty, zavolejte na klienta funkci (například funkce `broadcastMessage`).</span><span class="sxs-lookup"><span data-stu-id="6268e-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="6268e-172">Signál a jQuery v souboru index. html</span><span class="sxs-lookup"><span data-stu-id="6268e-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="6268e-173">Stránka *index. html* v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace.</span><span class="sxs-lookup"><span data-stu-id="6268e-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="6268e-174">Kód provede mnoho důležitých úloh.</span><span class="sxs-lookup"><span data-stu-id="6268e-174">The code carries out many important tasks.</span></span> <span data-ttu-id="6268e-175">Deklaruje proxy server pro odkazování na centrum, deklaruje funkci, kterou může server volat, aby zavolal obsah do klientů, a spustí připojení k odesílání zpráv do centra.</span><span class="sxs-lookup"><span data-stu-id="6268e-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="6268e-176">V JavaScriptu odkaz na třídu serveru a jeho členové musí být camelCase.</span><span class="sxs-lookup"><span data-stu-id="6268e-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="6268e-177">Ukázka kódu odkazuje na C# třídu *ChatHub* v jazyce JavaScript jako `chatHub`.</span><span class="sxs-lookup"><span data-stu-id="6268e-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="6268e-178">V tomto bloku kódu vytvoříte ve skriptu funkci zpětného volání.</span><span class="sxs-lookup"><span data-stu-id="6268e-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="6268e-179">Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi.</span><span class="sxs-lookup"><span data-stu-id="6268e-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="6268e-180">Dva řádky, které obsah ve formátu HTML kóduje před jeho zobrazením, jsou volitelné a zobrazují dobrý způsob, jak zabránit vkládání skriptu.</span><span class="sxs-lookup"><span data-stu-id="6268e-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="6268e-181">Tento kód otevře připojení k centru.</span><span class="sxs-lookup"><span data-stu-id="6268e-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="6268e-182">Tento přístup zajišťuje, že kód vytvoří připojení před tím, než se spustí obslužná rutina události.</span><span class="sxs-lookup"><span data-stu-id="6268e-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="6268e-183">Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce HTML.</span><span class="sxs-lookup"><span data-stu-id="6268e-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="6268e-184">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="6268e-184">Get the code</span></span>

[<span data-ttu-id="6268e-185">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="6268e-185">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="6268e-186">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="6268e-186">Additional resources</span></span>

<span data-ttu-id="6268e-187">Další informace o signalizaci naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="6268e-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="6268e-188">Projekt signálu</span><span class="sxs-lookup"><span data-stu-id="6268e-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="6268e-189">GitHub a ukázky signálů</span><span class="sxs-lookup"><span data-stu-id="6268e-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="6268e-190">Wiki signálu</span><span class="sxs-lookup"><span data-stu-id="6268e-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="6268e-191">Další kroky</span><span class="sxs-lookup"><span data-stu-id="6268e-191">Next steps</span></span>

<span data-ttu-id="6268e-192">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="6268e-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6268e-193">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="6268e-193">Set up the project</span></span>
> * <span data-ttu-id="6268e-194">Byla spuštěna ukázka</span><span class="sxs-lookup"><span data-stu-id="6268e-194">Ran the sample</span></span>
> * <span data-ttu-id="6268e-195">Zkontrolování kódu</span><span class="sxs-lookup"><span data-stu-id="6268e-195">Examined the code</span></span>

<span data-ttu-id="6268e-196">Přejděte k dalšímu článku, kde se dozvíte, jak používat signalizaci a MVC 5.</span><span class="sxs-lookup"><span data-stu-id="6268e-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6268e-197">Signal 2 a MVC 5</span><span class="sxs-lookup"><span data-stu-id="6268e-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)