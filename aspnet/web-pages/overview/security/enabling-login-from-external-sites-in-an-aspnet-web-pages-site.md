---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: Přihlášení pomocí externích webů na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek vysvětluje, jak se přihlásit k webu ASP.NET Web Pages (Razor) pomocí Facebooku, Google, Twitteru, Yahoo a dalších webů – to znamená, jak podporovat...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638752"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="bd825-103">Přihlášení pomocí externích webů na webu ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="bd825-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="bd825-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bd825-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bd825-105">Tento článek vysvětluje, jak se přihlásit k webu ASP.NET Web Pages (Razor) pomocí Facebooku, Google, Twitteru, Yahoo a dalších webů – to znamená, jak podporovat OAuth a OpenID ve vaší lokalitě.</span><span class="sxs-lookup"><span data-stu-id="bd825-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="bd825-106">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="bd825-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="bd825-107">Jak povolit přihlášení z jiných webů při použití šablony webu WebMatrix Starter</span><span class="sxs-lookup"><span data-stu-id="bd825-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="bd825-108">Toto je funkce ASP.NET představená v článku:</span><span class="sxs-lookup"><span data-stu-id="bd825-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="bd825-109">Pomocná rutina `OAuthWebSecurity`</span><span class="sxs-lookup"><span data-stu-id="bd825-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bd825-110">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="bd825-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bd825-111">Webové stránky ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="bd825-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="bd825-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="bd825-112">WebMatrix 3</span></span>

<span data-ttu-id="bd825-113">Webové stránky ASP.NET zahrnují podporu pro poskytovatele [OAuth](http://oauth.net/) a [OpenID](http://openid.net/) .</span><span class="sxs-lookup"><span data-stu-id="bd825-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="bd825-114">Pomocí těchto poskytovatelů můžete uživatelům umožnit, aby se k webu přihlásili pomocí svých stávajících přihlašovacích údajů z Facebooku, Twitteru, Microsoftu a Google.</span><span class="sxs-lookup"><span data-stu-id="bd825-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="bd825-115">Například pro přihlášení pomocí účtu Facebook mohou uživatelé vybrat ikonu Facebook, která je přesměruje na přihlašovací stránku Facebooku, kde zadá informace o uživateli.</span><span class="sxs-lookup"><span data-stu-id="bd825-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="bd825-116">Pak můžou přidružit přihlášení ke službě Facebook ke svému účtu na vašem webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="bd825-117">Související vylepšení funkcí členství na webových stránkách je, že uživatelé můžou přidružit k jednomu účtu na svém webu několik přihlášení (včetně přihlášení ze sítí sociální sítě).</span><span class="sxs-lookup"><span data-stu-id="bd825-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="bd825-118">Tento obrázek ukazuje přihlašovací stránku ze šablony **úvodní lokality** , kde si uživatel může vybrat ikonu Facebook, Twitter, Google nebo Microsoft a povolit přihlášení pomocí externího účtu:</span><span class="sxs-lookup"><span data-stu-id="bd825-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![externí zprostředkovatelé](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="bd825-120">Můžete povolit členství OAuth a OpenID tím, že Odkomentujete pár řádků kódu v šabloně **webu Starter** .</span><span class="sxs-lookup"><span data-stu-id="bd825-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="bd825-121">Metody a vlastnosti, které používáte pro práci s poskytovateli OAuth a OpenID, jsou v třídě `WebMatrix.Security.OAuthWebSecurity`.</span><span class="sxs-lookup"><span data-stu-id="bd825-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="bd825-122">Šablona **úvodní lokality** obsahuje úplnou infrastrukturu členství, úplnou na přihlašovací stránce, databázi členství a veškerý kód, který potřebujete, aby se uživatelé mohli přihlásit k webu pomocí místních přihlašovacích údajů nebo z jiné lokality.</span><span class="sxs-lookup"><span data-stu-id="bd825-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="bd825-123">V této části najdete příklad toho, jak umožnit uživatelům přihlašovat se z externích lokalit na lokalitu, která je založená na šabloně **webu Starter** .</span><span class="sxs-lookup"><span data-stu-id="bd825-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="bd825-124">Po vytvoření webu počáteční web to uděláte (podrobnosti následují):</span><span class="sxs-lookup"><span data-stu-id="bd825-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="bd825-125">Pro lokality, které používají poskytovatele OAuth (Facebook, Twitter a Microsoft), vytvoříte aplikaci na externím webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="bd825-126">Tím získáte klíče aplikací, které budete potřebovat k vyvolání funkce přihlášení pro tyto lokality.</span><span class="sxs-lookup"><span data-stu-id="bd825-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="bd825-127">Pro lokality, které používají poskytovatele OpenID (Google), není nutné vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="bd825-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="bd825-128">Pro všechny tyto weby musíte mít účet, abyste se mohli přihlásit a vytvářet vývojářské aplikace.</span><span class="sxs-lookup"><span data-stu-id="bd825-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd825-129">Aplikace Microsoftu přijímají pro pracovní web pouze živou adresu URL, takže pro testování přihlášení nemůžete použít adresu URL místního webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="bd825-130">Upravte několik souborů na webu za účelem určení vhodného poskytovatele ověřování a odeslání přihlašovacích údajů na lokalitu, kterou chcete použít.</span><span class="sxs-lookup"><span data-stu-id="bd825-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="bd825-131">Tento článek poskytuje samostatné pokyny pro následující úlohy:</span><span class="sxs-lookup"><span data-stu-id="bd825-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="bd825-132">Povolení přihlášení Google</span><span class="sxs-lookup"><span data-stu-id="bd825-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="bd825-133">Povolení přihlášení na Facebooku</span><span class="sxs-lookup"><span data-stu-id="bd825-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="bd825-134">Povolení přihlášení k Twitteru</span><span class="sxs-lookup"><span data-stu-id="bd825-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="bd825-135">Povolení přihlášení Google</span><span class="sxs-lookup"><span data-stu-id="bd825-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="bd825-136">Vytvořte nebo otevřete web ASP.NET Web Pages založený na šabloně webu WebMatrix Starter.</span><span class="sxs-lookup"><span data-stu-id="bd825-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="bd825-137">Otevřete stránku *\_AppStart. cshtml* a odkomentujte následující řádek kódu.</span><span class="sxs-lookup"><span data-stu-id="bd825-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="bd825-138">Testování přihlášení Google</span><span class="sxs-lookup"><span data-stu-id="bd825-138">Testing Google login</span></span>

1. <span data-ttu-id="bd825-139">Spusťte stránku *Default. cshtml* vaší lokality a klikněte na tlačítko **Přihlásit** se.</span><span class="sxs-lookup"><span data-stu-id="bd825-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="bd825-140">Na *přihlašovací* stránce v části **použít jinou službu pro přihlášení** vyberte tlačítko Odeslat **Google** nebo **Yahoo** .</span><span class="sxs-lookup"><span data-stu-id="bd825-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="bd825-141">V tomto příkladu se používá přihlášení Google.</span><span class="sxs-lookup"><span data-stu-id="bd825-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="bd825-142">Webová stránka přesměruje požadavek na přihlašovací stránku Google.</span><span class="sxs-lookup"><span data-stu-id="bd825-142">The web page redirects the request to the Google login page.</span></span>

    ![Přihlášení Google](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="bd825-144">Zadejte přihlašovací údaje pro existující účet Google.</span><span class="sxs-lookup"><span data-stu-id="bd825-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="bd825-145">Pokud se Google zeptá, jestli chcete, aby *localhost* mohl používat informace z účtu, klikněte na tlačítko **povoleno**.</span><span class="sxs-lookup"><span data-stu-id="bd825-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="bd825-146">Kód používá k ověření uživatele token Google a pak se na tuto stránku vrátí na vašem webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="bd825-147">Tato stránka umožňuje uživatelům přidružit ke stávajícímu účtu na vašem webu svoje přihlašovací údaje Google, nebo můžou zaregistrovat nový účet a přidružit k externímu přihlášení.</span><span class="sxs-lookup"><span data-stu-id="bd825-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="bd825-149">Klikněte na tlačítko **přidružit** .</span><span class="sxs-lookup"><span data-stu-id="bd825-149">Choose the **Associate** button.</span></span> <span data-ttu-id="bd825-150">Prohlížeč se vrátí na domovskou stránku vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="bd825-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="bd825-151">Povolení přihlášení na Facebooku</span><span class="sxs-lookup"><span data-stu-id="bd825-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="bd825-152">Přejít na [web pro vývojáře na Facebooku](https://developers.facebook.com/apps) (Přihlaste se, pokud ještě nejste přihlášení).</span><span class="sxs-lookup"><span data-stu-id="bd825-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="bd825-153">Klikněte na tlačítko **vytvořit novou aplikaci** a potom podle pokynů pojmenujte a vytvořte novou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="bd825-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="bd825-154">V části **Vyberte, jak bude vaše aplikace integrována s Facebooku**, a zvolte část **Web** .</span><span class="sxs-lookup"><span data-stu-id="bd825-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="bd825-155">Do pole **Adresa URL webu** zadejte adresu URL vašeho webu (například `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="bd825-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="bd825-156">Pole **doména** je volitelné. tuto možnost můžete použít k zajištění ověřování pro celou doménu (například *example.com*).</span><span class="sxs-lookup"><span data-stu-id="bd825-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="bd825-157">Pokud používáte web na místním počítači s adresou URL, jako je například `http://localhost:12345` (kde číslo je číslo místního portu), můžete tuto hodnotu přidat do pole **Adresa URL webu** pro testování webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="bd825-158">Při každé změně čísla portu v místní lokalitě budete ale muset aktualizovat pole **Adresa URL webu** vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="bd825-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="bd825-159">Klikněte na tlačítko **Uložit změny** .</span><span class="sxs-lookup"><span data-stu-id="bd825-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="bd825-160">Zvolte znovu kartu **aplikace** a pak zobrazte úvodní stránku aplikace.</span><span class="sxs-lookup"><span data-stu-id="bd825-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="bd825-161">Zkopírujte **ID aplikace** a **tajné** hodnoty pro aplikaci a vložte je do dočasného textového souboru.</span><span class="sxs-lookup"><span data-stu-id="bd825-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="bd825-162">Tyto hodnoty předáte poskytovateli Facebooku ve vašem kódu webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="bd825-163">Zavřete web pro vývojáře Facebooku.</span><span class="sxs-lookup"><span data-stu-id="bd825-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="bd825-164">Teď provedete změny dvou stránek na webu tak, aby se uživatelé mohli přihlásit k webu pomocí svých účtů Facebook.</span><span class="sxs-lookup"><span data-stu-id="bd825-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="bd825-165">Vytvořte nebo otevřete web ASP.NET Web Pages založený na šabloně webu WebMatrix Starter.</span><span class="sxs-lookup"><span data-stu-id="bd825-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="bd825-166">Otevřete stránku *\_AppStart. cshtml* a Odkomentujte kód pro poskytovatele OAuth pro Facebook.</span><span class="sxs-lookup"><span data-stu-id="bd825-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="bd825-167">Blok kódu, který není v komentáři, vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="bd825-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="bd825-168">Zkopírujte hodnotu **ID aplikace** z aplikace Facebook jako hodnotu parametru `appId` (uvnitř uvozovek).</span><span class="sxs-lookup"><span data-stu-id="bd825-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="bd825-169">Zkopírujte hodnotu **tajného klíče aplikace** z aplikace Facebook jako hodnotu parametru `appSecret`.</span><span class="sxs-lookup"><span data-stu-id="bd825-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="bd825-170">Uložte soubor a zavřete ho.</span><span class="sxs-lookup"><span data-stu-id="bd825-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="bd825-171">Testování přihlašovacích údajů Facebooku</span><span class="sxs-lookup"><span data-stu-id="bd825-171">Testing Facebook login</span></span>

1. <span data-ttu-id="bd825-172">Spusťte stránku *Default. cshtml* webu a klikněte na tlačítko **Přihlásit** .</span><span class="sxs-lookup"><span data-stu-id="bd825-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="bd825-173">Na *přihlašovací* stránce v části **použít jinou službu pro přihlášení** vyberte ikonu **Facebook** .</span><span class="sxs-lookup"><span data-stu-id="bd825-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="bd825-174">Webová stránka přesměruje požadavek na přihlašovací stránku Facebooku.</span><span class="sxs-lookup"><span data-stu-id="bd825-174">The web page redirects the request to the Facebook login page.</span></span>

    ![OAuth – 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="bd825-176">Přihlaste se k účtu Facebook.</span><span class="sxs-lookup"><span data-stu-id="bd825-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="bd825-177">Kód používá token Facebooku k ověření a pak se vrátí na stránku, kde můžete přidružit své přihlášení ke službě Facebook k přihlašovacím údajům vašeho webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="bd825-178">Vaše uživatelské jméno nebo e-mailová adresa se vyplní do pole **e-mail** ve formuláři.</span><span class="sxs-lookup"><span data-stu-id="bd825-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="bd825-180">Klikněte na tlačítko **přidružit** .</span><span class="sxs-lookup"><span data-stu-id="bd825-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="bd825-181">Prohlížeč se vrátí na domovskou stránku a Vy jste přihlášení.</span><span class="sxs-lookup"><span data-stu-id="bd825-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="bd825-182">Povolení přihlášení k Twitteru</span><span class="sxs-lookup"><span data-stu-id="bd825-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="bd825-183">Přejděte na [web pro vývojáře na Twitteru](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="bd825-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="bd825-184">Zvolte odkaz **vytvořit aplikaci** a pak se přihlaste k webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="bd825-185">Ve formuláři **vytvořit aplikaci** vyplňte pole **název** a **Popis** .</span><span class="sxs-lookup"><span data-stu-id="bd825-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="bd825-186">Do pole **Web** zadejte adresu URL vašeho webu (například `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="bd825-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="bd825-187">Pokud testujete lokalitu místně (pomocí adresy URL, jako je `http://localhost:12345`), Twitter nemusí přijmout adresu URL.</span><span class="sxs-lookup"><span data-stu-id="bd825-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="bd825-188">Může ale být možné použít IP adresu místní zpětné smyčky (například `http://127.0.0.1:12345`).</span><span class="sxs-lookup"><span data-stu-id="bd825-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="bd825-189">Tím se zjednoduší proces testování aplikace místně.</span><span class="sxs-lookup"><span data-stu-id="bd825-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="bd825-190">Pokaždé, když se změní číslo portu místní lokality, budete muset aktualizovat pole **Web** vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="bd825-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="bd825-191">V poli **Adresa URL zpětného volání** zadejte adresu URL stránky na webu, na kterou se mají uživatelé vracet po přihlášení do Twitteru.</span><span class="sxs-lookup"><span data-stu-id="bd825-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="bd825-192">Chcete-li například odeslat uživatele na domovskou stránku úvodní lokality (která rozpozná jejich stav přihlášení), zadejte stejnou adresu URL, kterou jste zadali do pole **Web** .</span><span class="sxs-lookup"><span data-stu-id="bd825-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="bd825-193">Přijměte podmínky a klikněte na tlačítko **vytvořit aplikaci Twitter** .</span><span class="sxs-lookup"><span data-stu-id="bd825-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="bd825-194">Na úvodní stránce **Moje aplikace** vyberte aplikaci, kterou jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="bd825-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="bd825-195">Na kartě **Podrobnosti** se posuňte do dolní části a klikněte na tlačítko **vytvořit vlastní přístupový token** .</span><span class="sxs-lookup"><span data-stu-id="bd825-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="bd825-196">Na kartě **Podrobnosti** zkopírujte **klíč příjemce** a **tajné hodnoty příjemce** pro vaši aplikaci a vložte je do dočasného textového souboru.</span><span class="sxs-lookup"><span data-stu-id="bd825-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="bd825-197">Tyto hodnoty předáte poskytovateli Twitteru v kódu vašeho webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="bd825-198">Ukončete Web Twitter.</span><span class="sxs-lookup"><span data-stu-id="bd825-198">Exit the Twitter site.</span></span>

<span data-ttu-id="bd825-199">Teď provedete změny dvou stránek na webu tak, aby se uživatelé mohli přihlásit k webu pomocí svých účtů Twitteru.</span><span class="sxs-lookup"><span data-stu-id="bd825-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="bd825-200">Vytvořte nebo otevřete web ASP.NET Web Pages založený na šabloně webu WebMatrix Starter.</span><span class="sxs-lookup"><span data-stu-id="bd825-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="bd825-201">Otevřete stránku *\_AppStart. cshtml* a Odkomentujte kód pro poskytovatele služby Twitter OAuth.</span><span class="sxs-lookup"><span data-stu-id="bd825-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="bd825-202">Blok kódu, který není v komentáři, vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="bd825-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="bd825-203">Zkopírujte hodnotu **klíč příjemce** z aplikace Twitter jako hodnotu parametru `consumerKey` (uvnitř uvozovek).</span><span class="sxs-lookup"><span data-stu-id="bd825-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="bd825-204">Zkopírujte hodnotu **tajného klíče příjemce** z aplikace Twitter jako hodnotu parametru `consumerSecret`.</span><span class="sxs-lookup"><span data-stu-id="bd825-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="bd825-205">Uložte soubor a zavřete ho.</span><span class="sxs-lookup"><span data-stu-id="bd825-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="bd825-206">Testování přihlášení k Twitteru</span><span class="sxs-lookup"><span data-stu-id="bd825-206">Testing Twitter login</span></span>

1. <span data-ttu-id="bd825-207">Spusťte stránku *Default. cshtml* vaší lokality a klikněte na tlačítko pro **přihlášení** .</span><span class="sxs-lookup"><span data-stu-id="bd825-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="bd825-208">Na *přihlašovací* stránce v části **použít jinou službu pro přihlášení** vyberte ikonu **Twitteru** .</span><span class="sxs-lookup"><span data-stu-id="bd825-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="bd825-209">Webová stránka přesměruje požadavek na přihlašovací stránku na Twitteru pro vytvořenou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="bd825-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![OAuth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="bd825-211">Přihlaste se k účtu na Twitteru.</span><span class="sxs-lookup"><span data-stu-id="bd825-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="bd825-212">Tento kód k ověření uživatele používá token Twitteru a potom se vrátí na stránku, kde můžete přidružit vaše přihlášení k vašemu účtu webu.</span><span class="sxs-lookup"><span data-stu-id="bd825-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="bd825-213">Vaše jméno nebo e-mailová adresa se vyplní do pole **e-mail** ve formuláři.</span><span class="sxs-lookup"><span data-stu-id="bd825-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="bd825-215">Klikněte na tlačítko **přidružit** .</span><span class="sxs-lookup"><span data-stu-id="bd825-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="bd825-216">Prohlížeč se vrátí na domovskou stránku a Vy jste přihlášení.</span><span class="sxs-lookup"><span data-stu-id="bd825-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="bd825-217">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="bd825-217">Additional Resources</span></span>

- [<span data-ttu-id="bd825-218">Přizpůsobení chování v celém webu</span><span class="sxs-lookup"><span data-stu-id="bd825-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="bd825-219">Přidání zabezpečení a členství do webu ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="bd825-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
