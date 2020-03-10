---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: Průvodce rozhraním API pro centra ASP.NET Signales – Server (Signal 1. x) | Microsoft Docs
author: bradygaster
description: Tento dokument popisuje, jak programovat serverovou stranu rozhraní API centra ASP.NET pro Signal verze 1,1 s ukázkami kódu demonstratin...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579637"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a>Průvodce rozhraním API pro centra ASP.NET Signal-Server (signál 1. x)

autorem [Fletcher](https://github.com/pfletcher), který [Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument popisuje, jak programovat serverovou stranu rozhraní API centra ASP.NET pro Signal verze 1,1 s ukázkami kódu, které demonstrují běžné možnosti.
> 
> Rozhraní API pro centra signalizace vám umožní provádět Vzdálená volání procedur (RPC) ze serveru pro připojené klienty a klienty na server. V kódu serveru můžete definovat metody, které mohou být volány klienty, a volat metody, které jsou spouštěny v klientovi. V kódu klienta definujete metody, které mohou být volány ze serveru, a voláte metody, které jsou spuštěny na serveru. Signalizace postará o všechny instalace klienta na server za vás.
> 
> Nástroj Signal také nabízí nižší úroveň rozhraní API označované jako trvalá připojení. Úvod do nástroje pro signalizaci, centra a trvalá připojení nebo v kurzu, který ukazuje, jak sestavit kompletní aplikaci signalizace, najdete v tématu [signaler-Začínáme](index.md).

## <a name="overview"></a>Přehled

Tento dokument obsahuje následující části:

- [Jak zaregistrovat trasu signalizace a nakonfigurovat možnosti signalizace](#route)

    - [Adresa URL/SignalR](#signalrurl)
    - [Konfigurace možností signalizace](#options)
- [Jak vytvořit a používat třídy centra](#hubclass)

    - [Doba života objektu centra](#transience)
    - [Ve stylu CamelCase – velká a malá písmena názvů hub v klientech JavaScript](#hubnames)
    - [Více Center](#multiplehubs)
- [Jak definovat metody ve třídě centra, které můžou klienti volat](#hubmethods)

    - [Ve stylu CamelCase – velká a malá písmena názvů metod v klientech JavaScript](#methodnames)
    - [Kdy spustit asynchronně](#asyncmethods)
    - [Definování přetížení](#overloads)
- [Volání metod klienta z třídy hub](#callfromhub)

    - [Výběr klientů, kteří budou přijímat RPC](#selectingclients)
    - [Žádné ověřování v době kompilace pro názvy metod](#dynamicmethodnames)
    - [Porovnávání názvů metod bez rozlišení velkých a malých písmen](#caseinsensitive)
    - [Asynchronní spuštění](#asyncclient)
- [Správa členství ve skupinách z třídy hub](#groupsfromhub)

    - [Asynchronní provádění metod Add a Remove](#asyncgroupmethods)
    - [Trvalost členství ve skupině](#grouppersistence)
    - [Skupiny s jedním uživatelem](#singleusergroups)
- [Postup zpracování událostí životního cyklu připojení ve třídě centra](#connectionlifetime)

    - [Když se připojí, odpojí se a OnReconnected se zavolají.](#onreconnected)
    - [Stav volajícího není naplněný.](#nocallerstate)
- [Jak získat informace o klientovi z kontextové vlastnosti](#contextproperty)
- [Postup předání stavu mezi klienty a třídou centra](#passstate)
- [Jak zpracovávat chyby ve třídě centra](#handleErrors)
- [Jak volat klientské metody a spravovat skupiny mimo třídu centra](#callfromoutsidehub)

    - [Volání metod klienta](#callingclientsoutsidehub)
    - [Správa členství ve skupinách](#managinggroupsoutsidehub)
- [Jak povolit trasování](#tracing)
- [Postup přizpůsobení kanálu Center](#hubpipeline)

Dokumentaci k programům pro klienty naleznete v následujících zdrojích informací:

- [Průvodce rozhraním API pro centra signálů – JavaScriptový klient](index.md)
- [Průvodce rozhraním API pro centra signálů – klient .NET](index.md)

Odkazy na referenční témata rozhraní API odkazují na verzi rozhraní API .NET 4,5. Pokud používáte .NET 4, přečtěte si téma věnované [verzi rozhraní API rozhraní .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a>Jak zaregistrovat trasu signalizace a nakonfigurovat možnosti signalizace

Chcete-li definovat trasu, kterou budou klienti používat pro připojení k vašemu rozbočovači, zavolejte metodu [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) při spuštění aplikace. `MapHubs` je [metoda rozšíření](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) pro třídu `System.Web.Routing.RouteCollection`. Následující příklad ukazuje, jak definovat trasu centra signalizace v souboru *Global. asax* .

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

Pokud přidáváte funkce signalizace do aplikace ASP.NET MVC, ujistěte se, že je před ostatními trasa přidána trasa signálu. Další informace najdete v tématu [kurz: Začínáme s nástrojem Signal and MVC 4](index.md).

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>Adresa URL/SignalR

Ve výchozím nastavení je adresa URL trasy, kterou budou klienti používat pro připojení k vašemu centru, "/SignalR". (Nezaměňujte tuto adresu URL s adresou URL "/SignalR/Hubs", která je pro automaticky generovaný soubor JavaScriptu. Další informace o vygenerovaném proxy serveru najdete v tématu [Průvodce rozhraním API pro centra signalizace – JavaScriptový klient – vygenerovaný proxy server a co pro vás](index.md).)

Mohou nastat mimořádné okolnosti, které tuto základní adresu URL nedají použít pro signál. máte například složku v projektu s názvem *signaler* a nechcete změnit název. V takovém případě můžete změnit základní adresu URL, jak je znázorněno v následujících příkladech (nahraďte "/SignalR" v ukázkovém kódu požadovanou adresou URL).

**Kód serveru, který určuje adresu URL**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

**JavaScript – kód klienta, který určuje adresu URL (u generovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

**JavaScriptový kód klienta, který určuje adresu URL (bez vygenerovaného proxy serveru)**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

**Kód klienta .NET, který určuje adresu URL**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>Konfigurace možností signalizace

Přetížení metody `MapHubs` umožňují zadat vlastní adresu URL, vlastní překladač závislosti a následující možnosti:

- Povolí volání mezi doménami z klientů prohlížeče.

    V případě, že prohlížeč načítá stránku z `http://contoso.com`, připojení k signalizaci je ve stejné doméně, v `http://contoso.com/signalr`. Pokud stránka z `http://contoso.com` vytvoří připojení k `http://fabrikam.com/signalr`, což je připojení mezi doménami. Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázaná. Další informace najdete v tématu [Průvodce rozhraním API pro centra signálů ASP.NET – klient JavaScriptu – jak navázat připojení mezi doménami](index.md).
- Povolte podrobné chybové zprávy.

    Pokud dojde k chybám, je výchozím chováním signalizace odeslání do klientů oznamovací zpráva bez podrobností o tom, co se stalo. Odeslání podrobných informací o chybách klientům se nedoporučuje v produkčním prostředí, protože uživatelé se zlými úmysly můžou používat informace v útocích proti vaší aplikaci. Při řešení potíží můžete tuto možnost použít k dočasnému povolení více informativních zpráv o chybách.
- Zakáže automaticky generované soubory proxy JavaScriptu.

    Ve výchozím nastavení je soubor JavaScriptu s proxy pro vaše třídy centra vygenerovaný jako odpověď na adresu URL "/SignalR/Hubs". Pokud nechcete používat proxy servery JavaScript, nebo pokud chcete tento soubor vygenerovat ručně a můžete se podívat na fyzický soubor ve vašich klientech, můžete tuto možnost použít k zakázání generování proxy serveru. Další informace najdete v tématu [Průvodce rozhraním API pro centra signálů – klient JavaScript – jak vytvořit fyzický soubor pro proxy vygenerovaný signálem](index.md).

Následující příklad ukazuje, jak zadat adresu URL připojení signálů a tyto možnosti ve volání metody `MapHubs`. Chcete-li zadat vlastní adresu URL, nahraďte text "/SignalR" v příkladu adresou URL, kterou chcete použít.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>Jak vytvořit a používat třídy centra

Chcete-li vytvořit centrum, vytvořte třídu, která je odvozena z [Microsoft. ASPNET. signaler. hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx). Následující příklad ukazuje jednoduchou třídu centra pro aplikaci chatu.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

V tomto příkladu může připojený klient volat metodu `NewContosoChatMessage` a v případě, že je přijatá data, se budou všesměrově vysílat všem připojeným klientům.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>Doba života objektu centra

Nemusíte vytvářet instanci třídy centra ani volat své metody z vlastního kódu na serveru; To je vše, co pro vás prochází kanálem pro centra signalizace. Signál vytvoří novou instanci třídy centra pokaždé, když potřebuje zpracovat operaci centra, například když se klient připojí, odpojí nebo provede volání metody serveru.

Vzhledem k tomu, že instance třídy centra jsou přechodné, nemůžete je použít pro zachování stavu z jednoho volání metody do dalšího. Pokaždé, když server obdrží volání metody z klienta, zpracuje nová instance třídy hub zprávu. Chcete-li zachovat stav prostřednictvím více připojení a volání metod, použijte jinou metodu, jako je například databáze nebo statickou proměnnou na třídě centra, nebo jinou třídu, která není odvozena z `Hub`. Pokud uchováváte data v paměti pomocí metody, jako je statická proměnná na třídě centra, data budou ztracena při recyklování domény aplikace.

Pokud chcete odesílat zprávy klientům z vlastního kódu, který se spouští mimo třídu centra, nemůžete to provést vytvořením instance instance třídy centra, ale můžete to provést tak, že získáte odkaz na objekt kontextu signálu pro vaši třídu centra. Další informace najdete v tématu [jak volat klientské metody a spravovat skupiny mimo třídu centra](#callfromoutsidehub) dále v tomto tématu.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>Ve stylu CamelCase – velká a malá písmena názvů hub v klientech JavaScript

Ve výchozím nastavení klienti JavaScriptu odkazují na centra pomocí verze ve stylu CamelCase-použita názvu třídy. Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu. Předchozí příklad by se odkazoval jako `contosoChatHub` v kódu JavaScriptu.

**Server**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

Pokud chcete zadat jiný název, který budou klienti používat, přidejte atribut `HubName`. Použijete-li atribut `HubName`, nebudete mít v klientech jazyka JavaScript ve stylu CamelCase případnou změnu názvu.

**Server**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>Více Center

V aplikaci můžete definovat více tříd rozbočovačů. Když to uděláte, připojení se sdílí, ale skupiny se oddělují:

- Všichni klienti budou používat stejnou adresu URL k navázání připojení k signalizaci pomocí služby (/SignalR nebo vlastní adresy URL, pokud jste ji zadali), a toto připojení se používá pro všechna centra definovaná službou.

    V porovnání s definováním všech funkcí centra v jedné třídě neexistuje rozdíl mezi výkonem pro více Center.
- Všechna centra získají stejné informace požadavku HTTP.

    Vzhledem k tomu, že všechna centra sdílejí stejné připojení, jediné informace o požadavku HTTP, které server získá, jsou součástí původní žádosti HTTP, která vytváří připojení k signalizaci. Pokud použijete požadavek na připojení k předávání informací z klienta na server zadáním řetězce dotazu, nemůžete do různých Center zadávat různé řetězce dotazů. Všechna centra dostanou stejné informace.
- Vygenerovaný soubor proxy JavaScript bude obsahovat proxy pro všechna centra v jednom souboru.

    Informace o proxy serverech JavaScript najdete v tématu [Průvodce rozhraním API pro centra signalizace – JavaScriptový klient – vygenerovaný proxy server a co pro vás dělá](index.md).
- Skupiny se definují v rámci Center.

    V nástroji Signal můžete definovat pojmenované skupiny pro všesměrové vysílání pro submnožiny připojených klientů. Skupiny se uchovávají samostatně pro každé centrum. Například skupina s názvem "Administrators" by zahrnovala jednu sadu klientů pro třídu `ContosoChatHub` a stejný název skupiny by odkazoval na jinou sadu klientů pro třídu `StockTickerHub`.

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>Jak definovat metody ve třídě centra, které můžou klienti volat

K vystavení metody na rozbočovači, který chcete volat z klienta, deklarujte veřejnou metodu, jak je znázorněno v následujících příkladech.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

Můžete zadat návratový typ a parametry, včetně složitých typů a polí, stejně jako v libovolné C# metodě. Všechna data, která se zobrazí v parametrech nebo se vrátí volajícímu, se přenáší mezi klientem a serverem pomocí JSON a signalizace zpracovává vazbu složitých objektů a polí objektů automaticky.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>Ve stylu CamelCase – velká a malá písmena názvů metod v klientech JavaScript

Ve výchozím nastavení klienti JavaScriptu odkazují na metody centra pomocí verze ve stylu CamelCase-použita názvu metody. Signaler tuto změnu provede automaticky, aby kód JavaScriptu mohl vyhovovat konvencím JavaScriptu.

**Server**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

Pokud chcete zadat jiný název, který budou klienti používat, přidejte atribut `HubMethodName`.

**Server**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>Kdy spustit asynchronně

Pokud bude metoda dlouhodobě spuštěna nebo bude muset dělat práci, která by vyžadovala čekání, jako je například vyhledávání databáze nebo volání webové služby, udělejte asynchronní metodu tak, že vrátíte [úlohu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (místo `void` Return) nebo objekt [&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) objektu (místo `T` návratového typu). Při vrácení objektu `Task` z metody čeká signál, aby se `Task` dokončil, a poté pošle nezabalený výsledek zpátky klientovi, takže nedochází k žádnému rozdílu ve způsobu, jakým je volání metody v klientovi nijak zakódovat.

Když se metoda rozbočovače stane asynchronním, vyhnete se tak blokování připojení při použití přenosu protokolu WebSocket. Když se metoda rozbočovače provádí synchronně a přenos je WebSocket, následné vyvolání metod v centru od stejného klienta se zablokuje, dokud se nedokončí metoda centra.

Následující příklad ukazuje stejný kód pro spuštění synchronně nebo asynchronně, následovaný kódem JavaScriptu klienta, který funguje pro volání buď verze.

**Synchronizace**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

**Asynchronní – ASP.NET 4,5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

Další informace o použití asynchronních metod v ASP.NET 4,5 najdete v tématu [Použití asynchronních metod v ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).

<a id="overloads"></a>

### <a name="defining-overloads"></a>Definování přetížení

Pokud chcete definovat přetížení pro metodu, počet parametrů v každém přetížení musí být jiný. Pokud odlišujete přetížení pouhým zadáním různých typů parametrů, vaše třída centra se zkompiluje, ale služba Signaler vyvolá výjimku za běhu, když se klienti pokusí zavolat jedno z přetížení.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>Volání metod klienta z třídy hub

Chcete-li volat metody klienta ze serveru, použijte vlastnost `Clients` v metodě ve třídě hub. Následující příklad ukazuje serverový kód, který volá `addNewMessageToPage` na všech připojených klientech, a klientský kód, který definuje metodu v klientovi jazyka JavaScript.

**Server**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

Z metody klienta nelze získat návratovou hodnotu. syntaxe, jako je `int x = Clients.All.add(1,1)`, nefunguje.

Můžete zadat komplexní typy a pole pro parametry. Následující příklad předá klientovi komplexní typ v parametru metody.

**Serverový kód, který volá metodu klienta využívající složitý objekt**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

**Kód serveru, který definuje komplexní objekt**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>Výběr klientů, kteří budou přijímat RPC

Vlastnost klienti vrátí objekt [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) , který poskytuje několik možností určení klientů, kteří budou přijímat RPC:

- Všichni připojení klienti.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- Pouze volající klient.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- Všichni klienti s výjimkou volajícího klienta.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- Konkrétní klient identifikovaný IDENTIFIKÁTORem připojení.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    Tento příklad volá `addContosoChatMessageToPage` na volajícím klientovi a má stejný účinek jako použití `Clients.Caller`.
- Všichni připojení klienti s výjimkou určených klientů identifikovaných IDENTIFIKÁTORem připojení

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- Všichni připojení klienti v zadané skupině.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- Všechny připojené klienty v zadané skupině s výjimkou určených klientů identifikovaných podle ID připojení

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- Všichni připojení klienti v zadané skupině s výjimkou volajícího klienta.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>Žádné ověřování v době kompilace pro názvy metod

Název metody, který zadáte, je interpretován jako dynamický objekt, což znamená, že pro něj není k dispozici žádná technologie IntelliSense nebo kompilace. Výraz je vyhodnocen v době běhu. Když se spustí volání metody, Signal pošle klientovi název metody a hodnoty parametrů, a pokud má klient metodu, která odpovídá názvu, je tato metoda volána a hodnoty parametrů jsou předány. Pokud není v klientovi nalezena žádná vyhovující metoda, není vyvolána žádná chyba. Informace o formátu dat, která signalizace přenáší klientovi na pozadí při volání metody klienta, najdete v tématu [Úvod do nástroje Signal](index.md).

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>Porovnávání názvů metod bez rozlišení velkých a malých písmen

Porovnávání názvů metod nerozlišuje velká a malá písmena. Například `Clients.All.addContosoChatMessageToPage` na serveru spustí `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`nebo `addContosoChatMessageToPage` na klientovi.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>Asynchronní spuštění

Volanou metodu provádí asynchronně. Jakýkoli kód, který přichází po volání metody do klienta, se spustí okamžitě bez čekání na dokončení přenosu dat do klientů, pokud nezadáte, že následující řádky kódu by měly čekat na dokončení metody. Následující příklady kódu ukazují, jak postupně spouštět dvě metody klienta, jednu pomocí kódu, který funguje v rozhraní .NET 4,5, a jeden pomocí kódu, který funguje v rozhraní .NET 4.

**Příklad .NET 4,5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

**Příklad .NET 4**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

Použijete-li `await` nebo `ContinueWith` počkat na dokončení metody klienta před provedením dalšího řádku kódu, neznamená to, že klienti budou zprávu před spuštěním dalšího řádku kódu zobrazovat. "Dokončování" volání metody klienta znamená, že Signal dokončil vše potřebné k odeslání zprávy. Pokud potřebujete ověření, že klienti obdrželi zprávu, musíte tento mechanismus programovat sami. Například můžete kód metody `MessageReceived` v centru a v metodě `addContosoChatMessageToPage` na klientovi, kterou byste mohli volat `MessageReceived` po jakékoli práci, kterou potřebujete udělat na klientovi. V `MessageReceived` v centru můžete provádět práci, která závisí na skutečném příjmu a zpracování původního volání metody.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>Jak použít řetězcovou proměnnou jako název metody

Pokud chcete vyvolat metodu klienta pomocí proměnné řetězce jako název metody, přetypujte `Clients.All` (nebo `Clients.Others`, `Clients.Caller`atd.) na `IClientProxy` a pak zavolejte metodu [Invoke (MethodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>Správa členství ve skupinách z třídy hub

Skupiny v nástroji Signal poskytují metodu pro vysílání zpráv pro zadané podmnožiny připojených klientů. Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin.

Chcete-li spravovat členství ve skupině, použijte metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) a [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) poskytované vlastností `Groups` třídy hub. Následující příklad ukazuje metody `Groups.Add` a `Groups.Remove` používané v metodách centra, které jsou volány klientským kódem, následovaný kódem jazyka JavaScript, který je volá.

**Server**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

**Klient jazyka JavaScript pomocí vygenerovaného proxy**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

Nemusíte explicitně vytvářet skupiny. V důsledku toho se skupina automaticky vytvoří při prvním zadání názvu při volání `Groups.Add`a odstraní se, když odeberete Poslední připojení z jeho členství.

Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin. Signal odesílá zprávy klientům a skupinám na základě [modelu Pub/sub](http://en.wikipedia.org/wiki/Publish/subscribe)a server neudržuje seznamy skupin nebo členství ve skupinách. To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, všechny stavy, které tento signál udržuje, musí být šířeny do nového uzlu.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Asynchronní provádění metod Add a Remove

Metody `Groups.Add` a `Groups.Remove` provádějí asynchronně. Chcete-li přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, je nutné zajistit, aby byla metoda `Groups.Add` dokončena jako první. Následující příklady kódu ukazují, jak to provést, pomocí kódu, který funguje v rozhraní .NET 4,5 a jeden pomocí kódu, který funguje v rozhraní .NET 4.

**Příklad .NET 4,5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

**Příklad .NET 4**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>Trvalost členství ve skupině

Signál sleduje připojení, ne uživatele, takže pokud chcete, aby byl uživatel ve stejné skupině pokaždé, když uživatel vytvoří připojení, je nutné volat `Groups.Add` pokaždé, když uživatel vytvoří nové připojení.

Po dočasné ztrátě připojení občas může signál obnovit připojení automaticky. V takovém případě odesílatel obnovuje stejné připojení, nevytváří nové připojení, takže se automaticky obnoví členství klienta ve skupině. To je možné i v případě, že dočasné přerušení je výsledkem restartování nebo selhání serveru, protože stav připojení pro každého klienta, včetně členství ve skupinách, je Trip klientovi. Pokud dojde k výpadku serveru a jeho nahrazením novým serverem před vypršením časového limitu připojení, může se klient automaticky znovu připojit k novému serveru a znovu zaregistrovat do skupin, které je členem.

Pokud se připojení nedá obnovit automaticky po ztrátě připojení, nebo když vypršel časový limit připojení, nebo když se klient odpojí (například když se v prohlížeči přejde na novou stránku), ztratí se členství ve skupině. Až se uživatel příště připojí, vytvoří se nové připojení. Aby se zachovalo členství ve skupině, když stejný uživatel vytváří nové připojení, musí vaše aplikace sledovat přidružení uživatelů a skupin a obnovovat členství ve skupině pokaždé, když uživatel vytvoří nové připojení.

Další informace o připojení a opětovném připojení najdete v tématu [postup zpracování událostí životního cyklu připojení v třídě centra](#connectionlifetime) dále v tomto tématu.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>Skupiny s jedním uživatelem

Aplikace, které používají signál, obvykle musí sledovat přidružení mezi uživateli a připojení, aby věděli, který uživatel odeslal zprávu a kteří uživatelé by měli zprávu přijímat. Skupiny se používají v jednom ze dvou běžně používaných vzorů.

- Skupiny s jedním uživatelem.

    Můžete zadat uživatelské jméno jako název skupiny a při každém připojení nebo opětovném připojení uživatele přidat aktuální ID připojení ke skupině. K odesílání zpráv uživateli, který jste odeslali do skupiny. Nevýhodou této metody je, že skupina neposkytuje způsob, jak zjistit, jestli je uživatel online nebo offline.
- Sledujte přidružení mezi uživatelskými jmény a identifikátory připojení.

    Můžete uložit přidružení mezi jednotlivými uživatelskými jmény a jedním nebo více ID připojení ve slovníku nebo databázi a při každém připojení nebo odpojení uživatele aktualizovat uložená data. K odesílání zpráv uživateli zadejte ID připojení. Nevýhodou této metody je, že má více paměti.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>Postup zpracování událostí životního cyklu připojení ve třídě centra

Typickými důvody pro zpracování událostí životního cyklu připojení je sledovat, zda je uživatel připojen nebo nikoli, a sledovat přidružení mezi uživatelskými jmény a identifikátory připojení. Chcete-li spustit vlastní kód, když se klienti připojují nebo odpojí, přepište `OnConnected`, `OnDisconnected`a `OnReconnected` virtuální metody třídy hub, jak je znázorněno v následujícím příkladu.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>Když se připojí, odpojí se a OnReconnected se zavolají.

Pokaždé, když prohlížeč přejde na novou stránku, je nutné vytvořit nové připojení, což znamená, že signál spustí metodu `OnDisconnected` následovanou metodou `OnConnected`. Při navázání nového připojení se signálem vždy vytvoří nové ID připojení.

Metoda `OnReconnected` se volá, když se dokončí dočasná přerušení připojení, na které se může signál automaticky zotavit, například když se kabel dočasně odpojí a znovu připojí před vypršením časového limitu připojení. Metoda `OnDisconnected` je volána, když je klient odpojen a uživatel se nemůže automaticky znovu připojit, například když prohlížeč přejde na novou stránku. Proto je možné posloupnost událostí pro daného klienta `OnConnected`, `OnReconnected``OnDisconnected`; nebo `OnConnected``OnDisconnected`. Pro dané připojení se nezobrazí `OnConnected`sekvence, `OnDisconnected``OnReconnected`.

Metoda `OnDisconnected` se v některých scénářích nevolá, například když dojde k výpadku serveru nebo pokud se doména aplikace recykluje. Když je na řádku nebo v doméně aplikace dokončená recyklace jiného serveru, můžou se někteří klienti moci znovu připojit a spustit událost `OnReconnected`.

Další informace najdete v tématu [porozumění a zpracování událostí životního cyklu připojení v nástroji Signal](index.md).

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>Stav volajícího není naplněný.

Metody obslužné rutiny události doby života připojení jsou volány ze serveru, což znamená, že všechny stavy, které umístíte do objektu `state` v klientovi, nebudou naplněny do vlastnosti `Caller` na serveru. Informace o objektu `state` a vlastnosti `Caller` naleznete v tématu [jak předat stav mezi klienty a třídou centra](#passstate) dále v tomto tématu.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>Jak získat informace o klientovi z kontextové vlastnosti

Chcete-li získat informace o klientovi, použijte vlastnost `Context` třídy centra. Vlastnost `Context` vrátí objekt [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) , který poskytuje přístup k následujícím informacím:

- ID připojení volajícího klienta.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    ID připojení je identifikátor GUID, který je přiřazený signálem (hodnotu nemůžete zadat ve svém vlastním kódu). Pro každé připojení existuje jedno ID připojení a stejné ID připojení se používá pro všechna centra, pokud máte ve své aplikaci více rozbočovačů.
- Data hlavičky protokolu HTTP.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    Můžete také získat hlavičku protokolu HTTP z `Context.Headers`. Důvodem pro více odkazů na stejnou věc je, že nejprve byl vytvořen `Context.Headers`, byla vlastnost `Context.Request` přidána později a `Context.Headers` byla zachována z důvodu zpětné kompatibility.
- Dotaz na data řetězce.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    Můžete také získat data řetězce dotazu z `Context.QueryString`.

    Řetězec dotazu, který získáte v této vlastnosti, je ten, který se použil s požadavkem HTTP, který vytvořil připojení k signalizaci. Můžete přidat parametry řetězce dotazu do klienta nakonfigurováním připojení, což je pohodlný způsob, jak předat data o klientovi z klienta na server. Následující příklad ukazuje jeden ze způsobů, jak přidat řetězec dotazu v klientovi jazyka JavaScript při použití vygenerovaného proxy serveru.

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    Další informace o nastavení parametrů řetězce dotazu najdete v příručkách k rozhraní API pro klienty [JavaScriptu](index.md) a [.NET](index.md) .

    Metodu přenosu, která se používá pro připojení v datech řetězce dotazu, můžete najít spolu s jinými hodnotami, které interně používají signály:

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    Hodnota `transportMethod` bude "WebSockets", "serverSentEvents", "foreverFrame" nebo "longPolling". Všimněte si, že pokud zaškrtnete tuto hodnotu v metodě obslužné rutiny události `OnConnected`, může v některých scénářích zpočátku získat přenosovou hodnotu, která není koncovým vysjednaným způsobem přenosu pro připojení. V takovém případě metoda vyvolá výjimku a bude volána později po navázání finální metody přenosu.
- Soubory cookie.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    Soubory cookie můžete také získat z `Context.RequestCookies`.
- Informace o uživateli.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- Objekt HttpContext pro požadavek:

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    Místo `HttpContext.Current` k získání `HttpContext` objektu pro připojení k signalizaci použijte tuto metodu.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>Postup předání stavu mezi klienty a třídou centra

Klient proxy serveru poskytuje objekt `state`, ve kterém můžete ukládat data, která chcete přenést na server, pomocí jednotlivých volání metody. Na serveru můžete získat přístup k těmto datům ve vlastnosti `Clients.Caller` v metodách centra, které jsou volány klienty. Vlastnost `Clients.Caller` není vyplněna pro metody obslužné rutiny události doby života připojení `OnConnected`, `OnDisconnected`a `OnReconnected`.

Vytváření a aktualizace dat v objektu `state` a vlastnost `Clients.Caller` funguje v obou směrech. Hodnoty na serveru můžete aktualizovat a předávat je zpátky klientovi.

Následující příklad ukazuje kód klienta JavaScriptu, který ukládá stav pro přenos do serveru při každém volání metody.

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

Následující příklad ukazuje ekvivalentní kód v klientovi .NET.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

Ve třídě centra máte přístup k těmto datům ve vlastnosti `Clients.Caller`. Následující příklad ukazuje kód, který načte stav uvedený v předchozím příkladu.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> Tento mechanismus pro trvalý stav není určený pro velké objemy dat, protože vše, co vložíte do vlastnosti `state` nebo `Clients.Caller`, je Round-Trip s každým voláním metody. Je vhodný pro menší položky, jako jsou uživatelská jména nebo čítače.

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>Jak zpracovávat chyby ve třídě centra

Chcete-li zpracovat chyby, ke kterým dochází v metodách vaší třídy centra, použijte jednu nebo obě následující metody:

- Zabalte kód metody v blocích try-catch a Zaprotokolujte objekt výjimky. Pro účely ladění můžete výjimku odeslat klientovi, ale z bezpečnostních důvodů, které odesílají podrobné informace klientům v produkčním prostředí, se nedoporučuje.
- Vytvořte modul kanálu centra, který zpracovává metodu [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) . Následující příklad ukazuje modul kanálu, který protokoluje chyby, následovaný kódem v Global. asax, který vloží modul do kanálu rozbočovače.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

Další informace o modulech kanálu centra najdete v tématu [Postup přizpůsobení kanálu centra](#hubpipeline) dále v tomto tématu.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>Jak povolit trasování

Chcete-li povolit trasování na straně serveru, přidejte do souboru Web. config prvek System. Diagnostics, jak je znázorněno v následujícím příkladu:

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

Při spuštění aplikace v aplikaci Visual Studio můžete zobrazit protokoly v okně **výstup** .

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>Jak volat klientské metody a spravovat skupiny mimo třídu centra

Chcete-li volat metody klienta z jiné třídy než vaší třídy centra, získejte odkaz na objekt kontextu signálu pro centrum a použijte jej ke volání metod v klientovi nebo správě skupin.

Následující vzorová `StockTicker` Třída získá objekt kontextu, uloží ho do instance třídy, uloží instanci třídy do statické vlastnosti a použije kontext z instance třídy singleton k volání metody `updateStockPrice` na klientech, kteří jsou připojení k centru s názvem `StockTickerHub`.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

Pokud je třeba v dlouhodobém objektu použít kontext vícekrát, získejte odkaz a uložte ho místo pokaždé, když ho budete potřebovat znovu. Když se kontext získá, zajistíte tak, že signál klientům pošle zprávy ve stejném pořadí, ve kterém vaše metody rozbočovače provedou vyvolání metod klienta. Kurz, ve kterém se dozvíte, jak používat kontext signalizace pro centrum, najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal](index.md).

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>Volání metod klienta

Můžete určit, kteří klienti obdrží RPC, ale máte méně možností než při volání z třídy centra. Důvodem je, že kontext není přidružen ke konkrétnímu volání z klienta, takže žádné metody, které vyžadují znalosti aktuálního ID připojení, například `Clients.Others`nebo `Clients.Caller`nebo `Clients.OthersInGroup`, nejsou k dispozici. K dispozici jsou následující možnosti:

- Všichni připojení klienti.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- Konkrétní klient identifikovaný IDENTIFIKÁTORem připojení.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- Všichni připojení klienti s výjimkou určených klientů identifikovaných IDENTIFIKÁTORem připojení

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- Všichni připojení klienti v zadané skupině.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- Všechny připojené klienty v zadané skupině s výjimkou určených klientů identifikovaných podle ID připojení

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

Pokud voláte do nehub třídy z metod ve třídě centra, můžete předat aktuální ID připojení a použít ho pomocí `Clients.Client`, `Clients.AllExcept`nebo `Clients.Group` pro simulaci `Clients.Caller`, `Clients.Others`nebo `Clients.OthersInGroup`. V následujícím příkladu třída `MoveShapeHub` předá ID připojení ke třídě `Broadcaster`, aby třída `Broadcaster` mohla simulovat `Clients.Others`.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>Správa členství ve skupinách

Pro správu skupin máte stejné možnosti jako v rámci třídy centra.

- Přidání klienta do skupiny

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- Odebrání klienta ze skupiny

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>Postup přizpůsobení kanálu Center

Signaler umožňuje vložit do kanálu rozbočovače vlastní kód. Následující příklad ukazuje vlastní modul kanálů rozbočovače, který protokoluje každé volání příchozí metody přijaté z klienta a odchozí volání metody vyvolané na klientovi:

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

Následující kód v souboru *Global. asax* registruje modul, který se má spustit v kanálu centra:

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

Existuje mnoho různých metod, které lze přepsat. Úplný seznam naleznete v tématu [metody HubPipelineModule](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).
