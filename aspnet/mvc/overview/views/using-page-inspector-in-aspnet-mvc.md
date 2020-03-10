---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: Používání funkce Page Inspector v ASP.NET MVC | Microsoft Docs
author: rick-anderson
description: Nástroj Page Inspector v aplikaci Visual Studio 2012 je webovým nástrojem pro vývoj na webu s integrovaným prohlížečem. Vyberte libovolný prvek v integrovaném prohlížeči a klikněte na tlačítko inspektor stránky i...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538015"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="b8288-104">Použití Page Inspectoru v ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b8288-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="b8288-105">pomocí Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="b8288-105">by Tim Ammann</span></span>

> <span data-ttu-id="b8288-106">Nástroj Page Inspector v aplikaci Visual Studio 2012 je webovým nástrojem pro vývoj na webu s integrovaným prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="b8288-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="b8288-107">Vyberte libovolný prvek v integrovaném prohlížeči a kontrolor stránky okamžitě zvýrazní zdroj a šablonu stylů CSS elementu.</span><span class="sxs-lookup"><span data-stu-id="b8288-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="b8288-108">Můžete procházet libovolné zobrazení MVC, rychle najít zdroje vykreslených značek a použít nástroje prohlížeče přímo v prostředí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8288-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="b8288-109">Přehrát video</span><span class="sxs-lookup"><span data-stu-id="b8288-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="b8288-110">V tomto kurzu se dozvíte, jak povolit režim kontroly a pak rychle vyhledat a upravit značky a šablony stylů CSS v rámci webového projektu.</span><span class="sxs-lookup"><span data-stu-id="b8288-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="b8288-111">V tomto kurzu se používá projekt MVC, ale můžete také použít nástroj Page Inspector pro [webové formuláře](https://go.microsoft.com/?linkid=9802001) a jiné aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b8288-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="b8288-112">V tomto kurzu najdete následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="b8288-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="b8288-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b8288-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="b8288-114">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="b8288-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="b8288-115">Použití inspektoru stránky k procházení zobrazení</span><span class="sxs-lookup"><span data-stu-id="b8288-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="b8288-116">Povolit režim kontroly</span><span class="sxs-lookup"><span data-stu-id="b8288-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="b8288-117">Použití inspektoru stránky k provádění změn značek</span><span class="sxs-lookup"><span data-stu-id="b8288-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="b8288-118">Režim kontroly a okno HTML</span><span class="sxs-lookup"><span data-stu-id="b8288-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="b8288-119">Náhled změn CSS v okně styly</span><span class="sxs-lookup"><span data-stu-id="b8288-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="b8288-120">Automatická synchronizace šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="b8288-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="b8288-121">Použití ovládacího prvku pro výběr barvy CSS</span><span class="sxs-lookup"><span data-stu-id="b8288-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="b8288-122">Mapování dynamických prvků stránky na JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8288-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="b8288-123">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="b8288-123">Prerequisites</span></span>

- <span data-ttu-id="b8288-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) nebo [Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="b8288-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="b8288-125">Pokud chcete získat nejnovější verzi nástroje Page Inspector, nainstalujte sadu Windows Azure SDK pro .NET 2,0 pomocí [instalačního programu webové platformy](https://go.microsoft.com/fwlink/?LinkId=255386) .</span><span class="sxs-lookup"><span data-stu-id="b8288-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="b8288-126">Funkce Page Inspector je zabalené pomocí Microsoft Web Developer Tools.</span><span class="sxs-lookup"><span data-stu-id="b8288-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="b8288-127">Nejnovější verze je 1,3.</span><span class="sxs-lookup"><span data-stu-id="b8288-127">The latest version is 1.3.</span></span> <span data-ttu-id="b8288-128">Chcete-li zjistit, kterou verzi máte, spusťte aplikaci Visual Studio a v nabídce **help** vyberte **o Microsoft Visual Studio** .</span><span class="sxs-lookup"><span data-stu-id="b8288-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="b8288-129">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="b8288-129">Create a Web Application</span></span>

<span data-ttu-id="b8288-130">Nejprve vytvořte webovou aplikaci, ve které budete používat inspektor stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="b8288-131">V aplikaci Visual Studio vyberte **soubor** &gt; **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="b8288-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="b8288-132">Na levé straně rozbalte **C#vizuál**, vyberte **Web**a pak vyberte **Webová aplikace ASP.NET MVC4**.</span><span class="sxs-lookup"><span data-stu-id="b8288-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![Nová aplikace ASP.NET MVC](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="b8288-134">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8288-134">Click **OK**.</span></span>

<span data-ttu-id="b8288-135">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte **internetovou aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="b8288-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="b8288-136">Ponechá **Razor** jako výchozí zobrazovací modul.</span><span class="sxs-lookup"><span data-stu-id="b8288-136">Leave **Razor** as the default view engine.</span></span>

![Nový projekt ASP.NET MVC – Internetová aplikace](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="b8288-138">Aplikace se otevře v zobrazení **zdroje** .</span><span class="sxs-lookup"><span data-stu-id="b8288-138">The application opens in **Source** view.</span></span>

![Nová aplikace ASP.NET MVC v zobrazení zdroje](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="b8288-140">Teď, když máte aplikaci, se kterou pracujete, můžete ji zkontrolovat a upravit pomocí nástroje Page Inspector.</span><span class="sxs-lookup"><span data-stu-id="b8288-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="b8288-141">Použití inspektoru stránky k procházení zobrazení</span><span class="sxs-lookup"><span data-stu-id="b8288-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="b8288-142">V aplikaci Visual Studio 2012 můžete kliknout pravým tlačítkem myši na libovolné zobrazení v projektu, vybrat **Zobrazit v okně Kontrola stránky**a obrazovka inspektor stránky poukáže cestu a zobrazí stránku.</span><span class="sxs-lookup"><span data-stu-id="b8288-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="b8288-143">V **Průzkumník řešení**rozbalte složku **zobrazení** a pak do **domovské** složky.</span><span class="sxs-lookup"><span data-stu-id="b8288-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="b8288-144">Klikněte pravým tlačítkem na soubor index. cshtml a **v okně Kontrola stránky vyberte Zobrazit**.</span><span class="sxs-lookup"><span data-stu-id="b8288-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Zobrazit index. cshtml v inspektoru stránky](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="b8288-146">Ve výchozím nastavení je inspektor stránky ukotven jako okno na levé straně prostředí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8288-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="b8288-147">Pokud budete chtít, můžete ho ukotvit jinde nebo zrušit ukotvení okna.</span><span class="sxs-lookup"><span data-stu-id="b8288-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="b8288-148">Informace naleznete v tématu [How to: uspořádávat and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8288-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="b8288-149">V horním podokně okna inspektor stránky se zobrazuje aktuální stránka v okně prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b8288-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="b8288-150">Dolní podokno zobrazuje stránku v kódu HTML spolu s některými kartami, které umožňují kontrolovat různé aspekty stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="b8288-151">Dolní podokno se podobá [vývojářské nástroje F12](https://msdn.microsoft.com/ie/aa740478) v Internet Exploreru.</span><span class="sxs-lookup"><span data-stu-id="b8288-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Aplikace ASP.NET MVC v inspektoru stránky](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="b8288-153">V tomto kurzu použijete kartu **HTML** a **styly** k rychlému procházení a provádění změn v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b8288-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="b8288-154">EnableInspection režim</span><span class="sxs-lookup"><span data-stu-id="b8288-154">EnableInspection Mode</span></span>

<span data-ttu-id="b8288-155">Chcete-li umístit inspektor stránky do režimu kontroly, klikněte na tlačítko **prozkoumat** .</span><span class="sxs-lookup"><span data-stu-id="b8288-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="b8288-156">V režimu kontroly, když držíte ukazatel myši v jakékoli části vykreslené stránky, je zvýrazněn odpovídající zdrojový kód nebo kód.</span><span class="sxs-lookup"><span data-stu-id="b8288-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![Přepnout režim kontroly](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="b8288-158">Nyní přesuňte ukazatel myši na různé části stránky v rámci nástroje Page Inspector.</span><span class="sxs-lookup"><span data-stu-id="b8288-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="b8288-159">V takovém případě se ukazatel myši změní na velké znaménko plus a element pod je zvýrazněný:</span><span class="sxs-lookup"><span data-stu-id="b8288-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Najetí myší na div. Content-wrapper](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="b8288-161">Při přesunutí ukazatele myši zvýrazní aplikace Visual Studio odpovídající syntaxe Razor ve zdrojovém souboru.</span><span class="sxs-lookup"><span data-stu-id="b8288-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="b8288-162">Pokud prvek HTML pochází z jiného zdrojového souboru, Visual Studio automaticky otevře soubor.</span><span class="sxs-lookup"><span data-stu-id="b8288-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="b8288-163">V nástroji Page Inspector zobrazuje karta **HTML** kód HTML, který byl vygenerován z syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="b8288-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="b8288-164">Při přesunutí ukazatele myši jsou zvýrazněny prvky HTML.</span><span class="sxs-lookup"><span data-stu-id="b8288-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="b8288-165">Karta **styly** zobrazuje pravidla šablony stylů CSS pro element.</span><span class="sxs-lookup"><span data-stu-id="b8288-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="b8288-166">Použití inspektoru stránky k provádění změn značek</span><span class="sxs-lookup"><span data-stu-id="b8288-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="b8288-167">Page Inspector vám umožní najít značky, jejichž umístění nemusí být zřejmé.</span><span class="sxs-lookup"><span data-stu-id="b8288-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="b8288-168">Pak můžete značky upravit a zobrazit výsledné změny.</span><span class="sxs-lookup"><span data-stu-id="b8288-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="b8288-169">Pokud to chcete vidět, klikněte na **zkontrolovat** a potom se posuňte do dolní části stránky v okně Inspektor stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="b8288-170">Při přesunutí ukazatele myši do oblasti zápatí otevře okno Inspektor stránky soubor \_layout. cshtml a zvýrazní část stránky rozložení, kterou jste vybrali.</span><span class="sxs-lookup"><span data-stu-id="b8288-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="b8288-171">Jak vidíte, zápatí je definováno v souboru rozložení, a ne v samotném zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b8288-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![Dolní](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="b8288-173">Nyní přesuňte ukazatel myši na řádek s oznámením o autorských právech <a id="a"> </a>.</span><span class="sxs-lookup"><span data-stu-id="b8288-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="b8288-174">Na stránce \_layout. cshtml se zvýrazní odpovídající řádek.</span><span class="sxs-lookup"><span data-stu-id="b8288-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![Zvýrazněný řádek copyrightu pro zápatí](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="b8288-176">Přidejte nějaký text na konec řádku v souboru \_layout. cshtml.</span><span class="sxs-lookup"><span data-stu-id="b8288-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="b8288-177">&lt;p&gt;&amp;kopie; @DateTime.Now.Year – moje aplikace ASP.NET MVC Rocks&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="b8288-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="b8288-178">Nyní stiskněte kombinaci kláves CTRL + ALT + ENTER nebo kliknutím na panel aktualizace zobrazte výsledky v okně prohlížeče inspektoru stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![Moje aplikace ASP.NET Rocks!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="b8288-180">Možná jste si mysleli, že se zápatí definované v indexu. cshtml, ale je zavedené v \_layout. cshtml a inspektor stránky ho pro vás našel.</span><span class="sxs-lookup"><span data-stu-id="b8288-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="b8288-181">Režim kontroly a okno HTML</span><span class="sxs-lookup"><span data-stu-id="b8288-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="b8288-182">V dalším kroku budete mít rychlý přehled o okně HTML a o tom, jak mapuje prvky pro vás.</span><span class="sxs-lookup"><span data-stu-id="b8288-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="b8288-183">Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.</span><span class="sxs-lookup"><span data-stu-id="b8288-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="b8288-184">Klikněte na horní část stránky s textem "vaše logo".</span><span class="sxs-lookup"><span data-stu-id="b8288-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="b8288-185">Podrobněji prozkoumáte konkrétní prvek, takže zobrazení v okně prohlížeče se již nemění při přesunutí ukazatele myši.</span><span class="sxs-lookup"><span data-stu-id="b8288-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="b8288-186">Nyní přesuňte ukazatel myši do okna **HTML** .</span><span class="sxs-lookup"><span data-stu-id="b8288-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="b8288-187">Když přesunete ukazatel myši, inspektor stránky popisuje prvek v okně **HTML** a zvýrazní odpovídající prvek v okně prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="b8288-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![Okno HTML](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="b8288-189">Stejně jako předtím otevře okno \_layout. cshtml pro vás na dočasné kartě. klikněte na položku \_layout. cshtml dočasná karta a odpovídající kód se zvýrazní v&gt; části hlavičky &lt;pro vás:</span><span class="sxs-lookup"><span data-stu-id="b8288-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![Zvýrazněný kód](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="b8288-191">Náhled změn CSS v okně styly</span><span class="sxs-lookup"><span data-stu-id="b8288-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="b8288-192">V dalším kroku použijete okno **styly** kontroly stránky k zobrazení náhledu změn v šablonách stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="b8288-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="b8288-193">Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.</span><span class="sxs-lookup"><span data-stu-id="b8288-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="b8288-194">V okně prohlížeče inspektora stránky přesuňte ukazatel myši na domovskou stránku, dokud se nezobrazí popisek **div. Content-wrapper** .</span><span class="sxs-lookup"><span data-stu-id="b8288-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Najetí myší na div. Content-wrapper](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="b8288-196">Jednou klikněte v části div. Content-wrapper a pak přesuňte ukazatel myši do okna **styly** .</span><span class="sxs-lookup"><span data-stu-id="b8288-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="b8288-197">Okno **styly** zobrazuje všechna pravidla šablony stylů CSS pro tento element.</span><span class="sxs-lookup"><span data-stu-id="b8288-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="b8288-198">Přejděte dolů a najděte selektor třídy. Doporučené. Content-wrapper.</span><span class="sxs-lookup"><span data-stu-id="b8288-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="b8288-199">Nyní zrušte zaškrtnutí políčka u vlastnosti background-color.</span><span class="sxs-lookup"><span data-stu-id="b8288-199">Now clear the checkbox for the background-color property.</span></span>

![Vymazat barvu pozadí](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="b8288-201">Všimněte si, jak se zobrazí náhled změny v okně prohlížeče inspektoru stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="b8288-202">Zaškrtněte políčko znovu, potom dvakrát klikněte na hodnotu vlastnosti a změňte ji na červenou.</span><span class="sxs-lookup"><span data-stu-id="b8288-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="b8288-203">Tato změna se zobrazí okamžitě:</span><span class="sxs-lookup"><span data-stu-id="b8288-203">The change shows immediately:</span></span>

![Barva červeného pozadí](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="b8288-205">Okno **styly** usnadňuje testování a náhled změn CSS před potvrzením změn v samotné šabloně stylů.</span><span class="sxs-lookup"><span data-stu-id="b8288-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="b8288-206">Automatická synchronizace šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="b8288-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="b8288-207">Tato funkce vyžaduje verzi 1,3 ovládacího prvku Page Inspector.</span><span class="sxs-lookup"><span data-stu-id="b8288-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="b8288-208">Funkce automatické synchronizace šablon stylů CSS umožňuje přímo upravit soubor CSS a okamžitě zobrazit změny v prohlížeči kontroly stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="b8288-209">Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.</span><span class="sxs-lookup"><span data-stu-id="b8288-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="b8288-210">V prohlížeči Inspector stránky přesuňte ukazatel myši nad oddíl "Domovská stránka", dokud se nezobrazí popisek **div. Content-wrapper** .</span><span class="sxs-lookup"><span data-stu-id="b8288-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="b8288-211">Klikněte jednou pro výběr tohoto prvku.</span><span class="sxs-lookup"><span data-stu-id="b8288-211">Click once to select this element.</span></span>

<span data-ttu-id="b8288-212">Okno **styly** zobrazuje všechna pravidla šablony stylů CSS pro tento element.</span><span class="sxs-lookup"><span data-stu-id="b8288-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="b8288-213">Přejděte dolů a najděte selektor třídy. Doporučené. Content-wrapper.</span><span class="sxs-lookup"><span data-stu-id="b8288-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="b8288-214">Klikněte na ". Doporučené. obsah-obálka".</span><span class="sxs-lookup"><span data-stu-id="b8288-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="b8288-215">Page Inspector otevře soubor CSS, který definuje tento styl (Web. CSS) a zvýrazní odpovídající styl CSS.</span><span class="sxs-lookup"><span data-stu-id="b8288-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="b8288-216">Nyní změňte hodnotu `background-color` na "Red".</span><span class="sxs-lookup"><span data-stu-id="b8288-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="b8288-217">Tato změna se zobrazí okamžitě v prohlížeči Inspector stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="b8288-218">Použití ovládacího prvku pro výběr barvy CSS</span><span class="sxs-lookup"><span data-stu-id="b8288-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="b8288-219">Editor CSS v aplikaci Visual Studio 2012 má výběr barvy, který usnadňuje výběr a vložení barev.</span><span class="sxs-lookup"><span data-stu-id="b8288-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="b8288-220">Výběr barvy obsahuje standardní paletu barev, podporuje standardní názvy barev, kódy hash, RGB, RGBA, HSL a HSLA barvy a udržuje seznam barev, které jste naposledy použili v dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b8288-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="b8288-221">V předchozí části jste změnili hodnotu vlastnosti `background-color`.</span><span class="sxs-lookup"><span data-stu-id="b8288-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="b8288-222">Chcete-li vyvolat výběr barvy, umístěte kurzor za název vlastnosti a typ **#** nebo **RGB (** .</span><span class="sxs-lookup"><span data-stu-id="b8288-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![Panel pro výběr barvy CSS](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="b8288-224">Klikněte na barvu, kterou chcete vybrat, nebo stiskněte klávesu šipka dolů a pak použijte šipky vlevo a vpravo k procházení barev.</span><span class="sxs-lookup"><span data-stu-id="b8288-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="b8288-225">Při návštěvě barvy se zobrazí náhled odpovídající hexadecimální hodnoty:</span><span class="sxs-lookup"><span data-stu-id="b8288-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![Náhled hodnoty vlastnosti background-color](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="b8288-227">Pokud pruh barev nemá přesnou barvu, kterou chcete použít, můžete použít rozevírací nabídka pro výběr barvy.</span><span class="sxs-lookup"><span data-stu-id="b8288-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="b8288-228">Chcete-li jej otevřít, klikněte na dvojitou dvojitou šipku na pravém konci pruhu barev nebo na klávesnici stiskněte šipku dolů nebo dvakrát.</span><span class="sxs-lookup"><span data-stu-id="b8288-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![Místní nabídka pro výběr barvy CSS](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="b8288-230">Klikněte na barvu ze svislého pruhu na pravé straně.</span><span class="sxs-lookup"><span data-stu-id="b8288-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="b8288-231">Tím se v hlavním okně zobrazí barevný přechod pro tuto barvu.</span><span class="sxs-lookup"><span data-stu-id="b8288-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="b8288-232">Vyberte barvu přímo ze svislého pruhu stisknutím klávesy ENTER nebo kliknutím na libovolný bod v hlavním okně vyberte s větší přesností.</span><span class="sxs-lookup"><span data-stu-id="b8288-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="b8288-233">Pokud je na obrazovce počítače barva, kterou chcete použít (nemusí být uvnitř uživatelského rozhraní sady Visual Studio), můžete zachytit její hodnotu pomocí nástroje kapátka v pravém dolním rohu.</span><span class="sxs-lookup"><span data-stu-id="b8288-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="b8288-234">Můžete také změnit neprůhlednost barvy přesunutím posuvníku v dolní části výběru barvy.</span><span class="sxs-lookup"><span data-stu-id="b8288-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="b8288-235">Tím se změní hodnoty barev na hodnoty RGBA, protože formát RGBA může představovat neprůhlednost.</span><span class="sxs-lookup"><span data-stu-id="b8288-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="b8288-236">Po zvolení barvy stiskněte klávesu ENTER a zadáním středníku dokončete položku pozadí-Color v souboru *site. CSS* .</span><span class="sxs-lookup"><span data-stu-id="b8288-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="b8288-237">Panel aktualizace inspektoru stránky</span><span class="sxs-lookup"><span data-stu-id="b8288-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="b8288-238">Inspektor stránky hned detekuje změnu v souboru *Web. CSS* a zobrazí výstrahu na panelu aktualizace.</span><span class="sxs-lookup"><span data-stu-id="b8288-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![Aktualizovat panel](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="b8288-240">Chcete-li uložit všechny soubory a aktualizovat prohlížeč kontroly stránky, stiskněte klávesy CTRL + ALT + ENTER nebo klikněte na panel aktualizace.</span><span class="sxs-lookup"><span data-stu-id="b8288-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="b8288-241">Změna barvy zvýraznění se zobrazí v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="b8288-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="b8288-242">Mapování dynamických prvků stránky na JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8288-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="b8288-243">V moderních webových aplikacích se prvky na stránce často generují dynamicky pomocí JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="b8288-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="b8288-244">To znamená, že není k dispozici žádný statický kód (HTML nebo Razor), který by odpovídal těmto prvkům stránky.</span><span class="sxs-lookup"><span data-stu-id="b8288-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="b8288-245">S verzí 1,3 teď může inspektor stránky namapovat položky, které se dynamicky přidaly na stránku, zpátky do odpovídajícího kódu JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="b8288-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="b8288-246">K předvedení této funkce použijeme [šablonu jednostránkové aplikace (Spa)](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="b8288-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b8288-247">Šablona zabezpečeného hesla vyžaduje aktualizaci [ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650) .</span><span class="sxs-lookup"><span data-stu-id="b8288-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="b8288-248">V aplikaci Visual Studio vyberte **soubor** &gt; **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="b8288-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="b8288-249">Na levé straně rozbalte **C#vizuál**, vyberte **Web**a pak vyberte **Webová aplikace ASP.NET MVC4**.</span><span class="sxs-lookup"><span data-stu-id="b8288-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="b8288-250">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8288-250">Click **OK**.</span></span>

<span data-ttu-id="b8288-251">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte **aplikace s jednou stránkou**.</span><span class="sxs-lookup"><span data-stu-id="b8288-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="b8288-252">V Průzkumník řešení rozbalte složku **zobrazení** a pak do **domovské** složky.</span><span class="sxs-lookup"><span data-stu-id="b8288-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="b8288-253">Klikněte pravým tlačítkem na soubor index. cshtml a **v okně Kontrola stránky vyberte Zobrazit**.</span><span class="sxs-lookup"><span data-stu-id="b8288-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="b8288-254">První věc zobrazená v prohlížeči Inspector stránky je přihlašovací stránka.</span><span class="sxs-lookup"><span data-stu-id="b8288-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="b8288-255">Klikněte na zaregistrovat se a vytvořte uživatelské jméno a heslo.</span><span class="sxs-lookup"><span data-stu-id="b8288-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="b8288-256">Po registraci se aplikace přihlásí a vytvoří seznam úkolů s některými ukázkovými položkami.</span><span class="sxs-lookup"><span data-stu-id="b8288-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="b8288-257">Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.</span><span class="sxs-lookup"><span data-stu-id="b8288-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="b8288-258">V prohlížeči Inspector stránky klikněte na jednu z položek úkolů.</span><span class="sxs-lookup"><span data-stu-id="b8288-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="b8288-259">Všimněte si, že místo aby bylo zvýrazněno modře, je prvek zvýrazněný žlutě a "JS" vedle názvu elementu.</span><span class="sxs-lookup"><span data-stu-id="b8288-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="b8288-260">To znamená, že prvek byl vytvořen dynamicky prostřednictvím skriptu.</span><span class="sxs-lookup"><span data-stu-id="b8288-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="b8288-261">Navíc se na kartě **zásobník volání** zobrazí oranžové podtržení. To značí, že podokno **zásobník volání** obsahuje další informace o elementu.</span><span class="sxs-lookup"><span data-stu-id="b8288-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="b8288-262">Klikněte na kartu **zásobník volání** . V podokně **zásobník volání** se zobrazuje zásobník volání pro volání JavaScriptu, které vytvořilo element.</span><span class="sxs-lookup"><span data-stu-id="b8288-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="b8288-263">Volání externích knihoven, jako je jQuery, jsou sbalena, takže můžete snadno zobrazit volání skriptu aplikace.</span><span class="sxs-lookup"><span data-stu-id="b8288-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="b8288-264">Chcete-li zobrazit úplný zásobník, včetně volání externích knihoven, můžete rozbalit uzly s označením "externí knihovny":</span><span class="sxs-lookup"><span data-stu-id="b8288-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="b8288-265">Pokud kliknete na položku v zásobníku volání, aplikace Visual Studio otevře soubor kódu a zvýrazní odpovídající skript.</span><span class="sxs-lookup"><span data-stu-id="b8288-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="b8288-266">Viz také</span><span class="sxs-lookup"><span data-stu-id="b8288-266">See Also</span></span>

<span data-ttu-id="b8288-267">[Úvod do ASP.NET MVC 4 s Visual Studiem](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.NET Web)</span><span class="sxs-lookup"><span data-stu-id="b8288-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="b8288-268">[Úvod do inspektoru stránky](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (video pro kanál 9)</span><span class="sxs-lookup"><span data-stu-id="b8288-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="b8288-269">[Chybové zprávy v inspektoru stránky](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="b8288-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
