---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 6 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 8bfbe74f90eb03ea9aab7610842ef2578e80d113
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564223"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 6

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="implementing-table-per-hierarchy-inheritance"></a>Implementace dědičnosti tabulek na hierarchii

V předchozím kurzu jste pracovali se souvisejícími daty přidáním a odstraněním relací a přidáním nové entity, která má relaci k existující entitě. Tento kurz vám ukáže, jak implementovat dědičnost v datovém modelu.

V objektově orientovaném programování můžete použít dědičnost, aby bylo snazší pracovat se souvisejícími třídami. Můžete například vytvořit `Instructor` a `Student` třídy, které jsou odvozeny ze `Person` základní třídy. Můžete vytvořit stejné typy struktur dědičnosti mezi entitami v Entity Framework.

V této části kurzu nevytvoříte žádné nové webové stránky. Místo toho přidáte odvozenou entitu do datového modelu a upravíte stávající stránky pro použití nových entit.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>Dědičnost tabulek na základě hierarchie a typů

Databáze může ukládat informace o souvisejících objektech v jedné tabulce nebo ve více tabulkách. Například v databázi `School` obsahuje `Person` tabulka informace o studentech i instruktorech v jedné tabulce. Některé sloupce se vztahují jenom na instruktory (`HireDate`), některé jenom pro studenty (`EnrollmentDate`) a některé z obou (`LastName`, `FirstName`).

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

Entity Framework můžete nakonfigurovat tak, aby vytvářela `Instructor` a `Student` entity, které dědí od `Person` entity. Tento model generování struktury dědičnosti entit z jedné databázové tabulky se nazývá dědičnost *typu tabulka-na hierarchii* (TPH).

Pro kurzy používá databáze `School` jiný vzor. Online kurzy a kurzy na pracovišti jsou uloženy v samostatných tabulkách, z nichž každá má cizí klíč, který odkazuje na `Course` tabulku. Informace společné pro oba typy kurzů jsou uloženy pouze v `Course` tabulce.

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

Entity Framework datový model můžete nakonfigurovat tak, aby entity `OnlineCourse` a `OnsiteCourse` dědily z `Course` entity. Tento model generování struktury dědičnosti entit z oddělených tabulek pro každý typ, přičemž každá samostatná tabulka odkazuje zpět na tabulku, která ukládá data společná pro všechny typy, se nazývá dědičnost *tabulky na typ* (TPT).

Vzory dědičnosti TPH obvykle poskytují lepší výkon v Entity Framework než TPT vzory dědičnosti, protože vzory TPT můžou mít za následek složité spojování dotazů. Tento návod ukazuje, jak implementovat dědičnost typu TPH. Provedete to provedením následujících kroků:

- Vytvoří `Instructor` a `Student` typy entit, které jsou odvozeny z `Person`.
- Přesuňte vlastnosti, které se vztahují k odvozeným entitám z `Person` entitě na odvozené entity.
- Nastavte omezení vlastností v odvozených typech.
- Nastavit entitu `Person` jako abstraktní entitu
- Namapujte každou odvozenou entitu na `Person` tabulku s podmínkou, která určuje, zda `Person` řádek představuje tento odvozený typ.

## <a name="adding-instructor-and-student-entities"></a>Přidávání entit instruktor a student

Otevřete soubor <em>SchoolModel. edmx</em> , klikněte pravým tlačítkem myši na neobsazenou oblast v návrháři, vyberte <strong>Přidat</strong>a pak vyberte <strong>entita</strong><em>.</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

V dialogovém okně **Přidat entitu** pojmenujte entitu `Instructor` a nastavte její **typ základního typu** na možnost `Person`.

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

Klikněte na tlačítko **OK**. Návrhář vytvoří entitu `Instructor`, která je odvozena od `Person` entity. Nová entita ještě nemá žádné vlastnosti.

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

Zopakováním postupu vytvoříte entitu `Student`, která se také odvozuje od `Person`.

Pouze instruktoři mají data o přijetí, takže je nutné přesunout tuto vlastnost z entity `Person` do entity `Instructor`. V entitě `Person` klikněte pravým tlačítkem na vlastnost `HireDate` a klikněte na **Vyjmout**. Pak klikněte pravým tlačítkem na **vlastnosti** v entitě `Instructor` a klikněte na **Vložit**.

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

Datum přijetí `Instructor` entitě nemůže být null. Klikněte pravým tlačítkem na vlastnost `HireDate`, klikněte na **vlastnosti**a potom v okně **vlastnosti** změňte `Nullable` na `False`.

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

Opakujte postup pro přesunutí vlastnosti `EnrollmentDate` z entity `Person` do entity `Student`. Ujistěte se, že jste také nastavili `Nullable` `False` pro vlastnost `EnrollmentDate`.

Teď, když `Person` entita obsahuje jenom vlastnosti, které jsou společné pro `Instructor` a `Student` entit (kromě navigačních vlastností, které nepřesouváte), entitu jde ve struktuře dědičnosti použít jenom jako základní entitu. Proto je nutné se ujistit, že se nikdy nepovažuje za nezávislou entitu. Klikněte pravým tlačítkem na entitu `Person`, vyberte možnost **vlastnosti**a potom v okně **vlastnosti** změňte hodnotu vlastnosti **abstract** na hodnotu **true**.

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>Mapování entit instruktor a student na tabulku Person

Nyní potřebujete sdělit Entity Framework, jak odlišit `Instructor` a `Student` entity v databázi.

Klikněte pravým tlačítkem na entitu `Instructor` a vyberte **mapování tabulky**. V okně **Podrobnosti mapování** klikněte na **Přidat tabulku nebo zobrazení** a vyberte **osoba**.

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

Klikněte na **Přidat podmínku**a pak vyberte **ZaměstnánOd**.

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

Změňte **operátor** na hodnotu a **hodnotu nebo vlastnost** na **NOT NULL**.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

Opakujte postup pro entitu `Students` a určete, že tato entita se mapuje na tabulku `Person`, pokud sloupec `EnrollmentDate` není null. Pak datový model uložte a zavřete.

Sestavte projekt, aby se vytvořily nové entity jako třídy a aby byly dostupné v návrháři.

## <a name="using-the-instructor-and-student-entities"></a>Použití entit instruktor a student

Když jste vytvořili webové stránky, které pracují s daty student a instruktor, budete je mít k dispozici pro `Person` sadu entit a Vy jste filtrem `HireDate` nebo `EnrollmentDate` omezili vrácená data pro studenty nebo instruktory. Když ale teď svážete jednotlivé ovládací prvky zdroje dat s `Person` sadou entit, můžete určit, že se mají vybrat jenom `Student` nebo `Instructor` typy entit. Vzhledem k tomu, že Entity Framework ví, jak rozlišit studenty a instruktory v sadě entit `Person`, můžete ručně zadaná nastavení vlastností `Where` odebrat.

V návrháři aplikace Visual Studio můžete určit typ entity, který by měl ovládací prvek `EntityDataSource` vybrat v rozevíracím seznamu **EntityTypeFilter** Průvodce `Configure Data Source`, jak je znázorněno v následujícím příkladu.

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

A v okně **vlastnosti** můžete odebrat hodnoty `Where` klauzulí, které už nejsou potřeba, jak je znázorněno v následujícím příkladu.

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

Vzhledem k tomu, že jste změnili kód pro `EntityDataSource` ovládací prvky pro použití atributu `ContextTypeName`, nemůžete spustit průvodce **konfigurací zdroje dat** na `EntityDataSource` ovládací prvky, které jste již vytvořili. Proto provedete požadované změny změnou kódu místo.

Otevřete stránku *students. aspx* . V ovládacím prvku `StudentsEntityDataSource` odeberte atribut `Where` a přidejte atribut `EntityTypeFilter="Student"`. Značky teď budou vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

Nastavením atributu `EntityTypeFilter` zajistíte, že ovládací prvek `EntityDataSource` vybere pouze zadaný typ entity. Pokud jste chtěli načíst `Student` i `Instructor` typy entit, nemusíte tento atribut nastavit. (Máte možnost načíst více typů entit s jedním `EntityDataSource` ovládacím prvkem pouze v případě, že ovládací prvek používáte pro přístup k datům jen pro čtení. Pokud k vložení, aktualizaci nebo odstranění entit používáte ovládací prvek `EntityDataSource` a pokud sada entit, na kterou je vázána, může obsahovat více typů, můžete pracovat pouze s jedním typem entity a Vy musíte nastavit tento atribut.)

Opakujte postup pro ovládací prvek `SearchEntityDataSource`, s výjimkou odebrání pouze části atributu `Where`, který vybere `Student` entit namísto zcela odebrání vlastnosti. Otevírací značka ovládacího prvku bude nyní vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

Spusťte stránku a ověřte, zda stále funguje stejně jako dříve.

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

Aktualizujte následující stránky, které jste vytvořili v předchozích kurzech, aby místo `Person` entit používaly nové entity `Student` a `Instructor`, a pak je spouštějí, aby se ověřilo, že fungují stejně jako dříve:

- V *StudentsAdd. aspx*přidejte `EntityTypeFilter="Student"` k ovládacímu prvku `StudentsEntityDataSource`. Značky teď budou vypadat podobně jako v následujícím příkladu: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- V části *About. aspx*přidejte `EntityTypeFilter="Student"` do ovládacího prvku `StudentStatisticsEntityDataSource` a odstraňte `Where="it.EnrollmentDate is not null"`. Značky teď budou vypadat podobně jako v následujícím příkladu: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- V *instruktorech. aspx* a *InstructorsCourses. aspx*přidejte `EntityTypeFilter="Instructor"` do ovládacího prvku `InstructorsEntityDataSource` a odstraňte `Where="it.HireDate is not null"`. Označení v *instruktorech. aspx* teď vypadá podobně jako v následujícím příkladu: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    Označení v *InstructorsCourses. aspx* teď bude vypadat jako v následujícím příkladu:

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

V důsledku těchto změn jste vylepšili udržovatelnost aplikace Contoso University v několika ohledech. Přesunuli jste výběr a logiku ověřování z vrstvy uživatelského rozhraní (kód*aspx* ) a vytvořili jste nedílnou součást vrstvy přístupu k datům. Díky tomu je možné izolovat kód aplikace od změn, které můžete v budoucnu udělat pro schéma databáze nebo datový model. Můžete se třeba rozhodnout, že studenti můžou být zařazeni jako učitelé, a proto by získali datum přijetí. Pak můžete přidat novou vlastnost, která bude odlišit studenty od instruktorů a aktualizuje datový model. Žádný kód webové aplikace by se neměl měnit s výjimkou případů, kdy jste chtěli zobrazit datum přijetí studentů. Další výhodou přidání `Instructor` a `Student`ch entit je, že váš kód je snadněji srozumitelnější než při uvedení `Person` objektů, které byly ve skutečnosti studenty nebo instruktory.

Nyní jste viděli jeden ze způsobů implementace vzoru dědičnosti v Entity Framework. V následujícím kurzu se dozvíte, jak pomocí uložených procedur získat větší kontrolu nad tím, jak Entity Framework přistupuje k databázi.

> [!div class="step-by-step"]
> [Předchozí](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [Další](the-entity-framework-and-aspnet-getting-started-part-7.md)
