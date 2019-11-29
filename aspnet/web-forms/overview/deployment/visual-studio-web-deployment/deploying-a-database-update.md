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
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="7d4cd-103">Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace databáze</span><span class="sxs-lookup"><span data-stu-id="7d4cd-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>

<span data-ttu-id="7d4cd-104">tím, že [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7d4cd-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7d4cd-105">Stáhnout počáteční projekt</span><span class="sxs-lookup"><span data-stu-id="7d4cd-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="7d4cd-106">V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="7d4cd-107">Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7d4cd-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="7d4cd-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="7d4cd-108">Overview</span></span>

<span data-ttu-id="7d4cd-109">V tomto kurzu provedete změnu v databázi a související změny kódu, otestujete změny v aplikaci Visual Studio a potom nasadíte aktualizaci do prostředí testování, přípravy a produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="7d4cd-110">V tomto kurzu se nejprve dozvíte, jak aktualizovat databázi, která je spravovaná pomocí Migrace Code First, a později ukazuje, jak aktualizovat databázi pomocí poskytovatele dbDacFx.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="7d4cd-111">Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7d4cd-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="7d4cd-112">Nasazení aktualizace databáze pomocí Migrace Code First</span><span class="sxs-lookup"><span data-stu-id="7d4cd-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="7d4cd-113">V této části přidáte sloupec data narození do `Person` základní třídy pro entity `Student` a `Instructor`.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="7d4cd-114">Pak aktualizujete stránku, která zobrazuje data instruktora, aby zobrazila nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="7d4cd-115">Nakonec nasadíte změny do testování, přípravy a výroby.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="7d4cd-116">Přidání sloupce do tabulky v aplikační databázi</span><span class="sxs-lookup"><span data-stu-id="7d4cd-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="7d4cd-117">V projektu *ContosoUniversity. dal* otevřete *Person.cs* a na konci třídy `Person` přidejte následující vlastnost (před ní musí být dvě uzavírací složené závorky):</span><span class="sxs-lookup"><span data-stu-id="7d4cd-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="7d4cd-118">Dále aktualizujte metodu `Seed` tak, aby poskytovala hodnotu pro nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="7d4cd-119">Otevřete *Migrations\Configuration.cs* a nahraďte blok kódu, který začíná `var instructors = new List<Instructor>` s následujícím blokem kódu, který obsahuje informace o datu narození:</span><span class="sxs-lookup"><span data-stu-id="7d4cd-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="7d4cd-120">Sestavte řešení a pak otevřete okno **konzoly Správce balíčků** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="7d4cd-121">Ujistěte se, že je ContosoUniversity. DAL stále vybraný jako **výchozí projekt**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="7d4cd-122">V okně **konzoly Správce balíčků** vyberte jako **výchozí projekt**možnost **ContosoUniversity. dal** a potom zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="7d4cd-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="7d4cd-123">Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou třídu `DbMigration` a v metodě `Up` můžete zobrazit kód, který vytvoří nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="7d4cd-124">Metoda `Up` vytvoří sloupec při implementaci změny a metoda `Down` odstraní sloupec při vrácení změny zpět.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="7d4cd-126">Sestavte řešení a potom v okně **konzoly Správce balíčků** zadejte následující příkaz (Ujistěte se, že je projekt CONTOSOUNIVERSITY. dal stále vybraný):</span><span class="sxs-lookup"><span data-stu-id="7d4cd-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="7d4cd-127">Entity Framework spustí metodu `Up` a potom spustí metodu `Seed`.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="7d4cd-128">Zobrazit nový sloupec na stránce instruktoři</span><span class="sxs-lookup"><span data-stu-id="7d4cd-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="7d4cd-129">V projektu ContosoUniversity otevřete *instruktory. aspx* a přidejte nové pole šablony, abyste zobrazili datum narození.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="7d4cd-130">Přidejte ho mezi ty pro datum přijetí a přiřazení kanceláře:</span><span class="sxs-lookup"><span data-stu-id="7d4cd-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="7d4cd-131">(Pokud se odsazení kódu nesynchronizuje, můžete stisknutím kláves CTRL-K a potom CTRL-D soubor automaticky znovu zformátovat.)</span><span class="sxs-lookup"><span data-stu-id="7d4cd-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="7d4cd-132">Spusťte aplikaci a klikněte na odkaz **instruktoři** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="7d4cd-133">Po načtení stránky se zobrazí, že má nové pole data narození.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![Stránka instruktorů s DatumNarození](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="7d4cd-135">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="7d4cd-136">Nasazení aktualizace databáze</span><span class="sxs-lookup"><span data-stu-id="7d4cd-136">Deploy the database update</span></span>

1. <span data-ttu-id="7d4cd-137">V **Průzkumník řešení** vyberte projekt ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="7d4cd-138">Na panelu nástrojů **publikování webu jedním kliknutím** klikněte na profil publikování **testu** a pak klikněte na **Publikovat web**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="7d4cd-139">(Pokud je panel nástrojů zakázaný, vyberte projekt ContosoUniversity v **Průzkumník řešení**.)</span><span class="sxs-lookup"><span data-stu-id="7d4cd-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="7d4cd-140">Visual Studio nasadí aktualizovanou aplikaci a otevře se v prohlížeči na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="7d4cd-141">Spuštěním stránky **instruktory** ověřte, zda byla aktualizace úspěšně nasazena.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="7d4cd-142">Když se aplikace pokusí o přístup k databázi pro tuto stránku, Code First aktualizuje schéma databáze a spustí metodu `Seed`.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="7d4cd-143">Po zobrazení stránky se zobrazí očekávaný sloupec **Datum narození** s kalendářními daty.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="7d4cd-144">Na panelu nástrojů **publikování webu jedním kliknutím** klikněte na **pracovní** profil publikování a pak klikněte na **Publikovat web**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="7d4cd-145">Spuštěním stránky **instruktoři** v části fázování ověříte, že se aktualizace úspěšně nasadila.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="7d4cd-146">Na panelu nástrojů pro **publikování na webu** klikněte **na publikovat profil publikování a** pak klikněte na **Publikovat web**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="7d4cd-147">Spusťte stránku **instruktoři** v produkčním prostředí, abyste ověřili, že se aktualizace úspěšně nasadila.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="7d4cd-148">V případě skutečné aktualizace produkčních aplikací, která zahrnuje změnu v databázi, byste taky během nasazení normálně převzali aplikaci v režimu offline pomocí *aplikace\_offline. htm*, jak jste viděli v předchozím kurzu.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="7d4cd-149">Nasazení aktualizace databáze pomocí poskytovatele dbDacFx</span><span class="sxs-lookup"><span data-stu-id="7d4cd-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="7d4cd-150">V této části přidáte sloupec *Komentáře* do tabulky *uživatelů* v databázi členství a vytvoříte stránku, která vám umožní zobrazit a upravit komentáře pro každého uživatele.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="7d4cd-151">Pak nasadíte změny do testování, přípravy a výroby.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="7d4cd-152">Přidání sloupce do tabulky v databázi členství</span><span class="sxs-lookup"><span data-stu-id="7d4cd-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="7d4cd-153">V aplikaci Visual Studio otevřete **Průzkumník objektů systému SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="7d4cd-154">Rozbalte **(LocalDB) \v11.0**, rozbalte **databáze**, rozbalte **ASPNET-ContosoUniversity** (ne **ASPNET-ContosoUniversity-prod**) a pak rozbalte **tabulky**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="7d4cd-155">Pokud nevidíte **(LocalDB) \v11.0** pod uzlem **SQL Server** , klikněte pravým tlačítkem na uzel **SQL Server** a klikněte na **Přidat SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="7d4cd-156">V dialogovém okně **připojit k serveru** zadejte *(LocalDB) \V11.0* jako **název serveru**a pak klikněte na **připojit**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="7d4cd-157">Pokud nevidíte **ASPNET-ContosoUniversity**, spusťte projekt a přihlaste se pomocí přihlašovacích údajů *správce* (heslo je *devpwd*) a aktualizujte okno **Průzkumník objektů systému SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="7d4cd-158">Klikněte pravým tlačítkem myši na tabulku **Uživatelé** a potom klikněte na tlačítko **Návrhář zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![Návrhář zobrazení SSOX](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="7d4cd-160">V Návrháři přidejte sloupec *Komentáře* a nastavte hodnotu *nvarchar (128)* a Nullable a klikněte na tlačítko **aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![Přidávání sloupce komentáře](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="7d4cd-162">V okně **Náhled aktualizací databáze** klikněte na **aktualizovat databázi**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![Náhled aktualizací databáze](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="7d4cd-164">Vytvoří stránku pro zobrazení a úpravu nového sloupce.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="7d4cd-165">V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **účtu** v projektu ContosoUniversity, klikněte na **Přidat**a pak klikněte na **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="7d4cd-166">Vytvořte nový **webový formulář pomocí stránky předlohy** a pojmenujte jej *UserInfo. aspx*.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="7d4cd-167">Přijměte výchozí soubor *Web. Master* jako stránku předlohy.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="7d4cd-168">Zkopírujte následující kód do prvku `MainContent` `Content` (poslední z 3 `Content` prvků):</span><span class="sxs-lookup"><span data-stu-id="7d4cd-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="7d4cd-169">Klikněte pravým tlačítkem na stránku *UserInfo. aspx* a klikněte na **Zobrazit v prohlížeči**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="7d4cd-170">Přihlaste se pomocí přihlašovacích údajů uživatele *správce* (heslo je *devpwd*) a přidejte k uživateli nějaké komentáře, abyste ověřili, že stránka funguje správně.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![Stránka UserInfo](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="7d4cd-172">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="7d4cd-173">Nasazení aktualizace databáze</span><span class="sxs-lookup"><span data-stu-id="7d4cd-173">Deploy the database update</span></span>

<span data-ttu-id="7d4cd-174">K nasazení pomocí poskytovatele dbDacFx stačí v profilu publikování vybrat možnost **databáze aktualizace** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="7d4cd-175">Při počátečním nasazení ale při použití této možnosti jste ale nakonfigurovali i některé další skripty SQL, které se mají spustit: ty se pořád nacházejí v profilu a budete muset zabránit jejich opětovnému spuštění.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="7d4cd-176">Otevřete Průvodce **publikováním webu** kliknutím pravým tlačítkem myši na projekt ContosoUniversity a kliknutím na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="7d4cd-177">Vyberte profil **testu** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="7d4cd-178">Klikněte na kartu **Nastavení** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="7d4cd-179">V části **DefaultConnection**vyberte **aktualizovat databázi**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="7d4cd-180">Zakažte další skripty, které jste nakonfigurovali pro spuštění při počátečním nasazení:</span><span class="sxs-lookup"><span data-stu-id="7d4cd-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="7d4cd-181">Klikněte na **Konfigurovat aktualizace databáze**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="7d4cd-182">V dialogovém okně **Konfigurovat aktualizace databáze** zrušte zaškrtnutí políček vedle *oprávnění GRANT. SQL* a *ASPNET-data-dev. SQL*.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="7d4cd-183">Klikněte na **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-183">Click **Close**.</span></span>
6. <span data-ttu-id="7d4cd-184">Klikněte na kartu **Náhled** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="7d4cd-185">V části **databáze** a napravo od **DefaultConnection**klikněte na odkaz **databáze verze Preview** .</span><span class="sxs-lookup"><span data-stu-id="7d4cd-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![Náhled databáze](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="7d4cd-187">V okně náhledu se zobrazí skript, který se spustí v cílové databázi, aby schéma databáze odpovídalo schématu zdrojové databáze.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="7d4cd-188">Skript obsahuje příkaz ALTER TABLE, který přidá nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="7d4cd-189">Zavřete dialogové okno **Náhled databáze** a pak klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="7d4cd-190">Visual Studio nasadí aktualizovanou aplikaci a otevře se v prohlížeči na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="7d4cd-191">Spusťte stránku UserInfo (přidejte *účet/UserInfo. aspx* na domovskou stránku URL) a ověřte, zda byla aktualizace úspěšně nasazena.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="7d4cd-192">Budete se muset přihlásit zadáním *správce* a *devpwd*.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="7d4cd-193">Data v tabulkách nejsou ve výchozím nastavení nasazena a Vy jste nenakonfigurovali skript nasazení dat, který se má spustit, takže nebudete moct najít komentář, který jste přidali při vývoji.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="7d4cd-194">Nový komentář teď můžete přidat do přípravy, abyste ověřili, že se změna nasadila do databáze a stránka funguje správně.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="7d4cd-195">Pro nasazení do přípravy a výroby použijte stejný postup.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="7d4cd-196">Nezapomeňte zakázat nadbytečné skripty.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="7d4cd-197">Jediným rozdílem v porovnání s profilem testu je, že zakážete pouze jeden skript v pracovních a provozních profilech, protože byly nakonfigurovány tak, aby spouštěly pouze *ASPNET-prod-data. SQL*.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="7d4cd-198">Přihlašovací údaje pro pracovní a produkční prostředí jsou admin a prodpwd.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="7d4cd-199">V případě skutečné aktualizace produkčních aplikací, která zahrnuje změnu v databázi, byste taky během nasazování převedli aplikaci do offline režimu tak, že před publikováním a odstraněním aplikace nahrajete *\_offline. htm* , jak jste viděli v [předchozím kurzu](deploying-a-code-update.md).</span><span class="sxs-lookup"><span data-stu-id="7d4cd-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="7d4cd-200">Přehled</span><span class="sxs-lookup"><span data-stu-id="7d4cd-200">Summary</span></span>

<span data-ttu-id="7d4cd-201">Nyní jste nasadili aktualizaci aplikace, která zahrnovala změnu databáze pomocí Migrace Code First i poskytovatele dbDacFx.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![Stránka instruktorů s DatumNarození](deploying-a-database-update/_static/image8.png)

![Stránka UserInfo](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="7d4cd-204">V dalším kurzu se dozvíte, jak spustit nasazení pomocí příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="7d4cd-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7d4cd-205">[Předchozí](deploying-a-code-update.md)
> [Další](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="7d4cd-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
