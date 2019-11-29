---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Načítání a zobrazování dat s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 81cca22cb4752d071d2a68986ae9ac2bed737594
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633173"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="6d26b-104">Načítání a zobrazování dat s vazbami modelů a webovými formuláři</span><span class="sxs-lookup"><span data-stu-id="6d26b-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="6d26b-105">Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6d26b-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="6d26b-106">Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="6d26b-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="6d26b-107">Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.</span><span class="sxs-lookup"><span data-stu-id="6d26b-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="6d26b-108">Vzor vazby modelu funguje s libovolnou technologií pro přístup k datům.</span><span class="sxs-lookup"><span data-stu-id="6d26b-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="6d26b-109">V tomto kurzu použijete Entity Framework, ale můžete použít technologii pro přístup k datům, která je pro vás nejvhodnější.</span><span class="sxs-lookup"><span data-stu-id="6d26b-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="6d26b-110">Z ovládacího prvku vázaného na data, jako je ovládací prvek GridView, ListView, DetailsView nebo FormView, určíte názvy metod, které se mají použít pro výběr, aktualizaci, odstranění a vytváření dat.</span><span class="sxs-lookup"><span data-stu-id="6d26b-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="6d26b-111">V tomto kurzu zadáte hodnotu pro vlastnost SelectMethod.</span><span class="sxs-lookup"><span data-stu-id="6d26b-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="6d26b-112">V rámci této metody poskytnete logiku pro načítání dat.</span><span class="sxs-lookup"><span data-stu-id="6d26b-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="6d26b-113">V dalším kurzu nastavíte hodnoty pro UpdateMethod, DeleteMethod a určena metoda InsertMethod.</span><span class="sxs-lookup"><span data-stu-id="6d26b-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="6d26b-114">Celý projekt si můžete [Stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) v C# nebo Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="6d26b-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="6d26b-115">Kód ke stažení funguje v sadě Visual Studio 2012 a novějších.</span><span class="sxs-lookup"><span data-stu-id="6d26b-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="6d26b-116">Používá šablonu sady Visual Studio 2012, která je mírně odlišná než šablona sady Visual Studio 2017 uvedená v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="6d26b-117">V kurzu spustíte aplikaci v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d26b-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="6d26b-118">Aplikaci můžete nasadit také pro poskytovatele hostingu a zpřístupnit ji přes Internet.</span><span class="sxs-lookup"><span data-stu-id="6d26b-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="6d26b-119">Společnost Microsoft nabízí bezplatné webové hostování až pro 10 webů v</span><span class="sxs-lookup"><span data-stu-id="6d26b-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="6d26b-120">[bezplatný zkušební účet Azure](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="6d26b-120">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="6d26b-121">Informace o tom, jak nasadit webový projekt aplikace Visual Studio do Azure App Service Web Apps, naleznete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) Series.</span><span class="sxs-lookup"><span data-stu-id="6d26b-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="6d26b-122">Tento kurz také ukazuje, jak použít Migrace Entity Framework Code First k nasazení databáze SQL Server do Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6d26b-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6d26b-123">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="6d26b-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="6d26b-124">Microsoft Visual Studio 2017 nebo Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="6d26b-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="6d26b-125">Tento kurz také funguje se sadou Visual Studio 2012 a Visual Studio 2013, ale v uživatelském rozhraní a šabloně projektu jsou nějaké rozdíly.</span><span class="sxs-lookup"><span data-stu-id="6d26b-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="6d26b-126">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="6d26b-126">What you'll build</span></span>

<span data-ttu-id="6d26b-127">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="6d26b-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="6d26b-128">Vytváření datových objektů, které odrážejí vysokou univerzita s studenty registrovanými v kurzech</span><span class="sxs-lookup"><span data-stu-id="6d26b-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="6d26b-129">Vytváření tabulek databáze z objektů</span><span class="sxs-lookup"><span data-stu-id="6d26b-129">Build database tables from the objects</span></span>
* <span data-ttu-id="6d26b-130">Naplnit databázi testovacími daty</span><span class="sxs-lookup"><span data-stu-id="6d26b-130">Populate the database with test data</span></span>
* <span data-ttu-id="6d26b-131">Zobrazení dat ve webovém formuláři</span><span class="sxs-lookup"><span data-stu-id="6d26b-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="6d26b-132">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="6d26b-132">Create the project</span></span>

1. <span data-ttu-id="6d26b-133">V aplikaci Visual Studio 2017 vytvořte projekt **webové aplikace ASP.NET (.NET Framework)** s názvem **ContosoUniversityModelBinding**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![vytvořit projekt](retrieving-data/_static/image19.png)

2. <span data-ttu-id="6d26b-135">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-135">Select **OK**.</span></span> <span data-ttu-id="6d26b-136">Zobrazí se dialogové okno pro výběr šablony.</span><span class="sxs-lookup"><span data-stu-id="6d26b-136">The dialog box to select a template appears.</span></span>

   ![vybrat webové formuláře](retrieving-data/_static/image3.png)

3. <span data-ttu-id="6d26b-138">Vyberte šablonu **webových formulářů** .</span><span class="sxs-lookup"><span data-stu-id="6d26b-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="6d26b-139">V případě potřeby změňte ověřování na **jednotlivé uživatelské účty**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="6d26b-140">Vyberte **OK** a vytvořte projekt.</span><span class="sxs-lookup"><span data-stu-id="6d26b-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="6d26b-141">Upravit vzhled webu</span><span class="sxs-lookup"><span data-stu-id="6d26b-141">Modify site appearance</span></span>

   <span data-ttu-id="6d26b-142">Udělejte několik změn pro přizpůsobení vzhledu webu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="6d26b-143">Otevřete soubor Web. Master.</span><span class="sxs-lookup"><span data-stu-id="6d26b-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="6d26b-144">Změňte název, aby se zobrazila **Společnost Contoso University** a ne **Moje aplikace ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="6d26b-145">Změňte text záhlaví z **názvu aplikace** na **Univerzita Contoso**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="6d26b-146">Změňte navigační záhlaví odkazy na příslušné lokality.</span><span class="sxs-lookup"><span data-stu-id="6d26b-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="6d26b-147">Odeberte odkazy na **informace o** a **kontaktu** a místo toho odkaz na stránku **Students** , kterou vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="6d26b-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="6d26b-148">Uložte Web. Master.</span><span class="sxs-lookup"><span data-stu-id="6d26b-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="6d26b-149">Přidat webový formulář pro zobrazení dat studenta</span><span class="sxs-lookup"><span data-stu-id="6d26b-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="6d26b-150">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt, vyberte položku **Přidat** a **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="6d26b-151">V dialogovém okně **Přidat novou položku** vyberte **webový formulář se šablonou stránky předlohy** a pojmenujte ho **students. aspx**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![vytvořit stránku](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="6d26b-153">Vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="6d26b-154">Pro stránku předlohy webového formuláře vyberte **site. Master**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="6d26b-155">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="6d26b-156">Přidání datového modelu</span><span class="sxs-lookup"><span data-stu-id="6d26b-156">Add the data model</span></span>

<span data-ttu-id="6d26b-157">Ve složce **modely** přidejte třídu s názvem **UniversityModels.cs**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="6d26b-158">Klikněte pravým tlačítkem na **modely**, vyberte **Přidat**a **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="6d26b-159">Zobrazí se dialogové okno **Přidat novou položku** .</span><span class="sxs-lookup"><span data-stu-id="6d26b-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="6d26b-160">V levém navigačním panelu vyberte **kód**a pak **Třída**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![vytvořit třídu modelu](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="6d26b-162">Pojmenujte třídu **UniversityModels.cs** a vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="6d26b-163">V tomto souboru definujte `SchoolContext`, `Student`, `Enrollment`a třídy `Course` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="6d26b-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="6d26b-164">Třída `SchoolContext` je odvozena z `DbContext`, která spravuje připojení k databázi a změny v datech.</span><span class="sxs-lookup"><span data-stu-id="6d26b-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="6d26b-165">Ve třídě `Student` si všimněte atributů použitých pro vlastnosti `FirstName`, `LastName`a `Year`.</span><span class="sxs-lookup"><span data-stu-id="6d26b-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="6d26b-166">Tento kurz používá tyto atributy pro ověřování dat.</span><span class="sxs-lookup"><span data-stu-id="6d26b-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="6d26b-167">Chcete-li zjednodušit kód, jsou označeny pouze tyto vlastnosti s atributy ověřování dat.</span><span class="sxs-lookup"><span data-stu-id="6d26b-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="6d26b-168">Ve skutečném projektu byste použili atributy ověřování pro všechny vlastnosti, které vyžadují ověření.</span><span class="sxs-lookup"><span data-stu-id="6d26b-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="6d26b-169">Uložte UniversityModels.cs.</span><span class="sxs-lookup"><span data-stu-id="6d26b-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="6d26b-170">Nastavení databáze na základě tříd</span><span class="sxs-lookup"><span data-stu-id="6d26b-170">Set up the database based on classes</span></span>

<span data-ttu-id="6d26b-171">V tomto kurzu se používá [migrace Code First](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) k vytváření objektů a tabulek databáze.</span><span class="sxs-lookup"><span data-stu-id="6d26b-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="6d26b-172">Tyto tabulky obsahují informace o studentech a jejich kurzech.</span><span class="sxs-lookup"><span data-stu-id="6d26b-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="6d26b-173">Vyberte **nástroje** > **správce balíčků NuGet** > **konzole správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="6d26b-174">V **konzole správce balíčků**spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="6d26b-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="6d26b-175">Pokud se příkaz úspěšně dokončí, zobrazí se zpráva oznamující, že migrace byla povolena.</span><span class="sxs-lookup"><span data-stu-id="6d26b-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![Povolit migrace](retrieving-data/_static/image8.png)

      <span data-ttu-id="6d26b-177">Všimněte si, že byl vytvořen soubor s názvem *Configuration.cs* .</span><span class="sxs-lookup"><span data-stu-id="6d26b-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="6d26b-178">Třída `Configuration` má `Seed` metodu, která může předvyplnit tabulky databáze testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="6d26b-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="6d26b-179">Předem naplnit databázi</span><span class="sxs-lookup"><span data-stu-id="6d26b-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="6d26b-180">Otevřete Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="6d26b-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="6d26b-181">Do metody `Seed` přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="6d26b-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="6d26b-182">Přidejte také příkaz `using` pro obor názvů `ContosoUniversityModelBinding. Models`.</span><span class="sxs-lookup"><span data-stu-id="6d26b-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="6d26b-183">Uložte Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="6d26b-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="6d26b-184">V konzole správce balíčků spusťte příkaz **Add-Migration Initial**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="6d26b-185">Spusťte příkaz **Update-Database**.</span><span class="sxs-lookup"><span data-stu-id="6d26b-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="6d26b-186">Pokud při spuštění tohoto příkazu dojde k výjimce, hodnoty `StudentID` a `CourseID` se mohou lišit od hodnot metody `Seed`.</span><span class="sxs-lookup"><span data-stu-id="6d26b-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="6d26b-187">Otevřete tyto databázové tabulky a vyhledejte existující hodnoty pro `StudentID` a `CourseID`.</span><span class="sxs-lookup"><span data-stu-id="6d26b-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="6d26b-188">Přidejte tyto hodnoty do kódu pro osazení `Enrollments` tabulky.</span><span class="sxs-lookup"><span data-stu-id="6d26b-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="6d26b-189">Přidání ovládacího prvku GridView</span><span class="sxs-lookup"><span data-stu-id="6d26b-189">Add a GridView control</span></span>

<span data-ttu-id="6d26b-190">S vyplněnými daty databáze jste nyní připraveni načíst tato data a zobrazit je.</span><span class="sxs-lookup"><span data-stu-id="6d26b-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="6d26b-191">Otevřete studenty. aspx.</span><span class="sxs-lookup"><span data-stu-id="6d26b-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="6d26b-192">Vyhledejte zástupný symbol `MainContent`.</span><span class="sxs-lookup"><span data-stu-id="6d26b-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="6d26b-193">V rámci tohoto zástupného symbolu přidejte ovládací prvek **GridView** , který obsahuje tento kód.</span><span class="sxs-lookup"><span data-stu-id="6d26b-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="6d26b-194">Co je potřeba vzít v vědomí:</span><span class="sxs-lookup"><span data-stu-id="6d26b-194">Things to note:</span></span>
   * <span data-ttu-id="6d26b-195">Všimněte si hodnoty nastavené pro vlastnost `SelectMethod` v prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="6d26b-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="6d26b-196">Tato hodnota určuje metodu použitou k načtení dat GridView, které vytvoříte v následujícím kroku.</span><span class="sxs-lookup"><span data-stu-id="6d26b-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="6d26b-197">Vlastnost `ItemType` je nastavena na třídu `Student` vytvořenou dříve.</span><span class="sxs-lookup"><span data-stu-id="6d26b-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="6d26b-198">Toto nastavení umožňuje odkazovat na vlastnosti třídy v kódu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="6d26b-199">Například třída `Student` má kolekci s názvem `Enrollments`.</span><span class="sxs-lookup"><span data-stu-id="6d26b-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="6d26b-200">Můžete použít `Item.Enrollments` k načtení této kolekce a pak použít [syntaxi LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) k načtení součtu zaregistrovaných kreditů každého studenta.</span><span class="sxs-lookup"><span data-stu-id="6d26b-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="6d26b-201">Uložte studenty. aspx.</span><span class="sxs-lookup"><span data-stu-id="6d26b-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="6d26b-202">Přidat kód pro načtení dat</span><span class="sxs-lookup"><span data-stu-id="6d26b-202">Add code to retrieve data</span></span>

   <span data-ttu-id="6d26b-203">V souboru s kódem na pozadí pro studenty. aspx přidejte metodu určenou pro `SelectMethod` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="6d26b-204">Otevřete Students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="6d26b-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="6d26b-205">Přidejte `using` příkazy pro obory názvů `ContosoUniversityModelBinding. Models` a `System.Data.Entity`.</span><span class="sxs-lookup"><span data-stu-id="6d26b-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="6d26b-206">Přidejte metodu, kterou jste zadali pro `SelectMethod`:</span><span class="sxs-lookup"><span data-stu-id="6d26b-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="6d26b-207">Klauzule `Include` zvyšuje výkon dotazů, ale není vyžadována.</span><span class="sxs-lookup"><span data-stu-id="6d26b-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="6d26b-208">Bez klauzule `Include` se data načítají pomocí [*opožděného načítání*](https://en.wikipedia.org/wiki/Lazy_loading), což zahrnuje odeslání samostatného dotazu do databáze pokaždé, když se načtou související data.</span><span class="sxs-lookup"><span data-stu-id="6d26b-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="6d26b-209">S klauzulí `Include` se data načítají pomocí *načítání Eager*, což znamená, že jeden databázový dotaz načte všechna související data.</span><span class="sxs-lookup"><span data-stu-id="6d26b-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="6d26b-210">Pokud se související data nepoužívají, načítání Eager je méně efektivní, protože se načítají další data.</span><span class="sxs-lookup"><span data-stu-id="6d26b-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="6d26b-211">V tomto případě ale Eager načítání poskytuje nejlepší výkon, protože související data se zobrazují pro každý záznam.</span><span class="sxs-lookup"><span data-stu-id="6d26b-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="6d26b-212">Další informace o požadavcích na výkon při načítání souvisejících dat naleznete v části **opožděné, Eager a explicitní načítání souvisejících dat** v tématu [čtení souvisejících dat pomocí Entity Framework v článku aplikace ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) .</span><span class="sxs-lookup"><span data-stu-id="6d26b-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="6d26b-213">Ve výchozím nastavení jsou data řazena podle hodnot vlastnosti označené jako klíč.</span><span class="sxs-lookup"><span data-stu-id="6d26b-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="6d26b-214">Můžete přidat klauzuli `OrderBy` k určení jiné hodnoty řazení.</span><span class="sxs-lookup"><span data-stu-id="6d26b-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="6d26b-215">V tomto příkladu je použita výchozí vlastnost `StudentID` pro řazení.</span><span class="sxs-lookup"><span data-stu-id="6d26b-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="6d26b-216">V článku [řazení, stránkování a filtrování dat](sorting-paging-and-filtering-data.md) je povoleno, aby uživatel mohl vybrat sloupec pro řazení.</span><span class="sxs-lookup"><span data-stu-id="6d26b-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="6d26b-217">Uložte Students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="6d26b-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="6d26b-218">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="6d26b-218">Run your application</span></span> 

<span data-ttu-id="6d26b-219">Spusťte webovou aplikaci (**F5**) a přejděte na stránku **Students** , kde se zobrazí následující:</span><span class="sxs-lookup"><span data-stu-id="6d26b-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![Zobrazit data](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="6d26b-221">Automatické generování metod vazby modelu</span><span class="sxs-lookup"><span data-stu-id="6d26b-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="6d26b-222">Při práci prostřednictvím této série kurzů můžete jednoduše zkopírovat kód z kurzu do projektu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="6d26b-223">Ale jednou z nevýhod tohoto přístupu je, že se nemůžete seznámit s funkcí poskytovanými aplikací Visual Studio a automaticky vygenerovat kód pro metody vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="6d26b-224">Při práci na vašich vlastních projektech vám automatické generování kódu může ušetřit čas a pomohou vám získat představu o tom, jak implementovat operaci.</span><span class="sxs-lookup"><span data-stu-id="6d26b-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="6d26b-225">Tato část popisuje funkci automatického generování kódu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="6d26b-226">Tato část je pouze informativní a neobsahuje žádný kód, který je třeba implementovat do projektu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="6d26b-227">Při nastavování hodnoty pro `SelectMethod`, `UpdateMethod`, `InsertMethod`nebo `DeleteMethod` vlastností v kódu značky můžete vybrat možnost **vytvořit novou metodu** .</span><span class="sxs-lookup"><span data-stu-id="6d26b-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![Vytvoření metody](retrieving-data/_static/image18.png)

<span data-ttu-id="6d26b-229">Visual Studio nevytvoří pouze metodu v kódu na pozadí se správným podpisem, ale také generuje implementační kód pro provedení operace.</span><span class="sxs-lookup"><span data-stu-id="6d26b-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="6d26b-230">Pokud nejprve nastavíte vlastnost `ItemType` před použitím funkce Automatické generování kódu, vygenerovaný kód použije tento typ pro operace.</span><span class="sxs-lookup"><span data-stu-id="6d26b-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="6d26b-231">Například při nastavování vlastnosti `UpdateMethod` se automaticky vygeneruje následující kód:</span><span class="sxs-lookup"><span data-stu-id="6d26b-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="6d26b-232">Tento kód znovu není nutné přidat do projektu.</span><span class="sxs-lookup"><span data-stu-id="6d26b-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="6d26b-233">V dalším kurzu implementujete metody pro aktualizaci, odstranění a přidávání nových dat.</span><span class="sxs-lookup"><span data-stu-id="6d26b-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="6d26b-234">Přehled</span><span class="sxs-lookup"><span data-stu-id="6d26b-234">Summary</span></span>

<span data-ttu-id="6d26b-235">V tomto kurzu jste vytvořili třídy datového modelu a z těchto tříd vygenerovali databázi.</span><span class="sxs-lookup"><span data-stu-id="6d26b-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="6d26b-236">Vyplnili jste tabulky databáze testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="6d26b-236">You filled the database tables with test data.</span></span> <span data-ttu-id="6d26b-237">Použili jste vazbu modelu k načtení dat z databáze a následně jste zobrazili data v prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="6d26b-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="6d26b-238">V dalším [kurzu](updating-deleting-and-creating-data.md) tohoto seriálu povolíte aktualizaci, odstraňování a vytváření dat.</span><span class="sxs-lookup"><span data-stu-id="6d26b-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6d26b-239">Next</span><span class="sxs-lookup"><span data-stu-id="6d26b-239">Next</span></span>](updating-deleting-and-creating-data.md)
