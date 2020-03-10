---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: Použití funkce Page Inspector pro Visual Studio 2012 ve webových formulářích ASP.NET | Microsoft Docs
author: rick-anderson
description: Page Inspector for Visual Studio 2012 je nástroj pro vývoj webu s integrovaným prohlížečem. Vyberte libovolný prvek v integrovaném prohlížeči a klikněte na tlačítko inspektor stránky...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575920"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="00387-104">Použití Page Inspectoru pro Visual Studio 2012 ve webových formulářích ASP.NET</span><span class="sxs-lookup"><span data-stu-id="00387-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>

<span data-ttu-id="00387-105">pomocí Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="00387-105">by Tim Ammann</span></span>

> <span data-ttu-id="00387-106">Page Inspector for Visual Studio 2012 je nástroj pro vývoj webu s integrovaným prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="00387-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="00387-107">Vyberte libovolný prvek v integrovaném prohlížeči a kontrolor stránky okamžitě zvýrazní zdroj a šablonu stylů CSS elementu.</span><span class="sxs-lookup"><span data-stu-id="00387-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="00387-108">Můžete procházet libovolnou stránku aplikace, rychle najít zdroje vykresleného kódu a použít nástroje prohlížeče přímo v prostředí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00387-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="00387-109">V tomto kurzu se dozvíte, jak povolit režim kontroly a pak rychle vyhledat a upravit pravidla a text šablon stylů CSS v rámci webového projektu.</span><span class="sxs-lookup"><span data-stu-id="00387-109">This tutorial shows how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="00387-110">V tomto kurzu se používá projekt aplikace Web Forms, ale můžete také použít nástroj Page Inspector pro webové projekty a aplikace [MVC](https://go.microsoft.com/?linkid=9802002) .</span><span class="sxs-lookup"><span data-stu-id="00387-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="00387-111">V tomto kurzu najdete následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="00387-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="00387-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="00387-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="00387-113">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="00387-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="00387-114">Použití nástroje Page Inspector k zobrazení aplikace</span><span class="sxs-lookup"><span data-stu-id="00387-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="00387-115">Povolit režim kontroly</span><span class="sxs-lookup"><span data-stu-id="00387-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="00387-116">Použití inspektoru stránky k provádění změn značek</span><span class="sxs-lookup"><span data-stu-id="00387-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="00387-117">Režim kontroly a okno HTML</span><span class="sxs-lookup"><span data-stu-id="00387-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> [<span data-ttu-id="00387-118">Náhled změn CSS v okně styly</span><span class="sxs-lookup"><span data-stu-id="00387-118">Preview CSS Changes in the Styles Window</span></span>](#_7_previewing_css)
> 
> [<span data-ttu-id="00387-119">Automatická synchronizace šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="00387-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="00387-120">Použití ovládacího prvku pro výběr barvy CSS</span><span class="sxs-lookup"><span data-stu-id="00387-120">Using the CSS Color Picker</span></span>](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="00387-121">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="00387-121">Prerequisites</span></span>

- <span data-ttu-id="00387-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) nebo [Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="00387-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="00387-123">Pokud chcete získat nejnovější verzi nástroje Page Inspector, nainstalujte pomocí [instalačního programu webové platformy](https://go.microsoft.com/fwlink/?LinkId=255386) sadu Azure SDK pro .NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="00387-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="00387-124">Funkce Page Inspector je zabalené pomocí Microsoft Web Developer Tools.</span><span class="sxs-lookup"><span data-stu-id="00387-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="00387-125">Nejnovější verze je 1,3.</span><span class="sxs-lookup"><span data-stu-id="00387-125">The latest version is 1.3.</span></span> <span data-ttu-id="00387-126">Chcete-li zjistit, kterou verzi máte, spusťte aplikaci Visual Studio a v nabídce **help** vyberte **o Microsoft Visual Studio** .</span><span class="sxs-lookup"><span data-stu-id="00387-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="00387-127">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="00387-127">Create a Web Application</span></span>

<span data-ttu-id="00387-128">Nejprve vytvoříte webovou aplikaci, kterou použijete inspektor stránky s nástrojem.</span><span class="sxs-lookup"><span data-stu-id="00387-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="00387-129">V aplikaci Visual Studio vyberte **soubor** &gt; **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="00387-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="00387-130">Na levé straně rozbalte **C#vizuál**, vyberte **Web**a pak vyberte **ASP.NET Web Forms aplikace**.</span><span class="sxs-lookup"><span data-stu-id="00387-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![Nová aplikace webového formuláře](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="00387-132">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="00387-132">Click **OK**.</span></span>

<span data-ttu-id="00387-133">Aplikace se otevře v zobrazení **zdroje** .</span><span class="sxs-lookup"><span data-stu-id="00387-133">The application opens in **Source** view.</span></span>

![Nová aplikace webových formulářů v zobrazení zdroje](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="00387-135">Teď, když máte aplikaci, se kterou pracujete, můžete ji zkontrolovat a upravit pomocí nástroje Page Inspector.</span><span class="sxs-lookup"><span data-stu-id="00387-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="00387-136">Použití nástroje Page Inspector k zobrazení aplikace</span><span class="sxs-lookup"><span data-stu-id="00387-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="00387-137">V dalším kroku zobrazíte aplikaci s nástrojem Page Inspector.</span><span class="sxs-lookup"><span data-stu-id="00387-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="00387-138">V **Průzkumník řešení**klikněte pravým tlačítkem na projekt a pak zvolte **Zobrazit v okně Kontrola stránky**.</span><span class="sxs-lookup"><span data-stu-id="00387-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![Zobrazit v inspektoru stránky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="00387-140">Ve výchozím nastavení je při prvním spuštění nástroje pro kontrolu stránky ukotveno jako úzké okno na levé straně prostředí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00387-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="00387-141">Ponechte ukotvenou na levé straně a nastavte ji na požadovanou šířku, nebo ji ukotvěte do jedné z oblastí nástrojů nahoře, dole nebo vpravo:</span><span class="sxs-lookup"><span data-stu-id="00387-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![Ukotvené pozice inspektoru stránky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="00387-143">Pokud zrušíte ukotvení okna inspektoru stránky, můžete ho umístit mimo Visual Studio, nebo i na druhý monitor, pokud ho máte.</span><span class="sxs-lookup"><span data-stu-id="00387-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="00387-144">Pokud však chcete ALT + TAB mezi nástrojem Page Inspector a Visual Studio, když je okno Inspektor stránky neukotveno, přejdete do části **nástroje** &gt; **možnosti** &gt; **prostředí** &gt; **karty a okna**a v části **dobře**zaškrtnete zaškrtnutí políčka s **plovoucími okny nástrojů vždy v horní části hlavního okna**:</span><span class="sxs-lookup"><span data-stu-id="00387-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![Zrušte zaškrtnutí políčka plovoucího nástroje okna v systému Windows ALT + TAB mezi Visual Studio a oknem neukotvené kontroly stránky.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="00387-146">V horním podokně okna inspektor stránky se zobrazuje aktuální stránka v okně prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="00387-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="00387-147">Dolní podokno zobrazuje stránku v kódu HTML vlevo a některé karty na pravé straně, které umožňují kontrolu různých aspektů stránky.</span><span class="sxs-lookup"><span data-stu-id="00387-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="00387-148">Dolní podokno se podobá [vývojářské nástroje F12](https://msdn.microsoft.com/ie/aa740478) v Internet Exploreru.</span><span class="sxs-lookup"><span data-stu-id="00387-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="00387-149">(Na rozdíl od vývojářských nástrojů můžete použít inspektor stránky přímo v rámci sady Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="00387-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![Inspektor stránek](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="00387-151">V tomto kurzu použijete podokno Prohlížeč Inspector stránky a kartu **HTML** a **styly** , které vám pomůžou rychle procházet a dělat změny aplikace.</span><span class="sxs-lookup"><span data-stu-id="00387-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="00387-152">Povolit režim kontroly</span><span class="sxs-lookup"><span data-stu-id="00387-152">Enable Inspection Mode</span></span>

<span data-ttu-id="00387-153">V dalším kroku se zobrazí, jak funguje kontrolní režim nástroje Page Inspector.</span><span class="sxs-lookup"><span data-stu-id="00387-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="00387-154">V okně Inspektor stránky klikněte na tlačítko **prozkoumat** .</span><span class="sxs-lookup"><span data-stu-id="00387-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![Kontrola elementu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="00387-156">Chcete-li zobrazit kontrolní režim v akci, přesuňte ukazatel myši na různé části stránky v okně prohlížeče inspektoru stránky.</span><span class="sxs-lookup"><span data-stu-id="00387-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="00387-157">V takovém případě se ukazatel myši změní na velké znaménko plus a element pod je zvýrazněný:</span><span class="sxs-lookup"><span data-stu-id="00387-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Najetí myší na div. Content-wrapper](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="00387-159">Při přesunutí ukazatele myši Pamatujte na to, že</span><span class="sxs-lookup"><span data-stu-id="00387-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="00387-160">Obsah ve zobrazení **zdroje** se změní, aby se zobrazil kód odpovídající vybranému prvku na stránce.</span><span class="sxs-lookup"><span data-stu-id="00387-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="00387-161">Relevantní označení je zvýrazněno.</span><span class="sxs-lookup"><span data-stu-id="00387-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="00387-162">Pokud je zdroj v jiném souboru, tento soubor je otevřen v zobrazení zdroje s zvýrazněným odpovídajícím kódem.</span><span class="sxs-lookup"><span data-stu-id="00387-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="00387-163">Značka zobrazená na kartě **HTML** v inspektoru stránky se také změní, aby odpovídala vybranému prvku na stránce.</span><span class="sxs-lookup"><span data-stu-id="00387-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="00387-164">Na kartě **HTML** jsou relevantní značky poznačené.</span><span class="sxs-lookup"><span data-stu-id="00387-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="00387-165">Karta **styly** zobrazuje pravidla šablon stylů CSS vztahující se k aktuálnímu výběru.</span><span class="sxs-lookup"><span data-stu-id="00387-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="00387-166">Použití inspektoru stránky k provádění změn značek</span><span class="sxs-lookup"><span data-stu-id="00387-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="00387-167">Nyní uvidíte, jak můžete pomocí inspektora stránky vyhledat a změnit značky nebo text, jehož umístění nemusí být okamžitě zřejmé.</span><span class="sxs-lookup"><span data-stu-id="00387-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="00387-168">Umístěte inspektor stránky v režimu kontroly a potom přejděte k dolnímu okraji domovské stránky.</span><span class="sxs-lookup"><span data-stu-id="00387-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="00387-169">Jakmile zadáte oblast s zápatím, zobrazí se v okně zobrazení **zdroje** na dočasnou kartě na pravé straně stránky rozložení *Web. Master* a zvýrazní se část stránky předlohy, kterou jste vybrali.</span><span class="sxs-lookup"><span data-stu-id="00387-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="00387-170">Tím se dozvíte, jak může inspektor stránky najít a zobrazit obsah na stránce, která může být skutečně popsána z jiného souboru, než ze kterého jste původně otevřeli.</span><span class="sxs-lookup"><span data-stu-id="00387-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![Zvýraznění zápatí v režimu kontroly](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="00387-172">V okně prohlížeče inspektora stránky přesuňte ukazatel myši na řádek s oznámením o autorských <a id="a"> </a>právech.</span><span class="sxs-lookup"><span data-stu-id="00387-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="00387-173">Na stránce *site. Master* se zvýrazní odpovídající řádek.</span><span class="sxs-lookup"><span data-stu-id="00387-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![Zvýrazněný řádek copyrightu pro zápatí](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="00387-175">Přidejte nějaký text na konec řádku v souboru *Web. Master* .</span><span class="sxs-lookup"><span data-stu-id="00387-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="00387-176">&lt;p&gt;&amp;kopie; &lt;%: DateTime. Now. Year%&gt; – moje aplikace ASP.NET Rocks.&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="00387-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="00387-177">Nyní stiskněte kombinaci kláves CTRL + ALT + ENTER nebo kliknutím na panel aktualizace zobrazte výsledky v okně prohlížeče inspektoru stránky.</span><span class="sxs-lookup"><span data-stu-id="00387-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![Moje aplikace ASP.NET Rocks!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="00387-179">Možná jste si mysleli, že se zápatí nacházelo na stránce *Default. aspx* , ale že je na stránce rozložení stránky hlavní, ale jeho vzhled byl za vás.</span><span class="sxs-lookup"><span data-stu-id="00387-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="00387-180">Režim kontroly a okno HTML</span><span class="sxs-lookup"><span data-stu-id="00387-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="00387-181">V dalším kroku budete mít rychlý přehled o okně HTML a o tom, jak mapuje prvky pro vás.</span><span class="sxs-lookup"><span data-stu-id="00387-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="00387-182">Umístit inspektor stránky v režimu kontroly.</span><span class="sxs-lookup"><span data-stu-id="00387-182">Put Page Inspector in Inspection Mode.</span></span>

![Kontrola elementu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="00387-184">Klikněte na horní část stránky s textem "vaše logo".</span><span class="sxs-lookup"><span data-stu-id="00387-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="00387-185">Podrobněji prozkoumáte konkrétní prvek, takže zobrazení v okně prohlížeče se již nemění při přesunutí ukazatele myši.</span><span class="sxs-lookup"><span data-stu-id="00387-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="00387-186">Nyní přesuňte ukazatel myši do okna **HTML** .</span><span class="sxs-lookup"><span data-stu-id="00387-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="00387-187">Když přesunete ukazatel myši, inspektor stránky popisuje prvek v okně **HTML** a zvýrazní odpovídající prvek v okně prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="00387-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![Okno HTML](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="00387-189">Stejně jako dřív se otevře okno *site. Master* na dočasné kartě. klikněte na kartu Web. Master a v záhlaví &lt;&gt; oddílu se zvýrazní odpovídající kód:</span><span class="sxs-lookup"><span data-stu-id="00387-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![Zvýrazněný kód](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="00387-191">Náhled změn CSS v okně styly</span><span class="sxs-lookup"><span data-stu-id="00387-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="00387-192">Dále uvidíte, jak můžete pomocí okna **styly** kontroly stránky zobrazit náhled změn v šablonách stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="00387-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="00387-193">Kliknutím na tlačítko **zkontrolovat** můžete umístit inspektora stránky v režimu kontroly.</span><span class="sxs-lookup"><span data-stu-id="00387-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="00387-194">V okně prohlížeče inspektora stránky přesuňte ukazatel myši na domovskou stránku, dokud se nezobrazí popisek **div. Content-wrapper** .</span><span class="sxs-lookup"><span data-stu-id="00387-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Najetí myší na elementy](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="00387-196">Jednou klikněte v části div. Content-wrapper a pak přesuňte ukazatel myši do okna **styly** .</span><span class="sxs-lookup"><span data-stu-id="00387-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="00387-197">V selektoru třídy. Doporučené. obsah-obálka zrušte zaškrtnutí políčka a zaškrtněte políčko u vlastnosti Barva pozadí.</span><span class="sxs-lookup"><span data-stu-id="00387-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![Vymazat barvu pozadí](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="00387-199">Všimněte si, jak se zobrazí náhled změny v okně prohlížeče inspektoru stránky.</span><span class="sxs-lookup"><span data-stu-id="00387-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="00387-200">Zaškrtněte políčko znovu, potom dvakrát klikněte na hodnotu vlastnosti a změňte ji na `red`.</span><span class="sxs-lookup"><span data-stu-id="00387-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="00387-201">Tato změna se zobrazí okamžitě:</span><span class="sxs-lookup"><span data-stu-id="00387-201">The change shows immediately:</span></span>

![Barva červeného pozadí](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="00387-203">Okno **styly** usnadňuje testování a náhled změn CSS před potvrzením změn v samotné šabloně stylů.</span><span class="sxs-lookup"><span data-stu-id="00387-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="00387-204">Automatická synchronizace šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="00387-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="00387-205">Tato funkce vyžaduje verzi 1,3 ovládacího prvku Page Inspector.</span><span class="sxs-lookup"><span data-stu-id="00387-205">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="00387-206">Funkce automatické synchronizace šablon stylů CSS umožňuje přímo upravit soubor CSS a okamžitě zobrazit změny v prohlížeči kontroly stránky.</span><span class="sxs-lookup"><span data-stu-id="00387-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="00387-207">Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.</span><span class="sxs-lookup"><span data-stu-id="00387-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="00387-208">V prohlížeči Inspector stránky přesuňte ukazatel myši nad oddíl "Domovská stránka", dokud se nezobrazí popisek **div. Content-wrapper** .</span><span class="sxs-lookup"><span data-stu-id="00387-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="00387-209">Klikněte jednou pro výběr tohoto prvku.</span><span class="sxs-lookup"><span data-stu-id="00387-209">Click once to select this element.</span></span>

<span data-ttu-id="00387-210">Okno **styly** zobrazuje všechna pravidla šablony stylů CSS pro tento element.</span><span class="sxs-lookup"><span data-stu-id="00387-210">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="00387-211">Přejděte dolů a najděte selektor třídy. Doporučené. Content-wrapper.</span><span class="sxs-lookup"><span data-stu-id="00387-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="00387-212">Klikněte na ". Doporučené. obsah-obálka".</span><span class="sxs-lookup"><span data-stu-id="00387-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="00387-213">Page Inspector otevře soubor CSS, který definuje tento styl (Web. CSS) a zvýrazní odpovídající styl CSS.</span><span class="sxs-lookup"><span data-stu-id="00387-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![Soubor CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="00387-215">Nyní změňte hodnotu `background-color` na "Red".</span><span class="sxs-lookup"><span data-stu-id="00387-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="00387-216">Tato změna se zobrazí okamžitě v prohlížeči Inspector stránky.</span><span class="sxs-lookup"><span data-stu-id="00387-216">The change appears immediately in the Page Inspector browser.</span></span>

![Prohlížeč Inspector stránky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="00387-218">Použití ovládacího prvku pro výběr barvy CSS</span><span class="sxs-lookup"><span data-stu-id="00387-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="00387-219">V dalším kroku se dozvíte, jak pomocí nástroje Page Inspector rychle najít a změnit šablonu stylů CSS zvýrazněného textu ve výchozí aplikaci.</span><span class="sxs-lookup"><span data-stu-id="00387-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="00387-220">V tomto příkladu jste se rozhodli, že se vám nelíbí modrý zvýraznění a chcete ho změnit na jinou barvu.</span><span class="sxs-lookup"><span data-stu-id="00387-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="00387-221">Klikněte na tlačítko **prozkoumat** .</span><span class="sxs-lookup"><span data-stu-id="00387-221">Click the **Inspect** button.</span></span>

![Kontrola elementu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="00387-223">V okně prohlížeče inspektora stránky přesuňte ukazatel myši na zvýrazněné "videa, kurzy a ukázky" tak, aby se zobrazil popisek CSS "značka".</span><span class="sxs-lookup"><span data-stu-id="00387-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![Najetí myší na element značky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="00387-225">Klikněte na text, který chcete vybrat.</span><span class="sxs-lookup"><span data-stu-id="00387-225">Click the text to select it.</span></span> <span data-ttu-id="00387-226">Odpovídající selektor značek CSS se zobrazí v dolní části okna **styly** .</span><span class="sxs-lookup"><span data-stu-id="00387-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![označit selektor v okně styly](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="00387-228">Klikněte na selektor značek.</span><span class="sxs-lookup"><span data-stu-id="00387-228">Click the mark selector.</span></span> <span data-ttu-id="00387-229">Tím se otevře soubor *site. CSS* pro webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="00387-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="00387-230">Klikněte na kartu Web. CSS a zvýrazní se odpovídající šablona stylů CSS pro selektor:</span><span class="sxs-lookup"><span data-stu-id="00387-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![Označte selektor v šabloně stylů.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="00387-232">Vyberte a odeberte čáru s vlastností background-color.</span><span class="sxs-lookup"><span data-stu-id="00387-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="00387-233">Nyní použijete nový výběr barvy CSS sady Visual Studio 2012 k výběru nové barvy vlastnosti Barva pozadí **značky** .</span><span class="sxs-lookup"><span data-stu-id="00387-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="00387-234">Použití výběru barvy CSS sady Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="00387-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="00387-235">Editor CSS v aplikaci Visual Studio 2012 má výběr barvy, který usnadňuje výběr a vložení barev.</span><span class="sxs-lookup"><span data-stu-id="00387-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="00387-236">Má jednoduchý pruh barev a "rozbalovací" výběr, který nabízí lepší kontrolu.</span><span class="sxs-lookup"><span data-stu-id="00387-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="00387-237">Výběr barvy obsahuje standardní paletu barev, podporuje standardní názvy barev, kódy hash, RGB, RGBA, HSL a HSLA barvy a udržuje seznam barev, které jste naposledy použili v dokumentu.</span><span class="sxs-lookup"><span data-stu-id="00387-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="00387-238">Na řádku, kde byla vlastnost background-color, zadejte "BC" a stiskněte šipku dolů.</span><span class="sxs-lookup"><span data-stu-id="00387-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="00387-239">Když zadáte první znak každého slova ve vlastnosti oddělené spojovníky, například background-color, IntelliSense vyfiltruje seznam, abyste zobrazili pouze vlastnosti, které odpovídají:</span><span class="sxs-lookup"><span data-stu-id="00387-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Filtrované hodnoty IntelliSense](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="00387-241">Nyní zadejte dvojtečku.</span><span class="sxs-lookup"><span data-stu-id="00387-241">Now type a colon.</span></span> <span data-ttu-id="00387-242">Když to uděláte, bude vložen celý název vlastnosti Barva pozadí.</span><span class="sxs-lookup"><span data-stu-id="00387-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="00387-243">Zadejte **#** nebo **RGB (** a zobrazí se panel pro výběr barvy:</span><span class="sxs-lookup"><span data-stu-id="00387-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![Panel pro výběr barvy CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="00387-245">Chcete-li zjistit, jak panel pro výběr barvy funguje, klikněte na jeho barvy ukazatelem myši, nebo stiskněte klávesu šipka dolů a pak použijte šipky vlevo a vpravo k procházení barev.</span><span class="sxs-lookup"><span data-stu-id="00387-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="00387-246">Při návštěvě barvy se zobrazí náhled odpovídající hodnoty vlastnosti background-color:</span><span class="sxs-lookup"><span data-stu-id="00387-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![Náhled hodnoty vlastnosti background-color](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="00387-248">V tomto okamžiku můžete stisknutím klávesy Enter vybrat hodnotu a potom středníku (;) k dokončení položky šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="00387-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="00387-249">Prozatím přejděte k další části, abyste viděli, jak funguje automaticky otevírané okno pro výběr barvy.</span><span class="sxs-lookup"><span data-stu-id="00387-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="00387-250">Použití rozbalovací nabídky pro výběr barvy</span><span class="sxs-lookup"><span data-stu-id="00387-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="00387-251">Když pruh barev nemá přesnou barvu, kterou hledáte, můžete použít rozevírací nabídka pro výběr barvy.</span><span class="sxs-lookup"><span data-stu-id="00387-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="00387-252">Chcete-li jej otevřít, klikněte na dvojitou dvojitou šipku na pravém konci pruhu barev nebo na klávesnici stiskněte šipku dolů nebo dvakrát.</span><span class="sxs-lookup"><span data-stu-id="00387-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![Místní nabídka pro výběr barvy CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="00387-254">Klikněte na barvu ze svislého pruhu na pravé straně.</span><span class="sxs-lookup"><span data-stu-id="00387-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="00387-255">Tím se v hlavním okně zobrazí barevný přechod pro tuto barvu.</span><span class="sxs-lookup"><span data-stu-id="00387-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="00387-256">Vyberte barvu přímo ze svislého pruhu stisknutím klávesy ENTER nebo kliknutím na libovolný bod v hlavním okně vyberte s větší přesností.</span><span class="sxs-lookup"><span data-stu-id="00387-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="00387-257">Pokud je na obrazovce počítače barva, kterou chcete použít (nemusí být uvnitř uživatelského rozhraní sady Visual Studio), můžete zachytit její hodnotu pomocí nástroje kapátka v pravém dolním rohu.</span><span class="sxs-lookup"><span data-stu-id="00387-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="00387-258">Můžete také změnit neprůhlednost barvy přesunutím posuvníku v dolní části výběru barvy.</span><span class="sxs-lookup"><span data-stu-id="00387-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="00387-259">Tím se změní hodnoty barev na hodnoty RGBA, protože formát RGBA může představovat neprůhlednost.</span><span class="sxs-lookup"><span data-stu-id="00387-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="00387-260">Po zvolení barvy stiskněte klávesu ENTER a zadáním středníku dokončete položku pozadí-Color v souboru *site. CSS* .</span><span class="sxs-lookup"><span data-stu-id="00387-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="00387-261">Panel aktualizace inspektoru stránky</span><span class="sxs-lookup"><span data-stu-id="00387-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="00387-262">Funkce Page Inspector okamžitě rozpozná změnu v souboru *Web. CSS* (nebo do libovolného souboru v aplikaci) a zobrazí výstrahu na panelu aktualizace.</span><span class="sxs-lookup"><span data-stu-id="00387-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![Aktualizovat panel](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="00387-264">Chcete-li uložit všechny soubory a aktualizovat prohlížeč kontroly stránky, stiskněte klávesy CTRL + ALT + ENTER nebo klikněte na panel aktualizace.</span><span class="sxs-lookup"><span data-stu-id="00387-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="00387-265">Změna barvy zvýraznění se zobrazí v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="00387-265">The change in the highlight color appears in the browser:</span></span>

![Barva zvýraznění změněna](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="00387-267">Všimněte si, že jste pohodlně aktualizovali prohlížeč inspektoru stránky přímo z prostředí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00387-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="00387-268">Použití nástroje Page Inspector místo externího prohlížeče vám umožní zůstat v editoru při vývoji webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="00387-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="00387-269">Viz také</span><span class="sxs-lookup"><span data-stu-id="00387-269">See Also</span></span>

<span data-ttu-id="00387-270">[Úvod do inspektoru stránky](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (video pro kanál 9)</span><span class="sxs-lookup"><span data-stu-id="00387-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="00387-271">[Chybové zprávy v inspektoru stránky](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="00387-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
