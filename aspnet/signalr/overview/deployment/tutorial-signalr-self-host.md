---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 'Kurz: samoobslužný signál pro hostování | Microsoft Docs'
author: bradygaster
description: V tomto kurzu se dozvíte, jak vytvořit server s nástrojem Signal-Host 2 a jak se k němu připojit pomocí JavaScriptového klienta. Verze softwaru používané v kurzu V...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74578569"
---
# <a name="tutorial-signalr-self-host"></a>Kurz: SignalR v místním prostředí

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> V tomto kurzu se dozvíte, jak vytvořit server s nástrojem Signal-Host 2 a jak se k němu připojit pomocí JavaScriptového klienta.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Signal – verze 2
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>Pomocí sady Visual Studio 2012 s tímto kurzem
>
>
> Chcete-li použít Visual Studio 2012 s tímto kurzem, postupujte následovně:
>
> - Aktualizujte [Správce balíčků](http://docs.nuget.org/docs/start-here/installing-nuget) na nejnovější verzi.
> - Nainstalujte [instalační program webové platformy](https://www.microsoft.com/web/downloads/platform.aspx).
> - V instalačním programu webové platformy vyhledejte a nainstalujte **ASP.NET and Web Tools 2013,1 pro Visual Studio 2012**. Tím se nainstaluje šablony sady Visual Studio pro třídy signalizace, jako je například **centrum**.
> - Některé šablony (například **Třída Owin Startup**) nebudou k dispozici. pro tyto soubory použijte místo toho soubor třídy.
>
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Server signalizace je obvykle hostován v aplikaci ASP.NET ve službě IIS, ale může být také v místním prostředí (například v konzolové aplikaci nebo ve službě Windows) pomocí knihovny pro samoobslužné hostování. Tato knihovna, stejně jako všechny signály 2, je postavená na OWIN ([Open Web Interface for .NET](http://owin.org)). OWIN definuje abstrakci mezi webovými servery .NET a webovými aplikacemi. OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS.

Důvody pro nehostování ve službě IIS zahrnují:

- Prostředí, ve kterých služba IIS není k dispozici nebo je žádoucí, jako je například existující serverová farma bez služby IIS.
- Nároky na výkon služby IIS je třeba vyhnout.
- Funkce signalizace se přidá do existující aplikace, která běží ve službě Windows, v roli pracovního procesu Azure nebo v jiném procesu.

Pokud je řešení vyvíjené jako samostatný hostitel z důvodů výkonu, doporučuje se také otestovat aplikaci hostovanou službou IIS, aby se zjistilo zvýhodnění výkonu.

Tento kurz obsahuje následující oddíly:

- [Vytvoření serveru](#server)
- [Přístup k serveru pomocí JavaScriptového klienta](#js)

<a id="server"></a>

## <a name="creating-the-server"></a>Vytvoření serveru

V tomto kurzu vytvoříte Server, který je hostovaný v konzolové aplikaci, ale server se může hostovat v jakémkoli procesu, jako je například služba systému Windows nebo role pracovního procesu Azure. Vzorový kód pro hostování serveru signalizace ve službě systému Windows najdete v tématu [signál pro samoobslužné hostování ve službě systému Windows](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).

1. Otevřete Visual Studio 2013 s oprávněními správce. Vyberte **soubor**, **Nový projekt**. V uzlu  **C# vizuálu** v podokně **šablony** vyberte možnost **Windows** a vyberte šablonu **Konzolová aplikace** . Pojmenujte nový projekt "SignalRSelfHost" a klikněte na tlačítko **OK**.

    ![](tutorial-signalr-self-host/_static/image1.png)
2. Otevřete konzolu Správce balíčků NuGet výběrem **nástrojů** > **správce balíčků NuGet** > **konzole správce balíčků**.
3. V konzole správce balíčků zadejte následující příkaz:

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    Tento příkaz přidá do projektu knihovny pro samoobslužné hostování Signal 2.
4. V konzole správce balíčků zadejte následující příkaz:

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    Tento příkaz přidá do projektu knihovnu Microsoft. Owin. Cors. Tato knihovna se bude používat pro podporu mezi doménami, která je nutná pro aplikace, které hostuje signál a klienta webové stránky v různých doménách. Vzhledem k tomu, že budete hostovat server signálu a webového klienta na různých portech, znamená to, že pro komunikaci mezi těmito součástmi musí být povolena mezidoménová služba.
5. Obsah Program.cs nahraďte následujícím kódem.

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    Výše uvedený kód zahrnuje tři třídy:

    - **Program**, včetně metody **Main** definující primární cestu provádění. V této metodě se webová aplikace typu **spuštění** spouští na zadané adrese URL (`http://localhost:8080`). Pokud je na koncovém bodu vyžadováno zabezpečení, může být implementován protokol SSL. Další informace najdete v tématu [Postup: Konfigurace portu s certifikátem SSL](https://msdn.microsoft.com/library/ms733791.aspx) .
    - **Po spuštění**třída obsahující konfiguraci serveru signalizace (jediná konfigurace, kterou tento kurz používá, je volání `UseCors`) a volání `MapSignalR`, které vytváří trasy pro všechny objekty hub v projektu.
    - **MyHub**, třída centra signálů, kterou aplikace bude poskytovat klientům. Tato třída má jedinou metodu, kterou klienti budou **volat, aby**vysílaly zprávu všem ostatním připojeným klientům.
6. Zkompilujte a spusťte aplikaci. Adresa, na které je spuštěn server, by měla být zobrazena v okně konzoly.

    ![](tutorial-signalr-self-host/_static/image2.png)
7. Pokud spuštění selže s výjimkou `System.Reflection.TargetInvocationException was unhandled`, bude nutné restartovat aplikaci Visual Studio s oprávněními správce.
8. Než budete pokračovat k další části, zastavte aplikaci.

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a>Přístup k serveru pomocí JavaScriptového klienta

V této části použijete stejného klienta JavaScriptu v [kurzu Začínáme](../getting-started/tutorial-getting-started-with-signalr.md). Klientovi provedeme jenom jednu změnu, která bude explicitně definovat adresu URL centra. V případě samoobslužné aplikace nemusí být server nutně na stejné adrese jako adresa URL připojení (z důvodu reverzních proxy serverů a nástrojů pro vyrovnávání zatížení), takže adresu URL je potřeba definovat explicitně.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na řešení a vyberte **Přidat**, **Nový projekt**. Vyberte uzel **Web** a vyberte šablonu **webové aplikace ASP.NET** . Pojmenujte projekt "JavascriptClient" a klikněte na tlačítko **OK**.

    ![](tutorial-signalr-self-host/_static/image3.png)
2. Vyberte **prázdnou** šablonu a nechejte zbývající možnosti nevybrané. Vyberte **vytvořit projekt**.

    ![](tutorial-signalr-self-host/_static/image4.png)
3. V konzole správce balíčků vyberte projekt "JavascriptClient" v rozevíracím seznamu **výchozí projekt** a spusťte následující příkaz:

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    Tento příkaz nainstaluje do klienta knihovny pro signalizaci a JQuery, které budete potřebovat.
4. Klikněte pravým tlačítkem na projekt a vyberte **Přidat**, **Nová položka**. Vyberte uzel **Web** a vyberte stránku HTML. Pojmenujte stránku **Default. html**.

    ![](tutorial-signalr-self-host/_static/image5.png)
5. Obsah nové stránky HTML nahraďte následujícím kódem. Ověřte, zda odkazy na skript zde odpovídají skriptům ve složce Scripts v projektu.

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    Následující kód (zvýrazněný výše v ukázce kódu výše) je přidání, které jste provedli pro klienta použitého v kurzu získání vloženého textu (kromě upgradu kódu na Signal verze 2 Beta). Tento řádek kódu explicitně nastavuje základní adresu URL pro signál na serveru.

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. Klikněte pravým tlačítkem na řešení a vyberte **nastavit projekty po spuštění...** . Vyberte přepínač **více projektů po spuštění** a nastavte **akci** u obou projektů na **Spustit**.

    ![](tutorial-signalr-self-host/_static/image6.png)
7. Klikněte pravým tlačítkem na Default. html a vyberte **nastavit jako úvodní stránku**.
8. Spusťte aplikaci. Spustí se server a stránka. Pokud se stránka načte před spuštěním serveru, může být nutné znovu načíst webovou stránku (nebo v ladicím programu vybrat možnost **pokračovat** ).
9. Po zobrazení výzvy zadejte v prohlížeči uživatelské jméno. Zkopírujte adresu URL stránky do jiné karty nebo okna prohlížeče a zadejte jiné uživatelské jméno. Můžete odesílat zprávy z jednoho podokna prohlížeče do druhé, jako v kurzu Začínáme.
