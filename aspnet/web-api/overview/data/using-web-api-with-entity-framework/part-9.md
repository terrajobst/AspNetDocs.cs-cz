---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: Přidat novou položku do databáze | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557286"
---
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="38310-102">Přidání nové položky do databáze</span><span class="sxs-lookup"><span data-stu-id="38310-102">Add a New Item to the Database</span></span>

<span data-ttu-id="38310-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="38310-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="38310-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="38310-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="38310-105">V této části přidáte uživatelům možnost vytvořit novou knihu.</span><span class="sxs-lookup"><span data-stu-id="38310-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="38310-106">V App. js přidejte následující kód do modelu zobrazení:</span><span class="sxs-lookup"><span data-stu-id="38310-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="38310-107">V indexu. cshtml nahraďte následující kód:</span><span class="sxs-lookup"><span data-stu-id="38310-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="38310-108">Za:</span><span class="sxs-lookup"><span data-stu-id="38310-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="38310-109">Tento kód vytvoří formulář pro odeslání nového autora.</span><span class="sxs-lookup"><span data-stu-id="38310-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="38310-110">Hodnoty pro rozevírací seznam autora jsou vázány na data `authors` lze v modelu zobrazení zobrazit jako pozorovatelný.</span><span class="sxs-lookup"><span data-stu-id="38310-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="38310-111">Pro jiné vstupy formuláře jsou hodnoty vázány na data s vlastností `newBook` modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="38310-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="38310-112">Obslužná rutina odeslání ve formuláři je svázána s funkcí `addBook`:</span><span class="sxs-lookup"><span data-stu-id="38310-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="38310-113">Funkce `addBook` přečte aktuální hodnoty vstupů vázaných na data pro vytvoření objektu JSON.</span><span class="sxs-lookup"><span data-stu-id="38310-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="38310-114">Pak odešle objekt JSON do `/api/books`.</span><span class="sxs-lookup"><span data-stu-id="38310-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="38310-115">[Předchozí](part-8.md)
> [Další](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="38310-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
