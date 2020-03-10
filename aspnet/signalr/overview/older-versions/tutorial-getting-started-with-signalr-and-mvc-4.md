---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 'Kurz: Začínáme se signálem 1. x a MVC 4 | Microsoft Docs'
author: bradygaster
description: Pomocí ASP.NET signalizace a ASP.NET MVC 4 sestavte aplikaci Chat v reálném čase.
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579567"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="dd763-103">Kurz: Začínáme s knihovnou SignalR 1.x a MVC 4</span><span class="sxs-lookup"><span data-stu-id="dd763-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>

<span data-ttu-id="dd763-104">autor – [Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="dd763-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="dd763-105">V tomto kurzu se dozvíte, jak pomocí ASP.NET signalizace vytvořit aplikaci Chat v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="dd763-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="dd763-106">Přidáte signál do aplikace MVC 4 a vytvoříte zobrazení chatu pro odesílání a zobrazování zpráv.</span><span class="sxs-lookup"><span data-stu-id="dd763-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="dd763-107">Přehled</span><span class="sxs-lookup"><span data-stu-id="dd763-107">Overview</span></span>

<span data-ttu-id="dd763-108">V tomto kurzu se seznámíte s vývojem webových aplikací v reálném čase pomocí ASP.NET signalizace a ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="dd763-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="dd763-109">Kurz používá stejný kód aplikace chatu jako [Začínáme kurz pro signalizaci](tutorial-getting-started-with-signalr.md), ale ukazuje, jak ho přidat do aplikace MVC 4 založené na šabloně Internet.</span><span class="sxs-lookup"><span data-stu-id="dd763-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="dd763-110">V tomto tématu se seznámíte s následujícími vývojovými úkoly signalizace:</span><span class="sxs-lookup"><span data-stu-id="dd763-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="dd763-111">Přidání knihovny signalizace do aplikace MVC 4.</span><span class="sxs-lookup"><span data-stu-id="dd763-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="dd763-112">Vytvoření třídy centra pro nabízení obsahu klientům.</span><span class="sxs-lookup"><span data-stu-id="dd763-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="dd763-113">Posílání zpráv a zobrazování aktualizací z centra pomocí knihovny jQuery v nástroji Signald na webové stránce</span><span class="sxs-lookup"><span data-stu-id="dd763-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="dd763-114">Následující snímek obrazovky ukazuje dokončenou aplikaci Chat spuštěnou v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="dd763-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![Instance chatu](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="dd763-116">Řezů</span><span class="sxs-lookup"><span data-stu-id="dd763-116">Sections:</span></span>

- [<span data-ttu-id="dd763-117">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="dd763-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="dd763-118">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="dd763-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="dd763-119">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="dd763-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="dd763-120">Další kroky</span><span class="sxs-lookup"><span data-stu-id="dd763-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="dd763-121">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="dd763-121">Set up the Project</span></span>

<span data-ttu-id="dd763-122">Požadavky:</span><span class="sxs-lookup"><span data-stu-id="dd763-122">Prerequisites:</span></span>

- <span data-ttu-id="dd763-123">Visual Studio 2010 SP1, Visual Studio 2012 nebo Visual Studio 2012 Express.</span><span class="sxs-lookup"><span data-stu-id="dd763-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="dd763-124">Pokud nemáte Visual Studio, přečtěte si článek [ASP.NET downloads](https://www.asp.net/downloads) , kde získáte bezplatný vývojářský nástroj sady Visual Studio 2012 Express.</span><span class="sxs-lookup"><span data-stu-id="dd763-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="dd763-125">V případě sady Visual Studio 2010 nainstalujte [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span><span class="sxs-lookup"><span data-stu-id="dd763-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="dd763-126">V této části se dozvíte, jak vytvořit aplikaci ASP.NET MVC 4, přidat knihovnu signálů a vytvořit aplikaci Chat.</span><span class="sxs-lookup"><span data-stu-id="dd763-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="dd763-127">V aplikaci Visual Studio vytvořte aplikaci ASP.NET MVC 4, pojmenujte ji SignalRChat a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="dd763-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="dd763-128">V VS 2010 vyberte v ovládacím prvku rozevíracího seznamu verze rozhraní **.NET Framework 4** .</span><span class="sxs-lookup"><span data-stu-id="dd763-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="dd763-129">Kód signalizace běží na .NET Framework verzích 4 a 4,5.</span><span class="sxs-lookup"><span data-stu-id="dd763-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![Vytvořit web MVC](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="dd763-131">Vyberte šablonu internetové aplikace, zrušte zaškrtnutí políčka pro **Vytvoření projektu testu jednotek**a klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="dd763-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![Vytvořit internetový web MVC](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="dd763-133">Otevřete **nástroje > správce balíčků NuGet > konzole správce balíčků** a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="dd763-133">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="dd763-134">Tento krok přidá do projektu sadu souborů skriptu a odkazy na sestavení, které umožňují funkci signalizace.</span><span class="sxs-lookup"><span data-stu-id="dd763-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="dd763-135">V **Průzkumník řešení** rozbalte složku skripty.</span><span class="sxs-lookup"><span data-stu-id="dd763-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="dd763-136">Všimněte si, že knihovny skriptů pro signalizaci byly přidány do projektu.</span><span class="sxs-lookup"><span data-stu-id="dd763-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![Odkazy knihovny](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="dd763-138">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt, vyberte **Přidat | Novou složku**a přidejte novou složku s názvem **centra**.</span><span class="sxs-lookup"><span data-stu-id="dd763-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="dd763-139">Klikněte pravým tlačítkem na složku **Centers** , klikněte na **Přidat | Třídu**a vytvořte novou C# třídu s názvem **ChatHub.cs**.</span><span class="sxs-lookup"><span data-stu-id="dd763-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="dd763-140">Tuto třídu použijete jako rozbočovač serveru signalizace, který odesílá zprávy všem klientům.</span><span class="sxs-lookup"><span data-stu-id="dd763-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="dd763-141">Pokud používáte Visual Studio 2012 a máte nainstalovanou [aktualizaci ASP.NET and Web Tools 2012,2](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), můžete k vytvoření třídy centra použít novou šablonu položky signaler.</span><span class="sxs-lookup"><span data-stu-id="dd763-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="dd763-142">Provedete to tak, že kliknete pravým tlačítkem na složku **Centers** , kliknete na **Přidat | Nová položka**, vyberte **Třída centra signalizace (V1)** a pojmenujte třídu **ChatHub.cs**.</span><span class="sxs-lookup"><span data-stu-id="dd763-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>

1. <span data-ttu-id="dd763-143">Nahraďte kód ve třídě **ChatHub** následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="dd763-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="dd763-144">Otevřete soubor **Global. asax** pro projekt a přidejte volání metody `RouteTable.Routes.MapHubs();` jako první řádek kódu v metodě `Application_Start`.</span><span class="sxs-lookup"><span data-stu-id="dd763-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="dd763-145">Tento kód zaregistruje výchozí trasu pro centra signálů a musí se volat před registrací jakýchkoli jiných tras.</span><span class="sxs-lookup"><span data-stu-id="dd763-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="dd763-146">Metoda Completed `Application_Start` vypadá jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="dd763-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="dd763-147">Upravte třídu `HomeController` nalezenou v **Controllers/HomeController. cs** a přidejte následující metodu do třídy.</span><span class="sxs-lookup"><span data-stu-id="dd763-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="dd763-148">Tato metoda vrátí zobrazení **chatu** , které budete vytvářet v pozdějším kroku.</span><span class="sxs-lookup"><span data-stu-id="dd763-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="dd763-149">Klikněte pravým tlačítkem na právě vytvořenou metodu `Chat` a kliknutím na tlačítko **Přidat zobrazení** vytvořte nový soubor zobrazení.</span><span class="sxs-lookup"><span data-stu-id="dd763-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="dd763-150">V dialogovém okně **Přidat zobrazení** zaškrtněte políčko pro **použití rozložení nebo stránky předlohy** (zrušte zaškrtnutí těchto políček) a pak klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="dd763-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![Přidání zobrazení](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="dd763-152">Upravte nový soubor zobrazení s názvem **chat. cshtml**.</span><span class="sxs-lookup"><span data-stu-id="dd763-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="dd763-153">Po značce &lt;H2&gt; vložte následující oddíl &lt;div&gt; a `@section scripts` blok kódu na stránku.</span><span class="sxs-lookup"><span data-stu-id="dd763-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="dd763-154">Tento skript umožňuje stránce odesílat zprávy chatu a zobrazovat zprávy ze serveru.</span><span class="sxs-lookup"><span data-stu-id="dd763-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="dd763-155">V následujícím bloku kódu se zobrazí úplný kód pro zobrazení chatu.</span><span class="sxs-lookup"><span data-stu-id="dd763-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="dd763-156">Když přidáte do projektu sady Visual Studio signál a další knihovny skriptu, správce balíčků může nainstalovat verze skriptů, které jsou novější než verze uvedené v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="dd763-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="dd763-157">Ujistěte se, že odkazy skriptu v kódu odpovídají verzím knihoven skriptů nainstalovaných ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="dd763-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="dd763-158">**Uložit vše** pro projekt.</span><span class="sxs-lookup"><span data-stu-id="dd763-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="dd763-159">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="dd763-159">Run the Sample</span></span>

1. <span data-ttu-id="dd763-160">Stisknutím klávesy F5 spusťte projekt v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="dd763-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="dd763-161">Na řádku Adresa prohlížeče přidejte **/Home/chat** k adrese URL výchozí stránky projektu.</span><span class="sxs-lookup"><span data-stu-id="dd763-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="dd763-162">Stránka konverzace se načte do instance prohlížeče a zobrazí výzvu k zadání uživatelského jména.</span><span class="sxs-lookup"><span data-stu-id="dd763-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="dd763-164">Zadejte jméno uživatele.</span><span class="sxs-lookup"><span data-stu-id="dd763-164">Enter a user name.</span></span>
4. <span data-ttu-id="dd763-165">Zkopírujte adresu URL z adresního řádku prohlížeče a použijte ji k otevření dvou dalších instancí prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="dd763-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="dd763-166">V každé instanci prohlížeče zadejte jedinečné uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="dd763-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="dd763-167">V každé instanci prohlížeče přidejte komentář a klikněte na **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="dd763-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="dd763-168">Komentáře by se měly zobrazit ve všech instancích prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="dd763-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd763-169">Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru.</span><span class="sxs-lookup"><span data-stu-id="dd763-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="dd763-170">Centrum vysílá komentáře všem aktuálním uživatelům.</span><span class="sxs-lookup"><span data-stu-id="dd763-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="dd763-171">Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.</span><span class="sxs-lookup"><span data-stu-id="dd763-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="dd763-172">Následující snímek obrazovky ukazuje aplikaci Chat spuštěnou v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="dd763-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![Prohlížeče chatu](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="dd763-174">V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="dd763-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="dd763-175">Tento uzel je viditelný v režimu ladění, pokud používáte Internet Explorer jako prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="dd763-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="dd763-176">Existuje soubor skriptu **s názvem hub** , který knihovna signálů dynamicky generuje za běhu.</span><span class="sxs-lookup"><span data-stu-id="dd763-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="dd763-177">Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="dd763-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="dd763-178">Pokud používáte jiný prohlížeč než Internet Explorer, můžete k souboru dynamického **centra** přistupovat také tak, že na něj přejdete přímo, například http://mywebsite/signalr/hubs.</span><span class="sxs-lookup"><span data-stu-id="dd763-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![Generovaný skript centra](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="dd763-180">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="dd763-180">Examine the Code</span></span>

<span data-ttu-id="dd763-181">Chatovací aplikace pro signály znázorňuje dva základní úlohy vývoje signálu: vytváření rozbočovače jako hlavního objektu koordinace na serveru a použití knihovny jQuery nástroje Signal k posílání a přijímání zpráv.</span><span class="sxs-lookup"><span data-stu-id="dd763-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="dd763-182">Rozbočovače signálu</span><span class="sxs-lookup"><span data-stu-id="dd763-182">SignalR Hubs</span></span>

<span data-ttu-id="dd763-183">V ukázce kódu je třída **ChatHub** odvozena od třídy **Microsoft. ASPNET. signaler. hub** .</span><span class="sxs-lookup"><span data-stu-id="dd763-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="dd763-184">Odvození od třídy **centra** je užitečný způsob, jak vytvořit aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="dd763-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="dd763-185">Veřejné metody můžete vytvořit na třídě centra a potom k těmto metodám přistupovat voláním ze skriptů jQuery na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="dd763-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="dd763-186">V kódu chatu klienti volají metodu **ChatHub. Send** k odeslání nové zprávy.</span><span class="sxs-lookup"><span data-stu-id="dd763-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="dd763-187">Centrum pak pošle zprávu všem klientům voláním **clients. All. addNewMessageToPage**.</span><span class="sxs-lookup"><span data-stu-id="dd763-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="dd763-188">Metoda **Send** ukazuje několik konceptů centra:</span><span class="sxs-lookup"><span data-stu-id="dd763-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="dd763-189">Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.</span><span class="sxs-lookup"><span data-stu-id="dd763-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="dd763-190">Pro přístup ke všem klientům připojeným k tomuto centru použijte vlastnost **Microsoft. ASPNET. signaler. hub. clients** .</span><span class="sxs-lookup"><span data-stu-id="dd763-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="dd763-191">Chcete-li aktualizovat klienty, zavolejte na klienta funkci jQuery (například funkci `addNewMessageToPage`).</span><span class="sxs-lookup"><span data-stu-id="dd763-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="dd763-192">Signál a jQuery</span><span class="sxs-lookup"><span data-stu-id="dd763-192">SignalR and jQuery</span></span>

<span data-ttu-id="dd763-193">Soubor zobrazení **chat. cshtml** v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace.</span><span class="sxs-lookup"><span data-stu-id="dd763-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="dd763-194">Zásadní úlohy v kódu vytvářejí odkaz na automaticky generovaný proxy server pro centrum a deklaruje funkci, kterou může server volat, aby zavolal obsah do klientů, a spustí připojení pro posílání zpráv do centra.</span><span class="sxs-lookup"><span data-stu-id="dd763-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="dd763-195">Následující kód deklaruje proxy server pro rozbočovač.</span><span class="sxs-lookup"><span data-stu-id="dd763-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="dd763-196">V jQuery je odkaz na třídu serveru a jeho členy v případě ve stylu CamelCase.</span><span class="sxs-lookup"><span data-stu-id="dd763-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="dd763-197">Ukázka kódu odkazuje na C# třídu **ChatHub** ve jQuery jako **ChatHub**.</span><span class="sxs-lookup"><span data-stu-id="dd763-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="dd763-198">Pokud chcete odkazovat na třídu `ChatHub` v jQuery pomocí konvenčních malých písmen Pascal, jako byste měli C#v, upravte soubor třídy ChatHub.cs.</span><span class="sxs-lookup"><span data-stu-id="dd763-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="dd763-199">Přidejte příkaz `using`, který odkazuje na obor názvů `Microsoft.AspNet.SignalR.Hubs`.</span><span class="sxs-lookup"><span data-stu-id="dd763-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="dd763-200">Pak přidejte atribut `HubName` do třídy `ChatHub`, například `[HubName("ChatHub")]`.</span><span class="sxs-lookup"><span data-stu-id="dd763-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="dd763-201">Nakonec aktualizujte svůj odkaz jQuery na třídu `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="dd763-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>

<span data-ttu-id="dd763-202">Následující kód ukazuje, jak vytvořit funkci zpětného volání ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="dd763-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="dd763-203">Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi.</span><span class="sxs-lookup"><span data-stu-id="dd763-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="dd763-204">Volitelné volání funkce `htmlEncode` ukazuje způsob, jak HTML kódovat obsah zprávy před jeho zobrazením na stránce, jako způsob, jak zabránit vkládání skriptu.</span><span class="sxs-lookup"><span data-stu-id="dd763-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="dd763-205">Následující kód ukazuje, jak otevřít připojení pomocí centra.</span><span class="sxs-lookup"><span data-stu-id="dd763-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="dd763-206">Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce konverzace.</span><span class="sxs-lookup"><span data-stu-id="dd763-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="dd763-207">Tento přístup zajišťuje, aby bylo připojení vytvořeno před spuštěním obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="dd763-207">This approach ensures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="dd763-208">Další kroky</span><span class="sxs-lookup"><span data-stu-id="dd763-208">Next Steps</span></span>

<span data-ttu-id="dd763-209">Naučili jste se, že Signal je architektura pro vytváření webových aplikací v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="dd763-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="dd763-210">Zjistili jste také několik úloh vývoje signálů: Přidání signálu do aplikace ASP.NET, vytvoření třídy centra a odeslání a přijetí zpráv z centra.</span><span class="sxs-lookup"><span data-stu-id="dd763-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="dd763-211">Další informace o pokročilých konceptech pro vývoj signalizace najdete na následujících webech, na kterých se nachází zdrojový kód a zdroje signálů:</span><span class="sxs-lookup"><span data-stu-id="dd763-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="dd763-212">Projekt signálu</span><span class="sxs-lookup"><span data-stu-id="dd763-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="dd763-213">GitHub a ukázky signálů</span><span class="sxs-lookup"><span data-stu-id="dd763-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="dd763-214">Wiki signálu</span><span class="sxs-lookup"><span data-stu-id="dd763-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
