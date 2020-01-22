---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: Strategie dělení dat (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: b8c901ec30b6d37237f80100a2978350ac389b7a
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519164"
---
# <a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>Strategie dělení dat (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o řadě najdete v [první kapitole](introduction.md).

Dříve jsme viděli, jak snadné je škálovat webovou vrstvu cloudové aplikace tím, že přidáte a odeberete webové servery. Pokud ale všechny mají stejné úložiště dat, vaše kritická místa vaší aplikace se pohybují od front-endu po back-endu a Datová vrstva je nejzávažnější pro škálování. V této kapitole se podíváme na to, jak můžete vytvořit škálovatelnou datovou vrstvu pomocí dělení dat do několika relačních databází nebo kombinací relačního úložiště databáze s dalšími možnostmi úložiště dat.

Nastavení schématu dělení se nejlépe dokončí na stejný důvod zmíněný výše: je velmi obtížné změnit strategii úložiště dat, když je aplikace v produkčním prostředí. Pokud si myslíte, že zadáte nadzávažnější informace o různých přístupech, můžete se vyhnout tomu, že při selhání aplikace nebo při změně uspořádání dat aplikace a kódu přístupu k datům dojde k delší době.

## <a name="the-three-vs-of-data-storage"></a>Tři datové úložiště v vs.

Abyste zjistili, jestli potřebujete strategii dělení a co by měla být, zvažte tři otázky týkající se vašich dat:

- Volume – kolik dat budete nakonec ukládat? Pár gigabajtů? Pár stovek gigabajtů? Terabajtů? Petabajty?
- Rychlost – jakou rychlost budou vaše data růst? Je to interní aplikace, která negeneruje hodně dat? Externí aplikace, do které budou zákazníci nahrávat obrázky a videa?
- Různé – jaký typ dat budete ukládat? Relační, image, páry klíč-hodnota, sociální grafy?

Pokud si myslíte, že budete mít spoustu objemů, rychlostí nebo rozmanitosti, musíte pečlivě zvážit, jaký druh schématu dělení bude nejlépe umožňovat efektivní a efektivní škálování vaší aplikace, a zajistit, aby nedošlo k žádným kritickým bodům.

Vytváření oddílů má v podstatě tři přístupy:

- Vertikální dělení
- Horizontální dělení
- Hybridní dělení

## <a name="vertical-partitioning"></a>Vertikální dělení

Svislá část je podobná rozdělení tabulky po sloupcích: jedna sada sloupců přejde do jednoho úložiště dat a další sada sloupců přejde do jiného úložiště dat.

Předpokládejme například, že moje aplikace ukládá data o lidech, včetně obrázků:

![Tabulka dat](data-partitioning-strategies/_static/image1.png)

Když tato data reprezentujete jako tabulku a můžete se podívat na různé odrůdy dat, vidíte, že tři sloupce na levé straně obsahují řetězcová data, která je možné efektivně ukládat relační databází, zatímco dva sloupce na pravé straně mají v podstatě Bajtová pole, která c teré z obrazových souborů. Je možné ukládat data souborů obrázků do relační databáze a mnoho lidí to udělat, protože nechtějí ukládat data do systému souborů. Nemusí mít systém souborů schopný ukládat požadované objemy dat nebo nemusí spravovat samostatný systém zálohování a obnovení. Tento přístup funguje dobře pro místní databáze a pro malé objemy dat v cloudových databázích. V místním prostředí může být snazší, aby se usnadnilo, aby se zjednodušilo všechno, co je potřeba.

Ale v cloudové databázi je úložiště poměrně nákladné a velký objem imagí může způsobit, že velikost databáze přesáhne limity, při kterých může fungovat efektivně. Tyto problémy můžete vyřešit vertikálním rozdělením dat, což znamená, že pro každý sloupec v tabulce dat vyberete nejvhodnější úložiště dat. To, co by mohlo být pro tento příklad fungovat nejlépe, je vložení řetězcových dat do relační databáze a imagí v úložišti objektů BLOB.

![Tabulka dat svisle rozdělená na oddíly](data-partitioning-strategies/_static/image2.png)

Ukládání imagí v BLOB Storage místo databáze je v cloudu více praktické, než v místním prostředí, protože se nemusíte starat o nastavení souborových serverů nebo správu zálohování a obnovení dat uložených mimo relační databázi: vše Tím se automaticky zpracuje služba BLOB Storage.

Toto je přístup k dělení, který jsme implementovali v aplikaci pro opravu IT, a podíváme se na kód, který najdete v [kapitole BLOB Storage](unstructured-blob-storage.md). Bez tohoto schématu dělení a za předpokladu, že průměrná velikost Image je 3 MB, bude aplikace Fix it moct Uložit asi 40 000 úloh jenom předtím, než zasáhne maximální velikost databáze 150 gigabajtů. Po odebrání imagí může databáze aplikace uložit 10 časů jako mnoho úkolů. než se budete muset zamyslet na implementaci horizontálního schématu dělení, můžete to trvat mnohem déle. A když se aplikace škáluje, vaše náklady se budou považovat pomaleji, protože hromadné požadavky na úložiště se blíží velmi levnému úložišti objektů BLOB.

## <a name="horizontal-partitioning-sharding"></a>Horizontální dělení (sharding)

Vodorovná část je podobná rozdělení tabulky podle řádků: jedna sada řádků přejde do jednoho úložiště dat a další sada řádků přejde do jiného úložiště dat.

Vzhledem k tomu, že stejná sada dat je, Další možností je uložit různé rozsahy názvů zákazníků do různých databází.

![Tabulka dat horizontálně rozdělená](data-partitioning-strategies/_static/image3.png)

Pokud chcete zajistit, aby se data rovnoměrně rozhorizontálního dělenía, aby se předešlo značným skvrnám, měli byste být velmi opatrní. Tento jednoduchý příklad s použitím prvního písmene posledního názvu nesplňuje tento požadavek, protože příjmení, která začínají některými běžnými písmeny, má několik lidí. Měli byste využít omezení velikosti tabulky starší, než byste očekávali, protože některé databáze by byly velmi velké, zatímco většina by zůstala malá.

Vedlejší stranou horizontálního dělení na oddíly je, že může být obtížné provádět dotazy napříč všemi daty. V tomto příkladu by se dotaz musel nakreslit od až 26 různých databází, aby se získala všechna data, která aplikace ukládá.

## <a name="hybrid-partitioning"></a>Hybridní dělení

Můžete zkombinovat vertikální a horizontální dělení. V ukázkových datech například můžete ukládat obrázky do úložiště objektů BLOB a horizontálně rozdělit data řetězců.

![Hybridní oddíly v tabulce dat](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>Dělení produkční aplikace

V konceptuální části je snadné zjistit, jak funguje schéma dělení, ale jakékoli schéma dělení zvyšuje složitost kódu a zavádí mnoho nových komplikací, které je třeba řešit. Pokud přesouváte image do úložiště objektů blob, co uděláte při nečinnosti služby úložiště? Jak zvládnout zabezpečení objektů BLOB? Co se stane, když se databáze a úložiště objektů BLOB vystanou nesynchronizovanými? Pokud jste horizontálního dělení, jak budete zpracovávat dotazy napříč všemi databázemi?

Komplikace je možné spravovat tak dlouho, dokud je naplánujete před přechodem do produkčního prostředí. Spousta lidí, kteří si ji neudělali později. V průměru náš tým pro poradenské zákazníky (CAT) panicked telefonní hovory o jednou měsíčně od zákazníků, jejichž aplikace se ve skutečnosti vybírají a nevedly k tomuto plánování. A říkají něco jako: "Help! Všechno je v jednom úložišti dat a během 45 dnů se na něj nespouští místo. " A pokud máte spoustu obchodní logiky, kterou máte k dispozici v tom, jak přistupujete k úložišti dat a máte zákazníky, kteří používají vaši aplikaci, nemusíte v průběhu migrace přejít na denní dobu. Provedeme vás herculean úsilím, abychom zákazníkům usnadnili rozdělení jejich dat bez výpadku. Je velmi zajímavá a velmi scaryá a nejedná se o něco, co byste chtěli mít v situaci, kdy se můžete vyhnout! Zamyslete se nad tím a integrací IT do vaší aplikace, takže když se aplikace později rozroste, pomůže vám to být mnohem jednodušší.

## <a name="summary"></a>Přehled

Efektivní schéma dělení umožňuje, aby se vaše cloudová aplikace mohla škálovat tak, aby petabajty data v cloudu bez kritických míst. A nemusíte platit předem pro obrovské počítače nebo rozsáhlou infrastrukturu, protože byste aplikaci spustili v místním datovém centru. V cloudu můžete postupně přidávat kapacitu, jak ji budete potřebovat, a platíte jenom za to, jak budete používat.

V [Další části](unstructured-blob-storage.md) se dozvíte, jak aplikace pro opravu IT implementuje vertikální dělení tím, že ukládá obrázky do úložiště objektů BLOB.

## <a name="resources"></a>Prostředky

Další informace o strategiích dělení naleznete v následujících zdrojích informací.

Dokumentace:

- [Osvědčené postupy pro návrh rozsáhlých služeb na platformě Windows Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Dokument White Paper, který označuje Simms a Michael Thomassy.
- [Vzory a postupy Microsoft – vzory návrhu pro Cloud](https://msdn.microsoft.com/library/dn568099.aspx) Viz pokyny k dělení dat, horizontálního dělení vzor.

Videa:

- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět částí podle Ulrich Homann, matolin Mercuri a označit Simms. Prezentuje základní koncepty a principy architektury v rámci velmi přístupného a zajímavého způsobu, který vychází ze zkušeností zákazníků Microsoftu pro poradenské zákazníky (CAT) se skutečnými zákazníky. Viz diskuzi o dělení ve epizodě 7.
- [Sestavování velkých: lekcí získaných od zákazníků Windows Azure – část I](https://channel9.msdn.com/Events/Build/2012/3-029). Označení Simms popisuje schémata dělení, strategie horizontálního dělení, způsob implementace horizontálního dělení a SQL Databasech federace od 19:49. Podobně jako u řady Failsafe, ale odkazuje na další podrobnosti.

Vzorový kód:

- [Základy cloudových služeb v systému Windows Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Ukázková aplikace, která obsahuje databázi horizontálně dělené Popis implementovaného schématu horizontálního dělení najdete v tématu [dal – horizontálního dělení of RDBMS](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) na blogu Windows Azure.

> [!div class="step-by-step"]
> [Předchozí](data-storage-options.md)
> [Další](unstructured-blob-storage.md)
