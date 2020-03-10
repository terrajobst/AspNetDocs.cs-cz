---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: Přehled projektu Katana | Microsoft Docs
author: howarddierking
description: ASP.NET Framework bylo delší než deset let a platforma vypnula vývoj webů a služeb dlouhé. Jako web oC...
ms.author: riande
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 1f28db822930cdfd2ebf4cf9bb27d173f4aa4201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617234"
---
# <a name="an-overview-of-project-katana"></a>Přehled projektu Katana

podle [Howard Dierking](https://github.com/howarddierking)

> ASP.NET Framework bylo delší než deset let a platforma vypnula vývoj webů a služeb dlouhé. Jak se vyvinuly vývojové strategie pro webové aplikace, rozhraní se může vyvíjet v kroku s technologiemi, jako je ASP.NET MVC a ASP.NET Web API. Vzhledem k tomu, že vývoj webových aplikací převezme svůj další krok do světa cloud computingu, [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) Project poskytuje základní sadu komponent pro ASP.NET aplikace. díky tomu můžou být flexibilní, přenosné, odlehčené a poskytují lepší výkon – a navíc Cloud [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) Cloud optimalizuje vaše aplikace ASP.NET.

## <a name="why-katana--why-now"></a>Proč teď Katana – proč?

 Bez ohledu na to, jestli jedna z nich je diskuze o vývojářském rozhraní nebo produktu pro koncové uživatele, je důležité pochopit základní motivaci pro vytváření produktu – a část, která obsahuje informace o tom, kdo vytvořil produkt. ASP.NET byl původně vytvořen se dvěma zákazníky.   
  
**První skupina zákazníků byla klasických vývojářů ASP.** V tuto chvíli byla ASP jednou z primárních technologií pro vytváření dynamických webových stránek a aplikací založených na datech pomocí kódu interweaving a skriptu na straně serveru. Běhový modul ASP zadal skript na straně serveru se sadou objektů, které abstraktní základní aspekty základního protokolu HTTP a webového serveru poskytly přístup k dalším službám, jako je třeba relace a Správa stavu aplikace, mezipaměť atd. V případě výkonných klasických aplikací ASP se stala výzvou ke správě, protože se rozrostla o velikost a složitost. To bylo z velké části kvůli nedostatku struktury nalezené v skriptovacích prostředích, které jsou spojeny s duplikováním kódu, který je výsledkem prokládání kódu a značek. Aby nedošlo k velkému množství funkcí klasického ASP při řešení některých problémů, ASP.NET využili výhod kódu organizace, který poskytuje objektově orientované jazyky .NET Framework a zároveň zachovává serverový model programování na straně serveru. pro které klasické vývojáře v prostředí ASP byly zvyklí.

**Druhá skupina cílových zákazníků pro ASP.NET byla vývojářům podnikových aplikací pro Windows.** Na rozdíl od klasických vývojářů ASP, kteří byli zvyklí psát kód HTML a kód pro generování více značek HTML, vývojáři WinForms (jako jsou VB6 vývojáři) zvyklí na dobu návrhu, která obsahovala plátno a bohatou sadu uživatelů. ovládací prvky rozhraní. První verze ASP.NET (označovaná také jako "webové formuláře") poskytuje podobné prostředí v době návrhu spolu s modelem události na straně serveru pro součásti uživatelského rozhraní a sadu funkcí infrastruktury (například ViewState) pro vytvoření bezproblémového prostředí pro vývojáře. mezi programováním klienta a na straně serveru. Webové formuláře efektivně standardně skryly bezstavový charakter webu v rámci modelu stavové události, který byl obeznámený s nawinformsm vývojářů.

### <a name="challenges-raised-by-the-historical-model"></a>Výzvy vyvolané historickým modelem

**Netto výsledek byl vyspělý modul runtime a vývojář pro vývojáře s funkcemi.** Nicméně s touto funkcí – bohatě dorazila několik důležitých výzev. Nejprve rozhraní bylo **monolitické**, s logicky různorodými jednotkami funkcí, které jsou úzce spojeny ve stejném sestavení System. Web. dll (například základní objekty http s rozhraním Web Forms Framework). Druhý ASP.NET byl součástí většího .NET Framework, což znamená, že **Doba mezi verzemi byla v řádu let.** Díky tomu je obtížné ASP.NET udržet krok se všemi změnami provedenými při rychlém vývoji vývoje webu. Nakonec došlo k párování samotného souboru System. Web. dll s několika různými způsoby pro konkrétní možnost hostování webu: Internetová informační služba (IIS).

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>Postup vývoje: ASP.NET MVC a ASP.NET Web API

A hodně změn se při vývoji webu stalo! Webové aplikace byly stále vyvíjeny jako řady malých a zaměřených komponent, nikoli jako velká rozhraní. Počet komponent a četnost, s jakou byly vydány, se zvýšily při vyšší míře. Bylo jasné, že Průběžné škálování na webu by vyžadovalo menší, oddělené a více zaměřené místo většího a více funkcí, takže **tým ASP.NET provedl několik kroků vývoje, které umožní ASP.NET jako rodinu webových komponent, a ne jenom jedno rozhraní**.

Jedna z dřívějších změn byla nárůstem oblíbenosti modelu návrhu MVC (Model-View-Controller) s ohledem na vývojové architektury webu, jako jsou Ruby na železnici. Tento styl sestavování webových aplikací poskytuje vývojářům lepší kontrolu nad jeho značkou, přičemž stále zachovává oddělení značek a obchodní logiky, což bylo jedno z počátečních prodejních bodů pro ASP.NET. Aby bylo možné splnit požadavky na tento styl vývoje webových aplikací, společnost Microsoft pořídila možnost umístit si ji do budoucna ještě lepší díky **vývoji ASP.NET MVC mimo IP síť** (a nezahrnuje ji do .NET Framework). ASP.NET MVC byla vydána jako nezávislé stažení. Díky tomu má technický tým flexibilitu při poskytování aktualizací mnohem častěji, než bylo dřív možné.

Další hlavní směna při vývoji webových aplikací byla posunuta z dynamických vygenerovaných webových stránek do statického počátečního kódu s dynamickými oddíly generovanými na straně klienta, které komunikují **s back-end webovými rozhraními API prostřednictvím požadavků AJAX**. Tento architektonický posun pomáhá propeli vývoje webových rozhraní API a vývoj rozhraní ASP.NET webového rozhraní API. Stejně jako v případě ASP.NET MVC poskytuje vydání webového rozhraní API ASP.NET další příležitost k dalšímu vývojování ASP.NET jako více modulárních architektur. Technický tým využil výhod příležitostí a **sestavení ASP.NET webového rozhraní API tak, aby neobsahoval žádné závislosti na žádném z typů základních rozhraní nalezených v System. Web. dll**. To je povolené dvě věci: Nejdřív to znamenalo, že webové rozhraní API ASP.NET se může vyvíjet zcela samostatně (a může pokračovat v iteraci, protože se doručí přes NuGet). Za druhé, protože neexistovaly žádné externí závislosti k souboru System. Web. dll, a proto žádné závislosti na službu IIS, ASP.NET webové rozhraní API, zahrnovaly možnost spuštění ve vlastním hostiteli (například Konzolová aplikace, služba systému Windows atd.).

### <a name="the-future-a-nimble-framework"></a>Budoucnost: architektura čipernější

Odpojuje komponenty architektury od sebe a pak je vydává v NuGet, architektury by nyní mohly **iterovat nezávisle a**rychleji. Navíc se výkon a flexibilita schopnosti samoobslužného hostování webového rozhraní API ukázala jako pro vývojáře, kteří pro své služby chtěli **malý a odlehčený hostitel** . Ukázalo se, že je to atraktivní, ve skutečnosti i to, že se tato schopnost také chtěla, a tato možnost se provedla v tom, že každé rozhraní běželo ve vlastním hostitelském procesu na vlastní základní adrese a je potřeba ho spravovat (spuštěno, zastaveno atd.) nezávisle na sobě. Moderní webová aplikace obecně podporuje statické obsluhy souborů, dynamické generování stránek, webové rozhraní API a další nedávno v reálném čase nebo nabízená oznámení. Očekává se, že každá z těchto služeb by měla být spuštěná a spravovaná nezávisle, ale nejedná se o reálnou.

Co bylo potřeba, byla jediná hostující abstrakce, která by vývojářům umožnila sestavovat aplikaci z nejrůznějších různých komponent a platforem a pak tuto aplikaci spouštět na podpůrném hostiteli.

## <a name="the-open-web-interface-for-net-owin"></a>Otevřené webové rozhraní pro .NET (OWIN)

 Nechte inspirovat díky výhodám, které dosáhlo [racku](http://rack.github.io/) v komunitě Ruby, několik členů komunity .NET vystavili abstrakci mezi webovými servery a komponentami rozhraní. Dva cíle návrhu pro abstrakci OWIN byly jednoduché a to trvalou nejnižší možné závislosti na jiných typech rozhraní. Tyto dva cíle vám pomůžou zajistit:

- Nové komponenty mohou být snáze vyvíjeny a spotřebovány.
- Aplikace by se daly snadněji rozportovat mezi hostiteli a potenciálně celými platformami a operačními systémy.

Výsledná abstrakce se skládá ze dvou základních prvků. První je slovník prostředí. Tato struktura dat zodpovídá za ukládání všech stavů potřebných ke zpracování požadavků a odpovědí HTTP a také všech relevantních stavů serveru. Slovník prostředí je definován následujícím způsobem:

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

Webový server kompatibilní s OWIN zodpovídá za načtení slovníku prostředí s daty, jako jsou například datové proudy a kolekce hlaviček pro požadavek HTTP a odpověď. Je pak zodpovědností za komponenty aplikace nebo rozhraní k naplnění nebo aktualizaci slovníku o další hodnoty a zápis do datového proudu zprávy odpovědi.

Kromě určení typu pro slovník prostředí definuje specifikace OWIN seznam párů hodnot klíčů základního slovníku. Například v následující tabulce jsou uvedeny požadované klíče slovníku pro požadavek HTTP:

| Název klíče | Popis hodnoty |
| --- | --- |
| `"owin.RequestBody"` | Datový proud s textem žádosti, pokud existuje. Stream. null se dá použít jako zástupný symbol, pokud není k dispozici žádný text žádosti. Podívejte se na [Text žádosti](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics). |
| `"owin.RequestHeaders"` | `IDictionary<string, string[]>` hlaviček požadavku. Viz [záhlaví](http://owin.org/html/owin.html#3-3-headers). |
| `"owin.RequestMethod"` | `string` obsahující metodu požadavku HTTP žádosti (např. `"GET"`, `"POST"`). |
| `"owin.RequestPath"` | `string` obsahující cestu požadavku. Cesta musí být relativní ke kořenu delegáta aplikace; viz [cesty](http://owin.org/html/owin.html#5-3-paths). |
| `"owin.RequestPathBase"` | `string` obsahující část cesty požadavku odpovídající "kořenu" delegáta aplikace; viz [cesty](http://owin.org/html/owin.html#5-3-paths). |
| `"owin.RequestProtocol"` | `string` obsahující název a verzi protokolu (např. `"HTTP/1.0"` nebo `"HTTP/1.1"`). |
| `"owin.RequestQueryString"` | `string` obsahující komponentu řetězce dotazu identifikátoru URI požadavku HTTP bez úvodní "?" (např. `"foo=bar&baz=quux"`). Hodnota může být prázdný řetězec. |
| `"owin.RequestScheme"` | `string` obsahující schéma identifikátoru URI použité pro požadavek (např. `"http"`, `"https"`); viz [schéma identifikátoru URI](http://owin.org/html/owin.html#5-1-uri-scheme). |

Druhým prvkem klíče OWIN je delegát aplikace. Toto je signatura funkce, která slouží jako primární rozhraní mezi všemi komponentami v aplikaci OWIN. Definice pro delegáta aplikace je následující:

`Func<IDictionary<string, object>, Task>;`

Delegát aplikace je pak jednoduše implementací typu delegáta Func, kde funkce přijímá slovník prostředí jako vstup a vrací úlohu. Tento návrh má pro vývojáře několik aspektů:

- Aby bylo možné zapsat součásti OWIN, je vyžadován velmi malý počet závislostí typu. Tím se významně zvyšuje přístupnost OWIN vývojářům.
- Asynchronní návrh umožňuje, aby abstrakce byla efektivní s zpracováním výpočetních prostředků, zejména v dalších náročných vstupně-výstupních operacích.
- Vzhledem k tomu, že delegát aplikace je atomická jednotka provádění a protože je slovník prostředí převeden jako parametr delegáta, mohou být součásti OWIN snadno zřetězeny k vytváření složitých kanálů zpracování HTTP.

Z perspektivy implementace je OWIN specifikace ([http://owin.org/html/owin.html](http://owin.org/html/owin.html)). Jeho cílem je, že se nejedná o další webové rozhraní, ale spíše o specifikaci, jak webové architektury a webové servery pracují.

Pokud jste prošetřili [Owin](http://owin.org/) nebo [Katana](https://github.com/aspnet/AspNetKatana/wiki), můžete si také všimnout [balíčku NuGet Owin](http://nuget.org/packages/Owin) a Owin. dll. Tato knihovna obsahuje jedno rozhraní [IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs), které formalizes a kodifikovaně sekvenci spouštění popsanou v [části 4](http://owin.org/html/owin.html#4-application-startup) specifikace Owin. I když se nevyžaduje pro sestavování serverů OWIN, rozhraní [IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs) poskytuje konkrétní referenční bod a používá ho komponenty projektu Katana.

## <a name="project-katana"></a>Katana projektu

Vzhledem k tomu, že specifikace [Owin](http://owin.org/html/owin.html) i *Knihovna Owin. dll* jsou vlastněné komunitou a komunitním open source, představuje projekt [Katana](https://github.com/aspnet/AspNetKatana/wiki) sadu komponent Owin, které při současném použití Open Source jsou sestavené a vydané společností Microsoft. Mezi tyto komponenty patří jak komponenty infrastruktury, jako jsou hostitelé a servery, i funkční komponenty, jako jsou například komponenty pro ověřování a vazby do architektury, jako jsou například [signalizační](../../../signalr/index.md) a [ASP.NET webové rozhraní API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md). Projekt má následující tři cíle na nejvyšší úrovni: 

- **Přenosné** – součásti by měly být schopné snadno nahradit nové komponenty, jakmile budou k dispozici. To zahrnuje všechny typy komponent, od rozhraní po server a hostitele. Důvodem tohoto cíle je, že architektury třetích stran se můžou bez problémů spouštět na serverech Microsoftu, zatímco Microsoft Framework může běžet na serverech a hostitelích třetích stran.
- **Modulární/flexibilní**– na rozdíl od mnoha platforem, které obsahují nesčetných funkcí, které jsou ve výchozím nastavení zapnuté, Katana komponenty projektu by měly být malé a zaměřené na řízení vývojářům aplikací, které určují komponenty, které se mají použít ve své aplikaci.
- **Odlehčená/výkonná/škálovatelná** – zrušením tradičního pojmu rozhraní do sady malých, zaměřených komponent, které jsou explicitně přidané vývojářem aplikace, může výsledná aplikace Katana spotřebovat méně výpočetních prostředků, a výsledkem je zpracování větší zátěže než u jiných typů serverů a platforem. Protože požadavky aplikace vyžadují více funkcí z základní infrastruktury, je možné je přidat do kanálu OWIN, ale to by mělo být explicitní rozhodnutí v rámci vývojáře aplikace. Nahrazování komponent na nižší úrovni navíc znamená, že jakmile budou k dispozici, nové vysoce výkonné servery je možné bezproblémově zavádět, aby se zlepšil výkon aplikací OWIN bez narušení těchto aplikací.

## <a name="getting-started-with-katana-components"></a>Začínáme s komponentami Katana

Při prvním zavedení je jedním aspektem architektury [Node. js](http://nodejs.org/) , která ihned nastala pozornost pro lidi, jako je jednoduchost toho, jak může vytvořit webový server a spustit ho. Pokud byly cíle Katana na základě [Node. js](http://nodejs.org/), může je jedna z nich sumarizovat vyslovením, že Katana přináší mnoho výhod [Node. js](http://nodejs.org/) (a rozhraní jako IT), aniž by vývojář vyvolal vše, co ví o vývoji ASP.NET webových aplikací. Aby tento příkaz mohl držet hodnotu true, musí být Začínáme s projektem Katana stejně jednoduché pro [Node. js](http://nodejs.org/).

## <a name="creating-hello-world"></a>Vytváření Hello World!

Jedním z významných rozdílů mezi jazykem JavaScript a vývojem .NET je přítomnost (nebo absence) kompilátoru. V takovém případě je výchozím bodem jednoduchého serveru Katana projekt sady Visual Studio. Můžeme však začít s největším počtem typů projektů: prázdná webová aplikace v ASP.NET.

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

V dalším kroku nainstalujeme do projektu balíček [Microsoft. Owin. Host. SystemWeb](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) NuGet. Tento balíček poskytuje server OWIN, který běží v kanálu žádosti ASP.NET. Dá se najít v [galerii NuGet](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) a dá se nainstalovat pomocí dialogového okna Správce balíčků sady Visual Studio nebo konzoly Správce balíčků pomocí tohoto příkazu:

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

Při instalaci balíčku `Microsoft.Owin.Host.SystemWeb` se jako závislosti nainstaluje několik dalších balíčků. Jedna z těchto závislostí je `Microsoft.Owin`, knihovny, která poskytuje několik pomocných typů a metod pro vývoj aplikací OWIN. Tyto typy můžeme použít k rychlému zápisu následujícího serveru Hello World.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

Tento velmi jednoduchý webový server se teď dá spustit pomocí příkazu **F5** sady Visual Studio a obsahuje úplnou podporu pro ladění.

## <a name="switching-hosts"></a>Přepínání hostitelů

Ve výchozím nastavení se předchozí příklad "Hello World" spustí v kanálu žádosti ASP.NET, který používá System. Web v kontextu služby IIS. To může sama o sobě přidat obrovské hodnoty, protože nám to umožňuje těžit z flexibility a možnosti sestavování kanálu OWIN s možnostmi správy a celkovou dobou zralosti služby IIS. Mohou však nastat případy, kdy nejsou vyžadovány výhody poskytované službou IIS a že je potřeba pro menší, jednodušší hostitele. Co je potřeba, abyste mohli spustit náš jednoduchý webový server mimo IIS a System. Web?

K ilustraci cíle přenositelnosti je potřeba, aby se přechod z hostitele webového serveru do příkazového řádku zavedl jednoduše přidáním závislostí serveru a hostitele do výstupní složky projektu a pak od hostitele. V tomto příkladu budeme hostovat náš webový server na hostiteli Katana s názvem `OwinHost.exe` a použijeme Server Katana HttpListener. Podobně jako ostatní komponenty Katana budou získány z NuGet pomocí následujícího příkazu:

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

Z příkazového řádku můžeme přejít do kořenové složky projektu a jednoduše spustit `OwinHost.exe` (která byla nainstalována ve složce Tools příslušného balíčku NuGet). Ve výchozím nastavení je `OwinHost.exe` nakonfigurovaný tak, aby hledal server založený na HttpListener, a proto není potřeba žádná další konfigurace. Navigace ve webovém prohlížeči `http://localhost:5000/` zobrazuje aplikaci, která je teď spuštěná prostřednictvím konzoly.

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Architektura Katana

 Architektura komponenty Katana rozděluje aplikaci do čtyř logických vrstev, jak je znázorněno níže: *hostitel, server, middleware* a *aplikace*. Architektura součásti je určena takovým způsobem, že implementace těchto vrstev lze snadno nahradit, v mnoha případech bez nutnosti překompilování aplikace.   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>Hostitel

 Hostitel zodpovídá za:

- Správa základního procesu.
- Orchestrace pracovního postupu, který vede k výběru serveru a vytváření OWIN kanálu, přes který se budou zpracovávat požadavky.

  V současnosti existují 3 možnosti primárního hostování pro aplikace založené na Katana:  
  
**IIS/ASP. NET**: použití standardních typů HttpModule a HttpHandler, kanály Owin lze spustit ve službě IIS jako součást toku požadavků ASP.NET. Podpora hostování ASP.NET je povolená tak, že se do projektu webové aplikace nainstaluje balíček NuGet Microsoft. AspNet. Host. SystemWeb. Vzhledem k tomu, že služba IIS funguje jako hostitel i server, rozlišení serveru nebo hostitele OWIN se v tomto balíčku NuGet nerovná, což znamená, že při použití hostitele SystemWeb nemůže vývojář použít alternativní implementaci serveru.  
  
**Vlastní hostitel**: sada komponent Katana poskytuje vývojářům možnost hostovat aplikace ve vlastním vlastním procesu, ať už se jedná o konzolovou aplikaci, službu systému Windows atd. Tato funkce vypadá podobně jako funkce samoobslužného hostitele poskytované webovým rozhraním API. Následující příklad ukazuje vlastního hostitele kódu webového rozhraní API:  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Nastavení samostatného hostitele pro aplikaci Katana je podobné:

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Jedním z významných rozdílů mezi webovými rozhraními API a Katana pro samostatné hostitele je, že v příkladu Katana pro samoobslužné hostitele chybí konfigurační kód webového rozhraní API. Aby bylo možné povolit přenositelnost i možnosti složení, Katana odděluje kód, který spouští server, z kódu, který konfiguruje kanál zpracování požadavků. Kód, který konfiguruje webové rozhraní API, je pak obsažen ve spuštění třídy, které je dále zadáno jako parametr typu ve webové aplikaci. Start.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

Spouštěcí třída bude podrobněji popsána dále v článku. Nicméně kód potřebný ke spuštění procesu samostatného hostitele Katana vypadá podobně jako kód, který můžete v samoobslužných hostitelských aplikacích pro ASP.NET webového rozhraní API použít ještě dnes.

**OwinHost. exe**: i když některé budou chtít napsat vlastní proces pro spouštění webových aplikací Katana, spousta by chtěla jednoduše spustit předem sestavený spustitelný soubor, který může spustit server a spustit jeho aplikaci. V tomto scénáři sada součástí Katana zahrnuje `OwinHost.exe`. Při spuštění z kořenového adresáře projektu spustí tento spustitelný soubor Server (ve výchozím nastavení používá server HttpListener) a použije konvence k vyhledání a spuštění třídy pro spuštění uživatele. Pro podrobnější řízení poskytuje spustitelný soubor řadu dalších parametrů příkazového řádku.

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>Server

 I když je hostitel zodpovědný za spuštění a údržbu procesu, ve kterém je aplikace spuštěná, zodpovědnost serveru je otevřít síťový soket, naslouchat žádostem a posílat je prostřednictvím kanálu součástí OWIN zadaných uživatelem (jako vy Možná už jste si všimli, že tento kanál je zadaný ve třídě pro spuštění vývojáře aplikace. V současné době projekt Katana zahrnuje dvě implementace serveru: 

- **Microsoft. Owin. Host. SystemWeb**: jak je uvedeno výše, služba IIS v součinnosti s kanálem ASP.NET funguje jako hostitel i server. Proto při volbě této možnosti hostování spravuje služba IIS aspekty na úrovni hostitele, jako je aktivace procesu a naslouchá požadavkům HTTP. U webových aplikací ASP.NET odešle požadavky do kanálu ASP.NET. Hostitel Katana SystemWeb registruje http HttpModules a HttpHandler k zachycení požadavků v průběhu toku přes kanál HTTP a jejich odeslání prostřednictvím kanálu OWIN zadaného uživatelem.
- **Microsoft. Owin. Host. HttpListener**: jak je uvedeno, tento Katana Server používá třídu HttpListener .NET Framework k otevření soketu a odeslání požadavků do kanálu Owin zadaného vývojářem. Aktuálně se jedná o výchozí výběr serveru pro rozhraní API Katana pro samoobslužné hostování i pro OwinHost. exe.

## <a name="middlewareframework"></a>Middleware/architektura

 Jak už bylo zmíněno, pokud server přijme požadavek od klienta, zodpovídá za jeho předání prostřednictvím kanálu OWIN komponent, které jsou určeny spouštěcím kódem vývojáře. Tyto komponenty kanálu se označují jako middleware.  
 Na velmi základní úrovni musí komponenta middleware OWIN jednoduše implementovat delegáta aplikace OWIN, aby se dala volat.

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

Pro zjednodušení vývoje a složení součástí middleware však Katana podporuje několik konvence a pomocné typy pro komponenty middlewaru. Nejběžnější je `OwinMiddleware` třídy. Vlastní komponenta middlewaru sestavená pomocí této třídy by vypadala podobně jako v následujícím příkladu: 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 Tato třída je odvozena z `OwinMiddleware`, implementuje konstruktor, který přijímá instanci dalšího middleware v kanálu jako jeden z jeho argumentů a poté předává základnímu konstruktoru. Další argumenty používané pro konfiguraci middleware jsou také deklarovány jako parametry konstruktoru za následujícím parametrem middlewaru.   
  
V době běhu je middleware spouštěna prostřednictvím přepsané `Invoke` metody. Tato metoda přijímá jeden argument typu `OwinContext`. Tento kontextový objekt je k dispozici v balíčku `Microsoft.Owin` NuGet popsaném dříve a poskytuje přístup se silným typem ke slovníku požadavků, odpovědí a prostředí a také několik dalších pomocných typů.   
  
Třídu middlewaru lze snadno přidat do kanálu OWIN ve spouštěcím kódu aplikace následujícím způsobem:   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

Protože infrastruktura Katana jednoduše vytvoří kanál OWINch součástí middlewaru a protože komponenty jednoduše potřebují podporovat delegáta aplikace, aby se účastnili kanálu, můžou být komponenty middlewaru v rozsahu od jednoduchých protokolovacích nástrojů až po celá rozhraní, jako je ASP.NET, webové rozhraní API nebo [signál](../../../signalr/index.md). Například přidání webového rozhraní API ASP.NET do předchozího kanálu OWIN vyžaduje přidání následujícího spouštěcího kódu:

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Infrastruktura Katana vytvoří kanál komponent middlewaru na základě pořadí, ve kterém byly přidány do objektu IAppBuilder v metodě konfigurace. V našem příkladu může LoggerMiddleware zpracovávat všechny požadavky, které procházejí kanálem, bez ohledu na to, jak jsou tyto požadavky nakonec zpracovávány. To umožňuje výkonnou situaci, kdy součást middlewaru (například součást pro ověřování) může zpracovávat požadavky na kanál, který obsahuje více komponent a platforem (např. webové rozhraní API ASP.NET, Signaler a statický souborový server).
 
## <a name="applications"></a>Aplikace

Jak je znázorněno v předchozích příkladech, OWIN a projekt Katana by se nemusely představit jako nový aplikační model aplikace, ale spíše jako abstrakce pro odkládání aplikačních modelů a platforem aplikace z infrastruktury serveru a hostingu. Například při sestavování webových aplikací rozhraní API bude rozhraní vývojář i nadále používat rozhraní Web API ASP.NET, bez ohledu na to, jestli aplikace běží v kanálu OWIN pomocí komponent z projektu Katana. Jedno místo, kde bude OWIN kód viditelný pro vývojáře aplikace, bude spouštěcí kód aplikace, kde vývojář vytvoří kanál OWIN. Ve spouštěcím kódu Vývojář zaregistruje řadu UseXxch příkazů, obecně jeden pro každou komponentu middlewaru, která bude zpracovávat příchozí požadavky. Toto prostředí bude mít stejný účinek jako registrace modulů HTTP v aktuálním systému System. Web World. Na konci kanálu se obvykle zaregistruje middlewarový middleware většího rozhraní, například webové rozhraní API ASP.NET nebo [Signal](../../../signalr/index.md) . Křížové komponenty middlewaru, jako jsou například pro ověřování nebo ukládání do mezipaměti, jsou obecně registrovány na začátku kanálu, takže budou zpracovávat požadavky na všechny architektury a součásti registrované později v kanálu. Oddělení součástí middlewaru od sebe od sebe od sebe a od základních komponent infrastruktury umožňuje vyvíjet komponenty v různých rychlostí a přitom zajistit, aby celkový systém zůstával stabilní.

## <a name="components--nuget-packages"></a>Komponenty – balíčky NuGet

Podobně jako u mnoha současných knihoven a architektur se komponenty projektu Katana doručují jako sada balíčků NuGet. V nadcházející verzi 2,0 vypadá graf závislosti balíčků Katana následujícím způsobem. (Pro větší zobrazení klikněte na obrázek.)

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Skoro každý balíček v projektu Katana závisí přímo nebo nepřímo na balíčku Owin. Můžete si uvědomit, že se jedná o balíček obsahující rozhraní IAppBuilder, které poskytuje konkrétní implementaci spouštěcí sekvence aplikace popsané v části 4 specifikace OWIN. Mnohé z těchto balíčků jsou navíc závislé na Microsoft. Owin, který poskytuje sadu pomocných typů pro práci s požadavky HTTP a odpověďmi. Zbytek balíčku může být klasifikován jako hostitelský balíček infrastruktury (servery nebo hostitelé) nebo middleware. Balíčky a závislosti, které jsou externí pro projekt Katana, se zobrazují oranžová.

Infrastruktura hostování pro katana 2,0 zahrnuje servery založené na SystemWeb a HttpListener, balíček OwinHost pro spouštění aplikací OWIN pomocí OwinHost. exe a balíček Microsoft. Owin. hosting pro aplikace OWIN pro samoobslužné hostování v vlastní hostitel (například Konzolová aplikace, služba systému Windows atd.)

Pro katana 2,0 jsou komponenty middlewaru primárně zaměřené na poskytování různých způsobů ověřování. K dispozici je jedna další součást middlewaru pro diagnostiku, která umožňuje podporu pro úvodní a chybovou stránku. Jak OWIN roste abstrakci hostování v de facto, ekosystém součástí middlewaru, které vyvinula společnost Microsoft i třetí strany, bude také růst v čísle.

## <a name="conclusion"></a>Závěr

 Od svého začátku se cíl projektu Katana nevytvořil, a proto si vývojáři vynutí, aby se ještě seznámili s jiným webovým rozhraním. Místo toho bylo cílem vytvořit abstrakci, která vývojářům webových aplikací .NET nabídne více možností výběru, než bylo dříve možné. Rozbalením logických vrstev typického zásobníku webových aplikací do sady nahraditelných komponent Katana projekt umožňuje komponentám v celém zásobníku, aby se zlepšily v jakékoliv míře, což dává smysl pro tyto komponenty. Díky vytvoření všech komponent kolem jednoduché abstrakce OWIN Katana umožňuje architekturám a aplikacím postaveným na nich, aby byly přenosné napříč různými servery a hostiteli. Tím, že vývojář předloží kontrolu nad zásobníkem, Katana zajistí, že vývojář provede maximální volbu toho, jak by měl být zjednodušený a jak by měl svůj webový zásobník obsahovat funkce.  

## <a name="for-more-information-about-katana"></a>Další informace o Katana

- Projekt Katana na GitHubu: [https://github.com/aspnet/AspNetKatana/](https://github.com/aspnet/AspNetKatana/).
- Video: [Katana projekt – OWIN pro ASP.NET –](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)Howard Dierking.

## <a name="acknowledgements"></a>Poděkování

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/): (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) Rick je hlavní programovací zapisovač pro zaměření Microsoftu na Azure a MVC.
- [Scott Hanselman](http://www.hanselman.com/blog/): (Twitter [@shanselman](https://twitter.com/shanselman) )
- [Jan Galloway](https://weblogs.asp.net/jgalloway/default.aspx): (Twitter [@jongalloway](https://twitter.com/jongalloway) )
