---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 – modely a přístup k datům | Microsoft Docs
author: rick-anderson
description: 'Poznámka: Toto praktické cvičení předpokládá, že máte základní znalosti o ASP.NET MVC. Pokud jste ještě ASP.NET MVC nepoužívali, doporučujeme, abyste přešli na ASP.NET MVC 4...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560198"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="f9c06-104">ASP.NET MVC 4 – modely a přístup k datům</span><span class="sxs-lookup"><span data-stu-id="f9c06-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="f9c06-105">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f9c06-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="f9c06-106">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="f9c06-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="f9c06-107">Tato praktická cvičení předpokládá, že máte základní znalosti o **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="f9c06-108">Pokud jste ještě **ASP.NET MVC** nepoužívali, doporučujeme, abyste si převzali v praxi **ASP.NET MVC 4** pro praktické cvičení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="f9c06-109">Toto testovací prostředí vás provede vylepšeními a novými funkcemi, které jsme dříve popsali pomocí menších změn ve vzorové webové aplikaci, která je součástí zdrojové složky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c06-110">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="f9c06-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="f9c06-111">Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NET modelech MVC 4 a přístup k datům](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span><span class="sxs-lookup"><span data-stu-id="f9c06-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="f9c06-112">V **ASP.NET MVC** se praktická praktická cvičení předáváte pevně zakódovaným datům z řadičů do šablon zobrazení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="f9c06-113">Pro vytvoření reálné webové aplikace ale můžete chtít použít skutečnou databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="f9c06-114">Tato praktická cvičení vám ukáže, jak používat databázový stroj, aby bylo možné ukládat a načítat data potřebná pro aplikaci pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="f9c06-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="f9c06-115">K tomu je potřeba začít s existující databází a vytvořit z ní model EDM (Entity Data Model).</span><span class="sxs-lookup"><span data-stu-id="f9c06-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="f9c06-116">V rámci tohoto testovacího prostředí budete splňovat **Database First** přístup a také **Code First** přístup.</span><span class="sxs-lookup"><span data-stu-id="f9c06-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="f9c06-117">Můžete ale také použít **model First** přístup, vytvořit stejný model pomocí nástrojů a pak z něj vygenerovat databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="f9c06-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span><span class="sxs-lookup"><span data-stu-id="f9c06-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="f9c06-119">*Database First vs. Model First*</span><span class="sxs-lookup"><span data-stu-id="f9c06-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="f9c06-120">Po vygenerování modelu provedete v StoreController správné úpravy, abyste poskytovali zobrazení ze Storu s daty potřebnými z databáze namísto použití pevně zakódovaných dat.</span><span class="sxs-lookup"><span data-stu-id="f9c06-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="f9c06-121">Nebudete muset dělat žádné změny v šablonách zobrazení, protože StoreController vrátí stejný ViewModels k šablonám zobrazení, i když to bude čas od databáze pocházet.</span><span class="sxs-lookup"><span data-stu-id="f9c06-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="f9c06-122">**Code First přístup**</span><span class="sxs-lookup"><span data-stu-id="f9c06-122">**The Code First Approach**</span></span>

<span data-ttu-id="f9c06-123">Code First přístup nám umožňuje definovat model z kódu bez generování tříd, které jsou obecně spojeny s rozhraním.</span><span class="sxs-lookup"><span data-stu-id="f9c06-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="f9c06-124">V kódu nejprve objekty modelu jsou definovány s POCOs, &quot;é obyčejné staré objekty CLR&quot;.</span><span class="sxs-lookup"><span data-stu-id="f9c06-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="f9c06-125">POCOs jsou jednoduché jednoduché třídy, které nemají žádnou dědičnost a neimplementují rozhraní.</span><span class="sxs-lookup"><span data-stu-id="f9c06-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="f9c06-126">Z nich můžeme automaticky vygenerovat databázi nebo můžeme použít stávající databázi a vytvořit mapování třídy z kódu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="f9c06-127">Výhodami použití tohoto přístupu je, že model zůstává nezávisle na rozhraní Persistence (v tomto případě Entity Framework), protože třídy POCOs nejsou spojeny s rozhraním Mapping Framework.</span><span class="sxs-lookup"><span data-stu-id="f9c06-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c06-128">Toto testovací prostředí vychází z ASP.NET MVC 4 a verze ukázkové aplikace pro hudební úložiště, která je přizpůsobená a minimalizovaná tak, aby odpovídala pouze funkcím uvedeným v tomto praktickém testovacím prostředí.</span><span class="sxs-lookup"><span data-stu-id="f9c06-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="f9c06-129">Pokud si chcete projít celou výukovou aplikaci pro **obchod s hudbou** , najdete ji v [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="f9c06-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f9c06-130">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="f9c06-130">Prerequisites</span></span>

<span data-ttu-id="f9c06-131">K dokončení tohoto testovacího prostředí musíte mít následující položky:</span><span class="sxs-lookup"><span data-stu-id="f9c06-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f9c06-132">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).</span><span class="sxs-lookup"><span data-stu-id="f9c06-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f9c06-133">Nastavení</span><span class="sxs-lookup"><span data-stu-id="f9c06-133">Setup</span></span>

<span data-ttu-id="f9c06-134">**Instalace fragmentů kódu**</span><span class="sxs-lookup"><span data-stu-id="f9c06-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="f9c06-135">Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9c06-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f9c06-136">Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f9c06-137">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze C: použití fragmentů kódu](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="f9c06-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f9c06-138">Cvičení</span><span class="sxs-lookup"><span data-stu-id="f9c06-138">Exercises</span></span>

<span data-ttu-id="f9c06-139">Tato praktická cvičení se skládají z následujících cvičení:</span><span class="sxs-lookup"><span data-stu-id="f9c06-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="f9c06-140">Cvičení 1: Přidání databáze</span><span class="sxs-lookup"><span data-stu-id="f9c06-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="f9c06-141">Cvičení 2: vytvoření databáze pomocí Code First</span><span class="sxs-lookup"><span data-stu-id="f9c06-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="f9c06-142">Cvičení 3: dotazování databáze s parametry</span><span class="sxs-lookup"><span data-stu-id="f9c06-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="f9c06-143">Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="f9c06-144">Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="f9c06-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="f9c06-145">Odhadovaný čas dokončení tohoto testovacího prostředí: **35 minut**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="f9c06-146">Cvičení 1: Přidání databáze</span><span class="sxs-lookup"><span data-stu-id="f9c06-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="f9c06-147">V tomto cvičení se dozvíte, jak do řešení přidat databázi s tabulkami aplikace MusicStore, aby se mohla využívat jejich data.</span><span class="sxs-lookup"><span data-stu-id="f9c06-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="f9c06-148">Jakmile je databáze generována s modelem a přidána do řešení, upravíte třídu StoreController, aby poskytovala šablonu zobrazení s daty z databáze namísto použití pevně zakódovaných hodnot.</span><span class="sxs-lookup"><span data-stu-id="f9c06-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="f9c06-149">Úloha 1 – Přidání databáze</span><span class="sxs-lookup"><span data-stu-id="f9c06-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="f9c06-150">V této úloze přidáte již vytvořenou databázi s hlavními tabulkami aplikace MusicStore do řešení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="f9c06-151">Otevřete řešení **zahájit** , které se nachází ve složce **source/EX1-AddingADatabaseDBFirst/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f9c06-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="f9c06-152">Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9c06-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f9c06-153">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f9c06-154">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f9c06-155">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f9c06-156">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f9c06-157">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="f9c06-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f9c06-158">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f9c06-159">Přidat soubor databáze **MvcMusicStore**</span><span class="sxs-lookup"><span data-stu-id="f9c06-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="f9c06-160">V tomto praktickém testovacím prostředí budete používat už vytvořenou databázi s názvem **MvcMusicStore. mdf**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="f9c06-161">Provedete to tak, že kliknete pravým tlačítkem na složku **Data\_aplikace** , přejdete na **Přidat** a potom kliknete na **existující položka**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="f9c06-162">Přejděte na **\Source\Assets** a vyberte soubor **MvcMusicStore. mdf** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="f9c06-163">![Přidání existující položky](aspnet-mvc-4-models-and-data-access/_static/image2.png "Přidání existující položky")</span><span class="sxs-lookup"><span data-stu-id="f9c06-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="f9c06-164">*Přidání existující položky*</span><span class="sxs-lookup"><span data-stu-id="f9c06-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="f9c06-165">![Soubor databáze MvcMusicStore. mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "Soubor databáze MvcMusicStore. mdf")</span><span class="sxs-lookup"><span data-stu-id="f9c06-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="f9c06-166">*Soubor databáze MvcMusicStore. mdf*</span><span class="sxs-lookup"><span data-stu-id="f9c06-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="f9c06-167">Databáze byla přidána do projektu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-167">The database has been added to the project.</span></span> <span data-ttu-id="f9c06-168">I v případě, že se databáze nachází v řešení, můžete ji dotazovat a aktualizovat, protože byla hostována na jiném databázovém serveru.</span><span class="sxs-lookup"><span data-stu-id="f9c06-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="f9c06-169">![Databáze MvcMusicStore v Průzkumník řešení](aspnet-mvc-4-models-and-data-access/_static/image4.png "Databáze MvcMusicStore v Průzkumník řešení")</span><span class="sxs-lookup"><span data-stu-id="f9c06-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="f9c06-170">*Databáze MvcMusicStore v Průzkumník řešení*</span><span class="sxs-lookup"><span data-stu-id="f9c06-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="f9c06-171">Ověřte připojení k databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-171">Verify the connection to the database.</span></span> <span data-ttu-id="f9c06-172">Chcete-li to provést, dvakrát klikněte na **MvcMusicStore. mdf** pro navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="f9c06-173">![Připojování k MvcMusicStore. mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Připojování k MvcMusicStore. mdf")</span><span class="sxs-lookup"><span data-stu-id="f9c06-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="f9c06-174">*Připojování k MvcMusicStore. mdf*</span><span class="sxs-lookup"><span data-stu-id="f9c06-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="f9c06-175">Úloha 2 – Vytvoření datového modelu</span><span class="sxs-lookup"><span data-stu-id="f9c06-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="f9c06-176">V této úloze vytvoříte datový model, který bude pracovat s databází přidanou v předchozí úloze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="f9c06-177">Vytvořte datový model, který bude představovat databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="f9c06-178">Chcete-li to provést, klikněte v Průzkumník řešení pravým tlačítkem myši na složku **modely** , přejděte na **Přidat** a klikněte na **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="f9c06-179">V dialogovém okně **Přidat novou položku** vyberte šablonu **dat** a pak položku **ADO.NET model EDM (Entity Data Model)** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="f9c06-180">Změňte název datového modelu na **StoreDB. edmx** a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="f9c06-181">![Přidání model EDM (Entity Data Model) StoreDB ADO.NET](aspnet-mvc-4-models-and-data-access/_static/image6.png "Přidání model EDM (Entity Data Model) StoreDB ADO.NET")</span><span class="sxs-lookup"><span data-stu-id="f9c06-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="f9c06-182">*Přidání model EDM (Entity Data Model) StoreDB ADO.NET*</span><span class="sxs-lookup"><span data-stu-id="f9c06-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="f9c06-183">Zobrazí se **průvodce model EDM (Entity Data Model)** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="f9c06-184">Tento průvodce vás provede vytvořením vrstvy modelu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="f9c06-185">Vzhledem k tomu, že se model má vytvořit na základě nedávno přidané existující databáze, vyberte **Generovat z databáze** a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="f9c06-186">![Výběr obsahu modelu](aspnet-mvc-4-models-and-data-access/_static/image7.png "Výběr obsahu modelu")</span><span class="sxs-lookup"><span data-stu-id="f9c06-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="f9c06-187">*Výběr obsahu modelu*</span><span class="sxs-lookup"><span data-stu-id="f9c06-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="f9c06-188">Vzhledem k tomu, že generujete model z databáze, budete muset zadat připojení, které se má použít.</span><span class="sxs-lookup"><span data-stu-id="f9c06-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="f9c06-189">Klikněte na **nové připojení**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="f9c06-190">Vyberte **Microsoft SQL Server soubor databáze** a klikněte na **pokračovat**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="f9c06-191">![Zvolit zdroj dat](aspnet-mvc-4-models-and-data-access/_static/image8.png "Zvolit zdroj dat")</span><span class="sxs-lookup"><span data-stu-id="f9c06-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="f9c06-192">*Dialog zvolit zdroj dat*</span><span class="sxs-lookup"><span data-stu-id="f9c06-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="f9c06-193">Klikněte na **Procházet** a vyberte databázi **MvcMusicStore. mdf** umístěnou ve složce **App\_data** a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="f9c06-194">![Vlastnosti připojení](aspnet-mvc-4-models-and-data-access/_static/image9.png "Vlastnosti připojení")</span><span class="sxs-lookup"><span data-stu-id="f9c06-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="f9c06-195">*Vlastnosti připojení*</span><span class="sxs-lookup"><span data-stu-id="f9c06-195">*Connection properties*</span></span>
6. <span data-ttu-id="f9c06-196">Vygenerovaná třída by měla mít stejný název jako připojovací řetězec entity, proto změňte její název na **MusicStoreEntities** a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="f9c06-197">![Výběr datového připojení](aspnet-mvc-4-models-and-data-access/_static/image10.png "Výběr datového připojení")</span><span class="sxs-lookup"><span data-stu-id="f9c06-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="f9c06-198">*Výběr datového připojení*</span><span class="sxs-lookup"><span data-stu-id="f9c06-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="f9c06-199">Vyberte databázové objekty, které chcete použít.</span><span class="sxs-lookup"><span data-stu-id="f9c06-199">Choose the database objects to use.</span></span> <span data-ttu-id="f9c06-200">Protože model entity bude používat pouze tabulky databáze, vyberte možnost **tabulky** a ujistěte se, že jsou vybrány také **sloupce zahrnout cizí klíče v modelu** a **doplnit jednotné nebo množné číslo vygenerované názvy objektů** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="f9c06-201">Změňte obor názvů modelu na **MvcMusicStore. model** a klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="f9c06-202">![Výběr databázových objektů](aspnet-mvc-4-models-and-data-access/_static/image11.png "Výběr databázových objektů")</span><span class="sxs-lookup"><span data-stu-id="f9c06-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="f9c06-203">*Výběr databázových objektů*</span><span class="sxs-lookup"><span data-stu-id="f9c06-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9c06-204">Pokud se zobrazí dialogové okno upozornění zabezpečení, kliknutím na tlačítko **OK** spusťte šablonu a vygenerujte třídy pro entity modelu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="f9c06-205">Bude se zobrazovat diagram entit pro databázi, zatímco bude vytvořena samostatná třída, která mapuje každou tabulku na databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="f9c06-206">Například tabulka **alba** bude reprezentovaná třídou **alba** , kde každý sloupec v tabulce se namapuje na vlastnost třídy.</span><span class="sxs-lookup"><span data-stu-id="f9c06-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="f9c06-207">To vám umožní dotazovat se na objekty, které reprezentují řádky v databázi, a pracovat s nimi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="f9c06-208">![Diagram entit](aspnet-mvc-4-models-and-data-access/_static/image12.png "Diagram entit")</span><span class="sxs-lookup"><span data-stu-id="f9c06-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="f9c06-209">*Diagram entit*</span><span class="sxs-lookup"><span data-stu-id="f9c06-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9c06-210">Šablony T4 (. TT) spouštějí kód pro generování tříd entit a přepíše existující třídy se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="f9c06-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="f9c06-211">V tomto příkladu třídy &quot;alba&quot;, &quot;Žánr&quot; a &quot;umělec&quot; byly přepsány generovaným kódem.</span><span class="sxs-lookup"><span data-stu-id="f9c06-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="f9c06-212">Úloha 3 – sestavování aplikace</span><span class="sxs-lookup"><span data-stu-id="f9c06-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="f9c06-213">V této úloze zkontrolujete, že i když generování modelu odebralo třídy **alba**, **žánru** a **interpretu** , sestavení projektu bylo úspěšné pomocí nových tříd datového modelu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="f9c06-214">Sestavte projekt výběrem položky nabídky **sestavení** a poté **Sestavte MvcMusicStore**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="f9c06-215">![Sestavení projektu](aspnet-mvc-4-models-and-data-access/_static/image13.png "Sestavení projektu")</span><span class="sxs-lookup"><span data-stu-id="f9c06-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="f9c06-216">*Sestavení projektu*</span><span class="sxs-lookup"><span data-stu-id="f9c06-216">*Building the project*</span></span>
2. <span data-ttu-id="f9c06-217">Sestavení projektu bylo úspěšné.</span><span class="sxs-lookup"><span data-stu-id="f9c06-217">The project builds successfully.</span></span> <span data-ttu-id="f9c06-218">Proč to pořád funguje?</span><span class="sxs-lookup"><span data-stu-id="f9c06-218">Why does it still work?</span></span> <span data-ttu-id="f9c06-219">Tento postup funguje, protože tabulky databáze obsahují pole obsahující vlastnosti, které jste použili v **albu** a **žánru**odebraných tříd.</span><span class="sxs-lookup"><span data-stu-id="f9c06-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="f9c06-220">![Sestavení byla úspěšná](aspnet-mvc-4-models-and-data-access/_static/image14.png "Sestavení byla úspěšná")</span><span class="sxs-lookup"><span data-stu-id="f9c06-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="f9c06-221">*Sestavení byla úspěšná*</span><span class="sxs-lookup"><span data-stu-id="f9c06-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="f9c06-222">Zatímco Návrhář zobrazuje entity ve formátu diagramu, jsou ve skutečnosti C# třídy.</span><span class="sxs-lookup"><span data-stu-id="f9c06-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="f9c06-223">Rozbalte uzel **StoreDB. edmx** v Průzkumník řešení a potom **StoreDB.TT**se zobrazí nové vygenerované entity.</span><span class="sxs-lookup"><span data-stu-id="f9c06-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="f9c06-224">![Generované soubory](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generované soubory")</span><span class="sxs-lookup"><span data-stu-id="f9c06-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="f9c06-225">*Generované soubory*</span><span class="sxs-lookup"><span data-stu-id="f9c06-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="f9c06-226">Úloha 4 – dotazování databáze</span><span class="sxs-lookup"><span data-stu-id="f9c06-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="f9c06-227">V této úloze aktualizujete třídu StoreController tak, aby namísto použití dat pevně zakódované se dotazoval na databázi, aby se načetly informace.</span><span class="sxs-lookup"><span data-stu-id="f9c06-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="f9c06-228">Otevřete **Controllers\StoreController.cs** a přidejte do třídy následující pole pro uložení instance třídy **MusicStoreEntities** s názvem **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="f9c06-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="f9c06-229">(Fragment kódu – *modely a přístup k datům – EX1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="f9c06-230">Třída **MusicStoreEntities** zpřístupňuje vlastnost kolekce pro každou tabulku v databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="f9c06-231">Aktualizujte metodu akce **procházení** a načtěte Žánr se všemi **alba**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="f9c06-232">(Fragment kódu – *modely a přístup k datům – EX1 Store – procházení*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="f9c06-233">Používáte funkci rozhraní .NET s názvem **LINQ** (jazykově integrovaný dotaz) k zápisu výrazů dotazů silně typovaného na tyto kolekce – což spustí kód pro databázi a vrátí objekty, pro které lze programovat.</span><span class="sxs-lookup"><span data-stu-id="f9c06-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="f9c06-234">Další informace o LINQ najdete na [webu MSDN](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9c06-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="f9c06-235">Aktualizujte metodu akce **indexu** , aby se načetly všechny žánry.</span><span class="sxs-lookup"><span data-stu-id="f9c06-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="f9c06-236">(Fragment kódu – *modely a přístup k datům – index úložiště EX1*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="f9c06-237">Aktualizujte metodu akce **indexu** pro načtení všech žánrů a transformaci kolekce na seznam.</span><span class="sxs-lookup"><span data-stu-id="f9c06-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="f9c06-238">(Fragment kódu – *modely a přístup k datům – EX1 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="f9c06-239">Úloha 5 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="f9c06-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="f9c06-240">V této úloze zkontrolujete, že se na stránce index úložiště nyní zobrazí žánry uložené v databázi místo pevně zakódované.</span><span class="sxs-lookup"><span data-stu-id="f9c06-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="f9c06-241">Nemusíte měnit šablonu zobrazení, protože **StoreController** vrací stejné entity jako předtím, i když data pocházejí z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="f9c06-242">Znovu sestavte řešení a stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f9c06-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f9c06-243">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="f9c06-243">The project starts in the Home page.</span></span> <span data-ttu-id="f9c06-244">Ověřte, že nabídka **žánrů** již není seznam pevně zakódované a data jsou přímo načtena z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="f9c06-246">*Procházení žánrů z databáze*</span><span class="sxs-lookup"><span data-stu-id="f9c06-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="f9c06-247">Teď přejděte na libovolný Žánr a ověřte, jestli jsou alba naplněná z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="f9c06-248">![Procházení alb z databáze](aspnet-mvc-4-models-and-data-access/_static/image17.png "Procházení alb z databáze")</span><span class="sxs-lookup"><span data-stu-id="f9c06-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="f9c06-249">*Procházení alb z databáze*</span><span class="sxs-lookup"><span data-stu-id="f9c06-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="f9c06-250">Cvičení 2: vytvoření databáze pomocí Code First</span><span class="sxs-lookup"><span data-stu-id="f9c06-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="f9c06-251">V tomto cvičení se naučíte, jak pomocí Code Firstho přístupu vytvořit databázi s tabulkami aplikace MusicStore a jak přistupovat k datům.</span><span class="sxs-lookup"><span data-stu-id="f9c06-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="f9c06-252">Po vygenerování modelu upravíte StoreController tak, aby poskytoval šablonu zobrazení s daty vytvořenými z databáze namísto použití hodnot pevně zakódované.</span><span class="sxs-lookup"><span data-stu-id="f9c06-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c06-253">Pokud jste dokončili cvičení 1 a již jste pracovali s přístupem Database First, nyní se dozvíte, jak získat stejné výsledky s jiným procesem.</span><span class="sxs-lookup"><span data-stu-id="f9c06-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="f9c06-254">Úkoly společné s cvičením 1 byly označeny pro usnadnění čtení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="f9c06-255">Pokud jste nedokončili cvičení 1, ale chtěli byste se naučit Code Firstý přístup, můžete začít z tohoto cvičení a získat úplné pokrytí tématu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="f9c06-256">Úloha 1 – vyplnění ukázkových dat</span><span class="sxs-lookup"><span data-stu-id="f9c06-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="f9c06-257">V této úloze naplníte databázi ukázkovými daty při jejím prvním vytvoření pomocí kódu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="f9c06-258">Otevřete řešení **zahájit** , které se nachází ve složce **source/EX2-CreatingADatabaseCodeFirst/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="f9c06-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="f9c06-259">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f9c06-260">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9c06-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f9c06-261">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f9c06-262">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f9c06-263">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f9c06-264">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f9c06-265">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="f9c06-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f9c06-266">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f9c06-267">Přidejte soubor **sampleData.cs** do složky **modely** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="f9c06-268">Provedete to tak, že kliknete pravým tlačítkem na složku **modely** , najeďte na **Přidat** a potom kliknete na **existující položka**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="f9c06-269">Přejděte na **\Source\Assets** a vyberte soubor **sampleData.cs** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="f9c06-270">![Kód pro vyplnění ukázkových dat](aspnet-mvc-4-models-and-data-access/_static/image18.png "Kód pro vyplnění ukázkových dat")</span><span class="sxs-lookup"><span data-stu-id="f9c06-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="f9c06-271">*Kód pro vyplnění ukázkových dat*</span><span class="sxs-lookup"><span data-stu-id="f9c06-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="f9c06-272">Otevřete soubor **Global.asax.cs** a přidejte následující příkazy *using* .</span><span class="sxs-lookup"><span data-stu-id="f9c06-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="f9c06-273">(Fragment kódu – *modely a přístup k datům – EX2 Global asax používá*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="f9c06-274">V metodě **aplikace\_Start ()** přidejte následující řádek pro nastavení inicializátoru databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="f9c06-275">(Fragment kódu – *modely a přístup k datům – EX2 Global asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="f9c06-276">Úloha 2 – konfigurace připojení k databázi</span><span class="sxs-lookup"><span data-stu-id="f9c06-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="f9c06-277">Teď, když jste již přidali databázi do našeho projektu, budete do souboru **Web. config** napsáni připojovacím řetězcem.</span><span class="sxs-lookup"><span data-stu-id="f9c06-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="f9c06-278">Přidat připojovací řetězec do **souboru Web. config**. Provedete to tak, že otevřete soubor **Web. config** v kořenovém adresáři projektu a nahradíte připojovací řetězec s názvem DefaultConnection tímto řádkem v části **&lt;connectionStrings&gt;** oddíl:</span><span class="sxs-lookup"><span data-stu-id="f9c06-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="f9c06-279">![Umístění souboru Web. config](aspnet-mvc-4-models-and-data-access/_static/image19.png "Umístění souboru Web. config")</span><span class="sxs-lookup"><span data-stu-id="f9c06-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="f9c06-280">*Umístění souboru Web. config*</span><span class="sxs-lookup"><span data-stu-id="f9c06-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="f9c06-281">Úloha 3 – práce s modelem</span><span class="sxs-lookup"><span data-stu-id="f9c06-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="f9c06-282">Teď, když už máte nakonfigurované připojení k databázi, propojíte model s databázovými tabulkami.</span><span class="sxs-lookup"><span data-stu-id="f9c06-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="f9c06-283">V této úloze vytvoříte třídu, která bude propojena s databází pomocí Code First.</span><span class="sxs-lookup"><span data-stu-id="f9c06-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="f9c06-284">Mějte na paměti, že existuje existující třída modelu POCO, která by se měla upravovat.</span><span class="sxs-lookup"><span data-stu-id="f9c06-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c06-285">Pokud jste dokončili cvičení 1, poznamenejte si, že tento krok byl proveden průvodcem.</span><span class="sxs-lookup"><span data-stu-id="f9c06-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="f9c06-286">Tím, že provádíte Code First, ručně vytvoříte třídy, které budou propojeny s datovými entitami.</span><span class="sxs-lookup"><span data-stu-id="f9c06-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="f9c06-287">Otevřete **Žánr** třídy modelu POCO ze složky projektu **modelů** a zahrňte ID.</span><span class="sxs-lookup"><span data-stu-id="f9c06-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="f9c06-288">Použijte vlastnost int s názvem **GenreId**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="f9c06-289">(Fragment kódu – *modely a přístup k datům – Ex2 Code First Žánr*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="f9c06-290">Chcete-li pracovat s konvencemi Code First, musí mít Žánr třídy vlastnost primárního klíče, která bude automaticky rozpoznána.</span><span class="sxs-lookup"><span data-stu-id="f9c06-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="f9c06-291">Další informace o konvencích pro Code First najdete v tomto [článku na webu MSDN](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9c06-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="f9c06-292">Nyní otevřete **album** třídy modelu POCO ze složky projekt **modelů** a zahrňte cizí klíče a vytvořte vlastnosti s názvy **GenreId** a **ArtistId**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="f9c06-293">Tato třída již má **GenreId** pro primární klíč.</span><span class="sxs-lookup"><span data-stu-id="f9c06-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="f9c06-294">(Fragment kódu – *modely a přístup k datům – Ex2 Code First alba*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="f9c06-295">Otevřete **Interpret** třídy modelu POCO a zahrňte vlastnost **ArtistId** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="f9c06-296">(Fragment kódu – *modely a přístup k datům – Ex2 Code First Interpret*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="f9c06-297">Klikněte pravým tlačítkem na složku projekt **modelů** a vyberte **Přidat | Třída**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="f9c06-298">Název souboru **MusicStoreEntities.cs**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="f9c06-299">Pak klikněte na tlačítko **Přidat.**</span><span class="sxs-lookup"><span data-stu-id="f9c06-299">Then, click **Add.**</span></span>

    <span data-ttu-id="f9c06-300">![Přidání třídy](aspnet-mvc-4-models-and-data-access/_static/image20.png "Přidání třídy")</span><span class="sxs-lookup"><span data-stu-id="f9c06-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="f9c06-301">*Přidání nové položky*</span><span class="sxs-lookup"><span data-stu-id="f9c06-301">*Adding a new item*</span></span>

    <span data-ttu-id="f9c06-302">![Přidání Class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Přidání Class2")</span><span class="sxs-lookup"><span data-stu-id="f9c06-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="f9c06-303">*Přidání třídy*</span><span class="sxs-lookup"><span data-stu-id="f9c06-303">*Adding a class*</span></span>
5. <span data-ttu-id="f9c06-304">Otevřete třídu, kterou jste právě vytvořili, **MusicStoreEntities.cs**a vložte obory názvů **System. data. entity** a **System. data. entity. Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="f9c06-305">Nahraďte deklaraci třídy za účelem rozšiřování třídy **DbContext** : deklarujte veřejnou **negenerickými** a přepište metodu **OnModelCreating** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="f9c06-306">Po provedení tohoto kroku získáte doménovou třídu, která bude propojit váš model s Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="f9c06-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="f9c06-307">Aby to bylo možné, nahraďte kód třídy následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="f9c06-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="f9c06-308">(Fragment kódu – *modely a přístup k datům – Ex2 Code First MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="f9c06-309">Pomocí Entity Framework **DbContext** a **negenerickými** budete moci zadat dotaz na Žánr třídy POCO.</span><span class="sxs-lookup"><span data-stu-id="f9c06-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="f9c06-310">Rozšířením metody **OnModelCreating** zadáte v **kódu** , jak bude Žánr mapován na databázovou tabulku.</span><span class="sxs-lookup"><span data-stu-id="f9c06-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="f9c06-311">Další informace o DBContext a Negenerickými najdete v tomto článku na webu MSDN: [odkaz](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="f9c06-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="f9c06-312">Úloha 4 – dotazování databáze</span><span class="sxs-lookup"><span data-stu-id="f9c06-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="f9c06-313">V této úloze aktualizujete třídu StoreController tak, aby namísto použití dat pevně zakódované se načetla z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c06-314">Tato úloha je společná s cvičením 1.</span><span class="sxs-lookup"><span data-stu-id="f9c06-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="f9c06-315">Pokud jste dokončili cvičení 1, Všimněte si, že tyto kroky jsou stejné v obou případech (první databáze nebo kód Code First).</span><span class="sxs-lookup"><span data-stu-id="f9c06-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="f9c06-316">Liší se v tom, jak jsou data propojena s modelem, ale přístup k datovým entitám je z kontroleru transparentní.</span><span class="sxs-lookup"><span data-stu-id="f9c06-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>

1. <span data-ttu-id="f9c06-317">Otevřete **Controllers\StoreController.cs** a přidejte do třídy následující pole pro uložení instance třídy **MusicStoreEntities** s názvem **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="f9c06-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="f9c06-318">(Fragment kódu – *modely a přístup k datům – EX1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="f9c06-319">Třída **MusicStoreEntities** zpřístupňuje vlastnost kolekce pro každou tabulku v databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="f9c06-320">Aktualizujte metodu akce **procházení** a načtěte Žánr se všemi **alba**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="f9c06-321">(Fragment kódu – *modely a přístup k datům – EX2 Store – procházení*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="f9c06-322">Používáte funkci rozhraní .NET s názvem **LINQ** (jazykově integrovaný dotaz) k zápisu výrazů dotazů silně typovaného na tyto kolekce – což spustí kód pro databázi a vrátí objekty, pro které lze programovat.</span><span class="sxs-lookup"><span data-stu-id="f9c06-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="f9c06-323">Další informace o LINQ najdete na [webu MSDN](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="f9c06-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="f9c06-324">Aktualizujte metodu akce **indexu** , aby se načetly všechny žánry.</span><span class="sxs-lookup"><span data-stu-id="f9c06-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="f9c06-325">(Fragment kódu – *modely a přístup k datům – index úložiště EX2*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="f9c06-326">Aktualizujte metodu akce **indexu** pro načtení všech žánrů a transformaci kolekce na seznam.</span><span class="sxs-lookup"><span data-stu-id="f9c06-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="f9c06-327">(Fragment kódu – *modely a přístup k datům – EX2 Store GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="f9c06-328">Úloha 5 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="f9c06-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="f9c06-329">V této úloze zkontrolujete, že se na stránce index úložiště nyní zobrazí žánry uložené v databázi místo pevně zakódované.</span><span class="sxs-lookup"><span data-stu-id="f9c06-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="f9c06-330">Nemusíte měnit šablonu zobrazení, protože **StoreController** vrací stejný **StoreIndexViewModel** jako předtím, ale tentokrát se data podávají z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="f9c06-331">Znovu sestavte řešení a stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f9c06-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f9c06-332">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="f9c06-332">The project starts in the Home page.</span></span> <span data-ttu-id="f9c06-333">Ověřte, že nabídka **žánrů** již není seznam pevně zakódované a data jsou přímo načtena z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="f9c06-335">*Procházení žánrů z databáze*</span><span class="sxs-lookup"><span data-stu-id="f9c06-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="f9c06-336">Teď přejděte na libovolný Žánr a ověřte, jestli jsou alba naplněná z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="f9c06-337">![Procházení alb z databáze](aspnet-mvc-4-models-and-data-access/_static/image23.png "Procházení alb z databáze")</span><span class="sxs-lookup"><span data-stu-id="f9c06-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="f9c06-338">*Procházení alb z databáze*</span><span class="sxs-lookup"><span data-stu-id="f9c06-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="f9c06-339">Cvičení 3: dotazování databáze s parametry</span><span class="sxs-lookup"><span data-stu-id="f9c06-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="f9c06-340">V tomto cvičení se dozvíte, jak zadat dotaz na databázi pomocí parametrů a jak používat tvarování výsledků dotazů, což je funkce, která snižuje počet přístupů k databázi tím, že efektivněji získává data.</span><span class="sxs-lookup"><span data-stu-id="f9c06-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c06-341">Další informace o tvarování výsledků dotazů najdete v následujícím [článku na webu MSDN](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9c06-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="f9c06-342">Úloha 1 – Změna StoreController, aby se načetly alba z databáze</span><span class="sxs-lookup"><span data-stu-id="f9c06-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="f9c06-343">V této úloze změníte třídu **StoreController** pro přístup k databázi, aby se načetla alba z konkrétního žánru.</span><span class="sxs-lookup"><span data-stu-id="f9c06-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="f9c06-344">Otevřete řešení **, které se nachází** ve složce **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** , pokud chcete použít přístup k prvnímu kódu nebo složku **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** , pokud chcete použít přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="f9c06-345">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="f9c06-346">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9c06-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f9c06-347">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f9c06-348">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f9c06-349">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f9c06-350">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f9c06-351">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="f9c06-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f9c06-352">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f9c06-353">Otevřete třídu **StoreController** a změňte metodu akce **procházení** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="f9c06-354">Provedete to tak, že v **Průzkumník řešení**rozbalíte složku **Controllers (řadiče** ) a dvakrát kliknete na **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="f9c06-355">Chcete-li načíst alba pro určitý Žánr, změňte metodu akce **procházení** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="f9c06-356">Chcete-li to provést, nahraďte následující kód:</span><span class="sxs-lookup"><span data-stu-id="f9c06-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="f9c06-357">(Fragment kódu – *modely a přístup k datům – EX3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="f9c06-358">Chcete-li naplnit kolekci entity, je nutné použít metodu **include** k určení, že chcete načíst alba.</span><span class="sxs-lookup"><span data-stu-id="f9c06-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="f9c06-359">Můžete použít. Rozšíření **Single ()** v jazyce LINQ, protože v tomto případě je pro album očekáván pouze jeden Žánr.</span><span class="sxs-lookup"><span data-stu-id="f9c06-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="f9c06-360">Metoda **Single ()** bere výraz lambda jako parametr, což v tomto případě Určuje jeden objekt žánru, který má název shodný s definovanou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="f9c06-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="f9c06-361">Budete využívat funkci, která vám umožní označit další související entity, které chcete načíst, i když je objekt žánru načten.</span><span class="sxs-lookup"><span data-stu-id="f9c06-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="f9c06-362">Tato funkce se nazývá **tvarování výsledků dotazů**a umožňuje snížit počet potřebných přístupů k databázi a získat informace.</span><span class="sxs-lookup"><span data-stu-id="f9c06-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="f9c06-363">V tomto scénáři budete chtít předem načíst alba pro žánr, který načtete.</span><span class="sxs-lookup"><span data-stu-id="f9c06-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="f9c06-364">Dotaz obsahuje **žánry. zahrnout (&quot;alba&quot;)** k indikaci, že chcete také související alba.</span><span class="sxs-lookup"><span data-stu-id="f9c06-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="f9c06-365">Výsledkem bude efektivnější aplikace, protože data o žánrech a albech budou načtena v jedné databázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="f9c06-366">Úloha 2 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="f9c06-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="f9c06-367">V této úloze spustíte aplikaci a načtete alba konkrétního žánru z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="f9c06-368">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f9c06-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f9c06-369">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="f9c06-369">The project starts in the Home page.</span></span> <span data-ttu-id="f9c06-370">Chcete-li ověřit, zda jsou výsledky z databáze načítány, změňte adresu URL na **/Store/Browse? Žánr = pop** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="f9c06-371">![Procházení podle žánru](aspnet-mvc-4-models-and-data-access/_static/image24.png "Procházení podle žánru")</span><span class="sxs-lookup"><span data-stu-id="f9c06-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="f9c06-372">*Prochází se/Store/Browse? Žánr = pop*</span><span class="sxs-lookup"><span data-stu-id="f9c06-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="f9c06-373">Úloha 3 – přístup k albu podle ID</span><span class="sxs-lookup"><span data-stu-id="f9c06-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="f9c06-374">V této úloze zopakujete předchozí postup, abyste získali alba podle jejich ID.</span><span class="sxs-lookup"><span data-stu-id="f9c06-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="f9c06-375">V případě potřeby zavřete prohlížeč a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9c06-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="f9c06-376">Otevřete třídu **StoreController** a změňte metodu akce **Details** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="f9c06-377">Provedete to tak, že v **Průzkumník řešení**rozbalíte složku **Controllers (řadiče** ) a dvakrát kliknete na **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="f9c06-378">Změňte metodu akce **Details** , aby se načetly informace o albu na základě jejich **ID**. Chcete-li to provést, nahraďte následující kód:</span><span class="sxs-lookup"><span data-stu-id="f9c06-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="f9c06-379">(Fragment kódu – *modely a přístup k datům – EX3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="f9c06-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="f9c06-380">Úloha 4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="f9c06-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="f9c06-381">V této úloze spustíte aplikaci ve webovém prohlížeči a získáte podrobnosti o albu podle jejich ID.</span><span class="sxs-lookup"><span data-stu-id="f9c06-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="f9c06-382">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f9c06-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f9c06-383">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="f9c06-383">The project starts in the Home page.</span></span> <span data-ttu-id="f9c06-384">Změňte adresu URL tak, aby **/Store/Details/51** nebo procházela žánry, a vyberte album, abyste ověřili, že se výsledky načítají z databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="f9c06-385">![Podrobnosti o procházení](aspnet-mvc-4-models-and-data-access/_static/image25.png "Podrobnosti o procházení")</span><span class="sxs-lookup"><span data-stu-id="f9c06-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="f9c06-386">*Procházení/Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="f9c06-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="f9c06-387">Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="f9c06-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f9c06-388">Souhrn</span><span class="sxs-lookup"><span data-stu-id="f9c06-388">Summary</span></span>

<span data-ttu-id="f9c06-389">Po absolvování tohoto praktického cvičení se naučíte základy modelů ASP.NET MVC a přístup k datům, a to pomocí **Database First** přístupu a **Code First** přístupu:</span><span class="sxs-lookup"><span data-stu-id="f9c06-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="f9c06-390">Postup přidání databáze do řešení za účelem využití svých dat</span><span class="sxs-lookup"><span data-stu-id="f9c06-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="f9c06-391">Postup aktualizace řadičů k poskytnutí šablon zobrazení s daty z databáze místo pevně zakódovaného kódu</span><span class="sxs-lookup"><span data-stu-id="f9c06-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="f9c06-392">Postup dotazování databáze pomocí parametrů</span><span class="sxs-lookup"><span data-stu-id="f9c06-392">How to query the database using parameters</span></span>
- <span data-ttu-id="f9c06-393">Jak používat tvarování výsledků dotazu, funkci, která snižuje počet přístupů k databázím a efektivnější načítání dat</span><span class="sxs-lookup"><span data-stu-id="f9c06-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="f9c06-394">Jak použít Database First a Code First přístupy v Microsoft Entity Framework k propojení databáze s modelem</span><span class="sxs-lookup"><span data-stu-id="f9c06-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f9c06-395">Příloha A: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="f9c06-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f9c06-396">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f9c06-397">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="f9c06-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f9c06-398">Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="f9c06-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f9c06-399">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="f9c06-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f9c06-400">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-400">Click on **Install Now**.</span></span> <span data-ttu-id="f9c06-401">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="f9c06-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f9c06-402">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="f9c06-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f9c06-403">![Nainstalovat Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="f9c06-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f9c06-404">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="f9c06-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f9c06-405">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="f9c06-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="f9c06-407">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="f9c06-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f9c06-408">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="f9c06-408">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="f9c06-410">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="f9c06-410">*Installation progress*</span></span>
6. <span data-ttu-id="f9c06-411">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-411">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="f9c06-413">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="f9c06-413">*Installation completed*</span></span>
7. <span data-ttu-id="f9c06-414">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="f9c06-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f9c06-415">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="f9c06-417">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="f9c06-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f9c06-418">Příloha B: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="f9c06-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="f9c06-419">V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c06-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="f9c06-420">Úloha 1 – Vytvoření nového webu z portálu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="f9c06-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="f9c06-421">Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="f9c06-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9c06-422">S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="f9c06-423">[Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="f9c06-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="f9c06-424">![Přihlaste se k Windows Azure Portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Přihlaste se k Windows Azure Portal")</span><span class="sxs-lookup"><span data-stu-id="f9c06-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="f9c06-425">*Přihlášení k Windows Azure Portál pro správu*</span><span class="sxs-lookup"><span data-stu-id="f9c06-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="f9c06-426">Na panelu příkazů klikněte na **Nový** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="f9c06-427">![Vytvoření nového webu](aspnet-mvc-4-models-and-data-access/_static/image32.png "Vytvoření nového webu")</span><span class="sxs-lookup"><span data-stu-id="f9c06-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="f9c06-428">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="f9c06-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="f9c06-429">Klikněte na **compute** | **Web**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="f9c06-430">Pak vyberte možnost **rychlé vytvoření** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="f9c06-431">Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9c06-432">Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat.</span><span class="sxs-lookup"><span data-stu-id="f9c06-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="f9c06-433">Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál.</span><span class="sxs-lookup"><span data-stu-id="f9c06-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="f9c06-434">Nezahrnuje kroky pro nastavení databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="f9c06-435">![Vytvoření nového webu pomocí rychlého vytvoření](aspnet-mvc-4-models-and-data-access/_static/image33.png "Vytvoření nového webu pomocí rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="f9c06-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="f9c06-436">*Vytvoření nového webu pomocí rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="f9c06-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="f9c06-437">Počkejte, než se nový **Web** vytvoří.</span><span class="sxs-lookup"><span data-stu-id="f9c06-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="f9c06-438">Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="f9c06-439">Ověřte, zda nový web funguje.</span><span class="sxs-lookup"><span data-stu-id="f9c06-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="f9c06-440">![Procházení na nový web](aspnet-mvc-4-models-and-data-access/_static/image34.png "Procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="f9c06-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="f9c06-441">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="f9c06-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="f9c06-442">![Běžící Web](aspnet-mvc-4-models-and-data-access/_static/image35.png "Běžící Web")</span><span class="sxs-lookup"><span data-stu-id="f9c06-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="f9c06-443">*Běžící Web*</span><span class="sxs-lookup"><span data-stu-id="f9c06-443">*Web site running*</span></span>
6. <span data-ttu-id="f9c06-444">Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="f9c06-445">![Otevření stránek správy webu](aspnet-mvc-4-models-and-data-access/_static/image36.png "Otevření stránek správy webu")</span><span class="sxs-lookup"><span data-stu-id="f9c06-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="f9c06-446">*Otevření stránek správy webu*</span><span class="sxs-lookup"><span data-stu-id="f9c06-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="f9c06-447">Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9c06-448">*Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace.</span><span class="sxs-lookup"><span data-stu-id="f9c06-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="f9c06-449">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace.</span><span class="sxs-lookup"><span data-stu-id="f9c06-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="f9c06-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c06-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="f9c06-451">![Stahuje se publikační profil webu.](aspnet-mvc-4-models-and-data-access/_static/image37.png "Stahuje se publikační profil webu.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="f9c06-452">*Stahuje se publikační profil webu.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="f9c06-453">Stáhněte si soubor profilu publikování do známého umístění.</span><span class="sxs-lookup"><span data-stu-id="f9c06-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="f9c06-454">V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9c06-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="f9c06-455">![Ukládání souboru profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image38.png "Ukládá se publikační profil.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="f9c06-456">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="f9c06-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="f9c06-457">Úloha 2 – Konfigurace databázového serveru</span><span class="sxs-lookup"><span data-stu-id="f9c06-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="f9c06-458">Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="f9c06-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="f9c06-459">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="f9c06-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="f9c06-460">Pro uložení aplikační databáze budete potřebovat server SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f9c06-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="f9c06-461">SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="f9c06-462">Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="f9c06-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="f9c06-463">Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách.</span><span class="sxs-lookup"><span data-stu-id="f9c06-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="f9c06-464">Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="f9c06-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="f9c06-465">![Řídicí panel serveru SQL Database](aspnet-mvc-4-models-and-data-access/_static/image39.png "Řídicí panel serveru SQL Database")</span><span class="sxs-lookup"><span data-stu-id="f9c06-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="f9c06-466">*Řídicí panel serveru SQL Database*</span><span class="sxs-lookup"><span data-stu-id="f9c06-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="f9c06-467">V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru.</span><span class="sxs-lookup"><span data-stu-id="f9c06-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="f9c06-468">Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](aspnet-mvc-4-models-and-data-access/_static/image40.png).</span><span class="sxs-lookup"><span data-stu-id="f9c06-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![Přidává se IP adresa klienta.](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="f9c06-470">*Přidává se IP adresa klienta.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="f9c06-471">Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="f9c06-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrdit změny](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="f9c06-473">*Potvrdit změny*</span><span class="sxs-lookup"><span data-stu-id="f9c06-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f9c06-474">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="f9c06-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="f9c06-475">Vraťte se do řešení ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f9c06-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="f9c06-476">V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="f9c06-477">![Publikování aplikace](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="f9c06-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="f9c06-478">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="f9c06-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="f9c06-479">Importujte profil publikování, který jste uložili v prvním úkolu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="f9c06-480">![Import profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image44.png "Import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="f9c06-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="f9c06-481">*Importuje se publikační profil.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="f9c06-482">Klikněte na **ověřit připojení**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-482">Click **Validate Connection**.</span></span> <span data-ttu-id="f9c06-483">Po dokončení ověřování klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9c06-484">Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="f9c06-485">![Ověřování připojení](aspnet-mvc-4-models-and-data-access/_static/image45.png "Ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="f9c06-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="f9c06-486">*Ověřování připojení*</span><span class="sxs-lookup"><span data-stu-id="f9c06-486">*Validating connection*</span></span>
4. <span data-ttu-id="f9c06-487">Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="f9c06-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="f9c06-488">![Konfigurace nasazení webu](aspnet-mvc-4-models-and-data-access/_static/image46.png "Konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="f9c06-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="f9c06-489">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="f9c06-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="f9c06-490">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="f9c06-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="f9c06-491">Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="f9c06-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="f9c06-492">V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="f9c06-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="f9c06-493">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="f9c06-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="f9c06-494">Zadejte nový název databáze.</span><span class="sxs-lookup"><span data-stu-id="f9c06-494">Type a new database name.</span></span>

     <span data-ttu-id="f9c06-495">![Konfigurace cílového připojovacího řetězce](aspnet-mvc-4-models-and-data-access/_static/image47.png "Konfigurace cílového připojovacího řetězce")</span><span class="sxs-lookup"><span data-stu-id="f9c06-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="f9c06-496">*Konfigurace cílového připojovacího řetězce*</span><span class="sxs-lookup"><span data-stu-id="f9c06-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="f9c06-497">Pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-497">Then click **OK**.</span></span> <span data-ttu-id="f9c06-498">Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="f9c06-499">![Vytvoření databáze](aspnet-mvc-4-models-and-data-access/_static/image48.png "Vytváří se řetězec databáze.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="f9c06-500">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="f9c06-500">*Creating the database*</span></span>
7. <span data-ttu-id="f9c06-501">Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení.</span><span class="sxs-lookup"><span data-stu-id="f9c06-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="f9c06-502">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-502">Then click **Next**.</span></span>

    <span data-ttu-id="f9c06-503">![Připojovací řetězec ukazující na SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Připojovací řetězec ukazující na SQL Database")</span><span class="sxs-lookup"><span data-stu-id="f9c06-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="f9c06-504">*Připojovací řetězec ukazující na SQL Database*</span><span class="sxs-lookup"><span data-stu-id="f9c06-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="f9c06-505">Na stránce **Náhled** klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="f9c06-506">![Publikování webové aplikace](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="f9c06-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="f9c06-507">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="f9c06-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="f9c06-508">Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.</span><span class="sxs-lookup"><span data-stu-id="f9c06-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="f9c06-509">Příloha C: používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="f9c06-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="f9c06-510">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="f9c06-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f9c06-511">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="f9c06-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f9c06-512">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-models-and-data-access/_static/image51.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="f9c06-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="f9c06-513">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="f9c06-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="f9c06-514">***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="f9c06-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="f9c06-515">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="f9c06-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f9c06-516">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="f9c06-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f9c06-517">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f9c06-518">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="f9c06-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f9c06-519">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="f9c06-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f9c06-520">![Začněte psát název fragmentu.](aspnet-mvc-4-models-and-data-access/_static/image52.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="f9c06-521">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="f9c06-522">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-models-and-data-access/_static/image53.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="f9c06-523">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="f9c06-524">![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-models-and-data-access/_static/image54.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="f9c06-525">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="f9c06-526">***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první.</span><span class="sxs-lookup"><span data-stu-id="f9c06-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f9c06-527">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f9c06-528">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="f9c06-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f9c06-529">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="f9c06-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f9c06-530">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-models-and-data-access/_static/image55.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="f9c06-531">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="f9c06-532">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-models-and-data-access/_static/image56.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="f9c06-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="f9c06-533">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="f9c06-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
