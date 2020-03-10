---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: Použití hodnot řetězce dotazu k filtrování dat s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639095"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="34204-104">Použití hodnot řetězce dotazu k filtrování dat s vazbami modelů a webovými formuláři</span><span class="sxs-lookup"><span data-stu-id="34204-104">Using query string values to filter data with model binding and web forms</span></span>

<span data-ttu-id="34204-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="34204-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="34204-106">Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="34204-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="34204-107">Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="34204-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="34204-108">Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.</span><span class="sxs-lookup"><span data-stu-id="34204-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="34204-109">V tomto kurzu se dozvíte, jak předat hodnotu v řetězci dotazu a použít tuto hodnotu k načtení dat prostřednictvím vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="34204-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="34204-110">Tento kurz sestaví na projektu vytvořeném v [předchozích](retrieving-data.md) částech řady.</span><span class="sxs-lookup"><span data-stu-id="34204-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="34204-111">Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB.</span><span class="sxs-lookup"><span data-stu-id="34204-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="34204-112">Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="34204-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="34204-113">Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="34204-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="34204-114">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="34204-114">What you'll build</span></span>

<span data-ttu-id="34204-115">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="34204-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="34204-116">Přidání nové stránky pro zobrazení zaregistrovaných kurzů pro studenta</span><span class="sxs-lookup"><span data-stu-id="34204-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="34204-117">Načte zaregistrované kurzy pro vybraného studenta na základě hodnoty v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="34204-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="34204-118">Přidání hypertextového odkazu s hodnotou řetězce dotazu ze zobrazení mřížky na novou stránku</span><span class="sxs-lookup"><span data-stu-id="34204-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="34204-119">Postup v tomto kurzu se podobá tomu, co jste provedli v předchozím [kurzu](sorting-paging-and-filtering-data.md) , chcete-li filtrovat zobrazené studenty na základě výběru uživatele v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="34204-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="34204-120">V tomto kurzu jste pomocí atributu **Control** v metodě SELECT určili, že hodnota parametru pochází z ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="34204-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="34204-121">V tomto kurzu použijete atribut **QueryString** v metodě SELECT k určení, že hodnota parametru pochází z řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="34204-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="34204-122">Přidání nové stránky pro zobrazení kurzů studenta</span><span class="sxs-lookup"><span data-stu-id="34204-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="34204-123">Přidejte nový webový formulář, který používá hlavní stránku Web. Master, a pojmenujte si **kurzy**stránky.</span><span class="sxs-lookup"><span data-stu-id="34204-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="34204-124">V souboru **kurzů. aspx** přidejte zobrazení mřížky pro zobrazení kurzů pro vybraného studenta.</span><span class="sxs-lookup"><span data-stu-id="34204-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="34204-125">Definování metody Select</span><span class="sxs-lookup"><span data-stu-id="34204-125">Define the select method</span></span>

<span data-ttu-id="34204-126">V **courses.aspx.cs**přidáte metodu Select s názvem, který jste zadali ve vlastnosti **SelectMethod** zobrazení mřížky.</span><span class="sxs-lookup"><span data-stu-id="34204-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="34204-127">V této metodě definujete dotaz pro načtení kurzů studenta a určíte, že parametr pochází z hodnoty řetězce dotazu se stejným názvem, jako má parametr.</span><span class="sxs-lookup"><span data-stu-id="34204-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="34204-128">Nejprve je třeba přidat následující příkazy **using** .</span><span class="sxs-lookup"><span data-stu-id="34204-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="34204-129">Pak do Courses.aspx.cs přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="34204-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="34204-130">Atribut QueryString znamená, že hodnota řetězce dotazu s názvem StudentID je automaticky přiřazena k parametru v této metodě.</span><span class="sxs-lookup"><span data-stu-id="34204-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="34204-131">Přidat hypertextový odkaz s hodnotou řetězce dotazu</span><span class="sxs-lookup"><span data-stu-id="34204-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="34204-132">V zobrazení mřížky na studenty. aspx přidáte pole hypertextového odkazu, které odkazuje na stránku nových kurzů.</span><span class="sxs-lookup"><span data-stu-id="34204-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="34204-133">Hypertextový odkaz bude obsahovat hodnotu řetězce dotazu s ID studenta.</span><span class="sxs-lookup"><span data-stu-id="34204-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="34204-134">V části studenty. aspx přidejte následující pole do sloupců zobrazení mřížky pod polem pro celkové kredity.</span><span class="sxs-lookup"><span data-stu-id="34204-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="34204-135">Spusťte aplikaci a Všimněte si, že zobrazení mřížky teď obsahuje odkaz kurzy.</span><span class="sxs-lookup"><span data-stu-id="34204-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![Přidat hypertextový odkaz](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="34204-137">Po kliknutí na jeden z odkazů se zobrazí zaregistrované kurzy tohoto studenta.</span><span class="sxs-lookup"><span data-stu-id="34204-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![Zobrazit kurzy](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="34204-139">Závěr</span><span class="sxs-lookup"><span data-stu-id="34204-139">Conclusion</span></span>

<span data-ttu-id="34204-140">V tomto kurzu jste přidali odkaz s hodnotou řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="34204-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="34204-141">Tuto hodnotu řetězce dotazu jste použili pro hodnotu parametru v metodě SELECT.</span><span class="sxs-lookup"><span data-stu-id="34204-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="34204-142">V dalším [kurzu](adding-business-logic-layer.md)přesunete kód ze souborů kódu na pozadí do vrstvy obchodní logiky a do vrstvy přístupu k datům.</span><span class="sxs-lookup"><span data-stu-id="34204-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34204-143">[Předchozí](integrating-jquery-ui.md)
> [Další](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="34204-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
