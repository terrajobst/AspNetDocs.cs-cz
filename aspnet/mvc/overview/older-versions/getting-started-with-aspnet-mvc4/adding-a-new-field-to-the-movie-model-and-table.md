---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: Přidání nového pole do modelu a tabulky filmů | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457697"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="52997-104">Přidání nového pole do modelu a tabulky Movie</span><span class="sxs-lookup"><span data-stu-id="52997-104">Adding a New Field to the Movie Model and Table</span></span>

<span data-ttu-id="52997-105">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="52997-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="52997-106">K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="52997-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="52997-107">Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.</span><span class="sxs-lookup"><span data-stu-id="52997-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="52997-108">V této části použijete Migrace Entity Framework Code First k migraci některých změn do tříd modelu, takže se změna aplikuje na databázi.</span><span class="sxs-lookup"><span data-stu-id="52997-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="52997-109">Ve výchozím nastavení platí, že při použití Entity Framework Code First k automatickému vytvoření databáze, stejně jako v tomto kurzu, Code First přidá do databáze tabulku, která bude sledovat, zda je schéma databáze synchronizované s třídami modelů, ze kterých byla vygenerována.</span><span class="sxs-lookup"><span data-stu-id="52997-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="52997-110">Pokud nejsou synchronizované, Entity Framework vyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="52997-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="52997-111">Díky tomu je snazší sledovat problémy v době vývoje, které byste jinak mohli najít (překrytím chyb) v době běhu.</span><span class="sxs-lookup"><span data-stu-id="52997-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="52997-112">Nastavení Migrace Code First pro změny modelu</span><span class="sxs-lookup"><span data-stu-id="52997-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="52997-113">Pokud používáte Visual Studio 2012, poklikejte na soubor *filmů. mdf* z Průzkumník řešení a otevřete nástroj Database Tool.</span><span class="sxs-lookup"><span data-stu-id="52997-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="52997-114">Visual Studio Express pro web se zobrazí Průzkumník databáze, v aplikaci Visual Studio 2012 se zobrazí Průzkumník serveru.</span><span class="sxs-lookup"><span data-stu-id="52997-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="52997-115">Pokud používáte Visual Studio 2010, použijte Průzkumník objektů systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="52997-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="52997-116">V databázovém nástroji (Průzkumník databáze Průzkumník serveru nebo Průzkumník objektů systému SQL Server) klikněte pravým tlačítkem na `MovieDBContext` a výběrem **Odstranit** vyřaďte databázi filmů.</span><span class="sxs-lookup"><span data-stu-id="52997-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="52997-117">Přejděte zpět na Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="52997-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="52997-118">Klikněte pravým tlačítkem na soubor *filmů. mdf* a výběrem **Odstranit** odeberte databázi filmů.</span><span class="sxs-lookup"><span data-stu-id="52997-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="52997-119">Sestavte aplikaci, abyste se ujistili, že nejsou k dispozici žádné chyby.</span><span class="sxs-lookup"><span data-stu-id="52997-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="52997-120">V nabídce **Nástroje** klikněte na **Správce balíčků NuGet** a pak na **Konzola Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="52997-120">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![Přidat Man Pack](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="52997-122">V okně **konzoly Správce balíčků** na `PM>`ovém řádku zadejte Enable-migrations-ContextTypeName MvcMovie. Models. MovieDBContext.</span><span class="sxs-lookup"><span data-stu-id="52997-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="52997-123">Příkaz **Povolit – migrace** (zobrazený výše) vytvoří soubor *Configuration.cs* v nové složce *migrace* .</span><span class="sxs-lookup"><span data-stu-id="52997-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="52997-124">Visual Studio otevře soubor *Configuration.cs* .</span><span class="sxs-lookup"><span data-stu-id="52997-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="52997-125">Metodu `Seed` v souboru *Configuration.cs* nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="52997-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="52997-126">Klikněte pravým tlačítkem myši na červenou vlnovku pod `Movie` a vyberte **vyřešit** a pak **použijte** **MvcMovie. Models;**</span><span class="sxs-lookup"><span data-stu-id="52997-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="52997-127">Tím přidáte následující příkaz using:</span><span class="sxs-lookup"><span data-stu-id="52997-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="52997-128">Migrace Code First volá metodu `Seed` po každé migraci (to znamená volání metody **Update-Database** v konzole správce balíčků) a tato metoda aktualizuje řádky, které již byly vloženy, nebo je vloží, pokud ještě neexistují.</span><span class="sxs-lookup"><span data-stu-id="52997-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>

<span data-ttu-id="52997-129">**Stisknutím kombinace kláves CTRL + SHIFT + B Sestavte projekt.** (Pokud v tomto okamžiku nebudete sestavovat, následující kroky selžou.)</span><span class="sxs-lookup"><span data-stu-id="52997-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="52997-130">Dalším krokem je vytvoření třídy `DbMigration` pro prvotní migraci.</span><span class="sxs-lookup"><span data-stu-id="52997-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="52997-131">Tato migrace vytvoří novou databázi. to je důvod, proč jste odstranili soubor *Movie. mdf* v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="52997-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="52997-132">V okně **konzoly Správce balíčků** zadejte příkaz "Přidání-migrace počátečního" a vytvořte prvotní migraci.</span><span class="sxs-lookup"><span data-stu-id="52997-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="52997-133">Název "Initial" je libovolný a slouží k pojmenování vytvořeného souboru migrace.</span><span class="sxs-lookup"><span data-stu-id="52997-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="52997-134">Migrace Code First vytvoří další soubor třídy ve složce *migrations* (s názvem *{DateStamp}\_Initial.cs* ) a tato třída obsahuje kód, který vytvoří schéma databáze.</span><span class="sxs-lookup"><span data-stu-id="52997-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="52997-135">Název souboru migrace je předem vyřešen s časovým razítkem, které vám pomůžou s řazením.</span><span class="sxs-lookup"><span data-stu-id="52997-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="52997-136">Projděte si soubor *{dateStamp}\_Initial.cs* , který obsahuje pokyny k vytvoření tabulky filmů pro filmovou databázi.</span><span class="sxs-lookup"><span data-stu-id="52997-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="52997-137">Při aktualizaci databáze v níže uvedených pokynech se tento soubor *{dateStamp}\_Initial.cs* spustí a vytvoří se schéma databáze.</span><span class="sxs-lookup"><span data-stu-id="52997-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="52997-138">Pak se metoda **počáteční** hodnoty spustí k naplnění databáze testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="52997-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="52997-139">V **konzole správce balíčků**zadejte příkaz "Update-Database" a vytvořte databázi a spusťte metodu **počáteční** hodnoty.</span><span class="sxs-lookup"><span data-stu-id="52997-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="52997-140">Pokud se zobrazí chyba, která indikuje, že tabulka již existuje a nelze ji vytvořit, je pravděpodobné, že jste aplikaci spustili po odstranění databáze a před provedením `update-database`.</span><span class="sxs-lookup"><span data-stu-id="52997-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="52997-141">V takovém případě odstraňte soubor *Movies. mdf* znovu a opakujte příkaz `update-database`.</span><span class="sxs-lookup"><span data-stu-id="52997-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="52997-142">Pokud se vám stále stala chyba, odstraňte složku a obsah migrace a pak začněte s pokyny v horní části této stránky (to znamená odstranění souboru *filmů. mdf* a následného povolení migrace).</span><span class="sxs-lookup"><span data-stu-id="52997-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="52997-143">Spusťte aplikaci a přejděte na adresu URL */Movies* .</span><span class="sxs-lookup"><span data-stu-id="52997-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="52997-144">Zobrazí se data počáteční hodnoty.</span><span class="sxs-lookup"><span data-stu-id="52997-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="52997-145">Přidání vlastnosti hodnocení do modelu videa</span><span class="sxs-lookup"><span data-stu-id="52997-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="52997-146">Začněte přidáním nové vlastnosti `Rating` do existující třídy `Movie`.</span><span class="sxs-lookup"><span data-stu-id="52997-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="52997-147">Otevřete soubor *Models\Movie.cs* a přidejte vlastnost `Rating`, jako je tato:</span><span class="sxs-lookup"><span data-stu-id="52997-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="52997-148">Úplná `Movie` třída teď vypadá jako v následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="52997-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="52997-149">Sestavte aplikaci pomocí příkazu nabídky **build** &gt;**Build Movie** nebo stisknutím kombinace kláves CTRL + SHIFT + B.</span><span class="sxs-lookup"><span data-stu-id="52997-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="52997-150">Teď, když jste aktualizovali `Model` třídu, budete také muset aktualizovat šablony zobrazení *\Views\Movies\Index.cshtml* a *\Views\Movies\Create.cshtml* , aby se zobrazila nová vlastnost `Rating` v zobrazení prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="52997-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="52997-151">Otevřete soubor<em>\Views\Movies\Index.cshtml</em> a přidejte `<th>Rating</th>` záhlaví sloupce hned za sloupec <strong>Price</strong> .</span><span class="sxs-lookup"><span data-stu-id="52997-151">Open the<em>\Views\Movies\Index.cshtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="52997-152">Pak přidejte `<td>` sloupec poblíž konce šablony, aby se vygenerovala `@item.Rating` hodnota.</span><span class="sxs-lookup"><span data-stu-id="52997-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="52997-153">Níže vidíte, že aktualizovaná šablona zobrazení <em>index. cshtml</em> vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="52997-153">Below is what the updated <em>Index.cshtml</em> view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="52997-154">Potom otevřete soubor *\Views\Movies\Create.cshtml* a přidejte následující kód poblíž konce formuláře.</span><span class="sxs-lookup"><span data-stu-id="52997-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="52997-155">Tím vykreslíte textové pole, abyste mohli při vytváření nového filmu zadat hodnocení.</span><span class="sxs-lookup"><span data-stu-id="52997-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="52997-156">Nyní jste aktualizovali kód aplikace, aby podporoval novou vlastnost `Rating`.</span><span class="sxs-lookup"><span data-stu-id="52997-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="52997-157">Nyní spusťte aplikaci a přejděte na adresu URL */Movies* .</span><span class="sxs-lookup"><span data-stu-id="52997-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="52997-158">Když to uděláte, zobrazí se jedna z následujících chyb:</span><span class="sxs-lookup"><span data-stu-id="52997-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="52997-159">Tato chyba se zobrazuje, protože aktualizovaná třída modelu `Movie` v aplikaci je nyní odlišná od schématu `Movie` tabulky existující databáze.</span><span class="sxs-lookup"><span data-stu-id="52997-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="52997-160">(V tabulce databáze nejsou žádné `Rating` sloupce.)</span><span class="sxs-lookup"><span data-stu-id="52997-160">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="52997-161">K řešení této chyby je potřeba několik přístupů:</span><span class="sxs-lookup"><span data-stu-id="52997-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="52997-162">Entity Framework automaticky vyřadit a znovu vytvořit databázi na základě nového schématu třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="52997-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="52997-163">Tento přístup je velmi výhodný při aktivním vývoji na testovací databázi. umožňuje rychlou vývoj modelu a schématu databáze dohromady.</span><span class="sxs-lookup"><span data-stu-id="52997-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="52997-164">Nevýhodou, ale je to, že ztratíte stávající data v databázi, takže *nechcete tento* přístup použít v provozní databázi.</span><span class="sxs-lookup"><span data-stu-id="52997-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="52997-165">Použití inicializátoru k automatickému osazení databáze s testovacími daty je často produktivním způsobem pro vývoj aplikace.</span><span class="sxs-lookup"><span data-stu-id="52997-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="52997-166">Další informace o Entity Frameworkch inicializátorech databáze najdete v [kurzu ASP.NET MVC/Entity Framework](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Dykstra.</span><span class="sxs-lookup"><span data-stu-id="52997-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="52997-167">Explicitně upravte schéma existující databáze tak, aby odpovídalo třídám modelu.</span><span class="sxs-lookup"><span data-stu-id="52997-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="52997-168">Výhodou tohoto přístupu je, že zachováte data.</span><span class="sxs-lookup"><span data-stu-id="52997-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="52997-169">Tuto změnu můžete provést buď ručně, nebo vytvořením skriptu změny databáze.</span><span class="sxs-lookup"><span data-stu-id="52997-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="52997-170">K aktualizaci schématu databáze použijte Migrace Code First.</span><span class="sxs-lookup"><span data-stu-id="52997-170">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="52997-171">V tomto kurzu použijeme Migrace Code First.</span><span class="sxs-lookup"><span data-stu-id="52997-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="52997-172">Aktualizujte metodu počáteční hodnoty tak, aby poskytovala hodnotu pro nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="52997-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="52997-173">Otevřete soubor Migrations\Configuration.cs a přidejte pole hodnocení do každého objektu filmu.</span><span class="sxs-lookup"><span data-stu-id="52997-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="52997-174">Sestavte řešení a otevřete okno **konzoly Správce balíčků** a zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="52997-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="52997-175">Příkaz `add-migration` oznamuje migračnímu rozhraní, aby kontroloval aktuální model videa s aktuálním schématem video DB a vytvořil potřebný kód pro migraci databáze do nového modelu.</span><span class="sxs-lookup"><span data-stu-id="52997-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="52997-176">AddRatingMig je libovolný a slouží k pojmenování souboru migrace.</span><span class="sxs-lookup"><span data-stu-id="52997-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="52997-177">Je užitečné použít pro krok migrace smysluplný název.</span><span class="sxs-lookup"><span data-stu-id="52997-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="52997-178">Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou `DbMigration` odvozenou třídu a v metodě `Up` můžete zobrazit kód, který vytvoří nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="52997-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="52997-179">Sestavte řešení a potom v okně **konzoly Správce balíčků** zadejte příkaz Update-Database.</span><span class="sxs-lookup"><span data-stu-id="52997-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="52997-180">Následující obrázek ukazuje výstup v okně **konzoly Správce balíčků** (AddRatingMig data razítko se liší.)</span><span class="sxs-lookup"><span data-stu-id="52997-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="52997-181">Spusťte aplikaci znovu a přejděte na adresu URL/Movies.</span><span class="sxs-lookup"><span data-stu-id="52997-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="52997-182">Můžete zobrazit nové pole hodnocení.</span><span class="sxs-lookup"><span data-stu-id="52997-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="52997-183">Kliknutím na odkaz **vytvořit nový** přidejte nový film.</span><span class="sxs-lookup"><span data-stu-id="52997-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="52997-184">Všimněte si, že můžete přidat hodnocení.</span><span class="sxs-lookup"><span data-stu-id="52997-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="52997-186">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="52997-186">Click **Create**.</span></span> <span data-ttu-id="52997-187">Nový film, včetně hodnocení, se teď zobrazí v seznamu filmů:</span><span class="sxs-lookup"><span data-stu-id="52997-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="52997-189">Do šablon zobrazení Edit, Details a SearchIndex byste měli také přidat pole `Rating`.</span><span class="sxs-lookup"><span data-stu-id="52997-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="52997-190">Znovu můžete zadat příkaz "aktualizovat databázi" v okně **konzoly Správce balíčků** a provést žádné změny, protože schéma odpovídá modelu.</span><span class="sxs-lookup"><span data-stu-id="52997-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="52997-191">V této části jste viděli, jak můžete upravovat objekty modelu a udržovat databázi synchronizované se změnami.</span><span class="sxs-lookup"><span data-stu-id="52997-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="52997-192">Zjistili jste taky způsob, jak naplnit nově vytvořenou databázi pomocí ukázkových dat, abyste si mohli vyzkoušet scénáře.</span><span class="sxs-lookup"><span data-stu-id="52997-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="52997-193">Teď se podíváme na to, jak můžete přidat bohatou logiku ověřování do tříd modelu a povolit uplatnění některých obchodních pravidel.</span><span class="sxs-lookup"><span data-stu-id="52997-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="52997-194">[Předchozí](examining-the-edit-methods-and-edit-view.md)
> [Další](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="52997-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
