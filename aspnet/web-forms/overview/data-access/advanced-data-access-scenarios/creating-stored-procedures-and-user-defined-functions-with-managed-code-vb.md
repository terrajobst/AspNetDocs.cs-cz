---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: Vytváření uložených procedur a uživatelsky definovaných funkcí se spravovaným kódem (VB) | Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 se integruje s modulem CLR (Common Language Runtime) .NET a umožňuje vývojářům vytvářet databázové objekty prostřednictvím spravovaného kódu. Tento kurz...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ac5f71d519689a9dc84fb82a04196d520cca6e1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74609803"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>Vytvoření uložených procedur a uživatelsky definovaných funkcí spravovaným kódem (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip) nebo [stažení PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005 se integruje s modulem CLR (Common Language Runtime) .NET a umožňuje vývojářům vytvářet databázové objekty prostřednictvím spravovaného kódu. V tomto kurzu se dozvíte, jak vytvořit spravované uložené procedury a spravované uživatelsky definované funkce pomocí C# Visual Basic nebo kódu. Zjistili jsme také, jak tyto edice sady Visual Studio umožňují ladit takové objekty spravované databáze.

## <a name="introduction"></a>Úvod

Databáze jako Microsoft s SQL Server 2005 pro vkládání, úpravu a načítání dat použijte [příkaz Transact-jazyk SQL (Structured Query Language) (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) . Většina databázových systémů zahrnuje konstrukce pro seskupení řady příkazů SQL, které se pak dají spustit jako jediná opakovaně použitelná jednotka. Uložené procedury jsou jedním příkladem. Další je *uživatelsky definované funkce*(UDF), což je konstruktor, který prověříme podrobněji v kroku 9.

V jádru je SQL navržený pro práci se sadami dat. Příkazy `SELECT`, `UPDATE`a `DELETE`, které se vztahují na všechny záznamy v odpovídající tabulce a jsou omezeny pouze pomocí jejich `WHERE` klauzulí. Pro práci s jedním záznamem je teď k dispozici mnoho funkcí jazyka a pro manipulaci s skalárními daty. [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) umožňují, aby se sada záznamů prošla cyklicky v jednom okamžiku. Funkce pro manipulaci s řetězci, jako je `LEFT`, `CHARINDEX`a `PATINDEX` fungují s skalárními daty. SQL zahrnuje také příkazy toku řízení, jako je `IF` a `WHILE`.

Před Microsoft SQL Server 2005 bylo možné uložené procedury a UDF definovat pouze jako kolekci příkazů T-SQL. SQL Server 2005 je však navržena tak, aby poskytovala integraci s modulem [CLR (Common Language Runtime)](https://msdn.microsoft.com/netframework/aa497266.aspx), což je modul runtime používaný všemi sestaveními .NET. V důsledku toho lze uložené procedury a UDF v databázi SQL Server 2005 vytvořit pomocí spravovaného kódu. To znamená, že můžete vytvořit uloženou proceduru nebo UDF jako metodu ve třídě Visual Basic. To umožňuje těmto uloženým procedurám a UDF využívat funkce v .NET Framework a z vlastních tříd.

V tomto kurzu podíváme se, jak vytvořit spravované uložené procedury a uživatelsky definované funkce a jak je integrovat do naší databáze Northwind. Pojďme začít!

> [!NOTE]
> Objekty spravované databáze nabízí oproti jejich protějškům SQL některé výhody. Bohatá a známá možnost jazyka a možnost opakovaného použití existujícího kódu a logiky jsou hlavními výhodami. Ale spravované databázové objekty budou pravděpodobně méně efektivní, pokud pracujete se sadami dat, která nezahrnují řadu procedurálních postupů. Podrobnější diskuzi o výhodách použití spravovaného kódu oproti T-SQL najdete v [výhodách použití spravovaného kódu k vytváření databázových objektů](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx).

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>Krok 1: Přesun databáze Northwind z`App_Data`

Všechny naše kurzy proto používaly soubor databáze Microsoft SQL Server 2005 Express edice ve složce Web Application `App_Data`. Umístění databáze do `App_Data` zjednodušené distribuce a spuštění těchto kurzů, protože všechny soubory se nacházely v jednom adresáři a nevyžadovaly žádné další kroky konfigurace k otestování tohoto kurzu.

Pro účely tohoto kurzu ale můžeme přesunout databázi Northwind z `App_Data` a explicitně ji zaregistrovat s instancí SQL Server 2005 Express Edition databáze. I když můžeme provést postup pro tento kurz s databází ve složce `App_Data`, je několik kroků mnohem jednodušší, protože explicitně zaregistrujete databázi pomocí instance databáze SQL Server 2005 Express Edition.

Stažení pro tento kurz obsahuje dva soubory databáze – `NORTHWND.MDF` a `NORTHWND_log.LDF` umístit do složky s názvem `DataFiles`. Pokud s vaší vlastní implementací kurzů pracujete, zavřete Visual Studio a přesuňte `NORTHWND.MDF` a `NORTHWND_log.LDF` soubory ze složky `App_Data` webů do složky mimo web. Až budou soubory databáze přesunuty do jiné složky, potřebujeme zaregistrovat databázi Northwind s instancí SQL Server 2005 Express Edition databáze. To se dá udělat z SQL Server Management Studio. Pokud máte v počítači nainstalovanou edici SQL Server 2005, která není Express, je už pravděpodobně Management Studio nainstalovaná. Pokud máte v počítači jenom SQL Server 2005 Express Edition, Stáhněte a nainstalujte [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796).

Spusťte SQL Server Management Studio. Jak ukazuje obrázek 1, Management Studio začíná dotazem, ke kterému serveru se má připojit. Jako název serveru zadejte localhost\SQLExpress, v rozevíracím seznamu ověřování vyberte ověřování systému Windows a klikněte na připojit.

![Připojte se k příslušné instanci databáze.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**Obrázek 1**: připojení k příslušné instanci databáze

Po připojení se v okně Průzkumník objektů zobrazí informace o instanci databáze SQL Server 2005 Express Edition, včetně jejích databází, informací o zabezpečení, možnostech správy a tak dále.

Musíme připojit databázi Northwind ve složce `DataFiles` (nebo kdekoli, kde jste ji přesunuli) do instance databáze SQL Server 2005 Express Edition. Klikněte pravým tlačítkem na složku databáze a v místní nabídce vyberte možnost připojit. Tím zobrazíte dialogové okno připojit databáze. Klikněte na tlačítko Přidat, přejděte k příslušnému souboru `NORTHWND.MDF` a klikněte na tlačítko OK. V tuto chvíli by vaše obrazovka měla vypadat podobně jako na obrázku 2.

[![se připojit k příslušné instanci databáze.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**Obrázek 2**: připojení k příslušné instanci databáze ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png))

> [!NOTE]
> Při připojování k instanci SQL Server 2005 Express Edition přes Management Studio dialogové okno připojit databáze vám neumožňuje přejít k podrobnostem o adresářích profilu uživatele, jako jsou dokumenty. Proto nezapomeňte umístit `NORTHWND.MDF` a `NORTHWND_log.LDF` soubory do adresáře profilu, který není profil uživatele.

Kliknutím na tlačítko OK připojte databázi. Dialogové okno připojit databáze bude zavřeno a Průzkumník objektů by nyní měl zobrazit databázi s pouhou připojením. Je pravděpodobné, že databáze Northwind má název, jako `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`. Přejmenujte databázi na Northwind tak, že kliknete pravým tlačítkem na databázi a zvolíte přejmenovat.

![Přejmenujte databázi na Northwind.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**Obrázek 3**: Přejmenování databáze na Northwind

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>Krok 2: vytvoření nového řešení a SQL Server projektu v aplikaci Visual Studio

Pokud chcete vytvořit spravované uložené procedury nebo UDF v SQL Server 2005, zapíšeme uloženou proceduru a logiku UDF jako kód Visual Basic ve třídě. Po zapsání kódu budeme muset zkompilovat tuto třídu do sestavení (`.dll` soubor), zaregistrovat sestavení s databází SQL Server a pak vytvořit uloženou proceduru nebo objekt UDF v databázi, který odkazuje na odpovídající metodu v sestavení. Tyto kroky je možné provést ručně. Kód můžeme vytvořit v libovolném textovém editoru, zkompilovat ho z příkazového řádku pomocí kompilátoru Visual Basic (`vbc.exe`), zaregistrovat ho v databázi pomocí příkazu [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) nebo Management Studio a přidat uloženou proceduru nebo objekt UDF prostřednictvím podobných prostředků. Verze Professional a Team Systems sady Visual Studio naštěstí obsahují SQL Server typ projektu, který automatizuje tyto úlohy. V tomto kurzu provedeme použití typu projektu SQL Server k vytvoření spravované uložené procedury a systému souborů UDF.

> [!NOTE]
> Pokud používáte Visual Web Developer nebo edici Standard sady Visual Studio, budete muset místo toho použít ruční přístup. Krok 13 poskytuje podrobné pokyny k provedení těchto kroků ručně. Doporučujeme, abyste si přečetli kroky 2 až 12 před čtením kroku 13, protože tyto kroky zahrnují důležité pokyny ke konfiguraci SQL Server, které je nutné použít bez ohledu na to, jakou verzi sady Visual Studio používáte.

Začněte otevřením sady Visual Studio. V nabídce soubor klikněte na položku Nový projekt. zobrazí se dialogové okno Nový projekt (viz obrázek 4). Přejděte k podrobnostem o typu projektu databáze a potom ze šablon uvedených na pravé straně zvolte vytvoření nového projektu SQL Server. Zvolil (a) jsem název tohoto projektu `ManagedDatabaseConstructs` a umístili do řešení s názvem `Tutorial75`.

[![vytvoření nového projektu SQL Server](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**Obrázek 4**: vytvoření nového projektu SQL Server ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png))

Kliknutím na tlačítko OK v dialogovém okně Nový projekt vytvořte řešení a SQL Server projekt.

SQL Server projekt je svázán s konkrétní databází. V důsledku toho po vytvoření nového SQL Server projektu se hned zobrazí výzva k zadání těchto informací. Obrázek 5 zobrazuje dialogové okno Nový odkaz na databázi, které bylo vyplněné tak, aby odkazovalo na databázi Northwind, kterou jsme zaregistrovali v SQL Server 2005 Express Edition instance databáze v kroku 1.

![Přidružit SQL Server projekt k databázi Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**Obrázek 5**: přidružení SQL Server projektu k databázi Northwind

Aby bylo možné ladit spravované uložené procedury a UDF, vytvoříme v rámci tohoto projektu podporu ladění SQL/CLR pro toto připojení. Pokaždé, když se přiřadí SQL Server projekt k nové databázi (jako na obrázku 5), Visual Studio se zeptá, jestli chceme povolit ladění SQL/CLR na připojení (viz obrázek 6). Klikněte na možnost Ano.

![Povolit ladění SQL/CLR](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**Obrázek 6**: povolení ladění SQL/CLR

V tomto okamžiku byl do řešení přidán nový projekt SQL Server. Obsahuje složku s názvem `Test Scripts` se souborem s názvem `Test.sql`, který se používá pro ladění objektů spravované databáze, které byly vytvořeny v projektu. Podíváme se na ladění v kroku 12.

Nyní můžeme do tohoto projektu přidat nové spravované uložené procedury a UDF, ale před tím, než začneme, bude nejdřív zahrnovat naši existující webovou aplikaci do řešení. V nabídce soubor vyberte možnost Přidat a zvolte možnost existující web. Přejděte do příslušné složky webu a klikněte na OK. Jak ukazuje obrázek 7, aktualizuje řešení tak, aby zahrnovalo dva projekty: web a `ManagedDatabaseConstructs` SQL Server projektu.

![Průzkumník řešení teď obsahuje dva projekty.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**Obrázek 7**: Průzkumník řešení nyní obsahuje dva projekty

Hodnota `NORTHWNDConnectionString` v `Web.config` aktuálně odkazuje na soubor `NORTHWND.MDF` ve složce `App_Data`. Vzhledem k tomu, že jsme tuto databázi odebrali z `App_Data` a explicitně ji zaregistrovali v instanci databáze SQL Server 2005 Express Edition, musíme odpovídajícím způsobem aktualizovat hodnotu `NORTHWNDConnectionString`. Otevřete `Web.config` soubor na webu a změňte hodnotu `NORTHWNDConnectionString` tak, aby řetězec připojení četl: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`. Po této změně by oddíl `<connectionStrings>` v `Web.config` měl vypadat nějak takto:

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> Jak je popsáno v [předchozím kurzu](debugging-stored-procedures-vb.md), při ladění SQL Serverho objektu z klientské aplikace, jako je například web ASP.NET, musíme sdružování připojení vypnout. Připojovací řetězec, který je zobrazen výše, zakáže sdružování připojení (`Pooling=false`). Pokud neplánujete ladění spravovaných uložených procedur a UDF z webu ASP.NET, povolte sdružování připojení.

## <a name="step-3-creating-a-managed-stored-procedure"></a>Krok 3: vytvoření spravované uložené procedury

Chcete-li přidat spravovanou uloženou proceduru do databáze Northwind, nejprve je třeba vytvořit uloženou proceduru jako metodu v projektu SQL Server. Z Průzkumník řešení klikněte pravým tlačítkem myši na název projektu `ManagedDatabaseConstructs` a vyberte možnost Přidat novou položku. Tím se zobrazí dialogové okno Přidat novou položku, ve kterém jsou uvedeny typy objektů spravované databáze, které lze přidat do projektu. Jak ukazuje obrázek 8, zahrnuje uložené procedury a uživatelsky definované funkce mimo jiné.

Nechte začít tím, že přidáte uloženou proceduru, která jednoduše vrátí všechny produkty, které byly ukončeny. Pojmenujte nový soubor uložené procedury `GetDiscontinuedProducts.vb`.

[![přidat novou uloženou proceduru s názvem GetDiscontinuedProducts. vb](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**Obrázek 8**: přidejte novou uloženou proceduru s názvem `GetDiscontinuedProducts.vb` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png)

Tím se vytvoří nový soubor třídy Visual Basic s následujícím obsahem:

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

Všimněte si, že uložená procedura je implementována jako metoda `Shared` v souboru `Partial` třídy s názvem `StoredProcedures`. Kromě toho je metoda `GetDiscontinuedProducts` upravena pomocí [atributu`SqlProcedure`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx), který označuje metodu jako uloženou proceduru.

Následující kód vytvoří objekt `SqlCommand` a nastaví jeho `CommandText` na `SELECT` dotaz, který vrátí všechny sloupce z tabulky `Products` pro produkty, jejichž `Discontinued` pole se rovná 1. Pak provede příkaz a pošle výsledky zpátky do klientské aplikace. Přidejte tento kód do metody `GetDiscontinuedProducts`.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

Všechny objekty spravované databáze mají přístup k [objektu`SqlContext`](https://msdn.microsoft.com/library/ms131108.aspx) , který představuje kontext volajícího. `SqlContext` poskytuje přístup k [objektu`SqlPipe`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) prostřednictvím jeho [vlastnosti`Pipe`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx). Tento objekt `SqlPipe` slouží k trajektování informací mezi databází SQL Server a volající aplikací. Jak uvádí název, [metoda`ExecuteAndSend`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) spustí předaný `SqlCommand` objekt a vrátí výsledky zpět do klientské aplikace.

> [!NOTE]
> Objekty spravované databáze jsou nejvhodnější pro uložené procedury a UDF, které používají procedurální logiku, nikoli logiku založenou na sadě. Procesní logika zahrnuje práci se sadami dat pro jednotlivé řádky nebo práci s skalárními daty. Metoda `GetDiscontinuedProducts`, kterou jsme právě vytvořili, ale nezahrnuje žádnou procesní logiku. Proto by se ideálním způsobem implementoval jako uložená procedura T-SQL. Je implementován jako spravovaná uložená procedura k předvedení kroků potřebných pro vytváření a nasazování spravovaných uložených procedur.

## <a name="step-4-deploying-the-managed-stored-procedure"></a>Krok 4: nasazení spravované uložené procedury

Po dokončení tohoto kódu jsme připraveni ho nasadit do databáze Northwind. Nasazení SQL Server projektu zkompiluje kód do sestavení, zaregistruje sestavení s databází a vytvoří odpovídající objekty v databázi a propojí je s odpovídajícími metodami v sestavení. Přesná sada úloh prováděných možností nasadit je přesnější napsaný v kroku 13. Klikněte pravým tlačítkem na název projektu `ManagedDatabaseConstructs` v Průzkumník řešení a vyberte možnost nasadit. Nasazení ale neproběhne úspěšně s následující chybou: Nesprávná syntaxe poblíž textu EXTERNAL. Abyste tuto funkci mohli povolit, možná budete muset nastavit úroveň kompatibility aktuální databáze na vyšší hodnotu. `sp_dbcmptlevel`uložené procedury najdete v nápovědě.

Tato chybová zpráva se zobrazí při pokusu o registraci sestavení s databází Northwind. Aby bylo možné zaregistrovat sestavení s databází SQL Server 2005, musí být úroveň kompatibility databáze s nastavená na 90. Ve výchozím nastavení mají nové databáze SQL Server 2005 úroveň kompatibility 90. Databáze vytvořené pomocí Microsoft SQL Server 2000 ale mají výchozí úroveň kompatibility 80. Vzhledem k tomu, že databáze Northwind byla zpočátku databáze Microsoft SQL Server 2000, je její úroveň kompatibility aktuálně nastavená na 80 a proto se musí zvýšit na 90, aby bylo možné zaregistrovat objekty spravované databáze.

Pokud chcete aktualizovat úroveň kompatibility databáze s, otevřete nové okno dotazu v Management Studio a zadejte:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

Kliknutím na ikonu spustit na panelu nástrojů spustíte výše uvedený dotaz.

[![aktualizovat úroveň kompatibility databáze Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**Obrázek 9**: aktualizace úrovně kompatibility s databází Northwind ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image17.png))

Po aktualizaci úrovně kompatibility znovu nasaďte SQL Server projekt. Tentokrát by se nasazení mělo dokončit bez chyby.

Vraťte se do SQL Server Management Studio, klikněte pravým tlačítkem na databázi Northwind v Průzkumník objektů a vyberte aktualizovat. Potom přejděte do složky programovatelnost a potom rozbalte složku sestavení. Jak ukazuje obrázek 10, databáze Northwind nyní obsahuje sestavení generované projektem `ManagedDatabaseConstructs`.

![Sestavení ManagedDatabaseConstructs je teď zaregistrované u databáze Northwind.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**Obrázek 10**: sestavení `ManagedDatabaseConstructs` je teď zaregistrované v databázi Northwind.

Rozbalte také složku uložené procedury. Zobrazí se uložená procedura s názvem `GetDiscontinuedProducts`. Tato uložená procedura byla vytvořena procesem nasazení a odkazuje na metodu `GetDiscontinuedProducts` v sestavení `ManagedDatabaseConstructs`. Když je spuštěna uložená procedura `GetDiscontinuedProducts`, je následně spuštěna metoda `GetDiscontinuedProducts`. Vzhledem k tomu, že se jedná o spravovanou uloženou proceduru, nelze ji upravovat pomocí Management Studio (tedy ikonu zámku vedle názvu uložené procedury).

![Uložená procedura GetDiscontinuedProducts je uvedená ve složce uložené procedury.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**Obrázek 11**: uložená procedura `GetDiscontinuedProducts` je uvedena ve složce uložené procedury.

Než budeme volat spravovanou uloženou proceduru, musíme ještě víc vyřešit: databáze je nakonfigurovaná tak, aby zabránila spuštění spravovaného kódu. Ověřte to tak, že otevřete nové okno dotazu a spustíte uloženou proceduru `GetDiscontinuedProducts`. Zobrazí se následující chybová zpráva: provádění kódu uživatele v .NET Framework je zakázáno. Povolte možnost konfigurace s povoleným modulem CLR.

Chcete-li zjistit informace o konfiguraci databáze Northwind, zadejte a spusťte příkaz `exec sp_configure` v okně dotazu. To ukazuje, že nastavení s povoleným modulem CLR je aktuálně nastaveno na hodnotu 0.

[![je nastavení s povoleným modulem CLR aktuálně nastaveno na hodnotu 0.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**Obrázek 12**: nastavení s povoleným modulem CLR je aktuálně nastaveno na hodnotu 0 ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image22.png)

Všimněte si, že každé nastavení konfigurace na obrázku 12 obsahuje čtyři uvedené hodnoty: minimální a maximální hodnoty a konfigurační a běhové hodnoty. Chcete-li aktualizovat konfigurační hodnotu nastavení s povoleným modulem CLR, spusťte následující příkaz:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

Pokud `exec sp_configure` znovu spustíte, uvidíte, že výše uvedený příkaz aktualizoval konfigurační hodnotu s povoleným modulem CLR na hodnotu 1, ale hodnota běhu je stále nastavená na hodnotu 0. Aby tato změna konfigurace mohla mít vliv na tuto změnu, musíme spustit [příkaz`RECONFIGURE`](https://msdn.microsoft.com/library/ms176069.aspx), který nastaví hodnotu spustit na aktuální konfigurační hodnotu. Stačí zadat `RECONFIGURE` v okně dotazu a kliknout na ikonu spustit na panelu nástrojů. Pokud spustíte `exec sp_configure` nyní by se měla zobrazit hodnota 1 pro nastavení konfigurace s povoleným modulem CLR a hodnoty spustit.

Po dokončení konfigurace s povoleným CLR jsme připraveni spustit uloženou proceduru spravovaného `GetDiscontinuedProducts`. V okně dotazu zadejte a spusťte příkaz `exec` `GetDiscontinuedProducts`. Vyvoláním uložené procedury dojde k provedení odpovídajícího spravovaného kódu v metodě `GetDiscontinuedProducts`. Tento kód vydá dotaz `SELECT`, který vrátí všechny produkty, které jsou ukončeny, a vrátí tato data do volající aplikace, která je v této instanci SQL Server Management Studio. Management Studio obdrží tyto výsledky a zobrazí je v okně výsledků.

[![uloženou proceduru GetDiscontinuedProducts vrátí všechny ukončené produkty.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**Obrázek 13**: uložená procedura `GetDiscontinuedProducts` vrátí všechny ukončené produkty ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image25.png)

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>Krok 5: vytváření spravovaných uložených procedur, které přijímají vstupní parametry

Mnoho dotazů a uložených procedur, které jsme vytvořili v těchto kurzech, používá *parametry*. Například v kurzu [vytváření nových uložených procedur pro typovou sadu dat s objekty TableAdapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) jsme vytvořili uloženou proceduru s názvem `GetProductsByCategoryID`, která přijala vstupní parametr s názvem `@CategoryID`. Uložená procedura pak vrátí všechny produkty, jejichž `CategoryID` pole odpovídalo hodnotě zadaného `@CategoryID` parametru.

Chcete-li vytvořit spravovanou uloženou proceduru, která přijímá vstupní parametry, stačí zadat tyto parametry v definici metody s. K ilustraci tohoto můžete přidat další spravovanou uloženou proceduru do projektu `ManagedDatabaseConstructs` s názvem `GetProductsWithPriceLessThan`. Tato spravovaná uložená procedura přijme vstupní parametr udávající cenu a vrátí všechny produkty, jejichž `UnitPrice` pole je menší než hodnota parametru s.

Chcete-li do projektu přidat novou uloženou proceduru, klikněte pravým tlačítkem na název projektu `ManagedDatabaseConstructs` a vyberte možnost Přidat novou uloženou proceduru. Pojmenujte soubor `GetProductsWithPriceLessThan.vb`. Jak jsme viděli v kroku 3, vytvoří se nový soubor Visual Basic třídy s metodou pojmenovanou `GetProductsWithPriceLessThan` umístěnou v `StoredProcedures``Partial` třídy.

Aktualizujte definici `GetProductsWithPriceLessThan` metody s tak, aby přijímala [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) vstupní parametr s názvem `price` a napsali kód, který se má provést, a vrátí výsledky dotazu:

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

Definice a kód metody `GetProductsWithPriceLessThan` se úzce podobá definici a kódu metody `GetDiscontinuedProducts` vytvořené v kroku 3. Jediným rozdílem je, že metoda `GetProductsWithPriceLessThan` akceptuje jako vstupní parametr (`price`), dotaz `SqlCommand` s obsahuje parametr (`@MaxPrice`) a parametr se přidá do `SqlCommand` kolekce `Parameters` s a přiřadí hodnotu `price` proměnné.

Po přidání tohoto kódu znovu nasaďte SQL Server projekt. Potom se vraťte do SQL Server Management Studio a aktualizujte složku uložených procedur. Měla by se zobrazit nová položka `GetProductsWithPriceLessThan`. V okně dotazu zadejte a spusťte příkaz `exec GetProductsWithPriceLessThan 25`, který zobrazí seznam všech produktů nižších než $25, jak ukazuje obrázek 14.

[Zobrazí se ![produkty pod $25.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**Obrázek 14**: zobrazí se produkty pod $25 ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png)).

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>Krok 6: volání spravované uložené procedury z vrstvy přístupu k datům

V tuto chvíli jsme přidali `GetDiscontinuedProducts` a `GetProductsWithPriceLessThan` spravované uložené procedury do projektu `ManagedDatabaseConstructs` a zaregistrovali je pomocí databáze Northwind SQL Server. Tyto spravované uložené procedury jsme vyvolali také z SQL Server Management Studio (viz obrázek 13 a 14). Aby mohla naše aplikace ASP.NET používat tyto spravované uložené procedury, musíme je přidat do vrstev přístupu k datům a obchodní logiky v architektuře. V tomto kroku přidáme dvě nové metody do `ProductsTableAdapter` v datové sadě `NorthwindWithSprocs` typu, která se původně vytvořila v kurzu [vytváření nových uložených procedur pro objekty TableAdapter typových datových sad](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) . V kroku 7 přidáme odpovídající metody do knihoven BLL.

Otevřete `NorthwindWithSprocs` typovou datovou sadu v sadě Visual Studio a začněte přidáním nové metody do `ProductsTableAdapter` s názvem `GetDiscontinuedProducts`. Chcete-li přidat novou metodu do TableAdapter, klikněte pravým tlačítkem myši na název TableAdapter v návrháři a vyberte možnost Přidat dotaz z kontextové nabídky.

> [!NOTE]
> Vzhledem k tomu, že jsme databázi Northwind přesunuli ze složky `App_Data` do instance databáze služby SQL Server 2005 Express Edition, je nutné, aby odpovídající připojovací řetězec v souboru Web. config odrážel tuto změnu. V kroku 2 jsme probrali aktualizaci `NORTHWNDConnectionString` hodnoty v `Web.config`. Pokud jste zapomněli tuto aktualizaci udělat, zobrazí se mu chybová zpráva při přidávání dotazu se nezdařilo. Nelze najít `NORTHWNDConnectionString` připojení pro `Web.config` objektů v dialogovém okně při pokusu o přidání nové metody do TableAdapter. Chcete-li tuto chybu vyřešit, klikněte na tlačítko OK a potom přejděte na `Web.config` a aktualizujte hodnotu `NORTHWNDConnectionString`, jak je popsáno v kroku 2. Pak zkuste metodu znovu přidat do TableAdapter. Tentokrát by měla fungovat bez chyby.

Přidáním nové metody se spustí Průvodce konfigurací dotazu TableAdapter, který jsme v minulých kurzech používali mnohokrát. První krok vás vyzve k zadání způsobu, jakým má TableAdapter přistupovat k databázi: prostřednictvím ad-hoc SQL příkazu nebo prostřednictvím nové nebo existující uložené procedury. Vzhledem k tomu, že už jsme vytvořili a zaregistrovali `GetDiscontinuedProducts` spravovanou uloženou proceduru s databází, zvolte možnost použít existující uloženou proceduru a stiskněte tlačítko Další.

[![zvolit možnost použít existující uloženou proceduru](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**Obrázek 15**: vyberte možnost použít existující uloženou proceduru ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png)

Na další obrazovce se zobrazí výzva pro uloženou proceduru, kterou bude metoda volat. Z rozevíracího seznamu vyberte spravovanou uloženou proceduru `GetDiscontinuedProducts` a stiskněte tlačítko Další.

[![vyberte spravovanou uloženou proceduru GetDiscontinuedProducts.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**Obrázek 16**: vyberte spravovanou uloženou proceduru `GetDiscontinuedProducts` ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png)).

Pak se zobrazí výzva k určení, zda bude uložená procedura vracet řádky, jedinou hodnotu nebo nic. Vzhledem k tomu, že `GetDiscontinuedProducts` vrátí sadu vyřazených produktů, vyberte první možnost (tabulková data) a klikněte na další.

[![výběr možnosti tabulková data](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**Obrázek 17**: vyberte možnost tabulková data ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png)).

Poslední obrazovka průvodce umožňuje zadat použité vzory přístupu k datům a názvy výsledných metod. Ponechte zaškrtnuté obě políčka a pojmenujte metody `FillByDiscontinued` a `GetDiscontinuedProducts`. Kliknutím na Dokončit dokončete průvodce.

[![pojmenovat metody FillByDiscontinued a GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**Obrázek 18**: pojmenování metod `FillByDiscontinued` a `GetDiscontinuedProducts` ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png))

Zopakováním těchto kroků vytvoříte metody s názvem `FillByPriceLessThan` a `GetProductsWithPriceLessThan` v `ProductsTableAdapter` pro `GetProductsWithPriceLessThan` spravovanou uloženou proceduru.

Obrázek 19 ukazuje snímek obrazovky návrháře DataSet po přidání metod do `ProductsTableAdapter` pro `GetDiscontinuedProducts` a `GetProductsWithPriceLessThan` spravované uložené procedury.

[![ProductsTableAdapter zahrnuje nové metody přidané v tomto kroku.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**Obrázek 19**: `ProductsTableAdapter` obsahuje nové metody přidané v tomto kroku ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png)

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>Krok 7: Přidání odpovídajících metod do vrstvy obchodní logiky

Teď, když jsme aktualizovali vrstvu přístupu k datům tak, aby zahrnovala metody pro volání spravovaných uložených procedur přidaných v krocích 4 a 5, musíme přidat odpovídající metody do vrstvy obchodní logiky. Do třídy `ProductsBLLWithSprocs` přidejte následující dvě metody:

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

Obě metody jednoduše volají odpovídající metodu DAL a vracejí instanci `ProductsDataTable`. `DataObjectMethodAttribute` značky nad každou metodou způsobí, že tyto metody budou zahrnuty v rozevíracím seznamu na kartě vybrat v Průvodci přidáním zdroje dat v prvku ObjectDataSource.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>Krok 8: vyvolání spravovaných uložených procedur z prezentační vrstvy

S rozšířenou obchodní logikou a vrstvami přístupu k datům, aby zahrnovaly podporu pro volání `GetDiscontinuedProducts` a `GetProductsWithPriceLessThan` spravovaných uložených procedur, teď můžeme zobrazit výsledky těchto uložených procedur prostřednictvím stránky ASP.NET.

Otevřete stránku `ManagedFunctionsAndSprocs.aspx` ve složce `AdvancedDAL` a z panelu nástrojů přetáhněte prvek GridView do návrháře. Nastavte vlastnost `ID` ovládacího prvku GridView na `DiscontinuedProducts` a ze své inteligentní značky ji navažte na nový prvek ObjectDataSource s názvem `DiscontinuedProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby vyčetl data z `ProductsBLLWithSprocs` třídy s `GetDiscontinuedProducts` metody.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLLWithSprocs](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**Obrázek 20**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLLWithSprocs` ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png))

[![zvolte metodu GetDiscontinuedProducts z rozevíracího seznamu na kartě vybrat.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**Obrázek 21**: v rozevíracím seznamu na kartě Vybrat vyberte metodu `GetDiscontinuedProducts` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png)

Vzhledem k tomu, že se tato mřížka použije jenom k zobrazení informací o produktu, nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné) a pak klikněte na Dokončit.

Po dokončení průvodce bude Visual Studio automaticky přidávat vlastnost BoundField nebo třídě CheckBoxField podporována pro každé datové pole v `ProductsDataTable`. Chvíli odeberete všechna tato pole s výjimkou `ProductName` a `Discontinued`, na kterých by se měly prvky GridView a ObjectDataSource s deklarativním označením podobat následujícímu:

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

Chvíli počkejte, než tuto stránku zobrazíte v prohlížeči. Při návštěvě stránky prvek ObjectDataSource volá metodu `ProductsBLLWithSprocs` třídy s `GetDiscontinuedProducts`. Jak jsme viděli v kroku 7, tato metoda volá do `GetDiscontinuedProducts` metody DAL s `ProductsDataTable` třídy s, která vyvolá uloženou proceduru `GetDiscontinuedProducts`. Tato uložená procedura je spravovaná uložená procedura a spustí kód, který jsme vytvořili v kroku 3, a vrátíte tak ukončené produkty.

Výsledky vracené spravovanou uloženou procedurou jsou zabaleny do `ProductsDataTable`y pomocí DAL a následně vráceny do knihoven BLL, které je pak vrátí do prezentační vrstvy, kde jsou svázány s ovládacím prvek GridView a zobrazeny. Podle očekávání obsahuje mřížka seznam produktů, které byly ukončeny.

[![seznamu ukončených produktů.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**Obrázek 22**: Seznam vyřazených produktů je uveden ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png)).

Pro další postupy přidejte do stránky textové pole a další prvek GridView. Má-li tento prvek GridView Zobrazit produkty menší, než je množství zadané v textovém poli, voláním metody `ProductsBLLWithSprocs` třídy s `GetProductsWithPriceLessThan`.

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>Krok 9: vytvoření a volání T-SQL UDF

Uživatelsky definované funkce nebo UDF jsou objekty databáze, které úzce napodobují sémantiku funkcí v programovacích jazycích. Podobně jako funkce v Visual Basic může UDF zahrnovat proměnlivý počet vstupních parametrů a vracet hodnotu konkrétního typu. Systém UDF může vracet buď skalární data – řetězec, celé číslo a tak dále nebo tabulková data. Pojďme se rychle podívat na oba typy UDF, počínaje verzí UDF, která vrací skalární datový typ.

Následující systém souborů UDF vypočítá odhadovanou hodnotu inventáře pro určitý produkt. Udělá to tak, že převezme tři vstupní parametry – `UnitPrice`, `UnitsInStock`a `Discontinued` hodnoty pro konkrétní produkt a vrátí hodnotu typu `money`. Vypočítá odhadovanou hodnotu inventáře vynásobením `UnitPrice` `UnitsInStock`. U ukončených položek je tato hodnota poloviční.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

Až bude tato UDF přidána do databáze, dá se najít prostřednictvím Management Studio rozšířením složky pro programovatelnost, funkce a pak funkcí skalární hodnoty. Dá se použít v `SELECT`ch dotazech, jako je například:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

Přidal (a) jsem `udf_ComputeInventoryValue` UDF do databáze Northwind; Obrázek 23 zobrazuje výstup výše uvedeného dotazu `SELECT` při zobrazení prostřednictvím Management Studio. Také si všimněte, že systém souborů UDF je uveden ve složce funkce skalárních hodnot v Průzkumník objektů.

[![jsou uvedené všechny hodnoty inventáře produktů s produktem.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**Obrázek 23**: v seznamu jsou uvedeny všechny hodnoty inventáře produktu s. ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png)

UDF může také vracet tabulková data. Můžete například vytvořit systém souborů UDF, který vrátí produkty patřící do konkrétní kategorie:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

`udf_GetProductsByCategoryID` UDF akceptuje vstupní parametr `@CategoryID` a vrátí výsledky zadaného `SELECT`ho dotazu. Po vytvoření může být tato UDF odkazována v klauzuli `FROM` (nebo `JOIN`) dotazu `SELECT`. Následující příklad vrátí hodnoty `ProductID`, `ProductName`a `CategoryID` pro jednotlivé nápoje.

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

Přidal (a) jsem `udf_GetProductsByCategoryID` UDF do databáze Northwind; Obrázek 24 zobrazuje výstup výše uvedeného dotazu `SELECT` při zobrazení prostřednictvím Management Studio. UDF, které vracejí tabulková data, lze nalézt ve složce funkce Průzkumník objektů s tabulkou hodnota.

[pro každý nápoj se uvádí ![ProductID, NázevVýrobku a KódKategorie.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**Obrázek 24**: `ProductID`, `ProductName`a `CategoryID` jsou uvedeny pro každé nápoje ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png)).

> [!NOTE]
> Další informace o vytvoření a použití UDF najdete v [úvodu k uživatelsky definovaným funkcím](http://www.sqlteam.com/item.asp?ItemID=1955). Podívejte se také na [výhody a nevýhody uživatelsky definovaných funkcí](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1).

## <a name="step-10-creating-a-managed-udf"></a>Krok 10: vytvoření spravovaného systému souborů UDF

`udf_ComputeInventoryValue` a `udf_GetProductsByCategoryID` UDF vytvořené v předchozích příkladech jsou objekty databáze T-SQL. SQL Server 2005 také podporuje spravované UDF, které lze přidat do projektu `ManagedDatabaseConstructs` stejným způsobem jako spravované uložené procedury z kroků 3 a 5. V tomto kroku umožníme implementovat `udf_ComputeInventoryValue` UDF ve spravovaném kódu.

Chcete-li do projektu `ManagedDatabaseConstructs` přidat spravovanou systém souborů UDF, klikněte pravým tlačítkem myši na název projektu v Průzkumník řešení a vyberte možnost Přidat novou položku. Vyberte uživatelsky definovanou šablonu v dialogovém okně Přidat novou položku a pojmenujte nový soubor UDF `udf_ComputeInventoryValue_Managed.vb`.

[![přidání nového spravovaného systému souborů UDF do projektu ManagedDatabaseConstructs](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**Obrázek 25**: Přidání nového spravovaného systému souborů UDF do projektu `ManagedDatabaseConstructs` ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png))

Uživatelsky definovaná Šablona funkce vytvoří třídu `Partial` s názvem `UserDefinedFunctions` s metodou, jejíž název je stejný jako název třídy s názvem (`udf_ComputeInventoryValue_Managed`, v této instanci). Tato metoda je upravena pomocí [atributu`SqlFunction`](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx), který označí metodu jako spravovanou systém souborů UDF.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

Metoda `udf_ComputeInventoryValue` aktuálně vrací [objekt`SqlString`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) a nepřijímá žádné vstupní parametry. Musíme aktualizovat definici metody tak, aby přijímala tři vstupní parametry – `UnitPrice`, `UnitsInStock`a `Discontinued` – a vrátí objekt `SqlMoney`. Logika pro výpočet hodnoty inventáře je stejná jako v T-SQL `udf_ComputeInventoryValue` UDF.

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

Všimněte si, že vstupní parametry metody UDF s jsou odpovídající typy SQL: `SqlMoney` pro pole `UnitPrice`, [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) pro `UnitsInStock`a [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) pro `Discontinued`. Tyto datové typy reflektují typy definované v `Products` tabulce: `UnitPrice` sloupec je typu `money`, `UnitsInStock` sloupec typu `smallint`a `Discontinued` sloupec typu `bit`.

Kód začíná vytvořením instance `SqlMoney` s názvem `inventoryValue`, která je přiřazena hodnota 0. Tabulka `Products` povoluje hodnoty `NULL` databáze ve sloupcích `UnitsInPrice` a `UnitsInStock`. Proto musíme nejdřív projít, abyste zjistili, jestli tyto hodnoty obsahují `NULL` s, což provedeme prostřednictvím vlastnosti `SqlMoney` Object s [`IsNull`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx). Pokud `UnitPrice` i `UnitsInStock` obsahují hodnoty, které nejsou`NULL`, vypočítáme `inventoryValue`, aby to byl produkt těchto dvou. Pokud `Discontinued` má hodnotu true, pak se hodnota zkrátí.

> [!NOTE]
> Objekt `SqlMoney` umožňuje vynásobit dvě instance `SqlMoney`. Neumožňuje vynásobení instance `SqlMoney` literálem v číslu s plovoucí desetinnou čárkou. Proto pokud chcete poloviční `inventoryValue` vynásobit novou instancí `SqlMoney`, která má hodnotu 0,5.

## <a name="step-11-deploying-the-managed-udf"></a>Krok 11: nasazení spravovaného systému souborů UDF

Teď, když se vytvořila spravovaná UDF, jsme připraveni ji nasadit do databáze Northwind. Jak jsme viděli v kroku 4, spravované objekty v SQL Server projektu se nasadí kliknutím pravým tlačítkem myši na název projektu v Průzkumník řešení a zvolením možnosti nasadit z kontextové nabídky.

Po nasazení projektu se vraťte k SQL Server Management Studio a aktualizujte složku funkcí skalárního vyhodnotit. Nyní byste měli vidět dvě položky:

- `dbo.udf_ComputeInventoryValue` – systém souborů n-SQL UDF vytvořený v kroku 9 a
- `dbo.udf ComputeInventoryValue_Managed` – spravovaná UDF vytvořená v kroku 10, který jste právě nasadili.

K otestování tohoto spravovaného systému souborů UDF spusťte následující dotaz v rámci Management Studio:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

Tento příkaz používá místo sady T-SQL `udf_ComputeInventoryValue` UDF spravovaný `udf ComputeInventoryValue_Managed` UDF, ale výstup je stejný. Přejděte zpět na obrázek 23 a zobrazte snímek obrazovky s výstupem ve formátu UDF.

## <a name="step-12-debugging-the-managed-database-objects"></a>Krok 12: ladění objektů spravované databáze

V kurzu [ladění uložených procedur](debugging-stored-procedures-vb.md) jsme probrali tři možnosti pro ladění SQL Server prostřednictvím sady Visual Studio: přímé ladění databáze, ladění aplikace a ladění z projektu SQL Server. Spravované objekty databáze nelze ladit prostřednictvím přímého ladění databáze, ale lze je ladit z klientské aplikace a přímo z SQL Server projektu. Aby ladění fungovalo, musí však databáze SQL Server 2005 umožňovat ladění SQL/CLR. Načtěte si, že když jsme poprvé vytvořili `ManagedDatabaseConstructs` projektu Visual Studio, bylo požádáno, jestli jsme chtěli povolit ladění SQL/CLR (viz obrázek 6 v kroku 2). Toto nastavení lze upravit kliknutím pravým tlačítkem myši na databázi z okna Průzkumník serveru.

![Ujistěte se, že databáze umožňuje ladění SQL/CLR.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**Obrázek 26**: Ujistěte se, že databáze umožňuje ladění SQL/CLR.

Představte si, že jsme chtěli ladit `GetProductsWithPriceLessThan` spravovanou uloženou proceduru. Začneme nastavením zarážky v kódu metody `GetProductsWithPriceLessThan`.

[![nastavit zarážku v metodě GetProductsWithPriceLessThan](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**Obrázek 27**: nastavení zarážky v metodě `GetProductsWithPriceLessThan` ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png))

Pojďme se nejdřív podívat na ladění objektů spravované databáze z SQL Server projektu. Vzhledem k tomu, že naše řešení obsahuje dva projekty – `ManagedDatabaseConstructs` SQL Server projektu společně s naším webem – aby bylo možné ladit z SQL Server projektu, musíme aplikaci Visual Studio, aby při zahájení ladění spouštěla projekt `ManagedDatabaseConstructs` SQL Server. V Průzkumník řešení klikněte pravým tlačítkem na projekt `ManagedDatabaseConstructs` a v místní nabídce vyberte možnost nastavit jako spouštěný projekt.

Při spuštění projektu `ManagedDatabaseConstructs` z ladicího programu se spustí příkazy SQL v souboru `Test.sql`, který je umístěn ve složce `Test Scripts`. Chcete-li například otestovat `GetProductsWithPriceLessThan` spravovanou uloženou proceduru, nahraďte existující `Test.sql` obsah souboru následujícím příkazem, který vyvolá `GetProductsWithPriceLessThan` spravovanou uloženou proceduru procházející v `@CategoryID` hodnotě 14,95:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

Po zadání výše uvedeného skriptu do `Test.sql`spusťte ladění, a to tak, že v nabídce ladění kliknete na možnost Spustit ladění, nebo na panelu nástrojů na ikonu zeleného přehrávání. Tím se sestaví projekty v rámci řešení, nasadíte objekty spravované databáze do databáze Northwind a potom spustíte skript `Test.sql`. V tomto okamžiku bude dosaženo zarážky a můžeme Krokovat s metodou `GetProductsWithPriceLessThan`, prozkoumávat hodnoty vstupních parametrů a tak dále.

[Bylo dosaženo ![zarážky v metodě GetProductsWithPriceLessThan.](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**Obrázek 28**: bylo dosaženo zarážky v metodě `GetProductsWithPriceLessThan` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png)

Aby bylo možné objekt databáze SQL ladit prostřednictvím klientské aplikace, je nezbytné, aby byla databáze nakonfigurována pro podporu ladění aplikace. V Průzkumník serveru klikněte pravým tlačítkem na databázi a ujistěte se, že je zaškrtnutá možnost ladění aplikace. Kromě toho musíme nakonfigurovat aplikaci ASP.NET pro integraci s ladicím programem SQL a zakázat sdružování připojení. Tyto kroky byly podrobněji popsány v kroku 2 v kurzu [ladění uložených procedur](debugging-stored-procedures-vb.md) .

Po nakonfigurování aplikace a databáze ASP.NET nastavte web ASP.NET jako spouštěný projekt a spusťte ladění. Pokud navštívíte stránku, která volá jeden ze spravovaných objektů, které mají zarážku, aplikace se zastaví a ovládací prvek se přesměruje na ladicí program, kde můžete krokovat kód, jak je znázorněno na obrázku 28.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>Krok 13: ruční kompilace a nasazování spravovaných databázových objektů

SQL Server projekty usnadňují vytváření, kompilování a nasazování spravovaných databázových objektů. SQL Server projekty jsou však k dispozici pouze v edicích Professional a Team Systems sady Visual Studio. Pokud používáte Visual Web Developer nebo edici Standard sady Visual Studio a chcete používat spravované databázové objekty, budete je muset vytvořit a nasadit ručně. Zahrnuje čtyři kroky:

1. Vytvořte soubor, který obsahuje zdrojový kód objektu Managed Database.
2. Zkompilujte objekt do sestavení,
3. Zaregistrujte sestavení pomocí databáze SQL Server 2005 a
4. Vytvořte objekt databáze v SQL Server, který odkazuje na příslušnou metodu v sestavení.

K ilustraci těchto úloh vytvoříme novou spravovanou uloženou proceduru, která vrátí tyto produkty, jejichž `UnitPrice` je větší než zadaná hodnota. V počítači vytvořte nový soubor s názvem `GetProductsWithPriceGreaterThan.vb` a do souboru zadejte následující kód (k tomu můžete použít Visual Studio, Poznámkový blok nebo libovolný textový editor):

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

Tento kód je skoro totožný s metodou `GetProductsWithPriceLessThan` vytvořenou v kroku 5. Jediným rozdílem jsou názvy metod, klauzuli `WHERE` a název parametru použitý v dotazu. Zpět v metodě `GetProductsWithPriceLessThan`, klauzule `WHERE` Read: `WHERE UnitPrice < @MaxPrice`. V `GetProductsWithPriceGreaterThan`používáme: `WHERE UnitPrice > @MinPrice`.

Teď je potřeba tuto třídu zkompilovat do sestavení. Z příkazového řádku přejděte do adresáře, kam jste uložili soubor `GetProductsWithPriceGreaterThan.vb` a použijte C# kompilátor (`csc.exe`) pro zkompilování souboru třídy do sestavení:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

Pokud složka obsahující v `bc.exe` není v `PATH`systému, budete muset plně odkazovat na svou cestu, `%WINDOWS%\Microsoft.NET\Framework\version\`, například:

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]

[![zkompilovat GetProductsWithPriceGreaterThan. vb do sestavení](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**Obrázek 29**: kompilace `GetProductsWithPriceGreaterThan.vb` do sestavení ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png))

Příznak `/t` určuje, že soubor Visual Basic třídy by měl být zkompilován do knihovny DLL (spíše než do spustitelného souboru). Příznak `/out` Určuje název výsledného sestavení.

> [!NOTE]
> Místo kompilace souboru `GetProductsWithPriceGreaterThan.vb` třídy z příkazového řádku můžete alternativně použít [Visual Basic Express Edition](https://msdn.microsoft.com/vstudio/express/vb/) nebo vytvořit samostatný projekt knihovny tříd v aplikaci Visual Studio Standard Edition. S Ren Jacob Lauritsen poskytla jako takový projekt Visual Basic Express Edition kód pro uloženou proceduru `GetProductsWithPriceGreaterThan` a dva spravované uložené procedury a soubory UDF vytvořené v krocích 3, 5 a 10. Projekt s Ren s obsahuje také příkazy T-SQL potřebné k přidání odpovídajících databázových objektů.

S kódem kompilovaným do sestavení je připraveno zaregistrovat sestavení v rámci databáze SQL Server 2005. To lze provést prostřednictvím T-SQL pomocí příkazu `CREATE ASSEMBLY`nebo prostřednictvím SQL Server Management Studio. Zaměřte se na používání Management Studio.

V Management Studio rozbalte složku programovatelnost v databázi Northwind. Jedna z jejích podsložek je sestavení. Chcete-li do databáze ručně přidat nové sestavení, klikněte pravým tlačítkem na složku Assemblies a v místní nabídce vyberte možnost nové sestavení. Tím se zobrazí dialogové okno nové sestavení (viz obrázek 30). Klikněte na tlačítko Procházet, vyberte `ManuallyCreatedDBObjects.dll` sestavení, které jsme právě shromáždili, a potom kliknutím na tlačítko OK přidejte sestavení do databáze. V Průzkumník objektů byste neměli vidět `ManuallyCreatedDBObjects.dll` sestavení.

[![do databáze přidat sestavení ManuallyCreatedDBObjects. dll](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**Obrázek 30**: přidání sestavení `ManuallyCreatedDBObjects.dll` do databáze ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png))

![ManuallyCreatedDBObjects. dll je uveden v Průzkumník objektů](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**Obrázek 31**: `ManuallyCreatedDBObjects.dll` je uveden v Průzkumník objektů

I když jsme přidali sestavení do databáze Northwind, ještě jsme přiřadili uloženou proceduru s metodou `GetProductsWithPriceGreaterThan` v sestavení. Chcete-li to provést, otevřete nové okno dotazu a spusťte následující skript:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

Tím se vytvoří nová uložená procedura v databázi Northwind s názvem `GetProductsWithPriceGreaterThan` a přidruží ji k spravované metodě `GetProductsWithPriceGreaterThan` (která je ve třídě `StoredProcedures`, která je v `ManuallyCreatedDBObjects`sestavení).

Po provedení výše uvedeného skriptu aktualizujte složku uložené procedury v Průzkumník objektů. Měla by se zobrazit nová uložená procedura entry-`GetProductsWithPriceGreaterThan` – s ikonou zámku vedle ní. Chcete-li tuto uloženou proceduru otestovat, zadejte a spusťte následující skript v okně dotazu:

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

Jak ukazuje obrázek 32, výše uvedený příkaz zobrazí informace o těchto produktech s `UnitPrice` větší než $24,95.

[![knihovna ManuallyCreatedDBObjects. dll je uvedena v Průzkumník objektů](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**Obrázek 32**: `ManuallyCreatedDBObjects.dll` je uveden v Průzkumník objektů ([kliknutím zobrazíte obrázek v plné velikosti](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png)).

## <a name="summary"></a>Přehled

Microsoft SQL Server 2005 poskytuje integraci s modulem CLR (Common Language Runtime), který umožňuje vytváření databázových objektů pomocí spravovaného kódu. Dřív se tyto objekty databáze daly vytvořit jenom pomocí T-SQL, ale teď můžeme tyto objekty vytvořit pomocí programovacích jazyků .NET, jako je Visual Basic. V tomto kurzu jsme vytvořili dva spravované uložené procedury a spravované uživatelsky definované funkce.

Visual Studio s SQL Server typ projektu usnadňuje vytváření, kompilování a nasazování spravovaných databázových objektů. Navíc nabízí bohatou podporu ladění. SQL Server typy projektů jsou však k dispozici pouze v edicích Professional a Team Systems sady Visual Studio. Pro ty, které používají Visual Web Developer nebo edici Standard sady Visual Studio, je nutné provést kroky vytvoření, kompilace a nasazení ručně, jak jsme viděli v kroku 13.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Výhody a nevýhody uživatelem definovaných funkcí](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [Vytváření objektů SQL Server 2005 ve spravovaném kódu](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Vytváření aktivačních událostí pomocí spravovaného kódu v SQL Server 2005](http://www.15seconds.com/issue/041006.htm)
- [Postupy: vytvoření a spuštění uložené procedury modulu CLR SQL Server](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [Postupy: vytvoření a spuštění funkce CLR SQL Server uživatelsky definované funkci](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [Postupy: úprava skriptu `Test.sql` pro spouštění objektů SQL](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [Úvod do uživatelem definovaných funkcí](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Spravovaný kód a SQL Server 2005 (video)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Referenční dokumentace jazyka Transact-SQL](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [Návod: vytvoření uložené procedury ve spravovaném kódu](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor potenciálních zákazníků pro tento kurz byl S Ren Jacob Lauritsen. Kromě toho, že tento článek obsahuje, je k dispozici také C# projekt Visual Express Edition, který je součástí tohoto článku ke stažení, aby bylo možné ručně kompilovat objekty spravované databáze. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](debugging-stored-procedures-vb.md)
