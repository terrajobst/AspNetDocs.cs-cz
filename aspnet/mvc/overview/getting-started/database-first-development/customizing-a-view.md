---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'Kurz: přizpůsobení zobrazení pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na změnu automaticky generovaných zobrazení pro vylepšení prezentace.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583592"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="5a048-103">Kurz: přizpůsobení zobrazení pro EF Database First pomocí aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="5a048-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="5a048-104">Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="5a048-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="5a048-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="5a048-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="5a048-106">Generovaný kód odpovídá sloupcům v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="5a048-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="5a048-107">Tento kurz se zaměřuje na změnu automaticky generovaných zobrazení pro vylepšení prezentace.</span><span class="sxs-lookup"><span data-stu-id="5a048-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="5a048-108">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="5a048-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a048-109">Přidání kurzů na stránku podrobností studenta</span><span class="sxs-lookup"><span data-stu-id="5a048-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="5a048-110">Potvrďte, že jsou kurzy přidané na stránku.</span><span class="sxs-lookup"><span data-stu-id="5a048-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a048-111">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="5a048-111">Prerequisites</span></span>

* [<span data-ttu-id="5a048-112">Změna databáze</span><span class="sxs-lookup"><span data-stu-id="5a048-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="5a048-113">Přidání kurzů k podrobnostem studenta</span><span class="sxs-lookup"><span data-stu-id="5a048-113">Add courses to student detail</span></span>

<span data-ttu-id="5a048-114">Generovaný kód poskytuje dobrý výchozí bod pro vaši aplikaci, ale nutně neposkytuje všechny funkce, které v aplikaci potřebujete.</span><span class="sxs-lookup"><span data-stu-id="5a048-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="5a048-115">Kód můžete přizpůsobit tak, aby splňoval konkrétní požadavky vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="5a048-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="5a048-116">V současné době vaše aplikace nezobrazuje zaregistrované kurzy pro vybraného studenta.</span><span class="sxs-lookup"><span data-stu-id="5a048-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="5a048-117">V této části přidáte zaregistrované kurzy pro každého studenta do zobrazení **podrobností** pro studenta.</span><span class="sxs-lookup"><span data-stu-id="5a048-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="5a048-118">Otevřete **zobrazení** > **Students** > *Details. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="5a048-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="5a048-119">Pod poslední &lt;značka&gt;/DL, ale před uzavírací &lt;/div&gt; značky přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="5a048-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="5a048-120">Tento kód vytvoří tabulku, která zobrazí řádek pro každý záznam v tabulce zápisu pro vybraného studenta.</span><span class="sxs-lookup"><span data-stu-id="5a048-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="5a048-121">Metoda **Display** vykresluje HTML pro objekt (ModelItem), který představuje výraz.</span><span class="sxs-lookup"><span data-stu-id="5a048-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="5a048-122">Použijte metodu Display (místo pouhého vložení hodnoty vlastnosti v kódu), abyste se ujistili, že je hodnota formátována správně na základě jejího typu a šablony pro daný typ.</span><span class="sxs-lookup"><span data-stu-id="5a048-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="5a048-123">V tomto příkladu každý výraz vrátí jednu vlastnost z aktuálního záznamu ve smyčce a hodnoty jsou primitivní typy, které se vykreslují jako text.</span><span class="sxs-lookup"><span data-stu-id="5a048-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="5a048-124">Přidávají se potvrzení kurzů.</span><span class="sxs-lookup"><span data-stu-id="5a048-124">Confirm courses are added</span></span>

<span data-ttu-id="5a048-125">Spusťte řešení.</span><span class="sxs-lookup"><span data-stu-id="5a048-125">Run the solution.</span></span> <span data-ttu-id="5a048-126">Klikněte na **seznam studentů** a vyberte **Podrobnosti** pro jednoho z studentů.</span><span class="sxs-lookup"><span data-stu-id="5a048-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="5a048-127">V zobrazení se zobrazí zaregistrované kurzy.</span><span class="sxs-lookup"><span data-stu-id="5a048-127">You will see the enrolled courses have been included in the view.</span></span>

![student s registrací](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="5a048-129">Další kroky</span><span class="sxs-lookup"><span data-stu-id="5a048-129">Next steps</span></span>
<span data-ttu-id="5a048-130">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="5a048-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a048-131">Přidání kurzů na stránku podrobností studenta</span><span class="sxs-lookup"><span data-stu-id="5a048-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="5a048-132">Potvrzení, že se kurzy přidávají na stránku</span><span class="sxs-lookup"><span data-stu-id="5a048-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="5a048-133">Přejděte k dalšímu kurzu, kde se dozvíte, jak přidat datové poznámky, abyste určili požadavky na ověření a formátování zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5a048-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5a048-134">Vylepšení ověřování dat</span><span class="sxs-lookup"><span data-stu-id="5a048-134">Enhance data validation</span></span>](enhancing-data-validation.md)
