---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Kurz: všesměrové vysílání serveru pomocí návěstí 2 | Microsoft Docs'
author: tdykstra
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET Signal 2 k poskytování funkcí všesměrového vysílání serveru.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536601"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>Kurz: všesměrové vysílání serveru pomocí Signaler 2

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET Signal 2 k poskytování funkcí všesměrového vysílání serveru. Všesměrové vysílání serveru znamená, že server spouští komunikaci odesílaná klientům.

Aplikace, kterou vytvoříte v tomto kurzu, simuluje burzovní, což je typický scénář pro funkce všesměrového vysílání serveru. Server pravidelně aktualizuje skladové ceny a vysílá aktualizace všem připojeným klientům. V prohlížeči se čísla a symboly ve sloupcích **změnit** a **%** dynamicky mění v reakci na oznámení ze serveru. Pokud otevřete další prohlížeče na stejné adrese URL, všechny zobrazí stejná data a stejné změny dat současně.

![Vytvoření webu](tutorial-server-broadcast-with-signalr/_static/image1.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvoření projektu
> * Nastavení serverového kódu
> * Kontrola kódu serveru
> * Nastavení kódu klienta
> * Projděte si kód klienta.
> * Testování aplikace
> * Povolte protokolování

> [!IMPORTANT]
> Pokud nechcete s postupem sestavování aplikace pracovat, můžete do nového prázdného projektu webové aplikace ASP.NET nainstalovat Signal. ukázkový balíček. Pokud nainstalujete balíček NuGet bez provedení kroků v tomto kurzu, musíte postupovat podle pokynů v souboru *Readme. txt* . Chcete-li spustit balíček, je třeba přidat třídu pro spuštění OWIN, která volá metodu `ConfigureSignalR` v nainstalovaném balíčku. Pokud nepřidáte třídu Startup OWIN, zobrazí se chybová zpráva. Viz část [instalace ukázky StockTicker](#install-the-stockticker-sample) tohoto článku.

## <a name="prerequisites"></a>Předpoklady

* Sada [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) se sadou funkcí **Vývoj pro ASP.NET a web**.

## <a name="create-the-project"></a>Vytvoření projektu

V této části se dozvíte, jak použít Visual Studio 2017 k vytvoření prázdné webové aplikace v ASP.NET.

1. V aplikaci Visual Studio vytvořte webovou aplikaci v ASP.NET.

    ![Vytvoření webu](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. V okně **Nová webová aplikace v ASP.NET – signaler. StockTicker** ponechte vybrané **prázdné** a vyberte **OK**.

## <a name="set-up-the-server-code"></a>Nastavení serverového kódu

V této části nastavíte kód, který běží na serveru.

### <a name="create-the-stock-class"></a>Vytvoření třídy akcie

Začnete vytvořením třídy *burzovního* modelu, kterou použijete k ukládání a přenosu informací o zásobách.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **třídu**.

1. Pojmenujte třídu *Stock* a přidejte ji do projektu.

1. Nahraďte kód v souboru *Stock.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    Dvě vlastnosti, které nastavíte při vytváření akcií, jsou `Symbol` (například MSFT pro Microsoft) a `Price`. Ostatní vlastnosti závisí na tom, jak a kdy jste nastavili `Price`. Při prvním nastavení `Price`se hodnota rozšíří na `DayOpen`. Po nastavení `Price`aplikace vypočítá hodnoty vlastností `Change` a `PercentChange` na základě rozdílu mezi `Price` a `DayOpen`.

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>Vytvoření tříd StockTickerHub a StockTicker

K řízení interakce mezi klientem a serverem použijete rozhraní API centra signalizace. Třída `StockTickerHub`, která je odvozena od `Hub` Signal třídy, bude zpracovávat přijímání připojení a volání metod od klientů. Také je nutné zachovat skladová data a spustit objekt `Timer`. Objekt `Timer` bude pravidelně spouštět cenové aktualizace nezávisle na připojeních klienta. Tyto funkce nemůžete umístit do `Hub` třídy, protože rozbočovače jsou přechodné. Aplikace vytvoří instanci `Hub` třídy pro každý úkol v centru, jako třeba připojení a volání z klienta na server. Proto mechanismus, který udržuje skladová data, aktualizuje ceny a vysílá, je nutné, aby ceny aktualizací běžely v samostatné třídě. Pojmenujte třídu `StockTicker`.

![Všesměrové vysílání z StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

Přejete si, aby na serveru běžela jenom jedna instance `StockTicker` třídy, takže budete muset nastavit odkaz z každé instance `StockTickerHub` na instanci `StockTicker` typu singleton. Třída `StockTicker` musí vysílat klientům, protože má uložená data a triggery, ale `StockTicker` není třída `Hub`. Třída `StockTicker` musí získat odkaz na objekt kontextu připojení centra signalizace. Pak může pomocí objektu kontextu připojení vysílače vysílat klientům.

#### <a name="create-stocktickerhubcs"></a>Vytvořit StockTickerHub.cs

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.

1. V **položce Přidat novou položku-Signal. StockTicker**vyberte **Installed** > **Visual C#**  > **Web** > **signaler** a pak vyberte **Třída centra signalizace (v2)** .

1. Pojmenujte třídu *StockTickerHub* a přidejte ji do projektu.

    Tento krok vytvoří soubor třídy *StockTickerHub.cs* . Současně přidá sadu souborů skriptu a odkazy na sestavení, které podporuje signalizaci do projektu.

1. Nahraďte kód v souboru *StockTickerHub.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. Uložte soubor.

Aplikace používá třídu [centra](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) k definování metod, které mohou klienti volat na serveru. Definujete jednu metodu: `GetAllStocks()`. Když se klient poprvé připojí k serveru, zavolá tuto metodu, aby získal seznam všech populací s jejich aktuálními cenami. Metoda může běžet synchronně a vracet `IEnumerable<Stock>`, protože vrací data z paměti.

Pokud metoda musela získat data pomocí něčeho, co by vyžadovala čekání, jako je vyhledávání databáze nebo volání webové služby, zadejte `Task<IEnumerable<Stock>>` jako návratovou hodnotu pro povolení asynchronního zpracování. Další informace najdete v tématu [Průvodce rozhraním API pro centra ASP.NET signálu – Server – kdy se má provést asynchronní spuštění](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).

Atribut `HubName` určuje, jak bude aplikace odkazovat na centrum v kódu JavaScriptu na klientovi. Výchozí název v klientovi Pokud tento atribut nepoužíváte, je camelCase verze názvu třídy, který v tomto případě by byl `stockTickerHub`.

Jak uvidíte později při vytváření `StockTicker` třídy, aplikace vytvoří instanci typu Singleton této třídy ve své statické vlastnosti `Instance`. Tato instance typu Singleton `StockTicker` je v paměti bez ohledu na počet klientů, kteří se připojují nebo odpojí. Tato instance je to, co metoda `GetAllStocks()` používá k vrácení aktuálních informací o zásobách.

#### <a name="create-stocktickercs"></a>Create StockTicker.cs

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **třídu**.

1. Pojmenujte třídu *StockTicker* a přidejte ji do projektu.

1. Nahraďte kód v souboru *StockTicker.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

Vzhledem k tomu, že všechna vlákna budou spouštět stejnou instanci StockTicker kódu, musí být třída StockTicker bezpečná pro přístup z více vláken.

### <a name="examine-the-server-code"></a>Kontrola kódu serveru

Pokud prohlížíte kód serveru, pomůže vám pochopit, jak aplikace funguje.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>Ukládání instance singleton do statického pole

Kód inicializuje pole static `_instance`, které vrátí vlastnost `Instance` s instancí třídy. Vzhledem k tomu, že konstruktor je privátní, je jedinou instancí třídy, kterou může aplikace vytvořit. Aplikace používá [opožděnou inicializaci](/dotnet/framework/performance/lazy-initialization) pro pole `_instance`. Není z důvodů výkonu. Je potřeba se ujistit, že vytváření instancí je bezpečné pro přístup z více vláken.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

Pokaždé, když se klient připojí k serveru, nová instance třídy StockTickerHub spuštěné v samostatném vlákně získá instanci StockTicker singleton z vlastnosti `StockTicker.Instance` static, jak jste viděli dříve ve třídě `StockTickerHub`.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Ukládání uložených dat v ConcurrentDictionary

Konstruktor inicializuje kolekci `_stocks` s některými ukázkovými datovými daty a `GetAllStocks` vrátí tyto akcie. Jak bylo uvedeno dříve, tato kolekce populací je vrácena `StockTickerHub.GetAllStocks`, což je metoda serveru ve třídě `Hub`, kterou mohou klienti volat.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

Kolekce akcie je definována jako [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) typ pro bezpečnost vlákna. Jako alternativu můžete použít objekt [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) a explicitně zamknout slovník při provádění změn v něm.

Pro tuto ukázkovou aplikaci je to v pořádku, pokud ukládáte data aplikace do paměti a ztratíte data, když aplikace odstraní instanci `StockTicker`. V reálné aplikaci byste měli pracovat s back-end datovým úložištěm, jako je databáze.

#### <a name="periodically-updating-stock-prices"></a>Pravidelná aktualizace cen akcií

Konstruktor spustí objekt `Timer`, který pravidelně volá metody, které aktualizují skladové ceny náhodným základem.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer` volá `UpdateStockPrices`, která předá hodnotu null v parametru State. Před aktualizací cen aplikace převezme zámek na objekt `_updateStockPricesLock`. Kód zkontroluje, jestli už jiný podproces aktualizuje ceny, a pak na každý Sklad v seznamu zavolá `TryUpdateStockPrice`. `TryUpdateStockPrice` metoda rozhoduje o tom, jestli se má změnit cena akcií, a kolik se má změnit. Pokud se změní cena akcií, aplikace zavolá `BroadcastStockPrice`, aby vysílaly na všech připojených klientech změnu ceny akcií.

Příznak `_updatingStockPrices` označený jako [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) , aby se zajistilo, že je bezpečný pro přístup z více vláken.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

V reálné aplikaci by metoda `TryUpdateStockPrice` zavolala webovou službu, aby vyhledala cenu. V tomto kódu aplikace používá generátor náhodných čísel k náhodnému provedení změn.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>Získání kontextu signálu, aby třída StockTicker mohla vysílat klientům

Vzhledem k tomu, že změny ceny pocházejí zde v objektu `StockTicker`, je objekt, který musí volat metodu `updateStockPrice` na všech připojených klientech. Ve třídě `Hub` máte rozhraní API pro volání metod klienta, ale `StockTicker` nejsou odvozeny od třídy `Hub` a nemají odkaz na žádný objekt `Hub`. Pro všesměrové vysílání pro připojené klienty musí třída `StockTicker` získat kontextovou instanci signálu pro `StockTickerHub` třídu a použít ji pro volání metod v klientech.

Kód získá odkaz na kontext signalizace při vytvoření instance třídy singleton, předá tento odkaz na konstruktor a konstruktor ho vloží do vlastnosti `Clients`.

Existují dva důvody, proč chcete kontext získat pouze jednou: získání kontextu je nákladná úloha a když aplikace zachová zamýšlené pořadí zpráv odesílaných klientovi.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

Získání vlastnosti `Clients` kontextu a jeho vložení do vlastnosti `StockTickerClient` umožňuje napsat kód pro volání klientských metod, které vypadají stejně jako ve třídě `Hub`. Chcete-li například vysílat do všech klientů, můžete zapisovat `Clients.All.updateStockPrice(stock)`.

Metoda `updateStockPrice`, kterou voláte v `BroadcastStockPrice`, ještě neexistuje. Později ji přidáte při psaní kódu, který běží na klientovi. Na `updateStockPrice` tady můžete odkazovat, protože `Clients.All` je dynamická, což znamená, že aplikace vyhodnotí výraz za běhu. Když se spustí toto volání metody, odesílatel pošle do klienta název metody a hodnotu parametru. Pokud má klient metodu s názvem `updateStockPrice`, aplikace tuto metodu zavolá a předá jí hodnotu parametru.

`Clients.All` znamená odeslání všem klientům. Signalizace nabízí další možnosti určení klientů nebo skupin klientů, které se mají odeslat. Další informace najdete v tématu [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>Registrace trasy signalizace

Server musí znát, která adresa URL má zachytit a směrovat na signál. K tomu přidejte třídu pro spuštění OWIN:

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.

1. V **položce Přidat novou položku-Signal. StockTicker** vyberte **nainstalované** > **Visual C#**  > **Web** a pak vyberte **třídu pro spuštění Owin**.

1. Pojmenujte *spouštěcí* třídu a vyberte **OK**.

1. Nahraďte výchozí kód v souboru *Startup.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

Nyní jste dokončili nastavování kódu serveru. V další části nastavíte klienta.

## <a name="set-up-the-client-code"></a>Nastavení kódu klienta

V této části nastavíte kód, který se spouští na klientovi.

### <a name="create-the-html-page-and-javascript-file"></a>Vytvoření stránky HTML a souboru JavaScriptu

Na stránce HTML se zobrazí data a soubor JavaScriptu bude organizovat data.

#### <a name="create-stocktickerhtml"></a>Create StockTicker.html

Nejprve přidáte klienta HTML.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **stránku HTML**.

1. Pojmenujte soubor *StockTicker* a vyberte **OK**.

1. Nahraďte výchozí kód v souboru *StockTicker. html* tímto kódem:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    KÓD HTML vytvoří tabulku s pěti sloupci, řádkem záhlaví a datovým řádkem s jedinou buňkou, která zahrnuje všechny pět sloupců. Řádek dat zobrazuje "načítání..." při každém spuštění aplikace. JavaScriptový kód odstraní tento řádek a přidá ho do svých řádků s uloženými daty načtenými ze serveru.

    Značky skriptu určují:

    * Soubor skriptu jQuery.

    * Základní soubor skriptu nástroje Signaler.

    * Soubor skriptu proxy signalizace.

    * Soubor skriptu StockTicker, který vytvoříte později.

    Aplikace dynamicky generuje soubor skriptu proxy serverů signalizace. Určuje adresu URL "/SignalR/Hubs" a definuje metody proxy pro metody ve třídě hub, v tomto případě pro `StockTickerHub.GetAllStocks`. Pokud budete chtít, můžete tento soubor JavaScriptu vygenerovat ručně pomocí [nástrojů pro signalizaci](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/). Nezapomeňte zakázat dynamické vytváření souborů ve volání metody `MapHubs`.

1. V **Průzkumník řešení**rozbalte položku **skripty**.

    Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.

    > [!IMPORTANT]
    > Správce balíčků nainstaluje novější verzi skriptů nástroje Signal.

1. Aktualizujte odkazy na skripty v bloku kódu tak, aby odpovídaly verzím souborů skriptu v projektu.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na *StockTicker. html*a pak vyberte **nastavit jako úvodní stránku**.

#### <a name="create-stocktickerjs"></a>Create StockTicker.js

Nyní vytvořte soubor JavaScriptu.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **soubor JavaScriptu**.

1. Pojmenujte soubor *StockTicker* a vyberte **OK**.

1. Přidejte tento kód do souboru *StockTicker. js* :

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>Projděte si kód klienta.

Pokud prohlížíte kód klienta, pomůže vám se dozvědět, jak kód klienta komunikuje s kódem serveru, aby aplikace fungovala.

#### <a name="starting-the-connection"></a>Spouští se připojení.

`$.connection` odkazuje na proxy signálů. Kód získá odkaz na proxy pro třídu `StockTickerHub` a vloží jej do proměnné `ticker`. Název proxy je název, který byl nastaven atributem `HubName`:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

Po definování všech proměnných a funkcí se poslední řádek kódu v souboru inicializuje připojením k signalizaci voláním funkce Signal `start`. Funkce `start` provádí asynchronní a vrací [odložený objekt jQuery](http://api.jquery.com/category/deferred-object/). Můžete zavolat funkci Hotovo pro určení funkce, která má být volána, když aplikace dokončí asynchronní akci.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>Získávání všech populací

Funkce `init` volá funkci `getAllStocks` na serveru a používá informace, které server vrátí k aktualizaci skladové tabulky. Všimněte si, že ve výchozím nastavení je nutné použít camelCasing na straně klienta, i když název metody je Pascal-použita na serveru. Pravidlo camelCasing se vztahuje pouze na metody, nikoli na objekty. Například odkazujete na `stock.Symbol` a `stock.Price`, nikoli `stock.symbol` nebo `stock.price`.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

V metodě `init` aplikace vytvoří HTML pro řádek tabulky pro každý burzovní objekt přijatý ze serveru voláním `formatStock` k formátování vlastností objektu `stock` a následným voláním `supplant` k nahrazení zástupných symbolů v `rowTemplate` proměnné s hodnotami vlastností objektu `stock`. Výsledný kód HTML se pak připojí k uložené tabulce.

> [!NOTE]
> Zavoláte `init` tím, že ho předáte do jako `callback` funkce, která se spustí po dokončení asynchronní funkce `start`. Pokud jste po volání `start`zavolali `init` jako samostatný příkaz jazyka JavaScript, funkce by nebyla úspěšná, protože by běžela okamžitě bez čekání na dokončení funkce Start pro dokončení navázání připojení. V takovém případě se funkce `init` pokusí zavolat funkci `getAllStocks` předtím, než aplikace naváže připojení k serveru.

#### <a name="getting-updated-stock-prices"></a>Získání aktualizovaných cen akcií

Když server změní cenu akcií, zavolá `updateStockPrice` v připojených klientech. Aplikace přidá funkci do vlastnosti klient `stockTicker`ového proxy serveru, aby byla dostupná pro volání ze serveru.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

Funkce `updateStockPrice` formátuje burzovní objekt přijatý ze serveru do řádku tabulky stejným způsobem jako ve funkci `init`. Místo připojení řádku k tabulce najde aktuální řádek v tabulce a nahradí ho novým řádkem.

## <a name="test-the-application"></a>Testování aplikace

Aplikaci můžete otestovat a ujistit se, že funguje. Zobrazí se všechna okna prohlížeče s živými zásobami, kde se pohybuje ceny akcií.

1. Na panelu nástrojů zapněte **ladění skriptů** a pak výběrem tlačítka Přehrát spusťte aplikaci v režimu ladění.

    ![Snímek obrazovky uživatele, který zapíná režim ladění a vybere možnost Přehrát.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    Otevře se okno prohlížeče, ve kterém se zobrazí **tabulka živé akcie**. V tabulce se zpočátku zobrazuje "načítání...". Po krátké době aplikace zobrazuje počáteční skladová data a pak se ceny akcií začnou měnit.

1. Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.

    Počáteční zobrazovací displej je stejný jako první prohlížeč a změny probíhají současně.

1. Zavřete všechny prohlížeče, otevřete nový prohlížeč a přejdete na stejnou adresu URL.

    Objekt typu Singleton StockTicker pokračuje v běhu na serveru. **Tabulka živých zásob** uvádí, že zásoby se pořád mění. Počáteční tabulka se nezobrazuje s nulovými hodnotami změny.

1. Zavřete prohlížeč.

## <a name="enable-logging"></a>Povolte protokolování

Signál má vestavěnou funkci protokolování, kterou můžete na klientovi povolit, aby při řešení potíží mohl pomoci. V této části povolíte protokolování a uvidíte příklady, které ukazují, jak protokoly říkají, které z následujících signálů přenosových metod používá:

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket), které podporuje služba IIS 8 a aktuální prohlížeče.

* [Události odeslané serverem](http://en.wikipedia.org/wiki/Server-sent_events), které podporují jiné prohlížeče než Internet Explorer.

* [Trvale rámec](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), který podporuje Internet Explorer.

* [Dlouhé cyklické dotazování AJAX](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), podporované všemi prohlížeči

Pro jakékoli dané připojení vybírá signál nejlepší metodu přenosu, kterou podporuje server i klientská podpora.

1. Otevřete *StockTicker. js*.

1. Přidejte tento zvýrazněný řádek kódu, chcete-li povolit protokolování bezprostředně před kódem, který inicializuje připojení na konci souboru:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. Stisknutím klávesy **F5** spusťte projekt.

1. Otevřete okno vývojářské nástroje v prohlížeči a vyberte konzolu, abyste zobrazili protokoly. Možná budete muset aktualizovat stránku, aby se zobrazily protokoly signalizace vyjednávat přenosovou metodou pro nové připojení.

    * Pokud používáte Internet Explorer 10 v systému Windows 8 (IIS 8), je přenosová metoda **WebSockets**.

    * Pokud používáte Internet Explorer 10 v systému Windows 7 (IIS 7,5), je přenosová metoda **IFRAME**.

    * Pokud používáte Firefox 19 v systému Windows 8 (IIS 8), je přenosová metoda **WebSockets**.

        > [!TIP]
        > V prohlížeči Firefox nainstalujte doplněk Firebug a získejte okno konzoly.

    * Pokud používáte Firefox 19 v systému Windows 7 (IIS 7,5), přenosová metoda je události **odesílané serverem** .

## <a name="install-the-stockticker-sample"></a>Instalace ukázky StockTicker

[Microsoft. ASPNET. signaler. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) nainstaluje aplikaci StockTicker. Balíček NuGet zahrnuje více funkcí, než je zjednodušená verze, kterou jste vytvořili úplně od začátku. V této části kurzu nainstalujete balíček NuGet a zkontrolujete nové funkce a kód, který je implementuje.

> [!IMPORTANT]
> Pokud balíček nainstalujete bez provedení předchozích kroků tohoto kurzu, musíte do svého projektu přidat třídu pro spuštění OWIN. Tento krok popisuje tento soubor Readme. txt pro balíček NuGet.

### <a name="install-the-signalrsample-nuget-package"></a>Instalace nástroje Signal. Sample NuGet Package

1. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt a vyberte **Spravovat balíčky NuGet**.

1. Ve **Správci balíčků NuGet: Signal. StockTicker**, vyberte **Procházet**.

1. Ze **zdroje balíčku**vyberte možnost **NuGet.org**.

1. Do vyhledávacího pole zadejte *Signal. Sample* a vyberte **Microsoft. ASPNET. signaler. Sample** > **install**.

1. V **Průzkumník řešení**rozbalte složku *Signal. Sample* .

    Instalace nástroje Signal. vzorový balíček vytvořil složku a její obsah.

1. Ve složce *Signal. Sample* klikněte pravým tlačítkem na *StockTicker. html*a pak vyberte **nastavit jako úvodní stránku**.

    > [!NOTE]
    > Instalace nástroje Signal. vzorový balíček NuGet může změnit verzi jQuery, kterou máte ve složce *Scripts* . Nový soubor *StockTicker. html* , který balíček nainstaluje do nástroje *Signal. vzorová* složka bude synchronizována s verzí jQuery, kterou balíček nainstaluje, ale pokud chcete znovu spustit původní soubor *StockTicker. html* , bude pravděpodobně nutné nejprve aktualizovat odkaz jQuery ve značce Script.

### <a name="run-the-application"></a>Spuštění aplikace

 Tabulka, kterou jste viděli v první aplikaci, měla užitečné funkce. Celá burzovní aplikace na více datových cyklech zobrazuje nové funkce: vodorovné posuvné okno, které zobrazuje burzovní data a zásoby, které mění barvu při jejich zvyšování a poklesu.

1. Stisknutím klávesy **F5** spusťte aplikaci.

     Při prvním spuštění aplikace je "trh" "zavřený" a zobrazí se statická tabulka a okno se značkami, které se neposunují.

1. Vyberte **otevřít trh**.

    ![Snímek obrazovky živého ticku](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * Pole se seznamem **živých akcií** se začne posouvat vodorovně a server začne pravidelně vysílat změny cen akcií na náhodném základě.

    * Pokaždé, když se změní cena na zásobě, aplikace aktualizuje **tabulku Live Stock** a **živý**burzovní modul.

    * Když je cenová změna zásob kladná, aplikace zobrazí akcie se zeleným pozadím.

    * Když je změna záporná, aplikace zobrazí burzovní skladem s červeným pozadím.

1. Vyberte možnost **Zavřít trh**.

    * Zastaví se aktualizace tabulky.

    * Tato značka zastaví rolování.

1. Vyberte **obnovit**.

    * Všechna skladová data se resetují.

    * Aplikace obnoví počáteční stav předtím, než se změny cen spustí.

1. Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.

1. Stejná data se v každém prohlížeči zobrazují v současné době dynamicky.

1. Když vyberete kterýkoli z ovládacích prvků, všechny prohlížeče budou reagovat stejně jako ve stejnou dobu.

### <a name="live-stock-ticker-display"></a>Živý displej se zobrazením akcií

**Živý burzovní** displej je neuspořádaný seznam prvku `<div>` formátovaného na jeden řádek pomocí stylů CSS. Aplikace inicializuje a aktualizuje pro něj stejný způsob jako tabulka: nahrazením zástupných symbolů v řetězci šablony `<li>` a dynamickém přidáním `<li>` prvků do `<ul>` elementu. Aplikace zahrnuje posouvání pomocí funkce jQuery `animate` pro změnu levého okraje seznamu neuspořádaného v rámci `<div>`.

#### <a name="signalrsample-stocktickerhtml"></a>Signale. Sample StockTicker. html

Burzovní kód HTML s taktem:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>Signal. Sample StockTicker. CSS

Burzovní kód pro vystavení akcií:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>Signalizace. Ukázka signálu. StockTicker. js

Kód jQuery, který usnadňuje posunutí:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Další metody na serveru, který může klient volat

Pro přidání flexibility do aplikace jsou k dispozici další metody, které může aplikace volat.

#### <a name="signalrsample-stocktickerhubcs"></a>Signál. Sample StockTickerHub.cs

Třída `StockTickerHub` definuje čtyři další metody, které může klient volat:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

Aplikace volá `OpenMarket`, `CloseMarket`a `Reset` v reakci na tlačítka v horní části stránky. Ukazují vzor jednoho klienta, který aktivuje změnu stavu okamžitě šířenou pro všechny klienty. Každá z těchto metod volá metodu ve třídě `StockTicker`, která způsobuje změnu stavu trhu a pak vysílá nový stav.

#### <a name="signalrsample-stocktickercs"></a>Signál. Sample StockTicker.cs

Ve třídě `StockTicker` aplikace udržuje stav trhu s vlastností `MarketState`, která vrací `MarketState` hodnotu výčtu:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

Každá z metod, které mění stav trhu, je v bloku zámku, protože třída `StockTicker` musí být bezpečná pro přístup z více vláken:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

Chcete-li zajistit, aby byl tento kód bezpečný pro přístup z více vláken, `_marketState` pole, které vrátí vlastnost `MarketState` určenou `volatile`:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

Metody `BroadcastMarketStateChange` a `BroadcastMarketReset` jsou podobné metodě BroadcastStockPrice, kterou jste již viděli, s výjimkou volání různých metod definovaných v klientovi:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>Další funkce v klientovi, které může server volat

Funkce `updateStockPrice` nyní zpracovává tabulku i zobrazení značek a používá `jQuery.Color` k blikání červené a zelené barvy.

Nové funkce v nástroji *Signal. StockTicker. js* povolují a zakazují tlačítka na základě stavu trhu. Také zastavují nebo spouštějí automatické **posouvání akcií.** Vzhledem k tomu, že se do `ticker.client`přidávají mnoho funkcí, aplikace k jejich přidání používá [funkci jQuery Extended](http://api.jquery.com/jQuery.extend/) .

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Další nastavení klienta po navázání připojení

Poté, co klient připojení naváže, provede další práci:

* Zjistěte, jestli je trh otevřený nebo zavřený pro volání příslušné `marketOpened` nebo `marketClosed` funkce.

* Připojte volání metody serveru k tlačítkům.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

Metody serveru nejsou kabelové až do tlačítek, dokud aplikace nevytvoří připojení. To znamená, že kód nemůže volat metody serveru předtím, než budou k dispozici.

## <a name="additional-resources"></a>Další zdroje

V tomto kurzu jste se naučili, jak programovat aplikaci pro signalizaci, která vysílá zprávy ze serveru do všech připojených klientů. Nyní můžete zprávy pravidelně vysílat a reagovat na oznámení od libovolného klienta. Koncept instance s více vlákny můžete použít k údržbě stavu serveru ve scénářích hraní online her pro více hráčů. Příklad najdete v tématu [hry pro sestřelení na základě signalizace](https://github.com/NTaylorMullen/ShootR).

Kurzy, které ukazují scénáře komunikace peer-to-peer, najdete v tématu [Začínáme s nástrojem pro signalizaci](introduction-to-signalr.md) a [aktualizací v reálném čase pomocí nástroje signaler](tutorial-high-frequency-realtime-with-signalr.md).

Další informace o signalizaci naleznete v následujících zdrojích informací:

* [ASP.NET signál](../../index.md)
* [Projekt signálu](http://signalr.net/)
* [GitHub a ukázky signálů](https://github.com/SignalR/SignalR)
* [Wiki signálu](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Projekt se vytvořil.
> * Nastavení serverového kódu
> * Zkontrolovali jste kód serveru.
> * Nastavení kódu klienta
> * Prověření klientského kódu
> * Otestování aplikace
> * Povolené protokolování

V dalším článku se dozvíte, jak vytvořit webovou aplikaci v reálném čase, která používá signál ASP.NET 2.
> [!div class="nextstepaction"]
> [Vytvoření webové aplikace v reálném čase pomocí signalizace](real-time-web-applications-with-signalr.md)
