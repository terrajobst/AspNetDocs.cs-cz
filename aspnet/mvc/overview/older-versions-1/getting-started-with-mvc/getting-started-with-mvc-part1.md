---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: Úvod do ASP.NET MVC | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581583"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="61f8a-104">Úvod do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="61f8a-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="61f8a-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="61f8a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="61f8a-106">Aktualizovaná verze, pokud je tento kurz k dispozici [zde](../../getting-started/introduction/getting-started.md) , pomocí [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span><span class="sxs-lookup"><span data-stu-id="61f8a-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="61f8a-107">Nový kurz používá ASP.NET MVC 5, který poskytuje mnoho vylepšení v rámci tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="61f8a-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="61f8a-108">Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="61f8a-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="61f8a-109">Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.</span><span class="sxs-lookup"><span data-stu-id="61f8a-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="61f8a-110">Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="61f8a-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="61f8a-111">Pojďme udělat naši první webovou aplikaci v ASP.NET MVC s použitím [aplikace Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span><span class="sxs-lookup"><span data-stu-id="61f8a-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="61f8a-112">Vytvoříme trochu aplikaci seznamu filmů, která nám umožní vytvořit a vypsat filmy.</span><span class="sxs-lookup"><span data-stu-id="61f8a-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="61f8a-113">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="61f8a-113">What You'll Build</span></span>

<span data-ttu-id="61f8a-114">Tady jsou dva snímky obrazovky aplikace, kterou vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="61f8a-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="61f8a-115">Budete mít jednoduchou tabulku filmů s různými sloupci.</span><span class="sxs-lookup"><span data-stu-id="61f8a-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="61f8a-116">[Seznam filmů ![– Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="61f8a-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="61f8a-117">A budete mít formulář pro vytvoření, abychom mohli do seznamu přidat filmy.</span><span class="sxs-lookup"><span data-stu-id="61f8a-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="61f8a-118">[![vytvoření videa – Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="61f8a-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="61f8a-119">Dovednosti, se kterými se naučíte</span><span class="sxs-lookup"><span data-stu-id="61f8a-119">Skills You'll Learn</span></span>

<span data-ttu-id="61f8a-120">V tomto kurzu se naučíte základy vytvoření webové aplikace ASP.NET MVC pomocí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61f8a-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="61f8a-121">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="61f8a-121">You'll learn:</span></span>

- <span data-ttu-id="61f8a-122">Vytvoření nového projektu ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="61f8a-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="61f8a-123">Vytvoření nové databáze pomocí SQL Server</span><span class="sxs-lookup"><span data-stu-id="61f8a-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="61f8a-124">Vytvoření řadičů a zobrazení ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="61f8a-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="61f8a-125">Jak načíst a zobrazit data</span><span class="sxs-lookup"><span data-stu-id="61f8a-125">How to retrieve and display data</span></span>
- <span data-ttu-id="61f8a-126">Jak upravit data a povolit ověřování dat</span><span class="sxs-lookup"><span data-stu-id="61f8a-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="61f8a-127">Postup aktualizace schématu databáze</span><span class="sxs-lookup"><span data-stu-id="61f8a-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="61f8a-128">Začínáme</span><span class="sxs-lookup"><span data-stu-id="61f8a-128">Get Started</span></span>

<span data-ttu-id="61f8a-129">Začněte spuštěním aplikace Visual Web Developer 2010 Express (nahlaste ji "souboru vwd" od této chvíle) a na úvodní obrazovce vyberte nový projekt.</span><span class="sxs-lookup"><span data-stu-id="61f8a-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="61f8a-130">Visual Web Developer je integrované vývojové prostředí (IDE).</span><span class="sxs-lookup"><span data-stu-id="61f8a-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="61f8a-131">Stejně jako při psaní dokumentů v aplikaci Microsoft Word použijete k vytvoření aplikací rozhraní IDE.</span><span class="sxs-lookup"><span data-stu-id="61f8a-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="61f8a-132">V horní části je panel nástrojů s různými možnostmi, které jsou vám k dispozici, a také v nabídce, kterou byste mohli použít k výběru souboru | Nový projekt.</span><span class="sxs-lookup"><span data-stu-id="61f8a-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="61f8a-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="61f8a-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="61f8a-134">Vytvoření první aplikace</span><span class="sxs-lookup"><span data-stu-id="61f8a-134">Creating Your First Application</span></span>

<span data-ttu-id="61f8a-135">Můžete vytvářet aplikace pomocí Visual Basic nebo vizuálu C#.</span><span class="sxs-lookup"><span data-stu-id="61f8a-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="61f8a-136">Prozatím na levé straně C# vyberte vizuál a pak vyberte webová aplikace ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="61f8a-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="61f8a-137">Pojmenujte svůj projekt "filmy" a klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="61f8a-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="61f8a-138">[![nový projekt](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="61f8a-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="61f8a-139">Na pravé straně je Průzkumník řešení, kde se zobrazují všechny soubory a složky v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="61f8a-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="61f8a-140">Velké okno uprostřed je místo, kde upravujete kód a strávíte nejvíce času.</span><span class="sxs-lookup"><span data-stu-id="61f8a-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="61f8a-141">Aplikace Visual Studio použila pro projekt ASP.NET MVC, který jste právě vytvořili, výchozí šablonu, takže teď máte funkční aplikaci, aniž byste museli cokoli dělat!</span><span class="sxs-lookup"><span data-stu-id="61f8a-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="61f8a-142">Toto je jednoduché "Hello World!</span><span class="sxs-lookup"><span data-stu-id="61f8a-142">This is a simple "Hello World!</span></span> <span data-ttu-id="61f8a-143">projekt a je dobrým místem, kde se má aplikace spouštět.</span><span class="sxs-lookup"><span data-stu-id="61f8a-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="61f8a-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="61f8a-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="61f8a-145">Na panelu nástrojů vyberte tlačítko Přehrát.</span><span class="sxs-lookup"><span data-stu-id="61f8a-145">Select the "play" button to the toolbar.</span></span>

![Spustit ladění](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="61f8a-147">Jedná se o zelenou šipku ukazující vpravo, která zkompiluje váš program a spustí aplikaci ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="61f8a-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="61f8a-148">*Poznámka: místo toho můžete stisknout klávesu F5 na klávesnici nebo vybrat ladění&gt;spustit ladění z nabídky ladění.*</span><span class="sxs-lookup"><span data-stu-id="61f8a-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="61f8a-149">Tím dojde k tomu, že Visual Web Developer spustí vývoj webového serveru a spustí naši webovou aplikaci (k povolení tohoto postupu není nutná žádná konfigurace nebo ruční kroky).</span><span class="sxs-lookup"><span data-stu-id="61f8a-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="61f8a-150">Pak spustí prohlížeč a nakonfiguruje ho pro procházení domovské stránky aplikace.</span><span class="sxs-lookup"><span data-stu-id="61f8a-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="61f8a-151">Všimněte si, že adresní řádek prohlížeče říká "localhost", a ne něco jako example.com.</span><span class="sxs-lookup"><span data-stu-id="61f8a-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="61f8a-152">To je způsobeno tím, že localhost vždy odkazuje na vlastní místní počítač – v tomto případě je spuštěna aplikace, kterou jsme právě vytvořili.</span><span class="sxs-lookup"><span data-stu-id="61f8a-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="61f8a-153">[![domovskou stránku](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="61f8a-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="61f8a-154">Tato výchozí šablona vám umožní přejít na dvě stránky a základní přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="61f8a-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="61f8a-155">Pojďme změnit, jak tato aplikace funguje, a v procesu ASP.NET MVC se dozvíte trochu.</span><span class="sxs-lookup"><span data-stu-id="61f8a-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="61f8a-156">Zavřete prohlížeč a můžete změnit nějaký kód.</span><span class="sxs-lookup"><span data-stu-id="61f8a-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="61f8a-157">Next</span><span class="sxs-lookup"><span data-stu-id="61f8a-157">Next</span></span>](getting-started-with-mvc-part2.md)
