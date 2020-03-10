---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-cs
title: Základy zabezpečení a podpora ASP.NET (C#) | Microsoft Docs
author: rick-anderson
description: Toto je první kurz v sérii kurzů, které procházejí postupy pro ověřování návštěvníků prostřednictvím webového formuláře a autorizaci přístupu k části...
ms.author: riande
ms.date: 01/13/2008
ms.assetid: 07e15538-2f29-40c6-b2e7-e6115075ac83
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-cs
msc.type: authoredcontent
ms.openlocfilehash: 1ccaac101a83d0e28b07b220b8b7b61a9039227e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640250"
---
# <a name="security-basics-and-aspnet-support-c"></a>Základy zabezpečení a podpora ASP.NET (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_cs.pdf)

> Toto je první kurz v řadě kurzů, které procházejí postupy pro ověřování návštěvníků prostřednictvím webového formuláře, autorizaci přístupu k určitým stránkám a funkcím a správě uživatelských účtů v aplikaci ASP.NET.

## <a name="introduction"></a>Úvod

Co se jedná o fóra na jednom pracovišti, elektronického obchodování weby, weby online e-maily, weby portálu a lokality sociálních sítí? Všechny nabízejí *uživatelské účty*. Lokality, které nabízejí uživatelské účty, musí poskytovat několik služeb. Aspoň noví Návštěvníci musí být schopní vytvořit účet a vracet návštěvníky, aby se mohli přihlásit. Tyto webové aplikace můžou učinit rozhodnutí na základě přihlášeného uživatele: některé stránky nebo akce můžou být omezené jenom na přihlášené uživatele nebo na určitou podmnožinu uživatelů. Další stránky mohou zobrazovat informace specifické pro přihlášeného uživatele nebo mohou zobrazit více nebo méně informací v závislosti na tom, co uživatel stránku zobrazuje.

Toto je první kurz v řadě kurzů, které procházejí postupy pro ověřování návštěvníků prostřednictvím webového formuláře, autorizaci přístupu k určitým stránkám a funkcím a správě uživatelských účtů v aplikaci ASP.NET. V průběhu těchto kurzů podíváme se na postupy:

- Identifikace uživatelů a jejich protokolování do webu
- Použijte ASP. Rozhraní členství v síti pro správu uživatelských účtů
- Vytváření, aktualizace a odstraňování uživatelských účtů
- Omezení přístupu k webové stránce, adresáři nebo konkrétním funkcím na základě přihlášeného uživatele
- Použijte ASP. .NET Framework Roles pro přidružení uživatelských účtů k rolím
- Správa rolí uživatelů
- Omezení přístupu k webové stránce, adresáři nebo konkrétním funkcím na základě role přihlášeného uživatele
- Přizpůsobte a rozšíříte ASP. Webové ovládací prvky zabezpečení sítě

Tyto kurzy jsou stručné a poskytují podrobné pokyny s mnoha snímky obrazovky, které vás provedou procesem vizuálně. Každý kurz je k dispozici v C# a Visual Basic verzích a zahrnuje stažení kompletního používaného kódu. (Tento první kurz se zaměřuje na koncepce zabezpečení z pohledu vysoké úrovně, a proto neobsahuje žádný přidružený kód.)

V tomto kurzu budeme pojednávat o důležitých konceptech zabezpečení a o tom, jaká zařízení jsou k dispozici v ASP.NET, která vám pomůžou implementovat ověřování formulářů, autorizaci, uživatelské účty a role. Pojďme začít!

> [!NOTE]
> Zabezpečení je důležitým aspektem jakékoli aplikace, která zahrnuje rozhodování o fyzických, technologických a politických rozhodnutích a vyžaduje vysoký stupeň plánování a znalostí v doméně. Tato série kurzů není určená jako vodítko pro vývoj zabezpečených webových aplikací. Místo toho se zaměřuje konkrétně na ověřování ve formulářích, autorizaci, uživatelské účty a role. I když jsou v této sérii popsány některé koncepce zabezpečení, které se týkají těchto problémů, ostatní jsou neprozkoumatelné.

## <a name="authentication-authorization-user-accounts-and-roles"></a>Ověřování, autorizace, uživatelské účty a role

Ověřování, autorizaci, uživatelské účty a role jsou čtyři výrazy, které se budou často používat v rámci této série kurzů, takže chci v rámci kontextu zabezpečení webu udělat rychlou chvilku, jak tyto výrazy definovat. V modelu klient-server, jako je například Internet, existuje mnoho scénářů, ve kterých server potřebuje identifikovat klienta, který požadavek odeslal. *Ověřování* je proces, který zjišťuje identitu klienta. Klient, který byl úspěšně identifikován, se označuje jako *ověřený*. Neidentifikovaný klient se označuje jako *neověřené* nebo *anonymní*.

Systémy zabezpečeného ověřování zahrnují alespoň jednu z následujících tří omezujících vlastností: [něco](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html), co znáte, nebo něco, co máte. Většina webových aplikací se spoléhá na něco, co klient ví, jako je například heslo nebo PIN kód. Informace, které slouží k identifikaci uživatelského jména a hesla, jsou například označovány jako *přihlašovací údaje*. Tento kurz se zaměřuje na *ověřování pomocí formulářů*. Jedná se o model ověřování, ve kterém se uživatelé přihlašují k webu zadáním přihlašovacích údajů ve formuláři webové stránky. Tento typ ověřování jsme dřív narazili na. Přejít na libovolný elektronického obchodování Web Až budete připraveni k rezervaci, budete požádáni o přihlášení zadáním uživatelského jména a hesla do textových polí na webové stránce.

Kromě určení klientů může server vyžadovat omezení prostředků nebo funkcí, které jsou dostupné v závislosti na klientovi, který požadavek odeslal. *Autorizace* je proces, který určuje, jestli má konkrétní uživatel oprávnění pro přístup k určitému prostředku nebo funkcím.

*Uživatelský účet* je úložiště, ve kterém se uchovávají informace o konkrétním uživateli. Uživatelské účty musí obsahovat minimálně informace, které uživatele jedinečně identifikují, například přihlašovací jméno uživatele a heslo. Spolu s těmito základními informacemi můžou uživatelské účty zahrnovat například e-mailovou adresu uživatele,. Datum a čas vytvoření účtu; Datum a čas posledního přihlášení; křestní jméno a příjmení; telefonní číslo; a poštovní adresa. Při použití ověřování pomocí formulářů se informace o uživatelském účtu obvykle ukládají do relační databáze, jako je Microsoft SQL Server.

Webové aplikace, které podporují uživatelské účty, můžou volitelně seskupit uživatele do *rolí*. Role je jednoduše popisek, který se používá pro uživatele, a poskytuje abstrakci pro definování autorizačních pravidel a funkcí na úrovni stránky. Web může například zahrnovat roli správce s autorizačními pravidly, která zakazují všem správcům přístup k určité sadě webových stránek. Kromě toho může být k dispozici celá řada stránek, které jsou přístupné všem uživatelům (včetně nesprávců), a mohou zobrazovat další data nebo nabízet další funkce při návštěvě uživatelů v roli správců. Pomocí rolí můžeme tato autorizační pravidla definovat na základě rolí, nikoli podle uživatele.

## <a name="authenticating-users-in-an-aspnet-application"></a>Ověřování uživatelů v aplikaci ASP.NET

Když uživatel zadá adresu URL do okna adresa prohlížeče nebo klikne na odkaz, prohlížeč vytvoří na webovém serveru požadavek [http (Hypertext Transfer Protocol)](http://en.wikipedia.org/wiki/HTTP) pro zadaný obsah, poASP.NET stránku, obrázek, soubor JavaScriptu nebo jakýkoli jiný typ obsahu. Webový server je na úkol, který vrací požadovaný obsah. V takovém případě je třeba určit počet věcí o žádosti, včetně toho, kdo žádost odeslal a zda je identita autorizována k načtení požadovaného obsahu.

Ve výchozím nastavení prohlížeče odesílají požadavky HTTP, u kterých chybí žádný druh identifikačních informací. Pokud ale prohlížeč obsahuje informace o ověřování, pak webový server spustí ověřovací pracovní postup, který se pokusí identifikovat klienta, který požadavek odeslal. Kroky pracovního postupu ověřování závisí na typu ověřování používaného webovou aplikací. ASP.NET podporuje tři typy ověřování: Windows, Passport a Forms. Tento kurz se zaměřuje na ověřování pomocí formulářů, ale potrváme vám několik minut na porovnání a kontrastu úložišť uživatelů a pracovních postupů pro ověřování systému Windows.

### <a name="authentication-via-windows-authentication"></a>Ověřování pomocí ověřování systému Windows

Pracovní postup ověřování systému Windows používá jednu z následujících metod ověřování:

- Základní ověřování
- Ověřování hodnotou hash
- Integrované ověřování systému Windows

Všechny tři techniky fungují přibližně stejným způsobem: Pokud neoprávněný, anonymní požadavek dorazí, webový server pošle zpět odpověď HTTP, která indikuje, že autorizace je nutná k pokračování. Prohlížeč pak zobrazí modální dialogové okno, které vyzve uživatele k zadání uživatelského jména a hesla (viz obrázek 1). Tyto informace se pak odesílají zpátky na webový server přes hlavičku HTTP.

![Modální dialogové okno vyzve uživatele k zadání přihlašovacích údajů.](security-basics-and-asp-net-support-cs/_static/image1.png)

**Obrázek 1**: modální dialogové okno vyzve uživatele k zadání přihlašovacích údajů.

Zadané přihlašovací údaje se ověřují proti uživatelskému úložišti Windows webového serveru. To znamená, že každý ověřený uživatel ve vaší webové aplikaci musí mít ve vaší organizaci účet systému Windows. Toto je maloobchodech v intranetových scénářích. Při použití integrovaného ověřování systému Windows v intranetovém nastavení prohlížeč automaticky poskytuje webový server s přihlašovacími údaji použitými pro přihlášení k síti, čímž potlačí dialogové okno zobrazené na obrázku 1. I když je ověřování systému Windows Skvělé pro intranetové aplikace, obvykle je neproveditelné pro internetové aplikace, protože nechcete vytvářet účty systému Windows pro každého a každého uživatele, který se zaregistruje na vašem webu.

### <a name="authentication-via-forms-authentication"></a>Ověřování prostřednictvím ověřování pomocí formulářů

Ověřování prostřednictvím formulářů je naopak ideální pro internetové webové aplikace. Odvolání tohoto ověřování pomocí formulářů identifikuje uživatele zobrazením výzvy k zadání přihlašovacích údajů prostřednictvím webového formuláře. Proto když se uživatel pokusí o přístup k neautorizovanému prostředku, automaticky se přesměruje na přihlašovací stránku, kde můžou zadat své přihlašovací údaje. Odeslané přihlašovací údaje se pak ověřují proti vlastnímu úložišti uživatelů – obvykle databáze.

Po ověření odeslaných přihlašovacích údajů se pro uživatele vytvoří *lístek ověřování pomocí formulářů* . Tento lístek indikuje, že uživatel byl ověřený a obsahuje identifikační informace, jako je například uživatelské jméno. Lístek ověřování pomocí formulářů je (obvykle) uložený jako soubor cookie v klientském počítači. Následné návštěvy na webu proto zahrnují lístek ověřování na základě formulářů v požadavku HTTP a tím umožníte, aby webová aplikace identifikovala uživatele po přihlášení.

Obrázek 2 znázorňuje pracovní postup ověřování pomocí formulářů ze Vantage bodu vysoké úrovně. Všimněte si, jak se části ověřování a autorizace v ASP.NET chovají jako dvě samostatné entity. Systém ověřování formuláři identifikuje uživatele (nebo sestavy, které jsou anonymní). Systém autorizací určuje, jestli má uživatel přístup k požadovanému prostředku. Pokud je uživatel neautorizovaný (jako na obrázku 2 při pokusu o anonymní návštěvě ProtectedPage. aspx), systém autorizace hlásí, že uživatel je odepřený, což způsobí, že systém ověřováním formulářů automaticky přesměruje uživatele na přihlašovací stránku.

Po úspěšném přihlášení uživatele zahrnují následné požadavky HTTP lístek ověřování formuláře. Systém ověřování založeného na formulářích pouze identifikuje uživatele – jedná se o autorizační systém, který určuje, zda uživatel může získat přístup k požadovanému prostředku.

![Pracovní postup ověřování formulářů](security-basics-and-asp-net-support-cs/_static/image2.png)

**Obrázek 2**: pracovní postup ověřování formulářů

V dalších dvou kurzech se budeme dig do ověřování prostřednictvím formulářů,[což je Přehled ověřování formulářů](an-overview-of-forms-authentication-cs.md) a [Konfigurace ověřování formulářů a Pokročilá témata](forms-authentication-configuration-and-advanced-topics-cs.md). Další informace najdete na ASP. Možnosti ověřování netto najdete v tématu [ověřování ASP.NET](https://msdn.microsoft.com/library/eeyk640h.aspx).

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>Omezení přístupu k webovým stránkám, adresářům a funkcím stránky

ASP.NET obsahuje dva způsoby, jak určit, jestli má konkrétní uživatel oprávnění pro přístup k určitému souboru nebo adresáři:

- **Autorizace souborů** – protože ASP.NET stránky a webové služby jsou implementované jako soubory, které se nacházejí v systému souborů webového serveru, přístup k těmto souborům se dá zadat pomocí seznamů Access Control (ACL). Autorizace souborů se nejčastěji používá při ověřování systému Windows, protože seznamy ACL jsou oprávnění, která platí pro účty systému Windows. Při použití ověřování pomocí formulářů se všechny požadavky na úrovni operačního systému a systému souborů spouští stejným účtem systému Windows, bez ohledu na to, uživatel navštívil web.
- **Autorizace adresy URL**– s autorizací adresy URL určuje vývojář stránky autorizační pravidla v souboru Web. config. Tato autorizační pravidla určují, kteří uživatelé nebo role mají povolený přístup, nebo jsou odepřeni přístup k určitým stránkám nebo adresářům v aplikaci.

Autorizace souborů a autorizace adres URL definují autorizační pravidla pro přístup ke konkrétní ASP.NET stránce nebo pro všechny ASP.NET stránky v konkrétním adresáři. Pomocí těchto postupů můžeme dát ASP.NET pokyn, aby odepřel žádosti na konkrétní stránku pro konkrétního uživatele, nebo povolit přístup k sadě uživatelů a odepřít přístup všem ostatním. Informace o scénářích, ve kterých mají všichni uživatelé přístup na stránku, ale funkce stránky závisí na uživateli? Například mnoho webů, které podporují uživatelské účty, má stránky, které zobrazují jiný obsah nebo data pro ověřené uživatele a anonymní uživatele. Anonymní uživatel se může podívat na odkaz pro přihlášení k webu, zatímco ověřený uživatel by místo toho zobrazil zprávu, jako je Vítejte zpět, *uživatelské jméno* a odkaz pro odhlášení. Další příklad: při prohlížení položky na webu aukce se zobrazí různé informace v závislosti na tom, zda jste uchazečem, nebo o jednu aukci položky.

Tyto úpravy na úrovni stránky je možné provést deklarativně nebo programově. Chcete-li zobrazit jiný obsah pro anonymní než ověřené uživatele, jednoduše přetáhněte [ovládací prvek LoginView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) na stránku a zadejte příslušný obsah do svých šablon AnonymousTemplate a LoggedInTemplate. Případně můžete programově určit, jestli je aktuální žádost ověřená a kdo je uživatel a jaké role patří (pokud existují). Tyto informace můžete použít k zobrazení nebo skrytí sloupců v mřížce nebo panelech na stránce.

Tato série obsahuje tři kurzy, které se zaměřují na autorizaci. ***Ověřování na základě uživatele***ověřuje, jak omezit přístup k stránce nebo stránkám v adresáři pro konkrétní uživatelské účty. ***Ověřování na základě rolí*** vyhledává autorizační pravidla na úrovni role; a konečně ***zobrazení obsahu na základě kurzu aktuálně přihlášeného uživatele*** zkoumá úpravu obsahu a funkcí konkrétní stránky na základě toho, co uživatel navštíví stránku. Další informace najdete na ASP. Možnosti autorizace netto najdete v tématu [autorizace ASP.NET](https://msdn.microsoft.com/library/wce3kxhd.aspx).

## <a name="user-accounts-and-roles"></a>Uživatelské účty a role

Formátu. Ověřování pomocí formulářů sítě poskytuje infrastrukturu pro uživatele, aby se přihlásili k lokalitě a aby jejich ověřený stav byl zapamatovatný přes návštěvy stránky. A autorizace URL nabízí rámec pro omezení přístupu ke konkrétním souborům nebo složkám v ASP.NET aplikaci. Žádná funkce ale ale poskytuje prostředky pro ukládání informací o uživatelském účtu nebo správě rolí.

Před ASP.NET 2,0 byly vývojáři odpovědni za vytváření vlastních úložišť uživatelů a rolí. Byly také na zavěšení pro návrh uživatelských rozhraní a psaní kódu pro základní stránky související s uživatelským účtem, jako je přihlašovací stránka a stránka, k vytvoření nového účtu mimo jiné. Bez vestavěné architektury uživatelských účtů v ASP.NET museli všichni vývojáři implementující uživatelské účty dorazit na vlastní rozhodnutí o návrhu na otázky, jako je Návody ukládání hesel nebo jiné citlivé informace? a jaké pokyny mám v souvislosti s délkou a silou hesla ukládat?

V současné době implementace uživatelských účtů v aplikaci ASP.NET mnohem jednodušší díky *rozhraní členství* a vestavěným přihlašovacím webovým ovládacím prvkům. Rozhraní členství je několik tříd v [oboru názvů System. Web. Security](https://msdn.microsoft.com/library/system.web.security.aspx) , který poskytuje funkce pro provádění základních úloh souvisejících s uživatelským účtem. Klíčovou třídou v rozhraní členství je [Třída členství](https://msdn.microsoft.com/library/system.web.security.membership.aspx), která má metody jako:

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- ValidateUser

Rozhraní členství používá [model poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), který čistě odděluje rozhraní API rozhraní pro členství z jeho implementace. To umožňuje vývojářům použít společné rozhraní API, ale jim umožní používat implementaci, která splňuje vlastní potřeby svých aplikací. V krátkém případě třída členství definuje základní funkce architektury (metody, vlastnosti a události), ale ve skutečnosti neposkytuje žádné podrobnosti implementace. Místo toho metody třídy členství vyvolají nakonfigurovaného poskytovatele, což je to, co provádí skutečnou práci. Například pokud je vyvolána metoda CreateUser třídy členství, třída Membership neví podrobnosti o úložišti uživatele. Neví se, jestli se uživatelé uchovávají v databázi nebo v souboru XML nebo v jiném úložišti. Třída členství kontroluje konfiguraci webové aplikace, aby určila, k jakému poskytovateli je delegováno volání, a že třída poskytovatele zodpovídá za vytvoření nového uživatelského účtu v příslušném úložišti uživatele. Tato interakce je znázorněna na obrázku 3.

Společnost Microsoft dodává dvě třídy zprostředkovatele členství v .NET Framework:

- [ActiveDirectoryMembershipProvider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) – implementuje rozhraní API pro členství ve službě Active Directory a serverech služby Active Directory Application Mode (ADAM).
- [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) – implementuje rozhraní API pro členství v databázi SQL Server.

Tato série kurzů se zaměřuje výhradně na SqlMembershipProvider.

[![model poskytovatele umožňuje, aby byly různé implementace bez problémů zapojeny do rozhraní&lt;/Strong&gt;](security-basics-and-asp-net-support-cs/_static/image4.png)](security-basics-and-asp-net-support-cs/_static/image3.png)

**Obrázek 03**: model poskytovatele umožňuje bez problémů připojit různé implementace do architektury ([kliknutím zobrazíte obrázek v plné velikosti).](security-basics-and-asp-net-support-cs/_static/image5.png)

Výhodou modelu poskytovatele je, že je možné vyvíjet alternativní implementace od společnosti Microsoft, dodavatelů třetích stran nebo jednotlivých vývojářů a bezproblémově zapojených do rozhraní členství. Společnost Microsoft například vydala [poskytovatele členství pro databáze aplikace Microsoft Access](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi). Další informace o zprostředkovatelích členství najdete v tématu [Sada nástrojů pro zprostředkovatele](https://msdn.microsoft.com/asp.net/aa336558.aspx), která zahrnuje návod poskytovatelů členství, ukázkové vlastní zprostředkovatele, více než 100 stránek dokumentace k modelu poskytovatele a kompletní zdrojový kód pro předdefinované poskytovatele členství (konkrétně ActiveDirectoryMembershipProvider a SqlMembershipProvider).

ASP.NET 2,0 také zavádí rámec rolí. Podobně jako rozhraní členství, rozhraní role je sestaveno základem modelem poskytovatele. Jeho rozhraní API je zveřejněné přes [třídu role](https://msdn.microsoft.com/library/system.web.security.roles.aspx) a .NET Framework lodí se třemi třídami poskytovatele:

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) – spravuje informace o rolích v úložišti zásad autorizace Správce autorizací, jako je například služba Active Directory nebo ADAM.
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) – implementuje role v databázi SQL Server.
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) – přidruží informace role na základě skupiny oken návštěvníka. Tato metoda se obvykle používá při ověřování systému Windows.

Tato série kurzů se zaměřuje výhradně na SqlRoleProvider.

Vzhledem k tomu, že model poskytovatele zahrnuje jediné rozhraní API pro přeposílání (třídy členství a rolí), je možné vytvořit funkce kolem tohoto rozhraní API, aniž byste si museli dělat starosti s podrobnostmi implementace – ty jsou zpracovávány poskytovateli vybranými na stránce. maximalizac. Toto sjednocené rozhraní API umožňuje výrobcům Microsoftu a třetích stran vytvářet webové ovládací prvky, které jsou rozhraními s architekturou členství a rolí. ASP.NET se dodává s řadou [přihlašovacích webových ovládacích prvků](https://msdn.microsoft.com/library/ms178329.aspx) pro implementaci běžných uživatelských rozhraní uživatelských účtů. [Přihlašovací ovládací prvek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) například vyzve uživatele k zadání přihlašovacích údajů, ověří je a pak je přihlásí do ověřování pomocí formulářů. [Ovládací prvek LoginView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) nabízí šablony pro zobrazení různých značek anonymním uživatelům oproti ověřeným uživatelům nebo jiné označení na základě role uživatele. A [ovládací prvek ovládacím CreateUserWizard](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx) poskytuje podrobné uživatelské rozhraní pro vytvoření nového uživatelského účtu.

Pod rámec pokrývá různé přihlašovací ovládací prvky interakci s architekturou pro členství a role. Většinu ovládacích prvků pro přihlášení lze implementovat bez nutnosti napsat jediný řádek kódu. Tyto ovládací prvky podrobněji prověříme v budoucích kurzech, včetně technik pro rozšíření a přizpůsobení jejich funkcí.

## <a name="summary"></a>Souhrn

Všechny webové aplikace, které podporují uživatelské účty, vyžadují podobné funkce, jako například: možnost přihlášení uživatelů a jejich stav přihlášení při návštěvě stránky. Webová stránka pro nové návštěvníky pro vytvoření účtu; a schopnost vývojáře stránky určit, který prostředek, data a funkce jsou k dispozici pro uživatele nebo role. Úkoly ověřování a autorizace uživatelů a správy uživatelských účtů a rolí se výjimečně snadno s ASP.NET aplikacemi díky ověřování prostřednictvím formulářů, autorizaci adres URL a architekturám členství a rolí.

V průběhu několika dalších kurzů prověříme tyto aspekty vytvořením pracovní webové aplikace od základů podle kroků. V dalším dvou kurzech se podrobněji prozkoumáme ověřování formulářů. V akci se zobrazí pracovní postup ověřování pomocí formulářů, Dissect lístek ověřování pomocí formulářů, projednávat problémy zabezpečení a zjistíte, jak nakonfigurovat systém ověřování pomocí formulářů – vše při vytváření webové aplikace, která umožňuje návštěvníkům přihlášení a odhlášení.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [ASP.NET 2,0 členství, role, ověřování formulářů a prostředky zabezpečení](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [Pokyny pro zabezpečení ASP.NET 2,0](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET ověřování](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [Autorizace ASP.NET](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [Přehled ovládacích prvků přihlášení ASP.NET](https://msdn.microsoft.com/library/ms178329.aspx)
- [Zkoumání členství, rolí a profilů v ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Jak můžu: zabezpečit web pomocí členství a rolí?](https://asp.net/learn/videos/video-45.aspx) (Video)
- [Úvod do členství](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [Středisko pro vývojáře zabezpečení MSDN](https://msdn.microsoft.com/security/default.aspx)
- [Professional ASP.NET 2,0 zabezpečení, členství a Správa rolí](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [Sada nástrojů pro poskytovatele](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Vedoucí recenzent pro tento kurz byl tento kurz zkontrolován řadou užitečných revidujících. Kontroloři vedoucí pro tento kurz zahrnují Alicja Maziarz, John Suru a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](an-overview-of-forms-authentication-cs.md)
