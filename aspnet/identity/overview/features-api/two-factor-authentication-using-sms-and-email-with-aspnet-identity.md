---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: Dvojúrovňové ověřování pomocí SMS a e-mailu s ASP.NET Identity-ASP.NET 4. x
author: HaoK
description: V tomto kurzu se dozvíte, jak nastavit dvojúrovňové ověřování (2FA) pomocí SMS a e-mailu. Tento článek napsal Rick Anderson (@RickAndMSFT), PR...
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 5f5218ca6c65ed3a2cd39d4e100349efa35d14cd
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115100"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="cc56d-104">Dvojúrovňové ověřování pomocí SMS a e-mailu s ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="cc56d-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>

<span data-ttu-id="cc56d-105">[Hao Kung](https://github.com/HaoK), [Pranav Rastogi předvádí](https://github.com/rustd), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Suhas Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="cc56d-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="cc56d-106">V tomto kurzu se dozvíte, jak nastavit dvojúrovňové ověřování (2FA) pomocí SMS a e-mailu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="cc56d-107">Tento článek napsal Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav rastogi předvádí ([@rustd](https://twitter.com/rustd)), Hao Kung a Suhas Joshi.</span><span class="sxs-lookup"><span data-stu-id="cc56d-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="cc56d-108">Vzorek NuGet byl napsán hlavně pomocí Hao Kung.</span><span class="sxs-lookup"><span data-stu-id="cc56d-108">The NuGet sample was written primarily by Hao Kung.</span></span>

<span data-ttu-id="cc56d-109">Toto téma obsahuje následující témata:</span><span class="sxs-lookup"><span data-stu-id="cc56d-109">This topic covers the following:</span></span>

- [<span data-ttu-id="cc56d-110">Sestavení ukázky identity</span><span class="sxs-lookup"><span data-stu-id="cc56d-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="cc56d-111">Nastavení SMS pro dvojúrovňové ověřování</span><span class="sxs-lookup"><span data-stu-id="cc56d-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="cc56d-112">Povolit dvojúrovňové ověřování</span><span class="sxs-lookup"><span data-stu-id="cc56d-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="cc56d-113">Jak zaregistrovat poskytovatele dvou faktorů ověřování</span><span class="sxs-lookup"><span data-stu-id="cc56d-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="cc56d-114">Kombinování sociálních a místních přihlašovacích účtů</span><span class="sxs-lookup"><span data-stu-id="cc56d-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="cc56d-115">Uzamčení účtu před útoky hrubou silou</span><span class="sxs-lookup"><span data-stu-id="cc56d-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="cc56d-116">Sestavení ukázky identity</span><span class="sxs-lookup"><span data-stu-id="cc56d-116">Building the Identity sample</span></span>

<span data-ttu-id="cc56d-117">V této části použijete NuGet ke stažení ukázky, se kterou budeme pracovat.</span><span class="sxs-lookup"><span data-stu-id="cc56d-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="cc56d-118">Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="cc56d-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="cc56d-119">Nainstalujte Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) nebo novější.</span><span class="sxs-lookup"><span data-stu-id="cc56d-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="cc56d-120">Upozornění: k dokončení tohoto kurzu je nutné nainstalovat aktualizaci Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) .</span><span class="sxs-lookup"><span data-stu-id="cc56d-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>

1. <span data-ttu-id="cc56d-121">Vytvořte nový ***prázdný*** webový projekt v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cc56d-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="cc56d-122">V konzole správce balíčků zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="cc56d-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="cc56d-123">V tomto kurzu použijeme [SendGrid](http://sendgrid.com/) k posílání e-mailů a [Twilio](https://www.twilio.com/) nebo [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) pro text SMS.</span><span class="sxs-lookup"><span data-stu-id="cc56d-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="cc56d-124">Balíček `Identity.Samples` nainstaluje kód, se kterým budeme pracovat.</span><span class="sxs-lookup"><span data-stu-id="cc56d-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="cc56d-125">Nastavte [projekt na použití SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cc56d-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="cc56d-126">*Volitelné*: postupujte podle pokynů v [kurzu e-mailové potvrzení](account-confirmation-and-password-recovery-with-aspnet-identity.md) , abyste připojili SendGrid a pak spustili aplikaci a zaregistrovali e-mailový účet.</span><span class="sxs-lookup"><span data-stu-id="cc56d-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="cc56d-127">*Volitelné:* Z ukázky odeberte potvrzovací kód e-mailového odkazu (kód `ViewBag.Link` v řadiči účtů.</span><span class="sxs-lookup"><span data-stu-id="cc56d-127">*Optional:* Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="cc56d-128">Podívejte se na metody akcí `DisplayEmail` a `ForgotPasswordConfirmation` a zobrazení Razor).</span><span class="sxs-lookup"><span data-stu-id="cc56d-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="cc56d-129">*Volitelné:* Odeberte kód `ViewBag.Status` z řadičů pro správu a účtů a ze zobrazení *Views\Account\VerifyCode.cshtml* a *Views\Manage\VerifyPhoneNumber.cshtml* Razor.</span><span class="sxs-lookup"><span data-stu-id="cc56d-129">*Optional:* Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml* and *Views\Manage\VerifyPhoneNumber.cshtml* razor views.</span></span> <span data-ttu-id="cc56d-130">Alternativně můžete `ViewBag.Status` zobrazení, abyste otestovali, jak tato aplikace funguje lokálně, aniž byste museli zapojovat a odesílat e-maily a zprávy SMS.</span><span class="sxs-lookup"><span data-stu-id="cc56d-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="cc56d-131">Upozornění: Pokud v této ukázce změníte některá z nastavení zabezpečení, budou se v aplikacích výroby muset projít auditem zabezpečení, který explicitně volá provedené změny.</span><span class="sxs-lookup"><span data-stu-id="cc56d-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="cc56d-132">Nastavení SMS pro dvojúrovňové ověřování</span><span class="sxs-lookup"><span data-stu-id="cc56d-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="cc56d-133">V tomto kurzu najdete pokyny k použití Twilio nebo ASPSMS, ale můžete použít jakéhokoli jiného poskytovatele serveru SMS.</span><span class="sxs-lookup"><span data-stu-id="cc56d-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="cc56d-134">**Vytvoření uživatelského účtu pomocí poskytovatele služby SMS**</span><span class="sxs-lookup"><span data-stu-id="cc56d-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="cc56d-135">Vytvořte účet [Twilio](https://www.twilio.com/try-twilio) nebo [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) .</span><span class="sxs-lookup"><span data-stu-id="cc56d-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="cc56d-136">**Instalace dalších balíčků nebo přidávání odkazů na služby**</span><span class="sxs-lookup"><span data-stu-id="cc56d-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="cc56d-137">Twilio</span><span class="sxs-lookup"><span data-stu-id="cc56d-137">Twilio:</span></span>  
   <span data-ttu-id="cc56d-138">V konzole správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="cc56d-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="cc56d-139">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="cc56d-139">ASPSMS:</span></span>  
   <span data-ttu-id="cc56d-140">Je potřeba přidat následující odkaz na službu:</span><span class="sxs-lookup"><span data-stu-id="cc56d-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="cc56d-141">Adresáře</span><span class="sxs-lookup"><span data-stu-id="cc56d-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="cc56d-142">Obor názvů:</span><span class="sxs-lookup"><span data-stu-id="cc56d-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="cc56d-143">**Zjišťování přihlašovacích údajů uživatele poskytovatele služby SMS**</span><span class="sxs-lookup"><span data-stu-id="cc56d-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="cc56d-144">Twilio</span><span class="sxs-lookup"><span data-stu-id="cc56d-144">Twilio:</span></span>  
   <span data-ttu-id="cc56d-145">Na kartě **řídicí panel** účtu Twilio zkopírujte **identifikátor SID účtu** a **ověřovací token**.</span><span class="sxs-lookup"><span data-stu-id="cc56d-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="cc56d-146">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="cc56d-146">ASPSMS:</span></span>  
   <span data-ttu-id="cc56d-147">V nastavení účtu přejděte na **vlastnosti UserKey** a zkopírujte je společně s vaším vlastním **heslem**.</span><span class="sxs-lookup"><span data-stu-id="cc56d-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="cc56d-148">Později budou tyto hodnoty uloženy v proměnných `SMSAccountIdentification` a `SMSAccountPassword`.</span><span class="sxs-lookup"><span data-stu-id="cc56d-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="cc56d-149">**Zadání SenderID/původce**</span><span class="sxs-lookup"><span data-stu-id="cc56d-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="cc56d-150">Twilio</span><span class="sxs-lookup"><span data-stu-id="cc56d-150">Twilio:</span></span>  
   <span data-ttu-id="cc56d-151">Na kartě **čísla** zkopírujte své Twilio telefonní číslo.</span><span class="sxs-lookup"><span data-stu-id="cc56d-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="cc56d-152">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="cc56d-152">ASPSMS:</span></span>  
   <span data-ttu-id="cc56d-153">V nabídce **odemknout původci** odemkněte jeden nebo více původců nebo vyberte alfanumerický původ (není podporován všemi sítěmi).</span><span class="sxs-lookup"><span data-stu-id="cc56d-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="cc56d-154">Tuto hodnotu uložíme později do proměnné `SMSAccountFrom`.</span><span class="sxs-lookup"><span data-stu-id="cc56d-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="cc56d-155">**Přenáší se přihlašovací údaje poskytovatele SMS do aplikace.**</span><span class="sxs-lookup"><span data-stu-id="cc56d-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="cc56d-156">Zpřístupnit přihlašovací údaje a telefonní číslo odesilatele k aplikaci:</span><span class="sxs-lookup"><span data-stu-id="cc56d-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="cc56d-157">Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="cc56d-158">Účet a přihlašovací údaje se přidají do výše uvedeného kódu, aby se ukázka snadno zachovala.</span><span class="sxs-lookup"><span data-stu-id="cc56d-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="cc56d-159">Viz Jan atten 's [ASP.NET MVC: zachovejte soukromé nastavení ze správy zdrojového kódu](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc56d-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="cc56d-160">**Implementace přenosu dat do poskytovatele služby SMS**</span><span class="sxs-lookup"><span data-stu-id="cc56d-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="cc56d-161">Nakonfigurujte třídu `SmsService` v souboru *App\_Start\IdentityConfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="cc56d-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="cc56d-162">V závislosti na použitém poskytovateli serveru SMS aktivujte **Twilio** nebo část **ASPSMS** :</span><span class="sxs-lookup"><span data-stu-id="cc56d-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="cc56d-163">Spusťte aplikaci a přihlaste se pomocí účtu, který jste předtím zaregistrovali.</span><span class="sxs-lookup"><span data-stu-id="cc56d-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="cc56d-164">Klikněte na své ID uživatele, které aktivuje metodu `Index` akce v kontroleru `Manage`.</span><span class="sxs-lookup"><span data-stu-id="cc56d-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="cc56d-165">Klikněte na tlačítko Přidat.</span><span class="sxs-lookup"><span data-stu-id="cc56d-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="cc56d-166">Během několika sekund obdržíte textovou zprávu s ověřovacím kódem.</span><span class="sxs-lookup"><span data-stu-id="cc56d-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="cc56d-167">Zadejte ji a stiskněte **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="cc56d-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="cc56d-168">V zobrazení Správa se zobrazí vaše telefonní číslo.</span><span class="sxs-lookup"><span data-stu-id="cc56d-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="cc56d-169">Kontrola kódu</span><span class="sxs-lookup"><span data-stu-id="cc56d-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="cc56d-170">Metoda `Index` akce v kontroleru `Manage` nastavuje stavovou zprávu na základě předchozí akce a obsahuje odkazy na změnu místního hesla nebo přidání místního účtu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="cc56d-171">Metoda `Index` taky zobrazuje stav nebo telefonní číslo 2FA, externí přihlášení, 2FA povoleno a pamatuje 2FA metodu pro tento prohlížeč (vysvětlení později).</span><span class="sxs-lookup"><span data-stu-id="cc56d-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="cc56d-172">Kliknutím na své ID uživatele (e-mailové adresy) v záhlaví se zpráva nepředá.</span><span class="sxs-lookup"><span data-stu-id="cc56d-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="cc56d-173">Kliknutí na **telefonní číslo: odebrat** předávání odkazů `Message=RemovePhoneSuccess` jako řetězec dotazu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="cc56d-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="cc56d-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="cc56d-175">Metoda `AddPhoneNumber` akce zobrazí dialogové okno pro zadání telefonního čísla, které může přijímat zprávy SMS.</span><span class="sxs-lookup"><span data-stu-id="cc56d-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="cc56d-176">Kliknutím na tlačítko **Odeslat ověřovací kód** se zaúčtuje telefonní číslo do metody HTTP POST `AddPhoneNumber` Action.</span><span class="sxs-lookup"><span data-stu-id="cc56d-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="cc56d-177">Metoda `GenerateChangePhoneNumberTokenAsync` vygeneruje token zabezpečení, který se nastaví ve zprávě SMS.</span><span class="sxs-lookup"><span data-stu-id="cc56d-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="cc56d-178">Pokud je nakonfigurovaná služba SMS, token se pošle jako řetězec &quot;je váš bezpečnostní kód &lt;token&gt;&quot;.</span><span class="sxs-lookup"><span data-stu-id="cc56d-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="cc56d-179">Metoda `SmsService.SendAsync` pro je volána asynchronně, pak je aplikace přesměrována na metodu `VerifyPhoneNumber` akce (která zobrazuje následující dialog), kde můžete zadat ověřovací kód.</span><span class="sxs-lookup"><span data-stu-id="cc56d-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="cc56d-180">Jakmile zadáte kód a kliknete na Odeslat, kód se publikuje do metody HTTP POST `VerifyPhoneNumber` Action.</span><span class="sxs-lookup"><span data-stu-id="cc56d-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="cc56d-181">Metoda `ChangePhoneNumberAsync` kontroluje vystavený bezpečnostní kód.</span><span class="sxs-lookup"><span data-stu-id="cc56d-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="cc56d-182">Je-li kód správný, je telefonní číslo přidáno do pole `PhoneNumber` `AspNetUsers` tabulce.</span><span class="sxs-lookup"><span data-stu-id="cc56d-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="cc56d-183">Pokud je toto volání úspěšné, je volána metoda `SignInAsync`:</span><span class="sxs-lookup"><span data-stu-id="cc56d-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="cc56d-184">Parametr `isPersistent` nastaví, zda je relace ověřování trvala napříč několika požadavky.</span><span class="sxs-lookup"><span data-stu-id="cc56d-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="cc56d-185">Když změníte profil zabezpečení, vygeneruje se nové bezpečnostní razítko, které se uloží do pole `SecurityStamp` tabulky *AspNetUsers* .</span><span class="sxs-lookup"><span data-stu-id="cc56d-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="cc56d-186">Poznámka: pole `SecurityStamp` se liší od souboru cookie zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cc56d-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="cc56d-187">Soubor cookie zabezpečení není uložený v `AspNetUsers` tabulce (nebo nikde jinde v databázi identity).</span><span class="sxs-lookup"><span data-stu-id="cc56d-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="cc56d-188">Token cookie zabezpečení je podepsaný svým držitelem pomocí [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) a vytvoří se s informacemi o `UserId, SecurityStamp` a času vypršení platnosti.</span><span class="sxs-lookup"><span data-stu-id="cc56d-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="cc56d-189">Middleware souboru cookie kontroluje soubory cookie u jednotlivých požadavků.</span><span class="sxs-lookup"><span data-stu-id="cc56d-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="cc56d-190">Metoda `SecurityStampValidator` ve třídě `Startup` narazí na databázi a pravidelně kontroluje razítko zabezpečení, jak je uvedeno v `validateInterval`.</span><span class="sxs-lookup"><span data-stu-id="cc56d-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="cc56d-191">K této situaci dochází pouze každých 30 minut (v naší ukázce), pokud neměníte profil zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cc56d-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="cc56d-192">Interval 30 minut byl zvolen pro minimalizaci cest k databázi.</span><span class="sxs-lookup"><span data-stu-id="cc56d-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="cc56d-193">Metoda `SignInAsync` musí být volána, když je provedena jakákoli změna v profilu zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cc56d-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="cc56d-194">Když se profil zabezpečení změní, databáze aktualizuje pole `SecurityStamp` a bez volání metody `SignInAsync` byste si měli zůstat přihlášeni *pouze* až do okamžiku, kdy kanál Owin narazí do databáze (`validateInterval`).</span><span class="sxs-lookup"><span data-stu-id="cc56d-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="cc56d-195">Můžete to otestovat tak, že změníte metodu `SignInAsync` pro okamžité vrácení a nastavíte vlastnost `validateInterval` souborů cookie na 30 minut na 5 sekund:</span><span class="sxs-lookup"><span data-stu-id="cc56d-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="cc56d-196">U výše uvedených změn kódu můžete změnit svůj profil zabezpečení (například změnou stavu **dvou faktorů povolených**) a při neúspěchu `SecurityStampValidator.OnValidateIdentity` metody se odhlásí za 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="cc56d-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="cc56d-197">Odeberte návratovou čáru v metodě `SignInAsync`, udělejte jinou změnu profilu zabezpečení a nebudete se odhlásit. Metoda `SignInAsync` generuje nový soubor cookie zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cc56d-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="cc56d-198">Povolit dvojúrovňové ověřování</span><span class="sxs-lookup"><span data-stu-id="cc56d-198">Enable two-factor authentication</span></span>

<span data-ttu-id="cc56d-199">V ukázkové aplikaci je nutné použít uživatelské rozhraní pro povolení dvojúrovňové ověřování (2FA).</span><span class="sxs-lookup"><span data-stu-id="cc56d-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="cc56d-200">Pokud chcete povolit 2FA, na navigačním panelu klikněte na své ID uživatele (e-mailový alias).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="cc56d-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="cc56d-201">Klikněte na Povolit 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="cc56d-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="cc56d-202">Odhlaste se a pak se znovu přihlaste.</span><span class="sxs-lookup"><span data-stu-id="cc56d-202">Log out, then log back in.</span></span> <span data-ttu-id="cc56d-203">Pokud jste povolili e-mail (viz můj [předchozí kurz](account-confirmation-and-password-recovery-with-aspnet-identity.md)), můžete vybrat zprávu SMS nebo E-mail pro 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="cc56d-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="cc56d-204">Zobrazí se stránka ověření kódu, kde můžete zadat kód (ze serveru SMS nebo e-mailu).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="cc56d-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="cc56d-205">Kliknutím na **Zapamatovat si tento prohlížeč** zabráníte tomu, abyste pomocí 2FA přihlásili s tímto počítačem a prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="cc56d-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="cc56d-206">Povolením 2FA a kliknutím na **Zapamatovat si tento prohlížeč** vám poskytne silnou 2FA ochranu od uživatelů se zlými úmysly, kteří se pokoušejí získat přístup k vašemu účtu, pokud k vašemu počítači nemají přístup.</span><span class="sxs-lookup"><span data-stu-id="cc56d-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="cc56d-207">To můžete provést na jakémkoli privátním počítači, který pravidelně používáte.</span><span class="sxs-lookup"><span data-stu-id="cc56d-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="cc56d-208">Nastavením možnosti **pamatovat si tento prohlížeč**získáte zvýšení zabezpečení 2FA z počítačů, které pravidelně nepoužíváte, a získáte pohodlí v tom, že nebudete moct procházet 2FA na svých počítačích.</span><span class="sxs-lookup"><span data-stu-id="cc56d-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="cc56d-209">Jak zaregistrovat poskytovatele dvou faktorů ověřování</span><span class="sxs-lookup"><span data-stu-id="cc56d-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="cc56d-210">Při vytváření nového projektu MVC obsahuje soubor *IdentityConfig.cs* následující kód pro registraci zprostředkovatele dvou faktorů ověřování:</span><span class="sxs-lookup"><span data-stu-id="cc56d-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="cc56d-211">Přidat telefonní číslo pro 2FA</span><span class="sxs-lookup"><span data-stu-id="cc56d-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="cc56d-212">Metoda `AddPhoneNumber` akce v kontroleru `Manage` vygeneruje token zabezpečení a pošle ho na telefonní číslo, které jste zadali.</span><span class="sxs-lookup"><span data-stu-id="cc56d-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="cc56d-213">Po odeslání tokenu se přesměruje na metodu `VerifyPhoneNumber` akce, kde můžete zadat kód k registraci serveru SMS pro 2FA.</span><span class="sxs-lookup"><span data-stu-id="cc56d-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="cc56d-214">2FA serveru SMS se nepoužívá, dokud neověříte telefonní číslo.</span><span class="sxs-lookup"><span data-stu-id="cc56d-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="cc56d-215">Povolení 2FA</span><span class="sxs-lookup"><span data-stu-id="cc56d-215">Enabling 2FA</span></span>

<span data-ttu-id="cc56d-216">Metoda `EnableTFA` akce povoluje 2FA:</span><span class="sxs-lookup"><span data-stu-id="cc56d-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="cc56d-217">Všimněte si, že `SignInAsync` musí být volána, protože možnost Povolit 2FA je změnou profilu zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cc56d-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="cc56d-218">Pokud je povolená možnost 2FA, bude uživatel muset použít 2FA k přihlášení s použitím 2FA přístupů, které zaregistrovali (SMS a e-mail v ukázce).</span><span class="sxs-lookup"><span data-stu-id="cc56d-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="cc56d-219">Můžete přidat další poskytovatele 2FA, jako jsou například generátory kódu QR, nebo můžete napsat vlastní (viz [používání služby Google Authenticator s ASP.NET identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span><span class="sxs-lookup"><span data-stu-id="cc56d-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="cc56d-220">Kódy 2FA se generují pomocí [algoritmu jednorázového hesla založeného na čase](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) a kódy jsou platné po dobu šesti minut.</span><span class="sxs-lookup"><span data-stu-id="cc56d-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="cc56d-221">Pokud zadáte kód více než šest minut, zobrazí se chybová zpráva neplatného kódu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="cc56d-222">Kombinování sociálních a místních přihlašovacích účtů</span><span class="sxs-lookup"><span data-stu-id="cc56d-222">Combine social and local login accounts</span></span>

<span data-ttu-id="cc56d-223">Místní a sociální účty můžete zkombinovat kliknutím na svůj e-mailový odkaz.</span><span class="sxs-lookup"><span data-stu-id="cc56d-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="cc56d-224">V následující sekvenci &quot;RickAndMSFT@gmail.com&quot; nejdřív vytvořená jako místní přihlašovací jméno, ale můžete účet vytvořit jako sociální protokol a pak přidat místní přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="cc56d-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="cc56d-225">Klikněte na odkaz **Správa** .</span><span class="sxs-lookup"><span data-stu-id="cc56d-225">Click on the **Manage** link.</span></span> <span data-ttu-id="cc56d-226">Poznamenejte si externí (sociální přihlášení) přidružená k tomuto účtu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="cc56d-227">Klikněte na odkaz na jiný protokol služby a přijměte žádosti o aplikace.</span><span class="sxs-lookup"><span data-stu-id="cc56d-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="cc56d-228">Tyto dva účty byly zkombinovány, budete se moci přihlásit pomocí obou účtů.</span><span class="sxs-lookup"><span data-stu-id="cc56d-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="cc56d-229">Je možné, že budete chtít, aby uživatelé mohli přidávat místní účty v případě výpadku služby sociálního protokolu v případě nedostatku nebo pravděpodobně ztratili přístup ke svému sociálnímu účtu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="cc56d-230">Na následujícím obrázku je to, že se jedná o sociální přihlášení (které vidíte z **externích přihlášení: 1** zobrazeno na stránce).</span><span class="sxs-lookup"><span data-stu-id="cc56d-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="cc56d-231">Kliknutím na **Vybrat heslo** můžete přidat místní přihlašování ke stejnému účtu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="cc56d-232">Uzamčení účtu před útoky hrubou silou</span><span class="sxs-lookup"><span data-stu-id="cc56d-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="cc56d-233">Můžete chránit účty ve vaší aplikaci před slovníkovými útoky tím, že povolíte uzamčení uživatele.</span><span class="sxs-lookup"><span data-stu-id="cc56d-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="cc56d-234">Následující kód v metodě `ApplicationUserManager Create` konfiguruje odblokování:</span><span class="sxs-lookup"><span data-stu-id="cc56d-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="cc56d-235">Výše uvedený kód umožňuje uzamčení pouze pro dva faktory ověřování.</span><span class="sxs-lookup"><span data-stu-id="cc56d-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="cc56d-236">I když můžete povolit možnost Uzamknout pro přihlášení změnou `shouldLockout` na hodnotu true v metodě `Login` řadiče účtů, doporučujeme Nepovolit možnost Uzamknout pro přihlášení, protože účet je náchylný k útokům prostřednictvím přihlašovacích údajů pro [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) .</span><span class="sxs-lookup"><span data-stu-id="cc56d-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="cc56d-237">V ukázkovém kódu je uzamčení pro účet správce vytvořené v metodě `ApplicationDbInitializer Seed` zakázané:</span><span class="sxs-lookup"><span data-stu-id="cc56d-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="cc56d-238">Vyžaduje se, aby uživatel měl ověřený e-mailový účet.</span><span class="sxs-lookup"><span data-stu-id="cc56d-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="cc56d-239">Následující kód vyžaduje, aby uživatel měl ověřený e-mailový účet, než se může přihlásit:</span><span class="sxs-lookup"><span data-stu-id="cc56d-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="cc56d-240">Jak SignInManager vyhledává požadavek 2FA</span><span class="sxs-lookup"><span data-stu-id="cc56d-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="cc56d-241">Místní přihlašovací protokol i protokol pro sociální sítě kontrolují, zda je povolený 2FA.</span><span class="sxs-lookup"><span data-stu-id="cc56d-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="cc56d-242">Pokud je povolený 2FA, metoda přihlašování `SignInManager` vrátí `SignInStatus.RequiresVerification`a uživatel se přesměruje na metodu `SendCode` akce, kde bude muset zadat kód pro dokončení protokolu.</span><span class="sxs-lookup"><span data-stu-id="cc56d-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="cc56d-243">Pokud je v místním souboru cookie uživatelů nastavená RememberMe, `SignInManager` vrátí `SignInStatus.Success` a nebude muset projít přes 2FA.</span><span class="sxs-lookup"><span data-stu-id="cc56d-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="cc56d-244">Následující kód ukazuje metodu `SendCode` akce.</span><span class="sxs-lookup"><span data-stu-id="cc56d-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="cc56d-245">[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) se vytvoří se všemi metodami 2FA povolenými pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="cc56d-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="cc56d-246">[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) se předává Pomocníkovi [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) , který umožňuje uživateli vybrat přístup 2FA (obvykle e-mail a SMS).</span><span class="sxs-lookup"><span data-stu-id="cc56d-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="cc56d-247">Jakmile uživatel odešle přístup 2FA, je volána metoda akce `HTTP POST SendCode`, `SignInManager` odešle kód 2FA a uživatel je přesměrován na metodu `VerifyCode` akce, kde může zadat kód pro dokončení přihlášení.</span><span class="sxs-lookup"><span data-stu-id="cc56d-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="cc56d-248">2FA uzamčení</span><span class="sxs-lookup"><span data-stu-id="cc56d-248">2FA Lockout</span></span>

<span data-ttu-id="cc56d-249">I když můžete nastavit uzamčení účtu při neúspěchu při pokusu o přihlášení k přihlašovacím údajům, bude se vaše přihlášení nahlížet na uzamčení [systému DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) .</span><span class="sxs-lookup"><span data-stu-id="cc56d-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="cc56d-250">Uzamčení účtu doporučujeme používat jenom s 2FA.</span><span class="sxs-lookup"><span data-stu-id="cc56d-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="cc56d-251">Při vytvoření `ApplicationUserManager` ukázkový kód nastaví uzamčení 2FA a `MaxFailedAccessAttemptsBeforeLockout` na pět.</span><span class="sxs-lookup"><span data-stu-id="cc56d-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="cc56d-252">Jakmile se uživatel přihlásí (prostřednictvím místního účtu nebo účtu na sociálních sítích), uloží se každý neúspěšný pokus na 2FA a pokud se dosáhne maximálního počtu pokusů, uživatel se zablokuje na pět minut (můžete nastavit čas uzamčení pomocí `DefaultAccountLockoutTimeSpan`).</span><span class="sxs-lookup"><span data-stu-id="cc56d-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="cc56d-253">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="cc56d-253">Additional Resources</span></span>

- <span data-ttu-id="cc56d-254">[ASP.NET identity doporučené prostředky](../getting-started/aspnet-identity-recommended-resources.md) Úplný seznam blogů identity, videí, výukových kurzů a skvělých odkazů</span><span class="sxs-lookup"><span data-stu-id="cc56d-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="cc56d-255">[Aplikace MVC 5 s přihlašováním na Facebooku, Twitter, LinkedIn a Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) také ukazuje, jak přidat informace o profilu do tabulky uživatelů.</span><span class="sxs-lookup"><span data-stu-id="cc56d-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="cc56d-256">[ASP.NET MVC a identita 2,0: Seznámení se základy](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) pomocí Jan atten.</span><span class="sxs-lookup"><span data-stu-id="cc56d-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="cc56d-257">Potvrzení účtu a obnovení hesla pomocí ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="cc56d-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="cc56d-258">Úvod do ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="cc56d-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="cc56d-259">[Oznamujeme RTM ASP.NET identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) podle Pranav Rastogi předvádí.</span><span class="sxs-lookup"><span data-stu-id="cc56d-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="cc56d-260">[ASP.NET Identity 2,0: nastavení ověřování účtu a dvojúrovňové autorizace](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) pomocí Jan atten.</span><span class="sxs-lookup"><span data-stu-id="cc56d-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
