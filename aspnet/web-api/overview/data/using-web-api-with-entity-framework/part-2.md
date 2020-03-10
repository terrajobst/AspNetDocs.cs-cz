---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: Přidání modelů a řadičů | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557538"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="6b438-102">Přidání modelů a kontrolerů</span><span class="sxs-lookup"><span data-stu-id="6b438-102">Add Models and Controllers</span></span>

<span data-ttu-id="6b438-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6b438-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6b438-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="6b438-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="6b438-105">V této části přidáte třídy modelů, které definují entity databáze.</span><span class="sxs-lookup"><span data-stu-id="6b438-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="6b438-106">Pak přidáte řadiče webového rozhraní API, které u těchto entit provádějí operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="6b438-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="6b438-107">Přidat třídy modelu</span><span class="sxs-lookup"><span data-stu-id="6b438-107">Add Model Classes</span></span>

<span data-ttu-id="6b438-108">V tomto kurzu vytvoříme databázi pomocí přístupu Code First k Entity Framework (EF).</span><span class="sxs-lookup"><span data-stu-id="6b438-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="6b438-109">Pomocí Code First zapisujete C# třídy, které odpovídají tabulkám databáze, a EF vytvoří databázi.</span><span class="sxs-lookup"><span data-stu-id="6b438-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="6b438-110">(Další informace najdete v tématu [Entity Framework vývojové přístupy](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span><span class="sxs-lookup"><span data-stu-id="6b438-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="6b438-111">Začneme definováním našich doménových objektů jako POCOs (objekty CLR ve starém Old).</span><span class="sxs-lookup"><span data-stu-id="6b438-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="6b438-112">Vytvoříme následující POCOs:</span><span class="sxs-lookup"><span data-stu-id="6b438-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="6b438-113">Autor</span><span class="sxs-lookup"><span data-stu-id="6b438-113">Author</span></span>
- <span data-ttu-id="6b438-114">Book</span><span class="sxs-lookup"><span data-stu-id="6b438-114">Book</span></span>

<span data-ttu-id="6b438-115">V Průzkumník řešení klikněte pravým tlačítkem na složku modely.</span><span class="sxs-lookup"><span data-stu-id="6b438-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="6b438-116">Vyberte **Přidat**a pak vybrat **třídu**.</span><span class="sxs-lookup"><span data-stu-id="6b438-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="6b438-117">Pojmenujte `Author`třídy.</span><span class="sxs-lookup"><span data-stu-id="6b438-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="6b438-118">Nahraďte celý často používaný kód v Author.cs následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="6b438-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="6b438-119">Přidejte další třídu s názvem `Book`s následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="6b438-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="6b438-120">Entity Framework použijí tyto modely k vytváření databázových tabulek.</span><span class="sxs-lookup"><span data-stu-id="6b438-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="6b438-121">U každého modelu se vlastnost `Id` stane sloupcem primárního klíče tabulky databáze.</span><span class="sxs-lookup"><span data-stu-id="6b438-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="6b438-122">V třídě Book `AuthorId` definuje cizí klíč do tabulky `Author`.</span><span class="sxs-lookup"><span data-stu-id="6b438-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="6b438-123">(Pro zjednodušení jsem předpokládáme, že každá kniha má jednoho autora.) Třída Book také obsahuje navigační vlastnost se souvisejícím `Author`.</span><span class="sxs-lookup"><span data-stu-id="6b438-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="6b438-124">Navigační vlastnost slouží k přístupu k souvisejícímu `Author` v kódu.</span><span class="sxs-lookup"><span data-stu-id="6b438-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="6b438-125">Vyberu si další informace o navigačních vlastnostech v části 4, [zpracování vztahů mezi entitami](part-4.md).</span><span class="sxs-lookup"><span data-stu-id="6b438-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="6b438-126">Přidat řadiče webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6b438-126">Add Web API Controllers</span></span>

<span data-ttu-id="6b438-127">V této části přidáme řadiče webového rozhraní API, které podporují operace CRUD (vytváření, čtení, aktualizace a odstraňování).</span><span class="sxs-lookup"><span data-stu-id="6b438-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="6b438-128">Řadiče budou používat Entity Framework ke komunikaci s databázovou vrstvou.</span><span class="sxs-lookup"><span data-stu-id="6b438-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="6b438-129">Nejprve můžete odstranit soubory Controllers/ValuesController. cs.</span><span class="sxs-lookup"><span data-stu-id="6b438-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="6b438-130">Tento soubor obsahuje ukázkový kontroler webového rozhraní API, ale pro tento kurz ho nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="6b438-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="6b438-131">V dalším kroku Sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="6b438-131">Next, build the project.</span></span> <span data-ttu-id="6b438-132">Lešení webového rozhraní API používá reflexi k nalezení tříd modelu, takže potřebuje zkompilované sestavení.</span><span class="sxs-lookup"><span data-stu-id="6b438-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="6b438-133">V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="6b438-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="6b438-134">Vyberte **Přidat**a pak vybrat **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="6b438-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="6b438-135">V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte jako kontroler webové rozhraní API 2 akce pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6b438-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="6b438-136">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6b438-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="6b438-137">V dialogovém okně **Přidat řadič** proveďte následující:</span><span class="sxs-lookup"><span data-stu-id="6b438-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="6b438-138">V rozevíracím seznamu **třída modelu** vyberte třídu `Author`.</span><span class="sxs-lookup"><span data-stu-id="6b438-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="6b438-139">(Pokud ji nevidíte v rozevíracím seznamu, ujistěte se, že jste projekt sestavili.)</span><span class="sxs-lookup"><span data-stu-id="6b438-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="6b438-140">Podívejte se na použití akcí asynchronního kontroleru.</span><span class="sxs-lookup"><span data-stu-id="6b438-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="6b438-141">Ponechte název kontroleru &quot;AuthorsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="6b438-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="6b438-142">Klikněte na tlačítko plus (+) vedle pole **Třída datového kontextu**.</span><span class="sxs-lookup"><span data-stu-id="6b438-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="6b438-143">V dialogu **nový kontext dat** ponechte výchozí název a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6b438-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="6b438-144">Kliknutím na tlačítko **Přidat** dokončete dialog **Přidat řadič** .</span><span class="sxs-lookup"><span data-stu-id="6b438-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="6b438-145">Dialogové okno přidá do projektu dvě třídy:</span><span class="sxs-lookup"><span data-stu-id="6b438-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="6b438-146">`AuthorsController` definuje kontroler webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6b438-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="6b438-147">Kontroler implementuje REST API, které klienti používají k provádění operací CRUD v seznamu autorů.</span><span class="sxs-lookup"><span data-stu-id="6b438-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="6b438-148">`BookServiceContext` spravuje objekty entit za běhu, což zahrnuje vyplnění objektů daty z databáze, sledování změn a uchování dat v databázi.</span><span class="sxs-lookup"><span data-stu-id="6b438-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="6b438-149">Dědí z `DbContext`.</span><span class="sxs-lookup"><span data-stu-id="6b438-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="6b438-150">V tomto okamžiku Sestavte projekt znovu.</span><span class="sxs-lookup"><span data-stu-id="6b438-150">At this point, build the project again.</span></span> <span data-ttu-id="6b438-151">Teď Projděte stejný postup, abyste přidali kontroler rozhraní API pro `Book` entit.</span><span class="sxs-lookup"><span data-stu-id="6b438-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="6b438-152">Tentokrát vyberte `Book` pro třídu modelu a vyberte existující třídu `BookServiceContext` třídy datového kontextu.</span><span class="sxs-lookup"><span data-stu-id="6b438-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="6b438-153">(Nevytvářet nový kontext dat.) Kliknutím na **Přidat** přidejte kontroler.</span><span class="sxs-lookup"><span data-stu-id="6b438-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="6b438-154">[Předchozí](part-1.md)
> [Další](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="6b438-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
