---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
title: Konfigurace webu, který používá Aplikační služby (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET verze 2,0 představila řadu aplikačních služeb, které jsou součástí .NET Framework a slouží jako sada stavebních blokových služeb, které yo...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 9c31a42f-d8bb-4c0f-9ccc-597d4f70ac42
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
msc.type: authoredcontent
ms.openlocfilehash: 19e7258b558372259c7554a36c6ad73ce572dfa8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588690"
---
# <a name="configuring-a-website-that-uses-application-services-vb"></a>Konfigurace webu, který používá aplikační služby (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_vb.pdf)

> ASP.NET verze 2,0 představila řadu aplikačních služeb, které jsou součástí .NET Framework a slouží jako sada stavebních blokových služeb, které můžete použít k přidání bohatých funkcí do vaší webové aplikace. V tomto kurzu se seznámíte s postupem konfigurace webu v produkčním prostředí pro používání aplikačních služeb a řešení běžných potíží se správou uživatelských účtů a rolí v produkčním prostředí.

## <a name="introduction"></a>Úvod

ASP.NET verze 2,0 představila řadu *aplikačních služeb*, které jsou součástí .NET Framework a slouží jako sada stavebních blokových služeb, které můžete použít k přidání bohatých funkcí do vaší webové aplikace. Aplikační služby zahrnují:

- **Membership** – rozhraní API pro vytváření a správu uživatelských účtů.
- **Role** – rozhraní API pro kategorizaci uživatelů do skupin.
- **Profile** – rozhraní API pro ukládání vlastního obsahu, který je specifický pro uživatele.
- **Mapa webu** – rozhraní API pro definování logické struktury web s ve formě hierarchie, která se dá zobrazit prostřednictvím navigačních ovládacích prvků, jako jsou nabídky a popis cesty.
- **Individuální nastavení** – rozhraní API pro zachování předvoleb přizpůsobení, nejčastěji se používá u [*WebParts*](https://msdn.microsoft.com/library/e0s9t4ck.aspx).
- **Monitorování stavu** – rozhraní API pro monitorování výkonu, zabezpečení, chyb a dalších metrik stavu systému pro běžící webovou aplikaci.

Rozhraní API služby Application Services nejsou svázána se specifickou implementací. Místo toho dejte aplikačním službám pokyn, aby používaly konkrétního *poskytovatele*, a tento poskytovatel implementuje službu pomocí konkrétní technologie. Nejčastěji používané poskytovatele pro internetové webové aplikace hostované na webové hostující společnosti jsou tito poskytovatelé, kteří používají implementaci databáze SQL Server. `SqlMembershipProvider` je například poskytovatel pro rozhraní API pro členství, který ukládá informace o uživatelském účtu do databáze Microsoft SQL Server.

Při použití aplikačních služeb a zprostředkovatelů SQL Server se při nasazování aplikace přidávají nějaké výzvy. V případě startů musí být objekty databáze služby Application Services správně vytvořeny v databázích vývoje i v produkčním prostředí a náležitě inicializovány. K dispozici jsou také důležitá nastavení konfigurace, která je třeba provést.

> [!NOTE]
> Rozhraní API služby Application Services bylo navrženo pomocí [*modelu poskytovatele*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), což je vzor návrhu, který umožňuje poskytnout podrobné informace o implementaci rozhraní API v době běhu. .NET Framework se dodává s řadou poskytovatelů aplikačních služeb, které se dají použít, jako jsou `SqlMembershipProvider` a `SqlRoleProvider`, které jsou poskytovatelé pro rozhraní API pro členství a role, které používají implementaci databáze SQL Server. Můžete také vytvořit vlastního poskytovatele a vytvořit jeho modul plug-in. Ve skutečnosti již webová aplikace recenze obsahuje vlastního zprostředkovatele pro rozhraní API mapy webu (`ReviewSiteMapProvider`), které vytvoří mapu webu z dat v tabulkách `Genres` a `Books` v databázi.

V tomto kurzu se naučíte, jak rozšířit webovou aplikaci recenze knih na používání rozhraní API pro členství a role. Pak provede nasazení webové aplikace, která používá aplikační služby, s implementací databáze SQL Server a uzavírá se běžnými problémy se správou uživatelských účtů a rolí v produkčním prostředí.

## <a name="updates-to-the-book-reviews-application"></a>Aktualizace knihy aplikace recenze

V posledních několika kurzech se webová aplikace recenze pro knihu aktualizovala ze statického webu na dynamickou webovou aplikaci řízenou daty, která se dokončí sadou stránek pro správu pro správu žánrů a recenzí. Tato část pro správu ale v tuto chvíli není chráněná – libovolný uživatel, který zná (nebo odhadne) adresu URL stránky pro správu, může Waltz a vytvářet, upravovat nebo odstraňovat recenze na našem webu. Běžný způsob ochrany některých částí webu je implementace uživatelských účtů a následné použití autorizačních pravidel URL k omezení přístupu k určitým uživatelům nebo rolím. Tato příručka podporuje uživatelské účty a role, které jsou dostupné pro stažení v knize. Má definováno jednu roli s názvem admin a uživatelé v této roli mají přístup ke stránkám pro správu.

> [!NOTE]
> Ve webové aplikaci recenze knih jsem vytvořil tři uživatelské účty: Scott, Jisun a Alice. Všichni tři uživatelé mají stejné heslo: **heslo!** Scott a Jisun jsou v roli správce, ale Alice není. Stránky bez správy jsou stále přístupné pro anonymní uživatele. To znamená, že se k návštěvě webu nemusíte přihlašovat, pokud ho nechcete spravovat, v takovém případě se musíte přihlásit jako uživatel v roli správce.

Aktualizovaná stránka s přehledem aplikací v knize byla aktualizována tak, aby obsahovala jiné uživatelské rozhraní pro ověřené a anonymní uživatele. Pokud se na webu navštíví anonymní uživatel, uvidí v pravém horním rohu odkaz na přihlášení. Ověřený uživatel uvidí zprávu "Vítejte zpátky, *username*!". a odkaz pro odhlášení. K dispozici je také přihlašovací stránka (`~/Login.aspx`), která obsahuje přihlašovací webový ovládací prvek, který poskytuje uživatelské rozhraní a logiku pro ověřování návštěvníka. Pouze správci mohou vytvářet nové účty. (K dispozici jsou stránky pro vytváření a správu uživatelských účtů ve složce `~/Admin`)

### <a name="configuring-the-membership-and-roles-apis"></a>Konfigurace rozhraní API pro členství a role

V knize recenze webová aplikace používá rozhraní API členství a rolí k podpoře uživatelských účtů a k seskupení těchto uživatelů do rolí (konkrétně role správce). Třídy poskytovatele `SqlMembershipProvider` a `SqlRoleProvider` se používají proto, že chceme ukládat informace o účtu a rolích do databáze SQL Server.

> [!NOTE]
> Tento kurz není určen jako podrobné posouzení při konfiguraci webové aplikace pro podporu rozhraní API pro členství a role. Podrobné informace o těchto rozhraních API a krocích, které je třeba provést při konfiguraci webu pro jejich použití, najdete v tématu [*kurzy zabezpečení webu*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).

Chcete-li použít aplikační služby s databází SQL Server, musíte nejprve přidat databázové objekty používané těmito zprostředkovateli do databáze, kde chcete ukládat informace o uživatelském účtu a roli. Tyto požadované objekty databáze obsahují celou řadu tabulek, zobrazení a uložených procedur. Pokud není uvedeno jinak, třídy poskytovatele `SqlMembershipProvider` a `SqlRoleProvider` používají databázi SQL Server Express Edition s názvem `ASPNETDB` umístěnou ve složce `App_Data` aplikace. Pokud taková databáze neexistuje, automaticky se vytvoří s potřebnými databázovými objekty podle těchto zprostředkovatelů za běhu.

Je možné, a obvykle ideální, k vytvoření objektů databáze služby Application Services ve stejné databázi, kde jsou uložena data specifická pro web s aplikacemi. .NET Framework se dodává s nástrojem nazvaným `aspnet_regsql.exe`, který nainstaluje databázové objekty do zadané databáze. Jsem si prošli a použili jste tento nástroj k přidání těchto objektů do databáze `Reviews.mdf` ve složce `App_Data` (vývojová databáze). Po přidání těchto objektů do provozní databáze uvidíme, jak tento nástroj použít později v tomto kurzu.

Pokud přidáte objekty databáze služby Application Services do jiné databáze než `ASPNETDB`, bude nutné přizpůsobit konfigurace tříd poskytovatelů `SqlMembershipProvider` a `SqlRoleProvider`, aby používaly příslušnou databázi. Chcete-li přizpůsobit zprostředkovatele členství, přidejte do části `<system.web>` v `Web.config`[ *&lt;prvek&gt; Membership*](https://msdn.microsoft.com/library/1b9hw62f.aspx) ; ke konfiguraci poskytovatele rolí použijte [ *&lt;prvek&gt; roleManager*](https://msdn.microsoft.com/library/ms164660.aspx) . Následující fragment kódu je povedený z knihy recenze aplikace s `Web.config` a zobrazuje nastavení konfigurace pro rozhraní API pro členství a role. Všimněte si, že zaregistrujete nové poskytovatele – `ReviewMembership` a `ReviewRole`, která používají poskytovatele `SqlMembershipProvider` a `SqlRoleProvider`, v uvedeném pořadí.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample1.xml)]

`<authentication>` prvek `Web.config` souboru s byl také nakonfigurován pro podporu ověřování založeného na formulářích.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>Omezení přístupu ke stránkám pro správu

ASP.NET usnadňuje udělení nebo odmítnutí přístupu ke konkrétnímu souboru nebo složce podle uživatele nebo role pomocí funkce pro *autorizaci adresy URL* . (Krátce jsme probrali ověřování URL v *základních rozdílech mezi službou IIS a vývojovým serverem ASP.NET* a ukázali, jak služba IIS a vývojový server ASP.NET používají pravidla autorizace adresy URL odlišně pro statický vs dynamický obsah.) Vzhledem k tomu, že chceme zakázat přístup ke složce `~/Admin` s výjimkou uživatelů v roli správce, musíme do této složky přidat autorizační pravidla URL. Konkrétně autorizační pravidla URL potřebují povolit uživatelům v roli správce a odepřít všem ostatním uživatelům. To lze provést přidáním souboru `Web.config` do složky `~/Admin` s následujícím obsahem:

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample3.xml)]

Další informace o funkci autorizace adresy URL ASP.NET a o tom, jak ji použít k vyzkoušení autorizačních pravidel pro uživatele a role, najdete v kurzech k autorizaci [*uživatelů*](../../older-versions-security/membership/user-based-authorization-vb.md) a autorizaci na [*základě rolí*](../../older-versions-security/roles/role-based-authorization-vb.md) v tématu [*kurzy zabezpečení na webu*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).

## <a name="deploying-a-web-application-that-uses-application-services"></a>Nasazení webové aplikace, která používá Aplikační služby

Při nasazení webu, který používá aplikační služby a poskytovatele, který ukládá informace o aplikačních službách v databázi, je nezbytné, aby byly objekty databáze potřebné aplikačními službami vytvořeny v provozní databázi. Provozní databáze zpočátku tyto objekty neobsahuje, takže když je aplikace poprvé nasazena (nebo když je nasazená poprvé po přidání aplikačních služeb), musíte provést další kroky, abyste získali tyto požadované databázové objekty. provozní databáze.

Při nasazení webu, který používá aplikační služby, se může vyskytnout další výzva, pokud máte v úmyslu replikovat uživatelské účty vytvořené ve vývojovém prostředí do provozního prostředí. V závislosti na konfiguraci členství a rolí je možné, že i v případě, že jste úspěšně zkopírovali uživatelské účty, které byly vytvořeny ve vývojovém prostředí, do provozní databáze, tito uživatelé se nebudou moci přihlásit k webové aplikaci v produkčním prostředí. Podíváme se na příčinu tohoto problému a podíváme se, jak to brání.

ASP.NET se dodává s dobrým [*nástrojem pro správu webu (WSAT)* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) , který se dá spustit ze sady Visual Studio a umožňuje správu uživatelských účtů, rolí a autorizačních pravidel prostřednictvím webového rozhraní. WSAT bohužel funguje jenom pro místní weby, což znamená, že se nedá použít k vzdálené správě uživatelských účtů, rolí a autorizačních pravidel pro webovou aplikaci v produkčním prostředí. Podíváme se na různé způsoby implementace WSAT podobného chování z produkčního webu.

### <a name="adding-the-database-objects-using-aspnet_regsqlexe"></a>Přidání databázových objektů pomocí ASPNET\_regsql. exe

Kurz *nasazení databáze* ukázal, jak zkopírovat tabulky a data z vývojové databáze do provozní databáze a tyto techniky je určitě možné použít ke zkopírování databázových objektů služby Application Services do provozní databáze. Další možností je nástroj `aspnet_regsql.exe`, který přidává nebo odebírá objekty databáze služby Application Services z databáze.

> [!NOTE]
> Nástroj `aspnet_regsql.exe` vytvoří databázové objekty v zadané databázi. Nemigruje data v těchto databázových objektech z vývojové databáze do provozní databáze. Pokud máte v úmyslu zkopírovat informace o uživatelském účtu a roli do databáze vývoje do provozní databáze, použijte techniky popsané v kurzu *nasazení databáze* .

Pojďme se podívat na postup přidání databázových objektů do provozní databáze pomocí nástroje `aspnet_regsql.exe`. Začněte tím, že otevřete Průzkumníka Windows a přejdete do adresáře .NET Framework verze 2,0 v počítači,% WINDIR% \ Microsoft. NET\Framework\v2.0.50727. Měli byste najít nástroj `aspnet_regsql.exe`. Tento nástroj lze použít z příkazového řádku, ale obsahuje také grafické uživatelské rozhraní; dvojím kliknutím na soubor `aspnet_regsql.exe` spusťte jeho grafickou komponentu.

Nástroj se spustí zobrazením úvodní obrazovky vysvětlující její účel. Kliknutím na tlačítko Další přejdete na obrazovku vybrat možnost instalace, která je znázorněna na obrázku 1. Z tohoto místa můžete zvolit přidání databázových objektů služby Application Services nebo jejich odebrání z databáze. Vzhledem k tomu, že chceme tyto objekty přidat do provozní databáze, vyberte možnost konfigurovat SQL Server pro aplikační služby a klikněte na další.

[![můžete nakonfigurovat SQL Server pro Aplikační služby](configuring-a-website-that-uses-application-services-vb/_static/image2.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image1.jpg)

**Obrázek 1**: vyberte možnost konfigurace SQL Server pro aplikační služby ([kliknutím zobrazíte obrázek v plné velikosti).](configuring-a-website-that-uses-application-services-vb/_static/image3.jpg)

Na obrazovce Výběr serveru a databáze se zobrazí výzva k zadání informací, které se připojí k databázi. Zadejte databázový server, přihlašovací údaje zabezpečení a název databáze, který vám dodala vaše webová hostující společnost, a klikněte na další.

> [!NOTE]
> Po zadání vašeho databázového serveru a přihlašovacích údajů se při rozšiřování rozevíracího seznamu databáze může zobrazit chyba. Nástroj `aspnet_regsql.exe` se dotazuje na systémovou tabulku `sysdatabases`, aby načetla seznam databází na serveru, ale některé společnosti pro hostování webů zablokují své databázové servery, aby tyto informace nebyly veřejně dostupné. Pokud se zobrazí tato chyba, můžete zadat název databáze přímo do rozevíracího seznamu.

[![zadejte nástroj s informacemi o připojení databáze s.](configuring-a-website-that-uses-application-services-vb/_static/image5.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image4.jpg)

**Obrázek 2**: Poskytněte nástroji informace o připojení databáze s ([kliknutím zobrazíte obrázek v plné velikosti).](configuring-a-website-that-uses-application-services-vb/_static/image6.jpg)

Následující obrazovka shrnuje akce, které se chystáte provést, a to proto, aby objekty databáze služby Application Services byly přidány do zadané databáze. Kliknutím na tlačítko Další dokončete tuto akci. Po chvíli se zobrazí poslední obrazovka s vědomím, že byly přidány objekty databáze (viz obrázek 3).

[![úspěch! Objekty databáze Aplikační služby byly přidány do provozní databáze.](configuring-a-website-that-uses-application-services-vb/_static/image8.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image7.jpg)

**Obrázek 3**: úspěch! Objekty databáze Aplikační služby byly přidány do provozní databáze ([kliknutím zobrazíte obrázek v plné velikosti).](configuring-a-website-that-uses-application-services-vb/_static/image9.jpg)

Chcete-li ověřit, zda byly objekty databáze služby Application Services úspěšně přidány do provozní databáze, otevřete SQL Server Management Studio a připojte se k provozní databázi. Jak ukazuje obrázek 4, měli byste teď zobrazit tabulky databáze služby Application Services ve vaší databázi, `aspnet_Applications`, `aspnet_Membership`, `aspnet_Users`a tak dále.

[![ověřte, že se databázové objekty přidaly do provozní databáze.](configuring-a-website-that-uses-application-services-vb/_static/image11.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image10.jpg)

**Obrázek 4**: potvrďte, že se objekty databáze přidaly do provozní databáze ([kliknutím zobrazíte obrázek v plné velikosti).](configuring-a-website-that-uses-application-services-vb/_static/image12.jpg)

Nástroj `aspnet_regsql.exe` budete muset použít jenom při prvním nasazení webové aplikace, po tom, co jste začali používat aplikační služby. Jakmile se tyto objekty databáze nacházejí v provozní databázi, nebude nutné je znovu přidávat ani upravovat.

### <a name="copying-user-accounts-from-development-to-production"></a>Kopírování uživatelských účtů z vývoje do produkčního prostředí

Při použití tříd poskytovatele `SqlMembershipProvider` a `SqlRoleProvider` k ukládání informací služby Application Services do databáze SQL Server jsou informace o uživatelském účtu a roli uloženy v nejrůznějších databázových tabulkách, včetně `aspnet_Users`, `aspnet_Membership`, `aspnet_Roles`a `aspnet_UsersInRoles`, mimo jiné. Pokud během vývoje vytváříte uživatelské účty ve vývojovém prostředí, můžete tyto uživatelské účty v produkčním prostředí replikovat zkopírováním odpovídajících záznamů z příslušných databázových tabulek. Pokud jste použili Průvodce publikováním databáze k nasazení objektů databáze služby Application Services, jste se také rozhodli zkopírovat záznamy, což by vedlo k tomu, že uživatelské účty vytvořené při vývoji budou také v produkčním prostředí. V závislosti na nastavení konfigurace ale můžete zjistit, že uživatelé, jejichž účty byly vytvořeny ve vývoji a zkopírovány do produkčního prostředí, se nemohou přihlašovat z produkčního webu. Co nabízí?

Třídy poskytovatele `SqlMembershipProvider` a `SqlRoleProvider` byly navrženy tak, aby jedna databáze mohla sloužit jako úložiště uživatelů pro několik aplikací, kde každá aplikace může teoreticky mít uživatele s překrývajícími se uživatelskými jmény a rolemi se stejným názvem. Pro zajištění této flexibility udržuje databáze seznam aplikací v tabulce `aspnet_Applications` a každý uživatel je přidružen k jedné z těchto aplikací. Konkrétně tabulka `aspnet_Users` má `ApplicationId` sloupec, který přiřazuje jednotlivé uživatele k záznamu v tabulce `aspnet_Applications`.

Kromě sloupce `ApplicationId` obsahuje tabulka `aspnet_Applications` také sloupec `ApplicationName`, který pro aplikaci poskytuje výstižnější název. Když se webová stránka pokusí pracovat s uživatelským účtem, jako je například ověření přihlašovacích údajů uživatele z přihlašovací stránky, musí sdělit třídu `SqlMembershipProvider`, se kterou aplikace pracuje. Obvykle to dělá zadáním názvu aplikace a tato hodnota pochází z konfigurace poskytovatele s v `Web.config` – konkrétně prostřednictvím atributu `applicationName`.

Ale co se stane, pokud atribut `applicationName` není zadán v `Web.config`? V takovém případě členský systém používá jako hodnotu `applicationName` kořenovou cestu aplikace. Pokud atribut `applicationName` není explicitně nastaven v `Web.config`, existuje možnost, že vývojové prostředí a provozní prostředí používají jiný kořenový adresář aplikace, a proto budou přidruženy k různým názvům aplikací v aplikačních službách. Pokud k takovému neshodě dojde, uživatelé, kteří vytvořili ve vývojovém prostředí, budou mít `ApplicationId` hodnotu, která se neshoduje s hodnotou `ApplicationId` pro produkční prostředí. Výsledkem je, že uživatelé se nebudou moci přihlásit.

> [!NOTE]
> Pokud v této situaci zjistíte, že se uživatelské účty zkopírovaly do produkčního prostředí s neodpovídajícím `ApplicationId` hodnotou – můžete napsat dotaz, který aktualizuje tyto nesprávné `ApplicationId` hodnoty na `ApplicationId` používané v produkčním prostředí. Po aktualizaci se nyní uživatelé, jejichž účty byly vytvořeny ve vývojovém prostředí, budou moci přihlásit k webové aplikaci v produkčním prostředí.

Dobrá zpráva je, že existuje jednoduchý krok, který umožňuje zajistit, aby dvě prostředí používala stejný `ApplicationId` – explicitně nastavte atribut `applicationName` v `Web.config` pro všechny vaše poskytovatele služby Application Services. Explicitně nastavil (a) atribut `applicationName` na "BookReviews" v elementech `<membership>` a `<roleManager>`, jak ukazuje tento fragment kódu `Web.config`.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample4.xml)]

Další diskuzi o nastavení atributu `applicationName` a jeho odůvodnění najdete v blogovém příspěvku [*Scott Guthrie*](https://weblogs.asp.net/scottgu/) s, [*vždy nastavte vlastnost ApplicationName při konfiguraci členství v ASP.NET a dalších zprostředkovatelích*](https://weblogs.asp.net/scottgu/443634).

### <a name="managing-user-accounts-in-the-production-environment"></a>Správa uživatelských účtů v produkčním prostředí

Nástroj pro správu webu ASP.NET (WSAT) usnadňuje vytváření a správu uživatelských účtů, definování a použití rolí a kontrolu pravidel autorizace na základě uživatelů a rolí. WSAT můžete spustit ze sady Visual Studio tak, že přejdete na Průzkumník řešení a kliknete na ikonu konfigurace ASP.NET nebo přejdete na nabídku webu nebo projektu a vyberete položku nabídky konfigurace ASP.NET. WSAT bohužel může pracovat pouze s místními weby. Proto nemůžete použít WSAT z pracovní stanice ke správě webu v produkčním prostředí.

Dobrá zpráva je, že všechny funkce vystavené službou WSAT jsou k dispozici programově prostřednictvím rozhraní API pro členství a role. mnoho obrazovek WSAT navíc používá standardní ovládací prvky související s přihlášením ASP.NET. V krátkém případě můžete na web přidat ASP.NET stránky, které nabízejí nezbytné možnosti správy.

Odvoláte si předchozí kurz aktualizace webové aplikace Book recenze, aby zahrnovala složku `~/Admin` a tato složka je nakonfigurovaná tak, aby umožňovala uživatelům pouze roli správce. Přidal (a) jsem stránku do složky s názvem `CreateAccount.aspx`, ze které může správce vytvořit nový uživatelský účet. Tato stránka používá ovládací prvek ovládacím CreateUserWizard k zobrazení uživatelského rozhraní a back-endu logiky pro vytvoření nového uživatelského účtu. Čím víc, přizpůsobili jsme ovládací prvek tak, aby zahrnoval zaškrtávací políčko, které vás vyzve k přidání nového uživatele do role správce (viz obrázek 5). S malým množstvím práce můžete vytvořit vlastní sadu stránek, která implementuje úkoly související se správou uživatelů a rolí, které by jinak poskytovala služba WSAT.

> [!NOTE]
> Další informace o tom, jak používat rozhraní API pro členství a role společně s webovými ovládacími prvky ASP.NET souvisejících s přihlášením, najdete v tématu [*kurzy zabezpečení webu*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md). Další informace o přizpůsobení ovládacího prvku ovládacím CreateUserWizard naleznete v tématu [*vytváření uživatelských účtů*](../../older-versions-security/membership/creating-user-accounts-vb.md) a [*ukládání dalších*](../../older-versions-security/membership/storing-additional-user-information-vb.md) kurzů pro uživatele, případně v článku o [*Erich Peterson*](http://www.erichpeterson.com/) s, [*přizpůsobení ovládacího prvku ovládacím CreateUserWizard*](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx).

[Správci ![můžou vytvářet nové uživatelské účty.](configuring-a-website-that-uses-application-services-vb/_static/image14.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image13.jpg)

**Obrázek 5**: Správci mohou vytvářet nové uživatelské účty ([kliknutím zobrazíte obrázek v plné velikosti](configuring-a-website-that-uses-application-services-vb/_static/image15.jpg)).

Pokud potřebujete plnou funkčnost nástroje WSAT, podívejte se na [*vlastní nástroj pro správu*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)webu, ve kterém se autor Dan clem provede procesem vytvoření vlastního nástroje, který je podobný WSAT. Dan sdílí zdrojový kód aplikace s aplikací (v C#) a obsahuje podrobné pokyny pro jeho přidání na hostovaný Web.

## <a name="summary"></a>Přehled

Při nasazení webové aplikace, která používá implementaci databáze služby Application Services, je třeba nejprve zajistit, aby provozní databáze měla požadované objekty databáze. Tyto objekty lze přidat pomocí technik popsaných v kurzu *nasazení databáze* . Alternativně můžete použít nástroj `aspnet_regsql.exe`, jak jsme viděli v tomto kurzu. Další problémy jsme se dotkli při synchronizaci názvu aplikace používaného ve vývojovém a produkčním prostředí (což je důležité, pokud chcete, aby uživatelé a role vytvořené ve vývojovém prostředí byly platné při výrobě) a techniky pro Správa uživatelů a rolí v produkčním prostředí.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [*Nástroj pro registraci SQL Server ASP.NET (aspnet_regsql. exe)* ](https://msdn.microsoft.com/library/ms229862.aspx)
- [*Vytvoření databáze Aplikační služby pro SQL Server*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*Vytváření schématu členství v SQL Server*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb.md)
- [*Zkoumání členství, rolí a profilu ASP.NET s*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*Postup při zavedení vlastního nástroje pro správu webu*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*Kurzy zabezpečení webu*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*Přehled nástroje pro správu webu*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [Předchozí](configuring-the-production-web-application-to-use-the-production-database-vb.md)
> [Další](strategies-for-database-development-and-deployment-vb.md)
