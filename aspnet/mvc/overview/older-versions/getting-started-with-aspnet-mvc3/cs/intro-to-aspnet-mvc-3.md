---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: Úvod do ASP.NET MVC 3 (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457523"
---
# <a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="63e19-103">Úvod do ASP.NET MVC 3 (C#)</span><span class="sxs-lookup"><span data-stu-id="63e19-103">Intro to ASP.NET MVC 3 (C#)</span></span>

<span data-ttu-id="63e19-104">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="63e19-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="63e19-105">K [dispozici je](../../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="63e19-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="63e19-106">Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.</span><span class="sxs-lookup"><span data-stu-id="63e19-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="63e19-107">V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63e19-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="63e19-108">Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="63e19-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="63e19-109">Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="63e19-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="63e19-110">Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:</span><span class="sxs-lookup"><span data-stu-id="63e19-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="63e19-111">Požadavky sady Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="63e19-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="63e19-112">Aktualizace nástrojů MVC 3 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="63e19-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="63e19-113">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)</span><span class="sxs-lookup"><span data-stu-id="63e19-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="63e19-114">Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="63e19-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="63e19-115">Projekt Visual Web Developer se C# zdrojovým kódem je k dispozici pro toto téma.</span><span class="sxs-lookup"><span data-stu-id="63e19-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="63e19-116">[Stáhněte si C# verzi](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="63e19-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="63e19-117">Pokud dáváte přednost Visual Basic, přepněte se na [Visual Basic verzi](../vb/intro-to-aspnet-mvc-3.md) tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="63e19-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="63e19-118">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="63e19-118">What You'll Build</span></span>

<span data-ttu-id="63e19-119">Implementujete jednoduchou aplikaci se seznamem videí, která podporuje vytváření, úpravy a výpis filmů z databáze.</span><span class="sxs-lookup"><span data-stu-id="63e19-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="63e19-120">Níže jsou uvedeny dva snímky obrazovky aplikace, kterou vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="63e19-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="63e19-121">Obsahuje stránku, která zobrazuje seznam filmů z databáze:</span><span class="sxs-lookup"><span data-stu-id="63e19-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="63e19-123">Aplikace také umožňuje přidávat, upravovat a odstraňovat filmy a také zobrazit podrobnosti o jednotlivých uživatelích.</span><span class="sxs-lookup"><span data-stu-id="63e19-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="63e19-124">Všechny scénáře zadávání dat zahrnují ověřování, aby se zajistilo, že jsou data uložená v databázi správná.</span><span class="sxs-lookup"><span data-stu-id="63e19-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="63e19-125">Dovednosti, se kterými se naučíte</span><span class="sxs-lookup"><span data-stu-id="63e19-125">Skills You'll Learn</span></span>

<span data-ttu-id="63e19-126">Tady je seznam toho, co se naučíte:</span><span class="sxs-lookup"><span data-stu-id="63e19-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="63e19-127">Jak vytvořit nový projekt ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="63e19-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="63e19-128">Vytvoření řadičů a zobrazení ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="63e19-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="63e19-129">Vytvoření nové databáze pomocí Entity Framework Code First paradigma</span><span class="sxs-lookup"><span data-stu-id="63e19-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="63e19-130">Jak načíst a zobrazit data</span><span class="sxs-lookup"><span data-stu-id="63e19-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="63e19-131">Jak upravit data a povolit ověřování dat.</span><span class="sxs-lookup"><span data-stu-id="63e19-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="63e19-132">Začínáme</span><span class="sxs-lookup"><span data-stu-id="63e19-132">Getting Started</span></span>

<span data-ttu-id="63e19-133">Spusťte aplikaci Visual Web Developer 2010 Express ("Visual Web Developer" pro krátkou verzi) a na **úvodní** stránce vyberte **Nový projekt** .</span><span class="sxs-lookup"><span data-stu-id="63e19-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="63e19-134">Visual Web Developer je integrované vývojové prostředí (IDE).</span><span class="sxs-lookup"><span data-stu-id="63e19-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="63e19-135">Stejně jako při psaní dokumentů v aplikaci Microsoft Word použijete k vytvoření aplikací rozhraní IDE.</span><span class="sxs-lookup"><span data-stu-id="63e19-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="63e19-136">V aplikaci Visual Web Developer je v horní části zobrazen panel nástrojů s různými možnostmi, které jsou vám k dispozici.</span><span class="sxs-lookup"><span data-stu-id="63e19-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="63e19-137">K dispozici je také nabídka, která poskytuje další způsob, jak provádět úlohy v integrovaném vývojovém prostředí.</span><span class="sxs-lookup"><span data-stu-id="63e19-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="63e19-138">(Například namísto výběru **nového projektu** na **úvodní** stránce můžete použít nabídku a vybrat **soubor** &gt; **Nový projekt**.)</span><span class="sxs-lookup"><span data-stu-id="63e19-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="63e19-139">Vytvoření první aplikace</span><span class="sxs-lookup"><span data-stu-id="63e19-139">Creating Your First Application</span></span>

<span data-ttu-id="63e19-140">Můžete vytvářet aplikace pomocí Visual Basic nebo vizuálu C# jako programovací jazyk.</span><span class="sxs-lookup"><span data-stu-id="63e19-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="63e19-141">Vyberte vizuál C# na levé straně a pak vyberte **webovou aplikaci ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="63e19-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="63e19-142">Pojmenujte projekt "MvcMovie" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="63e19-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="63e19-143">(Pokud dáváte přednost Visual Basic, přepněte se na [Visual Basic verzi](../vb/intro-to-aspnet-mvc-3.md) tohoto kurzu.)</span><span class="sxs-lookup"><span data-stu-id="63e19-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="63e19-144">V dialogovém okně **Nový projekt ASP.NET MVC 3** vyberte možnost **Internetová aplikace**.</span><span class="sxs-lookup"><span data-stu-id="63e19-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="63e19-145">Zkontrolujte **použití značek HTML5** a ponechte **Razor** jako výchozí modul zobrazení.</span><span class="sxs-lookup"><span data-stu-id="63e19-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="63e19-146">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="63e19-146">Click **OK**.</span></span> <span data-ttu-id="63e19-147">Visual Web Developer použil výchozí šablonu pro projekt ASP.NET MVC, který jste právě vytvořili, takže teď máte funkční aplikaci, aniž by bylo potřeba cokoli dělat!</span><span class="sxs-lookup"><span data-stu-id="63e19-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="63e19-148">Toto je jednoduché "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="63e19-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="63e19-149">a je to vhodné místo pro spuštění vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="63e19-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="63e19-150">V nabídce **ladění** vyberte **Spustit ladění**.</span><span class="sxs-lookup"><span data-stu-id="63e19-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="63e19-151">Všimněte si, že klávesová zkratka pro spuštění ladění je F5.</span><span class="sxs-lookup"><span data-stu-id="63e19-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="63e19-152">F5 způsobí, že Visual Web Developer spustí vývojový webový server a spustí webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="63e19-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="63e19-153">Visual Web Developer potom spustí prohlížeč a otevře domovskou stránku aplikace.</span><span class="sxs-lookup"><span data-stu-id="63e19-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="63e19-154">Všimněte si, že adresní řádek prohlížeče uvádí `localhost` a ne něco jako `example.com`.</span><span class="sxs-lookup"><span data-stu-id="63e19-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="63e19-155">To je proto, že `localhost` vždy odkazuje na vlastní místní počítač, v tomto případě je spuštěná aplikace, kterou jste právě sestavili.</span><span class="sxs-lookup"><span data-stu-id="63e19-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="63e19-156">Když Visual Web Developer spustí webový projekt, pro webový server se použije náhodný port.</span><span class="sxs-lookup"><span data-stu-id="63e19-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="63e19-157">Na následujícím obrázku je číslo náhodného portu 43246.</span><span class="sxs-lookup"><span data-stu-id="63e19-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="63e19-158">Při spuštění aplikace se pravděpodobně zobrazí jiné číslo portu.</span><span class="sxs-lookup"><span data-stu-id="63e19-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="63e19-159">Přímo z tohoto pole vám tato výchozí šablona nabídne dvě stránky, které můžete navštívit, a základní přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="63e19-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="63e19-160">Dalším krokem je změna fungování této aplikace a další informace o ASP.NET MVC v procesu.</span><span class="sxs-lookup"><span data-stu-id="63e19-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="63e19-161">Zavřete prohlížeč a Pojďme změnit nějaký kód.</span><span class="sxs-lookup"><span data-stu-id="63e19-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="63e19-162">Next</span><span class="sxs-lookup"><span data-stu-id="63e19-162">Next</span></span>](adding-a-controller.md)
