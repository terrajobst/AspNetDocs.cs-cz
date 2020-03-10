---
uid: webhooks/receiving/dependencies
title: Závislosti přijímače webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Závislosti přijímače a injektáže závislostí v webhookech ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637282"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="ee14a-103">Závislosti přijímače webhooků ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ee14a-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="ee14a-104">Microsoft ASP.NET webhooků je navržená s ohledem na injektáže závislostí.</span><span class="sxs-lookup"><span data-stu-id="ee14a-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="ee14a-105">Většina závislostí v systému se dá nahradit alternativními implementacemi pomocí modulu injektáže závislostí.</span><span class="sxs-lookup"><span data-stu-id="ee14a-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="ee14a-106">Seznam závislostí přijímače najdete v tématu [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) .</span><span class="sxs-lookup"><span data-stu-id="ee14a-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="ee14a-107">Pokud není zaregistrována žádná závislost, použije se výchozí implementace.</span><span class="sxs-lookup"><span data-stu-id="ee14a-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="ee14a-108">Seznam výchozích implementací naleznete v tématu [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) .</span><span class="sxs-lookup"><span data-stu-id="ee14a-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
