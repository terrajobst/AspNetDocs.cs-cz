---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: Příprava na nasazení databáze | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: cdcb3578725c41e3c801afd54e6d34455bc4b281
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636995"
---
# <a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: Příprava na nasazení databáze

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu se dozvíte, jak připravit projekt pro nasazení databáze. Databázová struktura a některé (ne všechny) dat v obou databázích aplikace musí být nasazeny do testovacích, pracovních a produkčních prostředí.

Při vývoji aplikace se obvykle zadávají testovací data do databáze, kterou nechcete nasadit na živý Web. Můžete ale také mít nějaká provozní data, která chcete nasadit. V tomto kurzu nakonfigurujete projekt contoso University a připravíte skripty SQL tak, aby se při nasazení zahrnovala správná data.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](troubleshooting.md).

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

Ukázková aplikace používá SQL Server Express LocalDB. SQL Server Express je bezplatná edice SQL Server. Obvykle se používá během vývoje, protože je založen na stejném databázovém stroji jako plné verze SQL Server. Můžete testovat pomocí SQL Server Express a zajistit, aby se aplikace chovala stejně v produkčním prostředí s několika výjimkami pro funkce, které se liší od SQL Server edicí.

LocalDB je speciální režim provádění SQL Server Express, který umožňuje pracovat s databázemi jako se soubory *. mdf* . Soubory databáze LocalDB jsou obvykle uloženy ve složce *App\_data* webového projektu. Funkce uživatelské instance v SQL Server Express také umožňuje pracovat se soubory *. mdf* , ale funkce uživatelské instance je zastaralá. Proto se LocalDB doporučuje pro práci se soubory *. mdf* .

Pro produkční webové aplikace se typicky nepoužívá SQL Server Express. LocalDB se konkrétně nedoporučuje pro použití v produkčním prostředí s webovou aplikací, protože není navržená pro práci se službou IIS.

V aplikaci Visual Studio 2012 se LocalDB nainstaluje ve výchozím nastavení pomocí sady Visual Studio. V aplikaci Visual Studio 2010 a starších verzích SQL Server Express (bez LocalDB) je ve výchozím nastavení nainstalovány v aplikaci Visual Studio; To je důvod, proč jste ho nainstalovali jako jeden z požadavků v [prvním kurzu v této řadě](introduction.md).

Další informace o edicích SQL Server, včetně LocalDB, najdete v následujících zdrojích [pracujících s SQL Server databázemi](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver).

## <a name="entity-framework-and-universal-providers"></a>Entity Framework a univerzální poskytovatelé

Pro přístup k databázi vyžaduje aplikace Contoso University následující software, který musí být nasazený s aplikací, protože není zahrnutý v .NET Framework:

- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (umožňuje systému členství v ASP.NET použít Azure SQL Database)
- [Entity Framework](https://msdn.microsoft.com/library/gg696172.aspx)

Vzhledem k tomu, že je tento software součástí balíčků NuGet, projekt je již nastaven tak, aby požadovaná sestavení byla nasazena s projektem. (Odkazy odkazují na aktuální verze těchto balíčků, které mohou být novější než ty, které jsou nainstalovány v počátečním projektu, který jste stáhli pro účely tohoto kurzu.)

Pokud nasazujete jako poskytovatele hostování třetí strany místo Azure, ujistěte se, že používáte Entity Framework 5,0 nebo novější. Starší verze Migrace Code First vyžadují úplný vztah důvěryhodnosti a většina poskytovatelů hostingu spustí vaši aplikaci ve středním vztahu důvěryhodnosti. Další informace o střední důvěryhodnosti najdete v kurzu [nasazení do služby IIS jako testovací prostředí](deploying-to-iis.md) .

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>Konfigurace Migrace Code First pro nasazení aplikační databáze

Databáze aplikace Contoso University je spravovaná pomocí Code First a Vy ji nasadíte pomocí Migrace Code First. Přehled nasazení databáze pomocí Migrace Code First najdete v [prvním kurzu v této sérii](introduction.md).

Když nasadíte databázi aplikace, obvykle nebudete jednoduše nasazovat vývojovou databázi se všemi daty v ní do produkčního prostředí, protože většina dat v nich je pravděpodobně pouze pro účely testování. Například názvy studentů v testovací databázi jsou fiktivní. Na druhé straně často nemůžete nasadit pouze databázovou strukturu bez jakýchkoli dat. Některá data v testovací databázi můžou být skutečná data a musí se nacházet, když uživatelé začnou aplikaci používat. Vaše databáze může mít například tabulku, která obsahuje platné hodnoty úrovně nebo názvy skutečných oddělení.

Chcete-li tento běžný scénář simulovat, nakonfigurujete metodu Migrace Code First `Seed`, která vloží do databáze pouze data, která mají být v produkčním prostředí. Tato `Seed` metoda by neměla vkládat testovací data, protože se spustí v produkčním prostředí po Code First vytvoří databázi v produkčním prostředí.

V dřívějších verzích Code First před vydáním migrace bylo běžné, že `Seed` metody pro vkládání testovacích dat, protože při vývoji se při každé změně modelu musela tato databáze zcela odstranit a znovu vytvořit úplně od začátku. Při Migrace Code First se testovací data uchovávají po změnách databáze, takže včetně testovacích dat v metodě `Seed` není nutné. Projekt, který jste stáhli, používá metodu zahrnující všechna data v metodě `Seed` třídy inicializátoru. V tomto kurzu zakážete tuto třídu inicializátoru a povolíte migrace. Pak aktualizujete `Seed` metodu ve třídě konfigurace Migraces tak, že vloží jenom data, která chcete vložit do produkčního prostředí.

Následující diagram znázorňuje schéma databáze aplikace:

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

V těchto kurzech předpokládáme, že při prvním nasazení webu by měly být tabulky `Student` a `Enrollment` prázdné. Ostatní tabulky obsahují data, která musí být předem načtena při provozu aplikace.

### <a name="disable-the-initializer"></a>Zakázat inicializátor

Vzhledem k tomu, že budete používat Migrace Code First, nemusíte používat `DropCreateDatabaseIfModelChanges` Code First inicializátor. Kód pro tento inicializátor je v souboru *SchoolInitializer.cs* v projektu CONTOSOUNIVERSITY. dal. Nastavení v prvku `appSettings` souboru *Web. config* způsobí, že se tento inicializátor spustí pokaždé, když se aplikace pokusí o přístup k databázi poprvé:

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

Otevřete soubor *Web. config* aplikace a odeberte nebo odkomentujte `add` element, který určuje třídu inicializátoru Code First. `appSettings` element teď vypadá takto:

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> Dalším způsobem, jak určit třídu inicializátoru, je to provést voláním `Database.SetInitializer` v metodě `Application_Start` v souboru *Global. asax* . Pokud povolujete migrace v projektu, který používá tuto metodu k určení inicializátoru, odeberte tento řádek kódu.

> [!NOTE]
> Pokud používáte Visual Studio 2013, přidejte následující kroky mezi kroky 2 a 3: (a) v PMC zadáním příkazu Update-Package EntityFramework-verze 6.1.1 získáte aktuální verzi EF. Pak (b) Sestavte projekt, abyste získali seznam chyb sestavení a opravili je. Odstraňte příkazy using pro obory názvů, které už neexistují, klikněte pravým tlačítkem myši a kliknutím na tlačítko vyřešit přidejte příkazy using, kde jsou potřeba, a změňte výskyty položky System. data. EntityState na System. data. entity. EntityState.

### <a name="enable-code-first-migrations"></a>Povolit Migrace Code First

1. Ujistěte se, že projekt ContosoUniversity (ne ContosoUniversity. DAL) je nastaven jako spouštěný projekt. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt ContosoUniversity a vyberte **nastavit jako spouštěný projekt**. Migrace Code First se podívá na spouštěný projekt, aby se našel připojovací řetězec databáze.
2. V nabídce **nástroje** vyberte **správce balíčků NuGet** > **konzolu Správce balíčků**.

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. V horní části okna **konzoly Správce balíčků** vyberte jako výchozí projekt CONTOSOUNIVERSITY. dal a potom v `PM>`ovém řádku zadejte "Enable-migrations" (Povolit – migrace).

    ![Enable – migrace – příkaz](preparing-databases/_static/image4.png)

    (Pokud se zobrazí chyba s informací o tom, že příkaz *Enable-migrations* není známý, zadejte příkaz *Update-Package EntityFramework-REINSTALL* a zkuste to znovu.)

    Tento příkaz vytvoří složku *migrace* v projektu CONTOSOUNIVERSITY. dal a umístí ji do složky dva soubory: soubor *Configuration.cs* , který můžete použít ke konfiguraci migrace, a soubor *InitialCreate.cs* pro první migraci, která vytváří databázi.

    ![Složka migrace](preparing-databases/_static/image5.png)

    Projekt DAL jste vybrali v rozevíracím seznamu **výchozí projekt** **konzoly Správce balíčků** , protože příkaz `enable-migrations` musí být spuštěn v projektu, který obsahuje třídu Code First Context. Když je tato třída v projektu knihovny tříd, Migrace Code First vyhledá připojovací řetězec databáze ve spouštěcím projektu pro řešení. V řešení ContosoUniversity byl webový projekt nastaven jako spouštěný projekt. Pokud nechcete určit projekt, který má připojovací řetězec jako spouštěný projekt v aplikaci Visual Studio, můžete zadat spouštěný projekt v příkazu PowerShellu. Chcete-li zobrazit syntaxi příkazu, zadejte příkaz `get-help enable-migrations`.

    Příkaz `enable-migrations` automaticky vytvořil první migraci, protože databáze již existuje. Alternativou je, že migrace vytvoří databázi. K tomu použijte **Průzkumník serveru** nebo **Průzkumník objektů systému SQL Server** k odstranění databáze ContosoUniversity před povolením migrace. Po povolení migrace vytvořte první migraci ručně zadáním příkazu Add-Migration InitialCreate. Databázi pak můžete vytvořit zadáním příkazu "Update-Database".

### <a name="set-up-the-seed-method"></a>Nastavení metody osazení

Pro účely tohoto kurzu přidáte pevná data přidáním kódu do metody `Seed` třídy Migrace Code First `Configuration`. Migrace Code First volá metodu `Seed` po každé migraci.

Vzhledem k tomu, že metoda `Seed` se spouští po každé migraci, už jsou v tabulkách data po první migraci. Chcete-li tuto situaci zpracovat, použijte metodu `AddOrUpdate` k aktualizaci řádků, které již byly vloženy, nebo je vložte, pokud ještě neexistují. Metoda `AddOrUpdate` možná není nejlepší volbou pro váš scénář. Další informace najdete v tématu povýšení [metody EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) na blogu Julie Lerman.

1. Otevřete soubor *Configuration.cs* a nahraďte komentáře v metodě `Seed` následujícím kódem:

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. Odkazy na `List` mají červené vlnovky pod nimi, protože ještě nemáte příkaz `using` pro svůj obor názvů. Klikněte pravým tlačítkem myši na jednu z instancí `List` a klikněte na možnost **vyřešit**a pak klikněte na možnost **použít System. Collections. Generic**.

    ![Vyřešit pomocí příkazu Using](preparing-databases/_static/image6.png)

    Tento výběr nabídky přidá následující kód do příkazů `using` v horní části souboru.

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. Stisknutím kombinace kláves CTRL + SHIFT + B Sestavte projekt.

Projekt je nyní připraven k nasazení databáze *ContosoUniversity* . Po nasazení aplikace, při prvním spuštění a přechodu na stránku, která přistupuje k databázi, Code First vytvoří databázi a spustí tuto metodu `Seed`.

> [!NOTE]
> Přidání kódu do metody `Seed` je jedním z mnoha způsobů, jak vložit pevná data do databáze. Alternativou je přidání kódu do `Up` a `Down` metody každé migrační třídy. Metody `Up` a `Down` obsahují kód, který implementuje změny databáze. Příklady najdete v kurzu [nasazení aktualizace databáze](deploying-a-database-update.md) .
> 
> Můžete také napsat kód, který provede příkazy SQL pomocí metody `Sql`. Například pokud jste přidávali sloupec rozpočet do tabulky oddělení a chtěli jste v rámci migrace inicializovat všechny rozpočty oddělení $1 000,00, můžete do metody `Up` pro tuto migraci přidat následující řádek kódu:
> 
> `Sql("UPDATE Department SET Budget = 1000");`

## <a name="create-scripts-for-membership-database-deployment"></a>Vytváření skriptů pro nasazení databáze členství

Společnost Contoso University používá k ověřování a autorizaci uživatelů systém členství v ASP.NET a ověřování pomocí formulářů. Stránka **aktualizovat kredity** je přístupná pouze uživatelům, kteří jsou v roli správce.

Spusťte aplikaci a klikněte na **kurzy**a pak klikněte na **aktualizovat kredity**.

![Kliknout na aktualizovat kredity](preparing-databases/_static/image7.png)

**Přihlašovací** stránka se zobrazí, protože stránka **aktualizovat kredity** vyžaduje oprávnění správce.

Jako uživatelské jméno zadejte *admin* a jako heslo *devpwd* a klikněte na **Přihlásit**se.

![Přihlašovací stránka](preparing-databases/_static/image8.png)

Zobrazí se stránka **aktualizovat kredity** .

![Stránka aktualizace kreditů](preparing-databases/_static/image9.png)

Informace o uživatelích a rolích jsou v databázi *ASPNET-ContosoUniversity* , která je určena připojovacím řetězcem **DefaultConnection** v souboru *Web. config* .

Tato databáze není spravovaná nástrojem Entity Framework Code First, takže je nemůžete nasadit pomocí migrace. K nasazení schématu databáze použijete poskytovatele dbDacFx a nakonfigurujete profil publikování pro spuštění skriptu, který bude vkládat počáteční data do tabulek databáze.

> [!NOTE]
> Nový systém členství v ASP.NET (nyní nazvaný ASP.NET Identity) byl představen s Visual Studio 2013. Nový systém umožňuje zachovat obě tabulky aplikace i členství ve stejné databázi a můžete použít Migrace Code First k nasazení obou. Ukázková aplikace používá starší systém členství ASP.NET, který se nedá nasadit pomocí Migrace Code First. Postupy pro nasazení této databáze členství platí také pro všechny další scénáře, ve kterých aplikace potřebuje nasadit databázi SQL Server, kterou nevytvořila Entity Framework Code First.

To je moc, ale nechcete, aby byla stejná data v produkčním prostředí, která máte ve vývoji. Při prvním nasazení lokality je běžné vyloučit ze všech nebo všech uživatelských účtů, které vytvoříte pro testování. Proto stažený projekt má dvě databáze členství: *ASPNET-ContosoUniversity. mdf* s vývojářskými uživateli a *ASPNET-ContosoUniversity-prod. mdf* s produkčními uživateli. V tomto kurzu se uživatelská jména shodují v obou databázích: *správce* i správce *.* Oba uživatelé mají heslo *devpwd* ve vývojové databázi a v *prodpwd* v provozní databázi.

Nasadíte vývojové uživatele do testovacího prostředí a produkčních uživatelů na přípravu a produkci. V tomto kurzu vytvoříte dva skripty SQL, jeden pro vývoj a jeden pro produkční prostředí a v pozdějších kurzech nakonfigurujete proces publikování tak, aby je spouštěl.

> [!NOTE]
> Databáze členství ukládá hash hesla účtů. Aby bylo možné nasadit účty z jednoho počítače do jiného, je nutné zajistit, aby rutiny hash nevytvářely na cílovém serveru různé hodnoty hash, než na zdrojovém počítači. Když použijete ASP.NET Universal Providers, vygenerují se stejné hodnoty hash, pokud neměníte výchozí algoritmus. Výchozí algoritmus je HMACSHA256 a je určen v atributu **ověřování** elementu **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** v souboru Web. config.

Skripty pro nasazení dat můžete vytvořit ručně pomocí SQL Server Management Studio (SSMS) nebo pomocí nástroje třetí strany. V tomto zbývajícím kurzu se dozvíte, jak to udělat v SSMS, ale pokud nechcete instalovat a používat SSMS, můžete získat skripty z dokončené verze projektu a přeskočit do části, kam je uložíte ve složce řešení.

Pokud chcete nainstalovat SSMS, nainstalujte ho z [webu Download Center: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) kliknutím na [ENU\x64\SQLManagementStudio\_x64\_CSY. exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe) nebo [ENU\x86\SQLManagementStudio\_x86\_CSY. exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe). Pokud pro svůj systém zvolíte nesprávný systém, instalace se nezdaří a můžete vyzkoušet druhý.

(Upozorňujeme, že jde o stažení 600 megabajtů. Instalace může trvat dlouhou dobu a bude vyžadovat restartování počítače.)

Na první stránce centra instalace SQL Server klikněte na **nový SQL Server samostatnou instalaci nebo přidejte funkce do existující instalace**a postupujte podle pokynů a přijměte výchozí možnosti.

### <a name="create-the-development-database-script"></a>Vytvoření skriptu vývojové databáze

1. Spusťte SSMS.
2. V dialogovém okně **připojit k serveru** zadejte *(LocalDB) \V11.0* jako **název serveru**, ponechte **ověřování** nastavené na **ověřování systému Windows**a pak klikněte na **připojit**.

    ![SSMS připojit k serveru](preparing-databases/_static/image10.png)
3. V okně **Průzkumník objektů** rozbalte **databáze**, klikněte pravým tlačítkem na **ASPNET-ContosoUniversity**, klikněte na **úlohy**a pak klikněte na **vygenerovat skripty**.

    ![SSMS generovat skripty](preparing-databases/_static/image11.png)
4. V dialogovém okně **generovat a publikovat skripty** klikněte na **nastavit možnosti skriptování**.

    Krok **zvolit objekty** můžete přeskočit, protože výchozí hodnota je **skripty celá databáze a všechny databázové objekty** a to vše, co chcete.
5. Klikněte na **Upřesnit**.

    ![Možnosti skriptování SSMS](preparing-databases/_static/image12.png)
6. V dialogovém okně **Pokročilé možnosti skriptování** přejděte dolů na položku **typy dat a skript**a v rozevíracím seznamu klikněte na možnost **pouze data** .
7. Změňte **databázi použití skriptu** na **false**. Příkazy USE nejsou platné pro Azure SQL Database a nejsou potřebné pro SQL Server Express nasazení v testovacím prostředí.

    ![Pouze data skriptu SSMS bez příkazu USE](preparing-databases/_static/image13.png)
8. Klikněte na tlačítko **OK**.
9. V dialogovém okně **generovat a publikovat skripty** se v poli **název souboru** určuje, kde se skript vytvoří. Změňte cestu ke složce řešení (složka, která obsahuje soubor ContosoUniversity. sln) a název souboru na *ASPNET-data-dev. SQL*.
10. Kliknutím na **Další** přejděte na kartu **Souhrn** a vytvořte skript znovu kliknutím na **Další** .

    ![Skript SSMS se vytvořil.](preparing-databases/_static/image14.png)
11. Klikněte na **Finish** (Dokončit).

### <a name="create-the-production-database-script"></a>Vytvoření produkčního skriptu databáze

Vzhledem k tomu, že jste projekt nespouštěli s provozní databází, není dosud připojen k instanci LocalDB. Proto je třeba nejprve připojit databázi.

1. V **Průzkumník objektů**SSMS klikněte pravým tlačítkem na **databáze** a klikněte na **připojit**.

    ![SSMS připojit](preparing-databases/_static/image15.png)
2. V dialogovém okně **připojit databáze** klikněte na **Přidat** a potom přejděte k souboru *ASPNET-ContosoUniversity-prod. mdf* ve složce *App\_data* .

     ![SSMS přidat soubor. mdf pro připojení](preparing-databases/_static/image16.png)
3. Klikněte na tlačítko **OK**.
4. Použijte stejný postup, který jste použili dříve, k vytvoření skriptu pro produkční soubor. Název souboru skriptu *ASPNET-data-prod. SQL*.

## <a name="summary"></a>Souhrn

Obě databáze jsou teď připravené k nasazení a ve složce řešení máte dva skripty pro nasazení dat.

![Skripty pro nasazení dat](preparing-databases/_static/image17.png)

V následujícím kurzu nakonfigurujete nastavení projektu, která mají vliv na nasazení, a nastavíte automatickou transformaci souborů *Web. config* pro nastavení, která se musí v nasazené aplikaci lišit.

## <a name="more-information"></a>Další informace

Další informace o NuGet najdete v tématu [Správa knihoven projektů pomocí NuGet](https://msdn.microsoft.com/magazine/hh547106.aspx) a [dokumentace k NuGet](http://docs.nuget.org/docs/start-here/overview). Pokud nechcete používat NuGet, budete se muset dozvědět, jak analyzovat balíček NuGet, abyste zjistili, co má při instalaci. (Například může nakonfigurovat transformace *souboru Web. config* , nakonfigurovat skripty prostředí PowerShell tak, aby běžely v době sestavování atd.) Další informace o tom, jak NuGet funguje, najdete v tématu [Vytvoření a publikování balíčku](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) a [konfiguračního souboru a transformací zdrojového kódu](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations).

> [!div class="step-by-step"]
> [Předchozí](introduction.md)
> [Další](web-config-transformations.md)
