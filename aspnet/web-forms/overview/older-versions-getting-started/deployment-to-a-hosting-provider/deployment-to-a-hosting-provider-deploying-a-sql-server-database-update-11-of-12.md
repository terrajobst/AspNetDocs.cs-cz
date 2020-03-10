---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení SQL Server aktualizace databáze-11 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528124"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="d2e19-103">Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení SQL Server aktualizace databáze-11 z 12</span><span class="sxs-lookup"><span data-stu-id="d2e19-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>

<span data-ttu-id="d2e19-104">tím, že [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d2e19-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d2e19-105">Stáhnout počáteční projekt</span><span class="sxs-lookup"><span data-stu-id="d2e19-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="d2e19-106">V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web.</span><span class="sxs-lookup"><span data-stu-id="d2e19-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="d2e19-107">Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu.</span><span class="sxs-lookup"><span data-stu-id="d2e19-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="d2e19-108">Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="d2e19-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="d2e19-109">Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit jiné edice SQL Server než SQL Server Compact a ukazuje, jak nasadit na weby Windows Azure najdete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2e19-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="d2e19-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="d2e19-110">Overview</span></span>

<span data-ttu-id="d2e19-111">V tomto kurzu se dozvíte, jak nasadit aktualizaci databáze do úplné SQL Server databáze.</span><span class="sxs-lookup"><span data-stu-id="d2e19-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="d2e19-112">Vzhledem k tomu, že Migrace Code First provádí veškerou práci s aktualizací databáze, proces je téměř shodný s tím, co jste provedli pro SQL Server Compact v kurzu [nasazení aktualizace databáze](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) .</span><span class="sxs-lookup"><span data-stu-id="d2e19-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="d2e19-113">Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="d2e19-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="d2e19-114">Přidání nového sloupce do tabulky</span><span class="sxs-lookup"><span data-stu-id="d2e19-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="d2e19-115">V této části kurzu provedete změnu v databázi a odpovídající změny kódu a pak je otestujete v aplikaci Visual Studio v článku Příprava pro jejich nasazení do testovacích a produkčních prostředí.</span><span class="sxs-lookup"><span data-stu-id="d2e19-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="d2e19-116">Tato změna zahrnuje přidání sloupce `OfficeHours` k entitě `Instructor` a zobrazení nových informací na webové stránce **instruktoři** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="d2e19-117">V projektu ContosoUniversity. DAL otevřete *Instructor.cs* a přidejte následující vlastnost mezi `HireDate` a `Courses` vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="d2e19-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="d2e19-118">Aktualizujte třídu inicializátoru tak, aby vyzkoušela nový sloupec s testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="d2e19-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="d2e19-119">Otevřete *Migrations\Configuration.cs* a nahraďte blok kódu, který začíná `var instructors = new List<Instructor>` s následujícím blokem kódu, který obsahuje nový sloupec:</span><span class="sxs-lookup"><span data-stu-id="d2e19-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="d2e19-120">V projektu ContosoUniversity otevřete *instruktory. aspx* a přidejte nové pole šablony pro pracovní dobu Office těsně před uzavírací `</Columns>` značku v prvním `GridView`m ovládacím prvku:</span><span class="sxs-lookup"><span data-stu-id="d2e19-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="d2e19-121">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="d2e19-121">Build the solution.</span></span>

<span data-ttu-id="d2e19-122">Otevřete okno **konzoly Správce balíčků** a jako **výchozí projekt**vyberte ContosoUniversity. dal.</span><span class="sxs-lookup"><span data-stu-id="d2e19-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="d2e19-123">Zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="d2e19-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="d2e19-124">Spusťte aplikaci a vyberte stránku **instruktoři** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="d2e19-125">Načtení stránky trvá trochu déle než obvykle, protože Entity Framework znovu vytvoří databázi a semena s testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="d2e19-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="d2e19-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d2e19-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="d2e19-127">Nasazení aktualizace databáze do testovacího prostředí</span><span class="sxs-lookup"><span data-stu-id="d2e19-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="d2e19-128">Při použití Migrace Code First je metoda nasazení změny databáze do SQL Server stejná jako u SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="d2e19-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="d2e19-129">Je však nutné změnit profil publikování testu, protože je stále nastaven na migraci z SQL Server Compact na SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d2e19-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="d2e19-130">Prvním krokem je odebrání transformací připojovacích řetězců, které jste vytvořili v předchozím kurzu.</span><span class="sxs-lookup"><span data-stu-id="d2e19-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="d2e19-131">Ty už nejsou potřeba, protože v profilu publikování zadáte transformace připojovacích řetězců, jak jste předtím nakonfigurovali kartu **balíček/publikování SQL** pro migraci na SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d2e19-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="d2e19-132">Otevřete soubor *Web. test. config* a odeberte `connectionStrings` element.</span><span class="sxs-lookup"><span data-stu-id="d2e19-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="d2e19-133">Jedinou zbývající transformací v souboru *Web. test. config* je hodnota `Environment` v elementu `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="d2e19-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="d2e19-134">Nyní můžete aktualizovat profil publikování a publikovat do testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="d2e19-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="d2e19-135">Otevřete Průvodce **publikováním webu** a poté přepněte na kartu **profil** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="d2e19-136">Vyberte profil publikování **testu** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="d2e19-137">Vyberte kartu **Nastavení** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="d2e19-138">Klikněte na **Povolit nová vylepšení publikování databáze**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="d2e19-139">Do pole Připojovací řetězec pro **SchoolContext**zadejte stejnou hodnotu, jakou jste použili v transformačním souboru *Web. test. config* v předchozím kurzu:</span><span class="sxs-lookup"><span data-stu-id="d2e19-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="d2e19-140">Vyberte **Execute migrace Code First (spouští se při spuštění aplikace)** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="d2e19-141">(Ve vaší verzi sady Visual Studio může být zaškrtávací políčko označeno jako **migrace Code First**.)</span><span class="sxs-lookup"><span data-stu-id="d2e19-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="d2e19-142">Do pole Připojovací řetězec pro **DefaultConnection**zadejte stejnou hodnotu, jakou jste použili v transformačním souboru *Web. test. config* v předchozím kurzu:</span><span class="sxs-lookup"><span data-stu-id="d2e19-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="d2e19-143">Ponechte vymazané **aktualizaci databáze** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="d2e19-144">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-144">Click **Publish**.</span></span>

<span data-ttu-id="d2e19-145">Visual Studio nasadí změny kódu do testovacího prostředí a otevře prohlížeč na domovské stránce společnosti Contoso University.</span><span class="sxs-lookup"><span data-stu-id="d2e19-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="d2e19-146">Vyberte stránku instruktoři.</span><span class="sxs-lookup"><span data-stu-id="d2e19-146">Select the Instructors page.</span></span>

<span data-ttu-id="d2e19-147">Když aplikace tuto stránku spustí, pokusí se získat přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="d2e19-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="d2e19-148">Migrace Code First zkontroluje, jestli je databáze aktuální, a zjistí, že se zatím nepoužila poslední migrace.</span><span class="sxs-lookup"><span data-stu-id="d2e19-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="d2e19-149">Migrace Code First aplikuje nejnovější migraci, spustí metodu `Seed` a pak se stránka normálně spustí.</span><span class="sxs-lookup"><span data-stu-id="d2e19-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="d2e19-150">Zobrazí se sloupec nové hodiny Office s dosazením dat.</span><span class="sxs-lookup"><span data-stu-id="d2e19-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="d2e19-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d2e19-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="d2e19-152">Nasazení aktualizace databáze do provozního prostředí</span><span class="sxs-lookup"><span data-stu-id="d2e19-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="d2e19-153">Je třeba změnit profil publikování také pro produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="d2e19-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="d2e19-154">V takovém případě odeberete stávající profil a vytvoříte nový pomocí importu aktualizovaného souboru. publishsettings.</span><span class="sxs-lookup"><span data-stu-id="d2e19-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="d2e19-155">Aktualizovaný soubor bude obsahovat připojovací řetězec pro databázi SQL Server na adrese Cytanium.</span><span class="sxs-lookup"><span data-stu-id="d2e19-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="d2e19-156">Jak bylo zobrazeno, když jste nasadili do testovacího prostředí, již nepotřebujete transformaci připojovacího řetězce v transformačním souboru *Web. produkční. config* .</span><span class="sxs-lookup"><span data-stu-id="d2e19-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="d2e19-157">Otevřete tento soubor a odeberte `connectionStrings` element.</span><span class="sxs-lookup"><span data-stu-id="d2e19-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="d2e19-158">Zbývající transformace jsou pro hodnotu `Environment` v elementu `appSettings` a element `location`, který omezuje přístup k knihovny elmah zpráv o chybách.</span><span class="sxs-lookup"><span data-stu-id="d2e19-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="d2e19-159">Před vytvořením nového publikačního profilu pro produkci si stáhněte aktualizovaný soubor. publishsettings stejným způsobem jako dříve v kurzu [nasazení do provozního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) .</span><span class="sxs-lookup"><span data-stu-id="d2e19-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="d2e19-160">(V ovládacím panelu Cytanium klikněte na **weby**a pak klikněte na web **contosouniversity.com** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="d2e19-161">Vyberte kartu **publikování na webu** a pak klikněte na **Stáhnout profil publikování pro tento web**.) Důvodem je, že je třeba v souboru. publishsettings vybrat připojovací řetězec databáze.</span><span class="sxs-lookup"><span data-stu-id="d2e19-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="d2e19-162">Připojovací řetězec nebyl při prvním stažení souboru k dispozici, protože jste stále používali SQL Server Compact a jste vytvořili databázi SQL Server na Cytanium.</span><span class="sxs-lookup"><span data-stu-id="d2e19-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="d2e19-163">Teď můžete aktualizovat profil publikování a publikovat ho v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d2e19-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="d2e19-164">Otevřete Průvodce **publikováním webu** a poté přepněte na kartu **profil** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="d2e19-165">Klikněte na **Spravovat profily**a pak odstraňte produkční profil.</span><span class="sxs-lookup"><span data-stu-id="d2e19-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="d2e19-166">Zavřete průvodce **publikováním webu** a uložte tuto změnu.</span><span class="sxs-lookup"><span data-stu-id="d2e19-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="d2e19-167">Spusťte průvodce **publikováním webu** znovu a pak klikněte na **importovat**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="d2e19-168">Na kartě **připojení** změňte **cílovou adresu URL** na odpovídající hodnotu, pokud používáte dočasnou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d2e19-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="d2e19-169">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-169">Click **Next**.</span></span>

<span data-ttu-id="d2e19-170">Na kartě **Nastavení** klikněte na **Povolit nová vylepšení publikování databáze**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="d2e19-171">V rozevíracím seznamu připojovací řetězec pro **SchoolContext**vyberte připojovací řetězec Cytanium.</span><span class="sxs-lookup"><span data-stu-id="d2e19-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="d2e19-173">Vyberte možnost **spustit Code First migrace (spouští se při spuštění aplikace)** .</span><span class="sxs-lookup"><span data-stu-id="d2e19-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="d2e19-174">V rozevíracím seznamu připojovací řetězec pro **DefaultConnection**vyberte připojovací řetězec Cytanium.</span><span class="sxs-lookup"><span data-stu-id="d2e19-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="d2e19-175">Vyberte kartu **profil** , klikněte na **Spravovat profily**a přejmenujte profil z "contosouniversity.com-nasazení webu" na "produkční".</span><span class="sxs-lookup"><span data-stu-id="d2e19-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="d2e19-176">Zavřete profil publikování a uložte změnu a pak znovu otevřete.</span><span class="sxs-lookup"><span data-stu-id="d2e19-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="d2e19-177">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="d2e19-177">Click **Publish**.</span></span> <span data-ttu-id="d2e19-178">(Pro skutečný produkční web byste aplikaci zkopírovali *\_offline. htm* do produkčního prostředí a před publikováním ji uložte do složky projektu a pak ji po dokončení nasazení odebrat.)</span><span class="sxs-lookup"><span data-stu-id="d2e19-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="d2e19-179">Visual Studio nasadí změny kódu do testovacího prostředí a otevře prohlížeč na domovské stránce společnosti Contoso University.</span><span class="sxs-lookup"><span data-stu-id="d2e19-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="d2e19-180">Vyberte stránku instruktoři.</span><span class="sxs-lookup"><span data-stu-id="d2e19-180">Select the Instructors page.</span></span>

<span data-ttu-id="d2e19-181">Migrace Code First aktualizuje databázi stejným způsobem jako v testovacím prostředí.</span><span class="sxs-lookup"><span data-stu-id="d2e19-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="d2e19-182">Zobrazí se sloupec nové hodiny Office s dosazením dat.</span><span class="sxs-lookup"><span data-stu-id="d2e19-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="d2e19-184">Nyní jste úspěšně nasadili aktualizaci aplikace, která zahrnovala změnu databáze, pomocí SQL Server databáze.</span><span class="sxs-lookup"><span data-stu-id="d2e19-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="d2e19-185">Další informace</span><span class="sxs-lookup"><span data-stu-id="d2e19-185">More Information</span></span>

<span data-ttu-id="d2e19-186">Tím se dokončí Tato série kurzů pro nasazení webové aplikace v ASP.NET k poskytovateli hostingu třetí strany.</span><span class="sxs-lookup"><span data-stu-id="d2e19-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="d2e19-187">Další informace o všech tématech popsaných v těchto kurzech naleznete v části [Mapa obsahu nasazení ASP.NET](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="d2e19-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d2e19-188">Poděkování</span><span class="sxs-lookup"><span data-stu-id="d2e19-188">Acknowledgements</span></span>

<span data-ttu-id="d2e19-189">Chci nás zasílat na následující lidi, kteří významně přispěli k obsahu této série kurzů:</span><span class="sxs-lookup"><span data-stu-id="d2e19-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="d2e19-190">Alberto Poblacion, MVP &amp; MCT, Španělsko</span><span class="sxs-lookup"><span data-stu-id="d2e19-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="d2e19-191">Jarod Ferguson, MVP pro vývoj datových platforem, USA</span><span class="sxs-lookup"><span data-stu-id="d2e19-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="d2e19-192">Harsh Mittal, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d2e19-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="d2e19-193">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d2e19-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="d2e19-194">Mike Pope, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d2e19-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="d2e19-195">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d2e19-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="d2e19-196">Raffaele Rialdi, Itálie</span><span class="sxs-lookup"><span data-stu-id="d2e19-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="d2e19-197">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="d2e19-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="d2e19-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="d2e19-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="d2e19-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="d2e19-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="d2e19-200">[Scott Hunterem, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="d2e19-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="d2e19-201">Srđan Božović, Srbsko</span><span class="sxs-lookup"><span data-stu-id="d2e19-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="d2e19-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="d2e19-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2e19-203">[Předchozí](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [Další](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="d2e19-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
