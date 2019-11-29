---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
title: Zobrazení více záznamů na řádku pomocí ovládacího prvku DataList (C#) | Microsoft Docs
author: rick-anderson
description: V tomto krátkém kurzu budeme prozkoumat, jak přizpůsobit rozložení prvku DataList pomocí vlastností RepeatColumns a RepeatDirection.
ms.author: riande
ms.date: 09/13/2006
ms.assetid: cf5acaf5-d4f6-4957-badc-b89956b285f3
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3280a7b5f28207d3e640a6480f47869ce19692bc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74638594"
---
# <a name="showing-multiple-records-per-row-with-the-datalist-control-c"></a>Zobrazení více záznamů na řádku ovládacím prvkem DataList (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_CS.exe) nebo [Stáhnout PDF](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/datatutorial31cs1.pdf)

> V tomto krátkém kurzu budeme prozkoumat, jak přizpůsobit rozložení prvku DataList pomocí vlastností RepeatColumns a RepeatDirection.

## <a name="introduction"></a>Úvod

Příklady DataList, které jsme viděli v minulých dvou kurzech, vykreslily každý záznam z jeho zdroje dat jako řádek ve formátu HTML s jedním sloupcem `<table>`. I když toto je výchozí chování prvku DataList, je velmi snadné přizpůsobit zobrazení prvku DataList tak, že položky zdroje dat jsou rozloženy v tabulce více sloupců tabulky s více řádky. Kromě toho je možné mít všechny položky zdroje dat zobrazené v rámci více sloupců DataList na jednom řádku.

Rozložení prvku DataList s můžeme přizpůsobit pomocí jeho `RepeatColumns` a `RepeatDirection` vlastností, které v uvedeném pořadí označují, kolik sloupců je vykresleno a zda jsou tyto položky rozloženy svisle nebo vodorovně. Obrázek 1 například ukazuje prvek DataList, který zobrazí informace o produktu v tabulce se třemi sloupci.

[![DataList zobrazuje tři produkty na řádek](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image1.png)

**Obrázek 1**: DataList zobrazuje tři produkty na řádek ([kliknutím zobrazíte obrázek v plné velikosti).](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image3.png)

Zobrazením více položek zdroje dat na řádek může prvek DataList efektivněji využít horizontální prostor na obrazovce. V tomto krátkém kurzu prozkoumáme tyto dvě vlastnosti DataList.

## <a name="step-1-displaying-product-information-in-a-datalist"></a>Krok 1: zobrazení informací o produktu v prvku DataList

Než prověříme vlastnosti `RepeatColumns` a `RepeatDirection`, je nejdřív možné vytvořit DataList na naší stránce, kde se zobrazí informace o produktu pomocí standardního tabulkového rozložení s jedním sloupcem. V tomto příkladu se zobrazí název produktu, kategorie a cena s použitím následujícího kódu:

[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample1.html)]

Zjistili jsme, jak navazovat data na DataList v předchozích příkladech, takže se tyto kroky rychle přesouvají. Začněte otevřením stránky `RepeatColumnAndDirection.aspx` ve složce `DataListRepeaterBasics` a přetažením prvku DataList z panelu nástrojů do návrháře. Z inteligentní značky DataList s Přihlaste se k vytvoření nového prvku ObjectDataSource a nakonfigurujte ho tak, aby načetl data z metody `ProductsBLL` třídy s `GetProducts`, a to výběrem možnosti (žádné) z Průvodce VLOŽENÍm, aktualizací a ODSTRANĚNÍm.

Po vytvoření a svázání nového prvku ObjectDataSource s prvkem DataList bude aplikace Visual Studio automaticky vytvářet `ItemTemplate`, které zobrazí název a hodnotu pro každé pole dat produktu. Upravte `ItemTemplate` buď přímo prostřednictvím deklarativní značky, nebo z možnosti Upravit šablony v inteligentní značce DataList s tak, aby používala značky uvedené výše, nahraďte *název produktu*, *název kategorie*a *cenový* text pomocí ovládacích prvků popisek, které používají příslušnou syntaxi datové vazby k přiřazení hodnot jejich `Text`m vlastnostem. Po aktualizaci `ItemTemplate`by vaše deklarativní označení stránky mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample2.aspx)]

Všimněte si, že v syntaxi `Eval` DataBinding pro `UnitPrice`jsem zahrnul specifikátor formátu, což naformátuje vrácenou hodnotu jako měnu `Eval("UnitPrice", "{0:C}").`

Chvíli počkejte, než navštívíte stránku v prohlížeči. Jak je znázorněno na obrázku 2, DataList se vykresluje jako tabulka s jedním sloupcem a více řádky produktů.

[Ve výchozím nastavení ![DataList vykreslí jako tabulku s jedním sloupcem, více řádky.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image4.png)

**Obrázek 2**: ve výchozím nastavení se DataList vykresluje jako tabulka s jedním sloupcem a více řádky ([kliknutím zobrazíte obrázek v plné velikosti).](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image6.png)

## <a name="step-2-changing-the-datalist-s-layout-direction"></a>Krok 2: Změna směru rozložení DataList s

I když je výchozím chováním prvku DataList rozvrhnout své položky svisle v tabulce s více řádky v jednom sloupci, toto chování lze snadno změnit prostřednictvím [vlastnosti`RepeatDirection`](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)prvků DataList. Vlastnost `RepeatDirection` může přijmout jednu ze dvou možných hodnot: `Horizontal` nebo `Vertical` (výchozí).

Změnou vlastnosti `RepeatDirection` z `Vertical` na `Horizontal`, DataList vykreslí své záznamy na jednom řádku a vytvoří jeden sloupec na položku zdroje dat. Pro ilustraci tohoto efektu klikněte na prvek DataList v návrháři a poté z okno Vlastnosti změňte vlastnost `RepeatDirection` z `Vertical` na `Horizontal`. V důsledku toho Návrhář upraví rozložení prvku DataList s a vytvoří rozhraní s více sloupci (viz obrázek 3) s jedním řádkem.

[![vlastnost RepeatDirection Určuje způsob, jakým jsou rozloženy položky DataList s.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image7.png)

**Obrázek 3**: vlastnost `RepeatDirection` určuje způsob, jakým jsou rozloženy položky DataList s ([kliknutím zobrazíte obrázek v plné velikosti).](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image9.png)

Při zobrazování malých objemů dat může být jedním řádkem tabulka s více sloupci ideální způsob, jak maximalizovat obrazovku. U větších objemů dat však bude jeden řádek vyžadovat mnoho sloupců, které budou tyto položky vložit do pravé části obrazovky. Obrázek 4 znázorňuje produkty při vykreslování v prvku DataList s jedním řádkem. Vzhledem k tomu, že existuje mnoho produktů (více než 80), se uživatel bude muset posunout doprava a zobrazit informace o jednotlivých produktech.

[![u dostatečně velkých zdrojů dat bude jeden sloupec DataList vyžadovat horizontální posouvání.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image10.png)

**Obrázek 4**: u dostatečně velkých zdrojů dat bude pro jeden sloupec DataList nutné horizontální posouvání ([kliknutím zobrazíte obrázek v plné velikosti).](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image12.png)

## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>Krok 3: zobrazení dat ve více sloupcích tabulky s více řádky

Pro vytvoření víceřádkového prvku DataList pro více řádků je potřeba nastavit [vlastnost`RepeatColumns`](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx) na počet zobrazených sloupců. Ve výchozím nastavení je vlastnost `RepeatColumns` nastavena na hodnotu 0, což způsobí, že prvek DataList zobrazí všechny položky v jednom řádku nebo sloupci (v závislosti na hodnotě vlastnosti `RepeatDirection`).

V našem příkladu si můžeme zobrazit tři produkty na řádek tabulky. Proto nastavte vlastnost `RepeatColumns` na hodnotu 3. Po provedení této změny si chvíli počkejte, než se výsledky zobrazí v prohlížeči. Jak ukazuje obrázek 5, produkty jsou teď uvedené v tabulce se třemi sloupci a více řádky.

[na řádek se zobrazují tři produkty ![.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image13.png)

**Obrázek 5**: pro jednotlivé řádky se zobrazují tři produkty ([kliknutím zobrazíte obrázek v plné velikosti).](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image15.png)

Vlastnost `RepeatDirection` ovlivňuje způsob, jakým jsou položky v prvku DataList rozloženy. Obrázek 5 zobrazuje výsledky s vlastností `RepeatDirection` nastavenou na hodnotu `Horizontal`. Všimněte si, že první tři produkty Chai, změn a anýzový sirup jsou uvedené zleva doprava, shora dolů. Další tři produkty (počínaje Antonem s názvem "3. Cajun)" se zobrazí na řádku pod první tři. Změna vlastnosti `RepeatDirection` zpět na `Vertical`, ale rozloží tyto produkty shora dolů, zleva doprava, jak ukazuje obrázek 6.

[![zde jsou produkty rozloženy svisle.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image16.png)

**Obrázek 6**: v tomto případě jsou produkty rozloženy svisle ([kliknutím zobrazíte obrázek v plné velikosti](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image18.png)).

Počet řádků zobrazených ve výsledné tabulce závisí na počtu celkových záznamů svázaných s ovládacím prvkům DataList. Přesně to má strop celkového počtu položek zdroje dat dělený hodnotou vlastnosti `RepeatColumns`. Vzhledem k tomu, že `Products` tabulka v současnosti obsahuje 84 produktů, které jsou v tuto chvíli dělitelné 3, je to 28 řádků. Pokud počet položek ve zdroji dat a hodnotě vlastnosti `RepeatColumns` není rozdělitelný, bude mít poslední řádek nebo sloupec prázdné buňky. Pokud je `RepeatDirection` nastaveno na `Vertical`, bude mít poslední sloupec prázdné buňky. Pokud je `RepeatDirection` `Horizontal`, bude mít poslední řádek prázdné buňky.

## <a name="summary"></a>Přehled

Prvek DataList ve výchozím nastavení zobrazuje seznam položek v tabulce s více řádky, což napodobuje rozložení prvku GridView s jednou vlastností TemplateField. I když je toto výchozí rozložení přijatelné, můžeme maximalizovat vzhled obrazovky zobrazením několika položek zdrojů dat na jeden řádek. K tomu je potřeba jednoduše nastavit vlastnost `RepeatColumns` DataList na počet sloupců, které se mají zobrazit na řádek. Kromě toho se dá vlastnost `RepeatDirection` DataList použít k určení, jestli se má obsah tabulky s více sloupci a více řádky nacházet vodorovně od zleva doprava, shora dolů nebo vertikálně od shora dolů, zleva doprava.

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor potenciálních zákazníků pro tento kurz byl Jan Suru. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
> [Další](nested-data-web-controls-cs.md)
