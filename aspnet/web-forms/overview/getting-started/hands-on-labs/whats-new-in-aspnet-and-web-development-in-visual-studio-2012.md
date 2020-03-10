---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Co je nového v ASP.NET a vývoji pro web v aplikaci Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: Nová verze sady Visual Studio zavádí řadu vylepšení, která se zaměřují na zlepšení prostředí a výkonu při práci s webovými technologiemi....
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525933"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="97d14-103">Novinky ASP.NET a webového vývoje v sadě Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="97d14-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>

<span data-ttu-id="97d14-104">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="97d14-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="97d14-105">Nová verze sady Visual Studio zavádí řadu vylepšení, která se zaměřují na zlepšení prostředí a výkonu při práci s webovými technologiemi.</span><span class="sxs-lookup"><span data-stu-id="97d14-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="97d14-106">Editory sady Visual Studio pro šablony stylů CSS, JavaScript a HTML byly zcela přepracované tak, aby obsahovaly mnoho dalších pomůcek v kódu na vyžádání, jako je IntelliSense a automatické odsazení.</span><span class="sxs-lookup"><span data-stu-id="97d14-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="97d14-107">S ohledem na výkon, sdružování a minifikace jsou teď integrované jako integrované funkce, které zjednodušují dobu načítání stránek.</span><span class="sxs-lookup"><span data-stu-id="97d14-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="97d14-108">Visual Studio vám umožní pracovat s nejnovějšími technologiemi webů.</span><span class="sxs-lookup"><span data-stu-id="97d14-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="97d14-109">Pomocí CSS3 fragmentů kódu pro různé prohlížeče se můžete ujistit, že váš web funguje bez ohledu na klientskou platformu a zároveň využívá nové prvky a funkce HTML5.</span><span class="sxs-lookup"><span data-stu-id="97d14-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="97d14-110">Psaní a profilace kódu v jazyce JavaScript by měla být snazší s touto verzí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97d14-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="97d14-111">Seznamy IntelliSense, integrovaná dokumentace XML a navigační funkce jsou nyní k dispozici pro kód jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="97d14-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="97d14-112">Teď máte katalog JavaScriptu na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="97d14-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="97d14-113">Kromě toho můžete kontrolovat ECMAScript5 dodržování předpisů pomocí skriptů a zjišťovat chyby syntaxe v rané fázi.</span><span class="sxs-lookup"><span data-stu-id="97d14-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="97d14-114">Takže tato verze sady Visual Studio implementuje předdefinované sdružování a minifikace.</span><span class="sxs-lookup"><span data-stu-id="97d14-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="97d14-115">Soubory skriptu a šablony stylů budou zabaleny a komprimovány, aby lokalita rychleji prováděla.</span><span class="sxs-lookup"><span data-stu-id="97d14-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="97d14-116">Toto testovací prostředí vás provede vylepšeními a novými funkcemi, které jsme dříve popsali pomocí menších změn ve vzorové webové aplikaci, která je součástí zdrojové složky.</span><span class="sxs-lookup"><span data-stu-id="97d14-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="97d14-117">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="97d14-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="97d14-118">Cíle</span><span class="sxs-lookup"><span data-stu-id="97d14-118">Objectives</span></span>

<span data-ttu-id="97d14-119">V tomto cvičení se naučíte:</span><span class="sxs-lookup"><span data-stu-id="97d14-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="97d14-120">Použití nových funkcí a vylepšení v editoru šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="97d14-121">Použití nových funkcí a vylepšení v editoru HTML</span><span class="sxs-lookup"><span data-stu-id="97d14-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="97d14-122">Použití nových funkcí a vylepšení v editoru JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="97d14-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="97d14-123">Konfigurace a použití sdružování a minifikace</span><span class="sxs-lookup"><span data-stu-id="97d14-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="97d14-124">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="97d14-124">Prerequisites</span></span>

- <span data-ttu-id="97d14-125">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).</span><span class="sxs-lookup"><span data-stu-id="97d14-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="97d14-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (pro instalační skripty – už nainstalované v systémech Windows 8 a windows Server 2008 R2)</span><span class="sxs-lookup"><span data-stu-id="97d14-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="97d14-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) nebo prohlížeč kompatibilní s HTML5</span><span class="sxs-lookup"><span data-stu-id="97d14-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="97d14-128">Cvičení</span><span class="sxs-lookup"><span data-stu-id="97d14-128">Exercises</span></span>

<span data-ttu-id="97d14-129">Tato cvičení v testovacím prostředí zahrnuje následující cvičení:</span><span class="sxs-lookup"><span data-stu-id="97d14-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="97d14-130">Cvičení 1: co je nového v editoru šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="97d14-131">Cvičení 2: co je nového v editoru HTML</span><span class="sxs-lookup"><span data-stu-id="97d14-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="97d14-132">Cvičení 3: co je nového v editoru JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="97d14-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="97d14-133">Cvičení 4: sdružování a minifikace</span><span class="sxs-lookup"><span data-stu-id="97d14-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="97d14-134">Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.</span><span class="sxs-lookup"><span data-stu-id="97d14-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="97d14-135">Cvičení 1: co je nového v editoru šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="97d14-136">Vývojáři webu by měli znát mnoho potíží souvisejících s úpravou šablon stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="97d14-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="97d14-137">Jedním z největších problémů stylu CSS je kompatibilita mezi prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="97d14-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="97d14-138">K tomu často dochází, když po použití stylů na webu zjistíte, že vypadá jinak, když ho otevřete v jiném prohlížeči nebo zařízení.</span><span class="sxs-lookup"><span data-stu-id="97d14-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="97d14-139">Proto může dojít k výraznému odstranění těchto vizuálních problémů, aby se zajistilo, že když nakonec budete pracovat v jednom prohlížeči, bude se v ostatních prohlížečích porušen.</span><span class="sxs-lookup"><span data-stu-id="97d14-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="97d14-140">Visual Studio teď obsahuje funkce, které vývojářům umožňují efektivně přistupovat k šablonám stylů CSS, pracovat a uspořádávat je.</span><span class="sxs-lookup"><span data-stu-id="97d14-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="97d14-141">V rámci tohoto cvičení budete splňovat nové funkce pro efektivní organizaci a edici a také fragmenty kódu CSS3 pro zajištění kompatibility mezi prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="97d14-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="97d14-142">Úloha 1 – nové funkce editoru</span><span class="sxs-lookup"><span data-stu-id="97d14-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="97d14-143">V této úloze zjistíte nové funkce editoru šablon stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="97d14-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="97d14-144">Tento nový Editor vám pomůže zvýšit produktivitu tím, že využívá nové inteligentní odsazení, vylepšené komentáře ke kódu a vylepšený seznam IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="97d14-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="97d14-145">Spusťte **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** nacházející se ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="97d14-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="97d14-146">V Průzkumník řešení otevřete soubor **Web. CSS** umístěný ve složce **Styles** .</span><span class="sxs-lookup"><span data-stu-id="97d14-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="97d14-147">Ujistěte se, že jsou nástroje **textový editor** na panelu nástrojů viditelné.</span><span class="sxs-lookup"><span data-stu-id="97d14-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="97d14-148">Provedete to tak, že vyberete možnost nabídky **zobrazit** | **panely nástrojů** a pak zkontrolujete možnosti **textového editoru** .</span><span class="sxs-lookup"><span data-stu-id="97d14-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="97d14-149">Všimněte si, že od této nové verze se pro Editor šablon stylů CSS také povoluje tlačítko **Komentář** (![tlačítko pro komentář](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) a tlačítko zrušit **Komentář** (![odkomentovat tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)).</span><span class="sxs-lookup"><span data-stu-id="97d14-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="97d14-150">![Povolování nástrojů editoru a šablon stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Povolování nástrojů editoru a šablon stylů CSS")</span><span class="sxs-lookup"><span data-stu-id="97d14-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="97d14-151">*Povolování nástrojů editoru a šablon stylů CSS*</span><span class="sxs-lookup"><span data-stu-id="97d14-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="97d14-152">Posuňte kód a vyberte libovolnou definici třídy CSS.</span><span class="sxs-lookup"><span data-stu-id="97d14-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="97d14-153">Kliknutím na tlačítko **Komentář** (![komentář-tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) přidejte poznámky k vybraným řádkům.</span><span class="sxs-lookup"><span data-stu-id="97d14-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="97d14-154">Pak klikněte na tlačítko zrušit **Komentář** (![odkomentovat tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)), aby se změny projevily.</span><span class="sxs-lookup"><span data-stu-id="97d14-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="97d14-155">Klikněte na **sbalit** (![sbalit](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)) a **rozbalte** (![rozbalit](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) tlačítka umístěná na levém okraji textu.</span><span class="sxs-lookup"><span data-stu-id="97d14-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="97d14-156">Všimněte si, že teď můžete skrýt styly, které nepoužíváte, aby se zobrazila čisticí zobrazení.</span><span class="sxs-lookup"><span data-stu-id="97d14-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="97d14-157">![Sbalení tříd CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Sbalení tříd CSS")</span><span class="sxs-lookup"><span data-stu-id="97d14-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="97d14-158">*Sbalení tříd CSS*</span><span class="sxs-lookup"><span data-stu-id="97d14-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="97d14-159">Ujistěte se, že je zapnutá funkce chytrého odsazení.</span><span class="sxs-lookup"><span data-stu-id="97d14-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="97d14-160">Vyberte možnost nabídky **nástroje** | **Možnosti** a pak v levém podokně obrazovky vyberte **textový editor** | stránce **formátování** **šablon stylů CSS** | .</span><span class="sxs-lookup"><span data-stu-id="97d14-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="97d14-161">Ověřte možnost **hierarchického odsazení** .</span><span class="sxs-lookup"><span data-stu-id="97d14-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="97d14-162">![Povoluje se hierarchické odsazení.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Povoluje se hierarchické odsazení.")</span><span class="sxs-lookup"><span data-stu-id="97d14-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="97d14-163">*Povoluje se hierarchické odsazení.*</span><span class="sxs-lookup"><span data-stu-id="97d14-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="97d14-164">Vyhledejte definici hlavní třídy (. Main) a připojíte styl k elementům div.</span><span class="sxs-lookup"><span data-stu-id="97d14-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="97d14-165">Všimněte si, že kód se zarovnává automaticky a pomůže uživatelům najít nadřazené třídy na první pohled.</span><span class="sxs-lookup"><span data-stu-id="97d14-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="97d14-166">CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="97d14-167">![Hierarchické zarovnání v šablonách stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchické zarovnání v šablonách stylů CSS")</span><span class="sxs-lookup"><span data-stu-id="97d14-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="97d14-168">*Hierarchické zarovnání v šablonách stylů CSS*</span><span class="sxs-lookup"><span data-stu-id="97d14-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="97d14-169">Uvnitř **. Main** – třída div vyhledejte kurzor na konci **ohraničení: 0px;** a stisknutím klávesy **ENTER** zobrazte seznam IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="97d14-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="97d14-170">Začněte psát **nahoru** a Všimněte si, jak je seznam filtrovaný při psaní.</span><span class="sxs-lookup"><span data-stu-id="97d14-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="97d14-171">V seznamu se zobrazí prvky, které obsahují **horní** část slova (v předchozích verzích sady Visual Studio, seznam je filtrován podle položek, které *začínají* termínem).</span><span class="sxs-lookup"><span data-stu-id="97d14-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="97d14-172">![Vylepšení technologie IntelliSense v šablonách stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "Vylepšení technologie IntelliSense v šablonách stylů CSS")</span><span class="sxs-lookup"><span data-stu-id="97d14-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="97d14-173">*Vylepšení technologie IntelliSense v šablonách stylů CSS*</span><span class="sxs-lookup"><span data-stu-id="97d14-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="97d14-174">Úkol 2 – Výběr barvy</span><span class="sxs-lookup"><span data-stu-id="97d14-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="97d14-175">V této úloze se zobrazí nový dialog pro výběr barvy CSS, který je integrovaný do sady Visual Studio IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="97d14-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="97d14-176">V **lokalitě. CSS** vyhledejte definici třídy hlaviček (. Header) a umístěte kurzor vedle atributu **background-color** atribut mezi &quot;:&quot; a &quot;#&quot; znaků na daném řádku kódu **.**</span><span class="sxs-lookup"><span data-stu-id="97d14-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="97d14-177">![Vyhledání kurzoru](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Vyhledání kurzoru")</span><span class="sxs-lookup"><span data-stu-id="97d14-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="97d14-178">*Vyhledání kurzoru*</span><span class="sxs-lookup"><span data-stu-id="97d14-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="97d14-179">Odstraňte **dvojtečku** (:) a zapište ho znovu, abyste zobrazili výběr barvy.</span><span class="sxs-lookup"><span data-stu-id="97d14-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="97d14-180">Všimněte si, že první barvy, které vidíte, jsou nejčastějšími barvami webu.</span><span class="sxs-lookup"><span data-stu-id="97d14-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="97d14-181">Pokud kliknete na bílou barvu, jeho kód barvy HTML (#fff) nahradí aktuální kód barvy v šabloně stylů.</span><span class="sxs-lookup"><span data-stu-id="97d14-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="97d14-182">![Výběr barvy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Výběr barvy")</span><span class="sxs-lookup"><span data-stu-id="97d14-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="97d14-183">*Výběr barvy*</span><span class="sxs-lookup"><span data-stu-id="97d14-183">*Color picker*</span></span>
3. <span data-ttu-id="97d14-184">Stisknutím tlačítka **Rozbalit** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) na výběr barvy Zobrazte barevný přechod a potom přetažením ukazatele přechodu vyberte jinou barvu.</span><span class="sxs-lookup"><span data-stu-id="97d14-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="97d14-185">Potom klikněte na tlačítko **kapátka** a vyberte libovolnou barvu na obrazovce.</span><span class="sxs-lookup"><span data-stu-id="97d14-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="97d14-186">Všimněte si, že se hodnota barvy pozadí při přesunu kurzoru dynamicky mění.</span><span class="sxs-lookup"><span data-stu-id="97d14-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="97d14-187">![Barevný přechod pro výběr barvy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Barevný přechod pro výběr barvy")</span><span class="sxs-lookup"><span data-stu-id="97d14-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="97d14-188">*Barevný přechod pro výběr barvy*</span><span class="sxs-lookup"><span data-stu-id="97d14-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="97d14-189">V posuvníku **neprůhlednosti** přesuňte selektor do středu pruhu, aby se snížila průhlednost.</span><span class="sxs-lookup"><span data-stu-id="97d14-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="97d14-190">Všimněte si, že hodnota pozadí-barva teď změní měřítko na RGBA.</span><span class="sxs-lookup"><span data-stu-id="97d14-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="97d14-191">![Průhlednost výběru barvy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Průhlednost výběru barvy")</span><span class="sxs-lookup"><span data-stu-id="97d14-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="97d14-192">*Průhlednost výběru barvy*</span><span class="sxs-lookup"><span data-stu-id="97d14-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-193">Definice barvy RGBA (červená, zelená, modrá, alfa) v CSS3 umožňuje definovat hodnotu neprůhlednosti barvy pro jednu položku.</span><span class="sxs-lookup"><span data-stu-id="97d14-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="97d14-194">Na rozdíl od **neprůhlednosti –** podobný atribut CSS **-** RGBA barvy jsou také kompatibilní s nejnovějšími prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="97d14-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="97d14-195">Úloha 3 – fragmenty kódu kompatibilní se šablonou stylů CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="97d14-196">V této úloze se naučíte používat fragmenty CSS3 kompatibilní s více prohlížeči, abyste mohli implementovat některé funkce na vašem webu.</span><span class="sxs-lookup"><span data-stu-id="97d14-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="97d14-197">V souboru **Web. CSS** Najděte hlavičku třídy CSS pro **záhlaví** (. Header) a umístěte kurzor pod **/\*poloměru ohraničení\*/** zástupný symbol pro přidání nového fragmentu.</span><span class="sxs-lookup"><span data-stu-id="97d14-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="97d14-198">Stiskněte klávesu **ENTER** , chcete-li zobrazit seznam IntelliSense a zadat **protokol RADIUS** pro filtrování seznamu.</span><span class="sxs-lookup"><span data-stu-id="97d14-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="97d14-199">Vyberte možnost **border-RADIUS** ze seznamu dvojitým kliknutím a potom stiskněte klávesu **tabulátor** pro vložení fragmentu.</span><span class="sxs-lookup"><span data-stu-id="97d14-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="97d14-200">Pak zadejte velikost poloměru v pixelech a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="97d14-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="97d14-201">Například zadejte **15px**.</span><span class="sxs-lookup"><span data-stu-id="97d14-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="97d14-202">Atributy CSS3 přidané fragmentem kódu vykreslí zaoblené ohraničení v prohlížeči dodržování předpisů HTML5, včetně prohlížečů Mozilla a WebKit.</span><span class="sxs-lookup"><span data-stu-id="97d14-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="97d14-203">![Použití výstřižku Border-RADIUS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Použití výstřižku Border-RADIUS")</span><span class="sxs-lookup"><span data-stu-id="97d14-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="97d14-204">*Použití výstřižku Border-RADIUS*</span><span class="sxs-lookup"><span data-stu-id="97d14-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="97d14-205">Použijte stejné fragmenty **ohraničení** ve stylu stránky (. Page).</span><span class="sxs-lookup"><span data-stu-id="97d14-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="97d14-206">CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="97d14-207">Stisknutím klávesy **F5** spusťte řešení.</span><span class="sxs-lookup"><span data-stu-id="97d14-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="97d14-208">Všimněte si, že každá stránka má nyní zaoblené ohraničení.</span><span class="sxs-lookup"><span data-stu-id="97d14-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="97d14-209">![Zaoblené rohy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Zaoblené rohy")</span><span class="sxs-lookup"><span data-stu-id="97d14-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="97d14-210">*Zaoblené rohy*</span><span class="sxs-lookup"><span data-stu-id="97d14-210">*Rounded corners*</span></span>
4. <span data-ttu-id="97d14-211">Zavřete prohlížeč a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97d14-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="97d14-212">Otevřete soubor **Custom. CSS** umístěný ve složce **styly** a umístěte kurzor do **div. images ul li img** definice třídy.</span><span class="sxs-lookup"><span data-stu-id="97d14-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="97d14-213">Stiskněte klávesu ENTER, chcete-li zobrazit seznam IntelliSense, zadejte **pole-Shadow** a stiskněte klávesu **TAB** dvakrát pro vložení výchozího fragmentu stínového kódu do definice třídy.</span><span class="sxs-lookup"><span data-stu-id="97d14-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="97d14-214">Nastavte stínové hodnoty na **10px 10px 5px #888**.</span><span class="sxs-lookup"><span data-stu-id="97d14-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="97d14-215">Pak zadejte **border-RADIUS** a vložte fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="97d14-216">Zadejte **15px** pro nastavení velikosti poloměru a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="97d14-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="97d14-217">![Zaoblené rohy se stínem](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Zaoblené rohy se stínem")</span><span class="sxs-lookup"><span data-stu-id="97d14-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="97d14-218">*Zaoblené rohy se stínem*</span><span class="sxs-lookup"><span data-stu-id="97d14-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-219">V tuto chvíli se atribut Shadow vloží s odpovídající předponou (MOZ, WebKit, o), aby se podporovaly prohlížeče Mozilla a WebKit (Chrome, Safari, Konkeror).</span><span class="sxs-lookup"><span data-stu-id="97d14-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="97d14-220">Vytvořit novou třídu **div. images ul li IMG: najeďte myší** pod **div. images ul li img** definice třídy a umístěte kurzor do závorek **.**</span><span class="sxs-lookup"><span data-stu-id="97d14-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="97d14-221">CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="97d14-222">Pro vložení transformačního výstřižku zadejte **transformaci** a stiskněte klávesu **TAB** dvakrát.</span><span class="sxs-lookup"><span data-stu-id="97d14-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="97d14-223">Pak zadejte **otočit (-15deg)** , chcete-li změnit hodnotu úhlu otočení při přechodu na obrázky.</span><span class="sxs-lookup"><span data-stu-id="97d14-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="97d14-224">CSS</span><span class="sxs-lookup"><span data-stu-id="97d14-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="97d14-225">Stisknutím klávesy **F5** spusťte řešení a přejděte na stránku CSS3.</span><span class="sxs-lookup"><span data-stu-id="97d14-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="97d14-226">Všimněte si, že obrázky mají zaoblené rohy a stínování box.</span><span class="sxs-lookup"><span data-stu-id="97d14-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="97d14-227">Najeďte myší na obrázky a sledujte jejich otočení.</span><span class="sxs-lookup"><span data-stu-id="97d14-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="97d14-228">![Transformovat fragment kódu pro otočení obrázku](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transformovat fragment kódu pro otočení obrázku")</span><span class="sxs-lookup"><span data-stu-id="97d14-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="97d14-229">*Transformovat fragment kódu pro otočení obrázku*</span><span class="sxs-lookup"><span data-stu-id="97d14-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-230">Pokud používáte Internet Explorer 10 a nevidíte stíny, ujistěte se, že je režim dokumentu nastavený na IE10 standardy.</span><span class="sxs-lookup"><span data-stu-id="97d14-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="97d14-231">Stisknutím klávesy **F12** otevřete nástroje pro vývojáře v aplikaci Internet Explorer a kliknutím na **režim dokumentu** přejděte na IE10 Standards.</span><span class="sxs-lookup"><span data-stu-id="97d14-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![o-cz](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="97d14-233">Cvičení 2: co je nového v editoru HTML</span><span class="sxs-lookup"><span data-stu-id="97d14-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="97d14-234">Visual Studio má Vylepšený editor HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="97d14-235">Některá vylepšení zahrnutá v této verzi jsou inteligentní odsazení v dokumentech HTML, fragmentech HTML5, počátečních a koncových značkách HTML a při ověřování HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="97d14-236">V průběhu tohoto cvičení uvidíte, jak tyto změny zlepšují Fluency při práci na webu značek.</span><span class="sxs-lookup"><span data-stu-id="97d14-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="97d14-237">Podobně jako editor CSS byl také vylepšen Editor HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="97d14-238">Většina těchto vylepšení je malými těmi, které usnadňují život webové vývojáře.</span><span class="sxs-lookup"><span data-stu-id="97d14-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="97d14-239">Podobně jako u více fragmentů kódu pro HTML5, inteligentní odsazení, porovnání počátečních a koncových značek, pokud jsou úpravy a ověřování cílené na typ dokumentu HTML, jsou některá z těchto vylepšení.</span><span class="sxs-lookup"><span data-stu-id="97d14-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="97d14-240">Úloha 1 – Vylepšené ověřování typu DOCTYPE</span><span class="sxs-lookup"><span data-stu-id="97d14-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="97d14-241">Editor HTML nyní má možnost kontrolovat typ DOCTYPE stránky, i když definice může být na stránce předlohy.</span><span class="sxs-lookup"><span data-stu-id="97d14-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="97d14-242">V závislosti na typu DOCTYPE stránky se Editor HTML ověří se správnou sadou pravidel a vyfiltruje seznam IntelliSense, který bude zohledňovat prvky DOCTYPE.</span><span class="sxs-lookup"><span data-stu-id="97d14-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="97d14-243">V této úloze změníte typ DOCTYPE stránky, abyste viděli, jak se odpovídajícím způsobem změní chování editoru HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="97d14-244">Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="97d14-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="97d14-245">Otevřete stránku **Web. Master** .</span><span class="sxs-lookup"><span data-stu-id="97d14-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="97d14-246">Všimněte si cílového schématu pro panel nástrojů ověření.</span><span class="sxs-lookup"><span data-stu-id="97d14-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="97d14-247">Způsob, jakým se Editor HTML chová (ověřování, IntelliSense atd.), se správně změní tak, aby odpovídal vybranému typu doctype.</span><span class="sxs-lookup"><span data-stu-id="97d14-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="97d14-248">![Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML")</span><span class="sxs-lookup"><span data-stu-id="97d14-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="97d14-249">*Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML*</span><span class="sxs-lookup"><span data-stu-id="97d14-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="97d14-250">Změňte cílové schéma na HTML 4,01.</span><span class="sxs-lookup"><span data-stu-id="97d14-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="97d14-251">![Změna typu doctype na panelu nástrojů pro úpravy zdrojového kódu HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Změna typu doctype na panelu nástrojů pro úpravy zdrojového kódu HTML")</span><span class="sxs-lookup"><span data-stu-id="97d14-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="97d14-252">*Změna typu doctype na panelu nástrojů pro úpravy zdrojového kódu HTML*</span><span class="sxs-lookup"><span data-stu-id="97d14-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="97d14-253">Umístěte kurzor pod prvek **body** a začněte psát název elementu HTML5 (například **video**).</span><span class="sxs-lookup"><span data-stu-id="97d14-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="97d14-254">Všimněte si, že prvek není k dispozici v seznamu technologie IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="97d14-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="97d14-255">![Prvky HTML5 nejsou uvedené](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "Prvky HTML5 nejsou uvedené")</span><span class="sxs-lookup"><span data-stu-id="97d14-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="97d14-256">*Prvky HTML5 nejsou uvedené*</span><span class="sxs-lookup"><span data-stu-id="97d14-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="97d14-257">Vraťte změny do cílového schématu pro panel nástrojů ověření a z rozevíracího seznamu vyhledá typ DOCTYPE: XHTML5.</span><span class="sxs-lookup"><span data-stu-id="97d14-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="97d14-258">![Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML")</span><span class="sxs-lookup"><span data-stu-id="97d14-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="97d14-259">*Obnovit typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML*</span><span class="sxs-lookup"><span data-stu-id="97d14-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="97d14-260">Umístěte kurzor pod prvek **tělo** a začněte psát prvek HTML5 znovu (například jako **video**).</span><span class="sxs-lookup"><span data-stu-id="97d14-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="97d14-261">Všimněte si, že prvky HTML5 jsou nyní k dispozici v seznamu technologie IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="97d14-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="97d14-262">![Jsou uvedeny prvky HTML5](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "Jsou uvedeny prvky HTML5")</span><span class="sxs-lookup"><span data-stu-id="97d14-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="97d14-263">*Jsou uvedeny prvky HTML5*</span><span class="sxs-lookup"><span data-stu-id="97d14-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="97d14-264">Úloha 2 – Automatické aktualizace značek start/end</span><span class="sxs-lookup"><span data-stu-id="97d14-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="97d14-265">Visual Studio teď aktualizuje značky otevírání nebo zavírání HTML prvku, který upravujete, aby se vzájemně shodovaly.</span><span class="sxs-lookup"><span data-stu-id="97d14-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="97d14-266">Tato nová funkce zvýší vaši produktivitu při úpravě značek HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="97d14-267">Na stránce **Default. aspx** přidejte element **H3** s názvem (například Visual Studio 2012 Rocks!).</span><span class="sxs-lookup"><span data-stu-id="97d14-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. <span data-ttu-id="97d14-268">Změňte značku **H3** a zadejte **H2** nebo **H1.**</span><span class="sxs-lookup"><span data-stu-id="97d14-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="97d14-269">Všimněte si, že se koncová značka automaticky aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="97d14-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="97d14-270">Můžete také změnit koncovou značku, abyste viděli, že se odpovídajícím způsobem aktualizují počáteční značky.</span><span class="sxs-lookup"><span data-stu-id="97d14-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="97d14-271">![Automatická aktualizace koncových značek](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatická aktualizace koncových značek")</span><span class="sxs-lookup"><span data-stu-id="97d14-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="97d14-272">*Automatická aktualizace koncových značek*</span><span class="sxs-lookup"><span data-stu-id="97d14-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="97d14-273">Úloha 3 – nové fragmenty kódu HTML5</span><span class="sxs-lookup"><span data-stu-id="97d14-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="97d14-274">Visual Studio teď obsahuje několik fragmentů kódu HTML5.</span><span class="sxs-lookup"><span data-stu-id="97d14-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="97d14-275">V tomto úkolu použijete některé z těchto fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="97d14-276">Přidejte novou složku s názvem **zvuk** do kořenového adresáře složky webu.</span><span class="sxs-lookup"><span data-stu-id="97d14-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="97d14-277">Otevřete Průzkumníka Windows a zkopírujte libovolný zvukový soubor do **zvukové** složky řešení **WhatsNewASPNET. sln** .</span><span class="sxs-lookup"><span data-stu-id="97d14-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="97d14-278">Na stránce **Default. aspx** Najděte kurzor v části Web11 Rocks.</span><span class="sxs-lookup"><span data-stu-id="97d14-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="97d14-279">Hlaviček.</span><span class="sxs-lookup"><span data-stu-id="97d14-279">Header.</span></span> <span data-ttu-id="97d14-280">Zadejte **zvuk** a stiskněte klávesu Tabulátor.</span><span class="sxs-lookup"><span data-stu-id="97d14-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="97d14-281">Nový editor HTML obsahuje fragmenty kódu pro obsah HTML5.</span><span class="sxs-lookup"><span data-stu-id="97d14-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="97d14-282">Nezapomeňte použít správnou definici DOCTYPE a povolit fragmenty HTML5.</span><span class="sxs-lookup"><span data-stu-id="97d14-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="97d14-283">![Vkládání fragmentů kódu HTML5](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Vkládání fragmentů kódu HTML5")</span><span class="sxs-lookup"><span data-stu-id="97d14-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="97d14-284">*Vkládání fragmentů kódu HTML5*</span><span class="sxs-lookup"><span data-stu-id="97d14-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="97d14-285">Aktualizujte zdroj zvuku tak, aby odkazoval na existující zvukový soubor.</span><span class="sxs-lookup"><span data-stu-id="97d14-285">Update the audio source to point to an existing audio file.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > <span data-ttu-id="97d14-286">Do řešení budete muset přidat zvukový soubor.</span><span class="sxs-lookup"><span data-stu-id="97d14-286">You will need to add the audio file to the solution.</span></span>
4. <span data-ttu-id="97d14-287">Stiskněte klávesu **F5** ke spuštění lokality a přehrání zvuku.</span><span class="sxs-lookup"><span data-stu-id="97d14-287">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="97d14-288">![Spuštění ovládacího prvku zvuk](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Spuštění ovládacího prvku zvuk")</span><span class="sxs-lookup"><span data-stu-id="97d14-288">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="97d14-289">*Spuštění ovládacího prvku zvuk*</span><span class="sxs-lookup"><span data-stu-id="97d14-289">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-290">Můžete také vyzkoušet další fragmenty kódu, které jsou součástí sady Visual Studio, například video, obrázek atd.</span><span class="sxs-lookup"><span data-stu-id="97d14-290">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="97d14-291">Nyní se pokuste vložit ovládací prvek do některé části stránky.</span><span class="sxs-lookup"><span data-stu-id="97d14-291">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="97d14-292">Například zkuste vložit ovládací prvek **GridView** , ale místo zadání **&lt;mřížky** začněte psát **&lt;GV**.</span><span class="sxs-lookup"><span data-stu-id="97d14-292">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="97d14-293">Všimněte si, že seznam IntelliSense zobrazí ovládací prvek **ASP: GridView** .</span><span class="sxs-lookup"><span data-stu-id="97d14-293">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="97d14-294">Technologie IntelliSense v editoru HTML nyní poskytuje vyhledávání na základě názvu a velikosti písmen a také částečné porovnávání (načítání všech prvků, které obsahují podmínky).</span><span class="sxs-lookup"><span data-stu-id="97d14-294">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="97d14-295">![Vložení prvku GridView se seznamy technologie IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Vložení prvku GridView se seznamy technologie IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="97d14-295">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="97d14-296">*Vložení prvku GridView se seznamy technologie IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="97d14-296">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="97d14-297">Pokud zadáte **&lt;Grid** , zobrazí se všechny položky, které se shodují s termínem, ale Visual Studio navrhne ovládací prvek **GridView** :</span><span class="sxs-lookup"><span data-stu-id="97d14-297">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="97d14-298">![Vložení prvku GridView pomocí seznamů IntelliSense a částečného spárování](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Vložení prvku GridView pomocí seznamů IntelliSense a částečného spárování")</span><span class="sxs-lookup"><span data-stu-id="97d14-298">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="97d14-299">*Vložení prvku GridView pomocí seznamů IntelliSense a částečného spárování*</span><span class="sxs-lookup"><span data-stu-id="97d14-299">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="97d14-300">Úloha 4 – inteligentní značky editoru HTML</span><span class="sxs-lookup"><span data-stu-id="97d14-300">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="97d14-301">Dalším vylepšením v editoru HTML je funkce inteligentních značek.</span><span class="sxs-lookup"><span data-stu-id="97d14-301">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="97d14-302">Inteligentní značky usnadňují provádění běžných nebo opakujících se úloh vývoje na základě jednotlivých ovládacích prvků.</span><span class="sxs-lookup"><span data-stu-id="97d14-302">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="97d14-303">Tato funkce byla již k dispozici v Návrháři HTML, ale ne v editoru HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-303">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="97d14-304">Otevřete **Web. Master** a vyhledejte prvek **ASP: menu** .</span><span class="sxs-lookup"><span data-stu-id="97d14-304">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="97d14-305">Umístěte kurzor na značku Start a Všimněte si, že malý glyf zobrazený v dolní části elementu – kliknutím na něj otevřete nabídku inteligentní úlohy.</span><span class="sxs-lookup"><span data-stu-id="97d14-305">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="97d14-306">Všimněte si, že máte rychlý přístup k některým úlohám souvisejícím s ovládacím prvkem nabídky.</span><span class="sxs-lookup"><span data-stu-id="97d14-306">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="97d14-307">![Inteligentní úkoly pro ovládací prvek nabídky](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Inteligentní úkoly pro ovládací prvek nabídky")</span><span class="sxs-lookup"><span data-stu-id="97d14-307">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="97d14-308">*Inteligentní úkoly pro ovládací prvek nabídky*</span><span class="sxs-lookup"><span data-stu-id="97d14-308">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="97d14-309">Úkol 5 – inteligentní odsazení</span><span class="sxs-lookup"><span data-stu-id="97d14-309">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="97d14-310">Jedním z osvědčených postupů ve formátu HTML je odsadit vnořené prvky, aby kód zůstal čitelný.</span><span class="sxs-lookup"><span data-stu-id="97d14-310">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="97d14-311">V aplikaci Visual Studio 2012 zjistíte, že editor při psaní kódu automaticky odsadí prvky.</span><span class="sxs-lookup"><span data-stu-id="97d14-311">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="97d14-312">V předchozí verzi sady Visual Studio bylo inteligentní odsazení k dispozici v editoru XML, ale ne v editoru HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-312">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>

1. <span data-ttu-id="97d14-313">Ujistěte se, že je konfigurace odsazení v editoru HTML nastavená na inteligentní odsazení.</span><span class="sxs-lookup"><span data-stu-id="97d14-313">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="97d14-314">To provedete tak, že vyberete **nástroje |** Možnost nabídky možnosti a potom vyberte **textový editor | HTML | Stránka karty** v levém podokně obrazovky</span><span class="sxs-lookup"><span data-stu-id="97d14-314">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="97d14-315">Vyberte možnost inteligentní odsazení.</span><span class="sxs-lookup"><span data-stu-id="97d14-315">Select the Smart indentation option.</span></span>

    <span data-ttu-id="97d14-316">![Nastavení editoru HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "Nastavení editoru HTML")</span><span class="sxs-lookup"><span data-stu-id="97d14-316">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="97d14-317">*Nastavení editoru HTML*</span><span class="sxs-lookup"><span data-stu-id="97d14-317">*HTML Editor settings*</span></span>
2. <span data-ttu-id="97d14-318">Na stránce **Default. aspx** odeberte veškerý obsah v rámci prvku zvuk.</span><span class="sxs-lookup"><span data-stu-id="97d14-318">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="97d14-319">Umístěte kurzor na konec otevřeného **zvukového** prvku a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="97d14-319">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="97d14-320">Všimněte si, že nová pozice kurzoru má další úroveň odsazení.</span><span class="sxs-lookup"><span data-stu-id="97d14-320">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="97d14-321">![Inteligentní odsazení v editoru HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Inteligentní odsazení v editoru HTML")</span><span class="sxs-lookup"><span data-stu-id="97d14-321">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="97d14-322">*Inteligentní odsazení v editoru HTML*</span><span class="sxs-lookup"><span data-stu-id="97d14-322">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="97d14-323">Obnovte zvukovou značku pomocí odebraného obsahu nebo zavřete **Default. aspx** bez uložení změn.</span><span class="sxs-lookup"><span data-stu-id="97d14-323">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="97d14-324">Úloha 6 – extrakce do uživatelského ovládacího prvku</span><span class="sxs-lookup"><span data-stu-id="97d14-324">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="97d14-325">Nástroje refaktoringu, které jsou součástí sady Visual Studio, například extrakce části kódu pro funkci, jsou skvělé funkce, které usnadňují vylepšení a refaktoring existujícího kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-325">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="97d14-326">Protějšek pro stránky ASP.NET by představoval extrakci kódu HTML do uživatelského ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="97d14-326">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="97d14-327">Ruční provedení by zahrnovalo několik kroků, jako je vytvoření nového uživatelského ovládacího prvku, přesunutí oddílu kódu do uživatelského ovládacího prvku, registrace předpony značky pro uživatelský ovládací prvek a nakonec, vytvoření instance uživatelského ovládacího prvku na stránkách.</span><span class="sxs-lookup"><span data-stu-id="97d14-327">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="97d14-328">Nový nástroj pro *extrakci do uživatelského ovládacího prvku* teď provede všechny tyto kroky automaticky.</span><span class="sxs-lookup"><span data-stu-id="97d14-328">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="97d14-329">V této úloze použijete novou kontextovou operaci extrahovat do uživatelského ovládacího prvku pro vygenerování nového uživatelského ovládacího prvku z vybraného kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-329">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="97d14-330">Na stránce **Default. aspx** vyberte prvky **H2** a **audio** .</span><span class="sxs-lookup"><span data-stu-id="97d14-330">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="97d14-331">Klikněte pravým tlačítkem a vyberte **extrahovat do uživatelského ovládacího prvku**.</span><span class="sxs-lookup"><span data-stu-id="97d14-331">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="97d14-332">![Možnost extrahovat do nabídky uživatelského ovládacího prvku](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Možnost extrahovat do nabídky uživatelského ovládacího prvku")</span><span class="sxs-lookup"><span data-stu-id="97d14-332">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="97d14-333">*Možnost extrahovat do nabídky uživatelského ovládacího prvku*</span><span class="sxs-lookup"><span data-stu-id="97d14-333">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="97d14-334">Zadejte název nového uživatelského ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="97d14-334">Type a name for the new user control.</span></span> <span data-ttu-id="97d14-335">Například **jukebox. ascx**a pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="97d14-335">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="97d14-336">![Ukládání extrahovaných uživatelských ovládacích prvků](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Ukládání extrahovaných uživatelských ovládacích prvků")</span><span class="sxs-lookup"><span data-stu-id="97d14-336">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="97d14-337">*Ukládání extrahovaných uživatelských ovládacích prvků*</span><span class="sxs-lookup"><span data-stu-id="97d14-337">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="97d14-338">Všimněte si, že vybraný kód byl extrahován do uživatelského ovládacího prvku a původní umístění vybraného kódu bylo nahrazeno instancí nového uživatelského ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="97d14-338">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="97d14-339">![Stránka se automaticky aktualizovala tak, aby používala nový uživatelský ovládací prvek.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Stránka se automaticky aktualizovala tak, aby používala nový uživatelský ovládací prvek.")</span><span class="sxs-lookup"><span data-stu-id="97d14-339">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="97d14-340">*Stránka se automaticky aktualizovala tak, aby používala nový uživatelský ovládací prvek.*</span><span class="sxs-lookup"><span data-stu-id="97d14-340">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="97d14-341">Stisknutím klávesy **F5** spusťte stránku a ověřte, zda ovládací prvek funguje.</span><span class="sxs-lookup"><span data-stu-id="97d14-341">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="97d14-342">Cvičení 3: co je nového v editoru JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="97d14-342">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="97d14-343">Psaní nebo úprava kódu JavaScriptu není jednoduchý úkol, zejména v případě, že se vaše aplikace začne zvětšovat a vy zjistíte, že budete pracovat s dlouhými soubory a stovkami funkcí.</span><span class="sxs-lookup"><span data-stu-id="97d14-343">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="97d14-344">Vývojáři skriptu obvykle potřebují udělat nějakou další práci, aby bylo možné udržet čitelnost kódu a procházet mezi soubory.</span><span class="sxs-lookup"><span data-stu-id="97d14-344">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="97d14-345">Díky zahrnutí knihoven JavaScriptu, jako je jQuery, se navigace v skriptech stala samotným výzvou z důvodu délky kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-345">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="97d14-346">Visual Studio obnovilo Editor jazyka JavaScript se příslibem tak, aby byl režim kódu přístupný a uspořádaný.</span><span class="sxs-lookup"><span data-stu-id="97d14-346">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="97d14-347">Mnoho funkcí sady Visual Studio, které již C# existovaly v nástroji nebo editory VB, jsou nyní implementovány v editoru JavaScriptu: přejít k definici, automatické odsazení, dokumentaci a ověření při psaní.</span><span class="sxs-lookup"><span data-stu-id="97d14-347">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="97d14-348">Díky obnovenému seznamu IntelliSense budete mít katalog funkcí JavaScriptu na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="97d14-348">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="97d14-349">V tomto cvičení se seznámíte s některými novými funkcemi a vylepšeními editoru JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="97d14-349">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="97d14-350">Budete procházet ukázkové soubory a zjišťovat všechny nové charakteristiky, které budou v sadě Visual Studio 2012 efektivnější pro programování v JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="97d14-350">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="97d14-351">Úloha 1 – nové funkce editoru JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="97d14-351">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="97d14-352">Tato úloha vás seznámí s některými z nových funkcí editoru JavaScriptu, které se zaměřují na organizování kódu a lepší uživatelské prostředí.</span><span class="sxs-lookup"><span data-stu-id="97d14-352">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="97d14-353">Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="97d14-353">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="97d14-354">Stisknutím klávesy **F5** spusťte aplikaci a potom klikněte na odkaz JavaScriptu na navigačním panelu.</span><span class="sxs-lookup"><span data-stu-id="97d14-354">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="97d14-355">Aktualizujte stránku několikrát a podívejte se, jak čítače zvýší.</span><span class="sxs-lookup"><span data-stu-id="97d14-355">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="97d14-356">![Čítač stránky](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Čítač stránky")</span><span class="sxs-lookup"><span data-stu-id="97d14-356">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="97d14-357">*Čítač stránky*</span><span class="sxs-lookup"><span data-stu-id="97d14-357">*Page counter*</span></span>
3. <span data-ttu-id="97d14-358">Zavřete prohlížeč a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97d14-358">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="97d14-359">Otevřete stránku **JavaScript. aspx** a vyhledejte&lt;blok **&gt;skriptu** (viz níže).</span><span class="sxs-lookup"><span data-stu-id="97d14-359">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="97d14-360">Následující kód používá místní úložiště HTML5 k uložení proměnné *pageLoadCount* , která ukládá počet navštívených stránek aktuálním uživatelem.</span><span class="sxs-lookup"><span data-stu-id="97d14-360">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="97d14-361">Místní úložiště je databáze klíč-hodnota na straně klienta, kterou přináší Standard HTML5.</span><span class="sxs-lookup"><span data-stu-id="97d14-361">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="97d14-362">Data se ukládají v místním počítači do prohlížeče uživatele.</span><span class="sxs-lookup"><span data-stu-id="97d14-362">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="97d14-363">Než budete pokračovat v dalších krocích, ujistěte se, že je typ DOCTYPE nastavený na XHTML5.</span><span class="sxs-lookup"><span data-stu-id="97d14-363">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="97d14-364">Upravte kód a Všimněte si, že technologie IntelliSense pro JavaScript obsahuje funkce HTML5, jako je místní úložiště, a jejich vnitřní metody.</span><span class="sxs-lookup"><span data-stu-id="97d14-364">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="97d14-365">![Funkce jazyka HTML5 JavaScriptu v JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "Funkce jazyka HTML5 JavaScriptu v JavaScriptu")</span><span class="sxs-lookup"><span data-stu-id="97d14-365">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="97d14-366">*Funkce jazyka HTML5 JavaScriptu v JavaScriptu*</span><span class="sxs-lookup"><span data-stu-id="97d14-366">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="97d14-367">Klikněte na libovolnou levou hranatou závorku ( **{** ) ze skriptovacího kódu a Všimněte si, že se zvýrazní hranaté závorky.</span><span class="sxs-lookup"><span data-stu-id="97d14-367">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="97d14-368">![Hranaté závorky jsou zvýrazněné](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Hranaté závorky jsou zvýrazněné")</span><span class="sxs-lookup"><span data-stu-id="97d14-368">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="97d14-369">*Hranaté závorky jsou zvýrazněné*</span><span class="sxs-lookup"><span data-stu-id="97d14-369">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="97d14-370">Odkomentujte funkci **testAutoAlign ()** (vyberte tři řádky a můžete použít **klávesovou zkratku CTRL** + **K**; **CTRL** + **U**) a vyhledejte kurzor uvnitř kódu funkce.</span><span class="sxs-lookup"><span data-stu-id="97d14-370">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="97d14-371">Stiskněte klávesu ENTER a přidejte tak druhý řádek.</span><span class="sxs-lookup"><span data-stu-id="97d14-371">Press enter to append a second line.</span></span> <span data-ttu-id="97d14-372">Všimněte si, že kód je nyní **zarovnán** a **automaticky odsazen**.</span><span class="sxs-lookup"><span data-stu-id="97d14-372">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="97d14-373">![JavaScriptový kód se automaticky zarovnává.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScriptový kód se automaticky zarovnává.")</span><span class="sxs-lookup"><span data-stu-id="97d14-373">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="97d14-374">*JavaScriptový kód se automaticky zarovnává.*</span><span class="sxs-lookup"><span data-stu-id="97d14-374">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="97d14-375">Úloha 2 – ověřování JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="97d14-375">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="97d14-376">V této úloze zjistíte nové ověřování JavaScriptu pro ECMAScript5 Standard.</span><span class="sxs-lookup"><span data-stu-id="97d14-376">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="97d14-377">Tato funkce vám pomůže s psaním kompatibilního kódu JavaScriptu a zároveň zabraňuje problémům skriptování před nasazením lokality.</span><span class="sxs-lookup"><span data-stu-id="97d14-377">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="97d14-378">Visual Studio 2010 implementovalo dodržování předpisů ECMAStript3, zatímco Visual Studio 2012 zajišťuje dodržování předpisů ECMAScript5.</span><span class="sxs-lookup"><span data-stu-id="97d14-378">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>

1. <span data-ttu-id="97d14-379">Otevřete **ECMA5script5. js** umístěný ve složce projektu **Scripts\custom** .</span><span class="sxs-lookup"><span data-stu-id="97d14-379">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="97d14-380">Nyní budete testovat ověření pro ECMAScript5 Standard.</span><span class="sxs-lookup"><span data-stu-id="97d14-380">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="97d14-381">Na prvním řádku souboru můžete &quot; **použít striktní** &quot;, což umožňuje **striktní režim**ECMAScript5.</span><span class="sxs-lookup"><span data-stu-id="97d14-381">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="97d14-382">Tento režim se skládá z podmnožiny jazyka, který objasňuje nejednoznačnosti z minulé edice a přidává některé nové funkce, jako jsou metody getter a setter, podpora knihoven pro JSON a další kompletní reflexe vlastností objektu.</span><span class="sxs-lookup"><span data-stu-id="97d14-382">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="97d14-383">Otevřete **Seznam chyb** , pokud ještě není otevřený (**Zobrazit** nabídku | **Seznam chyb**).</span><span class="sxs-lookup"><span data-stu-id="97d14-383">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="97d14-384">Všimněte si, že je deklarace **funkce** podtržená.</span><span class="sxs-lookup"><span data-stu-id="97d14-384">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="97d14-385">Důvodem je, že ve standardních funkcích ECMA5 nelze vnořovat do jazykových struktur.</span><span class="sxs-lookup"><span data-stu-id="97d14-385">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="97d14-386">V seznamu chyb se zobrazí podrobnosti upozornění.</span><span class="sxs-lookup"><span data-stu-id="97d14-386">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="97d14-387">![Chybová zpráva ověřování JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "Chybová zpráva ověřování JavaScriptu")</span><span class="sxs-lookup"><span data-stu-id="97d14-387">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="97d14-388">*Chybová zpráva ověřování JavaScriptu*</span><span class="sxs-lookup"><span data-stu-id="97d14-388">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="97d14-389">Odkomentujte **&quot;použijte striktní&quot;** a Všimněte si, že chyby zmizí, ale upozornění zůstanou.</span><span class="sxs-lookup"><span data-stu-id="97d14-389">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="97d14-390">Na posledním řádku souboru zapište libovolný řetězec, například **&quot;test&quot;** (včetně uvozovek pro indikaci, že se jedná o řetězec).</span><span class="sxs-lookup"><span data-stu-id="97d14-390">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="97d14-391">Napište tečku vedle řetězce pro zobrazení seznamu IntelliSense a vyberte možnost **Trim** .</span><span class="sxs-lookup"><span data-stu-id="97d14-391">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="97d14-392">V ECMAScript5 standard mají hodnoty a proměnné řetězců také definovány řetězcové metody, jako je například Trim, Velká písmena, hledání a nahrazování.</span><span class="sxs-lookup"><span data-stu-id="97d14-392">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="97d14-393">![Seznam IntelliSense v JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "Seznam IntelliSense v JavaScriptu")</span><span class="sxs-lookup"><span data-stu-id="97d14-393">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="97d14-394">*Seznam IntelliSense v JavaScriptu*</span><span class="sxs-lookup"><span data-stu-id="97d14-394">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="97d14-395">Úloha 3 – dokumentace XML pro JavaScript</span><span class="sxs-lookup"><span data-stu-id="97d14-395">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="97d14-396">V této úloze budete zkoumat funkce sady Visual Studio pro dokumentaci XML v JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="97d14-396">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="97d14-397">Zobrazí se seznam JavaScript IntelliSense, který teď zobrazí dokumentaci XML každé funkce.</span><span class="sxs-lookup"><span data-stu-id="97d14-397">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="97d14-398">Kromě toho se v JavaScriptu objeví navigační funkce.</span><span class="sxs-lookup"><span data-stu-id="97d14-398">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="97d14-399">Otevřete soubor **XMLDoc. js** umístěný ve složce **skripty nebo vlastní** složka projektu.</span><span class="sxs-lookup"><span data-stu-id="97d14-399">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="97d14-400">Tento soubor obsahuje dokumentaci XML ke každé z funkcí jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="97d14-400">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="97d14-401">![Dokumentace XML JavaScriptu integrovaná do IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "Dokumentace XML JavaScriptu integrovaná do IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="97d14-401">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="97d14-402">*Dokumentace XML JavaScriptu integrovaná do IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="97d14-402">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="97d14-403">Pod funkcí **Přidat** funkci v souboru **XMLDoc. js** vytvořte novou funkci s názvem **test**.</span><span class="sxs-lookup"><span data-stu-id="97d14-403">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="97d14-404">Ve funkci **test** volejte funkci **násobení** , která přijímá dva parametry.</span><span class="sxs-lookup"><span data-stu-id="97d14-404">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="97d14-405">Všimněte si, že se v poli s popisem zobrazuje dokumentace k funkci **násobit** .</span><span class="sxs-lookup"><span data-stu-id="97d14-405">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="97d14-406">![Dokumentace XML pro funkce JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "Dokumentace XML pro funkce JavaScriptu")</span><span class="sxs-lookup"><span data-stu-id="97d14-406">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="97d14-407">*Dokumentace XML pro funkce JavaScriptu*</span><span class="sxs-lookup"><span data-stu-id="97d14-407">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="97d14-408">Dokončete příkaz volání funkce a zadejte *tečku* pro otevření seznamu IntelliSense na vrácené hodnotě.</span><span class="sxs-lookup"><span data-stu-id="97d14-408">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="97d14-409">Všimněte si, že Visual Studio detekuje **vrácenou** hodnotu v dokumentaci a považuje hodnotu za číslo.</span><span class="sxs-lookup"><span data-stu-id="97d14-409">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="97d14-410">![Dokumentace XML pro návratové typy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "Dokumentace XML pro návratové typy")</span><span class="sxs-lookup"><span data-stu-id="97d14-410">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="97d14-411">*Dokumentace XML pro návratové typy*</span><span class="sxs-lookup"><span data-stu-id="97d14-411">*XML documentation for return types*</span></span>
5. <span data-ttu-id="97d14-412">Nyní vložte volání funkce Add.</span><span class="sxs-lookup"><span data-stu-id="97d14-412">Now, insert a call to add function.</span></span> <span data-ttu-id="97d14-413">Všimněte si, že editor JavaScriptu teď podporuje přetížení funkcí.</span><span class="sxs-lookup"><span data-stu-id="97d14-413">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="97d14-414">Když napíšete název funkce, budete moci vybrat kterékoli z dostupných přetížení uvedených v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="97d14-414">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="97d14-415">![Dokumentace XML pro přetížení](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "Dokumentace XML pro přetížení")</span><span class="sxs-lookup"><span data-stu-id="97d14-415">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="97d14-416">*Dokumentace XML pro přetížení*</span><span class="sxs-lookup"><span data-stu-id="97d14-416">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="97d14-417">Otevřete soubor **GotoDefinition. js** a vyhledejte volání funkce **$ (). html ()** .</span><span class="sxs-lookup"><span data-stu-id="97d14-417">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="97d14-418">Vyhledejte kurzor ve **formátu HTML**.</span><span class="sxs-lookup"><span data-stu-id="97d14-418">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="97d14-419">Stiskněte klávesu **F12** a přejděte do definice.</span><span class="sxs-lookup"><span data-stu-id="97d14-419">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="97d14-420">Všimněte si, že teď máte přístup k kódu JavaScriptu a můžete ho Procházet bez použití nástroje **find** .</span><span class="sxs-lookup"><span data-stu-id="97d14-420">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="97d14-421">Vyhledejte kurzor v instrukci jQuery před blokem podpisu ve spodní části souboru kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-421">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="97d14-422">Stiskněte klávesu **F12**.</span><span class="sxs-lookup"><span data-stu-id="97d14-422">Press **F12**.</span></span> <span data-ttu-id="97d14-423">Přejdete na soubor knihovny jQuery.</span><span class="sxs-lookup"><span data-stu-id="97d14-423">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="97d14-424">Všimněte si, že můžete také procházet soubory jQuery pomocí **F12**.</span><span class="sxs-lookup"><span data-stu-id="97d14-424">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="97d14-425">![Přechod na definice jQuery](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Přechod na definice jQuery")</span><span class="sxs-lookup"><span data-stu-id="97d14-425">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="97d14-426">*Přechod na definice jQuery*</span><span class="sxs-lookup"><span data-stu-id="97d14-426">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="97d14-427">Ujistěte se, že GotoDefinition. js neobsahuje žádné chyby syntaxe před uložením souboru.</span><span class="sxs-lookup"><span data-stu-id="97d14-427">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="97d14-428">Cvičení 4: sdružování a minifikace</span><span class="sxs-lookup"><span data-stu-id="97d14-428">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="97d14-429">Kolikrát vaše weby obsahují více než jeden soubor JavaScript nebo CSS?</span><span class="sxs-lookup"><span data-stu-id="97d14-429">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="97d14-430">Toto je velmi běžný scénář, kdy může sdružování a minifikace snížit velikost souboru a zrychlit jeho provádění.</span><span class="sxs-lookup"><span data-stu-id="97d14-430">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="97d14-431">Nová funkce sdružování v sadě ASP.NET 4,5 sbalí sadu souborů JS nebo CSS do jediného prvku a zmenší její velikost tím, že minifikace obsah (tj. odebrání nevyžadují prázdné mezery, odebrání komentářů a omezení identifikátorů).</span><span class="sxs-lookup"><span data-stu-id="97d14-431">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="97d14-432">Sdružování a minifikace v ASP.NET 4,5 se provádí za běhu, aby proces mohl identifikovat uživatelského agenta (například IE, Mozilla atd.), a tak vylepšit komprimaci tím, že se zacílení na prohlížeč uživatelů (například odstranění věcí, které jsou specifické pro Mozilla. Když požadavek pochází z IE).</span><span class="sxs-lookup"><span data-stu-id="97d14-432">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="97d14-433">V tomto cvičení se naučíte, jak povolit a používat různé typy sdružování a minifikace v ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="97d14-433">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="97d14-434">Úloha 1 – instalace balíčku sdružování a minifikace z NuGetu</span><span class="sxs-lookup"><span data-stu-id="97d14-434">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="97d14-435">Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="97d14-435">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="97d14-436">Otevřete konzolu Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="97d14-436">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="97d14-437">Chcete-li to provést, použijte **zobrazení** nabídky | jiné **konzoly Správce balíčků** | **systému Windows** .</span><span class="sxs-lookup"><span data-stu-id="97d14-437">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="97d14-438">![Otevření Správce balíčků file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Otevření konzoly Správce balíčků")</span><span class="sxs-lookup"><span data-stu-id="97d14-438">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="97d14-439">*Otevření konzoly Správce balíčků*</span><span class="sxs-lookup"><span data-stu-id="97d14-439">*Opening the package manager console*</span></span>
3. <span data-ttu-id="97d14-440">V **konzole správce balíčků** zadejte **Install-Package Microsoft. Web. Optimization** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="97d14-440">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="97d14-441">Úloha 2 – výchozí sady svazků</span><span class="sxs-lookup"><span data-stu-id="97d14-441">Task 2 - Default Bundles</span></span>

<span data-ttu-id="97d14-442">Nejjednodušší způsob, jak použít sdružování a minifikace, je povolit výchozí balíčky.</span><span class="sxs-lookup"><span data-stu-id="97d14-442">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="97d14-443">Tato metoda používá konvence k tomu, aby vám umožnil odkazování na sadu a minifikovaného verzi pro soubory JS a CSS ve složce.</span><span class="sxs-lookup"><span data-stu-id="97d14-443">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="97d14-444">V této úloze se dozvíte, jak povolit a odkazovat na soubory minifikovaného JS a šablony stylů CSS a zobrazit výsledný výstup.</span><span class="sxs-lookup"><span data-stu-id="97d14-444">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="97d14-445">Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="97d14-445">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="97d14-446">V **Průzkumník řešení**rozbalte složky **Styles**, **Scripts\custom** a **Scripts\bundle** .</span><span class="sxs-lookup"><span data-stu-id="97d14-446">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="97d14-447">Všimněte si, že aplikace používá více než jeden soubor CSS a JS.</span><span class="sxs-lookup"><span data-stu-id="97d14-447">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="97d14-448">![Více šablon stylů a souborů JavaScriptu v aplikaci](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Více šablon stylů a souborů JavaScriptu v aplikaci")</span><span class="sxs-lookup"><span data-stu-id="97d14-448">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="97d14-449">*Více šablon stylů a souborů JavaScriptu v aplikaci*</span><span class="sxs-lookup"><span data-stu-id="97d14-449">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="97d14-450">Otevřete soubor **Global.asax.cs** .</span><span class="sxs-lookup"><span data-stu-id="97d14-450">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="97d14-451">Všimněte si, že nový obor názvů **Microsoft. Web. Optimization je označený** jako komentář na začátku souboru.</span><span class="sxs-lookup"><span data-stu-id="97d14-451">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="97d14-452">Odkomentujte direktivu using, aby zahrnovala funkce sdružování a minifikace.</span><span class="sxs-lookup"><span data-stu-id="97d14-452">Uncomment the using directive to include the bundling and minification features.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. <span data-ttu-id="97d14-453">Vyhledejte **aplikaci\_metodu Start** .</span><span class="sxs-lookup"><span data-stu-id="97d14-453">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="97d14-454">V této metodě Odkomentujte volání EnableDefaultBundles, jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-454">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="97d14-455">Díky tomu je možné odkazovat na kolekci souborů šablon stylů CSS ve složce pomocí cesty k této složce, a navíc &quot;šablon stylů CSS&quot; nebo&quot; příponou &quot;JS.</span><span class="sxs-lookup"><span data-stu-id="97d14-455">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. <span data-ttu-id="97d14-456">Otevřete soubor **Optimization. aspx** a vyhledejte ovládací prvek obsahu pro **HeadContent**.</span><span class="sxs-lookup"><span data-stu-id="97d14-456">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="97d14-457">Všimněte si, že soubory CSS a soubory JS mají jedinou odkazovanou značku.</span><span class="sxs-lookup"><span data-stu-id="97d14-457">Notice the CSS files and the JS files have a single referenced tag.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > <span data-ttu-id="97d14-458">Tento kód je určen pro demonstrační účely.</span><span class="sxs-lookup"><span data-stu-id="97d14-458">This code is for demo purposes.</span></span> <span data-ttu-id="97d14-459">V ideálním případě budete odkazovat na sady v souboru site. Master.</span><span class="sxs-lookup"><span data-stu-id="97d14-459">Ideally, you will reference the bundles in the Site.Master file.</span></span> <span data-ttu-id="97d14-460">V tomto ukázkovém kódu zjistíte, že některé z těchto souborů jsou také odkazovány pomocí souboru site. Master, takže tento poslední odkaz bude redundantní.</span><span class="sxs-lookup"><span data-stu-id="97d14-460">In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.</span></span>
6. <span data-ttu-id="97d14-461">Všimněte si, že odkazy používají konvence sdružování v atributu **href** k získání všech souborů CSS nebo JS ze složky Styles (styly) a Scripts\custom (v uvedeném pořadí).</span><span class="sxs-lookup"><span data-stu-id="97d14-461">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="97d14-462">Můžete použít cesty **Scripts/Custom/js** , jak je znázorněno níže, chcete-li seskupit a minimalizuje všechny soubory JS v rámci **skriptů nebo vlastní** složky.</span><span class="sxs-lookup"><span data-stu-id="97d14-462">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="97d14-463">Toto je výchozí chování u výchozích sad.</span><span class="sxs-lookup"><span data-stu-id="97d14-463">This is the default behavior with the default bundles.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. <span data-ttu-id="97d14-464">Otevřete soubor **Styles\Site.CSS** .</span><span class="sxs-lookup"><span data-stu-id="97d14-464">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="97d14-465">Všimněte si, že původní soubor CSS obsahuje odsazený kód, prázdné mezery a komentáře, které soubor zvětší.</span><span class="sxs-lookup"><span data-stu-id="97d14-465">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="97d14-466">(Také soubor JavaScriptu obsahuje prázdné mezery a komentáře).</span><span class="sxs-lookup"><span data-stu-id="97d14-466">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="97d14-467">![Jeden z původních souborů CSS ve složce Scripts](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Jeden z původních souborů CSS ve složce Scripts")</span><span class="sxs-lookup"><span data-stu-id="97d14-467">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="97d14-468">*Jeden z původních souborů CSS ve složce Scripts*</span><span class="sxs-lookup"><span data-stu-id="97d14-468">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="97d14-469">Stisknutím klávesy **F5** spusťte aplikaci a přejděte na stránku **optimalizace** .</span><span class="sxs-lookup"><span data-stu-id="97d14-469">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="97d14-470">Klikněte na odkaz **Sada šablon stylů CSS** a stáhněte a otevřete soubor.</span><span class="sxs-lookup"><span data-stu-id="97d14-470">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="97d14-471">Prohlédněte si soubor minifikovanéhoed.</span><span class="sxs-lookup"><span data-stu-id="97d14-471">Check out the minified bundled file.</span></span> <span data-ttu-id="97d14-472">Všimněte si, že se odebraly všechny prázdné mezery, komentáře a znaky odsazení, což vygeneruje menší soubor.</span><span class="sxs-lookup"><span data-stu-id="97d14-472">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="97d14-473">![Rozbalené soubory šablon stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Rozbalené soubory šablon stylů CSS")</span><span class="sxs-lookup"><span data-stu-id="97d14-473">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="97d14-474">*Rozbalené soubory šablon stylů CSS*</span><span class="sxs-lookup"><span data-stu-id="97d14-474">*Bundled CSS files*</span></span>
10. <span data-ttu-id="97d14-475">Nyní klikněte na odkaz **sady prostředků js** a otevřete soubor sady JavaScript.</span><span class="sxs-lookup"><span data-stu-id="97d14-475">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="97d14-476">Upozornění Průzkumníka můžete bez obav ignorovat.</span><span class="sxs-lookup"><span data-stu-id="97d14-476">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="97d14-477">Všimněte si, že soubory JavaScriptu ve **vlastní** složce jsou také seskupené a minifikovaného.</span><span class="sxs-lookup"><span data-stu-id="97d14-477">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="97d14-478">![Seskupené soubory JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Seskupené soubory JavaScriptu")</span><span class="sxs-lookup"><span data-stu-id="97d14-478">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="97d14-479">*Seskupené soubory JavaScriptu*</span><span class="sxs-lookup"><span data-stu-id="97d14-479">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="97d14-480">Povolení komprese souborů CSS nebo JS bylo v předchozí verzi ASP.NET mnohem složitější.</span><span class="sxs-lookup"><span data-stu-id="97d14-480">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="97d14-481">Nyní, jak jste viděli, stačí přidat jeden řádek do souboru *Global. asax* , aby se povolilo sdružování, a pak odkazovaly na soubory z vaší lokality.</span><span class="sxs-lookup"><span data-stu-id="97d14-481">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="97d14-482">Úloha 3 – statické sady</span><span class="sxs-lookup"><span data-stu-id="97d14-482">Task 3 - Static Bundles</span></span>

<span data-ttu-id="97d14-483">Přístup ke statickým svazkům vám umožní přizpůsobit sadu souborů na sady, odkaz a metodu minifikace, která se použije.</span><span class="sxs-lookup"><span data-stu-id="97d14-483">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="97d14-484">V této úloze nakonfigurujete statickou sadu pro definování konkrétní sady souborů, které se mají seskupit a minimalizuje.</span><span class="sxs-lookup"><span data-stu-id="97d14-484">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="97d14-485">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="97d14-485">Close the browser.</span></span>
2. <span data-ttu-id="97d14-486">Otevřete soubor **Global.asax.cs** a vyhledejte **aplikaci\_spustit** metodu.</span><span class="sxs-lookup"><span data-stu-id="97d14-486">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="97d14-487">Odkomentujte kód statické sady, jak je znázorněno v následujícím kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-487">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="97d14-488">Definujete statickou sadu, na kterou se bude odkazovat &quot; **~/StaticBundle**&quot; virtuální cesta, a použijte **JsMinify** pro minifikace všech zadaných souborů pomocí metody **AddFile** .</span><span class="sxs-lookup"><span data-stu-id="97d14-488">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="97d14-489">Nakonec přidáváte statickou sadu do **Kompletované sady prostředků** a povolíte ji.</span><span class="sxs-lookup"><span data-stu-id="97d14-489">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="97d14-490">Všimněte si, že soubory nejsou umístěny na stejném místě; Toto je další výhoda oproti výchozímu sdružování.</span><span class="sxs-lookup"><span data-stu-id="97d14-490">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. <span data-ttu-id="97d14-491">Otevřete soubor **Optimization. aspx** .</span><span class="sxs-lookup"><span data-stu-id="97d14-491">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="97d14-492">Všimněte si, že odkaz na **svazek statického js** používá cestu, kterou jste deklarovali při konfiguraci statické sady v souboru Global.asax.cs: **/StaticBundle**.</span><span class="sxs-lookup"><span data-stu-id="97d14-492">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. <span data-ttu-id="97d14-493">Stisknutím klávesy **F5** spusťte aplikaci a potom přejděte na stránku **optimalizace** .</span><span class="sxs-lookup"><span data-stu-id="97d14-493">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="97d14-494">Kliknutím na odkaz **sady statických js** otevřete soubor.</span><span class="sxs-lookup"><span data-stu-id="97d14-494">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="97d14-495">Všimněte si, že soubor JavaScriptu minifikovanéhoed je výstupem všech souborů JavaScriptu nakonfigurovaných v souboru statické sady v cestě &quot;/StaticBundle&quot;.</span><span class="sxs-lookup"><span data-stu-id="97d14-495">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="97d14-496">![Sada statických souborů JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Sada statických souborů JavaScriptu")</span><span class="sxs-lookup"><span data-stu-id="97d14-496">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="97d14-497">*Sada statických souborů JavaScriptu*</span><span class="sxs-lookup"><span data-stu-id="97d14-497">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="97d14-498">Zavřete prohlížeč a vraťte se do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97d14-498">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="97d14-499">Úloha 4 – sady svazků dynamické složky</span><span class="sxs-lookup"><span data-stu-id="97d14-499">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="97d14-500">V této úloze se naučíte konfigurovat sady prostředků dynamické složky.</span><span class="sxs-lookup"><span data-stu-id="97d14-500">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="97d14-501">Výkonem dynamického sdružování je, že můžete zahrnovat statické JavaScripty i jiné soubory v jazycích, které se zkompiluje do JavaScriptu, a proto vyžadují určité zpracování ještě před provedením sdružování.</span><span class="sxs-lookup"><span data-stu-id="97d14-501">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="97d14-502">V tomto příkladu se naučíte, jak pomocí třídy **DynamicFolderBundle** vytvořit dynamickou sadu souborů napsaných v CofeeScript.</span><span class="sxs-lookup"><span data-stu-id="97d14-502">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="97d14-503">CofeeScript je programovací jazyk, který se kompiluje do JavaScriptu a poskytuje jednodušší syntaxi pro psaní kódu JavaScriptu, což usnadňuje zkrácení a čitelnost JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="97d14-503">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="97d14-504">Otevřete soubor **Global.asax.cs** a vyhledejte **aplikaci\_spustit** metodu.</span><span class="sxs-lookup"><span data-stu-id="97d14-504">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="97d14-505">Odkomentujte kód dynamické sady, jak je znázorněno v následujícím kódu.</span><span class="sxs-lookup"><span data-stu-id="97d14-505">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="97d14-506">Definujete sadu prostředků dynamické složky, která bude používat vlastní procesor **CoffeeMinify** minifikace, který se bude vztahovat pouze na soubory s příponou&quot; &quot; **. kávy** (soubory CoffeeScript).</span><span class="sxs-lookup"><span data-stu-id="97d14-506">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="97d14-507">Všimněte si, že pomocí vzoru hledání můžete vybrat soubory, které se mají seskupit do složky, například '\*. káva '.</span><span class="sxs-lookup"><span data-stu-id="97d14-507">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. <span data-ttu-id="97d14-508">Otevřete konzolu Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="97d14-508">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="97d14-509">Chcete-li to provést, použijte **zobrazení** nabídky | jiné **konzoly Správce balíčků** | **systému Windows** .</span><span class="sxs-lookup"><span data-stu-id="97d14-509">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="97d14-510">V **konzole správce balíčků** zadejte **Install-Package CoffeeSharp** a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="97d14-510">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="97d14-511">Klikněte na tlačítko **Zobrazit všechny soubory** v okně **Průzkumník řešení**</span><span class="sxs-lookup"><span data-stu-id="97d14-511">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="97d14-512">![Zobrazení všech souborů](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Zobrazení všech souborů")</span><span class="sxs-lookup"><span data-stu-id="97d14-512">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="97d14-513">*Zobrazení všech souborů*</span><span class="sxs-lookup"><span data-stu-id="97d14-513">*Showing all files*</span></span>
6. <span data-ttu-id="97d14-514">V **Průzkumník řešení** klikněte pravým tlačítkem na soubor **CoffeeMinify.cs** a vyberte **zahrnout do projektu** .</span><span class="sxs-lookup"><span data-stu-id="97d14-514">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="97d14-515">![Zahrnout soubor CoffeeMinify.cs do projektu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Zahrnout soubor CoffeeMinify.cs do projektu")</span><span class="sxs-lookup"><span data-stu-id="97d14-515">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="97d14-516">*Zahrnout soubor CoffeeMinify.cs do projektu*</span><span class="sxs-lookup"><span data-stu-id="97d14-516">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="97d14-517">Otevřete soubor **CoffeeMinify.cs** .</span><span class="sxs-lookup"><span data-stu-id="97d14-517">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="97d14-518">Tato třída dědí z JsMinify, aby minimalizuje výstup JavaScriptu, který je výsledkem kompilace kódu CoffeeScript.</span><span class="sxs-lookup"><span data-stu-id="97d14-518">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="97d14-519">Volá kompilátor CoffeeScript pro vygenerování kódu JavaScriptu a pak ho pošle metodě JsMinify. Process, aby minimalizuje výsledný kód.</span><span class="sxs-lookup"><span data-stu-id="97d14-519">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. <span data-ttu-id="97d14-520">Otevřete soubory **Script1. kávy** a **Script2. kávy** ze složky **skripty/sady prostředků** .</span><span class="sxs-lookup"><span data-stu-id="97d14-520">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="97d14-521">Tyto soubory budou zahrnovat kód CoffeScript, který se má kompilovat při provádění sdružování s třídou CoffeeMinify.</span><span class="sxs-lookup"><span data-stu-id="97d14-521">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="97d14-522">V zájmu zjednodušení jsou poskytnuté soubory CoffeeScript, včetně ukázkového kódu CoffeeScript.</span><span class="sxs-lookup"><span data-stu-id="97d14-522">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="97d14-523">Komentáře jsou vyloučeny z procesu JsMinify.</span><span class="sxs-lookup"><span data-stu-id="97d14-523">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="97d14-524">![Soubory CoffeeScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "Soubory CoffeeScript")</span><span class="sxs-lookup"><span data-stu-id="97d14-524">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="97d14-525">*Soubory CoffeeScript*</span><span class="sxs-lookup"><span data-stu-id="97d14-525">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) poskytuje jednodušší syntaxi pro psaní kódu JavaScriptu, vylepšení zkrácení a čitelnosti JavaScriptu, jakož i přidávání dalších funkcí, jako je porozumění poli a porovnávání vzorů.</span><span class="sxs-lookup"><span data-stu-id="97d14-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="97d14-527">Otevřete soubor **Optimization. aspx** a vyhledejte odkazy na skupinu.</span><span class="sxs-lookup"><span data-stu-id="97d14-527">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="97d14-528">Všimněte si, že odkaz na **svazek dynamické knihovny JS** odkazuje na složku **Scripts/** **re/Coffees** pomocí přípony pro, kterou jste nakonfigurovali pro sadu svazků dynamické složky.</span><span class="sxs-lookup"><span data-stu-id="97d14-528">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. <span data-ttu-id="97d14-529">Stisknutím klávesy **F5** spusťte aplikaci a potom přejděte na stránku **optimalizace** .</span><span class="sxs-lookup"><span data-stu-id="97d14-529">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="97d14-530">Kliknutím na odkaz **sady dynamických js** Otevřete vygenerovaný soubor.</span><span class="sxs-lookup"><span data-stu-id="97d14-530">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="97d14-531">Všimněte si, že obsah, který byl součástí této sady, obsahuje pouze soubory **. kávy** .</span><span class="sxs-lookup"><span data-stu-id="97d14-531">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="97d14-532">Můžete také zjistit, že kód CoffeeScript byl zkompilován do JavaScriptu a řádky s komentářem byly odstraněny.</span><span class="sxs-lookup"><span data-stu-id="97d14-532">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="97d14-533">![Sada dynamických souborů JS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Sada dynamických souborů JS")</span><span class="sxs-lookup"><span data-stu-id="97d14-533">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="97d14-534">*Sada dynamických souborů JS*</span><span class="sxs-lookup"><span data-stu-id="97d14-534">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="97d14-535">Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="97d14-535">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="97d14-536">Souhrn</span><span class="sxs-lookup"><span data-stu-id="97d14-536">Summary</span></span>

<span data-ttu-id="97d14-537">Toto testovací prostředí vám pomůže pochopit, co je nového v ASP.NET a vývoji pro web v aplikaci Visual Studio 2012 a jak využít výhod různých vylepšení v rámci sady Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="97d14-537">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="97d14-538">Po absolvování tohoto praktického cvičení se naučíte používat nové funkce a vylepšení editorů Visual Studio 2012 pro šablony stylů CSS, JavaScript a HTML.</span><span class="sxs-lookup"><span data-stu-id="97d14-538">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="97d14-539">Navíc se naučíte, jak Visual Studio 2012 implementuje předdefinované sdružování a minifikace.</span><span class="sxs-lookup"><span data-stu-id="97d14-539">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="97d14-540">Příloha A: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="97d14-540">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="97d14-541">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="97d14-541">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="97d14-542">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="97d14-542">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="97d14-543">Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="97d14-543">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="97d14-544">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="97d14-544">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="97d14-545">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="97d14-545">Click on **Install Now**.</span></span> <span data-ttu-id="97d14-546">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="97d14-546">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="97d14-547">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="97d14-547">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="97d14-548">![Nainstalovat Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="97d14-548">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="97d14-549">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="97d14-549">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="97d14-550">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="97d14-550">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="97d14-552">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="97d14-552">*Accepting the license terms*</span></span>
5. <span data-ttu-id="97d14-553">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="97d14-553">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="97d14-555">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="97d14-555">*Installation progress*</span></span>
6. <span data-ttu-id="97d14-556">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="97d14-556">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="97d14-558">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="97d14-558">*Installation completed*</span></span>
7. <span data-ttu-id="97d14-559">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="97d14-559">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="97d14-560">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="97d14-560">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="97d14-562">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="97d14-562">*VS Express for Web tile*</span></span>

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="97d14-563">Příloha B: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="97d14-563">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="97d14-564">V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="97d14-564">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="97d14-565">Úloha 1 – Vytvoření nového webu z portálu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="97d14-565">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="97d14-566">Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="97d14-566">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-567">S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu.</span><span class="sxs-lookup"><span data-stu-id="97d14-567">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="97d14-568">[Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="97d14-568">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="97d14-569">![Přihlaste se k Windows Azure Portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Přihlaste se k Windows Azure Portal")</span><span class="sxs-lookup"><span data-stu-id="97d14-569">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="97d14-570">*Přihlášení k Windows Azure Portál pro správu*</span><span class="sxs-lookup"><span data-stu-id="97d14-570">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="97d14-571">Na panelu příkazů klikněte na **Nový** .</span><span class="sxs-lookup"><span data-stu-id="97d14-571">Click **New** on the command bar.</span></span>

    <span data-ttu-id="97d14-572">![Vytvoření nového webu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Vytvoření nového webu")</span><span class="sxs-lookup"><span data-stu-id="97d14-572">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="97d14-573">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="97d14-573">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="97d14-574">Klikněte na **compute** | **Web**.</span><span class="sxs-lookup"><span data-stu-id="97d14-574">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="97d14-575">Pak vyberte možnost **rychlé vytvoření** .</span><span class="sxs-lookup"><span data-stu-id="97d14-575">Then select **Quick Create** option.</span></span> <span data-ttu-id="97d14-576">Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.</span><span class="sxs-lookup"><span data-stu-id="97d14-576">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-577">Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat.</span><span class="sxs-lookup"><span data-stu-id="97d14-577">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="97d14-578">Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál.</span><span class="sxs-lookup"><span data-stu-id="97d14-578">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="97d14-579">Nezahrnuje kroky pro nastavení databáze.</span><span class="sxs-lookup"><span data-stu-id="97d14-579">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="97d14-580">![Vytvoření nového webu pomocí rychlého vytvoření](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Vytvoření nového webu pomocí rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="97d14-580">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="97d14-581">*Vytvoření nového webu pomocí rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="97d14-581">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="97d14-582">Počkejte, než se nový **Web** vytvoří.</span><span class="sxs-lookup"><span data-stu-id="97d14-582">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="97d14-583">Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** .</span><span class="sxs-lookup"><span data-stu-id="97d14-583">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="97d14-584">Ověřte, zda nový web funguje.</span><span class="sxs-lookup"><span data-stu-id="97d14-584">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="97d14-585">![Procházení na nový web](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="97d14-585">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="97d14-586">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="97d14-586">*Browsing to the new web site*</span></span>

    <span data-ttu-id="97d14-587">![Běžící Web](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Běžící Web")</span><span class="sxs-lookup"><span data-stu-id="97d14-587">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="97d14-588">*Běžící Web*</span><span class="sxs-lookup"><span data-stu-id="97d14-588">*Web site running*</span></span>
6. <span data-ttu-id="97d14-589">Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="97d14-589">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="97d14-590">![Otevření stránek správy webu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Otevření stránek správy webu")</span><span class="sxs-lookup"><span data-stu-id="97d14-590">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="97d14-591">*Otevření stránek správy webu*</span><span class="sxs-lookup"><span data-stu-id="97d14-591">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="97d14-592">Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .</span><span class="sxs-lookup"><span data-stu-id="97d14-592">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-593">*Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace.</span><span class="sxs-lookup"><span data-stu-id="97d14-593">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="97d14-594">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace.</span><span class="sxs-lookup"><span data-stu-id="97d14-594">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="97d14-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="97d14-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="97d14-596">![Stahuje se publikační profil webu.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Stahuje se publikační profil webu.")</span><span class="sxs-lookup"><span data-stu-id="97d14-596">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="97d14-597">*Stahuje se publikační profil webu.*</span><span class="sxs-lookup"><span data-stu-id="97d14-597">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="97d14-598">Stáhněte si soubor profilu publikování do známého umístění.</span><span class="sxs-lookup"><span data-stu-id="97d14-598">Download the publish profile file to a known location.</span></span> <span data-ttu-id="97d14-599">V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97d14-599">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="97d14-600">![Ukládání souboru profilu publikování](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Ukládá se publikační profil.")</span><span class="sxs-lookup"><span data-stu-id="97d14-600">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="97d14-601">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="97d14-601">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="97d14-602">Úloha 2 – Konfigurace databázového serveru</span><span class="sxs-lookup"><span data-stu-id="97d14-602">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="97d14-603">Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="97d14-603">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="97d14-604">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="97d14-604">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="97d14-605">Pro uložení aplikační databáze budete potřebovat server SQL Database.</span><span class="sxs-lookup"><span data-stu-id="97d14-605">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="97d14-606">SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**.</span><span class="sxs-lookup"><span data-stu-id="97d14-606">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="97d14-607">Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="97d14-607">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="97d14-608">Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách.</span><span class="sxs-lookup"><span data-stu-id="97d14-608">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="97d14-609">Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="97d14-609">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="97d14-610">![Řídicí panel serveru SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "Řídicí panel serveru SQL Database")</span><span class="sxs-lookup"><span data-stu-id="97d14-610">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="97d14-611">*Řídicí panel serveru SQL Database*</span><span class="sxs-lookup"><span data-stu-id="97d14-611">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="97d14-612">V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru.</span><span class="sxs-lookup"><span data-stu-id="97d14-612">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="97d14-613">Provedete to tak, že kliknete na **Konfigurovat**, vyberete IP adresu z **aktuální IP adresy klienta** a vložíte ji do textových polí **Počáteční IP adresa** a **koncová IP** adresa.</span><span class="sxs-lookup"><span data-stu-id="97d14-613">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="97d14-614">Zadejte název pravidla a klikněte na tlačítko ![přidat-Client-IP-Address-tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) tlačítko.</span><span class="sxs-lookup"><span data-stu-id="97d14-614">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![Přidává se IP adresa klienta.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="97d14-616">*Přidává se IP adresa klienta.*</span><span class="sxs-lookup"><span data-stu-id="97d14-616">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="97d14-617">Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="97d14-617">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrdit změny](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="97d14-619">*Potvrdit změny*</span><span class="sxs-lookup"><span data-stu-id="97d14-619">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="97d14-620">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="97d14-620">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="97d14-621">Vraťte se do řešení ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="97d14-621">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="97d14-622">V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="97d14-622">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="97d14-623">![Publikování aplikace](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="97d14-623">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="97d14-624">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="97d14-624">*Publishing the web site*</span></span>
2. <span data-ttu-id="97d14-625">Importujte profil publikování, který jste uložili v prvním úkolu.</span><span class="sxs-lookup"><span data-stu-id="97d14-625">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="97d14-626">![Import profilu publikování](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="97d14-626">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="97d14-627">*Importuje se publikační profil.*</span><span class="sxs-lookup"><span data-stu-id="97d14-627">*Importing publish profile*</span></span>
3. <span data-ttu-id="97d14-628">Klikněte na **ověřit připojení**.</span><span class="sxs-lookup"><span data-stu-id="97d14-628">Click **Validate Connection**.</span></span> <span data-ttu-id="97d14-629">Po dokončení ověřování klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="97d14-629">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97d14-630">Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="97d14-630">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="97d14-631">![Ověřování připojení](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="97d14-631">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="97d14-632">*Ověřování připojení*</span><span class="sxs-lookup"><span data-stu-id="97d14-632">*Validating connection*</span></span>
4. <span data-ttu-id="97d14-633">Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="97d14-633">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="97d14-634">![Konfigurace nasazení webu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="97d14-634">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="97d14-635">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="97d14-635">*Web deploy configuration*</span></span>
5. <span data-ttu-id="97d14-636">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="97d14-636">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="97d14-637">Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="97d14-637">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="97d14-638">V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="97d14-638">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="97d14-639">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="97d14-639">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="97d14-640">Zadejte nový název databáze, například: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="97d14-640">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="97d14-641">![Konfigurace cílového připojovacího řetězce](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Konfigurace cílového připojovacího řetězce")</span><span class="sxs-lookup"><span data-stu-id="97d14-641">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="97d14-642">*Konfigurace cílového připojovacího řetězce*</span><span class="sxs-lookup"><span data-stu-id="97d14-642">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="97d14-643">Pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="97d14-643">Then click **OK**.</span></span> <span data-ttu-id="97d14-644">Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="97d14-644">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="97d14-645">![Vytvoření databáze](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Vytváří se řetězec databáze.")</span><span class="sxs-lookup"><span data-stu-id="97d14-645">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="97d14-646">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="97d14-646">*Creating the database*</span></span>
7. <span data-ttu-id="97d14-647">Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení.</span><span class="sxs-lookup"><span data-stu-id="97d14-647">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="97d14-648">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="97d14-648">Then click **Next**.</span></span>

    <span data-ttu-id="97d14-649">![Připojovací řetězec ukazující na SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Připojovací řetězec ukazující na SQL Database")</span><span class="sxs-lookup"><span data-stu-id="97d14-649">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="97d14-650">*Připojovací řetězec ukazující na SQL Database*</span><span class="sxs-lookup"><span data-stu-id="97d14-650">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="97d14-651">Na stránce **Náhled** klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="97d14-651">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="97d14-652">![Publikování webové aplikace](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="97d14-652">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="97d14-653">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="97d14-653">*Publishing the web application*</span></span>
9. <span data-ttu-id="97d14-654">Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.</span><span class="sxs-lookup"><span data-stu-id="97d14-654">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="97d14-655">![Aplikace byla publikována na platformě Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Aplikace byla publikována na platformě Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="97d14-655">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="97d14-656">*Aplikace byla publikována na platformě Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="97d14-656">*Application published to Windows Azure*</span></span>
