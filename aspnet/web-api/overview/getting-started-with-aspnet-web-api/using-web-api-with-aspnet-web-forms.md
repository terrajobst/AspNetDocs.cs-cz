---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Použití webového rozhraní API s ASP.NET webovými formuláři – ASP.NET 4. x
author: MikeWasson
description: Kurz s kódem krok za krokem k přidání webového rozhraní API do aplikace ASP.NET Forms pro ASP.NET 4. x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556775"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="9f1f3-103">Použití rozhraní Web API s webovými formuláři ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9f1f3-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="9f1f3-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9f1f3-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9f1f3-105">Tento kurz vás provede jednotlivými kroky přidání webového rozhraní API do tradiční aplikace webových formulářů ASP.NET v ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="9f1f3-106">Přehled</span><span class="sxs-lookup"><span data-stu-id="9f1f3-106">Overview</span></span>

<span data-ttu-id="9f1f3-107">I když je webové rozhraní API ASP.NET zabalené s ASP.NET MVC, je snadné přidat webové rozhraní API do tradiční aplikace webové formuláře ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="9f1f3-108">Chcete-li použít webové rozhraní API v aplikaci webových formulářů, existují dva hlavní kroky:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="9f1f3-109">Přidejte kontroler webového rozhraní API, který je odvozený od třídy **ApiController** .</span><span class="sxs-lookup"><span data-stu-id="9f1f3-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="9f1f3-110">Přidejte směrovací tabulku do **aplikace\_spustit** metodu.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="9f1f3-111">Vytvoření projektu webových formulářů</span><span class="sxs-lookup"><span data-stu-id="9f1f3-111">Create a Web Forms Project</span></span>

<span data-ttu-id="9f1f3-112">Spusťte Visual Studio a na **úvodní** stránce vyberte **Nový projekt** .</span><span class="sxs-lookup"><span data-stu-id="9f1f3-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="9f1f3-113">Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="9f1f3-114">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** .</span><span class="sxs-lookup"><span data-stu-id="9f1f3-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="9f1f3-115">V **části C#vizuál** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="9f1f3-116">V seznamu šablon projektu vyberte **ASP.NET aplikace webových formulářů**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="9f1f3-117">Zadejte název projektu a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="9f1f3-118">Vytvoření modelu a kontroleru</span><span class="sxs-lookup"><span data-stu-id="9f1f3-118">Create the Model and Controller</span></span>

<span data-ttu-id="9f1f3-119">V tomto kurzu se jako [Začínáme](tutorial-your-first-web-api.md) kurz používá stejný model a třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="9f1f3-120">Nejprve přidejte třídu modelu.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-120">First, add a model class.</span></span> <span data-ttu-id="9f1f3-121">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat třídu**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="9f1f3-122">Pojmenujte produkt třídy a přidejte následující implementaci:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="9f1f3-123">V dalším kroku přidejte do projektu kontroler webového rozhraní API. *kontroler* je objekt, který zpracovává požadavky HTTP na webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="9f1f3-124">V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="9f1f3-125">Vyberte možnost **Přidat novou položku**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="9f1f3-126">V části **Nainstalované šablony**rozbalte **položku C# vizuál** a vyberte možnost **Web**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="9f1f3-127">Pak ze seznamu šablon vyberte **Třída kontroleru webového rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="9f1f3-128">Pojmenujte kontroler "ProductsController" a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="9f1f3-129">Průvodce **přidáním nové položky** vytvoří soubor s názvem ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="9f1f3-130">Odstraňte metody, které průvodce zahrnul, a přidejte následující metody:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="9f1f3-131">Další informace o kódu v tomto kontroleru najdete v kurzu [Začínáme](tutorial-your-first-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="9f1f3-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="9f1f3-132">Přidat informace o směrování</span><span class="sxs-lookup"><span data-stu-id="9f1f3-132">Add Routing Information</span></span>

<span data-ttu-id="9f1f3-133">Dále přidáte trasu identifikátoru URI, aby byly identifikátory URI formuláře &quot;/API/Products/&quot; směrovány do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="9f1f3-134">V **Průzkumník řešení**dvakrát klikněte na Global. asax a otevřete soubor kódu na pozadí Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="9f1f3-135">Přidejte následující příkaz **using** .</span><span class="sxs-lookup"><span data-stu-id="9f1f3-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="9f1f3-136">Poté do aplikace přidejte následující kód **\_počáteční** metoda:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="9f1f3-137">Další informace o směrovacích tabulkách najdete v tématu [směrování ve webovém rozhraní API ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="9f1f3-138">Add Client-Side AJAX</span><span class="sxs-lookup"><span data-stu-id="9f1f3-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="9f1f3-139">To je všechno, co potřebujete k vytvoření webového rozhraní API, ke kterému mají přístup klienti.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="9f1f3-140">Nyní přidáme stránku HTML, která používá jQuery k volání rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="9f1f3-141">Ujistěte se, že vaše stránka předlohy (například *site. Master*) obsahuje `ContentPlaceHolder` `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="9f1f3-142">Otevřete soubor default. aspx.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-142">Open the file Default.aspx.</span></span> <span data-ttu-id="9f1f3-143">Nahraďte často používaný text v části hlavní obsah, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="9f1f3-144">Dále do oddílu `HeaderContent` přidejte odkaz na zdrojový soubor jQuery:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="9f1f3-145">Poznámka: odkaz na skript lze snadno přidat přetažením z **Průzkumník řešení** do okna Editor kódu.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="9f1f3-146">Pod značkou skriptu jQuery přidejte následující blok skriptu:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="9f1f3-147">Když se dokument načte, vytvoří tento skript požadavek AJAX, aby &quot;API/Products&quot;.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="9f1f3-148">Požadavek vrátí seznam produktů ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="9f1f3-149">Skript přidá informace o produktu do tabulky HTML.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="9f1f3-150">Při spuštění aplikace by měla vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
