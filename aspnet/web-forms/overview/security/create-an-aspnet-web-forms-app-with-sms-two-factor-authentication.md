---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: Vytvoření aplikace webových formulářů v ASP.NET pomocí služby ověřování serveru SMS (C#) | Microsoft Docs
author: Erikre
description: V tomto kurzu se dozvíte, jak vytvořit aplikaci webových formulářů ASP.NET se dvěma faktory ověřování. Tento kurz je navržený tak, aby vyplnil kurz s názvem CR...
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c9558aca8a655071c0c94ed66433cf721f26c011
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78565462"
---
# <a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>Vytvoření aplikace webových formulářů ASP.NET s dvoufaktorovým ověřováním prostřednictvím SMS (C#)

od [Erik Reitan](https://github.com/Erikre)

[Stažení aplikace webových formulářů ASP.NET s využitím e-mailu a ověření SMS pomocí dvou faktorů](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> V tomto kurzu se dozvíte, jak vytvořit aplikaci webových formulářů ASP.NET se dvěma faktory ověřování. Tento kurz je navržený tak, aby vyplnil kurz [s názvem vytvoření zabezpečené aplikace webového formuláře ASP.NET s registrací uživatele, potvrzením e-mailu a resetováním hesla](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md). Tento kurz je navíc založený na [kurzu MVC](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)pro Rick Anderson.

## <a name="introduction"></a>Úvod

Tento kurz vás provede kroky potřebnými k vytvoření aplikace webových formulářů ASP.NET, která podporuje dvojúrovňové ověřování pomocí sady Visual Studio. Dvojúrovňové ověřování je dodatečným krokem ověření uživatele. Tento dodatečný krok generuje během přihlašování jedinečné osobní identifikační číslo (PIN). PIN kód se obvykle pošle uživateli jako e-mail nebo zpráva SMS. Uživatel vaší aplikace pak zadá PIN kód jako dodatečnou ověřovací míru při přihlašování.

### <a name="tutorial-tasks-and-information"></a>Úlohy a informace kurzu:

- [Vytvoření aplikace webových formulářů v ASP.NET](#createWebForms)
- [Nastavení SMS a dvojúrovňové ověřování](#SMS)
- [Povolit dvojúrovňové ověřování pro registrovaného uživatele](#use2FA)
- [Další zdroje](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>Vytvoření aplikace webových formulářů v ASP.NET

Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Nainstalujte taky [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší. Také budete muset vytvořit účet [Twilio](https://www.twilio.com/try-twilio) , jak je vysvětleno níže.

> [!NOTE]
> Důležité: k dokončení tohoto kurzu musíte nainstalovat [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.

1. Vytvořte nový projekt (**soubor** -&gt; **Nový projekt**) a v dialogovém okně **Nový projekt** vyberte šablonu **Webová aplikace ASP.NET** spolu s .NET Framework verzí 4.5.2.
2. V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu **webových formulářů** . U **jednotlivých uživatelských účtů**ponechte výchozí ověřování. Potom kliknutím na tlačítko **OK** vytvořte nový projekt.  
    Dialogové okno ![nový projekt v ASP.NET](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. Povolte SSL (Secure Sockets Layer) (SSL) pro projekt. Postupujte podle kroků, které jsou k dispozici v části **povolení SSL pro projekt** v Začínáme v rámci [řady kurzů pro webové formuláře](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).
4. V aplikaci Visual Studio otevřete **konzolu správce** balíčků (**nástroje** -&gt; správce **balíčků NuGet** -&gt; **konzole správce balíčků**) a zadejte následující příkaz:  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>Nastavení SMS a dvojúrovňové ověřování

V tomto kurzu se používá Twilio, ale můžete použít libovolného poskytovatele služby SMS.

1. Vytvořte účet [Twilio](https://www.twilio.com/try-twilio) .
2. Na kartě **řídicí panel** účtu Twilio zkopírujte **identifikátor SID účtu** a **ověřovací token.** Později je přidáte do své aplikace.
3. Na kartě **čísla** zkopírujte také **telefonní číslo** Twilio.
4. Pro aplikaci zpřístupníte **identifikátor SID účtu**Twilio, **ověřovací token** a **telefonní číslo** . Chcete-li zachovat věci jednoduché, uložte tyto hodnoty do souboru *Web. config* . Když nasadíte do Azure, můžete hodnoty bezpečně ukládat do oddílu **appSettings** na kartě Konfigurace webu. Při přidávání telefonního čísla se taky používají jenom čísla.   
   Všimněte si, že můžete také přidat přihlašovací údaje SendGrid. SendGrid je služba e-mailových oznámení. Podrobnosti o tom, jak povolit SendGrid, najdete v části "připojení SendGrid" v kurzu [s názvem vytvoření zabezpečené ASP.NET aplikace webových formulářů s registrací uživatele, potvrzení e-mailu a resetování hesla.](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu. V tomto příkladu je účet a přihlašovací údaje uložené v oddílu **appSettings** souboru *Web. config* . V Azure můžete tyto hodnoty bezpečně uložit na kartě **[Konfigurace](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** v Azure Portal. Související informace najdete v tématu Rick Anderson s názvem [osvědčené postupy pro nasazování hesel a dalších citlivých dat do ASP.NET a Azure](/aspnet/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
5. V souboru *App\_Start\IdentityConfig.cs* nakonfigurujte třídu `SmsService` tím, že provedete následující změny zvýrazněné žlutě: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. Na začátek souboru *IdentityConfig.cs* přidejte následující příkazy `using`: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. Aktualizujte soubor *account/Manage. aspx* odebráním zvýrazněných řádků žlutě:  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. V obslužné rutině `Page_Load` *Manage.aspx.cs* kódu na pozadí odkomentujte řádek kódu zvýrazněný žlutě, aby se zobrazil jako následující: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. V CodeBehind *účtu*/*TwoFactorAuthenticationSignIn.aspx.cs*aktualizujte obslužnou rutinu `Page_Load` přidáním následujícího kódu zvýrazněného žlutě: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   Tím, že se výše uvedená změna kódu provede, neobnoví se u ovládacího prvků "zprostředkovatelé", který obsahuje možnosti ověřování, první hodnota. Umožní uživateli úspěšně vybrat všechny možnosti, které se mají použít při ověřování, nikoli jenom první.
10. V **Průzkumník řešení**klikněte pravým tlačítkem myši na *Default. aspx* a vyberte **nastavit jako úvodní stránku**.
11. Otestováním aplikace nejprve sestavte aplikaci (**Ctrl**+**SHIFT**+**B**) a pak spusťte aplikaci (**F5**) a buď vyberte možnost **Registrovat** , chcete-li vytvořit nový uživatelský účet, nebo vyberte možnost **Přihlásit se v** případě, že byl uživatelský účet již zaregistrován.
12. Po přihlášení (jako uživatel) na navigačním panelu klikněte na ID uživatele (e-mailová adresa) a zobrazte stránku **Spravovat účet** (spravovat. aspx).  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. Klikněte na **Přidat** další k **telefonnímu číslu** na stránce **Spravovat účet** .  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. Přidejte telefonní číslo, kde jste vy (jako uživatel) mohli přijímat zprávy SMS (textové zprávy), a klikněte na tlačítko **Odeslat** .   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    V tomto okamžiku aplikace použije přihlašovací údaje ze *souboru Web. config* ke kontaktování Twilio. Zpráva SMS (textová zpráva) se pošle na telefon přidružený k uživatelskému účtu. Můžete ověřit, že se zpráva Twilio poslala zobrazením řídicího panelu Twilio.
15. Během několika sekund obdrží telefon přidružený k uživatelskému účtu textovou zprávu obsahující ověřovací kód. Zadejte ověřovací kód a stiskněte **Odeslat**.  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>Povolení dvojúrovňového ověřování u registrovaného uživatele

V tuto chvíli jste povolili dvojúrovňové ověřování pro vaši aplikaci. Aby uživatel mohl použít dvojúrovňové ověřování, může jednoduše změnit jejich nastavení pomocí uživatelského rozhraní. 

1. Jako uživatel vaší aplikace můžete povolit dvojúrovňové ověřování pro konkrétní účet kliknutím na ID uživatele (e-mailový alias) na navigačním panelu, abyste zobrazili stránku **Spravovat účet** . Potom kliknutím na odkaz **Povolit** povolte pro tento účet dvojúrovňové ověřování.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. Odhlaste se a potom se znovu přihlaste. Pokud jste povolili e-mail, můžete pro dvojúrovňové ověřování vybrat buď zprávu SMS, nebo e-mail. Pokud jste nepovolili e-mail, přečtěte si kurz [s názvem vytvoření zabezpečené aplikace webových formulářů ASP.NET pomocí registrace uživatele, potvrzení e-mailu a resetování hesla](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. Zobrazí se stránka se dvěma faktory ověřování, kde můžete zadat kód (ze serveru SMS nebo e-mailu).![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 Kliknutím na **Zapamatovat si tento prohlížeč** zabráníte tomu, abyste se přihlásili Pomocí dvojúrovňového ověřování, když použijete prohlížeč a zařízení, kde jste zaškrtli políčko. Pokud uživatelé se zlými úmysly nemůžou získat přístup k vašemu zařízení, povolit dvojúrovňové ověřování a kliknout na **Zapamatovat si tento prohlížeč** , nabídne vám pohodlný přístup k heslu a zároveň si zachová ochranu silným dvojúrovňovém ověřováním pro veškerý přístup z nedůvěryhodných zařízení. Můžete to provést na libovolném privátní zařízení, kterou používáte pravidelně.

<a id="addRes"></a>
## <a name="additional-resources"></a>Další prostředky

- [Dvoufaktorové ověřování pomocí SMS a e-mailu s ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [Odkazy na ASP.NET Identity doporučené prostředky](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Nasazení zabezpečené aplikace webových formulářů ASP.NET pomocí členství, protokolu OAuth a SQL Database na web Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [Série kurzů pro webové formuláře v ASP.NET – přidání poskytovatele OAuth 2,0](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [Série kurzů pro webové formuláře v ASP.NET – povolení SSL pro projekt](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [Potvrzení účtu a obnovení hesla pomocí ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Vytvoření aplikace na Facebooku a připojení aplikace k projektu](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
