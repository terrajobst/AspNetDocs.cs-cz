---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: Návrh pro dosažení selhání (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: 348232af531b5d53dc3cb46d6d2c7931d95a572d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457125"
---
# <a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>Návrh pro dosažení selhání (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Jedna z věcí, které je třeba vzít v úvahu při sestavování libovolného typu aplikace, ale zvláště z nich, která bude běžet v cloudu, kde ji bude používat spousta lidí, je návrh aplikace, aby mohl řádně zpracovat selhání a dál doručovat hodnoty, a to co nejvíc. provést. Vzhledem k dostatečnému času jsou věci v jakémkoli prostředí nebo jakémkoli softwarovém systému nesprávné. Jak vaše aplikace zpracovává tyto situace, určuje, jak dlouho budou vaši zákazníci získávat a kolik času je potřeba věnovat analýze a opravám problémů.

## <a name="types-of-failures"></a>Typy selhání

Existují dvě základní kategorie selhání, které chcete zpracovat odlišně:

- Přechodné, samočinné chyby, jako například občasné problémy s připojením k síti.
- Dlouhodobá selhání, která vyžadují zásah.

V případě přechodného selhání můžete implementovat zásady opakování, abyste zajistili, že většina času rychle a automaticky obnovuje aplikaci. Vaši zákazníci si můžou všimnout trochu delší doby odezvy, jinak to neovlivní. Ukážeme několik způsobů, jak tyto chyby zpracovat v [kapitole s přechodným zpracováním chyb](transient-fault-handling.md).

V případě neúspěchů můžete implementovat funkci monitorování a protokolování, která vás upozorní, když dojde k problémům a která usnadňuje analýzu původní příčiny. Ukážeme několik způsobů, které vám pomůžou udržet si přehled o těchto druzích chyb v části [monitorování a telemetrie](monitoring-and-telemetry.md).

## <a name="failure-scope"></a>Rozsah selhání

Také je nutné se zamyslet na rozsah selhání – ať už je to ovlivněný jednotlivý počítač, celou službu, jako je například SQL Database nebo úložiště nebo celá oblast.

![Rozsah selhání](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>Selhání počítačů

V Azure se server, který selhal, automaticky nahrazuje novým a dobře navrženou cloudovou aplikací z tohoto typu selhání automaticky a rychle. Dříve jsme zdůraznili výhody škálovatelnosti bezstavových webových vrstev a snadné obnovení z neúspěšného serveru je další výhodou Statelessness. Snadné obnovení je také jednou z výhod funkcí PaaS (Platform-as-a-Service), jako jsou SQL Database a Azure App Service Web Apps. Chyby hardwaru jsou zřídka, ale když k nim dojde, jsou automaticky zpracovány. dokonce nemusíte psát kód pro zpracování selhání počítače při použití některé z těchto služeb.

### <a name="service-failures"></a>Selhání služby

Cloudové aplikace obvykle používají více služeb. Třeba aplikace pro opravu IT používá službu SQL Database, služba úložiště a webová aplikace se nasadí do Azure App Service. Co vaše aplikace udělá v případě, že jedna ze služeb, na které závisí, se nezdaří? U některých chyb služby se může stát, že to bude nejlepší, ale zkuste to znovu později. Ale v mnoha scénářích to můžete dělat lépe. Například když vaše back-endové úložiště dat nefunguje, můžete přijmout uživatelský vstup, zobrazit "vaši žádost byla přijata" a dočasně uložit vstup někde došlo jinak; až bude služba, kterou potřebujete, zase funkční, můžete načíst vstup a zpracovat ho.

V kapitole [pracovní vzor orientovaný na fronty](queue-centric-work-pattern.md) se zobrazuje jeden ze způsobů, jak tento scénář zpracovat. Aplikace opravit IT ukládá úkoly v SQL Database, ale není nutné, aby při SQL Database mimo provoz ukončili práci. V této kapitole se dozvíte, jak uložit vstup uživatele pro úkol ve frontě a použít pracovní proces ke čtení fronty a aktualizaci úlohy. Pokud je SQL mimo provoz, možnost vytvářet opravy IT úkoly není nijak ovlivněna; pracovní proces může čekat a zpracovat nové úlohy, když je SQL Database k dispozici.

### <a name="region-failures"></a>Selhání oblasti

Může dojít k selhání celé oblasti. Přírodní katastrofa může zničit datové centrum, může se tak rozřezat meteorem, liniovou linii v datacentru může vyjmout zemědělec Burying za krávu backhoe atd. Pokud je vaše aplikace hostovaná v datacentru stricken? Je možné nastavit aplikaci v Azure tak, aby běžela v několika oblastech současně, takže pokud dojde k havárii v jednom, budete pokračovat v práci v jiné oblasti. Taková selhání představují extrémně vzácná opakování a většina aplikací neskočí přes jednodušší, který je nutný k zajištění nepřerušované služby prostřednictvím selhání tohoto řazení. Informace o tom, jak zajistit dostupnost aplikace i přes selhání oblasti, najdete v části Resources na konci kapitoly.

Cílem Azure je zajistit, aby zpracování všech těchto druhů chyb bylo mnohem snazší, a v následujících kapitolách vidíte některé příklady, jak to máme.

## <a name="slas"></a>Smlouvy SLA

Lidé často uslyší smlouvy o úrovni služeb (SLA) v cloudovém prostředí. V podstatě se příslibů, že společnosti pracují na tom, jak je jejich služba spolehlivá. 99,9% smlouva SLA znamená, že byste měli očekávat, že služba bude správně fungovat 99,9% času. To je poměrně obvyklá hodnota pro smlouvu SLA, která má jako velmi vysoké číslo, ale nemůžete zjistit, kolik času se ve skutečnosti nejvíce nezobrazuje. Tady je tabulka, která ukazuje, jak velké množství výpadků v procentech v rámci smlouvy SLA v roce, v měsíci a v týdnu.

![Tabulka SLA](design-to-survive-failures/_static/image2.png)

Smlouva SLA 99,9% znamená, že vaše služba by mohla být mimo provoz 8,76 hodin v roce 43,2 nebo v minutách za měsíc. To je mnohem více, než většina uživatelů uvědomuje. Takže jako vývojář si přejete vědět, že je možné určit určitou dobu v čase, a zajistit tak bezproblémové zpracování. V určitém okamžiku bude aplikace používat vaši aplikaci a služba bude mimo provoz a vy chcete minimalizovat negativní dopad na zákazníka.

Jedna z věcí, které byste měli znát o smlouvě SLA, je to, na který časový rámec odkazuje: znamená to, že se čas obnoví každý týden, každý měsíc nebo každý rok? V Azure se hodiny resetují každý měsíc, což je pro vás lepší než roční smlouva SLA, protože roční smlouva SLA by mohla skrýt špatné měsíce tím, že je odkompenzuje s řadou dobrých měsíců.

Samozřejmě vždycky snažímei lepší, než je smlouva SLA; obvykle je to mnohem méně. Slibem je to, že pokud budeme v provozu déle, než je maximální doba mimo provoz, můžete požádat o peníze zpátky. Množství peněz, které vrátíte, by pravděpodobně zcela neplatilo, ale tento aspekt smlouvy SLA funguje jako zásada vynucení a umožňuje vám, abyste měli jistotu, že to máme hodně vážně.

### <a name="composite-slas"></a>Složené smlouvy SLA

Důležitou věcí, kterou je třeba vzít v úvahu, když se díváte na SLA, je dopad použití několika služeb v aplikaci, přičemž každá služba má samostatnou smlouvu SLA. Například aplikace pro opravu IT používá Azure App Service Web Apps, Azure Storage a SQL Database. Tady jsou čísla smluv SLA pro datum, kdy je tato elektronická příručka zapisována v prosinci, 2013:

![Web SLA, úložiště, SQL Database](design-to-survive-failures/_static/image3.png)

Jaká je maximální doba mimo provoz, kterou byste měli očekávat pro aplikaci na základě těchto služeb SLA? Můžete si všimnout, že čas v čase v tomto případě bude stejný jako nejhorší procento smlouvy SLA, nebo v tomto případě 99,9%. To by mělo být pravdivé, pokud se všechny tři služby vždy nezdařily ve stejnou dobu, ale nemusí nutně to, co se skutečně stane. Každá služba může selhat nezávisle v různých časech, takže je nutné vypočítat složenou smlouvu SLA vynásobením jednotlivých čísel SLA.

![Složené smlouvy SLA](design-to-survive-failures/_static/image4.png)

Takže vaše aplikace by nemohla být nejenom 43,2 minut v měsíci, ale 3 časy, 108 minut v měsíci a pořád i v rámci omezení smlouvy SLA pro Azure.

Tento problém není jedinečný pro Azure. Ve skutečnosti poskytujeme nejlepší cloudové SLA jakékoli dostupné cloudové služby a budete mít podobné problémy, se kterými se můžete zabývat, pokud použijete cloudové služby od libovolného dodavatele. Z toho důvodu je důležité se zamyslet nad tím, jak můžete aplikaci navrhnout, aby nedocházelo k bezproblémovému selhání služby, protože by mohla být často dostatečná, aby ovlivnila vaše zákazníky nebo uživatele.

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>Cloudový SLA ve srovnání s prostředím Enterprise v čase

Lidé někdy říkají, že v mé podnikové aplikaci tyto problémy nemají. Pokud si vyžádáte, jak dlouhou dobu využije měsíc ve skutečnosti, obvykle se jedná o "dobře se děje". A pokud si vyžádáte, jak často se to bude připustit k tomu, že je někdy potřeba zálohovat nebo nainstalovat nový server nebo aktualizovat software. Samozřejmě se počítá jako doba mimo provoz. Většina podnikových aplikací, pokud nejsou obzvláště důležité, jsou ve skutečnosti po dobu delší, než je doba povolená SLA naší služby. Ale když je váš server a vaše infrastruktura a zodpovídáte za něj a jejich kontrolu, myslíte o tom, že Angst méně času. V cloudovém prostředí závisíte na někoho jiného a nevíte, co se chystá, takže se o něm budete moct lépe zajímat.

Když podnik dosáhne většího množství v čase, než se dostanete od smlouvy SLA pro Cloud, vytráví spoustu dalších peněz na hardwaru. Cloudová služba by mohla to udělat, ale musela by pro své služby účtovat mnohem více. Místo toho můžete využít cenově výhodné službu a navrhnout software tak, aby nevyhnutelné chyby způsobily minimální přerušení pro vaše zákazníky. Vaše úloha jako Cloud App Designer není natolik velká, aby nedocházelo k selhání, protože se tak vyhnete pohromě a uděláte to tak, že se zaměříte na software, ne na hardware. Vzhledem k tomu, že podnikové aplikace se snaží maximalizovat střední dobu mezi selháními, cloudové aplikace se snaží minimalizovat střední dobu obnovení.

### <a name="not-all-cloud-services-have-slas"></a>Ne všechny cloudové služby mají SLA

Nezapomeňte také, že ne každá cloudová služba má ještě smlouvu SLA. Pokud je vaše aplikace závislá na službě, která nemá žádnou záruku, možná se vám může stát mnohem déle, než můžete představit. Pokud například povolíte přihlášení k webu pomocí poskytovatele sociálních sítí, jako je Facebook nebo Twitter, poraďte se s poskytovatelem služeb a zjistěte, jestli se jedná o smlouvu SLA, a nemůžete tu najít. Pokud ale ověřovací služba přestane být v provozu nebo není schopna podporovat objem požadavků, které jste v něm vyvolali, budou vaši zákazníci z vaší aplikace uzamčeni. Můžete být vypnuté po dobu více dní. Tvůrci jedné nové aplikace očekávali stovky milionů souborů ke stažení a využili se na Facebooku ověřování – ale nemuseli se mluvit na Facebook, než se zabývali a zjistili, že pro tuto službu neexistovala žádná smlouva SLA.

### <a name="not-all-downtime-counts-toward-slas"></a>Ne všechna výpadky se započítává k SLA

Některé cloudové služby můžou službu odepřít, pokud je vaše aplikace používá. To se označuje jako *omezování*. Pokud má služba smlouvu SLA, měla by stanovit podmínky, za kterých se může omezit, a váš návrh aplikace by se měl vyhnout těmto podmínkám a reagovat odpovídajícím způsobem na omezení, pokud k nim dojde. Například pokud se požadavky na službu nedaří spustit, když překročíte určitý počet za sekundu, chcete zajistit, aby automatické opakování neprobíhalo tak rychle, aby toto omezení mohlo pokračovat. Další informace o omezování najdete v [kapitole zpracování přechodných chyb](transient-fault-handling.md).

## <a name="summary"></a>Souhrn

Tato kapitola se pokusila získat informace o tom, proč je reálné cloudové aplikace navržená tak, aby se neúspěšně zadržely chyby. Od [Další kapitoly](monitoring-and-telemetry.md)se zbývající vzory v této sérii přejdou podrobněji o některých strategiích, které můžete použít k těmto akcím:

- Dobře se [monitoruje a telemetrie](monitoring-and-telemetry.md), takže můžete rychle zjistit chyby, které vyžadují zásah, a máte dostatečné informace, jak je vyřešit.
- [Zpracování přechodných chyb](transient-fault-handling.md) implementací inteligentní logiky opakování, aby se vaše aplikace automaticky obnovila v případě, že se může a vrátí k logice pro [přerušení okruhu](transient-fault-handling.md#circuitbreakers) , když to nemůže.
- Použijte [distribuované ukládání do mezipaměti](distributed-caching.md) , abyste minimalizovali problémy s propustností, latencí a připojením s přístupem k databázi.
- Implementujte volné spojení pomocí [vzoru práce orientovaného na fronty](queue-centric-work-pattern.md), aby mohl front-end aplikace i nadále fungovat, když je back-end mimo provoz.

## <a name="resources"></a>Prostředky

Další informace najdete v těchto e-knihách v pozdějších kapitolách a na následujících zdrojích.

Nápovědě

- [Failsafe: pokyny pro odolné cloudové architektury](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Dokument white paper o matolin Mercuri, Ulrich Homann a Andrew Townhill. Verze webové stránky pro video řady FailSafe
- [Osvědčené postupy pro návrh rozsáhlých služeb v Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Dokument White Paper, který označuje Simms a Michael Thomassy.
- [Technické pokyny pro provozní kontinuitu Azure](https://msdn.microsoft.com/library/windowsazure/hh873027.aspx). Dokument White Paper od nadWicklineho a Jason Skořepa.
- [Zotavení po havárii a vysoká dostupnost pro aplikace Azure](https://msdn.microsoft.com/library/windowsazure/dn251004.aspx) Dokument White Paper od Michaela McKeown, Hanu Kommalapati a Jason Skořepa.
- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Viz pokyny pro nasazení ve více datových centrech, vzorek přerušení okruhu.
- [Podpora Azure – smlouvy o úrovni služeb](https://azure.microsoft.com/support/legal/sla/).
- [Provozní kontinuita v Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/hh852669.aspx). Dokumentace k SQL Database funkcím vysoké dostupnosti a zotavení po havárii.
- [Vysoká dostupnost a zotavení po havárii pro SQL Server v Azure Virtual Machines](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx).

Videa:

- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět částí podle Ulrich Homann, matolin Mercuri a označit Simms. Prezentuje základní koncepty a principy architektury v rámci velmi přístupného a zajímavého způsobu, který vychází ze zkušeností zákazníků Microsoftu pro poradenské zákazníky (CAT) se skutečnými zákazníky. Díly 1 a 8 se podrobněji dostanou do předdefinovaných důvodů selhání při navrhování cloudových aplikací. Viz také následná diskuze o omezování v epizody 2 od 49:57, diskuzi o bodech selhání a režimech selhání ve epizody 2 počínaje 56:05 a diskuzi o přepínacích modulech okruhu ve epizodě 3 od 40:55.
- [Sestavování velkých: lekcí získaných od zákazníků Azure – část II](https://channel9.msdn.com/Events/Build/2012/3-030). Označte Simms rozhovory o návrhu pro selhání a instrumentaci všeho. Podobně jako u řady Failsafe, ale odkazuje na další podrobnosti.

> [!div class="step-by-step"]
> [Předchozí](unstructured-blob-storage.md)
> [Další](monitoring-and-telemetry.md)
