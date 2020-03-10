---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Vytvoření databáze | Microsoft Docs
author: microsoft
description: Krok 2 ukazuje postup vytvoření databáze obsahující všechna data o večeři a protokolu RSVP pro naši aplikaci NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581002"
---
# <a name="create-a-database"></a><span data-ttu-id="4438c-103">Vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="4438c-103">Create a Database</span></span>

<span data-ttu-id="4438c-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4438c-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="4438c-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="4438c-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="4438c-106">Toto je krok 2 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="4438c-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="4438c-107">Krok 2 ukazuje postup vytvoření databáze obsahující všechna data o večeři a protokolu RSVP pro naši aplikaci NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="4438c-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="4438c-108">Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.</span><span class="sxs-lookup"><span data-stu-id="4438c-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="4438c-109">NerdDinner krok 2: vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="4438c-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="4438c-110">K uložení všech dat o večeři a protokolu RSVP pro naši aplikaci NerdDinner budeme používat databázi.</span><span class="sxs-lookup"><span data-stu-id="4438c-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="4438c-111">Následující postup ukazuje vytvoření databáze pomocí bezplatné SQL Server Express edice (kterou můžete snadno nainstalovat pomocí verze V2 [Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4438c-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="4438c-112">Veškerý kód, který zapíšeme, bude pracovat s SQL Server Express i s úplným SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4438c-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="4438c-113">Vytvoření nové databáze SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="4438c-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="4438c-114">Začneme tak, že kliknete pravým tlačítkem na náš webový projekt a pak vyberete příkaz nabídky **přidat&gt;nové položky** :</span><span class="sxs-lookup"><span data-stu-id="4438c-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="4438c-115">Tím se zobrazí dialogové okno Přidat novou položku v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4438c-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="4438c-116">Vyfiltrujeme podle kategorie "data" a vyberete šablonu položky "SQL Server Database":</span><span class="sxs-lookup"><span data-stu-id="4438c-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="4438c-117">Pojmenujte SQL Server Express databázi, kterou chceme vytvořit "NerdDinner. mdf" a stiskněte OK.</span><span class="sxs-lookup"><span data-stu-id="4438c-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="4438c-118">Visual Studio se pak zeptá, jestli chceme přidat tento soubor do našeho adresáře \app\_dat (což je adresář, který se už nastavil pomocí seznamů ACL pro čtení i zápis):</span><span class="sxs-lookup"><span data-stu-id="4438c-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="4438c-119">Klikneme na Ano a vytvoří se nová databáze, která se přidá do našich Průzkumník řešení:</span><span class="sxs-lookup"><span data-stu-id="4438c-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="4438c-120">Vytváření tabulek v rámci naší databáze</span><span class="sxs-lookup"><span data-stu-id="4438c-120">Creating Tables within our Database</span></span>

<span data-ttu-id="4438c-121">Nyní máme novou prázdnou databázi.</span><span class="sxs-lookup"><span data-stu-id="4438c-121">We now have a new empty database.</span></span> <span data-ttu-id="4438c-122">Pojďme do ní přidat některé tabulky.</span><span class="sxs-lookup"><span data-stu-id="4438c-122">Let's add some tables to it.</span></span>

<span data-ttu-id="4438c-123">Provedeme to tak, že přejdete na okno karty Průzkumník serveru v rámci sady Visual Studio, které nám umožní spravovat databáze a servery.</span><span class="sxs-lookup"><span data-stu-id="4438c-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="4438c-124">SQL Server Express databáze uložené ve složce dat\_\app v naší aplikaci se automaticky zobrazí v Průzkumník serveru.</span><span class="sxs-lookup"><span data-stu-id="4438c-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="4438c-125">Volitelně můžete použít ikonu "připojit k databázi" v horní části okna Průzkumník serveru k přidání dalších databází SQL Server (místní i vzdálené) do seznamu současně:</span><span class="sxs-lookup"><span data-stu-id="4438c-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="4438c-126">Do naší databáze NerdDinner přidáme dvě tabulky – jednu pro uložení našich večeře a druhou pro sledování přijetí protokolu RSVP do nich.</span><span class="sxs-lookup"><span data-stu-id="4438c-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="4438c-127">Nové tabulky můžeme vytvořit tak, že kliknete pravým tlačítkem na složku Tables v naší databázi a zvolíte příkaz nabídky Přidat novou tabulku:</span><span class="sxs-lookup"><span data-stu-id="4438c-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="4438c-128">Otevře se Návrhář tabulky, který nám umožní nakonfigurovat schéma naší tabulky.</span><span class="sxs-lookup"><span data-stu-id="4438c-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="4438c-129">V tabulce "večeře" přidáme 10 sloupců dat:</span><span class="sxs-lookup"><span data-stu-id="4438c-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="4438c-130">Chceme, aby sloupec "DinnerID" byl pro tabulku jedinečným primárním klíčem.</span><span class="sxs-lookup"><span data-stu-id="4438c-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="4438c-131">To můžeme nakonfigurovat tak, že kliknete pravým tlačítkem na sloupec "DinnerID" a vyberete položku nabídky "nastavit primární klíč":</span><span class="sxs-lookup"><span data-stu-id="4438c-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="4438c-132">Kromě toho, že DinnerID primární klíč, chceme také nakonfigurovat jako sloupec identity, jehož hodnota se automaticky zvyšuje, protože se do tabulky přidají nové řádky dat (to znamená, že první vložená řada večeře bude mít DinnerID 1, druhý vložený řádek. bude mít DinnerIDu 2 atd.</span><span class="sxs-lookup"><span data-stu-id="4438c-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="4438c-133">To můžeme udělat tak, že vyberete sloupec "DinnerID" a potom pomocí editoru "vlastnosti sloupce" nastavíte vlastnost "(je identity)" na sloupci na hodnotu "Ano".</span><span class="sxs-lookup"><span data-stu-id="4438c-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="4438c-134">Použijeme standardní výchozí hodnoty identity (počínaje 1 a přírůstkem 1 na každém novém řádku večeře):</span><span class="sxs-lookup"><span data-stu-id="4438c-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="4438c-135">Tuto tabulku pak uložíte zadáním kombinace kláves CTRL + S nebo pomocí příkazu **File-&gt;Save** .</span><span class="sxs-lookup"><span data-stu-id="4438c-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="4438c-136">Tím se zobrazí výzva k pojmenování tabulky.</span><span class="sxs-lookup"><span data-stu-id="4438c-136">This will prompt us to name the table.</span></span> <span data-ttu-id="4438c-137">Budeme pojmenovat "večeře":</span><span class="sxs-lookup"><span data-stu-id="4438c-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="4438c-138">Naše nová tabulka večeře se pak zobrazí v naší databázi v Průzkumníku serveru.</span><span class="sxs-lookup"><span data-stu-id="4438c-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="4438c-139">Pak zopakujeme výše uvedené kroky a vytvoříme tabulku "RSVP".</span><span class="sxs-lookup"><span data-stu-id="4438c-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="4438c-140">Tato tabulka má 3 sloupce.</span><span class="sxs-lookup"><span data-stu-id="4438c-140">This table with have 3 columns.</span></span> <span data-ttu-id="4438c-141">Nastavíme sloupec RsvpID jako primární klíč a zároveň nastavíme sloupec identity:</span><span class="sxs-lookup"><span data-stu-id="4438c-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="4438c-142">Budeme ho ukládat a dát mu název "RSVP".</span><span class="sxs-lookup"><span data-stu-id="4438c-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="4438c-143">Nastavení vztahu cizího klíče mezi tabulkami</span><span class="sxs-lookup"><span data-stu-id="4438c-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="4438c-144">Teď máme v naší databázi dvě tabulky.</span><span class="sxs-lookup"><span data-stu-id="4438c-144">We now have two tables within our database.</span></span> <span data-ttu-id="4438c-145">Náš poslední krok pro návrh schématu bude nastavit relaci 1:1 mezi těmito dvěma tabulkami – aby bylo možné přidružit každý řádek večeře k nule nebo více řádkům protokolu RSVP, které se na něj vztahují.</span><span class="sxs-lookup"><span data-stu-id="4438c-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="4438c-146">To provedeme tak, že nakonfigurujete sloupec "DinnerID" tabulky protokolu RSVP tak, aby měl relaci cizího klíče se sloupcem "DinnerID" v tabulce "večeřes".</span><span class="sxs-lookup"><span data-stu-id="4438c-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="4438c-147">Pokud to chcete udělat, otevřete tabulku protokolu RSVP v Návrháři tabulky tak, že na ni dvakrát kliknete v Průzkumníku serveru.</span><span class="sxs-lookup"><span data-stu-id="4438c-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="4438c-148">Pak vyberete sloupec "DinnerID", klikněte pravým tlačítkem myši a vyberte relaci... příkaz místní nabídky:</span><span class="sxs-lookup"><span data-stu-id="4438c-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="4438c-149">Zobrazí se dialogové okno, které můžeme použít k nastavení vztahů mezi tabulkami:</span><span class="sxs-lookup"><span data-stu-id="4438c-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="4438c-150">Kliknutím na tlačítko Přidat přidáte novou relaci do dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="4438c-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="4438c-151">Po přidání relace rozbalíme uzel "tabulky a specifikace sloupce" stromové zobrazení v mřížce vlastností na pravé straně dialogového okna a potom kliknete na "...". tlačítko napravo od něj:</span><span class="sxs-lookup"><span data-stu-id="4438c-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="4438c-152">Kliknutí na... tlačítko zobrazí další dialog, který nám umožní určit, které tabulky a sloupce jsou součástí relace, a také nám umožnit pojmenovat relaci.</span><span class="sxs-lookup"><span data-stu-id="4438c-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="4438c-153">V tabulce s primárními klíči se změní na "večeře" a jako primární klíč vyberete sloupec "DinnerID" v tabulce večeře.</span><span class="sxs-lookup"><span data-stu-id="4438c-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="4438c-154">Naše tabulka protokolu RSVP bude tabulka cizího klíče a protokol RSVP. Sloupec DinnerID bude přidružen jako cizí klíč:</span><span class="sxs-lookup"><span data-stu-id="4438c-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="4438c-155">Každý řádek v tabulce protokolu RSVP se teď přidruží k řádku v tabulce večeře.</span><span class="sxs-lookup"><span data-stu-id="4438c-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="4438c-156">SQL Server zachovává referenční integritu pro nás – a zabráníme přidání nového řádku protokolu RSVP, pokud neodkazuje na platný řádek večeře.</span><span class="sxs-lookup"><span data-stu-id="4438c-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="4438c-157">Tím se také zabrání v odstranění řádku večeře, pokud se na něj stále vztahují řádky protokolu RSVP.</span><span class="sxs-lookup"><span data-stu-id="4438c-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="4438c-158">Přidávání dat do tabulek</span><span class="sxs-lookup"><span data-stu-id="4438c-158">Adding Data to our Tables</span></span>

<span data-ttu-id="4438c-159">Pojďme to dokončit přidáním ukázkových dat do tabulky večeři.</span><span class="sxs-lookup"><span data-stu-id="4438c-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="4438c-160">Do tabulky můžeme přidat data tak, že na ni kliknete pravým tlačítkem myši v rámci Průzkumník serveru a vyberete příkaz Zobrazit data tabulky:</span><span class="sxs-lookup"><span data-stu-id="4438c-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="4438c-161">Přidáme pár řádků dat o večeři, které můžeme později použít při zahájení implementace aplikace:</span><span class="sxs-lookup"><span data-stu-id="4438c-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="4438c-162">Další krok</span><span class="sxs-lookup"><span data-stu-id="4438c-162">Next Step</span></span>

<span data-ttu-id="4438c-163">Dokončili jsme vytváření naší databáze.</span><span class="sxs-lookup"><span data-stu-id="4438c-163">We've finished creating our database.</span></span> <span data-ttu-id="4438c-164">Nyní vytvoříme třídy modelů, které můžeme použít k dotazování a aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="4438c-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4438c-165">[Předchozí](create-a-new-aspnet-mvc-project.md)
> [Další](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="4438c-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
