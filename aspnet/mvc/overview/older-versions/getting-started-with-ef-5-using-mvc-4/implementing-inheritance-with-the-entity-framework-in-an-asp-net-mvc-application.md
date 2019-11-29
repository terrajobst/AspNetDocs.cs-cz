---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: Implementace dědičnosti s Entity Framework v aplikaci ASP.NET MVC (8 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595322"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>Implementace dědičnosti s Entity Framework v aplikaci ASP.NET MVC (8 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozím kurzu jste zpracovali výjimky souběžnosti. Tento kurz vám ukáže, jak implementovat dědičnost v datovém modelu.

V objektově orientovaném programování můžete použít dědičnost k eliminaci nadbytečného kódu. V tomto kurzu změníte `Instructor` a `Student` třídy tak, aby byly odvozeny ze `Person` základní třídy obsahující vlastnosti, jako `LastName`, které jsou společné pro instruktory i studenty. Nepřidáte ani neměníte žádné webové stránky, ale změníte část kódu a tyto změny se automaticky projeví v databázi.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>Dědičnost tabulek na základě hierarchie a typů

V objektově orientovaném programování můžete použít dědičnost, aby bylo snazší pracovat se souvisejícími třídami. Například třídy `Instructor` a `Student` v datovém modelu `School` sdílejí několik vlastností, což má za následek redundantní kód:

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

Předpokládejme, že chcete eliminovat redundantní kód pro vlastnosti, které jsou sdíleny `Instructor` a `Student` entit. Můžete vytvořit `Person` základní třídu, která obsahuje pouze tyto sdílené vlastnosti, a poté nastavit `Instructor` a `Student` entit z této základní třídy, jak je znázorněno na následujícím obrázku:

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

Existuje několik způsobů, jak lze tuto strukturu dědičnosti znázornit v databázi. Můžete mít `Person`ovou tabulku, která obsahuje informace o studentech i instruktorech v jedné tabulce. Některé sloupce by se mohly vztahovat jenom na instruktory (`HireDate`), některé jenom pro studenty (`EnrollmentDate`), u obou (`LastName`, `FirstName`). Obvykle byste měli sloupec *diskriminátoru* , který určuje, který typ každý řádek představuje. Sloupec diskriminátoru může mít například "instruktor" pro studenty a studenta.

![Tabulka-podle hierarchy_example](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

Tento model generování struktury dědičnosti entit z jedné databázové tabulky se nazývá dědičnost *typu tabulka-na hierarchii* (TPH).

Alternativou je, že databáze vypadá podobně jako struktura dědičnosti. Například můžete mít pouze pole název v tabulce `Person` a mají oddělené tabulky `Instructor` a `Student` s poli data.

![Tabulka-podle type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

Tento model vytvoření tabulky databáze pro každou třídu entity se nazývá dědičnost *tabulky podle typu* (TPT).

Vzory dědičnosti TPH obvykle poskytují lepší výkon v Entity Framework než TPT vzory dědičnosti, protože vzory TPT můžou mít za následek složité spojování dotazů. Tento kurz ukazuje, jak implementovat dědičnosti TPH. Provedete to provedením následujících kroků:

- Vytvořte třídu `Person` a změňte `Instructor` a `Student` třídy, aby byly odvozeny od `Person`.
- Přidejte kód mapování modelu do databáze do třídy kontextu databáze.
- Změňte `InstructorID` a `StudentID` odkazy v celém projektu na `PersonID`.

## <a name="creating-the-person-class"></a>Vytvoření třídy Person

 Poznámka: po vytvoření následujících tříd nebudete moct projekt zkompilovat, dokud neaktualizujete řadiče, které používají tyto třídy. 

Ve složce *modely* vytvořte *Person.cs* a nahraďte kód šablony následujícím kódem:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

V *Instructor.cs*odvodíte třídu `Instructor` z `Person` třídy a odstraňte pole klíč a název. Kód bude vypadat jako v následujícím příkladu:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Udělejte podobné změny v *student.cs*. Třída `Student` bude vypadat jako v následujícím příkladu:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>Přidání typu entity Person do modelu

Do *SchoolContext.cs*přidejte vlastnost `DbSet` pro typ entity `Person`:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

To je vše, co Entity Framework potřebuje, aby bylo možné nakonfigurovat dědičnost tabulek na hierarchii. Jak vidíte, po opětovném vytvoření databáze bude mít `Person` tabulku místo `Student` a `Instructor` tabulek.

## <a name="changing-instructorid-and-studentid-to-personid"></a>Změna InstructorID a StudentID na PersonID

V *SchoolContext.cs*změňte v příkazu instruktor-Course Mapping `MapRightKey("InstructorID")` na `MapRightKey("PersonID")`:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

Tato změna se nevyžaduje. pouze změní název sloupce InstructorID v tabulce m:n (n:n JOIN). Pokud jste název opustili jako InstructorID, aplikace bude pořád fungovat správně. Zde je dokončený *SchoolContext.cs*:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

Dále je třeba změnit `InstructorID` na `PersonID` a `StudentID` na `PersonID` v rámci projektu ***s výjimkou*** souborů migrace s časovým razítkem ve složce *migrace* . Chcete-li vyhledat a otevřít pouze soubory, které je třeba změnit, proveďte globální změnu otevřených souborů. Jediným souborem ve složce *migraces* , který byste měli změnit, je *Migrations\Configuration.cs.*

1. > [!IMPORTANT]
   > Začněte tím, že zavřete všechny otevřené soubory v aplikaci Visual Studio.
2. Klikněte na **Najít a nahradit – vyhledejte všechny soubory** v nabídce **Upravit** a pak vyhledejte všechny soubory v projektu, které obsahují `InstructorID`.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. V okně **výsledky hledání** otevřete každý soubor ***s výjimkou*** &lt;časového razítka&gt; *\_. cs* soubory migrace ve složce *migrace* dvakrát klikněte na jeden řádek pro každý soubor.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. Otevřete dialogové okno **nahradit v souborech** a změňte položku **Zobrazit ve** **všech otevřených dokumentech**.
5. Pomocí dialogového okna **nahradit v souborech** změňte všechny `InstructorID` na `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. Vyhledá všechny soubory v projektu, které obsahují `StudentID`.
7. V okně **výsledky hledání** otevřete každý soubor ***s výjimkou*** &lt;časového razítka&gt; *\_\** soubory migrace cs ve složce *migrace* dvakrát klikněte na jeden řádek pro každý soubor.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. Otevřete dialogové okno **nahradit v souborech** a změňte položku **Zobrazit ve** **všech otevřených dokumentech**.
9. Pomocí dialogového okna **nahradit v souborech** změňte všechny `StudentID` na `PersonID`.   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. Sestavte projekt.

(Všimněte si, že to ukazuje *nevýhodu* `classnameID`ho vzoru pro pojmenovávání primárních klíčů. Pokud jste pojmenovali ID primárního klíče bez předpony názvu třídy, *není* nyní nutné žádné přejmenování.)

## <a name="create-and-update-a-migrations-file"></a>Vytvoření a aktualizace souboru migrace

V konzole správce balíčků (PMC) zadejte následující příkaz:

`Add-Migration Inheritance`

Spusťte příkaz `Update-Database` v PMC. Příkaz v tomto okamžiku selže, protože máme existující data, která migrace nedokáže zpracovat. Zobrazí se následující chyba:

*Příkaz ALTER TABLE je v konfliktu s omezením CIZÍho klíče "FK\_dbo. Oddělení\_dbo. Person\_PersonID ". Ke konfliktu došlo v databázi "ContosoUniversity", tabulce "dbo". Person, sloupec ' PersonID '.*

Otevřete *migrace\&lt; timestamp&gt;\_Inheritance.cs* a nahraďte metodu `Up` následujícím kódem:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

Znovu spusťte příkaz `update-database`.

> [!NOTE]
> Při migraci dat a provádění změn schématu je možné získat další chyby. Pokud získáte chyby migrace, které nemůžete vyřešit, můžete pokračovat v kurzu změnou připojovacího řetězce v souboru *Web. config* nebo odstraněním databáze. Nejjednodušším přístupem je přejmenovat databázi v souboru *Web. config* . Například změňte název databáze na CU\_test, jak je znázorněno v následujícím příkladu:
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> V případě nové databáze nejsou k dispozici žádná data k migraci a příkaz `update-database` je mnohem větší, než může být dokončena bez chyb. Pokyny k odstranění databáze naleznete v tématu [How to drop a Database from a Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/). Pokud tento přístup potrváte, abyste mohli pokračovat v tomto kurzu, přeskočte na konci tohoto kurzu krok nasazení, protože nasazená lokalita by při automatickém spuštění migrace mohla získat stejnou chybu. Pokud chcete řešit potíže s chybami migrace, nejlepším prostředkem je Entity Framework fóra nebo StackOverflow.com.

## <a name="testing"></a>Testování

Spusťte web a vyzkoušejte různé stránky. Vše funguje stejně jako dříve.

V **Průzkumník serveru** rozbalte **SchoolContext** a pak **tabulky**a uvidíte, že tabulky **student** a **instruktor** byly nahrazeny tabulkou **Person** . Rozbalte tabulku **Person (osoba** ) a uvidíte, že obsahuje všechny sloupce, které se používají v tabulkách **student** a **instruktor** .

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Klikněte pravým tlačítkem myši na tabulku Person a potom kliknutím na možnost **Zobrazit data tabulky** zobrazte sloupec diskriminátor.

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

Následující diagram znázorňuje strukturu nové školní databáze:

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>Přehled

Pro třídy `Person`, `Student`a `Instructor` se teď implementovala dědičnost tabulky na hierarchii. Další informace o této a dalších strukturách dědičnosti najdete v tématu [strategie mapování dědičnosti](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) na blogu Morteza Manavi. V dalším kurzu uvidíte několik způsobů implementace úložiště a pracovní jednotky vzorů.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Předchozí](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Další](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
