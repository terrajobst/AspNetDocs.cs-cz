---
uid: whitepapers/aspnet-data-access-content-map
title: Přístup k datům ASP.NET – doporučené prostředky | Microsoft Docs
author: rick-anderson
description: Toto téma obsahuje odkazy na zdroje informací o tom, jak přistupovat k datům ve webových aplikacích v ASP.NET, primárně pomocí Entity Framework a SQL se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633131"
---
# <a name="aspnet-data-access---recommended-resources"></a>Přístup k datům ASP.NET – doporučené zdroje informací

> Toto téma obsahuje odkazy na zdroje informací o tom, jak přistupovat k datům ve webových aplikacích v ASP.NET, primárně pomocí Entity Framework a SQL Server.
> 
> Pokud znáte skvělý Blogový příspěvek, vlákno [StackOverflow](http://stackoverflow.com) nebo jakýkoli jiný odkaz, který by byl užitečný, [pošlete nám e-mail](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) s odkazem.
> 
> Poslední aktualizace 4/3/2014

Téma obsahuje následující části:

- [Začínáme s přístupem k datům v ASP.NET](#gettingstarted)
- [Použití Entity Framework](#ef)

    - [Použití Entity Framework Code First](#cf)
    - [Použití Migrace Entity Framework Code First](#efcfmigrations)
    - [Použití Entity Framework Database First nebo Model First (Návrhář EF)](#efdbf)
    - [Načítání souvisejících dat v Entity Framework (opožděné načítání, načítání Eager a explicitní načítání)](#efrelateddata)
    - [Optimalizace výkonu Entity Framework](#optimizingef)
    - [Zpracování souběžnosti v aplikaci Entity Framework](#efconcurrency)
    - [Knihy týkající se Entity Framework](#efbooks)
    - [Další prostředky Entity Framework](#otherefresources)
- [Datové vazby v aplikacích ASP.NET Web Forms](#wfdatabinding)

    - [Použití vazby modelu webového formuláře](#wfmodelbinding)
    - [Používání ovládacích prvků datových zdrojů webových formulářů](#wfdsc)
    - [Použití ovládacích prvků webového formuláře a výrazů pro datovou vazbu](#wfdbc)
- [Práce s databázemi SQL Server](#sqlserver)

    - [Práce s SQL Server Express databáze LocalDB](#sslocaldb)
    - [Práce s databázemi SQL Server Express](#sse)
    - [Práce s Windows Azure SQL Database](#ssdb)
    - [Výběr mezi SQL Server a Windows Azure SQL Database](#ssdbchoosing)
- [Práce se systémy správy databáze NoSQL](#nosql)
- [Použití dotazů LINQ v aplikacích ASP.NET](#linq)
- [Použití dynamického generování dat](#dd)
- [Zabezpečení přístupu k datům](#securing)
- [Optimalizace výkonu přístupu k datům](#optimizingdataaccess)
- [Nasazení databáze](#deploying)
- [Přístup k datům prostřednictvím webové služby](#webservice)
- [Další zdroje](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>Začínáme s přístupem k datům v ASP.NET

- [Možnosti úložiště dat (vytváření skutečných cloudových aplikací s využitím Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). Kapitola elektronické knihy o vývoji pro Cloud Zavádí databáze NoSQL jako alternativu, kterou mnoho vývojářů, kteří znají relační databáze, často přehlédnout. Obsahuje pokyny pro to, co je potřeba vzít v úvahu při volbě relačních nebo NoSQL nebo výběru konkrétní platformy.
- [ASP.NET možnosti přístupu k datům](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). Úvod do možností přístupu k datům pro relační databáze pro ASP.NET a pokyny k výběru platforem a přístupových metod, které jsou vhodné pro váš scénář.
- [Relační databáze](http://en.wikipedia.org/wiki/Relational_database). Wikipedii). Pokud jste nepracovali s relačními databázemi, podívejte se na tuto stránku, kde najdete Úvod do terminologie a konceptů relační databáze. Úvod do SQL Server zejména v části [práce s SQL Server databázemi](#sqlserver) dále v tomto tématu.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Použití Entity Framework

- [Přístup k vývoji Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Pokyny k výběru Entity Frameworkho přístupu pro vývoj Database First, Model First nebo Code First.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Použití Entity Framework Code First

Následující kurzy nabízejí ukázkové aplikace ke stažení:

- [Začínáme s EF 6 pomocí MVC 5](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Pokrývá široké spektrum Entity Frameworkch Code Firstch scénářů, včetně migrací a funkcí EF 6, jako je odolnost připojení, zachycení příkazů a asynchronní. Toto je aktualizovaná verze [řady EF 5/MVC 4](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Předchozí řada obsahuje kurz o vzorech úložiště a jednotky práce, které nejsou zahrnuté do nové řady.
- [Seznámení s ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md). Pokrývá užší škálu Entity Frameworkch scénářů Code First, ale nabízí komplexnější úlohy představení funkcí MVC.
- [Vazby modelů a webové formuláře](https://go.microsoft.com/fwlink/?LinkId=286117). Používá Code First v aplikaci webových formulářů.
- [Začínáme s webovými formuláři ASP.NET 4,5](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Úvod do webových formulářů s určitou pokrytí Code First. Používá vazbu modelu.
- [Hudební úložiště MVC](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md) Používá Code First v aplikaci MVC 3 pro elektronické obchodování, která také implementuje členství a autorizaci. Použitá verze MVC a ASP.NET členství v systému (ověřování a autorizace) je zastaralá. Další informace o členství v ASP.NET najdete v tématu [https://asp.net/identity](https://asp.net/identity).

Další zdroje informací:

- [Entity Framework-Code First do existující databáze](https://msdn.microsoft.com/data/jj200620). MSDN. Video a návod, který ukazuje, jak použít Code First s existující databází.
- [Centrum pro vývojáře dat – Entity Framework](https://msdn.microsoft.com/data/ef). MSDN. Průvodce Entity Framework dokumentaci vytvořenou a udržovanou Entity Framework týmem najdete [v odkazu Začínáme](https://msdn.microsoft.com/data/ee712907) .

Další informace [o Entity Framework](#efbooks) a [dalších entity Frameworkch prostředcích](#otherefresources) najdete dále v tomto tématu.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Použití Migrace Entity Framework Code First

Většina výše uvedených kurzů Code First zahrnuje migrace. Viz také následující zdroje informací.

- [ASP.NET nasazení webu pomocí sady Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). Série kurzů se dvěma částmi, které ukazují, jak používat Migrace Code First k nasazení databáze.
- [Nasaďte zabezpečenou aplikaci ASP.NET MVC 5 s členstvím, protokolem OAuth a SQL Database na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Microsoft Azure). Jak používat migrace k nasazení členství a dat aplikací do Azure.
- [Přehled nasazení webu pro Visual Studio a ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) Vysvětlení, jak je Migrace Code First integrována do funkcí nasazení webu sady Visual Studio, naleznete v části **Konfigurace nasazení databáze v aplikaci Visual Studio** .
- [Centrum pro vývojáře dat – migrace Code First](https://msdn.microsoft.com/data/jj591621) (MSDN). Dokumentace k migraci Entity Framework týmu.
- [Migrace seriálu pro záznam dění](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). Blogu EF). Tři videa o pokročilých tématech v Migrace Code First.
- [Migrace Code First s weby webových stránek ASP.NET](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites). Mikesdotnetting blog). Ukazuje, jak použít Code First migrace s webem ASP.NET webové stránky vložením kontextu dat do projektu knihovny tříd sady Visual Studio.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Použití Entity Framework Database First nebo Model First (Návrhář EF)

- [Začínáme s Entity Framework 6 Database First pomocí MVC 5](../mvc/overview/getting-started/database-first-development/setting-up-database.md). Spusťte skript v Průzkumník serveru k vytvoření databáze a pak použijte návrháře Entity Framework k vytvoření datového modelu. Ukazuje, jak vytvořit jednoduché webové stránky CRUD a pro jiné funkce zpracování dat můžete postupovat podle některého z Code Firstch kurzů, protože všechny pracovní postupy EF používají stejné rozhraní DbContext API.

Následující zdroje jsou starší. Jsou užitečné, pokud chcete použít Entity Framework verze 4,0 a chcete použít ovládací prvek zdroje dat pro datovou vazbu v aplikaci webových formulářů.

- [Začínáme s Entity Framework 4,0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). Ukazuje, jak použít ovládací prvek **EntityDataSource** .
- [Pokračování v Entity Framework](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(ukazuje, jak používat ovládací prvek **ObjectDataSource** . Obsahuje kurz týkající se zpracování souběžnosti, kurz na výkon EF a kurz týkající se novinek v EF 4,0.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Zpracování souvisejících dat v Entity Framework (opožděné načítání, Eager načítání a explicitní načítání)

- [Čtení souvisejících dat s Entity Framework v aplikaci ASP.NET MVC](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, ukázková aplikace MVC Uvedené metody platí také pro vazby modelů webových formulářů a Database First pracovní postup.
- [Data Developer Center – načítání souvisejících entit](https://msdn.microsoft.com/data/jj574232) (MSDN). V dokumentaci Entity Framework týmu o načítání souvisejících dat.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Optimalizace výkonu Entity Framework

- [Pokročilé scénáře Entity Framework pro aplikaci ASP.NET](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md) Ukazuje, jak spustit vlastní příkazy SQL nebo volat vlastní uložené procedury, jak zakázat detekci změn a jak zakázat ověřování při ukládání změn.
- [Požadavky na výkon pro Entity Framework 5](https://msdn.microsoft.com/data/hh949853) (MSDN).
- [Požadavky na výkon (Entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [Maximalizace výkonu s Entity Framework ve webové aplikaci ASP.NET](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md) Platí pro Entity Framework 4,0.
- Viz také [Optimalizace přístupu k datům ASP.NET](#optimizingdataaccess) dále v tomto tématu.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Zpracování souběžnosti v aplikaci Entity Framework

- [Zpracování souběžnosti s Entity Framework v aplikaci ASP.NET MVC](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First rozhraní API DbContext pomocí ukázkové aplikace MVC.
- [Centrum pro vývojáře dat – optimistické vzorce souběžnosti](https://msdn.microsoft.com/data/jj592904) (MSDN). Dokumentace k souběžnosti týmu Entity Framework.
- [Zpracování souběžnosti s Entity Framework ve webové aplikaci v ASP.NET](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Platí pro Entity Framework 4,0. Database First rozhraní ObjectContext API využívající ukázkovou aplikaci webových formulářů.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Knihy týkající se Entity Framework

- [Programování Entity Framework: DbContext](http://shop.oreilly.com/product/0636920022237.do) podle Julie Lerman a Rowan Miller.
- [Programovací Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) od Julie Lerman a Rowan Miller.

Obě tyto knihy jsou aktuální doporučenými postupy. Poskytují komplexnější přehled o Entity Framework, než cokoli dostupné na internetu. Další kniha, [programový Entity Framework](http://shop.oreilly.com/product/9780596807252.do) od Julie Lerman, je větší a komplexnější, ale je starší, ale mnoho z těchto postupů již není doporučeným způsobem použití Entity Framework. Viz také seznam knih doporučený Entity Framework týmem v [centru pro vývojáře dat – knihy](https://msdn.microsoft.com/data/aa937716) na webu MSDN.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Další prostředky Entity Framework

- [Týmový blog Entity Framework (ADO.NET)](https://blogs.msdn.com/b/adonet/). Jeden z nejlepších zdrojů pro nejaktuálnější informace a oznámení o nových vylepšeních. Další Blogy související s EF najdete v části Blogroll na adrese Začínáme [s Entity Framework](https://msdn.microsoft.com/data/ee712907).
- [Časopis MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx). Podívejte se na sloupec **datových bodů** , který je často o tématech souvisejících s Entity Framework.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>Datové vazby v aplikacích ASP.NET Web Forms

- [ASP.NET webové formuláře – možnosti přístupu k datům](https://msdn.microsoft.com/library/jj822927.aspx) (<a id="wfmodelbinding"></a>MSDN).

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Použití vazby modelu webového formuláře

- [Vazby modelů a webové formuláře](https://go.microsoft.com/fwlink/?LinkId=286117). Řada kurzů s použitím EF Code First.
- [Vazba modelu webových formulářů – část 1: výběr dat](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (blog společnosti Scott Guthrie). V těchto starších blogových příspěvcích má vlastnost, která je aktuálně pojmenována ItemType, název typ modelu, ale jinak informace, které obsahují, jsou platné.
- [Vazba modelu webových formulářů – část 2: filtrování dat](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (blog společnosti Scott Guthrie).
- [Vazba modelu webových formulářů – část 3: aktualizace a ověřování](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (blog Scott Guthrie).
- [Vazba modelu webových formulářů ASP.NET 4,5](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md) (video).
- [Vazba modelu – část 1 – výběr dat](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (video)
- [Vazba modelu – část 2 – filtrování](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (video).
- [Začínáme s webovými formuláři ASP.NET 4,5 – zobrazení datových položek a podrobností](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Používání ovládacích prvků datových zdrojů webových formulářů

- [Ovládací prvky webového serveru pro zdroj dat](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN).
- [Oznamujeme vydání dynamického zprostředkovatele dat a ovládacího prvku EntityDataSource pro Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (blog pro vývoj webu společnosti Microsoft).

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Použití ovládacích prvků webového formuláře a výrazů pro datovou vazbu

- [Vazby modelů a webové formuláře](https://go.microsoft.com/fwlink/?LinkId=286117). Série kurzů, které používají EF Code First.
- [Začínáme s webovými formuláři ASP.NET 4,5 – zobrazení datových položek a podrobností](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)
- [Ovládací prvky pro data se silným typem](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (blog Scott Guthrie).
- [Datové ovládací prvky silného typu](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (video).
- [Datové ovládací prvky ASP.NET 4,5 Web Forms silného typu](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (video).
- [Ovládací prvky webového serveru vázané na data](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [Přehled výrazů datové vazby](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Tato stránka pokrývá jenom **vyhodnocení** a **vázání**; nebyla aktualizována, aby zahrnovala **položku** a **položku BindItem**.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>Práce s databázemi SQL Server

- [Funkce SQL Server Database](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Obecný úvod k nejrůznějším tématům SQL Server najdete v položkách v tomto obsahu v tématu.
- [Edice SQL Server](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Shrnutí dostupných edicí SQL Server s odkazy na Další informace o každé z nich.)
- [SQL Server připojovací řetězce pro webové aplikace ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Použití SQL Server Compact pro webové aplikace ASP.NET](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Microsoft SQL Server: ukázky produktu databáze](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Ukázkové databáze AdventureWorks
- [Instalace ukázkových databází](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Kromě zde uvedených metod si také můžete stáhnout jeden z ukázkových souborů. mdf do složky aplikace\_data webového projektu, převést databázi na LocalDB a vytvořit připojovací řetězec LocalDB. Informace o tom, jak to provést, najdete v tématu [How to: upgrade to LocalDB](https://msdn.microsoft.com/library/hh873188.aspx).

V následujících částech najdete další informace o práci s SQL Server Express a LocalDB a výběr mezi SQL Server a SQL Database.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>Práce s SQL Server Express databáze LocalDB

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). Oficiální Úvod na MSDN pro LocalDB.
- [SQL Server připojovací řetězce pro webové aplikace ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Postupy: upgrade na LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). Postup migrace souboru MDF ze starší verze SQL Server Express do LocalDB. I když si stáhnete jednu z [ukázkových databází SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=117483), musíte projít tento proces.
- [Představujeme LocalDB, což je vylepšený SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express blog). Obsahuje další informace o tom, proč byl LocalDB vytvořen, než je součástí MSDN.
- [LocalDB: kde je moje databáze?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express blog). Informace o tom, kde jsou vytvořeny soubory databáze LocalDB.
- [Použití LocalDB s plnou službou IIS, část 1: Profil uživatele](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express blog). LocalDB není navržený tak, aby fungoval se službou IIS. Tato série příspěvků na blogu vysvětluje problémy a některá alternativní řešení.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>Práce s databázemi SQL Server Express

- [SQL Server připojovací řetězce pro webové aplikace ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). Použijete-li nastavení připojovacího řetězce AttachDBFileName s SQL Server Express, přečtěte si část o uživatelské instanci této stránky zvlášť.
- [Jak převzít vlastnictví vašich místních SQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (SQL Server Express blog). Běžný problém nedokáže pracovat s SQL Server Express databázemi, protože nejste správcem instance SQL Server Express. Ve výchozím nastavení má správce jenom osoba, která je nainstalovaná SQL Server Express. Tento blog vysvětluje, jak sami sebe SQL Server Express správce, pokud jste správcem počítače.
- [Může moje webová aplikace ASP.NET používat databázi SQL Server Express v produkčním prostředí?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Práce s Windows Azure SQL Database

- [Nasaďte zabezpečenou aplikaci ASP.NET MVC s členstvím, protokolem OAuth a SQL Database na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (Microsoft Azure Web).
- [Databáze SQL](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure lokality). Kurzy Začínáme a návody.
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). Uzel nejvyšší úrovně obsahu pro SQL Database v knihovně MSDN.
- [Rejstřík článků na webu TechNet pro Windows Azure SQL Database](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (Web Microsoft TechNet).
- [Blok aplikace pro zpracování přechodných chyb](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Rozhraní, které umožňuje zpracovat přechodné chyby sítě a chyby připojení, které jsou výsledkem omezení. K dispozici v balíčku NuGet: [Enterprise Library 5,0 – blok aplikace pro zpracování přechodného selhání](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- [Začínáme s SQL Database a Entity Framework](https://msdn.microsoft.com/data/jj556244) (MSDN).
- [Windows Azure Training Kit](https://www.microsoft.com/download/details.aspx?id=8396) (Stažení softwaru společnosti Microsoft). Obsahuje praktická cvičení pro SQL Database.
- [Fórum komunity Windows Azure SQL Database](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Přechod na Windows Azure SQL Database](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN). Jedna kapitola komplexního uceleného scénáře od týmu Microsoft Patterns and Practices. Obsahuje informace o tom, proč možná budete chtít migrovat a jak migrovat z SQL Server na SQL Database.
- [Migrace SQL Server databází do Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).
- [Průvodce migrací SQL Database](http://sqlazuremw.codeplex.com/). Open source nástroj pro migraci databází do a z SQL Database.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>Výběr mezi SQL Server a Windows Azure SQL Database

- [Porovnejte SQL Server s Windows Azure SQL Database](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Web Microsoft TechNet).
- [Migrace dat do Windows Azure SQL Database: nástroje a techniky](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). Obsahuje oddíly, které porovnávají SQL Server SQL Database a poskytují pokyny k migraci z SQL Server na SQL Database.
- [Průvodce doručováním Windows Azure SQL Database](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (Web Microsoft TechNet).
- [Omezení funkcí SQL Server (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Windows Azure Table Storage a windows Azure SQL Database – porovnání a kontrast](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Pro aplikaci, kterou nasazujete do Windows Azure, může být Windows Azure Table Storage alternativou Azure SQL Database Windows. Toto téma vám pomůže při rozhodování mezi těmito alternativami.
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Pokyny a omezení (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>Práce se systémy správy databáze NoSQL

- [Windows Azure Data Services](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure lokality). Podívejte se na část [Průvodce funkcemi služby Table Service](https://docs.microsoft.com/azure/) a **Velká data** stránky.
- [ASP.NET vícevrstvé aplikace s využitím tabulek, front a objektů BLOB služby Storage](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure lokality). Komplexní kurz ke stažení ukázkové aplikace, která používá tabulky NoSQL Windows Azure Storage.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>Použití dotazů LINQ v aplikacích ASP.NET

- [ASP.NET možnosti přístupu k datům](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). Obsahuje úvod do jazyka LINQ.
- [Výuková videa LINQ](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (Jana Stagner 's blog).
- [ASP.NET fórum ve vlákně s odkazy na dynamické zdroje LINQ](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq).

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Použití dynamického generování dat

- [Šablony dynamických datových projektů](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). Pokyny k použití dynamických datových projektů.
- [ASP.NET dynamická data](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Zabezpečení přístupu k datům

- [Zabezpečení přístupu k datům v ASP.NET](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [Požadavky na zabezpečení (Entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [Postupy: zabezpečení připojovacích řetězců při použití ovládacích prvků zdroje dat](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN).

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Optimalizace výkonu přístupu k datům

- [ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET Caching](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [Zlepšení výkonu ASP.NET](https://msdn.microsoft.com/library/ff647787) (MSDN). V horní části této stránky se zobrazí upozornění "vyřazený obsah", ale většina informací je stále relevantní a není k dispozici žádný srovnatelný aktualizovaný prostředek.
- [Zlepšení výkonu SQL Server](https://msdn.microsoft.com/library/ff647793) (MSDN). Stejný komentář jako předchozí odkaz

Viz také [optimalizace Entity Framework výkonu](#optimizingef) výše v tomto tématu.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Nasazení databáze

- [Nasazení webu ASP.NET – doporučené prostředky](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Přístup k datům prostřednictvím webové služby

- [Přístup k datům prostřednictvím webové služby](https://msdn.microsoft.com/library/ms178359.aspx#webservice) (MSDN). Pokyny k používání webového rozhraní API versus WCF.
- [Začínáme s webovým rozhraním API ASP.NET](../web-api/index.md)
- [WCF Data Services](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Další prostředky

- [ASP.NET Data Access – Nejčastější dotazy](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [Kurzy webových formulářů ASP.NET – data](../web-forms/overview/data-access/index.md) Většina těchto kurzů je poměrně stará; Ujistěte se, že jste si přečetli [Možnosti přístupu k datům ASP.NET](https://msdn.microsoft.com/library/ms178359.aspx) a [Možnosti úložiště dat (vytváření skutečných cloudových aplikací s Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) , takže se nedostanete příliš daleko do metody přístupu k datům, která není pro váš scénář správná.
- [Mapa obsahu ASP.NET MVC](../mvc/overview/getting-started/recommended-resources-for-mvc.md)
- [Kurzy webových stránek ASP.NET – data](../web-pages/overview/data/index.md)
- [Přístup k datům v aplikaci Visual Studio](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). Obsahuje seznam odkazů podobných této mapě obsahu, ale se zaměřením na sadu Visual Studio, nikoli ASP.NET.
