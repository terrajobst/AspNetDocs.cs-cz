---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: použití asynchronních a uložených procedur s EF v aplikaci ASP.NET MVC'
description: V tomto kurzu vidíte, jak implementovat asynchronní programovací model a Naučte se používat uložené procedury.
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583438"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="381b3-103">Kurz: použití asynchronních a uložených procedur s EF v aplikaci ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="381b3-103">Tutorial: Use async and stored procedures with EF in an ASP.NET MVC App</span></span>

<span data-ttu-id="381b3-104">V předchozích kurzech jste zjistili, jak číst a aktualizovat data pomocí synchronního programovacího modelu.</span><span class="sxs-lookup"><span data-stu-id="381b3-104">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="381b3-105">V tomto kurzu vidíte, jak implementovat asynchronní programovací model.</span><span class="sxs-lookup"><span data-stu-id="381b3-105">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="381b3-106">Asynchronní kód může zajistit lepší výkon aplikace, protože zajišťuje lepší využití prostředků serveru.</span><span class="sxs-lookup"><span data-stu-id="381b3-106">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="381b3-107">V tomto kurzu zjistíte také, jak používat uložené procedury pro operace vložení, aktualizace a odstranění u entity.</span><span class="sxs-lookup"><span data-stu-id="381b3-107">In this tutorial you also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="381b3-108">Nakonec aplikaci znovu nasadíte do Azure spolu se všemi změnami databáze, které jste implementovali od prvního nasazení.</span><span class="sxs-lookup"><span data-stu-id="381b3-108">Finally, you redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="381b3-109">Následující ilustrace znázorňují některé stránky, se kterými budete pracovat.</span><span class="sxs-lookup"><span data-stu-id="381b3-109">The following illustrations show some of the pages that you'll work with.</span></span>

![Stránka oddělení](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Vytvořit oddělení](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="381b3-112">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="381b3-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="381b3-113">Informace o asynchronním kódu</span><span class="sxs-lookup"><span data-stu-id="381b3-113">Learn about asynchronous code</span></span>
> * <span data-ttu-id="381b3-114">Vytvoření řadiče oddělení</span><span class="sxs-lookup"><span data-stu-id="381b3-114">Create a Department controller</span></span>
> * <span data-ttu-id="381b3-115">Použití uložených procedur</span><span class="sxs-lookup"><span data-stu-id="381b3-115">Use stored procedures</span></span>
> * <span data-ttu-id="381b3-116">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="381b3-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="381b3-117">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="381b3-117">Prerequisites</span></span>

* [<span data-ttu-id="381b3-118">Aktualizace souvisejících dat</span><span class="sxs-lookup"><span data-stu-id="381b3-118">Updating Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a><span data-ttu-id="381b3-119">Proč použít asynchronní kód</span><span class="sxs-lookup"><span data-stu-id="381b3-119">Why use asynchronous code</span></span>

<span data-ttu-id="381b3-120">Webový server má omezený počet vláken, které jsou k dispozici, a v situacích, vysokého zatížení všech dostupných vláken může být používán.</span><span class="sxs-lookup"><span data-stu-id="381b3-120">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="381b3-121">Pokud k tomu dojde, server nemůže zpracovat nové žádosti, dokud se uvolnit vlákna.</span><span class="sxs-lookup"><span data-stu-id="381b3-121">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="381b3-122">Přestože se nejedná skutečně každé dílo vzhledem k tomu, že čekání na vstupně-výstupních operací na dokončení, může kódem synchronní svázané několika vlákny.</span><span class="sxs-lookup"><span data-stu-id="381b3-122">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="381b3-123">Asynchronní kód když proces čeká na vstupně-výstupních operací na dokončení, je jeho vlákno uvolněn pro server určený pro zpracováním jiných požadavků.</span><span class="sxs-lookup"><span data-stu-id="381b3-123">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="381b3-124">Výsledkem je, že asynchronní kód umožňuje efektivnější využití prostředků serveru a server je povolen pro zpracování většího objemu dat bez prodlev.</span><span class="sxs-lookup"><span data-stu-id="381b3-124">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="381b3-125">V dřívějších verzích rozhraní .NET byla psaní a testování asynchronního kódu složitá, náchylná k chybám a obtížné ladění.</span><span class="sxs-lookup"><span data-stu-id="381b3-125">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="381b3-126">V rozhraní .NET 4,5, psaní, testování a ladění asynchronního kódu je mnohem jednodušší, že byste měli obecně zapisovat asynchronní kód, pokud nemáte důvod na.</span><span class="sxs-lookup"><span data-stu-id="381b3-126">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="381b3-127">Asynchronní kód zavádí malé množství režijních nákladů, ale u situací s nízkým objemem provozu je dosaženo zanedbatelného výkonu, zatímco v případě vysoké situace v provozu je potenciální zlepšení výkonu značné.</span><span class="sxs-lookup"><span data-stu-id="381b3-127">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="381b3-128">Další informace o asynchronním programování naleznete v tématu [použití asynchronní podpory rozhraní .NET 4.5 k zamezení blokování volání](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span><span class="sxs-lookup"><span data-stu-id="381b3-128">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-department-controller"></a><span data-ttu-id="381b3-129">Vytvořit kontroler oddělení</span><span class="sxs-lookup"><span data-stu-id="381b3-129">Create Department controller</span></span>

<span data-ttu-id="381b3-130">Vytvoření řadiče oddělení stejným způsobem jako u předchozích řadičů, s výjimkou tohoto času zaškrtněte políčko **použít asynchronní akce kontroleru** .</span><span class="sxs-lookup"><span data-stu-id="381b3-130">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller actions** check box.</span></span>

<span data-ttu-id="381b3-131">Následující zajímavá místa ukazují, co bylo přidáno do synchronního kódu pro metodu `Index` pro zajištění asynchronního:</span><span class="sxs-lookup"><span data-stu-id="381b3-131">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="381b3-132">Byly provedeny čtyři změny, aby bylo možné Entity Framework dotaz databáze spustit asynchronně:</span><span class="sxs-lookup"><span data-stu-id="381b3-132">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="381b3-133">Metoda je označena pomocí klíčového slova `async`, která dává kompilátoru pokyn ke generování zpětných volání pro části těla metody a k automatickému vytvoření vráceného objektu `Task<ActionResult>`.</span><span class="sxs-lookup"><span data-stu-id="381b3-133">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="381b3-134">Návratový typ se změnil z `ActionResult` na `Task<ActionResult>`.</span><span class="sxs-lookup"><span data-stu-id="381b3-134">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="381b3-135">Typ `Task<T>` představuje průběžnou práci s výsledkem typu `T`.</span><span class="sxs-lookup"><span data-stu-id="381b3-135">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="381b3-136">Klíčové slovo `await` bylo použito pro volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="381b3-136">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="381b3-137">Když kompilátor uvidí toto klíčové slovo, pak na pozadí rozdělí metodu do dvou částí.</span><span class="sxs-lookup"><span data-stu-id="381b3-137">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="381b3-138">První část končí operací, která se spouští asynchronně.</span><span class="sxs-lookup"><span data-stu-id="381b3-138">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="381b3-139">Druhá část je vložena do metody zpětného volání, která je volána po dokončení operace.</span><span class="sxs-lookup"><span data-stu-id="381b3-139">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="381b3-140">Byla volána asynchronní verze metody rozšíření `ToList`.</span><span class="sxs-lookup"><span data-stu-id="381b3-140">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="381b3-141">Proč se příkaz `departments.ToList` změnil, ale ne příkaz `departments = db.Departments`?</span><span class="sxs-lookup"><span data-stu-id="381b3-141">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="381b3-142">Důvodem je, že se spustí asynchronně pouze příkazy, které způsobují odeslání dotazů nebo příkazů do databáze.</span><span class="sxs-lookup"><span data-stu-id="381b3-142">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="381b3-143">Příkaz `departments = db.Departments` nastaví dotaz, ale dotaz není proveden, dokud není volána metoda `ToList`.</span><span class="sxs-lookup"><span data-stu-id="381b3-143">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="381b3-144">Proto je provedena asynchronně pouze metoda `ToList`.</span><span class="sxs-lookup"><span data-stu-id="381b3-144">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="381b3-145">V metodě `Details` a metodách `Edit` `HttpGet` a `Delete` je metoda `Find` ta, která způsobí odeslání dotazu do databáze, takže se jedná o metodu, která se provede asynchronně:</span><span class="sxs-lookup"><span data-stu-id="381b3-145">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="381b3-146">V metodách `Create`, `HttpPost Edit`a `DeleteConfirmed` je to volání metody `SaveChanges`, které způsobuje provedení příkazu, nikoli příkazy, jako je například `db.Departments.Add(department)`, které způsobují úpravu pouze entit v paměti.</span><span class="sxs-lookup"><span data-stu-id="381b3-146">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="381b3-147">Otevřete *Views\Department\Index.cshtml*a nahraďte kód šablony následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="381b3-147">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="381b3-148">Tento kód změní název z indexu na oddělení, přesune jméno správce napravo a poskytne celé jméno správce.</span><span class="sxs-lookup"><span data-stu-id="381b3-148">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="381b3-149">V zobrazeních vytvořit, odstranit, podrobnosti a upravit změňte Titulek pole `InstructorID` na "správce" stejným způsobem, jako jste změnili pole název oddělení na "oddělení" v zobrazení kurzu.</span><span class="sxs-lookup"><span data-stu-id="381b3-149">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="381b3-150">V zobrazeních vytvořit a upravit použijte následující kód:</span><span class="sxs-lookup"><span data-stu-id="381b3-150">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="381b3-151">V zobrazeních odstranění a podrobnosti použijte následující kód:</span><span class="sxs-lookup"><span data-stu-id="381b3-151">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="381b3-152">Spusťte aplikaci a klikněte na kartu **oddělení** .</span><span class="sxs-lookup"><span data-stu-id="381b3-152">Run the application, and click the **Departments** tab.</span></span>

<span data-ttu-id="381b3-153">Vše funguje stejně jako v ostatních řadičích, ale v tomto kontroleru jsou všechny dotazy SQL spouštěny asynchronně.</span><span class="sxs-lookup"><span data-stu-id="381b3-153">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="381b3-154">Některé věci, které je potřeba znát při použití asynchronního programování s Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="381b3-154">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="381b3-155">Asynchronní kód není bezpečný pro přístup z více vláken.</span><span class="sxs-lookup"><span data-stu-id="381b3-155">The async code is not thread safe.</span></span> <span data-ttu-id="381b3-156">Jinými slovy, jinými slovy, nepokoušejte se souběžně provádět více operací pomocí stejné instance kontextu.</span><span class="sxs-lookup"><span data-stu-id="381b3-156">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="381b3-157">Chcete-li využít výhod výkonu asynchronního kódu, zajistěte, aby všechny balíčky knihovny, které používáte (například pro stránkování), používaly také Async, pokud volají jakékoli Entity Framework metody, které způsobují odesílání dotazů do databáze.</span><span class="sxs-lookup"><span data-stu-id="381b3-157">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures"></a><span data-ttu-id="381b3-158">Použití uložených procedur</span><span class="sxs-lookup"><span data-stu-id="381b3-158">Use stored procedures</span></span>

<span data-ttu-id="381b3-159">Někteří vývojáři a specializující upřednostňují použití uložených procedur pro přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="381b3-159">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="381b3-160">V dřívějších verzích Entity Framework můžete načíst data pomocí uložené procedury spuštěním [nezpracovaného dotazu SQL](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), ale nemůžete dát pokyn EF k použití uložených procedur pro operace aktualizace.</span><span class="sxs-lookup"><span data-stu-id="381b3-160">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="381b3-161">V EF 6 je snadné nakonfigurovat Code First pro použití uložených procedur.</span><span class="sxs-lookup"><span data-stu-id="381b3-161">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="381b3-162">Do *DAL\SchoolContext.cs*přidejte zvýrazněný kód do metody `OnModelCreating`.</span><span class="sxs-lookup"><span data-stu-id="381b3-162">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="381b3-163">Tento kód instruuje Entity Framework pro použití uložených procedur pro operace vložení, aktualizace a odstranění v entitě `Department`.</span><span class="sxs-lookup"><span data-stu-id="381b3-163">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="381b3-164">V konzole pro správu balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="381b3-164">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="381b3-165">Otevřete *migrace\\&lt;časové razítko&gt;\_DepartmentSP.cs* a zobrazte kód v metodě `Up`, která vytvoří uložené procedury INSERT, Update a Delete:</span><span class="sxs-lookup"><span data-stu-id="381b3-165">Open *Migrations\\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="381b3-166">V konzole pro správu balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="381b3-166">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="381b3-167">Spusťte aplikaci v režimu ladění, klikněte na kartu **oddělení** a pak klikněte na **vytvořit novou**.</span><span class="sxs-lookup"><span data-stu-id="381b3-167">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="381b3-168">Zadejte data nového oddělení a pak klikněte na **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="381b3-168">Enter data for a new department, and then click **Create**.</span></span>

6. <span data-ttu-id="381b3-169">V aplikaci Visual Studio se podívejte na protokoly v okně **výstup** , abyste viděli, že se k vložení nového řádku oddělení použila uložená procedura.</span><span class="sxs-lookup"><span data-stu-id="381b3-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![Vložení oddělení SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="381b3-171">Code First vytvoří výchozí názvy uložených procedur.</span><span class="sxs-lookup"><span data-stu-id="381b3-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="381b3-172">Pokud používáte existující databázi, může být nutné přizpůsobit názvy uložených procedur, aby bylo možné použít uložené procedury, které jsou již v databázi definovány.</span><span class="sxs-lookup"><span data-stu-id="381b3-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="381b3-173">Další informace o tom, jak to provést, najdete v tématu [Entity Framework Code First vkládání, aktualizace a odstraňování uložených procedur](https://msdn.microsoft.com/data/dn468673).</span><span class="sxs-lookup"><span data-stu-id="381b3-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="381b3-174">Chcete-li upravit, které generované uložené procedury mají, můžete upravit generovaný kód pro migraci `Up` metodu, která vytvoří uloženou proceduru.</span><span class="sxs-lookup"><span data-stu-id="381b3-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="381b3-175">To znamená, že se vaše změny projeví při spuštění migrace a budou se používat v provozní databázi, když se migrace po nasazení spustí automaticky v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="381b3-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="381b3-176">Pokud chcete změnit existující uloženou proceduru, která byla vytvořena v předchozí migraci, můžete k vygenerování prázdné migrace použít příkaz Add-Migration a pak ručně napsat kód, který volá metodu [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) .</span><span class="sxs-lookup"><span data-stu-id="381b3-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="381b3-177">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="381b3-177">Deploy to Azure</span></span>

<span data-ttu-id="381b3-178">Tato část vyžaduje, abyste v kurzu [migrace a nasazení](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) této série dokončili oddíl volitelné **nasazení aplikace do Azure** .</span><span class="sxs-lookup"><span data-stu-id="381b3-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="381b3-179">Pokud jste převedli chyby, které jste vyřešili odstraněním databáze v místním projektu, přeskočte tuto část.</span><span class="sxs-lookup"><span data-stu-id="381b3-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="381b3-180">V aplikaci Visual Studio klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a v místní nabídce vyberte **publikovat** .</span><span class="sxs-lookup"><span data-stu-id="381b3-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="381b3-181">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="381b3-181">Click **Publish**.</span></span>

    <span data-ttu-id="381b3-182">Visual Studio nasadí aplikaci do Azure a aplikace se otevře ve výchozím prohlížeči spuštěném v Azure.</span><span class="sxs-lookup"><span data-stu-id="381b3-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="381b3-183">Otestujte aplikaci, abyste ověřili, že funguje.</span><span class="sxs-lookup"><span data-stu-id="381b3-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="381b3-184">Při prvním spuštění stránky, která přistupuje k databázi, Entity Framework spustí všechny migrace `Up` metody potřebné k zajištění aktuálnosti databáze s aktuálním datovým modelem.</span><span class="sxs-lookup"><span data-stu-id="381b3-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="381b3-185">Nyní můžete použít všechny webové stránky, které jste přidali od posledního nasazení, včetně stránek oddělení, které jste přidali v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="381b3-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="381b3-186">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="381b3-186">Get the code</span></span>

[<span data-ttu-id="381b3-187">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="381b3-187">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="381b3-188">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="381b3-188">Additional resources</span></span>

<span data-ttu-id="381b3-189">Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="381b3-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="381b3-190">Další kroky</span><span class="sxs-lookup"><span data-stu-id="381b3-190">Next steps</span></span>

<span data-ttu-id="381b3-191">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="381b3-191">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="381b3-192">Seznámili jste se o asynchronním kódu</span><span class="sxs-lookup"><span data-stu-id="381b3-192">Learned about asynchronous code</span></span>
> * <span data-ttu-id="381b3-193">Vytvořil se kontroler oddělení.</span><span class="sxs-lookup"><span data-stu-id="381b3-193">Created a Department controller</span></span>
> * <span data-ttu-id="381b3-194">Použité uložené procedury</span><span class="sxs-lookup"><span data-stu-id="381b3-194">Used stored procedures</span></span>
> * <span data-ttu-id="381b3-195">Nasazené do Azure</span><span class="sxs-lookup"><span data-stu-id="381b3-195">Deployed to Azure</span></span>

<span data-ttu-id="381b3-196">V dalším článku se dozvíte, jak řešit konflikty, když více uživatelů aktualizuje stejnou entitu současně.</span><span class="sxs-lookup"><span data-stu-id="381b3-196">Advance to the next article to learn how to handle conflicts when multiple users update the same entity at the same time.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="381b3-197">Zpracování souběžnosti</span><span class="sxs-lookup"><span data-stu-id="381b3-197">Handling concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
