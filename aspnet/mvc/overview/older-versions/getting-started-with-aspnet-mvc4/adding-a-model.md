---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: Přidání modelu | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457801"
---
# <a name="adding-a-model"></a><span data-ttu-id="554de-104">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="554de-104">Adding a Model</span></span>

<span data-ttu-id="554de-105">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="554de-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="554de-106">K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="554de-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="554de-107">Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.</span><span class="sxs-lookup"><span data-stu-id="554de-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="554de-108">V této části přidáte některé třídy pro správu filmů v databázi.</span><span class="sxs-lookup"><span data-stu-id="554de-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="554de-109">Tyto třídy budou &quot;model&quot; součást aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="554de-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="554de-110">K definování a práci s těmito třídami modelů použijete .NET Framework technologie pro přístup k datům, která je známá jako [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) .</span><span class="sxs-lookup"><span data-stu-id="554de-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="554de-111">Entity Framework (často označované jako EF) podporují vývojové paradigma nazvané *Code First*.</span><span class="sxs-lookup"><span data-stu-id="554de-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="554de-112">Code First umožňuje vytvářet objekty modelu zápisem jednoduchých tříd.</span><span class="sxs-lookup"><span data-stu-id="554de-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="554de-113">(Tyto třídy jsou také známé jako třídy POCO, od &quot;objektů CLR, které jsou prosté staré.&quot;) Databázi pak můžete z vašich tříd vytvořit průběžně, což umožňuje velmi čistý a rychlý vývojový pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="554de-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="554de-114">Přidávání tříd modelu</span><span class="sxs-lookup"><span data-stu-id="554de-114">Adding Model Classes</span></span>

<span data-ttu-id="554de-115">V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.</span><span class="sxs-lookup"><span data-stu-id="554de-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="554de-116">Zadejte název *třídy* &quot;filmový&quot;.</span><span class="sxs-lookup"><span data-stu-id="554de-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="554de-117">Do `Movie` třídy přidejte následující pět vlastností:</span><span class="sxs-lookup"><span data-stu-id="554de-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="554de-118">K reprezentaci filmů v databázi použijeme třídu `Movie`.</span><span class="sxs-lookup"><span data-stu-id="554de-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="554de-119">Každá instance `Movie` objektu bude odpovídat řádku v tabulce databáze a každá vlastnost `Movie` třídy bude namapována na sloupec v tabulce.</span><span class="sxs-lookup"><span data-stu-id="554de-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="554de-120">Do stejného souboru přidejte následující třídu `MovieDBContext`:</span><span class="sxs-lookup"><span data-stu-id="554de-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="554de-121">Třída `MovieDBContext` představuje kontext Entity Framework filmového databáze, který zpracovává načítání, ukládání a aktualizaci instancí tříd `Movie` v databázi.</span><span class="sxs-lookup"><span data-stu-id="554de-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="554de-122">`MovieDBContext` je odvozen ze `DbContext` základní třídy poskytované Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="554de-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="554de-123">Aby bylo možné odkazovat `DbContext` a `DbSet`, je nutné do horní části souboru přidat následující příkaz `using`:</span><span class="sxs-lookup"><span data-stu-id="554de-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="554de-124">Úplný soubor *Movie.cs* je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="554de-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="554de-125">(Několik příkazů using, které nejsou potřeba, se odebralo.)</span><span class="sxs-lookup"><span data-stu-id="554de-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="554de-126">Vytvoření připojovacího řetězce a práce s databází SQL Serveru LocalDB</span><span class="sxs-lookup"><span data-stu-id="554de-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="554de-127">Třída `MovieDBContext`, kterou jste vytvořili, zpracovává úlohu připojení k databázi a mapování objektů `Movie` na záznamy databáze.</span><span class="sxs-lookup"><span data-stu-id="554de-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="554de-128">Jedna otázka, na kterou se můžete zeptat, ale je, jak určit databázi, ke které se bude připojovat.</span><span class="sxs-lookup"><span data-stu-id="554de-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="554de-129">Provedete to tak, že přidáte informace o připojení do souboru *Web. config* aplikace.</span><span class="sxs-lookup"><span data-stu-id="554de-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="554de-130">Otevřete kořenový soubor *Web. config* aplikace.</span><span class="sxs-lookup"><span data-stu-id="554de-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="554de-131">(Ne soubor *Web. config* ve složce *views* .) Otevřete soubor *Web. config* , který je popsaný červeně.</span><span class="sxs-lookup"><span data-stu-id="554de-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="554de-132">Přidejte následující připojovací řetězec do prvku `<connectionStrings>` v souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="554de-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="554de-133">Následující příklad ukazuje část souboru *Web. config* s přidaným novým připojovacím řetězcem:</span><span class="sxs-lookup"><span data-stu-id="554de-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="554de-134">Tento malý objem kódu a XML je vše, co potřebujete k tomu, abyste mohli zastupovat a ukládat data videa v databázi.</span><span class="sxs-lookup"><span data-stu-id="554de-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="554de-135">V dalším kroku vytvoříte novou třídu `MoviesController`, kterou můžete použít k zobrazení dat filmu a umožníte uživatelům vytvářet nové seznamy filmů.</span><span class="sxs-lookup"><span data-stu-id="554de-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="554de-136">[Předchozí](adding-a-view.md)
> [Další](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="554de-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
