---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: Použití migrace EF v aplikaci ASP.NET MVC a nasazení do Azure'
author: tdykstra
description: V tomto kurzu povolíte Code First migrace a nasadíte aplikaci do cloudu v Azure.
ms.author: riande
ms.date: 01/16/2019
ms.topic: tutorial
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 989dd0f0e18b338be057b9c5657586eff996d8ea
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000768"
---
# <a name="tutorial-use-ef-migrations-in-an-aspnet-mvc-app-and-deploy-to-azure"></a>Kurz: Použití migrace EF v aplikaci ASP.NET MVC a nasazení do Azure

Proto byla webová aplikace Contoso University Sample spuštěná místně v IIS Express ve vývojovém počítači. Chcete-li zajistit, aby byla skutečná aplikace k dispozici ostatním uživatelům pro použití přes Internet, je nutné ji nasadit na poskytovatele hostování webů. V tomto kurzu povolíte Code First migrace a nasadíte aplikaci do cloudu v Azure:

- Povolte Migrace Code First. Funkce migrace umožňuje změnit datový model a nasadit změny v produkčním prostředí aktualizací schématu databáze bez nutnosti vyřadit a znovu vytvořit databázi.
- Nasaďte do Azure. Tento krok je nepovinný. můžete pokračovat ve zbývajících kurzech, aniž byste museli projekt nasadit.

Pro nasazení doporučujeme použít proces průběžné integrace se správou zdrojových kódů, ale v tomto kurzu se tato témata nevztahují. Další informace najdete v kapitolách [správy zdrojového kódu](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) a [průběžné integrace](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) [vytváření skutečných cloudových aplikací s Azure](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Povolit Code First migrace
> * Nasazení aplikace v Azure (volitelné)

## <a name="prerequisites"></a>Požadavky

- [Odolnost připojení a zachycení příkazů](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-code-first-migrations"></a>Povolit Code First migrace

Při vývoji nové aplikace se datový model často mění a pokaždé, když se model změní, se nesynchronizuje s databází. Nakonfigurovali jste Entity Framework pro automatické vyřazení a opětovné vytvoření databáze pokaždé, když změníte datový model. Když přidáváte, odebíráte nebo měníte třídy entit nebo změníte `DbContext` třídu, při příštím spuštění aplikace se automaticky odstraní existující databáze, vytvoří se nová, která odpovídá modelu, a jeho semena s testovacími daty.

Tato metoda uchování databáze v synchronizaci s datovým modelem funguje dobře, dokud aplikaci nenainstalujete do produkčního prostředí. Když je aplikace spuštěná v produkčním prostředí, obvykle ukládá data, která chcete zachovat, a nechcete přijít o všechny pokaždé, když uděláte změnu, jako je přidání nového sloupce. Funkce [migrace Code First](https://msdn.microsoft.com/data/jj591621) tento problém vyřeší tím, že povolí Code First aktualizaci schématu databáze místo vyřazení a opětovného vytváření databáze. V tomto kurzu nasadíte aplikaci a připravíte ji na to, abyste povolili migrace.

1. Zakažte inicializátor, který jste nastavili dříve, zadáním komentáře nebo `contexts` odstraněním elementu, který jste přidali do souboru Web. config aplikace.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. V souboru *Web. config* aplikace změňte také název databáze v připojovacím řetězci na ContosoUniversity2.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    Tato změna nastaví projekt tak, aby první migrace vytvořila novou databázi. To se nevyžaduje, ale uvidíte později, proč je to dobré.
3. Z **nástroje** nabídce vyberte možnost **Správce balíčků NuGet** > **Konzola správce balíčků**.

1. `PM>` Na příkazovém řádku zadejte následující příkazy:

    ```text
    enable-migrations
    add-migration InitialCreate
    ```

    Příkaz vytvoří složku *migrace* v projektu ContosoUniversity a vloží do této složky soubor Configuration.cs, který můžete upravit a nakonfigurovat migrace. `enable-migrations`

    (Pokud jste nenalezli krok výše, který vás přesměruje na změnu názvu databáze, migrace nalezne existující databázi a automaticky provede `add-migration` příkaz. To je v pořádku, jenom to znamená, že před nasazením databáze nespustíte test migrace kódu. Později po spuštění `update-database` příkazu se nic nestane, protože databáze již existuje.)

    Otevřete soubor *ContosoUniversity\Migrations\Configuration.cs* . Podobně jako Třída inicializátoru, kterou jste viděli dříve `Configuration` , třída `Seed` obsahuje metodu.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    Účelem metody [počáteční](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) hodnoty je umožnit vložení nebo aktualizaci dat testu po Code First vytvoření nebo aktualizace databáze. Metoda je volána při vytvoření databáze a pokaždé, když je schéma databáze aktualizováno po změně datového modelu.

### <a name="set-up-the-seed-method"></a>Nastavení metody osazení

Když vyřadíte a znovu vytvoříte databázi pro každou změnu datového modelu, použijete `Seed` metodu třídy inicializátoru pro vložení testovacích dat, protože po každé změně modelu je databáze vyřazena a všechna testovací data budou ztracena. Při Migrace Code First se testovací data uchovávají po změnách databáze, takže včetně testovacích dat v metodě [osazení](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) obvykle není nutné. Ve skutečnosti nechcete `Seed` , aby metoda vložila testovací data, pokud budete používat migrace k nasazení databáze do produkčního prostředí, protože tato `Seed` Metoda bude spuštěna v produkčním prostředí. V takovém případě chcete `Seed` , aby metoda vložila do databáze pouze data, která potřebujete v produkčním prostředí. Například můžete chtít, aby databáze zahrnovala názvy vlastních oddělení v `Department` tabulce, když bude aplikace k dispozici v produkčním prostředí.

Pro účely tohoto kurzu budete pro nasazení používat migrace, ale vaše `Seed` metoda bude přesto vkládat testovací data, aby bylo snazší zjistit, jak funguje funkce aplikace bez nutnosti ručního vkládání hodně dat.

1. Nahraďte obsah souboru *Configuration.cs* následujícím kódem, který načte testovací data do nové databáze.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    Metoda [počáteční](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) hodnoty přebírá objekt kontextu databáze jako vstupní parametr a kód v metodě používá tento objekt k přidání nových entit do databáze. Pro každý typ entity kód vytvoří kolekci nových entit, přidá je do příslušné vlastnosti [negenerickými](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) a poté uloží změny do databáze. Není nutné volat metodu [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) za každou skupinu entit, jak je zde provedeno, ale to vám pomůže najít zdroj problému, pokud dojde k výjimce, když kód zapisuje do databáze.

    Některé příkazy, které vkládají data, používají metodu [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) k provedení operace "Upsert". Vzhledem k `Seed` tomu, že se metoda spouští při `update-database` každém spuštění příkazu, obvykle po každé migraci, nemůžete jenom vkládat data, protože řádky, které se pokoušíte přidat, už po první migraci vytvářející databázi budou. Operace "Upsert" zabraňuje chybám, které by byly provedeny při pokusu o vložení řádku, který již existuje, ale ***přepíše*** všechny změny dat, které jste mohli provést při testování aplikace. S testovacími daty v některých tabulkách možná nebudete chtít, aby došlo k tomu, že v některých případech změníte data při testování, které chcete po aktualizaci databáze zůstat. V takovém případě chcete provést operaci podmíněného vložení: vložte řádek pouze v případě, že ještě neexistuje. Metoda počáteční hodnoty používá obě přístupy.

    První parametr předaný metodě [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) určuje vlastnost, která má být použita pro kontrolu, zda řádek již existuje. Pro data testovacího studenta, která poskytujete, `LastName` se dá vlastnost použít pro tento účel, protože každé příjmení v seznamu je jedinečné:

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    Tento kód předpokládá, že poslední názvy jsou jedinečné. Pokud ručně přidáte studenta s duplicitním posledním názvem, při příštím provedení migrace se zobrazí následující výjimka:

    **Sekvence obsahuje více než jeden element.**

    Informace o tom, jak zpracovat redundantní data, jako jsou například dva studenti s názvem "Alexander Carson", naleznete v tématu [osazení a ladění Entity Framework (EF) databáze](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) na blogu Rick Anderson. Další informace o této `AddOrUpdate` metodě najdete v tématu s informací o [metodě EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) na blogu Julie Lerman.

    Kód, který vytváří `Enrollment` entity, předpokládá, že `ID` máte hodnotu `students` v entitách v kolekci, i když jste tuto vlastnost nenastavili v kódu, který vytváří kolekci.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    Zde můžete použít `ID` vlastnost, `ID` protože hodnota je nastavena `students` při volání `SaveChanges` kolekce. EF automaticky získá hodnotu primárního klíče, když vloží entitu do databáze a aktualizuje `ID` vlastnost entity v paměti.

    Kód, který přidá každou `Enrollment` entitu `Enrollments` do sady `AddOrUpdate` entit, nepoužívá metodu. Kontroluje, zda entita již existuje, a vloží entitu, pokud neexistuje. Tento přístup zachovává změny ve třídě registrace pomocí uživatelského rozhraní aplikace. Kód projde každým členem `Enrollment` [seznamu](https://msdn.microsoft.com/library/6sh2ey19.aspx) a pokud se registrace nenalezne v databázi, přidá registraci do databáze. Při první aktualizaci databáze bude databáze prázdná, takže se přidá každá registrace.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

2. Sestavte projekt.

### <a name="execute-the-first-migration"></a>Provedení první migrace

Při spuštění `add-migration` příkazu migrace vygenerovala kód, který by vytvořil databázi od začátku. Tento kód je také ve složce *migraces* v souboru s názvem  *&lt;TimeStamp&gt;\_InitialCreate.cs*. Metoda třídy vytvoří tabulky databáze, které odpovídají sadám `Down` entit datového modelu, a metoda je odstraní. `InitialCreate` `Up`

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Migrace volá `Up` metodu, která implementuje změny datového modelu pro migraci. Když zadáte příkaz pro vrácení aktualizace, migrace volá `Down` metodu.

Toto je počáteční migrace, která byla vytvořena při zadání `add-migration InitialCreate` příkazu. Parametr (`InitialCreate` v příkladu) se používá pro název souboru a může být libovolný, co potřebujete. obvykle si vybíráte slovo nebo frázi, která shrnuje, co se v migraci provádí. Můžete třeba pojmenovat pozdější AddDepartmentTable &quot;&quot;migrace.

Pokud jste vytvořili počáteční migraci i v případě, že databáze již existuje, je vytvořen kód pro vytvoření databáze, ale nemusí být spuštěn, protože databáze již odpovídá datovému modelu. Když nasadíte aplikaci do jiného prostředí, kde databáze ještě neexistuje, tento kód se spustí, aby se vytvořila vaše databáze, takže je dobré ho nejdřív otestovat. To je důvod, proč jste změnili název databáze v připojovacím řetězci dříve&mdash;, takže migrace mohou vytvořit nové od začátku.

1. V okně **konzoly Správce balíčků** zadejte následující příkaz:

    `update-database`

    Příkaz spustí metodu pro vytvoření databáze `Seed` a poté spustí metodu pro naplnění databáze. `Up` `update-database` Po nasazení aplikace se stejný proces spustí automaticky v produkčním prostředí, jak je uvedeno v následující části.
2. Pomocí **Průzkumník serveru** můžete zkontrolovat databázi jako v prvním kurzu a spustit aplikaci, abyste ověřili, že všechno pořád funguje stejně jako dřív.

## <a name="deploy-to-azure"></a>Nasazení do Azure

Proto byla aplikace spuštěna místně v IIS Express ve vývojovém počítači. Aby ho mohli používat i ostatní uživatelé přes Internet, musíte ho nasadit do poskytovatele hostování webů. V této části kurzu ho nasadíte do Azure. Tato část je volitelná. Můžete to přeskočit a pokračovat v následujícím kurzu nebo můžete upravit pokyny v této části pro jiného poskytovatele hostingu podle vašeho výběru.

### <a name="use-code-first-migrations-to-deploy-the-database"></a>Nasazení databáze pomocí Code First migrace

K nasazení databáze budete používat Migrace Code First. Když vytvoříte profil publikování, který použijete ke konfiguraci nastavení pro nasazení ze sady Visual Studio, vyberete zaškrtávací políčko s názvem **aktualizace databáze**. Toto nastavení způsobí, že proces nasazení automaticky konfiguruje soubor *Web. config* aplikace na cílovém serveru tak, aby Code First používal `MigrateDatabaseToLatestVersion` třídu inicializátoru.

Visual Studio během procesu nasazování neprovádí žádnou práci s databází, zatímco kopíruje projekt na cílový server. Když spustíte nasazenou aplikaci a přistupuje k databázi poprvé po nasazení, Code First zkontroluje, jestli databáze odpovídá datovému modelu. Pokud dojde k neshodě, Code First automaticky vytvoří databázi (Pokud ještě neexistuje) nebo aktualizuje schéma databáze na nejnovější verzi (Pokud databáze existuje, ale neodpovídá modelu). Pokud aplikace implementuje `Seed` metodu migrace, metoda se spustí po vytvoření databáze nebo aktualizaci schématu.

`Seed` Metoda migrace vloží testovací data. Pokud jste nasadili do provozního prostředí, budete muset změnit `Seed` metodu tak, aby byla vložena pouze data, která chcete vložit do provozní databáze. Například v aktuálním datovém modelu možná budete chtít mít reálné kurzy, ale fiktivní studenty ve vývojové databázi. Můžete napsat `Seed` metodu pro načtení ve vývoji a pak před nasazením do produkčního prostředí odkomentovat fiktivní studenty. Nebo můžete napsat `Seed` metodu pro načtení pouze kurzů a zadat fiktivní studenty do testovací databáze ručně pomocí uživatelského rozhraní aplikace.

### <a name="get-an-azure-account"></a>Získat účet Azure

Budete potřebovat účet Azure. Pokud ho ještě nemáte, ale máte předplatné sady Visual Studio, můžete [si aktivovat výhody](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/
)předplatného. V opačném případě můžete během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v tématu [bezplatnou zkušební verzi Azure](https://azure.microsoft.com/free/).

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>Vytvoření webu a databáze SQL v Azure

Vaše webová aplikace v Azure se spustí ve sdíleném hostitelském prostředí, což znamená, že se spustí na virtuálních počítačích, které jsou sdílené s jinými klienty Azure. Sdílené hostitelské prostředí představuje nízký nákladový způsob, jak začít v cloudu. Později, pokud se webový provoz zvýší, aplikace může škálovat tak, aby splňovala nutnost spuštění na vyhrazených virtuálních počítačích. Pokud chcete získat další informace o možnostech cen pro Azure App Service, přečtěte si [App Service ceny](https://azure.microsoft.com/pricing/details/app-service/).

Databázi nasadíte do služby Azure SQL Database. SQL Database je cloudová služba relačních databází, která je založená na technologii SQL Server. Nástroje a aplikace, které pracují s SQL Server, fungují také s SQL Database.

1. V [portál pro správu Azure](https://portal.azure.com)zvolte na levé straně možnost **vytvořit prostředek** a potom v podokně **nové** (nebo v okně) zvolte **Zobrazit vše** .zobrazí se všechny dostupné prostředky. V části **Web** okna **vše** vyberte **Web App + SQL** . Nakonec klikněte na tlačítko **vytvořit**.

    ![Vytvořit prostředek na webu Azure Portal](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/create-azure-resource.png)

   Otevře se formulář pro vytvoření nové **nové webové aplikace a prostředku SQL** .

2. Do pole **název aplikace** zadejte řetězec, který chcete použít jako jedinečnou adresu URL pro vaši aplikaci. Úplná adresa URL se skládá z toho, co tady zadáte, a navíc k výchozí doméně Azure App Services (. azurewebsites.net). Pokud už je **název aplikace** zabraný, Průvodce vás upozorní na červenou zprávu s *názvem aplikace není k dispozici* . Pokud je **název aplikace** k dispozici, zobrazí se zelená značka zaškrtnutí.

3. V poli **předplatné** vyberte předplatné Azure, ve kterém chcete **App Service** umístit.

4. V textovém poli **Skupina prostředků** vyberte skupinu prostředků nebo vytvořte novou. Toto nastavení určuje, které datové centrum bude web běžet v. Další informace o skupinách prostředků najdete v tématu [skupiny prostředků](/azure/azure-resource-manager/resource-group-overview#resource-groups).

5. Kliknutím na **App Service** *oddíl App Service*vytvořte nový **App Service plán** (můžeto být stejný název jako App Service), **umístění**a **cenová úroveň** (bezplatná možnost).

6. Klikněte na **SQL Database**a pak zvolte **vytvořit novou databázi** nebo vyberte existující databázi.

7. Do pole **název** zadejte název vaší databáze.
8. Klikněte na pole **cílový server** a pak vyberte **vytvořit nový server**. Případně, pokud jste dříve vytvořili server, můžete tento server vybrat ze seznamu dostupných serverů.
9. Vyberte možnost **cenová úroveň** , vyberte možnost *Free*. Pokud potřebujete další prostředky, je možné databázi kdykoli škálovat. Další informace o cenách Azure SQL najdete v tématu [Azure SQL Database ceny](https://azure.microsoft.com/pricing/details/sql-database/managed/).
10. Podle [](/sql/relational-databases/collations/collation-and-unicode-support) potřeby upravte kolaci.
11. Zadejte **uživatelské jméno správce SQL** a **heslo správce SQL**.

    - Pokud jste vybrali **nový SQL Database Server**, definujte nové jméno a heslo, které použijete později při přístupu k databázi.
    - Pokud jste vybrali Server, který jste vytvořili dříve, zadejte přihlašovací údaje pro tento server.

12. Kolekce telemetrie se dá povolit pro App Service pomocí Application Insights. S malou konfigurací Application Insights shromažďuje cenné informace o událostech, výjimkách, závislostech, žádostech a trasování. Další informace o Application Insights najdete v tématu [Azure monitor](https://azure.microsoft.com/services/monitor/).
13. Kliknutím na **vytvořit** v dolní části označíte, že jste hotovi.

    Portál pro správu se vrátí na stránku řídicího panelu a v oblasti **oznámení** v horní části stránky se zobrazí, že se web vytváří. Po delší dobu (obvykle méně než minutu) se zobrazí oznámení o úspěšném nasazení. V navigačním panelu vlevo se nový App Service zobrazí v části **App Services** a v části **databáze SQL** se zobrazí nová databáze SQL.

### <a name="deploy-the-app-to-azure"></a>Nasazení aplikace do Azure

1. V aplikaci Visual Studio klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a v místní nabídce vyberte **publikovat** .

2. Na stránce **Vyberte cíl publikování** zvolte **App Service** a pak **Vyberte existující**a pak zvolte **publikovat**.

    ![Výběr cílové stránky pro publikování](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/publish-select-existing-azure-app-service.png)

3. Pokud jste ještě nepřidali předplatné Azure v aplikaci Visual Studio, proveďte kroky na obrazovce. Tyto kroky umožňují aplikaci Visual Studio připojit se k předplatnému Azure, takže seznam **App Services** bude obsahovat váš web.

4. Na stránce **App Service** vyberte **předplatné** , do kterého jste přidali App Service. V části **zobrazení**vyberte **Skupina prostředků**. Rozbalte skupinu prostředků, do které jste přidali App Service, a pak vyberte App Service. Pro publikování aplikace klikněte na **tlačítko OK** .

5. Okno **výstup** zobrazuje, jaké akce nasazení byly provedeny, a oznamuje úspěšné dokončení nasazení.

6. Po úspěšném nasazení se výchozí prohlížeč automaticky otevře na adrese URL nasazeného webu.

    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/cloud-app-browser.png)

    Vaše aplikace je teď spuštěná v cloudu.

V tuto chvíli se databáze *SchoolContext* vytvořila ve službě Azure SQL Database, protože jste vybrali **Execute migrace Code First (spouští se při spuštění aplikace)** . Soubor *Web. config* na nasazeném webu byl změněn tak, aby byl inicializátor [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) spuštěn při prvním načtení nebo zápisu dat do databáze (ke kterému došlo po výběru karty **Students** ):

![Soubor Web. config – výňatek](https://asp.net/media/4367421/mig.png)

Proces nasazení taky vytvořil nový připojovací řetězec *\_(SchoolContext DatabasePublish*migrace Code First), který se používá k aktualizaci schématu databáze a k osazení databáze.

![Připojovací řetězec v souboru Web. config](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

Nasazenou verzi souboru Web. config můžete najít na svém vlastním počítači v *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*. K nasazenému souboru *Web. config* se můžete dostat pomocí FTP. Pokyny najdete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio: Nasazení aktualizace](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)kódu. Postupujte podle pokynů, které začínají na používání nástroje FTP, potřebujete tři věci: adresa URL serveru FTP, uživatelské jméno a heslo. "

> [!NOTE]
> Webová aplikace neimplementuje zabezpečení, takže kdokoli, kdo najde adresu URL, může data změnit. Pokyny k zabezpečení webu najdete v tématu [nasazení zabezpečené aplikace ASP.NET MVC pomocí členství, protokolu OAuth a SQL Database do Azure](/aspnet/core/security/authorization/secure-data). Dalším lidem můžete zabránit v používání webu zastavením služby pomocí Portál pro správu Azure nebo **Průzkumník serveru** v aplikaci Visual Studio.

![Zastavit položku nabídky služby App Service](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/server-explorer-stop-app-service.png)

## <a name="advanced-migrations-scenarios"></a>Scénáře pokročilých migrací

Pokud nasadíte databázi tak, že automaticky spustíte migrace, jak je znázorněno v tomto kurzu, a nasazujete na web, který běží na více serverech, můžete získat více serverů, které se pokoušejí spustit migrace současně. Migrace jsou atomické, takže pokud se dva servery pokusí spustit stejnou migraci, bude jedna z nich úspěšná a druhá selže (za předpokladu, že operace nejde udělat dvakrát). V takovém případě, pokud se chcete těmto problémům vyhnout, můžete volat migrace ručně a nastavit vlastní kód tak, aby se stalo pouze jednou. Další informace najdete v tématu [spuštění a skriptování migrace z kódu](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/) na blogu Rowan Miller a [migrace. exe](/ef/ef6/modeling/code-first/migrations/migrate-exe) (pro provádění migrací z příkazového řádku).

Informace o dalších scénářích migrace najdete v tématu [migrace datových řad pro záznam dění](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)v/v.

## <a name="update-specific-migration"></a>Aktualizovat konkrétní migraci

`update-database -target MigrationName`

`update-database -target MigrationName` Příkaz spustí cílenou migraci.

## <a name="ignore-migration-changes-to-database"></a>Ignorovat změny migrace v databázi

`Add-migration MigrationName -ignoreChanges`

`ignoreChanges`Vytvoří prázdnou migraci s aktuálním modelem jako snímkem.

## <a name="code-first-initializers"></a>Inicializátory Code First

V části nasazení jste viděli, že se používá inicializátor [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) . Code First také poskytuje další inicializátory, včetně [metodu createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (výchozí), [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) (který jste použili dříve) a [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx). `DropCreateAlways` Inicializátor může být užitečný pro nastavení podmínek pro testování částí. Můžete také napsat vlastní Inicializátory a můžete zavolat inicializátor explicitně, pokud nechcete čekat, dokud aplikace nenačte nebo zapíše do databáze.

Další informace o inicializátorech naleznete v tématu [Principy inicializátorů databáze v Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm) a v kapitole 6 příručky [programovacího Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman a Rowan Miller.

## <a name="get-the-code"></a>Získat kód

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v prostředcích, které jsou doporučeny pro [přístup k datům ASP.NET](xref:whitepapers/aspnet-data-access-content-map).

## <a name="next-steps"></a>Další postup

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Povolené migrace Code First
> * Nasazení aplikace v Azure (volitelné)

V dalším článku se dozvíte, jak vytvořit složitější datový model pro aplikaci ASP.NET MVC.
> [!div class="nextstepaction"]
> [Vytvoření komplexnějšího datového modelu](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
