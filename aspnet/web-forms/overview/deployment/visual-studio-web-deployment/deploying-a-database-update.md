---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace databáze | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636822"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace databáze

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu provedete změnu v databázi a související změny kódu, otestujete změny v aplikaci Visual Studio a potom nasadíte aktualizaci do prostředí testování, přípravy a produkčního prostředí.

V tomto kurzu se nejprve dozvíte, jak aktualizovat databázi, která je spravovaná pomocí Migrace Code First, a později ukazuje, jak aktualizovat databázi pomocí poskytovatele dbDacFx.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](troubleshooting.md).

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a>Nasazení aktualizace databáze pomocí Migrace Code First

V této části přidáte sloupec data narození do `Person` základní třídy pro entity `Student` a `Instructor`. Pak aktualizujete stránku, která zobrazuje data instruktora, aby zobrazila nový sloupec. Nakonec nasadíte změny do testování, přípravy a výroby.

### <a name="add-a-column-to-a-table-in-the-application-database"></a>Přidání sloupce do tabulky v aplikační databázi

1. V projektu *ContosoUniversity. dal* otevřete *Person.cs* a na konci třídy `Person` přidejte následující vlastnost (před ní musí být dvě uzavírací složené závorky):

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    Dále aktualizujte metodu `Seed` tak, aby poskytovala hodnotu pro nový sloupec. Otevřete *Migrations\Configuration.cs* a nahraďte blok kódu, který začíná `var instructors = new List<Instructor>` s následujícím blokem kódu, který obsahuje informace o datu narození:

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. Sestavte řešení a pak otevřete okno **konzoly Správce balíčků** . Ujistěte se, že je ContosoUniversity. DAL stále vybraný jako **výchozí projekt**.
3. V okně **konzoly Správce balíčků** vyberte jako **výchozí projekt**možnost **ContosoUniversity. dal** a potom zadejte následující příkaz:

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou třídu `DbMigration` a v metodě `Up` můžete zobrazit kód, který vytvoří nový sloupec. Metoda `Up` vytvoří sloupec při implementaci změny a metoda `Down` odstraní sloupec při vrácení změny zpět.

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. Sestavte řešení a potom v okně **konzoly Správce balíčků** zadejte následující příkaz (Ujistěte se, že je projekt CONTOSOUNIVERSITY. dal stále vybraný):

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    Entity Framework spustí metodu `Up` a potom spustí metodu `Seed`.

### <a name="display-the-new-column-in-the-instructors-page"></a>Zobrazit nový sloupec na stránce instruktoři

1. V projektu ContosoUniversity otevřete *instruktory. aspx* a přidejte nové pole šablony, abyste zobrazili datum narození. Přidejte ho mezi ty pro datum přijetí a přiřazení kanceláře:

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    (Pokud se odsazení kódu nesynchronizuje, můžete stisknutím kláves CTRL-K a potom CTRL-D soubor automaticky znovu zformátovat.)
2. Spusťte aplikaci a klikněte na odkaz **instruktoři** .

    Po načtení stránky se zobrazí, že má nové pole data narození.

    ![Stránka instruktorů s DatumNarození](deploying-a-database-update/_static/image2.png)
3. Zavřete prohlížeč.

### <a name="deploy-the-database-update"></a>Nasazení aktualizace databáze

1. V **Průzkumník řešení** vyberte projekt ContosoUniversity.
2. Na panelu nástrojů **publikování webu jedním kliknutím** klikněte na profil publikování **testu** a pak klikněte na **Publikovat web**. (Pokud je panel nástrojů zakázaný, vyberte projekt ContosoUniversity v **Průzkumník řešení**.)

    Visual Studio nasadí aktualizovanou aplikaci a otevře se v prohlížeči na domovské stránce.
3. Spuštěním stránky **instruktory** ověřte, zda byla aktualizace úspěšně nasazena.

    Když se aplikace pokusí o přístup k databázi pro tuto stránku, Code First aktualizuje schéma databáze a spustí metodu `Seed`. Po zobrazení stránky se zobrazí očekávaný sloupec **Datum narození** s kalendářními daty.
4. Na panelu nástrojů **publikování webu jedním kliknutím** klikněte na **pracovní** profil publikování a pak klikněte na **Publikovat web**.
5. Spuštěním stránky **instruktoři** v části fázování ověříte, že se aktualizace úspěšně nasadila.
6. Na panelu nástrojů pro **publikování na webu** klikněte **na publikovat profil publikování a** pak klikněte na **Publikovat web**.
7. Spusťte stránku **instruktoři** v produkčním prostředí, abyste ověřili, že se aktualizace úspěšně nasadila.

    V případě skutečné aktualizace produkčních aplikací, která zahrnuje změnu v databázi, byste taky během nasazení normálně převzali aplikaci v režimu offline pomocí *aplikace\_offline. htm*, jak jste viděli v předchozím kurzu.

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a>Nasazení aktualizace databáze pomocí poskytovatele dbDacFx

V této části přidáte sloupec *Komentáře* do tabulky *uživatelů* v databázi členství a vytvoříte stránku, která vám umožní zobrazit a upravit komentáře pro každého uživatele. Pak nasadíte změny do testování, přípravy a výroby.

### <a name="add-a-column-to-a-table-in-the-membership-database"></a>Přidání sloupce do tabulky v databázi členství

1. V aplikaci Visual Studio otevřete **Průzkumník objektů systému SQL Server**.
2. Rozbalte **(LocalDB) \v11.0**, rozbalte **databáze**, rozbalte **ASPNET-ContosoUniversity** (ne **ASPNET-ContosoUniversity-prod**) a pak rozbalte **tabulky**.

    Pokud nevidíte **(LocalDB) \v11.0** pod uzlem **SQL Server** , klikněte pravým tlačítkem na uzel **SQL Server** a klikněte na **Přidat SQL Server**. V dialogovém okně **připojit k serveru** zadejte *(LocalDB) \V11.0* jako **název serveru**a pak klikněte na **připojit**.

    Pokud nevidíte **ASPNET-ContosoUniversity**, spusťte projekt a přihlaste se pomocí přihlašovacích údajů *správce* (heslo je *devpwd*) a aktualizujte okno **Průzkumník objektů systému SQL Server** .
3. Klikněte pravým tlačítkem myši na tabulku **Uživatelé** a potom klikněte na tlačítko **Návrhář zobrazení**.

    ![Návrhář zobrazení SSOX](deploying-a-database-update/_static/image3.png)
4. V Návrháři přidejte sloupec *Komentáře* a nastavte hodnotu *nvarchar (128)* a Nullable a klikněte na tlačítko **aktualizovat**.

    ![Přidávání sloupce komentáře](deploying-a-database-update/_static/image4.png)
5. V okně **Náhled aktualizací databáze** klikněte na **aktualizovat databázi**.

    ![Náhled aktualizací databáze](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a>Vytvoří stránku pro zobrazení a úpravu nového sloupce.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **účtu** v projektu ContosoUniversity, klikněte na **Přidat**a pak klikněte na **Nová položka**.
2. Vytvořte nový **webový formulář pomocí stránky předlohy** a pojmenujte jej *UserInfo. aspx*. Přijměte výchozí soubor *Web. Master* jako stránku předlohy.
3. Zkopírujte následující kód do prvku `MainContent` `Content` (poslední z 3 `Content` prvků):

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. Klikněte pravým tlačítkem na stránku *UserInfo. aspx* a klikněte na **Zobrazit v prohlížeči**.
5. Přihlaste se pomocí přihlašovacích údajů uživatele *správce* (heslo je *devpwd*) a přidejte k uživateli nějaké komentáře, abyste ověřili, že stránka funguje správně.

    ![Stránka UserInfo](deploying-a-database-update/_static/image6.png)
6. Zavřete prohlížeč.

## <a name="deploy-the-database-update"></a>Nasazení aktualizace databáze

K nasazení pomocí poskytovatele dbDacFx stačí v profilu publikování vybrat možnost **databáze aktualizace** . Při počátečním nasazení ale při použití této možnosti jste ale nakonfigurovali i některé další skripty SQL, které se mají spustit: ty se pořád nacházejí v profilu a budete muset zabránit jejich opětovnému spuštění.

1. Otevřete Průvodce **publikováním webu** kliknutím pravým tlačítkem myši na projekt ContosoUniversity a kliknutím na **publikovat**.
2. Vyberte profil **testu** .
3. Klikněte na kartu **Nastavení** .
4. V části **DefaultConnection**vyberte **aktualizovat databázi**.
5. Zakažte další skripty, které jste nakonfigurovali pro spuštění při počátečním nasazení:

    1. Klikněte na **Konfigurovat aktualizace databáze**.
    2. V dialogovém okně **Konfigurovat aktualizace databáze** zrušte zaškrtnutí políček vedle *oprávnění GRANT. SQL* a *ASPNET-data-dev. SQL*.
    3. Klikněte na **Zavřít**.
6. Klikněte na kartu **Náhled** .
7. V části **databáze** a napravo od **DefaultConnection**klikněte na odkaz **databáze verze Preview** .

    ![Náhled databáze](deploying-a-database-update/_static/image7.png)

    V okně náhledu se zobrazí skript, který se spustí v cílové databázi, aby schéma databáze odpovídalo schématu zdrojové databáze. Skript obsahuje příkaz ALTER TABLE, který přidá nový sloupec.
8. Zavřete dialogové okno **Náhled databáze** a pak klikněte na **publikovat**.

    Visual Studio nasadí aktualizovanou aplikaci a otevře se v prohlížeči na domovské stránce.
9. Spusťte stránku UserInfo (přidejte *účet/UserInfo. aspx* na domovskou stránku URL) a ověřte, zda byla aktualizace úspěšně nasazena. Budete se muset přihlásit zadáním *správce* a *devpwd*.

    Data v tabulkách nejsou ve výchozím nastavení nasazena a Vy jste nenakonfigurovali skript nasazení dat, který se má spustit, takže nebudete moct najít komentář, který jste přidali při vývoji. Nový komentář teď můžete přidat do přípravy, abyste ověřili, že se změna nasadila do databáze a stránka funguje správně.
10. Pro nasazení do přípravy a výroby použijte stejný postup.

    Nezapomeňte zakázat nadbytečné skripty. Jediným rozdílem v porovnání s profilem testu je, že zakážete pouze jeden skript v pracovních a provozních profilech, protože byly nakonfigurovány tak, aby spouštěly pouze *ASPNET-prod-data. SQL*.

    Přihlašovací údaje pro pracovní a produkční prostředí jsou admin a prodpwd.

    V případě skutečné aktualizace produkčních aplikací, která zahrnuje změnu v databázi, byste taky během nasazování převedli aplikaci do offline režimu tak, že před publikováním a odstraněním aplikace nahrajete *\_offline. htm* , jak jste viděli v [předchozím kurzu](deploying-a-code-update.md).

## <a name="summary"></a>Přehled

Nyní jste nasadili aktualizaci aplikace, která zahrnovala změnu databáze pomocí Migrace Code First i poskytovatele dbDacFx.

![Stránka instruktorů s DatumNarození](deploying-a-database-update/_static/image8.png)

![Stránka UserInfo](deploying-a-database-update/_static/image9.png)

V dalším kurzu se dozvíte, jak spustit nasazení pomocí příkazového řádku.

> [!div class="step-by-step"]
> [Předchozí](deploying-a-code-update.md)
> [Další](command-line-deployment.md)
