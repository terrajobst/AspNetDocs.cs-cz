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
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a>Dvojúrovňové ověřování pomocí SMS a e-mailu s ASP.NET Identity

[Hao Kung](https://github.com/HaoK), [Pranav Rastogi předvádí](https://github.com/rustd), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Suhas Joshi](https://github.com/suhasj)

> V tomto kurzu se dozvíte, jak nastavit dvojúrovňové ověřování (2FA) pomocí SMS a e-mailu.
> 
> Tento článek napsal Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav rastogi předvádí ([@rustd](https://twitter.com/rustd)), Hao Kung a Suhas Joshi. Vzorek NuGet byl napsán hlavně pomocí Hao Kung.

Toto téma obsahuje následující témata:

- [Sestavení ukázky identity](#build)
- [Nastavení SMS pro dvojúrovňové ověřování](#SMS)
- [Povolit dvojúrovňové ověřování](#enable2)
- [Jak zaregistrovat poskytovatele dvou faktorů ověřování](#reg)
- [Kombinování sociálních a místních přihlašovacích účtů](#combine)
- [Uzamčení účtu před útoky hrubou silou](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>Sestavení ukázky identity

V této části použijete NuGet ke stažení ukázky, se kterou budeme pracovat. Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Nainstalujte Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) nebo novější.

> [!NOTE]
> Upozornění: k dokončení tohoto kurzu je nutné nainstalovat aktualizaci Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) .

1. Vytvořte nový ***prázdný*** webový projekt v ASP.NET.
2. V konzole správce balíčků zadejte následující příkazy:  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   V tomto kurzu použijeme [SendGrid](http://sendgrid.com/) k posílání e-mailů a [Twilio](https://www.twilio.com/) nebo [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) pro text SMS. Balíček `Identity.Samples` nainstaluje kód, se kterým budeme pracovat.
3. Nastavte [projekt na použití SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
4. *Volitelné*: postupujte podle pokynů v [kurzu e-mailové potvrzení](account-confirmation-and-password-recovery-with-aspnet-identity.md) , abyste připojili SendGrid a pak spustili aplikaci a zaregistrovali e-mailový účet.
5. *Volitelné:* Z ukázky odeberte potvrzovací kód e-mailového odkazu (kód `ViewBag.Link` v řadiči účtů. Podívejte se na metody akcí `DisplayEmail` a `ForgotPasswordConfirmation` a zobrazení Razor).
6. *Volitelné:* Odeberte kód `ViewBag.Status` z řadičů pro správu a účtů a ze zobrazení *Views\Account\VerifyCode.cshtml* a *Views\Manage\VerifyPhoneNumber.cshtml* Razor. Alternativně můžete `ViewBag.Status` zobrazení, abyste otestovali, jak tato aplikace funguje lokálně, aniž byste museli zapojovat a odesílat e-maily a zprávy SMS.

> [!NOTE]
> Upozornění: Pokud v této ukázce změníte některá z nastavení zabezpečení, budou se v aplikacích výroby muset projít auditem zabezpečení, který explicitně volá provedené změny.

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
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   Adresáře  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   Obor názvů:  
    `ASPSMSX2`
3. **Zjišťování přihlašovacích údajů uživatele poskytovatele služby SMS**  
  
   Twilio  
   Na kartě **řídicí panel** účtu Twilio zkopírujte **identifikátor SID účtu** a **ověřovací token**.  
  
   ASPSMS:  
   V nastavení účtu přejděte na **vlastnosti UserKey** a zkopírujte je společně s vaším vlastním **heslem**.  
  
   Později budou tyto hodnoty uloženy v proměnných `SMSAccountIdentification` a `SMSAccountPassword`.
4. **Zadání SenderID/původce**  
  
   Twilio  
   Na kartě **čísla** zkopírujte své Twilio telefonní číslo.  
  
   ASPSMS:  
   V nabídce **odemknout původci** odemkněte jeden nebo více původců nebo vyberte alfanumerický původ (není podporován všemi sítěmi).  
  
   Tuto hodnotu uložíme později do proměnné `SMSAccountFrom`.
5. **Přenáší se přihlašovací údaje poskytovatele SMS do aplikace.**  
  
   Zpřístupnit přihlašovací údaje a telefonní číslo odesilatele k aplikaci:

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu. Účet a přihlašovací údaje se přidají do výše uvedeného kódu, aby se ukázka snadno zachovala. Viz Jan atten 's [ASP.NET MVC: zachovejte soukromé nastavení ze správy zdrojového kódu](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).
6. **Implementace přenosu dat do poskytovatele služby SMS**  
  
   Nakonfigurujte třídu `SmsService` v souboru *App\_Start\IdentityConfig.cs* .  
  
   V závislosti na použitém poskytovateli serveru SMS aktivujte **Twilio** nebo část **ASPSMS** : 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. Spusťte aplikaci a přihlaste se pomocí účtu, který jste předtím zaregistrovali.
8. Klikněte na své ID uživatele, které aktivuje metodu `Index` akce v kontroleru `Manage`.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. Klikněte na tlačítko Přidat.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. Během několika sekund obdržíte textovou zprávu s ověřovacím kódem. Zadejte ji a stiskněte **Odeslat**.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. V zobrazení Správa se zobrazí vaše telefonní číslo.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>Kontrola kódu

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

Metoda `Index` akce v kontroleru `Manage` nastavuje stavovou zprávu na základě předchozí akce a obsahuje odkazy na změnu místního hesla nebo přidání místního účtu. Metoda `Index` taky zobrazuje stav nebo telefonní číslo 2FA, externí přihlášení, 2FA povoleno a pamatuje 2FA metodu pro tento prohlížeč (vysvětlení později). Kliknutím na své ID uživatele (e-mailové adresy) v záhlaví se zpráva nepředá. Kliknutí na **telefonní číslo: odebrat** předávání odkazů `Message=RemovePhoneSuccess` jako řetězec dotazu.  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

Metoda `AddPhoneNumber` akce zobrazí dialogové okno pro zadání telefonního čísla, které může přijímat zprávy SMS.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

Kliknutím na tlačítko **Odeslat ověřovací kód** se zaúčtuje telefonní číslo do metody HTTP POST `AddPhoneNumber` Action.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

Metoda `GenerateChangePhoneNumberTokenAsync` vygeneruje token zabezpečení, který se nastaví ve zprávě SMS. Pokud je nakonfigurovaná služba SMS, token se pošle jako řetězec &quot;je váš bezpečnostní kód &lt;token&gt;&quot;. Metoda `SmsService.SendAsync` pro je volána asynchronně, pak je aplikace přesměrována na metodu `VerifyPhoneNumber` akce (která zobrazuje následující dialog), kde můžete zadat ověřovací kód.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

Jakmile zadáte kód a kliknete na Odeslat, kód se publikuje do metody HTTP POST `VerifyPhoneNumber` Action.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

Metoda `ChangePhoneNumberAsync` kontroluje vystavený bezpečnostní kód. Je-li kód správný, je telefonní číslo přidáno do pole `PhoneNumber` `AspNetUsers` tabulce. Pokud je toto volání úspěšné, je volána metoda `SignInAsync`:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

Parametr `isPersistent` nastaví, zda je relace ověřování trvala napříč několika požadavky.

Když změníte profil zabezpečení, vygeneruje se nové bezpečnostní razítko, které se uloží do pole `SecurityStamp` tabulky *AspNetUsers* . Poznámka: pole `SecurityStamp` se liší od souboru cookie zabezpečení. Soubor cookie zabezpečení není uložený v `AspNetUsers` tabulce (nebo nikde jinde v databázi identity). Token cookie zabezpečení je podepsaný svým držitelem pomocí [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) a vytvoří se s informacemi o `UserId, SecurityStamp` a času vypršení platnosti.

Middleware souboru cookie kontroluje soubory cookie u jednotlivých požadavků. Metoda `SecurityStampValidator` ve třídě `Startup` narazí na databázi a pravidelně kontroluje razítko zabezpečení, jak je uvedeno v `validateInterval`. K této situaci dochází pouze každých 30 minut (v naší ukázce), pokud neměníte profil zabezpečení. Interval 30 minut byl zvolen pro minimalizaci cest k databázi.

Metoda `SignInAsync` musí být volána, když je provedena jakákoli změna v profilu zabezpečení. Když se profil zabezpečení změní, databáze aktualizuje pole `SecurityStamp` a bez volání metody `SignInAsync` byste si měli zůstat přihlášeni *pouze* až do okamžiku, kdy kanál Owin narazí do databáze (`validateInterval`). Můžete to otestovat tak, že změníte metodu `SignInAsync` pro okamžité vrácení a nastavíte vlastnost `validateInterval` souborů cookie na 30 minut na 5 sekund:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

U výše uvedených změn kódu můžete změnit svůj profil zabezpečení (například změnou stavu **dvou faktorů povolených**) a při neúspěchu `SecurityStampValidator.OnValidateIdentity` metody se odhlásí za 5 sekund. Odeberte návratovou čáru v metodě `SignInAsync`, udělejte jinou změnu profilu zabezpečení a nebudete se odhlásit. Metoda `SignInAsync` generuje nový soubor cookie zabezpečení.

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>Povolit dvojúrovňové ověřování

V ukázkové aplikaci je nutné použít uživatelské rozhraní pro povolení dvojúrovňové ověřování (2FA). Pokud chcete povolit 2FA, na navigačním panelu klikněte na své ID uživatele (e-mailový alias).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
Klikněte na Povolit 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) Odhlaste se a pak se znovu přihlaste. Pokud jste povolili e-mail (viz můj [předchozí kurz](account-confirmation-and-password-recovery-with-aspnet-identity.md)), můžete vybrat zprávu SMS nebo E-mail pro 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) Zobrazí se stránka ověření kódu, kde můžete zadat kód (ze serveru SMS nebo e-mailu).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) Kliknutím na **Zapamatovat si tento prohlížeč** zabráníte tomu, abyste pomocí 2FA přihlásili s tímto počítačem a prohlížečem. Povolením 2FA a kliknutím na **Zapamatovat si tento prohlížeč** vám poskytne silnou 2FA ochranu od uživatelů se zlými úmysly, kteří se pokoušejí získat přístup k vašemu účtu, pokud k vašemu počítači nemají přístup. To můžete provést na jakémkoli privátním počítači, který pravidelně používáte. Nastavením možnosti **pamatovat si tento prohlížeč**získáte zvýšení zabezpečení 2FA z počítačů, které pravidelně nepoužíváte, a získáte pohodlí v tom, že nebudete moct procházet 2FA na svých počítačích. 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>Jak zaregistrovat poskytovatele dvou faktorů ověřování

Při vytváření nového projektu MVC obsahuje soubor *IdentityConfig.cs* následující kód pro registraci zprostředkovatele dvou faktorů ověřování:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>Přidat telefonní číslo pro 2FA

Metoda `AddPhoneNumber` akce v kontroleru `Manage` vygeneruje token zabezpečení a pošle ho na telefonní číslo, které jste zadali.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

Po odeslání tokenu se přesměruje na metodu `VerifyPhoneNumber` akce, kde můžete zadat kód k registraci serveru SMS pro 2FA. 2FA serveru SMS se nepoužívá, dokud neověříte telefonní číslo.

## <a name="enabling-2fa"></a>Povolení 2FA

Metoda `EnableTFA` akce povoluje 2FA:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

Všimněte si, že `SignInAsync` musí být volána, protože možnost Povolit 2FA je změnou profilu zabezpečení. Pokud je povolená možnost 2FA, bude uživatel muset použít 2FA k přihlášení s použitím 2FA přístupů, které zaregistrovali (SMS a e-mail v ukázce).

Můžete přidat další poskytovatele 2FA, jako jsou například generátory kódu QR, nebo můžete napsat vlastní (viz [používání služby Google Authenticator s ASP.NET identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).

> [!NOTE]
> Kódy 2FA se generují pomocí [algoritmu jednorázového hesla založeného na čase](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) a kódy jsou platné po dobu šesti minut. Pokud zadáte kód více než šest minut, zobrazí se chybová zpráva neplatného kódu.

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>Kombinování sociálních a místních přihlašovacích účtů

Místní a sociální účty můžete zkombinovat kliknutím na svůj e-mailový odkaz. V následující sekvenci &quot;RickAndMSFT@gmail.com&quot; nejdřív vytvořená jako místní přihlašovací jméno, ale můžete účet vytvořit jako sociální protokol a pak přidat místní přihlašovací údaje.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

Klikněte na odkaz **Správa** . Poznamenejte si externí (sociální přihlášení) přidružená k tomuto účtu.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

Klikněte na odkaz na jiný protokol služby a přijměte žádosti o aplikace. Tyto dva účty byly zkombinovány, budete se moci přihlásit pomocí obou účtů. Je možné, že budete chtít, aby uživatelé mohli přidávat místní účty v případě výpadku služby sociálního protokolu v případě nedostatku nebo pravděpodobně ztratili přístup ke svému sociálnímu účtu.

Na následujícím obrázku je to, že se jedná o sociální přihlášení (které vidíte z **externích přihlášení: 1** zobrazeno na stránce).

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

Kliknutím na **Vybrat heslo** můžete přidat místní přihlašování ke stejnému účtu.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>Uzamčení účtu před útoky hrubou silou

Můžete chránit účty ve vaší aplikaci před slovníkovými útoky tím, že povolíte uzamčení uživatele. Následující kód v metodě `ApplicationUserManager Create` konfiguruje odblokování:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

Výše uvedený kód umožňuje uzamčení pouze pro dva faktory ověřování. I když můžete povolit možnost Uzamknout pro přihlášení změnou `shouldLockout` na hodnotu true v metodě `Login` řadiče účtů, doporučujeme Nepovolit možnost Uzamknout pro přihlášení, protože účet je náchylný k útokům prostřednictvím přihlašovacích údajů pro [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) . V ukázkovém kódu je uzamčení pro účet správce vytvořené v metodě `ApplicationDbInitializer Seed` zakázané:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>Vyžaduje se, aby uživatel měl ověřený e-mailový účet.

Následující kód vyžaduje, aby uživatel měl ověřený e-mailový účet, než se může přihlásit:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>Jak SignInManager vyhledává požadavek 2FA

Místní přihlašovací protokol i protokol pro sociální sítě kontrolují, zda je povolený 2FA. Pokud je povolený 2FA, metoda přihlašování `SignInManager` vrátí `SignInStatus.RequiresVerification`a uživatel se přesměruje na metodu `SendCode` akce, kde bude muset zadat kód pro dokončení protokolu. Pokud je v místním souboru cookie uživatelů nastavená RememberMe, `SignInManager` vrátí `SignInStatus.Success` a nebude muset projít přes 2FA.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

Následující kód ukazuje metodu `SendCode` akce. [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) se vytvoří se všemi metodami 2FA povolenými pro uživatele. [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) se předává Pomocníkovi [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) , který umožňuje uživateli vybrat přístup 2FA (obvykle e-mail a SMS).

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

Jakmile uživatel odešle přístup 2FA, je volána metoda akce `HTTP POST SendCode`, `SignInManager` odešle kód 2FA a uživatel je přesměrován na metodu `VerifyCode` akce, kde může zadat kód pro dokončení přihlášení.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA uzamčení

I když můžete nastavit uzamčení účtu při neúspěchu při pokusu o přihlášení k přihlašovacím údajům, bude se vaše přihlášení nahlížet na uzamčení [systému DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) . Uzamčení účtu doporučujeme používat jenom s 2FA. Při vytvoření `ApplicationUserManager` ukázkový kód nastaví uzamčení 2FA a `MaxFailedAccessAttemptsBeforeLockout` na pět. Jakmile se uživatel přihlásí (prostřednictvím místního účtu nebo účtu na sociálních sítích), uloží se každý neúspěšný pokus na 2FA a pokud se dosáhne maximálního počtu pokusů, uživatel se zablokuje na pět minut (můžete nastavit čas uzamčení pomocí `DefaultAccountLockoutTimeSpan`).

<a id="addRes"></a>

## <a name="additional-resources"></a>Další prostředky

- [ASP.NET identity doporučené prostředky](../getting-started/aspnet-identity-recommended-resources.md) Úplný seznam blogů identity, videí, výukových kurzů a skvělých odkazů
- [Aplikace MVC 5 s přihlašováním na Facebooku, Twitter, LinkedIn a Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) také ukazuje, jak přidat informace o profilu do tabulky uživatelů.
- [ASP.NET MVC a identita 2,0: Seznámení se základy](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) pomocí Jan atten.
- [Potvrzení účtu a obnovení hesla pomocí ASP.NET Identity](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Úvod do ASP.NET Identity](../getting-started/introduction-to-aspnet-identity.md)
- [Oznamujeme RTM ASP.NET identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) podle Pranav Rastogi předvádí.
- [ASP.NET Identity 2,0: nastavení ověřování účtu a dvojúrovňové autorizace](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) pomocí Jan atten.
