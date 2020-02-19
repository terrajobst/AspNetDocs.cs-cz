---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: Aplikace ASP.NET MVC 5 s SMS a e-mailovým ověřováním | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 se dvěma faktory ověřování. Měli byste dokončit vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s...
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457593"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="0ca89-104">Aplikace ASP.NET MVC 5 s dvoufaktorovým ověřováním pomocí SMS a e-mailu</span><span class="sxs-lookup"><span data-stu-id="0ca89-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>

<span data-ttu-id="0ca89-105">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0ca89-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="0ca89-106">V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 se dvěma faktory ověřování.</span><span class="sxs-lookup"><span data-stu-id="0ca89-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="0ca89-107">Před pokračováním musíte [vytvořit zabezpečenou webovou aplikaci ASP.NET MVC 5 s přihlášením, potvrzením e-mailem a resetováním hesla](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) .</span><span class="sxs-lookup"><span data-stu-id="0ca89-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="0ca89-108">Dokončenou aplikaci si můžete stáhnout [tady](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="0ca89-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="0ca89-109">Stažení obsahuje ladicí služby, které vám umožní testovat potvrzení e-mailu a SMS bez nastavování e-mailu nebo poskytovatele služby SMS.</span><span class="sxs-lookup"><span data-stu-id="0ca89-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="0ca89-110">Tento kurz napsal [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="0ca89-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

- [<span data-ttu-id="0ca89-111">Vytvoření aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0ca89-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="0ca89-112">Nastavení SMS pro dvojúrovňové ověřování</span><span class="sxs-lookup"><span data-stu-id="0ca89-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="0ca89-113">Povolit dvojúrovňové ověřování</span><span class="sxs-lookup"><span data-stu-id="0ca89-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="0ca89-114">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="0ca89-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="0ca89-115">Vytvoření aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0ca89-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="0ca89-116">Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="0ca89-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="0ca89-117">Nainstalujte [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="0ca89-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="0ca89-118">Upozornění: před pokračováním musíte [vytvořit zabezpečenou webovou aplikaci ASP.NET MVC 5 s přihlášením, potvrzením e-mailem a resetováním hesla](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) .</span><span class="sxs-lookup"><span data-stu-id="0ca89-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="0ca89-119">Chcete-li dokončit tento kurz, je nutné nainstalovat [aktualizaci Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="0ca89-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="0ca89-120">Vytvořte nový webový projekt v ASP.NET a vyberte šablonu MVC.</span><span class="sxs-lookup"><span data-stu-id="0ca89-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="0ca89-121">Webové formuláře také podporují ASP.NET Identity, takže můžete postupovat podle podobných kroků v aplikaci webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="0ca89-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="0ca89-122">U **jednotlivých uživatelských účtů**ponechte výchozí ověřování.</span><span class="sxs-lookup"><span data-stu-id="0ca89-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="0ca89-123">Pokud chcete aplikaci hostovat v Azure, nechte zaškrtávací políčko zaškrtnuté.</span><span class="sxs-lookup"><span data-stu-id="0ca89-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="0ca89-124">Později v tomto kurzu provedeme nasazení do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ca89-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="0ca89-125">Můžete si [otevřít účet Azure zdarma](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0ca89-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="0ca89-126">Nastavte [projekt na použití SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0ca89-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="0ca89-127">Nastavení SMS pro dvojúrovňové ověřování</span><span class="sxs-lookup"><span data-stu-id="0ca89-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="0ca89-128">V tomto kurzu najdete pokyny k použití Twilio nebo ASPSMS, ale můžete použít jakéhokoli jiného poskytovatele serveru SMS.</span><span class="sxs-lookup"><span data-stu-id="0ca89-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="0ca89-129">**Vytvoření uživatelského účtu pomocí poskytovatele služby SMS**</span><span class="sxs-lookup"><span data-stu-id="0ca89-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="0ca89-130">Vytvořte účet [Twilio](https://www.twilio.com/try-twilio) nebo [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) .</span><span class="sxs-lookup"><span data-stu-id="0ca89-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="0ca89-131">**Instalace dalších balíčků nebo přidávání odkazů na služby**</span><span class="sxs-lookup"><span data-stu-id="0ca89-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="0ca89-132">Twilio</span><span class="sxs-lookup"><span data-stu-id="0ca89-132">Twilio:</span></span>  
   <span data-ttu-id="0ca89-133">V konzole správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="0ca89-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="0ca89-134">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="0ca89-134">ASPSMS:</span></span>  
   <span data-ttu-id="0ca89-135">Je potřeba přidat následující odkaz na službu:</span><span class="sxs-lookup"><span data-stu-id="0ca89-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="0ca89-136">Adresáře</span><span class="sxs-lookup"><span data-stu-id="0ca89-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="0ca89-137">Obor názvů:</span><span class="sxs-lookup"><span data-stu-id="0ca89-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="0ca89-138">**Zjišťování přihlašovacích údajů uživatele poskytovatele služby SMS**</span><span class="sxs-lookup"><span data-stu-id="0ca89-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="0ca89-139">Twilio</span><span class="sxs-lookup"><span data-stu-id="0ca89-139">Twilio:</span></span>  
   <span data-ttu-id="0ca89-140">Na kartě **řídicí panel** účtu Twilio zkopírujte **identifikátor SID účtu** a **ověřovací token**.</span><span class="sxs-lookup"><span data-stu-id="0ca89-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="0ca89-141">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="0ca89-141">ASPSMS:</span></span>  
   <span data-ttu-id="0ca89-142">V nastavení účtu přejděte na **vlastnosti UserKey** a zkopírujte je společně s vaším vlastním **heslem**.</span><span class="sxs-lookup"><span data-stu-id="0ca89-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="0ca89-143">Tyto hodnoty budeme později ukládat do souboru *Web. config* v rámci klíčů `"SMSAccountIdentification"` a `"SMSAccountPassword"`.</span><span class="sxs-lookup"><span data-stu-id="0ca89-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="0ca89-144">**Zadání SenderID/původce**</span><span class="sxs-lookup"><span data-stu-id="0ca89-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="0ca89-145">Twilio</span><span class="sxs-lookup"><span data-stu-id="0ca89-145">Twilio:</span></span>  
   <span data-ttu-id="0ca89-146">Na kartě **čísla** zkopírujte své Twilio telefonní číslo.</span><span class="sxs-lookup"><span data-stu-id="0ca89-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="0ca89-147">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="0ca89-147">ASPSMS:</span></span>  
   <span data-ttu-id="0ca89-148">V nabídce **odemknout původci** odemkněte jeden nebo více původců nebo vyberte alfanumerický původ (není podporován všemi sítěmi).</span><span class="sxs-lookup"><span data-stu-id="0ca89-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="0ca89-149">Tuto hodnotu bude později Uloženo v souboru *Web. config* v rámci klíče `"SMSAccountFrom"`.</span><span class="sxs-lookup"><span data-stu-id="0ca89-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="0ca89-150">**Přenáší se přihlašovací údaje poskytovatele SMS do aplikace.**</span><span class="sxs-lookup"><span data-stu-id="0ca89-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="0ca89-151">Nastavte přihlašovací údaje a telefonní číslo odesilatele k aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0ca89-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="0ca89-152">Abychom zachovali něco jednoduchého, uložíme tyto hodnoty do souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="0ca89-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="0ca89-153">Po nasazení do Azure můžeme hodnoty bezpečně ukládat v části **nastavení aplikace** na kartě Konfigurace webu.</span><span class="sxs-lookup"><span data-stu-id="0ca89-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="0ca89-154">Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="0ca89-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="0ca89-155">Účet a přihlašovací údaje se přidají do výše uvedeného kódu, aby se ukázka snadno zachovala.</span><span class="sxs-lookup"><span data-stu-id="0ca89-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="0ca89-156">Podívejte [se na osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0ca89-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="0ca89-157">**Implementace přenosu dat do poskytovatele služby SMS**</span><span class="sxs-lookup"><span data-stu-id="0ca89-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="0ca89-158">Nakonfigurujte třídu `SmsService` v souboru *App\_Start\IdentityConfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="0ca89-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="0ca89-159">V závislosti na použitém poskytovateli serveru SMS aktivujte **Twilio** nebo část **ASPSMS** :</span><span class="sxs-lookup"><span data-stu-id="0ca89-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="0ca89-160">Aktualizace zobrazení *Views\Manage\Index.cshtml* Razor: (Poznámka: Neodstraňujte pouze komentáře v ukončovacím kódu, použijte následující kód.)</span><span class="sxs-lookup"><span data-stu-id="0ca89-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="0ca89-161">Ověřte, že metody akcí `EnableTwoFactorAuthentication` a `DisableTwoFactorAuthentication` v `ManageController` mají atribut[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) :</span><span class="sxs-lookup"><span data-stu-id="0ca89-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="0ca89-162">Spusťte aplikaci a přihlaste se pomocí účtu, který jste předtím zaregistrovali.</span><span class="sxs-lookup"><span data-stu-id="0ca89-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="0ca89-163">Klikněte na své ID uživatele, které aktivuje metodu `Index` akce v kontroleru `Manage`.</span><span class="sxs-lookup"><span data-stu-id="0ca89-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="0ca89-164">Klikněte na Přidat.</span><span class="sxs-lookup"><span data-stu-id="0ca89-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="0ca89-165">Metoda `AddPhoneNumber` akce zobrazí dialogové okno pro zadání telefonního čísla, které může přijímat zprávy SMS.</span><span class="sxs-lookup"><span data-stu-id="0ca89-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="0ca89-166">Během několika sekund obdržíte textovou zprávu s ověřovacím kódem.</span><span class="sxs-lookup"><span data-stu-id="0ca89-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="0ca89-167">Zadejte ji a stiskněte **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="0ca89-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="0ca89-168">V zobrazení Správa se zobrazí vaše telefonní číslo.</span><span class="sxs-lookup"><span data-stu-id="0ca89-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="0ca89-169">Povolení dvoufaktorového ověřování</span><span class="sxs-lookup"><span data-stu-id="0ca89-169">Enable two-factor authentication</span></span>

<span data-ttu-id="0ca89-170">V aplikaci vygenerované šablonou je nutné použít uživatelské rozhraní pro povolení dvojúrovňové ověřování (2FA).</span><span class="sxs-lookup"><span data-stu-id="0ca89-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="0ca89-171">Pokud chcete povolit 2FA, na navigačním panelu klikněte na své ID uživatele (e-mailový alias).</span><span class="sxs-lookup"><span data-stu-id="0ca89-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="0ca89-172">Klikněte na Povolit 2FA.</span><span class="sxs-lookup"><span data-stu-id="0ca89-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="0ca89-173">Odhlaste se a potom se znovu přihlaste.</span><span class="sxs-lookup"><span data-stu-id="0ca89-173">Logout, then log back in.</span></span> <span data-ttu-id="0ca89-174">Pokud jste povolili e-mail (viz můj [předchozí kurz](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), můžete vybrat zprávu SMS nebo E-mail pro 2FA.</span><span class="sxs-lookup"><span data-stu-id="0ca89-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="0ca89-175">Zobrazí se stránka ověření kódu, kde můžete zadat kód (ze serveru SMS nebo e-mailu).</span><span class="sxs-lookup"><span data-stu-id="0ca89-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="0ca89-176">Kliknutím na toto zaškrtávací políčko **prohlížeč zapamatujte** , že nebudete muset používat 2FA k přihlášení při použití prohlížeče a zařízení, kde jste zaškrtli políčko.</span><span class="sxs-lookup"><span data-stu-id="0ca89-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="0ca89-177">Pokud uživatelé se zlými úmysly nezískají přístup k vašemu zařízení, povolí 2FA a kliknou na zapamatovat si, že **Tento prohlížeč** vám poskytne pohodlný přístup k heslům, ale přitom zachovává silnou ochranu 2FA pro veškerý přístup z nedůvěryhodných zařízení.</span><span class="sxs-lookup"><span data-stu-id="0ca89-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="0ca89-178">Můžete to provést na libovolném privátní zařízení, kterou používáte pravidelně.</span><span class="sxs-lookup"><span data-stu-id="0ca89-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="0ca89-179">V tomto kurzu se seznámíte s tím, jak povolit 2FA v nové aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0ca89-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="0ca89-180">Můj kurz [– dvojúrovňové ověřování pomocí SMS a e-mailu s ASP.NET identity se](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) podrobněji odkazuje na kód za ukázkou.</span><span class="sxs-lookup"><span data-stu-id="0ca89-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="0ca89-181">Další materiály a zdroje informací</span><span class="sxs-lookup"><span data-stu-id="0ca89-181">Additional Resources</span></span>

- <span data-ttu-id="0ca89-182">[Dvojúrovňové ověřování pomocí SMS a e-mailu s ASP.NET identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Přejde na podrobnosti o dvojúrovňové ověřování.</span><span class="sxs-lookup"><span data-stu-id="0ca89-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="0ca89-183">Odkazy na ASP.NET Identity doporučené prostředky</span><span class="sxs-lookup"><span data-stu-id="0ca89-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="0ca89-184">[Potvrzení účtu a obnovení hesla pomocí ASP.NET identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Přechází na další podrobnosti o obnovení hesla a potvrzení účtu.</span><span class="sxs-lookup"><span data-stu-id="0ca89-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="0ca89-185">[Aplikace MVC 5 s přihlašováním na Facebooku, Twitteru, LinkedInu a Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) V tomto kurzu se dozvíte, jak napsat aplikaci ASP.NET MVC 5 s autorizací na Facebooku a Google OAuth 2.</span><span class="sxs-lookup"><span data-stu-id="0ca89-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="0ca89-186">Také ukazuje, jak přidat další data do databáze identity.</span><span class="sxs-lookup"><span data-stu-id="0ca89-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="0ca89-187">[Nasaďte zabezpečenou aplikaci ASP.NET MVC s členstvím, protokolem OAuth a SQL Database do webu Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="0ca89-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="0ca89-188">Tento kurz přidá nasazení Azure, způsob zabezpečení vaší aplikace pomocí rolí, způsob použití rozhraní API pro členství v přidávání uživatelů a rolí a další funkce zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="0ca89-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="0ca89-189">Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="0ca89-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="0ca89-190">Vytvoření aplikace na Facebooku a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="0ca89-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="0ca89-191">Nastavení SSL v projektu</span><span class="sxs-lookup"><span data-stu-id="0ca89-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [<span data-ttu-id="0ca89-192">Jak nastavit C# vývojové prostředí ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0ca89-192">How to set up your C# and ASP.NET MVC development environment</span></span>](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
