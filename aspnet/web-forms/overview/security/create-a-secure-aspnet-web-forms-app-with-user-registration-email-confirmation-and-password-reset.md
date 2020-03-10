---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: Vytvoření zabezpečené aplikace webových formulářů ASP.NET pomocí registrace uživatele, potvrzení e-mailu a resetování hesla (C#) | Microsoft Docs
author: Erikre
description: V tomto kurzu se dozvíte, jak vytvořit aplikaci webových formulářů ASP.NET s registrací uživatele, potvrzením e-mailu a resetováním hesla pomocí člena ASP.NET Identity...
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: af3653bc164810126bc3bf8f1b1794d75642d807
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78625151"
---
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a>Vytvoření zabezpečené aplikace webových formulářů ASP.NET s registrací uživatele, potvrzením e-mailu a resetováním hesla (C#)

od [Erik Reitan](https://github.com/Erikre)

> V tomto kurzu se dozvíte, jak vytvořit aplikaci webových formulářů ASP.NET s registrací uživatele, potvrzením e-mailu a resetováním hesla pomocí systému členství v ASP.NET Identity. Tento kurz vychází z [kurzu MVC](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)pro Rick Anderson.

## <a name="introduction"></a>Úvod

Tento kurz vás provede kroky potřebnými k vytvoření aplikace webových formulářů ASP.NET pomocí sady Visual Studio a ASP.NET 4,5 k vytvoření zabezpečené aplikace webových formulářů s registrací uživatelů, potvrzením e-mailu a resetováním hesla.

### <a name="tutorial-tasks-and-information"></a>Úlohy a informace kurzu:

- [Vytvoření aplikace webových formulářů v ASP.NET](#createWebForms)
- [Připojit SendGrid](#SG)
- [Vyžadovat před přihlášením e-mailové potvrzení](#require)
- [Obnovení a resetování hesla](#reset)
- [Poslat znovu odkaz na potvrzení e-mailu](#rsend)
- [Řešení potíží s aplikací](#dbg)
- [Další zdroje](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>Vytvoření aplikace webových formulářů v ASP.NET

Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Nainstalujte taky [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.

> [!NOTE]
> Upozornění: k dokončení tohoto kurzu je nutné nainstalovat [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) nebo vyšší.

1. Vytvořte nový projekt (**soubor** -&gt; **Nový projekt**) a v dialogovém okně **Nový projekt** vyberte šablonu **Webová aplikace ASP.NET** a nejnovější verzi .NET Framework.
2. V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu **webových formulářů** . U **jednotlivých uživatelských účtů**ponechte výchozí ověřování. Pokud chcete aplikaci hostovat v Azure, ponechejte zaškrtnuté políčko **hostitel v cloudu** .   
 Potom kliknutím na tlačítko **OK** vytvořte nový projekt.  
    Dialogové okno ![nový projekt v ASP.NET](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)
3. Povolte SSL (Secure Sockets Layer) (SSL) pro projekt. Postupujte podle kroků, které jsou k dispozici v části **povolení SSL pro projekt** v Začínáme v rámci [řady kurzů pro webové formuláře](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).
4. Spusťte aplikaci, klikněte na odkaz **zaregistrovat** a zaregistrujte nového uživatele. V tomto okamžiku je jediným ověřením e-mailu založené na atributu [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) , aby byla e-mailová adresa ve správném formátu. Úpravou kódu budete moct přidat potvrzení e-mailu. Zavřete okno prohlížeče.
5. V **Průzkumník serveru** sady Visual Studio (**zobrazení** -&gt; **Průzkumník serveru**) přejděte na **Connections\DefaultConnection\Tables\AspNetUsers dat**, klikněte pravým tlačítkem a vyberte možnost **Otevřít definici tabulky**. 

    Následující obrázek ukazuje schéma `AspNetUsers` tabulky:

    ![Schéma tabulky AspNetUsers](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. V **Průzkumník serveru**klikněte pravým tlačítkem myši na tabulku **AspNetUsers** a vyberte možnost **Zobrazit data tabulky**.  
  
    ![Data tabulky AspNetUsers](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 V tomto okamžiku nebyl potvrzen e-mail pro registrovaného uživatele.
7. Pokud chcete uživatele odstranit, klikněte na řádek a vyberte Odstranit. Tento e-mail přidáte znovu v dalším kroku a odešlete potvrzovací zprávu na e-mailovou adresu.

## <a name="email-confirmation"></a>Potvrzení e-mailu

Je osvědčeným postupem ověření e-mailu při registraci nového uživatele, aby se ověřilo, že nezosobňuje někoho jiného (tj. není zaregistrovaný v e-mailu někoho jiného). Předpokládejme, že máte diskuzní fórum, chcete zabránit `"bob@cpandl.com"` registraci jako `"joe@contoso.com"`. Bez potvrzení e-mailu `"joe@contoso.com"` možné z vaší aplikace získat nechtěný e-mail. Předpokládejme, že se Bob omylem zaregistrovali jako `"bib@cpandl.com"` a jste si ho všimli, ale nemohlo použít obnovení hesla, protože aplikace nemá správný e-mail. Potvrzení e-mailu poskytuje jenom omezené ochrany z roboty a neposkytuje ochranu před určenými odesilateli nevyžádané pošty.

Obecně je vhodné zabránit novým uživatelům v posílání jakýchkoli dat na web před potvrzením e-mailu, textové zprávy SMS nebo jiného mechanismu. V níže uvedených částech povolíme e-mailové potvrzení a upravíte kód tak, aby se nově zaregistrovaní uživatelé nemohli přihlásit, dokud se nepotvrdí jejich e-maily. V tomto kurzu použijete e-mailovou službu SendGrid.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>Připojit SendGrid

SendGrid změnila rozhraní API od chvíle, kdy byl tento kurz napsán. Aktuální pokyny pro SendGrid najdete v tématu [SendGrid](http://sendgrid.com/) nebo [Povolení potvrzení účtu a obnovení hesla](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery).

I když tento kurz ukazuje, jak přidat e-mailové oznámení prostřednictvím [SendGrid](http://sendgrid.com/), můžete posílat e-maily pomocí protokolu SMTP a dalších mechanismů (viz [Další zdroje informací](#addRes)).

1. V aplikaci Visual Studio otevřete **konzolu správce** balíčků (**nástroje** -&gt; správce **balíčků NuGet** -&gt; **konzole správce balíčků**) a zadejte následující příkaz:  
    `Install-Package SendGrid`
2. Přejdete na [stránku registrace Azure SendGrid](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) a zaregistrujete se na bezplatný účet SendGrid. Bezplatný účet SendGrid můžete také zaregistrovat přímo na [webu SendGrid](http://www.sendgrid.com).
3. Z **Průzkumník řešení** otevřete soubor *IdentityConfig.cs* ve složce *App\_Start* a přidejte následující kód zvýrazněný žlutě do třídy `EmailService`, abyste mohli nakonfigurovat **SendGrid**:

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. Na začátek souboru *IdentityConfig.cs* přidejte také následující příkazy `using`: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. Chcete-li tuto ukázku uchovávat snadno, uložte hodnoty účtu e-mailové služby do části `appSettings` v souboru *Web. config* . Přidejte následující kód XML zvýrazněný žlutě do souboru *Web. config* v kořenovém adresáři projektu:

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu. V tomto příkladu je účet a přihlašovací údaje uložené v části **AppSetting** souboru *Web. config* . V Azure můžete tyto hodnoty bezpečně uložit na kartě **[Konfigurace](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** v Azure Portal. Související informace najdete v tématu Rick Anderson s názvem [osvědčené postupy pro nasazování hesel a dalších citlivých dat do ASP.NET a Azure](https://go.microsoft.com/fwlink/?LinkId=513141).
6. Přidejte hodnoty e-mailové služby tak, aby odrážely vaše hodnoty ověřování SendGrid (uživatelské jméno a heslo), abyste mohli úspěšně odesílat e-maily z vaší aplikace. Nezapomeňte místo e-mailové adresy, kterou jste zadali SendGrid, použít název svého účtu SendGrid.

### <a name="enable-email-confirmation"></a>Povolit potvrzení e-mailu

 Chcete-li povolit e-mailové potvrzení, upravte registrační kód pomocí následujících kroků.  

1. Ve složce *account (účet* ) otevřete kód *Register.aspx.cs* a aktualizujte metodu `CreateUser_Click`, abyste povolili následující zvýrazněné změny: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. V **Průzkumník řešení**klikněte pravým tlačítkem myši na *Default. aspx* a vyberte **nastavit jako úvodní stránku**.
3. Spusťte aplikaci stisknutím klávesy **F5.** Po zobrazení stránky klikněte na odkaz **zaregistrovat** , aby se zobrazila stránka registrace.
4. Zadejte svůj e-mail a heslo a potom kliknutím na tlačítko **zaregistrovat** odešlete e-mailovou zprávu přes SendGrid.  
   Aktuální stav projektu a kódu umožní uživateli, aby se přihlásili po dokončení registračního formuláře, i když nepotvrzují svůj účet.
5. Zkontrolujte svůj e-mailový účet a kliknutím na odkaz potvrďte svůj e-mail.  
   Po odeslání registračního formuláře budete přihlášeni.  
    ![Ukázkový web – přihlášený](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>Vyžadovat před přihlášením e-mailové potvrzení

I když jste e-mailový účet potvrdili, nemusíte v tomto okamžiku kliknout na odkaz obsažený v ověřovacím e-mailu, abyste mohli plně přihlášeni. V následující části upravíte kód, který vyžaduje, aby noví uživatelé měli potvrzené e-maily, než se přihlásí (budou ověřeni).

1. V **Průzkumník řešení** sady Visual Studio aktualizujte událost `CreateUser_Click` v kódu *Register.aspx.cs* na pozadí, který je obsažený ve složce *Accounts* , s následujícími zvýrazněnými změnami: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. Aktualizujte metodu `LogIn` v kódu *Login.aspx.cs* na pozadí s následujícími zvýrazněnými změnami: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a>Spuštění aplikace

 Teď, když jste implementovali kód, abyste zkontrolovali, jestli je e-mailová adresa uživatele potvrzená, můžete zjistit **funkčnost na** **přihlašovacích a přihlašovacích** stránkách. 

1. Odstraňte všechny účty v tabulce **AspNetUsers** , které obsahují e-mailový alias, který chcete otestovat.
2. Spusťte aplikaci (**F5**) a ověřte, že se nemůžete zaregistrovat jako uživatel, dokud nepotvrdíte svoji e-mailovou adresu.
3. Před potvrzením nového účtu prostřednictvím e-mailu, který se právě poslal, se pokuste přihlásit pomocí nového účtu.  
 Uvidíte, že se nemůžete přihlásit a že musíte mít potvrzený e-mailový účet.
4. Po potvrzení své e-mailové adresy se přihlaste k aplikaci.

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a>Obnovení a resetování hesla

1. V aplikaci Visual Studio odeberte znaky komentářů z metody `Forgot` v kódu *Forgot.aspx.cs* na pozadí, který je obsažený ve složce *účtu* , aby se metoda zobrazila takto: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. Otevřete stránku *Login. aspx* . Nahraďte značku na konci oddílu **loginForm** , jak je zvýrazněno níže: 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. Otevřete *Login.aspx.cs* kód na pozadí a odkomentujte následující řádek kódu zvýrazněný žlutě od obslužné rutiny události `Page_Load`: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. Spusťte aplikaci stisknutím klávesy **F5.** Po zobrazení stránky klikněte na odkaz **Přihlásit** se.
5. Klikněte na odkaz **zapomenuté heslo?** . zobrazí se stránka **zapomenuté heslo** .
6. Zadejte svou e-mailovou adresu a kliknutím na tlačítko **Odeslat** odešlete e-mail na adresu, která vám umožní resetovat heslo.   
   Ověřte e-mailový účet a kliknutím na odkaz zobrazte stránku pro **resetování hesla** .
7. Na stránce **resetovat heslo** zadejte svůj e-mail, heslo a potvrzení hesla. Pak stiskněte tlačítko **obnovit** .  
   Po úspěšném resetování hesla se zobrazí stránka **změněné heslo** . Nyní se můžete přihlásit pomocí nového hesla.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>Poslat znovu odkaz na potvrzení e-mailu

Jakmile uživatel vytvoří nový místní účet, pošlete jim odkaz na potvrzení, že se musí použít, aby se mohli přihlásit. Pokud uživatel omylem odstraní potvrzovací e-mail nebo e-mail nikdy nepřijde, bude potřebovat poslat potvrzovací odkaz znovu. Následující změny kódu ukazují, jak tuto možnost povolit.

1. V aplikaci Visual Studio otevřete **Login.aspx.cs** kód na pozadí a přidejte následující obslužnou rutinu události za obslužnou rutinu události `LogIn`:   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. Upravte obslužnou rutinu události `LogIn` v kódu *Login.aspx.cs* na pozadí změnou kódu zvýrazněného žlutě následujícím způsobem: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. Stránku *Login. aspx* aktualizujte tak, že přidáte kód zvýrazněný žlutě, jak je znázorněno níže: 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. Odstraňte všechny účty v tabulce **AspNetUsers** , které obsahují e-mailový alias, který chcete otestovat.
5. Spusťte aplikaci (**F5**) a zaregistrujte svou e-mailovou adresu.
6. Před potvrzením nového účtu prostřednictvím e-mailu, který se právě poslal, se pokuste přihlásit pomocí nového účtu.  
   Uvidíte, že se nemůžete přihlásit a že musíte mít potvrzený e-mailový účet. Kromě toho teď můžete znovu poslat potvrzovací zprávu na váš e-mailový účet.
7. Zadejte svou e-mailovou adresu a heslo a potom klikněte na tlačítko **znovu odeslat potvrzení** .
8. Po potvrzení e-mailové adresy na základě nově odeslané e-mailové zprávy se přihlaste k aplikaci.

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a>Řešení potíží s aplikací

Pokud neobdržíte e-mail obsahující odkaz pro ověření vašich přihlašovacích údajů:

- Ověřte složku s nevyžádanou poštou nebo spamem.
- Přihlaste se k účtu SendGrid a klikněte na [odkaz e-mailová aktivita](https://sendgrid.com/logs/index).
- Měli byste použít název uživatelského účtu SendGrid jako hodnotu *Web. config* , a ne svou e-mailovou adresu účtu SendGrid.

<a id="addRes"></a>
## <a name="additional-resources"></a>Další prostředky

- [Odkazy na ASP.NET Identity doporučené prostředky](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [Potvrzení účtu a obnovení hesla pomocí ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Série kurzů pro webové formuláře v ASP.NET – přidání poskytovatele OAuth 2,0](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [Nasazení zabezpečené aplikace webových formulářů ASP.NET pomocí členství, protokolu OAuth a SQL Database pro Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [Série kurzů pro webové formuláře v ASP.NET – povolení SSL pro projekt](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
