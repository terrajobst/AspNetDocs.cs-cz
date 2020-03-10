---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: Dynamické Přidání podokna pro přiznávání (VB) | Microsoft Docs
author: wenz
description: Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: be48db5ea3de4af46b0f864cc9e73d2f518294a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598320"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a>Dynamické Přidání podokna pro přiznávání (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)

> Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány v rámci samotné stránky, ale kód na straně serveru lze použít k dosažení stejného výsledku.

## <a name="overview"></a>Přehled

Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány v rámci samotné stránky, ale kód na straně serveru lze použít k dosažení stejného výsledku.

## <a name="steps"></a>Kroky

Řízení přiznávání zveřejňuje všechny důležité vlastnosti kódu na straně serveru. Mimo jiné vlastnost `Panes` uděluje přístup ke kolekci podoken, která tvoří danou přiznávání. Každé podokno je typu `AccordionPane`. Proto je triviální vytvořit takové podokno:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

Vlastnost `HeaderContainer` `AccordionPane` poskytuje přístup k ovládacím prvkům ASP.NET v části záhlaví v podokně; vlastnost `ContentContainer` `AccordionPane` má pro oddíl Content v podokně stejný obsah. To umožňuje ASP.NET kódu přidávat obsah do podoken:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

Nakonec je třeba přidat podokna do `Panes` kolekce přiznávání:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

Tady je kompletní kód na straně serveru, který do ovládacího prvku pro řízení přihlašování přičítá dvě podokna:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

Jediným chybějícím prvkem je samotné přiznávání, které závisí na přítomnosti ovládacího prvku ASP.NET `ScriptManager`:

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

Chcete-li dokončit příklad, dvě třídy CSS, na které se odkazuje v ovládacím prvku pro přiznávání, poskytují informace o stylu prohlížeče:

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

[![data v přiznávání dynamicky přidal kód na straně serveru.](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)

Data v přiznávání se dynamicky přidala přes kód na straně serveru ([kliknutím zobrazíte obrázek v plné velikosti).](dynamically-adding-an-accordion-pane-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](databinding-to-an-accordion-vb.md)
