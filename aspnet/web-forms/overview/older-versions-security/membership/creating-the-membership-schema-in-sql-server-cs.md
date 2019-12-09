---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: Vytváření schématu členství v SQL Server (C#) | Microsoft Docs
author: rick-anderson
description: Tento kurz začíná zkoumáním technik pro přidání potřebného schématu do databáze, aby bylo možné používat SqlMembershipProvider. Po připojení k síti Wi...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 97623e7c13ab7799b9dadbb8e52be8e0cd99e252
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595038"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>Vytvoření schématu členství v SQL Serveru (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> Tento kurz začíná zkoumáním technik pro přidání potřebného schématu do databáze, aby bylo možné používat SqlMembershipProvider. V tomto případě probereme klíčové tabulky ve schématu a podíváme se na jejich účel a důležitost. V tomto kurzu se dozvíte, jak říct aplikaci ASP.NET, kterou by měl poskytovatel členství použít.

## <a name="introduction"></a>Úvod

Předchozí dva kurzy byly zkontrolovány pomocí ověřování pomocí formulářů k identifikaci návštěvníků webu. Architektura pro ověřování pomocí formulářů umožňuje vývojářům snadno přihlašovat uživatele do webu a zapamatovat si je na stránkách přes použití ověřovacích lístků. Třída `FormsAuthentication` zahrnuje metody pro generování lístku a jejich přidání do souborů cookie návštěvníka. `FormsAuthenticationModule` prověřuje všechny příchozí požadavky a pro ty s platným ověřovacím lístkem vytvoří a přidruží `GenericPrincipal` a objekt `FormsIdentity` s aktuální žádostí. Ověřování pomocí formulářů je pouze mechanismus pro udělení ověřovacího lístku návštěvníkovi při přihlášení a v následných požadavcích na analýzu tohoto lístku za účelem určení identity uživatele. Aby webová aplikace podporovala uživatelské účty, stále musíme implementovat uživatelské úložiště a přidat funkce pro ověření přihlašovacích údajů, registraci nových uživatelů a nesčetných dalších úloh souvisejících s uživatelským účtem.

Před ASP.NET 2,0 byly vývojáři na vidlici pro implementaci všech úkolů souvisejících s uživatelským účtem. Naštěstí tým ASP.NET tyto nedostatky rozpoznal a zavedl rámec členství v ASP.NET 2,0. Rozhraní členství je sada tříd v .NET Framework, které poskytují programové rozhraní pro provádění úloh souvisejících s uživatelským účtem. Tato architektura je sestavená základem [modelem poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), který vývojářům umožňuje připojit přizpůsobenou implementaci do standardizovaného rozhraní API.

Jak je popsáno v <a id="Tutorial1"> </a>kurzu [*Základy zabezpečení a ASP.net support*](../introduction/security-basics-and-asp-net-support-cs.md) , .NET Framework se dodává se dvěma integrovanými zprostředkovateli členství: [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) a [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx). V takovém případě používá `SqlMembershipProvider` jako uživatelské úložiště Microsoft SQL Server databázi. Aby bylo možné tohoto poskytovatele použít v aplikaci, musíme poskytovatelem sdělit, jakou databázi použít jako úložiště. Jak je možné si představit, `SqlMembershipProvider` očekává, že databáze úložiště uživatelů má některé databázové tabulky, zobrazení a uložené procedury. Musíme do vybrané databáze přidat toto očekávané schéma.

Tento kurz začíná zkoumáním technik pro přidání potřebného schématu do databáze nástroje, aby bylo možné použít `SqlMembershipProvider`. V tomto případě probereme klíčové tabulky ve schématu a podíváme se na jejich účel a důležitost. V tomto kurzu se dozvíte, jak říct aplikaci ASP.NET, kterou by měl poskytovatel členství použít.

Pojďme začít!

## <a name="step-1-deciding-where-to-place-the-user-store"></a>Krok 1: rozhodnutí, kam umístit úložiště uživatele

Data aplikace ASP.NET se běžně ukládají v několika tabulkách v databázi. Při implementaci `SqlMembershipProvider`ho schématu databáze se musíte rozhodnout, jestli se má schéma členství umístit do stejné databáze jako data aplikace nebo do alternativní databáze.

Doporučujeme vyhledat schéma členství ve stejné databázi jako data aplikace z následujících důvodů:

- **Udržovatelnost** aplikace, jejíž data jsou zapouzdřená v jedné databázi, je snazší pochopit, udržovat a nasazovat než aplikace, která má dvě samostatné databáze.
- **Relační integrita** hledáním tabulek souvisejících s členstvím ve stejné databázi, jako jsou tabulky aplikace, je možné stanovit [omezení cizího klíče](http://en.wikipedia.org/wiki/Foreign_key) mezi primárními klíči v tabulkách souvisejících s členstvím a souvisejícími tabulkami aplikací.

Oddělit úložiště uživatele a data aplikací do samostatných databází dává smysl jenom v případě, že máte více aplikací, které jednotlivé databáze využívají samostatně, ale potřebují sdílet běžné uživatelské úložiště.

### <a name="creating-a-database"></a>Vytvoření databáze

Aplikace, kterou jsme sestavili, protože druhý kurz ještě nevyžadoval databázi. Pro úložiště uživatelů to ale budeme potřebovat. Pojďme ho vytvořit a potom do něj přidat schéma vyžadované poskytovatelem `SqlMembershipProvider` (viz krok 2).

> [!NOTE]
> V této sérii kurzů budeme k ukládání tabulek aplikací a `SqlMembershipProvider` schématu používat databázi [edice Microsoft SQL Server 2005 Express](https://msdn.microsoft.com/sql/Aa336346.aspx) . Toto rozhodnutí bylo provedeno ze dvou důvodů: první z důvodu jeho nákladu zdarma – edice Express je nejužitečnější verze SQL Server 2005; druhý SQL Server 2005 Express Edition databáze lze umístit přímo do `App_Data` složky webové aplikace, takže cinch zabalí databázi a webovou aplikaci společně v jednom souboru ZIP a znovu ji nasadí bez jakýchkoli zvláštních instrukcí pro instalaci nebo možností konfigurace. Pokud byste chtěli postupovat s použitím SQL Server verze non-Express edice, je to klidně. Postup je prakticky identický. Schéma `SqlMembershipProvider` bude fungovat s libovolnou verzí Microsoft SQL Server 2000 a.

V Průzkumník řešení klikněte pravým tlačítkem myši na složku `App_Data` a vyberte možnost Přidat novou položku. (Pokud se složka `App_Data` v projektu nezobrazí, klikněte pravým tlačítkem na projekt v Průzkumník řešení, vyberte Přidat složku ASP.NET a vyberte `App_Data`.) V dialogovém okně Přidat novou položku vyberte možnost Přidat novou SQL Database s názvem `SecurityTutorials.mdf`. V tomto kurzu přidáme schéma `SqlMembershipProvider` do této databáze. v dalších kurzech vytvoříme další tabulky pro zachycení dat aplikace.

[![přidat nový SQL Database s názvem databáze SecurityTutorials. mdf do složky App_Data](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**Obrázek 1**: přidejte novou SQL Database nazvanou `SecurityTutorials.mdf` Database do složky `App_Data` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-cs/_static/image3.png)

Přidání databáze do složky `App_Data` je automaticky obsahuje v zobrazení Průzkumník databáze. (Ve verzi aplikace Visual Studio, která není edice Express, se Průzkumník databáze nazývá Průzkumník serveru.) Přejít do Průzkumníka databáze a rozšířit právě přidanou databázi `SecurityTutorials`. Pokud nevidíte Průzkumník databáze na obrazovce, přejděte do nabídky Zobrazit a zvolte Průzkumník databáze nebo stiskněte kombinaci kláves CTRL + ALT + S. Jak ukazuje obrázek 2, `SecurityTutorials` databáze je prázdná – neobsahuje žádné tabulky, žádná zobrazení a žádné uložené procedury.

[![databáze SecurityTutorials je aktuálně prázdná.](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**Obrázek 2**: databáze `SecurityTutorials` je aktuálně prázdná ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-cs/_static/image6.png)

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>Krok 2: Přidání schématu`SqlMembershipProvider`do databáze

`SqlMembershipProvider` vyžaduje, aby byla v databázi úložiště uživatelů nainstalována konkrétní sada tabulek, zobrazení a uložených procedur. Tyto požadované objekty databáze je možné přidat pomocí [nástroje`aspnet_regsql.exe`](https://msdn.microsoft.com/library/ms229862.aspx). Tento soubor se nachází ve složce `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\`.

> [!NOTE]
> Nástroj `aspnet_regsql.exe` nabízí jak funkci příkazového řádku, tak grafické uživatelské rozhraní. Grafické rozhraní je uživatelsky přívětivější a podíváme se v tomto kurzu. Rozhraní příkazového řádku je užitečné v případě, že je nutné přidat schéma `SqlMembershipProvider` automatizovaně, například ve scénářích vytváření skriptů nebo automatizovaného testování.

Nástroj `aspnet_regsql.exe` slouží k přidání nebo odebrání *aplikačních služeb ASP.NET* do zadané SQL Server databáze. Služba ASP.NET Application Services zahrnuje schémata pro `SqlMembershipProvider` a `SqlRoleProvider`společně se schématy pro poskytovatele založené na SQL pro jiné architektury ASP.NET 2,0. Pro nástroj `aspnet_regsql.exe` musíme poskytnout dvě bity informací:

- Zda chceme přidat nebo odebrat aplikační služby a
- Databáze, ze které se má přidat nebo odebrat schéma služby Application Services

Při zobrazení výzvy k použití databáze vyzve nástroj `aspnet_regsql.exe` k zadání názvu serveru, na kterém se databáze nachází, pověření zabezpečení pro připojení k databázi a název databáze. Pokud používáte SQL Server bez verze Express, měli byste již znát tyto informace, protože se jedná o stejné informace, které je nutné poskytnout prostřednictvím připojovacího řetězce při práci s databází prostřednictvím webové stránky ASP.NET. Určení názvu serveru a databáze při použití databáze SQL Server 2005 Express Edition ve složce `App_Data`, ale o něco se podílí.

V následující části je jasné, jak zadat název serveru a databáze pro databázi SQL Server 2005 Express Edition do složky `App_Data`. Pokud nepoužíváte SQL Server 2005 Express Edition bez obav, můžete přeskočit k části instalace Aplikační služby.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>Určení názvu serveru a databáze pro databázi SQL Server 2005 Express Edition ve složce`App_Data`

Aby bylo možné použít nástroj `aspnet_regsql.exe` musíme znát název serveru a databáze. Název serveru je `localhost\InstanceName`. Nejpravděpodobněji je *instance* `SQLExpress`. Pokud jste však nainstalovali SQL Server 2005 Express Edition ručně (to znamená, že jste ho při instalaci sady Visual Studio nenainstalovali automaticky), je možné, že jste vybrali jiný název instance.

Název databáze je bitová trickier, která se má určit. Databáze ve složce `App_Data` mají typicky název databáze, který obsahuje [globálně jedinečný identifikátor](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) spolu s cestou k databázovému souboru. Aby bylo možné přidat schéma služby Application Services pomocí `aspnet_regsql.exe`, je potřeba určit tento název databáze.

Nejjednodušší způsob, jak zjistit název databáze, je prozkoumávat ji pomocí SQL Server Management Studio. SQL Server Management Studio poskytuje grafické rozhraní pro správu databází SQL Server 2005, ale nedodává se s edicí Express verze SQL Server 2005. Dobrá zpráva je, že si [můžete stáhnout](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) bezplatnou verzi Express SQL Server Management Studio.

> [!NOTE]
> Pokud máte na počítači nainstalovanou verzi SQL Server 2005, která není edice Express Express, je pravděpodobně nainstalovaná plná verze Management Studio. Pomocí úplné verze můžete určit název databáze podle stejných kroků, jak je uvedeno níže pro edici Express.

Začněte zavřením sady Visual Studio, abyste zajistili, že všechny zámky, které Visual Studio zaručí v souboru databáze, se zavřou. V dalším kroku spusťte SQL Server Management Studio a připojte se k databázi `localhost\InstanceName` pro SQL Server 2005 Express Edition. Jak bylo uvedeno dříve, je pravděpodobné, že je název instance `SQLExpress`. Jako možnost ověřování vyberte ověřování systému Windows.

[![připojení k instanci SQL Server 2005 Express Edition](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**Obrázek 3**: Připojte se k instanci SQL Server 2005 Express Edition ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-cs/_static/image9.png)

Po připojení k instanci SQL Server 2005 Express Edition Management Studio zobrazí složky pro databáze, nastavení zabezpečení, objekty serveru atd. Pokud rozbalíte kartu databáze, zjistíte, že `SecurityTutorials.mdf` *databáze není zaregistrovaná* v instanci databáze. je potřeba nejdřív připojit databázi.

Klikněte pravým tlačítkem na složku databáze a v místní nabídce vyberte připojit. Tím se zobrazí dialogové okno připojit databáze. Odsud klikněte na tlačítko Přidat, přejděte do databáze `SecurityTutorials.mdf` a klikněte na OK. Obrázek 4: po výběru databáze `SecurityTutorials.mdf` se zobrazí dialogové okno připojit databáze. Po úspěšném připojení databáze se na obrázku 5 zobrazuje Průzkumník objektů Management Studio.

[![připojit databázi SecurityTutorials. mdf](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**Obrázek 4**: připojení databáze `SecurityTutorials.mdf` ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-cs/_static/image12.png))

[![se databáze SecurityTutorials. mdf zobrazí ve složce databáze.](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**Obrázek 5**: `SecurityTutorials.mdf` databáze se zobrazí ve složce databáze ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-cs/_static/image15.png)

Jak ukazuje obrázek 5, `SecurityTutorials.mdf` databáze má místo názvu abstruse. Pojďme změnit na srozumitelnější (a jednodušší typ) názvu. Klikněte pravým tlačítkem na databázi, v místní nabídce vyberte Přejmenovat a přejmenujte ji `SecurityTutorialsDatabase`. Tento název souboru se nezmění, stačí pouze název, který databáze používá k identifikaci SQL Server.

[![přejmenovat databázi na SecurityTutorialsDatabase](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**Obrázek 6**: Přejmenování databáze na `SecurityTutorialsDatabase`([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-cs/_static/image18.png))

V tomto okamžiku víme, že název serveru a databáze pro soubor `SecurityTutorials.mdf` databáze: `localhost\InstanceName` a `SecurityTutorialsDatabase`, v uvedeném pořadí. Nyní jsme připraveni nainstalovat aplikační služby prostřednictvím nástroje `aspnet_regsql.exe`.

### <a name="installing-the-application-services"></a>Instalace Aplikační služby

Chcete-li spustit nástroj `aspnet_regsql.exe`, přejděte do nabídky Start a vyberte možnost spustit. Do textového pole zadejte `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe` a klikněte na OK. Případně můžete pomocí Průzkumníka Windows přejít k podrobnostem do příslušné složky a dvakrát kliknout na soubor `aspnet_regsql.exe`. Při obou přístupech dojde k rozhledání stejných výsledků.

Spuštění nástroje `aspnet_regsql.exe` bez argumentů příkazového řádku spustí grafické uživatelské rozhraní Průvodce nastavením služby ASP.NET SQL Server. Průvodce usnadňuje přidání nebo odebrání aplikačních služeb ASP.NET v zadané databázi. První obrazovka průvodce, zobrazená na obrázku 7, popisuje účel tohoto nástroje.

[![použít Průvodce nastavením SQL Server ASP.NET k přidání schématu členství](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**Obrázek 7**: pomocí průvodce instalací SQL Server ASP.NET můžete přidat schéma členství ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-cs/_static/image21.png)

Druhý krok v Průvodci vás zeptá, jestli chceme přidat aplikační služby nebo je odebrat. Vzhledem k tomu, že chceme přidat tabulky, zobrazení a uložené procedury, které jsou nezbytné pro `SqlMembershipProvider`, vyberte možnost konfigurovat SQL Server pro aplikační služby. Pokud později chcete toto schéma z databáze odebrat, spusťte tohoto průvodce znovu, ale místo toho vyberte možnost odebrat informace o službě aplikace z existující databáze.

[![vyberte možnost konfigurovat SQL Server pro Aplikační služby.](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**Obrázek 8**: vyberte možnost konfigurovat SQL Server pro aplikační služby ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-cs/_static/image24.png)).

Třetí krok vás vyzve k zadání informací o databázi: název serveru, ověřovací informace a název databáze. Pokud jste spolu s tímto kurzem pojmenovali a Přidali jste databázi `SecurityTutorials.mdf` do `App_Data`, připojili ji k `localhost\InstanceName`a přejmenovali ji na `SecurityTutorialsDatabase`, použijte následující hodnoty:

- Server: `localhost\InstanceName`
- Ověřování systému Windows
- Databáze: `SecurityTutorialsDatabase`

[![zadejte informace o databázi.](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**Obrázek 9**: zadání informací o databázi ([kliknutím zobrazíte obrázek v plné velikosti](creating-the-membership-schema-in-sql-server-cs/_static/image27.png))

Po zadání informací o databázi klikněte na další. Poslední krok shrnuje kroky, které se provedou. Kliknutím na tlačítko Další nainstalujte aplikační služby a pak dokončete průvodce.

> [!NOTE]
> Pokud jste použili Management Studio k připojení databáze a přejmenování souboru databáze, nezapomeňte před znovu otevřením sady Visual Studio odpojit databázi a zavřít Management Studio. Pokud chcete odpojit databázi `SecurityTutorialsDatabase`, klikněte pravým tlačítkem na název databáze a v nabídce úlohy vyberte Odpojit.

Po dokončení průvodce se vraťte do sady Visual Studio a přejděte do Průzkumníka databáze. Rozbalte složku tabulky. Měla by se zobrazit řada tabulek, jejichž názvy začínají předponou `aspnet_`. Podobně je možné najít řadu zobrazení a uložených procedur ve složkách zobrazení a uložené procedury. Tyto databázové objekty tvoří schéma služby Application Services. V kroku 3 prověříme objekty databáze pro členství a pro konkrétní role.

[do databáze bylo přidáno ![nejrůznějších tabulek, zobrazení a uložených procedur.](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**Obrázek 10**: do databáze se přidala celá řada tabulek, zobrazení a uložených procedur ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-cs/_static/image30.png)

> [!NOTE]
> Grafické uživatelské rozhraní nástroje pro `aspnet_regsql.exe` nainstaluje celé schéma služby Application Services. Ale při provádění `aspnet_regsql.exe` z příkazového řádku můžete určit, jaké konkrétní součásti aplikačních služeb nainstalovat (nebo odebrat). Proto pokud chcete přidat pouze tabulky, zobrazení a uložené procedury, které jsou nezbytné pro poskytovatele `SqlMembershipProvider` a `SqlRoleProvider`, spusťte `aspnet_regsql.exe` z příkazového řádku. Alternativně můžete ručně spustit příslušnou podmnožinu T-SQL Create Scripts, kterou používá `aspnet_regsql.exe`. Tyto skripty se nacházejí ve složce `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` s názvy jako `InstallCommon.sql`,`InstallMembership.sql`,`InstallRoles.sql`, `InstallProfile.sql`,`InstallSqlState.sql`atd.

V tuto chvíli jsme vytvořili databázové objekty, které potřebuje `SqlMembershipProvider`. Pořád ale potřebujeme instruovat rozhraní pro členství, které by mělo používat `SqlMembershipProvider` (vs, `ActiveDirectoryMembershipProvider`) a jestli má `SqlMembershipProvider` používat databázi `SecurityTutorials`. Podíváme se na to, jak určit poskytovatele, který se má použít, a jak přizpůsobit nastavení vybraného poskytovatele v kroku 4. Nejdřív se podíváme na objekty databáze, které jste právě vytvořili.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>Krok 3: Prohlédněte si základní tabulky schématu

Při práci s architekturou členství a rolí v aplikaci ASP.NET jsou podrobnosti implementace zapouzdřeny zprostředkovatelem. V budoucích kurzech budeme rozhraní s těmito rozhraními používat prostřednictvím tříd .NET Framework `Membership` a `Roles`. Pokud používáte tato rozhraní API na vysoké úrovni, nemusíte se v dodržovali s podrobnostmi na nízké úrovni, jako jsou třeba dotazy, které jsou spouštěny nebo které tabulky upravují `SqlMembershipProvider` a `SqlRoleProvider`.

V tomto případě jsme mohli bez obav použít rámec členství a rolí, aniž byste prozkoumali schéma databáze vytvořené v kroku 2. Při vytváření tabulek pro ukládání aplikačních dat ale můžeme potřebovat vytvořit entity, které se vztahují na uživatele nebo role. Pomáhá znát `SqlMembershipProvider` a `SqlRoleProvider` schémat při určování omezení cizího klíče mezi tabulkami dat aplikace a tabulkami vytvořenými v kroku 2. Kromě toho může být někdy nutné použít rozhraní s uživateli a rolemi role přímo na úrovni databáze (místo přes `Membership` nebo `Roles` třídy).

### <a name="partitioning-the-user-store-into-applications"></a>Rozdělení uživatelského úložiště do aplikací

Rozhraní pro členství a role jsou navržena tak, aby bylo možné sdílet jediné úložiště uživatelů a rolí mezi mnoha různými aplikacemi. Aplikace ASP.NET, která používá rámec členství nebo rolí, musí určovat, který oddíl aplikace se má použít. V krátkém případě může více webových aplikací používat stejné úložiště uživatelů a rolí. Obrázek 11 znázorňuje úložiště uživatelů a rolí, která jsou rozdělená na tři aplikace: HRSite, CustomerSite a SalesSite. Každá z těchto tří webových aplikací má své vlastní jedinečné uživatele a role, ale všechny fyzicky ukládají informace o uživatelských účtech a rolích ve stejných databázových tabulkách.

[Uživatelské účty ![můžou být rozdělené mezi několik aplikací.](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**Obrázek 11**: uživatelské účty můžou být rozdělené mezi více aplikací ([kliknutím zobrazíte obrázek v plné velikosti).](creating-the-membership-schema-in-sql-server-cs/_static/image33.png)

V tabulce `aspnet_Applications` se tyto oddíly definují. Každá aplikace, která používá databázi k ukládání informací o uživatelském účtu, je reprezentována řádkem v této tabulce. Tabulka `aspnet_Applications` má čtyři sloupce: `ApplicationId`, `ApplicationName`, `LoweredApplicationName`a `Description`. `ApplicationId` je typu [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) a je to primární klíč tabulky; `ApplicationName` poskytuje jedinečný popisný název pro každou aplikaci.

Ostatní tabulky vztahující se k členství a rolím odkazují zpátky na pole `ApplicationId` v `aspnet_Applications`. Například tabulka `aspnet_Users`, která obsahuje záznam pro každý uživatelský účet, má pole `ApplicationId` cizího klíče; Ditto pro tabulku `aspnet_Roles`. Pole `ApplicationId` v těchto tabulkách určuje oddíl aplikace, ke kterému patří uživatelský účet nebo role.

### <a name="storing-user-account-information"></a>Ukládání informací o uživatelském účtu

Informace o uživatelském účtu jsou umístěné ve dvou tabulkách: `aspnet_Users` a `aspnet_Membership`. Tabulka `aspnet_Users` obsahuje pole, která obsahují základní informace o uživatelském účtu. Tři nejvíce relevantní sloupce jsou:

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` je primární klíč (a typu `uniqueidentifier`). `UserName` je typu `nvarchar(256)` a společně s heslem vytvoří přihlašovací údaje uživatele. (Heslo uživatele je uloženo v `aspnet_Membership` tabulce.) `ApplicationId` propojí uživatelský účet s konkrétní aplikací v `aspnet_Applications`. Ve sloupcích `UserName` a `ApplicationId` je [omezení složené`UNIQUE`](https://msdn.microsoft.com/library/ms191166.aspx) . To zajišťuje, že v dané aplikaci je každé uživatelské jméno jedinečné, ale umožňuje použití stejného `UserName` v různých aplikacích.

Tabulka `aspnet_Membership` obsahuje další informace o uživatelském účtu, například heslo, e-mailovou adresu, datum posledního přihlášení a jejich dobu a tak dále. Mezi záznamy v tabulkách `aspnet_Users` a `aspnet_Membership` existuje korespondence 1:1. Tento vztah je zajištěný polem `UserId` v `aspnet_Membership`, které slouží jako primární klíč tabulky. Podobně jako u `aspnet_Users` tabulky zahrnuje `aspnet_Membership` pole `ApplicationId`, které spojuje tyto informace s konkrétním oddílem aplikace.

### <a name="securing-passwords"></a>Zabezpečení hesel

Informace o heslech jsou uloženy v `aspnet_Membership` tabulce. `SqlMembershipProvider` umožňuje ukládat hesla do databáze pomocí jedné z následujících tří postupů:

- **Clear** – heslo je uloženo v databázi jako prostý text. Tuto možnost rozhodně neodrazí. Pokud je databáze ohrožená hackerem, který vyhledává zadní vrátka nebo Disgruntled zaměstnanec, který má přístup k databázi, jsou k dispozici pouze pověření jednotlivých uživatelů.
- **Hash** – hesla se používají pomocí jednosměrného algoritmu hash a náhodně generované hodnoty Salt. Tato hodnota hash (spolu s hodnotou Salt) je uložená v databázi.
- **Šifrované** – zašifrovaná verze hesla je uložená v databázi.

Použitá technika úložiště hesla závisí na nastaveních `SqlMembershipProvider` určených v `Web.config`. Podíváme se na přizpůsobení nastavení `SqlMembershipProvider` v kroku 4. Výchozím chováním je uložení hodnoty hash hesla.

Sloupce zodpovědné za uložení hesla jsou `Password`, `PasswordFormat`a `PasswordSalt`. `PasswordFormat` je pole typu `int` jehož hodnota označuje techniku použitou pro uložení hesla: 0 pro vymazání. 1 pro algoritmus hash; 2 pro šifrování. `PasswordSalt` je přiřazen náhodně generovaný řetězec bez ohledu na použitou techniku úložiště hesla; hodnota `PasswordSalt` se používá jenom při výpočtu hodnoty hash hesla. A konečně sloupec `Password` obsahuje skutečná data o heslech, jedná se o heslo pro heslo, hodnotu hash hesla nebo šifrované heslo.

Tabulka 1 znázorňuje, jaké tři sloupce můžou vypadat jako u různých technik úložiště při ukládání hesla MySecret! .

| **Technika úložiště&lt;\_o3a\_p/&gt;** | **Heslo&lt;\_o3a\_p/&gt;** | **PasswordFormat&lt;\_o3a\_p/&gt;** | **PasswordSalt&lt;\_o3a\_p/&gt;** |
| --- | --- | --- | --- |
| Vymazat | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| Rozdělí | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| Šifrovaná | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/AA/oqAXGLHJNBw = = |

**Tabulka 1**: příklad hodnot polí souvisejících s heslem při ukládání hesla MySecret!

> [!NOTE]
> Konkrétní šifrovací algoritmus nebo algoritmus hash používaný `SqlMembershipProvider` jsou určeny nastavením v elementu `<machineKey>`. Tento prvek konfigurace jsme probrali v kroku 3 <a id="Tutorial3"> </a>kurzu [*Konfigurace ověřování formulářů a Pokročilá témata*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) .

### <a name="storing-roles-and-role-associations"></a>Ukládání rolí a přidružení rolí

Rozhraní role umožňují vývojářům definovat sadu rolí a určit, co uživatelé patří k rolím. Tyto informace jsou zachyceny v databázi prostřednictvím dvou tabulek: `aspnet_Roles` a `aspnet_UsersInRoles`. Každý záznam v `aspnet_Roles` tabulce představuje roli konkrétní aplikace. Podobně jako u `aspnet_Users` tabulky má `aspnet_Roles` tabulka tři sloupce, které jsou relevantní pro naši diskuzi:

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` je primární klíč (a typu `uniqueidentifier`). `RoleName` je typu `nvarchar(256)`. A `ApplicationId` propojí uživatelský účet s konkrétní aplikací v `aspnet_Applications`. Pro sloupce `RoleName` a `ApplicationId` existuje omezení složené `UNIQUE`, které zajišťuje, že v dané aplikaci je název každé role jedinečný.

Tabulka `aspnet_UsersInRoles` slouží jako mapování mezi uživateli a rolemi. K dispozici jsou pouze dva sloupce – `UserId` a `RoleId` a dohromady tvoří složený primární klíč.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>Krok 4: určení poskytovatele a přizpůsobení jeho nastavení

Všechny architektury, které podporují model poskytovatele – jako jsou například rozhraní pro členství a role – neobsahují detaily implementace samy a místo toho deleguje tuto zodpovědnost na třídu poskytovatele. V případě rozhraní členství definuje třída `Membership` rozhraní API pro správu uživatelských účtů, ale nekomunikuje přímo s žádným uživatelským úložištěm. Místo toho metody třídy `Membership` předají požadavek nakonfigurovanému poskytovateli – budeme používat `SqlMembershipProvider`. Když vyvoláme jednu z metod ve třídě `Membership`, jak by rozhraní členství znalo delegování volání do `SqlMembershipProvider`?

Třída `Membership` má [vlastnost`Providers`](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) , která obsahuje odkaz na všechny třídy registrovaných zprostředkovatelů, které jsou k dispozici pro použití v rámci architektury členství. Každý registrovaný zprostředkovatel má přidružené jméno a typ. Název nabízí uživatelsky přívětivý způsob, jak odkazovat na určitého poskytovatele v kolekci `Providers`, zatímco typ identifikuje třídu poskytovatele. Každý registrovaný zprostředkovatel navíc může obsahovat nastavení konfigurace. Nastavení konfigurace pro rámec členství zahrnuje `passwordFormat` a `requiresUniqueEmail`, mezi mnoho dalších. Úplný seznam konfiguračních nastavení používaných `SqlMembershipProvider`najdete v tabulce 2.

Obsah vlastnosti `Providers` se určuje prostřednictvím nastavení konfigurace webové aplikace. Ve výchozím nastavení mají všechny webové aplikace poskytovatele s názvem `AspNetSqlMembershipProvider` typu `SqlMembershipProvider`. Tento výchozí zprostředkovatel členství je zaregistrován v `machine.config` (nachází se na `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)`:

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

Jak ukazuje kód uvedený výše, [prvek`<membership>`](https://msdn.microsoft.com/library/1b9hw62f.aspx) definuje nastavení konfigurace pro rozhraní členství, zatímco [`<providers>` podřízený prvek](https://msdn.microsoft.com/library/6d4936ht.aspx) určuje registrované zprostředkovatele. Poskytovatelé mohou být přidáni nebo odebráni pomocí [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) nebo [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) prvky; pomocí elementu [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) odeberte všechny aktuálně registrované zprostředkovatele. Jak ukazuje výše uvedený kód, `machine.config` přidá poskytovatele s názvem `AspNetSqlMembershipProvider` typu `SqlMembershipProvider`.

Kromě atributů `name` a `type` obsahuje element `<add>` atributy, které definují hodnoty pro různá nastavení konfigurace. Tabulka 2 uvádí dostupná nastavení konfigurace specifická pro `SqlMembershipProvider`, spolu s popisem každého z nich.

> [!NOTE]
> Všechny výchozí hodnoty zaznamenané v tabulce 2 odkazují na výchozí hodnoty definované ve třídě `SqlMembershipProvider`. Všimněte si, že ne všechna nastavení konfigurace v `AspNetSqlMembershipProvider` odpovídat výchozím hodnotám `SqlMembershipProvider` třídy. Pokud není například zadáno ve zprostředkovateli členství, výchozí nastavení `requiresUniqueEmail` má hodnotu true. `AspNetSqlMembershipProvider` však tuto výchozí hodnotu přepíše tím, že explicitně zadáte hodnotu `false`.

| **Nastavení&lt;\_o3a\_p/&gt;** | **Popis&lt;\_o3a\_p/&gt;** |
| --- | --- |
| `ApplicationName` | Odvolání, že rozhraní členství umožňuje rozdělit jednotlivé úložiště uživatelů na oddíly mezi více aplikacemi. Toto nastavení označuje název oddílu aplikace používaného poskytovatelem členství. Pokud tato hodnota není explicitně zadána, je nastavena za běhu na hodnotu pro virtuální kořenovou cestu aplikace. |
| `commandTimeout` | Určuje hodnotu časového limitu příkazu SQL (v sekundách). Výchozí hodnota je 30. |
| `connectionStringName` | Název připojovacího řetězce v prvku `<connectionStrings>`, který se má použít pro připojení k databázi úložiště uživatele. Tato hodnota je povinná. |
| `description` | Poskytuje uživatelsky přívětivý popis zaregistrovaného poskytovatele. |
| `enablePasswordRetrieval` | Určuje, jestli uživatelé můžou načítat zapomenuté heslo. Výchozí hodnota je `false`. |
| `enablePasswordReset` | Určuje, jestli uživatelé můžou resetovat svoje heslo. Výchozí hodnota je `true`. |
| `maxInvalidPasswordAttempts` | Maximální počet neúspěšných pokusů o přihlášení, které se mohou vyskytnout pro daného uživatele během zadaného `passwordAttemptWindow`, než bude uživatel uzamčen. Výchozí hodnota je 5. |
| `minRequiredNonalphanumericCharacters` | Minimální počet nealfanumerických znaků, které se musí objevit v uživatelském hesle. Tato hodnota musí být v rozmezí od 0 do 128. Výchozí hodnota je 1. |
| `minRequiredPasswordLength` | Minimální počet znaků vyžadovaných v hesle. Tato hodnota musí být v rozmezí od 0 do 128. Výchozí hodnota je 7. |
| `name` | Název zaregistrovaného poskytovatele. Tato hodnota je povinná. |
| `passwordAttemptWindow` | Počet minut, během kterých jsou sledovány neúspěšné pokusy o přihlášení Pokud uživatel zadá neplatné přihlašovací údaje `maxInvalidPasswordAttempts` časy v rámci tohoto zadaného okna, budou uzamčeny. Výchozí hodnota je 10. |
| `PasswordFormat` | Formát úložiště hesla: `Clear`, `Hashed`nebo `Encrypted`. Výchozí hodnota je `Hashed`. |
| `passwordStrengthRegularExpression` | Pokud je tento regulární výraz k dispozici, slouží k vyhodnocení síly vybraného hesla uživatele při vytváření nového účtu nebo při změně hesla. Výchozí hodnota je prázdný řetězec. |
| `requiresQuestionAndAnswer` | Určuje, jestli uživatel musí při načítání nebo resetování hesla odpovědět na jeho bezpečnostní otázku. Výchozí hodnota je `true`. |
| `requiresUniqueEmail` | Uvádí, zda všechny uživatelské účty v daném oddílu aplikace musí mít jedinečnou e-mailovou adresu. Výchozí hodnota je `true`. |
| `type` | Určuje typ poskytovatele. Tato hodnota je povinná. |

**Tabulka 2**: nastavení konfigurace členství a `SqlMembershipProvider`

Kromě `AspNetSqlMembershipProvider`mohou být jiní poskytovatelé členství zaregistrovaní na základě aplikace tak, že do `Web.config` souboru přidají podobný kód.

> [!NOTE]
> Architektura rolí funguje v podstatě stejným způsobem: v `machine.config` je výchozí registrovaný zprostředkovatel rolí a registrovaní poskytovatelé můžou být přizpůsobeni na základě aplikace v `Web.config`. V budoucím kurzu podíváme se na podrobné informace o architektuře rolí a o konfiguraci.

### <a name="customizing-thesqlmembershipprovidersettings"></a>Přizpůsobení nastavení`SqlMembershipProvider`

Výchozí `SqlMembershipProvider` (`AspNetSqlMembershipProvider`) má atribut `connectionStringName` nastaven na `LocalSqlServer`. Podobně jako poskytovatel `AspNetSqlMembershipProvider` je `LocalSqlServer` název připojovacího řetězce definovaný v `machine.config`.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

Jak vidíte, tento připojovací řetězec definuje databázi edice SQL 2005 Express v umístění | DataDirectory | Aspnetdb. mdf. Řetězec | DataDirectory | se převede za běhu tak, aby odkazovaly na adresář `~/App_Data/`, takže cesta k databázi | DataDirectory | Aspnetdb. mdf "překládá `~/App_Data`/`aspnet.mdf`.

Pokud v souboru `Web.config` aplikace neurčíme žádné informace o poskytovateli členství, aplikace použije výchozího registrovaného poskytovatele členství `AspNetSqlMembershipProvider`. Pokud databáze `~/App_Data/aspnet.mdf` neexistuje, modul runtime ASP.NET ho automaticky vytvoří a přidá schéma služby Application Services. Nechci ale používat databázi `aspnet.mdf`; místo toho chceme použít databázi `SecurityTutorials.mdf`, kterou jsme vytvořili v kroku 2. Tuto úpravu lze provést jedním ze dvou způsobů:

- <strong>Zadejte hodnotu pro</strong> <strong>název připojovacího řetězce`LocalSqlServer`v</strong> <strong>`Web.config`</strong> <strong>.</strong> Přepsáním hodnoty názvu připojovacího řetězce `LocalSqlServer` v `Web.config`můžeme použít výchozího registrovaného poskytovatele členství (`AspNetSqlMembershipProvider`) a správně pracovat s databází `SecurityTutorials.mdf`. Tento přístup je v případě, že se jedná o obsah s nastavením konfigurace určeným `AspNetSqlMembershipProvider`, přesně. Další informace o této technice najdete v příspěvku na blogu [Scott Guthrie](https://weblogs.asp.net/scottgu/), [konfigurace ASP.NET 2,0 Aplikační služby pro použití SQL Server 2000 nebo SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- <strong>Přidejte nového registrovaného poskytovatele typu</strong> <strong>`SqlMembershipProvider`</strong> <strong>a nakonfigurujte jeho</strong> nastavení<strong>`connectionStringName`</strong> <strong>tak, aby odkazovalo</strong> na databázi<strong>`SecurityTutorials.mdf`</strong> <strong>.</strong> Tento přístup je užitečný ve scénářích, kdy chcete kromě připojovacího řetězce databáze upravit i další vlastnosti konfigurace. V mých vlastních projektech tento přístup vždycky používám z důvodu jeho flexibility a čitelnosti.

Předtím, než můžeme přidat nového registrovaného poskytovatele, který odkazuje na databázi `SecurityTutorials.mdf`, musíme nejdřív do části `<connectionStrings>` v `Web.config`přidat odpovídající hodnotu připojovacího řetězce. Následující kód přidá nový připojovací řetězec s názvem `SecurityTutorialsConnectionString`, který odkazuje na databázi SQL Server 2005 Express Edition `SecurityTutorials.mdf` ve složce `App_Data`.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> Pokud používáte alternativní databázový soubor, podle potřeby aktualizujte připojovací řetězec. Další informace o vytváření správného připojovacího řetězce najdete v tématu [connectionStrings.com](http://www.connectionstrings.com/).

Dále přidejte do souboru `Web.config` následující označení konfigurace členství. Tento kód zaregistruje nového poskytovatele s názvem `SecurityTutorialsSqlMembershipProvider`.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

Kromě registrace poskytovatele `SecurityTutorialsSqlMembershipProvider` definuje výše uvedený `SecurityTutorialsSqlMembershipProvider` jako výchozího zprostředkovatele (prostřednictvím atributu `defaultProvider` v elementu `<membership>`). Odvolání, že rozhraní členství může mít více registrovaných zprostředkovatelů. Vzhledem k tomu, že `AspNetSqlMembershipProvider` je zaregistrován jako první poskytovatel v `machine.config`, slouží jako výchozí zprostředkovatel, pokud neurčíte jinak.

V současné době má naše aplikace dva registrované zprostředkovatele: `AspNetSqlMembershipProvider` a `SecurityTutorialsSqlMembershipProvider`. Před registrací poskytovatele `SecurityTutorialsSqlMembershipProvider` však můžeme vymazal všechny dřív registrované zprostředkovatele přidáním [`<clear />` elementu](https://msdn.microsoft.com/library/t062y6yc.aspx) bezprostředně před `<add>` element. Tím se vymaže `AspNetSqlMembershipProvider` ze seznamu registrovaných zprostředkovatelů, což znamená, že `SecurityTutorialsSqlMembershipProvider` by to byl jediný registrovaný poskytovatel členství. Pokud jsme tento přístup použili, nemuseli jsme `SecurityTutorialsSqlMembershipProvider` jako výchozího poskytovatele označit jako výchozího zprostředkovatele, protože by to byl jediný registrovaný poskytovatel členství. Další informace o používání `<clear />`najdete v tématu [použití `<clear />` při přidávání zprostředkovatelů](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx).

Všimněte si, že nastavení `connectionStringName` `SecurityTutorialsSqlMembershipProvider`odkazuje na název připojovacího řetězce, který je právě přidaný `SecurityTutorialsConnectionString`, a že jeho `applicationName` nastavení bylo nastaveno na hodnotu SecurityTutorials. Kromě toho nastavení `requiresUniqueEmail` bylo nastaveno na `true`. Všechny ostatní možnosti konfigurace se shodují s hodnotami v `AspNetSqlMembershipProvider`. Pokud chcete, můžete tady dělat jakékoli změny konfigurace. Například můžete zvýšit sílu hesla vyžadováním dvou než alfanumerických znaků místo jednoho nebo zvýšením délky hesla na osm znaků namísto sedmi.

> [!NOTE]
> Odvolání, že rozhraní členství umožňuje rozdělit jednotlivé úložiště uživatelů na oddíly mezi více aplikacemi. Nastavení `applicationName` poskytovatele členství indikuje, jaká aplikace poskytovatel používá při práci s úložištěm uživatele. Je důležité, abyste explicitně nastavili hodnotu pro nastavení konfigurace `applicationName`, protože pokud `applicationName` není explicitně nastaven, je při spuštění přiřazená k virtuální kořenové cestě webové aplikace. To funguje, pokud se nemění virtuální kořenová cesta aplikace, ale pokud přesunete aplikaci na jinou cestu, nastavení `applicationName` se změní také. Pokud k tomu dojde, zprostředkovatel členství začne pracovat s jiným oddílem aplikace, než se dřív používal. Uživatelské účty vytvořené před přesunem se budou nacházet v jiném oddílu aplikace a uživatelé se už nebudou moct k lokalitě přihlašovat. Podrobnější diskusi k této problematice najdete v tématu [vždy nastavte vlastnost `applicationName` při konfiguraci členství v ASP.NET 2,0 a dalších zprostředkovatelů](https://weblogs.asp.net/scottgu/443634).

## <a name="summary"></a>Přehled

V tuto chvíli máme databázi s nakonfigurovanými aplikačními službami (`SecurityTutorials.mdf`) a nakonfigurovali jsme naši webovou aplikaci tak, aby rozhraní členství používalo poskytovatele `SecurityTutorialsSqlMembershipProvider`, kterého jsme právě zaregistrovali. Tento registrovaný zprostředkovatel je typu `SqlMembershipProvider` a má `connectionStringName` nastaven na příslušný připojovací řetězec (`SecurityTutorialsConnectionString`) a explicitně nastavenou hodnotu `applicationName`.

Nyní jsme připraveni použít rozhraní pro členství z naší aplikace. V dalším kurzu podíváme se, jak vytvořit nové uživatelské účty. Po prozkoumání ověření uživatelů, provádění ověřování na základě uživatelů a ukládání dalších informací souvisejících s uživatelem do databáze.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Při konfiguraci členství v ASP.NET 2,0 a dalších zprostředkovatelích vždycky nastavit vlastnost `applicationName`](https://weblogs.asp.net/scottgu/443634)
- [Konfigurace ASP.NET 2,0 Aplikační služby pro použití SQL Server 2000 nebo SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [Stáhnout SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [Zkoumání členství, rolí a profilů v ASP.NET 2,0 s](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Element `<add>` pro poskytovatele pro členství](https://msdn.microsoft.com/library/whae3t94.aspx)
- [Element `<membership>`](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [Element `<providers>` pro členství](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [Použití `<clear />` při přidávání zprostředkovatelů](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [Práce přímo s `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Výukové video o tématech obsažených v tomto kurzu

- [Principy členství v ASP.NET](../../../videos/authentication/understanding-aspnet-memberships.md)
- [Konfigurace SQL kvůli spolupráci se schématy členství](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [Změna nastavení členství ve výchozím schématu členství](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Alicja Maziarz. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com).

> [!div class="step-by-step"]
> [Next](creating-user-accounts-cs.md)
