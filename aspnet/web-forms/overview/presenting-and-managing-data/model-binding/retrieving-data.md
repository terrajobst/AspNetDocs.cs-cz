---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Načtení a zobrazení dat ovládacím prvkem modelu vazby a webových formulářů | Dokumentace Microsoftu
author: Rick-Anderson
description: V této sérii kurzů ukazuje základní aspekty v použití vazby modelu s projektem aplikace webových formulářů ASP.NET. Data interakce díky vazby modelu další přímo-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 08cb65f9ef8f5c36070454e011f41554d81f333f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131530"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="e84f2-104">Načtení a zobrazení dat ovládacím prvkem vazby modelu a webové formuláře</span><span class="sxs-lookup"><span data-stu-id="e84f2-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="e84f2-105">V této sérii kurzů ukazuje základní aspekty v použití vazby modelu s projektem aplikace webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e84f2-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="e84f2-106">Vazby modelu díky dat interakce více přímočaré než pracující s daty objektů zdroje (například ObjectDataSource nebo SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="e84f2-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="e84f2-107">Tato série začíná úvodní materiály a přesune pokročilejších pojmech v budoucích kurzech.</span><span class="sxs-lookup"><span data-stu-id="e84f2-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="e84f2-108">Vzoru vazby modelu funguje s technologií přístupu všechny data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="e84f2-109">V tomto kurzu budete používat Entity Framework, ale můžete použít technologii přístup data, která je nejvíc známými.</span><span class="sxs-lookup"><span data-stu-id="e84f2-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="e84f2-110">Z ovládacího prvku serveru vázané na data, jako je například ovládacího prvku GridView, ListView, DetailsView nebo FormView zadáte názvy metod používaných pro výběr, aktualizace, odstraňování a vytváření data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="e84f2-111">V tomto kurzu můžete zadat hodnotu pro metody SelectMethod.</span><span class="sxs-lookup"><span data-stu-id="e84f2-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="e84f2-112">V rámci této metody pro načítání dat zadáte logiku.</span><span class="sxs-lookup"><span data-stu-id="e84f2-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="e84f2-113">V dalším kurzu nastavíte hodnoty pro UpdateMethod a DeleteMethod InsertMethod.</span><span class="sxs-lookup"><span data-stu-id="e84f2-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="e84f2-114">Je možné [Stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) dokončený projekt v C# nebo Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="e84f2-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="e84f2-115">Ke stažení kódu funguje pomocí sady Visual Studio 2012 a novější.</span><span class="sxs-lookup"><span data-stu-id="e84f2-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="e84f2-116">Používá šablonu Visual Studio 2012, která se trochu liší od sady Visual Studio 2017 šablonu uvedenou v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="e84f2-117">V tomto kurzu spustíte aplikaci v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e84f2-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="e84f2-118">Můžete také nasadit aplikaci do poskytovatele hostitelských služeb a zpřístupnit přes internet.</span><span class="sxs-lookup"><span data-stu-id="e84f2-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="e84f2-119">Společnost Microsoft nabízí bezplatné webových hostitelských služeb pro až 10 webových serverů ve</span><span class="sxs-lookup"><span data-stu-id="e84f2-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="e84f2-120">[Bezplatný zkušební účet Azure](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="e84f2-120">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="e84f2-121">Informace o tom, jak nasadit webový projekt sady Visual Studio do Azure App Service Web Apps, najdete v článku [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) řady.</span><span class="sxs-lookup"><span data-stu-id="e84f2-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="e84f2-122">Tento kurz také ukazuje způsob použití migrace Entity Framework Code First pro nasazení databáze SQL serveru do služby Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e84f2-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e84f2-123">V tomto kurzu použili verze softwaru</span><span class="sxs-lookup"><span data-stu-id="e84f2-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="e84f2-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="e84f2-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="e84f2-125">V tomto kurzu se také pracuje s Visual Studio 2012 a Visual Studio 2013, ale existují určité rozdíly v šabloně uživatelského rozhraní a projektu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="e84f2-126">Co budete vytvářet</span><span class="sxs-lookup"><span data-stu-id="e84f2-126">What you'll build</span></span>

<span data-ttu-id="e84f2-127">V tomto kurzu budete:</span><span class="sxs-lookup"><span data-stu-id="e84f2-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="e84f2-128">Vytváření datových objektů, které odpovídají vysoké školy se zúčastnili studenti zapsáni na kurzy</span><span class="sxs-lookup"><span data-stu-id="e84f2-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="e84f2-129">Vytváření databázových tabulek z objektů</span><span class="sxs-lookup"><span data-stu-id="e84f2-129">Build database tables from the objects</span></span>
* <span data-ttu-id="e84f2-130">Naplnění databáze testovací data</span><span class="sxs-lookup"><span data-stu-id="e84f2-130">Populate the database with test data</span></span>
* <span data-ttu-id="e84f2-131">Zobrazení dat v webového formuláře</span><span class="sxs-lookup"><span data-stu-id="e84f2-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="e84f2-132">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="e84f2-132">Create the project</span></span>

1. <span data-ttu-id="e84f2-133">Vytvořte v sadě Visual Studio 2017 **webová aplikace ASP.NET (.NET Framework)** projekt s názvem **ContosoUniversityModelBinding**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![Vytvoření projektu](retrieving-data/_static/image19.png)

2. <span data-ttu-id="e84f2-135">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-135">Select **OK**.</span></span> <span data-ttu-id="e84f2-136">Zobrazí se dialogové okno Vybrat šablonu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-136">The dialog box to select a template appears.</span></span>

   ![Vyberte webových formulářů](retrieving-data/_static/image3.png)

3. <span data-ttu-id="e84f2-138">Vyberte **webových formulářů** šablony.</span><span class="sxs-lookup"><span data-stu-id="e84f2-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="e84f2-139">V případě potřeby změňte ověření **jednotlivé uživatelské účty**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="e84f2-140">Vyberte **OK** pro vytvoření projektu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="e84f2-141">Upravit vzhled webu</span><span class="sxs-lookup"><span data-stu-id="e84f2-141">Modify site appearance</span></span>

   <span data-ttu-id="e84f2-142">Proveďte několik změn pro přizpůsobení vzhledu webu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="e84f2-143">Otevřete soubor Site.Master.</span><span class="sxs-lookup"><span data-stu-id="e84f2-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="e84f2-144">Změna názvu zobrazíte **Contoso University** a ne **My ASP.NET Application**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="e84f2-145">Změní celý text záhlaví z **název_aplikace** k **Contoso University**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="e84f2-146">Změna navigačních odkazů záhlaví na lokalitu odpovídající značky.</span><span class="sxs-lookup"><span data-stu-id="e84f2-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="e84f2-147">Odebrat odkazy na **o** a **kontakt** a místo toho propojit **studenty** stránky, které vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="e84f2-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="e84f2-148">Uložte Site.Master.</span><span class="sxs-lookup"><span data-stu-id="e84f2-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="e84f2-149">Přidejte webový formulář pro zobrazení údajů studentů</span><span class="sxs-lookup"><span data-stu-id="e84f2-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="e84f2-150">V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt, vyberte **přidat** a potom **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="e84f2-151">V **přidat novou položku** dialogové okno, vyberte **webové formuláře se stránkou předlohy** šablony a pojmenujte ho **Students.aspx**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![Vytvoření stránky](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="e84f2-153">Vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="e84f2-154">Webový formulář stránky předlohy, vyberte **Site.Master**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="e84f2-155">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="e84f2-156">Přidání datového modelu</span><span class="sxs-lookup"><span data-stu-id="e84f2-156">Add the data model</span></span>

<span data-ttu-id="e84f2-157">V **modely** složky, přidejte třídu pojmenovanou **UniversityModels.cs**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="e84f2-158">Klikněte pravým tlačítkem na **modely**vyberte **přidat**a potom **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="e84f2-159">Zobrazí se dialogové okno **Přidat novou položku**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="e84f2-160">V levé navigační nabídce vyberte **kód**, pak **třídy**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![Vytvoření tříd modelu](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="e84f2-162">Název třídy **UniversityModels.cs** a vyberte **přidat**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="e84f2-163">V tomto souboru, definujte `SchoolContext`, `Student`, `Enrollment`, a `Course` třídy následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="e84f2-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="e84f2-164">`SchoolContext` Třída odvozena z `DbContext`, který spravuje připojení k databázi a změny v datech.</span><span class="sxs-lookup"><span data-stu-id="e84f2-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="e84f2-165">V `Student` třídy, Všimněte si, že atributy použité `FirstName`, `LastName`, a `Year` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="e84f2-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="e84f2-166">Tento kurz používá pro ověření dat těchto atributů.</span><span class="sxs-lookup"><span data-stu-id="e84f2-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="e84f2-167">Pro zjednodušení kódu, jenom tyto vlastnosti jsou označeny ověření dat atributy.</span><span class="sxs-lookup"><span data-stu-id="e84f2-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="e84f2-168">V projektu aplikace skutečný platit atributů ověření pro všechny vlastnosti nutnosti ověření.</span><span class="sxs-lookup"><span data-stu-id="e84f2-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="e84f2-169">Uložte UniversityModels.cs.</span><span class="sxs-lookup"><span data-stu-id="e84f2-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="e84f2-170">Nastavení databáze, které jsou založeny na třídách</span><span class="sxs-lookup"><span data-stu-id="e84f2-170">Set up the database based on classes</span></span>

<span data-ttu-id="e84f2-171">Tento kurz používá [migrace Code First](https://docs.microsoft.com/en-us/ef/ef6/modeling/code-first/migrations/) k vytváření objektů a databázových tabulek.</span><span class="sxs-lookup"><span data-stu-id="e84f2-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/en-us/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="e84f2-172">Tyto tabulky ukládání informací o studenty a jejich přípravy.</span><span class="sxs-lookup"><span data-stu-id="e84f2-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="e84f2-173">Vyberte **nástroje** > **Správce balíčků NuGet** > **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="e84f2-174">V **Konzola správce balíčků**, spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="e84f2-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="e84f2-175">Pokud se příkaz úspěšně dokončí, zobrazí se zpráva s informacemi o tom, že migrace byla povolena.</span><span class="sxs-lookup"><span data-stu-id="e84f2-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![povolení migrace](retrieving-data/_static/image8.png)

      <span data-ttu-id="e84f2-177">Všimněte si, že soubor s názvem *Configuration.cs* se vytvořil.</span><span class="sxs-lookup"><span data-stu-id="e84f2-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="e84f2-178">`Configuration` Třída nemá `Seed` metodu, která můžete předvyplnit databázových tabulek s testovací data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="e84f2-179">Předběžnému naplnění databáze</span><span class="sxs-lookup"><span data-stu-id="e84f2-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="e84f2-180">Otevřete Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="e84f2-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="e84f2-181">Přidejte následující kód, který `Seed` metody.</span><span class="sxs-lookup"><span data-stu-id="e84f2-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="e84f2-182">Přidejte také `using` příkaz `ContosoUniversityModelBinding. Models` oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="e84f2-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="e84f2-183">Uložte Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="e84f2-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="e84f2-184">V konzole Správce balíčků, spusťte příkaz **přidat migrace počáteční**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="e84f2-185">Spusťte příkaz **aktualizace databáze**.</span><span class="sxs-lookup"><span data-stu-id="e84f2-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="e84f2-186">Pokud se zobrazí výjimka při spuštění tohoto příkazu `StudentID` a `CourseID` hodnoty mohou být odlišné od `Seed` hodnoty metody.</span><span class="sxs-lookup"><span data-stu-id="e84f2-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="e84f2-187">Otevřete tyto databázové tabulky a vyhledejte existující hodnoty pro `StudentID` a `CourseID`.</span><span class="sxs-lookup"><span data-stu-id="e84f2-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="e84f2-188">Přidejte tyto hodnoty do kódu pro synchronizace replik indexů `Enrollments` tabulky.</span><span class="sxs-lookup"><span data-stu-id="e84f2-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="e84f2-189">Přidání ovládacího prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="e84f2-189">Add a GridView control</span></span>

<span data-ttu-id="e84f2-190">Pomocí dat z databáze mají údaj vyplněný teď jste připravení tato data načíst a zobrazit je.</span><span class="sxs-lookup"><span data-stu-id="e84f2-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="e84f2-191">Otevřete Students.aspx.</span><span class="sxs-lookup"><span data-stu-id="e84f2-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="e84f2-192">Vyhledejte `MainContent` zástupný symbol.</span><span class="sxs-lookup"><span data-stu-id="e84f2-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="e84f2-193">V rámci tohoto zástupného symbolu, přidejte **GridView** ovládací prvek, který obsahuje tento kód.</span><span class="sxs-lookup"><span data-stu-id="e84f2-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="e84f2-194">Co je potřeba mějte na paměti:</span><span class="sxs-lookup"><span data-stu-id="e84f2-194">Things to note:</span></span>
   * <span data-ttu-id="e84f2-195">Všimněte si, že tato hodnota nastavena pro `SelectMethod` vlastnost v prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="e84f2-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="e84f2-196">Tato hodnota určuje metodu použitou k načtení dat prvku GridView, kterou vytvoříte v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="e84f2-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="e84f2-197">`ItemType` Je nastavena na `Student` třídy vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="e84f2-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="e84f2-198">Toto nastavení umožňuje odkazovat na vlastnosti třídy v kódu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="e84f2-199">Například `Student` třída má kolekci s názvem `Enrollments`.</span><span class="sxs-lookup"><span data-stu-id="e84f2-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="e84f2-200">Můžete použít `Item.Enrollments` načíst tuto kolekci a pak použít [syntaxi LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) načíst každý student je zaregistrovaná kredity součet.</span><span class="sxs-lookup"><span data-stu-id="e84f2-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="e84f2-201">Save Students.aspx.</span><span class="sxs-lookup"><span data-stu-id="e84f2-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="e84f2-202">Přidejte kód pro načtení dat</span><span class="sxs-lookup"><span data-stu-id="e84f2-202">Add code to retrieve data</span></span>

   <span data-ttu-id="e84f2-203">V souboru modelu code-behind Students.aspx přidejte zadaný pro metodu `SelectMethod` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="e84f2-204">Open Students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="e84f2-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="e84f2-205">Přidat `using` příkazů `ContosoUniversityModelBinding. Models` a `System.Data.Entity` obory názvů.</span><span class="sxs-lookup"><span data-stu-id="e84f2-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="e84f2-206">Přidejte metodu, která jste zadali pro `SelectMethod`:</span><span class="sxs-lookup"><span data-stu-id="e84f2-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="e84f2-207">`Include` Klauzule zvyšuje výkon dotazů, ale není povinné.</span><span class="sxs-lookup"><span data-stu-id="e84f2-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="e84f2-208">Bez `Include` klauzule, data jsou načítány s použitím [ *opožděné načtení*](https://en.wikipedia.org/wiki/Lazy_loading), což zahrnuje odesílání samostatný dotaz do databáze pokaždé, když týkající se data načítají.</span><span class="sxs-lookup"><span data-stu-id="e84f2-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="e84f2-209">S `Include` klauzule, data jsou načítány s použitím *předběžné načítání*, což znamená, že jeden databázový dotaz načte všechny související data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="e84f2-210">Pokud související data se nepoužívá, předběžné načítání je méně efektivní, protože je načtena další data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="e84f2-211">Ale v takovém případě předběžné načítání umožňuje nejlepší výkon, protože se pro každý záznam zobrazí související data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="e84f2-212">Další informace o aspektech týkajících se výkonu při načítání související data, najdete v článku **opožděné Eager a explicitní načítání souvisejících dat** tématu [čtení souvisejících dat s Entity Framework v ASP.NET Aplikace MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) článku.</span><span class="sxs-lookup"><span data-stu-id="e84f2-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="e84f2-213">Ve výchozím nastavení data seřazené podle hodnoty vlastnosti označeným jako klíč.</span><span class="sxs-lookup"><span data-stu-id="e84f2-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="e84f2-214">Můžete přidat `OrderBy` klauzule můžete zadat hodnotu různé řazení.</span><span class="sxs-lookup"><span data-stu-id="e84f2-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="e84f2-215">V tomto příkladu výchozí `StudentID` vlastnost se používá pro řazení.</span><span class="sxs-lookup"><span data-stu-id="e84f2-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="e84f2-216">V [řazení, stránkování a filtrování dat](sorting-paging-and-filtering-data.md) článku, uživatel je povolená a vyberte sloupec pro řazení.</span><span class="sxs-lookup"><span data-stu-id="e84f2-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="e84f2-217">Save Students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="e84f2-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="e84f2-218">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="e84f2-218">Run your application</span></span> 

<span data-ttu-id="e84f2-219">Spuštění webové aplikace (**F5**) a přejděte **studenty** stránku, která se zobrazí následující:</span><span class="sxs-lookup"><span data-stu-id="e84f2-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![zobrazení dat](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="e84f2-221">Automatické generování metody vazby modelu</span><span class="sxs-lookup"><span data-stu-id="e84f2-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="e84f2-222">Při práci prostřednictvím v této sérii kurzů, můžete jednoduše zkopírovat kód z kurzu do projektu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="e84f2-223">Jednou z nevýhod tohoto přístupu je, že nemusí se dozvěděli o funkci poskytovaný sadou Visual Studio k automatickému generování kódu pro metody vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="e84f2-224">Při práci na vašich vlastních projektů, automatické generování kódu můžete vám ušetří čas a nápovědu získáte představu o tom, jak implementovat operace.</span><span class="sxs-lookup"><span data-stu-id="e84f2-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="e84f2-225">Tato část popisuje funkci generování automatických kódu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="e84f2-226">Tato část je pouze informativní a neobsahuje žádný kód, který budete muset implementovat ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="e84f2-227">Při nastavování hodnoty pro `SelectMethod`, `UpdateMethod`, `InsertMethod`, nebo `DeleteMethod` vlastností v kódu značek, můžete vybrat **vytvořit novou metodu** možnost.</span><span class="sxs-lookup"><span data-stu-id="e84f2-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![Vytvořit metodu](retrieving-data/_static/image18.png)

<span data-ttu-id="e84f2-229">Visual Studio nejen vytvoří metodu v kódu s správný podpis, ale také vygeneruje implementační kód k provedení této operace.</span><span class="sxs-lookup"><span data-stu-id="e84f2-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="e84f2-230">Pokud nejprve nastavíte `ItemType` vlastnost před použitím automatické generování kódu funkce, které zadejte generovaný kód používá pro operace.</span><span class="sxs-lookup"><span data-stu-id="e84f2-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="e84f2-231">Například při nastavení `UpdateMethod` se automaticky vygeneruje vlastnost, následující kód:</span><span class="sxs-lookup"><span data-stu-id="e84f2-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="e84f2-232">Tento kód znovu, nemusí být přidány do projektu.</span><span class="sxs-lookup"><span data-stu-id="e84f2-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="e84f2-233">V dalším kurzu budete implementovat metody pro aktualizaci, odstranění a přidání nových dat.</span><span class="sxs-lookup"><span data-stu-id="e84f2-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="e84f2-234">Souhrn</span><span class="sxs-lookup"><span data-stu-id="e84f2-234">Summary</span></span>

<span data-ttu-id="e84f2-235">V tomto kurzu jste vytvořili tříd datových modelů a generují databázi z těchto tříd.</span><span class="sxs-lookup"><span data-stu-id="e84f2-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="e84f2-236">Naplní tabulek databáze se testovací data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-236">You filled the database tables with test data.</span></span> <span data-ttu-id="e84f2-237">Vazby modelu se používá k načtení dat z databáze a pak se zobrazují data v GridView.</span><span class="sxs-lookup"><span data-stu-id="e84f2-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="e84f2-238">V dalším [kurzu](updating-deleting-and-creating-data.md) v této sérii budou moci aktualizace, odstraňování a vytváření data.</span><span class="sxs-lookup"><span data-stu-id="e84f2-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e84f2-239">Next</span><span class="sxs-lookup"><span data-stu-id="e84f2-239">Next</span></span>](updating-deleting-and-creating-data.md)
