---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165854"
---
**Upozornění**: Následující kód používá `GetTempFileName`, kterou vyvolá `IOException` Pokud víc než 65 535 soubory jsou vytvořeny bez odstranění předchozí dočasné soubory. Skutečné aplikace by měla buď odstranit dočasné soubory nebo použijte `GetTempPath` a `GetRandomFileName` vytvořit název dočasného souboru. Limit 65535 soubory je jeden server, aby mohly používat jiné aplikace na serveru všechny soubory 65535. 
