---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: Přístup k datům modelu z kontroleru | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540388"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="7f26b-104">Přístup k datům modelu z kontroleru</span><span class="sxs-lookup"><span data-stu-id="7f26b-104">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="7f26b-105">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7f26b-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="7f26b-106">K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7f26b-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="7f26b-107">Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.</span><span class="sxs-lookup"><span data-stu-id="7f26b-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="7f26b-108">V této části vytvoříte novou třídu `MoviesController` a napíšete kód, který načte data videa a zobrazí se v prohlížeči pomocí šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="7f26b-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="7f26b-109">Než začnete pokračovat k dalšímu kroku, **sestavte aplikaci** .</span><span class="sxs-lookup"><span data-stu-id="7f26b-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="7f26b-110">Klikněte pravým tlačítkem na složku *Controllers* a vytvořte nový kontroler `MoviesController`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="7f26b-111">Níže uvedené možnosti se nezobrazí, dokud nevytvoříte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="7f26b-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="7f26b-112">Vyberte následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="7f26b-112">Select the following options:</span></span>

- <span data-ttu-id="7f26b-113">Název kontroleru: **MoviesController**.</span><span class="sxs-lookup"><span data-stu-id="7f26b-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="7f26b-114">(Toto je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="7f26b-114">(This is the default.</span></span> <span data-ttu-id="7f26b-115">)</span><span class="sxs-lookup"><span data-stu-id="7f26b-115">)</span></span>
- <span data-ttu-id="7f26b-116">Šablona: **kontroler MVC s akcemi a zobrazeními pro čtení/zápis pomocí Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="7f26b-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="7f26b-117">Třída modelu: **video (MvcMovie. Models)** .</span><span class="sxs-lookup"><span data-stu-id="7f26b-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="7f26b-118">Třída kontextu dat: **MovieDBContext (MvcMovie. Models)** .</span><span class="sxs-lookup"><span data-stu-id="7f26b-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="7f26b-119">Zobrazení: **Razor (cshtml)** .</span><span class="sxs-lookup"><span data-stu-id="7f26b-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="7f26b-120">(Výchozí nastavení.)</span><span class="sxs-lookup"><span data-stu-id="7f26b-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="7f26b-122">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="7f26b-122">Click **Add**.</span></span> <span data-ttu-id="7f26b-123">Visual Studio Express vytvoří následující soubory a složky:</span><span class="sxs-lookup"><span data-stu-id="7f26b-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="7f26b-124">Soubor *MoviesController.cs* ve složce *řadičů* projektu.</span><span class="sxs-lookup"><span data-stu-id="7f26b-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="7f26b-125">Složka *filmy* ve složce *zobrazení* projektu.</span><span class="sxs-lookup"><span data-stu-id="7f26b-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="7f26b-126">*Vytvořte. cshtml, odstraňte. cshtml, details. cshtml, upravte. cshtml*a *index. cshtml* ve složce New *Views\Movies* .</span><span class="sxs-lookup"><span data-stu-id="7f26b-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="7f26b-127">ASP.NET MVC 4 automaticky vytvořila metody a zobrazení akcí CRUD (vytváření, čtení, aktualizace a odstraňování) (automatické vytváření metod a zobrazení operací CRUD se říká generování uživatelského rozhraní).</span><span class="sxs-lookup"><span data-stu-id="7f26b-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="7f26b-128">Nyní máte plně funkční webovou aplikaci, která umožňuje vytvářet, zobrazovat, upravovat a odstraňovat položky filmů.</span><span class="sxs-lookup"><span data-stu-id="7f26b-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="7f26b-129">Spusťte aplikaci a přejděte k řadiči `Movies` připojením */Movies* k adrese URL v adresním řádku prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="7f26b-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="7f26b-130">Vzhledem k tomu, že se aplikace spoléhá na výchozí směrování (definované v souboru *Global. asax* ), je požadavek prohlížeče `http://localhost:xxxxx/Movies` směrován do výchozí metody `Index` action kontroleru `Movies`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="7f26b-131">Jinými slovy, `http://localhost:xxxxx/Movies` požadavek prohlížeče je ve skutečnosti stejný jako `http://localhost:xxxxx/Movies/Index`žádosti prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="7f26b-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="7f26b-132">Výsledkem je prázdný seznam filmů, protože jste to ještě nepřidali.</span><span class="sxs-lookup"><span data-stu-id="7f26b-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="7f26b-133">Vytvoření filmu</span><span class="sxs-lookup"><span data-stu-id="7f26b-133">Creating a Movie</span></span>

<span data-ttu-id="7f26b-134">Vyberte odkaz **vytvořit nový** .</span><span class="sxs-lookup"><span data-stu-id="7f26b-134">Select the **Create New** link.</span></span> <span data-ttu-id="7f26b-135">Zadejte podrobnosti o videu a potom klikněte na tlačítko **vytvořit** .</span><span class="sxs-lookup"><span data-stu-id="7f26b-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="7f26b-136">Kliknutím na tlačítko **vytvořit** dojde k odeslání formuláře na server, kde jsou informace o filmu uloženy v databázi.</span><span class="sxs-lookup"><span data-stu-id="7f26b-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="7f26b-137">Pak budete přesměrováni na adresu URL */Movies* , kde uvidíte nově vytvořený film v seznamu.</span><span class="sxs-lookup"><span data-stu-id="7f26b-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="7f26b-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span><span class="sxs-lookup"><span data-stu-id="7f26b-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="7f26b-139">Vytvořte ještě několik dalších záznamů filmů.</span><span class="sxs-lookup"><span data-stu-id="7f26b-139">Create a couple more movie entries.</span></span> <span data-ttu-id="7f26b-140">Zkuste odkazy **Upravit**, **Podrobnosti**a **Odstranit** , které jsou všechny funkční.</span><span class="sxs-lookup"><span data-stu-id="7f26b-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="7f26b-141">Prověřování generovaného kódu</span><span class="sxs-lookup"><span data-stu-id="7f26b-141">Examining the Generated Code</span></span>

<span data-ttu-id="7f26b-142">Otevřete soubor *Controllers\MoviesController.cs* a prověřte vygenerovanou metodu `Index`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="7f26b-143">Část kontroleru videí s metodou `Index` je uvedena níže.</span><span class="sxs-lookup"><span data-stu-id="7f26b-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="7f26b-144">Následující řádek z třídy `MoviesController` vytváří instanci kontextu databáze videa, jak je popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="7f26b-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="7f26b-145">Můžete použít kontext databáze videa k dotazování, úpravám a odstraňování filmů.</span><span class="sxs-lookup"><span data-stu-id="7f26b-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="7f26b-146">Požadavek na kontroler `Movies` vrátí všechny položky v tabulce `Movies` v databázi videa a poté předá výsledky do zobrazení `Index`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="7f26b-147">Modely silného typu a klíčové slovo @model</span><span class="sxs-lookup"><span data-stu-id="7f26b-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="7f26b-148">Dříve v tomto kurzu jste viděli, jak může řadič předat data nebo objekty do šablony zobrazení pomocí objektu `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="7f26b-149">`ViewBag` je dynamický objekt, který poskytuje pohodlný způsob, jak předat informace do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="7f26b-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="7f26b-150">ASP.NET MVC také poskytuje možnost předat data silného typu nebo objekty do šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="7f26b-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="7f26b-151">Tento přístup silného typu umožňuje lepší kontrolu kódu a bohatší IntelliSense v editoru sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f26b-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="7f26b-152">Mechanizmus pro generování uživatelského rozhraní v aplikaci Visual Studio používal tento přístup ke třídě `MoviesController` a zobrazení šablon při vytváření metod a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="7f26b-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="7f26b-153">V souboru *Controllers\MoviesController.cs* prověřte vygenerovanou metodu `Details`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="7f26b-154">Část kontroleru videí s metodou `Details` je uvedena níže.</span><span class="sxs-lookup"><span data-stu-id="7f26b-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="7f26b-155">Pokud je nalezen `Movie`, je do zobrazení podrobností předána instance modelu `Movie`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="7f26b-156">Prověřte obsah souboru *Views\Movies\Details.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="7f26b-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="7f26b-157">Zahrnutím příkazu `@model` v horní části souboru šablony zobrazení můžete určit typ objektu, který zobrazení očekává.</span><span class="sxs-lookup"><span data-stu-id="7f26b-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="7f26b-158">Když jste vytvořili kontroler filmů, Visual Studio automaticky v horní části souboru *Details. cshtml* obsahuje následující příkaz `@model`:</span><span class="sxs-lookup"><span data-stu-id="7f26b-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="7f26b-159">Tato direktiva `@model` umožňuje přístup k videu, který kontroler předává do zobrazení pomocí objektu `Model` se silným typem.</span><span class="sxs-lookup"><span data-stu-id="7f26b-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="7f26b-160">Například v šabloně *Details. cshtml* kód předá do každého pole video `DisplayNameFor` a [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) nápovědu HTML pomocí objektu silného typu `Model`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="7f26b-161">Metody Create a Edit a zobrazení šablony také předají objekt filmového modelu.</span><span class="sxs-lookup"><span data-stu-id="7f26b-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="7f26b-162">Prohlédněte si šablonu zobrazení *index. cshtml* a metodu `Index` v souboru *MoviesController.cs* .</span><span class="sxs-lookup"><span data-stu-id="7f26b-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="7f26b-163">Všimněte si, jak kód vytvoří objekt [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) při volání pomocné metody `View` v metodě akce `Index`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="7f26b-164">Kód pak předá tento seznam `Movies` z kontroleru k zobrazení:</span><span class="sxs-lookup"><span data-stu-id="7f26b-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="7f26b-165">Když jste vytvořili kontroler filmů, Visual Studio Express do horní části souboru *index. cshtml* automaticky zahrnout následující `@model` příkaz:</span><span class="sxs-lookup"><span data-stu-id="7f26b-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="7f26b-166">Tato direktiva `@model` umožňuje přístup k seznamu filmů, které kontroler předává do zobrazení, pomocí silně typovaného objektu `Model`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="7f26b-167">Například v šabloně *index. cshtml* kód projde pomocí příkazu `foreach` přes `Model` objekt silného typu:</span><span class="sxs-lookup"><span data-stu-id="7f26b-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="7f26b-168">Vzhledem k tomu, že objekt `Model` je silného typu (jako objekt `IEnumerable<Movie>`), je každý objekt `item` ve smyčce zadán jako `Movie`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="7f26b-169">Kromě dalších výhod to znamená, že získáte kontrolu v době kompilace kódu a úplnou podporu technologie IntelliSense v editoru kódu:</span><span class="sxs-lookup"><span data-stu-id="7f26b-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="7f26b-171">Práce s SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="7f26b-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="7f26b-172">Entity Framework Code First zjistil, že zadaný připojovací řetězec databáze odkazoval na `Movies` databázi, která ještě neexistuje, takže Code First databázi automaticky vytvořil.</span><span class="sxs-lookup"><span data-stu-id="7f26b-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="7f26b-173">Můžete ověřit, že se vytvořila, a to tak, že se podíváte na složku *Data\_App* .</span><span class="sxs-lookup"><span data-stu-id="7f26b-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="7f26b-174">Pokud nevidíte soubor *filmy. mdf* , klikněte na tlačítko **Zobrazit všechny soubory** na panelu nástrojů **Průzkumník řešení** , klikněte na tlačítko **aktualizovat** a potom rozbalte složku *\_data App* .</span><span class="sxs-lookup"><span data-stu-id="7f26b-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="7f26b-175">Dvojím kliknutím na *filmy. mdf* otevřete **Průzkumníka databáze**a potom rozbalte složku **Tables (tabulky** ) a zobrazte tabulku filmů.</span><span class="sxs-lookup"><span data-stu-id="7f26b-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="7f26b-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="7f26b-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="7f26b-177">Pokud se Průzkumník databáze nezobrazí, v nabídce **nástroje** vyberte **připojit k databázi**a pak zrušte dialog **Zvolit zdroj dat** .</span><span class="sxs-lookup"><span data-stu-id="7f26b-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="7f26b-178">Tím se vynutí otevření Průzkumníka databáze.</span><span class="sxs-lookup"><span data-stu-id="7f26b-178">This will force open the database explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="7f26b-179">Pokud používáte souboru vwd nebo Visual Studio 2010 a získáte chybu podobnou následující:</span><span class="sxs-lookup"><span data-stu-id="7f26b-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="7f26b-180">Databáze ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES. MDF nelze otevřít, protože je verze 706.</span><span class="sxs-lookup"><span data-stu-id="7f26b-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="7f26b-181">Tento server podporuje verzi 655 a starší.</span><span class="sxs-lookup"><span data-stu-id="7f26b-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="7f26b-182">Cesta k downgradu není podporována.</span><span class="sxs-lookup"><span data-stu-id="7f26b-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="7f26b-183">&quot;výjimka nebyla ošetřena uživatelským kódem&quot; zadaný SqlConnection neurčuje počáteční katalog.</span><span class="sxs-lookup"><span data-stu-id="7f26b-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="7f26b-184">Musíte nainstalovat [nástroje SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) a [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span><span class="sxs-lookup"><span data-stu-id="7f26b-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="7f26b-185">Ověřte `MovieDBContext` připojovací řetězec zadaný na předchozí stránce.</span><span class="sxs-lookup"><span data-stu-id="7f26b-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>

<span data-ttu-id="7f26b-186">Kliknutím pravým tlačítkem na tabulku `Movies` a výběrem **Zobrazit data tabulky** zobrazíte data, která jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="7f26b-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="7f26b-187">Klikněte pravým tlačítkem na tabulku `Movies` a vyberte možnost **Otevřít definici tabulky** . zobrazí se struktura tabulky, která Entity Framework Code First vytvořena.</span><span class="sxs-lookup"><span data-stu-id="7f26b-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="7f26b-188">Všimněte si, jak se schéma `Movies` tabulky mapuje na třídu `Movie`, kterou jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="7f26b-188">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="7f26b-189">Entity Framework Code First automaticky vytvořil toto schéma na základě vaší třídy `Movie`.</span><span class="sxs-lookup"><span data-stu-id="7f26b-189">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="7f26b-190">Až skončíte, připojení zavřete kliknutím pravým tlačítkem na *MovieDBContext* a výběrem možnosti **Zavřít připojení**.</span><span class="sxs-lookup"><span data-stu-id="7f26b-190">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="7f26b-191">(Pokud připojení neukončíte, při příštím spuštění projektu se může zobrazit chyba.</span><span class="sxs-lookup"><span data-stu-id="7f26b-191">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

<span data-ttu-id="7f26b-192">Teď máte databázi a jednoduchou stránku se seznamem, ze které můžete zobrazit obsah.</span><span class="sxs-lookup"><span data-stu-id="7f26b-192">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="7f26b-193">V dalším kurzu prověříme zbytek vygenerovaného kódu a přidáte `SearchIndex` metodu a `SearchIndex` zobrazení, které vám umožní vyhledat filmy v této databázi.</span><span class="sxs-lookup"><span data-stu-id="7f26b-193">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7f26b-194">[Předchozí](adding-a-model.md)
> [Další](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="7f26b-194">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
