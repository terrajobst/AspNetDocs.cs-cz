---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[Postupy:]  Ukládat ASP.NET stránku na základě informací v hlavičce HTTP | Microsoft Docs'
author: rick-anderson
description: V tomto videu Chris pixelů na ukazuje, jak zachovat stránku ve výstupní mezipaměti ASP.NET na základě informací v hlavičce HTTP stránky. Nejdřív potenciální HTTP HEA...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624969"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="22c33-104">[Postupy:]  Ukládat ASP.NET stránku na základě informací v hlavičce protokolu HTTP do mezipaměti</span><span class="sxs-lookup"><span data-stu-id="22c33-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>

<span data-ttu-id="22c33-105">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="22c33-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="22c33-106">V tomto videu Chris pixelů na ukazuje, jak zachovat stránku ve výstupní mezipaměti ASP.NET na základě informací v hlavičce HTTP stránky.</span><span class="sxs-lookup"><span data-stu-id="22c33-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="22c33-107">Nejprve jsou zkontrolovány možné hodnoty hlaviček protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="22c33-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="22c33-108">Pak se vytvoří Ukázková stránka a pak se pomocí atributu VaryByHeader s atributem, který obsahuje hodnotu "Accept-Language", vytvoří hlavičku HTTP pro řízení ukládání do mezipaměti na základě jazyka prohlížeče uživatele.</span><span class="sxs-lookup"><span data-stu-id="22c33-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="22c33-109">Ukázková stránka se zobrazuje v IE, která je nastavená na angličtinu a pak v prohlížeči FireFox, která je nastavená na používání francouzštiny.</span><span class="sxs-lookup"><span data-stu-id="22c33-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="22c33-110">Nakonec je diskutována možnost přesunout definici mezipaměti do CacheProfile v souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="22c33-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="22c33-111">&#9654;Přehrát video (12 minut)</span><span class="sxs-lookup"><span data-stu-id="22c33-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
