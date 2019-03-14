---
ms.openlocfilehash: 568fa161b27e554fd8b474670b8f9a7ec2f39f45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072781"
---
<span data-ttu-id="08512-101">Následující tabulka obsahuje podrobnosti o parametry generátor kódu ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="08512-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="08512-102">Parametr</span><span class="sxs-lookup"><span data-stu-id="08512-102">Parameter</span></span>               | <span data-ttu-id="08512-103">Popis</span><span class="sxs-lookup"><span data-stu-id="08512-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="08512-104">-m</span><span class="sxs-lookup"><span data-stu-id="08512-104">-m</span></span>  | <span data-ttu-id="08512-105">Název modelu.</span><span class="sxs-lookup"><span data-stu-id="08512-105">The name of the model.</span></span> |
| <span data-ttu-id="08512-106">-dc</span><span class="sxs-lookup"><span data-stu-id="08512-106">-dc</span></span>  | <span data-ttu-id="08512-107">Data kontextu.</span><span class="sxs-lookup"><span data-stu-id="08512-107">The data context.</span></span> |
| <span data-ttu-id="08512-108">-udl</span><span class="sxs-lookup"><span data-stu-id="08512-108">-udl</span></span> | <span data-ttu-id="08512-109">Použijte výchozí rozložení.</span><span class="sxs-lookup"><span data-stu-id="08512-109">Use the default layout.</span></span> |
| <span data-ttu-id="08512-110">--relativeFolderPath</span><span class="sxs-lookup"><span data-stu-id="08512-110">--relativeFolderPath</span></span> | <span data-ttu-id="08512-111">Relativní cesta k výstupní složce vytvořte zobrazení.</span><span class="sxs-lookup"><span data-stu-id="08512-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="08512-112">--useDefaultLayout</span><span class="sxs-lookup"><span data-stu-id="08512-112">--useDefaultLayout</span></span> | <span data-ttu-id="08512-113">Výchozí rozložení by měla sloužit pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="08512-113">The default layout should be used for the views.</span></span> |
| <span data-ttu-id="08512-114">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="08512-114">--referenceScriptLibraries</span></span> | <span data-ttu-id="08512-115">Přidá `_ValidationScriptsPartial` upravovat a vytvářet stránky</span><span class="sxs-lookup"><span data-stu-id="08512-115">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="08512-116">Použití `h` přepínače můžete zobrazit nápovědu pro `aspnet-codegenerator controller` příkaz:</span><span class="sxs-lookup"><span data-stu-id="08512-116">Use the `h` switch to get help on the `aspnet-codegenerator controller` command:</span></span>

```console
dotnet aspnet-codegenerator controller -h
```