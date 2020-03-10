---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: Úprava indexu Z-v DropShadow (C#) | Microsoft Docs
author: wenz
description: Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Tento stín je však někdy v konfliktu s jinými ovládacími prvky pro insta...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613881"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a>Úprava indexu Z ovládacího prvku DropShadow (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Tento stín je však někdy v konfliktu s jinými ovládacími prvky, například ovládací prvek nabídky ASP.NET. Když se položka nabídky objeví, zobrazí se za stínem.

## <a name="overview"></a>Přehled

Ovládací prvek DropShadow v sadě nástrojů AJAX Control Toolkit rozšiřuje panel o Vržený stín. Tento stín je však někdy v konfliktu s jinými ovládacími prvky, například ovládací prvek nabídky ASP.NET. Když se položka nabídky objeví, zobrazí se za stínem.

## <a name="steps"></a>Kroky

Kód se zahájí pomocí samotného panelu, který obsahuje dostatek textu, aby panel obsahoval dostatek textu, aby bylo možné tento efekt zobrazit:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

Další panel je umístěn přímo před `panelShadow` panel. Obsahuje nabídku s vodorovnou orientací, aby se zobrazovaly položky nabídky (nebo místo toho: v rámci) `dropShadow` panel):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

Pak se přidá `DropShadowExtender`, aby se rozšířil panel `panelShadow` s efektem vrženého stínu:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

Nakonec ovládací prvek `ScriptManager` AJAX ASP.NET umožňuje, aby sada nástrojů pracovala:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

Když spustíte tento skript, položky nabídky se zobrazí pod panelem. Nabídka však používá třídu CSS `panel`, kde stačí definovat dvě věci, aby se prvky zobrazovaly před druhým panelem:

- Relativní umístění
- Kladný z-index

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

Ovládací prvek `DropShadowExtender` pak není v konfliktu s ovládacím prvkem nabídky.

[![před: položka nabídky není viditelná.](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

Před: položka nabídky není zobrazená ([kliknutím zobrazíte obrázek v plné velikosti).](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png)

[![po: zobrazí se položka nabídky.](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

Po: zobrazí se položka nabídky ([kliknutím zobrazíte obrázek v plné velikosti](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png)).

> [!div class="step-by-step"]
> [Next](manipulating-dropshadow-properties-from-client-code-cs.md)
