---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: Aktualizace souvisejících dat pomocí EF v aplikaci ASP.NET MVC'
description: V tomto kurzu aktualizujete související data. U většiny vztahů se to dá udělat aktualizací polí cizího klíče nebo vlastností navigace.
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616002"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a>Kurz: Aktualizace souvisejících dat pomocí EF v aplikaci ASP.NET MVC

V předchozím kurzu jste zobrazili související data. V tomto kurzu aktualizujete související data. U většiny vztahů se to dá udělat aktualizací polí cizího klíče nebo vlastností navigace. U vztahů n:n Entity Framework nezveřejňuje tabulku JOIN přímo, takže přidáte a odeberete entity do a z odpovídajících vlastností navigace.

Následující ilustrace znázorňují některé stránky, se kterými budete pracovat.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![Úprava vyučujících pomocí kurzů](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přizpůsobení stránek kurzů
> * Stránka Přidat Office k instruktorům
> * Přidat kurzy na stránku instruktorů
> * Aktualizovat DeleteConfirmed
> * Přidání umístění a kurzů Office na stránku pro vytvoření

## <a name="prerequisites"></a>Předpoklady

* [Čtení souvisejících dat](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a>Přizpůsobení stránek kurzů

Když se vytvoří nová entita kurzu, musí mít relaci s existujícím oddělením. Pro usnadnění tohoto kódu se vygenerovaný kód skládá z metod kontroleru a vytváření a upravování zobrazení, která obsahují rozevírací seznam pro výběr oddělení. Rozevírací seznam nastaví vlastnost `Course.DepartmentID` cizího klíče a to je vše, co Entity Framework potřebuje, aby se načetla vlastnost `Department` navigace s příslušnou `Department`ou entitou. Použijete generovaný kód, ale mírně ho změníte a přidáte tak zpracování chyb a seřadíte rozevírací seznam.

V *CourseController.cs*odstraňte čtyři metody `Create` a `Edit` a nahraďte je následujícím kódem:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

Na začátek souboru přidejte následující příkaz `using`:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Metoda `PopulateDepartmentsDropDownList` načte seznam všech oddělení seřazených podle názvu, vytvoří kolekci `SelectList` pro rozevírací seznam a předá kolekci do zobrazení ve vlastnosti `ViewBag`. Metoda přijímá volitelný parametr `selectedDepartment`, který umožňuje volajícímu kódu určit položku, která bude vybrána při vykreslení rozevíracího seznamu. Zobrazení přejmenuje `DepartmentID` pomocníka [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) a pomoc pak ví, aby prohledal `ViewBag` objekt pro `SelectList` s názvem `DepartmentID`.

Metoda `HttpGet` `Create` volá metodu `PopulateDepartmentsDropDownList` bez nastavení vybrané položky, protože pro nový kurz se oddělení ještě nevytvořilo:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

Metoda `HttpGet` `Edit` Nastaví vybranou položku na základě ID oddělení, které je již přiřazeno k upravovanému kurzu:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

Metody `HttpPost` pro `Create` a `Edit` také obsahují kód, který nastaví vybranou položku, když znovu zobrazí stránku po chybě:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

Tento kód zajišťuje, že když se znovu zobrazí stránka s chybovou zprávou, zůstane vybraná možnost jakékoliv oddělení.

Zobrazení kurzu jsou již vygenerovaná pomocí rozevíracích seznamů pro pole oddělení, ale pro toto pole nechcete DepartmentID titulek, takže následující zvýrazněnou změnu v souboru *Views\Course\Create.cshtml* změňte na titulek.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

Udělejte stejnou změnu v *Views\Course\Edit.cshtml*.

Obvykle generátor negeneruje primární klíč, protože hodnota klíče je vygenerovaná databází a nedá se změnit a není smysluplná hodnota, která se má zobrazit uživatelům. Pro entity kurzu, které modul generování klíčů obsahuje textové pole pro pole `CourseID`, protože má za to, že atribut `DatabaseGeneratedOption.None` znamená, že uživatel by měl být schopný zadat hodnotu primárního klíče. Ale nerozumí to, že tento počet je smysluplný, protože ho chcete zobrazit v ostatních zobrazeních, takže ho budete muset přidat ručně.

Do pole **název** v *Views\Course\Edit.cshtml*přidejte pole číslo kurzu. Vzhledem k tomu, že se jedná o primární klíč, je zobrazený, ale nedá se změnit.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

Pro číslo kurzu v zobrazení pro úpravy již existuje skryté pole (`Html.HiddenFor` pomocník). Přidání pomocné rutiny *HTML. LabelFor* eliminuje nutnost skrytého pole, protože nezpůsobí, že se číslo kurzu zahrne do publikovaných dat, když uživatel klikne na **Uložit** na stránce Upravit.

V *Views\Course\Delete.cshtml* a *Views\Course\Details.cshtml*Změňte popisek název oddělení z "název" na "oddělení" a před pole **název** přidejte pole číslo kurzu.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

Spusťte stránku **vytvořit** (Zobrazit index kurzu, klikněte na **vytvořit nový**) a zadejte data nového kurzu:

| Hodnota | Nastavení |
| ----- | ------- |
| Číslo | Zadejte *1000*. |
| Název | Zadejte *algebraický*. |
| Kredity | Zadejte *4*. |
|Oddělení | Vyberte **matematické**. |

Klikněte na možnost **Vytvořit**. Na stránce index kurzu se zobrazí nový kurz přidaný do seznamu. Název oddělení v seznamu stránek indexu pochází z navigační vlastnosti, která ukazuje, že relace byla správně vytvořena.

Spusťte stránku **Upravit** (zobrazí se stránka index kurzu a v kurzu klikněte na **Upravit** ).

Změňte data na stránce a klikněte na **Uložit**. Zobrazí se stránka index kurzu s aktualizovanými daty kurzu.

## <a name="add-office-to-instructors-page"></a>Stránka Přidat Office k instruktorům

Když upravíte záznam instruktora, chcete mít schopnost aktualizovat přiřazení kanceláře instruktora. Entita `Instructor` má relaci typu 1:1 s entitou `OfficeAssignment`, což znamená, že je nutné zpracovat následující situace:

- Pokud uživatel zruší přiřazení sady Office a původně měl hodnotu, je nutné odebrat a odstranit `OfficeAssignment` entitu.
- Pokud uživatel zadá hodnotu přiřazení Office a původně byl prázdný, musíte vytvořit novou entitu `OfficeAssignment`.
- Pokud uživatel změní hodnotu přiřazení Office, musíte změnit hodnotu v existující entitě `OfficeAssignment`.

Otevřete *InstructorController.cs* a podívejte se na metodu `HttpGet` `Edit`:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Vygenerovaný kód tady není tak, jak chcete. Je nastavená data pro rozevírací seznam, ale vy budete potřebovat textové pole. Tuto metodu nahraďte následujícím kódem:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

Tento kód zruší příkaz `ViewBag` a přidá Eager načítání pro přidruženou entitu `OfficeAssignment`. Eager se nedá načíst pomocí metody `Find`, takže se místo toho používají metody `Where` a `Single` k výběru instruktora.

Metodu `HttpPost` `Edit` nahraďte následujícím kódem. který zpracovává aktualizace přiřazení Office:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Odkaz na `RetryLimitExceededException` vyžaduje příkaz `using`; Pokud ho chcete přidat, najeďte myší na `RetryLimitExceededException`. Zobrazí se následující zpráva: ![ zprávu výjimky opakování](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

Vyberte **Zobrazit možné opravy**a pak **použijte System. data. entity. Infrastructure.**

![Vyřešit výjimku opakování](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

Kód provede následující:

- Změní název metody na `EditPost`, protože signatura je nyní shodná s metodou `HttpGet` (atribut `ActionName` určuje, že se/Edit/adresa URL stále používá).
- Načte aktuální entitu `Instructor` z databáze pomocí načítání Eager pro navigační vlastnost `OfficeAssignment`. To se shoduje s tím, co jste provedli v metodě `HttpGet` `Edit`.
- Aktualizuje načtenou entitu `Instructor` hodnotami z pořadače modelů. [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) přetížení umožňuje seznam *povolených* vlastností, které chcete zahrnout. Tím zabráníte převzetí služeb při selhání, jak je vysvětleno v [druhém kurzu](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- Pokud je umístění kanceláře prázdné, vlastnost `Instructor.OfficeAssignment` nastaví na hodnotu null, aby se související řádek v tabulce `OfficeAssignment` odstranil.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- Uloží změny do databáze.

V *Views\Instructor\Edit.cshtml*po prvcích `div` pro pole **Datum přijetí** přidejte nové pole pro úpravy umístění kanceláře:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

Spusťte stránku (vyberte kartu **instruktoři** a pak klikněte na **Upravit** v instruktorovi). Změňte **umístění kanceláře** a klikněte na **Uložit**.

## <a name="add-courses-to-instructors-page"></a>Přidat kurzy na stránku instruktorů

Instruktoři můžou učit libovolný počet kurzů. Teď vylepšíte stránku pro úpravu instruktoru přidáním možnosti změnit přiřazení kurzů pomocí skupiny zaškrtávacích políček.

Vztah mezi entitami `Course` a `Instructor` je mnoho až mnoho, což znamená, že nemáte přímý přístup k vlastnostem cizího klíče, které jsou v tabulce JOIN. Místo toho můžete přidat a odebrat entity do a z `Instructor.Courses` navigační vlastnost.

Uživatelské rozhraní, které umožňuje změnit, ke kterým kurzům je instruktor přiřazen, je skupina zaškrtávacích políček. Zobrazí se zaškrtávací políčko pro každý kurz v databázi a jsou vybrány ty, ke kterým je instruktor aktuálně přiřazen. Uživatel může zaškrtnutím nebo zrušením zaškrtnutí políček změnit přiřazení kurzů. Pokud byl počet kurzů mnohem větší, pravděpodobně budete chtít použít jinou metodu prezentace dat v zobrazení, ale při vytváření nebo odstraňování relací byste měli použít stejnou metodu manipulace s navigačními vlastnostmi.

Chcete-li poskytnout data do zobrazení pro seznam zaškrtávacích políček, použijte třídu zobrazení modelu. Vytvořte *AssignedCourseData.cs* ve složce *ViewModels* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

V *InstructorController.cs*nahraďte metodu `HttpGet` `Edit` následujícím kódem. Změny jsou zvýrazněné.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

Kód přidá načtení Eager pro vlastnost navigace `Courses` a zavolá novou metodu `PopulateAssignedCourseData` k poskytnutí informací pro pole zaškrtávacího políčka pomocí třídy zobrazení `AssignedCourseData`.

Kód v metodě `PopulateAssignedCourseData` čte všechny `Course` entit, aby bylo možné načíst seznam kurzů pomocí třídy zobrazení modelu. Pro každý kurz kód kontroluje, zda se v `Courses` navigační vlastnost instruktory vyskytuje kurz. K vytvoření efektivního vyhledávání při kontrole, jestli je kurz přiřazen instruktorovi, jsou kurzy přiřazené k instruktorovi vloženy do kolekce [HashSet –](https://msdn.microsoft.com/library/bb359438.aspx) . Vlastnost `Assigned` je nastavena na `true` pro kurzy, ke kterým je instruktor přiřazen. Zobrazení použije tuto vlastnost k určení, která zaškrtávací políčka se musí zobrazit jako vybraná. Nakonec se seznam předává do zobrazení ve vlastnosti `ViewBag`.

Dále přidejte kód, který se spustí, když uživatel klikne na **Uložit**. Metodu `EditPost` nahraďte následujícím kódem, který volá novou metodu, která aktualizuje `Courses` navigační vlastnost entity `Instructor`. Změny jsou zvýrazněné.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

Signatura metody se teď liší od metody `HttpGet` `Edit`, takže se název metody změní z `EditPost` zpět na `Edit`.

Vzhledem k tomu, že zobrazení nemá kolekci `Course` entit, pořadač modelů nemůže automaticky aktualizovat navigační vlastnost `Courses`. Namísto použití pořadače modelů k aktualizaci `Courses` navigační vlastnosti to provedete v nové metodě `UpdateInstructorCourses`. Proto je nutné vyloučit vlastnost `Courses` z vazby modelu. To nevyžaduje žádné změny kódu, který volá [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) , protože používáte přetížení seznamu *povolených* položek a `Courses` není v seznamu zahrnutí.

Pokud nebyla vybrána žádná zaškrtávací políčka, kód v `UpdateInstructorCourses` inicializuje vlastnost `Courses` navigace s prázdnou kolekcí:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

Kód pak projde všemi kurzy v databázi a zkontroluje každý kurz s těmi, které jsou aktuálně přiřazeny k instruktorovi, a k těm, které byly vybrány v zobrazení. Aby bylo možné efektivně vyhledávat, jsou tyto dvě kolekce uloženy v `HashSet`ch objektech.

Pokud je vybráno zaškrtávací políčko pro kurz, ale kurz není v navigační vlastnosti `Instructor.Courses`, kurz se přidá do kolekce v navigační vlastnosti.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

Pokud není vybrané zaškrtávací políčko pro kurz, ale kurz je v navigační vlastnosti `Instructor.Courses`, kurz se odebere z navigační vlastnosti.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

V *Views\Instructor\Edit.cshtml*přidejte pole **kurzů** s polem se zaškrtávacím políčky přidáním následujícího kódu hned za prvky `div` pro pole `OfficeAssignment` a před `div` element pro tlačítko **Uložit** :

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

Pokud vložíte kód a konce řádků a odsazení nevypadají jako v tomto případě, ručně opravte vše, aby vypadala tady. Odsazení nemusí být dokonalé, ale `@</tr><tr>`, `@:<td>`, `@:</td>`a `@</tr>` řádky musí být na jednom řádku, jak je znázorněno, nebo se zobrazí chyba za běhu.

Tento kód vytvoří tabulku HTML, která má tři sloupce. V každém sloupci je zaškrtávací políčko následované titulkem, který se skládá z čísla a názvu kurzu. Všechna zaškrtávací políčka mají stejný název ("selectedCourses"), který informuje pořadač modelů o tom, že se mají považovat za skupinu. Atribut `value` každé zaškrtávací políčko je nastaven na hodnotu `CourseID.` při zveřejnění stránky, pořadač modelu předává pole do kontroleru, který se skládá z `CourseID`ch hodnot pouze pro zaškrtávací políčka, která jsou vybrána.

Při počátečním vygenerování zaškrtávacích políček se u kurzů přiřazených k instruktoru `checked` atributy, které je vyberou (zobrazí se zaškrtnuté).

Po změně přiřazení kurzů budete chtít, abyste mohli ověřit změny, když se lokalita vrátí na stránku `Index`. Proto je nutné přidat sloupec do tabulky na této stránce. V takovém případě nemusíte používat objekt `ViewBag`, protože informace, které chcete zobrazit, jsou již v `Courses` navigační vlastnosti entity `Instructor`, kterou předáváte na stránku jako model.

V *Views\Instructor\Index.cshtml*přidejte nadpis **kurzů** hned za záhlaví **kanceláře** , jak je znázorněno v následujícím příkladu:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

Pak přidejte novou buňku s podrobnostmi hned za buňku s podrobnostmi umístění kanceláře:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

Spuštěním stránky **index instruktora** zobrazíte kurzy přiřazené jednotlivým instruktorům.

Kliknutím na tlačítko **Upravit** na instruktoru zobrazíte stránku pro úpravy.

Změňte některá přiřazení kurzů a klikněte na **Uložit**. Změny, které provedete, se projeví na stránce indexu.

 Poznámka: přístup, který je zde povedený pro úpravu dat kurzu instruktora funguje dobře, když existuje omezený počet kurzů. Pro kolekce, které jsou mnohem větší, by se vyžadovalo jiné uživatelské rozhraní a odlišná metoda aktualizace.

## <a name="update-deleteconfirmed"></a>Aktualizovat DeleteConfirmed

V *InstructorController.cs*odstraňte metodu `DeleteConfirmed` a vložte následující kód na místo.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

Tento kód provede následující změnu:

- Pokud je instruktor přiřazen jako správce libovolného oddělení, odebere z tohoto oddělení přiřazení instruktora. Bez tohoto kódu byste dostali chybu referenční integrity, pokud jste se pokusili odstranit instruktora, který byl přiřazený jako správce pro oddělení.

Tento kód nezpracovává scénář jednoho instruktora přiřazeného jako správce pro více oddělení. V posledním kurzu přidáte kód, který zabrání tomu, aby se tento scénář stalo.

## <a name="add-office-location-and-courses-to-the-create-page"></a>Přidání umístění a kurzů Office na stránku pro vytvoření

V *InstructorController.cs*odstraňte `HttpGet` a `HttpPost` `Create` metody a pak na své místo přidejte následující kód:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

Tento kód se podobá tomu, co jste viděli pro metody úprav s tím rozdílem, že zpočátku nejsou vybrané žádné kurzy. Metoda `HttpGet` `Create` volá metodu `PopulateAssignedCourseData`, protože by mohly být vybrány kurzy, ale za účelem poskytnutí prázdné kolekce pro `foreach` smyčka v zobrazení (jinak kód zobrazení by vyvolal výjimku s nulovým odkazem).

Metoda HttpPost Create přidá každý vybraný kurz do navigační vlastnosti kurzů před kódem šablony, který zkontroluje chyby ověřování a přidá nového instruktora do databáze. Kurzy se přidávají i v případě, že dojde k chybám modelu, takže když dojde k chybám modelu (například uživatel zaznamená neplatné datum), takže když se stránka znovu zobrazí s chybovou zprávou, všechny vybrané kurzy se automaticky obnoví.

Všimněte si, že aby bylo možné přidat kurzy do navigační vlastnosti `Courses`, je nutné tuto vlastnost inicializovat jako prázdnou kolekci:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

Jako alternativu k tomu, že se jedná o kód kontroleru, to můžete provést v modelu instruktoru změnou vlastnosti getter na automaticky vytvořit kolekci, pokud neexistuje, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

Pokud upravíte vlastnost `Courses` tímto způsobem, můžete v řadiči odebrat explicitní inicializační kód vlastnosti.

V *Views\Instructor\Create.cshtml*přidejte zaškrtávací políčka umístění kanceláře a kurz po poli Datum přijetí a před tlačítko **Odeslat** .

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

Po vložení kódu opravte zalomení řádků a odsazení stejným způsobem jako u stránky pro úpravy.

Spusťte stránku vytvořit a přidejte instruktora.

<a id="transactions"></a>

## <a name="handling-transactions"></a>Zpracování transakcí

Jak je vysvětleno v [kurzu základní funkce CRUD](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), ve výchozím nastavení Entity Framework implicitně implementuje transakce. V případě scénářů, kde potřebujete větší kontrolu – například pokud chcete zahrnout operace provedené mimo Entity Framework v transakci – viz [práce s transakcemi](https://msdn.microsoft.com/data/dn456843) na webu MSDN.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-step"></a>Další krok

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Stránky přizpůsobených kurzů
> * Stránka pro přidání kanceláře k instruktorům
> * Přidání kurzů na stránku instruktorů
> * Aktualizovaný DeleteConfirmed
> * Přidání umístění a kurzů Office na stránku vytvořit

Přejděte k dalšímu článku, kde se dozvíte, jak implementovat asynchronní programovací model.
> [!div class="nextstepaction"]
> [Model asynchronního programování](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
