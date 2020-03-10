---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'Kurz: vylepšení ověřování dat pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na přidání datových poznámek k datovému modelu a určení požadavků na ověření a formátování zobrazení.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616275"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="0266c-103">Kurz: vylepšení ověřování dat pro EF Database First pomocí aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0266c-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="0266c-104">Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="0266c-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="0266c-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="0266c-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="0266c-106">Generovaný kód odpovídá sloupcům v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="0266c-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="0266c-107">Tento kurz se zaměřuje na přidání datových poznámek k datovému modelu a určení požadavků na ověření a formátování zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0266c-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="0266c-108">Vylepšili jsme se na základě zpětné vazby uživatelů v části komentáře.</span><span class="sxs-lookup"><span data-stu-id="0266c-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="0266c-109">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="0266c-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0266c-110">Přidat datové poznámky</span><span class="sxs-lookup"><span data-stu-id="0266c-110">Add data annotations</span></span>
> * <span data-ttu-id="0266c-111">Přidat třídy metadat</span><span class="sxs-lookup"><span data-stu-id="0266c-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0266c-112">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="0266c-112">Prerequisites</span></span>

* [<span data-ttu-id="0266c-113">Přizpůsobení zobrazení</span><span class="sxs-lookup"><span data-stu-id="0266c-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="0266c-114">Přidat datové poznámky</span><span class="sxs-lookup"><span data-stu-id="0266c-114">Add data annotations</span></span>

<span data-ttu-id="0266c-115">Jak jste viděli v předchozím tématu, některá pravidla ověření dat se automaticky aplikují na vstup uživatele.</span><span class="sxs-lookup"><span data-stu-id="0266c-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="0266c-116">Můžete například zadat jenom číslo vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="0266c-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="0266c-117">Chcete-li zadat další pravidla pro ověřování dat, můžete do třídy modelu přidat datové poznámky.</span><span class="sxs-lookup"><span data-stu-id="0266c-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="0266c-118">Tyto poznámky jsou v rámci vaší webové aplikace aplikovány na zadanou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="0266c-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="0266c-119">Můžete také použít atributy formátování, které mění způsob zobrazení vlastností; například změna hodnoty používané pro textové popisky.</span><span class="sxs-lookup"><span data-stu-id="0266c-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="0266c-120">V tomto kurzu přidáte poznámky k datům, abyste omezili délku hodnot poskytnutých pro vlastnosti FirstName, LastName a MiddleName.</span><span class="sxs-lookup"><span data-stu-id="0266c-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="0266c-121">V databázi jsou tyto hodnoty omezeny na 50 znaků; ve vaší webové aplikaci se ale omezení počtu znaků aktuálně nevynutilo.</span><span class="sxs-lookup"><span data-stu-id="0266c-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="0266c-122">Pokud uživatel zadá pro jednu z těchto hodnot více než 50 znaků, stránka při pokusu o uložení hodnoty do databáze dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="0266c-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="0266c-123">Také omezíte hodnotu pro hodnoty mezi 0 a 4.</span><span class="sxs-lookup"><span data-stu-id="0266c-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="0266c-124">Vyberte **modely** > **ContosoModel. edmx** > **ContosoModel.TT** a otevřete soubor *student.cs* .</span><span class="sxs-lookup"><span data-stu-id="0266c-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="0266c-125">Do třídy přidejte následující zvýrazněný kód.</span><span class="sxs-lookup"><span data-stu-id="0266c-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="0266c-126">Otevřete *Enrollment.cs* a přidejte následující zvýrazněný kód.</span><span class="sxs-lookup"><span data-stu-id="0266c-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="0266c-127">Sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="0266c-127">Build the solution.</span></span>

<span data-ttu-id="0266c-128">Klikněte na **seznam studentů** a vyberte **Upravit**.</span><span class="sxs-lookup"><span data-stu-id="0266c-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="0266c-129">Pokud se pokusíte zadat více než 50 znaků, zobrazí se chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="0266c-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![zobrazit chybovou zprávu](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="0266c-131">Vraťte se na domovskou stránku.</span><span class="sxs-lookup"><span data-stu-id="0266c-131">Go back to the home page.</span></span> <span data-ttu-id="0266c-132">Klikněte na **seznam** registrací a vyberte **Upravit**.</span><span class="sxs-lookup"><span data-stu-id="0266c-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="0266c-133">Došlo k pokusu o poskytnutí třídy nad 4.</span><span class="sxs-lookup"><span data-stu-id="0266c-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="0266c-134">Tato chyba se zobrazí: *hodnota třídy musí být mezi 0 a 4.*</span><span class="sxs-lookup"><span data-stu-id="0266c-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="0266c-135">Přidat třídy metadat</span><span class="sxs-lookup"><span data-stu-id="0266c-135">Add metadata classes</span></span>

<span data-ttu-id="0266c-136">Přidávání ověřovacích atributů přímo do třídy modelu funguje, když neočekáváte, že se databáze mění; Pokud se ale vaše databáze změní a potřebujete znovu vygenerovat třídu modelu, ztratíte všechny atributy, které jste použili u třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="0266c-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="0266c-137">Tento přístup může být velice neefektivní a náchylný ke ztrátě důležitých ověřovacích pravidel.</span><span class="sxs-lookup"><span data-stu-id="0266c-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="0266c-138">Chcete-li se tomuto problému vyhnout, můžete přidat třídu metadat obsahující atributy.</span><span class="sxs-lookup"><span data-stu-id="0266c-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="0266c-139">Při přidružení třídy modelu k třídě metadat se tyto atributy aplikují na model.</span><span class="sxs-lookup"><span data-stu-id="0266c-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="0266c-140">V tomto přístupu třída modelu může být znovu vygenerována bez ztráty všech atributů, které byly aplikovány na třídu metadat.</span><span class="sxs-lookup"><span data-stu-id="0266c-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="0266c-141">Ve složce **modely** přidejte třídu s názvem *metadata.cs*.</span><span class="sxs-lookup"><span data-stu-id="0266c-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="0266c-142">Nahraďte kód v *metadata.cs* následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="0266c-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="0266c-143">Tyto třídy metadat obsahují všechny atributy ověřování, které jste předtím použili u tříd modelu.</span><span class="sxs-lookup"><span data-stu-id="0266c-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="0266c-144">Atribut **zobrazení** se používá ke změně hodnoty používané pro textové popisky.</span><span class="sxs-lookup"><span data-stu-id="0266c-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="0266c-145">Nyní je třeba přidružit třídy modelů k třídám metadat.</span><span class="sxs-lookup"><span data-stu-id="0266c-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="0266c-146">Ve složce **modely** přidejte třídu s názvem *PartialClasses.cs*.</span><span class="sxs-lookup"><span data-stu-id="0266c-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="0266c-147">Obsah souboru nahraďte následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="0266c-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="0266c-148">Všimněte si, že každá třída je označena jako třída `partial` a každý odpovídá názvu a oboru názvů jako třída, která je automaticky vygenerována.</span><span class="sxs-lookup"><span data-stu-id="0266c-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="0266c-149">Použitím atributu metadata na částečnou třídu zajistíte, aby atributy ověřování dat byly použity na automaticky generovanou třídu.</span><span class="sxs-lookup"><span data-stu-id="0266c-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="0266c-150">Tyto atributy nebudou ztraceny při opětovném vygenerování tříd modelu, protože atribut metadata je použit v dílčích třídách, které nejsou znovu vygenerovány.</span><span class="sxs-lookup"><span data-stu-id="0266c-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="0266c-151">Chcete-li znovu vygenerovat automaticky generované třídy, otevřete soubor *ContosoModel. edmx* .</span><span class="sxs-lookup"><span data-stu-id="0266c-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="0266c-152">Znovu klikněte pravým tlačítkem myši na návrhovou plochu a vyberte **aktualizovat model z databáze**.</span><span class="sxs-lookup"><span data-stu-id="0266c-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="0266c-153">I když jste databázi nezměnili, tento proces znovu vygeneruje třídy.</span><span class="sxs-lookup"><span data-stu-id="0266c-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="0266c-154">Na kartě **aktualizovat** vyberte **tabulky** a **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="0266c-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="0266c-155">Uložte soubor *ContosoModel. edmx* , aby se změny projevily.</span><span class="sxs-lookup"><span data-stu-id="0266c-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="0266c-156">Otevřete soubor *student.cs* nebo soubor *Enrollment.cs* a Všimněte si, že výše použité atributy ověření dat již nejsou v souboru.</span><span class="sxs-lookup"><span data-stu-id="0266c-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="0266c-157">Spusťte ale aplikaci a Všimněte si, že ověřovací pravidla se při zadávání dat pořád používají.</span><span class="sxs-lookup"><span data-stu-id="0266c-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="0266c-158">Závěr</span><span class="sxs-lookup"><span data-stu-id="0266c-158">Conclusion</span></span>

<span data-ttu-id="0266c-159">Tato série poskytuje jednoduchý příklad, jak generovat kód z existující databáze, která umožňuje uživatelům upravovat, aktualizovat, vytvářet a odstraňovat data.</span><span class="sxs-lookup"><span data-stu-id="0266c-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="0266c-160">Používá ASP.NET MVC 5, Entity Framework a ASP.NET generování uživatelského rozhraní pro vytvoření projektu.</span><span class="sxs-lookup"><span data-stu-id="0266c-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="0266c-161">Úvodní příklad Code First vývoje najdete v článku [Začínáme s ASP.NET MVC 5](../introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0266c-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="0266c-162">Pokročilejší příklad najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC 4](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="0266c-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="0266c-163">Všimněte si, že rozhraní API DbContext, které používáte pro práci s daty v Database First, je stejné jako rozhraní API, které používáte pro práci s daty v Code First.</span><span class="sxs-lookup"><span data-stu-id="0266c-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="0266c-164">I v případě, že máte v úmyslu použít Database First, můžete se dozvědět, jak zpracovávat složitější scénáře, jako je čtení a aktualizace souvisejících dat, zpracování konfliktů souběžnosti a tak dále v kurzu Code First.</span><span class="sxs-lookup"><span data-stu-id="0266c-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="0266c-165">Jediný rozdíl je v tom, jak jsou vytvořeny databáze, třídy kontextu a třídy entit.</span><span class="sxs-lookup"><span data-stu-id="0266c-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0266c-166">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="0266c-166">Additional resources</span></span>

<span data-ttu-id="0266c-167">Úplný seznam poznámek k ověření dat, které můžete použít pro vlastnosti a třídy, naleznete v tématu [System. ComponentModel. DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span><span class="sxs-lookup"><span data-stu-id="0266c-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0266c-168">Další kroky</span><span class="sxs-lookup"><span data-stu-id="0266c-168">Next steps</span></span>

<span data-ttu-id="0266c-169">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="0266c-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0266c-170">Přidané datové poznámky</span><span class="sxs-lookup"><span data-stu-id="0266c-170">Added data annotations</span></span>
> * <span data-ttu-id="0266c-171">Přidané třídy metadat</span><span class="sxs-lookup"><span data-stu-id="0266c-171">Added metadata classes</span></span>

<span data-ttu-id="0266c-172">Další informace o tom, jak nasadit webovou aplikaci a databázi SQL pro Azure App Service, najdete v tomto kurzu:</span><span class="sxs-lookup"><span data-stu-id="0266c-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0266c-173">Nasazení aplikace .NET pro Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0266c-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
