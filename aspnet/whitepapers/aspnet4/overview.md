---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 a Visual Studio 2010 – přehled vývoje webů | Microsoft Docs
author: rick-anderson
description: Tento dokument obsahuje přehled mnoha nových funkcí pro ASP.NET, které jsou součástí the.NET Framework 4 a Visual Studio 2010.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: ecde48f6bd88ee5f569bfeb8b70c26a50bc869c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576873"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 a Visual Studio 2010 – přehled vývoje webu

> Tento dokument obsahuje přehled mnoha nových funkcí pro ASP.NET, které jsou součástí the.NET Framework 4 a Visual Studio 2010.
> 
> [Stáhnout tento dokument White Paper](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

**Obsah**

**[Základní služby](#0.2__Toc253429238 "_Toc253429238")**  
[Refaktoring souboru Web. config](#0.2__Toc253429239 "_Toc253429239")  
[Rozšiřitelné ukládání výstupu do mezipaměti](#0.2__Toc253429240 "_Toc253429240")  
[Automatické spouštění webových aplikací](#0.2__Toc253429241 "_Toc253429241")  
[Trvalé přesměrování stránky](#0.2__Toc253429242 "_Toc253429242")  
[Zmenší se stav relace.](#0.2__Toc253429243 "_Toc253429243")  
[Rozšíření rozsahu povolených adres URL](#0.2__Toc253429244 "_Toc253429244")  
[Rozšiřitelné ověřování žádostí](#0.2__Toc253429245 "_Toc253429245")  
[Ukládání objektů do mezipaměti a rozšiřitelnost objektů do mezipaměti](#0.2__Toc253429246 "_Toc253429246")  
[Extensible HTML, adresa URL a kódování hlaviček protokolu HTTP](#0.2__Toc253429247 "_Toc253429247")  
[Sledování výkonu pro jednotlivé aplikace v jednom pracovním procesu](#0.2__Toc253429248 "_Toc253429248")  
[Cílení na více platforem](#0.2__Toc253429249 "_Toc253429249")

**[Jazyka](#0.2__Toc253429250 "_Toc253429250")**  
[jQuery zahrnutý do webových formulářů a MVC](#0.2__Toc253429251 "_Toc253429251")  
[Podpora Content Delivery Network](#0.2__Toc253429252 "_Toc253429252")  
[Explicitní skripty ScriptManager](#0.2__Toc253429253 "_Toc253429253")

**[Webové formuláře](#0.2__Toc253429256 "_Toc253429256")**  
[Nastavení meta značek pomocí vlastností Page. MetaKeywords a Page. MetaDescription](#0.2__Toc253429257 "_Toc253429257")  
[Povolení stavu zobrazení pro jednotlivé ovládací prvky](#0.2__Toc253429258 "_Toc253429258")  
[Změny možností prohlížeče](#0.2__Toc253429259 "_Toc253429259")  
[Směrování v ASP.NET 4](#0.2__Toc253429260 "_Toc253429260")  
[Nastavení ID klientů](#0.2__Toc253429261 "_Toc253429261")  
[Trvalé vybírání výběru řádků v datových ovládacích prvcích](#0.2__Toc253429262 "_Toc253429262")  
[Ovládací prvek grafu ASP.NET](#0.2__Toc253429263 "_Toc253429263")  
[Filtrování dat pomocí ovládacího prvku třídou QueryExtender](#0.2__Toc253429264 "_Toc253429264")  
[Výrazy kódovaného kódu ve formátu HTML](#0.2__Toc253429265 "_Toc253429265")  
[Změny šablony projektu](#0.2__Toc253429266 "_Toc253429266")  
[Vylepšení šablon stylů CSS](#0.2__Toc253429267 "_Toc253429267")  
[Skrytí prvků div kolem skrytých polí](#0.2__Toc253429268 "_Toc253429268")  
[Vykreslení vnější tabulky pro ovládací prvky s šablonou](#0.2__Toc253429269 "_Toc253429269")  
[Vylepšení ovládacího prvku ListView](#0.2__Toc253429270 "_Toc253429270")  
[Vylepšení ovládacího prvku CheckBoxList a RadioButtonList](#0.2__Toc253429271 "_Toc253429271")  
[Vylepšení ovládacích prvků nabídky](#0.2__Toc253429272 "_Toc253429272")  
[Průvodce a ovládací prvky ovládacím CreateUserWizard 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[Podpora oblastí](#0.2__Toc253429275 "_Toc253429275")  
[Podpora ověřování atributů poznámky k datům](#0.2__Toc253429276 "_Toc253429276")  
[Pomocník s šablonami](#0.2__Toc253429277 "_Toc253429277")

**[Dynamická data](#0.2__Toc253429278 "_Toc253429278")**  
[Povolení dynamických dat pro existující projekty](#0.2__Toc253429279 "_Toc253429279")  
[Deklarativní syntaxe ovládacího prvku ovládacího prvku DynamicDataManager](#0.2__Toc253429280 "_Toc253429280")  
[Šablony entit](#0.2__Toc253429281 "_Toc253429281")  
[Nové šablony polí pro adresy URL a e-mailové adresy](#0.2__Toc253429282 "_Toc253429282")  
[Vytváření odkazů pomocí ovládacího prvku ovládací DynamicHyperLink](#0.2__Toc253429283 "_Toc253429283")  
[Podpora dědičnosti v datovém modelu](#0.2__Toc253429284 "_Toc253429284")  
[Podpora relací M:n (jenom Entity Framework)](#0.2__Toc253429285 "_Toc253429285")  
[Nové atributy pro řízení zobrazení a podpory výčtů](#0.2__Toc253429286 "_Toc253429286")  
[Rozšířená podpora pro filtry](#0.2__Toc253429287 "_Toc253429287")

**[Vylepšení vývoje webu sady Visual Studio 2010](#0.2__Toc253429288 "_Toc253429288")**  
[Vylepšená kompatibilita šablon stylů CSS](#0.2__Toc253429289 "_Toc253429289")  
[Fragmenty kódu HTML a JavaScriptu](#0.2__Toc253429290 "_Toc253429290")  
[Vylepšení JavaScript IntelliSense](#0.2__Toc253429291 "_Toc253429291")

**[Nasazení webové aplikace pomocí sady Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**  
[Balíčky webu](#0.2__Toc253429293 "_Toc253429293")  
[Transformace Web. config](#0.2__Toc253429294 "_Toc253429294")  
[Nasazení databáze](#0.2__Toc253429295 "_Toc253429295")  
[Publikování jedním kliknutím pro webové aplikace](#0.2__Toc253429296 "_Toc253429296")  
[Prostředky](#0.2__Toc253429297 "_Toc253429297")

**[Právní omezení](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>Základní služby

ASP.NET 4 zavádí řadu funkcí, které zlepšují základní služby ASP.NET, jako je ukládání výstupu do mezipaměti a ukládání stavu relací.

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>Refaktoring souboru Web. config

`Web.config` soubor obsahující konfiguraci webové aplikace výrazně vzrostl v posledních několika verzích .NET Framework, protože byly přidány nové funkce, jako je například AJAX, směrování a integrace se službou IIS 7. Díky tomu bylo obtížnější nakonfigurovat nebo spustit nové webové aplikace bez nástroje, jako je například Visual Studio. V. rozhraní .NET Framework 4 byly hlavní prvky konfigurace přesunuty do souboru `machine.config` a aplikace nyní tato nastavení zdědí. To umožňuje, aby soubor `Web.config` v aplikacích ASP.NET 4 buď prázdný, nebo obsahoval pouze následující řádky, které určují verzi rozhraní .NET Framework, na kterou je aplikace cílena:

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>Rozšiřitelné ukládání výstupu do mezipaměti

Vzhledem k tomu, že čas vydání ASP.NET 1,0, ukládání výstupu do mezipaměti umožňuje vývojářům ukládat generovaný výstup stránek, ovládacích prvků a odpovědí HTTP do paměti. Na následujících webových požadavcích může ASP.NET poskytovat obsah rychleji díky načtení vygenerovaného výstupu z paměti místo opětovného generování výstupu od začátku. Tento přístup má ale omezení – vygenerovaný obsah vždycky musí být uložený v paměti a na serverech, u kterých dochází k velkým objemům provozu, může paměť spotřebovaná výstupním ukládáním do mezipaměti soutěžit s nároky na paměť z jiných částí webové aplikace.

ASP.NET 4 přidá bod rozšiřitelnosti do ukládání výstupu do mezipaměti, který umožňuje konfigurovat jednoho nebo více vlastních poskytovatelů výstupní mezipaměti. Poskytovatelé výstupní mezipaměti můžou použít jakýkoliv mechanismus úložiště k uchování obsahu HTML. Díky tomu je možné vytvářet vlastní poskytovatele výstupní mezipaměti pro různé mechanismy trvalosti, které můžou zahrnovat místní nebo vzdálené disky, cloudové úložiště a moduly distribuovaných mezipamětí.

Vlastní poskytovatele výstupní mezipaměti vytvoříte jako třídu, která je odvozena od nového typu *System. Web. Caching. OutputCacheProvider* . Potom můžete nakonfigurovat zprostředkovatele v souboru `Web.config` pomocí nového dílčího oddílu *providers* elementu *OutputCache* , jak je znázorněno v následujícím příkladu:

[!code-xml[Main](overview/samples/sample2.xml)]

Ve výchozím nastavení v ASP.NET 4 všechny odpovědi HTTP, vykreslené stránky a ovládací prvky používají výstupní mezipaměť v paměti, jak je znázorněno v předchozím příkladu, kde je atribut *defaultProvider* nastaven na hodnotu AspNetInternalProvider. Výchozí zprostředkovatele výstupní mezipaměti, který se používá pro webovou aplikaci, můžete změnit zadáním jiného názvu poskytovatele pro hodnotu *defaultProvider*.

Kromě toho můžete vybrat různé poskytovatele výstupní mezipaměti pro jednotlivé ovládací prvky a jednotlivé požadavky. Nejjednodušší způsob, jak zvolit jiného poskytovatele výstupní mezipaměti pro různé webové uživatelské ovládací prvky, je provést deklarativní postup pomocí nového atributu *ProviderName* v direktivě ovládacího prvku, jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample3.aspx)]

Zadání jiného zprostředkovatele výstupní mezipaměti pro požadavek HTTP vyžaduje trochu více práce. Namísto deklarativního určení poskytovatele přepíšete novou metodu *GetOuputCacheProviderName* v souboru `Global.asax` pro programové zadání poskytovatele, kterého chcete použít pro konkrétní požadavek. Následující příklad ukazuje, jak to provést.

[!code-csharp[Main](overview/samples/sample4.cs)]

S přidáním rozšiřitelnosti poskytovatele výstupní mezipaměti do ASP.NET 4 teď můžete ve svých webech pokračovat efektivněji a více inteligentními strategiemi pro ukládání výstupu do mezipaměti. Například je možné ukládat do mezipaměti stránky "Top 10" stránek v paměti, při ukládání stránek do mezipaměti, které získávají nižší provoz na disku. Alternativně můžete ukládat do mezipaměti všechny různé kombinace pro vykreslenou stránku, ale použít distribuovanou mezipaměť, aby byla spotřeba paměti převedena z front-end webových serverů.

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>Automatické spouštění webových aplikací

Některé webové aplikace potřebují před obsluhou první žádosti načíst velké objemy dat nebo provést náročné zpracování inicializace. V dřívějších verzích ASP.NET byly pro tyto situace nutné navrhnout vlastní přístupy do "probuzení" ASP.NET aplikace a poté spustit inicializační kód během *\_metoda Load* v souboru `Global.asax`.

Nová funkce škálovatelnosti s názvem *Automatický start* , která přímo řeší tento scénář, je k dispozici, když ASP.NET 4 běží ve službě IIS 7,5 v systému Windows Server 2008 R2. Funkce automatického spuštění poskytuje řízený přístup pro spuštění fondu aplikací, inicializaci aplikace ASP.NET a následné přijetí požadavků HTTP.

> [!NOTE] 
> 
> Modul pro zahřívání aplikace služby IIS pro IIS 7,5
> 
> Tým služby IIS vydal první beta verzi testovacího modulu aplikace pro IIS 7,5. Tím se aplikace zahřívá ještě před tím, než je popsáno výše. Místo psaní vlastního kódu zadáte adresy URL prostředků, které se mají provést, než webová aplikace přijme požadavky ze sítě. K tomuto zahřívání dojde během spouštění služby IIS (Pokud jste nakonfigurovali fond aplikací IIS jako *AlwaysRunning*) a při recyklování pracovního procesu služby IIS. Během recyklování stará pracovní proces služby IIS nadále zpracovává požadavky, dokud se nově vytvořený pracovní proces plně neuvolní, takže aplikace nebudou mít žádné přerušení ani jiné problémy z důvodu neprvotních mezipamětí. Všimněte si, že tento modul funguje s libovolnou verzí ASP.NET, počínaje verzí 2,0.
> 
> Další informace najdete v tématu [zahřívání aplikace](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) na webu IIS.NET. Návod, který ukazuje, jak používat funkci pro zahřívání, najdete v tématu [Začínáme s modulem pro zahřívání aplikace IIS 7,5](https://www.iis.net/learn/manage) na webu IIS.NET.

Aby bylo možné používat funkci automatického spuštění, Správce služby IIS nastaví fond aplikací ve službě IIS 7,5 tak, aby se automaticky spouštěl pomocí následující konfigurace `applicationHost.config` souboru:

[!code-xml[Main](overview/samples/sample5.xml)]

Vzhledem k tomu, že jeden fond aplikací může obsahovat více aplikací, určíte jednotlivé aplikace, které mají být automaticky spuštěny, pomocí následující konfigurace v souboru `applicationHost.config`:

[!code-xml[Main](overview/samples/sample6.xml)]

Pokud je server služby IIS 7,5 studeny nebo pokud dojde k recyklování jednotlivých fondů aplikací, služba IIS 7,5 používá informace v souboru `applicationHost.config` k určení, které webové aplikace je třeba automaticky spustit. Pro každou aplikaci, která je označena pro automatické spuštění, pošle služba IIS 7.5 požadavek na ASP.NET 4 ke spuštění aplikace ve stavu, během kterého aplikace dočasně nepřijímá požadavky HTTP. Pokud je v tomto stavu, ASP.NET vytvoří instanci typu definovaného atributem *serviceAutoStartProvider* (jak je znázorněno v předchozím příkladu) a volá do svého veřejného vstupního bodu.

Můžete vytvořit spravovaný typ automatického spuštění s nezbytným vstupním bodem implementací rozhraní *neimplementuje IProcessHostPreloadClient* , jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](overview/samples/sample7.cs)]

Po spuštění inicializačního kódu v metodě *přednačtení* a návratovou metodou bude aplikace ASP.NET připravená na zpracování požadavků.

Díky přidání automatického startu ke službě IIS 0,5 a ASP.NET 4 teď máte jasně definovaný přístup k náročné inicializaci aplikace před zpracováním prvního požadavku HTTP. Můžete například použít novou funkci automatického spuštění k inicializaci aplikace a pak signalizovat Nástroj pro vyrovnávání zatížení, že aplikace byla inicializována a připravena přijímat přenosy HTTP.

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>Trvalé přesměrování stránky

Mezi webovými aplikacemi se běžně přesouvá stránky a další obsah v průběhu času, což může vést k akumulaci zastaralých odkazů ve vyhledávačích. V ASP.NET vývojáři tradičně zpracovali požadavky na staré adresy URL pomocí metody *Response. Redirect* pro přesměrování požadavku na novou adresu URL. Metoda *přesměrování* však vystaví odpověď nalezeno http 302 (dočasné přesměrování), což vede k tomu, že se uživatelé pokusí o přístup ke starým adresám URL.

ASP.NET 4 přidává novou pomocnou metodu *RedirectPermanent* , která usnadňuje vystavení HTTP 301 přesunutí trvalých odpovědí, jako v následujícím příkladu:

[!code-csharp[Main](overview/samples/sample8.cs)]

Vyhledávací moduly a další uživatelské agenti, kteří rozpoznávají trvalé přesměrování, uloží novou adresu URL, která je přidružená k obsahu, což eliminuje nepotřebnou dobu odezvy, kterou prohlížeč provede pro dočasné přesměrování.

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>Zmenší se stav relace.

ASP.NET poskytuje dvě výchozí možnosti pro ukládání stavu relace napříč webovou farmou: Zprostředkovatel stavu relace, který vyvolá nezpracovaný Server stavu relace, a poskytovatele stavu relace, který ukládá data do databáze Microsoft SQL Server. Vzhledem k tomu, že obě možnosti zahrnují ukládání informací o stavu mimo pracovní proces webové aplikace, je nutné před odesláním do vzdáleného úložiště serializovat stav relace. V závislosti na tom, kolik informací vývojář ukládá do stavu relace, může být velikost serializovaných dat poměrně velká.

ASP.NET 4 zavádí novou možnost komprese pro oba typy zprostředkovatelů stavu relací mimo proces. Pokud je možnost konfigurace *compressionEnabled* zobrazená v následujícím příkladu nastavená na *hodnotu true*, ASP.NET se komprimuje (a dekomprimuje) serializovaného stavu relace pomocí třídy .NET Framework *System. IO. Compression. GZipStream* .

[!code-xml[Main](overview/samples/sample9.xml)]

Díky jednoduchému přidání nového atributu do souboru `Web.config` mohou aplikace s náhradními cykly procesoru na webových serverech realizovat výrazné snížení velikosti serializovaných dat o stavu relace.

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>Rozšíření rozsahu povolených adres URL

ASP.NET 4 zavádí nové možnosti rozšíření velikosti adres URL aplikací. Předchozí verze ASP.NET omezené cesty URL délky na 260 znaků na základě limitu souborů NTFS. V ASP.NET 4 máte možnost tento limit zvýšit (nebo snížit) pro vaše aplikace pomocí dvou nových atributů konfigurace prostředí *httpRuntime* . Následující příklad ukazuje tyto nové atributy.

[!code-xml[Main](overview/samples/sample10.xml)]

Pro povolení delších nebo kratších cest (část adresy URL, která nezahrnuje protokol, název serveru a řetězec dotazu), upravte atribut *[nakonfigurovanou parametru MaxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* . Pro povolení delších nebo kratších řetězců dotazu upravte hodnotu atributu *[nakonfigurovanou parametru MaxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* .

ASP.NET 4 také umožňuje nakonfigurovat znaky používané kontrolou znaků adresy URL. Když ASP.NET najde neplatný znak v části cesty adresy URL, požadavek odmítne a vydá chybu HTTP 400. V předchozích verzích ASP.NET byly kontroly znaků adresy URL omezeny na pevně danou sadu znaků. V ASP.NET 4 můžete přizpůsobit sadu platných znaků pomocí nového atributu *RequestPathInvalidCharacters* konfiguračního prvku *httpRuntime* , jak je znázorněno v následujícím příkladu:

[!code-xml[Main](overview/samples/sample11.xml)]

Ve výchozím nastavení definuje atribut *RequestPathInvalidCharacters* osm znaků jako neplatných. (V řetězci, který je přiřazen k *RequestPathInvalidCharacters* ve výchozím nastavení jsou zakódovány znaky menší než (&lt;), větší než (&gt;) a ampersand (&amp;), protože soubor `Web.config` je soubor XML.) V případě potřeby můžete upravit sadu neplatných znaků.

> [!NOTE]
> Poznámka ASP.NET 4: vždy odmítne cesty URL obsahující znaky v rozsahu ASCII hodnoty 0x00 na 0x1F, protože to jsou neplatné znaky adresy URL definované v dokumentu RFC 2396 sdružení IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)). V případě verzí Windows serveru, na kterých běží IIS 6 nebo vyšší, ovladač zařízení protokolu HTTP. sys automaticky odmítá adresy URL těmito znaky.

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>Rozšiřitelné ověřování žádostí

Ověření žádosti ASP.NET vyhledá příchozí data požadavku HTTP pro řetězce, které se běžně používají při útocích skriptování mezi weby (XSS). Pokud jsou nalezeny potenciálně řetězce XSS, žádosti o ověření označí podezřelý řetězec a vrátí chybu. Integrované ověřování žádostí vrátí chybu pouze v případě, že najde nejběžnější řetězce používané v útocích XSS. Předchozí pokusy o, aby ověřování XSS bylo více agresivní, vedlo k příliš mnoha falešně pozitivním hodnotám. Zákazníci ale můžou chtít, aby ověřování žádostí bylo výkonnější nebo naopak mohlo chtít záměrně uvolnit kontroly XSS pro konkrétní stránky nebo konkrétní typy požadavků.

V ASP.NET 4 byla funkce ověření žádosti rozšiřitelná, takže můžete používat vlastní logiku pro ověření požadavků. Chcete-li provést prodloužení žádosti o ověření, vytvořte třídu, která je odvozena z nového typu *System. Web. util. RequestValidator* , a nakonfigurujete aplikaci (v oddílu *httpRuntime* souboru `Web.config`) tak, aby používala vlastní typ. Následující příklad ukazuje, jak nakonfigurovat vlastní třídu pro ověření požadavků:

[!code-xml[Main](overview/samples/sample12.xml)]

Nový atribut *RequestValidationType* vyžaduje standardní .NET Framework řetězec identifikátoru typu, který určuje třídu, která poskytuje vlastní ověření žádosti. Pro každý požadavek ASP.NET vyvolá vlastní typ pro zpracování jednotlivých příchozích dat požadavků HTTP. Příchozí adresa URL, všechny hlavičky protokolu HTTP (soubory cookie a vlastní hlavičky) a tělo entity jsou k dispozici pro kontrolu vlastní třídou ověření žádosti, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](overview/samples/sample13.cs)]

V případech, kdy nechcete kontrolovat příchozí data HTTP, může třída ověření žádosti přejít zpět, aby bylo možné ASP.NET výchozí požadavek spustit pouhým voláním *Base. IsValidRequestString.*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>Ukládání objektů do mezipaměti a rozšiřitelnost objektů do mezipaměti

Od první vydané verze ASP.NET zahrnulo výkonnou mezipaměť objektů v paměti (*System. Web. Caching. cache*). Implementace mezipaměti je tak oblíbená, že se použila v jiných než webových aplikacích. Je však nevhodné, aby aplikace model Windows Forms nebo WPF zahrnovaly odkaz na `System.Web.dll` pouze k tomu, aby bylo možné použít mezipaměť objektů ASP.NET.

Aby bylo ukládání do mezipaměti k dispozici pro všechny aplikace, .NET Framework 4 zavádí nové sestavení, nový obor názvů, některé základní typy a konkrétní implementaci ukládání do mezipaměti. Nové sestavení `System.Runtime.Caching.dll` obsahuje nové rozhraní API pro ukládání do mezipaměti v oboru názvů *System. Runtime. Caching* . Obor názvů obsahuje dvě základní sady tříd:

- Abstraktní typy, které poskytují základ pro vytvoření jakéhokoli typu vlastní implementace mezipaměti.
- Konkrétní implementace mezipaměti objektů v paměti (třída *System. Runtime. Caching. MemoryCache* ).

Nová třída *MemoryCache* je úzce modelována v mezipaměti ASP.NET a sdílí většinu logiky modulu interní mezipaměti s ASP.NET. I když rozhraní API pro veřejné ukládání do mezipaměti v *System. Runtime. Caching* bylo aktualizované tak, aby podporovalo vývoj vlastních mezipamětí, pokud jste použili objekt ASP.NET *cache* , najdete v nových rozhraních API známé koncepty.

Podrobná diskuse nové třídy *MemoryCache* a podpůrná základní rozhraní API by vyžadovala celý dokument. Následující příklad vám ale poskytne představu o tom, jak nové rozhraní API mezipaměti funguje. Příklad byl napsán pro model Windows Forms aplikaci bez jakékoli závislosti na `System.Web.dll`.

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>Extensible HTML, adresa URL a kódování hlaviček protokolu HTTP

V ASP.NET 4 můžete vytvořit vlastní rutiny kódování pro následující běžné úlohy kódování textu:

- Kódování HTML.
- Kódování adresy URL.
- Kódování atributu HTML.
- Kódování odchozích hlaviček protokolu HTTP.

Vlastní kodér můžete vytvořit odvozením z nového typu *System. Web. util. HttpEncoder* a následnou konfigurací ASP.NET pro použití vlastního typu v oddílu *httpRuntime* souboru `Web.config`, jak je znázorněno v následujícím příkladu:

[!code-xml[Main](overview/samples/sample15.xml)]

Po nakonfigurování vlastního kodéru ASP.NET automaticky volá vlastní implementaci kódování vždy, když jsou volány veřejné metody kódování tříd *System. Web. HttpUtility* nebo *System. Web. HttpServerUtility* . To umožňuje, aby jedna část týmu vývoje webu vytvořila vlastní kodér, který implementuje agresivní kódování znaků, zatímco zbytek týmu vývoje webu nadále používá rozhraní API pro kódování ASP.NET. Centrální konfigurací vlastního kodéru v prvku *httpRuntime* je zaručeno, že všechna volání kódování textu z rozhraní API pro kódování ASP.NET jsou směrována prostřednictvím vlastního kodéru.

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>Sledování výkonu pro jednotlivé aplikace v jednom pracovním procesu

Aby bylo možné zvýšit počet webů, které lze hostovat na jednom serveru, mnoho hostitelů v jednom pracovním procesu spouští více aplikací ASP.NET. Pokud ale více aplikací používá jeden sdílený pracovní proces, je obtížné správcům serverů identifikovat jednotlivé aplikace, u kterých dochází k problémům.

ASP.NET 4 využívá novou funkci pro monitorování prostředků, kterou zavádí modul CLR. Chcete-li povolit tuto funkci, můžete do konfiguračního souboru `aspnet.config` přidat následující fragment konfigurace XML.

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> Všimněte si, že `aspnet.config` soubor je v adresáři, ve kterém je nainstalovaná .NET Framework. Nejedná se o soubor `Web.config`.

Pokud je povolená funkce *appDomainResourceMonitoring* , jsou v kategorii výkonu "aplikace ASP.NET" k dispozici dva nové čítače výkonu: *% času spravovaného procesoru* a *použitá spravovaná paměť*. Oba tyto čítače výkonu využívají novou funkci správy prostředků aplikace CLR v doméně ke sledování odhadovaného času procesoru a využití spravované paměti u jednotlivých aplikací ASP.NET. V důsledku toho se v ASP.NET 4 teď pro správce zobrazí podrobnější zobrazení spotřeby prostředků jednotlivých aplikací spuštěných v jednom pracovním procesu.

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>Cílení na více verzí

Můžete vytvořit aplikaci, která cílí na konkrétní verzi .NET Framework. V ASP.NET 4 umožňuje nový atribut v elementu *compilation* `Web.config` souboru cílit na .NET Framework 4 a novější. Pokud explicitně cílíte na .NET Framework 4 a pokud zahrnete volitelné prvky do souboru `Web.config`, například do záznamů pro *System. CodeDom*, tyto prvky musí být správné pro .NET Framework 4. (Pokud explicitně necílíte na .NET Framework 4, cílové rozhraní se odvozuje z nedostatku položky v souboru `Web.config`.)

Následující příklad ukazuje použití atributu *targetFramework* v elementu *compilation* souboru `Web.config`.

[!code-xml[Main](overview/samples/sample17.xml)]

Všimněte si následujícího informací o cílení na konkrétní verzi .NET Framework:

- Ve fondu aplikací .NET Framework 4 předpokládá systém sestavení ASP.NET .NET Framework 4 jako cíl, pokud soubor `Web.config` neobsahuje atribut *targetFramework* nebo pokud chybí soubor `Web.config`. (Může být nutné provést změny v kódování vaší aplikace, aby byly spouštěny pod .NET Framework 4.)
- Pokud zahrnete atribut *targetFramework* a pokud je v souboru `Web.config` definován prvek *System. CodeDom* , musí tento soubor obsahovat správné položky .NET Framework 4.
- Použijete-li příkaz *aspnet\_Compiler* k předkompilování aplikace (například v prostředí sestavení), je nutné použít správnou verzi příkazu *ASPNET\_kompilátoru* pro cílovou architekturu. Použijte kompilátor dodaný s .NET Framework 2,0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) ke kompilaci pro .NET Framework 3,5 a starší verze. Použijte kompilátor, který je dodáván s .NET Framework 4 ke kompilaci aplikací vytvořených pomocí této architektury nebo použití novějších verzí.
- V době běhu kompilátor používá nejnovější sestavení rozhraní, která jsou nainstalována v počítači (a proto v mezipaměti GAC). Pokud je aktualizace provedena později v rozhraní (například je nainstalována hypotetická verze 4,1), budete moci používat funkce v novější verzi rozhraní i v případě, že atribut *targetFramework* cílí na nižší verzi (například 4,0). (Nicméně v době návrhu v aplikaci Visual Studio 2010 nebo při použití příkazu *aspnet\_Compiler* , způsobí použití novějších funkcí rozhraní chyby kompilátoru).

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>jQuery zahrnutý do webových formulářů a MVC

Šablony sady Visual Studio pro webové formuláře i MVC obsahují Open Source knihovnu jQuery. Při vytváření nového webu nebo projektu se vytvoří složka skripty obsahující následující 3 soubory:

- jQuery 1.4.1. js – unminified verze knihovny jQuery, která je čitelná pro člověka.
- jQuery 14,1. min. js – verze minifikovaného knihovny jQuery.
- jQuery 1.4.1-vsdoc. js – soubor dokumentace technologie IntelliSense pro knihovnu jQuery.

Při vývoji aplikace zahrňte unminified verzi jQuery. Zahrňte minifikovaného verzi jQuery pro produkční aplikace.

Například následující stránka webového formuláře ukazuje, jak lze pomocí jQuery změnit barvu pozadí ovládacích prvků TextBox ASP.NET na žlutou, pokud mají fokus.

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>Podpora Content Delivery Network

Microsoft Ajax Content Delivery Network (CDN) umožňuje snadno přidávat do svých webových aplikací skripty ASP.NET AJAX a jQuery. Knihovnu jQuery můžete například začít jednoduše přidáním značky `<script>` na stránku, která odkazuje na Ajax.microsoft.com takto:

[!code-html[Main](overview/samples/sample19.html)]

Díky využití služby Microsoft Ajax CDN můžete významně zlepšit výkon aplikací AJAX. Obsah Microsoft Ajax CDN je uložený v mezipaměti na serverech umístěných po celém světě. Kromě toho Microsoft Ajax CDN umožňuje prohlížečům znovu použít soubory JavaScriptu v mezipaměti pro weby, které se nacházejí v různých doménách.

Microsoft Ajax Content Delivery Network podporuje protokol SSL (HTTPS) pro případ, že potřebujete poskytovat webovou stránku pomocí SSL (Secure Sockets Layer).

Pokud CDN není k dispozici, implementujte záložní. Otestujte záložní.

Další informace o službě Microsoft Ajax CDN najdete na následujícím webu:

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ScriptManager ASP.NET podporuje Microsoft Ajax CDN. Jednoduše nastavením jedné vlastnosti – vlastnost EnableCdn můžete načíst všechny soubory JavaScriptu rozhraní ASP.NET Framework z CDN:

[!code-aspx[Main](overview/samples/sample20.aspx)]

Po nastavení vlastnosti EnableCdn na hodnotu true rozhraní ASP.NET Framework načte všechny soubory JavaScriptu ASP.NET Framework ze sítě CDN včetně všech souborů JavaScriptu používaných pro ověřování a UpdatePanel. Nastavení této vlastnosti může mít výrazný vliv na výkon vaší webové aplikace.

Můžete nastavit cestu CDN pro vlastní soubory JavaScriptu pomocí atributu WebResource. Nová vlastnost CdnPath Určuje cestu k CDN použité v případě, že nastavíte vlastnost EnableCdn na hodnotu true:

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>Explicitní skripty ScriptManager

Pokud jste v minulosti použili ASP.NET ScriptManger, pak jste museli načíst celou knihovnu monolitické ASP.NET AJAX. Když využijete novou vlastnost ScriptManager. AjaxFrameworkMode, můžete přesně řídit, které součásti knihovny AJAX ASP.NET Library jsou načteny a načteny pouze součásti knihovny ASP.NET AJAX, kterou potřebujete.

Vlastnost ScriptManager. AjaxFrameworkMode lze nastavit na následující hodnoty:

- Enabled – určuje, že ovládací prvek ScriptManager automaticky obsahuje soubor skriptu MicrosoftAjax. js, což je kombinovaný soubor skriptu každého skriptu Core Framework (starší chování).
- Zakázáno – určuje, že všechny funkce skriptu Microsoft AJAX jsou zakázané a že ovládací prvek ScriptManager neodkazuje na žádné skripty automaticky.
- Explicitní – určuje, že budete explicitně zahrnovat odkazy na skripty do samostatného souboru skriptu pro jednotlivé architektury, který vaše stránka vyžaduje, a že budete mít odkazy na závislosti, které každý soubor skriptu vyžaduje.

Například pokud nastavíte vlastnost AjaxFrameworkMode na hodnotu explicitní, můžete určit konkrétní skripty komponenty AJAX v ASP.NET, které potřebujete:

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Webové formuláře

Webové formuláře byly základní funkcí v ASP.NET od vydání ASP.NET 1,0. V této oblasti se nachází celá řada vylepšení pro ASP.NET 4, včetně následujících:

- Možnost nastavení *meta* značek.
- Větší kontrola nad stavem zobrazení.
- Jednodušší způsoby práce s funkcemi prohlížeče.
- Podpora pro použití směrování ASP.NET s webovými formuláři.
- Větší kontrola nad generovanými identifikátory.
- Možnost zachovat vybrané řádky v ovládacích prvcích dat.
- Větší kontrola nad vykresleným HTML v ovládacích prvcích *FormView* a *ListView* .
- Podpora filtrování pro ovládací prvky zdroje dat.

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>Nastavení meta značek pomocí vlastností Page. MetaKeywords a Page. MetaDescription

ASP.NET 4 přidá dvě vlastnosti do třídy *Page* , *MetaKeywords* a *MetaDescription*. Tyto dvě vlastnosti reprezentují odpovídající *metaznačky* značek na stránce, jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample23.aspx)]

Tyto dvě vlastnosti fungují stejným způsobem jako vlastnost *nadpisu* stránky. Dodržují tato pravidla:

1. Pokud element *head* neobsahuje žádné *metaznačky* , které by odpovídaly názvům vlastností (tj. Name = "Keywords" pro *Page. MetaKeywords* a Name = "Description" pro *Page. MetaDescription*, což znamená, že tyto vlastnosti nebyly nastaveny), *metaznačky* budou přidány na stránku, když je vykreslena.
2. Pokud již existují *meta* značky s těmito názvy, tyto vlastnosti se chovají jako metody Get a set pro obsah existujících značek.

Tyto vlastnosti lze nastavit za běhu, což vám umožní získat obsah z databáze nebo jiného zdroje, což umožňuje dynamicky nastavit značky pro popis toho, k čemu konkrétní stránka slouží.

Můžete také nastavit vlastnosti *klíčová slova* a *Popis* v direktivě *@ Page* v horní části značky stránky webových formulářů, jako v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample24.aspx)]

Tato akce přepíše obsah *metaznačky* (pokud existuje) již deklarovaný na stránce.

Obsah *meta* značky Description se používá ke zlepšení výsledků hledání v náhledech v Google. (Podrobnosti najdete v tématu [zlepšení fragmentů kódu pomocí Meta Description změně](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) v centrálním blogu správce internetového správce.) Google a Windows Live Search nepoužívají obsah klíčových slov pro cokoli, ale může to být i u jiných vyhledávacích strojů. Další informace najdete v tématu [doporučení META klíčová slova](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) na webu průvodce vyhledávacími moduly.

Tyto nové vlastnosti jsou jednoduchou funkcí, ale ukládají vám z požadavku, aby je bylo možné přidat ručně nebo pomocí vlastního kódu pro vytvoření *meta* značek.

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>Povolení stavu zobrazení pro jednotlivé ovládací prvky

Ve výchozím nastavení je pro stránku povolen stav zobrazení, s výsledkem, že každý ovládací prvek na stránce potenciálně ukládá stav zobrazení, i když není pro aplikaci vyžadován. Data o stavu zobrazení jsou součástí značky, kterou vygeneruje stránka, a zvyšují dobu potřebnou k odeslání stránky klientovi a jeho následnému vrácení. Ukládání většího stavu zobrazení, než je nutné, může způsobit výrazné snížení výkonu. V dřívějších verzích ASP.NET můžou vývojáři zakázat stav zobrazení pro jednotlivé ovládací prvky, aby se snížila velikost stránky, ale museli tak učinit explicitně pro jednotlivé ovládací prvky. V ASP.NET 4 obsahují ovládací prvky webového serveru vlastnost *ViewStateMode* , která umožňuje zakázat stav zobrazení ve výchozím nastavení a pak ho povolit pouze pro ovládací prvky, které to vyžadují na stránce.

Vlastnost *ViewStateMode* přebírá výčet, který má tři hodnoty: *Enabled*, *disabled*a *Inherit*. *Povoleno* umožňuje zobrazit stav pro tento ovládací prvek a pro všechny podřízené ovládací prvky, které jsou nastaveny na *dědění* nebo nemají žádnou hodnotu. *Disabled* zakáže stav zobrazení a *dědění* určuje, že ovládací prvek používá nastavení *ViewStateMode* z nadřazeného ovládacího prvku.

Následující příklad ukazuje, jak funguje vlastnost *ViewStateMode* . Značky a kód pro ovládací prvky na následující stránce obsahují hodnoty pro vlastnost *ViewStateMode* :

[!code-aspx[Main](overview/samples/sample25.aspx)]

Jak vidíte, kód umožňuje zakázat stav zobrazení pro ovládací prvek PlaceHolder1. Podřízený ovládací prvek Label1 zdědí tuto hodnotu vlastnosti (vlastnost*Inherit* je výchozí hodnota pro ovládací prvky *ViewStateMode* ), a proto neuloží žádný stav zobrazení. V ovládacím prvku PlaceHolder2 je *ViewStateMode* nastaven na *povoleno*, takže Label2 zdědí tuto vlastnost a ukládá stav zobrazení. Při prvním načtení stránky je vlastnost *text* obou ovládacích prvků *popisek* nastavena na řetězec "[třídu dynamicvalue]".

Vlivem těchto nastavení je to, že při prvním načtení stránky se v prohlížeči zobrazí následující výstup:

Zakázané `: [DynamicValue]`

Povoleno:`[DynamicValue]`

Po zpětném odeslání se ale zobrazí následující výstup:

Zakázané `: [DeclaredValue]`

Povoleno:`[DynamicValue]`

Ovládací prvek Label1 (jehož hodnota *ViewStateMode* je nastavená na *disabled*) nezachovává hodnotu, na kterou byl v kódu nastaven. Nicméně ovládací prvek Label2 (jehož hodnota *ViewStateMode* je nastavená na *Enabled*) zachovává svůj stav.

*ViewStateMode* můžete také nastavit v direktivě *@ Page* , jako v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample26.aspx)]

Třída *stránky* je pouze jiný ovládací prvek; funguje jako nadřazený ovládací prvek pro všechny ostatní ovládací prvky na stránce. Výchozí hodnota *ViewStateMode* je *povolena* pro instance *stránky*. Vzhledem k tomu, že ovládací prvky, které jsou ve výchozím nastavení *děděny*, zdědí ovládací prvky vlastnost *Enabled* , pokud jste nenastavili *ViewStateMode* na úrovni stránky nebo ovládacího prvku.

Hodnota vlastnosti *ViewStateMode* určuje, zda je stav zobrazení udržován pouze v případě, že je vlastnost *EnableViewState* nastavena na *hodnotu true*. Pokud je vlastnost *EnableViewState* nastavená na *false*, stav zobrazení se nezachová ani v případě, že je *ViewStateMode* nastavené na *povoleno*.

Dobrá možnost použití této funkce je s ovládacími prvky *ContentPlaceHolder* na stránkách předlohy, kde můžete nastavit *ViewStateMode* na *zakázáno* pro stránku předlohy a pak ji povolit individuálně pro ovládací prvky *ContentPlaceHolder* , které zase obsahují ovládací prvky, které vyžadují stav zobrazení.

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>Změny možností prohlížeče

ASP.NET určuje možnosti prohlížeče, které uživatel používá k procházení webu pomocí funkce s názvem *Možnosti prohlížeče*. Schopnosti prohlížeče jsou reprezentovány objektem *HttpBrowserCapabilities* (vystaveno vlastností *Request. browser* ). Například můžete použít objekt *HttpBrowserCapabilities* k určení, zda typ a verze aktuálního prohlížeče podporují určitou verzi JavaScriptu. Nebo můžete použít objekt *HttpBrowserCapabilities* k určení, zda požadavek pochází z mobilního zařízení.

Objekt *HttpBrowserCapabilities* je řízen sadou definičních souborů prohlížeče. Tyto soubory obsahují informace o možnostech konkrétního prohlížeče. V ASP.NET 4 se tyto soubory definic prohlížeče aktualizovaly tak, aby obsahovaly informace o nedávno zavedených prohlížečích a zařízeních, jako je Google Chrome, výzkum v oblasti Motion BlackBerry smartphone a Apple iPhone.

V následujícím seznamu jsou uvedeny nové soubory definice prohlížeče:

- *BlackBerry. browser*
- *Chrome. browser*
- *Výchozí prohlížeč*
- *Firefox. browser*
- *Brána. browser*
- *Obecný prohlížeč*
- *prohlížeč IE. browser*
- *iemobile. browser*
- *iPhone. browser*
- *Opera. browser*
- *Safari. browser*

#### <a name="using-browser-capabilities-providers"></a>Použití poskytovatelů možností prohlížeče

V ASP.NET verze 3,5 Service Pack 1 můžete definovat možnosti, které má prohlížeč v následujících ohledech:

- Na úrovni počítače můžete vytvořit nebo aktualizovat soubor XML `.browser` v následující složce:

- [!code-console[Main](overview/samples/sample27.cmd)]

- Po definování schopnosti prohlížeče spustíte následující příkaz z příkazového řádku sady Visual Studio, abyste mohli znovu sestavit sestavení schopností prohlížeče a přidat ho do GAC:

- [!code-console[Main](overview/samples/sample28.cmd)]

- Pro jednotlivé aplikace vytvoříte `.browser` soubor ve složce `App_Browsers` aplikace.

Tyto přístupy vyžadují, abyste změnili soubory XML a pro změny na úrovni počítače, musíte po spuštění procesu ASPNET\_regbrowsers. exe restartovat aplikaci.

ASP.NET 4 zahrnuje funkci označovanou jako *poskytovatelé možností prohlížeče*. Jak název navrhuje, umožňuje vytvořit poskytovatele, který zase umožňuje používat vlastní kód k určení možností prohlížeče.

V praxi vývojáři často nedefinují možnosti vlastního prohlížeče. Aktualizace souborů prohlížeče je těžká, proces pro jejich aktualizaci je poměrně složitý a syntaxe XML pro `.browser` soubory může být složitá pro použití a definování. To by vedlo k tomu, že v případě, že existovala společná syntaxe definice prohlížeče nebo databáze, která obsahuje aktuální definice prohlížeče nebo je to i webová služba pro takovou databázi, je tento proces mnohem jednodušší. Funkce pro nové poskytovatele schopností prohlížeče tyto scénáře umožňují a jsou praktické pro vývojáře třetích stran.

Existují dva hlavní přístupy k používání nové funkce poskytovatele možností prohlížeče ASP.NET 4: rozšíření funkcí definice schopností prohlížeče ASP.NET nebo jejich úplné nahrazení. Následující části popisují první způsob, jak tyto funkce nahradit, a postup, jak je zvětšit.

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>Nahrazení funkcí možností prohlížeče ASP.NET

K úplnému nahrazení funkce definice schopností prohlížeče ASP.NET použijte následující postup:

1. Vytvořte třídu zprostředkovatele, která je odvozena z *HttpCapabilitiesProvider* a přepíše metodu *GetBrowserCapabilities* , jak je uvedeno v následujícím příkladu: 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    Kód v tomto příkladu vytvoří nový objekt *HttpBrowserCapabilities* , který určí pouze schopnost s názvem Browser a nastaví tuto schopnost na MyCustomBrowser.
2. Zaregistrujte zprostředkovatele v aplikaci. 

    Aby bylo možné použít poskytovatele s aplikací, je nutné přidat atribut *Provider* do oddílu *browserCaps* v souborech `Web.config` nebo `Machine.config`. (Můžete také definovat atributy poskytovatele v elementu *umístění* pro konkrétní adresáře v aplikaci, například ve složce pro určité mobilní zařízení.) Následující příklad ukazuje, jak nastavit atribut *Provider* v konfiguračním souboru:

    [!code-xml[Main](overview/samples/sample30.xml)]

    Dalším způsobem, jak zaregistrovat novou definici schopností prohlížeče, je použít kód, jak je znázorněno v následujícím příkladu:

    [!code-csharp[Main](overview/samples/sample31.cs)]

    Tento kód musí být spuštěn v *aplikaci\_spuštění* události `Global.asax` souboru. Aby se zajistilo, že mezipaměť zůstane v platném stavu pro vyřešený objekt *HttpCapabilitiesBase* , musí dojít ke změně třídy *BrowserCapabilitiesProvider* .

#### <a name="caching-the-httpbrowsercapabilities-object"></a>Ukládání objektu HttpBrowserCapabilities do mezipaměti

Předchozí příklad obsahuje jeden problém, což znamená, že kód se spustí pokaždé, když se vyvolá vlastní zprostředkovatel, aby se získal objekt *HttpBrowserCapabilities* . Tato situace může nastat několikrát během každé žádosti. V příkladu kód poskytovatele nedělá mnoho. Nicméně pokud kód ve vlastním zprostředkovateli provádí významnou práci, aby získal objekt *HttpBrowserCapabilities* , může to mít vliv na výkon. Chcete-li zabránit tomu, aby se to stalo, můžete objekt *HttpBrowserCapabilities* Uložit do mezipaměti. Postupujte podle těchto kroků:

1. Vytvořte třídu, která je odvozena z *HttpCapabilitiesProvider*, podobně jako v následujícím příkladu: 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    V příkladu kód generuje klíč mezipaměti voláním vlastní metody BuildCacheKey a získá dobu ukládání do mezipaměti voláním vlastní metody GetCacheTime. Kód pak přidá vyřešený objekt *HttpBrowserCapabilities* do mezipaměti. Objekt lze načíst z mezipaměti a znovu použít u dalších požadavků, které využívají vlastního zprostředkovatele.
2. Zaregistrujte poskytovatele s aplikací, jak je popsáno v předchozím postupu.

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>Rozšíření funkcí prohlížeče ASP.NET

Předchozí část popisuje, jak vytvořit nový objekt *HttpBrowserCapabilities* v ASP.NET 4. Funkce prohlížeče ASP.NET můžete také roztáhnout přidáním nových definic schopností prohlížeče do těch, které jsou už v ASP.NET. To můžete provést bez použití definic prohlížeče XML. Následující postup ukazuje, jak.

1. Vytvořte třídu, která je odvozena z *HttpCapabilitiesEvaluator* a přepíše metodu *GetBrowserCapabilities* , jak je znázorněno v následujícím příkladu: 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    Tento kód nejprve používá funkci schopností prohlížeče ASP.NET k pokusu o identifikaci prohlížeče. Pokud však není identifikován žádný prohlížeč na základě informací definovaných v žádosti (tj. Pokud je vlastnost *prohlížeče* objektu *HttpBrowserCapabilities* řetězec "unknown"), kód volá vlastního poskytovatele (MyBrowserCapabilitiesEvaluator), který identifikuje prohlížeč.
2. Zaregistrujte poskytovatele u aplikace, jak je popsáno v předchozím příkladu.

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>Rozšíření funkcí prohlížeče přidáním nových funkcí do stávajících definic schopností

Kromě vytvoření vlastního poskytovatele definice prohlížeče a dynamického vytváření nových definic prohlížeče můžete rozšířit existující definice prohlížečů o další možnosti. To vám umožní použít definici, která se blíží k tomu, co potřebujete, ale nemá jenom několik možností. K tomu použijte následující postup.

1. Vytvořte třídu, která je odvozena z *HttpCapabilitiesEvaluator* a přepíše metodu *GetBrowserCapabilities* , jak je znázorněno v následujícím příkladu: 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    Ukázkový kód rozšiřuje existující třídu ASP.NET *HttpCapabilitiesEvaluator* a získá objekt *HttpBrowserCapabilities* , který odpovídá aktuální definici žádosti pomocí následujícího kódu:

    [!code-csharp[Main](overview/samples/sample35.cs)]

    Kód pak může přidat nebo změnit schopnost tohoto prohlížeče. Existují dva způsoby, jak zadat novou funkci prohlížeče:

    - Přidejte dvojici klíč/hodnota k objektu *IDictionary* , který je vystavený vlastností *Capabilities* objektu *HttpCapabilitiesBase* . V předchozím příkladu kód přidá schopnost s názvem MultiTouch s hodnotou *true*.
    - Nastavte existující vlastnosti objektu *HttpCapabilitiesBase* . V předchozím příkladu kód nastaví vlastnost *rámců* na *hodnotu true*. Tato vlastnost je jednoduše přistupující objekt pro objekt *IDictionary* , který je vystavený vlastností *Capabilities* . 

        > [!NOTE]
        > Poznámka: Tento model se vztahuje na jakoukoliv vlastnost *HttpBrowserCapabilities*, včetně adaptérů ovládacích prvků.
2. Zaregistrujte poskytovatele s aplikací, jak je popsáno v předchozím postupu.

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>Směrování v ASP.NET 4

ASP.NET 4 přidává integrovanou podporu pro používání směrování s webovými formuláři. Směrování umožňuje nakonfigurovat aplikaci tak, aby přijímala adresy URL požadavků, které nemapují fyzické soubory. Místo toho můžete použít směrování k definování adres URL, které jsou smysluplné pro uživatele a které můžou pro vaši aplikaci pomáhat s optimalizací vyhledávačů (SEO). Například adresa URL stránky, která zobrazuje kategorie produktů v existující aplikaci, může vypadat jako v následujícím příkladu:

[!code-console[Main](overview/samples/sample36.cmd)]

Pomocí směrování můžete nakonfigurovat aplikaci tak, aby při vykreslování stejných informací přijímala následující adresu URL:

[!code-console[Main](overview/samples/sample37.cmd)]

Směrování bylo od verze ASP.NET 3,5 SP1 k dispozici. (Příklad použití směrování v ASP.NET 3,5 SP1 najdete v tématu [použití směrování s Webformami](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Název této položky") na blogu Filip Haack.) ASP.NET 4 ale obsahuje některé funkce, které usnadňují používání směrování, včetně následujících:

- Třída *PageRouteHandler* , což je jednoduchá obslužná rutina http, kterou použijete při definování tras. Třída předává data na stránku, na kterou je požadavek směrován.
- Nové vlastnosti *HttpRequest. třída RequestContext* a *Page. parametr RouteData* (což je proxy server pro objekt *HttpRequest. Třída requestContext. parametr RouteData* ). Tyto vlastnosti usnadňují přístup k informacím, které se předávají z trasy.
- Následující nové tvůrci výrazů, které jsou definovány v *System. Web. Compilation. RouteUrlExpressionBuilder* a *System. Web. Compilation. RouteValueExpressionBuilder*:
- *RouteUrl*, která poskytuje jednoduchý způsob, jak vytvořit adresu URL, která odpovídá adrese URL trasy v rámci ovládacího prvku ASP.NET serveru.
- *RouteValue*, která poskytuje jednoduchý způsob, jak extrahovat informace z objektu *RouteContext* .
- Třída *RouteParameter* , která usnadňuje předávání dat obsažených v objektu *RouteContext* do dotazu pro řízení zdrojů dat (podobně jako [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).

#### <a name="routing-for-web-forms-pages"></a>Směrování pro stránky webových formulářů

Následující příklad ukazuje, jak definovat trasu webových formulářů pomocí nové metody *MapPageRoute* třídy *Route* :

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4 zavádí metodu *MapPageRoute* . Následující příklad je ekvivalentní k definici SearchRoute, která je uvedená v předchozím příkladu, ale používá třídu *PageRouteHandler* .

[!code-csharp[Main](overview/samples/sample39.cs)]

Kód v příkladu mapuje trasu na fyzickou stránku (v první trase na `~/search.aspx`). První definice trasy také určuje, že parametr s názvem searchterm by měl být extrahován z adresy URL a předán na stránku.

Metoda *MapPageRoute* podporuje následující přetížení metod:

- *MapPageRoute (řetězec-řetěz, řetězec routeUrl, String physicalFile, bool checkPhysicalUrlAccess)*
- *MapPageRoute (řetězec-řetěz, řetězec routeUrl, String physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary Defaults)*
- *MapPageRoute (řetězec, řetěz, řetězec routeUrl, String physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary Defaults, omezení RouteValueDictionary)*

Parametr *checkPhysicalUrlAccess* určuje, zda má trasa kontrolovat oprávnění zabezpečení pro fyzickou stránku, na kterou se směruje (v tomto případě Search. aspx) a oprávnění na příchozí adrese URL (v tomto případě Search/{searchterm}). Pokud je hodnota *checkPhysicalUrlAccess* *false*, budou kontrolována pouze oprávnění příchozí adresy URL. Tato oprávnění se definují v souboru `Web.config` s použitím nastavení, jako je třeba následující:

[!code-xml[Main](overview/samples/sample40.xml)]

V ukázkové konfiguraci je přístup k fyzické stránce `search.aspx` pro všechny uživatele s výjimkou těch, kteří jsou v roli správce, odepřený. Pokud je parametr *checkPhysicalUrlAccess* nastaven na *hodnotu true* (což je výchozí hodnota), budou mít přístup k adrese URL/Search/{searchterm} jenom oprávnění uživatelé s oprávněními správce, protože fyzická stránka hledání. aspx je omezená na uživatele v této roli. Pokud je *checkPhysicalUrlAccess* nastavené na *false* a lokalita je nakonfigurovaná tak, jak je znázorněno v předchozím příkladu, všichni ověření uživatelé mají povolený přístup k adrese URL/Search/{searchterm}.

#### <a name="reading-routing-information-in-a-web-forms-page"></a>Čtení informací o směrování na stránce webového formuláře

V kódu fyzické stránky webových formulářů můžete získat přístup k informacím, které směrování vyvolalo z adresy URL (nebo jiné informace, které přidal jiný objekt do objektu *parametr RouteData* ) pomocí dvou nových vlastností: *HttpRequest. třída RequestContext* a *Page. parametr RouteData*. (*Page. parametr RouteData* zabalí *HttpRequest. Třída requestContext. parametr RouteData*.) Následující příklad ukazuje, jak použít *Page. parametr RouteData*.

[!code-csharp[Main](overview/samples/sample41.cs)]

Kód extrahuje hodnotu, která byla předána parametru searchterm, jak je definováno v příkladu předchozí trasy. Vezměte v úvahu následující adresu URL požadavku:

[!code-console[Main](overview/samples/sample42.cmd)]

Po provedení tohoto požadavku se na stránce `search.aspx` vykreslí slovo "Scott".

#### <a name="accessing-routing-information-in-markup"></a>Přístup k informacím o směrování v kódu

Metoda popsaná v předchozí části ukazuje, jak získat data směrování v kódu na stránce webového formuláře. Můžete také použít výrazy v kódu, které vám umožní přístup ke stejným informacím. Tvůrci výrazů představují výkonný a elegantní způsob práce s deklarativním kódem. (Další informace najdete v tématu [s vlastními tvůrci výrazů](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) na blogu Filip Haack.)

ASP.NET 4 obsahuje dva nové tvůrci výrazů pro směrování webových formulářů. Následující příklad ukazuje, jak je používat.

[!code-aspx[Main](overview/samples/sample43.aspx)]

V příkladu se výraz *RouteUrl* používá k definování adresy URL, která je založena na parametru směrování. Tím se ušetříte tím, že zadáte úplnou adresu URL do značky a umožníte změnit strukturu adresy URL později bez nutnosti jakékoli změny tohoto odkazu.

V závislosti na dříve definované trase generuje tento kód následující adresu URL:

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET automaticky funguje v závislosti na vstupních parametrech správnou trasou (to znamená, že generuje správnou adresu URL). Do výrazu můžete také zahrnout název směrování, který vám umožní určit trasu, která se má použít.

Následující příklad ukazuje, jak použít výraz *RouteValue* .

[!code-aspx[Main](overview/samples/sample45.aspx)]

Když se stránka obsahující tento ovládací prvek spustí, zobrazí se v popisku hodnota "Scott".

Výraz *RouteValue* usnadňuje použití směrovacích dat ve značkách a zabraňuje tomu, aby v kódu používala složitější syntaxi Page. parametr RouteData ["x"].

#### <a name="using-route-data-for-data-source-control-parameters"></a>Použití dat směrování pro parametry ovládacího prvku zdroje dat

Třída *RouteParameter* umožňuje zadat data směrování jako hodnotu parametru pro dotazy v ovládacím prvku zdroje dat. [Funguje podobně](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) jako třída, jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample46.aspx)]

V tomto případě se hodnota parametru Route searchterm použije pro parametr @companyname v příkazu *Select* .

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>Nastavení ID klientů

Nová vlastnost *ClientIDMode* řeší dlouhotrvající problém v ASP.NET, konkrétně způsob, jakým ovládací prvky vytvoří atribut *ID* pro prvky, které vykreslují. Znalost atributu *ID* pro vykreslené elementy je důležitá, pokud vaše aplikace obsahuje skript klienta, který na tyto prvky odkazuje.

Atribut *ID* ve formátu HTML, který je vykreslen pro ovládací prvky webového serveru, je vygenerován na základě vlastnosti *ClientID* ovládacího prvku. Do ASP.NET 4 byl algoritmus pro vygenerování atributu *ID* z vlastnosti *ClientID* zřetězený názvový kontejner (pokud existuje) s ID a v případě opakovaných ovládacích prvků (jako v ovládacích prvcích dat) pro přidání předpony a sekvenčního čísla. I když má vždycky zaručeno, že identifikátory ovládacích prvků na stránce jsou jedinečné, výsledkem algoritmu jsou ID ovládacích prvků, které nebyly předvídatelné, a bylo by proto obtížné odkazovat v klientském skriptu.

Nová vlastnost *ClientIDMode* umožňuje zadat přesnější způsob generování ID klienta pro ovládací prvky. Můžete nastavit vlastnost *ClientIDMode* pro jakýkoli ovládací prvek, včetně stránky. Možná nastavení jsou následující:

- *AutoID* – jedná se o ekvivalent algoritmu pro generování hodnot vlastností *ClientID* , které byly použity v dřívějších verzích nástroje ASP.NET.
- *Static* – určuje, že hodnota *ClientID* bude stejná jako ID bez zřetězení identifikátorů nadřazených názvových kontejnerů. To může být užitečné pro webové uživatelské ovládací prvky. Vzhledem k tomu, že webový uživatelský ovládací prvek může být umístěn na různých stránkách a v různých ovládacích prvcích kontejneru, může být obtížné napsat klientský skript pro ovládací prvky, které používají algoritmus *AutoID* , protože nemůžete předpovědět, jaké hodnoty ID budou.
- *Předvídatelné* – Tato možnost je primárně určena pro použití v ovládacích prvcích dat, které používají opakující se šablony. Zřetězuje vlastnosti ID názvových kontejnerů ovládacího prvku, ale generované hodnoty *ClientID* neobsahují řetězce, jako je například "ctlxxx". Toto nastavení funguje ve spojení s vlastností *ClientIDRowSuffix* ovládacího prvku. Vlastnost *ClientIDRowSuffix* nastavíte na název datového pole a hodnota tohoto pole se použije jako přípona pro generovanou hodnotu *ClientID* . Obvykle byste použili primární klíč datového záznamu jako hodnotu *ClientIDRowSuffix* .
- *Inherit* – toto nastavení je výchozí chování pro ovládací prvky. Určuje, že generování ID ovládacího prvku je stejné jako jeho nadřazený objekt.

Vlastnost *ClientIDMode* lze nastavit na úrovni stránky. To definuje výchozí hodnotu *ClientIDMode* pro všechny ovládací prvky na aktuální stránce.

Výchozí hodnota *ClientIDMode* na úrovni stránky je *AutoID*a výchozí hodnota *ClientIDMode* na úrovni ovládacího prvku je *děděna*. V důsledku toho, pokud nenastavíte tuto vlastnost kdekoli v kódu, všechny ovládací prvky budou standardně *AutoID* algoritmus.

Hodnotu na úrovni stránky nastavíte v direktivě *@ Page* , jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample47.aspx)]

Hodnotu *ClientIDMode* můžete také nastavit v konfiguračním souboru, a to buď na úrovni počítače (počítač), nebo na úrovni aplikace. To definuje výchozí nastavení *ClientIDMode* pro všechny ovládací prvky na všech stránkách v aplikaci. Pokud nastavíte hodnotu na úrovni počítače, definuje se výchozí nastavení *ClientIDMode* pro všechny weby na tomto počítači. Následující příklad ukazuje nastavení *ClientIDMode* v konfiguračním souboru:

[!code-xml[Main](overview/samples/sample48.xml)]

Jak bylo uvedeno dříve, hodnota vlastnosti *ClientID* je odvozena z názvového kontejneru pro nadřazený ovládací prvek ovládacího prvku. V některých případech, například při použití stránek předlohy, mohou ovládací prvky končit ID, jako jsou ty v následujícím vykresleném HTML:

[!code-html[Main](overview/samples/sample49.html)]

I když je *vstupní* prvek zobrazený v kódu (z ovládacího prvku *TextBox* ) pouze dva kontejnery pojmenování hluboko na stránce (vnořené ovládací prvky *ContentPlaceHolder* ), z důvodu způsobu zpracování stránek předlohy je konečný výsledek ovládací prvek ID ovládacího prvku, například následující:

[!code-console[Main](overview/samples/sample50.cmd)]

U tohoto ID je zaručeno, že je na stránce jedinečný, ale pro většinu účelů je to zbytečně dlouhé. Představte si, že chcete snížit délku vykresleného ID a mít větší kontrolu nad tím, jak se ID vygeneruje. (Například chcete odstranit předpony "ctlxxx".) Nejjednodušší způsob, jak toho dosáhnout, je nastavit vlastnost *ClientIDMode* , jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample51.aspx)]

V této ukázce je vlastnost *ClientIDMode* nastavena na hodnotu *static* pro nejvzdálenější element *NamingPanel* a je nastavena na *předvídatelné* pro vnitřní prvek *NamingControl* . Toto nastavení má za následek následující značky (zbytek stránky a stránka předlohy se považuje za stejnou jako v předchozím příkladu):

[!code-html[Main](overview/samples/sample52.html)]

*Statické* nastavení má vliv na resetování hierarchie názvů pro všechny ovládací prvky uvnitř nejvzdálenějšího prvku *NamingPanel* a odstranění identifikátorů *ContentPlaceHolder* a *MasterPage* z generovaného ID. ( *Název* atributu vykreslených prvků není nijak ovlivněn, takže normální funkce ASP.NET jsou uchovány pro události, stav zobrazení a tak dále.) Vedlejším účinkem resetování hierarchie názvů je, že i když přesunete značky pro prvky *NamingPanel* do jiného ovládacího prvku *ContentPlaceHolder* , vykreslená ID klientů zůstanou stejná.

> [!NOTE]
> Všimněte si, že je k dispaměti, abyste se ujistili, že ID vykreslených ovládacích prvků jsou jedinečná. Pokud nejsou, může přerušit všechny funkce, které vyžadují jedinečné identifikátory pro jednotlivé prvky HTML, jako je například klient *Document. getElementById* .

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>Vytváření předvídatelných ID klientů v ovládacích prvcích vázaných na data

Hodnoty *ClientID* , které jsou generovány pro ovládací prvky v ovládacím prvku seznamu vázaného na data pomocí staršího algoritmu, mohou být dlouhé a nejsou skutečně předvídatelné. Funkce *ClientIDMode* vám může pomáhat získat větší kontrolu nad tím, jak se tyto identifikátory generují.

Označení v následujícím příkladu obsahuje ovládací prvek *ListView* :

[!code-aspx[Main](overview/samples/sample53.aspx)]

V předchozím příkladu jsou vlastnosti *ClientIDMode* a *RowClientIDRowSuffix* nastaveny v označení. Vlastnost *ClientIDRowSuffix* lze použít pouze v ovládacích prvcích vázaných na data a její chování se liší v závislosti na tom, který ovládací prvek používáte. Rozdíly jsou tyto:

- Ovládací prvek *GridView* – můžete zadat název jednoho nebo více sloupců ve zdroji dat, které jsou kombinovány v době běhu, a vytvořit tak ID klientů. Například pokud nastavíte *RowClientIDRowSuffix* na "ProductName, ProductID", identifikátory ovládacího prvku pro vykreslené elementy budou mít formát podobný následujícímu:

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView* – ovládací prvek – můžete zadat jeden sloupec ve zdroji dat, který je připojen k ID klienta. Například pokud nastavíte *ClientIDRowSuffix* na "ProductName", vygenerované identifikátory ovládacího prvku budou mít formát podobný následujícímu:

- [!code-console[Main](overview/samples/sample55.cmd)]

- V tomto případě je koncové číslo 1 odvozeno z ID produktu aktuální datové položky.

- *Repeater* – ovládací prvek – tento ovládací prvek nepodporuje vlastnost *ClientIDRowSuffix* . V ovládacím prvku *Repeater* je použit index aktuálního řádku. Při použití ClientIDMode = "předvídatelného" s ovládacím prvkem *Repeater* se generují ID klientů, které mají následující formát:

- [!code-console[Main](overview/samples/sample56.cmd)]

- Koncová hodnota 0 je index aktuálního řádku.

Ovládací prvky *FormView* a *DetailsView* nezobrazují více řádků, takže nepodporují vlastnost *ClientIDRowSuffix* .

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>Trvalé vybírání výběru řádků v datových ovládacích prvcích

Ovládací prvky *GridView* a *ListView* můžou dovolit uživatelům vybrat řádek. V předchozích verzích ASP.NET byl výběr založen na indexu řádku na stránce. Pokud například vyberete třetí položku na stránce 1 a pak přejdete na stránku 2, vybere se třetí položka na této stránce.

Trvalý výběr byl zpočátku podporován pouze v dynamických datových projektech v .NET Framework 3,5 SP1. Když je tato funkce povolená, aktuální vybraná položka je založena na datovém klíči pro položku. To znamená, že pokud na stránce 1 vyberete třetí řádek a přesunete na stránku 2, na stránce 2 není nic vybráno. Když přejdete zpátky na stránku 1, třetí řádek je stále vybraný. Trvalý výběr je nyní podporován pro ovládací prvky *GridView* a *ListView* ve všech projektech pomocí vlastnosti *EnablePersistedSelection* , jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>Ovládací prvek grafu ASP.NET

Ovládací prvek *grafu* ASP.NET rozbalí nabídky vizualizace dat v .NET Framework. Pomocí ovládacího prvku *graf* můžete vytvářet ASP.NET stránky, které mají intuitivní a vizuálně působivé grafy pro komplexní statistické nebo finanční analýzy. Ovládací prvek *grafu* ASP.NET byl představen jako doplněk pro verzi .NET Framework verze 3,5 SP1 a je součástí verze .NET Framework 4.

Ovládací prvek obsahuje následující funkce:

- 35 různých typů grafů.
- Neomezený počet oblastí grafu, názvů, legend a poznámek.
- Širokou škálu nastavení vzhledu pro všechny prvky grafu.
- podpora 3D pro většinu typů grafů.
- Inteligentní popisky dat, které lze automaticky umístit kolem datových bodů.
- Čáry pruhů, oddělovacích čar měřítka a logaritmické měřítko.
- Více než 50 finančních a statistických vzorců pro analýzu a transformaci dat.
- Jednoduchá vazba a manipulace s daty grafu
- Podpora pro běžné formáty dat, jako jsou data, časy a měna
- Podpora pro interaktivitu a přizpůsobení událostí, včetně událostí klientského kliknutí v AJAX.
- Správa stavu.
- Binární streamování.

Následující obrázky znázorňují příklady finančních grafů vyprodukovaných ovládacím prvkem grafu ASP.NET.

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

Obrázek 2: příklady ovládacího prvku graf ASP.NET

Další příklady použití ovládacího prvku graf ASP.NET najdete v tématu Ukázka kódu na stránce [ukázek prostředí pro ovládací prvky Microsoft Chart](https://go.microsoft.com/fwlink/?LinkId=128300) na webu MSDN. Další ukázky obsahu komunity najdete na [fóru řízení grafu](https://go.microsoft.com/fwlink/?LinkId=128713).

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>Přidání ovládacího prvku graf na stránku ASP.NET

Následující příklad ukazuje, jak přidat ovládací prvek *grafu* na stránku ASP.NET pomocí značek. V tomto příkladu generuje ovládací prvek *graf* pro statické datové body sloupcový graf.

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>Použití 3D grafů

Ovládací prvek *grafu* obsahuje kolekci *ChartArea* , která může obsahovat objekty *ChartArea* definující charakteristiky oblastí grafu. Chcete-li například pro oblast grafu použít 3D, použijte vlastnost *Area3DStyle* jako v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample59.aspx)]

Následující obrázek ukazuje prostorový graf se čtyřmi řadami typu *pruhového* grafu.

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

Obrázek 3:3 pruhový graf D

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>Použití oddělovacích čar měřítka a logaritmických stupnicí

Oddělovací čáry měřítka a logaritmická měřítka jsou dva další způsoby, jak přidat sofistikovanější do grafu. Tyto funkce jsou specifické pro každou osu v oblasti grafu. Chcete-li například použít tyto funkce na primární ose Y oblasti grafu, použijte vlastnost *Axis.* ScaleBreakStyle a vlastnosti v objektu *ChartArea* . Následující fragment kódu ukazuje, jak používat oddělovací čáry měřítka na primární ose Y.

[!code-aspx[Main](overview/samples/sample60.aspx)]

Následující obrázek ukazuje osu Y s povolenými oddělovacími oddělovači stupnice.

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

Obrázek 4: oddělovací čáry měřítka

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>Filtrování dat pomocí ovládacího prvku třídou QueryExtender

Velmi běžnou úlohou pro vývojáře, kteří vytvářejí webové stránky řízené daty, je filtrování dat. To je tradičně provedeno vytvořením klauzulí *WHERE* v ovládacích prvcích zdroje dat. Tento přístup může být složitý a v některých případech syntaxe *WHERE* neumožňuje využívat všechny funkce podkladové databáze.

Aby bylo filtrování snazší, přidal se do ASP.NET 4 nový ovládací prvek *třídou QueryExtender* . Tento ovládací prvek lze přidat k ovládacím prvkům *EntityDataSource* nebo *LinqDataSource* za účelem filtrování dat vrácených těmito ovládacími prvky. Vzhledem k tomu, že ovládací prvek *třídou QueryExtender* spoléhá na LINQ, na databázovém serveru se použije filtr předtím, než se data odešlou na stránku, což má za následek velice efektivní operace.

Ovládací prvek *třídou QueryExtender* podporuje celou řadu možností filtrování. Následující části popisují tyto možnosti a poskytují příklady, jak je používat.

#### <a name="search"></a>Hledat

Pro možnost hledání provede ovládací prvek *třídou QueryExtender* hledání v zadaných polích. V následujícím příkladu ovládací prvek používá text, který je zadán v ovládacím prvku TextBoxSearch a vyhledává jeho obsah ve sloupcích `ProductName` a `Supplier.CompanyName` v datech, která jsou vrácena z ovládacího prvku *LinqDataSource* .

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>Rozsah

Možnost rozsah je podobná možnosti hledání, ale určuje dvojici hodnot pro definování rozsahu. V následujícím příkladu ovládací prvek *třídou QueryExtender* vyhledává sloupec `UnitPrice` v datech vrácených z ovládacího prvku *LinqDataSource* . Rozsah je čten z ovládacích prvků TextBoxFrom a TextBoxTo na stránce.

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

Možnost výrazu vlastnosti umožňuje definovat porovnání s hodnotou vlastnosti. Pokud se výraz vyhodnotí jako *true*, vrátí se data, která se vyhodnocují. V následujícím příkladu ovládací prvek *třídou QueryExtender* filtruje data porovnáním dat ve sloupci `Discontinued` k hodnotě z ovládacího prvku CheckBoxDiscontinued na stránce.

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

Nakonec můžete zadat vlastní výraz pro použití s ovládacím prvkem *třídou QueryExtender* . Tato možnost umožňuje zavolat funkci na stránce, která definuje vlastní logiku filtru. Následující příklad ukazuje, jak deklarativně zadat vlastní výraz v ovládacím prvku *třídou QueryExtender* .

[!code-aspx[Main](overview/samples/sample64.aspx)]

Následující příklad ukazuje vlastní funkci, která je vyvolána ovládacím prvkem *třídou QueryExtender* . V tomto případě, namísto použití databázového dotazu, který obsahuje klauzuli *WHERE* , kód používá dotaz LINQ k filtrování dat.

[!code-csharp[Main](overview/samples/sample65.cs)]

Tyto příklady znázorňují v jednom okamžiku pouze jeden výraz, který se používá v ovládacím prvku *třídou QueryExtender* . Do ovládacího prvku *třídou QueryExtender* však lze zahrnout více výrazů.

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Výrazy kódovaného kódu ve formátu HTML

Některé weby ASP.NET (zejména s ASP.NET MVC) se velmi spoléhají na použití `<%`= `expression %>` syntaxi (často nazývané "Code Nuggets"), která zapisuje nějaký text do odpovědi. Pokud používáte výrazy kódu, je snadné zakódovat text ve formátu HTML, pokud text pochází ze vstupu uživatele, může zůstat stránky otevřené pro útok XSS (křížení skriptování mezi weby).

ASP.NET 4 zavádí následující novou syntaxi pro výrazy kódu:

[!code-aspx[Main](overview/samples/sample66.aspx)]

Tato syntaxe při zápisu do odpovědi používá kódování HTML ve výchozím nastavení. Tento nový výraz se efektivně převede na následující:

[!code-aspx[Main](overview/samples/sample67.aspx)]

Například &lt;%: Request ["UserInput"]%&gt; provádí kódování HTML na hodnotě *požadavku ["userinput"]* .

Cílem této funkce je, aby bylo možné nahradit všechny výskyty staré syntaxe novou syntaxí, takže nebudete muset se rozhodnout pro každý krok, který se má použít. Existují však případy, kdy je výstup textu určen jako HTML nebo je již kódován. v takovém případě to může vést k dvojímu kódování.

V těchto případech ASP.NET 4 zavádí nové rozhraní *IHtmlString*spolu s konkrétní implementací *HtmlString*. Instance těchto typů umožňují určit, že návratová hodnota je již správně kódována (nebo jinak prověřena) pro zobrazení jako HTML a že hodnota by proto neměla být znovu kódována ve formátu HTML. Například následující by neměl být (a není) kódovaný v jazyce HTML:

[!code-aspx[Main](overview/samples/sample68.aspx)]

Pomocné metody ASP.NET MVC 2 byly aktualizovány tak, aby fungovaly s touto novou syntaxí, takže nejsou dvojitě zakódovány, ale pouze v případě, že používáte ASP.NET 4. Tato nová syntaxe nefunguje, když aplikaci spouštíte pomocí ASP.NET 3,5 SP1.

Mějte na paměti, že to nezaručuje ochranu proti útokům XSS. Například kód HTML, který používá hodnoty atributu, které nejsou v uvozovkách, může obsahovat vstup uživatele, který je stále náchylný. Všimněte si, že výstup ovládacích prvků ASP.NET a ASP.NET pomocníka MVC vždy obsahuje hodnoty atributu v uvozovkách, což je doporučený přístup.

Podobně tato syntaxe neprovádí kódování jazyka JavaScript, například při vytváření řetězce JavaScriptu na základě vstupu uživatele.

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>Změny šablony projektu

V dřívějších verzích ASP.NET, při použití sady Visual Studio k vytvoření nového projektu webu nebo projektu webové aplikace, výsledné projekty obsahují pouze stránku Default. aspx, výchozí `Web.config` soubor a složku `App_Data`, jak je znázorněno na následujícím obrázku:

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio také podporuje prázdný typ projektu webu, který neobsahuje žádné soubory, jak je znázorněno na následujícím obrázku:

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

Výsledkem je, že pro začátečníky existuje velmi málo informací o tom, jak vytvořit produkční webovou aplikaci. Proto ASP.NET 4 zavádí tři nové šablony, jednu pro prázdný projekt webové aplikace a jednu pro webovou aplikaci a projekt webu.

#### <a name="empty-web-application-template"></a>Prázdná šablona webové aplikace

Jak je navrženo, prázdná šablona webové aplikace je dewebový projekt webové aplikace. Tuto šablonu projektu vyberete v dialogovém okně Nový projekt aplikace Visual Studio, jak je znázorněno na následujícím obrázku:

[![](overview/_static/image7.png)](overview/_static/image6.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](overview/_static/image8.png))

Když vytvoříte prázdnou webovou aplikaci v ASP.NET, Visual Studio vytvoří následující rozložení složky:

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

To je podobné jako prázdné rozložení webu z dřívějších verzí ASP.NET, s jednou výjimkou. V aplikaci Visual Studio 2010 prázdné webové aplikace a prázdné projekty webu obsahují následující minimální `Web.config` soubor, který obsahuje informace používané v aplikaci Visual Studio k identifikaci architektury, na kterou projekt cílí:

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

Bez této vlastnosti *targetFramework* se v aplikaci Visual Studio standardně cílí na .NET Framework 2,0, aby při otevírání starších aplikací zůstala zachována kompatibilita.

#### <a name="web-application-and-web-site-project-templates"></a>Šablony projektů webové aplikace a webu

Další dvě nové šablony projektu, které jsou dodávány se sadou Visual Studio 2010, obsahují významné změny. Následující obrázek ukazuje rozložení projektu, které je vytvořeno při vytváření nového projektu webové aplikace. (Rozložení projektu webu je prakticky identické.)

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

Projekt obsahuje několik souborů, které nebyly vytvořeny v dřívějších verzích. Kromě toho je nový projekt webové aplikace nakonfigurován se základními funkcemi členství, což vám umožní rychle začít v zabezpečení přístupu k nové aplikaci. Z důvodu tohoto zahrnutí soubor `Web.config` pro nový projekt obsahuje položky, které se používají ke konfiguraci členství, rolí a profilů. Následující příklad ukazuje soubor `Web.config` pro nový projekt webové aplikace. (V tomto případě je *roleManager* zakázaný.)

[![](overview/_static/image13.png)](overview/_static/image12.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](overview/_static/image14.png))

Projekt obsahuje také druhý `Web.config` soubor v adresáři `Account`. Druhý konfigurační soubor poskytuje způsob, jak zabezpečit přístup ke stránce ChangePassword. aspx pro přihlášené uživatele. Následující příklad ukazuje obsah druhého souboru `Web.config`.

![](overview/_static/image15.png)

Stránky vytvořené ve výchozím nastavení v nových šablonách projektů také obsahují více obsahu než v předchozích verzích. Projekt obsahuje výchozí stránku předlohy a soubor CSS a výchozí stránka (default. aspx) je nastavena na používání hlavní stránky ve výchozím nastavení. Výsledkem je, že při prvním spuštění webové aplikace nebo webu je již funkční výchozí (Domovská) stránka. Ve skutečnosti se podobá výchozí stránce, kterou vidíte při spuštění nové aplikace MVC.

[![](overview/_static/image17.png)](overview/_static/image16.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](overview/_static/image18.png))

Záměrem těchto změn v šablonách projektů je poskytnout pokyny, jak začít vytvářet novou webovou aplikaci. V případě sémanticky správné značky kompatibilní s NORMou XHTML 1,0 a s rozložením, které je zadáno pomocí šablon stylů CSS, stránky v šablonách reprezentují osvědčené postupy pro sestavování webových aplikací ASP.NET 4. Výchozí stránky mají také rozložení se dvěma sloupci, které lze snadno přizpůsobit.

Představte si například, že pro novou webovou aplikaci, kterou chcete změnit některé barvy, a místo loga moje aplikace ASP.NET vložte logo společnosti. K tomu je potřeba vytvořit v části `Content` nový adresář pro uložení obrázku loga:

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

Chcete-li přidat obrázek na stránku, otevřete `Site.Master` soubor, najděte, kde je text aplikace ASP.NET definován a nahraďte ho prvkem *obrázku* , jehož atribut *Src* je nastaven na nový obrázek loga, jak je uvedeno v následujícím příkladu:

[![](overview/_static/image21.png)](overview/_static/image20.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](overview/_static/image22.png))

Pak můžete přejít do souboru Web. CSS a upravit definice třídy CSS a změnit barvu pozadí stránky a také záhlaví.

Výsledkem těchto změn je, že můžete zobrazit vlastní domovskou stránku s velmi malým úsilím:

[![](overview/_static/image24.png)](overview/_static/image23.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>Vylepšení šablon stylů CSS

Jednou z hlavních oblastí práce v ASP.NET 4 bylo pomáhat s vykreslováním HTML, který je kompatibilní s nejnovějšími standardy HTML. To zahrnuje změny způsobu, jakým ovládací prvky webového serveru ASP.NET používají šablony stylů CSS.

#### <a name="compatibility-setting-for-rendering"></a>Nastavení kompatibility pro vykreslování

Ve výchozím nastavení platí, že pokud webová aplikace nebo web cílí na .NET Framework 4, atribut *controlRenderingCompatibilityVersion* elementu *Pages* je nastaven na hodnotu "4,0". Tento prvek je definovaný v souboru `Web.config` na úrovni počítače a ve výchozím nastavení se vztahuje na všechny aplikace ASP.NET 4:

[!code-xml[Main](overview/samples/sample69.xml)]

Hodnota pro *controlRenderingCompatibility* je řetězec, který umožňuje v budoucích verzích povolit nové definice verzí. V aktuální verzi jsou pro tuto vlastnost podporovány následující hodnoty:

- "3,5". Toto nastavení označuje starší verze vykreslování a značek. Značky vykreslené ovládacími prvky jsou 100% zpětně kompatibilní a nastavení vlastnosti *xhtmlConformance* je dodrženo.
- "4,0". Pokud má vlastnost toto nastavení, ovládací prvky webového serveru ASP.NET:
- Vlastnost *xhtmlConformance* je vždy považována za "Strict". V důsledku toho ovládací prvky vykreslují striktní značky XHTML 1,0.
- Zákaz nevstupních ovládacích prvků již nevykresluje neplatné styly.
- prvky *div* kolem skrytých polí jsou nyní ve stylu, takže nekolidují s uživatelem vytvořenými pravidly šablon stylů CSS.
- Ovládací prvky nabídky vykreslují kód, který je sémanticky správný a dodržuje pokyny pro usnadnění přístupu.
- Ovládací prvky ověřování nevykreslují vložené styly.
- Ovládací prvky, které dříve vykreslily Border = "0" (ovládací prvky, které jsou odvozeny z ovládacího prvku *tabulka* ASP.NET a ovládací prvek *Obrázek* ASP.NET) již tento atribut nevykreslí.

#### <a name="disabling-controls"></a>Zakázání ovládacích prvků

V ASP.NET 3,5 SP1 a starších verzích rozhraní vykresluje atribut *disabled* v kódu HTML pro všechny ovládací prvky, jejichž vlastnost *Enabled* je nastavena na *hodnotu false*. V souladu se specifikací HTML 4,01 by však měl mít tento atribut pouze *vstupní* prvky.

V ASP.NET 4 můžete nastavit vlastnost *controlRenderingCompatibilityVersion* na hodnotu "3,5", jak je znázorněno v následujícím příkladu:

[!code-xml[Main](overview/samples/sample70.xml)]

Můžete vytvořit značku pro ovládací prvek *popisek* , jako je následující, což zakáže ovládací prvek:

[!code-aspx[Main](overview/samples/sample71.aspx)]

Ovládací prvek *popisek* by vykresluje následující kód HTML:

[!code-html[Main](overview/samples/sample72.html)]

V ASP.NET 4 můžete nastavit *controlRenderingCompatibilityVersion* na "4,0". V takovém případě pouze ovládací prvky, které vykreslují *vstupní* prvky, vykreslí atribut *disabled* , pokud je vlastnost *Enabled* ovládacího prvku nastavena na *hodnotu false*. Ovládací prvky, které nevykreslují *vstupní* prvky HTML, vykreslí atribut *třídy* , který odkazuje na třídu šablony stylů CSS, kterou lze použít k definování zakázaného vzhledu ovládacího prvku. Například ovládací prvek *popisku* zobrazený v předchozím příkladu by generoval následující kód:

[!code-html[Main](overview/samples/sample73.html)]

Výchozí hodnota pro třídu, která je určená pro tento ovládací prvek, je "aspNetDisabled". Tuto výchozí hodnotu však můžete změnit nastavením statické vlastnosti static *DisabledCssClass* třídy *WebControl* . Pro vývojáře ovládacích prvků lze chování použít pro konkrétní ovládací prvek také definovat pomocí vlastnosti *SupportsDisabledAttribute* .

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>Skrytí prvků div kolem skrytých polí

ASP.NET 2,0 a novější verze vykreslí skrytá pole specifická pro systém (například *skrytý* element, který se používá k ukládání informací o stavu zobrazení) uvnitř elementu *div* , aby bylo možné dodržovat Standard XHTML. To však může způsobit problém, pokud pravidlo CSS ovlivňuje prvky *div* na stránce. Například může mít za následek, že se na stránce kolem skrytých prvků *div* zobrazí čára o velikosti 1 obr. V ASP.NET 4 prvky *div* , které obklopují skrytá pole vygenerovaná ASP.NET přidejte odkaz na třídu CSS jako v následujícím příkladu:

[!code-html[Main](overview/samples/sample74.html)]

Pak můžete definovat třídu šablony stylů CSS, která se vztahuje pouze na *skryté* prvky, které jsou generovány pomocí ASP.NET, jako v následujícím příkladu:

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>Vykreslení vnější tabulky pro ovládací prvky s šablonou

Ve výchozím nastavení následující ovládací prvky webového serveru ASP.NET, které podporují šablony, jsou automaticky zabaleny do vnější tabulky, která se používá k aplikování vložených stylů:

- *Třídě*
- *Hlas*
- *PasswordRecovery*
- *Metodu ChangePassword*
- *Tip*
- *Ovládacím CreateUserWizard*

Do těchto ovládacích prvků byla přidána nová vlastnost s názvem *RenderOuterTable* , která umožňuje odebrat vnější tabulku ze značky. Zvažte například následující příklad ovládacího prvku *FormView* :

[!code-aspx[Main](overview/samples/sample76.aspx)]

Tento kód vykresluje následující výstup na stránku, která obsahuje tabulku HTML:

[!code-html[Main](overview/samples/sample77.html)]

Chcete-li zabránit vykreslování tabulky, můžete nastavit vlastnost *RenderOuterTable* ovládacího prvku *FormView* , jak je uvedeno v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample78.aspx)]

Předchozí příklad vykreslí následující výstup bez elementů *Table*, *TR*a *td* :

> Obsah

Toto vylepšení může zjednodušit styl obsahu ovládacího prvku pomocí šablony stylů CSS, protože ovládací prvek nevykresluje žádné neočekávané značky.

> [!NOTE]
> Všimněte si, že tato změna zakazuje podporu pro funkci automatického formátování v návrháři sady Visual Studio 2010, protože již není element *Table* , který by mohl mít atributy stylu hostitele, které jsou generovány pomocí možnosti automatického formátu.

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>Vylepšení ovládacího prvku ListView

V ASP.NET 4 bylo snazší použít ovládací prvek *ListView* . V dřívější verzi ovládacího prvku je nutné zadat šablonu rozložení, která obsahovala serverový ovládací prvek se známým ID. Následující kód ukazuje typický příklad použití ovládacího prvku *ListView* v ASP.NET 3,5.

[!code-aspx[Main](overview/samples/sample79.aspx)]

V ASP.NET 4 ovládací prvek *ListView* nevyžaduje šablonu rozložení. Značka uvedená v předchozím příkladu může být nahrazena následujícím kódem:

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>Vylepšení ovládacího prvku CheckBoxList a RadioButtonList

V ASP.NET 3,5 můžete určit rozložení pro *CheckBoxList* a *RadioButtonList* pomocí následujících dvou nastavení:

- *Tok*. Ovládací prvek vykresluje prvky *span* tak, aby obsahoval jeho obsah.
- *Tabulka*: Ovládací prvek vykresluje prvek *tabulky* obsahující jeho obsah.

Následující příklad ukazuje značky pro každý z těchto ovládacích prvků.

[!code-aspx[Main](overview/samples/sample81.aspx)]

Ve výchozím nastavení vykreslují ovládací prvky HTML podobný následujícímu:

[!code-html[Main](overview/samples/sample82.html)]

Vzhledem k tomu, že tyto ovládací prvky obsahují seznamy položek, pro vykreslování sémantického správného formátu HTML, by měly vykreslovat jejich obsah pomocí prvků seznamu HTML (*li*). To usnadňuje uživatelům, kteří čtou webové stránky pomocí technologie pro usnadnění, a usnadňují používání ovládacích prvků stylu CSS.

V ASP.NET 4 podporují ovládací prvky *CheckBoxList* a *RadioButtonList* pro vlastnost *RepeatLayout ovládacího* následující nové hodnoty:

- *OrderedList* – obsah se vykresluje jako *li* element v rámci elementu *ol* .
- *Rozložení UnorderedList* – obsah se vykresluje jako *li* element v elementu *ul* .

Následující příklad ukazuje, jak použít tyto nové hodnoty.

[!code-aspx[Main](overview/samples/sample83.aspx)]

Předchozí kód generuje následující kód HTML:

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> Poznámka: Pokud nastavíte *RepeatLayout ovládacího* na *OrderedList* nebo *rozložení UnorderedList*, vlastnost *RepeatDirection* již nemůže být použita a v době běhu vyvolá výjimku, pokud byla vlastnost nastavena v rámci kódu nebo kódu. Vlastnost by neměl žádnou hodnotu, protože vizuální rozložení těchto ovládacích prvků je místo toho definováno pomocí šablony stylů CSS.

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>Vylepšení ovládacích prvků nabídky

Před ASP.NET 4 ovládací prvek *nabídky* vykreslil řadu tabulek HTML. To ztěžuje použití stylů CSS mimo nastavení vložených vlastností a také nedodržuje standardy přístupnosti.

V ASP.NET 4 ovládací prvek nyní vykresluje HTML pomocí sémantického kódu, který se skládá z neuspořádaného seznamu a prvků seznamu. Následující příklad ukazuje značky na stránce ASP.NET pro ovládací prvek *nabídky* .

[!code-aspx[Main](overview/samples/sample85.aspx)]

Když se stránka vykreslí, ovládací prvek vytvoří následující kód HTML (kód při *kliknutí* byl vynechán pro přehlednost):

[!code-html[Main](overview/samples/sample86.html)]

Kromě vylepšení vykreslování bylo vylepšena navigace pomocí klávesnice v nabídce s využitím správy fokusu. Když ovládací prvek *nabídky* získá fokus, můžete použít klávesy se šipkami k procházení prvků. Ovládací prvek *nabídky* teď také připojí přístupné role a atributy standardu ARIA (Rich Internet Applications)[a následují](http://www.w3.org/TR/wai-aria-practices/#menu "Pokyny pro ARIA v nabídce")vyhledá vylepšené možnosti usnadnění.

Styly pro ovládací prvek nabídky jsou vykreslovány v bloku stylu v horní části stránky, nikoli v řádku s vykreslenými prvky jazyka HTML. Pokud chcete mít plnou kontrolu nad stylem ovládacího prvku, můžete nastavit novou vlastnost *IncludeStyleBlock* na *hodnotu false*. v takovém případě není blok stylu vygenerován. Jedním ze způsobů, jak tuto vlastnost použít, je použít funkci automatického formátování v návrháři sady Visual Studio k nastavení vzhledu nabídky. Pak můžete spustit stránku, otevřít zdroj stránky a potom zkopírovat zavykreslený blok stylu do externího souboru CSS. V sadě Visual Studio vraťte styly zpět a nastavte *IncludeStyleBlock* na *false (NEPRAVDA*). Výsledkem je, že se vzhled nabídky definuje pomocí stylů v externí šabloně stylů.

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>Průvodce a ovládací prvky ovládacím CreateUserWizard

*Průvodce* ASP.NET a ovládací prvky *ovládacím CreateUserWizard* podporují šablony, které umožňují definovat kód HTML, který vykreslují. (*Ovládacím CreateUserWizard* se odvozuje od *Průvodce*.) Následující příklad ukazuje značku pro plně *ovládacím CreateUserWizard* ovládací prvek s šablonou:

[!code-aspx[Main](overview/samples/sample87.aspx)]

Ovládací prvek vykresluje kód HTML podobný následujícímu:

[!code-html[Main](overview/samples/sample88.html)]

V ASP.NET 3,5 SP1, i když můžete změnit obsah šablony, máte stále omezenou kontrolu nad výstupem ovládacího prvku *Průvodce* . V ASP.NET 4 můžete vytvořit šablonu šablony *LayoutTemplate* a vložit *zástupné* ovládací prvky (pomocí rezervovaných názvů) a určit tak, jak chcete, aby se *ovládací prvek Průvodce* vykreslil. Následující příklad ukazuje:

[!code-aspx[Main](overview/samples/sample89.aspx)]

Příklad obsahuje následující pojmenované zástupné symboly v elementu *LayoutTemplate* :

- *headerPlaceholder* – v době běhu je toto nahrazeno obsahem elementu *Šablona HeaderTemplate* .
- *sideBarPlaceholder* – v době běhu je toto nahrazeno obsahem elementu *oddíl SideBarTemplate* .
- *wizardStepPlaceHolder* – v době běhu je toto nahrazeno obsahem elementu *WizardStepTemplate* .
- *navigationPlaceholder* – v době běhu je tato nahrazena všemi navigačními šablonami, které jste definovali.

Označení v příkladu, který používá zástupné symboly, vykresluje následující HTML (bez obsahu, který je ve skutečnosti definovaný v šablonách):

[!code-html[Main](overview/samples/sample90.html)]

Jediný kód HTML, který není nyní definován uživatelem, je prvek *span* . (V budoucích verzích předpokládáme, že i element *span* nebude vykreslený.) Teď vám poskytne plnou kontrolu nad prakticky veškerým obsahem generovaným ovládacím prvkem *Průvodce* .

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC byla představena jako doplňková architektura pro ASP.NET 3,5 SP1 v březnu 2009. Visual Studio 2010 obsahuje ASP.NET MVC 2, který obsahuje nové funkce a možnosti.

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>Podpora oblastí

Oblasti umožňují seskupit řadiče a zobrazení do sekcí velké aplikace v relativní izolaci od ostatních oddílů. Každou oblast lze implementovat jako samostatný projekt ASP.NET MVC, na který může odkazovat hlavní aplikace. To pomáhá spravovat složitost při sestavování rozsáhlých aplikací a usnadňuje spolupráci více týmů v rámci jedné aplikace.

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>Podpora ověřování atributů poznámky k datům

Atributy *DataAnnotations* umožňují připojit logiku ověřování k modelu pomocí atributů metadat. V ASP.NET dynamických datech v ASP.NET 3,5 SP1 byly představeny atributy *DataAnnotations* . Tyto atributy byly integrovány do výchozího pořadače modelů a poskytují prostředky založené na metadatech pro ověření vstupu uživatele.

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>Pomocník s šablonami

Pomocníky s šablonou umožňují automaticky přidružit šablony pro úpravy a zobrazení s datovými typy. Například můžete použít pomocníka šablony k určení, že prvek uživatelského rozhraní pro výběr data je automaticky vykreslen pro hodnotu *System. DateTime* . To se podobá šablonám polí v dynamických datech ASP.NET.

Pomocné metody *HTML. EditorFor* a *HTML. DisplayFor* mají integrovanou podporu pro vykreslování standardních datových typů i pro komplexní objekty s více vlastnostmi. Také přizpůsobují vykreslování tím, že vám umožní použít pro objekt *ViewModel* atributy poznámek k datům, jako je *DisplayName* a *ScaffoldColumn* .

Často budete chtít výstup z pomocníků uživatelského rozhraní ještě více přizpůsobit a mít úplnou kontrolu nad tím, co je vygenerováno. Pomocné metody *HTML. EditorFor* a *HTML. DisplayFor* podporují tento mechanismus pomocí mechanismu šablonování, který umožňuje definovat externí šablony, které mohou přepsat a řídit výstup vykreslený. Šablony lze vykreslit jednotlivě pro třídu.

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dynamická data

Dynamická data byla představena ve verzi .NET Framework 3,5 SP1 v polovině 2008. Tato funkce poskytuje mnoho vylepšení pro vytváření aplikací založených na datech, včetně následujících:

- Prostředí RAD pro rychlé vytvoření webu založeného na datech.
- Automatické ověřování založené na omezeních definovaných v datovém modelu.
- Možnost snadné změny kódu, který je generován pro pole v ovládacích prvcích *GridView* a *DetailsView* pomocí šablon polí, které jsou součástí projektu dynamických dat.

> [!NOTE]
> Poznámka: Další informace naleznete v [dokumentaci k dynamickým datům](https://msdn.microsoft.com/library/cc488545.aspx) v knihovně MSDN.

U ASP.NET 4 se rozšířila dynamická data, která vývojářům ještě zvyšují výkon pro rychlé vytváření webů založených na datech.

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>Povolení dynamických dat pro existující projekty

Funkce dynamických dat, které byly dodávány ve službě .NET Framework 3,5 SP1, dostaly nové funkce, například následující:

- Šablony polí – tyto poskytují šablony založené na datových typech pro ovládací prvky vázané na data. Šablony polí poskytují jednodušší způsob, jak přizpůsobit vzhled ovládacích prvků dat než použití polí šablon pro každé pole.
- Ověřování – dynamická data umožňují používat atributy u datových tříd k určení ověřování pro běžné scénáře, jako jsou povinná pole, kontrola rozsahu, kontrola typu, porovnávání vzorů pomocí regulárních výrazů a vlastní ověřování. Ověřování je vynutilo ovládacími prvky dat.

Tyto funkce ale měly následující požadavky:

- Vrstva přístupu k datům měla být založená na Entity Framework nebo LINQ to SQL.
- Jediné ovládací prvky zdroje dat, které jsou podporovány pro tyto funkce, byly ovládací prvky *EntityDataSource* nebo *LinqDataSource* .
- Funkce vyžadovala webový projekt, který byl vytvořen pomocí šablon dynamických dat nebo dynamických datových entit, aby měly všechny soubory, které byly požadovány pro podporu funkce.

Hlavním cílem podpory dynamických dat v ASP.NET 4 je povolení nové funkce dynamických dat pro všechny aplikace ASP.NET. Následující příklad ukazuje značky pro ovládací prvky, které mohou využívat funkci dynamických dat na stávající stránce.

[!code-aspx[Main](overview/samples/sample91.aspx)]

V kódu stránky musí být přidán následující kód, aby bylo možné povolit podporu dynamických dat pro tyto ovládací prvky:

[!code-csharp[Main](overview/samples/sample92.cs)]

Když je ovládací prvek *GridView* v režimu úprav, dynamická data automaticky ověří, že zadaná data jsou ve správném formátu. Pokud není, zobrazí se chybová zpráva.

Tato funkce také poskytuje další výhody, jako je možnost zadat výchozí hodnoty pro režim vkládání. Bez dynamických dat, chcete-li implementovat výchozí hodnotu pro pole, je nutné se připojit k události, vyhledat ovládací prvek (pomocí *FindControl*) a nastavit jeho hodnotu. V ASP.NET 4 volání *EnableDynamicData* podporuje druhý parametr, který umožňuje předat výchozí hodnoty pro jakékoli pole objektu, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>Deklarativní syntaxe ovládacího prvku ovládacího prvku DynamicDataManager

Ovládací prvek *ovládacího prvku DynamicDataManager* byl vylepšen, takže jej lze nakonfigurovat deklarativně, jako u většiny ovládacích prvků v ASP.NET, namísto pouze v kódu. Označení ovládacího prvku *ovládacího prvku DynamicDataManager* vypadá jako v následujícím příkladu:

[!code-aspx[Main](overview/samples/sample94.aspx)]

Tento kód umožňuje dynamické chování dat pro ovládací prvek GridView1, na který je odkazováno v oddíle *DataControls* ovládacího prvku *ovládacího prvku DynamicDataManager* .

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>Šablony entit

Šablony entit nabízejí nový způsob přizpůsobení rozložení dat bez nutnosti vytvořit vlastní stránku. Šablony stránky používají ovládací prvek *FormView* (namísto ovládacího prvku *DetailsView* , jak je použit v šablonách stránky v dřívějších verzích dynamických dat) a ovládací prvek *DynamicEntity* pro vykreslení šablon entit. Tím získáte větší kontrolu nad značkou, která je vykreslena dynamickými daty.

Následující seznam zobrazuje nové rozložení adresáře projektu, které obsahuje šablony entit:

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate` adresář obsahuje šablony pro zobrazení objektů datového modelu. Ve výchozím nastavení jsou objekty vykreslovány pomocí šablony `Default.ascx`, která poskytuje značky, které vypadají stejně jako značky vytvořené ovládacím prvkem *DetailsView* používanými dynamickými daty v ASP.NET 3,5 SP1. Následující příklad ukazuje značku ovládacího prvku `Default.ascx`:

[!code-aspx[Main](overview/samples/sample96.aspx)]

Výchozí šablony lze upravit pro změnu vzhledu a chování celého webu. K dispozici jsou šablony pro operace zobrazení, úprav a vložení. Nové šablony lze přidat na základě názvu datového objektu, aby bylo možné změnit vzhled a chování pouze jednoho typu objektu. Můžete například přidat následující šablonu:

[!code-console[Main](overview/samples/sample97.cmd)]

Šablona může obsahovat následující kód:

[!code-aspx[Main](overview/samples/sample98.aspx)]

Nové šablony entit se zobrazí na stránce pomocí nového ovládacího prvku *DynamicEntity* . V době běhu je tento ovládací prvek nahrazen obsahem šablony entity. Následující kód ukazuje ovládací prvek *FormView* v šabloně stránky `Detail.aspx`, který používá šablonu entity. Všimněte si, že element *DynamicEntity* ve značce.

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>Nové šablony polí pro adresy URL a e-mailové adresy

ASP.NET 4 zavádí dvě nové předdefinované šablony polí `EmailAddress.ascx` a `Url.ascx`. Tyto šablony jsou používány pro pole, která jsou označena jako *EmailAddress* nebo *URL* s atributem *DataType* . Pro objekty *EmailAddress* se pole zobrazí jako hypertextový odkaz, který je vytvořen pomocí protokolu *mailto:* . Když uživatel klikne na odkaz, otevře se e-mailový klient uživatele a vytvoří kostru zprávy. Objekty, které jsou zadány jako *URL* , se zobrazují jako běžné hypertextové odkazy.

Následující příklad ukazuje, jak budou označena pole.

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>Vytváření odkazů pomocí ovládacího prvku ovládací DynamicHyperLink

Dynamická data používají novou funkci směrování, která byla přidána v .NET Framework 3,5 SP1 pro řízení adres URL, které koncoví uživatelé uvidí při přístupu k webu. Nový ovládací prvek *ovládací DynamicHyperLink* usnadňuje vytváření odkazů na stránky v dynamickém datovém webu. Následující příklad ukazuje, jak použít ovládací prvek *ovládací DynamicHyperLink* :

[!code-aspx[Main](overview/samples/sample101.aspx)]

Tento kód vytvoří odkaz, který odkazuje na stránku seznamu pro `Products` tabulku na základě tras, které jsou definovány v souboru `Global.asax`. Ovládací prvek automaticky používá výchozí název tabulky, na kterém je založena stránka dynamická data.

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>Podpora dědičnosti v datovém modelu

Entity Framework i LINQ to SQL podporují dědičnost ve svých datových modelech. Příkladem může být databáze s `InsurancePolicy` tabulkou. Může také obsahovat `CarPolicy` a `HousePolicy` tabulky, které mají stejná pole jako `InsurancePolicy` a pak přidat další pole. Byla změněna dynamická data, aby bylo možné pochopit zděděné objekty v datovém modelu a podporovat generování uživatelského rozhraní pro zděděné tabulky.

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>Podpora relací M:n (jenom Entity Framework)

Entity Framework má bohatou podporu pro relace m:n mezi tabulkami, které jsou implementovány vyvoláním relace jako kolekce objektu *entity* . Přidala se nová `ManyToMany.ascx` a `ManyToMany_Edit.ascx` šablony polí pro zajištění podpory pro zobrazování a úpravu dat, která jsou součástí vztahů m:n.

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>Nové atributy pro řízení zobrazení a podpory výčtů

Přidaný *DisplayAttribute* vám poskytne další kontrolu nad tím, jak se pole zobrazují. Atribut *DisplayName* v dřívějších verzích dynamických dat vám umožní změnit název, který se používá jako titulek pro pole. Nová třída *DisplayAttribute* vám umožňuje určit více možností pro zobrazení pole, například pořadí, ve kterém se pole zobrazuje, a informace o tom, jestli se pole použije jako filtr. Atribut také poskytuje nezávislé řízení názvu používaného pro popisky v ovládacím prvku *GridView* , název použitý v ovládacím prvku *DetailsView* , text v nápovědě pro pole a vodoznak, který se používá pro pole (Pokud pole akceptuje textový vstup).

Přidala se třída *atribut EnumDataTypeAttribute* , která umožňuje mapovat pole na výčty. Při použití tohoto atributu u pole zadáte typ výčtu. Dynamická data používají novou šablonu pole `Enumeration.ascx` k vytvoření uživatelského rozhraní pro zobrazení a úpravy hodnot výčtu. Šablona mapuje hodnoty z databáze na názvy ve výčtu.

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>Rozšířená podpora pro filtry

Dynamické datové 1,0 dodávané s integrovanými filtry pro logické sloupce a sloupce cizího klíče. Filtry neumožňují určit, zda byly zobrazeny nebo v jakém pořadí byly zobrazeny. Nový atribut *DisplayAttribute* řeší oba tyto problémy tím, že poskytuje kontrolu nad tím, zda se sloupec zobrazí jako filtr a v jakém pořadí bude zobrazen.

Dalším vylepšením je, že podpora filtrování byla znovu[vytvořena, aby používala novou](#0.2__QueryExtender "_QueryExtender") funkci webových formulářů. To vám umožní vytvořit filtry bez nutnosti znalosti ovládacího prvku zdroje dat, se kterými se filtry budou používat. Společně s těmito rozšířeními byly filtry také změněny na ovládací prvky šablon, což umožňuje přidat nové. Nakonec výše zmíněná třída *DisplayAttribute* umožňuje přepsat výchozí filtr stejným způsobem, jakým *UIHint* umožňuje přepsat výchozí šablonu pole pro sloupec.

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Vylepšení vývoje webu sady Visual Studio 2010

Vývoj pro web v aplikaci Visual Studio 2010 byl vylepšen pro větší kompatibilitu šablon stylů CSS, zvýšení produktivity pomocí HTML a ASP.NET fragmentů kódu a nového dynamického JavaScriptu jazyka IntelliSense.

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>Vylepšená kompatibilita šablon stylů CSS

Návrhář aplikace Visual Web Developer v aplikaci Visual Studio 2010 byl aktualizován pro zlepšení dodržování standardů šablon stylů CSS 2,1. Návrhář lépe zachovává integritu zdroje HTML a je robustnější než v předchozích verzích sady Visual Studio. V rámci digestoře se také provedla vylepšení architektury, která budou lépe umožňovat budoucí vylepšení vykreslování, rozložení a služby.

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>Fragmenty kódu HTML a JavaScriptu

V editoru HTML technologie IntelliSense automaticky dokončuje názvy značek. Funkce fragmentů technologie IntelliSense automaticky dokončuje celé značky a další. V aplikaci Visual Studio 2010 jsou fragmenty technologie IntelliSense podporovány pro JavaScript, C# společně a Visual Basic, které byly podporovány v dřívějších verzích sady Visual Studio.

Visual Studio 2010 obsahuje více než 200 fragmentů kódu, které vám pomůžou s automatickým dokončováním běžných značek ASP.NET a HTML, včetně požadovaných atributů (například runat = "Server") a společných atributů specifických pro značku (například *ID*, *DataSourceID*, *ControlToValidate*a *text*).

Můžete stáhnout další fragmenty kódu nebo můžete napsat vlastní fragmenty, které zapouzdřují bloky kódu, které vy nebo váš tým používáte pro běžné úkoly.

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>Vylepšení JavaScript IntelliSense

V jazyce Visual 2010 byla přepracována technologie JavaScript IntelliSense, aby poskytovala ještě bohatší možnosti úprav. Technologie IntelliSense nyní rozpoznává objekty, které byly dynamicky generovány metodami, jako je například *registerNamespace* , a podobnými technikami, které používá jiné rozhraní JavaScript. Vylepšili jsme výkon při analýze velkých knihoven skriptů a zobrazení IntelliSense s malým nebo žádným zpožděním zpracování. Kompatibilita se významně zvýšila, aby podporovala skoro všechny knihovny třetích stran a podporovaly různé styly kódování. Dokumentační komentáře jsou nyní analyzovány při psaní a jsou okamžitě využity technologií IntelliSense.

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>Nasazení webové aplikace pomocí sady Visual Studio 2010

Když vývojáři ASP.NET nasadí webovou aplikaci, často zjistí, že narazí na následující problémy:

- Nasazení do sdíleného hostitelského serveru vyžaduje technologie, jako je FTP, což může být pomalé. Kromě toho je nutné ručně provést úlohy, jako je spouštění skriptů SQL pro konfiguraci databáze, a je třeba změnit nastavení služby IIS, jako je například konfigurace složky virtuálního adresáře jako aplikace.
- V podnikovém prostředí musí správci kromě nasazení souborů webové aplikace často upravovat konfigurační soubory ASP.NET a nastavení služby IIS. Správci databáze musí spustit sérii skriptů SQL pro získání databáze aplikace. Takové instalace jsou náročné na práci, ale jsou často hodiny dokončené a je nutné je pečlivě zdokumentovat.

Visual Studio 2010 obsahuje technologie, které řeší tyto problémy a umožňují bezproblémové nasazení webových aplikací. Jednou z těchto technologií je nástroj pro nasazení webu služby IIS (MsDeploy. exe).

Funkce pro nasazení webu v aplikaci Visual Studio 2010 obsahují následující hlavní oblasti:

- Balíčky webu
- Transformace Web. config
- Nasazení databáze
- Publikování jedním kliknutím pro webové aplikace

Následující části obsahují podrobné informace o těchto funkcích.

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>Balíčky webu

Sada Visual Studio 2010 používá nástroj MSDeploy k vytvoření komprimovaného souboru (. zip) pro vaši aplikaci, který se označuje jako *webový balíček*. Soubor balíčku obsahuje metadata o vaší aplikaci a následující obsah:

- Nastavení služby IIS, které zahrnuje nastavení fondu aplikací, nastavení chybových stránek atd.
- Skutečný webový obsah, který zahrnuje webové stránky, uživatelské ovládací prvky, statický obsah (obrázky a soubory HTML) atd.
- SQL Server schémat a dat databáze.
- Certifikáty zabezpečení, součásti k instalaci v globální mezipaměti sestavení (GAC), nastavení registru atd.

Webový balíček můžete zkopírovat na libovolný server a pak ho nainstalovat ručně pomocí Správce služby IIS. Případně pro automatizované nasazení lze balíček nainstalovat pomocí příkazů příkazového řádku nebo pomocí rozhraní API pro nasazení.

Visual Studio 2010 poskytuje předdefinované úlohy a cíle nástroje MSBuild pro vytváření webových balíčků. Další informace najdete v tématu [Přehled nasazení projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) na webu MSDN a [10 + 20 důvodů, proč byste měli vytvořit webový balíček](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) na blogu Vishal Joshi.

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Transformace Web. config

V případě nasazení webové aplikace Visual Studio 2010 zavádí [XML Document Transforming (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), což je funkce, která umožňuje transformovat `Web.config` soubor z nastavení pro vývoj na produkční nastavení. Nastavení transformace jsou určena v transformačních souborech s názvem `web.debug.config`, `web.release.config`a tak dále. (Názvy těchto souborů odpovídají konfiguracím MSBuild.) Transformační soubor obsahuje pouze změny, které je třeba provést v nasazeném souboru `Web.config`. Změny se určují pomocí jednoduché syntaxe.

Následující příklad ukazuje část `web.release.config` souboru, který může být vytvořen pro nasazení konfigurace vydané verze. Klíčové slovo Replace v příkladu určuje, že během nasazování bude uzel *ConnectionString* v souboru `Web.config` nahrazen hodnotami uvedenými v příkladu.

[!code-xml[Main](overview/samples/sample102.xml)]

Další informace naleznete v tématu [Syntaxe transformace Web. config pro nasazení projektu webové aplikace](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) na webu MSDN <a id="0.2_a"></a> a[nasazení webu: transformace Web. config](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) na blogu Vishal Joshi.

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>Nasazení databáze

Balíček pro nasazení sady Visual Studio 2010 může zahrnovat závislosti na databázích SQL Server. V rámci definice balíčku zadejte připojovací řetězec pro zdrojovou databázi. Při vytváření webového balíčku vytvoří Visual Studio 2010 skripty SQL pro schéma databáze a volitelně data a přidá je do balíčku. Můžete také zadat vlastní skripty SQL a určit pořadí, ve kterém by se měly spouštět na serveru. V okamžiku nasazení zadejte připojovací řetězec, který je vhodný pro cílový server. proces nasazení pak pomocí tohoto připojovacího řetězce spustí skripty, které vytvářejí schéma databáze a data přidávají.

Kromě toho můžete pomocí publikování jedním kliknutím nakonfigurovat nasazení pro publikování databáze přímo při publikování aplikace na vzdálené sdílené hostitelské lokalitě. Další informace najdete v tématu [Postup: nasazení databáze pomocí projektu webové aplikace](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) na webu MSDN a [nasazení databáze s vs 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) na blogu Vishal Joshi.

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>Publikování jedním kliknutím pro webové aplikace

Visual Studio 2010 také umožňuje používat službu IIS Remote Management Service k publikování webové aplikace na vzdáleném serveru. Můžete vytvořit profil publikování pro svůj hostitelský účet nebo pro testovací servery nebo pracovní servery. Každý profil může bezpečně ukládat příslušné přihlašovací údaje. Pak můžete nasadit na libovolný cílový server jedním kliknutím pomocí panelu nástrojů pro publikování na webu jedním kliknutím. Pomocí sady Visual Studio 2010 můžete také publikovat pomocí příkazového řádku MSBuild. To vám umožní nakonfigurovat prostředí týmu sestavení tak, aby zahrnovalo publikování v modelu průběžné integrace.

Další informace najdete v tématu [Postup: nasazení projektu webové aplikace pomocí publikování jedním kliknutím a nasazení webu](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) na webu MSDN a v části [Web 1 – klikněte na publikovat v sadě vs 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) na blogu pro Vishal Joshi. Chcete-li zobrazit video prezentace týkající se nasazení webové aplikace v sadě Visual Studio 2010, přečtěte si téma [VS 2010 pro webové verze Developer](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) Preview na blogu Vishal Joshi.

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>Prostředky

Následující weby poskytují další informace o ASP.NET 4 a Visual Studio 2010.

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) – oficiální dokumentace pro ASP.NET 4 na webu MSDN.
- [https://www.asp.net/](https://www.asp.net/) – vlastní web týmu ASP.NET.
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) a [ASP.NET se mapa obsahu dynamických dat](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) – online prostředky na týmovém webu ASP.NET a v oficiální dokumentaci pro ASP.NET dynamická data.
- [https://www.asp.net/ajax/](../../ajax/index.md) – hlavní webový prostředek pro vývoj v ASP.NET AJAX.
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) – Blog týmu Visual Web Developer, který obsahuje informace o funkcích sady Visual Studio 2010.
- [ASP.NET webstack](https://github.com/aspnet/AspNetWebStack) – hlavní webový prostředek pro verzi preview verze ASP.NET.

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>Právní omezení

Toto je předběžný dokument a může být podstatně měněn před konečným komerčním vydáním softwaru popsaného v tomto dokumentu.

Informace obsažené v tomto dokumentu představují aktuální pohled společnosti Microsoft Corporation na problémy, které jsou popsány k datu publikování. Vzhledem k tomu, že Microsoft musí reagovat na měnící se podmínky na trhu, neměl by být interpretován jako závazek společnosti Microsoft a společnost Microsoft nemůže zaručit přesnost všech informací, které jsou uvedeny po datu publikování.

Tento dokument White Paper slouží pouze k informativním účelům. SPOLEČNOST MICROSOFT NEPOSKYTUJE ŽÁDNÉ ZÁRUKY, AŤ UŽ VÝSLOVNĚ UVEDENÉ, PŘEDPOKLÁDANÉ NEBO STATUTÁRNÍ, JAKO INFORMACE V TOMTO DOKUMENTU.

Dodržování všech platných zákonů o autorských právech je zodpovědností uživatele. Bez omezení práv v rámci autorského práva nesmí být žádná část tohoto dokumentu reprodukována, ukládána do systému pro načítání nebo převedena v jakémkoli tvaru nebo jakýmkoli prostředkem (elektronickými, mechanicky, fotokopírováním, záznamem nebo jiným) nebo pro jakékoli účely. bez výslovného písemného svolení společnosti Microsoft Corporation.

Společnost Microsoft může mít patenty, patentové aplikace, ochranné známky, autorská práva nebo jiná práva duševního vlastnictví, která zahrnují předmět v tomto dokumentu. S výjimkou výslovně uvedených v písemné licenční smlouvě od společnosti Microsoft vám poskytnutí tohoto dokumentu neposkytuje žádnou licenci na tyto patenty, ochranné známky, autorská práva ani jiné duševní vlastnictví.

Pokud není uvedeno jinak, jsou ukázkové společnosti, organizace, produkty, názvy domén, e-mailové adresy, loga, osoby, místa a události uvedené v ukázkách smyšlené a bez jakýchkoli souvislostí se skutečnou společností, organizací, produktem, názvem domény, e-mailem. adresa, logo, osoba, místo nebo událost jsou zamýšlené nebo by se měly odvodit.

© 2009 Microsoft Corporation. Všechna práva vyhrazena.

Microsoft a Windows jsou buď registrované ochranné známky, nebo ochranné známky společnosti Microsoft Corporation v USA a dalších zemích.

Názvy skutečných společností a produktů uvedených v tomto dokumentu můžou být ochranné známky jejich příslušných vlastníků.
