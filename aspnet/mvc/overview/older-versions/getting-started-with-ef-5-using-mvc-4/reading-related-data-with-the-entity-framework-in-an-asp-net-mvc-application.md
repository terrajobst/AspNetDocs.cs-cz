---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: Čtení souvisejících dat s Entity Framework v aplikaci ASP.NET MVC (5 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e1752022b66952783039fbea0c2880e2f9be6ef8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595213"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>Čtení souvisejících dat s Entity Framework v aplikaci ASP.NET MVC (5 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozím kurzu jste dokončili model školních dat. V tomto kurzu si přečtete a zobrazíte související data – to znamená data, která Entity Framework načíst do vlastností navigace.

Následující ilustrace znázorňují stránky, se kterými budete pracovat.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>Opožděné, Eager a explicitní načítání souvisejících dat

Existuje několik způsobů, jak může Entity Framework načíst související data do navigačních vlastností entity:

- *Opožděné načítání*. Při prvním načtení entity se nenačte související data. Při prvním pokusu o přístup k navigační vlastnosti je však automaticky načtena data potřebná pro tuto vlastnost navigace. Výsledkem je, že se do databáze pošle víc dotazů – jednu pro samotnou entitu a druhou, a to pokaždé, když se musí načíst související data pro danou entitu. 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *Eager načítání*. Když se entita přečte, načtou se spolu s ní související data. To obvykle vede k tomu, že se vytvoří dotaz s jedním spojením, který načte všechna potřebná data. Eager načítání lze zadat pomocí metody `Include`.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *Explicitní načítání*. To se podobá opožděnému načítání, s tím rozdílem, že explicitně načtete související data v kódu; k tomu nedochází automaticky při přístupu k navigační vlastnosti. Související data načtoute ručně tak, že získáte položku Správce stavu objektu pro entitu a zavoláte metodu `Collection.Load` pro kolekce nebo metodu `Reference.Load` pro vlastnosti, které obsahují jednu entitu. (Pokud jste chtěli načíst navigační vlastnost správce, měli byste v následujícím příkladu nahradit `Collection(x => x.Courses)` `Reference(x => x.Administrator)`.)

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

Vzhledem k tomu, že ihned nezískají hodnoty vlastností, opožděné načítání a explicitní načítání jsou také označovány jako *odložené načítání*.

Obecně platí, že pokud víte, že potřebujete související data pro každou načtenou entitu, Eager načítání nabízí nejlepší výkon, protože jeden dotaz odeslaný do databáze je obvykle efektivnější než samostatné dotazy pro každou načtenou entitu. Například ve výše uvedených příkladech předpokládáme, že každé oddělení má deset souvisejících kurzů. Příkladem Eager načtení může být pouze jeden (JOIN) dotaz a jedna zpáteční cesta k databázi. Příklady opožděného načítání a explicitního načítání budou mít za následek jedenácté dotazy a jedenácté odezvy na databázi. Další výměna cest k databázi je obzvláště neškodná na výkon, pokud je latence vysoká.

Na druhé straně je v některých scénářích opožděné načítání efektivnější. Načtení Eager může způsobit, že se vygeneruje velmi složité spojení, které SQL Server nemůže efektivně zpracovat. Nebo pokud potřebujete přístup k vlastnostem navigace entity jenom pro podmnožinu sady entit, které zpracováváte, může opožděné načítání zlepšit, protože Eager načítání by načetlo víc dat, než kolik potřebujete. Pokud je výkon kritický, je nejlepší testovat výkon oběma způsoby, abyste mohli nejlépe vybrat.

Obvykle byste měli explicitní načítání používat pouze v případě, že jste zapnuli opožděné načítání. Jeden scénář, kdy byste měli zapnout opožděné načítání, je během serializace. Opožděné načítání a serializace se dobře nespojují. Pokud nemusíte pozor, můžete v případě, že je povoleno opožděné načítání, dotazování výrazně víc dat, než jste zamýšleli. Serializace obecně funguje při přístupu k jednotlivým vlastnostem instance typu. Přístup k vlastnostem aktivuje opožděné načítání a tyto opožděné načtené entity jsou serializovány. Proces serializace pak přistupuje ke všem vlastnostem opožděně načtených entit, což potenciálně způsobuje ještě více opožděného načítání a serializaci. Chcete-li zabránit této reakci řetězu spuštění, před serializací entity zapněte opožděné načtení.

Třída kontextu databáze provádí opožděné načítání ve výchozím nastavení. Existují dva způsoby, jak zakázat opožděné načítání:

- U specifických vlastností navigace vynechejte klíčové slovo `virtual` při deklaraci vlastnosti.
- U všech navigačních vlastností nastavte `LazyLoadingEnabled` na `false`. Například můžete do konstruktoru třídy kontextu vložit následující kód: 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Opožděné načítání může maskovat kód, který způsobuje problémy s výkonem. Například kód, který nespecifikuje Eager nebo explicitní načítání, ale zpracovává velký objem entit a používá několik navigačních vlastností v každé iteraci, může být velmi neefektivní (kvůli velkému počtu zpátečních cest k databázi). Aplikace, která při vývoji používá místní SQL Server, může mít problémy s výkonem při přesunu na Azure SQL Database z důvodu zvýšené latence a opožděného načítání. Profilování dotazů databáze pomocí realistického zatížení testu vám pomůže určit, jestli je vhodné opožděné načítání. Další informace najdete v tématu [strategie Demystifying Entity Framework: načtení souvisejících dat](https://msdn.microsoft.com/magazine/hh205756.aspx) a [použití Entity Framework ke snížení latence sítě na SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).

## <a name="create-a-courses-index-page-that-displays-department-name"></a>Stránka vytvoření indexu kurzů, která zobrazuje název oddělení

Entita `Course` obsahuje navigační vlastnost, která obsahuje entitu `Department` oddělení, ke kterému je kurz přiřazen. Pokud chcete v seznamu kurzů zobrazit název přiřazeného oddělení, musíte získat vlastnost `Name` z `Department` entity, která je ve vlastnosti navigace v `Course.Department`.

Vytvořte kontroler s názvem `CourseController` pro `Course` typ entity pomocí stejných možností, které jste předtím provedli pro `Student` kontroler, jak je znázorněno na následujícím obrázku (kromě obrázku, vaše kontextová třída je v oboru názvů DAL, nikoli v oboru názvů modelů):

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

Otevřete *Controllers\CourseController.cs* a podívejte se na metodu `Index`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Automatické generování uživatelského rozhraní určilo načítání Eager pro navigační vlastnost `Department` pomocí metody `Include`.

Otevřete *Views\Course\Index.cshtml* a nahraďte existující kód následujícím kódem. Změny jsou zvýrazněny:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

Provedli jste následující změny ve vygenerovaném kódu:

- Změnili jste záhlaví z **indexu** na **kurzy**.
- Přesunuli jsme odkazy na řádky vlevo.
- Do **čísla** nadpisu se přidal sloupec, který zobrazuje hodnotu vlastnosti `CourseID`. (Ve výchozím nastavení nejsou primární klíče vygenerované, protože obvykle mají koncové uživatele smysl. V tomto případě je však primární klíč smysluplný a chcete jej zobrazit.)
- Změnil se záhlaví posledního sloupce z **DepartmentID** (název cizího klíče na `Department` entitu) na **oddělení**.

Všimněte si, že pro poslední sloupec generovaný kód zobrazuje vlastnost `Name` `Department` entity, která je načtena do navigační vlastnosti `Department`:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

Pokud chcete zobrazit seznam s názvy oddělení, spusťte stránku (vyberte kartu **kurzy** na domovské stránce společnosti Contoso University).

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>Stránka pro vytvoření indexu instruktorů, na které se zobrazují kurzy a registrace

V této části vytvoříte kontrolér a zobrazení pro entitu `Instructor`, aby se zobrazila stránka s indexem instruktorů:

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Tato stránka čte a zobrazuje související data následujícími způsoby:

- Seznam instruktorů zobrazuje související data z `OfficeAssignment` entitu. Entity `Instructor` a `OfficeAssignment` jsou v relaci jednosměrového a nulového vztahu. Pro `OfficeAssignment` entit budete používat načítání Eager. Jak bylo vysvětleno dříve, načítání Eager je obvykle efektivnější, pokud potřebujete související data pro všechny načtené řádky primární tabulky. V takovém případě chcete zobrazit přiřazení Office pro všechny zobrazené instruktory.
- Když uživatel vybere instruktora, zobrazí se související entity `Course`. Entity `Instructor` a `Course` jsou v relaci m:n. Pro `Course` entit a jejich souvisejících `Department` entit budete používat Eager načítání. V tomto případě může být opožděné načítání efektivnější, protože potřebujete kurzy jenom pro vybraného instruktora. Tento příklad ukazuje, jak používat Eager načítání pro navigační vlastnosti v rámci entit, které jsou samy v navigační vlastnosti.
- Když uživatel vybere kurz, zobrazí se související data ze sady entit `Enrollments`. Entity `Course` a `Enrollment` jsou v relaci 1: n. Přidáte explicitní načítání `Enrollment` entit a jejich souvisejících `Student` entit. (Explicitní načítání není nutné, protože je povolené opožděné načítání, ale ukazuje, jak provést explicitní načítání.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>Vytvoření modelu zobrazení pro zobrazení indexu instruktora

Stránka index instruktora zobrazuje tři různé tabulky. Proto vytvoříte model zobrazení, který obsahuje tři vlastnosti, z nichž každý uchovává data pro jednu z tabulek.

Ve složce *ViewModels* vytvořte *InstructorIndexData.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>Přidání stylu pro vybrané řádky

Chcete-li označit vybrané řádky, potřebujete jinou barvu pozadí. Chcete-li zadat styl pro toto uživatelské rozhraní, přidejte následující zvýrazněný kód do oddílu `/* info and errors */` v *Content\Site.CSS*, jak je znázorněno níže:

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>Vytvoření kontroleru a zobrazení instruktory

Vytvořte řadič `InstructorController`, jak je znázorněno na následujícím obrázku:

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

Otevřete *Controllers\InstructorController.cs* a přidejte příkaz `using` pro obor názvů `ViewModels`:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Generovaný kód v metodě `Index` určuje Eager načítání pouze pro `OfficeAssignment` navigační vlastnost:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Chcete-li načíst další související data a vložit je do modelu zobrazení, nahraďte metodu `Index` následujícím kódem:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Metoda přijímá volitelná data směrování (`id`) a parametr řetězce dotazu (`courseID`), který poskytuje hodnoty ID vybraného instruktora a vybraný kurz a předá všechna požadovaná data zobrazení. Parametry jsou k dispozici na stránce **vybrané** hypertextové odkazy.

> [!TIP]
> 
> **Směrování dat**
> 
> Data směrování jsou data, která modelový pořadač nalezl v segmentu URL zadaném ve směrovací tabulce. Výchozí trasa například určuje `controller`, `action`a `id` segmenty:
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> V následující adrese URL se výchozí mapy tras `Instructor` jako `controller``Index` jako `action` a 1 jako `id`. Jedná se o hodnoty dat tras.
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "? courseID = 2021" je hodnota řetězce dotazu. Pořadač modelů bude fungovat i v případě, že předáte `id` jako hodnotu řetězce dotazu:
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> Adresy URL jsou vytvořeny `ActionLink` příkazy v zobrazení Razor. V následujícím kódu se parametr `id` shoduje s výchozí trasou, takže `id` přidána do dat trasy.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> V následujícím kódu `courseID` neodpovídá parametru ve výchozí trase, takže se přidá jako řetězec dotazu.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

Kód začíná vytvořením instance modelu zobrazení a jeho vložením do seznamu instruktorů. Kód určuje Eager načítání pro `Instructor.OfficeAssignment` a navigační vlastnost `Instructor.Courses`.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

Druhá metoda `Include` načte kurzy a pro každý kurz, který je načte, se Eager načítání pro `Course.Department` navigační vlastnost.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Jak bylo zmíněno dříve, Eager načítání není vyžadováno, ale je provedeno za účelem zvýšení výkonu. Vzhledem k tomu, že zobrazení vždy vyžaduje `OfficeAssignment` entitu, je efektivnější ho načíst ve stejném dotazu. `Course` entity jsou požadovány, když je na webové stránce vybrán instruktor, takže načítání Eager je lepší než opožděné načítání pouze v případě, že se stránka zobrazuje častěji s kurzem vybraným než bez.

Pokud bylo vybráno ID instruktora, je vybraný instruktor načten ze seznamu instruktorů v modelu zobrazení. Vlastnost `Courses` modelu zobrazení je poté načtena s `Course` entit z `Courses` navigační vlastnost tohoto instruktora.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

Metoda `Where` vrací kolekci, ale v tomto případě kritéria předaná této metodě mají za následek jenom jednu entitu `Instructor`, která se vrací. Metoda `Single` převede kolekci na jedinou entitu `Instructor`, která vám umožní přístup k vlastnosti `Courses` této entity.

[Jedinou](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) metodu pro kolekci použijete, když víte, že kolekce bude obsahovat pouze jednu položku. Metoda `Single` vyvolá výjimku, pokud je předaná kolekce prázdná nebo je-li k dispozici více než jedna položka. Alternativa je [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), která vrací výchozí hodnotu (`null` v tomto případě), pokud je kolekce prázdná. Nicméně v tomto případě by přesto došlo k výjimce (při pokusu o nalezení vlastnosti `Courses` na `null` odkazu) a zpráva o výjimce by byla méně zřetelně označovala příčinu problému. Při volání metody `Single` lze také předat podmínku `Where` namísto volání metody `Where` samostatně:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Namísto:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

V dalším případě se vybraný kurz načte ze seznamu kurzů v modelu zobrazení. Vlastnost `Enrollments` modelu zobrazení je načtena s `Enrollment` entitami z `Enrollments` navigační vlastnost tohoto kurzu.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>Úprava zobrazení indexu instruktorů

V *Views\Instructor\Index.cshtml*nahraďte existující kód následujícím kódem. Změny jsou zvýrazněny:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

V existujícím kódu jste provedli následující změny:

- Třída modelu se změnila na `InstructorIndexData`.
- Změnila se název stránky z **indexu** na **instruktory**.
- Přesunuli jsme sloupce propojení řádků na levou stranu.
- Byl odebrán sloupec **FullName** .
- Přidání sloupce **Office** , který zobrazí `item.OfficeAssignment.Location` pouze v případě, že `item.OfficeAssignment` není null. (Vzhledem k tomu, že se jedná o relaci typu 1:1, nemusí se jednat o související entitu `OfficeAssignment`.) 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- Přidaný kód, který bude dynamicky přidávat `class="selectedrow"` do `tr`ho prvku vybraného instruktora. Tím se nastaví barva pozadí pro vybraný řádek pomocí třídy šablony stylů CSS, kterou jste vytvořili dříve. (`valign` atribut bude užitečný v následujícím kurzu, když do tabulky přidáte sloupec s více řádky.) 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- Přidali jsme nový `ActionLink` označený jako **vybraný bezprostředně před** ostatními odkazy v každém řádku, což způsobí odeslání vybraného ID instruktoru do metody `Index`.

Spusťte aplikaci a vyberte kartu **instruktory** . Stránka zobrazuje vlastnost `Location` souvisejících entit `OfficeAssignment` a prázdnou buňku tabulky, pokud neexistuje žádná související entita `OfficeAssignment`.

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

V souboru *Views\Instructor\Index.cshtml* přidejte po zavření `table` element (na konci souboru) následující zvýrazněný kód. Zobrazí se seznam kurzů souvisejících s instruktorem, když je vybrán instruktor.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

Tento kód načte vlastnost `Courses` modelu zobrazení a zobrazí seznam kurzů. Poskytuje taky `Select` hypertextový odkaz, který pošle ID vybraného kurzu do metody `Index` akce.

> [!NOTE]
> Soubor *. CSS* je uložen v mezipaměti prohlížečem. Pokud při spuštění aplikace nevidíte žádné změny, proveďte pevně danou aktualizaci (při kliknutí na tlačítko **aktualizovat** stiskněte klávesu CTRL nebo stiskněte klávesy CTRL + F5).

Spusťte stránku a vyberte instruktor. Nyní se zobrazí mřížka zobrazující kurzy přiřazené k vybranému instruktorovi a pro každý kurz vidíte název přiřazeného oddělení.

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Po tom, co jste právě přidali blok kódu, přidejte následující kód. Zobrazí se seznam studentů, kteří jsou v kurzu při výběru tohoto kurzu zaregistrovaní.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

Tento kód načte vlastnost `Enrollments` modelu zobrazení, aby se zobrazil seznam studentů zaregistrovaných v kurzu.

Spusťte stránku a vyberte instruktor. Pak vyberte kurz, ve kterém se zobrazí seznam zaregistrovaných studentů a jejich třídy.

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>Přidávání explicitního načítání

Otevřete *InstructorController.cs* a podívejte se, jak metoda `Index` získá seznam zápisů pro vybraný kurz:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

Když jste načetli seznam instruktorů, zadali jste Eager načítání pro vlastnost navigace `Courses` a vlastnost `Department` každého kurzu. Pak vložíte kolekci `Courses` do modelu zobrazení a teď k `Enrollments` navigační vlastnost přistupujete z jedné entity v této kolekci. Vzhledem k tomu, že jste nezadali Eager načítání pro vlastnost navigace `Course.Enrollments`, data z této vlastnosti se zobrazí na stránce v důsledku opožděného načítání.

Pokud jste zakázali opožděné načítání beze změny kódu jiným způsobem, vlastnost `Enrollments` by měla hodnotu null, bez ohledu na to, kolik registrů v kurzu skutečně mělo. V takovém případě, pokud chcete načíst vlastnost `Enrollments`, je nutné zadat buď načítání Eager nebo explicitní načítání. Už jste viděli, jak Eager načíst. Aby bylo možné zobrazit příklad explicitního načítání, nahraďte metodu `Index` následujícím kódem, který explicitně načte vlastnost `Enrollments`. Změněný kód je zvýrazněný.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

Po získání vybrané entity `Course` se v novém kódu explicitně načte vlastnost navigace pro `Enrollments` tohoto kurzu:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

Pak explicitně načte všechny související entity `Student` `Enrollment` entit:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

Všimněte si, že pomocí metody `Collection` načíst vlastnost kolekce, ale u vlastnosti, která obsahuje pouze jednu entitu, použijete metodu `Reference`. Teď můžete spustit stránku index instruktora a na stránce se zobrazí žádný rozdíl, i když jste změnili způsob, jakým se data načítají.

## <a name="summary"></a>Přehled

Nyní jste používali všechny tři způsoby (opožděné, Eager a explicitní) k načtení souvisejících dat do navigačních vlastností. V dalším kurzu se dozvíte, jak aktualizovat související data.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Předchozí](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [Další](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
