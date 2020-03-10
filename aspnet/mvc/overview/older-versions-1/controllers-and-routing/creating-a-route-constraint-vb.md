---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: Vytvoření omezení trasy (VB) | Microsoft Docs
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak se požadavky prohlížeče shodují s trasami vytvořením omezení trasy pomocí regulárních výrazů.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 205742dd8f866c8828008c8aac7ab3f98b173ceb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601386"
---
# <a name="creating-a-route-constraint-vb"></a>Vytvoření omezení trasy (VB)

od [Stephen Walther](https://github.com/StephenWalther)

> V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak se požadavky prohlížeče shodují s trasami vytvořením omezení trasy pomocí regulárních výrazů.

Omezení tras použijete k omezení požadavků prohlížeče, které odpovídají konkrétní trase. K určení omezení trasy můžete použít regulární výraz.

Představte si například, že jste v souboru Global. asax definovali trasu v seznamu 1.

**Výpis 1 – Global. asax. vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

Výpis 1 obsahuje trasu s názvem produkt. Můžete použít trasu produktu k mapování požadavků prohlížeče na ProductController obsaženou v seznamu 2.

**Výpis 2 – Controllers\ProductController.vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

Všimněte si, že akce podrobnosti () vystavená produktovým adaptérem přijímá jeden parametr s názvem productId. Tento parametr je celočíselným parametrem.

Trasa definovaná v seznamu 1 bude odpovídat všem následujícím adresám URL:

- /Product/23
- /Product/7

Tato trasa bohužel bude taky odpovídat následujícím adresám URL:

- /Product/blah
- /Product/apple

Vzhledem k tomu, že akce Details () očekává parametr typu Integer, vytvoření požadavku, který obsahuje něco jiného než celočíselné hodnoty způsobí chybu. Pokud například zadáte adresu URL/Product/Apple do prohlížeče, zobrazí se chybová stránka na obrázku 1.

[![dialogového okna Nový projekt](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)

**Obrázek 01**: zobrazení rozbalené stránky ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-route-constraint-vb/_static/image2.png))

Co opravdu chcete udělat, odpovídá jenom adresám URL, které obsahují správné celé číslo productId. Omezení můžete použít při definování trasy, která bude omezovat adresy URL, které odpovídají trase. Upravená trasa produktu v seznamu 3 obsahuje omezení regulárního výrazu, které odpovídá pouze celým číslům.

**Výpis 3 – Global. asax. vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

Regulární výraz \D + odpovídá jednomu nebo více celým číslům. Toto omezení způsobí, že trasa produktu bude odpovídat následujícím adresám URL:

- /Product/3
- /Product/8999

Ale ne následující adresy URL:

- /Product/apple
- /Product

Tyto požadavky prohlížeče budou zpracovány jinou trasou, nebo pokud nejsou k dispozici žádné vyhovující trasy, nebude možné *najít prostředek* , který se vrátí.

> [!div class="step-by-step"]
> [Předchozí](creating-custom-routes-vb.md)
> [Další](creating-a-custom-route-constraint-vb.md)
