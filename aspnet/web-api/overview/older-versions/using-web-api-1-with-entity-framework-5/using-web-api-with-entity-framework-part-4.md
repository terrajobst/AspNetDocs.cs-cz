---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 'Část 4: Přidání zobrazení pro správce | Dokumentace Microsoftu'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: ff46c7cbdf13a048e57ad88ab39077357e35c5b3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071458"
---
<a name="part-4-adding-an-admin-view"></a><span data-ttu-id="a6fd7-102">Část 4: Přidání zobrazení pro správce</span><span class="sxs-lookup"><span data-stu-id="a6fd7-102">Part 4: Adding an Admin View</span></span>
====================
<span data-ttu-id="a6fd7-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a6fd7-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a6fd7-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="a6fd7-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="a6fd7-105">Přidání zobrazení správce</span><span class="sxs-lookup"><span data-stu-id="a6fd7-105">Add an Admin View</span></span>

<span data-ttu-id="a6fd7-106">Teď vytvoříme zapnout na straně klienta a přidáme stránku, která využívají data z kontroleru pro správce.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="a6fd7-107">Na stránce vám umožní uživatelům vytvořit, upravit nebo odstranit produktů, pomocí zasílání požadavků AJAX na kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="a6fd7-108">V Průzkumníku řešení rozbalte složku řadiče a otevřete soubor s názvem HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="a6fd7-109">Tento soubor obsahuje kontroler MVC.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-109">This file contains an MVC controller.</span></span> <span data-ttu-id="a6fd7-110">Přidat metodu s názvem `Admin`:</span><span class="sxs-lookup"><span data-stu-id="a6fd7-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="a6fd7-111">**HttpRouteUrl** metoda vytvoří identifikátor URI pro webové rozhraní API, a to uchovává v kontejneru a zobrazení pro pozdější.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="a6fd7-112">V dalším kroku umístění kurzoru text v rámci `Admin` metodě akce, pak klikněte pravým tlačítkem a vyberte **přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="a6fd7-113">Tím se otevře **přidat zobrazení** dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="a6fd7-114">V **přidat zobrazení** dialogového okna, název zobrazení "Admin".</span><span class="sxs-lookup"><span data-stu-id="a6fd7-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="a6fd7-115">Zaškrtněte políčko s popiskem **vytvoření zobrazení se silnými typy**.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="a6fd7-116">V části **třídy modelu**, vyberte "Produktu (ProductStore.Models)".</span><span class="sxs-lookup"><span data-stu-id="a6fd7-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="a6fd7-117">Všechny další možnosti ponechte jejich výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="a6fd7-118">Kliknutím na **přidat** přidá soubor s názvem Admin.cshtml v rámci zobrazení Domů.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="a6fd7-119">Otevřete tento soubor a přidejte následující kód HTML.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="a6fd7-120">Tento kód HTML definuje strukturu stránky, ale žádné funkce je připraveno, ještě.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="a6fd7-121">Vytvořit odkaz na stránku pro správu</span><span class="sxs-lookup"><span data-stu-id="a6fd7-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="a6fd7-122">V Průzkumníku řešení rozbalte složku zobrazení a poté rozbalte složku Shared.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="a6fd7-123">Otevřete soubor s názvem \_Layout.cshtml.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="a6fd7-124">Vyhledejte **ul** element s id = "nabídka" a odkaz akce pro zobrazení správce:</span><span class="sxs-lookup"><span data-stu-id="a6fd7-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="a6fd7-125">V projektu vzorku můžu provedli několik dalších tyto kosmetické změny, jako je například nahradit řetězec "Zde bude vaše logo".</span><span class="sxs-lookup"><span data-stu-id="a6fd7-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="a6fd7-126">Tyto nemají vliv na funkce aplikace.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="a6fd7-127">Je možné projekt stáhnout a porovnat soubory.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-127">You can download the project and compare the files.</span></span>


<span data-ttu-id="a6fd7-128">Spusťte aplikaci a klikněte na odkaz "Admin", který se zobrazí v horní části domovské stránky.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="a6fd7-129">Na stránce správy by měl vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="a6fd7-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="a6fd7-130">Pravé teď na stránce nic nedělá.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="a6fd7-131">V další části používáme rozhraní Knockout.js k vytvoření dynamického uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="a6fd7-132">Přidat autorizaci</span><span class="sxs-lookup"><span data-stu-id="a6fd7-132">Add Authorization</span></span>

<span data-ttu-id="a6fd7-133">Na stránce správy je nyní k dispozici všem uživatelům následujícím webu.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="a6fd7-134">Změňme ji omezit oprávnění správcům.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="a6fd7-135">Začněte přidáním role "Správce" a uživatel s oprávněním správce.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="a6fd7-136">V Průzkumníku řešení rozbalte složku filtry a otevřete soubor s názvem InitializeSimpleMembershipAttribute.cs.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="a6fd7-137">Vyhledejte `SimpleMembershipInitializer` konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="a6fd7-138">Po volání **WebSecurity.InitializeDatabaseConnection**, přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="a6fd7-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="a6fd7-139">Toto je quick-and-dirty způsob, jak přidat roli "Správce" a vytvořte uživatele pro roli.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="a6fd7-140">V Průzkumníku řešení rozbalte složku řadiče a otevření souboru HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="a6fd7-141">Přidat **Authorize** atribut `Admin` metody.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="a6fd7-142">Otevřete soubor AdminController.cs a přidejte **Authorize** atribut pro celou `AdminController` třídy.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="a6fd7-143">MVC a webového rozhraní API, jak definovat **Authorize** atributy v různých oborech názvů.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="a6fd7-144">Aplikace MVC používá **System.Web.Mvc.AuthorizeAttribute**, zatímco webového rozhraní API používá **System.Web.Http.AuthorizeAttribute**.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>


<span data-ttu-id="a6fd7-145">Pouze správci teď mohou zobrazit stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="a6fd7-146">Navíc pokud odešlete požadavek HTTP kontroleru pro správce, žádost musí obsahovat soubor cookie ověřování.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="a6fd7-147">Pokud ne, server odešle odpověď HTTP 401 (Neautorizováno).</span><span class="sxs-lookup"><span data-stu-id="a6fd7-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="a6fd7-148">Zobrazí se to ve Fiddleru odesláním požadavek GET na `http://localhost:*port*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="a6fd7-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a6fd7-149">[Předchozí](using-web-api-with-entity-framework-part-3.md)
> [další](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="a6fd7-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
