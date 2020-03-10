---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: Co je nového v ASP.NET 4,5 a Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje nové funkce a vylepšení, které jsou představené v ASP.NET 4,5. Popisuje také vylepšení vývoje pro web...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526675"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>Novinky v ASP.NET 4.5 a v sadě Visual Studio 2012

> Tento dokument popisuje nové funkce a vylepšení, které jsou představené v ASP.NET 4,5. Popisuje také vylepšení vývoje webu v aplikaci Visual Studio 2012. Tento dokument byl původně publikován dne 29. února 2012.

- [ASP.NET Core Runtime a architektura](#_Toc318097372)

    - [Asynchronní čtení a zápis požadavků a odpovědí HTTP](#_Toc318097373)
    - [Vylepšení zpracování HttpRequest](#_Toc318097374)
    - [Asynchronní vyprázdnění odpovědi](#_Toc318097375)
    - [Podpora pro asynchronní moduly a obslužné rutiny založené na *úlohách* *await*](#_Toc318097376)
    - [Asynchronní moduly HTTP](#_Toc318097377)
    - [Asynchronní obslužné rutiny HTTP](#_Toc318097378)
    - [Nové funkce ověřování žádostí ASP.NET](#_Toc318097379)
    - [Odložené ověření žádosti ("opožděné")](#_Toc318097380)
    - [Podpora pro neověřené žádosti](#_Toc318097381)
    - [Knihovna AntiXSS](#_Toc318097382)
    - [Podpora protokolu WebSockets](#_Toc318097383)
    - [Vytváření sady a minifikace](#_Toc318097384)
    - [Vylepšení výkonu pro hostování webů](#_Toc_perf)

        - [Klíčové faktory výkonu](#_Toc_perf_1)
        - [Požadavky na nové funkce výkonu](#_Toc_perf_2)
        - [Sdílení společných sestavení](#_Toc_perf_3)
        - [Použití více jader JIT kompilace pro rychlejší spuštění](#_Toc_perf_4)
        - [Optimalizace shromažďování paměti pro optimalizaci paměti](#_Toc_perf_5)
        - [Předběžné načtení pro webové aplikace](#_Toc_perf_6)
- [Webové formuláře ASP.NET](#_Toc318097385)

    - [Ovládací prvky dat silného typu](#_Toc318097386)
    - [Vazby modelu](#_Toc318097387)

        - [Výběr dat](#_Toc318097388)
        - [Zprostředkovatelé hodnot](#_Toc318097389)
        - [Filtrování podle hodnot z ovládacího prvku](#_Toc318097390)
    - [Výrazy vázání dat kódované HTML](#_Toc318097391)
    - [Nenáročná ověření](#_Toc318097392)
    - [Aktualizace HTML5](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET webové stránky 2](#_Toc318097395)
- [Visual Studio 2012 Release Candidate](#_Toc318097396)

    - [Sdílení projektů mezi Visual Studio 2010 a Visual Studio 2012 Release Candidate (kompatibilita projektů)](#project-compatibility)
    - [Změny konfigurace v šablonách webu ASP.NET 4,5](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [Nativní podpora služby IIS 7 pro směrování ASP.NET](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [Editor HTML](#_Toc318097397)

        - [Inteligentní úlohy](#_Toc318097398)
        - [POČKA-podpora ARIA](#_Toc318097399)
        - [Nové fragmenty HTML5](#_Toc318097400)
        - [Extrahovat do uživatelského ovládacího prvku](#_Toc318097401)
        - [IntelliSense pro kód Nuggets v atributech](#_Toc318097402)
        - [Automatické přejmenování párové značky při přejmenování počáteční nebo uzavírací značky](#_Toc318097403)
        - [Generování obslužné rutiny událostí](#_Toc318097404)
        - [Inteligentní odsazení](#_Toc318097405)
        - [Automatické snížení dokončování příkazů](#_Toc318097406)
    - [Editor JavaScriptu](#_Toc318097407)

        - [Osnova kódu](#_Toc318097408)
        - [Spárování složených závorek](#_Toc318097409)
        - [Přejít k definici](#_Toc318097410)
        - [Podpora ECMAScript5](#_Toc318097411)
        - [IntelliSense modelu DOM](#_Toc318097412)
        - [Přetížení signatur VSDOC](#_Toc318097413)
        - [Implicitní odkazy](#_Toc318097414)
    - [Editor šablon stylů CSS](#_Toc318097415)

        - [Automatické snížení dokončování příkazů](#_Toc318097416)
        - [Hierarchické odsazení](#_Toc318097417)
        - [Podpora šablon stylů CSS hackatony](#_Toc318097418)
        - [Schémata specifická pro dodavatele (– MOZ-,-WebKit)](#_Toc318097419)
        - [Podpora komentářů a zrušení komentářů](#_Toc318097420)
        - [Výběr barvy](#_Toc318097421)
        - [Fragmenty](#_Toc318097422)
        - [Vlastní oblasti](#_Toc318097423)
    - [Inspektor stránky](#_Toc318097424)
    - [Publikování](#_Toc318097425)

        - [Profily publikování](#_Toc318097426)
        - [Předkompilace a sloučení ASP.NET](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [Právní omezení](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core Runtime a architektura

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>Asynchronní čtení a zápis požadavků a odpovědí HTTP

ASP.NET 4 zavedlo možnost číst entitu požadavku HTTP jako datový proud pomocí metody *HttpRequest. GetBufferlessInputStream není* . Tato metoda poskytuje přístup ke streamování do entity požadavku. Nicméně se prováděl synchronně, který je spojený s vláknem po dobu trvání žádosti.

ASP.NET 4,5 podporuje možnost asynchronního čtení datových proudů v entitě požadavku HTTP a možnost vyprázdnit asynchronně. ASP.NET 4,5 také umožňuje dvojí ukládání entity požadavku HTTP, která poskytuje snazší integraci s podřízenými obslužnými rutinami HTTP, jako jsou například obslužné rutiny stránky ASPX a řadiče ASP.NET MVC.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>Vylepšení zpracování HttpRequest

Odkaz na datový proud vrácený serverem ASP.NET 4,5 z *HttpRequest. GetBufferlessInputStream není* podporuje synchronní i asynchronní metody čtení. Objekt *Stream* vrácený z *GetBufferlessInputStream není* nyní implementuje metody BeginRead a funkci EndRead. Metody asynchronního *datového proudu* umožňují asynchronní čtení entity požadavku v blocích, zatímco ASP.NET uvolní aktuální vlákno mezi každou iterací asynchronního čtecího cyklu.

ASP.NET 4,5 taky přidalo doprovodnou metodu pro čtení entity požadavku v zásobníku způsobem: *HttpRequest. GetBufferedInputStream*. Toto nové přetížení funguje jako *GetBufferlessInputStream není*a podporuje synchronní i asynchronní čtení. Při čtení ale *GetBufferedInputStream* také kopíruje bajty entit do vnitřních vyrovnávacích pamětí ASP.NET, aby mohly podřízené moduly a obslužné rutiny stále přistupovat k entitě požadavku. Pokud například některý nadřazený kód v kanálu už přečte entitu žádosti pomocí *GetBufferedInputStream*, můžete dál používat *HttpRequest. Form* nebo *HttpRequest. Files*. To vám umožní provádět asynchronní zpracování v žádosti (například streamování velkého souboru do databáze), ale pořád spouštějte stránky. aspx a ASP.NET řadiče MVC.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>Asynchronní vyprázdnění odpovědi

Odesílání odpovědí klientovi HTTP může trvat značnou dobu, než je klient mnohem pryč nebo má připojení s malou šířkou pásma. Obvykle ASP.NET ukládá bajty odezvy při vytváření aplikací. ASP.NET pak provede jednu operaci odeslání časově rozlišených vyrovnávacích pamětí na konci zpracování žádosti.

Je-li odezva ve vyrovnávací paměti velká (například streamování velkého souboru do klienta), je nutné pravidelně volat *HttpResponse. Flush* pro odeslání výstupu do vyrovnávací paměti do klienta a zachování využití paměti v rámci řízení. Protože *vyprázdnění* je však synchronní volání, iterativní volání metody *flush* stále spotřebovává vlákno po dobu trvání potenciálně dlouho běžících požadavků.

ASP.NET 4,5 přidává podporu pro asynchronní provádění vyprázdnění pomocí metod *BeginFlush* a *EndFlush* třídy *HttpResponse* . Pomocí těchto metod můžete vytvořit asynchronní moduly a asynchronní obslužné rutiny, které přírůstkově odesílají data klientovi bez nutnosti vytvářet vlákna operačního systému. V mezi voláními *BeginFlush* a *EndFlush* , ASP.NET uvolní aktuální vlákno. Tím se podstatně sníží celkový počet aktivních vláken, která jsou potřeba k podpoře dlouhotrvajících stahování HTTP.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>Podpora pro asynchronní moduly a obslužné rutiny založené na *úlohách* *await*

.NET Framework 4 představila asynchronní programovací koncept, který se označuje jako *úloha*. Úkoly jsou reprezentovány typem *úkolu* a souvisejícími typy v oboru názvů *System. Threading. Tasks* . .NET Framework 4,5 sestavuje pomocí vylepšení kompilátoru, která usnadňují práci s objekty *úloh* . V .NET Framework 4,5 podporují kompilátory dvě nová klíčová slova: *await* a *Async*. Klíčové slovo *await* je syntaktická zkratka pro značící, že část kódu by měla asynchronně čekat na nějakou jinou část kódu. Klíčové slovo *Async* představuje pomocný parametr, který můžete použít k označení metod jako asynchronních metod založených na úlohách.

Kombinace *operátoru await*, *Async*a objektu *Task* usnadňuje psaní asynchronního kódu v rozhraní .NET 4,5. ASP.NET 4,5 podporuje tato zjednodušení s novými rozhraními API, která umožňují psát asynchronní moduly HTTP a asynchronní obslužné rutiny HTTP s využitím nových vylepšení kompilátoru.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>Asynchronní moduly HTTP

Předpokládejme, že chcete provést asynchronní práci v rámci metody, která vrací objekt *Task* . Následující příklad kódu definuje asynchronní metodu, která umožňuje asynchronní volání ke stažení domovské stránky společnosti Microsoft. Všimněte si použití klíčového slova *Async* v signatuře metody a volání *await* pro *DownloadStringTaskAsync*.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

To je všechno, co je potřeba napsat – .NET Framework automaticky zpracuje odvinutí zásobníku volání při čekání na dokončení stahování a také po dokončení stahování automaticky obnoví zásobník volání.

Nyní předpokládejme, že chcete použít tuto asynchronní metodu v asynchronním modulu ASP.NET HTTP. ASP.NET 4,5 obsahuje pomocnou metodu (*EventHandlerTaskAsyncHelper*) a nový typ delegáta (*TaskEventHandler*), který můžete použít k integraci asynchronních metod založených na úlohách se starším asynchronním programovacím modelem VYSTAVENÝM kanálem http ASP.NET. Tento příklad ukazuje, jak:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>Asynchronní obslužné rutiny HTTP

Tradiční přístup k psaní asynchronních obslužných rutin v ASP.NET je implementovat rozhraní *IHttpAsyncHandler* . ASP.NET 4,5 zavádí asynchronní základní typ *HttpTaskAsyncHandler* , který lze odvodit z, což výrazně usnadňuje zápis asynchronních obslužných rutin.

Typ *HttpTaskAsyncHandler* je abstraktní a vyžaduje, abyste přepsali metodu *ProcessRequestAsync* . Interně ASP.NET se postará o integraci návratové signatury (objektu *úlohy* ) *ProcessRequestAsync* se starším asynchronním programovacím modelem používaným kanálem ASP.NET.

Následující příklad ukazuje, jak lze použít *úlohu* a *očekávat* jako součást implementace asynchronní obslužné rutiny http:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>Nové funkce ověřování žádostí ASP.NET

Ve výchozím nastavení ASP.NET provádí ověření žádosti – prověřuje požadavky na hledání kódu nebo skriptu v polích, hlavičkách, souborech cookie a tak dále. Pokud je zjištěno, ASP.NET vyvolá výjimku. Tato možnost slouží jako první linii obrany proti potenciálním útokům prostřednictvím skriptování mezi weby.

ASP.NET 4,5 usnadňuje selektivní čtení neověřených dat žádosti. ASP.NET 4,5 také integruje oblíbenou knihovnu AntiXSS, která byla dříve externí knihovnou.

Vývojáři se často žádají o možnost selektivně vypnout ověřování žádostí pro své aplikace. Například pokud je vaše aplikace fóra software, možná budete chtít uživatelům umožnit odesílat příspěvky a komentáře ve formátu HTML, ale stále se ujistěte, že ověření žádosti kontroluje všechno ostatní.

ASP.NET 4,5 zavádí dvě funkce, které usnadňují selektivní práci s neověřeným vstupem: odložené ("opožděné") ověření žádosti a přístup k neověřeným datům žádosti.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>Odložené ověření žádosti ("opožděné")

V ASP.NET 4,5 se ve výchozím nastavení všechna data žádostí vztahují k žádosti o ověření. Aplikaci však můžete nakonfigurovat tak, aby odložit žádosti o ověření, dokud nebudete mít ve skutečnosti přístup k datům žádosti. (Někdy se označuje jako ověřování opožděným požadavkem na základě termínů, jako je opožděné načítání pro určité scénáře dat.) Aplikaci můžete nakonfigurovat tak, aby používala odložené ověřování v souboru Web. config nastavením atributu *RequestValidationMode* na 4,5 v prvku *httpRUntime* , jak je uvedeno v následujícím příkladu:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

Pokud je režim ověřování požadavku nastavený na 4,5, aktivuje se ověření žádosti jenom pro konkrétní hodnotu požadavku a jenom v případě, že váš kód přistupuje k této hodnotě. Například pokud váš kód získá hodnotu Request. Form ["fórum\_post"], ověření žádosti je vyvoláno pouze pro tento prvek v kolekci Form. Žádný z ostatních prvků v kolekci *formulářů* není ověřen. V předchozích verzích ASP.NET bylo vyvoláno ověření žádosti pro celou kolekci požadavků, pokud byl k jakémukoli prvku v kolekci otevřen. Nové chování usnadňuje různým součástem aplikací zobrazení různých dat požadavků, aniž by bylo nutné vyžádat ověřování v jiných částech.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>Podpora pro neověřené žádosti

Odložené ověření žádosti neřeší problém s selektivním obejít ověřením požadavku. Volání Request. Form ["fórum\_post"] stále aktivuje ověření žádosti pro tuto konkrétní hodnotu požadavku. Můžete však chtít získat přístup k tomuto poli bez aktivace ověřování, protože chcete v tomto poli povolený kód.

K tomu ASP.NET 4,5 teď podporuje neověřený přístup k žádostem o data. ASP.NET 4,5 obsahuje novou *neověřenou* vlastnost kolekce ve třídě *HttpRequest* . Tato kolekce poskytuje přístup ke všem běžným hodnotám požadavků na data, jako jsou *formuláře*, *řetězce dotazu*, *soubory cookie*a *adresy URL*.

Pomocí příkladu fóra si můžete přečíst neověřená data žádosti. Nejdřív musíte aplikaci nakonfigurovat tak, aby používala nový režim ověřování žádostí:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

Pak můžete použít vlastnost *HttpRequest. unvalidateed* pro čtení hodnoty neověřené formuláře:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> Zabezpečení – *používejte neověřená data žádosti s opatrností!* ASP.NET 4,5 přidal neověřené vlastnosti a kolekce požadavků, aby bylo snazší získat přístup k velmi konkrétním neověřeným datům žádosti. Je však nutné i nadále provádět vlastní ověřování pro nezpracovaná data žádosti, aby se zajistilo, že uživatelé nebudou uživatelům vykreslováni nebezpečný text.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>Knihovna AntiXSS

Vzhledem k oblíbenosti knihovny Microsoft AntiXSS Library teď ASP.NET 4,5 nově zahrnuje rutiny kódování jádra z verze 4,0 této knihovny.

Rutiny kódování jsou implementovány typem *AntiXssEncoder* v novém oboru názvů *System. Web. Security. AntiXSS* . Typ *AntiXssEncoder* můžete použít přímo voláním libovolné statické metody kódování, které jsou implementovány v typu. Nejjednodušší přístup k použití nových rutin anti-XSS je však nakonfigurovat aplikaci ASP.NET tak, aby ve výchozím nastavení používala třídu *AntiXssEncoder* . Chcete-li to provést, přidejte do souboru Web. config následující atribut:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

Pokud je atribut *encoderType* nastaven na použití typu *AntiXssEncoder* , všechna výstupní kódování v ASP.NET automaticky používá nové rutiny kódování.

Jedná se o části externí knihovny AntiXSS, které jsou součástí ASP.NET 4,5:

- *HtmlEncode*, *HtmlFormUrlEncode*a *HtmlAttributeEncode*
- *XmlAttributeEncode* a *XmlEncode*
- *UrlEncode* a *UrlPathEncode* (nové)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Podpora protokolu WebSockets

Protokol WebSockets je síťový protokol založený na standardech, který definuje způsob, jak vytvořit zabezpečenou obousměrnou komunikaci mezi klientem a serverem přes protokol HTTP v reálném čase. Společnost Microsoft spolupracovala s orgány standardu IETF i W3C, aby vám pomohly definovat protokol. Protokol WebSockets podporuje libovolný klient (ne jenom prohlížeče), přičemž společnost Microsoft investuje značné prostředky podporující protokol WebSockets v klientském i mobilním operačním systému.

Protokol WebSockets výrazně usnadňuje vytváření dlouhotrvajících přenosů dat mezi klientem a serverem. Například psaní aplikace chatu je mnohem snazší, protože je možné vytvořit skutečné dlouhotrvající připojení mezi klientem a serverem. Nemusíte se uchýlit k alternativním řešením, jako je pravidelné cyklické dotazování nebo dlouhé cyklické dotazování prostřednictvím protokolu HTTP pro simulaci chování soketu.

ASP.NET 4,5 a IIS 8 zahrnují podporu WebSocket na nízké úrovni, která vývojářům ASP.NET umožňuje používat spravovaná rozhraní API pro asynchronní čtení a zápis řetězců a binárních dat do objektu WebSockets. V případě ASP.NET 4,5 existuje nový obor názvů *System. Web. WebSockets* , který obsahuje typy pro práci s protokolem WebSockets.

Klient prohlížeče vytvoří připojení typu WebSocket vytvořením objektu *WebSocket* modelu DOM, který odkazuje na adresu URL v aplikaci ASP.NET, jak je uvedeno v následujícím příkladu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

Koncovým bodům WebSockets v ASP.NET můžete vytvořit pomocí libovolného typu modulu nebo obslužné rutiny. V předchozím příkladu byl použit soubor. ashx, protože soubory. ashx představují rychlý způsob, jak vytvořit obslužnou rutinu.

Podle protokolu WebSockets přijímá aplikace ASP.NET požadavek na WebSockets klienta, protože indikuje, že požadavek by měl být upgradován z požadavku HTTP GET na požadavek protokolu WebSockets. Tady je příklad:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

Metoda *AcceptWebSocketRequest* akceptuje delegáta funkce, protože ASP.NET odvíjí aktuální požadavek HTTP a pak přenáší řízení na delegáta funkce. Koncepčně tento přístup je podobný jako při použití metody *System. Threading. Thread*, kde definujete delegáta spuštění vlákna, ve kterém je prováděna práce na pozadí.

Po ASP.NET a klientovi úspěšně dokončili metodu handshake u WebSockets, ASP.NET volá vašeho delegáta a spustí se aplikace WebSockets. Následující příklad kódu ukazuje jednoduchou aplikaci pro ozvěnu, která používá integrovanou podporu WebSockets v ASP.NET:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

Podpora rozhraní .NET 4,5 pro klíčové slovo *await* a asynchronní operace založené na úlohách je přirozenou vhodnou pro psaní aplikací WebSockets. Příklad kódu ukazuje, že požadavek WebSockets se v ASP.NET spouští kompletně asynchronně. Aplikace počká asynchronně, aby se odeslala zpráva z klienta voláním metody *await Socket. Metody ReceiveAsync*. Podobně můžete odeslat asynchronní zprávu klientovi voláním metody *await Socket. SendAsync*.

V prohlížeči aplikace přijímá zprávy o soketech WebSocket prostřednictvím funkce *Message* . Chcete-li odeslat zprávu z prohlížeče, zavolejte metodu *Send* typu DOM objektu *WebSocket* , jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

V budoucnu můžeme pro tyto funkce vydávat aktualizace, které v této verzi pro aplikace WebSockets vypustily některé z kódů nízké úrovně, které jsou potřeba v této verzi.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>Sdružování a minifikace

Sdružování umožňuje kombinovat jednotlivé soubory JavaScriptu a CSS do sady, která může být zpracována jako jeden soubor. Minifikace dehustí soubory JavaScript a CSS odebráním prázdných a jiných znaků, které nejsou vyžadovány. Tyto funkce fungují s webovými formuláři, ASP.NET MVC a webovými stránkami.

Sady se vytvářejí pomocí třídy sady nebo jedné z jejích podřízených tříd, ScriptBundle a StyleBundle. Po nakonfigurování instance sady se sada zpřístupní pro příchozí požadavky pouhým přidáním do globální instance sady Prostředkůcollection. Ve výchozích šablonách se konfigurace sady prostředků provádí v souboru BundleConfig. Tato výchozí konfigurace vytvoří sady pro všechny základní skripty a soubory šablon stylů CSS používané šablonami.

Na sady jsou odkazovány v rámci zobrazení pomocí jedné z několika možných pomocných metod. Aby bylo možné podporovat vykreslování různých značek pro sadu při ladění a v režimu vydání, třídy ScriptBundle a StyleBundle mají pomocnou metodu, vykreslení. V režimu ladění vygeneruje vykreslování označení pro každý prostředek v sadě. V režimu vydání vygeneruje vykreslování jeden element označení pro celý svazek. Přepínání mezi režimem ladění a vydání lze dosáhnout úpravou atributu Debug elementu compilation v souboru Web. config, jak je znázorněno níže:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

Povolení nebo zakázání optimalizace je také možné nastavit přímo prostřednictvím vlastnosti kompletace. EnableOptimizations.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

Když jsou soubory seskupeny, jsou nejprve řazeny abecedně (podle způsobu jejich zobrazení v **Průzkumník řešení**). Jsou potom uspořádány tak, aby byly nejprve načteny známé knihovny a jejich vlastní rozšíření (například jQuery, MooTools a Dojo). Například Poslední objednávka pro sdružování složky skripty, jak vidíte výše, bude:

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a. js

Soubory CSS jsou také řazeny abecedně a pak znovu uspořádány tak, aby obnovily. CSS a normalizují. CSS přicházejí před jakýmkoli jiným souborem. Konečné řazení ve výše zobrazené složce stylů bude toto:

1. reset.css
2. Content. CSS
3. forms.css
4. globals.css
5. menu.css
6. styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Vylepšení výkonu pro hostování webů

.NET Framework 4,5 a Windows 8 přináší funkce, které vám pomůžou dosáhnout výrazného zvýšení výkonu pro úlohy webového serveru. To zahrnuje snížení (až 35%). v době spuštění i v paměti pro weby hostující webové servery, které používají ASP.NET.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>Klíčové faktory výkonu

V ideálním případě by měly být všechny weby aktivní a v paměti, aby se zajistila rychlá odezva na další požadavek, kdykoli tam přijde. Mezi faktory, které mohou ovlivnit odezvu lokality, patří:

- Čas potřebný k restartování lokality po recyklaci fondu aplikací. Toto je čas potřebný ke spuštění procesu webového serveru pro lokalitu, když jsou sestavení lokality již v paměti. (Sestavení platformy jsou stále v paměti, protože jsou používány jinými lokalitami.) Tato situace je označována jako "studená lokalita, spuštění s teplým rozhraním" nebo pouze "spuštění z studené lokality".
- Kolik paměti web zabírá. Jedná se o využití paměti na webu nebo nesdílená pracovní sada.

Nové vylepšení výkonu se zaměřuje na oba tyto faktory.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>Požadavky na nové funkce výkonu

Požadavky na nové funkce lze rozdělit do těchto kategorií:

- Vylepšení, která běží na .NET Framework 4.
- Vylepšení, která vyžadují .NET Framework 4,5, ale mohou běžet v libovolné verzi systému Windows.
- Vylepšení, která jsou k dispozici pouze s .NET Framework 4,5 spuštěnou v systému Windows 8.

Výkon se zvyšuje s každou úrovní vylepšení, kterou máte možnost povolit.

Některá vylepšení .NET Framework 4,5 využívají širší funkce výkonu, které platí i pro jiné scénáře.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>Sdílení společných sestavení

**Požadavek**: .NET Framework 4 a sada Visual Studio 11 Developer Preview SDK

Různé weby na serveru často používají stejná pomocná sestavení (například sestavení ze sady počátečních nebo ukázkových aplikací). Každá lokalita má svou vlastní kopii těchto sestavení v adresáři bin. I když je kód objektu pro sestavení identický, jsou fyzicky oddělená sestavení, takže každé sestavení musí být čteno samostatně během spuštění studené lokality a udržováno odděleně v paměti.

Nové funkce pro interning tuto neúčinnost vyřeší a snižují požadavky na paměť RAM i dobu načítání. Interning umožňuje systému Windows uchovat jednu kopii každého sestavení v systému souborů a jednotlivá sestavení ve složkách bin webu budou nahrazena symbolické odkazy na jednu kopii. Pokud jednotlivá lokalita potřebuje odlišnou verzi sestavení, bude symbolický odkaz nahrazen novou verzí sestavení a bude ovlivněn pouze tento web.

Sdílení sestavení pomocí symbolických odkazů vyžaduje nový nástroj nazvaný ASPNET\_interne. exe, který umožňuje vytvořit a spravovat úložiště interně sestavených sestavení. Je k dispozici jako součást sady Visual Studio 11 Developer Preview SDK. (Bude ale fungovat v systému, který má jenom nainstalované .NET Framework 4, za předpokladu, že máte nainstalovanou nejnovější [aktualizaci](https://support.microsoft.com/kb/2468871).)

Chcete-li zajistit, aby byla všechna opravňující sestavení interně, spusťte příkaz ASPNET\_učně. exe pravidelně (například jednou týdně jako naplánovaná úloha). Typické použití je následující:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

Pokud chcete zobrazit všechny možnosti, spusťte nástroj bez argumentů.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>Použití více jader JIT kompilace pro rychlejší spuštění

**Požadavek**: .NET Framework 4,5

Pro studený start lokality je nutné číst pouze sestavení z disku, ale lokalita musí být kompilována JIT. U složitých webů může tato možnost zvýšit významné zpoždění. Nová technika pro obecné účely v .NET Framework 4,5 zkracuje tato zpoždění tím, že rozprostře kompilaci JIT napříč dostupnými jádry procesoru. V takovém případě je to co nejvíc a co nejdříve s použitím informací shromážděných během předchozích spuštění webu. Tato funkce je implementovaná metodou [System. Runtime. ProfileOptimization. StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) .

JIT – kompilace s použitím více jader je ve výchozím nastavení ve ASP.NET povolená, takže nemusíte dělat žádné výhody, abyste tuto funkci využili. Chcete-li tuto funkci zakázat, proveďte následující nastavení v souboru Web. config:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>Optimalizace shromažďování paměti pro optimalizaci paměti

**Požadavek**: .NET Framework 4,5

Když je web spuštěný, jeho použití haldy uvolňování paměti (GC) může představovat významný faktor využití paměti. Stejně jako jakýkoli systém uvolňování paměti, .NET Framework GC přináší kompromisy mezi časem procesoru (četnost a násobek kolekcí) a spotřebou paměti (navíc místo, které se používá pro nové, uvolněné nebo volné objekty). Pro předchozí verze jsme poskytli pokyny, jak nakonfigurovat GC pro dosažení správného zůstatku (například viz [Konfigurace sdíleného hostování ASP.NET 2.0/3.5](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).

Pro .NET Framework 4,5 místo více samostatných nastavení je k dispozici nastavení konfigurace definované úlohou, které umožňuje všechna dříve doporučená nastavení GC a nové ladění, které přináší dodatečný výkon pro jednotlivé lokality. pracovní sada.

Pokud chcete povolit optimalizaci paměti GC, přidejte do souboru Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config následující nastavení:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(Pokud jste obeznámeni s předchozími pokyny pro změny v souboru ASPNET. config, Všimněte si, že toto nastavení nahrazuje staré nastavení – například není nutné nastavovat gcServer, gcConcurrent atd. Není nutné odebrat staré nastavení.)

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Předběžné načtení pro webové aplikace

**Požadavek**: .NET Framework 4,5 běží v systému Windows 8

Pro několik verzí Windows zahrnovali technologii známou jako předspouštěcí [program, který](http://en.wikipedia.org/wiki/Prefetcher) snižuje náklady na čtení na disku při spuštění aplikace. Vzhledem k tomu, že studený start je pro klientské aplikace v podstatě problém, tato technologie není součástí Windows serveru, což zahrnuje jenom komponenty, které jsou pro server nezbytné. Předběžné načtení je teď k dispozici v nejnovější verzi Windows serveru, kde může optimalizovat spuštění jednotlivých webů.

Pro Windows Server není předčítat standardně povolený. Pro povolení a konfiguraci předběžného načítání pro webové hostování s vysokou hustotou spusťte na příkazovém řádku následující sadu příkazů:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

Potom pro integraci předběžného načítání s aplikacemi ASP.NET přidejte do souboru Web. config následující:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET – webové formuláře

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>Ovládací prvky dat silného typu

V ASP.NET 4,5 obsahují webové formuláře některá vylepšení pro práci s daty. Prvním vylepšením jsou ovládací prvky dat silného typu. Pro ovládací prvky webových formulářů v předchozích verzích ASP.NET se zobrazí hodnota vázaná na data pomocí *Eval* a výrazu datové vazby:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

Pro obousměrnou datovou vazbu použijete *vazbu*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

V době běhu tato volání používají reflexi ke čtení hodnoty zadaného člena a následnému zobrazení výsledku v kódu. Tento přístup usnadňuje vázání dat proti libovolným neobrazovým datům.

Nicméně výrazy vázání dat nepodporují funkce jako IntelliSense pro názvy členů, navigaci (například přejít na definici) nebo kontrolu doby kompilace těchto názvů.

Pro vyřešení tohoto problému přidává ASP.NET 4,5 možnost deklarovat datový typ dat, ke kterým je ovládací prvek vázán. Provedete to pomocí nové vlastnosti *ItemType* . Při nastavení této vlastnosti jsou k dispozici dvě nové typové proměnné v rozsahu výrazů datové vazby: *Item* a *položku BindItem*. Vzhledem k tomu, že proměnné jsou silného typu, získáte kompletní výhody prostředí pro vývoj v aplikaci Visual Studio.

Pro obousměrné výrazy vázání dat použijte proměnnou *položku BindItem* :

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

Většina ovládacích prvků v rozhraní webových formulářů ASP.NET, které podporují datovou vazbu, byla aktualizována tak, aby podporovala vlastnost *ItemType* .

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>Vazba modelu

Vazba modelu rozšiřuje datové vazby v ovládacích prvcích webových formulářů ASP.NET, aby fungovaly s přístupem k datům zaměřeným na kód. Zahrnuje koncepty z ovládacího prvku *ObjectDataSource* a z modelu vazby v ASP.NET MVC.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>Výběr dat

Chcete-li nakonfigurovat ovládací prvek data na použití vazby modelu pro výběr dat, nastavte vlastnost *SelectMethod* ovládacího prvku na název metody v kódu stránky. Ovládací prvek data volá metodu v příslušnou dobu životního cyklu stránky a automaticky vytvoří vazby vrácených dat. Není nutné explicitně volat metodu *DataBind* .

V následujícím příkladu je ovládací prvek *GridView* nakonfigurován pro použití metody s názvem *GetCategories*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

V kódu stránky vytvoříte metodu *GetCategories* . Pro jednoduchou operaci Select metoda nepotřebuje žádné parametry a měla by vracet objekt *IEnumerable* nebo *IQueryable* . Pokud je nastavena vlastnost New *ItemType* (která umožňuje výrazy vázání silného typu dat, jak je vysvětleno [dříve)](#_Toc318097386) , měly by být vráceny obecné verze těchto rozhraní – *IEnumerable&lt;T&gt;* nebo *IQueryable&lt;t&gt;* s parametrem *t* , který se shoduje s typem vlastnosti *ItemType* (například *IQueryable&lt;kategorie&gt;* ).

Následující příklad ukazuje kód pro metodu *GetCategories* . V tomto příkladu se používá model Entity Framework Code First s ukázkovou databází Northwind. Kód zajistí, že dotaz vrátí podrobnosti o souvisejících produktech pro každou kategorii pomocí metody *include* . (Tím zajistíte, že element *TemplateField* v kódu zobrazuje počet produktů v každé kategorii bez nutnosti [Vybrat n + 1](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

Při spuštění stránky volá ovládací prvek *GridView* metodu *GetCategories* automaticky a vykresluje vracená data pomocí nakonfigurovaných polí:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Vzhledem k tomu, že metoda Select vrátí objekt *IQueryable* , může ovládací prvek *GridView* před spuštěním dotazu ještě více manipulovat. Ovládací prvek *GridView* například může přidat výrazy dotazu pro řazení a stránkování do vráceného objektu *IQueryable* před jeho spuštěním, aby tyto operace prováděl základní zprostředkovatel LINQ. V takovém případě Entity Framework zajistěte, aby se tyto operace prováděly v databázi.

Následující příklad ukazuje ovládací prvek *GridView* upravený tak, aby povoloval řazení a stránkování:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

Nyní když se stránka spustí, ovládací prvek může zajistit, aby se zobrazila pouze aktuální stránka dat a byla seřazena podle vybraného sloupce:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

Chcete-li filtrovat vrácená data, je třeba přidat parametry do metody Select. Tyto parametry se naplní vazbou modelu za běhu a můžete je použít k modifikaci dotazu před vrácením dat.

Předpokládejme například, že chcete dovolit uživatelům filtrovat produkty zadáním klíčového slova do řetězce dotazu. Do metody lze přidat parametr a aktualizovat kód, aby používal hodnotu parametru:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

Tento kód obsahuje výraz *WHERE* , pokud je zadána hodnota pro *klíčové slovo* a následně vrátí výsledky dotazu.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>Zprostředkovatelé hodnot

Předchozí příklad nebyl závislý na tom, kde hodnota pro parametr *klíčového slova* přichází. Chcete-li tyto informace označit, můžete použít atribut parametru. V tomto příkladu můžete použít třídu *QueryStringAttribute* , která je v oboru názvů *System. Web. ModelBinding* :

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

Tím se dá pokyn k vytvoření vazby modelu k pokusu o vazbu hodnoty z řetězce dotazu k parametru *klíčového slova* v době běhu. (To může zahrnovat provádění převodu typu, i když v tomto případě není.) Pokud nelze zadat hodnotu a typ může mít hodnotu null, je vyvolána výjimka.

Zdroje hodnot pro tyto metody jsou označovány jako zprostředkovatelé hodnoty a atributy parametrů, které označují, který zprostředkovatel hodnot použít, se označují jako atributy zprostředkovatele hodnoty. Webové formuláře budou zahrnovat zprostředkovatele hodnot a odpovídající atributy pro všechny běžné zdroje vstupu uživatele v aplikaci webových formulářů, jako je řetězec dotazu, soubory cookie, hodnoty formulářů, ovládací prvky, stav zobrazení, stav relace a vlastnosti profilu. Můžete také napsat vlastní zprostředkovatele hodnot.

Ve výchozím nastavení se název parametru používá jako klíč k vyhledání hodnoty v kolekci zprostředkovatele hodnot. V příkladu kód bude hledat hodnotu řetězce dotazu s názvem "klíčové slovo" (například ~/default.aspx? klíčové slovo = název aplikace). Vlastní klíč můžete zadat tak, že ho předáte jako argument atributu parametru. Pokud například chcete použít hodnotu proměnné řetězce dotazu s názvem q, můžete to udělat takto:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

Pokud je tato metoda v kódu stránky, mohou uživatelé filtrovat výsledky předáním klíčového slova pomocí řetězce dotazu:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

Vazba modelu dosahuje mnoha úloh, které byste jinak museli kódovat, a to: čtení hodnoty, kontrola hodnoty null, pokus o její převedení na příslušný typ, kontrolu, zda byl převod úspěšný, a nakonec použití hodnoty v poli zadávání. Vazba modelu má za následek méně kódu a možnost znovu použít funkce v celé aplikaci.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>Filtrování podle hodnot z ovládacího prvku

Předpokládejme, že chcete tento příklad zvětšit, aby uživatel mohl zvolit hodnotu filtru z rozevíracího seznamu. Přidejte následující rozevírací seznam do značky a nakonfigurujte ho tak, aby získal data z jiné metody pomocí vlastnosti *SelectMethod* :

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

Obvykle byste také přidali element *šablonu EmptyDataTemplate* do ovládacího prvku *GridView* , aby ovládací prvek zobrazil zprávu, pokud nebyly nalezeny žádné odpovídající produkty:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

V kódu stránky přidejte novou metodu Select pro rozevírací seznam:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

Nakonec aktualizujte metodu *GetProducts* Select tak, aby v rozevíracím seznamu převzala nový parametr, který obsahuje ID vybrané kategorie:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

Nyní, když je stránka spuštěna, mohou uživatelé vybrat kategorii z rozevíracího seznamu a ovládací prvek *GridView* je automaticky znovu svázán, aby zobrazil filtrovaná data. To je možné, protože vazba modelu sleduje hodnoty parametrů pro metody Select a zjišťuje, zda se po zpětném odeslání změnila jakákoli hodnota parametru. Pokud ano, vazba modelu vynutí přidružený ovládací prvek dat, aby se znovu váže k datům.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>Výrazy vázání dat kódované HTML

Výsledek výrazů datových vazeb teď můžete kódovat ve formátu HTML. Přidejte dvojtečku (:) na konec předpony &lt;% #, která označuje výraz datové vazby:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>Nenáročná ověření

Nyní můžete nakonfigurovat vestavěné ovládací prvky pro validátory, aby používaly nenápadný JavaScript pro logiku ověřování na straně klienta. To významně snižuje množství vykreslování JavaScriptu vloženého do značek stránky a zmenšuje celkovou velikost stránky. Nenápadný jazyk JavaScript pro ovládací prvky validátoru můžete nakonfigurovat některým z těchto způsobů:

- Globálně přidáním následujícího nastavení do *&lt;appSettings&gt;* elementu v souboru Web. config: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- Globálně nastavením vlastnosti static *System. Web. UI. ValidationSettings. UnobtrusiveValidationMode* na *UnobtrusiveValidationMode. WebForms* (obvykle v metodě *Start aplikace\_* v souboru Global. asax).
- Jednotlivě pro stránku nastavením nové vlastnosti *UnobtrusiveValidationMode* třídy *Page* na *UnobtrusiveValidationMode. WebForms*.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>Aktualizace HTML5

Některá vylepšení byla provedena v ovládacích prvcích webového formuláře Server, aby bylo možné využívat nové funkce HTML5:

- Vlastnost *TextMode* ovládacího prvku *TextBox* byla aktualizována tak, aby podporovala nové typy vstupu HTML5, jako je *e-mail*, *DateTime*a tak dále.
- Ovládací prvek *nahrání* souboru teď podporuje více nahrávání souborů z prohlížečů, které podporují tuto funkci HTML5.
- Ovládací prvky validátoru nyní podporují ověřování prvků jazyka HTML5.
- Nové prvky HTML5 obsahující atributy, které reprezentují adresu URL, teď podporují runat = "Server". V důsledku toho můžete použít konvence ASP.NET v cestách URL, jako je například operátor ~ představující kořen aplikace (například &lt;video runat = "Server" src = "~/myVideo.wmv"/&gt;).
- Ovládací prvek *UpdatePanel* byl vyřešen pro podporu při odesílání vstupních polí HTML5.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 beta je teď součástí sady Visual Studio 11 Beta. ASP.NET MVC je architektura pro vývoj vysoce testovatelné a udržovatelnější webové aplikace s využitím vzoru MVC (Model-View-Controller). ASP.NET MVC 4 usnadňuje sestavování aplikací pro mobilní web a zahrnuje webové rozhraní API ASP.NET, které vám pomůže vytvořit služby HTTP, které mohou mít přístup k libovolnému zařízení. Další informace najdete v [poznámkách k verzi ASP.NET MVC 4](mvc4-release-notes.md).

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET Web Pages 2

Mezi nové funkce patří následující:

- Nové a aktualizované šablony webu.
- Přidání ověřování na straně serveru a na straně klienta pomocí pomocné rutiny *ověřování* .
- Schopnost registrovat skripty pomocí Správce prostředků.
- Povolení přihlášení z Facebooku a dalších webů pomocí OAuth a OpenID.
- Přidání map pomocí pomocníka *Maps* .
- Spouštění aplikací webových stránek vedle sebe.
- Vykreslování stránek pro mobilní zařízení.

Další informace o těchto funkcích a příklady kódu na celé stránce najdete v [hlavních funkcích webových stránek 2 beta](https://go.microsoft.com/fwlink/?LinkID=227824).

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta

V této části najdete informace o vylepšeních vývoje webu v aplikaci Visual Web Developer 11 beta a Visual Studio 2012 Release Candidate.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Sdílení projektů mezi Visual Studio 2010 a Visual Studio 2012 Release Candidate (kompatibilita projektů)

Až do sady Visual Studio 2012 Release Candidate otevřete existující projekt v novější verzi sady Visual Studio, který spustil Průvodce převodem. Tím se vynutil upgrade obsahu (assetů) projektu a řešení na nové formáty, které nebyly zpětně kompatibilní. Proto po převodu nemůžete otevřít projekt ve starší verzi sady Visual Studio.

Spousta zákazníků nám řekla, že se nejednalo o správný přístup. V aplikaci Visual Studio 11 Beta teď podporujeme sdílení projektů a řešení se sadou Visual Studio 2010 SP1. To znamená, že pokud v aplikaci Visual Studio 2012 Release Candidate otevřete projekt 2010, bude možné projekt otevřít v aplikaci Visual Studio 2010 SP1.

> [!NOTE]
> Mezi Visual Studio 2010 SP1 a Visual Studio 2012 Release Candidate nelze sdílet několik typů projektů. Mezi ně patří některé starší projekty (například projekty ASP.NET MVC 2) nebo projekty pro zvláštní účely (například projekty pro instalaci).

Při prvním otevření webového projektu sady Visual Studio 2010 SP1 v aplikaci Visual Studio 11 Beta jsou do souboru projektu přidány následující vlastnosti:

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags, UpgradeBackupLocation a OldToolsVersion se používají procesem, který upgraduje soubor projektu. Nemají žádný vliv na práci s projektem v aplikaci Visual Studio 2010.

VisualStudioVersion je nová vlastnost, kterou používá MSBuild 4,5, která označuje verzi sady Visual Studio pro aktuální projekt. Vzhledem k tomu, že tato vlastnost v MSBuild 4,0 neexistuje (verze MSBuild, kterou používá Visual Studio 2010 SP1), vložíme do souboru projektu výchozí hodnotu.

Vlastnost VSToolsPath slouží k určení správného souboru. targets pro import z cesty reprezentované nastavením MSBuildExtensionsPath32.

Existují také některé změny související s importovanými prvky. Tyto změny jsou požadovány, aby podporovaly kompatibilitu mezi oběma verzemi sady Visual Studio.

> [!NOTE]
> Pokud je projekt sdílen mezi Visual Studio 2010 SP1 a Visual Studio 11 Beta na dvou různých počítačích a pokud projekt obsahuje místní databázi ve složce App\_data, je nutné zajistit, aby byla verze SQL Server používaná databází nainstalována na obou počítačích.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>Změny konfigurace v šablonách webu ASP.NET 4,5

Následující změny byly provedeny v souboru *Web. config* pro web, který je vytvořen pomocí šablon webu v aplikaci Visual Studio 2012 Release Candidate:

- V elementu `<httpRuntime>` je nyní ve výchozím nastavení nastaven atribut `encoderType` na použití typů AntiXSS, které byly přidány do ASP.NET. Podrobnosti najdete v tématu [knihovna AntiXSS](#_Toc318097382).
- Také v prvku `<httpRuntime>` je atribut `requestValidationMode` nastaven na hodnotu "4,5". To znamená, že ve výchozím nastavení je ověřování žádostí nastaveno na použití odloženého ověřování ("opožděné"). Podrobnosti najdete v tématu [nové funkce ověřování žádostí ASP.NET](#_Toc318097379).
- Element `<modules>` `<system.webServer>` oddílu neobsahuje atribut `runAllManagedModulesForAllRequests`. (Výchozí hodnota je false.) To znamená, že pokud používáte verzi služby IIS 7, která nebyla aktualizována na verzi SP1, můžete mít problémy se směrováním v nové lokalitě. Další informace najdete v tématu [nativní podpora služby IIS 7 pro směrování ASP.NET](#Native_Support_In_IIS7_For_ASPNET_Routine).

Tyto změny neovlivní stávající aplikace. Mohou však představovat rozdíl mezi chováním mezi stávajícími weby a novými weby, které vytvoříte pro ASP.NET 4,5 pomocí nových šablon.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>Nativní podpora služby IIS 7 pro směrování ASP.NET

Nejedná se o změnu ASP.NET jako na takové, ale změny v šablonách pro nové projekty webů, které vás mohou ovlivnit, pokud pracujete se starší verzí služby IIS 7, která nemá použitu aktualizaci SP1.

V ASP.NET můžete pro aplikace přidat následující nastavení konfigurace, aby bylo možné podporovat směrování:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

Pokud má **runAllManagedModulesForAllRequests** hodnotu true, adresa url jako `http://mysite/myapp/home` přejde na ASP.NET, a to i v případě, že na adrese URL není žádná přípona *. aspx*, *. Mvc*nebo podobná přípona.

Aktualizace, kterou provedla služba IIS 7, činí nepotřebnou hodnotu nastavení **runAllManagedModulesForAllRequests** a podporuje směrování ASP.NET nativně. (Informace o této aktualizaci najdete v článku věnovaném podpora Microsoftu [je k dispozici aktualizace, která umožňuje určitým obslužným rutinám služby iis 7,0 nebo iis 7,5 zpracovávat požadavky, jejichž adresy URL nekončí tečkou](https://support.microsoft.com/kb/980368).)

Pokud váš web běží na službě IIS 7 a pokud se aktualizovala služba IIS, nemusíte nastavit **runAllManagedModulesForAllRequests** na hodnotu true. V takovém případě se nastavení na hodnotu true nedoporučuje, protože k vyžádání přináší nepotřebnou režii při zpracování. Pokud je toto nastavení pravdivé, Projděte si také všechny požadavky, včetně souborů pro *. htm*, *. jpg*a dalších statických souborů, prostřednictvím kanálu žádosti ASP.NET.

Pokud vytvoříte nový web ASP.NET 4,5 pomocí šablon, které jsou k dispozici v aplikaci Visual Studio 2012 RC, konfigurace webu nezahrnuje nastavení **runAllManagedModulesForAllRequests** . To znamená, že ve výchozím nastavení je hodnota false.

Pokud pak Web spustíte v systému Windows 7 bez nainstalované aktualizace SP1, služba IIS 7 nebude obsahovat požadovanou aktualizaci. V důsledku toho směrování nebude fungovat a zobrazí se chyby. Pokud máte problém s tím, že směrování nefunguje, můžete provést následující akce:

- Aktualizace systému Windows 7 na verzi SP1, která přidá aktualizaci do služby IIS 7.
- Nainstalujte aktualizaci popsanou v podpora Microsoftu výše uvedeném článku.
- Nastavte **runAllManagedModulesForAllRequests** na hodnotu true v souboru Web. config tohoto webu. Všimněte si, že tato akce přidá určitou režii k žádostem.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>Editor HTML

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>Inteligentní úlohy

V zobrazení Návrh komplexní vlastnosti serverových ovládacích prvků mají často přidružená dialogová okna a průvodce, což usnadňuje jejich nastavení. Například můžete použít speciální dialogové okno k přidání zdroje dat do ovládacího prvku *Repeater* nebo k přidání sloupců do ovládacího prvku *GridView* .

Tento typ nápovědu uživatelského rozhraní pro komplexní vlastnosti však není v zobrazení zdroje k dispozici. Proto Visual Studio 11 zavádí inteligentní úkoly pro zobrazení zdroje. Inteligentní úlohy jsou kontextové zkratky pro běžně používané funkce v editorech C# a Visual Basic.

Pro ovládací prvky webových formulářů ASP.NET se inteligentní úlohy zobrazují na značek serveru jako malý glyf, pokud je kurzor uvnitř elementu:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

Inteligentní panel se rozšíří po kliknutí na glyf nebo stisknutí kombinace kláves CTRL +. (tečka), stejně jako v editorech kódu. Pak zobrazí zástupce, které jsou podobné inteligentním úlohám v zobrazení Návrh.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

Například Inteligentní panel na předchozím obrázku ukazuje možnosti úkolů GridView. Pokud zvolíte možnost Upravit sloupce, zobrazí se následující dialogové okno:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

Naplnění dialogového okna nastaví stejné vlastnosti, které můžete nastavit v zobrazení Návrh. Po kliknutí na tlačítko OK se značka ovládacího prvku aktualizuje o nové nastavení:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>POČKA-podpora ARIA

Psaní přístupných webů je stále důležitější. [Standard počka-Aria Accessibility](http://www.w3.org/WAI/intro/aria) definuje, jak můžou vývojáři psát přístupné weby. Tento standard je nyní plně podporován v aplikaci Visual Studio.

Atribut *role* teď má například úplnou technologii IntelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

Standard POČKA-ARIA také zavádí atributy, které mají předponu *Aria* , což umožňuje přidat sémantiku do dokumentu HTML5. Visual Studio také plně podporuje tyto atributy *Aria* :

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>Nové fragmenty HTML5

Pro rychlejší a snazší psaní značek HTML5, Visual Studio obsahuje několik fragmentů kódu. Příkladem je fragment videa:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

Chcete-li vyvolat fragment, stiskněte klávesu TAB dvakrát, pokud je prvek vybrán v technologii IntelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

Tím se vytvoří fragment, který můžete přizpůsobit.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>Extrahovat do uživatelského ovládacího prvku

Ve velkých webových stránkách může být vhodné přesunout jednotlivé kousky do uživatelských ovládacích prvků. Tato forma refaktoringu může přispět ke zvýšení čitelnosti stránky a může zjednodušit strukturu stránky.

Chcete-li to usnadnit, při úpravách stránek webových formulářů ve zdrojovém zobrazení teď můžete vybrat text na stránce, kliknout na něj pravým tlačítkem a pak vybrat extrahovat do uživatelského ovládacího prvku:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>IntelliSense pro kód Nuggets v atributech

Visual Studio má vždy k dispozici IntelliSense pro kód na straně serveru Nuggets na libovolné stránce nebo v ovládacím prvku. Nyní Visual Studio zahrnuje technologii IntelliSense pro kód Nuggets i v atributech HTML.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

To usnadňuje vytváření výrazů pro datové vazby:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>Automatické přejmenování párové značky při přejmenování počáteční nebo uzavírací značky

Pokud přejmenujete element jazyka HTML (například změníte značku *div* na značku *záhlaví* ), odpovídající otevírací nebo uzavírací značka se změní také v reálném čase.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

To pomáhá zabránit chybě, při které zapomenete změnit uzavírací značku nebo změnit nesprávný.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>Generování obslužné rutiny událostí

Visual Studio teď obsahuje funkce ve zdrojovém zobrazení, které vám pomůžou psát obslužné rutiny událostí a vytvořit je ručně. Pokud upravujete název události ve zdrojovém zobrazení, IntelliSense zobrazí &lt;vytvořit novou událost&gt;, která vytvoří obslužnou rutinu události v kódu stránky, který má správný podpis:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

Ve výchozím nastavení bude obslužná rutina události používat ID ovládacího prvku pro název metody zpracování události:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

Výsledná obslužná rutina události bude vypadat takto (v tomto případě v C#):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>Inteligentní odsazení

Když stisknete klávesu ENTER uvnitř prázdného prvku jazyka HTML, Editor umístí kurzor na správné místo:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

Pokud stisknete klávesu ENTER v tomto umístění, koncová značka se přesune dolů a odsadí, aby odpovídala počáteční značce. Bod vložení je také odsazený:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>Automatické snížení dokončování příkazů

Seznam IntelliSense v aplikaci Visual Studio teď filtruje na základě toho, co zadáte, aby zobrazoval pouze relevantní možnosti:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense také filtruje v závislosti na velikosti písmen jednotlivých slov v seznamu IntelliSense. Pokud například zadáte "DL", zobrazí se oba typy DL a ASP: DataList:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

Díky této funkci se dá rychleji získat dokončování příkazů pro známé prvky.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript – editor

Editor jazyka JavaScript v aplikaci Visual Studio 2012 Release Candidate je zcela nový a významně zlepšuje možnosti práce s JavaScriptem v aplikaci Visual Studio.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>Osnova kódu

Oblasti osnovy se teď automaticky vytvoří pro všechny funkce, které vám umožní sbalit části souboru, které nesouvisí s vaším aktuálním fokusem.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>Spárování složených závorek

Když umístíte bod vložení na levou nebo pravou složenou závorku, Editor zvýrazní vyhovující.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>Přejít k definici

Příkaz Přejít na definici umožňuje přejít na zdroj funkce nebo proměnné.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>Podpora ECMAScript5

Editor podporuje novou syntaxi a rozhraní API v ECMAScript5, nejnovější verzi standardu, která popisuje jazyk JavaScript.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>IntelliSense modelu DOM

Technologie IntelliSense pro rozhraní API modelu DOM byla vylepšena s podporou pro řadu nových rozhraní API HTML5, včetně *querySelector*, Dom Storage, zasílání zpráv mezi dokumenty a *plátna*. Model DOM technologie IntelliSense je nyní poháněn jedním jednoduchým souborem JavaScriptu, nikoli definicí knihovny nativního typu. To usnadňuje rozšiřování a nahrazování.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>Přetížení signatur VSDOC

Podrobné komentáře technologie IntelliSense lze nyní deklarovat pro samostatné přetížení funkcí jazyka JavaScript pomocí nového prvku *&gt;signatury&lt;* , jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>Implicitní odkazy

Nyní můžete přidat soubory JavaScriptu do centrálního seznamu, který bude implicitně zahrnutý do seznamu souborů, které jsou v daném souboru JavaScriptu nebo odkazy na blok, což znamená, že získáte IntelliSense pro svůj obsah. Například můžete přidat soubory jQuery do centrálního seznamu souborů a získáte IntelliSense pro funkce jQuery v jakémkoli bloku JavaScriptu souboru, bez ohledu na to, zda jste na něj explicitně odkazováni (pomocí///&lt;odkaz/&gt;) nebo ne.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS Editor

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>Automatické snížení dokončování příkazů

Seznam IntelliSense pro CSS teď filtruje na základě vlastností a hodnot šablon stylů CSS, které jsou podporované vybraným schématem.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

Technologie IntelliSense také podporuje hledání v případě nadpisu:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>Hierarchické odsazení

Editor šablon stylů CSS používá k zobrazení hierarchických pravidel odsazení, což vám poskytne přehled o logickém uspořádání kaskádových pravidel. V následujícím příkladu je #list selektor kaskádový podřízený seznamu a je proto odsazen.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

Následující příklad ukazuje složitější dědičnost:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

Odsazení pravidla závisí na jeho nadřazeném pravidle. Hierarchické odsazení je ve výchozím nastavení povoleno, ale můžete ho zakázat v dialogovém okně Možnosti (nástroje, možnosti z panelu nabídek):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>Podpora šablon stylů CSS hackatony

Analýza stovek souborů CSS reálného světa ukazuje, že šablony stylů CSS hackatony jsou velmi běžné a teď Visual Studio podporuje nejčastěji používané. Tato podpora zahrnuje technologii IntelliSense a ověřování hackatony (\*) a podtržítka (\_) vlastnosti:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

K dispozici jsou také typické hackatonyy selektorů, aby se zachovalo hierarchické odsazení i při jejich použití. Typickým napadením selektoru, který se používá pro cílení na Internet Explorer 7, je předřadit selektor pomocí *\*: First-Child + HTML*. Pomocí tohoto pravidla se zachová hierarchická odsazení:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>Schémata specifická pro dodavatele (– MOZ-,-WebKit)

CSS3 zavádí mnoho vlastností, které byly implementovány různými prohlížeči v různých časech. Toto dřív vynutilo vývojářům kód pro konkrétní prohlížeče pomocí syntaxe specifické pro dodavatele. Tyto vlastnosti specifické pro prohlížeč jsou nyní součástí technologie IntelliSense.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>Podpora komentářů a zrušení komentářů

Nyní můžete komentovat a odkomentovat pravidla šablony stylů CSS pomocí stejných klávesových zkratek, které používáte v editoru kódu (CTRL + K, C pro komentáře a CTRL + K, můžete odkomentovat).

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Výběr barvy

V předchozích verzích sady Visual Studio se technologie IntelliSense pro atributy, které se týkají barev, skládají z rozevíracího seznamu pojmenovaných hodnot barvy. Tento seznam byl nahrazen úplným nástrojem pro výběr barev.

Když zadáte hodnotu barvy, výběr barvy se zobrazí automaticky a zobrazí seznam dříve použitých barev následovaný výchozí paletou barev. Barvu můžete vybrat pomocí myši nebo klávesnice.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

Seznam lze rozšířit na úplný výběr barev. Výběr umožňuje řídit alfa kanál automatickým převodem jakékoli barvy na RGBA při přesunutí posuvníku neprůhlednosti:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>Fragmenty

Fragmenty kódu v editoru šablon stylů CSS usnadňují a urychlují vytváření stylů pro různé prohlížeče. Mnoho vlastností CSS3, které vyžadují nastavení specifické pro prohlížeč, je teď zahrnuté do fragmentů kódu.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

Fragmenty kódu CSS podporují pokročilé scénáře (například dotazy CSS3 na média) zadáním symbolu (@), který zobrazuje seznam IntelliSense.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

Když vyberete @media hodnota a stisknete klávesu TAB, Editor CSS vloží následující fragment kódu:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

Stejně jako u fragmentů kódu můžete vytvořit vlastní fragmenty stylů CSS.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>Vlastní oblasti

Oblasti pojmenovaného kódu, které jsou již k dispozici v editoru kódu, jsou nyní k dispozici pro úpravy šablon stylů CSS. To vám umožní snadno seskupit související bloky stylu.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

Při sbalení oblasti se zobrazí název oblasti:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Inspektor stránek

Page Inspector je nástroj, který vykresluje webovou stránku (HTML, webové formuláře, ASP.NET MVC nebo webové stránky) v integrovaném vývojovém prostředí (IDE) sady Visual Studio a umožňuje prozkoumávat zdrojový kód i výsledný výstup. Pro stránky ASP.NET vám umožňuje určit, který kód na straně serveru vytvořil kód HTML, který se vykreslí do prohlížeče.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

Další informace o nástroji Page Inspector najdete v následujících kurzech:

- Používání funkce Page Inspector v [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)
- Použití funkce Page Inspector ve [webových formulářích ASP.NET](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)

<a id="_Toc318097425"></a>
### <a name="publishing"></a>Publikování

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>Profily publikování

V aplikaci Visual Studio 2010 nejsou informace o publikování pro projekty webových aplikací uloženy ve správě verzí a nejsou určeny pro sdílení s jinými uživateli. V aplikaci Visual Studio 2012 Release Candidate byl změněn formát profilu publikování. Byl proveden týmový artefakt a je nyní snadné ho využít ze sestavení založených na MSBuildu. Informace o konfiguraci sestavení jsou v dialogovém okně publikovat, aby bylo možné snadno přepínat konfigurace sestavení před publikováním.

Profily publikování se ukládají do složky PublishProfiles. Umístění složky závisí na používaném programovacím jazyku:

- C#: Properties\PublishProfiles
- Visual Basic: moje Project\PublishProfiles

Každý profil je soubor MSBuild. Během publikování se tento soubor importuje do souboru MSBuild projektu. Pokud chcete v aplikaci Visual Studio 2010 provádět změny v procesu publikování nebo balíčku, je nutné přidat vlastní nastavení do souboru s názvem **ProjectName**. WPP. targets. Tato možnost je stále podporovaná, ale teď můžete přidat vlastní nastavení do samotného profilu publikování. Tímto způsobem se vlastní nastavení použijí jenom pro tento profil.

Můžete teď také využít profily publikování z MSBuild. K tomu použijte následující příkaz při sestavování projektu:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

Hodnota Project. csproj je cesta projektu a název profilu je název profilu, který chcete publikovat. Případně místo předání názvu profilu pro vlastnost *publishprofile* můžete předat úplnou cestu k publikačnímu profilu.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>Předkompilace a sloučení ASP.NET

Pro projekty webových aplikací sada Visual Studio 2012 Release Candidate přidá na stránce Vlastnosti balíčku/publikování webu možnost, která umožňuje předkompilovat a sloučit obsah webu při publikování nebo zabalení projektu. Chcete-li zobrazit tyto možnosti, klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, zvolte možnost vlastnosti a pak zvolte stránku balíček/publikování webové vlastnosti. Následující ilustrace znázorňuje předkompilování této aplikace před možností publikování.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

Pokud je vybrána tato možnost, sada Visual Studio předkompiluje aplikaci vždy, když webovou aplikaci publikujete nebo zabalíte. Chcete-li určit, jak má být lokalita předkompilována nebo jak jsou sestavení sloučena, klikněte na tlačítko Upřesnit a nakonfigurujte tyto možnosti.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

Výchozí webový server pro testování webových projektů v aplikaci Visual Studio je nyní IIS Express. Vývojový server sady Visual Studio je stále možností pro místní webový server během vývoje, ale IIS Express je teď doporučeným serverem. Zkušenost s používáním IIS Express v aplikaci Visual Studio 11 Beta je velmi podobná použití v aplikaci Visual Studio 2010 SP1.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>Právní omezení

Toto je předběžný dokument a může být podstatně měněn před konečným komerčním vydáním softwaru popsaného v tomto dokumentu.

Informace obsažené v tomto dokumentu představují aktuální pohled společnosti Microsoft Corporation na problémy, které jsou popsány k datu publikování. Vzhledem k tomu, že Microsoft musí reagovat na měnící se podmínky na trhu, neměl by být interpretován jako závazek společnosti Microsoft a společnost Microsoft nemůže zaručit přesnost všech informací, které jsou uvedeny po datu publikování.

Tento dokument White Paper slouží pouze k informativním účelům. SPOLEČNOST MICROSOFT NEPOSKYTUJE ŽÁDNÉ ZÁRUKY, AŤ UŽ VÝSLOVNĚ UVEDENÉ, PŘEDPOKLÁDANÉ NEBO STATUTÁRNÍ, JAKO INFORMACE V TOMTO DOKUMENTU.

Dodržování všech platných zákonů o autorských právech je zodpovědností uživatele. Bez omezení práv v rámci autorského práva nesmí být žádná část tohoto dokumentu reprodukována, ukládána do systému pro načítání nebo převedena v jakémkoli tvaru nebo jakýmkoli prostředkem (elektronickými, mechanicky, fotokopírováním, záznamem nebo jiným) nebo pro jakékoli účely. bez výslovného písemného svolení společnosti Microsoft Corporation.

Společnost Microsoft může mít patenty, patentové aplikace, ochranné známky, autorská práva nebo jiná práva duševního vlastnictví, která zahrnují předmět v tomto dokumentu. S výjimkou výslovně uvedených v písemné licenční smlouvě od společnosti Microsoft vám poskytnutí tohoto dokumentu neposkytuje žádnou licenci na tyto patenty, ochranné známky, autorská práva ani jiné duševní vlastnictví.

Pokud není uvedeno jinak, jsou ukázkové společnosti, organizace, produkty, názvy domén, e-mailové adresy, loga, osoby, místa a události uvedené v ukázkách smyšlené a bez jakýchkoli souvislostí se skutečnou společností, organizací, produktem, názvem domény, e-mailem. adresa, logo, osoba, místo nebo událost jsou zamýšlené nebo by se měly odvodit.

© 2012 Microsoft Corporation. Všechna práva vyhrazena.

Microsoft a Windows jsou buď registrované ochranné známky, nebo ochranné známky společnosti Microsoft Corporation v USA a dalších zemích.

Názvy skutečných společností a produktů uvedených v tomto dokumentu můžou být ochranné známky jejich příslušných vlastníků.
