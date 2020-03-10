---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 3: řazení a filtrování | Microsoft Docs'
author: tdykstra
description: Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená Začínáme pomocí řady kurzů Entity Framework 4,0. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631668"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 3: řazení a filtrování

tím, že [Dykstra](https://github.com/tdykstra)

> Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená [Začínáme pomocí řady kurzů Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) . Pokud jste nedokončili předchozí kurzy, jako výchozí bod tohoto kurzu si můžete aplikaci, kterou jste vytvořili, [Stáhnout](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Můžete si také [Stáhnout aplikaci](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , která je vytvořená úplnou řadou kurzů. Pokud máte dotazy k kurzům, můžete je publikovat na [fórum ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

V předchozím kurzu jste implementovali vzor úložiště v n-vrstvé webové aplikaci, která používá Entity Framework a ovládací prvek `ObjectDataSource`. V tomto kurzu se dozvíte, jak provádět řazení a filtrování a zpracovávat scénáře hlavní-podrobnosti. Na stránku *oddělení. aspx* přidáte následující vylepšení:

- Textové pole, které uživatelům umožní vybrat oddělení podle jména.
- Seznam kurzů pro každé oddělení zobrazené v mřížce
- Možnost řazení kliknutím na záhlaví sloupců.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>Přidání možnosti řazení sloupců GridView

Otevřete stránku *oddělení. aspx* a přidejte atribut `SortParameterName="sortExpression"` do ovládacího prvku `ObjectDataSource` s názvem `DepartmentsObjectDataSource`. (Později vytvoříte metodu `GetDepartments`, která převezme parametr s názvem `sortExpression`.) Značky pro otevírací značku ovládacího prvku nyní připomínají následující příklad.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

Přidejte atribut `AllowSorting="true"` do počáteční značky `GridView` ovládacího prvku. Značky pro otevírací značku ovládacího prvku nyní připomínají následující příklad.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

V *departments.aspx.cs*nastavte výchozí pořadí řazení voláním metody `Sort` `GridView` ovládacího prvku z metody `Page_Load`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

Můžete přidat kód, který seřadí nebo filtruje buď ve třídě obchodní logiky, nebo ve třídě úložiště. Pokud to provedete ve třídě obchodní logika, bude řazení nebo filtrování provedeno po načtení dat z databáze, protože třída obchodní logiky pracuje s objektem `IEnumerable` vráceným úložištěm. Pokud přidáte kód pro řazení a filtrování do třídy úložiště a provedete jej před převodem výrazu LINQ nebo objektu na objekt `IEnumerable`, budou příkazy předány do databáze ke zpracování, což je obvykle efektivnější. V tomto kurzu implementujete řazení a filtrování způsobem, který způsobí, že se zpracování provádí v databázi, tj. v úložišti.

Chcete-li přidat možnosti řazení, je nutné přidat novou metodu do rozhraní úložiště a třídy úložiště a také do třídy obchodní logiky. V souboru *ISchoolRepository.cs* přidejte novou `GetDepartments` metodu, která převezme parametr `sortExpression`, který se použije k řazení seznamu vrácených oddělení:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

Parametr `sortExpression` určí sloupec, podle kterého se má řadit, a směr řazení.

Do souboru *SchoolRepository.cs* přidejte kód pro novou metodu:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

Změňte existující metodu `GetDepartments` bez parametrů pro volání nové metody:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

V testovacím projektu přidejte následující novou metodu do *MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

Pokud jste chtěli vytvořit jakékoli testy jednotek, které jsou závislé na této metodě vracející seřazený seznam, museli byste seznam před jeho vrácením seřadit. V tomto kurzu nebudete vytvářet testy jako v tomto kurzu, takže metoda může jednoduše vrátit Neseřazený seznam oddělení.

V souboru *SchoolBL.cs* přidejte následující novou metodu do třídy obchodní logiky:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

Tento kód předá parametr řazení metodě úložiště.

Spusťte stránku *oddělení. aspx* .

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

Nyní můžete kliknout na záhlaví kteréhokoli sloupce a řadit podle daného sloupce. Pokud je sloupec již seřazený, kliknutím na záhlaví obrátíte směr řazení.

## <a name="adding-a-search-box"></a>Přidání vyhledávacího pole

V této části přidáte textové pole hledání, propojíte ho s ovládacím prvkem `ObjectDataSource` pomocí parametru Control a přidáte metodu do třídy obchodní logiky pro podporu filtrování.

Otevřete stránku *oddělení. aspx* a přidejte následující značku mezi nadpisem a prvním ovládacím prvkem `ObjectDataSource`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

V ovládacím prvku `ObjectDataSource` s názvem `DepartmentsObjectDataSource`proveďte následující kroky:

- Přidejte `SelectParameters` element pro parametr s názvem `nameSearchString`, který získá hodnotu zadanou v ovládacím prvku `SearchTextBox`.
- Změňte hodnotu atributu `SelectMethod` na `GetDepartmentsByName`. (Tuto metodu vytvoříte později.)

Značky pro ovládací prvek `ObjectDataSource` nyní připomínají následující příklad:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

Do *ISchoolRepository.cs*přidejte metodu `GetDepartmentsByName`, která přijímá parametry `sortExpression` a `nameSearchString`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

Do *SchoolRepository.cs*přidejte následující novou metodu:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

Tento kód používá metodu `Where` k výběru položek, které obsahují hledaný řetězec. Pokud je hledaný řetězec prázdný, budou vybrány všechny záznamy. Všimněte si, že pokud zadáte volání metody společně v jednom příkazu (`Include`, pak `OrderBy`a pak `Where`), metoda `Where` musí vždy být poslední.

Změňte existující metodu `GetDepartments`, která převezme parametr `sortExpression` pro volání nové metody:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

Do *MockSchoolRepository.cs* v testovacím projektu přidejte následující novou metodu:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

Do *SchoolBL.cs*přidejte následující novou metodu:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

Spusťte stránku *oddělení. aspx* a zadejte hledaný řetězec, abyste se ujistili, že logika výběru funguje. Pole text nechejte prázdné a zkuste hledání zkontrolovat, zda jsou vráceny všechny záznamy.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>Přidání sloupce podrobností pro každý řádek mřížky

V dalším kroku chcete zobrazit všechny kurzy pro každé oddělení zobrazené v pravé buňce mřížky. K tomuto účelu použijete vnořený ovládací prvek `GridView` a provedete jeho vázání na data z `Courses` navigační vlastnosti entity `Department`.

Otevřete panel *oddělení. aspx* a v části značky pro ovládací prvek `GridView` určete obslužnou rutinu pro událost `RowDataBound`. Značky pro otevírací značku ovládacího prvku nyní připomínají následující příklad.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

Přidejte nový element `TemplateField` za pole šablony `Administrator`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

Tento kód vytvoří vnořený `GridView` ovládací prvek, který zobrazuje číslo kurzu a název seznamu kurzů. Neurčuje zdroj dat, protože ho v obslužné rutině `RowDataBound` provedete v kódu.

Otevřete *departments.aspx.cs* a přidejte následující obslužnou rutinu pro událost `RowDataBound`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

Tento kód získá `Department` entitu z argumentů události, převede `Courses` navigační vlastnost na kolekci `List` a dataváže vnořenou `GridView` do kolekce.

Otevřete soubor *SchoolRepository.cs* a zadejte Eager načítání pro navigační vlastnost `Courses` voláním metody `Include` v dotazu objektu, který vytvoříte v metodě `GetDepartmentsByName`. Příkaz `return` v metodě `GetDepartmentsByName` nyní vypadá podobně jako v následujícím příkladu.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

Spusťte stránku. Kromě možnosti řazení a filtrování, které jste přidali dříve, ovládací prvek GridView nyní zobrazuje informace o vnořeném kurzu pro každé oddělení.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

Tím se dokončí Úvod ke scénářům řazení, filtrování a hlavní-podrobnosti. V dalším kurzu se dozvíte, jak zpracovávat souběžnost.

> [!div class="step-by-step"]
> [Předchozí](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [Další](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
