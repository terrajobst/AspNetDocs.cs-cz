---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 'Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: nasazení SQL Server Compact databází – 2 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: 56ceabc79947967846d342354fd033510be5f05a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568115"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: nasazení SQL Server Compact databází – 2 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak nastavit dvě databáze SQL Server Compact a databázový stroj pro nasazení.

Pro přístup k databázi vyžaduje aplikace Contoso University následující software, který musí být nasazený s aplikací, protože není zahrnutý v .NET Framework:

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) (databázový stroj).
- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (umožňující systému členství v ASP.NET použít SQL Server Compact)
- [Entity Framework 5,0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)(Code First s migracemi).

Také je nutné nasadit strukturu databáze a některé (ne všechny) dat v obou databázích aplikace. Při vývoji aplikace se obvykle zadávají testovací data do databáze, kterou nechcete nasadit na živý Web. Můžete ale také zadat některá provozní data, která chcete nasadit. V tomto kurzu nakonfigurujete projekt společnosti Contoso University tak, aby byl při nasazení zahrnut požadovaný software a správná data.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Compact versus SQL Server Express

Ukázková aplikace používá SQL Server Compact 4,0. Tento databázový stroj je relativně nová možnost pro weby. starší verze SQL Server Compact nefungují v prostředí pro hostování webů. SQL Server Compact nabízí několik výhod v porovnání s častější scénáří vývoje pomocí SQL Server Express a nasazení na celou SQL Server. V závislosti na tom, jaký poskytovatel hostingu zvolíte, může být SQL Server Compact pro nasazení levnější, protože někteří poskytovatelé se za podporu celé databáze SQL Server účtují zvlášť. Pro SQL Server Compact se neúčtují žádné další poplatky, protože databázový stroj můžete nasadit jako součást webové aplikace.

Měli byste si však být vědomi i jejich omezení. SQL Server Compact nepodporuje uložené procedury, triggery, zobrazení nebo replikaci. (Úplný seznam SQL Serverch funkcí, které nepodporují SQL Server Compact, najdete v tématu [rozdíly mezi SQL Server Compact a SQL Server](https://msdn.microsoft.com/library/bb896140.aspx).) Kromě toho některé nástroje, které můžete použít k manipulaci s schématy a daty v SQL Server Express a SQL Server databáze nefungují s SQL Server Compact. Například nemůžete použít nástroje SQL Server Management Studio nebo SQL Server Data Tools v aplikaci Visual Studio s databázemi SQL Server Compact. Máte k dispozici další možnosti pro práci s SQL Server Compact databázemi:

- Můžete použít Průzkumník serveru v aplikaci Visual Studio, která nabízí omezené funkce manipulace s databází pro SQL Server Compact.
- Můžete použít funkci manipulace s databází [WebMatrix](https://www.microsoft.com/web/webmatrix/), která má více funkcí než Průzkumník serveru.
- Můžete použít relativně plně vybavené nástroje třetích stran nebo open source nástroje, jako jsou [SQL Server Compact nástrojů](https://github.com/ErikEJ/SqlCeToolbox) a [SQL Compact data a nástroj skriptu schématu](https://github.com/ErikEJ/SqlCeToolbox).
- Můžete napsat a spustit vlastní skripty DDL (Data Definition Language), abyste mohli manipulovat se schématem databáze.

Můžete začít s SQL Server Compact a pak upgradovat později podle potřeb vývoje. V dalších kurzech v této sérii se dozvíte, jak migrovat z SQL Server Compact do SQL Server Express a SQL Server. Pokud však vytváříte novou aplikaci a očekáváte, že budete potřebovat SQL Server v blízké budoucnosti, je pravděpodobně nejlepší začít s SQL Server nebo SQL Server Express.

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>Konfigurace databázového stroje SQL Server Compact pro nasazení

Software vyžadovaný pro přístup k datům v aplikaci Contoso University byl přidán instalací následujících balíčků NuGet:

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System. Web. Providers](http://nuget.org/List/Packages/System.Web.Providers) (ASP.NET Universal Providers)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework. SqlServerCompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

Odkazy odkazují na aktuální verze těchto balíčků, které mohou být novější než ty, které jsou nainstalovány v počátečním projektu, který jste si stáhli pro účely tohoto kurzu. Pro nasazení pro poskytovatele hostingu se ujistěte, že používáte Entity Framework 5,0 nebo novější. Starší verze Migrace Code First vyžadují úplný vztah důvěryhodnosti a u mnoha poskytovatelů hostingu, které vaše aplikace bude běžet ve středním vztahu důvěryhodnosti. Další informace o střední důvěryhodnosti najdete v kurzu [nasazení do služby IIS jako testovací prostředí](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) .

Instalace balíčku NuGet se obecně postará o všechno, co potřebujete k nasazení tohoto softwaru s aplikací. V některých případech zahrnuje úlohy, jako je například změna souboru Web. config a přidání skriptů prostředí PowerShell, které se spustí při každém sestavení řešení. **Pokud chcete přidat podporu pro některé z těchto funkcí (například SQL Server Compact a Entity Framework) bez použití NuGet, ujistěte se, že víte, jakou instalaci balíčku NuGet provede, abyste mohli stejnou práci provést ručně.**

Existuje jedna výjimka, kdy NuGet nebere v úvahu všechno, co musíte udělat, abyste zajistili úspěšné nasazení. Balíček NuGet SqlServerCompact přidá do projektu skript po sestavení, který kopíruje nativní sestavení do složek *x86* a *amd64* ve složce *bin* projektu, ale skript nezahrnuje tyto složky v projektu. V důsledku toho Nasazení webu nebude kopírovat na cílový web, pokud je do projektu ručně nezahrnete. (Toto chování je výsledkem výchozí konfigurace nasazení. Další možností, kterou v těchto kurzech nebudete používat, je změna nastavení, které řídí toto chování. Nastavení, které lze změnit, je **pouze souborů potřebných ke spuštění aplikace** v části **položky k nasazení** na kartě **Balení/publikování webu** v okně **vlastností projektu** . Změna tohoto nastavení se obecně nedoporučuje, protože to může mít za následek nasazení mnoha dalších souborů do provozního prostředí, než je potřeba. Další informace o alternativách naleznete v kurzu [Konfigurace vlastností projektu](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md) .)

Sestavte projekt a potom v **Průzkumník řešení** klikněte na **Zobrazit všechny soubory** , pokud jste to ještě neudělali. Možná budete muset taky kliknout na **aktualizovat**.

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

Rozbalte složku **bin** a zobrazte složky **amd64** a **x86** a potom vyberte tyto složky, klikněte pravým tlačítkem myši a vyberte možnost **zahrnout do projektu**.

![amd64_and_x86_in_Solution_Explorer.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

Ikony složky se změní, aby se zobrazilo, že složka byla obsažena v projektu.

![Solution_Explorer_amd64_included.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>Konfigurace Migrace Code First pro nasazení aplikační databáze

Když nasadíte databázi aplikace, obvykle nebudete jednoduše nasazovat vývojovou databázi se všemi daty v ní do produkčního prostředí, protože většina dat v nich je pravděpodobně pouze pro účely testování. Například názvy studentů v testovací databázi jsou fiktivní. Na druhé straně často nemůžete nasadit pouze databázovou strukturu bez jakýchkoli dat. Některá data v testovací databázi můžou být skutečná data a musí se nacházet, když uživatelé začnou aplikaci používat. Vaše databáze může mít například tabulku, která obsahuje platné hodnoty úrovně nebo názvy skutečných oddělení.

Chcete-li tento běžný scénář simulovat, nakonfigurujete metodu Migrace Code First počáteční hodnoty, která vloží do databáze pouze data, která mají být v produkčním prostředí. Tato metoda osazení nevloží testovací data, protože se spustí v produkčním prostředí po Code First vytvoří databázi v produkčním prostředí.

V dřívějších verzích Code First před vydáním migrace bylo běžné, že metody počátečního vkládání testovacích dat jsou také v případě, že se při vývoji každé změny modelu databáze musela úplně odstranit a znovu vytvořit od začátku. Při Migrace Code First se testovací data uchovávají po změnách databáze, takže včetně testovacích dat v metodě osazení není nutné. Projekt, který jste stáhli, používá metodu před migrací pro zahrnutí všech dat do počáteční metody třídy inicializátoru. V tomto kurzu zakážete třídu inicializátoru a povolíte migrace. Pak aktualizujete metodu počáteční hodnoty ve třídě konfigurace Migraces tak, že vloží jenom data, která chcete vložit do produkčního prostředí.

Následující diagram znázorňuje schéma databáze aplikace:

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

V těchto kurzech předpokládáme, že při prvním nasazení webu by měly být tabulky `Student` a `Enrollment` prázdné. Ostatní tabulky obsahují data, která musí být předem načtena při provozu aplikace.

Vzhledem k tomu, že budete používat Migrace Code First, už nemusíte používat inicializátor Code First **DropCreateDatabaseIfModelChanges** . Kód pro tento inicializátor je v souboru SchoolInitializer.cs v projektu ContosoUniversity. DAL. Nastavení v elementu **appSettings** souboru Web. config způsobí, že se tento inicializátor spustí pokaždé, když se aplikace pokusí o přístup k databázi poprvé:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

Otevřete soubor Web. config aplikace a odeberte prvek, který určuje třídu inicializátoru Code First z elementu appSettings. Element appSettings teď vypadá takto:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> Dalším způsobem, jak určit třídu inicializátoru, je to provést voláním `Database.SetInitializer` v metodě `Application_Start` v souboru *Global. asax* . Pokud povolujete migrace v projektu, který používá tuto metodu k určení inicializátoru, odeberte tento řádek kódu.

Dále povolte Migrace Code First.

Prvním krokem je ujistit se, že projekt ContosoUniversity je nastaven jako spouštěný projekt. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt ContosoUniversity a vyberte **nastavit jako spouštěný projekt**. Migrace Code First se podívá na spouštěný projekt, aby se našel připojovací řetězec databáze.

V nabídce **Nástroje** klikněte na **Správce balíčků NuGet** a pak na **Konzola Správce balíčků**.

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

V horní části okna **konzoly Správce balíčků** vyberte jako výchozí projekt CONTOSOUNIVERSITY. dal a potom v `PM>`ovém řádku zadejte "Enable-migrations" (Povolit – migrace).

![Povolit – migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

Tento příkaz vytvoří soubor *Configuration.cs* v nové složce *migrace* v projektu ContosoUniversity. dal.

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

Vybrali jste projekt DAL, protože příkaz "Enable-migrations" musí být spuštěn v projektu, který obsahuje třídu kontextu Code First. Když je tato třída v projektu knihovny tříd, Migrace Code First vyhledá připojovací řetězec databáze ve spouštěcím projektu pro řešení. V řešení ContosoUniversity byl webový projekt nastaven jako spouštěný projekt. (Pokud jste nechtěli určit projekt, který má připojovací řetězec jako spouštěný projekt v aplikaci Visual Studio, můžete zadat spouštěný projekt v příkazu PowerShellu. Pokud chcete zobrazit syntaxi příkazu pro příkaz Povolit – migrace, můžete zadat příkaz "Get-Help Enable-migrations".)

Otevřete soubor Configuration.cs a nahraďte komentáře v metodě `Seed` následujícím kódem:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

Odkazy na `List` mají červené vlnovky pod nimi, protože ještě nemáte příkaz `using` pro svůj obor názvů. Klikněte pravým tlačítkem myši na jednu z instancí `List` a klikněte na možnost **vyřešit**a pak klikněte na možnost **použít System. Collections. Generic**.

![Vyřešit pomocí příkazu Using](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

Tento výběr nabídky přidá následující kód do příkazů `using` v horní části souboru.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> Přidání kódu do metody `Seed` je jedním z mnoha způsobů, jak vložit pevná data do databáze. Alternativou je přidání kódu do `Up` a `Down` metody každé migrační třídy. Metody `Up` a `Down` obsahují kód, který implementuje změny databáze. Příklady najdete v kurzu [nasazení aktualizace databáze](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) .
> 
> Můžete také napsat kód, který provede příkazy SQL pomocí metody `Sql`. Například pokud jste přidávali sloupec rozpočet do tabulky oddělení a chtěli jste v rámci migrace inicializovat všechny rozpočty oddělení $1 000,00, můžete do metody `Up` pro tuto migraci přidat následující řádek kódu:
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> Tento příklad zobrazený v tomto kurzu používá metodu `AddOrUpdate` v metodě `Seed` třídy Migrace Code First `Configuration`. Migrace Code First volá metodu `Seed` po každé migraci a tato metoda aktualizuje řádky, které již byly vloženy, nebo je vloží, pokud ještě neexistují. Metoda `AddOrUpdate` možná není nejlepší volbou pro váš scénář. Další informace najdete v tématu povýšení [metody EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) na blogu Julie Lerman.

Stisknutím kombinace kláves CTRL + SHIFT + B Sestavte projekt.

Dalším krokem je vytvoření třídy `DbMigration` pro prvotní migraci. Chcete, aby tato migrace vytvořila novou databázi, takže je nutné odstranit databázi, která již existuje. SQL Server Compact databáze jsou obsaženy v souborech *. sdf* ve složce *App\_data* . V **Průzkumník řešení**rozbalte *\_data aplikace* v projektu ContosoUniversity, abyste viděli dvě databáze SQL Server Compact, které jsou reprezentovány soubory *. sdf* .

Klikněte pravým tlačítkem na soubor *School. sdf* a klikněte na **Odstranit**.

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

V okně **konzoly Správce balíčků** zadejte příkaz "Přidání-migrace počátečního" a vytvořte počáteční migraci a pojmenujte ji "Initial".

![Přidat migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Migrace Code First vytvoří další soubor třídy ve složce *migrations* a tato třída obsahuje kód, který vytvoří schéma databáze.

V **konzole správce balíčků**zadejte příkaz "Update-Database" a vytvořte databázi a spusťte metodu **počáteční** hodnoty.

![update-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

(Pokud se zobrazí chyba, která indikuje, že tabulka již existuje a nelze ji vytvořit, je pravděpodobné, že jste aplikaci spustili po odstranění databáze a před provedením `update-database`. V takovém případě znovu odstraňte soubor *School. sdf* a opakujte příkaz `update-database`.)

Spusťte aplikaci. Stránka Students je teď prázdná, ale stránka instruktoři obsahuje instruktory. To je to, co budete mít v produkčním prostředí po nasazení aplikace.

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

Projekt je teď připravený k nasazení *školní* databáze.

## <a name="creating-a-membership-database-for-deployment"></a>Vytvoření databáze členství pro nasazení

Společnost Contoso University používá k ověřování a autorizaci uživatelů systém členství v ASP.NET a ověřování pomocí formulářů. Jedna z jejích stránek je přístupná pouze správcům. Pokud chcete zobrazit tuto stránku, spusťte aplikaci a v rozevírací nabídce v části **kurzy**vyberte **aktualizovat kredity** . Aplikace zobrazí **přihlašovací** stránku, protože pouze správci mají autorizaci k používání stránky **aktualizovat kredity** .

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

Přihlaste se jako správce pomocí hesla "pas $ W0rd" (Všimněte si čísla nula místo písmene "o" v "W0rd"). Po přihlášení se zobrazí stránka **aktualizace kredity** .

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

Při prvním nasazení lokality je běžné vyloučit ze všech nebo všech uživatelských účtů, které vytvoříte pro testování. V takovém případě nasadíte účet správce a žádné uživatelské účty. Místo ručního odstraňování testovacích účtů vytvoříte novou databázi členství, která má pouze jednoho uživatelského účtu správce, který budete potřebovat v produkčním prostředí.

> [!NOTE]
> Databáze členství ukládá hash hesla účtů. Aby bylo možné nasadit účty z jednoho počítače do jiného, je nutné zajistit, aby rutiny hash nevytvářely na cílovém serveru různé hodnoty hash, než na zdrojovém počítači. Když použijete ASP.NET Universal Providers, vygenerují se stejné hodnoty hash, pokud neměníte výchozí algoritmus. Výchozí algoritmus je HMACSHA256 a je určen v atributu **ověřování** elementu **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** v souboru Web. config.

Databáze členství není spravovaná pomocí Migrace Code First a není k dispozici žádný automatický inicializátor, který vysemena databáze pomocí testovacích účtů (jak je pro školní databázi). Proto pokud chcete zachovat dostupné testovací data, vytvořte kopii testovací databáze předtím, než vytvoříte novou.

V **Průzkumník řešení**přejmenujte soubor *ASPNET. sdf* ve složce *App\_data* na *ASPNET-dev. sdf*. (Nevytvářejte kopii, stačí ji přejmenovat – novou databázi vytvoříte za chvíli.)

V **Průzkumník řešení**se ujistěte, že je vybraný webový projekt (ContosoUniversity, ne CONTOSOUNIVERSITY. dal). Pak v nabídce **projekt** vyberte **Konfigurace ASP.NET** a spusťte **Nástroj pro správu**webu (Wat).

Vyberte kartu **Zabezpečení**.

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

Klikněte na **vytvořit nebo spravovat role** a přidejte roli **správce** .

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

Přejděte zpět na kartu **zabezpečení** , klikněte na tlačítko **vytvořit uživatele**a přidejte uživatele "správce" jako správce. Než kliknete na tlačítko **vytvořit uživatele** na stránce **vytvořit uživatele** , nezapomeňte zaškrtnout políčko **správce** . Heslo použité v tomto kurzu je "pas $ W0rd" a můžete zadat libovolnou e-mailovou adresu.

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

Zavřete prohlížeč. V **Průzkumník řešení**kliknutím na tlačítko Aktualizovat zobrazte nový soubor *ASPNET. sdf* .

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

Klikněte pravým tlačítkem na **ASPNET. sdf** a vyberte **zahrnout do projektu**.

## <a name="distinguishing-development-from-production-databases"></a>Odlišení vývoje od produkčních databází

V této části přejmenujete databáze tak, aby byly vývojové verze School-Dev. SDF a aspnet-Dev. SDF a produkční verze jsou School-Prod. SDF a aspnet-Prod. SDF. To není nutné, ale pomůžeme vám zachovávat zkušební a produkční verze databází, které jsou zaměňovány.

V **Průzkumník řešení**klikněte na **aktualizovat** a rozbalte složku data\_App, abyste viděli školní databázi, kterou jste vytvořili dříve. klikněte na něj pravým tlačítkem myši a vyberte možnost **zahrnout do projektu**.

![Including_School.sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

Přejmenujte *ASPNET. sdf* na *ASPNET-prod. sdf*.

Přejmenujte *School. sdf* na *School-dev. sdf*.

Když aplikaci spouštíte v aplikaci Visual Studio, nechcete používat verze *-výr* souborů databáze, chcete použít *vývojové* verze. Proto je nutné změnit připojovací řetězce v souboru Web. config tak, aby odkazovaly na verze pro *vývoj* databází. (Nevytvořili jste soubor School-Prod. SDF, ale to je v pořádku, protože Code First vytvoří tuto databázi v produkčním prostředí při prvním spuštění vaší aplikace.)

Otevřete soubor Web. config aplikace a vyhledejte připojovací řetězce:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

Změňte "ASPNET. sdf" na "aspnet-Dev. sdf" a změňte "School. sdf" na "School-Dev. sdf":

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

Databázový stroj SQL Server Compact a obě databáze jsou nyní připraveny k nasazení. V následujícím kurzu nastavíte automatickou transformaci souborů *Web. config* pro nastavení, která se musí lišit ve vývojových, testovacích a produkčních prostředích. (Mezi nastaveními, která musí být změněna, jsou připojovací řetězce, ale tyto změny nastavíte později při vytváření profilu publikování.)

## <a name="more-information"></a>Další informace

Další informace o NuGet najdete v tématu [Správa knihoven projektů pomocí NuGet](https://msdn.microsoft.com/magazine/hh547106.aspx) a [dokumentace k NuGet](http://docs.nuget.org/docs/start-here/overview). Pokud nechcete používat NuGet, budete se muset dozvědět, jak analyzovat balíček NuGet, abyste zjistili, co má při instalaci. (Například může nakonfigurovat transformace *souboru Web. config* , nakonfigurovat skripty prostředí PowerShell tak, aby běžely v době sestavování atd.) Další informace o tom, jak NuGet funguje, najdete v tématu obzvláště [vytváření a publikování balíčku](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) a [konfiguračního souboru a transformací zdrojového kódu](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations).

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [Další](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
