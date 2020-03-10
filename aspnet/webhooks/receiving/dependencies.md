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
# <a name="aspnet-webhooks-receiver-dependencies"></a>Závislosti přijímače webhooků ASP.NET

Microsoft ASP.NET webhooků je navržená s ohledem na injektáže závislostí. Většina závislostí v systému se dá nahradit alternativními implementacemi pomocí modulu injektáže závislostí.

Seznam závislostí přijímače najdete v tématu [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) . Pokud není zaregistrována žádná závislost, použije se výchozí implementace. Seznam výchozích implementací naleznete v tématu [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) .
