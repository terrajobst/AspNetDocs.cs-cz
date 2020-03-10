---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: Vytváření tříd modelu pomocí Entity Framework (C#) | Microsoft Docs
author: microsoft
description: V tomto kurzu se naučíte používat ASP.NET MVC s Microsoft Entity Framework. Naučíte se, jak pomocí Průvodce entitou vytvořit ADO.NET entitu da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 2e0e365c287fc455015d237ea466301335805d14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581163"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Vytvoření tříd modelu v sadě Entity Framework (C#)

od [Microsoftu](https://github.com/microsoft)

> V tomto kurzu se naučíte používat ASP.NET MVC s Microsoft Entity Framework. Naučíte se, jak pomocí Průvodce entitou vytvořit model EDM (Entity Data Model) ADO.NET. V průběhu tohoto kurzu sestavíme webovou aplikaci, která ukazuje, jak vybírat, vkládat, aktualizovat a odstraňovat databázová data pomocí Entity Framework.

Cílem tohoto kurzu je vysvětlit, jak můžete při sestavování aplikace ASP.NET MVC vytvořit třídy přístupu k datům pomocí Microsoft Entity Framework. V tomto kurzu se nepředpokládá žádné předchozí znalosti služby Microsoft Entity Framework. Na konci tohoto kurzu budete rozumět tomu, jak použít Entity Framework k výběru, vkládání, aktualizaci a odstraňování záznamů databáze.

Microsoft Entity Framework je nástroj pro mapování relačních objektů (O/RM), který umožňuje vygenerovat vrstvu přístupu k datům automaticky z databáze. Entity Framework vám umožní vyhnout se zdlouhavé práci na vytváření tříd přístupu k datům ručně.

Pro ilustraci, jak můžete používat Microsoft Entity Framework s ASP.NET MVC, vytvoříme jednoduchou ukázkovou aplikaci. Vytvoříme aplikaci filmové databáze, která vám umožní zobrazit a upravit záznamy filmové databáze.

V tomto kurzu se předpokládá, že máte Visual Studio 2008 nebo Visual Web Developer 2008 s aktualizací Service Pack 1. Aby bylo možné použít Entity Framework, potřebujete aktualizaci Service Pack 1. Aktualizaci Visual Studio 2008 Service Pack 1 nebo Visual Web Developer s aktualizací Service Pack 1 si můžete stáhnout z následující adresy:

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> Mezi ASP.NET MVC a Microsoft Entity Framework neexistuje žádné nezbytné připojení. Existuje několik alternativ Entity Framework, které můžete použít s ASP.NET MVC. Můžete například sestavit třídy MVC modelu pomocí jiných nástrojů pro/RM, jako je například Microsoft LINQ to SQL, NHibernate nebo Subsonic.

## <a name="creating-the-movie-sample-database"></a>Vytvoření ukázkové databáze filmů

Aplikace filmové databáze používá databázovou tabulku s názvem filmy, která obsahuje následující sloupce:

| Název sloupce | Typ dat | Chcete povoluje hodnoty null? | Je primární klíč? |
| --- | --- | --- | --- |
| ID | int | False | True |
| Název | nvarchar (100) | False | False |
| Ředitel | nvarchar (100) | False | False |

Tuto tabulku můžete přidat do projektu ASP.NET MVC pomocí následujících kroků:

1. V okně Průzkumník řešení klikněte pravým tlačítkem na složku data\_aplikace a vyberte možnost nabídky **Přidat, nová položka.**
2. V dialogovém okně **Přidat novou položku** vyberte **SQL Server databáze**, pojmenujte databázi MoviesDB. mdf a klikněte na tlačítko **Přidat** .
3. Dvojím kliknutím na soubor MoviesDB. mdf otevřete okno Průzkumník serveru/Průzkumník databáze.
4. Rozbalte připojení k databázi MoviesDB. mdf, klikněte pravým tlačítkem myši na složku tabulky a vyberte možnost nabídky **Přidat novou tabulku**.
5. V Návrháři tabulky přidejte sloupce ID, název a režisér.
6. Klikněte na tlačítko **Uložit** (má ikonu na disketě) a uložte novou tabulku s názvem filmy.

Po vytvoření databázové tabulky filmů byste měli do tabulky přidat ukázková data. Klikněte pravým tlačítkem myši na tabulku filmy a vyberte možnost nabídky **Zobrazit data tabulky**. Do mřížky, která se zobrazí, můžete zadat falešné filmové údaje.

## <a name="creating-the-adonet-entity-data-model"></a>Vytváření model EDM (Entity Data Model) ADO.NET

Aby bylo možné použít Entity Framework, je nutné vytvořit model EDM (Entity Data Model). Můžete využít výhod *průvodce model EDM (Entity Data Model)* sady Visual Studio k automatickému vygenerování model EDM (Entity Data Model) z databáze.

Postupujte následovně:

1. V okně Průzkumník řešení klikněte pravým tlačítkem na složku modely a vyberte možnost nabídky **Přidat, nová položka**.
2. V dialogovém okně **Přidat novou položku** vyberte kategorii dat (viz obrázek 1).
3. Vyberte šablonu **model EDM (Entity Data Model) ADO.NET** , zadejte model EDM (Entity Data Model) název MoviesDBModel. edmx a klikněte na tlačítko **Přidat** . Kliknutím na tlačítko **Přidat** spustíte Průvodce datovým modelem.
4. V kroku **zvolit obsah modelu** vyberte možnost **Generovat z databáze** a klikněte na tlačítko **Další** (viz obrázek 2).
5. V kroku **Zvolte datové připojení** vyberte připojení k databázi MoviesDB. mdf, zadejte název nastavení připojení entity MoviesDBEntities a klikněte na tlačítko **Další** (viz obrázek 3).
6. V kroku **Zvolte databázové objekty** vyberte tabulku video databáze a klikněte na tlačítko **Dokončit** (viz obrázek 4).

Po dokončení tohoto postupu se otevře Návrhář ADO.NET model EDM (Entity Data Model) (Entity Designer).

**Obrázek 1 – Vytvoření nového model EDM (Entity Data Model)**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**Obrázek 2 – krok výběr obsahu modelu**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**Obrázek 3 – Výběr datového připojení**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**Obrázek 4 – Výběr databázových objektů**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>Úprava model EDM (Entity Data Model) ADO.NET

Po vytvoření model EDM (Entity Data Model) můžete model upravit tím, že využijete výhod Entity Designer (viz obrázek 5). Entity Designer můžete kdykoli otevřít tak, že dvakrát kliknete na soubor MoviesDBModel. edmx obsažený ve složce modely v Průzkumník řešení okně.

**Obrázek 5 – Návrhář model EDM (Entity Data Model) ADO.NET**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

Můžete například použít Entity Designer ke změně názvů tříd, které generuje Průvodce daty modelu entity. Průvodce vytvořil novou třídu pro přístup k datům s názvem filmy. Jinými slovy, průvodce přiřadil třídu stejný název jako databázová tabulka. Vzhledem k tomu, že tuto třídu použijeme k reprezentování konkrétní instance videa, doporučujeme přejmenovat třídu z filmů na video.

Pokud chcete přejmenovat třídu entity, můžete dvakrát kliknout na název třídy v Entity Designer a zadat nový název (viz obrázek 6). Případně můžete název entity v okno Vlastnosti změnit po výběru entity v Entity Designer.

**Obrázek 6 – Změna názvu entity**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

Po provedení úprav nezapomeňte uložit model EDM (Entity Data Model) kliknutím na tlačítko Uložit (ikona na disketě). Na pozadí Entity Designer generuje sadu C# tříd. Tyto třídy můžete zobrazit otevřením souboru MoviesDBModel.Designer.cs z okna Průzkumník řešení.

Neměňte kód v souboru Designer.cs, protože změny budou při příštím použití Entity Designer přepsány. Pokud chcete roztáhnout funkce tříd entit definovaných v souboru Designer.cs, můžete vytvořit *částečné třídy* v samostatných souborech.

#### <a name="selecting-database-records-with-the-entity-framework"></a>Výběr záznamů databáze pomocí Entity Framework

Pojďme začít sestavovat naši aplikaci pro filmové databáze vytvořením stránky, která zobrazuje seznam filmových záznamů. U domovského kontroleru v výpisu 1 se zveřejňuje akce s názvem index (). Akce index () vrátí všechny záznamy filmů z tabulky filmové databáze tím, že využije Entity Framework.

**Výpis 1 – souboru controllers\homecontroller.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

Všimněte si, že kontroler v seznamu 1 obsahuje konstruktor. Konstruktor inicializuje pole na úrovni třídy s názvem \_DB. Pole \_dB představuje databázové entity vygenerované Microsoft Entity Framework. Pole \_DB je instancí třídy MoviesDBEntities, která byla vygenerována Entity Designer.

Aby bylo možné použít třídu theMoviesDBEntities v rámci domovského kontroleru, je nutné importovat obor názvů MovieEntityApp. Models (*MVCProjectName*. Modely).

Pole \_DB se používá v rámci akce index () k načtení záznamů z tabulky databáze filmů. Výraz \_DB. MovieSet představuje všechny záznamy z databázové tabulky filmů. Metoda ToList – () slouží k převodu sady filmů do obecné kolekce objektů Movie (list&lt;Movie&gt;).

Filmové záznamy se načítají pomocí LINQ to Entities. Akce index () v seznamu 1 používá *syntaxi metody* LINQ k načtení sady záznamů databáze. Pokud dáváte přednost, můžete místo toho použít *syntaxi dotazu* LINQ. Následující dva příkazy dělají stejnou věc:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

Použijte jakoukoli syntaxi syntaxe LINQ – syntaxi metody nebo syntaxi dotazů, které najdete nejvíc intuitivní. Mezi oběma přístupy nedochází k žádnému rozdílu ve výkonu – jediným rozdílem je styl.

Zobrazení v seznamu 2 slouží k zobrazení záznamů filmů.

**Výpis 2 – Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

Zobrazení v seznamu 2 obsahuje smyčku **foreach** , která projde každým záznamem videa a zobrazí hodnoty vlastností název a režisér záznamu videa. Všimněte si, že se vedle každého záznamu zobrazuje odkaz upravit a odstranit. Kromě toho se v dolní části zobrazení zobrazí odkaz Přidat film (viz obrázek 7).

**Obrázek 7 – zobrazení indexu**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

Zobrazení index je typu *zobrazení*. Zobrazení indexů obsahuje direktivu &lt;% @ Page%&gt; s atributem *Inherits* , který předává vlastnost model na seznam obecných seznamů objektů videa typu "silně typované" (seznam&lt;film).

## <a name="inserting-database-records-with-the-entity-framework"></a>Vkládání záznamů databáze pomocí Entity Framework

Entity Framework můžete použít k usnadnění vkládání nových záznamů do databázové tabulky. Výpis 3 obsahuje dvě nové akce přidané do třídy domovského kontroleru, které můžete použít k vložení nových záznamů do tabulky filmové databáze.

**Výpis 3 – souboru controllers\homecontroller.cs (Přidání metod)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

První akce Přidat () jednoduše vrátí zobrazení. Zobrazení obsahuje formulář pro přidání nového záznamu filmové databáze (viz obrázek 8). Při odeslání formuláře je vyvolána druhá akce Přidat ().

Všimněte si, že druhá akce Přidat () je upravena pomocí atributu AcceptVerbs. Tuto akci lze vyvolat pouze při provádění operace HTTP POST. Jinými slovy, tuto akci lze vyvolat pouze při publikování formuláře HTML.

Druhá akce Přidat () vytvoří novou instanci třídy Entity Framework Movie s použitím metody ASP.NET MVC TryUpdateModel (). Metoda TryUpdateModel () převezme pole v Podoběcollection předané do metody Add () a přiřadí hodnoty těchto polí formuláře HTML do třídy video.

Při použití Entity Framework je nutné při použití metod TryUpdateModel nebo UpdateModel pro aktualizaci vlastností třídy entity uvést "bílý seznam vlastností".

V dalším kroku akce Přidat () provede určité jednoduché ověření formuláře. Akce ověří, že vlastnosti title a Director mají hodnoty. Pokud dojde k chybě ověřování, do ModelState se přidá chybová zpráva o ověření.

Pokud nedošlo k chybám ověření, přidá se do tabulky video Database nový záznam filmu s použitím Entity Framework. Nový záznam se přidá do databáze s následujícími dvěma řádky kódu:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

První řádek kódu přidá novou entitu video do sady filmů sledovaných pomocí Entity Framework. Druhý řádek kódu uloží veškeré změny, které byly provedeny u filmů sledovaných zpět do podkladové databáze.

**Obrázek 8 – zobrazení přidat**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>Aktualizace databázových záznamů pomocí Entity Framework

Můžete použít skoro stejný přístup pro úpravu záznamu databáze s Entity Framework jako metodu, kterou jsme právě následovali za účelem vložení nového záznamu databáze. Výpis 4 obsahuje dvě nové akce kontroleru s názvem Edit (). První akce upravit () vrátí formulář HTML pro úpravu záznamu filmu. Druhá akce Edit () se pokusí aktualizovat databázi.

**Výpis 4 – souboru controllers\homecontroller.cs (upravit metody)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

Druhá akce Edit () začíná načtením záznamu filmu z databáze, která odpovídá ID upravovaného filmu. Následující příkaz LINQ to Entities přiřadí první záznam v databázi, který odpovídá konkrétnímu ID:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

Dále metoda TryUpdateModel () slouží k přiřazení hodnot polí formuláře HTML k vlastnostem entity video. Všimněte si, že je k dispozici prázdný seznam pro určení přesných vlastností, které se mají aktualizovat.

V dalším kroku se provede nějaké jednoduché ověření, které ověří, že vlastnosti názvu a režiséra filmu mají hodnoty. Pokud chybí hodnota vlastnosti, je přidána chybová zpráva ověření do ModelState a ModelState. IsValid vrátí hodnotu false.

Nakonec, pokud nejsou k dispozici žádné chyby ověřování, je podkladová tabulka databáze filmů aktualizována o všechny změny voláním metody SaveChanges ().

Při úpravách záznamů databáze je třeba předat ID upravovaného záznamu do akce kontroleru, která provádí aktualizaci databáze. V opačném případě akce kontroleru nebude informovat o tom, který záznam má být aktualizován v podkladové databázi. Zobrazení pro úpravy obsažené v seznamu 5 obsahuje skryté pole formuláře, které představuje ID upravovaného záznamu databáze.

**Výpis 5 – Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Odstranění záznamů databáze pomocí Entity Framework

Poslední databázová operace, kterou potřebujeme v tomto kurzu řešit, je odstraňování záznamů databáze. K odstranění konkrétního záznamu databáze můžete použít akci kontroleru v výpisu 6.

**Výpis 6--\Controllers\HomeController.cs (akce Odstranit)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Akce Odstranit () nejprve načte entitu videa, která odpovídá ID předané akci. Dále je film odstraněn z databáze voláním metody OdstranitObjekt () následovaný metodou SaveChanges (). Nakonec se uživatel přesměruje zpět do zobrazení indexu.

## <a name="summary"></a>Souhrn

Účelem tohoto kurzu je předvést, jak můžete vytvářet databázové webové aplikace s využitím ASP.NET MVC a Microsoft Entity Framework. Zjistili jste, jak vytvořit aplikaci, která umožňuje výběr, vložení, aktualizaci a odstranění záznamů databáze.

Nejprve jsme probrali, jak můžete pomocí Průvodce model EDM (Entity Data Model) vygenerovat model EDM (Entity Data Model) z aplikace Visual Studio. Dále se naučíte, jak pomocí LINQ to Entities načíst sadu databázových záznamů z databázové tabulky. Nakonec jsme použili Entity Framework k vkládání, aktualizaci a odstraňování záznamů databáze.

> [!div class="step-by-step"]
> [Next](creating-model-classes-with-linq-to-sql-cs.md)
