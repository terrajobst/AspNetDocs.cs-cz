---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3\. část: zobrazení a ViewModels | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 3 pokrývá zobrazení a ViewModels.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559806"
---
# <a name="part-3-views-and-viewmodels"></a><span data-ttu-id="03aa3-104">3\. část: Zobrazení a modely ViewModel</span><span class="sxs-lookup"><span data-stu-id="03aa3-104">Part 3: Views and ViewModels</span></span>

<span data-ttu-id="03aa3-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="03aa3-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="03aa3-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="03aa3-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="03aa3-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="03aa3-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="03aa3-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="03aa3-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="03aa3-109">Část 3 pokrývá zobrazení a ViewModels.</span><span class="sxs-lookup"><span data-stu-id="03aa3-109">Part 3 covers Views and ViewModels.</span></span>

<span data-ttu-id="03aa3-110">Zatím jsme právě vraceli řetězce z akcí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="03aa3-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="03aa3-111">To je dobrý způsob, jak získat představu o tom, jak ovladače fungují, ale není to, jak byste chtěli sestavit skutečnou webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="03aa3-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="03aa3-112">Budeme chtít lepší způsob, jak vygenerovat kód HTML zpátky do prohlížečů, které navštíví náš web – One, kde můžeme použít soubory šablon k jednoduššímu přizpůsobení odeslání obsahu HTML.</span><span class="sxs-lookup"><span data-stu-id="03aa3-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="03aa3-113">To je přesně to, co dělají zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="03aa3-114">Přidání šablony zobrazení</span><span class="sxs-lookup"><span data-stu-id="03aa3-114">Adding a View template</span></span>

<span data-ttu-id="03aa3-115">Chcete-li použít šablonu zobrazení, změníme metodu indexu HomeController tak, aby vracela ActionResult a vrátila zobrazení (), jako je například:</span><span class="sxs-lookup"><span data-stu-id="03aa3-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="03aa3-116">Výše uvedená změna znamená, že místo vrácení řetězce je třeba použít zobrazení k vygenerování výsledku zpět.</span><span class="sxs-lookup"><span data-stu-id="03aa3-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="03aa3-117">Nyní do našeho projektu přidáme příslušnou šablonu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="03aa3-118">K tomu umístíme textový kurzor v rámci metody akce indexu, potom klikněte pravým tlačítkem a vyberte Přidat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="03aa3-119">Tím zobrazíte dialogové okno Přidat zobrazení:</span><span class="sxs-lookup"><span data-stu-id="03aa3-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="03aa3-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="03aa3-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="03aa3-121">Dialog Přidat zobrazení umožňuje rychle a snadno generovat soubory šablon zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="03aa3-122">Dialog Přidat zobrazení se ve výchozím nastavení předem vyplní názvem šablony zobrazení, která se má vytvořit, aby odpovídala metodě akce, která ji bude používat.</span><span class="sxs-lookup"><span data-stu-id="03aa3-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="03aa3-123">Vzhledem k tomu, že jsme použili kontextovou nabídku přidat zobrazení v rámci metody akce index () našeho HomeController, zobrazí se v dialogovém okně Přidat zobrazení "index", protože ve výchozím nastavení se předběžně vyplní název zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="03aa3-124">Nepotřebujeme změnit žádnou z možností v tomto dialogu, takže klikněte na tlačítko Přidat.</span><span class="sxs-lookup"><span data-stu-id="03aa3-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="03aa3-125">Po kliknutí na tlačítko Přidat vytvoří Visual Web Developer novou index. cshtml šablona zobrazení pro nás v adresáři \Views\Home a vytvoří složku, pokud ještě neexistuje.</span><span class="sxs-lookup"><span data-stu-id="03aa3-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="03aa3-126">Název a umístění složky souboru index. cshtml jsou důležité a následují výchozí zásady vytváření názvů pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="03aa3-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="03aa3-127">Název adresáře \Views\Home odpovídá kontroleru, který má název HomeController.</span><span class="sxs-lookup"><span data-stu-id="03aa3-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="03aa3-128">Název šablony zobrazení, index, odpovídá metodě akce kontroleru, které zobrazení zobrazí.</span><span class="sxs-lookup"><span data-stu-id="03aa3-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="03aa3-129">ASP.NET MVC nám umožňuje vyhnout se nutnosti explicitně zadat název nebo umístění šablony zobrazení, když používáme toto zásady vytváření názvů k vrácení zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="03aa3-130">Ve výchozím nastavení bude při psaní kódu, jako je například v rámci našeho HomeController, vykreslena šablona zobrazení \Views\Home\Index.cshtml:</span><span class="sxs-lookup"><span data-stu-id="03aa3-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="03aa3-131">Visual Web Developer vytvořil a otevřel šablonu zobrazení index. cshtml po kliknutí na tlačítko Přidat v dialogovém okně Přidat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="03aa3-132">Obsah indexu. cshtml je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="03aa3-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="03aa3-133">Toto zobrazení používá syntaxe Razor, což je stručnější než modul zobrazení webových formulářů používaný ve webových formulářích ASP.NET a předchozích verzích ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="03aa3-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="03aa3-134">Modul zobrazení webových formulářů je stále k dispozici v ASP.NET MVC 3, ale mnoho vývojářů zjistí, že zobrazovací modul Razor přesně odpovídá vývoji ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="03aa3-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="03aa3-135">První tři řádky nastaví nadpis stránky pomocí ViewBag. title.</span><span class="sxs-lookup"><span data-stu-id="03aa3-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="03aa3-136">Podíváme se, jak tento postup ještě brzy funguje, ale nejdřív aktualizujte text záhlaví textu a zobrazí se stránka.</span><span class="sxs-lookup"><span data-stu-id="03aa3-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="03aa3-137">Aktualizujte &lt;H2&gt; tag, který říká "Toto je Domovská stránka", jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="03aa3-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="03aa3-138">Spuštění aplikace ukazuje, že náš nový text je viditelný na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="03aa3-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="03aa3-139">Použití rozložení pro běžné prvky webu</span><span class="sxs-lookup"><span data-stu-id="03aa3-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="03aa3-140">Většina webů má obsah, který je sdílen mezi mnoha stránkami: navigace, zápatí, obrázky s logem, odkazy na šablony stylů atd. Modul zobrazení Razor usnadňuje správu pomocí stránky s názvem \_layout. cshtml, která se pro nás vytvořila automaticky ve složce/Views/Shared.</span><span class="sxs-lookup"><span data-stu-id="03aa3-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="03aa3-141">Dvojím kliknutím na tuto složku zobrazíte obsah, který vidíte níže.</span><span class="sxs-lookup"><span data-stu-id="03aa3-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="03aa3-142">Obsah z našich individuálních zobrazení se zobrazí příkazem @RenderBody() a veškerý společný obsah, který chceme zobrazit mimo rozhraní, lze přidat do \_layout. cshtml Markup.</span><span class="sxs-lookup"><span data-stu-id="03aa3-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="03aa3-143">Chceme, aby vaše hudební úložiště MVC mělo společné záhlaví s odkazy na naši domovskou stránku a oblast úložiště na všech stránkách v lokalitě, takže přidáme tuto šablonu přímo nad tento příkaz @RenderBody().</span><span class="sxs-lookup"><span data-stu-id="03aa3-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="03aa3-144">Aktualizace šablony stylů</span><span class="sxs-lookup"><span data-stu-id="03aa3-144">Updating the StyleSheet</span></span>

<span data-ttu-id="03aa3-145">Prázdná šablona projektu obsahuje velmi zjednodušený soubor CSS, který obsahuje pouze styly používané k zobrazení ověřovacích zpráv.</span><span class="sxs-lookup"><span data-stu-id="03aa3-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="03aa3-146">Náš Návrhář nabízí několik dalších šablon stylů CSS a obrázků, které definují vzhled a chování pro náš web, takže je teď přidáme.</span><span class="sxs-lookup"><span data-stu-id="03aa3-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="03aa3-147">Aktualizovaný soubor a obrázky CSS jsou obsaženy v adresáři obsahu souboru MvcMusicStore-Assets. zip, který je k dispozici na stránce [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="03aa3-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="03aa3-148">Oba z nich vybereme v Průzkumníkovi Windows a vyřadíte je do složky obsahu našeho řešení ve Visual Web Developer, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="03aa3-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="03aa3-149">Zobrazí se výzva k potvrzení, jestli chcete přepsat existující soubor Web. CSS.</span><span class="sxs-lookup"><span data-stu-id="03aa3-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="03aa3-150">Klikněte na tlačítkoAno.</span><span class="sxs-lookup"><span data-stu-id="03aa3-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="03aa3-151">Složka obsah vaší aplikace se teď zobrazí takto:</span><span class="sxs-lookup"><span data-stu-id="03aa3-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="03aa3-152">Nyní spusťte aplikaci a sledujte, jak se naše změny hledají na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="03aa3-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="03aa3-153">Pojďme se podívat na to, co se změnilo: metoda akce indexu HomeController se našla a zobrazila se šablona \Views\Home\Index.cshtmlView, i když náš kód se nazývá "návratové zobrazení ()", protože naše šablona zobrazení následovala standardní konvence vytváření názvů.</span><span class="sxs-lookup"><span data-stu-id="03aa3-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="03aa3-154">Na domovské stránce se zobrazuje jednoduchá uvítací zpráva, která je definována v rámci šablony zobrazení \Views\Home\Index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="03aa3-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="03aa3-155">Domovská stránka používá naši šablonu \_layout. cshtml, takže úvodní zpráva je obsažena v rozložení HTML webu Standard.</span><span class="sxs-lookup"><span data-stu-id="03aa3-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="03aa3-156">Předání informací do našeho zobrazení pomocí modelu</span><span class="sxs-lookup"><span data-stu-id="03aa3-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="03aa3-157">Šablona zobrazení, která jenom zobrazuje pevně zakódované HTML, nebude vytvářet velice zajímavé webové stránky.</span><span class="sxs-lookup"><span data-stu-id="03aa3-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="03aa3-158">Abychom mohli vytvořit dynamický web, místo toho budeme chtít předat informace z našich akcí kontroleru do našich šablon zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="03aa3-159">Ve vzoru kontroleru zobrazení modelu se pojem model vztahuje na objekty, které představují data v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="03aa3-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="03aa3-160">Objekty modelu se často shodují s tabulkami v databázi, ale nemusí být.</span><span class="sxs-lookup"><span data-stu-id="03aa3-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="03aa3-161">Metody akcí kontroleru, které vracejí ActionResult, mohou předat objekt modelu do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="03aa3-162">Díky tomu může kontroler vyčistit všechny informace potřebné k vygenerování odpovědi a pak tyto informace předat do šablony zobrazení, která se použije k vygenerování příslušné odpovědi HTML.</span><span class="sxs-lookup"><span data-stu-id="03aa3-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="03aa3-163">To je nejjednodušší pochopit tím, že se zobrazí v akci, takže se můžeme začít.</span><span class="sxs-lookup"><span data-stu-id="03aa3-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="03aa3-164">Nejprve vytvoříme některé třídy modelu, které reprezentují žánry a alba v rámci našeho obchodu.</span><span class="sxs-lookup"><span data-stu-id="03aa3-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="03aa3-165">Pojďme začít vytvořením třídy žánru.</span><span class="sxs-lookup"><span data-stu-id="03aa3-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="03aa3-166">Klikněte pravým tlačítkem na složku modely v rámci projektu, vyberte možnost "Přidat třídu" a pojmenujte soubor "Genre.cs".</span><span class="sxs-lookup"><span data-stu-id="03aa3-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="03aa3-167">Pak přidejte vlastnost názvu veřejné řetězce do třídy, která byla vytvořena:</span><span class="sxs-lookup"><span data-stu-id="03aa3-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="03aa3-168">*Poznámka: v případě, že se zajímá, znamená C#to, že zápis {get; set;} používá automaticky implementované funkce vlastností. Díky tomu máme výhody vlastnosti bez nutnosti deklarovat pole pro zálohování.*</span><span class="sxs-lookup"><span data-stu-id="03aa3-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="03aa3-169">Potom postupujte podle stejných kroků a vytvořte třídu alba (s názvem Album.cs), která má název a vlastnost Žánr:</span><span class="sxs-lookup"><span data-stu-id="03aa3-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="03aa3-170">Nyní můžeme upravit StoreController pro použití zobrazení, která zobrazují dynamické informace z našeho modelu.</span><span class="sxs-lookup"><span data-stu-id="03aa3-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="03aa3-171">If – pro demonstrační účely: máme moje alba na základě ID žádosti. Tyto informace můžeme zobrazit jako v následujícím zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="03aa3-172">Začneme tak, že změníte akci úložiště Details, aby se zobrazily informace o jednom albu.</span><span class="sxs-lookup"><span data-stu-id="03aa3-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="03aa3-173">Přidejte do horní části třídy **StoreControllers** příkaz "using", který bude zahrnovat obor názvů MvcMusicStore. Models, takže nemusíme psát MvcMusicStore. Models. album pokaždé, když chceme použít třídu alba.</span><span class="sxs-lookup"><span data-stu-id="03aa3-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="03aa3-174">Oddíl "using" této třídy by se teď měl zobrazit jako níže.</span><span class="sxs-lookup"><span data-stu-id="03aa3-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="03aa3-175">V dalším kroku aktualizujeme akci kontroleru podrobností tak, aby vracela ActionResult místo řetězce, stejně jako u metody indexu HomeController.</span><span class="sxs-lookup"><span data-stu-id="03aa3-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="03aa3-176">Nyní můžeme upravit logiku, aby vracela objekt alba do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="03aa3-177">Později v tomto kurzu načteme data z databáze, ale hned teď k zahájení práce použijeme "fiktivní data".</span><span class="sxs-lookup"><span data-stu-id="03aa3-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="03aa3-178">*Poznámka: Pokud si nejste obeznámeni C#s, můžete předpokládat, že použití var znamená, že je naše proměnná alba pozdní vazbá. To není správné – C# kompilátor používá odvození typu na základě toho, co přiřadíme proměnné k určení toho, že album je typu album a kompilování lokální proměnné alba jako typ alba, takže získáme kontrolu v době kompilace a podporu editoru kódu Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="03aa3-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="03aa3-179">Teď vytvoříme šablonu zobrazení, která pomocí našeho alba vygeneruje odpověď HTML.</span><span class="sxs-lookup"><span data-stu-id="03aa3-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="03aa3-180">Než budeme udělat, musíme sestavit projekt, aby dialog Přidat zobrazení věděl o naší nově vytvořené třídě alba.</span><span class="sxs-lookup"><span data-stu-id="03aa3-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="03aa3-181">Projekt můžete sestavit tak, že vyberete položku nabídky Ladit ⇨ Build MvcMusicStore (pro další kredity, můžete k sestavení projektu použít zástupce CTRL + SHIFT-B).</span><span class="sxs-lookup"><span data-stu-id="03aa3-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="03aa3-182">Teď, když jsme si nastavili naše podpůrné třídy, jsme připraveni sestavit naši šablonu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="03aa3-183">Klikněte pravým tlačítkem v rámci metody Details a vyberte Přidat zobrazení... z místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="03aa3-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="03aa3-184">Vytvoříme novou šablonu zobrazení, jako jsme předtím pracovali s HomeController.</span><span class="sxs-lookup"><span data-stu-id="03aa3-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="03aa3-185">Protože ho vytváříme z StoreController, ve výchozím nastavení se vygeneruje v souboru \Views\Store\Index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="03aa3-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="03aa3-186">Na rozdíl od dřív, vrátíme zaškrtávací políčko vytvořit zobrazení se silným typem.</span><span class="sxs-lookup"><span data-stu-id="03aa3-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="03aa3-187">Potom v rámci příkazu "View data-Class" downlist vybereme naši třídu "album".</span><span class="sxs-lookup"><span data-stu-id="03aa3-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="03aa3-188">Tím se zobrazí dialogové okno Přidat zobrazení, ve kterém můžete vytvořit šablonu zobrazení, která očekává, že se objekt alba předává k použití.</span><span class="sxs-lookup"><span data-stu-id="03aa3-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="03aa3-189">Po kliknutí na tlačítko Přidat se vytvoří šablona zobrazení \Views\Store\Details.cshtml, která obsahuje následující kód.</span><span class="sxs-lookup"><span data-stu-id="03aa3-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="03aa3-190">Všimněte si prvního řádku, který označuje, že toto zobrazení je silně typované pro naši třídu alba.</span><span class="sxs-lookup"><span data-stu-id="03aa3-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="03aa3-191">Modul zobrazení Razor chápe, že byl předán objekt alba, takže můžeme snadno získat přístup k vlastnostem modelu a dokonce i využít výhod technologie IntelliSense v editoru aplikace Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="03aa3-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="03aa3-192">Aktualizujte &lt;H2&gt; tag, aby se zobrazila vlastnost title alba úpravou této čáry, která se zobrazí takto.</span><span class="sxs-lookup"><span data-stu-id="03aa3-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="03aa3-193">Všimněte si, že technologie IntelliSense je aktivována při zadání tečky po klíčovém slově @Model a zobrazení vlastností a metod, které třída alba podporuje.</span><span class="sxs-lookup"><span data-stu-id="03aa3-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="03aa3-194">Pojďme teď náš projekt znovu spustit a přejít na adresu URL/Store/Details/5.</span><span class="sxs-lookup"><span data-stu-id="03aa3-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="03aa3-195">Zobrazí se podrobnosti o albu, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="03aa3-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="03aa3-196">Teď povedeme k podobným aktualizacím pro metodu akce procházení pro Store.</span><span class="sxs-lookup"><span data-stu-id="03aa3-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="03aa3-197">Aktualizujte metodu tak, aby vrátila ActionResult, a upravte logiku metody tak, aby vytvořila nový objekt žánru a vrátil ho do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03aa3-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="03aa3-198">Klikněte pravým tlačítkem myši do metody Browse a vyberte Přidat zobrazení... v kontextové nabídce přidejte zobrazení, které je silného typu, a přidejte silný typ ke třídě Žánr.</span><span class="sxs-lookup"><span data-stu-id="03aa3-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="03aa3-199">Aktualizujte &lt;H2&gt; elementu v kódu zobrazení (v/Views/Store/Browse.cshtml), aby se zobrazily informace o žánru.</span><span class="sxs-lookup"><span data-stu-id="03aa3-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="03aa3-200">Teď náš projekt znovu spusťte a přejděte k/Store/Browse? Žánr = adresa URL disdisce.</span><span class="sxs-lookup"><span data-stu-id="03aa3-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="03aa3-201">Zobrazí se stránka pro procházení, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="03aa3-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="03aa3-202">Nakonec provedeme trochu složitější aktualizace metody a zobrazení akce **indexu úložiště** , abyste zobrazili seznam všech žánrů v našem obchodě.</span><span class="sxs-lookup"><span data-stu-id="03aa3-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="03aa3-203">Provedeme to pomocí seznamu žánrů jako našeho objektu modelu, nikoli jenom jediného žánru.</span><span class="sxs-lookup"><span data-stu-id="03aa3-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="03aa3-204">Klikněte pravým tlačítkem myši na metodu akce indexu úložiště a vyberte možnost přidat zobrazení jako dříve, jako třídu modelu vyberte Žánr a stiskněte tlačítko Přidat.</span><span class="sxs-lookup"><span data-stu-id="03aa3-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="03aa3-205">Nejdříve změníme deklaraci @model tak, aby označovala, že zobrazení očekává několik objektů žánrů, nikoli jenom jeden.</span><span class="sxs-lookup"><span data-stu-id="03aa3-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="03aa3-206">Změňte první řádek/Store/Index.cshtml ke čtení následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="03aa3-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="03aa3-207">To oznamuje modulu zobrazení Razor, že bude fungovat s objektem modelu, který může obsahovat několik žánrů objektů.</span><span class="sxs-lookup"><span data-stu-id="03aa3-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="03aa3-208">Používáme&lt;žánru IEnumerable&gt; spíše než seznam&lt;Žánr&gt;, protože je obecnější, což nám umožňuje změnit typ modelu později na libovolný typ objektu, který podporuje rozhraní IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="03aa3-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="03aa3-209">V dalším kroku procházíme objekty žánru v modelu, jak je uvedeno v následujícím kódu zobrazení dokončeno.</span><span class="sxs-lookup"><span data-stu-id="03aa3-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="03aa3-210">Všimněte si, že máme plnou podporu technologie IntelliSense, když tento kód zadáte, takže když zadáte "@Model."</span><span class="sxs-lookup"><span data-stu-id="03aa3-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="03aa3-211">Uvidíme všechny metody a vlastnosti podporované rozhraním IEnumerable typu Žánr.</span><span class="sxs-lookup"><span data-stu-id="03aa3-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="03aa3-212">V rámci naší smyčky "foreach" si Visual Web Developer ví, že každá položka je typu Žánr, takže jsme viděli IntelliSense pro každý typ žánru.</span><span class="sxs-lookup"><span data-stu-id="03aa3-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="03aa3-213">Dále funkce generování uživatelského rozhraní zkontrolovala objekt žánru a určila, že každá z nich bude mít vlastnost Name, takže projde a zapíše je. Také generuje odkazy pro úpravy, podrobnosti a odstranění na každou jednotlivou položku.</span><span class="sxs-lookup"><span data-stu-id="03aa3-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="03aa3-214">Budeme s tím využívat i v našich manažerech Storu, ale teď rádi máme místo toho jednoduchý seznam.</span><span class="sxs-lookup"><span data-stu-id="03aa3-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="03aa3-215">Když aplikaci spustíme a přejdeme na/Store, uvidíme, že se zobrazuje počet i seznam žánrů.</span><span class="sxs-lookup"><span data-stu-id="03aa3-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="03aa3-216">Přidávání odkazů mezi stránkami</span><span class="sxs-lookup"><span data-stu-id="03aa3-216">Adding Links between pages</span></span>

<span data-ttu-id="03aa3-217">Naše adresa URL/Store, ve které jsou uvedené žánry, jsou v současné době uvedeny názvy žánrů jednoduše jako prostý text.</span><span class="sxs-lookup"><span data-stu-id="03aa3-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="03aa3-218">Pojďme to změnit, takže místo prostého textu máme názvy žánrů odkaz na příslušnou adresu URL/Store/Browse, takže když kliknete na hudební žánr, jako je "disco", přejdete na adresu URL/Store/Browse? Žánr = disco.</span><span class="sxs-lookup"><span data-stu-id="03aa3-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="03aa3-219">Naši šablonu zobrazení \Views\Store\Index.cshtml bychom mohli aktualizovat tak, aby vyhledala tyto odkazy pomocí následujícího **kódu:**</span><span class="sxs-lookup"><span data-stu-id="03aa3-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="03aa3-220">To funguje, ale může vést k problémům později, protože spoléhá na pevně zakódované řetězec.</span><span class="sxs-lookup"><span data-stu-id="03aa3-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="03aa3-221">Například pokud jsme chtěli řadič přejmenovat, musíme vyhledat odkazy, které je potřeba aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="03aa3-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="03aa3-222">Alternativním přístupem, který můžeme použít, je využít pomocnou metodu HTML.</span><span class="sxs-lookup"><span data-stu-id="03aa3-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="03aa3-223">ASP.NET MVC obsahuje pomocné metody HTML, které jsou k dispozici z našeho kódu šablony zobrazení k provádění celé řady běžných úloh stejně jako to.</span><span class="sxs-lookup"><span data-stu-id="03aa3-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="03aa3-224">Pomocná metoda HTML. ActionLink () je obzvláště užitečná a usnadňuje tak vytváření &lt;HTML a&gt; odkazů a postará se o obtěžující podrobnosti, jako je například zajištění správné kódování adres URL cest.</span><span class="sxs-lookup"><span data-stu-id="03aa3-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="03aa3-225">HTML. ActionLink () má několik různých přetížení, které umožňují zadat co nejvíce informací, kolik potřebujete pro vaše odkazy.</span><span class="sxs-lookup"><span data-stu-id="03aa3-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="03aa3-226">V nejjednodušším případě zadáte pouze text odkazu a metodu Action, na kterou přejdete, když na klienta kliknete na hypertextový odkaz.</span><span class="sxs-lookup"><span data-stu-id="03aa3-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="03aa3-227">Například můžeme na stránce s podrobnostmi úložiště propojit metodu "/Store/" index () s textem odkazu a přejít do indexu úložiště pomocí následujícího volání:</span><span class="sxs-lookup"><span data-stu-id="03aa3-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="03aa3-228">*Poznámka: v tomto případě jsme nemuseli zadat název kontroleru, protože jsme právě provedli odkaz na jinou akci v rámci stejného kontroleru, který vykresluje aktuální zobrazení.*</span><span class="sxs-lookup"><span data-stu-id="03aa3-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="03aa3-229">Naše odkazy na stránku pro procházení budou muset předat parametr, takže použijeme další přetížení metody HTML. ActionLink, která přijímá tři parametry:</span><span class="sxs-lookup"><span data-stu-id="03aa3-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="03aa3-230">Text odkazu, ve kterém se zobrazí název žánru</span><span class="sxs-lookup"><span data-stu-id="03aa3-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="03aa3-231">Název akce kontroleru (Procházet)</span><span class="sxs-lookup"><span data-stu-id="03aa3-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="03aa3-232">Hodnoty parametrů směrování, zadání názvu (žánr) a hodnoty (název žánru)</span><span class="sxs-lookup"><span data-stu-id="03aa3-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="03aa3-233">Pokud to všechno dohromady, napíšeme tyto odkazy na zobrazení indexu úložiště:</span><span class="sxs-lookup"><span data-stu-id="03aa3-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="03aa3-234">Když teď znovu spustíte náš projekt a získáte přístup k adrese URL/Store/, zobrazí se seznam žánrů.</span><span class="sxs-lookup"><span data-stu-id="03aa3-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="03aa3-235">Každý Žánr je hypertextový odkaz – když se na něj klikne, pošle nám na náš/Store/Browse? Žánr = *[Žánr]* adresa URL.</span><span class="sxs-lookup"><span data-stu-id="03aa3-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="03aa3-236">HTML pro seznam žánru vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="03aa3-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> <span data-ttu-id="03aa3-237">[Předchozí](mvc-music-store-part-2.md)
> [Další](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="03aa3-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
