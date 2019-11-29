---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: Monitorování a telemetrie (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: 44941c9fd0dcd3223604fc4a4f2836f587578acb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585616"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>Monitorování a telemetrie (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Spousta lidí spoléhá na zákazníky, aby věděli, že jejich aplikace je mimo provoz. To není ve skutečnosti osvědčené postupy kdekoli a zejména v cloudu. Neexistuje žádná záruka na rychlé oznamování a při obdržení oznámení obdržíte často minimální nebo zavádějící data o tom, co se stalo. Díky dobrým systémům telemetrie a protokolování můžete vědět, co se s vaší aplikací právě dělá, a pokud se něco nepovede, zjistíte hned a získáte užitečné informace pro řešení potíží, se kterými můžete pracovat.

## <a name="buy-or-rent-a-telemetry-solution"></a>Koupit nebo pronajímat řešení telemetrie

> [!NOTE]
> Tento článek byl napsán před vydáním [Application Insights](/azure/application-insights/app-insights-overview) . Application Insights je preferovaný přístup k řešením telemetrie v Azure. Další informace najdete v tématu [nastavení Application Insights pro web ASP.NET](/azure/application-insights/app-insights-asp-net) .

Jedním z věcí, které jsou skvělé z hlediska cloudového prostředí, je, že je to opravdu snadné koupit nebo pronajímat své Victory. Telemetrii je příkladem. Aniž byste hodně napravili, můžete si předběžně využít a efektivně spustit systém telemetrie. Existuje spousta skvělých partnerů, kteří se integrují s Azure, a některé z nich mají bezplatné úrovně, takže můžete získat základní telemetrii pro nic. Tady je jen několik těch, které jsou aktuálně dostupné v Azure:

- [Nový Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [DynaTrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

Součástí nástroje [Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) jsou také funkce monitorování.

Rychle vám ukážeme, jak nastavit nové Relic, aby bylo možné Ukázat, jak snadné je použít systém telemetrie.

Na portálu pro správu Azure se zaregistrujte ke službě. Klikněte na **Nový**a pak na **Uložit**. Zobrazí se dialogové okno **zvolit doplněk** . Posuňte se dolů a klikněte na **Nový Relic**.

![Zvolit doplněk](monitoring-and-telemetry/_static/image1.png)

Klikněte na šipku doprava a vyberte požadovanou úroveň služby. V této ukázce použijeme úroveň Free.

![Přizpůsobení doplňku](monitoring-and-telemetry/_static/image2.png)

Klikněte na šipku vpravo a potvrďte, že "nákup" a nové Relic se teď zobrazují jako doplněk na portálu.

![Kontrola nákupu](monitoring-and-telemetry/_static/image3.png)

![Nový doplněk Relic na portálu pro správu](monitoring-and-telemetry/_static/image4.png)

Klikněte na **informace o připojení**a zkopírujte licenční klíč.

![Informace o připojení](monitoring-and-telemetry/_static/image5.png)

Přejděte na kartu **Konfigurovat** pro vaši webovou aplikaci na portálu, nastavte **sledování výkonu** na **doplněk**a nastavte rozevírací seznam **zvolit doplněk** na **New Relic**. Pak klikněte na **Uložit**.

![Nový Relic na kartě Konfigurace](monitoring-and-telemetry/_static/image6.png)

V aplikaci Visual Studio nainstalujte nový balíček NuGet Relic ve vaší aplikaci.

![Developer Analytics na kartě konfigurovat](monitoring-and-telemetry/_static/image7.png)

Nasaďte aplikaci do Azure a začněte ji používat. Vytvořte několik úkolů v oddělení IT, které vám poskytnou nějakou aktivitu pro monitorování nových Relic.

Pak se vraťte na **novou stránku Relic** na kartě **Doplňky** na portálu a klikněte na **Spravovat**. Portál vás pošle na nový portál pro správu Relic s použitím jednotného přihlašování pro ověřování, takže nemusíte zadávat svoje přihlašovací údaje znovu. Na stránce Přehled se zobrazuje řada statistik výkonu. (Kliknutím na obrázek zobrazíte celou velikost stránky s přehledem.)

[karta monitorování nové Relic ![](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

Tady je jen pár statistik, které vidíte:

- Průměrná doba odezvy v různou denní dobu.

    ![Doba odezvy](monitoring-and-telemetry/_static/image10.png)
- Míry propustnosti (v rámci požadavků za minutu) v různou denní dobu.

    ![Propustnost](monitoring-and-telemetry/_static/image11.png)
- Čas procesoru serveru strávený zpracováním různých požadavků HTTP.

    ![Časy webové transakce](monitoring-and-telemetry/_static/image12.png)
- Čas procesoru strávený v různých částech kódu aplikace:

    ![Podrobnosti trasování](monitoring-and-telemetry/_static/image13.png)
- Historické statistiky výkonu.

    ![Historický výkon](monitoring-and-telemetry/_static/image14.png)
- Volání externích služeb, jako jsou Blob service a statistiky o tom, jak spolehlivě a reagují na službu.

    ![Externí služby](monitoring-and-telemetry/_static/image15.png)

    ![Externí služby](monitoring-and-telemetry/_static/image16.png)

    ![Externí služba](monitoring-and-telemetry/_static/image17.png)
- Informace o tom, kde se nachází na světě nebo kam pochází přenos z americké webové aplikace.

    ![Geografické](monitoring-and-telemetry/_static/image18.png)

Můžete také nastavit sestavy a události. Můžete například vyslovit čas, kdy začnete zobrazovat chyby, poslat e-mail s upozorněním na pracovníky podpory.

![Sestavy](monitoring-and-telemetry/_static/image19.png)

New Relic je pouze jedním z příkladů systému telemetrie; to všechno můžete získat i z jiných služeb. Krásy cloudu je, že nemusíte psát žádný kód, a to kvůli minimálnímu nebo žádnému počtu výdajů, náhle získáte další informace o tom, jak se vaše aplikace používá, a o tom, co vaši zákazníci skutečně čelí.

<a id="log"></a>
## <a name="log-for-insight"></a>Protokol pro přehled

Balíček telemetrie je dobrý první krok, ale stále musíte instrumentovat vlastní kód. Služba telemetrie vás upozorní, když dojde k problému, a dozvíte se, co se zákazník setkává, ale nemusí vám poskytnout spoustu informací o tom, co se ve vašem kódu chystá.

Nechcete, aby bylo možné zjistit, co vaše aplikace dělá, nemusíte se vzdáleně přihlédnout do provozního serveru. To může být praktické, když máte jeden server, ale co se chystáte škálovat na stovky serverů a nevíte, které z nich potřebujete ke vzdálenému přihlášení? Vaše protokolování by mělo poskytovat dostatek informací, které nikdy nebudete muset vzdáleně přihlašovat k provozním serverům a analyzovat a ladit problémy. Měli byste přihlašovat dostatek informací, aby bylo možné izolovat problémy výhradně prostřednictvím protokolů.

### <a name="log-in-production"></a>Přihlášení v produkčním prostředí

Spousta lidí Zapíná trasování v produkčním prostředí pouze v případě, že dojde k problému a chtějí ladit. To může způsobit značnou prodlevu mezi okamžikem, kdy víte o problému, a časem, kdy získáte užitečné informace pro řešení potíží. A informace, které se zobrazí, nemusí být užitečné pro občasné chyby.

To, co doporučujeme v cloudovém prostředí, ve kterém je úložiště levné, je vždycky, když se přihlašujete v produkčním prostředí. Tímto způsobem dojde k chybám, které již jsou protokolovány, a máte historická data, která vám pomohou analyzovat problémy, které se v průběhu času vyvíjejí, nebo pravidelně provádět v různou dobu. Můžete automatizovat proces vyprázdnění a odstranit staré protokoly, ale možná zjistíte, že je dražší k nastavení takového procesu, než aby byly protokoly uchovávány.

Přidané náklady na protokolování jsou triviální v porovnání s množstvím času řešení potíží a peněz, které potřebujete k dispozici, když se něco pokazilo. Až se vám někdo upozorní, že při každé noci došlo k náhodné 8:00 chybě, ale nepamatuje si chybu, můžete si snadno zjistit, co byl problém.

Po dobu méně než $4 měsíců můžete uchovávat 50 gigabajty protokolů na ruce a dopad protokolování je triviální, pokud zachováte jednu věc – abyste se vyhnuli problémům s výkonem, ujistěte se, že je vaše knihovna protokolování asynchronní.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>Odlišení protokolů, které informují o protokolech, které vyžadují akci

Protokoly mají být určené k informování (Chci vědět) nebo jednat (chci něco udělat). Buďte opatrní jenom zapisovat protokoly Act pro problémy, které vyžadují, aby osoba, která má k osobu, nebo automatizovaný proces, provedou akci. Příliš mnoho protokolů ACT vytvoří šum, což vyžaduje příliš velkou práci, aby procházela vše, co by bylo možné najít skutečné problémy. A pokud se protokol ACT automaticky aktivuje s určitou akcí, jako je odeslání e-mailu pracovníkům podpory, vyhněte se tomu, aby se tisíce takových akcí aktivovaly jediným problémem.

V trasování rozhraní .NET System. Diagnostics je možné přiřazovat protokoly chyba, varování, informace a ladění/podrobnosti. Můžete odlišit ACT od protokolu o informování tím, že zachováte úroveň chyby pro protokoly ACT a použijete nižší úrovně pro protokoly informování.

![Úrovně protokolování](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>Konfigurovat úrovně protokolování za běhu

I když je vhodné, aby se protokolování v produkčním prostředí vždy nacházelo, další osvědčeným postupem je implementace protokolovacího rozhraní, které umožňuje v době běhu upravit úroveň podrobností, která se právě přihlašuje, bez nutnosti opětovného nasazení nebo restartování vaší aplikace. Například při použití trasovacího zařízení v `System.Diagnostics` můžete vytvořit chybu, varování, informace a ladit/podrobné protokoly. V produkčním prostředí vždy doporučujeme protokolovat protokoly chyb, varování a informací a budete chtít dynamicky přidávat ladění a podrobné protokolování pro řešení potíží případ od případu.

Web Apps v Azure App Service mají integrovanou podporu pro zápis `System.Diagnostics` protokolů do systému souborů, úložiště tabulek nebo úložiště objektů BLOB. U každého cíle úložiště můžete vybrat různé úrovně protokolování. úroveň protokolování můžete měnit průběžně bez restartování aplikace. Podpora úložiště objektů BLOB usnadňuje spouštění úloh analýzy [HDInsight](https://docs.microsoft.com/azure/hdinsight/) v protokolech aplikací, protože HDInsight ví, jak přímo pracovat s úložištěm BLOB.

### <a name="log-exceptions"></a>Protokolování výjimek

Nestačí pouze vložit *výjimku. ToString ()* ve vašem kódu protokolování. Které odnechávají kontextové informace. V případě chyb SQL opustí číslo chyby SQL. Pro všechny výjimky zahrňte kontextové informace, výjimku a vnitřní výjimky, abyste měli jistotu, že zadáváte všechno, co bude nutné pro řešení potíží. Kontextové informace můžou například zahrnovat název serveru, identifikátor transakce a uživatelské jméno (ale ne heslo nebo tajné klíče).

Pokud spoléháte na každého vývojáře, aby provede správnou věc s protokolováním výjimek, některé z nich nebudou. Aby bylo zajištěno, že se v každém okamžiku provede správný způsob zpracování výjimek, sestavte výjimku přímo do rozhraní protokolovacího nástroje: předejte objekt výjimky do třídy protokolovacího nástroje a správně protokolujte data výjimky ve třídě protokolovacího nástroje.

### <a name="log-calls-to-services"></a>Protokolování volání služeb

Důrazně doporučujeme zapsat protokol pokaždé, když vaše aplikace vyvolá službu, ať už se jedná o databázi nebo REST API nebo jakoukoli externí službu. Zahrňte do protokolu nejen náznaky úspěchu nebo selhání, ale jak dlouho trvaly jednotlivé žádosti. V cloudovém prostředí se často zobrazují problémy související s pomalými a nikoli úplnými výpadky. Něco, co obvykle trvá 10 milisekund, může náhle začít trvat sekundu. Když někdo upozorní na to, že vaše aplikace je pomalá, budete mít možnost se podívat na novou Relicu nebo libovolnou službu telemetrie, kterou máte, a pak si přejete mít možnost podívat se na vaše vlastní protokoly, které se podrobně do podrobností o tom, proč je pomalé.

### <a name="use-an-ilogger-interface"></a>Použití rozhraní ILogger

To, co doporučujeme při vytváření produkční aplikace, je vytvoření jednoduchého rozhraní *ILogger* a zaznamenání některých metod. Díky tomu je snadné změnit implementaci protokolování později a nemusíte projít celým vaším kódem. V rámci aplikace pro opravu IT můžeme použít třídu `System.Diagnostics.Trace`, ale místo toho ji používáme v rámci pokrývání třídy protokolování, která implementuje *ILogger*a provádíme volání metod *ILogger* v celé aplikaci.

V takovém případě můžete v případě, že někdy budete chtít, aby se protokolování nahlásilo, nahradit [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) jakýmkoli mechanismem protokolování, který chcete. Když se například vaše aplikace rozroste, můžete se rozhodnout, že chcete použít komplexnější balíček protokolování, jako je [nLOG](http://nlog-project.org/) nebo [blok aplikace protokolování podnikové knihovny](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx). ([Log4Net](http://logging.apache.org/log4net/) je další oblíbená architektura protokolování, ale neprovádí asynchronní protokolování.)

Jedním z možných důvodů použití architektury, jako je NLog, je usnadnit dělení výstupu protokolování do samostatných úložišť dat s vysokým objemem a vysoké hodnoty. To vám pomůže efektivně ukládat velké objemy dat informující o tom, že nepotřebujete provádět rychlé dotazy, a přitom zajistit rychlý přístup k datům ACT.

### <a name="semantic-logging"></a>Sémantické protokolování

Relativně nový způsob protokolování, který může vytvářet užitečnější diagnostické informace, najdete v tématu [blok aplikace sémantického protokolování v podnikové knihovně (oddíl)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). PLOŠINa používá [trasování událostí pro Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) a podporu technologie [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) v rozhraní .NET 4,5, aby bylo možné vytvářet více strukturovaných a Queryable protokolů. Můžete definovat jinou metodu pro každý typ události, kterou zaznamenáte, což vám umožní přizpůsobit informace, které zapisujete. Například pro protokolování chyby SQL Database můžete zavolat metodu `LogSQLDatabaseError`. Pro tento druh výjimky víte, že klíčovou částí informací je číslo chyby, takže můžete do signatury metody zahrnout parametr číslo chyby a zaznamenat číslo chyby jako samostatné pole v záznamu protokolu, který zapisujete. Vzhledem k tomu, že je číslo v samostatném poli, můžete snadněji a spolehlivě získávat sestavy založené na číslech chyb SQL, než byste mohli pouze zřetězit číslo chyby do řetězce zprávy.

## <a name="logging-in-the-fix-it-app"></a>Přihlášení do aplikace pro opravu IT

### <a name="the-ilogger-interface"></a>Rozhraní ILogger

Tady je rozhraní *ILogger* v aplikaci Fix it.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

Tyto metody umožňují zápis protokolů na stejných čtyřech úrovních podporovaných nástrojem *System. Diagnostics*. Metody TraceApi jsou k protokolování volání externích služeb s informacemi o latenci. Můžete také přidat sadu metod pro ladění/úroveň podrobností.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>Implementace protokolovacího nástroje rozhraní ILogger

Implementace rozhraní je skutečně jednoduchá. V podstatě pouze volá standardní metody *System. Diagnostics* . Následující fragment kódu ukazuje všechny tři metody informací a jednu z dalších.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>Volání metod ILogger

Pokaždé, když kód v aplikaci Fix it zachytí výjimku, zavolá metodu *ILogger* pro zaprotokolování podrobností o výjimce. A pokaždé, když provede volání do databáze, Blob service nebo REST API, spustí před voláním Stopwatch, zastaví Stopwatch při návratu služby a zaznamená uplynulý čas spolu s informacemi o úspěchu nebo neúspěchu.

Všimněte si, že zpráva protokolu obsahuje název třídy a název metody. Je vhodné zajistit, aby zprávy protokolu identifikovaly, kterou část kódu aplikace vytvořila.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

Takže teď pro pokaždé, když aplikace opravy IT nastavila volání SQL Database, uvidíte volání, metodu, která ji volala, a přesně to, jak dlouho trvalo.

![Dotaz SQL Database v protokolech](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

Pokud budete procházet protokoly, vidíte, že doba volání databáze je proměnná. Tyto informace mohou být užitečné: vzhledem k tomu, že aplikace protokoluje všechno, můžete analyzovat historické trendy v průběhu času v průběhu času databázová služba. Například služba může být v krátké době v čase, ale požadavky můžou selhat nebo může trvat zpomalení odezvy v určitou dobu.

Můžete to samé udělat pro Blob service – pro pokaždé, když aplikace nahraje nový soubor, se zobrazí protokol a uvidíte přesně, jak dlouho trvalo nahrávání každého souboru.

![Protokol nahrání objektu BLOB](monitoring-and-telemetry/_static/image23.png)

Je to jenom pár dalších řádků kódu, které se zapisují při každém volání služby, a teď vždycky, když někdo uvede, že se jedná o problém, přesně víte, co byl problém, nebo jestli byl právě pomalý. Můžete určit zdroj problému, aniž byste se museli vzdáleně přihlašovat k serveru, nebo zapnout protokolování, až k chybě dojde, a doufáme, že ho znovu vytvoříte.

## <a name="dependency-injection-in-the-fix-it-app"></a>Vkládání závislostí v aplikaci Fix it

Můžete si být u toho, jak konstruktor úložiště v příkladu zobrazeném výše získá implementaci rozhraní protokolovacího nástroje:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

Pro připojení rozhraní k implementaci aplikace používá [vkládání závislostí](http://en.wikipedia.org/wiki/Dependency_injection)(di) s [AutoFac](http://autofac.org/). DI vám umožňuje použít objekt založený na rozhraní na mnoha místech v kódu a musí se zadat jenom na jednom místě implementace, která se používá při vytváření instance rozhraní. To usnadňuje změnu implementace: například můžete chtít nahradit protokolovací nástroj System. Diagnostics pomocí protokolovacího nástroje NLog. Nebo pro automatizované testování byste mohli chtít nahradit podrobnější verzi protokolovacího nástroje.

Oprava IT aplikace používá DI ve všech úložištích a všech řadičích. Konstruktory tříd kontroleru získají rozhraní *ITaskRepository* stejným způsobem jako úložiště, které získá rozhraní protokolovacího nástroje:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

Aplikace používá knihovnu AutoFac DI k automatickému poskytování instancí *TaskRepository* a *protokolovacího* nástroje pro tyto konstruktory.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

Tento kód v podstatě říká, že kdekoli konstruktor potřebuje rozhraní *ILogger* , předejte instanci třídy *protokolovacího* nástroje a pokaždé, když potřebuje rozhraní *IFixItTaskRepository* , předejte instanci třídy *FixItTaskRepository* .

[AutoFac](http://autofac.org/) je jedním z mnoha rozhraní injektáže pro vkládání závislostí, které můžete použít. Další oblíbená z nich je [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx), což se doporučuje a podporuje vzory a postupy Microsoftu.

## <a name="built-in-logging-support-in-azure"></a>Integrovaná podpora protokolování v Azure

Azure podporuje následující typy [protokolování pro Web Apps v Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio):

- Trasování System. Diagnostics (můžete zapínat a vypínat a nastavovat úrovně za běhu bez restartování lokality).
- Události systému Windows.
- Protokoly služby IIS (HTTP/FREB).

Azure podporuje následující typy [přihlašování Cloud Services](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics):

- Trasování System. Diagnostics.
- Čítače výkonu.
- Události systému Windows.
- Protokoly služby IIS (HTTP/FREB).
- Monitorování vlastního adresáře.

Oprava aplikace IT používá trasování System. Diagnostics. Aby bylo možné povolit protokolování System. Diagnostics ve webové aplikaci, překlopte na portálu přepínač nebo zavolejte REST API. Na portálu klikněte na kartu **Konfigurace** vašeho webu a posuňte se dolů, aby se zobrazila část **Application Diagnostics** . Můžete zapnout nebo vypnout protokolování a vybrat úroveň protokolování, kterou požadujete. Můžete mít Azure zapisovat protokoly do systému souborů nebo do účtu úložiště.

![Diagnostika aplikací a diagnostika webu na kartě konfigurovat](monitoring-and-telemetry/_static/image24.png)

Po povolení protokolování v Azure můžete zobrazit protokoly v okně výstup sady Visual Studio při jejich vytváření.

![Nabídka protokoly streamování](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![Nabídka protokoly streamování](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

Do svého účtu úložiště můžete také zapisovat protokoly a zobrazit je s jakýmkoli nástrojem, který má přístup k Azure Storage Table service, jako je **Průzkumník serveru** v aplikaci Visual Studio nebo [Průzkumník služby Azure Storage](https://azure.microsoft.com/features/storage-explorer/).

![Přihlášení Průzkumník serveru](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>Přehled

Je velmi jednoduché implementovat předem připravený systém telemetrie, instrumentovat vlastní kód a konfigurovat protokolování v Azure. A když máte problémy s produkčním prostředím, kombinace systému telemetrie a vlastních protokolů vám pomůže rychle vyřešit problémy předtím, než se stanou významnými problémy pro vaše zákazníky.

V [Další části](transient-fault-handling.md) se podíváme na to, jak zpracovávat přechodné chyby, aby se nestaly provozními problémy, které je třeba prozkoumat.

## <a name="resources"></a>Prostředky

Další informace najdete v následujících materiálech.

Dokumentace převážně o telemetrie:

- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Přečtěte si téma pokyny k instrumentaci a telemetrie, pokyny pro měření služby, model monitorování stavu a konfigurace modulu runtime.
- [Haléřové Pinching v cloudu: povoluje se nové Relic sledování výkonu na Azure websites](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx).
- [Osvědčené postupy pro návrh rozsáhlých služeb v Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Dokument White Paper, který označuje Simms a Michael Thomassy. Viz část telemetrie a diagnostika.
- [Vývoj nové generace pomocí Application Insights](https://msdn.microsoft.com/magazine/dn683794.aspx). Článek na webu MSDN Magazine.

Dokumentace zejména o protokolování:

- [Blok aplikace sémantického protokolování (oddíl)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). Neilem Mackenzie prezentuje případ sémantického protokolování pomocí PLOŠINy.
- [Vytváření strukturovaných a smysluplných protokolů s sémantickým protokolováním](https://channel9.msdn.com/Events/Build/2013/3-336) Obrazový Juliánské Dominguez představuje případ pro sémantické protokolování pomocí PLOŠINy.
- [EF6 protokolování SQL – část 1: jednoduché protokolování](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/). Arthur Vickers ukazuje, jak protokolovat dotazy spouštěné Entity Framework v EF 6.
- [Odolnost připojení a zachycení příkazů pomocí Entity Framework v aplikaci ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Čtvrtá série kurzů s devíti částmi ukazuje, jak používat funkci zachycení příkazu pro EF 6 k protokolování příkazů SQL odeslaných do databáze pomocí Entity Framework.
- [Vylepšete protokolování C# pomocí atributů informací o volajícím volání 5,0](http://www.dotnetcurry.com/showarticle.aspx?ID=972). Jak snadno protokolovat název volající metody bez nutnosti pevně zakódovat ho do literálů nebo pomocí reflexe získat ručně.

Dokumentace převážně o řešení potíží:

- [Řešení potíží s Azure &amp; ladění blogu](https://blogs.msdn.com/b/kwill/).
- [AzureTools – diagnostický nástroj používaný týmem Azure Developer Support](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true). Zavádí a poskytuje odkaz ke stažení pro nástroj, který se dá použít na virtuálním počítači Azure ke stažení a spuštění široké škály nástrojů pro diagnostiku a monitorování. Užitečné v případě, že potřebujete diagnostikovat problém na konkrétním virtuálním počítači.
- [Řešení potíží s webovou aplikací v Azure App Service pomocí sady Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). Podrobný kurz pro zahájení práce s trasováním System. Diagnostics a vzdáleným laděním.

Videa:

- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět částí podle Ulrich Homann, matolin Mercuri a označit Simms. Prezentuje základní koncepty a principy architektury v rámci velmi přístupného a zajímavého způsobu, který vychází ze zkušeností zákazníků Microsoftu pro poradenské zákazníky (CAT) se skutečnými zákazníky. Díly 4 a 9 se týkají monitorování a telemetrie. Díl 9 obsahuje přehled služeb monitorování MetricsHub, AppDynamics, New Relic a PagerDuty.
- [Sestavování velkých: lekcí získaných od zákazníků Azure – část II](https://channel9.msdn.com/Events/Build/2012/3-030). Označte Simms rozhovory o návrhu pro selhání a instrumentaci všeho. Podobně jako u řady Failsafe, ale odkazuje na další podrobnosti.

Ukázka kódu:

- [Základy cloudových služeb v Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Ukázková aplikace vytvořená Microsoft Azure poradenským týmem pro zákazníky. Ukazuje postupy telemetrie a protokolování, jak je vysvětleno v následujících článcích. Ukázka implementuje protokolování aplikace pomocí [nLOG](http://nlog-project.org/). Související dokumentaci najdete v [článku o telemetrie a protokolování na webu TechNet wiki](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon).

> [!div class="step-by-step"]
> [Předchozí](design-to-survive-failures.md)
> [Další](transient-fault-handling.md)
