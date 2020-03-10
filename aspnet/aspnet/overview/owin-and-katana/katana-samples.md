---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Ukázky Katana | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584558"
---
# <a name="katana-samples"></a><span data-ttu-id="65867-102">Příklady použití sady Katana</span><span class="sxs-lookup"><span data-stu-id="65867-102">Katana Samples</span></span>

<span data-ttu-id="65867-103">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="65867-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="65867-104">Příklady použití sady Katana</span><span class="sxs-lookup"><span data-stu-id="65867-104">Katana Samples</span></span>

<span data-ttu-id="65867-105">**ASP.NET Routes Sample** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="65867-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="65867-106">V některých aplikacích budete chtít zapojit součásti OWIN do tabulky směrování Asp.Net vedle sebe pomocí jiných než OWIN komponent.</span><span class="sxs-lookup"><span data-stu-id="65867-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="65867-107">V této ukázce se dozvíte, jak používat metody rozšíření RouteCollection MapOwinPath a MapOwinRoute, které poskytuje Microsoft. Owin. Host. SystemWeb.</span><span class="sxs-lookup"><span data-stu-id="65867-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="65867-108">**Ukázka zřetězení kanálů** | [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="65867-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="65867-109">Kanály zpracování požadavků OWIN nemusí být lineární, můžou být větví na zpracování požadavků různými způsoby.</span><span class="sxs-lookup"><span data-stu-id="65867-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="65867-110">V této ukázce se dozvíte, jak vytvořit větvení kanál na základě cest požadavků nebo jiných dat požadavků, jako jsou hlavičky.</span><span class="sxs-lookup"><span data-stu-id="65867-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="65867-111">Tyto součásti jsou k dispozici v balíčku NuGet Microsoft. Owin. Mapping.</span><span class="sxs-lookup"><span data-stu-id="65867-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="65867-112">Ukázka [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) | **vlastního serveru** </span><span class="sxs-lookup"><span data-stu-id="65867-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="65867-113">Ukazuje, jak používat vlastní server OWIN při vlastním hostování OWIN.</span><span class="sxs-lookup"><span data-stu-id="65867-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="65867-114">**Vložený vzorový ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="65867-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="65867-115">Některé servery OWIN lze spustit v rámci vlastního procesu (&quot;&quot;v místním prostředí).</span><span class="sxs-lookup"><span data-stu-id="65867-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="65867-116">V této ukázce se dozvíte, jak spustit aplikaci OWIN pomocí nástrojů poskytovaných balíčkem NuGet Microsoft. Owin. Hosting.</span><span class="sxs-lookup"><span data-stu-id="65867-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="65867-117">**Ukázka HelloWorld** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="65867-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="65867-118">OWIN je abstrakce rozhraní API HTTP serveru, která umožňuje přenositelnost aplikace napříč různými servery.</span><span class="sxs-lookup"><span data-stu-id="65867-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="65867-119">Tato ukázka předvádí, jak psát Hello World aplikace pomocí některých **jednoduchých obálek** kolem nezpracovaného Owin abstrakce a jak ji spustit na webovém serveru, jako je ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="65867-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="65867-120">Ukázkový [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin) **Hello World Owin RAW** | </span><span class="sxs-lookup"><span data-stu-id="65867-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="65867-121">Tato ukázka předvádí, jak napsat aplikaci Hello World s využitím **nezpracovaného** abstrakce Owin a jak ji spustit na webovém serveru, jako je ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="65867-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="65867-122">**Ukázka signalizace** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="65867-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="65867-123">Ukazuje, jak používat k samoobslužnému hostování signál pomocí OWIN/Katana.</span><span class="sxs-lookup"><span data-stu-id="65867-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="65867-124">Další informace o signálu pro samoobslužné hostování najdete v tématu [kurz: samoobslužný hostitel signálu](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="65867-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="65867-125">Ukázka  [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) | **statických souborů**</span><span class="sxs-lookup"><span data-stu-id="65867-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="65867-126">Ukazuje, jak podporovat požadavky HTTP pro statické soubory pomocí OWIN/Katana.</span><span class="sxs-lookup"><span data-stu-id="65867-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="65867-127"> | [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) **webového rozhraní API** </span><span class="sxs-lookup"><span data-stu-id="65867-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="65867-128">V této ukázce se dozvíte, jak hostovat OWIN ve službě IIS a přidat webové rozhraní API do kanálu OWIN.</span><span class="sxs-lookup"><span data-stu-id="65867-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="65867-129">Ukázkový [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) | **webového soketu** </span><span class="sxs-lookup"><span data-stu-id="65867-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="65867-130">Ukazuje, jak podporovat webové sokety v OWIN pomocí třídy [System .NET. WebSockets.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) WebSocket.</span><span class="sxs-lookup"><span data-stu-id="65867-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
