---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC – Přehled směrování (VB) | Microsoft Docs
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak Framework ASP.NET MVC mapuje požadavky prohlížeče na akce kontroleru.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601533"
---
# <a name="aspnet-mvc-routing-overview-vb"></a><span data-ttu-id="550b3-103">ASP.NET MVC – přehled směrování (VB)</span><span class="sxs-lookup"><span data-stu-id="550b3-103">ASP.NET MVC Routing Overview (VB)</span></span>

<span data-ttu-id="550b3-104">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="550b3-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="550b3-105">V tomto kurzu Stephen Walther ukazuje, jak Framework ASP.NET MVC mapuje požadavky prohlížeče na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="550b3-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="550b3-106">V tomto kurzu se zavedete na důležitou funkci každé aplikace ASP.NET MVC s názvem *směrování ASP.NET*.</span><span class="sxs-lookup"><span data-stu-id="550b3-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="550b3-107">Modul směrování ASP.NET zodpovídá za mapování příchozích požadavků prohlížeče na konkrétní akce kontroleru MVC.</span><span class="sxs-lookup"><span data-stu-id="550b3-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="550b3-108">Na konci tohoto kurzu budete rozumět tomu, jak standardní směrovací tabulka vyžádá požadavky na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="550b3-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="550b3-109">Použití výchozí směrovací tabulky</span><span class="sxs-lookup"><span data-stu-id="550b3-109">Using the Default Route Table</span></span>

<span data-ttu-id="550b3-110">Když vytvoříte novou aplikaci ASP.NET MVC, aplikace je už nakonfigurovaná tak, aby používala směrování ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="550b3-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="550b3-111">Směrování ASP.NET se nastaví na dvou místech.</span><span class="sxs-lookup"><span data-stu-id="550b3-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="550b3-112">V konfiguračním souboru webu aplikace (soubor Web. config) je nejprve povoleno směrování ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="550b3-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="550b3-113">Konfigurační soubor obsahuje čtyři části, které jsou důležité pro směrování: oddíl System. Web. httpModules, System. Web. httpHandlers, System. webServer. Modules a System. webServer. handlers.</span><span class="sxs-lookup"><span data-stu-id="550b3-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="550b3-114">Dejte pozor, abyste tyto oddíly neodstranili, protože bez těchto oddílů nebude směrování nadále fungovat.</span><span class="sxs-lookup"><span data-stu-id="550b3-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="550b3-115">Druhé a důležitější je, že směrovací tabulka se vytvoří v souboru Global. asax aplikace.</span><span class="sxs-lookup"><span data-stu-id="550b3-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="550b3-116">Soubor Global. asax je speciální soubor, který obsahuje obslužné rutiny událostí pro události životního cyklu aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="550b3-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="550b3-117">Směrovací tabulka se vytvoří během události spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="550b3-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="550b3-118">Soubor v seznamu 1 obsahuje výchozí soubor Global. asax pro aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="550b3-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="550b3-119">**Výpis 1 – Global. asax. vb**</span><span class="sxs-lookup"><span data-stu-id="550b3-119">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

<span data-ttu-id="550b3-120">Při prvním spuštění aplikace MVC je volána metoda aplikace\_Start ().</span><span class="sxs-lookup"><span data-stu-id="550b3-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="550b3-121">Tato metoda pak zavolá metodu RegisterRoutes ().</span><span class="sxs-lookup"><span data-stu-id="550b3-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="550b3-122">Metoda RegisterRoutes () vytvoří směrovací tabulku.</span><span class="sxs-lookup"><span data-stu-id="550b3-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="550b3-123">Výchozí směrovací tabulka obsahuje jednu trasu (s názvem Default).</span><span class="sxs-lookup"><span data-stu-id="550b3-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="550b3-124">Výchozí trasa namapuje první segment adresy URL na název kontroleru, druhý segment adresy URL na akci kontroleru a třetí segment na parametr s názvem **ID**.</span><span class="sxs-lookup"><span data-stu-id="550b3-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="550b3-125">Představte si, že do adresního řádku webového prohlížeče zadáte následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="550b3-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="550b3-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="550b3-126">/Home/Index/3</span></span>

<span data-ttu-id="550b3-127">Výchozí trasa mapuje tuto adresu URL na následující parametry:</span><span class="sxs-lookup"><span data-stu-id="550b3-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="550b3-128">Controller = domů</span><span class="sxs-lookup"><span data-stu-id="550b3-128">controller = Home</span></span>

- <span data-ttu-id="550b3-129">Action = index</span><span class="sxs-lookup"><span data-stu-id="550b3-129">action = Index</span></span>

- <span data-ttu-id="550b3-130">id = 3</span><span class="sxs-lookup"><span data-stu-id="550b3-130">id = 3</span></span>

<span data-ttu-id="550b3-131">Po vyžádání adresy URL/Home/Index/3 se spustí následující kód:</span><span class="sxs-lookup"><span data-stu-id="550b3-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="550b3-132">HomeController. index (3)</span><span class="sxs-lookup"><span data-stu-id="550b3-132">HomeController.Index(3)</span></span>

<span data-ttu-id="550b3-133">Výchozí trasa obsahuje výchozí hodnoty pro všechny tři parametry.</span><span class="sxs-lookup"><span data-stu-id="550b3-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="550b3-134">Pokud řadič nezadáte, použije se výchozí hodnota parametru Controller na hodnotu **Home**.</span><span class="sxs-lookup"><span data-stu-id="550b3-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="550b3-135">Pokud akci nezadáte, použije se jako výchozí parametr akce **index**hodnoty.</span><span class="sxs-lookup"><span data-stu-id="550b3-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="550b3-136">Nakonec, pokud nezadáte ID, parametr ID se nastaví jako prázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="550b3-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="550b3-137">Pojďme se podívat na několik příkladů, jak výchozí trasa mapuje adresy URL na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="550b3-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="550b3-138">Představte si, že do adresního řádku prohlížeče zadáte následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="550b3-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="550b3-139">/Home</span><span class="sxs-lookup"><span data-stu-id="550b3-139">/Home</span></span>

<span data-ttu-id="550b3-140">Z důvodu výchozí výchozí hodnoty parametrů trasy bude zadání této adresy URL způsobit volání metody index () třídy HomeController v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="550b3-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="550b3-141">**Výpis 2-HomeController. vb**</span><span class="sxs-lookup"><span data-stu-id="550b3-141">**Listing 2 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

<span data-ttu-id="550b3-142">V seznamu 2 třída HomeController obsahuje metodu s názvem index (), která přijímá jeden parametr s názvem ID. Adresa URL/Home způsobí, že metoda index () bude volána s hodnotou Nothing jako hodnota parametru ID.</span><span class="sxs-lookup"><span data-stu-id="550b3-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with the value Nothing as the value of the Id parameter.</span></span>

<span data-ttu-id="550b3-143">Z důvodu způsobu, jakým rozhraní MVC Framework vyvolá akce kontroleru, adresa URL/Home také odpovídá metodě index () třídy HomeController v seznamu 3.</span><span class="sxs-lookup"><span data-stu-id="550b3-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="550b3-144">**Výpis 3-HomeController. vb (akce indexu bez parametru)**</span><span class="sxs-lookup"><span data-stu-id="550b3-144">**Listing 3 - HomeController.vb (Index action with no parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

<span data-ttu-id="550b3-145">Metoda index () v seznamu 3 nepřijímá žádné parametry.</span><span class="sxs-lookup"><span data-stu-id="550b3-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="550b3-146">Adresa URL/Home způsobí volání této metody index ().</span><span class="sxs-lookup"><span data-stu-id="550b3-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="550b3-147">Adresa URL/Home/Index/3 také vyvolá tuto metodu (ID je ignorováno).</span><span class="sxs-lookup"><span data-stu-id="550b3-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="550b3-148">Adresa URL/Home také odpovídá metodě index () třídy HomeController v seznamu 4.</span><span class="sxs-lookup"><span data-stu-id="550b3-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="550b3-149">**Výpis 4-HomeController. vb (akce indexu s parametrem s možnou hodnotou null)**</span><span class="sxs-lookup"><span data-stu-id="550b3-149">**Listing 4 - HomeController.vb (Index action with nullable parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

<span data-ttu-id="550b3-150">V seznamu 4 má metoda index () jeden celočíselný parametr.</span><span class="sxs-lookup"><span data-stu-id="550b3-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="550b3-151">Vzhledem k tomu, že parametr je parametr s možnou hodnotou null (může mít hodnotu Nothing), index () lze volat bez vyvolání chyby.</span><span class="sxs-lookup"><span data-stu-id="550b3-151">Because the parameter is a nullable parameter (can have the value Nothing), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="550b3-152">Nakonec volání metody index () v seznamu 5 s adresou URL/Home způsobí výjimku, protože parametr *ID není parametr s* možnou hodnotou null.</span><span class="sxs-lookup"><span data-stu-id="550b3-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="550b3-153">Pokud se pokusíte vyvolat metodu index (), zobrazí se chyba na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="550b3-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="550b3-154">**Výpis 5-HomeController. vb (akce indexu s parametrem ID)**</span><span class="sxs-lookup"><span data-stu-id="550b3-154">**Listing 5 - HomeController.vb (Index action with Id parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

<span data-ttu-id="550b3-155">[![volání akce kontroleru, která očekává hodnotu parametru.](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="550b3-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="550b3-156">**Obrázek 01**: vyvolání akce kontroleru, která očekává hodnotu parametru ([kliknutím zobrazíte obrázek v plné velikosti](asp-net-mvc-routing-overview-vb/_static/image2.png)).</span><span class="sxs-lookup"><span data-stu-id="550b3-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="550b3-157">Adresa URL/Home/Index/3 na druhé straně funguje pouze v případě, že se jedná o akci řadiče indexu v seznamu 5.</span><span class="sxs-lookup"><span data-stu-id="550b3-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="550b3-158">Požadavek/Home/Index/3 způsobí, že metoda index () bude volána s parametrem ID, který má hodnotu 3.</span><span class="sxs-lookup"><span data-stu-id="550b3-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="550b3-159">Souhrn</span><span class="sxs-lookup"><span data-stu-id="550b3-159">Summary</span></span>

<span data-ttu-id="550b3-160">Cílem tohoto kurzu je poskytnout stručný úvod k ASP.NET směrování.</span><span class="sxs-lookup"><span data-stu-id="550b3-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="550b3-161">Prozkoumali jsme výchozí směrovací tabulku, kterou získáte pomocí nové aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="550b3-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="550b3-162">Zjistili jste, jak výchozí trasa mapuje adresy URL na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="550b3-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="550b3-163">[Předchozí](creating-an-action-cs.md)
> [Další](understanding-action-filters-vb.md)</span><span class="sxs-lookup"><span data-stu-id="550b3-163">[Previous](creating-an-action-cs.md)
[Next](understanding-action-filters-vb.md)</span></span>
