---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 'Praktická cvičení: Visual Studio 2013 Web Tools | Microsoft Docs'
author: rick-anderson
description: Visual Studio je vynikající vývojové prostředí pro. SÍTĚ Windows a webové projekty. Obsahuje výkonný textový editor, který lze snadno použít k...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622673"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="b4b26-104">Praktické cvičení: Webové nástroje v sadě Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b4b26-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>

<span data-ttu-id="b4b26-105">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b4b26-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b4b26-106">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="b4b26-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="b4b26-107">Visual Studio je vynikající vývojové prostředí pro. SÍTĚ Windows a webové projekty.</span><span class="sxs-lookup"><span data-stu-id="b4b26-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="b4b26-108">Obsahuje výkonný textový editor, který lze snadno použít pro úpravu samostatných souborů bez projektu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="b4b26-109">Visual Studio při úpravách jednotlivých souborů udržuje plně vybavený strom analýzy.</span><span class="sxs-lookup"><span data-stu-id="b4b26-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="b4b26-110">To umožňuje, aby aplikace Visual Studio poskytovala neparalelní automatické dokončování a akce založené na dokumentech a prováděly vývojové prostředí mnohem rychleji a lépe příjemný.</span><span class="sxs-lookup"><span data-stu-id="b4b26-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="b4b26-111">Tyto funkce jsou zvláště výkonné v dokumentech HTML a CSS.</span><span class="sxs-lookup"><span data-stu-id="b4b26-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="b4b26-112">Všechna tato napájení jsou taky dostupná pro rozšíření, což usnadňuje rozšíření editorů o výkonné nové funkce, které vyhovují vašim potřebám.</span><span class="sxs-lookup"><span data-stu-id="b4b26-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="b4b26-113">Web Essentials je kolekce (převážně) vylepšení pro web, která se týkají sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="b4b26-114">Zahrnuje spoustu nových doplňování technologie IntelliSense (zejména pro CSS), nové funkce pro propojení prohlížeče, automatické JSHint pro soubory JavaScriptu, nová upozornění pro HTML a CSS a řadu dalších funkcí, které jsou nezbytné pro moderní vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="b4b26-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="b4b26-115">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="b4b26-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="b4b26-116">Přehled</span><span class="sxs-lookup"><span data-stu-id="b4b26-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b4b26-117">Cíle</span><span class="sxs-lookup"><span data-stu-id="b4b26-117">Objectives</span></span>

<span data-ttu-id="b4b26-118">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="b4b26-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="b4b26-119">Používejte nové funkce editoru HTML, které jsou součástí webových základních prvků, jako jsou například bohatý fragmenty kódu HTML5 a kódování Zen.</span><span class="sxs-lookup"><span data-stu-id="b4b26-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="b4b26-120">Používejte nové funkce editoru šablon stylů CSS, které jsou součástí sady Web Essentials, jako je výběr barvy a popis matice v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="b4b26-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="b4b26-121">Použití nových funkcí editoru JavaScriptu, které jsou součástí webu Essentials, jako je extrakce souborů a IntelliSense pro všechny elementy HTML</span><span class="sxs-lookup"><span data-stu-id="b4b26-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="b4b26-122">Výměna dat mezi prohlížečem a Visual Studio pomocí odkazu v prohlížeči</span><span class="sxs-lookup"><span data-stu-id="b4b26-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b4b26-123">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="b4b26-123">Prerequisites</span></span>

<span data-ttu-id="b4b26-124">Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:</span><span class="sxs-lookup"><span data-stu-id="b4b26-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="b4b26-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="b4b26-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="b4b26-126">Web Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="b4b26-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="b4b26-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="b4b26-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b4b26-128">Nastavení</span><span class="sxs-lookup"><span data-stu-id="b4b26-128">Setup</span></span>

<span data-ttu-id="b4b26-129">Aby bylo možné spustit cvičení v této praktické laboratorní laboratoři, budete muset nejprve nastavit prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4b26-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="b4b26-130">Otevřete okno Průzkumníka Windows a přejděte do **zdrojové** složky testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4b26-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="b4b26-131">Klikněte pravým tlačítkem na **Setup. cmd** a vyberte **Spustit jako správce** a spusťte proces instalace, který bude konfigurovat vaše prostředí a nainstaluje fragmenty kódu sady Visual Studio pro toto testovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4b26-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="b4b26-132">Pokud se zobrazí dialogové okno Řízení uživatelských účtů, potvrďte akci, abyste mohli pokračovat.</span><span class="sxs-lookup"><span data-stu-id="b4b26-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b26-133">Před spuštěním instalačního programu se ujistěte, že jste kontrolovali všechny závislosti pro toto testovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4b26-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="b4b26-134">Používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="b4b26-134">Using the Code Snippets</span></span>

<span data-ttu-id="b4b26-135">V celém dokumentu testovacího prostředí budete vyzváni k vložení bloků kódu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="b4b26-136">Pro usnadnění práce je většina tohoto kódu k dispozici jako fragmenty Visual Studio Code, ke kterým můžete přistupovat z Visual Studio 2013, abyste se vyhnuli nutnosti ho přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="b4b26-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b26-137">Každé cvičení se doprovází od počátečního řešení ve složce **Begin** cvičení, které vám umožní sledovat jednotlivá cvičení nezávisle na ostatních.</span><span class="sxs-lookup"><span data-stu-id="b4b26-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="b4b26-138">Všimněte si, že fragmenty kódu, které jsou přidány během cvičení, v těchto počátečních řešeních chybí a nemusí fungovat, dokud nedokončíte cvičení.</span><span class="sxs-lookup"><span data-stu-id="b4b26-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="b4b26-139">Ve zdrojovém kódu cvičení také najdete **koncovou** složku obsahující řešení sady Visual Studio s kódem, který je výsledkem dokončení kroků v příslušném cvičení.</span><span class="sxs-lookup"><span data-stu-id="b4b26-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="b4b26-140">Tato řešení můžete použít jako návod, pokud potřebujete další pomoc při práci s tímto praktickým cvičením.</span><span class="sxs-lookup"><span data-stu-id="b4b26-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b4b26-141">Cvičení</span><span class="sxs-lookup"><span data-stu-id="b4b26-141">Exercises</span></span>

<span data-ttu-id="b4b26-142">Tato praktická cvičení zahrnují následující cvičení:</span><span class="sxs-lookup"><span data-stu-id="b4b26-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="b4b26-143">Práce s odkazem na prohlížeč a Web Essentials</span><span class="sxs-lookup"><span data-stu-id="b4b26-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="b4b26-144">Využití fragmentů kódu a IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b4b26-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="b4b26-145">Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení.</span><span class="sxs-lookup"><span data-stu-id="b4b26-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="b4b26-146">Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="b4b26-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="b4b26-147">Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="b4b26-148">Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.</span><span class="sxs-lookup"><span data-stu-id="b4b26-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="b4b26-149">Cvičení 1: práce s odkazem na prohlížeč a Web Essentials</span><span class="sxs-lookup"><span data-stu-id="b4b26-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="b4b26-150">**Web Essentials** je rozšíření sady Visual Studio, které přináší řadu užitečných funkcí pro moderní vývoj webů, hlavně zaměřené na to, aby bylo prostředí vývoje webu mnohem rychlejší a příjemný.</span><span class="sxs-lookup"><span data-stu-id="b4b26-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="b4b26-151">Web Essentials můžete nainstalovat z galerie rozšíření v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="b4b26-152">**Odkaz na prohlížeč** je nová funkce, která je součástí Visual Studio 2013, která poskytuje kanál mezi rozhraním IDE sady Visual Studio a jakýmkoli otevřeným prohlížečem pro výměnu dat mezi webovou aplikací a Visual Studiem.</span><span class="sxs-lookup"><span data-stu-id="b4b26-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="b4b26-153">Web Essentials rozšiřuje prohlížeč s nástroji pro manipulaci s modelem objektu DOM a styly CSS vašich webových stránek přímo z prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b4b26-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="b4b26-154">V tomto cvičení prozkoumáte některé funkce, které podporuje **Web Essentials** a **Browser Link** , k vylepšení jednoduché stránky kvízu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="b4b26-155">Úloha 1 – spuštění projektu v několika prohlížečích</span><span class="sxs-lookup"><span data-stu-id="b4b26-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="b4b26-156">V této úloze nakonfigurujete webovou aplikaci tak, aby běžela v několika prohlížečích najednou, což je užitečné pro testování v různých prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="b4b26-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="b4b26-157">Otevřete **Microsoft Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="b4b26-158">V nabídce **soubor** vyberte **otevřít | Projekt nebo řešení...** a přejděte do složky **EX1-WorkingwithBrowserLinkandWebEssentials\Begin** ve **zdrojové** složce testovacího prostředí (C:\WebCampsTK\HOL\VSWebTooling\Source).</span><span class="sxs-lookup"><span data-stu-id="b4b26-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="b4b26-159">Vyberte možnost **Begin. sln** a klikněte na tlačítko **otevřít**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="b4b26-160">Na panelu nástrojů sady Visual Studio rozbalte nabídku prohlížeč a vyberte **Procházet pomocí...** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="b4b26-161">![Možnost Procházet s možností nabídky](visual-studio-2013-web-tools/_static/image1.png "Procházet pomocí... v nabídce prohlížeče")</span><span class="sxs-lookup"><span data-stu-id="b4b26-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="b4b26-162">*Možnost Procházet s možností nabídky*</span><span class="sxs-lookup"><span data-stu-id="b4b26-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="b4b26-163">V dialogovém okně **Procházet se systémem** vyberte **Google Chrome** a **Internet Explorer** tak, že podržíte klávesu **CTRL** a kliknete na **nastavit jako výchozí**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="b4b26-164">![Procházet s – dialogové okno](visual-studio-2013-web-tools/_static/image2.png "Procházet s – dialogové okno")</span><span class="sxs-lookup"><span data-stu-id="b4b26-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="b4b26-165">*Výběr několika výchozích prohlížečů*</span><span class="sxs-lookup"><span data-stu-id="b4b26-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="b4b26-166">Jako výchozí prohlížeč by se teď měly zobrazovat Google Chrome a Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b4b26-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="b4b26-167">Kliknutím na tlačítko **Storno** zavřete dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="b4b26-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="b4b26-168">![Google Chrome a Internet Explorer jako výchozí prohlížeče](visual-studio-2013-web-tools/_static/image3.png "Výchozí prohlížeče Google Chrome a Internet Exploreru")</span><span class="sxs-lookup"><span data-stu-id="b4b26-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="b4b26-169">*Google Chrome a Internet Explorer jako výchozí prohlížeče*</span><span class="sxs-lookup"><span data-stu-id="b4b26-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-170">Po konfiguraci výchozích prohlížečů se v nabídce prohlížeče vybere možnost **více prohlížečů** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="b4b26-171">![Více prohlížečů](visual-studio-2013-web-tools/_static/image4.png "Více prohlížečů")</span><span class="sxs-lookup"><span data-stu-id="b4b26-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="b4b26-172">Stisknutím **kombinace kláves CTRL** + **F5** spusťte aplikaci bez ladění.</span><span class="sxs-lookup"><span data-stu-id="b4b26-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="b4b26-173">Pokud jsou okna prohlížeče otevřená, umístěte jeden z nich nad druhý, aby se aktualizace zobrazily současně na obou prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="b4b26-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="b4b26-174">V prohlížečích by se měla zobrazit webová stránka s světle modrým obdélníkem.</span><span class="sxs-lookup"><span data-stu-id="b4b26-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="b4b26-175">![Umístění jednoho prohlížeče nad druhý](visual-studio-2013-web-tools/_static/image5.png "Umístění jednoho prohlížeče nad druhý")</span><span class="sxs-lookup"><span data-stu-id="b4b26-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="b4b26-176">*Umístění jednoho prohlížeče nad druhý*</span><span class="sxs-lookup"><span data-stu-id="b4b26-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="b4b26-177">Nezavírejte prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b4b26-177">Do not close the browsers.</span></span> <span data-ttu-id="b4b26-178">Budete je používat v dalším úkolu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="b4b26-179">Úkol 2 – použití kódování Zen k vytváření elementů jazyka HTML</span><span class="sxs-lookup"><span data-stu-id="b4b26-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="b4b26-180">**Zen** Code je modul plug-in editoru pro vysokorychlostní HTML, XML, XSL (nebo jakýkoli jiný formát strukturovaného kódu), který můžete kódovat a upravovat.</span><span class="sxs-lookup"><span data-stu-id="b4b26-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="b4b26-181">Jádrem tohoto modulu plug-in je výkonný modul zkratky, který umožňuje rozšířit výrazy podobné selektorům CSS v kódu HTML.</span><span class="sxs-lookup"><span data-stu-id="b4b26-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="b4b26-182">Kódování Zen je rychlý způsob, jak psát kód HTML pomocí syntaxe selektoru stylu CSS.</span><span class="sxs-lookup"><span data-stu-id="b4b26-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="b4b26-183">V tomto cvičení použijete funkci kódování Zen poskytovanou nástrojem Web Essentials k vygenerování tlačítek HTML, která reprezentují možnosti otázky.</span><span class="sxs-lookup"><span data-stu-id="b4b26-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="b4b26-184">Přepněte zpět do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="b4b26-185">Otevřete soubor **index. cshtml** umístěný v **zobrazeních** | **domovské** složce.</span><span class="sxs-lookup"><span data-stu-id="b4b26-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="b4b26-186">Nahrazení **&lt;!--TODO: sem přidejte možnosti--&gt;** komentář s následujícím kódem a stiskněte klávesu **TAB**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="b4b26-187">Kód by měl být rozšířen na HTML.</span><span class="sxs-lookup"><span data-stu-id="b4b26-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="b4b26-188">![Rozšířené HTML](visual-studio-2013-web-tools/_static/image6.png "Rozšířené HTML")</span><span class="sxs-lookup"><span data-stu-id="b4b26-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="b4b26-189">*Rozšířené HTML*</span><span class="sxs-lookup"><span data-stu-id="b4b26-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-190">Další informace o syntaxi kódování Zen najdete v následujícím [článku](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span><span class="sxs-lookup"><span data-stu-id="b4b26-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="b4b26-191">Kliknutím na tlačítko **Aktualizovat propojené prohlížeče** aktualizujte oba prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b4b26-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="b4b26-192">![Aktualizovat propojené prohlížeče](visual-studio-2013-web-tools/_static/image7.png "Aktualizovat propojené prohlížeče")</span><span class="sxs-lookup"><span data-stu-id="b4b26-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="b4b26-193">*Aktualizovat propojené prohlížeče*</span><span class="sxs-lookup"><span data-stu-id="b4b26-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="b4b26-194">![Internet Explorer – stránka se aktualizovala pomocí čtyř tlačítek](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer – stránka se aktualizovala pomocí čtyř tlačítek")</span><span class="sxs-lookup"><span data-stu-id="b4b26-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="b4b26-195">*Internet Explorer – stránka se aktualizovala pomocí čtyř tlačítek*</span><span class="sxs-lookup"><span data-stu-id="b4b26-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="b4b26-196">![Google Chrome – stránka se aktualizovala se čtyřmi tlačítky](visual-studio-2013-web-tools/_static/image9.png "Google Chrome – stránka se aktualizovala se čtyřmi tlačítky")</span><span class="sxs-lookup"><span data-stu-id="b4b26-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="b4b26-197">*Google Chrome – stránka se aktualizovala se čtyřmi tlačítky*</span><span class="sxs-lookup"><span data-stu-id="b4b26-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="b4b26-198">Přepněte zpět do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="b4b26-199">Přidali jste tlačítka na stránku, ale stále potřebujete přidat otázku šablony.</span><span class="sxs-lookup"><span data-stu-id="b4b26-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="b4b26-200">K tomu budete používat novou funkci ve Web Essentials s názvem **Lorem Ipsum Generator**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="b4b26-201">Vyhledejte element **div** s atributem **třídy** **front**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="b4b26-202">Přidejte následující kód jako první podřízený prvek **div**a stiskněte klávesu **TAB**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="b4b26-203">Kód by měl být rozšířen na HTML.</span><span class="sxs-lookup"><span data-stu-id="b4b26-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="b4b26-204">![Lorem Ipsum automaticky generovaný](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span><span class="sxs-lookup"><span data-stu-id="b4b26-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="b4b26-205">*Lorem Ipsum automaticky generovaný*</span><span class="sxs-lookup"><span data-stu-id="b4b26-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-206">Jako součást kódování Zen nyní můžete vytvořit Lore Ipsum kód přímo v editoru HTML.</span><span class="sxs-lookup"><span data-stu-id="b4b26-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="b4b26-207">Stačí napsat typ **Lorem** a stiskněte **kartu** a 30 slov Lorem Ipsum text.</span><span class="sxs-lookup"><span data-stu-id="b4b26-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="b4b26-208">Například</span><span class="sxs-lookup"><span data-stu-id="b4b26-208">E.g.</span></span> <span data-ttu-id="b4b26-209">*lorem10* vloží 10 lorech Ipsum slov.</span><span class="sxs-lookup"><span data-stu-id="b4b26-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="b4b26-210">Do horní části otázky přidáte logo pomocí jiné nové funkce ve webové části Web Essentials označované jako **generátor lorech pixelů**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="b4b26-211">Přidejte následující kód jako první podřízený prvek elementu **div** s **kontejnerem** jako hodnotu **třídy** a stiskněte klávesu **TAB**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="b4b26-212">Kód by měl být rozšířen na HTML.</span><span class="sxs-lookup"><span data-stu-id="b4b26-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="b4b26-213">![Automaticky vygenerované v lorech pixelech](visual-studio-2013-web-tools/_static/image11.png "Automaticky vygenerované v lorech pixelech")</span><span class="sxs-lookup"><span data-stu-id="b4b26-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="b4b26-214">*Automaticky vygenerované v lorech pixelech*</span><span class="sxs-lookup"><span data-stu-id="b4b26-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-215">Jako součást kódování Zen můžete také vygenerovat kód Lorech pixelů přímo v editoru HTML.</span><span class="sxs-lookup"><span data-stu-id="b4b26-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="b4b26-216">Stačí zadat **pix – 200x200-** animales a stiskněte **kartu** a značku **img** s 200x200 obrázkem zvíře se vloží.</span><span class="sxs-lookup"><span data-stu-id="b4b26-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="b4b26-217">Další informace najdete v tématu [lorech pixelů](http://www.lorempixel.com).</span><span class="sxs-lookup"><span data-stu-id="b4b26-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="b4b26-218">Kliknutím na tlačítko **Aktualizovat propojené prohlížeče** aktualizujte oba prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b4b26-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="b4b26-219">![Internet Explorer – automaticky vygenerovaný obrázek a text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer – automaticky vygenerovaný obrázek a text")</span><span class="sxs-lookup"><span data-stu-id="b4b26-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="b4b26-220">*Internet Explorer – automaticky vygenerovaný obrázek a text*</span><span class="sxs-lookup"><span data-stu-id="b4b26-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="b4b26-221">![Google Chrome – automaticky vygenerovaný obrázek a text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome – automaticky vygenerovaný obrázek a text")</span><span class="sxs-lookup"><span data-stu-id="b4b26-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="b4b26-222">*Google Chrome – automaticky vygenerovaný obrázek a text*</span><span class="sxs-lookup"><span data-stu-id="b4b26-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-223">Vzhledem k tomu, že obrázek je vybrán náhodně při přidávání fragmentu kódu, obrázek zobrazený v prohlížečích se může lišit.</span><span class="sxs-lookup"><span data-stu-id="b4b26-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="b4b26-224">Nezavírejte prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b4b26-224">Do not close the browsers.</span></span> <span data-ttu-id="b4b26-225">Budete je používat v dalším úkolu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="b4b26-226">Úloha 3 – aktualizace vlastnosti Style</span><span class="sxs-lookup"><span data-stu-id="b4b26-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="b4b26-227">V této úloze použijete funkci **kontrolního režimu** odkazu v prohlížeči ke zjištění přesného umístění, kde je vygenerován konkrétní element modelu DOM, a poté aktualizujete vlastnost Color daného elementu pomocí výběru barvy, který poskytuje sada Web Essentials.</span><span class="sxs-lookup"><span data-stu-id="b4b26-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="b4b26-228">V prohlížeči Internet Explorer stiskněte **CTRL** + **ALT** + **I** , aby se povolil režim kontroly.</span><span class="sxs-lookup"><span data-stu-id="b4b26-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="b4b26-229">Přesuňte ukazatel myši na světle modrý okraj a klikněte na.</span><span class="sxs-lookup"><span data-stu-id="b4b26-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="b4b26-230">![Přesunutí ukazatele na světle modrý okraj](visual-studio-2013-web-tools/_static/image14.png "Přesunutí ukazatele na světle modrý okraj")</span><span class="sxs-lookup"><span data-stu-id="b4b26-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="b4b26-231">*Přesunutí ukazatele na světle modrý okraj*</span><span class="sxs-lookup"><span data-stu-id="b4b26-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="b4b26-232">Přepněte zpět do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="b4b26-233">Všimněte si, jak je prvek jazyka HTML, který jste vybrali v prohlížeči, vybrán také v editoru HTML sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="b4b26-234">![HTML element vybraný v editoru HTML sady Visual Studio](visual-studio-2013-web-tools/_static/image15.png "HTML element vybraný v editoru HTML sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="b4b26-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="b4b26-235">*HTML element vybraný v editoru HTML sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="b4b26-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="b4b26-236">Nyní aktualizujete **přední** třídu CSS, aby bylo možné změnit styl vybraného elementu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="b4b26-237">Provedete **to tak,** že stisknutím **kombinace kláves CTRL** + otevřete vyhledávací pole **Navigovat** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="b4b26-238">Zadejte **site. CSS** a stisknutím klávesy **ENTER** soubor otevřete.</span><span class="sxs-lookup"><span data-stu-id="b4b26-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="b4b26-239">![Otevírá se soubor Web. CSS.](visual-studio-2013-web-tools/_static/image16.png "Otevírá se soubor Web. CSS.")</span><span class="sxs-lookup"><span data-stu-id="b4b26-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="b4b26-240">*Otevírá se soubor Web. CSS.*</span><span class="sxs-lookup"><span data-stu-id="b4b26-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="b4b26-241">Stisknutím **kombinace kláves CTRL** + **F** a zadáním **. Flip-Container. zepředu** Najděte Selektor šablon stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="b4b26-241">Press **CTRL** + **F** and type **.flip-container .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="b4b26-242">Kliknutím na světle modrý čtverec ve vlastnosti Border třídy otevřete výběr barvy.</span><span class="sxs-lookup"><span data-stu-id="b4b26-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="b4b26-243">![Otevření výběru barvy](visual-studio-2013-web-tools/_static/image17.png "Otevření výběru barvy")</span><span class="sxs-lookup"><span data-stu-id="b4b26-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="b4b26-244">*Otevření výběru barvy*</span><span class="sxs-lookup"><span data-stu-id="b4b26-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="b4b26-245">Rozbalte výběr barvy kliknutím na tlačítko s dvojitou šipkou a výběrem nové barvy.</span><span class="sxs-lookup"><span data-stu-id="b4b26-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="b4b26-246">![Rozbalení výběru barvy](visual-studio-2013-web-tools/_static/image18.png "Rozbalení výběru barvy")</span><span class="sxs-lookup"><span data-stu-id="b4b26-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="b4b26-247">*Rozbalení výběru barvy*</span><span class="sxs-lookup"><span data-stu-id="b4b26-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="b4b26-248">Stisknutím **kombinace kláves CTRL** + **ALT** + **ENTER** aktualizujte propojené prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b4b26-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="b4b26-249">Přepněte do aplikace Internet Explorer a Všimněte si, jak se změnila barva ohraničení.</span><span class="sxs-lookup"><span data-stu-id="b4b26-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="b4b26-250">![Internet Explorer – aktualizace barvy ohraničení](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer – aktualizace barvy ohraničení")</span><span class="sxs-lookup"><span data-stu-id="b4b26-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="b4b26-251">*Internet Explorer – aktualizace barvy ohraničení*</span><span class="sxs-lookup"><span data-stu-id="b4b26-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="b4b26-252">Přepněte na Google Chrome a Všimněte si, jak se změnila barva ohraničení.</span><span class="sxs-lookup"><span data-stu-id="b4b26-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="b4b26-253">![Google Chrome – aktualizace barvy ohraničení](visual-studio-2013-web-tools/_static/image20.png "Google Chrome – aktualizace barvy ohraničení")</span><span class="sxs-lookup"><span data-stu-id="b4b26-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="b4b26-254">*Google Chrome – aktualizace barvy ohraničení*</span><span class="sxs-lookup"><span data-stu-id="b4b26-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="b4b26-255">Přepněte zpět do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="b4b26-256">Přejděte na konec souboru **Web. CSS** a stisknutím klávesy **CTRL** + **F** Najděte selektor **. btn** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="b4b26-257">Všimněte si, že vlastnost **-WebKit-Border-RADIUS** je podtržená zeleně.</span><span class="sxs-lookup"><span data-stu-id="b4b26-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="b4b26-258">![-WebKit-Border-vlastnost poloměru pro selektor BTN](visual-studio-2013-web-tools/_static/image21.png "-WebKit-Border-vlastnost poloměru pro selektor BTN")</span><span class="sxs-lookup"><span data-stu-id="b4b26-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="b4b26-259">*-WebKit-Border-vlastnost poloměru pro selektor BTN*</span><span class="sxs-lookup"><span data-stu-id="b4b26-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="b4b26-260">Umístěte blikající kurzor do vlastnosti **-WebKit-Border-RADIUS** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="b4b26-261">Pod prvním písmenem prvního slova v této vlastnosti by se měla zobrazit modrá čára.</span><span class="sxs-lookup"><span data-stu-id="b4b26-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="b4b26-262">Toto je **inteligentní značka**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="b4b26-263">Stiskněte klávesu **CTRL** +  **.**</span><span class="sxs-lookup"><span data-stu-id="b4b26-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="b4b26-264">Chcete-li otevřít nabídku návrhy a klikněte na tlačítko **Přidat chybějící standardní vlastnost (Border-RADIUS)** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="b4b26-265">![Přidat chybějící návrh standardní vlastnosti](visual-studio-2013-web-tools/_static/image22.png "Přidat chybějící návrh standardní vlastnosti")</span><span class="sxs-lookup"><span data-stu-id="b4b26-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="b4b26-266">*Přidat chybějící návrh standardní vlastnosti*</span><span class="sxs-lookup"><span data-stu-id="b4b26-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="b4b26-267">Vlastnost **border-RADIUS** je automaticky přidána do pravidla šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="b4b26-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="b4b26-268">![Nebyla přidána standardní vlastnost.](visual-studio-2013-web-tools/_static/image23.png "Nebyla přidána standardní vlastnost.")</span><span class="sxs-lookup"><span data-stu-id="b4b26-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="b4b26-269">*Nebyla přidána standardní vlastnost.*</span><span class="sxs-lookup"><span data-stu-id="b4b26-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="b4b26-270">Přesuňte ukazatel na vlastnost **border-RADIUS** , abyste zobrazili **Popis matice v prohlížeči**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="b4b26-271">**Popisek matice prohlížeče** zobrazuje dostupnost vlastnosti v jednotlivých prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="b4b26-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="b4b26-272">![Popis matice v prohlížeči](visual-studio-2013-web-tools/_static/image24.png "Popis matice v prohlížeči")</span><span class="sxs-lookup"><span data-stu-id="b4b26-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="b4b26-273">*Popis matice v prohlížeči*</span><span class="sxs-lookup"><span data-stu-id="b4b26-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="b4b26-274">Všimněte si, že hodnota vlastnosti **border-RADIUS** je pořád podtržená.</span><span class="sxs-lookup"><span data-stu-id="b4b26-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="b4b26-275">Přesunutím ukazatele nad hodnotu zobrazíte zprávu s upozorněním.</span><span class="sxs-lookup"><span data-stu-id="b4b26-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="b4b26-276">![Border – upozornění na hodnotu vlastnosti protokolu RADIUS](visual-studio-2013-web-tools/_static/image25.png "Border – upozornění na hodnotu vlastnosti protokolu RADIUS")</span><span class="sxs-lookup"><span data-stu-id="b4b26-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="b4b26-277">*Border – upozornění na hodnotu vlastnosti protokolu RADIUS*</span><span class="sxs-lookup"><span data-stu-id="b4b26-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="b4b26-278">Odeberte jednotku hodnoty vlastnosti **border-RADIUS** navrhovanou popisem tlačítka.</span><span class="sxs-lookup"><span data-stu-id="b4b26-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="b4b26-279">Jako **border – poloměr** je standardní vlastnost pro definování, jak jsou zaoblené rohy ohraničení, a vlastnost **-WebKit-Border-RADIUS** můžete z pravidla CSS odebrat.</span><span class="sxs-lookup"><span data-stu-id="b4b26-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="b4b26-280">Umístěte blikající kurzor do vlastnosti **zalamování řádků** a Všimněte si, že inteligentní značka se zobrazí také níže.</span><span class="sxs-lookup"><span data-stu-id="b4b26-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="b4b26-281">Otevřete nabídku a klikněte na možnost **Přidat chybějící konkrétní dodavatele**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="b4b26-282">![Přidat návrh chybějících konkrétních dodavatelů](visual-studio-2013-web-tools/_static/image26.png "Přidat návrh chybějících konkrétních dodavatelů")</span><span class="sxs-lookup"><span data-stu-id="b4b26-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="b4b26-283">*Přidat návrh chybějících konkrétních dodavatelů*</span><span class="sxs-lookup"><span data-stu-id="b4b26-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="b4b26-284">Vlastnost **-MS-Word-Wrap** je automaticky přidána do pravidla šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="b4b26-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="b4b26-285">![Přidána vlastnost specifická pro dodavatele](visual-studio-2013-web-tools/_static/image27.png "Přidána vlastnost specifická pro dodavatele")</span><span class="sxs-lookup"><span data-stu-id="b4b26-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="b4b26-286">*Přidána vlastnost specifická pro dodavatele*</span><span class="sxs-lookup"><span data-stu-id="b4b26-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="b4b26-287">Úloha 4 – aktualizace kódu HTML z prohlížeče</span><span class="sxs-lookup"><span data-stu-id="b4b26-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="b4b26-288">V této úloze použijete funkci **návrhového režimu** odkazu prohlížeče pro úpravu objektu DOM z prohlížeče a přenos změn do zdrojového souboru HTML v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4b26-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="b4b26-289">V Google Chrome stiskněte **CTRL** + **ALT** + **D** pro povolení režimu návrhu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="b4b26-290">Přesuňte ukazatel myši na štítek **Lorem Ipsum dolor Sit Amet** a klikněte na.</span><span class="sxs-lookup"><span data-stu-id="b4b26-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="b4b26-291">![Úprava otázky](visual-studio-2013-web-tools/_static/image28.png "Úprava otázky")</span><span class="sxs-lookup"><span data-stu-id="b4b26-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="b4b26-292">*Úprava otázky*</span><span class="sxs-lookup"><span data-stu-id="b4b26-292">*Editing the question*</span></span>
3. <span data-ttu-id="b4b26-293">Měl by se zobrazit kurzor.</span><span class="sxs-lookup"><span data-stu-id="b4b26-293">A cursor should appear.</span></span> <span data-ttu-id="b4b26-294">Nahraďte původní text tak, jak vypadá, *když napíšem delší otázku?* , a potom stisknutím klávesy **ESC** Ukončete režim návrhu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="b4b26-295">![Upravený dotaz](visual-studio-2013-web-tools/_static/image29.png "Upravený dotaz")</span><span class="sxs-lookup"><span data-stu-id="b4b26-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="b4b26-296">*Upravený dotaz*</span><span class="sxs-lookup"><span data-stu-id="b4b26-296">*Question edited*</span></span>
4. <span data-ttu-id="b4b26-297">Přepněte zpátky do sady Visual Studio a otevřete **index. cshtml**, pokud ještě není otevřený.</span><span class="sxs-lookup"><span data-stu-id="b4b26-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="b4b26-298">Všimněte si, že vnitřní text prvku **&lt;p&gt;** byl aktualizován.</span><span class="sxs-lookup"><span data-stu-id="b4b26-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="b4b26-299">![Aktualizace otázky na stránce HTML](visual-studio-2013-web-tools/_static/image30.png "Aktualizace otázky na stránce HTML")</span><span class="sxs-lookup"><span data-stu-id="b4b26-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="b4b26-300">*Aktualizace otázky na stránce HTML*</span><span class="sxs-lookup"><span data-stu-id="b4b26-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="b4b26-301">Úloha 5-Kontrola upozornění spojených s SEO</span><span class="sxs-lookup"><span data-stu-id="b4b26-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="b4b26-302">**Optimalizace** vyhledávače (SEO) je proces, který je v seznamu výsledků vyhledávacího webu vyšší.</span><span class="sxs-lookup"><span data-stu-id="b4b26-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="b4b26-303">Čím vyšší je pořadí lokality a čím více je v seznamu uvedeno, tím více návštěvníkům získá web z tohoto vyhledávacího stroje.</span><span class="sxs-lookup"><span data-stu-id="b4b26-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="b4b26-304">Web Essentials zahrnuje analytický nástroj, který prověřuje kód HTML, oznamuje zjištěné problémy a poskytuje pomoc při jejich opravě.</span><span class="sxs-lookup"><span data-stu-id="b4b26-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="b4b26-305">Přejděte do nabídky **zobrazení** a kliknutím na **Seznam chyb** otevřete okno **Seznam chyb** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="b4b26-306">![Seznam chyb v nabídce zobrazení](visual-studio-2013-web-tools/_static/image31.png "Seznam chyb v nabídce zobrazení")</span><span class="sxs-lookup"><span data-stu-id="b4b26-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="b4b26-307">*Seznam chyb v nabídce zobrazení*</span><span class="sxs-lookup"><span data-stu-id="b4b26-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="b4b26-308">Všimněte si, že došlo k upozornění na stránku SEO upozorňující na to, že chybí **&lt;Značka meta&gt;** pro popis stránky.</span><span class="sxs-lookup"><span data-stu-id="b4b26-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="b4b26-309">Dvakrát klikněte na položku upozornění SEO, abyste ji opravili.</span><span class="sxs-lookup"><span data-stu-id="b4b26-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="b4b26-310">![Seznam chyb okno](visual-studio-2013-web-tools/_static/image32.png "okno Seznam chyb")</span><span class="sxs-lookup"><span data-stu-id="b4b26-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="b4b26-311">*Seznam chyb okno*</span><span class="sxs-lookup"><span data-stu-id="b4b26-311">*Error List window*</span></span>
3. <span data-ttu-id="b4b26-312">Kliknutím na tlačítko **Ano** v dialogovém okně **Web Essentials** vložíte popis &lt;meta&gt; tag.</span><span class="sxs-lookup"><span data-stu-id="b4b26-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="b4b26-313">![Dialogové okno Web Essentials](visual-studio-2013-web-tools/_static/image33.png "Dialogové okno Web Essentials")</span><span class="sxs-lookup"><span data-stu-id="b4b26-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="b4b26-314">*Dialogové okno Web Essentials*</span><span class="sxs-lookup"><span data-stu-id="b4b26-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="b4b26-315">Editor pro **\_layout. cshtml** se otevře a **&lt;Značka meta&gt;** je automaticky přidána do části **head** v souboru HTML.</span><span class="sxs-lookup"><span data-stu-id="b4b26-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="b4b26-316">![Meta značka automaticky přidána na _Layout stránce](visual-studio-2013-web-tools/_static/image34.png "Meta značka automaticky přidána na _Layout stránce")</span><span class="sxs-lookup"><span data-stu-id="b4b26-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="b4b26-317">*Meta značka se automaticky přidala do \_rozložení stránky.*</span><span class="sxs-lookup"><span data-stu-id="b4b26-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="b4b26-318">Změňte hodnotu atributu **Content** na *GeekQuiz* a uložte soubor.</span><span class="sxs-lookup"><span data-stu-id="b4b26-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="b4b26-319">Cvičení 2: využití fragmentů kódu a IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b4b26-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="b4b26-320">V případě aplikace Web Essentials byl Editor HTML rozšířen o další funkce.</span><span class="sxs-lookup"><span data-stu-id="b4b26-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="b4b26-321">V tomto cvičení se zobrazí některé nové funkce, které jsou užitečné při vývoji webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="b4b26-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="b4b26-322">Úloha 1 – použití IntelliSense v dokumentech HTML</span><span class="sxs-lookup"><span data-stu-id="b4b26-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="b4b26-323">První nová funkce, kterou se zobrazí v této úloze, se nazývá **Dynamická technologie IntelliSense**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="b4b26-324">Dynamická technologie IntelliSense čte jiné značky a atributy pro odvození možných ID, která budete používat.</span><span class="sxs-lookup"><span data-stu-id="b4b26-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="b4b26-325">V této úloze vytvoříte nový prvek formuláře HTML, který obsahuje popisek a vstupní pole.</span><span class="sxs-lookup"><span data-stu-id="b4b26-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="b4b26-326">Pak přidáte atribut **pro** k popisku, který ho sváže se vstupem, a uvidíte návrhy IntelliSense na základě ID vstupů v oboru.</span><span class="sxs-lookup"><span data-stu-id="b4b26-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="b4b26-327">Otevřete **Visual Studio Express 2013 pro web** a řešení **Begin. sln** nacházející se ve složce **source/EX2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="b4b26-328">Případně můžete pokračovat v řešení, které jste získali v předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="b4b26-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="b4b26-329">V **Průzkumník řešení**otevřete soubor **index. cshtml** umístěný v **zobrazeních** | **domovské** složce.</span><span class="sxs-lookup"><span data-stu-id="b4b26-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="b4b26-330">Do **oddílu&lt;&gt;** elementu přidejte následující formulář.</span><span class="sxs-lookup"><span data-stu-id="b4b26-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="b4b26-331">(Fragment kódu – *VisualStudio2013WebTooling* - *EX2* - *formulář*)</span><span class="sxs-lookup"><span data-stu-id="b4b26-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="b4b26-332">Vstupní značka by měla předcházet návěští s nějakým popisem pole.</span><span class="sxs-lookup"><span data-stu-id="b4b26-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="b4b26-333">Přidejte následující popisek před vstupní značku.</span><span class="sxs-lookup"><span data-stu-id="b4b26-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="b4b26-334">Atribut **for** **&lt;Label&gt;** určuje, na který prvek formuláře je popisek svázán.</span><span class="sxs-lookup"><span data-stu-id="b4b26-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="b4b26-335">Hodnota atributu musí být rovna ID souvisejícího prvku.</span><span class="sxs-lookup"><span data-stu-id="b4b26-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="b4b26-336">Přidejte atribut **pro** **&lt;popisku&gt;** elementu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="b4b26-337">Jak je znázorněno na následujícím obrázku, &quot;název&quot; hodnota se zobrazí v poli IntelliSense na základě ID prvků v rámci stejného oboru (ohraničující **&lt;formuláře&gt;** ).</span><span class="sxs-lookup"><span data-stu-id="b4b26-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="b4b26-338">![Zobrazení ID v IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Zobrazení ID v IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="b4b26-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="b4b26-339">*Zobrazení ID v IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="b4b26-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="b4b26-340">Odstraní naposledy přidaný **&lt;&gt;** element a jeho obsah.</span><span class="sxs-lookup"><span data-stu-id="b4b26-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="b4b26-341">Úloha 2 – používání fragmentů kódu HTML</span><span class="sxs-lookup"><span data-stu-id="b4b26-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="b4b26-342">HTML5 zavedlo více než 25 nových sémantických značek.</span><span class="sxs-lookup"><span data-stu-id="b4b26-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="b4b26-343">Visual Studio již pro tyto značky podporuje technologii IntelliSense, ale Visual Studio 2013 rychlejší a snadnější psaní značek přidáním nových fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="b4b26-344">I když tyto značky nejsou komplikované, jsou dodávány s několika malými odlišností, jako je například přidání správných záložních kodeků pro *zvukovou* značku.</span><span class="sxs-lookup"><span data-stu-id="b4b26-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="b4b26-345">V této úloze se zobrazí fragmenty kódu HTML pro značku zvuku.</span><span class="sxs-lookup"><span data-stu-id="b4b26-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="b4b26-346">Do souboru **index. cshtml** zadejte **&lt;AUD** dovnitř **&lt;oddílu&gt;** elementu, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="b4b26-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="b4b26-347">![Vložení prvku zvuk](visual-studio-2013-web-tools/_static/image36.png "Vložení prvku zvuk")</span><span class="sxs-lookup"><span data-stu-id="b4b26-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="b4b26-348">*Vložení prvku zvuk*</span><span class="sxs-lookup"><span data-stu-id="b4b26-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="b4b26-349">Stiskněte **tabulátor** dvakrát a Všimněte si, jak se na stránce přidá následující kód a kurzor se umístí do atributu **Src** prvního zdroje.</span><span class="sxs-lookup"><span data-stu-id="b4b26-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="b4b26-350">Po kliknutí na klávesu **TAB** dvakrát dojde k vložení fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="b4b26-351">Fragment zvuku zobrazuje standardní použití *zvukové* značky se dvěma zdrojovými soubory pro lepší podporu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="b4b26-352">Odstraňte druhý řádek a aktualizujte zdroj prvního řádku následujícím odkazem na WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span><span class="sxs-lookup"><span data-stu-id="b4b26-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="b4b26-353">Výsledný kód je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="b4b26-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="b4b26-354">Zdrojový soubor *KatanaProject. mp3* se používá jako příklad.</span><span class="sxs-lookup"><span data-stu-id="b4b26-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="b4b26-355">Pokud budete chtít, můžete použít jiný zdroj.</span><span class="sxs-lookup"><span data-stu-id="b4b26-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="b4b26-356">Soubor uložte stisknutím **kombinace kláves CTRL** + **S** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="b4b26-357">Stisknutím **kombinace kláves CTRL** + **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b4b26-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="b4b26-358">Všimněte si, že se do aplikace přidal zvukový přehrávač.</span><span class="sxs-lookup"><span data-stu-id="b4b26-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="b4b26-359">![Zvukový přehrávač v aplikaci Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Zvukový přehrávač v aplikaci Internet Explorer")</span><span class="sxs-lookup"><span data-stu-id="b4b26-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="b4b26-360">*Zvukový přehrávač v aplikaci Internet Explorer*</span><span class="sxs-lookup"><span data-stu-id="b4b26-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="b4b26-361">![Audio Player v Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio Player v Google Chrome")</span><span class="sxs-lookup"><span data-stu-id="b4b26-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="b4b26-362">*Audio Player v Google Chrome*</span><span class="sxs-lookup"><span data-stu-id="b4b26-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="b4b26-363">Nezavírejte prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b4b26-363">Do not close the browsers.</span></span> <span data-ttu-id="b4b26-364">Budete je používat v dalším úkolu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="b4b26-365">Úloha 3 – použití IntelliSense v dokumentech JavaScript</span><span class="sxs-lookup"><span data-stu-id="b4b26-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="b4b26-366">S Web Essentials 2013, šablony stylů a stránky HTML vytvoří seznam identifikátorů a názvů tříd.</span><span class="sxs-lookup"><span data-stu-id="b4b26-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="b4b26-367">V této úloze se dozvíte, jak tyto seznamy zlepšují podporu technologie IntelliSense v jazyce JavaScript v Web Essentials 2013.</span><span class="sxs-lookup"><span data-stu-id="b4b26-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="b4b26-368">V souboru **index. cshtml** přidejte následující kód pro definování značky **skriptu** pro kód jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b4b26-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="b4b26-369">Přidejte následující kód do značky **Script** pro definování funkce zpětného volání připravenosti.</span><span class="sxs-lookup"><span data-stu-id="b4b26-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="b4b26-370">(Fragment kódu – *VisualStudio2013WebTooling* - *EX2* - *ReadyFunction*)</span><span class="sxs-lookup"><span data-stu-id="b4b26-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="b4b26-371">Umístěte blikající kurzor do značky **Script** a stiskněte klávesu **CTRL** +  **.**</span><span class="sxs-lookup"><span data-stu-id="b4b26-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="b4b26-372">pro otevření nabídky návrh.</span><span class="sxs-lookup"><span data-stu-id="b4b26-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="b4b26-373">Klikněte na **extrahovat do souboru**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="b4b26-374">![Extrakce JavaScriptu do souboru návrhu](visual-studio-2013-web-tools/_static/image39.png "Extrakce JavaScriptu do souboru návrhu")</span><span class="sxs-lookup"><span data-stu-id="b4b26-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="b4b26-375">*Extrakce JavaScriptu do souboru návrhu*</span><span class="sxs-lookup"><span data-stu-id="b4b26-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="b4b26-376">V okně **Uložit jako** vyberte složku **skripty** , pojmenujte soubor **init. js** a klikněte na **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="b4b26-377">![Uložit jako okno](visual-studio-2013-web-tools/_static/image40.png "Uložit jako okno")</span><span class="sxs-lookup"><span data-stu-id="b4b26-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="b4b26-378">*Uložit jako okno*</span><span class="sxs-lookup"><span data-stu-id="b4b26-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-379">Vytvoří se soubor **init. js** a obsah skriptu se přesune do souboru.</span><span class="sxs-lookup"><span data-stu-id="b4b26-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="b4b26-380">![Soubor init. js vytvořený pomocí zahrnutého obsahu](visual-studio-2013-web-tools/_static/image41.png "Soubor init. js vytvořený pomocí zahrnutého obsahu")</span><span class="sxs-lookup"><span data-stu-id="b4b26-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="b4b26-381">*Soubor init. js vytvořený pomocí zahrnutého obsahu*</span><span class="sxs-lookup"><span data-stu-id="b4b26-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="b4b26-382">Otevřete soubor **index. cshtml** a ověřte, zda byla značka skriptu nahrazena odkazem na soubor **init. js** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="b4b26-383">![Reference k souboru init. js HTML](visual-studio-2013-web-tools/_static/image42.png "Reference k souboru init. js HTML")</span><span class="sxs-lookup"><span data-stu-id="b4b26-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="b4b26-384">*Reference k souboru init. js HTML*</span><span class="sxs-lookup"><span data-stu-id="b4b26-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="b4b26-385">Přejít na **Průzkumník řešení** a Všimněte si, že soubor **init. js** byl automaticky zahrnut do řešení.</span><span class="sxs-lookup"><span data-stu-id="b4b26-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="b4b26-386">![Soubor init. js zahrnutý v řešení](visual-studio-2013-web-tools/_static/image43.png "Soubor init. js zahrnutý v řešení")</span><span class="sxs-lookup"><span data-stu-id="b4b26-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="b4b26-387">*Soubor init. js zahrnutý v řešení*</span><span class="sxs-lookup"><span data-stu-id="b4b26-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="b4b26-388">Přepněte zpět do souboru **init. js** a aktualizujte tak **připravené** zpětné volání funkce.</span><span class="sxs-lookup"><span data-stu-id="b4b26-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="b4b26-389">Uvnitř definice zpětného volání funkce, která je předána *připravenému*, přidejte následující kód, který získá všechny prvky pomocí konkrétního atributu Class.</span><span class="sxs-lookup"><span data-stu-id="b4b26-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="b4b26-390">Stiskněte klávesu **CTRL** + **mezeru** mezi uvozovky uvnitř volání funkce **getElementsByClassName** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="b4b26-391">![Zobrazení technologie IntelliSense pro funkci getElementsByClassName](visual-studio-2013-web-tools/_static/image44.png "Zobrazení technologie IntelliSense pro funkci getElementsByClassName")</span><span class="sxs-lookup"><span data-stu-id="b4b26-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="b4b26-392">*Zobrazení technologie IntelliSense pro funkci getElementsByClassName*</span><span class="sxs-lookup"><span data-stu-id="b4b26-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-393">Všimněte si, že technologie IntelliSense zobrazuje třídy definované v šablonách stylů projektu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="b4b26-394">Nahraďte řádek, který jste vytvořili, pomocí následujícího kódu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="b4b26-395">Umístěte kurzor po **au** do uvozovek ve funkci **GetElementsByTagName** a stiskněte klávesy **CTRL** + **MEZERNÍK**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="b4b26-396">![Zobrazení IntelliSense pro metodu getElementByTagName](visual-studio-2013-web-tools/_static/image45.png "Zobrazení IntelliSense pro metodu getElementByTagName")</span><span class="sxs-lookup"><span data-stu-id="b4b26-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="b4b26-397">*Zobrazení IntelliSense pro metodu getElementsByTagName*</span><span class="sxs-lookup"><span data-stu-id="b4b26-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="b4b26-398">Ze seznamu vyberte **&quot;audio&quot;** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="b4b26-399">Výsledek je znázorněn na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="b4b26-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="b4b26-400">![Načítání elementů zvuku](visual-studio-2013-web-tools/_static/image46.png "Načítání elementů zvuku")</span><span class="sxs-lookup"><span data-stu-id="b4b26-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="b4b26-401">*Načítání elementů zvuku*</span><span class="sxs-lookup"><span data-stu-id="b4b26-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="b4b26-402">V **Průzkumník řešení**klikněte pravým tlačítkem myši na soubor **init. js** ve složce **Scripts** a v nabídce **Web Essentials** vyberte **minimalizuje soubory JavaScriptu** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="b4b26-403">![Soubory JavaScriptu minimalizuje](visual-studio-2013-web-tools/_static/image47.png "Soubory JavaScriptu minimalizuje")</span><span class="sxs-lookup"><span data-stu-id="b4b26-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="b4b26-404">*Soubory JavaScriptu minimalizuje*</span><span class="sxs-lookup"><span data-stu-id="b4b26-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="b4b26-405">Po zobrazení výzvy k povolení automatického minifikace, když se změní zdrojový soubor, klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="b4b26-406">![Povolení automatického upozornění minifikace](visual-studio-2013-web-tools/_static/image48.png "Povolení automatického upozornění minifikace")</span><span class="sxs-lookup"><span data-stu-id="b4b26-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="b4b26-407">*Povolení automatického upozornění minifikace*</span><span class="sxs-lookup"><span data-stu-id="b4b26-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4b26-408">Je vytvořen soubor **init. min. js** a je přidán jako závislost souboru **init. js** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="b4b26-409">![Byl vytvořen soubor init. min. js.](visual-studio-2013-web-tools/_static/image49.png "Byl vytvořen soubor init. min. js.")</span><span class="sxs-lookup"><span data-stu-id="b4b26-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="b4b26-410">*Byl vytvořen soubor init. min. js.*</span><span class="sxs-lookup"><span data-stu-id="b4b26-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="b4b26-411">Otevřete soubor **init. min. js** a Všimněte si, že soubor je minifikovaného.</span><span class="sxs-lookup"><span data-stu-id="b4b26-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="b4b26-412">![Obsah souboru init. min. js](visual-studio-2013-web-tools/_static/image50.png "Obsah souboru init. min. js")</span><span class="sxs-lookup"><span data-stu-id="b4b26-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="b4b26-413">*Obsah souboru init. min. js*</span><span class="sxs-lookup"><span data-stu-id="b4b26-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="b4b26-414">V souboru **init. js** přidejte následující kód pod voláním funkce **GetElementsByTagName** , aby se hrály všechny zvukové prvky.</span><span class="sxs-lookup"><span data-stu-id="b4b26-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="b4b26-415">(Fragment kódu – *VisualStudio2013WebTooling* - *EX2* - *PlayAudioElements*)</span><span class="sxs-lookup"><span data-stu-id="b4b26-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="b4b26-416">Uložte soubor kliknutím na tlačítko **CTRL** + **S** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="b4b26-417">Vzhledem k tomu, že soubor minifikovaného je již otevřen, zobrazí se dialogové okno s informacemi o tom, že soubor byl změněn mimo editor zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="b4b26-418">Klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="b4b26-418">Click **Yes**.</span></span>

    <span data-ttu-id="b4b26-419">![Upozornění Microsoft Visual Studio](visual-studio-2013-web-tools/_static/image51.png "Upozornění Microsoft Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="b4b26-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="b4b26-420">*Upozornění Microsoft Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="b4b26-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="b4b26-421">Přepněte zpět do souboru **init. min. js** a ověřte, zda byl soubor aktualizován pomocí nového kódu.</span><span class="sxs-lookup"><span data-stu-id="b4b26-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="b4b26-422">![Soubor init. min. js se aktualizoval.](visual-studio-2013-web-tools/_static/image52.png "Soubor init. min. js se aktualizoval.")</span><span class="sxs-lookup"><span data-stu-id="b4b26-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="b4b26-423">*Soubor init. min. js se aktualizoval.*</span><span class="sxs-lookup"><span data-stu-id="b4b26-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="b4b26-424">Klikněte na tlačítko **aktualizovat propojení prohlížeče** .</span><span class="sxs-lookup"><span data-stu-id="b4b26-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="b4b26-425">Po obnovení obou prohlížečů se zvukové přehrávače, které jste viděli v předchozí úloze, začnou automaticky přehrávat.</span><span class="sxs-lookup"><span data-stu-id="b4b26-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="b4b26-426">![Zvukový přehrávač zahrnutý v zobrazení](visual-studio-2013-web-tools/_static/image53.png "Zvukový přehrávač zahrnutý v zobrazení")</span><span class="sxs-lookup"><span data-stu-id="b4b26-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="b4b26-427">*Zvukový přehrávač zahrnutý v zobrazení*</span><span class="sxs-lookup"><span data-stu-id="b4b26-427">*Audio player included in view*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b4b26-428">Souhrn</span><span class="sxs-lookup"><span data-stu-id="b4b26-428">Summary</span></span>

<span data-ttu-id="b4b26-429">Vyplněním tohoto praktického cvičení jste se dozvěděli, jak:</span><span class="sxs-lookup"><span data-stu-id="b4b26-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="b4b26-430">Používejte nové funkce editoru HTML, které jsou součástí webových základních prvků, jako jsou například bohatý fragmenty kódu HTML5 a kódování Zen.</span><span class="sxs-lookup"><span data-stu-id="b4b26-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="b4b26-431">Používejte nové funkce editoru šablon stylů CSS, které jsou součástí sady Web Essentials, jako je výběr barvy a popis matice v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="b4b26-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="b4b26-432">Použití nových funkcí editoru JavaScriptu, které jsou součástí webu Essentials, jako je extrakce souborů a IntelliSense pro všechny elementy HTML</span><span class="sxs-lookup"><span data-stu-id="b4b26-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="b4b26-433">Výměna dat mezi prohlížečem a Visual Studio pomocí odkazu v prohlížeči</span><span class="sxs-lookup"><span data-stu-id="b4b26-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
