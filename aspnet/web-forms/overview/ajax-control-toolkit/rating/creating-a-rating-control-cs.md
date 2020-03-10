---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: Vytvoření ovládacího prvku hodnocení (C#) | Microsoft Docs
author: wenz
description: Mnoho webů, od elektronického obchodování po komunitní weby, nabízí svým uživatelům hodnocení článků nebo položek. To obvykle vyžaduje určité úsilí při psaní kódu, ale máme...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612341"
---
# <a name="creating-a-rating-control-c"></a>Vytvoření ovládacího prvku Rating (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)

> Mnoho webů, od elektronického obchodování po komunitní weby, nabízí svým uživatelům hodnocení článků nebo položek. To obvykle vyžaduje určité úsilí při psaní kódu, ale máme k dispozici sadu nástrojů Control Toolkit.

## <a name="overview"></a>Přehled

Mnoho webů, od elektronického obchodování po komunitní weby, nabízí svým uživatelům hodnocení článků nebo položek. To obvykle vyžaduje určité úsilí při psaní kódu, ale máme k dispozici sadu nástrojů Control Toolkit.

## <a name="steps"></a>Kroky

Nejdřív potřebujete (aspoň) dva druhy imagí: jednu pro vyplněnou položku hodnocení a jednu pro prázdnou položku hodnocení. Položka hodnocení je obvykle hvězdička nebo smajlík. V tomto scénáři najdete tři soubory, smajlík. png a prázdné. png a Smiley-Done. png jako součást souborů ke stažení zdrojového kódu pro účely tohoto kurzu.

Pak vytvořte nový soubor ASP.NET a začněte přidáním ovládacího prvku `ScriptManager`:

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

Pak přidejte ovládací prvek `Rating` z ovládací sady nástrojů AJAX pro ASP.NET. Pro tento příklad je nutné nastavit následující atributy:

- `CurrentRating` počáteční hodnocení, které se má použít
- `MaxRating` maximální hodnocení.
- `EmptyStarCssClass` třídy šablony stylů CSS, která se má použít, pokud je položka hodnocení (hvězda) prázdná
- `FilledStarCssClass` třídy šablony stylů CSS, která se má použít, když se vyplní položka hodnocení (hvězda)
- `StarCssClass` třídy CSS, která se má použít pro viditelné staty
- `WaitingStarCssClass` třídy šablony stylů CSS, která se má použít, když se na server pošle hodnocení hvězdičkami zpátky

A zde je značka, která vytvoří ovládací prvek hodnocení s pěti položkami (Smileys), z nichž není původně vyplněna žádná hodnota:

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

Tři odkazované třídy CSS teď potřebují zobrazit vhodné soubory obrázků, které je snadné použít CSS:

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

Ujistěte se, že zadáváte šířku a výšku tří imagí. v opačném případě se může zobrazit bitová kopie.

Nakonec by se měl výsledek hodnocení zobrazit uživateli (nebo alespoň v databázi). Přidejte tedy popisek pro výstup textové zprávy a tlačítko Odeslat pro odeslání zpět formuláře hodnocení na server:

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

V kódu na straně serveru přihlaste k ovládacímu prvku hodnocení prostřednictvím jeho `ID` a potom přejděte k jeho vlastnosti `CurrentRating`, která představuje počet vybraných položek hodnocení. v našem příkladu je to hodnota mezi 0 a 5.

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

Uložte stránku a načtěte ji do prohlížeče. Když najedete myší na položky hodnocení (počáteční prázdné), dojde k efektu JavaScriptu: hodnocení se změní. Když kliknete na sadu hvězdiček, aktuální hodnocení se zachová. Nakonec při odeslání formuláře výstup kódu na straně serveru vypíše vybrané hodnocení.

[![vytvoření systému hodnocení s minimálním kódem](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)

Vytvoření systému hodnocení s minimálním kódem ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-rating-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](creating-a-rating-control-vb.md)
