---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 3 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní v ASP.NET MV...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538904"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="40dfd-103">Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 3</span><span class="sxs-lookup"><span data-stu-id="40dfd-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>

<span data-ttu-id="40dfd-104">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="40dfd-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="40dfd-105">V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní ve webové aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="40dfd-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="working-with-complex-types"></a><span data-ttu-id="40dfd-106">Práce se složitými typy</span><span class="sxs-lookup"><span data-stu-id="40dfd-106">Working with Complex Types</span></span>

<span data-ttu-id="40dfd-107">V této části vytvoříte třídu adres a naučíte se, jak vytvořit šablonu pro její zobrazení.</span><span class="sxs-lookup"><span data-stu-id="40dfd-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="40dfd-108">Ve složce *modely* vytvořte nový soubor třídy s názvem *Person.cs* , kam umístíte dva typy: třídu `Person` a třídu `Address`.</span><span class="sxs-lookup"><span data-stu-id="40dfd-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="40dfd-109">Třída `Person` bude obsahovat vlastnost, která je zadána jako `Address`.</span><span class="sxs-lookup"><span data-stu-id="40dfd-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="40dfd-110">Typ `Address` je komplexní typ, což znamená, že se nejedná o jeden z předdefinovaných typů jako `int`, `string`nebo `double`.</span><span class="sxs-lookup"><span data-stu-id="40dfd-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="40dfd-111">Místo toho má několik vlastností.</span><span class="sxs-lookup"><span data-stu-id="40dfd-111">Instead, it has several properties.</span></span> <span data-ttu-id="40dfd-112">Kód pro nové třídy vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="40dfd-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="40dfd-113">V kontroleru `Movie` přidejte následující akci `PersonDetail` k zobrazení instance osoby:</span><span class="sxs-lookup"><span data-stu-id="40dfd-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="40dfd-114">Pak přidejte následující kód do kontroleru `Movie` k naplnění modelu `Person` pomocí některých ukázkových dat:</span><span class="sxs-lookup"><span data-stu-id="40dfd-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="40dfd-115">Otevřete soubor *Views\Movies\PersonDetail.cshtml* a přidejte následující kód pro zobrazení `PersonDetail`.</span><span class="sxs-lookup"><span data-stu-id="40dfd-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="40dfd-116">Stisknutím kombinace kláves CTRL + F5 spusťte aplikaci a přejděte na *video/PersonDetail*.</span><span class="sxs-lookup"><span data-stu-id="40dfd-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="40dfd-117">Zobrazení `PersonDetail` neobsahuje komplexní typ `Address`, jak vidíte na tomto snímku obrazovky.</span><span class="sxs-lookup"><span data-stu-id="40dfd-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="40dfd-118">(Není zobrazena žádná adresa.)</span><span class="sxs-lookup"><span data-stu-id="40dfd-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="40dfd-119">Data modelu `Address` nejsou zobrazena, protože se jedná o komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="40dfd-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="40dfd-120">Chcete-li zobrazit informace o adrese, otevřete znovu soubor *Views\Movies\PersonDetail.cshtml* a přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="40dfd-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="40dfd-121">Úplný kód pro zobrazení `PersonDetail` nyní vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="40dfd-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="40dfd-122">Spusťte aplikaci znovu a zobrazte `PersonDetail` zobrazení.</span><span class="sxs-lookup"><span data-stu-id="40dfd-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="40dfd-123">Zobrazí se nyní informace o adrese:</span><span class="sxs-lookup"><span data-stu-id="40dfd-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="40dfd-124">Vytvoření šablony pro komplexní typ</span><span class="sxs-lookup"><span data-stu-id="40dfd-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="40dfd-125">V této části vytvoříte šablonu, která bude použita k vykreslení `Address` komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="40dfd-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="40dfd-126">Když vytvoříte šablonu pro typ `Address`, ASP.NET MVC ji může automaticky použít k formátování modelu adresy kdekoli v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="40dfd-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="40dfd-127">To poskytuje způsob, jak řídit vykreslování `Address`ho typu z jediného místa v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="40dfd-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="40dfd-128">Ve složce *Views\Shared\DisplayTemplates* vytvořte s názvem **adresa**částečného zobrazení se silným typem:</span><span class="sxs-lookup"><span data-stu-id="40dfd-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="40dfd-129">Klikněte na **Přidat**a pak otevřete nový soubor *Views\Shared\DisplayTemplates\Address.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="40dfd-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="40dfd-130">Nové zobrazení obsahuje následující generovaný kód:</span><span class="sxs-lookup"><span data-stu-id="40dfd-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="40dfd-131">Spusťte aplikaci a zobrazte `PersonDetail` zobrazení.</span><span class="sxs-lookup"><span data-stu-id="40dfd-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="40dfd-132">Tentokrát `Address` šablona, kterou jste právě vytvořili, slouží k zobrazení `Address` komplexního typu, takže zobrazení vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="40dfd-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="40dfd-133">Shrnutí: způsoby určení formátu a šablony zobrazení modelu</span><span class="sxs-lookup"><span data-stu-id="40dfd-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="40dfd-134">Viděli jste, že můžete zadat formát nebo šablonu pro vlastnost modelu pomocí následujících přístupů:</span><span class="sxs-lookup"><span data-stu-id="40dfd-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="40dfd-135">Použití atributu `DisplayFormat` na vlastnost v modelu.</span><span class="sxs-lookup"><span data-stu-id="40dfd-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="40dfd-136">Například následující kód způsobí, že se datum zobrazí bez času:</span><span class="sxs-lookup"><span data-stu-id="40dfd-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="40dfd-137">Použití atributu [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) na vlastnost v modelu a určení datového typu.</span><span class="sxs-lookup"><span data-stu-id="40dfd-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="40dfd-138">Například následující kód způsobí, že se datum zobrazí bez času.</span><span class="sxs-lookup"><span data-stu-id="40dfd-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="40dfd-139">Pokud aplikace obsahuje šablonu *Date. cshtml* ve složce *Views\Shared\DisplayTemplates* nebo ve složce *Views\Movies\DisplayTemplates* , bude tato šablona použita k vykreslení vlastnosti `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="40dfd-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="40dfd-140">Jinak integrovaný systém ASP.NET šablonování zobrazí vlastnost jako datum.</span><span class="sxs-lookup"><span data-stu-id="40dfd-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="40dfd-141">Vytvoření šablony zobrazení ve složce *Views\Shared\DisplayTemplates* nebo ve složce *Views\Movies\DisplayTemplates* , jejíž název se shoduje s datovým typem, který chcete formátovat.</span><span class="sxs-lookup"><span data-stu-id="40dfd-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="40dfd-142">Například jste viděli, že *Views\Shared\DisplayTemplates\DateTime.cshtml* byl použit k vykreslení vlastností `DateTime` v modelu, bez přidání atributu do modelu a bez přidání kódu do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="40dfd-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="40dfd-143">Pomocí atributu [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) v modelu zadejte šablonu pro zobrazení vlastnosti modelu.</span><span class="sxs-lookup"><span data-stu-id="40dfd-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="40dfd-144">Explicitně přidejte název šablony zobrazení do volání [HTML. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="40dfd-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="40dfd-145">Přístup, který použijete, závisí na tom, co musíte udělat ve své aplikaci.</span><span class="sxs-lookup"><span data-stu-id="40dfd-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="40dfd-146">Ke smíchání těchto přístupů není Neběžné, abyste získali přesně takový druh formátování, které potřebujete.</span><span class="sxs-lookup"><span data-stu-id="40dfd-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="40dfd-147">V další části převedete ozubené kolečky a přejdete z přizpůsobení způsobu, jakým se zobrazí data pro přizpůsobení způsobu jejich zadávání.</span><span class="sxs-lookup"><span data-stu-id="40dfd-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="40dfd-148">DatePicker jQuery se připojíte k zobrazením pro úpravy v aplikaci, aby bylo možné zadat data uhlazený způsobem.</span><span class="sxs-lookup"><span data-stu-id="40dfd-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="40dfd-149">[Předchozí](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [Další](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="40dfd-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
