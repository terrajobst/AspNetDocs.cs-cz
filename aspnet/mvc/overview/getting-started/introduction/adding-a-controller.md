---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: Přidání kontroleru | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810774"
---
# <a name="adding-a-controller"></a><span data-ttu-id="02067-102">Přidání kontroleru</span><span class="sxs-lookup"><span data-stu-id="02067-102">Adding a Controller</span></span>

<span data-ttu-id="02067-103">od [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="02067-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="02067-104">MVC představuje *kontroler-View-Controller*.</span><span class="sxs-lookup"><span data-stu-id="02067-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="02067-105">MVC je vzor pro vývoj aplikací, které jsou dobře architektované, testovatelné a snadno udržovatelnější.</span><span class="sxs-lookup"><span data-stu-id="02067-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="02067-106">Aplikace založené na MVC obsahují:</span><span class="sxs-lookup"><span data-stu-id="02067-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="02067-107">Odels **M** : Třídy, které reprezentují data aplikace a používají logiku ověřování k vyhodnocování obchodních pravidel pro tato data.</span><span class="sxs-lookup"><span data-stu-id="02067-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="02067-108">**V** iews: Soubory šablon, které vaše aplikace používá k dynamickému generování odpovědí HTML.</span><span class="sxs-lookup"><span data-stu-id="02067-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="02067-109">Ontrollers **jazyka C** : Třídy, které zpracovávají příchozí požadavky prohlížeče, načítají data modelu a pak určují šablony zobrazení, které vracejí odpověď prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="02067-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="02067-110">Pokryjeme všechny tyto koncepty v této sérii kurzů a ukážeme vám, jak je používat k sestavení aplikace.</span><span class="sxs-lookup"><span data-stu-id="02067-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="02067-111">Pojďme začít vytvořením třídy Controller.</span><span class="sxs-lookup"><span data-stu-id="02067-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="02067-112">V **Průzkumník řešení**klikněte pravým tlačítkem na složku Controllers a pak klikněte na **Přidat**a pak na **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="02067-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="02067-113">V dialogovém okně **Přidat vygenerované uživatelské rozhraní** klikněte na kontroler **MVC 5 – prázdné**a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="02067-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="02067-114">Pojmenujte nový kontroler "HelloWorldController" a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="02067-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![Přidat kontroler](adding-a-controller/_static/image3.png)

<span data-ttu-id="02067-116">Všimněte si, že **Průzkumník řešení** , že se vytvořil nový soubor s názvem *HelloWorldController.cs* a novou složkou *Views\HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="02067-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="02067-117">Kontroler je otevřený v integrovaném vývojovém prostředí.</span><span class="sxs-lookup"><span data-stu-id="02067-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="02067-118">Obsah souboru nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="02067-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="02067-119">Metody kontroleru vrátí jako příklad řetězec HTML.</span><span class="sxs-lookup"><span data-stu-id="02067-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="02067-120">Kontroler má název `HelloWorldController` a první metoda je pojmenována. `Index`</span><span class="sxs-lookup"><span data-stu-id="02067-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="02067-121">Pojďme to vyvolat z prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="02067-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="02067-122">Spusťte aplikaci (stiskněte klávesu F5 nebo CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="02067-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="02067-123">V prohlížeči přidejte &quot;HelloWorld&quot; k cestě na adresním řádku.</span><span class="sxs-lookup"><span data-stu-id="02067-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="02067-124">(Například na ilustraci níže je to `http://localhost:1234/HelloWorld.`) stránka v prohlížeči bude vypadat jako na následujícím snímku obrazovky.</span><span class="sxs-lookup"><span data-stu-id="02067-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="02067-125">V metodě výše kód vrátil řetězec přímo.</span><span class="sxs-lookup"><span data-stu-id="02067-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="02067-126">Dozvěděli jste systém, aby vracel jenom určitý kód HTML a byl.</span><span class="sxs-lookup"><span data-stu-id="02067-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="02067-127">ASP.NET MVC vyvolá různé třídy kontroleru (a v rámci nich různé metody akcí) v závislosti na příchozí adrese URL.</span><span class="sxs-lookup"><span data-stu-id="02067-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="02067-128">Výchozí logika směrování adres URL, kterou používá ASP.NET MVC, používá formát podobný tomuto: k určení kódu, který se má vyvolat:</span><span class="sxs-lookup"><span data-stu-id="02067-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="02067-129">Formát pro směrování nastavíte v souboru *Start/\_RouteConfig. cs aplikace* .</span><span class="sxs-lookup"><span data-stu-id="02067-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="02067-130">Když aplikaci spustíte a nezadáte žádné segmenty adresy URL, použije se výchozí řídicí řadič a metoda "index" uvedená v části Defaults výše uvedeného kódu.</span><span class="sxs-lookup"><span data-stu-id="02067-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="02067-131">První část adresy URL určuje třídu kontroleru, která se má spustit.</span><span class="sxs-lookup"><span data-stu-id="02067-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="02067-132">Takže se */HelloWorld* mapuje na `HelloWorldController` třídu.</span><span class="sxs-lookup"><span data-stu-id="02067-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="02067-133">Druhá část adresy URL určuje metodu Action pro třídu, která má být provedena.</span><span class="sxs-lookup"><span data-stu-id="02067-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="02067-134">*/HelloWorld/index* by proto způsobila `Index` , že se `HelloWorldController` metoda třídy spustí.</span><span class="sxs-lookup"><span data-stu-id="02067-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="02067-135">Všimněte si, že jsme museli procházet na */HelloWorld* a `Index` metoda se ve výchozím nastavení použila.</span><span class="sxs-lookup"><span data-stu-id="02067-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="02067-136">Důvodem je, že metoda s `Index` názvem je výchozí metoda, která bude volána na řadiči, pokud není explicitně určena.</span><span class="sxs-lookup"><span data-stu-id="02067-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="02067-137">Třetí část segmentu adresy URL ( `Parameters`) je určena pro data trasy.</span><span class="sxs-lookup"><span data-stu-id="02067-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="02067-138">Později se v tomto kurzu zobrazí data o trasách.</span><span class="sxs-lookup"><span data-stu-id="02067-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="02067-139">Přejděte do `http://localhost:xxxx/HelloWorld/Welcome`.</span><span class="sxs-lookup"><span data-stu-id="02067-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="02067-140">Metoda se spustí a vrátí řetězec &quot;, který je to metoda akce Welcome... `Welcome` &quot;.</span><span class="sxs-lookup"><span data-stu-id="02067-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="02067-141">Výchozí mapování MVC je `/[Controller]/[ActionName]/[Parameters]`.</span><span class="sxs-lookup"><span data-stu-id="02067-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="02067-142">Pro tuto adresu URL kontroler je `HelloWorld` a `Welcome` je metodou Action.</span><span class="sxs-lookup"><span data-stu-id="02067-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="02067-143">Ještě jste nepoužili `[Parameters]` část této adresy URL.</span><span class="sxs-lookup"><span data-stu-id="02067-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="02067-144">Pojďme tento příklad mírně upravit, abyste mohli předat nějaké informace o parametrech z adresy URL do kontroleru (například */HelloWorld/Welcome? Name = Scott&amp;numtimes = 4*).</span><span class="sxs-lookup"><span data-stu-id="02067-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="02067-145">`Welcome` Změňte metodu tak, aby zahrnovala dva parametry, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="02067-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="02067-146">Všimněte si, že kód používá C# funkci volitelného parametru k označení toho, `numTimes` že parametr by měl být nastaven na hodnotu 1, pokud není pro tento parametr předána žádná hodnota.</span><span class="sxs-lookup"><span data-stu-id="02067-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="02067-147">Poznámka k zabezpečení: Výše uvedený kód používá [HttpUtility. HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) k ochraně aplikace před škodlivým vstupem (konkrétně JavaScript).</span><span class="sxs-lookup"><span data-stu-id="02067-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="02067-148">Další informace najdete v části [jak: Chraňte proti zneužití skriptů ve webové aplikaci použitím kódování HTML v řetězcích](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="02067-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="02067-149">Spusťte aplikaci a přejděte k ukázkové adrese URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span><span class="sxs-lookup"><span data-stu-id="02067-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="02067-150">Můžete zkusit použít jiné hodnoty pro `name` a `numtimes` v adrese URL.</span><span class="sxs-lookup"><span data-stu-id="02067-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="02067-151">[Systém vazby modelu ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automaticky mapuje pojmenované parametry z řetězce dotazu v adresním řádku na parametry v metodě.</span><span class="sxs-lookup"><span data-stu-id="02067-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="02067-152">V ukázce výše se nepoužívá segment adresy URL `Parameters`() `name` , parametry a `numTimes` jsou předány jako [řetězce dotazu](http://en.wikipedia.org/wiki/Query_string).</span><span class="sxs-lookup"><span data-stu-id="02067-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="02067-153">Okně?</span><span class="sxs-lookup"><span data-stu-id="02067-153">The ?</span></span> <span data-ttu-id="02067-154">(otazník) na výše uvedené adrese URL je oddělovač a následují řetězce dotazů.</span><span class="sxs-lookup"><span data-stu-id="02067-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="02067-155">&amp; Znak odděluje řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="02067-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="02067-156">Metodu Welcome nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="02067-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="02067-157">Spusťte aplikaci a zadejte následující adresu URL:`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="02067-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="02067-158">Tentokrát, kdy třetí segment `ID.` adresy URL odpovídá parametru `Welcome` trasy, metoda Action obsahuje parametr (`ID` `RegisterRoutes` ), který se shoduje se specifikací adresy URL v metodě.</span><span class="sxs-lookup"><span data-stu-id="02067-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="02067-159">V aplikacích ASP.NET MVC je obvyklejší předávat parametry jako údaje o trasách (jako je to u ID výše), než je předáte jako řetězce dotazů.</span><span class="sxs-lookup"><span data-stu-id="02067-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="02067-160">Můžete také přidat trasu, která bude `name` předat parametry i `numtimes` v jako směrovat data v adrese URL.</span><span class="sxs-lookup"><span data-stu-id="02067-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="02067-161">Do souboru *App\_Start\RouteConfig.cs* přidejte trasu "Hello":</span><span class="sxs-lookup"><span data-stu-id="02067-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="02067-162">Spusťte aplikaci a přejděte na `/localhost:XXX/HelloWorld/Welcome/Scott/3`adresu.</span><span class="sxs-lookup"><span data-stu-id="02067-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="02067-163">Pro mnoho aplikací MVC funguje výchozí trasa správně.</span><span class="sxs-lookup"><span data-stu-id="02067-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="02067-164">Později v tomto kurzu se dozvíte, jak data předávat pomocí pořadače modelů, a nebudete muset měnit výchozí trasu.</span><span class="sxs-lookup"><span data-stu-id="02067-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="02067-165">V těchto příkladech kontroler provedl &quot;součást VC&quot; v MVC – to znamená, že zobrazení a kontroler funguje.</span><span class="sxs-lookup"><span data-stu-id="02067-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="02067-166">Kontroler přímo vrací HTML.</span><span class="sxs-lookup"><span data-stu-id="02067-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="02067-167">Obvykle nechcete, aby řadiče vracely kód HTML přímo, protože to může být velmi nenáročné na kód.</span><span class="sxs-lookup"><span data-stu-id="02067-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="02067-168">Místo toho obvykle použijete samostatný soubor šablony zobrazení, který vám pomůžeme vygenerovat odpověď HTML.</span><span class="sxs-lookup"><span data-stu-id="02067-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="02067-169">Pojďme se podívat na to, jak to můžeme udělat.</span><span class="sxs-lookup"><span data-stu-id="02067-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="02067-170">[Předchozí](getting-started.md)Další
> [](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="02067-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
