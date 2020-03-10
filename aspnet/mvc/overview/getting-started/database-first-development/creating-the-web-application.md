---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'Kurz: Vytvoření webové aplikace a datových modelů pro EF Database First pomocí ASP.NET MVC'
description: Tento kurz se zaměřuje na vytvoření webové aplikace a generování datových modelů založených na vašich databázových tabulkách.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616268"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="6d9a9-103">Kurz: Vytvoření webové aplikace a datových modelů pro EF Database First pomocí ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="6d9a9-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="6d9a9-104">Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="6d9a9-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="6d9a9-106">Generovaný kód odpovídá sloupcům v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="6d9a9-107">Tento kurz se zaměřuje na vytvoření webové aplikace a generování datových modelů založených na vašich databázových tabulkách.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="6d9a9-108">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="6d9a9-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d9a9-109">Vytvoření webové aplikace v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d9a9-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="6d9a9-110">Generování modelů</span><span class="sxs-lookup"><span data-stu-id="6d9a9-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d9a9-111">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="6d9a9-111">Prerequisites</span></span>

* [<span data-ttu-id="6d9a9-112">Začínáme s Entity Framework 6 Database First pomocí MVC 5</span><span class="sxs-lookup"><span data-stu-id="6d9a9-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="6d9a9-113">Vytvoření webové aplikace v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d9a9-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="6d9a9-114">V novém řešení nebo stejném řešení jako databázový projekt vytvořte v aplikaci Visual Studio nový projekt a vyberte šablonu **webové aplikace ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="6d9a9-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="6d9a9-115">Pojmenujte projekt **ContosoSite**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-115">Name the project **ContosoSite**.</span></span>

![vytvořit projekt](creating-the-web-application/_static/image1.png)

<span data-ttu-id="6d9a9-117">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-117">Click **OK**.</span></span>

<span data-ttu-id="6d9a9-118">V okně Nový projekt ASP.NET vyberte šablonu **MVC** .</span><span class="sxs-lookup"><span data-stu-id="6d9a9-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="6d9a9-119">Nyní můžete zrušit výběr možnosti **hostitel v cloudu** , protože budete aplikaci nasazovat do cloudu později.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="6d9a9-120">Kliknutím na tlačítko **OK** vytvořte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="6d9a9-121">Projekt se vytvoří s výchozími soubory a složkami.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="6d9a9-122">V tomto kurzu budete používat Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="6d9a9-123">V projektu můžete pomocí okna spravovat balíčky NuGet dvakrát kontrolovat verzi Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="6d9a9-124">V případě potřeby aktualizujte svou verzi Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-124">If necessary, update your version of Entity Framework.</span></span>

![Zobrazit verzi](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="6d9a9-126">Generování modelů</span><span class="sxs-lookup"><span data-stu-id="6d9a9-126">Generate the models</span></span>

<span data-ttu-id="6d9a9-127">Nyní budete vytvářet Entity Framework modely z databázových tabulek.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="6d9a9-128">Tyto modely jsou třídy, které použijete pro práci s daty.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="6d9a9-129">Každý model zrcadlí tabulku v databázi a obsahuje vlastnosti, které odpovídají sloupcům v tabulce.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="6d9a9-130">Klikněte pravým tlačítkem na složku **modely** a vyberte položku **Přidat** a **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="6d9a9-131">V okně Přidat novou položku vyberte v levém podokně **data** a **ADO.NET model EDM (Entity Data Model)** z možností v prostředním podokně.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="6d9a9-132">Pojmenujte nový soubor modelu **ContosoModel**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="6d9a9-133">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-133">Click **Add**.</span></span>

<span data-ttu-id="6d9a9-134">V průvodci model EDM (Entity Data Model) vyberte **EF Designer z databáze**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="6d9a9-135">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-135">Click **Next**.</span></span>

<span data-ttu-id="6d9a9-136">Pokud máte databázová připojení definovaná v rámci vašeho vývojového prostředí, může se stát, že jedno z těchto připojení je předem vybrané.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="6d9a9-137">Chcete však vytvořit nové připojení k databázi, kterou jste vytvořili v první části tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="6d9a9-138">Klikněte na tlačítko **nové připojení** .</span><span class="sxs-lookup"><span data-stu-id="6d9a9-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="6d9a9-139">V okno Vlastnosti připojení zadejte název místního serveru, na kterém byla databáze vytvořena (v tomto případě **(LocalDB) \ProjectsV13**).</span><span class="sxs-lookup"><span data-stu-id="6d9a9-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="6d9a9-140">Po zadání názvu serveru vyberte ContosoUniversityData z dostupných databází.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![nastavit vlastnosti připojení](creating-the-web-application/_static/image8.png)

<span data-ttu-id="6d9a9-142">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-142">Click **OK**.</span></span>

<span data-ttu-id="6d9a9-143">Nyní jsou zobrazeny správné vlastnosti připojení.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="6d9a9-144">Můžete použít výchozí název pro připojení v souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="6d9a9-145">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-145">Click **Next**.</span></span>

<span data-ttu-id="6d9a9-146">Vyberte nejnovější verzi Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="6d9a9-147">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-147">Click **Next**.</span></span>

<span data-ttu-id="6d9a9-148">Vyberte **tabulky** a vygenerujte modely pro všechny tři tabulky.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="6d9a9-149">Klikněte na **Finish** (Dokončit).</span><span class="sxs-lookup"><span data-stu-id="6d9a9-149">Click **Finish**.</span></span>

<span data-ttu-id="6d9a9-150">Pokud se zobrazí upozornění zabezpečení, vyberte **OK** a pokračujte v práci s šablonou.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="6d9a9-151">Modely jsou generovány z tabulek databáze a zobrazí se diagram, který zobrazuje vlastnosti a vztahy mezi tabulkami.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![Diagram modelu](creating-the-web-application/_static/image11.png)

<span data-ttu-id="6d9a9-153">Složka modely nyní obsahuje mnoho nových souborů souvisejících s modely, které byly vygenerovány z databáze.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="6d9a9-154">Soubor **ContosoModel.Context.cs** obsahuje třídu, která je odvozena od třídy **DbContext** , a poskytuje vlastnost pro každou třídu modelu, která odpovídá databázové tabulce.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="6d9a9-155">Soubory **Course.cs**, **Enrollment.cs**a **student.cs** obsahují třídy modelů, které reprezentují tabulky databáze.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="6d9a9-156">Při práci s generováním uživatelského rozhraní použijete třídu Context a třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="6d9a9-157">Než budete pokračovat v tomto kurzu, sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="6d9a9-158">V další části vygenerujete kód založený na datových modelech, ale tento oddíl nebude fungovat, pokud projekt nebyl sestaven.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d9a9-159">Další kroky</span><span class="sxs-lookup"><span data-stu-id="6d9a9-159">Next steps</span></span>

<span data-ttu-id="6d9a9-160">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="6d9a9-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d9a9-161">Vytvořená webová aplikace v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6d9a9-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="6d9a9-162">Generované modely</span><span class="sxs-lookup"><span data-stu-id="6d9a9-162">Generated the models</span></span>

<span data-ttu-id="6d9a9-163">Přejděte k dalšímu kurzu, kde se dozvíte, jak vytvořit generovaný kód na základě datových modelů.</span><span class="sxs-lookup"><span data-stu-id="6d9a9-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6d9a9-164">Generování zobrazení</span><span class="sxs-lookup"><span data-stu-id="6d9a9-164">Generating views</span></span>](generating-views.md)
