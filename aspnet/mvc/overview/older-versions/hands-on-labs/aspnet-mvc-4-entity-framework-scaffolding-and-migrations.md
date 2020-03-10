---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework generování a migrace | Microsoft Docs
author: rick-anderson
description: Pokud jste obeznámeni s metodami kontroleru ASP.NET MVC 4 nebo jste dokončili &quot;pomocníky, formuláře a ověřování&quot; praktické cvičení, měli byste si být vědomi...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598901"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="fc93e-103">ASP.NET MVC 4 – generování uživatelského rozhraní a migrace sady Entity Framework</span><span class="sxs-lookup"><span data-stu-id="fc93e-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="fc93e-104">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="fc93e-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="fc93e-105">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="fc93e-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="fc93e-106">Pokud jste obeznámeni s metodami kontroleru ASP.NET MVC 4 nebo jste dokončili &quot;pomocníky, formuláře a ověřování&quot; praktických cvičeních, měli byste si uvědomit, že mnohé z logiky, jak vytvořit, aktualizovat, vypsat a odebrat jakoukoli entitu dat, se v rámci aplikace opakují.</span><span class="sxs-lookup"><span data-stu-id="fc93e-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="fc93e-107">Nezmiňujete si, že pokud má váš model několik tříd pro manipulaci, budete pravděpodobně strávit značnou dobu psaní příspěvku a metody GET pro každou entitu a také pro každé zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fc93e-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="fc93e-108">V tomto testovacím prostředí se naučíte, jak pomocí rozhraní ASP.NET MVC 4 automaticky vygenerovat základní hodnoty pro CRUD vaší aplikace (vytvoření, čtení, aktualizace a odstranění).</span><span class="sxs-lookup"><span data-stu-id="fc93e-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="fc93e-109">Od jednoduché třídy modelu a, bez psaní jednoho řádku kódu, vytvoříte kontroler, který bude obsahovat všechny operace CRUD, a také všechna potřebná zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fc93e-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="fc93e-110">Po sestavení a spuštění jednoduchého řešení budete mít vytvořenou databázi aplikace společně s logikou a zobrazeními MVC pro manipulaci s daty.</span><span class="sxs-lookup"><span data-stu-id="fc93e-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="fc93e-111">Kromě toho se dozvíte, jak snadné je použít Entity Framework migrace k provádění aktualizací modelů v celé aplikaci.</span><span class="sxs-lookup"><span data-stu-id="fc93e-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="fc93e-112">Entity Framework migrace vám umožní upravit databázi poté, co se model změnil pomocí jednoduchých kroků.</span><span class="sxs-lookup"><span data-stu-id="fc93e-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="fc93e-113">Díky všem těmto výhodám budete moct vytvářet a udržovat webové aplikace efektivněji a využívat nejnovější funkce ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="fc93e-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="fc93e-114">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Training Kit, která je dostupná v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="fc93e-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="fc93e-115">Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NET MVC 4 Entity Framework generování a migrace](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span><span class="sxs-lookup"><span data-stu-id="fc93e-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="fc93e-116">Cíle</span><span class="sxs-lookup"><span data-stu-id="fc93e-116">Objectives</span></span>

<span data-ttu-id="fc93e-117">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="fc93e-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="fc93e-118">Použijte generování ASP.NET pro operace CRUD v řadičích.</span><span class="sxs-lookup"><span data-stu-id="fc93e-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="fc93e-119">Změňte databázový model pomocí Entity Framework migrace.</span><span class="sxs-lookup"><span data-stu-id="fc93e-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="fc93e-120">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="fc93e-120">Prerequisites</span></span>

<span data-ttu-id="fc93e-121">K dokončení tohoto testovacího prostředí musíte mít následující položky:</span><span class="sxs-lookup"><span data-stu-id="fc93e-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="fc93e-122">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).</span><span class="sxs-lookup"><span data-stu-id="fc93e-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="fc93e-123">Nastavení</span><span class="sxs-lookup"><span data-stu-id="fc93e-123">Setup</span></span>

<span data-ttu-id="fc93e-124">**Instalace fragmentů kódu**</span><span class="sxs-lookup"><span data-stu-id="fc93e-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="fc93e-125">Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fc93e-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="fc93e-126">Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="fc93e-127">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze B: použití fragmentů kódu](#AppendixB)&quot;.</span><span class="sxs-lookup"><span data-stu-id="fc93e-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="fc93e-128">Cvičení</span><span class="sxs-lookup"><span data-stu-id="fc93e-128">Exercises</span></span>

<span data-ttu-id="fc93e-129">Následující cvičení tvoří tuto praktickou laboratoř:</span><span class="sxs-lookup"><span data-stu-id="fc93e-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="fc93e-130">Použití generování ASP.NET MVC 4 s Entity Framework migracemi</span><span class="sxs-lookup"><span data-stu-id="fc93e-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="fc93e-131">K tomuto cvičení doprovázíme **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="fc93e-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="fc93e-132">Pokud potřebujete další nápovědu k práci prostřednictvím tohoto cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="fc93e-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>

<span data-ttu-id="fc93e-133">Odhadovaný čas dokončení tohoto testovacího prostředí: **30 minut**</span><span class="sxs-lookup"><span data-stu-id="fc93e-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="fc93e-134">Cvičení 1: použití generování ASP.NET MVC 4 s Entity Framework migrací</span><span class="sxs-lookup"><span data-stu-id="fc93e-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="fc93e-135">Generování ASP.NET MVC poskytuje rychlý způsob, jak generovat operace CRUD standardizovaným způsobem, a vytvořit tak potřebnou logiku, která vaší aplikaci umožní pracovat s databázovou vrstvou.</span><span class="sxs-lookup"><span data-stu-id="fc93e-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="fc93e-136">V tomto cvičení se dozvíte, jak používat generování ASP.NET MVC 4 s kódem jako první k vytvoření metod CRUD.</span><span class="sxs-lookup"><span data-stu-id="fc93e-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="fc93e-137">Pak se naučíte, jak aktualizovat model pomocí změn v databázi pomocí Entity Framework migrace.</span><span class="sxs-lookup"><span data-stu-id="fc93e-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="fc93e-138">Úloha 1 – Vytvoření nového projektu ASP.NET MVC 4 pomocí generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="fc93e-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="fc93e-139">Pokud ještě není otevřený, spusťte **Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="fc93e-140">Vybrat **soubor | Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-140">Select **File | New Project**.</span></span> <span data-ttu-id="fc93e-141">V dialogovém okně Nový projekt v části **vizuál C# |** V části Web vyberte **webová aplikace ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="fc93e-142">Pojmenujte projekt **MVC4andEFMigrations** a nastavte umístění na složku **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** v tomto testovacím prostředí.</span><span class="sxs-lookup"><span data-stu-id="fc93e-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="fc93e-143">Nastavte **název řešení** na **zahájit** a ověřte, že je zaškrtnuté políčko **vytvořit adresář pro řešení** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="fc93e-144">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-144">Click **OK**.</span></span>

    <span data-ttu-id="fc93e-145">![Nový projekt ASP.NET MVC 4 – dialogové okno](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "Nový projekt ASP.NET MVC 4 – dialogové okno")</span><span class="sxs-lookup"><span data-stu-id="fc93e-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="fc93e-146">*Nový projekt ASP.NET MVC 4 – dialogové okno*</span><span class="sxs-lookup"><span data-stu-id="fc93e-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="fc93e-147">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu **Internetová aplikace** a ujistěte se, že je v nástroji **Razor** vybraný **modul zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="fc93e-148">Projekt vytvoříte kliknutím na **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="fc93e-149">![Nová ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "Nová ASP.NET MVC 4 Internet Application")</span><span class="sxs-lookup"><span data-stu-id="fc93e-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="fc93e-150">*Nová ASP.NET MVC 4 Internet Application*</span><span class="sxs-lookup"><span data-stu-id="fc93e-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="fc93e-151">V Průzkumník řešení klikněte pravým tlačítkem na **modely** a vyberte **Přidat | Třída** pro vytvoření jednoduché třídy Person (POCO).</span><span class="sxs-lookup"><span data-stu-id="fc93e-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="fc93e-152">Pojmenujte **ji a** klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="fc93e-153">Otevřete třídu Person a vložte následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="fc93e-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="fc93e-154">(Fragment kódu – *ASP.NET MVC 4 a migrace Entity Framework – vlastnosti osoby EX1*)</span><span class="sxs-lookup"><span data-stu-id="fc93e-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="fc93e-155">Klikněte na **sestavit | Sestavte řešení** a uložte změny a sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="fc93e-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="fc93e-156">![Sestavování aplikace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Sestavování aplikace")</span><span class="sxs-lookup"><span data-stu-id="fc93e-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="fc93e-157">*Sestavování aplikace*</span><span class="sxs-lookup"><span data-stu-id="fc93e-157">*Building the Application*</span></span>
7. <span data-ttu-id="fc93e-158">V Průzkumník řešení klikněte pravým tlačítkem na složku řadiče a vyberte **Přidat | Kontroler**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="fc93e-159">Pojmenujte kontrolér *PersonController* a dokončete **Možnosti generování uživatelského rozhraní** s následujícími hodnotami.</span><span class="sxs-lookup"><span data-stu-id="fc93e-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="fc93e-160">V rozevíracím seznamu **Šablona** vyberte **kontroler MVC s akcemi čtení/zápisu a zobrazeními pomocí Entity Framework** možnost.</span><span class="sxs-lookup"><span data-stu-id="fc93e-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="fc93e-161">V rozevíracím seznamu **třída modelu** vyberte třídu **Person** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="fc93e-162">V seznamu **Třída kontextu dat** vyberte **&lt;nový kontext dat...&gt;** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="fc93e-163">Vyberte libovolný název a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="fc93e-164">V rozevíracím seznamu **zobrazení** ověřte, zda je vybrána možnost **Razor** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="fc93e-165">![Přidání kontroleru osob s generováním uživatelského rozhraní](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Přidání kontroleru osob s generováním uživatelského rozhraní")</span><span class="sxs-lookup"><span data-stu-id="fc93e-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="fc93e-166">*Přidání kontroleru osob s generováním uživatelského rozhraní*</span><span class="sxs-lookup"><span data-stu-id="fc93e-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="fc93e-167">Kliknutím na **Přidat** vytvořte nový kontroler pro osobu s vytvářením uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="fc93e-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="fc93e-168">Nyní jste vygenerovali akce kontroleru a také zobrazení.</span><span class="sxs-lookup"><span data-stu-id="fc93e-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="fc93e-169">![Po vytvoření kontroleru osoba pomocí generování uživatelského rozhraní](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "Po vytvoření kontroleru osoba pomocí generování uživatelského rozhraní")</span><span class="sxs-lookup"><span data-stu-id="fc93e-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="fc93e-170">*Po vytvoření kontroleru osoba pomocí generování uživatelského rozhraní*</span><span class="sxs-lookup"><span data-stu-id="fc93e-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="fc93e-171">Otevřete třídu **PersonController** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-171">Open **PersonController** class.</span></span> <span data-ttu-id="fc93e-172">Všimněte si, že všechny metody akce CRUD byly vygenerovány automaticky.</span><span class="sxs-lookup"><span data-stu-id="fc93e-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="fc93e-173">![Uvnitř kontroleru osob](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Uvnitř kontroleru osob")</span><span class="sxs-lookup"><span data-stu-id="fc93e-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="fc93e-174">*Uvnitř kontroleru osob*</span><span class="sxs-lookup"><span data-stu-id="fc93e-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="fc93e-175">Úloha 2 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="fc93e-175">Task 2- Running the application</span></span>

<span data-ttu-id="fc93e-176">V tomto okamžiku databáze ještě není vytvořená.</span><span class="sxs-lookup"><span data-stu-id="fc93e-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="fc93e-177">V této úloze budete aplikaci spouštět poprvé a otestujete operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="fc93e-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="fc93e-178">Databáze se vytvoří průběžně s Code First.</span><span class="sxs-lookup"><span data-stu-id="fc93e-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="fc93e-179">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="fc93e-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="fc93e-180">V prohlížeči přidejte **/Person** k adrese URL pro otevření stránky osoba.</span><span class="sxs-lookup"><span data-stu-id="fc93e-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="fc93e-181">![První spuštění aplikace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "První spuštění aplikace")</span><span class="sxs-lookup"><span data-stu-id="fc93e-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="fc93e-182">*Aplikace: první spuštění*</span><span class="sxs-lookup"><span data-stu-id="fc93e-182">*Application: first run*</span></span>
3. <span data-ttu-id="fc93e-183">Teď budete zkoumat stránky osob a testovat operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="fc93e-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="fc93e-184">Kliknutím na **vytvořit novou** přidejte novou osobu.</span><span class="sxs-lookup"><span data-stu-id="fc93e-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="fc93e-185">Zadejte jméno a příjmení a klikněte na **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="fc93e-186">![Přidává se nová osoba.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Přidává se nová osoba.")</span><span class="sxs-lookup"><span data-stu-id="fc93e-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="fc93e-187">*Přidává se nová osoba.*</span><span class="sxs-lookup"><span data-stu-id="fc93e-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="fc93e-188">V seznamu osoby můžete odstranit, upravit nebo přidat položky.</span><span class="sxs-lookup"><span data-stu-id="fc93e-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="fc93e-189">![Seznam osob](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "Seznam osob")</span><span class="sxs-lookup"><span data-stu-id="fc93e-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="fc93e-190">*Seznam osob*</span><span class="sxs-lookup"><span data-stu-id="fc93e-190">*Person list*</span></span>
    3. <span data-ttu-id="fc93e-191">Kliknutím na **Podrobnosti** otevřete podrobnosti o osobě.</span><span class="sxs-lookup"><span data-stu-id="fc93e-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="fc93e-192">![Podrobnosti o osobě](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Podrobnosti o osobě")</span><span class="sxs-lookup"><span data-stu-id="fc93e-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="fc93e-193">*Podrobnosti o osobě*</span><span class="sxs-lookup"><span data-stu-id="fc93e-193">*Person's details*</span></span>
4. <span data-ttu-id="fc93e-194">Zavřete prohlížeč a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fc93e-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="fc93e-195">Všimněte si, že jste vytvořili celou CRUD pro entitu Person v rámci vaší aplikace – z modelu do zobrazení – nemusíte psát jediný řádek kódu!</span><span class="sxs-lookup"><span data-stu-id="fc93e-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="fc93e-196">Úloha 3 – aktualizace databáze pomocí Entity Framework migrace</span><span class="sxs-lookup"><span data-stu-id="fc93e-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="fc93e-197">V této úloze provedete aktualizaci databáze pomocí Entity Framework migrace.</span><span class="sxs-lookup"><span data-stu-id="fc93e-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="fc93e-198">Zjistíte, jak snadné je změnit model a odrážet změny v databázích pomocí funkce Entity Framework migrace.</span><span class="sxs-lookup"><span data-stu-id="fc93e-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="fc93e-199">Otevřete konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="fc93e-199">Open the Package Manager Console.</span></span> <span data-ttu-id="fc93e-200">Vyberte **nástroje** > **správce balíčků NuGet** > **konzole správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-200">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="fc93e-201">V konzole správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fc93e-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="fc93e-202">PMC</span><span class="sxs-lookup"><span data-stu-id="fc93e-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="fc93e-203">![Povolování migrací](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Povolování migrací")</span><span class="sxs-lookup"><span data-stu-id="fc93e-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="fc93e-204">*Povolování migrací*</span><span class="sxs-lookup"><span data-stu-id="fc93e-204">*Enabling migrations*</span></span>

    <span data-ttu-id="fc93e-205">Příkaz Enable-Migration vytvoří složku **migraces** , která obsahuje skript pro inicializaci databáze.</span><span class="sxs-lookup"><span data-stu-id="fc93e-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="fc93e-206">![Složka migrace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Složka migrace")</span><span class="sxs-lookup"><span data-stu-id="fc93e-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="fc93e-207">*Složka migrace*</span><span class="sxs-lookup"><span data-stu-id="fc93e-207">*Migrations folder*</span></span>
3. <span data-ttu-id="fc93e-208">Otevřete soubor **Configuration.cs** ve složce migraces.</span><span class="sxs-lookup"><span data-stu-id="fc93e-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="fc93e-209">Vyhledejte konstruktor třídy a změňte hodnotu **AutomaticMigrationsEnabled** na *true*.</span><span class="sxs-lookup"><span data-stu-id="fc93e-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="fc93e-210">Otevřete třídu Person a přidejte atribut pro prostřední jméno osoby.</span><span class="sxs-lookup"><span data-stu-id="fc93e-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="fc93e-211">Pomocí tohoto nového atributu měníte model.</span><span class="sxs-lookup"><span data-stu-id="fc93e-211">With this new attribute, you are changing the model.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="fc93e-212">Vybrat **Build |** Sestavte řešení v nabídce a sestavte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="fc93e-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="fc93e-213">![Sestavování aplikace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Sestavování aplikace")</span><span class="sxs-lookup"><span data-stu-id="fc93e-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="fc93e-214">*Sestavování aplikace*</span><span class="sxs-lookup"><span data-stu-id="fc93e-214">*Building the application*</span></span>
6. <span data-ttu-id="fc93e-215">V konzole správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fc93e-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="fc93e-216">PMC</span><span class="sxs-lookup"><span data-stu-id="fc93e-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="fc93e-217">Tento příkaz bude hledat změny v datových objektech a následně přidá potřebné příkazy pro úpravu databáze.</span><span class="sxs-lookup"><span data-stu-id="fc93e-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="fc93e-218">![Přidání druhého jména](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Přidání druhého jména")</span><span class="sxs-lookup"><span data-stu-id="fc93e-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="fc93e-219">*Přidání druhého jména*</span><span class="sxs-lookup"><span data-stu-id="fc93e-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="fc93e-220">Volitelné Spuštěním následujícího příkazu můžete vygenerovat skript SQL s rozdílovou aktualizací.</span><span class="sxs-lookup"><span data-stu-id="fc93e-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="fc93e-221">To vám umožní ručně aktualizovat databázi (v tomto případě není nutné), nebo použít změny v jiných databázích:</span><span class="sxs-lookup"><span data-stu-id="fc93e-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="fc93e-222">PMC</span><span class="sxs-lookup"><span data-stu-id="fc93e-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="fc93e-223">![Generování skriptu SQL](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generování skriptu SQL")</span><span class="sxs-lookup"><span data-stu-id="fc93e-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="fc93e-224">*Generování skriptu SQL*</span><span class="sxs-lookup"><span data-stu-id="fc93e-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="fc93e-225">![Aktualizace skriptu SQL](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "Aktualizace skriptu SQL")</span><span class="sxs-lookup"><span data-stu-id="fc93e-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="fc93e-226">*Aktualizace skriptu SQL*</span><span class="sxs-lookup"><span data-stu-id="fc93e-226">*SQL Script update*</span></span>
8. <span data-ttu-id="fc93e-227">V konzole správce balíčků zadejte následující příkaz pro aktualizaci databáze:</span><span class="sxs-lookup"><span data-stu-id="fc93e-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="fc93e-228">PMC</span><span class="sxs-lookup"><span data-stu-id="fc93e-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="fc93e-229">![Aktualizace databáze](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Aktualizace databáze")</span><span class="sxs-lookup"><span data-stu-id="fc93e-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="fc93e-230">*Aktualizace databáze*</span><span class="sxs-lookup"><span data-stu-id="fc93e-230">*Updating the Database*</span></span>

    <span data-ttu-id="fc93e-231">Tím se do tabulky **lidé** přidá sloupec **MiddleName** , který bude odpovídat aktuální definici třídy **Person** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="fc93e-232">Po aktualizaci databáze klikněte pravým tlačítkem na složku kontroleru a vyberte **Přidat | Kontroler** pro přidání řadiče pro fyzickou osobu (dokončeno se stejnými hodnotami)</span><span class="sxs-lookup"><span data-stu-id="fc93e-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="fc93e-233">Tím se aktualizují existující metody a zobrazení přidáním nového atributu.</span><span class="sxs-lookup"><span data-stu-id="fc93e-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="fc93e-234">![Přidání aktualizace kontroleru](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Přidání aktualizace kontroleru")</span><span class="sxs-lookup"><span data-stu-id="fc93e-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="fc93e-235">*Aktualizace kontroleru*</span><span class="sxs-lookup"><span data-stu-id="fc93e-235">*Updating the controller*</span></span>
10. <span data-ttu-id="fc93e-236">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-236">Click **Add**.</span></span> <span data-ttu-id="fc93e-237">Pak vyberte hodnoty **přepsat PersonController.cs** a **přepsat přidružená zobrazení** a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![Přidání ovladače přepsání](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="fc93e-239">*Aktualizace kontroleru*</span><span class="sxs-lookup"><span data-stu-id="fc93e-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="fc93e-240">Task4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="fc93e-240">Task4- Running the application</span></span>

1. <span data-ttu-id="fc93e-241">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="fc93e-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="fc93e-242">Otevřete **/Person**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-242">Open **/Person**.</span></span> <span data-ttu-id="fc93e-243">Všimněte si, že data byla zachována, zatímco byl přidán sloupec prostřední název.</span><span class="sxs-lookup"><span data-stu-id="fc93e-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="fc93e-244">![Druhé jméno přidané](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Druhé jméno přidané")</span><span class="sxs-lookup"><span data-stu-id="fc93e-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="fc93e-245">*Druhé jméno přidané*</span><span class="sxs-lookup"><span data-stu-id="fc93e-245">*Middle Name added*</span></span>
3. <span data-ttu-id="fc93e-246">Pokud kliknete na **Upravit**, budete moct k aktuální osobě přidat prostřední jméno.</span><span class="sxs-lookup"><span data-stu-id="fc93e-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="fc93e-247">![Střední název edice](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Střední název edice")</span><span class="sxs-lookup"><span data-stu-id="fc93e-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="fc93e-248">Souhrn</span><span class="sxs-lookup"><span data-stu-id="fc93e-248">Summary</span></span>

<span data-ttu-id="fc93e-249">V tomto praktickém cvičení jste se dozvěděli o jednoduchých krocích pro vytváření operací CRUD s ASP.NETm generováním uživatelského rozhraní MVC 4 pomocí libovolné třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="fc93e-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="fc93e-250">Pak jste se naučili, jak provést kompletní aktualizaci ve vaší aplikaci – z databáze do zobrazení – pomocí Entity Framework migrace.</span><span class="sxs-lookup"><span data-stu-id="fc93e-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="fc93e-251">Příloha A: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="fc93e-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="fc93e-252">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="fc93e-253">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="fc93e-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="fc93e-254">Přejděte do [ (Nastavení)https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) (Integrace a služby).</span><span class="sxs-lookup"><span data-stu-id="fc93e-254">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="fc93e-255">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="fc93e-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="fc93e-256">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-256">Click on **Install Now**.</span></span> <span data-ttu-id="fc93e-257">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="fc93e-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="fc93e-258">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="fc93e-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="fc93e-259">![Nainstalovat Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="fc93e-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="fc93e-260">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="fc93e-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="fc93e-261">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="fc93e-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="fc93e-263">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="fc93e-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="fc93e-264">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="fc93e-264">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="fc93e-266">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="fc93e-266">*Installation progress*</span></span>
6. <span data-ttu-id="fc93e-267">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-267">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="fc93e-269">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="fc93e-269">*Installation completed*</span></span>
7. <span data-ttu-id="fc93e-270">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="fc93e-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="fc93e-271">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="fc93e-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="fc93e-273">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="fc93e-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="fc93e-274">Příloha B: použití fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="fc93e-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="fc93e-275">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="fc93e-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="fc93e-276">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="fc93e-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="fc93e-277">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="fc93e-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="fc93e-278">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="fc93e-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="fc93e-279">***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="fc93e-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="fc93e-280">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="fc93e-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="fc93e-281">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="fc93e-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="fc93e-282">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="fc93e-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="fc93e-283">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="fc93e-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="fc93e-284">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="fc93e-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="fc93e-285">![Začněte psát název fragmentu.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="fc93e-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="fc93e-286">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="fc93e-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="fc93e-287">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="fc93e-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="fc93e-288">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="fc93e-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="fc93e-289">![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="fc93e-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="fc93e-290">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="fc93e-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="fc93e-291">***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první.</span><span class="sxs-lookup"><span data-stu-id="fc93e-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="fc93e-292">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="fc93e-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="fc93e-293">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="fc93e-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="fc93e-294">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="fc93e-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="fc93e-295">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="fc93e-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="fc93e-296">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="fc93e-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="fc93e-297">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="fc93e-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="fc93e-298">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="fc93e-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
