---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 8 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585909"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="be77a-104">Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 8</span><span class="sxs-lookup"><span data-stu-id="be77a-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>

<span data-ttu-id="be77a-105">tím, že [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="be77a-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="be77a-106">Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="be77a-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="be77a-107">Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="be77a-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="be77a-108">Formátování a ověření dat pomocí funkce dynamických dat</span><span class="sxs-lookup"><span data-stu-id="be77a-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="be77a-109">V předchozím kurzu jste implementovali uložené procedury.</span><span class="sxs-lookup"><span data-stu-id="be77a-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="be77a-110">V tomto kurzu se dozvíte, jak může funkce dynamických dat poskytovat následující výhody:</span><span class="sxs-lookup"><span data-stu-id="be77a-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="be77a-111">Pole jsou automaticky formátována pro zobrazení na základě jejich datového typu.</span><span class="sxs-lookup"><span data-stu-id="be77a-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="be77a-112">Pole se automaticky ověřují na základě jejich datového typu.</span><span class="sxs-lookup"><span data-stu-id="be77a-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="be77a-113">Do datového modelu můžete přidat metadata pro přizpůsobení formátování a chování ověřování.</span><span class="sxs-lookup"><span data-stu-id="be77a-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="be77a-114">Když to uděláte, můžete přidat pravidla formátování a ověřování na jednom místě a automaticky se použije všude, kde máte přístup k polím pomocí dynamických ovládacích prvků dat.</span><span class="sxs-lookup"><span data-stu-id="be77a-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="be77a-115">Chcete-li zjistit, jak to funguje, změňte ovládací prvky, které slouží k zobrazení a úpravě polí na stávající stránce *students. aspx* , a přidejte metadata formátování a ověření do polí název a datum pro `Student` typ entity.</span><span class="sxs-lookup"><span data-stu-id="be77a-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="be77a-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="be77a-117">Používání ovládacích prvků DynamicField a objektu DynamicControl</span><span class="sxs-lookup"><span data-stu-id="be77a-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="be77a-118">Otevřete stránku *students. aspx* a v ovládacím prvku `StudentsGridView` nahraďte **název** a **Datum registrace** `TemplateField` prvky následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="be77a-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="be77a-119">Tento kód používá ovládací prvky `DynamicControl` místo `TextBox` a ovládací prvky `Label` v poli Šablona názvu studenta a pro datum zápisu používá ovládací prvek `DynamicField`.</span><span class="sxs-lookup"><span data-stu-id="be77a-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="be77a-120">Nejsou zadány žádné formátovací řetězce.</span><span class="sxs-lookup"><span data-stu-id="be77a-120">No format strings are specified.</span></span>

<span data-ttu-id="be77a-121">Přidejte ovládací prvek `ValidationSummary` za ovládací prvek `StudentsGridView`.</span><span class="sxs-lookup"><span data-stu-id="be77a-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="be77a-122">V ovládacím prvku `SearchGridView` nahraďte značky pro sloupce **název** a **Datum zápisu** stejně jako v ovládacím prvku `StudentsGridView`, s výjimkou vynechat prvek `EditItemTemplate`.</span><span class="sxs-lookup"><span data-stu-id="be77a-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="be77a-123">Prvek `Columns` ovládacího prvku `SearchGridView` nyní obsahuje následující kód:</span><span class="sxs-lookup"><span data-stu-id="be77a-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="be77a-124">Otevřete *students.aspx.cs* a přidejte následující příkaz `using`:</span><span class="sxs-lookup"><span data-stu-id="be77a-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="be77a-125">Přidejte obslužnou rutinu pro událost `Init` stránky:</span><span class="sxs-lookup"><span data-stu-id="be77a-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="be77a-126">Tento kód určuje, že dynamická data budou poskytovat formátování a ověřování v těchto ovládacích prvcích vázaných na data pro pole `Student` entitu.</span><span class="sxs-lookup"><span data-stu-id="be77a-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="be77a-127">Pokud se zobrazí chybová zpráva podobná následujícímu příkladu při spuštění stránky, obvykle znamená, že jste zapomněli volat metodu `EnableDynamicData` v `Page_Init`:</span><span class="sxs-lookup"><span data-stu-id="be77a-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="be77a-128">Spusťte stránku.</span><span class="sxs-lookup"><span data-stu-id="be77a-128">Run the page.</span></span>

<span data-ttu-id="be77a-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="be77a-130">Ve sloupci **Datum zápisu** se zobrazí čas společně s datem, protože typ vlastnosti je `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="be77a-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="be77a-131">Později to opravíte.</span><span class="sxs-lookup"><span data-stu-id="be77a-131">You'll fix that later.</span></span>

<span data-ttu-id="be77a-132">Prozatím si všimněte, že dynamická data automaticky poskytují základní ověření dat.</span><span class="sxs-lookup"><span data-stu-id="be77a-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="be77a-133">Klikněte například na **Upravit**, zrušte zaškrtnutí políčka datum, klikněte na **aktualizovat**a uvidíte, že dynamická data automaticky vytvoří toto povinné pole, protože v datovém modelu se nepovoluje hodnota null.</span><span class="sxs-lookup"><span data-stu-id="be77a-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="be77a-134">Stránka zobrazuje hvězdičku za polem a chybovou zprávu v ovládacím prvku `ValidationSummary`:</span><span class="sxs-lookup"><span data-stu-id="be77a-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="be77a-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="be77a-136">Můžete vynechat ovládací prvek `ValidationSummary`, protože můžete také umístit ukazatel myši na hvězdičku, aby se zobrazila chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="be77a-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="be77a-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="be77a-138">Dynamická data také ověří, že data zadaná v poli **Datum registrace** jsou platné datum:</span><span class="sxs-lookup"><span data-stu-id="be77a-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="be77a-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="be77a-140">Jak vidíte, jedná se o obecnou chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="be77a-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="be77a-141">V další části se dozvíte, jak přizpůsobit zprávy a také pravidla pro ověřování a formátování.</span><span class="sxs-lookup"><span data-stu-id="be77a-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="be77a-142">Přidání metadat do datového modelu</span><span class="sxs-lookup"><span data-stu-id="be77a-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="be77a-143">Obvykle chcete přizpůsobit funkce poskytované dynamickými daty.</span><span class="sxs-lookup"><span data-stu-id="be77a-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="be77a-144">Můžete například změnit způsob zobrazení dat a obsah chybových zpráv.</span><span class="sxs-lookup"><span data-stu-id="be77a-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="be77a-145">Pravidla pro ověřování dat se obvykle přizpůsobují tak, aby poskytovala více funkcí, než jaká dynamická data poskytuje automaticky na základě datových typů.</span><span class="sxs-lookup"><span data-stu-id="be77a-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="be77a-146">K tomu je třeba vytvořit dílčí třídy, které odpovídají typům entit.</span><span class="sxs-lookup"><span data-stu-id="be77a-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="be77a-147">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **ContosoUniversity** , vyberte možnost **Přidat odkaz**a přidejte odkaz na `System.ComponentModel.DataAnnotations`.</span><span class="sxs-lookup"><span data-stu-id="be77a-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="be77a-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="be77a-149">Ve složce *dal* vytvořte nový soubor třídy, pojmenujte ho *student.cs*a v něm nahraďte kód šablony následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="be77a-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="be77a-150">Tento kód vytvoří pro entitu `Student` částečnou třídu.</span><span class="sxs-lookup"><span data-stu-id="be77a-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="be77a-151">Atribut `MetadataType` aplikovaný na tuto částečnou třídu identifikuje třídu, kterou používáte k určení metadat.</span><span class="sxs-lookup"><span data-stu-id="be77a-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="be77a-152">Třída metadat může mít libovolný název, ale použití názvu entity plus "metadata" je běžný postup.</span><span class="sxs-lookup"><span data-stu-id="be77a-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="be77a-153">Atributy použité pro vlastnosti třídy metadata určují formátování, ověřování, pravidla a chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="be77a-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="be77a-154">Zde uvedené atributy budou mít následující výsledky:</span><span class="sxs-lookup"><span data-stu-id="be77a-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="be77a-155">`EnrollmentDate` se zobrazí jako datum (bez času).</span><span class="sxs-lookup"><span data-stu-id="be77a-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="be77a-156">Obě pole název musí mít délku 25 nebo méně znaků a je k dispozici vlastní chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="be77a-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="be77a-157">Obě pole jména jsou povinná a vlastní chybová zpráva je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="be77a-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="be77a-158">Spusťte znovu stránku *students. aspx* a uvidíte, že se data nyní zobrazují bez časů:</span><span class="sxs-lookup"><span data-stu-id="be77a-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="be77a-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="be77a-160">Upravte řádek a pokuste se vymazat hodnoty v polích název.</span><span class="sxs-lookup"><span data-stu-id="be77a-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="be77a-161">Hvězdičky indikující chyby pole se zobrazí hned po opuštění pole, než kliknete na tlačítko **aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="be77a-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="be77a-162">Po kliknutí na možnost **aktualizovat**se na stránce zobrazí text chybové zprávy, kterou jste zadali.</span><span class="sxs-lookup"><span data-stu-id="be77a-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="be77a-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="be77a-164">Zkuste zadat názvy, které jsou delší než 25 znaků, klikněte na **aktualizovat**a na stránce se zobrazí text chybové zprávy, kterou jste zadali.</span><span class="sxs-lookup"><span data-stu-id="be77a-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="be77a-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="be77a-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="be77a-166">Teď, když jste nastavili tato pravidla formátování a ověřování v metadatech datového modelu, pravidla se automaticky použijí na všech stránkách, které zobrazují nebo povolují změny těchto polí, pokud použijete ovládací prvky `DynamicControl` nebo `DynamicField`.</span><span class="sxs-lookup"><span data-stu-id="be77a-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="be77a-167">Tím se sníží množství redundantního kódu, který musíte napsat, což usnadňuje programování a testování, a zajišťuje, aby formátování a ověřování dat bylo konzistentní v celé aplikaci.</span><span class="sxs-lookup"><span data-stu-id="be77a-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="be77a-168">Další informace</span><span class="sxs-lookup"><span data-stu-id="be77a-168">More Information</span></span>

<span data-ttu-id="be77a-169">Tím se tato série kurzů dokončí Začínáme Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="be77a-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="be77a-170">Další materiály, které vám pomůžou naučit se používat Entity Framework, najdete [v prvním kurzu v další Entity Framework řadě kurzů](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) nebo na následujících webech:</span><span class="sxs-lookup"><span data-stu-id="be77a-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="be77a-171">Nejčastější dotazy k Entity Framework</span><span class="sxs-lookup"><span data-stu-id="be77a-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="be77a-172">Blog týmu Entity Framework</span><span class="sxs-lookup"><span data-stu-id="be77a-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="be77a-173">Entity Framework v knihovně MSDN</span><span class="sxs-lookup"><span data-stu-id="be77a-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="be77a-174">Entity Framework v centru pro vývojáře dat MSDN</span><span class="sxs-lookup"><span data-stu-id="be77a-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="be77a-175">Přehled ovládacího prvku webového serveru EntityDataSource v knihovně MSDN</span><span class="sxs-lookup"><span data-stu-id="be77a-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="be77a-176">Odkaz na rozhraní API ovládacího prvku EntityDataSource v knihovně MSDN</span><span class="sxs-lookup"><span data-stu-id="be77a-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="be77a-177">Entity Framework fóra na webu MSDN</span><span class="sxs-lookup"><span data-stu-id="be77a-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="be77a-178">Blog Julie Lerman</span><span class="sxs-lookup"><span data-stu-id="be77a-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [<span data-ttu-id="be77a-179">Předchozí</span><span class="sxs-lookup"><span data-stu-id="be77a-179">Previous</span></span>](the-entity-framework-and-aspnet-getting-started-part-7.md)
