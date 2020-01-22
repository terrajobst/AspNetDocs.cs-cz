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
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu a resetováním hesla (C#)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 s potvrzením e-mailu a resetováním hesla pomocí systému členství v ASP.NET Identity.

Aktualizovanou verzi tohoto kurzu, který používá .NET Core, najdete [v tématu potvrzení účtu a obnovení hesla v ASP.NET Core](/aspnet/core/security/authentication/accconfirm).

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>Vytvoření aplikace ASP.NET MVC

Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Nainstalujte [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.

> [!NOTE]
> Upozornění: k dokončení tohoto kurzu je nutné nainstalovat [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.

1. Vytvořte nový webový projekt v ASP.NET a vyberte šablonu MVC. Webové formuláře také podporují ASP.NET Identity, takže můžete postupovat podle podobných kroků v aplikaci webových formulářů.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. U **jednotlivých uživatelských účtů**ponechte výchozí ověřování. Pokud chcete aplikaci hostovat v Azure, nechte zaškrtávací políčko zaškrtnuté. Později v tomto kurzu provedeme nasazení do Azure. Můžete si [otevřít účet Azure zdarma](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
3. Nastavte [projekt na použití SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
4. Spusťte aplikaci, klikněte na odkaz **zaregistrovat** a zaregistrujte uživatele. V tomto okamžiku je jediným ověřením e-mailu atribut [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) .
5. V Průzkumník serveru přejděte na **Connections\DefaultConnection\Tables\AspNetUsers dat**, klikněte pravým tlačítkem a vyberte **Otevřít definici tabulky**.

    Následující obrázek ukazuje `AspNetUsers` schéma:

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. Klikněte pravým tlačítkem na tabulku **AspNetUsers** a vyberte **Zobrazit data tabulky**.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 V tomto okamžiku nebyl e-mail potvrzen.
7. Klikněte na řádek a vyberte Odstranit. Tento e-mail přidáte znovu v dalším kroku a odešlete potvrzovací e-mail.

## <a name="email-confirmation"></a>Potvrzení e-mailu

Osvědčeným postupem je ověření e-mailu nové registrace uživatele, aby se ověřilo, že nezosobňuje někdo jiný (tj. nezaregistroval se v e-mailu někoho jiného). Předpokládejme, že máte diskuzní fórum, chcete zabránit `"bob@example.com"` registraci jako `"joe@contoso.com"`. Bez potvrzení e-mailu `"joe@contoso.com"` možné z vaší aplikace získat nechtěný e-mail. Předpokládejme, že se Bob omylem zaregistrovali jako `"bib@example.com"` a jste si ho všimli, takže by nebylo možné použít obnovení hesla, protože aplikace nemá správný e-mail. Potvrzení e-mailu poskytuje jenom omezené zabezpečení z roboty a neposkytuje ochranu proti stanoveným odesilatelům nevyžádané pošty. má spoustu pracovních e-mailových aliasů, které můžou použít k registraci.

Obecně je vhodné zabránit novým uživatelům v posílání dat na web před potvrzením e-mailu, textové zprávy SMS nebo jiného mechanismu. <a id="build"></a>V níže uvedených částech povolíme e-mailové potvrzení a upravíte kód tak, aby se nově zaregistrovaní uživatelé nemohli přihlásit, dokud se nepotvrdí jejich e-maily.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>Připojit SendGrid

Pokyny v této části nejsou aktuální. Aktualizované pokyny najdete v tématu [Konfigurace poskytovatele e-mailu SendGrid](/aspnet/core/security/authentication/accconfirm#configure-email-provider) .

I když tento kurz ukazuje, jak přidat e-mailové oznámení prostřednictvím [SendGrid](http://sendgrid.com/), můžete posílat e-maily pomocí protokolu SMTP a dalších mechanismů (viz [Další zdroje informací](#addRes)).

1. V konzole správce balíčků zadejte následující příkaz: 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. Přejít na [stránku registrace Azure SendGrid](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) a zaregistrujte si bezplatný účet SendGrid. Nakonfigurujte SendGrid přidáním kódu podobného následujícímu v *app_start/identityconfig.cs*:

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

Je potřeba přidat následující:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

Abychom tuto ukázku zachovali jednoduše, uložíme nastavení aplikace do souboru *Web. config* :

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu. Účet a přihlašovací údaje jsou uložené v appSetting. V Azure můžete tyto hodnoty bezpečně uložit na kartě **[Konfigurace](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** v Azure Portal. Podívejte [se na osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).

### <a name="enable-email-confirmation-in-the-account-controller"></a>Povolit potvrzení e-mailu v řadiči účtů

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

Ověřte, jestli má soubor *Views\Account\ConfirmEmail.cshtml* správnou syntaxi Razor. (Znak @ v prvním řádku může chybět. )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

Spusťte aplikaci a klikněte na odkaz zaregistrovat. Po odeslání registračního formuláře jste přihlášeni.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

Zkontrolujte svůj e-mailový účet a kliknutím na odkaz potvrďte svůj e-mail.

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>Vyžadovat před přihlášením e-mailové potvrzení

V současné době, kdy uživatel dokončuje registrační formulář, jsou přihlášeni. Obecně budete chtít před přihlášením do aplikace potvrdit jejich e-maily. V níže uvedené části upravíte kód tak, aby se noví uživatelé museli před přihlášením (ověřeným) povinně potvrdit e-mail. Aktualizujte metodu `HttpPost Register` o následující zvýrazněné změny:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

Přidáním komentáře k metodě `SignInAsync` nebude uživatel přihlášený registrací. `TempData["ViewBagLink"] = callbackUrl;` řádek lze použít k [ladění aplikace](#dbg) a registraci testu bez odeslání e-mailu. `ViewBag.Message` slouží k zobrazení pokynů pro potvrzení. [Ukázka stažení](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) obsahuje kód pro otestování potvrzení e-mailu bez nastavení e-mailu a lze jej také použít k ladění aplikace.

Vytvořte soubor `Views\Shared\Info.cshtml` a přidejte následující kód Razor:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

Přidejte [atribut autorizace](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) do metody `Contact` Action domovského kontroleru. Kliknutím na odkaz **kontaktů** ověříte, že anonymní uživatelé nemají přístup a že k nim mají přístup i ověření uživatelé.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

Musíte také aktualizovat metodu `HttpPost Login` akce:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

Aktualizujte zobrazení *Views\Shared\Error.cshtml* , aby se zobrazila chybová zpráva:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

Odstraňte všechny účty v tabulce **AspNetUsers** , které obsahují e-mailový alias, pomocí kterého chcete testovat. Spusťte aplikaci a ověřte, že se nemůžete přihlásit, dokud nepotvrdíte svoji e-mailovou adresu. Po potvrzení své e-mailové adresy klikněte na odkaz **kontakt** .

<a id="reset"></a>
## <a name="password-recoveryreset"></a>Obnovení a resetování hesla

Odeberte znaky komentáře z metody `HttpPost ForgotPassword` akce v řadiči účtů:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

Odeberte znaky komentáře z `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) v souboru zobrazení *Views\Account\Login.cshtml* Razor:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

Přihlašovací stránka se teď zobrazí jako odkaz pro resetování hesla.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>Poslat znovu odkaz na potvrzení e-mailu

Jakmile uživatel vytvoří nový místní účet, pošlete jim odkaz na potvrzení, že se musí použít, aby se mohli přihlásit. Pokud uživatel omylem odstraní potvrzovací e-mail nebo e-mail nikdy nepřijde, bude potřebovat poslat potvrzovací odkaz znovu. Následující změny kódu ukazují, jak tuto možnost povolit.

Do dolní části souboru *Controllers\AccountController.cs* přidejte následující pomocnou metodu:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

Aktualizujte metodu Register pro použití nové pomocné rutiny:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

Aktualizujte metodu login a znovu odešlete heslo, pokud uživatelský účet nebyl potvrzen:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>Kombinování sociálních a místních přihlašovacích účtů

Místní a sociální účty můžete zkombinovat kliknutím na svůj e-mailový odkaz. V následující sekvenci **RickAndMSFT@gmail.com** nejdřív vytvoříme jako místní přihlašovací údaje, ale můžete účet vytvořit jako sociální protokol a pak přidat místní přihlašovací údaje.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

Klikněte na odkaz **Správa** . Všimněte si **externích přihlášení: 0** přidružených k tomuto účtu.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

Klikněte na odkaz na jiný protokol služby a přijměte žádosti o aplikace. Tyto dva účty byly zkombinovány, budete se moci přihlásit pomocí obou účtů. Je možné, že budete chtít, aby uživatelé mohli přidávat místní účty v případě výpadku služby sociálního protokolu v případě nedostatku nebo pravděpodobně ztratili přístup ke svému sociálnímu účtu.

Na následujícím obrázku je to, že se jedná o sociální přihlášení (které vidíte z **externích přihlášení: 1** zobrazeno na stránce).

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

Kliknutím na **Vybrat heslo** můžete přidat místní přihlašování ke stejnému účtu.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>Podrobnější informace o potvrzení e-mailu

V tomto tématu se zobrazí informace o [potvrzení a obnovení hesla účtu](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) kurzu, které se ASP.NET identity přecházejí do tohoto tématu.

<a id="dbg"></a>
## <a name="debugging-the-app"></a>Ladění aplikace

Pokud neobdržíte e-mail s odkazem:

- Ověřte složku s nevyžádanou poštou nebo spamem.
- Přihlaste se k účtu SendGrid a klikněte na [odkaz e-mailová aktivita](https://sendgrid.com/logs/index).

Pokud chcete otestovat odkaz pro ověření bez e-mailu, Stáhněte si [hotovou ukázku](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952). Na stránce se zobrazí potvrzovací odkaz a potvrzovací kódy.

<a id="addRes"></a>
## <a name="additional-resources"></a>Další materiály a zdroje informací

- [Odkazy na ASP.NET Identity doporučené prostředky](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Potvrzení účtu a obnovení hesla pomocí ASP.NET identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Přechází na další podrobnosti o obnovení hesla a potvrzení účtu.
- [Aplikace MVC 5 s přihlašováním na Facebooku, Twitteru, LinkedInu a Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) V tomto kurzu se dozvíte, jak napsat aplikaci ASP.NET MVC 5 s autorizací na Facebooku a Google OAuth 2. Také ukazuje, jak přidat další data do databáze identity.
- [Nasaďte zabezpečenou aplikaci ASP.NET MVC s členstvím, protokolem OAuth a SQL Database do Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Tento kurz přidá nasazení Azure, způsob zabezpečení vaší aplikace pomocí rolí, způsob použití rozhraní API pro členství v přidávání uživatelů a rolí a další funkce zabezpečení.
- [Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Vytvoření aplikace na Facebooku a připojení aplikace k projektu](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [Nastavení SSL v projektu](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
