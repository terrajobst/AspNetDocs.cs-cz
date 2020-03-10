---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 'Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 2: Přidání vrstvy obchodní logiky a testování částí | Microsoft Docs'
author: tdykstra
description: Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená Začínáme pomocí řady kurzů Entity Framework 4,0. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 24344cc33d7c26d7c408db26c0530ef2c708a7d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546765"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 2: Přidání vrstvy obchodní logiky a testování částí

tím, že [Dykstra](https://github.com/tdykstra)

> Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená [Začínáme pomocí řady kurzů Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) . Pokud jste nedokončili předchozí kurzy, jako výchozí bod tohoto kurzu si můžete aplikaci, kterou jste vytvořili, [Stáhnout](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Můžete si také [Stáhnout aplikaci](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , která je vytvořená úplnou řadou kurzů. Pokud máte dotazy k kurzům, můžete je publikovat na [fórum ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

V předchozím kurzu jste vytvořili n-vrstvou webovou aplikaci pomocí Entity Framework a ovládacího prvku `ObjectDataSource`. V tomto kurzu se dozvíte, jak přidat obchodní logiku při zachování vrstvy knihoven BLL (Business-Logic Layer) a vrstvy přístupu k datům (DAL) odděleně a ukazuje, jak vytvořit automatizované testy jednotek pro knihoven BLL.

V tomto kurzu provedete následující úlohy:

- Vytvořte rozhraní úložiště, které deklaruje metody přístupu k datům, které potřebujete.
- Implementujte rozhraní úložiště ve třídě úložiště.
- Vytvořte třídu obchodní logiky, která volá třídu úložiště pro provádění funkcí přístupu k datům.
- Připojte ovládací prvek `ObjectDataSource` k třídě Business-Logic místo do třídy úložiště.
- Vytvořte projekt jednotky a testování a třídu úložiště, která pro své úložiště dat používá kolekce v paměti.
- Vytvořte test jednotek pro obchodní logiku, který chcete přidat do třídy obchodní logiky, a potom spusťte test a podívejte se, že se nedaří.
- Implementujte obchodní logiku do třídy Business-Logic a pak znovu spusťte test jednotky a podívejte se, jak je úspěch.

Budete pracovat se stránkami *oddělení. aspx* a *DepartmentsAdd. aspx* , které jste vytvořili v předchozím kurzu.

## <a name="creating-a-repository-interface"></a>Vytvoření rozhraní úložiště

Začnete vytvořením rozhraní úložiště.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

Ve složce *dal* vytvořte nový soubor třídy, pojmenujte ho *ISchoolRepository.cs*a stávající kód nahraďte následujícím kódem:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

Rozhraní definuje jednu metodu pro každou metodu CRUD (Create, Read, Update, DELETE), kterou jste vytvořili ve třídě úložiště.

Ve třídě `SchoolRepository` v *SchoolRepository.cs*označte, že tato třída implementuje rozhraní `ISchoolRepository`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>Vytvoření třídy Business-Logic

V dalším kroku vytvoříte třídu Business-Logic. Provedete to tak, abyste mohli přidat obchodní logiku, která bude spuštěna ovládacím prvkem `ObjectDataSource`, i když to ještě neuděláte. Nyní bude nová třída Business-Logic provádět pouze stejné operace CRUD jako úložiště.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

Vytvořte novou složku a pojmenujte ji *knihoven BLL*. (V reálné aplikaci by byla vrstva Business-Logic obvykle implementována jako knihovna tříd – samostatný projekt, ale pokud chcete tento kurz uchovávat snadno, třídy knihoven BLL budou uloženy ve složce projektu.)

Ve složce *knihoven BLL* vytvořte nový soubor třídy, pojmenujte ho *SchoolBL.cs*a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

Tento kód vytvoří stejné metody CRUD, jaké jste viděli dříve ve třídě úložiště, ale místo toho, aby přístup k metodám Entity Framework přímo, volá metody třídy úložiště.

Proměnná třídy, která obsahuje odkaz na třídu úložiště, je definována jako typ rozhraní a kód, který vytváří instanci třídy úložiště, je obsažen ve dvou konstruktorech. Konstruktor bez parametrů bude použit ovládacím prvkem `ObjectDataSource`. Vytvoří instanci třídy `SchoolRepository`, kterou jste vytvořili dříve. Druhý konstruktor umožňuje jakýkoli kód, který vytvoří instanci třídy Business-Logic k předání do libovolného objektu, který implementuje rozhraní úložiště.

Metody CRUD, které volají třídu úložiště a dva konstruktory, umožňují použít třídu Business-Logic s libovolným úložištěm back-endové databáze, kterou zvolíte. Třída Business-Logic není nutná vědět, jak třída, kterou volá, přechovává data. (To se často označuje jako *ignorování perzistence*.) To usnadňuje testování částí, protože je možné připojit třídu Business-Logic k implementaci úložiště, která používá něco jednoduchého jako kolekce `List` v paměti pro ukládání dat.

> [!NOTE]
> Technicky jsou objekty entit stále nestálé – ignorují se, protože jsou vytvořeny z tříd, které dědí z `EntityObject` třídy Entity Framework. Pro trvalé ignorování trvalosti můžete použít *prosté staré objekty CLR*nebo *POCOs*namísto objektů, které dědí z třídy `EntityObject`. Používání POCOs překračuje rámec tohoto kurzu. Další informace najdete v tématu [testování a Entity Framework 4,0](https://msdn.microsoft.com/library/ff714955.aspx) na webu MSDN.)

Nyní můžete propojit ovládací prvky `ObjectDataSource` k třídě Business-Logic místo do úložiště a ověřit, že vše funguje stejně jako dříve.

V *odděleních. aspx* a *DepartmentsAdd. aspx*změňte všechny výskyty `TypeName="ContosoUniversity.DAL.SchoolRepository"` na `TypeName="ContosoUniversity.BLL.SchoolBL`". (Všechny jsou ve všech čtyřech instancích.)

Spusťte stránky *oddělení. aspx* a *DepartmentsAdd. aspx* a ověřte, zda stále fungují stejně jako dříve.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>Vytvoření projektu jednotky a testování a implementace úložiště

Přidejte do řešení nový projekt pomocí šablony **testovacího projektu** a pojmenujte ho `ContosoUniversity.Tests`.

V testovacím projektu přidejte odkaz na `System.Data.Entity` a přidejte odkaz na projekt do projektu `ContosoUniversity`.

Nyní můžete vytvořit třídu úložiště, kterou budete používat s testováním částí. Úložiště dat pro toto úložiště bude v rámci třídy.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

V testovacím projektu vytvořte nový soubor třídy, pojmenujte jej *MockSchoolRepository.cs*a stávající kód nahraďte následujícím kódem:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

Tato třída úložiště má stejné metody CRUD jako ta, která přistupuje k Entity Framework přímo, ale spolupracuje s kolekcemi `List` v paměti místo databáze. To usnadňuje, aby testovací třída nastavila a ověřovala testy jednotek pro třídu obchodní logiky.

## <a name="creating-unit-tests"></a>Vytváření testů jednotek

Šablona projektu **testu** vytvořila třídu pro testování jednotek se zástupnými procedurami a vaším dalším úkolem je upravit tuto třídu přidáním metod testování částí do IT pro obchodní logiku, kterou chcete přidat do třídy Business-Logic.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

Ve společnosti Contoso University může být každý jednotlivý instruktor správcem jediného oddělení a Vy musíte přidat obchodní logiku, abyste toto pravidlo vynutili. Začnete tak, že přidáte testy a spustíte testy, abyste je viděli neúspěšná. Pak přidáte kód a znovu spustíte testy, očekává se, že se zobrazí.

Otevřete soubor *UnitTest1.cs* a přidejte `using` příkazy pro obchodní logiku a vrstvy přístupu k datům, které jste vytvořili v projektu ContosoUniversity:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

Metodu `TestMethod1` nahraďte následujícími metodami:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

Metoda `CreateSchoolBL` vytvoří instanci třídy úložiště, kterou jste vytvořili pro projekt testování částí, který pak předá do nové instance třídy Business-Logic. Metoda pak pomocí třídy Business-Logic vloží tři oddělení, která můžete použít v testovacích metodách.

Testovací metody ověřují, zda třída Business-Logic vyvolá výjimku, pokud se někdo pokusí vložit nové oddělení se stejným správcem, jako má stávající oddělení, nebo pokud se někdo pokusí aktualizovat Správce oddělení jeho nastavením na ID osoby. Kdo je již správcem jiného oddělení.

Třídu výjimek jste ještě nevytvořili, takže tento kód se nezkompiluje. Pokud ho chcete zkompilovat, klikněte pravým tlačítkem na `DuplicateAdministratorException` a vyberte **Generovat**a pak **Třída**.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

Tím se vytvoří třída v testovacím projektu, kterou můžete odstranit po vytvoření třídy Exception v hlavním projektu. a implementovali obchodní logiku.

Spusťte projekt testů. Jak bylo očekáváno, testy selžou.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>Přidání obchodní logiky, která provede test Pass

V dalším kroku implementujete obchodní logiku, která znemožňuje nastavit jako správce oddělení někoho, kdo už je správcem jiného oddělení. Vyvoláte výjimku z vrstvy obchodní logiky a pak ji zachytíte do prezentační vrstvy, pokud uživatel upraví oddělení a klikne na tlačítko **aktualizovat** po výběru uživatele, který je již správcem. (Můžete také odebrat instruktory z rozevíracího seznamu, kteří jsou již správci, než stránku vykreslíte, ale účelem tohoto postupu je práce s vrstvou obchodní logiky.)

Začněte tím, že vytvoříte třídu výjimek, kterou vyvoláte, když se uživatel pokusí vytvořit instruktora o více než jednom oddělení. V hlavním projektu vytvořte nový soubor třídy ve složce *knihoven BLL* , pojmenujte ho *DuplicateAdministratorException.cs*a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

Nyní odstraňte dočasný soubor *DuplicateAdministratorException.cs* , který jste předtím vytvořili v testovacím projektu, aby bylo možné kompilovat.

V hlavním projektu otevřete soubor *SchoolBL.cs* a přidejte následující metodu, která obsahuje logiku ověřování. (Kód odkazuje na metodu, kterou vytvoříte později.)

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

Tuto metodu zavoláte při vkládání nebo aktualizaci entit `Department`, abyste zkontrolovali, jestli jiné oddělení už má stejného správce.

Kód volá metodu pro hledání `Department` entitu, která má stejnou hodnotu `Administrator` vlastností jako entita, která je vložena nebo aktualizována. Pokud je jeden nalezen, kód vyvolá výjimku. Pokud vložená nebo aktualizovaná entita neobsahuje žádnou `Administrator` hodnotu, není vyžadována žádná kontrola ověřování, a pokud je metoda volána během aktualizace, není vyvolána žádná výjimka, a `Department` nalezenou entitou `Department`, která je v aktualizované entitě shodná.

Zavolejte novou metodu z `Insert` a `Update`ch metod:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

Do *ISchoolRepository.cs*přidejte následující deklaraci pro novou metodu přístupu k datům:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

Do *SchoolRepository.cs*přidejte následující příkaz `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

Do *SchoolRepository.cs*přidejte následující novou metodu přístupu k datům:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

Tento kód načte `Department` entity, které mají zadaného správce. Mělo by být nalezeno pouze jedno oddělení (pokud existuje). Vzhledem k tomu, že do databáze není integrováno žádné omezení, je návratový typ kolekce v případě, že je nalezeno více oddělení.

Ve výchozím nastavení, když kontext objektu načítá entity z databáze, uchovává jejich sledování ve Správci stavu objektu. Parametr `MergeOption.NoTracking` určuje, že toto sledování nebude pro tento dotaz provedeno. To je nezbytné, protože dotaz může vracet přesně entitu, kterou se pokoušíte aktualizovat, a pak tuto entitu nemůžete připojit. Pokud například upravíte oddělení historie na stránce *oddělení. aspx* a necháte správce beze změny, bude tento dotaz vracet oddělení historie. Pokud není nastavena `NoTracking`, kontext objektu již má entitu oddělení historie ve Správci stavu objektu. Poté, co připojíte entitu historie oddělení, která je znovu vytvořena ze stavu zobrazení, vyvolá kontext objektu výjimku, která říká `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`.

(Jako alternativu k určení `MergeOption.NoTracking`můžete vytvořit nový kontext objektu pouze pro tento dotaz. Vzhledem k tomu, že by měl kontext nového objektu svůj vlastní Správce stavu objektu, by při volání metody `Attach` nedocházelo k žádnému konfliktu. Kontext nového objektu by sdílel metadata a připojení k databázi s původním kontextem objektu, takže snížení výkonu tohoto alternativního přístupu bude minimální. Zde uvedený postup však zavádí možnost `NoTracking`, kterou najdete v jiných kontextech, které jsou užitečné. Možnost `NoTracking` je podrobněji popsána v pozdějším kurzu této série.)

V testovacím projektu přidejte novou metodu přístupu k datům do *MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

Tento kód používá LINQ k provedení stejného výběru dat, který `ContosoUniversity` úložiště projektu používá LINQ to Entities pro.

Spusťte test projektu znovu. Tentokrát testy proběhnou.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>Zpracování výjimek ObjectDataSource

V projektu `ContosoUniversity` spusťte stránku *oddělení. aspx* a zkuste změnit správce oddělení na někoho, kdo už je správcem pro jiné oddělení. (Mějte na paměti, že můžete upravovat jenom oddělení, která jste přidali během tohoto kurzu, protože se databáze nachází předem s neplatnými daty.) Zobrazí se následující chybová stránka serveru:

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

Nechcete, aby uživatelé viděli tento druh chybové stránky, takže potřebujete přidat kód pro zpracování chyb. Otevřete panel *oddělení. aspx* a určete obslužnou rutinu pro událost `OnUpdated` `DepartmentsObjectDataSource`. Počáteční značka `ObjectDataSource` nyní vypadá podobně jako v následujícím příkladu.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

Do *departments.aspx.cs*přidejte následující příkaz `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

Přidejte následující obslužnou rutinu pro událost `Updated`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

Pokud ovládací prvek `ObjectDataSource` zachytí výjimku při pokusu o provedení aktualizace, předá výjimku v argumentu události (`e`) do této obslužné rutiny. Kód v obslužné rutině kontroluje, zda je výjimkou duplicitní výjimka správce. Pokud je, kód vytvoří ovládací prvek validátor, který obsahuje chybovou zprávu pro zobrazení ovládacího prvku `ValidationSummary`.

Spusťte stránku a pokuste se znovu nastavit někoho jako správce dvou oddělení. Tentokrát `ValidationSummary` ovládací prvek zobrazuje chybovou zprávu.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

Udělejte podobné změny na stránce *DepartmentsAdd. aspx* . V *DepartmentsAdd. aspx*zadejte obslužnou rutinu pro událost `OnInserted` `DepartmentsObjectDataSource`. Výsledný kód bude vypadat podobně jako v následujícím příkladu.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

Do *DepartmentsAdd.aspx.cs*přidejte stejný příkaz `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

Přidejte následující obslužnou rutinu události:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

Teď můžete otestovat stránku *DepartmentsAdd.aspx.cs* a ověřit tak, že se také správně zpracovávají pokusy, aby jedna osoba mohla udělat správce více než jednoho oddělení.

Tím se dokončí Úvod do implementace vzoru úložiště pro použití ovládacího prvku `ObjectDataSource` s Entity Framework. Další informace o vzorcích a testování úložiště najdete v tématu testování dokumentů na webu MSDN [a Entity Framework 4,0](https://msdn.microsoft.com/library/ff714955.aspx).

V následujícím kurzu se dozvíte, jak do aplikace přidat funkce řazení a filtrování.

> [!div class="step-by-step"]
> [Předchozí](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [Další](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
