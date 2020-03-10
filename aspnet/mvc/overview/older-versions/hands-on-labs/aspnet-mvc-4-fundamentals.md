---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 – základy | Microsoft Docs
author: rick-anderson
description: Tato praktická cvičení vychází z hudebního úložiště MVC (Model View Controller), aplikace kurz, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MV...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598817"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="4168b-103">ASP.NET MVC 4 – základy</span><span class="sxs-lookup"><span data-stu-id="4168b-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="4168b-104">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="4168b-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="4168b-105">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="4168b-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="4168b-106">Tato praktická cvičení vychází z hudebního úložiště MVC (Model View Controller), aplikace kurz, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="4168b-107">V průběhu tohoto testovacího prostředí se naučíte jednoduchost, ale budete tyto technologie používat dohromady.</span><span class="sxs-lookup"><span data-stu-id="4168b-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="4168b-108">Začnete s jednoduchou aplikací a budete ji sestavovat, dokud nebudete mít plně funkční webovou aplikaci ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="4168b-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="4168b-109">Toto testovací prostředí spolupracuje s ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="4168b-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="4168b-110">Pokud chcete prozkoumat verzi ASP.NET MVC 3 v aplikaci kurz, najdete ji v [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="4168b-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="4168b-111">Tato praktická cvičení předpokládá, že má vývojář zkušenosti s technologiemi webového vývoje, jako je HTML a JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4168b-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="4168b-112">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="4168b-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="4168b-113">Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NET MVC 4 – základy](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span><span class="sxs-lookup"><span data-stu-id="4168b-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="4168b-114">Aplikace pro hudební úložiště</span><span class="sxs-lookup"><span data-stu-id="4168b-114">The Music Store application</span></span>

<span data-ttu-id="4168b-115">Webová aplikace pro hudební úložiště, která bude sestavená v rámci tohoto testovacího prostředí, zahrnuje tři hlavní části: nákupy, rezervace a správa.</span><span class="sxs-lookup"><span data-stu-id="4168b-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="4168b-116">Návštěvníci budou moci procházet alba podle žánru, přidávat alba do svého košíku, kontrolovat jejich výběr a nakonec pokračovat v rezervaci a dokončit objednávku.</span><span class="sxs-lookup"><span data-stu-id="4168b-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="4168b-117">Kromě toho Správci úložiště budou moct spravovat dostupná alba i hlavní vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="4168b-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="4168b-118">![Obrazovky pro hudební úložiště](aspnet-mvc-4-fundamentals/_static/image1.png "Obrazovky pro hudební úložiště")</span><span class="sxs-lookup"><span data-stu-id="4168b-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="4168b-119">*Obrazovky pro hudební úložiště*</span><span class="sxs-lookup"><span data-stu-id="4168b-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="4168b-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="4168b-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="4168b-121">Aplikace pro hudební úložiště bude sestavena pomocí **kontroleru zobrazení modelu (MVC)** , což je model architektury, který odděluje aplikaci do tří hlavních součástí:</span><span class="sxs-lookup"><span data-stu-id="4168b-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="4168b-122">**Modely**: objekty modelu jsou části aplikace, které implementují logiku domény.</span><span class="sxs-lookup"><span data-stu-id="4168b-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="4168b-123">Objekty modelu často také načítají a ukládají stav modelu v databázi.</span><span class="sxs-lookup"><span data-stu-id="4168b-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="4168b-124">**Zobrazení:** Zobrazení jsou komponenty, které zobrazují uživatelské rozhraní (UI) aplikace.</span><span class="sxs-lookup"><span data-stu-id="4168b-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="4168b-125">Toto uživatelské rozhraní je zpravidla vytvořeno na základě dat modelu.</span><span class="sxs-lookup"><span data-stu-id="4168b-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="4168b-126">Příkladem může být zobrazení pro úpravy alb, která zobrazují textová pole a rozevírací seznam na základě aktuálního stavu objektu alba.</span><span class="sxs-lookup"><span data-stu-id="4168b-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="4168b-127">**Řadiče:** Řadiče jsou komponenty, které zpracovávají interakci uživatele, manipulují s modelem a nakonec vyberou zobrazení pro vykreslení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="4168b-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="4168b-128">V aplikaci MVC zobrazení pouze zobrazuje informace, zatímco kontroler zpracovává vstup uživatele a interakci s uživatelem a reaguje na ně.</span><span class="sxs-lookup"><span data-stu-id="4168b-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="4168b-129">Vzor MVC vám pomůže vytvářet aplikace, které oddělují různé aspekty aplikace (vstupní logiku, obchodní logika a logika uživatelského rozhraní), a současně poskytuje volné spojení mezi těmito prvky.</span><span class="sxs-lookup"><span data-stu-id="4168b-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="4168b-130">Toto oddělení vám pomůže se správou složitosti při sestavování aplikace, protože umožňuje soustředit se na jeden aspekt implementace v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="4168b-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="4168b-131">Kromě toho vzor MVC usnadňuje testování aplikací a také podporuje používání služby TDD (test-řízeného vývoje) pro vytváření aplikací.</span><span class="sxs-lookup"><span data-stu-id="4168b-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="4168b-132">Rozhraní **ASP.NET MVC** nabízí alternativu ke vzorům webových formulářů ASP.NET pro vytváření webových aplikací založených na ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="4168b-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="4168b-133">Rozhraní **ASP.NET MVC** je odlehčené, vysoce testovatelné prezentační rozhraní, které (stejně jako u webových aplikací) je integrované s existujícími funkcemi ASP.NET, jako jsou stránky předlohy a ověřování založené na členství, takže získáte všechny možnosti základního rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4168b-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="4168b-134">To je užitečné, pokud jste již obeznámeni s webovými formuláři ASP.NET, protože všechny knihovny, které už používáte, jsou k dispozici také v ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="4168b-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="4168b-135">Kromě toho volné spojení mezi třemi hlavními komponentami aplikace MVC podporuje také paralelní vývoj.</span><span class="sxs-lookup"><span data-stu-id="4168b-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="4168b-136">Například jeden vývojář může pracovat na zobrazení, druhý vývojář může pracovat s logikou kontroleru a třetí vývojář se může soustředit na obchodní logiku v modelu.</span><span class="sxs-lookup"><span data-stu-id="4168b-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="4168b-137">Cíle</span><span class="sxs-lookup"><span data-stu-id="4168b-137">Objectives</span></span>

<span data-ttu-id="4168b-138">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="4168b-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="4168b-139">Vytvoření aplikace ASP.NET MVC od začátku na základě kurzu aplikace pro hudební úložiště</span><span class="sxs-lookup"><span data-stu-id="4168b-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="4168b-140">Přidání řadičů pro zpracování adres URL na domovské stránce webu a procházení hlavních funkcí</span><span class="sxs-lookup"><span data-stu-id="4168b-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="4168b-141">Přidání zobrazení pro přizpůsobení obsahu zobrazeného spolu s jeho stylem</span><span class="sxs-lookup"><span data-stu-id="4168b-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="4168b-142">Přidání tříd modelu do zahrnutí a správy dat a logiky domény</span><span class="sxs-lookup"><span data-stu-id="4168b-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="4168b-143">Použití vzoru modelu zobrazení k předávání informací z akcí kontroleru do šablon zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="4168b-144">Prozkoumejte novou šablonu ASP.NET MVC 4 pro internetové aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="4168b-145">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="4168b-145">Prerequisites</span></span>

<span data-ttu-id="4168b-146">K dokončení tohoto testovacího prostředí musíte mít následující položky:</span><span class="sxs-lookup"><span data-stu-id="4168b-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="4168b-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (pokyny k jeho instalaci najdete v [příloze A](#AppendixA) )</span><span class="sxs-lookup"><span data-stu-id="4168b-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="4168b-148">Nastavení</span><span class="sxs-lookup"><span data-stu-id="4168b-148">Setup</span></span>

<span data-ttu-id="4168b-149">**Instalace fragmentů kódu**</span><span class="sxs-lookup"><span data-stu-id="4168b-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="4168b-150">Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="4168b-151">Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .</span><span class="sxs-lookup"><span data-stu-id="4168b-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="4168b-152">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze C: použití fragmentů kódu](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="4168b-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="4168b-153">Cvičení</span><span class="sxs-lookup"><span data-stu-id="4168b-153">Exercises</span></span>

<span data-ttu-id="4168b-154">Tato praktická cvičení se skládají z následujících cvičení:</span><span class="sxs-lookup"><span data-stu-id="4168b-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="4168b-155">Cvičení 1: vytvoření projektu webové aplikace MusicStore ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4168b-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="4168b-156">Cvičení 2: vytvoření kontroleru</span><span class="sxs-lookup"><span data-stu-id="4168b-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="4168b-157">Cvičení 3: předávání parametrů řadiči</span><span class="sxs-lookup"><span data-stu-id="4168b-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="4168b-158">Cvičení 4: Vytvoření zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="4168b-159">Cvičení 5: vytvoření modelu zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="4168b-160">Cvičení 6: použití parametrů v zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="4168b-161">Cvičení 7: zaASP.NETm s novou šablonou MVC 4</span><span class="sxs-lookup"><span data-stu-id="4168b-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="4168b-162">Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="4168b-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="4168b-163">Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="4168b-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="4168b-164">Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.</span><span class="sxs-lookup"><span data-stu-id="4168b-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="4168b-165">Cvičení 1: vytvoření projektu webové aplikace MusicStore ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4168b-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="4168b-166">V tomto cvičení se naučíte, jak vytvořit aplikaci ASP.NET MVC v aplikaci Visual Studio 2012 Express for Web i v její hlavní organizaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="4168b-167">Kromě toho se dozvíte, jak přidat nový kontroler a nastavit jeho zobrazení na domovské stránce aplikace jednoduchý řetězec.</span><span class="sxs-lookup"><span data-stu-id="4168b-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="4168b-168">Úloha 1 – Vytvoření projektu webové aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4168b-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="4168b-169">V této úloze vytvoříte prázdný projekt aplikace ASP.NET MVC pomocí šablony MVC sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="4168b-170">Spusťte **vs Express for Web**.</span><span class="sxs-lookup"><span data-stu-id="4168b-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="4168b-171">V nabídce **soubor** klikněte na příkaz **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="4168b-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="4168b-172">V dialogovém okně **Nový projekt** vyberte typ projektu **webové aplikace ASP.NET MVC 4** , který je umístěn v **části C#vizuál,** seznam **webových** šablon.</span><span class="sxs-lookup"><span data-stu-id="4168b-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="4168b-173">Změňte **název** na *MvcMusicStore*.</span><span class="sxs-lookup"><span data-stu-id="4168b-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="4168b-174">Nastavte umístění řešení v rámci nové **počáteční** složky ve zdrojové složce cvičení, například **[vaše-hol-Path] \Source\Ex01-CreatingMusicStoreProject\Begin**.</span><span class="sxs-lookup"><span data-stu-id="4168b-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="4168b-175">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="4168b-175">Click **OK**.</span></span>

    <span data-ttu-id="4168b-176">![Vytvoření nového projektu – dialogové okno](aspnet-mvc-4-fundamentals/_static/image2.png "Vytvoření nového projektu – dialogové okno")</span><span class="sxs-lookup"><span data-stu-id="4168b-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="4168b-177">*Vytvoření nového projektu – dialogové okno*</span><span class="sxs-lookup"><span data-stu-id="4168b-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="4168b-178">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu **Basic** a ujistěte se, že vybraný **zobrazovací modul** je **Razor**.</span><span class="sxs-lookup"><span data-stu-id="4168b-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="4168b-179">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="4168b-179">Click **OK**.</span></span>

    <span data-ttu-id="4168b-180">![Nový projekt ASP.NET MVC 4 – dialogové okno](aspnet-mvc-4-fundamentals/_static/image3.png "Nový projekt ASP.NET MVC 4 – dialogové okno")</span><span class="sxs-lookup"><span data-stu-id="4168b-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="4168b-181">*Nový projekt ASP.NET MVC 4 – dialogové okno*</span><span class="sxs-lookup"><span data-stu-id="4168b-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="4168b-182">Úloha 2 – zkoumání struktury řešení</span><span class="sxs-lookup"><span data-stu-id="4168b-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="4168b-183">Rozhraní ASP.NET MVC obsahuje šablonu projektu sady Visual Studio, která vám pomůže vytvořit webové aplikace podporující vzor MVC.</span><span class="sxs-lookup"><span data-stu-id="4168b-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="4168b-184">Tato šablona vytvoří novou webovou aplikaci ASP.NET MVC s požadovanými složkami, šablonami položek a položkami konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="4168b-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="4168b-185">V této úloze provedete kontrolu struktury řešení, abyste pochopili prvky, které jsou součástí a jejich vztahy.</span><span class="sxs-lookup"><span data-stu-id="4168b-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="4168b-186">Následující složky jsou zahrnuté ve všech aplikacích ASP.NET MVC, protože rozhraní ASP.NET MVC ve výchozím nastavení používá ke konfiguraci&quot; přístup &quot;konvenci a vytváří některé výchozí předpoklady na základě zásad vytváření názvů složek.</span><span class="sxs-lookup"><span data-stu-id="4168b-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="4168b-187">Po vytvoření projektu zkontrolujte strukturu složek, která byla vytvořena v Průzkumník řešení na pravé straně:</span><span class="sxs-lookup"><span data-stu-id="4168b-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="4168b-188">![Struktura složek ASP.NET MVC v Průzkumník řešení](aspnet-mvc-4-fundamentals/_static/image4.png "Struktura složek ASP.NET MVC v Průzkumník řešení")</span><span class="sxs-lookup"><span data-stu-id="4168b-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="4168b-189">*Struktura složek ASP.NET MVC v Průzkumník řešení*</span><span class="sxs-lookup"><span data-stu-id="4168b-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="4168b-190">**Řadiče**.</span><span class="sxs-lookup"><span data-stu-id="4168b-190">**Controllers**.</span></span> <span data-ttu-id="4168b-191">Tato složka bude obsahovat třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="4168b-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="4168b-192">V aplikaci založené na MVC jsou řadiče zodpovědné za zpracování interakce koncového uživatele, manipulace s modelem a nakonec výběr zobrazení pro vykreslení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="4168b-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="4168b-193">Rozhraní MVC vyžaduje, aby názvy všech řadičů byly ukončeny řadičem &quot;&quot;-například HomeController, LoginController nebo ProductController.</span><span class="sxs-lookup"><span data-stu-id="4168b-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="4168b-194">**Modely**.</span><span class="sxs-lookup"><span data-stu-id="4168b-194">**Models**.</span></span> <span data-ttu-id="4168b-195">Tato složka je poskytována pro třídy, které reprezentují aplikační model pro webovou aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="4168b-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="4168b-196">To obvykle zahrnuje kód, který definuje objekty a logiku pro interakci s úložištěm dat.</span><span class="sxs-lookup"><span data-stu-id="4168b-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="4168b-197">Skutečné objekty modelu obvykle budou v samostatných knihovnách tříd.</span><span class="sxs-lookup"><span data-stu-id="4168b-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="4168b-198">Při vytváření nové aplikace ale můžete zahrnout třídy a pak je přesunout do samostatných knihoven tříd později v rámci vývojového cyklu.</span><span class="sxs-lookup"><span data-stu-id="4168b-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="4168b-199">**Zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-199">**Views**.</span></span> <span data-ttu-id="4168b-200">Tato složka je doporučené umístění pro zobrazení, součásti zodpovědné za zobrazení uživatelského rozhraní aplikace.</span><span class="sxs-lookup"><span data-stu-id="4168b-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="4168b-201">Zobrazení používají soubory. aspx,. ascx,. cshtml a. Master, kromě všech dalších souborů, které se vztahují k vykreslování zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="4168b-202">Složka zobrazení obsahuje složku pro každý kontroler; Složka má název s předponou názvu kontroleru.</span><span class="sxs-lookup"><span data-stu-id="4168b-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="4168b-203">Například pokud máte řadič s názvem **HomeController**, složka zobrazení bude obsahovat složku s názvem Home.</span><span class="sxs-lookup"><span data-stu-id="4168b-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="4168b-204">Ve výchozím nastavení, když rozhraní ASP.NET MVC načte zobrazení, vyhledá soubor. aspx s požadovaným názvem zobrazení ve složce Views\controllerName (**zobrazení [kontrolér] [Action]. aspx**) nebo (**zobrazení [kontrolér] [Action]. cshtml**) pro zobrazení Razor.</span><span class="sxs-lookup"><span data-stu-id="4168b-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4168b-205">Kromě dříve uvedených složek používá webová aplikace MVC soubor **Global. asax** k nastavení výchozích nastavení směrování adres URL a používá soubor **Web. config** ke konfiguraci aplikace.</span><span class="sxs-lookup"><span data-stu-id="4168b-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="4168b-206">Úloha 3 – přidání HomeController</span><span class="sxs-lookup"><span data-stu-id="4168b-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="4168b-207">V aplikacích ASP.NET, které nepoužívají architekturu MVC, je interakce uživatele uspořádána kolem stránek a kolem vyvolání a zpracování událostí z těchto stránek.</span><span class="sxs-lookup"><span data-stu-id="4168b-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="4168b-208">Naproti tomu interakce uživatele s aplikacemi ASP.NET MVC je uspořádaná kolem řadičů a jejich metod jejich akcí.</span><span class="sxs-lookup"><span data-stu-id="4168b-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="4168b-209">Na druhé straně rozhraní ASP.NET MVC mapuje adresy URL na třídy, které jsou označovány jako řadiče.</span><span class="sxs-lookup"><span data-stu-id="4168b-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="4168b-210">Řadiče zpracovávají příchozí požadavky, zpracovávají uživatelský vstup a interakce, spouštějí příslušnou logiku aplikace a určí odpověď pro odeslání zpátky klientovi (zobrazení HTML, stažení souboru, přesměrování na jinou adresu URL atd.).</span><span class="sxs-lookup"><span data-stu-id="4168b-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="4168b-211">V případě zobrazení HTML třída kontroleru obvykle volá samostatnou součást zobrazení, která generuje kód HTML pro požadavek.</span><span class="sxs-lookup"><span data-stu-id="4168b-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="4168b-212">V aplikaci MVC zobrazení pouze zobrazuje informace, zatímco kontroler zpracovává vstup uživatele a interakci s uživatelem a reaguje na ně.</span><span class="sxs-lookup"><span data-stu-id="4168b-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="4168b-213">V této úloze přidáte třídu kontroléru, která bude zpracovávat adresy URL na domovské stránce webu hudebního úložiště.</span><span class="sxs-lookup"><span data-stu-id="4168b-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="4168b-214">V Průzkumník řešení klikněte pravým tlačítkem na složku **řadiče** , vyberte **Přidat** a pak příkaz **kontroleru** :</span><span class="sxs-lookup"><span data-stu-id="4168b-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="4168b-215">![Přidat kontroler – příkaz](aspnet-mvc-4-fundamentals/_static/image5.png "Přidat kontroler – příkaz")</span><span class="sxs-lookup"><span data-stu-id="4168b-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="4168b-216">*Přidat kontroler – příkaz*</span><span class="sxs-lookup"><span data-stu-id="4168b-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="4168b-217">Zobrazí se dialogové okno **Přidat řadič** .</span><span class="sxs-lookup"><span data-stu-id="4168b-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="4168b-218">Pojmenujte kontrolér *HomeController* a stiskněte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="4168b-219">![Dialogové okno Přidat řadič](aspnet-mvc-4-fundamentals/_static/image6.png "Dialogové okno Přidat řadič")</span><span class="sxs-lookup"><span data-stu-id="4168b-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="4168b-220">*Dialogové okno Přidat řadič*</span><span class="sxs-lookup"><span data-stu-id="4168b-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="4168b-221">Soubor **HomeController.cs** se vytvoří ve složce **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="4168b-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="4168b-222">Aby **HomeController** vrátil řetězec na jeho akci index, nahraďte metodu **indexu** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="4168b-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="4168b-223">(Fragment kódu – *základy ASP.NET MVC 4 – EX1 HomeController index*)</span><span class="sxs-lookup"><span data-stu-id="4168b-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="4168b-224">Úloha 4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="4168b-225">V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="4168b-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="4168b-226">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="4168b-227">Projekt je zkompilován a spustí se místní webový server služby IIS.</span><span class="sxs-lookup"><span data-stu-id="4168b-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="4168b-228">Místní webový server služby IIS bude automaticky otevřít webový prohlížeč, který odkazuje na adresu URL webového serveru.</span><span class="sxs-lookup"><span data-stu-id="4168b-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="4168b-229">![Aplikace spuštěná ve webovém prohlížeči](aspnet-mvc-4-fundamentals/_static/image7.png "Aplikace spuštěná ve webovém prohlížeči")</span><span class="sxs-lookup"><span data-stu-id="4168b-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="4168b-230">*Aplikace spuštěná ve webovém prohlížeči*</span><span class="sxs-lookup"><span data-stu-id="4168b-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-231">Místní webový server služby IIS spustí web na náhodném bezplatném čísle portu.</span><span class="sxs-lookup"><span data-stu-id="4168b-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="4168b-232">Na obrázku výše je web spuštěný v `http://localhost:50103/`, takže se používá port 50103.</span><span class="sxs-lookup"><span data-stu-id="4168b-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="4168b-233">Vaše číslo portu se může lišit.</span><span class="sxs-lookup"><span data-stu-id="4168b-233">Your port number may vary.</span></span>
2. <span data-ttu-id="4168b-234">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="4168b-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="4168b-235">Cvičení 2: vytvoření kontroleru</span><span class="sxs-lookup"><span data-stu-id="4168b-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="4168b-236">V tomto cvičení se dozvíte, jak aktualizovat kontroler pro implementaci jednoduchých funkcí aplikace pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="4168b-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="4168b-237">Tento kontroler definuje metody akcí pro zpracování všech následujících specifických požadavků:</span><span class="sxs-lookup"><span data-stu-id="4168b-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="4168b-238">Stránka se seznamem hudebních žánrů v obchodě s hudbou</span><span class="sxs-lookup"><span data-stu-id="4168b-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="4168b-239">Stránka pro procházení, na které jsou uvedena všechna hudební alba pro určitý Žánr</span><span class="sxs-lookup"><span data-stu-id="4168b-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="4168b-240">Stránka s podrobnostmi, která zobrazuje informace o konkrétním hudebním albu</span><span class="sxs-lookup"><span data-stu-id="4168b-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="4168b-241">V rozsahu tohoto cvičení budou tyto akce jednoduše vracet řetězec nyní.</span><span class="sxs-lookup"><span data-stu-id="4168b-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="4168b-242">Úloha 1 – Přidání nové třídy StoreController</span><span class="sxs-lookup"><span data-stu-id="4168b-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="4168b-243">V této úloze přidáte nový kontroler.</span><span class="sxs-lookup"><span data-stu-id="4168b-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="4168b-244">Pokud ještě není otevřený, spusťte **VS Express for Web 2012**.</span><span class="sxs-lookup"><span data-stu-id="4168b-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="4168b-245">V nabídce **soubor** klikněte na příkaz **Otevřít projekt**.</span><span class="sxs-lookup"><span data-stu-id="4168b-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="4168b-246">V dialogovém okně Otevřít projekt přejděte na **Source\Ex02-CreatingAController\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="4168b-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="4168b-247">Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="4168b-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="4168b-248">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="4168b-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4168b-249">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4168b-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4168b-250">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="4168b-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4168b-251">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4168b-252">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="4168b-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4168b-253">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="4168b-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4168b-254">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="4168b-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="4168b-255">Přidejte nový kontroler.</span><span class="sxs-lookup"><span data-stu-id="4168b-255">Add the new controller.</span></span> <span data-ttu-id="4168b-256">Provedete to tak, že kliknete pravým tlačítkem myši na složku **Controllers** v rámci Průzkumník řešení, vyberete **Přidat** a pak příkaz **Controller** .</span><span class="sxs-lookup"><span data-stu-id="4168b-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="4168b-257">Změňte **název kontroleru** na *StoreController*a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="4168b-258">![Dialogové okno Přidat řadič](aspnet-mvc-4-fundamentals/_static/image8.png "Dialogové okno Přidat řadič")</span><span class="sxs-lookup"><span data-stu-id="4168b-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="4168b-259">*Dialogové okno Přidat řadič*</span><span class="sxs-lookup"><span data-stu-id="4168b-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="4168b-260">Úloha 2 – Změna akcí StoreController</span><span class="sxs-lookup"><span data-stu-id="4168b-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="4168b-261">V této úloze upravíte metody kontroleru, které se nazývají **Akce**.</span><span class="sxs-lookup"><span data-stu-id="4168b-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="4168b-262">Akce zodpovídá za zpracování požadavků URL a určení obsahu, který se má poslat zpátky do prohlížeče nebo uživatele, který adresu URL vyvolal.</span><span class="sxs-lookup"><span data-stu-id="4168b-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="4168b-263">Třída **StoreController** již obsahuje metodu **indexu** .</span><span class="sxs-lookup"><span data-stu-id="4168b-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="4168b-264">Použijete ji později v tomto testovacím prostředí k implementaci stránky, která obsahuje všechny žánry hudebního obchodu.</span><span class="sxs-lookup"><span data-stu-id="4168b-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="4168b-265">Prozatím jednoduše nahraďte metodu **indexu** následujícím kódem, který vrátí řetězec &quot;Hello z Store. index ()&quot;:</span><span class="sxs-lookup"><span data-stu-id="4168b-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="4168b-266">(Fragment kódu – *základy ASP.NET MVC 4 – EX2 StoreController index*)</span><span class="sxs-lookup"><span data-stu-id="4168b-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="4168b-267">Přidejte metody **Browse** a **Details** .</span><span class="sxs-lookup"><span data-stu-id="4168b-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="4168b-268">Chcete-li to provést, přidejte do **StoreController**následující kód:</span><span class="sxs-lookup"><span data-stu-id="4168b-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="4168b-269">(Fragment kódu – *základy ASP.NET MVC 4 – EX2 StoreController BrowseAndDetails*)</span><span class="sxs-lookup"><span data-stu-id="4168b-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4168b-270">Úloha 3 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="4168b-271">V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="4168b-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="4168b-272">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4168b-273">Projekt se spustí na **domovské** stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="4168b-274">Změňte adresu URL pro ověření implementace jednotlivých akcí.</span><span class="sxs-lookup"><span data-stu-id="4168b-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="4168b-275">**/Store**.</span><span class="sxs-lookup"><span data-stu-id="4168b-275">**/Store**.</span></span> <span data-ttu-id="4168b-276">V **&quot;Store. index () se zobrazí&quot;Hello** .</span><span class="sxs-lookup"><span data-stu-id="4168b-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="4168b-277">**/Store/Browse**.</span><span class="sxs-lookup"><span data-stu-id="4168b-277">**/Store/Browse**.</span></span> <span data-ttu-id="4168b-278">Zobrazí se **&quot;Hello z Storu. Browse ()&quot;** .</span><span class="sxs-lookup"><span data-stu-id="4168b-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="4168b-279">**/Store/Details**.</span><span class="sxs-lookup"><span data-stu-id="4168b-279">**/Store/Details**.</span></span> <span data-ttu-id="4168b-280">V části Store se zobrazí **&quot;Hello. Details ()&quot;** .</span><span class="sxs-lookup"><span data-stu-id="4168b-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="4168b-281">![Procházení StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Procházení StoreBrowse")</span><span class="sxs-lookup"><span data-stu-id="4168b-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="4168b-282">*Procházení/Store/Browse*</span><span class="sxs-lookup"><span data-stu-id="4168b-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="4168b-283">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="4168b-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="4168b-284">Cvičení 3: předávání parametrů řadiči</span><span class="sxs-lookup"><span data-stu-id="4168b-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="4168b-285">Až do této chvíle jste vrátili konstantní řetězce z řadičů.</span><span class="sxs-lookup"><span data-stu-id="4168b-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="4168b-286">V tomto cvičení se dozvíte, jak předat parametry do kontroleru pomocí adresy URL a řetězce dotazu a potom provést akce metody, které reagují na text do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="4168b-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="4168b-287">Úloha 1 – Přidání parametru žánru do StoreController</span><span class="sxs-lookup"><span data-stu-id="4168b-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="4168b-288">V této úloze použijete dotaz **QueryString** k odeslání parametrů metodě akce **procházení** v **StoreController**.</span><span class="sxs-lookup"><span data-stu-id="4168b-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="4168b-289">Pokud ještě není otevřený, spusťte **vs Express for Web**.</span><span class="sxs-lookup"><span data-stu-id="4168b-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="4168b-290">V nabídce **soubor** klikněte na příkaz **Otevřít projekt**.</span><span class="sxs-lookup"><span data-stu-id="4168b-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="4168b-291">V dialogovém okně Otevřít projekt přejděte na **Source\Ex03-PassingParametersToAController\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="4168b-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="4168b-292">Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="4168b-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="4168b-293">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="4168b-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4168b-294">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4168b-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4168b-295">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="4168b-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4168b-296">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4168b-297">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="4168b-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4168b-298">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="4168b-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4168b-299">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="4168b-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="4168b-300">Otevřete třídu **StoreController** .</span><span class="sxs-lookup"><span data-stu-id="4168b-300">Open **StoreController** class.</span></span> <span data-ttu-id="4168b-301">Provedete to tak, že v **Průzkumník řešení**rozbalíte složku **Controllers (řadiče** ) a dvakrát kliknete na **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="4168b-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="4168b-302">Změňte metodu **procházení** a přidejte parametr řetězce pro požadavek na konkrétní Žánr.</span><span class="sxs-lookup"><span data-stu-id="4168b-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="4168b-303">ASP.NET MVC při vyvolání automaticky předáte všechny parametry dotazu nebo formuláře odeslání s názvem **Žánr** na tuto metodu Action.</span><span class="sxs-lookup"><span data-stu-id="4168b-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="4168b-304">Chcete-li to provést, nahraďte metodu **Browse** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="4168b-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="4168b-305">(Fragment kódu – *základy ASP.NET MVC 4 – EX3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="4168b-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="4168b-306">Používáte metodu nástroje **HttpUtility. HtmlEncode** , která uživatelům brání v vkládání JavaScriptu do zobrazení s odkazem jako **/Store/Browse? Žánr =&lt;okno skriptu&gt;Window. Location = '[http://hackersite.com](http://hackersite.com)'&lt;/Script&gt;** .</span><span class="sxs-lookup"><span data-stu-id="4168b-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="4168b-307">Další vysvětlení najdete v [tomto článku na webu MSDN](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span><span class="sxs-lookup"><span data-stu-id="4168b-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="4168b-308">Úloha 2 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="4168b-309">V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči a použijete parametr **žánru** .</span><span class="sxs-lookup"><span data-stu-id="4168b-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="4168b-310">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4168b-311">Projekt se spustí na **domovské** stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="4168b-312">Změňte adresu URL na */Store/Browse? Žánr = disco* pro ověření, že akce přijímá parametr žánru.</span><span class="sxs-lookup"><span data-stu-id="4168b-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="4168b-313">![Procházení StoreBrowseGenre = disco](aspnet-mvc-4-fundamentals/_static/image10.png "Procházení StoreBrowseGenre = disco")</span><span class="sxs-lookup"><span data-stu-id="4168b-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="4168b-314">*Prochází se/Store/Browse? Žánr = disco*</span><span class="sxs-lookup"><span data-stu-id="4168b-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="4168b-315">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="4168b-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="4168b-316">Úloha 3 – Přidání parametru ID vloženého v adrese URL</span><span class="sxs-lookup"><span data-stu-id="4168b-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="4168b-317">V této úloze použijete **adresu URL** k předání parametru **ID** metodě akce **Details** **StoreController**.</span><span class="sxs-lookup"><span data-stu-id="4168b-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="4168b-318">Výchozí konvence směrování ASP.NET MVC je zacházet s segmentem adresy URL za názvem metody akce jako s parametrem s názvem **ID**. Pokud vaše metoda Action má parametr s názvem ID, pak ASP.NET MVC automaticky předává segment adresy URL jako parametr.</span><span class="sxs-lookup"><span data-stu-id="4168b-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="4168b-319">V části **úložiště URL/podrobnosti/5**se **ID** bude interpretovat jako **5**.</span><span class="sxs-lookup"><span data-stu-id="4168b-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="4168b-320">Změňte metodu **Details** objektu **StoreController**přidáním parametru **int** s názvem **ID**. Chcete-li to provést, nahraďte metodu **Details** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="4168b-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="4168b-321">(Fragment kódu – *základy ASP.NET MVC 4 – EX3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="4168b-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="4168b-322">Úloha 4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="4168b-323">V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči a použijete parametr **ID** .</span><span class="sxs-lookup"><span data-stu-id="4168b-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="4168b-324">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4168b-325">Projekt se spustí na **domovské** stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="4168b-326">Změňte adresu URL na */Store/Details/5* a ověřte tak, že akce přijme parametr ID.</span><span class="sxs-lookup"><span data-stu-id="4168b-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="4168b-327">![Procházení StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Procházení StoreDetails5")</span><span class="sxs-lookup"><span data-stu-id="4168b-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="4168b-328">*Procházení/Store/Details/5*</span><span class="sxs-lookup"><span data-stu-id="4168b-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="4168b-329">Cvičení 4: Vytvoření zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="4168b-330">Zatím jste vrátili řetězce z akcí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="4168b-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="4168b-331">I když je to užitečný způsob, jak porozumět tomu, jak řadiče fungují, nezpůsobuje to, jak vaše skutečné webové aplikace sestavíte.</span><span class="sxs-lookup"><span data-stu-id="4168b-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="4168b-332">Zobrazení jsou komponenty, které poskytují lepší přístup k vygenerování kódu HTML zpátky do prohlížeče pomocí souborů šablon.</span><span class="sxs-lookup"><span data-stu-id="4168b-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="4168b-333">V tomto cvičení se dozvíte, jak přidat stránku předlohy rozložení, abyste mohli nastavit šablonu pro běžný obsah HTML, šablonu stylů pro vylepšení vzhledu a chování webu a nakonec šablony zobrazení, která umožňuje HomeController vrátit kód HTML.</span><span class="sxs-lookup"><span data-stu-id="4168b-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a><span data-ttu-id="4168b-334">Úloha 1 – Změna souboru \_layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="4168b-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="4168b-335">Soubor **~/Views/Shared/\_layout. cshtml** vám umožní nastavit šablonu pro Common HTML pro použití v celém webu.</span><span class="sxs-lookup"><span data-stu-id="4168b-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="4168b-336">V této úloze přidáte stránku předlohy rozložení se společným záhlavím s odkazy na domovskou stránku a oblast úložiště.</span><span class="sxs-lookup"><span data-stu-id="4168b-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="4168b-337">Pokud ještě není otevřený, spusťte **vs Express for Web**.</span><span class="sxs-lookup"><span data-stu-id="4168b-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="4168b-338">V nabídce **soubor** klikněte na příkaz **Otevřít projekt**.</span><span class="sxs-lookup"><span data-stu-id="4168b-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="4168b-339">V dialogovém okně Otevřít projekt přejděte na **Source\Ex04-CreatingAView\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="4168b-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="4168b-340">Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="4168b-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="4168b-341">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="4168b-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4168b-342">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4168b-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4168b-343">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="4168b-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4168b-344">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4168b-345">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="4168b-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4168b-346">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="4168b-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4168b-347">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="4168b-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="4168b-348">Soubor <strong>\_layout. cshtml</strong> obsahuje rozložení kontejneru HTML pro všechny stránky na webu.</span><span class="sxs-lookup"><span data-stu-id="4168b-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="4168b-349">Zahrnuje&lt;prvek <strong>&gt;HTML</strong> pro odpověď HTML a také <strong>&lt;&gt;</strong> a <strong>&lt;tělo&gt;</strong> prvků.</span><span class="sxs-lookup"><span data-stu-id="4168b-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="4168b-350"><strong>@RenderBody()</strong> v těle HTML identifikují oblasti, které zobrazují šablony, budou moci vyplnit dynamickým obsahem.</span><span class="sxs-lookup"><span data-stu-id="4168b-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="4168b-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="4168b-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="4168b-352">Přidejte společnou hlavičku s odkazy na domovskou stránku a oblast pro ukládání na všech stránkách v lokalitě.</span><span class="sxs-lookup"><span data-stu-id="4168b-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="4168b-353">Chcete-li to provést, přidejte následující kód &lt;tělo&gt; příkaz.</span><span class="sxs-lookup"><span data-stu-id="4168b-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="4168b-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="4168b-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="4168b-355">Zahrňte div pro vykreslení oddílu tělo každé stránky.</span><span class="sxs-lookup"><span data-stu-id="4168b-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="4168b-356">Nahraďte <strong>@RenderBody()</strong> následujícím zvýrazněným kódem: (C#)</span><span class="sxs-lookup"><span data-stu-id="4168b-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="4168b-357">Věděli jste, že?</span><span class="sxs-lookup"><span data-stu-id="4168b-357">Did you know?</span></span> <span data-ttu-id="4168b-358">Visual Studio 2012 obsahuje fragmenty kódu, které usnadňují přidávání běžně používaného kódu do HTML, souborů kódu a dalších.</span><span class="sxs-lookup"><span data-stu-id="4168b-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="4168b-359">Vyzkoušejte si to zadáním **&lt;div&gt;** a dvojím stisknutím klávesy **TAB** vložte úplnou značku **div** .</span><span class="sxs-lookup"><span data-stu-id="4168b-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="4168b-360">Úloha 2 – Přidání šablony stylů CSS</span><span class="sxs-lookup"><span data-stu-id="4168b-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="4168b-361">Prázdná šablona projektu obsahuje velmi zjednodušený soubor CSS, který obsahuje pouze styly používané k zobrazení základních formulářů a ověřovacích zpráv.</span><span class="sxs-lookup"><span data-stu-id="4168b-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="4168b-362">K vylepšení vzhledu a chování webu budete používat další šablony stylů CSS a obrázky (potenciálně poskytované návrhářem).</span><span class="sxs-lookup"><span data-stu-id="4168b-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="4168b-363">V této úloze přidáte šablonu stylů CSS, která definuje styly webu.</span><span class="sxs-lookup"><span data-stu-id="4168b-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="4168b-364">Do složky **Source\Assets\Content** v tomto testovacím prostředí se zahrnou i soubory CSS a obrázky.</span><span class="sxs-lookup"><span data-stu-id="4168b-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="4168b-365">Pokud je chcete přidat do aplikace, přetáhněte jejich obsah z okna **Průzkumníka Windows** do **Průzkumník řešení** v Visual Studio Express pro web, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="4168b-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="4168b-366">![Přetahování obsahu stylu](aspnet-mvc-4-fundamentals/_static/image12.png "Přetahování obsahu stylu")</span><span class="sxs-lookup"><span data-stu-id="4168b-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="4168b-367">*Přetahování obsahu stylu*</span><span class="sxs-lookup"><span data-stu-id="4168b-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="4168b-368">Zobrazí se dialogové okno s upozorněním, které požádá o potvrzení o nahrazení souboru **site. CSS** a některých existujících imagí.</span><span class="sxs-lookup"><span data-stu-id="4168b-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="4168b-369">Zaškrtněte políčko **použít pro všechny položky** a klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="4168b-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="4168b-370">Úloha 3 – Přidání šablony zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="4168b-371">V této úloze přidáte šablonu zobrazení, která vygeneruje odpověď HTML, která bude používat stránku předlohy rozložení a šablony stylů CSS přidané v tomto cvičení.</span><span class="sxs-lookup"><span data-stu-id="4168b-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="4168b-372">Chcete-li použít šablonu zobrazení při procházení domovské stránky webu, budete nejprve muset označit, že místo vrácení řetězce bude metoda **HomeController index** vracet **zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="4168b-373">Otevřete třídu **HomeController** a změňte její metodu **indexu** tak, aby vracela **ActionResult**a vrátila **zobrazení ()** .</span><span class="sxs-lookup"><span data-stu-id="4168b-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="4168b-374">(Fragment kódu – *základy ASP.NET MVC 4 – Ex4 HomeController index*)</span><span class="sxs-lookup"><span data-stu-id="4168b-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="4168b-375">Nyní je třeba přidat příslušnou šablonu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="4168b-376">Provedete to tak, že **kliknete pravým tlačítkem myši** do metody **index** Action a vyberete **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="4168b-377">Tím se zobrazí dialogové okno **Přidat zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="4168b-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="4168b-378">![Přidání zobrazení v rámci metody index](aspnet-mvc-4-fundamentals/_static/image13.png "Přidání zobrazení v rámci metody index")</span><span class="sxs-lookup"><span data-stu-id="4168b-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="4168b-379">*Přidání zobrazení v rámci metody index*</span><span class="sxs-lookup"><span data-stu-id="4168b-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="4168b-380">Zobrazí se dialogové okno **Přidat zobrazení** , ve kterém se vygeneruje soubor šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="4168b-381">Ve výchozím nastavení toto dialogové okno předem vyplní název šablony zobrazení tak, aby odpovídala metodě akce, která ji bude používat.</span><span class="sxs-lookup"><span data-stu-id="4168b-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="4168b-382">Vzhledem k tomu, že jste použili místní nabídku **Přidat zobrazení** v rámci metody akce **indexu** v rámci HomeController, má dialogové okno **Přidat zobrazení** index jako výchozí název zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="4168b-383">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-383">Click **Add**.</span></span>

    <span data-ttu-id="4168b-384">![Přidat dialog zobrazení](aspnet-mvc-4-fundamentals/_static/image14.png "Přidat dialog zobrazení")</span><span class="sxs-lookup"><span data-stu-id="4168b-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="4168b-385">*Přidat dialog zobrazení*</span><span class="sxs-lookup"><span data-stu-id="4168b-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="4168b-386">Visual Studio vygeneruje šablonu zobrazení **index. cshtml** ve složce **Views\Home** a pak ji otevře.</span><span class="sxs-lookup"><span data-stu-id="4168b-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="4168b-387">![Vytvořilo se zobrazení domovského indexu.](aspnet-mvc-4-fundamentals/_static/image15.png "Vytvořilo se zobrazení domovského indexu.")</span><span class="sxs-lookup"><span data-stu-id="4168b-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="4168b-388">*Vytvořilo se zobrazení domovského indexu.*</span><span class="sxs-lookup"><span data-stu-id="4168b-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-389">název a umístění souboru **index. cshtml** je relevantní a řídí se výchozími zásadami vytváření názvů pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="4168b-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="4168b-390">Složka \Views\**Home*\* odpovídá názvu kontroleru (**Domovský** adaptér).</span><span class="sxs-lookup"><span data-stu-id="4168b-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="4168b-391">Název šablony zobrazení (**index**) se shoduje s metodou akce kontroleru, která zobrazení zobrazí.</span><span class="sxs-lookup"><span data-stu-id="4168b-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="4168b-392">V ASP.NET MVC se tak vyhnete nutnosti explicitně zadat název nebo umístění šablony zobrazení při použití těchto zásad vytváření názvů k vrácení zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="4168b-393">Vygenerovaná šablona zobrazení je založena na dříve definované šabloně **\_layout. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="4168b-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="4168b-394">Aktualizujte vlastnost ViewBag. title na **domovskou**stránku a změňte hlavní obsah na **Toto je Domovská stránka**, jak je znázorněno v následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="4168b-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="4168b-395">V Průzkumník řešení vyberte projekt **MvcMusicStore** a spusťte aplikaci stisknutím klávesy **F5** .</span><span class="sxs-lookup"><span data-stu-id="4168b-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="4168b-396">Úloha 4: ověření</span><span class="sxs-lookup"><span data-stu-id="4168b-396">Task 4: Verification</span></span>

<span data-ttu-id="4168b-397">Chcete-li ověřit, zda jste správně provedli všechny kroky v předchozím cvičení, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="4168b-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="4168b-398">S aplikací otevřenými v prohlížeči byste měli mít na paměti následující:</span><span class="sxs-lookup"><span data-stu-id="4168b-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="4168b-399">Našla se metoda akce indexu HomeController a zobrazila se šablona zobrazení **\Views\Home\Index.cshtml** , i když kód se nazývá **návratové zobrazení ()** , protože šablona zobrazení následovala standardní konvence pojmenování.</span><span class="sxs-lookup"><span data-stu-id="4168b-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="4168b-400">Na domovské stránce se zobrazí uvítací zpráva definovaná v rámci šablony zobrazení **\Views\Home\Index.cshtml** .</span><span class="sxs-lookup"><span data-stu-id="4168b-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="4168b-401">Domovská stránka používá šablonu **\_layout. cshtml** , takže úvodní zpráva je obsažena v rozložení HTML webu Standard.</span><span class="sxs-lookup"><span data-stu-id="4168b-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="4168b-402">![Zobrazení domovského indexu pomocí definovaných LayoutPage a stylů](aspnet-mvc-4-fundamentals/_static/image16.png "Zobrazení domovského indexu pomocí definovaných LayoutPage a stylů")</span><span class="sxs-lookup"><span data-stu-id="4168b-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="4168b-403">*Zobrazení domovského indexu pomocí definovaných LayoutPage a stylů*</span><span class="sxs-lookup"><span data-stu-id="4168b-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="4168b-404">Cvičení 5: vytvoření modelu zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="4168b-405">Zatím jste provedli zobrazení pevně zakódované HTML, ale aby bylo možné vytvářet dynamické webové aplikace, měla by šablona zobrazení přijímat informace z kontroleru.</span><span class="sxs-lookup"><span data-stu-id="4168b-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="4168b-406">Jednou z běžných postupů, které je vhodné použít k tomuto účelu, je **ViewModel** vzor, který umožňuje řadiči sbalit všechny informace potřebné k vygenerování příslušné odpovědi HTML.</span><span class="sxs-lookup"><span data-stu-id="4168b-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="4168b-407">V tomto cvičení se naučíte, jak vytvořit třídu ViewModel a přidat požadované vlastnosti: počet žánrů ve Storu a seznam těchto žánrů.</span><span class="sxs-lookup"><span data-stu-id="4168b-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="4168b-408">Také aktualizujete StoreController na použití vytvořeného ViewModel a nakonec vytvoříte novou šablonu zobrazení, na které se zobrazí zmíněné vlastnosti na stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="4168b-409">Úloha 1 – Vytvoření třídy ViewModel</span><span class="sxs-lookup"><span data-stu-id="4168b-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="4168b-410">V této úloze vytvoříte třídu ViewModel, která bude implementovat scénář výpisu žánrů ze Storu.</span><span class="sxs-lookup"><span data-stu-id="4168b-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="4168b-411">Pokud ještě není otevřený, spusťte **vs Express for Web**.</span><span class="sxs-lookup"><span data-stu-id="4168b-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="4168b-412">V nabídce **soubor** klikněte na příkaz **Otevřít projekt**.</span><span class="sxs-lookup"><span data-stu-id="4168b-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="4168b-413">V dialogovém okně Otevřít projekt přejděte na **Source\Ex05-CreatingAViewModel\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="4168b-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="4168b-414">Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="4168b-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="4168b-415">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="4168b-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4168b-416">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4168b-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4168b-417">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="4168b-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4168b-418">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4168b-419">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="4168b-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4168b-420">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="4168b-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4168b-421">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="4168b-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="4168b-422">Vytvořte složku **ViewModels** , která bude obsahovat ViewModel.</span><span class="sxs-lookup"><span data-stu-id="4168b-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="4168b-423">To provedete tak, že kliknete pravým tlačítkem na projekt **MvcMusicStore** nejvyšší úrovně, vyberete **Přidat** a pak **novou složku**.</span><span class="sxs-lookup"><span data-stu-id="4168b-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="4168b-424">![Přidání nové složky](aspnet-mvc-4-fundamentals/_static/image17.png "Přidání nové složky")</span><span class="sxs-lookup"><span data-stu-id="4168b-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="4168b-425">*Přidání nové složky*</span><span class="sxs-lookup"><span data-stu-id="4168b-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="4168b-426">Pojmenujte složku *ViewModels*.</span><span class="sxs-lookup"><span data-stu-id="4168b-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="4168b-427">![ViewModels složka v Průzkumník řešení](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels složka v Průzkumník řešení")</span><span class="sxs-lookup"><span data-stu-id="4168b-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="4168b-428">*ViewModels složka v Průzkumník řešení*</span><span class="sxs-lookup"><span data-stu-id="4168b-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="4168b-429">Vytvořte třídu **ViewModel** .</span><span class="sxs-lookup"><span data-stu-id="4168b-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="4168b-430">Provedete to tak, že kliknete pravým tlačítkem na nedávno vytvořenou složku **ViewModels** , vyberete **Přidat** a pak **novou položku**.</span><span class="sxs-lookup"><span data-stu-id="4168b-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="4168b-431">V části **kód**zvolte položku **třídy** a pojmenujte soubor *StoreIndexViewModel.cs*a pak klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="4168b-432">![Přidání nové třídy](aspnet-mvc-4-fundamentals/_static/image19.png "Přidání nové třídy")</span><span class="sxs-lookup"><span data-stu-id="4168b-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="4168b-433">*Přidání nové třídy*</span><span class="sxs-lookup"><span data-stu-id="4168b-433">*Adding a new Class*</span></span>

    <span data-ttu-id="4168b-434">![Vytváření třídy StoreIndexViewModel](aspnet-mvc-4-fundamentals/_static/image20.png "Vytváření třídy StoreIndexViewModel")</span><span class="sxs-lookup"><span data-stu-id="4168b-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="4168b-435">*Vytváření třídy StoreIndexViewModel*</span><span class="sxs-lookup"><span data-stu-id="4168b-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="4168b-436">Úloha 2 – Přidání vlastností do třídy ViewModel</span><span class="sxs-lookup"><span data-stu-id="4168b-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="4168b-437">Existují dva parametry, které mají být předány z StoreController do šablony zobrazení, aby bylo možné vygenerovat očekávanou odpověď HTML: počet žánrů ve Storu a seznam těchto žánrů.</span><span class="sxs-lookup"><span data-stu-id="4168b-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="4168b-438">V této úloze přidáte tyto 2 vlastnosti do třídy **StoreIndexViewModel** : **NumberOfGenres** (celé číslo) a **žánry** (seznam řetězců).</span><span class="sxs-lookup"><span data-stu-id="4168b-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="4168b-439">Přidejte vlastnosti **NumberOfGenres** a **žánrs** do třídy **StoreIndexViewModel** .</span><span class="sxs-lookup"><span data-stu-id="4168b-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="4168b-440">K tomu přidejte následující 2 řádky do definice třídy:</span><span class="sxs-lookup"><span data-stu-id="4168b-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="4168b-441">(Fragment kódu – *základní informace o ASP.NET MVC 4 – Ex5 StoreIndexViewModel vlastnosti*)</span><span class="sxs-lookup"><span data-stu-id="4168b-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="4168b-442">Zápis **{Get; Set;}** používá C#funkci automaticky implementovaného vlastností.</span><span class="sxs-lookup"><span data-stu-id="4168b-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="4168b-443">Poskytuje výhody vlastnosti, aniž by bylo nutné deklarovat pole pro zálohování.</span><span class="sxs-lookup"><span data-stu-id="4168b-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="4168b-444">Úloha 3 – aktualizace StoreController pro použití StoreIndexViewModel</span><span class="sxs-lookup"><span data-stu-id="4168b-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="4168b-445">Třída **StoreIndexViewModel** zapouzdřuje informace potřebné k předání metody indexu **StoreController**do šablony zobrazení, aby bylo možné vygenerovat odpověď.</span><span class="sxs-lookup"><span data-stu-id="4168b-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="4168b-446">V této úloze aktualizujete **StoreController** tak, aby používal **StoreIndexViewModel**.</span><span class="sxs-lookup"><span data-stu-id="4168b-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="4168b-447">Otevřete třídu **StoreController** .</span><span class="sxs-lookup"><span data-stu-id="4168b-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="4168b-448">![Otevírání třídy StoreController](aspnet-mvc-4-fundamentals/_static/image21.png "Otevírání třídy StoreController")</span><span class="sxs-lookup"><span data-stu-id="4168b-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="4168b-449">*Otevírání třídy StoreController*</span><span class="sxs-lookup"><span data-stu-id="4168b-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="4168b-450">Aby bylo možné použít třídu **StoreIndexViewModel** z **StoreController**, přidejte následující obor názvů na začátek kódu **StoreController** :</span><span class="sxs-lookup"><span data-stu-id="4168b-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="4168b-451">(Fragment kódu – *ASP.NET MVC 4 – Ex5 StoreIndexViewModel s využitím ViewModels*)</span><span class="sxs-lookup"><span data-stu-id="4168b-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="4168b-452">Změňte metodu akce **indexu** **StoreController**tak, aby vytvořila a naplnila objekt **StoreIndexViewModel** a pak ho předá do šablony zobrazení, aby se s ním generovala odpověď HTML.</span><span class="sxs-lookup"><span data-stu-id="4168b-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-453">V testovacím prostředí &quot;ASP.NET MVC a přístup k datům&quot; budete psát kód, který načte seznam žánrů ze Storu z databáze.</span><span class="sxs-lookup"><span data-stu-id="4168b-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="4168b-454">V následujícím kódu vytvoříte **seznam** fiktivních datových žánrů, které naplní **StoreIndexViewModel**.</span><span class="sxs-lookup"><span data-stu-id="4168b-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="4168b-455">Po vytvoření a nastavení objektu **StoreIndexViewModel** bude předán jako argument metody **zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="4168b-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="4168b-456">To znamená, že šablona zobrazení bude používat tento objekt k vygenerování odpovědi HTML.</span><span class="sxs-lookup"><span data-stu-id="4168b-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="4168b-457">Nahraďte metodu **indexu** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="4168b-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="4168b-458">(Fragment kódu – *ASP.NET MVC 4 – metoda Ex5 StoreController index*)</span><span class="sxs-lookup"><span data-stu-id="4168b-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="4168b-459">Pokud si nejste obeznámeni C#s, můžete předpokládat, že použití **var** znamená, že proměnná **viewModel** je pozdní vazbou.</span><span class="sxs-lookup"><span data-stu-id="4168b-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="4168b-460">To není správné – C# kompilátor používá odvození typu v závislosti na tom, co přiřadíte proměnné, abyste zjistili, že **ViewModel** je typu **StoreIndexViewModel**.</span><span class="sxs-lookup"><span data-stu-id="4168b-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="4168b-461">Také sestavením místní proměnné **viewModel** jako typu **StoreIndexViewModel** získáte kontrolu doby kompilace a podporu editoru kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="4168b-462">Úloha 4 – Vytvoření šablony zobrazení, která používá StoreIndexViewModel</span><span class="sxs-lookup"><span data-stu-id="4168b-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="4168b-463">V této úloze vytvoříte šablonu zobrazení, která bude používat objekt StoreIndexViewModel předaný z kontroleru k zobrazení seznamu žánrů.</span><span class="sxs-lookup"><span data-stu-id="4168b-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="4168b-464">Než vytvoříte novou šablonu zobrazení, sestavte projekt tak, aby **dialog Přidat zobrazení** věděl o třídě **StoreIndexViewModel** .</span><span class="sxs-lookup"><span data-stu-id="4168b-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="4168b-465">Sestavte projekt výběrem položky nabídky **sestavení** a poté **Sestavte MvcMusicStore**.</span><span class="sxs-lookup"><span data-stu-id="4168b-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="4168b-466">![Sestavení projektu](aspnet-mvc-4-fundamentals/_static/image22.png "Sestavení projektu")</span><span class="sxs-lookup"><span data-stu-id="4168b-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="4168b-467">*Sestavení projektu*</span><span class="sxs-lookup"><span data-stu-id="4168b-467">*Building the project*</span></span>
2. <span data-ttu-id="4168b-468">Vytvoří novou šablonu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-468">Create a new View template.</span></span> <span data-ttu-id="4168b-469">Provedete to tak, že kliknete pravým tlačítkem dovnitř metody **indexu** a vyberete **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="4168b-470">![Přidání zobrazení](aspnet-mvc-4-fundamentals/_static/image23.png "Přidání zobrazení")</span><span class="sxs-lookup"><span data-stu-id="4168b-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="4168b-471">*Přidání zobrazení*</span><span class="sxs-lookup"><span data-stu-id="4168b-471">*Adding a View*</span></span>
3. <span data-ttu-id="4168b-472">Vzhledem k tomu, že se **dialogové okno Přidat zobrazení** vyvolalo z **StoreController**, přidá se ve výchozím nastavení do souboru **\Views\Store\Index.cshtml** šablona zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="4168b-473">Zaškrtněte políčko **vytvořit silně typovou vlastnost zobrazení** a pak jako **třídu modelu**vyberte **StoreIndexViewModel** .</span><span class="sxs-lookup"><span data-stu-id="4168b-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="4168b-474">Také se ujistěte, že vybraný zobrazovací modul je **Razor**.</span><span class="sxs-lookup"><span data-stu-id="4168b-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="4168b-475">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-475">Click **Add**.</span></span>

    <span data-ttu-id="4168b-476">![Přidat dialog zobrazení](aspnet-mvc-4-fundamentals/_static/image24.png "Přidat dialog zobrazení")</span><span class="sxs-lookup"><span data-stu-id="4168b-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="4168b-477">*Přidat dialog zobrazení*</span><span class="sxs-lookup"><span data-stu-id="4168b-477">*Add View Dialog*</span></span>

    <span data-ttu-id="4168b-478">Vytvoří a otevře se soubor šablony zobrazení **\Views\Store\Index.cshtml** .</span><span class="sxs-lookup"><span data-stu-id="4168b-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="4168b-479">Na základě informací poskytnutých v dialogovém okně **Přidat zobrazení** v posledním kroku bude šablona zobrazení očekávat instanci **StoreIndexViewModel** jako data, která se mají použít k vygenerování odpovědi HTML.</span><span class="sxs-lookup"><span data-stu-id="4168b-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="4168b-480">Všimněte si, že šablona dědí `ViewPage<musicstore.viewmodels.storeindexviewmodel>` v C#.</span><span class="sxs-lookup"><span data-stu-id="4168b-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="4168b-481">Úloha 5 – aktualizace šablony zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="4168b-482">V této úloze aktualizujete šablonu zobrazení vytvořenou v posledním úkolu, aby se získal počet žánrů a jejich názvy v rámci stránky.</span><span class="sxs-lookup"><span data-stu-id="4168b-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="4168b-483">K provedení kódu v rámci šablony zobrazení použijete syntaxi @ (často se označuje jako &quot;kódu&quot;Nuggets).</span><span class="sxs-lookup"><span data-stu-id="4168b-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="4168b-484">V souboru **index. cshtml** v rámci složky **úložiště** nahraďte kód následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="4168b-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="4168b-485">Přeskočíte seznam žánrů v **StoreIndexViewModel** a vytvořte&gt;seznam HTML **&lt;ul** pomocí smyčky **foreach** .</span><span class="sxs-lookup"><span data-stu-id="4168b-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="4168b-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="4168b-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="4168b-487">Stisknutím klávesy **F5** spusťte aplikaci a přejděte na **/Store**.</span><span class="sxs-lookup"><span data-stu-id="4168b-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="4168b-488">Zobrazí se seznam žánrů předaných do objektu **StoreIndexViewModel** z **StoreController** do šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="4168b-489">![Zobrazit zobrazení seznamu žánrů](aspnet-mvc-4-fundamentals/_static/image26.png "Zobrazit zobrazení seznamu žánrů")</span><span class="sxs-lookup"><span data-stu-id="4168b-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="4168b-490">*Zobrazit zobrazení seznamu žánrů*</span><span class="sxs-lookup"><span data-stu-id="4168b-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="4168b-491">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="4168b-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="4168b-492">Cvičení 6: použití parametrů v zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="4168b-493">V cvičení 3 jste zjistili, jak předat parametry do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="4168b-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="4168b-494">V tomto cvičení se naučíte používat tyto parametry v šabloně zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="4168b-495">Pro tento účel se nejprve zavedete na model třídy, které vám pomůžou spravovat vaše data a logiku domény.</span><span class="sxs-lookup"><span data-stu-id="4168b-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="4168b-496">Dále se naučíte, jak vytvořit odkazy na stránky v aplikaci ASP.NET MVC, aniž byste museli mít obavy, jako je kódování cest URL.</span><span class="sxs-lookup"><span data-stu-id="4168b-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="4168b-497">Úloha 1 – Přidání tříd modelu</span><span class="sxs-lookup"><span data-stu-id="4168b-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="4168b-498">Na rozdíl od ViewModels, které jsou vytvořeny pouze k předání informací z kontroleru do zobrazení, třídy modelu jsou sestaveny tak, aby obsahovaly a spravovaly data a logiku domény.</span><span class="sxs-lookup"><span data-stu-id="4168b-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="4168b-499">V této úloze přidáte dvě třídy modelu, které budou představovat tyto koncepty: **Žánr** a **album**.</span><span class="sxs-lookup"><span data-stu-id="4168b-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="4168b-500">Pokud ještě není otevřený, spusťte **vs Express for Web**</span><span class="sxs-lookup"><span data-stu-id="4168b-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="4168b-501">V nabídce **soubor** klikněte na příkaz **Otevřít projekt**.</span><span class="sxs-lookup"><span data-stu-id="4168b-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="4168b-502">V dialogovém okně Otevřít projekt přejděte na **Source\Ex06-UsingParametersInView\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="4168b-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="4168b-503">Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="4168b-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="4168b-504">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="4168b-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4168b-505">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4168b-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4168b-506">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="4168b-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4168b-507">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4168b-508">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="4168b-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4168b-509">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="4168b-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4168b-510">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="4168b-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="4168b-511">Přidejte třídu modelu **žánru** .</span><span class="sxs-lookup"><span data-stu-id="4168b-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="4168b-512">Provedete to tak, že kliknete pravým tlačítkem na složku **modely** v **Průzkumník řešení**, vyberete **Přidat** a pak **novou položku** .</span><span class="sxs-lookup"><span data-stu-id="4168b-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="4168b-513">V části **kód**zvolte položku **třídy** a pojmenujte soubor *Genre.cs*a pak klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="4168b-514">![Přidání třídy](aspnet-mvc-4-fundamentals/_static/image27.png "Přidání třídy")</span><span class="sxs-lookup"><span data-stu-id="4168b-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="4168b-515">*Přidání nové položky*</span><span class="sxs-lookup"><span data-stu-id="4168b-515">*Adding a new item*</span></span>

    <span data-ttu-id="4168b-516">![Přidat třídu modelu žánru](aspnet-mvc-4-fundamentals/_static/image28.png "Přidat třídu modelu žánru")</span><span class="sxs-lookup"><span data-stu-id="4168b-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="4168b-517">*Přidat třídu modelu žánru*</span><span class="sxs-lookup"><span data-stu-id="4168b-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="4168b-518">Přidejte do třídy žánru vlastnost **název** .</span><span class="sxs-lookup"><span data-stu-id="4168b-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="4168b-519">Chcete-li to provést, přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="4168b-519">To do this, add the following code:</span></span>

    <span data-ttu-id="4168b-520">(Fragment kódu – *základy ASP.NET MVC 4 – Žánr Ex6*)</span><span class="sxs-lookup"><span data-stu-id="4168b-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="4168b-521">Za stejným postupem jako předtím přidejte třídu **alba** .</span><span class="sxs-lookup"><span data-stu-id="4168b-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="4168b-522">Provedete to tak, že kliknete pravým tlačítkem na složku **modely** v **Průzkumník řešení**, vyberete **Přidat** a pak **novou položku** .</span><span class="sxs-lookup"><span data-stu-id="4168b-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="4168b-523">V části **kód**zvolte položku **třídy** a pojmenujte soubor *album.cs*a pak klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="4168b-524">Přidejte dvě vlastnosti do třídy alba: **Žánr** a **title**.</span><span class="sxs-lookup"><span data-stu-id="4168b-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="4168b-525">Chcete-li to provést, přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="4168b-525">To do this, add the following code:</span></span>

    <span data-ttu-id="4168b-526">(Fragment kódu – *základy ASP.NET MVC 4 – album Ex6*)</span><span class="sxs-lookup"><span data-stu-id="4168b-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="4168b-527">Úloha 2 – Přidání StoreBrowseViewModel</span><span class="sxs-lookup"><span data-stu-id="4168b-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="4168b-528">V této úloze se použije **StoreBrowseViewModel** , aby se zobrazila alba odpovídající vybranému žánru.</span><span class="sxs-lookup"><span data-stu-id="4168b-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="4168b-529">V této úloze vytvoříte tuto třídu a pak přidáte dvě vlastnosti, které budou zpracovávat **Žánr** a seznam jeho **alb**.</span><span class="sxs-lookup"><span data-stu-id="4168b-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="4168b-530">Přidejte třídu **StoreBrowseViewModel** .</span><span class="sxs-lookup"><span data-stu-id="4168b-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="4168b-531">Provedete to tak, že kliknete pravým tlačítkem na složku **ViewModels** v **Průzkumník řešení**, vyberete **Přidat** a pak **novou položku** .</span><span class="sxs-lookup"><span data-stu-id="4168b-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="4168b-532">V části **kód**zvolte položku **třídy** a pojmenujte soubor *StoreBrowseViewModel.cs*a pak klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="4168b-533">Přidejte odkaz na modely ve třídě **StoreBrowseViewModel** .</span><span class="sxs-lookup"><span data-stu-id="4168b-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="4168b-534">Chcete-li to provést, přidejte následující obor názvů using:</span><span class="sxs-lookup"><span data-stu-id="4168b-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="4168b-535">(Fragment kódu – *základy ASP.NET MVC 4 – Ex6 UsingModel*)</span><span class="sxs-lookup"><span data-stu-id="4168b-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="4168b-536">Přidejte dvě vlastnosti do třídy **StoreBrowseViewModel** : **Žánr** a **alba**.</span><span class="sxs-lookup"><span data-stu-id="4168b-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="4168b-537">Chcete-li to provést, přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="4168b-537">To do this, add the following code:</span></span>

    <span data-ttu-id="4168b-538">(Fragment kódu – *základy ASP.NET MVC 4 – Ex6 ModelProperties*)</span><span class="sxs-lookup"><span data-stu-id="4168b-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="4168b-539">Co je **seznam&lt;alba&gt;** ?: Tato definice používá typ **&gt;typu seznam&lt;t** , kde **t** omezuje typ, na který prvky tohoto **seznamu** patří, v tomto případě **alba** (nebo některé z jeho potomků).</span><span class="sxs-lookup"><span data-stu-id="4168b-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="4168b-540">Tato schopnost navrhovat třídy a metody, které odloží specifikace jednoho nebo více typů, dokud není deklarována třída nebo metoda a instance kódu klienta je funkcí C# jazyka s názvem **Obecné**.</span><span class="sxs-lookup"><span data-stu-id="4168b-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="4168b-541">**Seznam&lt;t&gt;** je obecný ekvivalent typu **ArrayList** a je k dispozici v oboru názvů **System. Collections. Generic** .</span><span class="sxs-lookup"><span data-stu-id="4168b-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="4168b-542">Jednou z výhod použití **generických** typů je, že od zadání typu není nutné provádět kontrolu typu operací, jako je například přetypování prvků do **alba** , stejně jako při práci s objektem **ArrayList**.</span><span class="sxs-lookup"><span data-stu-id="4168b-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="4168b-543">Úloha 3 – použití nového ViewModel v StoreController</span><span class="sxs-lookup"><span data-stu-id="4168b-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="4168b-544">V této úloze upravíte metody akce **Browse** a **Detail** pro **StoreController**, které budou používat nový **StoreBrowseViewModel**.</span><span class="sxs-lookup"><span data-stu-id="4168b-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="4168b-545">Přidejte odkaz do složky modely ve třídě **StoreController** .</span><span class="sxs-lookup"><span data-stu-id="4168b-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="4168b-546">Provedete to tak, že rozbalíte složku **Controllers** v **Průzkumník řešení** a otevřete třídu **StoreController** .</span><span class="sxs-lookup"><span data-stu-id="4168b-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="4168b-547">Pak přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="4168b-547">Then add the following code:</span></span>

    <span data-ttu-id="4168b-548">(Fragment kódu – *základy ASP.NET MVC 4 – Ex6 UsingModelInController*)</span><span class="sxs-lookup"><span data-stu-id="4168b-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="4168b-549">Nahraďte metodu akce **procházení** a použijte třídu **StoreViewBrowseController** .</span><span class="sxs-lookup"><span data-stu-id="4168b-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="4168b-550">Vytvoříte Žánr a dva nové objekty alba s fiktivními daty (v dalším cvičení budete spotřebovávat skutečná data z databáze).</span><span class="sxs-lookup"><span data-stu-id="4168b-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="4168b-551">Chcete-li to provést, nahraďte metodu **Browse** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="4168b-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="4168b-552">(Fragment kódu – *základy ASP.NET MVC 4 – Ex6 BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="4168b-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="4168b-553">Nahraďte metodu Action **Details** pro použití třídy **StoreViewBrowseController** .</span><span class="sxs-lookup"><span data-stu-id="4168b-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="4168b-554">Vytvoří se nový objekt **alba** , který se má vrátit do **zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="4168b-555">Chcete-li to provést, nahraďte metodu **Details** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="4168b-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="4168b-556">(Fragment kódu – *základy ASP.NET MVC 4 – Ex6 DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="4168b-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="4168b-557">Úloha 4 – Přidání šablony zobrazení pro procházení</span><span class="sxs-lookup"><span data-stu-id="4168b-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="4168b-558">V této úloze přidáte zobrazení pro **procházení** , ve kterém se zobrazí alba pro určitý Žánr.</span><span class="sxs-lookup"><span data-stu-id="4168b-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="4168b-559">Předtím, než vytvoříte novou šablonu zobrazení, byste měli sestavit projekt tak, aby dialog **Přidat zobrazení** věděl o třídě **ViewModel** , která se má použít.</span><span class="sxs-lookup"><span data-stu-id="4168b-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="4168b-560">Sestavte projekt výběrem položky nabídky **sestavení** a poté **Sestavte MvcMusicStore**.</span><span class="sxs-lookup"><span data-stu-id="4168b-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="4168b-561">Přidejte zobrazení pro **procházení** .</span><span class="sxs-lookup"><span data-stu-id="4168b-561">Add a **Browse** View.</span></span> <span data-ttu-id="4168b-562">Provedete to tak, že kliknete pravým tlačítkem na metodu akce **procházení** **StoreController** a kliknete na **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="4168b-563">V dialogovém okně **Přidat zobrazení** ověřte, zda je název zobrazení **procházen**.</span><span class="sxs-lookup"><span data-stu-id="4168b-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="4168b-564">Zaškrtněte políčko **vytvořit zobrazení silného typu** a v rozevírací nabídce **třída modelu** vyberte **StoreBrowseViewModel** .</span><span class="sxs-lookup"><span data-stu-id="4168b-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="4168b-565">Ostatní pole ponechte výchozí hodnotou.</span><span class="sxs-lookup"><span data-stu-id="4168b-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="4168b-566">Pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-566">Then click **Add**.</span></span>

    <span data-ttu-id="4168b-567">![Přidání zobrazení procházení](aspnet-mvc-4-fundamentals/_static/image29.png "Přidání zobrazení procházení")</span><span class="sxs-lookup"><span data-stu-id="4168b-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="4168b-568">*Přidání zobrazení procházení*</span><span class="sxs-lookup"><span data-stu-id="4168b-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="4168b-569">Upravte **procházení. cshtml** pro zobrazení informací o žánru a přístup k objektu **StoreBrowseViewModel** , který je předán šabloně zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="4168b-570">Chcete-li to provést, nahraďte obsah následujícím způsobem:C#()</span><span class="sxs-lookup"><span data-stu-id="4168b-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="4168b-571">Úloha 5 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="4168b-572">V této úloze otestujete, že metoda **procházení** načte alba z akce **Procházet** metodu.</span><span class="sxs-lookup"><span data-stu-id="4168b-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="4168b-573">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4168b-574">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-574">The project starts in the Home page.</span></span> <span data-ttu-id="4168b-575">Změňte adresu URL na **/Store/Browse? Žánr = disco** pro ověření, že akce vrátí dvě alba.</span><span class="sxs-lookup"><span data-stu-id="4168b-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="4168b-576">![Procházení – Uložit alba na discích](aspnet-mvc-4-fundamentals/_static/image30.png "Procházení – Uložit alba na discích")</span><span class="sxs-lookup"><span data-stu-id="4168b-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="4168b-577">*Procházení – Uložit alba na discích*</span><span class="sxs-lookup"><span data-stu-id="4168b-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="4168b-578">Úloha 6 – zobrazení informací o konkrétním albu</span><span class="sxs-lookup"><span data-stu-id="4168b-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="4168b-579">V této úloze implementujete zobrazení **úložiště/podrobností** pro zobrazení informací o konkrétním albu.</span><span class="sxs-lookup"><span data-stu-id="4168b-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="4168b-580">V této praktické laboratorní laboratoři se všechno, co zobrazíte o albu, již nachází v šabloně **zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="4168b-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="4168b-581">Takže místo vytvoření třídy **StoreDetailsViewModel** použijete aktuální šablonu **StoreBrowseViewModel** , která do ní předává album.</span><span class="sxs-lookup"><span data-stu-id="4168b-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="4168b-582">V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="4168b-583">Přidejte nové zobrazení **podrobností** pro metodu Action **StoreController** **Details** .</span><span class="sxs-lookup"><span data-stu-id="4168b-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="4168b-584">Provedete to tak, že kliknete pravým tlačítkem na metodu **Details** ve třídě **StoreController** a kliknete na **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="4168b-585">V dialogovém okně **Přidat zobrazení** ověřte, zda je **název zobrazení** **detailed**.</span><span class="sxs-lookup"><span data-stu-id="4168b-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="4168b-586">Zaškrtněte políčko **vytvořit zobrazení silného typu** a v rozevíracím seznamu **třída modelu** vyberte **album** .</span><span class="sxs-lookup"><span data-stu-id="4168b-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="4168b-587">Ostatní pole ponechte výchozí hodnotou.</span><span class="sxs-lookup"><span data-stu-id="4168b-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="4168b-588">Pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-588">Then click **Add**.</span></span> <span data-ttu-id="4168b-589">Tím se vytvoří a otevře soubor **\Views\Store\Details.cshtml** .</span><span class="sxs-lookup"><span data-stu-id="4168b-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="4168b-590">![Přidání zobrazení podrobností](aspnet-mvc-4-fundamentals/_static/image31.png "Přidání zobrazení podrobností")</span><span class="sxs-lookup"><span data-stu-id="4168b-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="4168b-591">*Přidání zobrazení podrobností*</span><span class="sxs-lookup"><span data-stu-id="4168b-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="4168b-592">Upravte soubor **Details. cshtml** pro zobrazení informací o albu a přístup k objektu **alba** , který je předán šabloně zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="4168b-593">Chcete-li to provést, nahraďte obsah následujícím způsobem:C#()</span><span class="sxs-lookup"><span data-stu-id="4168b-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="4168b-594">Úloha 7 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="4168b-595">V této úloze otestujete, že zobrazení **podrobností** načte informace o albu z metody **Action Details** .</span><span class="sxs-lookup"><span data-stu-id="4168b-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="4168b-596">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4168b-597">Projekt se spustí na **domovské** stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="4168b-598">Změňte adresu URL na **/Store/Details/5** a ověřte informace o albu.</span><span class="sxs-lookup"><span data-stu-id="4168b-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="4168b-599">![Podrobnosti o albu procházení](aspnet-mvc-4-fundamentals/_static/image32.png "Podrobnosti o albu procházení")</span><span class="sxs-lookup"><span data-stu-id="4168b-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="4168b-600">*Podrobnosti o procházení alba*</span><span class="sxs-lookup"><span data-stu-id="4168b-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="4168b-601">Úloha 8 – přidávání odkazů mezi stránkami</span><span class="sxs-lookup"><span data-stu-id="4168b-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="4168b-602">V tomto úkolu přidáte odkaz v zobrazení úložiště tak, aby měl odkaz v rámci každého názvu žánru na příslušnou adresu URL **/Store/Browse** .</span><span class="sxs-lookup"><span data-stu-id="4168b-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="4168b-603">Když kliknete na Žánr, například, bude instance **discového**ovládání přejít na **/Store/Browse? Žánr =** adresa URL.</span><span class="sxs-lookup"><span data-stu-id="4168b-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="4168b-604">V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="4168b-605">Aktualizujte stránku **index** a přidejte odkaz na stránku **procházení** .</span><span class="sxs-lookup"><span data-stu-id="4168b-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="4168b-606">To provedete tak, že v **Průzkumník řešení** rozbalíte složku **zobrazení** , pak na složku **Store** a dvakrát kliknete na stránku **index. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="4168b-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="4168b-607">Přidejte odkaz na zobrazení procházení, které indikuje vybraný Žánr.</span><span class="sxs-lookup"><span data-stu-id="4168b-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="4168b-608">Chcete-li to provést, nahraďte následující zvýrazněný kód v rámci **&lt;&gt;** značkyC#: ()</span><span class="sxs-lookup"><span data-stu-id="4168b-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="4168b-609">Další postup by se propojuje přímo se stránkou s kódem podobným následujícímu:</span><span class="sxs-lookup"><span data-stu-id="4168b-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="4168b-610">&lt;a href =&quot;/Store/Browse? Žánr =@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="4168b-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="4168b-611">I když tento přístup funguje, závisí na pevně zakódované řetězci.</span><span class="sxs-lookup"><span data-stu-id="4168b-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="4168b-612">Pokud později řadič přejmenujete, budete muset tuto instrukci změnit ručně.</span><span class="sxs-lookup"><span data-stu-id="4168b-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="4168b-613">Lepší alternativou je použití pomocné metody **HTML** .</span><span class="sxs-lookup"><span data-stu-id="4168b-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="4168b-614">ASP.NET MVC obsahuje pomocnou metodu HTML, která je pro takové úkoly k dispozici.</span><span class="sxs-lookup"><span data-stu-id="4168b-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="4168b-615">Pomocná metoda **HTML. ActionLink ()** usnadňuje vytváření **&lt;ch odkazů&gt;** , aby se zajistilo správné kódování URL cest.</span><span class="sxs-lookup"><span data-stu-id="4168b-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="4168b-616">HTML. ActionLink má několik přetížení.</span><span class="sxs-lookup"><span data-stu-id="4168b-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="4168b-617">V tomto cvičení použijete jeden, který má tři parametry:</span><span class="sxs-lookup"><span data-stu-id="4168b-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="4168b-618">Text odkazu, ve kterém se zobrazí název žánru</span><span class="sxs-lookup"><span data-stu-id="4168b-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="4168b-619">Název akce kontroleru (**Procházet**)</span><span class="sxs-lookup"><span data-stu-id="4168b-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="4168b-620">Hodnoty parametrů směrování, zadání názvu (**Žánr**) a hodnoty (**název žánru**)</span><span class="sxs-lookup"><span data-stu-id="4168b-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="4168b-621">Úloha 9 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="4168b-622">V této úloze otestujete, že se každý žánr zobrazuje s odkazem na příslušnou adresu URL **/Store/Browse** .</span><span class="sxs-lookup"><span data-stu-id="4168b-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="4168b-623">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4168b-624">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-624">The project starts in the Home page.</span></span> <span data-ttu-id="4168b-625">Změňte adresu URL na **/Store** , abyste ověřili, že každý žánr odkazuje na příslušnou adresu URL **/Store/Browse** .</span><span class="sxs-lookup"><span data-stu-id="4168b-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="4168b-626">![Procházení žánrů s odkazy na stránku procházení](aspnet-mvc-4-fundamentals/_static/image33.png "Procházení žánrů s odkazy na stránku procházení")</span><span class="sxs-lookup"><span data-stu-id="4168b-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="4168b-627">*Procházení žánrů s odkazy na stránku procházení*</span><span class="sxs-lookup"><span data-stu-id="4168b-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="4168b-628">Úloha 10 – použití dynamické kolekce ViewModel k předání hodnot</span><span class="sxs-lookup"><span data-stu-id="4168b-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="4168b-629">V této úloze se naučíte jednoduchou a výkonnou metodu předávání hodnot mezi kontrolkou a zobrazením bez provedení změn v modelu.</span><span class="sxs-lookup"><span data-stu-id="4168b-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="4168b-630">ASP.NET MVC 4 poskytuje kolekci &quot;ViewModel&quot;, která se dá přiřadit k libovolné dynamické hodnotě a k nim přistupovaly i v řadičích a zobrazeních.</span><span class="sxs-lookup"><span data-stu-id="4168b-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="4168b-631">Nyní použijete dynamickou kolekci ViewBag k předání seznamu &quot;ch **žánrů označených hvězdičkou**&quot; z kontroleru do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="4168b-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="4168b-632">Zobrazení indexu úložiště bude mít přístup k **ViewModel** a zobrazí se informace.</span><span class="sxs-lookup"><span data-stu-id="4168b-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="4168b-633">V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="4168b-634">Otevřete **StoreController.cs** a upravte metodu **index** a vytvořte seznam žánrů označených hvězdičkou do kolekce ViewModel:</span><span class="sxs-lookup"><span data-stu-id="4168b-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="4168b-635">Pro přístup k vlastnostem můžete také použít syntaxi **ViewBag [&quot;označených hvězdičkou&quot;]** .</span><span class="sxs-lookup"><span data-stu-id="4168b-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="4168b-636">Ikona hvězdičky **&quot;označených hvězdičkou. png&quot;** obsažená ve složce **Source\Assets\Images** tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="4168b-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="4168b-637">Chcete-li jej přidat do aplikace, přetáhněte jeho obsah z okna **Průzkumníka Windows** do **Průzkumník řešení** v aplikaci Visual Web Developer Express, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="4168b-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="4168b-638">![Přidání obrázku hvězdičky do řešení](aspnet-mvc-4-fundamentals/_static/image34.png "Přidání obrázku hvězdičky do řešení")</span><span class="sxs-lookup"><span data-stu-id="4168b-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="4168b-639">*Přidání obrázku hvězdičky do řešení*</span><span class="sxs-lookup"><span data-stu-id="4168b-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="4168b-640">Otevřete zobrazení **Store/index. cshtml** a upravte obsah.</span><span class="sxs-lookup"><span data-stu-id="4168b-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="4168b-641">V kolekci **ViewBag** si přečtete vlastnost &quot;označených hvězdičkou&quot; a zobrazí se dotaz, jestli je aktuální název žánru v seznamu.</span><span class="sxs-lookup"><span data-stu-id="4168b-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="4168b-642">V takovém případě se zobrazí ikona hvězdičky přímo na odkaz Žánr.</span><span class="sxs-lookup"><span data-stu-id="4168b-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="4168b-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="4168b-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="4168b-644">Úloha 11 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="4168b-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="4168b-645">V této úloze otestujete, že žánry označených hvězdičkou zobrazí ikonu hvězdičky.</span><span class="sxs-lookup"><span data-stu-id="4168b-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="4168b-646">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4168b-647">Projekt se spustí na **domovské** stránce.</span><span class="sxs-lookup"><span data-stu-id="4168b-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="4168b-648">Změňte adresu URL na **/Store** a ověřte, že každý doporučený Žánr má popisek pro respektování:</span><span class="sxs-lookup"><span data-stu-id="4168b-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="4168b-649">![Procházení žánrů pomocí označených hvězdičkou elementů](aspnet-mvc-4-fundamentals/_static/image35.png "Procházení žánrů pomocí označených hvězdičkou elementů")</span><span class="sxs-lookup"><span data-stu-id="4168b-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="4168b-650">*Procházení žánrů pomocí označených hvězdičkou elementů*</span><span class="sxs-lookup"><span data-stu-id="4168b-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="4168b-651">Cvičení 7: zaASP.NETm s novou šablonou MVC 4</span><span class="sxs-lookup"><span data-stu-id="4168b-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="4168b-652">V tomto cvičení budete zkoumat vylepšení v šablonách projektů ASP.NET MVC 4 a Prohlédněte si nejdůležitější funkce nové šablony.</span><span class="sxs-lookup"><span data-stu-id="4168b-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="4168b-653">Úloha 1: zkoumání šablony internetové aplikace ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="4168b-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="4168b-654">Pokud ještě není otevřený, spusťte **vs Express for Web**</span><span class="sxs-lookup"><span data-stu-id="4168b-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="4168b-655">Vyberte **soubor | Nové |** Příkaz nabídky projektu</span><span class="sxs-lookup"><span data-stu-id="4168b-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="4168b-656">V dialogovém okně **Nový projekt** vyberte **vizuál C#| Webová** šablona ve stromu levého podokna a volba **webové aplikace ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="4168b-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="4168b-657">**Pojmenujte** projekt *MusicStore* a aktualizujte **název řešení** na *začátek*a pak vyberte umístění (nebo ponechte výchozí) a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="4168b-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="4168b-658">![Vytváří se nový projekt ASP.NET MVC 4.](aspnet-mvc-4-fundamentals/_static/image36.png "Vytváří se nový projekt ASP.NET MVC 4.")</span><span class="sxs-lookup"><span data-stu-id="4168b-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="4168b-659">*Vytváří se nový projekt ASP.NET MVC 4.*</span><span class="sxs-lookup"><span data-stu-id="4168b-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="4168b-660">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **Internetová aplikace** a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="4168b-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="4168b-661">Všimněte si, že jako zobrazovací modul můžete vybrat buď Razor, nebo ASPX.</span><span class="sxs-lookup"><span data-stu-id="4168b-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="4168b-662">![Vytváří se nová internetová aplikace ASP.NET MVC 4.](aspnet-mvc-4-fundamentals/_static/image37.png "Vytváří se nová internetová aplikace ASP.NET MVC 4.")</span><span class="sxs-lookup"><span data-stu-id="4168b-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="4168b-663">*Vytváří se nová internetová aplikace ASP.NET MVC 4.*</span><span class="sxs-lookup"><span data-stu-id="4168b-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-664">Syntaxe Razor byla představena v ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="4168b-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="4168b-665">Jeho cílem je minimalizovat počet znaků a klávesových úhozů vyžadovaných v souboru a povolit tak rychlé a kapalné pracovní postupy v kódování.</span><span class="sxs-lookup"><span data-stu-id="4168b-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="4168b-666">Razor využívá stávající C#jazykové dovednosti v/vb (nebo jiné) a poskytuje syntaxi značek šablony, která umožňuje pracovní postup pro vytváření kódu ve formátu Super HTML.</span><span class="sxs-lookup"><span data-stu-id="4168b-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="4168b-667">Stisknutím klávesy **F5** spusťte řešení a zobrazte obnovenou šablonu.</span><span class="sxs-lookup"><span data-stu-id="4168b-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="4168b-668">Můžete se podívat na následující funkce:</span><span class="sxs-lookup"><span data-stu-id="4168b-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="4168b-669">**Šablony moderního stylu**</span><span class="sxs-lookup"><span data-stu-id="4168b-669">**Modern-style templates**</span></span>

        <span data-ttu-id="4168b-670">Šablony byly obnoveny, což poskytuje další styly pro moderní vzhled.</span><span class="sxs-lookup"><span data-stu-id="4168b-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="4168b-671">![Šablony přeformátované na ASP.NET MVC 4](aspnet-mvc-4-fundamentals/_static/image38.png "Šablony přeformátované na ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="4168b-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="4168b-672">*Šablony přeformátované na ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="4168b-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="4168b-673">**Adaptivní vykreslování**</span><span class="sxs-lookup"><span data-stu-id="4168b-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="4168b-674">Podívejte se na změnu velikosti okna prohlížeče a Všimněte si, jak se rozložení stránky dynamicky přizpůsobí nové velikosti okna.</span><span class="sxs-lookup"><span data-stu-id="4168b-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="4168b-675">Tyto šablony používají techniku adaptivního vykreslování k tomu, aby se správně vykreslily na stolních i mobilních platformách bez jakýchkoli úprav.</span><span class="sxs-lookup"><span data-stu-id="4168b-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="4168b-676">![Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů](aspnet-mvc-4-fundamentals/_static/image39.png "Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů")</span><span class="sxs-lookup"><span data-stu-id="4168b-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="4168b-677">*Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů*</span><span class="sxs-lookup"><span data-stu-id="4168b-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="4168b-678">Zavřete prohlížeč a ukončete ladicí program a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="4168b-679">Nyní se můžete podívat na řešení a vyzkoušet některé nové funkce, které zavedly ASP.NET MVC 4 v šabloně projektu.</span><span class="sxs-lookup"><span data-stu-id="4168b-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="4168b-680">![ASP.NET MVC4-Internet-Application-Project-Template](aspnet-mvc-4-fundamentals/_static/image40.png "Šablona projektu internetové aplikace ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="4168b-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="4168b-681">*Šablona projektu internetové aplikace ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="4168b-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="4168b-682">**Značky HTML5**</span><span class="sxs-lookup"><span data-stu-id="4168b-682">**HTML5 markup**</span></span>

       <span data-ttu-id="4168b-683">Procházejte zobrazením šablon a zjistěte nový kód motivu, například otevřete **o zobrazení. cshtml** v rámci **domovské** složky.</span><span class="sxs-lookup"><span data-stu-id="4168b-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="4168b-684">![Nová šablona s použitím značek Razor a HTML5](aspnet-mvc-4-fundamentals/_static/image41.png "Nová šablona s použitím značek Razor a HTML5")</span><span class="sxs-lookup"><span data-stu-id="4168b-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="4168b-685">*Nová šablona s použitím značek Razor a HTML5*</span><span class="sxs-lookup"><span data-stu-id="4168b-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="4168b-686">**Zahrnuté knihovny JavaScriptu**</span><span class="sxs-lookup"><span data-stu-id="4168b-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="4168b-687">**jQuery**: jQuery zjednodušuje procházení dokumentů HTML, zpracování událostí, animaci a interakce AJAX.</span><span class="sxs-lookup"><span data-stu-id="4168b-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="4168b-688">**uživatelské rozhraní jQuery**: Tato knihovna poskytuje abstrakce pro interakci a animace nízké úrovně, pokročilé efekty a widgety, které jsou postaveny na knihovně JavaScript jQuery.</span><span class="sxs-lookup"><span data-stu-id="4168b-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="4168b-689">Informace o uživatelském rozhraní jQuery a jQuery najdete v [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="4168b-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="4168b-690">**KnockoutJS**: výchozí šablona ASP.NET MVC 4 teď zahrnuje **KnockoutJS**, rozhraní JavaScript MVVM, které umožňuje vytvářet bohatou a vysoce reagující webové aplikace pomocí JavaScriptu a HTML.</span><span class="sxs-lookup"><span data-stu-id="4168b-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="4168b-691">Podobně jako v ASP.NET MVC 3 jsou knihovny rozhraní jQuery a jQuery také součástí ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="4168b-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="4168b-692">Další informace o knihovně KnockOutJS můžete získat v tomto odkazu: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="4168b-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="4168b-693">**Modernizr**: Tato knihovna je spouštěna automaticky, takže při použití technologií HTML5 a CSS3 je váš web kompatibilní se staršími prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="4168b-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="4168b-694">Další informace o knihovně modernizr můžete získat v tomto odkazu: [http://www.modernizr.com/](http://www.modernizr.com/).</span><span class="sxs-lookup"><span data-stu-id="4168b-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="4168b-695">**SimpleMembership zahrnuté v řešení**</span><span class="sxs-lookup"><span data-stu-id="4168b-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="4168b-696">SimpleMembership byl navržen jako náhrada pro předchozí roli ASP.NET a systém poskytovatele členství.</span><span class="sxs-lookup"><span data-stu-id="4168b-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="4168b-697">Má mnoho nových funkcí, které vývojářům usnadňuje zabezpečení webových stránek pružnější způsobem.</span><span class="sxs-lookup"><span data-stu-id="4168b-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="4168b-698">Pro integraci SimpleMembership si už sada internetových šablon nastavila několik věcí, například AccountController se připraví na použití OAuthWebSecurity (pro registraci, přihlašování, správu atd.) a zabezpečení webu pomocí protokolu OAuth.</span><span class="sxs-lookup"><span data-stu-id="4168b-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="4168b-699">![SimpleMembership zahrnuté v řešení](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership zahrnuté v řešení")</span><span class="sxs-lookup"><span data-stu-id="4168b-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="4168b-700">*SimpleMembership zahrnuté v řešení*</span><span class="sxs-lookup"><span data-stu-id="4168b-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="4168b-701">Další informace o [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) najdete na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="4168b-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="4168b-702">Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="4168b-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="4168b-703">Souhrn</span><span class="sxs-lookup"><span data-stu-id="4168b-703">Summary</span></span>

<span data-ttu-id="4168b-704">Vyplněním tohoto praktického cvičení se naučíte základy ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="4168b-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="4168b-705">Základní prvky aplikace MVC a jejich interakce</span><span class="sxs-lookup"><span data-stu-id="4168b-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="4168b-706">Vytvoření aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4168b-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="4168b-707">Postup přidání a konfigurace řadičů pro zpracování parametrů předaných prostřednictvím adresy URL a řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="4168b-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="4168b-708">Postup přidání stránky předlohy rozložení pro nastavení šablony pro běžný obsah HTML, šablony stylů pro vylepšení vzhledu a chování a šablony zobrazení pro zobrazení obsahu HTML</span><span class="sxs-lookup"><span data-stu-id="4168b-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="4168b-709">Jak používat vzor ViewModel pro předávání vlastností do šablony zobrazení, aby se zobrazily dynamické informace</span><span class="sxs-lookup"><span data-stu-id="4168b-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="4168b-710">Použití parametrů předaných řadičům v šabloně zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="4168b-711">Postup přidání odkazů na stránky v aplikaci ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4168b-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="4168b-712">Postup přidání a používání dynamických vlastností v zobrazení</span><span class="sxs-lookup"><span data-stu-id="4168b-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="4168b-713">Vylepšení v šablonách projektů ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="4168b-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="4168b-714">Příloha A: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="4168b-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="4168b-715">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="4168b-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="4168b-716">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="4168b-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="4168b-717">Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="4168b-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="4168b-718">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="4168b-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="4168b-719">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="4168b-719">Click on **Install Now**.</span></span> <span data-ttu-id="4168b-720">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="4168b-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="4168b-721">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="4168b-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="4168b-722">![Nainstalovat Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="4168b-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="4168b-723">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="4168b-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="4168b-724">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="4168b-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="4168b-726">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="4168b-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="4168b-727">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="4168b-727">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="4168b-729">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="4168b-729">*Installation progress*</span></span>
6. <span data-ttu-id="4168b-730">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="4168b-730">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="4168b-732">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="4168b-732">*Installation completed*</span></span>
7. <span data-ttu-id="4168b-733">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="4168b-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="4168b-734">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="4168b-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="4168b-736">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="4168b-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="4168b-737">Příloha B: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="4168b-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="4168b-738">V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="4168b-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="4168b-739">Úloha 1 – Vytvoření nového webu z portálu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="4168b-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="4168b-740">Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="4168b-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-741">S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu.</span><span class="sxs-lookup"><span data-stu-id="4168b-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="4168b-742">[Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="4168b-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="4168b-743">![Přihlaste se k Windows Azure Portal](aspnet-mvc-4-fundamentals/_static/image48.png "Přihlaste se k Windows Azure Portal")</span><span class="sxs-lookup"><span data-stu-id="4168b-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="4168b-744">*Přihlášení k Windows Azure Portál pro správu*</span><span class="sxs-lookup"><span data-stu-id="4168b-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="4168b-745">Na panelu příkazů klikněte na **Nový** .</span><span class="sxs-lookup"><span data-stu-id="4168b-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="4168b-746">![Vytvoření nového webu](aspnet-mvc-4-fundamentals/_static/image49.png "Vytvoření nového webu")</span><span class="sxs-lookup"><span data-stu-id="4168b-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="4168b-747">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="4168b-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="4168b-748">Klikněte na **compute** | **Web**.</span><span class="sxs-lookup"><span data-stu-id="4168b-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="4168b-749">Pak vyberte možnost **rychlé vytvoření** .</span><span class="sxs-lookup"><span data-stu-id="4168b-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="4168b-750">Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.</span><span class="sxs-lookup"><span data-stu-id="4168b-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-751">Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat.</span><span class="sxs-lookup"><span data-stu-id="4168b-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="4168b-752">Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál.</span><span class="sxs-lookup"><span data-stu-id="4168b-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="4168b-753">Nezahrnuje kroky pro nastavení databáze.</span><span class="sxs-lookup"><span data-stu-id="4168b-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="4168b-754">![Vytvoření nového webu pomocí rychlého vytvoření](aspnet-mvc-4-fundamentals/_static/image50.png "Vytvoření nového webu pomocí rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="4168b-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="4168b-755">*Vytvoření nového webu pomocí rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="4168b-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="4168b-756">Počkejte, než se nový **Web** vytvoří.</span><span class="sxs-lookup"><span data-stu-id="4168b-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="4168b-757">Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** .</span><span class="sxs-lookup"><span data-stu-id="4168b-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="4168b-758">Ověřte, zda nový web funguje.</span><span class="sxs-lookup"><span data-stu-id="4168b-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="4168b-759">![Procházení na nový web](aspnet-mvc-4-fundamentals/_static/image51.png "Procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="4168b-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="4168b-760">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="4168b-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="4168b-761">![Běžící Web](aspnet-mvc-4-fundamentals/_static/image52.png "Běžící Web")</span><span class="sxs-lookup"><span data-stu-id="4168b-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="4168b-762">*Běžící Web*</span><span class="sxs-lookup"><span data-stu-id="4168b-762">*Web site running*</span></span>
6. <span data-ttu-id="4168b-763">Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="4168b-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="4168b-764">![Otevření stránek správy webu](aspnet-mvc-4-fundamentals/_static/image53.png "Otevření stránek správy webu")</span><span class="sxs-lookup"><span data-stu-id="4168b-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="4168b-765">*Otevření stránek správy webu*</span><span class="sxs-lookup"><span data-stu-id="4168b-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="4168b-766">Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .</span><span class="sxs-lookup"><span data-stu-id="4168b-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-767">*Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace.</span><span class="sxs-lookup"><span data-stu-id="4168b-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="4168b-768">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace.</span><span class="sxs-lookup"><span data-stu-id="4168b-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="4168b-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="4168b-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="4168b-770">![Stahuje se publikační profil webu.](aspnet-mvc-4-fundamentals/_static/image54.png "Stahuje se publikační profil webu.")</span><span class="sxs-lookup"><span data-stu-id="4168b-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="4168b-771">*Stahuje se publikační profil webu.*</span><span class="sxs-lookup"><span data-stu-id="4168b-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="4168b-772">Stáhněte si soubor profilu publikování do známého umístění.</span><span class="sxs-lookup"><span data-stu-id="4168b-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="4168b-773">V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4168b-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="4168b-774">![Ukládání souboru profilu publikování](aspnet-mvc-4-fundamentals/_static/image55.png "Ukládá se publikační profil.")</span><span class="sxs-lookup"><span data-stu-id="4168b-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="4168b-775">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="4168b-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="4168b-776">Úloha 2 – Konfigurace databázového serveru</span><span class="sxs-lookup"><span data-stu-id="4168b-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="4168b-777">Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="4168b-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="4168b-778">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="4168b-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="4168b-779">Pro uložení aplikační databáze budete potřebovat server SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4168b-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="4168b-780">SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**.</span><span class="sxs-lookup"><span data-stu-id="4168b-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="4168b-781">Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="4168b-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="4168b-782">Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách.</span><span class="sxs-lookup"><span data-stu-id="4168b-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="4168b-783">Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="4168b-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="4168b-784">![Řídicí panel serveru SQL Database](aspnet-mvc-4-fundamentals/_static/image56.png "Řídicí panel serveru SQL Database")</span><span class="sxs-lookup"><span data-stu-id="4168b-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="4168b-785">*Řídicí panel serveru SQL Database*</span><span class="sxs-lookup"><span data-stu-id="4168b-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="4168b-786">V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru.</span><span class="sxs-lookup"><span data-stu-id="4168b-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="4168b-787">Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](aspnet-mvc-4-fundamentals/_static/image57.png).</span><span class="sxs-lookup"><span data-stu-id="4168b-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![Přidává se IP adresa klienta.](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="4168b-789">*Přidává se IP adresa klienta.*</span><span class="sxs-lookup"><span data-stu-id="4168b-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="4168b-790">Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="4168b-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrdit změny](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="4168b-792">*Potvrdit změny*</span><span class="sxs-lookup"><span data-stu-id="4168b-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="4168b-793">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="4168b-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="4168b-794">Vraťte se do řešení ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="4168b-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="4168b-795">V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="4168b-796">![Publikování aplikace](aspnet-mvc-4-fundamentals/_static/image60.png "Publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="4168b-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="4168b-797">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="4168b-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="4168b-798">Importujte profil publikování, který jste uložili v prvním úkolu.</span><span class="sxs-lookup"><span data-stu-id="4168b-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="4168b-799">![Import profilu publikování](aspnet-mvc-4-fundamentals/_static/image61.png "Import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="4168b-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="4168b-800">*Importuje se publikační profil.*</span><span class="sxs-lookup"><span data-stu-id="4168b-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="4168b-801">Klikněte na **ověřit připojení**.</span><span class="sxs-lookup"><span data-stu-id="4168b-801">Click **Validate Connection**.</span></span> <span data-ttu-id="4168b-802">Po dokončení ověřování klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="4168b-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4168b-803">Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="4168b-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="4168b-804">![Ověřování připojení](aspnet-mvc-4-fundamentals/_static/image62.png "Ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="4168b-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="4168b-805">*Ověřování připojení*</span><span class="sxs-lookup"><span data-stu-id="4168b-805">*Validating connection*</span></span>
4. <span data-ttu-id="4168b-806">Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="4168b-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="4168b-807">![Konfigurace nasazení webu](aspnet-mvc-4-fundamentals/_static/image63.png "Konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="4168b-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="4168b-808">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="4168b-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="4168b-809">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="4168b-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="4168b-810">Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="4168b-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="4168b-811">V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="4168b-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="4168b-812">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="4168b-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="4168b-813">Zadejte nový název databáze, například: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="4168b-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="4168b-814">![Konfigurace cílového připojovacího řetězce](aspnet-mvc-4-fundamentals/_static/image64.png "Konfigurace cílového připojovacího řetězce")</span><span class="sxs-lookup"><span data-stu-id="4168b-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="4168b-815">*Konfigurace cílového připojovacího řetězce*</span><span class="sxs-lookup"><span data-stu-id="4168b-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="4168b-816">Pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="4168b-816">Then click **OK**.</span></span> <span data-ttu-id="4168b-817">Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="4168b-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="4168b-818">![Vytvoření databáze](aspnet-mvc-4-fundamentals/_static/image65.png "Vytváří se řetězec databáze.")</span><span class="sxs-lookup"><span data-stu-id="4168b-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="4168b-819">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="4168b-819">*Creating the database*</span></span>
7. <span data-ttu-id="4168b-820">Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení.</span><span class="sxs-lookup"><span data-stu-id="4168b-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="4168b-821">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="4168b-821">Then click **Next**.</span></span>

    <span data-ttu-id="4168b-822">![Připojovací řetězec ukazující na SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Připojovací řetězec ukazující na SQL Database")</span><span class="sxs-lookup"><span data-stu-id="4168b-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="4168b-823">*Připojovací řetězec ukazující na SQL Database*</span><span class="sxs-lookup"><span data-stu-id="4168b-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="4168b-824">Na stránce **Náhled** klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="4168b-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="4168b-825">![Publikování webové aplikace](aspnet-mvc-4-fundamentals/_static/image67.png "Publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="4168b-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="4168b-826">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="4168b-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="4168b-827">Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.</span><span class="sxs-lookup"><span data-stu-id="4168b-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="4168b-828">![Aplikace byla publikována na platformě Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Aplikace byla publikována na platformě Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="4168b-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="4168b-829">*Aplikace byla publikována na platformě Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="4168b-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="4168b-830">Příloha C: používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="4168b-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="4168b-831">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="4168b-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="4168b-832">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="4168b-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="4168b-833">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-fundamentals/_static/image69.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="4168b-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="4168b-834">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="4168b-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="4168b-835">***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="4168b-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="4168b-836">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="4168b-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="4168b-837">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="4168b-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="4168b-838">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="4168b-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="4168b-839">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="4168b-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="4168b-840">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="4168b-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="4168b-841">![Začněte psát název fragmentu.](aspnet-mvc-4-fundamentals/_static/image70.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="4168b-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="4168b-842">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="4168b-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="4168b-843">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-fundamentals/_static/image71.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="4168b-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="4168b-844">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="4168b-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="4168b-845">![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-fundamentals/_static/image72.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="4168b-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="4168b-846">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="4168b-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="4168b-847">***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první.</span><span class="sxs-lookup"><span data-stu-id="4168b-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="4168b-848">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="4168b-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="4168b-849">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="4168b-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="4168b-850">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="4168b-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="4168b-851">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-fundamentals/_static/image73.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="4168b-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="4168b-852">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="4168b-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="4168b-853">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-fundamentals/_static/image74.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="4168b-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="4168b-854">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="4168b-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
