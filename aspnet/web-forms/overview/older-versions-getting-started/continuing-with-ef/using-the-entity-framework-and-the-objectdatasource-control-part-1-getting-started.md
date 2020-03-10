---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 'Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 1: Začínáme | Microsoft Docs'
author: tdykstra
description: Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená Začínáme pomocí řady Entity Framework kurzů. Pokud jo...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2f14707eb058d438495dd2bc4c17b976c471fc97
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547290"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>Použití Entity Framework 4,0 a ovládacího prvku ObjectDataSource, část 1: Začínáme

tím, že [Dykstra](https://github.com/tdykstra)

> Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená [Začínáme pomocí řady kurzů Entity Framework 4,0](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) . Pokud jste nedokončili předchozí kurzy, jako výchozí bod tohoto kurzu si můžete aplikaci, kterou jste vytvořili, [Stáhnout](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Můžete si také [Stáhnout aplikaci](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , která je vytvořená úplnou řadou kurzů.
> 
> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Ukázková aplikace je web pro fiktivní univerzitě společnosti Contoso. Zahrnuje funkce, jako student přijetí, kurz vytvoření a přiřazení instruktorem.
> 
> V tomto kurzu se zobrazí C#příklady v. [Ukázka ke stažení](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) obsahuje kód v obou C# i Visual Basic.
> 
> ## <a name="database-first"></a>Database First
> 
> Existují tři způsoby, jak můžete pracovat s daty v Entity Framework: *Database First*, *model First*a *Code First*. Tento kurz je určen pro Database First. Informace o rozdílech mezi těmito pracovními postupy a pokyny pro výběr nejvhodnějšího řešení pro váš scénář najdete v tématu [Entity Framework vývojové pracovní postupy](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="web-forms"></a>Webové formuláře
> 
> Podobně jako u Začínáme řady používá tento kurz model webových formulářů ASP.NET a předpokládá, že víte, jak pracovat s webovými formuláři ASP.NET v sadě Visual Studio. Pokud to neuděláte, přečtěte si téma [Začínáme s webovými formuláři ASP.NET 4,5](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Pokud dáváte přednost práci s architekturou ASP.NET MVC, přečtěte si téma [Začínáme s Entity Framework pomocí ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).
> 
> ## <a name="software-versions"></a>Verze softwaru
> 
> | **Zobrazuje se v tomto kurzu.** | **Funguje taky s** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web. Kurz nebyl testován s novějšími verzemi sady Visual Studio. Výběry nabídek, dialogová okna a šablony obsahují mnoho rozdílů. |
> | .NET 4 | .NET 4,5 je zpětně kompatibilní s .NET 4, ale kurz nebyl testován pomocí .NET 4,5. |
> | Entity Framework 4 | Kurz nebyl testován s novějšími verzemi Entity Framework. Počínaje Entity Framework 5, EF používá ve výchozím nastavení `DbContext API` zavedené pomocí EF 4,1. Ovládací prvek EntityDataSource byl navržený tak, aby používal rozhraní `ObjectContext` API. Informace o tom, jak používat ovládací prvek EntityDataSource s rozhraním `DbContext` API, najdete v [tomto blogovém příspěvku](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx). |
> 
> ## <a name="questions"></a>Otázky
> 
> Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra ASP.NET Entity Framework](https://forums.asp.net/1227.aspx), [Entity Framework a LINQ to Entities fóra](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)nebo [StackOverflow.com](http://stackoverflow.com/).

Ovládací prvek `EntityDataSource` umožňuje vytvořit aplikaci velmi rychle, ale obvykle vyžaduje, abyste zachovali významnou velikost obchodní logiky a logiky přístupu k datům na stránkách *aspx* . Pokud očekáváte, že vaše aplikace bude v složitosti složitá a bude vyžadovat trvalou údržbu, můžete ještě víc zvýšit dobu vývoje, abyste mohli vytvořit *n-vrstvou* nebo *vrstvenou* strukturu aplikace, kterou je víc udržovatelnější. Pro implementaci této architektury oddělíte prezentační vrstvu od vrstvy obchodní logiky (knihoven BLL) a vrstvy přístupu k datům (DAL). Jedním ze způsobů implementace této struktury je použití ovládacího prvku `ObjectDataSource` místo ovládacího prvku `EntityDataSource`. Při použití ovládacího prvku `ObjectDataSource` implementujete vlastní kód pro přístup k datům a potom jej vyvoláte na stránkách *aspx* pomocí ovládacího prvku, který má mnoho stejných funkcí jako jiné ovládací prvky zdroje dat. To vám umožní kombinovat výhody n-vrstvého přístupu s výhodami použití ovládacího prvku webové formuláře pro přístup k datům.

Ovládací prvek `ObjectDataSource` poskytuje větší flexibilitu i jiným způsobem. Vzhledem k tomu, že píšete vlastní kód pro přístup k datům, je snazší provádět více než jen číst, vkládat, aktualizovat nebo odstraňovat konkrétní typ entity, což jsou úkoly, které je navržený `EntityDataSource` ovládací prvek. Můžete například provést protokolování při každé aktualizaci entity, archivovat data při každém odstranění entity nebo automaticky kontrolovat a aktualizovat související data při vložení řádku s hodnotou cizího klíče.

## <a name="business-logic-and-repository-classes"></a>Obchodní logika a třídy úložiště

Ovládací prvek `ObjectDataSource` funguje vyvoláním třídy, kterou vytvoříte. Třída obsahuje metody, které načítají a aktualizují data, a poskytuje názvy těchto metod ovládacímu prvku `ObjectDataSource` v kódu. Při vykreslování nebo zpracování zpětného odeslání `ObjectDataSource` volá metody, které jste zadali.

Kromě základních operací CRUD může třída, kterou vytvoříte pro použití s ovládacím prvkem `ObjectDataSource`, potřebovat spustit obchodní logiku, když `ObjectDataSource` čte nebo aktualizuje data. Když například aktualizujete oddělení, možná budete muset ověřit, že žádní jiná oddělení nemají stejného správce, protože jedna osoba nemůže být správcem více než jednoho oddělení.

V některé dokumentaci `ObjectDataSource`, jako je například [Přehled třídy ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx), ovládací prvek volá třídu, která je označována jako *obchodní objekt* , který obsahuje obchodní logiku a logiku přístupu k datům. V tomto kurzu vytvoříte samostatné třídy pro obchodní logiku a datovou logiku pro přístup k datům. Třída, která zapouzdřuje logiku přístupu k datům, se nazývá *úložiště*. Třída obchodní logiky zahrnuje metody obchodní logiky i metody přístupu k datům, ale metody přístupu k datům volají úložiště k provádění úloh přístupu k datům.

Vytvoříte také abstrakci vrstvy mezi knihoven BLL a DAL, která usnadňuje automatizované testování částí knihoven BLL. Tato abstraktní vrstva je implementována vytvořením rozhraní a použitím rozhraní při vytváření instance úložiště ve třídě Business-Logic. Díky tomu je možné poskytnout třídu Business-Logic s odkazem na libovolný objekt, který implementuje rozhraní úložiště. Pro běžný provoz zadáte objekt úložiště, který pracuje s Entity Framework. Pro účely testování poskytnete objekt úložiště, který pracuje s daty uloženými způsobem, který lze snadno manipulovat, například proměnné třídy definované jako kolekce.

Následující ilustrace znázorňuje rozdíl mezi třídou obchodní logiky, která zahrnuje logiku přístupu k datům bez úložiště a jednoho, který používá úložiště.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

Začnete vytvořením webových stránek, ve kterých je ovládací prvek `ObjectDataSource` vázaný přímo na úložiště, protože provádí pouze základní úlohy přístupu k datům. V dalším kurzu vytvoříte třídu obchodní logiky s logikou ověřování a navážete ovládací prvek `ObjectDataSource` na tuto třídu místo na třídu úložiště. Budete také vytvářet testy jednotek pro logiku ověřování. V třetím kurzu v této sérii přidáte funkce řazení a filtrování do aplikace.

Stránky, které v tomto kurzu vytvoříte, pracují s `Departments` sadou entit datového modelu, kterou jste vytvořili v [Začínáme řadě kurzů](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>Aktualizace databáze a datového modelu

Tento kurz začnete tím, že v databázi provedete dvě změny, které vyžadují odpovídající změny v datovém modelu, který jste vytvořili v [Začínáme pomocí výukových kurzů Entity Framework a webových formulářů](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) . V jednom z těchto kurzů jste ručně provedli změny v návrháři, aby se datový model synchronizoval s databází po změně databáze. V tomto kurzu použijete **model aktualizace návrháře z databázového** nástroje k automatické aktualizaci datového modelu.

### <a name="adding-a-relationship-to-the-database"></a>Přidání vztahu k databázi

V sadě Visual Studio otevřete webovou aplikaci Contoso University, kterou jste vytvořili v [Začínáme, pomocí řady kurzů Entity Framework a webové formuláře](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) a pak otevřete databázové diagramy `SchoolDiagram`.

Pokud se podíváte na `Department` tabulku v databázovém diagramu, uvidíte, že má sloupec `Administrator`. Tento sloupec je cizí klíč k tabulce `Person`, ale v databázi není definovaná žádná relace cizího klíče. Je nutné vytvořit relaci a aktualizovat datový model tak, aby Entity Framework mohl tento vztah automaticky zpracovat.

V databázovém diagramu klikněte pravým tlačítkem na tabulku `Department` a vyberte možnost **relace**.

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

V poli **relace cizího klíče** klikněte na **Přidat**a potom klikněte na tři tečky pro **specifikace tabulek a sloupců**.

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

V dialogovém okně **tabulky a sloupce** nastavte tabulku primárních klíčů a pole tak, aby `Person` a `PersonID`, a nastavte tabulku a pole cizího klíče na `Department` a `Administrator`. (Když to uděláte, název vztahu se změní z `FK_Department_Department` na `FK_Department_Person`.)

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

Klikněte na **OK** v poli **tabulky a sloupce** , v poli **relace cizího klíče** klikněte na **Zavřít** a změny uložte. Pokud se zobrazí dotaz, zda chcete uložit `Person` a `Department` tabulky, klikněte na tlačítko **Ano**.

> [!NOTE]
> Pokud jste odstranili `Person` řádky, které odpovídají datům, která jsou již ve sloupci `Administrator`, nebudete moci tuto změnu uložit. V takovém případě použijte Editor tabulek v **Průzkumník serveru** k ujištění, že hodnota `Administrator` v každém `Department` řádku obsahuje ID záznamu, který ve skutečnosti existuje v tabulce `Person`.
> 
> Po uložení změny nebudete moci odstranit řádek z `Person` tabulky, pokud je tato osoba správcem oddělení. V produkční aplikaci byste zadali konkrétní chybovou zprávu, když omezení databáze brání odstranění, nebo byste zadali kaskádové odstranění. Příklad způsobu určení kaskádového odstranění naleznete v [části Entity Framework a ASP.NET – Začínáme část 2](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md).

### <a name="adding-a-view-to-the-database"></a>Přidání zobrazení do databáze

Na stránce Nová *oddělení. aspx* , kterou budete vytvářet, chcete zadat rozevírací seznam instruktorů s názvy ve formátu "poslední, první", aby uživatelé mohli vybrat správce oddělení. Abyste to usnadnili, vytvoříte zobrazení v databázi. Zobrazení bude obsahovat pouze data potřebná v rozevíracím seznamu: úplný název (správně formátovaný) a klíč záznamu.

V **Průzkumník serveru**rozbalte *School. mdf*, klikněte pravým tlačítkem na složku **zobrazení** a vyberte **Přidat nové zobrazení**.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

Po zobrazení dialogového okna **Přidat tabulku** klikněte na **Zavřít** a vložte následující příkaz SQL do podokna SQL:

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

Uložte zobrazení jako `vInstructorName`.

### <a name="updating-the-data-model"></a>Aktualizace datového modelu

Ve složce *dal* otevřete soubor *SchoolModel. edmx* , klikněte pravým tlačítkem myši na plochu návrhu a vyberte **aktualizovat model z databáze**.

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

V dialogovém okně **Zvolte objekty databáze** vyberte kartu **Přidat** a vyberte zobrazení, které jste právě vytvořili.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

Klikněte na **Finish** (Dokončit).

V Návrháři vidíte, že nástroj vytvořil `vInstructorName` entitu a nové přidružení mezi entitami `Department` a `Person`.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> Ve **výstupu** a **Seznam chyb** Windows se může zobrazit zpráva upozorňující na to, že nástroj automaticky vytvořil primární klíč pro nové zobrazení `vInstructorName`. Toto je očekávané chování.

Když odkazujete na novou entitu `vInstructorName` v kódu, nechcete použít konvenci databáze pro předponu s malým písmenem "v". Proto přejmenujete entitu a sadu entit v modelu.

Otevřete **prohlížeč modelů**. V seznamu se zobrazí `vInstructorName` jako typ entity a zobrazení.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

V části **SchoolModel** (ne **SchoolModel. Store**) klikněte pravým tlačítkem myši na **vInstructorName** a vyberte **vlastnosti**. V okně **vlastnosti** změňte vlastnost název na **název** "Instructor" a změňte vlastnost **název sady entit** na hodnotu "InstructorNames".

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

Uložte a zavřete datový model a pak znovu sestavte projekt.

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>Použití třídy úložiště a ovládacího prvku ObjectDataSource

Ve složce *dal* vytvořte nový soubor třídy, pojmenujte ho *SchoolRepository.cs*a stávající kód nahraďte následujícím kódem:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

Tento kód poskytuje jednu `GetDepartments` metodu, která vrátí všechny entity v sadě entit `Departments`. Vzhledem k tomu, že víte, že budete mít přístup k vlastnosti navigace `Person` pro každý vrácený řádek, zadáte načtení Eager pro tuto vlastnost pomocí metody `Include`. Třída také implementuje rozhraní `IDisposable`, aby bylo zajištěno, že se připojení k databázi uvolní při uvolnění objektu.

> [!NOTE]
> Běžným postupem je vytvoření třídy úložiště pro každý typ entity. V tomto kurzu se používá jedna třída úložiště pro několik typů entit. Další informace o vzoru úložiště najdete v příspěvkůch na blogu [týmu týmu Entity Framework](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) a na [blogu Julie Lerman](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/).

Metoda `GetDepartments` vrátí objekt `IEnumerable` namísto objektu `IQueryable`, aby bylo zajištěno, že vrácená kolekce bude použitelná i po vyřazení samotného objektu úložiště. Objekt `IQueryable` může způsobit přístup k databázi vždy, když se k němu přistupuje, ale objekt úložiště může být uvolněný časem, kdy se ovládací prvek datové vazby pokusí data vykreslit. Místo objektu `IEnumerable` můžete vrátit jiný typ kolekce, například objekt `IList`. Vrácení objektu `IEnumerable` však zajistí, že můžete provádět typické úlohy zpracování seznamu jen pro čtení, například `foreach` smyčky a dotazy LINQ, ale nemůžete přidávat nebo odebírat položky v kolekci, což by mohlo znamenat, že by tyto změny byly trvale uložené v databázi.

Vytvořte stránku *oddělení. aspx* , která používá hlavní stránku *Web. Master* , a přidejte následující kód do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

Tento kód vytvoří ovládací prvek `ObjectDataSource`, který používá třídu úložiště, kterou jste právě vytvořili, a ovládací prvek `GridView` k zobrazení dat. Ovládací prvek `GridView` Určuje příkazy pro **Úpravy** a **odstranění** , ale ještě jste nepřidali kód pro jejich podporu.

Několik sloupců používá `DynamicField` ovládacích prvků, aby bylo možné využívat funkce automatického formátování a ověřování dat. Aby fungovaly, budete muset volat metodu `EnableDynamicData` v obslužné rutině události `Page_Init`. (`DynamicControl` ovládací prvky nejsou použity v poli `Administrator`, protože nefungují s navigačními vlastnostmi.)

Atributy `Vertical-Align="Top"` budou důležité později při přidání sloupce, který má vnořený ovládací prvek `GridView` do mřížky.

Otevřete soubor *departments.aspx.cs* a přidejte následující příkaz `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

Pak přidejte následující obslužnou rutinu pro událost `Init` stránky:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

Ve složce *dal* vytvořte nový soubor třídy s názvem *Department.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

Tento kód přidá metadata do datového modelu. Určuje, že vlastnost `Budget` entity `Department` ve skutečnosti představuje měnu, i když je její datový typ `Decimal`, a určuje, že hodnota musí být mezi 0 a $1 000 000,00. Určuje také, že vlastnost `StartDate` má být formátována jako datum ve formátu mm/dd/rrrr.

Spusťte stránku *oddělení. aspx* .

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

Všimněte si, že i když jste nezadali formátovací řetězec do značky stránky *. aspx* pro sloupce **rozpočtového** **data nebo datum zahájení** , použily se pro ně výchozí měna a formátování data pomocí ovládacích prvků `DynamicField` s použitím metadat, která jste zadali v souboru *Department.cs* .

## <a name="adding-insert-and-delete-functionality"></a>Přidávání funkcí INSERT a DELETE

Otevřete *SchoolRepository.cs*a přidejte následující kód, aby bylo možné vytvořit metodu `Insert` a metodu `Delete`. Kód také obsahuje metodu s názvem `GenerateDepartmentID`, která vypočítá další dostupnou hodnotu klíče záznamu pro použití metodou `Insert`. K tomu je potřeba, protože databáze není nakonfigurovaná tak, aby se automaticky počítala s `Department` tabulkou.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Metoda Attach

Metoda `DeleteDepartment` volá metodu `Attach`, aby bylo možné znovu vytvořit odkaz, který je udržován ve Správci stavu objektů objektu Context mezi entitou v paměti a řádkem databáze, kterou představuje. K tomuto musí dojít před voláním metody `SaveChanges`.

Pojem *kontext objektu* odkazuje na třídu Entity Framework, která je odvozena od `ObjectContext` třídy, kterou používáte pro přístup k sadám entit a entitám. V kódu pro tento projekt je třída pojmenována `SchoolEntities`a instance je vždy pojmenována `context`. *Správce stavu objektu* kontextu objektu je třída, která je odvozena od třídy `ObjectStateManager`. Kontakt objektu používá správce stavu objektu k ukládání objektů entit a k udržení přehledu o tom, zda je každá z nich synchronizována s odpovídajícím řádkem nebo řádky tabulky v databázi.

Při čtení entity je kontext objektu uložen ve Správci stavu objektu a udržuje přehled o tom, zda je reprezentace objektu synchronizována s databází. Například pokud změníte hodnotu vlastnosti, příznak je nastaven tak, aby označoval, že vlastnost, kterou jste změnili, již není synchronizována s databází. Poté při volání metody `SaveChanges` ví kontext objektu, co dělat v databázi, protože správce stavu objektu ví přesně, co se liší od aktuálního stavu entity a stavu databáze.

Nicméně tento proces obvykle nefunguje ve webové aplikaci, protože instance kontextu objektu, který čte entitu, spolu s vše ve Správci stavu objektu, je po vykreslení stránky uvolněna. Instance kontextu objektu, která musí použít změny, je nová instance, která je vytvořena pro zpracování zpětného volání. V případě metody `DeleteDepartment` `ObjectDataSource` ovládací prvek znovu vytvoří původní verzi entity z hodnot ve stavu zobrazení, ale tato nově vytvořená `Department` entita neexistuje ve Správci stavu objektu. Pokud jste pro tuto znovu vytvořenou entitu volali metodu `DeleteObject`, volání by nebylo úspěšné, protože kontext objektu neví, zda je entita synchronizována s databází. Nicméně volání metody `Attach` znovu naváže stejné sledování mezi znovu vytvořenou entitou a hodnotami v databázi, které byly původně provedeny automaticky při čtení entity v dřívější instanci kontextu objektu.

Existují situace, kdy nechcete, aby kontext objektu sledoval entity ve Správci stavu objektu, a můžete nastavit příznaky, abyste zabránili tomu, aby to bylo možné provést. Příklady najdete v dalších kurzech v této sérii.

### <a name="the-savechanges-method"></a>Metoda SaveChanges

Tato jednoduchá třída úložiště znázorňuje základní principy provádění operací CRUD. V tomto příkladu je metoda `SaveChanges` volána ihned po každé aktualizaci. V produkční aplikaci můžete chtít zavolat metodu `SaveChanges` od samostatné metody a poskytnout vám větší kontrolu nad tím, kdy se databáze aktualizuje. (Na konci dalšího kurzu najdete odkaz na dokument White Paper, který se zabývá vzorem pracovní jednotky, který je jedním z přístupů k koordinaci souvisejících aktualizací.) Všimněte si také, že v příkladu metoda `DeleteDepartment` nezahrnuje kód pro zpracování konfliktů souběžnosti; Tento kód se přidá v pozdějším kurzu této série.

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>Načítají se názvy instruktorů k výběru při vložení.

Uživatelé musí být schopni vybrat správce ze seznamu instruktorů v rozevíracím seznamu při vytváření nových oddělení. Proto přidejte následující kód do *SchoolRepository.cs* k vytvoření metody pro načtení seznamu instruktorů pomocí zobrazení, které jste vytvořili dříve:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>Vytvoření stránky pro vkládání oddělení

Vytvořte stránku *DepartmentsAdd. aspx* , která používá stránku *Web. Master* , a přidejte následující kód do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

Tento kód vytvoří dva ovládací prvky `ObjectDataSource`, jeden pro vložení nových entit `Department` a jeden pro načtení názvů instruktorů pro ovládací prvek `DropDownList`, který se používá pro výběr správců oddělení. Značka vytvoří ovládací prvek `DetailsView` pro zadávání nových oddělení a určuje obslužnou rutinu události `ItemInserting` ovládacího prvku, takže můžete nastavit `Administrator` hodnotu cizího klíče. Na konci je ovládací prvek `ValidationSummary` pro zobrazení chybových zpráv.

Otevřete *DepartmentsAdd.aspx.cs* a přidejte následující příkaz `using`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

Přidejte následující proměnnou třídy a metody:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

Metoda `Page_Init` povoluje funkci dynamických dat. Obslužná rutina události `Init` ovládacího prvku `DropDownList` uloží odkaz na ovládací prvek a obslužná rutina události `Inserting` ovládacího prvku `DetailsView` používá tento odkaz k získání hodnoty `PersonID` vybraného instruktora a aktualizaci vlastnosti `Administrator` cizího klíče entity `Department`.

Spusťte stránku, přidejte informace pro nové oddělení a potom klikněte na odkaz **Vložit** .

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

Zadejte hodnoty pro jiné nové oddělení. Do pole **rozpočet** a kartu zadejte číslo větší než 1 000 000,00 do dalšího pole. V poli se zobrazí hvězdička, pokud na ni podržíte ukazatel myši, zobrazí se chybová zpráva, kterou jste zadali v metadatech tohoto pole.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

Klikněte na tlačítko **Vložit**a zobrazí se chybová zpráva zobrazená ovládacím prvkem `ValidationSummary` v dolní části stránky.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

Potom zavřete prohlížeč a otevřete stránku *oddělení. aspx* . Přidejte možnost odstranění do stránky *oddělení. aspx* přidáním atributu `DeleteMethod` k ovládacímu prvku `ObjectDataSource` a atribut `DataKeyNames` pro ovládací prvek `GridView`. Úvodní značky pro tyto ovládací prvky teď budou vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

Spusťte stránku.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

Odstraňte oddělení, které jste přidali při spuštění stránky *DepartmentsAdd. aspx* .

## <a name="adding-update-functionality"></a>Přidání funkce Update

Otevřete *SchoolRepository.cs* a přidejte následující metodu `Update`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

Kliknete-li na tlačítko **aktualizovat** na stránce *oddělení. aspx* , ovládací prvek `ObjectDataSource` vytvoří dvě entity `Department`, které budou předána metodě `UpdateDepartment`. Jeden obsahuje původní hodnoty, které byly uloženy ve stavu zobrazení, a druhý obsahuje nové hodnoty, které byly zadány v ovládacím prvku `GridView`. Kód v metodě `UpdateDepartment` předá entitu `Department`, která má původní hodnoty do metody `Attach`, aby bylo možné navázat sledování mezi entitou a čím se v databázi. Potom kód předá `Department` entitu, která má nové hodnoty metody `ApplyCurrentValues`. Kontext objektu porovnává staré a nové hodnoty. Pokud je nová hodnota odlišná od původní hodnoty, kontext objektu změní hodnotu vlastnosti. Metoda `SaveChanges` pak aktualizuje pouze změněné sloupce v databázi. (Pokud je však funkce Update pro tuto entitu namapována na uloženou proceduru, bude celý řádek aktualizován bez ohledu na to, které sloupce byly změněny.)

Otevřete soubor *departments. aspx* a přidejte následující atributy do ovládacího prvku `DepartmentsObjectDataSource`:

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 To způsobuje, že staré hodnoty budou uloženy ve stavu zobrazení tak, aby je bylo možné porovnat s novými hodnotami v metodě `Update`.
- `OldValuesParameterFormatString="orig{0}"`   
 Tím se ovládací prvek informuje o tom, že název parametru původních hodnot je `origDepartment`.

Značka pro otevírací značku ovládacího prvku `ObjectDataSource` nyní vypadá podobně jako v následujícím příkladu:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

Přidejte atribut `OnRowUpdating="DepartmentsGridView_RowUpdating"` k ovládacímu prvku `GridView`. Použijete ho k nastavení hodnoty vlastnosti `Administrator` na základě řádku, který uživatel vybere v rozevíracím seznamu. Počáteční značka `GridView` nyní vypadá podobně jako v následujícím příkladu:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

Do ovládacího prvku `GridView` přidejte ovládací prvek `EditItemTemplate` pro sloupec `Administrator`, a to hned za ovládací prvek `ItemTemplate` pro tento sloupec:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

Tento ovládací prvek `EditItemTemplate` je podobný ovládacímu prvku `InsertItemTemplate` na stránce *DepartmentsAdd. aspx* . Rozdíl je v tom, že počáteční hodnota ovládacího prvku je nastavena pomocí atributu `SelectedValue`.

Před ovládacím prvkem `GridView` přidejte ovládací prvek `ValidationSummary` stejným způsobem jako na stránce *DepartmentsAdd. aspx* .

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

Otevřete *departments.aspx.cs* a hned po deklaraci částečné třídy přidejte následující kód, který vytvoří soukromé pole pro odkaz na ovládací prvek `DropDownList`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

Pak přidejte obslužné rutiny pro událost `Init` ovládacího prvku `DropDownList` a událost `RowUpdating` ovládacího prvku `GridView`:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

Obslužná rutina události `Init` uloží odkaz na ovládací prvek `DropDownList` v poli třída. Obslužná rutina události `RowUpdating` používá odkaz k získání hodnoty, kterou uživatel zadal, a jeho použití na vlastnost `Administrator` entity `Department`.

Pomocí stránky *DepartmentsAdd. aspx* přidejte nové oddělení, potom spusťte stránku *oddělení. aspx* a klikněte na tlačítko **Upravit** na řádku, který jste přidali.

> [!NOTE]
> Nebudete moct upravit řádky, které jste nepřidali (to znamená, že už jsou v databázi), z důvodu neplatných dat v databázi. Správci pro řádky, které byly vytvořeny v databázi, jsou studenti. Pokud se pokusíte jeden z nich upravit, zobrazí se chybová stránka, která hlásí chybu, například `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`

[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

Pokud zadáte neplatnou hodnotu **rozpočtu** a kliknete na **aktualizovat**, zobrazí se stejná hvězdička a chybová zpráva, kterou jste viděli na stránce *oddělení. aspx* .

Změňte hodnotu pole nebo vyberte jiného správce a klikněte na **aktualizovat**. Tato změna se zobrazí.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

Tím se dokončí Úvod k použití ovládacího prvku `ObjectDataSource` pro základní operace CRUD (vytvoření, čtení, aktualizace, odstranění) s Entity Framework. Vytvořili jste jednoduchou n-vrstvou aplikaci, ale vrstva Business-Logic je stále pevně spojena s vrstvou přístupu k datům, což ztěžuje automatizované testování částí. V následujícím kurzu se dozvíte, jak implementovat vzor úložiště pro usnadnění testování částí.

> [!div class="step-by-step"]
> [Next](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
