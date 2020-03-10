---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET and Web Tools pro Visual Studio 2013 poznámky k verzi | Microsoft Docs
author: microsoft
description: Tento dokument popisuje vydání ASP.NET and Web Tools pro Visual Studio 2013.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557930"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>ASP.NET a webové nástroje pro Visual Studio 2013 – poznámky k verzi

od [Microsoftu](https://github.com/microsoft)

> Tento dokument popisuje vydání ASP.NET and Web Tools pro Visual Studio 2013.

## <a name="contents"></a>Obsah

- [Poznámky k instalaci](#TOC1)
- [Dokumentace](#TOC2)
- [Požadavky na software](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Nové funkce v ASP.NET and Web Tools pro Visual Studio 2013

- [Jeden ASP.NET](#TOC6)
- [Nové prostředí webového projektu](#newproj)
- [ASP.NET generování uživatelského rozhraní](#scaffold)
- [Browser Link](#browser-link)
- [Vylepšení webového editoru sady Visual Studio](#web-editor)
- [Podpora Azure App Service Web Apps v aplikaci Visual Studio](#waws)
- [Vylepšení publikování na webu](#publish)
- [NuGet 2.7](#nuget)
- [Webové formuláře ASP.NET](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [Webové rozhraní API 2 ASP.NET](#TOC11)
- [ASP.NET signál](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Komponenty Microsoft OWIN](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [Pozastavení aplikace ASP.NET](#TOC15)
- [Známé problémy a zásadní změny](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET and Web Tools pro Visual Studio 2013 jsou v hlavním instalačním programu rozčleněné a dají se stáhnout [tady](https://www.asp.net/downloads).

<a id="TOC2"></a>
## <a name="documentation"></a>Dokumentace

Kurzy a další informace o ASP.NET and Web Tools pro Visual Studio 2013 jsou k dispozici na webu [ASP.NET](https://www.asp.net/).

<a id="TOC4"></a>
## <a name="software-requirements"></a>Požadavky na software

ASP.NET and Web Tools vyžaduje Visual Studio 2013.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Nové funkce v ASP.NET and Web Tools pro Visual Studio 2013

V následujících částech jsou popsány funkce, které byly představeny v této verzi.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>Jeden ASP.NET

S vydáním Visual Studio 2013 jsme udělali krok k sjednocení zkušeností s používáním technologií ASP.NET, abyste mohli snadno kombinovat a porovnat ty, které chcete. Můžete například spustit projekt pomocí MVC a snadno přidat stránky webových formulářů do projektu, nebo webové rozhraní API pro generování uživatelského rozhraní v projektu webových formulářů. Jeden ASP.NET je vše, co usnadňuje vývojářům práci v ASP.NET. Bez ohledu na to, jakou technologii si zvolíte, můžete mít jistotu, že sestavíte na důvěryhodném základním rozhraní jednoho ASP.NET.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>Nové prostředí webového projektu

Vylepšili jsme možnosti vytváření nových webových projektů v Visual Studio 2013. V dialogovém okně **Nový webový projekt ASP.NET** můžete vybrat požadovaný typ projektu, nakonfigurovat libovolnou kombinaci technologií (webové formuláře, MVC, webové rozhraní API), nakonfigurovat možnosti ověřování a přidat projekt testu jednotek.

![Nový projekt ASP.NET](release-notes/_static/image1.png)

Nové dialogové okno umožňuje změnit výchozí možnosti ověřování pro mnoho šablon. Například při vytváření projektu webových formulářů ASP.NET můžete vybrat některou z následujících možností:

- Bez ověřování
- Individuální uživatelské účty (členství v ASP.NET nebo přihlašování k poskytovateli sociálních sítí)
- Účty organizace (Active Directory v internetové aplikaci)
- Ověřování systému Windows (služba Active Directory v intranetové aplikaci)

![Možnosti ověřování](release-notes/_static/image2.png)

Další informace o novém procesu pro vytváření webových projektů naleznete [v tématu creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md). Další informace o nových možnostech ověřování najdete v tématu [ASP.NET identity](#TOC8) dále v tomto dokumentu.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET generování uživatelského rozhraní

Generování uživatelského rozhraní ASP.NET je rozhraní pro generování kódu pro webové aplikace v ASP.NET. Umožňuje snadno přidat do projektu často používaný kód, který komunikuje s datovým modelem.

V předchozích verzích sady Visual Studio bylo generování uživatelského rozhraní omezeno na ASP.NET projekty MVC. Pomocí Visual Studio 2013 můžete nyní použít generování uživatelského rozhraní pro libovolný projekt ASP.NET, včetně webových formulářů. Visual Studio 2013 aktuálně nepodporuje generování stránek pro projekt webových formulářů, ale můžete i nadále používat generování uživatelského rozhraní s webovými formuláři přidáním závislostí MVC do projektu. Do budoucí aktualizace se přidají podpora pro generování stránek webových formulářů.

Při použití generování uživatelského rozhraní zajišťujeme, aby byly v projektu nainstalované všechny požadované závislosti. Například pokud začnete s projektem ASP.NET Web Forms a potom použijete generování uživatelského rozhraní pro přidání kontroleru webového rozhraní API, požadované balíčky NuGet a odkazy se automaticky přidají do projektu.

Chcete-li přidat generování uživatelského rozhraní MVC do projektu webových formulářů, přidejte **novou vygenerované položky** a v dialogovém okně vyberte **závislosti MVC 5** . K dispozici jsou dvě možnosti pro generování uživatelského rozhraní MVC; Minimální a plná. Pokud vyberete minimální, do projektu se přidají jenom balíčky NuGet a odkazy pro ASP.NET MVC. Pokud vyberete možnost úplná, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.

Podpora pro generování generovaných asynchronních řadičů používá nové asynchronní funkce z Entity Framework 6.

Další informace a kurzy najdete v tématu [Přehled generování uživatelského rozhraní ASP.NET](aspnet-scaffolding-overview.md).

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Odkaz na prohlížeč – kanál signálu mezi prohlížečem a Visual Studio

Nová funkce [odkaz v prohlížeči](using-browser-link.md) umožňuje připojit více prohlížečů k sadě Visual Studio a aktualizovat je všechny kliknutím na tlačítko na panelu nástrojů. Můžete připojit více prohlížečů k vašemu vývojovému webu, včetně emulátorů pro mobilní zařízení, a kliknutím na aktualizovat aktualizovat všechny prohlížeče současně. Odkaz na prohlížeč také zpřístupňuje rozhraní API, které vývojářům umožňuje psát rozšíření Browser Link Extensions.

![](release-notes/_static/image3.png)

Tím, že vývojářům umožní využít rozhraní API pro připojení k prohlížeči, je možné vytvořit velmi pokročilé scénáře, které překračují hranice mezi Visual Studio a jakýmkoli připojeným prohlížečem. Web Essentials využívá rozhraní API k vytvoření integrovaného prostředí mezi Visual Studio a vývojářskými nástroji v prohlížeči, vzdáleného řízení emulátorů pro mobilní zařízení a další spoustou.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Vylepšení webového editoru sady Visual Studio

Visual Studio 2013 obsahuje nový editor HTML pro soubory Razor a soubory HTML ve webových aplikacích. Nový editor HTML poskytuje jedno sjednocené schéma založené na HTML5. Má automatické dokončování složených závorek, uživatelské rozhraní jQuery a atribut AngularJS pro technologii IntelliSense, atributy seskupování IntelliSense, ID a název třídy IntelliSense a další vylepšení, včetně lepšího výkonu, formátování a inteligentních operací.

Následující snímek obrazovky ukazuje použití funkce Bootstrap atributu IntelliSense v editoru HTML.

![IntelliSense v editoru HTML](release-notes/_static/image4.png)

Visual Studio 2013 také přináší CoffeeScript i méně editorů. Editor LESS se dodává se všemi studenými funkcemi z editoru šablon stylů CSS a má konkrétní IntelliSense pro proměnné a objekty Mixin napříč všemi méně dokumenty v řetězci @import.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Podpora Azure App Service Web Apps v aplikaci Visual Studio

V Visual Studio 2013 se sadou Azure SDK pro .NET 2,2 můžete pomocí **Průzkumník serveru** komunikovat přímo se vzdálenými webovými aplikacemi. Můžete se přihlásit ke svému účtu Azure, vytvářet nové webové aplikace, konfigurovat aplikace, zobrazovat protokoly v reálném čase a další. Po vydání sady SDK 2,2 budete moci spustit v režimu ladění vzdáleně v Azure. Většina nových funkcí pro Azure App Service Web Apps v sadě Visual Studio 2012 funguje i při instalaci aktuální verze sady Azure SDK pro .NET.

Další informace najdete v následujících zdrojích:

- [Vytvoření webové aplikace v ASP.NET v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Řešení potíží s webovou aplikací v Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Vylepšení publikování na webu

Visual Studio 2013 zahrnují nové a vylepšené funkce publikování na webu. Tady je několik z nich:

- Snadné [Automatické automatizace šifrování souborů Web. config](https://go.microsoft.com/fwlink/?LinkId=325529). (Tento odkaz a následující dva body dokumentaci na webu MSDN, které nemusí být k dispozici, dokud neuplyne pozdě v den 10/17.)
- Snadná [automatizace při nasazení aplikace v režimu offline](https://go.microsoft.com/fwlink/?LinkId=325530).
- Nakonfigurujte Nasazení webu pro [použití kontrolního součtu souborů namísto data poslední změny](https://go.microsoft.com/fwlink/?LinkId=325531) pro určení, které soubory se mají zkopírovat na server.
- Jednotlivé vybrané soubory (včetně souboru Web. config) můžete rychle publikovat při použití metod pro publikování FTP nebo systému souborů a také pomocí Nasazení webu.

Další informace o nasazení webu ASP.NET najdete [na webu ASP.NET](https://go.microsoft.com/fwlink/?LinkId=322027).

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2,7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány v [poznámkách k verzi nuget 2,7](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Tato verze NuGet také odstraňuje nutnost poskytnout explicitní souhlas funkce obnovení balíčku NuGet pro stažení balíčků. Souhlas (a související zaškrtávací políčko v dialogovém okně Předvolby NuGet) je teď udělené instalací NuGet. Nově funguje i obnovení balíčků ve výchozím nastavení.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET – webové formuláře

### <a name="one-aspnet"></a>Jeden ASP.NET

Šablony projektů webových formulářů se hladce integrují s novým jedním ASP.NETm prostředím. Do projektu webových formulářů můžete přidat podporu MVC a webového rozhraní API a ověřování můžete nakonfigurovat pomocí jednoho Průvodce vytvořením projektu ASP.NET. Další informace najdete v tématu [vytváření ASP.NET webových projektů v Visual Studio 2013](creating-web-projects-in-visual-studio.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Šablony projektů webových formulářů podporují novou ASP.NET Identity Framework. Šablony teď podporují vytváření projektu v intranetu webových formulářů. Další informace najdete v tématu [metody ověřování](creating-web-projects-in-visual-studio.md#auth) při **vytváření ASP.NET webových projektů v Visual Studio 2013**.

### <a name="bootstrap"></a>Spouštěcí rutina

Šablony webových formulářů používají [bootstrap](http://twitter.github.io/bootstrap/) k zajištění elegantního a reakce na vzhled a chování, které lze snadno přizpůsobit. Další informace naleznete v tématu [bootstrap v šablonách webového projektu Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>Jeden ASP.NET

Šablony projektů webové MVC se hladce integrují s novým ASP.NET prostředím. Můžete přizpůsobit projekt MVC a nakonfigurovat ověřování pomocí jednoho Průvodce vytvořením projektu ASP.NET. Úvodní kurz k ASP.NET MVC 5 najdete na adrese [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

Informace o tom, jak upgradovat projekty MVC 4 na MVC 5, najdete v tématu [Postup upgradu ASP.NET MVC 4 a projektu webového rozhraní API na ASP.NET MVC 5 a webové rozhraní API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Šablony projektů MVC byly aktualizovány, aby používaly ASP.NET Identity pro ověřování a správu identit. Kurz týkající se webu Facebook a ověřování Google a nového rozhraní API pro členství najdete v části [Vytvoření aplikace ASP.NET MVC 5 s aplikacemi Facebook a Google OAuth2 a OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) a [vytvoření aplikace pro ASP.NET MVC s ověřováním a SQL DB a nasazením do Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).

### <a name="bootstrap"></a>Spouštěcí rutina

Šablona projektu MVC byla aktualizována tak, aby používala [bootstrap](http://getbootstrap.com/) , aby poskytovala elegantní a reagující vzhled a dojem, že je možné snadno přizpůsobit. Další informace naleznete v tématu [bootstrap v šablonách webového projektu Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).

### <a name="authentication-filters"></a>Filtry ověřování

Filtry ověřování jsou novým druhem filtru v ASP.NET MVC, který se spouští před autorizačními filtry v kanálu služby ASP.NET MVC, a umožňuje pro všechny řadiče zadat logiku ověřování pro jednotlivé akce, řadiče nebo globálně. Ověřovací filtry zpracovávají přihlašovací údaje v žádosti a poskytují odpovídající objekt zabezpečení. Ověřovací filtry mohou také přidat výzvy ověřování v reakci na neautorizované žádosti.

### <a name="filter-overrides"></a>Přepsání filtru

Nyní můžete přepsat, které filtry se vztahují na danou metodu akce nebo kontroler zadáním filtru pro přepsání. Filtry přepsání určují sadu typů filtrů, které by neměly být spuštěny pro daný obor (akce nebo kontroler). To vám umožní nakonfigurovat filtry, které se použijí globálně, ale pak vyloučit určité globální filtry z použití na konkrétní akce nebo řadiče.

### <a name="attribute-routing"></a>Směrování atributů

ASP.NET MVC teď podporuje směrování atributů. díky příspěvku ve službě Tim McCall je autorem [http://attributerouting.net](http://attributerouting.net). Při směrování atributů můžete zadat trasy zadáním poznámek k vašim akcím a řadičům.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>Webové rozhraní API 2 technologie ASP.NET

### <a name="attribute-routing"></a>Směrování atributů

Webové rozhraní API ASP.NET teď podporuje směrování atributů. díky příspěvku ve službě Tim McCall je autorem [http://attributerouting.net](http://attributerouting.net). Při směrování atributů můžete zadat své trasy webového rozhraní API zadáním poznámek k vašim akcím a řadičům takto:

[!code-csharp[Main](release-notes/samples/sample1.cs)]

Směrování atributů nabízí větší kontrolu nad identifikátory URI ve webovém rozhraní API. Můžete například snadno definovat hierarchii prostředků pomocí jediného kontroleru rozhraní API:

[!code-csharp[Main](release-notes/samples/sample2.cs)]

Směrování atributů také poskytuje pohodlný Syntax pro určení volitelných parametrů, výchozích hodnot a omezení trasy:

[!code-csharp[Main](release-notes/samples/sample3.cs)]

Další informace o směrování atributů najdete v tématu [Směrování atributů ve webovém rozhraní API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).

### <a name="oauth-20"></a>OAuth 2.0

Webové rozhraní API a šablony projektů aplikace na jedné stránce teď podporují autorizaci pomocí OAuth 2,0. OAuth 2,0 je architektura pro autorizaci přístupu klienta k chráněným prostředkům. Funguje pro celou řadu klientů, včetně prohlížečů a mobilních zařízení.

Podpora OAuth 2,0 vychází z nového middlewaru zabezpečení poskytnutého komponentami Microsoft OWIN pro ověřování držitele a implementaci role autorizačního serveru. Klienty je taky možné autorizovat pomocí autorizačního serveru organizace, jako je Azure Active Directory nebo ADFS ve Windows Serveru 2012 R2.

### <a name="odata-improvements"></a>Vylepšení OData

**Podpora pro $select, $expand, $batch a $value**

ASP.NET Web API OData teď má úplnou podporu pro $select, $expand a $value. Můžete také použít $batch pro vyžádání dávkování a zpracování sad změn.

Možnosti $select a $expand umožňují změnit tvar dat vrácených z koncového bodu OData. Další informace najdete v tématu [představujeme $Select a $expand podporu ve webovém rozhraní API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).

**Vylepšené rozšíření**

Formátovací moduly OData jsou teď rozšiřitelné. Můžete přidat metadata záznamů o atomech, podporu pojmenovaných datových proudů a mediálních odkazů, přidat poznámky k instanci a přizpůsobit způsob generování odkazů.

**Podpora typu bez typu**

Nyní můžete vytvářet služby OData bez nutnosti definovat typy CLR pro vaše typy entit. Místo toho můžou vaše řadiče OData brát nebo vracet instance **IEdmObject**, což jsou deserializace formátovacích modulů OData.

**Opětovné použití existujícího modelu**

Pokud už máte existující entity data model (EDM), můžete ho teď znovu použít přímo místo toho, abyste museli sestavovat nový. Například pokud používáte Entity Framework, můžete použít model EDM, který pro vás sestaví sestavení EF.

### <a name="request-batching"></a>Dávkování požadavků

Dávkování požadavků kombinuje více operací do jedné žádosti HTTP POST, aby snížilo zatížení sítě a poskytovalo hladší a méně konverzace uživatelského rozhraní. Webové rozhraní API ASP.NET teď podporuje několik strategií pro dávkování žádostí:

- Použijte koncový bod $batch služby OData.
- Zabalit více požadavků do jedné žádosti MIME na jednu část.
- Použijte vlastní formát dávkování.

Pokud chcete povolit dávkování žádostí, jednoduše přidejte trasu s obslužnou rutinou dávkování do vaší konfigurace webového rozhraní API:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

Můžete také řídit, zda jsou požadavky nebo provedeny postupně, nebo v libovolném pořadí.

### <a name="portable-aspnet-web-api-client"></a>Klient webového rozhraní API pro přenosné ASP.NET

Nyní můžete používat klienta webového rozhraní API ASP.NET k vytváření přenosných knihoven tříd, které fungují v aplikacích pro Windows Store a Windows Phone 8. Můžete také vytvářet přenosné formátovací moduly, které lze sdílet mezi klientem a serverem.

### <a name="improved-testability"></a>Vylepšená testování

Webové rozhraní API 2 významně usnadňuje testování řadičů rozhraní API na jednotkách. Stačí vytvořit instanci vašeho kontroleru rozhraní API se zprávou a konfigurací požadavku a pak zavolat metodu akce, kterou chcete otestovat. Pro metody akcí, které provádějí vytváření odkazů, je také snadné vytvořit třídu **UrlHelper** .

### <a name="ihttpactionresult"></a>IHttpActionResult

Teď můžete implementovat IHttpActionResult k zapouzdření výsledku vašich metod akce webového rozhraní API. IHttpActionResult vrácená z metody akce webového rozhraní API je prováděna modulem runtime webového rozhraní API ASP.NET a vytvoří výslednou odpověď na zprávu. IHttpActionResult může být vrácen z jakékoli akce webového rozhraní API pro zjednodušení testování částí implementace webového rozhraní API. Pro usnadnění práce se vydává řada implementací IHttpActionResult, včetně výsledků pro vracení specifických stavových kódů, formátovaného obsahu nebo odpovědí vydaných obsahem.

### <a name="httprequestcontext"></a>HttpRequestContext

Nový **HttpRequestContext** sleduje všechny stavy, které jsou svázané s požadavkem, ale není okamžitě k dispozici z požadavku. Pomocí nástroje **HttpRequestContext** můžete například získat data o trasách, objekt zabezpečení přidružený k žádosti, klientský certifikát, **UrlHelper** a kořen virtuální cesty. Můžete snadno vytvořit **HttpRequestContext** pro účely testování částí.

Vzhledem k tomu, že objekt zabezpečení pro požadavek se předá na **vlákno. CurrentPrincipal**, je teď k dispozici objekt zabezpečení po celou dobu životnosti žádosti, když je v kanálu webového rozhraní API.

### <a name="cors"></a>CORS

Díky dalšímu skvělému příspěvku z Brock Allen teď ASP.NET nyní plně podporuje sdílení žádostí mezi zdroji (CORS).

Zabezpečení prohlížečů brání webovým stránkám v odesílání požadavků AJAX na jinou doménu. [CORS](http://www.w3.org/TR/cors/) je standard W3C, který umožňuje serveru zmírnit zásady stejného zdroje. Při použití CORS může server explicitně umožnit některé žádosti o více zdrojů a současně odmítat jiné.

Webové rozhraní API 2 teď podporuje CORS, včetně automatického zpracování požadavků na kontrolu před výstupem. Další informace najdete v tématu [Povolení žádostí mezi zdroji v ASP.NET webovém rozhraní API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).

### <a name="authentication-filters"></a>Filtry ověřování

Filtry ověřování jsou novým druhem filtru ve webovém rozhraní API ASP.NET, který se spouští před autorizačními filtry v kanálu webového rozhraní API ASP.NET, a umožňuje pro všechny řadiče zadat logiku ověřování pro jednotlivé akce, řadiče nebo globálně. Ověřovací filtry zpracovávají přihlašovací údaje v žádosti a poskytují odpovídající objekt zabezpečení. Ověřovací filtry mohou také přidat výzvy ověřování v reakci na neautorizované žádosti.

### <a name="filter-overrides"></a>Přepsání filtru

Nyní můžete přepsat, které filtry se vztahují na danou metodu akce nebo kontroler, zadáním filtru pro přepsání. Filtry přepsání určují sadu typů filtrů, které by neměly být spuštěny pro daný obor (Action nebo Controller). To umožňuje přidat globální filtry, ale pak některé z určitých akcí nebo řadičů vyloučit.

### <a name="owin-integration"></a>Integrace OWIN

Webové rozhraní API ASP.NET teď plně podporuje OWIN a dají se spustit na jakémkoli hostiteli podporujícím OWIN. K dispozici je také **HostAuthenticationFilter** , který poskytuje integraci s ověřovacím systémem Owin.

Díky integraci OWIN můžete webové rozhraní API samostatně hostovat ve vlastním procesu společně s dalšími OWIN middleware, jako je například Signaler. Další informace najdete v tématu [použití Owin k samoobslužnému hostování ASP.NET webového rozhraní API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET signál 2,0

Následující části popisují funkce nástroje Signal 2,0.

- [Postavené na OWIN](#builtonowin)
- [MapHubs a MapConnection jsou nyní MapSignalR](#MapSignalR)
- [Podpora mezi doménami](#crossdomain)
- [Podpora iOS a Androidu prostřednictvím MonoTouch a MonoDroid](#mobile)
- [Přenosný klient .NET](#portable)
- [Nový balíček pro samoobslužné hostování](#selfhost)
- [Zpětně kompatibilní serverová podpora](#backwardcompat)
- [Odebrala se podpora serveru pro .NET 4,0.](#remove40)
- [Odeslání zprávy do seznamu klientů a skupin](#messagelist)
- [Odeslání zprávy konkrétnímu uživateli](#sendtouser)
- [Lepší podpora zpracování chyb](#errorhandling)
- [Snadnější testování částí Center](#unittesting)
- [Zpracování chyb JavaScriptu](#javascripterror)

Příklad, jak upgradovat existující projekt 1. x na Signaler 2,0, najdete v tématu [Upgrade aplikace Signal 1. x](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>Postavené na OWIN

Návěstí 2,0 je zcela postavené na [Owin (otevřené webové rozhraní pro .NET)](http://owin.org/). Tato změna způsobí, že proces nastavení signalizace je mnohem větší konzistence mezi aplikacemi, které jsou hostovány v rámci hostování webů a v místním prostředí, ale také vyžadovala několik změn rozhraní API.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs a MapConnection jsou nyní MapSignalR

Z důvodu kompatibility s normami OWIN byly tyto metody přejmenovány na `MapSignalR`. `MapSignalR`, který se volá bez parametrů, namapuje všechna centra (jako `MapHubs` ve verzi 1. x). Chcete-li namapovat jednotlivé objekty **PersistentConnection** , zadejte typ připojení jako parametr typu a příponu adresy URL pro připojení jako první argument.

Metoda `MapSignalR` je volána ve třídě spuštění Owin. Visual Studio 2013 obsahuje novou šablonu pro třídu pro spuštění Owin; Chcete-li použít tuto šablonu, postupujte následovně:

1. Klikněte pravým tlačítkem na projekt.
2. Vyberte **Přidat**, **Nová položka...**
3. Vyberte **spouštěcí třídu Owin**. Pojmenujte novou třídu **Startup.cs**.

Ve **webové aplikaci** se následně do procesu spouštění Owin přidá třída Startup Owin obsahující metodu `MapSignalR` pomocí položky v uzlu nastavení aplikace souboru Web. config, jak je znázorněno níže.

V **samoobslužné aplikaci**je spouštěcí třída předána jako parametr typu metody `WebApp.Start`.

**Mapování Center a připojení v návěsti 1. x (ze souboru globální aplikace ve webové aplikaci):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**Mapování Center a připojení v nástroji Signal 2,0 (ze souboru spouštěcí třídy Owin):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

V **samoobslužné aplikaci**je spouštěcí třída předána jako parametr typu pro metodu `WebApp.Start`, jak je znázorněno níže.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>Podpora mezi doménami

V návěsti 1. x byly požadavky křížové domény řízené jediným příznakem EnableCrossDomain. Tento příznak ovládá požadavky JSONP i CORS. Pro větší flexibilitu byla ze serverové součásti signalizace odebrána veškerá podpora CORS (klienti JavaScriptu pořád používají CORS normálně, pokud se zjistí, že ji prohlížeč podporuje) a byl k dispozici nový middleware OWIN pro podporu těchto scénářů.

Pokud je ve službě Signal-2,0 vyžadováno, aby klient (podporoval požadavky mezi doménami ve starších prohlížečích), bude muset být povolen explicitně nastavením `EnableJSONP` u objektu `HubConfiguration` na `true`, jak je uvedeno níže. Služba JSONP je ve výchozím nastavení zakázána, protože je méně bezpečná než CORS.

Chcete-li přidat nový middleware CORS do služby Signal 2,0, přidejte do projektu knihovnu `Microsoft.Owin.Cors` a zavolejte `UseCors` před middlewari signálu, jak je znázorněno v následující části.

**Do projektu se přidává soubor Microsoft. Owin. Cors**: Pokud chcete tuto knihovnu nainstalovat, spusťte následující příkaz v konzole správce balíčků:

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

Tento příkaz přidá do projektu verzi 2.0.0 balíčku.

**Volání UseCors**

Následující fragmenty kódu ukazují, jak implementovat připojení mezi doménami v návěsti 1. x a 2,0.

**Implementace požadavků mezi doménami v nástroji Signal 1. x (z globálního souboru aplikace)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**Implementace žádostí mezi doménami v nástroji Signal 2,0 (ze souboru C# kódu)**

Následující kód ukazuje, jak povolit CORS nebo JSONP v projektu Signal 2,0. Tato ukázka kódu používá `Map` a `RunSignalR` namísto `MapSignalR`, takže middleware CORS běží pouze pro požadavky na signál, které vyžadují podporu CORS (nikoli pro všechny přenosy v cestě zadané v `MapSignalR`.) `Map` lze také použít pro jakýkoli jiný middlewarový kód, který je třeba spustit pro konkrétní předponu adresy URL, nikoli pro celou aplikaci.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>Podpora iOS a Androidu prostřednictvím MonoTouch a MonoDroid

Pro klienty se systémy iOS a Android se přidala podpora pomocí komponent MonoTouch a MonoDroid z [knihovny Xamarin](https://xamarin.com/). Další informace o tom, jak je používat, najdete v tématu [použití komponent Xamarin](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln). Tyto součásti budou k dispozici v [Xamarin Storu](https://store.xamarin.com/) , až bude dostupná verze nástroje Signal RTW.

<a id="portable"></a># # # Přenosný klient .NET

Pro lepší vývoj pro různé platformy se klienti Silverlight, WinRT a Windows Phone nahradili jedním přenosným klientem rozhraní .NET, který podporuje tyto platformy:

- NET 4.5
- Silverlight 5
- WinRT (.NET pro aplikace pro Windows Store)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>Nový balíček pro samoobslužné hostování

Nyní je k dispozici balíček NuGet, který usnadňuje zahájení práce s nástrojem pro samoobslužné hostování (aplikace na základě signálů, které jsou hostovány v rámci procesu nebo jiné aplikace) místo hostování na webovém serveru. Chcete-li upgradovat projekt pro samoobslužné hostování sestavený pomocí nástroje Signal 1. x, odeberte balíček Microsoft. AspNet. Signaler. Owin a přidejte balíček Microsoft. AspNet. Signaler. SelfHost. Další informace o tom, jak začít s balíčkem pro samoobslužné hostování, najdete v tématu [kurz: samoobslužný hostitel signálu](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>Zpětně kompatibilní serverová podpora

V předchozích verzích nástroje Signal bylo nutné, aby byly verze balíčku signálu použité v klientovi a na serveru identické. Aby bylo možné podporovat silné klientské aplikace, které by bylo obtížné aktualizovat, služba Signal 2,0 nyní podporuje použití novější verze serveru se starším klientem. **Poznámka: návěstí 2,0 nepodporuje servery sestavené se staršími verzemi s novějšími klienty.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>Odebrala se podpora serveru pro .NET 4,0.

Návěstí 2,0 vynechalo podporu pro interoperabilitu serveru s .NET 4,0. .NET 4,5 musí být používáno se servery signálů 2,0. Pro Signal 2,0 je stále k dispozici klient .NET 4,0.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>Odeslání zprávy do seznamu klientů a skupin

V nástroji Signal 2,0 je možné odeslat zprávu pomocí seznamu ID klientů a skupin. Následující fragmenty kódu ukazují, jak to provést.

**Odeslání zprávy do seznamu klientů a skupin pomocí PersistentConnection**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**Odeslání zprávy do seznamu klientů a skupin pomocí Center**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>Odeslání zprávy konkrétnímu uživateli

Tato funkce umožňuje uživatelům určit, co je ID uživatele založené na IRequest prostřednictvím nového rozhraní IUserIdProvider:

**Rozhraní IUserIdProvider**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

Ve výchozím nastavení bude k dispozici implementace, která jako uživatelské jméno používá IPrincipal.Identity.Name uživatele.

V centrech budete moct posílat zprávy těmto uživatelům pomocí nového rozhraní API:

**Použití rozhraní API klientů. User**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>Lepší podpora zpracování chyb

Uživatelé teď můžou vyvolávat **HubException** z jakéhokoli vyvolání centra. Konstruktor **HubException** může přebírat zprávu řetězce a objekt extra chybové údaje. Nástroj Signal vygeneruje výjimku automaticky a pošle ji klientovi, kde bude použit k zamítnutí nebo selhání volání metody rozbočovače.

Nastavení **Zobrazit podrobné výjimky centra** nemá žádné vliv na **HubException** , které se odesílají zpátky do klienta, nebo ne. Vždycky se posílá.

**Kód na straně serveru ukazující odeslání HubException klientovi**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**Kód klienta JavaScriptu, který ukazuje reakci na HubException odeslaný ze serveru**

[!code-html[Main](release-notes/samples/sample16.html)]

**Kód klienta .NET, který ukazuje odpověď na HubException odeslaný ze serveru**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>Snadnější testování částí Center

Návěstí 2,0 obsahuje rozhraní s názvem `IHubCallerConnectionContext` v centrech, které usnadňuje vytváření postranních volání na straně klienta. Následující fragmenty kódu ukazují použití tohoto rozhraní s oblíbenými testovacími [xUnit.NET](https://github.com/xunit/xunit) a [MOQ](https://code.google.com/p/moq/).

**Signál pro testování částí pomocí xUnit.net**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Signál pro testování částí pomocí MOQ**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>Zpracování chyb JavaScriptu

V nástroji Signal 2,0 všechny zpětná volání zpracovávající chyby JavaScriptu vrátí objekty chyb JavaScriptu místo nezpracovaných řetězců. Díky tomu může signál signalizovat bohatší informace obslužné rutiny chyb. Vnitřní výjimku můžete získat z vlastnosti `source` chyby.

**JavaScriptový kód klienta, který zpracovává výjimku spustit. neúspěch**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>Nový systém členství v ASP.NET

ASP.NET Identity je nový systém členství pro aplikace ASP.NET. ASP.NET Identity usnadňuje integraci dat profilů specifických pro uživatele s daty aplikací. ASP.NET Identity také umožňuje zvolit model trvalosti pro profily uživatelů v aplikaci. Data můžete ukládat do databáze SQL Server nebo do jiného úložiště dat, včetně úložišť dat NoSQL, jako jsou například Azure Storage tabulky. Další informace naleznete v tématu [jednotlivé uživatelské účty](creating-web-projects-in-visual-studio.md#indauth) při **vytváření ASP.NET webových projektů v Visual Studio 2013**.

### <a name="claims-based-authentication"></a>Ověřování na základě deklarací

ASP.NET nyní podporuje ověřování založené na deklaracích, kde je identita uživatele reprezentována jako sada deklarací z důvěryhodného vystavitele. Uživatele je možné ověřit pomocí uživatelského jména a hesla, které jsou zachovány v databázi aplikace, nebo pomocí poskytovatelů sociálních identit (například účty Microsoft, Facebook, Google, Twitter) nebo pomocí účtů organizace prostřednictvím Azure Active Directory nebo Active Directory Federation Services (AD FS) (ADFS).

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Integrace s Azure Active Directory a službou Windows Server Active Directory

Nyní můžete vytvářet ASP.NET projekty, které pro ověřování používají Azure Active Directory nebo Windows Server Active Directory (AD). Další informace najdete v tématu [účty organizace](creating-web-projects-in-visual-studio.md#orgauth) při **vytváření ASP.NET webových projektů v Visual Studio 2013**.

### <a name="owin-integration"></a>Integrace OWIN

Ověřování ASP.NET je teď založené na middlewaru OWIN, který se dá použít na jakémkoli hostiteli založeném na OWIN. Další informace o OWIN najdete v části následující [součásti Microsoft Owin](#TOC7) .

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Komponenty Microsoft OWIN

[Open Web Interface for .NET](http://owin.org/) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi. OWIN odpojí webovou aplikaci od serveru a vytváří tak webové aplikace Host-nezávislá. Můžete například hostovat webovou aplikaci založenou na OWIN ve službě IIS nebo její vlastní hostování ve vlastním procesu.

Změny zavedené v součástech Microsoft OWIN (označované také jako projekt Katana) zahrnují nové součásti serveru a hostitele, nové pomocné knihovny a middlewaru a nový middleware ověřování.

Další informace o OWIN a Katana najdete v tématu [co je nového v Owin a Katana](../../../aspnet/overview/owin-and-katana/index.md).

**Poznámka: aplikace [Owin](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) nejde spustit v klasickém režimu služby IIS. musí být spuštěny v integrovaném režimu.**

**Poznámka: aplikace [Owin](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) musí běžet v úplném vztahu důvěryhodnosti.**

### <a name="new-servers-and-hosts"></a>Nové servery a hostitelé

V této verzi byly přidány nové komponenty, které umožňují scénáře pro samoobslužné hostování. Mezi tyto komponenty patří následující balíčky NuGet:

- **Microsoft. Owin. Host. HttpListener**. Poskytuje server OWIN, který používá **HttpListener** k naslouchání požadavkům HTTP a jejich směrování do kanálu Owin.
- **Microsoft. Owin. hosting** poskytuje knihovnu pro vývojáře, kteří chtějí sami HOSTOVAT kanál Owin ve vlastním procesu, jako je například Konzolová aplikace nebo služba systému Windows.
- **OwinHost**. Poskytuje samostatný spustitelný soubor, který zalomí `Microsoft.Owin.Hosting` a umožňuje vlastní hostování kanálu OWIN bez nutnosti psát vlastní hostitelskou aplikaci.

Kromě toho balíček `Microsoft.Owin.Host.SystemWeb` nyní umožňuje middlewaru poskytovat pokyn serveru **SystemWeb** , který označuje, že middleware by měly být volány během konkrétní fáze ASP.NET kanálu. Tato funkce je zvláště užitečná pro middleware ověřování, který by měl běžet na začátku v kanálu ASP.NET.

### <a name="helper-libraries-and-middleware"></a>Pomocné knihovny a middleware

I když můžete zapisovat komponenty OWIN jenom pomocí funkcí a definic typů ze specifikace OWIN, nový balíček `Microsoft.Owin` poskytuje uživatelsky přívětivější sadu abstrakcí. Tento balíček kombinuje několik starších balíčků (například `Owin.Extensions`, `Owin.Types`) do jednoho dobře strukturovaného objektového modelu, který lze následně snadno použít v jiných komponentách OWIN. Ve skutečnosti většina komponent Microsoft OWIN nyní používá tento balíček.

> [!NOTE]
> Aplikace [Owin](http://www.owin.org) nemůžou běžet v klasickém režimu služby IIS. musí být spuštěny v integrovaném režimu.

> [!NOTE]
> [Owin](http://www.owin.org) aplikace musí být spuštěny v úplném vztahu důvěryhodnosti.

Tato verze zahrnuje také balíček Microsoft. Owin. Diagnostics, který zahrnuje middleware k ověření běžící aplikace OWIN a middlewaru chybových stránek, které vám pomůžou prozkoumat selhání.

### <a name="authentication-components"></a>Komponenty ověřování

K dispozici jsou následující komponenty pro ověřování.

- **Microsoft. Owin. Security. Active**. Umožňuje ověřování pomocí místních nebo cloudových adresářových služeb.
- **Microsoft. Owin. Security. cookies** umožňuje ověřování pomocí souborů cookie. Tento balíček se dřív jmenoval `Microsoft.Owin.Security.Forms`.
- **Microsoft. Owin. Security. Facebook** umožňuje ověřování pomocí služby Facebook na Facebooku.
- **Microsoft. Owin. Security. Google** umožňuje ověřování pomocí služby Google založené na OpenID.
- **Microsoft. Owin. Security. JWT** umožňuje ověřování pomocí tokenů JWT.
- **Microsoft. Owin. Security. MicrosoftAccount** umožňuje ověřování pomocí účtů Microsoft.
- **Microsoft. Owin. Security. OAuth**. Poskytuje autorizační Server OAuth a také middleware pro ověřování nosných tokenů.
- **Microsoft. Owin. Security. Twitter** umožňuje ověřování pomocí služby Twitter na bázi OAuth.

Tato verze zahrnuje také balíček `Microsoft.Owin.Cors`, který obsahuje middleware pro zpracování požadavků protokolu HTTP mezi zdroji.

> [!NOTE]
> V konečné verzi Visual Studio 2013 byla odebrána podpora pro podpis JWT.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Seznam nových funkcí a dalších změn v Entity Framework 6 najdete v části [Entity Framework Historie verzí](https://msdn.com/data/jj574253).

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3 obsahuje následující nové funkce:

- Podpora pro úpravu karet. Dříve při použití možnosti **zachovat záložky** nefungovala v aplikaci Visual Studio příkaz **Formát dokumentu** , automatické odsazení a automatické formátování. Tato změna opravuje formátování sady Visual Studio pro kód Razor pro formátování tabulátoru.
- Podpora pravidel pro přepis adres URL při generování odkazů
- Odebrání transparentního atributu zabezpečení
  > [!NOTE]
  > Toto je zásadní změna a má Razor 3 kompatibilní s MVC4 a starším, zatímco Razor 2 je nekompatibilní s MVC5 nebo sestaveními kompilovanými proti MVC5.

Problémy Razor 3 opravené ve Visual Studio 2013 z předběžných verzí najdete [tady](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>Pozastavení aplikace ASP.NET

Pozastavení aplikace ASP.NET je funkce měnící hru v .NET Framework 4.5.1, která odmění uživatelské prostředí a ekonomický model pro hostování velkých počtů ASP.NET webů v jednom počítači. Další informace najdete v tématu [pozastavení aplikace ASP.NET – reagující na sdílené webové hostování .NET](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>Známé problémy a zásadní změny

Tato část popisuje známé problémy a zásadní změny ASP.NET and Web Tools pro Visual Studio 2013.

### <a name="nuget"></a>NuGet

- [Nové obnovení balíčku nefunguje na mono při použití souboru sln](https://nuget.codeplex.com/workitem/3596) – bude opraveno v nadcházejícím stažení NuGet. exe a aktualizace [balíčku NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) .
- [Nové obnovení balíčku nefunguje s WIX projekty](https://nuget.codeplex.com/workitem/3598) – bude opraveno v nadcházejícím stažení NuGet. exe a aktualizace [balíčku NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) .
- [Automatické obnovení balíčku nefunguje pro projekty ve složce řešení](https://nuget.codeplex.com/workitem/3625) – bude opraveno v NuGet 2,8.

### <a name="aspnet-web-api"></a>Webové rozhraní API ASP.NET

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)` nevrací `IQueryable<T>` vždy, protože jsme přidali podporu pro `$select` a `$expand`.

    Naše předchozí ukázky pro `ODataQueryOptions<T>` vždycky přetypování návratové hodnoty z `ApplyTo` na `IQueryable<T>`. To dříve fungovalo, protože možnosti dotazu, které jsme dříve podporovali (`$filter`, `$orderby`, `$skip`, `$top`) nemění tvar dotazu. Teď, když podporujeme `$select` a `$expand` návratovou hodnotu z `ApplyTo` nebudou `IQueryable<T>` vždycky.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    Pokud používáte vzorový kód ze starší verze, bude pokračovat v práci, pokud klient neodešle `$select` a `$expand`. Pokud však chcete podporovat `$select` a `$expand` je nutné tento kód změnit.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **Request. URL nebo Třída requestContext. URL má během dávkového požadavku hodnotu null.**

    V případě dávkového zpracování má **UrlHelper** při použití z **Request. URL** nebo **Třída requestContext. URL**hodnotu null.

    Tento problém je momentálně sledován: [BatchRequestContext. URL má pro požadavek Batch hodnotu null](http://aspnetwebstack.codeplex.com/workitem/1301).

    Alternativním řešením tohoto problému je vytvoření nové instance **UrlHelper**, jako v následujícím příkladu:

    **Vytváření nové instance třídy UrlHelper**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. Pokud máte zobrazení, která se AntiForgerToken ověřováním, při použití MVC5 a OrgAuth může při odesílání dat do zobrazení docházet k následující chybě:

    **Chyba:**

    *Chyba serveru v aplikaci/*

    <em>Deklarace identity typu<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>nebo<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>nebyla v poskytnutém hodnota ClaimsIdentity nalezena. Pokud chcete povolit podporu tokenů ochrany proti padělání pomocí ověřování založeného na deklaracích, ověřte prosím, jestli nakonfigurovaný zprostředkovatel deklarací poskytuje obě tyto deklarace na hodnota ClaimsIdentity instancích, které generuje. Pokud nakonfigurované zprostředkovatel deklarací místo toho používá jiný typ deklarace identity jako jedinečný identifikátor, dá se nakonfigurovat nastavením static Property AntiForgeryConfig. UniqueClaimTypeIdentifier.</em>

    **Alternativní řešení**:

    Přidejte následující řádek do Global. asax k opravě:

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    Tato akce bude opravena pro další vydání.
2. Po upgradu aplikace MVC4 na MVC5 Sestavte řešení a spusťte ho. Měla by se zobrazit následující chyba:

    Určitého System. Web. webpages. Razor. Configuration. HostSection nelze přetypovat na [B] System. Web. webpages. Razor. Configuration. HostSection. Typ A pochází z ' System. Web. webpages. Razor, Version = 2.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' v kontextu ' default ' na pozici ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ System. Web. webpages. Razor. dll '. Typ B pochází z ' System. Web. webpages. Razor, Version = 3.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' v kontextu ' default ' na pozici ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01 \ System. Web. webpages. Razor. dll '.

    Chcete-li opravit uvedenou chybu, otevřete *všechny* soubory Web. config (včetně těch ve složce views) ve vašem projektu a proveďte následující kroky:

   1. Aktualizuje všechny výskyty verze "4.0.0.0" z "System. Web. Mvc" na "5.0.0.0".
   2. Aktualizuje všechny výskyty verze "2.0.0.0" z "System. Web. helps", &quot;System. Web. webpages&quot; a &quot;System. Web. webpages. Razor&quot; na "3.0.0.0".

      Například po provedení výše uvedených změn by vazby sestavení měly vypadat takto:

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      Informace o tom, jak upgradovat projekty MVC 4 na MVC 5, najdete v tématu [Postup upgradu ASP.NET MVC 4 a projektu webového rozhraní API na ASP.NET MVC 5 a webové rozhraní API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).
3. Při ověřování na straně klienta s nenáročným ověřováním jQuery je ověřovací zpráva někdy nesprávná pro element input HTML s typem = ' Number '. Při zadání neplatného čísla namísto správné zprávy, která vyžaduje platné číslo, se zobrazí chyba ověření požadované hodnoty (pole stáří je povinné).

    Tento problém se běžně objevuje s generovaným kódem pro model s vlastností Integer v zobrazeních vytvořit a upravit.

    Pokud chcete tento problém obejít, změňte pomocníka editoru z:

    `@Html.EditorFor(person => person.Age)`

    Komu:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 už nepodporuje částečnou důvěryhodnost. Projekty, které propojuje s binárními soubory MVC nebo WebAPI, by měly odebrat atribut [atributy SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) a atribut [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) . Odebrání těchto atributů odstraní chyby kompilátoru, například následující.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > Všimněte si, že v důsledku vedlejších účinků nelze ve stejné aplikaci použít sestavení 4,0 a 5,0. Je potřeba je aktualizovat na 5,0.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>Šablona SPA s autorizací na Facebooku může způsobit nestabilitu v IE, pokud je web hostovaný v zóně intranetu.

Šablona SPA poskytuje externí přihlášení pomocí Facebooku. Když je projekt vytvořený pomocí šablony místně spuštěný, přihlášení může způsobit chybu aplikace IE.

Řešení:

1. Hostování webu v zóně Internet; ani

2. Otestujte scénář v jiném prohlížeči než IE.

### <a name="web-forms-scaffolding"></a>Webové formuláře – generování uživatelského rozhraní

Generování uživatelského rozhraní webových formulářů z VS2013 bylo odebráno a bude k dispozici v budoucí aktualizaci sady Visual Studio. Můžete však i nadále používat generování uživatelského rozhraní v rámci projektu webových formulářů přidáním závislosti MVC a generováním generování uživatelského rozhraní pro MVC. Projekt bude obsahovat kombinaci webových formulářů a MVC.

Chcete-li přidat MVC do projektu webových formulářů, přidejte novou vygenerované položky a vyberte **závislosti MVC 5**. V závislosti na tom, jestli potřebujete všechny soubory obsahu, jako jsou skripty, vyberte buď minimální, nebo úplné. Pak přidejte vygenerované položky pro MVC, které vytvoří zobrazení a kontroler v projektu.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>Rozhraní API pro MVC a webové rozhraní API – chyba při nenalezení protokolu HTTP 404

Pokud při přidávání vygenerované položky do projektu dojde k chybě, je možné, že váš projekt zůstane v nekonzistentním stavu. Některé změny generované generováním uživatelského rozhraní se vrátí zpátky, ale jiné změny, třeba nainstalované balíčky NuGet, se nebudou vracet zpátky. Pokud se změny konfigurace směrování vrátí zpět, uživatelům se při přechodu na vygenerované položky zobrazí chyba HTTP 404.

Alternativní řešení:

- Pokud chcete tuto chybu pro MVC opravit, přidejte novou vygenerované položky a vyberte závislosti MVC 5 (minimální nebo plné). Tento proces přidá všechny požadované změny do projektu.
- Oprava této chyby pro webové rozhraní API:

  1. Přidejte do projektu třídu WebApiConfig.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. Nakonfigurujte WebApiConfig. Register v aplikaci\_metodu Start v Global. asax následujícím způsobem:

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
