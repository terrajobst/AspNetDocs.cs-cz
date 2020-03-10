---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 'Část 1: Přehled a vytvoření projektu | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556075"
---
# <a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="fd5f3-102">Část 1: Přehled a vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="fd5f3-102">Part 1: Overview and Creating the Project</span></span>

<span data-ttu-id="fd5f3-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fd5f3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="fd5f3-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="fd5f3-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="fd5f3-105">Entity Framework je rozhraní pro mapování objektů a relačních objektů.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="fd5f3-106">Mapuje doménové objekty ve vašem kódu na entity v relační databázi.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="fd5f3-107">Ve většině případů se nemusíte starat o databázovou vrstvu, protože ji Entity Framework postará za vás.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="fd5f3-108">Kód zpracovává objekty a změny jsou uchovány v databázi.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="fd5f3-109">O tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="fd5f3-109">About the Tutorial</span></span>

<span data-ttu-id="fd5f3-110">V tomto kurzu vytvoříte jednoduchou aplikaci ze Storu.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="fd5f3-111">Existují dvě hlavní části aplikace.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-111">There are two main parts to the application.</span></span> <span data-ttu-id="fd5f3-112">Normální uživatelé mohou zobrazit produkty a vytvářet objednávky:</span><span class="sxs-lookup"><span data-stu-id="fd5f3-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="fd5f3-113">Správci můžou vytvořit, odstranit nebo upravit produkty:</span><span class="sxs-lookup"><span data-stu-id="fd5f3-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="fd5f3-114">Dovednosti, se kterými se naučíte</span><span class="sxs-lookup"><span data-stu-id="fd5f3-114">Skills You'll Learn</span></span>

<span data-ttu-id="fd5f3-115">Tady je seznam toho, co se naučíte:</span><span class="sxs-lookup"><span data-stu-id="fd5f3-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="fd5f3-116">Jak používat Entity Framework s webovým rozhraním API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fd5f3-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="fd5f3-117">Jak použít vyseknutí. js k vytvoření dynamického uživatelského rozhraní klienta.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="fd5f3-118">Jak používat ověřování pomocí formulářů s webovým rozhraním API k ověřování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="fd5f3-119">I když je tento kurz samostatný, možná si budete chtít nejdřív přečíst následující kurzy:</span><span class="sxs-lookup"><span data-stu-id="fd5f3-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="fd5f3-120">Vaše první webové rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fd5f3-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="fd5f3-121">Vytvoření webového rozhraní API, které podporuje operace CRUD</span><span class="sxs-lookup"><span data-stu-id="fd5f3-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="fd5f3-122">K [disASP.NET](../../../../mvc/index.md) je také užitečné některé znalosti o MVC.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="fd5f3-123">Přehled</span><span class="sxs-lookup"><span data-stu-id="fd5f3-123">Overview</span></span>

<span data-ttu-id="fd5f3-124">V nejvyšší úrovni je tady architektura aplikace:</span><span class="sxs-lookup"><span data-stu-id="fd5f3-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="fd5f3-125">ASP.NET MVC vygeneruje stránky HTML pro klienta.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="fd5f3-126">Webové rozhraní API ASP.NET zpřístupňuje operace CRUD s daty (produkty a objednávky).</span><span class="sxs-lookup"><span data-stu-id="fd5f3-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="fd5f3-127">Entity Framework překládá C# modely používané WEBOVÝm rozhraním API do databázových entit.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="fd5f3-128">Následující diagram znázorňuje způsob reprezentace objektů domény v různých vrstvách aplikace: databázová vrstva, objektový model a nakonec formát drátu, který slouží k přenosu dat do klienta prostřednictvím protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="fd5f3-129">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd5f3-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="fd5f3-130">Můžete vytvořit projekt kurzu pomocí aplikace Visual Web Developer Express nebo plné verze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="fd5f3-131">Na **úvodní** stránce klikněte na **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="fd5f3-132">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** .</span><span class="sxs-lookup"><span data-stu-id="fd5f3-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="fd5f3-133">V **části C#vizuál** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="fd5f3-134">V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="fd5f3-135">Pojmenujte projekt "ProductStore" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="fd5f3-136">V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte možnost **Internet aplikace** a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="fd5f3-137">Šablona "Internetová aplikace" vytvoří aplikaci ASP.NET MVC, která podporuje ověřování formulářů.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="fd5f3-138">Pokud teď aplikaci spustíte, už obsahuje některé funkce:</span><span class="sxs-lookup"><span data-stu-id="fd5f3-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="fd5f3-139">Noví uživatelé se můžou zaregistrovat kliknutím na odkaz zaregistrovat v pravém horním rohu.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="fd5f3-140">Registrovaní uživatelé se můžou přihlásit kliknutím na odkaz Přihlásit se.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="fd5f3-141">Informace o členství jsou trvalé v databázi, která je vytvořena automaticky.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="fd5f3-142">Další informace o ověřování pomocí formulářů v ASP.NET MVC najdete v tématu [Návod: použití ověřování pomocí formulářů v ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span><span class="sxs-lookup"><span data-stu-id="fd5f3-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="fd5f3-143">Aktualizovat soubor CSS</span><span class="sxs-lookup"><span data-stu-id="fd5f3-143">Update the CSS File</span></span>

<span data-ttu-id="fd5f3-144">Tento krok je kosmetický, ale stránky se vykreslí jako dřívější snímky obrazovky.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="fd5f3-145">V Průzkumník řešení rozbalte složku obsahu a otevřete soubor s názvem site. CSS.</span><span class="sxs-lookup"><span data-stu-id="fd5f3-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="fd5f3-146">Přidejte následující styly CSS:</span><span class="sxs-lookup"><span data-stu-id="fd5f3-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="fd5f3-147">Next</span><span class="sxs-lookup"><span data-stu-id="fd5f3-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
