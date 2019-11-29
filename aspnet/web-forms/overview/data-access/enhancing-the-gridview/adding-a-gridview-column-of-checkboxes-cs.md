---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
title: Přidání sloupce zaškrtávacích políček do prvku GridViewC#() | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na postup přidání sloupce zaškrtávacích políček do ovládacího prvku GridView, který uživateli poskytne intuitivní způsob výběru více řádků G...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: f63a9443-2db0-4f80-8246-840d3e86c2a3
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: b9d1ed50e8d88202c3286b4cd0e9ebf111dfbe21
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592484"
---
# <a name="adding-a-gridview-column-of-checkboxes-c"></a>Přidání sloupce zaškrtávacích políček do ovládacího prvku GridView (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_CS.exe) nebo [Stáhnout PDF](adding-a-gridview-column-of-checkboxes-cs/_static/datatutorial52cs1.pdf)

> V tomto kurzu se podíváme na postup přidání sloupce zaškrtávacích políček do ovládacího prvku GridView, který uživateli poskytne intuitivní způsob výběru více řádků prvku GridView.

## <a name="introduction"></a>Úvod

V předchozím kurzu jsme prozkoumali, jak do prvku GridView přidat sloupec přepínacích tlačítek pro účely výběru konkrétního záznamu. Sloupec přepínacích tlačítek je vhodné uživatelské rozhraní, když je uživatel omezen na výběr maximálně jedné položky z mřížky. Občas ale můžeme chtít uživateli dovolit vybrat libovolný počet položek z mřížky. Webové e-mailové klienty, například obvykle zobrazují seznam zpráv se sloupcem zaškrtávacích políček. Uživatel může vybrat libovolný počet zpráv a pak provést některé akce, například přesunutí e-mailů do jiné složky nebo jejich odstranění.

V tomto kurzu se dozvíte, jak přidat sloupec zaškrtávacích políček a jak určit, která zaškrtávací políčka byla kontrolována při postbacku. Konkrétně sestavíme příklad, který bude úzce napodobovat webové uživatelské rozhraní e-mailového klienta. Náš příklad obsahuje stránkované zobrazení obsahující seznam produktů v tabulce databáze `Products` a zaškrtávací políčko v každém řádku (viz obrázek 1). Tlačítko Odstranit vybrané produkty po kliknutí odstraní vybrané produkty.

[![každý řádek produktu obsahuje zaškrtávací políčko](adding-a-gridview-column-of-checkboxes-cs/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image1.png)

**Obrázek 1**: každý řádek produktu obsahuje zaškrtávací políčko ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-checkboxes-cs/_static/image2.png)).

## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>Krok 1: Přidání stránkovaného prvku GridView, který obsahuje informace o produktu

Předtím, než se obáváme o přidání sloupce zaškrtávacích políček, se nejdříve zaměřte na výpis produktů v prvku GridView, který podporuje stránkování. Začněte otevřením stránky `CheckBoxField.aspx` ve složce `EnhancedGridView` a přetažením prvku GridView z panelu nástrojů do návrháře, nastavením jeho `ID` na `Products`. Dále můžete zvolit svázání prvku GridView s novým prvkem ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby používal třídu `ProductsBLL`, zavoláním metody `GetProducts()`, která vrátí data. Vzhledem k tomu, že tento prvek GridView bude jen pro čtení, nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné).

[![vytvořit nový prvek ObjectDataSource s názvem ProductsDataSource](adding-a-gridview-column-of-checkboxes-cs/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image3.png)

**Obrázek 2**: vytvoření nového prvku ObjectDataSource s názvem `ProductsDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-checkboxes-cs/_static/image4.png))

[![nakonfigurovat prvek ObjectDataSource pro načtení dat pomocí metody GetProducts ()](adding-a-gridview-column-of-checkboxes-cs/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image5.png)

**Obrázek 3**: Konfigurace prvku ObjectDataSource pro načtení dat pomocí metody `GetProducts()` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-checkboxes-cs/_static/image6.png))

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](adding-a-gridview-column-of-checkboxes-cs/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image7.png)

**Obrázek 4**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti).](adding-a-gridview-column-of-checkboxes-cs/_static/image8.png)

Po dokončení Průvodce konfigurací zdroje dat vytvoří Visual Studio pro datová pole související s produktem automaticky ovládací prvky pro vytváření vázaných dat a CheckBoxColumn. Stejně jako v předchozím kurzu odeberte všechny kromě `ProductName`, `CategoryName`a `UnitPrice` BoundFields a změňte `HeaderText` vlastnosti na produkt, kategorii a cenu. Nakonfigurujte `UnitPrice` vlastnost BoundField, aby se jeho hodnota formátovala jako měna. Také nakonfigurujte prvek GridView tak, aby podporoval stránkování zaškrtnutím políčka Povolit stránkování z inteligentní značky.

Umožňuje také přidat uživatelské rozhraní pro odstranění vybraných produktů. Přidejte webové ovládací prvky tlačítko pod prvek GridView, nastavením jeho `ID` na `DeleteSelectedProducts` a jeho vlastnost `Text` k odstranění vybraných produktů. Místo toho, abyste z databáze skutečně odstranili produkty, se v tomto příkladu zobrazí jen zpráva s informacemi o tom, které produkty byly odstraněny. Chcete-li to přizpůsobit, přidejte ovládací prvek popisek webu pod tlačítko. Nastavte jeho ID na `DeleteResults`, vymažte jeho vlastnost `Text` a nastavte jeho vlastnosti `Visible` a `EnableViewState` na `false`.

Po provedení těchto změn by deklarativní označení GridView, ObjectDataSource, Button a Label s popisky měly vypadat podobně jako následující:

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample1.aspx)]

Chvíli si zobrazte stránku v prohlížeči (viz obrázek 5). V tomto okamžiku byste měli vidět název, kategorii a cenu prvních deseti produktů.

[![je uveden název, kategorie a cena za prvních deset produktů.](adding-a-gridview-column-of-checkboxes-cs/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image9.png)

**Obrázek 5**: v seznamu je uveden název, kategorie a cena prvních deseti produktů ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-checkboxes-cs/_static/image10.png)).

## <a name="step-2-adding-a-column-of-checkboxes"></a>Krok 2: Přidání sloupce zaškrtávacích políček

Vzhledem k tomu, že ASP.NET 2,0 obsahuje třídě CheckBoxField podporována, může se stát, že se dá použít k přidání sloupce zaškrtávacích políček do prvku GridView. Bohužel, to znamená, že třídě CheckBoxField podporována je navržen pro práci s logickým datovým polem. To znamená, že aby bylo možné použít třídě CheckBoxField podporována, je nutné zadat podkladové datové pole, jehož hodnota je kontrolována, aby bylo zjištěno, zda je zaškrtnuté políčko vykresleno. Třídě CheckBoxField podporována nemůžeme použít pro pouhé zahrnutí sloupce nezaškrtnutých políček.

Místo toho je nutné přidat TemplateField a přidat webový ovládací prvek CheckBox do jeho `ItemTemplate`. Pokračujte a přidejte TemplateField do `Products` GridView a nastavte ho jako první (úplně vlevo) pole. Z inteligentní značky GridView s klikněte na odkaz Upravit šablony a přetáhněte webový ovládací prvek CheckBox ze sady nástrojů do `ItemTemplate`. Nastavte tuto vlastnost `ID` vlastností na `ProductSelector`.

[![přidat webový ovládací prvek CheckBox s názvem ProductSelector do vlastnosti TemplateField s ItemTemplate](adding-a-gridview-column-of-checkboxes-cs/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image11.png)

**Obrázek 6**: Přidejte webový ovládací prvek CheckBox s názvem `ProductSelector` do `ItemTemplate` TemplateField s ([kliknutím zobrazíte obrázek v plné velikosti).](adding-a-gridview-column-of-checkboxes-cs/_static/image12.png)

Po přidání webového ovládacího prvku TemplateField a CheckBox teď každý řádek obsahuje zaškrtávací políčko. Obrázek 7 ukazuje tuto stránku při zobrazení v prohlížeči po přidání pole TemplateField a CheckBox.

[![každý produktový řádek teď obsahuje zaškrtávací políčko.](adding-a-gridview-column-of-checkboxes-cs/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image13.png)

**Obrázek 7**: každý produktový řádek teď obsahuje zaškrtávací políčko ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-checkboxes-cs/_static/image14.png)).

## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>Krok 3: určení, která zaškrtávací políčka byla kontrolována při postbacku

V tuto chvíli máme sloupec se zaškrtávacími políčky, ale neexistuje žádný způsob, jak určit, která zaškrtávací políčka byla zkontrolována při zpětném odeslání. Když se klikne na tlačítko Odstranit vybrané produkty, potřebujeme, abyste věděli, jaké zaškrtávací políčko bylo zkontrolováno, aby bylo možné tyto produkty odstranit.

Vlastnost GridView s [`Rows`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) poskytuje přístup k datovým řádkům v prvku GridView. Můžeme iterovat prostřednictvím těchto řádků, programově získat přístup k ovládacímu prvku CheckBox a potom pomocí jeho vlastnosti `Checked` zjistit, zda bylo políčko zaškrtnuto.

Vytvořte obslužnou rutinu události pro webové ovládací prvky tlačítko `DeleteSelectedProducts` `Click` událost a přidejte následující kód:

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample2.cs)]

Vlastnost `Rows` vrací kolekci instancí `GridViewRow`, které strukturu datové řádky GridView s. Zde `foreach` cyklus vyčíslí tuto kolekci. Pro každý objekt `GridViewRow` je zaškrtávací políčko řádky s programově dostupné pomocí `row.FindControl("controlID")`. Pokud je zaškrtávací políčko zaškrtnuto, bude z kolekce `DataKeys` načtena odpovídající hodnota `ProductID`. V tomto cvičení jednoduše zobrazíme informativní zprávu v popisku `DeleteResults`, i když v pracovní aplikaci zavoláme metodu `DeleteProduct(productID)` `ProductsBLL` třídy s.

Po přidání této obslužné rutiny události se kliknutím na tlačítko Odstranit vybrané produkty teď zobrazí `ProductID` s vybraných produktů.

[![, když se klikne na tlačítko Odstranit vybrané produkty, zobrazí se vybrané produkty ProductID.](adding-a-gridview-column-of-checkboxes-cs/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image15.png)

**Obrázek 8**: když se na tlačítko Odstranit vybrané produkty klikne na vybrané produkty `ProductID` s, zobrazí se seznam ([kliknutím zobrazíte obrázek v plné velikosti).](adding-a-gridview-column-of-checkboxes-cs/_static/image16.png)

## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>Krok 4: přidání všech tlačítek a zrušení kontroly všech tlačítek

Pokud chce uživatel odstranit všechny produkty na aktuální stránce, musí zaškrtnout každé deset zaškrtávacích políček. Tento proces můžeme přispět tak, že přidáte tlačítko pro kontrolu všech, které po kliknutí vybere všechna zaškrtávací políčka v mřížce. Tlačítko zrušit kontrolu všech by bylo stejně užitečné.

Přidejte dvě webové ovládací prvky tlačítka na stránku a umístěte je nad prvek GridView. Nastavte první `ID` s pro `CheckAll` a jeho vlastnost `Text` pro kontrolu všech; nastavte druhý `ID` s `UncheckAll` a jeho vlastnost `Text` na zrušit kontrolu všech.

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample3.aspx)]

Dále vytvořte metodu v třídě Code-on s názvem `ToggleCheckState(checkState)`, která při vyvolání vytvoří výčet `Products` kolekce `Rows` GridView. a nastaví každou vlastnost CheckBox s `Checked` na hodnotu předaného parametru *checkState* .

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample4.cs)]

Dále vytvořte obslužné rutiny událostí `Click` pro tlačítka `CheckAll` a `UncheckAll`. V obslužné rutině události `CheckAll` s, jednoduše zavolejte `ToggleCheckState(true)`; v `UncheckAll`volejte `ToggleCheckState(false)`.

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample5.cs)]

V tomto kódu kliknutím na tlačítko zkontrolovat vše způsobí postback a zkontroluje všechna zaškrtávací políčka v prvku GridView. Podobně klikněte na zrušit zaškrtnutí všech políček zrušit výběr. Obrázek 9 zobrazí obrazovku po zaškrtnutí tlačítka pro kontrolu všech.

[![kliknutí na tlačítko pro kontrolu všech výběrová zaškrtávací políčka](adding-a-gridview-column-of-checkboxes-cs/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image17.png)

**Obrázek 9**: kliknutím na tlačítko pro kontrolu všech vyberete zaškrtávací políčka ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-checkboxes-cs/_static/image18.png)).

> [!NOTE]
> Při zobrazování sloupce zaškrtávacích políček je jedním z přístupů k výběru nebo odvolbě všech zaškrtávacích políček zaškrtávací políčko v řádku záhlaví. Aktuální kontrolu a zrušit kontrolu všech implementací navíc vyžaduje postback. Zaškrtávací políčka lze zaškrtnout nebo zrušit bez zaškrtnutí, ale výhradně prostřednictvím skriptu na straně klienta, čímž zajistíte snappier uživatelské prostředí. Chcete-li se podívat na zaškrtávací políčko pro kontrolu všech a zrušit zaškrtnutí všech podrobností, společně s diskusí o používání technik na straně klienta, zaškrtněte políčko kontrolovat [všechna políčka v prvku GridView pomocí skriptu na straně klienta a zaškrtnutím políčka zaškrtnout vše](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx).

## <a name="summary"></a>Přehled

V případech, kdy potřebujete umožnit uživatelům zvolit libovolný počet řádků z prvku GridView, než budete pokračovat, přidání sloupce zaškrtávacích políček je jedna možnost. Jak jsme viděli v tomto kurzu, včetně sloupce zaškrtávacích políček v prvku GridView, zahrnuje přidání pole TemplateField s webovým ovládacím prvkem CheckBox. Pomocí webového ovládacího prvku (proti vložení značek přímo do šablony, jako jsme to dělali v předchozím kurzu) ASP.NET automaticky pamatuje, jaké zaškrtávací políčko byly a nebyly zkontrolovány v rámci zpětného odeslání. K určení, zda je dané zaškrtávací políčko zaškrtnuto, nebo ke změně stavu zaškrtnutí, můžeme také programově přistupovat k zaškrtávacím políčkům v kódu.

Tento kurz a poslední z nich se prohlédlo přidáním sloupce selektor řádku do prvku GridView. V našem dalším kurzu budeme posuzovat, jak, v rámci práce, můžeme do prvku GridView přidat možnosti vkládání.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](adding-a-gridview-column-of-radio-buttons-cs.md)
> [Další](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
