---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: Přidání sloupce do modelu | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543580"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="b2cfd-104">Přidání sloupce do modelu</span><span class="sxs-lookup"><span data-stu-id="b2cfd-104">Adding a Column to the Model</span></span>

<span data-ttu-id="b2cfd-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="b2cfd-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="b2cfd-106">Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="b2cfd-107">Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="b2cfd-108">Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="b2cfd-109">V této části se dozvíte, jak můžeme udělat změny schématu naší databáze a zpracovat změny v rámci naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="b2cfd-110">Pojďme do tabulky filmů přidat sloupec hodnocení.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="b2cfd-111">Vraťte se do prostředí IDE a klikněte na Průzkumník databáze.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="b2cfd-112">Klikněte pravým tlačítkem myši na tabulku filmů a vyberte možnost otevřít definici tabulky.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="b2cfd-113">Přidejte sloupec hodnocení, jak je vidět níže.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="b2cfd-114">Vzhledem k tomu, že zatím nemáme žádná hodnocení, může sloupec povolit hodnoty null.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="b2cfd-115">Klikněte na Uložit.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-115">Click Save.</span></span>

<span data-ttu-id="b2cfd-116">[![úprava tabulky filmů](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b2cfd-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="b2cfd-117">Pak se vraťte do Průzkumník řešení a otevřete soubor video. edmx (který je ve složce \Models).</span><span class="sxs-lookup"><span data-stu-id="b2cfd-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="b2cfd-118">Klikněte pravým tlačítkem na plochu návrhu (bílá oblast) a vyberte aktualizovat model z databáze.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="b2cfd-119">[Filmy ![– Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b2cfd-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="b2cfd-120">Tím se spustí Průvodce aktualizací.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="b2cfd-121">Klikněte na kartu aktualizovat a pak klikněte na Dokončit.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="b2cfd-122">Naše třída filmového modelu se pak aktualizuje pomocí nového sloupce.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-122">Our Movie model class will then be updated with the new column.</span></span>

![Průvodce aktualizací (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="b2cfd-124">Po kliknutí na Dokončit uvidíte nový sloupec hodnocení, který je v našem modelu přidaný do entity video.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="b2cfd-125">[Entita ![Movie](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="b2cfd-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="b2cfd-126">Přidali jsme do databázového modelu sloupec, ale zobrazení na něm nevědí.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="b2cfd-127">Aktualizace zobrazení se změnami modelu</span><span class="sxs-lookup"><span data-stu-id="b2cfd-127">Update Views with Model Changes</span></span>

<span data-ttu-id="b2cfd-128">Existuje několik způsobů, jak můžeme aktualizovat naše šablony zobrazení tak, aby odpovídaly novému sloupci hodnocení.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="b2cfd-129">Vzhledem k tomu, že jsme tato zobrazení vytvořili pomocí dialogového okna Přidat zobrazení, můžeme je odstranit a znovu vytvořit.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="b2cfd-130">Obvykle ale lidé už provedli úpravy svých šablon zobrazení z počátečního generování vygenerovaného uživatelského rozhraní a budou chtít přidat nebo odstranit pole ručně, stejně jako u pole ID pro vytvoření.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="b2cfd-131">Otevřete šablonu \Views\Movies\Index.aspx a přidejte &lt;&gt;hodnocení&lt;/th&gt; do hlavičky tabulky filmů.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="b2cfd-132">Přidal (a) jsem mi svůj Žánr.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-132">I added mine after Genre.</span></span> <span data-ttu-id="b2cfd-133">Pak ve stejném umístění sloupce, ale dole, přidejte čáru pro výstup našeho nového hodnocení.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="b2cfd-134">Poslední šablona index. aspx bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="b2cfd-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="b2cfd-135">Pak otevřete šablonu \Views\Movies\Create.aspx a přidejte popisek a textové pole pro naši novou vlastnost hodnocení:</span><span class="sxs-lookup"><span data-stu-id="b2cfd-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="b2cfd-136">Naše finální šablona Create. aspx bude vypadat jako tato a změníme název našeho prohlížeče a sekundární &lt;H2&gt; title na něco, co je třeba "vytvořit film".</span><span class="sxs-lookup"><span data-stu-id="b2cfd-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="b2cfd-137">Spusťte aplikaci a nyní máte nové pole v databázi, které bylo přidáno na stránku vytvořit.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="b2cfd-138">Přidejte nový film – tentokrát se hodnocením a klikněte na vytvořit.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="b2cfd-139">[![vytvoření videa – Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="b2cfd-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="b2cfd-140">Po kliknutí na vytvořit se vám pošle na stránku index, kde nový film je uvedený ve sloupci nový hodnocení v databázi.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="b2cfd-141">[Seznam filmů ![– Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="b2cfd-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="b2cfd-142">Tento základní kurz vám umožní začít vytvářet řadiče a přidružit je k zobrazením a prodávat je s využitím pevně zakódovaných dat.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="b2cfd-143">Pak jsme vytvořili a navrhli databázi a umístili do ní nějaká data.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="b2cfd-144">Data z databáze jsme načetli a zobrazili v tabulce HTML.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="b2cfd-145">Pak jsme přidali formulář pro vytvoření, který uživateli umožňuje přidávat data do databáze přímo z webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="b2cfd-146">Přidali jsme ověření a pak jsme provedli ověřování pomocí JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="b2cfd-147">Nakonec jsme změnili databázi tak, aby obsahovala nový sloupec dat, a pak jsme aktualizovali naše dvě stránky a vytvořili a zobrazili Tato nová data.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="b2cfd-148">Nyní teď doporučujeme přejít na náš podrobný kurz pro[úložiště hudby "MVC Music](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" a také na mnoho videí a prostředků na [https://asp.net/mvc](https://asp.net/mvc) , abyste se dozvěděli ještě více o ASP.NET MVC!</span><span class="sxs-lookup"><span data-stu-id="b2cfd-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="b2cfd-149">Užijte si ji!</span><span class="sxs-lookup"><span data-stu-id="b2cfd-149">Enjoy!</span></span>

- <span data-ttu-id="b2cfd-150">Scott Hanselman – [http://hanselman.com](http://hanselman.com) a [@shanselman](http://twitter.com/shanselman) na Twitteru.</span><span class="sxs-lookup"><span data-stu-id="b2cfd-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b2cfd-151">Předchozí</span><span class="sxs-lookup"><span data-stu-id="b2cfd-151">Previous</span></span>](getting-started-with-mvc-part7.md)
