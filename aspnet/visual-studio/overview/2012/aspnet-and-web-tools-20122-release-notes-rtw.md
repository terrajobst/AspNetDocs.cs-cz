---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: Zpráva k vydání verze ASP.NET and Web Tools 2012,2 | Microsoft Docs
author: rick-anderson
description: Poznámky k verzi ASP.NET and Web Tools 2012,2.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579518"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET a webové nástroje – poznámky k verzi 2012.2

> Tento dokument popisuje vydání ASP.NET and Web Tools 2012,2. Jedná se o aktualizaci webových nástrojů sady Visual Studio a ASP.NET.

- [Poznámky k instalaci](#_Installation)
- [Dokumentace](#_Documentation)
- [Podpora](#_Support)
- [Požadavky na software](#_Software_Requirements)
- [Nové funkce v ASP.NET and Web Tools 2012,2](#_New_Features_in)

    - [Nástroje](#_Tooling)
    - [Publikování na webu](#_Web_Publishing)
    - [Šablony ASP.NET MVC](#_Templates)
    - [Webové rozhraní API v ASP.NET](#_ASP.NET_Web_API)

    - [ASP.NET signál](#_ASP.NET_SignalR)
    - [Popisné adresy URL ASP.NET](#_ASP.NET_Friendly_URLs)
- [Známé problémy a zásadní změny](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET and Web Tools 2012,2 pro Visual Studio 2012 lze nainstalovat pomocí [instalačního programu webové platformy](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2). Jedná se o aktualizaci sady Visual Studio 2012 nebo Visual Studio Express 2012 pro web, která je povinná. Pokud nemáte nainstalovanou aplikaci Visual Studio, nainstaluje se Visual Studio Express 2012 pro web.

ASP.NET and Web Tools 2012,2 můžete také nainstalovat ručně. Je nutné, aby byla nainstalována aplikace Visual Studio 2012 nebo Visual Studio Express 2012 pro web. Pak postupujte podle následujících pokynů: 

1. Stáhněte si instalační program [ASP.NET a web frameworks 2012,2 z webu](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) Download Center.
2. Po zobrazení výzvy klikněte na spustit. Soubor můžete také uložit a spustit ho později.
3. Ověřte verzi sady Visual Studio, kterou budete aktualizovat. To můžete provést spuštěním sady Visual Studio, kterou chcete aktualizovat. Pak klikněte na položku nabídky Help.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. Pokud se zobrazí položka nabídky &quot;o Microsoft Visual Studio 2012 pro webové&quot; Stáhněte si [web Vývojářské nástroje 2012,2-Visual Studio Express 2012 pro web](https://go.microsoft.com/fwlink/?LinkID=282228). Jinak stáhněte [Web Vývojářské nástroje 2012,2 – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. Po zobrazení výzvy klikněte na spustit. Soubor můžete také uložit a spustit ho později.

> [!NOTE]
> Verze ASP.NET and Web Tools 2012,2 nezahrnuje nástroje SQL Server Data Tools. SQL Server a databáze Windows Azure SQL poskytují bohatší sadu databázových nástrojů, včetně vývoje v rámci projektu, porovnání schémat a vylepšené možnosti nasazení databáze. Další informace nebo informace o instalaci nástrojů SQL Server Data Tools najdete v [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).

<a id="_Documentation"></a>
## <a name="documentation"></a>Dokumentace

Kurzy a další informace o ASP.NET and Web Tools 2012,2 jsou k dispozici na webu ASP.NET (https://www.asp.net).

<a id="_Support"></a>
## <a name="support"></a>Podpora

ASP.NET and Web Tools 2012,2 je oficiálně vydaná a podporovaná. Můžete použít svůj normální kanál podpory. Můžete také publikovat otázky do fór ASP.NET ([https://forums.asp.net/](https://forums.asp.net/)), kde členové komunity ASP.NET mají často možnost zajistit neformální podporu.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Požadavky na software

ASP.NET and Web Tools 2012,2 vyžaduje Visual Studio 2012 nebo Visual Studio Express 2012 pro web.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>Nové funkce v ASP.NET and Web Tools 2012,2

Tato část popisuje funkce, které byly představeny ve verzi ASP.NET and Web Tools 2012,2.

<a id="_Tooling"></a>
### <a name="tooling"></a>Nástroje

- Inspektor stránek 

    - Podporuje mapování výběru JavaScriptu, které umožňuje inspektoru stránky mapovat položky, které se dynamicky přidaly na stránku zpátky do odpovídajícího kódu JavaScriptu.
    - Možnost Zobrazit aktualizace šablon stylů CSS v reálném čase.
    - Další informace najdete v tématu [Automatická synchronizace šablon stylů CSS a mapování výběru JavaScriptu v nástroji Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).
- Editor 

    - Podporuje zvýrazňování syntaxe pro CoffeeScript, Mustache, handlebars a JsRender.
    - Editor HTML poskytuje IntelliSense pro vyseknutí vazeb.
    - MÉNĚ úprav a podpora kompilátoru, aby bylo možné vytvářet dynamickou šablonu stylů CSS s menším množstvím.
    - Vložte JSON jako třídu .NET. Pomocí tohoto speciálního příkazu pro vložení vložte JSON do C# souboru kódu nebo VB.NET a Visual Studio automaticky vygeneruje třídy .NET odvozené od JSON.
- Podpora emulátoru mobilního emulátoru přidává rozšiřující zavěšení, aby bylo možné nainstalovat emulátory třetích stran jako VSIX. Instalované emulátory se zobrazí v rozevírací nabídce F5, aby mohli vývojáři zobrazit náhled svých webů v různých mobilních zařízeních. Přečtěte si další informace o této funkci v záznamu blogu Scott Hanselman na [nové integraci browserstackem se sadou Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Publikování na webu

- Projekty webu teď mají stejné prostředí pro publikování jako projekty webových aplikací, včetně publikování na webech Windows Azure.
- Selektivní publikování &#8211; jednoho nebo více souborů, můžete provádět následující akce (po publikování na nasazení webu koncový bod): 

    - Publikujte vybrané soubory.
    - Podívejte se na rozdíl mezi místním souborem a vzdáleným souborem.
    - Aktualizujte místní soubor se vzdáleným souborem nebo aktualizujte vzdálený soubor místním souborem.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>Šablony ASP.NET MVC

- Nová šablona aplikací pro Facebook usnadňuje vytváření aplikací pro prostředí Facebook Canvas. Pomocí pár jednoduchých kroků můžete vytvořit aplikaci pro Facebook, která získává data od přihlášeného uživatele a integruje se s jeho přáteli. Šablona obsahuje novou knihovnu, která se stará o všechny záležitosti související se sestavováním aplikací pro Facebook, jako jsou oprávnění, ověřování, přístup k datům sítě Facebook a další. Další informace o použití šablony aplikace Facebook naleznete v tématu [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).
- Nová šablona MVC jednostránkové aplikace umožňuje vývojářům sestavit interaktivní webovou aplikaci na straně klienta, která navíc k rozhraní ASP.NET Web API využívá technologie HTML 5, CSS 3 a oblíbené knihovny Knockout a jQuery jazyka JavaScript. Šablona obsahuje aplikaci seznamu "todo", která ukazuje běžné postupy pro sestavení aplikace jazyka HTML5 v JavaScriptu, která používá rozhraní API RESTful serveru. Další informace najdete na [https://www.asp.net/single-page-application](../../../single-page-application/index.md).
- Nyní můžete vytvořit VSIX, který přidá nové šablony do dialogového okna Nový projekt ASP.NET MVC. Přečtěte si, jak tady: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- Šablony projektů &#8211; FixedDisplayModes balíčku MVC byly aktualizovány tak, aby zahrnovaly nový balíček NuGet FixedDisplayModes, který obsahuje alternativní řešení pro chybu v MVC 4. Další informace o opravě obsažené v balíčku najdete v tomto blogovém příspěvku ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) od týmu MVC.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>Webové rozhraní API ASP.NET

Webové rozhraní API pro ASP.NET bylo vylepšené o několik nových funkcí:

- ASP.NET webového rozhraní API OData
- Trasování webového rozhraní API ASP.NET
- Stránka s webovou pomocí rozhraní API pro ASP.NET

#### <a name="aspnet-web-api-odata"></a>ASP.NET webového rozhraní API OData

ASP.NET Web API OData vám poskytne flexibilitu, kterou potřebujete k vytváření koncových bodů OData s bohatou obchodní logikou prostřednictvím libovolného zdroje dat. Pomocí ASP.NET webového rozhraní API OData ovládáte množství sémantiky OData, které chcete zveřejnit. ASP.NET Web API OData je součástí šablon projektů ASP.NET MVC 4 a je dostupný i z NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).

ASP.NET Web API OData aktuálně podporuje následující funkce:

- Pro povolení sémantiky dotazů OData použijte atribut [Queryable].
- Umožňuje snadno ověřit dotazy OData a omezit sadu podporovaných možností dotazů, operátorů a funkcí.
- Parametr BIND pro ODataQueryOptions přímo pro získání abstraktní reprezentace stromu syntaxe dotazu, který lze následně ověřit a použít na rozhraní IQueryable nebo IEnumerable.
- Povolí stránkování řízené službou a další generování odkazů na stránce zadáním omezení výsledků pro atribut [Queryable].
- Vyžádá zadání vloženého počtu celkového počtu vyhovujících prostředků pomocí $inlinecount.
- Řízení šíření hodnoty null.
- Libovolný/všechny operátory v $filter.
- Odvodí model dat entity podle konvence nebo explicitně upravte model způsobem podobným Entity Framework kód jako první.
- Vystavení sad entit odvozením z EntitySetController.
- Jednoduché, přizpůsobitelné konvence pro vystavení navigačních vlastností, manipulace s odkazy a implementace akcí OData.
- Zjednodušené směrování pomocí metody rozšíření MapODataRoute.
- Podpora správy verzí vyvoláním více modelů EDM.
- Vystavte dokument služby a $metadata, abyste pro vaše webové rozhraní API mohli vygenerovat klienty (.NET, Windows Phone, Windows Store atd.).
- Podpora pro podrobné formáty Atom, JSON a JSON pro OData.
- Vytvořit, aktualizovat, částečně aktualizovat (opravit) a odstranit entity.
- Dotazování a manipulace s relacemi mezi entitami.
- Vytvořte propojení vztahů, která jsou propojená s vašimi trasami.
- Komplexní typy.
- Dědičnost typu entity
- Vlastnosti kolekce.
- Výčt.
- Akce OData
- Postavené na stejném základu jako WCF Data Services, konkrétně ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).

Další informace o ASP.NET Web API OData najdete v tématu [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).

#### <a name="aspnet-web-api-tracing"></a>Trasování webového rozhraní API ASP.NET

Trasování webového rozhraní API ASP.NET integruje data trasování z vašich webových rozhraní API pomocí trasování .NET. V šabloně projektu webového rozhraní API je teď ve výchozím nastavení povolená. Data trasování pro vaše webová rozhraní API se odesílají do okna výstup a zpřístupňují se prostřednictvím IntelliTrace. Trasování webového rozhraní API ASP.NET umožňuje trasovat informace o webovém rozhraní API při hostování na platformě Windows Azure prostřednictvím integrace s [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx). Můžete taky nainstalovat a povolit trasování ASP.NET webového rozhraní API v libovolné aplikaci pomocí balíčku NuGet ASP.NET webového rozhraní API pro trasování ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).

Další informace o konfiguraci a použití trasování webového rozhraní API v ASP.NET najdete [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).

#### <a name="aspnet-web-api-help-page"></a>Stránka s webovou pomocí rozhraní API pro ASP.NET

V šabloně projektu webového rozhraní API je teď ve výchozím nastavení zahrnutá Stránka s ASP.NET webové rozhraní API. Stránka s nápovědu webového rozhraní API pro ASP.NET automaticky generuje dokumentaci k webovým rozhraním API, včetně koncových bodů HTTP, podporovaných metod HTTP, parametrů a ukázkové datové části zprávy žádosti a odpovědi. Dokumentace se automaticky načte z komentářů ve vašem kódu. Stránku s usnadněním webového rozhraní API pro ASP.NET můžete přidat do libovolné aplikace pomocí balíčku NuGet stránky ASP.NET pro Web API ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).

Další informace o nastavení a přizpůsobení stránky pro nápovědu webového rozhraní API pro ASP.NET najdete v tématu [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>Funkce SignalR technologie ASP.NET

ASP.NET Signal usnadňuje přidání webových funkcí v reálném čase do vaší aplikace ASP.NET, a to pomocí WebSockets, pokud jsou k dispozici, a automaticky se vrátí k jiným technikům, když ne.

Další informace o používání ASP.NET signalizace najdete v tématu [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>Přátelské adresy URL technologie ASP.NET

ASP.NET FriendlyURLs umožňuje vývojářům webových formulářů velmi snadno generovat adresy URL pro prohlížení čisticích souborů (bez přípony. aspx). Nevyžaduje žádnou konfiguraci a dá se použít s existujícími aplikacemi ASP.NET v 4.0. Funkce FriendlyURLs také usnadňuje vývojářům přidávat mobilní podporu do svých aplikací tím, že podporují přepínání mezi zobrazeními počítačů a mobilních zobrazení.

Další informace o instalaci a použití ASP.NETch adres URL najdete v tématu [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Známé problémy a zásadní změny

V této části jsou popsány známé problémy a zásadní změny, které jsou součástí verze ASP.NET and Web Tools 2012,2.

### <a name="installation-issues"></a>Problémy s instalací

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Instalace sady Visual Studio 2012 mimo pořadí

Instalace další SKU sady Visual Studio 2012 po instalaci ASP.NET and Web Tools 2012,2 bude vyžadovat operaci opravy. Vezměte v úvahu následující sekvenci:

1. Instalace sady Visual Studio 2012 Express for Web
2. Nainstalovat ASP.NET and Web Tools 2012,2
3. Instalace sady Visual Studio 2012 Professional, Premium nebo Ultimate

Krok 2 má za následek jenom instalaci aktualizací pro Express for Web. Aby bylo zajištěno, že další SKU nainstalovaná během kroku 3 obsahuje aktualizaci, budete muset opravit ASP.NET and Web Tools 2012,2 a nainstalovat aktualizace pro poslední nainstalovanou SKU. To platí také v případě, že SKU v krocích 1 a 3 jsou stornovány.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Instalace Microsoft ASP.NET and Web Tools 2012,2, když je Visual Studio otevřené

Pokud je v nástroji VS otevřený během instalace Microsoft ASP.NET and Web Tools 2012,2, může Visual Studio končit špatným stavem. Doporučujeme, aby uživatelé před pokračováním v instalaci zavřeli všechny instance sady Visual Studio.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Ruší se instalace ASP.NET and Web Tools 2012,2 během instalace.

Zrušení instalace ASP.NET and Web Tools 2012,2 při instalaci ponechá Visual Studio v nesprávném stavu. K vyřešení tohoto problému použijte následující postup: 

- Přejít na Přidat odebrat programy
- Pokud je k dispozici Microsoft ASP.NET and Web Tools 2012,2, odinstalujte ji.
- Přeinstalujte Microsoft ASP.NET and Web Tools 2012,2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>Po odinstalování ASP.NET and Web Tools 2012,2 chybí šablony ASP.NET MVC 4 a web Razor v2.

Odinstalace ASP.NET and Web Tools 2012,2 také odinstaluje všechny šablony webu ASP.NET MVC 4 a Razor v2 ze sady Visual Studio 2012.

Alternativním řešením je opravit instalaci sady Visual Studio 2012 pro přeinstalaci šablon webu ASP.NET MVC 4 a Razor v2.

### <a name="tooling-issues"></a>Problémy s nástrojem

#### <a name="nuget-error-reported-during-project-creation"></a>Chyba NuGet nahlášená během vytváření projektu

Po instalaci ASP.NET and Web Tools 2012,2 se při vytváření projektu MVC 4 může zobrazit následující chyba.

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET and Web Tools 2012,2 dodává NuGet 2,1 a aktualizuje rozšíření v aplikaci Visual Studio 2012. V některých případech se instalačnímu programu VSIX nepodaří správně aktualizovat VSIX. Následující kroky vám umožní vyřešit tento problém:

1. Spusťte Visual Studio 2012 jako správce.
2. Přejít na nástroje – rozšíření&gt;a aktualizace a odinstalace NuGet.
3. Zavřete Visual Studio.
4. Přejděte do instalační složky ASP.NET and Web Tools 2012,2:

    1. Pro Visual Studio 2012: **Program Files\Microsoft ASP. NET\ASP.NET Web Stack\Visual Studio 2012**
    2. Pro Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP. NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**
5. Poklikejte na NuGet. Tools. vsix a přeinstalujte NuGet.

### <a name="web-api-issues"></a>Problémy s webovým rozhraním API

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>Analýza problémů v $filter a literálech DateTime

Analyzátor identifikátoru URI OData nedokáže správně analyzovat částečné literály DateTime. Například $filter = Start EQ DateTime "2012-12-31T12:00" se nezdařilo správně analyzovat. Alternativním řešením je použití úplného literálu, $filter = Start EQ DateTime ' 2012-12-31T12:00:00 '.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData nepodporuje názvy vlastností s rozlišováním velkých a malých písmen.

OData nepodporuje názvy vlastností nerozlišující velikosti písmen v dotazech OData a cestě OData. Viz pracovní položky:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Pokud mají uživatelé v JavaScriptu na straně klienta a na straně serveru různá velká písmena, budou se pravděpodobně setkat s tímto problémem. Tento problém je záměrné v protokolu OData. Mnoho uživatelů ale tento problém oznamuje. Aby uživatelé mohli tento problém obejít, musí opravit případy v adrese URL.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>Výchozí konvence směrování OData nepodporuje vlastnost POST/PUT pro navigační vlastnost.

Výchozí konvence směrování OData nepodporuje vlastnost POST/PUT pro navigační vlastnost. Viz pracovní položka [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366). Tato často používaná konvence ve výchozích konvencích neexistuje.

Aby uživatelé mohli tento problém obejít, je potřeba, aby rozšířili novou konvenci směrování, aby ji podporovala.

### <a name="facebook-template-issues"></a>Problémy s šablonou Facebooku

#### <a name="facebook-application-template-only-works-using-net-45"></a>Šablona aplikace pro Facebook funguje pouze pomocí .NET 4,5

V rozevíracím seznamu Framework v dialogovém okně Nový projekt musíte vybrat .NET 4,5, abyste viděli šablonu aplikace Facebook v ASP.NET MVC 4.

#### <a name="real-time-update-controller"></a>Kontroler aktualizací v reálném čase

Šablona aplikace na Facebooku umožňuje uživateli snadno vytvořit kontroler webového rozhraní API pro zpracování aktualizací v reálném čase z Facebooku. Pokud je váš vývojový počítač za překladem adres (NAT), nemusí váš kontroler fungovat bez další konfigurace sítě. Podrobnosti najdete tady: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Konflikty hodnot řetězců dotazů pomocí parametrů OAuth pro Facebook

Následující pole jsou v konfliktu s adresou URL zpětného volání dialogového okna Facebook OAuth. Nepřidávat vlastní hodnoty řetězce dotazu s následujícími názvy: kód, chyba, chyba\_popis, chyba\_důvod.

#### <a name="using-page-inspector-with-facebook-template"></a>Použití funkce Page Inspector se šablonou Facebook

Během ladění aplikace na Facebooku nemůžete použít funkci Page Inspector v aplikaci Visual Studio 2012. Inspektor stránky v současné době nepodporuje prvky IFrame.

### <a name="single-page-application-template-issues"></a>Problémy šablony aplikace s jednou stránkou

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>Při použití aktualizace JQuery 1.9/vyseknutí 2.2.1 při spuštění výchozího projektu MVC SPA se nezpracovává nová událost pro úpravu položky ToDo s fokusem.

Při použití aktualizace JQuery 1.9/vyseknutí 2.2.1 při spuštění výchozího projektu MVC pro ověřování po vstupu do seznamu úkolů se už po zadání nové položky ToDo do seznamu úkolů nepřejdete do nového pole pro úpravu položky ToDo.

Na referenční informace o alternativním řešení [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)a udělejte podobnou opravu následujícímu ukázkovému kódu:

Soubor todo. model. js  
 Function ToDoList (data), přidejte následující:  
 **samy.-Select = Ko. propozorovatelný (NEPRAVDA);**

Function todoList. prototyp. addTodo přidejte následující černý text:  
 **samo. s volbou (true);**  
 osobní. newTodoTitle (&quot;&quot;);

Soubor index. cshtml přidejte následující černý text:  
 data formuláře &lt;– BIND =&quot;odeslat: addTodo&quot;&gt;  
 &lt;Input Class =&quot;addTodo&quot; typ =&quot;text&quot; data-BIND =&quot;hodnota: newTodoTitle, zástupný symbol: ' sem zadejte text pro přidání ', blurOnEnter: true, **HasFocus: selektivně**, událost: {rozostření: addTodo}&quot; /&gt;  
 &lt;&gt;
