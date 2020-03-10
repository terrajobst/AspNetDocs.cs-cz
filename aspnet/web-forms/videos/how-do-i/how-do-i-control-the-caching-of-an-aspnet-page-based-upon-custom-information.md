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
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a>[Postupy:] Řízení ukládání stránky ASP.NET do mezipaměti na základě vlastních informací

autor – [Chris pixelů na](https://twitter.com/chrispels)

V tomto videu Chris pixelů na ukazuje, jak řídit kritéria pro ukládání ASP.NET stránky do mezipaměti na základě vlastních informací. Vytvoří se Ukázková stránka a pak se použije direktiva OutputCache s atributem hodnota VaryByCustom, který obsahuje vlastní hodnotu. Dále metoda GetVaryCustomByString () je přepsána v modulu Global. asax, který poskytuje zpracování vlastního atributu. V této metodě je vrácen řetězec, který jednoznačně identifikuje verzi stránky uloženou v mezipaměti. Nakonec je diskuzi o tom, jak je možné ukládání do mezipaměti pomocí vlastní hodnoty použít několika způsoby pro web.

[&#9654;Přehrát video (12 minut)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
