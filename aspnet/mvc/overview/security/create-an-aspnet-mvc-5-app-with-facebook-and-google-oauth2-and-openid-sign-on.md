---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Vytvoření aplikace MVC 5 pomocí služby Facebook, Twitter, LinkedIn a Google OAuth2 Signing (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5, která uživatelům umožňuje přihlásit se pomocí OAuth 2,0 s přihlašovacími údaji z externího předběžné...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566078"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="cdada-103">Vytvoření aplikace ASP.NET MVC 5 s přihlášením přes Facebook, Twitter, LinkedIn a Google OAuth2 (C#)</span><span class="sxs-lookup"><span data-stu-id="cdada-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="cdada-104">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cdada-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="cdada-105">V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5, která uživatelům umožňuje přihlásit se pomocí [OAuth 2,0](http://oauth.net/2/) s přihlašovacími údaji od externího poskytovatele ověřování, jako je Facebook, Twitter, LinkedIn, Microsoft nebo Google.</span><span class="sxs-lookup"><span data-stu-id="cdada-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="cdada-106">V zájmu zjednodušení se tento kurz zaměřuje na práci s přihlašovacími údaji z Facebooku a Google.</span><span class="sxs-lookup"><span data-stu-id="cdada-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="cdada-107">Povolení těchto přihlašovacích údajů na webech přináší významnou výhodu, protože miliony uživatelů již mají účty s těmito externími poskytovateli.</span><span class="sxs-lookup"><span data-stu-id="cdada-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="cdada-108">Tito uživatelé můžou být přihlášeni k vašemu webu, pokud je nepotřebují vytvořit a zapamatovat si novou sadu přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="cdada-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="cdada-109">Viz také [aplikace ASP.NET MVC 5 se serverem SMS a e-mailovým ověřováním pomocí e-mailu](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cdada-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="cdada-110">Tento kurz také ukazuje, jak přidat data profilu pro uživatele a jak používat rozhraní API pro členství k přidávání rolí.</span><span class="sxs-lookup"><span data-stu-id="cdada-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="cdada-111">Tento kurz napsal [Rick Anderson](https://blogs.msdn.com/rickAndy) (pořiďte prosím na Twitteru: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="cdada-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="cdada-112">začínáme</span><span class="sxs-lookup"><span data-stu-id="cdada-112">Getting Started</span></span>

<span data-ttu-id="cdada-113">Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="cdada-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="cdada-114">Nainstalujte Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="cdada-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="cdada-115">Nápovědu k Dropboxu, GitHubu, LinkedInu, Instagramu, vyrovnávací paměti, Salesforce, pára, výměně zásobníku, TripIt, Twitch, Twitteru, Yahoo! a dalším službám najdete v tomto [ukázkovém projektu](https://github.com/matthewdunsdon/oauthforaspnet).</span><span class="sxs-lookup"><span data-stu-id="cdada-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="cdada-116">Pokud chcete používat Google OAuth 2 a ladit místně bez upozornění SSL, musíte nainstalovat Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="cdada-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="cdada-117">Na **úvodní** stránce klikněte na **Nový projekt** , nebo můžete použít nabídku a vybrat **soubor**a pak **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="cdada-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="cdada-118">Vytvoření první aplikace</span><span class="sxs-lookup"><span data-stu-id="cdada-118">Creating Your First Application</span></span>

<span data-ttu-id="cdada-119">Klikněte **na nový projekt** **, pak na** levé straně vyberte **vizuál C#**  a potom vyberte **Webová aplikace ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="cdada-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="cdada-120">Pojmenujte projekt "MvcAuth" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdada-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="cdada-121">V dialogovém okně **Nový projekt ASP.NET** klikněte na **MVC**.</span><span class="sxs-lookup"><span data-stu-id="cdada-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="cdada-122">Pokud ověřování neplatí pro **jednotlivé uživatelské účty**, klikněte na tlačítko **změnit ověřování** a vyberte **jednotlivé uživatelské účty**.</span><span class="sxs-lookup"><span data-stu-id="cdada-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="cdada-123">Když zkontrolujete **hostitele v cloudu**, aplikace bude velmi snadná pro hostování v Azure.</span><span class="sxs-lookup"><span data-stu-id="cdada-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="cdada-124">Pokud jste vybrali možnost **hostitel v cloudu**, dokončete dialog konfigurace.</span><span class="sxs-lookup"><span data-stu-id="cdada-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="cdada-125">Použití NuGet k aktualizaci na nejnovější middleware OWIN</span><span class="sxs-lookup"><span data-stu-id="cdada-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="cdada-126">Pomocí Správce balíčků NuGet aktualizujte [middleware Owin](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span><span class="sxs-lookup"><span data-stu-id="cdada-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="cdada-127">V nabídce vlevo vyberte **aktualizace** .</span><span class="sxs-lookup"><span data-stu-id="cdada-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="cdada-128">Můžete kliknout na tlačítko **Aktualizovat vše** nebo můžete vyhledat jenom Owin balíčky (zobrazené na následujícím obrázku):</span><span class="sxs-lookup"><span data-stu-id="cdada-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="cdada-129">Na následujícím obrázku jsou zobrazeny pouze balíčky OWIN:</span><span class="sxs-lookup"><span data-stu-id="cdada-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="cdada-130">V konzole správce balíčků (PMC) můžete zadat příkaz `Update-Package`, který bude aktualizovat všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="cdada-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="cdada-131">Spusťte aplikaci stisknutím klávesy **F5** nebo **kombinací kláves CTRL + F5** .</span><span class="sxs-lookup"><span data-stu-id="cdada-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="cdada-132">Na následujícím obrázku je číslo portu 1234.</span><span class="sxs-lookup"><span data-stu-id="cdada-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="cdada-133">Při spuštění aplikace se zobrazí jiné číslo portu.</span><span class="sxs-lookup"><span data-stu-id="cdada-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="cdada-134">V závislosti na velikosti okna prohlížeče možná budete muset kliknout na navigační ikonu, aby se zobrazily odkazy **Domů**, **informace**, **kontakt**, **registrace** a **přihlášení** .</span><span class="sxs-lookup"><span data-stu-id="cdada-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="cdada-135">Nastavení SSL v projektu</span><span class="sxs-lookup"><span data-stu-id="cdada-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="cdada-136">Pokud se chcete připojit k poskytovatelům ověřování, jako je Google a Facebook, budete muset nastavit službu IIS Express, aby používala protokol SSL.</span><span class="sxs-lookup"><span data-stu-id="cdada-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="cdada-137">Je důležité, abyste po přihlášení používali protokol SSL a nevrátili se zpátky na HTTP. váš přihlašovací soubor cookie je stejně tajný jako uživatelské jméno a heslo a bez použití protokolu SSL, který odesíláte do prostého textu po celém drátě.</span><span class="sxs-lookup"><span data-stu-id="cdada-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="cdada-138">Kromě toho už jste popsali čas k provedení metody handshake a zabezpečení kanálu (což je hromadný protokol HTTPS, než HTTP) předtím, než se spustí kanál MVC, takže se po přihlášení znovu přesměruje na protokol HTTP, a to tak, že se aktuální žádost nebo budoucnost neuplatní. požadavky jsou mnohem rychlejší.</span><span class="sxs-lookup"><span data-stu-id="cdada-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="cdada-139">V **Průzkumník řešení**klikněte na projekt **MvcAuth** .</span><span class="sxs-lookup"><span data-stu-id="cdada-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="cdada-140">Stiskněte klávesu F4 pro zobrazení vlastností projektu.</span><span class="sxs-lookup"><span data-stu-id="cdada-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="cdada-141">Případně můžete v nabídce **zobrazení** vybrat **okno Vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="cdada-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="cdada-142">Změňte možnost **SSL povoleno** na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="cdada-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="cdada-143">Zkopírujte adresu URL SSL (která bude `https://localhost:44300/`, pokud jste nevytvořili jiné projekty SSL).</span><span class="sxs-lookup"><span data-stu-id="cdada-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="cdada-144">V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **MvcAuth** a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="cdada-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="cdada-145">Vyberte kartu **Web** a pak vložte adresu URL SSL do pole **Adresa URL projektu** .</span><span class="sxs-lookup"><span data-stu-id="cdada-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="cdada-146">Uložte soubor (CTL + S).</span><span class="sxs-lookup"><span data-stu-id="cdada-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="cdada-147">Tuto adresu URL budete potřebovat ke konfiguraci aplikací pro Facebook a Google Authentication.</span><span class="sxs-lookup"><span data-stu-id="cdada-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="cdada-148">Přidejte atribut [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) do kontroleru `Home`, aby se vyžadovalo, aby všechny požadavky měly používat protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cdada-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="cdada-149">Bezpečnějším přístupem je přidání filtru [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) do aplikace.</span><span class="sxs-lookup"><span data-stu-id="cdada-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="cdada-150">Přečtěte si část &quot;Ochrana aplikace pomocí protokolu SSL a&quot; autorizace atributu v tomto kurzu [vytvořte aplikaci ASP.NET MVC s ověřováním a SQL DB a nasaďte ji do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="cdada-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="cdada-151">Část domovského kontroleru je uvedená níže.</span><span class="sxs-lookup"><span data-stu-id="cdada-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="cdada-152">Stiskněte klávesy CTRL+F5 a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="cdada-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="cdada-153">Pokud jste certifikát nainstalovali v minulosti, můžete přeskočit zbytek této části a přejít na [Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu](#goog), jinak postupujte podle pokynů pro důvěřování certifikátu podepsanému svým držitelem, který IIS Express vygeneroval.</span><span class="sxs-lookup"><span data-stu-id="cdada-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="cdada-154">Přečtěte si dialogové okno **Upozornění zabezpečení** a pak klikněte na tlačítko **Ano** , pokud chcete nainstalovat certifikát reprezentující localhost.</span><span class="sxs-lookup"><span data-stu-id="cdada-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="cdada-155">Aplikace IE zobrazuje *domovskou* stránku a neexistují žádná upozornění SSL.</span><span class="sxs-lookup"><span data-stu-id="cdada-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="cdada-156">Google Chrome také akceptuje certifikát a zobrazí obsah HTTPS bez upozornění.</span><span class="sxs-lookup"><span data-stu-id="cdada-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="cdada-157">Firefox používá vlastní úložiště certifikátů, takže zobrazí upozornění.</span><span class="sxs-lookup"><span data-stu-id="cdada-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="cdada-158">V případě naší aplikace můžete bezpečně kliknout na možnost **rozumím rizikům**.</span><span class="sxs-lookup"><span data-stu-id="cdada-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="cdada-159">Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="cdada-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="cdada-160">Informace o aktuálních pokynech k Google OAuth najdete [v tématu Konfigurace ověřování Google v ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="cdada-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="cdada-161">Přejděte do [konzoly pro vývojáře Google](https://console.developers.google.com/).</span><span class="sxs-lookup"><span data-stu-id="cdada-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="cdada-162">Pokud jste projekt ještě nevytvořili, vyberte na levé kartě možnost **přihlašovací údaje** a pak vyberte **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="cdada-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="cdada-163">Na levé kartě klikněte na **přihlašovací údaje**.</span><span class="sxs-lookup"><span data-stu-id="cdada-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="cdada-164">Klikněte na **vytvořit přihlašovací údaje** a pak na **ID klienta OAuth**.</span><span class="sxs-lookup"><span data-stu-id="cdada-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="cdada-165">V dialogovém okně **vytvořit ID klienta** ponechte výchozí **webovou aplikaci** pro typ aplikace.</span><span class="sxs-lookup"><span data-stu-id="cdada-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="cdada-166">Nastavte **ověřené zdroje JavaScriptu** na adresu URL SSL, kterou jste použili výše (`https://localhost:44300/`, pokud jste nevytvořili jiné projekty SSL).</span><span class="sxs-lookup"><span data-stu-id="cdada-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="cdada-167">Nastavte **autorizovaný identifikátor URI pro přesměrování** na:</span><span class="sxs-lookup"><span data-stu-id="cdada-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="cdada-168">Klikněte na položku nabídky obrazovka pro vyjádření souhlasu OAuth a pak nastavte svou e-mailovou adresu a název produktu.</span><span class="sxs-lookup"><span data-stu-id="cdada-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="cdada-169">Po vyplnění formuláře klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="cdada-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="cdada-170">Klikněte na položku nabídky knihovna, vyhledejte **Google + API**, klikněte na ni a potom stiskněte povolit.</span><span class="sxs-lookup"><span data-stu-id="cdada-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="cdada-171">Následující obrázek ukazuje povolená rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="cdada-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="cdada-172">Ve Správci rozhraní API Google API navštivte kartu **přihlašovací údaje** a získejte **ID klienta**.</span><span class="sxs-lookup"><span data-stu-id="cdada-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="cdada-173">Stáhněte si a uložte soubor JSON s použitím tajných klíčů.</span><span class="sxs-lookup"><span data-stu-id="cdada-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="cdada-174">Zkopírujte a vložte **ClientID** a **ClientSecret** do metody `UseGoogleAuthentication` nalezené v souboru *Startup.auth.cs* ve složce *app_start* .</span><span class="sxs-lookup"><span data-stu-id="cdada-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="cdada-175">Níže uvedené hodnoty **ClientID** a **ClientSecret** jsou ukázky a nefungují.</span><span class="sxs-lookup"><span data-stu-id="cdada-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="cdada-176">Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="cdada-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="cdada-177">Účet a přihlašovací údaje se přidají do výše uvedeného kódu, aby se ukázka snadno zachovala.</span><span class="sxs-lookup"><span data-stu-id="cdada-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="cdada-178">Další informace najdete v tématu [osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cdada-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="cdada-179">Stisknutím **kombinace kláves CTRL + F5** Sestavte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="cdada-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="cdada-180">Klikněte na odkaz **Přihlásit** se.</span><span class="sxs-lookup"><span data-stu-id="cdada-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="cdada-181">V části **použít jinou službu pro přihlášení**klikněte na **Google**.</span><span class="sxs-lookup"><span data-stu-id="cdada-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="cdada-182">Pokud jste si nedostali některý z výše uvedených kroků, dojde k chybě HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="cdada-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="cdada-183">Překontrolujte výše uvedené kroky.</span><span class="sxs-lookup"><span data-stu-id="cdada-183">Recheck your steps above.</span></span> <span data-ttu-id="cdada-184">Pokud nejste požádáni o nastavení (například **název produktu**), přidejte chybějící položku a uložte ji. aby ověřování fungovalo, může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="cdada-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="cdada-185">Budete přesměrováni na web Google, kam budete zadávat své přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="cdada-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="cdada-186">Po zadání přihlašovacích údajů se zobrazí výzva k udělení oprávnění k této webové aplikaci, kterou jste právě vytvořili:</span><span class="sxs-lookup"><span data-stu-id="cdada-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="cdada-187">Klikněte na **přijmout**.</span><span class="sxs-lookup"><span data-stu-id="cdada-187">Click **Accept**.</span></span> <span data-ttu-id="cdada-188">Nyní budete přesměrováni zpět na stránku **registrace** aplikace MvcAuth, kde můžete zaregistrovat svůj účet Google.</span><span class="sxs-lookup"><span data-stu-id="cdada-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="cdada-189">Máte možnost změnit název místní registrace e-mailu, který se používá pro váš účet Gmail, ale obecně chcete zachovat výchozí alias e-mailu (tj. ten, který jste použili pro ověřování).</span><span class="sxs-lookup"><span data-stu-id="cdada-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="cdada-190">Klikněte na **zaregistrovat**.</span><span class="sxs-lookup"><span data-stu-id="cdada-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="cdada-191">Vytvoření aplikace na Facebooku a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="cdada-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="cdada-192">Pokyny k aktuálním OAuth2 ověřování na Facebooku najdete v tématu [Konfigurace ověřování na Facebooku](/aspnet/core/security/authentication/social/facebook-logins) .</span><span class="sxs-lookup"><span data-stu-id="cdada-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="cdada-193">Prověřte data členství</span><span class="sxs-lookup"><span data-stu-id="cdada-193">Examine the Membership Data</span></span>

<span data-ttu-id="cdada-194">V nabídce **zobrazení** klikněte na příkaz **Průzkumník serveru**.</span><span class="sxs-lookup"><span data-stu-id="cdada-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="cdada-195">Rozbalte položku **DefaultConnection (MvcAuth)** , rozbalte položku **tabulky**, klikněte pravým tlačítkem myši na položku **AspNetUsers** a klikněte na možnost **Zobrazit data tabulky**.</span><span class="sxs-lookup"><span data-stu-id="cdada-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![data tabulky aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="cdada-197">Přidání dat profilu do třídy uživatele</span><span class="sxs-lookup"><span data-stu-id="cdada-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="cdada-198">V této části přidáte k uživatelským datům během registrace datum narození a domovské město, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="cdada-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![REG s domovským městem a bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="cdada-200">Otevřete soubor *Models\IdentityModels.cs* a přidejte vlastnosti rodného data a domovské města:</span><span class="sxs-lookup"><span data-stu-id="cdada-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="cdada-201">Otevřete soubor *Models\AccountViewModels.cs* a nastavte vlastnosti rodného data a domovské města v `ExternalLoginConfirmationViewModel`.</span><span class="sxs-lookup"><span data-stu-id="cdada-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="cdada-202">Otevřete soubor *Controllers\AccountController.cs* a přidejte kód pro datum narození a domovské město v metodě `ExternalLoginConfirmation` akce, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="cdada-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="cdada-203">Přidejte datum narození a domovské město do souboru *Views\Account\ExternalLoginConfirmation.cshtml* :</span><span class="sxs-lookup"><span data-stu-id="cdada-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="cdada-204">Odstraňte databázi členství, abyste mohli znovu zaregistrovat svůj účet Facebook s vaší aplikací a ověřit, že můžete přidat nové informace o profilu narození a domovské města.</span><span class="sxs-lookup"><span data-stu-id="cdada-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="cdada-205">Z **Průzkumník řešení**klikněte na ikonu **Zobrazit všechny soubory** , klikněte pravým tlačítkem na *přidat\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;. mdf* a klikněte na **Odstranit**.</span><span class="sxs-lookup"><span data-stu-id="cdada-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="cdada-206">V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků** (PMC).</span><span class="sxs-lookup"><span data-stu-id="cdada-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="cdada-207">Do PMC zadejte následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="cdada-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="cdada-208">Povolit – migrace</span><span class="sxs-lookup"><span data-stu-id="cdada-208">Enable-Migrations</span></span>
2. <span data-ttu-id="cdada-209">Inicializace přidání – migrace</span><span class="sxs-lookup"><span data-stu-id="cdada-209">Add-Migration Init</span></span>
3. <span data-ttu-id="cdada-210">Aktualizace – databáze</span><span class="sxs-lookup"><span data-stu-id="cdada-210">Update-Database</span></span>

<span data-ttu-id="cdada-211">Spusťte aplikaci a pomocí Facebooku a Google se přihlaste a zaregistrujte některé uživatele.</span><span class="sxs-lookup"><span data-stu-id="cdada-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="cdada-212">Prověřte data členství</span><span class="sxs-lookup"><span data-stu-id="cdada-212">Examine the Membership Data</span></span>

<span data-ttu-id="cdada-213">V nabídce **zobrazení** klikněte na příkaz **Průzkumník serveru**.</span><span class="sxs-lookup"><span data-stu-id="cdada-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="cdada-214">Klikněte pravým tlačítkem na **AspNetUsers** a pak klikněte na **Zobrazit data tabulky**.</span><span class="sxs-lookup"><span data-stu-id="cdada-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="cdada-215">Pole `HomeTown` a `BirthDate` jsou uvedena níže.</span><span class="sxs-lookup"><span data-stu-id="cdada-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="cdada-216">Odhlášení aplikace a přihlášení pomocí jiného účtu</span><span class="sxs-lookup"><span data-stu-id="cdada-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="cdada-217">Pokud se přihlásíte k aplikaci přes Facebook, a pak se odhlásíte a zkusíte se přihlásit pomocí jiného účtu Facebook (pomocí stejného prohlížeče), budete k němu přihlášeni hned přes předchozí účet Facebook, který jste použili.</span><span class="sxs-lookup"><span data-stu-id="cdada-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="cdada-218">Aby bylo možné použít jiný účet, musíte přejít na Facebook a odhlásit se v Facebooku.</span><span class="sxs-lookup"><span data-stu-id="cdada-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="cdada-219">Stejné pravidlo platí pro všechny ostatní poskytovatele ověřování třetí strany.</span><span class="sxs-lookup"><span data-stu-id="cdada-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="cdada-220">Případně se můžete přihlásit pomocí jiného účtu pomocí jiného prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="cdada-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdada-221">Další kroky</span><span class="sxs-lookup"><span data-stu-id="cdada-221">Next Steps</span></span>

<span data-ttu-id="cdada-222">Pokyny pro Yahoo a LinkedIn najdete v tématu [představení zprostředkovatelů zabezpečení Yahoo a LinkedIn OAuth pro Owin](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) pomocí Jerrie Pelser.</span><span class="sxs-lookup"><span data-stu-id="cdada-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="cdada-223">Pokud chcete získat tlačítka pro přihlášení přes sociální sítě, přečtěte si část Jerrie – tlačítka pro přihlášení k ASP.NET MVC 5.</span><span class="sxs-lookup"><span data-stu-id="cdada-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="cdada-224">Postupujte podle kurzu [Vytvoření aplikace ASP.NET MVC s ověřováním a SQL DB a nasaďte ji do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), která pokračuje v tomto kurzu a zobrazí se následující:</span><span class="sxs-lookup"><span data-stu-id="cdada-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="cdada-225">Jak nasadit aplikaci do Azure</span><span class="sxs-lookup"><span data-stu-id="cdada-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="cdada-226">Jak zabezpečit aplikaci pomocí rolí.</span><span class="sxs-lookup"><span data-stu-id="cdada-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="cdada-227">Jak zabezpečit aplikaci pomocí [atribut RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) a [autorizovat](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filtry.</span><span class="sxs-lookup"><span data-stu-id="cdada-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="cdada-228">Jak používat rozhraní API pro členství k přidávání uživatelů a rolí.</span><span class="sxs-lookup"><span data-stu-id="cdada-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="cdada-229">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit.</span><span class="sxs-lookup"><span data-stu-id="cdada-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="cdada-230">Můžete také požádat o nová témata při [zobrazení kódu](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span><span class="sxs-lookup"><span data-stu-id="cdada-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="cdada-231">Můžete dokonce požádat o nové funkce, které se mají přidat do ASP.NET, a hlasovat o nich.</span><span class="sxs-lookup"><span data-stu-id="cdada-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="cdada-232">Můžete například hlasovat pro nástroj k [vytváření a správě uživatelů a rolí.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="cdada-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="cdada-233">Dobré vysvětlení, jak služba ASP.NET External Authentication Services funguje, najdete v tématu věnovaném [externím ověřovacím službám](https://asp.net/web-api/overview/security/external-authentication-services)Robert blog.</span><span class="sxs-lookup"><span data-stu-id="cdada-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="cdada-234">Článek Robert také podrobně popisuje, jak povolit ověřování Microsoft a Twitter.</span><span class="sxs-lookup"><span data-stu-id="cdada-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="cdada-235">Skvělého kurzu pro Dykstra [EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) ukazuje, jak pracovat s Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="cdada-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
