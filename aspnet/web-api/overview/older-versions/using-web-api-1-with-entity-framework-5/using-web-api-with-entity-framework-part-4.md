---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4\. část: Přidání zobrazení Správce | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556012"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="516b0-102">4\. část: Přidání zobrazení pro správu</span><span class="sxs-lookup"><span data-stu-id="516b0-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="516b0-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="516b0-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="516b0-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="516b0-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="516b0-105">Přidat zobrazení Správce</span><span class="sxs-lookup"><span data-stu-id="516b0-105">Add an Admin View</span></span>

<span data-ttu-id="516b0-106">Teď se změní na stranu klienta a přidá se stránka, která může využívat data z kontroleru správce.</span><span class="sxs-lookup"><span data-stu-id="516b0-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="516b0-107">Stránka umožní uživatelům vytvářet, upravovat nebo odstraňovat produkty, a to odesláním požadavků AJAX do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="516b0-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="516b0-108">V Průzkumník řešení rozbalte složku řadiče a otevřete soubor s názvem HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="516b0-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="516b0-109">Tento soubor obsahuje kontroler MVC.</span><span class="sxs-lookup"><span data-stu-id="516b0-109">This file contains an MVC controller.</span></span> <span data-ttu-id="516b0-110">Přidejte metodu s názvem `Admin`:</span><span class="sxs-lookup"><span data-stu-id="516b0-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="516b0-111">Metoda **HttpRouteUrl** vytvoří identifikátor URI webového rozhraní API a uložíme ho do balíčku zobrazení pro pozdější verzi.</span><span class="sxs-lookup"><span data-stu-id="516b0-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="516b0-112">Dále umístěte kurzor na text do metody `Admin` akce, klikněte pravým tlačítkem myši a vyberte možnost **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="516b0-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="516b0-113">Tím se zobrazí dialogové okno **Přidat zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="516b0-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="516b0-114">V dialogovém okně **Přidat zobrazení** pojmenujte zobrazení "admin".</span><span class="sxs-lookup"><span data-stu-id="516b0-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="516b0-115">Zaškrtněte políčko s názvem **vytvořit zobrazení silného typu**.</span><span class="sxs-lookup"><span data-stu-id="516b0-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="516b0-116">V části **třída modelu**vyberte produkt (ProductStore. Models).</span><span class="sxs-lookup"><span data-stu-id="516b0-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="516b0-117">U ostatních možností ponechte výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="516b0-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="516b0-118">Kliknutím na **Přidat** přidáte do zobrazení/domů soubor s názvem admin. cshtml.</span><span class="sxs-lookup"><span data-stu-id="516b0-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="516b0-119">Otevřete tento soubor a přidejte následující kód HTML.</span><span class="sxs-lookup"><span data-stu-id="516b0-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="516b0-120">Tento kód HTML definuje strukturu stránky, ale ještě není kabelem funkční.</span><span class="sxs-lookup"><span data-stu-id="516b0-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="516b0-121">Vytvoří odkaz na stránku správce.</span><span class="sxs-lookup"><span data-stu-id="516b0-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="516b0-122">V Průzkumník řešení rozbalte složku zobrazení a potom rozbalte sdílenou složku.</span><span class="sxs-lookup"><span data-stu-id="516b0-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="516b0-123">Otevřete soubor s názvem \_layout. cshtml.</span><span class="sxs-lookup"><span data-stu-id="516b0-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="516b0-124">Vyhledejte element **ul** s ID = "nabídka" a odkaz akce pro zobrazení Správce:</span><span class="sxs-lookup"><span data-stu-id="516b0-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="516b0-125">V ukázkovém projektu jsem udělal několik dalších změn kosmetických prostředků, jako je například nahrazení řetězce "vaše logo".</span><span class="sxs-lookup"><span data-stu-id="516b0-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="516b0-126">Neovlivňují funkce aplikace.</span><span class="sxs-lookup"><span data-stu-id="516b0-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="516b0-127">Můžete stáhnout projekt a porovnat soubory.</span><span class="sxs-lookup"><span data-stu-id="516b0-127">You can download the project and compare the files.</span></span>

<span data-ttu-id="516b0-128">Spusťte aplikaci a klikněte na odkaz správce, který se zobrazí v horní části domovské stránky.</span><span class="sxs-lookup"><span data-stu-id="516b0-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="516b0-129">Stránka pro správu by měla vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="516b0-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="516b0-130">V tuto chvíli stránka není cokoli dělat.</span><span class="sxs-lookup"><span data-stu-id="516b0-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="516b0-131">V další části použijeme vyseknutí. js k vytvoření dynamického uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="516b0-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="516b0-132">Přidat autorizaci</span><span class="sxs-lookup"><span data-stu-id="516b0-132">Add Authorization</span></span>

<span data-ttu-id="516b0-133">Stránka pro správu je aktuálně přístupná všem návštěvníkům webu.</span><span class="sxs-lookup"><span data-stu-id="516b0-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="516b0-134">Pojďme to změnit, aby se omezilo oprávnění pro správce.</span><span class="sxs-lookup"><span data-stu-id="516b0-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="516b0-135">Začněte přidáním role správce a uživatele správce.</span><span class="sxs-lookup"><span data-stu-id="516b0-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="516b0-136">V Průzkumník řešení rozbalte složku filtry a otevřete soubor s názvem InitializeSimpleMembershipAttribute.cs.</span><span class="sxs-lookup"><span data-stu-id="516b0-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="516b0-137">Vyhledejte konstruktor `SimpleMembershipInitializer`.</span><span class="sxs-lookup"><span data-stu-id="516b0-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="516b0-138">Po volání metody **WebSecurity. InitializeDatabaseConnection**přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="516b0-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="516b0-139">Toto je rychlý a špinavý způsob, jak přidat roli správce a vytvořit uživatele pro tuto roli.</span><span class="sxs-lookup"><span data-stu-id="516b0-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="516b0-140">V Průzkumník řešení rozbalte složku řadiče a otevřete soubor HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="516b0-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="516b0-141">Přidejte atribut **autorizace** do metody `Admin`.</span><span class="sxs-lookup"><span data-stu-id="516b0-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="516b0-142">Otevřete soubor AdminController.cs a přidejte atribut **autorizuje** do celé `AdminController` třídy.</span><span class="sxs-lookup"><span data-stu-id="516b0-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="516b0-143">MVC a webové rozhraní API definují **autorizační** atributy v různých oborech názvů.</span><span class="sxs-lookup"><span data-stu-id="516b0-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="516b0-144">MVC používá **System. Web. Mvc. AuthorizeAttribute**, zatímco webové rozhraní API používá **System. Web. http. AuthorizeAttribute**.</span><span class="sxs-lookup"><span data-stu-id="516b0-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>

<span data-ttu-id="516b0-145">Stránku Správce teď můžou zobrazit jenom správci.</span><span class="sxs-lookup"><span data-stu-id="516b0-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="516b0-146">Pokud odešlete požadavek HTTP kontroleru správce, musí požadavek obsahovat ověřovací soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="516b0-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="516b0-147">V takovém případě pošle Server odpověď HTTP 401 (Neautorizovaná).</span><span class="sxs-lookup"><span data-stu-id="516b0-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="516b0-148">Můžete to zobrazit v Fiddler odesláním žádosti o získání `http://localhost:*port*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="516b0-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="516b0-149">[Předchozí](using-web-api-with-entity-framework-part-3.md)
> [Další](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="516b0-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
