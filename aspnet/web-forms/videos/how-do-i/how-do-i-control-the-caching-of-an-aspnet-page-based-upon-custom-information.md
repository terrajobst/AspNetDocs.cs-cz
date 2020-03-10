---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[Postupy:] Řízení ukládání stránky ASP.NET do mezipaměti na základě vlastních informací | Microsoft Docs'
author: rick-anderson
description: V tomto videu Chris pixelů na ukazuje, jak řídit kritéria pro ukládání ASP.NET stránky do mezipaměti na základě vlastních informací. Vytvoří se Ukázková stránka a pak O...
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624731"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="f6727-104">[Postupy:] Řízení ukládání stránky ASP.NET do mezipaměti na základě vlastních informací</span><span class="sxs-lookup"><span data-stu-id="f6727-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="f6727-105">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f6727-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f6727-106">V tomto videu Chris pixelů na ukazuje, jak řídit kritéria pro ukládání ASP.NET stránky do mezipaměti na základě vlastních informací.</span><span class="sxs-lookup"><span data-stu-id="f6727-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="f6727-107">Vytvoří se Ukázková stránka a pak se použije direktiva OutputCache s atributem hodnota VaryByCustom, který obsahuje vlastní hodnotu.</span><span class="sxs-lookup"><span data-stu-id="f6727-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="f6727-108">Dále metoda GetVaryCustomByString () je přepsána v modulu Global. asax, který poskytuje zpracování vlastního atributu.</span><span class="sxs-lookup"><span data-stu-id="f6727-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="f6727-109">V této metodě je vrácen řetězec, který jednoznačně identifikuje verzi stránky uloženou v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="f6727-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="f6727-110">Nakonec je diskuzi o tom, jak je možné ukládání do mezipaměti pomocí vlastní hodnoty použít několika způsoby pro web.</span><span class="sxs-lookup"><span data-stu-id="f6727-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="f6727-111">&#9654;Přehrát video (12 minut)</span><span class="sxs-lookup"><span data-stu-id="f6727-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
