---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'Kurz: Změna databáze pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na zajištění aktualizace struktury databáze a rozšíření této změny v rámci webové aplikace.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616261"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="3102f-103">Kurz: Změna databáze pro EF Database First pomocí aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="3102f-103">Tutorial: Change the database for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="3102f-104">Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="3102f-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="3102f-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="3102f-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="3102f-106">Generovaný kód odpovídá sloupcům v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="3102f-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="3102f-107">Tento kurz se zaměřuje na zajištění aktualizace struktury databáze a rozšíření této změny v rámci webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="3102f-107">This tutorial focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>

<span data-ttu-id="3102f-108">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="3102f-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3102f-109">Přidání sloupce</span><span class="sxs-lookup"><span data-stu-id="3102f-109">Add a column</span></span>
> * <span data-ttu-id="3102f-110">Přidat vlastnost do zobrazení</span><span class="sxs-lookup"><span data-stu-id="3102f-110">Add the property to the views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3102f-111">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="3102f-111">Prerequisites</span></span>

* [<span data-ttu-id="3102f-112">Generování zobrazení</span><span class="sxs-lookup"><span data-stu-id="3102f-112">Generating views</span></span>](generating-views.md)

## <a name="add-a-column"></a><span data-ttu-id="3102f-113">Přidání sloupce</span><span class="sxs-lookup"><span data-stu-id="3102f-113">Add a column</span></span>

<span data-ttu-id="3102f-114">Pokud aktualizujete strukturu tabulky v databázi, je nutné zajistit, aby se vaše změna rozšířila na datový model, zobrazení a kontroler.</span><span class="sxs-lookup"><span data-stu-id="3102f-114">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="3102f-115">Pro účely tohoto kurzu přidáte do tabulky student nový sloupec, kde poznamenejte prostřední jméno studenta.</span><span class="sxs-lookup"><span data-stu-id="3102f-115">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="3102f-116">Chcete-li přidat tento sloupec, otevřete databázový projekt a otevřete soubor student. SQL.</span><span class="sxs-lookup"><span data-stu-id="3102f-116">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="3102f-117">Pomocí návrháře nebo kódu T-SQL přidejte sloupec s názvem **MiddleName** , který je nvarchar (50) a povoluje hodnoty null.</span><span class="sxs-lookup"><span data-stu-id="3102f-117">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

<span data-ttu-id="3102f-118">Tuto změnu nasaďte do místní databáze spuštěním databázového projektu (nebo F5).</span><span class="sxs-lookup"><span data-stu-id="3102f-118">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="3102f-119">Nové pole je přidáno do tabulky.</span><span class="sxs-lookup"><span data-stu-id="3102f-119">The new field is added to the table.</span></span> <span data-ttu-id="3102f-120">Pokud ji v Průzkumník objektů systému SQL Server nevidíte, klikněte na tlačítko Aktualizovat v podokně.</span><span class="sxs-lookup"><span data-stu-id="3102f-120">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![Zobrazit nový sloupec](changing-the-database/_static/image2.png)

<span data-ttu-id="3102f-122">Nový sloupec v databázové tabulce existuje, ale v současné době neexistuje ve třídě datového modelu.</span><span class="sxs-lookup"><span data-stu-id="3102f-122">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="3102f-123">Model musíte aktualizovat tak, aby obsahoval nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="3102f-123">You must update the model to include your new column.</span></span> <span data-ttu-id="3102f-124">Ve složce **modely** otevřete soubor **ContosoModel. edmx** pro zobrazení diagramu modelu.</span><span class="sxs-lookup"><span data-stu-id="3102f-124">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="3102f-125">Všimněte si, že model student neobsahuje vlastnost MiddleName.</span><span class="sxs-lookup"><span data-stu-id="3102f-125">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="3102f-126">Klikněte pravým tlačítkem myši kamkoli na návrhovou plochu a vyberte **aktualizovat model z databáze**.</span><span class="sxs-lookup"><span data-stu-id="3102f-126">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

<span data-ttu-id="3102f-127">V Průvodci aktualizací vyberte kartu **aktualizovat** a pak vyberte **tabulky** > **dbo** > **student**.</span><span class="sxs-lookup"><span data-stu-id="3102f-127">In the Update Wizard, select the **Refresh** tab and then select **Tables** > **dbo** > **Student**.</span></span> <span data-ttu-id="3102f-128">Klikněte na **Finish** (Dokončit).</span><span class="sxs-lookup"><span data-stu-id="3102f-128">Click **Finish**.</span></span>

<span data-ttu-id="3102f-129">Po dokončení procesu aktualizace obsahuje databázový diagram novou vlastnost **MiddleName** .</span><span class="sxs-lookup"><span data-stu-id="3102f-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="3102f-130">Uložte soubor **ContosoModel. edmx** .</span><span class="sxs-lookup"><span data-stu-id="3102f-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="3102f-131">Tento soubor musíte uložit, aby se nová vlastnost rozšířila na třídu **student.cs** .</span><span class="sxs-lookup"><span data-stu-id="3102f-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="3102f-132">Nyní jste aktualizovali databázi a model.</span><span class="sxs-lookup"><span data-stu-id="3102f-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="3102f-133">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="3102f-133">Build the solution.</span></span>

## <a name="add-the-property-to-the-views"></a><span data-ttu-id="3102f-134">Přidat vlastnost do zobrazení</span><span class="sxs-lookup"><span data-stu-id="3102f-134">Add the property to the views</span></span>

<span data-ttu-id="3102f-135">Zobrazení však stále neobsahují novou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="3102f-135">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="3102f-136">Chcete-li aktualizovat zobrazení, máte dvě možnosti – můžete buď znovu vygenerovat zobrazení, a to tak, že znovu přidáte generování uživatelského rozhraní pro třídu studenta, nebo můžete do stávajících zobrazení přidat novou vlastnost ručně.</span><span class="sxs-lookup"><span data-stu-id="3102f-136">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="3102f-137">V tomto kurzu znovu přidáte generování uživatelského rozhraní, protože jste neudělali žádné přizpůsobené změny v automaticky generovaných zobrazeních.</span><span class="sxs-lookup"><span data-stu-id="3102f-137">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="3102f-138">Můžete zvážit ruční přidání vlastnosti, když jste provedli změny zobrazení a nechcete přijít o tyto změny.</span><span class="sxs-lookup"><span data-stu-id="3102f-138">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="3102f-139">Chcete-li zajistit opětovné vytvoření zobrazení, odstraňte složku **studenti** v **zobrazeních**a odstraňte **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="3102f-139">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="3102f-140">Pak klikněte pravým tlačítkem na složku **Controllers** a přidejte pro model **studenta** generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3102f-140">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="3102f-141">Znovu pojmenujte kontroler **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="3102f-141">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="3102f-142">Vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="3102f-142">Select **Add**.</span></span>

<span data-ttu-id="3102f-143">Znovu sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="3102f-143">Build the solution again.</span></span> <span data-ttu-id="3102f-144">Zobrazení teď obsahují vlastnost MiddleName.</span><span class="sxs-lookup"><span data-stu-id="3102f-144">The views now contain the MiddleName property.</span></span>

![Zobrazit prostřední jméno](changing-the-database/_static/image5.png)

## <a name="next-steps"></a><span data-ttu-id="3102f-146">Další kroky</span><span class="sxs-lookup"><span data-stu-id="3102f-146">Next steps</span></span>

<span data-ttu-id="3102f-147">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="3102f-147">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3102f-148">Přidání sloupce</span><span class="sxs-lookup"><span data-stu-id="3102f-148">Added a column</span></span>
> * <span data-ttu-id="3102f-149">Přidání vlastnosti do zobrazení</span><span class="sxs-lookup"><span data-stu-id="3102f-149">Added the property to the views</span></span>

<span data-ttu-id="3102f-150">Přejděte k dalšímu kurzu, kde se dozvíte, jak přizpůsobit zobrazení pro zobrazení podrobností o záznamu studenta.</span><span class="sxs-lookup"><span data-stu-id="3102f-150">Advance to the next tutorial to learn how to customize the view for showing details about a student record.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3102f-151">Přizpůsobení zobrazení</span><span class="sxs-lookup"><span data-stu-id="3102f-151">Customize a view</span></span>](customizing-a-view.md)