---
title: Migrace z Microsoft.Extensions.Logging 2.1 k 2.2 nebo 3.0.
author: pakrym
description: Zjistěte, jak migrovat aplikace ASP.NET Core, která používá Microsoft.Extensions.Logging z 2.1 2.2 nebo 3.0.
ms.author: pakrym
ms.custom: mvc
ms.date: 01/04/2019
uid: migration/logging-nonaspnetcore
ms.openlocfilehash: 2519ddc02cee5978483bcaef4341a52aad3ba2a6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077614"
---
# <a name="migrate-from-microsoftextensionslogging-21-to-22-or-30"></a><span data-ttu-id="dbdfd-103">Migrace z Microsoft.Extensions.Logging 2.1 k 2.2 nebo 3.0.</span><span class="sxs-lookup"><span data-stu-id="dbdfd-103">Migrate from Microsoft.Extensions.Logging 2.1 to 2.2 or 3.0</span></span>

<span data-ttu-id="dbdfd-104">Tento článek popisuje běžné kroky při migraci aplikace ASP.NET Core, která používá `Microsoft.Extensions.Logging` z 2.1 2.2 nebo 3.0.</span><span class="sxs-lookup"><span data-stu-id="dbdfd-104">This article outlines the common steps for migrating a non-ASP.NET Core application that uses `Microsoft.Extensions.Logging` from 2.1 to 2.2 or 3.0.</span></span>

## <a name="21-to-22"></a><span data-ttu-id="dbdfd-105">Z verze 2.1 do verze 2.2</span><span class="sxs-lookup"><span data-stu-id="dbdfd-105">2.1 to 2.2</span></span>

<span data-ttu-id="dbdfd-106">Ruční vytvoření `ServiceCollection` a volat `AddLogging`.</span><span class="sxs-lookup"><span data-stu-id="dbdfd-106">Manually create `ServiceCollection` and call `AddLogging`.</span></span>

<span data-ttu-id="dbdfd-107">2.1 Příklad:</span><span class="sxs-lookup"><span data-stu-id="dbdfd-107">2.1 example:</span></span>

```csharp
using (var loggerFactory = new LoggerFactory())
{
    loggerFactory.AddConsole();

    // use loggerFactory
}
```

<span data-ttu-id="dbdfd-108">2,2 příklad:</span><span class="sxs-lookup"><span data-stu-id="dbdfd-108">2.2 example:</span></span>

```csharp
var serviceCollection = new ServiceCollection();
serviceCollection.AddLogging(builder => builder.AddConsole());

using (var serviceProvider = serviceCollection.BuildServiceProvider())
using (var loggerFactory = serviceProvider.GetService<ILoggerFactory>())
{
    // use loggerFactory
}
```

## <a name="21-to-30"></a><span data-ttu-id="dbdfd-109">2.1 až 3.0</span><span class="sxs-lookup"><span data-stu-id="dbdfd-109">2.1 to 3.0</span></span>

<span data-ttu-id="dbdfd-110">3.0, použijte `LoggingFactory.Create`.</span><span class="sxs-lookup"><span data-stu-id="dbdfd-110">In 3.0, use `LoggingFactory.Create`.</span></span>

<span data-ttu-id="dbdfd-111">2.1 Příklad:</span><span class="sxs-lookup"><span data-stu-id="dbdfd-111">2.1 example:</span></span>

```csharp
using (var loggerFactory = new LoggerFactory())
{
    loggerFactory.AddConsole();

    // use loggerFactory
}
```

<span data-ttu-id="dbdfd-112">3.0 Příklad:</span><span class="sxs-lookup"><span data-stu-id="dbdfd-112">3.0 example:</span></span>

```csharp
using (var loggerFactory = LoggerFactory.Create(builder => builder.AddConsole()))
{
    // use loggerFactory
}
```

## <a name="additional-resources"></a><span data-ttu-id="dbdfd-113">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="dbdfd-113">Additional resources</span></span>

<xref:fundamentals/logging/index>