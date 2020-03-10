---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: Použití OWIN k samoobslužnému hostování ASP.NET webového rozhraní API – ASP.NET 4. x
author: rick-anderson
description: Kurz s kódem ukazujícím, jak hostovat webové rozhraní API ASP.NET v konzolové aplikaci.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556537"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="792ac-103">Použití OWIN k samoobslužnému hostování ASP.NET webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="792ac-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 

> <span data-ttu-id="792ac-104">V tomto kurzu se dozvíte, jak hostovat webové rozhraní API v ASP.NET v konzolové aplikaci pomocí OWIN pro samoobslužné hostování rozhraní Web API.</span><span class="sxs-lookup"><span data-stu-id="792ac-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="792ac-105">[Open Web Interface for .NET](http://owin.org) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="792ac-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="792ac-106">OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS.</span><span class="sxs-lookup"><span data-stu-id="792ac-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="792ac-107">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="792ac-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="792ac-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="792ac-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="792ac-109">Webové rozhraní API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="792ac-109">Web API 5.2.7</span></span>

> [!NOTE]
> <span data-ttu-id="792ac-110">Úplný zdrojový kód pro tento kurz najdete na adrese [GitHub.com/ASPNET/Samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span><span class="sxs-lookup"><span data-stu-id="792ac-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="792ac-111">Vytvoření konzolové aplikace</span><span class="sxs-lookup"><span data-stu-id="792ac-111">Create a console application</span></span>

<span data-ttu-id="792ac-112">V nabídce **soubor** klikněte na příkaz **Nový**a vyberte možnost **projekt**.</span><span class="sxs-lookup"><span data-stu-id="792ac-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="792ac-113">Z **instalace**vyberte v **části C#vizuál** možnost **Windows Desktop** a pak vyberte **Konzolová aplikace (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="792ac-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="792ac-114">Pojmenujte projekt "OwinSelfhostSample" a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="792ac-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="792ac-115">Přidat webové rozhraní API a balíčky OWIN</span><span class="sxs-lookup"><span data-stu-id="792ac-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="792ac-116">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="792ac-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="792ac-117">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="792ac-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="792ac-118">Tím se nainstaluje balíček SelfHost OWIN pro WebAPI a všechny požadované balíčky OWIN.</span><span class="sxs-lookup"><span data-stu-id="792ac-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="792ac-119">Konfigurace webového rozhraní API pro samoobslužné hostování</span><span class="sxs-lookup"><span data-stu-id="792ac-119">Configure Web API for self-host</span></span>

<span data-ttu-id="792ac-120">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a výběrem **přidat** / **třídu** přidejte novou třídu.</span><span class="sxs-lookup"><span data-stu-id="792ac-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="792ac-121">Pojmenujte `Startup`třídy.</span><span class="sxs-lookup"><span data-stu-id="792ac-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="792ac-122">Celý často používaný kód nahraďte tímto souborem:</span><span class="sxs-lookup"><span data-stu-id="792ac-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="792ac-123">Přidat kontroler webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="792ac-123">Add a Web API controller</span></span>

<span data-ttu-id="792ac-124">Dále přidejte třídu kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="792ac-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="792ac-125">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a výběrem **přidat** / **třídu** přidejte novou třídu.</span><span class="sxs-lookup"><span data-stu-id="792ac-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="792ac-126">Pojmenujte `ValuesController`třídy.</span><span class="sxs-lookup"><span data-stu-id="792ac-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="792ac-127">Celý často používaný kód nahraďte tímto souborem:</span><span class="sxs-lookup"><span data-stu-id="792ac-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="792ac-128">Spuštění hostitele OWIN a vytvoření žádosti pomocí HttpClient</span><span class="sxs-lookup"><span data-stu-id="792ac-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="792ac-129">Nahraďte celý často používaný kód v souboru Program.cs následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="792ac-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="792ac-130">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="792ac-130">Run the application</span></span>

<span data-ttu-id="792ac-131">Chcete-li spustit aplikaci, stiskněte klávesu F5 v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="792ac-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="792ac-132">Výstup by měl vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="792ac-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="792ac-133">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="792ac-133">Additional resources</span></span>

[<span data-ttu-id="792ac-134">Přehled projektu Katana</span><span class="sxs-lookup"><span data-stu-id="792ac-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="792ac-135">Hostování webového rozhraní API v ASP.NET v roli pracovního procesu Azure</span><span class="sxs-lookup"><span data-stu-id="792ac-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
