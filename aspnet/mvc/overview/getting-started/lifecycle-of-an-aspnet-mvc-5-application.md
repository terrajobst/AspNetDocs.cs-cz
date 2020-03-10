---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: Životní cyklus aplikace ASP.NET MVC 5 | Microsoft Docs
author: cephalin
description: Stáhněte si dokument PDF, který graf životní cyklus aplikace ASP.NET MVC 5. Tento dokument životního cyklu poskytuje podrobný pohled na životní cyklus MVC...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582199"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a>Životní cyklus aplikace ASP.NET MVC 5

podle [Cephas](https://github.com/cephalin)

[Stáhnout dokument PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

Tady si můžete stáhnout dokument PDF, který seřadí životní cyklus každé aplikace ASP.NET MVC 5, od přijetí požadavku HTTP k odeslání odpovědi HTTP zpátky klientovi. Je navržený jako vzdělávací nástroj pro uživatele, kteří jsou noví v ASP.NET MVC, a také jako referenci pro uživatele, kteří potřebují přejít na konkrétní aspekty aplikace. Dokument PDF má následující funkce:

- Relevantní fáze [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) vám pomůžou pochopit, kde se MVC integruje do [životního cyklu aplikace ASP.NET](https://msdn.microsoft.com/library/bb470252.aspx).
- Základní pohled na životní cyklus aplikace MVC, kde můžete pochopit hlavní fáze, které každá aplikace MVC projde v kanálu zpracování požadavků.  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- Podrobné zobrazení obsahuje podrobné informace o podrobnostech kanálu zpracování požadavků. Můžete porovnat zobrazení na nejvyšší úrovni a detailní zobrazení a zjistit, jak se v různých fázích shromažďují údaje o životním cyklu. [Stáhněte si PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) , abyste viděli větší pohled.
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- Umístění a účel všech přepisovatelných metod objektu [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) v kanálu zpracování požadavků. Může nebo nemusí být nutné přepsat libovolnou metodu, ale je důležité, abyste porozuměli jejich roli v životním cyklu aplikace, abyste mohli psát kód ve vhodné fázi životního cyklu pro daný efekt.
- Plnohodnotnou diagramy ukazující způsob, jakým jsou vyvolány jednotlivé typy filtrů (ověřování, autorizace, akce a výsledek).
- Odkaz na užitečný článek nebo blog z každého bodu zájmu v zobrazení podrobností

## <a name="next-steps"></a>Další kroky

Vyhovuje tento dokument vašim potřebám? Vážíme si vašeho názoru. Pokud máte nějaké dotazy k životnímu cyklu ASP.NET MVC v aplikaci, [StackOverflow](http://stackoverflow.com/help) a [fóra ASP.NET MVC](https://forums.asp.net/1146.aspx) jsou skvělé místa pro dotazování. Sledujte [mě](https://twitter.com/Cephas_MSFT) na Twitteru, abyste mohli získat aktualizace na mých nejnovějších kurzech.
