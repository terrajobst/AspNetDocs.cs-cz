---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 'Část 6: Členství technologie ASP.NET | Dokumentace Microsoftu'
author: JoeStagner
description: V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace Tailspin Spyworks. Část 6 přidá členství technologie ASP.NET.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: c847db058bc03115210f12eeb0c3c76fecc8a31e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075592"
---
<a name="part-6-aspnet-membership"></a><span data-ttu-id="b3591-104">Část 6: Členství v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b3591-104">Part 6: ASP.NET Membership</span></span>
====================
<span data-ttu-id="b3591-105">podle [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="b3591-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="b3591-106">Tailspin Spyworks ukazuje, jak mimořádně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="b3591-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="b3591-107">Zobrazuje vypnout použití skvělých nových funkcí v technologii ASP.NET 4 k sestavení nebo online úložiště, včetně nákupu, Pokladna a správu.</span><span class="sxs-lookup"><span data-stu-id="b3591-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="b3591-108">V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="b3591-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="b3591-109">Část 6 přidá členství technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b3591-109">Part 6 adds ASP.NET Membership.</span></span>


## <a id="_Toc260221672"></a>  <span data-ttu-id="b3591-110">Práce s členství technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b3591-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="b3591-111">Klikněte na tlačítko zabezpečení</span><span class="sxs-lookup"><span data-stu-id="b3591-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="b3591-112">Ujistěte se, že se používá ověřování pomocí formulářů.</span><span class="sxs-lookup"><span data-stu-id="b3591-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="b3591-113">Použijte odkaz "Create User" k vytvoření několika uživatelů.</span><span class="sxs-lookup"><span data-stu-id="b3591-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="b3591-114">Až budete hotovi, najdete v okně Průzkumník řešení a aktualizujte zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b3591-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="b3591-115">Všimněte si, ASPNETDB. Byl vytvořen MDF bez problémů.</span><span class="sxs-lookup"><span data-stu-id="b3591-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="b3591-116">Tento soubor obsahuje tabulky, které podporují služby ASP.NET core jako je členství.</span><span class="sxs-lookup"><span data-stu-id="b3591-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="b3591-117">Teď můžeme začít implementace proces platby u pokladny.</span><span class="sxs-lookup"><span data-stu-id="b3591-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="b3591-118">Začněte tím, že vytvoření CheckOut.aspx stránky.</span><span class="sxs-lookup"><span data-stu-id="b3591-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="b3591-119">Na stránce CheckOut.aspx by měl být k dispozici pouze uživatelům, kteří přihlášeni, takže jsme se omezení přístupu k přihlášení uživatelů a přesměrovává uživatele, kteří nejsou přihlášeni na přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="b3591-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="b3591-120">Provedete to tak přidáme následující konfigurační oddíl souboru web.config.</span><span class="sxs-lookup"><span data-stu-id="b3591-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="b3591-121">Šablona pro aplikace webových formulářů ASP.NET automaticky přidat oddíl ověřování do souboru web.config a navázat na výchozí přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="b3591-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="b3591-122">Upravíme Login.aspx souboru kódu na pozadí k migraci anonymní nákupního košíku, když se uživatel přihlásí.</span><span class="sxs-lookup"><span data-stu-id="b3591-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="b3591-123">Změnit na stránce\_událostí načtení následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="b3591-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="b3591-124">Pak přidejte obslužnou rutinu události "LoggedIn" následujícím způsobem nastavte název relace na nově přihlášeného uživatele a změnit id dočasné relace v nákupním košíku jménu uživatele voláním metody MigrateCart v našich MyShoppingCart třídy.</span><span class="sxs-lookup"><span data-stu-id="b3591-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="b3591-125">(Implementováno v souboru .cs)</span><span class="sxs-lookup"><span data-stu-id="b3591-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="b3591-126">Implementujte metodu MigrateCart() tímto způsobem.</span><span class="sxs-lookup"><span data-stu-id="b3591-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="b3591-127">V checkout.aspx jsme budete používat EntityDataSource a GridView v našich podívejte se na stránku podobně, jako jsme to udělali v našich nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="b3591-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="b3591-128">Všimněte si, že naše ovládacího prvku GridView určuje obslužnou rutinu události "ondatabound" s názvem MyList\_RowDataBound můžeme implementovat tuto obslužnou rutinu události následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="b3591-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="b3591-129">Tato metoda udržuje průběžný součet z nákupního košíku a každý řádek je vázán aktualizuje dolní řádek prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="b3591-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="b3591-130">V této fázi jsme implementovali prezentaci "recenzi" aby bylo možné umístit.</span><span class="sxs-lookup"><span data-stu-id="b3591-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="b3591-131">Umožňuje zpracovat scénáři prázdný košíku přidáním několika řádků kódu na naši stránku\_zatížení události:</span><span class="sxs-lookup"><span data-stu-id="b3591-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="b3591-132">Když uživatel klikne na tlačítko "Odeslat" jsme spustí následující kód v obslužné rutině události klikněte na tlačítko Odeslat.</span><span class="sxs-lookup"><span data-stu-id="b3591-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="b3591-133">"Maso" proces odeslání objednávky je implementovaná v metodě SubmitOrder() naše MyShoppingCart třídy.</span><span class="sxs-lookup"><span data-stu-id="b3591-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="b3591-134">SubmitOrder bude:</span><span class="sxs-lookup"><span data-stu-id="b3591-134">SubmitOrder will:</span></span>

- <span data-ttu-id="b3591-135">Provést všechny položky v nákupním košíku a jejich používání při vytváření nového záznamu pořadí a propojené OrderDetails záznamy.</span><span class="sxs-lookup"><span data-stu-id="b3591-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="b3591-136">Výpočet expediční datum.</span><span class="sxs-lookup"><span data-stu-id="b3591-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="b3591-137">Vymažte nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="b3591-137">Clear the shopping cart.</span></span>


[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="b3591-138">Pro účely této ukázkové aplikaci výpočtu datum expedice jednoduše přidejte dva dny na aktuální datum.</span><span class="sxs-lookup"><span data-stu-id="b3591-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="b3591-139">Spuštění aplikace teď umožní nám to otestovat nákupní proces od začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="b3591-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3591-140">[Předchozí](tailspin-spyworks-part-5.md)
> [další](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="b3591-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
