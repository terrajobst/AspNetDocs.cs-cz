---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: Distribuované ukládání do mezipaměti (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: c66187b990a828c53bd2f8115e3c9660fc6022ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582814"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>Distribuované ukládání do mezipaměti (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Předchozí kapitola vyhledala přechodný způsob zpracování chyb a uvedla do mezipaměti jako strategii pro přerušení okruhu. V této části najdete další informace o ukládání do mezipaměti, včetně toho, kdy je použít, běžné vzory jejich používání a jak je implementovat v Azure.

## <a name="what-is-distributed-caching"></a>Co je distribuované ukládání do mezipaměti

Mezipaměť poskytuje přístup s vysokou propustností a nízkou latencí pro běžně používaná data aplikací tím, že ukládá data do paměti. Pro cloudovou aplikaci je to nejužitečnější typ mezipaměti distribuované mezipaměti, což znamená, že data se neukládají na jednotlivé paměti webového serveru, ale v jiných cloudových prostředcích a data uložená v mezipaměti jsou dostupná pro všechny webové servery aplikace (nebo jiné cloudové virtuální počítače, které ar e používané aplikací

![Diagram znázorňující více webových serverů, které přistupují k serverům mezipaměti](distributed-caching/_static/image1.png)

Když se aplikace škáluje přidáním nebo odebráním serverů nebo když jsou servery nahrazené z důvodu upgradů nebo chyb, data uložená v mezipaměti zůstávají dostupná pro každý server, na kterém je aplikace spuštěná.

Díky zamezení vysoké latence přístupu k datům trvalého úložiště dat může ukládání do mezipaměti výrazně zlepšit odezvu aplikace. Například načítání dat z mezipaměti je mnohem rychlejší než načítání z relační databáze.

Vedlejší výhodou ukládání do mezipaměti je snížení provozu do trvalého úložiště dat, což může vést k nižším nákladům v případě, že se pro trvalé úložiště dat účtují poplatky za výstup dat.

## <a name="when-to-use-distributed-caching"></a>Kdy použít distribuované ukládání do mezipaměti

Ukládání do mezipaměti funguje nejlépe pro úlohy aplikací, které usnadňují čtení než zápis dat, a když datový model podporuje organizaci klíč/hodnota, kterou použijete k ukládání a načítání dat v mezipaměti. Je také užitečné, když uživatelé aplikace sdílejí spoustu společných dat; mezipaměť například neposkytuje tolik výhod, pokud každý uživatel obvykle získá data jedinečná pro daného uživatele. V případě, že ukládání do mezipaměti může být velmi výhodné, patří katalog produktů, protože se data nemění často a všichni zákazníci se hledají stejná data.

Výhoda ukládání do mezipaměti je stále větší, ale čím víc je aplikace škálovaná, protože omezení propustnosti a zpoždění latence trvalého úložiště dat se stanou větším limitem celkového výkonu aplikace. Mezipaměť ale můžete implementovat i z jiných důvodů než výkon. V případě dat, která nemusí být dokonale aktuální, je-li zobrazena uživateli, může přístup k mezipaměti sloužit jako přerušení okruhu, pokud trvalé úložiště dat nereaguje nebo není k dispozici.

## <a name="popular-cache-population-strategies"></a>Oblíbené strategie plnění mezipaměti

Aby bylo možné načíst data z mezipaměti, je nutné je nejprve uložit. K dispozici je několik strategií pro získání dat, která potřebujete do mezipaměti:

- Na vyžádání nebo v mezipaměti

    Aplikace se pokusí načíst data z mezipaměti a když mezipaměť neobsahuje data ("neúspěšné"), aplikace ukládá data do mezipaměti, takže bude příště k dispozici. Až se aplikace příště pokusí získat stejná data, najde, co je v mezipaměti hledání ("dosaženo"). Chcete-li zabránit načtení dat uložených v mezipaměti, která se změnila v databázi, při provádění změn v úložišti dat dojde k neplatnosti.
- Nabízení dat na pozadí

    Služby na pozadí zadávají data do mezipaměti podle pravidelného plánu a aplikace se vždycky stáhnou z mezipaměti. Tento přístup funguje skvěle se zdroji dat s vysokou latencí, které nevyžadují vždycky vracet nejnovější data.
- Přerušení okruhů

    Aplikace obvykle komunikuje přímo s trvalým úložištěm dat, ale pokud má trvalé úložiště dat problémy s dostupností, aplikace načte data z mezipaměti. Data mohla být vložena do mezipaměti s využitím strategie pro nabízení dat z mezipaměti nebo na pozadí. Jedná se o strategii zpracování chyb, nikoli strategii zvýšení výkonu.

Aby bylo možné zachovat data v mezipaměti, můžete položky související s mezipamětí odstranit, pokud aplikace vytváří, aktualizuje nebo odstraňuje data. Pokud je dobře pro vaši aplikaci někdy data, která jsou mírně zastaralá, můžete se spolehnout na konfigurovatelnou dobu vypršení platnosti a nastavit limit toho, jak se můžou data starých dat ukládat.

Můžete nakonfigurovat absolutní vypršení platnosti (čas od vytvoření položky mezipaměti) nebo klouzavé vypršení platnosti (čas od posledního otevření položky mezipaměti). Absolutní doba vypršení platnosti se používá v závislosti na mechanismu vypršení platnosti mezipaměti, aby se zabránilo příliš zastaralosti dat. V aplikaci Fix it ručně vyřadíme zastaralé položky mezipaměti a k uchování nejaktuálnějších dat v mezipaměti použijeme klouzavé vypršení platnosti. Bez ohledu na to, jakou zásadu vypršení platnosti zvolíte, mezipaměť po dosažení limitu paměti automaticky vyřadí nejstarší (nejméně naposledy použité nebo LRU) položky.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>Ukázkový kód v mezipaměti pro opravu IT aplikace

V následujícím ukázkovém kódu zkontrolujeme při načítání úlohy opravit IT první mezipaměť. Pokud se úkol najde v mezipaměti, vrátíme ho. Pokud se nenalezne, získáme ho z databáze a uložíme do mezipaměti. Změny, které jste provedli pro přidání ukládání do mezipaměti do metody `FindTaskByIdAsync`, jsou zvýrazněné.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Když aktualizujete nebo odstraníte úlohu opravit IT, musíte zrušit platnost (odebrat) úlohu uloženou v mezipaměti. V opačném případě se budoucí pokusy o čtení této úlohy budou i nadále získávat ze starých dat z mezipaměti.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

Jedná se o ukázky pro ilustraci jednoduchého kódu pro ukládání do mezipaměti. do mezipaměti se neimplementovala mezipaměť, kterou je v projektu ke stažení opravit.

## <a name="azure-caching-services"></a>Služby ukládání do mezipaměti Azure

Azure nabízí následující služby ukládání do mezipaměti: [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx) a [Azure Managed Cache](https://msdn.microsoft.com/library/dn386094.aspx). Azure Redis Cache je založená na oblíbených [Open source Redis Cache](http://redis.io/) a je první volbou pro většinu scénářů ukládání do mezipaměti.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>Stav relace ASP.NET pomocí poskytovatele mezipaměti

Jak je uvedeno v [kapitole Doporučené postupy pro vývoj webu](web-development-best-practices.md), doporučujeme vyhnout se použití stavu relace. Pokud vaše aplikace vyžaduje stav relace, je dalším osvědčeným postupem vyhnout se výchozímu zprostředkovateli v paměti, protože nepovoluje horizontální navýšení kapacity (více instancí webového serveru). Zprostředkovatel stavu relace ASP.NET SQL Server umožňuje, aby lokalita, která běží na více webových serverech, používala stav relace, ale dojde k tomu při vysoké latenci v porovnání se zprostředkovatelem v paměti. Nejlepším řešením, pokud potřebujete použít stav relace, je použití poskytovatele mezipaměti, jako je [zprostředkovatel stavu relace pro Azure cache](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx).

## <a name="summary"></a>Přehled

Viděli jste, jak může aplikace opravit IT implementovat ukládání do mezipaměti, aby se zlepšila doba odezvy a škálovatelnost, a aby mohla aplikace nadále reagovat na operace čtení, pokud databáze není k dispozici. V [Další části](queue-centric-work-pattern.md) se dozvíte, jak dál vylepšit škálovatelnost a zajistit, aby aplikace pokračovala v reakci na operace zápisu.

## <a name="resources"></a>Prostředky

Další informace o ukládání do mezipaměti najdete v následujících zdrojích informací.

Dokumentace

- [Mezipaměť Azure](https://msdn.microsoft.com/library/gg278356.aspx). Oficiální dokumentace MSDN o ukládání do mezipaměti v Azure.
- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Viz pokyny k ukládání do mezipaměti a model doplňování mezipaměti.
- [Failsafe: pokyny pro odolné cloudové architektury](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Dokument white paper o matolin Mercuri, Ulrich Homann a Andrew Townhill. Informace najdete v části ukládání do mezipaměti.
- [Osvědčené postupy pro návrh rozsáhlých služeb v Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). W. Dokument White Paper, který označuje Simms a Michael Thomassy. Viz část distribuované ukládání do mezipaměti.
- [Distribuované ukládání do mezipaměti pro cestu k škálovatelnosti](https://msdn.microsoft.com/magazine/dd942840.aspx). Starší (2009) článek o časopise MSDN Magazine, ale jasně psaný Úvod do ukládání distribuovaných mezipamětí. přejde do větší hloubky než do mezipamětí v FailSafe a v dokumentu White Paper s osvědčenými postupy.

Videa

- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět částí podle Ulrich Homann, matolin Mercuri a označit Simms. 400 nabízí přehled o tom, jak architekt cloudových aplikací. Tato série se zaměřuje na teorie a důvody, proč; Další podrobné informace o tom, jak označit Simms, najdete v tématu vytváření velkých řad. Podívejte se na diskuzi o ukládání do mezipaměti ve epizody 3 od 1:24:14.
- [Sestavování velkých: lekcí získaných od zákazníků Azure – část I](https://channel9.msdn.com/Events/Build/2012/3-029). Simon Davies popisuje distribuované ukládání do mezipaměti počínaje 46:00. Podobně jako u řady Failsafe, ale odkazuje na další podrobnosti. Prezentace byla zadána 31. října 2012, takže nepokrývá službu ukládání do mezipaměti Web Apps v Azure App Service, která byla představena v 2013.

Ukázka kódu

- [Základy cloudových služeb v Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Ukázková aplikace, která implementuje distribuované ukládání do mezipaměti. Seznamte se se základními informacemi v doprovodném blogu o [cloudových službách – základy ukládání do mezipaměti](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx).

> [!div class="step-by-step"]
> [Předchozí](transient-fault-handling.md)
> [Další](queue-centric-work-pattern.md)
