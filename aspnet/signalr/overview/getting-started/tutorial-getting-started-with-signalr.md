---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 'Kurz: chat v reálném čase s nástrojem Signal 2 | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se naučíte používat funkci SignalR k vytvoření aplikace pro chatování v reálném čase. Přidáte signál do prázdné webové aplikace v ASP.NET.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536979"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>Kurz: chat v reálném čase s nástrojem Signal 2

V tomto kurzu se dozvíte, jak pomocí signalizace vytvořit aplikaci Chat v reálném čase. Přidáte signál do prázdné webové aplikace v ASP.NET a vytvoříte stránku HTML pro odesílání a zobrazování zpráv.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Nastavení projektu
> * Spuštění ukázky
> * Kontrola kódu

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Předpoklady

* Sada [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) se sadou funkcí **Vývoj pro ASP.NET a web**.

## <a name="set-up-the-project"></a>Nastavení projektu

V této části se dozvíte, jak použít Visual Studio 2017 a Signal 2 k vytvoření prázdné webové aplikace v ASP.NET, přidání signálu a vytvoření aplikace chatu.

1. V aplikaci Visual Studio vytvořte webovou aplikaci v ASP.NET.

    ![Vytvoření webu](tutorial-getting-started-with-signalr/_static/image2.png)

1. V okně **Nový projekt ASP.NET – SignalRChat** ponechte vybrané **prázdné** a vyberte **OK**.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.

1. V **příkaz Přidat novou položku-SignalRChat**vyberte možnost **nainstalováno** ** > C# > ** webového ** > a** vyberte položku **centrum signalizace (v2)** .

1. Pojmenujte třídu *ChatHub* a přidejte ji do projektu.

    Tento krok vytvoří soubor třídy *ChatHub.cs* a přidá sadu souborů skriptu a odkazy na sestavení, které podporují signalizaci do projektu.

1. Nahraďte kód v novém souboru třídy *ChatHub.cs* tímto kódem:

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.

1. V **položce Přidat novou položku – SignalRChat** vyberte **nainstalované** > **Visual C#**  > **Web** a pak vyberte **třídu pro spuštění Owin**.

1. Pojmenujte *spouštěcí* třídu a přidejte ji do projektu.

1. Nahraďte výchozí kód ve *spouštěcí* třídě tímto kódem:

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **stránku HTML**.

1. Pojmenujte nový *index* stránky a vyberte **OK**.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na stránku HTML, kterou jste vytvořili, a vyberte **nastavit jako úvodní stránku**.

1. Nahraďte výchozí kód na stránce HTML tímto kódem:

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. V **Průzkumník řešení**rozbalte položku **skripty**.

    Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.

    > [!IMPORTANT]
    > Správce balíčků možná nainstaloval novější verzi skriptů nástroje Signaler.

1. Ověřte, zda odkazy skriptu v bloku kódu odpovídají verzím souborů skriptu v projektu.

    Odkazy skriptu z původního bloku kódu:

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. Pokud se neshodují, aktualizujte soubor *. html* .

1. V řádku nabídek vyberte **soubor** > **Uložit vše**.

## <a name="run-the-sample"></a>Spuštění ukázky

1. Na panelu nástrojů zapněte **ladění skriptů** a pak výběrem tlačítka Přehrát spusťte ukázku v režimu ladění.

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr/_static/image3.png)

1. Po otevření prohlížeče zadejte název vaší identity chatu.

1. Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.

1. V každém prohlížeči zadejte jedinečný název.

1. Nyní přidejte komentář a vyberte **Odeslat**. Tento postup opakujte v ostatních prohlížečích. Komentáře se zobrazí v reálném čase.

    > [!NOTE]
    > Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru. Centrum vysílá komentáře všem aktuálním uživatelům. Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.

    Podívejte se, jak aplikace chat běží ve třech různých prohlížečích. Když Anand a Zuzana odesílají zprávy, všechny prohlížeče se aktualizují v reálném čase:

    ![Všechny tři prohlížeče zobrazují stejnou historii chatu.](tutorial-getting-started-with-signalr/_static/image4.png)

1. V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci. K dispozici je soubor skriptu s názvem *centra* , který knihovna signálů generuje za běhu. Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru.

    ![automaticky vygenerovaný skript Centers v uzlu dokumenty skriptu](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>Kontrola kódu

Aplikace SignalRChat ukazuje dva základní úlohy vývoje signálu. Ukazuje, jak vytvořit centrum. Server používá toto centrum jako hlavní objekt koordinace. Centrum používá ke posílání a přijímání zpráv knihovnu jQuery nástroje Signal.

### <a name="signalr-hubs-in-the-chathubcs"></a>Rozbočovače signálů v ChatHub.cs

Ve výše uvedeném příkladu kódu je třída `ChatHub` odvozena od `Microsoft.AspNet.SignalR.Hub` třídy. Odvození od `Hub` třídy je užitečný způsob, jak vytvořit aplikaci signalizace. Veřejné metody můžete vytvořit na třídě centra a pak je použít tak, že je zavoláte ze skriptů na webové stránce.

V kódu chatu klienti volají metodu `ChatHub.Send` k odeslání nové zprávy. Centrum pak pošle zprávu všem klientům voláním `Clients.All.broadcastMessage`.

Metoda `Send` ukazuje několik konceptů centra:

* Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.

* `Microsoft.AspNet.SignalR.Hub.Clients` dynamickou vlastnost můžete použít ke komunikaci se všemi klienty připojenými k tomuto centru.

* Chcete-li aktualizovat klienty, zavolejte na klienta funkci (například funkce `broadcastMessage`).

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>Signál a jQuery v souboru index. html

Stránka *index. html* v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace. Kód provede mnoho důležitých úloh. Deklaruje proxy server pro odkazování na centrum, deklaruje funkci, kterou může server volat, aby zavolal obsah do klientů, a spustí připojení k odesílání zpráv do centra.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> V JavaScriptu odkaz na třídu serveru a jeho členové musí být camelCase. Ukázka kódu odkazuje na C# třídu *ChatHub* v jazyce JavaScript jako `chatHub`.

V tomto bloku kódu vytvoříte ve skriptu funkci zpětného volání.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi. Dva řádky, které obsah ve formátu HTML kóduje před jeho zobrazením, jsou volitelné a zobrazují dobrý způsob, jak zabránit vkládání skriptu.

Tento kód otevře připojení k centru.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> Tento přístup zajišťuje, že kód vytvoří připojení před tím, než se spustí obslužná rutina události.

Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce HTML.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a>Další zdroje

Další informace o signalizaci naleznete v následujících zdrojích informací:

* [Projekt signálu](http://signalr.net)

* [GitHub a ukázky signálů](https://github.com/SignalR/SignalR)

* [Wiki signálu](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Další kroky

V tomto kurzu:

> [!div class="checklist"]
> * Nastavení projektu
> * Byla spuštěna ukázka
> * Zkontrolování kódu

Přejděte k dalšímu článku, kde se dozvíte, jak používat signalizaci a MVC 5.
> [!div class="nextstepaction"]
> [Signal 2 a MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)