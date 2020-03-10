---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Vytvořit nový projekt ASP.NET MVC | Microsoft Docs
author: microsoft
description: V kroku 1 se dozvíte, jak umístit základní strukturu aplikace NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580932"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="7a61f-103">Vytvoření nového projektu ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="7a61f-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="7a61f-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7a61f-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7a61f-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="7a61f-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="7a61f-106">Toto je krok 1 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="7a61f-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="7a61f-107">V kroku 1 se dozvíte, jak umístit základní strukturu aplikace NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="7a61f-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="7a61f-108">Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.</span><span class="sxs-lookup"><span data-stu-id="7a61f-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="7a61f-109">NerdDinner krok 1: soubor –&gt;nový projekt</span><span class="sxs-lookup"><span data-stu-id="7a61f-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="7a61f-110">Aplikaci NerdDinner zahájíme tak, že vyberete položku nabídky **soubor&gt;nový projekt** v rámci sady visual Studio 2008 nebo Free Visual Web Developer 2008 Express.</span><span class="sxs-lookup"><span data-stu-id="7a61f-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="7a61f-111">Tím se zobrazí dialogové okno Nový projekt.</span><span class="sxs-lookup"><span data-stu-id="7a61f-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="7a61f-112">Pokud chcete vytvořit novou aplikaci ASP.NET MVC, na levé straně dialogového okna vyberte uzel web a pak na pravé straně vyberte šablonu projektu webová aplikace ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="7a61f-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="7a61f-113">*Důležité: Ujistěte se, že jste stáhli a nainstalovali ASP.NET MVC – v opačném případě se nezobrazí v dialogovém okně Nový projekt. V2 [Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx) můžete použít, pokud jste ho ještě nenainstalovali (ASP.NET MVC je k dispozici v části "webová platforma –&gt;architektury a moduly runtime").*</span><span class="sxs-lookup"><span data-stu-id="7a61f-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="7a61f-114">Pojmenujte nový projekt, který vytvoříme "NerdDinner" a potom kliknutím na tlačítko OK ho vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="7a61f-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="7a61f-115">Po kliknutí na OK se zobrazí další dialogové okno s výzvou, aby bylo možné volitelně vytvořit projekt testování částí pro novou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="7a61f-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="7a61f-116">Tento projekt testů jednotek nám umožňuje vytvářet automatizované testy, které ověřují funkčnost a chování naší aplikace (něco si ukážeme, jak postupovat později v tomto kurzu).</span><span class="sxs-lookup"><span data-stu-id="7a61f-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="7a61f-117">V rozevíracím seznamu "testovací rozhraní" v rámci výše uvedeného dialogového okna se naplní všechny dostupné šablony projektů testu jednotek ASP.NET MVC nainstalované v počítači.</span><span class="sxs-lookup"><span data-stu-id="7a61f-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="7a61f-118">Verze je možné stáhnout pro NUnit, MBUnit a XUnit.</span><span class="sxs-lookup"><span data-stu-id="7a61f-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="7a61f-119">Podporuje se taky integrované rozhraní test Unit pro testování částí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a61f-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="7a61f-120">*Poznámka: rozhraní Visual Studio Unit Test Framework je k dispozici pouze v edici Visual Studio 2008 Professional a vyšších verzích. Pokud používáte VS 2008 Standard Edition nebo Visual Web Developer 2008 Express, budete si muset stáhnout a nainstalovat rozšíření NUnit, MBUnit nebo XUnit pro ASP.NET MVC, aby se toto dialogové okno zobrazilo. Dialogové okno se nezobrazí, pokud nejsou nainstalovány žádné testovací rozhraní.*</span><span class="sxs-lookup"><span data-stu-id="7a61f-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="7a61f-121">Pro testovací projekt, který vytvoříme, použijeme výchozí název "NerdDinner. Tests" a použijeme možnost rozhraní "test jednotek sady Visual Studio".</span><span class="sxs-lookup"><span data-stu-id="7a61f-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="7a61f-122">Když klikneme na tlačítko OK, Visual Studio vytvoří řešení pro nás se dvěma projekty – jednu pro naši webovou aplikaci a jednu pro naše testy jednotek:</span><span class="sxs-lookup"><span data-stu-id="7a61f-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="7a61f-123">Zkoumání struktury adresáře NerdDinner</span><span class="sxs-lookup"><span data-stu-id="7a61f-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="7a61f-124">Při vytváření nové aplikace ASP.NET MVC se sadou Visual Studio automaticky přidá do projektu řadu souborů a adresářů:</span><span class="sxs-lookup"><span data-stu-id="7a61f-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="7a61f-125">Projekty ASP.NET MVC mají ve výchozím nastavení šest adresářů nejvyšší úrovně:</span><span class="sxs-lookup"><span data-stu-id="7a61f-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="7a61f-126">**Službě**</span><span class="sxs-lookup"><span data-stu-id="7a61f-126">**Directory**</span></span> | <span data-ttu-id="7a61f-127">**Účel**</span><span class="sxs-lookup"><span data-stu-id="7a61f-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="7a61f-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="7a61f-128">**/Controllers**</span></span> | <span data-ttu-id="7a61f-129">Kam vložíte třídy kontroleru, které zpracovávají požadavky URL</span><span class="sxs-lookup"><span data-stu-id="7a61f-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="7a61f-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="7a61f-130">**/Models**</span></span> | <span data-ttu-id="7a61f-131">Kam vložíte třídy, které reprezentují a manipulují s daty</span><span class="sxs-lookup"><span data-stu-id="7a61f-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="7a61f-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="7a61f-132">**/Views**</span></span> | <span data-ttu-id="7a61f-133">Kam vložíte soubory šablon uživatelského rozhraní, které jsou zodpovědné za vykreslování výstupu</span><span class="sxs-lookup"><span data-stu-id="7a61f-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="7a61f-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="7a61f-134">**/Scripts**</span></span> | <span data-ttu-id="7a61f-135">Kam vložíte soubory knihovny JavaScriptu a skripty (. js)</span><span class="sxs-lookup"><span data-stu-id="7a61f-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="7a61f-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="7a61f-136">**/Content**</span></span> | <span data-ttu-id="7a61f-137">Kam vložíte soubory CSS a obrázky a další nedynamický nebo nejavascriptový obsah</span><span class="sxs-lookup"><span data-stu-id="7a61f-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="7a61f-138">**Data\_/App**</span><span class="sxs-lookup"><span data-stu-id="7a61f-138">**/App\_Data**</span></span> | <span data-ttu-id="7a61f-139">Kam ukládáte datové soubory, které chcete číst a zapisovat.</span><span class="sxs-lookup"><span data-stu-id="7a61f-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="7a61f-140">ASP.NET MVC nevyžaduje tuto strukturu.</span><span class="sxs-lookup"><span data-stu-id="7a61f-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="7a61f-141">Vývojáři, kteří pracují na rozsáhlých aplikacích, obvykle rozdělí aplikaci na více projektů, aby ji bylo možné snadněji spravovat (například třídy datového modelu často přecházejí do samostatného projektu knihovny tříd z webové aplikace).</span><span class="sxs-lookup"><span data-stu-id="7a61f-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="7a61f-142">Výchozí struktura projektu ale poskytuje dobrý výchozí adresářovou konvenci, kterou můžeme použít k vyčištění naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="7a61f-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="7a61f-143">Po rozbalení adresáře/Controllers zjistíme, že Visual Studio přidalo dvě třídy kontroleru – HomeController a AccountController – ve výchozím nastavení do projektu:</span><span class="sxs-lookup"><span data-stu-id="7a61f-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="7a61f-144">Když rozšíříme adresář/views, najdete tři podsložky –/Home,/Account a/Shared – a do projektu se ve výchozím nastavení přidaly taky několik souborů šablon, které jsou v nich taky přidané:</span><span class="sxs-lookup"><span data-stu-id="7a61f-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="7a61f-145">Když rozbalíme adresáře/Content a/Scripts, zjistíme soubor Web. CSS, který se používá k vytvoření stylu HTML na webu, a také ke knihovnám JavaScriptu, které umožňují podporu ASP.NET AJAX a jQuery v rámci aplikace:</span><span class="sxs-lookup"><span data-stu-id="7a61f-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="7a61f-146">Když rozbalíte projekt NerdDinner. Tests, najdete dvě třídy, které obsahují testy jednotek pro naše třídy kontroleru:</span><span class="sxs-lookup"><span data-stu-id="7a61f-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="7a61f-147">Tyto výchozí soubory přidané sadou Visual Studio poskytují základní strukturu pro funkční aplikaci – dokončeno s domovskou stránkou, stránka, přihlašovací stránky/odhlášení/registrace účtu a Neošetřená chybová stránka (všechna drátová a funkční).</span><span class="sxs-lookup"><span data-stu-id="7a61f-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="7a61f-148">Spuštění aplikace NerdDinner</span><span class="sxs-lookup"><span data-stu-id="7a61f-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="7a61f-149">Projekt můžeme spustit tak, že vyberete buď ladění **&gt;spustit ladění** nebo **ladění –&gt;spustit bez ladění** položek nabídky:</span><span class="sxs-lookup"><span data-stu-id="7a61f-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="7a61f-150">Tím se spustí integrovaný webový server ASP.NET, který je součástí sady Visual Studio, a spusťte naši aplikaci:</span><span class="sxs-lookup"><span data-stu-id="7a61f-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="7a61f-151">Níže je Domovská stránka našeho nového projektu (adresa URL: "/") při spuštění:</span><span class="sxs-lookup"><span data-stu-id="7a61f-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="7a61f-152">Kliknutím na kartu o se zobrazí stránka about (adresa URL: "/Home/About"):</span><span class="sxs-lookup"><span data-stu-id="7a61f-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="7a61f-153">Kliknutím na odkaz přihlásit v pravém horním rohu se dostanete na přihlašovací stránku (adresa URL: "/Account/LogOn").</span><span class="sxs-lookup"><span data-stu-id="7a61f-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="7a61f-154">Pokud nemáme přihlašovací účet, můžeme kliknout na odkaz zaregistrovat (URL: "/Account/Register") a vytvořit ho:</span><span class="sxs-lookup"><span data-stu-id="7a61f-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="7a61f-155">Kód, který implementuje výše uvedenou funkci domů, o a odhlášení nebo registrace, se ve výchozím nastavení přidal, když jsme vytvořili náš nový projekt.</span><span class="sxs-lookup"><span data-stu-id="7a61f-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="7a61f-156">Použijeme ho jako výchozí bod naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="7a61f-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="7a61f-157">Testování aplikace NerdDinner</span><span class="sxs-lookup"><span data-stu-id="7a61f-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="7a61f-158">Pokud používáme edici Professional nebo vyšší verze sady Visual Studio 2008, můžeme použít integrovanou podporu IDE pro testování částí v rámci sady Visual Studio k otestování projektu:</span><span class="sxs-lookup"><span data-stu-id="7a61f-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="7a61f-159">Když vyberete jednu z výše uvedených možností, otevře se v prostředí IDE podokno "Výsledky testů" a poskytneme nám stav úspěch/selhání na 27 jednotkových testů, které jsou součástí našeho nového projektu, který se zabývá integrovanými funkcemi:</span><span class="sxs-lookup"><span data-stu-id="7a61f-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="7a61f-160">Později v tomto kurzu budeme hovořit o automatizovaném testování a přidat další testy jednotek, které pokrývají funkčnost aplikace, kterou implementujeme.</span><span class="sxs-lookup"><span data-stu-id="7a61f-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="7a61f-161">Další krok</span><span class="sxs-lookup"><span data-stu-id="7a61f-161">Next Step</span></span>

<span data-ttu-id="7a61f-162">Teď máme základní strukturu aplikace.</span><span class="sxs-lookup"><span data-stu-id="7a61f-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="7a61f-163">Teď [vytvoříme databázi, do které se budou ukládat data aplikací](create-a-database.md).</span><span class="sxs-lookup"><span data-stu-id="7a61f-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7a61f-164">[Předchozí](introducing-the-nerddinner-tutorial.md)
> [Další](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="7a61f-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
