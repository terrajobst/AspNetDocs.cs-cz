---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 'Část 5: úpravy formulářů a šablonování | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 5 pokrývá úpravy formulářů a šablonování.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559547"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="886e4-104">5\. část: Editační formuláře a šablonování textu</span><span class="sxs-lookup"><span data-stu-id="886e4-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="886e4-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="886e4-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="886e4-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="886e4-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="886e4-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="886e4-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="886e4-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="886e4-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="886e4-109">Část 5 pokrývá úpravy formulářů a šablonování.</span><span class="sxs-lookup"><span data-stu-id="886e4-109">Part 5 covers Edit Forms and Templating.</span></span>

<span data-ttu-id="886e4-110">V poslední kapitole jsme načetli data z naší databáze a zobrazili jsme ji.</span><span class="sxs-lookup"><span data-stu-id="886e4-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="886e4-111">V této kapitole také povolíme úpravy dat.</span><span class="sxs-lookup"><span data-stu-id="886e4-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="886e4-112">Vytváření StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="886e4-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="886e4-113">Začneme vytvořením nového kontroleru s názvem **StoreManagerController**.</span><span class="sxs-lookup"><span data-stu-id="886e4-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="886e4-114">Pro tento kontroler využijeme funkce pro generování uživatelského rozhraní, které jsou k dispozici v aktualizaci nástrojů ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="886e4-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="886e4-115">V dialogovém okně Přidat řadič nastavte možnosti, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="886e4-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="886e4-116">Když kliknete na tlačítko Přidat, uvidíte, že mechanismus generování uživatelského rozhraní ASP.NET MVC 3 má pro vás dobrý objem práce:</span><span class="sxs-lookup"><span data-stu-id="886e4-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="886e4-117">Vytvoří nový StoreManagerController s místní proměnnou Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="886e4-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="886e4-118">Přidá složku StoreManager do složky zobrazení projektu.</span><span class="sxs-lookup"><span data-stu-id="886e4-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="886e4-119">Přidá vytvořit. cshtml, DELETE. cshtml, details. cshtml, Edit. cshtml a index. cshtml, silně typované na třídu alba.</span><span class="sxs-lookup"><span data-stu-id="886e4-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="886e4-120">Nová třída kontroleru StoreManager zahrnuje operace CRUD (vytvořit, číst, aktualizovat, odstranit), které znají, jak pracovat s třídou modelu alba a použít náš Entity Framework kontext pro přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="886e4-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="886e4-121">Úprava vygenerovaného zobrazení</span><span class="sxs-lookup"><span data-stu-id="886e4-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="886e4-122">Je důležité si uvědomit, že i když byl tento kód vygenerován pro nás, jedná se o standardní ASP.NET kód MVC, stejně jako v průběhu tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="886e4-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="886e4-123">Je vhodné vám ušetřit čas při psaní často používaného kódu kontroleru a vytváření zobrazení se silnými typy, ale toto není druh generovaného kódu, který jste mohli vidět s nepříjemné upozorněními v komentářích k tomu, jak nesmí změnit. znakovou.</span><span class="sxs-lookup"><span data-stu-id="886e4-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="886e4-124">Toto je váš kód a očekává se, že ho změníte.</span><span class="sxs-lookup"><span data-stu-id="886e4-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="886e4-125">Pojďme tedy začít rychle upravovat v zobrazení indexu StoreManager (/Views/StoreManager/Index.cshtml).</span><span class="sxs-lookup"><span data-stu-id="886e4-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="886e4-126">V tomto zobrazení se zobrazí tabulka, která obsahuje seznam alb v našem úložišti s odkazy upravit/podrobnosti/odstranit a obsahuje veřejné vlastnosti alba.</span><span class="sxs-lookup"><span data-stu-id="886e4-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="886e4-127">Odebereme pole AlbumArtUrl, protože toto zobrazení není velice užitečné.</span><span class="sxs-lookup"><span data-stu-id="886e4-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="886e4-128">V části &lt;tabulky&gt; kódu zobrazení odeberte &lt;&gt; a &lt;&gt; TD, jak ukazují zvýrazněné řádky níže:</span><span class="sxs-lookup"><span data-stu-id="886e4-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="886e4-129">Upravený kód zobrazení se zobrazí takto:</span><span class="sxs-lookup"><span data-stu-id="886e4-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="886e4-130">První pohled na správce úložiště</span><span class="sxs-lookup"><span data-stu-id="886e4-130">A first look at the Store Manager</span></span>

<span data-ttu-id="886e4-131">Nyní spusťte aplikaci a přejděte do/StoreManager/.</span><span class="sxs-lookup"><span data-stu-id="886e4-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="886e4-132">Tím se zobrazí index Správce úložiště, který jsme právě změnili, a zobrazí se seznam alb ve Storu s odkazy na úpravy, podrobnosti a odstranění.</span><span class="sxs-lookup"><span data-stu-id="886e4-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="886e4-133">Kliknutím na odkaz Upravit se zobrazí formulář pro úpravy s poli pro album, včetně rozevíracích seznamů žánru a umělce.</span><span class="sxs-lookup"><span data-stu-id="886e4-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="886e4-134">V dolní části klikněte na odkaz zpět na seznam a pak klikněte na odkaz podrobnosti pro album.</span><span class="sxs-lookup"><span data-stu-id="886e4-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="886e4-135">Zobrazí se podrobné informace o jednotlivých albech.</span><span class="sxs-lookup"><span data-stu-id="886e4-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="886e4-136">Znovu klikněte na odkaz zpět na seznam a pak klikněte na odkaz odstranit.</span><span class="sxs-lookup"><span data-stu-id="886e4-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="886e4-137">Tím se zobrazí potvrzovací dialogové okno s podrobnostmi o albu a s dotazem, jestli jsme si jisti, že ji chceme odstranit.</span><span class="sxs-lookup"><span data-stu-id="886e4-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="886e4-138">Kliknutí na tlačítko Odstranit v dolní části odstraní album a vrátíte se na stránku index, kde se zobrazí odstraněné album.</span><span class="sxs-lookup"><span data-stu-id="886e4-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="886e4-139">Neudělali jsme se správcem úložiště, ale máme pracovní kontroler a kód zobrazení pro zahájení operací CRUD.</span><span class="sxs-lookup"><span data-stu-id="886e4-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="886e4-140">Podívejte se na kód kontroleru Správce úložiště.</span><span class="sxs-lookup"><span data-stu-id="886e4-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="886e4-141">Kontroler Správce úložiště obsahuje dobrý objem kódu.</span><span class="sxs-lookup"><span data-stu-id="886e4-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="886e4-142">Podívejme se na to shora dolů.</span><span class="sxs-lookup"><span data-stu-id="886e4-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="886e4-143">Kontroler zahrnuje některé standardní obory názvů pro kontroler MVC a také odkaz na obor názvů našich modelů.</span><span class="sxs-lookup"><span data-stu-id="886e4-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="886e4-144">Kontroler má soukromou instanci MusicStoreEntities, kterou používají všechny akce kontroleru pro přístup k datům.</span><span class="sxs-lookup"><span data-stu-id="886e4-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="886e4-145">Akce indexu a podrobností Správce úložiště</span><span class="sxs-lookup"><span data-stu-id="886e4-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="886e4-146">Zobrazení index načte seznam alb, včetně informací o žánru a informacích o jednotlivých albech, jak jsme se předtím viděli při práci na metodě procházení Store.</span><span class="sxs-lookup"><span data-stu-id="886e4-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="886e4-147">Zobrazení index je po odkazech na propojené objekty, aby mohl zobrazit název a jméno žánru každého alba, aby byl kontroler efektivní a dotazován na tyto informace v původní žádosti.</span><span class="sxs-lookup"><span data-stu-id="886e4-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="886e4-148">Akce kontroleru řadiče StoreManager funguje úplně stejně jako akce s podrobnostmi řadiče úložiště, které jsme napsali jako předchozí dotaz na album podle ID pomocí metody Find () a pak ji vrátíte do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="886e4-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="886e4-149">Metody akce vytvoření</span><span class="sxs-lookup"><span data-stu-id="886e4-149">The Create Action Methods</span></span>

<span data-ttu-id="886e4-150">Metody akce vytvoření se trochu liší od těch, které jsme doposud viděli, protože zpracovávají vstup z formuláře.</span><span class="sxs-lookup"><span data-stu-id="886e4-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="886e4-151">Když uživatel poprvé navštíví/StoreManager/Create/, zobrazí se prázdná forma.</span><span class="sxs-lookup"><span data-stu-id="886e4-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="886e4-152">Tato stránka HTML bude obsahovat prvek &lt;Form&gt;, který obsahuje ovládací prvky DropDown a TextBox Input, kde mohou zadat podrobnosti o albu.</span><span class="sxs-lookup"><span data-stu-id="886e4-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="886e4-153">Jakmile uživatel vyplní hodnoty ve formuláři alba, může kliknutím na tlačítko Uložit odeslat tyto změny zpět do naší aplikace, aby se uložily v rámci databáze.</span><span class="sxs-lookup"><span data-stu-id="886e4-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="886e4-154">Když uživatel stiskne tlačítko Uložit, &lt;formulář&gt; provede odeslání do adresy URL/StoreManager/Create/a odešle &lt;formuláře&gt; hodnoty jako součást příspěvku HTTP.</span><span class="sxs-lookup"><span data-stu-id="886e4-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="886e4-155">ASP.NET MVC nám umožňuje snadno rozdělit logiku těchto dvou scénářů volání adresy URL tím, že nám umožní implementovat dvě samostatné metody "vytvoření" v rámci naší třídy StoreManagerController – jednu pro zpracování počátečního protokolu HTTP-GET na adresu URL/StoreManager/Create/a druhý pro zpracování HTTP-POST u odeslaných změn.</span><span class="sxs-lookup"><span data-stu-id="886e4-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="886e4-156">Předávání informací do zobrazení pomocí ViewBag</span><span class="sxs-lookup"><span data-stu-id="886e4-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="886e4-157">Používali jsme ViewBag dříve v tomto kurzu, ale nemluviliy se o nich hodně.</span><span class="sxs-lookup"><span data-stu-id="886e4-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="886e4-158">ViewBag nám umožňuje předat informace do zobrazení bez použití objektu modelu silného typu.</span><span class="sxs-lookup"><span data-stu-id="886e4-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="886e4-159">V takovém případě musí akce upravit HTTP-získat Controller předat seznam žánrů a umělců do formuláře k naplnění rozevíracích seznamů a nejjednodušší způsob, jak to udělat, aby byly vráceny jako ViewBag položky.</span><span class="sxs-lookup"><span data-stu-id="886e4-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="886e4-160">ViewBag je dynamický objekt, což znamená, že můžete zadat ViewBag. foo nebo ViewBag. YourNameHere, aniž by bylo nutné psát kód pro definování těchto vlastností.</span><span class="sxs-lookup"><span data-stu-id="886e4-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="886e4-161">V tomto případě kód kontroleru používá ViewBag. GenreId a ViewBag. ArtistId, aby hodnoty rozevíracího seznamu odeslané ve formuláři byly GenreId a ArtistId, což jsou vlastnosti alba, které budou nastaveny.</span><span class="sxs-lookup"><span data-stu-id="886e4-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="886e4-162">Tyto hodnoty rozevíracích seznamů jsou vráceny do formuláře pomocí objektu SelectList, který je sestaven pouze pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="886e4-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="886e4-163">To se provádí pomocí kódu takto:</span><span class="sxs-lookup"><span data-stu-id="886e4-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="886e4-164">Jak vidíte z kódu metody akce, jsou použity tři parametry pro vytvoření tohoto objektu:</span><span class="sxs-lookup"><span data-stu-id="886e4-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="886e4-165">Seznam položek, které budou zobrazeny v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="886e4-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="886e4-166">Všimněte si, že to není pouze řetězec – předáváme seznam žánrů.</span><span class="sxs-lookup"><span data-stu-id="886e4-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="886e4-167">Dalším parametrem, který je předán do SelectList, je vybraná hodnota.</span><span class="sxs-lookup"><span data-stu-id="886e4-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="886e4-168">Tímto způsobem SelectList ví, jak předem vybrat položku v seznamu.</span><span class="sxs-lookup"><span data-stu-id="886e4-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="886e4-169">To bude snazší pochopit, kdy se podíváme na formulář pro úpravy, který je poměrně podobný.</span><span class="sxs-lookup"><span data-stu-id="886e4-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="886e4-170">Konečný parametr je vlastnost, která má být zobrazena.</span><span class="sxs-lookup"><span data-stu-id="886e4-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="886e4-171">V tomto případě to znamená, že vlastnost Genre.Name se zobrazí uživateli.</span><span class="sxs-lookup"><span data-stu-id="886e4-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="886e4-172">V takovém případě je akce HTTP-GET Create poměrně jednoduchá – do ViewBag se přidají dvě SelectLists a do formuláře se nepředává žádný objekt modelu (protože ještě nebyl vytvořen).</span><span class="sxs-lookup"><span data-stu-id="886e4-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="886e4-173">Pomocník HTML pro zobrazení rozevíracích seznamu v zobrazení pro vytváření</span><span class="sxs-lookup"><span data-stu-id="886e4-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="886e4-174">Vzhledem k tomu, že jsme mluvilii, jak jsou hodnoty rozevíracího seznamu předávány zobrazení, se podívejme na zobrazení a podívejte se, jak se tyto hodnoty zobrazují.</span><span class="sxs-lookup"><span data-stu-id="886e4-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="886e4-175">V kódu zobrazení (/Views/StoreManager/Create.cshtml) se zobrazí následující volání pro zobrazení rozevírací nabídky Žánr.</span><span class="sxs-lookup"><span data-stu-id="886e4-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="886e4-176">To se označuje jako pomocník HTML – metoda nástroje, která provádí běžné úkoly zobrazení.</span><span class="sxs-lookup"><span data-stu-id="886e4-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="886e4-177">Pomocníky HTML jsou velmi užitečné při zachování stručného a čitelného kódu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="886e4-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="886e4-178">Pomocná rutina HTML. DropDownList je poskytována ASP.NET MVC, ale jakmile se později ukážeme, že je možné vytvořit vlastní pomůcky pro kód zobrazení, budeme v naší aplikaci znovu používat.</span><span class="sxs-lookup"><span data-stu-id="886e4-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="886e4-179">Volání HTML. DropDownList stačí pouze 2 věci – kde získat seznam k zobrazení a jaká hodnota (pokud existuje) by měla být předem vybraná.</span><span class="sxs-lookup"><span data-stu-id="886e4-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="886e4-180">První parametr, GenreId, instruuje DropDownList, aby hledal hodnotu s názvem GenreId v modelu nebo v ViewBag.</span><span class="sxs-lookup"><span data-stu-id="886e4-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="886e4-181">Druhý parametr se používá k označení hodnoty, která se má zobrazit v rozevíracím seznamu původně vybrané.</span><span class="sxs-lookup"><span data-stu-id="886e4-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="886e4-182">Vzhledem k tomu, že se jedná o formulář pro vytvoření, není k dispozici žádná hodnota, která se má Předvybrat a zadat řetězec. je předána hodnota Empty</span><span class="sxs-lookup"><span data-stu-id="886e4-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="886e4-183">Zpracování hodnot publikovaných formulářů</span><span class="sxs-lookup"><span data-stu-id="886e4-183">Handling the Posted Form values</span></span>

<span data-ttu-id="886e4-184">Jak jsme probrali dřív, ke každému formuláři jsou přidruženy dvě metody akcí.</span><span class="sxs-lookup"><span data-stu-id="886e4-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="886e4-185">První zpracuje požadavek HTTP-GET a zobrazí formulář.</span><span class="sxs-lookup"><span data-stu-id="886e4-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="886e4-186">Druhý zpracovává požadavek HTTP-POST, který obsahuje odeslané hodnoty formuláře.</span><span class="sxs-lookup"><span data-stu-id="886e4-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="886e4-187">Všimněte si, že akce kontroleru má atribut [HttpPost], který oznamuje ASP.NET MVC, že by měl reagovat pouze na požadavky HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="886e4-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="886e4-188">Tato akce má čtyři zodpovědnosti:</span><span class="sxs-lookup"><span data-stu-id="886e4-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="886e4-189">Přečtěte si hodnoty formuláře.</span><span class="sxs-lookup"><span data-stu-id="886e4-189">Read the form values</span></span>
- 2. <span data-ttu-id="886e4-190">Kontrola, zda hodnoty formuláře přecházejí do libovolných ověřovacích pravidel</span><span class="sxs-lookup"><span data-stu-id="886e4-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="886e4-191">Pokud je odeslání formuláře platné, uložte data a zobrazte aktualizovaný seznam.</span><span class="sxs-lookup"><span data-stu-id="886e4-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="886e4-192">Pokud odeslání formuláře není platné, zobrazí se znovu formulář s chybami ověřování.</span><span class="sxs-lookup"><span data-stu-id="886e4-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="886e4-193">Čtení hodnot formuláře s vazbou modelu</span><span class="sxs-lookup"><span data-stu-id="886e4-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="886e4-194">Akce kontroleru zpracovává odeslání formuláře, které zahrnuje hodnoty pro GenreId a ArtistId (z rozevíracího seznamu) a hodnoty TextBox pro title, Price a AlbumArtUrl.</span><span class="sxs-lookup"><span data-stu-id="886e4-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="886e4-195">I když je možné přímo získat přístup k hodnotám formuláře, lepším řešením je použití možností vazby modelu integrovaných do ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="886e4-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="886e4-196">Když akce kontroleru převezme typ modelu jako parametr, ASP.NET MVC se pokusí naplnit objekt daného typu pomocí vstupů formuláře (stejně jako hodnoty Route a QueryString).</span><span class="sxs-lookup"><span data-stu-id="886e4-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="886e4-197">To dělá tak, že vyhledá hodnoty, jejichž názvy odpovídají vlastnostem objektu modelu, například při nastavení hodnoty GenreId nového objektu alba, vyhledá vstup s názvem GenreId.</span><span class="sxs-lookup"><span data-stu-id="886e4-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="886e4-198">Při vytváření zobrazení pomocí standardních metod v ASP.NET MVC budou formuláře vždy vykresleny pomocí názvů vlastností jako názvy vstupních polí, takže názvy polí budou přesně odpovídat.</span><span class="sxs-lookup"><span data-stu-id="886e4-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="886e4-199">Ověřování modelu</span><span class="sxs-lookup"><span data-stu-id="886e4-199">Validating the Model</span></span>

<span data-ttu-id="886e4-200">Model je ověřen pomocí jednoduchého volání ModelState. IsValid.</span><span class="sxs-lookup"><span data-stu-id="886e4-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="886e4-201">Zatím jsme nepřidali žádná ověřovací pravidla do naší třídy alba. provedeme to tak, že v tuto chvíli Tato kontrola nebude mnohem dělat.</span><span class="sxs-lookup"><span data-stu-id="886e4-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="886e4-202">Důležité je, aby se tato kontrola ModelStat. IsValid přizpůsobila ověřovacím pravidlům, která jsme umístili do našeho modelu, takže budoucí změny pravidel ověřování nebudou pro kód akce kontroleru vyžadovat žádné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="886e4-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="886e4-203">Uložení odeslaných hodnot</span><span class="sxs-lookup"><span data-stu-id="886e4-203">Saving the submitted values</span></span>

<span data-ttu-id="886e4-204">Pokud odesláním formuláře projde ověřování, je čas uložit hodnoty do databáze.</span><span class="sxs-lookup"><span data-stu-id="886e4-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="886e4-205">U Entity Framework, který pouze vyžaduje přidání modelu do kolekce alba a volání metody SaveChanges.</span><span class="sxs-lookup"><span data-stu-id="886e4-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="886e4-206">Entity Framework generuje vhodné příkazy SQL pro zachování hodnoty.</span><span class="sxs-lookup"><span data-stu-id="886e4-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="886e4-207">Po uložení dat přesměrujeme zpátky na seznam alb, abychom mohli zobrazit naši aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="886e4-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="886e4-208">To se provádí vrácením RedirectToAction s názvem akce kontroleru, kterou chceme zobrazit.</span><span class="sxs-lookup"><span data-stu-id="886e4-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="886e4-209">V tomto případě je to metoda indexu.</span><span class="sxs-lookup"><span data-stu-id="886e4-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="886e4-210">Zobrazení neplatných odeslání formulářů s chybami ověřování</span><span class="sxs-lookup"><span data-stu-id="886e4-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="886e4-211">V případě neplatného vstupu formuláře jsou hodnoty rozevíracího seznamu přidány do ViewBag (jako v případě HTTP-GET) a hodnoty vázaného modelu jsou předány zpět do zobrazení pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="886e4-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="886e4-212">Chyby ověřování se automaticky zobrazí pomocí @Html.ValidationMessageFor pomocníka HTML.</span><span class="sxs-lookup"><span data-stu-id="886e4-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="886e4-213">Testování formuláře pro vytvoření</span><span class="sxs-lookup"><span data-stu-id="886e4-213">Testing the Create Form</span></span>

<span data-ttu-id="886e4-214">Pokud chcete tento test vyzkoušet, spusťte aplikaci a přejděte k/StoreManager/Create/– zobrazí se prázdný formulář, který vrátila metoda StoreController Create HTTP-GET.</span><span class="sxs-lookup"><span data-stu-id="886e4-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="886e4-215">Vyplňte některé hodnoty a kliknutím na tlačítko vytvořit formulář odešlete.</span><span class="sxs-lookup"><span data-stu-id="886e4-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="886e4-216">Zpracování úprav</span><span class="sxs-lookup"><span data-stu-id="886e4-216">Handling Edits</span></span>

<span data-ttu-id="886e4-217">Pár akcí úprav (HTTP-GET a HTTP-POST) se velmi podobá metodám pro vytváření akcí, které jsme právě prohlédli na.</span><span class="sxs-lookup"><span data-stu-id="886e4-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="886e4-218">Vzhledem k tomu, že scénář úprav zahrnuje práci s existujícím albumm, metoda upravit HTTP-GET načte album na základě parametru ID, která byla předána prostřednictvím trasy.</span><span class="sxs-lookup"><span data-stu-id="886e4-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="886e4-219">Tento kód pro načtení alba podle AlbumId je stejný jako v případě, že jste předtím prohlédli v akci kontroleru podrobností.</span><span class="sxs-lookup"><span data-stu-id="886e4-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="886e4-220">Stejně jako u metody Create/HTTP-GET jsou hodnoty rozevíracího seznamu vraceny prostřednictvím ViewBag.</span><span class="sxs-lookup"><span data-stu-id="886e4-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="886e4-221">To umožňuje vrátit album jako náš objekt modelu do zobrazení (které je silně typované pro třídu alba) a současně předat další data (např. seznam žánrů) prostřednictvím ViewBag.</span><span class="sxs-lookup"><span data-stu-id="886e4-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="886e4-222">Akce upravit HTTP-POST je velmi podobná akci vytvoření HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="886e4-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="886e4-223">Jediným rozdílem je, že místo přidání nového alba do databáze. Kolekce alb: aktuální instance alba vyhledáváme pomocí DB. Záznam (album) a nastavení jeho stavu na hodnotu změněno.</span><span class="sxs-lookup"><span data-stu-id="886e4-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="886e4-224">Tato zpráva oznamuje Entity Framework, že upravujeme existující album na rozdíl od vytvoření nového alba.</span><span class="sxs-lookup"><span data-stu-id="886e4-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="886e4-225">Tuto akci můžeme otestovat spuštěním aplikace a přechodem na/StoreManger/a následným kliknutím na odkaz upravit pro album.</span><span class="sxs-lookup"><span data-stu-id="886e4-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="886e4-226">Tím se zobrazí formulář pro úpravy zobrazený metodou upravit HTTP-GET.</span><span class="sxs-lookup"><span data-stu-id="886e4-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="886e4-227">Vyplňte některé hodnoty a klikněte na tlačítko Uložit.</span><span class="sxs-lookup"><span data-stu-id="886e4-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="886e4-228">Tato funkce odešle formulář, uloží hodnoty a vrátí nás do seznamu alb, kde je zobrazeno, že byly hodnoty aktualizovány.</span><span class="sxs-lookup"><span data-stu-id="886e4-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="886e4-229">Odstraňování zpracování</span><span class="sxs-lookup"><span data-stu-id="886e4-229">Handling Deletion</span></span>

<span data-ttu-id="886e4-230">Odstranění probíhá stejným vzorem jako operace Upravit a vytvořit, a to pomocí jedné akce kontroleru pro zobrazení potvrzovacího formuláře a další akce kontroleru pro zpracování odesílání formuláře.</span><span class="sxs-lookup"><span data-stu-id="886e4-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="886e4-231">Akce řadiče HTTP-GET Delete je přesně stejná jako u předchozí akce kontroleru podrobností Správce úložiště.</span><span class="sxs-lookup"><span data-stu-id="886e4-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="886e4-232">Pomocí šablony pro odstranění obsahu zobrazení zobrazíme formulář, který je silně zadaný pro typ alba.</span><span class="sxs-lookup"><span data-stu-id="886e4-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="886e4-233">Šablona pro odstranění zobrazuje všechna pole pro model, ale můžeme ho zjednodušit poměrně k tétomu bitu.</span><span class="sxs-lookup"><span data-stu-id="886e4-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="886e4-234">Změňte kód zobrazení v/Views/StoreManager/Delete.cshtml na následující.</span><span class="sxs-lookup"><span data-stu-id="886e4-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="886e4-235">Tím se zobrazí zjednodušené potvrzení o odstranění.</span><span class="sxs-lookup"><span data-stu-id="886e4-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="886e4-236">Kliknutím na tlačítko Odstranit dojde k odeslání formuláře zpět na server, který provede akci DeleteConfirmed.</span><span class="sxs-lookup"><span data-stu-id="886e4-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="886e4-237">Náš postup pro odstranění ovladače HTTP-POST provede tyto akce:</span><span class="sxs-lookup"><span data-stu-id="886e4-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="886e4-238">Načte album podle ID.</span><span class="sxs-lookup"><span data-stu-id="886e4-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="886e4-239">Odstraní album a uloží změny.</span><span class="sxs-lookup"><span data-stu-id="886e4-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="886e4-240">Přesměruje na index, který ukazuje, že se album odebralo ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="886e4-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="886e4-241">Pokud to chcete otestovat, spusťte aplikaci a přejděte do/StoreManager.</span><span class="sxs-lookup"><span data-stu-id="886e4-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="886e4-242">Vyberte album ze seznamu a klikněte na odkaz odstranit.</span><span class="sxs-lookup"><span data-stu-id="886e4-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="886e4-243">Zobrazí se vám obrazovka pro potvrzení odstranění.</span><span class="sxs-lookup"><span data-stu-id="886e4-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="886e4-244">Kliknutím na tlačítko Odstranit odeberete album a vrátíte se na stránku index Správce úložiště, kde se zobrazí, že se album odstranilo.</span><span class="sxs-lookup"><span data-stu-id="886e4-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="886e4-245">Zkrácení textu pomocí vlastní pomůcky HTML</span><span class="sxs-lookup"><span data-stu-id="886e4-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="886e4-246">Máme jeden možný problém s naší stránkou indexu správce obchodů.</span><span class="sxs-lookup"><span data-stu-id="886e4-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="886e4-247">Vlastnosti názvu našeho alba a jméno umělce můžou být dostatečně dlouhé, aby mohly vyvolat formátování tabulky.</span><span class="sxs-lookup"><span data-stu-id="886e4-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="886e4-248">Vytvoříme vlastní nápovědu HTML, která nám umožní snadno zkrátit tyto a další vlastnosti v našich zobrazeních.</span><span class="sxs-lookup"><span data-stu-id="886e4-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="886e4-249">Syntaxe @helper Razor má poměrně snadné vytváření vlastních pomocných funkcí pro použití ve vašich zobrazeních.</span><span class="sxs-lookup"><span data-stu-id="886e4-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="886e4-250">Otevřete zobrazení/Views/StoreManager/Index.cshtml a přidejte následující kód přímo za @model řádek.</span><span class="sxs-lookup"><span data-stu-id="886e4-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="886e4-251">Tato pomocná metoda přebírá řetězec a povoluje maximální délku.</span><span class="sxs-lookup"><span data-stu-id="886e4-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="886e4-252">Pokud je zadaný text kratší než zadaná délka, pomocník ho zapíše tak, jak je.</span><span class="sxs-lookup"><span data-stu-id="886e4-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="886e4-253">Pokud je delší, zkrátí text a vykreslí "...". pro zbytek.</span><span class="sxs-lookup"><span data-stu-id="886e4-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="886e4-254">Teď můžeme použít naši podpůrnou pomoc, aby se zajistilo, že vlastnosti názvu alba i jméno interpreta jsou kratší než 25 znaků.</span><span class="sxs-lookup"><span data-stu-id="886e4-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="886e4-255">Úplný kód zobrazení pomocí našeho nového pomocníka pro zkracování se zobrazí níže.</span><span class="sxs-lookup"><span data-stu-id="886e4-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="886e4-256">Když teď procházíme adresu URL/StoreManager/, budou se alba a tituly uchovávat pod maximálními délkami.</span><span class="sxs-lookup"><span data-stu-id="886e4-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="886e4-257">Poznámka: v tomto příkladu se zobrazuje jednoduchý případ vytváření a používání pomocníka v jednom zobrazení.</span><span class="sxs-lookup"><span data-stu-id="886e4-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="886e4-258">Další informace o vytváření pomocníků, které můžete použít v celém webu, najdete v příspěvku na blogu: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="886e4-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="886e4-259">[Předchozí](mvc-music-store-part-4.md)
> [Další](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="886e4-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
