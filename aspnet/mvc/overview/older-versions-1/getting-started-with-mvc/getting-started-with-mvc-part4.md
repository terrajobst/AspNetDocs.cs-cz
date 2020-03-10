---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Vytvoření databáze | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581436"
---
# <a name="creating-a-database"></a><span data-ttu-id="0cb3f-104">Vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="0cb3f-104">Creating a Database</span></span>

<span data-ttu-id="0cb3f-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="0cb3f-106">Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="0cb3f-107">Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="0cb3f-108">Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="0cb3f-109">V této části vytvoříme novou databázi SQL Express, kterou použijeme k ukládání a načítání našich filmových dat.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="0cb3f-110">V integrovaném vývojovém prostředí sady Visual Web Developer vyberte Zobrazit | Průzkumník serveru.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="0cb3f-111">Klikněte pravým tlačítkem na datová připojení a klikněte na Přidat připojení...</span><span class="sxs-lookup"><span data-stu-id="0cb3f-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="0cb3f-113">V dialogovém okně Zvolit zdroj dat vyberte možnost Microsoft SQL Server a vyberte možnost pokračovat.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="0cb3f-114">V dialogovém okně Přidat připojení zadejte ".\SQLEXPRESS" pro název vašeho serveru a jako název nové databáze zadejte "filmy".</span><span class="sxs-lookup"><span data-stu-id="0cb3f-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="0cb3f-115">[dialog ![přidat připojení](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="0cb3f-116">Klikněte na OK a zobrazí se dotaz, jestli chcete vytvořit tuto databázi.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="0cb3f-117">Vyberte Ano.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-117">Select yes.</span></span>

<span data-ttu-id="0cb3f-118">[![vytvořit filmy?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="0cb3f-119">Nyní máte v Průzkumník serveru prázdnou databázi.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-119">Now you've got an empty database in Server Explorer.</span></span>

![Přidat novou tabulku](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="0cb3f-121">Klikněte pravým tlačítkem na tabulky a klikněte na Přidat tabulku.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="0cb3f-122">Zobrazí se Návrhář tabulky.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-122">The Table Designer will appear.</span></span> <span data-ttu-id="0cb3f-123">Přidejte sloupce pro ID, název, ReleaseDate, Žánr a cenu.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="0cb3f-124">Klikněte pravým tlačítkem na sloupec ID a pak klikněte na nastavit primární klíč.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="0cb3f-125">Tady vidíte, jak vypadají moje oblasti návrhu.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="0cb3f-126">[![Editor databázových tabulek](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="0cb3f-127">Také vyberte sloupec ID a v části vlastnosti sloupce níže změňte "specifikace identity" na "Ano".</span><span class="sxs-lookup"><span data-stu-id="0cb3f-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="0cb3f-128">[![vlastnosti identity-Column](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="0cb3f-129">Až to bude hotové, klikněte na panelu nástrojů na ikonu Uložit nebo vyberte soubor | Uložte si z nabídky a pojmenujte tabulku "**film**" (v jednotném čísle).</span><span class="sxs-lookup"><span data-stu-id="0cb3f-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="0cb3f-130">Máme databázi a tabulku!</span><span class="sxs-lookup"><span data-stu-id="0cb3f-130">We've got a database and a table!</span></span>

<span data-ttu-id="0cb3f-131">[![zvolit název](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="0cb3f-132">Vraťte se na Průzkumník serveru a klikněte pravým tlačítkem myši na tabulku video a pak vyberte možnost zobrazit data tabulky.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="0cb3f-133">Zadejte několik filmů, aby naše databáze měla nějaká data.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="0cb3f-134">[![úpravy databázových tabulek](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="0cb3f-135">Vytvoření modelu</span><span class="sxs-lookup"><span data-stu-id="0cb3f-135">Creating a Model</span></span>

<span data-ttu-id="0cb3f-136">Nyní přejděte zpět na Průzkumník řešení na pravé straně rozhraní IDE a klikněte pravým tlačítkem na složku modely a vyberte Přidat | Nová položka.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="0cb3f-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="0cb3f-138">Z naší nové databáze vytvoříme model entity.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="0cb3f-139">Tím se do našeho projektu přidá sada tříd, která nám usnadňuje dotazování na data v naší databázi a manipulaci s nimi.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="0cb3f-140">Na levé straně dialogového okna vyberte datový uzel a pak vyberte šablonu ADO.NET model EDM (Entity Data Model) Item.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="0cb3f-141">Pojmenujte ho Movies. edmx.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="0cb3f-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="0cb3f-143">Klikněte na tlačítko Přidat.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-143">Click the "Add" button.</span></span> <span data-ttu-id="0cb3f-144">Pak se spustí Průvodce model EDM (Entity Data Model).</span><span class="sxs-lookup"><span data-stu-id="0cb3f-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="0cb3f-145">V novém dialogovém okně, které se zobrazí, vyberte možnost generovat z databáze.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="0cb3f-146">Vzhledem k tomu, že jsme právě vytvořili databázi, je potřeba sdělit Entity Framework o naší nové databázi a její tabulce.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="0cb3f-147">Kliknutím na tlačítko Další uložíte připojení k databázi v konfiguraci naší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="0cb3f-148">Nyní zaškrtněte políčko tabulky a video a klikněte na tlačítko Dokončit.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="0cb3f-149">[Průvodce model EDM (Entity Data Model) ![](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="0cb3f-150">Nyní můžeme zobrazit naši novou tabulku filmů v Entity Framework Designer a přistupovat k ní z kódu.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="0cb3f-151">[Filmy ![– Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="0cb3f-152">Na návrhové ploše vidíte třídu "video".</span><span class="sxs-lookup"><span data-stu-id="0cb3f-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="0cb3f-153">Tato třída se mapuje na tabulku "film" v naší databázi a každá vlastnost v ní je namapována na sloupec s tabulkou.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="0cb3f-154">Každá instance třídy "video" bude odpovídat řádku v tabulce "video".</span><span class="sxs-lookup"><span data-stu-id="0cb3f-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="0cb3f-155">Pokud se vám nelíbí výchozí konvence pojmenování a mapování, které používá Entity Framework, můžete k jejich změně nebo přizpůsobení použít návrháře Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="0cb3f-156">Pro tuto aplikaci použijeme výchozí hodnoty a jenom soubor uložte tak, jak je.</span><span class="sxs-lookup"><span data-stu-id="0cb3f-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="0cb3f-157">Teď budeme pracovat s některými skutečnými daty!</span><span class="sxs-lookup"><span data-stu-id="0cb3f-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0cb3f-158">[Předchozí](getting-started-with-mvc-part3.md)
> [Další](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="0cb3f-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
