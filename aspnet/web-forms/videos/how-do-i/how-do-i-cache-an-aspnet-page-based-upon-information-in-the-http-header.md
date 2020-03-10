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
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a>[Postupy:]  Ukládat ASP.NET stránku na základě informací v hlavičce protokolu HTTP do mezipaměti

autor – [Chris pixelů na](https://twitter.com/chrispels)

V tomto videu Chris pixelů na ukazuje, jak zachovat stránku ve výstupní mezipaměti ASP.NET na základě informací v hlavičce HTTP stránky. Nejprve jsou zkontrolovány možné hodnoty hlaviček protokolu HTTP. Pak se vytvoří Ukázková stránka a pak se pomocí atributu VaryByHeader s atributem, který obsahuje hodnotu "Accept-Language", vytvoří hlavičku HTTP pro řízení ukládání do mezipaměti na základě jazyka prohlížeče uživatele. Ukázková stránka se zobrazuje v IE, která je nastavená na angličtinu a pak v prohlížeči FireFox, která je nastavená na používání francouzštiny. Nakonec je diskutována možnost přesunout definici mezipaměti do CacheProfile v souboru Web. config.

[&#9654;Přehrát video (12 minut)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
