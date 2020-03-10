---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 'Kurz: vysílání serveru pomocí ASP.NET signalizace 1. x | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET signál k poskytování funkcí všesměrového vysílání serveru. Všesměrové vysílání serveru znamená, že se jedná o obecnou...
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579406"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>Kurz: Serverové vysílání s knihovnou ASP.NET SignalR 1.x

autorem [Fletcher](https://github.com/pfletcher), který [Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET signál k poskytování funkcí všesměrového vysílání serveru. Všesměrové vysílání serveru znamená, že se komunikace odesílaná klientům spouští serverem. Tento scénář vyžaduje jiný programovací přístup než scénáře peer-to-peer, jako jsou například aplikace chatu, ve kterých je komunikace odesílaná klientům iniciována jedním nebo více klienty.
> 
> Aplikace, kterou vytvoříte v tomto kurzu, simuluje burzovní, což je typický scénář pro funkce všesměrového vysílání serveru.
> 
> Komentáře k tomuto kurzu jsou Vítá vás. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com).

## <a name="overview"></a>Přehled

Balíček NuGet [Microsoft. ASPNET. signale. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet nainstaluje ukázku simulované burzovní aplikace v projektu Visual studia. V první části tohoto kurzu vytvoříte zjednodušenou verzi této aplikace od začátku. Ve zbývající části kurzu nainstalujete balíček NuGet a zkontrolujete další funkce a kód, které vytvoří.

Burzovní aplikace se nachází jako zástupce druhu aplikace v reálném čase, ve kterém chcete pravidelně vysílat oznámení ze serveru do všech připojených klientů.

Aplikace, kterou sestavíte v první části tohoto kurzu, zobrazí mřížku s uloženými daty.

![Počáteční verze StockTicker](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

Server pravidelně aktualizuje skladové ceny a nahraje aktualizace všem připojeným klientům. V prohlížeči se v reakci na oznámení ze serveru dynamicky mění čísla a symboly ve sloupcích **Změna** a **%** . Pokud otevřete další prohlížeče na stejné adrese URL, všechny zobrazí stejná data a stejné změny dat současně.

Tento kurz obsahuje následující oddíly:

- [Požadavky](#prerequisites)
- [Vytvořit projekt](#createproject)
- [Přidání balíčků NuGet pro signál](#nugetpackages)
- [Nastavení serverového kódu](#server)
- [Nastavení kódu klienta](#client)
- [Testování aplikace](#test)
- [Povolení protokolování](#enablelogging)
- [Instalace a kontrola úplné ukázky StockTicker](#fullsample)
- [Další kroky](#nextsteps)

> [!NOTE]
> Pokud nechcete pracovat s postupem sestavování aplikace, můžete do nového **prázdného projektu webové aplikace ASP.NET** nainstalovat signál. ukázkový balíček a pomocí těchto kroků získat vysvětlení kódu. První část kurzu se zabývá podmnožinou signálu. vzorový kód a druhá část vysvětluje klíčové funkce dalších funkcí v nástroji Signal. Sample Package.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Předpoklady

Než začnete, ujistěte se, že máte v počítači nainstalovanou aplikaci Visual Studio 2012 nebo 2010 SP1. Pokud nemáte Visual Studio, přečtěte si článek [ASP.NET downloads](https://www.asp.net/downloads) , kde získáte bezplatnou aplikaci visual Studio 2012 Express for Web.

Pokud máte Visual Studio 2010, ujistěte se, že je nainstalováno [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) .

<a id="createproject"></a>

## <a name="create-the-project"></a>Vytvoření projektu

1. V nabídce **soubor** klikněte na příkaz **Nový projekt**.
2. V dialogovém okně **Nový projekt** rozbalte **C#** v části **šablony** a vyberte možnost **Web**.
3. Vyberte šablonu **ASP.NET prázdné webové aplikace** , pojmenujte ho *signaler. StockTicker*a klikněte na **OK**.

    ![Dialogové okno Nový projekt](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>Přidání balíčků NuGet pro signál

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>Přidání balíčků Signal a JQuery NuGet

Pomocí instalace balíčku NuGet můžete do projektu přidat funkci signalizace.

1. Klikněte na **nástroje | Správce balíčků NuGet | Konzola správce balíčků**.
2. Ve Správci balíčků zadejte následující příkaz.

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    Balíček signalizace nainstaluje několik dalších balíčků NuGet jako závislosti. Po dokončení instalace máte všechny součásti serveru a klienta, které jsou nutné k použití signalizace v aplikaci ASP.NET.

<a id="server"></a>

## <a name="set-up-the-server-code"></a>Nastavení serverového kódu

V této části nastavíte kód, který běží na serveru.

### <a name="create-the-stock-class"></a>Vytvoření třídy akcie

Začnete vytvořením třídy burzovního modelu, kterou použijete k ukládání a přenosu informací o zásobách.

1. Vytvořte nový soubor třídy ve složce projektu a pojmenujte jej *Stock.cs*a potom kód šablony nahraďte následujícím kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    Tyto dvě vlastnosti, které nastavíte při vytváření akcií, jsou symbolem (například MSFT pro Microsoft) a cenou. Ostatní vlastnosti závisí na tom, jak a kdy jste nastavili cenu. Při prvním nastavení ceny se hodnota rozšíří na DayOpen. Po dalším nastavování ceny se hodnoty vlastností Change a PercentChange vypočítávají na základě rozdílu mezi cenou a DayOpen.

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>Vytvoření tříd StockTicker a StockTickerHub

K řízení interakce mezi klientem a serverem použijete rozhraní API centra signalizace. Třída StockTickerHub, která je odvozena z třídy centra signálů, bude zpracovávat přijímání připojení a volání metod od klientů. Je také potřeba zachovat skladová data a spustit objekt časovače, aby pravidelně spouštěl cenové aktualizace, nezávisle na připojeních klienta. Tyto funkce nemůžete umístit do třídy centra, protože instance centra jsou přechodné. Instance třídy centra se vytvoří pro každou operaci na rozbočovači, například připojení a volání z klienta na server. Proto mechanismus, který udržuje skladová data, aktualizuje ceny a vysílá, je nutné, aby se aktualizace ceny spouštěly v samostatné třídě, kterou pojmenovat StockTicker.

![Všesměrové vysílání z StockTicker](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

Chcete, aby na serveru běžela jenom jedna instance třídy StockTicker, takže budete muset nastavit odkaz z každé instance StockTickerHub na instanci StockTicker typu singleton. Třída StockTicker musí umožňovat všesměrové vysílání klientům, protože má uložená data a aktivuje aktualizace, ale StockTicker není třída centra. Třída StockTicker proto musí získat odkaz na objekt kontextu připojení centra signalizace. Pak může pomocí objektu kontextu připojení vysílače vysílat klientům.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a klikněte na příkaz **Přidat novou položku**.
2. Pokud máte Visual Studio 2012 s [aktualizací ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=279941), klikněte v části  **C# vizuál** na **Web** a vyberte šablonu položky **Třída rozbočovače signálu** . V opačném případě vyberte šablonu **třídy** .
3. Pojmenujte novou třídu *StockTickerHub.cs*a pak klikněte na **Přidat**.

    ![Přidat StockTickerHub.cs](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. Nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    Třída [centra](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) se používá k definování metod, které mohou klienti volat na serveru. Definujete jednu metodu: `GetAllStocks()`. Když se klient poprvé připojí k serveru, zavolá tuto metodu, aby získal seznam všech populací s jejich aktuálními cenami. Metoda může provádět synchronní a vracet `IEnumerable<Stock>`, protože vrací data z paměti. Pokud metoda musela získat data pomocí něčeho, co by vyžadovala čekání, například vyhledávání databáze nebo volání webové služby, zadejte `Task<IEnumerable<Stock>>` jako návratovou hodnotu pro povolení asynchronního zpracování. Další informace najdete v tématu [Průvodce rozhraním API pro centra ASP.NET signálu – Server – kdy se má provést asynchronní spuštění](index.md).

    Atribut HubName určuje, jak bude v klientovi odkazováno na centrum JavaScript Code. Výchozí název na klientovi Pokud nepoužíváte tento atribut, je ve stylu CamelCase verze použita názvu třídy, což v tomto případě by bylo stockTickerHub.

    Jak uvidíte později při vytváření třídy StockTicker, vytvoří se instance singleton této třídy ve vlastnosti statické instance. Tato instance typu Singleton StockTicker zůstává v paměti bez ohledu na to, kolik klientů se připojuje nebo odpojuje a že tato instance je to, co metoda GetAllStocks používá k vrácení aktuálních informací o zásobách.
5. Vytvořte nový soubor třídy ve složce projektu a pojmenujte jej *StockTicker.cs*a potom kód šablony nahraďte následujícím kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    Vzhledem k tomu, že více vláken bude používat stejnou instanci StockTicker kódu, musí být třída StockTicker threadsafe.

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>Ukládání instance singleton do statického pole

    Kód inicializuje pole instance statického \_, které vrátí vlastnost instance s instancí třídy, a toto je jediná instance třídy, kterou lze vytvořit, protože konstruktor je označen jako Private. [Opožděná inicializace](https://msdn.microsoft.com/library/dd997286.aspx) se používá pro pole \_instance, nikoli z důvodů výkonu, ale pro zajištění, že je vytvoření instance threadsafe.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    Pokaždé, když se klient připojí k serveru, nová instance třídy StockTickerHub spuštěné v samostatném vlákně získá instanci StockTicker singleton z statické vlastnosti StockTicker. instance, jak jste viděli dříve ve třídě StockTickerHub.

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Ukládání uložených dat v ConcurrentDictionary

    Konstruktor inicializuje kolekci \_ch populací s některými vzorovými daty a GetAllStocks vrátí akcie. Jak jste viděli dříve, tato kolekce populací se zase vrací pomocí StockTickerHub. GetAllStocks, což je metoda serveru ve třídě centra, kterou můžou klienti volat.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    Kolekce akcie je definována jako [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) typ pro bezpečnost vlákna. Jako alternativu můžete použít objekt [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) a explicitně zamknout slovník při provádění změn v něm.

    Pro tuto ukázkovou aplikaci je možné uložit data aplikace do paměti a ztratit data, když je instance StockTicker vyřazena. V reálné aplikaci byste pracovali s back-end datovým úložištěm, jako je databáze.

    ### <a name="periodically-updating-stock-prices"></a>Pravidelná aktualizace cen akcií

    Konstruktor spustí objekt Timer, který pravidelně volá metody, které aktualizují skladové ceny náhodným základem.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices je volána časovačem, který předává hodnotu null v parametru State. Před aktualizací cen se na \_objekt updateStockPricesLock zavede zámek. Kód zkontroluje, jestli už jiný podproces aktualizuje ceny, a pak na každou populaci v seznamu zavolá TryUpdateStockPrice. Metoda TryUpdateStockPrice rozhoduje o tom, jestli se má změnit cena akcií, a kolik se má změnit. Pokud dojde ke změně ceny akcií, BroadcastStockPrice se zavolá, aby se změnila cena za zásobu u všech připojených klientů.

    Příznak \_updatingStockPrices je označený jako [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) , aby se zajistilo, že přístup k němu je threadsafe.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    V reálné aplikaci metoda TryUpdateStockPrice zavolá webovou službu, aby vyhledala cenu. v tomto kódu používá generátor náhodných čísel k náhodnému provedení změn.

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>Získání kontextu signálu, aby třída StockTicker mohla vysílat klientům

    Vzhledem k tomu, že změny ceny pocházejí zde v objektu StockTicker, jedná se o objekt, který musí volat metodu updateStockPrice na všech připojených klientech. Ve třídě centra máte rozhraní API pro volání metod klienta, ale StockTicker není odvozeno od třídy hub a nemá odkaz na žádný objekt hub. Aby bylo proto možné vysílat klientům připojeným, třída StockTicker musí získat kontextovou instanci signálu pro třídu StockTickerHub a použít ji k volání metod v klientech.

    Kód získá odkaz na kontext signalizace při vytvoření instance třídy singleton, předá tento odkaz na konstruktor a konstruktor ho vloží do vlastnosti klienti.

    Existují dva důvody, proč chcete kontext získat pouze jednou: získání kontextu je náročná operace a jeho získání je zajištěno, že se zachová zamýšlené pořadí zpráv odesílaných klientům.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    Získání vlastnosti klientů kontextu a jeho vložení do vlastnosti StockTickerClient umožňuje napsat kód pro volání klientských metod, které vypadají stejně jako ve třídě centra. Například pro všesměrové vysílání pro všechny klienty můžete napsat clients. All. updateStockPrice (Stock).

    Metoda updateStockPrice, kterou voláte v BroadcastStockPrice, ještě neexistuje. později ji přidáte při psaní kódu, který běží na klientovi. Sem můžete odkazovat na updateStockPrice, protože klienti. All jsou dynamické, což znamená, že se výraz vyhodnotí za běhu. Když se spustí toto volání metody, odesílatel pošle do klienta název metody a hodnotu parametru. Pokud má klient metodu s názvem updateStockPrice, bude tato metoda volána a hodnota parametru bude předána.

    Klienti. All znamená odeslání všem klientům. Signalizace nabízí další možnosti určení klientů nebo skupin klientů, které se mají odeslat. Další informace najdete v tématu [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>Registrace trasy signalizace

Server musí znát, která adresa URL má zachytit a směrovat na signál. K tomu je třeba přidat kód do souboru *Global. asax* .

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a potom klikněte na tlačítko **Přidat novou položku**.
2. Vyberte šablonu položky **globální třídy aplikace** a klikněte na tlačítko **Přidat**.

    ![Add global.asax](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. Přidejte registrační kód trasy signalizace do aplikace\_spustit metodu:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    Ve výchozím nastavení je základní adresa URL pro všechny přenosy signálu "/SignalR" a "/SignalR/Hubs" se používá k načtení dynamicky generovaného souboru JavaScriptu, který definuje proxy pro všechna centra ve vaší aplikaci. Metoda MapHubs zahrnuje přetížení, která umožňují zadat jinou základní adresu URL a určité možnosti signalizace v instanci třídy [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) .
4. Do horní části souboru přidejte příkaz using:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. Uložte a zavřete soubor *Global. asax* a sestavte projekt.

Nyní jste dokončili nastavení kódu serveru. V další části nastavíte klienta.

<a id="client"></a>

## <a name="set-up-the-client-code"></a>Nastavení kódu klienta

1. Vytvořte nový soubor HTML ve složce projektu a pojmenujte jej *StockTicker. html*.
2. Nahraďte kód šablony následujícím kódem:

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    HTML vytvoří tabulku s 5 sloupci, řádkem záhlaví a datovým řádkem s jedinou buňkou, která zahrnuje všechny 5 sloupců. Řádek data zobrazí "načítání..." a zobrazí se pouze při spuštění aplikace. JavaScriptový kód odstraní tento řádek a přidá ho do svých řádků s uloženými daty načtenými ze serveru.

    Značky skriptu určují soubor skriptu jQuery, základní soubor skriptu signálu, soubor skriptu proxy signalizace a soubor skriptu StockTicker, který vytvoříte později. Soubor skriptu proxy signálů, který určuje adresu URL "/SignalR/Hubs", je dynamicky generován a definuje metody proxy pro metody ve třídě centra, v tomto případě pro StockTickerHub. GetAllStocks. Pokud budete chtít, můžete tento soubor JavaScriptu vygenerovat ručně pomocí [nástrojů pro signalizaci](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) a zakázat dynamické vytváření souborů ve volání metody MapHubs.
3. > [!IMPORTANT]
   > Ujistěte se, že odkazy na soubory JavaScriptu v souboru *StockTicker. html* jsou správné. To znamená, že verze jQuery ve značce Script (1.8.2 v příkladu) je stejná jako verze jQuery ve složce Scripts vašeho projektu a ujistěte se, že verze signalizace ve značce skriptu je stejná jako verze signalizace *ve složce* *skriptů* vašeho projektu. V případě potřeby změňte názvy souborů ve značkách skriptu.
4. V **Průzkumník řešení**klikněte pravým tlačítkem na *StockTicker. html*a pak klikněte na **nastavit jako úvodní stránku**.
5. Vytvořte nový soubor JavaScriptu ve složce projektu a pojmenujte ho *StockTicker. js*.
6. Nahraďte kód šablony následujícím kódem:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $. připojení odkazuje na proxy signálů. Kód získá odkaz na proxy třídu pro třídu StockTickerHub a umístí ji do proměnné Tick. Název proxy je název, který byl nastaven atributem [HubName]:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    Po definování všech proměnných a funkcí inicializuje poslední řádek kódu v souboru připojení k signalizaci voláním funkce pro spuštění signálu. Funkce Start se provádí asynchronně a vrací [odložený objekt jQuery](http://api.jquery.com/category/deferred-object/), což znamená, že můžete zavolat funkci Hotovo a zadat funkci, která bude volána po dokončení asynchronní operace.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    Funkce Init volá funkci getAllStocks na serveru a používá informace, které server vrátí k aktualizaci skladové tabulky. Všimněte si, že ve výchozím nastavení je v klientovi nutné použít ve stylu CamelCase velká a malá písmena, ale název metody je Pascal-použita na serveru. Pravidlo ve stylu CamelCase-velká písmena se vztahuje pouze na metody, nikoli na objekty. Například odkazujete na akcie. Symbol a burzovní. Price, not Stock. symbol nebo Stock. Price.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    Pokud jste chtěli použít na klientovi velká písmena Pascal, nebo pokud jste chtěli použít zcela jiný název metody, mohli byste metodu hub pomocí atributu HubMethodName vytvořit stejným způsobem jako samotnou třídu centra s atributem HubName.

    V metodě Init je pro každý uložený objekt přijatý ze serveru vytvořen kód HTML pro řádek tabulky voláním formatStock pro formátování vlastností uloženého objektu a následným voláním supplant (která je definována v horní části *StockTicker. js*) k nahrazení zástupných symbolů v proměnné rowTemplate s hodnotami uložených vlastností objektu. Výsledný kód HTML se pak připojí k uložené tabulce.

    Zavoláte init tím, že ho předáte do jako funkci zpětného volání, která se spustí po dokončení asynchronní funkce spuštění. Pokud jste jako příkaz init jako samostatného JavaScriptu použili po volání metody Start, funkce by nefungovala, protože by se spouštěla okamžitě bez čekání na dokončení funkce Start pro dokončení navázání připojení. V takovém případě se funkce init pokusí zavolat funkci getAllStocks před navázáním připojení k serveru.

    Když server změní cenu akcií, zavolá updateStockPrice na připojené klienty. Funkce je přidána do vlastnosti klienta proxy serveru stockTicker, aby byla k dispozici pro volání ze serveru.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    Funkce updateStockPrice formátuje burzovní objekt přijatý ze serveru do řádku tabulky stejným způsobem jako ve funkci init. Místo připojení řádku k tabulce ale nalezne aktuální řádek v tabulce a nahradí ho novým řádkem.

<a id="test"></a>

## <a name="test-the-application"></a>Testování aplikace

1. Stisknutím klávesy F5 spusťte aplikaci v režimu ladění.

    V tabulce po prvním zobrazení se zobrazí "načítání...". řádek a po krátkém zpoždění se zobrazí počáteční skladová data a pak se ceny akcií začnou měnit.

    ![Načítá](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![Počáteční skladová tabulka](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![Skladová tabulka, která přijímá změny ze serveru](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. Zkopírujte adresu URL z panelu Adresa prohlížeče a vložte ji do jednoho nebo více nových oken prohlížeče.

    Počáteční zobrazovací displej je stejný jako první prohlížeč a změny probíhají současně.
3. Zavřete všechny prohlížeče a otevřete nový prohlížeč a pak přejít na stejnou adresu URL.

    Objekt typu Singleton StockTicker pokračuje v běhu na serveru, takže zobrazená tabulka v zásobách ukazuje, že zásoby se nadále mění. (Počáteční tabulka se nezobrazuje s nulovými hodnotami změny.)
4. Zavřete prohlížeč.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Povolte protokolování

Signál má vestavěnou funkci protokolování, kterou můžete na klientovi povolit, aby při řešení potíží mohl pomoci. V této části povolíte protokolování a uvidíte příklady, které ukazují, jak protokoly říkají, které z následujících signálů přenosových metod používá:

- [WebSockets](http://en.wikipedia.org/wiki/WebSocket), které podporuje služba IIS 8 a aktuální prohlížeče.
- [Události odeslané serverem](http://en.wikipedia.org/wiki/Server-sent_events), které podporují jiné prohlížeče než Internet Explorer.
- [Trvale rámec](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), který podporuje Internet Explorer.
- [Dlouhé cyklické dotazování AJAX](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), podporované všemi prohlížeči

Pro jakékoli dané připojení vybírá signál nejlepší metodu přenosu, kterou podporuje server i klientská podpora.

1. Otevřete *StockTicker. js* a přidejte řádek kódu, který povolí protokolování hned před kódem, který inicializuje připojení na konci souboru:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. Stisknutím klávesy F5 spusťte projekt.
3. Otevřete okno vývojářské nástroje v prohlížeči a vyberte konzolu, abyste zobrazili protokoly. Možná budete muset aktualizovat stránku, aby se zobrazily protokoly signalizace vyjednávat přenosovou metodou pro nové připojení.

    Pokud používáte Internet Explorer 10 v systému Windows 8 (IIS 8), je přenosová metoda WebSockets.

    ![Konzola IE 10 IIS 8](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    Pokud používáte Internet Explorer 10 v systému Windows 7 (IIS 7,5), je přenosová metoda IFRAME.

    ![Konzola IE 10, IIS 7,5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    V prohlížeči Firefox nainstalujte doplněk Firebug a získejte okno konzoly. Pokud používáte Firefox 19 v systému Windows 8 (IIS 8), je přenosová metoda WebSockets.

    ![Firefox 19 WebSockets služby IIS 8](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    Pokud používáte Firefox 19 v systému Windows 7 (IIS 7,5), přenosová metoda je události odesílané serverem.

    ![Konzola Firefox 19 IIS 7,5](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>Instalace a kontrola úplné ukázky StockTicker

Aplikace StockTicker, která je nainstalovaná balíčkem [Microsoft. ASPNET. signaler. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet, zahrnuje více funkcí, než je zjednodušená verze, kterou jste právě vytvořili úplně od začátku. V této části kurzu nainstalujete balíček NuGet a zkontrolujete nové funkce a kód, který je implementuje.

### <a name="install-the-signalrsample-nuget-package"></a>Instalace nástroje Signal. Sample NuGet Package

1. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt a pak klikněte na **Spravovat balíčky NuGet**.
2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **online**, do pole **Hledat online** zadejte *Signal. Sample* a pak klikněte na **nainstalovat** v nástroji **Signal. Sample** Package.

    ![Nainstalovat signál. ukázkový balíček](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. V souboru *Global. asax* přidejte komentář k části Route. Routes. MapHubs (); řádek, který jste přidali dříve v aplikaci\_spustit metodu.

    Kód v souboru *Global. asax* již není potřeba, protože signál. ukázkový balíček registruje trasu signálů do souboru *App\_Start/RegisterHubs. cs* :

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    Třída webactivator, na kterou je odkazováno atributem Assembly, je obsažena v balíčku WebActivatorEx NuGet, který je nainstalován jako závislost v balíčku nástroje Signal. Sample.
4. V **Průzkumník řešení**rozbalte složku *Signal. Sample* , která byla vytvořena instalací nástroje Signal. Sample Package.
5. Ve složce *Signal. Sample* klikněte pravým tlačítkem na *StockTicker. html*a pak klikněte na **nastavit jako úvodní stránku**.

    > [!NOTE]
    > Instalace nástroje Signal. vzorový balíček NuGet může změnit verzi jQuery, kterou máte ve složce *Scripts* . Nový soubor *StockTicker. html* , který balíček nainstaluje do nástroje *Signal. vzorová* složka bude synchronizována s verzí jQuery, kterou balíček nainstaluje, ale pokud chcete znovu spustit původní soubor *StockTicker. html* , bude pravděpodobně nutné nejprve aktualizovat odkaz jQuery ve značce Script.

### <a name="run-the-application"></a>Spuštění aplikace

1. Stisknutím klávesy F5 spusťte aplikaci.

    Kromě mřížky, kterou jste viděli dříve, zobrazuje celá burzovní aplikace v pravém okně, ve kterém se zobrazují stejná burzovní data. Při prvním spuštění aplikace je "trh" "zavřený" a zobrazí se statická mřížka a okno se značkami, které se neposunují.

    ![Spuštění obrazovky StockTicker](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    Po kliknutí na **otevřít na trhu**se pole se seznamem **živých zásob** začne posouvat vodorovně a server začne pravidelně vysílat změny cen akcií náhodně. Pokaždé, když se změní cena za zásobu, aktualizují se i živá **Skladová tabulka** a pole se seznamem **živých akcií** . Pokud je změna cen akcií kladná, zobrazí se akcie se zeleným pozadím a pokud je změna záporná, zobrazí se na skladě červené pozadí.

    ![Aplikace StockTicker, otevřený trh](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    Tlačítko **Zavřít na trhu** zastaví změny a zastaví rolování a tlačítko **reset** obnoví všechna skladovaná data do počátečního stavu před zahájením změn cen. Pokud otevřete více oken prohlížeče a přejdete na stejnou adresu URL, zobrazí se stejná data v každém prohlížeči v současné době dynamicky aktualizována. Po kliknutí na jedno z těchto tlačítek všechny prohlížeče reagují stejným způsobem současně.

### <a name="live-stock-ticker-display"></a>Živý displej se zobrazením akcií

**Živý burzovní** displej je neuspořádaný seznam v elementu div, který je formátovaný na jeden řádek pomocí stylů CSS. Tento ovládací prvek se inicializuje a aktualizuje stejným způsobem jako tabulka: nahrazením zástupných symbolů v &lt;li&gt; řetězce šablony a dynamickém přidáním &lt;li&gt; prvků do prvku &lt;ul&gt;. Posouvání se provádí pomocí funkce jQuery animace, která v rámci div mění okraj vlevo od neuspořádaného seznamu.

Burzovní modul HTML s taktem:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

Základní funkce pro vystavování akcií:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

Kód jQuery, který usnadňuje posunutí:

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Další metody na serveru, který může klient volat

Třída StockTickerHub definuje čtyři další metody, které může klient volat:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

OpenMarket, CloseMarket a Reset jsou volány v reakci na tlačítka v horní části stránky. Ukazují vzor jednoho klienta, který aktivuje změnu stavu, která je okamžitě šířena všem klientům. Každá z těchto metod volá metodu ve třídě StockTicker, která ovlivňuje změnu stavu trhu a pak vysílá nový stav.

Ve třídě StockTicker je stav trhu uchováván pomocí vlastnosti MarketState, která vrací hodnotu výčtu MarketState:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

Každá z metod, které mění stav trhu, je v bloku zámku, protože třída StockTicker musí být threadsafe:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

Chcete-li zajistit, aby byl tento kód threadsafe, pole \_marketState, které vrací vlastnost MarketState, je označeno jako volatile,

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

Metody BroadcastMarketStateChange a BroadcastMarketReset jsou podobné metodě BroadcastStockPrice, kterou jste již viděli, s výjimkou volání různých metod definovaných v klientovi:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>Další funkce v klientovi, které může server volat

Funkce updateStockPrice nyní zpracovává mřížku i zobrazení značek a používá jQuery. Color k blikání červených a zelených barev.

Nové funkce v nástroji *Signal. StockTicker. js* povolují a zakazují tlačítka na základě stavu na trhu a zastavují nebo spouštějí horizontální posouvání okna se značkami. Vzhledem k tomu, že se přidávají více funkcí do Tick. Client, je k jejich přidání použita [funkce jQuery Extended](http://api.jquery.com/jQuery.extend/) .

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Další nastavení klienta po navázání připojení

Poté, co klient připojení naváže, provede další práci: zjistit, jestli je trh otevřený nebo zavřený, aby mohl volat příslušnou funkci marketOpened nebo marketClosed, a připojit volání metody serveru k tlačítkům.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

Metody serveru nejsou kabelové až po navázání spojení, takže se kód nemůže pokusit volat metody serveru předtím, než budou k dispozici.

<a id="nextsteps"></a>

## <a name="next-steps"></a>Další kroky

V tomto kurzu jste se naučili, jak programovat aplikaci pro signalizaci, která vysílá zprávy ze serveru do všech připojených klientů, a to v pravidelných intervalech a jako reakci na oznámení od libovolného klienta. Vzor použití vícehodnotové instance s více vlákny k údržbě stavu serveru lze také použít ve scénářích hraní online her pro více hráčů. Příklad najdete v tématu [hry pro sestřelení, která je založená na nástroji Signal](https://github.com/NTaylorMullen/ShootR).

Kurzy, které ukazují scénáře komunikace peer-to-peer, najdete v tématu [Začínáme s nástrojem pro signalizaci](index.md) a [aktualizací v reálném čase pomocí nástroje signaler](index.md).

Další informace o pokročilých konceptech vývoje signálů najdete v následujících lokalitách, které jsou ve zdrojovém kódu a prostředcích signalizace:

- [ASP.NET signál](https://asp.net/signalr/)
- [Projekt signálu](http://signalr.net/)
- [GitHub a ukázky signálů](https://github.com/SignalR/SignalR)
- [Wiki signálu](https://github.com/SignalR/SignalR/wiki)
