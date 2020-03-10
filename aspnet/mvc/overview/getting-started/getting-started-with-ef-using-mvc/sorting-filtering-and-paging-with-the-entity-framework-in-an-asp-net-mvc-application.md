---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: Přidání řazení, filtrování a stránkování pomocí Entity Framework v aplikaci ASP.NET MVC | Microsoft Docs'
author: tdykstra
description: V tomto kurzu přidáte na stránku indexu **studentů** funkce řazení, filtrování a stránkování. Můžete také vytvořit jednoduchou stránku seskupení.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616037"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="fd343-104">Kurz: Přidání řazení, filtrování a stránkování s Entity Framework v aplikaci MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fd343-104">Tutorial: Add sorting, filtering, and paging with the Entity Framework in an ASP.NET MVC application</span></span>

<span data-ttu-id="fd343-105">V [předchozím kurzu](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)jste implementovali sadu webových stránek pro základní operace CRUD pro `Student` entit.</span><span class="sxs-lookup"><span data-stu-id="fd343-105">In the [previous tutorial](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="fd343-106">V tomto kurzu přidáte na stránku indexu **studentů** funkce řazení, filtrování a stránkování.</span><span class="sxs-lookup"><span data-stu-id="fd343-106">In this tutorial you add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="fd343-107">Můžete také vytvořit jednoduchou stránku seskupení.</span><span class="sxs-lookup"><span data-stu-id="fd343-107">You also create a simple grouping page.</span></span>

<span data-ttu-id="fd343-108">Následující obrázek ukazuje, jak stránka bude vypadat, až budete hotovi.</span><span class="sxs-lookup"><span data-stu-id="fd343-108">The following image shows what the page will look like when you're done.</span></span> <span data-ttu-id="fd343-109">Záhlaví sloupců jsou odkazy, na které může uživatel kliknout pro řazení podle daného sloupce.</span><span class="sxs-lookup"><span data-stu-id="fd343-109">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="fd343-110">Kliknutí na záhlaví sloupce se opakovaně přepíná mezi vzestupném a sestupným řazením.</span><span class="sxs-lookup"><span data-stu-id="fd343-110">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="fd343-112">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="fd343-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fd343-113">Přidat odkazy na řazení sloupců</span><span class="sxs-lookup"><span data-stu-id="fd343-113">Add column sort links</span></span>
> * <span data-ttu-id="fd343-114">Přidání vyhledávacího pole</span><span class="sxs-lookup"><span data-stu-id="fd343-114">Add a Search box</span></span>
> * <span data-ttu-id="fd343-115">Přidat stránkování</span><span class="sxs-lookup"><span data-stu-id="fd343-115">Add paging</span></span>
> * <span data-ttu-id="fd343-116">Vytvoření stránky o stránku</span><span class="sxs-lookup"><span data-stu-id="fd343-116">Create an About page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd343-117">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="fd343-117">Prerequisites</span></span>

* [<span data-ttu-id="fd343-118">Implementace základních funkcí CRUD</span><span class="sxs-lookup"><span data-stu-id="fd343-118">Implementing Basic CRUD Functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a><span data-ttu-id="fd343-119">Přidat odkazy na řazení sloupců</span><span class="sxs-lookup"><span data-stu-id="fd343-119">Add column sort links</span></span>

<span data-ttu-id="fd343-120">Chcete-li přidat řazení na stránku indexu studenta, změňte metodu `Index` řadiče `Student` a přidejte kód do zobrazení indexu `Student`.</span><span class="sxs-lookup"><span data-stu-id="fd343-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="fd343-121">Přidání funkcí řazení do metody index</span><span class="sxs-lookup"><span data-stu-id="fd343-121">Add sorting functionality to the Index method</span></span>

- <span data-ttu-id="fd343-122">V *Controllers\StudentController.cs*nahraďte metodu `Index` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="fd343-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="fd343-123">Tento kód přijímá `sortOrder` parametr z řetězce dotazu v adrese URL.</span><span class="sxs-lookup"><span data-stu-id="fd343-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="fd343-124">Hodnota řetězce dotazu je poskytnuta ASP.NET MVC jako parametr metody Action.</span><span class="sxs-lookup"><span data-stu-id="fd343-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="fd343-125">Parametr je řetězec, který je buď "Name", nebo "date", volitelně následovaný podtržítkem a řetězcem "desc" pro určení sestupného pořadí.</span><span class="sxs-lookup"><span data-stu-id="fd343-125">The parameter is a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="fd343-126">Výchozí pořadí řazení je vzestupné.</span><span class="sxs-lookup"><span data-stu-id="fd343-126">The default sort order is ascending.</span></span>

<span data-ttu-id="fd343-127">Při prvním vyžádání stránky indexu není k dispozici žádný řetězec dotazu.</span><span class="sxs-lookup"><span data-stu-id="fd343-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="fd343-128">Studenti se zobrazí ve vzestupném pořadí podle `LastName`, což je výchozí nastavení zavedené v případě příkazu `switch`.</span><span class="sxs-lookup"><span data-stu-id="fd343-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="fd343-129">Když uživatel klikne na hypertextový odkaz záhlaví sloupce, v řetězci dotazu je uvedena odpovídající hodnota `sortOrder`.</span><span class="sxs-lookup"><span data-stu-id="fd343-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="fd343-130">Použijí se tyto dvě proměnné `ViewBag`, aby zobrazení mohl konfigurovat hypertextové odkazy záhlaví sloupců pomocí příslušných hodnot řetězce dotazu:</span><span class="sxs-lookup"><span data-stu-id="fd343-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="fd343-131">Jedná se o Ternární příkazy.</span><span class="sxs-lookup"><span data-stu-id="fd343-131">These are ternary statements.</span></span> <span data-ttu-id="fd343-132">První z nich určuje, že pokud parametr `sortOrder` má hodnotu null nebo je prázdný, `ViewBag.NameSortParm` by měl být nastaven na "Name\_desc"; v opačném případě by měl být nastaven na prázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="fd343-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="fd343-133">Tyto dva příkazy umožňují zobrazení nastavit hypertextové odkazy záhlaví sloupce následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="fd343-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="fd343-134">Aktuální pořadí řazení</span><span class="sxs-lookup"><span data-stu-id="fd343-134">Current sort order</span></span> | <span data-ttu-id="fd343-135">Hypertextový odkaz na poslední jméno</span><span class="sxs-lookup"><span data-stu-id="fd343-135">Last Name Hyperlink</span></span> | <span data-ttu-id="fd343-136">Hypertextový odkaz na datum</span><span class="sxs-lookup"><span data-stu-id="fd343-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd343-137">Příjmení vzestupné</span><span class="sxs-lookup"><span data-stu-id="fd343-137">Last Name ascending</span></span> | <span data-ttu-id="fd343-138">descending</span><span class="sxs-lookup"><span data-stu-id="fd343-138">descending</span></span> | <span data-ttu-id="fd343-139">ascending</span><span class="sxs-lookup"><span data-stu-id="fd343-139">ascending</span></span> |
| <span data-ttu-id="fd343-140">Příjmení sestupně</span><span class="sxs-lookup"><span data-stu-id="fd343-140">Last Name descending</span></span> | <span data-ttu-id="fd343-141">ascending</span><span class="sxs-lookup"><span data-stu-id="fd343-141">ascending</span></span> | <span data-ttu-id="fd343-142">ascending</span><span class="sxs-lookup"><span data-stu-id="fd343-142">ascending</span></span> |
| <span data-ttu-id="fd343-143">Datum vzestupné</span><span class="sxs-lookup"><span data-stu-id="fd343-143">Date ascending</span></span> | <span data-ttu-id="fd343-144">ascending</span><span class="sxs-lookup"><span data-stu-id="fd343-144">ascending</span></span> | <span data-ttu-id="fd343-145">descending</span><span class="sxs-lookup"><span data-stu-id="fd343-145">descending</span></span> |
| <span data-ttu-id="fd343-146">Datum sestupné</span><span class="sxs-lookup"><span data-stu-id="fd343-146">Date descending</span></span> | <span data-ttu-id="fd343-147">ascending</span><span class="sxs-lookup"><span data-stu-id="fd343-147">ascending</span></span> | <span data-ttu-id="fd343-148">ascending</span><span class="sxs-lookup"><span data-stu-id="fd343-148">ascending</span></span> |

<span data-ttu-id="fd343-149">Metoda používá [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) k určení sloupce, podle kterého se má řadit.</span><span class="sxs-lookup"><span data-stu-id="fd343-149">The method uses [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) to specify the column to sort by.</span></span> <span data-ttu-id="fd343-150">Kód vytvoří <xref:System.Linq.IQueryable%601> proměnnou před příkazem `switch`, upraví ji v příkazu `switch` a zavolá metodu `ToList` po příkazu `switch`.</span><span class="sxs-lookup"><span data-stu-id="fd343-150">The code creates an <xref:System.Linq.IQueryable%601> variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="fd343-151">Při vytváření a úpravách `IQueryable` proměnných se do databáze neodesílají žádné dotazy.</span><span class="sxs-lookup"><span data-stu-id="fd343-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="fd343-152">Dotaz není proveden, dokud nepřevedete objekt `IQueryable` do kolekce voláním metody, jako je například `ToList`.</span><span class="sxs-lookup"><span data-stu-id="fd343-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="fd343-153">Proto tento kód má za následek jeden dotaz, který není proveden do příkazu `return View`.</span><span class="sxs-lookup"><span data-stu-id="fd343-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="fd343-154">Jako alternativu k psaní různých příkazů LINQ pro každé pořadí řazení můžete dynamicky vytvořit příkaz LINQ.</span><span class="sxs-lookup"><span data-stu-id="fd343-154">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="fd343-155">Informace o dynamickém LINQ naleznete v tématu [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span><span class="sxs-lookup"><span data-stu-id="fd343-155">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="fd343-156">Přidat hypertextové odkazy záhlaví sloupce do zobrazení indexu studenta</span><span class="sxs-lookup"><span data-stu-id="fd343-156">Add column heading hyperlinks to the Student index view</span></span>

1. <span data-ttu-id="fd343-157">V *Views\Student\Index.cshtml*nahraďte prvky `<tr>` a `<th>` pro řádek záhlaví zvýrazněným kódem:</span><span class="sxs-lookup"><span data-stu-id="fd343-157">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   <span data-ttu-id="fd343-158">Tento kód používá informace ve vlastnostech `ViewBag` k nastavení hypertextových odkazů s příslušnými hodnotami řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="fd343-158">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

2. <span data-ttu-id="fd343-159">Spusťte stránku a kliknutím na záhlaví sloupce **Poslední název** a **Datum registrace** ověřte, že řazení funguje.</span><span class="sxs-lookup"><span data-stu-id="fd343-159">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

   <span data-ttu-id="fd343-160">Po kliknutí na záhlaví **příjmení** se studenty zobrazí v sestupném pořadí příjmení.</span><span class="sxs-lookup"><span data-stu-id="fd343-160">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

## <a name="add-a-search-box"></a><span data-ttu-id="fd343-161">Přidání vyhledávacího pole</span><span class="sxs-lookup"><span data-stu-id="fd343-161">Add a Search box</span></span>

<span data-ttu-id="fd343-162">Chcete-li přidat filtrování na stránku indexu studentů, přidejte do zobrazení textové pole a tlačítko Odeslat a proveďte odpovídající změny v `Index` metodě.</span><span class="sxs-lookup"><span data-stu-id="fd343-162">To add filtering to the Students index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="fd343-163">Textové pole umožňuje zadat řetězec, který chcete vyhledat v polích jméno a příjmení.</span><span class="sxs-lookup"><span data-stu-id="fd343-163">The text box lets you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="fd343-164">Přidání funkce filtrování do metody index</span><span class="sxs-lookup"><span data-stu-id="fd343-164">Add filtering functionality to the Index method</span></span>

- <span data-ttu-id="fd343-165">V *Controllers\StudentController.cs*nahraďte metodu `Index` následujícím kódem (změny jsou zvýrazněny):</span><span class="sxs-lookup"><span data-stu-id="fd343-165">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="fd343-166">Kód přidá parametr `searchString` do metody `Index`.</span><span class="sxs-lookup"><span data-stu-id="fd343-166">The code adds a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="fd343-167">Hodnota vyhledávacího řetězce je přijímána z textového pole, které přidáte do zobrazení index.</span><span class="sxs-lookup"><span data-stu-id="fd343-167">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="fd343-168">Přidá také klauzuli `where` do příkazu LINQ, který vybere pouze studenty, jejichž křestní jméno nebo příjmení obsahuje hledaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="fd343-168">It also adds a `where` clause to the LINQ statement that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="fd343-169">Příkaz, který přidá klauzuli <xref:System.Linq.Queryable.Where%2A>, se spustí pouze v případě, že existuje hodnota, která se má vyhledat.</span><span class="sxs-lookup"><span data-stu-id="fd343-169">The statement that adds the <xref:System.Linq.Queryable.Where%2A> clause executes only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="fd343-170">V mnoha případech můžete zavolat stejnou metodu buď na Entity Framework sadu entit nebo jako metodu rozšíření v kolekci v paměti.</span><span class="sxs-lookup"><span data-stu-id="fd343-170">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="fd343-171">Výsledky jsou normálně stejné, ale v některých případech se mohou lišit.</span><span class="sxs-lookup"><span data-stu-id="fd343-171">The results are normally the same but in some cases may be different.</span></span>
>
> <span data-ttu-id="fd343-172">Například .NET Framework implementace metody `Contains` vrátí všechny řádky, když do ní předáte prázdný řetězec, ale zprostředkovatel Entity Framework pro SQL Server Compact 4,0 vrátí nulové řádky pro prázdné řetězce.</span><span class="sxs-lookup"><span data-stu-id="fd343-172">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="fd343-173">Proto kód v příkladu (vložení příkazu `Where` do příkazu `if`) zajistí, že získáte stejné výsledky pro všechny verze SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fd343-173">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="fd343-174">Kromě toho .NET Framework implementace `Contains` metody ve výchozím nastavení provádí porovnávání s rozlišováním velkých a malých písmen, Entity Framework ale zprostředkovatelé SQL Server ve výchozím nastavení nerozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="fd343-174">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="fd343-175">Proto voláním metody `ToUpper` pro zajištění, že test explicitně nerozlišuje velká a malá písmena, zajistí, že se výsledky nezmění při pozdějším změně kódu pro použití úložiště, které vrátí kolekci `IEnumerable` namísto objektu `IQueryable`.</span><span class="sxs-lookup"><span data-stu-id="fd343-175">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="fd343-176">(Při volání metody `Contains` v kolekci `IEnumerable`, získáte .NET Framework implementaci. Pokud ji voláte na `IQueryable` objekt, získáte implementaci poskytovatele databáze.)</span><span class="sxs-lookup"><span data-stu-id="fd343-176">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
>
> <span data-ttu-id="fd343-177">Zpracování hodnot null se může také lišit pro různé poskytovatele databáze nebo při použití objektu `IQueryable` v porovnání s použitím kolekce `IEnumerable`.</span><span class="sxs-lookup"><span data-stu-id="fd343-177">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="fd343-178">V některých scénářích například `Where` podmínka, například `table.Column != 0`, nesmí vracet sloupce, které mají `null` jako hodnotu.</span><span class="sxs-lookup"><span data-stu-id="fd343-178">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="fd343-179">Ve výchozím nastavení EF generuje další operátory SQL pro zajištění rovnosti mezi hodnotami null v databázi funguje stejně jako v paměti, ale můžete nastavit příznak [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) v EF6 nebo volat metodu [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) v EF Core pro konfiguraci tohoto chování.</span><span class="sxs-lookup"><span data-stu-id="fd343-179">By default, EF generates additional SQL operators to make equality between null values work in the database like it works in memory, but you can set the [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) flag in EF6 or call the [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) method in EF Core to configure this behavior.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="fd343-180">Přidání vyhledávacího pole do zobrazení indexu studenta</span><span class="sxs-lookup"><span data-stu-id="fd343-180">Add a search box to the Student index view</span></span>

1. <span data-ttu-id="fd343-181">V *Views\Student\Index.cshtml*přidejte zvýrazněný kód těsně před otevírací značku `table`, aby se vytvořil titulek, textové pole a tlačítko **hledání** .</span><span class="sxs-lookup"><span data-stu-id="fd343-181">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. <span data-ttu-id="fd343-182">Spusťte stránku, zadejte hledaný řetězec a kliknutím na tlačítko **Hledat** ověřte, zda filtrování funguje.</span><span class="sxs-lookup"><span data-stu-id="fd343-182">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

   <span data-ttu-id="fd343-183">Všimněte si, že adresa URL neobsahuje hledaný řetězec "a", což znamená, že pokud tuto stránku zařadíte do záložky, nezobrazí se při použití záložky filtrovaný seznam.</span><span class="sxs-lookup"><span data-stu-id="fd343-183">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="fd343-184">To platí také pro odkazy na řazení sloupců, protože budou řadit celý seznam.</span><span class="sxs-lookup"><span data-stu-id="fd343-184">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="fd343-185">Později v tomto kurzu změníte tlačítko **hledání** na použití řetězců dotazů pro kritéria filtru.</span><span class="sxs-lookup"><span data-stu-id="fd343-185">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging"></a><span data-ttu-id="fd343-186">Přidat stránkování</span><span class="sxs-lookup"><span data-stu-id="fd343-186">Add paging</span></span>

<span data-ttu-id="fd343-187">Pokud chcete přidat stránkování na stránku indexu studentů, začněte tím, že nainstalujete balíček NuGet **PagedList. Mvc** .</span><span class="sxs-lookup"><span data-stu-id="fd343-187">To add paging to the Students index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="fd343-188">Pak provedete další změny v metodě `Index` a přidáte odkazy na stránkování do zobrazení `Index`.</span><span class="sxs-lookup"><span data-stu-id="fd343-188">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="fd343-189">**PagedList. Mvc** je jedním z mnoha dobrých balíčků pro stránkování a seřazení pro ASP.NET MVC a její použití je určeno pouze jako příklad, nikoli jako doporučení pro jiné možnosti.</span><span class="sxs-lookup"><span data-stu-id="fd343-189">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span>

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="fd343-190">Instalace balíčku NuGet PagedList. MVC</span><span class="sxs-lookup"><span data-stu-id="fd343-190">Install the PagedList.MVC NuGet package</span></span>

<span data-ttu-id="fd343-191">Balíček NuGet **PagedList. Mvc** automaticky nainstaluje balíček **PagedList** jako závislost.</span><span class="sxs-lookup"><span data-stu-id="fd343-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="fd343-192">Balíček **PagedList** nainstaluje typ kolekce `PagedList` a metody rozšíření pro kolekce `IQueryable` a `IEnumerable`.</span><span class="sxs-lookup"><span data-stu-id="fd343-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="fd343-193">Metody rozšíření vytvářejí v kolekci `PagedList` jednu stránku dat mimo `IQueryable` nebo `IEnumerable`a kolekce `PagedList` poskytuje několik vlastností a metod, které usnadňují stránkování.</span><span class="sxs-lookup"><span data-stu-id="fd343-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="fd343-194">Balíček **PagedList. Mvc** nainstaluje pomocný objekt pro stránkování, který zobrazí tlačítka stránkování.</span><span class="sxs-lookup"><span data-stu-id="fd343-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

1. <span data-ttu-id="fd343-195">V nabídce **nástroje** vyberte **Správce balíčků NuGet** a pak **konzolu Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="fd343-195">From the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span></span>

2. <span data-ttu-id="fd343-196">V okně **konzoly Správce balíčků** se ujistěte, že je **zdroj balíčku** **NuGet.org** a **výchozí projekt** je **ContosoUniversity**, a potom zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fd343-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

   ```text
   Install-Package PagedList.Mvc
   ```

3. <span data-ttu-id="fd343-197">Sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="fd343-197">Build the project.</span></span>

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="fd343-198">Přidání funkce stránkování do metody index</span><span class="sxs-lookup"><span data-stu-id="fd343-198">Add paging functionality to the Index method</span></span>

1. <span data-ttu-id="fd343-199">Do *Controllers\StudentController.cs*přidejte příkaz `using` pro obor názvů `PagedList`:</span><span class="sxs-lookup"><span data-stu-id="fd343-199">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. <span data-ttu-id="fd343-200">Nahraďte metodu `Index` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="fd343-200">Replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   <span data-ttu-id="fd343-201">Tento kód přidá parametr `page`, aktuální parametr pořadí řazení a aktuální parametr filtru na signaturu metody:</span><span class="sxs-lookup"><span data-stu-id="fd343-201">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="fd343-202">Při prvním zobrazení stránky, nebo pokud uživatel neklikl na odkaz na stránkování nebo řazení, mají všechny parametry hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="fd343-202">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters are null.</span></span> <span data-ttu-id="fd343-203">Pokud se klikne na odkaz na stránkování, `page` proměnná obsahuje číslo stránky k zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fd343-203">If a paging link is clicked, the `page` variable contains the page number to display.</span></span>

   <span data-ttu-id="fd343-204">Vlastnost `ViewBag` poskytuje zobrazení s aktuálním pořadím řazení, protože musí být součástí odkazů stránkování, aby při stránkování zůstalo stejné pořadí řazení:</span><span class="sxs-lookup"><span data-stu-id="fd343-204">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   <span data-ttu-id="fd343-205">Jiná vlastnost, `ViewBag.CurrentFilter`, poskytuje zobrazení s aktuálním řetězcem filtru.</span><span class="sxs-lookup"><span data-stu-id="fd343-205">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="fd343-206">Tato hodnota musí být součástí odkazů stránkování, aby bylo možné zachovat nastavení filtru během stránkování, a při zobrazení stránky musí být obnovena do textového pole.</span><span class="sxs-lookup"><span data-stu-id="fd343-206">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="fd343-207">Pokud se hledaný řetězec během stránkování změní, je nutné obnovit stránku na 1, protože nový filtr může mít za následek zobrazení různých dat.</span><span class="sxs-lookup"><span data-stu-id="fd343-207">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="fd343-208">Hledaný řetězec se změní, když je v textovém poli vložena hodnota a stisknete tlačítko Odeslat.</span><span class="sxs-lookup"><span data-stu-id="fd343-208">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="fd343-209">V takovém případě parametr `searchString` nemá hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="fd343-209">In that case, the `searchString` parameter is not null.</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   <span data-ttu-id="fd343-210">Na konci metody `ToPagedList` metoda rozšíření na `IQueryable` objekt Students převede dotaz studenta na jednu stránku studentů v typu kolekce, který podporuje stránkování.</span><span class="sxs-lookup"><span data-stu-id="fd343-210">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="fd343-211">Tato jediná strana studentů se pak předává do zobrazení:</span><span class="sxs-lookup"><span data-stu-id="fd343-211">That single page of students is then passed to the view:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   <span data-ttu-id="fd343-212">Metoda `ToPagedList` přebírá číslo stránky.</span><span class="sxs-lookup"><span data-stu-id="fd343-212">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="fd343-213">Dvě otazníky reprezentují [operátor slučování s hodnotou null](/dotnet/csharp/language-reference/operators/null-coalescing-operator).</span><span class="sxs-lookup"><span data-stu-id="fd343-213">The two question marks represent the [null-coalescing operator](/dotnet/csharp/language-reference/operators/null-coalescing-operator).</span></span> <span data-ttu-id="fd343-214">Operátor slučování null definuje výchozí hodnotu pro typ s možnou hodnotou null. výraz `(page ?? 1)` znamená vrátit hodnotu `page`, pokud má hodnotu, nebo vrátí hodnotu 1, pokud `page` má hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="fd343-214">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="fd343-215">Přidat odkazy na stránkování do zobrazení indexu studenta</span><span class="sxs-lookup"><span data-stu-id="fd343-215">Add paging links to the Student index view</span></span>

1. <span data-ttu-id="fd343-216">V *Views\Student\Index.cshtml*nahraďte existující kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="fd343-216">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="fd343-217">Změny jsou zvýrazněné.</span><span class="sxs-lookup"><span data-stu-id="fd343-217">The changes are highlighted.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   <span data-ttu-id="fd343-218">Příkaz `@model` v horní části stránky určuje, že zobrazení nyní Získá objekt `PagedList` namísto objektu `List`.</span><span class="sxs-lookup"><span data-stu-id="fd343-218">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

   <span data-ttu-id="fd343-219">Příkaz `using` pro `PagedList.Mvc` poskytuje přístup k Pomocníkovi MVC pro tlačítka stránkování.</span><span class="sxs-lookup"><span data-stu-id="fd343-219">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

   <span data-ttu-id="fd343-220">Kód používá přetížení [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) , které umožňuje určit [FormMethod. Get](/previous-versions/aspnet/dd460179(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="fd343-220">The code uses an overload of [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) that allows it to specify [FormMethod.Get](/previous-versions/aspnet/dd460179(v=vs.100)).</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   <span data-ttu-id="fd343-221">Výchozí [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) odesílá data formuláře pomocí příspěvku, což znamená, že parametry jsou předány v těle zprávy HTTP a nejsou v adrese URL jako řetězce dotazů.</span><span class="sxs-lookup"><span data-stu-id="fd343-221">The default [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="fd343-222">Když zadáte příkaz HTTP GET, data formuláře se předávají v adrese URL jako řetězce dotazů, které uživatelům umožňují záložku URL.</span><span class="sxs-lookup"><span data-stu-id="fd343-222">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="fd343-223">[Pokyny pro konsorcium W3C pro použití http vám](http://www.w3.org/2001/tag/doc/whenToUseGet.html) doporučují použít Get, když akce nevede k aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="fd343-223">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

   <span data-ttu-id="fd343-224">Textové pole se inicializuje s aktuálním hledaným řetězcem, takže když kliknete na novou stránku, můžete zobrazit aktuální hledaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="fd343-224">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   <span data-ttu-id="fd343-225">Záhlaví sloupce odkazuje pomocí řetězce dotazu k předání aktuálního vyhledávacího řetězce k řadiči, aby uživatel mohl seřadit výsledky filtru:</span><span class="sxs-lookup"><span data-stu-id="fd343-225">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   <span data-ttu-id="fd343-226">Zobrazí se aktuální stránka a celkový počet stránek.</span><span class="sxs-lookup"><span data-stu-id="fd343-226">The current page and total number of pages are displayed.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   <span data-ttu-id="fd343-227">Pokud neexistují žádné stránky k zobrazení, zobrazí se hodnota "stránka 0 0".</span><span class="sxs-lookup"><span data-stu-id="fd343-227">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="fd343-228">(V takovém případě je číslo stránky větší než počet stránek, protože `Model.PageNumber` 1 a `Model.PageCount` je 0.)</span><span class="sxs-lookup"><span data-stu-id="fd343-228">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

   <span data-ttu-id="fd343-229">Tlačítka stránkování jsou zobrazena pomocí pomocníka `PagedListPager`:</span><span class="sxs-lookup"><span data-stu-id="fd343-229">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   <span data-ttu-id="fd343-230">Pomocná aplikace `PagedListPager` poskytuje řadu možností, které můžete přizpůsobit, včetně adres URL a stylů.</span><span class="sxs-lookup"><span data-stu-id="fd343-230">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="fd343-231">Další informace najdete v tématu [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) na webu GitHubu.</span><span class="sxs-lookup"><span data-stu-id="fd343-231">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

2. <span data-ttu-id="fd343-232">Spusťte stránku.</span><span class="sxs-lookup"><span data-stu-id="fd343-232">Run the page.</span></span>

   <span data-ttu-id="fd343-233">Kliknutím na odkazy na stránkování v různých pořadích řazení zajistěte, aby stránkování fungovalo.</span><span class="sxs-lookup"><span data-stu-id="fd343-233">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="fd343-234">Pak zadejte hledaný řetězec a zkuste znovu vytvořit stránkování, abyste ověřili, že stránkování funguje i správně s řazením a filtrováním.</span><span class="sxs-lookup"><span data-stu-id="fd343-234">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page"></a><span data-ttu-id="fd343-235">Vytvoření stránky o stránku</span><span class="sxs-lookup"><span data-stu-id="fd343-235">Create an About page</span></span>

<span data-ttu-id="fd343-236">Pro stránku se stránkou společnosti Contoso na univerzitě se zobrazí, kolik studentů se zaregistrovalo pro každé datum registrace.</span><span class="sxs-lookup"><span data-stu-id="fd343-236">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="fd343-237">To vyžaduje seskupování a jednoduché výpočty skupin.</span><span class="sxs-lookup"><span data-stu-id="fd343-237">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="fd343-238">K tomu je třeba provést následující akce:</span><span class="sxs-lookup"><span data-stu-id="fd343-238">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="fd343-239">Vytvořte třídu zobrazení modelu pro data, která potřebujete předat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fd343-239">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="fd343-240">V kontroleru `Home` upravte metodu `About`.</span><span class="sxs-lookup"><span data-stu-id="fd343-240">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="fd343-241">Upravte zobrazení `About`.</span><span class="sxs-lookup"><span data-stu-id="fd343-241">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="fd343-242">Vytvoření modelu zobrazení</span><span class="sxs-lookup"><span data-stu-id="fd343-242">Create the View Model</span></span>

<span data-ttu-id="fd343-243">Vytvořte složku *ViewModels* ve složce projektu.</span><span class="sxs-lookup"><span data-stu-id="fd343-243">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="fd343-244">V této složce přidejte soubor třídy *EnrollmentDateGroup.cs* a nahraďte kód šablony následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="fd343-244">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="fd343-245">Úprava domovského kontroleru</span><span class="sxs-lookup"><span data-stu-id="fd343-245">Modify the Home Controller</span></span>

1. <span data-ttu-id="fd343-246">V *HomeController.cs*přidejte na začátek souboru následující příkazy `using`:</span><span class="sxs-lookup"><span data-stu-id="fd343-246">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. <span data-ttu-id="fd343-247">Přidejte proměnnou třídy pro kontext databáze hned za levou složenou závorku pro třídu:</span><span class="sxs-lookup"><span data-stu-id="fd343-247">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. <span data-ttu-id="fd343-248">Nahraďte metodu `About` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="fd343-248">Replace the `About` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   <span data-ttu-id="fd343-249">Příkaz LINQ seskupuje entity studenta podle data registrace, vypočítá počet entit v každé skupině a ukládá výsledky do kolekce `EnrollmentDateGroup` objektů modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fd343-249">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

4. <span data-ttu-id="fd343-250">Přidejte `Dispose` metodu:</span><span class="sxs-lookup"><span data-stu-id="fd343-250">Add a `Dispose` method:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="fd343-251">Úprava zobrazení o produktu</span><span class="sxs-lookup"><span data-stu-id="fd343-251">Modify the About View</span></span>

1. <span data-ttu-id="fd343-252">Nahraďte kód v souboru *Views\Home\About.cshtml* následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="fd343-252">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. <span data-ttu-id="fd343-253">Spusťte aplikaci a klikněte na odkaz **informace** .</span><span class="sxs-lookup"><span data-stu-id="fd343-253">Run the app and click the **About** link.</span></span>

   <span data-ttu-id="fd343-254">Počet studentů pro každé datum registrace se zobrazí v tabulce.</span><span class="sxs-lookup"><span data-stu-id="fd343-254">The count of students for each enrollment date displays in a table.</span></span>

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a><span data-ttu-id="fd343-256">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="fd343-256">Get the code</span></span>

[<span data-ttu-id="fd343-257">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="fd343-257">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="fd343-258">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="fd343-258">Additional resources</span></span>

<span data-ttu-id="fd343-259">Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="fd343-259">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd343-260">Další kroky</span><span class="sxs-lookup"><span data-stu-id="fd343-260">Next steps</span></span>

<span data-ttu-id="fd343-261">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="fd343-261">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fd343-262">Přidat odkazy na řazení sloupců</span><span class="sxs-lookup"><span data-stu-id="fd343-262">Add column sort links</span></span>
> * <span data-ttu-id="fd343-263">Přidání vyhledávacího pole</span><span class="sxs-lookup"><span data-stu-id="fd343-263">Add a Search box</span></span>
> * <span data-ttu-id="fd343-264">Přidat stránkování</span><span class="sxs-lookup"><span data-stu-id="fd343-264">Add paging</span></span>
> * <span data-ttu-id="fd343-265">Vytvoření stránky o stránku</span><span class="sxs-lookup"><span data-stu-id="fd343-265">Create an About page</span></span>

<span data-ttu-id="fd343-266">Přejděte k dalšímu článku, kde se dozvíte, jak používat odolnost připojení a zachycení příkazů.</span><span class="sxs-lookup"><span data-stu-id="fd343-266">Advance to the next article to learn how to use connection resiliency and command interception.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fd343-267">Odolnost připojení a zachycení příkazu</span><span class="sxs-lookup"><span data-stu-id="fd343-267">Connection resiliency and command interception</span></span>](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
