---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: Aktualizace, odstraňování a vytváření dat s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586644"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="e61f0-104">Aktualizace, odstraňování a vytváření dat pomocí vazeb modelů a webových formulářů</span><span class="sxs-lookup"><span data-stu-id="e61f0-104">Updating, deleting, and creating data with model binding and web forms</span></span>

<span data-ttu-id="e61f0-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e61f0-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e61f0-106">Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e61f0-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="e61f0-107">Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="e61f0-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="e61f0-108">Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.</span><span class="sxs-lookup"><span data-stu-id="e61f0-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="e61f0-109">V tomto kurzu se dozvíte, jak vytvářet, aktualizovat a odstraňovat data s vazbou modelu.</span><span class="sxs-lookup"><span data-stu-id="e61f0-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="e61f0-110">Nastavíte následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="e61f0-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="e61f0-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="e61f0-111">DeleteMethod</span></span>
> - <span data-ttu-id="e61f0-112">Určena metoda InsertMethod</span><span class="sxs-lookup"><span data-stu-id="e61f0-112">InsertMethod</span></span>
> - <span data-ttu-id="e61f0-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="e61f0-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="e61f0-114">Tyto vlastnosti obdrží název metody, která zpracovává odpovídající operaci.</span><span class="sxs-lookup"><span data-stu-id="e61f0-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="e61f0-115">V rámci této metody poskytnete logiku pro interakci s daty.</span><span class="sxs-lookup"><span data-stu-id="e61f0-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="e61f0-116">Tento kurz sestaví na projektu vytvořeném v první [části](retrieving-data.md) řady.</span><span class="sxs-lookup"><span data-stu-id="e61f0-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="e61f0-117">Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB.</span><span class="sxs-lookup"><span data-stu-id="e61f0-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="e61f0-118">Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e61f0-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="e61f0-119">Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="e61f0-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="e61f0-120">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="e61f0-120">What you'll build</span></span>

<span data-ttu-id="e61f0-121">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="e61f0-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="e61f0-122">Přidat šablony dynamických dat</span><span class="sxs-lookup"><span data-stu-id="e61f0-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="e61f0-123">Povolení aktualizace a odstraňování dat prostřednictvím metod vazby modelu</span><span class="sxs-lookup"><span data-stu-id="e61f0-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="e61f0-124">Použití pravidel ověřování dat – povolení vytvoření nového záznamu v databázi</span><span class="sxs-lookup"><span data-stu-id="e61f0-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="e61f0-125">Přidat šablony dynamických dat</span><span class="sxs-lookup"><span data-stu-id="e61f0-125">Add dynamic data templates</span></span>

<span data-ttu-id="e61f0-126">Pro zajištění nejlepšího uživatelského prostředí a minimalizaci opakování kódu budete používat šablony dynamických dat.</span><span class="sxs-lookup"><span data-stu-id="e61f0-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="e61f0-127">Předem připravené šablony dynamických dat můžete snadno integrovat do stávající lokality instalací balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="e61f0-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="e61f0-128">Z okna **Spravovat balíčky NuGet**nainstalujte **DynamicDataTemplatesCS**.</span><span class="sxs-lookup"><span data-stu-id="e61f0-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![šablony dynamických dat](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="e61f0-130">Všimněte si, že projekt teď obsahuje složku s názvem **DynamicData**.</span><span class="sxs-lookup"><span data-stu-id="e61f0-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="e61f0-131">V této složce se nacházejí šablony, které jsou automaticky aplikovány na dynamické ovládací prvky ve webových formulářích.</span><span class="sxs-lookup"><span data-stu-id="e61f0-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![Složka s dynamickými daty](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="e61f0-133">Povolit aktualizace a odstraňování</span><span class="sxs-lookup"><span data-stu-id="e61f0-133">Enable updating and deleting</span></span>

<span data-ttu-id="e61f0-134">Umožnění uživatelům aktualizovat a odstraňovat záznamy v databázi se velmi podobá procesu načítání dat.</span><span class="sxs-lookup"><span data-stu-id="e61f0-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="e61f0-135">Ve vlastnostech **UpdateMethod** a **DeleteMethod** zadáte názvy metod, které provádějí tyto operace.</span><span class="sxs-lookup"><span data-stu-id="e61f0-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="e61f0-136">Pomocí ovládacího prvku GridView můžete také zadat automatické generování tlačítek upravit a odstranit.</span><span class="sxs-lookup"><span data-stu-id="e61f0-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="e61f0-137">Následující zvýrazněný kód ukazuje přidání do kódu GridView.</span><span class="sxs-lookup"><span data-stu-id="e61f0-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="e61f0-138">V souboru kódu na pozadí přidejte příkaz using pro **System. data. entity. Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="e61f0-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="e61f0-139">Pak přidejte následující metody Update a DELETE.</span><span class="sxs-lookup"><span data-stu-id="e61f0-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="e61f0-140">Metoda **TryUpdateModel** aplikuje odpovídající hodnoty vázaných na data z webového formuláře na datovou položku.</span><span class="sxs-lookup"><span data-stu-id="e61f0-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="e61f0-141">Datová položka se načte na základě hodnoty parametru ID.</span><span class="sxs-lookup"><span data-stu-id="e61f0-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="e61f0-142">Vynutilit požadavky na ověření</span><span class="sxs-lookup"><span data-stu-id="e61f0-142">Enforce validation requirements</span></span>

<span data-ttu-id="e61f0-143">Atributy ověřování, které jste použili u vlastností FirstName, LastName a year ve třídě student, se automaticky vynutily při aktualizaci dat.</span><span class="sxs-lookup"><span data-stu-id="e61f0-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="e61f0-144">Ovládací prvky DynamicField přidávají validátory klientů a serverů na základě ověřovacích atributů.</span><span class="sxs-lookup"><span data-stu-id="e61f0-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="e61f0-145">Vlastnosti FirstName a LastName jsou povinné.</span><span class="sxs-lookup"><span data-stu-id="e61f0-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="e61f0-146">FirstName nesmí být delší než 20 znaků a příjmení nesmí být delší než 40 znaků.</span><span class="sxs-lookup"><span data-stu-id="e61f0-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="e61f0-147">Hodnota Year musí být platná pro výčet AcademicYear.</span><span class="sxs-lookup"><span data-stu-id="e61f0-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="e61f0-148">Pokud uživatel porušuje jeden z požadavků na ověření, aktualizace nepokračuje.</span><span class="sxs-lookup"><span data-stu-id="e61f0-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="e61f0-149">Chcete-li zobrazit chybovou zprávu, přidejte ovládací prvek ovládací souhrnu ověření nad prvek GridView.</span><span class="sxs-lookup"><span data-stu-id="e61f0-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="e61f0-150">Chcete-li zobrazit chyby ověřování z vazby modelu, nastavte vlastnost **ShowModelStateErrors** na **hodnotu true**.</span><span class="sxs-lookup"><span data-stu-id="e61f0-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="e61f0-151">Spusťte webovou aplikaci a aktualizujte a odstraňte všechny záznamy.</span><span class="sxs-lookup"><span data-stu-id="e61f0-151">Run the web application, and update and delete any of the records.</span></span>

![aktualizovat data](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="e61f0-153">Všimněte si, že když se v režimu úprav hodnota vlastnosti Year automaticky vykreslí jako rozevírací seznam.</span><span class="sxs-lookup"><span data-stu-id="e61f0-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="e61f0-154">Vlastnost year je hodnota výčtu a šablona dynamická data pro hodnotu výčtu Určuje rozevírací seznam pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="e61f0-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="e61f0-155">Tuto šablonu můžete najít tak, že otevřete **výčet\_upravit soubor. ascx** ve složce **DynamicData**/**FieldTemplates** .</span><span class="sxs-lookup"><span data-stu-id="e61f0-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="e61f0-156">Pokud zadáte platné hodnoty, aktualizace se úspěšně dokončí.</span><span class="sxs-lookup"><span data-stu-id="e61f0-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="e61f0-157">Pokud porušujete jeden z požadavků na ověření, aktualizace nebude pokračovat a zobrazí se chybová zpráva nad mřížkou.</span><span class="sxs-lookup"><span data-stu-id="e61f0-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![chybová zpráva](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="e61f0-159">Přidat nové záznamy</span><span class="sxs-lookup"><span data-stu-id="e61f0-159">Add new records</span></span>

<span data-ttu-id="e61f0-160">Ovládací prvek GridView nezahrnuje vlastnost **určena metoda InsertMethod** , a proto nemůže být použit pro přidání nového záznamu s vazbou modelu.</span><span class="sxs-lookup"><span data-stu-id="e61f0-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="e61f0-161">Vlastnost určena metoda InsertMethod můžete najít v ovládacích prvcích **FormView**, **DetailsView**nebo **ListView** .</span><span class="sxs-lookup"><span data-stu-id="e61f0-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="e61f0-162">V tomto kurzu použijete ovládací prvek FormView k přidání nového záznamu.</span><span class="sxs-lookup"><span data-stu-id="e61f0-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="e61f0-163">Nejdřív přidejte odkaz na novou stránku, kterou vytvoříte pro přidání nového záznamu.</span><span class="sxs-lookup"><span data-stu-id="e61f0-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="e61f0-164">Nad ovládací souhrnu ověření přidejte:</span><span class="sxs-lookup"><span data-stu-id="e61f0-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="e61f0-165">Nový odkaz se zobrazí v horní části obsahu pro stránku students.</span><span class="sxs-lookup"><span data-stu-id="e61f0-165">The new link will appear at the top of the content for the Students page.</span></span>

![nový odkaz](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="e61f0-167">Pak přidejte nový webový formulář pomocí stránky předlohy a pojmenujte ho **AddStudent**.</span><span class="sxs-lookup"><span data-stu-id="e61f0-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="e61f0-168">Jako hlavní stránku vyberte site. Master.</span><span class="sxs-lookup"><span data-stu-id="e61f0-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="e61f0-169">Pole pro přidání nového studenta vygenerujete pomocí ovládacího prvku **DynamicEntity** .</span><span class="sxs-lookup"><span data-stu-id="e61f0-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="e61f0-170">Ovládací prvek DynamicEntity vykreslí tyto upravitelné vlastnosti ve třídě určené vlastností ItemType.</span><span class="sxs-lookup"><span data-stu-id="e61f0-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="e61f0-171">Vlastnost StudentID byla označena atributem **[ScaffoldColumn (false)]** , takže není vykreslena.</span><span class="sxs-lookup"><span data-stu-id="e61f0-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="e61f0-172">Do zástupného textu MainContent stránky AddStudent přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="e61f0-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="e61f0-173">V souboru kódu na pozadí (AddStudent.aspx.cs) přidejte příkaz **using** pro obor názvů **ContosoUniversityModelBinding. Models** .</span><span class="sxs-lookup"><span data-stu-id="e61f0-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="e61f0-174">Pak přidejte následující metody pro určení způsobu vložení nového záznamu a obslužné rutiny události pro tlačítko Storno.</span><span class="sxs-lookup"><span data-stu-id="e61f0-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="e61f0-175">Uložte všechny změny.</span><span class="sxs-lookup"><span data-stu-id="e61f0-175">Save all of the changes.</span></span>

<span data-ttu-id="e61f0-176">Spusťte webovou aplikaci a vytvořte nového studenta.</span><span class="sxs-lookup"><span data-stu-id="e61f0-176">Run the web application and create a new student.</span></span>

![Přidat nového studenta](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="e61f0-178">Klikněte na **Vložit** a Všimněte si, že se vytvořil nový student.</span><span class="sxs-lookup"><span data-stu-id="e61f0-178">Click **Insert** and notice the new student has been created.</span></span>

![Zobrazit nového studenta](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="e61f0-180">Závěr</span><span class="sxs-lookup"><span data-stu-id="e61f0-180">Conclusion</span></span>

<span data-ttu-id="e61f0-181">V tomto kurzu jste povolili aktualizace, odstraňování a vytváření dat.</span><span class="sxs-lookup"><span data-stu-id="e61f0-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="e61f0-182">Pravidla ověřování se používají při interakci s daty.</span><span class="sxs-lookup"><span data-stu-id="e61f0-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="e61f0-183">V dalším [kurzu](sorting-paging-and-filtering-data.md) v této sérii budete umožňovat řazení, stránkování a filtrování dat.</span><span class="sxs-lookup"><span data-stu-id="e61f0-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e61f0-184">[Předchozí](retrieving-data.md)
> [Další](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="e61f0-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
