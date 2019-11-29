---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: Vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC (1 z 10) | Microsoft Docs
author: tdykstra
description: K dispozici je novější verze této série kurzů, pro Visual Studio 2013 Entity Framework 6 a MVC 5. Ukázková webová aplikace společnosti Contoso University de...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8ee5aa22b6b2329b01d41437f30508e28a2288b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595974"
---
# <a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>Vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC (1 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > K dispozici je [novější verze této série kurzů](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) , pro Visual Studio 2013 Entity Framework 6 a MVC 5.
> 
> 
> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Entity Framework 5 a Visual Studio 2012. Ukázková aplikace je web pro fiktivní univerzitě společnosti Contoso. Zahrnuje funkce, jako je například využití studenta, vytváření kurzu a přiřazení instruktora. V této sérii kurzů se dozvíte, jak sestavit ukázkovou aplikaci Contoso University. [Dokončenou aplikaci](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)si můžete stáhnout.
> 
> ## <a name="code-first"></a>Code First
> 
> Existují tři způsoby, jak můžete pracovat s daty v Entity Framework: *Database First*, *model First*a *Code First*. Tento kurz je určen pro Code First. Informace o rozdílech mezi těmito pracovními postupy a pokyny pro výběr nejvhodnějšího řešení pro váš scénář najdete v tématu [Entity Framework vývojové pracovní postupy](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="mvc"></a>MVC
> 
> Ukázková aplikace je postavená na [ASP.NET MVC](../../../index.md). Pokud dáváte přednost práci s modelem webových formulářů ASP.NET, přečtěte si téma [vázání modelů a kurzy webových formulářů](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) a [Mapa obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).
> 
> ## <a name="software-versions"></a>Verze softwaru
> 
> | **Zobrazuje se v tomto kurzu.** | **Funguje taky s** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Visual Studio 2012 Express for Web. Tuto sadu automaticky nainstaluje sada Windows Azure SDK, pokud ještě nemáte VS 2012 nebo VS 2012 Express pro web. Visual Studio 2013 by měl fungovat, ale kurz se s ním netestoval a některé nabídky a dialogová okna se liší. Pro nasazení Windows Azure se vyžaduje [verze VS 2013 sady Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323510) . |
> | .NET 4.5 | Většina zobrazených funkcí bude fungovat v .NET 4, ale některé ne. Například podpora výčtu v EF vyžaduje rozhraní .NET 4,5. |
> | Entity Framework 5 |  |
> | [Windows Azure SDK 2,1](https://go.microsoft.com/fwlink/p/?linkid=323511) | Pokud přeskočíte kroky nasazení Windows Azure, nebudete potřebovat sadu SDK. Po vydání nové verze sady SDK bude odkaz instalovat novější verzi. V takovém případě může být nutné přizpůsobit některé pokyny novému uživatelskému rozhraní a funkcím. |
> 
> ## <a name="questions"></a>Otázky
> 
> Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra ASP.NET Entity Framework](https://forums.asp.net/1227.aspx), [Entity Framework a LINQ to Entities fóra](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)nebo [StackOverflow.com](http://stackoverflow.com/).
> 
> ## <a name="acknowledgments"></a>Potvrzení
> 
> Podívejte se na poslední kurz v řadě pro [potvrzení a poznámku o jazyce VB](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments).
> 
> ## <a name="original-version-of-the-tutorial"></a>Původní verze kurzu
> 
> Původní verze kurzu je k dispozici v [e-knize EF 4,1/MVC 3](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC).

## <a name="the-contoso-university-web-application"></a>Webová aplikace Contoso University

Aplikace, kterou budete sestavovat v těchto kurzech, je jednoduchý web na univerzitě.

Uživatelé můžou zobrazit a aktualizovat informace o studentech, kurzech a instruktorech. Tady je několik obrazovek, které vytvoříte.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

Styl uživatelského rozhraní tohoto webu byl ponechán blízko toho, co vygenerovaly předdefinované šablony, takže se tento kurz může soustředit hlavně na použití Entity Framework.

## <a name="prerequisites"></a>Požadavky

Pokyny a snímky obrazovky v tomto kurzu předpokládají, že používáte sadu [Visual studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) nebo [Visual Studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131), s nejnovější aktualizací a sadou Azure SDK pro .NET nainstalovanou od července 2013. To všechno můžete získat pomocí následujícího odkazu:

[Azure SDK pro .NET (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

Pokud máte nainstalovanou aplikaci Visual Studio, bude výše uvedený odkaz instalovat všechny chybějící součásti. Pokud nemáte Visual Studio, bude tento odkaz instalovat Visual Studio 2012 Express for Web. Můžete použít Visual Studio 2013, ale některé z požadovaných postupů a obrazovek se budou lišit.

## <a name="create-an-mvc-web-application"></a>Vytvoření webové aplikace MVC

Otevřete Visual Studio a vytvořte nový C# projekt s názvem "ContosoUniversity" pomocí šablony **webové aplikace ASP.NET MVC 4** . Ujistěte se, že cílíte na **.NET Framework 4,5** (budete používat [vlastnosti`enum`](https://msdn.microsoft.com/data/hh859576.aspx)a budete potřebovat .NET 4,5).

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu **Internetová aplikace** .

Nechejte vybraný modul zobrazení **Razor** a nechejte nezaškrtnuté políčko **vytvořit projekt testování částí** .

Klikněte na tlačítko **OK**.

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>Nastavení stylu webu

V několika jednoduchých změnách se nastaví nabídka web, rozložení a Domovská stránka.

Otevřete *Views\Shared\\_Layout. cshtml*a nahraďte obsah souboru následujícím kódem. Změny jsou zvýrazněny.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

Tento kód provede následující změny:

- Nahradí instance šablon "Moje aplikace ASP.NET MVC" a "logo" v rámci "contoso University".
- Přidá několik odkazů akcí, které budou použity později v tomto kurzu.

V *Views\Home\Index.cshtml*nahraďte obsah souboru následujícím kódem, který eliminuje odstavce šablony o ASP.NET a MVC:

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

V *souboru controllers\homecontroller.cs*změňte hodnotu `ViewBag.Message` v metodě `Index` Action na "Vítejte na společnosti Contoso University!", jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

Stisknutím kombinace kláves CTRL + F5 web spusťte. V hlavní nabídce se zobrazí domovská stránka.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>Vytvoření datového modelu

V dalším kroku vytvoříte třídy entit pro aplikaci Contoso University. Začnete s následujícími třemi entitami:

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

Mezi entitami `Student` a `Enrollment` existuje vztah 1:1 a mezi `Course`mi a `Enrollment` entitami existuje vztah 1: n. Jinými slovy, student může být zaregistrovaný v jakémkoli počtu kurzů a kurz může mít zaregistrovaný libovolný počet studentů.

V následujících částech vytvoříte třídu pro každou z těchto entit.

> [!NOTE]
> Pokud se pokusíte zkompilovat projekt před dokončením vytváření všech těchto tříd entit, zobrazí se chyby kompilátoru.

### <a name="the-student-entity"></a>Entita studenta

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

Ve složce *modely* vytvořte *student.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

Vlastnost `StudentID` se změní na sloupec primárního klíče tabulky databáze, který odpovídá této třídě. Ve výchozím nastavení Entity Framework interpretuje vlastnost s názvem `ID` nebo *classname* `ID` jako primární klíč.

Vlastnost `Enrollments` je *navigační vlastnost*. Navigační vlastnosti obsahují další entity, které se vztahují k této entitě. V tomto případě bude vlastnost `Enrollments` entity `Student` obsahovat všechny entity `Enrollment`, které souvisejí s entitou `Student`. Jinými slovy, pokud daný `Student` řádek v databázi obsahuje dva související `Enrollment` řádky (řádky, které obsahují hodnotu primárního klíče tohoto studenta ve sloupci `StudentID` cizí klíč), tato vlastnost `Student` `Enrollments` navigace této entity bude obsahovat tyto dvě entity `Enrollment`.

Navigační vlastnosti jsou obvykle definovány jako `virtual` tak, aby mohly využívat určité Entity Framework funkce, jako je *opožděné načítání*. (Opožděné načítání bude vysvětleno později v kurzu [čtení souvisejících dat](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) dále v této sérii.

Pokud navigační vlastnost může obsahovat více entit (jako v relacích m:n nebo 1:1), musí se jednat o seznam, ve kterém lze přidávat, odstraňovat a aktualizovat položky, například `ICollection`.

### <a name="the-enrollment-entity"></a>Entita registrace

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

Ve složce *modely* vytvořte *Enrollment.cs* a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

Vlastnost plat je [výčet](https://msdn.microsoft.com/data/hh859576.aspx). Otazník po deklaraci typu `Grade` označuje, že vlastnost `Grade` může [mít hodnotu null](https://msdn.microsoft.com/library/2cf62fcy.aspx). Třídu, která má hodnotu null, se liší od nulové třídy – hodnota null znamená, že se nejedná o známku nebo ještě nebyla přiřazena.

Vlastnost `StudentID` je cizí klíč a odpovídající navigační vlastnost je `Student`. Entita `Enrollment` je přidružená k jedné entitě `Student`, takže vlastnost může uchovávat jenom jednu entitu `Student` (na rozdíl od `Student.Enrollments` navigační vlastnost, kterou jste viděli dříve, která může obsahovat několik entit `Enrollment`).

Vlastnost `CourseID` je cizí klíč a odpovídající navigační vlastnost je `Course`. Entita `Enrollment` je přidružená k jedné entitě `Course`.

### <a name="the-course-entity"></a>Entita kurzu

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

Ve složce *modely* vytvořte *Course.cs*a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

Vlastnost `Enrollments` je navigační vlastnost. Entita `Course` může souviset s libovolným počtem entit `Enrollment`.

Vyberu si další informace o [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)). None)] v dalším kurzu. V podstatě vám tento atribut umožňuje zadat primární klíč pro kurz místo toho, aby ho databáze vygenerovala.

## <a name="create-the-database-context"></a>Vytvoření kontextu databáze

Hlavní třída, která koordinuje funkce Entity Framework pro daný datový model, je třída *kontextu databáze* . Tuto třídu vytvoříte odvozením z třídy [System. data. entity. DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) . Ve vašem kódu určíte, které entity budou zahrnuty v datovém modelu. Můžete také přizpůsobit určité chování Entity Framework. V tomto projektu je třída pojmenována `SchoolContext`.

Vytvořte složku s názvem *dal* (pro úroveň přístupu k datům). V této složce vytvořte nový soubor třídy s názvem *SchoolContext.cs*a nahraďte existující kód následujícím kódem:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Tento kód vytvoří vlastnost [negenerickými](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) pro každou sadu entit. V Entity Framework terminologii *sada entit* obvykle odpovídá tabulce databáze a *entita* odpovídá řádku v tabulce.

Příkaz `modelBuilder.Conventions.Remove` v metodě [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) zabraňuje v pluralitování názvů tabulek. Pokud jste to neudělali, vygenerované tabulky budou pojmenovány `Students`, `Courses`a `Enrollments`. Místo toho se názvy tabulek `Student`, `Course`a `Enrollment`. Vývojáři nesouhlasí s tím, zda by měly být názvy tabulek v množném čísle. V tomto kurzu se používá jednotný formulář, ale důležitým bodem je, že můžete vybrat libovolný formulář, který dáváte přednost při zahrnutí nebo vynechání tohoto řádku kódu.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) je zjednodušená verze databázového stroje SQL Server Express, která se spouští na vyžádání a běží v uživatelském režimu. LocalDB se spouští ve speciálním režimu provádění SQL Server Express, který umožňuje pracovat s databázemi jako se soubory *. mdf* . Soubory databáze LocalDB jsou obvykle uloženy ve složce *App\_data* webového projektu. Funkce uživatelské instance v SQL Server Express také umožňuje pracovat se soubory *. mdf* , ale funkce uživatelské instance je zastaralá. Proto se LocalDB doporučuje pro práci se soubory *. mdf* .

Pro produkční webové aplikace se typicky nepoužívá SQL Server Express. LocalDB se konkrétně nedoporučuje pro použití v produkčním prostředí s webovou aplikací, protože není navržená pro práci se službou IIS.

V aplikaci Visual Studio 2012 a novějších verzích je LocalDB ve výchozím nastavení nainstalován v aplikaci Visual Studio. V aplikaci Visual Studio 2010 a starších verzích SQL Server Express (bez LocalDB) je ve výchozím nastavení nainstalovány v aplikaci Visual Studio; Pokud používáte aplikaci Visual Studio 2010, je nutné ji nainstalovat ručně.

V tomto kurzu budete pracovat s LocalDB, aby bylo možné databázi Uložit do složky *aplikace\_data* jako soubor *. mdf* . Otevřete kořenový soubor *Web. config* a přidejte do kolekce `connectionStrings` nový připojovací řetězec, jak je znázorněno v následujícím příkladu. (Nezapomeňte aktualizovat soubor *Web. config* v kořenové složce projektu. V podsložce *zobrazení* je také soubor *Web. config* , který není nutné aktualizovat.)

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

Ve výchozím nastavení Entity Framework hledá připojovací řetězec s názvem stejný jako `DbContext` třída (`SchoolContext` pro tento projekt). Připojovací řetězec, který jste přidali, určuje databázi LocalDB s názvem *ContosoUniversity. mdf* umístěnou ve složce *App\_data* . Další informace najdete v tématu [SQL Server připojovacích řetězců pro webové aplikace ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).

Nemusíte ve skutečnosti zadávat připojovací řetězec. Pokud neposkytnete připojovací řetězec, Entity Framework vám ho vytvořit. databáze ale nemusí být ve složce *app\_data* vaší aplikace. Informace o tom, kde se databáze vytvoří, najdete v tématu [Code First do nové databáze](https://msdn.microsoft.com/data/jj193542).

Kolekce `connectionStrings` má také připojovací řetězec s názvem `DefaultConnection`, který se používá pro databázi členství. V tomto kurzu nebudete používat databázi členství. Jediným rozdílem mezi dvěma připojovacími řetězci je název databáze a hodnota atributu name.

## <a name="set-up-and-execute-a-code-first-migration"></a>Nastavení a provedení migrace Code First

Při prvním spuštění vývoje aplikace se datový model často mění a pokaždé, když se model změní, se v databázi nesynchronizuje. Můžete nakonfigurovat Entity Framework pro automatické vyřazení a opětovné vytvoření databáze pokaždé, když změníte datový model. Nejedná se o problém, který brzy vyvíjíme, protože testovací data se snadno znovu vytvoří, ale po nasazení do produkčního prostředí budete obvykle chtít aktualizovat schéma databáze, aniž byste museli databázi vynechat. Funkce migrace umožňuje Code First aktualizovat databázi, aniž by byla vyhozena a znovu vytvořena. Brzy v cyklu vývoje nového projektu můžete chtít použít [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) k vyřazení, opětovnému vytvoření a opětovnému vytvoření počáteční databáze při každém změně modelu. Jakmile budete připraveni k nasazení aplikace, můžete převést na přístup k migraci. V tomto kurzu budete používat jenom migrace. Další informace najdete v tématu [migrace Code First](https://msdn.microsoft.com/data/jj591621) a [migrace datových řad pro záznam dění](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)v/v.

### <a name="enable-code-first-migrations"></a>Povolit Migrace Code First

1. V nabídce **nástroje** klikněte na **Správce balíčků NuGet** a pak na **Konzola správce balíčků**.

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. Do `PM>`ového řádku zadejte následující příkaz:

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![Enable – migrace – příkaz](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    Tento příkaz vytvoří složku *migrace* v projektu ContosoUniversity a vloží do této složky soubor *Configuration.cs* , který můžete upravit a nakonfigurovat migrace.

    ![Složka migrace](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    Třída `Configuration` zahrnuje `Seed` metodu, která je volána při vytvoření databáze a pokaždé, když je aktualizována po změně datového modelu.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    Účelem této `Seed` metody je umožnit vložení testovacích dat do databáze poté, co je Code First vytvoří nebo aktualizuje.

### <a name="set-up-the-seed-method"></a>Nastavení metody osazení

Metoda [počáteční](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) hodnoty se spustí, když migrace Code First vytvoří databázi a pokaždé, když aktualizuje databázi na nejnovější migraci. Účelem metody osazení je umožnit vložení dat do tabulek předtím, než aplikace poprvé přistupuje k databázi.

V dřívějších verzích Code First před vydáním migrace bylo běžné, že `Seed` metody pro vkládání testovacích dat, protože při vývoji se při každé změně modelu databáze musela úplně odstranit a znovu vytvořit od začátku. Při Migrace Code First se testovací data uchovávají po změnách databáze, takže včetně testovacích dat v metodě [osazení](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) obvykle není nutné. Ve skutečnosti nechcete, aby metoda `Seed` vkládání testovacích dat, pokud budete používat migrace k nasazení databáze do produkčního prostředí, protože metoda `Seed` se spustí v produkčním prostředí. V takovém případě má metoda `Seed` vložit do databáze pouze data, která chcete vložit do produkčního prostředí. Například můžete chtít, aby databáze zahrnovala vlastní názvy oddělení v tabulce `Department`, když se aplikace zpřístupní v produkčním prostředí.

Pro účely tohoto kurzu budete pro nasazení používat migrace, ale vaše `Seed` metoda bude přesto vkládat testovací data, aby bylo snazší zjistit, jak funguje funkce aplikace, aniž by bylo nutné ručně vkládat spoustu dat.

1. Nahraďte obsah souboru *Configuration.cs* následujícím kódem, který načte testovací data do nové databáze. 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    Metoda [počáteční](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) hodnoty přebírá objekt kontextu databáze jako vstupní parametr a kód v metodě používá tento objekt k přidání nových entit do databáze. Pro každý typ entity kód vytvoří kolekci nových entit, přidá je do příslušné vlastnosti [negenerickými](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) a poté uloží změny do databáze. Není nutné volat metodu [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) za každou skupinu entit, jak je zde provedeno, ale to vám pomůže najít zdroj problému, pokud dojde k výjimce, když kód zapisuje do databáze.

    Některé příkazy, které vkládají data, používají metodu [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) k provedení operace "Upsert". Vzhledem k tomu, že metoda `Seed` se spouští při každé migraci, nemůžete jenom vkládat data, protože řádky, které se pokoušíte přidat, už po první migraci vytvářející databázi budou. Operace "Upsert" zabraňuje chybám, které by byly provedeny při pokusu o vložení řádku, který již existuje, ale ***přepíše*** všechny změny dat, které jste mohli provést při testování aplikace. S testovacími daty v některých tabulkách možná nebudete chtít, aby došlo k tomu, že v některých případech změníte data při testování, které chcete po aktualizaci databáze zůstat. V takovém případě chcete provést operaci podmíněného vložení: vložte řádek pouze v případě, že ještě neexistuje. Metoda počáteční hodnoty používá obě přístupy.

    První parametr předaný metodě [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) určuje vlastnost, která má být použita pro kontrolu, zda řádek již existuje. Pro data testovacího studenta, která poskytujete, se dá pro tento účel použít vlastnost `LastName`, protože každé příjmení v seznamu je jedinečné:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    Tento kód předpokládá, že poslední názvy jsou jedinečné. Pokud ručně přidáte studenta s duplicitním posledním názvem, při příštím provedení migrace se zobrazí následující výjimka.

    Sekvence obsahuje více než jeden element.

    Další informace o metodě `AddOrUpdate` naleznete v tématu podrobnější informace [k metodě EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) na blogu Julie Lerman.

    Kód, který přidává `Enrollment` entit, nepoužívá metodu `AddOrUpdate`. Kontroluje, zda entita již existuje, a vloží entitu, pokud neexistuje. Tento přístup zachovává změny v úrovni registrace, když se spustí migrace. Kód projde každým členem [seznamu](https://msdn.microsoft.com/library/6sh2ey19.aspx) `Enrollment`a v případě, že se registrace v databázi nenajde, přidá do databáze registraci. Při první aktualizaci databáze bude databáze prázdná, takže se přidá každá registrace.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    Informace o tom, jak ladit metodu `Seed` a jak zpracovat redundantní data, jako jsou například dva studenti s názvem "Alexander Carson", naleznete v tématu [osazení a ladění Entity Framework (EF) databáze](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) na blogu Rick Anderson.
2. Sestavte projekt.

### <a name="create-and-execute-the-first-migration"></a>Vytvoření a provedení první migrace

1. V okně konzoly Správce balíčků zadejte následující příkazy: 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    Příkaz `add-migration` přidá do složky migrace soubor *[dateStamp]\_InitialCreate.cs* obsahující kód, který vytvoří databázi. První parametr (`InitialCreate)` se používá pro název souboru a může být libovolný, co potřebujete. obvykle si vybíráte slovo nebo frázi, která shrnuje, co se v migraci provádí. Můžete třeba pojmenovat pozdější migraci &quot;AddDepartmentTable&quot;.

    ![Složka migrace s počáteční migrací](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    Metoda `Up` třídy `InitialCreate` vytvoří tabulky databáze, které odpovídají sadám entit datového modelu, a metoda `Down` je odstraní. Migrace zavolá metodu `Up` pro implementaci změn datového modelu pro migraci. Když zadáte příkaz pro vrácení aktualizace, migrace zavolá metodu `Down`. Následující kód ukazuje obsah souboru `InitialCreate`:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    Příkaz `update-database` spustí metodu `Up` k vytvoření databáze a poté spustí metodu `Seed` k naplnění databáze.

Pro datový model se teď vytvořila databáze SQL Server. Název databáze je *ContosoUniversity*a soubor *. mdf* je ve složce *aplikace projektu\_dat* , protože to je to, co jste zadali v připojovacím řetězci.

K zobrazení databáze v aplikaci Visual Studio můžete použít buď **Průzkumník serveru** , nebo **Průzkumník objektů systému SQL Server** (SSOX). V tomto kurzu použijete **Průzkumník serveru**. V Visual Studio Express 2012 pro web se **Průzkumník serveru** nazývá **Průzkumník databáze**.

1. V nabídce **zobrazení** klikněte na příkaz **Průzkumník serveru**.
2. Klikněte na ikonu **Přidat připojení** .

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. Pokud se zobrazí výzva s dialogovým oknem **Zvolit zdroj dat** , klikněte na **Microsoft SQL Server**a potom klikněte na **pokračovat**.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. V dialogovém okně **Přidat připojení** zadejte do pole **název serveru** **(LocalDB) \v11.0** . V části **Vybrat nebo zadat název databáze**vyberte možnost **ContosoUniversity.**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. Klikněte na tlačítko **OK.**
6. Rozbalte položku **SchoolContext** a potom rozbalte položku **tabulky**.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. Klikněte pravým tlačítkem myši na tabulku **student** a kliknutím na možnost **Zobrazit data tabulky** Zobrazte sloupce, které byly vytvořeny, a řádky, které byly vloženy do tabulky.

    ![Tabulka studenta](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>Vytvoření kontroleru a zobrazení studenta

Dalším krokem je vytvoření kontroleru a zobrazení ASP.NET MVC ve vaší aplikaci, které mohou pracovat s jednou z těchto tabulek.

1. Chcete-li vytvořit řadič `Student`, klikněte pravým tlačítkem myši na složku **Controllers** v **Průzkumník řešení**, vyberte možnost **Přidat**a poté klikněte na možnost **kontroler**. V dialogovém okně **Přidat řadič** proveďte následující výběry a potom klikněte na tlačítko **Přidat**: 

   - Název kontroleru: **StudentController**.
   - Šablona: **kontroler MVC s akcemi a zobrazeními pro čtení/zápis pomocí Entity Framework**.
   - Třída modelu: **student (ContosoUniversity. Models)** . (Pokud v rozevíracím seznamu tuto možnost nevidíte, sestavte projekt a zkuste to znovu.)
   - Třída kontextu dat: **SchoolContext (ContosoUniversity. Models)** .
   - Zobrazení: **Razor (cshtml)** . (Výchozí nastavení.)

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio otevře soubor *Controllers\StudentController.cs* . Uvidíte, že byla vytvořena proměnná třídy, která vytvoří instanci objektu kontextu databáze:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     Metoda `Index` akce načte seznam studentů ze sady entit *studentů* načtením vlastnosti `Students` instance kontextu databáze:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     Zobrazení *Student\Index.cshtml* zobrazí tento seznam v tabulce:

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. Stisknutím kombinace kláves CTRL + F5 spusťte projekt.

     Kliknutím na kartu **Students** zobrazíte testovací data, která byla vložená metodou `Seed`.

     ![Stránka indexu studenta](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>Konvence

Množství kódu, který jste museli zapsat, aby Entity Framework mohl vytvořit úplnou databázi, je minimální z důvodu použití *konvencí*nebo předpokladů, které Entity Framework provádí. Některé z nich již byly zaznamenány:

- V množném čísle se používají v názvech tabulek názvy tříd entit.
- Názvy vlastností entit se používají pro názvy sloupců.
- Vlastnosti entity s názvem `ID` nebo *classname* `ID` jsou rozpoznávány jako vlastnosti primárního klíče.

Zjistili jste, že konvence je možné přepsat (například jste určili, že by se názvy tabulek neměly být v množném čísle) a další informace o konvencích a jejich přepsání v kurzu [vytvoření složitějšího datového modelu](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) později v této sérii. Další informace najdete v tématu [konvence Code First](https://msdn.microsoft.com/data/jj679962).

## <a name="summary"></a>Přehled

Nyní jste vytvořili jednoduchou aplikaci, která používá Entity Framework a SQL Server Express k ukládání a zobrazování dat. V následujícím kurzu se dozvíte, jak provádět základní operace CRUD (vytváření, čtení, aktualizace, odstranění). Zpětnou vazbu můžete v dolní části této stránky opustit. Dejte nám prosím jistotu, jak se vám tato část kurzu líbí a jak ji můžeme vylepšit.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Next](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
