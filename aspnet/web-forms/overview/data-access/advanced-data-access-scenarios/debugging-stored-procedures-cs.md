---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
title: Ladění uložených procedur (C#) | Microsoft Docs
author: rick-anderson
description: Edice Visual Studio Professional a Team System umožňují nastavit zarážky a krokovat s tím, že se v rámci SQL Server nastavují uložené procedury a ladění se uloží...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: c655c324-2ffa-4c21-8265-a254d79a693d
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
msc.type: authoredcontent
ms.openlocfilehash: 12a8500b107345b9cc9ab457016fdef09ca1bb9d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74604866"
---
# <a name="debugging-stored-procedures-c"></a>Ladění uložených procedur (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_CS.zip) nebo [stažení PDF](debugging-stored-procedures-cs/_static/datatutorial74cs1.pdf)

> Edice Visual Studio Professional a Team System umožňují nastavit zarážky a krokovat s tím, že se v rámci SQL Server nastavují uložené procedury a budou ladit uložené procedury stejně snadné jako ladit kód aplikace. Tento kurz ukazuje přímé ladění databáze a ladění aplikací uložených procedur.

## <a name="introduction"></a>Úvod

Visual Studio poskytuje bohatou ladicí prostředí. S několika úhozy stisknutými klávesami nebo kliknutím na myš lze pomocí zarážek zastavit provádění programu a prozkoumávat jeho stav a tok řízení. Spolu s laděním kódu aplikace nabízí Visual Studio podporu pro ladění uložených procedur z SQL Server. Stejně jako zarážky lze nastavit v rámci kódu třídy ASP.NET kódu na pozadí nebo třídy vrstvy obchodní logiky, takže je možné je také umístit v uložených procedurách.

V tomto kurzu se podíváme na kroky do uložených procedur z Průzkumník serveru v sadě Visual Studio a také na postup nastavení zarážek, které jsou dosaženy při volání uložené procedury z běžící aplikace ASP.NET.

> [!NOTE]
> Uložené procedury lze bohužel využít pouze ve verzích Professional a Team Systems sady Visual Studio. Pokud používáte Visual Web Developer nebo standardní verzi sady Visual Studio, budete připraveni si přečíst spolu s postupem, který je nezbytný pro ladění uložených procedur, ale tyto kroky nebude možné replikovat na vašem počítači.

## <a name="sql-server-debugging-concepts"></a>Koncepty ladění SQL Server

Microsoft SQL Server 2005 byla navržena tak, aby poskytovala integraci s modulem [CLR (Common Language Runtime)](https://msdn.microsoft.com/netframework/aa497266.aspx), což je modul runtime používaný všemi sestaveními .NET. V důsledku toho SQL Server 2005 podporuje objekty spravované databáze. To znamená, že můžete vytvořit databázové objekty, jako jsou uložené procedury a uživatelsky definované funkce (UDF) jako metody C# ve třídě. To umožňuje těmto uloženým procedurám a UDF využívat funkce v .NET Framework a z vlastních tříd. Samozřejmě SQL Server 2005 také poskytuje podporu pro objekty databáze T-SQL.

SQL Server 2005 nabízí podporu ladění pro objekty T-SQL i pro objekty spravované databáze. Tyto objekty se ale dají ladit jenom v edicích Visual Studio 2005 Professional a Team Systems. V tomto kurzu prověříme ladění objektů databáze T-SQL. V dalším kurzu se podíváme na ladění spravovaných databázových objektů.

[Přehled ladění T-SQL a CLR v položce SQL Server 2005](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx) blogu [integrace SQL Server 2005 CLR](https://blogs.msdn.com/sqlclr/default.aspx) obsahuje tři způsoby, jak ladit SQL Server 2005 objektů ze sady Visual Studio:

- **Přímé ladění databáze (DDD)** – z Průzkumník serveru můžeme Krokovat s libovolným objektem databáze T-SQL, například s uloženými procedurami a UDF. Podíváme se na DDD v kroku 1.
- **Ladění aplikace** – můžeme nastavovat zarážky v rámci objektu databáze a pak spustit naši aplikaci ASP.NET. Při spuštění objektu databáze se zarážka narazí a ovládací prvek se přepnul do ladicího programu. Všimněte si, že při ladění aplikace nemůžeme Krokovat s databázovým objektem z kódu aplikace. Je nutné explicitně nastavit zarážky v těchto uložených procedurách nebo UDF, kde chceme zastavit ladicí program. Ladění aplikace se prozkoumá počínaje krokem 2.
- **Ladění z SQL Server Visual Studio Professional projektů** a týmových systémů zahrnuje SQL Server typ projektu, který se běžně používá k vytváření objektů spravované databáze. Podíváme se na použití projektů SQL Server a ladění obsahu v dalším kurzu.

Visual Studio může ladit uložené procedury na místních a vzdálených SQL Server instancích. Místní instance SQL Server je ta, která je nainstalovaná na stejném počítači jako Visual Studio. Pokud se databáze SQL Server, kterou používáte, nenachází ve vývojovém počítači, je považována za vzdálenou instanci. V těchto kurzech používáme místní instance SQL Server. Ladění uložených procedur ve vzdálené instanci systému SQL Server vyžaduje více kroků konfigurace než při ladění uložených procedur na místní instanci.

Pokud používáte instanci místního SQL Server, můžete začít s krokem 1 a tento kurz vyřešit na konci. Používáte-li instanci vzdáleného SQL Server, budete nejprve muset zajistit, aby při ladění jste přihlášeni k vývojovému počítači pomocí uživatelského účtu systému Windows, který má SQL Server přihlášení na vzdálené instanci. Kromě toho musí být toto přihlášení k databázi i přihlášení databáze používané pro připojení k databázi z běžící aplikace ASP.NET členy role `sysadmin`. Další informace o konfiguraci sady Visual Studio a SQL Server k ladění vzdálené instance naleznete v části ladění T-SQL Database objektů na vzdálených instancích na konci tohoto kurzu.

Nakonec je třeba pochopit, že podpora ladění pro objekty databáze T-SQL není jako podpora ladění pro aplikace .NET jako rozšířená. Například podmínky zarážky a filtry nejsou podporovány, k dispozici je pouze podmnožina ladicích oken, nelze použít příkaz Upravit a pokračovat, okamžité okno je vygenerováno nepoužitelné a tak dále. Další informace najdete v tématu [omezení příkazů a funkcí ladicího programu](https://msdn.microsoft.com/library/ms165035(VS.80).aspx) .

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>Krok 1: přímé krokování do uložené procedury

Visual Studio usnadňuje přímé ladění databázového objektu. Pojďme se podívat na to, jak používat funkci přímého ladění databáze (DDD) ke krokování do `Products_SelectByCategoryID` uložené procedury v databázi Northwind. Jak název naznačuje, `Products_SelectByCategoryID` vrátí informace o produktu pro konkrétní kategorii. byl vytvořen v kurzu [použití existujících uložených procedur pro typový DataSet s objekty TableAdapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) . Začněte tím, že na Průzkumník serveru zahájíte a rozbalíte uzel databáze Northwind. Potom přejděte do složky uložené procedury, klikněte pravým tlačítkem na uloženou proceduru `Products_SelectByCategoryID` a v místní nabídce vyberte možnost krok do uložené procedury. Tím se spustí ladicí program.

Vzhledem k tomu, že `Products_SelectByCategoryID` uložená procedura očekává `@CategoryID` vstupní parametr, zobrazí se výzva k poskytnutí této hodnoty. Zadejte hodnotu 1, která bude vracet informace o nápojích.

![Pro parametr @CategoryID použijte hodnotu 1.](debugging-stored-procedures-cs/_static/image1.png)

**Obrázek 1**: pro parametr `@CategoryID` použijte hodnotu 1.

Po zadání hodnoty parametru `@CategoryID` je uložená procedura spuštěna. Místo spuštění k dokončení, ale ladicí program zastaví provádění prvního příkazu. Poznamenejte si žlutou šipku na okraji a určete aktuální umístění v uložené proceduře. Hodnoty parametrů můžete zobrazit a upravit pomocí okno Kukátko nebo přesunutím ukazatele myši na název parametru v uložené proceduře.

[![, že se ladicí program zastavil v prvním příkazu uložené procedury](debugging-stored-procedures-cs/_static/image3.png)](debugging-stored-procedures-cs/_static/image2.png)

**Obrázek 2**: ladicí program se zastavil v prvním příkazu uložené procedury ([kliknutím zobrazíte obrázek v plné velikosti).](debugging-stored-procedures-cs/_static/image4.png)

Chcete-li postupně procházet uloženou proceduru v jednom příkazu, klikněte na tlačítko krokovat na panelu nástrojů nebo stiskněte klávesu F10. Uložená procedura `Products_SelectByCategoryID` obsahuje jeden příkaz `SELECT`, takže se při stisknutí klávesy F10 pozastaví jediný příkaz a dokončí se spuštění uložené procedury. Po dokončení uložené procedury se její výstup zobrazí v okně výstup a ladicí program skončí.

> [!NOTE]
> Ladění T-SQL probíhá na úrovni příkazu; příkaz `SELECT` nelze krokovat.

## <a name="step-2-configuring-the-website-for-application-debugging"></a>Krok 2: Konfigurace webu pro ladění aplikace

Při ladění uložené procedury přímo z Průzkumník serveru je užitečná, v mnoha scénářích je více zajímáme o ladění uložené procedury při jejím volání z naší aplikace ASP.NET. Do uložené procedury v sadě Visual Studio můžeme přidat zarážky a pak začít ladit aplikaci ASP.NET. Když je z aplikace vyvolána uložená procedura se zarážkami, spuštění se zastaví na zarážce a můžeme zobrazit a změnit hodnoty parametrů uložené procedury a krokovat s jejími příkazy, stejně jako v kroku 1.

Před zahájením ladění uložených procedur volaných z aplikace musíme dát pokyn webové aplikaci ASP.NET, aby byla integrována s ladicím programem SQL Server. Začněte tím, že kliknete pravým tlačítkem na název webu v Průzkumník řešení (`ASPNET_Data_Tutorial_74_CS`). Zvolte možnost stránky vlastností z kontextové nabídky, vyberte položku Možnosti spuštění vlevo a zaškrtněte políčko SQL Server v části ladicí programy (viz obrázek 3).

[![zaškrtněte políčko SQL Server na stránkách vlastností aplikace.](debugging-stored-procedures-cs/_static/image6.png)](debugging-stored-procedures-cs/_static/image5.png)

**Obrázek 3**: zaškrtněte políčko SQL Server na stránkách vlastností aplikace ([kliknutím zobrazíte obrázek v plné velikosti).](debugging-stored-procedures-cs/_static/image7.png)

Kromě toho je potřeba aktualizovat připojovací řetězec databáze, který aplikace používá, aby bylo sdružování připojení zakázané. Při zavření připojení k databázi se odpovídající objekt `SqlConnection` umístí do fondu dostupných připojení. Při navazování připojení k databázi je možné z tohoto fondu načíst dostupný objekt připojení, ale nemusíte vytvářet a navazovat nové připojení. Toto sdružování objektů připojení je vylepšení výkonu a je ve výchozím nastavení povoleno. Nicméně když ladění chceme vypnout sdružování připojení, protože při práci s připojením, které bylo získáno z fondu, není správně znovu navázána infrastruktura ladění.

Pokud chcete zakázat sdružování připojení, aktualizujte `NORTHWNDConnectionString` v `Web.config` tak, aby obsahovalo `Pooling=false` nastavení.

[!code-xml[Main](debugging-stored-procedures-cs/samples/sample1.xml)]

> [!NOTE]
> Po dokončení ladění SQL Server prostřednictvím aplikace ASP.NET Nezapomeňte obnovit sdružování připojení odebráním nastavení `Pooling` z připojovacího řetězce (nebo jeho nastavením na `Pooling=true`).

V tomto okamžiku byla aplikace ASP.NET nakonfigurována tak, aby umožnila aplikaci Visual Studio při vyvolání prostřednictvím webové aplikace ladit objekty databáze SQL Server. Vše, co zbývá nyní, je přidat zarážku do uložené procedury a spustit ladění!

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>Krok 3: Přidání zarážky a ladění

Otevřete uloženou proceduru `Products_SelectByCategoryID` a nastavte zarážku na začátku `SELECT`, a to tak, že kliknete na příslušné místo nebo umístíte kurzor na začátek příkazu `SELECT` a zahájíte F9. Obrázek 4 znázorňuje, že se zarážka zobrazuje v okraji jako červený kroužek.

[![nastavit zarážku v uložené proceduře Products_SelectByCategoryID](debugging-stored-procedures-cs/_static/image9.png)](debugging-stored-procedures-cs/_static/image8.png)

**Obrázek 4**: nastavení zarážky v uložené proceduře `Products_SelectByCategoryID` ([kliknutím zobrazíte obrázek v plné velikosti](debugging-stored-procedures-cs/_static/image10.png))

Aby bylo možné objekt databáze SQL ladit prostřednictvím klientské aplikace, je nezbytné, aby byla databáze nakonfigurována pro podporu ladění aplikace. Když nakonfigurujete zarážku, toto nastavení by mělo být automaticky přepnuto na, ale je obezřetné pro dvojité kontroly. Pravým tlačítkem myši klikněte na uzel `NORTHWND.MDF` v Průzkumník serveru. Místní nabídka by měla obsahovat položku kontrolované nabídky s názvem ladění aplikace.

![Ujistěte se, že je povolená možnost ladění aplikace.](debugging-stored-procedures-cs/_static/image11.png)

**Obrázek 5**: Ujistěte se, že je povolená možnost ladění aplikace.

Když je nastavená zarážka a je povolená možnost ladění aplikace, můžeme při volání z aplikace ASP.NET ladit uloženou proceduru. Spusťte ladicí program tak, že přejdete do nabídky ladění a zvolíte Spustit ladění, když kliknete na F5 nebo na ikonu zeleného přehrávání na panelu nástrojů. Tím se spustí ladicí program a spustí se web.

`Products_SelectByCategoryID` uloženou proceduru se vytvořil v kurzu [použití existujících uložených procedur pro typový DataSet s objekty TableAdapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) . Jeho odpovídající webová stránka (`~/AdvancedDAL/ExistingSprocs.aspx`) obsahuje prvek GridView, který zobrazuje výsledky vrácené touto uloženou procedurou. Navštivte tuto stránku v prohlížeči. Po dosažení stránky bude dosaženo zarážky v uložené proceduře `Products_SelectByCategoryID` a ovládací prvek vrácen do sady Visual Studio. Stejně jako v kroku 1 můžete krokovat s příkazy uložené procedury a zobrazit a upravit hodnoty parametrů.

[![stránce ExistingSprocs. aspx se zpočátku zobrazí nápoje.](debugging-stored-procedures-cs/_static/image13.png)](debugging-stored-procedures-cs/_static/image12.png)

**Obrázek 6**: na stránce `ExistingSprocs.aspx` se zpočátku zobrazují nápoje ([kliknutím zobrazíte obrázek v plné velikosti](debugging-stored-procedures-cs/_static/image14.png)).

[![bylo dosaženo zarážky uložené procedury s.](debugging-stored-procedures-cs/_static/image16.png)](debugging-stored-procedures-cs/_static/image15.png)

**Obrázek 7**: bylo dosaženo zarážky uložené procedury s ([kliknutím zobrazíte obrázek v plné velikosti).](debugging-stored-procedures-cs/_static/image17.png)

Jak ukazuje okno Kukátko na obrázku 7, hodnota parametru `@CategoryID` je 1. Důvodem je, že stránka `ExistingSprocs.aspx` zpočátku zobrazuje produkty v kategorii nápoje, která má `CategoryID` hodnotu 1. Z rozevíracího seznamu vyberte jinou kategorii. To způsobí, že postback a znovu spustí uloženou proceduru `Products_SelectByCategoryID`. Zarážka je znovu navolána, ale tentokrát hodnota parametru `@CategoryID` odráží vybranou položku rozevíracího seznamu `CategoryID`.

[![v rozevíracím seznamu zvolit jinou kategorii](debugging-stored-procedures-cs/_static/image19.png)](debugging-stored-procedures-cs/_static/image18.png)

**Obrázek 8**: v rozevíracím seznamu vyberte jinou kategorii ([kliknutím zobrazíte obrázek v plné velikosti).](debugging-stored-procedures-cs/_static/image20.png)

[![parametr @CategoryID odráží kategorii vybranou z webové stránky.](debugging-stored-procedures-cs/_static/image22.png)](debugging-stored-procedures-cs/_static/image21.png)

**Obrázek 9**: parametr `@CategoryID` odráží kategorii vybranou z webové stránky ([kliknutím zobrazíte obrázek v plné velikosti).](debugging-stored-procedures-cs/_static/image23.png)

> [!NOTE]
> Pokud se zarážka v uložené proceduře `Products_SelectByCategoryID` při návštěvě stránky `ExistingSprocs.aspx` neprojeví, ujistěte se, že je zaškrtnuto políčko SQL Server v části ladicí programy na stránce vlastností aplikace ASP.NET, že sdružování připojení je zakázané a že je povolená možnost ladění aplikace Database s. Pokud stále dochází k problémům, restartujte Visual Studio a zkuste to znovu.

## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>Ladění T-SQL Database objektů na vzdálených instancích

Ladění databázových objektů prostřednictvím sady Visual Studio je poměrně jasné, pokud je instance databáze SQL Server na stejném počítači jako Visual Studio. Pokud se však SQL Server a aplikace Visual Studio nacházejí v různých počítačích, je nutné provést určitou pečlivou konfiguraci, aby vše správně fungovalo. Existují dva základní úlohy:

- Ujistěte se, že přihlášení použité pro připojení k databázi prostřednictvím ADO.NET patří do role `sysadmin`.
- Ujistěte se, že uživatelský účet systému Windows používaný aplikací Visual Studio ve vývojovém počítači je platným přihlašovacím účtem SQL Server, který patří do role `sysadmin`.

První krok je poměrně jednoduchý. Nejdřív identifikujte uživatelský účet použitý k připojení k databázi z aplikace ASP.NET a potom z SQL Server Management Studio přidejte tento přihlašovací účet do role `sysadmin`.

Druhý úkol vyžaduje, aby uživatelský účet systému Windows, který používáte k ladění aplikace, byl platným přihlašovacím jménem na vzdálené databázi. Je ale pravděpodobné, že účet systému Windows, ke kterému jste se přihlásili, není platným přihlašovacím SQL Server. Místo přidání vašeho konkrétního přihlašovacího účtu do SQL Server je vhodnější určit jako účet služby SQL Server ladění nějaký uživatelský účet systému Windows. Chcete-li poté ladit databázové objekty instance vzdálené SQL Server, spusťte sadu Visual Studio s použitím přihlašovacích údajů přihlašovacího účtu systému Windows.

Příkladem může být vyjasnění věcí. Představte si, že v doméně Windows je účet systému Windows s názvem `SQLDebug`. Tento účet by se musel do instance vzdálené SQL Server přidat jako platné přihlášení a jako člen role `sysadmin`. Pokud pak chcete ladit vzdálenou SQL Server instanci ze sady Visual Studio, musíme jako `SQLDebug`ho uživatele spustit Visual Studio. To se dá udělat tak, že se odhlásíte z naší pracovní stanice, přihlásíte se zpátky jako `SQLDebug`a pak spustíte Visual Studio, ale jednodušší přístup se přihlaste k naší pracovní stanici pomocí vlastních přihlašovacích údajů a pak pomocí `runas.exe` spustíte Visual Studio jako `SQLDebug` uživatele. `runas.exe` umožňuje spuštění konkrétní aplikace pod GUI jiného uživatelského účtu. Chcete-li spustit aplikaci Visual Studio jako `SQLDebug`, můžete do příkazového řádku zadat následující příkaz:

[!code-console[Main](debugging-stored-procedures-cs/samples/sample2.cmd)]

Podrobnější vysvětlení tohoto procesu naleznete v části [William R. Vaughn](http://betav.com/BLOG/billva/) s *hitchhiker s Guide to Visual Studio a SQL Server, sedm Edition a* [Jak: nastavit SQL Server oprávnění pro ladění](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx).

> [!NOTE]
> Pokud na vašem vývojovém počítači běží Windows XP Service Pack 2, budete muset nakonfigurovat bránu firewall pro připojení k Internetu, aby povolovala vzdálené ladění. Článek [Postupy: povolení ladění SQL Server 2005](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx) obsahuje poznámky k tomu, že se jedná o dva kroky: (a) na hostitelském počítači sady Visual Studio, je třeba přidat `Devenv.exe` do seznamu výjimek a otevřít port TCP 135; a (b) na vzdáleném počítači (SQL) musíte otevřít port TCP 135 a přidat `sqlservr.exe` do seznamu výjimek. Pokud vaše zásady domény vyžadují síťovou komunikaci pomocí protokolu IPSec, je nutné otevřít porty UDP 4500 a UDP 500.

## <a name="summary"></a>Přehled

Kromě poskytování podpory ladění pro kód aplikace .NET nabízí Visual Studio také řadu možností ladění pro SQL Server 2005. V tomto kurzu jsme se podívali na dvě z těchto možností: přímé ladění databáze a ladění aplikací. Chcete-li přímo ladit objekt databáze T-SQL, vyhledejte objekt pomocí Průzkumník serveru klikněte na něj pravým tlačítkem myši a vyberte možnost Krokovat s vnořením. Tím se spustí ladicí program a zablokuje se na prvním příkazu v databázovém objektu, ve kterém je možné Krokovat s příkazy Object a zobrazovat a upravovat hodnoty parametrů. V kroku 1 jsme použili tento přístup ke krokování s `Products_SelectByCategoryID` uloženou procedurou.

Ladění aplikace umožňuje, aby se zarážky nastavily přímo v rámci databázových objektů. Když je objekt databáze se zarážkami vyvolán z klientské aplikace (například webové aplikace ASP.NET), program se zastaví, když ladicí program převezme. Ladění aplikace je užitečné, protože jasně ukazuje, co akce aplikace způsobí vyvolání konkrétního databázového objektu. Vyžaduje ale trochu více konfigurací a nastavení než přímé ladění databáze.

Objekty databáze lze také ladit prostřednictvím SQL Serverch projektů. Podíváme se na použití SQL Server projekty a jejich použití k vytváření a ladění objektů spravované databáze v dalším kurzu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](protecting-connection-strings-and-other-configuration-information-cs.md)
> [Další](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
