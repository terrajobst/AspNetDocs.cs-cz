---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Vytvoření databáze | Dokumentace Microsoftu
author: shanselman
description: Toto je kurz pro začátečníky, který vysvětluje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117678"
---
# <a name="creating-a-database"></a><span data-ttu-id="efd90-104">Vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="efd90-104">Creating a Database</span></span>

<span data-ttu-id="efd90-105">podle [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="efd90-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="efd90-106">Toto je kurz pro začátečníky, který vysvětluje základy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="efd90-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="efd90-107">Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.</span><span class="sxs-lookup"><span data-stu-id="efd90-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="efd90-108">Přejděte [výukové centrum pro ASP.NET MVC](../../../index.md) najít další technologie ASP.NET MVC, kurzů a ukázek.</span><span class="sxs-lookup"><span data-stu-id="efd90-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="efd90-109">V této části jsme se chystáte vytvořit novou databázi SQL Express, který použijeme k ukládání a načítání naše data o filmech.</span><span class="sxs-lookup"><span data-stu-id="efd90-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="efd90-110">Z integrovaného vývojového prostředí Visual Web Developer, vyberte zobrazení | Průzkumník serveru.</span><span class="sxs-lookup"><span data-stu-id="efd90-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="efd90-111">Klikněte pravým tlačítkem na datová připojení a klikněte na tlačítko Přidat připojení...</span><span class="sxs-lookup"><span data-stu-id="efd90-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="efd90-113">V dialogovém okně Zvolit zdroj dat vyberte Microsoft SQL Server a vyberte možnost pokračovat.</span><span class="sxs-lookup"><span data-stu-id="efd90-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="efd90-114">V dialogovém okně Přidat připojení zadejte ". \SQLEXPRESS" pro název serveru a zadejte "Filmy" jako název pro novou databázi.</span><span class="sxs-lookup"><span data-stu-id="efd90-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="efd90-115">[![Přidat připojení – dialogové okno](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="efd90-116">Klikněte na tlačítko OK a zobrazí se dotaz, pokud chcete vytvořit databázi.</span><span class="sxs-lookup"><span data-stu-id="efd90-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="efd90-117">Výběrem možnosti Ano.</span><span class="sxs-lookup"><span data-stu-id="efd90-117">Select yes.</span></span>

<span data-ttu-id="efd90-118">[![Vytvářet videa?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="efd90-119">Nyní máte v Průzkumníku serveru k dispozici prázdnou databázi.</span><span class="sxs-lookup"><span data-stu-id="efd90-119">Now you've got an empty database in Server Explorer.</span></span>

![Přidat novou tabulku](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="efd90-121">Klikněte pravým tlačítkem na tabulky a klikněte na tlačítko Přidat tabulku.</span><span class="sxs-lookup"><span data-stu-id="efd90-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="efd90-122">Zobrazí se Návrhář tabulky.</span><span class="sxs-lookup"><span data-stu-id="efd90-122">The Table Designer will appear.</span></span> <span data-ttu-id="efd90-123">Přidání sloupce pro Id, název, ReleaseDate, rozšířením podle tematických a ceny.</span><span class="sxs-lookup"><span data-stu-id="efd90-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="efd90-124">Klikněte pravým tlačítkem na sloupec ID a klikněte na nastavit primární klíč.</span><span class="sxs-lookup"><span data-stu-id="efd90-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="efd90-125">Tady je Moje návrhu oblasti, které vypadá.</span><span class="sxs-lookup"><span data-stu-id="efd90-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="efd90-126">[![Editor tabulek databáze](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="efd90-127">Vyberte sloupec Id také a v části Vlastnosti sloupce níže změňte "Specifikace Identity" na "Ano".</span><span class="sxs-lookup"><span data-stu-id="efd90-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="efd90-128">[![IsIdentity – vlastnosti sloupce](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="efd90-129">Když máte to Hotovo, klikněte na ikonu Uložit na panelu nástrojů nebo si vybrat soubor | Uložte v nabídce a pojmenujte tabulku "**film**" (singulární).</span><span class="sxs-lookup"><span data-stu-id="efd90-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="efd90-130">Máme databáze a tabulky!</span><span class="sxs-lookup"><span data-stu-id="efd90-130">We've got a database and a table!</span></span>

<span data-ttu-id="efd90-131">[![Zvolte název](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="efd90-132">Přejděte zpět do Průzkumníka serveru a tabulky Movie klikněte pravým tlačítkem myši a pak vyberte "Zobrazit Data tabulky."</span><span class="sxs-lookup"><span data-stu-id="efd90-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="efd90-133">Zadejte několik filmy, aby naše databáze má nějaká data.</span><span class="sxs-lookup"><span data-stu-id="efd90-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="efd90-134">[![Úpravy tabulek databáze](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="efd90-135">Vytvoření modelu</span><span class="sxs-lookup"><span data-stu-id="efd90-135">Creating a Model</span></span>

<span data-ttu-id="efd90-136">Nyní, přepněte zpět do Průzkumníku řešení v integrovaném vývojovém prostředí pravé straně a klikněte pravým tlačítkem na složku modely a vyberte možnost Přidat | Nová položka.</span><span class="sxs-lookup"><span data-stu-id="efd90-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="efd90-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="efd90-138">My budeme k vytvoření modelu Entity z naší nové databáze.</span><span class="sxs-lookup"><span data-stu-id="efd90-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="efd90-139">Sada tříd bude přidán do projektu, který usnadňuje nám pro dotazování a manipulaci s daty v rámci naší databázi.</span><span class="sxs-lookup"><span data-stu-id="efd90-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="efd90-140">Vyberte datový uzel na levé straně dialogového okna a pak vyberte šablonu položky ADO.NET Entity Data Model.</span><span class="sxs-lookup"><span data-stu-id="efd90-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="efd90-141">Pojmenujte ji Movies.edmx.</span><span class="sxs-lookup"><span data-stu-id="efd90-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="efd90-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="efd90-143">Klikněte na tlačítko "Přidat".</span><span class="sxs-lookup"><span data-stu-id="efd90-143">Click the "Add" button.</span></span> <span data-ttu-id="efd90-144">Tím se spustí potom "Průvodce entitního modelu dat".</span><span class="sxs-lookup"><span data-stu-id="efd90-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="efd90-145">V dialogovém okně Nový, která se otevře vyberte možnost Generovat z databáze.</span><span class="sxs-lookup"><span data-stu-id="efd90-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="efd90-146">Protože jsme právě databázi, potřebujeme jenom Entity Framework říct naši novou databázi a její tabulky.</span><span class="sxs-lookup"><span data-stu-id="efd90-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="efd90-147">Klikněte na tlačítko vedle uložit připojení k naší databázi v konfiguraci naši webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="efd90-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="efd90-148">Teď zkontrolujte tabulky a filmové zaškrtávací políčko a klikněte na tlačítko Dokončit.</span><span class="sxs-lookup"><span data-stu-id="efd90-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="efd90-149">[![Průvodce datovým modelem entity](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="efd90-150">Nyní jsme najdete v naší nové tabulky Movie v Entity Framework Designer a k němu přístup z kódu.</span><span class="sxs-lookup"><span data-stu-id="efd90-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="efd90-151">[![Videa – Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="efd90-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="efd90-152">Na návrhové ploše vidíte třídou "Video".</span><span class="sxs-lookup"><span data-stu-id="efd90-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="efd90-153">Tato třída se mapuje na tabulku "Video" v naší databázi a každou vlastnost v něm se mapuje na sloupec v tabulce.</span><span class="sxs-lookup"><span data-stu-id="efd90-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="efd90-154">Každá instance třídy "Video" bude odpovídat řádek v tabulce "Video".</span><span class="sxs-lookup"><span data-stu-id="efd90-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="efd90-155">Pokud se vám výchozí názvy a mapování konvencemi použitými rozhraním Entity Framework, můžete změnit nebo si je přizpůsobit, Entity Framework designer.</span><span class="sxs-lookup"><span data-stu-id="efd90-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="efd90-156">Pro tuto aplikaci použijeme výchozí hodnoty a stačí uložit soubor jako-je.</span><span class="sxs-lookup"><span data-stu-id="efd90-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="efd90-157">Nyní se budeme pracovat s daty skutečné!</span><span class="sxs-lookup"><span data-stu-id="efd90-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="efd90-158">[Předchozí](getting-started-with-mvc-part3.md)
> [další](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="efd90-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
