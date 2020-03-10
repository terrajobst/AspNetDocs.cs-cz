---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: Zobrazení tabulky databázových dat (C#) | Microsoft Docs
author: microsoft
description: V tomto kurzu si ukážeme dvě metody zobrazení sady záznamů databáze. Zobrazuje se dvě metody formátování sady záznamů databáze v HTML...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3c908d030076fc8400190ef3cf1672632ac1ed6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543139"
---
# <a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="2caf8-104">Zobrazení tabulky databázových dat (C#)</span><span class="sxs-lookup"><span data-stu-id="2caf8-104">Displaying a Table of Database Data (C#)</span></span>

<span data-ttu-id="2caf8-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2caf8-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2caf8-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="2caf8-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="2caf8-107">V tomto kurzu si ukážeme dvě metody zobrazení sady záznamů databáze.</span><span class="sxs-lookup"><span data-stu-id="2caf8-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="2caf8-108">Zobrazuje se dvě metody formátování sady záznamů databáze v tabulce HTML.</span><span class="sxs-lookup"><span data-stu-id="2caf8-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="2caf8-109">Nejprve ukazuje, jak lze naformátovat záznamy databáze přímo v rámci zobrazení.</span><span class="sxs-lookup"><span data-stu-id="2caf8-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="2caf8-110">Dále ukážeme, jak můžete při formátování záznamů databáze využít výhod částečných.</span><span class="sxs-lookup"><span data-stu-id="2caf8-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="2caf8-111">Cílem tohoto kurzu je vysvětlit, jak můžete zobrazit tabulku dat databáze HTML v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2caf8-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="2caf8-112">Nejprve se naučíte, jak pomocí nástrojů pro generování uživatelského rozhraní, které jsou součástí sady Visual Studio, vygenerovat zobrazení, které automaticky zobrazí sadu záznamů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="2caf8-113">V dalším kroku se dozvíte, jak při formátování záznamů databáze použít částečnou jako šablonu.</span><span class="sxs-lookup"><span data-stu-id="2caf8-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="2caf8-114">Vytvoření tříd modelu</span><span class="sxs-lookup"><span data-stu-id="2caf8-114">Create the Model Classes</span></span>

<span data-ttu-id="2caf8-115">Chystáme se zobrazit sadu záznamů z tabulky databáze filmů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="2caf8-116">Tabulka video s filmy obsahuje následující sloupce:</span><span class="sxs-lookup"><span data-stu-id="2caf8-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>

| <span data-ttu-id="2caf8-117">**Název sloupce**</span><span class="sxs-lookup"><span data-stu-id="2caf8-117">**Column Name**</span></span> | <span data-ttu-id="2caf8-118">**Datový typ**</span><span class="sxs-lookup"><span data-stu-id="2caf8-118">**Data Type**</span></span> | <span data-ttu-id="2caf8-119">**Povoluje hodnoty null.**</span><span class="sxs-lookup"><span data-stu-id="2caf8-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2caf8-120">ID</span><span class="sxs-lookup"><span data-stu-id="2caf8-120">Id</span></span> | <span data-ttu-id="2caf8-121">Int</span><span class="sxs-lookup"><span data-stu-id="2caf8-121">Int</span></span> | <span data-ttu-id="2caf8-122">False</span><span class="sxs-lookup"><span data-stu-id="2caf8-122">False</span></span> |
| <span data-ttu-id="2caf8-123">Název</span><span class="sxs-lookup"><span data-stu-id="2caf8-123">Title</span></span> | <span data-ttu-id="2caf8-124">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="2caf8-124">Nvarchar(200)</span></span> | <span data-ttu-id="2caf8-125">False</span><span class="sxs-lookup"><span data-stu-id="2caf8-125">False</span></span> |
| <span data-ttu-id="2caf8-126">Ředitel</span><span class="sxs-lookup"><span data-stu-id="2caf8-126">Director</span></span> | <span data-ttu-id="2caf8-127">NVarchar(50)</span><span class="sxs-lookup"><span data-stu-id="2caf8-127">NVarchar(50)</span></span> | <span data-ttu-id="2caf8-128">False</span><span class="sxs-lookup"><span data-stu-id="2caf8-128">False</span></span> |
| <span data-ttu-id="2caf8-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="2caf8-129">DateReleased</span></span> | <span data-ttu-id="2caf8-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="2caf8-130">DateTime</span></span> | <span data-ttu-id="2caf8-131">False</span><span class="sxs-lookup"><span data-stu-id="2caf8-131">False</span></span> |

<span data-ttu-id="2caf8-132">Aby bylo možné znázornit tabulku filmů v naší aplikaci ASP.NET MVC, musíme vytvořit třídu modelu.</span><span class="sxs-lookup"><span data-stu-id="2caf8-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="2caf8-133">V tomto kurzu používáme Microsoft Entity Framework k vytváření tříd modelů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2caf8-134">V tomto kurzu používáme Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2caf8-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="2caf8-135">Je ale důležité si uvědomit, že k interakci s databází z aplikace ASP.NET MVC, včetně LINQ to SQL, NHibernate nebo ADO.NET, můžete použít celou řadu různých technologií.</span><span class="sxs-lookup"><span data-stu-id="2caf8-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="2caf8-136">Pomocí těchto kroků spusťte Průvodce model EDM (Entity Data Model):</span><span class="sxs-lookup"><span data-stu-id="2caf8-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="2caf8-137">V okně Průzkumník řešení klikněte pravým tlačítkem na složku modely a vyberte možnost nabídky **Přidat, nová položka**.</span><span class="sxs-lookup"><span data-stu-id="2caf8-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="2caf8-138">Vyberte kategorii **dat** a vyberte šablonu **model EDM (Entity Data Model) ADO.NET** .</span><span class="sxs-lookup"><span data-stu-id="2caf8-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="2caf8-139">Udělte datovému modelu název *MoviesDBModel. edmx* a klikněte na tlačítko **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="2caf8-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="2caf8-140">Po kliknutí na tlačítko Přidat se zobrazí průvodce model EDM (Entity Data Model) (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="2caf8-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="2caf8-141">Pomocí těchto kroků dokončete Průvodce:</span><span class="sxs-lookup"><span data-stu-id="2caf8-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="2caf8-142">V kroku **zvolit obsah modelu** vyberte možnost **Generovat z databáze** .</span><span class="sxs-lookup"><span data-stu-id="2caf8-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="2caf8-143">V kroku **Vybrat datové připojení** použijte datové připojení *MoviesDB. mdf* a název *MoviesDBEntities* pro nastavení připojení.</span><span class="sxs-lookup"><span data-stu-id="2caf8-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="2caf8-144">Klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="2caf8-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="2caf8-145">V kroku **Zvolte databázové objekty** rozbalte uzel tabulky a vyberte tabulku filmy.</span><span class="sxs-lookup"><span data-stu-id="2caf8-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="2caf8-146">Zadejte *modely* názvů a klikněte na tlačítko **Dokončit** .</span><span class="sxs-lookup"><span data-stu-id="2caf8-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="2caf8-147">[![vytváření tříd LINQ to SQL](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2caf8-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="2caf8-148">**Obrázek 01**: vytváření tříd LINQ to SQL ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="2caf8-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>

<span data-ttu-id="2caf8-149">Po dokončení průvodce model EDM (Entity Data Model) se otevře Návrhář model EDM (Entity Data Model).</span><span class="sxs-lookup"><span data-stu-id="2caf8-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="2caf8-150">Návrhář by měl zobrazit entitu filmy (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="2caf8-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="2caf8-151">[![návrháře model EDM (Entity Data Model)](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2caf8-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="2caf8-152">**Obrázek 02**: Návrhář model EDM (Entity Data Model) ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="2caf8-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>

<span data-ttu-id="2caf8-153">Než budeme pokračovat, musíme udělat jednu změnu.</span><span class="sxs-lookup"><span data-stu-id="2caf8-153">We need to make one change before we continue.</span></span> <span data-ttu-id="2caf8-154">Průvodce data entity vygeneruje třídu modelu s názvem *filmy* , která představuje tabulku databáze filmů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="2caf8-155">Vzhledem k tomu, že použijeme třídu filmů k reprezentování konkrétního filmu, musíme upravit název třídy tak, aby se místo *filmů* použil *film* (číslo v čísle místo plural).</span><span class="sxs-lookup"><span data-stu-id="2caf8-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="2caf8-156">Dvakrát klikněte na název třídy na návrhové ploše a změňte název třídy z filmů na film.</span><span class="sxs-lookup"><span data-stu-id="2caf8-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="2caf8-157">Po provedení této změny klikněte na tlačítko **Uložit** (ikona disketové jednotky) a vygenerujte třídu video.</span><span class="sxs-lookup"><span data-stu-id="2caf8-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="2caf8-158">Vytvoření kontroleru filmů</span><span class="sxs-lookup"><span data-stu-id="2caf8-158">Create the Movies Controller</span></span>

<span data-ttu-id="2caf8-159">Teď, když máme způsob reprezentace našich záznamů v databázi, můžeme vytvořit kontroler, který vrátí kolekci filmů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="2caf8-160">V okně Visual Studio Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers a vyberte možnost nabídky **Přidat, kontroler** (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="2caf8-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="2caf8-161">[![nabídky přidat řadič](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2caf8-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="2caf8-162">**Obrázek 03**: nabídka přidat řadič ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2caf8-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>

<span data-ttu-id="2caf8-163">Po zobrazení dialogového okna **Přidat řadič** zadejte název kontroleru MovieController (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="2caf8-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="2caf8-164">Kliknutím na tlačítko **Přidat** přidejte nový kontroler.</span><span class="sxs-lookup"><span data-stu-id="2caf8-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="2caf8-165">[![dialogového okna přidat řadič](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2caf8-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="2caf8-166">**Obrázek 04**: dialogové okno Přidat řadič ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="2caf8-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>

<span data-ttu-id="2caf8-167">Musíme Upravit akci index () zpřístupněnou pro kontroler filmů, aby vracela sadu záznamů databáze.</span><span class="sxs-lookup"><span data-stu-id="2caf8-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="2caf8-168">Upravte kontroler tak, aby vypadal jako kontroler v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="2caf8-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="2caf8-169">**Výpis 1 – Controllers\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="2caf8-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="2caf8-170">V seznamu 1 třída MoviesDBEntities slouží k reprezentaci databáze MoviesDB.</span><span class="sxs-lookup"><span data-stu-id="2caf8-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="2caf8-171">Chcete-li použít tuto třídu, je nutné importovat obor názvů MvcApplication1. Models, například:</span><span class="sxs-lookup"><span data-stu-id="2caf8-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="2caf8-172">použití MvcApplication1. Models;</span><span class="sxs-lookup"><span data-stu-id="2caf8-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="2caf8-173">Entity výrazu *. MovieSet. ToList – ()* vrátí sadu všech filmů z tabulky databáze filmů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="2caf8-174">Vytvoření zobrazení</span><span class="sxs-lookup"><span data-stu-id="2caf8-174">Create the View</span></span>

<span data-ttu-id="2caf8-175">Nejjednodušší způsob, jak zobrazit sadu databázových záznamů v tabulce HTML, je využít výhody generování uživatelského rozhraní, které poskytuje Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2caf8-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="2caf8-176">Sestavte aplikaci výběrem možnosti nabídky **sestavení, řešení sestavení**.</span><span class="sxs-lookup"><span data-stu-id="2caf8-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="2caf8-177">Před otevřením dialogového okna **Přidat zobrazení** nebo z vašich datových tříd se v dialogovém okně nezobrazují vaše aplikace.</span><span class="sxs-lookup"><span data-stu-id="2caf8-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="2caf8-178">Klikněte pravým tlačítkem myši na akci index () a vyberte možnost nabídky **Přidat zobrazení** (viz obrázek 5).</span><span class="sxs-lookup"><span data-stu-id="2caf8-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="2caf8-179">[![přidání zobrazení](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2caf8-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="2caf8-180">**Obrázek 05**: Přidání zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="2caf8-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>

<span data-ttu-id="2caf8-181">V dialogovém okně **Přidat zobrazení** zaškrtněte políčko **vytvořit zobrazení silného typu**.</span><span class="sxs-lookup"><span data-stu-id="2caf8-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="2caf8-182">Jako **třídu zobrazení dat**vyberte třídu filmů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="2caf8-183">Vyberte možnost *seznam* jako **obsah zobrazení** (viz obrázek 6).</span><span class="sxs-lookup"><span data-stu-id="2caf8-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="2caf8-184">Výběrem těchto možností se vytvoří zobrazení se silným typem, které zobrazí seznam filmů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="2caf8-185">[![dialogového okna Přidat zobrazení](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2caf8-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="2caf8-186">**Obrázek 6**: dialogové okno Přidat zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="2caf8-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>

<span data-ttu-id="2caf8-187">Po kliknutí na tlačítko **Přidat** se zobrazení v seznamu 2 vygeneruje automaticky.</span><span class="sxs-lookup"><span data-stu-id="2caf8-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="2caf8-188">Toto zobrazení obsahuje kód potřebný k iterování v kolekci filmů a zobrazení všech vlastností filmu.</span><span class="sxs-lookup"><span data-stu-id="2caf8-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="2caf8-189">**Výpis 2 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="2caf8-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="2caf8-190">Aplikaci můžete spustit výběrem možnosti nabídky **ladění, spustit ladění** (nebo stisknutím klávesy F5).</span><span class="sxs-lookup"><span data-stu-id="2caf8-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="2caf8-191">Spuštění aplikace spustí aplikaci Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="2caf8-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="2caf8-192">Pokud přejdete na adresu URL/Movie, uvidíte stránku na obrázku 7.</span><span class="sxs-lookup"><span data-stu-id="2caf8-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="2caf8-193">[![tabulce filmů](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2caf8-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="2caf8-194">**Obrázek 07**: tabulka filmů ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="2caf8-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>

<span data-ttu-id="2caf8-195">Pokud se vám nezobrazují žádné informace o vzhledu mřížky záznamů databáze na obrázku 7, můžete jednoduše upravit zobrazení indexu.</span><span class="sxs-lookup"><span data-stu-id="2caf8-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="2caf8-196">Můžete například změnit hlavičku *DateReleased* na *Datum vydání* úpravou zobrazení index.</span><span class="sxs-lookup"><span data-stu-id="2caf8-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="2caf8-197">Vytvoření šablony s částečnou</span><span class="sxs-lookup"><span data-stu-id="2caf8-197">Create a Template with a Partial</span></span>

<span data-ttu-id="2caf8-198">Pokud se zobrazení příliš komplikované, je vhodné začít přerušit zobrazení na částečný.</span><span class="sxs-lookup"><span data-stu-id="2caf8-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="2caf8-199">Použití částečně usnadňuje pochopení a udržování vašich zobrazení.</span><span class="sxs-lookup"><span data-stu-id="2caf8-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="2caf8-200">Vytvoříme částečně, kterou můžeme použít jako šablonu k formátování každého záznamu filmové databáze.</span><span class="sxs-lookup"><span data-stu-id="2caf8-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="2caf8-201">Pomocí těchto kroků můžete vytvořit částečnou:</span><span class="sxs-lookup"><span data-stu-id="2caf8-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="2caf8-202">Klikněte pravým tlačítkem na složku Views\Movie a vyberte možnost nabídky **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="2caf8-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="2caf8-203">Zaškrtněte políčko s názvem *vytvořit částečné zobrazení (. ascx)* .</span><span class="sxs-lookup"><span data-stu-id="2caf8-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="2caf8-204">Pojmenujte částečnou *MovieTemplate*.</span><span class="sxs-lookup"><span data-stu-id="2caf8-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="2caf8-205">Zaškrtněte políčko s názvem **vytvořit zobrazení silného typu**.</span><span class="sxs-lookup"><span data-stu-id="2caf8-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="2caf8-206">Jako *třídu zobrazení dat*vyberte video.</span><span class="sxs-lookup"><span data-stu-id="2caf8-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="2caf8-207">Jako *zobrazení obsahu*vyberte prázdné.</span><span class="sxs-lookup"><span data-stu-id="2caf8-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="2caf8-208">Kliknutím na tlačítko **Přidat** přidáte do projektu částečnou možnost.</span><span class="sxs-lookup"><span data-stu-id="2caf8-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="2caf8-209">Po dokončení těchto kroků upravte MovieTemplate částečně tak, aby vypadaly jako v seznamu 3.</span><span class="sxs-lookup"><span data-stu-id="2caf8-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="2caf8-210">**Výpis 3 – Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="2caf8-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="2caf8-211">Částečně v seznamu 3 obsahuje šablonu pro jeden řádek záznamů.</span><span class="sxs-lookup"><span data-stu-id="2caf8-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="2caf8-212">Změněné zobrazení indexu v seznamu 4 používá částečnou MovieTemplate.</span><span class="sxs-lookup"><span data-stu-id="2caf8-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="2caf8-213">**Výpis 4 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="2caf8-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="2caf8-214">Zobrazení v seznamu 4 obsahuje smyčku foreach, která prochází všemi filmy.</span><span class="sxs-lookup"><span data-stu-id="2caf8-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="2caf8-215">Pro každý film se k naformátování videa používá částečná MovieTemplate.</span><span class="sxs-lookup"><span data-stu-id="2caf8-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="2caf8-216">MovieTemplate je vykreslen voláním pomocné metody RenderPartial ().</span><span class="sxs-lookup"><span data-stu-id="2caf8-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="2caf8-217">Změněné zobrazení indexu vykreslí velmi stejnou tabulku HTML záznamů databáze.</span><span class="sxs-lookup"><span data-stu-id="2caf8-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="2caf8-218">Zobrazení se ale významně zjednodušilo.</span><span class="sxs-lookup"><span data-stu-id="2caf8-218">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="2caf8-219">Metoda RenderPartial () je odlišná od většiny ostatních pomocných metod, protože nevrací řetězec.</span><span class="sxs-lookup"><span data-stu-id="2caf8-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="2caf8-220">Proto je nutné volat metodu RenderPartial () pomocí &lt;% HTML. RenderPartial (); %&gt; místo &lt;% = HTML. RenderPartial (); %&gt;.</span><span class="sxs-lookup"><span data-stu-id="2caf8-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="2caf8-221">Souhrn</span><span class="sxs-lookup"><span data-stu-id="2caf8-221">Summary</span></span>

<span data-ttu-id="2caf8-222">Cílem tohoto kurzu bylo vysvětlit, jak můžete zobrazit sadu záznamů databáze v tabulce HTML.</span><span class="sxs-lookup"><span data-stu-id="2caf8-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="2caf8-223">Nejdřív jste zjistili, jak vrátit sadu záznamů databáze z akce kontroleru tím, že využijete výhod Entity Framework Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="2caf8-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="2caf8-224">Dále jste zjistili, jak používat generování uživatelského rozhraní sady Visual Studio k vygenerování zobrazení, které automaticky zobrazuje kolekci položek.</span><span class="sxs-lookup"><span data-stu-id="2caf8-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="2caf8-225">Nakonec jste zjistili, jak zjednodušit zobrazení využitím částečného.</span><span class="sxs-lookup"><span data-stu-id="2caf8-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="2caf8-226">Zjistili jste, jak použít částečný jako šablonu, abyste mohli naformátovat každý záznam v databázi.</span><span class="sxs-lookup"><span data-stu-id="2caf8-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2caf8-227">[Předchozí](creating-model-classes-with-linq-to-sql-cs.md)
> [Další](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="2caf8-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>
