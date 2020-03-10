---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Použití Migrace Code First k osazení databáze | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557454"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="2ab66-102">Použití Migrace Code First k osazení databáze</span><span class="sxs-lookup"><span data-stu-id="2ab66-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="2ab66-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2ab66-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="2ab66-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="2ab66-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="2ab66-105">V této části použijete [migrace Code First](https://msdn.microsoft.com/data/jj591621) v EF k osazení databáze s testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="2ab66-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="2ab66-106">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="2ab66-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="2ab66-107">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="2ab66-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="2ab66-108">Tento příkaz přidá do projektu složku s názvem migrace a ve složce Migraces vytvoří soubor kódu s názvem Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="2ab66-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="2ab66-109">Otevřete soubor Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="2ab66-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="2ab66-110">Přidejte následující příkaz **using** .</span><span class="sxs-lookup"><span data-stu-id="2ab66-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="2ab66-111">Poté do metody **Configuration. Seed** přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="2ab66-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="2ab66-112">V okně konzoly Správce balíčků zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="2ab66-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="2ab66-113">První příkaz vygeneruje kód, který vytvoří databázi, a druhý příkaz spustí tento kód.</span><span class="sxs-lookup"><span data-stu-id="2ab66-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="2ab66-114">Databáze je vytvořena lokálně pomocí [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ab66-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="2ab66-115">Prozkoumat rozhraní API (volitelné)</span><span class="sxs-lookup"><span data-stu-id="2ab66-115">Explore the API (Optional)</span></span>

<span data-ttu-id="2ab66-116">Stisknutím klávesy F5 spusťte aplikaci v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="2ab66-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="2ab66-117">Visual Studio spustí IIS Express a spustí vaši webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2ab66-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="2ab66-118">Visual Studio potom spustí prohlížeč a otevře domovskou stránku aplikace.</span><span class="sxs-lookup"><span data-stu-id="2ab66-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="2ab66-119">Když Visual Studio spustí webový projekt, přiřadí číslo portu.</span><span class="sxs-lookup"><span data-stu-id="2ab66-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="2ab66-120">Na následujícím obrázku je číslo portu 50524.</span><span class="sxs-lookup"><span data-stu-id="2ab66-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="2ab66-121">Při spuštění aplikace se zobrazí jiné číslo portu.</span><span class="sxs-lookup"><span data-stu-id="2ab66-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="2ab66-122">Domovská stránka se implementuje pomocí ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2ab66-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="2ab66-123">V horní části stránky je odkaz, který říká "rozhraní API".</span><span class="sxs-lookup"><span data-stu-id="2ab66-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="2ab66-124">Tento odkaz vám umožní automaticky vygenerovanou stránku s nápovědu pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2ab66-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="2ab66-125">(Pokud se chcete dozvědět, jak se tato stránka této stránky vygenerovala, a jak na stránku přidat vlastní dokumentaci, přečtěte si téma [Vytvoření stránek s nápovědu pro webové rozhraní API ASP.NET](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Kliknutím na odkazy na stránku v nápovědě zobrazíte podrobnosti o rozhraní API, včetně formátu požadavků a odpovědí.</span><span class="sxs-lookup"><span data-stu-id="2ab66-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="2ab66-126">Rozhraní API povoluje operace CRUD v databázi.</span><span class="sxs-lookup"><span data-stu-id="2ab66-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="2ab66-127">Následující shrnuje rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2ab66-127">The following summarizes the API.</span></span>

| <span data-ttu-id="2ab66-128">Autoři</span><span class="sxs-lookup"><span data-stu-id="2ab66-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="2ab66-129">GET api/authors</span><span class="sxs-lookup"><span data-stu-id="2ab66-129">GET api/authors</span></span> | <span data-ttu-id="2ab66-130">Získá všechny autory.</span><span class="sxs-lookup"><span data-stu-id="2ab66-130">Get all authors.</span></span> |
| <span data-ttu-id="2ab66-131">GET api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="2ab66-131">GET api/authors/{id}</span></span> | <span data-ttu-id="2ab66-132">Získejte autora podle ID.</span><span class="sxs-lookup"><span data-stu-id="2ab66-132">Get an author by ID.</span></span> |
| <span data-ttu-id="2ab66-133">POST /api/authors</span><span class="sxs-lookup"><span data-stu-id="2ab66-133">POST /api/authors</span></span> | <span data-ttu-id="2ab66-134">Vytvořit nového autora</span><span class="sxs-lookup"><span data-stu-id="2ab66-134">Create a new author.</span></span> |
| <span data-ttu-id="2ab66-135">PUT /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="2ab66-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="2ab66-136">Aktualizace existujícího autora</span><span class="sxs-lookup"><span data-stu-id="2ab66-136">Update an existing author.</span></span> |
| <span data-ttu-id="2ab66-137">DELETE /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="2ab66-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="2ab66-138">Odstraní autora.</span><span class="sxs-lookup"><span data-stu-id="2ab66-138">Delete an author.</span></span> |

| <span data-ttu-id="2ab66-139">Knihy</span><span class="sxs-lookup"><span data-stu-id="2ab66-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="2ab66-140">GET /api/books</span><span class="sxs-lookup"><span data-stu-id="2ab66-140">GET /api/books</span></span> | <span data-ttu-id="2ab66-141">Získejte všechny knihy.</span><span class="sxs-lookup"><span data-stu-id="2ab66-141">Get all books.</span></span> |
| <span data-ttu-id="2ab66-142">GET /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="2ab66-142">GET /api/books/{id}</span></span> | <span data-ttu-id="2ab66-143">Získat knihu podle ID</span><span class="sxs-lookup"><span data-stu-id="2ab66-143">Get a book by ID.</span></span> |
| <span data-ttu-id="2ab66-144">POST /api/books</span><span class="sxs-lookup"><span data-stu-id="2ab66-144">POST /api/books</span></span> | <span data-ttu-id="2ab66-145">Vytvořte novou knihu.</span><span class="sxs-lookup"><span data-stu-id="2ab66-145">Create a new book.</span></span> |
| <span data-ttu-id="2ab66-146">PUT /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="2ab66-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="2ab66-147">Aktualizuje existující knihu.</span><span class="sxs-lookup"><span data-stu-id="2ab66-147">Update an existing book.</span></span> |
| <span data-ttu-id="2ab66-148">DELETE /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="2ab66-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="2ab66-149">Odstraní knihu.</span><span class="sxs-lookup"><span data-stu-id="2ab66-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="2ab66-150">Zobrazit databázi (volitelné)</span><span class="sxs-lookup"><span data-stu-id="2ab66-150">View the Database (Optional)</span></span>

<span data-ttu-id="2ab66-151">Při spuštění příkazu Update-Database se v EF vytvořila databáze a volala se metoda `Seed`.</span><span class="sxs-lookup"><span data-stu-id="2ab66-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="2ab66-152">Když aplikaci spouštíte místně, EF používá [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ab66-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="2ab66-153">Databázi můžete zobrazit v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ab66-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="2ab66-154">V nabídce **Zobrazení** vyberte **Průzkumník objektů systému SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2ab66-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="2ab66-155">V dialogovém okně **připojit k serveru** zadejte do pole **název serveru** text "(LocalDB) \v11.0".</span><span class="sxs-lookup"><span data-stu-id="2ab66-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="2ab66-156">U možnosti **ověřování** ponechte možnost ověřování systému Windows.</span><span class="sxs-lookup"><span data-stu-id="2ab66-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="2ab66-157">Klikněte na **Připojit**.</span><span class="sxs-lookup"><span data-stu-id="2ab66-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="2ab66-158">Visual Studio se připojí k LocalDB a zobrazí vaše existující databáze v okně Průzkumník objektů systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2ab66-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="2ab66-159">Uzly můžete rozbalit a zobrazit tak tabulky, které jsme vytvořili v EF.</span><span class="sxs-lookup"><span data-stu-id="2ab66-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="2ab66-160">Data zobrazíte tak, že kliknete pravým tlačítkem na tabulku a vyberete **Zobrazit data**.</span><span class="sxs-lookup"><span data-stu-id="2ab66-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="2ab66-161">Následující snímek obrazovky ukazuje výsledky pro tabulku Books.</span><span class="sxs-lookup"><span data-stu-id="2ab66-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="2ab66-162">Všimněte si, že EF naplnilo databázi daty počáteční hodnoty a tabulka obsahuje cizí klíč do tabulky autoři.</span><span class="sxs-lookup"><span data-stu-id="2ab66-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="2ab66-163">[Předchozí](part-2.md)
> [Další](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="2ab66-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
