---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 'Praktická cvičení: Údržba Azure websites: Správa změn a škálování | Microsoft Docs'
author: rick-anderson
description: V tomto testovacím prostředí se dozvíte, jak Microsoft Azure usnadňuje sestavování a nasazování webů do produkčního prostředí.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624269"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="1ba1c-103">Praktické cvičení: Udržitelné weby Azure – správa změn a škálování</span><span class="sxs-lookup"><span data-stu-id="1ba1c-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>

<span data-ttu-id="1ba1c-104">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="1ba1c-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="1ba1c-105">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="1ba1c-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="1ba1c-106">Microsoft Azure usnadňuje sestavování a nasazování webů do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="1ba1c-107">Ale nejste hotovi, když je vaše aplikace živá, teprve začínáte!</span><span class="sxs-lookup"><span data-stu-id="1ba1c-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="1ba1c-108">Budete muset zpracovat měnící se požadavky, aktualizace databáze, škálování a další.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="1ba1c-109">Naštěstí Azure App Service máte na problém s mnoha funkcemi, které vám pomůžou zajistit bezproblémové fungování vašich webů.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="1ba1c-110">Azure nabízí možnosti bezpečného a flexibilního vývoje, nasazení a škálování libovolné webové aplikace velikosti.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="1ba1c-111">Využijte své stávající nástroje k vytváření a nasazování aplikací bez starostí se správou infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="1ba1c-112">Pomocí snadného nasazení obsahu vytvořeného pomocí oblíbeného vývojového nástroje můžete zřídit produkční webovou aplikaci sami v řádu minut.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="1ba1c-113">Existující web můžete nasadit přímo ze správy zdrojového kódu s podporou pro **Git**, **GitHub**, **Bitbucket**, **TFS**a dokonce i **Dropbox**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="1ba1c-114">Nasaďte přímo z oblíbeného integrovaného vývojového prostředí (IDE) nebo ze skriptů pomocí **prostředí PowerShell** v nástrojích pro Windows nebo rozhraní příkazového **řádku**</span><span class="sxs-lookup"><span data-stu-id="1ba1c-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="1ba1c-115">Po nasazení Udržujte Vaše weby stále aktuální díky podpoře průběžného nasazování.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="1ba1c-116">Azure poskytuje škálovatelné, odolné cloudové úložiště, zálohování a řešení obnovení pro libovolná data, Velká i malá.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="1ba1c-117">Když nasazujete aplikace do provozního prostředí, služby úložiště, jako jsou tabulky, objekty BLOB a databáze SQL, vám pomůžou škálovat aplikace v cloudu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="1ba1c-118">Databáze SQL jsou důležité při nasazování nových verzí aplikace udržovat produktivní databázi v aktuálním stavu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="1ba1c-119">Díky **migrace Entity Framework Code First**je vývoj a nasazení datového modelu zjednodušené, aby se vaše prostředí aktualizovala během několika minut.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="1ba1c-120">Tato praktická cvičení vám ukáže různá témata, se kterými se můžete setkat při nasazení webové aplikace do produkčních prostředí v Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="1ba1c-121">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="1ba1c-122">Podrobnější pokrytí tohoto tématu najdete v tématu [sestavování reálných cloudových aplikací pomocí elektronické knihy Azure](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="1ba1c-123">Přehled</span><span class="sxs-lookup"><span data-stu-id="1ba1c-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="1ba1c-124">Cíle</span><span class="sxs-lookup"><span data-stu-id="1ba1c-124">Objectives</span></span>

<span data-ttu-id="1ba1c-125">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="1ba1c-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="1ba1c-126">Povolit Entity Framework migrace s existujícím modelem</span><span class="sxs-lookup"><span data-stu-id="1ba1c-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="1ba1c-127">Aktualizujte objektový model a databázi odpovídajícím způsobem pomocí Entity Framework migrace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="1ba1c-128">Nasazení do Azure App Service pomocí Gitu</span><span class="sxs-lookup"><span data-stu-id="1ba1c-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="1ba1c-129">Vrácení zpět k předchozímu nasazení pomocí portálu pro správu Azure</span><span class="sxs-lookup"><span data-stu-id="1ba1c-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="1ba1c-130">Škálování webové aplikace pomocí Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1ba1c-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="1ba1c-131">Konfigurace automatického škálování pro webovou aplikaci pomocí Portál pro správu Azure</span><span class="sxs-lookup"><span data-stu-id="1ba1c-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="1ba1c-132">Vytvoření a konfigurace projektu zátěžového testu v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ba1c-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="1ba1c-133">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="1ba1c-133">Prerequisites</span></span>

<span data-ttu-id="1ba1c-134">Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:</span><span class="sxs-lookup"><span data-stu-id="1ba1c-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="1ba1c-135">[Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/) nebo více</span><span class="sxs-lookup"><span data-stu-id="1ba1c-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="1ba1c-136">Sada Azure SDK pro .NET 2,2</span><span class="sxs-lookup"><span data-stu-id="1ba1c-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="1ba1c-137">Systém správy verzí GITU</span><span class="sxs-lookup"><span data-stu-id="1ba1c-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="1ba1c-138">Microsoft Azure předplatné</span><span class="sxs-lookup"><span data-stu-id="1ba1c-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="1ba1c-139">Zaregistrujte si [bezplatnou zkušební verzi](https://aka.ms/watk-freetrial)</span><span class="sxs-lookup"><span data-stu-id="1ba1c-139">Sign up for a [Free Trial](https://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="1ba1c-140">Pokud máte Visual Studio Professional, Test Professional, Premium nebo Ultimate s MSDN nebo MSDN Platforms předplatitelem, aktivujte si [výhodu MSDN](https://aka.ms/watk-msdn) hned teď, abyste mohli začít vyvíjet a testovat v Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](https://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="1ba1c-141">[BizSpark](https://aka.ms/watk-bizspark) členové automaticky získají výhody Azure prostřednictvím předplatného Visual Studio Ultimate with MSDN.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-141">[BizSpark](https://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="1ba1c-142">Členové programu [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials obdrží zdarma měsíční kredit Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-142">Members of the [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="1ba1c-143">Nastavení</span><span class="sxs-lookup"><span data-stu-id="1ba1c-143">Setup</span></span>

<span data-ttu-id="1ba1c-144">Aby bylo možné spustit cvičení v této praktické laboratorní laboratoři, budete muset nejprve nastavit prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="1ba1c-145">Otevřete Průzkumníka Windows a přejděte do **zdrojové** složky testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="1ba1c-146">Klikněte pravým tlačítkem na **Setup. cmd** a vyberte **Spustit jako správce** a spusťte proces instalace, který bude konfigurovat vaše prostředí a nainstaluje fragmenty kódu sady Visual Studio pro toto testovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="1ba1c-147">Pokud se zobrazí dialogové okno Řízení uživatelských účtů, potvrďte akci, abyste mohli pokračovat.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba1c-148">Před spuštěním instalačního programu se ujistěte, že jste kontrolovali všechny závislosti pro toto testovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="1ba1c-149">Používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="1ba1c-149">Using the Code Snippets</span></span>

<span data-ttu-id="1ba1c-150">V celém dokumentu testovacího prostředí budete vyzváni k vložení bloků kódu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="1ba1c-151">Pro usnadnění práce je většina tohoto kódu k dispozici jako fragmenty Visual Studio Code, ke kterým můžete přistupovat z Visual Studio 2013, abyste se vyhnuli nutnosti ho přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba1c-152">Každé cvičení se doprovází od počátečního řešení ve složce **Begin** cvičení, které vám umožní sledovat jednotlivá cvičení nezávisle na ostatních.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="1ba1c-153">Všimněte si, že fragmenty kódu, které jsou přidány během cvičení, v těchto počátečních řešeních chybí a nemusí fungovat, dokud nedokončíte cvičení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="1ba1c-154">Ve zdrojovém kódu cvičení také najdete **koncovou** složku obsahující řešení sady Visual Studio s kódem, který je výsledkem dokončení kroků v příslušném cvičení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="1ba1c-155">Tato řešení můžete použít jako návod, pokud potřebujete další pomoc při práci s tímto praktickým cvičením.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="1ba1c-156">Cvičení</span><span class="sxs-lookup"><span data-stu-id="1ba1c-156">Exercises</span></span>

<span data-ttu-id="1ba1c-157">Tato praktická cvičení zahrnují následující cvičení:</span><span class="sxs-lookup"><span data-stu-id="1ba1c-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="1ba1c-158">Použití migrace Entity Framework</span><span class="sxs-lookup"><span data-stu-id="1ba1c-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="1ba1c-159">Nasazení webové aplikace do přípravy</span><span class="sxs-lookup"><span data-stu-id="1ba1c-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="1ba1c-160">Provádění vrácení nasazení v produkčním prostředí</span><span class="sxs-lookup"><span data-stu-id="1ba1c-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="1ba1c-161">Škálování pomocí Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1ba1c-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="1ba1c-162">[Použití automatického škálování pro Web Apps](#Exercise5) (volitelné pro Visual Studio 2013 Ultimate Edition)</span><span class="sxs-lookup"><span data-stu-id="1ba1c-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="1ba1c-163">Odhadovaný čas dokončení tohoto testovacího prostředí: **75 minut**</span><span class="sxs-lookup"><span data-stu-id="1ba1c-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="1ba1c-164">Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="1ba1c-165">Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="1ba1c-166">Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="1ba1c-167">Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="1ba1c-168">Cvičení 1: použití migrace Entity Framework</span><span class="sxs-lookup"><span data-stu-id="1ba1c-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="1ba1c-169">Když vyvíjíte aplikaci, váš datový model se může v průběhu času měnit.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="1ba1c-170">Tyto změny mohou ovlivnit existující model v databázi (Pokud vytváříte novou verzi) a je důležité udržovat databázi v aktuálním stavu, aby nedocházelo k chybám.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="1ba1c-171">Chcete-li zjednodušit sledování těchto změn v modelu, **migrace Entity Framework Code First** automaticky zjišťovat změny, které porovnávají model s databázovým schématem, a vygeneruje konkrétní kód pro aktualizaci databáze a vytváří nové *verze* vaší databáze.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="1ba1c-172">V tomto cvičení se dozvíte, jak povolit **migrace** pro vaši aplikaci a jak snadno zjišťovat a generovat změny pro aktualizaci databází.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="1ba1c-173">Úloha 1 – povolení migrací</span><span class="sxs-lookup"><span data-stu-id="1ba1c-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="1ba1c-174">V této úloze provedete kroky povolení **migrace Entity Framework Code First** do databáze **kvízu informatik** , změnu modelu a porozumění způsobu, jakým se tyto změny projeví v databázi.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="1ba1c-175">Otevřete Visual Studio a otevřete soubor řešení **GeekQuiz. sln** z **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="1ba1c-176">Sestavte řešení, aby se daly stáhnout a nainstalovat závislosti balíčku **NuGet** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="1ba1c-177">Provedete to tak, že kliknete pravým tlačítkem na řešení a kliknete na **Sestavit řešení** nebo stisknete **CTRL + SHIFT + B**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="1ba1c-178">V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-178">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="1ba1c-179">V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="1ba1c-180">Vytvoří se počáteční migrace založená na stávajícím modelu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="1ba1c-181">![Povolování migrací](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Povolování migrací")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="1ba1c-182">*Povolování migrací*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-183">Tento příkaz přidá složku **migrace** do projektu informatik kvízu, který obsahuje soubor s názvem **Configuration.cs**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="1ba1c-184">Třída **Configuration** umožňuje nakonfigurovat, jak se budou migrace chovat pro váš kontext.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="1ba1c-185">U povolených migrací je potřeba aktualizovat třídu **Configuration** , aby se databáze naplnila počátečními daty, která **informatik kvíz** vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="1ba1c-186">V části **migrace**nahraďte soubor **Configuration.cs** souborem, který se nachází ve složce **Source\Assets** v tomto testovacím prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-187">Vzhledem k tomu, že **migrace** zavolá metodu **počáteční** hodnoty s každou aktualizací databáze, je nutné zajistit, aby záznamy nebyly v databázi duplikovány.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="1ba1c-188">Metoda **AddOrUpdate** vám pomůže zabránit duplicitním datům.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="1ba1c-189">Chcete-li přidat počáteční migraci, zadejte následující příkaz a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-190">Ujistěte se, že v instanci LocalDB není žádná databáze s názvem &quot;GeekQuizProd&quot;.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="1ba1c-191">![Přidává se migrace základního schématu.](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Přidává se migrace základního schématu.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="1ba1c-192">*Přidává se migrace základního schématu.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-193">**Příkaz Add-Migration** vygeneruje další migraci na základě změn, které jste provedli v modelu od vytvoření poslední migrace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="1ba1c-194">V takovém případě se jako první migrace projektu přidá skripty pro vytvoření všech tabulek definovaných ve třídě **TriviaContext** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="1ba1c-195">Spuštěním následujícího příkazu proveďte migraci k aktualizaci databáze.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="1ba1c-196">Pro tento příkaz určíte příznak **verbose** , který zobrazí příkazy SQL, které se aplikují na cílovou databázi.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="1ba1c-197">![Vytváření počáteční databáze](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Vytváření počáteční databáze")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="1ba1c-198">*Vytváření počáteční databáze*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-199">**Aktualizace – databáze** bude platit pro všechny probíhající migrace do databáze.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="1ba1c-200">V tomto případě vytvoří databázi pomocí připojovacího řetězce definovaného v souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="1ba1c-201">Přejděte do nabídky **Zobrazit** a otevřete **Průzkumník objektů systému SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="1ba1c-202">![Otevřít v Průzkumník objektů systému SQL Server](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Otevřít v Průzkumník objektů systému SQL Server")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="1ba1c-203">*Otevřít v Průzkumník objektů systému SQL Server*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="1ba1c-204">V okně **Průzkumník objektů systému SQL Server** se připojte k instanci LocalDB kliknutím pravým tlačítkem myši na uzel **SQL Server** a vybráním možnosti **Přidat SQL Server...** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="1ba1c-205">![Přidání instance SQL Server](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Přidání instance SQL Server")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="1ba1c-206">*Přidání instance SQL Server do Průzkumník objektů systému SQL Server*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="1ba1c-207">Nastavte **název serveru** na *(LocalDB) \v11.0* a v režimu ověřování nechte **ověřování systému Windows** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="1ba1c-208">Pokračujte kliknutím na **Připojit**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="1ba1c-209">![Připojování k LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Připojování k LocalDB")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="1ba1c-210">*Připojování k LocalDB*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="1ba1c-211">Otevřete databázi **GeekQuizProd** a rozbalte uzel **tabulky** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="1ba1c-212">Jak vidíte, příkaz **Update-Database** vygeneroval všechny tabulky definované ve třídě **TriviaContext** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="1ba1c-213">Vyhledejte **dbo. TriviaQuestions** tabulku a otevřete uzel sloupce.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="1ba1c-214">V další úloze přidáte do této tabulky nový sloupec a aktualizujete databázi pomocí **migrací**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="1ba1c-215">![Sloupce otázek minihry](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Sloupce otázek minihry")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="1ba1c-216">*Sloupce otázek minihry*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="1ba1c-217">Úloha 2 – aktualizace schématu databáze pomocí migrací</span><span class="sxs-lookup"><span data-stu-id="1ba1c-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="1ba1c-218">V této úloze použijete **migrace Entity Framework Code First** k detekci změny v modelu a vygenerujete potřebný kód pro aktualizaci databáze.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="1ba1c-219">Entitu **TriviaQuestions** aktualizujete tak, že do ní přidáte novou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="1ba1c-220">Potom spustíte příkazy pro vytvoření nové migrace, které budou zahrnovat nový sloupec v tabulce.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="1ba1c-221">V **Průzkumník řešení**dvakrát klikněte na soubor **TriviaQuestion.cs** , který se nachází uvnitř složky **modely** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="1ba1c-222">Přidejte novou vlastnost s názvem **Hint**, jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="1ba1c-223">V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="1ba1c-224">Vytvoří se nová migrace odrážející změnu v našem modelu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="1ba1c-225">![Přidání – migrace](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Přidání – migrace")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="1ba1c-226">*Přidání – migrace*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-227">Soubor migrace se skládá ze dvou metod, **nahoru** a **dolů**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="1ba1c-228">Metoda **up** se použije k určení, které změny aktuální verze naší aplikace musí platit pro databázi.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="1ba1c-229">**Dolů** se používá k vrácení změn, které jsme přidali do metody **up** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="1ba1c-230">Když migrace databáze aktualizuje databázi, spustí všechny migrace v pořadí časových razítek a jenom ty, které se od poslední aktualizace nepoužily (tabulka \_MigrationHistory udržuje přehled o tom, které migrace se použily).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="1ba1c-231">Metoda **up** pro všechny migrace bude volána a provede změny, které jsme určili v databázi.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="1ba1c-232">Pokud se rozhodnete vrátit k předchozí migraci, bude volána metoda **dolů** , která provede změny v obráceném pořadí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="1ba1c-233">V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="1ba1c-234">Výstup příkazu **Update-Database** vygeneroval příkaz **ALTER TABLE** jazyka SQL pro přidání nového sloupce do tabulky **TriviaQuestions** , jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="1ba1c-235">![Přidat vygenerovaný příkaz SQL sloupce](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Přidat vygenerovaný příkaz SQL sloupce")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="1ba1c-236">*Přidat vygenerovaný příkaz SQL sloupce*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="1ba1c-237">V **Průzkumník objektů systému SQL Server**aktualizujte **dbo. TriviaQuestions** tabulku a ověřte, že se zobrazuje nový sloupec s **nápovědou** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="1ba1c-238">![Zobrazení nového sloupce s nápovědou](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Zobrazení nového sloupce s nápovědou")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="1ba1c-239">*Zobrazení nového sloupce s nápovědou*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="1ba1c-240">Zpět v editoru **TriviaQuestion.cs** přidejte do vlastnosti *Hint* omezení **StringLength** , jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="1ba1c-241">V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="1ba1c-242">V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="1ba1c-243">Výstup příkazu **Update-Database** vygeneroval příkaz **ALTER TABLE** jazyka SQL, který aktualizuje typ sloupce *pomocného parametru* tabulky **TriviaQuestions** , jak je znázorněno na obrázku níže.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="1ba1c-244">![Vygenerované příkazy ALTER COLUMN SQL](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Vygenerované příkazy ALTER COLUMN SQL")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="1ba1c-245">*Vygenerované příkazy ALTER COLUMN SQL*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="1ba1c-246">V **Průzkumník objektů systému SQL Server**aktualizujte **dbo. TriviaQuestions** tabulku a ověřte, zda je typ sloupce **pomocným parametrem** **nvarchar (150)** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="1ba1c-247">![Zobrazuje se nové omezení.](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Zobrazuje se nové omezení.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="1ba1c-248">*Zobrazuje se nové omezení.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="1ba1c-249">Cvičení 2: nasazení webové aplikace do přípravy</span><span class="sxs-lookup"><span data-stu-id="1ba1c-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="1ba1c-250">**Web Apps v Azure App Service** vám umožní provést dvoufázové publikování.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="1ba1c-251">Při dvoufázovém publikování se vytvoří pozice pro pracovní místo pro každý výchozí produkční web a umožní vám tyto sloty prohodit bez času.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="1ba1c-252">To je opravdu užitečné k ověření změn před vydáním veřejné, přírůstkově integrování obsahu webu a vrácení zpět, pokud změny nefungují podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="1ba1c-253">V tomto cvičení nasadíte aplikaci **informatik kvíz** do přípravného prostředí vaší webové aplikace pomocí správy zdrojového kódu Git.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="1ba1c-254">K tomu vytvoříte webovou aplikaci a zřídíte požadované komponenty na portálu pro správu, nakonfigurujete úložiště **Git** a nahrajete zdrojový kód aplikace z místního počítače do přípravného slotu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="1ba1c-255">Provozní databázi budete aktualizovat také pomocí **migrace Code First** , kterou jste vytvořili v předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="1ba1c-256">Pak spustíte aplikaci v tomto testovacím prostředí, abyste ověřili její činnost.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="1ba1c-257">Jakmile budete přesvědčeni, že funguje podle vašich očekávání, budete aplikaci propagovat na produkční.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba1c-258">Aby bylo možné povolit dvoufázové publikování, musí být webová aplikace ve **standardním režimu**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="1ba1c-259">Všimněte si, že při změně webové aplikace na standardní režim budou účtovány další poplatky.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="1ba1c-260">Další informace o cenách najdete v tématu [App Service ceny](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="1ba1c-261">Úloha 1 – Vytvoření webové aplikace v Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1ba1c-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="1ba1c-262">V této úloze vytvoříte webovou aplikaci v **Azure App Service** na portálu pro správu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="1ba1c-263">Také nakonfigurujete **SQL Database** pro zachování dat aplikace a nakonfigurujete místní úložiště Git pro správu zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="1ba1c-264">Přejít na [portál pro správu Azure](https://manage.windowsazure.com) a přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![Přihlaste se k portálu pro správu Azure.](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="1ba1c-266">*Přihlaste se k portálu pro správu Azure.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="1ba1c-267">Na panelu příkazů v dolní části stránky klikněte na **Nový** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="1ba1c-268">![Vytváří se nová webová aplikace.](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Vytváří se nová webová aplikace.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="1ba1c-269">*Vytváří se nová webová aplikace.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="1ba1c-270">Klikněte na **COMPUTE**, **Web** a pak na **vlastní vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="1ba1c-271">![Vytvoření nové webové aplikace pomocí vlastního vytvoření](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Vytvoření nové webové aplikace pomocí vlastního vytvoření")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="1ba1c-272">*Vytvoření nové webové aplikace pomocí vlastního vytvoření*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="1ba1c-273">V dialogovém okně **Nový web – vlastní vytvoření** zadejte dostupnou **adresu URL** (např. *informatik-kvíz*), vyberte umístění v rozevíracím seznamu **oblast** a v rozevíracím seznamu **databáze** vyberte **vytvořit novou databázi SQL** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="1ba1c-274">Nakonec zaškrtněte políčko **publikovat ze správy zdrojového kódu** a klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![Přizpůsobení nové webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="1ba1c-276">*Přizpůsobení nové webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="1ba1c-277">Pro nastavení databáze zadejte následující informace:</span><span class="sxs-lookup"><span data-stu-id="1ba1c-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="1ba1c-278">Do textového pole **název** zadejte název databáze (např. *geekquiz\_DB*).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="1ba1c-279">V **rozevíracím** seznamu Server vyberte **Nový server databáze SQL**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="1ba1c-280">Případně můžete vybrat existující server.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="1ba1c-281">Do polí **uživatelské jméno databáze** a **heslo databáze** zadejte uživatelské jméno a heslo správce pro server služby SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="1ba1c-282">Pokud vyberete server, který jste už vytvořili, zobrazí se výzva k zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![Určení nastavení databáze](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="1ba1c-284">*Určení nastavení databáze*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="1ba1c-285">Pokračujte kliknutím na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="1ba1c-286">Vyberte **místní úložiště Git** pro správu zdrojového kódu, která se má použít, a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-287">Může se zobrazit výzva k zadání přihlašovacích údajů pro nasazení (uživatelské jméno a heslo).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![Vytváření úložiště Git](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="1ba1c-289">*Vytváření úložiště Git*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="1ba1c-290">Počkejte, než se vytvoří nová webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-291">Ve výchozím nastavení poskytuje Azure domény na *azurewebsites.NET* , ale také umožňuje nastavit vlastní domény pomocí portálu pro správu Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="1ba1c-292">Vlastní domény ale můžete spravovat jenom v případě, že používáte určité Azure App Service režimy.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="1ba1c-293">Azure App Service je k dispozici v edicích Free, Shared, Basic, Standard a Premium.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="1ba1c-294">V režimu Free a Shared běží všechny webové aplikace v prostředí s více klienty a mají kvóty pro využití procesoru, paměti a sítě.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="1ba1c-295">Maximální počet bezplatných aplikací se může u vašeho plánu lišit.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="1ba1c-296">Ve standardním režimu zvolíte, které aplikace se spouštějí na vyhrazených virtuálních počítačích, které odpovídají standardním výpočetním prostředkům Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="1ba1c-297">V nabídce **škálování** webové aplikace můžete najít konfiguraci režimu webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="1ba1c-298">![Azure App Service režimy](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service režimy")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="1ba1c-299">Pokud používáte **sdílený** nebo **standardní** režim, budete moct spravovat vlastní domény pro vaši webovou aplikaci, a to tak, že přejdete do nabídky **Konfigurace** vaší aplikace a kliknete na **Spravovat domény** v části *názvy domén*.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="1ba1c-300">![Správa domén](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Správa domén")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="1ba1c-301">![Správa vlastních domén](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Správa vlastních domén")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="1ba1c-302">Po vytvoření webové aplikace klikněte na odkaz ve sloupci **Adresa URL** a ověřte, jestli je spuštěná nová webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![Procházení nové webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="1ba1c-304">*Procházení nové webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-304">*Browsing to the new web app*</span></span>

    ![spuštěná webová aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="1ba1c-306">*spuštěná webová aplikace*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="1ba1c-307">Úloha 2 – Vytvoření produkčního SQL Database</span><span class="sxs-lookup"><span data-stu-id="1ba1c-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="1ba1c-308">V této úloze použijete **migrace Entity Framework Code First** k vytvoření databáze cílící na instanci **Azure SQL Database** , kterou jste vytvořili v předchozím úkolu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="1ba1c-309">V Portál pro správu přejděte do webové aplikace, kterou jste vytvořili v předchozím úkolu, a přejděte na **řídicí panel**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="1ba1c-310">Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Zobrazit připojovací řetězce** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="1ba1c-311">![Zobrazit připojovací řetězce](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "Zobrazit připojovací řetězce")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="1ba1c-312">*Zobrazit připojovací řetězce*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-312">*View connection strings*</span></span>
3. <span data-ttu-id="1ba1c-313">Zkopírujte hodnotu **připojovacího řetězce** a zavřete dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="1ba1c-314">![Připojovací řetězec v Azure Portál pro správu](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Připojovací řetězec v Azure Portál pro správu")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="1ba1c-315">*Připojovací řetězec v Azure Portál pro správu*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="1ba1c-316">Kliknutím na **databáze SQL** zobrazíte seznam databází SQL v Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="1ba1c-317">![Nabídka SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "Nabídka SQL Database")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="1ba1c-318">*Nabídka SQL Database*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="1ba1c-319">Vyhledejte databázi, kterou jste vytvořili v předchozí úloze, a klikněte na server.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="1ba1c-320">![Server SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "Server služby SQL Database")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="1ba1c-321">*Server SQL Database*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-321">*SQL Database server*</span></span>
6. <span data-ttu-id="1ba1c-322">Na stránce **rychlé zprovoznění** serveru klikněte na možnost **Konfigurovat**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="1ba1c-323">![Konfigurace nabídky](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Konfigurace nabídky")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="1ba1c-324">*Konfigurace nabídky*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-324">*Configure menu*</span></span>
7. <span data-ttu-id="1ba1c-325">V části **povolené IP adresy** klikněte na odkaz **Přidat na adresu povolených IP adres** , aby se vaše IP adresa mohla připojit k serveru SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="1ba1c-326">![Povolené IP adresy](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Povolené IP adresy")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="1ba1c-327">*Povolené IP adresy*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="1ba1c-328">Kliknutím na **Save (Uložit** ) v dolní části stránky dokončete krok.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="1ba1c-329">Přepněte zpět do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="1ba1c-330">V **konzole správce balíčků**spusťte následující příkaz, kterým nahradíte zástupný symbol *[text-Connection-String]* připojovacím řetězcem, který jste zkopírovali z Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="1ba1c-331">![Aktualizace databáze cílící na Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Aktualizace databáze cílící na Windows Azure SQL Database")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="1ba1c-332">*Aktualizace cílení databáze Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="1ba1c-333">Úloha 3 – nasazení informatik kvízu do přípravy pomocí Gitu</span><span class="sxs-lookup"><span data-stu-id="1ba1c-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="1ba1c-334">V této úloze povolíte připravené publikování ve vaší webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="1ba1c-335">Pak použijete Git k publikování aplikace informatik kvízu přímo z místního počítače do přípravného prostředí vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="1ba1c-336">Vraťte se na portál a kliknutím na název webové aplikace pod sloupcem **název** zobrazíte stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![Otevření stránek správy webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="1ba1c-338">*Otevření stránek správy webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="1ba1c-339">Přejděte na stránku **škálování** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="1ba1c-340">V části **Obecné** vyberte pro konfiguraci možnost **Standard** a na panelu příkazů klikněte na **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-341">Chcete-li spustit všechny webové aplikace v aktuální oblasti a předplatném ve **standardním** režimu, ponechte zaškrtnuté políčko **zaškrtnout vše** v části **zvolit konfiguraci webů** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="1ba1c-342">V opačném případě zrušte zaškrtnutí políčka **Vybrat vše** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="1ba1c-343">![Upgrade webové aplikace na standardní režim](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrade webové aplikace na standardní režim")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="1ba1c-344">*Upgrade webové aplikace na standardní režim*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="1ba1c-345">Kliknutím na tlačítko **Ano** potvrďte změny.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="1ba1c-346">![Potvrzení změny do standardního režimu](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Pokračování ve změně režimu webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="1ba1c-347">*Potvrzení změny do standardního režimu*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="1ba1c-348">Přejděte na stránku **řídicí panel** a klikněte na **povolit dvoufázové publikování** v části **rychlý přehled** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="1ba1c-349">![Povolení dvoufázové publikování](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Povolení dvoufázové publikování")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="1ba1c-350">*Povolení dvoufázové publikování*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="1ba1c-351">Kliknutím na **Ano** povolíte dvoufázové publikování.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="1ba1c-352">![Potvrzení připraveného publikování](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Kliknutím na Ano povolíte dvoufázové publikování.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="1ba1c-353">*Potvrzení připraveného publikování*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="1ba1c-354">V seznamu webových aplikací rozbalte značku vlevo od názvu vaší webové aplikace a zobrazte tak pracovní slot pro přípravu na pracovišti.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="1ba1c-355">Má název vaší webové aplikace, za nímž následuje ***(příprava)***.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="1ba1c-356">Kliknutím na pracovní web přejdete na stránku správy.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="1ba1c-357">![Navigace do pracovní webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigace do pracovní webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="1ba1c-358">*Navigace do pracovní aplikace*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="1ba1c-359">Všimněte si, že stránka správy vypadá jako jakákoli jiná stránka správy webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="1ba1c-360">Přejděte na stránku **nasazení** a zkopírujte hodnotu **adresy URL Gitu** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="1ba1c-361">Budete ho používat později v tomto cvičení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-361">You will use it later in this exercise.</span></span>

    ![Kopíruje se hodnota adresy URL Gitu.](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="1ba1c-363">*Kopíruje se hodnota adresy URL Gitu.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="1ba1c-364">Otevřete novou konzolu **Git bash** a spusťte následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="1ba1c-365">Aktualizujte zástupný text *[vaše aplikace-cesta]* s cestou k řešení **GeekQuiz** , které najdete ve složce **Source\Ex1-DeployingWebSiteToStaging\Begin** tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Inicializace Gitu a první potvrzení](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="1ba1c-367">*Inicializace Gitu a první potvrzení*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="1ba1c-368">Spuštěním následujícího příkazu nahrajte webovou aplikaci do vzdáleného úložiště **Git** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="1ba1c-369">Zástupný symbol nahraďte adresou URL, kterou jste získali z portálu pro správu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="1ba1c-370">Zobrazí se výzva k zadání hesla pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Doručování do Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="1ba1c-372">*Doručování do Azure*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-373">Když nasadíte obsah do hostitele FTP nebo úložiště GIT webové aplikace, musíte provést ověření pomocí **přihlašovacích údajů pro nasazení** , které jste vytvořili na stránkách pro správu **rychlé zprovoznění** nebo **řídicího panelu** webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="1ba1c-374">Pokud vaše přihlašovací údaje pro nasazení neznáte, můžete je snadno obnovit pomocí portálu pro správu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="1ba1c-375">Otevřete stránku **řídicí panel** webové aplikace a klikněte na odkaz **resetovat přihlašovací údaje pro nasazení** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="1ba1c-376">Zadejte nové heslo a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="1ba1c-377">Přihlašovací údaje pro nasazení jsou platné pro použití se všemi webovými aplikacemi, které jsou přidružené k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="1ba1c-378">Aby bylo možné ověřit, zda byla webová aplikace úspěšně vložena do Azure, přejděte zpět na portál pro správu a klikněte na **weby**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="1ba1c-379">Vyhledejte svou webovou aplikaci a rozbalte položku, abyste zobrazili pracovní pozici pracovního serveru.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="1ba1c-380">Kliknutím na jeho **název** přejdete na stránku správy.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="1ba1c-381">Kliknutím na **nasazení** zobrazte **historii nasazení**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="1ba1c-382">Ověřte, že existuje **aktivní nasazení** s *&quot;úvodní&quot;potvrzení* .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![Aktivní nasazení](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="1ba1c-384">*Aktivní nasazení*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-384">*Active deployment*</span></span>
13. <span data-ttu-id="1ba1c-385">Nakonec na panelu příkazů klikněte na tlačítko **Procházet** a přejděte do webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![Procházet webovou aplikaci](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="1ba1c-387">*Procházet webovou aplikaci*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-387">*Browse web app*</span></span>
14. <span data-ttu-id="1ba1c-388">Pokud je aplikace úspěšně nasazená, zobrazí se stránka pro přihlášení kvízu informatik.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-389">Adresa URL adresy nasazené aplikace obsahuje název webové aplikace následovaný po *přípravě*.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![Aplikace spuštěná v přípravném prostředí](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="1ba1c-391">*Aplikace spuštěná v přípravném prostředí*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="1ba1c-392">Pokud chcete aplikaci prozkoumat, klikněte na **zaregistrovat** a zaregistrujte nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="1ba1c-393">Vyplňte podrobnosti účtu zadáním uživatelského jména, e-mailové adresy a hesla.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="1ba1c-394">V dalším kroku aplikace zobrazuje první otázku kvízu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="1ba1c-395">Odpovězte na pár otázek a ujistěte se, že funguje podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![Aplikace připravená k použití](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="1ba1c-397">*Aplikace připravená k použití*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="1ba1c-398">Úloha 4 – propagace webové aplikace do produkčního prostředí</span><span class="sxs-lookup"><span data-stu-id="1ba1c-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="1ba1c-399">Teď, když jste ověřili, že webová aplikace funguje správně v přípravném prostředí, jste připraveni ji propagovat na produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="1ba1c-400">V této úloze provedete záměnu pracovní pozice webu na pozici produkčního pracoviště.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="1ba1c-401">Vraťte se na portál pro správu a vyberte pracovní pozici pracovního serveru.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="1ba1c-402">Na panelu příkazů klikněte na **prohodit** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-402">Click **Swap** in the command bar.</span></span>

    ![Přeměna do produkčního prostředí](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="1ba1c-404">*Přeměna do produkčního prostředí*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-404">*Swap to production*</span></span>
2. <span data-ttu-id="1ba1c-405">Kliknutím na **Ano** v potvrzovacím dialogovém okně pokračujte v operaci swap.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="1ba1c-406">Azure okamžitě zamění obsah produkčního webu s obsahem pracovní lokality.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-407">Některá nastavení ze připravené verze se automaticky zkopírují do produkční verze (např. přepsání připojovacích řetězců, mapování obslužných rutin atd.), ostatní nastavení se ale nezmění (například koncové body DNS, vazby SSL atd.).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![Potvrzení operace prohození](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="1ba1c-409">*Potvrzení operace prohození*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="1ba1c-410">Po dokončení prohození vyberte produkční slot a kliknutím na tlačítko **Procházet** na panelu příkazů otevřete provozní Web.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="1ba1c-411">Všimněte si adresy URL v adresním řádku.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-412">Možná budete muset aktualizovat prohlížeč, aby se mezipaměť vymazala.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="1ba1c-413">V Internet Exploreru to můžete udělat stisknutím **kombinace kláves CTRL + R**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![Webová aplikace spuštěná v produkčním prostředí](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="1ba1c-415">V konzole **GitBash** aktualizujte VZDÁLENOU adresu URL pro místní úložiště Git, aby se cílí na produkční slot.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="1ba1c-416">Uděláte to tak, že spustíte následující příkaz, kterým nahradíte zástupné symboly vaším uživatelským jménem nasazení a název vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-417">V následujících cvičeních provedete změny v produkčním webu místo přípravy jenom pro jednoduchost testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="1ba1c-418">Ve scénáři reálného světa se doporučuje před zvýšením úrovně produkčního prostředí ověřit změny v přípravném prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="1ba1c-419">Cvičení 3: provádění vrácení nasazení v produkčním prostředí</span><span class="sxs-lookup"><span data-stu-id="1ba1c-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="1ba1c-420">K dispozici jsou situace, kdy nemáte přípravný slot pro provádění horkého swapu mezi příchodem a výrobou, například pokud pracujete s **bezplatným** nebo **sdíleným** režimem.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="1ba1c-421">V těchto scénářích byste měli testovat aplikaci v testovacím prostředí – buď místně, nebo ve vzdálené lokalitě – před nasazením do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="1ba1c-422">Je však možné, že v produkčním prostředí může dojít k problému, který nebyl zjištěn během testovací fáze.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="1ba1c-423">V takovém případě je důležité mít mechanismus snadného přepnutí na předchozí a více stabilní verze aplikace co nejrychleji.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="1ba1c-424">V **Azure App Service**umožňuje průběžné nasazování ze správy zdrojového kódu to díky akci **opětovného nasazení** , která je k dispozici na portálu pro správu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="1ba1c-425">Azure sleduje nasazení přidružená k potvrzením, která jsou vložená do úložiště, a poskytuje možnost znovu nasadit aplikaci pomocí libovolného z předchozích nasazení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="1ba1c-426">V tomto cvičení provedete změnu kódu v aplikaci **informatik kvízu** , která záměrně vloží *chybu*.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="1ba1c-427">Aplikaci nasadíte do produkčního prostředí, aby se zobrazila chyba. potom můžete využít funkci opětovného nasazení a vrátit se k předchozímu stavu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="1ba1c-428">Úloha 1 – aktualizace aplikace informatik kvíz</span><span class="sxs-lookup"><span data-stu-id="1ba1c-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="1ba1c-429">V tomto úkolu refaktorujte malé části kódu třídy **TriviaController** , abyste mohli extrahovat část logiky, která načte vybranou možnost kvízu z databáze do nové metody.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="1ba1c-430">Přepněte do instance sady Visual Studio s řešením **GeekQuiz** z předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="1ba1c-431">V **Průzkumník řešení**otevřete soubor **TriviaController.cs** ve složce **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="1ba1c-432">Vyhledejte metodu **StoreAsync** a vyberte kód zvýrazněný na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![Výběr kódu](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="1ba1c-434">*Výběr kódu*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-434">*Selecting the code*</span></span>
4. <span data-ttu-id="1ba1c-435">Klikněte pravým tlačítkem myši na vybraný kód, rozbalte nabídku **refaktoration** a vyberte **Extrahovat metodu...** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![Extrakce kódu jako nové metody](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="1ba1c-437">*Výběr metody extrakce*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="1ba1c-438">V dialogovém okně **Extrahovat metodu** pojmenujte novou metodu *MatchesOption* a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![Zadání názvu metody](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="1ba1c-440">*Určení názvu extrahované metody*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="1ba1c-441">Vybraný kód je poté extrahován do metody **MatchesOption** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="1ba1c-442">Výsledný kód je zobrazen v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="1ba1c-443">Změny uložte stisknutím **kombinace kláves CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="1ba1c-444">Úloha 2 – opětovné nasazení aplikace informatik kvíz</span><span class="sxs-lookup"><span data-stu-id="1ba1c-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="1ba1c-445">Nyní budete předávat změny, které jste provedli v předchozím úkolu, do úložiště, které aktivuje nové nasazení do provozního prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="1ba1c-446">Pak Troubleshot problém pomocí **vývojářských nástrojů F12** , které poskytuje Internet Explorer, a pak proveďte vrácení zpět k předchozímu nasazení z portálu pro správu Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="1ba1c-447">Otevřete novou konzolu **Git bash** a nasaďte aktualizovanou aplikaci na Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="1ba1c-448">Spuštěním následujících příkazů nahrajte změny do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="1ba1c-449">Aktualizujte zástupný text *[Your-Application-Path]* cestou k řešení **GeekQuiz** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="1ba1c-450">Zobrazí se výzva k zadání hesla pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Vložení refaktoringového kódu do Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="1ba1c-452">*Vložení refaktoringového kódu do Azure*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="1ba1c-453">Spusťte Internet Explorer a přejděte do vaší webové aplikace (např. `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="1ba1c-454">Přihlaste se pomocí dříve vytvořených přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="1ba1c-455">Stisknutím klávesy **F12** spusťte vývojové nástroje, vyberte kartu **síť** a kliknutím na tlačítko **Přehrát** spusťte záznam.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="1ba1c-456">![Spouští se záznam v síti.](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Spouští se záznam v síti.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="1ba1c-457">*Spouští se záznam v síti.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-457">*Starting network recording*</span></span>
5. <span data-ttu-id="1ba1c-458">Vyberte libovolnou možnost kvízu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-458">Select any option of the quiz.</span></span> <span data-ttu-id="1ba1c-459">Uvidíte, že se nic nestane.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="1ba1c-460">V okně **F12** položka odpovídající požadavku POST HTTP zobrazí výsledek http **500** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![Chyba HTTP 500](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="1ba1c-462">*Chyba HTTP 500*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="1ba1c-463">Vyberte kartu **Konzola** . S podrobnostmi o příčině se protokoluje chyba.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![Chyba protokolu](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="1ba1c-465">*Chyba protokolu*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-465">*Logged error*</span></span>
8. <span data-ttu-id="1ba1c-466">Vyhledejte část s podrobnostmi o chybě.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-466">Locate the details part of the error.</span></span> <span data-ttu-id="1ba1c-467">Tato chyba je jasně způsobena refaktoringem kódu, který jste protvrdili v předchozích krocích.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="1ba1c-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="1ba1c-469">Nezavírejte prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-469">Do not close the browser.</span></span>
10. <span data-ttu-id="1ba1c-470">V nové instanci prohlížeče přejděte na [portál pro správu Azure](https://manage.windowsazure.com) a přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="1ba1c-471">Vyberte **websites** a klikněte na webovou aplikaci, kterou jste vytvořili v cvičení 2.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="1ba1c-472">Přejděte na stránku **nasazení** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="1ba1c-473">Všimněte si, že všechna potvrzení změn jsou uvedena v historii nasazení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![Seznam existujících nasazení](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="1ba1c-475">*Seznam existujících nasazení*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="1ba1c-476">Vyberte předchozí potvrzení a klikněte na panelu příkazů na **znovu nasadit** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![Opětovné nasazení předchozího potvrzení změn](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="1ba1c-478">*Opětovné nasazení předchozího potvrzení změn*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="1ba1c-479">Po zobrazení výzvy k potvrzení klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-479">When prompted to confirm, click **Yes**.</span></span>

    ![Potvrzení opětovného nasazení](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="1ba1c-481">Po dokončení nasazení přepněte zpátky do instance prohlížeče s vaší webovou aplikací a stiskněte klávesy **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="1ba1c-482">Klikněte na kteroukoli z možností.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-482">Click any of the options.</span></span> <span data-ttu-id="1ba1c-483">Nyní bude provedeno překlápění animace a zobrazí se výsledek (*správný/nesprávný*).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="1ba1c-484">Volitelné Přepněte do konzoly **Git bash** a spusťte následující příkazy, které se vrátí k předchozímu potvrzení změn.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-485">Tyto příkazy vytvoří nové potvrzení, které zruší všechny změny v úložišti Git, které byly provedeny v nesprávném potvrzení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="1ba1c-486">Azure pak znovu nasadí aplikaci pomocí nového potvrzení změn.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="1ba1c-487">Cvičení 4: škálování pomocí Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1ba1c-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="1ba1c-488">**Bloby** představují nejjednodušší způsob, jak ukládat velké objemy nestrukturovaných textových nebo binárních dat, jako je video, zvuk a obrázky.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="1ba1c-489">Když přesunete statický obsah vaší aplikace do úložiště, pomůže vám škálovat aplikaci tím, že obsluhuje obrázky nebo dokumenty přímo v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="1ba1c-490">V tomto cvičení přesunete statický obsah vaší aplikace do kontejneru objektů BLOB.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="1ba1c-491">Potom nakonfigurujete aplikaci tak, aby do kontejneru objektů BLOB přidala **pravidlo pro přepsání adresy URL ASP.NET** v **souboru Web. config** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="1ba1c-492">Úloha 1 – Vytvoření účtu Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1ba1c-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="1ba1c-493">V této úloze se dozvíte, jak vytvořit nový účet úložiště pomocí portálu pro správu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="1ba1c-494">Přejděte na [portál pro správu Azure](https://manage.windowsazure.com) a přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="1ba1c-495">Vybrat **Nový | Data Services | Úložiště | Rychlé vytvoření** a začněte vytvářet nový účet úložiště.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="1ba1c-496">Zadejte jedinečný název pro účet a vyberte **oblast** ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="1ba1c-497">Pokračujte kliknutím na **vytvořit účet úložiště** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="1ba1c-498">![Vytváří se nový účet úložiště.](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Vytváří se nový účet úložiště.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="1ba1c-499">*Vytváří se nový účet úložiště.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="1ba1c-500">V části **úložiště** počkejte, než se stav nového účtu úložiště změní na *online* , aby bylo možné pokračovat v následujícím kroku.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="1ba1c-501">![Účet úložiště se vytvořil.](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Účet úložiště se vytvořil.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="1ba1c-502">*Účet úložiště se vytvořil.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-502">*Storage Account created*</span></span>
4. <span data-ttu-id="1ba1c-503">Klikněte na název účtu úložiště a potom klikněte na odkaz **řídicí panel** v horní části stránky.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="1ba1c-504">Stránka **řídicí panel** poskytuje informace o stavu účtu a koncových bodech služby, které lze použít v rámci svých aplikací.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="1ba1c-505">![Zobrazuje se řídicí panel účtu úložiště.](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Zobrazuje se řídicí panel účtu úložiště.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="1ba1c-506">*Zobrazuje se řídicí panel účtu úložiště.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="1ba1c-507">Na navigačním panelu klikněte na tlačítko **Správa přístupových klíčů** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="1ba1c-508">![Tlačítko pro správu přístupových klíčů](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Tlačítko pro správu přístupových klíčů")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="1ba1c-509">*Tlačítko pro správu přístupových klíčů*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="1ba1c-510">V dialogovém okně **Správa přístupových klíčů** zkopírujte **název účtu úložiště** a **Primární přístupový klíč** , protože je budete potřebovat v následujícím cvičení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="1ba1c-511">Pak zavřete dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="1ba1c-512">![Dialogové okno Správa přístupového klíče](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Dialogové okno Správa přístupového klíče")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="1ba1c-513">*Dialogové okno Správa přístupového klíče*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="1ba1c-514">Úloha 2 – nahrání Assetu do Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1ba1c-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="1ba1c-515">V této úloze použijete okno Průzkumník serveru ze sady Visual Studio pro připojení k vašemu účtu úložiště.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="1ba1c-516">Pak vytvoříte kontejner objektů BLOB a nahrajete do kontejneru soubor s logem informatik kvízu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="1ba1c-517">Přepněte do instance sady Visual Studio s řešením **GeekQuiz** z předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="1ba1c-518">V řádku nabídek vyberte **Zobrazit** a pak klikněte na **Průzkumník serveru**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="1ba1c-519">V **Průzkumník serveru**klikněte pravým tlačítkem myši na uzel **Azure** a vyberte **připojit k Azure...** . Přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![Připojení k Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="1ba1c-521">*Připojení k Azure*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="1ba1c-522">Rozbalte uzel **Azure** , klikněte pravým tlačítkem na **úložiště** a vyberte **připojit externí úložiště...** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="1ba1c-523">V dialogovém okně **Přidat nový účet úložiště** zadejte **název účtu** a **klíč účtu** , který jste získali v předchozí úloze, a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![Dialogové okno Přidat nový účet úložiště](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="1ba1c-525">*Dialogové okno Přidat nový účet úložiště*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="1ba1c-526">Váš účet úložiště by se měl zobrazit pod uzlem **úložiště** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="1ba1c-527">Rozbalte svůj účet úložiště, klikněte pravým tlačítkem na **objekty blob** a vyberte **vytvořit kontejner objektů BLOB...** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="1ba1c-528">![Vytvořit kontejner objektů BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Vytvořit kontejner objektů blob")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="1ba1c-529">*Vytvořit kontejner objektů BLOB*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="1ba1c-530">V dialogovém okně **vytvořit kontejner objektů BLOB** zadejte název kontejneru objektů BLOB a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="1ba1c-531">![Dialogové okno vytvořit kontejner objektů BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Dialogové okno vytvořit kontejner objektů BLOB")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="1ba1c-532">*Dialogové okno vytvořit kontejner objektů BLOB*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="1ba1c-533">Nový kontejner objektů BLOB by měl být přidán do uzlu **objekty blob** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="1ba1c-534">Změňte přístupová oprávnění v kontejneru tak, aby kontejner byl veřejný.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="1ba1c-535">Provedete to tak, že kliknete pravým tlačítkem na kontejner **imagí** a vyberete **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="1ba1c-536">![vlastnosti kontejneru imagí](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "vlastnosti kontejneru imagí")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="1ba1c-537">*Vlastnosti kontejneru imagí*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-537">*Images container properties*</span></span>
9. <span data-ttu-id="1ba1c-538">V okně **vlastnosti** nastavte **veřejný přístup pro čtení** na **kontejner**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="1ba1c-539">![Změna veřejné vlastnosti přístupu pro čtení](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Změna veřejné vlastnosti přístupu pro čtení")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="1ba1c-540">*Změna veřejné vlastnosti přístupu pro čtení*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="1ba1c-541">Když se zobrazí dotaz, jestli jste si jisti, že chcete změnit vlastnost veřejného přístupu, klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="1ba1c-542">![Upozornění Microsoft Visual Studio](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Upozornění Microsoft Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="1ba1c-543">*Upozornění Microsoft Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="1ba1c-544">V **Průzkumník serveru**klikněte pravým tlačítkem na kontejner objektů BLOB **imagí** a vyberte **Zobrazit kontejner objektů BLOB**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="1ba1c-545">![Zobrazit kontejner objektů BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Zobrazit kontejner objektů BLOB")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="1ba1c-546">*Zobrazit kontejner objektů BLOB*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-546">*View Blob Container*</span></span>
12. <span data-ttu-id="1ba1c-547">Kontejner imagí by měl být otevřen v novém okně a legenda bez položek by měla být zobrazena.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="1ba1c-548">Kliknutím na ikonu **nahrát** nahrajte soubor do kontejneru objektů BLOB.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="1ba1c-549">![Kontejner imagí bez záznamů](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Kontejner imagí bez záznamů")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="1ba1c-550">*Kontejner imagí bez záznamů*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="1ba1c-551">V dialogovém okně **nahrát objekt BLOB** přejděte do složky **assets (prostředky** ) v testovacím prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="1ba1c-552">Vyberte soubor **logo-Big. png** a klikněte na **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="1ba1c-553">Počkejte, než se soubor nahraje.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="1ba1c-554">Až se nahrávání dokončí, soubor by měl být uvedený v kontejneru images.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="1ba1c-555">Pravým tlačítkem myši klikněte na položku soubor a vyberte možnost **Kopírovat adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="1ba1c-556">![Kopírovat adresu URL objektu BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Kopírovat adresu URL souboru objektu BLOB")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="1ba1c-557">*Kopírovat adresu URL objektu BLOB*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="1ba1c-558">Otevřete Internet Explorer a vložte adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="1ba1c-559">V prohlížeči by se měl zobrazit následující obrázek.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="1ba1c-560">![Obrázek logo-Big. png z Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "Obrázek logo-Big. png z úložiště")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="1ba1c-561">*Obrázek logo-Big. png z Azure Blob Storage*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="1ba1c-562">Úloha 3 – aktualizace řešení pro využívání statického obsahu z Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1ba1c-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="1ba1c-563">V této úloze nakonfigurujete řešení **GeekQuiz** , aby se využila bitová kopie nahraná do Azure Blob Storage (namísto image umístěná ve webové aplikaci) přidáním pravidla pro přepsání adresy URL ASP.NET v souboru **Web. config** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="1ba1c-564">V aplikaci Visual Studio otevřete soubor **Web. config** v rámci projektu **GeekQuiz** a vyhledejte prvek **&gt;&lt;System. webServer** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="1ba1c-565">Přidejte následující kód, který přidá pravidlo pro přepsání adresy URL a aktualizuje zástupný text názvem svého účtu úložiště.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="1ba1c-566">(Fragment kódu – *WebSitesInProduction-Ex4-UrlRewriteRule*)</span><span class="sxs-lookup"><span data-stu-id="1ba1c-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="1ba1c-567">Přepsání adresy URL je proces zachycení příchozího webového požadavku a přesměrování požadavku na jiný prostředek.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="1ba1c-568">Pravidla přepisu adresy URL přidávají modulu přepisu, když je potřeba přesměrovat požadavek a kde by se měla přesměrovat.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="1ba1c-569">Pravidlo přepisování se skládá ze dvou řetězců: vzor, který má být hledán v požadované adrese URL (obvykle pomocí regulárních výrazů), a řetězec, který má nahradit vzor, pokud byl nalezen.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="1ba1c-570">Další informace najdete v tématu [přepsání adresy URL v ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="1ba1c-571">Změny uložte stisknutím **kombinace kláves CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="1ba1c-572">Otevřete novou konzolu **Git bash** a nasaďte aktualizovanou aplikaci na Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="1ba1c-573">Spuštěním následujících příkazů nahrajte změny do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="1ba1c-574">Aktualizujte zástupný text *[Your-Application-Path]* cestou k řešení **GeekQuiz** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="1ba1c-575">Zobrazí se výzva k zadání hesla pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Nasazení aktualizace do Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="1ba1c-577">*Nasazení aktualizace do Azure*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="1ba1c-578">Úloha 4 – ověření</span><span class="sxs-lookup"><span data-stu-id="1ba1c-578">Task 4 – Verification</span></span>

<span data-ttu-id="1ba1c-579">V této úloze použijete **Internet Explorer** k procházení aplikace **informatik kvíz** a zkontrolujete, že pravidlo pro přepsání adresy URL pro Image funguje a že budete přesměrováni na Image hostovanou v **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="1ba1c-580">Spusťte Internet Explorer a přejděte do vaší webové aplikace (např. `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="1ba1c-581">Přihlaste se pomocí dříve vytvořených přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="1ba1c-582">![Zobrazení webové aplikace kvízu informatik s obrázkem](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Zobrazení webové aplikace kvízu informatik s obrázkem")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="1ba1c-583">*Zobrazení webové aplikace kvízu informatik s obrázkem*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="1ba1c-584">Stisknutím klávesy **F12** spusťte vývojové nástroje, vyberte kartu **síť** a spusťte záznam.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="1ba1c-585">![Spouští se záznam v síti.](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Spouští se záznam v síti.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="1ba1c-586">*Spouští se záznam v síti.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-586">*Starting network recording*</span></span>
3. <span data-ttu-id="1ba1c-587">Stisknutím **kombinace kláves CTRL + F5** aktualizujte webovou stránku.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="1ba1c-588">Po načtení stránky by se měla zobrazit žádost HTTP adresy URL **/img/logo-Big.png** s výsledkem http **301** (přesměrování) a jinou žádostí o `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url s výsledkem http **200** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="1ba1c-589">![Ověření přesměrování adresy URL](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Zobrazuje se přesměrování v nástrojích pro vývoj")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="1ba1c-590">*Ověření přesměrování adresy URL*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="1ba1c-591">Cvičení 5: použití automatického škálování pro Web Apps</span><span class="sxs-lookup"><span data-stu-id="1ba1c-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="1ba1c-592">Toto cvičení je volitelné, protože vyžaduje podporu webového zatížení &amp; testování výkonu, které je k dispozici pouze pro **Visual Studio 2013 Ultimate Edition**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="1ba1c-593">Další informace o konkrétních funkcích Visual Studio 2013 najdete v [tématu](https://www.microsoft.com/visualstudio/eng/products/compare)porovnání verzí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>

<span data-ttu-id="1ba1c-594">**Azure App Service Web Apps** poskytuje funkci automatického škálování pro webové aplikace běžící ve **standardním režimu**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="1ba1c-595">Automatické škálování umožňuje Azure automaticky škálovat počet instancí webové aplikace v závislosti na zatížení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="1ba1c-596">Když je zapnuté automatické škálování, Azure zkontroluje procesor vaší webové aplikace jednou za pět minut a v daném časovém okamžiku přidá instance podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="1ba1c-597">Pokud je využití procesoru nízké, Azure odstraní instance jednou za dvě hodiny, aby se zajistilo, že výkon vaší webové aplikace nebude degradován.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="1ba1c-598">V tomto cvičení provedete kroky nutné ke konfiguraci funkce **automatického škálování** pro webovou aplikaci **informatik kvíz** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="1ba1c-599">Tuto funkci ověříte spuštěním zátěžového testu sady Visual Studio pro vygenerování dostatečného zatížení procesoru v aplikaci pro aktivaci upgradu instance.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="1ba1c-600">Úloha 1 – Konfigurace automatického škálování na základě metriky procesoru</span><span class="sxs-lookup"><span data-stu-id="1ba1c-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="1ba1c-601">V této úloze použijete portál pro správu Azure k povolení funkce automatického škálování pro webovou aplikaci, kterou jste vytvořili v cvičení 2.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="1ba1c-602">Na [portálu pro správu Azure](https://manage.windowsazure.com/)vyberte **weby** a klikněte na webovou aplikaci, kterou jste vytvořili v cvičení 2.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="1ba1c-603">Přejděte na stránku **škálování** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="1ba1c-604">V části **kapacita** vyberte možnost **CPU** pro **škálování podle konfigurace metriky** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-605">Při škálování podle CPU Azure dynamicky přizpůsobí počet instancí, které aplikace používá, pokud se změní využití procesoru.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="1ba1c-606">![Výběr pro škálování podle procesoru](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Výběr metriky procesoru pro automatické škálování")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="1ba1c-607">*Výběr pro škálování podle procesoru*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="1ba1c-608">Změňte **cílovou konfiguraci procesoru** na **20**-**40** procent.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-609">Tento rozsah představuje průměrné využití procesoru vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="1ba1c-610">Azure bude přidávat nebo odebírat instance, aby se vaše webová aplikace udržovala v tomto rozsahu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="1ba1c-611">Minimální a maximální počet instancí použitých pro škálování je zadaný v konfiguraci **počtu instancí** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="1ba1c-612">Azure nebude nikdy nad rámec tohoto limitu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="1ba1c-613">Výchozí hodnoty **CÍLOVÉHO procesoru** se upravují pouze pro účely tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="1ba1c-614">Konfigurací rozsahu procesoru s malými hodnotami zvýšíte pravděpodobnost aktivace automatického škálování, když se na aplikaci umístí střední zatížení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="1ba1c-615">![Změna cílového procesoru na hodnotu mezi 20 a 40%](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Změna cílového procesoru na hodnotu mezi 20 a 40%")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="1ba1c-616">*Změna cílového procesoru na hodnotu mezi 20 a 40%*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="1ba1c-617">Změny uložte kliknutím na **Uložit** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="1ba1c-618">Úloha 2 – zátěžové testování pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ba1c-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="1ba1c-619">Teď, když je nakonfigurované **Automatické škálování** , vytvoříte v aplikaci Visual Studio **projekt webového výkonu a zátěžového testu** , který vygeneruje některé zatížení procesoru ve vaší webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="1ba1c-620">Otevřete **Visual Studio Ultimate 2013** a vyberte **soubor | Nové | Projekt...** pro spuštění nového řešení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="1ba1c-621">![Vytvoření nového projektu](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Vytvoření nového projektu")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="1ba1c-622">*Vytvoření nového projektu*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-622">*Creating a new project*</span></span>
2. <span data-ttu-id="1ba1c-623">V dialogovém okně **Nový projekt** vyberte v vizuálu  **C# projekt testování výkonu webu a zátěžový test | Karta test** . Ujistěte se, že je vybraná možnost **.NET Framework 4,5** , název projektu *WebAndLoadTestProject*, vyberte **umístění** a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="1ba1c-624">![Vytvoření nového projektu webového a zátěžového testu](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Vytvoření nového projektu webového a zátěžového testu")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="1ba1c-625">*Vytvoření nového projektu webového a zátěžového testu*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="1ba1c-626">V **WebTest1. webtest** klikněte pravým tlačítkem myši na uzel **WebTest1** a klikněte na **Přidat žádost**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="1ba1c-627">![Přidání žádosti do WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Přidání žádosti do WebTest1")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="1ba1c-628">*Přidání žádosti do WebTest1*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="1ba1c-629">V okně **vlastnosti** nového uzlu požadavku aktualizujte vlastnost **Adresa URL** tak, aby odkazovala na adresu URL vaší webové aplikace (např. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="1ba1c-630">![Změna vlastnosti adresy URL](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Změna vlastnosti adresy URL")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="1ba1c-631">*Změna vlastnosti adresy URL*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="1ba1c-632">V okně **WebTest1. webtest** klikněte pravým tlačítkem myši na **WebTest1** a klikněte na **Přidat smyčku...** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="1ba1c-633">![Přidání smyčky do WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Přidání smyčky do WebTest1")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="1ba1c-634">*Přidání smyčky do WebTest1*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="1ba1c-635">V dialogovém okně **přidat podmíněné pravidlo a položky do cyklu** vyberte pravidlo **smyčky for** a upravte následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="1ba1c-636">**Koncová hodnota:** 1000</span><span class="sxs-lookup"><span data-stu-id="1ba1c-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="1ba1c-637">**Název kontextového parametru:** Iterátor</span><span class="sxs-lookup"><span data-stu-id="1ba1c-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="1ba1c-638">**Přírůstková hodnota:** 1</span><span class="sxs-lookup"><span data-stu-id="1ba1c-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="1ba1c-639">![Výběr pravidla smyčky for a aktualizace vlastností](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Výběr pravidla smyčky for a aktualizace vlastností")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="1ba1c-640">*Výběr pravidla smyčky for a aktualizace vlastností*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="1ba1c-641">V části **smyčka Items (položky v cyklu** ) vyberte požadavek, který jste dříve vytvořili jako první a poslední položku pro smyčku.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="1ba1c-642">Pokračujte kliknutím na tlačítko **OK** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="1ba1c-643">![Výběr první a poslední položky pro smyčku](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Výběr první a poslední položky pro smyčku")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="1ba1c-644">*Výběr první a poslední položky pro smyčku*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="1ba1c-645">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **WebAndLoadTestProject** , rozbalte nabídku **Přidat** a vyberte **zátěžový test...** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="1ba1c-646">![Přidání zátěžového testu do projektu WebAndLoadTestProject](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Přidání zátěžového testu do projektu WebAndLoadTestProject")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="1ba1c-647">*Přidání zátěžového testu do projektu WebAndLoadTestProject*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="1ba1c-648">V dialogovém okně **nový Průvodce zátěžovým testem** klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="1ba1c-649">![Nový Průvodce zátěžovým testem](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "Nový Průvodce zátěžovým testem")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="1ba1c-650">*Nový Průvodce zátěžovým testem*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="1ba1c-651">Na stránce **scénář** vyberte **Nepoužívat časy přemýšlení** a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="1ba1c-652">![Výběr nepoužití časů promýšlení](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Výběr nepoužití časů promýšlení")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="1ba1c-653">*Výběr nepoužití časů promýšlení*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="1ba1c-654">Na stránce **vzor zatížení** se ujistěte, že je vybraná možnost **konstantního zatížení** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="1ba1c-655">Změňte nastavení **počet uživatelů** na **250** uživatelů a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="1ba1c-656">![Změna počtu uživatelů na 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Změna počtu uživatelů na 250")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="1ba1c-657">*Změna počtu uživatelů na 250*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="1ba1c-658">Na stránce **model kombinace testů** vyberte na **základě pořadí sekvenčních testů** a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="1ba1c-659">![Výběr modelu kombinace testů](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Výběr modelu kombinace testů")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="1ba1c-660">*Výběr modelu kombinace testů*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="1ba1c-661">Na stránce **model** poměru testů klikněte na tlačítko **Přidat...** a přidejte do kombinace test.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="1ba1c-662">![Přidání testu do kombinace testů](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Přidání testu do kombinace testů")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="1ba1c-663">*Přidání testu do kombinace testů*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="1ba1c-664">V dialogovém okně **Přidat testy** poklikejte na **WebTest1** a přidejte test do seznamu **vybraných testů** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="1ba1c-665">Pokračujte kliknutím na tlačítko **OK** .</span><span class="sxs-lookup"><span data-stu-id="1ba1c-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="1ba1c-666">![Přidání testu WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Přidání testu WebTest1")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="1ba1c-667">*Přidání testu WebTest1*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="1ba1c-668">Zpátky na stránce **kombinace testů** klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="1ba1c-669">![Dokončuje se stránka kombinace testů.](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Dokončuje se stránka kombinace testů.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="1ba1c-670">*Dokončuje se stránka kombinace testů.*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="1ba1c-671">Na stránce **kombinace sítě** klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="1ba1c-672">![Kliknutí na tlačítko Další na stránce kombinace sítě](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Kliknutí na tlačítko Další na stránce kombinace sítě")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="1ba1c-673">*Kliknutí na tlačítko Další na stránce kombinace sítě*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="1ba1c-674">Na stránce **kombinace prohlížečů** jako typ prohlížeče vyberte **Internet Explorer 10,0** a klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="1ba1c-675">![Výběr typu prohlížeče](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Výběr typu prohlížeče")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="1ba1c-676">*Výběr typu prohlížeče*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="1ba1c-677">Na stránce **sady čítačů** klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="1ba1c-678">![Kliknutí na další na stránce sady čítačů](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Kliknutí na další na stránce sady čítačů")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="1ba1c-679">*Kliknutí na další na stránce sady čítačů*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="1ba1c-680">Na stránce **nastavení spuštění** nastavte **dobu trvání zátěžového testu** na **5 minut** a klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="1ba1c-681">![Nastavení doby trvání zátěžového testu na 5 minut](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Nastavení doby trvání zátěžového testu na 5 minut")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="1ba1c-682">*Nastavení doby trvání zátěžového testu na 5 minut*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="1ba1c-683">V **Průzkumník řešení**dvakrát klikněte na soubor **Local. Settings** a prozkoumejte nastavení testu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="1ba1c-684">Ve výchozím nastavení používá Visual Studio místní počítač ke spuštění testů.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-685">Alternativně můžete nakonfigurovat projekt testů tak, aby spouštěl zátěžové testy v cloudu pomocí **Azure test Plans**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="1ba1c-686">Azure Test Plans poskytuje cloudovou službu zátěžového testování, která simuluje realističtější zatížení, což vyloučí omezení místních prostředí, jako je kapacita procesoru, dostupná paměť a šířka pásma sítě.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="1ba1c-687">Další informace o použití Azure Test Plans ke spouštění zátěžových testů naleznete v tématu [scénáře zátěžového testování](/azure/devops/test/load-test/overview?view=vsts).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![Nastavení testu](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="1ba1c-689">Úloha 3 – ověření automatického škálování</span><span class="sxs-lookup"><span data-stu-id="1ba1c-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="1ba1c-690">Nyní spustíte zátěžový test, který jste vytvořili v předchozí úloze, a zjistíte, jak se webová aplikace chová při zatížení.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="1ba1c-691">V **Průzkumník řešení**dvakrát klikněte na **LoadTest1. LoadTest** a otevřete zátěžový test.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="1ba1c-692">![Otevírání LoadTest1. LoadTest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Otevírání LoadTest1. LoadTest")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="1ba1c-693">*Otevírání LoadTest1. LoadTest*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="1ba1c-694">V okně **LoadTest1. LoadTest** kliknutím na první tlačítko v panelu nástrojů Spusťte zátěžový test.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="1ba1c-695">![Spuštění zátěžového testu](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Spuštění zátěžového testu")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="1ba1c-696">*Spuštění zátěžového testu*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-696">*Running the load test*</span></span>
3. <span data-ttu-id="1ba1c-697">Počkejte na dokončení zátěžového testu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-698">Zátěžový test simuluje více uživatelů, kteří odesílají požadavky do webové aplikace současně.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="1ba1c-699">Po spuštění testu můžete monitorovat dostupné čítače a odhalit případné chyby, varování nebo jiné informace, které se týkají vašeho běhu zátěžového testu.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="1ba1c-700">![Zátěžový test běží](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Čeká se na dokončení zátěžového testu.")</span><span class="sxs-lookup"><span data-stu-id="1ba1c-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="1ba1c-701">*Zátěžový test běží*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-701">*Load test running*</span></span>
4. <span data-ttu-id="1ba1c-702">Po dokončení testu se vraťte na portál pro správu a přejděte na stránku **škálování** vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="1ba1c-703">V části **kapacita** byste měli vidět v grafu, že se automaticky nasadila nová instance.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![Automaticky nasazená nová instance](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="1ba1c-705">*Automaticky nasazená nová instance*</span><span class="sxs-lookup"><span data-stu-id="1ba1c-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba1c-706">Může trvat několik minut, než se změny objeví v grafu (Pokud chcete stránku aktualizovat, stiskněte klávesu **CTRL + F5** pravidelně).</span><span class="sxs-lookup"><span data-stu-id="1ba1c-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="1ba1c-707">Pokud žádné změny nevidíte, můžete vyzkoušet následující:</span><span class="sxs-lookup"><span data-stu-id="1ba1c-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="1ba1c-708">Prodloužit dobu trvání zátěžového testu (například na **10 minut**)</span><span class="sxs-lookup"><span data-stu-id="1ba1c-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="1ba1c-709">Snižte maximální a minimální hodnoty **cílového rozsahu procesoru** v konfiguraci automatického škálování vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="1ba1c-710">Spusťte zátěžový test v cloudu pomocí **Azure test Plans**.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="1ba1c-711">Další informace [](/azure/devops/test/load-test/index?view=vsts)</span><span class="sxs-lookup"><span data-stu-id="1ba1c-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="1ba1c-712">Souhrn</span><span class="sxs-lookup"><span data-stu-id="1ba1c-712">Summary</span></span>

<span data-ttu-id="1ba1c-713">V tomto praktickém cvičení jste zjistili, jak nastavit a nasadit aplikaci do produkčních webových aplikací v Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="1ba1c-714">Začali jste zjišťováním a aktualizací databází pomocí **migrace Entity Framework Code First**a pak pokračovali nasazením nových verzí webu pomocí **Gitu** a vrácením se zpět do nejnovější stabilní verze vaší lokality.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="1ba1c-715">Kromě toho jste zjistili, jak škálovat aplikaci pomocí úložiště, aby se váš statický obsah přesunul do kontejneru objektů BLOB.</span><span class="sxs-lookup"><span data-stu-id="1ba1c-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
