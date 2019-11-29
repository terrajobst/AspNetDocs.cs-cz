---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 'Kurz: chat v reálném čase s nástrojem Signal 2 a MVC 5 | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se dozvíte, jak pomocí ASP.NET signalizace 2 vytvořit aplikaci chatu v reálném čase. Přidáte signalizaci do aplikace MVC 5.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600474"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a>Kurz: chat v reálném čase s nástrojem Signal 2 a MVC 5

V tomto kurzu se dozvíte, jak pomocí ASP.NET signalizace 2 vytvořit aplikaci chatu v reálném čase. Přidáte signalizaci do aplikace MVC 5 a vytvoříte zobrazení chatu pro odesílání a zobrazování zpráv.

V tomto kurzu:

> [!div class="checklist"]
> * Nastavení projektu
> * Spuštění ukázky
> * Kontrola kódu

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Požadavky

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) s úlohou **vývoje ASP.NET a webu** .

## <a name="set-up-the-project"></a>Nastavení projektu

V této části se dozvíte, jak pomocí sady Visual Studio 2017 a nástroje Signal 2 vytvořit prázdnou aplikaci ASP.NET MVC 5, přidat knihovnu signálů a vytvořit aplikaci Chat.

1. V aplikaci Visual Studio vytvořte aplikaci C# ASP.NET, která cílí na .NET Framework 4,5, pojmenujte ji SignalRChat a klikněte na tlačítko OK.

    ![Vytvoření webu](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. V **New ASP.NET Web Application – SignalRMvcChat**vyberte **MVC** a pak vyberte **změnit ověřování**.

1. V nabídce **změnit ověřování**vyberte **bez ověřování** a klikněte na **OK**.

    ![Vyberte bez ověřování.](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. V **New ASP.NET webová aplikace – SignalRMvcChat**vyberte **OK**.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **Nová položka**.

1. V **příkaz Přidat novou položku-SignalRChat**vyberte možnost **nainstalováno** ** > C# > ** webového ** > a** vyberte položku **centrum signalizace (v2)** .

1. Pojmenujte třídu *ChatHub* a přidejte ji do projektu.

    Tento krok vytvoří soubor třídy *ChatHub.cs* a přidá sadu souborů skriptu a odkazy na sestavení, které podporují signalizaci do projektu.

1. Nahraďte kód v novém souboru třídy *ChatHub.cs* tímto kódem:

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat** > **třídu**.

1. Pojmenujte nové *spuštění* třídy a přidejte je do projektu.

1. Nahraďte kód v souboru třídy *Startup.cs* tímto kódem:

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. V **Průzkumník řešení**vyberte možnost **řadiče** > **HomeController.cs**.

1. Přidejte tuto metodu do *HomeController.cs*.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    Tato metoda vrátí zobrazení **chatu** , které vytvoříte v pozdějším kroku.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na **zobrazení** > **Domů**a vyberte **Přidat** >  **zobrazení**.

1. V části **Přidat zobrazení**pojmenujte nové zobrazení **chat** a vyberte **Přidat**.

1. Obsah **chat. cshtml** nahraďte tímto kódem:

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. V **Průzkumník řešení**rozbalte položku **skripty**.

    Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.

    > [!IMPORTANT]
    > Správce balíčků možná nainstaloval novější verzi skriptů nástroje Signaler.

1. Ověřte, zda odkazy skriptu v bloku kódu odpovídají verzím souborů skriptu v projektu.

    Odkazy skriptu z původního bloku kódu:

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. Pokud se neshodují, aktualizujte soubor *. cshtml* .

1. V řádku nabídek vyberte **soubor** > **Uložit vše**.

## <a name="run-the-sample"></a>Spuštění ukázky

1. Na panelu nástrojů zapněte **ladění skriptů** a pak výběrem tlačítka Přehrát spusťte ukázku v režimu ladění.

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. Po otevření prohlížeče zadejte název vaší identity chatu.

1. Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do adresních úseček.

1. V každém prohlížeči zadejte jedinečný název.

1. Nyní přidejte komentář a vyberte **Odeslat**. Tento postup opakujte v ostatních prohlížečích. Komentáře se zobrazí v reálném čase.

    > [!NOTE]
    > Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru. Centrum vysílá komentáře všem aktuálním uživatelům. Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.

    Podívejte se, jak aplikace chat běží ve třech různých prohlížečích. Když Anand a Zuzana odesílají zprávy, všechny prohlížeče se aktualizují v reálném čase:

    ![Všechny tři prohlížeče zobrazují stejnou historii chatu.](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci. K dispozici je soubor skriptu s názvem *centra* , který knihovna signálů generuje za běhu. Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru.

    ![automaticky vygenerovaný skript Centers v uzlu dokumenty skriptu](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a>Kontrola kódu

Chatovací aplikace signalizace ukazuje dva základní úlohy vývoje signálu. Ukazuje, jak vytvořit centrum. Server používá toto centrum jako hlavní objekt koordinace. Centrum používá ke posílání a přijímání zpráv knihovnu jQuery nástroje Signal.

### <a name="signalr-hubs-in-the-chathubcs"></a>Rozbočovače signálů v ChatHub.cs

V ukázce kódu je třída `ChatHub` odvozena od `Microsoft.AspNet.SignalR.Hub` třídy. Odvození od `Hub` třídy je užitečný způsob, jak vytvořit aplikaci signalizace. Veřejné metody můžete vytvořit na třídě centra a potom k těmto metodám přistupovat voláním ze skriptů na webové stránce.

V kódu chatu klienti volají metodu `ChatHub.Send` k odeslání nové zprávy. Centrum pak pošle zprávu všem klientům voláním `Clients.All.addNewMessageToPage`.

Metoda `Send` ukazuje několik konceptů centra:

* Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.

* `Microsoft.AspNet.SignalR.Hub.Clients` dynamickou vlastnost můžete použít ke komunikaci se všemi klienty připojenými k tomuto centru.

* Chcete-li aktualizovat klienty, zavolejte na klienta funkci (například funkce `addNewMessageToPage`).

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a>Signál a jQuery chat. cshtml

Soubor zobrazení *chat. cshtml* v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace.  Kód provede mnoho důležitých úloh. Vytvoří odkaz na automaticky vygenerovaný proxy server pro centrum, deklaruje funkci, kterou může server volat, aby zavolal obsah do klientů, a spustí připojení k odesílání zpráv do centra.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> V jazyce JavaScript je odkaz na třídu serveru a jeho členy v camelCase. Ukázka kódu odkazuje na C# třídu `ChatHub` v jazyce JavaScript jako `chatHub`.

V tomto bloku kódu vytvoříte ve skriptu funkci zpětného volání.

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi. Volitelné volání funkce `htmlEncode` ukazuje způsob, jak HTML kódovat obsah zprávy před jeho zobrazením na stránce. Je to způsob, jak zabránit vkládání skriptu.

Tento kód otevře připojení k centru.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> Tento přístup zajišťuje, že navážete připojení, než se spustí obslužná rutina události.

Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce konverzace.

## <a name="get-the-code"></a>Získat kód

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a>Další materiály a zdroje informací

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

V dalším článku se dozvíte, jak vytvořit webovou aplikaci, která používá signál ASP.NET 2 k poskytování funkcí vysoké frekvence zasílání zpráv.
> [!div class="nextstepaction"]
> [Webová aplikace s vysokou frekvencí zasílání zpráv](tutorial-high-frequency-realtime-with-signalr.md)