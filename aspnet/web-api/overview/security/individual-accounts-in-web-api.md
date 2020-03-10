---
uid: web-api/overview/security/individual-accounts-in-web-api
title: Zabezpečení webového rozhraní API pomocí individuálních účtů a místního přihlášení v ASP.NET Web API 2,2 | Microsoft Docs
author: MikeWasson
description: V tomto tématu se dozvíte, jak zabezpečit webové rozhraní API pomocí OAuth2 k ověřování vůči databázi členství. Verze softwaru používané v kurzu Visual Studio 201...
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555193"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a>Zabezpečení webového rozhraní API pomocí individuálních účtů a místního přihlášení v ASP.NET Web API 2,2

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout ukázkovou aplikaci](https://github.com/MikeWasson/LocalAccountsApp)

> V tomto tématu se dozvíte, jak zabezpečit webové rozhraní API pomocí OAuth2 k ověřování vůči databázi členství.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - [Visual Studio 2013 Update 3](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [Webové rozhraní API 2,2](../releases/whats-new-in-aspnet-web-api-22.md)
> - [ASP.NET Identity 2,1](../../../identity/index.md)

V Visual Studio 2013 šablona projektu webového rozhraní API nabízí tři možnosti ověřování:

- **Jednotlivé účty.** Aplikace používá databázi členství.
- **Účty organizace.** Uživatelé se přihlásí pomocí svých Azure Active Directory, Office 365 nebo místních přihlašovacích údajů služby Active Directory.
- **Ověřování systému Windows.** Tato možnost je určená pro intranetové aplikace a používá modul služby IIS pro ověřování systému Windows.

Další podrobnosti o těchto možnostech naleznete v tématu [Creating ASP.NET Web Projects in Visual Studio 2013](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth).

Jednotlivé účty poskytují uživateli dva způsoby přihlášení:

- **Místní přihlášení**. Uživatel se registruje v lokalitě a zadá uživatelské jméno a heslo. Aplikace ukládá hodnotu hash hesla do databáze členství. Když se uživatel přihlásí, systém ASP.NET Identity ověří heslo.
- **Sociální přihlášení**. Uživatel se přihlásí pomocí externí služby, jako je Facebook, Microsoft nebo Google. Aplikace stále vytvoří položku pro uživatele v databázi členství, ale neuloží žádné přihlašovací údaje. Uživatel se ověří tak, že se přihlásí k externí službě.

Tento článek se dohlíží na scénář místního přihlášení. Pro místní i sociální přihlášení používá webové rozhraní API OAuth2 k ověřování požadavků. Toky přihlašovacích údajů se ale liší pro místní a sociální přihlášení.

V tomto článku ukážeme jednoduchou aplikaci, která umožňuje uživateli přihlásit se a odesílat ověřená volání AJAX do webového rozhraní API. Vzorový kód si můžete stáhnout [tady](https://github.com/MikeWasson/LocalAccountsApp). Tento soubor Readme popisuje, jak vytvořit ukázku od začátku v aplikaci Visual Studio.

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

Ukázková aplikace používá pro odesílání požadavků AJAX vyseknutí. js pro datové vazby a jQuery. Zaměřím se na volání AJAX, takže nemusíte znát vyseknutí. js pro tento článek.

V takovém případě popíšeme:

- Co aplikace dělá na straně klienta.
- Co se děje na serveru.
- Provoz HTTP uprostřed.

Nejdřív musíme definovat několik OAuth2 terminologie.

- *Prostředek*. Některá data, která lze chránit.
- *Server prostředků*. Server, který je hostitelem prostředku.
- *Vlastník prostředku*. Entita, která může udělit oprávnění pro přístup k prostředku. (Obvykle uživatel.)
- *Klient*: aplikace, která chce získat přístup k prostředku. V tomto článku je klient webovým prohlížečem.
- *Přístupový token* Token, který uděluje přístup k prostředku.
- *Nosný token* Konkrétní typ přístupového tokenu s vlastností, kterou může kdokoli použít k použití tokenu. Jinými slovy, klient pro použití nosných tokenů nevyžaduje kryptografický klíč ani jiný tajný klíč. Z tohoto důvodu by se měly tokeny nosiče použít jenom přes HTTPS a měly by mít poměrně krátké časy vypršení platnosti.
- *Autorizační Server*. Server, který poskytuje přístupové tokeny.

Aplikace může fungovat jako autorizační Server a server prostředků. Šablona projektu webového rozhraní API se řídí tímto modelem.

## <a name="local-login-credential-flow"></a>Tok místních přihlašovacích přihlašovacích údajů

Pro místní přihlášení používá webové rozhraní API [tok hesla vlastníka prostředku](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) definovaný v OAuth2.

1. Uživatel zadá do klienta jméno a heslo.
2. Klient odešle tyto přihlašovací údaje na autorizační Server.
3. Autorizační Server ověří přihlašovací údaje a vrátí přístupový token.
4. Pro přístup k chráněnému prostředku klient zahrne přístupový token do autorizační hlavičky žádosti HTTP.

![](individual-accounts-in-web-api/_static/image3.png)

Když v šabloně projektu webového rozhraní API vyberete **jednotlivé účty** , projekt zahrnuje autorizační Server, který ověřuje přihlašovací údaje uživatele a tokeny problémů. Následující diagram znázorňuje stejný tok přihlašovacích údajů v souvislosti s komponentami webového rozhraní API.

![](individual-accounts-in-web-api/_static/image4.png)

V tomto scénáři fungují řadiče webového rozhraní API jako servery prostředků. Filtr ověřování ověřuje přístupové tokeny a používá atribut **[autorizovat]** k ochraně prostředku. Pokud má kontroler nebo akce atribut **[autorizovat]** , musí být všechny požadavky na tento kontroler nebo akce ověřeny. V opačném případě se autorizace odepře a webové rozhraní API vrátí chybu 401 (Neautorizováno).

Autorizační Server a filtr ověřování navolají do komponenty [middleware Owin](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) , která zpracovává podrobnosti o OAuth2. Tento návrh popíšeme podrobněji dále v tomto kurzu.

## <a name="sending-an-unauthorized-request"></a>Posílá se neautorizovaný požadavek.

Začněte tím, že aplikaci spustíte a kliknete na tlačítko **rozhraní API pro volání** . Po dokončení žádosti by se měla v poli **výsledek** zobrazit chybová zpráva. Důvodem je, že požadavek neobsahuje přístupový token, takže požadavek je neautorizovaný.

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

Tlačítko **rozhraní API volání** ODEŠLE požadavek AJAX na ~/API/Values, který vyvolá akci kontroleru webového rozhraní API. Zde je oddíl kódu JavaScriptu, který odesílá požadavek AJAX. V ukázkové aplikaci je veškerý kód aplikace JavaScriptu umístěný v souboru Scripts\app.js.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

Až se uživatel přihlásí, neexistuje žádný nosný token, takže v žádosti nebude žádná autorizační hlavička. To způsobí, že požadavek vrátí chybu 401.

Zde je požadavek HTTP. (Používám [Fiddler](http://www.telerik.com/fiddler) k zachycení provozu protokolu HTTP.)

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

Odpověď HTTP:

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

Všimněte si, že odpověď obsahuje hlavičku WWW-Authenticate s výzvou nastavenou na nosiče. To znamená, že server očekává nosný token.

## <a name="register-a-user"></a>Registrace uživatele

V části **registrace** aplikace zadejte e-mail a heslo a klikněte na tlačítko **Registrovat** .

Pro tuto ukázku nemusíte používat platnou e-mailovou adresu, ale skutečná aplikace tuto adresu potvrzuje. (Podívejte se na téma [Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu a resetováním hesla](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) Pro heslo použijte něco jako "Heslo1!", s velkým písmenem, malým písmenem, číslicí a nealfanumerickým znakem. Aby aplikace zůstala jednoduchá, jsem opustili ověřování na straně klienta, takže pokud dojde k potížím s formátem hesla, zobrazí se chyba 400 (chybná žádost).

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

Tlačítko **zaregistrovat** ODEŠLE požadavek post na ~/API/Account/Register/.. Tělo žádosti je objekt JSON, který obsahuje jméno a heslo. Zde je kód JavaScriptu, který odesílá požadavek:

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

Požadavek HTTP:

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

Odpověď HTTP:

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

Tato žádost je zpracována třídou `AccountController`. Interně `AccountController` používá ASP.NET Identity ke správě databáze členství.

Pokud aplikaci spouštíte místně ze sady Visual Studio, uživatelské účty jsou uloženy v LocalDB v tabulce AspNetUsers. Chcete-li zobrazit tabulky v aplikaci Visual Studio, klikněte na nabídku **zobrazení** , vyberte možnost **Průzkumník serveru**a poté rozbalte položku **datová připojení**.

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a>Získání přístupového tokenu

Zatím jsme neudělali žádné OAuth, ale teď se zobrazí autorizační Server OAuth v akci, když požádáme o přístupový token. V oblasti **přihlášení** ukázkové aplikace zadejte e-mail a heslo a klikněte na **Přihlásit**se.

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

Tlačítko pro **přihlášení** odešle požadavek na koncový bod tokenu. Tělo požadavku obsahuje následující data zakódovaná ve formátu adresy URL:

- udělit\_typ: heslo
- uživatelské jméno: &lt;e-mailu uživatele&gt;
- heslo: &lt;hesla&gt;

Zde je kód JavaScriptu, který odesílá požadavek AJAX:

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

Pokud je požadavek úspěšný, autorizační server vrátí přístupový token v těle odpovědi. Všimněte si, že do úložiště relace ukládáme token, který použijeme později při odesílání požadavků do rozhraní API. Na rozdíl od některých forem ověřování (například ověřování na základě souborů cookie) nebude prohlížeč automaticky zahrnovat přístupový token do následujících požadavků. Aplikace musí to provést explicitně. To je dobré, protože omezuje [CSRF ohrožení zabezpečení](preventing-cross-site-request-forgery-csrf-attacks.md).

Požadavek HTTP:

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

Uvidíte, že požadavek obsahuje přihlašovací údaje uživatele. K zajištění zabezpečení transportní vrstvy je *nutné* použít https.

Odpověď HTTP:

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

Z důvodu čitelnosti jsme kód JSON odsadí a zkrátili jste přístupový token, který je poměrně dlouhý.

Vlastnosti `access_token`, `token_type`a `expires_in` jsou definovány specifikací OAuth2. Ostatní vlastnosti (`userName`, `.issued`a `.expires`) jsou pouze pro informativní účely. Můžete najít kód, který přidá tyto další vlastnosti v metodě `TokenEndpoint` v souboru/Providers/ApplicationOAuthProvider.cs.

## <a name="send-an-authenticated-request"></a>Odeslat ověřený požadavek

Teď, když máme nosný token, můžeme do rozhraní API vytvořit ověřený požadavek. To se provádí nastavením autorizační hlavičky v žádosti. Pokud to chcete zobrazit, klikněte znovu na tlačítko **zavolat rozhraní API** .

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

Požadavek HTTP:

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

Odpověď HTTP:

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a>Odhlásit se

Vzhledem k tomu, že prohlížeč neukládá do mezipaměti přihlašovací údaje ani přístupový token, odhlášení je prostě "forgetting" tokenu, protože ho odebíráme z úložiště relace:

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a>Porozumění šabloně projektu jednotlivých účtů

Když v šabloně projektu webové aplikace ASP.NET vyberete **jednotlivé účty** , projekt zahrnuje:

- OAuth2 autorizační Server.
- Koncový bod webového rozhraní API pro správu uživatelských účtů
- Model EF pro ukládání uživatelských účtů.

Tady jsou hlavní třídy aplikace, které implementují tyto funkce:

- `AccountController`. Poskytuje koncový bod webového rozhraní API pro správu uživatelských účtů. Akce `Register` je jediná ta, kterou jsme použili v tomto kurzu. Další metody pro třídu podporují resetování hesla, sociální přihlášení a další funkce.
- `ApplicationUser`definované v/Models/IdentityModels.cs. Tato třída je model EF pro uživatelské účty v databázi členství.
- `ApplicationUserManager`definovaná v/App\_Start/IdentityConfig. cs Tato třída je odvozená od [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) a provádí operace s uživatelskými účty, jako je například vytvoření nového uživatele, ověřování hesel a tak dále a automaticky ukládá změny v databázi.
- `ApplicationOAuthProvider`. Tento objekt se připojí k middlewaru OWIN a zpracovává události vyvolané middlewarem. Je odvozen z [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx).

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a>Konfigurace autorizačního serveru

V StartupAuth.cs následující kód konfiguruje autorizační Server OAuth2.

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

Vlastnost `TokenEndpointPath` je cesta URL ke koncovému bodu autorizačního serveru. To je adresa URL, kterou aplikace používá k získání nosných tokenů.

Vlastnost `Provider` Určuje zprostředkovatele, který se připojí k middlewaru OWIN a zpracovává události, které middleware vyvolala.

Toto je základní tok, když chce aplikace získat token:

1. K získání přístupového tokenu aplikace pošle požadavek na ~/token.
2. Volání middlewaru OAuth `GrantResourceOwnerCredentials` na poskytovateli.
3. Zprostředkovatel zavolá `ApplicationUserManager`, aby ověřil přihlašovací údaje a vytvořila identitu deklarací identity.
4. V případě úspěchu vytvoří poskytovatel ověřovací lístek, který slouží ke generování tokenu.

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

Middleware OAuth neví o uživatelských účtech žádné informace. Zprostředkovatel komunikuje mezi middlewarem a ASP.NET Identity. Další informace o implementaci autorizačního serveru najdete v tématu [Owin OAuth 2,0 Authorization Server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md).

### <a name="configuring-web-api-to-use-bearer-tokens"></a>Konfigurace webového rozhraní API pro použití nosných tokenů

V metodě `WebApiConfig.Register` následující kód nastaví ověřování pro kanál webového rozhraní API:

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

Třída **HostAuthenticationFilter** umožňuje ověřování pomocí nosných tokenů.

Metoda **SuppressDefaultHostAuthentication** oznamuje webovému rozhraní API, že bude ignorovat jakékoli ověřování, ke kterému dojde předtím, než požadavek dosáhne kanálu webového rozhraní API, a to buď prostřednictvím služby IIS, nebo middleware Owin. Tímto způsobem můžeme omezit webové rozhraní API tak, aby se ověřilo jenom pomocí nosných tokenů.

> [!NOTE]
> Zejména část MVC vaší aplikace může používat ověřování pomocí formulářů, které ukládá přihlašovací údaje do souboru cookie. Ověřování na základě souborů cookie vyžaduje použití tokenů ochrany proti padělání, aby se zabránilo útokům CSRF. To je problém pro webová rozhraní API, protože neexistuje pohodlný způsob, jak webové rozhraní API odeslat token proti padělání klientovi. (Další informace o tomto problému najdete v tématu [prevence útoků CSRF ve webovém rozhraní API](preventing-cross-site-request-forgery-csrf-attacks.md).) Volání **SuppressDefaultHostAuthentication** zajistí, že webové rozhraní API není zranitelné vůči útokům CSRF z přihlašovacích údajů uložených v souborech cookie.

V případě, že klient požaduje chráněný prostředek, je zde postup v kanálu webového rozhraní API:

1. Filtr **HostAuthentication** volá middleware OAuth pro ověření tokenu.
2. Middleware převede token na identitu deklarací identity.
3. V tomto okamžiku je požadavek *ověřený* , ale není *autorizovaný*.
4. Ověřovací filtr prověřuje identitu deklarací identity. Pokud deklarace identity opravňuje uživatele k tomuto prostředku, je žádost autorizována. Ve výchozím nastavení bude mít atribut **[autorizační]** autorizaci všech požadavků, které jsou ověřeny. Můžete je ale autorizovat podle role nebo jiných deklarací identity. Další informace najdete v tématu [ověřování a autorizace ve webovém rozhraní API](authentication-and-authorization-in-aspnet-web-api.md).
5. Pokud jsou předchozí kroky úspěšné, kontroler vrátí chráněný prostředek. V opačném případě klient obdrží chybu 401 (Neautorizováno).

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a>Další prostředky

- [ASP.NET Identity](../../../identity/index.md)
- [Principy funkcí zabezpečení v ŠABLONĚ Spa pro VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx). Blogový příspěvek MSDN od společnosti Hongye Sun.
- [Neprotínají se šablony jednotlivých účtů webového rozhraní API – část 2: místní účty](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/). Příspěvek na blogu od Dominick Baier.
- [Ověřování hostitele a webové rozhraní API pomocí Owin](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/). Dobré vysvětlení `SuppressDefaultHostAuthentication` a `HostAuthenticationFilter` od Brock Allen.
- [Přizpůsobení informací o profilu v ASP.NET identity v šablonách VS 2013](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx). Příspěvek na blogu MSDN od Pranav Rastogi předvádí.
- [Za správu životnosti žádosti pro třídu UserManager v ASP.NET identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx). Příspěvek na blogu MSDN od Suhas Joshi s dobrým vysvětlením `UserManager` třídy.
