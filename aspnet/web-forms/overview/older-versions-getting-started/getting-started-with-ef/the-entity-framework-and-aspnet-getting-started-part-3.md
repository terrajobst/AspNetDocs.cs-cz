---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 3 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 88debb11a9157dce9ff000b1cb459b876dbceaf3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78643246"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 3

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="filtering-ordering-and-grouping-data"></a>Filtrování, řazení a seskupování dat

V předchozím kurzu jste použili ovládací prvek `EntityDataSource` k zobrazení a úpravě dat. V tomto kurzu budete filtrovat, řadit a seskupovat data. Pokud to provedete nastavením vlastností ovládacího prvku `EntityDataSource`, syntaxe se liší od jiných ovládacích prvků zdroje dat. Jak vidíte, můžete však použít ovládací prvek `QueryExtender` k minimalizaci těchto rozdílů.

Stránku *students. aspx* změníte pro filtrování studentů, řazení podle názvu a hledání názvu. Můžete také změnit stránku *kurzy. aspx* a zobrazit si kurzy pro vybrané oddělení a vyhledat kurzy podle jména. Nakonec přidáte do stránky *About. aspx* statistiku studenta.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>Použití vlastnosti EntityDataSource "Where" k filtrování dat

Otevřete stránku *students. aspx* , kterou jste vytvořili v předchozím kurzu. V případě, že je aktuálně nakonfigurován, ovládací prvek `GridView` na stránce zobrazí všechny názvy ze `People` sady entit. Chcete-li však zobrazit pouze studenty, které lze najít, vyberte `Person` entity, které mají data registrace, která nejsou null.

Přepněte do zobrazení **Návrh** a vyberte ovládací prvek `EntityDataSource`. V okně **vlastnosti** nastavte vlastnost `Where` na hodnotu `it.EnrollmentDate is not null`.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

Syntaxe, kterou použijete ve vlastnosti `Where` ovládacího prvku `EntityDataSource` je Entity SQL. Entity SQL se podobá jazyku Transact-SQL, ale je přizpůsobená pro použití s entitami spíše než databázovými objekty. Ve výrazu `it.EnrollmentDate is not null`slovo `it` představuje odkaz na entitu vrácenou dotazem. Proto `it.EnrollmentDate` odkazuje na vlastnost `EnrollmentDate` entity `Person`, kterou vrátí ovládací prvek `EntityDataSource`.

Spusťte stránku. Seznam studentů teď obsahuje jenom studenty. (Nejsou zobrazeny žádné řádky, pokud není k dispozici žádné datum registrace.)

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>Použití vlastnosti OrderBy EntityDataSource k objednání dat

Také chcete, aby byl tento seznam v pořadí podle názvu, když se poprvé zobrazuje. Když je stránka *studenty. aspx* stále otevřená v zobrazení **Návrh** a stále je vybraný ovládací prvek `EntityDataSource`, v okně **vlastnosti** nastavte vlastnost **OrderBy** na hodnotu `it.LastName`.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

Spusťte stránku. Seznam studentů je teď v pořadí podle příjmení.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>Použití parametru ovládacího prvku pro nastavení vlastnosti Where

Stejně jako ostatní ovládací prvky zdroje dat můžete hodnoty parametrů předat vlastnosti `Where`. Na stránce tutorial *. aspx* , kterou jste vytvořili v části 2 tohoto kurzu, můžete použít tuto metodu k zobrazení kurzů přidružených k oddělení, které uživatel vybere v rozevíracím seznamu.

Otevřete *kurzy. aspx* a přepněte se do zobrazení **Návrh** . Přidejte na stránku druhý ovládací prvek `EntityDataSource` a pojmenujte ho `CoursesEntityDataSource`. Připojte ho k `SchoolEntities`mu modelu a jako hodnotu **EntitySetName** vyberte `Courses`.

V okně **vlastnosti** klikněte na tlačítko se třemi tečkami v poli vlastnost **WHERE** . (Před použitím okna **vlastností** se ujistěte, že je ještě vybraný ovládací prvek `CoursesEntityDataSource`.)

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

Zobrazí se dialogové okno **Editor výrazů** . V tomto dialogovém okně vyberte **automaticky generovat výraz WHERE na základě zadaných parametrů**a pak klikněte na **Přidat parametr**. Pojmenujte parametr `DepartmentID`, jako **zdrojovou hodnotu parametru** vyberte **Control** a jako hodnotu **ControlID** vyberte **DepartmentsDropDownList** .

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

Klikněte na **Zobrazit upřesňující vlastnosti**a v okně **vlastnosti** dialogového okna **Editor výrazů** změňte vlastnost `Type` na `Int32`.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

Až to budete mít, klikněte na **OK**.

Pod rozevíracím seznamem přidejte do stránky ovládací prvek `GridView` a pojmenujte ho `CoursesGridView`. Připojte jej k ovládacímu prvku `CoursesEntityDataSource` zdroj dat, klikněte na tlačítko **Aktualizovat schéma**, klikněte na možnost **Upravit sloupce**a odeberte sloupec `DepartmentID`. Kód ovládacího prvku `GridView` se podobá následujícímu příkladu.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

Pokud uživatel změní vybrané oddělení v rozevíracím seznamu, chcete, aby se seznam přidružených kurzů automaticky změnil. Chcete-li k tomu dojít, vyberte rozevírací seznam a v okně **vlastnosti** nastavte vlastnost `AutoPostBack` na hodnotu `True`.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

Nyní, když jste dokončili používání návrháře, přepněte do zobrazení **zdroje** a nahraďte vlastnosti `ConnectionString` a `DefaultContainer` název ovládacího prvku `CoursesEntityDataSource` atributem `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`. Až budete hotovi, značky pro ovládací prvek budou vypadat jako v následujícím příkladu.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

Spusťte stránku a pomocí rozevíracího seznamu vyberte různá oddělení. V ovládacím prvku `GridView` se zobrazí jenom kurzy, které nabízí vybrané oddělení.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>Použití vlastnosti GroupBy ovládacího prvku GroupBy k seskupení dat

Předpokládejme, že společnost Contoso University chce na svou stránku umístit nějaké statistiky těla studenta. Konkrétně chce zobrazit rozpis počtu studentů podle data, která zapsala.

Otevřete *About. aspx*a v zobrazení **zdroj** nahraďte stávající obsah ovládacího prvku `BodyContent` textem "Statistika textu studenta" mezi značkami `h2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

Po záhlaví přidejte ovládací prvek `EntityDataSource` a pojmenujte ho `StudentStatisticsEntityDataSource`. Připojte ho k `SchoolEntities`, vyberte sadu entit `People` a nechejte pole pro **Výběr** v průvodci beze změny. V okně **vlastnosti** nastavte následující vlastnosti:

- Chcete-li filtrovat pouze studenty, nastavte vlastnost `Where` na hodnotu `it.EnrollmentDate is not null`.
- Chcete-li seskupit výsledky podle data registrace, nastavte vlastnost `GroupBy` na hodnotu `it.EnrollmentDate`.
- Chcete-li vybrat datum registrace a počet studentů, nastavte vlastnost `Select` na hodnotu `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`.
- Chcete-li seřadit výsledky podle data registrace, nastavte vlastnost `OrderBy` na hodnotu `it.EnrollmentDate`.

V zobrazení **zdroj** nahraďte vlastnosti `ConnectionString` a `DefaultContainer` název vlastností `ContextTypeName`. Označení ovládacího prvku `EntityDataSource` nyní vypadá podobně jako v následujícím příkladu.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

Syntaxe vlastností `Select`, `GroupBy`a `Where` se podobá jazyku Transact-SQL s výjimkou klíčového slova `it`, které určuje aktuální entitu.

Přidejte následující kód pro vytvoření `GridView` ovládacího prvku pro zobrazení dat.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

Spuštěním stránky zobrazíte seznam obsahující počet studentů podle data registrace.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>Použití ovládacího prvku třídou QueryExtender pro filtrování a řazení

Ovládací prvek `QueryExtender` poskytuje způsob, jak zadat filtrování a řazení v kódu. Syntaxe je nezávislá na systému správy databáze (DBMS), který používáte. Je také všeobecně nezávislá na Entity Framework, s výjimkou, že syntaxe, kterou používáte pro navigační vlastnosti, je pro Entity Framework jedinečná.

V této části kurzu použijete ovládací prvek `QueryExtender` k filtrování a objednání dat a jedno z polí ORDER by bude navigační vlastnost.

(Pokud dáváte přednost použití kódu místo označení pro rozšiřování dotazů, které jsou automaticky generovány ovládacím prvkem `EntityDataSource`, můžete to provést zpracováním události `QueryCreated`. To je způsob, jakým ovládací prvek `QueryExtender` rozšiřuje dotazy na `EntityDataSource`.)

Otevřete stránku *kurzy. aspx* a pod značkou, kterou jste přidali dříve, vložte následující kód, který vytvoří nadpis, textové pole pro zadání vyhledávacích řetězců, tlačítko vyhledávání a `EntityDataSource` ovládacího prvku, který je svázán se sadou entit `Courses`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

Všimněte si, že vlastnost `Include` ovládacího prvku `EntityDataSource` je nastavena na hodnotu `Department`. V databázi `Course` tabulka neobsahuje název oddělení; obsahuje `DepartmentID` sloupec cizího klíče. Pokud jste se dotazovat na databázi přímo, abyste získali název oddělení spolu s daty kurzu, museli byste se připojit k tabulkám `Course` a `Department`. Nastavením vlastnosti `Include` na `Department`zadáte, že by Entity Framework měla dělat možnost získat související `Department` entitu, když získá `Course` entitu. Entita `Department` se pak uloží do navigační vlastnosti `Department` entity `Course`. (Ve výchozím nastavení třída `SchoolEntities`, která byla generována návrhářem datového modelu, načte související data, když je potřeba, a Vy jste na tuto třídu nastavili řízení zdrojů dat, takže není nutné nastavit vlastnost `Include`. Nicméně nastavení zvyšuje výkon stránky, protože v opačném případě by Entity Framework provedla samostatná volání databáze k načtení dat pro `Course` entit a pro související entity `Department`.)

Po právě vytvořeném ovládacím prvku `EntityDataSource` vložte následující kód, který vytvoří `QueryExtender` ovládací prvek vázaný na tento ovládací prvek `EntityDataSource`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

Element `SearchExpression` určuje, že chcete vybrat kurzy, jejichž názvy odpovídají hodnotě zadané v textovém poli. Porovná se pouze tolik znaků, kolik je zadáno v textovém poli, protože vlastnost `SearchType` určuje `StartsWith`.

Element `OrderByExpression` určuje, že sada výsledků bude seřazena podle názvu kurzu v rámci názvu oddělení. Všimněte si, jak je zadáno jméno oddělení: `Department.Name`. Vzhledem k tomu, že přidružení mezi `Course` entitou a entitou `Department` je 1:1, vlastnost `Department` navigace obsahuje entitu `Department`. (Pokud se jednalo o relaci 1: n, vlastnost by obsahovala kolekci.) Chcete-li získat název oddělení, je nutné zadat vlastnost `Name` entity `Department`.

Nakonec přidejte ovládací prvek `GridView` pro zobrazení seznamu kurzů:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

První sloupec je pole šablony, které zobrazuje název oddělení. Výraz datové vazby Určuje `Department.Name`stejným způsobem, jako jste viděli v ovládacím prvku `QueryExtender`.

Spusťte stránku. Počáteční zobrazení zobrazuje seznam všech kurzů v pořadí podle jednotlivých oddělení a potom podle názvu kurzu.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

Zadejte "m" a kliknutím na **Hledat** zobrazte všechny kurzy, jejichž názvy začínají znakem "m" (hledání nerozlišuje malá a velká písmena).

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>Použití operátoru "Like" k filtrování dat

Můžete dosáhnout efektu podobného ovládacímu prvku `QueryExtender` `StartsWith`, `Contains`a `EndsWith` typy hledání pomocí operátoru `Like` ve vlastnosti `EntityDataSource` ovládacího prvku `Where`. V této části kurzu se dozvíte, jak pomocí operátoru `Like` Hledat studenta podle jména.

Otevřete *studenty. aspx* v zobrazení **zdroje** . Po ovládacím prvku `GridView` přidejte následující kód:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

Tento kód se podobá tomu, co jste viděli dříve, s výjimkou hodnoty vlastnosti `Where`. Druhá část výrazu `Where` definuje dílčí řetězcové vyhledávání (`LIKE %FirstMidName% or LIKE %LastName%`), které v textovém poli vyhledá první i poslední název.

Spusťte stránku. Zpočátku vidíte všechny studenty, protože výchozí hodnota pro parametr `StudentName` je "%".

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

Do textového pole zadejte písmeno "g" a klikněte na tlačítko **Hledat**. Zobrazí se seznam studentů, které mají v prvním nebo posledním jménu "g".

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

Teď jste zobrazili, aktualizovali, vyfiltrováni, objednali a seskupili data z jednotlivých tabulek. V dalším kurzu začnete pracovat se souvisejícími daty (scénáře hlavních podrobností).

> [!div class="step-by-step"]
> [Předchozí](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [Další](the-entity-framework-and-aspnet-getting-started-part-4.md)
