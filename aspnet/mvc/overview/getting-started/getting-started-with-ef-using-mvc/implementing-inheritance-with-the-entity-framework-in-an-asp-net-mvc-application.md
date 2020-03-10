---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: Implementace dědičnosti s EF v aplikacích ASP.NET MVC 5'
description: Tento kurz vám ukáže, jak implementovat dědičnost v datovém modelu.
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583060"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a><span data-ttu-id="de6d4-103">Kurz: Implementace dědičnosti s EF v aplikaci ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="de6d4-103">Tutorial: Implement Inheritance with EF in an ASP.NET MVC 5 app</span></span>

<span data-ttu-id="de6d4-104">V předchozím kurzu jste zpracovali výjimky souběžnosti.</span><span class="sxs-lookup"><span data-stu-id="de6d4-104">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="de6d4-105">Tento kurz vám ukáže, jak implementovat dědičnost v datovém modelu.</span><span class="sxs-lookup"><span data-stu-id="de6d4-105">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="de6d4-106">V objektově orientovaném programování můžete použít [Dědičnost](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) k usnadnění [opětovného použití kódu](http://en.wikipedia.org/wiki/Code_reuse).</span><span class="sxs-lookup"><span data-stu-id="de6d4-106">In object-oriented programming, you can use [inheritance](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) to facilitate [code reuse](http://en.wikipedia.org/wiki/Code_reuse).</span></span> <span data-ttu-id="de6d4-107">V tomto kurzu změníte `Instructor` a `Student` třídy tak, aby byly odvozeny ze `Person` základní třídy obsahující vlastnosti, jako `LastName`, které jsou společné pro instruktory i studenty.</span><span class="sxs-lookup"><span data-stu-id="de6d4-107">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="de6d4-108">Nepřidáte ani neměníte žádné webové stránky, ale změníte část kódu a tyto změny se automaticky projeví v databázi.</span><span class="sxs-lookup"><span data-stu-id="de6d4-108">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

<span data-ttu-id="de6d4-109">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="de6d4-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="de6d4-110">Naučte se mapovat dědění na databázi.</span><span class="sxs-lookup"><span data-stu-id="de6d4-110">Learn to map inheritance to database</span></span>
> * <span data-ttu-id="de6d4-111">Vytvoření třídy Person</span><span class="sxs-lookup"><span data-stu-id="de6d4-111">Create the Person class</span></span>
> * <span data-ttu-id="de6d4-112">Aktualizace instruktora a studenta</span><span class="sxs-lookup"><span data-stu-id="de6d4-112">Update Instructor and Student</span></span>
> * <span data-ttu-id="de6d4-113">Přidat osobu do modelu</span><span class="sxs-lookup"><span data-stu-id="de6d4-113">Add Person to the Model</span></span>
> * <span data-ttu-id="de6d4-114">Vytváření a aktualizace migrací</span><span class="sxs-lookup"><span data-stu-id="de6d4-114">Create and Update Migrations</span></span>
> * <span data-ttu-id="de6d4-115">Testování implementace</span><span class="sxs-lookup"><span data-stu-id="de6d4-115">Test the implementation</span></span>
> * <span data-ttu-id="de6d4-116">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="de6d4-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de6d4-117">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="de6d4-117">Prerequisites</span></span>

* [<span data-ttu-id="de6d4-118">Ošetření souběžnosti</span><span class="sxs-lookup"><span data-stu-id="de6d4-118">Handling Concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a><span data-ttu-id="de6d4-119">Mapování dědičnosti na databázi</span><span class="sxs-lookup"><span data-stu-id="de6d4-119">Map inheritance to database</span></span>

<span data-ttu-id="de6d4-120">Třídy `Instructor` a `Student` v datovém modelu `School` mají několik vlastností, které jsou identické:</span><span class="sxs-lookup"><span data-stu-id="de6d4-120">The `Instructor` and `Student` classes in the `School` data model have several properties that are identical:</span></span>

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="de6d4-122">Předpokládejme, že chcete eliminovat redundantní kód pro vlastnosti, které jsou sdíleny `Instructor` a `Student` entit.</span><span class="sxs-lookup"><span data-stu-id="de6d4-122">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="de6d4-123">Nebo chcete napsat službu, která může formátovat názvy bez caring, jestli název pochází od instruktora nebo studenta.</span><span class="sxs-lookup"><span data-stu-id="de6d4-123">Or you want to write a service that can format names without caring whether the name came from an instructor or a student.</span></span> <span data-ttu-id="de6d4-124">Můžete vytvořit `Person` základní třídu, která obsahuje pouze tyto sdílené vlastnosti, a poté nastavit `Instructor` a `Student` entit z této základní třídy, jak je znázorněno na následujícím obrázku:</span><span class="sxs-lookup"><span data-stu-id="de6d4-124">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="de6d4-126">Existuje několik způsobů, jak lze tuto strukturu dědičnosti znázornit v databázi.</span><span class="sxs-lookup"><span data-stu-id="de6d4-126">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="de6d4-127">Můžete mít `Person`ovou tabulku, která obsahuje informace o studentech i instruktorech v jedné tabulce.</span><span class="sxs-lookup"><span data-stu-id="de6d4-127">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="de6d4-128">Některé sloupce by se mohly vztahovat jenom na instruktory (`HireDate`), některé jenom pro studenty (`EnrollmentDate`), u obou (`LastName`, `FirstName`).</span><span class="sxs-lookup"><span data-stu-id="de6d4-128">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="de6d4-129">Obvykle byste měli sloupec *diskriminátoru* , který určuje, který typ každý řádek představuje.</span><span class="sxs-lookup"><span data-stu-id="de6d4-129">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="de6d4-130">Sloupec diskriminátoru může mít například "instruktor" pro studenty a studenta.</span><span class="sxs-lookup"><span data-stu-id="de6d4-130">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Table-per-hierarchy_example](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="de6d4-132">Tento model generování struktury dědičnosti entit z jedné databázové tabulky se nazývá dědičnost *typu tabulka-na hierarchii* (TPH).</span><span class="sxs-lookup"><span data-stu-id="de6d4-132">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="de6d4-133">Alternativou je, že databáze vypadá podobně jako struktura dědičnosti.</span><span class="sxs-lookup"><span data-stu-id="de6d4-133">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="de6d4-134">Například můžete mít pouze pole název v tabulce `Person` a mají oddělené tabulky `Instructor` a `Student` s poli data.</span><span class="sxs-lookup"><span data-stu-id="de6d4-134">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="de6d4-136">Tento model vytvoření tabulky databáze pro každou třídu entity se nazývá dědičnost *tabulky podle typu* (TPT).</span><span class="sxs-lookup"><span data-stu-id="de6d4-136">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="de6d4-137">Ještě další možností je mapovat všechny neabstraktní typy na jednotlivé tabulky.</span><span class="sxs-lookup"><span data-stu-id="de6d4-137">Yet another option is to map all non-abstract types to individual tables.</span></span> <span data-ttu-id="de6d4-138">Všechny vlastnosti třídy, včetně děděných vlastností, jsou mapovány na sloupce odpovídající tabulky.</span><span class="sxs-lookup"><span data-stu-id="de6d4-138">All properties of a class, including inherited properties, map to columns of the corresponding table.</span></span> <span data-ttu-id="de6d4-139">Tento model se nazývá dědičnost tříd (TPC) podle konkrétní třídy.</span><span class="sxs-lookup"><span data-stu-id="de6d4-139">This pattern is called Table-per-Concrete Class (TPC) inheritance.</span></span> <span data-ttu-id="de6d4-140">Pokud jste implementovali dědičnost TPC pro třídy `Person`, `Student`a `Instructor`, jak je uvedeno výše, tabulky `Student` a `Instructor` by po implementaci dědičnosti nevypadaly jinak než předtím.</span><span class="sxs-lookup"><span data-stu-id="de6d4-140">If you implemented TPC inheritance for the `Person`, `Student`, and `Instructor` classes as shown earlier, the `Student` and `Instructor` tables would look no different after implementing inheritance than they did before.</span></span>

<span data-ttu-id="de6d4-141">Vzorce dědičnosti TPC a TPH obvykle poskytují lepší výkon ve vzorcích dědičnosti Entity Framework než TPT, protože vzory TPT můžou mít za následek složité spojování dotazů.</span><span class="sxs-lookup"><span data-stu-id="de6d4-141">TPC and TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span>

<span data-ttu-id="de6d4-142">Tento kurz ukazuje, jak implementovat dědičnosti TPH.</span><span class="sxs-lookup"><span data-stu-id="de6d4-142">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="de6d4-143">TPH je výchozím vzorem dědičnosti v Entity Framework, takže vše, co musíte udělat, je vytvořit `Person` třídy, změnit `Instructor` a `Student` třídy, aby byly odvozeny z `Person`, přidejte do `DbContext`novou třídu a vytvořte migraci.</span><span class="sxs-lookup"><span data-stu-id="de6d4-143">TPH is the default inheritance pattern in the Entity Framework, so all you have to do is create a `Person` class, change the `Instructor` and `Student` classes to derive from `Person`, add the new class to the `DbContext`, and create a migration.</span></span> <span data-ttu-id="de6d4-144">(Informace o tom, jak implementovat další vzory dědičnosti, najdete v tématu [mapování dědičnosti typu tabulka na typ (TPT)](https://msdn.microsoft.com/data/jj591617#2.5) a [mapování dědičnosti třídy (TPC) na konkrétní třídu ()](https://msdn.microsoft.com/data/jj591617#2.6) v dokumentaci MSDN Entity Framework.)</span><span class="sxs-lookup"><span data-stu-id="de6d4-144">(For information about how to implement the other inheritance patterns, see [Mapping the Table-Per-Type (TPT) Inheritance](https://msdn.microsoft.com/data/jj591617#2.5) and [Mapping the Table-Per-Concrete Class (TPC) Inheritance](https://msdn.microsoft.com/data/jj591617#2.6) in the MSDN Entity Framework documentation.)</span></span>

## <a name="create-the-person-class"></a><span data-ttu-id="de6d4-145">Vytvoření třídy Person</span><span class="sxs-lookup"><span data-stu-id="de6d4-145">Create the Person class</span></span>

<span data-ttu-id="de6d4-146">Ve složce *modely* vytvořte *Person.cs* a nahraďte kód šablony následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="de6d4-146">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a><span data-ttu-id="de6d4-147">Aktualizace instruktora a studenta</span><span class="sxs-lookup"><span data-stu-id="de6d4-147">Update Instructor and Student</span></span>

<span data-ttu-id="de6d4-148">Teď aktualizujte *Instructor.cs* a *student.cs* , aby dědily hodnoty z *Person.SC*.</span><span class="sxs-lookup"><span data-stu-id="de6d4-148">Now update the *Instructor.cs* and *Student.cs* to inherit values from the *Person.sc*.</span></span>

<span data-ttu-id="de6d4-149">V *Instructor.cs*odvodíte třídu `Instructor` z `Person` třídy a odstraňte pole klíč a název.</span><span class="sxs-lookup"><span data-stu-id="de6d4-149">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="de6d4-150">Kód bude vypadat jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="de6d4-150">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="de6d4-151">Udělejte podobné změny v *student.cs*.</span><span class="sxs-lookup"><span data-stu-id="de6d4-151">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="de6d4-152">Třída `Student` bude vypadat jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="de6d4-152">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a><span data-ttu-id="de6d4-153">Přidat osobu do modelu</span><span class="sxs-lookup"><span data-stu-id="de6d4-153">Add Person to the Model</span></span>

<span data-ttu-id="de6d4-154">Do *SchoolContext.cs*přidejte vlastnost `DbSet` pro typ entity `Person`:</span><span class="sxs-lookup"><span data-stu-id="de6d4-154">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="de6d4-155">To je vše, co Entity Framework potřebuje, aby bylo možné nakonfigurovat dědičnost tabulek na hierarchii.</span><span class="sxs-lookup"><span data-stu-id="de6d4-155">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="de6d4-156">Jak vidíte, při aktualizaci databáze bude mít `Person` tabulku místo tabulek `Student` a `Instructor`.</span><span class="sxs-lookup"><span data-stu-id="de6d4-156">As you'll see, when the database is updated, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="create-and-update-migrations"></a><span data-ttu-id="de6d4-157">Vytváření a aktualizace migrací</span><span class="sxs-lookup"><span data-stu-id="de6d4-157">Create and Update Migrations</span></span>

<span data-ttu-id="de6d4-158">V konzole správce balíčků (PMC) zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="de6d4-158">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="de6d4-159">Spusťte příkaz `Update-Database` v PMC.</span><span class="sxs-lookup"><span data-stu-id="de6d4-159">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="de6d4-160">Příkaz v tomto okamžiku selže, protože máme existující data, která migrace nedokáže zpracovat.</span><span class="sxs-lookup"><span data-stu-id="de6d4-160">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="de6d4-161">Zobrazí se chybová zpráva podobná následující:</span><span class="sxs-lookup"><span data-stu-id="de6d4-161">You get an error message like the following one:</span></span>

> <span data-ttu-id="de6d4-162">*Nelze vyřadit objekt dbo. Instructor, protože na něj odkazuje omezení CIZÍho klíče.*</span><span class="sxs-lookup"><span data-stu-id="de6d4-162">*Could not drop object 'dbo.Instructor' because it is referenced by a FOREIGN KEY constraint.*</span></span>

<span data-ttu-id="de6d4-163">Otevřete *migrace\&lt; timestamp&gt;\_Inheritance.cs* a nahraďte metodu `Up` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="de6d4-163">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="de6d4-164">Tento kód má na starosti následující úlohy aktualizace databáze:</span><span class="sxs-lookup"><span data-stu-id="de6d4-164">This code takes care of the following database update tasks:</span></span>

- <span data-ttu-id="de6d4-165">Odebere omezení a indexy cizího klíče, které odkazují na tabulku studenta.</span><span class="sxs-lookup"><span data-stu-id="de6d4-165">Removes foreign key constraints and indexes that point to the Student table.</span></span>
- <span data-ttu-id="de6d4-166">Přejmenuje tabulku instruktora jako osobu a provede změny potřebné k uložení dat studenta:</span><span class="sxs-lookup"><span data-stu-id="de6d4-166">Renames the Instructor table as Person and makes changes needed for it to store Student data:</span></span>

    - <span data-ttu-id="de6d4-167">Přidá EnrollmentDate s možnou hodnotou null pro studenty.</span><span class="sxs-lookup"><span data-stu-id="de6d4-167">Adds nullable EnrollmentDate for students.</span></span>
    - <span data-ttu-id="de6d4-168">Přidá sloupec diskriminátoru, který označuje, zda je řádek určen studentem nebo instruktorem.</span><span class="sxs-lookup"><span data-stu-id="de6d4-168">Adds Discriminator column to indicate whether a row is for a student or an instructor.</span></span>
    - <span data-ttu-id="de6d4-169">Vytvoří hodnotu Nullable s možnou hodnotou null, protože řádky studenta nebudou mít data přijetí.</span><span class="sxs-lookup"><span data-stu-id="de6d4-169">Makes HireDate nullable since student rows won't have hire dates.</span></span>
    - <span data-ttu-id="de6d4-170">Přidá dočasné pole, které bude použito k aktualizaci cizích klíčů, které odkazují na studenty.</span><span class="sxs-lookup"><span data-stu-id="de6d4-170">Adds a temporary field that will be used to update foreign keys that point to students.</span></span> <span data-ttu-id="de6d4-171">Když zkopírujete studenty do tabulky Person, získají se nové hodnoty primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="de6d4-171">When you copy students into the Person table they'll get new primary key values.</span></span>
- <span data-ttu-id="de6d4-172">Zkopíruje data z tabulky student do tabulky Person (osoba).</span><span class="sxs-lookup"><span data-stu-id="de6d4-172">Copies data from the Student table into the Person table.</span></span> <span data-ttu-id="de6d4-173">To způsobí, že studenti získají přiřazené nové hodnoty primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="de6d4-173">This causes students to get assigned new primary key values.</span></span>
- <span data-ttu-id="de6d4-174">Opravuje hodnoty cizích klíčů, které odkazují na studenty.</span><span class="sxs-lookup"><span data-stu-id="de6d4-174">Fixes foreign key values that point to students.</span></span>
- <span data-ttu-id="de6d4-175">Znovu vytvoří omezení a indexy cizího klíče, které se teď odkazují na tabulku Person.</span><span class="sxs-lookup"><span data-stu-id="de6d4-175">Re-creates foreign key constraints and indexes, now pointing them to the Person table.</span></span>

<span data-ttu-id="de6d4-176">(Pokud jste použili GUID místo celého čísla jako typ primárního klíče, hodnoty primárního klíče studenta se nemusejí změnit a některé z těchto kroků by mohly být vynechány.)</span><span class="sxs-lookup"><span data-stu-id="de6d4-176">(If you had used GUID instead of integer as the primary key type, the student primary key values wouldn't have to change, and several of these steps could have been omitted.)</span></span>

<span data-ttu-id="de6d4-177">Znovu spusťte příkaz `update-database`.</span><span class="sxs-lookup"><span data-stu-id="de6d4-177">Run the `update-database` command again.</span></span>

<span data-ttu-id="de6d4-178">(V produkčním systému provedete odpovídající změny v metodě Down pro případ, že byste to museli použít pro návrat k předchozí verzi databáze.</span><span class="sxs-lookup"><span data-stu-id="de6d4-178">(In a production system you would make corresponding changes to the Down method in case you ever had to use that to go back to the previous database version.</span></span> <span data-ttu-id="de6d4-179">V tomto kurzu nebudete používat metodu Down.)</span><span class="sxs-lookup"><span data-stu-id="de6d4-179">For this tutorial you won't be using the Down method.)</span></span>

> [!NOTE]
> <span data-ttu-id="de6d4-180">Při migraci dat a provádění změn schématu je možné získat další chyby.</span><span class="sxs-lookup"><span data-stu-id="de6d4-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="de6d4-181">Pokud se zobrazí chyby migrace, které nemůžete vyřešit, můžete pokračovat v kurzu změnou připojovacího řetězce v souboru *Web. config* nebo odstraněním databáze.</span><span class="sxs-lookup"><span data-stu-id="de6d4-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or by deleting the database.</span></span> <span data-ttu-id="de6d4-182">Nejjednodušším přístupem je přejmenovat databázi v souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="de6d4-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="de6d4-183">Například změňte název databáze na ContosoUniversity2, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="de6d4-183">For example, change the database name to ContosoUniversity2 as shown in the following example:</span></span>
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> <span data-ttu-id="de6d4-184">V případě nové databáze nejsou k dispozici žádná data k migraci a příkaz `update-database` je mnohem větší, než může být dokončena bez chyb.</span><span class="sxs-lookup"><span data-stu-id="de6d4-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="de6d4-185">Pokyny k odstranění databáze naleznete v tématu [How to drop a Database from a Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span><span class="sxs-lookup"><span data-stu-id="de6d4-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="de6d4-186">Pokud tento přístup potrváte, abyste mohli pokračovat v tomto kurzu, přeskočte krok nasazení na konci tohoto kurzu nebo ho nasaďte na novou lokalitu a databázi.</span><span class="sxs-lookup"><span data-stu-id="de6d4-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial or deploy to a new site and database.</span></span> <span data-ttu-id="de6d4-187">Pokud nasadíte aktualizaci na stejnou lokalitu, do které jste už nasadili, EF se při automatickém spuštění migrace zobrazí stejná chyba.</span><span class="sxs-lookup"><span data-stu-id="de6d4-187">If you deploy an update to the same site you've been deploying to already, EF will get the same error there when it runs migrations automatically.</span></span> <span data-ttu-id="de6d4-188">Pokud chcete řešit potíže s chybami migrace, nejlepším prostředkem je Entity Framework fóra nebo StackOverflow.com.</span><span class="sxs-lookup"><span data-stu-id="de6d4-188">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="test-the-implementation"></a><span data-ttu-id="de6d4-189">Testování implementace</span><span class="sxs-lookup"><span data-stu-id="de6d4-189">Test the implementation</span></span>

<span data-ttu-id="de6d4-190">Spusťte web a vyzkoušejte různé stránky.</span><span class="sxs-lookup"><span data-stu-id="de6d4-190">Run the site and try various pages.</span></span> <span data-ttu-id="de6d4-191">Vše funguje stejně jako dříve.</span><span class="sxs-lookup"><span data-stu-id="de6d4-191">Everything works the same as it did before.</span></span>

<span data-ttu-id="de6d4-192">V **Průzkumník serveru** rozbalte **Connections\SchoolContext data** a pak **tabulky**a uvidíte, že tabulky **student** a **instruktor** byly nahrazeny tabulkou **Person** .</span><span class="sxs-lookup"><span data-stu-id="de6d4-192">In **Server Explorer,** expand **Data Connections\SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="de6d4-193">Rozbalte tabulku **Person (osoba** ) a uvidíte, že obsahuje všechny sloupce, které se používají v tabulkách **student** a **instruktor** .</span><span class="sxs-lookup"><span data-stu-id="de6d4-193">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

<span data-ttu-id="de6d4-194">Klikněte pravým tlačítkem myši na tabulku Person a potom kliknutím na možnost **Zobrazit data tabulky** zobrazte sloupec diskriminátor.</span><span class="sxs-lookup"><span data-stu-id="de6d4-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

<span data-ttu-id="de6d4-195">Následující diagram znázorňuje strukturu nové školní databáze:</span><span class="sxs-lookup"><span data-stu-id="de6d4-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="de6d4-197">Nasazení do Azure</span><span class="sxs-lookup"><span data-stu-id="de6d4-197">Deploy to Azure</span></span>

<span data-ttu-id="de6d4-198">Tato část vyžaduje, abyste dokončili volitelné **nasazení aplikace do Azure** v [části 3, řazení, filtrování a stránkování](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) této série kurzů.</span><span class="sxs-lookup"><span data-stu-id="de6d4-198">This section requires you to have completed the optional **Deploying the app to Azure** section in [Part 3, Sorting, Filtering, and Paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) of this tutorial series.</span></span> <span data-ttu-id="de6d4-199">Pokud jste převedli chyby, které jste vyřešili odstraněním databáze v místním projektu, přeskočte tento krok; nebo vytvořte novou lokalitu a databázi a nasaďte ji do nového prostředí.</span><span class="sxs-lookup"><span data-stu-id="de6d4-199">If you had migrations errors that you resolved by deleting the database in your local project, skip this step; or create a new site and database, and deploy to the new environment.</span></span>

1. <span data-ttu-id="de6d4-200">V aplikaci Visual Studio klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a v místní nabídce vyberte **publikovat** .</span><span class="sxs-lookup"><span data-stu-id="de6d4-200">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

2. <span data-ttu-id="de6d4-201">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="de6d4-201">Click **Publish**.</span></span>

    <span data-ttu-id="de6d4-202">Webová aplikace se otevře ve výchozím prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="de6d4-202">The Web app opens in your default browser.</span></span>

3. <span data-ttu-id="de6d4-203">Otestujte aplikaci, abyste ověřili, že funguje.</span><span class="sxs-lookup"><span data-stu-id="de6d4-203">Test the application to verify it's working.</span></span>

    <span data-ttu-id="de6d4-204">Při prvním spuštění stránky, která přistupuje k databázi, Entity Framework spustí všechny migrace `Up` metody potřebné k zajištění aktuálnosti databáze s aktuálním datovým modelem.</span><span class="sxs-lookup"><span data-stu-id="de6d4-204">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="de6d4-205">Získání kódu</span><span class="sxs-lookup"><span data-stu-id="de6d4-205">Get the code</span></span>

[<span data-ttu-id="de6d4-206">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="de6d4-206">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="de6d4-207">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="de6d4-207">Additional resources</span></span>

<span data-ttu-id="de6d4-208">Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="de6d4-208">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="de6d4-209">Další informace o této a dalších strukturách dědičnosti najdete v tématu model [dědičnosti TPT](https://msdn.microsoft.com/data/jj618293) a [vzor dědičnosti TPH](https://msdn.microsoft.com/data/jj618292) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="de6d4-209">For more information about this and other inheritance structures, see [TPT Inheritance Pattern](https://msdn.microsoft.com/data/jj618293) and [TPH Inheritance Pattern](https://msdn.microsoft.com/data/jj618292) on MSDN.</span></span> <span data-ttu-id="de6d4-210">V dalším kurzu se dozvíte, jak zvládnout celou řadu poměrně pokročilých scénářů Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="de6d4-210">In the next tutorial you'll see how to handle a variety of relatively advanced Entity Framework scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de6d4-211">Další kroky</span><span class="sxs-lookup"><span data-stu-id="de6d4-211">Next steps</span></span>

<span data-ttu-id="de6d4-212">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="de6d4-212">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="de6d4-213">Bylo naučeno k mapování dědičnosti na databázi.</span><span class="sxs-lookup"><span data-stu-id="de6d4-213">Learned to map inheritance to database</span></span>
> * <span data-ttu-id="de6d4-214">Byla vytvořena třída Person.</span><span class="sxs-lookup"><span data-stu-id="de6d4-214">Created the Person class</span></span>
> * <span data-ttu-id="de6d4-215">Aktualizovaný instruktor a student</span><span class="sxs-lookup"><span data-stu-id="de6d4-215">Updated Instructor and Student</span></span>
> * <span data-ttu-id="de6d4-216">Do modelu se přidala osoba.</span><span class="sxs-lookup"><span data-stu-id="de6d4-216">Added Person to the Model</span></span>
> * <span data-ttu-id="de6d4-217">Vytvořené a aktualizované migrace</span><span class="sxs-lookup"><span data-stu-id="de6d4-217">Created and Update Migrations</span></span>
> * <span data-ttu-id="de6d4-218">Otestování implementace</span><span class="sxs-lookup"><span data-stu-id="de6d4-218">Tested the implementation</span></span>
> * <span data-ttu-id="de6d4-219">Nasazené do Azure</span><span class="sxs-lookup"><span data-stu-id="de6d4-219">Deployed to Azure</span></span>

<span data-ttu-id="de6d4-220">V dalším článku se dozvíte o tématech, o kterých je užitečné vědět, když překročíte základy vývoje webových aplikací ASP.NET, které používají Entity Framework Code First.</span><span class="sxs-lookup"><span data-stu-id="de6d4-220">Advance to the next article to learn about topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="de6d4-221">Pokročilé scénáře pro Entity Framework</span><span class="sxs-lookup"><span data-stu-id="de6d4-221">Advanced Entity Framework Scenarios</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
