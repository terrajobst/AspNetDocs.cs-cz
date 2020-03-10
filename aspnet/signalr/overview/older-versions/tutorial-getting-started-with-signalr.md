---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 'Kurz: Začínáme se signálem 1. x | Microsoft Docs'
author: bradygaster
description: Použijte signál ASP.NET k vytvoření aplikace chat v reálném čase na stránce HTML.
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623541"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="aa56f-103">Kurz: Začínáme s knihovnou SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="aa56f-103">Tutorial: Getting Started with SignalR 1.x</span></span>

<span data-ttu-id="aa56f-104">autor – [Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="aa56f-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="aa56f-105">V tomto kurzu se naučíte používat funkci SignalR k vytvoření aplikace pro chatování v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="aa56f-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="aa56f-106">Přidáte signál do prázdné webové aplikace v ASP.NET a vytvoříte stránku HTML pro odesílání a zobrazování zpráv.</span><span class="sxs-lookup"><span data-stu-id="aa56f-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="aa56f-107">Přehled</span><span class="sxs-lookup"><span data-stu-id="aa56f-107">Overview</span></span>

<span data-ttu-id="aa56f-108">V tomto kurzu se seznámíte s vývojem signalizace tím, že se dozvíte, jak vytvořit jednoduchou chatovací aplikaci založenou na prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="aa56f-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="aa56f-109">Přidáte knihovnu signálů do prázdné webové aplikace v ASP.NET, vytvoříte třídu centra pro posílání zpráv klientům a vytvoříte stránku HTML, která umožní uživatelům odesílat a přijímat zprávy chatu.</span><span class="sxs-lookup"><span data-stu-id="aa56f-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="aa56f-110">Podobný kurz, který ukazuje, jak vytvořit aplikaci chatu v MVC 4 pomocí zobrazení MVC, najdete v tématu [Začínáme s nástrojem Signal and MVC 4](index.md).</span><span class="sxs-lookup"><span data-stu-id="aa56f-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aa56f-111">V tomto kurzu se používá verze nástroje Signal (verze 1. x).</span><span class="sxs-lookup"><span data-stu-id="aa56f-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="aa56f-112">Podrobnosti o změnách mezi signálem 1. x a 2,0 naleznete v tématu Upgrade pro předaných [projektů s návěstí 1. x](../releases/upgrading-signalr-1x-projects-to-20.md).</span><span class="sxs-lookup"><span data-stu-id="aa56f-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="aa56f-113">Signal je open source knihovna .NET pro vytváření webových aplikací, které vyžadují živé interakce uživatelů nebo aktualizace dat v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="aa56f-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="aa56f-114">Mezi příklady patří sociální aplikace, hry pro víc uživatelů, obchodní spolupráce a novinky, počasí nebo aplikace pro finanční aktualizace.</span><span class="sxs-lookup"><span data-stu-id="aa56f-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="aa56f-115">Ty se často nazývají aplikace v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="aa56f-115">These are often called real-time applications.</span></span>

<span data-ttu-id="aa56f-116">Návěstí zjednodušuje proces vytváření aplikací v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="aa56f-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="aa56f-117">Obsahuje knihovnu serveru ASP.NET a klientskou knihovnu JavaScriptu, která usnadňuje správu připojení klient-server a nabízených aktualizací obsahu klientům.</span><span class="sxs-lookup"><span data-stu-id="aa56f-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="aa56f-118">Knihovnu signálů můžete přidat do existující aplikace ASP.NET, abyste získali funkce v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="aa56f-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="aa56f-119">V tomto kurzu se dozvíte o následujících úkolech pro vývoj signálů:</span><span class="sxs-lookup"><span data-stu-id="aa56f-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="aa56f-120">Přidání knihovny signalizace do webové aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa56f-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="aa56f-121">Vytvoření třídy centra pro nabízení obsahu klientům.</span><span class="sxs-lookup"><span data-stu-id="aa56f-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="aa56f-122">Posílání zpráv a zobrazování aktualizací z centra pomocí knihovny jQuery v nástroji Signald na webové stránce</span><span class="sxs-lookup"><span data-stu-id="aa56f-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="aa56f-123">Následující snímek obrazovky ukazuje aplikaci Chat spuštěnou v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="aa56f-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="aa56f-124">Každý nový uživatel může publikovat komentáře a zobrazit komentáře přidané poté, co se uživatel připojí k chatu.</span><span class="sxs-lookup"><span data-stu-id="aa56f-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![Instance chatu](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="aa56f-126">Řezů</span><span class="sxs-lookup"><span data-stu-id="aa56f-126">Sections:</span></span>

- [<span data-ttu-id="aa56f-127">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="aa56f-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="aa56f-128">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="aa56f-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="aa56f-129">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="aa56f-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="aa56f-130">Další kroky</span><span class="sxs-lookup"><span data-stu-id="aa56f-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="aa56f-131">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="aa56f-131">Set up the Project</span></span>

<span data-ttu-id="aa56f-132">V této části se dozvíte, jak vytvořit prázdnou webovou aplikaci v ASP.NET, přidat signál a vytvořit aplikaci Chat.</span><span class="sxs-lookup"><span data-stu-id="aa56f-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="aa56f-133">Požadavky:</span><span class="sxs-lookup"><span data-stu-id="aa56f-133">Prerequisites:</span></span>

- <span data-ttu-id="aa56f-134">Visual Studio 2010 SP1 nebo 2012.</span><span class="sxs-lookup"><span data-stu-id="aa56f-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="aa56f-135">Pokud nemáte Visual Studio, přečtěte si článek [ASP.NET downloads](https://www.asp.net/downloads) , kde získáte bezplatný vývojářský nástroj sady Visual Studio 2012 Express.</span><span class="sxs-lookup"><span data-stu-id="aa56f-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="aa56f-136">[Microsoft ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=279941).</span><span class="sxs-lookup"><span data-stu-id="aa56f-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="aa56f-137">V případě sady Visual Studio 2012 tento instalační program přidá do sady Visual Studio nové funkce ASP.NET včetně šablon signálů.</span><span class="sxs-lookup"><span data-stu-id="aa56f-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="aa56f-138">V případě sady Visual Studio 2010 SP1 není instalační služba k dispozici, ale tento kurz můžete dokončit instalací balíčku NuGet pro signalizaci, jak je popsáno v krocích pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="aa56f-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="aa56f-139">Následující kroky používají Visual Studio 2012 k vytvoření prázdné webové aplikace ASP.NET a přidání knihovny signalizace:</span><span class="sxs-lookup"><span data-stu-id="aa56f-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="aa56f-140">V aplikaci Visual Studio vytvořte prázdnou webovou aplikaci v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa56f-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![Vytvořit prázdný web](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="aa56f-142">Otevřete **konzolu Správce balíčků** tak, že vyberete **nástroje | Správce balíčků NuGet | Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-142">Open the **Package Manager Console** by selecting **Tools | NuGet Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="aa56f-143">Do okna konzoly zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="aa56f-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="aa56f-144">Tento příkaz nainstaluje nejnovější verzi signalizace 1. x.</span><span class="sxs-lookup"><span data-stu-id="aa56f-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="aa56f-145">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt, vyberte **Přidat | Třída**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="aa56f-146">Pojmenujte novou třídu **ChatHub**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="aa56f-147">V **Průzkumník řešení** rozbalte uzel skripty.</span><span class="sxs-lookup"><span data-stu-id="aa56f-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="aa56f-148">Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.</span><span class="sxs-lookup"><span data-stu-id="aa56f-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![Odkazy knihovny](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="aa56f-150">Nahraďte kód ve třídě **ChatHub** následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="aa56f-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="aa56f-151">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a pak klikněte na **Přidat | Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="aa56f-152">V dialogovém okně **Přidat novou položku** vyberte možnost **globální třída aplikace** a klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![Přidat globální](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="aa56f-154">Po poskytnuté příkazy `using` ve třídě Global.asax.cs přidejte následující příkazy `using`.</span><span class="sxs-lookup"><span data-stu-id="aa56f-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="aa56f-155">Přidejte následující řádek kódu do metody `Application_Start` globální třídy k registraci výchozí trasy pro centra signálu.</span><span class="sxs-lookup"><span data-stu-id="aa56f-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="aa56f-156">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a pak klikněte na **Přidat | Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="aa56f-157">V dialogovém okně **Přidat novou položku** vyberte možnost stránka HTML a klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="aa56f-158">V **Průzkumník řešení**klikněte pravým tlačítkem na právě vytvořenou stránku HTML a pak klikněte na **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="aa56f-159">Nahraďte výchozí kód na stránce HTML následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="aa56f-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="aa56f-160">**Uložit vše** pro projekt.</span><span class="sxs-lookup"><span data-stu-id="aa56f-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="aa56f-161">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="aa56f-161">Run the Sample</span></span>

1. <span data-ttu-id="aa56f-162">Stisknutím klávesy F5 spusťte projekt v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="aa56f-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="aa56f-163">Stránka HTML se načte do instance prohlížeče a zobrazí výzvu k zadání uživatelského jména.</span><span class="sxs-lookup"><span data-stu-id="aa56f-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="aa56f-165">Zadejte jméno uživatele.</span><span class="sxs-lookup"><span data-stu-id="aa56f-165">Enter a user name.</span></span>
3. <span data-ttu-id="aa56f-166">Zkopírujte adresu URL z adresního řádku prohlížeče a použijte ji k otevření dvou dalších instancí prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="aa56f-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="aa56f-167">V každé instanci prohlížeče zadejte jedinečné uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="aa56f-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="aa56f-168">V každé instanci prohlížeče přidejte komentář a klikněte na **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="aa56f-169">Komentáře by se měly zobrazit ve všech instancích prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="aa56f-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa56f-170">Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru.</span><span class="sxs-lookup"><span data-stu-id="aa56f-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="aa56f-171">Centrum vysílá komentáře všem aktuálním uživatelům.</span><span class="sxs-lookup"><span data-stu-id="aa56f-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="aa56f-172">Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.</span><span class="sxs-lookup"><span data-stu-id="aa56f-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="aa56f-173">Následující snímek obrazovky ukazuje aplikaci Chat spuštěnou ve třech instancích prohlížeče, všechny, které jsou aktualizovány, když jedna instance pošle zprávu:</span><span class="sxs-lookup"><span data-stu-id="aa56f-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![Prohlížeče chatu](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="aa56f-175">V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="aa56f-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="aa56f-176">Existuje soubor skriptu **s názvem hub** , který knihovna signálů dynamicky generuje za běhu.</span><span class="sxs-lookup"><span data-stu-id="aa56f-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="aa56f-177">Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="aa56f-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![Generovaný skript centra](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="aa56f-179">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="aa56f-179">Examine the Code</span></span>

<span data-ttu-id="aa56f-180">Chatovací aplikace pro signály znázorňuje dva základní úlohy vývoje signálu: vytváření rozbočovače jako hlavního objektu koordinace na serveru a použití knihovny jQuery nástroje Signal k posílání a přijímání zpráv.</span><span class="sxs-lookup"><span data-stu-id="aa56f-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="aa56f-181">Rozbočovače signálu</span><span class="sxs-lookup"><span data-stu-id="aa56f-181">SignalR Hubs</span></span>

<span data-ttu-id="aa56f-182">V ukázce kódu je třída **ChatHub** odvozena od třídy **Microsoft. ASPNET. signaler. hub** .</span><span class="sxs-lookup"><span data-stu-id="aa56f-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="aa56f-183">Odvození od třídy **centra** je užitečný způsob, jak vytvořit aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="aa56f-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="aa56f-184">Veřejné metody můžete vytvořit na třídě centra a potom k těmto metodám přistupovat voláním ze skriptů jQuery na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="aa56f-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="aa56f-185">V kódu chatu klienti volají metodu **ChatHub. Send** k odeslání nové zprávy.</span><span class="sxs-lookup"><span data-stu-id="aa56f-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="aa56f-186">Centrum pak pošle zprávu všem klientům voláním **clients. All. broadcastMessage**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="aa56f-187">Metoda **Send** ukazuje několik konceptů centra:</span><span class="sxs-lookup"><span data-stu-id="aa56f-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="aa56f-188">Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.</span><span class="sxs-lookup"><span data-stu-id="aa56f-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="aa56f-189">K přístupu ke všem klientům připojeným k tomuto centru použijte dynamickou vlastnost **Microsoft. ASPNET. signaler. hub. clients** .</span><span class="sxs-lookup"><span data-stu-id="aa56f-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="aa56f-190">Chcete-li aktualizovat klienty, zavolejte na klienta funkci jQuery (například funkci `broadcastMessage`).</span><span class="sxs-lookup"><span data-stu-id="aa56f-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="aa56f-191">Signál a jQuery</span><span class="sxs-lookup"><span data-stu-id="aa56f-191">SignalR and jQuery</span></span>

<span data-ttu-id="aa56f-192">Stránka HTML v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace.</span><span class="sxs-lookup"><span data-stu-id="aa56f-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="aa56f-193">Základní úlohy v kódu deklaruje proxy server pro odkazování na centrum a deklaraci funkce, kterou může server volat, aby zavolal obsah do klientů a spouštěl připojení pro odesílání zpráv do centra.</span><span class="sxs-lookup"><span data-stu-id="aa56f-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="aa56f-194">Následující kód deklaruje proxy server pro rozbočovač.</span><span class="sxs-lookup"><span data-stu-id="aa56f-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="aa56f-195">V jQuery je odkaz na třídu serveru a jeho členy v případě ve stylu CamelCase.</span><span class="sxs-lookup"><span data-stu-id="aa56f-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="aa56f-196">Ukázka kódu odkazuje na C# třídu **ChatHub** ve jQuery jako **ChatHub**.</span><span class="sxs-lookup"><span data-stu-id="aa56f-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>

<span data-ttu-id="aa56f-197">Následující kód je způsob, jak ve skriptu vytvořit funkci zpětného volání.</span><span class="sxs-lookup"><span data-stu-id="aa56f-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="aa56f-198">Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi.</span><span class="sxs-lookup"><span data-stu-id="aa56f-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="aa56f-199">Dva řádky, které obsah HTML zakóduje před jeho zobrazením, jsou volitelné a zobrazují jednoduchý způsob, jak zabránit vkládání skriptu.</span><span class="sxs-lookup"><span data-stu-id="aa56f-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="aa56f-200">Následující kód ukazuje, jak otevřít připojení pomocí centra.</span><span class="sxs-lookup"><span data-stu-id="aa56f-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="aa56f-201">Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce HTML.</span><span class="sxs-lookup"><span data-stu-id="aa56f-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="aa56f-202">Tento přístup si zajistěte, aby bylo připojení navázáno, než se spustí obslužná rutina události.</span><span class="sxs-lookup"><span data-stu-id="aa56f-202">This approach insures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="aa56f-203">Další kroky</span><span class="sxs-lookup"><span data-stu-id="aa56f-203">Next Steps</span></span>

<span data-ttu-id="aa56f-204">Naučili jste se, že Signal je architektura pro vytváření webových aplikací v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="aa56f-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="aa56f-205">Zjistili jste také několik úloh vývoje signálů: Přidání signálu do aplikace ASP.NET, vytvoření třídy centra a odeslání a přijetí zpráv z centra.</span><span class="sxs-lookup"><span data-stu-id="aa56f-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="aa56f-206">Ukázkovou aplikaci můžete vytvořit v tomto kurzu nebo v jiných aplikacích, které jsou k dispozici prostřednictvím Internetu, jejich nasazením pro poskytovatele hostingu.</span><span class="sxs-lookup"><span data-stu-id="aa56f-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="aa56f-207">Microsoft nabízí bezplatné webové hostování až pro 10 webů na bezplatném [zkušebním účtu Windows Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="aa56f-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="aa56f-208">Návod, jak nasadit ukázkovou aplikaci pro signalizaci, najdete v tématu [publikování ukázky Začínáme jako webu Windows Azure](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa56f-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="aa56f-209">Podrobné informace o tom, jak nasadit webový projekt aplikace Visual Studio na web Windows Azure, najdete v tématu [nasazení aplikace ASP.NET na web Windows Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span><span class="sxs-lookup"><span data-stu-id="aa56f-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="aa56f-210">(Poznámka: přenos pomocí protokolu WebSocket není v současné době pro weby Windows Azure podporován.</span><span class="sxs-lookup"><span data-stu-id="aa56f-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="aa56f-211">Pokud není přenos pomocí protokolu WebSocket k dispozici, používá signál další dostupné přenosy, jak je popsáno v části přenosy v [tématu Úvod do signalizace](index.md).)</span><span class="sxs-lookup"><span data-stu-id="aa56f-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="aa56f-212">Další informace o pokročilých konceptech pro vývoj signalizace najdete na následujících webech, na kterých se nachází zdrojový kód a zdroje signálů:</span><span class="sxs-lookup"><span data-stu-id="aa56f-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="aa56f-213">Projekt signálu</span><span class="sxs-lookup"><span data-stu-id="aa56f-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="aa56f-214">GitHub a ukázky signálů</span><span class="sxs-lookup"><span data-stu-id="aa56f-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="aa56f-215">Wiki signálu</span><span class="sxs-lookup"><span data-stu-id="aa56f-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
