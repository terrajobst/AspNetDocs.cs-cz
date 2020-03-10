---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: Aplikace Signal test jednotek | Microsoft Docs
author: bradygaster
description: Tento článek popisuje, jak používat funkce testování částí nástroje Signaler 2,0.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578671"
---
# <a name="unit-testing-signalr-applications"></a><span data-ttu-id="544a5-103">Testování jednotek aplikace knihovnou SignalR</span><span class="sxs-lookup"><span data-stu-id="544a5-103">Unit Testing SignalR Applications</span></span>

<span data-ttu-id="544a5-104">Po [Fletcheru](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="544a5-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="544a5-105">Tento článek popisuje použití funkcí testování částí v Signaler 2.</span><span class="sxs-lookup"><span data-stu-id="544a5-105">This article describes using the Unit Testing features of SignalR 2.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="544a5-106">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="544a5-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="544a5-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="544a5-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="544a5-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="544a5-108">.NET 4.5</span></span>
> - <span data-ttu-id="544a5-109">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="544a5-109">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="544a5-110">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="544a5-110">Questions and comments</span></span>
>
> <span data-ttu-id="544a5-111">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="544a5-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="544a5-112">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="544a5-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="544a5-113">Aplikace signalizace testování částí</span><span class="sxs-lookup"><span data-stu-id="544a5-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="544a5-114">Pomocí funkcí testování částí ve službě Signaler 2 můžete vytvořit testy jednotek pro vaši aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="544a5-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="544a5-115">Signal 2 obsahuje rozhraní [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) , které se dá použít k vytvoření objektu pro simulaci vašich metod rozbočovače pro účely testování.</span><span class="sxs-lookup"><span data-stu-id="544a5-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="544a5-116">V této části přidáte testy jednotek pro aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) pomocí [XUnit.NET](https://github.com/xunit/xunit) a [MOQ](https://github.com/Moq/moq4).</span><span class="sxs-lookup"><span data-stu-id="544a5-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="544a5-117">XUnit.net se bude používat k řízení testu. MOQ se použije k vytvoření objektu [makety](http://en.wikipedia.org/wiki/Mock_object) pro testování.</span><span class="sxs-lookup"><span data-stu-id="544a5-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="544a5-118">V případě potřeby lze použít jiné rozhraní pro návrhy. [NSubstitute](http://nsubstitute.github.io/) je také dobrou volbou.</span><span class="sxs-lookup"><span data-stu-id="544a5-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="544a5-119">V tomto kurzu se dozvíte, jak nastavit objekt kresby dvěma způsoby: nejprve pomocí objektu `dynamic` (představený v .NET Framework 4) a s použitím rozhraní.</span><span class="sxs-lookup"><span data-stu-id="544a5-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="544a5-120">Obsah</span><span class="sxs-lookup"><span data-stu-id="544a5-120">Contents</span></span>

<span data-ttu-id="544a5-121">Tento kurz obsahuje následující oddíly.</span><span class="sxs-lookup"><span data-stu-id="544a5-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="544a5-122">Testování částí s dynamickým</span><span class="sxs-lookup"><span data-stu-id="544a5-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="544a5-123">Testování částí podle typu</span><span class="sxs-lookup"><span data-stu-id="544a5-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="544a5-124">Testování částí s dynamickým</span><span class="sxs-lookup"><span data-stu-id="544a5-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="544a5-125">V této části přidáte test jednotek pro aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) pomocí dynamického objektu.</span><span class="sxs-lookup"><span data-stu-id="544a5-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="544a5-126">Nainstalujte [rozšíření XUnit Runner](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="544a5-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="544a5-127">Buď dokončete [kurz Začínáme](../getting-started/tutorial-getting-started-with-signalr.md), nebo si stáhněte dokončenou aplikaci z [Galerie kódu na webu MSDN](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span><span class="sxs-lookup"><span data-stu-id="544a5-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="544a5-128">Pokud používáte aplikaci Začínáme ke stažení, otevřete **konzolu Správce balíčků** a kliknutím na **obnovit** přidejte do projektu balíček signalizace.</span><span class="sxs-lookup"><span data-stu-id="544a5-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![Obnovit balíčky](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="544a5-130">Přidejte projekt do řešení pro testování částí.</span><span class="sxs-lookup"><span data-stu-id="544a5-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="544a5-131">Klikněte pravým tlačítkem na své řešení v **Průzkumník řešení** a vyberte **Přidat**, **Nový projekt...** . V **C#** uzlu vyberte uzel **Windows** .</span><span class="sxs-lookup"><span data-stu-id="544a5-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="544a5-132">Vyberte možnost **Knihovna tříd**.</span><span class="sxs-lookup"><span data-stu-id="544a5-132">Select **Class Library**.</span></span> <span data-ttu-id="544a5-133">Pojmenujte nový projekt **TestLibrary** a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="544a5-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![Vytvořit knihovnu testů](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="544a5-135">Přidejte odkaz do projektu knihovny testů do projektu SignalRChat.</span><span class="sxs-lookup"><span data-stu-id="544a5-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="544a5-136">Klikněte pravým tlačítkem na projekt **TestLibrary** a vyberte **Přidat**, **odkaz.** ... V uzlu **řešení** vyberte uzel **projekty** a zaškrtněte **SignalRChat**.</span><span class="sxs-lookup"><span data-stu-id="544a5-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="544a5-137">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="544a5-137">Click **OK**.</span></span>

    ![Přidat odkaz na projekt](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="544a5-139">Přidejte do projektu **TestLibrary** balíčky signálu, MOQ a XUnit.</span><span class="sxs-lookup"><span data-stu-id="544a5-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="544a5-140">V **konzole správce balíčků**nastavte výchozí rozevírací seznam **projektu** na **TestLibrary**.</span><span class="sxs-lookup"><span data-stu-id="544a5-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="544a5-141">V okně konzoly spusťte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="544a5-141">Run the following commands in the console window:</span></span>

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![Nainstalovat balíčky](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="544a5-143">Vytvořte testovací soubor.</span><span class="sxs-lookup"><span data-stu-id="544a5-143">Create the test file.</span></span> <span data-ttu-id="544a5-144">Klikněte pravým tlačítkem na projekt **TestLibrary** a klikněte na **Přidat...** , **Třída**.</span><span class="sxs-lookup"><span data-stu-id="544a5-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="544a5-145">Pojmenujte novou třídu **Tests.cs**.</span><span class="sxs-lookup"><span data-stu-id="544a5-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="544a5-146">Obsah Tests.cs nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="544a5-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="544a5-147">Ve výše uvedeném kódu je testovací klient vytvořen pomocí objektu `Mock` z knihovny [MOQ](https://github.com/Moq/moq4) , typu [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in signal 2,1, přiřazení `dynamic` pro parametr typu.) Rozhraní `IHubCallerConnectionContext` je objekt proxy, pomocí kterého jste na klientovi vyvolali metody.</span><span class="sxs-lookup"><span data-stu-id="544a5-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="544a5-148">Funkce `broadcastMessage` je pak definována pro maketa klienta, aby ji bylo možné volat pomocí `ChatHub` třídy.</span><span class="sxs-lookup"><span data-stu-id="544a5-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="544a5-149">Testovací modul pak zavolá metodu `Send` třídy `ChatHub`, která zase volá napodobnou `broadcastMessage` funkci.</span><span class="sxs-lookup"><span data-stu-id="544a5-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="544a5-150">Sestavte řešení stisknutím klávesy **F6**.</span><span class="sxs-lookup"><span data-stu-id="544a5-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="544a5-151">Spusťte Jednotkový test.</span><span class="sxs-lookup"><span data-stu-id="544a5-151">Run the unit test.</span></span> <span data-ttu-id="544a5-152">V aplikaci Visual Studio vyberte **test**, **Windows**, **Průzkumník testů**.</span><span class="sxs-lookup"><span data-stu-id="544a5-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="544a5-153">V okně Průzkumník testů klikněte pravým tlačítkem na **HubsAreMockableViaDynamic** a vyberte **Spustit vybrané testy**.</span><span class="sxs-lookup"><span data-stu-id="544a5-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Průzkumník testů](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="544a5-155">Ověřte, zda byl test úspěšný, kontrolou dolního podokna v okně Průzkumníka testů.</span><span class="sxs-lookup"><span data-stu-id="544a5-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="544a5-156">V okně se zobrazí, že test proběhl úspěšně.</span><span class="sxs-lookup"><span data-stu-id="544a5-156">The window will show that the test passed.</span></span>

    ![Test byl úspěšný](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="544a5-158">Testování částí podle typu</span><span class="sxs-lookup"><span data-stu-id="544a5-158">Unit testing by type</span></span>

<span data-ttu-id="544a5-159">V této části přidáte test pro aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) pomocí rozhraní, které obsahuje metodu, která má být testována.</span><span class="sxs-lookup"><span data-stu-id="544a5-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="544a5-160">Proveďte kroky 1-7 v části [testování částí pomocí dynamického](#dynamic) kurzu výše.</span><span class="sxs-lookup"><span data-stu-id="544a5-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="544a5-161">Obsah Tests.cs nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="544a5-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="544a5-162">Ve výše uvedeném kódu se vytvoří rozhraní definující signaturu `broadcastMessage` metody, pro kterou testovací modul vytvoří strojového klienta.</span><span class="sxs-lookup"><span data-stu-id="544a5-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="544a5-163">Napodobný klient je pak vytvořen pomocí objektu `Mock` typu [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in Signal 2,1, přiřazení `dynamic` parametru typu.) Rozhraní `IHubCallerConnectionContext` je objekt proxy, pomocí kterého jste na klientovi vyvolali metody.</span><span class="sxs-lookup"><span data-stu-id="544a5-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="544a5-164">Test poté vytvoří instanci `ChatHub`a poté vytvoří maketnou verzi metody `broadcastMessage`, která je zase vyvolána voláním metody `Send` na rozbočovači.</span><span class="sxs-lookup"><span data-stu-id="544a5-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="544a5-165">Sestavte řešení stisknutím klávesy **F6**.</span><span class="sxs-lookup"><span data-stu-id="544a5-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="544a5-166">Spusťte Jednotkový test.</span><span class="sxs-lookup"><span data-stu-id="544a5-166">Run the unit test.</span></span> <span data-ttu-id="544a5-167">V aplikaci Visual Studio vyberte **test**, **Windows**, **Průzkumník testů**.</span><span class="sxs-lookup"><span data-stu-id="544a5-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="544a5-168">V okně Průzkumník testů klikněte pravým tlačítkem na **HubsAreMockableViaDynamic** a vyberte **Spustit vybrané testy**.</span><span class="sxs-lookup"><span data-stu-id="544a5-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Průzkumník testů](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="544a5-170">Ověřte, zda byl test úspěšný, kontrolou dolního podokna v okně Průzkumníka testů.</span><span class="sxs-lookup"><span data-stu-id="544a5-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="544a5-171">V okně se zobrazí, že test proběhl úspěšně.</span><span class="sxs-lookup"><span data-stu-id="544a5-171">The window will show that the test passed.</span></span>

    ![Test byl úspěšný](unit-testing-signalr-applications/_static/image8.png)
