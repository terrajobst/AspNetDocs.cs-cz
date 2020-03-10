---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: Vysoká frekvence v reálném čase pomocí návěstí 1. x | Microsoft Docs
author: bradygaster
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která pomocí ASP.NET signalizace poskytuje funkce pro vysokou četnost zasílání zpráv. Zasílání zpráv s vysokou frekvencí v...
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623499"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a>Vysokofrekvenční reálný čas s knihovnou SignalR 1.x

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která pomocí ASP.NET signalizace poskytuje funkce pro vysokou četnost zasílání zpráv. Vysoká frekvence zasílání zpráv v tomto případě znamená aktualizace, které se odesílají s pevnou sazbou. v případě této aplikace až 10 zpráv za sekundu.
> 
> Aplikace, kterou vytvoříte v tomto kurzu, zobrazí obrazec, který mohou uživatelé přetáhnout. Pozice obrazce ve všech ostatních připojených prohlížečích se pak aktualizuje tak, aby odpovídala pozici přetaženého obrazce pomocí časované aktualizace.
> 
> Koncepty představené v tomto kurzu obsahují aplikace v reálném čase a jiné aplikace simulace.
> 
> Komentáře k tomuto kurzu jsou Vítá vás. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com).

## <a name="overview"></a>Přehled

Tento kurz ukazuje, jak vytvořit aplikaci, která sdílí stav objektu s ostatními prohlížeči v reálném čase. Aplikace, kterou vytvoříme, se nazývá MoveShape. Na stránce MoveShape se zobrazí element DIV HTML, který uživatel může přetáhnout; Když uživatel přetáhne div, jeho nová poloha se pošle na server, který pak všem ostatním připojeným klientům sdělí, aby aktualizoval pozici obrazce na shodu.

![Okno aplikace](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

Aplikace vytvořená v tomto kurzu je založená na ukázce podle Damian Edwards. Video obsahující tuto ukázku lze zobrazit [zde](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).

V tomto kurzu začneme demonstrující, jak odesílat zprávy signálu z každé události, která aktivuje se při přetažení obrazce. Každý připojený klient pak aktualizuje pozici místní verze tvaru pokaždé, když se přijme zpráva.

I když aplikace bude fungovat pomocí této metody, nejedná se o doporučený programovací model, protože by nedocházelo k hornímu limitu počtu zpráv, které se odesílají, takže klienti a servery by mohli být zahlceni se zprávami a výkonem by se snížila hodnota . Zobrazená animace na straně klienta by byla také oddělená, protože by byl tvar okamžitě přesunutý podle jednotlivých metod, nikoli bez plynulého přesunu na každé nové místo. V pozdějších částech tohoto kurzu se dozvíte, jak vytvořit funkci časovače, která omezuje maximální rychlost, kterou odesílají zprávy klient nebo server, a způsob plynulého přesunutí obrazce mezi umístěními. Konečnou verzi aplikace vytvořenou v tomto kurzu lze stáhnout z [Galerie kódu](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).

Tento kurz obsahuje následující oddíly:

- [Požadavky](#prerequisites)
- [Vytvořit projekt](#createtheproject)
- [Přidání nástroje Signal ASP.NET a JQuery. UI balíčky NuGet](#nugetpackages)
- [Vytvoření základní aplikace](#baseapp)
- [Přidat smyčku klienta](#clientloop)
- [Přidat smyčku serveru](#serverloop)
- [Přidat plynulou animaci na klienta](#animation)
- [Další kroky](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Předpoklady

Tento kurz vyžaduje Visual Studio 2012 nebo Visual Studio 2010. Pokud se používá Visual Studio 2010, bude projekt používat .NET Framework 4 místo .NET Framework 4,5.

Pokud používáte Visual Studio 2012, doporučujeme nainstalovat [aktualizaci ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650). Tato aktualizace obsahuje nové funkce, jako jsou například vylepšení publikování, nové funkce a nové šablony.

Pokud máte Visual Studio 2010, ujistěte se, že je nainstalováno [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) .

<a id="createtheproject"></a>

## <a name="create-the-project"></a>Vytvoření projektu

V této části vytvoříme projekt v aplikaci Visual Studio.

1. V nabídce **soubor** klikněte na příkaz **Nový projekt**.
2. V dialogovém okně **Nový projekt** rozbalte **C#** v části **šablony** a vyberte možnost **Web**.
3. Vyberte šablonu **ASP.NET prázdné webové aplikace** , pojmenujte projekt *MoveShapeDemo*a klikněte na **OK**.

    ![Vytvoření nového projektu](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a>Přidání balíčků nástroje Signal a JQuery. UI NuGet

Pomocí instalace balíčku NuGet můžete do projektu přidat funkci signalizace. V tomto kurzu se taky použije balíček JQuery. UI, který umožňuje přetáhnout a animovat tvar.

1. Klikněte na **nástroje | Správce balíčků NuGet | Konzola správce balíčků**.
2. Ve Správci balíčků zadejte následující příkaz.

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    Balíček signalizace nainstaluje několik dalších balíčků NuGet jako závislosti. Po dokončení instalace máte všechny součásti serveru a klienta, které jsou nutné k použití signalizace v aplikaci ASP.NET.
3. Zadejte následující příkaz do konzoly Správce balíčků a nainstalujte balíčky JQuery a JQuery. UI.

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>Vytvoření základní aplikace

V této části vytvoříme prohlížečovou aplikaci, která během každé události přesunutí myši pošle umístění obrazce na server. Server pak tyto informace všesměrově vysílá do všech ostatních připojených klientů, když se obdrží. Tuto aplikaci rozšíříme v dalších oddílech.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat**, **Třída.** ... Pojmenujte třídu **MoveShapeHub** a klikněte na **Přidat**.
2. Nahraďte kód v nové třídě **MoveShapeHub** následujícím kódem.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    Výše uvedená třída `MoveShapeHub` je implementací centra signalizace. Stejně jako v kurzu [Začínáme s nástrojem Signal](index.md) má centrum metodu, kterou klienti budou volat přímo. V takovém případě klient pošle objekt obsahující nové souřadnice X a Y obrazce na server, který pak bude šířen do všech ostatních připojených klientů. Signál bude tento objekt automaticky serializovat pomocí formátu JSON.

    Objekt, který bude odeslán do klienta (`ShapeModel`) obsahuje členy pro uložení pozice tvaru. Verze objektu na serveru také obsahuje člena, který sleduje, která data klienta jsou ukládána, takže daný klient nebude odesílat vlastní data. Tento člen používá atribut `JsonIgnore` pro zachování jeho serializace a odeslání klientovi.
3. V dalším kroku nastavíme při spuštění aplikace rozbočovač. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a pak klikněte na **Přidat | Globální třída aplikace** Přijměte výchozí název *globální* a klikněte na tlačítko **OK**.

    ![Přidat globální třídu aplikace](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. Po poskytnuté příkazy **using** ve třídě Global.asax.cs přidejte následující příkaz `using`.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. Do metody `Application_Start` globální třídy přidejte následující řádek kódu k registraci výchozí trasy pro signál.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    Váš soubor Global. asax by měl vypadat takto:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. V dalším kroku přidáme klienta. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a pak klikněte na **Přidat | Nová položka**. V dialogovém okně **Přidat novou položku** vyberte **stránku HTML**. Dejte stránce vhodný název (například **Default. html**) a klikněte na **Přidat**.
7. V **Průzkumník řešení**klikněte pravým tlačítkem na právě vytvořenou stránku a pak klikněte na **nastavit jako úvodní stránku**.
8. Nahraďte výchozí kód na stránce HTML následujícím fragmentem kódu.

    > [!NOTE]
    > Ověřte, že níže uvedené odkazy na skript se shodují s balíčky přidanými do projektu ve složce Scripts. V aplikaci Visual Studio 2010 se verze JQuery a Signal přidaná do projektu nemusí shodovat s čísly verze uvedenými níže.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    Výše uvedený kód HTML a JavaScript vytvoří červený div s názvem tvar, umožňuje chování obrazce pomocí knihovny jQuery a používá událost `drag` obrazce k odeslání pozice obrazce na server.
9. Spusťte aplikaci stisknutím klávesy F5. Zkopírujte adresu URL stránky a vložte ji do druhého okna prohlížeče. Přetáhněte tvar v jednom z oken prohlížeče; tvar v jiném okně prohlížeče by se měl přesunout.

    ![Okno aplikace](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>Přidat smyčku klienta

Vzhledem k tomu, že při odeslání umístění obrazce při každé události přesunutí myši dojde k vytvoření zbytečných síťových přenosů, musí být zprávy z klienta omezeny. Pomocí funkce JavaScript `setInterval` nastavíme smyčku, která pošle nové informace o poloze na server s pevnou sazbou. Tato smyčka je velmi základní reprezentace "Game Loop", opakovaně nazývaná funkce, která zařídí všechny funkce hry nebo jiné simulace.

1. Aktualizujte kód klienta na stránce HTML tak, aby odpovídal následujícímu fragmentu kódu.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    Výše uvedená aktualizace přidá funkci `updateServerModel`, která se volá s pevnou frekvencí. Tato funkce odesílá data pozice na server vždy, když příznak `moved` označuje, že je k odeslání k dispozici nová data o poloze.
2. Spusťte aplikaci stisknutím klávesy F5. Zkopírujte adresu URL stránky a vložte ji do druhého okna prohlížeče. Přetáhněte tvar v jednom z oken prohlížeče; tvar v jiném okně prohlížeče by se měl přesunout. Vzhledem k tomu, že počet zpráv, které se odesílají na server, bude omezený, animace nebude zobrazená jako hladká jako v předchozí části.

    ![Okno aplikace](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>Přidat smyčku serveru

V aktuální aplikaci se zprávy odesílané ze serveru do klienta dostanou tak často, jak jsou přijímány. To představuje podobný problém, jak byl vidět na klientovi. zprávy je možné odeslat častěji, než je potřeba, a připojení se může v důsledku toho dezahlceno. Tato část popisuje, jak aktualizovat server pro implementaci časovače, který omezuje rychlost odchozích zpráv.

1. Obsah `MoveShapeHub.cs` nahraďte následujícím fragmentem kódu.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    Výše uvedený kód rozbalí klienta, aby přidal třídu `Broadcaster`, která omezuje odchozí zprávy pomocí `Timer` třídy z rozhraní .NET Framework.

    Vzhledem k tomu, že je samotné centrum přechodný (je vytvořeno pokaždé, když je potřeba), vytvoří se `Broadcaster` jako singleton. Opožděná inicializace (představená v rozhraní .NET 4) se používá k odložení jeho vytvoření až do chvíle, kdy je potřeba, aby první instance centra byla kompletně vytvořena před spuštěním časovače.

    Volání funkce `UpdateShape` klientů se pak přesune mimo `UpdateModel` metodu rozbočovače, aby se už nevolala okamžitě při přijetí příchozích zpráv. Místo toho budou zprávy klientům odesílány rychlostí 25 volání za sekundu, které jsou spravovány časovačem `_broadcastLoop` v rámci `Broadcaster` třídy.

    Namísto toho, místo volání metody klienta z centra přímo, musí `Broadcaster` Třída získat odkaz na aktuálně používané centrum (`_hubContext`) pomocí `GlobalHost`.
2. Spusťte aplikaci stisknutím klávesy F5. Zkopírujte adresu URL stránky a vložte ji do druhého okna prohlížeče. Přetáhněte tvar v jednom z oken prohlížeče; tvar v jiném okně prohlížeče by se měl přesunout. V prohlížeči nebude viditelný rozdíl v předchozí části, ale počet zpráv, které se odesílají do klienta, bude omezený.

    ![Okno aplikace](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>Přidat plynulou animaci na klienta

Aplikace je skoro dokončená, ale během přesunu na zprávy serveru můžeme udělat ještě lepší vylepšení při pohybu obrazce v klientovi. Namísto nastavení pozice obrazce na nové umístění, které je zadáno serverem, použijeme funkci `animate` knihovny uživatelského rozhraní JQuery k plynulému přesunutí obrazce mezi aktuální a novou pozicí.

1. Aktualizujte metodu `updateShape` klienta tak, aby vypadala jako zvýrazněný kód:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    Výše uvedený kód přesune tvar ze starého umístění na nový, který je dán serverem, v průběhu intervalu animace (v tomto případě 100 milisekund). Všechny předchozí animace spuštěné na tomto tvaru jsou před zahájením nové animace vymazány.
2. Spusťte aplikaci stisknutím klávesy F5. Zkopírujte adresu URL stránky a vložte ji do druhého okna prohlížeče. Přetáhněte tvar v jednom z oken prohlížeče; tvar v jiném okně prohlížeče by se měl přesunout. Pohyb obrazce v druhém okně by měl být menší než Jerky, protože jeho pohyb se interpoluje v čase, ale nenastavuje se jednou pro příchozí zprávu.

    ![Okno aplikace](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>Další kroky

V tomto kurzu jste se naučili, jak programovat aplikaci pro signalizaci, která odesílá vysokorychlostní zprávy mezi klienty a servery. Toto paradigma komunikace je užitečné při vývoji online her a dalších simulací, jako [je například hra pro sestřelení vytvořená pomocí nástroje Signal](http://shootr.signalr.net).

Kompletní aplikaci vytvořenou v tomto kurzu lze stáhnout z [Galerie kódu](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).

Chcete-li získat další informace o konceptech vývoje signálu, navštivte následující weby a vyhledejte zdrojový kód a prostředky signalizace:

- [Projekt signálu](http://signalr.net)
- [GitHub a ukázky signálů](https://github.com/SignalR/SignalR)
- [Wiki signálu](https://github.com/SignalR/SignalR/wiki)
