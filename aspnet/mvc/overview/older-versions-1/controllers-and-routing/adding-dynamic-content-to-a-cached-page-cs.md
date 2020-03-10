---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: Přidání dynamického obsahu na stránku v mezipamětiC#() | Microsoft Docs
author: microsoft
description: Naučte se, jak na stejné stránce kombinovat dynamický obsah a obsah uložený v mezipaměti. Náhrada po mezipaměti umožňuje zobrazit dynamický obsah, jako je například oznámení banneru o...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601582"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>Přidání dynamického obsahu do stránky v mezipaměti (C#)

od [Microsoftu](https://github.com/microsoft)

> Naučte se, jak na stejné stránce kombinovat dynamický obsah a obsah uložený v mezipaměti. Náhrada po mezipaměti umožňuje zobrazit dynamický obsah, jako jsou reklamní reklamy nebo položky zpráv, v rámci stránky, která je v mezipaměti výstupu.

Když využijete ukládání výstupu do mezipaměti, můžete významně zlepšit výkon aplikace ASP.NET MVC. Místo opětovného generování stránky každou a pokaždé, když je stránka vyžádána, lze stránku vygenerovat jednou a Uložit do mezipaměti pro více uživatelů.

Ale došlo k problému. Co když potřebujete na stránce zobrazit dynamický obsah? Představte si například, že chcete na stránce zobrazit reklamy banner. Nechcete, aby oznámení banneru bylo uložené v mezipaměti, aby se každý uživatel zobrazoval stejně jako reklama. Nemusíte nijak využít žádné peníze.

Naštěstí je snadné řešení. Můžete využít funkci rozhraní ASP.NET, která se nazývá *substituce po mezipaměti*. Substituce po mezipaměti umožňuje nahradit dynamický obsah na stránce, která je v paměti uložena do mezipaměti.

Když ukládáte stránku do mezipaměti pomocí atributu [OutputCache], stránka je uložena do mezipaměti na serveru i v klientovi (webový prohlížeč). Když použijete substituci po mezipaměti, stránka je ukládána pouze do mezipaměti na serveru.

#### <a name="using-post-cache-substitution"></a>Použití náhrady po mezipaměti

Použití náhrady po mezipaměti vyžaduje dva kroky. Nejprve je třeba definovat metodu, která vrátí řetězec reprezentující dynamický obsah, který chcete zobrazit na stránce v mezipaměti. Dále zavoláte metodu HttpResponse. WriteSubstitution (), která vloží dynamický obsah do stránky.

Představte si například, že chcete náhodně zobrazit různé položky zpráv na stránce v mezipaměti. Třída v seznamu 1 zpřístupňuje jedinou metodu s názvem RenderNews (), která náhodně vrátí jednu položku zprávy ze seznamu tří položek zpráv.

**Výpis 1 – Models\News.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

Chcete-li využít výhod po nahrazení po mezipaměti, zavoláte metodu HttpResponse. WriteSubstitution (). Metoda WriteSubstitution () nastaví kód pro nahrazení oblasti stránky v mezipaměti dynamickým obsahem. Metoda WriteSubstitution () slouží k zobrazení položky náhodné zprávy v zobrazení v seznamu 2.

**Výpis 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

Metoda RenderNews je předána metodě WriteSubstitution (). Všimněte si, že metoda RenderNews není volána (nejsou k dispozici žádné závorky). Místo toho je předán odkaz na metodu WriteSubstitution ().

Zobrazení index je uloženo v mezipaměti. Zobrazení je vráceno řadičem v seznamu 3. Všimněte si, že akce index () je upravena pomocí atributu [OutputCache], který způsobí, že zobrazení indexu bude uloženo do mezipaměti po dobu 60 sekund.

**Výpis 3 – souboru controllers\homecontroller.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

I když je zobrazení indexu uloženo do mezipaměti, při vyžádání stránky indexu se zobrazí jiné náhodné položky zpráv. Když vyžádáte stránku indexu, čas zobrazený stránkou se nezmění po dobu 60 sekund (viz obrázek 1). Skutečnost, že se čas nezmění, potvrzuje, že je stránka uložena do mezipaměti. Obsah, který je vložen metodou WriteSubstitution () – náhodná zpráva – mění se pomocí jednotlivých požadavků.

**Obrázek 1 – vkládání dynamických položek zpráv na stránce v mezipaměti**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Použití náhrady po mezipaměti v pomocných metodách

Jednodušší způsob, jak využít substituci po mezipaměti, je zapouzdřit volání metody WriteSubstitution () v rámci vlastní pomocné metody. Tento přístup je znázorněný pomocnou metodou v seznamu 4.

**Výpis 4 – AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

Výpis 4 obsahuje statickou třídu, která zveřejňuje dvě metody: RenderBanner () a RenderBannerInternal (). Metoda RenderBanner () představuje skutečnou pomocnou metodu. Tato metoda rozšiřuje standardní třídu ASP.NET MVC HtmlHelper, takže můžete volat HTML. RenderBanner () v zobrazení stejně jako jakákoli jiná pomocná metoda.

Metoda RenderBanner () volá metodu HttpResponse. WriteSubstitution (), která předává metodu RenderBannerInternal () metodě WriteSubstitution ().

Metoda RenderBannerInternal () je privátní metoda. Tato metoda nebude vystavena jako pomocná metoda. Metoda RenderBannerInternal () náhodně vrátí jednu hlavičku oznámení reklamy ze seznamu tří obrázků reklamní reklamy.

Změněné zobrazení indexu v seznamu 5 ukazuje, jak lze použít pomocnou metodu RenderBanner (). Všimněte si, že v horní části zobrazení je k dispozici další direktiva &lt;% @ import%&gt;, která umožňuje importovat obor názvů MvcApplication1. helps. Pokud opomíjení pro import tohoto oboru názvů, metoda RenderBanner () se nezobrazí jako metoda ve vlastnosti HTML.

**Výpis 5 – Views\Home\Index.aspx (s metodou RenderBanner ())**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

Když vyžádáte stránku vygenerovanou zobrazením v seznamu 5, zobrazí se u každé žádosti jiné oznámení banneru (viz obrázek 2). Tato stránka je uložena do mezipaměti, ale pomocí pomocné metody RenderBanner () je inzerování reklamy dynamicky vloženo.

**Obrázek 2 – zobrazení indexu s náhodným inzerováním banneru**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>Souhrn

V tomto kurzu se vysvětluje, jak můžete dynamicky aktualizovat obsah na stránce v mezipaměti. Zjistili jste, jak pomocí metody HttpResponse. WriteSubstitution () povolit vložení dynamického obsahu na stránku v mezipaměti. Zjistili jste také, jak zapouzdřit volání do metody WriteSubstitution () v rámci pomocné metody HTML.

Využijte možnost ukládání do mezipaměti, kdykoli to bude možné – může to mít výrazný dopad na výkon webových aplikací. Jak je vysvětleno v tomto kurzu, můžete využít výhod ukládání do mezipaměti i v případě, že na svých stránkách potřebujete zobrazit dynamický obsah.

> [!div class="step-by-step"]
> [Předchozí](improving-performance-with-output-caching-cs.md)
> [Další](creating-a-controller-cs.md)
