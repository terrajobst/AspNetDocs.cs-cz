---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 'Kurz: Vytvoření aplikace s vysokou frekvencí v reálném čase pomocí signalizace 2 | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která pomocí ASP.NET signalizace poskytuje funkce pro vysokou četnost zasílání zpráv.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600458"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a>Kurz: Vytvoření aplikace s vysokou frekvencí v reálném čase pomocí signálů 2

V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci, která používá signál ASP.NET 2 k poskytování funkcí vysoké frekvence zasílání zpráv. V takovém případě "vysokorychlostní zasílání zpráv" znamená, že server odesílá aktualizace za pevnou sazbu. Za sekundu vám pošleme až 10 zpráv.

Vytvořená aplikace zobrazí obrazec, který mohou uživatelé přetáhnout. Server aktualizuje pozici obrazce ve všech připojených prohlížečích tak, aby se shodovala s pozicí přetaženého obrazce pomocí časované aktualizace.

Koncepty představené v tomto kurzu obsahují aplikace v reálném čase a jiné aplikace simulace.

V tomto kurzu:

> [!div class="checklist"]
> * Nastavení projektu
> * Vytvoření základní aplikace
> * Mapování na centrum při spuštění aplikace
> * Přidání klienta
> * Spuštění aplikace
> * Přidat smyčku klienta
> * Přidat smyčku serveru
> * Přidat plynulou animaci

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Požadavky

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) s úlohou **vývoje ASP.NET a webu** .

## <a name="set-up-the-project"></a>Nastavení projektu

V této části vytvoříte projekt v aplikaci Visual Studio 2017.

V této části se dozvíte, jak pomocí sady Visual Studio 2017 vytvořit prázdnou webovou aplikaci v ASP.NET a přidat knihovny Signal a jQuery. UI.

1. V aplikaci Visual Studio vytvořte webovou aplikaci v ASP.NET.

    ![Vytvoření webu](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. V okně **Nová webová aplikace v ASP.NET – MoveShapeDemo** ponechte vybrané **prázdné** a vyberte **OK**.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.

1. V **příkaz Přidat novou položku-MoveShapeDemo**vyberte možnost **nainstalováno** ** > C# > ** webového ** > a** vyberte položku **centrum signalizace (v2)** .

1. Pojmenujte třídu *MoveShapeHub* a přidejte ji do projektu.

    Tento krok vytvoří soubor třídy *MoveShapeHub.cs* . Současně přidá sadu souborů skriptu a odkazy na sestavení, které podporují signalizaci do projektu.

1. Vyberte **nástroje** > **správce balíčků NuGet** > **konzole správce balíčků**.

1. V **konzole správce balíčků**spusťte tento příkaz:

    ```console
    Install-Package jQuery.UI.Combined
    ```

    Příkaz nainstaluje knihovnu uživatelského rozhraní jQuery. Použijete ho k animaci obrazce.

1. V **Průzkumník řešení**rozbalte uzel skripty.

    ![Odkazy knihovny skriptů](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    Knihovny skriptů pro jQuery, jQueryUI a Signal jsou viditelné v projektu.

## <a name="create-the-base-application"></a>Vytvoření základní aplikace

V této části vytvoříte aplikaci v prohlížeči. Aplikace během každé události přesunutí myši pošle umístění obrazce na server. Server všesměrově vysílá tyto informace všem ostatním připojeným klientům v reálném čase. Další informace o této aplikaci najdete v dalších částech.

1. Otevřete soubor *MoveShapeHub.cs* .

1. Nahraďte kód v souboru *MoveShapeHub.cs* tímto kódem:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. Uložte soubor.

Třída `MoveShapeHub` je implementací centra signalizace. Stejně jako v kurzu [Začínáme s nástrojem Signal](tutorial-getting-started-with-signalr.md) má centrum metodu, kterou klienti volají přímo. V tomto případě klient pošle objekt s novými souřadnicemi X a Y obrazce na server. Tyto souřadnice se dostanou do všech ostatních připojených klientů. Návěstí tento objekt automaticky serializovat pomocí formátu JSON.

Aplikace odešle objekt `ShapeModel` klientovi. Má členy pro uložení pozice obrazce. Verze objektu na serveru má také člena, aby mohla sledovat, která data klienta jsou ukládána. Tento objekt brání serveru v posílání dat klienta zpět do sebe samé. Tento člen používá atribut `JsonIgnore` k tomu, aby aplikace mohla v serializaci dat a jejich odeslání zpátky klientovi.

## <a name="map-to-the-hub-when-app-starts"></a>Mapování na centrum při spuštění aplikace

V dalším kroku nastavíte při spuštění aplikace mapování na centrum. V nástroji Signal 2 Přidání třídy OWIN Startup vytvoří mapování.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.

1. V **položce Přidat novou položku – MoveShapeDemo** vyberte **nainstalované** > **Visual C#**  > **Web** a pak vyberte **třídu pro spuštění Owin**.

1. Pojmenujte *spouštěcí* třídu a vyberte **OK**.

1. Nahraďte výchozí kód v souboru *Startup.cs* tímto kódem:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

Spouštěcí třída OWIN volá `MapSignalR`, když aplikace spustí metodu `Configuration`. Aplikace přidá třídu do procesu spouštění OWIN pomocí atributu `OwinStartup` Assembly.

## <a name="add-the-client"></a>Přidání klienta

Přidejte stránku HTML pro klienta.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **stránku HTML**.

1. Pojmenujte stránku **jako výchozí** a vyberte **OK**.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na *Default. html* a vyberte **nastavit jako úvodní stránku**.

1. Nahraďte výchozí kód ve *výchozím souboru. html* tímto kódem:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. V **Průzkumník řešení**rozbalte položku **skripty**.

    Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.

    > [!IMPORTANT]
    > Správce balíčků nainstaluje novější verzi skriptů nástroje Signaler.

1. Aktualizujte odkazy na skripty v bloku kódu tak, aby odpovídaly verzím souborů skriptu v projektu.

Tento kód HTML a JavaScriptu vytvoří červené `div` s názvem `shape`. Umožňuje chování obrazce při přetahování pomocí knihovny jQuery a používá událost `drag` k odeslání pozice obrazce na server.

## <a name="run-the-app"></a>Spuštění aplikace

Aplikaci můžete spustit tak, aby se'e svou práci. Když přetáhnete tvar kolem okna prohlížeče, obrazec se přesune i v jiných prohlížečích.

1. Na panelu nástrojů zapněte **ladění skriptů** a pak vyberte tlačítko Přehrát a spusťte aplikaci v režimu ladění.

    ![Snímek obrazovky uživatele, který zapíná režim ladění a vybere možnost Přehrát.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    Otevře se okno prohlížeče s červeným tvarem v pravém horním rohu.

1. Zkopírujte adresu URL stránky.

1. Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.

1. Přetáhněte tvar v jednom z oken prohlížeče. Následuje tvar v jiném okně prohlížeče.

Přestože aplikace funguje pomocí této metody, není doporučený programovací model. Počet zpráv, které se odesílají, nejsou horním limitem. V důsledku toho se klienti a Server budou zahlceni zprávami a snížení výkonu. Aplikace také zobrazuje na klientovi nesouvislou animaci. Tato Jerky animace se stane, protože tvar je okamžitě přesunut každou metodou. Je lepší, pokud se obrazec plynule přesune do každého nového umístění. V dalším kroku se dozvíte, jak tyto problémy vyřešit.

## <a name="add-the-client-loop"></a>Přidat smyčku klienta

Odeslání umístění obrazce při každé události přesunutí myši vytvoří zbytečný objem síťového provozu. Aplikace potřebuje omezit zprávy od klienta.

Pomocí funkce `setInterval` JavaScriptu můžete nastavit smyčku, která na server odesílá informace o nové pozici s pevnou sazbou. Tato smyčka představuje základní reprezentaci "smyčky hry". Tato funkce je opakovaně volána, která zařídí všechny funkce hry.

1. Nahraďte kód klienta ve *výchozím souboru. html* tímto kódem:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > Je nutné znovu nahradit odkazy na skript. Musí odpovídat verzím skriptů v projektu.

    Tento nový kód přidá funkci `updateServerModel`. Nazývá se pevná frekvence. Funkce odesílá data pozice na server vždy, když příznak `moved` označuje, že je k odeslání k dispozici nová data o poloze.

1. Kliknutím na tlačítko Přehrát spusťte aplikaci.

1. Zkopírujte adresu URL stránky.

1. Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.

1. Přetáhněte tvar v jednom z oken prohlížeče. Následuje tvar v jiném okně prohlížeče.

Vzhledem k tomu, že aplikace omezuje počet zpráv, které se odesílají na server, animace se v první době neprojeví jako hladká.

## <a name="add-the-server-loop"></a>Přidat smyčku serveru

V aktuální aplikaci se zprávy odesílané ze serveru do klienta dostanou tak často, jak jsou přijaty. Tento provoz v síti představuje podobný problém, jaký vidíte na klientovi.

Aplikace může posílat zprávy častěji, než je potřeba. V důsledku toho může dojít k zahlcení připojení. Tato část popisuje, jak aktualizovat server a přidat časovač, který omezuje rychlost odchozích zpráv.

1. Nahraďte obsah `MoveShapeHub.cs` tímto kódem:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. Kliknutím na tlačítko Přehrát spusťte aplikaci.

1. Zkopírujte adresu URL stránky.

1. Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.

1. Přetáhněte tvar v jednom z oken prohlížeče.

Tento kód rozbalí klienta, aby přidal třídu `Broadcaster`. Nová třída omezuje odchozí zprávy pomocí `Timer` třídy z rozhraní .NET Framework.

Je dobré vědět, že je samotný rozbočovač přechodný. Je vytvořen pokaždé, když je potřeba. Aplikace proto vytvoří `Broadcaster` jako typ singleton. Používá opožděnou inicializaci pro odložení `Broadcaster`ho vytváření, dokud není potřeba. To zaručuje, že aplikace před spuštěním časovače úplně vytvoří první instanci centra.

Volání funkce `UpdateShape` klientů je pak přesunuto mimo metodu `UpdateModel` centra. Už se nevolá hned, kdykoli aplikace obdrží příchozí zprávy. Místo toho aplikace odesílá zprávy klientům rychlostí 25 volání za sekundu. Proces je spravován pomocí časovače `_broadcastLoop` z `Broadcaster` třídy.

A konečně místo volání metody klienta z rozbočovače přímo, `Broadcaster` třídy musí získat odkaz na aktuálně fungující `_hubContext` centrum. Získá odkaz s `GlobalHost`.

## <a name="add-smooth-animation"></a>Přidat plynulou animaci

Aplikace je skoro dokončená, ale můžeme udělat ještě jedno zlepšení. Aplikace přesune obrazec na klientovi v reakci na zprávy serveru. Místo nastavování pozice obrazce k novému umístění, které je zadáno serverem, použijte funkci `animate` knihovny uživatelského rozhraní JQuery. Může obrazec plynule přemísťovat mezi aktuální a novou pozicí.

1. Aktualizujte metodu `updateShape` klienta ve výchozím souboru *. html* tak, aby vypadala jako zvýrazněný kód:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. Kliknutím na tlačítko Přehrát spusťte aplikaci.

1. Zkopírujte adresu URL stránky.

1. Otevřete jiný prohlížeč a vložte adresu URL do panelu Adresa.

1. Přetáhněte tvar v jednom z oken prohlížeče.

Pohyb tvaru v druhém okně se zobrazuje méně Jerky. Aplikace interpoluje svůj pohyb v čase, ale nenastavuje se jednou pro příchozí zprávu.

Tento kód přesune obrazec ze starého umístění do nového. Server dává pozici tvaru v průběhu intervalu animace. V tomto případě je to 100 milisekund. Aplikace vymaže všechny předchozí animace běžící na tvaru před zahájením nové animace.

## <a name="get-the-code"></a>Získat kód

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a>Další materiály a zdroje informací

Paradigmata komunikace, o které jste se dozvěděli, je užitečná při vývoji online her a dalších simulací, jako [je hra programu pro seznámení vytvořená pomocí nástroje Signal](https://shootr.azurewebsites.net/).

Další informace o signalizaci naleznete v následujících zdrojích informací:

* [Projekt signálu](http://signalr.net)

* [GitHub a ukázky signálů](https://github.com/SignalR/SignalR)

* [Wiki signálu](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Další kroky

V tomto kurzu:

> [!div class="checklist"]
> * Nastavení projektu
> * Vytvoření základní aplikace
> * Namapováno na centrum při spuštění aplikace
> * Přidání klienta
> * Aplikace byla spuštěna
> * Přidala se smyčka klienta.
> * Přidání smyčky serveru
> * Přidání plynulé animace

V dalším článku se dozvíte, jak vytvořit webovou aplikaci, která používá ASP.NET Signal 2 k poskytování funkcí všesměrového vysílání serveru.
> [!div class="nextstepaction"]
> [Signál 2 a všesměrové vysílání serveru](tutorial-server-broadcast-with-signalr.md)