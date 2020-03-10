---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: Povolení žádostí o více zdrojů v ASP.NET webovém rozhraní API 2 | Microsoft Docs
author: MikeWasson
description: Ukazuje, jak podporovat sdílení prostředků mezi zdroji (CORS) ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555704"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="503a3-103">Povolení žádostí mezi zdroji v ASP.NET webovém rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="503a3-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="503a3-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="503a3-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="503a3-105">Zabezpečení prohlížečů brání webovým stránkám v odesílání požadavků AJAX na jinou doménu.</span><span class="sxs-lookup"><span data-stu-id="503a3-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="503a3-106">Toto omezení se nazývá *zásady stejného původu*a brání škodlivému webu v čtení citlivých dat z jiné lokality.</span><span class="sxs-lookup"><span data-stu-id="503a3-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="503a3-107">V některých případech však můžete chtít povolit jiným webům volat vaše webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="503a3-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="503a3-108">[Sdílení prostředků mezi zdroji](http://www.w3.org/TR/cors/) (CORS) je standard W3C, který umožňuje serveru zmírnit zásady stejného zdroje.</span><span class="sxs-lookup"><span data-stu-id="503a3-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="503a3-109">Při použití CORS může server explicitně umožnit některé žádosti o více zdrojů a současně odmítat jiné.</span><span class="sxs-lookup"><span data-stu-id="503a3-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="503a3-110">CORS je bezpečnější a pružnější než u předchozích technik, jako je [JSONP](http://en.wikipedia.org/wiki/JSONP).</span><span class="sxs-lookup"><span data-stu-id="503a3-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="503a3-111">V tomto kurzu se dozvíte, jak ve vaší aplikaci webového rozhraní API povolit CORS.</span><span class="sxs-lookup"><span data-stu-id="503a3-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="503a3-112">Software použitý v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="503a3-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="503a3-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="503a3-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="503a3-114">Webové rozhraní API 2,2</span><span class="sxs-lookup"><span data-stu-id="503a3-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="503a3-115">Úvod</span><span class="sxs-lookup"><span data-stu-id="503a3-115">Introduction</span></span>

<span data-ttu-id="503a3-116">Tento kurz ukazuje podporu CORS ve webovém rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="503a3-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="503a3-117">Začneme vytvořením dvou ASP.NET projektů – One s názvem "WebService", který hostuje kontroler webového rozhraní API a druhý s názvem "webový klient", který volá webovou službu.</span><span class="sxs-lookup"><span data-stu-id="503a3-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="503a3-118">Vzhledem k tomu, že jsou tyto dvě aplikace hostovány v různých doménách, požadavek AJAX od WebClient na WebService je požadavek na více zdrojů.</span><span class="sxs-lookup"><span data-stu-id="503a3-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="503a3-119">Co je "stejný zdroj"?</span><span class="sxs-lookup"><span data-stu-id="503a3-119">What is "same origin"?</span></span>

<span data-ttu-id="503a3-120">Dvě adresy URL mají stejný původ, pokud mají totožná schémata, hostitele a porty.</span><span class="sxs-lookup"><span data-stu-id="503a3-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="503a3-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="503a3-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="503a3-122">Tyto dvě adresy URL mají stejný původ:</span><span class="sxs-lookup"><span data-stu-id="503a3-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="503a3-123">Tyto adresy URL mají jiný původ než předchozí dvě:</span><span class="sxs-lookup"><span data-stu-id="503a3-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="503a3-124">`http://example.net` – odlišná doména</span><span class="sxs-lookup"><span data-stu-id="503a3-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="503a3-125">`http://example.com:9000/foo.html` – jiný port</span><span class="sxs-lookup"><span data-stu-id="503a3-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="503a3-126">`https://example.com/foo.html` – odlišné schéma</span><span class="sxs-lookup"><span data-stu-id="503a3-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="503a3-127">`http://www.example.com/foo.html` – odlišná subdoména</span><span class="sxs-lookup"><span data-stu-id="503a3-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="503a3-128">Internet Explorer při porovnávání míst původu nebere v úvahu port.</span><span class="sxs-lookup"><span data-stu-id="503a3-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="503a3-129">Vytvoření projektu WebService</span><span class="sxs-lookup"><span data-stu-id="503a3-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="503a3-130">V této části se předpokládá, že už máte informace o tom, jak vytvářet projekty webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="503a3-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="503a3-131">Pokud ne, přečtěte si téma [Začínáme s webovým rozhraním API ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="503a3-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="503a3-132">Spusťte Visual Studio a vytvořte nový projekt **webové aplikace v ASP.NET (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="503a3-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="503a3-133">V dialogovém okně **Nová webová aplikace v ASP.NET** vyberte šablonu **prázdného** projektu.</span><span class="sxs-lookup"><span data-stu-id="503a3-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="503a3-134">V části **Přidat složky a základní reference pro**vyberte zaškrtávací políčko **webové rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="503a3-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Dialogové okno Nový projekt ASP.NET v aplikaci Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="503a3-136">Přidejte kontroler webového rozhraní API s názvem `TestController` s následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="503a3-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="503a3-137">Aplikaci můžete spustit místně nebo nasadit do Azure.</span><span class="sxs-lookup"><span data-stu-id="503a3-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="503a3-138">(Pro snímky obrazovky v tomto kurzu se aplikace nasadí do Azure App Service Web Apps.) Chcete-li ověřit, zda webové rozhraní API funguje, přejděte na adresu `http://hostname/api/test/`, kde *název hostitele* je doména, do které jste aplikaci nasadili.</span><span class="sxs-lookup"><span data-stu-id="503a3-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="503a3-139">Měl by se zobrazit text odpovědi &quot;GET: test Message&quot;.</span><span class="sxs-lookup"><span data-stu-id="503a3-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![Webový prohlížeč zobrazující zkušební zprávu](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="503a3-141">Vytvoření projektu WebClient</span><span class="sxs-lookup"><span data-stu-id="503a3-141">Create the WebClient project</span></span>

1. <span data-ttu-id="503a3-142">Vytvořte další projekt **webové aplikace v ASP.NET (.NET Framework)** a vyberte šablonu projektu **MVC** .</span><span class="sxs-lookup"><span data-stu-id="503a3-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="503a3-143">Volitelně můžete vybrat možnost **změnit ověřování** > **bez ověřování**.</span><span class="sxs-lookup"><span data-stu-id="503a3-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="503a3-144">Pro tento kurz nepotřebujete ověřování.</span><span class="sxs-lookup"><span data-stu-id="503a3-144">You don't need authentication for this tutorial.</span></span>

   ![Šablona MVC v dialogovém okně Nový projekt ASP.NET v aplikaci Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="503a3-146">V **Průzkumník řešení**otevřete *zobrazení souborů/domů/index. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="503a3-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="503a3-147">Nahraďte kód v tomto souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="503a3-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="503a3-148">Pro proměnnou *serviceUrl* použijte identifikátor URI aplikace WebService.</span><span class="sxs-lookup"><span data-stu-id="503a3-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="503a3-149">Spusťte aplikaci webového klienta lokálně nebo ji publikujte na jiném webu.</span><span class="sxs-lookup"><span data-stu-id="503a3-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="503a3-150">Po kliknutí na tlačítko vyzkoušet se odešle požadavek AJAX do aplikace WebService pomocí metody HTTP uvedené v rozevíracím seznamu (GET, POST nebo PUT).</span><span class="sxs-lookup"><span data-stu-id="503a3-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="503a3-151">To vám umožní prošetřit různé požadavky na více zdrojů.</span><span class="sxs-lookup"><span data-stu-id="503a3-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="503a3-152">V současné době aplikace webové služby nepodporuje CORS, takže pokud kliknete na tlačítko, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="503a3-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![V prohlížeči se chyba "vyzkoušet IT"](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="503a3-154">Pokud sledujete provoz protokolu HTTP v nástroji jako [Fiddler](https://www.telerik.com/fiddler), uvidíte, že prohlížeč odesílá požadavek GET a požadavek je úspěšný, ale volání AJAX vrátí chybu.</span><span class="sxs-lookup"><span data-stu-id="503a3-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="503a3-155">Je důležité pochopit, že zásady stejného původu nebrání prohlížeči *Odeslat* požadavek.</span><span class="sxs-lookup"><span data-stu-id="503a3-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="503a3-156">Místo toho zabrání aplikaci zobrazit *odpověď*.</span><span class="sxs-lookup"><span data-stu-id="503a3-156">Instead, it prevents the application from seeing the *response*.</span></span>

![Webový ladicí program Fiddler zobrazující webové požadavky](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="503a3-158">Povolení CORS</span><span class="sxs-lookup"><span data-stu-id="503a3-158">Enable CORS</span></span>

<span data-ttu-id="503a3-159">Teď v aplikaci WebService povolíte CORS.</span><span class="sxs-lookup"><span data-stu-id="503a3-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="503a3-160">Nejdřív přidejte balíček NuGet CORS.</span><span class="sxs-lookup"><span data-stu-id="503a3-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="503a3-161">V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="503a3-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="503a3-162">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="503a3-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="503a3-163">Tento příkaz nainstaluje nejnovější balíček a aktualizuje všechny závislosti, včetně základních knihoven webových rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="503a3-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="503a3-164">Použijte příznak `-Version` k zacílení na konkrétní verzi.</span><span class="sxs-lookup"><span data-stu-id="503a3-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="503a3-165">Balíček CORS vyžaduje webové rozhraní API 2,0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="503a3-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="503a3-166">Otevřete soubor *App\_Start/WebApiConfig. cs*.</span><span class="sxs-lookup"><span data-stu-id="503a3-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="503a3-167">Do metody **WebApiConfig. Register** přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="503a3-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="503a3-168">Dále přidejte atribut **[EnableCors]** do třídy `TestController`:</span><span class="sxs-lookup"><span data-stu-id="503a3-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="503a3-169">Pro parametr *původes* použijte identifikátor URI, kde jste nasadili aplikaci WebClient.</span><span class="sxs-lookup"><span data-stu-id="503a3-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="503a3-170">To umožňuje, aby se požadavky na více zdrojů od WebClient a pořád nepovolovaly všechny ostatní požadavky mezi doménami.</span><span class="sxs-lookup"><span data-stu-id="503a3-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="503a3-171">Později popište parametry pro **[EnableCors]** podrobněji.</span><span class="sxs-lookup"><span data-stu-id="503a3-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="503a3-172">Na konec adresy URL *původních* míst nepoužívejte lomítko.</span><span class="sxs-lookup"><span data-stu-id="503a3-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="503a3-173">Znovu nasaďte aktualizovanou aplikaci WebService.</span><span class="sxs-lookup"><span data-stu-id="503a3-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="503a3-174">Nemusíte aktualizovat WebClient.</span><span class="sxs-lookup"><span data-stu-id="503a3-174">You don't need to update WebClient.</span></span> <span data-ttu-id="503a3-175">Požadavek AJAX z WebClient by teď měl být úspěšný.</span><span class="sxs-lookup"><span data-stu-id="503a3-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="503a3-176">Metody GET, PUT a POST jsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="503a3-176">The GET, PUT, and POST methods are all allowed.</span></span>

![Webový prohlížeč zobrazující úspěšnou zkušební zprávu](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="503a3-178">Jak CORS funguje</span><span class="sxs-lookup"><span data-stu-id="503a3-178">How CORS Works</span></span>

<span data-ttu-id="503a3-179">Tato část popisuje, co se stane v žádosti CORS, na úrovni zpráv HTTP.</span><span class="sxs-lookup"><span data-stu-id="503a3-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="503a3-180">Je důležité pochopit, jak CORS funguje, abyste mohli správně nakonfigurovat atribut **[EnableCors]** a řešit potíže, pokud nefungují podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="503a3-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="503a3-181">Specifikace CORS zavádí několik nových hlaviček protokolu HTTP, které umožňují žádosti mezi zdroji.</span><span class="sxs-lookup"><span data-stu-id="503a3-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="503a3-182">Pokud prohlížeč podporuje CORS, nastavuje tyto hlavičky pro žádosti mezi zdroji automaticky. v kódu JavaScriptu nemusíte nic dělat.</span><span class="sxs-lookup"><span data-stu-id="503a3-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="503a3-183">Tady je příklad žádosti o více zdrojů.</span><span class="sxs-lookup"><span data-stu-id="503a3-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="503a3-184">Hlavička "Origin" poskytuje doménu lokality, která požadavek provádí.</span><span class="sxs-lookup"><span data-stu-id="503a3-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="503a3-185">Pokud server tuto žádost povoluje, nastaví hlavičku Access-Control-Allow-Origin.</span><span class="sxs-lookup"><span data-stu-id="503a3-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="503a3-186">Hodnota této hlavičky odpovídá záhlaví původu, nebo se jedná o zástupnou hodnotu "\*", což znamená, že je povolen libovolný původ.</span><span class="sxs-lookup"><span data-stu-id="503a3-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="503a3-187">Pokud odpověď nezahrnuje hlavičku Access-Control-Allow-Origin, požadavek AJAX se nezdařil.</span><span class="sxs-lookup"><span data-stu-id="503a3-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="503a3-188">Konkrétně prohlížeč požadavek nepovoluje.</span><span class="sxs-lookup"><span data-stu-id="503a3-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="503a3-189">I v případě, že server vrátí úspěšnou odpověď, prohlížeč nezpřístupňuje odpověď klientské aplikaci.</span><span class="sxs-lookup"><span data-stu-id="503a3-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="503a3-190">**Požadavky na kontrolu před výstupem**</span><span class="sxs-lookup"><span data-stu-id="503a3-190">**Preflight Requests**</span></span>

<span data-ttu-id="503a3-191">V případě některých žádostí CORS pošle prohlížeč další žádost s názvem "žádost o kontrolu před odesláním skutečné žádosti o prostředek".</span><span class="sxs-lookup"><span data-stu-id="503a3-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="503a3-192">Prohlížeč může požadavek na předběžné kontroly přeskočit, pokud jsou splněné následující podmínky:</span><span class="sxs-lookup"><span data-stu-id="503a3-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="503a3-193">Metoda Request je GET, HEAD nebo POST *a*</span><span class="sxs-lookup"><span data-stu-id="503a3-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="503a3-194">Aplikace nenastavuje žádné hlavičky požadavků *, které jsou* jiné než akceptující, Accept-Language, Content-Language, Content-Type nebo Last-ID.</span><span class="sxs-lookup"><span data-stu-id="503a3-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="503a3-195">Hlavička Content-Type (Pokud je nastavena) je jedna z následujících:</span><span class="sxs-lookup"><span data-stu-id="503a3-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="503a3-196">Application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="503a3-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="503a3-197">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="503a3-197">multipart/form-data</span></span>
    - <span data-ttu-id="503a3-198">text/plain</span><span class="sxs-lookup"><span data-stu-id="503a3-198">text/plain</span></span>

<span data-ttu-id="503a3-199">Pravidlo týkající se hlaviček požadavků platí pro hlavičky, které aplikace nastaví pomocí volání **setRequestHeader** na objektu **XMLHttpRequest** .</span><span class="sxs-lookup"><span data-stu-id="503a3-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="503a3-200">(Specifikace CORS volá tyto "hlavičky žádostí o autora".) Pravidlo se nevztahuje na hlavičky, které může *prohlížeč* nastavit, jako je například uživatelský agent, hostitel nebo délka obsahu.</span><span class="sxs-lookup"><span data-stu-id="503a3-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="503a3-201">Tady je příklad žádosti o kontrolu před výstupem:</span><span class="sxs-lookup"><span data-stu-id="503a3-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="503a3-202">Požadavek na lety používá metodu HTTP.</span><span class="sxs-lookup"><span data-stu-id="503a3-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="503a3-203">Obsahuje dvě speciální hlavičky:</span><span class="sxs-lookup"><span data-stu-id="503a3-203">It includes two special headers:</span></span>

- <span data-ttu-id="503a3-204">Access-Control-Request-method: metoda HTTP, která bude použita pro skutečný požadavek.</span><span class="sxs-lookup"><span data-stu-id="503a3-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="503a3-205">Access-Control-Request-Headers seznam hlaviček požadavků, které *aplikace* nastaví na skutečném požadavku.</span><span class="sxs-lookup"><span data-stu-id="503a3-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="503a3-206">(Znovu nezahrnuje hlavičky, které nastaví prohlížeč.)</span><span class="sxs-lookup"><span data-stu-id="503a3-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="503a3-207">Tady je příklad odpovědi za předpokladu, že server povoluje požadavek:</span><span class="sxs-lookup"><span data-stu-id="503a3-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="503a3-208">Odpověď obsahuje hlavičku Access-Control-Allow-Methods, která obsahuje seznam povolených metod, a volitelně hlavičku Access-Control-Allow-Headers, která obsahuje seznam povolených hlaviček.</span><span class="sxs-lookup"><span data-stu-id="503a3-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="503a3-209">Pokud je žádost o kontrolu předem úspěšná, prohlížeč pošle skutečný požadavek, jak je popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="503a3-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="503a3-210">Nástroje běžně používané k testování koncových bodů s požadavky na možnosti kontroly před výstupem (například [Fiddler](https://www.telerik.com/fiddler) a [post](https://www.getpostman.com/)) neodesílají ve výchozím nastavení hlavičky požadované možnosti.</span><span class="sxs-lookup"><span data-stu-id="503a3-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="503a3-211">Ověřte, že se v žádosti odesílají hlavičky `Access-Control-Request-Method` a `Access-Control-Request-Headers` a že hlavičky možností dosáhnou aplikace prostřednictvím služby IIS.</span><span class="sxs-lookup"><span data-stu-id="503a3-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="503a3-212">Pokud chcete nakonfigurovat službu IIS tak, aby aplikaci ASP.NET mohla přijímat a zpracovávat žádosti o možnosti, přidejte následující konfiguraci do souboru *Web. config* aplikace v části `<system.webServer><handlers>`:</span><span class="sxs-lookup"><span data-stu-id="503a3-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="503a3-213">Odebrání `OPTIONSVerbHandler` zabrání službě IIS ve zpracování požadavků na možnosti.</span><span class="sxs-lookup"><span data-stu-id="503a3-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="503a3-214">Nahrazení `ExtensionlessUrlHandler-Integrated-4.0` umožňuje požadavkům na přístup k aplikaci, protože registrace výchozího modulu povoluje pouze požadavky GET, HEAD, POST a DEBUG s příponami bez přípony.</span><span class="sxs-lookup"><span data-stu-id="503a3-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="503a3-215">Pravidla oboru pro [EnableCors]</span><span class="sxs-lookup"><span data-stu-id="503a3-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="503a3-216">Pro všechny řadiče webového rozhraní API ve vaší aplikaci můžete povolit CORS na akci, pro každý kontroler nebo globálně.</span><span class="sxs-lookup"><span data-stu-id="503a3-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="503a3-217">**Na akci**</span><span class="sxs-lookup"><span data-stu-id="503a3-217">**Per Action**</span></span>

<span data-ttu-id="503a3-218">Chcete-li povolit CORS pro jednu akci, nastavte v metodě Action atribut **[EnableCors]** .</span><span class="sxs-lookup"><span data-stu-id="503a3-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="503a3-219">Následující příklad povoluje CORS jenom pro metodu `GetItem`.</span><span class="sxs-lookup"><span data-stu-id="503a3-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="503a3-220">**Na kontroler**</span><span class="sxs-lookup"><span data-stu-id="503a3-220">**Per Controller**</span></span>

<span data-ttu-id="503a3-221">Pokud jste pro třídu kontroleru nastavili **[EnableCors]** , vztahuje se na všechny akce na řadiči.</span><span class="sxs-lookup"><span data-stu-id="503a3-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="503a3-222">Pro zakázání CORS pro akci přidejte k akci atribut **[DisableCors]** .</span><span class="sxs-lookup"><span data-stu-id="503a3-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="503a3-223">Následující příklad povoluje CORS pro každou metodu kromě `PutItem`.</span><span class="sxs-lookup"><span data-stu-id="503a3-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="503a3-224">**Univerzál**</span><span class="sxs-lookup"><span data-stu-id="503a3-224">**Globally**</span></span>

<span data-ttu-id="503a3-225">Pokud chcete povolit CORS pro všechny řadiče webového rozhraní API ve vaší aplikaci, předejte instanci **EnableCorsAttribute** do metody **EnableCors** :</span><span class="sxs-lookup"><span data-stu-id="503a3-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="503a3-226">Pokud nastavíte atribut ve více než jednom oboru, pořadí priorit je:</span><span class="sxs-lookup"><span data-stu-id="503a3-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="503a3-227">Akce</span><span class="sxs-lookup"><span data-stu-id="503a3-227">Action</span></span>
2. <span data-ttu-id="503a3-228">Kontrolér</span><span class="sxs-lookup"><span data-stu-id="503a3-228">Controller</span></span>
3. <span data-ttu-id="503a3-229">Globální</span><span class="sxs-lookup"><span data-stu-id="503a3-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="503a3-230">Nastavení povolených zdrojů</span><span class="sxs-lookup"><span data-stu-id="503a3-230">Set the allowed origins</span></span>

<span data-ttu-id="503a3-231">Parametr *origines* atributu **[EnableCors]** určuje, které zdroje mají povolený přístup k prostředku.</span><span class="sxs-lookup"><span data-stu-id="503a3-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="503a3-232">Hodnota je čárkami oddělený seznam povolených zdrojů.</span><span class="sxs-lookup"><span data-stu-id="503a3-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="503a3-233">Můžete také použít zástupnou hodnotu "\*" pro povolení požadavků z libovolného původu.</span><span class="sxs-lookup"><span data-stu-id="503a3-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="503a3-234">Před povolením požadavků z libovolného počátku zvažte pečlivou pozornost.</span><span class="sxs-lookup"><span data-stu-id="503a3-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="503a3-235">To znamená, že každý web může ve webovém rozhraní API vyvolat volání AJAX.</span><span class="sxs-lookup"><span data-stu-id="503a3-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="503a3-236">Nastavení povolených metod HTTP</span><span class="sxs-lookup"><span data-stu-id="503a3-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="503a3-237">Parametr *metody* atributu **[EnableCors]** určuje, které metody HTTP mají povolen přístup k prostředku.</span><span class="sxs-lookup"><span data-stu-id="503a3-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="503a3-238">Pro povolení všech metod použijte zástupný znak "\*".</span><span class="sxs-lookup"><span data-stu-id="503a3-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="503a3-239">Následující příklad povoluje pouze požadavky GET a POST.</span><span class="sxs-lookup"><span data-stu-id="503a3-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="503a3-240">Nastavení povolených hlaviček žádosti</span><span class="sxs-lookup"><span data-stu-id="503a3-240">Set the allowed request headers</span></span>

<span data-ttu-id="503a3-241">Tento článek popisuje předchozí způsob, jakým může požadavek na kontrolu před výstupem zahrnovat hlavičku Access-Control-Request-Headers, v níž je uveden seznam hlaviček protokolu HTTP, které aplikace nastavila (záhlaví žádostí s názvem "autor žádosti").</span><span class="sxs-lookup"><span data-stu-id="503a3-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="503a3-242">Parametr *Headers* atributu **[EnableCors]** určuje, které hlavičky žádostí autora jsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="503a3-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="503a3-243">Pro povolení všech hlaviček nastavte *záhlaví* na "\*".</span><span class="sxs-lookup"><span data-stu-id="503a3-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="503a3-244">Pokud chcete zobrazit konkrétní záhlaví, nastavte *záhlaví* na čárkami oddělený seznam povolených hlaviček:</span><span class="sxs-lookup"><span data-stu-id="503a3-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="503a3-245">Nicméně prohlížeče nejsou zcela konzistentní v tom, jak nastavily Access-Control-Request-Headers.</span><span class="sxs-lookup"><span data-stu-id="503a3-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="503a3-246">Například Chrome aktuálně obsahuje "Origin".</span><span class="sxs-lookup"><span data-stu-id="503a3-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="503a3-247">FireFox neobsahuje standardní hlavičky, jako je "Accept", ani když ji aplikace nastaví ve skriptu.</span><span class="sxs-lookup"><span data-stu-id="503a3-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="503a3-248">Pokud nastavíte *záhlaví* na jinou hodnotu než "\*", měli byste zahrnout aspoň "přijmout", "Content-Type" a "Origin" a také všechna vlastní záhlaví, která chcete podporovat.</span><span class="sxs-lookup"><span data-stu-id="503a3-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="503a3-249">Nastavení povolených hlaviček odpovědí</span><span class="sxs-lookup"><span data-stu-id="503a3-249">Set the allowed response headers</span></span>

<span data-ttu-id="503a3-250">Ve výchozím nastavení prohlížeč nezveřejňuje všechny hlavičky odpovědí na aplikaci.</span><span class="sxs-lookup"><span data-stu-id="503a3-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="503a3-251">Ve výchozím nastavení jsou k dispozici následující hlavičky odpovědí:</span><span class="sxs-lookup"><span data-stu-id="503a3-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="503a3-252">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="503a3-252">Cache-Control</span></span>
- <span data-ttu-id="503a3-253">Obsah – jazyk</span><span class="sxs-lookup"><span data-stu-id="503a3-253">Content-Language</span></span>
- <span data-ttu-id="503a3-254">Content-Type</span><span class="sxs-lookup"><span data-stu-id="503a3-254">Content-Type</span></span>
- <span data-ttu-id="503a3-255">Expires</span><span class="sxs-lookup"><span data-stu-id="503a3-255">Expires</span></span>
- <span data-ttu-id="503a3-256">Naposledy změněno</span><span class="sxs-lookup"><span data-stu-id="503a3-256">Last-Modified</span></span>
- <span data-ttu-id="503a3-257">Pragma</span><span class="sxs-lookup"><span data-stu-id="503a3-257">Pragma</span></span>

<span data-ttu-id="503a3-258">Specifikace CORS volá tyto [jednoduché hlavičky odpovědi](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span><span class="sxs-lookup"><span data-stu-id="503a3-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="503a3-259">Pro zpřístupnění dalších hlaviček pro aplikaci nastavte parametr *exposedHeaders* **[EnableCors]** .</span><span class="sxs-lookup"><span data-stu-id="503a3-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="503a3-260">V následujícím příkladu `Get` metoda kontroleru nastaví vlastní hlavičku s názvem "X-Custom-header".</span><span class="sxs-lookup"><span data-stu-id="503a3-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="503a3-261">Ve výchozím nastavení prohlížeč nebude tuto hlavičku vystavovat v žádosti o více zdrojů.</span><span class="sxs-lookup"><span data-stu-id="503a3-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="503a3-262">Pokud chcete, aby byla hlavička dostupná, zahrňte do *exposedHeaders*hodnotu "X-Custom-header".</span><span class="sxs-lookup"><span data-stu-id="503a3-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="503a3-263">Předávání přihlašovacích údajů v žádostech mezi zdroji</span><span class="sxs-lookup"><span data-stu-id="503a3-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="503a3-264">Přihlašovací údaje vyžadují zvláštní zpracování v žádosti CORS.</span><span class="sxs-lookup"><span data-stu-id="503a3-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="503a3-265">Ve výchozím nastavení prohlížeč neodesílá žádné přihlašovací údaje pomocí žádosti o více zdrojů.</span><span class="sxs-lookup"><span data-stu-id="503a3-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="503a3-266">Přihlašovací údaje zahrnují soubory cookie i schémata ověřování protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="503a3-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="503a3-267">Aby bylo možné odesílat přihlašovací údaje pomocí žádosti o více zdrojů, musí klient nastavit **XMLHttpRequest. withCredentials** na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="503a3-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="503a3-268">Přímé použití **XMLHttpRequest** :</span><span class="sxs-lookup"><span data-stu-id="503a3-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="503a3-269">V jQuery:</span><span class="sxs-lookup"><span data-stu-id="503a3-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="503a3-270">Server navíc musí přihlašovací údaje umožňovat.</span><span class="sxs-lookup"><span data-stu-id="503a3-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="503a3-271">Pokud chcete ve webovém rozhraní API zapnout přihlašovací údaje pro více zdrojů, nastavte vlastnost **SupportsCredentials** na hodnotu true v atributu **[EnableCors]** :</span><span class="sxs-lookup"><span data-stu-id="503a3-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="503a3-272">Pokud má tato vlastnost hodnotu true, bude odpověď HTTP zahrnovat hlavičku Access-Control-Allow-Credentials.</span><span class="sxs-lookup"><span data-stu-id="503a3-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="503a3-273">Tato hlavička obsahuje informace o prohlížeči, který server umožňuje přihlašovací údaje pro požadavek mezi zdroji.</span><span class="sxs-lookup"><span data-stu-id="503a3-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="503a3-274">Pokud prohlížeč odesílá přihlašovací údaje, ale odpověď nezahrnuje platné záhlaví Access-Control-Allow-Credentials, prohlížeč nezveřejňuje odpověď na aplikaci a požadavek AJAX selže.</span><span class="sxs-lookup"><span data-stu-id="503a3-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="503a3-275">Buďte opatrní při nastavení **SupportsCredentials** na hodnotu true, protože to znamená, že web v jiné doméně může posílat přihlašovací údaje přihlášeného uživatele k webovému rozhraní API jménem uživatele bez ohledu na uživatele.</span><span class="sxs-lookup"><span data-stu-id="503a3-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="503a3-276">Specifikace CORS také uvádí, že nastavení *původce* na &quot;\*&quot; je neplatné, pokud má **SupportsCredentials** hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="503a3-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="503a3-277">Vlastní poskytovatelé zásad CORS</span><span class="sxs-lookup"><span data-stu-id="503a3-277">Custom CORS policy providers</span></span>

<span data-ttu-id="503a3-278">Atribut **[EnableCors]** implementuje rozhraní **ICorsPolicyProvider** .</span><span class="sxs-lookup"><span data-stu-id="503a3-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="503a3-279">Můžete poskytnout vlastní implementaci vytvořením třídy, která je odvozena z **atributu** a implementuje **ICorsPolicyProvider**.</span><span class="sxs-lookup"><span data-stu-id="503a3-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="503a3-280">Nyní můžete použít atribut na místo, které byste umístili **[EnableCors]** .</span><span class="sxs-lookup"><span data-stu-id="503a3-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="503a3-281">Vlastní poskytovatel zásad CORS například mohl přečíst nastavení z konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="503a3-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="503a3-282">Jako alternativu k používání atributů můžete zaregistrovat objekt **ICorsPolicyProviderFactory** , který vytváří objekty **ICorsPolicyProvider** .</span><span class="sxs-lookup"><span data-stu-id="503a3-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="503a3-283">Chcete-li nastavit **ICorsPolicyProviderFactory**, zavolejte při spuštění metodu rozšíření **SetCorsPolicyProviderFactory** následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="503a3-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="503a3-284">Podpora prohlížeče</span><span class="sxs-lookup"><span data-stu-id="503a3-284">Browser support</span></span>

<span data-ttu-id="503a3-285">Balíček Web API CORS je technologie na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="503a3-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="503a3-286">Prohlížeč uživatele musí také podporovat CORS.</span><span class="sxs-lookup"><span data-stu-id="503a3-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="503a3-287">Stávající verze všech hlavních prohlížečů naštěstí zahrnují [podporu CORS](http://caniuse.com/cors).</span><span class="sxs-lookup"><span data-stu-id="503a3-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
