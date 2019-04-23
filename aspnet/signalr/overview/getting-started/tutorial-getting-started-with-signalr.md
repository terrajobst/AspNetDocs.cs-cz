---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 'Kurz: Chatování v reálném čase s knihovnou SignalR 2 | Dokumentace Microsoftu'
author: bradygaster
description: V tomto kurzu se naučíte používat funkci SignalR k vytvoření aplikace pro chatování v reálném čase. Přidáte do prázdná webová aplikace ASP.NET SignalR.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: ecc235454d4b95ce660a4373387f44720826b076
ms.sourcegitcommit: 2d53ed9e4c8b19d3526cbc689bfa8394c9449cec
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905641"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="e2fb6-104">Kurz: Chatování v reálném čase s knihovnou SignalR 2</span><span class="sxs-lookup"><span data-stu-id="e2fb6-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="e2fb6-105">V tomto kurzu se dozvíte, jak používat funkci SignalR k vytvoření aplikace pro chatování v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="e2fb6-106">Přidat prázdnou webovou aplikaci ASP.NET SignalR a vytvořte stránku HTML k odeslání a zobrazení zprávy.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="e2fb6-107">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2fb6-108">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="e2fb6-108">Set up the project</span></span>
> * <span data-ttu-id="e2fb6-109">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="e2fb6-109">Run the sample</span></span>
> * <span data-ttu-id="e2fb6-110">Prozkoumejte kód</span><span class="sxs-lookup"><span data-stu-id="e2fb6-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="e2fb6-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e2fb6-111">Prerequisites</span></span>

* <span data-ttu-id="e2fb6-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) s **vývoj pro ASP.NET a web** pracovního vytížení.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="e2fb6-113">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="e2fb6-113">Set up the Project</span></span>

<span data-ttu-id="e2fb6-114">Tato část ukazuje, jak pomocí sady Visual Studio 2017 a knihovnou SignalR 2 můžete vytvořit prázdnou webovou aplikaci ASP.NET, přidejte SignalR a vytvořit chatovací aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="e2fb6-115">V sadě Visual Studio vytvořte webovou aplikaci ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Vytvořte web](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="e2fb6-117">V **nový projekt ASP.NET – SignalRChat** okně, ponechejte tuto položku **prázdný** vybraný a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="e2fb6-118">V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt a vyberte **přidat** > **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="e2fb6-119">V **přidat novou položku - SignalRChat**vyberte **nainstalováno** > **Visual C#**   >  **webové**  >  **SignalR** a pak vyberte **třída rozbočovače SignalR (v2)**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="e2fb6-120">Název třídy *ChatHub* a přidejte ho do projektu.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="e2fb6-121">Tento krok vytvoří *ChatHub.cs* třídy soubor a přidá sadu souborů skriptů a odkazy na sestavení, podporující funkci SignalR k projektu.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="e2fb6-122">Nahraďte kód v novém *ChatHub.cs* soubor třídy s tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="e2fb6-123">V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt a vyberte **přidat** > **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="e2fb6-124">V **přidat novou položku - SignalRChat** vyberte **nainstalováno** > **Visual C#**   >  **webové** a pak Vyberte **třídy pro spuštění OWIN**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="e2fb6-125">Název třídy *spuštění* a přidejte ho do projektu.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="e2fb6-126">Nahraďte kód v *spuštění* třída s tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="e2fb6-127">V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt a vyberte **přidat** > **stránku HTML**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="e2fb6-128">Zadejte název nové stránky *index* a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="e2fb6-129">V **Průzkumníka řešení**, klikněte pravým tlačítkem na stránku HTML, který jste vytvořili a vyberte **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="e2fb6-130">Nahraďte kód výchozí stránku HTML s tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="e2fb6-131">V **Průzkumníka řešení**, rozbalte **skripty**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="e2fb6-132">Jsou viditelné v projektu knihovny skriptů pro knihovny jQuery a SignalR.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e2fb6-133">Správce balíčků nainstalovanou novější verzi skriptů SignalR.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="e2fb6-134">Zkontrolujte, jestli odkazy na skript v bloku kódu, které odpovídají verze souborů skript v projektu.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="e2fb6-135">Odkazy na skript z původního bloku kódu:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="e2fb6-136">Pokud se neshodují, aktualizujte *.html* souboru.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="e2fb6-137">V panelu nabídky vyberte **souboru** > **Uložit vše**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="e2fb6-138">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="e2fb6-138">Run the Sample</span></span>

1. <span data-ttu-id="e2fb6-139">Na panelu nástrojů, zapněte **ladění skriptů** a pak vyberte tlačítko Přehrát akci spustíte ukázku v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![Zadejte uživatelské jméno.](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="e2fb6-141">Pokud v prohlížeči se otevře, zadejte název pro svou identitu konverzace.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="e2fb6-142">Zkopírujte adresu URL z prohlížeče, otevřete dvou dalších prohlížečích a adresy URL vložte do řádku s adresou.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="e2fb6-143">V každé prohlížeče zadejte jedinečný název.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="e2fb6-144">Teď přidejte komentář a vyberte **odeslat**.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="e2fb6-145">Opakování, který v dalších prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="e2fb6-146">Komentáře se zobrazí v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fb6-147">Tento jednoduchý chatovací aplikaci nespravuje kontext diskuse na serveru.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="e2fb6-148">Centrum vysílá poznámky pro všechny aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="e2fb6-149">Uživatelé, kteří později připojit chat uvidí zprávy přidány od okamžiku, že se že připojí.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="e2fb6-150">Podívejte se jak chatovací aplikaci spustí ve třech různých prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="e2fb6-151">Při Tom Anand a Susan odesílat zprávy, všechny prohlížeče aktualizace v reálném čase:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![Všechny tři prohlížeče zobrazit historii stejné konverzace](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="e2fb6-153">V **Průzkumníka řešení**, zkontrolujte **dokumenty skriptu** uzel pro běžící aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="e2fb6-154">Existuje soubor skriptu s názvem *rozbočovače* generující knihovně SignalR v době běhu.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="e2fb6-155">Tento soubor skladuje komunikaci mezi jQuery skriptu a kódem na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![automaticky generované hubs skript v uzlu dokumenty skriptu](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="e2fb6-157">Prozkoumejte kód</span><span class="sxs-lookup"><span data-stu-id="e2fb6-157">Examine the Code</span></span>

<span data-ttu-id="e2fb6-158">Aplikace SignalRChat ukazuje dvě základní úlohy vývoj pro funkci SignalR.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="e2fb6-159">To ukazuje, jak vytvořit centrum.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-159">It shows you how to create a hub.</span></span> <span data-ttu-id="e2fb6-160">Server používá jako objekt hlavního koordinace daném rozbočovači.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="e2fb6-161">Centrum používá knihovny jQuery SignalR k odesílání a příjem zpráv.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="e2fb6-162">Rozbočovače SignalR v ChatHub.cs</span><span class="sxs-lookup"><span data-stu-id="e2fb6-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="e2fb6-163">V ukázkovém kódu výše `ChatHub` třída odvozena z `Microsoft.AspNet.SignalR.Hub` třídy.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="e2fb6-164">Odvozování z `Hub` třída je užitečný způsob, jak vytvořit aplikaci SignalR.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="e2fb6-165">Můžete vytvořit veřejné metody na třídě centra a potom použít tyto metody jejich voláním z skripty na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="e2fb6-166">V kódu, konverzace, klienti volání `ChatHub.Send` metoda odesílá nová zpráva.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="e2fb6-167">Centrum pak odešle zprávu pro všechny klienty voláním `Clients.All.broadcastMessage`.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="e2fb6-168">`Send` Metoda ukazuje několik konceptů hub:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="e2fb6-169">Deklarujte veřejné metody v rozbočovači, tak, aby klienti mohou volat.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="e2fb6-170">Použití `Microsoft.AspNet.SignalR.Hub.Clients` dynamických vlastností pro komunikaci se všemi klienty připojené pro toto centrum.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="e2fb6-171">Volání funkce na straně klienta (například `broadcastMessage` funkce) aktualizovat klienty.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="e2fb6-172">SignalR a jQuery v index.html</span><span class="sxs-lookup"><span data-stu-id="e2fb6-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="e2fb6-173">*Index.html* stránky ve vzorovém kódu ukazuje, jak používat knihovny jQuery SignalR pro komunikaci se rozbočovače SignalR.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="e2fb6-174">Kód provede celou řadu důležitých úloh.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-174">The code carries out many important tasks.</span></span> <span data-ttu-id="e2fb6-175">Deklaruje proxy server tak, aby odkazovaly rozbočovači, deklaruje funkci, že server může volat do předávaný obsah pro klienty a spustí připojení k odeslání zprávy do centra.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="e2fb6-176">V jazyce JavaScript odkaz na třídu serveru a jeho členy musí být camelCase.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="e2fb6-177">Odkazy na ukázkový kód C# *ChatHub* třídy v jazyce JavaScript jako `chatHub`.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="e2fb6-178">V tomto bloku kódu můžete vytvořit funkce zpětného volání ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="e2fb6-179">Třída rozbočovače na serveru volá tuto funkci tak, aby nabízel obsah aktualizací pro jednotlivé klienty.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="e2fb6-180">Dva řádky, že kódování HTML obsah před jeho zobrazení jsou volitelné a zobrazit vhodný způsob, jak brání injektáži skriptu.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="e2fb6-181">Tento kód otevře připojení v centru.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="e2fb6-182">Tento přístup zajišťuje, že kód naváže připojení před provedením obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="e2fb6-183">Kód spustí připojení a pak ji předá funkci pro zpracování události kliknutí na **odeslat** tlačítko na stránce HTML.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="e2fb6-184">Získat kód</span><span class="sxs-lookup"><span data-stu-id="e2fb6-184">Get the code</span></span>

[<span data-ttu-id="e2fb6-185">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="e2fb6-185">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="e2fb6-186">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="e2fb6-186">Additional resources</span></span>

<span data-ttu-id="e2fb6-187">Další informace o funkci SignalR naleznete v následujících zdrojích:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="e2fb6-188">Projekt SignalR</span><span class="sxs-lookup"><span data-stu-id="e2fb6-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="e2fb6-189">Funkce SignalR Githubu a ukázky</span><span class="sxs-lookup"><span data-stu-id="e2fb6-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="e2fb6-190">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="e2fb6-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="e2fb6-191">Další kroky</span><span class="sxs-lookup"><span data-stu-id="e2fb6-191">Next steps</span></span>

<span data-ttu-id="e2fb6-192">V tomto kurzu jste:</span><span class="sxs-lookup"><span data-stu-id="e2fb6-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2fb6-193">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="e2fb6-193">Set up the project</span></span>
> * <span data-ttu-id="e2fb6-194">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="e2fb6-194">Ran the sample</span></span>
> * <span data-ttu-id="e2fb6-195">Prozkoumat kód</span><span class="sxs-lookup"><span data-stu-id="e2fb6-195">Examined the code</span></span>

<span data-ttu-id="e2fb6-196">Přejděte k dalším článku se dozvíte, jak používat funkci SignalR a MVC 5.</span><span class="sxs-lookup"><span data-stu-id="e2fb6-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e2fb6-197">Knihovnou SignalR 2 a MVC 5</span><span class="sxs-lookup"><span data-stu-id="e2fb6-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)