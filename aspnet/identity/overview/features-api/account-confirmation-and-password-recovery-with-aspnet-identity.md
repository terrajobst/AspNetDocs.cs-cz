---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: Potvrzení účtu & obnovení hesla-ASP.NET Identity (C#)-ASP.NET 4. x
author: HaoK
description: Před provedením tohoto kurzu byste měli nejdřív dokončit vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu a resetováním hesla. Tento kurz...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4b2c88280df39aa81d60f9508910e8fe5d6db6b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616814"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>Potvrzení účtu a obnovení hesla pomocí ASP.NET Identity (C#)

> Před provedením tohoto kurzu byste měli nejdřív dokončit [Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu a resetováním hesla](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md). Tento kurz obsahuje další podrobnosti a ukáže vám, jak nastavit e-mail pro potvrzení místního účtu a umožní uživatelům resetovat zapomenuté heslo v ASP.NET Identity.

Místní uživatelský účet vyžaduje, aby uživatel vytvořil heslo pro účet a toto heslo bylo uloženo (bezpečně) ve webové aplikaci. ASP.NET Identity také podporuje účty sociálních sítí, které nevyžadují, aby uživatel pro aplikaci vytvořil heslo. [Účty sociálních sítí](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) používají k ověřování uživatelů třetí stranu (například Google, Twitter, Facebook nebo Microsoft). Toto téma obsahuje následující témata:

- [Vytvořte aplikaci ASP.NET MVC](#createMvc) a prozkoumejte funkce ASP.NET identity.
- [Sestavení ukázky identity](#build)
- [Nastavení potvrzení e-mailu](#email)

Noví uživatelé registrují svůj e-mailový alias, který vytvoří místní účet.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

Po výběru tlačítka zaregistrovat se na svou e-mailovou adresu pošle potvrzovací e-mail s ověřovacím tokenem.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

Uživateli se pošle e-mail s potvrzovacím tokenem pro svůj účet.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

Po výběru tohoto odkazu se účet potvrdí.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>Obnovení a resetování hesla

Místní uživatelé, kteří si zapomene heslo, můžou mít token zabezpečení odeslaný na svůj e-mailový účet, který jim umožňuje resetovat heslo.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
Uživatel brzy získá e-mail s odkazem, který jim umožňuje resetovat heslo.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
Výběr odkazu se převezme na stránku resetovat.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
Kliknutím na tlačítko **obnovit** potvrďte, že se heslo resetoval.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>Vytvoření webové aplikace v ASP.NET

Začněte instalací a spuštěním sady [Visual Studio 2017](https://visualstudio.microsoft.com/).

1. Vytvořte nový webový projekt v ASP.NET a vyberte šablonu MVC. Webové formuláře také podporují ASP.NET Identity, takže můžete postupovat podle podobných kroků v aplikaci webových formulářů.
2. Změňte ověřování na **jednotlivé uživatelské účty**.
3. Spusťte aplikaci, vyberte odkaz **zaregistrovat** a zaregistrujte uživatele. V tomto okamžiku je jediným ověřením e-mailu atribut [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) .
4. V Průzkumník serveru přejděte na **Connections\DefaultConnection\Tables\AspNetUsers dat**, klikněte pravým tlačítkem myši a vyberte **Otevřít definici tabulky**.

    Následující obrázek ukazuje `AspNetUsers` schéma:

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. Klikněte pravým tlačítkem myši na tabulku **AspNetUsers** a vyberte možnost **Zobrazit data tabulky**.  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   V tomto okamžiku nebyl e-mail potvrzen.

Výchozí úložiště dat pro ASP.NET Identity je Entity Framework, ale můžete ho nakonfigurovat tak, aby používalo jiné úložiště dat, a přidat další pole. Další informace najdete v části [Další materiály](#addRes) na konci tohoto kurzu.

[Třída Owin Startup](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( *Startup.cs* ) se volá při spuštění aplikace a vyvolá metodu `ConfigureAuth` v *App\_START\STARTUP.auth.cs*, která konfiguruje kanál Owin a inicializuje ASP.NET identity. Projděte si metodu `ConfigureAuth`. Každé volání `CreatePerOwinContext` zaregistruje zpětné volání (uložené v `OwinContext`), které se bude volat jednou za požadavek na vytvoření instance zadaného typu. Můžete nastavit bod přerušení v konstruktoru a metodu `Create` každého typu (`ApplicationDbContext, ApplicationUserManager`) a ověřit, že jsou volány na každém požadavku. Instance `ApplicationDbContext` a `ApplicationUserManager` je uložena v kontextu OWIN, který lze použít v celé aplikaci. ASP.NET Identity do kanálu OWIN prostřednictvím middleware souboru cookie. Další informace najdete v tématu [Správa životního cyklu požadavků pro třídu UserManager v ASP.NET identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).

Když změníte profil zabezpečení, vygeneruje se nové bezpečnostní razítko, které se uloží do pole `SecurityStamp` tabulky *AspNetUsers* . Poznámka: pole `SecurityStamp` se liší od souboru cookie zabezpečení. Soubor cookie zabezpečení není uložený v `AspNetUsers` tabulce (nebo nikde jinde v databázi identity). Token cookie zabezpečení je podepsaný svým držitelem pomocí [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) a vytvoří se s informacemi o `UserId, SecurityStamp` a času vypršení platnosti.

Middleware souboru cookie kontroluje soubory cookie u jednotlivých požadavků. Metoda `SecurityStampValidator` ve třídě `Startup` narazí na databázi a pravidelně kontroluje razítko zabezpečení, jak je uvedeno v `validateInterval`. K této situaci dochází pouze každých 30 minut (v naší ukázce), pokud neměníte profil zabezpečení. Interval 30 minut byl zvolen pro minimalizaci cest k databázi. Další podrobnosti najdete v tomto [kurzu pro dvoustupňové ověřování](index.md) .

Pro komentáře v kódu `UseCookieAuthentication` metoda podporuje ověřování souborem cookie. Pole `SecurityStamp` a související kód poskytují do aplikace další vrstvu zabezpečení, při změně hesla se odhlásíte z prohlížeče, ve kterém jste se přihlásili. Metoda `SecurityStampValidator.OnValidateIdentity` umožňuje aplikaci ověřit token zabezpečení při přihlášení uživatele, který se používá při změně hesla nebo použití externího přihlášení. To je nutné k tomu, aby bylo zajištěno, že všechny tokeny (soubory cookie) vygenerované se starým heslem jsou neověřené. Pokud v ukázkovém projektu změníte heslo uživatele, bude pro uživatele vygenerován nový token, všechny předchozí tokeny jsou neověřeny a pole `SecurityStamp` bude aktualizováno.

Systém identit vám umožní nakonfigurovat aplikaci, takže když se změní profil zabezpečení uživatelů (například když uživatel změní heslo nebo se změní přidružené přihlašovací údaje (například z Facebooku, Google, účet Microsoft atd.), uživatel se odhlásí ze všech. instance prohlížeče. Následující obrázek ukazuje například [ukázkovou aplikaci jednotného přihlašování](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) , která umožňuje uživateli odhlásit se ze všech instancí prohlížeče (v tomto případě IE, Firefox a Chrome) tím, že vybere jedno tlačítko. Alternativně vám ukázka umožňuje odhlásit se z konkrétní instance prohlížeče.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[Ukázková aplikace jednotného přihlašování](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) ukazuje, jak ASP.NET identity umožňuje znovu vygenerovat token zabezpečení. To je nutné k tomu, aby bylo zajištěno, že všechny tokeny (soubory cookie) vygenerované se starým heslem jsou neověřené. Tato funkce poskytuje další vrstvu zabezpečení pro vaši aplikaci. Když změníte heslo, budete odhlášeni, kam jste se přihlásili k této aplikaci.

Soubor *App\_Start\IdentityConfig.cs* obsahuje třídy `ApplicationUserManager`, `EmailService` a `SmsService`. Třídy `EmailService` a `SmsService` implementují rozhraní `IIdentityMessageService`, takže máte v každé třídě k dispozici společné metody konfigurace e-mailu a SMS. I když tento kurz ukazuje, jak přidat e-mailové oznámení prostřednictvím [SendGrid](http://sendgrid.com/), můžete posílat e-maily pomocí protokolu SMTP a dalších mechanismů.

Třída `Startup` také obsahuje kotlovou desku pro přidání sociálních přihlášení (Facebook, Twitter atd.). Další informace najdete v tématu můj kurz [MVC 5 s aplikací Facebook, Twitter, LinkedIn a Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) .

Projděte si třídu `ApplicationUserManager`, která obsahuje informace o identitě uživatelů, a nakonfiguruje následující funkce:

- Požadavky na sílu hesla.
- Uzamčení uživatele (počet pokusů a čas).
- Dvojúrovňové ověřování (2FA). Projdeme 2FA a SMS v jiném kurzu.
- Zapojení e-mailu a služeb SMS. (SMS se zobrazí v jiném kurzu).

Třída `ApplicationUserManager` je odvozena z obecné `UserManager<ApplicationUser>` třídy. `ApplicationUser` jsou odvozeny z [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx). `IdentityUser` je odvozen z obecné `IdentityUser` třídy:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

Výše uvedené vlastnosti se shodují s vlastnostmi v tabulce `AspNetUsers`, která je uvedená výše.

Obecné argumenty na `IUser` umožňují odvození třídy pomocí různých typů pro primární klíč. Podívejte se na ukázku [ChangePK](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) , která ukazuje, jak změnit primární klíč z řetězce na int nebo GUID.

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`) je definována v *Models\IdentityModels.cs* jako:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

Zvýrazněný kód výše generuje [hodnota ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx). Ověřování souborů cookie ASP.NET Identity a OWIN jsou založené na deklaracích, proto rozhraní vyžaduje, aby aplikace vygenerovala `ClaimsIdentity` pro uživatele. `ClaimsIdentity` obsahuje informace o všech deklaracích uživatele, jako je jméno uživatele, věk a jaké role uživatel patří. V této fázi můžete také přidat další deklarace identity pro uživatele.

Metoda OWIN `AuthenticationManager.SignIn` projde do `ClaimsIdentity` a přihlásí uživatele:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[Aplikace MVC 5 s přihlašováním na Facebooku, Twitter, LinkedIn a Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) ukazuje, jak můžete přidat další vlastnosti do třídy `ApplicationUser`.

## <a name="email-confirmation"></a>Potvrzení e-mailu

Je vhodné potvrdit e-mailem novou registraci uživatele s cílem ověřit, že nezosobňuje někoho jiného (tj. není zaregistrován v e-mailu někoho jiného). Předpokládejme, že máte diskuzní fórum, chcete zabránit `"bob@example.com"` registraci jako `"joe@contoso.com"`. Bez potvrzení e-mailu `"joe@contoso.com"` možné z vaší aplikace získat nechtěný e-mail. Předpokládejme, že se Bob omylem zaregistrovali jako `"bib@example.com"` a jste si ho všimli, takže by nebylo možné použít obnovení hesla, protože aplikace nemá správný e-mail. Potvrzení e-mailu poskytuje jenom omezené zabezpečení z roboty a neposkytuje ochranu proti stanoveným odesilatelům nevyžádané pošty. má spoustu pracovních e-mailových aliasů, které můžou použít k registraci. V níže uvedené ukázce nebude uživatel moci změnit heslo, dokud nebude potvrzen jejich účet (při výběru potvrzovacího odkazu přijatého na e-mailovém účtu, ve kterém se zaregistrovali). Tento pracovní postup můžete použít i na jiné scénáře, například odeslat odkaz pro potvrzení a resetování hesla u nových účtů vytvořených správcem a odeslání uživatele e-mailem, když změnil svůj profil a tak dále. Obecně je vhodné zabránit novým uživatelům v posílání dat na web před potvrzením e-mailu, textové zprávy SMS nebo jiného mechanismu. <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>Sestavení ucelenější ukázky

V této části použijete NuGet ke stažení ucelené ukázky, se kterou budeme pracovat.

1. Vytvořte nový ***prázdný*** webový projekt v ASP.NET.
2. V konzole správce balíčků zadejte následující příkazy: 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   V tomto kurzu použijeme [SendGrid](http://sendgrid.com/) k odeslání e-mailu. Balíček `Identity.Samples` nainstaluje kód, se kterým budeme pracovat.
3. Nastavte [projekt na použití SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
4. Otestujte vytváření místních účtů spuštěním aplikace, výběrem odkazu **registrace** a odesláním registračního formuláře.
5. Vyberte ukázkový emailový odkaz, který simuluje e-mailové potvrzení.
6. Z ukázky odeberte potvrzovací kód e-mailového odkazu (kód `ViewBag.Link` v řadiči účtů. Podívejte se na metody akcí `DisplayEmail` a `ForgotPasswordConfirmation` a zobrazení Razor).

> [!WARNING]
> Pokud změníte kterékoli nastavení zabezpečení v této ukázce, budou se v aplikacích výroby muset projít auditem zabezpečení, který explicitně volá provedené změny.

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>Projděte si kód v App\_Start\IdentityConfig.cs

Ukázka ukazuje, jak vytvořit účet a přidat ho do role *správce* . E-mail v ukázce byste měli nahradit e-mailem, který budete používat pro účet správce. Nejjednodušší způsob, jak teď vytvořit účet správce, je programově v metodě `Seed`. Doufáme, že budete mít nástroj v budoucnu, který vám umožní vytvářet a spravovat uživatele a role. Vzorový kód vám umožní vytvářet a spravovat uživatele a role, ale musíte nejdřív mít účet správce, aby bylo možné spouštět role a stránky pro správu uživatelů. V této ukázce se při osazení databáze vytvoří účet správce.

Změňte heslo a změňte název na účet, na který můžete dostávat e-mailová oznámení.

> [!WARNING]
> Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu.

Jak bylo zmíněno dříve, `app.CreatePerOwinContext` volání ve spouštěcí třídě přidává zpětná volání do metody `Create` třídy App DB Content, User Manager a správce rolí. Kanál OWIN volá metodu `Create` na těchto třídách pro každý požadavek a ukládá kontext pro každou třídu. Řadič účtu zpřístupňuje Správce uživatelů z kontextu HTTP (který obsahuje kontext OWIN):

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

Když uživatel zaregistruje místní účet, zavolá se `HTTP Post Register` metoda:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

Výše uvedený kód používá modelová data k vytvoření nového uživatelského účtu pomocí zadaného e-mailu a hesla. Pokud je e-mailový alias v úložišti dat, vytvoření účtu se nezdařilo a formulář se zobrazí znovu. Metoda `GenerateEmailConfirmationTokenAsync` vytvoří zabezpečený potvrzovací token a uloží ho do úložiště dat ASP.NET Identity. Metoda [URL. Action](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx) vytvoří odkaz obsahující `UserId` a potvrzovací token. Tento odkaz se pak odešle e-mailem uživateli, uživatel může vybrat odkaz v e-mailové aplikaci a potvrdit jeho účet.

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>Nastavení potvrzení e-mailu

Přejdete na [stránku registrace Azure SendGrid](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) a zaregistrujete si bezplatný účet. Pro konfiguraci SendGrid přidejte kód podobný následujícímu:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> E-mailové klienty často akceptují jenom textové zprávy (žádný HTML). Tuto zprávu byste měli zadat v textu a ve formátu HTML. V ukázce SendGrid se to provádí pomocí `myMessage.Text` a `myMessage.Html`ho kódu uvedeného výše.

Následující kód ukazuje, jak odeslat e-mail pomocí třídy [MailMessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) , kde `message.Body` vrátí pouze odkaz.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu. Účet a přihlašovací údaje jsou uložené v appSetting. V Azure můžete tyto hodnoty bezpečně uložit na kartě **[Konfigurace](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** v Azure Portal. Podívejte [se na osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).

Zadejte svoje přihlašovací údaje pro SendGrid, spusťte aplikaci, zaregistrujte si e-mailový alias. můžete vybrat odkaz potvrdit v e-mailu. Pokud se chcete podívat, jak to provést pomocí e-mailového účtu [Outlook.com](http://outlook.com) , přečtěte si téma [ C# konfigurace protokolu SMTP pro Outlook.com hostitele SMTP](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) a jeho[ASP.NET identity 2,0: nastavení ověření účtu a příspěvků se dvěma faktory autorizace](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) .

Jakmile uživatel vybere tlačítko **zaregistrovat** , pošle se na svou e-mailovou adresu potvrzovací e-mail obsahující ověřovací token.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

Uživateli se pošle e-mail s potvrzovacím tokenem pro svůj účet.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>Kontrola kódu

Následující kód ukazuje metodu `POST ForgotPassword`.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

Metoda se nezdařila v tichém režimu, pokud nebyl potvrzen e-mail uživatele. Pokud byla chyba publikována pro neplatnou e-mailovou adresu, mohou uživatelé se zlými úmysly pomocí těchto informací najít platné ID uživatele (e-mailové aliasy),

Následující kód ukazuje metodu `ConfirmEmail` v řadiči účtu, který se volá, když uživatel vybere odkaz na potvrzení v e-mailu, který jim byl odeslán:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

Po použití zapomenutého tokenu hesla se zruší jeho platnost. Následující změna kódu v metodě `Create` (v souboru *App\_Start\IdentityConfig.cs* ) nastaví vypršení platnosti tokenů za 3 hodiny.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

S výše uvedeným kódem vyprší platnost zapomenutého hesla a potvrzovacích tokenů pro e-mail za 3 hodiny. Výchozí `TokenLifespan` je jeden den.

Následující kód ukazuje metodu potvrzení e-mailu:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 Aby byla aplikace bezpečnější, ASP.NET Identity podporuje dvojúrovňové ověřování (2FA). Viz [ASP.NET Identity 2,0: nastavení ověřování účtu a dvojúrovňové autorizace](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) pomocí Jan atten. I když můžete nastavit uzamčení účtu při neúspěchu při pokusu o přihlášení k přihlašovacím údajům, bude se vaše přihlášení nahlížet na uzamčení [systému DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) . Uzamčení účtu doporučujeme používat jenom s 2FA.  
<a id="addRes"></a>

## <a name="additional-resources"></a>Další zdroje

- [Přehled poskytovatelů vlastního úložiště pro ASP.NET Identity](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Aplikace MVC 5 s přihlašováním na Facebooku, Twitter, LinkedIn a Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) také ukazuje, jak přidat informace o profilu do tabulky uživatelů.
- [ASP.NET MVC a identita 2,0: Seznámení se základy](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) pomocí Jan atten.
- [Úvod do ASP.NET Identity](../getting-started/introduction-to-aspnet-identity.md)
- [Oznamujeme RTM ASP.NET identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) podle Pranav Rastogi předvádí.
