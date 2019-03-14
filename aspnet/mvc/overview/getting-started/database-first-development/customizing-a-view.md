---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'Kurz: Přizpůsobení zobrazení pro EF Database First s ASP.NET MVC aplikace'
description: Tento kurz se zaměřuje na změny automaticky generované zobrazení k vylepšení v prezentaci.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067270"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="1afbb-103">Kurz: Přizpůsobení zobrazení pro EF Database First s ASP.NET MVC aplikace</span><span class="sxs-lookup"><span data-stu-id="1afbb-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="1afbb-104">Pomocí generování uživatelského rozhraní ASP.NET, MVC a Entity Framework, můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="1afbb-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="1afbb-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který umožňuje uživatelům zobrazit, upravit, vytvořit a odstranit data, která se nachází v databázové tabulce.</span><span class="sxs-lookup"><span data-stu-id="1afbb-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="1afbb-106">Generovaný kód odpovídá sloupců v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="1afbb-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="1afbb-107">Tento kurz se zaměřuje na změny automaticky generované zobrazení k vylepšení v prezentaci.</span><span class="sxs-lookup"><span data-stu-id="1afbb-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="1afbb-108">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="1afbb-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1afbb-109">Přidat kurzů na stránku podrobností studenta</span><span class="sxs-lookup"><span data-stu-id="1afbb-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="1afbb-110">Ověřit, že se na kurzy přidán na stránku</span><span class="sxs-lookup"><span data-stu-id="1afbb-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1afbb-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1afbb-111">Prerequisites</span></span>

* [<span data-ttu-id="1afbb-112">Změna databáze</span><span class="sxs-lookup"><span data-stu-id="1afbb-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="1afbb-113">Přidat podrobnosti o studentovi kurzy</span><span class="sxs-lookup"><span data-stu-id="1afbb-113">Add courses to student detail</span></span>

<span data-ttu-id="1afbb-114">Generovaný kód poskytuje dobrým výchozím bodem pro vaši aplikaci, ale neposkytuje nutně všechny funkce, které potřebujete ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="1afbb-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="1afbb-115">Můžete upravit kód pro konkrétní požadavkům vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="1afbb-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="1afbb-116">V současné době aplikace zaregistrovaná kurzy pro vybrané student nezobrazuje.</span><span class="sxs-lookup"><span data-stu-id="1afbb-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="1afbb-117">V této části přidáte zaregistrované kurzy pro každého studenta do **podrobnosti** zobrazení pro studenta.</span><span class="sxs-lookup"><span data-stu-id="1afbb-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="1afbb-118">Otevřít **zobrazení** > **studenty** > *Details.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="1afbb-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="1afbb-119">Pod poslední &lt;/dl&gt; značky, ale před uzavírající &lt;/div&gt; značky, přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="1afbb-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="1afbb-120">Tento kód vytvoří tabulku, která se zobrazí řádek pro každý záznam v tabulce registrace pro vybrané studentů.</span><span class="sxs-lookup"><span data-stu-id="1afbb-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="1afbb-121">**Zobrazení** metoda vykreslí HTML pro objekt (modelItem), který představuje výraz.</span><span class="sxs-lookup"><span data-stu-id="1afbb-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="1afbb-122">Použití zobrazení metody (místo v kódu jednoduše vložení hodnoty vlastnosti) do Ujistěte se, že hodnota formátována správně na základě jeho typu a šablonu pro daný typ.</span><span class="sxs-lookup"><span data-stu-id="1afbb-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="1afbb-123">V tomto příkladu každý výraz vrátí jedinou vlastnost z aktuální záznam ve smyčce a hodnoty jsou primitivní typy, které jsou generovány jako text.</span><span class="sxs-lookup"><span data-stu-id="1afbb-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="1afbb-124">Potvrďte, že jsou přidány kurzy</span><span class="sxs-lookup"><span data-stu-id="1afbb-124">Confirm courses are added</span></span>

<span data-ttu-id="1afbb-125">Spuštění řešení.</span><span class="sxs-lookup"><span data-stu-id="1afbb-125">Run the solution.</span></span> <span data-ttu-id="1afbb-126">Klikněte na tlačítko **seznamu studentů** a vyberte **podrobnosti** pro jeden z studenty.</span><span class="sxs-lookup"><span data-stu-id="1afbb-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="1afbb-127">Uvidíte, že registrovaná kurzy byla zahrnuta v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="1afbb-127">You will see the enrolled courses have been included in the view.</span></span>

![studenta s registrací](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="1afbb-129">Další kroky</span><span class="sxs-lookup"><span data-stu-id="1afbb-129">Next steps</span></span>
<span data-ttu-id="1afbb-130">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="1afbb-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1afbb-131">Přidání kurzů na stránku podrobností studenta</span><span class="sxs-lookup"><span data-stu-id="1afbb-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="1afbb-132">Potvrdit, že jsou na stránku přidá kurzy</span><span class="sxs-lookup"><span data-stu-id="1afbb-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="1afbb-133">Přejděte k dalšímu kurzu, přečtěte si, jak přidat datových poznámek k určení požadavků na ověření a zobrazení formátování.</span><span class="sxs-lookup"><span data-stu-id="1afbb-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1afbb-134">Vylepšení ověřování dat</span><span class="sxs-lookup"><span data-stu-id="1afbb-134">Enhance data validation</span></span>](enhancing-data-validation.md)
