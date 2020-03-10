---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 'Část 1: soubor-> Nový projekt | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 1 pokrývá přehled a soubor/nový projekt.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636127"
---
# <a name="part-1-file--new-project"></a><span data-ttu-id="4f1ed-104">1\. část: Soubor > Nový projekt</span><span class="sxs-lookup"><span data-stu-id="4f1ed-104">Part 1: File-> New Project</span></span>

<span data-ttu-id="4f1ed-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="4f1ed-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="4f1ed-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="4f1ed-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="4f1ed-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="4f1ed-109">Část 1 pokrývá přehled a soubor/nový projekt.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-109">Part 1 covers Overview and File/New Project.</span></span>

## <a id="_Toc260221666"></a><span data-ttu-id="4f1ed-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="4f1ed-110">Overview</span></span>

<span data-ttu-id="4f1ed-111">Tento kurz představuje úvod k ASP.NET WebForms.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="4f1ed-112">Začneme pomaleji, takže prostředí pro vývoj na webu na úrovni začátečník je v pořádku.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="4f1ed-113">Aplikace, kterou budeme sestavovat, je jednoduchý online obchod.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)

<span data-ttu-id="4f1ed-114">Uživatelé můžou procházet produkty podle kategorie:</span><span class="sxs-lookup"><span data-stu-id="4f1ed-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="4f1ed-115">Můžou si zobrazit jeden produkt a přidat ho do svého košíku:</span><span class="sxs-lookup"><span data-stu-id="4f1ed-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="4f1ed-116">Můžou si prohlédnout svůj košík a odebrat položky, které už nepotřebují:</span><span class="sxs-lookup"><span data-stu-id="4f1ed-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="4f1ed-117">Při pokračování na rezervaci se zobrazí výzva k zadání</span><span class="sxs-lookup"><span data-stu-id="4f1ed-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="4f1ed-118">Po objednání se zobrazí jednoduchá potvrzovací obrazovka:</span><span class="sxs-lookup"><span data-stu-id="4f1ed-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)

<span data-ttu-id="4f1ed-119">Začneme vytvořením nového projektu WebForms ASP.NET v aplikaci Visual Studio 2010 a my postupně přidáváme funkce pro vytvoření kompletní funkční aplikace.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="4f1ed-120">Podél toho se podíváme na přístup k databázi, zobrazení seznamu a mřížky, stránky aktualizace dat, ověření dat, použití stránek předloh pro konzistentní rozložení stránky, AJAX, ověřování, členství uživatelů a další.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="4f1ed-121">Můžete postupovat podle kroků nebo si můžete stáhnout dokončenou aplikaci z [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="4f1ed-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="4f1ed-122">Můžete použít buď Visual Studio 2010, nebo bezplatný Visual Web Developer 2010 z [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span><span class="sxs-lookup"><span data-stu-id="4f1ed-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="4f1ed-123">K sestavení aplikace můžete použít buď SQL Server, nebo bezplatný SQL Server Express k hostování databáze.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a><span data-ttu-id="4f1ed-124">Soubor/nový projekt</span><span class="sxs-lookup"><span data-stu-id="4f1ed-124">File / New Project</span></span>

<span data-ttu-id="4f1ed-125">Začneme tak, že vybereme nový projekt v nabídce soubor v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="4f1ed-126">Tím se otevře dialogové okno Nový projekt.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="4f1ed-127">Na levé straně vybereme skupinu Visual C# /web Templates a potom v prostředním sloupci zvolíte šablonu webová aplikace v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="4f1ed-128">Pojmenujte projekt TailspinSpyworks a stiskněte tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="4f1ed-129">Tím se vytvoří náš projekt.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-129">This will create our project.</span></span> <span data-ttu-id="4f1ed-130">Pojďme se podívat na složky, které jsou součástí naší aplikace v Průzkumník řešení na pravé straně.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="4f1ed-131">Prázdné řešení není zcela prázdné – přidá základní strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="4f1ed-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="4f1ed-132">Poznamenejte si konvence implementované výchozí šablonou projektu ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="4f1ed-133">Složka "Account" implementuje základní uživatelské rozhraní pro ASP. Podsystém členství v síti.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="4f1ed-134">Složka "skripty" slouží jako úložiště pro soubory JavaScriptu na straně klienta a základní soubory jQuery. js jsou ve výchozím nastavení k dispozici.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="4f1ed-135">Složka Styles (styly) slouží k uspořádání webových vizuálů webu (šablony stylů CSS).</span><span class="sxs-lookup"><span data-stu-id="4f1ed-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="4f1ed-136">Po stisknutí klávesy F5 ke spuštění naší aplikace a vykreslení stránky default. aspx se zobrazí následující.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="4f1ed-137">Naše první vylepšení aplikace bude nahradit soubor style. CSS od výchozích šablon WebForms s třídami šablony stylů CSS a přidruženými obrazovými soubory, které vykreslí vizuální asthetics, které chceme pro naši aplikaci Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="4f1ed-138">Až to uděláte, stránka default. aspx se takto vykreslí.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="4f1ed-139">Všimněte si odkazů na obrázek v pravém horním rohu stránky a položek nabídky, které byly přidány do stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="4f1ed-140">Pouze odkazy "přihlásit" a "účet" odkazují na stránky, které existují (vygenerované výchozí šablonou), a na ostatní stránky, které budeme implementovat při sestavování naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="4f1ed-141">Také přemístím stránku předlohy do adresáře Styles.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="4f1ed-142">I když se jedná jenom o předvolbu, může to chvíli udělat, pokud se rozhodnete, že aplikaci bude možné v budoucnu udělat jako srozumitelnou.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="4f1ed-143">Až to uděláte, budete muset změnit odkazy na hlavní stránku ve všech souborech. aspx vygenerovaných výchozími stránkami WebForms ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4f1ed-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4f1ed-144">Next</span><span class="sxs-lookup"><span data-stu-id="4f1ed-144">Next</span></span>](tailspin-spyworks-part-2.md)
