---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 'Část 1: Přehled a soubor > Nový projekt | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 1 pokrývá přehled a soubor > Nový projekt.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559981"
---
# <a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="e1ed2-104">1\. část: Přehled a Soubor->Nový projekt</span><span class="sxs-lookup"><span data-stu-id="e1ed2-104">Part 1: Overview and File->New Project</span></span>

<span data-ttu-id="e1ed2-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="e1ed2-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="e1ed2-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="e1ed2-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="e1ed2-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="e1ed2-109">Část 1 pokrývá přehled a soubor&gt;nový projekt.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-109">Part 1 covers Overview and File-&gt;New Project.</span></span>

## <a name="overview"></a><span data-ttu-id="e1ed2-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="e1ed2-110">Overview</span></span>

<span data-ttu-id="e1ed2-111">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Web Developer pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="e1ed2-112">Začneme pomaleji, takže prostředí pro vývoj na webu na úrovni začátečník je v pořádku.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="e1ed2-113">Aplikace, kterou budeme sestavovat, je jednoduchý hudební obchod.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="e1ed2-114">Existují tři hlavní části aplikace: nákupy, rezervace a správa.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="e1ed2-115">Návštěvníci můžou procházet alba podle žánru:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="e1ed2-116">Můžou zobrazit jedno album a přidat ho do svého košíku:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="e1ed2-117">Můžou si prohlédnout svůj košík a odebrat položky, které už nepotřebují:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="e1ed2-118">Při pokračování na rezervaci se zobrazí výzva k přihlášení nebo registraci pro uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="e1ed2-119">Po vytvoření účtu můžou Dokončit objednávku vyplněním informací o expedici a platbách.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="e1ed2-120">Abychom vám pomohli něco jednoduchého, máme k dispozici úžasné propagační akce: všechno je zdarma, pokud zadáte propagační kód "FREE".</span><span class="sxs-lookup"><span data-stu-id="e1ed2-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="e1ed2-121">Po objednání se zobrazí jednoduchá potvrzovací obrazovka:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="e1ed2-122">Kromě zákaznických stránek také sestavíme oddíl správce, který obsahuje seznam alb, ze kterých můžou správci vytvářet, upravovat a odstraňovat alba:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-122">In addition to customer-facing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="e1ed2-123">1. soubor-&gt; nový projekt</span><span class="sxs-lookup"><span data-stu-id="e1ed2-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="e1ed2-124">Instalace softwaru</span><span class="sxs-lookup"><span data-stu-id="e1ed2-124">Installing the software</span></span>

<span data-ttu-id="e1ed2-125">V tomto kurzu začnete vytvořením nového projektu ASP.NET MVC 3 pomocí bezplatného programu Visual Web Developer 2010 Express (který je zdarma) a pak postupně přidáváme funkce, které vytvoří kompletní funkční aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="e1ed2-126">Na základě toho se podíváme na přístup k databázi, scénáře pro publikování formulářů, ověřování dat, používání stránek předloh pro konzistentní rozložení stránky, používání AJAX pro aktualizace stránky a ověřování, přihlášení uživatele a další.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="e1ed2-127">Můžete postupovat podle jednotlivých kroků nebo si můžete stáhnout dokončenou aplikaci z [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="e1ed2-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="e1ed2-128">K sestavení aplikace můžete použít buď Visual Studio 2010 SP1 nebo Visual Web Developer 2010 Express SP1 (bezplatnou verzi sady Visual Studio 2010).</span><span class="sxs-lookup"><span data-stu-id="e1ed2-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="e1ed2-129">Pro hostování databáze budeme používat tuto SQL Server Compact (také bezplatnou).</span><span class="sxs-lookup"><span data-stu-id="e1ed2-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="e1ed2-130">Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="e1ed2-131">[Požadavky na Visual Studio Web Developer Express SP1]</span><span class="sxs-lookup"><span data-stu-id="e1ed2-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="e1ed2-132">[Aktualizace nástrojů ASP.NET MVC 3]</span><span class="sxs-lookup"><span data-stu-id="e1ed2-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="e1ed2-133">[SQL Server Compact 4,0] – včetně podpory modulu runtime a nástrojů</span><span class="sxs-lookup"><span data-stu-id="e1ed2-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>

### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="e1ed2-134">Vytvoření nového projektu ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="e1ed2-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="e1ed2-135">Začneme výběrem možnosti nový projekt v nabídce soubor v aplikaci Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="e1ed2-136">Tím se otevře dialogové okno Nový projekt.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="e1ed2-137">Na levé straně vybereme skupinu Visual C# -&gt; web Templates a potom v prostředním sloupci zvolíte šablonu webová aplikace ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="e1ed2-138">Pojmenujte projekt MvcMusicStore a stiskněte tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="e1ed2-139">Tím se zobrazí sekundární dialog, který nám umožní udělat pro náš projekt určitá nastavení specifická pro MVC.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="e1ed2-140">Vyberte následující:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-140">Select the following:</span></span>

<span data-ttu-id="e1ed2-141">Šablona projektu – vybrat prázdné</span><span class="sxs-lookup"><span data-stu-id="e1ed2-141">Project Template - select Empty</span></span>

<span data-ttu-id="e1ed2-142">Zobrazení modulu – výběr Razor</span><span class="sxs-lookup"><span data-stu-id="e1ed2-142">View Engine - select Razor</span></span>

<span data-ttu-id="e1ed2-143">Použít sémantické označení HTML5 – zaškrtnuto</span><span class="sxs-lookup"><span data-stu-id="e1ed2-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="e1ed2-144">Ověřte, že nastavení jsou uvedená níže, a pak stiskněte tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="e1ed2-145">Tím se vytvoří náš projekt.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-145">This will create our project.</span></span> <span data-ttu-id="e1ed2-146">Pojďme se podívat na složky, které byly přidány do naší aplikace v Průzkumník řešení na pravé straně.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="e1ed2-147">Prázdná šablona MVC 3 není zcela prázdná – přidá základní strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="e1ed2-148">ASP.NET MVC využívá některé základní zásady vytváření názvů pro názvy složek:</span><span class="sxs-lookup"><span data-stu-id="e1ed2-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="e1ed2-149">**Složka**</span><span class="sxs-lookup"><span data-stu-id="e1ed2-149">**Folder**</span></span> | <span data-ttu-id="e1ed2-150">**Účel**</span><span class="sxs-lookup"><span data-stu-id="e1ed2-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="e1ed2-151">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="e1ed2-151">**/Controllers**</span></span> | <span data-ttu-id="e1ed2-152">Řadiče reagují na vstup z prohlížeče, rozhodnou se s ním a vrátí odpověď uživateli.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="e1ed2-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="e1ed2-153">**/Views**</span></span> | <span data-ttu-id="e1ed2-154">Zobrazení obsahují šablony uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="e1ed2-155">**/Models**</span><span class="sxs-lookup"><span data-stu-id="e1ed2-155">**/Models**</span></span> | <span data-ttu-id="e1ed2-156">Modely uchovávají a manipulují s daty</span><span class="sxs-lookup"><span data-stu-id="e1ed2-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="e1ed2-157">**/Content**</span><span class="sxs-lookup"><span data-stu-id="e1ed2-157">**/Content**</span></span> | <span data-ttu-id="e1ed2-158">Tato složka obsahuje obrázky, šablony stylů CSS a jakýkoli další statický obsah.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="e1ed2-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="e1ed2-159">**/Scripts**</span></span> | <span data-ttu-id="e1ed2-160">Tato složka obsahuje naše soubory JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="e1ed2-161">Tyto složky jsou zahrnuté i do prázdné aplikace ASP.NET MVC, protože rozhraní ASP.NET MVC ve výchozím nastavení používá přístup "konvence před konfigurací" a vytváří některé výchozí předpoklady založené na zásadách vytváření názvů složek.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="e1ed2-162">Například řadiče ve výchozím nastavení vyhledávají zobrazení ve složce views, aniž byste je museli explicitně zadat ve svém kódu.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="e1ed2-163">Dodávání s výchozími konvencemi omezuje množství kódu, který musíte napsat, a může také usnadnit ostatním vývojářům pochopení vašeho projektu.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="e1ed2-164">Tyto konvence vyvysvětlíme podrobněji, protože sestavíme naši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1ed2-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e1ed2-165">Next</span><span class="sxs-lookup"><span data-stu-id="e1ed2-165">Next</span></span>](mvc-music-store-part-2.md)
