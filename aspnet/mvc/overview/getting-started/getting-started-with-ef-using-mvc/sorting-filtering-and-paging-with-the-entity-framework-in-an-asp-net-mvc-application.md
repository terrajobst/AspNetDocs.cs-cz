---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: Přidání řazení, filtrování a stránkování pomocí Entity Framework v aplikaci ASP.NET MVC | Microsoft Docs'
author: tdykstra
description: V tomto kurzu přidáte na stránku indexu **studentů** funkce řazení, filtrování a stránkování. Můžete také vytvořit jednoduchou stránku seskupení.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616037"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>Kurz: Přidání řazení, filtrování a stránkování s Entity Framework v aplikaci MVC ASP.NET

V [předchozím kurzu](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)jste implementovali sadu webových stránek pro základní operace CRUD pro `Student` entit. V tomto kurzu přidáte na stránku indexu **studentů** funkce řazení, filtrování a stránkování. Můžete také vytvořit jednoduchou stránku seskupení.

Následující obrázek ukazuje, jak stránka bude vypadat, až budete hotovi. Záhlaví sloupců jsou odkazy, na které může uživatel kliknout pro řazení podle daného sloupce. Kliknutí na záhlaví sloupce se opakovaně přepíná mezi vzestupném a sestupným řazením.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidat odkazy na řazení sloupců
> * Přidání vyhledávacího pole
> * Přidat stránkování
> * Vytvoření stránky o stránku

## <a name="prerequisites"></a>Předpoklady

* [Implementace základních funkcí CRUD](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>Přidat odkazy na řazení sloupců

Chcete-li přidat řazení na stránku indexu studenta, změňte metodu `Index` řadiče `Student` a přidejte kód do zobrazení indexu `Student`.

### <a name="add-sorting-functionality-to-the-index-method"></a>Přidání funkcí řazení do metody index

- V *Controllers\StudentController.cs*nahraďte metodu `Index` následujícím kódem:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Tento kód přijímá `sortOrder` parametr z řetězce dotazu v adrese URL. Hodnota řetězce dotazu je poskytnuta ASP.NET MVC jako parametr metody Action. Parametr je řetězec, který je buď "Name", nebo "date", volitelně následovaný podtržítkem a řetězcem "desc" pro určení sestupného pořadí. Výchozí pořadí řazení je vzestupné.

Při prvním vyžádání stránky indexu není k dispozici žádný řetězec dotazu. Studenti se zobrazí ve vzestupném pořadí podle `LastName`, což je výchozí nastavení zavedené v případě příkazu `switch`. Když uživatel klikne na hypertextový odkaz záhlaví sloupce, v řetězci dotazu je uvedena odpovídající hodnota `sortOrder`.

Použijí se tyto dvě proměnné `ViewBag`, aby zobrazení mohl konfigurovat hypertextové odkazy záhlaví sloupců pomocí příslušných hodnot řetězce dotazu:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Jedná se o Ternární příkazy. První z nich určuje, že pokud parametr `sortOrder` má hodnotu null nebo je prázdný, `ViewBag.NameSortParm` by měl být nastaven na "Name\_desc"; v opačném případě by měl být nastaven na prázdný řetězec. Tyto dva příkazy umožňují zobrazení nastavit hypertextové odkazy záhlaví sloupce následujícím způsobem:

| Aktuální pořadí řazení | Hypertextový odkaz na poslední jméno | Hypertextový odkaz na datum |
| --- | --- | --- |
| Příjmení vzestupné | descending | ascending |
| Příjmení sestupně | ascending | ascending |
| Datum vzestupné | ascending | descending |
| Datum sestupné | ascending | ascending |

Metoda používá [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) k určení sloupce, podle kterého se má řadit. Kód vytvoří <xref:System.Linq.IQueryable%601> proměnnou před příkazem `switch`, upraví ji v příkazu `switch` a zavolá metodu `ToList` po příkazu `switch`. Při vytváření a úpravách `IQueryable` proměnných se do databáze neodesílají žádné dotazy. Dotaz není proveden, dokud nepřevedete objekt `IQueryable` do kolekce voláním metody, jako je například `ToList`. Proto tento kód má za následek jeden dotaz, který není proveden do příkazu `return View`.

Jako alternativu k psaní různých příkazů LINQ pro každé pořadí řazení můžete dynamicky vytvořit příkaz LINQ. Informace o dynamickém LINQ naleznete v tématu [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>Přidat hypertextové odkazy záhlaví sloupce do zobrazení indexu studenta

1. V *Views\Student\Index.cshtml*nahraďte prvky `<tr>` a `<th>` pro řádek záhlaví zvýrazněným kódem:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   Tento kód používá informace ve vlastnostech `ViewBag` k nastavení hypertextových odkazů s příslušnými hodnotami řetězce dotazu.

2. Spusťte stránku a kliknutím na záhlaví sloupce **Poslední název** a **Datum registrace** ověřte, že řazení funguje.

   Po kliknutí na záhlaví **příjmení** se studenty zobrazí v sestupném pořadí příjmení.

## <a name="add-a-search-box"></a>Přidání vyhledávacího pole

Chcete-li přidat filtrování na stránku indexu studentů, přidejte do zobrazení textové pole a tlačítko Odeslat a proveďte odpovídající změny v `Index` metodě. Textové pole umožňuje zadat řetězec, který chcete vyhledat v polích jméno a příjmení.

### <a name="add-filtering-functionality-to-the-index-method"></a>Přidání funkce filtrování do metody index

- V *Controllers\StudentController.cs*nahraďte metodu `Index` následujícím kódem (změny jsou zvýrazněny):

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

Kód přidá parametr `searchString` do metody `Index`. Hodnota vyhledávacího řetězce je přijímána z textového pole, které přidáte do zobrazení index. Přidá také klauzuli `where` do příkazu LINQ, který vybere pouze studenty, jejichž křestní jméno nebo příjmení obsahuje hledaný řetězec. Příkaz, který přidá klauzuli <xref:System.Linq.Queryable.Where%2A>, se spustí pouze v případě, že existuje hodnota, která se má vyhledat.

> [!NOTE]
> V mnoha případech můžete zavolat stejnou metodu buď na Entity Framework sadu entit nebo jako metodu rozšíření v kolekci v paměti. Výsledky jsou normálně stejné, ale v některých případech se mohou lišit.
>
> Například .NET Framework implementace metody `Contains` vrátí všechny řádky, když do ní předáte prázdný řetězec, ale zprostředkovatel Entity Framework pro SQL Server Compact 4,0 vrátí nulové řádky pro prázdné řetězce. Proto kód v příkladu (vložení příkazu `Where` do příkazu `if`) zajistí, že získáte stejné výsledky pro všechny verze SQL Server. Kromě toho .NET Framework implementace `Contains` metody ve výchozím nastavení provádí porovnávání s rozlišováním velkých a malých písmen, Entity Framework ale zprostředkovatelé SQL Server ve výchozím nastavení nerozlišuje velká a malá písmena. Proto voláním metody `ToUpper` pro zajištění, že test explicitně nerozlišuje velká a malá písmena, zajistí, že se výsledky nezmění při pozdějším změně kódu pro použití úložiště, které vrátí kolekci `IEnumerable` namísto objektu `IQueryable`. (Při volání metody `Contains` v kolekci `IEnumerable`, získáte .NET Framework implementaci. Pokud ji voláte na `IQueryable` objekt, získáte implementaci poskytovatele databáze.)
>
> Zpracování hodnot null se může také lišit pro různé poskytovatele databáze nebo při použití objektu `IQueryable` v porovnání s použitím kolekce `IEnumerable`. V některých scénářích například `Where` podmínka, například `table.Column != 0`, nesmí vracet sloupce, které mají `null` jako hodnotu. Ve výchozím nastavení EF generuje další operátory SQL pro zajištění rovnosti mezi hodnotami null v databázi funguje stejně jako v paměti, ale můžete nastavit příznak [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) v EF6 nebo volat metodu [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) v EF Core pro konfiguraci tohoto chování.

### <a name="add-a-search-box-to-the-student-index-view"></a>Přidání vyhledávacího pole do zobrazení indexu studenta

1. V *Views\Student\Index.cshtml*přidejte zvýrazněný kód těsně před otevírací značku `table`, aby se vytvořil titulek, textové pole a tlačítko **hledání** .

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. Spusťte stránku, zadejte hledaný řetězec a kliknutím na tlačítko **Hledat** ověřte, zda filtrování funguje.

   Všimněte si, že adresa URL neobsahuje hledaný řetězec "a", což znamená, že pokud tuto stránku zařadíte do záložky, nezobrazí se při použití záložky filtrovaný seznam. To platí také pro odkazy na řazení sloupců, protože budou řadit celý seznam. Později v tomto kurzu změníte tlačítko **hledání** na použití řetězců dotazů pro kritéria filtru.

## <a name="add-paging"></a>Přidat stránkování

Pokud chcete přidat stránkování na stránku indexu studentů, začněte tím, že nainstalujete balíček NuGet **PagedList. Mvc** . Pak provedete další změny v metodě `Index` a přidáte odkazy na stránkování do zobrazení `Index`. **PagedList. Mvc** je jedním z mnoha dobrých balíčků pro stránkování a seřazení pro ASP.NET MVC a její použití je určeno pouze jako příklad, nikoli jako doporučení pro jiné možnosti.

### <a name="install-the-pagedlistmvc-nuget-package"></a>Instalace balíčku NuGet PagedList. MVC

Balíček NuGet **PagedList. Mvc** automaticky nainstaluje balíček **PagedList** jako závislost. Balíček **PagedList** nainstaluje typ kolekce `PagedList` a metody rozšíření pro kolekce `IQueryable` a `IEnumerable`. Metody rozšíření vytvářejí v kolekci `PagedList` jednu stránku dat mimo `IQueryable` nebo `IEnumerable`a kolekce `PagedList` poskytuje několik vlastností a metod, které usnadňují stránkování. Balíček **PagedList. Mvc** nainstaluje pomocný objekt pro stránkování, který zobrazí tlačítka stránkování.

1. V nabídce **nástroje** vyberte **Správce balíčků NuGet** a pak **konzolu Správce balíčků**.

2. V okně **konzoly Správce balíčků** se ujistěte, že je **zdroj balíčku** **NuGet.org** a **výchozí projekt** je **ContosoUniversity**, a potom zadejte následující příkaz:

   ```text
   Install-Package PagedList.Mvc
   ```

3. Sestavte projekt.

### <a name="add-paging-functionality-to-the-index-method"></a>Přidání funkce stránkování do metody index

1. Do *Controllers\StudentController.cs*přidejte příkaz `using` pro obor názvů `PagedList`:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. Nahraďte metodu `Index` následujícím kódem:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   Tento kód přidá parametr `page`, aktuální parametr pořadí řazení a aktuální parametr filtru na signaturu metody:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   Při prvním zobrazení stránky, nebo pokud uživatel neklikl na odkaz na stránkování nebo řazení, mají všechny parametry hodnotu null. Pokud se klikne na odkaz na stránkování, `page` proměnná obsahuje číslo stránky k zobrazení.

   Vlastnost `ViewBag` poskytuje zobrazení s aktuálním pořadím řazení, protože musí být součástí odkazů stránkování, aby při stránkování zůstalo stejné pořadí řazení:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   Jiná vlastnost, `ViewBag.CurrentFilter`, poskytuje zobrazení s aktuálním řetězcem filtru. Tato hodnota musí být součástí odkazů stránkování, aby bylo možné zachovat nastavení filtru během stránkování, a při zobrazení stránky musí být obnovena do textového pole. Pokud se hledaný řetězec během stránkování změní, je nutné obnovit stránku na 1, protože nový filtr může mít za následek zobrazení různých dat. Hledaný řetězec se změní, když je v textovém poli vložena hodnota a stisknete tlačítko Odeslat. V takovém případě parametr `searchString` nemá hodnotu null.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   Na konci metody `ToPagedList` metoda rozšíření na `IQueryable` objekt Students převede dotaz studenta na jednu stránku studentů v typu kolekce, který podporuje stránkování. Tato jediná strana studentů se pak předává do zobrazení:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   Metoda `ToPagedList` přebírá číslo stránky. Dvě otazníky reprezentují [operátor slučování s hodnotou null](/dotnet/csharp/language-reference/operators/null-coalescing-operator). Operátor slučování null definuje výchozí hodnotu pro typ s možnou hodnotou null. výraz `(page ?? 1)` znamená vrátit hodnotu `page`, pokud má hodnotu, nebo vrátí hodnotu 1, pokud `page` má hodnotu null.

### <a name="add-paging-links-to-the-student-index-view"></a>Přidat odkazy na stránkování do zobrazení indexu studenta

1. V *Views\Student\Index.cshtml*nahraďte existující kód následujícím kódem. Změny jsou zvýrazněné.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   Příkaz `@model` v horní části stránky určuje, že zobrazení nyní Získá objekt `PagedList` namísto objektu `List`.

   Příkaz `using` pro `PagedList.Mvc` poskytuje přístup k Pomocníkovi MVC pro tlačítka stránkování.

   Kód používá přetížení [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) , které umožňuje určit [FormMethod. Get](/previous-versions/aspnet/dd460179(v=vs.100)).

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   Výchozí [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) odesílá data formuláře pomocí příspěvku, což znamená, že parametry jsou předány v těle zprávy HTTP a nejsou v adrese URL jako řetězce dotazů. Když zadáte příkaz HTTP GET, data formuláře se předávají v adrese URL jako řetězce dotazů, které uživatelům umožňují záložku URL. [Pokyny pro konsorcium W3C pro použití http vám](http://www.w3.org/2001/tag/doc/whenToUseGet.html) doporučují použít Get, když akce nevede k aktualizaci.

   Textové pole se inicializuje s aktuálním hledaným řetězcem, takže když kliknete na novou stránku, můžete zobrazit aktuální hledaný řetězec.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   Záhlaví sloupce odkazuje pomocí řetězce dotazu k předání aktuálního vyhledávacího řetězce k řadiči, aby uživatel mohl seřadit výsledky filtru:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   Zobrazí se aktuální stránka a celkový počet stránek.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   Pokud neexistují žádné stránky k zobrazení, zobrazí se hodnota "stránka 0 0". (V takovém případě je číslo stránky větší než počet stránek, protože `Model.PageNumber` 1 a `Model.PageCount` je 0.)

   Tlačítka stránkování jsou zobrazena pomocí pomocníka `PagedListPager`:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   Pomocná aplikace `PagedListPager` poskytuje řadu možností, které můžete přizpůsobit, včetně adres URL a stylů. Další informace najdete v tématu [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) na webu GitHubu.

2. Spusťte stránku.

   Kliknutím na odkazy na stránkování v různých pořadích řazení zajistěte, aby stránkování fungovalo. Pak zadejte hledaný řetězec a zkuste znovu vytvořit stránkování, abyste ověřili, že stránkování funguje i správně s řazením a filtrováním.

## <a name="create-an-about-page"></a>Vytvoření stránky o stránku

Pro stránku se stránkou společnosti Contoso na univerzitě se zobrazí, kolik studentů se zaregistrovalo pro každé datum registrace. To vyžaduje seskupování a jednoduché výpočty skupin. K tomu je třeba provést následující akce:

- Vytvořte třídu zobrazení modelu pro data, která potřebujete předat zobrazení.
- V kontroleru `Home` upravte metodu `About`.
- Upravte zobrazení `About`.

### <a name="create-the-view-model"></a>Vytvoření modelu zobrazení

Vytvořte složku *ViewModels* ve složce projektu. V této složce přidejte soubor třídy *EnrollmentDateGroup.cs* a nahraďte kód šablony následujícím kódem:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Úprava domovského kontroleru

1. V *HomeController.cs*přidejte na začátek souboru následující příkazy `using`:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. Přidejte proměnnou třídy pro kontext databáze hned za levou složenou závorku pro třídu:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. Nahraďte metodu `About` následujícím kódem:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   Příkaz LINQ seskupuje entity studenta podle data registrace, vypočítá počet entit v každé skupině a ukládá výsledky do kolekce `EnrollmentDateGroup` objektů modelu zobrazení.

4. Přidejte `Dispose` metodu:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>Úprava zobrazení o produktu

1. Nahraďte kód v souboru *Views\Home\About.cshtml* následujícím kódem:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. Spusťte aplikaci a klikněte na odkaz **informace** .

   Počet studentů pro každé datum registrace se zobrazí v tabulce.

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidat odkazy na řazení sloupců
> * Přidání vyhledávacího pole
> * Přidat stránkování
> * Vytvoření stránky o stránku

Přejděte k dalšímu článku, kde se dozvíte, jak používat odolnost připojení a zachycení příkazů.
> [!div class="nextstepaction"]
> [Odolnost připojení a zachycení příkazu](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
