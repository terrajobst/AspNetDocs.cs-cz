---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: Konfigurace a instrumentace | Microsoft Docs
author: microsoft
description: Konfigurace a instrumentace v ASP.NET 2,0 jsou významné změny. Nové rozhraní API konfigurace ASP.NET umožňuje provádět změny konfigurace...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: cd5bedce5459e8cf8e72df8de69ebd82f2d97789
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626026"
---
# <a name="configuration-and-instrumentation"></a>Konfigurace a instrumentace

od [Microsoftu](https://github.com/microsoft)

> Konfigurace a instrumentace v ASP.NET 2,0 jsou významné změny. Nové rozhraní API konfigurace ASP.NET umožňuje provádět změny konfigurace prostřednictvím kódu programu. Kromě toho existuje mnoho nových nastavení konfigurace umožňujících nové konfigurace a instrumentaci.

Konfigurace a instrumentace v ASP.NET 2,0 jsou významné změny. Nové rozhraní API konfigurace ASP.NET umožňuje provádět změny konfigurace prostřednictvím kódu programu. Kromě toho existuje mnoho nových nastavení konfigurace umožňujících nové konfigurace a instrumentaci.

V tomto modulu probereme ASP.NET rozhraní API pro konfiguraci, protože souvisí s čtením a zápisem do konfiguračních souborů ASP.NET a my také pokryjeme instrumentaci ASP.NET. Také pokryjeme nové funkce, které jsou k dispozici v trasování ASP.NET.

## <a name="aspnet-configuration-api"></a>Rozhraní API pro konfiguraci ASP.NET

Rozhraní ASP.NET Configuration API umožňuje vyvíjet, nasazovat a spravovat konfigurační data aplikací pomocí jediného programovacího rozhraní. Rozhraní API pro konfiguraci můžete použít k vývoji a úpravám úplných konfigurací ASP.NET programově, aniž by bylo nutné přímo upravovat XML v konfiguračních souborech. Kromě toho můžete použít rozhraní API konfigurace v konzolových aplikacích a skriptech, které vyvíjíte, v nástrojích webové správy a v modulech snap-in konzoly MMC (Microsoft Management Console).

Následující dva nástroje pro správu konfigurace používají rozhraní API konfigurace a jsou součástí verze .NET Framework 2,0:

- Modul snap-in konzoly MMC ASP.NET, který používá rozhraní API konfigurace ke zjednodušení úloh správy a poskytuje integrované zobrazení dat místních konfigurací ze všech úrovní konfigurační hierarchie.
- Nástroj pro správu webu, který umožňuje spravovat nastavení konfigurace pro místní a vzdálené aplikace, včetně hostovaných lokalit.

Rozhraní ASP.NET Configuration API obsahuje sadu objektů správy ASP.NET, které můžete použít ke konfiguraci webových stránek a aplikací prostřednictvím kódu programu. Objekty správy jsou implementovány jako .NET Framework knihovny tříd. Programovací model rozhraní API pro konfiguraci pomáhá zajistit konzistenci a spolehlivost kódu vynucením datových typů v době kompilace. Aby bylo možné spravovat konfigurace aplikací snadněji, rozhraní API pro konfiguraci umožňuje zobrazit data sloučená ze všech bodů v konfigurační hierarchii jako jednu kolekci, namísto zobrazení dat jako samostatných kolekcí z různých konfigurační soubory. Rozhraní API pro konfiguraci navíc umožňuje manipulovat s celou konfigurací aplikace bez nutnosti přímo upravovat XML v konfiguračních souborech. Rozhraní API nakonec zjednodušuje konfigurační úlohy tím, že podporuje nástroje pro správu, jako je například nástroj pro správu webu. Rozhraní API pro konfiguraci zjednodušuje nasazení tím, že podporuje vytváření konfiguračních souborů na počítači a spouštění konfiguračních skriptů napříč více počítači.

> [!NOTE]
> Rozhraní API pro konfiguraci nepodporuje vytváření aplikací služby IIS.

## <a name="working-with-local-and-remote-configuration-settings"></a>Práce s nastavením místních a vzdálených konfigurací

Objekt konfigurace představuje sloučené zobrazení nastavení konfigurace, která se vztahují na konkrétní fyzickou entitu, jako je například počítač nebo na logickou entitu, jako je například aplikace nebo Web. Zadaná logická entita může existovat v místním počítači nebo na vzdáleném serveru. Pokud pro zadanou entitu neexistuje konfigurační soubor, představuje objekt konfigurace výchozí nastavení konfigurace definované souborem Machine. config.

Objekt konfigurace můžete získat pomocí jedné z otevřených metod konfigurace z následujících tříd:

1. Třída ConfigurationManager, pokud vaše entita je klientská aplikace.
2. Třída funkci WebConfigurationManager, pokud vaše entita je webová aplikace.

Tyto metody vrátí objekt konfigurace, který zase poskytne požadované metody a vlastnosti, které budou zpracovávat základní konfigurační soubory. K těmto souborům můžete přistupovat pro čtení nebo zápis.

### <a name="reading"></a>Čtení

K načtení informací o konfiguraci použijte metodu GetSection nebo GetSectionGroup. Uživatel nebo proces, který čte, musí mít oprávnění ke čtení pro všechny konfigurační soubory v hierarchii.

> [!NOTE]
> Použijete-li statickou metodu GetSection, která přijímá parametr Path, parametr Path musí odkazovat na aplikaci, ve které je kód spuštěn. V opačném případě se parametr ignoruje a vrátí se informace o konfiguraci aktuálně spuštěné aplikace.

### <a name="writing"></a>Zapsat

K zápisu informací o konfiguraci se používá jedna z metod uložení. Uživatel nebo proces, který zápis zapisuje, musí mít oprávnění k zápisu do konfiguračního souboru a adresáře na úrovni aktuální hierarchie konfigurace a také oprávnění ke čtení pro všechny konfigurační soubory v hierarchii.

Pokud chcete vygenerovat konfigurační soubor, který představuje zděděné nastavení konfigurace pro zadanou entitu, použijte jednu z následujících metod Save-Configuration:

1. Metoda Save pro vytvoření nového konfiguračního souboru.
2. Metoda SaveAs pro vygenerování nového konfiguračního souboru v jiném umístění.

## <a name="configuration-classes-and-namespaces"></a>Třídy konfigurace a obory názvů

Mnoho tříd a metod konfigurace je podobných. Následující tabulka popisuje nejběžněji používané konfigurační třídy a obory názvů.

| **Konfigurační třída nebo obor názvů** | **Popis** |
| --- | --- |
| Obor názvů [System. Configuration](https://msdn.microsoft.com/library/system.configuration.aspx) | Obsahuje hlavní třídy konfigurace pro všechny .NET Framework aplikace. Třídy obslužných rutin oddílu slouží k získávání konfiguračních dat pro oddíl z metod, jako je GetSection a GetSectionGroup. Tyto dvě metody jsou nestatické. |
| System. Configuration. Configuration – třída | Představuje sadu konfiguračních dat pro počítač, aplikaci, webový adresář nebo jiný prostředek. Tato třída obsahuje užitečné metody, jako je GetSection a GetSectionGroup, pro aktualizaci nastavení konfigurace a získání odkazů na oddíly a skupiny oddílů. Tato třída se používá jako návratový typ pro metody, které získávají konfigurační data pro dobu návrhu, jako jsou metody tříd funkci WebConfigurationManager a ConfigurationManager. |
| Obor názvů System. Web. Configuration | Obsahuje třídy obslužných rutin oddílu pro konfigurační oddíly ASP.NET definované v [nastavení konfigurace ASP.NET](https://msdn.microsoft.com/library/b5ysx397.aspx). Třídy obslužných rutin oddílu slouží k získávání konfiguračních dat pro oddíl z metod, jako je GetSection a GetSectionGroup. |
| System.Web.Configuration.WebConfigurationManager class | Poskytuje užitečné metody pro získání odkazů na konfigurační nastavení v době běhu a v době návrhu. Tyto metody používají třídu System. Configuration. Configuration jako návratový typ. Metodu static GetSection této třídy nebo nestatickou metodu GetSection třídy System. Configuration. ConfigurationManager lze použít jako zaměnitelné. Pro konfigurace webových aplikací se doporučuje třída System. Web. Configuration. funkci WebConfigurationManager namísto třídy System. Configuration. ConfigurationManager. |
| Obor názvů [System. Configuration. Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx) | Poskytuje způsob, jak přizpůsobit a roztáhnout poskytovatele konfigurace. Toto je základní třída pro všechny třídy poskytovatele v konfiguračním systému. |
| Obor názvů [System. Web. Management](https://msdn.microsoft.com/library/system.web.management.aspx) | Obsahuje třídy a rozhraní pro správu a monitorování stavu webových aplikací. Výhradně řečeno, tento obor názvů není považován za součást konfiguračního rozhraní API. Například trasování a vyvolávání událostí je dosaženo třídami v tomto oboru názvů. |
| Obor názvů [System. Management. Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) | Poskytuje třídy potřebné k tomu, aby instrumentace aplikací zveřejnila své informace o správě a události prostřednictvím rozhraní WMI (Windows Management Instrumentation) (WMI) k potenciálním spotřebitelům. Sledování stavu ASP.NET využívá rozhraní WMI k doručování událostí. Výhradně řečeno, tento obor názvů není považován za součást konfiguračního rozhraní API. |

## <a name="reading-from-aspnet-configuration-files"></a>Čtení z konfiguračních souborů ASP.NET

Třída funkci WebConfigurationManager je základní třídou pro čtení z konfiguračních souborů ASP.NET. Existují v podstatě tři kroky pro čtení konfiguračních souborů ASP.NET:

1. Získání objektu konfigurace pomocí metody OpenWebConfiguration
2. Získejte odkaz na požadovaný oddíl v konfiguračním souboru.
3. Přečtěte si požadované informace z konfiguračního souboru.

Objekt konfigurace představuje nereprezentuje konkrétní konfigurační soubor. Místo toho představuje sloučené zobrazení konfigurace počítače, aplikace nebo webu. Následující ukázka kódu vytvoří instanci objektu konfigurace, která představuje konfiguraci webové aplikace s názvem *ProductInfo*.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> Všimněte si, že pokud cesta/ProductInfo neexistuje, bude výše uvedený kód vracet výchozí konfiguraci, jak je uvedeno v souboru Machine. config.

Jakmile budete mít objekt konfigurace, můžete pomocí metody GetSection nebo GetSectionGroup přejít k nastavení konfigurace. Následující příklad získá odkaz na nastavení zosobnění pro výše uvedenou aplikaci ProductInfo:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>Zápis do konfiguračních souborů ASP.NET

Jako při čtení z konfiguračních souborů je třída funkci WebConfigurationManager základem pro zápis do konfiguračních souborů Asp.NET. Existují také tři kroky pro zápis do konfiguračních souborů ASP.NET.

1. Získání objektu konfigurace pomocí metody OpenWebConfiguration
2. Získejte odkaz na požadovaný oddíl v konfiguračním souboru.
3. Pomocí metody Save nebo SaveAs zapište požadované informace z konfiguračního souboru.

Následující kód změní atribut **Debug** elementu &lt;Compilation&gt; na hodnotu false:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

Po spuštění tohoto kódu se atribut **ladění** &lt;&gt; elementu compilation nastaví na hodnotu false pro soubor Web. config aplikace *WebApp* .

## <a name="systemwebmanagement-namespace"></a>System.Web.Management Namespace

Obor názvů System. Web. Management poskytuje třídy a rozhraní pro správu a monitorování stavu aplikací ASP.NET.

Protokolování se provádí definováním pravidla, které přidruží události ke zprostředkovateli. Pravidlo definuje typ událostí, které jsou odeslány poskytovateli. Následující základní události jsou k dispozici pro přihlášení:

| **EventCode** | Základní třída Event pro všechny události. Obsahuje vlastnosti vyžadované pro všechny události, jako je kód události, kód podrobností události, datum a čas vyvolání události, číslo sekvence, zpráva události a podrobnosti události. |
| --- | --- |
| **WebManagementEvent** | Základní třída Event pro události správy, například události životnosti aplikace, požadavek, chyba a audit. |
| **WebHeartbeatEvent** | Událost generovaná aplikací v pravidelných intervalech pro zachycení užitečných informací o stavu modulu runtime. |
| **WebAuditEvent** | Základní třída pro události auditu zabezpečení, které se používají k označení podmínek, jako je například Chyba autorizace, selhání dešifrování *atd.* |
| **WebRequestEvent** | Základní třída pro všechny informativní události požadavku. |
| **WebBaseErrorEvent** | Základní třída pro všechny události, které indikují chybové stavy. |

Typy zprostředkovatelů, které jsou k dispozici, vám umožní posílat výstup události do Prohlížeč událostí, SQL Server, rozhraní WMI (Windows Management Instrumentation) (WMI) a e-mailu. Předem nakonfigurované zprostředkovatele a mapování událostí omezují množství práce potřebné k načtení protokolu událostí.

ASP.NET 2,0 používá ke zpracování událostí v závislosti na doménách aplikací, které se spouštějí a zastavují, a také protokolování všech neošetřených výjimek do protokolu událostí. To pomáhá pokrýt některé ze základních scénářů. Řekněme například, že vaše aplikace vyvolá výjimku, ale uživatel chybu neuloží a nemůžete ho reprodukováni. S výchozím pravidlem protokolu událostí byste mohli shromáždit výjimku a informace zásobníku a získat tak lepší představu o tom, jaký druh chyby došlo. Další příklad se vztahuje, pokud vaše aplikace ztratí stav relace. V takovém případě můžete vyhledat v protokolu událostí, zda se doména aplikace recykluje a proč se doména aplikace zastavila na prvním místě.

Systém monitorování stavu je také rozšiřitelný. Můžete například definovat vlastní webové události, aktivovat je v rámci aplikace a potom definovat pravidlo pro odeslání informací o události poskytovateli, jako je například váš e-mail. To vám umožní snadnou vazbu vaší instrumentace s poskytovateli sledování stavu. V dalším příkladu byste mohli vyvolat událost pokaždé, když se zpracuje objednávka, a nastavit pravidlo, které odešle každou událost do databáze SQL Server. Můžete taky vyvolat událost, když se uživatel neúspěšně přihlašuje víckrát na řádku a nastaví událost pro použití e-mailových poskytovatelů.

Konfigurace pro výchozí zprostředkovatele a události je uložena v globálním souboru Web. config. Globální soubor Web. config ukládá všechna webová nastavení, která byla uložena v souboru Machine. config v ASP.NET 1x. Globální soubor Web. config je umístěný v následujícím adresáři:

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

Oddíl &lt;healthMonitoring&gt; globálního souboru Web. config poskytuje výchozí nastavení konfigurace. Můžete přepsat tato nastavení nebo nakonfigurovat vlastní nastavení implementací oddílu &lt;healthMonitoring&gt; v souboru Web. config pro vaši aplikaci.

Oddíl &lt;healthMonitoring&gt; globálního souboru Web. config obsahuje následující položky:

| **dodavateli** | Obsahuje zprostředkovatele nastavené pro Prohlížeč událostí, rozhraní WMI a SQL Server. |
| --- | --- |
| **eventMappings** | Obsahuje mapování pro různé třídy WebBase. Tento seznam můžete roztáhnout, pokud vygenerujete vlastní třídu Event. Vygenerování vlastní třídy Event poskytuje přesnější členitost poskytovatelům, kterým odesíláte informace. Můžete například nakonfigurovat neošetřené výjimky, které budou odesílány do SQL Server, při posílání vlastních událostí do e-mailu. |
| **pravidly** | Propojí pole eventMappings se zprostředkovatelem. |
| **do vyrovnávací paměti** | Používá se pro SQL Server a poskytovatele e-mailů k určení, jak často se mají události vyprázdnit poskytovateli. |

Níže je příklad kódu z globálního souboru Web. config.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>Jak ukládat události do Prohlížeč událostí

Jak bylo zmíněno dříve, poskytovatel pro protokolování událostí v Prohlížeč událostí je nakonfigurován v globálním souboru Web. config. Ve výchozím nastavení jsou protokolovány všechny události založené na **WebBaseErrorEvent** a **WebFailureAuditEvent** . Můžete přidat další pravidla, která zaprotokolují Další informace do protokolu událostí. Pokud jste například chtěli protokolovat všechny události (*tj.* každou událost na základě **EventCode**), mohli byste do souboru Web. config přidat následující pravidlo:

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

Toto pravidlo by propojí mapu událostí **všechny události** s poskytovatelem protokolu událostí. V globálním souboru Web. config jsou uvedeny oba tabulka eventMapping i zprostředkovatel.

## <a name="how-to-store-events-to-sql-server"></a>Jak ukládat události do SQL Server

Tato metoda používá databázi **aspnetdb** , která je generována nástrojem ASPNET\_regsql. exe. Výchozí zprostředkovatel používá připojovací řetězec LocalSqlServer, který používá databázi založenou na souborech ve složce App\_data nebo v místní instanci SQLExpress SQL Server. Připojovací řetězec LocalSqlServer i SqlProvider jsou konfigurovány v globálním souboru Web. config.

Připojovací řetězec LocalSqlServer v globálním souboru Web. config vypadá takto:

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Chcete-li použít jinou instanci SQL Server, je nutné použít nástroj ASPNET\_regsql. exe, který lze najít v%windir%\Microsoft.Net\Framework\v2.0.\* složky. Pomocí nástroje ASPNET\_regsql. exe vygenerujte vlastní databázi **aspnetdb** v instanci SQL Server a pak přidejte připojovací řetězec do konfiguračního souboru vašich aplikací a pak přidejte poskytovatele pomocí nového připojovacího řetězce. Jakmile budete mít vytvořenou databázi **aspnetdb** , budete muset nastavit pravidlo, které propojí tabulka eventMapping s SqlProvider.

Bez ohledu na to, jestli používáte výchozí SqlProvider, nebo nakonfigurovat vlastního poskytovatele, budete muset přidat pravidlo spojující zprostředkovatele s mapou událostí. Následující pravidlo propojuje nového poskytovatele, kterého jste vytvořili výše, s mapou události **všechny události** . Toto pravidlo zaznamená všechny události založené na **EventCode** a pošle je do MySqlWebEventProvider, které budou používat připojovací řetězec MYASPNETDB. Následující kód přidá pravidlo pro propojení poskytovatele s mapou události:

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

Pokud jste chtěli odeslat jenom chyby SQL Server, můžete přidat následující pravidlo:

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Postup přeposílání událostí do rozhraní WMI

Události můžete také přeposláním do WMI. Zprostředkovatel rozhraní WMI je ve výchozím nastavení nakonfigurován v globálním souboru Web. config.

Následující příklad kódu přidá pravidlo pro přeposílání událostí do rozhraní WMI:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

Budete muset přidat pravidlo, které přiřadí tabulka eventMapping k poskytovateli, a také aplikaci naslouchacího procesu WMI, která bude naslouchat událostem. Následující příklad kódu přidá pravidlo pro propojení zprostředkovatele rozhraní WMI s mapou události **všechny události** :

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>Postup přeposílání událostí do e-mailu

Můžete také přeslat události do e-mailu. Dejte pozor na to, která pravidla událostí namapujete na svého poskytovatele e-mailu, protože si můžete omylně poslat spoustu informací, které můžou být vhodnější pro SQL Server nebo protokol událostí. Existují dva poskytovatelé e-mailu. SimpleMailWebEventProvider a TemplatedMailWebEventProvider. Každá z nich má stejné atributy konfigurace s výjimkou atributů Template a detailedTemplateErrors, které jsou k dispozici pouze v TemplatedMailWebEventProvider.

> [!NOTE]
> Ani tito poskytovatelé e-mailů nejsou pro vás nakonfigurované. Budete je muset přidat do souboru Web. config.

Hlavním rozdílem mezi těmito dvěma poskytovateli e-mailů je, že SimpleMailWebEventProvider posílá e-maily v obecné šabloně, kterou nelze upravovat. Ukázkový soubor Web. config přidá tohoto poskytovatele e-mailu do seznamu nakonfigurovaných zprostředkovatelů pomocí následujícího pravidla:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

K propojení poskytovatele e-mailu s mapou události **všechny události** se přidá taky následující pravidlo:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2,0 – trasování

Existují tři hlavní vylepšení pro trasování v ASP.NET 2,0.

1. Funkce integrovaného trasování
2. Programový přístup k trasovacím zprávám
3. Vylepšené trasování na úrovni aplikace

## <a name="integrated-tracing-functionality"></a>Funkce integrovaného trasování

Nyní můžete směrovat zprávy vydávané třídou System. Diagnostics. Trace, aby ASP.NET výstup trasování, a směrovat zprávy vysílané trasováním ASP.NET do System. Diagnostics. Trace. Události instrumentace ASP.NET můžete také přeslat do System. Diagnostics. Trace. Tuto funkci poskytuje nový atribut **writeToDiagnosticsTrace**&gt; elementu &lt;Trace. Pokud je tato logická hodnota true, zprávy trasování ASP.NET se předávají do infrastruktury trasování System. Diagnostics pro použití všemi naslouchacími procesy, které jsou zaregistrované pro zobrazení trasovacích zpráv.

## <a name="programmatic-access-to-trace-messages"></a>Programový přístup k trasovacím zprávám

ASP.NET 2,0 umožňuje programový přístup ke všem trasovacím zprávám prostřednictvím třídy **TraceContextRecord** a kolekce **TraceRecords** . Nejúčinnější způsob přístupu ke trasovacím zprávám je registrace delegáta **TraceContextEventHandler** (také novinka v ASP.NET 2,0) pro zpracování nové události **TraceFinished** . Podle potřeby můžete procházet zprávy trasování.

Následující ukázka kódu Tento příklad ilustruje:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

Ve výše uvedeném příkladu se smyčka provede kolekcí TraceRecords a pak se každou zprávu zapíše do datového proudu odpovědí.

## <a name="improved-application-level-tracing"></a>Vylepšené trasování na úrovni aplikace

Trasování na úrovni aplikace je vylepšeno prostřednictvím zavedení nového atributu **mostRecent**&gt; elementu &lt;Trace. Tento atribut určuje, zda je zobrazen poslední výstup trasování na úrovni aplikace a starší data trasování přesahující limity, které jsou označeny atributem requestLimit, jsou zahozeny. Je-li nastavena hodnota false, zobrazí se data trasování pro požadavky, dokud není dosaženo atributu requestLimit.

## <a name="aspnet-command-line-tools"></a>Nástroje příkazového řádku ASP.NET

Při konfiguraci ASP.NET je k dispozici několik nástrojů příkazového řádku. ASP.NET vývojáři by měli být obeznámeni s nástrojem ASPNET\_regiis. exe. ASP.NET 2,0 poskytuje tři další nástroje příkazového řádku, které pomáhají při konfiguraci.

K dispozici jsou následující nástroje příkazového řádku:

| **Nástroj** | **Použití** |
| --- | --- |
| **ASPNET\_regiis. exe** | Umožňuje registraci ASP.NET se službou IIS. Existují dvě verze těchto nástrojů, které jsou dodávány s ASP.NET 2,0, jeden pro 32 systémy (ve složce Framework) a jeden pro 64-bit Systems (ve složce Framework64). Verze 64 nebude nainstalována na 32 operačním systému. |
| **ASPNET\_regsql. exe** | Nástroj pro registraci SQL Server ASP.NET slouží k vytvoření databáze Microsoft SQL Server pro použití poskytovateli SQL Server v ASP.NET nebo k přidání nebo odebrání možností z existující databáze. Soubor ASPNET\_regsql. exe je umístěný ve složce [jednotka:] \WINDOWS\Microsoft.NET\Framework\versionNumber na vašem webovém serveru. |
| **ASPNET\_regbrowsers. exe** | Nástroj pro registraci prohlížeče ASP.NET analyzuje a zkompiluje všechny definice prohlížečů v celém systému do sestavení a nainstaluje sestavení do globální mezipaměti sestavení (GAC). Nástroj používá definiční soubory prohlížeče (. Soubory prohlížeče) z podadresáře .NET Framework prohlížeče. Nástroj najdete v adresáři%SystemRoot%\Microsoft.NET\Framework\version\. |
| **ASPNET\_Compiler. exe** | Nástroj ASP.NET Compilation umožňuje kompilovat webovou aplikaci v ASP.NET, ať už na místě, nebo pro nasazení do cílového umístění, jako je například provozní server. Místní kompilace pomáhá výkon aplikace, protože koncoví uživatelé nenaleznou zpoždění prvního požadavku na aplikaci, zatímco je aplikace zkompilována. |

Vzhledem k tomu, že nástroj ASPNET\_regiis. exe není novinkou ASP.NET 2,0, nebudeme ho tady pojednávat.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>Nástroj pro registraci SQL Server ASP.NET – ASPNET\_regsql. exe

Pomocí nástroje pro registraci SQL Server ASP.NET můžete nastavit několik typů možností. Můžete zadat připojení SQL, určit, které ASP.NET aplikační služby se mají použít SQL Server ke správě informací, určení, která databáze nebo tabulka se používá pro funkci závislosti mezipaměti SQL, a přidání nebo odebrání podpory pro použití SQL Server k ukládání procedur a stavu relace.

Několik aplikačních služeb ASP.NET využívá poskytovatele ke správě ukládání a načítání dat ze zdroje dat. Každý zprostředkovatel je specifický pro zdroj dat. ASP.NET obsahuje poskytovatele SQL Server pro tyto funkce ASP.NET:

- Členství (třída [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) ).
- Správa rolí (třída [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) ).
- Profil (třída [SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx) ).
- Přizpůsobení Webové části (třída [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx) ).
- Webové události (třída [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx) ).

Když nainstalujete ASP.NET, soubor Machine. config pro server obsahuje prvky konfigurace, které určují poskytovatele SQL Server pro každou z funkcí ASP.NET, které jsou závislé na poskytovateli. Tito zprostředkovatelé se ve výchozím nastavení nakonfigurují pro připojení k místní uživatelské instanci SQL Server Express 2005. Pokud změníte výchozí připojovací řetězec používaný poskytovateli, pak předtím, než budete moci použít kteroukoli z funkcí ASP.NET nakonfigurovaných v konfiguraci počítače, je nutné nainstalovat databázi SQL Server a prvky databáze pro vaši zvolenou funkci pomocí ASPNET\_regsql. exe. Pokud databáze, kterou zadáte pomocí nástroje pro registraci SQL, ještě neexistuje (vytvoří se výchozí databáze, pokud není zadaná v příkazovém řádku), musí mít aktuální uživatel práva k vytváření databází v SQL Server a také vytváření schématu e. lements v rámci databáze.

### <a name="sql-cache-dependency"></a>Závislost mezipaměti SQL

Pokročilá funkce ukládání výstupu do mezipaměti ASP.NET je závislost mezipaměti SQL. Závislost mezipaměti SQL podporuje dva různé režimy provozu: jeden, který používá implementaci ASP.NET pro dotazování tabulky a druhý režim, který používá funkce oznamování dotazů SQL Server 2005. Nástroj pro registraci SQL se dá použít ke konfiguraci režimu cyklického dotazování tabulky.

### <a name="session-state"></a>Stav relace

Ve výchozím nastavení jsou hodnoty stavu relace a informace uloženy v paměti v rámci procesu ASP.NET. Případně můžete data relace ukládat do databáze SQL Server, kde ji můžete sdílet s více webovými servery. Pokud databáze, kterou zadáte pro stav relace s nástrojem pro registraci SQL, ještě neexistuje, musí mít aktuální uživatel práva k vytváření databází v SQL Server a také k vytváření elementů schématu v rámci databáze. Pokud databáze existuje, musí mít aktuální uživatel práva k vytváření elementů schématu v existující databázi.

Chcete-li nainstalovat databázi stavu relace na SQL Server, spusťte nástroj ASPNET\_regsql. exe a zadejte následující informace s příkazem:

- Název instance SQL Server s použitím možnosti **-S** .
- Přihlašovací údaje pro účet, který má oprávnění k vytvoření databáze na počítači se systémem SQL Server. Použijte možnost **-E** k používání aktuálně přihlášeného uživatele nebo použijte možnost **-U** k zadání hesla a zadáním ID uživatele spolu s možností **-P** .
- Možnost příkazového řádku **-ssadd** pro přidání databáze stavu relace.

Ve výchozím nastavení nemůžete použít nástroj ASPNET\_regsql. exe k instalaci databáze stavu relace do počítače se systémem SQL Server 2005 Express Edition.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>Nástroj pro registraci prohlížeče ASP.NET-ASPNET\_regbrowsers. exe

V ASP.NET verze 1,1 obsahuje soubor Machine. config oddíl s názvem &lt;browserCaps&gt;. Tato část obsahovala řadu položek XML, které definovaly konfigurace pro různé prohlížeče na základě regulárního výrazu. Pro ASP.NET verze 2,0, nový. Soubor prohlížeče definuje parametry konkrétního prohlížeče pomocí záznamů XML. Do nového prohlížeče přidáte informace přidáním nového. Soubor prohlížeče do složky umístěné na%SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers ve vašem systému.

Vzhledem k tomu, že aplikace nečte soubor. config pokaždé, když vyžaduje informace o prohlížeči, můžete vytvořit nový. Soubor prohlížeče a spuštěním ASPNET\_regbrowsers. exe přidejte požadované změny do sestavení. Díky tomu může server okamžitě přistupovat k novým informacím v prohlížeči, takže nemusíte vypínat žádné z vašich aplikací a vybírat informace. Aplikace může získat přístup k funkcím prohlížeče pomocí vlastnosti prohlížeče aktuálního HttpRequest.

Při spuštění ASPNET\_regbrowser. exe jsou k dispozici následující možnosti:

| **Možnost** | **Popis** |
| --- | --- |
| **-?** | Zobrazí text v nápovědě ASPNET\_regbbrowsers. exe v příkazovém okně. |
| **– i** | Vytvoří sestavení možností prohlížeče modulu runtime a nainstaluje ho do globální mezipaměti sestavení (GAC). |
| **-u** | Odinstaluje sestavení schopností prohlížeče modulu runtime z globální mezipaměti sestavení (GAC). |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>Nástroj ASP.NET Compilation – ASPNET\_Compiler. exe

Kompilační nástroj ASP.NET lze použít dvěma obecnými způsoby: pro místní kompilaci a kompilaci pro nasazení, kde je zadán cílový výstupní adresář.

### <a name="compiling-an-application-in-place"></a>[Kompilace aplikace na místě](https://msdn.microsoft.com/library/ms229863.aspx)

Kompilační nástroj ASP.NET může kompilovat aplikaci na místě, to znamená, že napodobuje chování při provádění více požadavků do aplikace, což způsobuje běžnou kompilaci. Uživatelům předkompilovaných webů nebude nacházet prodleva způsobená kompilováním stránky při prvním požadavku.

Když předkompilujete lokalitu na místě, platí následující položky:

- Lokalita si zachová své soubory a strukturu adresářů.
- Musíte mít kompilátory pro všechny programovací jazyky používané webem na serveru.
- Pokud dojde ke kompilaci jakéhokoli souboru, celá lokalita nebude zkompilována.

Můžete také znovu zkompilovat aplikaci na místě po přidání nových zdrojových souborů do této aplikace. Nástroj zkompiluje pouze nové nebo změněné soubory, Pokud nezahrnete možnost **-c** .

> [!NOTE]
> Kompilace aplikace, která obsahuje vnořenou aplikaci, nekompiluje vnořenou aplikaci. Vnořená aplikace musí být zkompilována samostatně.

### <a name="compiling-an-application-for-deployment"></a>[Kompilování aplikace pro nasazení](https://msdn.microsoft.com/library/ms229863.aspx)

Zkompilujete aplikaci pro nasazení (kompilace do cílového umístění) zadáním parametru targetDir. TargetDir může být konečné umístění webové aplikace nebo kompilovaná aplikace může být nasazena. Použití možnosti **-u** zkompiluje aplikaci takovým způsobem, že můžete provádět změny určitých souborů v kompilované aplikaci, aniž by bylo nutné je znovu kompilovat. ASPNET\_Compiler. exe rozlišuje mezi statickými a dynamickými typy souborů a zpracovává je jinak při vytváření výsledné aplikace.

- Statické typy souborů jsou ty, které nemají přidruženého kompilátoru nebo poskytovatele sestavení, jako jsou například soubory s názvem, jejichž přípona má přípony jako. CSS,. gif,. htm,. html,. jpg,. js a tak dále. Tyto soubory jsou jednoduše zkopírovány do cílového umístění, kde se jejich relativní místa v adresářové struktuře uchovávají.
- Dynamické typy souborů jsou ty, které mají přidruženého kompilátoru nebo poskytovatele sestavení, včetně souborů s příponou názvu souboru, které jsou specifické pro ASP.NET, například. asax,. ascx,. ashx,. aspx,. Browser,. Master a tak dále. Nástroj pro kompilaci ASP.NET generuje sestavení z těchto souborů. Pokud je možnost **-u** vynechána, nástroj také vytvoří soubory s příponou názvu souboru. KOMPILOVÁNo, které mapuje původní zdrojové soubory na jejich sestavení. Aby bylo zajištěno, že bude zachována adresářová struktura zdroje aplikace, nástroj vygeneruje v odpovídajících umístěních v cílové aplikaci zástupné soubory.

Pro indikaci, že obsah kompilované aplikace lze upravit, je nutné použít parametr **-u** . V opačném případě jsou následné změny ignorovány nebo způsobují chyby v době běhu.

Následující tabulka popisuje, jak Nástroj pro kompilaci ASP.NET zpracovává různé typy souborů, pokud je zahrnutá možnost **-u** .

| **Typ souboru** | **Akce kompilátoru** |
| --- | --- |
| .ascx, .aspx, .master | Tyto soubory jsou rozděleny do značek a zdrojového kódu, který zahrnuje jak soubory kódu na pozadí, tak i jakýkoli kód, který je uzavřen v &lt;&gt; prvky skriptu runat = "Server". Zdrojový kód je zkompilován do sestavení s názvy, které jsou odvozeny z algoritmu hash, a sestavení jsou umístěna do adresáře bin. Všechny vložené kódy, tj. kód uzavřený mezi **&lt;%** a **%&gt;** závorky, jsou součástí kódu a nejsou kompilovány. Vytvoří se nové soubory se stejným názvem, jako jsou zdrojové soubory, aby obsahovaly značky a umístily do odpovídajících výstupních adresářů. |
| .ashx, .asmx | Tyto soubory nejsou kompilovány a přesunuty do výstupních adresářů tak, jak jsou, a nejsou kompilovány. Pokud chcete zkompilovat kód obslužné rutiny, umístěte kód do souboru zdrojového kódu v adresáři App\_Code. |
| cs,. vb,. jsl,. cpp (nezahrnuje soubory kódu na pozadí pro typy souborů, které jsou uvedeny dříve) | Tyto soubory jsou kompilovány a zahrnuty jako prostředek v sestaveních, která na ně odkazují. Zdrojové soubory nejsou zkopírovány do výstupního adresáře. Pokud se na soubor s kódem neodkazuje, není zkompilován. |
| Vlastní typy souborů | Tyto soubory nejsou kompilovány. Tyto soubory jsou zkopírovány do odpovídajících výstupních adresářů. |
| Soubory zdrojového kódu v podadresáři\_App Code | Tyto soubory jsou zkompilovány do sestavení a umístěny do adresáře bin. |
| soubory. resx a. Resources v podadresáři App\_GlobalResources | Tyto soubory jsou zkompilovány do sestavení a umístěny do adresáře bin. V hlavním výstupním adresáři není vytvořená podadresář aplikace\_GlobalResources a žádné soubory. resx nebo. Resources umístěné ve zdrojovém adresáři se zkopírují do výstupních adresářů. |
| soubory. resx a. Resources v podadresáři App\_LocalResources | Tyto soubory nejsou kompilovány a jsou zkopírovány do odpovídajících výstupních adresářů. |
| soubory. skinu v podadresáři aplikace\_ch motivů | Soubory. Skin a statické soubory motivů nejsou kompilovány a zkopírovány do odpovídajících výstupních adresářů. |
| . browser – statické typy souborů Web. config: sestavení, která už jsou přítomná v adresáři bin | Tyto soubory jsou zkopírovány do výstupních adresářů. |

Následující tabulka popisuje, jak Nástroj pro kompilaci ASP.NET zpracovává různé typy souborů, když je vynechána možnost **-u** .

| **Typ souboru** | **Akce kompilátoru** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | Tyto soubory jsou rozděleny do značek a zdrojového kódu, který zahrnuje jak soubory kódu na pozadí, tak i jakýkoli kód, který je uzavřen v &lt;&gt; prvky skriptu runat = "Server". Zdrojový kód je zkompilován do sestavení s názvy, které jsou odvozeny z algoritmu hash. Výsledná sestavení jsou umístěna do adresáře bin. Všechny vložené kódy, tj. kód uzavřený mezi **&lt;%** a **%&gt;** závorky, jsou součástí kódu a nejsou kompilovány. Kompilátor vytvoří nové soubory, které obsahují značky se stejným názvem, jako mají zdrojové soubory. Tyto výsledné soubory jsou umístěny do adresáře bin. Kompilátor také vytvoří soubory se stejným názvem, jako mají zdrojové soubory, ale s příponou. KOMPILOVÁNo obsahující informace o mapování. Okně. ZKOMPILOVANÉ soubory jsou umístěny ve výstupních adresářích odpovídajících původnímu umístění zdrojových souborů. |
| .ascx | Tyto soubory jsou rozděleny do značek a zdrojového kódu. Zdrojový kód je zkompilován do sestavení a umístěn do adresáře bin s názvy, které jsou odvozeny z algoritmu hash. Nejsou generovány žádné soubory značek. |
| cs,. vb,. jsl,. cpp (nezahrnuje soubory kódu na pozadí pro typy souborů, které jsou uvedeny dříve) | Zdrojový kód, na který odkazuje sestavení generovaná ze souborů. ascx,. ashx nebo. aspx, je zkompilován do sestavení a umístěn do adresáře bin. Nejsou kopírovány žádné zdrojové soubory. |
| Vlastní typy souborů | Tyto soubory jsou kompilovány jako dynamické soubory. V závislosti na typu souboru, na kterém jsou založeny, může kompilátor umístit soubory mapování ve výstupních adresářích. |
| Soubory v podadresáři\_App Code | Soubory zdrojového kódu v tomto podadresáři jsou zkompilovány do sestavení a umístěny do adresáře bin. |
| Soubory v podadresáři aplikace\_GlobalResources | Tyto soubory jsou zkompilovány do sestavení a umístěny do adresáře bin. V hlavním výstupním adresáři není vytvořená podadresář aplikace\_GlobalResources. Pokud konfigurační soubor určuje, že soubory appliesTo = "All",. resx a. Resources se zkopírují do výstupních adresářů. Nejsou zkopírovány, pokud se na ně odkazuje pomocí [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx). |
| soubory. resx a. Resources v podadresáři App\_LocalResources | Tyto soubory jsou zkompilovány do sestavení s jedinečnými názvy a umístěny do adresáře bin. Do výstupních adresářů se nekopírují žádné soubory. resx nebo. Resource. |
| soubory. skinu v podadresáři aplikace\_ch motivů | Motivy jsou kompilovány do sestavení a umístěny do adresáře bin. Pro soubory. Skin se vytvoří zástupné soubory a umístí se do odpovídajícího výstupního adresáře. Statické soubory (například. CSS) se zkopírují do výstupních adresářů. |
| . browser – statické typy souborů Web. config: sestavení, která už jsou přítomná v adresáři bin | Tyto soubory jsou zkopírovány do výstupního adresáře. |

### <a name="fixed-assembly-names"></a>[Názvy pevných sestavení](https://msdn.microsoft.com/library/ms229863.aspx##)

Některé scénáře, například nasazení webové aplikace pomocí Instalační služba systému Windows MSI, vyžadují použití konzistentních názvů souborů a obsahu a také konzistentní struktury adresářů k identifikaci sestavení nebo konfiguračních nastavení pro aktualizace. V těchto případech můžete použít možnost **-fixednames** a určit tak, že kompilační nástroj ASP.NET by měl kompilovat sestavení pro každý zdrojový soubor namísto použití objektu, kde je kompilováno více stránek do sestavení. To může vést k velkému počtu sestavení, takže pokud máte obavy s škálovatelností, měli byste tuto možnost používat opatrně.

### <a name="strong-name-compilation"></a>[Kompilace se silným názvem](https://msdn.microsoft.com/library/ms229863.aspx##)

K dispozici jsou možnosti **-APTCA**, **-delaysign**, **-** a **-keyfile** , takže můžete použít ASPNET\_Compiler. exe pro vytváření silně pojmenovaných sestavení bez použití [nástroje Strong Name (Sn. exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) samostatně. Tyto možnosti odpovídají, v uvedeném pořadí, k **AllowPartiallyTrustedCallersAttribute**, **/delaysign.** , **AssemblyKeyNameAttribute**a **AssemblyKeyFileAttribute**.

Diskuze o těchto atributech nespadají do rozsahu tohoto kurzu.

## <a name="labs"></a>Testovací prostředí

Každé z následujících cvičení sestaví v předchozí laboratoři. Budete je muset udělat v uvedeném pořadí.

## <a name="lab-1-using-the-configuration-api"></a>Testovací prostředí 1: použití rozhraní API pro konfiguraci

1. Vytvořte nový web s názvem *mod9lab*.
2. Přidejte do webu nový soubor webové konfigurace.
3. Do souboru Web. config přidejte následující:

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

Tím se zajistí, že budete mít oprávnění ukládat změny do souboru Web. config.

1. Přidejte nový ovládací prvek popisek na Default. aspx a změňte ID na **lblDebugStatus**.
2. Přidat nový ovládací prvek tlačítko na Default. aspx.
3. Změňte ID ovládacího prvku tlačítko na **btnToggleDebug** a text pro **přepnutí stavu ladění**.
4. Otevřete zobrazení kódu pro soubor kódu na pozadí default. aspx a přidejte příkaz **using** pro **System. Web. Configuration** následujícím způsobem:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. Přidejte do třídy dvě soukromé proměnné a stránku\_inicializační metodu, jak je znázorněno níže:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. Přidejte následující kód pro\_načtení stránky:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Uložte a přejděte na Default. aspx. Všimněte si, že ovládací prvek popisek zobrazí aktuální stav ladění.
2. Dvakrát klikněte na ovládací prvek tlačítko v návrháři a přidejte následující kód do události Click pro ovládací prvek tlačítko:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Uložte a přejděte na Default. aspx a klikněte na tlačítko.
2. Po kliknutí na tlačítko otevřete soubor Web. config a sledujte atribut **Debug** v části&gt; &lt;Compilation.

## <a name="lab-2-logging-application-restarts"></a>Testovací prostředí 2: protokolování restartování aplikace

V tomto testovacím prostředí vytvoříte kód, který vám umožní přepnout protokolování vypnutí aplikace, spuštění a opětovnou kompilaci v Prohlížeč událostí.

1. Přidejte DropDownList do default. aspx a změňte ID na ddlLogAppEvents.
2. Nastavte vlastnost **AutoPostBack** pro vlastnost DropDownList na **hodnotu true**.
3. Přidejte tři položky do kolekce Items pro DropDownList. Naplňte **text** pro první položku jako *hodnotu* a hodnotu-1. Nastavte **text** a **hodnotu** druhé položky na **true** a **text** a **hodnotu** třetí položky **false**.
4. Přidejte nový popisek na Default. aspx. Změňte ID na **lblLogAppEvents**.
5. Otevřete zobrazení kódu na pozadí pro default. aspx a přidejte novou deklaraci pro proměnnou typu HealthMonitoringSection, jak je znázorněno níže:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. Do existujícího kódu na stránce\_init přidejte následující kód:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. Dvakrát klikněte na DropDownList a přidejte následující kód do události SelectedIndexChanged:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Přejděte na Default. aspx.
2. Nastavte rozevírací seznam na **false**.
3. Vymažte protokol aplikace v Prohlížeč událostí.
4. Chcete-li změnit atribut ladění aplikace, klikněte na tlačítko.
5. Aktualizujte protokol aplikace v Prohlížeč událostí. 

    1. Byly zaznamenány nějaké události?
    2. Proč nebo proč ne?
6. Nastavte rozevírací seznam na **hodnotu true.**
7. Kliknutím na tlačítko přepnete atribut ladění aplikace.
8. Aktualizujte Prohlížeč událostí přihlašovacího jména aplikace. 

    1. Byly zaznamenány nějaké události?
    2. Jaký byl důvod vypnutí aplikace?
9. Experimentujte s zapnutím a vypnutím protokolování a podívejte se na změny provedené v souboru Web. config.

## <a name="more-information"></a>Další informace:

Model poskytovatele ASP.NET 2.0 umožňuje vytvářet vlastní poskytovatele pro nejen instrumentaci aplikace, ale pro spoustu dalších použití, jako je například členství, profily atd. Podrobné informace o tom, jak napsat vlastního poskytovatele pro protokolování událostí aplikace do textového souboru, najdete na [tomto odkazu](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp).
