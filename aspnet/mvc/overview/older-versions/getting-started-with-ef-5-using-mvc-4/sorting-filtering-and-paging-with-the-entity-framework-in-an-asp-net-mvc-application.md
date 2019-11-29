---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: Řazení, filtrování a stránkování s Entity Framework v aplikaci ASP.NET MVC (3 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b1ddb70805dcb07fb60eea895ff572c054bde5c6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595224"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>Řazení, filtrování a stránkování pomocí Entity Framework v aplikaci ASP.NET MVC (3 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozím kurzu jste implementovali sadu webových stránek pro základní operace CRUD pro `Student` entit. V tomto kurzu přidáte na stránku indexu **studentů** funkce řazení, filtrování a stránkování. Vytvoří se také stránka, která provede jednoduché seskupení.

Na následujícím obrázku vidíte, jak stránka bude vypadat, až budete hotovi. Záhlaví sloupců jsou odkazy, na které může uživatel kliknout pro řazení podle daného sloupce. Kliknutí na záhlaví sloupce se opakovaně přepíná mezi vzestupném a sestupným řazením.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>Přidat odkazy na řazení sloupců na stránku indexu studentů

Chcete-li přidat řazení na stránku indexu studenta, změňte metodu `Index` řadiče `Student` a přidejte kód do zobrazení indexu `Student`.

### <a name="add-sorting-functionality-to-the-index-method"></a>Přidání funkcí řazení do metody index

V *Controllers\StudentController.cs*nahraďte metodu `Index` následujícím kódem:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Tento kód přijímá `sortOrder` parametr z řetězce dotazu v adrese URL. Hodnota řetězce dotazu je poskytnuta ASP.NET MVC jako parametr metody Action. Parametr bude řetězec, který je buď "Name", nebo "date", volitelně následovaný podtržítkem a řetězcem "desc" pro určení sestupného pořadí. Výchozí pořadí řazení je vzestupné.

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

Metoda používá [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) k určení sloupce, podle kterého se má řadit. Kód vytvoří proměnnou [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) před příkazem `switch`, upraví ji v příkazu `switch` a zavolá metodu `ToList` po `switch` příkaz. Při vytváření a úpravách `IQueryable` proměnných se do databáze neodesílají žádné dotazy. Dotaz není proveden, dokud nepřevedete objekt `IQueryable` do kolekce voláním metody, jako je například `ToList`. Proto tento kód má za následek jeden dotaz, který není proveden do příkazu `return View`.

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>Přidat hypertextové odkazy záhlaví sloupce do zobrazení indexu studenta

V *Views\Student\Index.cshtml*nahraďte prvky `<tr>` a `<th>` pro řádek záhlaví zvýrazněným kódem:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

Tento kód používá informace ve vlastnostech `ViewBag` k nastavení hypertextových odkazů s příslušnými hodnotami řetězce dotazu.

Spusťte stránku a kliknutím na záhlaví sloupce **Poslední název** a **Datum registrace** ověřte, že řazení funguje.

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

Po kliknutí na záhlaví **příjmení** se studenty zobrazí v sestupném pořadí příjmení.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>Přidání vyhledávacího pole na stránku indexu studentů

Chcete-li přidat filtrování na stránku indexu studentů, přidejte do zobrazení textové pole a tlačítko Odeslat a proveďte odpovídající změny v `Index` metodě. Textové pole umožňuje zadat řetězec, který bude hledán v poli jméno a příjmení.

### <a name="add-filtering-functionality-to-the-index-method"></a>Přidání funkce filtrování do metody index

V *Controllers\StudentController.cs*nahraďte metodu `Index` následujícím kódem (změny jsou zvýrazněny):

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

Přidali jste do metody `Index` parametr `searchString`. Do příkazu LINQ jste také přidali klauzuli `where`, která vybere pouze studenty, jejichž křestní jméno nebo příjmení obsahuje hledaný řetězec. Hodnota vyhledávacího řetězce je přijímána z textového pole, které přidáte do zobrazení index. Příkaz, který přidá klauzuli [WHERE](https://msdn.microsoft.com/library/bb535040.aspx) , je proveden pouze v případě, že existuje hodnota, která se má vyhledat.

> [!NOTE]
> V mnoha případech můžete zavolat stejnou metodu buď na Entity Framework sadu entit nebo jako metodu rozšíření v kolekci v paměti. Výsledky jsou normálně stejné, ale v některých případech se mohou lišit. Například .NET Framework implementace metody `Contains` vrátí všechny řádky, když do ní předáte prázdný řetězec, ale zprostředkovatel Entity Framework pro SQL Server Compact 4,0 vrátí nulové řádky pro prázdné řetězce. Proto kód v příkladu (vložení příkazu `Where` do příkazu `if`) zajistí, že získáte stejné výsledky pro všechny verze SQL Server. Kromě toho .NET Framework implementace `Contains` metody ve výchozím nastavení provádí porovnávání s rozlišováním velkých a malých písmen, Entity Framework ale zprostředkovatelé SQL Server ve výchozím nastavení nerozlišuje velká a malá písmena. Proto voláním metody `ToUpper` pro zajištění, že test explicitně nerozlišuje velká a malá písmena, zajistí, že se výsledky nezmění při pozdějším změně kódu pro použití úložiště, které vrátí kolekci `IEnumerable` namísto objektu `IQueryable`. (Při volání metody `Contains` v kolekci `IEnumerable`, získáte .NET Framework implementaci. Pokud ji voláte na `IQueryable` objekt, získáte implementaci poskytovatele databáze.)

### <a name="add-a-search-box-to-the-student-index-view"></a>Přidání vyhledávacího pole do zobrazení indexu studenta

V *Views\Student\Index.cshtml*přidejte zvýrazněný kód těsně před otevírací značku `table`, aby se vytvořil titulek, textové pole a tlačítko **hledání** .

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

Spusťte stránku, zadejte hledaný řetězec a kliknutím na tlačítko **Hledat** ověřte, zda filtrování funguje.

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Všimněte si, že adresa URL neobsahuje hledaný řetězec "a", což znamená, že pokud tuto stránku zařadíte do záložky, nezobrazí se při použití záložky filtrovaný seznam. Později v tomto kurzu změníte tlačítko **hledání** na použití řetězců dotazů pro kritéria filtru.

## <a name="add-paging-to-the-students-index-page"></a>Přidat stránkování na stránku indexu studentů

Pokud chcete přidat stránkování na stránku indexu studentů, začněte tím, že nainstalujete balíček NuGet **PagedList. Mvc** . Pak provedete další změny v metodě `Index` a přidáte odkazy na stránkování do zobrazení `Index`. **PagedList. Mvc** je jedním z mnoha dobrých balíčků pro stránkování a seřazení pro ASP.NET MVC a její použití je určeno pouze jako příklad, nikoli jako doporučení pro jiné možnosti. Na následujícím obrázku jsou znázorněny odkazy na stránkování.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>Instalace balíčku NuGet PagedList. MVC

Balíček NuGet **PagedList. Mvc** automaticky nainstaluje balíček **PagedList** jako závislost. Balíček **PagedList** nainstaluje typ kolekce `PagedList` a metody rozšíření pro kolekce `IQueryable` a `IEnumerable`. Metody rozšíření vytvářejí v kolekci `PagedList` jednu stránku dat mimo `IQueryable` nebo `IEnumerable`a kolekce `PagedList` poskytuje několik vlastností a metod, které usnadňují stránkování. Balíček **PagedList. Mvc** nainstaluje pomocný objekt pro stránkování, který zobrazí tlačítka stránkování.

V nabídce **nástroje** vyberte **Správce balíčků NuGet** a pak **spravujte balíčky NuGet pro řešení**.

V dialogovém okně **Spravovat balíčky NuGet** klikněte na kartu **online** a potom do vyhledávacího pole zadejte "stránkované". Po zobrazení balíčku **PagedList. Mvc** klikněte na **nainstalovat**.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

V poli **Vybrat projekty** klikněte na tlačítko **OK**.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>Přidání funkce stránkování do metody index

Do *Controllers\StudentController.cs*přidejte příkaz `using` pro obor názvů `PagedList`:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Metodu `Index` nahraďte následujícím kódem:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Tento kód přidá parametr `page`, aktuální parametr pořadí řazení a aktuální parametr filtru na signaturu metody, jak je znázorněno zde:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Při prvním zobrazení stránky, nebo pokud uživatel neklikl na odkaz na stránkování nebo řazení, všechny parametry budou mít hodnotu null. Pokud se klikne na odkaz na stránkování, proměnná `page` bude obsahovat číslo stránky, které se má zobrazit.

vlastnost `A ViewBag` poskytuje zobrazení s aktuálním pořadím řazení, protože musí být součástí odkazů stránkování, aby při stránkování zůstalo stejné pořadí řazení:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Jiná vlastnost, `ViewBag.CurrentFilter`, poskytuje zobrazení s aktuálním řetězcem filtru. Tato hodnota musí být součástí odkazů stránkování, aby bylo možné zachovat nastavení filtru během stránkování, a při zobrazení stránky musí být obnovena do textového pole. Pokud se hledaný řetězec během stránkování změní, je nutné obnovit stránku na 1, protože nový filtr může mít za následek zobrazení různých dat. Hledaný řetězec se změní, když je v textovém poli vložena hodnota a stisknete tlačítko Odeslat. V takovém případě parametr `searchString` nemá hodnotu null.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

Na konci metody `ToPagedList` metoda rozšíření na `IQueryable` objekt Students převede dotaz studenta na jednu stránku studentů v typu kolekce, který podporuje stránkování. Tato jediná strana studentů se pak předává do zobrazení:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Metoda `ToPagedList` přebírá číslo stránky. Dvě otazníky reprezentují [operátor slučování s hodnotou null](https://msdn.microsoft.com/library/ms173224.aspx). Operátor slučování null definuje výchozí hodnotu pro typ s možnou hodnotou null. výraz `(page ?? 1)` znamená vrátit hodnotu `page`, pokud má hodnotu, nebo vrátí hodnotu 1, pokud `page` má hodnotu null.

### <a name="add-paging-links-to-the-student-index-view"></a>Přidat odkazy na stránkování do zobrazení indexu studenta

V *Views\Student\Index.cshtml*nahraďte existující kód následujícím kódem:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

Příkaz `@model` v horní části stránky určuje, že zobrazení nyní Získá objekt `PagedList` namísto objektu `List`.

Příkaz `using` pro `PagedList.Mvc` poskytuje přístup k Pomocníkovi MVC pro tlačítka stránkování.

Kód používá přetížení [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) , které umožňuje určit [FormMethod. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

Výchozí [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) odesílá data formuláře pomocí příspěvku, což znamená, že parametry jsou předány v těle zprávy HTTP a nejsou v adrese URL jako řetězce dotazů. Když zadáte příkaz HTTP GET, data formuláře se předávají v adrese URL jako řetězce dotazů, které uživatelům umožňují záložku URL. [Pokyny pro konsorcium W3C pro použití HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) určují, že byste měli použít Get, když akce nevede k aktualizaci.

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

Spusťte stránku.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Kliknutím na odkazy na stránkování v různých pořadích řazení zajistěte, aby stránkování fungovalo. Pak zadejte hledaný řetězec a zkuste znovu vytvořit stránkování, abyste ověřili, že stránkování funguje i správně s řazením a filtrováním.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>Vytvoření stránky o stránku, která zobrazuje údaje o studentech

Pro stránku se stránkou společnosti Contoso na univerzitě se zobrazí, kolik studentů se zaregistrovalo pro každé datum registrace. To vyžaduje seskupování a jednoduché výpočty skupin. K tomu je třeba provést následující akce:

- Vytvořte třídu zobrazení modelu pro data, která potřebujete předat zobrazení.
- V kontroleru `Home` upravte metodu `About`.
- Upravte zobrazení `About`.

### <a name="create-the-view-model"></a>Vytvoření modelu zobrazení

Vytvořte složku *ViewModels* . V této složce přidejte soubor třídy *EnrollmentDateGroup.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Úprava domovského kontroleru

V *HomeController.cs*přidejte na začátek souboru následující příkazy `using`:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

Přidejte proměnnou třídy pro kontext databáze hned za levou složenou závorku pro třídu:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

Metodu `About` nahraďte následujícím kódem:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

Příkaz LINQ seskupuje entity studenta podle data registrace, vypočítá počet entit v každé skupině a ukládá výsledky do kolekce `EnrollmentDateGroup` objektů modelu zobrazení.

Přidejte `Dispose` metodu:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>Úprava zobrazení o produktu

Nahraďte kód v souboru *Views\Home\About.cshtml* následujícím kódem:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

Spusťte aplikaci a klikněte na odkaz **informace** . V tabulce se zobrazí počet studentů pro každé datum zápisu.

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>Volitelné: Nasaďte aplikaci do Windows Azure.

Zatím je vaše aplikace spuštěná místně v IIS Express ve vývojovém počítači. Aby ho mohli používat i ostatní uživatelé přes Internet, musíte ho nasadit do poskytovatele hostování webů. V této volitelné části kurzu ji nasadíte na web Windows Azure.

### <a name="using-code-first-migrations-to-deploy-the-database"></a>Nasazení databáze pomocí Migrace Code First

K nasazení databáze, kterou použijete Migrace Code First. Když vytvoříte profil publikování, který použijete ke konfiguraci nastavení pro nasazení ze sady Visual Studio, zaškrtněte políčko, které je označeno jako spouštěné **migrace Code First (spouští se při spuštění aplikace)** . Toto nastavení způsobí, že proces nasazení automaticky konfiguruje soubor *Web. config* aplikace na cílovém serveru tak, aby Code First používal třídu inicializátoru `MigrateDatabaseToLatestVersion`.

Aplikace Visual Studio během procesu nasazení neprovede žádné akce s databází. Když nasazená aplikace přistupuje k databázi poprvé po nasazení, Code First automaticky vytvoří databázi nebo aktualizuje schéma databáze na nejnovější verzi. Pokud aplikace implementuje migrace `Seed` metody, metoda se spustí po vytvoření databáze nebo aktualizaci schématu.

Vaše migrace `Seed` metodu vloží testovací data. Pokud jste nasadili do provozního prostředí, bude nutné změnit metodu `Seed` tak, aby do ní vložila pouze data, která chcete vložit do provozní databáze. Například v aktuálním datovém modelu možná budete chtít mít reálné kurzy, ale fiktivní studenty ve vývojové databázi. Můžete napsat metodu `Seed` pro načtení ve vývoji a pak před nasazením do produkčního prostředí odkomentovat fiktivní studenty. Nebo můžete napsat metodu `Seed` pro načtení pouze kurzů a zadat fiktivní studenty do testovací databáze ručně pomocí uživatelského rozhraní aplikace.

### <a name="get-a-windows-azure-account"></a>Získat účet Windows Azure

Budete potřebovat účet Microsoft Azure. Pokud ho ještě nemáte, můžete si během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v článku [bezplatná zkušební verze Windows Azure](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>Vytvoření webu a databáze SQL ve Windows Azure

Váš web Windows Azure se spustí ve sdíleném hostitelském prostředí, což znamená, že se spustí na virtuálních počítačích, které jsou sdílené s jinými klienty Windows Azure. Sdílené hostitelské prostředí představuje nízký nákladový způsob, jak začít v cloudu. Později, pokud se webový provoz zvýší, aplikace může škálovat tak, aby splňovala nutnost spuštění na vyhrazených virtuálních počítačích. Pokud potřebujete komplexnější architekturu, můžete migrovat do cloudové služby Microsoft Azure. Cloudové služby běží na vyhrazených virtuálních počítačích, které můžete konfigurovat podle svých potřeb.

Windows Azure SQL Database je cloudová služba relačních databází, která je založená na technologiích SQL Server. Nástroje a aplikace, které pracují s SQL Server, fungují i s SQL Database.

1. V [portál pro správu Windows Azure](https://manage.windowsazure.com/)klikněte na **webové servery** na levé kartě a potom klikněte na **Nový**.

    ![Nové tlačítko v Portál pro správu](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. Klikněte na **vlastní vytvořit**.

    ![Vytvořit s odkazem na databázi v Portál pro správu](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   **Nový web – otevře se Průvodce vytvořením vlastního** webu.
3. V kroku průvodce **Nový web** zadejte do pole **Adresa URL** řetězec, který použijete jako jedinečnou adresu URL pro vaši aplikaci. Úplná adresa URL bude obsahovat informace o tom, co zadáte, a příponu, která se zobrazí vedle textového pole. Ilustrace ukazuje "ConU", ale tato adresa URL je pravděpodobně provedena, takže budete muset zvolit jiný.

    ![Vytvořit s odkazem na databázi v Portál pro správu](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. V rozevíracím seznamu **oblast** vyberte oblast, která je pro vás blízko. Toto nastavení určuje, které datové centrum bude web běžet v.
5. V rozevíracím seznamu **databáze** vyberte **vytvořit bezplatnou 20 MB databáze SQL Database**.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. Do pole **název připojovacího řetězce databáze**zadejte *SchoolContext*.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. Klikněte na šipku, která odkazuje na pravou stranu v poli. Průvodce přejde do kroku **nastavení databáze** .
8. Do pole **název** zadejte *ContosoUniversityDB*.
9. V poli **Server** vyberte **Nový SQL Database Server**. Případně, pokud jste dříve vytvořili server, můžete vybrat tento server z rozevíracího seznamu.
10. Zadejte **přihlašovací jméno** a **heslo**správce. Pokud jste vybrali **nový SQL Database Server** nevstupujete sem existující jméno a heslo, zadáváte nové jméno a heslo, které teď definujete pro pozdější použití při přístupu k databázi. Pokud jste vybrali Server, který jste vytvořili dříve, zadáte přihlašovací údaje pro tento server. Pro tento kurz nezaškrtněte políčko ***Upřesnit*** . ***Rozšířené*** možnosti umožňují nastavit [kolaci](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)databáze.
11. Zvolte stejnou **oblast** , kterou jste zvolili pro web.
12. Kliknutím na značku zaškrtnutí v pravém dolním rohu pole označíte, že jste hotovi.   
  
    ![Krok nastavení databáze nového webu – Průvodce vytvořením databáze](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    Následující obrázek ukazuje použití existujícího SQL Server a přihlášení.   
  
    ![Krok nastavení databáze nového webu – Průvodce vytvořením databáze](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    Portál pro správu vrátí na stránku webové stránky a ve sloupci **stav** se zobrazí, že se web vytváří. Po delší dobu (obvykle méně než minutu) se ve sloupci **stav** zobrazí, že se lokalita úspěšně vytvořila. V navigačním panelu vlevo se zobrazí počet webů v účtu vedle ikony **webové stránky** a počet databází se zobrazí vedle ikony **databáze SQL** .

## <a name="deploy-the-application-to-windows-azure"></a>Nasazení aplikace do platformy Windows Azure

1. V aplikaci Visual Studio klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a v místní nabídce vyberte **publikovat** .  
  
    ![Místní nabídka publikovat v projektu](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. Na kartě **profil** průvodce **Publikovat web** klikněte na **importovat**.  
  
    ![Importovat nastavení publikování](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. Pokud jste ještě v aplikaci Visual Studio nepřidali své předplatné služby Windows Azure, proveďte následující kroky. V tomto postupu přidáte vaše předplatné, takže rozevírací seznam v části **importovat z webu Windows Azure** bude obsahovat váš web.

    a. V dialogovém okně **Importovat profil publikování** klikněte na **importovat z webu Windows Azure**a pak klikněte na **Přidat předplatné Windows Azure**.

    ![Přidat předplatné Windows Azure](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. V dialogovém okně **importovat předplatná Windows Azure** klikněte na **Stáhnout soubor předplatného**.

    ![Stáhnout soubor předplatného](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    r. V okně prohlížeče uložte soubor *. publishsettings* .

    ![Stažení souboru. publishsettings](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > Zabezpečení – soubor *publishsettings* obsahuje vaše přihlašovací údaje (nekódované), které se používají ke správě předplatných a služeb Windows Azure. Osvědčeným postupem zabezpečení pro tento soubor je uložit ho dočasně mimo vaše zdrojové adresáře (například ve složce *Libraries\Documents* ) a po dokončení importu ho odstranit. Uživatel se zlými úmysly, který získá přístup k souboru `.publishsettings`, může upravit, vytvořit a odstranit vaše služby Windows Azure.

    trojrozměrné. V dialogovém okně **importovat předplatná Windows Azure** klikněte na **Procházet** a přejděte na soubor *. publishsettings* .

    ![Stáhnout sub](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    cerebrální. Klikněte na **importovat**.

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. V dialogovém okně **Importovat profil publikování** vyberte **importovat z webu Windows Azure**, v rozevíracím seznamu vyberte svůj web a pak klikněte na **OK**.  
  
    ![Importovat publikační profil](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. Na kartě **připojení** klikněte na **ověřit připojení** a ujistěte se, že jsou nastavení správná.  
  
    ![Ověřit připojení](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. Po ověření připojení se zobrazí zelená značka zaškrtnutí vedle tlačítka **ověřit připojení** . Klikněte na tlačítko **Další**.  
  
    ![Připojení bylo úspěšně ověřeno.](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. V části **SchoolContext** otevřete rozevírací seznam **řetězce vzdáleného připojení** a vyberte připojovací řetězec pro databázi, kterou jste vytvořili.
8. Vyberte **Execute migrace Code First (spouští se při spuštění aplikace)** .
9. Zrušte kontrolu **použití tohoto připojovacího řetězce za běhu** pro **userContext (DefaultConnection)** , protože tato aplikace nepoužívá databázi členství.   
  
    ![Karta Nastavení](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. Klikněte na tlačítko **Další**.
11. Na kartě **Náhled** klikněte na možnost **Spustit náhled**.  
  
    ![Tlačítko StartPreview na kartě Preview](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    Karta zobrazuje seznam souborů, které se zkopírují na server. Zobrazení náhledu není vyžadováno pro publikování aplikace, ale je užitečnou funkcí, kterou je třeba znát. V takovém případě nemusíte nic dělat se seznamem zobrazených souborů. Při příštím nasazení této aplikace se v tomto seznamu zobrazí pouze soubory, které se změnily.  
  
    ![Výstup souboru StartPreview](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. Klikněte na **publikovat**.  
    Visual Studio zahájí proces kopírování souborů do Windows Azure serveru.
13. Okno **výstup** zobrazuje, jaké akce nasazení byly provedeny, a oznamuje úspěšné dokončení nasazení.  
  
    ![Úspěšné nasazení hlášení okna výstup](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. Po úspěšném nasazení se výchozí prohlížeč automaticky otevře na adrese URL nasazeného webu.  
    Aplikace, kterou jste vytvořili, je teď spuštěná v cloudu. Klikněte na kartu studenti.  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

V tomto okamžiku byla databáze *SchoolContext* vytvořena ve Windows Azure SQL Database, protože jste vybrali možnost **Spustit migrace Code First (spouští se při spuštění aplikace)** . Soubor *Web. config* na nasazeném webu byl změněn tak, aby byl spuštěn inicializátor [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) při prvním načtení nebo zápisu dat do databáze (ke kterému došlo po výběru karty **Students** ):

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

Proces nasazení také vytvořil nový připojovací řetězec *(SchoolContext\_DatabasePublish*), který migrace Code First použít k aktualizaci schématu databáze a k osazení databáze.

![Připojovací řetězec Database_Publish](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

Připojovací řetězec *DefaultConnection* je pro databázi členství (kterou v tomto kurzu nepoužíváme). Připojovací řetězec *SchoolContext* je pro databázi ContosoUniversity.

Nasazenou verzi souboru Web. config můžete najít na svém vlastním počítači v *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*. K nasazenému souboru *Web. config* se můžete dostat pomocí FTP. Pokyny najdete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace kódu](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md). Postupujte podle pokynů, které začínají na používání nástroje FTP, potřebujete tři věci: adresa URL serveru FTP, uživatelské jméno a heslo. "

> [!NOTE]
> Webová aplikace neimplementuje zabezpečení, takže kdokoli, kdo najde adresu URL, může data změnit. Pokyny k zabezpečení webu najdete v tématu [nasazení zabezpečené aplikace ASP.NET MVC pomocí členství, protokolu OAuth a SQL Database na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Jiným lidem můžete zabránit v používání webu pomocí Portál pro správu Windows Azure nebo **Průzkumník serveru** v aplikaci Visual Studio k zastavení lokality.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Inicializátory Code First

V části nasazení jste viděli, že se používá inicializátor [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) . Code First také poskytuje další inicializátory, které lze použít, včetně [metodu createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (výchozí), [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) a [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx). Inicializátor `DropCreateAlways` může být užitečný pro nastavení podmínek pro testování částí. Můžete také napsat vlastní Inicializátory a můžete zavolat inicializátor explicitně, pokud nechcete čekat, dokud aplikace nenačte nebo zapíše do databáze. Komplexní vysvětlení inicializátorů naleznete v části kapitola 6 příručky [programovacího Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) od Julie Lerman a Rowan Miller.

## <a name="summary"></a>Přehled

V tomto kurzu jste viděli, jak vytvořit datový model a implementovat základní funkce CRUD, řazení, filtrování, stránkování a seskupování. V dalším kurzu začnete seznámení s pokročilejšími tématy tím, že rozšíříte datový model.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Předchozí](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [Další](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
