---
uid: identity/overview/getting-started/aspnet-identity-recommended-resources
title: ASP.NET Identity doporučené prostředky – ASP.NET 4. x
author: Rick-Anderson
description: Toto téma obsahuje odkazy na materiály k dokumentaci týkající se použití ASP.NET Identity. Pokud znáte skvělý Blogový příspěvek, StackOverflow vlákno nebo jakékoli jiné...
ms.author: riande
ms.date: 04/09/2015
ms.assetid: 0f78aec2-f509-46fa-b20f-d5208425d8ec
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-recommended-resources
msc.type: authoredcontent
ms.openlocfilehash: 4b2a6689839f66121f4a32ee5934f6cda50ae812
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456567"
---
# <a name="aspnet-identity-recommended-resources"></a>ASP.NET Identity – doporučené zdroje informací

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> Toto téma obsahuje odkazy na materiály k dokumentaci týkající se použití ASP.NET Identity.
>
> Pokud znáte skvělý Blogový příspěvek, vlákno [StackOverflow](http://stackoverflow.com) nebo jakýkoli jiný odkaz, který by byl užitečný, [pošlete nám e-mail](mailto:aspnetue@microsoft.com?subject=Identity recommended resources) s odkazem nebo pouze ponechte zprávu v dolní části této stránky.

- [Začínáme s ASP.NET Identity](#gettingstarted)
- [Nové vybrané musí Přečtěte si články](#feat)
- [Zprostředkující ASP.NET Identity](#adv)
- [Videa](#video)
- [Kde klást otázky, vyžádat funkce, ohlásit chybu a noční sestavení](#samp)
- [Blogové příspěvky na identitě](#blog)
- [Vlastní poskytovatelé úložiště pro ASP.NET Identity](#cust)
- [Další prostředky identity](#additional)
- [Q &amp; A (otázka/odpověď)](#qand)

<a id="gettingstarted"></a>

## <a name="getting-started-with-aspnet-identity"></a>Začínáme s ASP.NET Identity

- [Aplikace MVC 5 s přihlašováním na Facebooku, Twitteru, LinkedInu a Google OAuth2](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) V tomto kurzu se dozvíte, jak napsat aplikaci ASP.NET MVC 5 s autorizací na Facebooku a Google OAuth 2. Také ukazuje, jak přidat další data do databáze identity.
- [Nasaďte zabezpečenou aplikaci ASP.NET MVC s členstvím, protokolem OAuth a SQL Database do Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Tento kurz přidá nasazení Azure, způsob zabezpečení vaší aplikace pomocí rolí, způsob použití rozhraní API pro členství v přidávání uživatelů a rolí a další funkce zabezpečení.
- [Úvod do ASP.NET Identity](introduction-to-aspnet-identity.md)
- [Vytvoření zabezpečené webové aplikace ASP.NET MVC 5 s přihlášením, potvrzením e-mailu a resetováním hesla](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)
- [Aplikace ASP.NET MVC 5 s dvoufaktorovým ověřováním pomocí SMS a e-mailu](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)

<a id="feat"></a>

## <a name="new-featured-must-read-articles"></a>Nové vybrané musí Přečtěte si články

- [Návod: ASP.NET IDENTITU MVC s ověřováním účtu Microsoft](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/) podle [Benjamin dne](http://www.benday.com/about/)
- [ASP.NET Identity 2,0 rozšíření modelů identit a používání celočíselných klíčů namísto řetězců](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
- [Ověřování tokenu AngularJS pomocí ASP.NET webového rozhraní API 2, Owin a identity](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [Thinktecture. IdentityManager jako náhrada za WSAT](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [ASP.NET Identity 2,0: přizpůsobení uživatelů a rolí](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)

<a id="adv"></a>

## <a name="intermediate-aspnet-identity"></a>Zprostředkující ASP.NET Identity

- [Potvrzení účtu a obnovení hesla pomocí ASP.NET Identity](../features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Dvoufaktorové ověřování pomocí SMS a e-mailu s ASP.NET Identity](../features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [Migrace stávajícího webu z členství SQL na ASP.NET Identity](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [Přidání ASP.NET Identity do prázdného nebo stávajícího projektu webových formulářů](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)
- Externí ověřování na webu MSDN Magazine [pomocí ASP.NET identity](https://msdn.microsoft.com/magazine/dn745860.aspx) Dino Esposito
- Časopis MSDN Magazine[první pohled na ASP.NET identity](https://msdn.microsoft.com/magazine/dn605872.aspx) podle Dino Esposito
- [ASP.NET Identity – uzamčení uživatele](http://tech.trailmax.info/2014/06/asp-net-identity-user-lockout/)

<a id="samp"></a>

## <a name="where-to-ask-questions-request-features-report-a-bug-and-nightly-builds"></a>Kde klást otázky, vyžádat funkce, ohlásit chybu a noční sestavení

- Pro StackOverflow použijte značku [ASPNET-identity](http://stackoverflow.com/questions/tagged/asp.net-identity)
- Pro fóra ASP.NETy příspěvek do [fóra zabezpečení](https://forums.asp.net/25.aspx) a přidejte **ASP.NET identity** k názvu.
- [ASP.NET identity na GitHubu](https://github.com/aspnet/AspNetIdentity) Získejte noční buildy, vyžádejte si funkce a otevřete chyby.

<a id="blog"></a>

## <a name="blog-posts-on-identity"></a>Blogové příspěvky na identitě

- [Co je SecurityStamp v ASP.NET Identity?](http://stackoverflow.com/questions/19487322/what-is-asp-net-identitys-iusersecuritystampstoretuser-interface/19505060#19505060)
- Od [Jan atten](https://twitter.com/xivSolutions)

    - [ASP.NET Identity 2,0 rozšíření modelů identit a používání celočíselných klíčů namísto řetězců](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
    - [ASP.NET Identity 2,0: přizpůsobení uživatelů a rolí](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)
    - [ASP.NET MVC a identita 2,0: Seznámení se základy](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)
    - [Nastavení ověření účtu a dvojúrovňové autorizace](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)
    - [Konfigurace připojení databáze a migrace kódu s prvními účty pro identity v ASP.NET MVC 5 a Visual Studio 2013](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)
- Od [Taiseer Joudeh](http://bitoftech.net/taiseer-joudeh-blog/)

    - [Ověřování založené na tokenech pomocí webového rozhraní API 2 pro ASP.NET, middleware Owin a ASP.NET Identity](http://bitoftech.net/2014/06/01/token-based-authentication-asp-net-web-api-2-owin-asp-net-identity/)
    - [Ověřování tokenu AngularJS pomocí ASP.NET webového rozhraní API 2, Owin a identity](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
    - [Povolte obnovovací tokeny OAuth v aplikaci AngularJS pomocí rozhraní ASP .NET Web API 2 a Owin – část 3.](http://bitoftech.net/2014/07/16/enable-oauth-refresh-tokens-angularjs-app-using-asp-net-web-api-2-owin/)
- Od [Anders Abel](https://twitter.com/anders_abel)

    - [Princip kanálu externího ověřování Owin](http://coding.abel.nu/2014/06/understanding-the-owin-external-authentication-pipeline/)
    - [Přehled ASP.NET Identity a Owin](http://coding.abel.nu/2014/06/asp-net-identity-and-owin-overview/)

  Autorem [k. Scott Allen](https://twitter.com/OdeToCode) při přihlášení k kódu

    - [ASP.NET Core identity](http://odetocode.com/blogs/scott/archive/2013/11/25/asp-net-core-identity.aspx) Tento blog prověřuje základní abstrakce, včetně IUser, IUserStore a I\*Storu.
    - [ASP.NET identity s Entity Framework](http://odetocode.com/blogs/scott/archive/2014/01/03/asp-net-identity-with-the-entity-framework.aspx) Individuální uživatelské účty v aplikacích MVC 5, webové rozhraní API a SPA, připojovací řetězce a Správa kontextů
    - [Možnosti vlastního nastavení pomocí ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/09/customization-options-with-asp-net-identity.aspx)
    - [Implementace ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- [Benjamin den](http://www.benday.com/about/)[– návod: identita ASP.NET MVC s ověřováním pomocí účtu Microsoft](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [Brock Allen](https://twitter.com/BrockLAllen)

    - [Úvod k externím poskytovatelům přihlášení (sociální přihlášení) pomocí middlewaru pro ověřování OWIN/Katana](http://brockallen.com/2014/01/09/a-primer-on-external-login-providers-social-logins-with-owinkatana-authentication-middleware/)
    - [Představujeme IdentityReboot](http://brockallen.com/2014/02/11/introducing-identityreboot/): sada rozšíření pro ASP.NET identity, které implementují hlavní chybějící funkce, na které jsem podal stížnost.
- [Pranav Rastogi předvádí](https://twitter.com/rustd)

    - [Získat další informace od poskytovatelů sociálních sítí](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [@beabigrockstar](https://twitter.com/beabigrockstar) (Jerrie Pelser)

    - [2. faktor ověřování](http://www.beabigrockstar.com/blog/2-factor-authentication-with-asp-net-identity-2-0-beta-1/)
    - [Používání služby Google Authenticator s ASP.NET Identity](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/)
    - [ASP.NET MVC 5 – ověřovací příručky](http://www.beabigrockstar.com/)
- [Získání dalších informací od poskytovatelů sociálních sítí použitých v šablonách projektů VS 2013](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [Vytvoření jednoduché aplikace ToDo pomocí ASP.NET Identity a přidružení uživatelů k ToDo](https://blogs.msdn.com/b/webdev/archive/2013/10/20/building-a-simple-todo-application-with-asp-net-identity-and-associating-users-with-todoes.aspx)
- [Problémy s integrací Google OpenId s ASP.NET identity](http://blog.technovert.com/2014/01/google-openid-integration-issues-asp-net-identity/) Pokud se zobrazí chyba: Chyba protokolu HTTP 404,15 – nenalezen modul filtrování požadavků je nakonfigurován tak, aby odepřel požadavek, který je řetězec dotazu příliš dlouhý.
- [Thinktecture. IdentityManager jako náhrada za WSAT](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [Ověřování tokenu AngularJS pomocí ASP.NET webového rozhraní API 2, Owin a identity](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [Jednoduchá Asp.net identity Core bez Entity Framework](https://code.msdn.microsoft.com/Simple-Aspnet-Identiy-Core-7475a961)
- [Práce s rolemi v ASP.NET identity pro MVC](http://www.dotnetfunda.com/articles/show/2898/working-with-roles-in-aspnet-identity-for-mvc) pomocí [Sheo Narayan](http://www.dotnetfunda.com/profile/sheonarayan.aspx)
- [Přechod na ASP.NET identity ze ASP.NET členství](http://webdojo.sharepoint.com/ajmatthews/_layouts/15/start.aspx#/Lists/Posts/Post.aspx?ID=2) podle Alistair Matthews

<a id="video"></a>

## <a name="videos"></a>Videa

- Kanál 9 [: zabezpečení aplikací a služeb ASP.NET: zabezpečení Facelift pro moderní aplikace](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B421#fbid=PhVT9E1WRtr?hashlink=fbid) od ido Flatow
- Kanál 9 [ASP.NET identity Úvod](https://channel9.msdn.com/Events/dotnetConf/2014/ASP-NET-Identity-Security) od Pranav Rastogi předvádí
- [ASP.NET ověřování pomocí ASP.NET identity](https://channel9.msdn.com/Shows/Web+Camps+TV/Special-Movember-Episode-ASPNET-Authentication-Provider) podle Cory Fowlera na Channel 9
- Kanál 9 [: vývoj moderních Web Apps: ASP.NET identity](https://channel9.msdn.com/Series/Building-Modern-Web-Apps/03) by Jan Koch
- Kanál 9 [zabezpečení webu pomocí ASP.NET identity](https://channel9.msdn.com/Events/TechDays/Techdays-2014-the-Netherlands/Securing-your-website-with-ASP-NET-Identity) Alex Thissen
- [Použití ASP.NET identity pro existující model databáze](https://www.youtube.com/watch?v=elfqejow5hM) Alexander Schmidt
- [ASP.NET jednu identitu](https://www.youtube.com/watch?v=w8GD-QIusKk) Ivaylo Kenov z Telerik
- [Česká ASP.NET identity](https://www.youtube.com/watch?v=tVbZp5brcpY) V této přednáškě vám ukážeme, jak nasadit základní ověřování, jak přidat podporu pro externí zprostředkovatele identity, jako je například Twitter nebo Facebook, a jak používat JEDNORÁZOVá hesla. [ASP.NET Identity je nástupce členem role Provider&#367; v ASP.NET, tedy knihovna pro zajišt&#283;ní autentizace uživatele.&#367; V této p&#345;ednášce si ukážeme, jak Nasad]

<a id="cust"></a>

## <a name="custom-storage-providers-for-aspnet-identity"></a>Vlastní poskytovatelé úložiště pro ASP.NET Identity

Pokud chcete napsat vlastního poskytovatele, přečtěte si [Přehled vlastních poskytovatelů úložiště pro ASP.NET identity](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md) a [implementaci ASP.NET identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx) a pak Projděte zdroj jednoho z následujících projektů OSS.

- Kurz: [Přehled poskytovatelů vlastních úložišť pro ASP.NET identity](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md) tím, že FitzMacken
- Blog: [implementace ASP.NET identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- Kurz:[nastavení základních účtů identit a jejich nasměrování do externí databáze](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx). [@xivSolutions](https://twitter.com/xivSolutions).
- Kurz[: implementace vlastního poskytovatele úložiště ASP.NET identity MySQL](../extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [Azure Table Storage](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) od James Randall.
- Azure Table Storage: [ASPNET. identity. TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) podle [@stuartleeks](https://twitter.com/stuartleeks).
- [CouchDB/Cloud podle Daniel Wertheim.](https://github.com/danielwertheim/mycouch.aspnet.identity)
- [Elastické hledání: elastická identita](https://github.com/bmbsqd/elastic-identity) podle Bombsquad AB
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) podle Jonathana Sheely Jonathana Sheely.
- [NHibernate. ASPNET. identity](https://github.com/milesibastos/NHibernate.AspNet.Identity) podle Antônio mil. Bastos.
- [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) podle [@tourismgeek](https://twitter.com/tourismgeek).
- [RavenDB. ASPNET. identity](https://github.com/ILMServices/RavenDB.AspNet.Identity) podle [ILMServices](http://www.ilmservice.com/).
- Redis: [Redis. ASPNET. identity](https://github.com/aminjam/Redis.AspNet.Identity)
- Šablony T4 pro generování kódu EF pro "první" databázi úložiště uživatele: [ASPNET. identity. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)

<a id="additional"></a>

## <a name="additional-aspnet-identity-resources"></a>Další prostředky ASP.NET Identity

- [Představujeme poskytovatele zabezpečení Yahoo a LinkedIn OAuth pro Owin](http://blog.beabigrockstar.com/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) pomocí Jerrie Pelser pro pokyny pro Yahoo a LinkedIn.

<a id="qand"></a>

## <a name="qampa-questionanswer"></a>Q&amp;A (otázka/odpověď)

- Otázka: zamčení uživatelé, kteří si zapnuli "zapamatování" (takže nebudou muset procházet 2FA v tomto počítači nebo prohlížeči), nejsou zamčené. Proč a jak zabráním? Odpovězte [sem](http://stackoverflow.com/questions/24312247/locked-out-users-can-login-if-they-have-auth-cookie).
- **Otázka**: Jak mohu ukládat vlastní deklarace identity, jako je například skutečný název uživatele, v souboru cookie ASP.NET identity, aby nedocházelo k zbytečným databázovým dotazům při každém požadavku. Odpovězte [sem](http://stackoverflow.com/questions/23622047/identity-cookie-loses-custom-claim-information-after-a-period-of-time).
- **Otázka: aktualizace hodnoty hash hesla AspNetUser**: Mám 2 projekty. Jeden z nich používá ověřování ASP.NET, druhý používá ověřování systému Windows, což je strana správy. Chci, aby projekt správce mohl spravovat uživatele druhé části. Můžu upravit všechno s výjimkou hesla. [Odpovězte sem](http://stackoverflow.com/questions/23880666/updating-aspnetuser-password-hash).
- **Otázka**: Jak můžu resetovat heslo jako správce pro jiné uživatele? Odpovězte [sem](http://stackoverflow.com/questions/23783249/identity-2-0-reset-password-by-admin/24211766#24211766).
- **Otázka**: mohu změnit zobrazený název pole UserName v ASP.NET MVC IdentityUser? Odpovězte [sem](http://stackoverflow.com/questions/23256650/can-i-change-the-displayed-name-of-the-username-field-in-asp-net-mvc-identityuse).
- **Otázka**: Jak můžu Gran oprávnění uživatelů k přidávání dalších uživatelů k určitým rolím? Odpovězte [sem](http://stackoverflow.com/questions/23695373/allow-users-to-grant-permissions-to-other-users-for-their-account-in-asp-net-ide).
- **Otázka**: ukládání informací o profilu v tabulce AspNetUsers a v tabulce AspNetUserClaims. Odpovězte [sem](http://stackoverflow.com/questions/23215727/is-there-any-benefit-to-storing-user-information-in-aspnetuserclaims-with-asp-ne).
- **Otázka**: zapamatujte si použití externího poskytovatele ověřování. Odpovězte [sem](http://stackoverflow.com/questions/23180896/how-to-remember-the-login-in-mvc5-when-an-external-provider-is-used).
- **Otázka**: Proč každý požadavek vyžaduje ApplicationDBContext, nemá příliš mnoho režie?. Odpověď, ne, režie je nízká.
- Otázka: Návody získat seznam přihlášených uživatelů? Odpovězte [sem](http://stackoverflow.com/questions/22995653/getting-a-list-of-logged-in-users-in-asp-net-identity/).
- Otázka: Jak můžu zjistit, kdy se uživatel přihlásí pomocí Microsoft. AspNet. identity? Odpovězte [sem](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698).
- Otázka: Návody získat lokalizované chybové zprávy pro identitu? Odpovězte [sem](http://stackoverflow.com/questions/22835981/asp-net-identity-localization-publickeytoken/22845864#22845864).
- Otázka: Návody nakonfigurovat CookieMiddleware, aby každých 30 minut získala nové deklarace identity? Odpovězte [sem](http://stackoverflow.com/questions/22682663/how-to-hold-the-cookies-claims-updated-with-mcv5-owin/22796932#22796932).
- Otázka: jak upravit deklarace identity pro uživatele po přihlášení? Odpovězte [sem](http://stackoverflow.com/questions/22768836/can-i-modify-claims-in-asp-net-identity-with-owin-after-calling-signin/22769963#22769963).
- Otázka: Návody Neověřovat tokeny zabezpečení? Odpovězte [sem](http://stackoverflow.com/questions/22755700/revoke-token-generated-by-usertokenprovider-in-asp-net-identity-2-0/22767286#22767286).
- Otázka: Jak lze ukládat deklarace identity v middlewaru souborů cookie? Odpovězte [sem](http://stackoverflow.com/questions/22320632/storing-retrieving-user-data-without-database-when-using-owin-cookie-authenticat/22541856#22541856).
- Otázka: chtěli byste mít kontrolu PIN nebo zabezpečení pro každou metodu akce v aplikaci MVC, ale chtěl bych Uložit úspěšné uživatele, aby nemuseli zadávat kód PIN při každém požadavku na tuto akci. Odpovězte [sem](http://stackoverflow.com/questions/22479958/security-check-an-user-to-a-access-controller-action/22486075#22486075).
- Otázka: Chci Uložit vrácenou e-mailovou adresu od poskytovatele sociálních sítí do databáze, jak to mám udělat? Odpověď [:](http://stackoverflow.com/questions/22888397/save-claims-to-db-on-login/22970969#22970969)
- Otázka: Jak můžu zjistit, kdy se uživatel přihlásí pomocí souboru cookie "zapamatování"? Odpovězte [sem](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698).
- Otázka: mohu změnit deklarace identity v ASP.NET Identity pomocí OWIN po volání přihlášení? Odpověď: volání přihlášení je přesně to, co byste chtěli udělat, když chcete upravit deklarace identity pro uživatele. V podstatě způsobí, že hodnota ClaimsIdentity se má serializovat do souboru cookie, takže se zobrazí nové deklarace v dalších požadavcích.
