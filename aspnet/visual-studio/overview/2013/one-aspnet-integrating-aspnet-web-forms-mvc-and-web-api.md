---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 'Praktická cvičení: jedna ASP.NET: integrace webových formulářů ASP.NET, MVC a webového rozhraní API | Microsoft Docs'
author: rick-anderson
description: ASP.NET je architektura pro vytváření webů, aplikací a služeb s využitím specializovaných technologií, jako je MVC, webové rozhraní API a další. S rozšířením ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623198"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="9a1d9-104">Praktické cvičení: jeden ASP.NET: Integrace webových formulářů ASP.NET, MVC a webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="9a1d9-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>

<span data-ttu-id="9a1d9-105">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="9a1d9-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="9a1d9-106">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="9a1d9-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="9a1d9-107">ASP.NET je architektura pro vytváření webů, aplikací a služeb s využitím specializovaných technologií, jako je MVC, webové rozhraní API a další.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="9a1d9-108">S rozšířením ASP.NET se od jeho vytvoření objevila a vyjádřily se, že tyto technologie jsou integrované, ale bylo nedávno vyvíjené úsilí při práci na **jednom ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="9a1d9-109">Visual Studio 2013 zavádí nový jednotný projektový systém, který umožňuje sestavit aplikaci a používat všechny technologie ASP.NET v jednom projektu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="9a1d9-110">Tato funkce eliminuje nutnost vybírat jednu technologii na začátku projektu a místo toho je doporučuje použít více ASP.NETch architektur v rámci jednoho projektu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="9a1d9-111">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="9a1d9-111">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="9a1d9-112">Přehled</span><span class="sxs-lookup"><span data-stu-id="9a1d9-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="9a1d9-113">Cíle</span><span class="sxs-lookup"><span data-stu-id="9a1d9-113">Objectives</span></span>

<span data-ttu-id="9a1d9-114">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="9a1d9-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="9a1d9-115">Vytvoření webu založeného na jednom typu projektu **ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="9a1d9-116">Použijte různé **ASP.NET** architektury, jako je **MVC** a **webové rozhraní API** , ve stejném projektu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="9a1d9-117">Identifikujte hlavní součásti aplikace **ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="9a1d9-118">Využijte rozhraní **ASP.NET pro generování uživatelského rozhraní** k automatickému vytvoření řadičů a zobrazení k provádění operací CRUD na základě tříd modelu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="9a1d9-119">Vystavte stejnou sadu informací v formátech strojového a uživatelsky čitelném pomocí správného nástroje pro každou úlohu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="9a1d9-120">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="9a1d9-120">Prerequisites</span></span>

<span data-ttu-id="9a1d9-121">Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:</span><span class="sxs-lookup"><span data-stu-id="9a1d9-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="9a1d9-122">[Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/) nebo více</span><span class="sxs-lookup"><span data-stu-id="9a1d9-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="9a1d9-123">Visual Studio 2013 Update 1</span><span class="sxs-lookup"><span data-stu-id="9a1d9-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="9a1d9-124">Nastavení</span><span class="sxs-lookup"><span data-stu-id="9a1d9-124">Setup</span></span>

<span data-ttu-id="9a1d9-125">Aby bylo možné spustit cvičení v této praktické laboratorní laboratoři, budete muset nejprve nastavit prostředí.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="9a1d9-126">Otevřete Průzkumníka Windows a přejděte do **zdrojové** složky testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="9a1d9-127">Klikněte pravým tlačítkem na **Setup. cmd** a vyberte **Spustit jako správce** a spusťte proces instalace, který bude konfigurovat vaše prostředí a nainstaluje fragmenty kódu sady Visual Studio pro toto testovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="9a1d9-128">Pokud se zobrazí dialogové okno Řízení uživatelských účtů, potvrďte akci, abyste mohli pokračovat.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="9a1d9-129">Před spuštěním instalačního programu se ujistěte, že jste kontrolovali všechny závislosti pro toto testovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="9a1d9-130">Používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="9a1d9-130">Using the Code Snippets</span></span>

<span data-ttu-id="9a1d9-131">V celém dokumentu testovacího prostředí budete vyzváni k vložení bloků kódu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="9a1d9-132">Pro usnadnění práce je většina tohoto kódu k dispozici jako fragmenty Visual Studio Code, ke kterým můžete přistupovat z Visual Studio 2013, abyste se vyhnuli nutnosti ho přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="9a1d9-133">Každé cvičení se doprovází od počátečního řešení ve složce **Begin** cvičení, které vám umožní sledovat jednotlivá cvičení nezávisle na ostatních.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="9a1d9-134">Všimněte si, že fragmenty kódu, které jsou přidány během cvičení, v těchto počátečních řešeních chybí a nemusí fungovat, dokud nedokončíte cvičení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="9a1d9-135">Ve zdrojovém kódu cvičení také najdete **koncovou** složku obsahující řešení sady Visual Studio s kódem, který je výsledkem dokončení kroků v příslušném cvičení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="9a1d9-136">Tato řešení můžete použít jako návod, pokud potřebujete další pomoc při práci s tímto praktickým cvičením.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="9a1d9-137">Cvičení</span><span class="sxs-lookup"><span data-stu-id="9a1d9-137">Exercises</span></span>

<span data-ttu-id="9a1d9-138">Tato praktická cvičení zahrnují následující cvičení:</span><span class="sxs-lookup"><span data-stu-id="9a1d9-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="9a1d9-139">Vytvoření nového projektu webových formulářů</span><span class="sxs-lookup"><span data-stu-id="9a1d9-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="9a1d9-140">Vytvoření kontroleru MVC pomocí generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="9a1d9-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="9a1d9-141">Vytvoření kontroleru webového rozhraní API pomocí generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="9a1d9-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="9a1d9-142">Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="9a1d9-143">Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="9a1d9-144">Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="9a1d9-145">Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="9a1d9-146">Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="9a1d9-147">Cvičení 1: vytvoření nového projektu webových formulářů</span><span class="sxs-lookup"><span data-stu-id="9a1d9-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="9a1d9-148">V tomto cvičení vytvoříte nový Web Forms v Visual Studio 2013 pomocí jednotného projektového prostředí **ASP.NET** , které vám umožní snadno integrovat webové formuláře, komponenty MVC a webové rozhraní API do stejné aplikace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="9a1d9-149">Pak budete prozkoumat vygenerované řešení a Identifikujte jeho části a nakonec uvidíte web v akci.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="9a1d9-150">Úloha 1 – Vytvoření nového webu s využitím jednoho ASP.NETového prostředí</span><span class="sxs-lookup"><span data-stu-id="9a1d9-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="9a1d9-151">V této úloze začnete vytvářet nový web v aplikaci Visual Studio na základě jednoho typu projektu **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="9a1d9-152">**Jedna ASP.neta** sjednocuje všechny technologie ASP.NET a dává vám možnost je podle potřeby kombinovat a odpovídat.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="9a1d9-153">Pak rozpoznáváte různé komponenty webových formulářů, MVC a webového rozhraní API, které se nachází v rámci aplikace vedle sebe.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="9a1d9-154">Otevřete **Visual Studio Express 2013 pro web** a vyberte **soubor | Nový projekt...** pro spuštění nového řešení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![Vytvoření nového projektu](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="9a1d9-156">*Vytvoření nového projektu*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="9a1d9-157">V dialogovém okně **Nový projekt** vyberte v části vizuál  **C# možnost Webová aplikace v ASP.NET | Kartu Web** a ujistěte se, že je vybrána možnost **.NET Framework 4,5** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="9a1d9-158">Pojmenujte projekt *MyHybridSite*, vyberte **umístění** a klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![Nový projekt webové aplikace v ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="9a1d9-160">*Vytvoření nového projektu webové aplikace v ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="9a1d9-161">V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu **webové formuláře** a vyberte možnosti **MVC** a **webové rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="9a1d9-162">Také se ujistěte, že je možnost **ověřování** nastavena na **jednotlivé uživatelské účty**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="9a1d9-163">Pokračujte kliknutím na tlačítko **OK** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-163">Click **OK** to continue.</span></span>

    ![Vytvoření nového projektu pomocí šablony webových formulářů, včetně komponent webového rozhraní API a MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="9a1d9-165">*Vytvoření nového projektu pomocí šablony webových formulářů, včetně komponent webového rozhraní API a MVC*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="9a1d9-166">Nyní můžete prozkoumat strukturu vygenerovaného řešení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-166">You can now explore the structure of the generated solution.</span></span>

    ![Zkoumání vygenerovaného řešení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="9a1d9-168">*Zkoumání vygenerovaného řešení*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="9a1d9-169">**Účet:** Tato složka obsahuje stránky webového formuláře k registraci, přihlášení a správu uživatelských účtů aplikace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="9a1d9-170">Tato složka se přidá, pokud je při konfiguraci šablony projektu webové formuláře vybrána možnost ověřování **individuálních uživatelských účtů** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="9a1d9-171">**Modely:** Tato složka bude obsahovat třídy, které reprezentují data vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="9a1d9-172">**Řadiče** a **zobrazení**: tyto složky jsou vyžadovány pro komponenty **webového rozhraní API** **ASP.NET MVC** a ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="9a1d9-173">V následujících cvičeních budete zkoumat technologie MVC a webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="9a1d9-174">Soubory **Default. aspx**, **Contact. aspx** a **About. aspx** jsou předem definované stránky webových formulářů, které lze použít jako výchozí body pro sestavení stránek specifických pro vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="9a1d9-175">Programovací logika těchto souborů se nachází v samostatném souboru, který je označován jako &quot;soubor&quot; s kódem na pozadí, který obsahuje &quot;. aspx. vb&quot; nebo &quot;. aspx.cs&quot; (v závislosti na používaném jazyce).</span><span class="sxs-lookup"><span data-stu-id="9a1d9-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="9a1d9-176">Logika kódu na pozadí běží na serveru a dynamicky vytváří výstup HTML stránky.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="9a1d9-177">Stránky **site. Master** a **site. Mobile. Master** definují vzhled a chování a standardní chování všech stránek v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="9a1d9-178">Dvojím kliknutím na soubor **Default. aspx** můžete prozkoumat obsah stránky.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![Prozkoumávání stránky default. aspx](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="9a1d9-180">*Prozkoumávání stránky default. aspx*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a1d9-181">Direktiva **stránky** v horní části souboru definuje atributy stránky webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="9a1d9-182">Například atribut **MasterPageFile** Určuje cestu k hlavní stránce – v tomto případě se jedná o stránku *site. Master* – a atribut **Inherits** definuje třídu kódu na pozadí pro stránku, která má dědit.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="9a1d9-183">Tato třída je umístěna v souboru určeném atributem **CodeBehind** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="9a1d9-184">Ovládací prvek **ASP: Content** obsahuje skutečný obsah stránky (text, značky a ovládací prvky) a je namapován na ovládací prvek **ASP: ContentPlaceHolder** na stránce předlohy.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="9a1d9-185">V tomto případě se obsah stránky vykreslí uvnitř ovládacího prvku *MainContent* , který je definovaný na stránce *site. Master* .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="9a1d9-186">Rozbalte **aplikaci\_spustit** složku a Všimněte si souboru **WebApiConfig.cs** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="9a1d9-187">Visual Studio zahrnulo tento soubor do vygenerovaného řešení, protože jste zahrnuli webové rozhraní API při konfiguraci projektu s jednou šablonou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="9a1d9-188">Otevřete soubor **WebApiConfig.cs** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="9a1d9-189">Ve třídě *WebApiConfig* najdete konfiguraci přidruženou k webovému rozhraní API, která MAPUJE trasy HTTP na **řadiče webového rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="9a1d9-190">Otevřete soubor **RouteConfig.cs** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="9a1d9-191">V rámci metody *RegisterRoutes* najdete konfiguraci přidruženou ke MVC, která MAPUJE trasy HTTP na **řadiče MVC**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="9a1d9-192">Úloha 2 – spuštění řešení</span><span class="sxs-lookup"><span data-stu-id="9a1d9-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="9a1d9-193">V této úloze spustíte vygenerované řešení, prozkoumejte aplikaci a některé její funkce, jako je přepis adres URL a integrované ověřování.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="9a1d9-194">Pokud chcete řešení spustit, stiskněte klávesu **F5** nebo klikněte na tlačítko **Start** , které se nachází na panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="9a1d9-195">Na domovské stránce aplikace by se měl otevřít v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-195">The application home page should open in the browser.</span></span>

    ![Spuštění řešení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="9a1d9-197">Ověřte, zda jsou vyvolány stránky webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="9a1d9-198">Pokud to chcete provést, přidejte **/Contact.aspx** k adrese URL na adresním řádku a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![Popisné adresy URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="9a1d9-200">*Popisné adresy URL*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a1d9-201">Jak vidíte, adresa URL se změní na **/Contact**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="9a1d9-202">Počínaje **ASP.NET 4**byly do webových formulářů přidány možnosti směrování adres URL, takže můžete napsat adresy url jako *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* místo *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="9a1d9-203">Další informace najdete v tématu [směrování adres URL](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span><span class="sxs-lookup"><span data-stu-id="9a1d9-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="9a1d9-204">Teď budete zkoumat tok ověřování integrovaný do aplikace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="9a1d9-205">Uděláte to tak, že kliknete na **Registrovat** v pravém horním rohu stránky.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![Registrace nového uživatele](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="9a1d9-207">*Registrace nového uživatele*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-207">*Registering a new user*</span></span>
4. <span data-ttu-id="9a1d9-208">Na stránce **zaregistrovat** zadejte **uživatelské jméno** a **heslo**a potom klikněte na **zaregistrovat**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![Registrovat stránku](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="9a1d9-210">*Registrovat stránku*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-210">*Register page*</span></span>
5. <span data-ttu-id="9a1d9-211">Aplikace registruje nový účet a uživatel je ověřený.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-211">The application registers the new account, and the user is authenticated.</span></span>

    ![Ověřeno uživatelem](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="9a1d9-213">*Ověřeno uživatelem*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-213">*User authenticated*</span></span>
6. <span data-ttu-id="9a1d9-214">Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="9a1d9-215">Cvičení 2: vytvoření kontroleru MVC pomocí generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="9a1d9-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="9a1d9-216">V tomto cvičení využijete rozhraní ASP.NET pro generování uživatelského rozhraní poskytované sadou Visual Studio k vytvoření kontroleru ASP.NET MVC 5 s akcemi a zobrazeními Razor k provádění operací CRUD, aniž byste museli psát jediný řádek kódu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="9a1d9-217">Proces generování uživatelského rozhraní použije Entity Framework Code First k vygenerování kontextu dat a schématu databáze v databázi SQL.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="9a1d9-218">**Informace o Entity Framework Code First**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="9a1d9-219">Entity Framework (EF) je objektově-relační Mapovač (ORM), který umožňuje vytvářet aplikace pro přístup k datům pomocí programování s modelem konceptuální aplikace namísto programování přímo pomocí schématu relačního úložiště.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="9a1d9-220">Pracovní postup modelování Entity Framework Code First umožňuje použít vlastní třídy domény k reprezentaci modelu, který se v EF spoléhá na použití funkcí dotazování, sledování změn a aktualizace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="9a1d9-221">Pomocí pracovního postupu Code Firstho vývoje nemusíte spouštět aplikaci vytvořením databáze nebo zadáním schématu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="9a1d9-222">Místo toho můžete napsat standardní třídy .NET, které definují nejvhodnější objekty doménového modelu pro vaši aplikaci, a Entity Framework vytvoří databázi za vás.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="9a1d9-223">Další informace o Entity Framework najdete [tady](../../../entity-framework.md).</span><span class="sxs-lookup"><span data-stu-id="9a1d9-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="9a1d9-224">Úloha 1 – Vytvoření nového modelu</span><span class="sxs-lookup"><span data-stu-id="9a1d9-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="9a1d9-225">Nyní definujete třídu **Person** , která bude modelem použitým procesem generování uživatelského rozhraní k vytvoření kontroleru MVC a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="9a1d9-226">Začnete vytvořením třídy typu **osoba** a operace CRUD v kontroleru se automaticky vytvoří pomocí funkcí generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="9a1d9-227">Otevřete **Visual Studio Express 2013 pro web** a řešení **MyHybridSite. sln** nacházející se ve složce **source/EX2-MvcScaffolding/Begin** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="9a1d9-228">Případně můžete pokračovat v řešení, které jste získali v předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="9a1d9-229">V **Průzkumník řešení**klikněte pravým tlačítkem na složku **modely** projektu **MyHybridSite** a vyberte **Přidat | Třída...** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![Přidání třídy modelu osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="9a1d9-231">*Přidání třídy modelu osoby*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="9a1d9-232">V dialogovém okně **Přidat novou položku** zadejte název souboru *Person.cs* a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![Vytvoření třídy modelu osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="9a1d9-234">*Vytvoření třídy modelu osoby*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="9a1d9-235">Obsah souboru **Person.cs** nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="9a1d9-236">Změny uložte stisknutím **kombinace kláves CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="9a1d9-237">(Fragment kódu – *BringingTogetherOneAspNet-EX2-PersonClass*)</span><span class="sxs-lookup"><span data-stu-id="9a1d9-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="9a1d9-238">V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **MyHybridSite** a vyberte **Build (sestavit**), nebo stiskněte **kombinaci kláves CTRL + SHIFT + B** a sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="9a1d9-239">Úloha 2 – Vytvoření kontroleru MVC</span><span class="sxs-lookup"><span data-stu-id="9a1d9-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="9a1d9-240">Teď, když se vytvoří model **osoby** , použijete ASP.NET MVC s Entity Framework k vytvoření akcí kontroleru CRUD a zobrazení pro **osobu**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="9a1d9-241">V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **řadiče** projektu **MyHybridSite** a vyberte **Přidat | Nová vygenerovaná položka...**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![Vytváření nového vygenerovaného kontroleru](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="9a1d9-243">*Vytváření nového vygenerovaného kontroleru*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="9a1d9-244">V dialogovém okně **Přidat vygenerované uživatelské rozhraní** vyberte **kontroler MVC 5 se zobrazeními, pomocí Entity Framework** a pak klikněte na **Přidat.**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![Výběr kontroleru MVC 5 se zobrazeními a Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="9a1d9-246">*Výběr kontroleru MVC 5 se zobrazeními a Entity Framework*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="9a1d9-247">Jako **název kontroleru**nastavte *MvcPersonController* , vyberte možnost **použít asynchronní řadič akce** a jako **třídu modelu**vyberte **Person (MyHybridSite. Models)** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![Přidání kontroleru MVC s generováním uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="9a1d9-249">*Přidání kontroleru MVC s generováním uživatelského rozhraní*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="9a1d9-250">V části **Třída kontextu dat**klikněte na **nový kontext dat..** ..</span><span class="sxs-lookup"><span data-stu-id="9a1d9-250">Under **Data context class**, click **New data context...**.</span></span>

    ![Vytvoření nového kontextu dat](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="9a1d9-252">*Vytvoření nového kontextu dat*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="9a1d9-253">V dialogovém okně **nový kontext dat** pojmenujte nový kontext dat *PersonContext* a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![Vytváření nového PersonContext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="9a1d9-255">*Vytváří se nový typ PersonContext.*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="9a1d9-256">Kliknutím na **Přidat** vytvořte nový kontroler pro **osobu** s vytvářením uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="9a1d9-257">Visual Studio potom vygeneruje akce kontroleru, kontext dat osoby a zobrazení Razor.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![Po vytvoření kontroleru MVC pomocí generování uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="9a1d9-259">*Po vytvoření kontroleru MVC pomocí generování uživatelského rozhraní*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="9a1d9-260">Otevřete soubor **MvcPersonController.cs** ve složce **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="9a1d9-261">Všimněte si, že metody akce CRUD byly vygenerovány automaticky.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="9a1d9-262">Zaškrtnutím políčka **použít asynchronní akce kontroleru** z možností generování uživatelského rozhraní v předchozích krocích aplikace Visual Studio vygeneruje asynchronní metody akcí pro všechny akce, které zahrnují přístup k datovému kontextu osoby.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="9a1d9-263">Doporučuje se používat asynchronní metody akcí pro dlouhotrvající, nevázané požadavky na procesor, aby nedošlo k tomu, aby webový server při zpracování žádosti prováděl práci.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="9a1d9-264">Úloha 3 – spuštění řešení</span><span class="sxs-lookup"><span data-stu-id="9a1d9-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="9a1d9-265">V této úloze znovu spustíte řešení a ověříte, že zobrazení pro **osobu** pracují podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="9a1d9-266">Přidáte novou osobu, která ověří, zda je úspěšně uložena do databáze.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="9a1d9-267">Stisknutím klávesy **F5** spusťte řešení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="9a1d9-268">Přejděte na **/MvcPerson**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="9a1d9-269">Zobrazí se vygenerované zobrazení, které zobrazuje seznam osob.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="9a1d9-270">Kliknutím na **vytvořit novou** přidejte novou osobu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-270">Click **Create New** to add a new person.</span></span>

    ![Navigace do zobrazení s vygenerovanými MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="9a1d9-272">*Navigace do zobrazení s vygenerovanými MVC*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="9a1d9-273">V zobrazení **vytvořit** zadejte pro osobu **jméno** a **stáří** a klikněte na **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![Přidává se nová osoba.](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="9a1d9-275">*Přidává se nová osoba.*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-275">*Adding a new person*</span></span>
5. <span data-ttu-id="9a1d9-276">Nová osoba se přidá do seznamu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-276">The new person is added to the list.</span></span> <span data-ttu-id="9a1d9-277">V seznamu element kliknutím na tlačítko **Podrobnosti** zobrazíte zobrazení podrobností osoby.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="9a1d9-278">Pak v zobrazení **podrobností** klikněte na **zpět k seznamu** a vraťte se do zobrazení seznamu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![Zobrazení podrobností osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="9a1d9-280">*Zobrazení podrobností osoby*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-280">*Person's details view*</span></span>
6. <span data-ttu-id="9a1d9-281">Kliknutím na odkaz **Odstranit** odstraňte osobu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="9a1d9-282">V zobrazení **Odstranit** klikněte na **Odstranit** a potvrďte operaci.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![Odstranění osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="9a1d9-284">*Odstranění osoby*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-284">*Deleting a person*</span></span>
7. <span data-ttu-id="9a1d9-285">Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="9a1d9-286">Cvičení 3: vytvoření kontroleru webového rozhraní API pomocí generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="9a1d9-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="9a1d9-287">Rozhraní Web API je součástí sady ASP.NET stack a je navržené pro snazší implementaci služby HTTP, obecně posílání a přijímání dat ve formátu JSON nebo XML prostřednictvím rozhraní RESTful API.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="9a1d9-288">V tomto cvičení použijete znovu generování uživatelského rozhraní ASP.NET, abyste vygenerovali webový kontroler API.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="9a1d9-289">V předchozím cvičení použijete stejné třídy **Person** a **PersonContext** , aby poskytovaly stejná data osob ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="9a1d9-290">Uvidíte, jak můžete stejné prostředky vystavovat různými způsoby v rámci stejné ASP.NET aplikace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="9a1d9-291">Úloha 1 – Vytvoření kontroleru webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="9a1d9-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="9a1d9-292">V této úloze vytvoříte nový **kontroler webového rozhraní API** , který bude zveřejňovat data osob ve formátu, ve kterém se jedná o počítač, jako je JSON.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="9a1d9-293">Pokud ještě není otevřený, otevřete **Visual Studio Express 2013 pro web** a otevřete řešení **MyHybridSite. sln** umístěné ve složce **source/EX3-WebApi/Begin** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="9a1d9-294">Případně můžete pokračovat v řešení, které jste získali v předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a1d9-295">Pokud začínáte s řešením zahájení z cvičení 3, sestavte řešení stisknutím **kombinace kláves CTRL + SHIFT + B** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="9a1d9-296">V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **řadiče** projektu **MyHybridSite** a vyberte **Přidat | Nová vygenerovaná položka...**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![Vytváření nového vygenerovaného kontroleru](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="9a1d9-298">*Vytváření nového vygenerovaného kontroleru*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="9a1d9-299">V dialogovém okně **Přidat vygenerované uživatelské rozhraní** v levém podokně vyberte **webové rozhraní API** , potom **kontroler webového rozhraní API 2 s akcemi pomocí Entity Framework** v prostředním podokně a pak klikněte na **Přidat.**</span><span class="sxs-lookup"><span data-stu-id="9a1d9-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="9a1d9-300">![Výběr kontroleru webového rozhraní API 2 s akcemi a Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Výběr kontroleru webového rozhraní API 2 s akcemi a Entity Framework")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="9a1d9-301">*Výběr kontroleru webového rozhraní API 2 s akcemi a Entity Framework*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="9a1d9-302">Jako **název kontroleru**nastavte *ApiPersonController* , vyberte možnost **použít asynchronní řadič akce** a jako **model** a třídy **kontextu dat** vyberte **Person (MyHybridSite. Models)** a **PersonContext (MyHybridSite. Models)** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="9a1d9-303">Pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-303">Then click **Add**.</span></span>

    <span data-ttu-id="9a1d9-304">![Přidání kontroleru webového rozhraní API s využitím uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Přidání kontroleru webového rozhraní API s využitím uživatelského rozhraní")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="9a1d9-305">*Přidání kontroleru webového rozhraní API s využitím uživatelského rozhraní*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="9a1d9-306">Visual Studio potom vytvoří třídu **ApiPersonController** se čtyřmi akcemi CRUD pro práci s daty.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="9a1d9-307">![Po vytvoření kontroleru webového rozhraní API s využitím uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "Po vytvoření kontroleru webového rozhraní API s využitím uživatelského rozhraní")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="9a1d9-308">*Po vytvoření kontroleru webového rozhraní API s využitím uživatelského rozhraní*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="9a1d9-309">Otevřete soubor **ApiPersonController.cs** a prozkoumejte metodu akce *getlidé* .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="9a1d9-310">Tato metoda se dotazuje pole DB typu **PersonContext** , aby získala data osob.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="9a1d9-311">Nyní si všimněte komentáře nad definicí metody.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="9a1d9-312">Poskytuje identifikátor URI, který zpřístupňuje tuto akci, kterou použijete v dalším úkolu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="9a1d9-313">Ve výchozím nastavení je webové rozhraní API nakonfigurované pro zachycení dotazů na */API* cestu, aby se předešlo kolizím s řadiči MVC.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="9a1d9-314">Pokud potřebujete toto nastavení změnit, přečtěte si téma [směrování ve webovém rozhraní API ASP.NET](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="9a1d9-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="9a1d9-315">Úloha 2 – spuštění řešení</span><span class="sxs-lookup"><span data-stu-id="9a1d9-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="9a1d9-316">V této úloze budete pomocí **vývojářských nástrojů** pro Internet Explorer F12 kontrolovat úplnou odpověď z kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="9a1d9-317">Zjistíte, jak můžete zachytit síťový provoz a získat tak lepší přehled o datech aplikace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="9a1d9-318">Ujistěte se, že je vybrána možnost **Internet Explorer** v nabídce **Start** , která je umístěna na panelu nástrojů sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Možnost aplikace Internet Explorer](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="9a1d9-320">**Vývojářské nástroje F12** mají rozsáhlou sadu funkcí, která není pokrytá v tomto cvičení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="9a1d9-321">Pokud se o něm chcete dozvědět víc, přečtěte si téma [použití vývojářských nástrojů F12](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="9a1d9-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>

1. <span data-ttu-id="9a1d9-322">Stisknutím klávesy **F5** spusťte řešení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a1d9-323">Aby bylo možné tento úkol provést správně, musí mít aplikace data.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="9a1d9-324">Pokud je databáze prázdná, můžete se vrátit k úloze 3 v cvičení 2 a postupovat podle pokynů, jak vytvořit novou osobu pomocí zobrazení MVC.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="9a1d9-325">Stisknutím klávesy **F12** v prohlížeči otevřete panel **vývojářské nástroje** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="9a1d9-326">Stiskněte klávesu **CTRL** + **4** nebo klikněte na ikonu **sítě** a potom klikněte na zelenou šipku tlačítka a zahajte zachytávání síťového provozu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="9a1d9-327">![Inicializace zachycení sítě webového rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Inicializace zachycení sítě webového rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="9a1d9-328">*Inicializace zachycení sítě webového rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="9a1d9-329">**Rozhraní API nebo ApiPerson** přidejte k adrese URL v adresním řádku prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="9a1d9-330">Nyní budete kontrolovat podrobnosti odpovědi z **ApiPersonController**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="9a1d9-331">![Načítání dat osob prostřednictvím webového rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Načítání dat osob prostřednictvím webového rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="9a1d9-332">*Načítání dat osob prostřednictvím webového rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a1d9-333">Po dokončení stahování se zobrazí výzva k provedení akce se staženým souborem.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="9a1d9-334">Nechejte dialogové okno otevřené, aby bylo možné sledovat obsah odpovědi prostřednictvím okna nástrojů pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="9a1d9-335">Nyní budete kontrolovat text odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="9a1d9-336">Chcete-li to provést, klikněte na kartu **Podrobnosti** a pak klikněte na **text odpovědi**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="9a1d9-337">Můžete kontrolovat, že stažená data jsou seznam objektů s **ID**vlastností, **názvem** a **stářím** , které odpovídají třídě **Person** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="9a1d9-338">![Zobrazení textu odpovědi webového rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Zobrazení textu odpovědi webového rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="9a1d9-339">*Zobrazení textu odpovědi webového rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="9a1d9-340">Úloha 3 – přidání stránek s usnadněním webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="9a1d9-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="9a1d9-341">Při vytváření webového rozhraní API je užitečné vytvořit stránku s přehledem, aby ostatní vývojáři věděli, jak vaše rozhraní API volat.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="9a1d9-342">Stránky dokumentace můžete vytvořit a aktualizovat ručně, ale je lepší je vygenerovat automaticky, aby nedocházelo k nutnosti provádět údržbu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="9a1d9-343">V této úloze použijete balíček NuGet k automatickému generování stránek s webovým rozhraním API na řešení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="9a1d9-344">V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-344">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="9a1d9-345">V okně **konzoly Správce balíčků** spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="9a1d9-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="9a1d9-346">Balíček **Microsoft. ASPNET. WebApi. HelpPage** nainstaluje nezbytná sestavení a přidá zobrazení MVC pro stránky s nápovědu ve složce **oblasti/HelpPage** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="9a1d9-347">![Oblast HelpPage](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "Oblast HelpPage")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="9a1d9-348">*Oblast HelpPage*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="9a1d9-349">Ve výchozím nastavení mají stránky pro nápovědu zástupné řetězce pro dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="9a1d9-350">Pomocí dokumentačních komentářů XML můžete vytvořit dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="9a1d9-351">Pokud chcete tuto funkci povolit, otevřete soubor **HelpPageConfig.cs** umístěný v **oblasti/HelpPage/App\_Start** a odkomentujte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="9a1d9-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="9a1d9-352">V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **MyHybridSite**, vyberte **vlastnosti** a klikněte na kartu **sestavení** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="9a1d9-353">![Karta sestavení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Oddíl Build")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="9a1d9-354">*Karta sestavení*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-354">*Build tab*</span></span>
5. <span data-ttu-id="9a1d9-355">V části **výstup**vyberte **soubor dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="9a1d9-356">Do pole pro úpravy zadejte **App\_data/XmlDocument. XML**.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="9a1d9-357">![Oddíl Output na kartě sestavení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Oddíl Output na kartě sestavení")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="9a1d9-358">*Oddíl Output na kartě sestavení*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="9a1d9-359">Změny uložte stisknutím **kombinace kláves CTRL** + **S** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="9a1d9-360">Otevřete soubor **ApiPersonController.cs** ze složky **Controllers** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="9a1d9-361">Zadejte nový řádek mezi podpisem metody *getlidech* a *//Get API/ApiPerson* a pak zadejte tři lomítka.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a1d9-362">Visual Studio automaticky vloží prvky XML, které definují dokumentaci k metodě.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="9a1d9-363">Přidejte souhrnný text a návratovou hodnotu metody *getlidé* .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="9a1d9-364">Měl by vypadat nějak takto.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="9a1d9-365">Stisknutím klávesy **F5** spusťte řešení.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="9a1d9-366">Připojením **/help** k adrese URL v adresním řádku přejdete na stránku s usnadněním.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="9a1d9-367">![Stránka s webovou pomocí rozhraní API pro ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "Stránka s webovou pomocí rozhraní API pro ASP.NET")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="9a1d9-368">*Stránka s webovou pomocí rozhraní API pro ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a1d9-369">Hlavním obsahem stránky je tabulka rozhraní API seskupených podle kontroleru.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="9a1d9-370">Položky tabulky jsou generovány dynamicky pomocí rozhraní **IApiExplorer** .</span><span class="sxs-lookup"><span data-stu-id="9a1d9-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="9a1d9-371">Pokud přidáte nebo aktualizujete kontroler rozhraní API, tabulka se automaticky aktualizuje při příštím sestavení aplikace.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="9a1d9-372">Sloupec **rozhraní API** obsahuje metodu HTTP a relativní identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="9a1d9-373">Sloupec **Description** obsahuje informace, které byly extrahovány z dokumentace metody.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="9a1d9-374">Všimněte si, že popis, který jste přidali nad definici metody, se zobrazí ve sloupci Popis.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="9a1d9-375">![Popis metody rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "Popis metody rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="9a1d9-376">*Popis metody rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-376">*API method description*</span></span>
13. <span data-ttu-id="9a1d9-377">Klikněte na jednu z metod rozhraní API a přejděte na stránku s podrobnějšími informacemi, včetně ukázkových těl odpovědí.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="9a1d9-378">![Stránka podrobností o podrobnostech](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Stránka podrobností o podrobnostech")</span><span class="sxs-lookup"><span data-stu-id="9a1d9-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="9a1d9-379">*Stránka podrobné informace*</span><span class="sxs-lookup"><span data-stu-id="9a1d9-379">*Detailed information page*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="9a1d9-380">Souhrn</span><span class="sxs-lookup"><span data-stu-id="9a1d9-380">Summary</span></span>

<span data-ttu-id="9a1d9-381">Vyplněním tohoto praktického cvičení jste se dozvěděli, jak:</span><span class="sxs-lookup"><span data-stu-id="9a1d9-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="9a1d9-382">Vytvořte novou webovou aplikaci s využitím jednoho ASP.NET prostředí v Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9a1d9-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="9a1d9-383">Integrujte několik ASP.NET technologií do jednoho jediného projektu.</span><span class="sxs-lookup"><span data-stu-id="9a1d9-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="9a1d9-384">Generování řadičů a zobrazení MVC z tříd modelu pomocí generování uživatelského rozhraní ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9a1d9-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="9a1d9-385">Generování řadičů webového rozhraní API, které využívají funkce jako asynchronní programování a přístup k datům prostřednictvím Entity Framework</span><span class="sxs-lookup"><span data-stu-id="9a1d9-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="9a1d9-386">Automatické generování stránek s nápovědu k webovému rozhraní API pro vaše řadiče</span><span class="sxs-lookup"><span data-stu-id="9a1d9-386">Automatically generate Web API Help Pages for your controllers</span></span>
