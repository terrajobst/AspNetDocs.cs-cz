---
uid: web-api/overview/security/external-authentication-services
title: Externí ověřovací služby s webovým rozhranímC#API ASP.NET () | Microsoft Docs
author: rmcmurray
description: Popisuje použití externích ověřovacích služeb ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555473"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="1d931-103">Služby externích ověřování s webovým rozhranímC#API ASP.NET ()</span><span class="sxs-lookup"><span data-stu-id="1d931-103">External Authentication Services with ASP.NET Web API (C#)</span></span>

<span data-ttu-id="1d931-104">Visual Studio 2017 a ASP.NET 4.7.2 rozšiřují možnosti zabezpečení pro [jednostránkové aplikace](../../../single-page-application/index.md) (Spa) a [webové rozhraní API](../../index.md) pro integraci s externími ověřovacími službami, mezi které patří několik OAuth/OpenID a služby sociální média ověřování: účty Microsoft, Twitter, Facebook a Google.</span><span class="sxs-lookup"><span data-stu-id="1d931-104">Visual Studio 2017 and ASP.NET 4.7.2 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>  

### <a name="in-this-walkthrough"></a><span data-ttu-id="1d931-105">V tomto návodu</span><span class="sxs-lookup"><span data-stu-id="1d931-105">In this Walkthrough</span></span>

- [<span data-ttu-id="1d931-106">Používání služeb externích ověřování</span><span class="sxs-lookup"><span data-stu-id="1d931-106">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="1d931-107">Vytvoření ukázkové webové aplikace</span><span class="sxs-lookup"><span data-stu-id="1d931-107">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="1d931-108">Povoluje se ověřování na Facebooku.</span><span class="sxs-lookup"><span data-stu-id="1d931-108">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="1d931-109">Povoluje se ověřování Google.</span><span class="sxs-lookup"><span data-stu-id="1d931-109">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="1d931-110">Povolení ověřování společnosti Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d931-110">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="1d931-111">Povolení ověřování na Twitteru</span><span class="sxs-lookup"><span data-stu-id="1d931-111">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="1d931-112">Další informace</span><span class="sxs-lookup"><span data-stu-id="1d931-112">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="1d931-113">Kombinování externích ověřovacích služeb</span><span class="sxs-lookup"><span data-stu-id="1d931-113">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="1d931-114">Konfigurace IIS Express pro použití plně kvalifikovaného názvu domény</span><span class="sxs-lookup"><span data-stu-id="1d931-114">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="1d931-115">Jak získat nastavení aplikace pro ověřování Microsoftu</span><span class="sxs-lookup"><span data-stu-id="1d931-115">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="1d931-116">Volitelné: zakázat místní registraci</span><span class="sxs-lookup"><span data-stu-id="1d931-116">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="1d931-117">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="1d931-117">Prerequisites</span></span>

<span data-ttu-id="1d931-118">Chcete-li postupovat podle příkladů v tomto návodu, musíte mít následující:</span><span class="sxs-lookup"><span data-stu-id="1d931-118">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="1d931-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1d931-119">Visual Studio 2017</span></span>
- <span data-ttu-id="1d931-120">Vývojářský účet s identifikátorem aplikace a tajným klíčem pro jednu z následujících služeb ověřování na sociálních médiích:</span><span class="sxs-lookup"><span data-stu-id="1d931-120">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

  - <span data-ttu-id="1d931-121">Účty Microsoft ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="1d931-121">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
  - <span data-ttu-id="1d931-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="1d931-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
  - <span data-ttu-id="1d931-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="1d931-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>
  - <span data-ttu-id="1d931-124">Google ([https://developers.google.com/](https://developers.google.com))</span><span class="sxs-lookup"><span data-stu-id="1d931-124">Google ([https://developers.google.com/](https://developers.google.com))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="1d931-125">Používání služeb externích ověřování</span><span class="sxs-lookup"><span data-stu-id="1d931-125">Using External Authentication Services</span></span>

<span data-ttu-id="1d931-126">Díky četnosti externích ověřovacích služeb, které jsou aktuálně dostupné vývojářům webu, můžete zkrátit dobu vývoje při vytváření nových webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="1d931-126">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="1d931-127">Webové uživatele obvykle mají několik stávajících účtů pro oblíbené webové služby a weby sociálních médií, proto když webová aplikace implementuje ověřovací služby z externí webové služby nebo webu sociálních médií, uloží dobu vývoje, která bylo stráveno vytvořením implementace ověřování.</span><span class="sxs-lookup"><span data-stu-id="1d931-127">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="1d931-128">Použití externí služby ověřování ukládá koncovým uživatelům, aby si pro vaši webovou aplikaci vytvářel jiný účet, a také si musí zapamatovat jiné uživatelské jméno a heslo.</span><span class="sxs-lookup"><span data-stu-id="1d931-128">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="1d931-129">V minulosti měli vývojáři dvě možnosti: vytvořit vlastní implementaci ověřování nebo se naučíte integrovat externí službu ověřování do svých aplikací.</span><span class="sxs-lookup"><span data-stu-id="1d931-129">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="1d931-130">Na nejvyšší úrovni představuje následující diagram jednoduchý tok požadavků pro uživatelského agenta (webový prohlížeč), který požaduje informace z webové aplikace, která je nakonfigurovaná na používání externí služby ověřování:</span><span class="sxs-lookup"><span data-stu-id="1d931-130">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

<span data-ttu-id="1d931-131">V předchozím diagramu agent uživatele (nebo webový prohlížeč v tomto příkladu) vytvoří požadavek na webovou aplikaci, která přesměruje webový prohlížeč na externí službu ověřování.</span><span class="sxs-lookup"><span data-stu-id="1d931-131">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="1d931-132">Uživatelský agent pošle své přihlašovací údaje do služby externího ověřování a pokud byl agent uživatele úspěšně ověřen, služba externí ověřování přesměruje uživatelského agenta do původní webové aplikace s určitou formou tokenu, kterou uživatelský agent se pošle webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="1d931-132">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="1d931-133">Webová aplikace použije token k ověření, zda byl uživatelský agent úspěšně ověřen pomocí externí služby ověřování, a webová aplikace může token použít k získání dalších informací o uživatelském agentovi.</span><span class="sxs-lookup"><span data-stu-id="1d931-133">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="1d931-134">Jakmile se aplikace dokončí zpracováním informací o uživatelském agentovi, Webová aplikace vrátí příslušnou odpověď agentovi uživatele na základě jeho autorizačního nastavení.</span><span class="sxs-lookup"><span data-stu-id="1d931-134">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="1d931-135">V tomto druhém příkladu Agent pro uživatele vychází z webové aplikace a externího autorizačního serveru a webová aplikace provádí další komunikaci s externím autorizačním serverem, aby načetla Další informace o uživateli. agenta</span><span class="sxs-lookup"><span data-stu-id="1d931-135">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

<span data-ttu-id="1d931-136">Sady Visual Studio 2017 a ASP.NET 4.7.2 umožňují vývojářům zajistit integraci s externími službami ověřování pro vývojáře díky integrované integraci pro následující služby ověřování:</span><span class="sxs-lookup"><span data-stu-id="1d931-136">Visual Studio 2017 and ASP.NET 4.7.2 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="1d931-137">Facebook</span><span class="sxs-lookup"><span data-stu-id="1d931-137">Facebook</span></span>
- <span data-ttu-id="1d931-138">Google</span><span class="sxs-lookup"><span data-stu-id="1d931-138">Google</span></span>
- <span data-ttu-id="1d931-139">Účty Microsoft (účty Windows Live ID)</span><span class="sxs-lookup"><span data-stu-id="1d931-139">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="1d931-140">Twitter</span><span class="sxs-lookup"><span data-stu-id="1d931-140">Twitter</span></span>

<span data-ttu-id="1d931-141">Příklady v tomto návodu ukazují, jak nakonfigurovat každou z podporovaných externích ověřovacích služeb pomocí nové šablony webové aplikace ASP.NET, která se dodává se sadou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1d931-141">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="1d931-142">V případě potřeby možná budete muset přidat svůj plně kvalifikovaný název domény do nastavení pro službu externího ověřování.</span><span class="sxs-lookup"><span data-stu-id="1d931-142">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="1d931-143">Tento požadavek vychází z omezení zabezpečení pro některé externí služby ověřování, které vyžadují, aby plně kvalifikovaný název domény v nastavení vaší aplikace odpovídal plně kvalifikovanému názvu domény, který používají vaši klienti.</span><span class="sxs-lookup"><span data-stu-id="1d931-143">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="1d931-144">(Kroky pro tento postup se u každé externí služby ověřování značně liší. budete se muset obrátit na dokumentaci pro každou službu externího ověřování a zjistit, jestli je to potřeba, a jak tato nastavení nakonfigurovat.) Pokud potřebujete nakonfigurovat IIS Express pro použití plně kvalifikovaného názvu domény pro testování tohoto prostředí, přečtěte si část [konfigurace IIS Express použití plně kvalifikovaného názvu domény](#FQDN) v tomto návodu.</span><span class="sxs-lookup"><span data-stu-id="1d931-144">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a><span data-ttu-id="1d931-145">Vytvoření ukázkové webové aplikace</span><span class="sxs-lookup"><span data-stu-id="1d931-145">Create a Sample Web Application</span></span>

<span data-ttu-id="1d931-146">Následující kroky vás provedou vytvořením ukázkové aplikace pomocí šablony webové aplikace ASP.NET a tuto ukázkovou aplikaci použijete pro každou službu externího ověřování dále v tomto návodu.</span><span class="sxs-lookup"><span data-stu-id="1d931-146">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="1d931-147">Spusťte Visual Studio 2017 a na úvodní stránce vyberte **Nový projekt** .</span><span class="sxs-lookup"><span data-stu-id="1d931-147">Start Visual Studio 2017 and select **New Project** from the Start page.</span></span> <span data-ttu-id="1d931-148">Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.</span><span class="sxs-lookup"><span data-stu-id="1d931-148">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

<span data-ttu-id="1d931-149">Po zobrazení dialogového okna **Nový projekt** vyberte možnost **nainstalováno** a rozbalte položku **vizuál C#** .</span><span class="sxs-lookup"><span data-stu-id="1d931-149">When the **New Project** dialog box is displayed, select **Installed** and expand **Visual C#**.</span></span> <span data-ttu-id="1d931-150">V **části C#vizuál** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="1d931-150">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="1d931-151">V seznamu šablon projektu vyberte **ASP.NET webová aplikace (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="1d931-151">In the list of project templates, select **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="1d931-152">Zadejte název projektu a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d931-152">Enter a name for your project and click **OK**.</span></span>

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

<span data-ttu-id="1d931-153">Po zobrazení **nového projektu ASP.NET** vyberte šablonu **aplikace s jednou stránkou** a klikněte na **vytvořit projekt**.</span><span class="sxs-lookup"><span data-stu-id="1d931-153">When the **New ASP.NET Project** is displayed, select the **Single Page Application** template and click **Create Project**.</span></span>

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

<span data-ttu-id="1d931-154">Počkejte, až Visual Studio 2017 vytvoří projekt.</span><span class="sxs-lookup"><span data-stu-id="1d931-154">Wait as Visual Studio 2017 creates your project.</span></span>

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

<span data-ttu-id="1d931-155">Po dokončení vytváření projektu v aplikaci Visual Studio 2017 otevřete soubor *Startup.auth.cs* , který je umístěn ve složce **App\_Start** .</span><span class="sxs-lookup"><span data-stu-id="1d931-155">When Visual Studio 2017 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="1d931-156">Při prvním vytvoření projektu nejsou v souboru *Startup.auth.cs* povoleny žádné externí ověřovací služby. Následující příklad ilustruje, jak se váš kód může podobat, kde jsou zvýrazněné oddíly, kde byste povolili externí službu ověřování a veškerá relevantní nastavení, aby bylo možné používat účty Microsoft, Twitter, Facebook nebo Google ověřování s vaší aplikací ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="1d931-156">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="1d931-157">Když stisknete klávesu F5 k sestavení a ladění webové aplikace, zobrazí se přihlašovací obrazovka, na které se zobrazí, že nebyly definovány žádné externí ověřovací služby.</span><span class="sxs-lookup"><span data-stu-id="1d931-157">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

<span data-ttu-id="1d931-158">V následujících částech se dozvíte, jak povolit každou z externích ověřovacích služeb, které jsou k dispozici v ASP.NET ve Visual Studiu 2017.</span><span class="sxs-lookup"><span data-stu-id="1d931-158">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2017.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="1d931-159">Povoluje se ověřování na Facebooku.</span><span class="sxs-lookup"><span data-stu-id="1d931-159">Enabling Facebook authentication</span></span>

<span data-ttu-id="1d931-160">Použití ověřování na Facebooku vyžaduje, abyste vytvořili vývojářský účet pro Facebook a váš projekt bude vyžadovat ID aplikace a tajný klíč z Facebooku, aby fungoval.</span><span class="sxs-lookup"><span data-stu-id="1d931-160">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="1d931-161">Informace o tom, jak vytvořit vývojářský účet pro Facebook a získat ID aplikace a tajný klíč, najdete v tématu [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span><span class="sxs-lookup"><span data-stu-id="1d931-161">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="1d931-162">Jakmile získáte ID aplikace a tajný klíč, použijte následující postup k povolení ověřování na Facebooku pro vaši webovou aplikaci:</span><span class="sxs-lookup"><span data-stu-id="1d931-162">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="1d931-163">Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .</span><span class="sxs-lookup"><span data-stu-id="1d931-163">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1d931-164">Vyhledejte část s ověřovacím kódem Facebooku:</span><span class="sxs-lookup"><span data-stu-id="1d931-164">Locate the Facebook authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="1d931-165">Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte ID aplikace a tajný klíč.</span><span class="sxs-lookup"><span data-stu-id="1d931-165">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="1d931-166">Po přidání těchto parametrů můžete projekt znovu zkompilovat:</span><span class="sxs-lookup"><span data-stu-id="1d931-166">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="1d931-167">Po stisknutí klávesy F5 k otevření webové aplikace ve webovém prohlížeči se zobrazí, že Facebook byl definován jako externí Služba ověřování:</span><span class="sxs-lookup"><span data-stu-id="1d931-167">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. <span data-ttu-id="1d931-168">Když kliknete na tlačítko **Facebook** , váš prohlížeč se přesměruje na přihlašovací stránku Facebooku:</span><span class="sxs-lookup"><span data-stu-id="1d931-168">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. <span data-ttu-id="1d931-169">Po zadání přihlašovacích údajů k Facebooku a kliknutí na **Přihlásit**se webový prohlížeč přesměruje zpátky do vaší webové aplikace. zobrazí se výzva k zadání **uživatelského jména** , které chcete přidružit k účtu Facebook:</span><span class="sxs-lookup"><span data-stu-id="1d931-169">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. <span data-ttu-id="1d931-170">Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** vaše webová aplikace zobrazí výchozí **domovskou stránku** pro váš účet Facebook:</span><span class="sxs-lookup"><span data-stu-id="1d931-170">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="1d931-171">Povoluje se ověřování Google.</span><span class="sxs-lookup"><span data-stu-id="1d931-171">Enabling Google Authentication</span></span>

<span data-ttu-id="1d931-172">Použití ověřování Google vyžaduje, abyste vytvořili účet pro vývojáře Google a váš projekt bude vyžadovat ID aplikace a tajný klíč od společnosti Google, aby mohl fungovat.</span><span class="sxs-lookup"><span data-stu-id="1d931-172">Using Google authentication requires you to create a Google developer account, and your project will require an application ID and secret key from Google in order to function.</span></span> <span data-ttu-id="1d931-173">Informace o vytvoření účtu vývojáře Google a získání ID aplikace a tajného klíče najdete v tématu [https://developers.google.com](https://developers.google.com).</span><span class="sxs-lookup"><span data-stu-id="1d931-173">For information about creating a Google developer account and obtaining your application ID and secret key, see [https://developers.google.com](https://developers.google.com).</span></span>

<span data-ttu-id="1d931-174">Pokud chcete povolit ověřování Google pro vaši webovou aplikaci, použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="1d931-174">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="1d931-175">Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .</span><span class="sxs-lookup"><span data-stu-id="1d931-175">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1d931-176">Vyhledejte oddíl ověřování Google Code:</span><span class="sxs-lookup"><span data-stu-id="1d931-176">Locate the Google authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="1d931-177">Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte ID aplikace a tajný klíč.</span><span class="sxs-lookup"><span data-stu-id="1d931-177">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="1d931-178">Po přidání těchto parametrů můžete projekt znovu zkompilovat:</span><span class="sxs-lookup"><span data-stu-id="1d931-178">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="1d931-179">Když stisknete klávesu F5 k otevření webové aplikace ve webovém prohlížeči, uvidíte, že Google byl definován jako externí Služba ověřování:</span><span class="sxs-lookup"><span data-stu-id="1d931-179">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. <span data-ttu-id="1d931-180">Když kliknete na tlačítko **Google** , váš prohlížeč se přesměruje na přihlašovací stránku Google:</span><span class="sxs-lookup"><span data-stu-id="1d931-180">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. <span data-ttu-id="1d931-181">Až zadáte svoje přihlašovací údaje Google a kliknete na **Přihlásit**, Google vás vyzve, abyste ověřili, že vaše webová aplikace má oprávnění k přístupu k vašemu účtu Google:</span><span class="sxs-lookup"><span data-stu-id="1d931-181">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. <span data-ttu-id="1d931-182">Když kliknete na **přijmout**, váš webový prohlížeč se přesměruje zpátky do vaší webové aplikace, kde se zobrazí výzva k zadání **uživatelského jména** , které chcete přidružit k vašemu účtu Google:</span><span class="sxs-lookup"><span data-stu-id="1d931-182">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. <span data-ttu-id="1d931-183">Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** vaše webová aplikace zobrazí výchozí **domovskou stránku** účtu Google:</span><span class="sxs-lookup"><span data-stu-id="1d931-183">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="1d931-184">Povolení ověřování společnosti Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d931-184">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="1d931-185">Ověřování společnosti Microsoft vyžaduje, abyste vytvořili vývojářský účet a aby fungovalo, vyžaduje ID klienta a tajný klíč klienta.</span><span class="sxs-lookup"><span data-stu-id="1d931-185">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="1d931-186">Informace o vytvoření účtu Microsoft Developer a získání ID klienta a tajného kódu klienta najdete v tématu [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span><span class="sxs-lookup"><span data-stu-id="1d931-186">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="1d931-187">Jakmile získáte klíč příjemce a tajný klíč příjemce, pomocí následujícího postupu povolte ověřování společnosti Microsoft pro vaši webovou aplikaci:</span><span class="sxs-lookup"><span data-stu-id="1d931-187">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="1d931-188">Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .</span><span class="sxs-lookup"><span data-stu-id="1d931-188">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1d931-189">Vyhledejte část kódu ověřování společnosti Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1d931-189">Locate the Microsoft authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="1d931-190">Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte ID klienta a tajný klíč klienta.</span><span class="sxs-lookup"><span data-stu-id="1d931-190">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="1d931-191">Po přidání těchto parametrů můžete projekt znovu zkompilovat:</span><span class="sxs-lookup"><span data-stu-id="1d931-191">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="1d931-192">Po stisknutí klávesy F5 k otevření webové aplikace ve webovém prohlížeči se zobrazí informace o tom, že společnost Microsoft byla definována jako externí Služba ověřování:</span><span class="sxs-lookup"><span data-stu-id="1d931-192">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. <span data-ttu-id="1d931-193">Když kliknete na tlačítko **Microsoft** , váš prohlížeč se přesměruje na přihlašovací stránku Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="1d931-193">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. <span data-ttu-id="1d931-194">Po zadání přihlašovacích údajů Microsoftu a kliknutí na **Přihlásit**se zobrazí výzva, abyste ověřili, že vaše webová aplikace má oprávnění pro přístup k vašemu účet Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1d931-194">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. <span data-ttu-id="1d931-195">Kliknete-li na tlačítko **Ano**, bude webový prohlížeč přesměrován zpět do vaší webové aplikace. zobrazí se výzva k zadání **uživatelského jména** , které chcete přidružit k vašemu účet Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1d931-195">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. <span data-ttu-id="1d931-196">Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** se ve vaší webové aplikaci zobrazí výchozí **Domovská stránka** pro váš účet Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1d931-196">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="1d931-197">Povolení ověřování na Twitteru</span><span class="sxs-lookup"><span data-stu-id="1d931-197">Enabling Twitter Authentication</span></span>

<span data-ttu-id="1d931-198">Ověřování pomocí Twitteru vyžaduje, abyste vytvořili vývojářský účet a aby mohli fungovat, vyžaduje klíč příjemce a klíč příjemce.</span><span class="sxs-lookup"><span data-stu-id="1d931-198">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="1d931-199">Informace o vytvoření účtu vývojáře pro Twitter a získání klíče příjemce a tajného kódu příjemce najdete v tématu [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span><span class="sxs-lookup"><span data-stu-id="1d931-199">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="1d931-200">Jakmile získáte klíč příjemce a tajný klíč příjemce, pomocí následujícího postupu povolte pro webovou aplikaci ověřování pomocí Twitteru:</span><span class="sxs-lookup"><span data-stu-id="1d931-200">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="1d931-201">Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .</span><span class="sxs-lookup"><span data-stu-id="1d931-201">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="1d931-202">Vyhledejte část s ověřováním na Twitteru v kódu:</span><span class="sxs-lookup"><span data-stu-id="1d931-202">Locate the Twitter authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="1d931-203">Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte svůj klíč příjemce a tajný klíč příjemce.</span><span class="sxs-lookup"><span data-stu-id="1d931-203">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="1d931-204">Po přidání těchto parametrů můžete projekt znovu zkompilovat:</span><span class="sxs-lookup"><span data-stu-id="1d931-204">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="1d931-205">Po stisknutí klávesy F5 k otevření webové aplikace ve webovém prohlížeči se zobrazí, že Twitter byl definován jako externí Služba ověřování:</span><span class="sxs-lookup"><span data-stu-id="1d931-205">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. <span data-ttu-id="1d931-206">Když kliknete na tlačítko **Twitter** , váš prohlížeč se přesměruje na přihlašovací stránku Twitteru:</span><span class="sxs-lookup"><span data-stu-id="1d931-206">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. <span data-ttu-id="1d931-207">Po zadání přihlašovacích údajů pro Twitter a kliknutí na **autorizovat**se webový prohlížeč přesměruje zpátky do vaší webové aplikace. zobrazí se výzva k zadání **uživatelského jména** , které chcete přidružit k vašemu účtu Twitteru:</span><span class="sxs-lookup"><span data-stu-id="1d931-207">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. <span data-ttu-id="1d931-208">Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** se ve vaší webové aplikaci zobrazí výchozí **Domovská stránka** pro váš účet na Twitteru:</span><span class="sxs-lookup"><span data-stu-id="1d931-208">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="1d931-209">Další informace</span><span class="sxs-lookup"><span data-stu-id="1d931-209">Additional Information</span></span>

<span data-ttu-id="1d931-210">Další informace o vytváření aplikací, které používají OAuth a OpenID, najdete v následujících adresách URL:</span><span class="sxs-lookup"><span data-stu-id="1d931-210">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="1d931-211">Kombinování externích ověřovacích služeb</span><span class="sxs-lookup"><span data-stu-id="1d931-211">Combining External Authentication Services</span></span>

<span data-ttu-id="1d931-212">Pro větší flexibilitu můžete současně definovat více externích služeb ověřování – to umožní uživatelům vaší webové aplikace používat účet z kterékoli z povolených externích ověřovacích služeb:</span><span class="sxs-lookup"><span data-stu-id="1d931-212">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="1d931-213">Konfigurace IIS Express pro použití plně kvalifikovaného názvu domény</span><span class="sxs-lookup"><span data-stu-id="1d931-213">Configure IIS Express to use a fully qualified domain name</span></span>

<span data-ttu-id="1d931-214">Někteří zprostředkovatelé externího ověřování nepodporují testování aplikace pomocí adresy HTTP, jako je `http://localhost:port/`.</span><span class="sxs-lookup"><span data-stu-id="1d931-214">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="1d931-215">Chcete-li tento problém obejít, můžete přidat statické mapování plně kvalifikovaného názvu domény (FQDN) do souboru hostitelů a nakonfigurovat možnosti projektu v aplikaci Visual Studio 2017 pro použití plně kvalifikovaného názvu domény pro testování/ladění.</span><span class="sxs-lookup"><span data-stu-id="1d931-215">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2017 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="1d931-216">Chcete-li tak učinit, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="1d931-216">To do so, use the following steps:</span></span>

- <span data-ttu-id="1d931-217">Přidejte statický plně kvalifikovaný název domény pro mapování souboru hostitelů:</span><span class="sxs-lookup"><span data-stu-id="1d931-217">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="1d931-218">Otevřete příkazový řádek se zvýšenými oprávněními v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="1d931-218">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="1d931-219">Zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="1d931-219">Type the following command:</span></span>

      <span data-ttu-id="1d931-220"><kbd>Poznámkový blok%WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="1d931-220"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="1d931-221">Do souboru hostitelů přidejte položku podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="1d931-221">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="1d931-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="1d931-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="1d931-223">Uložte a zavřete soubor hostitelů.</span><span class="sxs-lookup"><span data-stu-id="1d931-223">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="1d931-224">Nakonfigurujte projekt sady Visual Studio tak, aby používal plně kvalifikovaný název domény:</span><span class="sxs-lookup"><span data-stu-id="1d931-224">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="1d931-225">Když je projekt otevřen v aplikaci Visual Studio 2017, klikněte na nabídku **projekt** a potom vyberte vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="1d931-225">When your project is open in Visual Studio 2017, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="1d931-226">Například můžete vybrat **vlastnosti WebApplication1**.</span><span class="sxs-lookup"><span data-stu-id="1d931-226">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="1d931-227">Vyberte kartu **Web** .</span><span class="sxs-lookup"><span data-stu-id="1d931-227">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="1d931-228">Zadejte plně kvalifikovaný název domény pro <strong>adresu URL projektu</strong>.</span><span class="sxs-lookup"><span data-stu-id="1d931-228">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="1d931-229">Zadejte například <kbd><http://www.wingtiptoys.com></kbd> , pokud se jednalo o mapování plně kvalifikovaného názvu domény, které jste přidali do souboru hostitelů.</span><span class="sxs-lookup"><span data-stu-id="1d931-229">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="1d931-230">Nakonfigurujte IIS Express pro použití plně kvalifikovaného názvu domény pro vaši aplikaci:</span><span class="sxs-lookup"><span data-stu-id="1d931-230">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="1d931-231">Otevřete příkazový řádek se zvýšenými oprávněními v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="1d931-231">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="1d931-232">Zadáním následujícího příkazu přejděte do složky IIS Express:</span><span class="sxs-lookup"><span data-stu-id="1d931-232">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="1d931-233"><kbd>CD/d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="1d931-233"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="1d931-234">Zadáním následujícího příkazu přidejte do aplikace plně kvalifikovaný název domény:</span><span class="sxs-lookup"><span data-stu-id="1d931-234">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="1d931-235"><kbd>Appcmd. exe nastavení konfigurace-oddíl: System. applicationHost/sites/+&quot;[name = ' WebApplication1 ']. Bindings. [Protocol = ' http ', bindingInformation = ' \*: 80: www. wingtiptoys. com ']&quot;/Commit: apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="1d931-235"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="1d931-236">Kde **WebApplication1** je název vašeho projektu a **bindingInformation** obsahuje číslo portu a plně kvalifikovaný název domény, které chcete použít pro testování.</span><span class="sxs-lookup"><span data-stu-id="1d931-236">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="1d931-237">Jak získat nastavení aplikace pro ověřování Microsoftu</span><span class="sxs-lookup"><span data-stu-id="1d931-237">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="1d931-238">Propojení aplikace s Windows Live pro ověřování Microsoft je jednoduchý proces.</span><span class="sxs-lookup"><span data-stu-id="1d931-238">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="1d931-239">Pokud jste ještě nepřipojili aplikaci k Windows Live, můžete použít následující postup:</span><span class="sxs-lookup"><span data-stu-id="1d931-239">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="1d931-240">Po zobrazení výzvy vyhledejte [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) a zadejte své účet Microsoft jméno a heslo a pak klikněte na **Přihlásit**se:</span><span class="sxs-lookup"><span data-stu-id="1d931-240">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. <span data-ttu-id="1d931-241">Vyberte **Přidat aplikaci** a po zobrazení výzvy zadejte název aplikace a potom klikněte na **vytvořit**:</span><span class="sxs-lookup"><span data-stu-id="1d931-241">Select **Add an app** and enter the name of your application when prompted, and then click **Create**:</span></span>

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. <span data-ttu-id="1d931-242">V části **název** a jeho vlastnosti aplikace vyberte svou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="1d931-242">Select your app under **Name** and its application properties page appears.</span></span>

4. <span data-ttu-id="1d931-243">Zadejte doménu přesměrování vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="1d931-243">Enter the redirect domain for your application.</span></span> <span data-ttu-id="1d931-244">Zkopírujte **ID aplikace** a v části **tajné klíče aplikace**vyberte **generovat heslo**.</span><span class="sxs-lookup"><span data-stu-id="1d931-244">Copy the **Application ID** and, under **Application Secrets**, select **Generate Password**.</span></span> <span data-ttu-id="1d931-245">Zkopírujte heslo, které se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="1d931-245">Copy the password that appears.</span></span> <span data-ttu-id="1d931-246">ID a heslo aplikace jsou ID klienta a tajný klíč klienta.</span><span class="sxs-lookup"><span data-stu-id="1d931-246">The application ID and password are your client ID and client secret.</span></span> <span data-ttu-id="1d931-247">Vyberte **OK** a pak ho **uložte**.</span><span class="sxs-lookup"><span data-stu-id="1d931-247">Select **Ok** and then **Save**.</span></span>

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="1d931-248">Volitelné: zakázat místní registraci</span><span class="sxs-lookup"><span data-stu-id="1d931-248">Optional: Disable Local Registration</span></span>

<span data-ttu-id="1d931-249">Aktuální funkce místní registrace ASP.NET nezabrání v vytváření členských účtů automatizovaným programům (roboty). například pomocí technologie prevence a ověřování robota, jako je [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span><span class="sxs-lookup"><span data-stu-id="1d931-249">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="1d931-250">Z tohoto důvodu byste měli na přihlašovací stránce odebrat místní přihlašovací formulář a odkaz na registraci.</span><span class="sxs-lookup"><span data-stu-id="1d931-250">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="1d931-251">Provedete to tak, že otevřete stránku *\_Login. cshtml* v projektu a pak na řádek zadáte komentář k místnímu přihlašovacímu panelu a odkazu na registraci.</span><span class="sxs-lookup"><span data-stu-id="1d931-251">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="1d931-252">Výsledná stránka by měla vypadat jako následující ukázka kódu:</span><span class="sxs-lookup"><span data-stu-id="1d931-252">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="1d931-253">Po zakázání místního přihlašovacího panelu a registračního odkazu se na přihlašovací stránce zobrazí jenom externí poskytovatelé ověřování, které jste povolili:</span><span class="sxs-lookup"><span data-stu-id="1d931-253">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
