---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: Použití rozhraní OWIN k samoobslužnému hostování webového rozhraní API – ASP.NET ASP.NET 4.x
author: rick-anderson
description: Kurz s kódem ukazující, jak hostovat rozhraní ASP.NET Web API v konzolové aplikaci.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: a67db0bd061846af2db3599e0843ed7c6a22db1e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386512"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="ebc78-103">Použití rozhraní OWIN k samoobslužnému hostování webového rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ebc78-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 


> <span data-ttu-id="ebc78-104">Tento kurz ukazuje, jak hostovat v konzolové aplikaci, používá OWIN k samoobslužnému hostování webového rozhraní API rozhraní ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="ebc78-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="ebc78-105">[Otevřete Web Interface pro .NET](http://owin.org) (OWIN) definuje abstrakce mezi .NET webové servery a webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="ebc78-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="ebc78-106">OWIN odpojí webové aplikace ze serveru, který je ideální pro webové aplikace ve vašem vlastním procesu mimo službu IIS s vlastním hostováním OWIN.</span><span class="sxs-lookup"><span data-stu-id="ebc78-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ebc78-107">V tomto kurzu použili verze softwaru</span><span class="sxs-lookup"><span data-stu-id="ebc78-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="ebc78-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ebc78-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="ebc78-109">Web API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="ebc78-109">Web API 5.2.7</span></span>


> [!NOTE]
> <span data-ttu-id="ebc78-110">Úplný zdrojový kód můžete najít v tomto kurzu na [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span><span class="sxs-lookup"><span data-stu-id="ebc78-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="ebc78-111">Vytvoření konzolové aplikace</span><span class="sxs-lookup"><span data-stu-id="ebc78-111">Create a console application</span></span>

<span data-ttu-id="ebc78-112">Na **souboru** nabídce **nový**a pak vyberte **projektu**.</span><span class="sxs-lookup"><span data-stu-id="ebc78-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="ebc78-113">Z **nainstalováno**v části **Visual C#** vyberte **Windows Desktop** a pak vyberte **Konzolová aplikace (.Net Framework)**.</span><span class="sxs-lookup"><span data-stu-id="ebc78-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="ebc78-114">Zadejte název projektu "OwinSelfhostSample" a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebc78-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="ebc78-115">Přidejte balíčky webového rozhraní API a OWIN</span><span class="sxs-lookup"><span data-stu-id="ebc78-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="ebc78-116">Z **nástroje** příkaz **Správce balíčků NuGet**, vyberte **konzoly Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="ebc78-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ebc78-117">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="ebc78-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="ebc78-118">Tím se nainstaluje balíček selfhost WebAPI OWIN a všechny požadované balíčky OWIN.</span><span class="sxs-lookup"><span data-stu-id="ebc78-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="ebc78-119">Konfigurace webového rozhraní API pro hostování na vlastním serveru</span><span class="sxs-lookup"><span data-stu-id="ebc78-119">Configure Web API for self-host</span></span>

<span data-ttu-id="ebc78-120">V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **přidat** / **třídy** přidání nové třídy.</span><span class="sxs-lookup"><span data-stu-id="ebc78-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="ebc78-121">Název třídy `Startup`.</span><span class="sxs-lookup"><span data-stu-id="ebc78-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="ebc78-122">Nahraďte všechny často používaný kód v tomto souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="ebc78-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="ebc78-123">Přidat kontroler Web API</span><span class="sxs-lookup"><span data-stu-id="ebc78-123">Add a Web API controller</span></span>

<span data-ttu-id="ebc78-124">Dále přidejte třídu kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ebc78-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="ebc78-125">V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte **přidat** / **třídy** přidání nové třídy.</span><span class="sxs-lookup"><span data-stu-id="ebc78-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="ebc78-126">Název třídy `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="ebc78-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="ebc78-127">Nahraďte všechny často používaný kód v tomto souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="ebc78-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="ebc78-128">Spuštění hostitele OWIN a poslat žádost s HttpClient</span><span class="sxs-lookup"><span data-stu-id="ebc78-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="ebc78-129">Nahraďte všechny často používaný kód v souboru Program.cs následujícími způsoby:</span><span class="sxs-lookup"><span data-stu-id="ebc78-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="ebc78-130">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="ebc78-130">Run the application</span></span>

<span data-ttu-id="ebc78-131">Spusťte aplikaci stisknutím klávesy F5 v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebc78-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="ebc78-132">Výstup by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="ebc78-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="ebc78-133">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="ebc78-133">Additional resources</span></span>

[<span data-ttu-id="ebc78-134">Přehled projektu Katana</span><span class="sxs-lookup"><span data-stu-id="ebc78-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="ebc78-135">Hostování webového rozhraní API ASP.NET v roli pracovního procesu Azure</span><span class="sxs-lookup"><span data-stu-id="ebc78-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
