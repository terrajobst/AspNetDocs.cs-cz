---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 7 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603430"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 7

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="using-stored-procedures"></a>Použití uložených procedur

V předchozím kurzu jste implementovali vzor dědičnosti tabulky na hierarchii. V tomto kurzu se dozvíte, jak pomocí uložených procedur získat větší kontrolu nad přístupem k databázi.

Entity Framework vám umožní určit, že má používat uložené procedury pro přístup k databázi. Pro libovolný typ entity můžete zadat uloženou proceduru, která se má použít k vytvoření, aktualizaci nebo odstranění entit daného typu. V datovém modelu pak můžete přidat odkazy na uložené procedury, které lze použít k provádění úloh, jako je například načítání sad entit.

Použití uložených procedur je běžným požadavkem pro přístup k databázi. V některých případech může správce databáze vyžadovat, aby všechny přístupy k databázi procházely prostřednictvím uložených procedur z bezpečnostních důvodů. V jiných případech může být vhodné vytvořit obchodní logiku do některých procesů, které Entity Framework používá při aktualizaci databáze. Například pokaždé, když se odstraní entita, může být vhodné ji zkopírovat do archivní databáze. Nebo kdykoli je řádek aktualizován, může být vhodné zapsat řádek do tabulky protokolování, která zaznamenává, kdo provedl změnu. Tyto typy úloh můžete provádět v uložené proceduře, která je volána vždy, když Entity Framework odstraní entitu nebo aktualizuje entitu.

Stejně jako v předchozím kurzu nebudete vytvářet žádné nové stránky. Místo toho změníte způsob, jakým Entity Framework přistupuje k databázi pro některé stránky, které jste už vytvořili.

V tomto kurzu vytvoříte uložené procedury v databázi pro vkládání entit `Student` a `Instructor`. Přidáte je do datového modelu a určíte, že Entity Framework by je měli použít pro přidání `Student` a `Instructor` entit do databáze. Vytvoříte také uloženou proceduru, kterou můžete použít k načtení entit `Course`.

## <a name="creating-stored-procedures-in-the-database"></a>Vytváření uložených procedur v databázi

(Pokud používáte soubor *School. mdf* z projektu, který je k dispozici ke stažení v tomto kurzu, můžete tento oddíl přeskočit, protože uložené procedury již existují.)

V **Průzkumník serveru**rozbalte *School. mdf*, klikněte pravým tlačítkem na **uložené procedury**a vyberte **Přidat novou uloženou proceduru**.

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

Zkopírujte následující příkazy SQL a vložte je do okna uložené procedury, kde nahradíte kostru uložené procedury.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` entit mají čtyři vlastnosti: `PersonID`, `LastName`, `FirstName`a `EnrollmentDate`. Databáze automaticky vygeneruje hodnotu ID a uložená procedura akceptuje parametry pro ostatní tři. Uložená procedura vrátí hodnotu klíče záznamu nového řádku, aby Entity Framework mohl sledovat to, co je ve verzi entity, kterou udržuje v paměti.

Uložte a zavřete okno uložená procedura.

Vytvořte `InsertInstructor` uloženou proceduru stejným způsobem pomocí následujících příkazů SQL:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

Vytváření `Update` uložených procedur pro `Student` a `Instructor` entit. (Databáze již obsahuje `DeletePerson` uloženou proceduru, která bude fungovat pro `Instructor` a `Student` entit.)

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

V tomto kurzu namapujete všechny tři funkce--INSERT, Update a DELETE – pro každý typ entity. Entity Framework verze 4 umožňuje mapovat pouze jednu nebo dvě z těchto funkcí na uložené procedury bez mapování ostatních, s jednou výjimkou: Pokud namapujete funkci Update, ale ne funkci odstranit, Entity Framework vyvolá výjimku při pokus o odstranění entity V Entity Framework verze 3,5 jste v rámci mapování uložených procedur neměli velkou flexibilitu: Pokud jste namapovali jednu funkci, kterou jste museli namapovat na všechny tři.

Chcete-li vytvořit uloženou proceduru, která místo aktualizací dat načítá data, vytvořte ji, která vybere všechny `Course` entit pomocí následujících příkazů SQL:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>Přidání uložených procedur do datového modelu

Uložené procedury jsou nyní definovány v databázi, ale musí být přidány do datového modelu, aby byly k dispozici pro Entity Framework. Otevřete *SchoolModel. edmx*, klikněte pravým tlačítkem myši na návrhovou plochu a vyberte **aktualizovat model z databáze**. Na kartě **Přidat** dialogového okna **zvolit objekty databáze** rozbalte **uložené procedury**, vyberte nově vytvořené uložené procedury a uloženou proceduru `DeletePerson` a pak klikněte na **Dokončit**.

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>Mapování uložených procedur

V návrháři datového modelu klikněte pravým tlačítkem na entitu `Student` a vyberte možnost **mapování uložených procedur**.

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

Zobrazí se okno **Podrobnosti mapování** , ve kterém můžete zadat uložené procedury, které má Entity Framework použít pro vkládání, aktualizaci a odstraňování entit tohoto typu.

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

Nastavte funkci **INSERT** na **InsertStudent**. V okně se zobrazí seznam parametrů uložených procedur, z nichž každá musí být namapována na vlastnost entity. Dvě z nich jsou namapovány automaticky, protože názvy jsou stejné. Neexistuje žádná vlastnost entity s názvem `FirstName`, takže musíte ručně vybrat `FirstMidName` z rozevíracího seznamu, který zobrazuje dostupné vlastnosti entity. (To je proto, že jste změnili název vlastnosti `FirstName` na `FirstMidName` v prvním kurzu.)

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

Ve stejném okně **podrobností mapování** namapujte funkci `Update` na `UpdateStudent` uloženou proceduru (Ujistěte se, že jste zadali `FirstMidName` jako hodnotu parametru pro `FirstName`, jako jste byli pro `Insert` uloženou proceduru) a `Delete` funkcí do uložené procedury `DeletePerson`.

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

Použijte stejný postup k namapování uložených procedur vložení, aktualizace a odstranění pro instruktory na `Instructor` entitu.

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

U uložených procedur, které jsou čteny namísto aktualizací dat, použijete okno **prohlížeče modelů** k namapování úložné procedury na typ entity, kterou vrátí. V návrháři datového modelu klikněte pravým tlačítkem myši na návrhovou plochu a vyberte možnost **prohlížeč modelů**. Otevřete uzel **SchoolModel. Store** a pak otevřete uzel **uložené procedury** . Pak klikněte pravým tlačítkem na uloženou proceduru `GetCourses` a vyberte **Přidat import funkce**.

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

V dialogovém okně **Přidat import funkce** v části **vrátí kolekci** vybraných **entit**a vyberte možnost `Course` jako typ entity vráceno. Až to budete mít, klikněte na **OK**. Uložte a zavřete soubor *. edmx* .

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>Použití uložených procedur INSERT, Update a DELETE

Uložené procedury pro vkládání, aktualizaci a odstraňování dat jsou Entity Framework automaticky používány po jejich přidání do datového modelu a namapovány na příslušné entity. Nyní můžete spustit stránku *StudentsAdd. aspx* a pokaždé, když vytvoříte nového studenta, Entity Framework použijí uloženou proceduru `InsertStudent` k přidání nového řádku do tabulky `Student`.

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

Spusťte stránku *students. aspx* a v seznamu se zobrazí nový student.

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

Změňte název, abyste ověřili, že funkce Update funguje a pak odstraňte studenta, abyste ověřili, že funkce Delete funguje.

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>Použití vybraných uložených procedur

Entity Framework nespouští automaticky uložené procedury, jako je například `GetCourses`, a nelze je použít s ovládacím prvkem `EntityDataSource`. Pokud je chcete použít, zavolejte je z kódu.

Otevřete soubor *InstructorsCourses.aspx.cs* . Metoda `PopulateDropDownLists` používá dotaz LINQ to-Entities k načtení všech entit kurzu, aby mohla procházet seznam a zjistit, které z nich je k dis a které jsou nepřiřazené:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

Nahraďte následujícím kódem:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

Stránka teď používá uloženou proceduru `GetCourses` k načtení seznamu všech kurzů. Spusťte stránku, abyste ověřili, že funguje stejně jako dříve.

(Navigační vlastnosti entit načtených uloženou procedurou nemusí být automaticky naplněny daty souvisejícími s těmito entitami v závislosti na `ObjectContext` výchozím nastavení. Další informace najdete v tématu [načítání souvisejících objektů](https://msdn.microsoft.com/library/bb896272.aspx) v knihovně MSDN.)

V dalším kurzu se dozvíte, jak používat funkci dynamických dat, aby bylo snazší programovat a testovat formátování dat a pravidla ověřování. Místo určení u každého pravidla webové stránky, jako jsou například řetězce formátu dat a zda je pole vyžadováno, můžete zadat taková pravidla v metadatech datového modelu a automaticky je použít na každé stránce.

> [!div class="step-by-step"]
> [Předchozí](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [Další](the-entity-framework-and-aspnet-getting-started-part-8.md)
