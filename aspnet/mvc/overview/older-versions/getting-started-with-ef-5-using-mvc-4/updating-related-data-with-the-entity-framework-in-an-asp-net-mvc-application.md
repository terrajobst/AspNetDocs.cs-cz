---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: Aktualizace souvisejících dat s Entity Framework v aplikaci ASP.NET MVC (6 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592444"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>Aktualizace souvisejících dat s Entity Framework v aplikaci ASP.NET MVC (6 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozím kurzu jste zobrazili související data. v tomto kurzu aktualizujete související data. U většiny vztahů se to dá udělat tak, že aktualizujete příslušná pole cizího klíče. U vztahů m:n nezveřejňuje Entity Framework přímo tabulku JOIN, takže musíte explicitně přidat a odebrat entity z a do příslušných vlastností navigace.

Následující ilustrace znázorňují stránky, se kterými budete pracovat.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>Přizpůsobení stránek pro vytváření a úpravy pro kurzy

Když se vytvoří nová entita kurzu, musí mít relaci s existujícím oddělením. Pro usnadnění tohoto kódu se vygenerovaný kód skládá z metod kontroleru a vytváření a upravování zobrazení, která obsahují rozevírací seznam pro výběr oddělení. Rozevírací seznam nastaví vlastnost `Course.DepartmentID` cizího klíče a to je vše, co Entity Framework potřebuje, aby se načetla vlastnost `Department` navigace s příslušnou `Department`ou entitou. Použijete generovaný kód, ale mírně ho změníte a přidáte tak zpracování chyb a seřadíte rozevírací seznam.

V *CourseController.cs*odstraňte čtyři metody `Edit` a `Create` a nahraďte je následujícím kódem:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

Metoda `PopulateDepartmentsDropDownList` načte seznam všech oddělení seřazených podle názvu, vytvoří kolekci `SelectList` pro rozevírací seznam a předá kolekci do zobrazení ve vlastnosti `ViewBag`. Metoda přijímá volitelný parametr `selectedDepartment`, který umožňuje volajícímu kódu určit položku, která bude vybrána při vykreslení rozevíracího seznamu. Zobrazení pojmenuje `DepartmentID` do [pomocné rutiny `DropDownList`](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)a pomoc pak ví, že v objektu `ViewBag` vyhledá `SelectList` s názvem `DepartmentID`.

Metoda `HttpGet` `Create` volá metodu `PopulateDepartmentsDropDownList` bez nastavení vybrané položky, protože pro nový kurz se oddělení ještě nevytvořilo:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Metoda `HttpGet` `Edit` Nastaví vybranou položku na základě ID oddělení, které je již přiřazeno k upravovanému kurzu:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

Metody `HttpPost` pro `Create` a `Edit` také obsahují kód, který nastaví vybranou položku, když znovu zobrazí stránku po chybě:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Tento kód zajišťuje, že když se znovu zobrazí stránka s chybovou zprávou, zůstane vybraná možnost jakékoliv oddělení.

V *Views\Course\Create.cshtml*přidejte zvýrazněný kód pro vytvoření nového pole číslo kurzu před polem title ( **název** ). Jak je vysvětleno v předchozím kurzu, pole primárních klíčů se ve výchozím nastavení nestandardují, ale tento primární klíč je smysluplný, takže chcete, aby uživatel mohl zadat hodnotu klíče.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

V *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*a *Views\Course\Details.cshtml*přidejte pole číslo kurzu před pole **název** . Vzhledem k tomu, že se jedná o primární klíč, je zobrazený, ale nedá se změnit.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

Spusťte stránku **vytvořit** (Zobrazit index kurzu, klikněte na **vytvořit nový**) a zadejte data nového kurzu:

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

Klikněte na **vytvořit**. Na stránce index kurzu se zobrazí nový kurz přidaný do seznamu. Název oddělení v seznamu stránek indexu pochází z navigační vlastnosti, která ukazuje, že relace byla správně vytvořena.

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Spusťte stránku **Upravit** (zobrazí se stránka index kurzu a v kurzu klikněte na **Upravit** ).

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Změňte data na stránce a klikněte na **Uložit**. Zobrazí se stránka index kurzu s aktualizovanými daty kurzu.

## <a name="adding-an-edit-page-for-instructors"></a>Přidání stránky pro úpravy pro instruktory

Když upravíte záznam instruktora, chcete mít schopnost aktualizovat přiřazení kanceláře instruktora. Entita `Instructor` má relaci typu 1:1 s entitou `OfficeAssignment`, což znamená, že je nutné zpracovat následující situace:

- Pokud uživatel zruší přiřazení sady Office a původně měl hodnotu, je nutné odebrat a odstranit `OfficeAssignment` entitu.
- Pokud uživatel zadá hodnotu přiřazení Office a původně byl prázdný, musíte vytvořit novou entitu `OfficeAssignment`.
- Pokud uživatel změní hodnotu přiřazení Office, musíte změnit hodnotu v existující entitě `OfficeAssignment`.

Otevřete *InstructorController.cs* a podívejte se na metodu `HttpGet` `Edit`:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Vygenerovaný kód tady není tak, jak chcete. Je nastavená data pro rozevírací seznam, ale vy budete potřebovat textové pole. Tuto metodu nahraďte následujícím kódem:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Tento kód zruší příkaz `ViewBag` a přidá Eager načítání pro přidruženou entitu `OfficeAssignment`. Eager se nedá načíst pomocí metody `Find`, takže se místo toho používají metody `Where` a `Single` k výběru instruktora.

Metodu `HttpPost` `Edit` nahraďte následujícím kódem. který zpracovává aktualizace přiřazení Office:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Kód provede následující:

- Načte aktuální entitu `Instructor` z databáze pomocí načítání Eager pro navigační vlastnost `OfficeAssignment`. To se shoduje s tím, co jste provedli v metodě `HttpGet` `Edit`.
- Aktualizuje načtenou entitu `Instructor` hodnotami z pořadače modelů. [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) přetížení umožňuje seznam *povolených* vlastností, které chcete zahrnout. Tím zabráníte převzetí služeb při selhání, jak je vysvětleno v [druhém kurzu](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- Pokud je umístění kanceláře prázdné, vlastnost `Instructor.OfficeAssignment` nastaví na hodnotu null, aby se související řádek v tabulce `OfficeAssignment` odstranil.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- Uloží změny do databáze.

V *Views\Instructor\Edit.cshtml*po prvcích `div` pro pole **Datum přijetí** přidejte nové pole pro úpravy umístění kanceláře:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

Spusťte stránku (vyberte kartu **instruktoři** a pak klikněte na **Upravit** v instruktorovi). Změňte **umístění kanceláře** a klikněte na **Uložit**.

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>Přidání přiřazení kurzů do stránky pro úpravu instruktorů

Instruktoři můžou učit libovolný počet kurzů. Nyní vylepšíte stránku pro úpravu instruktoru přidáním možnosti změnit přiřazení kurzů pomocí skupiny zaškrtávacích políček, jak je znázorněno na následujícím snímku obrazovky:

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

Vztah mezi `Course` a `Instructor` entitami je mnoho až mnoho, což znamená, že nemáte přímý přístup k tabulce JOIN. Místo toho přidáte nebo odeberete entity do a z `Instructor.Courses` navigační vlastnost.

Uživatelské rozhraní, které umožňuje změnit, ke kterým kurzům je instruktor přiřazen, je skupina zaškrtávacích políček. Zobrazí se zaškrtávací políčko pro každý kurz v databázi a jsou vybrány ty, ke kterým je instruktor aktuálně přiřazen. Uživatel může zaškrtnutím nebo zrušením zaškrtnutí políček změnit přiřazení kurzů. Pokud byl počet kurzů mnohem větší, pravděpodobně budete chtít použít jinou metodu prezentace dat v zobrazení, ale při vytváření nebo odstraňování relací byste měli použít stejnou metodu manipulace s navigačními vlastnostmi.

Chcete-li poskytnout data do zobrazení pro seznam zaškrtávacích políček, použijte třídu zobrazení modelu. Vytvořte *AssignedCourseData.cs* ve složce *ViewModels* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

V *InstructorController.cs*nahraďte metodu `HttpGet` `Edit` následujícím kódem. Změny jsou zvýrazněny.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

Kód přidá načtení Eager pro vlastnost navigace `Courses` a zavolá novou metodu `PopulateAssignedCourseData` k poskytnutí informací pro pole zaškrtávacího políčka pomocí třídy zobrazení `AssignedCourseData`.

Kód v metodě `PopulateAssignedCourseData` čte všechny `Course` entit, aby bylo možné načíst seznam kurzů pomocí třídy zobrazení modelu. Pro každý kurz kód kontroluje, zda se v `Courses` navigační vlastnost instruktory vyskytuje kurz. K vytvoření efektivního vyhledávání při kontrole, jestli je kurz přiřazen instruktorovi, jsou kurzy přiřazené k instruktorovi vloženy do kolekce [HashSet –](https://msdn.microsoft.com/library/bb359438.aspx) . Vlastnost `Assigned` je nastavena na `true` pro kurzy, ke kterým je instruktor přiřazen. Zobrazení použije tuto vlastnost k určení, která zaškrtávací políčka se musí zobrazit jako vybraná. Nakonec se seznam předává do zobrazení ve vlastnosti `ViewBag`.

Dále přidejte kód, který se spustí, když uživatel klikne na **Uložit**. Nahraďte metodu `HttpPost` `Edit` následujícím kódem, který volá novou metodu, která aktualizuje `Courses` navigační vlastnost entity `Instructor`. Změny jsou zvýrazněny.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

Vzhledem k tomu, že zobrazení nemá kolekci `Course` entit, pořadač modelů nemůže automaticky aktualizovat navigační vlastnost `Courses`. Místo použití pořadače modelů k aktualizaci navigační vlastnosti kurzů to provedete v nové metodě `UpdateInstructorCourses`. Proto je nutné vyloučit vlastnost `Courses` z vazby modelu. To nevyžaduje žádné změny kódu, který volá [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) , protože používáte přetížení seznamu *povolených* položek a `Courses` není v seznamu zahrnutí.

Pokud nebyla vybrána žádná zaškrtávací políčka, kód v `UpdateInstructorCourses` inicializuje vlastnost `Courses` navigace s prázdnou kolekcí:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

Kód pak projde všemi kurzy v databázi a zkontroluje každý kurz s těmi, které jsou aktuálně přiřazeny k instruktorovi, a k těm, které byly vybrány v zobrazení. Aby bylo možné efektivně vyhledávat, jsou tyto dvě kolekce uloženy v `HashSet`ch objektech.

Pokud je vybráno zaškrtávací políčko pro kurz, ale kurz není v navigační vlastnosti `Instructor.Courses`, kurz se přidá do kolekce v navigační vlastnosti.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

Pokud není vybrané zaškrtávací políčko pro kurz, ale kurz je v navigační vlastnosti `Instructor.Courses`, kurz se odebere z navigační vlastnosti.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

V *Views\Instructor\Edit.cshtml*přidejte pole **kurzů** s polem zaškrtávacích políček přidáním následujícího zvýrazněného kódu hned za prvky `div` pro pole `OfficeAssignment`:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

Tento kód vytvoří tabulku HTML, která má tři sloupce. V každém sloupci je zaškrtávací políčko následované titulkem, který se skládá z čísla a názvu kurzu. Všechna zaškrtávací políčka mají stejný název ("selectedCourses"), který informuje pořadač modelů o tom, že se mají považovat za skupinu. Atribut `value` každé zaškrtávací políčko je nastaven na hodnotu `CourseID.` při zveřejnění stránky, pořadač modelu předává pole do kontroleru, který se skládá z `CourseID`ch hodnot pouze pro zaškrtávací políčka, která jsou vybrána.

Při počátečním vygenerování zaškrtávacích políček se u kurzů přiřazených k instruktoru `checked` atributy, které je vyberou (zobrazí se zaškrtnuté).

Po změně přiřazení kurzů budete chtít, abyste mohli ověřit změny, když se lokalita vrátí na stránku `Index`. Proto je nutné přidat sloupec do tabulky na této stránce. V takovém případě nemusíte používat objekt `ViewBag`, protože informace, které chcete zobrazit, jsou již v `Courses` navigační vlastnosti entity `Instructor`, kterou předáváte na stránku jako model.

V *Views\Instructor\Index.cshtml*přidejte nadpis **kurzů** hned za záhlaví **kanceláře** , jak je znázorněno v následujícím příkladu:

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

Pak přidejte novou buňku s podrobnostmi hned za buňku s podrobnostmi umístění kanceláře:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

Spuštěním stránky **index instruktora** zobrazíte kurzy přiřazené jednotlivým instruktorům:

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Kliknutím na tlačítko **Upravit** na instruktoru zobrazíte stránku pro úpravy.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

Změňte některá přiřazení kurzů a klikněte na **Uložit**. Změny, které provedete, se projeví na stránce indexu.

 Poznámka: přístup pro úpravy dat kurzu vyučující funguje dobře, když je k dispozici omezený počet kurzů. Pro kolekce, které jsou mnohem větší, by se vyžadovalo jiné uživatelské rozhraní a odlišná metoda aktualizace.  

## <a name="update-the-delete-method"></a>Aktualizace metody DELETE

Změňte kód v metodě HttpPost Delete tak, aby se při odstranění instruktoru odstranil záznam přiřazení Office (pokud existuje):

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

Pokud se pokusíte odstranit instruktora, který je přiřazený oddělení jako správce, zobrazí se chyba referenční integrity. Viz [aktuální verze tohoto kurzu](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) pro další kód, který automaticky odebere instruktora z libovolného oddělení, kde je instruktor přiřazen jako správce.

## <a name="summary"></a>Přehled

Právě jste dokončili tento Úvod k práci se souvisejícími daty. Zatím v těchto kurzech jste provedli celou škálu operací CRUD, ale zatím jste se nezabýváte problémy s souběžnosti. V dalším kurzu budeme zavádět téma souběžnosti, vysvětlit možnosti pro jeho zpracování a přidat zpracování souběžnosti do kódu CRUD, který jste už napsali pro jeden typ entity.

Odkazy na jiné prostředky Entity Framework najdete na konci [posledního kurzu v této řadě](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).

> [!div class="step-by-step"]
> [Předchozí](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Další](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
