---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
title: Protokolování podrobností o chybách pomocí knihovny ELMAHC#() | Microsoft Docs
author: rick-anderson
description: Protokolovací moduly a obslužné rutiny chyb (knihovny ELMAH) nabízí další přístup k protokolování chyb za běhu v produkčním prostředí. KNIHOVNY ELMAH je bezplatná Open Source chyba...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 11f6fe44-64ef-4a38-a3b4-35c7bb992352
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
msc.type: authoredcontent
ms.openlocfilehash: 5018023eced23e7a70eab90e649f85862c548940
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573428"
---
# <a name="logging-error-details-with-elmah-c"></a>Protokolování podrobností o chybách pomocí knihovny ELMAH (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_cs.pdf)

> Protokolovací moduly a obslužné rutiny chyb (knihovny ELMAH) nabízí další přístup k protokolování chyb za běhu v produkčním prostředí. KNIHOVNY ELMAH je bezplatná knihovna protokolování chyb open source, která obsahuje funkce, jako je filtrování chyb, a možnost Zobrazit protokol chyb z webové stránky, jako informační kanál RSS nebo stáhnout jako textový soubor s oddělovači. Tento kurz vás provede stažením a konfigurací knihovny ELMAH.

## <a name="introduction"></a>Úvod

[Předchozí kurz](logging-error-details-with-asp-net-health-monitoring-cs.md) prozkoumal ASP. Systém monitorování stavu sítě, který nabízí z knihovny box pro záznam nejrůznějších webových událostí. Mnoho vývojářů používá sledování stavu k protokolování a e-mailu podrobnosti o neošetřených výjimkách. Tento systém však obsahuje několik bodových bolesti. První a nejpřednější je chybějící jakékoli řazení uživatelského rozhraní pro zobrazení informací o protokolovaných událostech. Pokud chcete zobrazit shrnutí 10 posledních chyb nebo zobrazit podrobnosti o chybě, která se zobrazila za poslední týden, musíte buď POKE databázi, procházet e-mailovou schránku nebo vytvořit webovou stránku, která zobrazuje informace z `aspnet_WebEvent_Events` tabulce.

Další prvky s bolestim bodem kolem složitosti monitorování stavu. Vzhledem k tomu, že monitorování stavu lze použít k zaznamenání spoustu různých událostí a protože existuje celá řada možností, jak určit, jak a kdy jsou události zaznamenávány, je správně konfigurován systém pro sledování stavu, což může být náročný úkol. Nakonec dojde k problémům s kompatibilitou. Protože sledování stavu bylo poprvé přidáno do .NET Framework ve verzi 2,0, není k dispozici pro starší webové aplikace sestavené pomocí ASP.NET verze 1. x. Kromě toho třída `SqlWebEventProvider`, kterou jsme použili v předchozím kurzu k zaznamenání podrobností o chybách do databáze, funguje pouze s databázemi Microsoft SQL Server. Je potřeba vytvořit vlastní třídu poskytovatele protokolů, aby bylo možné protokolovat chyby do alternativního úložiště dat, jako je třeba soubor XML nebo databáze Oracle.

Alternativou systému sledování stavu jsou moduly protokolování chyb a obslužné rutiny (knihovny ELMAH), bezplatný systém protokolování chyb Open Source vytvořený pomocí [Atif Aziz](http://www.raboof.com/). Nejvýznamnější rozdíl mezi těmito dvěma systémy je ELAMH schopnost zobrazit seznam chyb a podrobné informace o konkrétní chybě z webové stránky a jako informační kanál RSS. KNIHOVNY ELMAH je snazší konfigurovat než monitorování stavu, protože protokoluje pouze chyby. Kromě toho knihovny ELMAH zahrnuje podporu pro aplikace ASP.NET 1. x, ASP.NET 2,0 a ASP.NET 3,5 a dodává se s různými poskytovateli zdrojů protokolů.

Tento kurz vás provede jednotlivými kroky přidávání knihovny ELMAH do aplikace ASP.NET. Pojďme začít!

> [!NOTE]
> Systém monitorování stavu a knihovny ELMAH obojí mají své vlastní sady specialistů a nevýhody. Doporučuje se vyzkoušet oba systémy a rozhodnout, co nejlépe vyhovuje vašim potřebám.

## <a name="adding-elmah-to-an-aspnet-web-application"></a>Přidání knihovny ELMAH do webové aplikace ASP.NET

Integrace knihovny ELMAH do nové nebo stávající aplikace ASP.NET je jednoduchý a přímočarý proces, který trvá méně než pět minut. V kostce se skládá ze čtyř jednoduchých kroků:

1. Stáhněte si knihovny ELMAH a přidejte do své webové aplikace sestavení `Elmah.dll`,
2. Zaregistrujte moduly HTTP a obslužnou rutinu knihovny ELMAH v `Web.config`,
3. Zadejte možnosti konfigurace knihovny ELMAH a
4. V případě potřeby vytvořte zdrojovou infrastrukturu protokolu chyb.

Pojďme si projít každý z těchto čtyř kroků najednou.

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>Krok 1: stažení souborů projektu knihovny ELMAH a přidání`Elmah.dll`do vaší webové aplikace

KNIHOVNY ELMAH 1,0 BETA 3 (Build 10617), nejaktuálnější verze v době psaní, je součástí stahování dostupného v tomto kurzu. Alternativně můžete navštívit [web knihovny elmah](https://code.google.com/p/elmah/) a získat nejnovější verzi nebo stáhnout zdrojový kód. Extrahujte knihovny ELMAH stáhnout do složky na ploše a vyhledejte soubor sestavení knihovny ELMAH (`Elmah.dll`).

> [!NOTE]
> `Elmah.dll` soubor se nachází ve složce pro stahování `Bin`, která má podsložky pro různé .NET Framework verze, a pro sestavení vydaných verzí a ladění. Použijte sestavení pro vydání pro příslušnou verzi rozhraní .NET Framework. Pokud například vytváříte webovou aplikaci ASP.NET 3,5, zkopírujte soubor `Elmah.dll` ze složky `Bin\net-3.5\Release`.

Dále otevřete Visual Studio a přidejte sestavení do projektu tak, že kliknete pravým tlačítkem na název webu v Průzkumník řešení a zvolíte přidat odkaz z místní nabídky. Tím se otevře dialogové okno Přidat odkaz. Přejděte na kartu Procházet a vyberte soubor `Elmah.dll`. Tato akce přidá soubor `Elmah.dll` do složky `Bin` webové aplikace.

> [!NOTE]
> Typ projektu webové aplikace (WAP) nezobrazuje složku `Bin` v Průzkumník řešení. Místo toho tyto položky zobrazí ve složce odkazy.

`Elmah.dll` sestavení zahrnuje třídy používané systémem knihovny ELMAH. Tyto třídy spadají do jedné ze tří kategorií:

- **Moduly HTTP** – modul HTTP je třída, která definuje obslužné rutiny událostí pro `HttpApplication` události, jako je například událost `Error`. KNIHOVNY ELMAH zahrnuje více modulů HTTP, tři nejvíc německých: 

    - `ErrorLogModule` – zaznamená neošetřené výjimky do zdroje protokolu.
    - `ErrorMailModule` – pošle podrobnosti o neošetřené výjimce v e-mailové zprávě.
    - `ErrorFilterModule` – používá filtry určené pro vývojáře k určení, které výjimky jsou protokolovány a které jsou ignorovány.
- **Obslužné rutiny HTTP** – obslužná rutina http je třída, která zodpovídá za generování značek pro konkrétní typ požadavku. KNIHOVNY ELMAH zahrnuje obslužné rutiny HTTP, které vykreslí podrobnosti o chybě jako webovou stránku, jako informační kanál RSS nebo jako soubor CSV (oddělený čárkami).
- **Zdroje protokolu chyb – při** nedostatku pole knihovny elmah mohou protokolovat chyby do paměti, do databáze Microsoft SQL Server, do databáze aplikace Microsoft Access, do databáze Oracle, do souboru XML, do databáze SQLite nebo do databáze služby Vista DB. Podobně jako systém monitorování stavu, architektura knihovny ELMAH se vytvořila pomocí modelu poskytovatele, což znamená, že v případě potřeby můžete v případě potřeby vytvářet a hladce integrovat vlastní vlastní zprostředkovatele zdrojů protokolů.

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>Krok 2: registrace modulu HTTP a obslužné rutiny knihovny ELMAH

I když `Elmah.dll` soubor obsahuje moduly HTTP a obslužné rutiny potřebné k automatickému protokolování neošetřených výjimek a zobrazení podrobností o chybách z webové stránky, musí být explicitně registrovány v konfiguraci webové aplikace. Po registraci se modul `ErrorLogModule` HTTP přihlásí k odběru události `Error` `HttpApplication`. Pokaždé, když je tato událost vyvolána, `ErrorLogModule` protokoluje podrobnosti výjimky do zadaného zdroje protokolu. V další části se dozvíte, jak definovat poskytovatele zdroje protokolu. "konfigurace knihovny ELMAH." `ErrorLogPageFactory` objekt pro vytváření obslužných rutin HTTP zodpovídá za generování značek při zobrazení protokolu chyb z webové stránky.

Konkrétní syntaxe pro registraci modulů a obslužných rutin HTTP závisí na webovém serveru, který lokalitu vyzývají. Moduly a obslužné rutiny HTTP ASP.NET Development Server a IIS verze 6,0 a starší jsou registrované v částech `<httpModules>` a `<httpHandlers>`, které se zobrazí v elementu `<system.web>`. Pokud používáte IIS 7,0, musí být zaregistrované v sekcích `<modules>` a `<handlers>` elementu `<system.webServer>`. Naštěstí můžete definovat moduly HTTP a obslužné rutiny na *obou* místech bez ohledu na to, který webový server se používá. Tato možnost je nejvíc přenosná, protože umožňuje použít stejnou konfiguraci ve vývojovém a produkčním prostředí bez ohledu na používaný webový server.

Začněte tím, že zaregistrujete modul HTTP `ErrorLogModule` a `ErrorLogPageFactory` obslužnou rutinu protokolu HTTP v části `<httpModules>` a `<httpHandlers>` v `<system.web>`. Pokud vaše konfigurace již tyto dva prvky definuje, stačí přidat prvek `<add>` pro modul HTTP a obslužnou rutinu knihovny ELMAH.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample1.xml)]

Dále Zaregistrujte modul HTTP a obslužnou rutinu knihovny ELMAH v elementu `<system.webServer>`. Stejně jako dřív, pokud tento prvek ještě není ve vaší konfiguraci přítomen, přidejte ho.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample2.xml)]

Ve výchozím nastavení je služba IIS 7 stížnosti v případě, že jsou moduly HTTP a obslužné rutiny registrovány v části `<system.web>`. Atribut `validateIntegratedModeConfiguration` v elementu `<validation>` instruuje službu IIS 7, aby potlačila takové chybové zprávy.

Všimněte si, že syntaxe pro registraci obslužné rutiny `ErrorLogPageFactory` HTTP obsahuje atribut `path`, který je nastaven na `elmah.axd`. Tento atribut informuje webovou aplikaci, že pokud požadavek dorazí na stránku s názvem `elmah.axd` pak žádost by měla zpracovat `ErrorLogPageFactory` obslužná rutina HTTP. V tomto kurzu uvidíme `ErrorLogPageFactory` obslužnou rutinu protokolu HTTP v akci později.

### <a name="step-3-configuring-elmah"></a>Krok 3: konfigurace knihovny ELMAH

KNIHOVNY ELMAH vyhledá své možnosti konfigurace v souboru `Web.config` webu v části vlastní konfigurační oddíl s názvem `<elmah>`. Aby bylo možné použít vlastní oddíl v `Web.config` musí být nejprve definován v elementu `<configSections>`. Otevřete soubor `Web.config` a přidejte následující kód do `<configSections>`:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample3.xml)]

> [!NOTE]
> Pokud konfigurujete knihovny ELMAH pro aplikaci ASP.NET 1. x, pak z výše uvedených prvků `<section>` odeberte atribut `requirePermission="false"`.

Výše uvedená syntaxe registruje vlastní část `<elmah>` a její pododdíly: `<security>`, `<errorLog>`, `<errorMail>`a `<errorFilter>`.

Dále přidejte část `<elmah>` do `Web.config`. Tato část by se měla zobrazit na stejné úrovni jako `<system.web>` element. V části `<elmah>` přidejte oddíly `<security>` a `<errorLog>`, například:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample4.xml)]

Atribut `allowRemoteAccess` oddílu `<security>` určuje, zda je povolen vzdálený přístup. Pokud je tato hodnota nastavená na 0, Webová stránka protokolu chyb se dá zobrazit jenom místně. Pokud je tento atribut nastaven na hodnotu 1, Webová stránka protokolu chyb je povolena pro vzdálené i místní návštěvníky. Teď pro vzdálené návštěvníky zakážeme webovou stránku protokolu chyb. Vzdálený přístup povolíme později, až budeme mít příležitost projednávat problémy se zabezpečením.

Oddíl `<errorLog>` definuje zdroj protokolu chyb, který určuje, kde se zaznamenávají podrobnosti o chybě. je podobný oddílu `<providers>` v systému sledování stavu. Výše uvedená syntaxe určuje třídu `SqlErrorLog` jako zdroj protokolu chyb, který protokoluje chyby do databáze Microsoft SQL Server určené hodnotou atributu `connectionStringName`.

> [!NOTE]
> KNIHOVNY ELMAH dodává s dalšími poskytovateli chybových protokolů, které lze použít k protokolování chyb do souboru XML, databáze aplikace Microsoft Access, databáze Oracle a dalších úložišť dat. Informace o tom, jak používat tyto alternativní zprostředkovatele protokolu chyb, najdete v ukázkovém `Web.config` souboru, který je součástí stahování knihovny ELMAH.

### <a name="step-4-creating-the-error-log-source-infrastructure"></a>Krok 4: vytvoření zdrojové infrastruktury protokolu chyb

Poskytovatel `SqlErrorLog` knihovny ELMAH zapisuje podrobnosti o chybách do zadané Microsoft SQL Server databáze. Poskytovatel `SqlErrorLog` očekává, že tato databáze má tabulku s názvem `ELMAH_Error` a tři uložené procedury: `ELMAH_GetErrorsXml`, `ELMAH_GetErrorXml`a `ELMAH_LogError`. Stažení knihovny ELMAH zahrnuje soubor s názvem `SQLServer.sql` ve složce `db`, která obsahuje T-SQL pro vytvoření této tabulky a těchto uložených procedur. Chcete-li použít poskytovatele `SqlErrorLog`, je nutné spustit tyto příkazy v databázi.

**Obrázky 1** a **2** znázorňují Průzkumník databáze v aplikaci Visual Studio po přidání databázových objektů potřebných poskytovatelem `SqlErrorLog`.

[![](logging-error-details-with-elmah-cs/_static/image2.png)](logging-error-details-with-elmah-cs/_static/image1.png)

**Obrázek 1**: poskytovatel `SqlErrorLog` protokoluje chyby do tabulky `ELMAH_Error`

[![](logging-error-details-with-elmah-cs/_static/image4.png)](logging-error-details-with-elmah-cs/_static/image3.png)

**Obrázek 2**: poskytovatel `SqlErrorLog` používá tři uložené procedury.

## <a name="elmah-in-action"></a>KNIHOVNY ELMAH v akci

V tuto chvíli jsme přidali knihovny ELMAH do webové aplikace, zaregistrovali modul HTTP `ErrorLogModule` a `ErrorLogPageFactory` obslužnou rutinu protokolu HTTP, zadali možnosti konfigurace knihovny ELMAH v `Web.config`a Přidali jste potřebné databázové objekty pro zprostředkovatele protokolu chyb `SqlErrorLog`. Teď jsme připraveni zobrazit knihovny ELMAH v akci! Navštivte web recenze knih a přejděte na stránku, která generuje chybu za běhu, například `Genre.aspx?ID=foo`, nebo neexistující stránku, například `NoSuchPage.aspx`. To, co vidíte při návštěvě těchto stránek, závisí na konfiguraci `<customErrors>` a na tom, jestli se navštívíte místně nebo vzdáleně. (Další informace o aktualizačním programu v tomto tématu najdete v [kurzu *zobrazení vlastní chybové stránky* ](displaying-a-custom-error-page-cs.md) .)

KNIHOVNY ELMAH nemá vliv na to, jaký obsah se zobrazí uživateli, když dojde k neošetřené výjimce; pouze zaznamená své podrobnosti. Tento protokol chyb je přístupný z webové stránky `elmah.axd` z kořenového adresáře vašeho webu, jako je například `http://localhost/BookReviews/elmah.axd`. (Tento soubor v projektu fyzicky neexistuje, ale když se do `elmah.axd` za běhu odešle požadavek do `ErrorLogPageFactory` obslužné rutiny HTTP, která generuje kód odeslaný zpět do prohlížeče.)

> [!NOTE]
> Můžete také použít stránku `elmah.axd` k tomu, aby knihovny ELMAH vygenerovala chybu testu. Návštěvy `elmah.axd/test` (jako v `http://localhost/BookReviews/elmah.axd/test`) způsobí, že knihovny ELMAH vyvolá výjimku typu `Elmah.TestException`, která obsahuje chybovou zprávu: "Toto je výjimka testu, kterou lze bezpečně ignorovat."

**Obrázek 3** ukazuje protokol chyb při návštěvě `elmah.axd` z vývojového prostředí.

[![](logging-error-details-with-elmah-cs/_static/image6.png)](logging-error-details-with-elmah-cs/_static/image5.png)

**Obrázek 3**: `Elmah.axd` zobrazí protokol chyb z webové stránky.  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-elmah-cs/_static/image7.png))

Protokol chyb na **obrázku 3** obsahuje šest záznamů o chybách. Každá položka zahrnuje stavový kód HTTP (404 nebo 500 pro tyto chyby), typ, popis, jméno přihlášeného uživatele, kdy k chybě došlo, a datum a čas. Kliknutím na odkaz Podrobnosti se zobrazí stránka, která obsahuje stejnou chybovou zprávu, která se zobrazuje na žlutou obrazovku podrobností chyby (viz **Obrázek 4**), spolu s hodnotami proměnných serveru v době chyby (viz **Obrázek 5**). Můžete také zobrazit nezpracovaný soubor XML, ve kterém jsou uloženy podrobnosti o chybě, což zahrnuje další informace, jako jsou například hodnoty v hlavičce HTTP POST.

[![](logging-error-details-with-elmah-cs/_static/image9.png)](logging-error-details-with-elmah-cs/_static/image8.png)

**Obrázek 4**: zobrazení podrobností o chybě YSOD  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-elmah-cs/_static/image10.png))

[![](logging-error-details-with-elmah-cs/_static/image12.png)](logging-error-details-with-elmah-cs/_static/image11.png)

**Obrázek 5**: zkoumání hodnot kolekce proměnných serveru v době chyby  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-elmah-cs/_static/image13.png))

Nasazení knihovny ELMAH na produkční web má za následek:

- Zkopírování souboru `Elmah.dll` do složky `Bin` v produkčním prostředí,
- Kopírování nastavení konfigurace specifického pro knihovny ELMAH do souboru `Web.config` používaného v produkčním prostředí a
- Přidání zdrojové infrastruktury protokolu chyb do provozní databáze.

Prozkoumali jsme postupy kopírování souborů z vývoje do produkčního prostředí v předchozích kurzech. Možná nejjednodušší způsob, jak získat zdrojovou infrastrukturu protokolu chyb v provozní databázi, je použít SQL Server Management Studio pro připojení k provozní databázi a pak spustit soubor `SqlServer.sql` skriptu, který vytvoří potřebnou tabulku a uložené procedury.

### <a name="viewing-the-error-details-page-on-production"></a>Zobrazení stránky s podrobnostmi o chybě v produkčním prostředí

Po nasazení webu do produkčního prostředí přejděte na produkční web a vygenerujte neošetřenou výjimku. Stejně jako ve vývojovém prostředí nemá knihovny ELMAH žádný vliv na chybovou stránku zobrazenou v případě, že dojde k neošetřené výjimce; místo toho pouze zaznamená chybu. Pokud se pokusíte navštívit stránku protokolu chyb (`elmah.axd`) z produkčního prostředí, zobrazí se na **obrázku 6**stránka zakázaná.

[![](logging-error-details-with-elmah-cs/_static/image15.png)](logging-error-details-with-elmah-cs/_static/image14.png)

**Obrázek 6**: ve výchozím nastavení nemohou vzdálení uživatelé zobrazit webovou stránku protokolu chyb.  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-elmah-cs/_static/image16.png))

V části `<security>` konfigurace knihovny ELMAH nastavíme atribut `allowRemoteAccess` na hodnotu 0, což zakáže vzdáleným uživatelům zobrazit protokol chyb. Je důležité zabránit anonymním návštěvníkům v prohlížení protokolu chyb, protože podrobnosti o chybě můžou odhalit slabá místa zabezpečení nebo jiné citlivé informace. Pokud se rozhodnete nastavit tento atribut na hodnotu 1 a povolit vzdálený přístup k protokolu chyb, je důležité zamknout `elmah.axd` cestu tak, aby k ní měli přístup jenom autorizovaní uživatelé. Toho lze dosáhnout přidáním prvku `<location>` do souboru `Web.config`.

Následující konfigurace povoluje přístup k webové stránce protokolu chyb pouze uživatelům v roli správce:

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample5.xml)]

> [!NOTE]
> V části [ *Konfigurace webu, který používá aplikační služby* kurzu](configuring-a-website-that-uses-application-services-cs.md), se přidala role správce a tři uživatelé v systému – Scott, Jisun a Alice. Uživatelé Scott a Jisun jsou členy role správce. Další informace o ověřování a autorizaci najdete v tématu naše [kurzy zabezpečení webu](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).

Protokol chyb v produkčním prostředí teď můžou zobrazit vzdálení uživatelé. pro snímky obrazovky webové stránky protokolu chyb odkazují zpět na **obrázky 3**, **4**a **5** . Pokud se ale anonymní uživatel nebo uživatel bez role správce pokusí zobrazit stránku protokolu chyb, automaticky se přesměruje na přihlašovací stránku (`Login.aspx`), jak ukazuje **Obrázek 7** .

[![](logging-error-details-with-elmah-cs/_static/image18.png)](logging-error-details-with-elmah-cs/_static/image17.png)

**Obrázek 7**: neoprávnění uživatelé se automaticky přesměrují na přihlašovací stránku  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-elmah-cs/_static/image19.png))

### <a name="programmatically-logging-errors"></a>Programové protokolování chyb

Modul HTTP knihovny ELMAH `ErrorLogModule` automaticky ukládá neošetřené výjimky do zadaného zdroje protokolu. Alternativně můžete protokolovat chybu bez nutnosti vyvolat neošetřenou výjimku pomocí třídy `ErrorSignal` a její `Raise` metody. Metodě `Raise` se předává objekt `Exception` a protokoluje se, jako by tato výjimka byla vyvolána a dosáhla modulu runtime ASP.NET bez zpracování. Rozdílem je však, že žádost pokračuje v provádění normálně po volání metody `Raise`, zatímco vyvolaná Neošetřená výjimka přerušuje normální spuštění žádosti a způsobí, že modul runtime ASP.NET zobrazí nakonfigurovanou chybovou stránku.

Třída `ErrorSignal` je užitečná v situacích, kdy dojde k nějaké akci, která může selhat, ale její selhání není závažné pro provedení celkové operace. Web může například obsahovat formulář, který převezme vstup uživatele, uloží ho do databáze a pak mu pošle e-mail s informacemi o tom, že se zpracovaly informace. Co se stane, když se informace v databázi úspěšně uloží, ale při posílání e-mailové zprávy dojde k chybě? Jednou z možností je vyvolat výjimku a odeslat uživatele na chybovou stránku. To však může Zaměňujte uživatele, že informace, které byly zadány, nebudou uloženy. Další možností je zaprotokolovat chybu související s e-mailem, ale neměňte uživatelské prostředí. Zde je `ErrorSignal` třída užitečná.

[!code-csharp[Main](logging-error-details-with-elmah-cs/samples/sample6.cs)]

## <a name="error-notification-via-email"></a>Chybové oznámení prostřednictvím e-mailu

Společně s protokolem chyb v databázi je také možné nakonfigurovat knihovny ELMAH na podrobnosti o chybě e-mailem pro zadaného příjemce. Tuto funkci poskytuje modul HTTP `ErrorMailModule`. Proto je nutné tento modul HTTP zaregistrovat v `Web.config`, aby bylo možné odeslat podrobnosti o chybě e-mailem.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample7.xml)]

Dále zadejte informace o chybě e-mailu v oddílu `<errorMail>` `<elmah>` elementu, který označuje odesílatele a příjemce e-mailu, předmět a informace o tom, jestli se e-mail pošle asynchronně.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample8.xml)]

Když se výše uvedená nastavení nastanou, knihovny ELMAH odešle support@example.com e-mail s podrobnostmi o chybě za běhu. Chybový e-mail knihovny ELMAH obsahuje stejné informace, které jsou uvedeny na webové stránce Podrobnosti o chybě, konkrétně v chybové zprávě, trasování zásobníku a proměnných serveru (odkazy zpět na **obrázky 4** a **5**). Chybový e-mail obsahuje také žlutou obrazovku s podrobnostmi o odvolaném obsahu jako přílohu (`YSOD.html`).

**Obrázek 8** ukazuje CHYBOVÝ e-mail knihovny elmah vygenerovaný na základě `Genre.aspx?ID=foo`. I když **Obrázek 8** zobrazuje pouze chybovou zprávu a trasování zásobníku, proměnné serveru jsou uvedeny dále v těle e-mailu.

[![](logging-error-details-with-elmah-cs/_static/image21.png)](logging-error-details-with-elmah-cs/_static/image20.png)

**Obrázek 8**: knihovny elmah můžete nakonfigurovat pro odesílání podrobností o chybě e-mailem.  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-elmah-cs/_static/image22.png))

## <a name="only-logging-errors-of-interest"></a>Pouze protokolování chyb v zájmu

Ve výchozím nastavení protokol knihovny ELMAH zapisuje podrobnosti o každé neošetřené výjimce, včetně 404 a dalších chyb protokolu HTTP. Můžete určit, že má knihovny ELMAH ignorovat tyto nebo jiné typy chyb pomocí filtrování chyb. Logika filtrování je prováděna modulem knihovny ELMAH `ErrorFilterModule` HTTP, který budete muset zaregistrovat v `Web.config`, aby bylo možné použít logiku filtrování. Pravidla pro filtrování jsou uvedena v části `<errorFilter>`.

Následující kód vydá pokyn knihovny ELMAH k chybám protokolu 404.

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample9.xml)]

> [!NOTE]
> Nezapomeňte, že pokud chcete použít filtrování chyb, musíte zaregistrovat `ErrorFilterModule` modul HTTP.

Element `<equal>` uvnitř oddílu `<test>` je označován jako kontrolní výraz. Pokud je kontrolní výraz vyhodnocen jako true, je chyba filtrována z protokolu knihovny ELMAH. K dispozici jsou další kontrolní výrazy, včetně: `<greater>`, `<greater-or-equal>`, `<not-equal>`, `<lesser>`, `<lesser-or-equal>`a tak dále. Můžete také kombinovat kontrolní výrazy pomocí `<and>` a `<or>` logických operátorů. A co víc, můžete dokonce zahrnout jednoduchý výraz JavaScriptu jako kontrolní výraz nebo napsat vlastní kontrolní výrazy v C# nebo Visual Basic.

Další informace o možnostech filtrování chyb v knihovny ELMAH najdete v [části filtrování chyb](https://code.google.com/p/elmah/wiki/ErrorFiltering) na [wikiwebu knihovny elmah](https://code.google.com/p/elmah/w/list).

## <a name="summary"></a>Souhrn

KNIHOVNY ELMAH poskytuje jednoduchý, ale účinný mechanismus pro protokolování chyb ve webové aplikaci v ASP.NET. Podobně jako systém sledování stavu společnosti Microsoft může knihovny ELMAH protokolovat chyby do databáze a odesílat podrobnosti o chybě vývojáři prostřednictvím e-mailu. Na rozdíl od systému monitorování stavu knihovny ELMAH zahrnuje podporu pro širší škálu úložišť dat protokolu chyb, mezi které patří: Microsoft SQL Server, Microsoft Access, Oracle, XML soubory a několik dalších. KNIHOVNY ELMAH navíc nabízí integrovaný mechanizmus pro zobrazení protokolu chyb a podrobnosti o konkrétní chybě z webové stránky `elmah.axd`. Stránka `elmah.axd` může také vykreslovat informace o chybě jako informační kanál RSS nebo jako textový soubor s oddělovači (CSV), který můžete číst pomocí aplikace Microsoft Excel. Můžete také instruovat knihovny ELMAH, aby vyfiltroval chyby z protokolu pomocí deklarativních nebo programových kontrolních výrazů. A knihovny ELMAH lze použít s aplikacemi ASP.NET verze 1. x.

Každá nasazená aplikace by měla mít nějaký mechanismus pro automatické protokolování neošetřených výjimek a odesílání oznámení do vývojového týmu. Bez ohledu na to, jestli se to provádí pomocí monitorování stavu nebo knihovny ELMAH, je sekundární. Jinými slovy, nezáleží na tom, zda používáte monitorování stavu nebo knihovny ELMAH; Vyhodnoťte oba systémy a pak zvolte ten, který nejlépe vyhovuje vašim potřebám. Důležité je, aby byl zaveden nějaký mechanismus pro protokolování neošetřených výjimek v produkčním prostředí.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [KNIHOVNY ELMAH – moduly a obslužné rutiny protokolu chyb](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [Stránka projektu knihovny elmah](https://code.google.com/p/elmah/) (zdrojový kód, ukázky, wiki)
- [Zapojení knihovny elmah do webové aplikace pro zachycení neošetřených výjimek](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx) (video)
- [Stránky protokolu chyb zabezpečení](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [Použití modulů a obslužných rutin HTTP k vytvoření zapojitelné součásti ASP.NET](https://msdn.microsoft.com/library/aa479332.aspx)
- [Kurzy zabezpečení webu](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [Předchozí](logging-error-details-with-asp-net-health-monitoring-cs.md)
> [Další](precompiling-your-website-cs.md)
