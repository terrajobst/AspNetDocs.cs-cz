---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: Možnosti úložiště dat (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 9357ed5aef39bed501cdac9ac26d46c884d4fae0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457177"
---
# <a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>Možnosti úložiště dat (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Většina lidí se používá u relačních databází a při návrhu cloudové aplikace se při navrhování cloudových aplikací zapřehlédnout další možnosti ukládání dat. Výsledkem může být optimální výkon, vysoké výdaje nebo horší, protože [NoSQL](http://en.wikipedia.org/wiki/NoSQL) (nerelační) databáze může zpracovávat některé úlohy efektivněji než relační databáze. Když si zákazníci vyžádají pomoc s řešením kritického problému s datovým úložištěm, je často to proto, že mají relační databázi, kde by jedna z možností NoSQL fungovala lépe. V těchto situacích by byl zákazník lépe vypnutý, pokud předtím implementoval řešení NoSQL před nasazením aplikace do produkčního prostředí.

Na druhé straně by také došlo k chybě, která předpokládá, že databáze NoSQL může dělat všechno dobře nebo dostatečně dobře. Pro všechny úlohy úložiště dat neexistuje žádná jediná vhodná volba pro správu dat. různá řešení pro správu dat jsou optimalizovaná pro různé úlohy. Většina reálných cloudových aplikací má nejrůznější požadavky na úložiště dat a často se hodí pro kombinaci více řešení pro ukládání dat.

Účelem této kapitoly je poskytnout vám širší smysl možností úložiště dat dostupných pro cloudovou aplikaci a některé základní pokyny k výběru těch, které vyhovují vašemu scénáři. Je vhodné si uvědomit, jaké možnosti máte k dispozici, a zamyslete se nad jejich sílami a slabinami před vývojem aplikace. Změna možností úložiště dat v produkční aplikaci může být extrémně obtížná, třeba když chcete změnit stroj Jet, zatímco je rovina v letadle.

## <a name="data-storage-options-on-azure"></a>Možnosti úložiště dat v Azure

Cloud umožňuje poměrně snadné použití nejrůznějších relačních a NoSQL úložišť dat. Tady jsou některé platformy pro úložiště dat, které můžete použít v Azure.

![](data-storage-options/_static/image1.png)

V tabulce jsou uvedeny čtyři typy databází NoSQL:

- [Databáze klíč/hodnota](https://msdn.microsoft.com/library/dn313285.aspx#sec7) ukládají jeden serializovaný objekt pro každou hodnotu klíče. Jsou vhodné pro ukládání velkých objemů dat, kde chcete získat jednu položku pro danou hodnotu klíče, a nemusíte se dotazovat na základě jiných vlastností položky.

    [Úložiště objektů BLOB v Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/) je databáze klíč/hodnota, která funguje jako úložiště souborů v cloudu s klíčovými hodnotami, které odpovídají názvům složek a souborů. Načtete soubor podle jeho složky a názvu souboru, ne tak, že vyhledáte hodnoty v obsahu souboru.

    [Azure Table Storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/) je také databáze klíč/hodnota. Každá hodnota se nazývá *entita* (podobná řádku, identifikovaná klíčem oddílu a klíčem řádku) a obsahuje více *vlastností* (podobně jako sloupce, ale ne všechny entity v tabulce musí sdílet stejné sloupce). Dotazování na jiné sloupce než klíč je mimořádně neefektivní a mělo by se jim vyhnout. Můžete například ukládat data profilu uživatele s jedním oddílem, který ukládá informace o jednom uživateli. Můžete ukládat data, jako je uživatelské jméno, hodnota hash hesla, datum narození a tak dále, v samostatných vlastnostech jedné entity nebo v samostatných entitách ve stejném oddílu. Ale nechcete se dotazovat na všechny uživatele s daným rozsahem dat narození a nemůžete spustit dotaz join mezi vaší tabulkou profilu a jinou tabulkou. Úložiště tabulek je škálovatelné a méně nákladné než relační databáze, ale neumožňuje složité dotazy nebo spojení.
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8) jsou databáze klíč/hodnota, ve kterých jsou tyto hodnoty *dokumenty*. "Dokument" se tady nepoužívá v smyslech dokumentu Wordu nebo Excelu, ale označuje kolekci pojmenovaných polí a hodnot, z nichž může být podřízený dokument. Například v tabulce historie objednávky může mít dokument objednávky číslo objednávky, datum objednávky a pole zákazníka. pole Customer (zákazník) může obsahovat pole jméno a adresa. Databáze kóduje data polí ve formátu, jako je například XML, YAML, JSON nebo BSON; nebo může použít prostý text. Jedna funkce, která nastavuje databáze dokumentů od databází typu klíč/hodnota, je možnost dotazování na neklíčová pole a definování sekundárních indexů, aby bylo možné dotazování zefektivnit. Díky tomu je databáze dokumentu vhodnější pro aplikace, které potřebují načítat data na základě kritérií složitějších, než je hodnota klíče dokumentu. Například v databázi dokumentů historie prodejní objednávky byste se mohli dotazovat na různá pole, jako je ID produktu, ID zákazníka, jméno zákazníka a tak dále. [MongoDB](http://www.mongodb.org/) je oblíbená databáze dokumentů.
- [Databáze rodiny sloupců](https://msdn.microsoft.com/library/dn313285.aspx#sec9) jsou úložiště dat klíč/hodnota, která umožňují strukturovat úložiště dat v kolekcích souvisejících sloupců nazývaných rodin sloupců. Například databáze sčítání může mít jednu skupinu sloupců pro jméno osoby (první, střední, poslední), jednu skupinu pro adresu osoby a jednu skupinu pro informace o profilu osoby (DOB, pohlaví atd.). Databáze pak může ukládat jednotlivé rodiny sloupců do samostatného oddílu a přitom uchovávat všechna data pro jednu osobu, která souvisí se stejným klíčem. Pak si můžete přečíst všechny informace o profilu, aniž byste museli číst všechny informace o jménech a adresách. [Cassandra](http://cassandra.apache.org/) je oblíbená databáze rodiny sloupců.
- [Databáze grafů](https://msdn.microsoft.com/library/dn313285.aspx#sec10) ukládají informace jako kolekci objektů a relací. Účelem databáze grafu je umožnit aplikaci efektivně provádět dotazy, které procházejí sítí objektů a vztahy mezi nimi. Objekty mohou být například zaměstnanci v databázi lidských zdrojů a je možné, že budete chtít usnadnit dotazy, jako je "hledání všech zaměstnanců, kteří přímo nebo nepřímo pracují pro Scott". [Neo4j](http://www.neo4j.org/) je oblíbená databáze grafu.

V porovnání s relačními databázemi nabízejí možnosti NoSQL mnohem větší škálovatelnost a cenovou efektivitu pro ukládání a analýzu nestrukturovaných dat. Kompromisem je, že neposkytují bohatou možnost dotazování a robustní integritu dat relačních databází. NoSQL bude dobře fungovat pro data protokolu služby IIS, což zahrnuje velký objem, který není potřeba pro spojování dotazů. NoSQL nebude fungovat dobře pro bankovní transakce, což vyžaduje absolutní integritu dat a zahrnuje mnoho vztahů k ostatním datům souvisejícím s účtem.

K dispozici je také novější kategorie databázové platformy s názvem [NewSQL](http://en.wikipedia.org/wiki/NewSQL) , která kombinuje škálovatelnost databáze NoSQL s možností dotazování a transakční integrity relační databáze. Databáze NewSQL jsou navržené pro distribuované úložiště a zpracování dotazů, což je často těžké implementovat v databázích "OldSQL". [NuoDB](http://www.nuodb.com/) je příklad databáze NewSQL, kterou je možné použít v Azure.

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop a MapReduce

Velké objemy dat, které můžete ukládat v databázích NoSQL, může být obtížné včas analyzovat. K tomu můžete použít rozhraní, jako je [Hadoop](http://hadoop.apache.org/) , které implementuje [MapReduce](http://en.wikipedia.org/wiki/MapReduce) funkce. V podstatě to znamená, že proces MapReduce je následující:

- Omezte velikost dat, která je třeba zpracovat, výběrem z úložiště dat pouze data, která skutečně potřebujete k analýze. Například chcete znát strukturu vaší uživatele v roce narození, takže v úložišti dat profilu uživatele vyberete jenom narozeniny roky.
- Rozdělte data do částí a odešlete je do různých počítačů ke zpracování. Počítač A vypočítá počet osob s 1950-1959 daty, počítač B 1960-1969 atd. Tato skupina počítačů se nazývá *cluster Hadoop*.
- Výsledky každé části proveďte společně po zpracování částí. Teď máte poměrně krátký seznam toho, kolik lidí pro každý rok narození a úlohu výpočtu procent v tomto souhrnném seznamu můžete spravovat.

V Azure umožňuje [HDInsight](https://azure.microsoft.com/services/hdinsight/) zpracovávat, analyzovat a získávat nové poznatky z velkých objemů dat pomocí výkonného systému Hadoop. Můžete ho například použít k analýze protokolů webového serveru:

- Povolte protokolování webového serveru do svého účtu úložiště. Tím se nastaví Azure pro zápis protokolů do služby BLOB Service pro všechny požadavky HTTP do vaší aplikace. Služba BLOB je v podstatě cloudové úložiště souborů a integruje se s HDInsight.

    ![Protokoly, které se mají Blob Storage](data-storage-options/_static/image2.png)
- Jak aplikace získá přenos, protokoly IIS webového serveru se zapisují do úložiště objektů BLOB.

    ![Protokoly webového serveru](data-storage-options/_static/image3.png)
- Na portálu klikněte na **nový** - **Data Services** - **HDInsight** - **rychle vytvořit**a zadejte název clusteru HDInsight, velikost clusteru (počet datových uzlů clusteru HDInsight) a uživatelské jméno a heslo pro cluster HDInsight.

    ![HDInsight](data-storage-options/_static/image4.png)

Teď můžete nastavit úlohy MapReduce k analýze protokolů a získat odpovědi na otázky, jako jsou:

- Jakou dobu má moje aplikace největší nebo nejnižší přenos?
- Do kterých zemí přichází můj provoz?
- Jaký je průměrný okolní příjem oblastí, ze kterých pochází provoz. (K dispozici je veřejná datová sada, která vám poskytne okolní příjem podle IP adresy a můžete ji porovnat s IP adresou v protokolech webového serveru.)
- Jak Vzpadá na okolní příjem z různých stránek nebo produktů v lokalitě?

Pak můžete použít odpovědi na otázky, jako jsou tyto, na cílové inzeráty na základě pravděpodobnosti, že zákazník zajímá nebo chce koupit určitý produkt.

Jak je vysvětleno v [kapitole automatizace všeho](automate-everything.md), většina funkcí, které můžete provádět na portálu, může být automatizovaná a zahrnuje nastavení a provádění úloh analýzy HDInsight. Typický skript HDInsight může obsahovat následující kroky:

- Zřídí cluster HDInsight a propojí ho s vaším účtem úložiště pro vstup do úložiště objektů BLOB.
- Nahrajte do clusteru HDInsight spustitelné soubory úlohy MapReduce (soubory. jar nebo. exe).
- Odešlete MapReduce, který ukládá výstupní data do úložiště objektů BLOB.
- Počkejte, než se úloha dokončí.
- Odstraňte cluster HDInsight.
- Přístup k výstupu z úložiště objektů BLOB

Spuštěním skriptu, který to dělá, minimalizujete dobu, po kterou se cluster HDInsight zřídí, což minimalizuje vaše náklady.

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>Platforma jako služba (PaaS) versus infrastruktura jako služba (IaaS)

Níže uvedené možnosti úložiště dat zahrnují řešení typu platforma jako služba (PaaS) a IaaS (Infrastructure-as-a-Service). PaaS znamená, že spravujete hardwarovou a softwarovou infrastrukturu a právě ji využíváte. SQL Database je funkce PaaS v Azure. Vyžádáte si databáze a na pozadí Azure nastavíme a nakonfigurujeme virtuální počítače a nastavíte na nich databáze. Nemáte přímý přístup k virtuálním počítačům a nemusíte je spravovat. IaaS znamená, že nastavíte, nakonfigurujete a spravujete virtuální počítače, které běží v naší infrastruktuře datacenter, a na ně zadáte cokoli, co potřebujete. Poskytujeme galerii předem nakonfigurovaných imagí virtuálních počítačů pro běžné konfigurace virtuálních počítačů. Můžete například nainstalovat předem nakonfigurované image virtuálních počítačů pro Windows Server 2008, Windows Server 2012, BizTalk Server, Oracle WebLogic Server, Oracle Database atd.

PaaS data Solutions, která nabízí Azure, zahrnují:

- Azure SQL Database (dříve označované jako SQL Azure). Cloudová relační databáze založená na SQL Server.
- Úložiště tabulek Azure. Databáze NoSQL klíč/hodnota.
- Úložiště objektů BLOB v Azure Úložiště souborů v cloudu.

V případě IaaS můžete spustit cokoli, co můžete načíst do virtuálního počítače, například:

- Relační databáze, například SQL Server, Oracle, MySQL, SQL Compact, SQLite nebo Postgres.
- Úložiště dat klíč/hodnota, jako jsou memcached, Redis, Cassandra a Riak.
- Sloupce úložišť dat, jako jsou například HBA.
- Dokumenty, jako jsou MongoDB, RavenDB a CouchDB.
- Databáze grafů, jako je Neo4j.

![Možnosti úložiště dat v Azure](data-storage-options/_static/image5.png)

Možnost IaaS poskytuje skoro neomezené možnosti ukládání dat a mnoho z nich je zvlášť snadné, protože můžete vytvářet virtuální počítače pomocí předem nakonfigurovaných imagí. Například na portálu pro správu přejděte na **Virtual Machines**, klikněte na kartu **bitové kopie** a klikněte na **Procházet virtuální počítač**.

![Procházet skladiště VM](data-storage-options/_static/image6.png)

Pak se zobrazí seznam [stovek předkonfigurovaných imagí virtuálních počítačů](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx)a můžete vytvořit virtuální počítač z image, která má předinstalovaného systému správy databáze, jako je například MongoDB, Neo4J, Redis, Cassandra nebo CouchDB:

![MongoDB ve skladu VM](data-storage-options/_static/image7.png)

Azure poskytuje IaaS možnosti úložiště dat co nejjednodušší, ale nabídky PaaS mají spoustu výhod, díky kterým jsou cenově výhodné a praktické pro mnoho scénářů:

- Nemusíte vytvářet virtuální počítače. k nastavení úložiště dat stačí použít portál nebo skript. Pokud chcete úložiště dat 200 terabajtů, stačí kliknout na tlačítko nebo spustit příkaz a v sekundách je připraveno k použití.
- Nemusíte spravovat ani opravovat virtuální počítače používané službou. Microsoft to dělá automaticky. – nemusíte si dělat starosti s nastavením infrastruktury pro škálování nebo vysokou dostupnost; Microsoft to všechno zpracuje za vás.
- Nemusíte kupovat licence. licenční poplatky jsou zahrnuté do poplatků za službu.
- Platíte jenom za to, co používáte.

PaaS možnosti úložiště dat v Azure zahrnují nabídky poskytovatelů třetích stran. Můžete například vybrat [doplněk MongoLabu](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/) z Azure Store a zřídit databázi MongoDB jako službu.

## <a name="choosing-a-data-storage-option"></a>Výběr možnosti úložiště dat

Žádný z přístupů není pro všechny scénáře správný. Pokud každý z nich uvádí, že je tato technologie odpověď, první věc, kterou je třeba zeptat, je "Co je otázka?", protože různá řešení jsou optimalizovaná pro různé věci. Relační model má určité výhody; To je důvod, proč je to pro dlouhou dobu. Existují však také mimo jiné na SQL, které lze řešit pomocí řešení NoSQL.

Často, co vidíte, je nejlepší způsob, jak se v jednom řešení používají SQL a NoSQL. I když uživatelé říkají, že jsou přechodu NoSQL, pokud si provedete další informace o tom, co dělají, často zjistíte, že používají několik různých NoSQL platforem: používají [CouchDB](http://wiki.apache.org/couchdb/Introduction)a [Redis](http://redis.io/)a [Riak](http://basho.com/riak/) pro různé věci. Dokonce i Facebook, který používá NoSQL, používá pro různé části služby jiné architektury NoSQL. Jednou z věcí, které jsou v cloudu Skvělé, je flexibilní flexibilita a přístup k nim, protože je snadné použít více datových řešení a integrovat je do jediné aplikace.

Tady jsou některé otázky, které je potřeba vzít v úvahu při výběru přístupu:

| Sémantika dat | – Jaká je základní sémantika úložiště dat a přístupu k datům (ukládáte relační nebo nestrukturovaná data)? Nestrukturovaná data, jako jsou mediální soubory, se nejlépe hodí pro úložiště objektů BLOB; kolekce souvisejících dat, jako jsou produkty, inventáře, dodavatelé, zákaznické objednávky atd., se nejlépe hodí v relační databázi. |
| --- | --- |
| Podpora dotazů | – Jak snadné je dotazování dat? – Jaké typy otázek se dají efektivně zeptat? Úložiště dat klíč/hodnota jsou velmi dobrá při získávání hodnoty klíče na jeden řádek, ale ne tak dobré pro složité dotazy. Pro úložiště dat profilu uživatele, kde vždycky získáváte data pro jednoho konkrétního uživatele, by úložiště dat klíč/hodnota mohlo dobře fungovat; v případě katalogu produktů, kde chcete získat různá seskupení na základě různých atributů produktu, může relační databáze lépe fungovat. Databáze NoSQL můžou efektivně ukládat velké objemy dat, ale je nutné strukturu databáze strukturovat, jak se aplikace dotazuje na data, a díky tomu je to obtížnější provádět ad hoc dotazy. V případě relační databáze můžete sestavit skoro jakýkoli typ dotazu. |
| Funkční projekce | – Možné dotazy, agregace atd., spustit na straně serveru? Když z tabulky v SQL Spouštím\*COUNT (), bude velmi efektivně provádět veškerou práci na serveru a vracet číslo, které hledáte. Pokud chci stejný výpočet z úložiště dat NoSQL, které nepodporuje agregaci, jedná se o neefektivní dotaz bez vazby a pravděpodobně vyprší časový limit. I v případě, že je dotaz úspěšný, je nutné načíst všechna data ze serveru do klienta a spočítat řádky v klientovi. – Jaké jazyky nebo typy výrazů lze použít? Pomocí relační databáze můžu použít SQL. S některými NoSQL databázemi, jako je Azure Table Storage, používám [OData](http://www.odata.org/)a všechno, co můžu udělat, je vyfiltrovat primární klíč a získat projekce (vyberte podmnožinu dostupných polí). |
| Snadná škálovatelnost | – Jak často a kolik bude nutné data škálovat? – Platforma nativně implementuje horizontální navýšení kapacity? – Jak snadné je přidat nebo odebrat kapacitu (velikost a propustnost)? Relační databáze a tabulky nejsou automaticky rozděleny, aby byly škálovatelné, takže je obtížné škálovat nad rámec určitých omezení. NoSQL úložiště dat, jako je Azure Table Storage, vše vše do celého oddílu a pro přidávání oddílů téměř není nijak omezené. Můžete snadno škálovat Table Storage až 200 terabajtů, ale maximální velikost databáze pro Azure SQL Database je 500 gigabajtů. Relační data můžete škálovat jejich rozdělením do více databází, ale nastavením aplikace pro podporu tohoto modelu zahrnuje spoustu programovací práce. |
| Instrumentace a možnosti správy | – Jak snadné je platforma pro instrumentaci, monitorování a správu? Budete si muset informovat o stavu a výkonu úložiště dat, abyste měli jistotu, co vám vám poskytne metrika, kterou vám platforma poskytuje zdarma, a co je potřeba vyvíjet sami. |
| Operace | – Jak snadné je platforma pro nasazení a spouštění v Azure? PaaS? IaaS? Linux? Table Storage a SQL Database se snadno nastavují v Azure. Platformy, které nejsou integrovanými řešeními Azure PaaS, vyžadují více úsilí. |
| Podpora rozhraní API | – Je dostupné rozhraní API, které usnadňuje práci s platformou? Pro službu Azure Table je k dispozici sada SDK s rozhraním .NET API, které podporuje asynchronní programovací model .NET 4,5. Pokud píšete aplikaci .NET, bude mnohem snazší psát a testovat kód pro službu Azure Table ve srovnání s jinou platformou úložiště dat ve sloupci klíč/hodnota, která nemá žádné rozhraní API nebo méně komplexní. |
| Integrita transakcí a konzistence dat | – Je důležité, aby platforma podporovala transakce, aby se zajistila konzistence dat? Pro udržení přehledu o odeslaných hromadných e-mailech může být výkon a náklady na úložiště dat důležitější než Automatická podpora pro transakce nebo referenční integrita v datové platformě, což znamená, že služba Azure Table je vhodnou volbou. Pro sledování zůstatků bankovních účtů nebo nákupních objednávek může být lepší volbou platforma relačních databází, která poskytuje silné transakční záruky. |
| Kontinuita podnikových procesů | – Jak snadné je zálohování, obnovování a zotavení po havárii? Dřív nebo novější produkční data budou poškozená a budete potřebovat funkci vrátit zpátky. Relační databáze často obsahují přesnější možnosti obnovení, jako je například možnost obnovení k určitému bodu v čase. Porozumění funkcím obnovení, které jsou k dispozici na každé platformě, kterou zvažujete, je důležitým faktorem, který je třeba zvážit. |
| Náklady | – Pokud více než jedna platforma může podporovat datovou úlohu, jak se porovnávají s náklady? Pokud například použijete ASP.NET Identity, můžete ukládat data profilu uživatele ve službě Azure Table Service nebo v Azure SQL Database. Pokud nepotřebujete zařízení s bohatou dotazováním SQL Database, můžete zvolit tabulky Azure v části, protože za dané množství úložiště stojí mnohem méně. |

Obecně doporučujeme znát odpověď na otázky v každé z těchto kategorií ještě předtím, než zvolíte řešení úložiště dat.

Kromě toho vaše zatížení může mít specifické požadavky, které mohou některé platformy podporovat lépe než jiné. Příklad:

- Vyžaduje vaše aplikace možnosti auditu?
- Jaké jsou vaše požadavky na data longevity – vyžadujete automatické archivování nebo vyprazdňování funkcí?
- Máte specializované požadavky na zabezpečení? Data například zahrnují PII (identifikovatelné osobní údaje), ale musíte být schopni zajistit, aby PII bylo vyloučeno z výsledků dotazu.
- Pokud máte nějaká data, která nejdou Uložit do cloudu, pokud jde o regulativní nebo technologický důvod, možná budete potřebovat cloudovou platformu pro úložiště dat, která usnadňuje integraci s místním úložištěm.

## <a name="demo--using-sql-database-in-azure"></a>Ukázka – používání SQL Database v Azure

Aplikace opravit IT používá k ukládání úkolů relační databázi. Skript prostředí Windows PowerShell pro vytvoření prostředí zobrazený v [části automatizovat vše](automate-everything.md) vytvoří dvě instance SQL Database. Můžete je zobrazit na portálu kliknutím na kartu **databáze SQL** .

![Databáze SQL na portálu](data-storage-options/_static/image8.png)

Je také snadné vytvořit databáze pomocí portálu.

Klikněte na **Nový--Data Services** -- **SQL Database** -- **rychle vytvořit**, zadejte název databáze, vyberte server, který už máte ve svém účtu, nebo vytvořte nový a klikněte na **vytvořit SQL Database**.

![Nová databáze SQL](data-storage-options/_static/image9.png)

Počkejte několik sekund a máte k dispozici databázi v Azure, kterou můžete použít.

![Vytvořil se nový SQL Database.](data-storage-options/_static/image10.png)

Takže Azure provede během několika sekund, které vám může trvat jeden den nebo týden nebo déle v místním prostředí. A vzhledem k tomu, že můžete stejně snadno vytvářet databáze automaticky ve skriptu nebo pomocí rozhraní API pro správu, můžete dynamicky škálovat rozšířením dat napříč více databázemi, pokud je vaše aplikace pro tuto aplikaci naprogramovaná.

Toto je příklad našeho modelu platformy jako služby. Nemusíte spravovat servery, my to máme. Nemusíte se starat o zálohování, my to máme. Je spuštěná ve vysoké dostupnosti – data v databázi se replikují na tři servery automaticky. Pokud počítač zemře, automaticky převezme služby při selhání a ztratíte žádná data. Server je pravidelně opravený, nemusíte se o to starat.

Klikněte na tlačítko a získáte přesný připojovací řetězec, který potřebujete, a můžete hned začít používat novou databázi.

![Připojovací řetězce](data-storage-options/_static/image11.png)

Řídicí panel zobrazuje historii připojení a velikost využitého úložiště.

![Řídicí panel SQL Database](data-storage-options/_static/image12.png)

Databáze můžete spravovat na portálu nebo pomocí SQL Serverch nástrojů, které už znáte, včetně SQL Server Management Studio (SSMS) a sady Visual Studio Tools Průzkumník objektů systému SQL Server (SSOX) a Průzkumník serveru.

![SSOX](data-storage-options/_static/image13.png)

Dalším dobrým aspektem je cenový model. Můžete začít vývoj s využitím bezplatné databáze 20 MB a provozní databáze začíná přibližně $5 měsíčně. Platíte jenom za objem dat, která ve skutečnosti ukládáte v databázi, a ne na maximální kapacitu. Nemusíte kupovat licenci.

SQL Database se snadno škáluje. V případě aplikace opravit IT je databáze vytvořená v našem skriptu pro automatizaci omezené na 1 4gigový. Pokud ho chcete škálovat až na 150 4gigový, můžete jednoduše přejít na portál a změnit toto nastavení, nebo spustit příkaz REST API a v sekundách máte databázi 150 4gigový, do které můžete nasadit data.

![SQL Database edice a velikosti](data-storage-options/_static/image14.png)

To je síla cloudu, která umožňuje rychle a snadno a okamžitě začít používat infrastrukturu.

Aplikace pro opravu IT používá dvě databáze SQL, jednu pro členství (ověřování a autorizaci) a jednu pro data a je to vše, co musíte udělat, abyste ji zřídili a mohli škálovat. Dříve jste viděli, jak zřídit databáze prostřednictvím skriptů prostředí Windows PowerShell, a teď jste viděli, jak snadné je na portálu.

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>Entity Framework versus přímý přístup k databázi pomocí ADO.NET

Oprava aplikace IT přistupuje k těmto databázím pomocí Entity Framework, doporučeného ORM od Microsoftu (Object-relační Mapovač) pro aplikace .NET. ORM je skvělý nástroj, který usnadňuje produktivitu vývojářů, ale produktivita v některých případech přináší náklady na snížený výkon. V reálné cloudové aplikaci nebudete volit mezi použitím EF nebo přímo pomocí ADO.NET – budete používat obojí. Ve většině případů při psaní kódu, který pracuje s databází, je získání maximálního výkonu nekritické a můžete využít výhod zjednodušeného kódování a testování, které získáte s Entity Framework. V situacích, kdy režie EF by způsobila nepřijatelný výkon, můžete napsat a spustit vlastní dotazy pomocí ADO.NET, a to v ideálním případě voláním uložených procedur.

Bez ohledu na to, jakou metodu používáte pro přístup k databázi, chcete co nejvíc minimalizovat "upovídanost". Jinými slovy, pokud můžete získat všechna data, která potřebujete v jedné sadě výsledků dotazu, a ne desítky nebo stovky menších, což je obvykle vhodnější. Pokud potřebujete například vypsat studenty a kurzy, které jsou zaregistrované v, je obvykle lepší získat všechna data v jednom dotazu join, ale Nezískávat studenty v jednom dotazu a provádět samostatné dotazy pro kurzy každého studenta.

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>Databáze SQL a Entity Framework v aplikaci Fix it

V aplikaci opravit IT třídu `FixItContext`, která je odvozena z třídy Entity Framework `DbContext`, identifikuje databázi a určuje tabulky v databázi. Kontext určuje sadu entit (tabulka) pro úkoly a kód předá do kontextu název připojovacího řetězce. Tento název odkazuje na připojovací řetězec, který je definován v souboru Web. config.

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

Připojovací řetězec v souboru *Web. config* má název AppDB (odkazuje na místní vývojovou databázi):

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

Entity Framework vytvoří tabulku *FixItTasks* na základě vlastností obsažených ve třídě `FixItTask` entity. Toto je jednoduchý objekt třídy POCO (prostý starý objekt CLR), což znamená, že nedědí z nebo nemá žádné závislosti na Entity Framework. Ale Entity Framework ví, jak na základě IT vytvořit tabulku a jak s ní provést operace CRUD (vytvořit-čtení-aktualizace-odstranění).

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![Tabulka FixItTasks](data-storage-options/_static/image15.png)

Oprava IT aplikace zahrnuje rozhraní úložiště, které používá pro operace CRUD při práci s úložištěm dat.

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

Všimněte si, že metody úložiště jsou všechny asynchronní, takže veškerý přístup k datům je možné provést kompletně asynchronním způsobem.

Implementace úložiště volá Entity Framework asynchronní metody pro práci s daty, včetně dotazů LINQ a operací vložení, aktualizace a odstranění. Zde je příklad kódu pro vyhledání úlohy opravy IT.

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

Všimněte si, že tady je také nějaký kód pro načasování a protokolování chyb. podíváme se na to později v [části monitorování a telemetrie](monitoring-and-telemetry.md).

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>Volba SQL Database (PaaS) oproti SQL Server ve virtuálním počítači (IaaS) v Azure

Skvělé SQL Server a Azure SQL Database je, že základní programovací model pro oba z nich je identický. V obou prostředích můžete použít většinu stejných dovedností. Můžete dokonce použít SQL Server databázi ve vývoji a instanci SQL Database v cloudu, což je způsob, jakým se nastavuje aplikace pro opravu IT.

Alternativně můžete spustit stejný SQL Server v cloudu, který spouštíte místně, a to tak, že ho nainstalujete na virtuální počítače s IaaS. U některých starších aplikací může být pro spuštění SQL Server ve virtuálním počítači lepší řešení. Vzhledem k tomu, že se databáze SQL Server spouští na vyhrazeném virtuálním počítači, má k ní k dispozici více prostředků než databáze SQL Database, která běží na sdíleném serveru. To znamená, že databáze SQL Server může být větší a stále dobře fungovat. Obecně platí, že menší velikost databáze a velikost tabulky, což je lepší případ použití pro SQL Database (PaaS).

Tady je několik pokynů pro výběr mezi těmito dvěma modely.

| Azure SQL Database (PaaS) | SQL Server ve virtuálním počítači (IaaS) |
| --- | --- |
| **Specialisté** – nemusíte vytvářet ani spravovat virtuální počítače, aktualizace nebo opravy operačního systému ani SQL; Azure to udělá za vás. – Integrovaná vysoká dostupnost s smlouvou SLA na úrovni databáze. – Nízké celkové náklady na vlastnictví, protože platíte jenom za to, co používáte (není nutná žádná licence). – Dobré pro zpracování velkých čísel menších databází (&lt;= 500 GB). – Snadno se dá dynamicky vytvářet nové databáze a povolit horizontální navýšení kapacity. | ***Specialisté*** – funkce kompatibilní s místními SQL Server. – Dá se implementovat SQL Server [vysoké dostupnosti přes AlwaysOn](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx) ve dvou a virtuálních počítačích s SLA na úrovni virtuálních počítačů. – Máte plnou kontrolu nad tím, jak se SQL spravuje. – Může znovu použít licence SQL, které už vlastníte, nebo platíte za jednu hodinu. -Dobrý pro zpracování méně než větších databází (1 TB +). |
| **Nevýhody** – některé funkce v porovnání s místními SQL Server (nedostatek [integrace CLR](https://technet.microsoft.com/library/ms131102.aspx), [TDE](https://technet.microsoft.com/library/bb934049.aspx), [kompresní podpora](https://technet.microsoft.com/library/cc280449.aspx), [SQL Server Reporting Services](https://technet.microsoft.com/library/ms159106.aspx)atd.) – omezení velikosti databáze 500 GB. | ***Nevýhody*** – aktualizace a opravy (operační systém a SQL) jsou vaší zodpovědností – vytváření a Správa databáze jsou vaší zodpovědností – diskové vstupně-výstupní operace (vstupně-výstupní operace za sekundu) omezené na přibližně 8000 (přes 16 datových jednotek). |

Pokud chcete použít SQL Server na virtuálním počítači, můžete použít vlastní licenci SQL Server nebo ji můžete platit za jednu hodinu. Například na portálu nebo prostřednictvím REST API můžete vytvořit nový virtuální počítač pomocí SQL Server Image.

![Vytvoření virtuálního počítače s SQL Server](data-storage-options/_static/image16.png)

![Seznam imagí SQL Server VM](data-storage-options/_static/image17.png)

Když vytvoříte virtuální počítač s bitovou kopií SQL Server, průběžně vám náklady na SQL Server licence budou za hodinu na základě vašeho využití virtuálního počítače. Pokud máte projekt, který se bude spouštět jenom po několik měsíců, je levnější uhradit hodinu. Pokud si myslíte, že váš projekt bude trvat až let, je levnější koupit si licenci obvyklým způsobem.

## <a name="summary"></a>Souhrn

Cloud Computing usnadňuje kombinaci a porovnávání přístupů do úložiště dat, aby nejlépe vyhovoval potřebám vaší aplikace. Pokud vytváříte novou aplikaci, pečlivě si promyslete otázky, které jsou tady uvedené, aby bylo možné vybrat přístupy, které budou fungovat i v případě, že vaše aplikace roste. V [Další části](data-partitioning-strategies.md) se vysvětlují některé strategie dělení, které můžete použít ke kombinování více přístupů k úložišti dat.

## <a name="resources"></a>Prostředky

Další informace najdete v následujících materiálech.

Výběr databázové platformy:

- [Přístup k datům pro vysoce škálovatelná řešení: používání SQL, NoSQL a trvalosti Polyglot](https://aka.ms/dag-doc). Elektronická kniha podle vzorů a postupů od Microsoftu, které jsou podrobně v různých druzích úložišť dat pro cloudové aplikace.
- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/ff898430.aspx) Podívejte se na Úvod do konzistence dat, pokyny pro replikaci a synchronizaci dat, model tabulky s Materializací, model materializované zobrazení.
- [Základní: kyselá alternativa](http://queue.acm.org/detail.cfm?id=1394128). Článek o kompromisech mezi konzistencí a škálovatelností dat
- [Sedm databází za sedm týdnů: Průvodce moderními databázemi a pohyb NoSQL](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921). Book by Eric Redmond a jim R. Wilson. Důrazně doporučujeme, abyste se seznámili s rozsahem dostupných platforem úložiště dat, které jsou dnes k dispozici.

Výběr mezi SQL Server a SQL Database:

- [Premium Preview pro SQL Database doprovodné](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)materiály. Úvod do SQL Database úrovně Premium a pokyny k tomu, kdy si je můžete vybrat přes SQL Database web a obchodní edice.
- [Pokyny a omezení (Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx). Stránka portálu, která odkazuje na dokumentaci týkající se omezení SQL Database, včetně těch, které se zaměřují na SQL Server funkce, které SQL Database nepodporují.
- [SQL Server ve službě Azure Virtual Machines](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx). Stránka portálu, která odkazuje na dokumentaci týkající se spuštění SQL Server v Azure.
- [Scott Guthrie vysvětluje databáze SQL v Azure](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/). 6\. Úvod k videu SQL Database Scottem Guthrie.
- [Modely aplikací a vývojové strategie pro SQL Server v Azure Virtual Machines](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx).

Používání Entity Framework a SQL Database ve webové aplikaci v ASP.NET

- [Začínáme s EF 6 pomocí MVC 5](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Devět kurzů, které vás provedou vytvořením aplikace MVC, která používá EF, a nasadí databázi do Azure a SQL Database.
- [ASP.NET nasazení webu pomocí sady Visual Studio](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). 12. série kurzů, které se podrobněji týkají nasazení databáze pomocí Code First EF.
- [Nasaďte zabezpečenou aplikaci ASP.NET MVC 5 s členstvím, protokolem OAuth a SQL Database na web Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/). Podrobný kurz, který vás provede vytvořením webové aplikace, která používá ověřování, ukládá tabulky aplikací v databázi členství, mění schéma databáze a nasadí aplikaci do Azure.
- [Mapa obsahu ASP.NET Data Access](https://go.microsoft.com/fwlink/p/?LinkId=282414). Odkazuje na prostředky pro práci s EF a SQL Database.

Používání MongoDB v Azure:

- [MongoLabu-MongoDB v Azure](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/). Stránka portálu pro dokumentaci ke spuštění MongoDB v Azure
- [Vytvořte web Azure, který se připojí k MongoDB běžícímu na virtuálním počítači v Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/). Podrobný kurz, ve kterém se dozvíte, jak používat databázi MongoDB ve webové aplikaci v ASP.NET.

HDInsight (Hadoop v Azure):

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/). Dokumentace k portálu HDInsight na webu [Azure](https://azure.microsoft.com/) .
- [Hadoop a HDInsight: velké objemy dat v Azure](https://msdn.microsoft.com/magazine/dn385705.aspx). Článek na webu MSDN Magazine od Bruno Terkaly a Ricardo Villalobos a Představujeme Hadoop v Azure.
- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Viz MapReduce vzor.

> [!div class="step-by-step"]
> [Předchozí](single-sign-on.md)
> [Další](data-partitioning-strategies.md)
