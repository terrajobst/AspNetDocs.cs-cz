---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: Programové nastavení hodnot parametru ObjectDataSource (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na přidání metody do našeho DAL a knihoven BLL, které přijmou jeden vstupní parametr a vrátí data. V příkladu se nastaví tento parametr...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: f1dd50f46528e8dd51f85e503604d3f0dbc21ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577054"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a>Programové nastavení hodnot parametru ObjectDataSource (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe) nebo [Stáhnout PDF](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)

> V tomto kurzu se podíváme na přidání metody do našeho DAL a knihoven BLL, které přijmou jeden vstupní parametr a vrátí data. V příkladu se tento parametr nastaví programově.

## <a name="introduction"></a>Úvod

Jak jsme viděli v [předchozím kurzu](declarative-parameters-vb.md), je k dispozici řada možností pro deklarativní předání hodnot parametrů metodám ovládacího prvku ObjectDataSource. Pokud hodnota parametru je pevně zakódována, přichází z webového ovládacího prvku na stránce nebo je v jakémkoli jiném zdroji, který je čitelný zdrojem dat `Parameter` objekt, například tato hodnota může být vázána na vstupní parametr bez psaní řádku kódu.

Může se ale stát, že když hodnota parametru pochází z nějakého zdroje, který už není na jednom z vestavěných zdrojů dat `Parameter` objekty. Pokud naše lokalita podporuje uživatelské účty, můžete nastavit parametr na základě aktuálně přihlášeného ID uživatele návštěvníka. Nebo může být nutné přizpůsobit hodnotu parametru před odesláním do metody základního objektu prvku ObjectDataSource.

Vždy, když je vyvolána metoda `Select` ObjectDataSource, prvek ObjectDataSource nejprve vyvolá [událost výběru](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx). Pak se vyvolá metoda základního objektu ObjectDataSource. Po dokončení [události](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) ovládacího prvku ObjectDataSource je aktivována (obrázek 1 znázorňuje tuto posloupnost událostí). Hodnoty parametrů předané metodě základního objektu prvku ObjectDataSource lze nastavit nebo přizpůsobit v obslužné rutině události `Selecting`.

[![vybrané události ObjectDataSource a výběr událostí před a po vyvolání metody podkladového objektu.](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)

**Obrázek 1**: událost `Selected` a `Selecting` prvku ObjectDataSource byly vyvolány před a po vyvolání příslušné metody objektu ([kliknutím zobrazíte obrázek v plné velikosti](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png))

V tomto kurzu se podíváme na přidání metody do našich DAL a knihoven BLLů, které přijímají jeden vstupní parametr `Month`typu `Integer` a vrátí `EmployeesDataTable` objekt naplněný zaměstnanci, kteří mají k dispozici svůj pronájem v zadaném `Month`. V našem příkladu se tento parametr nastaví programově na základě aktuálního měsíce a zobrazí se seznam "výročí zaměstnanců v tomto měsíci".

Pojďme začít!

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>Krok 1: Přidání metody do`EmployeesTableAdapter`

Pro náš první příklad musíme přidat způsob, jak načítat zaměstnance, jejichž `HireDate` v zadaném měsíci nastaly. Aby tato funkce byla v souladu s naší architekturou, musíme nejdřív vytvořit metodu v `EmployeesTableAdapter`, která se mapuje na správný příkaz SQL. Pokud to chcete provést, Začněte otevřením datové sady typu Northwind. Klikněte pravým tlačítkem myši na popisek `EmployeesTableAdapter` a vyberte možnost Přidat dotaz.

[![přidat nový dotaz do EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)

**Obrázek 2**: Přidání nového dotazu do `EmployeesTableAdapter` ([kliknutím zobrazíte obrázek v plné velikosti](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))

Vyberte, chcete-li přidat příkaz jazyka SQL, který vrací řádky. Když se dostanete na obrazovku příkazu pro zadání `SELECT`, výchozí příkaz `SELECT` pro `EmployeesTableAdapter` se už načte. Jednoduše přidejte v klauzuli `WHERE`: `WHERE DATEPART(m, HireDate) = @Month`. [DatePart](https://msdn.microsoft.com/library/ms174420.aspx) je funkce T-SQL, která vrací určitou část data typu `datetime`. v tomto případě používáme `DATEPART` k vrácení měsíce `HireDate` sloupce.

[![vrátí pouze ty řádky, ve kterých je sloupec HireDate menší nebo roven @HiredBeforeDate parametru.](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)

**Obrázek 3**: vrátí pouze ty řádky, ve kterých je `HireDate` sloupec menší nebo roven `@HiredBeforeDate` parametru ([kliknutím zobrazíte obrázek v plné velikosti).](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png)

Nakonec Změňte názvy metod `FillBy` a `GetDataBy` na `FillByHiredDateMonth` a `GetEmployeesByHiredDateMonth`, v uvedeném pořadí.

[![zvolit vhodnější názvy metod než FillBy a GetDataBy](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)

**Obrázek 4**: vyberte vhodnější názvy metod než `FillBy` a `GetDataBy` ([kliknutím zobrazíte obrázek v plné velikosti).](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png)

Kliknutím na Dokončit dokončete průvodce a vraťte se na návrhovou plochu datové sady. `EmployeesTableAdapter` by teď měl obsahovat novou sadu metod pro přístup k zaměstnancům najatým v zadaném měsíci.

[![se nové metody zobrazí v Návrhová plocha datové sady.](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)

**Obrázek 5**: nové metody se zobrazí v návrhová plocha datové sady ([kliknutím zobrazíte obrázek v plné velikosti).](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png)

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>Krok 2: Přidání metody`GetEmployeesByHiredDateMonth(month)`do vrstvy obchodní logiky

Vzhledem k tomu, že architektura naší aplikace používá samostatnou vrstvu pro obchodní logiku a logiku přístupu k datům, musíme do našich knihoven BLL přidat metodu, která zavolá na DAL, aby se načetly zaměstnanci zařazené před zadaným datem. Otevřete soubor `EmployeesBLL.vb` a přidejte následující metodu:

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

Stejně jako u našich dalších metod v této třídě `GetEmployeesByHiredDateMonth(month)` jednoduše zavolá na DAL a vrátí výsledky.

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>Krok 3: Zobrazení zaměstnanců, jejichž nájem výročí je tento měsíc

Náš poslední krok v tomto příkladu je zobrazit zaměstnance, jejichž pronájem je v tomto měsíci. Začněte přidáním prvku GridView na stránku `ProgrammaticParams.aspx` ve složce `BasicReporting` a přidejte nový prvek ObjectDataSource jako zdroj dat. Nakonfigurujte prvek ObjectDataSource tak, aby používal třídu `EmployeesBLL` s `SelectMethod` nastavenou na `GetEmployeesByHiredDateMonth(month)`.

[![použít třídu EmployeesBLL](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)

**Obrázek 6**: použití třídy `EmployeesBLL` ([kliknutím zobrazíte obrázek v plné velikosti](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))

[![vybrat z metody GetEmployeesByHiredDateMonth (měsíc)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)

**Obrázek 7**: vyberte z metody `GetEmployeesByHiredDateMonth(month)` ([kliknutím zobrazíte obrázek v plné velikosti](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png)).

Poslední obrazovka vás požádá o zadání zdroje hodnoty parametrů `month`. Vzhledem k tomu, že tuto hodnotu nastavíme programově, ponechte zdroj parametru nastavený na výchozí možnost None a klikněte na Dokončit.

[![ponechat zdroj parametru nastavený na None](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)

**Obrázek 8**: ponechte zdroj parametru nastavený na None ([kliknutím zobrazíte obrázek v plné velikosti).](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png)

Tím se vytvoří objekt `Parameter` v kolekci `SelectParameters` ObjectDataSource, která nemá zadanou hodnotu.

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

Pro programové nastavení této hodnoty musíme vytvořit obslužnou rutinu události pro událost `Selecting` prvku ObjectDataSource. Chcete-li to provést, přejděte na zobrazení Návrh a dvakrát klikněte na prvek ObjectDataSource. Případně vyberte prvek ObjectDataSource, přejděte na okno Vlastnosti a klikněte na ikonu blesku. Dále dvakrát klikněte na textové pole vedle události `Selecting` nebo zadejte název obslužné rutiny události, kterou chcete použít. Třetí možností je vytvořit obslužnou rutinu události výběrem prvku ObjectDataSource a jeho `Selecting` události z obou rozevíracích seznamů v horní části třídy kódu na pozadí stránky.

![Klikněte na ikonu blesku v okně Vlastnosti a uveďte události webového ovládacího prvku.](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

**Obrázek 9**: klikněte na ikonu blesku v okně Vlastnosti a uveďte události webového ovládacího prvku.

Všechny tři přístupy přidají novou obslužnou rutinu události pro událost `Selecting` ObjectDataSource do třídy kódu na pozadí stránky. V této obslužné rutině události můžeme číst a zapisovat do hodnot parametrů pomocí `e.InputParameters(parameterName)`, kde *`parameterName`* je hodnota atributu `Name` v `<asp:Parameter>` značce (`InputParameters` kolekce může být také indexována pořadovým číslem, jako v `e.InputParameters(index)`). Chcete-li nastavit parametr `month` na aktuální měsíc, přidejte následující do obslužné rutiny události `Selecting`:

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

Když navštívíte tuto stránku prostřednictvím prohlížeče, uvidíme, že tento měsíc byl přijat jenom jeden zaměstnanec (březen) Laura Callahan, který se od společnosti od 1994.

[![zaměstnanci, jejichž výročí jsou uvedené v tomto měsíci](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)

**Obrázek 10**: zaměstnanci, jejichž výročí jsou uvedené v tomto měsíci ([kliknutím zobrazíte obrázek v plné velikosti](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))

## <a name="summary"></a>Souhrn

Přestože hodnoty parametrů ObjectDataSource lze obvykle nastavit deklarativně, bez nutnosti kódu řádku, je snadné nastavit hodnoty parametrů programově. Vše, co musíme udělat, je vytvořit obslužnou rutinu události pro událost `Selecting` ObjectDataSource, která se aktivuje před vyvoláním metody podkladového objektu, a ručně nastavit hodnoty pro jeden nebo více parametrů prostřednictvím kolekce `InputParameters`.

V tomto kurzu se uzavírá základní oddíl vytváření sestav. V [dalším kurzu](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) se dozvíte, jak scénáře filtrování a hlavní-podrobnosti podíváme na postupy, které návštěvníkovi umožní filtrovat data a přejít k podrobnostem z hlavní sestavy na sestavu podrobností.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](declarative-parameters-vb.md)
