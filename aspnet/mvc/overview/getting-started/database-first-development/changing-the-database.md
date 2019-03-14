---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'Kurz: Změnit databázi pro EF Database First s ASP.NET MVC aplikace'
description: Tento kurz se zaměřuje na provádět aktualizaci struktura databáze změny a šíření tuto změnu v rámci webové aplikace.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070237"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="3e2f6-103">Kurz: Změnit databázi pro EF Database First s ASP.NET MVC aplikace</span><span class="sxs-lookup"><span data-stu-id="3e2f6-103">Tutorial: Change the database for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="3e2f6-104">Pomocí generování uživatelského rozhraní ASP.NET, MVC a Entity Framework, můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="3e2f6-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který umožňuje uživatelům zobrazit, upravit, vytvořit a odstranit data, která se nachází v databázové tabulce.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="3e2f6-106">Generovaný kód odpovídá sloupců v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="3e2f6-107">Tento kurz se zaměřuje na provádět aktualizaci struktura databáze změny a šíření tuto změnu v rámci webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-107">This tutorial focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>

<span data-ttu-id="3e2f6-108">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="3e2f6-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e2f6-109">Přidat sloupec</span><span class="sxs-lookup"><span data-stu-id="3e2f6-109">Add a column</span></span>
> * <span data-ttu-id="3e2f6-110">Přidat vlastnost do zobrazení</span><span class="sxs-lookup"><span data-stu-id="3e2f6-110">Add the property to the views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e2f6-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3e2f6-111">Prerequisites</span></span>

* [<span data-ttu-id="3e2f6-112">Generování zobrazení</span><span class="sxs-lookup"><span data-stu-id="3e2f6-112">Generating views</span></span>](generating-views.md)

## <a name="add-a-column"></a><span data-ttu-id="3e2f6-113">Přidat sloupec</span><span class="sxs-lookup"><span data-stu-id="3e2f6-113">Add a column</span></span>

<span data-ttu-id="3e2f6-114">Při aktualizaci struktury tabulky v databázi, je potřeba zajistit, že vaše změna rozšířena na datový model, zobrazení a kontroler.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-114">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="3e2f6-115">Pro účely tohoto kurzu přidáte nový sloupec do tabulky Student k zaznamenání prostřední jméno studenta.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-115">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="3e2f6-116">Chcete-li přidat tento sloupec, otevřete projekt databáze a otevřete soubor Student.sql.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-116">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="3e2f6-117">Pomocí návrháře nebo kód T-SQL, přidejte sloupec s názvem **MiddleName** , který je NVARCHAR(50) a povoluje hodnoty NULL.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-117">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

<span data-ttu-id="3e2f6-118">Nasaďte tuto změnu do místní databáze spuštěním projektu databáze (nebo F5).</span><span class="sxs-lookup"><span data-stu-id="3e2f6-118">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="3e2f6-119">Nové pole se přidá do tabulky.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-119">The new field is added to the table.</span></span> <span data-ttu-id="3e2f6-120">Pokud v Průzkumníku objektů SQL serveru ji nevidíte, klikněte na tlačítko Aktualizovat v podokně.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-120">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![Zobrazit nový sloupec](changing-the-database/_static/image2.png)

<span data-ttu-id="3e2f6-122">Nový sloupec existuje v tabulce databáze, ale neexistuje momentálně ve třídě datového modelu.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-122">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="3e2f6-123">Je nutné aktualizovat modelu, který má obsahovat nový sloupec.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-123">You must update the model to include your new column.</span></span> <span data-ttu-id="3e2f6-124">V **modely** složku, otevřete **ContosoModel.edmx** soubor k zobrazení diagramu modelu.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-124">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="3e2f6-125">Všimněte si, že Student model neobsahuje vlastnost MiddleName.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-125">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="3e2f6-126">Klikněte pravým tlačítkem kamkoli na návrhové ploše a vyberte **aktualizace modelů z databáze**.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-126">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

<span data-ttu-id="3e2f6-127">V Průvodci aktualizacemi, vyberte **aktualizovat** kartu a potom vyberte **tabulky** > **dbo** > **Student**.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-127">In the Update Wizard, select the **Refresh** tab and then select **Tables** > **dbo** > **Student**.</span></span> <span data-ttu-id="3e2f6-128">Klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-128">Click **Finish**.</span></span>

<span data-ttu-id="3e2f6-129">Po dokončení procesu aktualizace zahrnuje nový databázový diagram **MiddleName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="3e2f6-130">Uložit **ContosoModel.edmx** souboru.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="3e2f6-131">Je nutné uložit tento soubor pro novou vlastnost mají být předány **Student.cs** třídy.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="3e2f6-132">Teď jste aktualizovali databáze a modelu.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="3e2f6-133">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-133">Build the solution.</span></span>

## <a name="add-the-property-to-the-views"></a><span data-ttu-id="3e2f6-134">Přidat vlastnost do zobrazení</span><span class="sxs-lookup"><span data-stu-id="3e2f6-134">Add the property to the views</span></span>

<span data-ttu-id="3e2f6-135">Bohužel zobrazení stále neobsahují nové vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-135">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="3e2f6-136">Chcete-li aktualizovat zobrazení máte dvě možnosti – můžete znovu vygenerovat zobrazení tak, že znovu přidáte generování uživatelského rozhraní pro třídu Student nebo můžete ručně přidat nové vlastnosti pro stávající zobrazení.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-136">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="3e2f6-137">V tomto kurzu přidáte základní kostry aplikace znovu vzhledem k tomu, že všechny vlastní změny nebyla provedena pro automaticky generované zobrazení.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-137">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="3e2f6-138">Můžete zvážit, když změny provedené zobrazení a nechcete, aby tyto změny přijít o ručním přidání vlastnost.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-138">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="3e2f6-139">Aby se zajistilo zobrazení jsou znovu vytvořena, odstraňte **studenty** ve složce **zobrazení**a odstranit **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-139">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="3e2f6-140">Klikněte pravým tlačítkem na **řadiče** složky a přidat generování uživatelského rozhraní pro **Student** modelu.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-140">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="3e2f6-141">Znovu, název kontroleru **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-141">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="3e2f6-142">Vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-142">Select **Add**.</span></span>

<span data-ttu-id="3e2f6-143">Znovu sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-143">Build the solution again.</span></span> <span data-ttu-id="3e2f6-144">Zobrazení nyní obsahovat vlastnost MiddleName.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-144">The views now contain the MiddleName property.</span></span>

![Zobrazit křestní jméno](changing-the-database/_static/image5.png)

## <a name="next-steps"></a><span data-ttu-id="3e2f6-146">Další kroky</span><span class="sxs-lookup"><span data-stu-id="3e2f6-146">Next steps</span></span>

<span data-ttu-id="3e2f6-147">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="3e2f6-147">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e2f6-148">Přidat sloupec</span><span class="sxs-lookup"><span data-stu-id="3e2f6-148">Added a column</span></span>
> * <span data-ttu-id="3e2f6-149">Přidat vlastnost do zobrazení</span><span class="sxs-lookup"><span data-stu-id="3e2f6-149">Added the property to the views</span></span>

<span data-ttu-id="3e2f6-150">Přejděte k dalšímu kurzu, přečtěte si, jak přizpůsobit zobrazení k zobrazení podrobností o záznamu studentů.</span><span class="sxs-lookup"><span data-stu-id="3e2f6-150">Advance to the next tutorial to learn how to customize the view for showing details about a student record.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3e2f6-151">Přizpůsobení zobrazení</span><span class="sxs-lookup"><span data-stu-id="3e2f6-151">Customize a view</span></span>](customizing-a-view.md)