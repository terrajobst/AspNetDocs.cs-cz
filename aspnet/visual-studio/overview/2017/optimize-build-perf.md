---
uid: visual-studio/overview/2017/optimize-build-perf
title: Optimalizace výkonu sestavení pro řešení
author: AngelosP
description: Optimalizace výkonu sestavení pro řešení
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073801"
---
# <a name="optimize-build-performance-for-solution"></a>Optimalizace výkonu sestavení pro řešení

Visual Studio 2017 15.8 nebo vyšší zahrnují položky nabídky: **Sestavení** > **kompilace ASP.NET** > **optimalizovat výkon sestavení pro řešení**.

![snímek obrazovky s novou položku nabídky](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET zkompiluje za běhu, což znamená, že technologie ASP.NET provede s ní kopie kompilátor jeho zobrazení. Ale na počítači pro vývojáře při kopírování kompilátor neodpovídá kopie sady Visual Studio, sestavení je dopad na výkon v řádu sekund 1-3 na přírůstkové sestavení. Tato funkce aktualizuje váš projekt kopie kompilátor tak, aby odpovídala sadě Visual Studio, což obvykle urychlí přírůstková sestavení.

**To se vztahuje na ASP.NET Framework 4.7.1 nebo později pouze pro projekty, neplatí pro ASP.NET Core.**
