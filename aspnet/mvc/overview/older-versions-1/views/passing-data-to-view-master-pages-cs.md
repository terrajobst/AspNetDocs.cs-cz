---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: Předávání dat pro zobrazení stránek předlohy (C#) | Microsoft Docs
author: microsoft
description: Cílem tohoto kurzu je vysvětlit, jak můžete předat data z kontroleru na stránku zobrazení předlohy. Prověříme dvě strategie předávání dat do zobrazení m...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 1492175812b0a092cd1594a770e348efe9b4122b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593766"
---
# <a name="passing-data-to-view-master-pages-c"></a>Předání dat stránkám předlohy pro zobrazení (C#)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> Cílem tohoto kurzu je vysvětlit, jak můžete předat data z kontroleru na stránku zobrazení předlohy. Prověříme dvě strategie předávání dat na stránku zobrazení předlohy. Nejdřív se podíváme na jednoduché řešení, které vede k obtížné údržbě aplikace. V dalším kroku prověříme mnohem lepší řešení, které vyžaduje trochu pokročilejší práci, ale má za následek mnohem udržovatelnější aplikaci.

## <a name="passing-data-to-view-master-pages"></a>Předávání dat pro zobrazení stránek předlohy

Cílem tohoto kurzu je vysvětlit, jak můžete předat data z kontroleru na stránku zobrazení předlohy. Prověříme dvě strategie předávání dat na stránku zobrazení předlohy. Nejdřív se podíváme na jednoduché řešení, které vede k obtížné údržbě aplikace. V dalším kroku prověříme mnohem lepší řešení, které vyžaduje trochu pokročilejší práci, ale má za následek mnohem udržovatelnější aplikaci.

### <a name="the-problem"></a>Problém

Představte si, že vytváříte aplikaci filmové databáze a chcete zobrazit seznam kategorií filmů na každé stránce aplikace (viz obrázek 1). Představte si, že seznam kategorií filmů je uložený v databázové tabulce. V takovém případě by měla smysl načíst kategorie z databáze a vykreslovat seznam kategorií filmů v rámci zobrazení stránky předlohy.

[![zobrazení kategorií filmů na stránce zobrazení předlohy](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)

**Obrázek 01**: zobrazení kategorií filmů na stránce předlohy zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](passing-data-to-view-master-pages-cs/_static/image3.png))

Tady je problém. Jak načíst seznam kategorií videí na stránce předlohy? Nachází se na metody třídy modelu přímo na stránce předlohy. Jinými slovy, sestává z toho, že je nutné zahrnout kód pro načítání dat z databáze přímo na stránce předlohy. Obcházení řadičů MVC pro přístup k databázi by však narušilo čisté oddělení potíží, které je jednou z hlavních výhod sestavení aplikace MVC.

V aplikaci MVC chcete mít veškerou interakci mezi zobrazeními MVC a modelem MVC, aby je bylo možné zpracovat pomocí řadičů MVC. Toto oddělení obav má za následek udržovatelnější, přizpůsobitelnou a testovatelné aplikaci.

V aplikaci MVC jsou všechna data předaná do zobrazení – včetně hlavní stránky zobrazení – by měla být předána zobrazením pomocí akce kontroleru. Data by se měla předat dál tím, že se budou používat data zobrazení. Ve zbývající části tohoto kurzu prohlížíme dvě metody předávání dat zobrazení na stránku zobrazení předlohy.

### <a name="the-simple-solution"></a>Jednoduché řešení

Pojďme začít s nejjednodušším řešením pro předávání dat zobrazení z kontroleru na stránku zobrazení předlohy. Nejjednodušším řešením je předat data zobrazení stránky předlohy v každé a každé akci kontroleru.

Vezměte v úvahu kontroler v seznamu 1. Zpřístupňuje dvě akce s názvem `Index()` a `Details()`. Metoda `Index()` akce vrátí všechny filmy v tabulce databáze filmů. Metoda `Details()` akce vrátí každý film v konkrétní kategorii videa.

**Výpis 1 – `Controllers\HomeController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

Všimněte si, že akce index () i Details () přidávají dvě položky k zobrazení dat. Akce index () přidá dva klíče: kategorie a filmy. Klíč kategorie představuje seznam kategorií filmů zobrazených na stránce zobrazení předlohy. Klíč filmů představuje seznam filmů zobrazených na stránce zobrazení indexu.

Akce podrobnosti () také přidá dva klíče s názvem kategorie a filmy. Klíč kategorie, jednou znovu, představuje seznam kategorií filmů zobrazených na stránce předloha zobrazení. Klíč filmy představuje seznam filmů v určité kategorii zobrazené na stránce zobrazení podrobností (viz obrázek 2).

[![zobrazení podrobností](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)

**Obrázek 02**: zobrazení podrobností ([kliknutím zobrazíte obrázek v plné velikosti](passing-data-to-view-master-pages-cs/_static/image6.png))

Zobrazení index je obsaženo v seznamu 2. Jednoduše projde seznam filmů reprezentovaných položkou filmy v zobrazení dat.

**Výpis 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

Stránka zobrazení předlohy je obsažena v seznamu 3. Stránka Zobrazit předloha prochází a vykresluje všechny kategorie videí reprezentované položkou Categories z zobrazení dat.

**Výpis 3 – `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

Všechna data jsou předána do zobrazení a stránka zobrazení předlohy prostřednictvím zobrazení dat. To je správný způsob, jak předat data do stránky předlohy.

Co je to u tohoto řešení špatné? Problémem je to, že toto řešení porušuje zásadu SUCHÉho (princip "Neopakuj se"). Každá akce kontroleru musí pro zobrazení dat přidat stejný seznam kategorií videí. Pokud máte v aplikaci duplicitní kód, je vaše aplikace mnohem obtížnější udržovat, přizpůsobit a upravit.

### <a name="the-good-solution"></a>Dobré řešení

V této části prověříme alternativní a lepší řešení pro předávání dat z akce kontroleru na stránku zobrazení předlohy. Místo přidávání kategorií filmů pro hlavní stránku v každé akci kontroleru přidáváme kategorie videa do zobrazení dat jenom jednou. Všechna data zobrazení, která jsou používána stránkou předlohy zobrazení, se přidají do kontroleru aplikací.

Třída ApplicationController je obsažena v seznamu 4.

**Výpis 4 – `Controllers\ApplicationController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

Existují tři věci, které byste si měli všimnout o řadiči aplikace v seznamu 4. Nejprve si všimněte, že třída dědí ze základní třídy System. Web. Mvc. Controller. Kontroler aplikací je třída kontroleru.

Za druhé si všimněte, že třída kontroleru aplikace je abstraktní třída. Abstraktní třída je třída, která musí být implementována konkrétní třídou. Vzhledem k tomu, že je řadič aplikace abstraktní třídou, nelze vyvolat žádné metody definované ve třídě přímo. Pokud se pokusíte třídu aplikace vyvolat přímo, zobrazí se chybová zpráva, že se nepovedlo najít prostředek.

Třetí, Všimněte si, že kontroler aplikací obsahuje konstruktor, který přidá seznam kategorií videí pro zobrazení dat. Každá třída kontroleru, která dědí z kontroleru aplikace, volá automaticky konstruktor řadiče aplikace. Pokaždé, když zavoláte jakoukoli akci na jakémkoli řadiči, který dědí z kontroleru aplikace, jsou kategorie filmů zahrnuty do automaticky zobrazených dat.

Kontroler filmů v výpisu 5 dědí z řadiče aplikace.

**Výpis 5 – `Controllers\MoviesController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

Kontroler filmů, stejně jako u domovského kontroleru popsaných v předchozí části, zpřístupňuje dvě metody akcí s názvem `Index()` a `Details()`. Všimněte si, že seznam kategorií filmů zobrazených pomocí hlavní stránky zobrazení není přidaný k zobrazení dat v metodě `Index()` ani `Details()`. Vzhledem k tomu, že kontroler filmů dědí z kontroleru aplikace, je k automatickému zobrazení dat přidána seznam kategorií filmů.

Všimněte si, že toto řešení pro přidání dat zobrazení pro zobrazení hlavní stránky nebrání v rozporu s SUCHou (princip "Neopakuj se") principem. Kód pro přidání seznamu kategorií videí pro zobrazení dat je obsažen pouze v jednom umístění: konstruktor pro řadič aplikace.

### <a name="summary"></a>Přehled

V tomto kurzu jsme probrali dva přístupy k předávání dat zobrazení z kontroleru na stránku zobrazení Předloha. Nejprve jsme prozkoumali jednoduchý, ale obtížně zachováme přístup. V první části jsme probrali, jak můžete přidat data zobrazení pro stránku předlohy zobrazení v každé akci kontroleru v aplikaci. Dospěli jsme k závěru, že se jedná o špatný přístup, protože je v rozporu s SUCHou (princip "Neopakuj se") principem.

Dále jsme prozkoumali mnohem lepší strategii pro přidávání dat vyžadovaných stránkou předlohy zobrazení k zobrazení dat. Místo přidávání dat zobrazení v jednotlivých a všech akcích kontroléru jsme přidali data zobrazení pouze jednou v rámci kontroleru aplikace. Tímto způsobem se můžete vyhnout duplicitnímu kódu při předávání dat na stránku zobrazení předlohy v aplikaci ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](creating-page-layouts-with-view-master-pages-cs.md)
> [Další](asp-net-mvc-views-overview-vb.md)
