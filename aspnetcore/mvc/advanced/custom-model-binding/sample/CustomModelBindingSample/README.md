---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076552"
---
# <a name="custom-model-binding-demo"></a>Ukázka vazby vlastního modelu

Test `ByteArrayModelBinder` spuštěním aplikace a účtování řetězec s kódováním base64 `ImageController` koncový bod (`/api/image/`). Zadejte vlastnosti souboru a název souboru v textu žádosti jako data formuláře (pomocí [Postman](https://www.getpostman.com/) nebo něco podobného). Můžete použít [tento řetězec vzorku](Base64String.txt). Výsledek je uložen v *Image/wwwroot/nahrávání* složku s názvem souboru zadán.

K otestování v příkladu vlastní vazby, zkuste následující koncové body:

* /API/authors/1
* /API/authors/2 (Nenalezeno)
* /API/boundauthors/1
* /API/boundauthors/2 (Nenalezeno)
* /api/boundauthors/get/1
* (žádný obsah) /API/boundauthors/Get/2 &ndash; tato akce nemá zkontrolovat hodnoty null a vrátí *404 Nenalezeno*.
