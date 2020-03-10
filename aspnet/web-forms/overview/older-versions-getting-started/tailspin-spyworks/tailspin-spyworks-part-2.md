---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'Část 2: Vrstva přístupu k datům | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 2 pokrývá přidání vrstvy přístupu k datům.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573246"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="6f578-104">2\. část: Vrstva přístupu k datům</span><span class="sxs-lookup"><span data-stu-id="6f578-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="6f578-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="6f578-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="6f578-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="6f578-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="6f578-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="6f578-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="6f578-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="6f578-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="6f578-109">Část 2 pokrývá přidání vrstvy přístupu k datům.</span><span class="sxs-lookup"><span data-stu-id="6f578-109">Part 2 covers adding the data access layer.</span></span>

## <a id="_Toc260221668"></a><span data-ttu-id="6f578-110">Přidání vrstvy přístupu k datům</span><span class="sxs-lookup"><span data-stu-id="6f578-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="6f578-111">Naše aplikace elektronického obchodování bude záviset na dvou databázích.</span><span class="sxs-lookup"><span data-stu-id="6f578-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="6f578-112">Pro informace o zákaznících budeme používat standardní databázi členství v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6f578-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="6f578-113">Pro náš nákupní košík a katalog produktů implementujeme databázi SQL Express následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="6f578-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="6f578-114">Když jste vytvořili databázi (obchod. mdf) v aplikační složce\_aplikace, můžeme pokračovat v vytváření naší vrstvy přístupu k datům pomocí Entity Framework .NET.</span><span class="sxs-lookup"><span data-stu-id="6f578-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="6f578-115">Vytvoříme složku s názvem "přístup k datům\_" a na tuto složku kliknete pravým tlačítkem a vyberete Přidat novou položku.</span><span class="sxs-lookup"><span data-stu-id="6f578-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="6f578-116">V položce "nainstalované šablony" a potom vyberte "ADO.NET model EDM (Entity Data Model)" zadejte EDM\_Commerce. edmx jako název a klikněte na tlačítko Přidat.</span><span class="sxs-lookup"><span data-stu-id="6f578-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="6f578-117">Vyberte možnost generovat z databáze.</span><span class="sxs-lookup"><span data-stu-id="6f578-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="6f578-118">Uložte a sestavte.</span><span class="sxs-lookup"><span data-stu-id="6f578-118">Save and build.</span></span>

<span data-ttu-id="6f578-119">Teď jsme připraveni přidat naši první funkci – nabídku kategorie produktu.</span><span class="sxs-lookup"><span data-stu-id="6f578-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6f578-120">[Předchozí](tailspin-spyworks-part-1.md)
> [Další](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="6f578-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
