---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165854"
---
<span data-ttu-id="a72f2-101">**Upozornění**: Následující kód používá `GetTempFileName`, kterou vyvolá `IOException` Pokud víc než 65 535 soubory jsou vytvořeny bez odstranění předchozí dočasné soubory.</span><span class="sxs-lookup"><span data-stu-id="a72f2-101">**Warning**: The following code uses `GetTempFileName`, which throws an `IOException` if more than 65535 files are created without deleting previous temporary files.</span></span> <span data-ttu-id="a72f2-102">Skutečné aplikace by měla buď odstranit dočasné soubory nebo použijte `GetTempPath` a `GetRandomFileName` vytvořit název dočasného souboru.</span><span class="sxs-lookup"><span data-stu-id="a72f2-102">A real app should either delete temporary files or use `GetTempPath` and `GetRandomFileName` to create temporary file names.</span></span> <span data-ttu-id="a72f2-103">Limit 65535 soubory je jeden server, aby mohly používat jiné aplikace na serveru všechny soubory 65535.</span><span class="sxs-lookup"><span data-stu-id="a72f2-103">The 65535 files limit is per server, so another app on the server can use up all 65535 files.</span></span> 
