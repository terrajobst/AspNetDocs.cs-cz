---
uid: web-forms/videos/net-4/routing/how-do-i-use-routing-with-aspnet-web-forms
title: 'Jak mohu: používat směrování s webovými formuláři ASP.NET? | Dokumenty Microsoft'
author: rick-anderson
description: V tomto videu Chris pixelů na ukazuje, jak implementovat směrování pro webové formuláře v ASP.NET 4. Nejprve koncept směrování adresy URL se porovná s mapováním adresy URL na p...
ms.author: riande
ms.date: 10/15/2010
ms.assetid: a3ab6cd9-8f71-4b73-9336-21c0de078269
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-use-routing-with-aspnet-web-forms
msc.type: video
ms.openlocfilehash: f5036d780ed4fd0dd8caabbf4badb39fd9ee2de3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545155"
---
# <a name="how-do-i-use-routing-with-aspnet-web-forms"></a><span data-ttu-id="b0d10-105">Jak mohu: používat směrování s webovými formuláři ASP.NET?</span><span class="sxs-lookup"><span data-stu-id="b0d10-105">How Do I: Use Routing with ASP.NET Web Forms?</span></span>

<span data-ttu-id="b0d10-106">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="b0d10-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="b0d10-107">V tomto videu Chris pixelů na ukazuje, jak implementovat směrování pro webové formuláře v ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="b0d10-107">In this video Chris Pels shows how to implement routing for Web Forms in ASP.NET 4.</span></span> <span data-ttu-id="b0d10-108">Nejprve koncept směrování adresy URL se porovná s mapováním adresy URL na fyzický soubor v lokalitě.</span><span class="sxs-lookup"><span data-stu-id="b0d10-108">First, the concept of routing a URL is compared to mapping the URL to a physical file in the site.</span></span> <span data-ttu-id="b0d10-109">Pak je v souboru Global. asax pro aplikaci definována ukázková trasa pro adresu URL\_spuštění obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="b0d10-109">Then, a sample route for a URL is defined in the global.asax file Application\_Start event handler.</span></span> <span data-ttu-id="b0d10-110">Trasa obsahuje parametrizovanou hodnotu, kterou může uživatel zadat v adrese URL.</span><span class="sxs-lookup"><span data-stu-id="b0d10-110">The route contains a parameterized value that the user can enter in the URL.</span></span> <span data-ttu-id="b0d10-111">Pak se vytvoří Ukázková stránka a hodnota parametru Route se extrahuje na stránce\_načtení obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="b0d10-111">A sample page is then created and the route parameter value is extracted in the Page\_Load event handler.</span></span> <span data-ttu-id="b0d10-112">Dále je definována Druhá trasa s více parametry a trasami na stejnou stránku jako počáteční trasa.</span><span class="sxs-lookup"><span data-stu-id="b0d10-112">Next, a second route is defined that has multiple parameters and routes to the same page as the initial route.</span></span> <span data-ttu-id="b0d10-113">Obslužná rutina události\_načítání stránky je rozbalena pro extrakci hodnoty parametru další trasy a zobrazení různých informací v závislosti na tom, jaké hodnoty byly na stránku předány.</span><span class="sxs-lookup"><span data-stu-id="b0d10-113">The Page\_Load event handler is expanded to extract the additional route parameter value and display different information depending upon what values have been passed to the page.</span></span>

[<span data-ttu-id="b0d10-114">&#9654;Sledovat video (15 minut)</span><span class="sxs-lookup"><span data-stu-id="b0d10-114">&#9654; Watch video (15 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-routing-with-aspnet-web-forms)

> [!div class="step-by-step"]
> <span data-ttu-id="b0d10-115">[Předchozí](aspnet-4-quick-hit-outbound-webforms-routing.md)
> [Další](how-do-i-work-with-urls-in-aspnet-routing.md)</span><span class="sxs-lookup"><span data-stu-id="b0d10-115">[Previous](aspnet-4-quick-hit-outbound-webforms-routing.md)
[Next](how-do-i-work-with-urls-in-aspnet-routing.md)</span></span>
