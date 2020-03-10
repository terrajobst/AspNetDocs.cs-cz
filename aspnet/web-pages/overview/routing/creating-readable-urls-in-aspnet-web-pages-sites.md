---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: Vytváření čitelných adres URL na webech ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje směrování na webu ASP.NET Web Pages (Razor) a jak vám to umožňuje používat adresy URL, které jsou čitelnější a lepší pro SEO. Co budete...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628392"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>Vytváření čitelných adres URL na webech ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje směrování na webu ASP.NET Web Pages (Razor) a jak vám to umožňuje používat adresy URL, které jsou čitelnější a lepší pro SEO.
> 
> Naučíte se:
> 
> - Jak ASP.NET využívá směrování, abyste mohli používat čitelnější a prohledávatelné adresy URL.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

## <a name="about-routing"></a>O směrování

Adresy URL stránek na webu mohou mít dopad na to, jak dobře web funguje. Adresa URL, která je &quot;uživatelsky přívětivá&quot; může usnadnit používání webu uživateli. Může také pomáhat s optimalizací vyhledávání na webu (SEO). ASP.NET weby zahrnují možnost používat popisné adresy URL automaticky.

ASP.NET umožňuje vytvářet smysluplné adresy URL, které popisují akce uživatelů místo pouhého nasměrování na soubor na serveru. Vezměte v úvahu tyto adresy URL fiktivního blogu:

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

Porovnejte tyto adresy URL s těmito adresami:

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

V první dvojici by uživatel musel mít jistotu, že se blog zobrazuje pomocí stránky *blog. cshtml* , a pak by musel sestavit řetězec dotazu, který získá správnou kategorii nebo rozsah kalendářních dat. Druhá sada příkladů je mnohem snazší pochopit a vytvořit.

Adresy URL pro první příklad také odkazují přímo na konkrétní soubor (*blog. cshtml*). Pokud z nějakého důvodu byl blog přesunut do jiné složky na serveru nebo pokud byl blog přepsaný na jinou stránku, odkazy by byly nesprávné. Druhá sada adres URL neukazuje na konkrétní stránku, takže i v případě změny nebo implementace blogu budou adresy URL stále platné.

Na webových stránkách ASP.NET můžete vytvořit adresy URL příjemnější, jako jsou ty ve výše uvedených příkladech, protože ASP.NET používá *Směrování*. Směrování vytvoří logické mapování z adresy URL na stránku (nebo stránky), která může splnit požadavek. Vzhledem k tomu, že mapování je logické (nefyzické, pro určitý soubor), směrování poskytuje skvělou flexibilitu při definování adres URL pro váš web.

## <a name="how-routing-works"></a>Jak funguje směrování

Když ASP.NET zpracuje požadavek, přečte adresu URL, která určí, jak se má směrovat. ASP.NET se snaží porovnat jednotlivé segmenty adresy URL s soubory na disku, a to směrem zleva doprava. Pokud se vyskytne shoda, vše zbývající na adrese URL se předává stránce jako *informace o cestě*.

Představte si, že někdo vytvoří žádost pomocí této adresy URL:

`http://www.contoso.com/a/b/c`

Hledání bude vypadat takto:

1. Existuje soubor s cestou a názvem */a/b/c.cshtml*? Pokud ano, spusťte tuto stránku a nepředá do ní žádné informace. V opačném případě...
2. Existuje soubor s cestou a názvem */a/b.cshtml*? Pokud ano, spusťte tuto stránku a předejte jí hodnotu `c`. V opačném případě...
3. Existuje soubor s cestou a názvem */a.cshtml*? Pokud ano, spusťte tuto stránku a předejte jí hodnotu `b/c`.

Pokud hledání nenalezlo přesné shody souborů *. cshtml* v zadaných složkách, ASP.NET pokračuje v hledání těchto souborů:

1. */a/b/c/default.cshtml* (žádné informace o cestě).
2. */a/b/c/index.cshtml* (žádné informace o cestě).

> [!NOTE]
> Aby bylo jasné, požadavky na konkrétní stránky (tj. požadavky, které obsahují příponu názvu souboru *. cshtml* ) fungují stejně jako ty, které byste očekávali. Žádost, jako je `http://www.contoso.com/a/b.cshtml`, spustí stránku *b. cshtml* pouze přesně.

V rámci stránky můžete získat informace o cestě prostřednictvím vlastnosti `UrlData` stránky, což je slovník. Představte si, že máte soubor s názvem *ViewCustomers. cshtml* a váš web získá tuto žádost:

`http://mysite.com/myWebSite/ViewCustomers/1000`

Jak je popsáno v předchozích pravidlech, požadavek přejde na vaši stránku. Uvnitř stránky můžete použít kód podobný následujícímu k získání a zobrazení informací o cestě (v tomto případě hodnota &quot;1000&quot;):

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> Vzhledem k tomu, že směrování nezahrnuje úplné názvy souborů, může dojít k nejednoznačnosti, pokud máte stránky se stejným názvem, ale s různými příponami názvu souboru (například *MyPage. cshtml* a *MyPage. html*). Aby se zabránilo problémům se směrováním, je vhodné zajistit, aby ve vaší lokalitě nebyly stránky, jejichž názvy se liší pouze v jejich příponách.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[WebMatrix – adresy URL, UrlData a směrování pro SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO). Tento záznam blogu pomocí Jan slaného záznamu vám poskytne další podrobnosti o tom, jak funguje směrování na webových stránkách ASP.NET.
