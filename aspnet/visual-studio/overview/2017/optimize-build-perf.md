---
uid: visual-studio/overview/2017/optimize-build-perf
title: Optimalizace výkonu sestavení pro řešení
author: AngelosP
description: Optimalizace výkonu sestavení pro řešení
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622638"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="1d144-103">Optimalizace výkonu sestavení pro řešení</span><span class="sxs-lookup"><span data-stu-id="1d144-103">Optimize build performance for solution</span></span>

<span data-ttu-id="1d144-104">Visual Studio 2017 15,8 nebo novější zahrnuje položku nabídky: **Build** > **ASP.NET Compilation** > **optimalizuje výkon sestavení pro řešení**.</span><span class="sxs-lookup"><span data-stu-id="1d144-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![Snímek obrazovky nové položky nabídky](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="1d144-106">ASP.NET zkompiluje své zobrazení za běhu, což znamená, že projekt ASP.NET s ním nese kopii kompilátoru.</span><span class="sxs-lookup"><span data-stu-id="1d144-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="1d144-107">Avšak v počítači pro vývojáře, pokud se kopie kompilátoru neshoduje s kopírováním sady Visual Studio, výkon sestavení bude mít vliv na pořadí 1-3 sekund na přírůstkové sestavení.</span><span class="sxs-lookup"><span data-stu-id="1d144-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="1d144-108">Tato funkce aktualizuje kopii kompilátoru vašeho projektu tak, aby odpovídala aplikaci Visual Studio, která obvykle zrychluje přírůstkové sestavení.</span><span class="sxs-lookup"><span data-stu-id="1d144-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="1d144-109">**To platí jenom pro projekty ASP.NET Framework 4.7.1 nebo novější, ale nevztahuje se na ASP.NET Core.**</span><span class="sxs-lookup"><span data-stu-id="1d144-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
