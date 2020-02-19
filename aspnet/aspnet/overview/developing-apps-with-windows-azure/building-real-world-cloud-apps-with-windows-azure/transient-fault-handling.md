---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: Zpracování přechodných chyb (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 11/03/2015
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: e798cb83cfb97db63fef6dc38c8f62804461d01b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456852"
---
# <a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>Zpracování přechodných chyb (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Když navrhujete reálný cloudovou aplikaci, jedna z věcí, které je třeba zvážit, je způsob, jak zpracovat dočasná přerušení služeb. Tento problém je v cloudových aplikacích jednoznačně důležitý, protože jsou závislé na síťových připojeních a externích službách. Často se dá trochu histogramu, které se obvykle samy opraví, a pokud je nebudete moct inteligentně zvládnout, bude mít za následek špatné prostředí pro vaše zákazníky.

## <a name="causes-of-transient-failures"></a>Příčiny přechodných selhání

V cloudovém prostředí zjistíte, že se neúspěšná a Vyřazená databázová připojení probíhají pravidelně. To je částečně vzhledem k tomu, že procházíte dalšími nástroji pro vyrovnávání zatížení ve srovnání s místním prostředím, kde má váš webový server a databázový server přímé fyzické připojení. I když se někdy spoléháte na víceklientské služby, uvidíte, že volání služby bude pomalejší nebo delší, protože někdo jiný, kdo tuto službu používá, je velmi zatížen. V ostatních případech se může jednat o uživatele, který službu nevyužívá příliš často, a služba úmyslně omezuje připojení –, aby nedošlo k nepříznivému ovlivňování dalších klientů služby.

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>Omezení účinku přechodných selhání pomocí inteligentní logiky opakování/zálohování

Namísto vyvolání výjimky a zobrazení stránky, která není k dispozici nebo není k dispozici pro zákazníka, můžete rozpoznat chyby, které jsou obvykle přechodné, a automaticky opakovat operaci, která vedla k chybě, v hodlá, která před dlouhou dobu bude úspěšná. Ve většině případů bude operace při druhém pokusu úspěšná a z chyby se obnoví, aniž by zákazník musel vědět, že nastal problém.

Existuje několik způsobů, jak můžete implementovat logiku inteligentního opakování.

- Skupina Microsoft Patterns &amp; Practices má [blok s přechodným zpracováním chyb](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx) , který vše udělá, pokud používáte ADO.NET pro SQL Database přístup (ne prostřednictvím Entity Framework). Nastavili jste jenom zásady pro opakování – kolikrát se má dotaz nebo příkaz opakovat, a jak dlouho se má čekat mezi pokusy – a zabalit svůj kód SQL do bloku *using* .

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    TFH také podporuje [Azure mezipaměť hostovaná v instanci role](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx) a [Service Bus](https://azure.microsoft.com/services/service-bus/).
- Při použití Entity Framework nepracujete přímo s připojením SQL, takže nemůžete použít tento balíček Patterns and Practices, ale Entity Framework 6 sestaví tento druh logiky opakování přímo do rozhraní. Podobným způsobem jste určili strategii opakování a pak EF používá tuto strategii vždy, když přistupuje k databázi.

    Aby bylo možné tuto funkci použít v aplikaci opravit IT, je nutné přidat třídu, která je odvozena z *DbConfiguration* a zapnout logiku opakování.

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    Pro SQL Database výjimky, které rozhraní identifikuje jako obvykle přechodné chyby, zobrazí kód EF pokyn pro opakování operace až třikrát, s exponenciálním zpožděním mezi opakovanými pokusy a maximálním zpožděním 5 sekund. Exponenciální regrese znamená, že po každém neúspěšném pokusu bude před dalším pokusem čekat na delší dobu. Pokud se tři pokusy v řádku nezdaří, vyvolá výjimku. Následující část o přepínacích cyklech okruhu vysvětluje, proč potřebujete exponenciální zpětně a omezený počet opakovaných pokusů.

    Při používání služby Azure Storage můžete mít podobné problémy, protože aplikace pro opravu IT pro objekty blob funguje, protože rozhraní API pro klientské úložiště .NET již implementuje stejný druh logiky. Stačí jenom zadat zásady opakování, nebo to nemusíte dělat, pokud budete mít výchozí nastavení.

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>Vypínače okruhu

Existuje několik důvodů, proč nechcete opakovat příliš mnoho času za příliš dlouhou dobu:

- Příliš mnoho uživatelů, kteří trvale opakují neúspěšné požadavky, můžou snížit možnosti práce s ostatními uživateli. Pokud se v milionech lidí provádí všechny opakované opakované žádosti, mohli byste se zakládat na frontě odeslání služby IIS a zabránit tomu, aby vaše aplikace mohla zpracovávat požadavky, které jinak může úspěšně zpracovat.
- Pokud se každý opakuje z důvodu selhání služby, může to být tolik požadavků, které jsou zařazené do fronty, až se služba začne obnovovat.
- Pokud je chyba způsobená omezením a existuje okno času, které služba používá k omezování, může se pokusy o pokračování přesunout z tohoto okna a způsobit pokračování omezování.
- Může se stát, že uživatel čeká na vykreslení webové stránky. Tím, že uživatelé čekají na příliš dlouhou dobu, může být více obtěžující, což by se poměrně rychle poradí s tím, že se později pokusí

Exponenciální back-vypnuté adresy řeší některé z těchto potíží omezením četnosti opakovaných pokusů, které může služba získat z vaší aplikace. Je ale také nutné mít *přerušení okruhů*: to znamená, že u určité prahové hodnoty opakování vaše aplikace ukončí opakování a provede nějakou jinou akci, například jednu z následujících akcí:

- Vlastní záložní verze. Pokud nemůžete získat cenu akcií od společnosti Reuters, možná ji můžete získat z Bloomberg. nebo pokud nemůžete získat data z databáze, možná je můžete získat z mezipaměti.
- Tiché selhání. Pokud pro vaši aplikaci nepotřebujete vše, co potřebujete, stačí vrátit hodnotu null, pokud data nemůžete získat. Pokud zobrazujete úlohu opravy IT a Blob service neodpovídá, mohli byste zobrazit podrobnosti o úloze bez obrázku.
- Rychlá chyba. Pro uživatele se stala chyba, aby se zabránilo zahlcení služby pomocí opakovaných požadavků, které by mohly způsobit přerušení služby pro ostatní uživatele nebo rozšiřování okna omezování. Můžete zobrazit popis "zkusit znovu později".

Neexistují žádné zásady opakování pro všechny velikosti. Můžete to zkusit víckrát a déle počkat v asynchronním pracovním procesu na pozadí, než byste museli v synchronní webové aplikaci, kde uživatel čeká na odpověď. Mezi opakovanými pokusy pro službu relačních databází můžete čekat, než byste museli službu cache Service. Tady jsou některé ukázkové Doporučené zásady opakování, které vám poskytnou představu o tom, jak se čísla můžou lišit. ("Rychlé první" znamená před prvním opakováním žádné zpoždění.

![Ukázkové zásady opakování](transient-fault-handling/_static/image1.png)

Pokyny k zásadám pro opakování SQL Database najdete v tématu [řešení přechodných chyb a chyb připojení SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/).

## <a name="summary"></a>Souhrn

Strategie opakovaného nebo Back-off může přispět k dočasným chybám, které jsou pro zákazníka většinou neviditelné, a poskytuje rozhraní, které můžete použít k minimalizaci práce s implementací strategie bez ohledu na to, jestli používáte ADO.NET, Entity Framework nebo službu Azure Storage.

V [Další části](distributed-caching.md)se podíváme na to, jak zvýšit výkon a spolehlivost pomocí distribuované mezipaměti.

## <a name="resources"></a>Prostředky

Další informace naleznete v následujících zdrojích:

Dokumentace

- [Osvědčené postupy pro návrh rozsáhlých služeb v Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Dokument White Paper, který označuje Simms a Michael Thomassy. Podobně jako u řady Failsafe, ale odkazuje na další podrobnosti. Viz část telemetrie a diagnostika.
- [Failsafe: pokyny pro odolné cloudové architektury](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Dokument white paper o matolin Mercuri, Ulrich Homann a Andrew Townhill. Verze webové stránky pro video řady FailSafe
- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Viz vzor opakování, model správce agenta plánovače.
- Odolnost [proti chybám v Azure SQL Database](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx). Příspěvek na blogu od Adam petrossian.
- [Entity Framework – logika připojení/opakování](https://msdn.microsoft.com/data/dn456835). Jak používat a přizpůsobovat funkci zpracování přechodných chyb Entity Framework 6.
- [Odolnost připojení a zachycení příkazů pomocí Entity Framework v aplikaci ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Čtvrtá série kurzů s devíti částmi ukazuje, jak nastavit funkci odolnosti připojení EF 6 pro SQL Database.

Videa

- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět částí podle Ulrich Homann, matolin Mercuri a označit Simms. Prezentuje základní koncepty a principy architektury v rámci velmi přístupného a zajímavého způsobu, který vychází ze zkušeností zákazníků Microsoftu pro poradenské zákazníky (CAT) se skutečnými zákazníky. Podívejte se na diskuzi o přepínacích modulcích okruhů ve epizody 3 od 40:55.
- [Sestavování velkých: lekcí získaných od zákazníků Azure – část II](https://channel9.msdn.com/Events/Build/2012/3-030). Označte Simms rozhovory o návrhu pro selhání, zpracování přechodných chyb a proinstrumentování všeho.

Ukázka kódu

- [Základy cloudových služeb v Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Ukázková aplikace vytvořená poradenským týmem pro zákazníky Microsoft Azure, která ukazuje, jak použít [blok přechodného zpracování chyb v podnikové knihovně](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/) (TFH). Další informace najdete v článku [Vrstva přístupu k datům u aplikace Cloud Service Fundamentals – zpracování přechodných chyb](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx). TFH se doporučuje pro přístup k databázím přímo pomocí ADO.NET (bez použití Entity Framework).

> [!div class="step-by-step"]
> [Předchozí](monitoring-and-telemetry.md)
> [Další](distributed-caching.md)
