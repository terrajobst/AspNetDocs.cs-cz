---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: Přidání nového pole do modelu a tabulky databáze (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: b2b26b6009c55f02c8a4159bda839fe7aefea4c0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457259"
---
# <a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a><span data-ttu-id="bf8c6-103">Přidání nového pole do modelu a databázové tabulky Movie (VB)</span><span class="sxs-lookup"><span data-stu-id="bf8c6-103">Adding a New Field to the Movie Model and Database Table (VB)</span></span>

<span data-ttu-id="bf8c6-104">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="bf8c6-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="bf8c6-105">V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="bf8c6-106">Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="bf8c6-107">Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="bf8c6-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="bf8c6-108">Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="bf8c6-109">Požadavky sady Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="bf8c6-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="bf8c6-110">Aktualizace nástrojů MVC 3 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bf8c6-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="bf8c6-111">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)</span><span class="sxs-lookup"><span data-stu-id="bf8c6-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="bf8c6-112">Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="bf8c6-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="bf8c6-113">Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="bf8c6-114">[Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="bf8c6-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="bf8c6-115">Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/adding-a-new-field.md) tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-115">If you prefer C#, switch to the [C# version](../cs/adding-a-new-field.md) of this tutorial.</span></span>

<span data-ttu-id="bf8c6-116">V této části provedete některé změny tříd modelu a zjistíte, jak můžete aktualizovat schéma databáze tak, aby odpovídalo změnám modelu.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-116">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="bf8c6-117">Přidání vlastnosti hodnocení do modelu videa</span><span class="sxs-lookup"><span data-stu-id="bf8c6-117">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="bf8c6-118">Začněte přidáním nové vlastnosti `Rating` do existující třídy `Movie`.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-118">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="bf8c6-119">Otevřete soubor *Movie.cs* a přidejte vlastnost `Rating`, jako je tato:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-119">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

<span data-ttu-id="bf8c6-120">Úplná `Movie` třída teď vypadá jako v následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-120">The complete `Movie` class now looks like the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

<span data-ttu-id="bf8c6-121">Znovu zkompilujte aplikaci pomocí příkazu **Debug** &gt;**Build Movie** nabídky.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-121">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="bf8c6-122">Teď, když jste aktualizovali `Model` třídu, budete také muset aktualizovat šablony zobrazení *\Views\Movies\Index.vbhtml* a *\Views\Movies\Create.vbhtml* , aby se podporovala nová vlastnost `Rating`.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-122">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.vbhtml* and *\Views\Movies\Create.vbhtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="bf8c6-123">Otevřete soubor<em>\Views\Movies\Index.vbhtml</em> a přidejte `<th>Rating</th>` záhlaví sloupce hned za sloupec <strong>Price</strong> .</span><span class="sxs-lookup"><span data-stu-id="bf8c6-123">Open the<em>\Views\Movies\Index.vbhtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="bf8c6-124">Pak přidejte `<td>` sloupec poblíž konce šablony, aby se vygenerovala `@item.Rating` hodnota.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-124">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="bf8c6-125">Níže je uveden aktualizovaný vzhled šablony zobrazení <em>index. vbhtml</em> jako:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-125">Below is what the updated <em>Index.vbhtml</em> view template looks like:</span></span>

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

<span data-ttu-id="bf8c6-126">Potom otevřete soubor *\Views\Movies\Create.vbhtml* a přidejte následující kód poblíž konce formuláře.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-126">Next, open the *\Views\Movies\Create.vbhtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="bf8c6-127">Tím vykreslíte textové pole, abyste mohli při vytváření nového filmu zadat hodnocení.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-127">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="bf8c6-128">Správa rozdílů v modelu a schématu databáze</span><span class="sxs-lookup"><span data-stu-id="bf8c6-128">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="bf8c6-129">Nyní jste aktualizovali kód aplikace, aby podporoval novou vlastnost `Rating`.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-129">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="bf8c6-130">Nyní spusťte aplikaci a přejděte na adresu URL */Movies* .</span><span class="sxs-lookup"><span data-stu-id="bf8c6-130">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="bf8c6-131">Když to uděláte, zobrazí se tato chyba:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-131">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="bf8c6-132">Tato chyba se zobrazuje, protože aktualizovaná třída modelu `Movie` v aplikaci je nyní odlišná od schématu `Movie` tabulky existující databáze.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-132">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="bf8c6-133">(V tabulce databáze nejsou žádné `Rating` sloupce.)</span><span class="sxs-lookup"><span data-stu-id="bf8c6-133">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="bf8c6-134">Ve výchozím nastavení platí, že při použití Entity Framework Code First k automatickému vytvoření databáze, stejně jako v tomto kurzu, Code First přidá do databáze tabulku, která bude sledovat, zda je schéma databáze synchronizované s třídami modelů, ze kterých byla vygenerována.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-134">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="bf8c6-135">Pokud nejsou synchronizované, Entity Framework vyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-135">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="bf8c6-136">Díky tomu je snazší sledovat problémy v době vývoje, které byste jinak mohli najít (překrytím chyb) v době běhu.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-136">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="bf8c6-137">Funkce synchronizace se ověřuje tím, že se zobrazí chybová zpráva, kterou jste právě viděli.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-137">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="bf8c6-138">Existují dva přístupy k řešení této chyby:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-138">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="bf8c6-139">Entity Framework automaticky vyřadit a znovu vytvořit databázi na základě nového schématu třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-139">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="bf8c6-140">Tento přístup je velmi výhodný při aktivním vývoji na testovací databázi, protože umožňuje rychlou vývoj modelu a schématu databáze dohromady.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-140">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="bf8c6-141">Nevýhodou, ale je to, že ztratíte stávající data v databázi, takže *nechcete tento* přístup použít v provozní databázi.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-141">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="bf8c6-142">Explicitně upravte schéma existující databáze tak, aby odpovídalo třídám modelu.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-142">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="bf8c6-143">Výhodou tohoto přístupu je, že zachováte data.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-143">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="bf8c6-144">Tuto změnu můžete provést buď ručně, nebo vytvořením skriptu změny databáze.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-144">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="bf8c6-145">V tomto kurzu použijeme první přístup – budete mít Entity Framework Code First automaticky znovu vytvořit databázi, kdykoli se změní model.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-145">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="bf8c6-146">Automatické opětovné vytvoření databáze při změnách modelu</span><span class="sxs-lookup"><span data-stu-id="bf8c6-146">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="bf8c6-147">Pojďme aplikaci aktualizovat tak, aby Code First automaticky vynechala a znovu vytvořila databázi, kdykoli změníte model aplikace.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-147">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bf8c6-148">**Upozornění** Tento postup je vhodné povolit pro automatické vyřazení a opětovné vytvoření databáze pouze v případě, že používáte vývojové nebo testovací databáze a *nikdy* nemáte v provozní databázi, která obsahuje skutečná data.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-148">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="bf8c6-149">Použití na provozním serveru může způsobit ztrátu dat.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-149">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="bf8c6-150">V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-150">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="bf8c6-151">Pojmenujte třídu &quot;MovieInitializer&quot;.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-151">Name the class &quot;MovieInitializer&quot;.</span></span> <span data-ttu-id="bf8c6-152">Aktualizujte třídu `MovieInitializer` tak, aby obsahovala následující kód:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-152">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

<span data-ttu-id="bf8c6-153">Třída `MovieInitializer` určuje, že databáze používaná modelem by měla být vyřazena a automaticky vytvořena, pokud se třídy modelů stále mění.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-153">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="bf8c6-154">Kód obsahuje metodu `Seed` k určení některých výchozích dat, která mají být automaticky přidána do databáze při každém vytvoření (nebo opětovném vytvoření).</span><span class="sxs-lookup"><span data-stu-id="bf8c6-154">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="bf8c6-155">To poskytuje užitečný způsob, jak naplnit databázi pomocí některých ukázkových dat, aniž byste je museli ručně naplnit pokaždé, když provedete změnu modelu.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-155">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="bf8c6-156">Teď, když jste definovali `MovieInitializer` třídu, budete ji chtít nasměrovat tak, aby pokaždé, když se aplikace spustí, zkontroluje, jestli se třídy modelu liší od schématu v databázi.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-156">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="bf8c6-157">Pokud jsou, můžete spustit inicializátor pro opětovné vytvoření databáze, aby odpovídala modelu, a pak naplnit databázi ukázkovými daty.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-157">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="bf8c6-158">Otevřete soubor *Global. asax* , který je v kořenovém adresáři projektu `MvcMovies`:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-158">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

<span data-ttu-id="bf8c6-159">Soubor *Global. asax* obsahuje třídu, která definuje celou aplikaci pro projekt, a obsahuje `Application_Start` obslužnou rutinu události, která se spouští při prvním spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-159">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="bf8c6-160">Vyhledejte metodu `Application_Start` a přidejte volání `Database.SetInitializer` na začátku metody, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-160">Find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

<span data-ttu-id="bf8c6-161">Příkaz `Database.SetInitializer`, který jste právě přidali, indikuje, že databáze používaná instancí `MovieDBContext` by měla být automaticky odstraněna a znovu vytvořena, pokud se schéma a databáze neshodují.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-161">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="bf8c6-162">A jak jste viděli, naplní databázi také ukázkovými daty, která jsou zadána ve třídě `MovieInitializer`.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-162">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="bf8c6-163">Zavřete soubor *Global. asax* .</span><span class="sxs-lookup"><span data-stu-id="bf8c6-163">Close the *Global.asax* file.</span></span>

<span data-ttu-id="bf8c6-164">Spusťte aplikaci znovu a přejděte na adresu URL */Movies* .</span><span class="sxs-lookup"><span data-stu-id="bf8c6-164">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="bf8c6-165">Po spuštění aplikace zjistí, že struktura modelu již neodpovídá schématu databáze.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-165">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="bf8c6-166">Automaticky znovu vytvoří databázi tak, aby odpovídala nové struktuře modelů a naplnila databázi ukázkovými filmy:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-166">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

<span data-ttu-id="bf8c6-168">Kliknutím na odkaz **vytvořit nový** přidejte nový film.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-168">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="bf8c6-169">Všimněte si, že můžete přidat hodnocení.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-169">Note that you can add a rating.</span></span>

<span data-ttu-id="bf8c6-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="bf8c6-170">[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)</span></span>

<span data-ttu-id="bf8c6-171">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-171">Click **Create**.</span></span> <span data-ttu-id="bf8c6-172">Nový film, včetně hodnocení, se teď zobrazí v seznamu filmů:</span><span class="sxs-lookup"><span data-stu-id="bf8c6-172">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

<span data-ttu-id="bf8c6-174">V této části jste viděli, jak můžete upravovat objekty modelu a udržovat databázi synchronizované se změnami.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-174">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="bf8c6-175">Zjistili jste taky způsob, jak naplnit nově vytvořenou databázi pomocí ukázkových dat, abyste si mohli vyzkoušet scénáře.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-175">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="bf8c6-176">Teď se podíváme na to, jak můžete přidat bohatou logiku ověřování do tříd modelu a povolit uplatnění některých obchodních pravidel.</span><span class="sxs-lookup"><span data-stu-id="bf8c6-176">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bf8c6-177">[Předchozí](examining-the-edit-methods-and-edit-view.md)
> [Další](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="bf8c6-177">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
