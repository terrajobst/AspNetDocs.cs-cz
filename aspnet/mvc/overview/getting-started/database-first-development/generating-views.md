---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 'Kurz: generování zobrazení pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na použití generování uživatelského rozhraní ASP.NET k vygenerování řadičů a zobrazení.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616205"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="2b742-103">Kurz: generování zobrazení pro EF Database First pomocí aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="2b742-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="2b742-104">Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="2b742-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="2b742-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="2b742-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="2b742-106">Generovaný kód odpovídá sloupcům v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="2b742-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="2b742-107">Tento kurz se zaměřuje na použití generování uživatelského rozhraní ASP.NET k vygenerování řadičů a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="2b742-107">This tutorial focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="2b742-108">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="2b742-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b742-109">Přidat generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="2b742-109">Add scaffold</span></span>
> * <span data-ttu-id="2b742-110">Přidat odkazy na nová zobrazení</span><span class="sxs-lookup"><span data-stu-id="2b742-110">Add links to new views</span></span>
> * <span data-ttu-id="2b742-111">Zobrazit zobrazení studenta</span><span class="sxs-lookup"><span data-stu-id="2b742-111">Display student views</span></span>
> * <span data-ttu-id="2b742-112">Zobrazit zobrazení pro zápis</span><span class="sxs-lookup"><span data-stu-id="2b742-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="2b742-113">Požadavek</span><span class="sxs-lookup"><span data-stu-id="2b742-113">Prerequisite</span></span>

* [<span data-ttu-id="2b742-114">Vytvoření webové aplikace a datových modelů</span><span class="sxs-lookup"><span data-stu-id="2b742-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="2b742-115">Přidat generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="2b742-115">Add scaffold</span></span>

<span data-ttu-id="2b742-116">Jste připraveni vygenerovat kód, který bude poskytovat standardní operace s daty pro třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="2b742-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="2b742-117">Kód přidáte přidáním položky uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="2b742-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="2b742-118">Existuje mnoho možností pro typ generování uživatelského rozhraní, které můžete přidat; v tomto kurzu bude toto uživatelské rozhraní zahrnovat kontroler a zobrazení, které odpovídají modelům student a registrace, které jste vytvořili v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="2b742-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="2b742-119">Chcete-li zachovat konzistenci projektu, přidejte nový kontroler do složky existující **řadiče** .</span><span class="sxs-lookup"><span data-stu-id="2b742-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="2b742-120">Klikněte pravým tlačítkem na složku **řadiče** a vyberte **Přidat** > **Nová vygenerovaná položka**.</span><span class="sxs-lookup"><span data-stu-id="2b742-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="2b742-121">Pomocí možnosti **Entity Framework vyberte kontroler MVC 5 se zobrazeními** .</span><span class="sxs-lookup"><span data-stu-id="2b742-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="2b742-122">Tato možnost vygeneruje kontroler a zobrazení pro aktualizaci, odstranění, vytváření a zobrazování dat v modelu.</span><span class="sxs-lookup"><span data-stu-id="2b742-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![Přidat kontroler MVC](generating-views/_static/image2.png)

<span data-ttu-id="2b742-124">Vyberte **student (ContosoSite. Models)** pro třídu modelu a vyberte **ContosoUniversityDataEntities (ContosoSite. Models)** pro třídu kontextu.</span><span class="sxs-lookup"><span data-stu-id="2b742-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="2b742-125">Ponechte název kontroleru jako **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="2b742-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="2b742-126">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="2b742-126">Click **Add**.</span></span>

<span data-ttu-id="2b742-127">Pokud se zobrazí chyba, může to být způsobeno tím, že jste projekt nesestavili v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="2b742-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="2b742-128">Pokud ano, zkuste sestavit projekt a pak znovu přidat vygenerované položky.</span><span class="sxs-lookup"><span data-stu-id="2b742-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="2b742-129">Po dokončení procesu generování kódu se zobrazí nový kontroler a zobrazení v **řadičích** a **zobrazeních** projektu > složky **studentů** .</span><span class="sxs-lookup"><span data-stu-id="2b742-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>

<span data-ttu-id="2b742-130">Proveďte stejné kroky znovu, ale přidejte uživatelské rozhraní pro třídu **zápisu** .</span><span class="sxs-lookup"><span data-stu-id="2b742-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="2b742-131">Po dokončení budete mít k dispozici soubor **EnrollmentsController.cs** a složku v **zobrazení** s názvem **registrace** pomocí zobrazení vytvořit, odstranit, podrobnosti, úpravy a rejstřík.</span><span class="sxs-lookup"><span data-stu-id="2b742-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="2b742-132">Přidat odkazy na nová zobrazení</span><span class="sxs-lookup"><span data-stu-id="2b742-132">Add links to new views</span></span>

<span data-ttu-id="2b742-133">Aby bylo snazší přejít na nová zobrazení, můžete přidat několik hypertextových odkazů do zobrazení indexu pro studenty a registrace.</span><span class="sxs-lookup"><span data-stu-id="2b742-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="2b742-134">Otevřete soubor v **zobrazeních** > **Home** > *index. cshtml*, což je Domovská stránka vašeho webu.</span><span class="sxs-lookup"><span data-stu-id="2b742-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="2b742-135">Pod JumboTron přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="2b742-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="2b742-136">Pro metodu ActionLink je prvním parametrem text, který se má zobrazit v odkazu.</span><span class="sxs-lookup"><span data-stu-id="2b742-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="2b742-137">Druhým parametrem je akce a třetí parametr je název kontroleru.</span><span class="sxs-lookup"><span data-stu-id="2b742-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="2b742-138">Například první odkaz odkazuje na akci indexu v StudentsController.</span><span class="sxs-lookup"><span data-stu-id="2b742-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="2b742-139">Skutečný hypertextový odkaz je vytvořen z těchto hodnot.</span><span class="sxs-lookup"><span data-stu-id="2b742-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="2b742-140">První odkaz nakonec převezme uživatele do souboru **index. cshtml** v rámci složky **views/Students** .</span><span class="sxs-lookup"><span data-stu-id="2b742-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="2b742-141">Zobrazit zobrazení studenta</span><span class="sxs-lookup"><span data-stu-id="2b742-141">Display student views</span></span>

<span data-ttu-id="2b742-142">Ověřte, že kód přidaný do projektu správně zobrazuje seznam studentů a umožňuje uživatelům upravovat, vytvářet nebo odstraňovat záznamy studenta v databázi.</span><span class="sxs-lookup"><span data-stu-id="2b742-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="2b742-143">Klikněte pravým tlačítkem na **zobrazení** > soubor *. cshtml* pro **domovskou** > index a **v prohlížeči vyberte Zobrazit**.</span><span class="sxs-lookup"><span data-stu-id="2b742-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="2b742-144">Na domovské stránce aplikace vyberte **seznam studentů**.</span><span class="sxs-lookup"><span data-stu-id="2b742-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="2b742-145">Na stránce **index** si všimněte seznamu studentů a odkazů pro úpravu těchto dat.</span><span class="sxs-lookup"><span data-stu-id="2b742-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="2b742-146">Vyberte odkaz **vytvořit nový** a zadejte některé hodnoty pro nového studenta.</span><span class="sxs-lookup"><span data-stu-id="2b742-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="2b742-147">Klikněte na **vytvořit**a Všimněte si, že se do seznamu přidá nový student.</span><span class="sxs-lookup"><span data-stu-id="2b742-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="2b742-148">Zpět na stránce **index** vyberte odkaz **Upravit** a změňte některé hodnoty pro studenta.</span><span class="sxs-lookup"><span data-stu-id="2b742-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="2b742-149">Klikněte na **Uložit**a Všimněte si, že se změnil záznam studenta.</span><span class="sxs-lookup"><span data-stu-id="2b742-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="2b742-150">Nakonec vyberte odkaz **Odstranit** a potvrďte, že chcete záznam odstranit kliknutím na tlačítko **Odstranit** .</span><span class="sxs-lookup"><span data-stu-id="2b742-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="2b742-151">Bez psaní kódu jste přidali zobrazení, která provádějí běžné operace s daty v tabulce student.</span><span class="sxs-lookup"><span data-stu-id="2b742-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="2b742-152">Možná jste si všimli, že textový popisek pro pole je založen na vlastnosti databáze (například **LastName**), která není nutně ta, co chcete zobrazit na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="2b742-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="2b742-153">Například můžete chtít, aby popisek byl **Poslední název**.</span><span class="sxs-lookup"><span data-stu-id="2b742-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="2b742-154">Tento problém se zobrazením opravíte později v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="2b742-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="2b742-155">Zobrazit zobrazení pro zápis</span><span class="sxs-lookup"><span data-stu-id="2b742-155">Display enrollment views</span></span>

<span data-ttu-id="2b742-156">Vaše databáze obsahuje vztah 1:1 mezi tabulkami studentů a registrací a vztah 1: n mezi tabulkami kurzů a zápisů.</span><span class="sxs-lookup"><span data-stu-id="2b742-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="2b742-157">Zobrazení pro registraci správně zpracovávají tyto vztahy.</span><span class="sxs-lookup"><span data-stu-id="2b742-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="2b742-158">Přejděte na domovskou stránku vašeho webu a vyberte odkaz **seznam** registrací a pak klikněte na odkaz pro **Vytvoření nového** .</span><span class="sxs-lookup"><span data-stu-id="2b742-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="2b742-159">Zobrazení obsahuje formulář pro vytvoření nového záznamu registrace.</span><span class="sxs-lookup"><span data-stu-id="2b742-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="2b742-160">Zejména si všimněte, že formulář obsahuje rozevírací seznam **CourseID** a rozevírací seznam **StudentID** .</span><span class="sxs-lookup"><span data-stu-id="2b742-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="2b742-161">Obě jsou vyplněny hodnotami ze souvisejících tabulek.</span><span class="sxs-lookup"><span data-stu-id="2b742-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="2b742-162">Kromě toho se ověření zadaných hodnot automaticky použije na základě datového typu pole.</span><span class="sxs-lookup"><span data-stu-id="2b742-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="2b742-163">Pro **třídu** je vyžadováno číslo, takže se zobrazí chybová zpráva, pokud se pokusíte zadat nekompatibilní hodnotu: hodnota *pole musí být číslo.*</span><span class="sxs-lookup"><span data-stu-id="2b742-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="2b742-164">Ověřili jste, že automaticky vygenerovaná zobrazení umožňují uživatelům pracovat s daty v databázi.</span><span class="sxs-lookup"><span data-stu-id="2b742-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="2b742-165">V dalším kurzu v této sérii aktualizujete databázi a provedete příslušné změny ve webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2b742-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b742-166">Další kroky</span><span class="sxs-lookup"><span data-stu-id="2b742-166">Next steps</span></span>

<span data-ttu-id="2b742-167">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="2b742-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b742-168">Přidání uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="2b742-168">Added scaffold</span></span>
> * <span data-ttu-id="2b742-169">Přidané odkazy na nová zobrazení</span><span class="sxs-lookup"><span data-stu-id="2b742-169">Added links to new views</span></span>
> * <span data-ttu-id="2b742-170">Zobrazení zobrazení studenta</span><span class="sxs-lookup"><span data-stu-id="2b742-170">Displayed student views</span></span>
> * <span data-ttu-id="2b742-171">Zobrazení zápisu</span><span class="sxs-lookup"><span data-stu-id="2b742-171">Displayed enrollment views</span></span>

<span data-ttu-id="2b742-172">Přejděte k dalšímu kurzu, kde se dozvíte, jak změnit databázi.</span><span class="sxs-lookup"><span data-stu-id="2b742-172">Advance to the next tutorial to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2b742-173">Změna databáze</span><span class="sxs-lookup"><span data-stu-id="2b742-173">Change the database</span></span>](changing-the-database.md)