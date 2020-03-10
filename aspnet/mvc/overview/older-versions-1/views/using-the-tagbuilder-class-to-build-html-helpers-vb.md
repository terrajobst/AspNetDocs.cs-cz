---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: Použití třídy TagBuilder k vytváření pomocníků HTML (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther vás seznámí s užitečnou třídou nástrojů v rozhraní ASP.NET MVC s názvem třídy TagBuilder. Můžete snadno použít třídu TagBuilder...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600000"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a>Použití třídy TagBuilder k vytváření pomocníků HTML (VB)

od [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther vás seznámí s užitečnou třídou nástrojů v rozhraní ASP.NET MVC s názvem třídy TagBuilder. Třídu TagBuilder lze použít k snadnému sestavení značek jazyka HTML.

Rozhraní ASP.NET MVC obsahuje užitečnou třídu nástrojů nazvanou TagBuilder třídu, kterou lze použít při vytváření pomocníků HTML. Třída TagBuilder, jak naznačuje název třídy, umožňuje snadno vytvářet značky HTML. V tomto stručném kurzu se poskytuje přehled třídy TagBuilder a naučíte se, jak tuto třídu použít při vytváření jednoduchého pomocníka HTML, který vykresluje HTML &lt;img&gt; značky.

## <a name="overview-of-the-tagbuilder-class"></a>Přehled třídy TagBuilder

Třída TagBuilder je obsažena v oboru názvů System. Web. Mvc. Má pět metod:

- AddCssClass () – umožňuje přidat do značky nový atribut *Class = ""* .
- GenerateId () – umožňuje přidat atribut ID k značce. Tato metoda automaticky nahrazuje tečky v ID (ve výchozím nastavení jsou tečky nahrazeny podtržítky).
- MergeAttribute () – umožňuje přidat atributy do značky. Existuje více přetížení této metody.
- SetInnerText () – umožňuje nastavit vnitřní text značky. Vnitřní text je automaticky kódován HTML.
- ToString () – umožňuje vykreslit značku. Můžete určit, zda chcete vytvořit normální značku, počáteční značku, koncovou značku nebo samočinnou uzavírací značku.

Třída TagBuilder má čtyři důležité vlastnosti:

- Atributy – představuje všechny atributy značky.
- IdAttributeDotReplacement – představuje znak používaný metodou GenerateId () k nahrazení teček (výchozí je podtržítko).
- InnerHTML – představuje vnitřní obsah značky. Přiřazení řetězce k *této vlastnosti* nekóduje řetězec ve formátu HTML.
- TagName – představuje název značky.

Tyto metody a vlastnosti poskytují všechny základní metody a vlastnosti, které potřebujete k vytvoření značky jazyka HTML. Ve skutečnosti nemusíte používat třídu TagBuilder. Místo toho můžete použít třídu StringBuilder. Třída TagBuilder ale ještě víc zjednodušuje život.

## <a name="creating-an-image-html-helper"></a>Vytvoření pomocníka s obrázkem HTML

Při vytváření instance třídy TagBuilder předáte název značky, kterou chcete sestavit do konstruktoru TagBuilder. Dále můžete volat metody jako metody AddCssClass a MergeAttribute () pro úpravu atributů značky. Nakonec zavoláte metodu ToString () pro vykreslení značky.

Například výpis 1 obsahuje pomocníka s obrázkem HTML. Pomocná rutina Image je implementována interně pomocí TagBuilder, který představuje značku&gt; HTML &lt;img.

**Výpis 1 – Helpers\ImageHelper.vb**

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

Modul v seznamu 1 obsahuje dvě přetížené metody s názvem Image (). Při volání metody image () můžete předat objekt, který představuje sadu atributů HTML, nebo ne.

Všimněte si, jak metoda TagBuilder. MergeAttribute () slouží k přidání jednotlivých atributů, jako je například atribut src, do TagBuilder. Všimněte si navíc, jak metoda TagBuilder. MergeAttributes () slouží k přidání kolekce atributů do TagBuilder. Metoda MergeAttributes () přijímá slovník&lt;řetězec&gt; parametr. Třída RouteValueDictionary slouží k převodu objektu reprezentujícího kolekci atributů do slovníku&lt;řetězec&gt;objektu.

Po vytvoření pomocné rutiny image můžete použít pomocníka v zobrazeních ASP.NET MVC stejným způsobem jako kterýkoli jiný standardní pomocník HTML. Zobrazení v seznamu 2 používá pomocníka pro Image k zobrazení stejné image Xbox dvakrát (viz obrázek 1). Pomocná rutina () se nazývá s kolekcí atributů HTML i bez ní.

**Výpis 2 – Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

[![dialogového okna Nový projekt](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)

**Obrázek 01**: použití pomocné rutiny Image ([kliknutím zobrazíte obrázek v plné velikosti](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))

Všimněte si, že musíte importovat obor názvů přidružený k pomocné rutině image v horní části zobrazení index. aspx. Pomocná rutina se importuje s následující direktivou:

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

V Visual Basic aplikaci je výchozí obor názvů stejný jako název aplikace.

> [!div class="step-by-step"]
> [Předchozí](creating-custom-html-helpers-vb.md)
> [Další](creating-page-layouts-with-view-master-pages-vb.md)
