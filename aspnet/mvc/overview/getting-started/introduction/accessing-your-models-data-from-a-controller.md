---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Přístup k datům modelu z kontroleru | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 5d882d765133d32d3acdba9ffb5d43b69119a273
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615918"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="8998f-102">Přístup k datům modelu z kontroleru</span><span class="sxs-lookup"><span data-stu-id="8998f-102">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="8998f-103">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8998f-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="8998f-104">V této části vytvoříte novou třídu `MoviesController` a napíšete kód, který načte data videa a zobrazí se v prohlížeči pomocí šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8998f-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="8998f-105">Než začnete pokračovat k dalšímu kroku, **sestavte aplikaci** .</span><span class="sxs-lookup"><span data-stu-id="8998f-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="8998f-106">Pokud nevytvoříte aplikaci, zobrazí se chyba při přidávání kontroleru.</span><span class="sxs-lookup"><span data-stu-id="8998f-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="8998f-107">V Průzkumník řešení klikněte pravým tlačítkem na složku *Controllers* a pak klikněte na **Přidat**a pak na **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="8998f-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="8998f-108">V dialogovém okně **Přidat vygenerované uživatelské rozhraní** klikněte na **kontroler MVC 5 se zobrazeními, pomocí Entity Framework**a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="8998f-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="8998f-109">Vyberte **video (MvcMovie. Models)** pro třídu modelu.</span><span class="sxs-lookup"><span data-stu-id="8998f-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="8998f-110">Jako třídu kontextu dat vyberte **MovieDBContext (MvcMovie. Models)** .</span><span class="sxs-lookup"><span data-stu-id="8998f-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="8998f-111">Jako název kontroleru zadejte **MoviesController**.</span><span class="sxs-lookup"><span data-stu-id="8998f-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="8998f-112">Následující obrázek ukazuje dokončený dialog.</span><span class="sxs-lookup"><span data-stu-id="8998f-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="8998f-113">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="8998f-113">Click **Add**.</span></span> <span data-ttu-id="8998f-114">(Pokud se zobrazí chyba, pravděpodobně jste před zahájením přidávání kontroleru aplikaci nesestavili.) Visual Studio vytvoří následující soubory a složky:</span><span class="sxs-lookup"><span data-stu-id="8998f-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="8998f-115">Soubor *MoviesController.cs* ve složce *Controllers* .</span><span class="sxs-lookup"><span data-stu-id="8998f-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="8998f-116">Složka *Views\Movies*</span><span class="sxs-lookup"><span data-stu-id="8998f-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="8998f-117">*Vytvořte. cshtml, odstraňte. cshtml, details. cshtml, upravte. cshtml*a *index. cshtml* ve složce New *Views\Movies* .</span><span class="sxs-lookup"><span data-stu-id="8998f-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="8998f-118">Aplikace Visual Studio automaticky vytvořila metody a zobrazení akcí [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (vytváření, čtení, aktualizace a odstraňování) (automatické vytváření metod a zobrazení operace CRUD se říká generování uživatelského rozhraní).</span><span class="sxs-lookup"><span data-stu-id="8998f-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="8998f-119">Nyní máte plně funkční webovou aplikaci, která umožňuje vytvářet, zobrazovat, upravovat a odstraňovat položky filmů.</span><span class="sxs-lookup"><span data-stu-id="8998f-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="8998f-120">Spusťte aplikaci a klikněte na filmový odkaz **MVC** (nebo přejděte k řadiči `Movies` připojením */Movies* k adrese URL v adresním řádku prohlížeče).</span><span class="sxs-lookup"><span data-stu-id="8998f-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="8998f-121">Vzhledem k tomu, že se aplikace spoléhá na výchozí směrování (definované v souboru *App\_Start\RouteConfig.cs* ), požadavek `http://localhost:xxxxx/Movies` prohlížeče se směruje na výchozí metodu `Index` akce kontroleru `Movies`.</span><span class="sxs-lookup"><span data-stu-id="8998f-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="8998f-122">Jinými slovy, `http://localhost:xxxxx/Movies` požadavek prohlížeče je ve skutečnosti stejný jako `http://localhost:xxxxx/Movies/Index`žádosti prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="8998f-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="8998f-123">Výsledkem je prázdný seznam filmů, protože jste to ještě nepřidali.</span><span class="sxs-lookup"><span data-stu-id="8998f-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="8998f-124">Vytvoření filmu</span><span class="sxs-lookup"><span data-stu-id="8998f-124">Creating a Movie</span></span>

<span data-ttu-id="8998f-125">Vyberte odkaz **vytvořit nový** .</span><span class="sxs-lookup"><span data-stu-id="8998f-125">Select the **Create New** link.</span></span> <span data-ttu-id="8998f-126">Zadejte podrobnosti o videu a potom klikněte na tlačítko **vytvořit** .</span><span class="sxs-lookup"><span data-stu-id="8998f-126">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="8998f-127">V poli Price možná nebudete moct zadat desetinné nebo čárkové tečky.</span><span class="sxs-lookup"><span data-stu-id="8998f-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="8998f-128">aby bylo možné podporovat ověřování jQuery pro jiné než anglické národní prostředí, které používá čárku (&quot;,&quot;) pro desetinnou čárku a formáty kalendářních dat, které nejsou v češtině, je nutné zahrnout *globalizaci. js* a konkrétní soubory *kultury/globalizace. js* (z [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) a JavaScript pro použití `Globalize.parseFloat`.</span><span class="sxs-lookup"><span data-stu-id="8998f-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="8998f-129">Ukážeme si, jak to udělat v dalším kurzu.</span><span class="sxs-lookup"><span data-stu-id="8998f-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="8998f-130">Prozatím stačí zadat celá čísla, třeba 10.</span><span class="sxs-lookup"><span data-stu-id="8998f-130">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="8998f-131">Kliknutím na tlačítko **vytvořit** dojde k odeslání formuláře na server, kde jsou informace o filmu uloženy v databázi.</span><span class="sxs-lookup"><span data-stu-id="8998f-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="8998f-132">Pak budete přesměrováni na adresu URL */Movies* , kde uvidíte nově vytvořený film v seznamu.</span><span class="sxs-lookup"><span data-stu-id="8998f-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="8998f-133">Vytvořte ještě několik dalších záznamů filmů.</span><span class="sxs-lookup"><span data-stu-id="8998f-133">Create a couple more movie entries.</span></span> <span data-ttu-id="8998f-134">Zkuste odkazy **Upravit**, **Podrobnosti**a **Odstranit** , které jsou všechny funkční.</span><span class="sxs-lookup"><span data-stu-id="8998f-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="8998f-135">Prověřování generovaného kódu</span><span class="sxs-lookup"><span data-stu-id="8998f-135">Examining the Generated Code</span></span>

<span data-ttu-id="8998f-136">Otevřete soubor *Controllers\MoviesController.cs* a prověřte vygenerovanou metodu `Index`.</span><span class="sxs-lookup"><span data-stu-id="8998f-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="8998f-137">Část kontroleru videí s metodou `Index` je uvedena níže.</span><span class="sxs-lookup"><span data-stu-id="8998f-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="8998f-138">Požadavek na kontroler `Movies` vrátí všechny položky v tabulce `Movies` a poté předá výsledky do zobrazení `Index`.</span><span class="sxs-lookup"><span data-stu-id="8998f-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="8998f-139">Následující řádek z třídy `MoviesController` vytváří instanci kontextu databáze videa, jak je popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="8998f-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="8998f-140">Můžete použít kontext databáze videa k dotazování, úpravám a odstraňování filmů.</span><span class="sxs-lookup"><span data-stu-id="8998f-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="8998f-141">Modely silného typu a klíčové slovo @model</span><span class="sxs-lookup"><span data-stu-id="8998f-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="8998f-142">Dříve v tomto kurzu jste viděli, jak může řadič předat data nebo objekty do šablony zobrazení pomocí objektu `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="8998f-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="8998f-143">`ViewBag` je dynamický objekt, který poskytuje pohodlný způsob, jak předat informace do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8998f-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="8998f-144">MVC také poskytuje možnost předat objekty *silného* typu do šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8998f-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="8998f-145">Tento přístup silného typu umožňuje lepší kontrolu kódu a bohatší [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) v editoru sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8998f-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="8998f-146">Mechanismus generování uživatelského rozhraní v aplikaci Visual Studio používal tento přístup (to znamená předání modelu *silného* typu) s třídou `MoviesController` a zobrazení šablon při vytváření metod a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8998f-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="8998f-147">V souboru *Controllers\MoviesController.cs* prověřte vygenerovanou metodu `Details`.</span><span class="sxs-lookup"><span data-stu-id="8998f-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="8998f-148">Níže je uvedena metoda `Details`.</span><span class="sxs-lookup"><span data-stu-id="8998f-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="8998f-149">Parametr `id` se obecně předává jako data směrování, například `http://localhost:1234/movies/details/1` nastaví kontroler na filmový kontroler, akci na `details` a `id` na 1.</span><span class="sxs-lookup"><span data-stu-id="8998f-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="8998f-150">ID můžete předat také řetězci dotazu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="8998f-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="8998f-151">Pokud je nalezen `Movie`, je do zobrazení `Details` předána instance `Movie` modelu:</span><span class="sxs-lookup"><span data-stu-id="8998f-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="8998f-152">Projděte si obsah souboru *Views\Movies\Details.cshtml* :</span><span class="sxs-lookup"><span data-stu-id="8998f-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="8998f-153">Zahrnutím příkazu `@model` v horní části souboru šablony zobrazení můžete určit typ objektu, který zobrazení očekává.</span><span class="sxs-lookup"><span data-stu-id="8998f-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="8998f-154">Když jste vytvořili kontroler filmů, Visual Studio automaticky v horní části souboru *Details. cshtml* obsahuje následující příkaz `@model`:</span><span class="sxs-lookup"><span data-stu-id="8998f-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="8998f-155">Tato direktiva `@model` umožňuje přístup k videu, který kontroler předává do zobrazení pomocí objektu `Model` se silným typem.</span><span class="sxs-lookup"><span data-stu-id="8998f-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="8998f-156">Například v šabloně *Details. cshtml* kód předá do každého pole video `DisplayNameFor` a [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) nápovědu HTML pomocí objektu silného typu `Model`.</span><span class="sxs-lookup"><span data-stu-id="8998f-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="8998f-157">Metody `Create` a `Edit` a šablony zobrazení také předají objekt filmového modelu.</span><span class="sxs-lookup"><span data-stu-id="8998f-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="8998f-158">Prohlédněte si šablonu zobrazení *index. cshtml* a metodu `Index` v souboru *MoviesController.cs* .</span><span class="sxs-lookup"><span data-stu-id="8998f-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="8998f-159">Všimněte si, jak kód vytvoří objekt [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) při volání pomocné metody `View` v metodě akce `Index`.</span><span class="sxs-lookup"><span data-stu-id="8998f-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="8998f-160">Kód pak předá tento seznam `Movies` z metody `Index` akce do zobrazení:</span><span class="sxs-lookup"><span data-stu-id="8998f-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="8998f-161">Když jste vytvořili kontroler filmů, Visual Studio automaticky obsahuje následující příkaz `@model` v horní části souboru *index. cshtml* :</span><span class="sxs-lookup"><span data-stu-id="8998f-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="8998f-162">Tato direktiva `@model` umožňuje přístup k seznamu filmů, které kontroler předává do zobrazení, pomocí silně typovaného objektu `Model`.</span><span class="sxs-lookup"><span data-stu-id="8998f-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="8998f-163">Například v šabloně *index. cshtml* kód projde pomocí příkazu `foreach` přes `Model` objekt silného typu:</span><span class="sxs-lookup"><span data-stu-id="8998f-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="8998f-164">Vzhledem k tomu, že objekt `Model` je silného typu (jako objekt `IEnumerable<Movie>`), je každý objekt `item` ve smyčce zadán jako `Movie`.</span><span class="sxs-lookup"><span data-stu-id="8998f-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="8998f-165">Kromě dalších výhod to znamená, že získáte kontrolu v době kompilace kódu a úplnou podporu technologie IntelliSense v editoru kódu:</span><span class="sxs-lookup"><span data-stu-id="8998f-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="8998f-167">Práce s SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="8998f-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="8998f-168">Entity Framework Code First zjistil, že zadaný připojovací řetězec databáze odkazoval na `Movies` databázi, která ještě neexistuje, takže Code First databázi automaticky vytvořil.</span><span class="sxs-lookup"><span data-stu-id="8998f-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="8998f-169">Můžete ověřit, že se vytvořila, a to tak, že se podíváte na složku *Data\_App* .</span><span class="sxs-lookup"><span data-stu-id="8998f-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="8998f-170">Pokud nevidíte soubor *filmy. mdf* , klikněte na tlačítko **Zobrazit všechny soubory** na panelu nástrojů **Průzkumník řešení** , klikněte na tlačítko **aktualizovat** a potom rozbalte složku *\_data App* .</span><span class="sxs-lookup"><span data-stu-id="8998f-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="8998f-171">Dvojím kliknutím na *filmy. mdf* otevřete **Průzkumníka serveru**a potom rozbalte složku **Tables (tabulky** ) a zobrazte tabulku filmů.</span><span class="sxs-lookup"><span data-stu-id="8998f-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="8998f-172">Poznamenejte si klíčovou ikonu vedle pole ID.</span><span class="sxs-lookup"><span data-stu-id="8998f-172">Note the key icon next to ID.</span></span> <span data-ttu-id="8998f-173">Ve výchozím nastavení vlastnost EF vytvoří primární klíč s názvem ID.</span><span class="sxs-lookup"><span data-stu-id="8998f-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="8998f-174">Další informace o EF a MVC najdete v Dykstra skvělého kurzu na [MVC a EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="8998f-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="8998f-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="8998f-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="8998f-176">Kliknutím pravým tlačítkem na tabulku `Movies` a výběrem **Zobrazit data tabulky** zobrazíte data, která jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="8998f-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="8998f-177">Klikněte pravým tlačítkem na tabulku `Movies` a vyberte možnost **Otevřít definici tabulky** . zobrazí se struktura tabulky, která Entity Framework Code First vytvořena.</span><span class="sxs-lookup"><span data-stu-id="8998f-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="8998f-178">Všimněte si, jak se schéma `Movies` tabulky mapuje na třídu `Movie`, kterou jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="8998f-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="8998f-179">Entity Framework Code First automaticky vytvořil toto schéma na základě vaší třídy `Movie`.</span><span class="sxs-lookup"><span data-stu-id="8998f-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="8998f-180">Až skončíte, připojení zavřete kliknutím pravým tlačítkem na *MovieDBContext* a výběrem možnosti **Zavřít připojení**.</span><span class="sxs-lookup"><span data-stu-id="8998f-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="8998f-181">(Pokud připojení neukončíte, při příštím spuštění projektu se může zobrazit chyba.</span><span class="sxs-lookup"><span data-stu-id="8998f-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

<span data-ttu-id="8998f-182">Teď máte databázi a stránky k zobrazení, úpravám, aktualizaci a odstraňování dat.</span><span class="sxs-lookup"><span data-stu-id="8998f-182">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="8998f-183">V dalším kurzu prověříme zbytek vygenerovaného kódu a přidáte `SearchIndex` metodu a `SearchIndex` zobrazení, které vám umožní vyhledat filmy v této databázi.</span><span class="sxs-lookup"><span data-stu-id="8998f-183">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="8998f-184">Další informace o použití Entity Framework s MVC najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="8998f-184">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8998f-185">[Předchozí](creating-a-connection-string.md)
> [Další](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="8998f-185">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
