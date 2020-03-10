---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 'Část 10: konečné aktualizace navigace a navrhování webů, závěr | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 10 pokrývá konečné aktualizace navigace a S...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539366"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>10. část: Závěrečné aktualizace návrhu navigace a webu, závěr

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 10 pokrývá konečné aktualizace navigace a návrhu lokality, závěr.

Dokončili jsme všechny hlavní funkce pro náš web, ale pořád máme k dispozici některé funkce, které by bylo možné přidat do navigace na webu, na domovské stránce a na stránce pro procházení ve Storu.

## <a name="creating-the-shopping-cart-summary-partial-view"></a>Vytvoření částečného zobrazení souhrnu nákupního košíku

Chceme vystavit počet položek v nákupním košíku v rámci celé lokality.

![](mvc-music-store-part-10/_static/image1.png)

To lze snadno implementovat vytvořením částečného zobrazení, které je přidáno do našeho webu. Master.

Jak je uvedeno výše, kontroler ShoppingCart zahrnuje metodu CartSummary akce, která vrací částečné zobrazení:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

Chcete-li vytvořit částečné zobrazení CartSummary, klikněte pravým tlačítkem myši na složku views/ShoppingCart a vyberte možnost přidat zobrazení. Pojmenujte zobrazení CartSummary a zaškrtněte políčko "vytvořit částečné zobrazení", jak je znázorněno níže.

![](mvc-music-store-part-10/_static/image2.png)

Částečné zobrazení CartSummary je ve skutečnosti jednoduché – jedná se pouze o odkaz na zobrazení indexu ShoppingCart, které zobrazuje počet položek na vozíku. Úplný kód pro CartSummary. cshtml je následující:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

Částečné zobrazení na jakékoli stránce v lokalitě, včetně hlavního serveru, můžeme přidat pomocí metody HTML. RenderAction. RenderAction vyžaduje, abychom určili název akce ("CartSummary") a název kontroleru ("ShoppingCart"), jak je uvedeno níže.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

Před přidáním tohoto webu do rozložení lokality vytvoříme také nabídku Žánr, abychom mohli najednou vytvořit všechny aktualizace webu. Master.

## <a name="creating-the-genre-menu-partial-view"></a>Vytvoření částečného zobrazení nabídky žánru

Díky přidání nabídky žánru, která obsahuje všechny žánry, které jsou k dispozici v našem obchodě, můžeme pro naše uživatele mnohem usnadnit navigaci v obchodě.

![](mvc-music-store-part-10/_static/image3.png)

Budeme postupovat podle stejných kroků také při vytváření GenreMenu částečného zobrazení a pak je můžeme přidat do hlavního serveru. Nejprve přidejte následující akci GenreMenu Controller do StoreController:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

Tato akce vrátí seznam žánrů, které se zobrazí v částečném zobrazení, které vytvoříme v dalším kroku.

*Poznámka: Přidali jsme do této akce kontroleru atribut [ChildActionOnly], který indikuje, že tuto akci chcete použít jenom z částečného zobrazení. Tento atribut zabrání spuštění akce kontroleru procházením na/Store/GenreMenu. To se nevyžaduje u částečných zobrazení, ale je to dobrý postup, protože chceme zajistit, aby se naše akce kontroleru používaly jako v úmyslu. Vracíme také PartialView namísto zobrazení, což umožňuje, aby modul zobrazení věděl, že by neměl používat rozložení pro toto zobrazení, protože je zahrnutý v jiných zobrazeních.*

Klikněte pravým tlačítkem na akci GenreMenu Controller a vytvořte částečné zobrazení s názvem GenreMenu se silným typem pomocí třídy zobrazení žánru, jak je znázorněno níže.

![](mvc-music-store-part-10/_static/image4.png)

Aktualizujte kód zobrazení pro částečné zobrazení GenreMenu pro zobrazení položek pomocí neuspořádaného seznamu následujícím způsobem.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>Aktualizace rozložení lokality pro zobrazení našich částečných zobrazení

Naše částečná zobrazení můžeme přidat do rozložení webu (/Views/Shared/\_layout. cshtml) voláním HTML. RenderAction (). Přidáme je do obou i do některých dalších značek k jejich zobrazení, jak je znázorněno níže:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

Teď, když aplikaci spustíme, uvidíme v levé navigační oblasti a v horní části košíku.

## <a name="update-to-the-store-browse-page"></a>Aktualizace stránky pro procházení úložiště

Stránka pro procházení úložiště je funkční, ale nevypadá velmi dobrá. Stránku můžete aktualizovat tak, aby zobrazovala alba ve lepším rozložení, a to tak, že aktualizujete kód zobrazení (najdete v/Views/Store/Browse.cshtml) následujícím způsobem:

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

V tomto případě používáme adresu URL. Action namísto HTML. ActionLink, aby bylo možné pro odkaz použít speciální formátování, aby se zahrnula kresba alba.

*Poznámka: pro tato alba zobrazujeme obecné pokrytí alba. Tyto informace jsou uloženy v databázi a lze je upravovat prostřednictvím Správce úložiště. Vítá vás přidání vlastní kresby.*

Když teď procházíme na Žánr, uvidíme alba zobrazená v mřížce s kresbou alba.

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>Aktualizace domovské stránky, aby se zobrazila nejlepší prodejní alba

Chceme vymezit naše nejlepší prodejní alba na domovské stránce a zvýšit tak prodej. Provedeme některé aktualizace našich HomeControllerů, abychom to zpracovávala a mohli přidat i další grafiku.

Nejprve přidáme vlastnost navigace do naší třídy alba, aby EntityFramework ví, že jsou přidružená. Poslední pár řádků naší třídy **alba** by teď měl vypadat takto:

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*Poznámka: Tato akce vyžaduje přidání příkazu Using, který se má přenést do oboru názvů System. Collections. Generic.*

Nejprve přidáme pole storeDB a MvcMusicStore. Models pomocí příkazů, jako u našich dalších řadičů. Dále do HomeController přidáme následující metodu, která bude dotazovat se na naši databázi, aby se vyhledaly nejlepší prodejní alba podle OrderDetails.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

Jedná se o soukromou metodu, protože ji nechceme zpřístupnit jako akci kontroleru. Do HomeControlleru nabízíme pro jednoduchost, ale doporučujeme, abyste obchodní logiku přesunuli na samostatné třídy služby podle potřeby.

V takovém případě můžeme aktualizovat akci kontroleru indexů a dotazovat se na prvních 5 prodejních alb a vrátit je do zobrazení.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

Úplný kód pro aktualizovaný HomeController je znázorněný níže.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

Nakonec budeme muset aktualizovat naše zobrazení domovského indexu tak, aby bylo možné zobrazit seznam alb aktualizací typu modelu a přidáním seznamu alb do dolní části. Pomůžeme vám také přidat záhlaví a oddíl propagace na stránku.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

Teď, když aplikaci spustíme, uvidíme naši aktualizovanou domovskou stránku s nejlepšími prodejními alba a naší propagační zprávou.

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>Závěr

Zjistili jsme, že ASP.NET MVC usnadňuje vytváření sofistikovaných webů s přístupem k databázi, členstvím, AJAX atd. poměrně rychle. Snad v tomto kurzu jste získali nástroje, které potřebujete, abyste mohli začít vytvářet vlastní aplikace ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-9.md)
