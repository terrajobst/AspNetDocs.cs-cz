---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu aC#resetováním hesla () | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 s potvrzením e-mailu a resetováním hesla pomocí systému členství v ASP.NET Identity. CA...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 6169c972ad0f4ee2079d3638c54a5accc4b8b3de
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519346"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="4a478-104">Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu a resetováním hesla (C#)</span><span class="sxs-lookup"><span data-stu-id="4a478-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="4a478-105">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4a478-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4a478-106">V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 s potvrzením e-mailu a resetováním hesla pomocí systému členství v ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="4a478-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span>

<span data-ttu-id="4a478-107">Aktualizovanou verzi tohoto kurzu, který používá .NET Core, najdete [v tématu potvrzení účtu a obnovení hesla v ASP.NET Core](/aspnet/core/security/authentication/accconfirm).</span><span class="sxs-lookup"><span data-stu-id="4a478-107">For an updated version of this tutorial that uses .NET Core, see [Account confirmation and password recovery in ASP.NET Core](/aspnet/core/security/authentication/accconfirm).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="4a478-108">Vytvoření aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4a478-108">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="4a478-109">Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="4a478-109">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="4a478-110">Nainstalujte [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="4a478-110">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="4a478-111">Upozornění: k dokončení tohoto kurzu je nutné nainstalovat [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="4a478-111">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="4a478-112">Vytvořte nový webový projekt v ASP.NET a vyberte šablonu MVC.</span><span class="sxs-lookup"><span data-stu-id="4a478-112">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="4a478-113">Webové formuláře také podporují ASP.NET Identity, takže můžete postupovat podle podobných kroků v aplikaci webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="4a478-113">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="4a478-114">U **jednotlivých uživatelských účtů**ponechte výchozí ověřování.</span><span class="sxs-lookup"><span data-stu-id="4a478-114">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="4a478-115">Pokud chcete aplikaci hostovat v Azure, nechte zaškrtávací políčko zaškrtnuté.</span><span class="sxs-lookup"><span data-stu-id="4a478-115">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="4a478-116">Později v tomto kurzu provedeme nasazení do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a478-116">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="4a478-117">Můžete si [otevřít účet Azure zdarma](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4a478-117">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="4a478-118">Nastavte [projekt na použití SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4a478-118">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="4a478-119">Spusťte aplikaci, klikněte na odkaz **zaregistrovat** a zaregistrujte uživatele.</span><span class="sxs-lookup"><span data-stu-id="4a478-119">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="4a478-120">V tomto okamžiku je jediným ověřením e-mailu atribut [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) .</span><span class="sxs-lookup"><span data-stu-id="4a478-120">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="4a478-121">V Průzkumník serveru přejděte na **Connections\DefaultConnection\Tables\AspNetUsers dat**, klikněte pravým tlačítkem a vyberte **Otevřít definici tabulky**.</span><span class="sxs-lookup"><span data-stu-id="4a478-121">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="4a478-122">Následující obrázek ukazuje `AspNetUsers` schéma:</span><span class="sxs-lookup"><span data-stu-id="4a478-122">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="4a478-123">Klikněte pravým tlačítkem na tabulku **AspNetUsers** a vyberte **Zobrazit data tabulky**.</span><span class="sxs-lookup"><span data-stu-id="4a478-123">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="4a478-124">V tomto okamžiku nebyl e-mail potvrzen.</span><span class="sxs-lookup"><span data-stu-id="4a478-124">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="4a478-125">Klikněte na řádek a vyberte Odstranit.</span><span class="sxs-lookup"><span data-stu-id="4a478-125">Click on the row and select delete.</span></span> <span data-ttu-id="4a478-126">Tento e-mail přidáte znovu v dalším kroku a odešlete potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="4a478-126">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="4a478-127">Potvrzení e-mailu</span><span class="sxs-lookup"><span data-stu-id="4a478-127">Email confirmation</span></span>

<span data-ttu-id="4a478-128">Osvědčeným postupem je ověření e-mailu nové registrace uživatele, aby se ověřilo, že nezosobňuje někdo jiný (tj. nezaregistroval se v e-mailu někoho jiného).</span><span class="sxs-lookup"><span data-stu-id="4a478-128">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="4a478-129">Předpokládejme, že máte diskuzní fórum, chcete zabránit `"bob@example.com"` registraci jako `"joe@contoso.com"`.</span><span class="sxs-lookup"><span data-stu-id="4a478-129">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="4a478-130">Bez potvrzení e-mailu `"joe@contoso.com"` možné z vaší aplikace získat nechtěný e-mail.</span><span class="sxs-lookup"><span data-stu-id="4a478-130">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="4a478-131">Předpokládejme, že se Bob omylem zaregistrovali jako `"bib@example.com"` a jste si ho všimli, takže by nebylo možné použít obnovení hesla, protože aplikace nemá správný e-mail.</span><span class="sxs-lookup"><span data-stu-id="4a478-131">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="4a478-132">Potvrzení e-mailu poskytuje jenom omezené zabezpečení z roboty a neposkytuje ochranu proti stanoveným odesilatelům nevyžádané pošty. má spoustu pracovních e-mailových aliasů, které můžou použít k registraci.</span><span class="sxs-lookup"><span data-stu-id="4a478-132">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="4a478-133">Obecně je vhodné zabránit novým uživatelům v posílání dat na web před potvrzením e-mailu, textové zprávy SMS nebo jiného mechanismu.</span><span class="sxs-lookup"><span data-stu-id="4a478-133">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="4a478-134">V níže uvedených částech povolíme e-mailové potvrzení a upravíte kód tak, aby se nově zaregistrovaní uživatelé nemohli přihlásit, dokud se nepotvrdí jejich e-maily.</span><span class="sxs-lookup"><span data-stu-id="4a478-134">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="4a478-135">Připojit SendGrid</span><span class="sxs-lookup"><span data-stu-id="4a478-135">Hook up SendGrid</span></span>

<span data-ttu-id="4a478-136">Pokyny v této části nejsou aktuální.</span><span class="sxs-lookup"><span data-stu-id="4a478-136">The instructions in this section are not current.</span></span> <span data-ttu-id="4a478-137">Aktualizované pokyny najdete v tématu [Konfigurace poskytovatele e-mailu SendGrid](/aspnet/core/security/authentication/accconfirm#configure-email-provider) .</span><span class="sxs-lookup"><span data-stu-id="4a478-137">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="4a478-138">I když tento kurz ukazuje, jak přidat e-mailové oznámení prostřednictvím [SendGrid](http://sendgrid.com/), můžete posílat e-maily pomocí protokolu SMTP a dalších mechanismů (viz [Další zdroje informací](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="4a478-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="4a478-139">V konzole správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="4a478-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="4a478-140">Přejít na [stránku registrace Azure SendGrid](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) a zaregistrujte si bezplatný účet SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4a478-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="4a478-141">Nakonfigurujte SendGrid přidáním kódu podobného následujícímu v *app_start/identityconfig.cs*:</span><span class="sxs-lookup"><span data-stu-id="4a478-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="4a478-142">Je potřeba přidat následující:</span><span class="sxs-lookup"><span data-stu-id="4a478-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="4a478-143">Abychom tuto ukázku zachovali jednoduše, uložíme nastavení aplikace do souboru *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="4a478-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="4a478-144">Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="4a478-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="4a478-145">Účet a přihlašovací údaje jsou uložené v appSetting.</span><span class="sxs-lookup"><span data-stu-id="4a478-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="4a478-146">V Azure můžete tyto hodnoty bezpečně uložit na kartě **[Konfigurace](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** v Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4a478-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="4a478-147">Podívejte [se na osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="4a478-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="4a478-148">Povolit potvrzení e-mailu v řadiči účtů</span><span class="sxs-lookup"><span data-stu-id="4a478-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="4a478-149">Ověřte, jestli má soubor *Views\Account\ConfirmEmail.cshtml* správnou syntaxi Razor.</span><span class="sxs-lookup"><span data-stu-id="4a478-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="4a478-150">(Znak @ v prvním řádku může chybět.</span><span class="sxs-lookup"><span data-stu-id="4a478-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="4a478-151">)</span><span class="sxs-lookup"><span data-stu-id="4a478-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="4a478-152">Spusťte aplikaci a klikněte na odkaz zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="4a478-152">Run the app and click the Register link.</span></span> <span data-ttu-id="4a478-153">Po odeslání registračního formuláře jste přihlášeni.</span><span class="sxs-lookup"><span data-stu-id="4a478-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="4a478-154">Zkontrolujte svůj e-mailový účet a kliknutím na odkaz potvrďte svůj e-mail.</span><span class="sxs-lookup"><span data-stu-id="4a478-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="4a478-155">Vyžadovat před přihlášením e-mailové potvrzení</span><span class="sxs-lookup"><span data-stu-id="4a478-155">Require email confirmation before log in</span></span>

<span data-ttu-id="4a478-156">V současné době, kdy uživatel dokončuje registrační formulář, jsou přihlášeni.</span><span class="sxs-lookup"><span data-stu-id="4a478-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="4a478-157">Obecně budete chtít před přihlášením do aplikace potvrdit jejich e-maily.</span><span class="sxs-lookup"><span data-stu-id="4a478-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="4a478-158">V níže uvedené části upravíte kód tak, aby se noví uživatelé museli před přihlášením (ověřeným) povinně potvrdit e-mail.</span><span class="sxs-lookup"><span data-stu-id="4a478-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="4a478-159">Aktualizujte metodu `HttpPost Register` o následující zvýrazněné změny:</span><span class="sxs-lookup"><span data-stu-id="4a478-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="4a478-160">Přidáním komentáře k metodě `SignInAsync` nebude uživatel přihlášený registrací.</span><span class="sxs-lookup"><span data-stu-id="4a478-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="4a478-161">`TempData["ViewBagLink"] = callbackUrl;` řádek lze použít k [ladění aplikace](#dbg) a registraci testu bez odeslání e-mailu.</span><span class="sxs-lookup"><span data-stu-id="4a478-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="4a478-162">`ViewBag.Message` slouží k zobrazení pokynů pro potvrzení.</span><span class="sxs-lookup"><span data-stu-id="4a478-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="4a478-163">[Ukázka stažení](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) obsahuje kód pro otestování potvrzení e-mailu bez nastavení e-mailu a lze jej také použít k ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="4a478-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="4a478-164">Vytvořte soubor `Views\Shared\Info.cshtml` a přidejte následující kód Razor:</span><span class="sxs-lookup"><span data-stu-id="4a478-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="4a478-165">Přidejte [atribut autorizace](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) do metody `Contact` Action domovského kontroleru.</span><span class="sxs-lookup"><span data-stu-id="4a478-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="4a478-166">Kliknutím na odkaz **kontaktů** ověříte, že anonymní uživatelé nemají přístup a že k nim mají přístup i ověření uživatelé.</span><span class="sxs-lookup"><span data-stu-id="4a478-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="4a478-167">Musíte také aktualizovat metodu `HttpPost Login` akce:</span><span class="sxs-lookup"><span data-stu-id="4a478-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="4a478-168">Aktualizujte zobrazení *Views\Shared\Error.cshtml* , aby se zobrazila chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="4a478-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="4a478-169">Odstraňte všechny účty v tabulce **AspNetUsers** , které obsahují e-mailový alias, pomocí kterého chcete testovat.</span><span class="sxs-lookup"><span data-stu-id="4a478-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="4a478-170">Spusťte aplikaci a ověřte, že se nemůžete přihlásit, dokud nepotvrdíte svoji e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="4a478-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="4a478-171">Po potvrzení své e-mailové adresy klikněte na odkaz **kontakt** .</span><span class="sxs-lookup"><span data-stu-id="4a478-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="4a478-172">Obnovení a resetování hesla</span><span class="sxs-lookup"><span data-stu-id="4a478-172">Password recovery/reset</span></span>

<span data-ttu-id="4a478-173">Odeberte znaky komentáře z metody `HttpPost ForgotPassword` akce v řadiči účtů:</span><span class="sxs-lookup"><span data-stu-id="4a478-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="4a478-174">Odeberte znaky komentáře z `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) v souboru zobrazení *Views\Account\Login.cshtml* Razor:</span><span class="sxs-lookup"><span data-stu-id="4a478-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="4a478-175">Přihlašovací stránka se teď zobrazí jako odkaz pro resetování hesla.</span><span class="sxs-lookup"><span data-stu-id="4a478-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="4a478-176">Poslat znovu odkaz na potvrzení e-mailu</span><span class="sxs-lookup"><span data-stu-id="4a478-176">Resend email confirmation link</span></span>

<span data-ttu-id="4a478-177">Jakmile uživatel vytvoří nový místní účet, pošlete jim odkaz na potvrzení, že se musí použít, aby se mohli přihlásit.</span><span class="sxs-lookup"><span data-stu-id="4a478-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="4a478-178">Pokud uživatel omylem odstraní potvrzovací e-mail nebo e-mail nikdy nepřijde, bude potřebovat poslat potvrzovací odkaz znovu.</span><span class="sxs-lookup"><span data-stu-id="4a478-178">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="4a478-179">Následující změny kódu ukazují, jak tuto možnost povolit.</span><span class="sxs-lookup"><span data-stu-id="4a478-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="4a478-180">Do dolní části souboru *Controllers\AccountController.cs* přidejte následující pomocnou metodu:</span><span class="sxs-lookup"><span data-stu-id="4a478-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="4a478-181">Aktualizujte metodu Register pro použití nové pomocné rutiny:</span><span class="sxs-lookup"><span data-stu-id="4a478-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="4a478-182">Aktualizujte metodu login a znovu odešlete heslo, pokud uživatelský účet nebyl potvrzen:</span><span class="sxs-lookup"><span data-stu-id="4a478-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="4a478-183">Kombinování sociálních a místních přihlašovacích účtů</span><span class="sxs-lookup"><span data-stu-id="4a478-183">Combine social and local login accounts</span></span>

<span data-ttu-id="4a478-184">Místní a sociální účty můžete zkombinovat kliknutím na svůj e-mailový odkaz.</span><span class="sxs-lookup"><span data-stu-id="4a478-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="4a478-185">V následující sekvenci **RickAndMSFT@gmail.com** nejdřív vytvoříme jako místní přihlašovací údaje, ale můžete účet vytvořit jako sociální protokol a pak přidat místní přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="4a478-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="4a478-186">Klikněte na odkaz **Správa** .</span><span class="sxs-lookup"><span data-stu-id="4a478-186">Click on the **Manage** link.</span></span> <span data-ttu-id="4a478-187">Všimněte si **externích přihlášení: 0** přidružených k tomuto účtu.</span><span class="sxs-lookup"><span data-stu-id="4a478-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="4a478-188">Klikněte na odkaz na jiný protokol služby a přijměte žádosti o aplikace.</span><span class="sxs-lookup"><span data-stu-id="4a478-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="4a478-189">Tyto dva účty byly zkombinovány, budete se moci přihlásit pomocí obou účtů.</span><span class="sxs-lookup"><span data-stu-id="4a478-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="4a478-190">Je možné, že budete chtít, aby uživatelé mohli přidávat místní účty v případě výpadku služby sociálního protokolu v případě nedostatku nebo pravděpodobně ztratili přístup ke svému sociálnímu účtu.</span><span class="sxs-lookup"><span data-stu-id="4a478-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="4a478-191">Na následujícím obrázku je to, že se jedná o sociální přihlášení (které vidíte z **externích přihlášení: 1** zobrazeno na stránce).</span><span class="sxs-lookup"><span data-stu-id="4a478-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="4a478-192">Kliknutím na **Vybrat heslo** můžete přidat místní přihlašování ke stejnému účtu.</span><span class="sxs-lookup"><span data-stu-id="4a478-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="4a478-193">Podrobnější informace o potvrzení e-mailu</span><span class="sxs-lookup"><span data-stu-id="4a478-193">Email confirmation in more depth</span></span>

<span data-ttu-id="4a478-194">V tomto tématu se zobrazí informace o [potvrzení a obnovení hesla účtu](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) kurzu, které se ASP.NET identity přecházejí do tohoto tématu.</span><span class="sxs-lookup"><span data-stu-id="4a478-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="4a478-195">Ladění aplikace</span><span class="sxs-lookup"><span data-stu-id="4a478-195">Debugging the app</span></span>

<span data-ttu-id="4a478-196">Pokud neobdržíte e-mail s odkazem:</span><span class="sxs-lookup"><span data-stu-id="4a478-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="4a478-197">Ověřte složku s nevyžádanou poštou nebo spamem.</span><span class="sxs-lookup"><span data-stu-id="4a478-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="4a478-198">Přihlaste se k účtu SendGrid a klikněte na [odkaz e-mailová aktivita](https://sendgrid.com/logs/index).</span><span class="sxs-lookup"><span data-stu-id="4a478-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="4a478-199">Pokud chcete otestovat odkaz pro ověření bez e-mailu, Stáhněte si [hotovou ukázku](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="4a478-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="4a478-200">Na stránce se zobrazí potvrzovací odkaz a potvrzovací kódy.</span><span class="sxs-lookup"><span data-stu-id="4a478-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="4a478-201">Další materiály a zdroje informací</span><span class="sxs-lookup"><span data-stu-id="4a478-201">Additional Resources</span></span>

- [<span data-ttu-id="4a478-202">Odkazy na ASP.NET Identity doporučené prostředky</span><span class="sxs-lookup"><span data-stu-id="4a478-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="4a478-203">[Potvrzení účtu a obnovení hesla pomocí ASP.NET identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Přechází na další podrobnosti o obnovení hesla a potvrzení účtu.</span><span class="sxs-lookup"><span data-stu-id="4a478-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="4a478-204">[Aplikace MVC 5 s přihlašováním na Facebooku, Twitteru, LinkedInu a Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) V tomto kurzu se dozvíte, jak napsat aplikaci ASP.NET MVC 5 s autorizací na Facebooku a Google OAuth 2.</span><span class="sxs-lookup"><span data-stu-id="4a478-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="4a478-205">Také ukazuje, jak přidat další data do databáze identity.</span><span class="sxs-lookup"><span data-stu-id="4a478-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="4a478-206">[Nasaďte zabezpečenou aplikaci ASP.NET MVC s členstvím, protokolem OAuth a SQL Database do Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="4a478-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="4a478-207">Tento kurz přidá nasazení Azure, způsob zabezpečení vaší aplikace pomocí rolí, způsob použití rozhraní API pro členství v přidávání uživatelů a rolí a další funkce zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="4a478-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="4a478-208">Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="4a478-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="4a478-209">Vytvoření aplikace na Facebooku a připojení aplikace k projektu</span><span class="sxs-lookup"><span data-stu-id="4a478-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="4a478-210">Nastavení SSL v projektu</span><span class="sxs-lookup"><span data-stu-id="4a478-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
