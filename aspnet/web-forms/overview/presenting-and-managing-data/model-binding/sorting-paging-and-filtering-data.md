---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: Řazení, stránkování a filtrování dat pomocí vazeb modelů a webových formulářů | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548060"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="0cd13-104">Řazení, stránkování a filtrování dat pomocí vazeb modelů a webových formulářů</span><span class="sxs-lookup"><span data-stu-id="0cd13-104">Sorting, paging, and filtering data with model binding and web forms</span></span>

<span data-ttu-id="0cd13-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0cd13-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0cd13-106">Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0cd13-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="0cd13-107">Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="0cd13-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="0cd13-108">Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.</span><span class="sxs-lookup"><span data-stu-id="0cd13-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="0cd13-109">V tomto kurzu se dozvíte, jak přidat řazení, stránkování a filtrování dat prostřednictvím vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="0cd13-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="0cd13-110">Tento kurz sestaví na projektu vytvořeném v první [části](retrieving-data.md) řady.</span><span class="sxs-lookup"><span data-stu-id="0cd13-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="0cd13-111">Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB.</span><span class="sxs-lookup"><span data-stu-id="0cd13-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="0cd13-112">Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="0cd13-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="0cd13-113">Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="0cd13-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="0cd13-114">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="0cd13-114">What you'll build</span></span>

<span data-ttu-id="0cd13-115">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="0cd13-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="0cd13-116">Povolit řazení a stránkování dat</span><span class="sxs-lookup"><span data-stu-id="0cd13-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="0cd13-117">Povolit filtrování dat na základě výběru uživatelem</span><span class="sxs-lookup"><span data-stu-id="0cd13-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="0cd13-118">Přidat řazení</span><span class="sxs-lookup"><span data-stu-id="0cd13-118">Add sorting</span></span>

<span data-ttu-id="0cd13-119">Povolení řazení v prvku GridView je velmi snadné.</span><span class="sxs-lookup"><span data-stu-id="0cd13-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="0cd13-120">V souboru student. aspx stačí nastavit **AllowSorting** na **hodnotu true** v prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="0cd13-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="0cd13-121">Pro každý sloupec není nutné nastavovat hodnotu **SortExpression** , protože pole DataField je automaticky použito.</span><span class="sxs-lookup"><span data-stu-id="0cd13-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="0cd13-122">Prvek GridView upraví dotaz tak, aby zahrnoval řazení dat podle vybrané hodnoty.</span><span class="sxs-lookup"><span data-stu-id="0cd13-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="0cd13-123">Zvýrazněný kód ukazuje přidání, které je třeba provést, aby bylo možné řazení povolit.</span><span class="sxs-lookup"><span data-stu-id="0cd13-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="0cd13-124">Spuštění webové aplikace a testování záznamů studentů podle hodnot v různých sloupcích.</span><span class="sxs-lookup"><span data-stu-id="0cd13-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![Seřadit studenty](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="0cd13-126">Přidat stránkování</span><span class="sxs-lookup"><span data-stu-id="0cd13-126">Add paging</span></span>

<span data-ttu-id="0cd13-127">Povolení stránkování je také velmi snadné.</span><span class="sxs-lookup"><span data-stu-id="0cd13-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="0cd13-128">V prvku GridView nastavte vlastnost **li AllowPaging nastavena** na **hodnotu true** a nastavte vlastnost **PageSize** na počet záznamů, které chcete zobrazit na každé stránce.</span><span class="sxs-lookup"><span data-stu-id="0cd13-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="0cd13-129">V tomto kurzu ho můžete nastavit na 4.</span><span class="sxs-lookup"><span data-stu-id="0cd13-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="0cd13-130">Spusťte webovou aplikaci a Všimněte si, že nyní jsou záznamy rozděleny na více stránek s maximálně 4 záznamy zobrazenými na jedné stránce.</span><span class="sxs-lookup"><span data-stu-id="0cd13-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![Přidat stránkování](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="0cd13-132">Odložené provádění dotazů vylepšuje efektivitu aplikace.</span><span class="sxs-lookup"><span data-stu-id="0cd13-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="0cd13-133">Místo načtení celé datové sady prvek GridView upraví dotaz tak, aby načetl pouze záznamy pro aktuální stránku.</span><span class="sxs-lookup"><span data-stu-id="0cd13-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="0cd13-134">Filtrovat záznamy podle výběru uživatele</span><span class="sxs-lookup"><span data-stu-id="0cd13-134">Filter records by user selection</span></span>

<span data-ttu-id="0cd13-135">Vazba modelu přidá několik atributů, které umožňují určit, jak nastavit hodnotu pro parametr v metodě vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="0cd13-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="0cd13-136">Tyto atributy jsou v oboru názvů **System. Web. ModelBinding** .</span><span class="sxs-lookup"><span data-stu-id="0cd13-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="0cd13-137">Patří mezi ně:</span><span class="sxs-lookup"><span data-stu-id="0cd13-137">They include:</span></span>

- <span data-ttu-id="0cd13-138">Řízení</span><span class="sxs-lookup"><span data-stu-id="0cd13-138">Control</span></span>
- <span data-ttu-id="0cd13-139">Soubor cookie</span><span class="sxs-lookup"><span data-stu-id="0cd13-139">Cookie</span></span>
- <span data-ttu-id="0cd13-140">Formulář</span><span class="sxs-lookup"><span data-stu-id="0cd13-140">Form</span></span>
- <span data-ttu-id="0cd13-141">Profil</span><span class="sxs-lookup"><span data-stu-id="0cd13-141">Profile</span></span>
- <span data-ttu-id="0cd13-142">Řetězec dotazu</span><span class="sxs-lookup"><span data-stu-id="0cd13-142">QueryString</span></span>
- <span data-ttu-id="0cd13-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="0cd13-143">RouteData</span></span>
- <span data-ttu-id="0cd13-144">Relace</span><span class="sxs-lookup"><span data-stu-id="0cd13-144">Session</span></span>
- <span data-ttu-id="0cd13-145">Profilu</span><span class="sxs-lookup"><span data-stu-id="0cd13-145">UserProfile</span></span>
- <span data-ttu-id="0cd13-146">ViewState</span><span class="sxs-lookup"><span data-stu-id="0cd13-146">ViewState</span></span>

<span data-ttu-id="0cd13-147">V tomto kurzu použijete hodnotu ovládacího prvku k filtrování, které záznamy se zobrazí v prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="0cd13-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="0cd13-148">Přidáte atribut **Control** do metody dotazu, kterou jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="0cd13-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="0cd13-149">V [pozdějším](using-query-string-values-to-retrieve-data.md) kurzu použijete atribut **QueryString** na parametr a určíte tak, že hodnota parametru pochází z hodnoty řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="0cd13-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="0cd13-150">Nejdřív nad ovládací souhrnu ověření přidejte rozevírací seznam pro filtrování, které studenty se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="0cd13-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="0cd13-151">V souboru kódu na pozadí upravte metodu Select pro příjem hodnoty z ovládacího prvku a nastavte název parametru na název ovládacího prvku, který poskytuje hodnotu.</span><span class="sxs-lookup"><span data-stu-id="0cd13-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="0cd13-152">Pro vyřešení atributu ovládacího prvku je nutné přidat příkaz **using** pro obor názvů **System. Web. ModelBinding** .</span><span class="sxs-lookup"><span data-stu-id="0cd13-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="0cd13-153">Následující kód ukazuje znovu vypracovanou metodu Select pro filtrování vrácených dat na základě hodnoty rozevíracího seznamu.</span><span class="sxs-lookup"><span data-stu-id="0cd13-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="0cd13-154">Přidání atributu ovládacího prvku před parametr určuje, že hodnota pro tento parametr pochází z ovládacího prvku se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="0cd13-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="0cd13-155">Pokud chcete filtrovat seznam studentů, spusťte webovou aplikaci a v rozevíracím seznamu vyberte jiné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="0cd13-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![filtrovat studenty](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="0cd13-157">Závěr</span><span class="sxs-lookup"><span data-stu-id="0cd13-157">Conclusion</span></span>

<span data-ttu-id="0cd13-158">V tomto kurzu jste povolili řazení a stránkování dat.</span><span class="sxs-lookup"><span data-stu-id="0cd13-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="0cd13-159">Také jste povolili filtrování dat podle hodnoty ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="0cd13-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="0cd13-160">V dalším [kurzu](integrating-jquery-ui.md) vylepšíte uživatelské rozhraní integrací WIDGETU uživatelského rozhraní jQuery do šablony dynamických dat.</span><span class="sxs-lookup"><span data-stu-id="0cd13-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0cd13-161">[Předchozí](updating-deleting-and-creating-data.md)
> [Další](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="0cd13-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
