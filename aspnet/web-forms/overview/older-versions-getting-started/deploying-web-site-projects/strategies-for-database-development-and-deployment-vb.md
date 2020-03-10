---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-vb
title: Strategie pro vývoj a nasazování databází (VB) | Microsoft Docs
author: rick-anderson
description: Při prvním nasazení aplikace řízené daty můžete do produkčního prostředí zkopírovat databázi ve vývojovém prostředí. B...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 07b8905d-78ac-4252-97fb-8675b3fb0bbf
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ea4ade32fb05b9e69647ece7d1a4c400fe9fb21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546548"
---
# <a name="strategies-for-database-development-and-deployment-vb"></a>Strategie vývoje a nasazení databází (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial10_DBDevel_vb.pdf)

> Při prvním nasazení aplikace řízené daty můžete do produkčního prostředí zkopírovat databázi ve vývojovém prostředí. Ale při následném nasazení se skrytá kopie přepíše všechna data zadaná do provozní databáze. Místo toho nasazení databáze zahrnuje použití změn provedených ve vývojových databázích od posledního nasazení do provozní databáze. Tento kurz prověřuje tyto výzvy a nabízí různé strategie, které vám pomohou s dechronické a používáním změn provedených v databázi od posledního nasazení.

## <a name="introduction"></a>Úvod

Jak je popsáno v předchozích kurzech, nasazení aplikace ASP.NET zahrnuje kopírování relevantního obsahu z vývojového prostředí do provozního prostředí. Nasazení není jednorázová událost, ale místo toho, aby se nastavila při každém vydání nové verze softwaru, nebo když byly zjištěny nebo řešeny chyby nebo bezpečnostní otázky. Při kopírování stránek ASP.NET, obrázků, souborů JavaScriptu a dalších takových souborů do produkčního prostředí nemusíte se s tím, jak se tento soubor od posledního nasazení změnil. Soubor můžete zkopírovat do produkčního prostředí a přepsat tak stávající obsah. Tato jednoduchost se bohužel nerozšiřuje na nasazení databáze.

Při prvním nasazení aplikace řízené daty můžete do produkčního prostředí zkopírovat databázi ve vývojovém prostředí. Ale při následném nasazení se skrytá kopie přepíše všechna data zadaná do provozní databáze. Místo toho nasazení databáze zahrnuje použití *změn* provedených ve vývojových databázích od posledního nasazení do provozní databáze. Tento kurz prověřuje tyto výzvy a nabízí různé strategie, které vám pomohou s dechronické a používáním změn provedených v databázi od posledního nasazení.

## <a name="the-challenges-of-deploying-a-database"></a>Výzvy k nasazení databáze

Předtím, než byla aplikace řízená daty nasazena poprvé, existuje pouze jedna databáze, konkrétně databáze ve vývojovém prostředí, což je důvod, proč při prvním nasazení aplikace založené na datech zkopírovat databázi do vývojové prostředí v produkčním prostředí. Ale po nasazení aplikace jsou k dispozici dvě kopie databáze: jeden ve vývoji a jeden v produkčním prostředí.

Mezi nasazeními se může stát, že vývoj a provozní databáze nebudou synchronizovány. I když schéma produkční databáze s zůstane beze změny, schéma vývojové databáze s se může změnit při přidání nových funkcí. Je možné přidat nebo odebrat sloupce, tabulky, zobrazení nebo uložené procedury. Můžou být taky důležitá data, která se přidají do vývojové databáze. Mnoho aplikací řízených daty zahrnuje vyhledávací tabulky naplněné daty, která jsou pevně kódovaná, a specifická pro aplikace, která nejsou upravitelná uživatelem. Například web na aukci může mít rozevírací seznam s možnostmi, které popisují stav vydané položky, jako je nový, dobrý a věrný. Místo toho, aby byly tyto možnosti pevně zapsány přímo v rozevíracím seznamu, je obvykle vhodnější umístit je do databázové tabulky. Pokud během vývoje dojde k přidání nové podmínky s názvem nedostatečná, v případě nasazení aplikace se tento stejný záznam musí přidat do vyhledávací tabulky v provozní databázi.

V ideálním případě nasazení databáze zahrnuje kopírování databáze z vývoje do produkčního prostředí. Mějte ale na paměti, že Jakmile nasadíte aplikaci a obnovíte vývoj, provozní databáze se naplní skutečnými daty od skutečných uživatelů. Proto pokud byste chtěli jednoduše zkopírovat databázi z vývoje do produkčního prostředí při dalším nasazení, přepíšete provozní databázi a ztratíte stávající data. Čistým výsledkem je, že nasazení databáze povaří, aby se projevily změny provedené v vývojové databázi od posledního nasazení.

Vzhledem k tomu, že nasazení databáze zahrnuje použití změn ve schématu a případně dat od posledního nasazení, je třeba zachovat historii změn (nebo určit v době nasazení), aby bylo možné tyto změny použít v produkčním prostředí. Existují různé techniky pro správu a používání změn v datovém modelu.

### <a name="defining-the-baseline"></a>Definování standardních hodnot

Chcete-li zachovat změny v databázi aplikace, musíte mít nějaký počáteční stav, na který jsou změny aplikovány. V jednom krajním případě by počáteční stav mohl být prázdná databáze bez tabulek, zobrazení nebo uložených procedur. Výsledkem takového směrného plánu je velký protokol změn, protože musí zahrnovat vytváření všech tabulek databáze, zobrazení a uložených procedur spolu se všemi změnami provedenými po počátečním nasazení. Na druhém konci spektra můžete nastavit směrný plán jako verzi databáze, která je původně nasazena do provozního prostředí. Výsledkem této volby je mnohem menší protokol změn, protože obsahuje jenom změny, které se provedly v databázi po prvním nasazení. Toto je přístup, který nejlépe vyberu. A samozřejmě můžete zvolit více uprostřed přístupu k cestám, definovat směrný plán jako určitý bod mezi počátečním vytvořením databáze a při prvním nasazení databáze.

Po zvolení standardních hodnot zvažte vygenerování skriptu SQL, který lze provést pro opětovné vytvoření základní verze. Takový skript umožňuje rychle znovu vytvořit základní verzi databáze. Tato funkce je užitečná zejména ve větších projektech, kde může existovat více vývojářů pracujících na projektu nebo v dalších prostředích, jako je například testování nebo příprava, které potřebují svou vlastní kopii databáze.

K dispozici je celá řada nástrojů pro vygenerování skriptu SQL základní verze. Z SQL Server Management Studio (SSMS) můžete kliknout pravým tlačítkem na databázi, přejít do podnabídky úkoly a vybrat možnost Generovat skripty. Spustí se Průvodce skriptem, který vám dá pokyn vygenerovat soubor, který obsahuje příkazy SQL pro vytvoření objektů databáze s. Další možností je Průvodce publikováním databáze, který může generovat příkazy SQL nejen vytvořit schéma databáze, ale také data v databázových tabulkách. Průvodce publikováním databáze byl v kurzu *nasazení databáze* podrobněji přezkoumán. Bez ohledu na to, jaký nástroj používáte, byste měli mít na konci soubor skriptu, který můžete použít k opětovnému vytvoření základní verze vaší databáze, pokud by to bylo nutné.

## <a name="documenting-the-database-changes-in-prose"></a>Dokumentování změn databáze v prose

Nejjednodušší způsob, jak udržovat protokol změn v datovém modelu během fáze vývoje, je zaznamenat změny v prose. Například pokud během vývoje již nasazené aplikace přidáte nový sloupec do tabulky `Employees`, odeberete sloupec z tabulky `Orders` a přidáte novou tabulku (`ProductCategories`), měli byste zachovat textový soubor nebo dokument aplikace Microsoft Word s následující historií:

<a id="0.8_table01"></a>

| **Datum změny** | **Změnit podrobnosti** |
| --- | --- |
| 2009-02-03: | Do tabulky `Employees` se přidaly sloupce `DepartmentID` (`int`, NOT NULL). Do `Employees.DepartmentID`se přidalo omezení cizího klíče z `Departments.DepartmentID`. |
| 2009-02-05: | Z tabulky `Orders` byl odebrán `TotalWeight` sloupců. Data již zachycená v přidružených záznamech `OrderDetails`. |
| 2009-02-12: | Vytvořila se tabulka `ProductCategories`. Existují tři sloupce: `ProductCategoryID` (`int`, `IDENTITY`, `NOT NULL`), `CategoryName` (`nvarchar(50)`, `NOT NULL`) a `Active` (`bit`, `NOT NULL`). Přidání omezení primárního klíče do `ProductCategoryID`a výchozí hodnota 1 pro `Active`. |

Tento přístup má několik nevýhod. Pro Starter neexistuje žádná doufám pro automatizaci. Kdykoli je potřeba tyto změny použít pro databázi, například při nasazení aplikace, musí vývojář každou změnu ručně implementovat. Pokud navíc potřebujete znovu sestavit konkrétní verzi databáze ze směrného plánu pomocí protokolu změn, tak bude trvat více a více času, než se zvětší velikost protokolu. Další nevýhodou této metody je, že přehlednost a úroveň podrobností každé položky protokolu změn jsou ponechány osobě, která změnu zaznamená. V týmu s více vývojáři můžou být podrobnější, čitelnější nebo přesnější záznamy než jiné. Je také možné překlepy a další chyby při zadávání dat souvisejících s lidmi.

Hlavní výhodou pro dokumentování změn databáze v prose je jednoduchost. Nemusíte být obeznámeni se syntaxí SQL pro vytváření a změny databázových objektů. Místo toho můžete zaznamenávat změny v prose a implementovat je prostřednictvím grafického uživatelského rozhraní SQL Server Management Studio s.

Údržba protokolu změn v prose je, a to bez vysoké složitosti a nefunguje dobře s některými projekty, například s velkými rozsahy v oboru, mají časté změny v datovém modelu nebo obsahují více vývojářů. Ale tento přístup byl znám dobře v malých projektech, které mají pouze příležitostné změny v datovém modelu a kde jediný vývojář nemá silné pozadí v syntaxi SQL pro vytváření a změny databázových objektů.

> [!NOTE]
> I když jsou informace v protokolu změn, technicky, jenom do doby nasazení, doporučujeme udržovat historii změn. Místo toho, abyste zachovali jeden, stále rostoucí soubor protokolu změn, zvažte použití jiného souboru protokolu změn pro každou verzi databáze. Obvykle budete chtít verzi databáze pokaždé nasadit. Když zachováte protokol změn protokolů, můžete od základů znovu vytvořit libovolnou verzi databáze spuštěním skriptů protokolu změn od verze 1 a pokračovat, dokud nedosáhnete verze, kterou potřebujete znovu vytvořit.

## <a name="recording-the-sql-change-statements"></a>Záznam příkazů SQL Change

Hlavní nevýhodou zachovávání protokolu změn v prose je nedostatečná automatizace. V ideálním případě je implementace změn databáze do provozní databáze při nasazení tak snadné, když kliknete na tlačítko ke spuštění skriptu, nikoli ruční provedení seznamu pokynů. Tato automatizace je možná udržováním protokolu změn, který obsahuje tyto příkazy SQL, které se používají k změně datového modelu.

Syntaxe SQL obsahuje několik příkazů pro vytváření a úpravu různých databázových objektů. Například [*příkaz CREATE TABLE*](https://msdn.microsoft.com/library/ms174979.aspx)po spuštění vytvoří novou tabulku se zadanými sloupci a omezeními. [*Příkaz ALTER TABLE*](https://msdn.microsoft.com/library/ms190273.aspx) upraví existující tabulku, přidá, odebere nebo upraví její sloupce nebo omezení. K dispozici jsou také příkazy pro vytváření, úpravy a vyřazení indexů, zobrazení, uživatelsky definovaných funkcí, uložených procedur, triggerů a dalších databázových objektů.

V našem příkladu se vrátí obrázek, který během vývoje již nasazené aplikace přidáte nový sloupec do tabulky `Employees`, odeberete sloupec z tabulky `Orders` a přidáte novou tabulku (`ProductCategories`). Výsledkem takových akcí je soubor protokolu změn s následujícími příkazy SQL:

[!code-sql[Main](strategies-for-database-development-and-deployment-vb/samples/sample1.sql)]

Vložení těchto změn do provozní databáze při nasazení je operace jedním kliknutím: Open SQL Server Management Studio, připojte se k provozní databázi, otevřete nové okno dotazu, vložte obsah protokolu změn a kliknutím na Spustit spusťte skript.

## <a name="using-a-comparison-tool-to-synchronize-the-data-models"></a>Synchronizace datových modelů pomocí nástroje pro porovnání

Dokumentování změn databáze v prose je jednoduché, ale implementace změn vyžaduje, aby vývojář provedl každou změnu v provozní databázi po druhém. dokumentování příkazů Change SQL implementuje tyto změny v provozní databázi tak snadno a rychle, jako když kliknete na tlačítko, ale vyžaduje učení a sestavování příkazů SQL a syntaxi pro vytváření a změny databázových objektů. Nástroje pro porovnání databáze z obou přístupů nejlépe vyberou a vyhodí nejhorší.

Nástroj pro porovnání databáze porovnává schéma nebo data dvou databází a zobrazí souhrnnou sestavu s informacemi o tom, jak se databáze liší. Pak můžete kliknutím na tlačítko vygenerovat příkazy SQL pro synchronizaci jednoho nebo více databázových objektů. V kostce můžete použít nástroj pro porovnání databáze k porovnání databází vývoje a produkčního prostředí v době nasazení, což generuje soubor obsahující příkazy SQL, které při spuštění použijí změny ve schématu provozní databáze. zrcadlí schéma vývojové databáze s.

Existuje řada nástrojů pro porovnání databází jiných výrobců, které nabízí mnoho různých dodavatelů. Jedním z těchto příkladů je [*SQL Compare*](http://www.red-gate.com/products/SQL_Compare/), [*software červené brány*](http://www.red-gate.com/). Podívejme se, jak pomocí porovnání SQL porovnat a synchronizovat schémata vývoje a produkčních databází.

> [!NOTE]
> V době psaní tohoto zápisu aktuální verze SQL Compare byla verze 7,1 s cenou Standard Edition $395. Postup můžete sledovat stažením bezplatné 14 dní zkušební verze.

Po spuštění porovnávání SQL se otevře dialogové okno projekty porovnání, ve kterém se zobrazí uložené projekty porovnání SQL. Vytvoření nového projektu Tím se spustí Průvodce konfigurací projektu, který zobrazí výzvu k zadání informací o databázích, které se mají porovnat (viz obrázek 1). Zadejte informace pro databáze pro vývoj a produkční prostředí.

[![porovnání databází vývoje a výroby](strategies-for-database-development-and-deployment-vb/_static/image2.jpg)](strategies-for-database-development-and-deployment-vb/_static/image1.jpg)

**Obrázek 1**: porovnání databází vývoje a výroby ([kliknutím zobrazíte obrázek v plné velikosti](strategies-for-database-development-and-deployment-vb/_static/image3.jpg))

> [!NOTE]
> Pokud vaše databáze vývojového prostředí je databázový soubor SQL Express edice ve složce `App_Data` na vašem webu, budete muset databázi zaregistrovat na databázovém serveru SQL Server Express, aby ji bylo možné vybrat v dialogovém okně na obrázku 1. Nejjednodušší způsob, jak to provést, je otevřít SQL Server Management Studio (SSMS), připojit se k databázovému serveru SQL Server Express a připojit databázi. Pokud nemáte na svém počítači nainstalovanou SSMS, můžete si stáhnout a nainstalovat bezplatnou [*SQL Server 2008 Management Studio základní verzi*](https://www.microsoft.com/downloads/details.aspx?FamilyId=7522A683-4CB2-454E-B908-E805E9BD4E28&amp;displaylang=en).

Kromě výběru databází, které se mají porovnat, můžete také na kartě Možnosti zadat řadu nastavení porovnání. Jednu z možností, kterou možná budete chtít zapnout, je "ignorovat omezení a názvy indexů". V předchozím kurzu jsme přidali objekty databáze Application Services do databází vývoje a výroby. Pokud jste k vytvoření těchto objektů v provozní databázi použili nástroj `aspnet_regsql.exe`, zjistíte, že se názvy primárních a jedinečných omezení liší mezi vývojovými a provozními databázemi. V důsledku toho SQL Compare označí všechny tabulky aplikačních služeb tak, jak se liší. Můžete buď nechat nezaškrtnuté políčko "ignorovat omezení a indexovat názvy" a synchronizovat názvy omezení, nebo pořídit porovnávání SQL pro ignorování těchto rozdílů.

Po výběru databází k porovnání (a přezkoumání možností porovnání) klikněte na tlačítko Porovnat a spusťte porovnání. V průběhu několika dalších sekund SQL Compare prověřuje schémata dvou databází a vygeneruje sestavu, jak se liší. Jsem záměrně změny v vývojové databázi, aby ukázaly, jak se tyto nesrovnalosti poznamenaly v rozhraní SQL Compare. Jak ukazuje obrázek 2, přidám do tabulky `Authors` `BirthDate` sloupec, odebrali jste `ISBN` sloupec z tabulky `Books` a přidali jsme novou tabulku `Ratings`, která je určena k tomu, aby uživatelé navštívili tuto stránku jako počet zkontrolovaných knih.

> [!NOTE]
> Změny datového modelu provedené v tomto kurzu byly provedeny k ilustraci pomocí nástroje pro porovnání databáze. Tyto změny v databázi nenajdete v budoucích kurzech.

[![SQL Compare obsahuje rozdíly mezi vývojovým a provozním databázím.](strategies-for-database-development-and-deployment-vb/_static/image5.jpg)](strategies-for-database-development-and-deployment-vb/_static/image4.jpg)

**Obrázek 2**: SQL Compare obsahuje rozdíly mezi vývojovými a provozními databázemi ([kliknutím zobrazíte obrázek v plné velikosti).](strategies-for-database-development-and-deployment-vb/_static/image6.jpg)

SQL Compare rozděluje objekty databáze do skupin a rychle zobrazuje, jaké objekty existují v obou databázích, ale jsou odlišné, které objekty existují v jedné databázi, ale ne druhá, a které objekty jsou identické. Jak vidíte, existují dva objekty, které existují v obou databázích, ale jsou odlišné: `Authors` tabulce, která má sloupec přidán, a tabulce `Books`, která byla odstraněna. Existuje jeden objekt, který existuje pouze ve vývojové databázi, konkrétně nově vytvořená `Ratings` tabulka. A k dispozici jsou 117 objekty, které jsou v obou databázích identické.

Výběr databázového objektu zobrazí okno rozdíly SQL, které ukazuje, jak se tyto objekty liší. Okno rozdíly v systému SQL zobrazené dole na obrázku 2 zvýrazní, že `Authors` tabulka ve vývojové databázi má sloupec `BirthDate`, který se nenachází v tabulce `Authors` v provozní databázi.

Po kontrole rozdílů a výběru objektů, které chcete synchronizovat, je dalším krokem generování příkazů SQL potřebných k aktualizaci schématu provozní databáze, aby odpovídaly vývojové databázi. Toho je možné provést prostřednictvím Průvodce synchronizací. Průvodce synchronizací potvrdí, které objekty se mají synchronizovat, a shrnuje plán akcí (viz obrázek 3). Databáze můžete okamžitě synchronizovat nebo vygenerovat skript s příkazy SQL, které se dají spustit na vašem volném čase.

[![k synchronizaci schémat databází použít Průvodce synchronizací](strategies-for-database-development-and-deployment-vb/_static/image8.jpg)](strategies-for-database-development-and-deployment-vb/_static/image7.jpg)

**Obrázek 3**: k synchronizaci schémat databází použijte Průvodce synchronizací ([kliknutím zobrazíte obrázek v plné velikosti).](strategies-for-database-development-and-deployment-vb/_static/image9.jpg)

Nástroje pro porovnání databáze, jako je třeba software Red hradlo s SQL Compare, provádějí změny ve schématu vývojové databáze do provozní databáze stejně snadno jako Point a kliknutí.

> [!NOTE]
> Porovnávání SQL porovnává a synchronizuje dvě *schémata*databází. Bohužel data neporovnat a nesynchronizuje v rámci dvou tabulek databáze. Software červené brány nabízí produkt s názvem [*porovnání dat SQL*](http://www.red-gate.com/products/SQL_Data_Compare/) , který porovnává a synchronizuje data mezi dvěma databázemi, ale jedná se o samostatný produkt z porovnání SQL a náklady jiné $395.

## <a name="taking-the-application-offline-during-deployment"></a>Přepnutí aplikace do režimu offline během nasazení

Jak jsme viděli v těchto kurzech, nasazení je proces, který zahrnuje několik kroků: kopírování stránek ASP.NET, stránek předlohy, souborů CSS, souborů JavaScriptu, obrázků a dalšího potřebného obsahu z vývojového prostředí do produkčního prostředí. hlediska v případě potřeby se kopírují konfigurační informace specifické pro produkční prostředí. a použití změn pro datový model od posledního nasazení. V závislosti na počtu souborů a složitosti vaší databáze můžou tyto kroky trvat několik sekund, než se dokončí. Během tohoto okna je webová aplikace ve službě tokem a uživatelé, kteří navštíví web, můžou zaznamenat chyby nebo neočekávané chování.

Při nasazení webu je nejlepší převést webovou aplikaci do stavu offline, dokud se nasazení nedokončí. Převedení aplikace do offline režimu (a její následné zálohování po dokončení procesu nasazení) je stejně snadné jako nahrání souboru a jeho odstranění. Od ASP.NET 2,0 přebírá pouhá přítomnost souboru s názvem `app_offline.htm` v kořenovém adresáři aplikace s celým webem "offline". Každý požadavek na stránku ASP.NET na dané lokalitě automaticky odpoví obsahem `app_offline.htm` souboru. Po odebrání tohoto souboru se aplikace vrátí zpět do režimu online.

Převedení aplikace do režimu offline během nasazování je tak jednoduché jako nahrání souboru `app_offline.htm` do kořenového adresáře produkčního prostředí před zahájením procesu nasazení a jeho odstraněním (nebo přejmenováním na něco jiného) po dokončení nasazení. Další informace o tomto postupu najdete v článku Jan Peterson s, který přebírá [*aplikaci ASP.NET v režimu offline*](http://www.15seconds.com/issue/061207.htm).

## <a name="summary"></a>Souhrn

Hlavním problémem při nasazení aplikace řízené daty v průběhu nasazení databáze. Vzhledem k tomu, že existují dvě verze databáze – jeden ve vývojovém prostředí a jeden v produkčním prostředí – tato dvě databázová schémata můžou být nesynchronizovaná, protože nové funkce se přidávají při vývoji. Co víc, protože provozní databáze, která se naplní skutečnými daty od reálných uživatelů, nemůžete přepsat provozní databázi upravenou vývojovou databází, třeba když nasadíte soubory, které tvoří aplikaci (stránky ASP.NET, soubory obrázků a tak dále). Místo toho nasazení databáze zahrnuje implementaci přesné sady změn provedených ve vývojových databázích v provozní databázi od posledního nasazení.

V tomto kurzu jste se podívali na tři techniky pro údržbu a používání protokolu změn databáze. Nejjednodušším přístupem je zaznamenat změny v prose. I když tento cílem provádí implementaci těchto změn v provozní databázi ručním procesem, nevyžaduje znalost příkazů SQL pro vytváření a změnu databázových objektů. Propracovanější přístup a jeden, který je mnohem více palatable ve větších projektech nebo projektech s více vývojáři, je zaznamenat změny jako série příkazů SQL. To významně Hastens tyto změny do cílové databáze. Nejlepší z obou přístupů lze dosáhnout pomocí nástroje pro porovnání databáze, jako je například porovnání softwaru Red hradlo s SQL.

V tomto kurzu se uzavírá náš fokus na nasazení aplikace řízené daty. Další sada kurzů si vyhledá, jak reagovat na chyby v provozním prostředí. Podíváme se, jak místo žluté obrazovky smrti zobrazit přívětivou chybovou stránku. Podíváme se na to, jak protokolovat chyby a podrobnosti a jak vás upozornit, když dojde k těmto chybám.

Šťastné programování!

> [!div class="step-by-step"]
> [Předchozí](configuring-a-website-that-uses-application-services-vb.md)
> [Další](displaying-a-custom-error-page-vb.md)
