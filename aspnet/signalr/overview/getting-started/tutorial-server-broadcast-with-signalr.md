---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Kurz: všesměrové vysílání serveru pomocí návěstí 2 | Microsoft Docs'
author: tdykstra
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET Signal 2 k poskytování funkcí všesměrového vysílání serveru.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536601"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="9ae1b-103">Kurz: všesměrové vysílání serveru pomocí Signaler 2</span><span class="sxs-lookup"><span data-stu-id="9ae1b-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="9ae1b-104">V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET Signal 2 k poskytování funkcí všesměrového vysílání serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="9ae1b-105">Všesměrové vysílání serveru znamená, že server spouští komunikaci odesílaná klientům.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="9ae1b-106">Aplikace, kterou vytvoříte v tomto kurzu, simuluje burzovní, což je typický scénář pro funkce všesměrového vysílání serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="9ae1b-107">Server pravidelně aktualizuje skladové ceny a vysílá aktualizace všem připojeným klientům.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="9ae1b-108">V prohlížeči se čísla a symboly ve sloupcích **změnit** a **%** dynamicky mění v reakci na oznámení ze serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="9ae1b-109">Pokud otevřete další prohlížeče na stejné adrese URL, všechny zobrazí stejná data a stejné změny dat současně.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Vytvoření webu](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="9ae1b-111">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ae1b-112">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-112">Create the project</span></span>
> * <span data-ttu-id="9ae1b-113">Nastavení serverového kódu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-113">Set up the server code</span></span>
> * <span data-ttu-id="9ae1b-114">Kontrola kódu serveru</span><span class="sxs-lookup"><span data-stu-id="9ae1b-114">Examine the server code</span></span>
> * <span data-ttu-id="9ae1b-115">Nastavení kódu klienta</span><span class="sxs-lookup"><span data-stu-id="9ae1b-115">Set up the client code</span></span>
> * <span data-ttu-id="9ae1b-116">Projděte si kód klienta.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-116">Examine the client code</span></span>
> * <span data-ttu-id="9ae1b-117">Testování aplikace</span><span class="sxs-lookup"><span data-stu-id="9ae1b-117">Test the application</span></span>
> * <span data-ttu-id="9ae1b-118">Povolte protokolování</span><span class="sxs-lookup"><span data-stu-id="9ae1b-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ae1b-119">Pokud nechcete s postupem sestavování aplikace pracovat, můžete do nového prázdného projektu webové aplikace ASP.NET nainstalovat Signal. ukázkový balíček.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="9ae1b-120">Pokud nainstalujete balíček NuGet bez provedení kroků v tomto kurzu, musíte postupovat podle pokynů v souboru *Readme. txt* .</span><span class="sxs-lookup"><span data-stu-id="9ae1b-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="9ae1b-121">Chcete-li spustit balíček, je třeba přidat třídu pro spuštění OWIN, která volá metodu `ConfigureSignalR` v nainstalovaném balíčku.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="9ae1b-122">Pokud nepřidáte třídu Startup OWIN, zobrazí se chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="9ae1b-123">Viz část [instalace ukázky StockTicker](#install-the-stockticker-sample) tohoto článku.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ae1b-124">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="9ae1b-124">Prerequisites</span></span>

* <span data-ttu-id="9ae1b-125">Sada [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) se sadou funkcí **Vývoj pro ASP.NET a web**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="9ae1b-126">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-126">Create the project</span></span>

<span data-ttu-id="9ae1b-127">V této části se dozvíte, jak použít Visual Studio 2017 k vytvoření prázdné webové aplikace v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="9ae1b-128">V aplikaci Visual Studio vytvořte webovou aplikaci v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Vytvoření webu](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="9ae1b-130">V okně **Nová webová aplikace v ASP.NET – signaler. StockTicker** ponechte vybrané **prázdné** a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="9ae1b-131">Nastavení serverového kódu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-131">Set up the server code</span></span>

<span data-ttu-id="9ae1b-132">V této části nastavíte kód, který běží na serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="9ae1b-133">Vytvoření třídy akcie</span><span class="sxs-lookup"><span data-stu-id="9ae1b-133">Create the Stock class</span></span>

<span data-ttu-id="9ae1b-134">Začnete vytvořením třídy *burzovního* modelu, kterou použijete k ukládání a přenosu informací o zásobách.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="9ae1b-135">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **třídu**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="9ae1b-136">Pojmenujte třídu *Stock* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="9ae1b-137">Nahraďte kód v souboru *Stock.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="9ae1b-138">Dvě vlastnosti, které nastavíte při vytváření akcií, jsou `Symbol` (například MSFT pro Microsoft) a `Price`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="9ae1b-139">Ostatní vlastnosti závisí na tom, jak a kdy jste nastavili `Price`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="9ae1b-140">Při prvním nastavení `Price`se hodnota rozšíří na `DayOpen`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="9ae1b-141">Po nastavení `Price`aplikace vypočítá hodnoty vlastností `Change` a `PercentChange` na základě rozdílu mezi `Price` a `DayOpen`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="9ae1b-142">Vytvoření tříd StockTickerHub a StockTicker</span><span class="sxs-lookup"><span data-stu-id="9ae1b-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="9ae1b-143">K řízení interakce mezi klientem a serverem použijete rozhraní API centra signalizace.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="9ae1b-144">Třída `StockTickerHub`, která je odvozena od `Hub` Signal třídy, bude zpracovávat přijímání připojení a volání metod od klientů.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="9ae1b-145">Také je nutné zachovat skladová data a spustit objekt `Timer`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="9ae1b-146">Objekt `Timer` bude pravidelně spouštět cenové aktualizace nezávisle na připojeních klienta.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="9ae1b-147">Tyto funkce nemůžete umístit do `Hub` třídy, protože rozbočovače jsou přechodné.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="9ae1b-148">Aplikace vytvoří instanci `Hub` třídy pro každý úkol v centru, jako třeba připojení a volání z klienta na server.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="9ae1b-149">Proto mechanismus, který udržuje skladová data, aktualizuje ceny a vysílá, je nutné, aby ceny aktualizací běžely v samostatné třídě.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="9ae1b-150">Pojmenujte třídu `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-150">You'll name the class `StockTicker`.</span></span>

![Všesměrové vysílání z StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="9ae1b-152">Přejete si, aby na serveru běžela jenom jedna instance `StockTicker` třídy, takže budete muset nastavit odkaz z každé instance `StockTickerHub` na instanci `StockTicker` typu singleton.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="9ae1b-153">Třída `StockTicker` musí vysílat klientům, protože má uložená data a triggery, ale `StockTicker` není třída `Hub`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="9ae1b-154">Třída `StockTicker` musí získat odkaz na objekt kontextu připojení centra signalizace.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="9ae1b-155">Pak může pomocí objektu kontextu připojení vysílače vysílat klientům.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="9ae1b-156">Vytvořit StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="9ae1b-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="9ae1b-157">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="9ae1b-158">V **položce Přidat novou položku-Signal. StockTicker**vyberte **Installed** > **Visual C#**  > **Web** > **signaler** a pak vyberte **Třída centra signalizace (v2)** .</span><span class="sxs-lookup"><span data-stu-id="9ae1b-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="9ae1b-159">Pojmenujte třídu *StockTickerHub* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="9ae1b-160">Tento krok vytvoří soubor třídy *StockTickerHub.cs* .</span><span class="sxs-lookup"><span data-stu-id="9ae1b-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="9ae1b-161">Současně přidá sadu souborů skriptu a odkazy na sestavení, které podporuje signalizaci do projektu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="9ae1b-162">Nahraďte kód v souboru *StockTickerHub.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="9ae1b-163">Uložte soubor.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-163">Save the file.</span></span>

<span data-ttu-id="9ae1b-164">Aplikace používá třídu [centra](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) k definování metod, které mohou klienti volat na serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="9ae1b-165">Definujete jednu metodu: `GetAllStocks()`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="9ae1b-166">Když se klient poprvé připojí k serveru, zavolá tuto metodu, aby získal seznam všech populací s jejich aktuálními cenami.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="9ae1b-167">Metoda může běžet synchronně a vracet `IEnumerable<Stock>`, protože vrací data z paměti.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="9ae1b-168">Pokud metoda musela získat data pomocí něčeho, co by vyžadovala čekání, jako je vyhledávání databáze nebo volání webové služby, zadejte `Task<IEnumerable<Stock>>` jako návratovou hodnotu pro povolení asynchronního zpracování.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="9ae1b-169">Další informace najdete v tématu [Průvodce rozhraním API pro centra ASP.NET signálu – Server – kdy se má provést asynchronní spuštění](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span><span class="sxs-lookup"><span data-stu-id="9ae1b-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="9ae1b-170">Atribut `HubName` určuje, jak bude aplikace odkazovat na centrum v kódu JavaScriptu na klientovi.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="9ae1b-171">Výchozí název v klientovi Pokud tento atribut nepoužíváte, je camelCase verze názvu třídy, který v tomto případě by byl `stockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="9ae1b-172">Jak uvidíte později při vytváření `StockTicker` třídy, aplikace vytvoří instanci typu Singleton této třídy ve své statické vlastnosti `Instance`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="9ae1b-173">Tato instance typu Singleton `StockTicker` je v paměti bez ohledu na počet klientů, kteří se připojují nebo odpojí.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="9ae1b-174">Tato instance je to, co metoda `GetAllStocks()` používá k vrácení aktuálních informací o zásobách.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="9ae1b-175">Create StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="9ae1b-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="9ae1b-176">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **třídu**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="9ae1b-177">Pojmenujte třídu *StockTicker* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="9ae1b-178">Nahraďte kód v souboru *StockTicker.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="9ae1b-179">Vzhledem k tomu, že všechna vlákna budou spouštět stejnou instanci StockTicker kódu, musí být třída StockTicker bezpečná pro přístup z více vláken.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="9ae1b-180">Kontrola kódu serveru</span><span class="sxs-lookup"><span data-stu-id="9ae1b-180">Examine the server code</span></span>

<span data-ttu-id="9ae1b-181">Pokud prohlížíte kód serveru, pomůže vám pochopit, jak aplikace funguje.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="9ae1b-182">Ukládání instance singleton do statického pole</span><span class="sxs-lookup"><span data-stu-id="9ae1b-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="9ae1b-183">Kód inicializuje pole static `_instance`, které vrátí vlastnost `Instance` s instancí třídy.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="9ae1b-184">Vzhledem k tomu, že konstruktor je privátní, je jedinou instancí třídy, kterou může aplikace vytvořit.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="9ae1b-185">Aplikace používá [opožděnou inicializaci](/dotnet/framework/performance/lazy-initialization) pro pole `_instance`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="9ae1b-186">Není z důvodů výkonu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-186">It's not for performance reasons.</span></span> <span data-ttu-id="9ae1b-187">Je potřeba se ujistit, že vytváření instancí je bezpečné pro přístup z více vláken.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="9ae1b-188">Pokaždé, když se klient připojí k serveru, nová instance třídy StockTickerHub spuštěné v samostatném vlákně získá instanci StockTicker singleton z vlastnosti `StockTicker.Instance` static, jak jste viděli dříve ve třídě `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="9ae1b-189">Ukládání uložených dat v ConcurrentDictionary</span><span class="sxs-lookup"><span data-stu-id="9ae1b-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="9ae1b-190">Konstruktor inicializuje kolekci `_stocks` s některými ukázkovými datovými daty a `GetAllStocks` vrátí tyto akcie.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="9ae1b-191">Jak bylo uvedeno dříve, tato kolekce populací je vrácena `StockTickerHub.GetAllStocks`, což je metoda serveru ve třídě `Hub`, kterou mohou klienti volat.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="9ae1b-192">Kolekce akcie je definována jako [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) typ pro bezpečnost vlákna.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="9ae1b-193">Jako alternativu můžete použít objekt [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) a explicitně zamknout slovník při provádění změn v něm.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="9ae1b-194">Pro tuto ukázkovou aplikaci je to v pořádku, pokud ukládáte data aplikace do paměti a ztratíte data, když aplikace odstraní instanci `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="9ae1b-195">V reálné aplikaci byste měli pracovat s back-end datovým úložištěm, jako je databáze.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="9ae1b-196">Pravidelná aktualizace cen akcií</span><span class="sxs-lookup"><span data-stu-id="9ae1b-196">Periodically updating stock prices</span></span>

<span data-ttu-id="9ae1b-197">Konstruktor spustí objekt `Timer`, který pravidelně volá metody, které aktualizují skladové ceny náhodným základem.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="9ae1b-198">`Timer` volá `UpdateStockPrices`, která předá hodnotu null v parametru State.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="9ae1b-199">Před aktualizací cen aplikace převezme zámek na objekt `_updateStockPricesLock`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="9ae1b-200">Kód zkontroluje, jestli už jiný podproces aktualizuje ceny, a pak na každý Sklad v seznamu zavolá `TryUpdateStockPrice`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="9ae1b-201">`TryUpdateStockPrice` metoda rozhoduje o tom, jestli se má změnit cena akcií, a kolik se má změnit.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="9ae1b-202">Pokud se změní cena akcií, aplikace zavolá `BroadcastStockPrice`, aby vysílaly na všech připojených klientech změnu ceny akcií.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="9ae1b-203">Příznak `_updatingStockPrices` označený jako [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) , aby se zajistilo, že je bezpečný pro přístup z více vláken.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="9ae1b-204">V reálné aplikaci by metoda `TryUpdateStockPrice` zavolala webovou službu, aby vyhledala cenu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="9ae1b-205">V tomto kódu aplikace používá generátor náhodných čísel k náhodnému provedení změn.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="9ae1b-206">Získání kontextu signálu, aby třída StockTicker mohla vysílat klientům</span><span class="sxs-lookup"><span data-stu-id="9ae1b-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="9ae1b-207">Vzhledem k tomu, že změny ceny pocházejí zde v objektu `StockTicker`, je objekt, který musí volat metodu `updateStockPrice` na všech připojených klientech.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="9ae1b-208">Ve třídě `Hub` máte rozhraní API pro volání metod klienta, ale `StockTicker` nejsou odvozeny od třídy `Hub` a nemají odkaz na žádný objekt `Hub`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="9ae1b-209">Pro všesměrové vysílání pro připojené klienty musí třída `StockTicker` získat kontextovou instanci signálu pro `StockTickerHub` třídu a použít ji pro volání metod v klientech.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="9ae1b-210">Kód získá odkaz na kontext signalizace při vytvoření instance třídy singleton, předá tento odkaz na konstruktor a konstruktor ho vloží do vlastnosti `Clients`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="9ae1b-211">Existují dva důvody, proč chcete kontext získat pouze jednou: získání kontextu je nákladná úloha a když aplikace zachová zamýšlené pořadí zpráv odesílaných klientovi.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="9ae1b-212">Získání vlastnosti `Clients` kontextu a jeho vložení do vlastnosti `StockTickerClient` umožňuje napsat kód pro volání klientských metod, které vypadají stejně jako ve třídě `Hub`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="9ae1b-213">Chcete-li například vysílat do všech klientů, můžete zapisovat `Clients.All.updateStockPrice(stock)`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="9ae1b-214">Metoda `updateStockPrice`, kterou voláte v `BroadcastStockPrice`, ještě neexistuje.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="9ae1b-215">Později ji přidáte při psaní kódu, který běží na klientovi.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="9ae1b-216">Na `updateStockPrice` tady můžete odkazovat, protože `Clients.All` je dynamická, což znamená, že aplikace vyhodnotí výraz za běhu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="9ae1b-217">Když se spustí toto volání metody, odesílatel pošle do klienta název metody a hodnotu parametru. Pokud má klient metodu s názvem `updateStockPrice`, aplikace tuto metodu zavolá a předá jí hodnotu parametru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="9ae1b-218">`Clients.All` znamená odeslání všem klientům.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="9ae1b-219">Signalizace nabízí další možnosti určení klientů nebo skupin klientů, které se mají odeslat.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="9ae1b-220">Další informace najdete v tématu [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="9ae1b-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="9ae1b-221">Registrace trasy signalizace</span><span class="sxs-lookup"><span data-stu-id="9ae1b-221">Register the SignalR route</span></span>

<span data-ttu-id="9ae1b-222">Server musí znát, která adresa URL má zachytit a směrovat na signál.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="9ae1b-223">K tomu přidejte třídu pro spuštění OWIN:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="9ae1b-224">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="9ae1b-225">V **položce Přidat novou položku-Signal. StockTicker** vyberte **nainstalované** > **Visual C#**  > **Web** a pak vyberte **třídu pro spuštění Owin**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="9ae1b-226">Pojmenujte *spouštěcí* třídu a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="9ae1b-227">Nahraďte výchozí kód v souboru *Startup.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="9ae1b-228">Nyní jste dokončili nastavování kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="9ae1b-229">V další části nastavíte klienta.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="9ae1b-230">Nastavení kódu klienta</span><span class="sxs-lookup"><span data-stu-id="9ae1b-230">Set up the client code</span></span>

<span data-ttu-id="9ae1b-231">V této části nastavíte kód, který se spouští na klientovi.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="9ae1b-232">Vytvoření stránky HTML a souboru JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="9ae1b-233">Na stránce HTML se zobrazí data a soubor JavaScriptu bude organizovat data.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="9ae1b-234">Create StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="9ae1b-234">Create StockTicker.html</span></span>

<span data-ttu-id="9ae1b-235">Nejprve přidáte klienta HTML.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="9ae1b-236">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **stránku HTML**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="9ae1b-237">Pojmenujte soubor *StockTicker* a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="9ae1b-238">Nahraďte výchozí kód v souboru *StockTicker. html* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="9ae1b-239">KÓD HTML vytvoří tabulku s pěti sloupci, řádkem záhlaví a datovým řádkem s jedinou buňkou, která zahrnuje všechny pět sloupců.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="9ae1b-240">Řádek dat zobrazuje "načítání..." při každém spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="9ae1b-241">JavaScriptový kód odstraní tento řádek a přidá ho do svých řádků s uloženými daty načtenými ze serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="9ae1b-242">Značky skriptu určují:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-242">The script tags specify:</span></span>

    * <span data-ttu-id="9ae1b-243">Soubor skriptu jQuery.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-243">The jQuery script file.</span></span>

    * <span data-ttu-id="9ae1b-244">Základní soubor skriptu nástroje Signaler.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="9ae1b-245">Soubor skriptu proxy signalizace.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="9ae1b-246">Soubor skriptu StockTicker, který vytvoříte později.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="9ae1b-247">Aplikace dynamicky generuje soubor skriptu proxy serverů signalizace.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="9ae1b-248">Určuje adresu URL "/SignalR/Hubs" a definuje metody proxy pro metody ve třídě hub, v tomto případě pro `StockTickerHub.GetAllStocks`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="9ae1b-249">Pokud budete chtít, můžete tento soubor JavaScriptu vygenerovat ručně pomocí [nástrojů pro signalizaci](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span><span class="sxs-lookup"><span data-stu-id="9ae1b-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="9ae1b-250">Nezapomeňte zakázat dynamické vytváření souborů ve volání metody `MapHubs`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="9ae1b-251">V **Průzkumník řešení**rozbalte položku **skripty**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="9ae1b-252">Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9ae1b-253">Správce balíčků nainstaluje novější verzi skriptů nástroje Signal.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="9ae1b-254">Aktualizujte odkazy na skripty v bloku kódu tak, aby odpovídaly verzím souborů skriptu v projektu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="9ae1b-255">V **Průzkumník řešení**klikněte pravým tlačítkem na *StockTicker. html*a pak vyberte **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="9ae1b-256">Create StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="9ae1b-256">Create StockTicker.js</span></span>

<span data-ttu-id="9ae1b-257">Nyní vytvořte soubor JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="9ae1b-258">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **soubor JavaScriptu**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="9ae1b-259">Pojmenujte soubor *StockTicker* a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="9ae1b-260">Přidejte tento kód do souboru *StockTicker. js* :</span><span class="sxs-lookup"><span data-stu-id="9ae1b-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="9ae1b-261">Projděte si kód klienta.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-261">Examine the client code</span></span>

<span data-ttu-id="9ae1b-262">Pokud prohlížíte kód klienta, pomůže vám se dozvědět, jak kód klienta komunikuje s kódem serveru, aby aplikace fungovala.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="9ae1b-263">Spouští se připojení.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-263">Starting the connection</span></span>

<span data-ttu-id="9ae1b-264">`$.connection` odkazuje na proxy signálů.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="9ae1b-265">Kód získá odkaz na proxy pro třídu `StockTickerHub` a vloží jej do proměnné `ticker`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="9ae1b-266">Název proxy je název, který byl nastaven atributem `HubName`:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="9ae1b-267">Po definování všech proměnných a funkcí se poslední řádek kódu v souboru inicializuje připojením k signalizaci voláním funkce Signal `start`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="9ae1b-268">Funkce `start` provádí asynchronní a vrací [odložený objekt jQuery](http://api.jquery.com/category/deferred-object/).</span><span class="sxs-lookup"><span data-stu-id="9ae1b-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="9ae1b-269">Můžete zavolat funkci Hotovo pro určení funkce, která má být volána, když aplikace dokončí asynchronní akci.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="9ae1b-270">Získávání všech populací</span><span class="sxs-lookup"><span data-stu-id="9ae1b-270">Getting all the stocks</span></span>

<span data-ttu-id="9ae1b-271">Funkce `init` volá funkci `getAllStocks` na serveru a používá informace, které server vrátí k aktualizaci skladové tabulky.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="9ae1b-272">Všimněte si, že ve výchozím nastavení je nutné použít camelCasing na straně klienta, i když název metody je Pascal-použita na serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="9ae1b-273">Pravidlo camelCasing se vztahuje pouze na metody, nikoli na objekty.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="9ae1b-274">Například odkazujete na `stock.Symbol` a `stock.Price`, nikoli `stock.symbol` nebo `stock.price`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="9ae1b-275">V metodě `init` aplikace vytvoří HTML pro řádek tabulky pro každý burzovní objekt přijatý ze serveru voláním `formatStock` k formátování vlastností objektu `stock` a následným voláním `supplant` k nahrazení zástupných symbolů v `rowTemplate` proměnné s hodnotami vlastností objektu `stock`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="9ae1b-276">Výsledný kód HTML se pak připojí k uložené tabulce.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="9ae1b-277">Zavoláte `init` tím, že ho předáte do jako `callback` funkce, která se spustí po dokončení asynchronní funkce `start`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="9ae1b-278">Pokud jste po volání `start`zavolali `init` jako samostatný příkaz jazyka JavaScript, funkce by nebyla úspěšná, protože by běžela okamžitě bez čekání na dokončení funkce Start pro dokončení navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="9ae1b-279">V takovém případě se funkce `init` pokusí zavolat funkci `getAllStocks` předtím, než aplikace naváže připojení k serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="9ae1b-280">Získání aktualizovaných cen akcií</span><span class="sxs-lookup"><span data-stu-id="9ae1b-280">Getting updated stock prices</span></span>

<span data-ttu-id="9ae1b-281">Když server změní cenu akcií, zavolá `updateStockPrice` v připojených klientech.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="9ae1b-282">Aplikace přidá funkci do vlastnosti klient `stockTicker`ového proxy serveru, aby byla dostupná pro volání ze serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="9ae1b-283">Funkce `updateStockPrice` formátuje burzovní objekt přijatý ze serveru do řádku tabulky stejným způsobem jako ve funkci `init`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="9ae1b-284">Místo připojení řádku k tabulce najde aktuální řádek v tabulce a nahradí ho novým řádkem.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="9ae1b-285">Testování aplikace</span><span class="sxs-lookup"><span data-stu-id="9ae1b-285">Test the application</span></span>

<span data-ttu-id="9ae1b-286">Aplikaci můžete otestovat a ujistit se, že funguje.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="9ae1b-287">Zobrazí se všechna okna prohlížeče s živými zásobami, kde se pohybuje ceny akcií.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="9ae1b-288">Na panelu nástrojů zapněte **ladění skriptů** a pak výběrem tlačítka Přehrát spusťte aplikaci v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Snímek obrazovky uživatele, který zapíná režim ladění a vybere možnost Přehrát.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="9ae1b-290">Otevře se okno prohlížeče, ve kterém se zobrazí **tabulka živé akcie**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="9ae1b-291">V tabulce se zpočátku zobrazuje "načítání...". Po krátké době aplikace zobrazuje počáteční skladová data a pak se ceny akcií začnou měnit.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="9ae1b-292">Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="9ae1b-293">Počáteční zobrazovací displej je stejný jako první prohlížeč a změny probíhají současně.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="9ae1b-294">Zavřete všechny prohlížeče, otevřete nový prohlížeč a přejdete na stejnou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="9ae1b-295">Objekt typu Singleton StockTicker pokračuje v běhu na serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="9ae1b-296">**Tabulka živých zásob** uvádí, že zásoby se pořád mění.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="9ae1b-297">Počáteční tabulka se nezobrazuje s nulovými hodnotami změny.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="9ae1b-298">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="9ae1b-299">Povolte protokolování</span><span class="sxs-lookup"><span data-stu-id="9ae1b-299">Enable logging</span></span>

<span data-ttu-id="9ae1b-300">Signál má vestavěnou funkci protokolování, kterou můžete na klientovi povolit, aby při řešení potíží mohl pomoci.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="9ae1b-301">V této části povolíte protokolování a uvidíte příklady, které ukazují, jak protokoly říkají, které z následujících signálů přenosových metod používá:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="9ae1b-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), které podporuje služba IIS 8 a aktuální prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="9ae1b-303">[Události odeslané serverem](http://en.wikipedia.org/wiki/Server-sent_events), které podporují jiné prohlížeče než Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="9ae1b-304">[Trvale rámec](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), který podporuje Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="9ae1b-305">[Dlouhé cyklické dotazování AJAX](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), podporované všemi prohlížeči</span><span class="sxs-lookup"><span data-stu-id="9ae1b-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="9ae1b-306">Pro jakékoli dané připojení vybírá signál nejlepší metodu přenosu, kterou podporuje server i klientská podpora.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="9ae1b-307">Otevřete *StockTicker. js*.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="9ae1b-308">Přidejte tento zvýrazněný řádek kódu, chcete-li povolit protokolování bezprostředně před kódem, který inicializuje připojení na konci souboru:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="9ae1b-309">Stisknutím klávesy **F5** spusťte projekt.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="9ae1b-310">Otevřete okno vývojářské nástroje v prohlížeči a vyberte konzolu, abyste zobrazili protokoly.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="9ae1b-311">Možná budete muset aktualizovat stránku, aby se zobrazily protokoly signalizace vyjednávat přenosovou metodou pro nové připojení.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="9ae1b-312">Pokud používáte Internet Explorer 10 v systému Windows 8 (IIS 8), je přenosová metoda **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="9ae1b-313">Pokud používáte Internet Explorer 10 v systému Windows 7 (IIS 7,5), je přenosová metoda **IFRAME**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="9ae1b-314">Pokud používáte Firefox 19 v systému Windows 8 (IIS 8), je přenosová metoda **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="9ae1b-315">V prohlížeči Firefox nainstalujte doplněk Firebug a získejte okno konzoly.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="9ae1b-316">Pokud používáte Firefox 19 v systému Windows 7 (IIS 7,5), přenosová metoda je události **odesílané serverem** .</span><span class="sxs-lookup"><span data-stu-id="9ae1b-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="9ae1b-317">Instalace ukázky StockTicker</span><span class="sxs-lookup"><span data-stu-id="9ae1b-317">Install the StockTicker sample</span></span>

<span data-ttu-id="9ae1b-318">[Microsoft. ASPNET. signaler. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) nainstaluje aplikaci StockTicker.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="9ae1b-319">Balíček NuGet zahrnuje více funkcí, než je zjednodušená verze, kterou jste vytvořili úplně od začátku.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="9ae1b-320">V této části kurzu nainstalujete balíček NuGet a zkontrolujete nové funkce a kód, který je implementuje.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ae1b-321">Pokud balíček nainstalujete bez provedení předchozích kroků tohoto kurzu, musíte do svého projektu přidat třídu pro spuštění OWIN.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="9ae1b-322">Tento krok popisuje tento soubor Readme. txt pro balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="9ae1b-323">Instalace nástroje Signal. Sample NuGet Package</span><span class="sxs-lookup"><span data-stu-id="9ae1b-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="9ae1b-324">V **Průzkumník řešení**klikněte pravým tlačítkem na projekt a vyberte **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="9ae1b-325">Ve **Správci balíčků NuGet: Signal. StockTicker**, vyberte **Procházet**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="9ae1b-326">Ze **zdroje balíčku**vyberte možnost **NuGet.org**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="9ae1b-327">Do vyhledávacího pole zadejte *Signal. Sample* a vyberte **Microsoft. ASPNET. signaler. Sample** > **install**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="9ae1b-328">V **Průzkumník řešení**rozbalte složku *Signal. Sample* .</span><span class="sxs-lookup"><span data-stu-id="9ae1b-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="9ae1b-329">Instalace nástroje Signal. vzorový balíček vytvořil složku a její obsah.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="9ae1b-330">Ve složce *Signal. Sample* klikněte pravým tlačítkem na *StockTicker. html*a pak vyberte **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ae1b-331">Instalace nástroje Signal. vzorový balíček NuGet může změnit verzi jQuery, kterou máte ve složce *Scripts* .</span><span class="sxs-lookup"><span data-stu-id="9ae1b-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="9ae1b-332">Nový soubor *StockTicker. html* , který balíček nainstaluje do nástroje *Signal. vzorová* složka bude synchronizována s verzí jQuery, kterou balíček nainstaluje, ale pokud chcete znovu spustit původní soubor *StockTicker. html* , bude pravděpodobně nutné nejprve aktualizovat odkaz jQuery ve značce Script.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="9ae1b-333">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="9ae1b-333">Run the application</span></span>

 <span data-ttu-id="9ae1b-334">Tabulka, kterou jste viděli v první aplikaci, měla užitečné funkce.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="9ae1b-335">Celá burzovní aplikace na více datových cyklech zobrazuje nové funkce: vodorovné posuvné okno, které zobrazuje burzovní data a zásoby, které mění barvu při jejich zvyšování a poklesu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="9ae1b-336">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="9ae1b-337">Při prvním spuštění aplikace je "trh" "zavřený" a zobrazí se statická tabulka a okno se značkami, které se neposunují.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="9ae1b-338">Vyberte **otevřít trh**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-338">Select **Open Market**.</span></span>

    ![Snímek obrazovky živého ticku](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="9ae1b-340">Pole se seznamem **živých akcií** se začne posouvat vodorovně a server začne pravidelně vysílat změny cen akcií na náhodném základě.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="9ae1b-341">Pokaždé, když se změní cena na zásobě, aplikace aktualizuje **tabulku Live Stock** a **živý**burzovní modul.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="9ae1b-342">Když je cenová změna zásob kladná, aplikace zobrazí akcie se zeleným pozadím.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="9ae1b-343">Když je změna záporná, aplikace zobrazí burzovní skladem s červeným pozadím.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="9ae1b-344">Vyberte možnost **Zavřít trh**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="9ae1b-345">Zastaví se aktualizace tabulky.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-345">The table updates stop.</span></span>

    * <span data-ttu-id="9ae1b-346">Tato značka zastaví rolování.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="9ae1b-347">Vyberte **obnovit**.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-347">Select **Reset**.</span></span>

    * <span data-ttu-id="9ae1b-348">Všechna skladová data se resetují.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-348">All stock data is reset.</span></span>

    * <span data-ttu-id="9ae1b-349">Aplikace obnoví počáteční stav předtím, než se změny cen spustí.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="9ae1b-350">Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="9ae1b-351">Stejná data se v každém prohlížeči zobrazují v současné době dynamicky.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="9ae1b-352">Když vyberete kterýkoli z ovládacích prvků, všechny prohlížeče budou reagovat stejně jako ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="9ae1b-353">Živý displej se zobrazením akcií</span><span class="sxs-lookup"><span data-stu-id="9ae1b-353">Live Stock Ticker display</span></span>

<span data-ttu-id="9ae1b-354">**Živý burzovní** displej je neuspořádaný seznam prvku `<div>` formátovaného na jeden řádek pomocí stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="9ae1b-355">Aplikace inicializuje a aktualizuje pro něj stejný způsob jako tabulka: nahrazením zástupných symbolů v řetězci šablony `<li>` a dynamickém přidáním `<li>` prvků do `<ul>` elementu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="9ae1b-356">Aplikace zahrnuje posouvání pomocí funkce jQuery `animate` pro změnu levého okraje seznamu neuspořádaného v rámci `<div>`.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="9ae1b-357">Signale. Sample StockTicker. html</span><span class="sxs-lookup"><span data-stu-id="9ae1b-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="9ae1b-358">Burzovní kód HTML s taktem:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="9ae1b-359">Signal. Sample StockTicker. CSS</span><span class="sxs-lookup"><span data-stu-id="9ae1b-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="9ae1b-360">Burzovní kód pro vystavení akcií:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="9ae1b-361">Signalizace. Ukázka signálu. StockTicker. js</span><span class="sxs-lookup"><span data-stu-id="9ae1b-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="9ae1b-362">Kód jQuery, který usnadňuje posunutí:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="9ae1b-363">Další metody na serveru, který může klient volat</span><span class="sxs-lookup"><span data-stu-id="9ae1b-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="9ae1b-364">Pro přidání flexibility do aplikace jsou k dispozici další metody, které může aplikace volat.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="9ae1b-365">Signál. Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="9ae1b-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="9ae1b-366">Třída `StockTickerHub` definuje čtyři další metody, které může klient volat:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="9ae1b-367">Aplikace volá `OpenMarket`, `CloseMarket`a `Reset` v reakci na tlačítka v horní části stránky.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="9ae1b-368">Ukazují vzor jednoho klienta, který aktivuje změnu stavu okamžitě šířenou pro všechny klienty.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="9ae1b-369">Každá z těchto metod volá metodu ve třídě `StockTicker`, která způsobuje změnu stavu trhu a pak vysílá nový stav.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="9ae1b-370">Signál. Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="9ae1b-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="9ae1b-371">Ve třídě `StockTicker` aplikace udržuje stav trhu s vlastností `MarketState`, která vrací `MarketState` hodnotu výčtu:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="9ae1b-372">Každá z metod, které mění stav trhu, je v bloku zámku, protože třída `StockTicker` musí být bezpečná pro přístup z více vláken:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="9ae1b-373">Chcete-li zajistit, aby byl tento kód bezpečný pro přístup z více vláken, `_marketState` pole, které vrátí vlastnost `MarketState` určenou `volatile`:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="9ae1b-374">Metody `BroadcastMarketStateChange` a `BroadcastMarketReset` jsou podobné metodě BroadcastStockPrice, kterou jste již viděli, s výjimkou volání různých metod definovaných v klientovi:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="9ae1b-375">Další funkce v klientovi, které může server volat</span><span class="sxs-lookup"><span data-stu-id="9ae1b-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="9ae1b-376">Funkce `updateStockPrice` nyní zpracovává tabulku i zobrazení značek a používá `jQuery.Color` k blikání červené a zelené barvy.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="9ae1b-377">Nové funkce v nástroji *Signal. StockTicker. js* povolují a zakazují tlačítka na základě stavu trhu.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="9ae1b-378">Také zastavují nebo spouštějí automatické **posouvání akcií.**</span><span class="sxs-lookup"><span data-stu-id="9ae1b-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="9ae1b-379">Vzhledem k tomu, že se do `ticker.client`přidávají mnoho funkcí, aplikace k jejich přidání používá [funkci jQuery Extended](http://api.jquery.com/jQuery.extend/) .</span><span class="sxs-lookup"><span data-stu-id="9ae1b-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="9ae1b-380">Další nastavení klienta po navázání připojení</span><span class="sxs-lookup"><span data-stu-id="9ae1b-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="9ae1b-381">Poté, co klient připojení naváže, provede další práci:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="9ae1b-382">Zjistěte, jestli je trh otevřený nebo zavřený pro volání příslušné `marketOpened` nebo `marketClosed` funkce.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="9ae1b-383">Připojte volání metody serveru k tlačítkům.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="9ae1b-384">Metody serveru nejsou kabelové až do tlačítek, dokud aplikace nevytvoří připojení.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="9ae1b-385">To znamená, že kód nemůže volat metody serveru předtím, než budou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ae1b-386">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="9ae1b-386">Additional resources</span></span>

<span data-ttu-id="9ae1b-387">V tomto kurzu jste se naučili, jak programovat aplikaci pro signalizaci, která vysílá zprávy ze serveru do všech připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="9ae1b-388">Nyní můžete zprávy pravidelně vysílat a reagovat na oznámení od libovolného klienta.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="9ae1b-389">Koncept instance s více vlákny můžete použít k údržbě stavu serveru ve scénářích hraní online her pro více hráčů.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="9ae1b-390">Příklad najdete v tématu [hry pro sestřelení na základě signalizace](https://github.com/NTaylorMullen/ShootR).</span><span class="sxs-lookup"><span data-stu-id="9ae1b-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="9ae1b-391">Kurzy, které ukazují scénáře komunikace peer-to-peer, najdete v tématu [Začínáme s nástrojem pro signalizaci](introduction-to-signalr.md) a [aktualizací v reálném čase pomocí nástroje signaler](tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="9ae1b-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="9ae1b-392">Další informace o signalizaci naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="9ae1b-393">ASP.NET signál</span><span class="sxs-lookup"><span data-stu-id="9ae1b-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="9ae1b-394">Projekt signálu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="9ae1b-395">GitHub a ukázky signálů</span><span class="sxs-lookup"><span data-stu-id="9ae1b-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="9ae1b-396">Wiki signálu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="9ae1b-397">Další kroky</span><span class="sxs-lookup"><span data-stu-id="9ae1b-397">Next steps</span></span>

<span data-ttu-id="9ae1b-398">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="9ae1b-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ae1b-399">Projekt se vytvořil.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-399">Created the project</span></span>
> * <span data-ttu-id="9ae1b-400">Nastavení serverového kódu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-400">Set up the server code</span></span>
> * <span data-ttu-id="9ae1b-401">Zkontrolovali jste kód serveru.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-401">Examined the server code</span></span>
> * <span data-ttu-id="9ae1b-402">Nastavení kódu klienta</span><span class="sxs-lookup"><span data-stu-id="9ae1b-402">Set up the client code</span></span>
> * <span data-ttu-id="9ae1b-403">Prověření klientského kódu</span><span class="sxs-lookup"><span data-stu-id="9ae1b-403">Examined the client code</span></span>
> * <span data-ttu-id="9ae1b-404">Otestování aplikace</span><span class="sxs-lookup"><span data-stu-id="9ae1b-404">Tested the application</span></span>
> * <span data-ttu-id="9ae1b-405">Povolené protokolování</span><span class="sxs-lookup"><span data-stu-id="9ae1b-405">Enabled logging</span></span>

<span data-ttu-id="9ae1b-406">V dalším článku se dozvíte, jak vytvořit webovou aplikaci v reálném čase, která používá signál ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="9ae1b-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9ae1b-407">Vytvoření webové aplikace v reálném čase pomocí signalizace</span><span class="sxs-lookup"><span data-stu-id="9ae1b-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
