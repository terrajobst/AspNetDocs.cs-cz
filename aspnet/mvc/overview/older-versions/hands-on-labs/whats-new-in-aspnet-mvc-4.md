---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: Co je nového v ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 je architektura pro vytváření škálovatelných webových aplikací založených na standardech pomocí dobře zavedených vzorů návrhu a síly ASP.NET a...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539436"
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="af6f1-103">Novinky v ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="af6f1-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="af6f1-104">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="af6f1-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="af6f1-105">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="af6f1-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="af6f1-106">ASP.NET MVC 4 je architektura pro vytváření škálovatelných webových aplikací založených na standardech pomocí dobře zavedených vzorů návrhu a síly ASP.NET a rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="af6f1-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="af6f1-107">Tato nová, čtvrtá verze rozhraní se zaměřuje na snazší vývoj mobilních webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="af6f1-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="af6f1-108">Pokud chcete začít s, při vytváření nového projektu ASP.NET MVC 4 je teď šablona projektu mobilní aplikace, kterou můžete použít k vytvoření samostatné aplikace speciálně pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="af6f1-109">Kromě toho ASP.NET MVC 4 integruje s jQuery Mobile prostřednictvím balíčku NuGet jQuery. Mobile. MVC.</span><span class="sxs-lookup"><span data-stu-id="af6f1-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="af6f1-110">jQuery Mobile je architektura založená na HTML5 pro vývoj webových aplikací, které jsou kompatibilní se všemi oblíbenými platformami mobilních zařízení, včetně Windows Phone, iPhone, Androidu a tak dále.</span><span class="sxs-lookup"><span data-stu-id="af6f1-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="af6f1-111">Pokud však budete potřebovat specializaci, ASP.NET MVC 4 také umožňuje obsluhovat různá zobrazení různých zařízení a poskytovat optimalizace pro konkrétní zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="af6f1-112">V tomto praktickém cvičení začnete s ASP.NET MVC 4 &quot;Internet Application&quot; šablona projektu pro vytvoření aplikace Fotogalerie.</span><span class="sxs-lookup"><span data-stu-id="af6f1-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="af6f1-113">Pomocí nových funkcí jQuery Mobile a ASP.NET MVC 4 budete aplikaci postupně rozšiřovat, aby byla kompatibilní s různými mobilními zařízeními a webovými prohlížeči pro stolní počítače.</span><span class="sxs-lookup"><span data-stu-id="af6f1-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="af6f1-114">Naučíte se také nové složení kódu pro generování kódu a to, jak ASP.NET MVC 4 usnadňuje psaní asynchronních metod akcí díky podpoře úloh&lt;ActionResult&gt; návratových typů.</span><span class="sxs-lookup"><span data-stu-id="af6f1-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="af6f1-115">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="af6f1-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="af6f1-116">Projekt, který je specifický pro toto testovací prostředí, je k dispozici v části [novinky webových formulářů v ASP.NET 4,5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span><span class="sxs-lookup"><span data-stu-id="af6f1-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="af6f1-117">Cíle</span><span class="sxs-lookup"><span data-stu-id="af6f1-117">Objectives</span></span>

<span data-ttu-id="af6f1-118">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="af6f1-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="af6f1-119">Využijte výhod vylepšení šablon projektů ASP.NET MVC – včetně nové šablony projektu mobilní aplikace</span><span class="sxs-lookup"><span data-stu-id="af6f1-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="af6f1-120">Použití atributů zobrazení HTML5 a dotazů na média šablon stylů CSS ke zlepšení zobrazení na mobilních zařízeních</span><span class="sxs-lookup"><span data-stu-id="af6f1-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="af6f1-121">Použití jQuery Mobile pro progresivní vylepšení a vytváření webového uživatelského rozhraní optimalizovaného pro dotykové ovládání</span><span class="sxs-lookup"><span data-stu-id="af6f1-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="af6f1-122">Vytváření zobrazení specifických pro mobilní zařízení</span><span class="sxs-lookup"><span data-stu-id="af6f1-122">Create mobile-specific views</span></span>
- <span data-ttu-id="af6f1-123">Přepínání mezi zobrazeními mobilních a desktopových aplikací v aplikaci pomocí součásti pro přepínání zobrazení</span><span class="sxs-lookup"><span data-stu-id="af6f1-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="af6f1-124">Vytváření asynchronních řadičů pomocí podpory úloh</span><span class="sxs-lookup"><span data-stu-id="af6f1-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="af6f1-125">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="af6f1-125">Prerequisites</span></span>

<span data-ttu-id="af6f1-126">K dokončení tohoto testovacího prostředí musíte mít následující položky:</span><span class="sxs-lookup"><span data-stu-id="af6f1-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="af6f1-127">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nejvyšší (pokyny k instalaci najdete v [příloze B](#AppendixB) ).</span><span class="sxs-lookup"><span data-stu-id="af6f1-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="af6f1-128">[ASP.NET MVC 4](../../../mvc4.md) (zahrnuté v instalaci Microsoft Visual Studio 2012)</span><span class="sxs-lookup"><span data-stu-id="af6f1-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="af6f1-129">Emulátor Windows Phone (zahrnutý v [sadě Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span><span class="sxs-lookup"><span data-stu-id="af6f1-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="af6f1-130">Volitelné – [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) s **elektrickým rozšířením simulátoru Plum iPhone** (jenom pro cvičení 3 používá se k procházení webové aplikace pomocí simulátoru iPhone)</span><span class="sxs-lookup"><span data-stu-id="af6f1-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="af6f1-131">Nastavení</span><span class="sxs-lookup"><span data-stu-id="af6f1-131">Setup</span></span>

<span data-ttu-id="af6f1-132">V celém dokumentu testovacího prostředí budete vyzváni k vložení bloků kódu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="af6f1-133">Pro usnadnění práce je většina tohoto kódu poskytována jako fragmenty Visual Studio Code, které můžete použít v rámci sady Visual Studio, abyste se vyhnuli nutnosti je přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="af6f1-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="af6f1-134">Instalace fragmentů kódu:</span><span class="sxs-lookup"><span data-stu-id="af6f1-134">To install the code snippets:</span></span>

1. <span data-ttu-id="af6f1-135">Otevřete okno Průzkumníka Windows a přejděte do složky **Source\Setup** testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="af6f1-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="af6f1-136">Dvojím kliknutím na soubor **Setup. cmd** v této složce nainstalujete fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6f1-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="af6f1-137">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze A: používání fragmentů kódu](#AppendixA)&quot;.</span><span class="sxs-lookup"><span data-stu-id="af6f1-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="af6f1-138">Cvičení</span><span class="sxs-lookup"><span data-stu-id="af6f1-138">Exercises</span></span>

<span data-ttu-id="af6f1-139">Tato praktická cvičení zahrnují následující cvičení:</span><span class="sxs-lookup"><span data-stu-id="af6f1-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="af6f1-140">Nové šablony projektů ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="af6f1-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="af6f1-141">Vytvoření webové aplikace Galerie fotografií</span><span class="sxs-lookup"><span data-stu-id="af6f1-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="af6f1-142">Přidání podpory pro mobilní zařízení</span><span class="sxs-lookup"><span data-stu-id="af6f1-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="af6f1-143">Použití asynchronních řadičů</span><span class="sxs-lookup"><span data-stu-id="af6f1-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="af6f1-144">Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="af6f1-145">Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="af6f1-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="af6f1-146">Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="af6f1-147">Cvičení 1: nové šablony projektů ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="af6f1-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="af6f1-148">V tomto cvičení budete zkoumat vylepšení v šablonách projektů ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="af6f1-149">Kromě šablony internetové aplikace, která je již přítomna v MVC 3, tato verze nyní obsahuje samostatnou šablonu pro mobilní aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="af6f1-150">Nejprve se podíváte na některé relevantní funkce každé z těchto šablon.</span><span class="sxs-lookup"><span data-stu-id="af6f1-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="af6f1-151">Pak budete pracovat s tím, jak správně vykreslovat stránku na různých platformách, pomocí správného přístupu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="af6f1-152">Úloha 1 – prozkoumání šablony internetové aplikace</span><span class="sxs-lookup"><span data-stu-id="af6f1-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="af6f1-153">Otevřete **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="af6f1-154">Vyberte **soubor | Nové |** Příkaz nabídky projektu</span><span class="sxs-lookup"><span data-stu-id="af6f1-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="af6f1-155">V dialogovém okně **Nový projekt** vyberte **vizuál C# | Webová** šablona ve stromu levého podokna a výběr **webové aplikace ASP.NET MVC 4.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="af6f1-156">Pojmenujte **fotogalerii**projektů, vyberte umístění (nebo ponechte výchozí) a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-157">Později budete přizpůsobovat fotogalerii ASP.NET řešení MVC 4, které teď vytváříte.</span><span class="sxs-lookup"><span data-stu-id="af6f1-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="af6f1-158">![Vytvoření nového projektu](whats-new-in-aspnet-mvc-4/_static/image1.png "Vytvoření nového projektu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="af6f1-159">*Vytvoření nového projektu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-159">*Creating a new project*</span></span>
3. <span data-ttu-id="af6f1-160">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **Internetová aplikace** a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="af6f1-161">Ujistěte se, že jste vybrali Razor jako zobrazovací modul.</span><span class="sxs-lookup"><span data-stu-id="af6f1-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="af6f1-162">![Vytváří se nová internetová aplikace ASP.NET MVC 4.](whats-new-in-aspnet-mvc-4/_static/image2.png "Vytváří se nová internetová aplikace ASP.NET MVC 4.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="af6f1-163">*Vytváří se nová internetová aplikace ASP.NET MVC 4.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-164">Syntaxe Razor byla představena v ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="af6f1-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="af6f1-165">Jeho cílem je minimalizovat počet znaků a klávesových úhozů vyžadovaných v souboru a povolit tak rychlé a kapalné pracovní postupy v kódování.</span><span class="sxs-lookup"><span data-stu-id="af6f1-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="af6f1-166">Razor využívá stávající C# jazykové dovednosti/vb (nebo jiné) a poskytuje syntaxi značek šablony, která umožňuje pracovní postup pro vytváření kódu ve formátu Super HTML.</span><span class="sxs-lookup"><span data-stu-id="af6f1-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="af6f1-167">Stisknutím klávesy **F5** spusťte řešení a zobrazte obnovené šablony.</span><span class="sxs-lookup"><span data-stu-id="af6f1-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="af6f1-168">Můžete se podívat na následující funkce:</span><span class="sxs-lookup"><span data-stu-id="af6f1-168">You can check out the following features:</span></span>

    <span data-ttu-id="af6f1-169">**Šablony moderního stylu**</span><span class="sxs-lookup"><span data-stu-id="af6f1-169">**Modern-style templates**</span></span>

    <span data-ttu-id="af6f1-170">Šablony byly obnoveny, což poskytuje další styly pro moderní vzhled.</span><span class="sxs-lookup"><span data-stu-id="af6f1-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="af6f1-171">![Šablony přeformátované na ASP.NET MVC 4](whats-new-in-aspnet-mvc-4/_static/image3.png "Šablony s přestylem MVC 4")</span><span class="sxs-lookup"><span data-stu-id="af6f1-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="af6f1-172">*Šablony přeformátované na ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="af6f1-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="af6f1-173">![Nová stránka kontaktu](whats-new-in-aspnet-mvc-4/_static/image4.png "Nová stránka kontaktu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="af6f1-174">*Nová stránka kontaktu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-174">*New Contact page*</span></span>

    <span data-ttu-id="af6f1-175">**Adaptivní vykreslování**</span><span class="sxs-lookup"><span data-stu-id="af6f1-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="af6f1-176">Podívejte se na změnu velikosti okna prohlížeče a Všimněte si, jak se rozložení stránky dynamicky přizpůsobí nové velikosti okna.</span><span class="sxs-lookup"><span data-stu-id="af6f1-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="af6f1-177">Tyto šablony používají techniku adaptivního vykreslování k tomu, aby se správně vykreslily na stolních i mobilních platformách bez jakýchkoli úprav.</span><span class="sxs-lookup"><span data-stu-id="af6f1-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="af6f1-178">![Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů](whats-new-in-aspnet-mvc-4/_static/image5.png "Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů")</span><span class="sxs-lookup"><span data-stu-id="af6f1-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="af6f1-179">*Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů*</span><span class="sxs-lookup"><span data-stu-id="af6f1-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="af6f1-180">**Bohatší uživatelské rozhraní s JavaScriptem**</span><span class="sxs-lookup"><span data-stu-id="af6f1-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="af6f1-181">Dalším vylepšením výchozích šablon projektů je použití JavaScriptu k poskytnutí interaktivního JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="af6f1-182">Odkazy na přihlášení a registraci použité v šabloně exemplify, jak použít ověřování jQuery k ověření vstupních polí ze strany klienta.</span><span class="sxs-lookup"><span data-stu-id="af6f1-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![Ověření jQuery](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="af6f1-184">*Ověření jQuery*</span><span class="sxs-lookup"><span data-stu-id="af6f1-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-185">Všimněte si dvou částí přihlášení. v první části se můžete přihlásit pomocí registrovaného účtu z lokality a v druhé části se můžete přihlásit pomocí jiné ověřovací služby, jako je Google (ve výchozím nastavení vypnuté).</span><span class="sxs-lookup"><span data-stu-id="af6f1-185">Notice the two log in sections, in the first section you can log in using a registered account from the site and in the second section you can alternatively log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="af6f1-186">Zavřete prohlížeč a ukončete ladicí program a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6f1-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="af6f1-187">Otevřete soubor **authconfig.cs** umístěný ve složce **App\_Start** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="af6f1-188">Odebráním komentáře z posledního řádku zaregistrujete klienta Google pro ověřování *OAuth* .</span><span class="sxs-lookup"><span data-stu-id="af6f1-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="af6f1-189">Všimněte si, že můžete snadno povolit ověřování pomocí kterékoli služby OpenID nebo OAuth, jako je Facebook, Twitter, Microsoft atd.</span><span class="sxs-lookup"><span data-stu-id="af6f1-189">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="af6f1-190">Stisknutím klávesy **F5** spusťte řešení a přejděte na přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="af6f1-190">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="af6f1-191">Vyberte službu **Google** , abyste se mohli přihlásit.</span><span class="sxs-lookup"><span data-stu-id="af6f1-191">Select **Google** service to log in.</span></span>

    ![Výběr služby přihlášení](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="af6f1-193">*Výběr služby přihlášení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-193">*Selecting the log in service*</span></span>
10. <span data-ttu-id="af6f1-194">Přihlaste se pomocí svého účtu Google.</span><span class="sxs-lookup"><span data-stu-id="af6f1-194">Log in using your Google account.</span></span>
11. <span data-ttu-id="af6f1-195">Povolí, aby lokalita (localhost) načetla informace z účtu Google.</span><span class="sxs-lookup"><span data-stu-id="af6f1-195">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="af6f1-196">Nakonec se budete muset zaregistrovat na webu a přidružit k účtu Google.</span><span class="sxs-lookup"><span data-stu-id="af6f1-196">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![Přidružte svůj účet Google.](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="af6f1-198">*Přidruží se Váš účet Google.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-198">*Associating your Google account*</span></span>
13. <span data-ttu-id="af6f1-199">Zavřete prohlížeč a ukončete ladicí program a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6f1-199">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="af6f1-200">Nyní Prozkoumejte řešení a podívejte se na některé další nové funkce, které byly zavedeny ASP.NET MVC 4 v šabloně projektu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-200">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="af6f1-201">![Šablona projektu internetové aplikace ASP.NET MVC 4](whats-new-in-aspnet-mvc-4/_static/image9.png "Šablona projektu internetové aplikace ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="af6f1-201">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="af6f1-202">*Šablona projektu internetové aplikace ASP.NET MVC 4*</span><span class="sxs-lookup"><span data-stu-id="af6f1-202">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

    - <span data-ttu-id="af6f1-203">**HTML 5 – označení**</span><span class="sxs-lookup"><span data-stu-id="af6f1-203">**HTML 5 Markup**</span></span>

       <span data-ttu-id="af6f1-204">Procházejte zobrazením šablon a zjistěte nový kód motivu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-204">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="af6f1-205">![Nová šablona s použitím značek Razor a HTML5 o. cshtml](whats-new-in-aspnet-mvc-4/_static/image10.png "Nová šablona s použitím značek Razor a HTML5 o. cshtml")</span><span class="sxs-lookup"><span data-stu-id="af6f1-205">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="af6f1-206">*Nová šablona s použitím značek Razor a HTML5 (About. cshtml).*</span><span class="sxs-lookup"><span data-stu-id="af6f1-206">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
    - <span data-ttu-id="af6f1-207">**Aktualizované knihovny JavaScriptu**</span><span class="sxs-lookup"><span data-stu-id="af6f1-207">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="af6f1-208">Výchozí šablona ASP.NET MVC 4 nyní zahrnuje KnockoutJS, MVVM rozhraní JavaScript, které umožňuje vytvářet bohatě a vysoce reagující webové aplikace pomocí JavaScriptu a HTML.</span><span class="sxs-lookup"><span data-stu-id="af6f1-208">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="af6f1-209">Podobně jako v knihovnách uživatelského rozhraní MVC3, jQuery a jQuery jsou také zahrnuty v ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-209">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="af6f1-210">Další informace o knihovně KnockOutJS můžete získat v tomto odkazu: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="af6f1-210">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="af6f1-211">Kromě toho se můžete dozvědět o uživatelském rozhraní jQuery a jQuery v [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="af6f1-211">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="af6f1-212">Úloha 2 – prozkoumání šablony mobilní aplikace</span><span class="sxs-lookup"><span data-stu-id="af6f1-212">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="af6f1-213">ASP.NET MVC 4 usnadňuje vývoj webů pro mobilní a tabletové prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="af6f1-213">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="af6f1-214">Tato šablona má stejnou strukturu aplikace jako šablona internetové aplikace (Všimněte si, že kód kontroleru je prakticky identický), ale jeho styl byl upravený tak, aby se správně vykreslil v mobilních zařízeních na bázi dotykového ovládání.</span><span class="sxs-lookup"><span data-stu-id="af6f1-214">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="af6f1-215">Vyberte **soubor | Nové |** Příkaz nabídky projektu</span><span class="sxs-lookup"><span data-stu-id="af6f1-215">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="af6f1-216">V dialogovém okně **Nový projekt** vyberte **vizuál C# | Webová** šablona ve stromu levého podokna a volba **webové aplikace ASP.NET MVC 4.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-216">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="af6f1-217">Pojmenujte projekt **Fotogalerie. Mobile**, vyberte umístění (nebo ponechte výchozí), vyberte &quot;přidat do řešení&quot; a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-217">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="af6f1-218">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **mobilní aplikace** a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-218">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="af6f1-219">Ujistěte se, že jste vybrali Razor jako zobrazovací modul.</span><span class="sxs-lookup"><span data-stu-id="af6f1-219">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="af6f1-220">![Vytváří se nová mobilní aplikace ASP.NET MVC 4.](whats-new-in-aspnet-mvc-4/_static/image11.png "Vytváří se nová mobilní aplikace ASP.NET MVC 4.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-220">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="af6f1-221">*Vytváří se nová mobilní aplikace ASP.NET MVC 4.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-221">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="af6f1-222">Nyní můžete prozkoumat řešení a zjistit některé nové funkce, které zavedla šablona řešení ASP.NET MVC 4 pro mobilní zařízení:</span><span class="sxs-lookup"><span data-stu-id="af6f1-222">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="af6f1-223">**Knihovna jQuery Mobile**</span><span class="sxs-lookup"><span data-stu-id="af6f1-223">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="af6f1-224">Šablona projektu mobilní aplikace zahrnuje knihovnu jQuery Mobile Library, což je open source knihovna pro kompatibilitu s mobilním prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="af6f1-224">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="af6f1-225">jQuery Mobile používá progresivní rozšíření pro mobilní prohlížeče, které podporují šablony stylů CSS a JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af6f1-225">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="af6f1-226">Progresivní navýšení umožňuje všem prohlížečům zobrazovat základní obsah webové stránky, ale umožňuje jenom nejvýkonnějším prohlížečům zobrazit bohatou obsah.</span><span class="sxs-lookup"><span data-stu-id="af6f1-226">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="af6f1-227">Soubory jazyka JavaScript a CSS, které jsou součástí stylu jQuery Mobile, umožňují mobilním prohlížečům přizpůsobení obsahu na obrazovce, aniž by bylo nutné provádět změny v kódu stránky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-227">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="af6f1-229">*Knihovna jQuery Mobile obsažená v šabloně*</span><span class="sxs-lookup"><span data-stu-id="af6f1-229">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="af6f1-230">**Kód založený na HTML5**</span><span class="sxs-lookup"><span data-stu-id="af6f1-230">**HTML5 based markup**</span></span>

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="af6f1-232">*Šablona mobilní aplikace pomocí značek HTML5 (login. cshtml a index. cshtml)*</span><span class="sxs-lookup"><span data-stu-id="af6f1-232">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="af6f1-233">Stisknutím klávesy **F5** spusťte řešení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-233">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="af6f1-234">Otevřete **emulátor Windows Phone 7**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-234">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="af6f1-235">Na obrazovce Start telefonu otevřete Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="af6f1-235">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="af6f1-236">Podívejte se na adresu URL, kde byla spuštěna aplikace klasické pracovní plochy, a přejděte na tuto adresu URL z telefonu (např. `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="af6f1-236">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="af6f1-237">Nyní je možné zadat přihlašovací stránku nebo se podívat na stránku o službě.</span><span class="sxs-lookup"><span data-stu-id="af6f1-237">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="af6f1-238">Všimněte si, že styl webu je založený na nové aplikaci Metro pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-238">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="af6f1-239">Šablona projektu ASP.NET MVC 4 je na mobilních zařízeních správně zobrazena a zajišťuje, aby všechny prvky stránky byly viditelné a povolené.</span><span class="sxs-lookup"><span data-stu-id="af6f1-239">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="af6f1-240">Všimněte si, že odkazy v hlavičce jsou dostatečně velké, aby je bylo možné kliknout nebo klepnout na tlačítko.</span><span class="sxs-lookup"><span data-stu-id="af6f1-240">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="af6f1-241">![Stránky šablon projektů v mobilním zařízení](whats-new-in-aspnet-mvc-4/_static/image14.png "Stránky šablon projektů v mobilním zařízení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-241">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="af6f1-242">*Stránky šablon projektů v mobilním zařízení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-242">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="af6f1-243">Nová šablona používá také **zobrazovací značku meta**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-243">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="af6f1-244">Většina mobilních prohlížečů definuje šířku pro okno virtuálního prohlížeče nebo &quot;zobrazení&quot;, což je větší než skutečná šířka mobilního zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-244">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="af6f1-245">To umožňuje mobilním prohlížečům zobrazit celou webovou stránku uvnitř virtuálního zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-245">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="af6f1-246">**Značka meta zobrazení** umožňuje webovým vývojářům nastavit šířku, výšku a měřítko oblasti prohlížeče na mobilních zařízeních **.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-246">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="af6f1-247">Šablona ASP.NET MVC 4 pro mobilní aplikace nastaví zobrazení na šířku zařízení (&quot;Width =&quot;šířka zařízení) v šabloně rozložení (*Views\Shared\_layout. cshtml*), takže všechny stránky budou mít nastavené zobrazení na šířku obrazovky zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-247">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="af6f1-248">Všimněte si, že značka meta zobrazení nebude měnit výchozí zobrazení prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="af6f1-248">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="af6f1-249">Otevřete **\_layout. cshtml**, umístěný v **zobrazeních | Sdílená** složka a přikomentujte meta značce zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-249">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="af6f1-250">Spusťte aplikaci, pokud ještě není spuštěná, a podívejte se na rozdíly.</span><span class="sxs-lookup"><span data-stu-id="af6f1-250">Run the application, if not already opened, and check out the differences.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

<span data-ttu-id="af6f1-251">![Lokalita po přidání komentáře k meta značce zobrazení](whats-new-in-aspnet-mvc-4/_static/image15.png "Lokalita po přidání komentáře k meta značce zobrazení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-251">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

<span data-ttu-id="af6f1-252">*Lokalita po přidání komentáře k meta značce zobrazení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-252">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="af6f1-253">V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-253">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="af6f1-254">Odkomentujte metaznačku zobrazení značek.</span><span class="sxs-lookup"><span data-stu-id="af6f1-254">Uncomment the viewport meta tag.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="af6f1-255">Úloha 3 – použití adaptivního vykreslování</span><span class="sxs-lookup"><span data-stu-id="af6f1-255">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="af6f1-256">V této úloze se naučíte, jak na mobilních zařízeních a webových prohlížečích správně vykreslit webovou stránku bez jakéhokoli přizpůsobení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-256">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="af6f1-257">Již jste použili značku meta zobrazení s podobným účelem.</span><span class="sxs-lookup"><span data-stu-id="af6f1-257">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="af6f1-258">Nyní budete vyhovovat další výkonné metodě: *adaptivní vykreslování*.</span><span class="sxs-lookup"><span data-stu-id="af6f1-258">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="af6f1-259">Adaptivní vykreslování je technika, která používá **CSS3 multimediální dotazy** k přizpůsobení stylu použitému pro stránku.</span><span class="sxs-lookup"><span data-stu-id="af6f1-259">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="af6f1-260">Dotazy na multimédia definují podmínky v šabloně stylů a seskupují CSS styly pod určitou podmínkou.</span><span class="sxs-lookup"><span data-stu-id="af6f1-260">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="af6f1-261">Pouze v případě, že je podmínka pravdivá, je styl aplikován na deklarované objekty.</span><span class="sxs-lookup"><span data-stu-id="af6f1-261">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="af6f1-262">Flexibilita poskytovaná technikou adaptivního vykreslování umožňuje libovolné přizpůsobení zobrazení webu na různých zařízeních.</span><span class="sxs-lookup"><span data-stu-id="af6f1-262">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="af6f1-263">Můžete definovat tolik stylů, kolik chcete pro jednu šablonu stylů, aniž byste museli psát kód logiky pro výběr stylu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-263">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="af6f1-264">Proto je velmi úhledný způsob přizpůsobení stylů stránky, protože snižuje množství duplicitního kódu a logiky pro účely vykreslování.</span><span class="sxs-lookup"><span data-stu-id="af6f1-264">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="af6f1-265">Na druhé straně by se zvýšila spotřeba šířky pásma, protože velikost souborů CSS by mohla růst na okrajích.</span><span class="sxs-lookup"><span data-stu-id="af6f1-265">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="af6f1-266">Pomocí techniky adaptivního vykreslování se vaše lokalita **zobrazí správně, bez ohledu na prohlížeč.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-266">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="af6f1-267">Měli byste se však vzít v úvahu i v případě, že je větší zatížení šířky pásma velmi důležité.</span><span class="sxs-lookup"><span data-stu-id="af6f1-267">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="af6f1-268">Základní formát dotazu na média je: @media \[oboru: vše | Handheld | Tisk | projekce |\] obrazovky ([vlastnost: hodnota] a... [vlastnost: hodnota])</span><span class="sxs-lookup"><span data-stu-id="af6f1-268">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>

<span data-ttu-id="af6f1-269">Příklady dotazů na média: &gt; **@media All a (max-width: 1000px) a (min-width: 700px) {}:** pro všechna rozlišení mezi 700px a 1000px.</span><span class="sxs-lookup"><span data-stu-id="af6f1-269">Examples of media queries: &gt;**@media all and (max-width: 1000px) and (min-width: 700px) {}:** For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="af6f1-270">**@media obrazovka a (minimální šířka: 400px) a (max-width: 700px) {...}:** Pouze pro obrazovky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-270">**@media screen and (min-width: 400px) and (max-width: 700px) { ... }:** Only for screens.</span></span> <span data-ttu-id="af6f1-271">Rozlišení musí být mezi 400 a 700px.</span><span class="sxs-lookup"><span data-stu-id="af6f1-271">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="af6f1-272">**@media handheld a (minimální šířka: 20em), obrazovka a (minimální šířka: 20em) {...}:** Pro handheldy (mobilní zařízení a zařízení) a obrazovky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-272">**@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:** For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="af6f1-273">Minimální šířka musí být větší než 20em.</span><span class="sxs-lookup"><span data-stu-id="af6f1-273">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="af6f1-274">Další informace najdete na [webu W3C](http://www.w3.org/TR/css3-mediaqueries/).</span><span class="sxs-lookup"><span data-stu-id="af6f1-274">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>

<span data-ttu-id="af6f1-275">Nyní si prozkoumáte, jak adaptivní vykreslování funguje, a zlepšuje čitelnost šablony výchozích webů ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-275">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="af6f1-276">Otevřete řešení **fotogallery. sln** , které jste vytvořili v úloze 1, a vyberte projekt **Galerie** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-276">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="af6f1-277">Stisknutím klávesy **F5** spusťte řešení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-277">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="af6f1-278">Změňte velikost šířky prohlížeče a nastavte Windows na polovinu nebo méně, než je čtvrtina původní velikosti.</span><span class="sxs-lookup"><span data-stu-id="af6f1-278">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="af6f1-279">Všimněte si, co se stane s položkami v hlavičce: některé prvky se nezobrazí v oblasti viditelné v hlavičce.</span><span class="sxs-lookup"><span data-stu-id="af6f1-279">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="af6f1-280">V Průzkumníku řešení sady Visual Studio otevřete soubor **Web. CSS** , který se nachází ve složce projektu **obsahu** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-280">Open **Site.css** file from the Visual Studio Solution explorer, located in **Content** project folder.</span></span> <span data-ttu-id="af6f1-281">Stisknutím **kombinace kláves CTRL + F** otevřete integrované vyhledávání sady Visual Studio a napíšete `@media` a vyhledejte **mediální dotaz CSS**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-281">Press **CTRL + F** to open Visual Studio integrated search, and write `@media` to locate the **CSS media query**.</span></span>

    <span data-ttu-id="af6f1-282">Podmínka pro dotaz na multimédia definovaná v této šabloně funguje tímto způsobem: když velikost okna prohlížeče je pod **850 px**, použijí se pravidla CSS definovaná v tomto bloku médií.</span><span class="sxs-lookup"><span data-stu-id="af6f1-282">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="af6f1-283">![Hledání multimediálního dotazu](whats-new-in-aspnet-mvc-4/_static/image16.png "Hledání multimediálního dotazu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-283">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="af6f1-284">*Hledání multimediálního dotazu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-284">*Locating the media query*</span></span>
4. <span data-ttu-id="af6f1-285">Nahraďte hodnotu atributu max-width nastavenou v 850 px hodnotou **10px**, abyste mohli zakázat adaptivní vykreslování, a stisknutím **kláves CTRL + S** uložte změny.</span><span class="sxs-lookup"><span data-stu-id="af6f1-285">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="af6f1-286">Vraťte se do prohlížeče a stisknutím **kláves CTRL + F5** aktualizujte stránku se změnami, které jste provedli.</span><span class="sxs-lookup"><span data-stu-id="af6f1-286">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="af6f1-287">Všimněte si rozdílů na obou stránkách při úpravách šířky okna.</span><span class="sxs-lookup"><span data-stu-id="af6f1-287">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="af6f1-288">![Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.](whats-new-in-aspnet-mvc-4/_static/image17.png "Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="af6f1-289">*Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-289">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="af6f1-290">Teď se podívejme na to, co se stane na mobilních zařízeních:</span><span class="sxs-lookup"><span data-stu-id="af6f1-290">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="af6f1-291">![Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.](whats-new-in-aspnet-mvc-4/_static/image18.png "Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-291">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="af6f1-292">*Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-292">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="af6f1-293">I když si všimnete, že změny při vykreslování stránky ve webovém prohlížeči nejsou velmi důležité, při použití mobilního zařízení se rozdíly stanou jasnější.</span><span class="sxs-lookup"><span data-stu-id="af6f1-293">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="af6f1-294">Na levé straně obrázku vidíte, že vlastní styl zlepšil čitelnost.</span><span class="sxs-lookup"><span data-stu-id="af6f1-294">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="af6f1-295">Adaptivní vykreslování lze použít v mnoha dalších scénářích, což usnadňuje použití podmíněného stylování na webu a řešení běžných potíží se styly s úhledným přístupem.</span><span class="sxs-lookup"><span data-stu-id="af6f1-295">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="af6f1-296">Metadata zobrazení a dotazy na média šablony stylů CSS nejsou specifické pro ASP.NET MVC 4, takže můžete tyto funkce využít v libovolné webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="af6f1-296">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="af6f1-297">V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-297">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="af6f1-298">Cvičení 2: Vytvoření webové aplikace Galerie fotografií</span><span class="sxs-lookup"><span data-stu-id="af6f1-298">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="af6f1-299">V tomto cvičení budete pracovat s aplikací Fotogalerie pro zobrazování fotek.</span><span class="sxs-lookup"><span data-stu-id="af6f1-299">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="af6f1-300">Začnete s šablonou projektu ASP.NET MVC 4 a pak přidáte funkci pro načtení fotografií ze služby a jejich zobrazení na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="af6f1-300">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="af6f1-301">V následujícím cvičení budete toto řešení aktualizovat, aby se vylepšilo, jak se zobrazuje na mobilních zařízeních.</span><span class="sxs-lookup"><span data-stu-id="af6f1-301">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="af6f1-302">Úloha 1 – Vytvoření modelu fotografické služby</span><span class="sxs-lookup"><span data-stu-id="af6f1-302">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="af6f1-303">V této úloze vytvoříte objekt typu Photo Service, který načte obsah, který se zobrazí v galerii.</span><span class="sxs-lookup"><span data-stu-id="af6f1-303">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="af6f1-304">K tomu je potřeba přidat nový kontroler, který jednoduše vrátí soubor JSON s daty každé fotografie.</span><span class="sxs-lookup"><span data-stu-id="af6f1-304">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="af6f1-305">Otevřete **Visual Studio** , pokud ještě není otevřené.</span><span class="sxs-lookup"><span data-stu-id="af6f1-305">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="af6f1-306">Vyberte **soubor | Nové |** Příkaz nabídky projektu</span><span class="sxs-lookup"><span data-stu-id="af6f1-306">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="af6f1-307">V dialogovém okně **Nový projekt** vyberte **vizuál C# | Webová** šablona ve stromu levého podokna a výběr **webové aplikace ASP.NET MVC 4.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-307">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="af6f1-308">Pojmenujte **fotogalerii**projektů, vyberte umístění (nebo ponechte výchozí) a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-308">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="af6f1-309">Alternativně můžete pokračovat v práci ze stávajícího řešení ASP.NET MVC 4 pro **internetovou aplikaci** z **cvičení 1** a přeskočit další krok.</span><span class="sxs-lookup"><span data-stu-id="af6f1-309">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="af6f1-310">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **Internetová aplikace** a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-310">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="af6f1-311">Ujistěte se, že jste jako zobrazovací modul vybrali Razor.</span><span class="sxs-lookup"><span data-stu-id="af6f1-311">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="af6f1-312">V **Průzkumník řešení**klikněte pravým tlačítkem na složku **aplikace\_data** projektu a vyberte **Přidat | Existující položka**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-312">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="af6f1-313">Přejděte do složky **Source\Assets\App\_data** tohoto testovacího prostředí a přidejte soubor **photos. JSON** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-313">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="af6f1-314">Vytvořte nový kontroler s názvem s **ovladačem**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-314">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="af6f1-315">Provedete to tak, že kliknete pravým tlačítkem na složku **řadiče** , přejdete na **Přidat** a vyberte **kontroler.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-315">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="af6f1-316">Dokončete název kontroleru, ponechte **prázdnou šablonu KONTROLERU MVC** a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-316">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="af6f1-317">![Přidání kontroleru](whats-new-in-aspnet-mvc-4/_static/image19.png "Přidání kontroleru")</span><span class="sxs-lookup"><span data-stu-id="af6f1-317">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="af6f1-318">*Přidání kontroleru*</span><span class="sxs-lookup"><span data-stu-id="af6f1-318">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="af6f1-319">Nahraďte metodu **indexu** následující akcí **Galerie** a vraťte obsah ze souboru JSON, který jste nedávno přidali do projektu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-319">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="af6f1-320">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex02-Galerie – akce*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-320">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="af6f1-321">Stisknutím klávesy **F5** spusťte řešení a potom přejděte na následující adresu URL, abyste mohli otestovat napodobnou fotografii: `http://localhost:[port]/photo/gallery` (hodnota [port] závisí na aktuálním portu, ve kterém byla aplikace spuštěna).</span><span class="sxs-lookup"><span data-stu-id="af6f1-321">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="af6f1-322">Požadavek na tuto adresu URL by měl načíst obsah souboru **photos. JSON** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-322">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="af6f1-323">![Testování služby s napodobnou fotografií](whats-new-in-aspnet-mvc-4/_static/image20.png "Testování služby s napodobnou fotografií")</span><span class="sxs-lookup"><span data-stu-id="af6f1-323">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="af6f1-324">*Testování služby s napodobnou fotografií*</span><span class="sxs-lookup"><span data-stu-id="af6f1-324">*Testing the mocked photo service*</span></span>

<span data-ttu-id="af6f1-325">Ve skutečné implementaci byste mohli použít [webové rozhraní API ASP.NET](../../../../web-api/index.md) k implementaci služby Fotogalerie.</span><span class="sxs-lookup"><span data-stu-id="af6f1-325">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="af6f1-326">Rozhraní ASP.NET Web API usnadňuje sestavování služeb HTTP, které jsou poskytovány širokému spektru klientů, včetně prohlížečů a mobilních zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-326">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="af6f1-327">Rozhraní ASP.NET Web API představuje ideální platformu pro sestavování aplikací RESTful v rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="af6f1-327">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="af6f1-328">Úloha 2 – zobrazení galerie fotografií</span><span class="sxs-lookup"><span data-stu-id="af6f1-328">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="af6f1-329">V této úloze aktualizujete domovskou stránku, aby se zobrazila galerie fotografií pomocí napodobované služby, kterou jste vytvořili v prvním úkolu tohoto cvičení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-329">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="af6f1-330">Přidáte soubory modelů a aktualizujete zobrazení galerie.</span><span class="sxs-lookup"><span data-stu-id="af6f1-330">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="af6f1-331">V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-331">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="af6f1-332">Ve složce **modely** vytvořte třídu **Photo** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-332">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="af6f1-333">Provedete to tak, že kliknete pravým tlačítkem na složku **modely** , vyberete **Přidat** a klikněte na **Třída**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-333">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="af6f1-334">Potom nastavte název na **Photo.cs** a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-334">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="af6f1-335">Přidejte následující členy do třídy **Photo** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-335">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="af6f1-336">(Fragment kódu – *ASP.NET MVC 4 Lab – model Ex02-Photo*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="af6f1-337">Otevřete soubor **HomeController.cs** ze složky **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-337">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="af6f1-338">Přidejte následující příkazy using.</span><span class="sxs-lookup"><span data-stu-id="af6f1-338">Add the following using statements.</span></span>

    <span data-ttu-id="af6f1-339">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex02-HomeController using*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-339">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="af6f1-340">Aktualizujte akci **indexu** tak, aby používala **HttpClient** k načtení dat galerie, a potom pomocí **JavaScriptSerializer** ji deserializovat do modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-340">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="af6f1-341">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex02-index Action*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="af6f1-342">Otevřete soubor **index. cshtml** umístěný ve složce **Views\Home** a nahraďte veškerý obsah následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="af6f1-342">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="af6f1-343">Tento kód projde všemi fotografiemi načtenými ze služby a zobrazí je do neuspořádaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-343">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="af6f1-344">(Fragment kódu – *ASP.NET MVC 4 Lab – Ex02 – seznam fotek*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-344">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="af6f1-345">V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **obsahu** projektu a vyberte **Přidat | Existující položka**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-345">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="af6f1-346">Přejděte do složky **Source\Assets\Content** v tomto testovacím prostředí a přidejte soubor **Web. CSS** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-346">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="af6f1-347">Bude nutné potvrdit jeho náhradu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-347">You will have to confirm its replacement.</span></span> <span data-ttu-id="af6f1-348">Pokud máte soubor **Web. CSS** otevřený, budete se muset ujistit, že soubor znovu načtete.</span><span class="sxs-lookup"><span data-stu-id="af6f1-348">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="af6f1-349">Otevřete Průzkumníka souborů a zkopírujte celou složku **fotek** ve složce **Source\Assets** v tomto testovacím prostředí do kořenové složky projektu v Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-349">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="af6f1-350">Spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="af6f1-350">Run the application.</span></span> <span data-ttu-id="af6f1-351">Teď byste měli vidět domovskou stránku zobrazující fotky v galerii.</span><span class="sxs-lookup"><span data-stu-id="af6f1-351">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="af6f1-352">![Galerie fotografií](whats-new-in-aspnet-mvc-4/_static/image21.png "Galerie fotografií")</span><span class="sxs-lookup"><span data-stu-id="af6f1-352">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="af6f1-353">*Galerie fotografií*</span><span class="sxs-lookup"><span data-stu-id="af6f1-353">*Photo Gallery*</span></span>
11. <span data-ttu-id="af6f1-354">V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-354">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="af6f1-355">Cvičení 3: Přidání podpory pro mobilní zařízení</span><span class="sxs-lookup"><span data-stu-id="af6f1-355">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="af6f1-356">Jedna z klíčových aktualizací v ASP.NET MVC 4 je podpora pro vývoj pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-356">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="af6f1-357">V tomto cvičení budete prozkoumat ASP.NET MVC 4 nové funkce pro mobilní aplikace tím, že rozšíříte řešení Fotogalerie, které jste vytvořili v předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-357">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="af6f1-358">Úloha 1 – instalace jQuery Mobile v aplikaci ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="af6f1-358">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="af6f1-359">Otevřete řešení **zahájit** , které se nachází ve složce **source/EX3-MobileSupport/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="af6f1-359">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="af6f1-360">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-360">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="af6f1-361">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="af6f1-361">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="af6f1-362">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-362">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="af6f1-363">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-363">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="af6f1-364">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-364">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="af6f1-365">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-365">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="af6f1-366">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="af6f1-366">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="af6f1-367">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-367">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="af6f1-368">Otevřete **konzolu správce** balíčků kliknutím na nástroje **Správce balíčků NuGet** **nástroje** >  > možnosti nabídky **konzoly Správce balíčků** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-368">Open the **Package Manager Console** by clicking the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="af6f1-369">![Otevření konzoly Správce balíčků NuGet](whats-new-in-aspnet-mvc-4/_static/image22.png "Otevření konzoly Správce balíčků NuGet")</span><span class="sxs-lookup"><span data-stu-id="af6f1-369">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="af6f1-370">*Otevření konzoly Správce balíčků NuGet*</span><span class="sxs-lookup"><span data-stu-id="af6f1-370">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="af6f1-371">V konzole správce balíčků spusťte následující příkaz k instalaci balíčku **jQuery. Mobile. Mvc** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-371">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="af6f1-372">jQuery Mobile je open source knihovna pro sestavení webového uživatelského rozhraní optimalizovaného pro dotykové ovládání.</span><span class="sxs-lookup"><span data-stu-id="af6f1-372">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="af6f1-373">Balíček NuGet jQuery. Mobile. MVC zahrnuje pomocníky k používání jQuery Mobile s aplikací ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-373">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-374">Spuštěním následujícího příkazu budete stahovat knihovnu jQuery. Mobile. MVC z NuGet.</span><span class="sxs-lookup"><span data-stu-id="af6f1-374">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="af6f1-375">ČÁSTIC</span><span class="sxs-lookup"><span data-stu-id="af6f1-375">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="af6f1-376">Tento příkaz nainstaluje jQuery Mobile a některé pomocné soubory, včetně následujících:</span><span class="sxs-lookup"><span data-stu-id="af6f1-376">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="af6f1-377">**Zobrazení/Shared/\_layout. Mobile. cshtml**: je mobilní rozložení na bázi jQuery optimalizované pro menší obrazovku.</span><span class="sxs-lookup"><span data-stu-id="af6f1-377">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="af6f1-378">Když webová stránka obdrží požadavek z mobilního prohlížeče, nahradí původní rozložení (\_layout. cshtml) tímto.</span><span class="sxs-lookup"><span data-stu-id="af6f1-378">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="af6f1-379">Komponenta s přepínačem zobrazení: skládá se z částečného zobrazení **zobrazení/Shared/\_ViewSwitcher. cshtml** a řadiče **ViewSwitcherController.cs** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-379">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="af6f1-380">Tato součást zobrazí odkaz na mobilní prohlížeče, aby uživatelé mohli přepnout na desktopovou verzi stránky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-380">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="af6f1-381">![Projekt galerie fotografií s podporou mobilních zařízení](whats-new-in-aspnet-mvc-4/_static/image23.png "Projekt galerie fotografií s podporou mobilních zařízení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-381">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="af6f1-382">*Projekt galerie fotografií s podporou mobilních zařízení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-382">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="af6f1-383">Zaregistrujte mobilní sady.</span><span class="sxs-lookup"><span data-stu-id="af6f1-383">Register the Mobile bundles.</span></span> <span data-ttu-id="af6f1-384">Provedete to tak, že otevřete soubor **Global.asax.cs** a přidáte následující řádek.</span><span class="sxs-lookup"><span data-stu-id="af6f1-384">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="af6f1-385">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex03 – Registrace mobilních sad*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-385">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="af6f1-386">Spusťte aplikaci pomocí desktopového webového prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="af6f1-386">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="af6f1-387">Otevřete **emulátor Windows Phone 7** umístěný v **nabídce Start | Všechny programy | Windows Phone SDK 7,1 | Emulátor Windows Phone.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-387">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="af6f1-388">Na obrazovce Start telefonu otevřete Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="af6f1-388">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="af6f1-389">Podívejte se na adresu URL, kde je aplikace spuštěná, a přejděte na tuto adresu URL v prohlížeči telefonu (např. `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="af6f1-389">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="af6f1-390">Všimněte si, že vaše aplikace bude vypadat jinak v emulátoru Windows Phone, protože jQuery. Mobile. MVC vytvořilo v projektu nové prostředky, které zobrazují zobrazení optimalizovaná pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-390">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="af6f1-391">Všimněte si zprávy v horní části telefonu a zobrazuje odkaz, který se přepne do zobrazení plochy.</span><span class="sxs-lookup"><span data-stu-id="af6f1-391">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="af6f1-392">Kromě toho rozložení **\_layout. Mobile. cshtml** vytvořené balíčkem, který jste nainstalovali, zahrnuje jiné rozložení v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="af6f1-392">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-393">Zatím není k dispozici žádný odkaz pro návrat do mobilního zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-393">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="af6f1-394">Bude zahrnutý v novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="af6f1-394">It will be included in later versions.</span></span>

    <span data-ttu-id="af6f1-395">![Mobilní zobrazení domovské stránky Galerie fotografií](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobilní zobrazení domovské stránky Galerie fotografií")</span><span class="sxs-lookup"><span data-stu-id="af6f1-395">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="af6f1-396">*Mobilní zobrazení domovské stránky Galerie fotografií*</span><span class="sxs-lookup"><span data-stu-id="af6f1-396">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="af6f1-397">V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-397">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="af6f1-398">Úkol 2 – vytváření mobilních zobrazení</span><span class="sxs-lookup"><span data-stu-id="af6f1-398">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="af6f1-399">V této úloze vytvoříte mobilní verzi zobrazení index s obsahem upraveným pro lepší vzhled v mobilních zařízeních.</span><span class="sxs-lookup"><span data-stu-id="af6f1-399">In this task, you will create a mobile version of the index view with content adapted for better appearance in mobile devices.</span></span>

1. <span data-ttu-id="af6f1-400">Zkopírujte zobrazení **Views\Home\Index.cshtml** a vložte ho, aby se vytvořila kopie, přejmenujte nový soubor na **index. Mobile. cshtml**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-400">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="af6f1-401">Otevřete nový vytvořený **index. Mobile. cshtml** zobrazení a nahraďte existující značku &lt;ul&gt; tímto kódem.</span><span class="sxs-lookup"><span data-stu-id="af6f1-401">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="af6f1-402">Tímto způsobem aktualizujete značku &lt;ul&gt; pomocí poznámek k mobilním datům jQuery, aby se použily mobilní motivy z jQuery.</span><span class="sxs-lookup"><span data-stu-id="af6f1-402">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="af6f1-403">Všimněte si, že:</span><span class="sxs-lookup"><span data-stu-id="af6f1-403">Notice that:</span></span>
    > 
    > - <span data-ttu-id="af6f1-404">Atribut **role dat** nastavený na **ListView** vykreslí seznam pomocí stylů ListView.</span><span class="sxs-lookup"><span data-stu-id="af6f1-404">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="af6f1-405">Atribut **vsazení dat** nastavený na hodnotu true zobrazí seznam s zaobleným ohraničením a okrajem.</span><span class="sxs-lookup"><span data-stu-id="af6f1-405">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="af6f1-406">Atribut **filtru dat** nastavený na **hodnotu true** vygeneruje vyhledávací pole.</span><span class="sxs-lookup"><span data-stu-id="af6f1-406">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="af6f1-407">Další informace o konvencích pro mobilní zařízení jQuery najdete v dokumentaci k projektu: [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="af6f1-407">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="af6f1-408">Změny uložte stisknutím **kombinace kláves CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-408">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="af6f1-409">Přepněte na **emulátor Windows Phone** a aktualizujte lokalitu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-409">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="af6f1-410">Všimněte si nového vzhledu a chování seznamu galerie a také nového vyhledávacího pole v horní části.</span><span class="sxs-lookup"><span data-stu-id="af6f1-410">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="af6f1-411">Potom zadejte slovo do vyhledávacího pole (například **Tulips**), aby se spustilo hledání v galerii fotografií.</span><span class="sxs-lookup"><span data-stu-id="af6f1-411">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="af6f1-412">![Galerie s filtrováním pomocí stylu ListView](whats-new-in-aspnet-mvc-4/_static/image25.png "Galerie s filtrováním pomocí stylu ListView")</span><span class="sxs-lookup"><span data-stu-id="af6f1-412">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="af6f1-413">*Galerie s filtrováním pomocí stylu ListView*</span><span class="sxs-lookup"><span data-stu-id="af6f1-413">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="af6f1-414">Pro shrnutí jste použili recept pro zobrazení, pomocí kterého jste vytvořili kopii zobrazení index s příponou &quot;Mobile&quot;.</span><span class="sxs-lookup"><span data-stu-id="af6f1-414">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="af6f1-415">Tato přípona indikuje ASP.NET MVC 4, že každý požadavek vygenerovaný z mobilního zařízení bude používat tuto kopii indexu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-415">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="af6f1-416">Kromě toho jste aktualizovali mobilní verzi zobrazení index pro použití jQuery Mobile pro zlepšení vzhledu lokality a chování v mobilních zařízeních.</span><span class="sxs-lookup"><span data-stu-id="af6f1-416">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="af6f1-417">Vraťte se do sady Visual Studio a otevřete **Web. Mobile. CSS** nacházející se ve složce **obsahu** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-417">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="af6f1-418">Opravte umístění názvu fotografie, aby se zobrazila na pravé straně obrázku.</span><span class="sxs-lookup"><span data-stu-id="af6f1-418">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="af6f1-419">Chcete-li to provést, přidejte do souboru **Web. Mobile. CSS** následující kód.</span><span class="sxs-lookup"><span data-stu-id="af6f1-419">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="af6f1-420">CSS</span><span class="sxs-lookup"><span data-stu-id="af6f1-420">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="af6f1-421">Změny uložte stisknutím **kombinace kláves CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-421">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="af6f1-422">Přepněte zpátky na **emulátor Windows Phone** a aktualizujte lokalitu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-422">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="af6f1-423">Všimněte si, že název fotografie je teď správně umístěný.</span><span class="sxs-lookup"><span data-stu-id="af6f1-423">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="af6f1-424">![Název umístěný na pravé straně obrázku](whats-new-in-aspnet-mvc-4/_static/image26.png "Název umístěný na pravé straně obrázku")</span><span class="sxs-lookup"><span data-stu-id="af6f1-424">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="af6f1-425">*Název umístěný na pravé straně obrázku*</span><span class="sxs-lookup"><span data-stu-id="af6f1-425">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="af6f1-426">Úloha 3 – jQuery – mobilní motivy</span><span class="sxs-lookup"><span data-stu-id="af6f1-426">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="af6f1-427">Každé rozložení a widget v jQuery Mobile je navrženo kolem nového objektově orientovaného rozhraní CSS, které umožňuje použít kompletní motiv sjednocení vizuálního návrhu pro weby a aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-427">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="af6f1-428">výchozí motiv jQuery Mobile obsahuje 5 vzorků, kterým jsou uvedena písmena (a, b, c, d, e) pro rychlé reference.</span><span class="sxs-lookup"><span data-stu-id="af6f1-428">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="af6f1-429">V této úloze aktualizujete rozložení pro mobilní zařízení tak, aby používalo jiný motiv než výchozí.</span><span class="sxs-lookup"><span data-stu-id="af6f1-429">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="af6f1-430">Přepněte zpět do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6f1-430">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="af6f1-431">Otevřete soubor **\_layout. Mobile. cshtml** umístěný v **Views\Shared**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-431">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="af6f1-432">Najděte element div s rolí data-role nastavenou na &quot;&quot; stránky a aktualizujte **motiv dat** na &quot;**e**&quot;.</span><span class="sxs-lookup"><span data-stu-id="af6f1-432">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="af6f1-433">Změny uložte stisknutím **kombinace kláves CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-433">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="af6f1-434">Aktualizujte lokalitu v **emulátoru Windows Phone** a Všimněte si nového schématu barev.</span><span class="sxs-lookup"><span data-stu-id="af6f1-434">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="af6f1-435">![Mobilní rozložení s odlišným barevným schématem](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobilní rozložení s odlišným barevným schématem")</span><span class="sxs-lookup"><span data-stu-id="af6f1-435">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="af6f1-436">*Mobilní rozložení s odlišným barevným schématem*</span><span class="sxs-lookup"><span data-stu-id="af6f1-436">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="af6f1-437">Úloha 4 – použití součásti pro přepínání zobrazení a přepisování funkcí v prohlížeči</span><span class="sxs-lookup"><span data-stu-id="af6f1-437">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="af6f1-438">Konvence pro mobilní optimalizované webové stránky je přidat odkaz, jehož text je například desktopové zobrazení nebo režim celého webu, který umožňuje uživatelům přepnout na desktopovou verzi stránky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-438">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="af6f1-439">Balíček jQuery. Mobile. MVC obsahuje ukázkovou komponentu pro **přepínání zobrazení** pro tento účel, která se používá v zobrazení **\_layout. Mobile. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-439">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="af6f1-440">![Odkaz pro přepnutí na desktopové zobrazení](whats-new-in-aspnet-mvc-4/_static/image28.png "Odkaz pro přepnutí na desktopové zobrazení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-440">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="af6f1-441">*Odkaz pro přepnutí na desktopové zobrazení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-441">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="af6f1-442">Přepínač zobrazení používá novou funkci nazvanou **přepisování prohlížeče**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-442">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="af6f1-443">Tato funkce umožňuje, aby vaše aplikace považovala požadavky, jako kdyby byly přicházející z jiného prohlížeče (uživatelského agenta) než ten, ze kterého přicházejí.</span><span class="sxs-lookup"><span data-stu-id="af6f1-443">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="af6f1-444">V této úloze prozkoumáte ukázkovou implementaci přepínačů zobrazení přidaných jQuery. Mobile. MVC a nový prohlížeč přepsal funkce v ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-444">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="af6f1-445">Přepněte zpět do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6f1-445">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="af6f1-446">Otevřete zobrazení **\_layout. Mobile. cshtml** nacházející se ve složce **Views\Shared** a Všimněte si, že se na komponentu s přepínači zobrazení odkazuje jako na částečné zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-446">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="af6f1-447">![Mobilní rozložení pomocí součásti pro přepínač zobrazení](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobilní rozložení pomocí součásti pro přepínač zobrazení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-447">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="af6f1-448">*Mobilní rozložení pomocí součásti pro přepínač zobrazení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-448">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="af6f1-449">Otevřete částečné zobrazení **\_ViewSwitcher. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-449">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="af6f1-450">Částečné zobrazení používá novou metodu **ViewContext. HttpContext. GetOverriddenBrowser ()** k určení původu webového požadavku a zobrazí odpovídající odkaz pro přepnutí buď na Desktop nebo mobilní zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-450">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="af6f1-451">Metoda **GetOverriddenBrowser** vrací instanci **HttpBrowserCapabilitiesBase** , která odpovídá uživatelskému agentovi, který je aktuálně nastaven pro požadavek (skutečnost nebo přepsání).</span><span class="sxs-lookup"><span data-stu-id="af6f1-451">The **GetOverriddenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="af6f1-452">Tuto hodnotu můžete použít k získání vlastností, jako je například **IsMobileDevice**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-452">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="af6f1-453">![ViewSwitcher částečné zobrazení](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher částečné zobrazení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-453">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="af6f1-454">*ViewSwitcher částečné zobrazení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-454">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="af6f1-455">Otevřete třídu **ViewSwitcherController.cs** , která se nachází ve složce **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-455">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="af6f1-456">Podívejte se, že akce SwitchView je volána odkazem v komponentě ViewSwitcher a Všimněte si nových metod HttpContext.</span><span class="sxs-lookup"><span data-stu-id="af6f1-456">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="af6f1-457">Metoda **HttpContext. ClearOverriddenBrowser ()** odebere všechny přepsané uživatelské agenta pro aktuální požadavek.</span><span class="sxs-lookup"><span data-stu-id="af6f1-457">The **HttpContext.ClearOverriddenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="af6f1-458">Metoda **HttpContext. SetOverriddenBrowser ()** Přepisuje skutečnou hodnotu uživatelského agenta žádosti pomocí zadaného uživatelského agenta.</span><span class="sxs-lookup"><span data-stu-id="af6f1-458">The **HttpContext.SetOverriddenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="af6f1-459">![Kontroler ViewSwitcher](whats-new-in-aspnet-mvc-4/_static/image31.png "Kontroler ViewSwitcher")</span><span class="sxs-lookup"><span data-stu-id="af6f1-459">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="af6f1-460">*Kontroler ViewSwitcher*</span><span class="sxs-lookup"><span data-stu-id="af6f1-460">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="af6f1-461">Přepsání prohlížeče je základní funkcí ASP.NET MVC 4, která je k dispozici i v případě, že balíček jQuery. Mobile. MVC nenainstalujete.</span><span class="sxs-lookup"><span data-stu-id="af6f1-461">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="af6f1-462">Tato funkce ale ovlivňuje jenom zobrazení, rozložení a částečné zobrazení a nemá vliv na žádnou z funkcí, které závisí na objektu Request. browser.</span><span class="sxs-lookup"><span data-stu-id="af6f1-462">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="af6f1-463">Úkol 5 – přidání přepínačů zobrazení v desktopovém zobrazení</span><span class="sxs-lookup"><span data-stu-id="af6f1-463">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="af6f1-464">V této úloze aktualizujete rozložení plochy tak, aby zahrnovalo přepínač zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-464">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="af6f1-465">To umožní mobilním uživatelům přejít zpět do mobilního zobrazení při procházení plochy.</span><span class="sxs-lookup"><span data-stu-id="af6f1-465">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="af6f1-466">Aktualizujte lokalitu v **emulátoru Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-466">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="af6f1-467">V horní části Galerie klikněte na odkaz **zobrazení plochy** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-467">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="af6f1-468">Všimněte si, že v zobrazení plocha není žádný přepínač zobrazení, který vám umožní vrátit se do mobilního zobrazení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-468">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="af6f1-469">Vraťte se do sady Visual Studio a otevřete zobrazení **\_layout. cshtml** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-469">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="af6f1-470">Vyhledejte část přihlášení a vložte volání, které vykreslí **\_** částečné zobrazení pod\_částečném zobrazením **LogOnPartial** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-470">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="af6f1-471">Potom stisknutím **kombinace kláves CTRL + S** změny uložte.</span><span class="sxs-lookup"><span data-stu-id="af6f1-471">Then, press **CTRL + S** to save the changes.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="af6f1-472">Změny uložte stisknutím **kombinace kláves CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-472">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="af6f1-473">Aktualizujte stránku v emulátoru Windows Phone a dvakrát klikněte na obrazovku pro přiblížení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-473">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="af6f1-474">Všimněte si, že na domovské stránce se nyní zobrazuje odkaz **mobilní zobrazení** , který přepíná z mobilního zobrazení na Desktop.</span><span class="sxs-lookup"><span data-stu-id="af6f1-474">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="af6f1-475">![Přepínač zobrazení vykreslený v desktopovém zobrazení](whats-new-in-aspnet-mvc-4/_static/image32.png "Přepínač zobrazení vykreslený v desktopovém zobrazení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-475">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="af6f1-476">*Přepínač zobrazení vykreslený v desktopovém zobrazení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-476">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="af6f1-477">Přepněte znovu do mobilního zobrazení a přejděte na stránku **About** (http://localhost[port]/Home/about).</span><span class="sxs-lookup"><span data-stu-id="af6f1-477">Switch to the Mobile view again and browse to **About** page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="af6f1-478">Všimněte si, že i v případě, že jste ještě nevytvořili zobrazení About. Mobile. cshtml, zobrazí se stránka o aplikaci pomocí rozložení mobilní (\_layout. Mobile. cshtml).</span><span class="sxs-lookup"><span data-stu-id="af6f1-478">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="af6f1-479">![O stránce](whats-new-in-aspnet-mvc-4/_static/image33.png "O stránce")</span><span class="sxs-lookup"><span data-stu-id="af6f1-479">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="af6f1-480">*O stránce*</span><span class="sxs-lookup"><span data-stu-id="af6f1-480">*About page*</span></span>
8. <span data-ttu-id="af6f1-481">Nakonec otevřete web v desktopovém webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="af6f1-481">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="af6f1-482">Všimněte si, že žádný z předchozích aktualizací neovlivnil zobrazení plochy.</span><span class="sxs-lookup"><span data-stu-id="af6f1-482">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="af6f1-483">![Desktopové zobrazení galerie](whats-new-in-aspnet-mvc-4/_static/image34.png "Desktopové zobrazení galerie")</span><span class="sxs-lookup"><span data-stu-id="af6f1-483">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="af6f1-484">*Desktopové zobrazení galerie*</span><span class="sxs-lookup"><span data-stu-id="af6f1-484">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="af6f1-485">Úloha 6 – vytváření nových režimů zobrazení</span><span class="sxs-lookup"><span data-stu-id="af6f1-485">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="af6f1-486">Funkce nové režimy zobrazení umožňuje aplikaci vybrat zobrazení v závislosti na prohlížeči, který požadavek vygeneroval.</span><span class="sxs-lookup"><span data-stu-id="af6f1-486">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="af6f1-487">Pokud například prohlížeč stolních počítačů požaduje domovskou stránku, aplikace vrátí šablonu **Views\Home\Index.cshtml** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-487">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="af6f1-488">Pokud pak mobilní prohlížeč požaduje domovskou stránku, aplikace vrátí šablonu **Views\Home\Index.Mobile.cshtml** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-488">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="af6f1-489">V této úloze vytvoříte přizpůsobené rozložení pro zařízení iPhone a budete muset simulovat žádosti od zařízení iPhone.</span><span class="sxs-lookup"><span data-stu-id="af6f1-489">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="af6f1-490">K tomu můžete použít emulátor nebo simulátor pro iPhone (jako je [elektrický mobilní simulátor](http://www.electricplum.com/)) nebo prohlížeč s doplňky, které upravují uživatelského agenta.</span><span class="sxs-lookup"><span data-stu-id="af6f1-490">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="af6f1-491">Pokyny, jak nastavit řetězec uživatelského agenta v prohlížeči Safari pro emulaci iPhonu, najdete v článku [jak umožnit Safari předstírat je IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) v blogu David Alison.</span><span class="sxs-lookup"><span data-stu-id="af6f1-491">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="af6f1-492">**Všimněte si, že tato úloha je volitelná a vy můžete pokračovat v rámci testovacího prostředí bez jeho provedení.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-492">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="af6f1-493">V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-493">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="af6f1-494">Otevřete **Global.asax.cs** a přidejte následující příkaz using.</span><span class="sxs-lookup"><span data-stu-id="af6f1-494">Open **Global.asax.cs** and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="af6f1-495">Přidejte následující zvýrazněný kód do aplikace\_spustit metodu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-495">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="af6f1-496">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex03-iPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-496">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

<span data-ttu-id="af6f1-497">Zaregistrovali jste nové **DefaultDisplayMode s názvem &quot;iPhone&quot;** v rámci statického seznamu static **DisplayModeProvider. instance. Modes** , který se bude shodovat s každým příchozím požadavkem.</span><span class="sxs-lookup"><span data-stu-id="af6f1-497">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="af6f1-498">Pokud příchozí požadavek obsahuje řetězec &quot;iPhone&quot;, ASP.NET MVC najde zobrazení, jejichž název obsahuje příponu&quot; iPhone &quot;pro iPhone.</span><span class="sxs-lookup"><span data-stu-id="af6f1-498">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="af6f1-499">Parametr 0 označuje, jak konkrétní je nový režim; Toto zobrazení je například konkrétnější než obecné &quot;. mobilní&quot; pravidlo, které odpovídá žádostem z mobilních zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-499">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

<span data-ttu-id="af6f1-500">Po spuštění tohoto kódu bude aplikace při vygenerování žádosti v prohlížeči iPhone používat **Views\Shared\\_Layout. iPhone. cshtml** , které vytvoříte v dalších krocích.</span><span class="sxs-lookup"><span data-stu-id="af6f1-500">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

> [!NOTE]
> <span data-ttu-id="af6f1-501">Tento způsob testování žádosti pro iPhone byl pro demonstrační účely zjednodušený a nemusí fungovat podle očekávání pro každý řetězec agenta uživatele iPhone (například test rozlišuje malá a velká písmena).</span><span class="sxs-lookup"><span data-stu-id="af6f1-501">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>

4. <span data-ttu-id="af6f1-502">Vytvořte kopii souboru **\_layout. Mobile. cshtml** ve složce **Views\Shared** a přejmenujte kopii na &quot; **\_layout. cshtml**&quot;.</span><span class="sxs-lookup"><span data-stu-id="af6f1-502">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.cshtml**&quot;.</span></span>
5. <span data-ttu-id="af6f1-503">Otevřete **\_layout. iPhone. cshtml** , který jste vytvořili v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="af6f1-503">Open **\_Layout.iPhone.cshtml** you created in the previous step.</span></span>
6. <span data-ttu-id="af6f1-504">Najděte element div s atributem role dat nastavenou na **stránku** a změňte atribut **data-Theme** tak, **aby &quot;&quot;** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-504">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

<span data-ttu-id="af6f1-505">V aplikaci ASP.NET MVC 4 teď máte tři rozložení:</span><span class="sxs-lookup"><span data-stu-id="af6f1-505">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

1. <span data-ttu-id="af6f1-506">**\_layout. cshtml**: výchozí rozložení používané pro desktopové prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="af6f1-506">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
2. <span data-ttu-id="af6f1-507">**\_layout. Mobile. cshtml**: výchozí rozložení používané pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-507">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
3. <span data-ttu-id="af6f1-508">**\_layout. iPhone. cshtml**: konkrétní rozložení pro zařízení iPhone pomocí jiného barevného schématu, které rozlišuje \_layout. Mobile. cshtml.</span><span class="sxs-lookup"><span data-stu-id="af6f1-508">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="af6f1-509">Stisknutím klávesy **F5** spusťte aplikaci a procházejte lokalitou v **emulátoru Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-509">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="af6f1-510">Otevřete **simulátor pro iPhone** (pokyny k instalaci a konfiguraci simulátoru pro iPhone najdete v [příloze C](#AppendixC) ) a přejděte na web také.</span><span class="sxs-lookup"><span data-stu-id="af6f1-510">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="af6f1-511">Všimněte si, že každý telefon používá konkrétní šablonu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-511">Notice that each phone is using the specific template.</span></span>

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="af6f1-513">*Používání různých zobrazení pro každé mobilní zařízení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-513">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="af6f1-514">Cvičení 4: použití asynchronních řadičů</span><span class="sxs-lookup"><span data-stu-id="af6f1-514">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="af6f1-515">Microsoft .NET Framework 4,5 zavádí nové jazykové funkce v C# a Visual Basic k poskytování nového základu pro asynchronii v programování .NET.</span><span class="sxs-lookup"><span data-stu-id="af6f1-515">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="af6f1-516">Tato nová základ usnadňuje asynchronní programování podobným a přibližně jako synchronní programování.</span><span class="sxs-lookup"><span data-stu-id="af6f1-516">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="af6f1-517">Nyní je možné zapisovat metody asynchronních akcí v ASP.NET MVC 4 pomocí třídy **AsyncController** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-517">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="af6f1-518">Asynchronní metody akcí můžete použít pro dlouhotrvající požadavky, které nejsou vázané na procesor.</span><span class="sxs-lookup"><span data-stu-id="af6f1-518">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="af6f1-519">Tím předejdete blokování, aby webový server prováděl práci během zpracování žádosti.</span><span class="sxs-lookup"><span data-stu-id="af6f1-519">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="af6f1-520">Třída AsyncController se obvykle používá pro dlouhotrvající volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="af6f1-520">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="af6f1-521">Toto cvičení vysvětluje základy asynchronních operací v ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-521">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="af6f1-522">Pokud potřebujete hlubší podrobně, můžete se podívat na následující článek: [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="af6f1-522">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="af6f1-523">Úloha 1 – implementace asynchronního kontroleru</span><span class="sxs-lookup"><span data-stu-id="af6f1-523">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="af6f1-524">Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex4-Async/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="af6f1-524">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="af6f1-525">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-525">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="af6f1-526">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="af6f1-526">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="af6f1-527">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-527">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="af6f1-528">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-528">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="af6f1-529">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-529">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="af6f1-530">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-530">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="af6f1-531">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="af6f1-531">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="af6f1-532">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-532">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="af6f1-533">Otevřete třídu **HomeController.cs** ze složky **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-533">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="af6f1-534">Přidejte následující příkaz using.</span><span class="sxs-lookup"><span data-stu-id="af6f1-534">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="af6f1-535">Aktualizujte třídu **HomeController** tak, aby dědila z **AsyncController**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-535">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="af6f1-536">Řadiče, které jsou odvozeny od AsyncController, umožňují ASP.NET zpracování asynchronních požadavků a stále mohou obsluhovat synchronní metody akcí.</span><span class="sxs-lookup"><span data-stu-id="af6f1-536">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="af6f1-537">Přidejte klíčové slovo **Async** do metody **indexu** a vraťte typ **Task&lt;ActionResult&gt;** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-537">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="af6f1-538">Klíčové slovo **Async** je jedno z nových klíčových slov, které poskytuje .NET Framework 4,5. oznamuje kompilátoru, že tato metoda obsahuje asynchronní kód.</span><span class="sxs-lookup"><span data-stu-id="af6f1-538">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="af6f1-539">Objekt **úlohy** představuje asynchronní operaci, která může být dokončena v nějakém okamžiku v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-539">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="af6f1-540">Nahraďte **klienta. Volání GetAsync ()** s úplnou asynchronní verzí pomocí klíčového slova await, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="af6f1-540">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="af6f1-541">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-541">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="af6f1-542">V předchozí verzi jste používali vlastnost **Result** z objektu **Task** k blokování vlákna, dokud není výsledek vrácen (synchronizační verze).</span><span class="sxs-lookup"><span data-stu-id="af6f1-542">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="af6f1-543">Přidáním klíčového slova **await** říká kompilátoru, že asynchronně čeká na úlohu vrácenou z volání metody.</span><span class="sxs-lookup"><span data-stu-id="af6f1-543">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="af6f1-544">To znamená, že zbytek kódu bude proveden jako zpětné volání až po dokončení očekávané metody.</span><span class="sxs-lookup"><span data-stu-id="af6f1-544">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="af6f1-545">Další věcí k oznámení je, že nemusíte měnit blok try-catch, aby bylo možné provést tuto práci: výjimky, ke kterým dochází na pozadí nebo v popředí, budou stále zachyceny bez jakékoli další práce pomocí obslužné rutiny poskytované rozhraním.</span><span class="sxs-lookup"><span data-stu-id="af6f1-545">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="af6f1-546">Změňte kód tak, aby pokračoval v asynchronní implementaci nahrazením řádků novým kódem, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="af6f1-546">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="af6f1-547">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-547">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="af6f1-548">Spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="af6f1-548">Run the application.</span></span> <span data-ttu-id="af6f1-549">Všimnete si, že nebudete mít žádné zásadní změny, ale váš kód nebude blokovat vlákno z fondu vláken, což vylepší využití prostředků serveru a zlepšuje výkon.</span><span class="sxs-lookup"><span data-stu-id="af6f1-549">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-550">Další informace o nových asynchronních programovacích funkcích v testovacím prostředí &quot;**asynchronní programování v rozhraní .net 4,5 C# s a Visual Basic**&quot; zahrnutých v sadě Visual Studio Training Kit.</span><span class="sxs-lookup"><span data-stu-id="af6f1-550">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="af6f1-551">Úloha 2 – zpracování časových limitů s tokeny zrušení</span><span class="sxs-lookup"><span data-stu-id="af6f1-551">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="af6f1-552">Asynchronní metody akcí, které vracejí instance úloh, mohou také podporovat časové limity.</span><span class="sxs-lookup"><span data-stu-id="af6f1-552">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="af6f1-553">V této úloze aktualizujete kód metody indexu pro zpracování scénáře časového limitu pomocí tokenu zrušení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-553">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="af6f1-554">Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.</span><span class="sxs-lookup"><span data-stu-id="af6f1-554">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="af6f1-555">Do souboru **HomeController.cs** přidejte následující příkaz using.</span><span class="sxs-lookup"><span data-stu-id="af6f1-555">Add the following using statement to the **HomeController.cs** file.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="af6f1-556">Aktualizujte akci indexu tak, aby přijímala argument **CancellationToken** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-556">Update the Index action to receive a **CancellationToken** argument.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="af6f1-557">Aktualizujte volání **GetAsync** , aby se předal token zrušení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-557">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="af6f1-558">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-SendAsync with CancellationToken*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-558">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="af6f1-559">Naupravte metodu *indexu* s atributem **hodnota vlastnosti AsyncTimeout** nastaveným na 500 milisekund a atribut **HandleError** nakonfigurovaný tak, aby zpracovávala **TaskCanceledException** přesměrováním na zobrazení pro **vypršení časového limitu** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-559">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="af6f1-560">(Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-Attributes*)</span><span class="sxs-lookup"><span data-stu-id="af6f1-560">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="af6f1-561">Otevřete třídu **fotocontroller** a aktualizujte metodu **Galerie** tak, aby zpozdila spuštění 1000 milisekund (1 sekunda), aby se simulovala dlouhodobě spuštěná úloha.</span><span class="sxs-lookup"><span data-stu-id="af6f1-561">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 milliseconds (1 second) to simulate a long running task.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="af6f1-562">Otevřete soubor **Web. config** a povolte vlastní chyby přidáním následujícího elementu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-562">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="af6f1-563">Vytvořte nové zobrazení v **Views\Shared** s názvem **časované** a použijte výchozí rozložení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-563">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="af6f1-564">V Průzkumník řešení klikněte pravým tlačítkem na složku **Views\Shared** a vyberte **Přidat | Zobrazit**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-564">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="af6f1-565">![Používání různých zobrazení pro každé mobilní zařízení](whats-new-in-aspnet-mvc-4/_static/image36.png "Používání různých zobrazení pro každé mobilní zařízení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-565">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="af6f1-566">*Používání různých zobrazení pro každé mobilní zařízení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-566">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="af6f1-567">Aktualizujte obsah zobrazení s **časovým limitem** , jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="af6f1-567">Update the **TimedOut** view content as shown below.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="af6f1-568">Spusťte aplikaci a přejděte na kořenovou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="af6f1-568">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="af6f1-569">Když jste přidali **vlákno. režim spánku** je 1000 milisekund, zobrazí se chyba vypršení časového limitu, generovaná atributem **hodnota vlastnosti AsyncTimeout** a zachycení atributem **HandleError** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-569">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="af6f1-570">![Zpracovaná výjimka časového limitu](whats-new-in-aspnet-mvc-4/_static/image37.png "Zpracovaná výjimka časového limitu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-570">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="af6f1-571">*Zpracovaná výjimka časového limitu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-571">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="af6f1-572">Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure [v následujícím dodatku D: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixD).</span><span class="sxs-lookup"><span data-stu-id="af6f1-572">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="af6f1-573">Souhrn</span><span class="sxs-lookup"><span data-stu-id="af6f1-573">Summary</span></span>

<span data-ttu-id="af6f1-574">V tomto praktickém cvičení jste se seznámili s některými novými funkcemi rezidenty v ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-574">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="af6f1-575">Byly popsány následující koncepty:</span><span class="sxs-lookup"><span data-stu-id="af6f1-575">The following concepts have been discussed:</span></span>

- <span data-ttu-id="af6f1-576">Využijte výhod vylepšení šablon projektů ASP.NET MVC – včetně nové šablony projektu mobilní aplikace</span><span class="sxs-lookup"><span data-stu-id="af6f1-576">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="af6f1-577">Použití atributů zobrazení HTML5 a dotazů na média šablon stylů CSS ke zlepšení zobrazení na mobilních zařízeních</span><span class="sxs-lookup"><span data-stu-id="af6f1-577">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="af6f1-578">Použití jQuery Mobile pro progresivní vylepšení a vytváření webového uživatelského rozhraní optimalizovaného pro dotykové ovládání</span><span class="sxs-lookup"><span data-stu-id="af6f1-578">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="af6f1-579">Vytváření zobrazení specifických pro mobilní zařízení</span><span class="sxs-lookup"><span data-stu-id="af6f1-579">Create mobile-specific views</span></span>
- <span data-ttu-id="af6f1-580">Přepínání mezi zobrazeními mobilních a desktopových aplikací v aplikaci pomocí součásti pro přepínání zobrazení</span><span class="sxs-lookup"><span data-stu-id="af6f1-580">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="af6f1-581">Vytváření asynchronních řadičů pomocí podpory úloh</span><span class="sxs-lookup"><span data-stu-id="af6f1-581">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="af6f1-582">Příloha A: používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="af6f1-582">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="af6f1-583">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="af6f1-583">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="af6f1-584">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="af6f1-584">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="af6f1-585">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](whats-new-in-aspnet-mvc-4/_static/image38.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="af6f1-585">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="af6f1-586">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="af6f1-586">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="af6f1-587">***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="af6f1-587">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="af6f1-588">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="af6f1-588">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="af6f1-589">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="af6f1-589">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="af6f1-590">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-590">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="af6f1-591">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="af6f1-591">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="af6f1-592">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="af6f1-592">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="af6f1-593">![Začněte psát název fragmentu.](whats-new-in-aspnet-mvc-4/_static/image39.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-593">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="af6f1-594">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-594">*Start typing the snippet name*</span></span>

<span data-ttu-id="af6f1-595">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](whats-new-in-aspnet-mvc-4/_static/image40.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-595">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="af6f1-596">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-596">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="af6f1-597">![Stiskněte znovu TAB a fragment kódu se rozšíří.](whats-new-in-aspnet-mvc-4/_static/image41.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-597">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="af6f1-598">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-598">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="af6f1-599">***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)***</span><span class="sxs-lookup"><span data-stu-id="af6f1-599">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="af6f1-600">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-600">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="af6f1-601">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-601">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="af6f1-602">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-602">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="af6f1-603">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](whats-new-in-aspnet-mvc-4/_static/image42.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-603">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="af6f1-604">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-604">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="af6f1-605">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](whats-new-in-aspnet-mvc-4/_static/image43.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-605">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="af6f1-606">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-606">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="af6f1-607">Příloha B: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="af6f1-607">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="af6f1-608">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-608">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="af6f1-609">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="af6f1-609">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="af6f1-610">Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="af6f1-610">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="af6f1-611">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;*Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK*&quot;.</span><span class="sxs-lookup"><span data-stu-id="af6f1-611">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="af6f1-612">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-612">Click on **Install Now**.</span></span> <span data-ttu-id="af6f1-613">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="af6f1-613">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="af6f1-614">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="af6f1-614">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="af6f1-615">![Nainstalovat Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="af6f1-615">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="af6f1-616">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="af6f1-616">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="af6f1-617">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-617">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="af6f1-619">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="af6f1-619">*Accepting the license terms*</span></span>
5. <span data-ttu-id="af6f1-620">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-620">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="af6f1-622">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="af6f1-622">*Installation progress*</span></span>
6. <span data-ttu-id="af6f1-623">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-623">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="af6f1-625">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="af6f1-625">*Installation completed*</span></span>
7. <span data-ttu-id="af6f1-626">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="af6f1-626">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="af6f1-627">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-627">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="af6f1-629">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="af6f1-629">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="af6f1-630">Příloha C: instalace simulátoru WebMatrix 2 a iPhonu</span><span class="sxs-lookup"><span data-stu-id="af6f1-630">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="af6f1-631">Pro spuštění webu v simulovaném zařízení iPhone můžete použít rozšíření WebMatrix &quot;elektrického mobilního simulátoru pro iPhone&quot;pro iPhone.</span><span class="sxs-lookup"><span data-stu-id="af6f1-631">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="af6f1-632">Můžete také nakonfigurovat stejné rozšíření pro spuštění simulátoru ze sady Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="af6f1-632">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="af6f1-633">Úloha 1 – instalace WebMatrixu 2</span><span class="sxs-lookup"><span data-stu-id="af6f1-633">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="af6f1-634">Přejít na [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="af6f1-634">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="af6f1-635">Případně, pokud již máte nainstalován instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;&quot;*WebMatrix 2* .</span><span class="sxs-lookup"><span data-stu-id="af6f1-635">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*WebMatrix 2*&quot;.</span></span>
2. <span data-ttu-id="af6f1-636">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-636">Click on **Install Now**.</span></span> <span data-ttu-id="af6f1-637">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="af6f1-637">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="af6f1-638">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="af6f1-638">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="af6f1-639">![Nainstalovat WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Nainstalovat WebMatrix 2")</span><span class="sxs-lookup"><span data-stu-id="af6f1-639">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="af6f1-640">*Nainstalovat WebMatrix 2*</span><span class="sxs-lookup"><span data-stu-id="af6f1-640">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="af6f1-641">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="af6f1-641">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="af6f1-642">![Přijetí licenčních podmínek](whats-new-in-aspnet-mvc-4/_static/image50.png "Přijetí licenčních podmínek")</span><span class="sxs-lookup"><span data-stu-id="af6f1-642">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="af6f1-643">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="af6f1-643">*Accepting the license terms*</span></span>
5. <span data-ttu-id="af6f1-644">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-644">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="af6f1-645">![Průběh instalace](whats-new-in-aspnet-mvc-4/_static/image51.png "Průběh instalace")</span><span class="sxs-lookup"><span data-stu-id="af6f1-645">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="af6f1-646">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="af6f1-646">*Installation progress*</span></span>
6. <span data-ttu-id="af6f1-647">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-647">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="af6f1-648">![Instalace dokončena](whats-new-in-aspnet-mvc-4/_static/image52.png "Instalace dokončena")</span><span class="sxs-lookup"><span data-stu-id="af6f1-648">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="af6f1-649">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="af6f1-649">*Installation completed*</span></span>
7. <span data-ttu-id="af6f1-650">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="af6f1-650">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="af6f1-651">Úloha 2 – instalace rozšíření simulátoru iPhonu</span><span class="sxs-lookup"><span data-stu-id="af6f1-651">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="af6f1-652">Spusťte **WebMatrix** a otevřete libovolný existující web nebo vytvořte nový.</span><span class="sxs-lookup"><span data-stu-id="af6f1-652">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="af6f1-653">Na pásu karet **Domů** klikněte na tlačítko **Spustit** a vyberte **Přidat nový**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-653">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="af6f1-654">![Přidává se nové rozšíření WebMatrix.](whats-new-in-aspnet-mvc-4/_static/image53.png "Přidává se nové rozšíření WebMatrix.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-654">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="af6f1-655">*Přidává se nové rozšíření WebMatrix.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-655">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="af6f1-656">Vyberte **simulátor iPhone** a klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-656">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="af6f1-657">![Procházení rozšíření WebMatrixu](whats-new-in-aspnet-mvc-4/_static/image54.png "Procházení rozšíření WebMatrixu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-657">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="af6f1-658">*Procházení rozšíření WebMatrixu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-658">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="af6f1-659">V podrobnostech balíčku kliknutím na **instalovat** pokračujte v instalaci rozšíření.</span><span class="sxs-lookup"><span data-stu-id="af6f1-659">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="af6f1-660">![rozšíření simulátoru iPhonu](whats-new-in-aspnet-mvc-4/_static/image55.png "rozšíření simulátoru iPhonu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-660">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="af6f1-661">*rozšíření simulátoru iPhonu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-661">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="af6f1-662">Přečtěte si a přijměte smlouvu EULA pro rozšíření.</span><span class="sxs-lookup"><span data-stu-id="af6f1-662">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="af6f1-663">![Smlouva EULA rozšíření WebMatrix](whats-new-in-aspnet-mvc-4/_static/image56.png "Smlouva EULA rozšíření WebMatrix")</span><span class="sxs-lookup"><span data-stu-id="af6f1-663">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="af6f1-664">*Smlouva EULA rozšíření WebMatrix*</span><span class="sxs-lookup"><span data-stu-id="af6f1-664">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="af6f1-665">Nyní můžete web spustit z WebMatrixu pomocí možnosti simulátoru iPhonu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-665">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="af6f1-666">![Spustit pomocí iPhonu](whats-new-in-aspnet-mvc-4/_static/image57.png "Spustit pomocí iPhonu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-666">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="af6f1-667">*Spustit pomocí iPhonu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-667">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="af6f1-668">Úloha 3 – konfigurace sady Visual Studio 2012 pro spuštění simulátoru iPhonu</span><span class="sxs-lookup"><span data-stu-id="af6f1-668">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="af6f1-669">Otevřete **Visual Studio 2012** a otevřete libovolný web nebo vytvořte nový projekt.</span><span class="sxs-lookup"><span data-stu-id="af6f1-669">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="af6f1-670">Klikněte na šipku dolů na tlačítku spustit a vyberte **Procházet pomocí**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-670">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="af6f1-671">![Procházet](whats-new-in-aspnet-mvc-4/_static/image58.png "Procházet")</span><span class="sxs-lookup"><span data-stu-id="af6f1-671">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="af6f1-672">*Procházet*</span><span class="sxs-lookup"><span data-stu-id="af6f1-672">*Browse with*</span></span>
3. <span data-ttu-id="af6f1-673">V dialogovém okně &quot;procházení&quot; klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-673">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="af6f1-674">V dialogovém okně &quot;přidat program&quot; použijte následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="af6f1-674">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="af6f1-675">**Program**: C:\Users\*{CurrentUser} \* \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(aktualizujte cestu odpovídajícím způsobem)*</span><span class="sxs-lookup"><span data-stu-id="af6f1-675">**Program**: C:\Users\*{CurrentUser}\*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)*</span></span>
   - <span data-ttu-id="af6f1-676">**Argumenty**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="af6f1-676">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="af6f1-677">**Popisný název**: simulátor pro iPhone</span><span class="sxs-lookup"><span data-stu-id="af6f1-677">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="af6f1-678">![Přidat program](whats-new-in-aspnet-mvc-4/_static/image59.png "Přidat program")</span><span class="sxs-lookup"><span data-stu-id="af6f1-678">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="af6f1-679">*Přidat program pro procházení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-679">*Add program to browse with*</span></span>
5. <span data-ttu-id="af6f1-680">Klikněte na **OK** a zavřete dialogová okna.</span><span class="sxs-lookup"><span data-stu-id="af6f1-680">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="af6f1-681">Nyní je možné spouštět webové aplikace v simulátoru iPhone ze sady Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="af6f1-681">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="af6f1-682">![Procházet simulátorem iPhone](whats-new-in-aspnet-mvc-4/_static/image60.png "Procházet simulátorem iPhone")</span><span class="sxs-lookup"><span data-stu-id="af6f1-682">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="af6f1-683">*Procházet simulátorem iPhone*</span><span class="sxs-lookup"><span data-stu-id="af6f1-683">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="af6f1-684">Příloha D: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="af6f1-684">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="af6f1-685">V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="af6f1-685">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="af6f1-686">Úloha 1 – Vytvoření nového webu z portálu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="af6f1-686">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="af6f1-687">Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="af6f1-687">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-688">S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-688">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="af6f1-689">[Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="af6f1-689">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="af6f1-690">![Přihlaste se k Windows Azure Portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Přihlaste se k Windows Azure Portal")</span><span class="sxs-lookup"><span data-stu-id="af6f1-690">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="af6f1-691">*Přihlášení k Windows Azure Portál pro správu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-691">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="af6f1-692">Na panelu příkazů klikněte na **Nový** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-692">Click **New** on the command bar.</span></span>

    <span data-ttu-id="af6f1-693">![Vytvoření nového webu](whats-new-in-aspnet-mvc-4/_static/image62.png "Vytvoření nového webu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-693">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="af6f1-694">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-694">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="af6f1-695">Klikněte na **compute** | **Web**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-695">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="af6f1-696">Pak vyberte možnost **rychlé vytvoření** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-696">Then select **Quick Create** option.</span></span> <span data-ttu-id="af6f1-697">Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-697">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-698">Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat.</span><span class="sxs-lookup"><span data-stu-id="af6f1-698">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="af6f1-699">Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál.</span><span class="sxs-lookup"><span data-stu-id="af6f1-699">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="af6f1-700">Nezahrnuje kroky pro nastavení databáze.</span><span class="sxs-lookup"><span data-stu-id="af6f1-700">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="af6f1-701">![Vytvoření nového webu pomocí rychlého vytvoření](whats-new-in-aspnet-mvc-4/_static/image63.png "Vytvoření nového webu pomocí rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="af6f1-701">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="af6f1-702">*Vytvoření nového webu pomocí rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="af6f1-702">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="af6f1-703">Počkejte, než se nový **Web** vytvoří.</span><span class="sxs-lookup"><span data-stu-id="af6f1-703">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="af6f1-704">Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-704">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="af6f1-705">Ověřte, zda nový web funguje.</span><span class="sxs-lookup"><span data-stu-id="af6f1-705">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="af6f1-706">![Procházení na nový web](whats-new-in-aspnet-mvc-4/_static/image64.png "Procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="af6f1-706">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="af6f1-707">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="af6f1-707">*Browsing to the new web site*</span></span>

    <span data-ttu-id="af6f1-708">![Běžící Web](whats-new-in-aspnet-mvc-4/_static/image65.png "Běžící Web")</span><span class="sxs-lookup"><span data-stu-id="af6f1-708">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="af6f1-709">*Běžící Web*</span><span class="sxs-lookup"><span data-stu-id="af6f1-709">*Web site running*</span></span>
6. <span data-ttu-id="af6f1-710">Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-710">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="af6f1-711">![Otevření stránek správy webu](whats-new-in-aspnet-mvc-4/_static/image66.png "Otevření stránek správy webu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-711">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="af6f1-712">*Otevření stránek správy webu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-712">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="af6f1-713">Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-713">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-714">*Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-714">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="af6f1-715">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace.</span><span class="sxs-lookup"><span data-stu-id="af6f1-715">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="af6f1-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="af6f1-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="af6f1-717">![Stahuje se publikační profil webu.](whats-new-in-aspnet-mvc-4/_static/image67.png "Stahuje se publikační profil webu.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-717">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="af6f1-718">*Stahuje se publikační profil webu.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-718">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="af6f1-719">Stáhněte si soubor profilu publikování do známého umístění.</span><span class="sxs-lookup"><span data-stu-id="af6f1-719">Download the publish profile file to a known location.</span></span> <span data-ttu-id="af6f1-720">V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af6f1-720">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="af6f1-721">![Ukládání souboru profilu publikování](whats-new-in-aspnet-mvc-4/_static/image68.png "Ukládá se publikační profil.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-721">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="af6f1-722">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="af6f1-722">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="af6f1-723">Úloha 2 – Konfigurace databázového serveru</span><span class="sxs-lookup"><span data-stu-id="af6f1-723">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="af6f1-724">Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="af6f1-724">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="af6f1-725">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="af6f1-725">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="af6f1-726">Pro uložení aplikační databáze budete potřebovat server SQL Database.</span><span class="sxs-lookup"><span data-stu-id="af6f1-726">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="af6f1-727">SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-727">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="af6f1-728">Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="af6f1-728">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="af6f1-729">Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách.</span><span class="sxs-lookup"><span data-stu-id="af6f1-729">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="af6f1-730">Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="af6f1-730">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="af6f1-731">![Řídicí panel serveru SQL Database](whats-new-in-aspnet-mvc-4/_static/image69.png "Řídicí panel serveru SQL Database")</span><span class="sxs-lookup"><span data-stu-id="af6f1-731">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="af6f1-732">*Řídicí panel serveru SQL Database*</span><span class="sxs-lookup"><span data-stu-id="af6f1-732">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="af6f1-733">V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru.</span><span class="sxs-lookup"><span data-stu-id="af6f1-733">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="af6f1-734">Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](whats-new-in-aspnet-mvc-4/_static/image70.png).</span><span class="sxs-lookup"><span data-stu-id="af6f1-734">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![Přidává se IP adresa klienta.](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="af6f1-736">*Přidává se IP adresa klienta.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-736">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="af6f1-737">Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="af6f1-737">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrdit změny](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="af6f1-739">*Potvrdit změny*</span><span class="sxs-lookup"><span data-stu-id="af6f1-739">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="af6f1-740">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="af6f1-740">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="af6f1-741">Vraťte se do řešení ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="af6f1-741">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="af6f1-742">V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-742">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="af6f1-743">![Publikování aplikace](whats-new-in-aspnet-mvc-4/_static/image73.png "Publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="af6f1-743">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="af6f1-744">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-744">*Publishing the web site*</span></span>
2. <span data-ttu-id="af6f1-745">Importujte profil publikování, který jste uložili v prvním úkolu.</span><span class="sxs-lookup"><span data-stu-id="af6f1-745">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="af6f1-746">![Import profilu publikování](whats-new-in-aspnet-mvc-4/_static/image74.png "Import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="af6f1-746">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="af6f1-747">*Importuje se publikační profil.*</span><span class="sxs-lookup"><span data-stu-id="af6f1-747">*Importing publish profile*</span></span>
3. <span data-ttu-id="af6f1-748">Klikněte na **ověřit připojení**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-748">Click **Validate Connection**.</span></span> <span data-ttu-id="af6f1-749">Po dokončení ověřování klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-749">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6f1-750">Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-750">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="af6f1-751">![Ověřování připojení](whats-new-in-aspnet-mvc-4/_static/image75.png "Ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="af6f1-751">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="af6f1-752">*Ověřování připojení*</span><span class="sxs-lookup"><span data-stu-id="af6f1-752">*Validating connection*</span></span>
4. <span data-ttu-id="af6f1-753">Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="af6f1-753">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="af6f1-754">![Konfigurace nasazení webu](whats-new-in-aspnet-mvc-4/_static/image76.png "Konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="af6f1-754">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="af6f1-755">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="af6f1-755">*Web deploy configuration*</span></span>
5. <span data-ttu-id="af6f1-756">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="af6f1-756">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="af6f1-757">Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="af6f1-757">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="af6f1-758">V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="af6f1-758">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="af6f1-759">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="af6f1-759">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="af6f1-760">Zadejte nový název databáze, například: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="af6f1-760">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="af6f1-761">![Konfigurace cílového připojovacího řetězce](whats-new-in-aspnet-mvc-4/_static/image77.png "Konfigurace cílového připojovacího řetězce")</span><span class="sxs-lookup"><span data-stu-id="af6f1-761">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="af6f1-762">*Konfigurace cílového připojovacího řetězce*</span><span class="sxs-lookup"><span data-stu-id="af6f1-762">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="af6f1-763">Pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-763">Then click **OK**.</span></span> <span data-ttu-id="af6f1-764">Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-764">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="af6f1-765">![Vytvoření databáze](whats-new-in-aspnet-mvc-4/_static/image78.png "Vytváří se řetězec databáze.")</span><span class="sxs-lookup"><span data-stu-id="af6f1-765">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="af6f1-766">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="af6f1-766">*Creating the database*</span></span>
7. <span data-ttu-id="af6f1-767">Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení.</span><span class="sxs-lookup"><span data-stu-id="af6f1-767">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="af6f1-768">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-768">Then click **Next**.</span></span>

    <span data-ttu-id="af6f1-769">![Připojovací řetězec ukazující na SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Připojovací řetězec ukazující na SQL Database")</span><span class="sxs-lookup"><span data-stu-id="af6f1-769">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="af6f1-770">*Připojovací řetězec ukazující na SQL Database*</span><span class="sxs-lookup"><span data-stu-id="af6f1-770">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="af6f1-771">Na stránce **Náhled** klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="af6f1-771">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="af6f1-772">![Publikování webové aplikace](whats-new-in-aspnet-mvc-4/_static/image80.png "Publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="af6f1-772">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="af6f1-773">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="af6f1-773">*Publishing the web application*</span></span>
9. <span data-ttu-id="af6f1-774">Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.</span><span class="sxs-lookup"><span data-stu-id="af6f1-774">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="af6f1-775">![Aplikace byla publikována na platformě Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Aplikace byla publikována na platformě Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="af6f1-775">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="af6f1-776">*Aplikace byla publikována na platformě Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="af6f1-776">*Application published to Windows Azure*</span></span>
