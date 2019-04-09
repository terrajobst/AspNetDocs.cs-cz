---
uid: mvc/overview/getting-started/introduction/adding-search
title: Hledání | Dokumentace Microsoftu
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: 7b49c1e6425080693229c6c132df3879504c835c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379531"
---
# <a name="search"></a><span data-ttu-id="5c173-102">Hledat</span><span class="sxs-lookup"><span data-stu-id="5c173-102">Search</span></span>


[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="5c173-103">Přidání vyhledávací metody a zobrazení vyhledávání</span><span class="sxs-lookup"><span data-stu-id="5c173-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="5c173-104">V této části přidáte možnost vyhledávání `Index` metody akce, která umožňuje hledat filmy podle žánru nebo názvu.</span><span class="sxs-lookup"><span data-stu-id="5c173-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c173-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5c173-105">Prerequisites</span></span>

<span data-ttu-id="5c173-106">Tak, aby odpovídala této části snímky obrazovky, musíte spustit aplikaci (F5) a přidejte následující videa do databáze.</span><span class="sxs-lookup"><span data-stu-id="5c173-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="5c173-107">Název</span><span class="sxs-lookup"><span data-stu-id="5c173-107">Title</span></span> | <span data-ttu-id="5c173-108">Datum vydání</span><span class="sxs-lookup"><span data-stu-id="5c173-108">Release Date</span></span> | <span data-ttu-id="5c173-109">Genre</span><span class="sxs-lookup"><span data-stu-id="5c173-109">Genre</span></span> | <span data-ttu-id="5c173-110">Cena</span><span class="sxs-lookup"><span data-stu-id="5c173-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="5c173-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="5c173-111">Ghostbusters</span></span> | <span data-ttu-id="5c173-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="5c173-112">6/8/1984</span></span> | <span data-ttu-id="5c173-113">Komedie</span><span class="sxs-lookup"><span data-stu-id="5c173-113">Comedy</span></span> | <span data-ttu-id="5c173-114">6.99</span><span class="sxs-lookup"><span data-stu-id="5c173-114">6.99</span></span> |
| <span data-ttu-id="5c173-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="5c173-115">Ghostbusters II</span></span> | <span data-ttu-id="5c173-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="5c173-116">6/16/1989</span></span> | <span data-ttu-id="5c173-117">Komedie</span><span class="sxs-lookup"><span data-stu-id="5c173-117">Comedy</span></span> | <span data-ttu-id="5c173-118">6.99</span><span class="sxs-lookup"><span data-stu-id="5c173-118">6.99</span></span> |
| <span data-ttu-id="5c173-119">Globálním opice</span><span class="sxs-lookup"><span data-stu-id="5c173-119">Planet of the Apes</span></span> | <span data-ttu-id="5c173-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="5c173-120">3/27/1986</span></span> | <span data-ttu-id="5c173-121">Akce</span><span class="sxs-lookup"><span data-stu-id="5c173-121">Action</span></span> | <span data-ttu-id="5c173-122">5.99</span><span class="sxs-lookup"><span data-stu-id="5c173-122">5.99</span></span> |


## <a name="updating-the-index-form"></a><span data-ttu-id="5c173-123">Aktualizuje se Index formuláře</span><span class="sxs-lookup"><span data-stu-id="5c173-123">Updating the Index Form</span></span>

<span data-ttu-id="5c173-124">Začněte tím, že aktualizace `Index` metody akce ke stávající `MoviesController` třídy.</span><span class="sxs-lookup"><span data-stu-id="5c173-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="5c173-125">Zde je kód:</span><span class="sxs-lookup"><span data-stu-id="5c173-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="5c173-126">První řádek `Index` metoda vytvoří následující [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) dotaz pro výběr videa:</span><span class="sxs-lookup"><span data-stu-id="5c173-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="5c173-127">Dotaz je definován v tomto okamžiku, ale nebyl dosud spuštěn na databázi.</span><span class="sxs-lookup"><span data-stu-id="5c173-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="5c173-128">Pokud `searchString` parametr obsahuje řetězec, dotaz filmy je upravit tak, aby filtrování na základě hodnoty hledaný řetězec, pomocí následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="5c173-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="5c173-129">`s => s.Title` Je výše uvedený kód [výraz Lambda](https://msdn.microsoft.com/library/bb397687.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c173-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="5c173-130">Výrazy lambda se používají v založených na volání metody [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) dotazuje jako argumenty pro standardní metody operátoru dotazu, jako [kde](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) metodu používanou ve výše uvedeném kódu.</span><span class="sxs-lookup"><span data-stu-id="5c173-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="5c173-131">Dotazy LINQ nejsou provedeny, když jsou definovány, nebo při jejich změně voláním metody `Where` nebo `OrderBy`.</span><span class="sxs-lookup"><span data-stu-id="5c173-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="5c173-132">Místo toho provádění dotazu je odloženo, což znamená, že vyhodnocení výrazu je odloženo jeho očekávané hodnoty ve skutečnosti procházen nebo [ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx) metoda je volána.</span><span class="sxs-lookup"><span data-stu-id="5c173-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="5c173-133">V `Search` vzorku a spuštění dotazu v *Index.cshtml* zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5c173-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="5c173-134">Další informace o odložený dotaz, naleznete v tématu [provádění dotazu](https://msdn.microsoft.com/library/bb738633.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c173-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5c173-135">[Obsahuje](https://msdn.microsoft.com/library/bb155125.aspx) metodu spustíte v databázi, není kód jazyka c# výše.</span><span class="sxs-lookup"><span data-stu-id="5c173-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="5c173-136">V databázi [obsahuje](https://msdn.microsoft.com/library/bb155125.aspx) mapuje [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), což je malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="5c173-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="5c173-137">Nyní můžete aktualizovat `Index` zobrazení, které se uživateli zobrazí formulář.</span><span class="sxs-lookup"><span data-stu-id="5c173-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="5c173-138">Spusťte aplikaci a přejděte do */filmy/Index*.</span><span class="sxs-lookup"><span data-stu-id="5c173-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="5c173-139">Připojte řetězec dotazu jako `?searchString=ghost` na adresu URL.</span><span class="sxs-lookup"><span data-stu-id="5c173-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="5c173-140">Zobrazují se filtrované filmy.</span><span class="sxs-lookup"><span data-stu-id="5c173-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="5c173-142">Pokud se změní podpis `Index` metoda může mít parametr s názvem `id`, `id` parametr budou odpovídat `{id}` zástupný symbol pro výchozí trasy sady v *aplikace\_Start\ RouteConfig.cs* souboru.</span><span class="sxs-lookup"><span data-stu-id="5c173-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="5c173-143">Původní `Index` metoda vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="5c173-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="5c173-144">Upravené `Index` metoda vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="5c173-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="5c173-145">Nyní lze předat název vyhledávání jako data trasy (segment adresy URL) místo jako hodnotu řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="5c173-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="5c173-146">Ale nemůžete očekávat, že uživatelům změnit adresu URL pokaždé, když chtějí hledat videa.</span><span class="sxs-lookup"><span data-stu-id="5c173-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="5c173-147">Takže teď přidáte uživatelského rozhraní, aby to pomohl ostatním filtrovat videa.</span><span class="sxs-lookup"><span data-stu-id="5c173-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="5c173-148">Pokud jste změnili podpis `Index` metody testování jak předat parametru ID vázané na trasy, změňte ho tak, aby vaše `Index` metoda použije parametr řetězce s názvem `searchString`:</span><span class="sxs-lookup"><span data-stu-id="5c173-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="5c173-149">Otevřít *Views\Movies\Index.cshtml* souboru a jenom po `@Html.ActionLink("Create New", "Create")`, přidejte značku formuláře, jejichž přehled najdete níže:</span><span class="sxs-lookup"><span data-stu-id="5c173-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="5c173-150">`Html.BeginForm` Pomocné rutiny vytvoří počáteční `<form>` značky.</span><span class="sxs-lookup"><span data-stu-id="5c173-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="5c173-151">`Html.BeginForm` Pomocné rutiny způsobí, že formulář ke zveřejnění na sebe sama, jakmile uživatel formulář odešle kliknutím **filtr** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="5c173-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="5c173-152">Visual Studio 2013 obsahuje nice zlepšování při zobrazení a úpravy souborů zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5c173-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="5c173-153">Při spuštění aplikace se zobrazit soubor otevřít, Visual Studio 2013 vyvolá metoda akce kontroleru správné zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5c173-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="5c173-154">Když je zobrazení indexu otevřete v sadě Visual Studio (jak je znázorněno na obrázku výše), klepněte na pev.cenu F5 nebo F5 spusťte aplikaci a pak zkuste vyhledat videa.</span><span class="sxs-lookup"><span data-stu-id="5c173-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="5c173-155">Neexistuje žádná `HttpPost` přetížení `Index` metody.</span><span class="sxs-lookup"><span data-stu-id="5c173-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="5c173-156">Není nutné, protože metoda není změněn stav aplikace, stačí filtrování dat.</span><span class="sxs-lookup"><span data-stu-id="5c173-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="5c173-157">Můžete přidat následující `HttpPost Index` metody.</span><span class="sxs-lookup"><span data-stu-id="5c173-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="5c173-158">V takovém případě by odpovídala původce volání akce `HttpPost Index` metody a `HttpPost Index` spustili byste metodu, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="5c173-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="5c173-160">Ale i v případě, že přidáte to `HttpPost` verzi `Index` metoda, existuje omezení v tom, jak to vše implementován.</span><span class="sxs-lookup"><span data-stu-id="5c173-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="5c173-161">Představte si, že chcete konkrétní hledání (záložky) nebo chcete poslat odkaz s přáteli, mohou kliknout, chcete-li zobrazit stejné filtrovaný seznam videa.</span><span class="sxs-lookup"><span data-stu-id="5c173-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="5c173-162">Všimněte si, že adresa URL pro odeslání požadavku HTTP POST je stejný jako adresu URL pro požadavek na získání (localhost:xxxxx/filmy/Index) – není k dispozici žádné informace o vyhledávání v adrese URL samotného.</span><span class="sxs-lookup"><span data-stu-id="5c173-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="5c173-163">Pravé teď vyhledávací řetězec informace jsou odeslány na server jako hodnotu pole formuláře.</span><span class="sxs-lookup"><span data-stu-id="5c173-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="5c173-164">To znamená, že nelze zachytit tyto informace vyhledávání (záložky) nebo odeslat přátel v adrese URL.</span><span class="sxs-lookup"><span data-stu-id="5c173-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="5c173-165">Řešením je použití přetížení `BeginForm` , která určuje, že požadavek POST by měla přidat informace o hledání na adresu URL a, že by měl směrovat na `HttpGet` verzi `Index` metody.</span><span class="sxs-lookup"><span data-stu-id="5c173-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="5c173-166">Nahraďte existující konstruktor bez parametrů `BeginForm` metoda následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="5c173-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="5c173-168">Nyní když odešlete vyhledávání, adresa URL obsahuje hledaný řetězec dotazu.</span><span class="sxs-lookup"><span data-stu-id="5c173-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="5c173-169">Hledání budou také moct `HttpGet Index` metodě akce, i když máte `HttpPost Index` metody.</span><span class="sxs-lookup"><span data-stu-id="5c173-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="5c173-171">Přidání vyhledávání podle žánru</span><span class="sxs-lookup"><span data-stu-id="5c173-171">Adding Search by Genre</span></span>

<span data-ttu-id="5c173-172">Pokud jste přidali `HttpPost` verzi `Index` metoda, odstraňte ji.</span><span class="sxs-lookup"><span data-stu-id="5c173-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="5c173-173">V dalším kroku přidáte funkci, která umožňují uživatelům vyhledat filmy podle žánru.</span><span class="sxs-lookup"><span data-stu-id="5c173-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="5c173-174">Nahradit `Index` metodu s následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="5c173-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="5c173-175">Tato verze `Index` metoda přijímá další parametr, a to `movieGenre`.</span><span class="sxs-lookup"><span data-stu-id="5c173-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="5c173-176">Vytvoření první několika řádků kódu `List` objekt pro uložení žánry video z databáze.</span><span class="sxs-lookup"><span data-stu-id="5c173-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="5c173-177">Následující kód je dotaz LINQ, který načte všechny žánry z databáze.</span><span class="sxs-lookup"><span data-stu-id="5c173-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="5c173-178">Tento kód použije `AddRange` metoda Obecné `List` kolekce pro přidání různých žánry do seznamu.</span><span class="sxs-lookup"><span data-stu-id="5c173-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="5c173-179">(Bez `Distinct` modifikátor, byly přidány duplicitní žánry – například byly přidány komedie dvakrát v naší ukázce).</span><span class="sxs-lookup"><span data-stu-id="5c173-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="5c173-180">Pak uloží seznam žánry v kódu `ViewBag.MovieGenre` objektu.</span><span class="sxs-lookup"><span data-stu-id="5c173-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="5c173-181">Ukládání kategorie dat (takové film žánry) jako [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) objekt `ViewBag`, pak je obvyklý postup pro aplikace MVC se přístup k datům kategorie v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="5c173-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="5c173-182">Následující kód ukazuje, jak zkontrolovat `movieGenre` parametru.</span><span class="sxs-lookup"><span data-stu-id="5c173-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="5c173-183">Pokud není prázdná, omezí kód dál filmy dotaz omezit vybrané videa k zadaným rozšířením podle tematických.</span><span class="sxs-lookup"><span data-stu-id="5c173-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="5c173-184">Jak bylo uvedeno dříve, dotaz se nespouští na databázi, dokud není procházen seznamu video (který se stane v zobrazení po `Index` metoda akce vrací).</span><span class="sxs-lookup"><span data-stu-id="5c173-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="5c173-185">Přidání značek do zobrazení Index pro podporu vyhledávání podle žánru</span><span class="sxs-lookup"><span data-stu-id="5c173-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="5c173-186">Přidat `Html.DropDownList` pomocná rutina pro *Views\Movies\Index.cshtml* souboru, těsně před `TextBox` pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="5c173-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="5c173-187">Dokončený kód je zobrazena níže:</span><span class="sxs-lookup"><span data-stu-id="5c173-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="5c173-188">V následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="5c173-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="5c173-189">Poskytuje klíč pro parametr "MovieGenre" `DropDownList` pomocná rutina pro vyhledání `IEnumerable<SelectListItem>` v `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="5c173-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="5c173-190">`ViewBag` Používala v metodě akce:</span><span class="sxs-lookup"><span data-stu-id="5c173-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="5c173-191">Parametr "All" poskytuje popisku.</span><span class="sxs-lookup"><span data-stu-id="5c173-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="5c173-192">Pokud tato volba si prohlédnout v prohlížeči, uvidíte, že jeho atribut "value" je prázdný.</span><span class="sxs-lookup"><span data-stu-id="5c173-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="5c173-193">Protože kontroleru pouze filtruje `if` řetězec není `null` nebo je prázdná, prázdná hodnota pro odesílání `movieGenre` ukazuje všechny žánrů.</span><span class="sxs-lookup"><span data-stu-id="5c173-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="5c173-194">Můžete také nastavit možnost vybrat ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="5c173-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="5c173-195">Pokud byste chtěli "Komedie" jako výchozí možnost, chcete změnit kód v Kontroleru takto:</span><span class="sxs-lookup"><span data-stu-id="5c173-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="5c173-196">Spusťte aplikaci a přejděte do */filmy/Index*.</span><span class="sxs-lookup"><span data-stu-id="5c173-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="5c173-197">Zkuste hledat podle žánru, název filmu a obě kritéria.</span><span class="sxs-lookup"><span data-stu-id="5c173-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="5c173-198">V této části vytvoříte metody akce vyhledávání a zobrazení, které umožňují uživatelům vyhledat tak, že název filmu a rozšířením podle tematických.</span><span class="sxs-lookup"><span data-stu-id="5c173-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="5c173-199">V další části, budete pohledu na tom, jak přidat vlastnost, která má `Movie` modelu a přidání inicializátoru, který se automaticky vytvoří testovací databáze.</span><span class="sxs-lookup"><span data-stu-id="5c173-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c173-200">[Předchozí](examining-the-edit-methods-and-edit-view.md)
> [další](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="5c173-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
