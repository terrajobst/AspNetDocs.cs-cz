---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: Vytvoření složitějšího datového modelu pro ASP.NET aplikaci MVC (4 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9c19ec47ad98a319ddee17db014c4b15e3734778
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595351"
---
# <a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>Vytvoření složitějšího datového modelu pro ASP.NET aplikaci MVC (4 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozích kurzech jste pracovali s jednoduchým datovým modelem, který se skládá ze tří entit. V tomto kurzu přidáte další entity a vztahy a budete přizpůsobovat datový model zadáním pravidel formátování, ověřování a mapování databáze. Uvidíte dva způsoby přizpůsobení datového modelu: přidáním atributů do tříd entit a přidáním kódu do třídy kontextu databáze.

Až budete hotovi, třídy entit vytvoří dokončený datový model, který je znázorněn na následujícím obrázku:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>Přizpůsobení datového modelu pomocí atributů

V této části se dozvíte, jak přizpůsobit datový model pomocí atributů, které určují pravidla formátování, ověřování a mapování databáze. Pak v několika z následujících částí vytvoříte kompletní datový model `School` přidáním atributů do tříd, které jste už vytvořili, a vytvořením nových tříd pro zbývající typy entit v modelu.

### <a name="the-datatype-attribute"></a>Atribut DataType

Pro data o registraci studenta se aktuálně zobrazují všechny webové stránky, které jsou aktuálně současně s datem, i když jsou pro toto pole k disstará data. Pomocí atributů datových poznámek můžete vytvořit jednu změnu kódu, která bude opravovat formát zobrazení v každém zobrazení, které zobrazuje data. Chcete-li zobrazit příklad, jak to provést, přidáte atribut do vlastnosti `EnrollmentDate` ve třídě `Student`.

V *Models\Student.cs*přidejte příkaz `using` pro obor názvů `System.ComponentModel.DataAnnotations` a přidejte `DataType` a `DisplayFormat` atributy do vlastnosti `EnrollmentDate`, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

Atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) se používá k určení datového typu, který je konkrétnější než vnitřní typ databáze. V tomto případě chceme sledovat pouze datum, nikoli datum a čas. [Výčet DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) poskytuje mnoho datových typů, jako je *datum, čas, PhoneNumber, měna, EmailAddress* a další. Atribut `DataType` může také povolit aplikaci automatické poskytování funkcí specifických pro typ. Například odkaz `mailto:` lze vytvořit pro [typ DataType. EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)a selektor data lze zadat pro [typ DataType. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) v prohlížečích, které podporují [HTML5](http://html5.org/). Atributy [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) emitují atributy [data](http://ejohn.org/blog/html-5-data-attributes/) HTML 5 (vyslovované *datové přerušované*), které mohou prohlížeče HTML 5 pochopit. Atributy [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) neposkytují žádné ověření.

`DataType.Date` neurčuje formát data, které se zobrazí. Ve výchozím nastavení se datové pole zobrazuje v závislosti na výchozích formátech na základě objektu [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)serveru.

Atribut `DisplayFormat` slouží k explicitnímu zadání formátu data:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

Nastavení `ApplyFormatInEditMode` určuje, že zadané formátování by mělo být použito i v případě, že se hodnota v textovém poli zobrazí pro úpravy. (Pro některá pole (například pro hodnoty měny možná nebudete chtít), nebudete chtít v textovém poli pro úpravy chtít symbol měny.)

Můžete použít atribut [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) sám o sobě, ale obecně je vhodné použít také atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) . Atribut `DataType` předává *sémantiku* dat na rozdíl od způsobu vykreslování na obrazovce a poskytuje následující výhody, které nezískáte pomocí `DisplayFormat`:

- Prohlížeč může povolit funkce HTML5 (například pro zobrazení ovládacího prvku kalendáře, symbolu měny odpovídající národním prostředí, e-mailových odkazů atd.).
- Ve výchozím nastavení bude prohlížeč data vykreslovat pomocí správného formátu na základě vašeho [národního prostředí](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).
- Atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) může MVC povolit, aby vybrali šablonu pravého pole pro vykreslení dat ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) , pokud se používá samostatně, používá šablonu řetězce). Další informace najdete v tématu [šablony ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)pro Brad Wilson. (I když je napsaný pro MVC 2, Tento článek se stále vztahuje na aktuální verzi ASP.NET MVC.)

Použijete-li atribut `DataType` s polem datum, je nutné zadat atribut `DisplayFormat` také, aby bylo zajištěno, že pole bude v prohlížečích Chrome správně vykresleno. Další informace najdete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

Spusťte znovu stránku indexu studenta a Všimněte si, že časy se už nezobrazuje pro data registrace. Totéž platí pro všechna zobrazení, která používají model `Student`.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

Pravidla a zprávy pro ověřování dat můžete zadat také pomocí atributů. Předpokládejme, že chcete zajistit, aby uživatelé nezadali více než 50 znaků pro název. Chcete-li přidat toto omezení, přidejte atributy [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) do vlastností `LastName` a `FirstMidName`, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

Atribut [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) nezabrání uživateli v zadání prázdného místa pro název. Pro použití omezení na vstup můžete použít atribut [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) . Například následující kód vyžaduje, aby první znak byl velkými písmeny a aby zbývající znaky byly abecedně:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

Atribut [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) poskytuje podobnou funkci atributu [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , ale neposkytuje ověřování na straně klienta.

Spusťte aplikaci a klikněte na kartu **studenti** . Zobrazí se následující chyba:

*Model, který provedl zálohování kontextu ' SchoolContext ', se od vytvoření databáze změnil. Pokud chcete aktualizovat databázi ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)), zvažte použití migrace Code First.*

Model databáze se změnil způsobem, který vyžaduje změnu schématu databáze a Entity Framework zjistil, že. Pomocí migrace aktualizujete schéma bez ztráty dat přidaných do databáze pomocí uživatelského rozhraní. Pokud jste změnili data vytvořená metodou `Seed`, která se změní zpátky na původní stav z důvodu metody [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) , kterou používáte v metodě `Seed`. ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) je ekvivalentem operace "Upsert" z terminologie databáze.)

V konzole správce balíčků (PMC) zadejte následující příkazy:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

Příkaz `add-migration MaxLengthOnNames` vytvoří soubor s názvem *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*. Tento soubor obsahuje kód, který bude aktualizovat databázi tak, aby odpovídala aktuálnímu datovému modelu. Časové razítko, které se přiřadí k názvu souboru migrace, používá Entity Framework k seřazení migrace. Pokud po vytvoření více migrací dojde k vyřazení databáze nebo pokud projekt nasadíte pomocí migrace, budou všechny migrace použity v pořadí, ve kterém byly vytvořeny.

Spusťte stránku **vytvořit** a zadejte název delší než 50 znaků. Jakmile budete mít 50 znaků, ověřování na straně klienta okamžitě zobrazí chybovou zprávu.

![Chyba Val na straně klienta](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>Atribut Column

Můžete také použít atributy pro řízení způsobu, jakým jsou třídy a vlastnosti namapovány na databázi. Předpokládejme, že jste použili název `FirstMidName` pro pole jméno a příjmení, protože pole může obsahovat také prostřední jméno. Ale chcete, aby se sloupec databáze jmenoval `FirstName`, protože uživatelé, kteří budou psát ad hoc dotazy na databázi, jsou zvyklí na tento název. Chcete-li toto mapování provést, můžete použít atribut `Column`.

Atribut `Column` určuje, že při vytvoření databáze bude sloupec `Student` tabulky, která je mapována na vlastnost `FirstMidName`, pojmenován `FirstName`. Jinými slovy, pokud váš kód odkazuje na `Student.FirstMidName`, data budou pocházet z nebo aktualizována ve sloupci `FirstName` tabulky `Student`. Pokud názvy sloupců nezadáte, budou mít stejný název jako název vlastnosti.

Přidejte příkaz using pro atribut [System. ComponentModel. DataAnnotations. Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) a název sloupce do vlastnosti `FirstMidName`, jak je znázorněno v následujícím zvýrazněném kódu:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

Přidání [atributu Column](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) změní model, který SchoolContext zálohuje, takže se neshoduje s databází. Zadáním následujících příkazů v PMC vytvořte další migraci:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

V **Průzkumník serveru** (**Průzkumník databáze** Pokud používáte Express for Web) poklikejte na tabulku *student* .

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

Následující obrázek ukazuje původní název sloupce, protože byl předtím, než jste použili první dvě migrace. Kromě názvu sloupce, který se mění z `FirstMidName` na `FirstName`, se sloupce dvou názvů změnily z `MAX` délky na 50 znaků.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Změny v mapování databáze můžete také provést pomocí [rozhraní API Fluent](https://msdn.microsoft.com/data/jj591617), jak vidíte později v tomto kurzu.

> [!NOTE]
> Pokud se pokusíte zkompilovat ještě před dokončením vytváření všech těchto tříd entit, může dojít k chybám kompilátoru.

## <a name="create-the-instructor-entity"></a>Vytvořit entitu instruktora

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

Vytvořte *Models\Instructor.cs*a nahraďte kód šablony následujícím kódem:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Všimněte si, že některé vlastnosti jsou v entitě `Student` a `Instructor` stejné. V kurzu [Implementace dědičnosti](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) níže v této sérii budete Refaktorovat použití dědičnosti k odstranění této redundance.

### <a name="the-required-and-display-attributes"></a>Požadované a zobrazované atributy

Atributy vlastnosti `LastName` určují, že se jedná o požadované pole. titulek pro textové pole by měl být "příjmení" (místo názvu vlastnosti, který by byl "LastName" bez místa) a hodnota nesmí být delší než 50 znaků.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[Atribut StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) nastaví maximální délku v databázi a poskytuje ověřování na straně klienta a na straně serveru pro ASP.NET MVC. V tomto atributu můžete také zadat minimální délku řetězce, ale minimální hodnota nemá žádný vliv na schéma databáze. [Požadovaný atribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) není potřebný pro typy hodnot, jako jsou DateTime, int, Double a float. Hodnotovým typům nelze přiřadit hodnotu null, takže jsou jejich podstatou vyžadovány. Je možné odebrat [požadovaný atribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) a nahradit jej parametrem minimální délka pro atribut `StringLength`:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

Můžete umístit více atributů na jeden řádek, takže můžete také napsat třídu instruktora následujícím způsobem:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>Vypočítaná vlastnost FullName

`FullName` je vypočtená vlastnost, která vrací hodnotu, která je vytvořena zřetězením dvou dalších vlastností. Proto má pouze přistupující objekt `get` a v databázi nebude vygenerován žádný `FullName` sloupec.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Kurzy a navigační vlastnosti OfficeAssignment

Vlastnosti `Courses` a `OfficeAssignment` jsou navigační vlastnosti. Jak bylo vysvětleno dříve, jsou obvykle definovány jako [virtuální](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) , aby mohli využívat funkci Entity Framework s názvem [opožděné načítání](https://msdn.microsoft.com/magazine/hh205756.aspx). Kromě toho, pokud navigační vlastnost může obsahovat více entit, její typ musí implementovat rozhraní [ICollection&lt;t&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) . (Například [IList&lt;t&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) vyhodnoceny, ale ne [IEnumerable&lt;t&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) , protože `IEnumerable<T>` neimplementuje metodu [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).

Instruktor může naučit libovolný počet kurzů, takže `Courses` je definován jako kolekce `Course` entit. Naše obchodní pravidla mají stav, kdy instruktor může mít jenom jednu kancelář, takže `OfficeAssignment` definovaná jako jediná entita `OfficeAssignment` (která může být `null`, pokud není přiřazená žádná kancelář).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>Vytvoření entity OfficeAssignment

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

Vytvořte *Models\OfficeAssignment.cs* pomocí následujícího kódu:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Sestavte projekt, který uloží změny a ověří, že jste neudělali žádné chyby kopírování a vložení, které může kompilátor zachytit.

### <a name="the-key-attribute"></a>Klíčový atribut

Mezi `Instructor` a entitami `OfficeAssignment` existuje vztah 1:1 nebo jedna. Přiřazení kanceláře existuje jenom ve vztahu k instruktorovi, ke kterému je přiřazená, a proto jeho primární klíč je také cizí klíč k entitě `Instructor`. Entity Framework ale nemůžou automaticky rozpoznat `InstructorID` jako primární klíč této entity, protože její název nedodržuje konvence pojmenování `ID` `ID` nebo *ClassName* . Proto atribut `Key` slouží k identifikaci jako klíč:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Atribut `Key` můžete použít také v případě, že má entita svůj vlastní primární klíč, ale chcete vlastnost pojmenovat jinou než `classnameID` nebo `ID`. Ve výchozím nastavení EF považuje klíč za generovaný nedatabází, protože sloupec je určen pro identifikaci vztahu.

### <a name="the-foreignkey-attribute"></a>Atribut klíč ForeignKey

Pokud existuje vztah 1:1 nebo jedna nebo relace 1:1 mezi dvěma entitami (například mezi `OfficeAssignment` a `Instructor`), EF nemůže pracovat na konci vztahu objekt zabezpečení, který je závislý na konci. Relace 1:1 mají v každé třídě k druhé třídě referenční navigační vlastnost. [Atribut klíč ForeignKey](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) lze použít pro závislou třídu k vytvoření relace. Vynecháte-li [atribut klíč ForeignKey](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), při pokusu o vytvoření migrace se zobrazí následující chyba:

Nelze určit hlavní konec přidružení mezi typy ' ContosoUniversity. Models. OfficeAssignment ' a ' ContosoUniversity. Models. Instructor '. Hlavní konec tohoto přidružení musí být explicitně nakonfigurovaný buď pomocí rozhraní API Fluent, nebo datových poznámek.

Později v tomto kurzu ukážeme, jak nakonfigurovat tento vztah s rozhraním API Fluent.

### <a name="the-instructor-navigation-property"></a>Navigační vlastnost instruktora

Entita `Instructor` má `OfficeAssignment` navigační vlastnost s možnou hodnotou null (protože instruktor nemusí mít přiřazený Office) a entita `OfficeAssignment` má vlastnost navigace `Instructor`, která nesmí mít hodnotu null (protože přiřazení kanceláře nemůže existovat bez instruktora--`InstructorID` nemůže mít hodnotu null). Pokud má entita `Instructor` související entitu `OfficeAssignment`, bude mít Každá entita odkaz na jinou entitu v její navigační vlastnosti.

Můžete umístit atribut `[Required]` do navigační vlastnosti instruktora, abyste určili, že musí existovat související instruktor, ale nemusíte to dělat, protože cizí klíč InstructorID (což je také klíč k této tabulce) nemůže mít hodnotu null.

## <a name="modify-the-course-entity"></a>Úprava entity kurzu

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

V *Models\Course.cs*nahraďte kód, který jste přidali dříve, pomocí následujícího kódu:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

Entita kurzu má vlastnost cizího klíče `DepartmentID` která odkazuje na související entitu `Department` a má vlastnost `Department` navigace. Entity Framework nevyžaduje, abyste do datového modelu přidali vlastnost cizího klíče, když máte vlastnost navigace pro související entitu. EF v databázi automaticky vytvoří cizí klíče bez ohledu na to, kde jsou potřeba. Ale při používání cizího klíče v datovém modelu může být aktualizace jednodušší a efektivnější. Když například načtete entitu kurzu, která se má upravit, `Department` entita má hodnotu null, pokud ji nenačtete, takže když aktualizujete entitu kurzu, museli byste nejdřív načíst `Department` entitu. Pokud je v datovém modelu zahrnutá vlastnost cizího klíče `DepartmentID`, nemusíte před zahájením aktualizace načíst entitu `Department`.

### <a name="the-databasegenerated-attribute"></a>Atribut DatabaseGenerated

[Atribut DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) s parametrem [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) u vlastnosti `CourseID` určuje, že uživatel zadá hodnoty primárního klíče místo vygenerovaného databází.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

Ve výchozím nastavení Entity Framework předpokládá, že se hodnoty primárního klíče generují v databázi. To je to, co chcete ve většině scénářů. U `Course` entit však použijete uživatelem zadané číslo kurzu, například 1000 series pro jedno oddělení, 2000 řady pro jiné oddělení atd.

### <a name="foreign-key-and-navigation-properties"></a>Vlastnosti cizích klíčů a navigace

Vlastnosti cizího klíče a navigační vlastnosti v entitě `Course` odrážejí následující vztahy:

- Kurz se přiřadí jednomu oddělení, takže je `DepartmentID` cizí klíč a vlastnost navigace `Department` z výše uvedených důvodů. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- Kurz může mít zaregistrovaný libovolný počet studentů, takže navigační vlastnost `Enrollments` je kolekce: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- Kurz může být výukou více instruktorů, takže navigační vlastnost `Instructors` je kolekce: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>Vytvoření entity oddělení

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

Vytvořte *Models\Department.cs* pomocí následujícího kódu:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Atribut Column

Dříve jste použili [atribut sloupce](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) pro změnu mapování názvu sloupce. V kódu pro entitu `Department` se atribut `Column` používá ke změně mapování datových typů SQL tak, aby byl sloupec definován pomocí SQL Server [peněžního](https://msdn.microsoft.com/library/ms179882.aspx) typu v databázi:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Mapování sloupce není obecně vyžadováno, protože Entity Framework obvykle zvolí vhodný SQL Server datový typ na základě typu CLR, který definujete pro vlastnost. Typ CLR `decimal` namapuje na typ `decimal` SQL Server. Ale v tomto případě víte, že se ve sloupci budou držet peněžní částky, a datový typ [Money](https://msdn.microsoft.com/library/ms179882.aspx) je pro to vhodnější.

### <a name="foreign-key-and-navigation-properties"></a>Vlastnosti cizích klíčů a navigace

Vlastnosti cizího klíče a navigace odrážejí následující vztahy:

- Oddělení může nebo nemusí mít správce a správce je vždy instruktorem. Proto je vlastnost `InstructorID` zahrnutá jako cizí klíč k entitě `Instructor` a otazník se přidá za označení `int`ho typu k označení vlastnosti jako Nullable. Navigační vlastnost má název `Administrator`, ale obsahuje `Instructor` entitu: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- Oddělení může mít mnoho kurzů, takže existuje `Courses` navigační vlastnost: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > Podle konvence Entity Framework umožňuje odstranit Kaskádové odstraňování cizích klíčů, které neumožňují hodnotu null, a pro relace m:n. Výsledkem může být cyklická kaskádová odstranění pravidel, která způsobí výjimku při spuštění kódu inicializátoru. Například pokud jste nedefinovali vlastnost `Department.InstructorID` jako Nullable, při spuštění inicializátoru se zobrazí následující zpráva o výjimce: "referenční relace bude mít za následek cyklický odkaz, který není povolený." Pokud vaše obchodní pravidla vyžadují `InstructorID` vlastnost jako nenulovou hodnotu, budete muset pomocí následujících rozhraní API Fluent zakázat kaskádové odstranění u vztahu: 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modifying-the-student-entity"></a>Úprava entity studenta

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

V *Models\Student.cs*nahraďte kód, který jste přidali dříve, pomocí následujícího kódu. Změny jsou zvýrazněny.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>Entita registrace

 V *Models\Enrollment.cs*nahraďte kód, který jste přidali dříve, pomocí následujícího kódu.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>Vlastnosti cizích klíčů a navigace

Vlastnosti cizího klíče a vlastnosti navigace odrážejí následující vztahy:

- Záznam zápisu je pro jeden kurz, takže existuje `CourseID` vlastnost cizího klíče a vlastnost navigace `Course`: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- Záznam zápisu je určen pro jednoho studenta, takže existuje `StudentID` vlastnost cizího klíče a `Student` navigační vlastnost: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>Relace m:n

Mezi entitami `Student` a `Course` existuje vztah n:n a entita `Enrollment` funguje jako tabulka JOIN typu m:n *s datovou částí* v databázi. To znamená, že tabulka `Enrollment` obsahuje další data kromě cizích klíčů pro Spojené tabulky (v tomto případě primární klíč a vlastnost `Grade`).

Následující ilustrace znázorňuje, co tyto vztahy vypadají jako v diagramu entit. (Tento diagram byl vygenerován pomocí [Entity Framework nástrojů pro napájení](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d). Vytvoření diagramu není součástí kurzu, je zde pouze použito jako ilustrace.)

![Student – Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

Každá čára relace má 1 na jednom konci a hvězdičku (\*) na druhé straně, která indikuje relaci 1: n.

Pokud tabulka `Enrollment` neobsahovala informace o třídě, musí obsahovat pouze dva cizí klíče `CourseID` a `StudentID`. V takovém případě by to odpovídalo tabulkám JOIN m:n *bez datové části* (nebo *čisté joinové tabulky*) v databázi a nemuseli byste pro ni vytvořit třídu modelu. Entity `Instructor` a `Course` mají tento druh relace m:n a jak vidíte, neexistuje mezi nimi žádná třída entit:

![Instruktor – Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

V databázi se ale vyžaduje tabulka JOIN, jak je znázorněno v následujícím databázovém diagramu:

![Instruktor – Course_many-to-many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Entity Framework automaticky vytvoří tabulku `CourseInstructor` a Vy ji přečtete a aktualizujete nepřímo pomocí čtení a aktualizace vlastností navigace `Instructor.Courses` a `Course.Instructors`.

## <a name="entity-diagram-showing-relationships"></a>Diagram entit znázorňující vztahy

Následující ilustrace znázorňuje diagram, který nástroje Entity Framework Power Tools vytvoří pro dokončený školní model.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Kromě řádků relace m:n (\* to \*) a čar vztahů 1:1 (1 – n \*) v rámci vztahu mezi entitami instruktor a Department (0.. 1, \*) mezi entitami instruktora a oddělení můžete vidět čáru relace 1:1 nebo jedna (1 – 0.. 1) mezi entitami `Instructor` a `OfficeAssignment` a řádkem relace nula nebo jedna-n.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>Přizpůsobení datového modelu přidáním kódu do kontextu databáze

Dále přidáte nové entity do třídy `SchoolContext` a přizpůsobíte některé mapování pomocí volání [Fluent API](https://msdn.microsoft.com/data/jj591617) . (Rozhraní API je "Fluent", protože se často používá k zřetězení řady volání metody do jednoho příkazu.)

V tomto kurzu použijete rozhraní Fluent API jenom pro mapování databáze, které nemůžete s atributy dělat. Rozhraní Fluent API ale můžete použít i k určení většiny pravidel formátování, ověřování a mapování, která můžete provádět pomocí atributů. Některé atributy, jako je `MinimumLength`, se nedají použít s rozhraním API Fluent. Jak bylo zmíněno dříve, `MinimumLength` nemění schéma, používá pouze pravidlo ověřování na straně klienta a serveru.

Někteří vývojáři dávají přednost použití rozhraní Fluent API, aby mohli zachovat třídy entit "vyčistit". V případě potřeby můžete kombinovat atributy a rozhraní API Fluent a existuje několik úprav, které je možné provést jenom pomocí rozhraní Fluent API, ale obecně doporučujeme zvolit jednu z těchto dvou přístupů a použít ji konzistentně co nejvíce.

Chcete-li přidat nové entity do datového modelu a provést mapování databáze, které jste neprováděli pomocí atributů, nahraďte kód v *DAL\SchoolContext.cs* následujícím kódem:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

V příkazu New v metodě [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) se konfiguruje tabulka JOIN m:n:

- Pro relaci n:n mezi `Instructor` a `Course` entit kód určuje názvy tabulek a sloupců pro spojovací tabulku. Code First může nakonfigurovat relaci m:n pro vás bez tohoto kódu, ale pokud ji nebudete volat, pro sloupec `InstructorID` se zobrazí výchozí názvy, jako je například `InstructorInstructorID`.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

Následující kód poskytuje příklad způsobu, jakým byste mohli použít rozhraní Fluent API namísto atributů k určení vztahu mezi `Instructor` a `OfficeAssignment`mi entitami:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

Informace o tom, co se děje s příkazy "Fluent API" na pozadí, najdete v blogovém příspěvku [rozhraní Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) .

## <a name="seed-the-database-with-test-data"></a>Dosazení databáze pomocí testovacích dat

Nahraďte kód v souboru *Migrations\Configuration.cs* následujícím kódem, aby bylo možné poskytnout počáteční data pro nové entity, které jste vytvořili.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

Jak jste viděli v prvním kurzu, většinu tohoto kódu jednoduše aktualizuje nebo vytvoří nové objekty entit a načte vzorová data do vlastností podle potřeby pro testování. Všimněte si však, jak je zpracována entita `Course`, která má relaci n:n s `Instructor`ou entitou:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

Při vytváření objektu `Course` inicializujete `Instructors` navigační vlastnost jako prázdnou kolekci pomocí `Instructors = new List<Instructor>()`kódu. Díky tomu je možné přidat `Instructor` entit, které se vztahují k tomuto `Course` pomocí metody `Instructors.Add`. Pokud jste nevytvořili prázdný seznam, nebudete moct přidat tyto relace, protože vlastnost `Instructors` by měla hodnotu null a neměli byste mít `Add` metodu. Můžete také přidat inicializaci seznamu do konstruktoru.

## <a name="add-a-migration-and-update-the-database"></a>Přidání migrace a aktualizace databáze

V PMC zadejte příkaz `add-migration`:

`PM> add-Migration Chap4`

Pokud se pokusíte databázi v tomto okamžiku aktualizovat, zobrazí se následující chyba:

*Příkaz ALTER TABLE je v konfliktu s omezením CIZÍho klíče "FK\_dbo. Kurz\_dbo. Oddělení\_DepartmentID ". Ke konfliktu došlo v databázi "ContosoUniversity", tabulce "dbo". Oddělení ", sloupec" DepartmentID ".*

Upravte &lt;*časového razítka&gt;souboru \_Chap4.cs* a proveďte následující změny kódu (PŘIDÁTE příkaz SQL a upravíte příkaz `AddColumn`):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(Pokud přidáte nový `AddColumn` řádek, nezapomeňte přidat nebo odstranit existující řádek, nebo při zadání příkazu `update-database` se zobrazí chyba.)

Při provádění migrace s existujícími daty je někdy potřeba do databáze vložit zástupná data, aby se splnila omezení cizího klíče, a to je to, co právě děláte. Vygenerovaný kód přidá do tabulky `Course` `DepartmentID` cizí klíč, který nemůže mít hodnotu null. Pokud jsou v tabulce `Course` již řádky, když je spuštěn kód, operace `AddColumn` by nedošlo k chybě, protože SQL Server neví, jakou hodnotu umístit do sloupce, který nemůže mít hodnotu null. Proto jste změnili kód tak, aby novému sloupci poskytoval výchozí hodnotu, a vytvořili jste oddělení zástupných procedur s názvem "Temp", které bude fungovat jako výchozí oddělení. Výsledkem je, že pokud při spuštění tohoto kódu existují `Course` řádky, všechny budou v souvislosti s oddělením "dočasné".

Když se metoda `Seed` spustí, vloží řádky do tabulky `Department` a bude se vztahovat na stávající `Course` řádky na tyto nové `Department` řádky. Pokud jste v uživatelském rozhraní nepřidali žádné kurzy, nebudete už potřebovat "dočasné" oddělení nebo výchozí hodnotu ve sloupci `Course.DepartmentID`. Chcete-li umožnit možnost, že někdo mohl přidat kurzy pomocí aplikace, měli byste také aktualizovat kód metody `Seed`, abyste zajistili, že všechny `Course` řádky (ne pouze ty vložené v předchozích verzích `Seed` metody) mají platné hodnoty `DepartmentID` před odebráním výchozí hodnoty ze sloupce a odstraněním "dočasného" oddělení.

Po dokončení úprav &lt;*časového razítka&gt;souboru \_Chap4.cs* zadejte do PMC příkaz `update-database` a spusťte migraci.

> [!NOTE]
> Při migraci dat a provádění změn schématu je možné získat další chyby. Pokud se zobrazí chyby migrace, které nemůžete vyřešit, můžete buď změnit připojovací řetězec v souboru *Web. config* nebo odstranit databázi. Nejjednodušším přístupem je přejmenovat databázi v souboru *Web. config* . Například změňte název databáze na CU\_test, jak je znázorněno v následujícím příkladu:
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
> V případě nové databáze nejsou k dispozici žádná data k migraci a příkaz `update-database` je mnohem větší, než může být dokončena bez chyb. Pokyny k odstranění databáze naleznete v tématu [How to drop a Database from a Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).

Otevřete databázi v **Průzkumník serveru** jako dříve a rozbalte uzel **tabulky** , abyste viděli, že se vytvořily všechny tabulky. (Pokud stále **Průzkumník serveru** otevřít z dřívějšího času, klikněte na tlačítko **aktualizovat** .)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

Pro `CourseInstructor` tabulku jste nevytvořili třídu modelu. Jak bylo vysvětleno dříve, jedná se o spojovací tabulku pro relaci n:n mezi `Instructor` a `Course` entitami.

Klikněte pravým tlačítkem myši na `CourseInstructor` tabulku a vyberte možnost **Zobrazit data tabulky** a ověřte, zda obsahuje data v důsledku `Instructor`ch entit, které jste přidali do vlastnosti `Course.Instructors` navigace.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>Přehled

Teď máte složitější datový model a odpovídající databázi. V následujícím kurzu se dozvíte víc o různých způsobech přístupu k souvisejícím datům.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Předchozí](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Další](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
