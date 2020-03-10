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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538442"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>Aplikace ASP.NET MVC 5 s dvoufaktorovým ověřováním pomocí SMS a e-mailu

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5 se dvěma faktory ověřování. Před pokračováním musíte [vytvořit zabezpečenou webovou aplikaci ASP.NET MVC 5 s přihlášením, potvrzením e-mailem a resetováním hesla](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) . Dokončenou aplikaci si můžete stáhnout [tady](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952). Stažení obsahuje ladicí služby, které vám umožní testovat potvrzení e-mailu a SMS bez nastavování e-mailu nebo poskytovatele služby SMS.
> 
> Tento kurz napsal [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).

- [Vytvoření aplikace ASP.NET MVC](#createMvc)
- [Nastavení SMS pro dvojúrovňové ověřování](#SMS)
- [Povolit dvojúrovňové ověřování](#enable2)
- [Další zdroje](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>Vytvoření aplikace ASP.NET MVC

Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Nainstalujte [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.

> [!NOTE]
> Upozornění: před pokračováním musíte [vytvořit zabezpečenou webovou aplikaci ASP.NET MVC 5 s přihlášením, potvrzením e-mailem a resetováním hesla](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) . Chcete-li dokončit tento kurz, je nutné nainstalovat [aktualizaci Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.

1. Vytvořte nový webový projekt v ASP.NET a vyberte šablonu MVC. Webové formuláře také podporují ASP.NET Identity, takže můžete postupovat podle podobných kroků v aplikaci webových formulářů.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. U **jednotlivých uživatelských účtů**ponechte výchozí ověřování. Pokud chcete aplikaci hostovat v Azure, nechte zaškrtávací políčko zaškrtnuté. Později v tomto kurzu provedeme nasazení do Azure. Můžete si [otevřít účet Azure zdarma](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
3. Nastavte [projekt na použití SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a>Nastavení SMS pro dvojúrovňové ověřování

V tomto kurzu najdete pokyny k použití Twilio nebo ASPSMS, ale můžete použít jakéhokoli jiného poskytovatele serveru SMS.

1. **Vytvoření uživatelského účtu pomocí poskytovatele služby SMS**  
  
   Vytvořte účet [Twilio](https://www.twilio.com/try-twilio) nebo [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) .
2. **Instalace dalších balíčků nebo přidávání odkazů na služby**  
  
   Twilio  
   V konzole správce balíčků zadejte následující příkaz:  
    `Install-Package Twilio`  
  
   ASPSMS:  
   Je potřeba přidat následující odkaz na službu:  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   Adresáře  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   Obor názvů:  
    `ASPSMSX2`
3. **Zjišťování přihlašovacích údajů uživatele poskytovatele služby SMS**  
  
   Twilio  
   Na kartě **řídicí panel** účtu Twilio zkopírujte **identifikátor SID účtu** a **ověřovací token**.  
  
   ASPSMS:  
   V nastavení účtu přejděte na **vlastnosti UserKey** a zkopírujte je společně s vaším vlastním **heslem**.  
  
   Tyto hodnoty budeme později ukládat do souboru *Web. config* v rámci klíčů `"SMSAccountIdentification"` a `"SMSAccountPassword"`.
4. **Zadání SenderID/původce**  
  
   Twilio  
   Na kartě **čísla** zkopírujte své Twilio telefonní číslo.  
  
   ASPSMS:  
   V nabídce **odemknout původci** odemkněte jeden nebo více původců nebo vyberte alfanumerický původ (není podporován všemi sítěmi).  
  
   Tuto hodnotu bude později Uloženo v souboru *Web. config* v rámci klíče `"SMSAccountFrom"`.
5. **Přenáší se přihlašovací údaje poskytovatele SMS do aplikace.**  
  
   Nastavte přihlašovací údaje a telefonní číslo odesilatele k aplikaci. Abychom zachovali něco jednoduchého, uložíme tyto hodnoty do souboru *Web. config* . Po nasazení do Azure můžeme hodnoty bezpečně ukládat v části **nastavení aplikace** na kartě Konfigurace webu. 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu. Účet a přihlašovací údaje se přidají do výše uvedeného kódu, aby se ukázka snadno zachovala. Podívejte [se na osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
6. **Implementace přenosu dat do poskytovatele služby SMS**  
  
   Nakonfigurujte třídu `SmsService` v souboru *App\_Start\IdentityConfig.cs* .  
  
   V závislosti na použitém poskytovateli serveru SMS aktivujte **Twilio** nebo část **ASPSMS** : 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. Aktualizace zobrazení *Views\Manage\Index.cshtml* Razor: (Poznámka: Neodstraňujte pouze komentáře v ukončovacím kódu, použijte následující kód.)  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. Ověřte, že metody akcí `EnableTwoFactorAuthentication` a `DisableTwoFactorAuthentication` v `ManageController` mají atribut[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) :  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. Spusťte aplikaci a přihlaste se pomocí účtu, který jste předtím zaregistrovali.
10. Klikněte na své ID uživatele, které aktivuje metodu `Index` akce v kontroleru `Manage`.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. Klikněte na Přidat.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. Metoda `AddPhoneNumber` akce zobrazí dialogové okno pro zadání telefonního čísla, které může přijímat zprávy SMS.

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. Během několika sekund obdržíte textovou zprávu s ověřovacím kódem. Zadejte ji a stiskněte **Odeslat**.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. V zobrazení Správa se zobrazí vaše telefonní číslo.

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>Povolení dvoufaktorového ověřování

V aplikaci vygenerované šablonou je nutné použít uživatelské rozhraní pro povolení dvojúrovňové ověřování (2FA). Pokud chcete povolit 2FA, na navigačním panelu klikněte na své ID uživatele (e-mailový alias).

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

Klikněte na Povolit 2FA.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

Odhlaste se a potom se znovu přihlaste. Pokud jste povolili e-mail (viz můj [předchozí kurz](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), můžete vybrat zprávu SMS nebo E-mail pro 2FA.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

Zobrazí se stránka ověření kódu, kde můžete zadat kód (ze serveru SMS nebo e-mailu).

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

Kliknutím na toto zaškrtávací políčko **prohlížeč zapamatujte** , že nebudete muset používat 2FA k přihlášení při použití prohlížeče a zařízení, kde jste zaškrtli políčko. Pokud uživatelé se zlými úmysly nezískají přístup k vašemu zařízení, povolí 2FA a kliknou na zapamatovat si, že **Tento prohlížeč** vám poskytne pohodlný přístup k heslům, ale přitom zachovává silnou ochranu 2FA pro veškerý přístup z nedůvěryhodných zařízení. Můžete to provést na libovolném privátní zařízení, kterou používáte pravidelně.

V tomto kurzu se seznámíte s tím, jak povolit 2FA v nové aplikaci ASP.NET MVC. Můj kurz [– dvojúrovňové ověřování pomocí SMS a e-mailu s ASP.NET identity se](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) podrobněji odkazuje na kód za ukázkou.

<a id="addRes"></a>
## <a name="additional-resources"></a>Další prostředky

- [Dvojúrovňové ověřování pomocí SMS a e-mailu s ASP.NET identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Přejde na podrobnosti o dvojúrovňové ověřování.
- [Odkazy na ASP.NET Identity doporučené prostředky](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Potvrzení účtu a obnovení hesla pomocí ASP.NET identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Přechází na další podrobnosti o obnovení hesla a potvrzení účtu.
- [Aplikace MVC 5 s přihlašováním na Facebooku, Twitteru, LinkedInu a Google OAuth2](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) V tomto kurzu se dozvíte, jak napsat aplikaci ASP.NET MVC 5 s autorizací na Facebooku a Google OAuth 2. Také ukazuje, jak přidat další data do databáze identity.
- [Nasaďte zabezpečenou aplikaci ASP.NET MVC s členstvím, protokolem OAuth a SQL Database do webu Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Tento kurz přidá nasazení Azure, způsob zabezpečení vaší aplikace pomocí rolí, způsob použití rozhraní API pro členství v přidávání uživatelů a rolí a další funkce zabezpečení.
- [Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Vytvoření aplikace na Facebooku a připojení aplikace k projektu](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [Nastavení SSL v projektu](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [Jak nastavit C# vývojové prostředí ASP.NET MVC](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
