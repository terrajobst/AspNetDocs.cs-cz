---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: Implementace vzorového úložiště a pracovní jednotky v aplikaci ASP.NET MVC (9 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595244"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>Implementace úložiště a pracovní jednotky vzorů v aplikaci ASP.NET MVC (9 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozím kurzu jste použili dědičnost k omezení nadbytečného kódu v `Student` a `Instructor` třídy entit. V tomto kurzu se dozvíte několik způsobů použití úložiště a pracovní jednotky pro operace CRUD. Stejně jako v předchozím kurzu změníte v tomto případě, jak váš kód pracuje se stránkami, které jste už vytvořili, a ne vytvářením nových stránek.

## <a name="the-repository-and-unit-of-work-patterns"></a>Vzor úložiště a pracovní jednotky

Vzorce úložiště a pracovní jednotky jsou určeny k vytvoření abstrakce vrstvy mezi vrstvou pro přístup k datům a vrstvou obchodní logiky aplikace. Implementace těchto vzorů vám může přispět k izolaci aplikace před změnami v úložišti dat a může usnadnit automatizované testování částí nebo vývoj řízený testováním (TDD).

V tomto kurzu implementujete třídu úložiště pro každý typ entity. Pro `Student` typ entity vytvoříte rozhraní úložiště a třídu úložiště. Při vytváření instance úložiště v řadiči budete používat rozhraní tak, aby řadič přijal odkaz na libovolný objekt, který implementuje rozhraní úložiště. Když se kontroler spustí pod webovým serverem, obdrží úložiště, které funguje s Entity Framework. Když se kontroler spustí pod třídou testu jednotek, obdrží úložiště, které funguje s daty uloženými způsobem, který umožňuje snadnou manipulaci s testováním, jako je například kolekce v paměti.

Později v tomto kurzu použijete více úložišť a třídu pracovní jednotky pro `Course` a `Department` typy entit v řadiči `Course`. Třída Working koordinuje práci více úložišť tím, že vytvoří izolovanou třídu kontextu databáze, která je sdílena všemi nimi. Pokud jste chtěli mít možnost provádět automatizované testování částí, vytvoříte a použijete rozhraní pro tyto třídy stejným způsobem jako úložiště `Student`. Chcete-li však tento kurz zjednodušit, vytvoříte a použijete tyto třídy bez rozhraní.

Následující ilustrace znázorňuje jeden ze způsobů, jak conceptualize vztahy mezi třídami kontroleru a kontextu v porovnání s nepoužíváním úložiště nebo vzorce pracovní jednotky.

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

V této sérii kurzů nevytvoříte testy jednotek. Úvod ke službě TDD s aplikací MVC, která používá vzor úložiště, najdete v tématu [Návod: použití TDD s ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx). Další informace o vzoru úložiště najdete v následujících zdrojích informací:

- [Vzor úložiště](https://msdn.microsoft.com/library/ff649690.aspx) na webu MSDN.
- [Použití úložiště a pracovní jednotky vzorů s Entity Framework 4,0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) na blogu týmu Entity Framework.
- [Agilní Entity Framework 4 úložiště](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) příspěvků na blogu pro Julie Lerman.
- [Sestavování účtu na první pohled k aplikaci HTML5/jQuery](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) na blogu Wahlin.

> [!NOTE]
> Existuje mnoho způsobů implementace úložiště a jednotky pracovních vzorů. Můžete použít třídy úložiště s nebo bez třídy pracovní jednotky. Můžete implementovat jedno úložiště pro všechny typy entit nebo jeden pro každý typ. Pokud implementujete jeden pro každý typ, můžete použít samostatné třídy, obecnou základní třídu a odvozené třídy nebo abstraktní základní třídu a odvozené třídy. Můžete zahrnout obchodní logiku do úložiště nebo ji omezit na logiku přístupu k datům. Můžete také vytvořit abstraktní vrstvu do třídy kontextu databáze pomocí rozhraní [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) namísto [negenerickými](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) typů pro sady entit. Přístup k implementaci abstraktní vrstvy zobrazené v tomto kurzu představuje jednu z možností, jak zvážit, ne doporučení pro všechny scénáře a prostředí.

## <a name="creating-the-student-repository-class"></a>Vytvoření třídy úložiště studenta

Ve složce *dal* vytvořte soubor třídy s názvem *IStudentRepository.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

Tento kód deklaruje typickou sadu metod CRUD, včetně dvou metod čtení – jeden, který vrátí všechny `Student` entit a jeden, který nalezne jednu `Student` entitu podle ID.

Ve složce *dal* vytvořte soubor třídy s názvem *StudentRepository.cs* File. Nahraďte existující kód následujícím kódem, který implementuje rozhraní `IStudentRepository`:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

Kontext databáze je definován v proměnné třídy a konstruktor očekává, že volající objekt předáte do instance kontextu:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

Mohli byste vytvořit instanci nového kontextu v úložišti, ale pokud jste v jednom kontroleru použili více úložišť, každý z nich by měl mít samostatný kontext. Později použijete více úložišť v řadiči `Course` a uvidíte, jak může třída pracovní jednotky zajistit, aby všechna úložiště používala stejný kontext.

Úložiště implementuje [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) a odstraní kontext databáze, jak jste viděli dříve v řadiči, a jeho metody CRUD volají kontext databáze stejným způsobem jako dříve.

## <a name="change-the-student-controller-to-use-the-repository"></a>Změna kontroleru studenta pro použití úložiště

V *StudentController.cs*nahraďte kód, který je aktuálně ve třídě, pomocí následujícího kódu. Změny jsou zvýrazněny.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

Kontroler nyní deklaruje proměnnou třídy pro objekt, který implementuje rozhraní `IStudentRepository` namísto třídy kontextu:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

Výchozí konstruktor (bez parametrů) vytvoří novou instanci kontextu a nepovinný konstruktor umožňuje volajícímu předat instanci kontextu.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

(Pokud jste použili *vkládání závislostí*nebo di, nebudete potřebovat výchozí konstruktor, protože software di by zajistil, že by měl být vždy k dispozici správný objekt úložiště.)

V metodách CRUD se nyní místo kontextu zavolá úložiště:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

A metoda `Dispose` nyní místo kontextu odstraní úložiště:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

Spusťte web a klikněte na kartu **studenti** .

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

Stránka vypadá a funguje stejně jako předtím, než jste změnili kód tak, aby používal úložiště, a ostatní stránky studenta fungují také stejně. Existuje však důležitý rozdíl v tom, jak metoda `Index` kontroleru provádí filtrování a řazení. Původní verze této metody obsahovala následující kód:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

Aktualizovaná `Index` metoda obsahuje následující kód:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

Změnil se pouze zvýrazněný kód.

V původní verzi kódu `students` jako objekt `IQueryable`. Dotaz se do databáze pošle až do té doby, než se převede do kolekce pomocí metody, jako je například `ToList`. k tomu nedojde, dokud zobrazení indexu nepřistupuje k modelu studenta. Metoda `Where` v předchozím kódu se stala `WHERE` klauzulí v dotazu SQL, který je odeslán do databáze. To zase znamená, že databáze vrátí pouze vybrané entity. Avšak v důsledku změny `context.Students` `studentRepository.GetStudents()`je proměnná `students` po tomto příkazu kolekce `IEnumerable`, která zahrnuje všechny studenty v databázi. Konečný výsledek použití metody `Where` je stejný, ale nyní je práce prováděna v paměti na webovém serveru, nikoli v databázi. U dotazů, které vracejí velké objemy dat, to může být neefektivní.

> [!TIP]
> 
> **IQueryable vs. IEnumerable**
> 
> Po implementaci úložiště, jak je znázorněno zde, i když do **vyhledávacího** pole zadáte nějaký dotaz, který odešle do SQL Server vrátí všechny řádky studenta, protože nezahrnuje vaše kritéria hledání:
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> Tento dotaz vrátí všechna data studenta, protože úložiště provedlo dotaz bez znalosti kritérií hledání. Proces řazení, použití kritérií vyhledávání a výběr podmnožiny dat pro stránkování (v tomto případě se v tomto případě zobrazují pouze 3 řádky) se provádí v paměti později při volání metody `ToPagedList` v kolekci `IEnumerable`.
> 
> V předchozí verzi kódu (před implementací úložiště) se dotaz do databáze neposílá až po použití kritérií hledání, když se `ToPagedList` zavolá na objekt `IQueryable`.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> Když je ToPagedList volána u objektu `IQueryable`, dotaz odeslaný do SQL Server určuje hledaný řetězec a v důsledku toho vrátí pouze řádky, které splňují kritéria hledání, a žádné filtrování není nutné provést v paměti.
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> (Následující kurz vysvětluje, jak kontrolovat dotazy odeslané do SQL Server.)

V následující části se dozvíte, jak implementovat metody úložiště, které vám umožní určit, že tuto práci má udělat databáze.

Nyní jste vytvořili abstrakci vrstev mezi kontrolérem a kontextem Entity Framework databáze. Pokud provedete automatizované testování částí pomocí této aplikace, můžete vytvořit alternativní třídu úložiště v projektu testu jednotek, který implementuje `IStudentRepository` *.* Namísto volání kontextu pro čtení a zápis dat může tato třída úložiště s přípravou pracovat s kolekcemi v paměti za účelem testování funkcí kontroleru.

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>Implementace obecného úložiště a třídy pracovní jednotky

Vytvoření třídy úložiště pro každý typ entity může mít za následek hodně redundantního kódu a může způsobit částečné aktualizace. Předpokládejme například, že musíte aktualizovat dva různé typy entit jako součást stejné transakce. Pokud každá z nich používá samostatnou instanci kontextu databáze, může dojít k úspěšnému a druhá chyba může selhat. Jedním ze způsobů, jak minimalizovat redundantní kód, je použít obecné úložiště a jeden ze způsobů, jak zajistit, aby všechna úložiště používala stejný kontext databáze (a tak koordinovat všechny aktualizace) je použití třídy pracovní jednotky.

V této části kurzu vytvoříte třídu `GenericRepository` a třídu `UnitOfWork` a použijete je v řadiči `Course` pro přístup k `Department` i k `Course` sadě entit. Jak bylo vysvětleno dříve, aby byla tato část kurzu jednoduchá, nevytváříte pro tyto třídy rozhraní. Ale pokud byste je chtěli použít k usnadnění TDD, obvykle je implementujete s rozhraními stejným způsobem jako úložiště `Student`.

### <a name="create-a-generic-repository"></a>Vytvoření obecného úložiště

Ve složce *dal* vytvořte *GenericRepository.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

Proměnné třídy jsou deklarovány pro kontext databáze a pro sadu entit, pro kterou je vytvořena instance úložiště:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

Konstruktor přijímá instanci kontextu databáze a inicializuje proměnnou sady entit:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

Metoda `Get` používá výrazy lambda, které umožňují, aby volající kód určil podmínku filtru a sloupec, podle kterého se mají seřadit výsledky, a řetězcový parametr umožňuje volajícímu poskytnout seznam vlastností navigace oddělených čárkami pro Eager načítání:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

Kód `Expression<Func<TEntity, bool>> filter` znamená, že volající poskytne výraz lambda na základě typu `TEntity` a tento výraz vrátí logickou hodnotu. Pokud je například vytvořena instance úložiště pro `Student` typ entity, kód v metodě volání může určit `student => student.LastName == "Smith`&quot; pro parametr `filter`.

Kód `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` také znamená, že volající bude poskytovat výraz lambda. Ale v tomto případě je vstup do výrazu `IQueryable` objekt pro `TEntity` typ. Výraz vrátí uspořádanou verzi objektu `IQueryable`. Pokud je například vytvořena instance úložiště pro `Student` typ entity, kód v metodě volání může určit `q => q.OrderBy(s => s.LastName)` pro parametr `orderBy`.

Kód v metodě `Get` vytvoří objekt `IQueryable` a poté použije výraz filtru, pokud existuje:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

Následně se po analýze seznamu odděleného čárkami aplikují výrazy Eager:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

Nakonec použije výraz `orderBy`, pokud existuje, a vrátí výsledky; v opačném případě vrátí výsledky z neuspořádaného dotazu:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

Když zavoláte metodu `Get`, můžete filtrovat a řadit kolekci `IEnumerable` vrácenou metodou namísto zadání parametrů pro tyto funkce. Práce s řazením a filtrováním se ale pak provede v paměti na webovém serveru. Pomocí těchto parametrů zajistíte, aby se práce prováděla v databázi, nikoli na webovém serveru. Alternativou je vytvořit odvozené třídy pro konkrétní typy entit a přidat specializované `Get` metody, jako je například `GetStudentsInNameOrder` nebo `GetStudentsByName`. Ve složité aplikaci ale může dojít k velkému počtu odvozených tříd a specializovaných metod, které by mohly být zachovány.

Kód v metodách `GetByID`, `Insert`a `Update` je podobný tomu, co jste viděli v neobecném úložišti. (V signatuře `GetByID` neposkytujete parametr načítání Eager, protože Eager metodu nelze načíst pomocí metody `Find`.)

Pro metodu `Delete` jsou k dispozici dvě přetížení:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

Jedna z těchto z nich vám umožní předat jenom ID entity, která se má odstranit, a jedna vezme instanci entity. Jak jste viděli v kurzu [zpracování souběžnosti](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) , pro zpracování souběžnosti potřebujete `Delete` metodu, která převezme instanci entity, která obsahuje původní hodnotu vlastnosti sledování.

Toto obecné úložiště zpracuje typické požadavky CRUD. Pokud má konkrétní typ entity zvláštní požadavky, jako je složitější filtrování nebo řazení, můžete vytvořit odvozenou třídu, která má další metody pro tento typ.

## <a name="creating-the-unit-of-work-class"></a>Vytvoření třídy pracovní jednotky

Třída pracovní jednotka slouží k jednomu účelu: abyste se ujistili, že když používáte více úložišť, sdílejí jeden kontext databáze. Tímto způsobem, když je dokončená jednotka práce, můžete zavolat metodu `SaveChanges` v dané instanci kontextu a zajistit, aby všechny související změny byly koordinovány. Vše, co třída potřebuje, je metoda `Save` a vlastnost pro každé úložiště. Každá vlastnost úložiště vrací instanci úložiště, která byla vytvořena pomocí stejné instance kontextu databáze jako jiné instance úložiště.

Ve složce *dal* vytvořte soubor třídy s názvem *UnitOfWork.cs* a nahraďte kód šablony následujícím kódem:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

Kód vytvoří proměnné třídy pro kontext databáze a každé úložiště. Pro `context` proměnnou je vytvořena instance nového kontextu:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

Každá vlastnost úložiště kontroluje, zda úložiště již existuje. V takovém případě vytvoří instanci úložiště s předáním instance kontextu. V důsledku toho všechna úložiště sdílejí stejnou instanci kontextu.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

Metoda `Save` volá `SaveChanges` kontextu databáze.

Stejně jako jakákoli třída, která vytváří instance kontextu databáze v proměnné třídy, třída `UnitOfWork` implementuje `IDisposable` a odstraní kontext.

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>Změna kontroleru kurzu na použití třídy UnitOfWork a úložišť

Nahraďte kód, který aktuálně máte v *CourseController.cs* , následujícím kódem:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

Tento kód přidá proměnnou třídy pro třídu `UnitOfWork`. (Pokud jste zde používali rozhraní, nemusíte tady inicializovat proměnnou. místo toho byste měli implementovat vzor dvou konstruktorů stejným způsobem jako úložiště `Student`.)

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

Ve zbytku třídy se všechny odkazy na kontext databáze nahrazují odkazy na příslušné úložiště pomocí `UnitOfWork` vlastností pro přístup k úložišti. Metoda `Dispose` odstraní instanci `UnitOfWork`.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

Spusťte web a klikněte na kartu **kurzy** .

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

Stránka vypadá a funguje stejně jako před vašimi změnami a ostatní stránky kurzu fungují i stejně.

## <a name="summary"></a>Přehled

Právě jste implementovali jak úložiště, tak pracovní jednotky pracovních schémat. Výrazy lambda jste používali jako parametry metody v obecném úložišti. Další informace o tom, jak tyto výrazy použít s objektem `IQueryable`, naleznete v tématu [rozhraní IQueryable (t) (System. Linq](https://msdn.microsoft.com/library/bb351562.aspx) ) v knihovně MSDN. V dalším kurzu se dozvíte, jak zpracovat některé pokročilé scénáře.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Předchozí](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Další](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
