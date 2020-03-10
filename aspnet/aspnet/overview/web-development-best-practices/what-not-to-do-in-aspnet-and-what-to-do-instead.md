---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: Co dělat v ASP.NET a co dělat místo | Microsoft Docs
author: Rick-Anderson
description: Toto téma popisuje několik běžných chyb, které uživatelé provedou v rámci ASP.NET webových projektů. Poskytuje doporučení k tomu, abyste se vyhnuli těmto commo...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616989"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a>Co nedělat v ASP.NET a jak to udělat správně

> Toto téma popisuje několik běžných chyb, které uživatelé provedou v rámci ASP.NET webových projektů. Poskytuje doporučení k tomu, co byste měli udělat, abyste se vyhnuli těmto běžným chybám. Je založen na [prezentaci](http://vimeo.com/68390507) , kterou **Damian Edwards** na konferenci norských vývojářů.

## <a name="disclaimer"></a>Právní omezení

Toto téma není určené jako kompletní příručka, která zajišťuje zabezpečení a efektivitu aplikace. Stále je nutné dodržovat osvědčené postupy pro zabezpečení a výkon, které nejsou popsanými v tomto tématu. Navrhuje jenom to, jak se vyhnout běžným chybám souvisejícím s třídami a procesy .NET.

## <a name="overview"></a>Přehled

Toto téma obsahuje následující oddíly:

- [Dodržování standardů](#standards)

    - [Adaptéry ovládacích prvků](#adapters)
    - [Vlastnosti stylu u ovládacích prvků](#styleprop)
    - [Zpětná volání stránek a ovládacích prvků](#callback)
    - [Detekce schopností prohlížeče](#browsercap)
- [Zabezpečení](#security)

    - [Žádost o ověření](#validation)
    - [Ověřování a relace bez souborů cookie](#cookieless)
    - [EnableViewStateMac](#viewstatemac)
    - [Střední důvěryhodnost](#medium)
    - [&lt;appSettings&gt;](#appsettings)
    - [UrlPathEncode](#urlpathencode)
- [Spolehlivost a výkon](#performance)

    - [PreSendRequestHeaders a PreSendRequestContent](#presend)
    - [Asynchronní události stránky s webovými formuláři](#asyncevents)
    - [Práce s požárem a zapomenoutm](#fire)
    - [Tělo entity žádosti](#requestentity)
    - [Response. Redirect a Response. end](#redirect)
    - [EnableViewState a ViewStateMode](#viewstatemode)
    - [SqlMembershipProvider](#sqlprovider)
    - [Dlouho běžící požadavky (> 110 sekund)](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a>Dodržování standardů

<a id="adapters"></a>

### <a name="control-adapters"></a>Adaptéry ovládacích prvků

Doporučení: Ukončete používání adaptérů ovládacích prvků pro adaptivní vykreslování a místo toho používejte dotazy na média CSS a standardy HTML kompatibilní s normami.

Ovládací prvky adaptérů byly představeny v rozhraní .NET 2,0 pro vykreslování kódu prezentace, který byl přizpůsoben pro různá zařízení a prostředí. Nyní lze adaptivní vykreslování provést pomocí šablon stylů CSS a HTML. Měli byste ukončit používání adaptérů ovládacích prvků a převést všechny existující adaptéry na šablony stylů CSS a HTML.

Další informace najdete v tématech [dotazy na média](http://www.w3.org/TR/css3-mediaqueries/) a [Postupy: Přidání mobilních stránek do webových formulářů ASP.NET/aplikace MVC](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a>Vlastnosti stylu u ovládacích prvků

Doporučení: zastaví nastavení hodnot stylu v označení ovládacího prvku a místo toho nastaví hodnoty formátování v šablonách stylů CSS.

Ovládací prvky webového serveru obsahují desítky vlastností, které lze použít k nastavení vlastností vloženého stylu. Například vlastnost ForeColor nastavuje barvu textu ovládacího prvku. Stejný efekt můžete dosáhnout efektivněji prostřednictvím šablon stylů CSS. Šablony stylů umožňují centralizovat hodnoty stylu a vyhnout se nastavování těchto hodnot v celé aplikaci.

Následující příklad ukazuje třídu šablony stylů CSS, která nastaví text na červenou.

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

Následující příklad ukazuje, jak dynamicky použít třídu CSS.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a>Zpětná volání stránek a ovládacích prvků

Doporučení: Ukončete používání zpětných volání stránek a ovládacích prvků a místo toho použijte některý z následujících postupů: AJAX, UpdatePanel, MVC Methods, Web API nebo Signal.

V dřívějších verzích ASP.NET metody zpětného volání stránky a ovládacího prvku umožňují aktualizovat část webové stránky bez aktualizace celé stránky. Teď můžete provádět aktualizace na částečnou stránku prostřednictvím [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [webového rozhraní API](../../../web-api/index.md) nebo [signalizace](../../../signalr/index.md). Metody zpětného volání byste měli přestat používat, protože mohou způsobovat problémy s popisnými adresami URL a směrováním. Ve výchozím nastavení ovládací prvky nepovolují metody zpětného volání, ale pokud jste tuto funkci povolili v ovládacím prvku, měli byste je zakázat.

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a>Detekce schopností prohlížeče

Doporučení: Zastavte používání statického zjišťování schopností prohlížeče a místo toho použijte detekci dynamické funkce.

V dřívějších verzích ASP.NET byly podporované funkce pro každý prohlížeč uloženy v souboru XML. Rozpoznání podpory funkcí prostřednictvím statického vyhledávání není nejlepší přístup. Nyní můžete pomocí rozhraní pro detekci funkcí, jako je například [modernizr](http://modernizr.com/), dynamicky zjišťovat podporované funkce prohlížeče. Detekce funkcí Určuje podporu tím, že se pokusí použít metodu nebo vlastnost a pak zkontroluje, jestli prohlížeč vyrobí požadovaný výsledek. Ve výchozím nastavení je modernizr součástí šablon webových aplikací.

<a id="security"></a>

## <a name="security"></a>Zabezpečení

<a id="validation"></a>

### <a name="request-validation"></a>Žádost o ověření

Doporučení: ověření vstupu uživatele a kódování výstupu pro uživatele.

Ověření žádosti je funkce ASP.NET, která kontroluje každou žádost a zastaví žádost, pokud se najde zjištěná hrozba. Nezáleží na žádosti o ověření pro zabezpečení vaší aplikace proti útokům prostřednictvím skriptování napříč weby. Místo toho ověřte všechny vstupy uživatelů a zakódovat výstup. V některých omezených případech můžete použít regulární výrazy k ověření vstupu, ale ve složitějších případech byste měli ověřit vstup uživatele pomocí tříd .NET, které určují, jestli hodnota odpovídá povoleným hodnotám.

Následující příklad ukazuje, jak použít statickou metodu v třídě URI k určení, zda je identifikátor URI, který je poskytnut uživatelem, platný.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

Chcete-li ale dostatečně ověřit identifikátor URI, měli byste také zkontrolovat, zda určuje `http` nebo `https`. Následující příklad používá metody instance k ověření, že identifikátor URI je platný.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

Před vykreslením vstupu uživatele jako HTML nebo vložením vstupu uživatele do dotazu SQL zakódovat hodnoty, abyste zajistili, že není zahrnutý škodlivý kód.

Můžete kódovat hodnotu v kódu HTML pomocí syntaxe &lt;%:%&gt;, jak je znázorněno níže.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

Nebo v syntaxe Razor můžete kódovat HTML ve formátu @, jak je znázorněno níže.

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

Následující příklad ukazuje, jak HTML kódovat hodnotu v kódu na pozadí.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

Pro bezpečné kódování hodnoty pro příkazy SQL použijte parametry příkazu, jako je například [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx). <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a>Ověřování a relace bez souborů cookie

Doporučení: vyžadovat soubory cookie.

Předávání ověřovacích informací v řetězci dotazu není zabezpečené. Proto vyžaduje soubory cookie, pokud vaše aplikace zahrnuje ověřování. Pokud soubor cookie ukládá citlivé informace, zvažte vyžadování protokolu SSL pro soubor cookie.

Následující příklad ukazuje, jak zadat v souboru Web. config, který ověřování pomocí formulářů vyžaduje soubor cookie přenesený přes protokol SSL.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a>EnableViewStateMac

Doporučení: nikdy Nenastaveno na false.

Ve výchozím nastavení je EnableViewStateMac nastaveno na hodnotu true (pravda). I v případě, že vaše aplikace nepoužívá stav zobrazení, nenastavujte EnableViewStateMac na hodnotu false. Nastavením hodnoty false dojde k tomu, že vaše aplikace bude zranitelná pro skriptování mezi weby.

Od ASP.NET 4.5.2 modul runtime vynutil **enableViewStateMAC = true**. I v případě, že nastavíte hodnotu false, modul runtime tuto hodnotu ignoruje a pokračuje s hodnotou nastavenou na hodnotu true. Další informace najdete v tématu [ASP.NET 4.5.2 a enableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).

Následující příklad ukazuje, jak nastavit EnableViewStateMac na hodnotu true. Tuto hodnotu nemusíte ve skutečnosti nastavovat na hodnotu true, protože je ve výchozím nastavení true. Pokud jste ale na libovolné stránce aplikace nastavili na false hodnotu false, musíte tuto hodnotu hned opravit.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a>Střední důvěryhodnost

Doporučení: nezávisle na středním vztahu důvěryhodnosti (nebo jakékoli jiné úrovni důvěryhodnosti) jako hranice zabezpečení.

Při částečném vztahu důvěryhodnosti není vaše aplikace dostatečně chráněná a neměla by se používat. Místo toho použijte úplný vztah důvěryhodnosti a izolujte nedůvěryhodné aplikace v samostatných fondech aplikací. Spusťte také každý fond aplikací v rámci jedinečné identity. Další informace najdete v tématu [ASP.NET s částečným vztahem důvěryhodnosti nezaručuje izolaci aplikace](https://support.microsoft.com/kb/2698981).

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a>&lt;appSettings&gt;

Doporučení: Nepovolujte nastavení zabezpečení ve &lt;appSettings&gt; elementu.

Element appSettings obsahuje mnoho hodnot, které jsou požadovány pro aktualizace zabezpečení. Tyto hodnoty byste neměli měnit ani zakazovat. Pokud je nutné tyto hodnoty při nasazení aktualizace zakázat, ihned po dokončení nasazení znovu povolte.

Podrobnosti naleznete v tématu [ASP.NET appSettings element](https://msdn.microsoft.com/library/hh975440.aspx).

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a>UrlPathEncode

Doporučení: místo toho použijte [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) .

Metoda UrlPathEncode byla přidána do .NET Framework za účelem vyřešení velmi specifického problému s kompatibilitou prohlížeče. Nemá dostatečně zakódovat adresu URL a nechrání aplikaci před skriptováním mezi weby. Nikdy ji nepoužívejte ve své aplikaci. Místo toho použijte [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).

Následující příklad ukazuje, jak předat kódované adresy URL jako parametr řetězce dotazu pro ovládací prvek hypertextového odkazu.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a>Spolehlivost a výkon

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a>PreSendRequestHeaders a PreSendRequestContent

Doporučení: Nepoužívejte tyto události se spravovanými moduly. Místo toho napíšete nativní modul IIS, který provede požadovanou úlohu. Viz [vytváření modulů HTTP v nativním kódu](https://msdn.microsoft.com/library/ms693629.aspx).

Události [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) a [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) můžete použít s nativními moduly IIS.
> [!WARNING]
> Nepoužívejte `PreSendRequestHeaders` a `PreSendRequestContent` se spravovanými moduly, které implementují `IHttpModule`. Nastavení těchto vlastností může způsobit problémy s asynchronními požadavky. Kombinace požadavků na směrování (ARR) a WebSockets aplikace může vést k narušení přístupu, které by mohly způsobit selhání W3wp. Například iiscore! W3_CONTEXT_BASE:: GetIsLastNotification + 68 v souboru iiscore. dll způsobil výjimku narušení přístupu (0xC0000005).

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a>Asynchronní události stránky s webovými formuláři

Doporučení: ve webových formulářích Vyhněte se zápisu asynchronních metod void pro události životního cyklu stránky a místo toho použijte [Page. RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) pro asynchronní kód.

Když označíte událost stránky pomocí **Async** a **void**, nemůžete určit, kdy byl asynchronní kód dokončen. Místo toho použijte Page. RegisterAsyncTask ke spuštění asynchronního kódu způsobem, který umožňuje sledovat jeho dokončení.

Následující příklad ukazuje obslužnou rutinu kliknutí na tlačítko, která obsahuje asynchronní kód. Tento příklad zahrnuje asynchronní čtení řetězcové hodnoty, která je poskytována pouze jako zjednodušený příklad asynchronní úlohy a nikoli jako doporučený postup.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

Používáte-li asynchronní úlohy, nastavte cílové rozhraní HTTP runtime na 4,5 (nebo novější) v souboru Web. config. Nastavení cílové architektury na 4,5 zapne nový kontext synchronizace, který byl přidán v rozhraní .NET 4,5. Tato hodnota je nastavena ve výchozím nastavení v nových projektech v aplikaci Visual Studio, ale není nastavena, pokud pracujete s existujícím projektem.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a>Práce s požárem a zapomenoutm

Doporučení: při zpracování žádosti v rámci ASP.NET se vyhnete spouštění práce s požárem a nedovolenými událostmi (například volání metody fondu vláken. QueueUserWorkItem nebo vytvoření časovače, který opakovaně volá delegáta).

Pokud vaše aplikace funguje s požárem a zapomenutím, která běží v rámci ASP.NET, může se aplikace dostat do synchronizace. Doména aplikace může být kdykoli zničena, což znamená, že váš probíhající proces již nemusí odpovídat aktuálnímu stavu aplikace.

Tento typ práce byste měli přesunout mimo ASP.NET. K provedení průběžné práce můžete použít webové úlohy, služby systému Windows nebo roli pracovního procesu v Azure a spustit tento kód z jiného procesu.

Pokud musíte tuto práci provést v rámci ASP.NET, můžete přidat balíček NuGet s názvem [webbackground](http://www.nuget.org/packages/webbackgrounder) a spustit kód.

<a id="requestentity"></a>

### <a name="request-entity-body"></a>Tělo entity žádosti

Doporučení: Vyhněte se čtení požadavku. Form nebo Request. InputStream před událostí Execute obslužné rutiny.

Nejdříve byste měli číst z Request. Form nebo Request. InputStream během události Execute obslužné rutiny. V MVC je kontroler obslužná rutina a událost Execute při spuštění metody Action. Ve webových formulářích je stránka obslužná rutina a událost Execute, když je aktivována událost Page. init. Pokud si přečtete tělo entity požadavku dříve, než je událost Execute, budete mít vliv na zpracování žádosti.

Pokud potřebujete číst tělo entity požadavku před událostí Execute, použijte buď [Request. GetBufferlessInputStream není](https://msdn.microsoft.com/library/ff406798.aspx) , nebo [Request. GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx). Pokud používáte GetBufferlessInputStream není, získáte z požadavku nezpracovaný datový proud a Předpokládejme zodpovědnost za zpracování celého požadavku. Po volání GetBufferlessInputStream není nejsou požadavky Request. Form a Request. InputStream k dispozici, protože nebyly vyplněny ASP.NET. Když použijete GetBufferedInputStream, dostanete kopii datového proudu z požadavku. Request. Form a Request. InputStream jsou stále k dispozici později v žádosti, protože ASP.NET naplní další kopii.

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a>Response. Redirect a Response. end

Doporučení: Pamatujte na rozdíly ve způsobu zpracování vlákna po volání metody [Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).

Metoda [Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) volá metodu Response. end. V synchronním procesu volání Request. Redirect způsobí okamžité přerušení aktuálního vlákna. Nicméně v asynchronním procesu volání metody Response. Redirect neukončí aktuální vlákno, takže provádění kódu pro požadavek bude pokračovat. V asynchronním procesu je nutné vrátit úlohu z metody pro zastavení provádění kódu.

V projektu MVC byste neměli volat Response. Redirect. Místo toho vraťte RedirectResult.

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a>EnableViewState a ViewStateMode

Doporučení: použijte ViewStateMode namísto EnableViewState k poskytnutí podrobné kontroly nad tím, které ovládací prvky používají stav zobrazení.

Nastavíte-li atribut EnableViewState na hodnotu false v direktivě stránky, je stav zobrazení zakázán pro všechny ovládací prvky na stránce a nelze jej povolit. Pokud chcete povolit stav zobrazení pouze pro určité ovládací prvky na stránce, nastavte ViewStateMode na hodnotu zakázáno pro stránku.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

Potom nastavte ViewStateMode na Enabled pouze ovládací prvky, které skutečně potřebují stav zobrazení.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

Když povolíte stav zobrazení jenom pro ovládací prvky, které ho potřebují, můžete zmenšit velikost stavu zobrazení webových stránek.

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a>SqlMembershipProvider

Doporučení: použijte univerzální poskytovatele.

V aktuálních šablonách projektu byl SqlMembershipProvider nahrazen [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), který je k dispozici jako balíček NuGet. Pokud používáte SqlMembershipProvider v projektu, který byl vytvořen pomocí starší verze šablon, měli byste přepnout na Universal Providers. Univerzální poskytovatelé pracují se všemi databázemi, které jsou podporovány nástrojem Entity Framework.

Další informace najdete v tématu [představujeme ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a>Dlouho běžící požadavky (> 110 sekund)

Doporučení: pro připojené klienty použijte [objekty WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) nebo [Signal](../../../signalr/index.md) a použijte asynchronní vstupně-výstupní operace.

Dlouhotrvající požadavky mohou způsobit nepředvídatelné výsledky a špatný výkon ve vaší webové aplikaci. Výchozí nastavení časového limitu pro požadavek je 110 sekund. Pokud používáte stav relace s dlouho běžícím požadavkem, ASP.NET uvolní zámek objektu Session po 110 sekundách. Vaše aplikace ale může být uprostřed operace s objektem relace, když se zámek uvolní a operace se nemusí dokončit úspěšně. Pokud je druhá žádost od uživatele zablokovaná, zatímco je spuštěný první požadavek, druhý požadavek může získat přístup k objektu Session v nekonzistentním stavu.

Pokud vaše aplikace zahrnuje blokující (nebo synchronní) vstupně-výstupní operace, aplikace přestane reagovat.

Chcete-li zvýšit výkon, použijte asynchronní vstupně-výstupní operace v .NET Framework. K připojení klientů k serveru taky použijte objekty WebSockets nebo Signal. Tyto funkce jsou navržené tak, aby efektivně zpracovávala dlouhotrvající požadavky.
