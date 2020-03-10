---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: Povolení žádostí o více zdrojů v ASP.NET webovém rozhraní API 2 | Microsoft Docs
author: MikeWasson
description: Ukazuje, jak podporovat sdílení prostředků mezi zdroji (CORS) ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555704"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a>Povolení žádostí mezi zdroji v ASP.NET webovém rozhraní API 2

o [Jan Wasson](https://github.com/MikeWasson)

> Zabezpečení prohlížečů brání webovým stránkám v odesílání požadavků AJAX na jinou doménu. Toto omezení se nazývá *zásady stejného původu*a brání škodlivému webu v čtení citlivých dat z jiné lokality. V některých případech však můžete chtít povolit jiným webům volat vaše webové rozhraní API.
>
> [Sdílení prostředků mezi zdroji](http://www.w3.org/TR/cors/) (CORS) je standard W3C, který umožňuje serveru zmírnit zásady stejného zdroje. Při použití CORS může server explicitně umožnit některé žádosti o více zdrojů a současně odmítat jiné. CORS je bezpečnější a pružnější než u předchozích technik, jako je [JSONP](http://en.wikipedia.org/wiki/JSONP). V tomto kurzu se dozvíte, jak ve vaší aplikaci webového rozhraní API povolit CORS.
>
> ## <a name="software-used-in-the-tutorial"></a>Software použitý v tomto kurzu
>
> - [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Webové rozhraní API 2,2

## <a name="introduction"></a>Úvod

Tento kurz ukazuje podporu CORS ve webovém rozhraní API ASP.NET. Začneme vytvořením dvou ASP.NET projektů – One s názvem "WebService", který hostuje kontroler webového rozhraní API a druhý s názvem "webový klient", který volá webovou službu. Vzhledem k tomu, že jsou tyto dvě aplikace hostovány v různých doménách, požadavek AJAX od WebClient na WebService je požadavek na více zdrojů.

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>Co je "stejný zdroj"?

Dvě adresy URL mají stejný původ, pokud mají totožná schémata, hostitele a porty. ([RFC 6454](http://tools.ietf.org/html/rfc6454))

Tyto dvě adresy URL mají stejný původ:

- `http://example.com/foo.html`
- `http://example.com/bar.html`

Tyto adresy URL mají jiný původ než předchozí dvě:

- `http://example.net` – odlišná doména
- `http://example.com:9000/foo.html` – jiný port
- `https://example.com/foo.html` – odlišné schéma
- `http://www.example.com/foo.html` – odlišná subdoména

> [!NOTE]
> Internet Explorer při porovnávání míst původu nebere v úvahu port.

## <a name="create-the-webservice-project"></a>Vytvoření projektu WebService

> [!NOTE]
> V této části se předpokládá, že už máte informace o tom, jak vytvářet projekty webového rozhraní API. Pokud ne, přečtěte si téma [Začínáme s webovým rozhraním API ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).

1. Spusťte Visual Studio a vytvořte nový projekt **webové aplikace v ASP.NET (.NET Framework)** .
2. V dialogovém okně **Nová webová aplikace v ASP.NET** vyberte šablonu **prázdného** projektu. V části **Přidat složky a základní reference pro**vyberte zaškrtávací políčko **webové rozhraní API** .

   ![Dialogové okno Nový projekt ASP.NET v aplikaci Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. Přidejte kontroler webového rozhraní API s názvem `TestController` s následujícím kódem:

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. Aplikaci můžete spustit místně nebo nasadit do Azure. (Pro snímky obrazovky v tomto kurzu se aplikace nasadí do Azure App Service Web Apps.) Chcete-li ověřit, zda webové rozhraní API funguje, přejděte na adresu `http://hostname/api/test/`, kde *název hostitele* je doména, do které jste aplikaci nasadili. Měl by se zobrazit text odpovědi &quot;GET: test Message&quot;.

   ![Webový prohlížeč zobrazující zkušební zprávu](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a>Vytvoření projektu WebClient

1. Vytvořte další projekt **webové aplikace v ASP.NET (.NET Framework)** a vyberte šablonu projektu **MVC** . Volitelně můžete vybrat možnost **změnit ověřování** > **bez ověřování**. Pro tento kurz nepotřebujete ověřování.

   ![Šablona MVC v dialogovém okně Nový projekt ASP.NET v aplikaci Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. V **Průzkumník řešení**otevřete *zobrazení souborů/domů/index. cshtml*. Nahraďte kód v tomto souboru následujícím kódem:

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   Pro proměnnou *serviceUrl* použijte identifikátor URI aplikace WebService.

3. Spusťte aplikaci webového klienta lokálně nebo ji publikujte na jiném webu.

Po kliknutí na tlačítko vyzkoušet se odešle požadavek AJAX do aplikace WebService pomocí metody HTTP uvedené v rozevíracím seznamu (GET, POST nebo PUT). To vám umožní prošetřit různé požadavky na více zdrojů. V současné době aplikace webové služby nepodporuje CORS, takže pokud kliknete na tlačítko, zobrazí se chyba.

![V prohlížeči se chyba "vyzkoušet IT"](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> Pokud sledujete provoz protokolu HTTP v nástroji jako [Fiddler](https://www.telerik.com/fiddler), uvidíte, že prohlížeč odesílá požadavek GET a požadavek je úspěšný, ale volání AJAX vrátí chybu. Je důležité pochopit, že zásady stejného původu nebrání prohlížeči *Odeslat* požadavek. Místo toho zabrání aplikaci zobrazit *odpověď*.

![Webový ladicí program Fiddler zobrazující webové požadavky](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a>Povolení CORS

Teď v aplikaci WebService povolíte CORS. Nejdřív přidejte balíček NuGet CORS. V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

Tento příkaz nainstaluje nejnovější balíček a aktualizuje všechny závislosti, včetně základních knihoven webových rozhraní API. Použijte příznak `-Version` k zacílení na konkrétní verzi. Balíček CORS vyžaduje webové rozhraní API 2,0 nebo novější.

Otevřete soubor *App\_Start/WebApiConfig. cs*. Do metody **WebApiConfig. Register** přidejte následující kód:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

Dále přidejte atribut **[EnableCors]** do třídy `TestController`:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

Pro parametr *původes* použijte identifikátor URI, kde jste nasadili aplikaci WebClient. To umožňuje, aby se požadavky na více zdrojů od WebClient a pořád nepovolovaly všechny ostatní požadavky mezi doménami. Později popište parametry pro **[EnableCors]** podrobněji.

Na konec adresy URL *původních* míst nepoužívejte lomítko.

Znovu nasaďte aktualizovanou aplikaci WebService. Nemusíte aktualizovat WebClient. Požadavek AJAX z WebClient by teď měl být úspěšný. Metody GET, PUT a POST jsou povoleny.

![Webový prohlížeč zobrazující úspěšnou zkušební zprávu](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a>Jak CORS funguje

Tato část popisuje, co se stane v žádosti CORS, na úrovni zpráv HTTP. Je důležité pochopit, jak CORS funguje, abyste mohli správně nakonfigurovat atribut **[EnableCors]** a řešit potíže, pokud nefungují podle očekávání.

Specifikace CORS zavádí několik nových hlaviček protokolu HTTP, které umožňují žádosti mezi zdroji. Pokud prohlížeč podporuje CORS, nastavuje tyto hlavičky pro žádosti mezi zdroji automaticky. v kódu JavaScriptu nemusíte nic dělat.

Tady je příklad žádosti o více zdrojů. Hlavička "Origin" poskytuje doménu lokality, která požadavek provádí.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

Pokud server tuto žádost povoluje, nastaví hlavičku Access-Control-Allow-Origin. Hodnota této hlavičky odpovídá záhlaví původu, nebo se jedná o zástupnou hodnotu "\*", což znamená, že je povolen libovolný původ.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

Pokud odpověď nezahrnuje hlavičku Access-Control-Allow-Origin, požadavek AJAX se nezdařil. Konkrétně prohlížeč požadavek nepovoluje. I v případě, že server vrátí úspěšnou odpověď, prohlížeč nezpřístupňuje odpověď klientské aplikaci.

**Požadavky na kontrolu před výstupem**

V případě některých žádostí CORS pošle prohlížeč další žádost s názvem "žádost o kontrolu před odesláním skutečné žádosti o prostředek".

Prohlížeč může požadavek na předběžné kontroly přeskočit, pokud jsou splněné následující podmínky:

- Metoda Request je GET, HEAD nebo POST *a*
- Aplikace nenastavuje žádné hlavičky požadavků *, které jsou* jiné než akceptující, Accept-Language, Content-Language, Content-Type nebo Last-ID.
- Hlavička Content-Type (Pokud je nastavena) je jedna z následujících:

    - Application/x-www-form-urlencoded
    - multipart/form-data
    - text/plain

Pravidlo týkající se hlaviček požadavků platí pro hlavičky, které aplikace nastaví pomocí volání **setRequestHeader** na objektu **XMLHttpRequest** . (Specifikace CORS volá tyto "hlavičky žádostí o autora".) Pravidlo se nevztahuje na hlavičky, které může *prohlížeč* nastavit, jako je například uživatelský agent, hostitel nebo délka obsahu.

Tady je příklad žádosti o kontrolu před výstupem:

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

Požadavek na lety používá metodu HTTP. Obsahuje dvě speciální hlavičky:

- Access-Control-Request-method: metoda HTTP, která bude použita pro skutečný požadavek.
- Access-Control-Request-Headers seznam hlaviček požadavků, které *aplikace* nastaví na skutečném požadavku. (Znovu nezahrnuje hlavičky, které nastaví prohlížeč.)

Tady je příklad odpovědi za předpokladu, že server povoluje požadavek:

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

Odpověď obsahuje hlavičku Access-Control-Allow-Methods, která obsahuje seznam povolených metod, a volitelně hlavičku Access-Control-Allow-Headers, která obsahuje seznam povolených hlaviček. Pokud je žádost o kontrolu předem úspěšná, prohlížeč pošle skutečný požadavek, jak je popsáno výše.

Nástroje běžně používané k testování koncových bodů s požadavky na možnosti kontroly před výstupem (například [Fiddler](https://www.telerik.com/fiddler) a [post](https://www.getpostman.com/)) neodesílají ve výchozím nastavení hlavičky požadované možnosti. Ověřte, že se v žádosti odesílají hlavičky `Access-Control-Request-Method` a `Access-Control-Request-Headers` a že hlavičky možností dosáhnou aplikace prostřednictvím služby IIS.

Pokud chcete nakonfigurovat službu IIS tak, aby aplikaci ASP.NET mohla přijímat a zpracovávat žádosti o možnosti, přidejte následující konfiguraci do souboru *Web. config* aplikace v části `<system.webServer><handlers>`:

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

Odebrání `OPTIONSVerbHandler` zabrání službě IIS ve zpracování požadavků na možnosti. Nahrazení `ExtensionlessUrlHandler-Integrated-4.0` umožňuje požadavkům na přístup k aplikaci, protože registrace výchozího modulu povoluje pouze požadavky GET, HEAD, POST a DEBUG s příponami bez přípony.

## <a name="scope-rules-for-enablecors"></a>Pravidla oboru pro [EnableCors]

Pro všechny řadiče webového rozhraní API ve vaší aplikaci můžete povolit CORS na akci, pro každý kontroler nebo globálně.

**Na akci**

Chcete-li povolit CORS pro jednu akci, nastavte v metodě Action atribut **[EnableCors]** . Následující příklad povoluje CORS jenom pro metodu `GetItem`.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**Na kontroler**

Pokud jste pro třídu kontroleru nastavili **[EnableCors]** , vztahuje se na všechny akce na řadiči. Pro zakázání CORS pro akci přidejte k akci atribut **[DisableCors]** . Následující příklad povoluje CORS pro každou metodu kromě `PutItem`.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**Univerzál**

Pokud chcete povolit CORS pro všechny řadiče webového rozhraní API ve vaší aplikaci, předejte instanci **EnableCorsAttribute** do metody **EnableCors** :

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

Pokud nastavíte atribut ve více než jednom oboru, pořadí priorit je:

1. Akce
2. Kontrolér
3. Globální

## <a name="set-the-allowed-origins"></a>Nastavení povolených zdrojů

Parametr *origines* atributu **[EnableCors]** určuje, které zdroje mají povolený přístup k prostředku. Hodnota je čárkami oddělený seznam povolených zdrojů.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

Můžete také použít zástupnou hodnotu "\*" pro povolení požadavků z libovolného původu.

Před povolením požadavků z libovolného počátku zvažte pečlivou pozornost. To znamená, že každý web může ve webovém rozhraní API vyvolat volání AJAX.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a>Nastavení povolených metod HTTP

Parametr *metody* atributu **[EnableCors]** určuje, které metody HTTP mají povolen přístup k prostředku. Pro povolení všech metod použijte zástupný znak "\*". Následující příklad povoluje pouze požadavky GET a POST.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a>Nastavení povolených hlaviček žádosti

Tento článek popisuje předchozí způsob, jakým může požadavek na kontrolu před výstupem zahrnovat hlavičku Access-Control-Request-Headers, v níž je uveden seznam hlaviček protokolu HTTP, které aplikace nastavila (záhlaví žádostí s názvem "autor žádosti"). Parametr *Headers* atributu **[EnableCors]** určuje, které hlavičky žádostí autora jsou povoleny. Pro povolení všech hlaviček nastavte *záhlaví* na "\*". Pokud chcete zobrazit konkrétní záhlaví, nastavte *záhlaví* na čárkami oddělený seznam povolených hlaviček:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

Nicméně prohlížeče nejsou zcela konzistentní v tom, jak nastavily Access-Control-Request-Headers. Například Chrome aktuálně obsahuje "Origin". FireFox neobsahuje standardní hlavičky, jako je "Accept", ani když ji aplikace nastaví ve skriptu.

Pokud nastavíte *záhlaví* na jinou hodnotu než "\*", měli byste zahrnout aspoň "přijmout", "Content-Type" a "Origin" a také všechna vlastní záhlaví, která chcete podporovat.

## <a name="set-the-allowed-response-headers"></a>Nastavení povolených hlaviček odpovědí

Ve výchozím nastavení prohlížeč nezveřejňuje všechny hlavičky odpovědí na aplikaci. Ve výchozím nastavení jsou k dispozici následující hlavičky odpovědí:

- Cache-Control
- Obsah – jazyk
- Content-Type
- Expires
- Naposledy změněno
- Pragma

Specifikace CORS volá tyto [jednoduché hlavičky odpovědi](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header). Pro zpřístupnění dalších hlaviček pro aplikaci nastavte parametr *exposedHeaders* **[EnableCors]** .

V následujícím příkladu `Get` metoda kontroleru nastaví vlastní hlavičku s názvem "X-Custom-header". Ve výchozím nastavení prohlížeč nebude tuto hlavičku vystavovat v žádosti o více zdrojů. Pokud chcete, aby byla hlavička dostupná, zahrňte do *exposedHeaders*hodnotu "X-Custom-header".

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a>Předávání přihlašovacích údajů v žádostech mezi zdroji

Přihlašovací údaje vyžadují zvláštní zpracování v žádosti CORS. Ve výchozím nastavení prohlížeč neodesílá žádné přihlašovací údaje pomocí žádosti o více zdrojů. Přihlašovací údaje zahrnují soubory cookie i schémata ověřování protokolu HTTP. Aby bylo možné odesílat přihlašovací údaje pomocí žádosti o více zdrojů, musí klient nastavit **XMLHttpRequest. withCredentials** na hodnotu true.

Přímé použití **XMLHttpRequest** :

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

V jQuery:

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

Server navíc musí přihlašovací údaje umožňovat. Pokud chcete ve webovém rozhraní API zapnout přihlašovací údaje pro více zdrojů, nastavte vlastnost **SupportsCredentials** na hodnotu true v atributu **[EnableCors]** :

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

Pokud má tato vlastnost hodnotu true, bude odpověď HTTP zahrnovat hlavičku Access-Control-Allow-Credentials. Tato hlavička obsahuje informace o prohlížeči, který server umožňuje přihlašovací údaje pro požadavek mezi zdroji.

Pokud prohlížeč odesílá přihlašovací údaje, ale odpověď nezahrnuje platné záhlaví Access-Control-Allow-Credentials, prohlížeč nezveřejňuje odpověď na aplikaci a požadavek AJAX selže.

Buďte opatrní při nastavení **SupportsCredentials** na hodnotu true, protože to znamená, že web v jiné doméně může posílat přihlašovací údaje přihlášeného uživatele k webovému rozhraní API jménem uživatele bez ohledu na uživatele. Specifikace CORS také uvádí, že nastavení *původce* na &quot;\*&quot; je neplatné, pokud má **SupportsCredentials** hodnotu true.

## <a name="custom-cors-policy-providers"></a>Vlastní poskytovatelé zásad CORS

Atribut **[EnableCors]** implementuje rozhraní **ICorsPolicyProvider** . Můžete poskytnout vlastní implementaci vytvořením třídy, která je odvozena z **atributu** a implementuje **ICorsPolicyProvider**.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

Nyní můžete použít atribut na místo, které byste umístili **[EnableCors]** .

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

Vlastní poskytovatel zásad CORS například mohl přečíst nastavení z konfiguračního souboru.

Jako alternativu k používání atributů můžete zaregistrovat objekt **ICorsPolicyProviderFactory** , který vytváří objekty **ICorsPolicyProvider** .

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

Chcete-li nastavit **ICorsPolicyProviderFactory**, zavolejte při spuštění metodu rozšíření **SetCorsPolicyProviderFactory** následujícím způsobem:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a>Podpora prohlížeče

Balíček Web API CORS je technologie na straně serveru. Prohlížeč uživatele musí také podporovat CORS. Stávající verze všech hlavních prohlížečů naštěstí zahrnují [podporu CORS](http://caniuse.com/cors).
