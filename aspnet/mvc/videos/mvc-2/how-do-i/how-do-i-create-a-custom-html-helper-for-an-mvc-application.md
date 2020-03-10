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
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a>Jak mohu: vytvořit vlastní nápovědu HTML pro aplikaci MVC?

autor – [Chris pixelů na](https://twitter.com/chrispels)

V tomto videu Chris pixelů na ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici ve standardní sadě v aplikaci MVC. Nejdřív se vytvoří ukázková aplikace MVC s ukázkovým kontrolérem a zobrazením, které otestuje vlastní HtmlHelper. Dále je vytvořen modul s veřejnou funkcí, která představuje metodu rozšíření, která představuje implementaci vlastního HtmlHelper. Vlastní pomoc je určena k vytváření značek `<img>` na stránce a přijímá několik vstupních parametrů, včetně ID, adresy URL a alternativního textu pro značku obrázku. Logika je pak přidána do funkce pro vrácení dokončené `<img>` značky se zadanými informacemi. Pak se vlastní HtmlHelper použije na stránce demo k zobrazení obrázku. Nakonec je vlastní HtmlHelper rozbalený tak, aby zahrnovalo více přepsání konstruktoru, což poskytuje flexibilitu pro snazší vytváření různých `<img>` značek.

[&#9654;Sledovat video (18 minut)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> [Předchozí](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [Další](how-do-i-work-with-model-binders-in-an-mvc-application.md)
