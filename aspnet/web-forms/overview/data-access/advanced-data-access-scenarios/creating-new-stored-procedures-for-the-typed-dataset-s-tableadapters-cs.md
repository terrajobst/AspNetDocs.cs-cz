---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: Vytváření nových uložených procedur pro objekty TableAdapter (C#) typované datové sady | Microsoft Docs
author: rick-anderson
description: V předchozích kurzech jsme v našem kódu vytvořili příkazy SQL a předali příkazy do databáze, která se má spustit. Alternativním přístupem je použití s...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 751282ca-5870-4d66-84e4-6cefae23eb4a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: db0d83a0fd1f1f175001d20844b298be0cf7e1cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78533710"
---
# <a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>Vytvoření nových uložených procedur prvků TableAdapter typových sad dat (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_CS.zip) nebo [stažení PDF](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial67cs1.pdf)

> V předchozích kurzech jsme v našem kódu vytvořili příkazy SQL a předali příkazy do databáze, která se má spustit. Alternativním přístupem je použití uložených procedur, kde jsou příkazy SQL předem definovány v databázi. V tomto kurzu se dozvíte, jak může Průvodce TableAdapter vygenerovat nové uložené procedury pro nás.

## <a name="introduction"></a>Úvod

Vrstva přístupu k datům (DAL) pro tyto kurzy používá typové datové sady. Jak je popsáno v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-cs.md) , typové datové sady se skládají z DataTables a objekty TableAdapter silného typu. Datové tabulky reprezentují logické entity v systému, zatímco rozhraní objekty TableAdapter s podkladovou databází provádí práci s daty. To zahrnuje naplnění datových tabulek daty, provádění dotazů, které vracejí skalární data a vkládání, aktualizaci a odstraňování záznamů z databáze.

Příkazy SQL spouštěné objekty TableAdapter můžou být buď ad hoc příkazy SQL, například `SELECT columnList FROM TableName`nebo uložené procedury. Objekty TableAdapter v naší architektuře používá ad-hoc příkazy SQL. Mnoho vývojářů a správců databází ale raději ukládá uložené procedury přes ad hoc příkazy SQL kvůli zabezpečení, údržbě a důvodům pro aktualizaci. Další ardently upřednostňují ad-hoc příkazy SQL pro jejich flexibilitu. Ve své vlastní práci mám přednost uložených procedurám prostřednictvím ad-hoc příkazů SQL, ale zvolili byste používat ad-hoc SQL příkazy k zjednodušení předchozích kurzů.

Při definování TableAdapter nebo přidávání nových metod vytvoří průvodce TableAdaptery jenom tak, jak snadno vytvoří nové uložené procedury, nebo použije stávající uložené procedury, protože používá příkazy SQL ad hoc. V tomto kurzu podíváme se, jak má Průvodce TableAdapter s automaticky generovat uložené procedury. V dalším kurzu se podíváme na postup konfigurace metod TableAdapter s pro použití existujících nebo ručně vytvořených uložených procedur.

> [!NOTE]
> Informace o tom, že záznam blogu pro Rob Howard [ještě nepoužívá uložené procedury?](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/) a uložené procedury [Frans Bouma](https://weblogs.asp.net/fbouma/) s [jsou chybné, M Marie?](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx) pro Lively diskusi o specialistech a nevýhody uložených procedur a ad hoc SQL.

## <a name="stored-procedure-basics"></a>Základy uložených procedur

Funkce jsou konstrukce společné pro všechny programovací jazyky. Funkce je kolekce příkazů, které jsou spouštěny při volání funkce. Funkce mohou přijímat vstupní parametry a volitelně mohou vracet hodnotu. *[Uložené procedury](http://en.wikipedia.org/wiki/Stored_procedure)* jsou konstrukce databáze, které sdílejí mnoho podobností s funkcemi v programovacích jazycích. Uložená procedura se skládá ze sady příkazů T-SQL, které se spustí při volání uložené procedury. Uložená procedura může přijmout nulu na mnoho vstupních parametrů a může vracet skalární hodnoty, výstupní parametry nebo nejčastěji výsledné sady pro `SELECT` dotazů.

> [!NOTE]
> Uložené procedury se často označují jako sprocs nebo SPs.

Uložené procedury jsou vytvořeny pomocí příkazu jazyka t-SQL [`CREATE PROCEDURE`](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) . Například následující skript T-SQL vytvoří uloženou proceduru s názvem `GetProductsByCategoryID`, která převezme jeden parametr s názvem `@CategoryID` a vrátí pole `ProductID`, `ProductName`, `UnitPrice`a `Discontinued` těchto sloupců v tabulce `Products`, která mají odpovídající `CategoryID` hodnotu:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

Jakmile je tato uložená procedura vytvořena, lze ji volat pomocí následující syntaxe:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.sql)]

> [!NOTE]
> V dalším kurzu provedeme kontrolu vytváření uložených procedur prostřednictvím integrovaného vývojového prostředí sady Visual Studio. Pro tento kurz ale budeme dovolit, aby Průvodce TableAdapter automaticky vygeneroval uložené procedury pro nás.

Kromě pouhého vrácení dat jsou uložené procedury často používány k provádění více databázových příkazů v rámci oboru jedné transakce. Uložená procedura s názvem `DeleteCategory`může například přebírat parametr `@CategoryID` a provádět dva `DELETE` příkazy: First, One pro odstranění souvisejících produktů a druhá z nich odstraní určenou kategorii. Více příkazů v rámci uložené procedury *není* automaticky zabaleno v rámci transakce. K zajištění, aby se úložná procedura s více příkazy zpracovala jako atomická operace, je třeba vydat další příkazy T-SQL. V dalším kurzu uvidíme, jak zabalit uložené procedury s v rámci oboru transakce.

Při použití uložených procedur v rámci architektury metody rozhraní Data Access Layer s vyvolávají konkrétní uloženou proceduru místo vydání příkazu SQL ad hoc. Tím se v rámci architektury aplikace nacentralizace umístění provedených příkazů SQL (v databázi). Tato centralizovaná pravděpodobně usnadňuje hledání, analýzu a ladění dotazů a poskytuje mnohem jasný přehled toho, kde a jak se databáze používá.

Další informace o základních informacích o uložených procedurách najdete v tématu prostředky v části Další informace na konci tohoto kurzu.

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>Krok 1: vytvoření webových stránek pokročilých scénářů vrstvy přístupu k datům

Před zahájením naší diskuze o tom, jak vytvořit DAL pomocí uložených procedur, si nejdřív věnujte chvilku, aby se vytvořily stránky ASP.NET v našem projektu webu, který budeme potřebovat pro toto a další několik kurzů. Začněte přidáním nové složky s názvem `AdvancedDAL`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`

![Přidání stránek ASP.NET pro pokročilé kurzy k scénářům vrstev přístupu k datům](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**Obrázek 1**: přidání stránek ASP.NET pro pokročilé kurzy k scénářům vrstev přístupu k datům

Podobně jako v ostatních složkách `Default.aspx` ve složce `AdvancedDAL` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png))

Nakonec tyto stránky přidejte jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značky po práci s daty v dávce `<siteMapNode>`:

[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro kurzy k pokročilým scénářům DAL.

![Mapa webu teď obsahuje položky pro kurzy k pokročilým scénářům DAL](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)

**Obrázek 3**: Mapa webu teď obsahuje položky pro kurzy k pokročilým SCÉNÁŘům dal

## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>Krok 2: Konfigurace TableAdapter pro vytváření nových uložených procedur

Aby bylo možné předvést vytvoření vrstvy přístupu k datům, která používá uložené procedury místo příkazů SQL ad-hoc, umožňuje vytvořit novou typovou datovou sadu ve složce `~/App_Code/DAL` s názvem `NorthwindWithSprocs.xsd`. Vzhledem k tomu, že jsme tento proces pozměnili podrobněji v předchozích kurzech, budeme postupovat rychle podle těchto kroků. Pokud se vám zablokuje nebo potřebuje další podrobné pokyny k vytvoření a konfiguraci typované datové sady, přečtěte si kurz [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-cs.md) .

Přidejte do projektu novou datovou sadu tak, že kliknete pravým tlačítkem na složku `DAL`, zvolíte příkaz Přidat novou položku a vyberete šablonu datové sady, jak je znázorněno na obrázku 4.

[![do projektu s názvem NorthwindWithSprocs. xsd přidejte novou typovou datovou sadu.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png)

**Obrázek 4**: přidejte do projektu s názvem `NorthwindWithSprocs.xsd` novou typovou datovou sadu ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png)

Tím se vytvoří nová Zadaná datová sada, otevřete jejího návrháře, vytvořte novou TableAdapter a spusťte Průvodce konfigurací TableAdapter. První krok průvodce konfigurací TableAdapter vás vyzve k výběru databáze, se kterou chcete pracovat. Připojovací řetězec k databázi Northwind by měl být uveden v rozevíracím seznamu. Vyberte tuto možnost a klikněte na další.

Z této další obrazovky můžeme zvolit, jak má TableAdapter přistupovat k databázi. V předchozích kurzech jsme vybrali první možnost, použijte příkazy SQL. Pro tento kurz vyberte druhou možnost, vytvořte nové uložené procedury a klikněte na další.

[![dá TableAdapter vytvořit nové uložené procedury.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png)

**Obrázek 5**: Dejte TableAdapter pokyn k vytvoření nových uložených procedur ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png)).

Stejně jako v případě použití ad-hoc příkazů SQL je v následujícím kroku požádáni o poskytnutí příkazu `SELECT` pro hlavní dotaz TableAdapter s. Místo toho, abyste pomocí příkazu `SELECT`, který tady zadáte, provedli dotaz ad-hoc přímo, Průvodce TableAdapter vytvoří uloženou proceduru, která obsahuje tento `SELECT` dotaz.

Pro tento TableAdapter použijte následující dotaz `SELECT`:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

[![zadat dotaz SELECT](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png)

**Obrázek 6**: zadejte `SELECT` dotaz ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png)).

> [!NOTE]
> Výše uvedený dotaz se mírně liší od hlavního dotazu `ProductsTableAdapter` v datové sadě `Northwind` typu. Odvolání, že `ProductsTableAdapter` v datové sadě `Northwind` typu obsahuje dva korelační poddotazy k uvedení názvu kategorie a názvu společnosti pro každou kategorii produktů a dodavatele. V nadcházející [aktualizaci kurzu TableAdapter pro použití spojení](updating-the-tableadapter-to-use-joins-cs.md) se podíváme na přidání těchto souvisejících dat do této TableAdapter.

Chvíli počkejte, než kliknete na tlačítko Upřesnit možnosti. Odsud můžeme určit, jestli má průvodce generovat taky příkazy INSERT, Update a DELETE pro TableAdapter, jestli se má použít Optimistická souběžnost a jestli se má tabulka dat po vložení a aktualizaci aktualizovat. Ve výchozím nastavení je zaškrtnuta možnost Generovat příkazy INSERT, Update a DELETE. Nechte zaškrtnuto. Pro tento kurz ponechte nezaškrtnuté políčko Použít optimistické možnosti souběžnosti.

Při automatickém vytvoření uložených procedur průvodcem TableAdapter se zdá, že možnost aktualizovat tabulku dat je ignorována. Bez ohledu na to, zda je toto políčko zaškrtnuto, budou výsledné vložené a aktualizované uložené procedury načítat právě vložený nebo pouze aktualizovaný záznam, jak je uvedeno v kroku 3.

![Ponechte zaškrtnuté políčko Generovat příkazy INSERT, Update a DELETE.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png)

**Obrázek 7**: zaškrtnuté políčko Generovat příkazy INSERT, Update a DELETE

> [!NOTE]
> Pokud je zaškrtnuta možnost použít optimistickou souběžnost, Průvodce přidá další podmínky k klauzuli `WHERE`, které brání v aktualizaci dat, pokud byly provedeny změny v jiných polích. Další informace o použití integrované funkce řízení souběžnosti TableAdapter s najdete v tématu o [implementaci optimistického řízení souběžnosti](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) .

Po zadání `SELECT` dotazu a potvrzení, že je zaškrtnuta možnost Generovat příkazy INSERT, Update a DELETE, klikněte na tlačítko Další. Tato další obrazovka zobrazená na obrázku 8 vyzve k zadání názvů uložených procedur, které průvodce vytvoří pro výběr, vkládání, aktualizaci a odstraňování dat. Změňte názvy těchto uložených procedur na `Products_Select`, `Products_Insert`, `Products_Update`a `Products_Delete`.

[![přejmenovat uložené procedury](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**Obrázek 8**: přejmenování uložených procedur ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png))

Chcete-li zobrazit Průvodce T-SQL, pomocí kterého bude Průvodce TableAdapter vytvářet čtyři uložené procedury, klikněte na tlačítko Náhled skriptu SQL. V dialogovém okně Náhled skriptu SQL můžete skript Uložit do souboru nebo ho zkopírovat do schránky.

![Náhled skriptu SQL používaného k vygenerování uložených procedur](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**Obrázek 9**: náhled skriptu SQL, který slouží ke generování uložených procedur

Po pojmenování uložených procedur klikněte na tlačítko Další a pojmenujte odpovídající metody TableAdapter s. Stejně jako při použití ad-hoc příkazů SQL můžeme vytvořit metody, které naplní existující DataTable nebo vrátí nový. Můžeme také určit, jestli má TableAdapter zahrnovat vzor DB-Direct pro vkládání, aktualizaci a odstraňování záznamů. Nechejte zaškrtnutá všechna tři zaškrtávací políčka, ale přejmenujte zpět metodu DataTable na `GetProducts` (jak je znázorněno na obrázku 10).

[![pojmenovat metody Fill a GetProducts](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)

**Obrázek 10**: pojmenování metod `Fill` a `GetProducts` ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png))

Kliknutím na tlačítko Další zobrazíte souhrnné informace o krocích, které průvodce provede. Průvodce dokončíte kliknutím na tlačítko Dokončit. Po dokončení průvodce se vrátíte do návrháře DataSet s, který by teď měl zahrnovat `ProductsDataTable`.

[![návrháři DataSet zobrazuje nově přidané ProductsDataTable](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)

**Obrázek 11**: v Návrháři datové sady se zobrazuje nově přidaná `ProductsDataTable` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png)

## <a name="step-3-examining-the-newly-created-stored-procedures"></a>Krok 3: prozkoumání nově vytvořených uložených procedur

Průvodce TableAdapter použitý v kroku 2 automaticky vytvořil uložené procedury pro výběr, vkládání, aktualizaci a odstraňování dat. Tyto uložené procedury lze zobrazit nebo upravit pomocí sady Visual Studio tak, že na Průzkumník serveru zahájíte přechod do složky uložené procedury databáze. Jak ukazuje obrázek 12, databáze Northwind obsahuje čtyři nové uložené procedury: `Products_Delete`, `Products_Insert`, `Products_Select`a `Products_Update`.

![Čtyři uložené procedury vytvořené v kroku 2 najdete ve složce uložených procedur databáze s.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)

**Obrázek 12**: čtyři uložené procedury vytvořené v kroku 2 najdete ve složce uložených procedur databáze s.

> [!NOTE]
> Pokud se Průzkumník serveru nezobrazuje, přejděte do nabídky zobrazení a vyberte možnost Průzkumník serveru. Pokud se nezobrazí uložené procedury související s produktem přidané z kroku 2, zkuste kliknout pravým tlačítkem na složku uložené procedury a vybrat možnost aktualizovat.

Chcete-li zobrazit nebo upravit uloženou proceduru, dvakrát klikněte na její název v Průzkumník serveru nebo případně klikněte pravým tlačítkem na uloženou proceduru a vyberte možnost otevřít. Obrázek 13 ukazuje `Products_Delete` uloženou proceduru, když je otevřená.

[![uložené procedury lze otevřít a upravit v sadě Visual Studio](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png)

**Obrázek 13**: uložené procedury lze otevřít a upravit v rámci sady Visual Studio ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png)

Obsah uložených procedur `Products_Delete` i `Products_Select` je poměrně přímočarý. `Products_Insert` a `Products_Update` uložené procedury na druhé straně zaručí užší kontrolu, protože oba provádějí `SELECT` příkaz po jejich `INSERT` a `UPDATE`ch příkazů. Například následující SQL tvoří uloženou proceduru `Products_Insert`:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

Uložená procedura přijímá jako vstupní parametry `Products` sloupce, které byly vráceny dotazem `SELECT` uvedenými v průvodci TableAdapter s, a tyto hodnoty jsou použity v příkazu `INSERT`. Po použití příkazu `INSERT` se `SELECT` dotaz vrátí `Products` hodnoty sloupce (včetně `ProductID`) nově přidaného záznamu. Tato možnost aktualizace je užitečná při přidávání nového záznamu pomocí vzorce aktualizace dávky, protože automaticky aktualizuje nově přidané instance `ProductRow` `ProductID` vlastností s hodnotami automaticky zvýšenými na hodnoty přiřazené databází.

Tato funkce je znázorněna na následujícím kódu. Obsahuje `ProductsTableAdapter` a `ProductsDataTable` vytvořeny pro `NorthwindWithSprocs` typovou datovou sadu. Do databáze se přidá nový produkt vytvořením instance `ProductsRow`, zadáním jejich hodnot a voláním metody `Update` TableAdapter s předáním do `ProductsDataTable`. Interně, metoda TableAdapter s `Update` vytváří výčet `ProductsRow` instancí v předaném objektu DataTable (v tomto příkladu je pouze jedna, kterou jsme právě přidali), a provede příslušný příkaz INSERT, Update nebo DELETE. V tomto případě je spuštěna uložená procedura `Products_Insert`, která přidá nový záznam do tabulky `Products` a vrátí podrobnosti nově přidaného záznamu. Hodnota `ProductID` instance `ProductsRow` se pak aktualizuje. Po dokončení metody `Update` můžeme k nově přidanému `ProductID`mu záznamu přistupovat prostřednictvím vlastnosti `ProductsRow` s `ProductID`.

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.cs)]

Uložená procedura `Products_Update` podobně zahrnuje příkaz `SELECT` po svém příkazu `UPDATE`.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample7.sql)]

Všimněte si, že tato uložená procedura zahrnuje dva vstupní parametry `ProductID`: `@Original_ProductID` a `@ProductID`. Tato funkce umožňuje scénáře, kdy může být primární klíč změněn. Například v databázi zaměstnanců můžou jednotlivé záznamy zaměstnanců jako primární klíč používat číslo sociálního pojištění zaměstnance. Aby bylo možné změnit stávající číslo sociálního pojištění zaměstnance, je nutné zadat nové číslo sociálního pojištění i původní. V tabulce `Products` není tato funkce potřebná, protože sloupec `ProductID` je `IDENTITY` sloupec a neměl by být nikdy změněn. Ve skutečnosti příkaz `UPDATE` v uložené proceduře `Products_Update` nezahrnuje sloupec `ProductID` v seznamu sloupců. Takže zatímco `@Original_ProductID` se používá v klauzuli `UPDATE` Statement `WHERE`, je nadbytečné pro tabulku `Products` a je možné ji nahradit parametrem `@ProductID`. Při úpravách uložených procedur s parametrem je důležité, aby byly aktualizovány také metody TableAdapter, které používají tuto uloženou proceduru.

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>Krok 4: úprava parametrů uložené procedury s a aktualizace TableAdapter

Vzhledem k tomu, že parametr `@Original_ProductID` je nadbytečný, nechte ho z `Products_Update` uložené procedury odebrat úplně. Otevřete `Products_Update` uloženou proceduru, odstraňte parametr `@Original_ProductID` a v klauzuli `WHERE` příkazu `UPDATE` změňte název parametru používaný z `@Original_ProductID` na `@ProductID`. Po provedení těchto změn by měl T-SQL v rámci uložené procedury vypadat takto:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample8.sql)]

Chcete-li uložit tyto změny do databáze, klikněte na panelu nástrojů na ikonu Uložit nebo stiskněte klávesu CTRL + S. V tomto okamžiku `Products_Update` uložený postup neočekává `@Original_ProductID` vstupní parametr, ale TableAdapter je nakonfigurován tak, aby předával takový parametr. Můžete zobrazit parametry, které TableAdapter odešle `Products_Update` do uložené procedury, tak, že vyberete TableAdapter v Návrháři DataSet, přejdete na okno Vlastnosti a kliknete na tři tečky v kolekci `UpdateCommand` s `Parameters`. Tím se zobrazí dialogové okno Editor kolekcí parametrů zobrazené na obrázku 14.

![Editor kolekce Parameters obsahuje seznam parametrů použitých k předané uložené proceduře Products_Update](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png)

**Obrázek 14**: Editor kolekce parametrů obsahuje seznam parametrů použitých předaných do uložené procedury `Products_Update`

Tento parametr můžete z tohoto parametru odebrat pouhým výběrem parametru `@Original_ProductID` ze seznamu členů a kliknutím na tlačítko Odebrat.

Alternativně můžete aktualizovat parametry používané pro všechny metody tak, že kliknete pravým tlačítkem na TableAdapter v návrháři a zvolíte konfigurovat. Tím se zobrazí Průvodce konfigurací TableAdapter, v němž jsou uvedeny uložené procedury používané pro výběr, vložení, aktualizaci a odstranění, spolu s parametry, které očekávají uložené procedury. Pokud kliknete na rozevírací seznam aktualizace, vidíte `Products_Update` uložené procedury očekávaly vstupní parametry, které už nezahrnují `@Original_ProductID` (viz obrázek 15). Stačí kliknout na tlačítko Dokončit a automaticky aktualizovat kolekci parametrů, kterou používá TableAdapter.

[![můžete alternativně aktualizovat kolekce parametrů metod pomocí Průvodce konfigurací nástroje TableAdapter s](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**Obrázek 15**: Alternativně můžete použít Průvodce konfigurací TableAdapter s k aktualizaci kolekcí parametrů metod ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png)

## <a name="step-5-adding-additional-tableadapter-methods"></a>Krok 5: Přidání dalších metod TableAdapter

Jak je znázorněno v kroku 2, při vytváření nového TableAdapter je snadné automaticky vygenerovat odpovídající uložené procedury. Totéž platí při přidávání dalších metod do TableAdapter. K tomu je potřeba přidat metodu `GetProductByProductID(productID)` do `ProductsTableAdapter` vytvořené v kroku 2. Tato metoda povede jako vstup `ProductID` hodnoty a vrátí podrobnosti o zadaném produktu.

Začněte tím, že kliknete pravým tlačítkem na TableAdapter a zvolíte přidat dotaz z kontextové nabídky.

![Přidat nový dotaz do TableAdapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**Obrázek 16**: Přidání nového dotazu do TableAdapter

Tím se spustí Průvodce konfigurací dotazu TableAdapter, který nejprve vyzve k tomu, jak má TableAdapter mít přístup k databázi. Chcete-li vytvořit novou uloženou proceduru, vyberte možnost vytvořit novou uloženou proceduru a klikněte na tlačítko Další.

[![zvolit možnost vytvořit novou uloženou proceduru](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)

**Obrázek 17**: Volba možnosti vytvořit novou uloženou proceduru ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png))

Na další obrazovce se dozvíte, jak identifikovat typ dotazu, který se má provést, zda vrátí sadu řádků nebo jednu skalární hodnotu nebo proveďte příkaz `UPDATE`, `INSERT`nebo `DELETE`. Vzhledem k tomu, že metoda `GetProductByProductID(productID)` Vrátí řádek, ponechte vybranou možnost vybrat, která vrátí řádek a stiskněte tlačítko Další.

[![zvolte možnost vybrat, která vrátí řádek.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)

**Obrázek 18**: zvolte možnost vybrat, která vrátí řádek ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png)).

Na další obrazovce se zobrazí hlavní dotaz TableAdapter s, který přesně vypíše název uložené procedury (`dbo.Products_Select`). Nahraďte název uložené procedury následujícím příkazem `SELECT`, který vrátí všechna pole produktu pro určitý produkt:

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample9.sql)]

[![nahradit název uložené procedury dotazem SELECT](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)

**Obrázek 19**: nahraďte název uložené procedury `SELECT` dotazem ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png)

Na další obrazovce se zobrazí výzva, abyste pojmenovat uloženou proceduru, která se vytvoří. Zadejte název `Products_SelectByProductID` a klikněte na tlačítko Další.

[![pojmenovat novou uloženou proceduru Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**Obrázek 20**: Pojmenujte novou uloženou proceduru `Products_SelectByProductID` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image46.png)

Poslední krok průvodce umožňuje změnit vygenerované názvy metod a také určit, jestli se má použít vzor naplnit jako DataTable, vracet vzor DataTable nebo obojí. Pro tuto metodu ponechte zaškrtnuté obě možnosti, ale přejmenujte metody na `FillByProductID` a `GetProductByProductID`. Kliknutím na Další Zobrazte souhrnné informace o krocích, které průvodce provede, a kliknutím na Dokončit dokončete průvodce.

[![přejmenovat metody TableAdapter s na FillByProductID a GetProductByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image47.png)

**Obrázek 21**: Přejmenujte metody TableAdapter s na `FillByProductID` a `GetProductByProductID` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image49.png)

Po dokončení průvodce bude mít TableAdapter k dispozici novou metodu, `GetProductByProductID(productID)`, která při vyvolání spustí `Products_SelectByProductID` uloženou proceduru, která byla právě vytvořena. Chvíli počkejte, než se tato nová úložná procedura zobrazí z Průzkumník serveru tím, že se podělíte do složky uložené procedury a otevřete `Products_SelectByProductID` (pokud ji nevidíte, kliknete pravým tlačítkem na složku uložené procedury a zvolíte aktualizovat).

Všimněte si, že `SelectByProductID` uložená procedura má `@ProductID` jako vstupní parametr a spustí příkaz `SELECT`, který jsme zadali v průvodci.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>Krok 6: vytvoření třídy vrstvy obchodní logiky

V rámci řady kurzů jsme se rozhodli zachovat vrstvenou architekturu, ve které prezentační vrstva provedla všechna volání do vrstvy obchodní logiky (knihoven BLL). Aby bylo možné dodržovat toto rozhodnutí o návrhu, nejprve je nutné vytvořit třídu knihoven BLL pro novou typovou datovou sadu předtím, než bude možné získat přístup k datům produktu z prezentační vrstvy.

Vytvořte nový soubor třídy s názvem `ProductsBLLWithSprocs.cs` ve složce `~/App_Code/BLL` a přidejte do něj následující kód:

[!code-csharp[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample11.cs)]

Tato třída napodobuje sémantiku `ProductsBLL` třídy z předchozích kurzů, ale používá objekty `ProductsTableAdapter` a `ProductsDataTable` z datové sady `NorthwindWithSprocs`. Například nemusíte mít příkaz `using NorthwindTableAdapters` na začátku souboru třídy jako `ProductsBLL`, třída `ProductsBLLWithSprocs` používá `using NorthwindWithSprocsTableAdapters`. Podobně jsou objekty `ProductsDataTable` a `ProductsRow` použité v této třídě předpony s oborem názvů `NorthwindWithSprocs`. Třída `ProductsBLLWithSprocs` poskytuje dvě metody přístupu k datům, `GetProducts` a `GetProductByProductID`a metody pro přidání, aktualizaci a odstranění jedné instance produktu.

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>Krok 7: práce s`NorthwindWithSprocs`datovou sadou z prezentační vrstvy

V tuto chvíli jsme vytvořili DAL, který používá uložené procedury pro přístup k datům databáze a jejich úpravě. Také jsme vytvořili základní knihoven BLL s metodami pro načtení všech produktů nebo konkrétního produktu spolu s metodami pro přidávání, aktualizování a odstraňování produktů. Pokud chcete tento kurz zaokrouhlit, vytvoříme stránku ASP.NET, která pro zobrazení, aktualizaci a mazání záznamů používá `ProductsBLLWithSprocs` třídy knihoven BLL s.

Otevřete stránku `NewSprocs.aspx` ve složce `AdvancedDAL` a přetáhněte prvek GridView z panelu nástrojů do návrháře a pojmenujte jej `Products`. Z inteligentní značky GridView. Vyberte, že se má vytvořit vazba s novým prvkem ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby používal třídu `ProductsBLLWithSprocs`, jak je znázorněno na obrázku 22.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLLWithSprocs](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image50.png)

**Obrázek 22**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLLWithSprocs` ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image52.png))

Rozevírací seznam na kartě vybrat má dvě možnosti `GetProducts` a `GetProductByProductID`. Vzhledem k tomu, že chceme Zobrazit všechny produkty v prvku GridView, vyberte metodu `GetProducts`. Rozevírací seznamy na kartách aktualizace, vložení a odstranění obsahují pouze jednu metodu. Zajistěte, aby u každého z těchto rozevíracích seznamů byla zvolena odpovídající metoda, a potom klikněte na tlačítko Dokončit.

Po dokončení průvodce ObjectDataSource bude Visual Studio přidávat BoundFields a třídě CheckBoxField podporována do prvku GridView pro pole dat produktu. Zapněte integrované úpravy a odstraňování funkcí prvku GridView. zaškrtnutím možnosti Povolit úpravy a povolit odstraňování možností, které jsou k dispozici v inteligentní značce.

[![stránka obsahuje prvek GridView s povolenou úpravou a odstraněním podpory](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image53.png)

**Obrázek 23**: stránka obsahuje prvek GridView s povolenou úpravou a odstraněním podpory ([kliknutím zobrazíte obrázek v plné velikosti).](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image55.png)

Jak jsme probrali v předchozích kurzech, po dokončení průvodce ObjectDataSource s sada Visual Studio nastaví vlastnost `OldValuesParameterFormatString` na původní\_{0}. Tato hodnota se musí vrátit na výchozí hodnotu {0}, aby funkce změny dat správně fungovaly podle parametrů očekávaných metodami v našem knihoven BLL. Proto nezapomeňte nastavit vlastnost `OldValuesParameterFormatString` na {0} nebo odebrat vlastnost zcela z deklarativní syntaxe.

Po dokončení Průvodce konfigurací zdroje dat zapněte úpravy a odstranění podpory v prvku GridView a vraťte vlastnost ObjectDataSource s `OldValuesParameterFormatString` na její výchozí hodnotu, deklarativní označení stránky by mělo vypadat podobně jako následující:

[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample12.aspx)]

V tuto chvíli jsme mohli uklizenýovat prvek GridView přizpůsobením rozhraní pro úpravy, aby zahrnovalo ověřování, aby se sloupce `CategoryID` a `SupplierID` vykreslily jako DropDownList a tak dále. Na tlačítko Odstranit můžeme také přidat potvrzení na straně klienta a doporučujeme vám, abyste si mohli při implementaci těchto vylepšení vyučinit čas. Vzhledem k tomu, že tato témata jsou popsaná v předchozích kurzech, ale nebudeme se tady pokrývat.

Bez ohledu na to, zda vylepšíte prvek GridView nebo not, otestujte základní funkce stránky v prohlížeči. Jak ukazuje obrázek 24, stránka obsahuje seznam produktů v prvku GridView, které poskytují možnosti pro úpravu a odstranění řádků.

[![produktů lze zobrazit, upravit a odstranit z prvku GridView.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image56.png)

**Obrázek 24**: produkty si můžete zobrazit, upravit a odstranit z prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image58.png)).

## <a name="summary"></a>Souhrn

Objekty TableAdapter ve typované datové sadě má přístup k datům z databáze pomocí ad-hoc příkazů SQL nebo prostřednictvím uložených procedur. Při práci s uloženými postupy lze použít buď existující uložené procedury, nebo Průvodce TableAdapter vytvořit nové uložené procedury na základě dotazu `SELECT`. V tomto kurzu jsme se seznámili s tím, jak se pro nás automaticky vytvoří uložené procedury.

I když se automaticky vygenerované uložené procedury pomáhají ušetřit čas, existují určité případy, kdy úložná procedura vytvořená Průvodcem nezpůsobí zarovnání k tomu, co jsme vytvořili sami. Jedním z příkladů je `Products_Update` uložený postup, který očekával vstupní parametry `@Original_ProductID` a `@ProductID`, i když byl parametr `@Original_ProductID` nadbytečný.

V mnoha scénářích už jsou uložené procedury už vytvořené nebo je můžeme chtít vytvořit ručně, aby bylo možné ovládat příkazy uložené procedury s jemnějším stupněm řízení. V obou případech chceme, aby TableAdapter používal existující uložené procedury pro své metody. V dalším kurzu se naučíme, jak to provést.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Vytváření a údržba uložených procedur](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [Načítání skalárních dat z uložené procedury](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [Základy uložených procedur SQL Server](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [Uložené procedury: Přehled](http://www.sqlteam.com/item.asp?ItemID=563)
- [Zápis uložené procedury](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Geisenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
