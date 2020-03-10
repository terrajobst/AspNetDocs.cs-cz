---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 'Část 2: řadiče | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 2 pokrývá řadiče.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559876"
---
# <a name="part-2-controllers"></a><span data-ttu-id="0cd6a-104">2\. část: Kontrolery</span><span class="sxs-lookup"><span data-stu-id="0cd6a-104">Part 2: Controllers</span></span>

<span data-ttu-id="0cd6a-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="0cd6a-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0cd6a-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0cd6a-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="0cd6a-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0cd6a-109">Část 2 pokrývá řadiče.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-109">Part 2 covers Controllers.</span></span>

<span data-ttu-id="0cd6a-110">V případě tradičních webových architektur jsou příchozí adresy URL obvykle mapovány na soubory na disku.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="0cd6a-111">Příklad: požadavek na adresu URL, například "/Products.aspx" nebo "/Products.php", může být zpracován souborem "Products. aspx" nebo "Products. php".</span><span class="sxs-lookup"><span data-stu-id="0cd6a-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="0cd6a-112">Webové architektury MVC mapují adresy URL na kód serveru trochu jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="0cd6a-113">Namísto mapování příchozích adres URL na soubory místo toho namapujte adresy URL na metody třídy.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="0cd6a-114">Tyto třídy se nazývají "řadiče" a zodpovídají za zpracování příchozích požadavků HTTP, zpracování vstupu uživatele, načítání a ukládání dat a určení odpovědi, která se pošle zpátky klientovi (zobrazení HTML, stažení souboru, přesměrování na jiný). Adresa URL atd.).</span><span class="sxs-lookup"><span data-stu-id="0cd6a-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="0cd6a-115">Přidání HomeController</span><span class="sxs-lookup"><span data-stu-id="0cd6a-115">Adding a HomeController</span></span>

<span data-ttu-id="0cd6a-116">Budeme začínat aplikaci pro hudební úložiště MVC přidáním třídy Controller, která bude zpracovávat adresy URL na domovské stránce našeho webu.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="0cd6a-117">Budeme dodržovat výchozí konvence pojmenování ASP.NET MVC a volat IT HomeController.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="0cd6a-118">Klikněte pravým tlačítkem na složku Controllers v rámci Průzkumník řešení a vyberte Přidat a pak na Controller... systému</span><span class="sxs-lookup"><span data-stu-id="0cd6a-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="0cd6a-119">Tím se zobrazí dialogové okno Přidat kontroler.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="0cd6a-120">Pojmenujte kontroler "HomeController" a stiskněte tlačítko Přidat.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="0cd6a-121">Tím se vytvoří nový soubor HomeController.cs s následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="0cd6a-122">Chcete-li začít co nejjednodušší, nahraďte metodu indexu jednoduchou metodou, která pouze vrátí řetězec.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="0cd6a-123">Provedeme dvě změny:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-123">We'll make two changes:</span></span>

- <span data-ttu-id="0cd6a-124">Změna metody pro vrácení řetězce místo ActionResult</span><span class="sxs-lookup"><span data-stu-id="0cd6a-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="0cd6a-125">Změnou příkazu return vraťte text Hello z domova.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="0cd6a-126">Metoda by teď měla vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="0cd6a-127">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="0cd6a-127">Running the Application</span></span>

<span data-ttu-id="0cd6a-128">Teď web spusťte.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-128">Now let's run the site.</span></span> <span data-ttu-id="0cd6a-129">Můžeme spustit náš webový server a vyzkoušet web pomocí některého z následujících postupů:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="0cd6a-130">Vyberte položku nabídky ladění ⇨ spustit ladění.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="0cd6a-131">Klikněte na tlačítko se zelenou šipkou na panelu nástrojů ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="0cd6a-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="0cd6a-132">Použijte klávesovou zkratku F5.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="0cd6a-133">Pomocí kteréhokoli z výše uvedených kroků se zkompiluje náš projekt a následně se spustí vývojový server ASP.NET, který je integrován do aplikace Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="0cd6a-134">V dolním rohu obrazovky se zobrazí oznámení o tom, že se spustil vývojový server ASP.NET a zobrazí se číslo portu, pod kterým je spuštěný.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="0cd6a-135">Visual Web Developer pak automaticky otevře okno prohlížeče, jehož adresa URL odkazuje na náš webový server.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="0cd6a-136">Umožní vám to rychle vyzkoušet naši webovou aplikaci:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="0cd6a-137">Dobře, to bylo poměrně rychlé – vytvořili jsme nový web, Přidali jsme tři linky a v prohlížeči máme text.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="0cd6a-138">Nerakety vědy, ale je to na začátku.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="0cd6a-139">*Poznámka: Visual Web Developer zahrnuje vývojový server ASP.NET, který bude web spouštět na náhodném bezplatném čísle "port". Na snímku obrazovky výše je web spuštěný v `http://localhost:26641/`, takže používá port 26641. Vaše číslo portu se bude lišit. Když budeme v tomto kurzu pohovořit o adrese URL jako/Store/Browse, bude jít po čísle portu. Za předpokladu, že se číslo portu 26641, procházení na/Store/Browse znamená procházení na `http://localhost:26641/Store/Browse`.*</span><span class="sxs-lookup"><span data-stu-id="0cd6a-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="0cd6a-140">Přidání StoreController</span><span class="sxs-lookup"><span data-stu-id="0cd6a-140">Adding a StoreController</span></span>

<span data-ttu-id="0cd6a-141">Přidali jsme jednoduchý HomeController, který implementuje domovskou stránku našeho webu.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="0cd6a-142">Teď přidáme další kontroler, který použijeme k implementaci funkce procházení našeho obchodu s hudbou.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="0cd6a-143">Náš kontroler úložiště bude podporovat tři scénáře:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="0cd6a-144">Stránka se seznamem hudebních žánrů v našem hudebním obchodě</span><span class="sxs-lookup"><span data-stu-id="0cd6a-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="0cd6a-145">Stránka pro procházení, na které jsou uvedena všechna hudební alba v konkrétním žánru</span><span class="sxs-lookup"><span data-stu-id="0cd6a-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="0cd6a-146">Stránka s podrobnostmi, která zobrazuje informace o konkrétním hudebním albu</span><span class="sxs-lookup"><span data-stu-id="0cd6a-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="0cd6a-147">Začneme přidáním nové třídy StoreController.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="0cd6a-148">Pokud jste to ještě neudělali, ukončete aplikaci tak, že zavřete prohlížeč nebo vyberete položku nabídky Ladit ⇨ zastavit ladění.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="0cd6a-149">Nyní přidejte nové StoreController.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-149">Now add a new StoreController.</span></span> <span data-ttu-id="0cd6a-150">Stejně jako u HomeController to provedeme tak, že kliknete pravým tlačítkem na složku Controllers v rámci Průzkumník řešení a vyberete položku nabídky přidat řadič&gt;Controller.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="0cd6a-151">Náš nový StoreController už obsahuje metodu "index".</span><span class="sxs-lookup"><span data-stu-id="0cd6a-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="0cd6a-152">Pomocí této metody "index" implementujeme naši stránku se seznamem, kde jsou uvedeny všechny žánry v našem obchodě s hudbou.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="0cd6a-153">Přidáme také dvě další metody, které implementují dva další scénáře, které chceme StoreController zpracovat: Procházet a podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="0cd6a-154">Tyto metody (index, procházení a podrobnosti) v rámci našeho kontroleru se nazývají "akce kontroleru" a protože jste už viděli metodu akce HomeController. index (), jejich úkolem je reagovat na požadavky na adresu URL a (obecně řečeno) zjistit, který obsah má se poslat zpátky v prohlížeči nebo uživateli, který adresu URL vyvolal.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="0cd6a-155">Spustíme naši implementaci StoreController změnou metody theIndex () pro vrácení řetězce "Hello z Store. index ()" a my přidáme podobné metody pro Browse () a Details ():</span><span class="sxs-lookup"><span data-stu-id="0cd6a-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="0cd6a-156">Spusťte projekt znovu a procházejte následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="0cd6a-157">/Store</span><span class="sxs-lookup"><span data-stu-id="0cd6a-157">/Store</span></span>
- <span data-ttu-id="0cd6a-158">/Store/Browse</span><span class="sxs-lookup"><span data-stu-id="0cd6a-158">/Store/Browse</span></span>
- <span data-ttu-id="0cd6a-159">/Store/Details</span><span class="sxs-lookup"><span data-stu-id="0cd6a-159">/Store/Details</span></span>

<span data-ttu-id="0cd6a-160">Přístup k těmto adresám URL vyvolá metody akcí v rámci našeho kontroleru a návratové odezvy řetězce:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="0cd6a-161">To je skvělé, ale jedná se o pouze konstantní řetězce.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="0cd6a-162">Pojďme je udělat dynamicky, aby z adresy URL převzali informace a zobrazili je ve výstupu stránky.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="0cd6a-163">Nejdříve změníme metodu akce procházení, aby se z adresy URL načetla hodnota QueryString.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="0cd6a-164">To můžeme udělat přidáním parametru "Žánr" do naší metody akce.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="0cd6a-165">Když to provedeme, ASP.NET MVC při vyvolání automaticky předáte všechny parametry dotazu nebo formuláře odeslání s názvem "Žánr".</span><span class="sxs-lookup"><span data-stu-id="0cd6a-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="0cd6a-166">*Poznámka: pro úpravu vstupu uživatele používáme metodu Utility HttpUtility. HtmlEncode. To brání uživatelům v vkládání JavaScriptu do našeho zobrazení s odkazem jako/Store/Browse? Žánr =&lt;okno skriptu&gt;Window. Location = 'http://hackersite.com'&lt;/Script&gt;.*</span><span class="sxs-lookup"><span data-stu-id="0cd6a-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="0cd6a-167">Teď procházíme na/Store/Browse? Žánr = disco</span><span class="sxs-lookup"><span data-stu-id="0cd6a-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="0cd6a-168">Pojďme dále změnit akci podrobností pro čtení a zobrazení vstupního parametru s názvem ID.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="0cd6a-169">Na rozdíl od předchozí metody nevložíme hodnotu ID jako parametr QueryString.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="0cd6a-170">Místo toho ho vložíme přímo do samotné adresy URL.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="0cd6a-171">Příklad:/Store/Details/5.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="0cd6a-172">ASP.NET MVC nám umožňuje snadno to dělat bez nutnosti konfigurovat cokoli.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="0cd6a-173">Výchozí konvence směrování ASP.NET MVC je zacházet s segmentem adresy URL za názvem metody akce jako s parametrem s názvem "ID".</span><span class="sxs-lookup"><span data-stu-id="0cd6a-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="0cd6a-174">Pokud vaše metoda Action má parametr s názvem ID, pak ASP.NET MVC automaticky předává segment adresy URL jako parametr.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="0cd6a-175">Spusťte aplikaci a přejděte do/Store/Details/5:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="0cd6a-176">Pojďme si rekapitulace, co jsme doposud provedli:</span><span class="sxs-lookup"><span data-stu-id="0cd6a-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="0cd6a-177">V aplikaci Visual Web Developer jsme vytvořili nový projekt ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="0cd6a-178">Probrali jsme základní strukturu složek aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="0cd6a-179">Zjistili jsme, jak náš web spustit pomocí vývojového serveru ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0cd6a-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="0cd6a-180">Vytvořili jsme dvě třídy kontroleru: HomeController a StoreController.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="0cd6a-181">Do našich řadičů jsme přidali metody akcí, které reagují na žádosti URL a vracejí text do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="0cd6a-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0cd6a-182">[Předchozí](mvc-music-store-part-1.md)
> [Další](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="0cd6a-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
