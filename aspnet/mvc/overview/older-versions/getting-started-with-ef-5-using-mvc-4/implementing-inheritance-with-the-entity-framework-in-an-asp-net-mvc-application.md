---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: Implementace dědičnosti s Entity Framework v aplikaci ASP.NET MVC (8 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595322"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="f6e41-103">Implementace dědičnosti s Entity Framework v aplikaci ASP.NET MVC (8 z 10)</span><span class="sxs-lookup"><span data-stu-id="f6e41-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="f6e41-104">tím, že [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f6e41-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f6e41-105">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="f6e41-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="f6e41-106">Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="f6e41-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="f6e41-107">Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="f6e41-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="f6e41-108">Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.</span><span class="sxs-lookup"><span data-stu-id="f6e41-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="f6e41-109">Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován.</span><span class="sxs-lookup"><span data-stu-id="f6e41-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="f6e41-110">Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem.</span><span class="sxs-lookup"><span data-stu-id="f6e41-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="f6e41-111">Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="f6e41-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="f6e41-112">V předchozím kurzu jste zpracovali výjimky souběžnosti.</span><span class="sxs-lookup"><span data-stu-id="f6e41-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="f6e41-113">Tento kurz vám ukáže, jak implementovat dědičnost v datovém modelu.</span><span class="sxs-lookup"><span data-stu-id="f6e41-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="f6e41-114">V objektově orientovaném programování můžete použít dědičnost k eliminaci nadbytečného kódu.</span><span class="sxs-lookup"><span data-stu-id="f6e41-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="f6e41-115">V tomto kurzu změníte `Instructor` a `Student` třídy tak, aby byly odvozeny ze `Person` základní třídy obsahující vlastnosti, jako `LastName`, které jsou společné pro instruktory i studenty.</span><span class="sxs-lookup"><span data-stu-id="f6e41-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="f6e41-116">Nepřidáte ani neměníte žádné webové stránky, ale změníte část kódu a tyto změny se automaticky projeví v databázi.</span><span class="sxs-lookup"><span data-stu-id="f6e41-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="f6e41-117">Dědičnost tabulek na základě hierarchie a typů</span><span class="sxs-lookup"><span data-stu-id="f6e41-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="f6e41-118">V objektově orientovaném programování můžete použít dědičnost, aby bylo snazší pracovat se souvisejícími třídami.</span><span class="sxs-lookup"><span data-stu-id="f6e41-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="f6e41-119">Například třídy `Instructor` a `Student` v datovém modelu `School` sdílejí několik vlastností, což má za následek redundantní kód:</span><span class="sxs-lookup"><span data-stu-id="f6e41-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="f6e41-121">Předpokládejme, že chcete eliminovat redundantní kód pro vlastnosti, které jsou sdíleny `Instructor` a `Student` entit.</span><span class="sxs-lookup"><span data-stu-id="f6e41-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="f6e41-122">Můžete vytvořit `Person` základní třídu, která obsahuje pouze tyto sdílené vlastnosti, a poté nastavit `Instructor` a `Student` entit z této základní třídy, jak je znázorněno na následujícím obrázku:</span><span class="sxs-lookup"><span data-stu-id="f6e41-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="f6e41-124">Existuje několik způsobů, jak lze tuto strukturu dědičnosti znázornit v databázi.</span><span class="sxs-lookup"><span data-stu-id="f6e41-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="f6e41-125">Můžete mít `Person`ovou tabulku, která obsahuje informace o studentech i instruktorech v jedné tabulce.</span><span class="sxs-lookup"><span data-stu-id="f6e41-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="f6e41-126">Některé sloupce by se mohly vztahovat jenom na instruktory (`HireDate`), některé jenom pro studenty (`EnrollmentDate`), u obou (`LastName`, `FirstName`).</span><span class="sxs-lookup"><span data-stu-id="f6e41-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="f6e41-127">Obvykle byste měli sloupec *diskriminátoru* , který určuje, který typ každý řádek představuje.</span><span class="sxs-lookup"><span data-stu-id="f6e41-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="f6e41-128">Sloupec diskriminátoru může mít například "instruktor" pro studenty a studenta.</span><span class="sxs-lookup"><span data-stu-id="f6e41-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Tabulka-podle hierarchy_example](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="f6e41-130">Tento model generování struktury dědičnosti entit z jedné databázové tabulky se nazývá dědičnost *typu tabulka-na hierarchii* (TPH).</span><span class="sxs-lookup"><span data-stu-id="f6e41-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="f6e41-131">Alternativou je, že databáze vypadá podobně jako struktura dědičnosti.</span><span class="sxs-lookup"><span data-stu-id="f6e41-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="f6e41-132">Například můžete mít pouze pole název v tabulce `Person` a mají oddělené tabulky `Instructor` a `Student` s poli data.</span><span class="sxs-lookup"><span data-stu-id="f6e41-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Tabulka-podle type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="f6e41-134">Tento model vytvoření tabulky databáze pro každou třídu entity se nazývá dědičnost *tabulky podle typu* (TPT).</span><span class="sxs-lookup"><span data-stu-id="f6e41-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="f6e41-135">Vzory dědičnosti TPH obvykle poskytují lepší výkon v Entity Framework než TPT vzory dědičnosti, protože vzory TPT můžou mít za následek složité spojování dotazů.</span><span class="sxs-lookup"><span data-stu-id="f6e41-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="f6e41-136">Tento kurz ukazuje, jak implementovat dědičnosti TPH.</span><span class="sxs-lookup"><span data-stu-id="f6e41-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="f6e41-137">Provedete to provedením následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="f6e41-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="f6e41-138">Vytvořte třídu `Person` a změňte `Instructor` a `Student` třídy, aby byly odvozeny od `Person`.</span><span class="sxs-lookup"><span data-stu-id="f6e41-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="f6e41-139">Přidejte kód mapování modelu do databáze do třídy kontextu databáze.</span><span class="sxs-lookup"><span data-stu-id="f6e41-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="f6e41-140">Změňte `InstructorID` a `StudentID` odkazy v celém projektu na `PersonID`.</span><span class="sxs-lookup"><span data-stu-id="f6e41-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="f6e41-141">Vytvoření třídy Person</span><span class="sxs-lookup"><span data-stu-id="f6e41-141">Creating the Person Class</span></span>

 <span data-ttu-id="f6e41-142">Poznámka: po vytvoření následujících tříd nebudete moct projekt zkompilovat, dokud neaktualizujete řadiče, které používají tyto třídy.</span><span class="sxs-lookup"><span data-stu-id="f6e41-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="f6e41-143">Ve složce *modely* vytvořte *Person.cs* a nahraďte kód šablony následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="f6e41-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="f6e41-144">V *Instructor.cs*odvodíte třídu `Instructor` z `Person` třídy a odstraňte pole klíč a název.</span><span class="sxs-lookup"><span data-stu-id="f6e41-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="f6e41-145">Kód bude vypadat jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="f6e41-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="f6e41-146">Udělejte podobné změny v *student.cs*.</span><span class="sxs-lookup"><span data-stu-id="f6e41-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="f6e41-147">Třída `Student` bude vypadat jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="f6e41-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="f6e41-148">Přidání typu entity Person do modelu</span><span class="sxs-lookup"><span data-stu-id="f6e41-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="f6e41-149">Do *SchoolContext.cs*přidejte vlastnost `DbSet` pro typ entity `Person`:</span><span class="sxs-lookup"><span data-stu-id="f6e41-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="f6e41-150">To je vše, co Entity Framework potřebuje, aby bylo možné nakonfigurovat dědičnost tabulek na hierarchii.</span><span class="sxs-lookup"><span data-stu-id="f6e41-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="f6e41-151">Jak vidíte, po opětovném vytvoření databáze bude mít `Person` tabulku místo `Student` a `Instructor` tabulek.</span><span class="sxs-lookup"><span data-stu-id="f6e41-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="f6e41-152">Změna InstructorID a StudentID na PersonID</span><span class="sxs-lookup"><span data-stu-id="f6e41-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="f6e41-153">V *SchoolContext.cs*změňte v příkazu instruktor-Course Mapping `MapRightKey("InstructorID")` na `MapRightKey("PersonID")`:</span><span class="sxs-lookup"><span data-stu-id="f6e41-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="f6e41-154">Tato změna se nevyžaduje. pouze změní název sloupce InstructorID v tabulce m:n (n:n JOIN).</span><span class="sxs-lookup"><span data-stu-id="f6e41-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="f6e41-155">Pokud jste název opustili jako InstructorID, aplikace bude pořád fungovat správně.</span><span class="sxs-lookup"><span data-stu-id="f6e41-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="f6e41-156">Zde je dokončený *SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="f6e41-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="f6e41-157">Dále je třeba změnit `InstructorID` na `PersonID` a `StudentID` na `PersonID` v rámci projektu ***s výjimkou*** souborů migrace s časovým razítkem ve složce *migrace* .</span><span class="sxs-lookup"><span data-stu-id="f6e41-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="f6e41-158">Chcete-li vyhledat a otevřít pouze soubory, které je třeba změnit, proveďte globální změnu otevřených souborů.</span><span class="sxs-lookup"><span data-stu-id="f6e41-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="f6e41-159">Jediným souborem ve složce *migraces* , který byste měli změnit, je *Migrations\Configuration.cs.*</span><span class="sxs-lookup"><span data-stu-id="f6e41-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="f6e41-160">Začněte tím, že zavřete všechny otevřené soubory v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6e41-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="f6e41-161">Klikněte na **Najít a nahradit – vyhledejte všechny soubory** v nabídce **Upravit** a pak vyhledejte všechny soubory v projektu, které obsahují `InstructorID`.</span><span class="sxs-lookup"><span data-stu-id="f6e41-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="f6e41-162">V okně **výsledky hledání** otevřete každý soubor ***s výjimkou*** &lt;časového razítka&gt; *\_. cs* soubory migrace ve složce *migrace* dvakrát klikněte na jeden řádek pro každý soubor.</span><span class="sxs-lookup"><span data-stu-id="f6e41-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="f6e41-163">Otevřete dialogové okno **nahradit v souborech** a změňte položku **Zobrazit ve** **všech otevřených dokumentech**.</span><span class="sxs-lookup"><span data-stu-id="f6e41-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="f6e41-164">Pomocí dialogového okna **nahradit v souborech** změňte všechny `InstructorID` na `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="f6e41-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="f6e41-165">Vyhledá všechny soubory v projektu, které obsahují `StudentID`.</span><span class="sxs-lookup"><span data-stu-id="f6e41-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="f6e41-166">V okně **výsledky hledání** otevřete každý soubor ***s výjimkou*** &lt;časového razítka&gt; *\_\** soubory migrace cs ve složce *migrace* dvakrát klikněte na jeden řádek pro každý soubor.</span><span class="sxs-lookup"><span data-stu-id="f6e41-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="f6e41-167">Otevřete dialogové okno **nahradit v souborech** a změňte položku **Zobrazit ve** **všech otevřených dokumentech**.</span><span class="sxs-lookup"><span data-stu-id="f6e41-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="f6e41-168">Pomocí dialogového okna **nahradit v souborech** změňte všechny `StudentID` na `PersonID`.</span><span class="sxs-lookup"><span data-stu-id="f6e41-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="f6e41-169">Sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="f6e41-169">Build the project.</span></span>

<span data-ttu-id="f6e41-170">(Všimněte si, že to ukazuje *nevýhodu* `classnameID`ho vzoru pro pojmenovávání primárních klíčů.</span><span class="sxs-lookup"><span data-stu-id="f6e41-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="f6e41-171">Pokud jste pojmenovali ID primárního klíče bez předpony názvu třídy, *není* nyní nutné žádné přejmenování.)</span><span class="sxs-lookup"><span data-stu-id="f6e41-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="f6e41-172">Vytvoření a aktualizace souboru migrace</span><span class="sxs-lookup"><span data-stu-id="f6e41-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="f6e41-173">V konzole správce balíčků (PMC) zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="f6e41-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="f6e41-174">Spusťte příkaz `Update-Database` v PMC.</span><span class="sxs-lookup"><span data-stu-id="f6e41-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="f6e41-175">Příkaz v tomto okamžiku selže, protože máme existující data, která migrace nedokáže zpracovat.</span><span class="sxs-lookup"><span data-stu-id="f6e41-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="f6e41-176">Zobrazí se následující chyba:</span><span class="sxs-lookup"><span data-stu-id="f6e41-176">You get the following error:</span></span>

<span data-ttu-id="f6e41-177">*Příkaz ALTER TABLE je v konfliktu s omezením CIZÍho klíče "FK\_dbo. Oddělení\_dbo. Person\_PersonID ". Ke konfliktu došlo v databázi "ContosoUniversity", tabulce "dbo". Person, sloupec ' PersonID '.*</span><span class="sxs-lookup"><span data-stu-id="f6e41-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="f6e41-178">Otevřete *migrace\&lt; timestamp&gt;\_Inheritance.cs* a nahraďte metodu `Up` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="f6e41-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="f6e41-179">Znovu spusťte příkaz `update-database`.</span><span class="sxs-lookup"><span data-stu-id="f6e41-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e41-180">Při migraci dat a provádění změn schématu je možné získat další chyby.</span><span class="sxs-lookup"><span data-stu-id="f6e41-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="f6e41-181">Pokud získáte chyby migrace, které nemůžete vyřešit, můžete pokračovat v kurzu změnou připojovacího řetězce v souboru *Web. config* nebo odstraněním databáze.</span><span class="sxs-lookup"><span data-stu-id="f6e41-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="f6e41-182">Nejjednodušším přístupem je přejmenovat databázi v souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="f6e41-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="f6e41-183">Například změňte název databáze na CU\_test, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="f6e41-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="f6e41-184">V případě nové databáze nejsou k dispozici žádná data k migraci a příkaz `update-database` je mnohem větší, než může být dokončena bez chyb.</span><span class="sxs-lookup"><span data-stu-id="f6e41-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="f6e41-185">Pokyny k odstranění databáze naleznete v tématu [How to drop a Database from a Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span><span class="sxs-lookup"><span data-stu-id="f6e41-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="f6e41-186">Pokud tento přístup potrváte, abyste mohli pokračovat v tomto kurzu, přeskočte na konci tohoto kurzu krok nasazení, protože nasazená lokalita by při automatickém spuštění migrace mohla získat stejnou chybu.</span><span class="sxs-lookup"><span data-stu-id="f6e41-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="f6e41-187">Pokud chcete řešit potíže s chybami migrace, nejlepším prostředkem je Entity Framework fóra nebo StackOverflow.com.</span><span class="sxs-lookup"><span data-stu-id="f6e41-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="f6e41-188">Testování</span><span class="sxs-lookup"><span data-stu-id="f6e41-188">Testing</span></span>

<span data-ttu-id="f6e41-189">Spusťte web a vyzkoušejte různé stránky.</span><span class="sxs-lookup"><span data-stu-id="f6e41-189">Run the site and try various pages.</span></span> <span data-ttu-id="f6e41-190">Vše funguje stejně jako dříve.</span><span class="sxs-lookup"><span data-stu-id="f6e41-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="f6e41-191">V **Průzkumník serveru** rozbalte **SchoolContext** a pak **tabulky**a uvidíte, že tabulky **student** a **instruktor** byly nahrazeny tabulkou **Person** .</span><span class="sxs-lookup"><span data-stu-id="f6e41-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="f6e41-192">Rozbalte tabulku **Person (osoba** ) a uvidíte, že obsahuje všechny sloupce, které se používají v tabulkách **student** a **instruktor** .</span><span class="sxs-lookup"><span data-stu-id="f6e41-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="f6e41-194">Klikněte pravým tlačítkem myši na tabulku Person a potom kliknutím na možnost **Zobrazit data tabulky** zobrazte sloupec diskriminátor.</span><span class="sxs-lookup"><span data-stu-id="f6e41-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="f6e41-195">Následující diagram znázorňuje strukturu nové školní databáze:</span><span class="sxs-lookup"><span data-stu-id="f6e41-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="f6e41-197">Přehled</span><span class="sxs-lookup"><span data-stu-id="f6e41-197">Summary</span></span>

<span data-ttu-id="f6e41-198">Pro třídy `Person`, `Student`a `Instructor` se teď implementovala dědičnost tabulky na hierarchii.</span><span class="sxs-lookup"><span data-stu-id="f6e41-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="f6e41-199">Další informace o této a dalších strukturách dědičnosti najdete v tématu [strategie mapování dědičnosti](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) na blogu Morteza Manavi.</span><span class="sxs-lookup"><span data-stu-id="f6e41-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="f6e41-200">V dalším kurzu uvidíte několik způsobů implementace úložiště a pracovní jednotky vzorů.</span><span class="sxs-lookup"><span data-stu-id="f6e41-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="f6e41-201">Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).</span><span class="sxs-lookup"><span data-stu-id="f6e41-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f6e41-202">[Předchozí](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Další](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="f6e41-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
