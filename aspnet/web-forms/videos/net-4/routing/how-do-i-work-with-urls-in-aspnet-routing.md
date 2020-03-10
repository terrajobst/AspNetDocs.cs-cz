---
uid: web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
title: 'Jak můžu: pracovat s adresami URL ve směrování ASP.NET? | Dokumenty Microsoft'
author: rick-anderson
description: V tomto videu Chris pixelů na ukazuje, jak zadat adresy URL na webu, který využívá směrování ASP.NET. Nejprve je vytvořen web a směrování je definováno v rámci HK...
ms.author: riande
ms.date: 10/15/2010
ms.assetid: 08f9d0a7-cfa0-4914-a672-8a64295d7ba8
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
msc.type: video
ms.openlocfilehash: eb1060fd9cc9469dc2b1d2e918823316c36840cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78565126"
---
# <a name="how-do-i-work-with-urls-in-aspnet-routing"></a><span data-ttu-id="be842-105">Jak můžu: pracovat s adresami URL ve směrování ASP.NET?</span><span class="sxs-lookup"><span data-stu-id="be842-105">How Do I: Work with URLs in ASP.NET Routing?</span></span>

<span data-ttu-id="be842-106">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="be842-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="be842-107">V tomto videu Chris pixelů na ukazuje, jak zadat adresy URL na webu, který využívá směrování ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="be842-107">In this video Chris Pels shows how to specify URLs in a web site that utilizes ASP.NET routing.</span></span> <span data-ttu-id="be842-108">Nejprve je vytvořen web a směrování je definováno v globální třídě aplikace (. asax).</span><span class="sxs-lookup"><span data-stu-id="be842-108">First, a web site is created and routing is defined in the Global Application Class (.asax).</span></span> <span data-ttu-id="be842-109">V dalším kroku se vytvoří Ukázková webová stránka a adresa URL na základě definované trasy se přidá na stránku pomocí standardního "" pevného kódovaného "přístupu, např. ~/Stats/Visitors.</span><span class="sxs-lookup"><span data-stu-id="be842-109">Next, a sample web page is created and a URL based upon a defined route is added to the page using the standard "hard coded" approach, e.g., "~/Stats/Visitors".</span></span> <span data-ttu-id="be842-110">Další odkaz je následně přidán na stránku, která dynamicky generuje stejnou adresu URL v kódu pomocí metody RouteValue, která přijímá název a parametry trasy.</span><span class="sxs-lookup"><span data-stu-id="be842-110">Another link is then added to the page which dynamically generates the same URL in markup using the RouteValue method which accepts the route name and parameters.</span></span> <span data-ttu-id="be842-111">Stejná adresa URL je pak implementována pomocí kódu namísto značek přímo na stránce.</span><span class="sxs-lookup"><span data-stu-id="be842-111">The same URL is then implemented using code rather than markup directly in the page.</span></span> <span data-ttu-id="be842-112">Původní trasa a umístění fyzické stránky se pak změní a výsledkem je, že v pevně zakódovaném odkazu přestane fungovat, zatímco dynamicky vygenerované odkazy fungují správně.</span><span class="sxs-lookup"><span data-stu-id="be842-112">The original route and physical page location are then changed, resulting in the hard coded link no longer working whereas both dynamically generated links function properly.</span></span> <span data-ttu-id="be842-113">Nakonec je popsána hodnota dynamicky vygenerovaných odkazů.</span><span class="sxs-lookup"><span data-stu-id="be842-113">Finally, the value of dynamically generated links is then discussed.</span></span>

[<span data-ttu-id="be842-114">&#9654;Sledovat video (20 minut)</span><span class="sxs-lookup"><span data-stu-id="be842-114">&#9654; Watch video (20 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> [<span data-ttu-id="be842-115">Předchozí</span><span class="sxs-lookup"><span data-stu-id="be842-115">Previous</span></span>](how-do-i-use-routing-with-aspnet-web-forms.md)
