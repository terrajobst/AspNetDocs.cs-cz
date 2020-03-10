---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: Integrace DatePicker uživatelského rozhraní JQuery s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642476"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="c4d6d-104">Integrace DatePicker uživatelského rozhraní JQuery s vazbami modelů a webovými formuláři</span><span class="sxs-lookup"><span data-stu-id="c4d6d-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>

<span data-ttu-id="c4d6d-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c4d6d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c4d6d-106">Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="c4d6d-107">Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="c4d6d-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="c4d6d-108">Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="c4d6d-109">V tomto kurzu se dozvíte, jak přidat [widget DatePicker](http://jqueryui.com/datepicker/) uživatelského rozhraní jQuery do webového formuláře a použít vazbu modelu k aktualizaci databáze s vybranou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="c4d6d-110">Tento kurz sestaví na projektu vytvořeném v [první](retrieving-data.md) a [druhé](updating-deleting-and-creating-data.md) části řady.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="c4d6d-111">Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="c4d6d-112">Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="c4d6d-113">Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="c4d6d-114">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="c4d6d-114">What you'll build</span></span>

<span data-ttu-id="c4d6d-115">V tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="c4d6d-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="c4d6d-116">Přidejte do modelu vlastnost pro záznam data registrace studenta.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="c4d6d-117">Povolit uživateli vybrat datum registrace pomocí widgetu DatePicker uživatelského rozhraní JQuery</span><span class="sxs-lookup"><span data-stu-id="c4d6d-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="c4d6d-118">Vyhovět ověřovacím pravidlům pro datum zápisu</span><span class="sxs-lookup"><span data-stu-id="c4d6d-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="c4d6d-119">Pomůcka DatePicker uživatelského rozhraní JQuery umožňuje uživatelům snadno vybrat datum z kalendáře, který se zobrazí, když uživatel pracuje s polem.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="c4d6d-120">Použití tohoto widgetu může být vhodnější pro uživatele, než ruční zadání data.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="c4d6d-121">Integrace widgetu DatePicker do stránky, která používá vazbu modelu pro datové operace, vyžaduje jenom malé množství další práce.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="c4d6d-122">Přidat do modelu novou vlastnost</span><span class="sxs-lookup"><span data-stu-id="c4d6d-122">Add a new property to the model</span></span>

<span data-ttu-id="c4d6d-123">Nejprve do svého modelu studenta přidáte vlastnost **DateTime** a tuto změnu migrujete do databáze.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="c4d6d-124">Otevřete **UniversityModels.cs**a přidejte zvýrazněný kód do modelu studenta.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="c4d6d-125">**RangeAttribute** je součástí pro vymáhání ověřovacích pravidel pro vlastnost.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="c4d6d-126">Pro účely tohoto kurzu předpokládáme, že je společnost Contoso University založená na 1. lednu 2013 a proto jsou dřívější data registrace neplatná.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="c4d6d-127">V okně Správa balíčků přidejte migraci spuštěním příkazu **Add-Migration AddEnrollmentDate**.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="c4d6d-128">Všimněte si, že kód migrace přidá nový sloupec DateTime do tabulky student.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="c4d6d-129">Aby se shodovala s hodnotou, kterou jste zadali v RangeAttribute, přidejte výchozí hodnotu pro nový sloupec, jak je znázorněno v následujícím zvýrazněném kódu.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="c4d6d-130">Uložte změny do souboru migrace.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-130">Save your change to the migration file.</span></span>

<span data-ttu-id="c4d6d-131">Data nemusíte znovu naplnit.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-131">You do not need to seed the data again.</span></span> <span data-ttu-id="c4d6d-132">Proto ve složce migrace otevřete **Configuration.cs** a odeberte nebo Odkomentujte kód v metodě **osazení** .</span><span class="sxs-lookup"><span data-stu-id="c4d6d-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="c4d6d-133">Uložte soubor a zavřete ho.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-133">Save and close the file.</span></span>

<span data-ttu-id="c4d6d-134">Nyní spusťte příkaz **Update-Database**.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="c4d6d-135">Všimněte si, že sloupec teď v databázi existuje a všechny existující záznamy mají výchozí hodnotu pro EnrollmentDate.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="c4d6d-136">Přidat dynamické ovládací prvky pro datum registrace</span><span class="sxs-lookup"><span data-stu-id="c4d6d-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="c4d6d-137">Nyní přidáte ovládací prvky pro zobrazení a úpravu data registrace.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="c4d6d-138">V tomto okamžiku je hodnota upravována prostřednictvím textového pole.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="c4d6d-139">Později v tomto kurzu změníte textové pole na widget JQuery DatePicker.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="c4d6d-140">Nejprve je důležité si uvědomit, že nemusíte dělat žádné změny v souboru **AddStudent. aspx** .</span><span class="sxs-lookup"><span data-stu-id="c4d6d-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="c4d6d-141">Ovládací prvek DynamicEntity automaticky vykreslí novou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="c4d6d-142">Otevřete **studenty. aspx**a přidejte následující zvýrazněný kód.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="c4d6d-143">Spusťte aplikaci a Všimněte si, že můžete nastavit hodnotu pro datum zápisu zadáním data.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="c4d6d-144">Při přidávání nového studenta:</span><span class="sxs-lookup"><span data-stu-id="c4d6d-144">When adding a new student:</span></span>

![nastavit datum](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="c4d6d-146">Nebo úprava existující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="c4d6d-146">Or, editing an existing value:</span></span>

![Upravit datum](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="c4d6d-148">Zadání data funguje, ale nemusí se jednat o činnost zákazníka, kterou chcete poskytnout.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="c4d6d-149">V další části povolíte výběr data prostřednictvím kalendáře.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="c4d6d-150">Nainstalovat balíček NuGet pro práci s uživatelským rozhraním JQuery</span><span class="sxs-lookup"><span data-stu-id="c4d6d-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="c4d6d-151">Balíček NuGet **uživatelského rozhraní sady šťáv** umožňuje snadnou integraci WIDGETŮ uživatelského rozhraní jQuery do vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="c4d6d-152">Pokud chcete tento balíček použít, nainstalujte ho přes NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-152">To use this package, install it through NuGet.</span></span>

![Přidat uživatelské rozhraní šťávy](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="c4d6d-154">Verze rozhraní, kterou nainstalujete, může být v konfliktu s verzí JQuery ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="c4d6d-155">Než budete pokračovat v tomto kurzu, zkuste aplikaci spustit.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="c4d6d-156">Pokud dojde k chybě JavaScriptu, je nutné sjednotit verzi JQuery.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="c4d6d-157">Můžete buď přidat očekávanou verzi JQuery do složky Scripts (1.8.2 verze v době psaní tohoto kurzu), nebo v souboru site. Master zadat cestu k souboru JQuery.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="c4d6d-158">Přizpůsobit šablonu DateTime tak, aby zahrnovala widget DatePicker</span><span class="sxs-lookup"><span data-stu-id="c4d6d-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="c4d6d-159">Přidáte pomůcku DatePicker do šablony dynamických dat pro úpravu hodnoty DateTime.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="c4d6d-160">Přidáním widgetu do šablony se automaticky vykreslí ve formuláři pro přidání nového studenta a v zobrazení mřížky pro úpravy studentů.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="c4d6d-161">Otevřete **DateTime\_Edit. ascx**a přidejte následující zvýrazněný kód.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="c4d6d-162">V souboru kódu na pozadí nastavíte minimální a maximální datum pro DatePicker.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="c4d6d-163">Nastavením těchto hodnot zabráníte uživatelům přejít na neplatná data.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="c4d6d-164">Pokud je k dispozici, načtete minimální a maximální hodnoty z **RangeAttribute** ve vlastnosti DateTime.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="c4d6d-165">Otevřete **datový typ DateTime\_Edit.ascx.cs**a přidejte následující zvýrazněný kód na stránku\_načtení metody.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="c4d6d-166">Spusťte webovou aplikaci a přejděte na stránku AddStudent.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="c4d6d-167">Zadejte hodnoty pro pole a Všimněte si, že po kliknutí na textové pole pro datum zápisu se zobrazí kalendář.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![Výběr data](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="c4d6d-169">Vyberte datum a klikněte na tlačítko **Vložit**.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="c4d6d-170">RangeAttribute vynutil ověřování na serveru.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="c4d6d-171">Nastavením vlastnosti minDate v DatePicker použijete také ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="c4d6d-172">Kalendář neumožní uživateli přejít na datum před hodnotou minDate.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="c4d6d-173">Při úpravách záznamu v zobrazení mřížky se zobrazí také kalendář.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![DatePicker v prvku GridView](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="c4d6d-175">Závěr</span><span class="sxs-lookup"><span data-stu-id="c4d6d-175">Conclusion</span></span>

<span data-ttu-id="c4d6d-176">V tomto kurzu jste zjistili, jak začlenit widget JQuery do webového formuláře, který používá vazbu modelu.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="c4d6d-177">V dalším [kurzu](using-query-string-values-to-retrieve-data.md)budete při výběru dat používat hodnotu řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="c4d6d-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c4d6d-178">[Předchozí](sorting-paging-and-filtering-data.md)
> [Další](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="c4d6d-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
