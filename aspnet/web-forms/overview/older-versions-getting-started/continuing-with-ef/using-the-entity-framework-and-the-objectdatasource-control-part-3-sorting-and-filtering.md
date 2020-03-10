---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 3: řazení a filtrování | Microsoft Docs'
author: tdykstra
description: Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená Začínáme pomocí řady kurzů Entity Framework 4,0. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631668"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="c852b-104">Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 3: řazení a filtrování</span><span class="sxs-lookup"><span data-stu-id="c852b-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="c852b-105">tím, že [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c852b-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="c852b-106">Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená [Začínáme pomocí řady kurzů Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) .</span><span class="sxs-lookup"><span data-stu-id="c852b-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="c852b-107">Pokud jste nedokončili předchozí kurzy, jako výchozí bod tohoto kurzu si můžete aplikaci, kterou jste vytvořili, [Stáhnout](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) .</span><span class="sxs-lookup"><span data-stu-id="c852b-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="c852b-108">Můžete si také [Stáhnout aplikaci](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , která je vytvořená úplnou řadou kurzů.</span><span class="sxs-lookup"><span data-stu-id="c852b-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="c852b-109">Pokud máte dotazy k kurzům, můžete je publikovat na [fórum ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).</span><span class="sxs-lookup"><span data-stu-id="c852b-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="c852b-110">V předchozím kurzu jste implementovali vzor úložiště v n-vrstvé webové aplikaci, která používá Entity Framework a ovládací prvek `ObjectDataSource`.</span><span class="sxs-lookup"><span data-stu-id="c852b-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="c852b-111">V tomto kurzu se dozvíte, jak provádět řazení a filtrování a zpracovávat scénáře hlavní-podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="c852b-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="c852b-112">Na stránku *oddělení. aspx* přidáte následující vylepšení:</span><span class="sxs-lookup"><span data-stu-id="c852b-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="c852b-113">Textové pole, které uživatelům umožní vybrat oddělení podle jména.</span><span class="sxs-lookup"><span data-stu-id="c852b-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="c852b-114">Seznam kurzů pro každé oddělení zobrazené v mřížce</span><span class="sxs-lookup"><span data-stu-id="c852b-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="c852b-115">Možnost řazení kliknutím na záhlaví sloupců.</span><span class="sxs-lookup"><span data-stu-id="c852b-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="c852b-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c852b-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="c852b-117">Přidání možnosti řazení sloupců GridView</span><span class="sxs-lookup"><span data-stu-id="c852b-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="c852b-118">Otevřete stránku *oddělení. aspx* a přidejte atribut `SortParameterName="sortExpression"` do ovládacího prvku `ObjectDataSource` s názvem `DepartmentsObjectDataSource`.</span><span class="sxs-lookup"><span data-stu-id="c852b-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="c852b-119">(Později vytvoříte metodu `GetDepartments`, která převezme parametr s názvem `sortExpression`.) Značky pro otevírací značku ovládacího prvku nyní připomínají následující příklad.</span><span class="sxs-lookup"><span data-stu-id="c852b-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="c852b-120">Přidejte atribut `AllowSorting="true"` do počáteční značky `GridView` ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="c852b-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="c852b-121">Značky pro otevírací značku ovládacího prvku nyní připomínají následující příklad.</span><span class="sxs-lookup"><span data-stu-id="c852b-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="c852b-122">V *departments.aspx.cs*nastavte výchozí pořadí řazení voláním metody `Sort` `GridView` ovládacího prvku z metody `Page_Load`:</span><span class="sxs-lookup"><span data-stu-id="c852b-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="c852b-123">Můžete přidat kód, který seřadí nebo filtruje buď ve třídě obchodní logiky, nebo ve třídě úložiště.</span><span class="sxs-lookup"><span data-stu-id="c852b-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="c852b-124">Pokud to provedete ve třídě obchodní logika, bude řazení nebo filtrování provedeno po načtení dat z databáze, protože třída obchodní logiky pracuje s objektem `IEnumerable` vráceným úložištěm.</span><span class="sxs-lookup"><span data-stu-id="c852b-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="c852b-125">Pokud přidáte kód pro řazení a filtrování do třídy úložiště a provedete jej před převodem výrazu LINQ nebo objektu na objekt `IEnumerable`, budou příkazy předány do databáze ke zpracování, což je obvykle efektivnější.</span><span class="sxs-lookup"><span data-stu-id="c852b-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="c852b-126">V tomto kurzu implementujete řazení a filtrování způsobem, který způsobí, že se zpracování provádí v databázi, tj. v úložišti.</span><span class="sxs-lookup"><span data-stu-id="c852b-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="c852b-127">Chcete-li přidat možnosti řazení, je nutné přidat novou metodu do rozhraní úložiště a třídy úložiště a také do třídy obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="c852b-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="c852b-128">V souboru *ISchoolRepository.cs* přidejte novou `GetDepartments` metodu, která převezme parametr `sortExpression`, který se použije k řazení seznamu vrácených oddělení:</span><span class="sxs-lookup"><span data-stu-id="c852b-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="c852b-129">Parametr `sortExpression` určí sloupec, podle kterého se má řadit, a směr řazení.</span><span class="sxs-lookup"><span data-stu-id="c852b-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="c852b-130">Do souboru *SchoolRepository.cs* přidejte kód pro novou metodu:</span><span class="sxs-lookup"><span data-stu-id="c852b-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="c852b-131">Změňte existující metodu `GetDepartments` bez parametrů pro volání nové metody:</span><span class="sxs-lookup"><span data-stu-id="c852b-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="c852b-132">V testovacím projektu přidejte následující novou metodu do *MockSchoolRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="c852b-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="c852b-133">Pokud jste chtěli vytvořit jakékoli testy jednotek, které jsou závislé na této metodě vracející seřazený seznam, museli byste seznam před jeho vrácením seřadit.</span><span class="sxs-lookup"><span data-stu-id="c852b-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="c852b-134">V tomto kurzu nebudete vytvářet testy jako v tomto kurzu, takže metoda může jednoduše vrátit Neseřazený seznam oddělení.</span><span class="sxs-lookup"><span data-stu-id="c852b-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="c852b-135">V souboru *SchoolBL.cs* přidejte následující novou metodu do třídy obchodní logiky:</span><span class="sxs-lookup"><span data-stu-id="c852b-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="c852b-136">Tento kód předá parametr řazení metodě úložiště.</span><span class="sxs-lookup"><span data-stu-id="c852b-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="c852b-137">Spusťte stránku *oddělení. aspx* .</span><span class="sxs-lookup"><span data-stu-id="c852b-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="c852b-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c852b-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="c852b-139">Nyní můžete kliknout na záhlaví kteréhokoli sloupce a řadit podle daného sloupce.</span><span class="sxs-lookup"><span data-stu-id="c852b-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="c852b-140">Pokud je sloupec již seřazený, kliknutím na záhlaví obrátíte směr řazení.</span><span class="sxs-lookup"><span data-stu-id="c852b-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="c852b-141">Přidání vyhledávacího pole</span><span class="sxs-lookup"><span data-stu-id="c852b-141">Adding a Search Box</span></span>

<span data-ttu-id="c852b-142">V této části přidáte textové pole hledání, propojíte ho s ovládacím prvkem `ObjectDataSource` pomocí parametru Control a přidáte metodu do třídy obchodní logiky pro podporu filtrování.</span><span class="sxs-lookup"><span data-stu-id="c852b-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="c852b-143">Otevřete stránku *oddělení. aspx* a přidejte následující značku mezi nadpisem a prvním ovládacím prvkem `ObjectDataSource`:</span><span class="sxs-lookup"><span data-stu-id="c852b-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="c852b-144">V ovládacím prvku `ObjectDataSource` s názvem `DepartmentsObjectDataSource`proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="c852b-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="c852b-145">Přidejte `SelectParameters` element pro parametr s názvem `nameSearchString`, který získá hodnotu zadanou v ovládacím prvku `SearchTextBox`.</span><span class="sxs-lookup"><span data-stu-id="c852b-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="c852b-146">Změňte hodnotu atributu `SelectMethod` na `GetDepartmentsByName`.</span><span class="sxs-lookup"><span data-stu-id="c852b-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="c852b-147">(Tuto metodu vytvoříte později.)</span><span class="sxs-lookup"><span data-stu-id="c852b-147">(You'll create this method later.)</span></span>

<span data-ttu-id="c852b-148">Značky pro ovládací prvek `ObjectDataSource` nyní připomínají následující příklad:</span><span class="sxs-lookup"><span data-stu-id="c852b-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="c852b-149">Do *ISchoolRepository.cs*přidejte metodu `GetDepartmentsByName`, která přijímá parametry `sortExpression` a `nameSearchString`:</span><span class="sxs-lookup"><span data-stu-id="c852b-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="c852b-150">Do *SchoolRepository.cs*přidejte následující novou metodu:</span><span class="sxs-lookup"><span data-stu-id="c852b-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="c852b-151">Tento kód používá metodu `Where` k výběru položek, které obsahují hledaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="c852b-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="c852b-152">Pokud je hledaný řetězec prázdný, budou vybrány všechny záznamy.</span><span class="sxs-lookup"><span data-stu-id="c852b-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="c852b-153">Všimněte si, že pokud zadáte volání metody společně v jednom příkazu (`Include`, pak `OrderBy`a pak `Where`), metoda `Where` musí vždy být poslední.</span><span class="sxs-lookup"><span data-stu-id="c852b-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="c852b-154">Změňte existující metodu `GetDepartments`, která převezme parametr `sortExpression` pro volání nové metody:</span><span class="sxs-lookup"><span data-stu-id="c852b-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="c852b-155">Do *MockSchoolRepository.cs* v testovacím projektu přidejte následující novou metodu:</span><span class="sxs-lookup"><span data-stu-id="c852b-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="c852b-156">Do *SchoolBL.cs*přidejte následující novou metodu:</span><span class="sxs-lookup"><span data-stu-id="c852b-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="c852b-157">Spusťte stránku *oddělení. aspx* a zadejte hledaný řetězec, abyste se ujistili, že logika výběru funguje.</span><span class="sxs-lookup"><span data-stu-id="c852b-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="c852b-158">Pole text nechejte prázdné a zkuste hledání zkontrolovat, zda jsou vráceny všechny záznamy.</span><span class="sxs-lookup"><span data-stu-id="c852b-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="c852b-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c852b-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="c852b-160">Přidání sloupce podrobností pro každý řádek mřížky</span><span class="sxs-lookup"><span data-stu-id="c852b-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="c852b-161">V dalším kroku chcete zobrazit všechny kurzy pro každé oddělení zobrazené v pravé buňce mřížky.</span><span class="sxs-lookup"><span data-stu-id="c852b-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="c852b-162">K tomuto účelu použijete vnořený ovládací prvek `GridView` a provedete jeho vázání na data z `Courses` navigační vlastnosti entity `Department`.</span><span class="sxs-lookup"><span data-stu-id="c852b-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="c852b-163">Otevřete panel *oddělení. aspx* a v části značky pro ovládací prvek `GridView` určete obslužnou rutinu pro událost `RowDataBound`.</span><span class="sxs-lookup"><span data-stu-id="c852b-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="c852b-164">Značky pro otevírací značku ovládacího prvku nyní připomínají následující příklad.</span><span class="sxs-lookup"><span data-stu-id="c852b-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="c852b-165">Přidejte nový element `TemplateField` za pole šablony `Administrator`:</span><span class="sxs-lookup"><span data-stu-id="c852b-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="c852b-166">Tento kód vytvoří vnořený `GridView` ovládací prvek, který zobrazuje číslo kurzu a název seznamu kurzů.</span><span class="sxs-lookup"><span data-stu-id="c852b-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="c852b-167">Neurčuje zdroj dat, protože ho v obslužné rutině `RowDataBound` provedete v kódu.</span><span class="sxs-lookup"><span data-stu-id="c852b-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="c852b-168">Otevřete *departments.aspx.cs* a přidejte následující obslužnou rutinu pro událost `RowDataBound`:</span><span class="sxs-lookup"><span data-stu-id="c852b-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="c852b-169">Tento kód získá `Department` entitu z argumentů události, převede `Courses` navigační vlastnost na kolekci `List` a dataváže vnořenou `GridView` do kolekce.</span><span class="sxs-lookup"><span data-stu-id="c852b-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="c852b-170">Otevřete soubor *SchoolRepository.cs* a zadejte Eager načítání pro navigační vlastnost `Courses` voláním metody `Include` v dotazu objektu, který vytvoříte v metodě `GetDepartmentsByName`.</span><span class="sxs-lookup"><span data-stu-id="c852b-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="c852b-171">Příkaz `return` v metodě `GetDepartmentsByName` nyní vypadá podobně jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="c852b-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="c852b-172">Spusťte stránku.</span><span class="sxs-lookup"><span data-stu-id="c852b-172">Run the page.</span></span> <span data-ttu-id="c852b-173">Kromě možnosti řazení a filtrování, které jste přidali dříve, ovládací prvek GridView nyní zobrazuje informace o vnořeném kurzu pro každé oddělení.</span><span class="sxs-lookup"><span data-stu-id="c852b-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="c852b-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c852b-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="c852b-175">Tím se dokončí Úvod ke scénářům řazení, filtrování a hlavní-podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="c852b-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="c852b-176">V dalším kurzu se dozvíte, jak zpracovávat souběžnost.</span><span class="sxs-lookup"><span data-stu-id="c852b-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c852b-177">[Předchozí](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [Další](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="c852b-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
