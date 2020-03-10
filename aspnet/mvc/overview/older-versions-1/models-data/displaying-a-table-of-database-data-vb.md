---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: Zobrazení tabulky databázových dat (VB) | Microsoft Docs
author: microsoft
description: V tomto kurzu si ukážeme dvě metody zobrazení sady záznamů databáze. Zobrazuje se dvě metody formátování sady záznamů databáze v HTML...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: f2e2489ac8455913f55c746dbe05b9fe8272285b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543013"
---
# <a name="displaying-a-table-of-database-data-vb"></a>Zobrazení tabulky databázových dat (VB)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> V tomto kurzu si ukážeme dvě metody zobrazení sady záznamů databáze. Zobrazuje se dvě metody formátování sady záznamů databáze v tabulce HTML. Nejprve ukazuje, jak lze naformátovat záznamy databáze přímo v rámci zobrazení. Dále ukážeme, jak můžete při formátování záznamů databáze využít výhod částečných.

Cílem tohoto kurzu je vysvětlit, jak můžete zobrazit tabulku dat databáze HTML v aplikaci ASP.NET MVC. Nejprve se naučíte, jak pomocí nástrojů pro generování uživatelského rozhraní, které jsou součástí sady Visual Studio, vygenerovat zobrazení, které automaticky zobrazí sadu záznamů. V dalším kroku se dozvíte, jak při formátování záznamů databáze použít částečnou jako šablonu.

## <a name="create-the-model-classes"></a>Vytvoření tříd modelu

Chystáme se zobrazit sadu záznamů z tabulky databáze filmů. Tabulka video s filmy obsahuje následující sloupce:

<a id="0.4_table01"></a>

| **Název sloupce** | **Datový typ** | **Povoluje hodnoty null.** |
| --- | --- | --- |
| ID | Int | False |
| Název | Nvarchar(200) | False |
| Ředitel | NVarchar(50) | False |
| DateReleased | DateTime | False |

Aby bylo možné znázornit tabulku filmů v naší aplikaci ASP.NET MVC, musíme vytvořit třídu modelu. V tomto kurzu používáme Microsoft Entity Framework k vytváření tříd modelů.

> [!NOTE] 
> 
> V tomto kurzu používáme Microsoft Entity Framework. Je ale důležité si uvědomit, že k interakci s databází z aplikace ASP.NET MVC, včetně LINQ to SQL, NHibernate nebo ADO.NET, můžete použít celou řadu různých technologií.

Pomocí těchto kroků spusťte Průvodce model EDM (Entity Data Model):

1. V okně Průzkumník řešení klikněte pravým tlačítkem na složku modely a vyberte možnost nabídky **Přidat, nová položka**.
2. Vyberte kategorii **dat** a vyberte šablonu **model EDM (Entity Data Model) ADO.NET** .
3. Udělte datovému modelu název *MoviesDBModel. edmx* a klikněte na tlačítko **Přidat** .

Po kliknutí na tlačítko Přidat se zobrazí průvodce model EDM (Entity Data Model) (viz obrázek 1). Pomocí těchto kroků dokončete Průvodce:

1. V kroku **zvolit obsah modelu** vyberte možnost **Generovat z databáze** .
2. V kroku **Vybrat datové připojení** použijte datové připojení *MoviesDB. mdf* a název *MoviesDBEntities* pro nastavení připojení. Klikněte na tlačítko **Další**.
3. V kroku **Zvolte databázové objekty** rozbalte uzel tabulky a vyberte tabulku filmy. Zadejte *modely* názvů a klikněte na tlačítko **Dokončit** .

[![vytváření tříd LINQ to SQL](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**Obrázek 01**: vytváření tříd LINQ to SQL ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-vb/_static/image2.png))

Po dokončení průvodce model EDM (Entity Data Model) se otevře Návrhář model EDM (Entity Data Model). Návrhář by měl zobrazit entitu filmy (viz obrázek 2).

[![návrháře model EDM (Entity Data Model)](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**Obrázek 02**: Návrhář model EDM (Entity Data Model) ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-vb/_static/image4.png))

Než budeme pokračovat, musíme udělat jednu změnu. Průvodce data entity vygeneruje třídu modelu s názvem *filmy* , která představuje tabulku databáze filmů. Vzhledem k tomu, že použijeme třídu filmů k reprezentování konkrétního filmu, musíme upravit název třídy tak, aby se místo *filmů* použil *film* (číslo v čísle místo plural).

Dvakrát klikněte na název třídy na návrhové ploše a změňte název třídy z filmů na film. Po provedení této změny klikněte na tlačítko **Uložit** (ikona disketové jednotky) a vygenerujte třídu video.

## <a name="create-the-movies-controller"></a>Vytvoření kontroleru filmů

Teď, když máme způsob reprezentace našich záznamů v databázi, můžeme vytvořit kontroler, který vrátí kolekci filmů. V okně Visual Studio Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers a vyberte možnost nabídky **Přidat, kontroler** (viz obrázek 3).

[![nabídky přidat řadič](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**Obrázek 03**: nabídka přidat řadič ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-vb/_static/image6.png))

Po zobrazení dialogového okna **Přidat řadič** zadejte název kontroleru MovieController (viz obrázek 4). Kliknutím na tlačítko **Přidat** přidejte nový kontroler.

[![dialogového okna přidat řadič](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**Obrázek 04**: dialogové okno Přidat řadič ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-vb/_static/image8.png))

Musíme Upravit akci index () zpřístupněnou pro kontroler filmů, aby vracela sadu záznamů databáze. Upravte kontroler tak, aby vypadal jako kontroler v seznamu 1.

**Výpis 1 – Controllers\MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

V seznamu 1 třída MoviesDBEntities slouží k reprezentaci databáze MoviesDB. Entity výrazu *. MovieSet. ToList – ()* vrátí sadu všech filmů z tabulky databáze filmů.

## <a name="create-the-view"></a>Vytvoření zobrazení

Nejjednodušší způsob, jak zobrazit sadu databázových záznamů v tabulce HTML, je využít výhody generování uživatelského rozhraní, které poskytuje Visual Studio.

Sestavte aplikaci výběrem možnosti nabídky **sestavení, řešení sestavení**. Před otevřením dialogového okna **Přidat zobrazení** nebo z vašich datových tříd se v dialogovém okně nezobrazují vaše aplikace.

Klikněte pravým tlačítkem myši na akci index () a vyberte možnost nabídky **Přidat zobrazení** (viz obrázek 5).

[![přidání zobrazení](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**Obrázek 05**: Přidání zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-vb/_static/image10.png))

V dialogovém okně **Přidat zobrazení** zaškrtněte políčko **vytvořit zobrazení silného typu**. Jako **třídu zobrazení dat**vyberte třídu filmů. Vyberte možnost *seznam* jako **obsah zobrazení** (viz obrázek 6). Výběrem těchto možností se vytvoří zobrazení se silným typem, které zobrazí seznam filmů.

[![dialogového okna Přidat zobrazení](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**Obrázek 6**: dialogové okno Přidat zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-vb/_static/image12.png))

Po kliknutí na tlačítko **Přidat** se zobrazení v seznamu 2 vygeneruje automaticky. Toto zobrazení obsahuje kód potřebný k iterování v kolekci filmů a zobrazení všech vlastností filmu.

**Výpis 2 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

Aplikaci můžete spustit výběrem možnosti nabídky **ladění, spustit ladění** (nebo stisknutím klávesy F5). Spuštění aplikace spustí aplikaci Internet Explorer. Pokud přejdete na adresu URL/Movie, uvidíte stránku na obrázku 7.

[![tabulce filmů](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**Obrázek 07**: tabulka filmů ([kliknutím zobrazíte obrázek v plné velikosti](displaying-a-table-of-database-data-vb/_static/image14.png))

Pokud se vám nezobrazují žádné informace o vzhledu mřížky záznamů databáze na obrázku 7, můžete jednoduše upravit zobrazení indexu. Můžete například změnit hlavičku *DateReleased* na *Datum vydání* úpravou zobrazení index.

## <a name="create-a-template-with-a-partial"></a>Vytvoření šablony s částečnou

Pokud se zobrazení příliš komplikované, je vhodné začít přerušit zobrazení na částečný. Použití částečně usnadňuje pochopení a udržování vašich zobrazení. Vytvoříme částečně, kterou můžeme použít jako šablonu k formátování každého záznamu filmové databáze.

Pomocí těchto kroků můžete vytvořit částečnou:

1. Klikněte pravým tlačítkem na složku Views\Movie a vyberte možnost nabídky **Přidat zobrazení**.
2. Zaškrtněte políčko s názvem *vytvořit částečné zobrazení (. ascx)* .
3. Pojmenujte částečnou *MovieTemplate*.
4. Zaškrtněte políčko s názvem **vytvořit zobrazení silného typu**.
5. Jako *třídu zobrazení dat*vyberte video.
6. Jako *zobrazení obsahu*vyberte prázdné.
7. Kliknutím na tlačítko **Přidat** přidáte do projektu částečnou možnost.

Po dokončení těchto kroků upravte MovieTemplate částečně tak, aby vypadaly jako v seznamu 3.

**Výpis 3 – Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

Částečně v seznamu 3 obsahuje šablonu pro jeden řádek záznamů.

Změněné zobrazení indexu v seznamu 4 používá částečnou MovieTemplate.

**Výpis 4 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

Zobrazení v seznamu 4 obsahuje odpověď pro každou smyčku, která projde všemi filmy. Pro každý film se k naformátování videa používá částečná MovieTemplate. MovieTemplate je vykreslen voláním pomocné metody RenderPartial ().

Změněné zobrazení indexu vykreslí velmi stejnou tabulku HTML záznamů databáze. Zobrazení se ale významně zjednodušilo.

Metoda RenderPartial () je odlišná od většiny ostatních pomocných metod, protože nevrací řetězec. Proto je nutné volat metodu RenderPartial () pomocí &lt;% HTML. RenderPartial ()%&gt; namísto &lt;% = HTML. RenderPartial ()%&gt;.

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo vysvětlit, jak můžete zobrazit sadu záznamů databáze v tabulce HTML. Nejdřív jste zjistili, jak vrátit sadu záznamů databáze z akce kontroleru tím, že využijete výhod Entity Framework Microsoftu. Dále jste zjistili, jak používat generování uživatelského rozhraní sady Visual Studio k vygenerování zobrazení, které automaticky zobrazuje kolekci položek. Nakonec jste zjistili, jak zjednodušit zobrazení využitím částečného. Zjistili jste, jak použít částečný jako šablonu, abyste mohli naformátovat každý záznam v databázi.

> [!div class="step-by-step"]
> [Předchozí](creating-model-classes-with-linq-to-sql-vb.md)
> [Další](performing-simple-validation-vb.md)
