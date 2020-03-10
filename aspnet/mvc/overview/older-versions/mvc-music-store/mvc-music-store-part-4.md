---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4\. část: modely a přístup k datům | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 4 pokrývá modely a přístup k datům.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559673"
---
# <a name="part-4-models-and-data-access"></a><span data-ttu-id="a3987-104">4\. část: Modely a přístup k datům</span><span class="sxs-lookup"><span data-stu-id="a3987-104">Part 4: Models and Data Access</span></span>

<span data-ttu-id="a3987-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="a3987-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="a3987-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="a3987-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="a3987-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="a3987-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="a3987-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="a3987-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="a3987-109">Část 4 pokrývá modely a přístup k datům.</span><span class="sxs-lookup"><span data-stu-id="a3987-109">Part 4 covers Models and Data Access.</span></span>

<span data-ttu-id="a3987-110">Zatím jsme právě předali "" fiktivní data "z našich řadičů do našich šablon zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a3987-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="a3987-111">Teď jsme připraveni připojit skutečnou databázi.</span><span class="sxs-lookup"><span data-stu-id="a3987-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="a3987-112">V tomto kurzu pokryjeme, jak používat edici SQL Server Compact (často označovanou jako SQL CE) jako náš databázový stroj.</span><span class="sxs-lookup"><span data-stu-id="a3987-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="a3987-113">SQL CE je bezplatná, vložená databáze založená na souborech, která nevyžaduje žádnou instalaci nebo konfiguraci, což usnadňuje místní vývoj.</span><span class="sxs-lookup"><span data-stu-id="a3987-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="a3987-114">Přístup k databázi pomocí Entity Frameworkho kódu – první</span><span class="sxs-lookup"><span data-stu-id="a3987-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="a3987-115">K dotazování a aktualizaci databáze budeme používat podporu Entity Framework (EF), která je obsažená v projektech ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="a3987-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="a3987-116">EF je flexibilní rozhraní API pro mapování relačních objektů (ORM), které umožňuje vývojářům dotazovat a aktualizovat data uložená v databázi v objektově orientovaném způsobem.</span><span class="sxs-lookup"><span data-stu-id="a3987-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="a3987-117">Entity Framework verze 4 podporuje vývojové paradigma s názvem Code-First.</span><span class="sxs-lookup"><span data-stu-id="a3987-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="a3987-118">Code – First umožňuje vytvořit objekt modelu zápisem jednoduchých tříd (označovaných také jako POCO z objektů CLR "v prostém formátu") a může dokonce vytvořit databázi průběžně z vašich tříd.</span><span class="sxs-lookup"><span data-stu-id="a3987-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="a3987-119">Změny v našich třídách modelu</span><span class="sxs-lookup"><span data-stu-id="a3987-119">Changes to our Model Classes</span></span>

<span data-ttu-id="a3987-120">Využijeme funkci vytváření databáze v Entity Framework v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="a3987-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="a3987-121">Předtím, než to provedeme, provedeme několik menších změn našich tříd modelů, které se dají přidat do některých věcí, které použijeme později.</span><span class="sxs-lookup"><span data-stu-id="a3987-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="a3987-122">Přidání tříd interpretů</span><span class="sxs-lookup"><span data-stu-id="a3987-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="a3987-123">Naše alba budou přidružena k umělcům, takže přidáme jednoduchou třídu modelu pro popis interpreta.</span><span class="sxs-lookup"><span data-stu-id="a3987-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="a3987-124">Do složky modely s názvem Artist.cs přidejte novou třídu pomocí kódu uvedeného níže.</span><span class="sxs-lookup"><span data-stu-id="a3987-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="a3987-125">Aktualizují se třídy modelů</span><span class="sxs-lookup"><span data-stu-id="a3987-125">Updating our Model Classes</span></span>

<span data-ttu-id="a3987-126">Aktualizujte třídu alba, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="a3987-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="a3987-127">Dále proveďte následující aktualizace třídy žánru.</span><span class="sxs-lookup"><span data-stu-id="a3987-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a><span data-ttu-id="a3987-128">Přidání složky s\_dat aplikace</span><span class="sxs-lookup"><span data-stu-id="a3987-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="a3987-129">Do našeho projektu přidáme aplikaci\_datový adresář, abychom mohli uchovávat soubory databáze SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="a3987-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="a3987-130">Data\_aplikace jsou speciální adresář v ASP.NET, který už má správná oprávnění zabezpečení přístupu pro přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="a3987-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="a3987-131">V nabídce projekt vyberte Přidat složku ASP.NET a pak aplikace\_data.</span><span class="sxs-lookup"><span data-stu-id="a3987-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="a3987-132">Vytvoření připojovacího řetězce v souboru Web. config</span><span class="sxs-lookup"><span data-stu-id="a3987-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="a3987-133">Do konfiguračního souboru webu přidáme pár řádků, aby Entity Framework vědět, jak se připojit k naší databázi.</span><span class="sxs-lookup"><span data-stu-id="a3987-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="a3987-134">Dvakrát klikněte na soubor Web. config umístěný v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="a3987-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="a3987-135">Posuňte se k dolnímu okraji tohoto souboru a přidejte &lt;connectionStrings&gt; sekci přímo nad poslední řádek, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="a3987-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="a3987-136">Přidání třídy kontextu</span><span class="sxs-lookup"><span data-stu-id="a3987-136">Adding a Context Class</span></span>

<span data-ttu-id="a3987-137">Klikněte pravým tlačítkem na složku modely a přidejte novou třídu s názvem MusicStoreEntities.cs.</span><span class="sxs-lookup"><span data-stu-id="a3987-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="a3987-138">Tato třída bude představovat kontext databáze Entity Framework a bude zpracovávat naše operace vytvoření, čtení, aktualizace a odstranění pro nás.</span><span class="sxs-lookup"><span data-stu-id="a3987-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="a3987-139">Kód pro tuto třídu je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="a3987-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="a3987-140">To je to – neexistuje žádná další konfigurace, speciální rozhraní atd. Rozšířením základní třídy DbContext je naše třída MusicStoreEntities schopna zpracovat naše databázové operace pro nás.</span><span class="sxs-lookup"><span data-stu-id="a3987-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="a3987-141">Teď, když jsme se připojili, můžeme přidat několik dalších vlastností do našich tříd modelů a využít tak některé z dalších informací v naší databázi.</span><span class="sxs-lookup"><span data-stu-id="a3987-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="a3987-142">Přidávají se naše data katalogu Storu.</span><span class="sxs-lookup"><span data-stu-id="a3987-142">Adding our store catalog data</span></span>

<span data-ttu-id="a3987-143">Budeme využívat funkci Entity Framework, která přidá "počáteční" data do nově vytvořené databáze.</span><span class="sxs-lookup"><span data-stu-id="a3987-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="a3987-144">Tím se předem naplní náš katalog Storu seznamem žánrů, umělců a alb.</span><span class="sxs-lookup"><span data-stu-id="a3987-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="a3987-145">Stažení MvcMusicStore-Assets. zip – které zahrnovalo naše soubory návrhu webu použité dříve v tomto kurzu – obsahuje soubor třídy s těmito počátečními daty, který je umístěný ve složce s názvem Code.</span><span class="sxs-lookup"><span data-stu-id="a3987-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="a3987-146">Ve složce Code/modely vyhledejte soubor SampleData.cs a umístěte jej do složky modely v našem projektu, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="a3987-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="a3987-147">Nyní musíme přidat jeden řádek kódu, který sděluje Entity Framework o této třídě SampleData.</span><span class="sxs-lookup"><span data-stu-id="a3987-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="a3987-148">Dvojím kliknutím na soubor Global. asax v kořenovém adresáři projektu jej otevřete a přidejte následující řádek do horní části aplikace\_spustit metodu.</span><span class="sxs-lookup"><span data-stu-id="a3987-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="a3987-149">V tomto okamžiku dokončili jsme práci nutnou ke konfiguraci Entity Framework pro náš projekt.</span><span class="sxs-lookup"><span data-stu-id="a3987-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="a3987-150">Dotazy do databáze</span><span class="sxs-lookup"><span data-stu-id="a3987-150">Querying the Database</span></span>

<span data-ttu-id="a3987-151">Teď aktualizujeme naše StoreController tak, aby místo použití "fiktivních dat" místo toho volaly do naší databáze dotaz na všechny informace.</span><span class="sxs-lookup"><span data-stu-id="a3987-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="a3987-152">Zahájíme deklarováním pole v **StoreController** k uložení instance třídy MusicStoreEntities s názvem storeDB:</span><span class="sxs-lookup"><span data-stu-id="a3987-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="a3987-153">Aktualizace indexu úložiště pro dotazování databáze</span><span class="sxs-lookup"><span data-stu-id="a3987-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="a3987-154">Třída MusicStoreEntities je udržována Entity Framework a zpřístupňuje vlastnost kolekce pro každou tabulku v naší databázi.</span><span class="sxs-lookup"><span data-stu-id="a3987-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="a3987-155">Pojďme aktualizovat naši akci indexu StoreController a načíst všechny žánry v naší databázi.</span><span class="sxs-lookup"><span data-stu-id="a3987-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="a3987-156">Dříve jsme to provedli pomocí pevného kódování řetězcových dat.</span><span class="sxs-lookup"><span data-stu-id="a3987-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="a3987-157">Místo toho můžeme pouze Entity Framework použít Generesou kontextovou kolekci:</span><span class="sxs-lookup"><span data-stu-id="a3987-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="a3987-158">Od naší šablony zobrazení se nemusí provádět žádné změny, protože pořád vracíme stejné StoreIndexViewModel, jako jsme vrátili data z naší databáze hned teď!</span><span class="sxs-lookup"><span data-stu-id="a3987-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="a3987-159">Když znovu spustíte projekt a navštívíte adresu URL "/Store", zobrazí se teď seznam všech žánrů v naší databázi:</span><span class="sxs-lookup"><span data-stu-id="a3987-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="a3987-160">Aktualizace procházení a podrobností Storu pro použití živých dat</span><span class="sxs-lookup"><span data-stu-id="a3987-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="a3987-161">Pomocí metody Action/Store/Browse? Žánr = *[subžánr]* hledáme Žánr podle názvu.</span><span class="sxs-lookup"><span data-stu-id="a3987-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="a3987-162">Očekáváme jenom jeden výsledek, protože by nikdy neměl mít dvě položky pro stejný název žánru, a proto můžeme použít. Rozšíření Single () v LINQ pro dotaz na příslušný objekt žánru (ještě nepište):</span><span class="sxs-lookup"><span data-stu-id="a3987-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="a3987-163">Jediná metoda přijímá výraz lambda jako parametr, který určuje, že chceme, aby měl jeden objekt žánru tak, aby jeho název odpovídal hodnotě, kterou jsme definovali.</span><span class="sxs-lookup"><span data-stu-id="a3987-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="a3987-164">V výše uvedeném případě načítáme jeden objekt žánru s hodnotou názvu, která odpovídá discích.</span><span class="sxs-lookup"><span data-stu-id="a3987-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="a3987-165">Využijeme funkci Entity Framework, která nám umožní označit další související entity, které chceme načíst, i když se objekt žánru načte.</span><span class="sxs-lookup"><span data-stu-id="a3987-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="a3987-166">Tato funkce se nazývá tvarování výsledků dotazů a umožňuje snížit počet pokusů, které potřebujeme pro přístup k databázi, aby se načetly všechny informace, které potřebujeme.</span><span class="sxs-lookup"><span data-stu-id="a3987-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="a3987-167">Chceme předběžně načíst alba pro žánry, které načteme, abychom aktualizovali náš dotaz tak, aby se zahrnul ze žánrů. zahrňte ("alba"), abyste označili, že máme také související alba.</span><span class="sxs-lookup"><span data-stu-id="a3987-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="a3987-168">To je efektivnější, protože načte data žánru i alba v jediné žádosti databáze.</span><span class="sxs-lookup"><span data-stu-id="a3987-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="a3987-169">Tady je vysvětlení, jak vypadá naše aktualizovaná akce kontroleru procházení:</span><span class="sxs-lookup"><span data-stu-id="a3987-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="a3987-170">Teď můžeme aktualizovat zobrazení pro procházení Storu, aby se zobrazila alba, která jsou k dispozici v jednotlivých žánrech.</span><span class="sxs-lookup"><span data-stu-id="a3987-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="a3987-171">Otevřete šablonu zobrazení (najdete v/Views/Store/Browse.cshtml) a přidejte seznam alb s odrážkami, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="a3987-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="a3987-172">Po spuštění naší aplikace a přechodu na/Store/Browse? Žánr = Jazz vidíte, že se výsledky z databáze teď shromažďují a zobrazují se všechna alba v našem vybraném žánru.</span><span class="sxs-lookup"><span data-stu-id="a3987-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="a3987-173">Provedeme stejnou změnu na naši adresu URL/Store/Details/[ID] a nahradíme naše fiktivní data databázovým dotazem, který načte album, jehož ID odpovídá hodnotě parametru.</span><span class="sxs-lookup"><span data-stu-id="a3987-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="a3987-174">Spuštění naší aplikace a procházení na/Store/Details/1 ukazuje, že se z databáze teď shromažďují výsledky.</span><span class="sxs-lookup"><span data-stu-id="a3987-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="a3987-175">Teď, když je naše stránka s podrobnostmi o Storu nastavená tak, aby zobrazovala album podle ID alba, pojďme aktualizovat zobrazení pro **procházení** a propojit zobrazení podrobností.</span><span class="sxs-lookup"><span data-stu-id="a3987-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="a3987-176">Použijeme HTML. ActionLink, přesně tak, jak jsme přešli na odkaz z indexu úložiště k uložení na konci předchozí části.</span><span class="sxs-lookup"><span data-stu-id="a3987-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="a3987-177">Níže se zobrazí úplný zdroj zobrazení pro procházení.</span><span class="sxs-lookup"><span data-stu-id="a3987-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="a3987-178">Teď jsme schopni přejít ze stránky pro Store na stránku žánru, která obsahuje seznam dostupných alb a kliknutím na album si můžete zobrazit podrobnosti o tomto albu.</span><span class="sxs-lookup"><span data-stu-id="a3987-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="a3987-179">[Předchozí](mvc-music-store-part-3.md)
> [Další](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="a3987-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
