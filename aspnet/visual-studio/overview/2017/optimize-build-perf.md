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
# <a name="optimize-build-performance-for-solution"></a>Optimalizace výkonu sestavení pro řešení

Visual Studio 2017 15,8 nebo novější zahrnuje položku nabídky: **Build** > **ASP.NET Compilation** > **optimalizuje výkon sestavení pro řešení**.

![Snímek obrazovky nové položky nabídky](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET zkompiluje své zobrazení za běhu, což znamená, že projekt ASP.NET s ním nese kopii kompilátoru. Avšak v počítači pro vývojáře, pokud se kopie kompilátoru neshoduje s kopírováním sady Visual Studio, výkon sestavení bude mít vliv na pořadí 1-3 sekund na přírůstkové sestavení. Tato funkce aktualizuje kopii kompilátoru vašeho projektu tak, aby odpovídala aplikaci Visual Studio, která obvykle zrychluje přírůstkové sestavení.

**To platí jenom pro projekty ASP.NET Framework 4.7.1 nebo novější, ale nevztahuje se na ASP.NET Core.**
