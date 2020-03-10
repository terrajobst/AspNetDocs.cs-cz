---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: Úvod do ASP.NET Identity-ASP.NET 4. x
author: jongalloway
description: Systém členství v ASP.NET byl představený s ASP.NET 2,0 zpátky v 2005 a od té doby existovala mnoho změn v různých způsobech, proč se webové aplikace typický...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0268dfc16cd2cfb1e79ee14997a4c5eb247af950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583844"
---
# <a name="introduction-to-aspnet-identity"></a>Úvod do ASP.NET Identity

> Systém členství v ASP.NET byl představený s ASP.NET 2,0 zpátky v 2005 a od té doby existovala mnoho změn v tom, jak webové aplikace obvykle zpracovávají ověřování a autorizaci. ASP.NET Identity je nový pohled na to, jaký systém členství by měl být při vytváření moderních aplikací pro web, telefon nebo tablet.

## <a name="background-membership-in-aspnet"></a>Pozadí: členství v ASP.NET

### <a name="aspnet-membership"></a>Členství v ASP.NET

[Členství v ASP.NET](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx) bylo navrženo pro řešení požadavků na členství v lokalitě, které byly běžné v 2005, které zahrnovaly ověřování pomocí formulářů, a SQL Server databáze pro uživatelská jména, hesla a data profilu. Dnes existuje mnohem širší škála možností úložiště dat pro webové aplikace a většina vývojářů chce povolit svým webům používat poskytovatele sociálních identit k ověřování a autorizaci funkcí. Omezení návrhu členství v ASP.NET je obtížné převést:

- Schéma databáze bylo navrženo pro SQL Server a nelze je změnit. Můžete přidat informace o profilu, ale další data se zabalí do jiné tabulky, což ztěžuje přístup jakýmkoli prostředkem s výjimkou rozhraní API pro poskytovatele profilu.
- Systém poskytovatele vám umožňuje změnit úložiště zálohovaných dat, ale systém je navržený na základě předpokladů, které jsou vhodné pro relační databázi. Můžete napsat poskytovatele pro ukládání informací o členství v nerelačním mechanismu úložiště, jako je například Azure Storage tabulky, ale je nutné obejít relační návrh tak, že napíšete mnohem kód a spoustu `System.NotImplementedException` výjimek pro metody, které neplatí pro databáze NoSQL.
- Vzhledem k tomu, že funkce přihlášení a přihlášení jsou založené na ověřování pomocí formulářů, nemůže systém členství používat [Owin](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md). OWIN zahrnuje komponenty middlewaru pro ověřování, včetně podpory pro protokoly pomocí externích zprostředkovatelů identity (jako jsou účty Microsoft, Facebook, Google, Twitter) a přihlášení pomocí účtů organizace z místní služby Active Directory nebo Azure Active Directory. OWIN také zahrnuje podporu OAuth 2,0, JWT a CORS.

### <a name="aspnet-simple-membership"></a>ASP.NET jednoduché členství

[ASP.NET jednoduché členství](../../../web-pages/overview/security/16-adding-security-and-membership.md) bylo vyvinuto jako systém členství pro webové stránky ASP.NET. Byl vydaný pomocí WebMatrixu a sady Visual Studio 2010 SP1. Cílem jednoduchého členství bylo usnadnit přidávání funkcí členství do aplikace webové stránky.

Jednoduché členství usnadňuje přizpůsobení informací o profilu uživatele, ale stále sdílí ostatní problémy se členstvím v ASP.NET a má určitá omezení:

- Je těžké zachovat systémová data v nerelačním úložišti.
- Nemůžete ho použít s OWIN.
- Nefunguje dobře se stávajícími poskytovateli členství ASP.NET a není rozšiřitelný.

### <a name="aspnet-universal-providers"></a>ASP.NET Universal Providers

[ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) byly vyvinuty tak, aby bylo možné uchovávat informace o členství v Microsoft Azure SQL Database a také pracují s SQL Server Compact. Univerzální poskytovatelé byli postaveni na Entity Framework Code First, což znamená, že univerzální poskytovatelé lze použít k uchovávání dat v jakémkoli úložišti podporovaném EF. U univerzálních zprostředkovatelů se schéma databáze vyčistilo i hodně.

Univerzální poskytovatelé jsou postaveni na infrastruktuře členství v ASP.NET, takže stále mají stejná omezení jako poskytovatel SqlMembership. To znamená, že byly navržené pro relační databáze a je obtížné přizpůsobit profil a informace o uživateli. Tito zprostředkovatelé také stále používají ověřování pomocí formulářů pro funkce přihlášení a odhlášení.

## <a name="aspnet-identity"></a>ASP.NET Identity

Vzhledem k tom, že příběh členů v ASP.NET se vyvinulo v průběhu let, tým ASP.NET od zákazníků dozvěděl spoustu názoru.

Předpokladem, že se uživatelé přihlásí zadáním uživatelského jména a hesla, které zaregistrovali ve vaší vlastní aplikaci, již nejsou platné. Web se stalější sociální. Uživatelé vzájemně vzájemně pracují v reálném čase prostřednictvím sociálních kanálů, jako jsou Facebook, Twitter a další sociální weby. Vývojáři chtějí, aby se uživatelé mohli přihlašovat pomocí svých sociálních identit, aby mohli mít na svých webech bohatou činnost. Moderní systém členství musí umožňovat přihlašování na základě přesměrování na zprostředkovatele ověřování, jako je Facebook, Twitter a další.

Vývoj webů byl vyvinutý, takže jsme měli vzory vývoje webů. Testování částí kódu aplikace se stalo základním problémem pro vývojáře aplikací. V 2008 ASP.NET bylo přidáno nové rozhraní založené na vzoru MVC (Model-View-Controller), v rámci kterého mohou vývojáři pomáhat vývojářům při sestavování aplikací ASP.NET jednotek testovatelné. Vývojáři, kteří chtěli testovat svou logiku aplikace, také chtěli být schopni to udělat se systémem členství.

S ohledem na tyto změny vývoje webových aplikací bylo ASP.NET Identity vyvinuto s následujícími cíli:

- **Jeden ASP.NET Identity systém**

    - ASP.NET Identity lze použít se všemi ASP.NET architekturami, jako jsou ASP.NET MVC, webové formuláře, webové stránky, webové rozhraní API a Signal.
    - ASP.NET Identity lze použít při vytváření webů, telefonů, obchodů nebo hybridních aplikací.
- **Snadné zapojení do profilových dat o uživateli**

    - Máte kontrolu nad schématem informací o uživatelích a profilech. Můžete například snadno povolit, aby systém ukládal data narození zadaná uživateli při registraci účtu ve vaší aplikaci.

- **Ovládací prvek trvalosti**

    - Ve výchozím nastavení ukládá ASP.NET Identity systém do databáze všechny informace o uživateli. ASP.NET Identity používá Entity Framework Code First k implementaci veškerého mechanismu trvalosti.
    - Vzhledem k tomu, že byste měli řídit schéma databáze, je jednoduché provádět běžné úlohy, jako je například změna názvů tabulek nebo změna datového typu primárních klíčů.
    - Je snadné připojit se k různým mechanismům úložiště, jako je SharePoint, Azure Storage Table Service, NoSQL databáze atd., aniž by bylo nutné vyvolávat výjimky `System.NotImplementedExceptions`.
- **Testování částí**

    - ASP.NET Identity zpřístupňuje testovatelné webové aplikace. Můžete napsat testy jednotek pro části aplikace, které používají ASP.NET Identity.
- **Zprostředkovatel rolí**

    - Existuje zprostředkovatel rolí, který umožňuje omezit přístup k částem aplikace podle rolí. Můžete snadno vytvořit role, jako je například admin a přidat uživatele k rolím.
- **Založené na deklaracích**

    - ASP.NET Identity podporuje ověřování založené na deklaracích, kde je identita uživatele reprezentována jako sada deklarací. Deklarace identity umožňují vývojářům mnohem pružnější v popisu identity uživatele, než povoluje role. Vzhledem k tomu, že členství role je jenom logická hodnota (člen nebo nečlen), může deklarace identity zahrnovat rozšířené informace o identitě a členství uživatele.
- **Poskytovatelé sociálních přihlášení**

    - Do své aplikace můžete snadno přidat protokoly pro sociální sítě, jako je například účet Microsoft, Facebook, Twitter, Google a další, a data specifická pro uživatele v aplikaci ukládat.

- **Integrace OWIN**

    - Ověřování ASP.NET je teď založené na middlewaru OWIN, který se dá použít na jakémkoli hostiteli založeném na OWIN. ASP.NET Identity nemá žádnou závislost na System. Web. Jedná se o plně kompatibilní OWIN architekturu a dá se použít v libovolné aplikaci hostované v OWIN.
    - ASP.NET Identity používá ověřování OWIN pro přihlášení nebo odhlášení uživatelů na webu. To znamená, že místo použití FormsAuthentication k vygenerování souboru cookie použije aplikace OWIN CookieAuthentication.
- **Balíček NuGet**

    - ASP.NET Identity se znovu distribuuje jako balíček NuGet, který je nainstalovaný v šablonách ASP.NET MVC, Web Forms a Web API, které se dodávají se sadou Visual Studio 2017. Tento balíček NuGet si můžete stáhnout z galerie NuGet.
    - Uvolnění ASP.NET Identity jako balíčku NuGet usnadňuje týmu ASP.NET iterace na nových funkcích a opravách chyb a jejich doručování vývojářům agilním způsobem.

## <a name="get-started-with-aspnet-identity"></a>Začínáme s ASP.NET Identity

ASP.NET Identity se používá v šablonách projektů sady Visual Studio 2017 pro ASP.NET MVC, webové formuláře, webové rozhraní API a zabezpečené ověřování hesla. V tomto návodu ukážeme, jak šablony projektu používají ASP.NET Identity k přidání funkcí k registraci, přihlášení a odhlášení uživatele.

ASP.NET Identity je implementováno pomocí následujícího postupu. Účelem tohoto článku je poskytnout vám přehled o vysoké úrovni ASP.NET Identity; můžete postupovat podle kroku, nebo si jen přečtěte podrobnosti. Podrobnější pokyny k vytváření aplikací pomocí ASP.NET Identity, včetně použití nového rozhraní API k přidání uživatelů, rolí a informací o profilu, najdete v části Další kroky na konci tohoto článku.

1. Vytvořte aplikaci ASP.NET MVC s jednotlivými účty. Můžete použít ASP.NET Identity v ASP.NET MVC, webové formuláře, webové rozhraní API, signalizaci atd. V tomto článku začneme s aplikací ASP.NET MVC.  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. Vytvořený projekt obsahuje následující tři balíčky pro ASP.NET Identity.

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   Tento balíček má Entity Framework implementaci ASP.NET Identity, která bude uchovávat ASP.NET Identity data a schéma SQL Server.
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   Tento balíček má základní rozhraní pro ASP.NET Identity. Tento balíček se dá použít k zápisu implementace pro ASP.NET Identity, které cílí na různá úložiště trvalosti, jako je Azure Table Storage, databáze NoSQL atd.
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   Tento balíček obsahuje funkce, které slouží k připojení ověřování OWIN pomocí ASP.NET Identity v aplikacích ASP.NET. Tato možnost se používá, když do aplikace přidáte funkci přihlašování a zavoláte do middleware pro ověřování souborů cookie OWIN k vygenerování souboru cookie.
3. Vytváří se uživatel.  
   Spusťte aplikaci a kliknutím na odkaz **zaregistrovat** vytvořte uživatele. Následující obrázek ukazuje stránku registrace, která shromažďuje uživatelské jméno a heslo.  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   Když uživatel vybere tlačítko **Registrovat** , `Register` akce řadiče účtů vytvoří uživatele VOLÁNÍM rozhraní API ASP.NET identity, jak je zvýrazněno níže:

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. Přihlásit se.  
   Pokud byl uživatel úspěšně vytvořen, je přihlášen metodou `SignInAsync`.  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]

   Metoda `SignInManager.SignInAsync` generuje [hodnota ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx). Vzhledem k tomu, že ASP.NET Identity a ověřování souborů cookie OWIN jsou systémy založené na deklaracích, rozhraní vyžaduje, aby aplikace vygenerovala hodnota ClaimsIdentity pro uživatele. Hodnota ClaimsIdentity obsahuje informace o všech deklaracích identity pro uživatele, například o tom, k jakým rolím uživatel patří.   
 
5. Odhlaste se.  
   Vyberte odkaz **Odhlásit se** a zavolejte akci odhlášení v řadiči účtů. 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   Zvýrazněný kód výše ukazuje metodu OWIN `AuthenticationManager.SignOut`. To je obdobou jako metoda [FormsAuthentication. Signing](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) , kterou používá modul [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) ve webových formulářích.

## <a name="components-of-aspnet-identity"></a>Součásti ASP.NET Identity

Následující diagram ukazuje součásti ASP.NET Identity systému (vyberte na [tomto](introduction-to-aspnet-identity/_static/image3.png) nebo v diagramu, abyste ho rozšířili). Balíčky v zeleně tvoří ASP.NET Identity systém. Všechny ostatní balíčky jsou závislosti, které je potřeba k používání ASP.NET Identityho systému v aplikacích ASP.NET.

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

Následuje stručný popis balíčků NuGet, které nebyly dřív zmíněny:

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 Middleware, který umožňuje aplikaci používat ověřování na základě souborů cookie, podobně jako ASP. Ověřování formulářů netto.
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Entity Framework je pro relační databáze doporučena technologie pro přístup k datům společnosti Microsoft.

## <a name="migrating-from-membership-to-aspnet-identity"></a>Migrace z členství na ASP.NET Identity

Doufáme, že brzy poskytneme pokyny k migraci stávajících aplikací, které používají členství v ASP.NET nebo jednoduché členství v novém systému ASP.NET Identity.

## <a name="next-steps"></a>Další kroky

- [Vytvoření aplikace ASP.NET MVC 5 pomocí Facebooku a přihlášení Google OAuth2 a OpenID](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 Tento kurz používá rozhraní ASP.NET Identity API k přidání informací o profilu do uživatelské databáze a k ověřování pomocí Google a Facebooku.
- [Vytvořte aplikaci ASP.NET MVC s ověřováním a SQL DB a nasaďte ji do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 V tomto kurzu se dozvíte, jak pomocí rozhraní API identity přidat uživatele a role.
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 Ukázková aplikace, která ukazuje, jak přidat základní role a podporu uživatelů a jak provádět role a správu uživatelů.
