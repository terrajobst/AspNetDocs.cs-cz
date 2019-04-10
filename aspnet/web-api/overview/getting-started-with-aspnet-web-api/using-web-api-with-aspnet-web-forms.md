---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Použití rozhraní Web API s webovými formuláři ASP.NET – ASP.NET 4.x
author: MikeWasson
description: Výukový program s kódem krok za krokem k přidání webového rozhraní API do aplikace formuláře ASP.NET pro technologii ASP.NET 4.x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422574"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="5527c-103">Použití webového rozhraní API s webovými formuláři ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5527c-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="5527c-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5527c-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5527c-105">Tento kurz vás provede kroky k přidání webového rozhraní API pro tradiční aplikace webových formulářů ASP.NET v technologii ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="5527c-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="5527c-106">Přehled</span><span class="sxs-lookup"><span data-stu-id="5527c-106">Overview</span></span>

<span data-ttu-id="5527c-107">Přestože je součástí balíčku rozhraní ASP.NET Web API ASP.NET MVC, je jednoduše přidávat webového rozhraní API pro tradiční aplikace webových formulářů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5527c-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="5527c-108">Použití webového rozhraní API v aplikaci webových formulářů, existují dva hlavní kroky:</span><span class="sxs-lookup"><span data-stu-id="5527c-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="5527c-109">Přidání kontroleru webového rozhraní API, která je odvozena z **objektu ApiController** třídy.</span><span class="sxs-lookup"><span data-stu-id="5527c-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="5527c-110">Přidat do směrovací tabulky **aplikace\_Start** metoda.</span><span class="sxs-lookup"><span data-stu-id="5527c-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="5527c-111">Vytvořte projekt webových formulářů</span><span class="sxs-lookup"><span data-stu-id="5527c-111">Create a Web Forms Project</span></span>

<span data-ttu-id="5527c-112">Spusťte sadu Visual Studio a vyberte **nový projekt** z **Start** stránky.</span><span class="sxs-lookup"><span data-stu-id="5527c-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="5527c-113">Nebo z **souboru** nabídce vyberte možnost **nový** a potom **projektu**.</span><span class="sxs-lookup"><span data-stu-id="5527c-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="5527c-114">V **šablony** vyberte **nainstalované šablony** a rozbalte **Visual C#** uzlu.</span><span class="sxs-lookup"><span data-stu-id="5527c-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="5527c-115">V části **Visual C#** vyberte **webové**.</span><span class="sxs-lookup"><span data-stu-id="5527c-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="5527c-116">V seznamu šablon projektu vyberte **aplikace webových formulářů ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="5527c-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="5527c-117">Zadejte název projektu a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="5527c-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="5527c-118">Vytvoření modelu a kontroler</span><span class="sxs-lookup"><span data-stu-id="5527c-118">Create the Model and Controller</span></span>

<span data-ttu-id="5527c-119">Tento kurz používá stejné třídy modelu a kontroler jako [Začínáme](tutorial-your-first-web-api.md) kurzu.</span><span class="sxs-lookup"><span data-stu-id="5527c-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="5527c-120">Nejprve přidejte třídu modelu.</span><span class="sxs-lookup"><span data-stu-id="5527c-120">First, add a model class.</span></span> <span data-ttu-id="5527c-121">V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt a vyberte **přidat třídu**.</span><span class="sxs-lookup"><span data-stu-id="5527c-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="5527c-122">Název třídy produktu a přidejte následující implementaci:</span><span class="sxs-lookup"><span data-stu-id="5527c-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="5527c-123">Kontroler Web API v dalším kroku přidejte do projektu., A *řadič* je objekt, který zpracovává požadavky HTTP pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5527c-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="5527c-124">V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt.</span><span class="sxs-lookup"><span data-stu-id="5527c-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="5527c-125">Vyberte **přidat novou položku**.</span><span class="sxs-lookup"><span data-stu-id="5527c-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="5527c-126">V části **nainstalované šablony**, rozbalte **Visual C#** a vyberte **webové**.</span><span class="sxs-lookup"><span data-stu-id="5527c-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="5527c-127">Vyberte ze seznamu šablon **třída Kontroleru rozhraní Web API**.</span><span class="sxs-lookup"><span data-stu-id="5527c-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="5527c-128">Název kontroleru "ProductsController" a klikněte na **přidat**.</span><span class="sxs-lookup"><span data-stu-id="5527c-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="5527c-129">**Přidat novou položku** průvodce vytvořit soubor s názvem ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="5527c-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="5527c-130">Odstranit metody, které jsou zahrnuty v průvodci a přidejte následující metody:</span><span class="sxs-lookup"><span data-stu-id="5527c-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="5527c-131">Další informace o kódu v tomto kontroleru, najdete v článku [Začínáme](tutorial-your-first-web-api.md) kurzu.</span><span class="sxs-lookup"><span data-stu-id="5527c-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="5527c-132">Přidat informace o směrování</span><span class="sxs-lookup"><span data-stu-id="5527c-132">Add Routing Information</span></span>

<span data-ttu-id="5527c-133">V dalším kroku přidáme trasu URI tak tento identifikátory URI formuláře &quot;/webové rozhraníAPI/produkty/&quot; se směrují do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5527c-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="5527c-134">V **Průzkumníka řešení**, dvakrát klikněte pro otevření souboru modelu code-behind Global.asax.cs Global.asax.</span><span class="sxs-lookup"><span data-stu-id="5527c-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="5527c-135">Přidejte následující **pomocí** příkazu.</span><span class="sxs-lookup"><span data-stu-id="5527c-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="5527c-136">Pak přidejte následující kód, který **aplikace\_Start** metody:</span><span class="sxs-lookup"><span data-stu-id="5527c-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="5527c-137">Další informace o směrovacích tabulek naleznete v tématu [směrování v rozhraní ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="5527c-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="5527c-138">Add Client-Side AJAX</span><span class="sxs-lookup"><span data-stu-id="5527c-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="5527c-139">To je všechno, co potřebujete k vytvoření webového rozhraní API, které mohou klienti získat přístup.</span><span class="sxs-lookup"><span data-stu-id="5527c-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="5527c-140">Nyní Pojďme přidat stránku HTML, který používá jQuery pro volání rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5527c-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="5527c-141">Ujistěte se, že stránky předlohy (například *Site.Master*) zahrnuje `ContentPlaceHolder` s `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="5527c-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="5527c-142">Otevřete soubor Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="5527c-142">Open the file Default.aspx.</span></span> <span data-ttu-id="5527c-143">Jak je znázorněno, nahraďte často používaný text, který je v obsahu hlavní části:</span><span class="sxs-lookup"><span data-stu-id="5527c-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="5527c-144">V dalším kroku přidáte odkaz na zdrojový soubor jQuery v `HeaderContent` části:</span><span class="sxs-lookup"><span data-stu-id="5527c-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="5527c-145">Poznámka: Můžete snadno přidat odkaz na skript přetažením souboru z **Průzkumníka řešení** do okna editoru kódu.</span><span class="sxs-lookup"><span data-stu-id="5527c-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="5527c-146">Pod značku skriptu jQuery přidejte následující blok skriptu:</span><span class="sxs-lookup"><span data-stu-id="5527c-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="5527c-147">Po načtení dokumentu tento skript vytvoří požadavek AJAX &quot;produktů s rozhranímapi/&quot;.</span><span class="sxs-lookup"><span data-stu-id="5527c-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="5527c-148">Požadavek vrátí seznam produktů ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="5527c-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="5527c-149">Skript přidá informace o produktu do tabulky HTML.</span><span class="sxs-lookup"><span data-stu-id="5527c-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="5527c-150">Při spuštění aplikace by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="5527c-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
