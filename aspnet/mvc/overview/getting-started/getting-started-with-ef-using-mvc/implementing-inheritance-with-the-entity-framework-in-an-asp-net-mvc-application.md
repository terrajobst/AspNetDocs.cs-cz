---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: Implementace dědičnosti s EF v aplikacích ASP.NET MVC 5'
description: Tento kurz vám ukáže, jak implementovat dědičnost v datovém modelu.
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583060"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a>Kurz: Implementace dědičnosti s EF v aplikaci ASP.NET MVC 5

V předchozím kurzu jste zpracovali výjimky souběžnosti. Tento kurz vám ukáže, jak implementovat dědičnost v datovém modelu.

V objektově orientovaném programování můžete použít [Dědičnost](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) k usnadnění [opětovného použití kódu](http://en.wikipedia.org/wiki/Code_reuse). V tomto kurzu změníte `Instructor` a `Student` třídy tak, aby byly odvozeny ze `Person` základní třídy obsahující vlastnosti, jako `LastName`, které jsou společné pro instruktory i studenty. Nepřidáte ani neměníte žádné webové stránky, ale změníte část kódu a tyto změny se automaticky projeví v databázi.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Naučte se mapovat dědění na databázi.
> * Vytvoření třídy Person
> * Aktualizace instruktora a studenta
> * Přidat osobu do modelu
> * Vytváření a aktualizace migrací
> * Testování implementace
> * Nasazení do Azure

## <a name="prerequisites"></a>Předpoklady

* [Ošetření souběžnosti](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a>Mapování dědičnosti na databázi

Třídy `Instructor` a `Student` v datovém modelu `School` mají několik vlastností, které jsou identické:

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

Předpokládejme, že chcete eliminovat redundantní kód pro vlastnosti, které jsou sdíleny `Instructor` a `Student` entit. Nebo chcete napsat službu, která může formátovat názvy bez caring, jestli název pochází od instruktora nebo studenta. Můžete vytvořit `Person` základní třídu, která obsahuje pouze tyto sdílené vlastnosti, a poté nastavit `Instructor` a `Student` entit z této základní třídy, jak je znázorněno na následujícím obrázku:

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

Existuje několik způsobů, jak lze tuto strukturu dědičnosti znázornit v databázi. Můžete mít `Person`ovou tabulku, která obsahuje informace o studentech i instruktorech v jedné tabulce. Některé sloupce by se mohly vztahovat jenom na instruktory (`HireDate`), některé jenom pro studenty (`EnrollmentDate`), u obou (`LastName`, `FirstName`). Obvykle byste měli sloupec *diskriminátoru* , který určuje, který typ každý řádek představuje. Sloupec diskriminátoru může mít například "instruktor" pro studenty a studenta.

![Table-per-hierarchy_example](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

Tento model generování struktury dědičnosti entit z jedné databázové tabulky se nazývá dědičnost *typu tabulka-na hierarchii* (TPH).

Alternativou je, že databáze vypadá podobně jako struktura dědičnosti. Například můžete mít pouze pole název v tabulce `Person` a mají oddělené tabulky `Instructor` a `Student` s poli data.

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Tento model vytvoření tabulky databáze pro každou třídu entity se nazývá dědičnost *tabulky podle typu* (TPT).

Ještě další možností je mapovat všechny neabstraktní typy na jednotlivé tabulky. Všechny vlastnosti třídy, včetně děděných vlastností, jsou mapovány na sloupce odpovídající tabulky. Tento model se nazývá dědičnost tříd (TPC) podle konkrétní třídy. Pokud jste implementovali dědičnost TPC pro třídy `Person`, `Student`a `Instructor`, jak je uvedeno výše, tabulky `Student` a `Instructor` by po implementaci dědičnosti nevypadaly jinak než předtím.

Vzorce dědičnosti TPC a TPH obvykle poskytují lepší výkon ve vzorcích dědičnosti Entity Framework než TPT, protože vzory TPT můžou mít za následek složité spojování dotazů.

Tento kurz ukazuje, jak implementovat dědičnosti TPH. TPH je výchozím vzorem dědičnosti v Entity Framework, takže vše, co musíte udělat, je vytvořit `Person` třídy, změnit `Instructor` a `Student` třídy, aby byly odvozeny z `Person`, přidejte do `DbContext`novou třídu a vytvořte migraci. (Informace o tom, jak implementovat další vzory dědičnosti, najdete v tématu [mapování dědičnosti typu tabulka na typ (TPT)](https://msdn.microsoft.com/data/jj591617#2.5) a [mapování dědičnosti třídy (TPC) na konkrétní třídu ()](https://msdn.microsoft.com/data/jj591617#2.6) v dokumentaci MSDN Entity Framework.)

## <a name="create-the-person-class"></a>Vytvoření třídy Person

Ve složce *modely* vytvořte *Person.cs* a nahraďte kód šablony následujícím kódem:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a>Aktualizace instruktora a studenta

Teď aktualizujte *Instructor.cs* a *student.cs* , aby dědily hodnoty z *Person.SC*.

V *Instructor.cs*odvodíte třídu `Instructor` z `Person` třídy a odstraňte pole klíč a název. Kód bude vypadat jako v následujícím příkladu:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Udělejte podobné změny v *student.cs*. Třída `Student` bude vypadat jako v následujícím příkladu:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a>Přidat osobu do modelu

Do *SchoolContext.cs*přidejte vlastnost `DbSet` pro typ entity `Person`:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

To je vše, co Entity Framework potřebuje, aby bylo možné nakonfigurovat dědičnost tabulek na hierarchii. Jak vidíte, při aktualizaci databáze bude mít `Person` tabulku místo tabulek `Student` a `Instructor`.

## <a name="create-and-update-migrations"></a>Vytváření a aktualizace migrací

V konzole správce balíčků (PMC) zadejte následující příkaz:

`Add-Migration Inheritance`

Spusťte příkaz `Update-Database` v PMC. Příkaz v tomto okamžiku selže, protože máme existující data, která migrace nedokáže zpracovat. Zobrazí se chybová zpráva podobná následující:

> *Nelze vyřadit objekt dbo. Instructor, protože na něj odkazuje omezení CIZÍho klíče.*

Otevřete *migrace\&lt; timestamp&gt;\_Inheritance.cs* a nahraďte metodu `Up` následujícím kódem:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

Tento kód má na starosti následující úlohy aktualizace databáze:

- Odebere omezení a indexy cizího klíče, které odkazují na tabulku studenta.
- Přejmenuje tabulku instruktora jako osobu a provede změny potřebné k uložení dat studenta:

    - Přidá EnrollmentDate s možnou hodnotou null pro studenty.
    - Přidá sloupec diskriminátoru, který označuje, zda je řádek určen studentem nebo instruktorem.
    - Vytvoří hodnotu Nullable s možnou hodnotou null, protože řádky studenta nebudou mít data přijetí.
    - Přidá dočasné pole, které bude použito k aktualizaci cizích klíčů, které odkazují na studenty. Když zkopírujete studenty do tabulky Person, získají se nové hodnoty primárního klíče.
- Zkopíruje data z tabulky student do tabulky Person (osoba). To způsobí, že studenti získají přiřazené nové hodnoty primárního klíče.
- Opravuje hodnoty cizích klíčů, které odkazují na studenty.
- Znovu vytvoří omezení a indexy cizího klíče, které se teď odkazují na tabulku Person.

(Pokud jste použili GUID místo celého čísla jako typ primárního klíče, hodnoty primárního klíče studenta se nemusejí změnit a některé z těchto kroků by mohly být vynechány.)

Znovu spusťte příkaz `update-database`.

(V produkčním systému provedete odpovídající změny v metodě Down pro případ, že byste to museli použít pro návrat k předchozí verzi databáze. V tomto kurzu nebudete používat metodu Down.)

> [!NOTE]
> Při migraci dat a provádění změn schématu je možné získat další chyby. Pokud se zobrazí chyby migrace, které nemůžete vyřešit, můžete pokračovat v kurzu změnou připojovacího řetězce v souboru *Web. config* nebo odstraněním databáze. Nejjednodušším přístupem je přejmenovat databázi v souboru *Web. config* . Například změňte název databáze na ContosoUniversity2, jak je znázorněno v následujícím příkladu:
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> V případě nové databáze nejsou k dispozici žádná data k migraci a příkaz `update-database` je mnohem větší, než může být dokončena bez chyb. Pokyny k odstranění databáze naleznete v tématu [How to drop a Database from a Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/). Pokud tento přístup potrváte, abyste mohli pokračovat v tomto kurzu, přeskočte krok nasazení na konci tohoto kurzu nebo ho nasaďte na novou lokalitu a databázi. Pokud nasadíte aktualizaci na stejnou lokalitu, do které jste už nasadili, EF se při automatickém spuštění migrace zobrazí stejná chyba. Pokud chcete řešit potíže s chybami migrace, nejlepším prostředkem je Entity Framework fóra nebo StackOverflow.com.

## <a name="test-the-implementation"></a>Testování implementace

Spusťte web a vyzkoušejte různé stránky. Vše funguje stejně jako dříve.

V **Průzkumník serveru** rozbalte **Connections\SchoolContext data** a pak **tabulky**a uvidíte, že tabulky **student** a **instruktor** byly nahrazeny tabulkou **Person** . Rozbalte tabulku **Person (osoba** ) a uvidíte, že obsahuje všechny sloupce, které se používají v tabulkách **student** a **instruktor** .

Klikněte pravým tlačítkem myši na tabulku Person a potom kliknutím na možnost **Zobrazit data tabulky** zobrazte sloupec diskriminátor.

Následující diagram znázorňuje strukturu nové školní databáze:

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>Nasazení do Azure

Tato část vyžaduje, abyste dokončili volitelné **nasazení aplikace do Azure** v [části 3, řazení, filtrování a stránkování](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) této série kurzů. Pokud jste převedli chyby, které jste vyřešili odstraněním databáze v místním projektu, přeskočte tento krok; nebo vytvořte novou lokalitu a databázi a nasaďte ji do nového prostředí.

1. V aplikaci Visual Studio klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a v místní nabídce vyberte **publikovat** .

2. Klikněte na **Publikovat**.

    Webová aplikace se otevře ve výchozím prohlížeči.

3. Otestujte aplikaci, abyste ověřili, že funguje.

    Při prvním spuštění stránky, která přistupuje k databázi, Entity Framework spustí všechny migrace `Up` metody potřebné k zajištění aktuálnosti databáze s aktuálním datovým modelem.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

Další informace o této a dalších strukturách dědičnosti najdete v tématu model [dědičnosti TPT](https://msdn.microsoft.com/data/jj618293) a [vzor dědičnosti TPH](https://msdn.microsoft.com/data/jj618292) na webu MSDN. V dalším kurzu se dozvíte, jak zvládnout celou řadu poměrně pokročilých scénářů Entity Framework.

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Bylo naučeno k mapování dědičnosti na databázi.
> * Byla vytvořena třída Person.
> * Aktualizovaný instruktor a student
> * Do modelu se přidala osoba.
> * Vytvořené a aktualizované migrace
> * Otestování implementace
> * Nasazené do Azure

V dalším článku se dozvíte o tématech, o kterých je užitečné vědět, když překročíte základy vývoje webových aplikací ASP.NET, které používají Entity Framework Code First.
> [!div class="nextstepaction"]
> [Pokročilé scénáře pro Entity Framework](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
