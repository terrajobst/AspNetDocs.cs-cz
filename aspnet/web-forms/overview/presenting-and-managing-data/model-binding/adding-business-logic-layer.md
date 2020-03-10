---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: Přidání vrstvy obchodní logiky do projektu, který používá vazby modelu a webové formuláře | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634832"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="25650-104">Přidání vrstvy obchodní logiky do projektu, který používá vazby modelu a webové formuláře</span><span class="sxs-lookup"><span data-stu-id="25650-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="25650-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="25650-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="25650-106">Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="25650-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="25650-107">Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="25650-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="25650-108">Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.</span><span class="sxs-lookup"><span data-stu-id="25650-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="25650-109">V tomto kurzu se dozvíte, jak použít vazbu modelu s vrstvou obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="25650-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="25650-110">Nastavíte člena OnCallingDataMethods k určení, že k volání metod dat se používá jiný objekt než aktuální stránka.</span><span class="sxs-lookup"><span data-stu-id="25650-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="25650-111">Tento kurz sestaví na projektu vytvořeném v [předchozích](retrieving-data.md) částech řady.</span><span class="sxs-lookup"><span data-stu-id="25650-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="25650-112">Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB.</span><span class="sxs-lookup"><span data-stu-id="25650-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="25650-113">Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="25650-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="25650-114">Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="25650-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="25650-115">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="25650-115">What you'll build</span></span>

<span data-ttu-id="25650-116">Vazba modelu umožňuje vložit kód interakce dat do souboru kódu na pozadí webové stránky nebo samostatné třídy obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="25650-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="25650-117">Předchozí kurzy ukázaly, jak používat soubory kódu na pozadí pro kód interakce dat.</span><span class="sxs-lookup"><span data-stu-id="25650-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="25650-118">Tento přístup funguje pro malé weby, ale může vést k opakování kódu a většímu obtížnosti při údržbě velkého webu.</span><span class="sxs-lookup"><span data-stu-id="25650-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="25650-119">Může být také velmi obtížné programově testovat kód, který se nachází v souboru kódu na pozadí, protože není k dispozici žádná abstraktní vrstva.</span><span class="sxs-lookup"><span data-stu-id="25650-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="25650-120">Chcete-li centralizovat kód interakce dat, můžete vytvořit vrstvu obchodní logiky, která obsahuje veškerou logiku pro interakci s daty.</span><span class="sxs-lookup"><span data-stu-id="25650-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="25650-121">Pak zavoláte vrstvu obchodní logiky z webových stránek.</span><span class="sxs-lookup"><span data-stu-id="25650-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="25650-122">V tomto kurzu se dozvíte, jak přesunout celý kód, který jste napsali v předchozích kurzech, do vrstvy obchodní logiky a potom použít tento kód ze stránek.</span><span class="sxs-lookup"><span data-stu-id="25650-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="25650-123">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="25650-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="25650-124">Přesunout kód ze souborů kódu na pozadí do vrstvy obchodní logiky</span><span class="sxs-lookup"><span data-stu-id="25650-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="25650-125">Změna ovládacích prvků vázaných na data pro volání metod ve vrstvě obchodní logiky</span><span class="sxs-lookup"><span data-stu-id="25650-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="25650-126">Vytvoření vrstvy obchodní logiky</span><span class="sxs-lookup"><span data-stu-id="25650-126">Create business logic layer</span></span>

<span data-ttu-id="25650-127">Nyní vytvoříte třídu, která je volána z webových stránek.</span><span class="sxs-lookup"><span data-stu-id="25650-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="25650-128">Metody v této třídě vypadají podobně jako metody, které jste použili v předchozích kurzech, a obsahují atributy zprostředkovatele hodnoty.</span><span class="sxs-lookup"><span data-stu-id="25650-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="25650-129">Nejprve přidejte novou složku s názvem **knihoven BLL**.</span><span class="sxs-lookup"><span data-stu-id="25650-129">First, add a new folder called **BLL**.</span></span>

![Přidat složku](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="25650-131">Ve složce knihoven BLL vytvořte novou třídu s názvem **SchoolBL.cs**.</span><span class="sxs-lookup"><span data-stu-id="25650-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="25650-132">Bude obsahovat všechny operace s daty, které byly původně uloženy v souborech kódu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="25650-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="25650-133">Metody jsou skoro stejné jako metody v souboru kódu na pozadí, ale budou zahrnovat nějaké změny.</span><span class="sxs-lookup"><span data-stu-id="25650-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="25650-134">Nejdůležitější změnou poznámky je, že již nespouštíte kód z instance třídy **Page** .</span><span class="sxs-lookup"><span data-stu-id="25650-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="25650-135">Třída Page obsahuje metodu **TryUpdateModel** a vlastnost **ModelState** .</span><span class="sxs-lookup"><span data-stu-id="25650-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="25650-136">Když je tento kód přesunut do vrstvy obchodní logiky, nebudete již mít instanci třídy Page, která by tyto členy volala.</span><span class="sxs-lookup"><span data-stu-id="25650-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="25650-137">Chcete-li se tomuto problému vyhnout, je nutné přidat parametr **ModelMethodContext** k jakékoli metodě, která přistupuje k TryUpdateModel nebo ModelState.</span><span class="sxs-lookup"><span data-stu-id="25650-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="25650-138">Tento parametr ModelMethodContext můžete použít k volání TryUpdateModel nebo načtení ModelState.</span><span class="sxs-lookup"><span data-stu-id="25650-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="25650-139">Pro tento nový parametr není nutné měnit cokoli na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="25650-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="25650-140">Nahraďte kód v SchoolBL.cs následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="25650-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="25650-141">Revidovat existující stránky a načíst data z vrstvy obchodní logiky</span><span class="sxs-lookup"><span data-stu-id="25650-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="25650-142">Nakonec budete převádět stránky students. aspx, AddStudent. aspx a kurzy. aspx z použití dotazů v souboru kódu na pozadí pro použití vrstvy obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="25650-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="25650-143">V souborech s kódem na pozadí pro studenty, AddStudent a kurzy odstraňte nebo odkomentujte následující metody dotazů:</span><span class="sxs-lookup"><span data-stu-id="25650-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="25650-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="25650-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="25650-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="25650-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="25650-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="25650-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="25650-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="25650-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="25650-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="25650-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="25650-149">V souboru kódu na pozadí teď nemusíte mít žádný kód, který se týká operací s daty.</span><span class="sxs-lookup"><span data-stu-id="25650-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="25650-150">Obslužná rutina události **OnCallingDataMethods** umožňuje určit objekt, který se má použít pro metody dat.</span><span class="sxs-lookup"><span data-stu-id="25650-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="25650-151">V části studenty. aspx přidejte hodnotu pro tuto obslužnou rutinu události a změňte názvy metod dat na názvy metod ve třídě obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="25650-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="25650-152">V souboru kódu na pozadí pro studenty. aspx Definujte obslužnou rutinu události pro událost CallingDataMethods.</span><span class="sxs-lookup"><span data-stu-id="25650-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="25650-153">V této obslužné rutině události zadáte třídu obchodní logiky pro datové operace.</span><span class="sxs-lookup"><span data-stu-id="25650-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="25650-154">V AddStudent. aspx udělejte podobné změny.</span><span class="sxs-lookup"><span data-stu-id="25650-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="25650-155">V kurzů. aspx udělejte podobné změny.</span><span class="sxs-lookup"><span data-stu-id="25650-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="25650-156">Spusťte aplikaci a Všimněte si, že všechny stránky fungují stejně jako dříve.</span><span class="sxs-lookup"><span data-stu-id="25650-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="25650-157">Logika ověřování funguje také správně.</span><span class="sxs-lookup"><span data-stu-id="25650-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="25650-158">Závěr</span><span class="sxs-lookup"><span data-stu-id="25650-158">Conclusion</span></span>

<span data-ttu-id="25650-159">V tomto kurzu znovu rozřadíte aplikaci tak, aby používala vrstvu pro přístup k datům a vrstvu obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="25650-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="25650-160">Určili jste, že datové ovládací prvky používají objekt, který není aktuální stránkou pro datové operace.</span><span class="sxs-lookup"><span data-stu-id="25650-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="25650-161">Předchozí</span><span class="sxs-lookup"><span data-stu-id="25650-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
