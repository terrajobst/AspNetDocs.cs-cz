---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET, formuláře a ověřování pro MVC 4 | Microsoft Docs
author: rick-anderson
description: V ASP.NET MVC 4 modelech a praktických testovacích prostředích pro přístup k datům jste načetli a zobrazili data z databáze. V této praktické laboratorní laboratoři přidáte do...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539576"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="92c47-104">ASP.NET MVC 4 – pomocníci, formuláře a ověřování</span><span class="sxs-lookup"><span data-stu-id="92c47-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="92c47-105">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="92c47-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="92c47-106">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="92c47-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="92c47-107">V **ASP.NET MVC 4 modelech a** praktických testovacích prostředích pro přístup k datům jste načetli a zobrazili data z databáze.</span><span class="sxs-lookup"><span data-stu-id="92c47-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="92c47-108">V tomto praktickém cvičení přidáte do aplikace **hudebního úložiště** možnost upravovat tato data.</span><span class="sxs-lookup"><span data-stu-id="92c47-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="92c47-109">Na základě tohoto cíle se nejprve vytvoří kontroler, který bude podporovat akce vytváření, čtení, aktualizace a odstranění (CRUD) alb.</span><span class="sxs-lookup"><span data-stu-id="92c47-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="92c47-110">Vygenerujete šablonu zobrazení indexů s využitím funkce generování uživatelského rozhraní ASP.NET MVC k zobrazení vlastností alba v tabulce HTML.</span><span class="sxs-lookup"><span data-stu-id="92c47-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="92c47-111">Chcete-li toto zobrazení vylepšit, přidejte vlastní nápovědu HTML, která bude zkrátit dlouhé popisy.</span><span class="sxs-lookup"><span data-stu-id="92c47-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="92c47-112">Následně přidáte zobrazení upravit a vytvořit, která vám umožní změnit alba v databázi pomocí prvků formuláře jako rozevíracích seznamů.</span><span class="sxs-lookup"><span data-stu-id="92c47-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="92c47-113">Nakonec umožníte uživatelům odstranit album a zároveň jim zabráníte v zadávání nesprávných dat, a to tak, že se budou ověřovat jejich vstupy.</span><span class="sxs-lookup"><span data-stu-id="92c47-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="92c47-114">Tato praktická cvičení předpokládá, že máte základní znalosti o **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="92c47-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="92c47-115">Pokud jste ještě **ASP.NET MVC** nepoužívali, doporučujeme, abyste si převzali základní praktické prostředí pro **ASP.NET MVC** .</span><span class="sxs-lookup"><span data-stu-id="92c47-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="92c47-116">Toto testovací prostředí vás provede vylepšeními a novými funkcemi, které jsme dříve popsali pomocí menších změn ve vzorové webové aplikaci, která je součástí zdrojové složky.</span><span class="sxs-lookup"><span data-stu-id="92c47-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="92c47-117">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="92c47-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="92c47-118">Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NETch pomocníkech MVC 4, formulářích a ověřování](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span><span class="sxs-lookup"><span data-stu-id="92c47-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="92c47-119">Cíle</span><span class="sxs-lookup"><span data-stu-id="92c47-119">Objectives</span></span>

<span data-ttu-id="92c47-120">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="92c47-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="92c47-121">Vytvoření kontroleru pro podporu operací CRUD</span><span class="sxs-lookup"><span data-stu-id="92c47-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="92c47-122">Generování zobrazení indexu pro zobrazení vlastností entity v tabulce HTML</span><span class="sxs-lookup"><span data-stu-id="92c47-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="92c47-123">Přidat vlastní nápovědu HTML</span><span class="sxs-lookup"><span data-stu-id="92c47-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="92c47-124">Vytvoření a přizpůsobení zobrazení pro úpravy</span><span class="sxs-lookup"><span data-stu-id="92c47-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="92c47-125">Rozlišit mezi metodami akce, které reagují na volání HTTP-GET nebo HTTP-POST</span><span class="sxs-lookup"><span data-stu-id="92c47-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="92c47-126">Přidání a přizpůsobení zobrazení pro vytvoření</span><span class="sxs-lookup"><span data-stu-id="92c47-126">Add and customize a Create View</span></span>
- <span data-ttu-id="92c47-127">Zpracování odstranění entity</span><span class="sxs-lookup"><span data-stu-id="92c47-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="92c47-128">Ověření vstupu uživatele</span><span class="sxs-lookup"><span data-stu-id="92c47-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="92c47-129">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="92c47-129">Prerequisites</span></span>

<span data-ttu-id="92c47-130">K dokončení tohoto testovacího prostředí musíte mít následující položky:</span><span class="sxs-lookup"><span data-stu-id="92c47-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="92c47-131">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).</span><span class="sxs-lookup"><span data-stu-id="92c47-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="92c47-132">Nastavení</span><span class="sxs-lookup"><span data-stu-id="92c47-132">Setup</span></span>

<span data-ttu-id="92c47-133">**Instalace fragmentů kódu**</span><span class="sxs-lookup"><span data-stu-id="92c47-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="92c47-134">Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92c47-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="92c47-135">Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .</span><span class="sxs-lookup"><span data-stu-id="92c47-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="92c47-136">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze B: použití fragmentů kódu](#AppendixB)&quot;.</span><span class="sxs-lookup"><span data-stu-id="92c47-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="92c47-137">Cvičení</span><span class="sxs-lookup"><span data-stu-id="92c47-137">Exercises</span></span>

<span data-ttu-id="92c47-138">Následující cvičení tvoří tuto praktickou laboratoř:</span><span class="sxs-lookup"><span data-stu-id="92c47-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="92c47-139">Vytvoření kontroleru Správce úložiště a jeho zobrazení indexu</span><span class="sxs-lookup"><span data-stu-id="92c47-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="92c47-140">Přidání pomocníka jazyka HTML</span><span class="sxs-lookup"><span data-stu-id="92c47-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="92c47-141">Vytvoření zobrazení pro úpravy</span><span class="sxs-lookup"><span data-stu-id="92c47-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="92c47-142">Přidání zobrazení pro vytvoření</span><span class="sxs-lookup"><span data-stu-id="92c47-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="92c47-143">Odstraňování zpracování</span><span class="sxs-lookup"><span data-stu-id="92c47-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="92c47-144">Přidání ověřování</span><span class="sxs-lookup"><span data-stu-id="92c47-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="92c47-145">Použití nenápadu jQuery na straně klienta</span><span class="sxs-lookup"><span data-stu-id="92c47-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="92c47-146">Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="92c47-147">Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="92c47-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="92c47-148">Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**</span><span class="sxs-lookup"><span data-stu-id="92c47-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="92c47-149">Cvičení 1: vytvoření kontroleru Správce úložiště a jeho zobrazení indexu</span><span class="sxs-lookup"><span data-stu-id="92c47-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="92c47-150">V tomto cvičení se naučíte, jak vytvořit nový kontroler, který podporuje operace CRUD, přizpůsobení metody jeho akce index, která vrátí seznam alb z databáze a nakonec vygeneruje šablonu zobrazení indexu s využitím generování uživatelského rozhraní ASP.NET MVC. funkce pro zobrazení vlastností alba v tabulce HTML</span><span class="sxs-lookup"><span data-stu-id="92c47-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="92c47-151">Úloha 1 – Vytvoření StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="92c47-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="92c47-152">V této úloze vytvoříte nový kontroler s názvem **StoreManagerController** , který bude podporovat operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="92c47-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="92c47-153">Otevřete řešení **zahájit** , které se nachází ve složce **source/EX1-CreatingTheStoreManagerController/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="92c47-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="92c47-154">Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92c47-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="92c47-155">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92c47-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="92c47-156">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="92c47-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="92c47-157">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="92c47-158">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="92c47-159">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="92c47-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="92c47-160">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="92c47-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="92c47-161">Přidejte nový kontroler.</span><span class="sxs-lookup"><span data-stu-id="92c47-161">Add a new controller.</span></span> <span data-ttu-id="92c47-162">Provedete to tak, že kliknete pravým tlačítkem myši na složku **Controllers** v rámci Průzkumník řešení, vyberete **Přidat** a pak příkaz **Controller** .</span><span class="sxs-lookup"><span data-stu-id="92c47-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="92c47-163">Změňte název **kontroleru** na **StoreManagerController** a ujistěte se, že je vybraná možnost **kontroler MVC s prázdnými akcemi čtení/zápisu** .</span><span class="sxs-lookup"><span data-stu-id="92c47-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="92c47-164">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="92c47-164">Click **Add**.</span></span>

    <span data-ttu-id="92c47-165">![Dialogové okno Přidat řadič](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Dialogové okno Přidat řadič")</span><span class="sxs-lookup"><span data-stu-id="92c47-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="92c47-166">*Dialogové okno Přidat řadič*</span><span class="sxs-lookup"><span data-stu-id="92c47-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="92c47-167">Je vygenerována nová třída kontroleru.</span><span class="sxs-lookup"><span data-stu-id="92c47-167">A new Controller class is generated.</span></span> <span data-ttu-id="92c47-168">Vzhledem k tomu, že jste označili, že se mají přidat akce pro čtení a zápis, jsou pro ně běžné akce CRUD vytvořeny pomocí komentářů TODO, které jsou vyplněny, přičemž se zobrazí výzva k zahrnutí logiky specifické pro aplikaci</span><span class="sxs-lookup"><span data-stu-id="92c47-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="92c47-169">Úloha 2 – přizpůsobení indexu StoreManager</span><span class="sxs-lookup"><span data-stu-id="92c47-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="92c47-170">V této úloze přizpůsobíte metodu akce indexu StoreManager, která vrátí zobrazení se seznamem alb z databáze.</span><span class="sxs-lookup"><span data-stu-id="92c47-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="92c47-171">Ve třídě StoreManagerController přidejte následující direktivy *using* .</span><span class="sxs-lookup"><span data-stu-id="92c47-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="92c47-172">(Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování – EX1 s využitím MvcMusicStore*)</span><span class="sxs-lookup"><span data-stu-id="92c47-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="92c47-173">Přidejte do **StoreManagerController** pole pro uložení instance **MusicStoreEntities.**</span><span class="sxs-lookup"><span data-stu-id="92c47-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="92c47-174">(Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověření – EX1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="92c47-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="92c47-175">Implementujte akci indexu StoreManagerController, která vrátí zobrazení se seznamem alb.</span><span class="sxs-lookup"><span data-stu-id="92c47-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="92c47-176">Logika akce kontroleru bude velmi podobná akci indexu StoreController, která byla zapsána dříve.</span><span class="sxs-lookup"><span data-stu-id="92c47-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="92c47-177">Použijte LINQ k načtení všech alb, včetně informací o žánrech a interpretech k zobrazení.</span><span class="sxs-lookup"><span data-stu-id="92c47-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="92c47-178">(Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování – EX1 StoreManagerController index*)</span><span class="sxs-lookup"><span data-stu-id="92c47-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="92c47-179">Úloha 3 – Vytvoření zobrazení indexu</span><span class="sxs-lookup"><span data-stu-id="92c47-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="92c47-180">V této úloze vytvoříte šablonu zobrazení indexů, ve které se zobrazí seznam alb vrácených řadičem **StoreManager** .</span><span class="sxs-lookup"><span data-stu-id="92c47-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="92c47-181">Před vytvořením nové šablony zobrazení byste měli sestavit projekt tak, aby **dialog Přidat zobrazení** věděl o třídě **alba** , která se má použít.</span><span class="sxs-lookup"><span data-stu-id="92c47-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="92c47-182">Vybrat **Build | Sestavte MvcMusicStore** a sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="92c47-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="92c47-183">Klikněte pravým tlačítkem myši do metody **index** Action a vyberte **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="92c47-184">Tím se zobrazí dialogové okno **Přidat zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="92c47-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="92c47-185">![Přidat zobrazení](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Přidat zobrazení")</span><span class="sxs-lookup"><span data-stu-id="92c47-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="92c47-186">*Přidání zobrazení v rámci metody index*</span><span class="sxs-lookup"><span data-stu-id="92c47-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="92c47-187">V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **index**.</span><span class="sxs-lookup"><span data-stu-id="92c47-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="92c47-188">Vyberte možnost **vytvořit zobrazení silného typu** a z rozevíracího seznamu **třída modelu** vyberte **album (MvcMusicStore. model)** .</span><span class="sxs-lookup"><span data-stu-id="92c47-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="92c47-189">V rozevíracím seznamu **Šablona generování uživatelského rozhraní** vyberte možnost **seznam** .</span><span class="sxs-lookup"><span data-stu-id="92c47-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="92c47-190">Ponechte **modul zobrazení** na **Razor** a ostatní pole s výchozí hodnotou a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="92c47-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="92c47-191">![Přidání zobrazení indexu](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Přidání zobrazení indexu")</span><span class="sxs-lookup"><span data-stu-id="92c47-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="92c47-192">*Přidání zobrazení indexu*</span><span class="sxs-lookup"><span data-stu-id="92c47-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="92c47-193">Úloha 4 – přizpůsobení uživatelského rozhraní zobrazení indexu</span><span class="sxs-lookup"><span data-stu-id="92c47-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="92c47-194">V této úloze upravíte šablonu jednoduchého zobrazení vytvořenou funkcí generování uživatelského rozhraní ASP.NET MVC, aby se zobrazila pole, která chcete.</span><span class="sxs-lookup"><span data-stu-id="92c47-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="92c47-195">Podpora **generování uživatelského rozhraní** v rámci ASP.NET MVC generuje jednoduchou šablonu zobrazení, která obsahuje seznam všech polí v modelu alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="92c47-196">**Generování uživatelského rozhraní** poskytuje rychlý způsob, jak začít se zobrazením silného typu: místo ručního psaní šablony zobrazení, generování uživatelského rozhraní rychle vygeneruje výchozí šablonu a potom můžete vygenerovaný kód upravit.</span><span class="sxs-lookup"><span data-stu-id="92c47-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>

1. <span data-ttu-id="92c47-197">Zkontrolujte vytvořený kód.</span><span class="sxs-lookup"><span data-stu-id="92c47-197">Review the code created.</span></span> <span data-ttu-id="92c47-198">Vygenerovaný seznam polí bude součástí následující tabulky HTML, kterou **generování uživatelského rozhraní** používá pro zobrazení tabulkových dat.</span><span class="sxs-lookup"><span data-stu-id="92c47-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="92c47-199">Chcete-li zobrazit pouze pole **Žánr**, **umělec**, **název alba**a **ceny** , nahraďte **&lt;tabulku&gt;** kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="92c47-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="92c47-200">Tím se odstraní sloupce **adresy URL pro obrázek** **AlbumId** a alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="92c47-201">Také změní sloupce GenreId a ArtistId tak, aby zobrazovaly vlastnosti propojené třídy **Artist.Name** a **Genre.Name**a odebraly odkaz **Podrobnosti** .</span><span class="sxs-lookup"><span data-stu-id="92c47-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="92c47-202">Změňte následující popisy.</span><span class="sxs-lookup"><span data-stu-id="92c47-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="92c47-203">Úloha 5 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="92c47-204">V této úloze otestujete, že šablona zobrazení **indexu** StoreManager zobrazí seznam alb podle návrhu předchozích kroků.</span><span class="sxs-lookup"><span data-stu-id="92c47-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="92c47-205">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-206">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-206">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-207">Změňte adresu URL na **/StoreManager** , abyste ověřili, že se zobrazuje seznam alb a zobrazuje jejich **název**, **Interpret** a **Žánr**.</span><span class="sxs-lookup"><span data-stu-id="92c47-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="92c47-208">![Procházení seznamu alb](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Procházení seznamu alb")</span><span class="sxs-lookup"><span data-stu-id="92c47-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="92c47-209">*Procházení seznamu alb*</span><span class="sxs-lookup"><span data-stu-id="92c47-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="92c47-210">Cvičení 2: Přidání pomocníka HTML</span><span class="sxs-lookup"><span data-stu-id="92c47-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="92c47-211">Stránka indexu StoreManager má jeden potenciální problém: Vlastnosti názvu a jména umělce můžou být pro vyvolání formátování tabulky dostatečně dlouhé.</span><span class="sxs-lookup"><span data-stu-id="92c47-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="92c47-212">V tomto cvičení se dozvíte, jak přidat vlastní pomůcku HTML pro zkracování tohoto textu.</span><span class="sxs-lookup"><span data-stu-id="92c47-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="92c47-213">Na následujícím obrázku vidíte, jak se upraví formát z důvodu délky textu při použití malého velikosti prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="92c47-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="92c47-214">![Procházení seznamu alb s nezkráceným textem](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Procházení seznamu alb s nezkráceným textem")</span><span class="sxs-lookup"><span data-stu-id="92c47-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="92c47-215">*Procházení seznamu alb s nezkráceným textem*</span><span class="sxs-lookup"><span data-stu-id="92c47-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="92c47-216">Úloha 1 – rozšíření pomocné rutiny HTML</span><span class="sxs-lookup"><span data-stu-id="92c47-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="92c47-217">V této úloze přidáte novou metodu pro **oříznutí** objektu **HTML** vystaveného v zobrazeních ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="92c47-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="92c47-218">Chcete-li to provést, implementujte **metodu rozšíření** do předdefinované třídy **System. Web. Mvc. HtmlHelper** , kterou poskytuje ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="92c47-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="92c47-219">Další informace o **metodách rozšíření**najdete v tomto článku na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="92c47-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="92c47-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="92c47-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>

1. <span data-ttu-id="92c47-221">Otevřete řešení **zahájit** , které se nachází ve složce **source/EX2-AddingAnHTMLHelper/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="92c47-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="92c47-222">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="92c47-223">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92c47-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="92c47-224">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92c47-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="92c47-225">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="92c47-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="92c47-226">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="92c47-227">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="92c47-228">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="92c47-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="92c47-229">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="92c47-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="92c47-230">Otevřete zobrazení indexu StoreManager.</span><span class="sxs-lookup"><span data-stu-id="92c47-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="92c47-231">Chcete-li to provést, v Průzkumník řešení rozbalte složku **zobrazení** , poté **StoreManager** a otevřete soubor **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="92c47-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="92c47-232">Přidejte následující kód pod direktivu <strong>@model</strong> a definujte pomocnou metodu <strong>zkracování</strong> .</span><span class="sxs-lookup"><span data-stu-id="92c47-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="92c47-233">Úkol 2 – zkracování textu na stránce</span><span class="sxs-lookup"><span data-stu-id="92c47-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="92c47-234">V této úloze použijete metodu **zkracování** ke zkrácení textu v šabloně zobrazení.</span><span class="sxs-lookup"><span data-stu-id="92c47-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="92c47-235">Otevřete zobrazení indexu StoreManager.</span><span class="sxs-lookup"><span data-stu-id="92c47-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="92c47-236">Chcete-li to provést, v Průzkumník řešení rozbalte složku **zobrazení** , poté **StoreManager** a otevřete soubor **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="92c47-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="92c47-237">Nahraďte řádky, které zobrazují **název interpreta** **a název alba.**</span><span class="sxs-lookup"><span data-stu-id="92c47-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="92c47-238">Chcete-li to provést, nahraďte následující řádky.</span><span class="sxs-lookup"><span data-stu-id="92c47-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="92c47-239">Úloha 3 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="92c47-240">V této úloze otestujete, že šablona zobrazení **indexu** StoreManager zkrátí název alba a jméno umělce.</span><span class="sxs-lookup"><span data-stu-id="92c47-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="92c47-241">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-242">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-242">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-243">Změňte adresu URL na **/StoreManager** a ověřte, že dlouhé texty ve sloupci **název** a **Interpret** jsou zkrácené.</span><span class="sxs-lookup"><span data-stu-id="92c47-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="92c47-244">![Zkrácený název názvů a umělců](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Zkrácený název názvů a umělců")</span><span class="sxs-lookup"><span data-stu-id="92c47-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="92c47-245">*Zkrácený název názvů a umělců*</span><span class="sxs-lookup"><span data-stu-id="92c47-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="92c47-246">Cvičení 3: Vytvoření zobrazení pro úpravy</span><span class="sxs-lookup"><span data-stu-id="92c47-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="92c47-247">V tomto cvičení se naučíte, jak vytvořit formulář, který správcům úložiště umožní upravovat album.</span><span class="sxs-lookup"><span data-stu-id="92c47-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="92c47-248">Budou procházet adresu URL **/StoreManager/Edit/ID** (**ID** se jedná o jedinečné ID alba, které se má upravit), takže se k serveru vytvoří volání HTTP-GET.</span><span class="sxs-lookup"><span data-stu-id="92c47-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="92c47-249">Metoda akce úprav kontroleru načte příslušné album z databáze, vytvoří objekt **StoreManagerViewModel** , který ho zapouzdří (společně se seznamem umělců a žánrů), a pak ho předá do šablony zobrazení, kde se stránka HTML vykreslí zpátky uživateli.</span><span class="sxs-lookup"><span data-stu-id="92c47-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="92c47-250">Tato stránka bude obsahovat **&gt;element&lt;formuláře** s textovým polem a rozevíracími seznamy pro úpravu vlastností alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="92c47-251">Jakmile uživatel aktualizuje hodnoty formuláře alba a klikne na tlačítko **Uložit** , změny se odešlou prostřednictvím volání http-post zpět do **/StoreManager/Edit/ID**. I když adresa URL zůstává stejná jako při posledním volání, ASP.NET MVC zjistí, že je to HTTP-POST, a proto provede jinou metodu úprav akce (jedna dekorovaná s **[HTTPPOST]** ).</span><span class="sxs-lookup"><span data-stu-id="92c47-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="92c47-252">Úloha 1 – implementace metody HTTP-GET Edit Action</span><span class="sxs-lookup"><span data-stu-id="92c47-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="92c47-253">V této úloze implementujete verzi HTTP-GET metody Edit Action pro načtení příslušného alba z databáze a také seznam všech žánrů a umělců.</span><span class="sxs-lookup"><span data-stu-id="92c47-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="92c47-254">Bude tato data zabalit až do objektu **StoreManagerViewModel** definovaného v posledním kroku, který se pak předá do šablony zobrazení, ve které se odpověď vykreslí.</span><span class="sxs-lookup"><span data-stu-id="92c47-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="92c47-255">Otevřete řešení **zahájit** , které se nachází ve složce **source/EX3-CreatingTheEditView/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="92c47-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="92c47-256">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="92c47-257">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92c47-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="92c47-258">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92c47-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="92c47-259">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="92c47-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="92c47-260">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="92c47-261">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="92c47-262">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="92c47-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="92c47-263">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="92c47-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="92c47-264">Otevřete třídu **StoreManagerController** .</span><span class="sxs-lookup"><span data-stu-id="92c47-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="92c47-265">Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="92c47-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="92c47-266">Nahraďte metodu **HTTP-GET Edit** Action následujícím kódem k načtení vhodného **alba** a také seznamů **žánrů** a **umělců** .</span><span class="sxs-lookup"><span data-stu-id="92c47-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="92c47-267">(Fragment kódu – *ASP.NET MVC 4 a formuláře a ověření – EX3 STOREMANAGERCONTROLLER HTTP-GET Action Edit*)</span><span class="sxs-lookup"><span data-stu-id="92c47-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="92c47-268">Používáte **System. Web. Mvc** **SelectList** pro interprety a žánry namísto seznamu **System. Collections. Generic** .</span><span class="sxs-lookup"><span data-stu-id="92c47-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="92c47-269">**SelectList** je čisticí způsob, jak naplnit rozevírací seznamy HTML a spravovat věci, jako je aktuální výběr.</span><span class="sxs-lookup"><span data-stu-id="92c47-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="92c47-270">Vytvoření instance a pozdější nastavení těchto ViewModel objektů v akci kontroleru provede čistič scénářů pro úpravu formuláře.</span><span class="sxs-lookup"><span data-stu-id="92c47-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="92c47-271">Úkol 2 – Vytvoření zobrazení pro úpravy</span><span class="sxs-lookup"><span data-stu-id="92c47-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="92c47-272">V této úloze vytvoříte šablonu zobrazení pro úpravy, která bude později zobrazovat vlastnosti alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="92c47-273">Vytvořte zobrazení pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="92c47-273">Create the Edit View.</span></span> <span data-ttu-id="92c47-274">Provedete to tak, že kliknete pravým tlačítkem myši do metody **Upravit** akci a vyberete **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="92c47-275">V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **upraven**.</span><span class="sxs-lookup"><span data-stu-id="92c47-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="92c47-276">Zaškrtněte políčko **vytvořit zobrazení silného typu** a v rozevíracím seznamu **Třída zobrazení dat** vyberte **album (MvcMusicStore. model)** .</span><span class="sxs-lookup"><span data-stu-id="92c47-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="92c47-277">V rozevíracím seznamu **Šablona generování uživatelského rozhraní** vyberte **Upravit** .</span><span class="sxs-lookup"><span data-stu-id="92c47-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="92c47-278">Ostatní pole ponechte výchozí hodnotou a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="92c47-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="92c47-279">![Přidání zobrazení pro úpravy](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Přidání zobrazení pro úpravy")</span><span class="sxs-lookup"><span data-stu-id="92c47-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="92c47-280">*Přidání zobrazení pro úpravy*</span><span class="sxs-lookup"><span data-stu-id="92c47-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="92c47-281">Úloha 3 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="92c47-282">V této úloze otestujete, že na stránce pro **úpravu** zobrazení **StoreManager** se zobrazí hodnoty vlastností předaného alba jako parametr.</span><span class="sxs-lookup"><span data-stu-id="92c47-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="92c47-283">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-284">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-284">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-285">Změňte adresu URL na **/StoreManager/Edit/1** a ověřte, že se zobrazí hodnoty vlastnosti pro předané album.</span><span class="sxs-lookup"><span data-stu-id="92c47-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="92c47-286">![Zobrazení úprav alba pro procházení](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Zobrazení úprav alba pro procházení")</span><span class="sxs-lookup"><span data-stu-id="92c47-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="92c47-287">*Zobrazení úprav alba pro procházení*</span><span class="sxs-lookup"><span data-stu-id="92c47-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="92c47-288">Úloha 4 – implementace rozevíracích seznamu v šabloně editoru alba</span><span class="sxs-lookup"><span data-stu-id="92c47-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="92c47-289">V této úloze přidáte rozevírací seznam pro šablonu zobrazení vytvořenou v posledním úkolu, aby uživatel mohl vybírat ze seznamu umělců a žánrů.</span><span class="sxs-lookup"><span data-stu-id="92c47-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="92c47-290">Nahraďte celý kód sady polí **alba** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="92c47-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="92c47-291">Pro vykreslení rozevíracího seznamu pro výběr umělců a žánrů byl přidán pomocník **HTML. DropDownList** .</span><span class="sxs-lookup"><span data-stu-id="92c47-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="92c47-292">Parametry předané do **HTML. DropDownList** jsou:</span><span class="sxs-lookup"><span data-stu-id="92c47-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="92c47-293">Název pole formuláře ( **&quot;ArtistId&quot;** ).</span><span class="sxs-lookup"><span data-stu-id="92c47-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="92c47-294">**SelectList** hodnot rozevíracího seznamu.</span><span class="sxs-lookup"><span data-stu-id="92c47-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="92c47-295">Úloha 5 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="92c47-296">V této úloze otestujete, že stránka pro **úpravu** zobrazení StoreManager zobrazuje rozevírací seznam namísto textových polí umělec a Žánr ID.</span><span class="sxs-lookup"><span data-stu-id="92c47-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="92c47-297">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-298">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-298">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-299">Změňte adresu URL na **/StoreManager/Edit/1** a ověřte tak, že se budou zobrazovat rozevírací nabídky místo textových polí jméno umělce a žánru.</span><span class="sxs-lookup"><span data-stu-id="92c47-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="92c47-300">![Procházení zobrazení pro úpravy alba pomocí rozevíracích seznamu](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Procházení zobrazení pro úpravy alba pomocí rozevíracích seznamu")</span><span class="sxs-lookup"><span data-stu-id="92c47-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="92c47-301">*Prohlížení zobrazení pro úpravy alba, tentokrát s rozevíracími seznamy*</span><span class="sxs-lookup"><span data-stu-id="92c47-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="92c47-302">Úloha 6 – implementace metody akce HTTP-POST pro akci úprav</span><span class="sxs-lookup"><span data-stu-id="92c47-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="92c47-303">Teď, když se zobrazení pro úpravy zobrazuje podle očekávání, je nutné implementovat metodu akce HTTP-POST pro úpravy, aby se uložily změny provedené v albu.</span><span class="sxs-lookup"><span data-stu-id="92c47-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="92c47-304">V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92c47-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="92c47-305">Otevřete **StoreManagerController** ze složky **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="92c47-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="92c47-306">Nahraďte kód metody akce **http-post** pomocí následujícího postupu (Všimněte si, že metoda, která musí být nahrazena, je přetížená verze, která přijímá dva parametry):</span><span class="sxs-lookup"><span data-stu-id="92c47-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="92c47-307">(Fragment kódu – *ASP.NET MVC 4 a formuláře a ověřování – EX3 STOREMANAGERCONTROLLER http-post Action Edit*)</span><span class="sxs-lookup"><span data-stu-id="92c47-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="92c47-308">Tato metoda se spustí, když uživatel klikne na tlačítko **Uložit** v zobrazení a provede http-post hodnoty formuláře zpátky na server, aby byly uchovány v databázi.</span><span class="sxs-lookup"><span data-stu-id="92c47-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="92c47-309">Dekoratér **[HTTPPOST]** označuje, že metoda by měla být použita pro tyto scénáře http-post.</span><span class="sxs-lookup"><span data-stu-id="92c47-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="92c47-310">Metoda přebírá objekt **alba** .</span><span class="sxs-lookup"><span data-stu-id="92c47-310">The method takes an **Album** object.</span></span> <span data-ttu-id="92c47-311">ASP.NET MVC automaticky vytvoří objekt alba z publikovaných &lt;ových formulářů&gt; hodnot.</span><span class="sxs-lookup"><span data-stu-id="92c47-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="92c47-312">Metoda provede tyto kroky:</span><span class="sxs-lookup"><span data-stu-id="92c47-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="92c47-313">Pokud je model platný:</span><span class="sxs-lookup"><span data-stu-id="92c47-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="92c47-314">Aktualizujte záznam alba v kontextu tak, aby byl označen jako upravený objekt.</span><span class="sxs-lookup"><span data-stu-id="92c47-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="92c47-315">Uloží změny a přesměruje zobrazení indexu.</span><span class="sxs-lookup"><span data-stu-id="92c47-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="92c47-316">Pokud model není platný, naplní ViewBag pomocí **GenreId** a **ArtistId**, potom vrátí zobrazení s obdrženým objektem alba, aby uživatel mohl provést požadovanou aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="92c47-317">Úloha 7 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="92c47-318">V této úloze otestujete, že stránka pro **úpravu zobrazení StoreManager** ve skutečnosti ukládá aktualizovaná data alba v databázi.</span><span class="sxs-lookup"><span data-stu-id="92c47-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="92c47-319">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-320">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-320">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-321">Změňte adresu URL na **/StoreManager/Edit/1**.</span><span class="sxs-lookup"><span data-stu-id="92c47-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="92c47-322">Změňte název alba, který se má **načíst** , a klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="92c47-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="92c47-323">Ověřte, že se název alba ve skutečnosti změnil v seznamu alb.</span><span class="sxs-lookup"><span data-stu-id="92c47-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="92c47-324">![Aktualizace alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Aktualizace alba")</span><span class="sxs-lookup"><span data-stu-id="92c47-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="92c47-325">*Aktualizace alba*</span><span class="sxs-lookup"><span data-stu-id="92c47-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="92c47-326">Cvičení 4: Přidání zobrazení pro vytvoření</span><span class="sxs-lookup"><span data-stu-id="92c47-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="92c47-327">Teď, když **StoreManagerController** podporuje možnosti **úprav** , v tomto cvičení se dozvíte, jak přidat šablonu pro vytvoření zobrazení a umožnit tak správcům úložiště přidávat do aplikace nová alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="92c47-328">Stejně jako u funkce úprav budete implementovat scénář vytváření pomocí dvou samostatných metod v rámci třídy **StoreManagerController** :</span><span class="sxs-lookup"><span data-stu-id="92c47-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="92c47-329">Jedna metoda akce zobrazí prázdný formulář, když Správci úložiště nejdřív navštíví adresu URL **/StoreManager/Create** .</span><span class="sxs-lookup"><span data-stu-id="92c47-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="92c47-330">Druhá metoda akce zpracuje scénář, ve kterém Správce úložiště klikne na tlačítko **Uložit** v rámci formuláře a pošle hodnoty zpátky do adresy URL **/StoreManager/Create** jako http-post.</span><span class="sxs-lookup"><span data-stu-id="92c47-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="92c47-331">Úloha 1 – implementace metody akce HTTP-GET Create</span><span class="sxs-lookup"><span data-stu-id="92c47-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="92c47-332">V této úloze implementujete verzi HTTP-GET metody Create Action pro načtení seznamu všech žánrů a umělců, zabalit tato data do objektu **StoreManagerViewModel** , který pak bude předán do šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="92c47-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="92c47-333">Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex4-AddingACreateView/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="92c47-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="92c47-334">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="92c47-335">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92c47-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="92c47-336">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92c47-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="92c47-337">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="92c47-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="92c47-338">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="92c47-339">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="92c47-340">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="92c47-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="92c47-341">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="92c47-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="92c47-342">Otevřete třídu **StoreManagerController** .</span><span class="sxs-lookup"><span data-stu-id="92c47-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="92c47-343">Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="92c47-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="92c47-344">Kód metody **Create** Action nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="92c47-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="92c47-345">(Fragment kódu – *ASP.NET MVC 4 a formuláře a ověření – Ex4 STOREMANAGERCONTROLLER http – získat akci vytvořit*)</span><span class="sxs-lookup"><span data-stu-id="92c47-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="92c47-346">Úkol 2 – Přidání zobrazení pro vytvoření</span><span class="sxs-lookup"><span data-stu-id="92c47-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="92c47-347">V této úloze přidáte šablonu pro vytvoření zobrazení, která zobrazí nové (prázdné) formuláře alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="92c47-348">Klikněte pravým tlačítkem myši do metody **Create** Action a vyberte **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="92c47-349">Tím se zobrazí dialogové okno Přidat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="92c47-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="92c47-350">V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **vytvořen**.</span><span class="sxs-lookup"><span data-stu-id="92c47-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="92c47-351">Vyberte možnost **vytvořit zobrazení silného typu** a v rozevíracím seznamu **třída modelu** vyberte **album (MvcMusicStore. model)** a **vytvořte** z rozevíracího seznamu pro **šablonu generování uživatelského rozhraní** .</span><span class="sxs-lookup"><span data-stu-id="92c47-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="92c47-352">Ostatní pole ponechte výchozí hodnotou a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="92c47-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="92c47-353">![Přidání zobrazení pro vytvoření](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "Adding-a-Create-View. png")</span><span class="sxs-lookup"><span data-stu-id="92c47-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="92c47-354">*Přidání zobrazení pro vytvoření*</span><span class="sxs-lookup"><span data-stu-id="92c47-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="92c47-355">Aktualizujte pole **GenreId** a **ArtistId** tak, aby používala rozevírací seznam, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="92c47-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="92c47-356">Úloha 3 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="92c47-357">V této úloze otestujete, že se na stránce pro **Vytvoření** zobrazení **StoreManager** zobrazí prázdný formulář alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="92c47-358">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-359">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-359">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-360">Změňte adresu URL na **/StoreManager/Create**.</span><span class="sxs-lookup"><span data-stu-id="92c47-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="92c47-361">Ověřte, že se zobrazí prázdný formulář pro vyplňování nových vlastností alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="92c47-362">![Vytvořit zobrazení s prázdným formulářem](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Vytvořit zobrazení s prázdným formulářem")</span><span class="sxs-lookup"><span data-stu-id="92c47-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="92c47-363">*Vytvořit zobrazení s prázdným formulářem*</span><span class="sxs-lookup"><span data-stu-id="92c47-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="92c47-364">Úloha 4 – implementace metody akce HTTP-POST</span><span class="sxs-lookup"><span data-stu-id="92c47-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="92c47-365">V této úloze implementujete verzi HTTP-POST metody Create Action, která bude vyvolána, když uživatel klikne na tlačítko **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="92c47-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="92c47-366">Metoda by měla uložit nové album v databázi.</span><span class="sxs-lookup"><span data-stu-id="92c47-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="92c47-367">V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92c47-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="92c47-368">Otevřete třídu **StoreManagerController** .</span><span class="sxs-lookup"><span data-stu-id="92c47-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="92c47-369">Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="92c47-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="92c47-370">Nahraďte kód metody **http-post akce Create** následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="92c47-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="92c47-371">(Fragment kódu – *ASP.NETi a formuláře MVC 4 a ověřování – Ex4 STOREMANAGERCONTROLLER http-post Create Action*)</span><span class="sxs-lookup"><span data-stu-id="92c47-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="92c47-372">Akce vytvořit je poměrně podobná předchozí metodě úprav akce, ale místo nastavení objektu jako upraveného je přidána do kontextu.</span><span class="sxs-lookup"><span data-stu-id="92c47-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="92c47-373">Úloha 5 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="92c47-374">V této úloze otestujete, že stránka **StoreManager vytvořit** zobrazení vám umožní vytvořit nové album a pak přesměrovat do zobrazení indexu StoreManager.</span><span class="sxs-lookup"><span data-stu-id="92c47-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="92c47-375">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-376">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-376">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-377">Změňte adresu URL na **/StoreManager/Create**.</span><span class="sxs-lookup"><span data-stu-id="92c47-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="92c47-378">Vyplňte všechna pole formuláře daty nového alba, jako je například na následujícím obrázku:</span><span class="sxs-lookup"><span data-stu-id="92c47-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="92c47-379">![Vytvoření alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Vytvoření alba")</span><span class="sxs-lookup"><span data-stu-id="92c47-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="92c47-380">*Vytvoření alba*</span><span class="sxs-lookup"><span data-stu-id="92c47-380">*Creating an Album*</span></span>
3. <span data-ttu-id="92c47-381">Ověřte, že se přesměrujete na zobrazení indexu StoreManager, které obsahuje právě vytvořené nové album.</span><span class="sxs-lookup"><span data-stu-id="92c47-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="92c47-382">![Nové album vytvořeno](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "Nové album vytvořeno")</span><span class="sxs-lookup"><span data-stu-id="92c47-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="92c47-383">*Nové album vytvořeno*</span><span class="sxs-lookup"><span data-stu-id="92c47-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="92c47-384">Cvičení 5: zpracování odstranění</span><span class="sxs-lookup"><span data-stu-id="92c47-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="92c47-385">Možnost Odstranit alba ještě není naimplementovaná.</span><span class="sxs-lookup"><span data-stu-id="92c47-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="92c47-386">To je to, co se týká tohoto cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-386">This is what this exercise will be about.</span></span> <span data-ttu-id="92c47-387">Stejně jako dřív budete implementovat scénář odstranění pomocí dvou samostatných metod v rámci třídy **StoreManagerController** :</span><span class="sxs-lookup"><span data-stu-id="92c47-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="92c47-388">Jedna metoda akce zobrazí potvrzovací formulář.</span><span class="sxs-lookup"><span data-stu-id="92c47-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="92c47-389">Druhá metoda akce zpracuje odeslání formuláře.</span><span class="sxs-lookup"><span data-stu-id="92c47-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="92c47-390">Úloha 1 – implementace metody akce HTTP-GET DELETE</span><span class="sxs-lookup"><span data-stu-id="92c47-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="92c47-391">V této úloze implementujete verzi HTTP-GET metody akce DELETE pro načtení informací o albu.</span><span class="sxs-lookup"><span data-stu-id="92c47-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="92c47-392">Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex5-HandlingDeletion/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="92c47-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="92c47-393">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="92c47-394">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92c47-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="92c47-395">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92c47-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="92c47-396">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="92c47-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="92c47-397">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="92c47-398">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="92c47-399">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="92c47-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="92c47-400">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="92c47-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="92c47-401">Otevřete třídu **StoreManagerController** .</span><span class="sxs-lookup"><span data-stu-id="92c47-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="92c47-402">Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="92c47-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="92c47-403">Akce Odstranit řadič je přesně stejná jako předchozí akce kontroleru podrobností úložiště: dotazuje objekt **alba** z databáze pomocí **ID** zadaného v adrese URL a vrátí odpovídající **zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="92c47-404">Uděláte to tak, že nahradíte kód metody akce HTTP-GET **Delete** následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="92c47-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="92c47-405">(Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování – odstranění Ex5 zpracování http-získat akci odstranit*)</span><span class="sxs-lookup"><span data-stu-id="92c47-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="92c47-406">Klikněte pravým tlačítkem myši do metody **Delete** Action a vyberte **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="92c47-407">Tím se zobrazí dialogové okno Přidat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="92c47-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="92c47-408">V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **odstraněn**.</span><span class="sxs-lookup"><span data-stu-id="92c47-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="92c47-409">Vyberte možnost **vytvořit zobrazení silného typu** a v rozevíracím seznamu **třída modelu** vyberte **album (MvcMusicStore. model)** .</span><span class="sxs-lookup"><span data-stu-id="92c47-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="92c47-410">V rozevíracím seznamu **Šablona generování uživatelského rozhraní** vyberte **Odstranit** .</span><span class="sxs-lookup"><span data-stu-id="92c47-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="92c47-411">Ostatní pole ponechte výchozí hodnotou a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="92c47-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="92c47-412">![Přidání zobrazení pro odstranění](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Přidání zobrazení pro odstranění")</span><span class="sxs-lookup"><span data-stu-id="92c47-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="92c47-413">*Přidání zobrazení pro odstranění*</span><span class="sxs-lookup"><span data-stu-id="92c47-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="92c47-414">Šablona pro odstranění zobrazuje všechna pole z modelu.</span><span class="sxs-lookup"><span data-stu-id="92c47-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="92c47-415">Zobrazí se pouze název alba.</span><span class="sxs-lookup"><span data-stu-id="92c47-415">You will show only the album's title.</span></span> <span data-ttu-id="92c47-416">Chcete-li to provést, nahraďte obsah zobrazení následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="92c47-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="92c47-417">Úloha 2 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="92c47-418">V této úloze otestujete, že na stránce pro **odstranění** zobrazení **StoreManager** se zobrazí formulář pro odstranění potvrzení.</span><span class="sxs-lookup"><span data-stu-id="92c47-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="92c47-419">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-420">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-420">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-421">Změňte adresu URL na **/StoreManager**.</span><span class="sxs-lookup"><span data-stu-id="92c47-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="92c47-422">Vyberte jedno album, které chcete odstranit, kliknutím na **Odstranit** a ověřte, že se nové zobrazení nahraje.</span><span class="sxs-lookup"><span data-stu-id="92c47-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="92c47-423">![Odstranění alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Odstranění alba")</span><span class="sxs-lookup"><span data-stu-id="92c47-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="92c47-424">*Odstranění alba*</span><span class="sxs-lookup"><span data-stu-id="92c47-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="92c47-425">Úloha 3 – implementace metody akce odstranění HTTP-POST</span><span class="sxs-lookup"><span data-stu-id="92c47-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="92c47-426">V této úloze budete implementovat verzi HTTP-POST metody akce odstranění, která bude vyvolána, když uživatel klikne na tlačítko **Odstranit** .</span><span class="sxs-lookup"><span data-stu-id="92c47-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="92c47-427">Metoda by měla odstranit album v databázi.</span><span class="sxs-lookup"><span data-stu-id="92c47-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="92c47-428">V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92c47-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="92c47-429">Otevřete třídu **StoreManagerController** .</span><span class="sxs-lookup"><span data-stu-id="92c47-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="92c47-430">Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="92c47-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="92c47-431">Nahraďte kód metody akce **odstranění http-post** následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="92c47-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="92c47-432">(Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování-Ex5 akce odstranění http-post*)</span><span class="sxs-lookup"><span data-stu-id="92c47-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="92c47-433">Úloha 4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="92c47-434">V této úloze otestujete, že stránka zobrazení **StoreManager Delete** umožňuje odstranit album a pak přesměrovat do zobrazení indexu StoreManager.</span><span class="sxs-lookup"><span data-stu-id="92c47-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="92c47-435">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-436">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-436">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-437">Změňte adresu URL na **/StoreManager**.</span><span class="sxs-lookup"><span data-stu-id="92c47-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="92c47-438">Kliknutím na Odstranit vyberte jedno album, které chcete odstranit **.**</span><span class="sxs-lookup"><span data-stu-id="92c47-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="92c47-439">Potvrďte odstranění kliknutím na tlačítko **Odstranit** :</span><span class="sxs-lookup"><span data-stu-id="92c47-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="92c47-440">![Odstranění alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Odstranění alba")</span><span class="sxs-lookup"><span data-stu-id="92c47-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="92c47-441">*Odstranění alba*</span><span class="sxs-lookup"><span data-stu-id="92c47-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="92c47-442">Ověřte, že se album odstranilo, protože se nezobrazuje na stránce **index** .</span><span class="sxs-lookup"><span data-stu-id="92c47-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="92c47-443">Cvičení 6: Přidání ověřování</span><span class="sxs-lookup"><span data-stu-id="92c47-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="92c47-444">Formuláře pro vytváření a úpravy v současné době neprovádí žádný druh ověřování.</span><span class="sxs-lookup"><span data-stu-id="92c47-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="92c47-445">Pokud uživatel ponechá požadované pole prázdné nebo zadá písmena v poli Cena, první chyba, kterou získáte, bude z databáze.</span><span class="sxs-lookup"><span data-stu-id="92c47-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="92c47-446">Do aplikace můžete přidat ověřování přidáním datových poznámek ke třídě modelu.</span><span class="sxs-lookup"><span data-stu-id="92c47-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="92c47-447">Poznámky k datům umožňují popsat pravidla, která chcete použít pro vlastnosti modelu, a ASP.NET MVC se postará o vynucování a zobrazování příslušné zprávy pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="92c47-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="92c47-448">Úkol 1 – přidávání datových poznámek</span><span class="sxs-lookup"><span data-stu-id="92c47-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="92c47-449">V této úloze přidáte datové poznámky k modelu alba, ve kterém se v případě potřeby zobrazí zpráva pro vytvoření a úpravu stránky pro ověření.</span><span class="sxs-lookup"><span data-stu-id="92c47-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="92c47-450">Pro jednoduchou třídu modelu je přidání datové poznámky zpracováváno pouhým přidáním příkazu **using** pro **System. ComponentModel. DataAnnotation**a následným umístěním atributu **[required]** na příslušné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="92c47-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="92c47-451">V následujícím příkladu by vlastnost **Name** měla požadované pole v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="92c47-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="92c47-452">Toto je trochu složitější v případech, jako je tato aplikace, kde je vygenerována model EDM (Entity Data Model).</span><span class="sxs-lookup"><span data-stu-id="92c47-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="92c47-453">Pokud jste poznámky k datům přidali přímo do tříd modelu, budou přepsány při aktualizaci modelu z databáze.</span><span class="sxs-lookup"><span data-stu-id="92c47-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="92c47-454">Místo toho můžete použít částečné třídy metadat, které budou existovat pro uchování poznámek a jsou přidruženy ke třídám modelu pomocí atributu **[MetadataType]** .</span><span class="sxs-lookup"><span data-stu-id="92c47-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="92c47-455">Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex6-AddingValidation/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="92c47-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="92c47-456">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="92c47-457">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92c47-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="92c47-458">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92c47-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="92c47-459">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="92c47-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="92c47-460">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="92c47-461">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="92c47-462">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="92c47-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="92c47-463">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="92c47-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="92c47-464">Otevřete **album.cs** ze složky **modely** .</span><span class="sxs-lookup"><span data-stu-id="92c47-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="92c47-465">Nahraďte obsah **album.cs** zvýrazněným kódem, aby vypadal jako následující:</span><span class="sxs-lookup"><span data-stu-id="92c47-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="92c47-466">Řádek **[DisplayFormat (ConvertEmptyStringToNull = false)]** označuje, že prázdné řetězce z modelu nebudou převedeny na hodnotu null, pokud je datové pole aktualizováno ve zdroji dat.</span><span class="sxs-lookup"><span data-stu-id="92c47-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="92c47-467">Toto nastavení vyloučí výjimku, pokud Entity Framework přiřadí hodnoty null k modelu před tím, než datová Poznámka ověří pole.</span><span class="sxs-lookup"><span data-stu-id="92c47-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="92c47-468">(Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověření – částečná třída metadat alba Ex6*)</span><span class="sxs-lookup"><span data-stu-id="92c47-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="92c47-469">Tato částečná třída **alba** má atribut **MetadataType** , který odkazuje na třídu **AlbumMetaData** pro datové poznámky.</span><span class="sxs-lookup"><span data-stu-id="92c47-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="92c47-470">Jedná se o některé z atributů anotace dat, které používáte k přidání poznámky k modelu alba:</span><span class="sxs-lookup"><span data-stu-id="92c47-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="92c47-471">Required – označuje, že vlastnost je povinné pole.</span><span class="sxs-lookup"><span data-stu-id="92c47-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="92c47-472">DisplayName – definuje text, který se má použít u polí formuláře a ověřovacích zpráv.</span><span class="sxs-lookup"><span data-stu-id="92c47-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="92c47-473">DisplayFormat – určuje způsob zobrazení a formátování datových polí.</span><span class="sxs-lookup"><span data-stu-id="92c47-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="92c47-474">StringLength – definuje maximální délku pole řetězce.</span><span class="sxs-lookup"><span data-stu-id="92c47-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="92c47-475">Rozsah – poskytuje maximální a minimální hodnotu pro číselné pole.</span><span class="sxs-lookup"><span data-stu-id="92c47-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="92c47-476">ScaffoldColumn – umožňuje skrývání polí z formulářů editoru.</span><span class="sxs-lookup"><span data-stu-id="92c47-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="92c47-477">Úloha 2 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="92c47-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="92c47-478">V této úloze otestujete, že stránky pro vytváření a úpravy ověřují pole pomocí zobrazovaných názvů vybraných v posledním úkolu.</span><span class="sxs-lookup"><span data-stu-id="92c47-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="92c47-479">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="92c47-480">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-480">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-481">Změňte adresu URL na **/StoreManager/Create**.</span><span class="sxs-lookup"><span data-stu-id="92c47-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="92c47-482">Ověřte, že zobrazované názvy odpovídají těm v částečné třídě (jako je **Adresa URL obrázku alba** místo **AlbumArtUrl**).</span><span class="sxs-lookup"><span data-stu-id="92c47-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="92c47-483">Klikněte na **vytvořit**, aniž byste museli vyplnit formulář.</span><span class="sxs-lookup"><span data-stu-id="92c47-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="92c47-484">Ověřte, že se zobrazí odpovídající ověřovací zprávy.</span><span class="sxs-lookup"><span data-stu-id="92c47-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="92c47-485">![Ověřená pole na stránce vytvořit](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Ověřená pole na stránce vytvořit")</span><span class="sxs-lookup"><span data-stu-id="92c47-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="92c47-486">*Ověřená pole na stránce vytvořit*</span><span class="sxs-lookup"><span data-stu-id="92c47-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="92c47-487">Můžete ověřit, že se na stránce pro **Úpravy** dojde k stejnému.</span><span class="sxs-lookup"><span data-stu-id="92c47-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="92c47-488">Změňte adresu URL na **/StoreManager/Edit/1** a ověřte, že zobrazované názvy odpovídají těm, které jsou v částečné třídě (jako je **Adresa URL alba alba** místo **AlbumArtUrl**).</span><span class="sxs-lookup"><span data-stu-id="92c47-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="92c47-489">Vyprázdněte pole **název** a **Ceník** a klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="92c47-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="92c47-490">Ověřte, že se zobrazí odpovídající ověřovací zprávy.</span><span class="sxs-lookup"><span data-stu-id="92c47-490">Verify that you get the corresponding validation messages.</span></span>

    ![Ověřená pole na stránce pro úpravy](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="92c47-492">*Ověřená pole na stránce pro úpravy*</span><span class="sxs-lookup"><span data-stu-id="92c47-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="92c47-493">Cvičení 7: použití nenápadu jQuery na straně klienta</span><span class="sxs-lookup"><span data-stu-id="92c47-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="92c47-494">V tomto cvičení se dozvíte, jak povolit MVC 4 s nenáročném ověřování jQuery na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="92c47-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="92c47-495">Nezpůsobuje, že jQuery používá JavaScript s předponou data-AJAX k vyvolání metod akce na serveru místo rušivého vygenerování vložených klientských skriptů.</span><span class="sxs-lookup"><span data-stu-id="92c47-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="92c47-496">Úloha 1 – spuštění aplikace před tím, než se aktivuje nenáročná jQuery</span><span class="sxs-lookup"><span data-stu-id="92c47-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="92c47-497">V této úloze spustíte aplikaci před tím, než zadáte jQuery, aby bylo možné porovnat oba modely ověřování.</span><span class="sxs-lookup"><span data-stu-id="92c47-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="92c47-498">Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex7-UnobtrusivejQueryValidation/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="92c47-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="92c47-499">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="92c47-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="92c47-500">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92c47-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="92c47-501">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92c47-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="92c47-502">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="92c47-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="92c47-503">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="92c47-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="92c47-504">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="92c47-505">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="92c47-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="92c47-506">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="92c47-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="92c47-507">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="92c47-508">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-508">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-509">Přejděte na **/StoreManager/Create** a klikněte na **vytvořit** bez vyplnění formuláře, abyste ověřili, že se zobrazí ověřovací zprávy:</span><span class="sxs-lookup"><span data-stu-id="92c47-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="92c47-510">![Ověřování klienta zakázáno](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Ověřování klienta zakázáno")</span><span class="sxs-lookup"><span data-stu-id="92c47-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="92c47-511">*Ověřování klienta zakázáno*</span><span class="sxs-lookup"><span data-stu-id="92c47-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="92c47-512">V prohlížeči otevřete zdrojový kód HTML:</span><span class="sxs-lookup"><span data-stu-id="92c47-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="92c47-513">Úloha 2 – povolení nenáročného ověřování klienta</span><span class="sxs-lookup"><span data-stu-id="92c47-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="92c47-514">V této úloze povolíte v souboru **Web. config** , který je ve výchozím nastavení nastavené na hodnotu false, v každém novém projektu ASP.NET MVC 4 možnost jQuery neztratí **ověření klienta** .</span><span class="sxs-lookup"><span data-stu-id="92c47-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="92c47-515">Kromě toho přidáte potřebné odkazy na skripty, aby jQuery nenápadně fungovalo ověřování klienta.</span><span class="sxs-lookup"><span data-stu-id="92c47-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="92c47-516">Otevřete soubor **Web. config** v kořenovém adresáři projektu a ujistěte se, že hodnoty klíčů **ClientValidationEnabled** a **UnobtrusiveJavaScriptEnabled** jsou nastaveny na **hodnotu true**.</span><span class="sxs-lookup"><span data-stu-id="92c47-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="92c47-517">Můžete také povolit ověřování klientů pomocí kódu na Global.asax.cs a získat tak stejné výsledky:</span><span class="sxs-lookup"><span data-stu-id="92c47-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="92c47-518">**HtmlHelper. ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="92c47-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="92c47-519">Kromě toho můžete přiřadit atribut ClientValidationEnabled do libovolného kontroleru a mít tak vlastní chování.</span><span class="sxs-lookup"><span data-stu-id="92c47-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="92c47-520">Otevřete **vytvořit. cshtml** na adrese **Views\StoreManager**.</span><span class="sxs-lookup"><span data-stu-id="92c47-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="92c47-521">Zajistěte, aby se v zobrazení odkazovaly na následující soubory skriptu **jQuery. Validate** a **jQuery. Validate.** nepřehledy prostřednictvím &quot; **~/Bundles/jqueryval**&quot; sady.</span><span class="sxs-lookup"><span data-stu-id="92c47-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="92c47-522">Všechny tyto knihovny jQuery jsou zahrnuté v nových projektech MVC 4.</span><span class="sxs-lookup"><span data-stu-id="92c47-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="92c47-523">Další knihovny můžete najít ve složce **/Scripts** v projektu.</span><span class="sxs-lookup"><span data-stu-id="92c47-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="92c47-524">Aby bylo možné tyto knihovny ověřování fungovat, je třeba přidat odkaz na knihovnu jQuery Framework.</span><span class="sxs-lookup"><span data-stu-id="92c47-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="92c47-525">Vzhledem k tomu, že tento odkaz již byl přidán do souboru **\_layout. cshtml** , není nutné jej přidávat do tohoto konkrétního zobrazení.</span><span class="sxs-lookup"><span data-stu-id="92c47-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="92c47-526">Úloha 3 – spuštění aplikace pomocí nenápadu ověření jQuery</span><span class="sxs-lookup"><span data-stu-id="92c47-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="92c47-527">V této úloze otestujete, že šablona zobrazení **StoreManager** Create View provádí ověřování na straně klienta pomocí knihoven jQuery, když uživatel vytvoří nové album.</span><span class="sxs-lookup"><span data-stu-id="92c47-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="92c47-528">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="92c47-529">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="92c47-529">The project starts in the Home page.</span></span> <span data-ttu-id="92c47-530">Přejděte na **/StoreManager/Create** a klikněte na **vytvořit** bez vyplnění formuláře, abyste ověřili, že se zobrazí ověřovací zprávy:</span><span class="sxs-lookup"><span data-stu-id="92c47-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="92c47-531">![Ověření klienta s povoleným jQuery](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Ověření klienta s povoleným jQuery")</span><span class="sxs-lookup"><span data-stu-id="92c47-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="92c47-532">*Ověření klienta s povoleným jQuery*</span><span class="sxs-lookup"><span data-stu-id="92c47-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="92c47-533">V prohlížeči otevřete zdrojový kód pro vytvoření zobrazení:</span><span class="sxs-lookup"><span data-stu-id="92c47-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="92c47-534">U každého pravidla ověření klienta přidá příkaz jQuery atribut s data-Val-*rule*=&quot;&quot;*zprávy* .</span><span class="sxs-lookup"><span data-stu-id="92c47-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="92c47-535">Níže je uveden seznam značek, které nenápadí vložení jQuery do pole vstupu HTML k provedení ověření klienta:</span><span class="sxs-lookup"><span data-stu-id="92c47-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="92c47-536">Data – Val</span><span class="sxs-lookup"><span data-stu-id="92c47-536">Data-val</span></span>
   > - <span data-ttu-id="92c47-537">Data-Val-Number</span><span class="sxs-lookup"><span data-stu-id="92c47-537">Data-val-number</span></span>
   > - <span data-ttu-id="92c47-538">Data-Val-Range</span><span class="sxs-lookup"><span data-stu-id="92c47-538">Data-val-range</span></span>
   > - <span data-ttu-id="92c47-539">Data-Val-Range-min/data-Val-Range-max</span><span class="sxs-lookup"><span data-stu-id="92c47-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="92c47-540">Data-Val – povinné</span><span class="sxs-lookup"><span data-stu-id="92c47-540">Data-val-required</span></span>
   > - <span data-ttu-id="92c47-541">Data-Val-Length</span><span class="sxs-lookup"><span data-stu-id="92c47-541">Data-val-length</span></span>
   > - <span data-ttu-id="92c47-542">Data-Val-Length-Max/data-Val-Length-min.</span><span class="sxs-lookup"><span data-stu-id="92c47-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="92c47-543">Všechny hodnoty dat jsou vyplněny pomocí **poznámky k datům**modelu.</span><span class="sxs-lookup"><span data-stu-id="92c47-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="92c47-544">Veškerá logika, která funguje na straně serveru, se pak dá spustit na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="92c47-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="92c47-545">Například atribut Price má v modelu následující anotaci dat:</span><span class="sxs-lookup"><span data-stu-id="92c47-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="92c47-546">Po použití nenápadu jQuery je vygenerovaný kód:</span><span class="sxs-lookup"><span data-stu-id="92c47-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="92c47-547">Souhrn</span><span class="sxs-lookup"><span data-stu-id="92c47-547">Summary</span></span>

<span data-ttu-id="92c47-548">Díky tomuto praktickému cvičení jste se dozvěděli, jak uživatelům umožnit změnu dat uložených v databázi s použitím následujícího postupu:</span><span class="sxs-lookup"><span data-stu-id="92c47-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="92c47-549">Akce kontroleru, jako je index, vytvořit, upravit, odstranit</span><span class="sxs-lookup"><span data-stu-id="92c47-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="92c47-550">Funkce generování uživatelského rozhraní MVC pro ASP.NET pro zobrazení vlastností v tabulce HTML</span><span class="sxs-lookup"><span data-stu-id="92c47-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="92c47-551">Vlastní pomocníky HTML pro zlepšení uživatelského prostředí</span><span class="sxs-lookup"><span data-stu-id="92c47-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="92c47-552">Metody akcí, které reagují na volání HTTP-GET nebo HTTP-POST</span><span class="sxs-lookup"><span data-stu-id="92c47-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="92c47-553">Šablona sdíleného editoru pro podobné šablony zobrazení, jako je vytváření a úpravy</span><span class="sxs-lookup"><span data-stu-id="92c47-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="92c47-554">Formuláře, jako jsou rozevírací prvky</span><span class="sxs-lookup"><span data-stu-id="92c47-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="92c47-555">Datové poznámky pro ověřování modelu</span><span class="sxs-lookup"><span data-stu-id="92c47-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="92c47-556">Ověřování na straně klienta pomocí knihovny jQuery – nenáročná knihovna</span><span class="sxs-lookup"><span data-stu-id="92c47-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="92c47-557">Příloha A: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="92c47-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="92c47-558">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="92c47-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="92c47-559">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="92c47-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="92c47-560">Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="92c47-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="92c47-561">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="92c47-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="92c47-562">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="92c47-562">Click on **Install Now**.</span></span> <span data-ttu-id="92c47-563">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="92c47-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="92c47-564">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="92c47-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="92c47-565">![Nainstalovat Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="92c47-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="92c47-566">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="92c47-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="92c47-567">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="92c47-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="92c47-569">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="92c47-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="92c47-570">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="92c47-570">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="92c47-572">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="92c47-572">*Installation progress*</span></span>
6. <span data-ttu-id="92c47-573">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="92c47-573">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="92c47-575">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="92c47-575">*Installation completed*</span></span>
7. <span data-ttu-id="92c47-576">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="92c47-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="92c47-577">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="92c47-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="92c47-579">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="92c47-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="92c47-580">Příloha B: použití fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="92c47-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="92c47-581">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="92c47-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="92c47-582">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="92c47-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="92c47-583">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="92c47-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="92c47-584">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="92c47-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="92c47-585">***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="92c47-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="92c47-586">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="92c47-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="92c47-587">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="92c47-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="92c47-588">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="92c47-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="92c47-589">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="92c47-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="92c47-590">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="92c47-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="92c47-591">![Začněte psát název fragmentu.](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="92c47-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="92c47-592">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="92c47-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="92c47-593">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="92c47-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="92c47-594">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="92c47-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="92c47-595">![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="92c47-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="92c47-596">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="92c47-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="92c47-597">***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první.</span><span class="sxs-lookup"><span data-stu-id="92c47-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="92c47-598">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="92c47-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="92c47-599">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="92c47-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="92c47-600">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="92c47-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="92c47-601">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="92c47-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="92c47-602">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="92c47-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="92c47-603">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="92c47-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="92c47-604">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="92c47-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
