---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076552"
---
# <a name="custom-model-binding-demo"></a><span data-ttu-id="f2c87-101">Ukázka vazby vlastního modelu</span><span class="sxs-lookup"><span data-stu-id="f2c87-101">Custom Model Binding Demo</span></span>

<span data-ttu-id="f2c87-102">Test `ByteArrayModelBinder` spuštěním aplikace a účtování řetězec s kódováním base64 `ImageController` koncový bod (`/api/image/`).</span><span class="sxs-lookup"><span data-stu-id="f2c87-102">Test `ByteArrayModelBinder` by running the app and POSTing a base64-encoded string to the `ImageController` endpoint (`/api/image/`).</span></span> <span data-ttu-id="f2c87-103">Zadejte vlastnosti souboru a název souboru v textu žádosti jako data formuláře (pomocí [Postman](https://www.getpostman.com/) nebo něco podobného).</span><span class="sxs-lookup"><span data-stu-id="f2c87-103">Specify the file and filename properties in the request body as form-data (using [Postman](https://www.getpostman.com/) or a similar tool).</span></span> <span data-ttu-id="f2c87-104">Můžete použít [tento řetězec vzorku](Base64String.txt).</span><span class="sxs-lookup"><span data-stu-id="f2c87-104">You can use [this sample string](Base64String.txt).</span></span> <span data-ttu-id="f2c87-105">Výsledek je uložen v *Image/wwwroot/nahrávání* složku s názvem souboru zadán.</span><span class="sxs-lookup"><span data-stu-id="f2c87-105">The result is saved in the *wwwroot/images/upload* folder with the filename specified.</span></span>

<span data-ttu-id="f2c87-106">K otestování v příkladu vlastní vazby, zkuste následující koncové body:</span><span class="sxs-lookup"><span data-stu-id="f2c87-106">To test the custom binding example, try the following endpoints:</span></span>

* <span data-ttu-id="f2c87-107">/API/authors/1</span><span class="sxs-lookup"><span data-stu-id="f2c87-107">/api/authors/1</span></span>
* <span data-ttu-id="f2c87-108">/API/authors/2 (Nenalezeno)</span><span class="sxs-lookup"><span data-stu-id="f2c87-108">/api/authors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="f2c87-109">/API/boundauthors/1</span><span class="sxs-lookup"><span data-stu-id="f2c87-109">/api/boundauthors/1</span></span>
* <span data-ttu-id="f2c87-110">/API/boundauthors/2 (Nenalezeno)</span><span class="sxs-lookup"><span data-stu-id="f2c87-110">/api/boundauthors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="f2c87-111">/api/boundauthors/get/1</span><span class="sxs-lookup"><span data-stu-id="f2c87-111">/api/boundauthors/get/1</span></span>
* <span data-ttu-id="f2c87-112">(žádný obsah) /API/boundauthors/Get/2 &ndash; tato akce nemá zkontrolovat hodnoty null a vrátí *404 Nenalezeno*.</span><span class="sxs-lookup"><span data-stu-id="f2c87-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; This action doesn't check for null and returns a *404 Not Found*.</span></span>
