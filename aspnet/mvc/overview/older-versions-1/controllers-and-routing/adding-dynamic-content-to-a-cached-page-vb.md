---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: Přidání dynamického obsahu na stránku v mezipaměti (VB) | Microsoft Docs
author: microsoft
description: Naučte se, jak na stejné stránce kombinovat dynamický obsah a obsah uložený v mezipaměti. Náhrada po mezipaměti umožňuje zobrazit dynamický obsah, jako je například oznámení banneru o...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: f2f4372498e5a38bbfcb96d6e9f6338b0ef4df1f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601610"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a>Přidání dynamického obsahu do stránky v mezipaměti (VB)

od [Microsoftu](https://github.com/microsoft)

> Naučte se, jak na stejné stránce kombinovat dynamický obsah a obsah uložený v mezipaměti. Náhrada po mezipaměti umožňuje zobrazit dynamický obsah, jako jsou reklamní reklamy nebo položky zpráv, v rámci stránky, která je v mezipaměti výstupu.

Když využijete ukládání výstupu do mezipaměti, můžete významně zlepšit výkon aplikace ASP.NET MVC. Místo opětovného generování stránky každou a pokaždé, když je stránka vyžádána, lze stránku vygenerovat jednou a Uložit do mezipaměti pro více uživatelů.

Ale došlo k problému. Co když potřebujete na stránce zobrazit dynamický obsah? Představte si například, že chcete na stránce zobrazit reklamy banner. Nechcete, aby oznámení banneru bylo uložené v mezipaměti, aby se každý uživatel zobrazoval stejně jako reklama. Nemusíte nijak využít žádné peníze.

Naštěstí je snadné řešení. Můžete využít funkci rozhraní ASP.NET, která se nazývá *substituce po mezipaměti*. Substituce po mezipaměti umožňuje nahradit dynamický obsah na stránce, která je v paměti uložena do mezipaměti.

Když ukládáte stránku do mezipaměti pomocí atributu &lt;OutputCache&gt;, stránka je uložena do mezipaměti na serveru i klientovi (webový prohlížeč). Když použijete substituci po mezipaměti, stránka je ukládána pouze do mezipaměti na serveru.

#### <a name="using-post-cache-substitution"></a>Použití náhrady po mezipaměti

Použití náhrady po mezipaměti vyžaduje dva kroky. Nejprve je třeba definovat metodu, která vrátí řetězec reprezentující dynamický obsah, který chcete zobrazit na stránce v mezipaměti. Dále zavoláte metodu HttpResponse. WriteSubstitution (), která vloží dynamický obsah do stránky.

Představte si například, že chcete náhodně zobrazit různé položky zpráv na stránce v mezipaměti. Třída v seznamu 1 zpřístupňuje jedinou metodu s názvem RenderNews (), která náhodně vrátí jednu položku zprávy ze seznamu tří položek zpráv.

**Výpis 1 – Models\News.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

Chcete-li využít výhod po nahrazení po mezipaměti, zavoláte metodu HttpResponse. WriteSubstitution (). Metoda WriteSubstitution () nastaví kód pro nahrazení oblasti stránky v mezipaměti dynamickým obsahem. Metoda WriteSubstitution () slouží k zobrazení položky náhodné zprávy v zobrazení v seznamu 2.

**Výpis 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

Metoda RenderNews je předána metodě WriteSubstitution (). Všimněte si, že metoda RenderNews není volána. Místo toho je odkaz na metodu předána do WriteSubstitution () s použitím operátoru AddressOf.

Zobrazení index je uloženo v mezipaměti. Zobrazení je vráceno řadičem v seznamu 3. Všimněte si, že akce index () je upravena pomocí atributu &lt;OutputCache&gt;, který způsobí, že je zobrazení indexu uloženo do mezipaměti po dobu 60 sekund.

**Výpis 3 – Controllers\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

I když je zobrazení indexu uloženo do mezipaměti, při vyžádání stránky indexu se zobrazí jiné náhodné položky zpráv. Když vyžádáte stránku indexu, čas zobrazený stránkou se nezmění po dobu 60 sekund (viz obrázek 1). Skutečnost, že se čas nezmění, potvrzuje, že je stránka uložena do mezipaměti. Obsah, který je vložen metodou WriteSubstitution () – náhodná zpráva – mění se pomocí jednotlivých požadavků.

**Obrázek 1 – vkládání dynamických položek zpráv na stránce v mezipaměti**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Použití náhrady po mezipaměti v pomocných metodách

Jednodušší způsob, jak využít substituci po mezipaměti, je zapouzdřit volání metody WriteSubstitution () v rámci vlastní pomocné metody. Tento přístup je znázorněný pomocnou metodou v seznamu 4.

**Výpis 4 – Helpers\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

Výpis 4 obsahuje modul Visual Basic, který zpřístupňuje dvě metody: RenderBanner () a RenderBannerInternal (). Metoda RenderBanner () představuje skutečnou pomocnou metodu. Tato metoda rozšiřuje standardní třídu ASP.NET MVC HtmlHelper, takže můžete volat HTML. RenderBanner () v zobrazení stejně jako jakákoli jiná pomocná metoda.

Metoda RenderBanner () volá metodu HttpResponse. WriteSubstitution (), která předává metodu RenderBannerInternal () metodě WriteSubstitution ().

Metoda RenderBannerInternal () je privátní metoda. Tato metoda nebude vystavena jako pomocná metoda. Metoda RenderBannerInternal () náhodně vrátí jednu hlavičku oznámení reklamy ze seznamu tří obrázků reklamní reklamy.

Změněné zobrazení indexu v seznamu 5 ukazuje, jak lze použít pomocnou metodu RenderBanner (). Všimněte si, že v horní části zobrazení je k dispozici další direktiva &lt;% @ import%&gt;, která umožňuje importovat obor názvů MvcApplication1. helps. Pokud opomíjení pro import tohoto oboru názvů, metoda RenderBanner () se nezobrazí jako metoda ve vlastnosti HTML.

**Výpis 5 – Views\Home\Index.aspx (s metodou RenderBanner ())**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

Když vyžádáte stránku vygenerovanou zobrazením v seznamu 5, zobrazí se u každé žádosti jiné oznámení banneru (viz obrázek 2). Tato stránka je uložena do mezipaměti, ale pomocí pomocné metody RenderBanner () je inzerování reklamy dynamicky vloženo.

**Obrázek 2 – zobrazení indexu s náhodným inzerováním banneru**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>Souhrn

V tomto kurzu se vysvětluje, jak můžete dynamicky aktualizovat obsah na stránce v mezipaměti. Zjistili jste, jak pomocí metody HttpResponse. WriteSubstitution () povolit vložení dynamického obsahu na stránku v mezipaměti. Zjistili jste také, jak zapouzdřit volání do metody WriteSubstitution () v rámci pomocné metody HTML.

Využijte možnost ukládání do mezipaměti, kdykoli to bude možné – může to mít výrazný dopad na výkon webových aplikací. Jak je vysvětleno v tomto kurzu, můžete využít výhod ukládání do mezipaměti i v případě, že na svých stránkách potřebujete zobrazit dynamický obsah.

> [!div class="step-by-step"]
> [Předchozí](improving-performance-with-output-caching-vb.md)
> [Další](creating-a-controller-vb.md)
