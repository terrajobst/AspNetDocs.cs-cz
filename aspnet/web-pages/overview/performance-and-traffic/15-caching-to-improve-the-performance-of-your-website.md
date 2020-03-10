---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: Ukládání dat do mezipaměti na webu ASP.NET Web Pages (Razor) pro lepší výkon | Microsoft Docs
author: Rick-Anderson
description: Svůj web můžete urychlit tím, že ho uložíte – to znamená mezipaměť – výsledky dat, které by obvykle vyžadovaly značnou dobu načtení nebo zpracování...
ms.author: riande
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 01796d3ca699a6af5d9162b22a926551435c2040
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641517"
---
# <a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a>Ukládání dat do mezipaměti na webu ASP.NET Web Pages (Razor) pro lepší výkon

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak používat pomocníka k ukládání informací do mezipaměti pro rychlejší výkon na webu ASP.NET Web Pages (Razor). Svůj web můžete urychlit tím, že jeho úložiště &#8212; ukládá do mezipaměti &#8212; výsledky dat, která by obvykle vyžadovala značnou dobu načítání nebo zpracování a která se často nemění.
> 
> **Co se naučíte:** 
> 
> - Jak používat ukládání do mezipaměti ke zlepšení rychlosti odezvy vašeho webu.
> 
> Jedná se o funkce ASP.NET, které jsou představené v článku:
> 
> - Pomocná rutina `WebCache`
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

Pokaždé, když někdo požádá o stránku z vaší lokality, musí webový server provést nějakou práci, aby mohl splnit požadavek. Pro některé stránky může server potřebovat provádět úlohy, které provádějí (relativně) dlouhou dobu, například načtení dat z databáze. I v případě, že tyto úlohy netrvají v absolutních výrazech, může v případě velkého množství provozu celá řada jednotlivých požadavků, které způsobují, že webový server provádí složitou nebo pomalou úlohu, způsobit větší množství práce. To může mít nakonec vliv na výkon lokality.

Jedním ze způsobů, jak zlepšit výkon webu za takových okolností, je ukládat data do mezipaměti. Pokud vaše lokalita vrátí opakované požadavky na tytéž informace a informace pro každého uživatele nemusíte měnit a nejedná se o citlivou velikost, místo aby se znovu načetla nebo převedla jejich kalkulace, můžete načíst data jednou a pak výsledky uložit. Až v okamžiku, kdy se do této informace poprvé přijde požadavek, dostanete ho jenom z mezipaměti.

Obecně platí, že ukládáte do mezipaměti informace, které se často nemění. Když vložíte informace do mezipaměti, uloží se do paměti na webovém serveru. Můžete určit, jak dlouho se má ukládat do mezipaměti, od sekund po dny. Po vypršení doby ukládání do mezipaměti jsou informace automaticky odebrány z mezipaměti.

> [!NOTE]
> Položky v mezipaměti je možné odebrat z jiných důvodů než po jejichž uplynutí vypršela. Webový server může například dočasně spustit nedostatek paměti a jedním ze způsobů, jak může uvolnit paměť, je vygenerování položek z mezipaměti. Jak vidíte, i když jste do mezipaměti umístili informace, musíte zkontrolovat, jestli je pořád tam, kde ji potřebujete.

Představte si, že váš web obsahuje stránku, která zobrazuje aktuální teplotu a předpověď počasí. K získání tohoto typu informací můžete odeslat žádost externí službě. Vzhledem k tomu, že se tyto informace nezmění (například během doby dvou hodin) a protože externí volání vyžadují dobu a šířku pásma, je dobrým kandidátem na ukládání do mezipaměti.

## <a name="adding-caching-to-a-page"></a>Přidání ukládání do mezipaměti na stránku

ASP.NET zahrnuje pomocnou nápovědu pro `WebCache`, která usnadňuje přidání ukládání do mezipaměti do vaší lokality a přidání dat do mezipaměti. V tomto postupu vytvoříte stránku, která ukládá do mezipaměti aktuální čas. Nejedná se o reálný příklad, protože aktuální čas je něco, co se často mění a které není složité vypočítat. Je však dobrým způsobem, jak znázornit ukládání do mezipaměti v akci.

1. Přidejte do webu novou stránku s názvem *webcache. cshtml* .
2. Přidejte následující kód a značku na stránku:

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    Když ukládáte data do mezipaměti, vložíte je do mezipaměti s použitím názvu, který je jedinečný v rámci webu. V takovém případě použijete položku mezipaměti s názvem `CachedTime`. Toto je `cacheItemKey` zobrazený v příkladu kódu.

    Kód nejprve přečte položku `CachedTime` cache. Pokud je vrácena hodnota (tj. Pokud položka mezipaměti není null), kód pouze nastaví hodnotu proměnné čas na data mezipaměti.

    Pokud však položka mezipaměti neexistuje (to znamená, že je null), kód nastaví hodnotu času, přidá ji do mezipaměti a nastaví hodnotu vypršení platnosti na jednu minutu. Po jedné minutě se položka mezipaměti zahodí. (Výchozí hodnota vypršení platnosti položky v mezipaměti je 20 minut.) Příkaz `WebCache.Set(cacheItemKey, time, 1, false)` ukazuje, jak přidat aktuální časovou hodnotu do mezipaměti a nastavit její vypršení platnosti na 1 minutu. Nastavením parametru *parametr slidingExpiration* na `false` znamená, že se čas vypršení platnosti neobnovuje při každém vyžádání. Platnost vyprší přesně 1 minutu poté, co byla původně přidána do mezipaměti. Pokud tuto hodnotu nastavíte na `true` doba vypršení platnosti 1 minuta se resetuje pokaždé, když se hodnota z mezipaměti vyžádá.

    Tento kód ilustruje vzor, který byste měli vždy použít při ukládání dat do mezipaměti. Předtím, než získáte něco z mezipaměti, vždy nejprve ověřte, zda `WebCache.Get` metoda vrátila hodnotu null. Pamatujte na to, že položka mezipaměti mohla vypršet nebo mohla být z nějakého důvodu odebrána, takže se žádné z těchto položek nikdy nezaručuje, že by se v mezipaměti shodovaly.
3. V prohlížeči spusťte *webcache. cshtml* . (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Při prvním požadavku na stránku se data nenacházejí v mezipaměti a kód musí do mezipaměti přidat časový údaj.

    ![cache-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. Obnovte *webcache. cshtml* v prohlížeči. Tentokrát jsou časová data v mezipaměti. Všimněte si, že se čas od posledního zobrazení stránky nezměnil.

    ![cache-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. Počkejte jednu minutu, než se mezipaměť vyprázdní, a pak aktualizujte stránku. Tato stránka znovu indikuje, že časová data se v mezipaměti nenašly a aktualizovaná doba se přidala do mezipaměti.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

- [Zobrazení dat v grafu](https://go.microsoft.com/fwlink/?LinkId=202895)
- [Referenční dokumentace rozhraní webcache API](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)
