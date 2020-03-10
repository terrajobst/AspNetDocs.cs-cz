---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 'Kurz: Vytvoření aplikace s vysokou frekvencí v reálném čase pomocí signalizace 2 | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která pomocí ASP.NET signalizace poskytuje funkce pro vysokou četnost zasílání zpráv.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558623"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="72d2a-103">Kurz: Vytvoření aplikace s vysokou frekvencí v reálném čase pomocí signálů 2</span><span class="sxs-lookup"><span data-stu-id="72d2a-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="72d2a-104">V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá signál ASP.NET 2 k poskytování funkcí vysoké frekvence zasílání zpráv.</span><span class="sxs-lookup"><span data-stu-id="72d2a-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="72d2a-105">V takovém případě "vysokorychlostní zasílání zpráv" znamená, že server odesílá aktualizace za pevnou sazbu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="72d2a-106">Za sekundu vám pošleme až 10 zpráv.</span><span class="sxs-lookup"><span data-stu-id="72d2a-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="72d2a-107">Vytvořená aplikace zobrazí obrazec, který mohou uživatelé přetáhnout.</span><span class="sxs-lookup"><span data-stu-id="72d2a-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="72d2a-108">Server aktualizuje pozici obrazce ve všech připojených prohlížečích tak, aby se shodovala s pozicí přetaženého obrazce pomocí časované aktualizace.</span><span class="sxs-lookup"><span data-stu-id="72d2a-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="72d2a-109">Koncepty představené v tomto kurzu obsahují aplikace v reálném čase a jiné aplikace simulace.</span><span class="sxs-lookup"><span data-stu-id="72d2a-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="72d2a-110">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="72d2a-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72d2a-111">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="72d2a-111">Set up the project</span></span>
> * <span data-ttu-id="72d2a-112">Vytvoření základní aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-112">Create the base application</span></span>
> * <span data-ttu-id="72d2a-113">Mapování na centrum při spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="72d2a-114">Přidání klienta</span><span class="sxs-lookup"><span data-stu-id="72d2a-114">Add the client</span></span>
> * <span data-ttu-id="72d2a-115">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-115">Run the app</span></span>
> * <span data-ttu-id="72d2a-116">Přidat smyčku klienta</span><span class="sxs-lookup"><span data-stu-id="72d2a-116">Add the client loop</span></span>
> * <span data-ttu-id="72d2a-117">Přidat smyčku serveru</span><span class="sxs-lookup"><span data-stu-id="72d2a-117">Add the server loop</span></span>
> * <span data-ttu-id="72d2a-118">Přidat plynulou animaci</span><span class="sxs-lookup"><span data-stu-id="72d2a-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="72d2a-119">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="72d2a-119">Prerequisites</span></span>

* <span data-ttu-id="72d2a-120">Sada [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) se sadou funkcí **Vývoj pro ASP.NET a web**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="72d2a-121">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="72d2a-121">Set up the project</span></span>

<span data-ttu-id="72d2a-122">V této části vytvoříte projekt v aplikaci Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="72d2a-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="72d2a-123">V této části se dozvíte, jak pomocí sady Visual Studio 2017 vytvořit prázdnou webovou aplikaci v ASP.NET a přidat knihovny Signal a jQuery. UI.</span><span class="sxs-lookup"><span data-stu-id="72d2a-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="72d2a-124">V aplikaci Visual Studio vytvořte webovou aplikaci v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="72d2a-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Vytvoření webu](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="72d2a-126">V okně **Nová webová aplikace v ASP.NET – MoveShapeDemo** ponechte vybrané **prázdné** a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="72d2a-127">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="72d2a-128">V **příkaz Přidat novou položku-MoveShapeDemo**vyberte možnost **nainstalováno** \*\* > C# > \*\* webového \*\* > a\*\* vyberte položku **centrum signalizace (v2)** .</span><span class="sxs-lookup"><span data-stu-id="72d2a-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="72d2a-129">Pojmenujte třídu *MoveShapeHub* a přidejte ji do projektu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="72d2a-130">Tento krok vytvoří soubor třídy *MoveShapeHub.cs* .</span><span class="sxs-lookup"><span data-stu-id="72d2a-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="72d2a-131">Současně přidá sadu souborů skriptu a odkazy na sestavení, které podporují signalizaci do projektu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="72d2a-132">Vyberte **nástroje** > **správce balíčků NuGet** > **konzole správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="72d2a-133">V **konzole správce balíčků**spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="72d2a-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="72d2a-134">Příkaz nainstaluje knihovnu uživatelského rozhraní jQuery.</span><span class="sxs-lookup"><span data-stu-id="72d2a-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="72d2a-135">Použijete ho k animaci obrazce.</span><span class="sxs-lookup"><span data-stu-id="72d2a-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="72d2a-136">V **Průzkumník řešení**rozbalte uzel skripty.</span><span class="sxs-lookup"><span data-stu-id="72d2a-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![Odkazy knihovny skriptů](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="72d2a-138">Knihovny skriptů pro jQuery, jQueryUI a Signal jsou viditelné v projektu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="72d2a-139">Vytvoření základní aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-139">Create the base application</span></span>

<span data-ttu-id="72d2a-140">V této části vytvoříte aplikaci v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="72d2a-140">In this section, you create a browser application.</span></span> <span data-ttu-id="72d2a-141">Aplikace během každé události přesunutí myši pošle umístění obrazce na server.</span><span class="sxs-lookup"><span data-stu-id="72d2a-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="72d2a-142">Server všesměrově vysílá tyto informace všem ostatním připojeným klientům v reálném čase.</span><span class="sxs-lookup"><span data-stu-id="72d2a-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="72d2a-143">Další informace o této aplikaci najdete v dalších částech.</span><span class="sxs-lookup"><span data-stu-id="72d2a-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="72d2a-144">Otevřete soubor *MoveShapeHub.cs* .</span><span class="sxs-lookup"><span data-stu-id="72d2a-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="72d2a-145">Nahraďte kód v souboru *MoveShapeHub.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="72d2a-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="72d2a-146">Uložte soubor.</span><span class="sxs-lookup"><span data-stu-id="72d2a-146">Save the file.</span></span>

<span data-ttu-id="72d2a-147">Třída `MoveShapeHub` je implementací centra signalizace.</span><span class="sxs-lookup"><span data-stu-id="72d2a-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="72d2a-148">Stejně jako v kurzu [Začínáme s nástrojem Signal](tutorial-getting-started-with-signalr.md) má centrum metodu, kterou klienti volají přímo.</span><span class="sxs-lookup"><span data-stu-id="72d2a-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="72d2a-149">V tomto případě klient pošle objekt s novými souřadnicemi X a Y obrazce na server.</span><span class="sxs-lookup"><span data-stu-id="72d2a-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="72d2a-150">Tyto souřadnice se dostanou do všech ostatních připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="72d2a-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="72d2a-151">Návěstí tento objekt automaticky serializovat pomocí formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="72d2a-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="72d2a-152">Aplikace odešle objekt `ShapeModel` klientovi.</span><span class="sxs-lookup"><span data-stu-id="72d2a-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="72d2a-153">Má členy pro uložení pozice obrazce.</span><span class="sxs-lookup"><span data-stu-id="72d2a-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="72d2a-154">Verze objektu na serveru má také člena, aby mohla sledovat, která data klienta jsou ukládána.</span><span class="sxs-lookup"><span data-stu-id="72d2a-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="72d2a-155">Tento objekt brání serveru v posílání dat klienta zpět do sebe samé.</span><span class="sxs-lookup"><span data-stu-id="72d2a-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="72d2a-156">Tento člen používá atribut `JsonIgnore` k tomu, aby aplikace mohla v serializaci dat a jejich odeslání zpátky klientovi.</span><span class="sxs-lookup"><span data-stu-id="72d2a-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="72d2a-157">Mapování na centrum při spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-157">Map to the hub when app starts</span></span>

<span data-ttu-id="72d2a-158">V dalším kroku nastavíte při spuštění aplikace mapování na centrum.</span><span class="sxs-lookup"><span data-stu-id="72d2a-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="72d2a-159">V nástroji Signal 2 Přidání třídy OWIN Startup vytvoří mapování.</span><span class="sxs-lookup"><span data-stu-id="72d2a-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="72d2a-160">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="72d2a-161">V **položce Přidat novou položku – MoveShapeDemo** vyberte **nainstalované** > **Visual C#**  > **Web** a pak vyberte **třídu pro spuštění Owin**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="72d2a-162">Pojmenujte *spouštěcí* třídu a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="72d2a-163">Nahraďte výchozí kód v souboru *Startup.cs* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="72d2a-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="72d2a-164">Spouštěcí třída OWIN volá `MapSignalR`, když aplikace spustí metodu `Configuration`.</span><span class="sxs-lookup"><span data-stu-id="72d2a-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="72d2a-165">Aplikace přidá třídu do procesu spouštění OWIN pomocí atributu `OwinStartup` Assembly.</span><span class="sxs-lookup"><span data-stu-id="72d2a-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="72d2a-166">Přidání klienta</span><span class="sxs-lookup"><span data-stu-id="72d2a-166">Add the client</span></span>

<span data-ttu-id="72d2a-167">Přidejte stránku HTML pro klienta.</span><span class="sxs-lookup"><span data-stu-id="72d2a-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="72d2a-168">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **stránku HTML**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="72d2a-169">Pojmenujte stránku **jako výchozí** a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="72d2a-170">V **Průzkumník řešení**klikněte pravým tlačítkem myši na *Default. html* a vyberte **nastavit jako úvodní stránku**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="72d2a-171">Nahraďte výchozí kód ve *výchozím souboru. html* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="72d2a-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="72d2a-172">V **Průzkumník řešení**rozbalte položku **skripty**.</span><span class="sxs-lookup"><span data-stu-id="72d2a-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="72d2a-173">Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="72d2a-174">Správce balíčků nainstaluje novější verzi skriptů nástroje Signaler.</span><span class="sxs-lookup"><span data-stu-id="72d2a-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="72d2a-175">Aktualizujte odkazy na skripty v bloku kódu tak, aby odpovídaly verzím souborů skriptu v projektu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="72d2a-176">Tento kód HTML a JavaScriptu vytvoří červené `div` s názvem `shape`.</span><span class="sxs-lookup"><span data-stu-id="72d2a-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="72d2a-177">Umožňuje chování obrazce při přetahování pomocí knihovny jQuery a používá událost `drag` k odeslání pozice obrazce na server.</span><span class="sxs-lookup"><span data-stu-id="72d2a-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="72d2a-178">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-178">Run the app</span></span>

<span data-ttu-id="72d2a-179">Aplikaci můžete spustit tak, aby se'e svou práci.</span><span class="sxs-lookup"><span data-stu-id="72d2a-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="72d2a-180">Když přetáhnete tvar kolem okna prohlížeče, obrazec se přesune i v jiných prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="72d2a-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="72d2a-181">Na panelu nástrojů zapněte **ladění skriptů** a pak vyberte tlačítko Přehrát a spusťte aplikaci v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="72d2a-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![Snímek obrazovky uživatele, který zapíná režim ladění a vybere možnost Přehrát.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="72d2a-183">Otevře se okno prohlížeče s červeným tvarem v pravém horním rohu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="72d2a-184">Zkopírujte adresu URL stránky.</span><span class="sxs-lookup"><span data-stu-id="72d2a-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="72d2a-185">Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.</span><span class="sxs-lookup"><span data-stu-id="72d2a-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="72d2a-186">Přetáhněte tvar v jednom z oken prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="72d2a-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="72d2a-187">Následuje tvar v jiném okně prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="72d2a-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="72d2a-188">Přestože aplikace funguje pomocí této metody, není doporučený programovací model.</span><span class="sxs-lookup"><span data-stu-id="72d2a-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="72d2a-189">Počet zpráv, které se odesílají, nejsou horním limitem.</span><span class="sxs-lookup"><span data-stu-id="72d2a-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="72d2a-190">V důsledku toho se klienti a Server budou zahlceni zprávami a snížení výkonu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="72d2a-191">Aplikace také zobrazuje na klientovi nesouvislou animaci.</span><span class="sxs-lookup"><span data-stu-id="72d2a-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="72d2a-192">Tato Jerky animace se stane, protože tvar je okamžitě přesunut každou metodou.</span><span class="sxs-lookup"><span data-stu-id="72d2a-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="72d2a-193">Je lepší, pokud se obrazec plynule přesune do každého nového umístění.</span><span class="sxs-lookup"><span data-stu-id="72d2a-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="72d2a-194">V dalším kroku se dozvíte, jak tyto problémy vyřešit.</span><span class="sxs-lookup"><span data-stu-id="72d2a-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="72d2a-195">Přidat smyčku klienta</span><span class="sxs-lookup"><span data-stu-id="72d2a-195">Add the client loop</span></span>

<span data-ttu-id="72d2a-196">Odeslání umístění obrazce při každé události přesunutí myši vytvoří zbytečný objem síťového provozu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="72d2a-197">Aplikace potřebuje omezit zprávy od klienta.</span><span class="sxs-lookup"><span data-stu-id="72d2a-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="72d2a-198">Pomocí funkce `setInterval` JavaScriptu můžete nastavit smyčku, která na server odesílá informace o nové pozici s pevnou sazbou.</span><span class="sxs-lookup"><span data-stu-id="72d2a-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="72d2a-199">Tato smyčka představuje základní reprezentaci "smyčky hry".</span><span class="sxs-lookup"><span data-stu-id="72d2a-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="72d2a-200">Tato funkce je opakovaně volána, která zařídí všechny funkce hry.</span><span class="sxs-lookup"><span data-stu-id="72d2a-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="72d2a-201">Nahraďte kód klienta ve *výchozím souboru. html* tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="72d2a-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="72d2a-202">Je nutné znovu nahradit odkazy na skript.</span><span class="sxs-lookup"><span data-stu-id="72d2a-202">You have to replace the script references again.</span></span> <span data-ttu-id="72d2a-203">Musí odpovídat verzím skriptů v projektu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="72d2a-204">Tento nový kód přidá funkci `updateServerModel`.</span><span class="sxs-lookup"><span data-stu-id="72d2a-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="72d2a-205">Nazývá se pevná frekvence.</span><span class="sxs-lookup"><span data-stu-id="72d2a-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="72d2a-206">Funkce odesílá data pozice na server vždy, když příznak `moved` označuje, že je k odeslání k dispozici nová data o poloze.</span><span class="sxs-lookup"><span data-stu-id="72d2a-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="72d2a-207">Kliknutím na tlačítko Přehrát spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="72d2a-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="72d2a-208">Zkopírujte adresu URL stránky.</span><span class="sxs-lookup"><span data-stu-id="72d2a-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="72d2a-209">Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.</span><span class="sxs-lookup"><span data-stu-id="72d2a-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="72d2a-210">Přetáhněte tvar v jednom z oken prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="72d2a-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="72d2a-211">Následuje tvar v jiném okně prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="72d2a-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="72d2a-212">Vzhledem k tomu, že aplikace omezuje počet zpráv, které se odesílají na server, animace se v první době neprojeví jako hladká.</span><span class="sxs-lookup"><span data-stu-id="72d2a-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="72d2a-213">Přidat smyčku serveru</span><span class="sxs-lookup"><span data-stu-id="72d2a-213">Add the server loop</span></span>

<span data-ttu-id="72d2a-214">V aktuální aplikaci se zprávy odesílané ze serveru do klienta dostanou tak často, jak jsou přijaty.</span><span class="sxs-lookup"><span data-stu-id="72d2a-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="72d2a-215">Tento provoz v síti představuje podobný problém, jaký vidíte na klientovi.</span><span class="sxs-lookup"><span data-stu-id="72d2a-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="72d2a-216">Aplikace může posílat zprávy častěji, než je potřeba.</span><span class="sxs-lookup"><span data-stu-id="72d2a-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="72d2a-217">V důsledku toho může dojít k zahlcení připojení.</span><span class="sxs-lookup"><span data-stu-id="72d2a-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="72d2a-218">Tato část popisuje, jak aktualizovat server a přidat časovač, který omezuje rychlost odchozích zpráv.</span><span class="sxs-lookup"><span data-stu-id="72d2a-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="72d2a-219">Nahraďte obsah `MoveShapeHub.cs` tímto kódem:</span><span class="sxs-lookup"><span data-stu-id="72d2a-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="72d2a-220">Kliknutím na tlačítko Přehrát spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="72d2a-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="72d2a-221">Zkopírujte adresu URL stránky.</span><span class="sxs-lookup"><span data-stu-id="72d2a-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="72d2a-222">Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.</span><span class="sxs-lookup"><span data-stu-id="72d2a-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="72d2a-223">Přetáhněte tvar v jednom z oken prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="72d2a-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="72d2a-224">Tento kód rozbalí klienta, aby přidal třídu `Broadcaster`.</span><span class="sxs-lookup"><span data-stu-id="72d2a-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="72d2a-225">Nová třída omezuje odchozí zprávy pomocí `Timer` třídy z rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="72d2a-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="72d2a-226">Je dobré vědět, že je samotný rozbočovač přechodný.</span><span class="sxs-lookup"><span data-stu-id="72d2a-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="72d2a-227">Je vytvořen pokaždé, když je potřeba.</span><span class="sxs-lookup"><span data-stu-id="72d2a-227">It's created every time it's needed.</span></span> <span data-ttu-id="72d2a-228">Aplikace proto vytvoří `Broadcaster` jako typ singleton.</span><span class="sxs-lookup"><span data-stu-id="72d2a-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="72d2a-229">Používá opožděnou inicializaci pro odložení `Broadcaster`ho vytváření, dokud není potřeba.</span><span class="sxs-lookup"><span data-stu-id="72d2a-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="72d2a-230">To zaručuje, že aplikace před spuštěním časovače úplně vytvoří první instanci centra.</span><span class="sxs-lookup"><span data-stu-id="72d2a-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="72d2a-231">Volání funkce `UpdateShape` klientů je pak přesunuto mimo metodu `UpdateModel` centra.</span><span class="sxs-lookup"><span data-stu-id="72d2a-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="72d2a-232">Už se nevolá hned, kdykoli aplikace obdrží příchozí zprávy.</span><span class="sxs-lookup"><span data-stu-id="72d2a-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="72d2a-233">Místo toho aplikace odesílá zprávy klientům rychlostí 25 volání za sekundu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="72d2a-234">Proces je spravován pomocí časovače `_broadcastLoop` z `Broadcaster` třídy.</span><span class="sxs-lookup"><span data-stu-id="72d2a-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="72d2a-235">A konečně místo volání metody klienta z rozbočovače přímo, `Broadcaster` třídy musí získat odkaz na aktuálně fungující `_hubContext` centrum.</span><span class="sxs-lookup"><span data-stu-id="72d2a-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="72d2a-236">Získá odkaz s `GlobalHost`.</span><span class="sxs-lookup"><span data-stu-id="72d2a-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="72d2a-237">Přidat plynulou animaci</span><span class="sxs-lookup"><span data-stu-id="72d2a-237">Add smooth animation</span></span>

<span data-ttu-id="72d2a-238">Aplikace je skoro dokončená, ale můžeme udělat ještě jedno zlepšení.</span><span class="sxs-lookup"><span data-stu-id="72d2a-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="72d2a-239">Aplikace přesune obrazec na klientovi v reakci na zprávy serveru.</span><span class="sxs-lookup"><span data-stu-id="72d2a-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="72d2a-240">Místo nastavování pozice obrazce k novému umístění, které je zadáno serverem, použijte funkci `animate` knihovny uživatelského rozhraní JQuery.</span><span class="sxs-lookup"><span data-stu-id="72d2a-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="72d2a-241">Může obrazec plynule přemísťovat mezi aktuální a novou pozicí.</span><span class="sxs-lookup"><span data-stu-id="72d2a-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="72d2a-242">Aktualizujte metodu `updateShape` klienta ve výchozím souboru *. html* tak, aby vypadala jako zvýrazněný kód:</span><span class="sxs-lookup"><span data-stu-id="72d2a-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="72d2a-243">Kliknutím na tlačítko Přehrát spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="72d2a-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="72d2a-244">Zkopírujte adresu URL stránky.</span><span class="sxs-lookup"><span data-stu-id="72d2a-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="72d2a-245">Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.</span><span class="sxs-lookup"><span data-stu-id="72d2a-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="72d2a-246">Přetáhněte tvar v jednom z oken prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="72d2a-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="72d2a-247">Pohyb tvaru v druhém okně se zobrazuje méně Jerky.</span><span class="sxs-lookup"><span data-stu-id="72d2a-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="72d2a-248">Aplikace interpoluje svůj pohyb v čase, ale nenastavuje se jednou pro příchozí zprávu.</span><span class="sxs-lookup"><span data-stu-id="72d2a-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="72d2a-249">Tento kód přesune obrazec ze starého umístění do nového.</span><span class="sxs-lookup"><span data-stu-id="72d2a-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="72d2a-250">Server dává pozici tvaru v průběhu intervalu animace.</span><span class="sxs-lookup"><span data-stu-id="72d2a-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="72d2a-251">V tomto případě je to 100 milisekund.</span><span class="sxs-lookup"><span data-stu-id="72d2a-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="72d2a-252">Aplikace vymaže všechny předchozí animace běžící na tvaru před zahájením nové animace.</span><span class="sxs-lookup"><span data-stu-id="72d2a-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="72d2a-253">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="72d2a-253">Get the code</span></span>

[<span data-ttu-id="72d2a-254">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="72d2a-254">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a><span data-ttu-id="72d2a-255">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="72d2a-255">Additional resources</span></span>

<span data-ttu-id="72d2a-256">Paradigmata komunikace, o které jste se dozvěděli, je užitečná při vývoji online her a dalších simulací, jako [je hra programu pro seznámení vytvořená pomocí nástroje Signal](https://shootr.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="72d2a-256">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="72d2a-257">Další informace o signalizaci naleznete v následujících zdrojích informací:</span><span class="sxs-lookup"><span data-stu-id="72d2a-257">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="72d2a-258">Projekt signálu</span><span class="sxs-lookup"><span data-stu-id="72d2a-258">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="72d2a-259">GitHub a ukázky signálů</span><span class="sxs-lookup"><span data-stu-id="72d2a-259">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="72d2a-260">Wiki signálu</span><span class="sxs-lookup"><span data-stu-id="72d2a-260">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="72d2a-261">Další kroky</span><span class="sxs-lookup"><span data-stu-id="72d2a-261">Next steps</span></span>

<span data-ttu-id="72d2a-262">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="72d2a-262">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72d2a-263">Nastavení projektu</span><span class="sxs-lookup"><span data-stu-id="72d2a-263">Set up the project</span></span>
> * <span data-ttu-id="72d2a-264">Vytvoření základní aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-264">Created the base application</span></span>
> * <span data-ttu-id="72d2a-265">Namapováno na centrum při spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="72d2a-265">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="72d2a-266">Přidání klienta</span><span class="sxs-lookup"><span data-stu-id="72d2a-266">Added the client</span></span>
> * <span data-ttu-id="72d2a-267">Aplikace byla spuštěna</span><span class="sxs-lookup"><span data-stu-id="72d2a-267">Ran the app</span></span>
> * <span data-ttu-id="72d2a-268">Přidala se smyčka klienta.</span><span class="sxs-lookup"><span data-stu-id="72d2a-268">Added the client loop</span></span>
> * <span data-ttu-id="72d2a-269">Přidání smyčky serveru</span><span class="sxs-lookup"><span data-stu-id="72d2a-269">Added the server loop</span></span>
> * <span data-ttu-id="72d2a-270">Přidání plynulé animace</span><span class="sxs-lookup"><span data-stu-id="72d2a-270">Added smooth animation</span></span>

<span data-ttu-id="72d2a-271">V dalším článku se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET Signal 2 k poskytování funkcí všesměrového vysílání serveru.</span><span class="sxs-lookup"><span data-stu-id="72d2a-271">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="72d2a-272">Signál 2 a všesměrové vysílání serveru</span><span class="sxs-lookup"><span data-stu-id="72d2a-272">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)