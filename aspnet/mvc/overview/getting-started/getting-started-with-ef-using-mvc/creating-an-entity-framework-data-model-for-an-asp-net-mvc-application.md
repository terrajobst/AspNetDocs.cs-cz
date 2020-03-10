---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 'Kurz: Začínáme s Entity Framework 6 Code First pomocí MVC 5 | Microsoft Docs'
description: V této sérii kurzů se naučíte, jak vytvořit aplikaci ASP.NET MVC 5, která pro přístup k datům používá Entity Framework 6.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616128"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a>Kurz: Začínáme s Entity Framework 6 Code First pomocí MVC 5

> [!NOTE]
> Pro nový vývoj doporučujeme, abyste [ASP.NET Core Razor Pages](/aspnet/core/razor-pages) přes ASP.NET a zobrazení MVC. Řadu kurzů, která se podobá tomuto použití Razor Pages, najdete [v tématu Kurz: Začínáme s Razor Pages v ASP.NET Core](/aspnet/core/tutorials/razor-pages/razor-pages-start). Nový kurz:
> * Je snazší sledovat.
> * Poskytuje další EF Core osvědčených postupů.
> * Používá efektivnější dotazy.
> * Je aktuálnější s nejnovějším rozhraním API.
> * Zahrnuje další funkce.
> * Je upřednostňovaným přístupem k vývoji nových aplikací.

V této sérii kurzů se naučíte, jak vytvořit aplikaci ASP.NET MVC 5, která pro přístup k datům používá Entity Framework 6. V tomto kurzu se používá pracovní postup Code First. Informace o tom, jak zvolit mezi Code First, Database First a Model First, najdete v tématu [Vytvoření modelu](/ef/ef6/modeling/).

V této sérii kurzů se dozvíte, jak sestavit ukázkovou aplikaci Contoso University. Ukázková aplikace je jednoduchý web na univerzitě. Díky tomu můžete zobrazit a aktualizovat informace o studentech, kurzech a instruktorech. Tady jsou dvě obrazovky, které vytvoříte:

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![Upravit studenta](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvoření webové aplikace MVC
> * Nastavit styl lokality
> * Nainstalovat Entity Framework 6
> * Vytvoření datového modelu
> * Vytvoření kontextu databáze
> * Inicializovat databázi s testovacími daty
> * Nastavte pro použití LocalDB EF 6.
> * Vytvořit kontroler a zobrazení
> * Zobrazení databáze

## <a name="prerequisites"></a>Předpoklady

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a>Vytvoření webové aplikace MVC

1. Otevřete Visual Studio a vytvořte C# webový projekt pomocí šablony **webové aplikace ASP.NET (.NET Framework)** . Pojmenujte projekt *ContosoUniversity* a vyberte **OK**.

   ![Dialogové okno Nový projekt v aplikaci Visual Studio](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. V **New ASP.NET Web Application – ContosoUniversity**vyberte **MVC**.

   ![Dialogové okno Nová webová aplikace v aplikaci Visual Studio](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > Ve výchozím nastavení je možnost **ověřování** nastavena na **bez ověřování**. Pro tento kurz webová aplikace nepožaduje, aby se uživatelé přihlásili. Také neomezuje přístup na základě toho, kdo je přihlášený.

1. Vyberte **OK** a vytvořte projekt.

## <a name="set-up-the-site-style"></a>Nastavit styl lokality

V několika jednoduchých změnách se nastaví nabídka web, rozložení a Domovská stránka.

1. Otevřete *Views\Shared\\_Layout. cshtml*a proveďte následující změny:

   - Změňte všechny výskyty "Moje aplikace ASP.NET" a "název aplikace" na "contoso University".
   - Přidejte položky nabídky pro studenty, kurzy, instruktory a oddělení a odstraňte položku kontaktu.

   Změny jsou zvýrazněny v následujícím fragmentu kódu:

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. V *Views\Home\Index.cshtml*nahraďte obsah souboru následujícím kódem, který nahradí text o ASP.NET a MVC textem o této aplikaci:

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. Stisknutím kombinace kláves CTRL + F5 spustíte Web. V hlavní nabídce se zobrazí domovská stránka.

## <a name="install-entity-framework-6"></a>Nainstalovat Entity Framework 6

1. V nabídce **nástroje** zvolte **Správce balíčků NuGet**a pak zvolte **Konzola správce balíčků**.

2. V okně **konzoly Správce balíčků** zadejte následující příkaz:

   ```text
   Install-Package EntityFramework
   ```

Tento krok je jedním z několika kroků, které tento kurz provede ručně, ale to může být provedeno automaticky funkcí generování uživatelského rozhraní ASP.NET MVC. Provádíte je ručně, abyste viděli kroky požadované k použití Entity Framework (EF). Pro vytvoření kontroleru a zobrazení MVC použijete generování uživatelského rozhraní později. Alternativou je umožnit automatické instalaci balíčku NuGet pro EF, vytvoření třídy kontextu databáze a vytvoření připojovacího řetězce. Až to uděláte, stačí, když budete chtít tento krok provést, přeskočte tyto kroky a uživatelské rozhraní vašeho kontroleru MVC po vytvoření tříd entit.

## <a name="create-the-data-model"></a>Vytvoření datového modelu

V dalším kroku vytvoříte třídy entit pro aplikaci Contoso University. Začnete s následujícími třemi entitami:

**Kurz** <-> **registrace** <-> **studenta**

| Entity | Relace |
| -------- | ------------ |
| Kurz k registraci | 1: n |
| Student k registraci | 1: n |

Mezi entitami `Student` a `Enrollment` existuje vztah 1:1 a mezi `Course`mi a `Enrollment` entitami existuje vztah 1: n. Jinými slovy, student může být zaregistrovaný v jakémkoli počtu kurzů a kurz může mít zaregistrovaný libovolný počet studentů.

V následujících částech vytvoříte třídu pro každou z těchto entit.

> [!NOTE]
> Pokud se pokusíte zkompilovat projekt před dokončením vytváření všech těchto tříd entit, zobrazí se chyby kompilátoru.

### <a name="the-student-entity"></a>Entita studenta

- Ve složce *modely* vytvořte soubor třídy s názvem *student.cs* tak, že kliknete pravým tlačítkem na složku v **Průzkumník řešení** a zvolíte **Přidat** > **třídu**. Nahraďte kód šablony následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

Vlastnost `ID` se změní na sloupec primárního klíče tabulky databáze, který odpovídá této třídě. Ve výchozím nastavení Entity Framework interpretuje vlastnost s názvem `ID` nebo *classname* `ID` jako primární klíč.

Vlastnost `Enrollments` je *navigační vlastnost*. Navigační vlastnosti obsahují další entity, které se vztahují k této entitě. V tomto případě bude vlastnost `Enrollments` entity `Student` obsahovat všechny entity `Enrollment`, které souvisejí s entitou `Student`. Jinými slovy, pokud daný `Student` řádek v databázi obsahuje dva související `Enrollment` řádky (řádky, které obsahují hodnotu primárního klíče tohoto studenta ve sloupci `StudentID` cizí klíč), tato vlastnost `Student` `Enrollments` navigace této entity bude obsahovat tyto dvě entity `Enrollment`.

Navigační vlastnosti jsou obvykle definovány jako `virtual` tak, aby mohly využívat určité Entity Framework funkce, jako je *opožděné načítání*. (Opožděné načítání bude vysvětleno později v kurzu [čtení souvisejících dat](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) dále v této sérii.)

Pokud navigační vlastnost může obsahovat více entit (jako v relacích m:n nebo 1:1), musí se jednat o seznam, ve kterém lze přidávat, odstraňovat a aktualizovat položky, například `ICollection`.

### <a name="the-enrollment-entity"></a>Registrace entity

- Ve složce *modely* vytvořte *Enrollment.cs* a nahraďte existující kód následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

Vlastnost `EnrollmentID` bude primární klíč. Tato entita používá `ID` vzor *ClassName* místo `ID` sám sebe, jako jste viděli v entitě `Student`. Obvykle byste zvolili jeden model a používali ho v rámci svého datového modelu. V tomto příkladu variace znázorňuje, že můžete použít libovolný vzor. V pozdějším kurzu uvidíte, jak používat `ID` bez `classname` usnadňuje implementaci dědičnosti v datovém modelu.

Vlastnost `Grade` je [výčet](/ef/ef6/modeling/code-first/data-types/enums). Otazník po deklaraci typu `Grade` označuje, že vlastnost `Grade` může [mít hodnotu null](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types). Třídu, která má hodnotu null, se liší od nulové třídy – hodnota null znamená, že se nejedná o známku nebo ještě nebyla přiřazena.

Vlastnost `StudentID` je cizí klíč a odpovídající navigační vlastnost je `Student`. Entita `Enrollment` je přidružená k jedné entitě `Student`, takže vlastnost může uchovávat jenom jednu entitu `Student` (na rozdíl od `Student.Enrollments` navigační vlastnost, kterou jste viděli dříve, která může obsahovat několik entit `Enrollment`).

Vlastnost `CourseID` je cizí klíč a odpovídající navigační vlastnost je `Course`. Entita `Enrollment` je přidružená k jedné entitě `Course`.

Entity Framework interpretuje vlastnost jako vlastnost cizího klíče, pokud má název *&lt;navigační vlastnost&gt;&lt;název vlastnosti primárního klíče&gt;* (například `StudentID` pro `Student` navigační vlastnost, protože je `Student` primární klíč entity `ID`). Vlastnosti cizího klíče lze také pojmenovat stejným *&lt;název vlastnosti primárního klíče&gt;* (například `CourseID`, protože primární klíč entity `Course` je `CourseID`).

### <a name="the-course-entity"></a>Kurz entity

- Ve složce *modely* vytvořte *Course.cs*a nahraďte kód šablony následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

Vlastnost `Enrollments` je navigační vlastnost. Entita `Course` může souviset s libovolným počtem entit `Enrollment`.

Další informace o atributu <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> v pozdějším kurzu této série. V podstatě vám tento atribut umožňuje zadat primární klíč pro kurz místo toho, aby ho databáze vygenerovala.

## <a name="create-the-database-context"></a>Vytvoření kontextu databáze

Hlavní třída, která koordinuje funkce Entity Framework pro daný datový model, je třída *kontextu databáze* . Tuto třídu vytvoříte odvozením z třídy [System. data. entity. DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) . Ve vašem kódu určíte, které entity budou zahrnuty v datovém modelu. Můžete také přizpůsobit určité chování Entity Framework. V tomto projektu je třída pojmenována `SchoolContext`.

- Chcete-li vytvořit složku v projektu ContosoUniversity, klikněte pravým tlačítkem myši na projekt v **Průzkumník řešení** a klikněte na možnost **Přidat**a poté klikněte na možnost **Nová složka**. Pojmenujte novou složku *dal* (pro přístup k datům). V této složce vytvořte nový soubor třídy s názvem *SchoolContext.cs*a nahraďte kód šablony následujícím kódem:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>Zadání sad entit

Tento kód vytvoří vlastnost [negenerickými](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) pro každou sadu entit. V Entity Framework terminologii *sada entit* obvykle odpovídá tabulce databáze a *entita* odpovídá řádku v tabulce.

> [!NOTE]
>
> Můžete vynechat příkazy `DbSet<Enrollment>` a `DbSet<Course>` a bude fungovat stejně. Entity Framework by je implicitně zahrnovaly, protože `Student` entita odkazuje na entitu `Enrollment` a entita `Enrollment` odkazuje na entitu `Course`.

### <a name="specify-the-connection-string"></a>Zadejte připojovací řetězec

Název připojovacího řetězce (který přidáte do souboru Web. config později) je předán do konstruktoru.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

Místo názvu, který je uložen v souboru Web. config, můžete také předat samotný připojovací řetězec. Další informace o možnostech určení databáze, která se má použít, najdete v tématu [připojovací řetězce a modely](/ef/ef6/fundamentals/configuring/connection-strings).

Pokud nezadáte připojovací řetězec nebo název explicitně, Entity Framework předpokládá, že název připojovacího řetězce je stejný jako název třídy. Výchozí název připojovacího řetězce v tomto příkladu by pak byl `SchoolContext`stejný jako to, co explicitně zadáte.

### <a name="specify-singular-table-names"></a>Zadat jednotné názvy tabulek

Příkaz `modelBuilder.Conventions.Remove` v metodě [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) zabraňuje v pluralitování názvů tabulek. Pokud jste to neudělali, vygenerované tabulky v databázi budou pojmenovány `Students`, `Courses`a `Enrollments`. Místo toho se názvy tabulek `Student`, `Course`a `Enrollment`. Vývojáři nesouhlasí s tím, zda by měly být názvy tabulek v množném čísle. V tomto kurzu se používá jednotný formulář, ale důležitým bodem je, že můžete vybrat libovolný formulář, který dáváte přednost při zahrnutí nebo vynechání tohoto řádku kódu.

## <a name="initialize-db-with-test-data"></a>Inicializovat databázi s testovacími daty

Entity Framework může při spuštění aplikace automaticky vytvořit (nebo vyřadit a znovu vytvořit) databázi. Můžete určit, že se má provést při každém spuštění aplikace, nebo jenom v případě, že model není synchronizovaný se stávající databází. Můžete také napsat metodu `Seed`, která Entity Framework automaticky volá po vytvoření databáze, aby se naplnila testovacími daty.

Výchozím chováním je vytvořit databázi pouze v případě, že neexistuje (a vyvolat výjimku, pokud se model změnil a databáze již existuje). V této části určíte, že se má databáze při každé změně modelu vyřadit a znovu vytvořit. Vyřazení databáze způsobí ztrátu všech vašich dat. To je obvykle v pořádku během vývoje, protože metoda `Seed` se spustí, když se databáze znovu vytvoří a znovu vytvoří vaše testovací data. Ale v produkčním prostředí nechcete při každé změně schématu databáze obvykle ztratit všechna data. Později se dozvíte, jak zpracovat změny modelu pomocí Migrace Code First ke změně schématu databáze místo vyřazení a opětovnému vytvoření databáze.

1. Ve složce DAL vytvořte nový soubor třídy s názvem *SchoolInitializer.cs* a nahraďte kód šablony následujícím kódem, což způsobí, že se databáze vytvoří v případě potřeby a načte testovací data do nové databáze.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   Metoda `Seed` přebírá objekt kontextu databáze jako vstupní parametr a kód v metodě používá tento objekt k přidání nových entit do databáze. Pro každý typ entity kód vytvoří kolekci nových entit, přidá je do příslušné vlastnosti `DbSet` a poté uloží změny do databáze. Není nutné volat metodu `SaveChanges` za každou skupinu entit, jak je zde provedeno, ale to vám pomůže najít zdroj problému, pokud dojde k výjimce, když kód zapisuje do databáze.

2. Chcete-li sdělit, Entity Framework použít třídu inicializátoru, přidejte element do `entityFramework` elementu v souboru *Web. config* aplikace (ten v kořenové složce projektu), jak je znázorněno v následujícím příkladu:

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   `context type` Určuje plně kvalifikovaný název třídy kontextu a sestavení, ve kterém je, a `databaseinitializer type` Určuje plně kvalifikovaný název třídy inicializátoru a sestavení, ve kterém je. (Pokud nechcete, aby EF používal inicializátor, můžete nastavit atribut pro element `context`: `disableDatabaseInitialization="true"`.) Další informace najdete v tématu [nastavení konfiguračního souboru](/ef/ef6/fundamentals/configuring/config-file).

   Alternativou k nastavení inicializátoru v souboru *Web. config* je jeho provedení v kódu přidáním příkazu `Database.SetInitializer` do metody `Application_Start` v souboru *Global.asax.cs* . Další informace najdete v tématu [Principy inicializátorů databáze v Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm).

Aplikace je teď nastavená tak, aby při prvním přístupu k databázi v daném spuštění aplikace Entity Framework porovnává databázi s modelem (vaše `SchoolContext` třídy a třídy entit). V případě, že dojde k rozdílu, aplikace uvolní a znovu vytvoří databázi.

> [!NOTE]
> Když nasadíte aplikaci na provozní webový server, je nutné odebrat nebo zakázat kód, který databázi vyřazuje a znovu vytvoří. V pozdějším kurzu v této sérii provedete.

## <a name="set-up-ef-6-to-use-localdb"></a>Nastavte pro použití LocalDB EF 6.

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) je zjednodušená verze databázového stroje SQL Server Express. Instalaci a konfiguraci, spuštění na vyžádání a spuštění v uživatelském režimu je snadné. LocalDB se spouští ve speciálním režimu provádění SQL Server Express, který umožňuje pracovat s databázemi jako se soubory *. mdf* . Soubory databáze LocalDB můžete umístit do složky *Data\_aplikace* webového projektu, pokud chcete mít možnost zkopírovat databázi do projektu. Funkce uživatelské instance v SQL Server Express také umožňuje pracovat se soubory *. mdf* , ale funkce uživatelské instance je zastaralá. Proto se LocalDB doporučuje pro práci se soubory *. mdf* . LocalDB se ve výchozím nastavení instaluje v aplikaci Visual Studio.

Pro produkční webové aplikace se obvykle SQL Server Express nepoužívá. LocalDB se konkrétně nedoporučuje pro použití v produkčním prostředí s webovou aplikací, protože není navržená pro práci se službou IIS.

- V tomto kurzu budete pracovat s LocalDB. Otevřete soubor *Web. config* aplikace a přidejte `connectionStrings` element předcházející `appSettings` elementu, jak je znázorněno v následujícím příkladu. (Nezapomeňte aktualizovat soubor *Web. config* v kořenové složce projektu. V podsložce *zobrazení* je také soubor *Web. config* , který není nutné aktualizovat.)

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

Připojovací řetězec, který jste přidali, určuje, že Entity Framework bude používat databázi LocalDB s názvem *ContosoUniversity1. mdf*. (Databáze zatím neexistuje, ale EF ji vytvoří.) Pokud chcete vytvořit databázi ve složce *\_dat vaší aplikace* , můžete přidat `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` do připojovacího řetězce. Další informace o připojovacích řetězcích najdete v tématu [SQL Server připojovacích řetězců pro webové aplikace v ASP.NET](/previous-versions/aspnet/jj653752(v=vs.110)).

V souboru *Web. config* nebudete ve skutečnosti potřebovat připojovací řetězec. Pokud neposkytnete připojovací řetězec, Entity Framework používá výchozí připojovací řetězec na základě vaší třídy kontextu. Další informace najdete v tématu [Code First k nové databázi](/ef/ef6/modeling/code-first/workflows/new-database).

## <a name="create-controller-and-views"></a>Vytvořit kontroler a zobrazení

Teď vytvoříte webovou stránku, na které se budou zobrazovat data. Proces vyžádání dat automaticky aktivuje vytvoření databáze. Začnete vytvořením nového kontroleru. Než to uděláte, sestavte projekt, aby byly třídy modelů a kontextu dostupné pro generování uživatelského rozhraní kontroléru MVC.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na složku **řadiče** , vyberte **Přidat**a pak klikněte na **Nová vygenerovaná položka**.
2. V dialogovém okně **Přidat vygenerované uživatelské rozhraní** vyberte **kontroler MVC 5 se zobrazeními, pomocí Entity Framework**a pak zvolte **Přidat**.

     ![Dialogové okno Přidat generování uživatelského rozhraní v aplikaci Visual Studio](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. V dialogovém okně **Přidat řadič** proveďte následující výběry a pak zvolte **Přidat**:

   - Třída modelu: **student (ContosoUniversity. Models)** . (Pokud v rozevíracím seznamu tuto možnost nevidíte, sestavte projekt a zkuste to znovu.)
   - Třída kontextu dat: **SchoolContext (ContosoUniversity. dal)** .
   - Název kontroleru: **StudentController** (ne StudentsController).
   - Ponechte výchozí hodnoty pro ostatní pole.

     Po kliknutí na tlačítko **Přidat**generátor vytvoří soubor *StudentController.cs* a sadu zobrazení (soubory *. cshtml* ), které pracují s řadičem. V budoucnu, když vytváříte projekty, které používají Entity Framework, můžete také využít výhod některých dalších funkcí generátoru: Vytvořte svoji první třídu modelu, nevytvářejte připojovací řetězec a potom v poli **Přidat kontrolér** zadejte **nový kontext dat** tak, že vyberete tlačítko **+** vedle **třídy datový kontext**. Lešení vytvoří třídu `DbContext` a váš připojovací řetězec také jako kontroler a zobrazení.
4. Visual Studio otevře soubor *Controllers\StudentController.cs* . Vidíte, že byla vytvořena proměnná třídy, která vytvoří instanci objektu kontextu databáze:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     Metoda `Index` akce načte seznam studentů ze sady entit *studentů* načtením vlastnosti `Students` instance kontextu databáze:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     Zobrazení *Student\Index.cshtml* zobrazí tento seznam v tabulce:

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. Stisknutím kombinace kláves CTRL + F5 spusťte projekt. (Pokud se zobrazí chyba "nelze vytvořit stínovou kopii", zavřete prohlížeč a zkuste to znovu.)

     Kliknutím na kartu **Students** zobrazíte testovací data, která byla vložená metodou `Seed`. V závislosti na tom, jak úzká je okno prohlížeče, uvidíte v horním adresním řádku odkaz na kartu student nebo kliknutím na pravý horní roh zobrazíte odkaz.

     ![Tlačítko nabídky](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a>Zobrazení databáze

Když jste spustili stránku Students a aplikace se pokusila získat přístup k databázi, EF zjistila, že neexistovala žádná databáze a nebyla vytvořena. EF pak spustila metodu počáteční hodnoty k naplnění databáze daty.

K zobrazení databáze v aplikaci Visual Studio můžete použít buď **Průzkumník serveru** , nebo **Průzkumník objektů systému SQL Server** (SSOX). V tomto kurzu použijete **Průzkumník serveru**.

1. Zavřete prohlížeč.
2. V **Průzkumník serveru**rozbalte **datová připojení** (nejdřív možná budete muset vybrat tlačítko Aktualizovat), rozbalte **školní kontext (ContosoUniversity)** a potom rozbalte **tabulky** , abyste viděli tabulky v nové databázi.

3. Klikněte pravým tlačítkem myši na tabulku **student** a kliknutím na možnost **Zobrazit data tabulky** Zobrazte sloupce, které byly vytvořeny, a řádky, které byly vloženy do tabulky.

4. Zavřete **Průzkumník serveru** připojení.

Soubory databáze *ContosoUniversity1. mdf* a *. ldf* jsou ve složce *% USERPROFILE%* .

Vzhledem k tomu, že používáte inicializátor `DropCreateDatabaseIfModelChanges`, můžete nyní provést změnu `Student` třídy, znovu spustit aplikaci a databáze by se automaticky znovu vytvořila, aby odpovídala vaší změně. Pokud například přidáte vlastnost `EmailAddress` do třídy `Student`, spusťte znovu stránku Students a potom se znovu podívejte na tabulku a zobrazí se nový `EmailAddress` sloupec.

## <a name="conventions"></a>Zásady

Množství kódu, který jste museli zapsat, aby Entity Framework mohl vytvořit úplnou databázi, je minimální z důvodu *konvencí*nebo předpokladů, které Entity Framework provádí. Některé z nich již byly označeny nebo byly použity bez vědomí, že jsou:

- V množném čísle se používají v názvech tabulek názvy tříd entit.
- Názvy vlastností entit se používají pro názvy sloupců.
- Vlastnosti entity s názvem `ID` nebo *classname* `ID` jsou rozpoznávány jako vlastnosti primárního klíče.
- Vlastnost je interpretována jako vlastnost cizího klíče, pokud je pojmenována *&lt;název vlastnosti navigace&gt;&lt;název vlastnosti primárního klíče&gt;* (například `StudentID` pro `Student` navigační vlastnost, protože je `Student` primární klíč entity `ID`). Vlastnosti cizího klíče lze také pojmenovat stejným &lt;název vlastnosti primárního klíče&gt; (například `EnrollmentID`, protože primární klíč entity `Enrollment` je `EnrollmentID`).

Viděli jste, že konvence lze přepsat. Například jste určili, že názvy tabulek by neměly být v množném číslech a později uvidíte, jak vlastnost explicitně označit jako vlastnost cizího klíče.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Další informace o EF 6 najdete v těchto článcích:

* [Přístup k datům ASP.NET – doporučené zdroje informací](../../../../whitepapers/aspnet-data-access-content-map.md)

* [Code First konvence](/ef/ef6/modeling/code-first/conventions/built-in)

* [Vytvoření složitějšího datového modelu](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvořená webová aplikace MVC
> * Nastavit styl lokality
> * Nainstalováno Entity Framework 6
> * Vytvoření datového modelu
> * Byl vytvořen kontext databáze.
> * Inicializovaná databáze s testovacími daty
> * Nastavte pro použití LocalDB EF 6.
> * Vytvořen kontroler a zobrazení
> * Zobrazení databáze

V dalším článku se dozvíte, jak zkontrolovat a přizpůsobit kód vytvoření, čtení, aktualizace, odstranění (CRUD) v řadičích a zobrazeních.
> [!div class="nextstepaction"]
> [Implementace základní funkce CRUD](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)