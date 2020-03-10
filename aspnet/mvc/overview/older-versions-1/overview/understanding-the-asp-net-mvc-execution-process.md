---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Principy procesu provádění ASP.NET MVC | Microsoft Docs
author: microsoft
description: Přečtěte si, jak rozhraní ASP.NET MVC zpracovává požadavky prohlížeče krok za krokem.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541515"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="8bd97-103">Principy procesu spuštění ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8bd97-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="8bd97-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8bd97-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8bd97-105">Přečtěte si, jak rozhraní ASP.NET MVC zpracovává požadavky prohlížeče krok za krokem.</span><span class="sxs-lookup"><span data-stu-id="8bd97-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="8bd97-106">Požadavky na webovou aplikaci založenou na ASP.NET MVC se nejdřív procházejí objektem **UrlRoutingModule** , který je modulem http.</span><span class="sxs-lookup"><span data-stu-id="8bd97-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="8bd97-107">Tento modul analyzuje požadavek a provede výběr směrování.</span><span class="sxs-lookup"><span data-stu-id="8bd97-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="8bd97-108">Objekt **UrlRoutingModule** vybere první objekt směrování, který odpovídá aktuálnímu požadavku.</span><span class="sxs-lookup"><span data-stu-id="8bd97-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="8bd97-109">(Objekt směrování je třída, která implementuje **RouteBase**a je obvykle instancí třídy **Směrování** .) Pokud se žádné trasy neshodují, objekt **UrlRoutingModule** neprovede žádnou akci a umožní, aby se požadavek vrátil do normálního zpracování žádosti ASP.NET nebo služby IIS.</span><span class="sxs-lookup"><span data-stu-id="8bd97-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="8bd97-110">Z vybraného objektu **Směrování** Získá objekt **UrlRoutingModule** objekt **IRouteHandler** , který je spojen s objektem **Směrování** .</span><span class="sxs-lookup"><span data-stu-id="8bd97-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="8bd97-111">Obvykle se v aplikaci MVC jedná o instanci **MvcRouteHandler**.</span><span class="sxs-lookup"><span data-stu-id="8bd97-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="8bd97-112">Instance **IRouteHandler** vytvoří objekt **IHttpHandler** a předá ho objektu **IHttpContext** .</span><span class="sxs-lookup"><span data-stu-id="8bd97-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="8bd97-113">Ve výchozím nastavení je instance **IHttpHandler** pro MVC objektem **MvcHandler** .</span><span class="sxs-lookup"><span data-stu-id="8bd97-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="8bd97-114">Objekt **MvcHandler** pak vybere kontroler, který požadavek nakonec zpracuje.</span><span class="sxs-lookup"><span data-stu-id="8bd97-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd97-115">Když webová aplikace MVC v ASP.NET běží ve službě IIS 7,0, není pro projekty MVC potřeba žádná přípona názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="8bd97-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="8bd97-116">Ve službě IIS 6,0 však obslužná rutina vyžaduje mapování názvu souboru. Mvc na knihovnu DLL ASP.NET ISAPI.</span><span class="sxs-lookup"><span data-stu-id="8bd97-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="8bd97-117">Modul a obslužná rutina jsou vstupními body rozhraní ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="8bd97-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="8bd97-118">Provádějí tyto akce:</span><span class="sxs-lookup"><span data-stu-id="8bd97-118">They perform the following actions:</span></span>

- <span data-ttu-id="8bd97-119">Vyberte příslušný kontroler ve webové aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="8bd97-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="8bd97-120">Získat konkrétní instanci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="8bd97-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="8bd97-121">Zavolejte metodu **Execute** řadiče.</span><span class="sxs-lookup"><span data-stu-id="8bd97-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="8bd97-122">Následující seznam obsahuje fáze provádění pro webový projekt MVC:</span><span class="sxs-lookup"><span data-stu-id="8bd97-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="8bd97-123">Přijetí první žádosti o aplikaci</span><span class="sxs-lookup"><span data-stu-id="8bd97-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="8bd97-124">V souboru Global. asax jsou objekty **Směrování** přidány do objektu **Route** .</span><span class="sxs-lookup"><span data-stu-id="8bd97-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="8bd97-125">Provést směrování</span><span class="sxs-lookup"><span data-stu-id="8bd97-125">Perform routing</span></span> 

    - <span data-ttu-id="8bd97-126">Modul **UrlRoutingModule** používá první vyhovující objekt **Směrování** **v kolekci metody** pro vytvoření objektu **parametr RouteData** , který potom používá k vytvoření objektu **Třída requestContext** (**IHttpContext**).</span><span class="sxs-lookup"><span data-stu-id="8bd97-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="8bd97-127">Obslužná rutina žádosti o vytvoření MVC</span><span class="sxs-lookup"><span data-stu-id="8bd97-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="8bd97-128">Objekt **MvcRouteHandler** vytvoří instanci třídy **MvcHandler** a předá ji instanci **Třída requestContext** .</span><span class="sxs-lookup"><span data-stu-id="8bd97-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="8bd97-129">Vytvořit kontroler</span><span class="sxs-lookup"><span data-stu-id="8bd97-129">Create controller</span></span> 

    - <span data-ttu-id="8bd97-130">Objekt **MvcHandler** používá instanci **Třída requestContext** k identifikaci objektu **IControllerFactory** (obvykle instancí třídy **DefaultControllerFactory** ) k vytvoření instance kontroleru pomocí.</span><span class="sxs-lookup"><span data-stu-id="8bd97-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="8bd97-131">Spustit kontroler – instance **MvcHandler** volá metodu **Execute** příkazu Controller.</span><span class="sxs-lookup"><span data-stu-id="8bd97-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="8bd97-132">Vyvolat akci</span><span class="sxs-lookup"><span data-stu-id="8bd97-132">Invoke action</span></span> 

    - <span data-ttu-id="8bd97-133">Většina řadičů dědí ze základní třídy **řadiče** .</span><span class="sxs-lookup"><span data-stu-id="8bd97-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="8bd97-134">Pro řadiče, které to dělají, určí objekt **ControllerActionInvoker** , který je přidružen k řadiči, metodu Action třídy Controller, která má být volána, a poté zavolá tuto metodu.</span><span class="sxs-lookup"><span data-stu-id="8bd97-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="8bd97-135">Výsledek provedení</span><span class="sxs-lookup"><span data-stu-id="8bd97-135">Execute result</span></span> 

    - <span data-ttu-id="8bd97-136">Typická metoda Action může obdržet uživatelský vstup, připravit příslušná data odpovědi a pak výsledek spustit vrácením typu výsledku.</span><span class="sxs-lookup"><span data-stu-id="8bd97-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="8bd97-137">Předdefinované typy výsledků, které lze provést, zahrnují následující: **ViewResult** (který vykresluje zobrazení a je nejčastěji používaný výsledný typ), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**a **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="8bd97-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
