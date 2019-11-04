---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: čtení souvisejících dat pomocí EF v aplikaci ASP.NET MVC'
description: V tomto kurzu si přečtete a zobrazíte související data – to znamená data, která Entity Framework načíst do vlastností navigace.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445658"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>Kurz: čtení souvisejících dat pomocí EF v aplikaci ASP.NET MVC

V předchozím kurzu jste dokončili model školních dat. V tomto kurzu si přečtete a zobrazíte související data – to znamená data, která Entity Framework načíst do vlastností navigace.

Následující ilustrace znázorňují stránky, se kterými budete pracovat.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 5 pomocí Code First Entity Framework 6 a sady Visual Studio. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

V tomto kurzu:

> [!div class="checklist"]
> * Naučte se načítat související data
> * Vytvoření stránky kurzů
> * Vytvoření stránky instruktory

## <a name="prerequisites"></a>Požadavky

* [Vytvoření komplexnějšího datového modelu](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>Naučte se načítat související data

Existuje několik způsobů, jak může Entity Framework načíst související data do navigačních vlastností entity:

- *Opožděné načítání*. Při prvním načtení entity se nenačte související data. Při prvním pokusu o přístup k navigační vlastnosti je však automaticky načtena data potřebná pro tuto vlastnost navigace. Výsledkem je, že se do databáze pošle víc dotazů – jednu pro samotnou entitu a druhou, a to pokaždé, když se musí načíst související data pro danou entitu. Třída `DbContext` ve výchozím nastavení umožňuje opožděné načítání.

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *Eager načítání*. Když se entita přečte, načtou se spolu s ní související data. To obvykle vede k tomu, že se vytvoří dotaz s jedním spojením, který načte všechna potřebná data. Eager načítání lze zadat pomocí metody `Include`.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *Explicitní načítání*. To se podobá opožděnému načítání, s tím rozdílem, že explicitně načtete související data v kódu; k tomu nedochází automaticky při přístupu k navigační vlastnosti. Související data načtoute ručně tak, že získáte položku Správce stavu objektu pro entitu a zavoláte metodu [Collection. Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) pro kolekce nebo metodu [reference. Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) pro vlastnosti, které uchovávají jednu entitu. (Pokud jste chtěli načíst navigační vlastnost správce, měli byste v následujícím příkladu nahradit `Collection(x => x.Courses)` `Reference(x => x.Administrator)`.) Obvykle byste měli explicitní načítání používat pouze v případě, že jste zapnuli opožděné načítání.

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

Vzhledem k tomu, že ihned nezískají hodnoty vlastností, opožděné načítání a explicitní načítání jsou také označovány jako *odložené načítání*.

### <a name="performance-considerations"></a>Důležité informace o výkonu

Pokud víte, že pro každou načtenou entitu potřebujete související data, Eager načítání často nabízí nejlepší výkon, protože jediný dotaz odeslaný do databáze je obvykle efektivnější než samostatné dotazy pro každou načtenou entitu. Například ve výše uvedených příkladech předpokládáme, že každé oddělení má deset souvisejících kurzů. Příkladem Eager načtení může být pouze jeden (JOIN) dotaz a jedna zpáteční cesta k databázi. Příklady opožděného načítání a explicitního načítání budou mít za následek jedenácté dotazy a jedenácté odezvy na databázi. Další výměna cest k databázi je obzvláště neškodná na výkon, pokud je latence vysoká.

Na druhé straně je v některých scénářích opožděné načítání efektivnější. Načtení Eager může způsobit, že se vygeneruje velmi složité spojení, které SQL Server nemůže efektivně zpracovat. Nebo pokud potřebujete přístup k vlastnostem navigace entity jenom pro podmnožinu sady entit, které zpracováváte, může být opožděné načítání lepší, protože Eager načítání by načetlo víc dat, než kolik potřebujete. Pokud je výkon kritický, je nejlepší testovat výkon oběma způsoby, abyste mohli nejlépe vybrat.

Opožděné načítání může maskovat kód, který způsobuje problémy s výkonem. Například kód, který nespecifikuje Eager nebo explicitní načítání, ale zpracovává velký objem entit a používá několik navigačních vlastností v každé iteraci, může být velmi neefektivní (kvůli velkému počtu zpátečních cest k databázi). Aplikace, která při vývoji používá místní SQL Server, může mít problémy s výkonem při přesunu na Azure SQL Database z důvodu zvýšené latence a opožděného načítání. Profilování dotazů databáze pomocí realistického zatížení testu vám pomůže určit, jestli je vhodné opožděné načítání. Další informace najdete v tématu [strategie Demystifying Entity Framework: načtení souvisejících dat](https://msdn.microsoft.com/magazine/hh205756.aspx) a [použití Entity Framework ke snížení latence sítě na SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).

### <a name="disable-lazy-loading-before-serialization"></a>Zakázat opožděné načítání před serializací

Pokud necháte při serializaci povoleno opožděné načítání, můžete ukončit dotazování podstatně více dat, než jste zamýšleli. Serializace obecně funguje při přístupu k jednotlivým vlastnostem instance typu. Přístup k vlastnostem aktivuje opožděné načítání a tyto opožděné načtené entity jsou serializovány. Proces serializace pak přistupuje ke všem vlastnostem opožděně načtených entit, což potenciálně způsobuje ještě více opožděného načítání a serializaci. Chcete-li zabránit této reakci řetězu spuštění, před serializací entity zapněte opožděné načtení.

Serializace může být také složitá třídami proxy, které používá Entity Framework, jak je vysvětleno v [kurzu pokročilé scénáře](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies).

Jedním ze způsobů, jak zabránit problémům s serializací, je serializace objektů přenosu dat (DTO) místo objektů entit, jak je znázorněno v kurzu [použití webového rozhraní API s Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) .

Pokud DTO nepoužíváte, můžete zakázat opožděné načítání a vyhnout se problémům s proxy tím, že [zakážete vytváření proxy serveru](https://msdn.microsoft.com/data/jj592886.aspx).

Zde jsou některé další [způsoby, jak zakázat opožděné načítání](https://msdn.microsoft.com/data/jj574232):

- U specifických vlastností navigace vynechejte klíčové slovo `virtual` při deklaraci vlastnosti.
- Pro všechny navigační vlastnosti nastavte `LazyLoadingEnabled` na `false`a vložte následující kód do konstruktoru třídy Context:

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>Vytvoření stránky kurzů

Entita `Course` obsahuje navigační vlastnost, která obsahuje entitu `Department` oddělení, ke kterému je kurz přiřazen. Pokud chcete v seznamu kurzů zobrazit název přiřazeného oddělení, musíte získat vlastnost `Name` z `Department` entity, která je ve vlastnosti navigace v `Course.Department`.

Vytvořte kontroler s názvem `CourseController` (ne CoursesController) pro typ entity `Course` pomocí stejných možností pro **kontroler MVC 5 se zobrazeními, a to pomocí entity Frameworkho** lešení, které jste předtím použili pro řadič `Student`:

| Nastavením | Hodnota |
| ------- | ----- |
| Třída modelu | Vyberte **kurz (ContosoUniversity. Models)** . |
| Třída kontextu dat | Vyberte **SchoolContext (ContosoUniversity. dal)** . |
| Název kontroleru | Zadejte *CourseController*. Znovu *CoursesController* *s s.* Po výběru **kurzu (ContosoUniversity. Models)** se hodnota **název kontroleru** vyplní automaticky. Je nutné změnit hodnotu. |

Ponechte ostatní výchozí hodnoty a přidejte kontroler.

Otevřete *Controllers\CourseController.cs* a podívejte se na metodu `Index`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Automatické generování uživatelského rozhraní určilo Eager načítání pro navigační vlastnost `Department` pomocí metody `Include`.

Otevřete *Views\Course\Index.cshtml* a nahraďte kód šablony následujícím kódem. Změny jsou zvýrazněny:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

Provedli jste následující změny ve vygenerovaném kódu:

- Změnili jste záhlaví z **indexu** na **kurzy**.
- Byl přidán sloupec **číslo** , který zobrazuje hodnotu vlastnosti `CourseID`. Ve výchozím nastavení nejsou primární klíče vygenerované, protože jsou normálně nevýznamné pro koncové uživatele. V tomto případě je však primární klíč smysluplný a chcete jej zobrazit.
- Přesunuli jsme sloupec **oddělení** na pravou stranu a změnili jeho záhlaví. Modul pro generování uživatelského rozhraní se správně rozhodl zobrazit vlastnost `Name` z entity `Department`, ale na stránce kurzu by záhlaví sloupce mělo být **oddělením** , nikoli **názvem**.

Všimněte si, že pro sloupec oddělení obsahuje generovaný kód vlastnost `Name` `Department` entity, která je načtena do vlastnosti `Department` navigace:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

Pokud chcete zobrazit seznam s názvy oddělení, spusťte stránku (vyberte kartu **kurzy** na domovské stránce společnosti Contoso University).

## <a name="create-an-instructors-page"></a>Vytvoření stránky instruktory

V této části vytvoříte kontrolér a zobrazení pro entitu `Instructor`, aby se zobrazila stránka instruktoři. Tato stránka čte a zobrazuje související data následujícími způsoby:

- Seznam instruktorů zobrazuje související data z `OfficeAssignment` entitu. Entity `Instructor` a `OfficeAssignment` jsou v relaci jednosměrového a nulového vztahu. Pro `OfficeAssignment` entit budete používat načítání Eager. Jak bylo vysvětleno dříve, načítání Eager je obvykle efektivnější, pokud potřebujete související data pro všechny načtené řádky primární tabulky. V takovém případě chcete zobrazit přiřazení Office pro všechny zobrazené instruktory.
- Když uživatel vybere instruktora, zobrazí se související entity `Course`. Entity `Instructor` a `Course` jsou v relaci m:n. Pro `Course` entit a jejich souvisejících `Department` entit budete používat Eager načítání. V tomto případě může být opožděné načítání efektivnější, protože potřebujete kurzy jenom pro vybraného instruktora. Tento příklad ukazuje, jak používat Eager načítání pro navigační vlastnosti v rámci entit, které jsou samy v navigační vlastnosti.
- Když uživatel vybere kurz, zobrazí se související data ze sady entit `Enrollments`. Entity `Course` a `Enrollment` jsou v relaci 1: n. Přidáte explicitní načítání `Enrollment` entit a jejich souvisejících `Student` entit. (Explicitní načítání není nutné, protože je povolené opožděné načítání, ale ukazuje, jak provést explicitní načítání.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>Vytvoření modelu zobrazení pro zobrazení indexu instruktora

Stránka instruktoři zobrazuje tři různé tabulky. Proto vytvoříte model zobrazení, který obsahuje tři vlastnosti, z nichž každý uchovává data pro jednu z tabulek.

Ve složce *ViewModels* vytvořte *InstructorIndexData.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>Vytvoření kontroleru a zobrazení instruktora

Vytvoření kontroleru `InstructorController` (ne InstructorsController) s akcí EF pro čtení/zápis:

| Nastavením | Hodnota |
| ------- | ----- |
| Třída modelu | Vyberte **instruktor (ContosoUniversity. Models)** . |
| Třída kontextu dat | Vyberte **SchoolContext (ContosoUniversity. dal)** . |
| Název kontroleru | Zadejte *InstructorController*. Znovu *InstructorsController* *s s.* Po výběru **kurzu (ContosoUniversity. Models)** se hodnota **název kontroleru** vyplní automaticky. Je nutné změnit hodnotu. |

Ponechte ostatní výchozí hodnoty a přidejte kontroler.

Otevřete *Controllers\InstructorController.cs* a přidejte příkaz `using` pro obor názvů `ViewModels`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Generovaný kód v metodě `Index` určuje Eager načítání pouze pro `OfficeAssignment` navigační vlastnost:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Chcete-li načíst další související data a vložit je do modelu zobrazení, nahraďte metodu `Index` následujícím kódem:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Metoda přijímá volitelná data směrování (`id`) a parametr řetězce dotazu (`courseID`), který poskytuje hodnoty ID vybraného instruktora a vybraný kurz a předá všechna požadovaná data zobrazení. Parametry jsou k dispozici na stránce **vybrané** hypertextové odkazy.

Kód začíná vytvořením instance modelu zobrazení a jeho vložením do seznamu instruktorů. Kód určuje Eager načítání pro `Instructor.OfficeAssignment` a navigační vlastnost `Instructor.Courses`.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

Druhá metoda `Include` načte kurzy a pro každý kurz, který je načte, se Eager načítání pro `Course.Department` navigační vlastnost.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

Jak bylo zmíněno dříve, Eager načítání není vyžadováno, ale je provedeno za účelem zvýšení výkonu. Vzhledem k tomu, že zobrazení vždy vyžaduje `OfficeAssignment` entitu, je efektivnější ho načíst ve stejném dotazu. `Course` entity jsou požadovány, když je na webové stránce vybrán instruktor, takže načítání Eager je lepší než opožděné načítání pouze v případě, že se stránka zobrazuje častěji s kurzem vybraným než bez.

Pokud bylo vybráno ID instruktora, je vybraný instruktor načten ze seznamu instruktorů v modelu zobrazení. Vlastnost `Courses` modelu zobrazení je poté načtena s `Course` entit z `Courses` navigační vlastnost tohoto instruktora.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Metoda `Where` vrací kolekci, ale v tomto případě kritéria předaná této metodě mají za následek jenom jednu entitu `Instructor`, která se vrací. Metoda `Single` převede kolekci na jedinou entitu `Instructor`, která vám umožní přístup k vlastnosti `Courses` této entity.

[Jedinou](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) metodu pro kolekci použijete, když víte, že kolekce bude obsahovat pouze jednu položku. Metoda `Single` vyvolá výjimku, pokud je předaná kolekce prázdná nebo je-li k dispozici více než jedna položka. Alternativa je [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), která vrací výchozí hodnotu (`null` v tomto případě), pokud je kolekce prázdná. Nicméně v tomto případě by přesto došlo k výjimce (při pokusu o nalezení vlastnosti `Courses` na `null` odkazu) a zpráva o výjimce by byla méně zřetelně označovala příčinu problému. Při volání metody `Single` lze také předat podmínku `Where` namísto volání metody `Where` samostatně:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

Namísto:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

V dalším případě se vybraný kurz načte ze seznamu kurzů v modelu zobrazení. Vlastnost `Enrollments` modelu zobrazení je načtena s `Enrollment` entitami z `Enrollments` navigační vlastnost tohoto kurzu.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>Úprava zobrazení indexu instruktorů

V *Views\Instructor\Index.cshtml*nahraďte kód šablony následujícím kódem. Změny jsou zvýrazněny:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

V existujícím kódu jste provedli následující změny:

- Změnila třídu modelu na `InstructorIndexData`.
- Změnila se název stránky z **indexu** na **instruktory**.
- Přidání sloupce **Office** , který zobrazí `item.OfficeAssignment.Location` pouze v případě, že `item.OfficeAssignment` není null. (Vzhledem k tomu, že se jedná o relaci typu 1:1, nemusí se jednat o související entitu `OfficeAssignment`.)

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- Přidaný kód, který bude dynamicky přidávat `class="success"` do `tr`ho prvku vybraného instruktora. Tím se nastaví barva pozadí pro vybraný řádek pomocí třídy [bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) .

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- Přidali jsme nový `ActionLink` označený jako **vybraný bezprostředně před** ostatními odkazy v každém řádku, což způsobí odeslání vybraného ID instruktoru do metody `Index`.

Spusťte aplikaci a vyberte kartu **instruktory** . Stránka zobrazuje vlastnost `Location` souvisejících entit `OfficeAssignment` a prázdnou buňku tabulky, pokud neexistuje žádná související entita `OfficeAssignment`.

V souboru *Views\Instructor\Index.cshtml* přidejte po zavření `table` element (na konci souboru) následující kód. Tento kód zobrazuje seznam kurzů souvisejících s instruktorem, když je vybrán instruktor.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

Tento kód načte vlastnost `Courses` modelu zobrazení a zobrazí seznam kurzů. Poskytuje taky `Select` hypertextový odkaz, který pošle ID vybraného kurzu do metody `Index` akce.

Spusťte stránku a vyberte instruktor. Nyní se zobrazí mřížka zobrazující kurzy přiřazené k vybranému instruktorovi a pro každý kurz vidíte název přiřazeného oddělení.

Po tom, co jste právě přidali blok kódu, přidejte následující kód. Zobrazí se seznam studentů, kteří jsou v kurzu při výběru tohoto kurzu zaregistrovaní.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Tento kód načte vlastnost `Enrollments` modelu zobrazení, aby se zobrazil seznam studentů zaregistrovaných v kurzu.

Spusťte stránku a vyberte instruktor. Pak vyberte kurz, ve kterém se zobrazí seznam zaregistrovaných studentů a jejich třídy.

### <a name="adding-explicit-loading"></a>Přidávání explicitního načítání

Otevřete *InstructorController.cs* a podívejte se, jak metoda `Index` získá seznam zápisů pro vybraný kurz:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

Když jste načetli seznam instruktorů, zadali jste Eager načítání pro vlastnost navigace `Courses` a vlastnost `Department` každého kurzu. Pak vložíte kolekci `Courses` do modelu zobrazení a teď k `Enrollments` navigační vlastnost přistupujete z jedné entity v této kolekci. Vzhledem k tomu, že jste nezadali Eager načítání pro vlastnost navigace `Course.Enrollments`, data z této vlastnosti se zobrazí na stránce v důsledku opožděného načítání.

Pokud jste zakázali opožděné načítání beze změny kódu jiným způsobem, vlastnost `Enrollments` by měla hodnotu null, bez ohledu na to, kolik registrů v kurzu skutečně mělo. V takovém případě, pokud chcete načíst vlastnost `Enrollments`, je nutné zadat buď načítání Eager nebo explicitní načítání. Už jste viděli, jak Eager načíst. Aby bylo možné zobrazit příklad explicitního načítání, nahraďte metodu `Index` následujícím kódem, který explicitně načte vlastnost `Enrollments`. Změněný kód je zvýrazněný.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

Po získání vybrané entity `Course` se v novém kódu explicitně načte vlastnost navigace pro `Enrollments` tohoto kurzu:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

Pak explicitně načte všechny související entity `Student` `Enrollment` entit:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

Všimněte si, že pomocí metody `Collection` načíst vlastnost kolekce, ale u vlastnosti, která obsahuje pouze jednu entitu, použijete metodu `Reference`.

Spusťte stránku index instruktora nyní a uvidíte, že se na stránce zobrazuje žádný rozdíl, i když jste změnili způsob, jakým se data načítají.

## <a name="get-the-code"></a>Získat kód

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Další kroky

V tomto kurzu:

> [!div class="checklist"]
> * Zjistili jste, jak načíst související data
> * Stránka vytvoření kurzů
> * Stránka s instruktory se vytvořila.

Přejděte k dalšímu článku, kde se dozvíte, jak aktualizovat související data.

> [!div class="nextstepaction"]
> [Aktualizace souvisejících dat](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
