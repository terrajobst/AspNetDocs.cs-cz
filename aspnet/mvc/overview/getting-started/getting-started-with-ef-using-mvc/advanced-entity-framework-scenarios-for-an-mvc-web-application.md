---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 'Kurz: Přečtěte si o rozšířených scénářích EF pro webovou aplikaci MVC 5.'
description: V tomto kurzu se seznámíte s několika tématy, která jsou užitečná, když překročíte základy vývoje webových aplikací ASP.NET, které používají Entity Framework Code First.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2019
ms.locfileid: "58425272"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>Kurz: Přečtěte si o rozšířených scénářích EF pro webovou aplikaci MVC 5.

V předchozím kurzu jste implementovali dědičnost tabulek na hierarchii. V tomto kurzu se seznámíte s několika tématy, která jsou užitečná, když překročíte základy vývoje webových aplikací ASP.NET, které používají Entity Framework Code First. V prvních několika oddílech najdete podrobné pokyny, které vás provedou kódem a pomocí sady Visual Studio k dokončení úkolů, které následují, zavedou několik témat s stručnými úvody, které následují odkazy na zdroje, kde najdete další informace.

U většiny těchto témat budete pracovat se stránkami, které jste již vytvořili. Pokud chcete hromadné aktualizace použít nezpracovaných SQL, vytvoří se nová stránka, která aktualizuje počet kreditů všech kurzů v databázi:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Provádění nezpracovaných dotazů SQL
> * Provádění dotazů bez sledování
> * Kontrola dotazů SQL odeslaných do databáze

Naučíte se také:

> [!div class="checklist"]
> * Vytvoření vrstvy abstrakce
> * Proxy – třídy
> * Automatické zjišťování změn
> * Automatické ověřování
> * Entity Framework nástroje Power Tools
> * Zdrojový kód Entity Framework

## <a name="prerequisite"></a>Předpoklad

* [Implementace dědičnosti](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>Provádění nezpracovaných dotazů SQL

Rozhraní API pro Entity Framework Code First obsahuje metody, které umožňují předat příkazy SQL přímo do databáze. Máte následující možnosti:

- Použijte metodu [negenerickými. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) pro dotazy, které vracejí typy entit. Vrácené objekty musí být typu očekávaného `DbSet` objektem a automaticky sledovány pomocí kontextu databáze, pokud nevypnete sledování. (Další informace o metodě [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) naleznete v následující části.)
- Použijte metodu [Database. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) pro dotazy vracející typy, které nejsou entitami. Vrácená data nejsou sledována kontextem databáze, a to i v případě, že použijete tuto metodu k načtení typů entit.
- Pro příkazy, které nejsou dotazy Query, použijte [Database. ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) .

Jednou z výhod používání Entity Framework je, že se vyhnete tomu, že váš kód je příliš úzce k určité metodě ukládání dat. Provede to tím, že vygeneruje dotazy a příkazy SQL za vás, což vám taky zabrání v jejich psaní. Existují však výjimečné scénáře, pokud potřebujete spustit konkrétní dotazy SQL, které jste vytvořili ručně, a tyto metody umožňují zpracovávat takové výjimky.

Jak je vždy true při provádění příkazů SQL ve webové aplikaci, je nutné podniknout preventivní opatření k ochraně vašeho webu před útoky prostřednictvím injektáže SQL. Jedním ze způsobů, jak to provést, je použít parametrizované dotazy, aby se zajistilo, že řetězce odeslané webovou stránkou nejde interpretovat jako příkazy SQL. V tomto kurzu použijete parametrizované dotazy při integraci vstupu uživatele do dotazu.

### <a name="calling-a-query-that-returns-entities"></a>Volání dotazu, který vrací entity

Třída [negenerickými&lt;TEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx) poskytuje metodu, kterou lze použít ke spuštění dotazu, který vrací entitu typu `TEntity`. Chcete-li zjistit, jak to funguje, změňte kód v `Details` metodě `Department` kontroleru.

V *DepartmentController.cs* `Details` `db.Departments.SqlQuery` v`db.Departments.FindAsync` metodě nahraďte volání metody voláním metody, jak je znázorněno v následujícím zvýrazněném kódu:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

Chcete-li ověřit, zda nový kód funguje správně, vyberte kartu **oddělení** a potom **Podrobnosti** pro jedno z oddělení. Ujistěte se, že se všechna data zobrazují podle očekávání.

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>Volání dotazu, který vrací jiné typy objektů

Dříve jste vytvořili tabulku statistik studentů pro stránku o produktu, která ukázala počet studentů pro každé datum registrace. Kód, který je v *HomeController.cs* , používá LINQ:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

Předpokládejme, že chcete napsat kód, který načte tato data přímo v SQL místo použití LINQ. K tomu je nutné spustit dotaz, který vrací jinou entitu než objekty entity, což znamená, že je nutné použít metodu [Database. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) .

V *HomeController.cs*nahraďte příkaz LINQ v `About` metodě příkazem SQL, jak je znázorněno v následujícím zvýrazněném kódu:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

Spusťte stránku o produktu. Ověřte, že se zobrazí stejná data předtím.

### <a name="calling-an-update-query"></a>Volání aktualizačního dotazu

Předpokládejme, že správci služby contoso University chtějí v databázi provádět hromadné změny, jako je třeba Změna počtu kreditů pro každý kurz. Pokud má univerzita velký počet kurzů, je třeba je neefektivně načíst jako entity a jednotlivě je měnit. V této části implementujete webovou stránku, která uživateli umožní zadat faktor, podle kterého se má změnit počet kreditů pro všechny kurzy, a provedete změnu provedením příkazu SQL `UPDATE` . 

V *CourseController.cs*přidejte `UpdateCourseCredits` metody pro `HttpGet` a `HttpPost`:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

Když kontroler zpracuje `HttpGet` požadavek, nic se nevrátí `ViewBag.RowsAffected` do proměnné a zobrazení zobrazí prázdné textové pole a tlačítko Odeslat.

Po kliknutí `HttpPost` na tlačítko Aktualizovat je metoda volána a `multiplier` má hodnotu zadanou v textovém poli. Kód potom spustí SQL, který aktualizuje kurzy a vrátí počet ovlivněných řádků do zobrazení v `ViewBag.RowsAffected` proměnné. Když zobrazení Získá hodnotu v této proměnné, zobrazuje počet aktualizovaných řádků místo textového pole a tlačítka Odeslat.

V *CourseController.cs*klikněte pravým tlačítkem myši na jednu `UpdateCourseCredits` z metod a pak klikněte na **Přidat zobrazení**. Zobrazí se dialogové okno **Přidat zobrazení** . Ponechte výchozí nastavení a vyberte **Přidat**.

V *Views\Course\UpdateCourseCredits.cshtml*nahraďte kód šablony následujícím kódem:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

Spusťte metodu tak, že vyberete kartu **kurzy** a pak na konec adresy URL v adresním řádku prohlížeče přidáte "/UpdateCourseCredits" (například: `http://localhost:50205/Course/UpdateCourseCredits`). `UpdateCourseCredits` Do textového pole zadejte číslo:

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

Klikněte na tlačítko **aktualizace**. Zobrazí se počet ovlivněných řádků.

Kliknutím na **zpět na seznam** zobrazíte seznam kurzů s revidovaným počtem kreditů.

Další informace o nezpracovaných dotazech SQL najdete v tématu [raw SQL dotazy](https://msdn.microsoft.com/data/jj592907) na webu MSDN.

## <a name="no-tracking-queries"></a>Žádné dotazy pro sledování

Když kontext databáze načte řádky tabulky a vytvoří objekty entit, které je reprezentují, ve výchozím nastavení udržuje přehled o tom, zda jsou entity v paměti synchronizovány s těmi, které jsou v databázi. Data v paměti fungují jako mezipaměť a používají se při aktualizaci entity. Toto ukládání do mezipaměti je často zbytečné v rámci webové aplikace, protože instance kontextu jsou obvykle krátkodobé – neuvolňuje (nové je vytvořeno a odstraněno pro každý požadavek) a kontext, který čte entitu, je obvykle uvolněn předtím, než se entita znovu použije.

Sledování objektů entit v paměti můžete zakázat pomocí metody [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) . Mezi obvyklé scénáře, které byste mohli chtít udělat, patří následující:

- Dotaz načte takový velký objem dat, který vypne sledování, může výrazně zvýšit výkon.
- Chcete připojit entitu, abyste ji mohli aktualizovat, ale dříve jste načetli stejnou entitu pro jiný účel. Vzhledem k tomu, že entita je již sledována kontextem databáze, nelze připojit entitu, kterou chcete změnit. Jedním ze `AsNoTracking` způsobů, jak tuto situaci zvládnout, je použití možnosti s dřívějším dotazem.

Příklad, který ukazuje, jak použít metodu [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) , najdete v [dřívější verzi tohoto kurzu](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md). Tato verze kurzu nenastaví upravený příznak u entity vytvořené pomocí modelu pořadače v metodě Edit, takže to nepotřebuje `AsNoTracking`.

## <a name="examine-sql-sent-to-database"></a>Kontrola odeslání SQL serveru do databáze

Někdy je užitečné, abyste si mohli prohlédnout skutečné dotazy SQL, které se odesílají do databáze. V předchozím kurzu jste zjistili, jak to udělat v kódu pro zachycování. Nyní se zobrazí některé způsoby, jak to provést bez psaní kódu pro zachycování. Pokud to chcete vyzkoušet, podívejte se na jednoduchý dotaz a podívejte se na to, co se děje, když přidáte možnosti, jako je Eager načítání, filtrování a řazení.

V části `Index` *Controllers/CourseController*nahraďte metodu následujícím kódem, aby bylo možné dočasně zastavit načítání Eager:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

Nyní nastavte zarážku na `return` příkaz (F9 se kurzorem na daném řádku). Stisknutím klávesy **F5** spusťte projekt v režimu ladění a vyberte stránku index kurzu. Když kód dosáhne zarážky, prověřte `sql` proměnnou. Zobrazí se dotaz, který se odešle do SQL Server. Jedná se o jednoduchý `Select` příkaz.

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

Kliknutím na Lupa zobrazíte dotaz v **Vizualizér textu**.

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

Nyní přidáte rozevírací seznam na stránku indexu kurzů, aby uživatelé mohli filtrovat konkrétní oddělení. Kurzy seřadíte podle názvu a zadáte Eager načítání pro `Department` navigační vlastnost.

V *CourseController.cs*nahraďte `Index` metodu následujícím kódem:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

Obnovte zarážku na `return` příkazu.

Metoda přijímá vybranou hodnotu rozevíracího seznamu v `SelectedDepartment` parametru. Pokud není nic vybráno, bude mít tento parametr hodnotu null.

Do zobrazení rozevíracího seznamu se předává kolekceobsahujícívšechnaoddělení.`SelectList` Parametry předané `SelectList` konstruktoru určují název pole hodnoty, název textového pole a vybranou položku.

`Get` Pro metodu `Course` úložiště kód určuje výraz filtru, pořadí řazení `Department` a Eager načítání pro navigační vlastnost. Výraz filtru vždy vrátí hodnotu `true` , `SelectedDepartment` Pokud není nic vybráno v rozevíracím seznamu (tj. je null).

V *Views\Course\Index.cshtml*bezprostředně před počáteční `table` značkou přidejte následující kód k vytvoření rozevíracího seznamu a tlačítko Odeslat:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

Pokud se zarážka pořád nastavuje, spusťte stránku index kurzu. Pokračujte v první době, kdy kód narazí na zarážku, aby se stránka zobrazila v prohlížeči. V rozevíracím seznamu vyberte oddělení a klikněte na **Filtr**.

Tentokrát bude první zarážka pro dotaz oddělení v rozevíracím seznamu. Přeskočí tuto `query` proměnnou a zobrazí se, když kód příště dosáhne zarážky, aby se zobrazila informace `Course` o tom, jaký dotaz teď vypadá jako. Uvidíte něco podobného jako následující:

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

Vidíte, že dotaz je `JOIN` nyní dotazem, který načítá `Department` data společně s `Course` daty a obsahuje `WHERE` klauzuli.

`var sql = courses.ToString()` Odeberte řádek.

## <a name="create-an-abstraction-layer"></a>Vytvoření vrstvy abstrakce

Mnoho vývojářů napíše kód, který implementuje úložiště a pracovní postupy jako obálku kolem kódu, který pracuje s Entity Framework. Tyto vzory mají za cíl vytvořit vrstvu abstrakce mezi vrstvou pro přístup k datům a vrstvou obchodní logiky aplikace. Implementace těchto vzorů vám může přispět k izolaci aplikace před změnami v úložišti dat a může usnadnit automatizované testování částí nebo vývoj řízený testováním (TDD). Nicméně psaní dalšího kódu pro implementaci těchto vzorů není vždy nejlepší volbou pro aplikace, které používají EF, z několika důvodů:

- Třída kontextu EF sama neizolací váš kód z kódu specifického pro úložiště dat.
- Třída kontextu EF může fungovat jako jednotka pro práci s aktualizacemi databáze, které používáte pomocí EF.
- Funkce zavedené v Entity Framework 6 usnadňují implementaci TDD bez psaní kódu úložiště.

Další informace o implementaci vzorového úložiště a pracovní jednotky najdete v části [Entity Framework 5 této série kurzů](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md). Informace o způsobech implementace služby TDD v Entity Framework 6 najdete v následujících zdrojích informací:

- [Jak EF6 umožňuje snadnější napodobování DbSets](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [Testování pomocí makety architektury](https://msdn.microsoft.com/data/dn314429)
- [Testování s vlastními dvojitými testy](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>Proxy – třídy

Když Entity Framework vytvoří instance entit (například při spuštění dotazu), často je vytvoří jako instance dynamicky generovaného odvozeného typu, který funguje jako proxy pro entitu. Podívejte se například na následující dva obrázky ladicího programu. V prvním obrázku vidíte, že `student` proměnná je očekávaného `Student` typu hned po vytvoření instance entity. Po použití objektu EF v druhé imagi k načtení entity studenta z databáze se zobrazí Třída proxy.

![Před proxy třídou](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![Po proxy třídě](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

Tato třída proxy Přepisuje některé virtuální vlastnosti entity, aby mohl vkládat háky pro provádění akcí automaticky, když je k ní přistupovaná vlastnost. Jedna funkce, pro kterou se tento mechanismus používá, je opožděné načítání.

Ve většině případů nemusíte znát použití proxy serverů, ale existují výjimky:

- V některých případech můžete chtít zabránit Entity Framework v vytváření instancí proxy serveru. Například při serializaci entit, které obecně požadujete třídy POCO, nikoli proxy třídy. Jedním ze způsobů, jak zabránit problémům s serializací, je serializace objektů přenosu dat (DTO) místo objektů entit, jak je znázorněno v kurzu [použití webového rozhraní API s Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) . Další možností je [zakázat vytvoření proxy serveru](https://msdn.microsoft.com/data/jj592886.aspx).
- Při vytváření instance třídy entity pomocí `new` operátoru nezískáte instanci proxy. To znamená, že nezískáte funkce, jako je opožděné načítání a automatické sledování změn. Obvykle je to v pořádku. obecně nepotřebujete opožděné načítání, protože vytváříte novou entitu, která není v databázi, a obecně nepotřebujete sledování změn, pokud entitu výslovně označíte jako `Added`. Pokud však potřebujete opožděné načítání a potřebujete sledování změn, můžete vytvořit nové instance entit s proxy objekty pomocí metody `DbSet` [Create](https://msdn.microsoft.com/library/gg679504.aspx) třídy.
- Je možné, že budete chtít z typu proxy získat skutečný typ entity. Pomocí metody `ObjectContext` [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) třídy lze získat skutečný typ entity instance typu proxy serveru.

Další informace najdete v tématu [práce se servery proxy](https://msdn.microsoft.com/data/JJ592886.aspx) na webu MSDN.

## <a name="automatic-change-detection"></a>Automatické zjišťování změn

Entity Framework určuje, jak se entita změnila (takže se aktualizace musí odeslat do databáze) porovnáním aktuálních hodnot entity s původními hodnotami. Původní hodnoty se uloží, když je entita dotazována nebo připojena. Některé z metod, které způsobují automatickou detekci změn, jsou následující:

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

Pokud sledujete velký počet entit a v rámci smyčky několikrát voláte jednu z těchto metod, můžete dosáhnout výrazného zlepšení výkonu tím, že se pomocí vlastnosti [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) dočasně vypne funkce automatického zjišťování změn. Další informace najdete v tématu [automatické zjišťování změn](https://msdn.microsoft.com/data/jj556205) na webu MSDN.

## <a name="automatic-validation"></a>Automatické ověřování

Když zavoláte `SaveChanges` metodu, ve výchozím nastavení Entity Framework před aktualizací databáze ověřuje data ve všech vlastnostech všech změněných entit. Pokud jste aktualizovali velký počet entit a již jste ověřili data, je tato práce nepotřebná a je možné, že proces uložení změn trvá méně času tím, že se dočasně vypne ověřování. Můžete to udělat pomocí vlastnosti [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) . Další informace najdete v tématu [ověření](https://msdn.microsoft.com/data/gg193959) na webu MSDN.

## <a name="entity-framework-power-tools"></a>Entity Framework nástroje Power Tools

[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) je doplněk sady Visual Studio, který se používá k vytvoření diagramů datového modelu zobrazených v těchto kurzech. Nástroje mohou také provádět jiné funkce, jako je například generovat třídy entit založené na tabulkách v existující databázi, aby bylo možné použít databázi s Code First. Po instalaci nástrojů se některé další možnosti zobrazí v místních nabídkách. Například když kliknete pravým tlačítkem myši na třídu kontextu v **Průzkumník řešení**, zobrazí se možnost a **Entity Framework** . Díky tomu je možné vygenerovat diagram. Pokud používáte Code First nemůžete změnit datový model v diagramu, ale můžete se pohybovat, abyste snadněji pochopili.

![Diagram EF](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>Zdrojový kód Entity Framework

Zdrojový kód pro Entity Framework 6 je k dispozici na [GitHubu](https://github.com/aspnet/EntityFramework6). Můžete zakódovat chyby a můžete přispět vlastní vylepšení zdrojového kódu EF.

I když je zdrojový kód otevřený, Entity Framework je plně podporovaný jako produkt společnosti Microsoft. Tým Microsoft Entity Framework udržuje kontrolu nad tím, které příspěvky jsou přijaty, a testuje všechny změny kódu, aby se zajistila kvalita jednotlivých verzí.

## <a name="acknowledgments"></a>Potvrzení

- Dykstra napsal původní verzi tohoto kurzu, společně vytvořila aktualizaci EF 5 a napsala aktualizaci EF 6. Je to vedoucí programátor pro programování v týmu obsahu webové platformy a nástrojů Microsoftu.
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) obsahoval většinu práce, které aktualizují kurz pro EF 5 a MVC 4 a společně vytvořil aktualizaci EF 6. Rick je hlavní programovací zapisovač pro zaměření Microsoftu na Azure a MVC.
- [Rowan Miller](http://www.romiller.com) a další členové Entity Framework týmu s asistencí revize kódu a pomohli ladit mnoho problémů s migrací, které vznikly během aktualizace kurzu pro EF 5 a EF 6.

## <a name="troubleshoot-common-errors"></a>Řešení běžných chyb

### <a name="cannot-createshadow-copy"></a>Nelze vytvořit/stínovou kopii

Chybová zpráva:

> Nelze vytvořit nebo stínovou kopii&lt;souboru&gt;filename, pokud tento soubor již existuje.

Řešení

Počkejte několik sekund a aktualizujte stránku.

### <a name="update-database-not-recognized"></a>Aktualizace – databáze nebyla rozpoznána.

Chybová zpráva (z `Update-Database` příkazu v PMC):

> Termín "aktualizace databáze" nebyl rozpoznán jako název rutiny, funkce, souboru skriptu nebo spustitelného programu. Zkontrolujte pravopis názvu, nebo pokud byla vložena cesta, ověřte, zda je cesta správná, a akci opakujte.

Řešení

Ukončete aplikaci Visual Studio. Znovu otevřete projekt a zkuste to znovu.

### <a name="validation-failed"></a>Neúspěšné ověření

Chybová zpráva (z `Update-Database` příkazu v PMC):

> Nepodařilo se ověřit jednu nebo více entit. Další podrobnosti najdete ve vlastnosti ' EntityValidationErrors '.

Řešení

Jednou z příčin tohoto problému jsou chyby ověření při `Seed` spuštění metody. Tipy k ladění `Seed` metody naleznete v tématu [osazení a ladění Entity Framework (EF) databáze](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) .

### <a name="http-50019-error"></a>Chyba HTTP 500,19

Chybová zpráva:

> Chyba protokolu HTTP 500,19 – vnitřní chyba serveru: k požadované stránce nelze přistupovat, protože související konfigurační data stránky jsou neplatná.

Řešení

Jedním ze způsobů, jak získat tuto chybu, je použití více kopií řešení, přičemž každý z nich používá stejné číslo portu. Tento problém můžete obvykle vyřešit ukončením všech instancí aplikace Visual Studio a následným restartováním projektu, na kterém pracujete. Pokud to nepomůže, zkuste změnit číslo portu. Klikněte pravým tlačítkem na soubor projektu a pak klikněte na vlastnosti. Vyberte kartu **Web** a potom změňte číslo portu v textovém poli **Adresa URL projektu** .

### <a name="error-locating-sql-server-instance"></a>Při hledání instance SQL Server došlo k chybě.

Chybová zpráva:

> Při navazování připojení k SQL Server došlo k chybě související se sítí nebo instanci. Server nebyl nalezen nebo k němu nelze získat přístup. Ověřte, zda je název instance správný a zda je SQL Server nakonfigurovaná tak, aby povolovala vzdálená připojení. zprostředkovatele Síťová rozhraní SQL, chyba: 26 – Chyba při hledání zadaného serveru/instance)

Řešení

Ověřte připojovací řetězec. Pokud jste databázi odstranili ručně, změňte název databáze v řetězci konstrukce.

## <a name="get-the-code"></a>Získat kód

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

 Další informace o tom, jak pracovat s daty pomocí Entity Framework, najdete na [stránce dokumentace EF na webech MSDN](https://msdn.microsoft.com/data/ee712907) a ASP.NET, které jsou [doporučeny pro přístup k datům](../../../../whitepapers/aspnet-data-access-content-map.md).

Další informace o tom, jak nasadit webovou aplikaci po sestavení, najdete v tématu [ASP.NET Web Deployment – doporučené prostředky](../../../../whitepapers/aspnet-web-deployment-content-map.md) v knihovně MSDN.

Informace o dalších tématech souvisejících s MVC, jako je ověřování a autorizace, najdete v tématu [ASP.NET (Doporučené zdroje](../recommended-resources-for-mvc.md)informací) MVC.

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Provedené nezpracované dotazy SQL
> * Provedly se žádné dotazy pro sledování.
> * Prověření dotazů SQL odeslaných do databáze

Dozvěděli jste se také o:

> [!div class="checklist"]
> * Vytvoření vrstvy abstrakce
> * Proxy – třídy
> * Automatické zjišťování změn
> * Automatické ověřování
> * Entity Framework nástroje Power Tools
> * Zdrojový kód Entity Framework

Tím se dokončí Tato série kurzů na používání Entity Framework v aplikaci ASP.NET MVC. Pokud se chcete dozvědět o Database First EF, přečtěte si část databáze prvního kurzu.
> [!div class="nextstepaction"]
> [Entity Framework Database First](../database-first-development/setting-up-database.md)