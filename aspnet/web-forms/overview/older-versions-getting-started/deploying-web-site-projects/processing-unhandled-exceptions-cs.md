---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
title: Zpracování neošetřených výjimek (C#) | Microsoft Docs
author: rick-anderson
description: Pokud dojde k chybě za běhu u webové aplikace v produkčním prostředí, je důležité informovat vývojáře a protokolovat chybu, aby mohla být diagnostikována v La...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 5bc1afd5-2484-4528-b158-ab218ba150e8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 27d827238d944f86cd913d2b8ecd12729b99f391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629267"
---
# <a name="processing-unhandled-exceptions-c"></a>Zpracování neošetřených výjimek (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Zobrazit nebo stáhnout ukázkový kód](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs/samples) ([Jak stáhnout](/aspnet/core/tutorials/index#how-to-download-a-sample))

> Pokud dojde k běhové chybě na webové aplikaci v produkčním prostředí, je důležité informovat vývojáře a protokolovat chybu, aby mohla být diagnostikována v pozdějším časovém bodě. Tento kurz poskytuje přehled o tom, jak ASP.NET zpracovává běhové chyby a vypadá jedním ze způsobů, jak mít vlastní kód proveden kdykoli po neošetřené bublině výjimky až do modulu runtime ASP.NET.

## <a name="introduction"></a>Úvod

Pokud dojde k neošetřené výjimce v aplikaci ASP.NET, poukáže se až na modul runtime ASP.NET, který vyvolá událost `Error` a zobrazí příslušnou chybovou stránku. Existují tři různé typy chybových stránek: Chyba za běhu žlutá obrazovka smrti (YSOD); Podrobnosti výjimky YSOD; a vlastní chybové stránky. V [předchozím kurzu](displaying-a-custom-error-page-cs.md) jsme nakonfigurovali aplikaci tak, aby pro vzdálené uživatele používala vlastní chybovou stránku, a podrobnosti o výjimce YSOD pro uživatele, kteří navštěvují místně.

Použití vlastní uživatelsky přívětivé chybové stránky, která se shoduje s vzhledem a chováním webu, je preferována Výchozí chyba modulu runtime YSOD, ale zobrazení vlastní chybové stránky je jenom jedna část komplexního řešení pro zpracování chyb. Pokud dojde k chybě v aplikaci v produkčním prostředí, je důležité, aby byli vývojáři upozorněni na chybu, aby mohli odstát příčinu výjimky a vyřešit ji. Kromě toho by se měly zaprotokolovat podrobnosti o chybě, aby bylo možné chybu prozkoumat a diagnostikovat v pozdějším časovém bodě.

V tomto kurzu se dozvíte, jak získat přístup k podrobnostem o neošetřené výjimce tak, aby mohly být zaprotokolovány a vývojář upozorněni. V těchto dvou kurzech, které následují po provedení této akce, prozkoumejte knihovny protokolování chyb, které po bitu konfigurace automaticky upozorní vývojáře na chyby za běhu a zaprotokolují jejich podrobnosti.

> [!NOTE]
> Informace, které jsou zkoumány v tomto kurzu, jsou nejužitečnější, pokud potřebujete zpracovat neošetřené výjimky v některém jedinečném nebo vlastním přizpůsobeném způsobem. V případech, kdy stačí pouze zaprotokolovat výjimku a odeslat oznamovateli výstrahu pomocí knihovny protokolování chyb, je způsob, jak jít. Další dva kurzy poskytují přehled dvou takových knihoven.

## <a name="executing-code-when-theerrorevent-is-raised"></a>Spouštění kódu při vyvolání události`Error`

Události poskytují objekt mechanismus pro signalizaci, že došlo k něčemu nějakého zajímavého, a pro jiný objekt ke spuštění kódu v reakci. Jako vývojář ASP.NET jste zvyklí v souvislosti s událostmi. Pokud chcete spustit nějaký kód, když návštěvník klikne na konkrétní tlačítko, vytvoříte obslužnou rutinu události pro `Click` událost tlačítka a umístíte svůj kód. Vzhledem k tomu, že modul runtime ASP.NET vyvolává svou [událost`Error`](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) vždy, když dojde k neošetřené výjimce, následuje postup, který by měl kód pro protokolování podrobností o chybě jít v obslužné rutině události. Ale jak vytvoříte obslužnou rutinu události pro událost `Error`?

Událost `Error` je jednou z mnoha událostí ve [třídě`HttpApplication`](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) , která se vyvolala v určitých fázích kanálu http během životnosti žádosti. Například [událost`BeginRequest`](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx) `HttpApplication` třídy je vyvolána na začátku každého požadavku; jeho [událost`AuthenticateRequest`](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) je vyvolána, když modul zabezpečení identifikoval žadatele. Tyto `HttpApplication` události dávají vývojářům stránky způsob, jak provádět vlastní logiku v různých místech životního cyklu žádosti.

Obslužné rutiny událostí `HttpApplication` lze umístit do speciálního souboru s názvem `Global.asax`. Chcete-li vytvořit tento soubor na svém webu, přidejte novou položku do kořenového adresáře webu pomocí šablony globální třídy aplikace s názvem `Global.asax`.

[![](processing-unhandled-exceptions-cs/_static/image2.png)](processing-unhandled-exceptions-cs/_static/image1.png)

**Obrázek 1**: Přidání `Global.asax` do webové aplikace  
([Kliknutím zobrazíte obrázek v plné velikosti.](processing-unhandled-exceptions-cs/_static/image3.png))

Obsah a struktura `Global.asax`ho souboru vytvořeného v aplikaci Visual Studio se mírně liší podle toho, zda používáte projekt webové aplikace (WAP) nebo webový projekt (WSP). Pomocí WAP se `Global.asax` implementuje jako dva samostatné soubory – `Global.asax` a `Global.asax.cs`. `Global.asax` soubor neobsahuje žádnou hodnotu, ale direktivu `@Application`, která odkazuje na soubor `.cs`; obslužné rutiny událostí pro důležité jsou definovány v souboru `Global.asax.cs`. Pro WSPs je vytvořen pouze jeden soubor, `Global.asax`a obslužné rutiny událostí jsou definovány v bloku `<script runat="server">`.

`Global.asax` soubor vytvořený v šabloně WAP šablonou globální třídy aplikace sady Visual Studio obsahuje obslužné rutiny událostí s názvem `Application_BeginRequest`, `Application_AuthenticateRequest`a `Application_Error`, které jsou obslužnými rutinami událostí `HttpApplication` `BeginRequest`, `AuthenticateRequest`a `Error`v uvedeném pořadí. K dispozici jsou také obslužné rutiny událostí s názvem `Application_Start`, `Session_Start`, `Application_End`a `Session_End`, což jsou obslužné rutiny událostí, které se aktivují při spuštění webové aplikace, při spuštění nové relace, při ukončení aplikace a ukončení relace v uvedeném pořadí. `Global.asax` soubor vytvořený v WSP pomocí sady Visual Studio obsahuje jenom obslužné rutiny událostí `Application_Error`, `Application_Start`, `Session_Start`, `Application_End`a `Session_End`.

> [!NOTE]
> Při nasazování aplikace ASP.NET potřebujete zkopírovat soubor `Global.asax` do provozního prostředí. `Global.asax.cs` soubor, který je vytvořen v WAP, není nutné kopírovat do produkčního prostředí, protože tento kód je zkompilován do sestavení projektu.

Obslužné rutiny událostí vytvořené šablonou globální třídy aplikace sady Visual Studio nejsou vyčerpávající. Můžete přidat obslužnou rutinu události pro jakoukoli událost `HttpApplication` pojmenováním `Application_EventName`obslužné rutiny události. Do souboru `Global.asax` například můžete přidat následující kód, který vytvoří obslužnou rutinu události pro [událost`AuthorizeRequest`](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx):

[!code-cs[Main](processing-unhandled-exceptions-cs/samples/sample1.cs)]

Podobně můžete odebrat jakékoli obslužné rutiny událostí vytvořené šablonou globální třídy aplikace, které nejsou potřeba. Pro tento kurz vyžadujeme pro událost `Error` jenom obslužnou rutinu události; Nebojte se odebrat další obslužné rutiny událostí ze souboru `Global.asax`.

> [!NOTE]
> *Moduly HTTP* nabízejí jiný způsob definování obslužných rutin událostí pro `HttpApplication` události. Moduly HTTP jsou vytvořeny jako soubor třídy, který lze umístit přímo do projektu webové aplikace nebo rozdělit do samostatné knihovny tříd. Vzhledem k tomu, že je možné je rozdělit do knihovny tříd, moduly HTTP nabízejí flexibilnější a opakovaně použitelný model pro vytváření obslužných rutin událostí `HttpApplication`. Vzhledem k tomu, že `Global.asax` soubor je specifický pro webovou aplikaci, ve které se nachází, moduly HTTP lze zkompilovat do sestavení, kdy je potřeba přidat modul HTTP na web stejně snadno jako vyřazení sestavení ve složce `Bin` a registrace modulu v `Web.config`. Tento kurz se nezobrazuje při vytváření a používání modulů HTTP, ale dvě knihovny protokolování chyb, které se používají v následujících dvou kurzech, se implementují jako moduly HTTP. Další informace o výhodách modulů HTTP najdete v tématu [použití modulů HTTP a obslužných rutin k vytvoření zapojitelné součásti ASP.NET](https://msdn.microsoft.com/library/aa479332.aspx).

## <a name="retrieving-information-about-the-unhandled-exception"></a>Načítají se informace o neošetřené výjimce.

V tomto okamžiku máme soubor Global. asax s obslužnou rutinou události `Application_Error`. Když se spustí Tato obslužná rutina události, musíme sdělit vývojářům chybu a zaznamenat její podrobnosti. Aby bylo možné tyto úlohy provést, je nejdříve potřeba určit podrobnosti o výjimce, která byla vyvolána. K načtení podrobností o neošetřené výjimce, která způsobila vyvolání události `Error`, použijte [metodu`GetLastError`](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx) objektu serveru.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample2.cs)]

Metoda `GetLastError` vrátí objekt typu `Exception`, což je základní typ pro všechny výjimky v .NET Framework. Nicméně v kódu výše přetypování objekt výjimky vrácený `GetLastError` do objektu `HttpException`. Pokud dojde k vyvolání události `Error`, protože při zpracování prostředku ASP.NET došlo k výjimce, vyvolaná výjimka je zabalena do `HttpException`. Chcete-li získat skutečnou výjimku, která vyvolala událost chyby, použijte vlastnost `InnerException`. Pokud byla událost `Error` vyvolána z důvodu výjimky založené na protokolu HTTP, jako je například požadavek na neexistující stránku, je vyvolána `HttpException`, ale nemá vnitřní výjimku.

Následující kód používá `GetLastErrormessage` k načtení informací o výjimce, která aktivovala událost `Error` a uložení `HttpException` do proměnné s názvem `lastErrorWrapper`. Poté uloží typ, zprávu a trasování zásobníku z prvotní výjimky ve třech proměnných řetězce, zkontroluje, zda je `lastErrorWrapper` skutečnou výjimkou, která aktivovala událost `Error` (v případě výjimek založených na protokolu HTTP), nebo je pouze obálkou pro výjimku, která byla vyvolána při zpracování žádosti.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample3.cs)]

V tomto okamžiku máte všechny informace, které potřebujete k psaní kódu, který bude protokolovat podrobnosti o výjimce do databázové tabulky. Můžete vytvořit databázovou tabulku se sloupci pro každou z podrobností o chybě, která je zajímavá – typ, zprávu, trasování zásobníku a tak dále, a další užitečné informace, jako je adresa URL požadované stránky a jméno aktuálně přihlášeného uživatele. V `Application_Error` obslužné rutině události se pak můžete připojit k databázi a vložit do tabulky záznam. Podobně můžete přidat kód pro upozornění vývojáře chyby prostřednictvím e-mailu.

Knihovny protokolování chyb v následujících dvou kurzech poskytují funkce, které jsou vyhodnoceny jako dostupné, takže není potřeba sestavovat Toto protokolování chyb a oznámení sami. Nicméně pro ilustraci, že je vyvolána událost `Error` a že se obslužná rutina `Application_Error` události dá použít k protokolování podrobností o chybách a oznámení vývojáři, přidáme kód, který upozorní vývojáře, když dojde k chybě.

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>Upozorňování vývojáře, když dojde k neošetřené výjimce

Pokud dojde k neošetřené výjimce v produkčním prostředí, je důležité upozornit vývojového týmu, aby mohli vyhodnotit chybu a určit, jaké akce je třeba provést. Například pokud dojde k chybě při připojování k databázi, budete muset dvakrát ověřit připojovací řetězec a případně otevřít lístek podpory ve vaší společnosti pro hostování vašeho webu. Pokud došlo k výjimce z důvodu chyby programování, může být nutné přidat další kód nebo logiku ověřování, aby se předešlo takovým chybám v budoucnu.

.NET Framework třídy v [oboru názvů`System.Net.Mail`](https://msdn.microsoft.com/library/system.net.mail.aspx) usnadňují posílání e-mailů. [Třída`MailMessage`](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) představuje e-mailovou zprávu a má vlastnosti jako `To`, `From`, `Subject`, `Body`a `Attachments`. `SmtpClass` slouží k odeslání objektu `MailMessage` pomocí zadaného serveru SMTP; nastavení serveru SMTP lze zadat programově nebo deklarativně v [prvku`<system.net>`](https://msdn.microsoft.com/library/6484zdc1.aspx) v `Web.config file`. Další informace o posílání e-mailových zpráv v aplikaci ASP.NET najdete v článku o [posílání e-mailů v ASP.NET](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)a v tématu [Nejčastější dotazy k System .NET. mailu](http://systemnetmail.com/).

> [!NOTE]
> Element `<system.net>` obsahuje nastavení serveru SMTP používaného třídou `SmtpClient` při posílání e-mailu. Vaše společnost hostující váš web má pravděpodobně server SMTP, který můžete použít k odeslání e-mailu z aplikace. Informace o nastaveních serveru SMTP, která byste měli použít ve své webové aplikaci, najdete v části věnované podpoře svého webového hostitele.

Přidejte následující kód do obslužné rutiny události `Application_Error` k odeslání e-mailu vývojáři, když dojde k chybě:

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample4.cs)]

I když je výše uvedený kód poměrně dlouhý, je hromadně vytvořen kód HTML, který se zobrazí v e-mailu odeslanému vývojáři. Kód začíná odkazem na `HttpException` vrácenou metodou `GetLastError` (`lastErrorWrapper`). Skutečná výjimka, která byla vyvolána požadavkem, je načtena prostřednictvím `lastErrorWrapper.InnerException` a je přiřazena k proměnné `lastError`. Informace o typu, zprávě a trasování zásobníku jsou načteny z `lastError` a uloženy ve třech řetězcových proměnných.

Dále je vytvořen objekt `MailMessage` s názvem `mm`. Tělo e-mailu je formátováno ve formátu HTML a zobrazuje adresu URL požadované stránky, jméno aktuálně přihlášeného uživatele a informace o výjimce (typ, zpráva a trasování zásobníku). Jednou ze studených věcí o `HttpException` třídy je, že můžete vygenerovat kód HTML, který se používá k vytvoření podrobného povýšení obrazovky s podrobnostmi o smrti (YSOD) voláním [metody GetHtmlErrorMessage](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx). Tato metoda se tady používá k načtení podrobností o výjimce YSOD značky a jejímu přidání do e-mailu jako přílohy. Jedno slovo s upozorněním: Pokud výjimka, která aktivovala událost `Error`, byla výjimkou založenou na protokolu HTTP (například požadavek na neexistující stránku), vrátí metoda `GetHtmlErrorMessage` `null`.

Posledním krokem je odeslání `MailMessage`. To se provádí vytvořením nové metody `SmtpClient` a voláním její metody `Send`.

> [!NOTE]
> Před použitím tohoto kódu ve webové aplikaci budete chtít změnit hodnoty v `ToAddress` a `FromAddress` konstanty z support@example.com na libovolnou e-mailovou adresu, ze které se má e-mail s oznámením o chybách Odeslat a odkud z něj pochází. Také budete muset zadat nastavení serveru SMTP v části `<system.net>` v `Web.config`. Pokud chcete zjistit, jaké nastavení serveru SMTP chcete použít, obraťte se na svého poskytovatele webového hostitele.

V případě, že je tento kód na místě, kdy je k dispozici chyba, vývojář pošle e-mailovou zprávu, která shrnuje chybu a obsahuje YSOD. V předchozím kurzu jsme ukázali chybu za běhu, a to návštěvou Žánr. aspx a předáním neplatné `ID`é hodnoty pomocí řetězce dotazu, jako je `Genre.aspx?ID=foo`. Navštívení stránky pomocí souboru `Global.asax` v místě přináší stejné uživatelské prostředí jako v předchozím kurzu – ve vývojovém prostředí budete nadále zobrazovat podrobnosti o výjimce žlutá obrazovka smrti, zatímco v produkčním prostředí uvidíte vlastní chybovou stránku. Kromě tohoto existujícího chování vývojář posílá e-mail.

**Obrázek 2** ukazuje e-mail přijatý při návštěvě `Genre.aspx?ID=foo`. Tělo e-mailu shrnuje informace o výjimce, zatímco `YSOD.htm` příloha zobrazuje obsah zobrazený v podrobnostech výjimky YSOD (viz **Obrázek 3**).

[![](processing-unhandled-exceptions-cs/_static/image5.png)](processing-unhandled-exceptions-cs/_static/image4.png)

**Obrázek 2**: vývojář pošle e-mailové oznámení vždy, když dojde k neošetřené výjimce.  
([Kliknutím zobrazíte obrázek v plné velikosti.](processing-unhandled-exceptions-cs/_static/image6.png))

[![](processing-unhandled-exceptions-cs/_static/image8.png)](processing-unhandled-exceptions-cs/_static/image7.png)

**Obrázek 3**: e-mailové oznámení obsahují podrobnosti o výjimce YSOD jako příloha.  
([Kliknutím zobrazíte obrázek v plné velikosti.](processing-unhandled-exceptions-cs/_static/image9.png))

## <a name="what-about-using-the-custom-error-page"></a>Jak používat vlastní chybovou stránku?

Tento kurz ukázal způsob použití `Global.asax` a obslužné rutiny události `Application_Error` ke spuštění kódu, když dojde k neošetřené výjimce. Konkrétně jsme tuto obslužnou rutinu události použili k oznamování vývojářů chyby. Můžeme ho roztáhnout, aby se do databáze zaprotokoloval také podrobnosti o chybě. Přítomnost obslužné rutiny události `Application_Error` nemá vliv na činnost koncového uživatele. Pořád uvidí konfigurovanou chybovou stránku, nastavili jsme podrobnosti o chybě YSOD, chyba modulu runtime YSOD nebo vlastní chybovou stránku.

Při použití vlastní chybové stránky je důležité, abyste si zajímá, jestli `Global.asax` soubor a `Application_Error` událost. Pokud dojde k chybě, zobrazí se uživateli vlastní chybová stránka, takže nemůžeme vložit kód pro informování vývojáře a zaprotokolovat podrobnosti o chybách do třídy kódu na pozadí vlastní chybové stránky? I když můžete přidat kód do třídy kódu na pozadí vlastní chybové stránky, nemáte přístup k podrobnostem o výjimce, která aktivovala událost `Error` při použití techniky, kterou jsme prozkoumali v předchozím kurzu. Volání metody `GetLastError` z vlastní chybové stránky vrátí `Nothing`.

Důvodem tohoto chování je, že vlastní chybová stránka se dorazí přes přesměrování. Když Neošetřená výjimka dosáhne běhového prostředí ASP.NET, modul ASP.NET vyvolá událost `Error` (která spustí obslužnou rutinu události `Application_Error`) a poté *přesměruje* uživatele na vlastní chybovou stránku vyvoláním `Response.Redirect(customErrorPageUrl)`. Metoda `Response.Redirect` odesílá klientovi odpověď se stavovým kódem HTTP 302, který instruuje prohlížeč, aby si vyžádal novou adresu URL, konkrétně vlastní chybovou stránku. Prohlížeč pak tuto novou stránku automaticky vyžádá. Můžete říct, že vlastní chybová stránka byla vyžádána nezávisle na stránce, kde došlo k chybě, protože se v adresním řádku prohlížeče změnila adresa URL vlastní chybové stránky (viz **Obrázek 4**).

[![](processing-unhandled-exceptions-cs/_static/image11.png)](processing-unhandled-exceptions-cs/_static/image10.png)

**Obrázek 4**: když dojde k chybě, prohlížeč se přesměruje na adresu URL vlastní chybové stránky.  
([Kliknutím zobrazíte obrázek v plné velikosti.](processing-unhandled-exceptions-cs/_static/image12.png))

Čistým účinkem je to, že žádost, kde došlo k neošetřené výjimce, končí, když server odpoví pomocí přesměrování HTTP 302. Následující požadavek na vlastní chybovou stránku je zcela nový požadavek. v tomto okamžiku modul ASP.NET zahodil informace o chybě, a navíc nemá žádný způsob, jak přidružit neošetřenou výjimku v předchozí žádosti s novým požadavkem na vlastní chybovou stránku. To je důvod, proč `GetLastError` vrátí `null` při volání z vlastní chybové stránky.

Je ale možné, že se vlastní chybová stránka spustí během stejné žádosti, která způsobila chybu. Metoda [`Server.Transfer(url)`](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx) přenáší provádění na zadanou adresu URL a zpracuje ji v rámci stejné žádosti. Můžete přesunout kód v obslužné rutině události `Application_Error` do třídy s kódem na pozadí vlastní chybové stránky a nahradit ji v `Global.asax` následujícím kódem:

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample5.cs)]

Nyní když dojde k neošetřené výjimce, obslužná rutina události `Application_Error` přenáší řízení na příslušnou vlastní chybovou stránku na základě stavového kódu HTTP. Vzhledem k tomu, že došlo k přenosu ovládacího prvku, vlastní chybová stránka má přístup k neošetřeným informacím o výjimce prostřednictvím `Server.GetLastError` a může oznamovateli informovat vývojáře o chybě a zaznamenat její podrobnosti. `Server.Transfer` volání zastaví modul ASP.NET před přesměrováním uživatele na vlastní chybovou stránku. Místo toho se jako odpověď na stránku, která generovala chybu, vrátí obsah vlastní chybové stránky.

## <a name="summary"></a>Souhrn

Pokud dojde k neošetřené výjimce ve webové aplikaci ASP.NET, modul runtime ASP.NET vyvolá událost `Error` a zobrazí nakonfigurovanou chybovou stránku. Pro tuto chybu můžeme oznamovatele informovat, zaznamenat její podrobnosti nebo je zpracovat jiným způsobem tak, že vytvoříte obslužnou rutinu události pro událost Error. Existují dva způsoby, jak vytvořit obslužnou rutinu události pro `HttpApplication` události jako `Error`: v souboru `Global.asax` nebo v modulu HTTP. V tomto kurzu jste si ukázali, jak vytvořit obslužnou rutinu události `Error` v souboru `Global.asax`, která vývojářům oznamuje chybu prostřednictvím e-mailové zprávy.

Vytvoření obslužné rutiny události `Error` je užitečné, pokud potřebujete zpracovat neošetřené výjimky v některém jedinečném nebo vlastním přizpůsobeném způsobem. Nicméně vytvoření vlastní obslužné rutiny události `Error` k zaznamenání výjimky nebo pro informování vývojáře není nejúčinnějším využitím času, protože již existuje a snadno se používají knihovny protokolování chyb, které je možné nastavit během několika minut. Další dva kurzy prozkoumají dvě takové knihovny.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [ASP.NET moduly HTTP a obslužné rutiny HTTP – přehled](https://support.microsoft.com/kb/307985)
- [Řádně reagovat na neošetřené výjimky zpracování neošetřených výjimek](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [Třída `HttpApplication` a objekt aplikace ASP.NET](http://www.eggheadcafe.com/articles/20030211.asp)
- [Obslužné rutiny HTTP a moduly HTTP v ASP.NET](http://www.15seconds.com/Issue/020417.htm)
- [Odesílání e-mailů v ASP.NET](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [Princip souboru `Global.asax`](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [Použití modulů a obslužných rutin HTTP k vytvoření zapojitelné součásti ASP.NET](https://msdn.microsoft.com/library/aa479332.aspx)
- [Práce se souborem `Global.asax` ASP.NET](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [Práce s instancemi `HttpApplication`](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [Předchozí](displaying-a-custom-error-page-cs.md)
> [Další](logging-error-details-with-asp-net-health-monitoring-cs.md)
