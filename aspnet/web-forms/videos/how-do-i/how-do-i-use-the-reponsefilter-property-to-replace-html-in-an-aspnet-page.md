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
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="aea6e-104">[Postupy:] Použití vlastnosti reodezvy. Filter k nahrazení kódu HTML na stránce ASP.NET</span><span class="sxs-lookup"><span data-stu-id="aea6e-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>

<span data-ttu-id="aea6e-105">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="aea6e-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="aea6e-106">V tomto videu Chris pixelů na ukazuje, jak použít vlastnost reslat. Filter k zachycení a změně odesílaného HTML kódu na stránku.</span><span class="sxs-lookup"><span data-stu-id="aea6e-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="aea6e-107">Nejdřív se vytvoří Ukázková stránka s nějakým jednoduchým textem.</span><span class="sxs-lookup"><span data-stu-id="aea6e-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="aea6e-108">Pak se vytvoří vlastní třída streamu, která slouží jako náhradní datový proud pro aktuální datový proud, který se posílá do prohlížeče uživatele.</span><span class="sxs-lookup"><span data-stu-id="aea6e-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="aea6e-109">V této třídě vlastního datového proudu se obsah stránky načítá z datového proudu, změnil a pak se zapsal do datového proudu odpovědí.</span><span class="sxs-lookup"><span data-stu-id="aea6e-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="aea6e-110">V této vlastní třídě datového proudu je metoda zápisu přizpůsobená tak, aby nahradila kód HTML v datovém proudu základní odpovědi, a tím mění, co je odesláno do prohlížeče uživatele.</span><span class="sxs-lookup"><span data-stu-id="aea6e-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="aea6e-111">Nakonec je nová třída Stream přiřazená vlastnosti Response. Filter na stránce\_načíst událost, takže poskytuje mechanismus pro změnu obsahu stránky.</span><span class="sxs-lookup"><span data-stu-id="aea6e-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="aea6e-112">&#9654;Přehrát video (13 minut)</span><span class="sxs-lookup"><span data-stu-id="aea6e-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
