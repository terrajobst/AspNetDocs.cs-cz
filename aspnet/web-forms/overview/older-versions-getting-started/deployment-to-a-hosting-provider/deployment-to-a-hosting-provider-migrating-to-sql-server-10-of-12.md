---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 'Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: migrace na SQL Server-10 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640587"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>Nasazení webové aplikace v ASP.NET pomocí SQL Server Compact sady Visual Studio nebo Visual Web Developer: migrace na SQL Server-10 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak migrovat z SQL Server Compact na SQL Server. Jedním z důvodů, které byste mohli chtít udělat, je využití funkcí SQL Server, které SQL Server Compact nepodporuje, jako jsou uložené procedury, triggery, zobrazení nebo replikace. Další informace o rozdílech mezi SQL Server Compact a SQL Server najdete v kurzu [nasazení SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) .

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>SQL Server Express versus úplný SQL Server pro vývoj

Až se rozhodnete upgradovat na SQL Server, můžete ve svém vývojovém a testovacím prostředí používat SQL Server nebo SQL Server Express. Kromě rozdílů v podpoře nástrojů a funkcích databázového stroje existují rozdíly mezi implementacemi poskytovatele mezi SQL Server Compact a dalšími verzemi SQL Server. Tyto rozdíly mohou způsobit, že stejný kód generuje různé výsledky. Proto pokud se rozhodnete zachovat SQL Server Compact jako vývojovou databázi, měli byste web důkladně otestovat v SQL Server nebo SQL Server Express v testovacím prostředí před každým nasazením do produkčního prostředí.

Na rozdíl od SQL Server Compact SQL Server Express je v podstatě stejný databázový stroj a používá stejného poskytovatele .NET jako úplný SQL Server. Při testování pomocí SQL Server Express si můžete být jistí, že budete mít stejné výsledky jako v SQL Server. Většinu stejných databázových nástrojů můžete používat s SQL Server Express, které můžete použít s SQL Server (významnou výjimkou [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), a podporuje další funkce SQL Server, jako jsou uložené procedury, zobrazení, aktivační události a replikace. (Na produkčním webu ale obvykle musíte použít úplnou SQL Server. SQL Server Express lze spustit ve sdíleném hostitelském prostředí, ale není pro něj navrženo a mnoho poskytovatelů hostingu je nepodporuje.)

Pokud používáte Visual Studio 2012, obvykle pro vývojové prostředí zvolíte SQL Server Express LocalDB, protože to je to, co je ve výchozím nastavení nainstalováno v aplikaci Visual Studio. LocalDB ale ve službě IIS nefunguje, takže pro vaše testovací prostředí musíte použít buď SQL Server, nebo SQL Server Express.

### <a name="combining-databases-versus-keeping-them-separate"></a>Kombinování databází a jejich oddělené zachování

Aplikace Contoso University má dvě databáze SQL Server Compact: databáze členství (*ASPNET. sdf*) a aplikační databáze (*School. sdf*). Při migraci můžete tyto databáze migrovat do dvou samostatných databází nebo do jediné databáze. Možná je budete chtít kombinovat, aby bylo možné mezi databází aplikace a databází členství usnadnit spojení s databázemi. Váš plán hostování může také poskytnout důvod, jak je kombinovat. Poskytovatel hostingu může například účtovat více databází více nebo nemusí dokonce umožňovat více než jednu databázi. V tomto případě se jedná o hostitelský účet Cytanium Lite, který se používá pro tento kurz, který umožňuje pouze jednu databázi SQL Server.

V tomto kurzu migrujete své dvě databáze tímto způsobem:

- Migrujte na dvě databáze LocalDB ve vývojovém prostředí.
- Migrujte do dvou SQL Server Express databází v testovacím prostředí.
- Migrujte do jedné kombinované úplné SQL Server databáze v produkčním prostředí.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="installing-sql-server-express"></a>Instalace SQL Server Express

Ve výchozím nastavení je SQL Server Express automaticky nainstalován v aplikaci Visual Studio 2010, ale ve výchozím nastavení není nainstalována společně se sadou Visual Studio 2012. Pokud chcete nainstalovat SQL Server 2012 Express, klikněte na následující odkaz.

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

Vyberte možnost *CSY/x64/SQLEXPR\_x64\_CSY. exe* nebo *CSY/x86/SQLEXPR\_x86\_CSY. exe*a v Průvodci instalací přijměte výchozí nastavení. Další informace o možnostech instalace najdete v tématu [instalace SQL Server 2012 v Průvodci instalací (nastavení)](https://msdn.microsoft.com/library/ms143219.aspx).

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>Vytváření databází SQL Server Express pro testovací prostředí

Dalším krokem je vytvoření databáze členství v ASP.NET a školních databází.

V nabídce **zobrazení** vyberte **Průzkumník serveru** (**Průzkumník databáze** ve Visual Web Developer) a pak klikněte pravým tlačítkem na **datová připojení** a vyberte **vytvořit novou databázi SQL Server**.

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

V dialogovém okně **vytvořit novou databázi SQL Server** do pole **název serveru** zadejte ".\SQLEXPRESS" a do pole název **nového databáze** zadejte "ASPNET-test" a pak klikněte na **OK**.

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

Použijte stejný postup k vytvoření nové databáze SQL Server Express School s názvem "School-test".

(K těmto názvům databází připojujete "test", protože později vytvoříte další instanci každé databáze pro vývojové prostředí a potřebujete být schopni odlišit tyto dvě sady databází.)

**Průzkumník serveru** nyní zobrazuje dvě nové databáze.

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>Vytvoření skriptu pro udělení pro nové databáze

Když aplikace běží ve službě IIS na vývojovém počítači, aplikace přistupuje k databázi pomocí výchozích přihlašovacích údajů fondu aplikací. Ve výchozím nastavení ale identita fondu aplikací nemá oprávnění k otevření databází. Proto je nutné spustit skript pro udělení tohoto oprávnění. V této části vytvoříte skript, který později spustíte, abyste se ujistili, že aplikace může otevírat databáze při spuštění ve službě IIS.

Ve složce *SolutionFiles* řešení, kterou jste vytvořili v kurzu [nasazení do provozního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) , vytvořte nový soubor SQL s názvem *grant. SQL*. Zkopírujte následující příkazy SQL do souboru a pak soubor uložte a zavřete:

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> Tento skript je navržený tak, aby fungoval s SQL Server 2008 a s nastavením služby IIS v systému Windows 7, jak jsou uvedeny v tomto kurzu. Pokud používáte jinou verzi SQL Server nebo Windows nebo pokud jste v počítači nastavili službu IIS odlišně, může se stát, že se budou vyžadovat změny v tomto skriptu. Další informace o SQL Server skriptů naleznete v tématu [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).

> [!NOTE] 
> 
> **Poznámka k zabezpečení** Tento skript uděluje uživateli oprávnění\_oprávnění vlastníka, který přistupuje k databázi v době běhu, což je to, co budete mít v produkčním prostředí. V některých případech můžete chtít zadat uživatele, který má úplná oprávnění aktualizace schématu databáze jenom pro nasazení, a určit dobu běhu jiného uživatele, který má oprávnění jenom pro čtení a zápis dat. Další informace najdete v tématu **Kontrola automatických změn souboru Web. config pro migrace Code First** při [nasazení do služby IIS jako testovací prostředí](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md).

## <a name="configuring-database-deployment-for-the-test-environment"></a>Konfigurace nasazení databáze pro testovací prostředí

Dále nakonfigurujete aplikaci Visual Studio tak, aby provede následující úlohy pro každou databázi:

- Vygenerujte skript SQL, který vytvoří strukturu zdrojové databáze (tabulky, sloupce, omezení atd.) v cílové databázi.
- Vygenerujte skript SQL, který vloží data zdrojové databáze do tabulek v cílové databázi.
- V cílové databázi spusťte vygenerované skripty a vytvořený skript pro udělení.

Otevřete okno **Vlastnosti projektu** a vyberte kartu **balíček/publikovat SQL** .

Ujistěte se, že je v rozevíracím seznamu **Konfigurace** vybraná možnost **aktivní (vydaná verze)** nebo **vydaná verze** .

Klikněte na **Povolit tuto stránku**.

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

Karta **Balení/publikování kódu SQL** je obvykle zakázaná, protože specifikuje starší metodu nasazení. Ve většině scénářů byste měli nakonfigurovat nasazení databáze v průvodci **publikování webu** . Migrace z SQL Server Compact na SQL Server nebo SQL Server Express je zvláštní případ, pro který je tato metoda dobrá volbou.

Klikněte na **Importovat ze souboru Web. config**.

![Selecting_Import_from_Web. config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual Studio hledá připojovací řetězce v souboru *Web. config* , najde jednu pro databázi členství a jednu pro databázi školy a přidá do tabulky **databázových záznamů** řádek odpovídající každému připojovacímu řetězci. Připojovací řetězce, které najde, jsou pro existující databáze SQL Server Compact a vaším dalším krokem bude nakonfigurovat, jak a kde tyto databáze nasadit.

Nastavení nasazení databáze zadáte v části **Podrobnosti o položce databáze** pod tabulkou **položky databáze** . Nastavení zobrazená v části **Podrobnosti o položce databáze** se vztahuje na každý řádek v tabulce **databázové položky** , jak je znázorněno na následujícím obrázku.

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>Konfigurace nastavení nasazení pro databázi členství

V tabulce **položky databáze** vyberte řádek **DefaultConnection-Deployment** , abyste mohli konfigurovat nastavení, která se vztahují na databázi členství.

Do pole **připojovací řetězec pro cílovou databázi**zadejte připojovací řetězec, který odkazuje na novou SQL Server Express databázi členství. Připojovací řetězec, který potřebujete, můžete získat z **Průzkumník serveru**. V **Průzkumník serveru**rozbalte položku **datová připojení** a vyberte databázi **AspnetTest** a potom v okně **vlastnosti** Zkopírujte hodnotu **připojovacího řetězce** .

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

Do této části se vytvoří stejný připojovací řetězec:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

Tento připojovací řetězec zkopírujte a vložte do **připojovacího řetězce pro cílovou databázi** na kartě **Package/Publish SQL** .

Ujistěte se, že je vybraná možnost **načíst data nebo schéma z existující databáze** . To způsobuje, že se skripty SQL automaticky vygenerovaly a spustí v cílové databázi.

**Připojovací řetězec pro hodnotu zdrojové databáze** je extrahován ze souboru *Web. config* a odkazuje na databázi vývoje SQL Server Compact. Jedná se o zdrojovou databázi, která se použije ke generování skriptů, které se spustí později v cílové databázi. Vzhledem k tomu, že chcete nasadit produkční verzi databáze, změňte "aspnet-Dev. sdf" na "aspnet-Prod. sdf".

Změna **možností skriptování databáze** z **schématu pouze** na **schéma a data**, protože chcete kopírovat data (uživatelské účty a role) i strukturu databáze.

Pokud chcete nakonfigurovat nasazení tak, aby se spouštěly skripty pro udělení, které jste vytvořili dříve, musíte je přidat do oddílu **databázové skripty** . Klikněte na **Přidat skript**a v dialogovém okně **přidat skripty SQL** přejděte do složky, kam jste uložili skript pro udělení oprávnění (Jedná se o složku, která obsahuje soubor řešení). Vyberte soubor s názvem *grant. SQL*a klikněte na tlačítko **otevřít**.

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

Nastavení řádku **DefaultConnection-Deployment** v **položkách databáze** teď vypadá jako na následujícím obrázku:

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>Konfigurace nastavení nasazení pro školní databázi

V dalším kroku vyberte řádek **SchoolContext-Deployment** v tabulce **položky databáze** , aby se nakonfigurovali nastavení nasazení pro školní databázi.

K získání připojovacího řetězce pro novou SQL Server Express databázi můžete použít stejnou metodu, kterou jste použili dříve. Zkopírujte tento připojovací řetězec do **připojovacího řetězce pro cílovou databázi** na kartě **Package/Publish SQL** .

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

Ujistěte se, že je vybraná možnost **načíst data nebo schéma z existující databáze** .

**Připojovací řetězec pro hodnotu zdrojové databáze** je extrahován ze souboru *Web. config* a odkazuje na databázi vývoje SQL Server Compact. Pokud chcete nasadit produkční verzi databáze, změňte "School-Dev. sdf" na "School-Prod. sdf". (Soubor School-Prod. SDF se ve složce App\_data nikdy nevytvořil, takže tento soubor zkopírujete z testovacího prostředí do složky aplikace\_data ve složce projektu ContosoUniversity později.)

Změna **možností skriptování databáze** na **schéma a data**

Chcete také spustit skript, který uděluje oprávnění ke čtení a zápisu této databáze k identitě fondu aplikací, proto přidejte soubor skriptu *grant. SQL* jako u databáze členství.

Až skončíte, nastavení řádku **SchoolContext-Deployment** v **položkách databáze** budou vypadat jako na následujícím obrázku:

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

Uložte změny na kartě **Package/PUBLISH SQL** .

Zkopírujte soubor *School-prod. sdf* z složky *c:\inetpub\wwwroot\ContosoUniversity\App\_dat* do složky *App\_data* v projektu ContosoUniversity.

### <a name="specifying-transacted-mode-for-the-grant-script"></a>Určení transakčního režimu pro skript udělení

Proces nasazení generuje skripty, které nasazují schéma databáze a data. Ve výchozím nastavení se tyto skripty spouštějí v transakci. Vlastní skripty (jako skripty pro udělení) ale ve výchozím nastavení neběží v transakci. Pokud proces nasazení smíchá režimy transakce, může při spuštění skriptu při nasazení dojít k chybě časového limitu. V této části upravíte soubor projektu, aby bylo možné nakonfigurovat vlastní skripty pro spuštění v transakci.

V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **ContosoUniversity** a vyberte **Uvolnit projekt**.

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

Pak znovu klikněte pravým tlačítkem na projekt a vyberte **Upravit ContosoUniversity. csproj**.

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

Editor sady Visual Studio zobrazuje obsah XML souboru projektu. Všimněte si, že existuje několik prvků `PropertyGroup`. (V imagi byl obsah prvků `PropertyGroup` vynechán.)

![Okno editoru souboru projektu](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

První z nich, který nemá atribut `Condition`, je pro nastavení, která platí bez ohledu na konfiguraci sestavení. Jeden `PropertyGroup` element se vztahuje pouze na konfiguraci sestavení ladění (Všimněte si, že atribut `Condition`), jedna se vztahuje pouze na konfiguraci sestavení pro vydání a jedna se vztahuje pouze na konfiguraci sestavení testu. V elementu `PropertyGroup` pro konfiguraci sestavení pro vydání se zobrazí `PublishDatabaseSettings` prvek, který obsahuje nastavení, která jste zadali na kartě **Package/PUBLISH SQL** karta. Existuje `Object` element, který odpovídá jednotlivým zadaným skriptům udělení (Všimněte si dvou instancí "Grant. SQL"). Ve výchozím nastavení je `Transacted` atribut `Source` elementu pro každý skript pro udělení `False`.

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

Změňte hodnotu atributu `Transacted` elementu `Source` na `True`.

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

Uložte a zavřete soubor projektu a pak klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a vyberte **znovu načíst projekt**.

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>Nastavení transformací Web. config pro připojovací řetězce

Připojovací řetězce pro nové databáze SQL Express, které jste zadali na kartě **Balení/publikování kódu SQL** , jsou používány nasazení webu pouze pro aktualizaci cílové databáze během nasazení. Je stále nutné nastavit transformace *souboru Web. config* tak, aby připojovací řetězce v nasazeném souboru *Web. config* odkazovaly na nové databáze SQL Server Express. (Při použití karty **balíček/publikovat SQL** nemůžete konfigurovat připojovací řetězce v profilu publikování.)

Otevřete *Web. test. config* a v následujícím příkladu nahraďte element `connectionStrings` prvkem `connectionStrings`. (Nezapomeňte zkopírovat pouze Element connectionStrings, nikoli okolní kód, který je zde zobrazen, aby poskytoval kontext.)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

Tento kód způsobí, že atributy `connectionString` a `providerName` každého elementu `add` budou nahrazeny v nasazeném souboru *Web. config* . Tyto připojovací řetězce nejsou totožné s těmi, které jste zadali na kartě **Package/PUBLISH SQL** karta. Nastavení "MultipleActiveResultSets = True" bylo přidáno do těchto, protože je vyžadováno pro Entity Framework a univerzálním poskytovatelům.

## <a name="installing-sql-server-compact"></a>Instalace SQL Server Compact

Balíček NuGet SqlServerCompact SQL Server Compact poskytuje sestavení databázového stroje pro aplikaci Contoso University. Nyní ale nejedná se o aplikaci, ale Nasazení webu, která musí být schopna číst databáze SQL Server Compact, aby bylo možné vytvářet skripty pro spuštění v databázích SQL Server. Pokud chcete povolit Nasazení webu čtení SQL Server Compact databází, nainstalujte SQL Server Compact na vývojovém počítači pomocí následujícího odkazu: [Microsoft SQL Server Compact 4,0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6).

## <a name="deploying-to-the-test-environment"></a>Nasazení do testovacího prostředí

Aby bylo možné publikovat do testovacího prostředí, je nutné vytvořit profil publikování, který je nakonfigurován tak, aby používal kartu **Package/PUBLISH SQL** pro publikování databáze místo nastavení databáze profilu publikování.

Nejprve odstraňte existující testovací profil.

V **Průzkumník řešení**klikněte pravým tlačítkem na projekt ContosoUniversity a klikněte na **publikovat**.

Vyberte kartu **profil** .

Klikněte na **Spravovat profily**.

Vyberte **test**, klikněte na **Odebrat**a pak klikněte na **Zavřít**.

Zavřete průvodce **publikováním webu** a uložte tuto změnu.

Potom vytvořte nový profil testu a použijte ho k publikování projektu.

V **Průzkumník řešení**klikněte pravým tlačítkem na projekt ContosoUniversity a klikněte na **publikovat**.

Vyberte kartu **profil** .

V rozevíracím seznamu vyberte **&lt;nový...&gt;** a jako název profilu zadejte "test".

Do pole **Adresa URL služby** zadejte *localhost*.

Do pole **Web/aplikace** zadejte *Default Web site/ContosoUniversity*.

Do pole **cílová adresa URL** zadejte `http://localhost/ContosoUniversity/`.

Klikněte na tlačítko **Další**.

Karta **Nastavení** vás upozorní na to, že byla nakonfigurovaná karta **balíček/publikování SQL** , a získáte možnost je přepsat kliknutím na Povolit nová vylepšení publikování databáze. Pro toto nasazení nechcete přepsat nastavení karty pro **Balení/publikování SQL** , takže stačí kliknout na **Další**.

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

Zpráva na kartě **Preview** označuje, že **nejsou vybrány žádné databáze pro publikování**, ale to znamená, že publikování databáze není konfigurováno v profilu publikování.

Klikněte na **publikovat**.

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio nasadí aplikaci a otevře prohlížeč na domovské stránce webu v testovacím prostředí. Spuštěním stránky instruktory zjistíte, že se zobrazí stejná data, která jste viděli dříve. Spusťte stránku **Přidat studenty** , přidejte nového studenta a pak na stránce **Students** Zobrazte nového studenta. Tím ověříte, že můžete databázi aktualizovat. Vyberte stránku **aktualizovat kredity** (budete se muset přihlásit) a ověřte, jestli je databáze členství nasazená a máte k ní přístup.

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>Vytvoření databáze SQL Server pro produkční prostředí

Teď, když jste nasadili do testovacího prostředí, jste připraveni nastavit nasazení do produkčního prostředí. V rámci testovacího prostředí začínáte tím, že vytvoříte databázi, do které se nasadíte. Při odvolání z přehledu je plán hostování Cytanium Lite možné pouze pro jednu databázi SQL Server, takže nastavíte pouze jednu databázi, ne dvě. Všechny tabulky a data z členství a školních SQL Server Compact databází budou nasazeny do jedné databáze SQL Server v produkčním prostředí.

V [http://panel.cytanium.com](http://panel.cytanium.com)na ovládacím panelu Cytanium. Podržte myš nad **databázemi** a pak klikněte **SQL Server 2008**.

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

Na stránce **SQL Server 2008** klikněte na **vytvořit databázi**.

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

Pojmenujte databázi "School" a klikněte na **Uložit**. (Stránka automaticky přidá předponu "contoso", takže platný název bude "contosouSchool".)

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

Na stejné stránce klikněte na **vytvořit uživatele**. Na serverech Cytanium se místo použití integrovaného zabezpečení systému Windows a umožnění, aby identita fondu aplikací otevřela vaši databázi, vytvoříte uživatele, který má oprávnění k otevření vaší databáze. Přidáte přihlašovací údaje uživatele do připojovacích řetězců, které se nacházejí v produkčním souboru *Web. config* . V tomto kroku vytvoříte tyto přihlašovací údaje.

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

Vyplňte požadovaná pole na stránce **vlastností uživatele SQL** :

- Jako název zadejte "ContosoUniversityUser".
- Zadejte heslo.
- Jako výchozí databázi vyberte **contosouSchool** .
- Zaškrtněte políčko **contosouSchool** .

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>Konfigurace nasazení databáze pro produkční prostředí

Teď jste připraveni nastavit nastavení nasazení databáze na kartě **Package/PUBLISH SQL** , stejně jako jste to předtím pro testovací prostředí.

Otevřete okno **Vlastnosti projektu** , vyberte kartu **Balení/publikování kódu SQL** a ujistěte se, že je v rozevíracím seznamu **Konfigurace** vybrána možnost **aktivní (verze)** nebo **vydaná verze** .

Když nakonfigurujete nastavení nasazení pro každou databázi, je důležité rozdíl mezi tím, co v produkčním prostředí a testovacím prostředím provádíte při konfiguraci připojovacích řetězců. V testovacím prostředí jste zadali jiné připojovací řetězce cílové databáze, ale v produkčním prostředí bude cílový připojovací řetězec pro obě databáze stejný. Důvodem je to, že nasazujete obě databáze do jedné databáze v produkčním prostředí.

### <a name="configuring-deployment-settings-for-the-membership-database"></a>Konfigurace nastavení nasazení pro databázi členství

Chcete-li konfigurovat nastavení, která se vztahují na databázi členství, vyberte řádek **DefaultConnection-Deployment** v tabulce **položky databáze** .

Do pole **připojovací řetězec pro cílovou databázi**zadejte připojovací řetězec, který odkazuje na novou produkční SQL Server databázi, kterou jste právě vytvořili. Připojovací řetězec můžete získat z uvítacího e-mailu. Relevantní část e-mailu obsahuje následující vzorový připojovací řetězec:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

Po nahrazení tří proměnných bude připojovací řetězec, který potřebujete, vypadat jako v tomto příkladu:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

Tento připojovací řetězec zkopírujte a vložte do **připojovacího řetězce pro cílovou databázi** na kartě **Package/Publish SQL** .

Ujistěte se, že je stále vybraná možnost **načíst data a schéma z existující databáze** a že **možnosti skriptování databáze** jsou stále **schémat a data**.

V poli **databázové skripty** zrušte zaškrtnutí políčka vedle skriptu grant. SQL.

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>Konfigurace nastavení nasazení pro školní databázi

V dalším kroku vyberte řádek **SchoolContext-Deployment** v tabulce **položky databáze** , aby se nakonfigurovali nastavení školní databáze.

Zkopírujte stejný připojovací řetězec do **připojovacího řetězce pro cílovou databázi** , kterou jste zkopírovali do tohoto pole pro databázi členství.

Ujistěte se, že je stále vybraná možnost **načíst data a schéma z existující databáze** a že **možnosti skriptování databáze** jsou stále **schémat a data**.

V poli **databázové skripty** zrušte zaškrtnutí políčka vedle skriptu grant. SQL.

Uložte změny na kartě **Package/PUBLISH SQL** .

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>Nastavení transformací Web. config pro připojovací řetězce na provozní databáze

Dále nastavíte transformace *Web. config* tak, aby připojovací řetězce v nasazeném souboru *Web. config* odkazovaly na novou provozní databázi. Připojovací řetězec, který jste zadali na kartě **Balení/publikování SQL** pro nasazení webu, který se má použít, je stejný jako aplikace, kterou je třeba použít, s výjimkou přidání možnosti `MultipleResultSets`.

Otevřete *Web. produkční. config* a nahraďte `connectionStrings` element prvkem `connectionStrings`, který vypadá podobně jako v následujícím příkladu. (Zkopírujte pouze element `connectionStrings`, nikoli okolní značky, které jsou k dispozici pro zobrazení kontextu.)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

Někdy vidíte Rady, které vám pomohou při každém zašifrování připojovacích řetězců v souboru *Web. config* . To může být vhodné, pokud nasazujete na servery ve vaší vlastní podnikové síti. Pokud nasazujete do sdíleného hostitelského prostředí, ale důvěřujete bezpečnostním postupům poskytovatele hostingu a není nutné nebo praktické šifrovat připojovací řetězce.

## <a name="deploying-to-the-production-environment"></a>Nasazení do produkčního prostředí

Teď jste připraveni na nasazení do produkčního prostředí. Nasazení webu načte databáze SQL Server Compact ve složce *aplikace projektu\_data* a znovu vytvoří všechny své tabulky a data v provozní SQL Server databázi. Aby bylo možné publikovat pomocí nastavení karty **balíček/publikovat web** , je nutné vytvořit nový profil publikování pro produkční prostředí.

Nejdřív odstraňte existující provozní profil, protože jste předtím profil testu.

V **Průzkumník řešení**klikněte pravým tlačítkem na projekt ContosoUniversity a klikněte na **publikovat**.

Vyberte kartu **profil** .

Klikněte na **Spravovat profily**.

Vyberte možnost **Výroba**, klikněte na tlačítko **Odebrat**a pak klikněte na tlačítko **Zavřít**.

Zavřete průvodce **publikováním webu** a uložte tuto změnu.

Potom vytvořte nový provozní profil a použijte ho k publikování projektu.

V **Průzkumník řešení**klikněte pravým tlačítkem na projekt ContosoUniversity a klikněte na **publikovat**.

Vyberte kartu **profil** .

Klikněte na **importovat**a vyberte soubor. publishsettings, který jste předtím stáhli.

Na kartě **připojení** změňte **cílovou adresu URL** na správnou dočasnou adresu URL, která je v tomto příkladu http://contosouniversity.com.vserver01.cytanium.com.

Přejmenujte profil na produkční prostředí. (Vyberte kartu **profil** a klikněte na **Spravovat profily** k tomu).

Zavřete průvodce **publikováním webu** a uložte provedené změny.

V reálné aplikaci, ve které se databáze aktualizovala v produkčním prostředí, byste teď měli před publikováním udělat ještě dva další kroky:

1. Nahrajte *aplikaci\_offline. htm*, jak je znázorněno v kurzu [nasazení do provozního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) .
2. Pomocí funkce **Správce souborů** v Ovládacích panelech Cytanium zkopírujte soubory *ASPNET-prod. sdf* a *School-prod. sdf* z produkčního webu do složky *dat aplikace\_* projektu ContosoUniversity. Tím se zajistí, že data, která nasazujete do nové databáze SQL Server, obsahují nejnovější aktualizace provedené vaším provozním webem.

Na panelu nástrojů **publikování webu jedním kliknutím** ověřte, že je vybraný **produkční** profil, a pak klikněte na **publikovat**.

Pokud jste před publikováním nahráli <em>aplikaci\_offline. htm</em> , je nutné použít nástroj <strong>Správce souborů</strong> v ovládacím panelu Cytanium k odstranění <em>aplikace\_offline.</em> htm před testováním. Zároveň můžete odstranit soubory <em>. sdf</em> ze složky <em>App\_data</em> .

Nyní můžete otevřít prohlížeč a přejít na adresu URL vašeho veřejného webu a otestovat aplikaci stejným způsobem jako po nasazení do testovacího prostředí.

## <a name="switching-to-sql-server-express-localdb-in-development"></a>Přechod na SQL Server Express LocalDB ve vývoji

Jak bylo vysvětleno v přehledu, je obecně vhodné použít stejný databázový stroj ve vývoji, který používáte v testování a produkčním prostředí. (Mějte na paměti, že výhodou použití SQL Server Express ve vývoji je to, že databáze bude fungovat stejně ve vývojovém, testovacím a produkčním prostředí.) V této části nastavíte projekt ContosoUniversity tak, aby používal SQL Server Express LocalDB při spuštění aplikace ze sady Visual Studio.

Nejjednodušší způsob, jak provést tuto migraci, je umožnit Code First a systém členství pro vás vytvoří nové vývojové databáze. Použití této metody k migraci vyžaduje tři kroky:

1. Změnou připojovacích řetězců určete nové databáze SQL Express LocalDB.
2. Spusťte nástroj pro správu webu a vytvořte uživatele s oprávněními správce. Tím se vytvoří databáze členství.
3. K vytvoření a implementaci databáze aplikace použijte příkaz Migrace Code First Update-Database.

### <a name="updating-connection-strings-in-the-webconfig-file"></a>Aktualizace připojovacích řetězců v souboru Web. config

Otevřete soubor *Web. config* a nahraďte `connectionStrings` element následujícím kódem:

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>Vytváření databáze členství

V **Průzkumník řešení**vyberte projekt ContosoUniversity a potom v nabídce **projekt** klikněte na **Konfigurace ASP.NET** .

Vyberte kartu Zabezpečení.

Klikněte na **vytvořit nebo spravovat role**a pak vytvořte roli **správce** .

Vraťte se na kartu zabezpečení.

Klikněte na **vytvořit uživatele**a potom zaškrtněte políčko **správce** a vytvořte uživatele s názvem admin.

Zavřete **Nástroj pro správu**webu.

### <a name="creating-the-school-database"></a>Vytvoření školní databáze

Otevřete okno konzoly Správce balíčků.

V rozevíracím seznamu **výchozí projekt** vyberte projekt CONTOSOUNIVERSITY. dal.

Zadejte následující příkaz:

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

Migrace Code First aplikuje počáteční migraci, která vytvoří databázi, a pak použije migraci AddBirthDate, potom spustí metodu osazení.

Spusťte web stisknutím CTRL + F5. Stejně jako u testovacích a produkčních prostředí můžete spustit stránku **Přidat studenty** , přidat nového studenta a pak zobrazit nového studenta na stránce **Students** . Tím se ověří, že se vytvořila a inicializuje školní databáze a že k ní máte přístup pro čtení a zápis.

Vyberte stránku **aktualizovat kredity** a přihlaste se, abyste ověřili, jestli je databáze členství nasazená a jestli k ní máte přístup. Pokud jste nemigrovali své uživatelské účty, vytvořte účet správce a pak vyberte stránku **aktualizovat kredity** , abyste ověřili, že funguje.

## <a name="cleaning-up-sql-server-compact-files"></a>Čištění SQL Server Compactch souborů

Už nepotřebujete soubory a balíčky NuGet, které byly zahrnuté pro podporu SQL Server Compact. Pokud chcete (Tento krok není nutný), můžete vyčistit nepotřebné soubory a odkazy.

V **Průzkumník řešení**odstraňte soubory *. sdf* ze složky *App\_data* a ze složky z *přihrádky* *amd64* a *x86* .

V **Průzkumník řešení**klikněte pravým tlačítkem na řešení (ne na jeden z projektů) a pak klikněte na **Spravovat balíčky NuGet pro řešení**.

V levém podokně dialogového okna **Spravovat balíčky NuGet** vyberte **nainstalované balíčky**.

Vyberte balíček **EntityFramework. SqlServerCompact** a klikněte na **Spravovat**.

V dialogovém okně **Vybrat projekty** jsou vybrány oba projekty. Chcete-li balíček odinstalovat v obou projektech, zrušte zaškrtnutí políček a pak klikněte na tlačítko **OK**.

V dialogovém okně s dotazem, zda chcete odinstalovat závislé balíčky, klikněte na tlačítko Ne. Jedním z nich je balíček Entity Framework, který je třeba zachovat.

K odinstalaci balíčku **SqlServerCompact** použijte stejný postup. (Balíčky musí být v tomto pořadí odinstalovány, protože balíček **EntityFramework. SqlServerCompact** závisí na balíčku **SqlServerCompact** .)

Úspěšně jste migrovali SQL Server Express a plný SQL Server. V dalším kurzu provedete změnu další databáze a uvidíte, jak nasadit změny databáze, když testovací a provozní databáze používají SQL Server Express a úplné SQL Server.

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [Další](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
