---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: 'Jak mohu: vytvořit vlastní nápovědu HTML pro aplikaci MVC? | Dokumenty Microsoft'
author: rick-anderson
description: V tomto videu Chris pixelů na ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici ve standardní sadě v aplikaci MVC. Nejprve se zobrazí ukázkový přes MVC...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559043"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="5eef9-105">Jak mohu: vytvořit vlastní nápovědu HTML pro aplikaci MVC?</span><span class="sxs-lookup"><span data-stu-id="5eef9-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="5eef9-106">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="5eef9-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="5eef9-107">V tomto videu Chris pixelů na ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici ve standardní sadě v aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="5eef9-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="5eef9-108">Nejdřív se vytvoří ukázková aplikace MVC s ukázkovým kontrolérem a zobrazením, které otestuje vlastní HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="5eef9-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="5eef9-109">Dále je vytvořen modul s veřejnou funkcí, která představuje metodu rozšíření, která představuje implementaci vlastního HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="5eef9-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="5eef9-110">Vlastní pomoc je určena k vytváření značek `<img>` na stránce a přijímá několik vstupních parametrů, včetně ID, adresy URL a alternativního textu pro značku obrázku.</span><span class="sxs-lookup"><span data-stu-id="5eef9-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="5eef9-111">Logika je pak přidána do funkce pro vrácení dokončené `<img>` značky se zadanými informacemi.</span><span class="sxs-lookup"><span data-stu-id="5eef9-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="5eef9-112">Pak se vlastní HtmlHelper použije na stránce demo k zobrazení obrázku.</span><span class="sxs-lookup"><span data-stu-id="5eef9-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="5eef9-113">Nakonec je vlastní HtmlHelper rozbalený tak, aby zahrnovalo více přepsání konstruktoru, což poskytuje flexibilitu pro snazší vytváření různých `<img>` značek.</span><span class="sxs-lookup"><span data-stu-id="5eef9-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="5eef9-114">&#9654;Sledovat video (18 minut)</span><span class="sxs-lookup"><span data-stu-id="5eef9-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="5eef9-115">[Předchozí](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [Další](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="5eef9-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
