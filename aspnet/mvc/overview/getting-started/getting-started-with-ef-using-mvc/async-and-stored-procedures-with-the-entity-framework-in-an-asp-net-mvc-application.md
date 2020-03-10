---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: použití asynchronních a uložených procedur s EF v aplikaci ASP.NET MVC'
description: V tomto kurzu vidíte, jak implementovat asynchronní programovací model a Naučte se používat uložené procedury.
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583438"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a>Kurz: použití asynchronních a uložených procedur s EF v aplikaci ASP.NET MVC

V předchozích kurzech jste zjistili, jak číst a aktualizovat data pomocí synchronního programovacího modelu. V tomto kurzu vidíte, jak implementovat asynchronní programovací model. Asynchronní kód může zajistit lepší výkon aplikace, protože zajišťuje lepší využití prostředků serveru.

V tomto kurzu zjistíte také, jak používat uložené procedury pro operace vložení, aktualizace a odstranění u entity.

Nakonec aplikaci znovu nasadíte do Azure spolu se všemi změnami databáze, které jste implementovali od prvního nasazení.

Následující ilustrace znázorňují některé stránky, se kterými budete pracovat.

![Stránka oddělení](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Vytvořit oddělení](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Informace o asynchronním kódu
> * Vytvoření řadiče oddělení
> * Použití uložených procedur
> * Nasazení do Azure

## <a name="prerequisites"></a>Předpoklady

* [Aktualizace souvisejících dat](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a>Proč použít asynchronní kód

Webový server má omezený počet vláken, které jsou k dispozici, a v situacích, vysokého zatížení všech dostupných vláken může být používán. Pokud k tomu dojde, server nemůže zpracovat nové žádosti, dokud se uvolnit vlákna. Přestože se nejedná skutečně každé dílo vzhledem k tomu, že čekání na vstupně-výstupních operací na dokončení, může kódem synchronní svázané několika vlákny. Asynchronní kód když proces čeká na vstupně-výstupních operací na dokončení, je jeho vlákno uvolněn pro server určený pro zpracováním jiných požadavků. Výsledkem je, že asynchronní kód umožňuje efektivnější využití prostředků serveru a server je povolen pro zpracování většího objemu dat bez prodlev.

V dřívějších verzích rozhraní .NET byla psaní a testování asynchronního kódu složitá, náchylná k chybám a obtížné ladění. V rozhraní .NET 4,5, psaní, testování a ladění asynchronního kódu je mnohem jednodušší, že byste měli obecně zapisovat asynchronní kód, pokud nemáte důvod na. Asynchronní kód zavádí malé množství režijních nákladů, ale u situací s nízkým objemem provozu je dosaženo zanedbatelného výkonu, zatímco v případě vysoké situace v provozu je potenciální zlepšení výkonu značné.

Další informace o asynchronním programování naleznete v tématu [použití asynchronní podpory rozhraní .NET 4.5 k zamezení blokování volání](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).

## <a name="create-department-controller"></a>Vytvořit kontroler oddělení

Vytvoření řadiče oddělení stejným způsobem jako u předchozích řadičů, s výjimkou tohoto času zaškrtněte políčko **použít asynchronní akce kontroleru** .

Následující zajímavá místa ukazují, co bylo přidáno do synchronního kódu pro metodu `Index` pro zajištění asynchronního:

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

Byly provedeny čtyři změny, aby bylo možné Entity Framework dotaz databáze spustit asynchronně:

- Metoda je označena pomocí klíčového slova `async`, která dává kompilátoru pokyn ke generování zpětných volání pro části těla metody a k automatickému vytvoření vráceného objektu `Task<ActionResult>`.
- Návratový typ se změnil z `ActionResult` na `Task<ActionResult>`. Typ `Task<T>` představuje průběžnou práci s výsledkem typu `T`.
- Klíčové slovo `await` bylo použito pro volání webové služby. Když kompilátor uvidí toto klíčové slovo, pak na pozadí rozdělí metodu do dvou částí. První část končí operací, která se spouští asynchronně. Druhá část je vložena do metody zpětného volání, která je volána po dokončení operace.
- Byla volána asynchronní verze metody rozšíření `ToList`.

Proč se příkaz `departments.ToList` změnil, ale ne příkaz `departments = db.Departments`? Důvodem je, že se spustí asynchronně pouze příkazy, které způsobují odeslání dotazů nebo příkazů do databáze. Příkaz `departments = db.Departments` nastaví dotaz, ale dotaz není proveden, dokud není volána metoda `ToList`. Proto je provedena asynchronně pouze metoda `ToList`.

V metodě `Details` a metodách `Edit` `HttpGet` a `Delete` je metoda `Find` ta, která způsobí odeslání dotazu do databáze, takže se jedná o metodu, která se provede asynchronně:

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

V metodách `Create`, `HttpPost Edit`a `DeleteConfirmed` je to volání metody `SaveChanges`, které způsobuje provedení příkazu, nikoli příkazy, jako je například `db.Departments.Add(department)`, které způsobují úpravu pouze entit v paměti.

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

Otevřete *Views\Department\Index.cshtml*a nahraďte kód šablony následujícím kódem:

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

Tento kód změní název z indexu na oddělení, přesune jméno správce napravo a poskytne celé jméno správce.

V zobrazeních vytvořit, odstranit, podrobnosti a upravit změňte Titulek pole `InstructorID` na "správce" stejným způsobem, jako jste změnili pole název oddělení na "oddělení" v zobrazení kurzu.

V zobrazeních vytvořit a upravit použijte následující kód:

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

V zobrazeních odstranění a podrobnosti použijte následující kód:

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

Spusťte aplikaci a klikněte na kartu **oddělení** .

Vše funguje stejně jako v ostatních řadičích, ale v tomto kontroleru jsou všechny dotazy SQL spouštěny asynchronně.

Některé věci, které je potřeba znát při použití asynchronního programování s Entity Framework:

- Asynchronní kód není bezpečný pro přístup z více vláken. Jinými slovy, jinými slovy, nepokoušejte se souběžně provádět více operací pomocí stejné instance kontextu.
- Chcete-li využít výhod výkonu asynchronního kódu, zajistěte, aby všechny balíčky knihovny, které používáte (například pro stránkování), používaly také Async, pokud volají jakékoli Entity Framework metody, které způsobují odesílání dotazů do databáze.

## <a name="use-stored-procedures"></a>Použití uložených procedur

Někteří vývojáři a specializující upřednostňují použití uložených procedur pro přístup k databázi. V dřívějších verzích Entity Framework můžete načíst data pomocí uložené procedury spuštěním [nezpracovaného dotazu SQL](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), ale nemůžete dát pokyn EF k použití uložených procedur pro operace aktualizace. V EF 6 je snadné nakonfigurovat Code First pro použití uložených procedur.

1. Do *DAL\SchoolContext.cs*přidejte zvýrazněný kód do metody `OnModelCreating`.

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    Tento kód instruuje Entity Framework pro použití uložených procedur pro operace vložení, aktualizace a odstranění v entitě `Department`.
2. V konzole pro správu balíčků zadejte následující příkaz:

    `add-migration DepartmentSP`

    Otevřete *migrace\\&lt;časové razítko&gt;\_DepartmentSP.cs* a zobrazte kód v metodě `Up`, která vytvoří uložené procedury INSERT, Update a Delete:

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. V konzole pro správu balíčků zadejte následující příkaz:

     `update-database`
4. Spusťte aplikaci v režimu ladění, klikněte na kartu **oddělení** a pak klikněte na **vytvořit novou**.
5. Zadejte data nového oddělení a pak klikněte na **vytvořit**.

6. V aplikaci Visual Studio se podívejte na protokoly v okně **výstup** , abyste viděli, že se k vložení nového řádku oddělení použila uložená procedura.

     ![Vložení oddělení SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Code First vytvoří výchozí názvy uložených procedur. Pokud používáte existující databázi, může být nutné přizpůsobit názvy uložených procedur, aby bylo možné použít uložené procedury, které jsou již v databázi definovány. Další informace o tom, jak to provést, najdete v tématu [Entity Framework Code First vkládání, aktualizace a odstraňování uložených procedur](https://msdn.microsoft.com/data/dn468673).

Chcete-li upravit, které generované uložené procedury mají, můžete upravit generovaný kód pro migraci `Up` metodu, která vytvoří uloženou proceduru. To znamená, že se vaše změny projeví při spuštění migrace a budou se používat v provozní databázi, když se migrace po nasazení spustí automaticky v produkčním prostředí.

Pokud chcete změnit existující uloženou proceduru, která byla vytvořena v předchozí migraci, můžete k vygenerování prázdné migrace použít příkaz Add-Migration a pak ručně napsat kód, který volá metodu [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) .

## <a name="deploy-to-azure"></a>Nasazení do Azure

Tato část vyžaduje, abyste v kurzu [migrace a nasazení](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) této série dokončili oddíl volitelné **nasazení aplikace do Azure** . Pokud jste převedli chyby, které jste vyřešili odstraněním databáze v místním projektu, přeskočte tuto část.

1. V aplikaci Visual Studio klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a v místní nabídce vyberte **publikovat** .
2. Klikněte na **Publikovat**.

    Visual Studio nasadí aplikaci do Azure a aplikace se otevře ve výchozím prohlížeči spuštěném v Azure.
3. Otestujte aplikaci, abyste ověřili, že funguje.

    Při prvním spuštění stránky, která přistupuje k databázi, Entity Framework spustí všechny migrace `Up` metody potřebné k zajištění aktuálnosti databáze s aktuálním datovým modelem. Nyní můžete použít všechny webové stránky, které jste přidali od posledního nasazení, včetně stránek oddělení, které jste přidali v tomto kurzu.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Seznámili jste se o asynchronním kódu
> * Vytvořil se kontroler oddělení.
> * Použité uložené procedury
> * Nasazené do Azure

V dalším článku se dozvíte, jak řešit konflikty, když více uživatelů aktualizuje stejnou entitu současně.
> [!div class="nextstepaction"]
> [Zpracování souběžnosti](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
