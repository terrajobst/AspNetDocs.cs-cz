---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: Globální zpracování chyb v ASP.NET webového rozhraní API 2 – ASP.NET 4. x
author: davidmatson
description: Přehled globálních zpracování chyb v ASP.NET Web API 2 pro ASP.NET 4. x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 94f2d6d31d0b37f9bb0077e6258c70a2dfb1918d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457736"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>Globální zpracování chyb v ASP.NET webového rozhraní API 2

autorem [David Matson](https://github.com/davidmatson), [Rick Anderson](https://twitter.com/RickAndMSFT)

V tomto tématu najdete přehled globálních zpracování chyb v ASP.NET Web API 2 pro ASP.NET 4. x. Dnes ve webovém rozhraní API neexistuje jednoduchý způsob, jak protokolovat nebo nakládat chyby globálně. Některé neošetřené výjimky lze zpracovat prostřednictvím [filtrů výjimek](exception-handling.md), ale existuje několik případů, kdy filtry výjimek nemůžou zpracovat. Příklad:

1. Výjimky vyvolané z konstruktorů kontroleru.
2. Výjimky vyvolané z obslužných rutin zpráv
3. Během směrování byly vyvolány výjimky.
4. Výjimky vyvolané při serializaci obsahu odpovědi

Chceme poskytnout jednoduchý a konzistentní způsob, jak protokolovat a zpracovávat (kde je to možné) tyto výjimky. 

Existují dva hlavní případy pro zpracování výjimek, případ, kdy je možné odeslat chybovou odpověď, a případ, kdy můžeme udělat výjimku, se zaznamená výjimka. Příkladem pro druhý případ je výjimka, která je vyvolána ve středu obsahu odpovědi streamování; v takovém případě je příliš pozdě poslat novou zprávu s odpovědí, protože stavový kód, hlavičky a částečný obsah už jsou v rámci sítě, takže jsme připojení jednoduše přerušili. I když výjimku nejde zpracovat, aby vytvořila novou zprávu odpovědi, pořád podporuje protokolování výjimky. V případech, kdy můžeme zjistit chybu, můžeme vrátit příslušnou chybovou odpověď, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>Existující možnosti

Kromě [filtrů výjimek](exception-handling.md)se teď dají [obslužné rutiny zpráv](../advanced/http-message-handlers.md) používat dnes ke sledování všech odpovědí na úrovni 500, ale na těchto odpovědích jsou obtížné, protože nemají kontext o původní chybě. Obslužné rutiny zpráv mají také některá z stejných omezení jako filtry výjimek týkajících se případů, které mohou zpracovat. Webové rozhraní API sice má infrastrukturu trasování, která zachycuje chybové stavy. Tato trasovací infrastruktura je určená pro účely diagnostiky a není navržená ani vhodná pro provoz v produkčních prostředích. Globální zpracování výjimek a protokolování by mělo být služby, které mohou běžet během výroby a musí být zapojeny do stávajících řešení monitorování (například [knihovny elmah](https://code.google.com/p/elmah/) ).

### <a name="solution-overview"></a>Přehled řešení

 Poskytujeme dvě nové uživatelsky nahraditelné služby, [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) a IExceptionHandler pro protokolování a zpracování neošetřených výjimek. Služby jsou velmi podobné a mají dvě hlavní rozdíly:

1. Podporujeme registraci více protokolovacích protokolovacích nástrojů, ale jenom jednu obslužnou rutinu výjimky.
2. Protokolovací nástroje výjimky se vždy zavolají, i když se chystáme připojení přerušit. Obslužné rutiny výjimek se volají pouze v případě, že stále dokážeme zvolit, která odpověď se má odeslat.

Obě služby poskytují přístup ke kontextu výjimek, který obsahuje relevantní informace z místa, kde byla výjimka zjištěna, zejména [zprávy HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), vyvolaná výjimka a zdroj výjimky (podrobnosti níže).

### <a name="design-principles"></a>Principy návrhu

1. **Žádné neprůlomové změny** Vzhledem k tomu, že se tato funkce přidává v dílčí verzi, jedno důležité omezení, které ovlivňuje řešení, znamená, že nedochází k žádným nepodstatným změnám, a to ani k typu kontraktů nebo chování. Toto omezení vyvolalo nějaké vyčištění, které bychom chtěli udělat v souvislosti s existujícími bloky catch, které zapíná výjimky na 500 odpovědí. Toto dodatečné vyčištění je možné zvážit pro další hlavní vydání. Pokud je to pro vás důležité, můžete na něj hlasovat na [uživatelském hlasu ASP.NET webového rozhraní API](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception).
2. **Zachování konzistence pomocí konstrukcí webového rozhraní API** Kanál filtru webového rozhraní API je skvělým způsobem, jak zpracovávat problémy zaměřené na průřez a flexibilitu při použití logiky v oboru specifickém pro konkrétní akci, na konkrétního řadiče nebo na globálním rozsahu. Filtry, včetně filtrů výjimek, vždy mají kontexty Action a Controller i v případě, že jsou registrovány v globálním oboru. Tato smlouva dává smysl pro filtry, ale znamená, že filtry výjimek, dokonce i globálně vymezené, nejsou vhodné pro některé případy zpracování výjimek, jako jsou výjimky z obslužných rutin zpráv, kde neexistuje žádná akce nebo kontext kontroleru. Pokud chceme použít flexibilní rozsah poskytovaný filtry pro zpracování výjimek, pořád potřebujeme filtry výjimek. Pokud ale potřebujeme zpracovat výjimku mimo kontext kontroleru, potřebujeme také samostatnou konstrukci pro úplné zpracování globálních chyb (něco bez kontextu kontroleru a omezení kontextu akce).

### <a name="when-to-use"></a>Kdy použít

- Protokolovací nástroje jsou řešením pro zobrazení všech neošetřených výjimek zachycených webovým rozhraním API.
- Obslužné rutiny výjimek představují řešení pro přizpůsobení všech možných odpovědí na neošetřené výjimky zachycené webovým rozhraním API.
- Filtry výjimek jsou nejjednodušší řešení pro zpracování podmnožiny neošetřených výjimek týkajících se konkrétní akce nebo kontroleru.

### <a name="service-details"></a>Podrobnosti služby

 Protokolovací nástroj výjimky a rozhraní obslužných rutin jsou jednoduché asynchronní metody, které přebírají příslušné kontexty: 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 Poskytujeme také základní třídy pro obě tato rozhraní. Přepsání základních (synchronizovaných nebo asynchronních) metod se vyžaduje pro protokolování a zpracování v doporučených časech. Pro protokolování `ExceptionLogger` základní třída zaručí, že základní metoda protokolování je volána pouze jednou pro každou výjimku (i v případě, že je později šíří do dalšího zásobníku volání a je znovu zachycena). Základní třída `ExceptionHandler` zavolá metodu zpracování jádra pouze pro výjimky v horní části zásobníku volání a ignoruje staré vnořené bloky catch. (Zjednodušené verze těchto základních tříd jsou uvedené v příloze níže.) `IExceptionLogger` i `IExceptionHandler` přijímají informace o výjimce prostřednictvím `ExceptionContext`.

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

Když rozhraní volá protokolovací nástroj výjimky nebo obslužnou rutinu výjimky, vždy poskytne `Exception` a `Request`. S výjimkou testování částí také vždy poskytne `RequestContext`. V takovém případě se neposkytne `ControllerContext` a `ActionContext` (pouze při volání z bloku catch pro filtry výjimek). Při pokusu o zápis odpovědi bude velmi zřídka poskytovat `Response`(pouze v některých případech služby IIS). Vzhledem k tomu, že některé z těchto vlastností mohou být `null` je až příjemce, aby před přístupem ke členům třídy Exception kontroloval `null`.`CatchBlock` je řetězec, který označuje, který blok catch viděli výjimku. Řetězce bloku catch jsou následující:

- HttpServer (metoda SendAsync)
- HttpControllerDispatcher (metoda SendAsync)
- HttpBatchHandler (metoda SendAsync)
- IExceptionFilter (zpracování kanálu filtru výjimek v metody ExecuteAsync) (ApiController)
- OWIN hostitel:

    - HttpMessageHandlerAdapter. BufferResponseContentAsync (pro výstup do vyrovnávací paměti)
    - HttpMessageHandlerAdapter. CopyResponseContentAsync (pro výstup streamování)
- Webový hostitel:

    - HttpControllerHandler. WriteBufferedResponseContentAsync (pro výstup do vyrovnávací paměti)
    - HttpControllerHandler. WriteStreamedResponseContentAsync (pro výstup streamování)
    - HttpControllerHandler. WriteErrorResponseContentAsync (selhání při zotavení po chybě v režimu výstupu do vyrovnávací paměti)

Seznam řetězců bloku catch je také k dispozici prostřednictvím statických vlastností jen pro čtení. (Základní řetězec bloku catch je na statickém ExceptionCatchBlocks; zbytek se zobrazí na jedné statické třídě pro OWIN a webový hostitel).`IsTopLevelCatchBlock` je vhodný pro následující vzor zpracování výjimek pouze v horní části zásobníku volání. Namísto zapínání výjimek na 500 odpovědí kdekoli dojde k vnořenému bloku catch, obslužná rutina výjimky může umožnit šíření výjimek, dokud nebudou na hostiteli vidět.

Kromě `ExceptionContext`načítá protokolovací nástroj Další informace prostřednictvím úplné `ExceptionLoggerContext`:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

Druhá vlastnost, `CanBeHandled`, umožňuje protokolovacímu nástroje identifikovat výjimku, kterou nelze zpracovat. Když bude připojení přerušeno a nebude možné odeslat žádnou novou zprávu odpovědi, budou volány protokolovací nástroje, ale obslužná rutina ***nebude volána*** a protokolovací nástroje mohou tento scénář identifikovat z této vlastnosti.

Vedle `ExceptionContext`obslužná rutina získá jednu vlastnost, která může být nastavena na plný `ExceptionHandlerContext` pro zpracování výjimky:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

Obslužná rutina výjimky označuje, že byla zpracována výjimka nastavením vlastnosti `Result` na výsledek akce (například [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)nebo vlastní výsledek). Pokud má vlastnost `Result` hodnotu null, výjimka je neošetřená a původní výjimka bude znovu vyvolána.

Pro výjimky v horní části zásobníku volání jsme zavedli dodatečný krok, který zaručí, že odpověď je vhodná pro volající rozhraní API. Pokud se výjimka rozšíří až na hostitele, volající by uvidí žlutou obrazovku smrti nebo jiné reakce na hostitele, což je obvykle HTML a ne obvykle vhodná odpověď na chybu rozhraní API. V těchto případech výsledek začíná mimo null a pouze v případě, že vlastní obslužná rutina výjimky ji nastaví zpět na `null` (neošetřený), bude výjimka rozšířena na hostitele. Nastavení `Result` `null` v takových případech může být užitečné pro dva scénáře:

1. OWIN hostované webové rozhraní API s vlastními zpracováním výjimek registrovanými před nebo mimo webové rozhraní API.
2. Místní ladění prostřednictvím prohlížeče, kde žlutá obrazovka smrti je vlastně užitečnou odezvou na neošetřenou výjimku.

V případě protokolovacích nástrojů výjimek a obslužných rutin výjimek neuděláme nic k obnovení, pokud obslužná rutina nebo obslužná rutina sám vyvolá výjimku. (Jiné než umožnění šíření výjimky, pokud máte lepší přístup, zachovejte zpětnou vazbu na konci této stránky.) Kontrakt pro protokolovací nástroje a obslužné rutiny výjimek je, že by neměly umožnit šíření výjimek do jejich volajících; v opačném případě se výjimka rozšíří jenom na hostitele, což by vedlo k chybě HTML (jako je ASP. Žlutá obrazovka netto), která se odesílá zpátky klientovi (což obvykle není upřednostňovanou možností pro volající rozhraní API, které očekávají JSON nebo XML).

## <a name="examples"></a>Příklady

### <a name="tracing-exception-logger"></a>Protokolovací nástroj pro trasování výjimek

Protokolovací nástroj výjimky níže odesílá data výjimky do konfigurovaných zdrojů trasování (včetně okna výstup ladění v aplikaci Visual Studio).

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>Obslužná rutina výjimky vlastní chybové zprávy

Následující obrázek vytvoří vlastní chybovou odpověď pro klienty, včetně e-mailové adresy pro kontaktování podpory.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>Registrace filtrů výjimek

Pokud k vytvoření projektu použijete šablonu projektu webová aplikace ASP.NET MVC 4, vložte svůj konfigurační kód webového rozhraní API do třídy `WebApiConfig` ve složce *App/_Start* :

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>Příloha: podrobnosti základní třídy

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
