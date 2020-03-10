---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 'Praktická cvičení: webové aplikace v reálném čase se signálem | Microsoft Docs'
author: bradygaster
description: Webové aplikace v reálném čase umožňují doručování obsahu na straně serveru do připojených klientů v reálném čase. Pro vývojáře v ASP.NET, ASP...
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537098"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a>Praktické cvičené: Webové aplikace v reálném čase s knihovnou SignalR

podle [týmu webového Campy](https://twitter.com/webcamps)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[Stáhnout web Campy Training Kit, říjen 2015 Release](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> Webové aplikace v reálném čase umožňují doručování obsahu na straně serveru do připojených klientů v reálném čase. Pro vývojáře v ASP.NET je **ASP.NET Signal** knihovny, která do aplikací přidávají webové funkce v reálném čase. Využívá několik přenosů a automaticky vybírá nejlepší dostupný přenos, který je dán nejlepší dostupností klienta a serveru. Využívá rozhraní **WebSocket**, rozhraní API HTML5, které umožňuje obousměrnou komunikaci mezi prohlížečem a serverem.
> 
> **Signal** také poskytuje jednoduché, vysoké rozhraní API pro server pro vzdálené RPC (volání funkcí jazyka JavaScript v prohlížečích klientských počítačů z kódu .NET na straně serveru) ve vaší aplikaci ASP.NET a také přidání užitečných zavěšení pro správu připojení, jako jsou události připojení/odpojení, seskupování připojení a autorizace.
> 
> **Signalizace** je abstrakcí přes některé z přenosů, které jsou potřeba k tomu, aby fungovaly v reálném čase mezi klientem a serverem. Připojení k **signalizaci** začíná jako http a pak se převýší na připojení protokolu **WebSocket** , pokud je k dispozici. **WebSocket** je ideální přenos pro **signál**, protože zajišťuje nejúčinnější využití paměti serveru, má nejnižší latenci a má nejvíce základní funkce (například plně duplexní komunikaci mezi klientem a serverem), ale má i nejpřísnější požadavky: **WebSocket** vyžaduje, aby server používal **Windows Server 2012** nebo **Windows 8**, společně s **.NET Framework 4,5**. Pokud tyto požadavky nejsou splněné, pokusí se **signál** použít jiné přenosy, aby provedl připojení (jako je *dlouhé cyklické dotazování AJAX*).
> 
> Rozhraní API pro **signalizaci** obsahuje dva modely pro komunikaci mezi klienty a servery: **trvalá připojení** a **rozbočovače**. **Připojení** představuje jednoduchý koncový bod pro odesílání, seskupené nebo všesměrové zprávy o jednom příjemci. **Rozbočovač** je více kanálů vysoké úrovně postavených na rozhraní API pro připojení, které umožňuje klientovi a serveru volat metody navzájem přímo.
> 
> ![Architektura signalizace](real-time-web-applications-with-signalr/_static/image1.png)
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, říjen 2015 verze, která je k dispozici na adrese [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b).  Upozorňujeme, že odkaz na instalační program na této stránce už nefunguje. místo toho použijte jeden z odkazů v části assets (prostředky).

<a id="Overview"></a>
## <a name="overview"></a>Přehled

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Odesílat oznámení ze serveru klientovi pomocí signalizace.
- Horizontální navýšení kapacity aplikace pro signalizaci pomocí **SQL Server**.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:

- [Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/) nebo více

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

Aby bylo možné spustit cvičení v této praktické laboratorní laboratoři, budete muset nejprve nastavit prostředí.

1. Otevřete okno Průzkumníka Windows a přejděte do **zdrojové** složky testovacího prostředí.
2. Klikněte pravým tlačítkem na **Setup. cmd** a vyberte **Spustit jako správce** a spusťte proces instalace, který bude konfigurovat vaše prostředí a nainstaluje fragmenty kódu sady Visual Studio pro toto testovací prostředí.
3. Pokud se zobrazí dialogové okno Řízení uživatelských účtů, potvrďte akci, abyste mohli pokračovat.

> [!NOTE]
> Před spuštěním instalačního programu se ujistěte, že jste kontrolovali všechny závislosti pro toto testovací prostředí.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Používání fragmentů kódu

V celém dokumentu testovacího prostředí budete vyzváni k vložení bloků kódu. Pro usnadnění práce je většina tohoto kódu k dispozici jako fragmenty Visual Studio Code, ke kterým můžete přistupovat z Visual Studio 2013, abyste se vyhnuli nutnosti ho přidat ručně.

> [!NOTE]
> Každé cvičení se doprovází od počátečního řešení ve složce **Begin** cvičení, které vám umožní sledovat jednotlivá cvičení nezávisle na ostatních. Všimněte si, že fragmenty kódu, které jsou přidány během cvičení, v těchto počátečních řešeních chybí a nemusí fungovat, dokud nedokončíte cvičení. Ve zdrojovém kódu cvičení také najdete **koncovou** složku obsahující řešení sady Visual Studio s kódem, který je výsledkem dokončení kroků v příslušném cvičení. Tato řešení můžete použít jako návod, pokud potřebujete další pomoc při práci s tímto praktickým cvičením.

---

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení zahrnují následující cvičení:

1. [Práce s daty v reálném čase pomocí signálu](#Exercise1)
2. [Horizontální navýšení kapacity pomocí SQL Server](#Exercise2)

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**

> [!NOTE]
> Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení. Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna. Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** . Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>Cvičení 1: práce s daty v reálném čase pomocí signálu

I když se chat často používá jako příklad, můžete s využitím webové funkce v reálném čase využít celou řadu dalších možností. Pokaždé, když uživatel aktualizuje webovou stránku, aby zobrazil nová data, nebo když stránka převezme dlouhé cyklické dotazování v AJAX pro načtení nových dat, můžete použít signál.

Signál podporuje funkci **nabízeného oznámení** nebo **vysílání** serveru; zpracovává správu připojení automaticky. V klasických připojeních HTTP pro komunikaci mezi klientem a serverem je připojení znovu navázáno pro každý požadavek, ale signál poskytuje trvalé připojení mezi klientem a serverem. V nástroji Signal kód serveru volá klientský kód v prohlížeči pomocí vzdáleného volání procedur (RPC) místo modelu žádosti-odpověď, který dnes ví.

V tomto cvičení nakonfigurujete aplikaci **informatik kvíz** na použití nástroje Signal k zobrazení řídicího panelu statistiky s aktualizovanými metrikami, aniž by bylo nutné aktualizovat celou stránku.

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>Úloha 1 – prozkoumání stránky statistiky informatik kvízu

V této úloze provedete aplikaci a ověříte, jak se zobrazí stránka Statistika a jak můžete zlepšit způsob, jakým se informace aktualizují.

1. Otevřete **Visual Studio Express 2013 pro web** a otevřete řešení **GeekQuiz. sln** nacházející se ve složce **Source\Ex1-WorkingWithRealTimeData\Begin** .
2. Stisknutím klávesy **F5** spusťte řešení. **Přihlašovací** stránka by se měla zobrazit v prohlížeči.

    ![Spuštění řešení](real-time-web-applications-with-signalr/_static/image2.png "Spuštění řešení")

    *Spuštění řešení*
3. Kliknutím na **Registrovat** v pravém horním rohu stránky vytvořte nového uživatele v aplikaci.

    ![Odkaz na registraci](real-time-web-applications-with-signalr/_static/image3.png "Odkaz na registraci")

    *Odkaz na registraci*
4. Na stránce **zaregistrovat** zadejte **uživatelské jméno** a **heslo**a potom klikněte na **zaregistrovat**.

    ![Registrace uživatele](real-time-web-applications-with-signalr/_static/image4.png "Registrace uživatele")

    *Registrace uživatele*
5. Aplikace registruje nový účet a uživatel se ověří a znovu se přesměruje na domovskou stránku zobrazující první otázku kvízu.
6. Otevřete stránku **Statistika** v novém okně a stránku **domovské** stránky a **statistiky** umístěte vedle sebe.

    ![Souběžná okna](real-time-web-applications-with-signalr/_static/image5.png "Vedle sebe – okna")

    *Souběžná okna*
7. Na **domovské** stránce odpovězte na otázku kliknutím na jednu z možností.

    ![Zodpovězení otázky](real-time-web-applications-with-signalr/_static/image6.png "Zodpovězení otázky")

    *Zodpovězení otázky*
8. Po kliknutí na jedno z tlačítek by se měla zobrazit odpověď.

    ![Otázka zodpovězená správně](real-time-web-applications-with-signalr/_static/image7.png "Otázka zodpovězená správně")

    *Správně zodpovězená otázka*
9. Všimněte si, že informace uvedené na stránce Statistika jsou zastaralé. Aktualizujte stránku, aby se zobrazily aktualizované výsledky.

    ![Stránka Statistika](real-time-web-applications-with-signalr/_static/image8.png "Stránka Statistika")

    *Stránka Statistika*
10. Vraťte se do sady Visual Studio a zastavte ladění.

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>Úkol 2 – Přidání signálu do informatik kvízu pro zobrazení online grafů

V této úloze přidáte do řešení signalizaci a odešlete aktualizace klientům automaticky, když se na server pošle nová odpověď.

1. V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.
2. V okně **konzoly Správce balíčků** spusťte následující příkaz:

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![Instalace balíčku signálu](real-time-web-applications-with-signalr/_static/image9.png "Instalace balíčku signálu")

    *Instalace balíčku signálu*

   > [!NOTE]
   > Při instalaci balíčků NuGet nástroje **signaler** verze 2.0.2 ze značky nové aplikace MVC 5 budete muset před instalací signálu ručně aktualizovat balíčky **Owin** na verzi 2.0.1 (nebo vyšší). Chcete-li to provést, můžete spustit následující skript v **konzole správce balíčků**:
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > V budoucí verzi nástroje Signal se závislosti OWIN automaticky aktualizují.
3. V **Průzkumník řešení**rozbalte složku **Scripts** a Všimněte si, že do řešení byly přidány soubory nástroje signaler *js* .

    ![Reference k JavaScriptu pro signály](real-time-web-applications-with-signalr/_static/image10.png "Reference k JavaScriptu pro signály")

    *Reference k JavaScriptu pro signály*
4. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **GeekQuiz** , vyberte **Přidat** | **novou složku**a pojmenujte IT **centra**.
5. Klikněte pravým tlačítkem na složku **Centers** a vyberte **Přidat | Nová položka**.

    ![Přidat novou položku](real-time-web-applications-with-signalr/_static/image11.png "Přidat novou položku")

    *Přidat novou položku*
6. V dialogovém okně **Přidat novou položku** vyberte  **C# vizuál | Web | Uzel signál** v levém podokně, v prostředním podokně vyberte **třídy centra signalizace (v2)** , pojmenujte soubor **StatisticsHub.cs** a klikněte na tlačítko **Přidat**.

    ![Dialogové okno Přidat novou položku](real-time-web-applications-with-signalr/_static/image12.png "Dialogové okno Přidat novou položku")

    *Dialogové okno Přidat novou položku*
7. Nahraďte kód ve třídě **StatisticsHub** následujícím kódem.

    (Fragment kódu – *RealTimeSignalR-EX1-StatisticsHubClass*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. Otevřete **Startup.cs** a na konci **konfigurační** metody přidejte následující řádek.

    (Fragment kódu – *RealTimeSignalR-EX1-MapSignalR*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. Otevřete stránku **StatisticsService.cs** ve složce **služby** a přidejte následující direktivy using.

    (Fragment kódu – *RealTimeSignalR-EX1-UsingDirectives*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. Chcete-li informovat připojené klienty o aktualizacích, napřed načtěte **kontextový** objekt pro aktuální připojení. Objekt **centra** obsahuje metody pro posílání zpráv do jednoho klienta nebo všesměrového vysílání do všech připojených klientů. Přidejte následující metodu do třídy **StatisticsService** , abyste mohli vysílat statistická data.

    (Fragment kódu – *RealTimeSignalR-EX1-NotifyUpdatesMethod*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > Ve výše uvedeném kódu použijte libovolný název metody pro volání funkce na klientovi (tj.: *updateStatistics*). Název metody, který zadáte, je interpretován jako dynamický objekt, což znamená, že pro něj není k dispozici žádná technologie IntelliSense nebo kompilace. Výraz je vyhodnocen v době běhu. Když se spustí volání metody, Signal pošle klientovi název metody a hodnoty parametru. Pokud má klient metodu, která odpovídá názvu, je tato metoda volána a hodnoty parametrů jsou předány. Pokud není v klientovi nalezena žádná vyhovující metoda, není vyvolána žádná chyba. Další informace najdete v příručce k [rozhraní API pro centra ASP.NET Signal](../guide-to-the-api/hubs-api-guide-server.md).
11. Otevřete stránku **TriviaController.cs** uvnitř složky **Controllers** a přidejte následující direktivy using.

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. Do metody **post** akce přidejte následující zvýrazněný kód.

    (Fragment kódu – *RealTimeSignalR-EX1-NotifyUpdatesCall*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. Otevřete stránku **Statistika. cshtml** v **zobrazeních | Domovská** složka Vyhledejte oddíl **skripty** a na začátku oddílu přidejte odkazy na tento skript.

    (Fragment kódu – *RealTimeSignalR-EX1-SignalRScriptReferences*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > Když přidáte do projektu sady Visual Studio signál a další knihovny skriptu, správce balíčků může nainstalovat verzi souboru skriptu nástroje Signal, který je novější než verze uvedená v tomto tématu. Ujistěte se, že odkaz na skript v kódu odpovídá verzi knihovny skriptů nainstalované ve vašem projektu.
14. Přidejte následující zvýrazněný kód, který připojí klienta k centru signalizace a aktualizuje data statistiky při přijetí nové zprávy z centra.

    (Fragment kódu – *RealTimeSignalR-EX1-SignalRClientCode*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    V tomto kódu vytváříte proxy server rozbočovače a zaregistrujete obslužnou rutinu události, která naslouchá zprávám odesílaným serverem. V takovém případě budete naslouchat zprávám odeslaným pomocí metody *updateStatistics* .

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>Úloha 3 – spuštění řešení

V této úloze spustíte řešení a ověříte, že statistické zobrazení je po zodpovězení nové otázky aktualizováno automaticky pomocí signálu.

1. Stisknutím klávesy **F5** spusťte řešení.

    > [!NOTE]
    > Pokud jste se ještě přihlásili k aplikaci, přihlaste se pomocí uživatele, kterého jste vytvořili v úloze 1.
2. Otevřete stránku **Statistika** v novém okně a stránku **domovské** stránky a **statistiky** umístěte vedle sebe jako v úloze 1.
3. Na **domovské** stránce odpovězte na otázku kliknutím na jednu z možností.

    ![Zodpovězení jiné otázky](real-time-web-applications-with-signalr/_static/image13.png "Zodpovězení jiné otázky")

    *Zodpovězení jiné otázky*
4. Po kliknutí na jedno z tlačítek by se měla zobrazit odpověď. Všimněte si, že informace o statistice na stránce se aktualizují automaticky po zodpovězení otázky s aktualizovanými informacemi, aniž by bylo nutné aktualizovat celou stránku.

    ![Stránka Statistika aktualizována po odpovědi](real-time-web-applications-with-signalr/_static/image14.png "Stránka Statistika aktualizována po odpovědi")

    *Stránka Statistika aktualizována po odpovědi*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>Cvičení 2: horizontální navýšení kapacity pomocí SQL Server

Při škálování webové aplikace můžete obecně *zvolit možnosti* horizontálního navýšení kapacity a horizontálního *navýšení* kapacity. *Horizontální navýšení kapacity* znamená použití většího serveru s více prostředky (CPU, RAM atd.) během *horizontálního* navýšení kapacity znamená přidání dalších serverů pro zpracování zatížení. K tomuto problému dochází v případě, že klienti mohou směrovat na různé servery. Klient, který je připojen k jednomu serveru, nebude přijímat zprávy odesílané z jiného serveru.

Tyto problémy můžete vyřešit pomocí komponenty označované jako *backplane*pro přeposílání zpráv mezi servery. Když je povolený plán, každá instance aplikace odesílá zprávy do plánu pro replánování a znovu je přenáší do ostatních instancí aplikace.

V současné době existují tři typy řídicích plánů pro signalizaci:

- **Azure Service Bus Windows**. Service Bus je infrastruktura zasílání zpráv, která umožňuje komponentám posílání volně vázaných zpráv.
- **SQL Server**. SQL Server pro naplánování zapisuje zprávy do tabulek SQL. Plán pro použití Service Broker pro efektivní zasílání zpráv používá. Ale funguje i v případě, že Service Broker není povolená.
- **Redis**. Redis je úložiště hodnot klíč-hodnota v paměti. Redis podporuje vzor publikování/odběru ("pub/sub") pro posílání zpráv.

Každá zpráva se odesílá prostřednictvím sběrnice zpráv. Sběrnice zpráv implementuje rozhraní [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) , které poskytuje abstrakci pro publikování/odběr. Plán funguje tak, že nahradí výchozí **IMessageBus** sběrnicí, která je navržena pro tento plán.

Každá instance serveru se připojuje k vašemu schématu prostřednictvím sběrnice. Když se pošle zpráva, přejde do plánu pro replánování a znovu ho pošle na každý server. Když server obdrží zprávu od replánování, uloží zprávu do místní mezipaměti. Server pak doručuje zprávy klientům z místní mezipaměti.

Další informace o tom, jak vyplánování signalizace funguje, najdete v tomto [článku](../performance/scaleout-in-signalr.md).

> [!NOTE]
> V některých případech se může stát, že by se plán znovu stal kritickým bodem. Tady jsou některé typické scénáře signalizace:
> 
> - [Všesměrové vysílání serveru](tutorial-server-broadcast-with-signalr.md) (např. burzovní modul): v tomto scénáři dobře funguje plán, protože server řídí rychlost odesílání zpráv.
> - [Klient-klient](tutorial-getting-started-with-signalr.md) (např. chat): v tomto scénáři může být plán opětovného použití kritický, pokud se počet zpráv škáluje s počtem klientů. To znamená, že pokud se rychlost zpráv postupně zvětšuje při připojování více klientů.
> - [Vysoká frekvence v reálném](tutorial-high-frequency-realtime-with-signalr.md) čase (například hry v reálném čase): pro tento scénář se nedoporučuje použití schématu pro replánování.

V tomto cvičení použijete **SQL Server** k distribuci zpráv v rámci aplikace **informatik kvíz** . Tyto úlohy spustíte na jednom testovacím počítači, abyste se dozvěděli, jak nastavit konfiguraci, ale pokud chcete mít úplný efekt, budete muset aplikaci signalizace nasadit na dva nebo víc serverů. Je také nutné nainstalovat SQL Server na jednom ze serverů nebo na samostatném vyhrazeném serveru.

![Horizontální navýšení kapacity pomocí SQL Serverho diagramu](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>Úkol 1 – Princip scénáře

V této úloze spustíte 2 instance **informatik kvízu** s simulací více instancí služby IIS na místním počítači. V tomto scénáři při zodpovězení minihry dotazů na jednu aplikaci se aktualizace nebude informovat na stránce Statistika druhé instance. Tato simulace se podobá prostředí, ve kterém je vaše aplikace nasazená na více instancích a používá nástroj pro vyrovnávání zatížení ke komunikaci s nimi.

1. Otevřete řešení **Begin. sln** nacházející se ve složce **source/EX2-ScalingOutWithSQLServer/Begin** . Po načtení si všimněte **Průzkumník serveru** , že řešení má dva projekty se stejnými strukturami, ale s různými názvy. Tím dojde ke simulaci spuštění dvou instancí stejné aplikace na místním počítači.

    ![Zahájit řešení simulující 2 instance informatik kvízu](real-time-web-applications-with-signalr/_static/image16.png "Zahájit řešení simulující 2 instance informatik kvízu")

    *Zahájit řešení simulující 2 instance informatik kvízu*
2. Otevřete stránku vlastnosti řešení tak, že kliknete pravým tlačítkem na uzel řešení a vyberete **vlastnosti**. V části **spouštěný projekt**vyberte **více projektů po spuštění** a změňte hodnotu **Akce** pro oba projekty na *Start*.

    ![Spuštění více projektů](real-time-web-applications-with-signalr/_static/image17.png "Spuštění více projektů")

    *Spuštění více projektů*
3. Stisknutím klávesy **F5** spusťte řešení. Aplikace spustí dvě instance **informatik kvízu** na různých portech a simuluje několik instancí stejné aplikace. Připněte jeden z prohlížečů vlevo a druhý na pravé straně obrazovky. Přihlaste se pomocí svých přihlašovacích údajů nebo si zaregistrujte nového uživatele. Po přihlášení ponechte stránku minihry na levé straně a v prohlížeči napravo přejít na stránku **Statistika** .

    ![Informatik kvíz vedle sebe](real-time-web-applications-with-signalr/_static/image18.png)

    *Informatik kvíz vedle sebe*

    ![Informatik kvíz v různých portech](real-time-web-applications-with-signalr/_static/image19.png)

    *Informatik kvíz v různých portech*
4. Začněte s zodpovězením otázek v levém prohlížeči a všimnete si, že se stránka **Statistika** v pravém prohlížeči neaktualizuje. Důvodem je skutečnost, že nástroj **Signal** používá místní mezipaměť k distribuci zpráv napříč klienty a tento scénář simuluje více instancí, proto není mezi nimi sdílená mezipaměť. Můžete ověřit, že **signál** funguje, otestováním stejných kroků, ale pomocí jedné aplikace. V následujících úlohách nakonfigurujete plán pro replikaci zpráv mezi instancemi.
5. Vraťte se do sady Visual Studio a zastavte ladění.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>Úloha 2 – vytvoření SQL Serverho plánu

V této úloze vytvoříte databázi, která bude sloužit jako replánace pro aplikaci **informatik kvíz** . K procházení serveru a inicializaci databáze použijete **Průzkumník objektů systému SQL Server** . Navíc povolíte **Service Broker**.

1. V **aplikaci Visual Studio**otevřete nabídku **zobrazení** a vyberte možnost **Průzkumník objektů systému SQL Server**.
2. Připojte se k instanci LocalDB kliknutím pravým tlačítkem myši na uzel **SQL Server** a vybráním možnosti **Přidat SQL Server...** .

    ![Přidání instance SQL Server](real-time-web-applications-with-signalr/_static/image20.png "Přidání instance SQL Server")

    *Přidání instance SQL Server do Průzkumník objektů systému SQL Server*
3. Nastavte **název serveru** na *(LocalDB) \v11.0* a v režimu ověřování nechte **ověřování systému Windows** . Pokračujte kliknutím na **Připojit**.

    ![Připojování k LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Připojování k LocalDB")

    *Připojování k LocalDB*
4. Teď, když jste připojeni k instanci služby LocalDB, budete muset vytvořit databázi, která bude představovat SQL Server pro naplánování signálu. Provedete to tak, že kliknete pravým tlačítkem na uzel **databáze** a vyberete **Přidat novou databázi**.

    ![Přidání nové databáze](real-time-web-applications-with-signalr/_static/image22.png "Přidání nové databáze")

    *Přidání nové databáze*
5. Nastavte název databáze na *signaler* a kliknutím na **OK** ji vytvořte.

    ![Vytváření databáze signálů](real-time-web-applications-with-signalr/_static/image23.png "Vytváření databáze signálů")

    *Vytváření databáze signálů*

    > [!NOTE]
    > Můžete zvolit libovolný název databáze.
6. Pokud chcete dostávat aktualizace efektivněji z plánu, doporučujeme pro databázi povolit Service Broker. Service Broker poskytuje nativní podporu pro zasílání zpráv a zařazování do fronty v SQL Server. I bez Service Broker funguje i bez plánu. Otevřete nový dotaz tak, že kliknete pravým tlačítkem na databázi a vyberete **Nový dotaz**.

    ![Otevření nového dotazu](real-time-web-applications-with-signalr/_static/image24.png "Otevření nového dotazu")

    *Otevření nového dotazu*
7. Chcete-li ověřit, zda je povolena Service Broker, je nutné zadat dotaz na sloupec **is\_Broker\_Enabled** v zobrazení katalogu **Sys. databases** . V okně naposledy otevřeného dotazu spusťte následující skript.

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![Dotazování na stav Service Broker](real-time-web-applications-with-signalr/_static/image25.png "Dotazování na stav Service Broker")

    *Dotazování na stav Service Broker*
8. Pokud je hodnota sloupce **\_broker\_Enabled** ve vaší databázi &quot;0&quot;, povolte ji pomocí následujícího příkazu. Nahraďte **&lt;&gt;databáze** názvem, který jste nastavili při vytváření databáze (např.: signaler).

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![Povolení Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Povolení Service Broker")

    *Povolení Service Broker*

    > [!NOTE]
    > Pokud se zobrazí dotaz zablokování, ujistěte se, že neexistují žádné aplikace připojené k databázi.

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>Úloha 3 – konfigurace aplikace Signal

V této úloze nakonfigurujete **informatik kvíz** pro připojení k SQL Serverho opětovného plánování. Nejdřív přidáte balíček NuGet **Signal. SqlServer** a nakonfigurujete připojovací řetězec k databázi vašeho plánu.

1. Otevřete **konzolu Správce balíčků** z **nástrojů** > **Správce balíčků NuGet**. Ujistěte se, že je v rozevíracím seznamu **výchozí projekt** vybraná možnost projekt **GeekQuiz** . Zadáním následujícího příkazu nainstalujte balíček NuGet **Microsoft. ASPNET. signaler. SqlServer** .

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. Opakujte předchozí krok, ale tentokrát pro projekt **GeekQuiz2**.
3. Chcete-li nakonfigurovat SQL Server opětovného plánování, otevřete soubor **Startup.cs** projektu **GeekQuiz** a přidejte následující kód do metody **Configure** . Nahraďte **&lt;&gt;databáze** názvem vaší databáze, který jste použili při vytváření plánu SQL Server. Tento krok opakujte pro projekt **GeekQuiz2** .

    (Fragment kódu – *RealTimeSignalR-EX2-StartupConfiguration*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. Teď, když jsou oba projekty nakonfigurované pro použití SQL Serverho plánu, stiskněte klávesu **F5** , aby se spouštěla současně.
5. Znovu spustí **Visual Studio** dvě instance **informatik kvízu** na různých portech. Připněte jeden z prohlížečů vlevo a druhý na pravé straně obrazovky a přihlaste se pomocí svých přihlašovacích údajů. Ponechte stránku minihry na levé straně a pak přejít na **Statistika** pagein pravém prohlížeči.
6. Zahajte odpovědi na dotazy v levém prohlížeči. Tentokrát je stránka **Statistika** aktualizována v rámci plánu. Přepínání mezi aplikacemi (**Statistika** je nyní na levé straně a **minihry** je na pravé straně) a opakovaný test ověří, zda funguje pro obě instance. Replánování slouží jako *sdílená mezipaměť* zpráv pro každý připojený server a každý server bude ukládat zprávy do své vlastní místní mezipaměti pro distribuci do připojených klientů.
7. Vraťte se do sady Visual Studio a zastavte ladění.
8. Součást SQL Serverho naplánování automaticky generuje potřebné tabulky v zadané databázi. Na panelu **Průzkumník objektů systému SQL Server** otevřete databázi, kterou jste vytvořili pro replánování (např.: signaler), a rozbalte její tabulky. Měli byste vidět následující tabulky:

    ![Vygenerované tabulky pro naplánování](real-time-web-applications-with-signalr/_static/image27.png)

    *Vygenerované tabulky pro naplánování*
9. Klikněte pravým tlačítkem myši na položku **signaler. messages\_0** a vyberte **Zobrazit data**.

    ![Zobrazit tabulku zpráv pro naplánování signálu](real-time-web-applications-with-signalr/_static/image28.png)

    *Zobrazit tabulku zpráv pro naplánování signálu*
10. Při zodpovězení otázek minihry můžete zobrazit různé zprávy odesílané do **centra** . Při opětovném naplánování tyto zprávy distribuuje do jakékoli připojené instance.

    ![Tabulka zpráv pro naplánování](real-time-web-applications-with-signalr/_static/image29.png)

    *Tabulka zpráv pro naplánování*

---

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

V tomto praktickém cvičení jste se seznámili s postupem přidání **signálu** do aplikace a odesílání oznámení ze serveru do připojených klientů pomocí **Center**. Kromě toho jste zjistili, jak horizontální navýšení kapacity aplikace při nasazení aplikace v několika instancích služby IIS pomocí komponenty pro *replánování* .
