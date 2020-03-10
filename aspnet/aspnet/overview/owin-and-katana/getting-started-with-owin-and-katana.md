---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: Začínáme s OWIN a Katana | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584670"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="72df9-102">Začínáme se specifikací OWIN a sadou Katana</span><span class="sxs-lookup"><span data-stu-id="72df9-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="72df9-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="72df9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="72df9-104">[Open Web Interface for .NET (Owin)](http://owin.org/) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="72df9-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="72df9-105">Díky oddělení webového serveru od aplikace OWIN usnadňuje vytváření middlewaru pro vývoj webů .NET.</span><span class="sxs-lookup"><span data-stu-id="72df9-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="72df9-106">OWIN také usnadňuje portování webových aplikací jiným hostitelům&#8212;, jako je například samoobslužné hostování ve službě systému Windows nebo v jiném procesu.</span><span class="sxs-lookup"><span data-stu-id="72df9-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="72df9-107">OWIN je specifikace ve vlastnictví komunity, nikoli implementace.</span><span class="sxs-lookup"><span data-stu-id="72df9-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="72df9-108">Projekt Katana je sada open source OWIN komponent vyvinutých společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="72df9-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="72df9-109">Obecný přehled obou OWIN a Katana najdete v tématu [Přehled projektu Katana](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="72df9-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="72df9-110">V tomto článku přejdete přímo do kódu, abyste mohli začít.</span><span class="sxs-lookup"><span data-stu-id="72df9-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="72df9-111">V tomto kurzu se používá [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), ale můžete také použít Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="72df9-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="72df9-112">V aplikaci Visual Studio 2012 se liší několik kroků, které jsou uvedeny níže.</span><span class="sxs-lookup"><span data-stu-id="72df9-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="72df9-113">OWIN hostitele ve službě IIS</span><span class="sxs-lookup"><span data-stu-id="72df9-113">Host OWIN in IIS</span></span>

<span data-ttu-id="72df9-114">V této části budeme hostovat OWIN ve službě IIS.</span><span class="sxs-lookup"><span data-stu-id="72df9-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="72df9-115">Tato možnost nabízí flexibilitu a možnosti vytváření kanálu OWIN spolu s vyspělou sadou funkcí IIS.</span><span class="sxs-lookup"><span data-stu-id="72df9-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="72df9-116">Pomocí této možnosti se aplikace OWIN spustí v kanálu žádosti ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="72df9-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="72df9-117">Nejprve vytvořte nový projekt webové aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="72df9-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="72df9-118">(V aplikaci Visual Studio 2012 použijte prázdný typ projektu webové aplikace ASP.NET.)</span><span class="sxs-lookup"><span data-stu-id="72df9-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="72df9-119">V dialogovém okně **Nový projekt ASP.NET** vyberte **prázdnou** šablonu.</span><span class="sxs-lookup"><span data-stu-id="72df9-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="72df9-120">Přidání balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="72df9-120">Add NuGet Packages</span></span>

<span data-ttu-id="72df9-121">Dále přidejte požadované balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="72df9-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="72df9-122">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="72df9-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="72df9-123">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="72df9-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="72df9-124">Přidat třídu po spuštění</span><span class="sxs-lookup"><span data-stu-id="72df9-124">Add a Startup Class</span></span>

<span data-ttu-id="72df9-125">Dále přidejte třídu pro spuštění OWIN.</span><span class="sxs-lookup"><span data-stu-id="72df9-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="72df9-126">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost **Přidat**a pak vyberte možnost **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="72df9-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="72df9-127">V dialogovém okně **Přidat novou položku** vyberte **Owin třídy po spuštění**.</span><span class="sxs-lookup"><span data-stu-id="72df9-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="72df9-128">Další informace o konfiguraci třídy po spuštění naleznete v tématu [Owin Startup Class Detection](owin-startup-class-detection.md).</span><span class="sxs-lookup"><span data-stu-id="72df9-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="72df9-129">Do metody `Startup1.Configuration` přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="72df9-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="72df9-130">Tento kód přidá do kanálu OWIN jednoduchý objekt middleware, který je implementován jako funkce, která přijímá instanci **Microsoft. Owin. IOwinContext** .</span><span class="sxs-lookup"><span data-stu-id="72df9-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="72df9-131">Když server přijme požadavek HTTP, kanál OWIN vyvolá middleware.</span><span class="sxs-lookup"><span data-stu-id="72df9-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="72df9-132">Middleware nastaví typ obsahu pro odpověď a zapíše text odpovědi.</span><span class="sxs-lookup"><span data-stu-id="72df9-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="72df9-133">Šablona třídy po spuštění OWIN je k dispozici v Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="72df9-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="72df9-134">Pokud používáte Visual Studio 2012, stačí přidat novou prázdnou třídu s názvem `Startup1`a vložit do následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="72df9-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="72df9-135">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="72df9-135">Run the Application</span></span>

<span data-ttu-id="72df9-136">Stisknutím klávesy F5 spusťte ladění.</span><span class="sxs-lookup"><span data-stu-id="72df9-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="72df9-137">Visual Studio otevře okno prohlížeče, ve kterém se `http://localhost:*port*/`.</span><span class="sxs-lookup"><span data-stu-id="72df9-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="72df9-138">Stránka by měla vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="72df9-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="72df9-139">OWIN samostatného hostitele v konzolové aplikaci</span><span class="sxs-lookup"><span data-stu-id="72df9-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="72df9-140">Tuto aplikaci je snadné převést z hostování služby IIS na samoobslužné hostování ve vlastním procesu.</span><span class="sxs-lookup"><span data-stu-id="72df9-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="72df9-141">Při hostování služby IIS funguje služba IIS jako server HTTP i proces, který hostuje službu.</span><span class="sxs-lookup"><span data-stu-id="72df9-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="72df9-142">V případě samoobslužného hostování aplikace vytvoří proces a jako server HTTP používá třídu **HttpListener** .</span><span class="sxs-lookup"><span data-stu-id="72df9-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="72df9-143">V aplikaci Visual Studio vytvořte novou konzolovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="72df9-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="72df9-144">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="72df9-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="72df9-145">Přidejte třídu `Startup1` z části 1 tohoto kurzu do projektu.</span><span class="sxs-lookup"><span data-stu-id="72df9-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="72df9-146">Tuto třídu nemusíte měnit.</span><span class="sxs-lookup"><span data-stu-id="72df9-146">You don't need to modify this class.</span></span>

<span data-ttu-id="72df9-147">Implementujte metodu `Main` aplikace následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="72df9-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="72df9-148">Když spustíte konzolovou aplikaci, server začne naslouchat `http://localhost:9000`.</span><span class="sxs-lookup"><span data-stu-id="72df9-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="72df9-149">Pokud ve webovém prohlížeči přejdete na tuto adresu, zobrazí se stránka "Hello World".</span><span class="sxs-lookup"><span data-stu-id="72df9-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="72df9-150">Přidat diagnostiku OWIN</span><span class="sxs-lookup"><span data-stu-id="72df9-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="72df9-151">Balíček Microsoft. Owin. Diagnostics obsahuje middleware, který zachycuje neošetřené výjimky a zobrazuje stránku HTML s podrobnostmi o chybě.</span><span class="sxs-lookup"><span data-stu-id="72df9-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="72df9-152">Tato stránka funguje podobně jako na chybové stránce ASP.NET, která se někdy označuje jako "[žlutá obrazovka smrti](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span><span class="sxs-lookup"><span data-stu-id="72df9-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="72df9-153">Podobně jako u YSOD je chybová stránka Katana užitečná při vývoji, ale je dobrým zvykem ji zakázat v provozním režimu.</span><span class="sxs-lookup"><span data-stu-id="72df9-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="72df9-154">Chcete-li nainstalovat balíček diagnostiky do projektu, zadejte následující příkaz v okně konzoly Správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="72df9-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="72df9-155">Změňte kód v metodě `Startup1.Configuration` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="72df9-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="72df9-156">Nyní použijte kombinaci kláves CTRL + F5 ke spuštění aplikace bez ladění, aby se Visual Studio při výjimce nepřerušilo.</span><span class="sxs-lookup"><span data-stu-id="72df9-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="72df9-157">Aplikace se chová stejně jako předtím, dokud nepřejdete na `http://localhost/fail`, kde aplikace vyvolá výjimku.</span><span class="sxs-lookup"><span data-stu-id="72df9-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="72df9-158">Middleware chybové stránky bude zachytit výjimku a zobrazit stránku HTML s informacemi o chybě.</span><span class="sxs-lookup"><span data-stu-id="72df9-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="72df9-159">Kliknutím na karty můžete zobrazit zásobník, řetězec dotazu, soubory cookie, hlavičku požadavku a proměnné prostředí OWIN.</span><span class="sxs-lookup"><span data-stu-id="72df9-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="72df9-160">Další kroky</span><span class="sxs-lookup"><span data-stu-id="72df9-160">Next Steps</span></span>

- [<span data-ttu-id="72df9-161">Rozpoznání spouštěcí třídy OWIN</span><span class="sxs-lookup"><span data-stu-id="72df9-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="72df9-162">Použití OWIN k samoobslužnému hostování ASP.NET webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="72df9-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="72df9-163">Použití OWIN k samočinnému hostování signálu</span><span class="sxs-lookup"><span data-stu-id="72df9-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
