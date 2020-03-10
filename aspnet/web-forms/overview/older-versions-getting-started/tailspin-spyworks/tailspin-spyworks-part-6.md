---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: '6\. část: ASP.NET členství | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 6 přidává ASP.NET členství.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564181"
---
# <a name="part-6-aspnet-membership"></a><span data-ttu-id="7c122-104">6\. část: Členství v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7c122-104">Part 6: ASP.NET Membership</span></span>

<span data-ttu-id="7c122-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="7c122-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="7c122-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="7c122-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="7c122-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="7c122-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="7c122-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="7c122-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="7c122-109">Část 6 přidává ASP.NET členství.</span><span class="sxs-lookup"><span data-stu-id="7c122-109">Part 6 adds ASP.NET Membership.</span></span>

## <a id="_Toc260221672"></a><span data-ttu-id="7c122-110">Práce s ASP.NET členstvím</span><span class="sxs-lookup"><span data-stu-id="7c122-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="7c122-111">Klikněte na zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="7c122-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="7c122-112">Ujistěte se, že používáme ověřování pomocí formulářů.</span><span class="sxs-lookup"><span data-stu-id="7c122-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="7c122-113">Pomocí odkazu vytvořit uživatele můžete vytvořit několik uživatelů.</span><span class="sxs-lookup"><span data-stu-id="7c122-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="7c122-114">Až budete hotovi, přečtěte si okno Průzkumník řešení a aktualizujte zobrazení.</span><span class="sxs-lookup"><span data-stu-id="7c122-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="7c122-115">Všimněte si, že je k dispaměti ASPNETDB. Byla vytvořena pokuta MDF.</span><span class="sxs-lookup"><span data-stu-id="7c122-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="7c122-116">Tento soubor obsahuje tabulky pro podporu základních služeb ASP.NET, jako je třeba členství.</span><span class="sxs-lookup"><span data-stu-id="7c122-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="7c122-117">Nyní můžeme začít s implementací procesu registrace.</span><span class="sxs-lookup"><span data-stu-id="7c122-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="7c122-118">Začněte vytvořením stránky rezervovat. aspx.</span><span class="sxs-lookup"><span data-stu-id="7c122-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="7c122-119">Stránka rezervovat. aspx by měla být k dispozici pouze uživatelům, kteří jsou přihlášeni, a proto omezíme přístup k přihlášeným uživatelům a uživatelům, kteří nejsou přihlášení k přihlašovací stránce, budou přesměrováni.</span><span class="sxs-lookup"><span data-stu-id="7c122-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="7c122-120">K tomu přidáme následující do konfiguračního oddílu souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="7c122-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="7c122-121">Šablona pro aplikace webových formulářů ASP.NET automaticky přidala oddíl ověřování do našeho souboru Web. config a navázala výchozí přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="7c122-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="7c122-122">Pro migraci anonymního nákupního košíku, když se uživatel přihlásí, je nutné upravit soubor přihlašovacího jména. aspx.</span><span class="sxs-lookup"><span data-stu-id="7c122-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="7c122-123">Následujícím způsobem změňte událost\_načíst stránku.</span><span class="sxs-lookup"><span data-stu-id="7c122-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="7c122-124">Pak přidejte obslužnou rutinu události "LoggedIn", například tuto hodnotu, chcete-li nastavit název relace na nově přihlášeného uživatele a změnit ID dočasné relace v nákupním košíku na uživatele voláním metody MigrateCart v naší třídě MyShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="7c122-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="7c122-125">(Implementováno v souboru. cs)</span><span class="sxs-lookup"><span data-stu-id="7c122-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="7c122-126">Implementujte metodu MigrateCart (), jako to.</span><span class="sxs-lookup"><span data-stu-id="7c122-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="7c122-127">V rezervaci. aspx budeme na naší stránce rezervace používat EntityDataSource a GridView, což je mnohem stejně jako na naší stránce nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="7c122-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="7c122-128">Všimněte si, že náš ovládací prvek GridView Určuje obslužnou rutinu události "OnDataBound" s názvem MyList\_RowDataBound, takže implementuje tuto obslužnou rutinu události jako.</span><span class="sxs-lookup"><span data-stu-id="7c122-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="7c122-129">Tato metoda udržuje průběžný součet nákupního košíku, protože je každý řádek svázán a aktualizuje spodní řádek prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="7c122-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="7c122-130">V této fázi jsme implementovali "kontrolu" pro objednávku, která se má umístit.</span><span class="sxs-lookup"><span data-stu-id="7c122-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="7c122-131">Pořídíme scénář prázdného vozíku přidáním několika řádků kódu na naši stránku\_události načtení:</span><span class="sxs-lookup"><span data-stu-id="7c122-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="7c122-132">Když uživatel klikne na tlačítko Odeslat, spustí se v obslužné rutině události Click tlačítka pro odeslání následující kód.</span><span class="sxs-lookup"><span data-stu-id="7c122-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="7c122-133">"Maso" procesu odeslání objednávky je implementováno v metodě SubmitOrder () naší třídy MyShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="7c122-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="7c122-134">SubmitOrder bude:</span><span class="sxs-lookup"><span data-stu-id="7c122-134">SubmitOrder will:</span></span>

- <span data-ttu-id="7c122-135">Vezměte všechny řádkové položky v nákupním košíku a použijte je k vytvoření nového záznamu objednávky a přidružených záznamů OrderDetails.</span><span class="sxs-lookup"><span data-stu-id="7c122-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="7c122-136">Vypočítat datum expedice.</span><span class="sxs-lookup"><span data-stu-id="7c122-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="7c122-137">Vymažte nákupní košík.</span><span class="sxs-lookup"><span data-stu-id="7c122-137">Clear the shopping cart.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="7c122-138">Pro účely této ukázkové aplikace vypočítáme datum odeslání pouhým přidáním dvou dnů k aktuálnímu datu.</span><span class="sxs-lookup"><span data-stu-id="7c122-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="7c122-139">Spuštění aplikace teď umožní otestovat nákupní proces od začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="7c122-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7c122-140">[Předchozí](tailspin-spyworks-part-5.md)
> [Další](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="7c122-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
