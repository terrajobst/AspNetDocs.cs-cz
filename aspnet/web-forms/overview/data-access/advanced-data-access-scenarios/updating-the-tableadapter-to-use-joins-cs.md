---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
title: Aktualizace TableAdapter pro použití spojení (C#) | Microsoft Docs
author: rick-anderson
description: Při práci s databází je běžné požadovat data, která jsou rozdělená mezi několik tabulek. Pro načtení dat ze dvou různých tabulek můžeme použít buď...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 675531a7-cb54-4dd6-89ac-2636e4c285a5
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
msc.type: authoredcontent
ms.openlocfilehash: 24ff3645783dabfcdef5ac313a2d4833e4998efc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607855"
---
# <a name="updating-the-tableadapter-to-use-joins-c"></a>Aktualizace komponenty TableAdapter kvůli použití příkazů JOIN (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_CS.zip) nebo [stažení PDF](updating-the-tableadapter-to-use-joins-cs/_static/datatutorial69cs1.pdf)

> Při práci s databází je běžné požadovat data, která jsou rozdělená mezi několik tabulek. K načtení dat ze dvou různých tabulek můžeme použít buď korelační poddotaz, nebo operaci JOIN. V tomto kurzu porovnáváme korelační poddotazy a syntaxi spojení před zobrazením postupu vytvoření TableAdapter, který obsahuje spojení v jeho hlavním dotazu.

## <a name="introduction"></a>Úvod

V případě relačních databází se data, se kterými se snažíme pracovat, často rozcházejí mezi několik tabulek. Pokud například zobrazíte informace o produktu, Seznamte se s informacemi o odpovídajících kategoriích a dodavatelích v jednotlivých produktech. Tabulka `Products` obsahuje hodnoty `CategoryID` a `SupplierID`, ale skutečná kategorie a názvy dodavatelů jsou v `Categories` a `Suppliers`ch tabulkách v uvedeném pořadí.

Pokud chcete načíst informace z jiné související tabulky, můžeme použít *korelační poddotazy* nebo `JOIN`*s*. Korelační poddotaz je vnořený `SELECT` dotaz, který odkazuje na sloupce ve vnějším dotazu. Například v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-cs.md) jsme použili dva korelační poddotazy v hlavním dotazu `ProductsTableAdapter` s k vrácení názvů kategorií a dodavatelů pro každý produkt. `JOIN` je konstrukce SQL, která slučuje související řádky ze dvou různých tabulek. Při [dotazování dat pomocí ovládacího prvku SqlDataSource](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs.md) jsme použili `JOIN` k zobrazení informací o kategorii společně s každým produktem.

Důvodem, proč jsme abstainedi použití `JOIN` s s objekty TableAdapter, je z důvodu omezení v průvodci TableAdapterou pro automatické generování odpovídajících příkazů `INSERT`, `UPDATE`a `DELETE`. Pokud hlavní dotaz TableAdapter s obsahuje nějaké `JOIN` s, TableAdapter nemůže automaticky vytvořit ad-hoc příkazy SQL nebo uložené procedury pro své `InsertCommand`, `UpdateCommand`a `DeleteCommand` vlastnosti.

V tomto kurzu stručně porovnáme a narovnejte korelační poddotazy a `JOIN` s a teprve potom Prozkoumejte, jak vytvořit TableAdapter, který zahrnuje `JOIN` s v hlavním dotazu.

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>Porovnávání a kontrast u korelačních poddotazů a`JOIN` s

Odvolat, že `ProductsTableAdapter` vytvořená v prvním kurzu v datové sadě `Northwind` používá korelační poddotazy k vrácení všech odpovídajících kategorií produktů a názvu dodavatele v souvislosti s nimi. Hlavní dotaz `ProductsTableAdapter` s je uveden níže.

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample1.sql)]

Dva korelační poddotazy – `(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` a `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)` – jsou `SELECT` dotazy, které vracejí jednu hodnotu na produkt jako další sloupec v seznamu vnějších `SELECT` příkazů s.

Alternativně můžete `JOIN` použít k vrácení každého dodavatele produktu a názvu kategorie. Následující dotaz vrátí stejný výstup jako ten, ale používá `JOIN` s místo poddotazů:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample2.sql)]

`JOIN` sloučí záznamy z jedné tabulky s záznamy z jiné tabulky na základě některých kritérií. Ve výše uvedeném dotazu například `LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` instruuje SQL Server ke sloučení každého záznamu produktu s záznamem kategorie, jehož `CategoryID` hodnota odpovídá hodnotě `CategoryID` produktu s. Sloučený výsledek umožňuje pracovat s odpovídajícími poli kategorií pro každý produkt (například `CategoryName`).

> [!NOTE]
> `JOIN` s se běžně používají při dotazování dat z relačních databází. Pokud se syntaxí `JOIN` nepoužíváte nebo potřebujete na svém využití štětce, doporučujeme vám I v [kurzu spojení SQL](http://www.w3schools.com/sql/sql_join.asp) na [w3 školách](http://www.w3schools.com/). Pro čtení jsou také [`JOIN` základy](https://msdn.microsoft.com/library/ms191517.aspx) a [poddotazování](https://msdn.microsoft.com/library/ms189575.aspx) v sekcích [SQL Books Online](https://msdn.microsoft.com/library/ms130214.aspx).

Vzhledem k tomu, že `JOIN` s a korelační poddotazy lze použít k načtení souvisejících dat z jiných tabulek, mnoho vývojářů si ponechá své hlavy a zajímá, jaký přístup k použití. Všechny SQL Gurus I v mluvili mají zhruba stejnou věc, že nestačí pro výkon, protože SQL Server vytvoří zhruba totožné plány provádění. Jejich doporučení a pak je použít techniku, se kterou jste vy a váš tým nejvíc cítí. Znamená to, že po zaznamenání těchto rad ihned tyto odborníky vyjádří své preference `JOIN` s prostřednictvím korelačních poddotazů.

Při sestavování vrstvy přístupu k datům pomocí zadaných datových sad nástroje fungují lépe při použití poddotazů. Konkrétně Průvodce TableAdapterem nebude automaticky generovat odpovídající příkazy `INSERT`, `UPDATE`a `DELETE`, pokud hlavní dotaz obsahuje jakékoli `JOIN`, ale tyto příkazy automaticky vygeneruje při použití korelačních poddotazů.

Chcete-li tyto nedostatky prozkoumat, vytvořte v `~/App_Code/DAL` složce dočasnou typovou datovou sadu. V Průvodci konfigurací TableAdapter se vyberte použít ad hoc příkazy SQL a zadejte následující dotaz `SELECT` (viz obrázek 1):

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample3.sql)]

[![zadejte hlavní dotaz, který obsahuje spojení.](updating-the-tableadapter-to-use-joins-cs/_static/image2.png)](updating-the-tableadapter-to-use-joins-cs/_static/image1.png)

**Obrázek 1**: Zadejte hlavní dotaz, který obsahuje `JOIN` s ([kliknutím zobrazíte obrázek v plné velikosti).](updating-the-tableadapter-to-use-joins-cs/_static/image3.png)

Ve výchozím nastavení bude TableAdapter automaticky vytvářet `INSERT`, `UPDATE`a `DELETE` příkazy založené na hlavním dotazu. Pokud kliknete na tlačítko Upřesnit, uvidíte, že je tato funkce povolená. Bez ohledu na toto nastavení TableAdapter nebude moci vytvořit příkazy `INSERT`, `UPDATE`a `DELETE`, protože hlavní dotaz obsahuje `JOIN`.

![Zadejte hlavní dotaz, který obsahuje spojení.](updating-the-tableadapter-to-use-joins-cs/_static/image4.png)

**Obrázek 2**: Zadejte hlavní dotaz, který obsahuje `JOIN` s.

Kliknutím na Dokončit dokončete průvodce. V tomto okamžiku Návrhář DataSet obsahuje jeden TableAdapter s DataTable se sloupci pro každé pole vrácené v seznamu sloupců `SELECT` dotazů s. To zahrnuje `CategoryName` a `SupplierName`, jak ukazuje obrázek 3.

![Objekt DataTable obsahuje sloupec pro každé pole vrácené v seznamu sloupců.](updating-the-tableadapter-to-use-joins-cs/_static/image5.png)

**Obrázek 3**: objekt DataTable obsahuje sloupec pro každé pole vrácené v seznamu sloupců.

I když má objekt DataTable příslušné sloupce, nemá TableAdapter hodnoty pro jeho `InsertCommand`, `UpdateCommand`a vlastnosti `DeleteCommand`. Potvrďte to tak, že kliknete na TableAdapter v návrháři a pak přejdete na okno Vlastnosti. Uvidíte, že vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand` jsou nastavené na hodnotu (žádné).

[![vlastností InsertCommand, UpdateCommand a DeleteCommand jsou nastavené na (žádné).](updating-the-tableadapter-to-use-joins-cs/_static/image7.png)](updating-the-tableadapter-to-use-joins-cs/_static/image6.png)

**Obrázek 4**: vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand` jsou nastaveny na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti).](updating-the-tableadapter-to-use-joins-cs/_static/image8.png)

Pokud chcete tento problém obejít, můžeme ručně zadat příkazy a parametry SQL pro vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand` prostřednictvím okno Vlastnosti. Alternativně můžeme začít konfigurací hlavního dotazu *TableAdapter s, aby* neobsahoval žádné `JOIN` s. Tím umožníte, aby se příkazy `INSERT`, `UPDATE`a `DELETE` automaticky vygenerovaly pro nás. Po dokončení průvodce můžeme ručně aktualizovat `SelectCommand` TableAdapter s z okno Vlastnosti tak, aby obsahovaly syntaxi `JOIN`.

I když tento přístup funguje, je velmi poměrně křehký při použití ad-hoc dotazů SQL, protože pokaždé, když je hlavní dotaz TableAdapter. znovu nakonfigurován prostřednictvím průvodce, jsou znovu vytvořeny automaticky generované `INSERT`, `UPDATE`a `DELETE` příkazy. To znamená, že při kliknutí pravým tlačítkem na TableAdapter, zvolením možnosti konfigurovat z místní nabídky by došlo ke ztrátě všech úprav, které jsme později udělali, a pak průvodce znovu dokončil.

Brittleness automaticky generovaných příkazů `INSERT`, `UPDATE`a `DELETE` jsou naštěstí omezené na příkazy SQL ad hoc. Pokud vaše TableAdapter používá uložené procedury, můžete přizpůsobit uložené procedury `SelectCommand`, `InsertCommand`, `UpdateCommand`nebo `DeleteCommand` a znovu spustit Průvodce konfigurací TableAdapter bez obav, že uložené procedury budou upraveny.

V několika dalších krocích vytvoříme TableAdapter, který zpočátku používá hlavní dotaz, který vynechává jakékoli `JOIN` s, aby se automaticky vygenerovaly odpovídající uložené procedury INSERT, Update a DELETE. Pak aktualizujeme `SelectCommand` tak, aby používala `JOIN`, která vrací další sloupce ze souvisejících tabulek. Nakonec vytvoříme odpovídající třídu vrstvy obchodní logiky a ukážeme použití TableAdapter na webové stránce ASP.NET.

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>Krok 1: vytvoření TableAdapter pomocí zjednodušeného hlavního dotazu

Pro tento kurz přidáme TableAdapter a silně typované DataTable pro tabulku `Employees` v datové sadě `NorthwindWithSprocs`. Tabulka `Employees` obsahuje pole `ReportsTo`, které zadal `EmployeeID` manažera pro zaměstnance. Například zaměstnanec Anne veselé má `ReportTo` hodnotu 5, což je `EmployeeID` Steven Novák. V důsledku toho Anne sestavy do Steven, jejího manažera. Společně s vytvářením sestav o `ReportsTo` hodnotě v jednotlivých zaměstnancích můžete také chtít načíst název svého nadřízeného. To lze provést pomocí `JOIN`. Při počátečním vytváření TableAdapter ale pomocí `JOIN` nevylučuje Průvodce automatické generování odpovídajících možností vložení, aktualizace a odstranění. Proto začneme vytvořením TableAdapter, jehož hlavní dotaz neobsahuje žádné `JOIN` s. Potom v kroku 2 aktualizujeme hlavní uloženou proceduru dotazu, aby se načetl název správce s pomocí `JOIN`.

Začněte tím, že otevřete `NorthwindWithSprocs` datovou sadu ve složce `~/App_Code/DAL`. Klikněte pravým tlačítkem myši na návrháře, v místní nabídce vyberte možnost Přidat a vyberte položku nabídky TableAdapter. Tím se spustí Průvodce konfigurací TableAdapter. Obrázek 5 znázorňuje, že Průvodce vytvoří nové uložené procedury a klikne na tlačítko Další. Chcete-li aktualizovat informace o vytváření nových uložených procedur pomocí Průvodce TableAdapterem, Projděte si kurz [vytváření nových uložených procedur pro objekty TableAdapter typované sady dat](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) .

[![vyberte možnost vytvořit nové uložené procedury.](updating-the-tableadapter-to-use-joins-cs/_static/image10.png)](updating-the-tableadapter-to-use-joins-cs/_static/image9.png)

**Obrázek 5**: vyberte možnost vytvořit nové uložené procedury ([kliknutím zobrazíte obrázek v plné velikosti](updating-the-tableadapter-to-use-joins-cs/_static/image11.png)).

Pro hlavní dotaz TableAdapter s použijte následující příkaz `SELECT`:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample4.sql)]

Vzhledem k tomu, že tento dotaz neobsahuje žádné `JOIN` s, Průvodce TableAdapter automaticky vytvoří uložené procedury s odpovídajícími příkazy `INSERT`, `UPDATE`a `DELETE`, jakož i uloženou proceduru pro spuštění hlavního dotazu.

Následující krok umožňuje pojmenovat uložené procedury TableAdapter s. Použijte názvy `Employees_Select`, `Employees_Insert`, `Employees_Update`a `Employees_Delete`, jak je znázorněno na obrázku 6.

[![TableAdapter s uloženými procedurami](updating-the-tableadapter-to-use-joins-cs/_static/image13.png)](updating-the-tableadapter-to-use-joins-cs/_static/image12.png)

**Obrázek 6**: pojmenujte uložené procedury TableAdapter s ([kliknutím zobrazíte obrázek v plné velikosti](updating-the-tableadapter-to-use-joins-cs/_static/image14.png)).

Poslední krok vás vyzve k pojmenování metod TableAdapter s. Jako názvy metod použijte `Fill` a `GetEmployees`. Nezapomeňte také nechat zaškrtávací políčko vytvořit metody pro odeslání aktualizací přímo do databáze (GenerateDBDirectMethods).

[![pojmenovat metody TableAdapter s a GetEmployees](updating-the-tableadapter-to-use-joins-cs/_static/image16.png)](updating-the-tableadapter-to-use-joins-cs/_static/image15.png)

**Obrázek 7**: pojmenování metod TableAdapter s `Fill` a `GetEmployees` ([kliknutím zobrazíte obrázek v plné velikosti](updating-the-tableadapter-to-use-joins-cs/_static/image17.png))

Po dokončení průvodce chvíli počkejte, než se prohledá uložené procedury v databázi. Měli byste vidět čtyři nové: `Employees_Select`, `Employees_Insert`, `Employees_Update`a `Employees_Delete`. Potom zkontrolujte `EmployeesDataTable` a `EmployeesTableAdapter` právě vytvořené. Objekt DataTable obsahuje sloupec pro každé pole vrácené hlavním dotazem. Klikněte na TableAdapter a potom přejděte na okno Vlastnosti. Uvidíte, že vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand` jsou správně nakonfigurované pro volání odpovídajících uložených procedur.

[![TableAdapter zahrnuje možnosti vložení, aktualizace a odstranění.](updating-the-tableadapter-to-use-joins-cs/_static/image19.png)](updating-the-tableadapter-to-use-joins-cs/_static/image18.png)

**Obrázek 8**: TableAdapter zahrnuje možnosti vložení, aktualizace a odstranění ([kliknutím zobrazíte obrázek v plné velikosti](updating-the-tableadapter-to-use-joins-cs/_static/image20.png)).

Když se automaticky vytvoří uložené, aktualizovat a odstranit uložené procedury a správně nakonfigurované vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand`, je připraveno přizpůsobit uloženou proceduru `SelectCommand` s, aby vracela Další informace o manažerovi s pracovníkem. Konkrétně je potřeba aktualizovat uloženou proceduru `Employees_Select` tak, aby používala `JOIN`, a vracet `FirstName` a `LastName` hodnoty Manageru. Po aktualizaci uložené procedury bude nutné aktualizovat DataTable tak, aby obsahovala tyto další sloupce. Tyto dvě úlohy budeme řešit v krocích 2 a 3.

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>Krok 2: přizpůsobení uložené procedury tak, aby zahrnovala`JOIN`

Začněte tím, že na Průzkumník serveru zahájíte přechod do složky uložené procedury databáze Northwind a otevřete `Employees_Select` uloženou proceduru. Pokud tuto uloženou proceduru nevidíte, klikněte pravým tlačítkem na složku uložené procedury a vyberte aktualizovat. Aktualizujte uloženou proceduru tak, aby používala `LEFT JOIN` k vrácení jména a příjmení manažera:

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample5.sql)]

Po aktualizaci příkazu `SELECT` uložte změny tak, že v nabídce soubor kliknete na možnost Uložit `Employees_Select`. Případně můžete kliknout na ikonu Uložit na panelu nástrojů nebo stisknout CTRL + S. Po uložení změn klikněte pravým tlačítkem na `Employees_Select` uloženou proceduru v Průzkumník serveru a vyberte spustit. Tato akce spustí uloženou proceduru a zobrazí její výsledky v okně výstup (viz obrázek 9).

[![výsledky uložených procedur se zobrazí v okno Výstup](updating-the-tableadapter-to-use-joins-cs/_static/image22.png)](updating-the-tableadapter-to-use-joins-cs/_static/image21.png)

**Obrázek 9**: výsledky uložených procedur se zobrazí v okno výstup ([kliknutím zobrazíte obrázek v plné velikosti).](updating-the-tableadapter-to-use-joins-cs/_static/image23.png)

## <a name="step-3-updating-the-datatable-s-columns"></a>Krok 3: aktualizace sloupců DataTable s

V tomto okamžiku `Employees_Select` uložená procedura vrací `ManagerFirstName` a `ManagerLastName` hodnoty, ale v `EmployeesDataTable` chybí tyto sloupce. Tyto chybějící sloupce lze přidat do objektu DataTable jedním ze dvou způsobů:

- **Ručně** klikněte pravým tlačítkem na DataTable v Návrháři DataSet a v nabídce Přidat vyberte sloupec. Potom můžete sloupec pojmenovat a nastavit jeho vlastnosti odpovídajícím způsobem.
- **Automaticky** – Průvodce konfigurací TableAdapter aktualizuje sloupce DataTable s tak, aby odrážely pole vrácená `SelectCommand` uloženou procedurou. Při použití příkazů SQL ad hoc Průvodce odebere taky `InsertCommand`, `UpdateCommand`a `DeleteCommand` vlastnosti, protože `SelectCommand` teď obsahuje `JOIN`. Při použití uložených procedur ale tyto vlastnosti příkazu zůstanou beze změn.

V předchozích kurzech jsme prozkoumali Ruční přidávání sloupců DataTable, včetně [hlavní položky a podrobností pomocí seznamu hlavních záznamů s odrážkami s podrobnostmi](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) a [nahráním souborů](../working-with-binary-files/uploading-files-cs.md). v našem dalším kurzu se tento proces znovu podíváme podrobněji. Pro tento kurz ale použijte automatický přístup prostřednictvím Průvodce konfigurací TableAdapter.

Začněte tím, že kliknete pravým tlačítkem na `EmployeesTableAdapter` a v místní nabídce vyberete konfigurovat. Tím se zobrazí Průvodce konfigurací TableAdapter, který obsahuje uložené procedury používané pro výběr, vložení, aktualizaci a odstranění, spolu s jejich návratovými hodnotami a parametry (pokud existují). Obrázek 10 ukazuje tohoto průvodce. Tady vidíte, že `Employees_Select` uložená procedura teď vrací pole `ManagerFirstName` a `ManagerLastName`.

[![Průvodce zobrazí aktualizovaný seznam sloupců pro uloženou proceduru Employees_Select](updating-the-tableadapter-to-use-joins-cs/_static/image25.png)](updating-the-tableadapter-to-use-joins-cs/_static/image24.png)

**Obrázek 10**: Průvodce zobrazí aktualizovaný seznam sloupců pro uloženou proceduru `Employees_Select` ([kliknutím zobrazíte obrázek v plné velikosti).](updating-the-tableadapter-to-use-joins-cs/_static/image26.png)

Dokončete průvodce kliknutím na tlačítko Dokončit. Po návratu do návrháře DataSet `EmployeesDataTable` obsahuje dva další sloupce: `ManagerFirstName` a `ManagerLastName`.

[![EmployeesDataTable obsahuje dva nové sloupce.](updating-the-tableadapter-to-use-joins-cs/_static/image28.png)](updating-the-tableadapter-to-use-joins-cs/_static/image27.png)

**Obrázek 11**: `EmployeesDataTable` obsahuje dva nové sloupce ([kliknutím zobrazíte obrázek v plné velikosti](updating-the-tableadapter-to-use-joins-cs/_static/image29.png)).

K ilustraci, že je v platnosti aktualizovaný `Employees_Select` uložená procedura a že funkce INSERT, Update a DELETE TableAdapter jsou pořád funkční, umožňuje vytvořit webovou stránku, která uživatelům umožní zobrazit a odstranit zaměstnance. Předtím, než vytvoříme takovou stránku, musíme nejdřív vytvořit novou třídu v rámci vrstvy obchodní logiky pro práci s zaměstnanci z `NorthwindWithSprocs` datové sady. V kroku 4 vytvoříme třídu `EmployeesBLLWithSprocs`. V kroku 5 budeme tuto třídu používat ze stránky ASP.NET.

## <a name="step-4-implementing-the-business-logic-layer"></a>Krok 4: implementace vrstvy obchodní logiky

Vytvořte nový soubor třídy ve složce `~/App_Code/BLL` s názvem `EmployeesBLLWithSprocs.cs`. Tato třída napodobuje sémantiku existující třídy `EmployeesBLL`, pouze tento nový poskytuje méně metod a používá `NorthwindWithSprocs` datovou sadu (místo datové sady `Northwind`). Do třídy `EmployeesBLLWithSprocs` přidejte následující kód.

[!code-csharp[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample6.cs)]

Vlastnost `EmployeesBLLWithSprocs` třídy s `Adapter` vrací instanci `EmployeesTableAdapter``NorthwindWithSprocs` DataSet s. Používá se pro `GetEmployees` třídy a metody `DeleteEmployee`. Metoda `GetEmployees` volá `EmployeesTableAdapter` odpovídající metodu `GetEmployees`, která vyvolá uloženou proceduru `Employees_Select` a naplní její výsledky v `EmployeeDataTable`. Metoda `DeleteEmployee` podobně volá metodu `Delete` `EmployeesTableAdapter` s, která vyvolá `Employees_Delete` uloženou proceduru.

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>Krok 5: práce s daty v prezentační vrstvě

Po dokončení `EmployeesBLLWithSprocs` třídy jsme znovu připraveni pracovat s daty zaměstnanců prostřednictvím stránky ASP.NET. Otevřete stránku `JOINs.aspx` ve složce `AdvancedDAL` a přetáhněte prvek GridView z panelu nástrojů do návrháře a nastavte jeho vlastnost `ID` na `Employees`. Potom z inteligentní značky GridView s navažte mřížku k novému ovládacímu prvku ObjectDataSource s názvem `EmployeesDataSource`.

Nakonfigurujte prvek ObjectDataSource tak, aby používal třídu `EmployeesBLLWithSprocs` a na kartách SELECT a DELETE se ujistěte, že jsou v rozevíracích seznamech vybrány metody `GetEmployees` a `DeleteEmployee`. Kliknutím na Dokončit dokončete konfiguraci ObjectDataSource s.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu EmployeesBLLWithSprocs](updating-the-tableadapter-to-use-joins-cs/_static/image31.png)](updating-the-tableadapter-to-use-joins-cs/_static/image30.png)

**Obrázek 12**: Konfigurace prvku ObjectDataSource, aby používal třídu `EmployeesBLLWithSprocs` ([kliknutím zobrazíte obrázek v plné velikosti](updating-the-tableadapter-to-use-joins-cs/_static/image32.png))

[![mají ObjectDataSource použít metody GetEmployees a DeleteEmployee](updating-the-tableadapter-to-use-joins-cs/_static/image34.png)](updating-the-tableadapter-to-use-joins-cs/_static/image33.png)

**Obrázek 13**: v prvku ObjectDataSource použijte metody `GetEmployees` a `DeleteEmployee` ([kliknutím zobrazíte obrázek v plné velikosti](updating-the-tableadapter-to-use-joins-cs/_static/image35.png)).

Visual Studio přidá do prvku GridView vlastnost BoundField pro každý sloupec `EmployeesDataTable` s. Odeberte všechny tyto BoundFields s výjimkou `Title`, `LastName`, `FirstName`, `ManagerFirstName`a `ManagerLastName` a přejmenujte `HeaderText` vlastnosti pro poslední čtyři BoundFields na příjmení, jméno, správce s křestní jméno a správce s příjmení, v uvedeném pořadí.

Pokud chcete uživatelům povolit odstranění zaměstnanců z této stránky, musíme udělat dvě věci. Nejdřív dejte pokyn prvku GridView, aby poskytoval možnosti odstranění, a to zaškrtnutím možnosti Povolit odstranění z inteligentní značky. Potom změňte vlastnost ObjectDataSource s `OldValuesParameterFormatString` z hodnoty nastavené průvodcem ObjectDataSource (`original_{0}`) na jeho výchozí hodnotu (`{0}`). Po provedení těchto změn by deklarativní značky GridView a ObjectDataSource s měly vypadat podobně jako následující:

[!code-aspx[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample7.aspx)]

Otestujte stránku tím, že na ni navštívíte přes prohlížeč. Jak ukazuje obrázek 14, na stránce se zobrazí seznam všech zaměstnanců a jejich název manažera (za předpokladu, že mají jednu).

[![spojení v uložené proceduře Employees_Select vrátí název správce.](updating-the-tableadapter-to-use-joins-cs/_static/image37.png)](updating-the-tableadapter-to-use-joins-cs/_static/image36.png)

**Obrázek 14**: `JOIN` v uložené proceduře `Employees_Select` vrátí název správce s ([kliknutím zobrazíte obrázek v plné velikosti).](updating-the-tableadapter-to-use-joins-cs/_static/image38.png)

Kliknutím na tlačítko Odstranit spustíte pracovní postup odstranění, který má za následek provedení `Employees_Delete` uložené procedury. Pokus o `DELETE` příkaz v uložené proceduře se ale nezdařil z důvodu porušení omezení cizího klíče (viz obrázek 15). Konkrétně každý zaměstnanec má jeden nebo více záznamů v tabulce `Orders`, což způsobí selhání odstranění.

[![odstranění zaměstnance, který má odpovídající objednávky, má za následek porušení omezení cizího klíče.](updating-the-tableadapter-to-use-joins-cs/_static/image40.png)](updating-the-tableadapter-to-use-joins-cs/_static/image39.png)

**Obrázek 15**: odstranění zaměstnance, který má odpovídající objednávky, má za následek porušení omezení cizího klíče ([kliknutím zobrazíte obrázek v plné velikosti).](updating-the-tableadapter-to-use-joins-cs/_static/image41.png)

Aby bylo možné zaměstnance odstranit, můžete:

- Aktualizace omezení cizího klíče pro kaskádové odstranění
- Ručně odstraňte záznamy z `Orders` tabulky pro zaměstnance, které chcete odstranit, nebo
- Aktualizujte `Employees_Delete` uloženou proceduru tak, aby nejdřív před odstraněním záznamu `Employees` odstranila související záznamy z tabulky `Orders`. Tuto techniku jsme probrali v kurzu [použití existujících uložených procedur pro objekty TableAdapter typované datové sady](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) .

Tuto funkci mám jako cvičení pro čtenáře.

## <a name="summary"></a>Přehled

Při práci s relačními databázemi je běžné, že dotazy budou přijímat data z více souvisejících tabulek. Korelační poddotazy a `JOIN` s poskytují dvě různé techniky pro přístup k datům ze souvisejících tabulek v dotazu. V předchozích kurzech jsme nejčastěji používali korelační poddotazy, protože TableAdapter nemůže automaticky generovat příkazy `INSERT`, `UPDATE`a `DELETE` pro dotazy zahrnující `JOIN` s. I když je možné tyto hodnoty zadat ručně, při použití ad-hoc příkazů SQL budou po dokončení Průvodce konfigurací TableAdapter přepsány jakékoli vlastní nastavení.

Naštěstí objekty TableAdapter vytvořené pomocí uložených procedur netrpí stejnými brittleness, jako ty, které se vytvořily pomocí ad-hoc příkazů SQL. Proto je vhodné vytvořit TableAdapter, jehož hlavní dotaz používá při použití uložených procedur `JOIN`. V tomto kurzu jsme viděli, jak TableAdapter vytvořit. Zahájili jsme použití `SELECT`ho dotazu `JOIN`pro hlavní dotaz TableAdapter s, aby byly automaticky vytvořeny odpovídající uložené procedury INSERT, Update a DELETE. Po dokončení počáteční konfigurace TableAdapter jsme naplnili `SelectCommand` uloženou proceduru k použití `JOIN` a znovu spustili Průvodce konfigurací TableAdapter a aktualizovali sloupce `EmployeesDataTable` s.

Po opětovném spuštění Průvodce konfigurací TableAdapter se automaticky aktualizují `EmployeesDataTable` sloupce tak, aby odrážely datová pole vrácená `Employees_Select` uloženou procedurou. Alternativně jsme mohli tyto sloupce do objektu DataTable přidat ručně. V dalším kurzu budeme prozkoumat ručním přidáním sloupců do objektu DataTable.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Hilton Geisenow, David Suru a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [Další](adding-additional-datatable-columns-cs.md)
