---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: Přidání nového pole | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 5974e53e4610dccc7812df261dc97a9b0327de85
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456683"
---
# <a name="adding-a-new-field"></a><span data-ttu-id="983d5-102">Přidání nového pole</span><span class="sxs-lookup"><span data-stu-id="983d5-102">Adding a New Field</span></span>

<span data-ttu-id="983d5-103">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="983d5-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="983d5-104">V této části použijete Migrace Entity Framework Code First k migraci některých změn do tříd modelu, takže se změna aplikuje na databázi.</span><span class="sxs-lookup"><span data-stu-id="983d5-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="983d5-105">Ve výchozím nastavení platí, že při použití Entity Framework Code First k automatickému vytvoření databáze, stejně jako v tomto kurzu, Code First přidá do databáze tabulku, která bude sledovat, zda je schéma databáze synchronizované s třídami modelů, ze kterých byla vygenerována.</span><span class="sxs-lookup"><span data-stu-id="983d5-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="983d5-106">Pokud nejsou synchronizované, Entity Framework vyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="983d5-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="983d5-107">Díky tomu je snazší sledovat problémy v době vývoje, které byste jinak mohli najít (překrytím chyb) v době běhu.</span><span class="sxs-lookup"><span data-stu-id="983d5-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="983d5-108">Nastavení Migrace Code First pro změny modelu</span><span class="sxs-lookup"><span data-stu-id="983d5-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="983d5-109">Přejděte na Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="983d5-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="983d5-110">Klikněte pravým tlačítkem na soubor *filmů. mdf* a výběrem **Odstranit** odeberte databázi filmů.</span><span class="sxs-lookup"><span data-stu-id="983d5-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="983d5-111">Pokud nevidíte soubor *filmy. mdf* , klikněte na ikonu **Zobrazit všechny soubory** zobrazené níže v červeném obrysu.</span><span class="sxs-lookup"><span data-stu-id="983d5-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="983d5-112">Sestavte aplikaci, abyste se ujistili, že nejsou k dispozici žádné chyby.</span><span class="sxs-lookup"><span data-stu-id="983d5-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="983d5-113">V nabídce **Nástroje** klikněte na **Správce balíčků NuGet** a pak na **Konzola Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="983d5-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![Přidat Man Pack](adding-a-new-field/_static/image2.png)

<span data-ttu-id="983d5-115">V okně **konzoly Správce balíčků** na `PM>` příkazovém řádku zadejte</span><span class="sxs-lookup"><span data-stu-id="983d5-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="983d5-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span><span class="sxs-lookup"><span data-stu-id="983d5-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="983d5-117">Příkaz **Povolit – migrace** (zobrazený výše) vytvoří soubor *Configuration.cs* v nové složce *migrace* .</span><span class="sxs-lookup"><span data-stu-id="983d5-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="983d5-118">Visual Studio otevře soubor *Configuration.cs* .</span><span class="sxs-lookup"><span data-stu-id="983d5-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="983d5-119">Metodu `Seed` v souboru *Configuration.cs* nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="983d5-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="983d5-120">Najeďte myší na červenou vlnovku pod `Movie` a klikněte na `Show Potential Fixes` a pak klikněte na **použití** **MvcMovie. Models;**</span><span class="sxs-lookup"><span data-stu-id="983d5-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="983d5-121">Tím přidáte následující příkaz using:</span><span class="sxs-lookup"><span data-stu-id="983d5-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="983d5-122">Migrace Code First volá metodu `Seed` po každé migraci (to znamená volání metody **Update-Database** v konzole správce balíčků) a tato metoda aktualizuje řádky, které již byly vloženy, nebo je vloží, pokud ještě neexistují.</span><span class="sxs-lookup"><span data-stu-id="983d5-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="983d5-123">Metoda [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) v následujícím kódu provádí operaci "Upsert":</span><span class="sxs-lookup"><span data-stu-id="983d5-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="983d5-124">Vzhledem k tomu, že metoda [počáteční](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) hodnoty se spouští při každé migraci, nemůžete pouze vkládat data, protože řádky, které se pokoušíte přidat, budou již po první migraci, která databázi vytvořila, k dispozici.</span><span class="sxs-lookup"><span data-stu-id="983d5-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="983d5-125">Operace "[Upsert](http://en.wikipedia.org/wiki/Upsert)" zabraňuje chybám, které by byly provedeny při pokusu o vložení řádku, který již existuje, ale přepíše všechny změny dat, které jste mohli provést při testování aplikace.</span><span class="sxs-lookup"><span data-stu-id="983d5-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="983d5-126">S testovacími daty v některých tabulkách možná nebudete chtít, aby došlo k tomu, že v některých případech změníte data při testování, které chcete po aktualizaci databáze zůstat.</span><span class="sxs-lookup"><span data-stu-id="983d5-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="983d5-127">V takovém případě chcete provést operaci podmíněného vložení: vložte řádek pouze v případě, že ještě neexistuje.</span><span class="sxs-lookup"><span data-stu-id="983d5-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="983d5-128">První parametr předaný metodě [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) určuje vlastnost, která má být použita pro kontrolu, zda řádek již existuje.</span><span class="sxs-lookup"><span data-stu-id="983d5-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="983d5-129">Pro testovací data, která poskytujete, se vlastnost `Title` dá použít k tomuto účelu, protože každý název v seznamu je jedinečný:</span><span class="sxs-lookup"><span data-stu-id="983d5-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="983d5-130">Tento kód předpokládá, že názvy jsou jedinečné.</span><span class="sxs-lookup"><span data-stu-id="983d5-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="983d5-131">Pokud ručně přidáte duplicitní název, při příštím provedení migrace se zobrazí následující výjimka.</span><span class="sxs-lookup"><span data-stu-id="983d5-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
> <span data-ttu-id="983d5-132">*Sekvence obsahuje více než jeden element.*</span><span class="sxs-lookup"><span data-stu-id="983d5-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="983d5-133">Další informace o metodě [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) naleznete v tématu [postará se o metodu EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span><span class="sxs-lookup"><span data-stu-id="983d5-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>

<span data-ttu-id="983d5-134">**Stisknutím kombinace kláves CTRL + SHIFT + B Sestavte projekt.** (Následující kroky selžou, pokud v tomto okamžiku nebudete sestavovat.)</span><span class="sxs-lookup"><span data-stu-id="983d5-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="983d5-135">Dalším krokem je vytvoření třídy `DbMigration` pro prvotní migraci.</span><span class="sxs-lookup"><span data-stu-id="983d5-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="983d5-136">Tato migrace vytvoří novou databázi. to je důvod, proč jste odstranili soubor *Movie. mdf* v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="983d5-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="983d5-137">V okně **konzoly Správce balíčků** zadejte příkaz `add-migration Initial` pro vytvoření prvotní migrace.</span><span class="sxs-lookup"><span data-stu-id="983d5-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="983d5-138">Název "Initial" je libovolný a slouží k pojmenování vytvořeného souboru migrace.</span><span class="sxs-lookup"><span data-stu-id="983d5-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="983d5-139">Migrace Code First vytvoří další soubor třídy ve složce *migrations* (s názvem *{DateStamp}\_Initial.cs* ) a tato třída obsahuje kód, který vytvoří schéma databáze.</span><span class="sxs-lookup"><span data-stu-id="983d5-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="983d5-140">Název souboru migrace je předem vyřešen s časovým razítkem, které vám pomůžou s řazením.</span><span class="sxs-lookup"><span data-stu-id="983d5-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="983d5-141">Projděte si soubor *{dateStamp}\_Initial.cs* , který obsahuje pokyny pro vytvoření tabulky `Movies` pro filmovou databázi.</span><span class="sxs-lookup"><span data-stu-id="983d5-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="983d5-142">Při aktualizaci databáze v níže uvedených pokynech se tento soubor *{dateStamp}\_Initial.cs* spustí a vytvoří se schéma databáze.</span><span class="sxs-lookup"><span data-stu-id="983d5-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="983d5-143">Pak se metoda **počáteční** hodnoty spustí k naplnění databáze testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="983d5-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="983d5-144">V **konzole správce balíčků**zadejte příkaz `update-database` pro vytvoření databáze a spuštění metody `Seed`.</span><span class="sxs-lookup"><span data-stu-id="983d5-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="983d5-145">Pokud se zobrazí chyba, která indikuje, že tabulka již existuje a nelze ji vytvořit, je pravděpodobné, že jste aplikaci spustili po odstranění databáze a před provedením `update-database`.</span><span class="sxs-lookup"><span data-stu-id="983d5-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="983d5-146">V takovém případě odstraňte soubor *Movies. mdf* znovu a opakujte příkaz `update-database`.</span><span class="sxs-lookup"><span data-stu-id="983d5-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="983d5-147">Pokud se vám stále stala chyba, odstraňte složku a obsah migrace a pak začněte s pokyny v horní části této stránky (to znamená odstranění souboru *filmů. mdf* a následného povolení migrace).</span><span class="sxs-lookup"><span data-stu-id="983d5-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="983d5-148">Pokud se stále zobrazí chyba, otevřete Průzkumník objektů systému SQL Server a odeberte databázi ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="983d5-148">If you still get an error, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="983d5-149">Spusťte aplikaci a přejděte na adresu URL */Movies* .</span><span class="sxs-lookup"><span data-stu-id="983d5-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="983d5-150">Zobrazí se data počáteční hodnoty.</span><span class="sxs-lookup"><span data-stu-id="983d5-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="983d5-151">Přidání vlastnosti hodnocení do modelu videa</span><span class="sxs-lookup"><span data-stu-id="983d5-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="983d5-152">Začněte přidáním nové vlastnosti `Rating` do existující třídy `Movie`.</span><span class="sxs-lookup"><span data-stu-id="983d5-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="983d5-153">Otevřete soubor *Models\Movie.cs* a přidejte vlastnost `Rating`, jako je tato:</span><span class="sxs-lookup"><span data-stu-id="983d5-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="983d5-154">Úplná `Movie` třída teď vypadá jako v následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="983d5-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="983d5-155">Sestavte aplikaci (CTRL + SHIFT + B).</span><span class="sxs-lookup"><span data-stu-id="983d5-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="983d5-156">Vzhledem k tomu, že jste přidali nové pole do `Movie` třídy, budete také muset aktualizovat *seznam* vazeb, aby byla tato nová vlastnost zahrnutá.</span><span class="sxs-lookup"><span data-stu-id="983d5-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="983d5-157">Aktualizujte atribut `bind` pro metody `Create` a `Edit` akcí tak, aby zahrnovaly vlastnost `Rating`:</span><span class="sxs-lookup"><span data-stu-id="983d5-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="983d5-158">Je také nutné aktualizovat šablony zobrazení, aby se zobrazily, vytvořili a upravili novou vlastnost `Rating` v zobrazení prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="983d5-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="983d5-159">Otevřete soubor *\Views\Movies\Index.cshtml* a přidejte `<th>Rating</th>` záhlaví sloupce hned za sloupec **Price** .</span><span class="sxs-lookup"><span data-stu-id="983d5-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="983d5-160">Pak přidejte `<td>` sloupec poblíž konce šablony, aby se vygenerovala `@item.Rating` hodnota.</span><span class="sxs-lookup"><span data-stu-id="983d5-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="983d5-161">Níže vidíte, že aktualizovaná šablona zobrazení *index. cshtml* vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="983d5-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="983d5-162">Potom otevřete soubor *\Views\Movies\Create.cshtml* a přidejte pole `Rating` s následujícím zvýrazněným označením.</span><span class="sxs-lookup"><span data-stu-id="983d5-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighted markup.</span></span> <span data-ttu-id="983d5-163">Tím vykreslíte textové pole, abyste mohli při vytváření nového filmu zadat hodnocení.</span><span class="sxs-lookup"><span data-stu-id="983d5-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="983d5-164">Nyní jste aktualizovali kód aplikace, aby podporoval novou vlastnost `Rating`.</span><span class="sxs-lookup"><span data-stu-id="983d5-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="983d5-165">Spusťte aplikaci a přejděte na adresu URL */Movies* .</span><span class="sxs-lookup"><span data-stu-id="983d5-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="983d5-166">Když to uděláte, zobrazí se jedna z následujících chyb:</span><span class="sxs-lookup"><span data-stu-id="983d5-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="983d5-167">Model, který provedl zálohování kontextu ' MovieDBContext ', se od vytvoření databáze změnil.</span><span class="sxs-lookup"><span data-stu-id="983d5-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="983d5-168">Zvažte použití Migrace Code First k aktualizaci databáze (https://go.microsoft.com/fwlink/?LinkId=238269).</span><span class="sxs-lookup"><span data-stu-id="983d5-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="983d5-169">Tato chyba se zobrazuje, protože aktualizovaná třída modelu `Movie` v aplikaci je nyní odlišná od schématu `Movie` tabulky existující databáze.</span><span class="sxs-lookup"><span data-stu-id="983d5-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="983d5-170">(V tabulce databáze nejsou žádné `Rating` sloupce.)</span><span class="sxs-lookup"><span data-stu-id="983d5-170">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="983d5-171">K řešení této chyby je potřeba několik přístupů:</span><span class="sxs-lookup"><span data-stu-id="983d5-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="983d5-172">Entity Framework automaticky vyřadit a znovu vytvořit databázi na základě nového schématu třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="983d5-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="983d5-173">Tento přístup je velmi výhodný v rané fázi vývoje, když provádíte aktivní vývoj na testovací databázi. umožňuje rychlou vývoj modelu a schématu databáze dohromady.</span><span class="sxs-lookup"><span data-stu-id="983d5-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="983d5-174">Nevýhodou, ale je to, že ztratíte stávající data v databázi, takže *nechcete tento* přístup použít v provozní databázi.</span><span class="sxs-lookup"><span data-stu-id="983d5-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="983d5-175">Použití inicializátoru k automatickému osazení databáze s testovacími daty je často produktivním způsobem pro vývoj aplikace.</span><span class="sxs-lookup"><span data-stu-id="983d5-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="983d5-176">Další informace o Entity Framework inicializátorech databáze najdete v [kurzu ASP.NET MVC/Entity Framework](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="983d5-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="983d5-177">Explicitně upravte schéma existující databáze tak, aby odpovídalo třídám modelu.</span><span class="sxs-lookup"><span data-stu-id="983d5-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="983d5-178">Výhodou tohoto přístupu je, že zachováte data.</span><span class="sxs-lookup"><span data-stu-id="983d5-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="983d5-179">Tuto změnu můžete provést buď ručně, nebo vytvořením skriptu změny databáze.</span><span class="sxs-lookup"><span data-stu-id="983d5-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="983d5-180">K aktualizaci schématu databáze použijte Migrace Code First.</span><span class="sxs-lookup"><span data-stu-id="983d5-180">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="983d5-181">V tomto kurzu použijeme Migrace Code First.</span><span class="sxs-lookup"><span data-stu-id="983d5-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="983d5-182">Aktualizujte metodu počáteční hodnoty tak, aby poskytovala hodnotu pro nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="983d5-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="983d5-183">Otevřete soubor Migrations\Configuration.cs a přidejte pole hodnocení do každého objektu filmu.</span><span class="sxs-lookup"><span data-stu-id="983d5-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="983d5-184">Sestavte řešení a otevřete okno **konzoly Správce balíčků** a zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="983d5-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="983d5-185">Příkaz `add-migration` oznamuje migračnímu rozhraní, aby kontroloval aktuální model videa s aktuálním schématem video DB a vytvořil potřebný kód pro migraci databáze do nového modelu.</span><span class="sxs-lookup"><span data-stu-id="983d5-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="983d5-186">*Hodnocení* názvu je libovolné a slouží k pojmenování souboru migrace.</span><span class="sxs-lookup"><span data-stu-id="983d5-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="983d5-187">Je užitečné použít pro krok migrace smysluplný název.</span><span class="sxs-lookup"><span data-stu-id="983d5-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="983d5-188">Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou `DbMigration` odvozenou třídu a v metodě `Up` můžete zobrazit kód, který vytvoří nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="983d5-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="983d5-189">Sestavte řešení a potom v okně **konzoly Správce balíčků** zadejte příkaz `update-database`.</span><span class="sxs-lookup"><span data-stu-id="983d5-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="983d5-190">Následující obrázek ukazuje výstup v okně **konzoly Správce balíčků** (nedokončené *hodnocení* data razítka se liší.)</span><span class="sxs-lookup"><span data-stu-id="983d5-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="983d5-191">Spusťte aplikaci znovu a přejděte na adresu URL/Movies.</span><span class="sxs-lookup"><span data-stu-id="983d5-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="983d5-192">Můžete zobrazit nové pole hodnocení.</span><span class="sxs-lookup"><span data-stu-id="983d5-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="983d5-193">Kliknutím na odkaz **vytvořit nový** přidejte nový film.</span><span class="sxs-lookup"><span data-stu-id="983d5-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="983d5-194">Všimněte si, že můžete přidat hodnocení.</span><span class="sxs-lookup"><span data-stu-id="983d5-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="983d5-196">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="983d5-196">Click **Create**.</span></span> <span data-ttu-id="983d5-197">Nový film, včetně hodnocení, se teď zobrazí v seznamu filmů:</span><span class="sxs-lookup"><span data-stu-id="983d5-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="983d5-199">Teď, když projekt používá migrace, nebudete muset databázi vyřadit, když přidáte nové pole nebo jinak aktualizujete schéma.</span><span class="sxs-lookup"><span data-stu-id="983d5-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="983d5-200">V další části provedete další změny schématu a použijete migrace k aktualizaci databáze.</span><span class="sxs-lookup"><span data-stu-id="983d5-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="983d5-201">Měli byste také přidat pole `Rating` do šablon zobrazení upravit, podrobnosti a odstranit.</span><span class="sxs-lookup"><span data-stu-id="983d5-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="983d5-202">Znovu můžete zadat příkaz "aktualizovat databázi" v okně **konzoly Správce balíčků** a spustit žádný kód migrace, protože schéma odpovídá modelu.</span><span class="sxs-lookup"><span data-stu-id="983d5-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="983d5-203">Spuštěním příkazu "Update-Database" však znovu spustíte metodu `Seed`, a pokud jste změnili jakékoli počáteční údaje, změny se ztratí, protože `Seed` metoda upsertuje data.</span><span class="sxs-lookup"><span data-stu-id="983d5-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="983d5-204">Další informace o metodě `Seed` najdete v oblíbeném [kurzu ASP.NET MVC/Entity Framework](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Dykstra.</span><span class="sxs-lookup"><span data-stu-id="983d5-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="983d5-205">V této části jste viděli, jak můžete upravovat objekty modelu a udržovat databázi synchronizované se změnami.</span><span class="sxs-lookup"><span data-stu-id="983d5-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="983d5-206">Zjistili jste taky způsob, jak naplnit nově vytvořenou databázi pomocí ukázkových dat, abyste si mohli vyzkoušet scénáře.</span><span class="sxs-lookup"><span data-stu-id="983d5-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="983d5-207">Toto bylo jenom rychlý Úvod k Code First. Další informace najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) pro ucelený kurz na daném předmětu.</span><span class="sxs-lookup"><span data-stu-id="983d5-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="983d5-208">Teď se podíváme na to, jak můžete přidat bohatou logiku ověřování do tříd modelu a povolit uplatnění některých obchodních pravidel.</span><span class="sxs-lookup"><span data-stu-id="983d5-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="983d5-209">[Předchozí](adding-search.md)
> [Další](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="983d5-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
