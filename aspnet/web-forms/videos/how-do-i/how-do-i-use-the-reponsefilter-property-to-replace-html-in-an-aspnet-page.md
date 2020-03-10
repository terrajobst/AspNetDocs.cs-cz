---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[Postupy:] Pomocí vlastnosti reodezvy. Filter nahraďte HTML na stránce ASP.NET | Microsoft Docs'
author: rick-anderson
description: V tomto videu Chris pixelů na ukazuje, jak použít vlastnost reslat. Filter k zachycení a změně odesílaného HTML kódu na stránku. Nejprve se vytvoří Ukázková stránka w...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602814"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[Postupy:] Použití vlastnosti reodezvy. Filter k nahrazení kódu HTML na stránce ASP.NET

autor – [Chris pixelů na](https://twitter.com/chrispels)

V tomto videu Chris pixelů na ukazuje, jak použít vlastnost reslat. Filter k zachycení a změně odesílaného HTML kódu na stránku. Nejdřív se vytvoří Ukázková stránka s nějakým jednoduchým textem. Pak se vytvoří vlastní třída streamu, která slouží jako náhradní datový proud pro aktuální datový proud, který se posílá do prohlížeče uživatele. V této třídě vlastního datového proudu se obsah stránky načítá z datového proudu, změnil a pak se zapsal do datového proudu odpovědí. V této vlastní třídě datového proudu je metoda zápisu přizpůsobená tak, aby nahradila kód HTML v datovém proudu základní odpovědi, a tím mění, co je odesláno do prohlížeče uživatele. Nakonec je nová třída Stream přiřazená vlastnosti Response. Filter na stránce\_načíst událost, takže poskytuje mechanismus pro změnu obsahu stránky.

[&#9654;Přehrát video (13 minut)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
