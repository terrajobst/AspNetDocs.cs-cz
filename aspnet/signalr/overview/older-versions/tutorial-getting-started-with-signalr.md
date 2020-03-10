---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 'Kurz: Začínáme se signálem 1. x | Microsoft Docs'
author: bradygaster
description: Použijte signál ASP.NET k vytvoření aplikace chat v reálném čase na stránce HTML.
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623541"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a>Kurz: Začínáme s knihovnou SignalR 1.x

autor – [Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> V tomto kurzu se naučíte používat funkci SignalR k vytvoření aplikace pro chatování v reálném čase. Přidáte signál do prázdné webové aplikace v ASP.NET a vytvoříte stránku HTML pro odesílání a zobrazování zpráv.

## <a name="overview"></a>Přehled

V tomto kurzu se seznámíte s vývojem signalizace tím, že se dozvíte, jak vytvořit jednoduchou chatovací aplikaci založenou na prohlížeči. Přidáte knihovnu signálů do prázdné webové aplikace v ASP.NET, vytvoříte třídu centra pro posílání zpráv klientům a vytvoříte stránku HTML, která umožní uživatelům odesílat a přijímat zprávy chatu. Podobný kurz, který ukazuje, jak vytvořit aplikaci chatu v MVC 4 pomocí zobrazení MVC, najdete v tématu [Začínáme s nástrojem Signal and MVC 4](index.md).

> [!NOTE]
> V tomto kurzu se používá verze nástroje Signal (verze 1. x). Podrobnosti o změnách mezi signálem 1. x a 2,0 naleznete v tématu Upgrade pro předaných [projektů s návěstí 1. x](../releases/upgrading-signalr-1x-projects-to-20.md).

Signal je open source knihovna .NET pro vytváření webových aplikací, které vyžadují živé interakce uživatelů nebo aktualizace dat v reálném čase. Mezi příklady patří sociální aplikace, hry pro víc uživatelů, obchodní spolupráce a novinky, počasí nebo aplikace pro finanční aktualizace. Ty se často nazývají aplikace v reálném čase.

Návěstí zjednodušuje proces vytváření aplikací v reálném čase. Obsahuje knihovnu serveru ASP.NET a klientskou knihovnu JavaScriptu, která usnadňuje správu připojení klient-server a nabízených aktualizací obsahu klientům. Knihovnu signálů můžete přidat do existující aplikace ASP.NET, abyste získali funkce v reálném čase.

V tomto kurzu se dozvíte o následujících úkolech pro vývoj signálů:

- Přidání knihovny signalizace do webové aplikace ASP.NET.
- Vytvoření třídy centra pro nabízení obsahu klientům.
- Posílání zpráv a zobrazování aktualizací z centra pomocí knihovny jQuery v nástroji Signald na webové stránce

Následující snímek obrazovky ukazuje aplikaci Chat spuštěnou v prohlížeči. Každý nový uživatel může publikovat komentáře a zobrazit komentáře přidané poté, co se uživatel připojí k chatu.

![Instance chatu](tutorial-getting-started-with-signalr/_static/image1.png)

Řezů

- [Nastavení projektu](#setup)
- [Spuštění ukázky](#run)
- [Kontrola kódu](#code)
- [Další kroky](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>Nastavení projektu

V této části se dozvíte, jak vytvořit prázdnou webovou aplikaci v ASP.NET, přidat signál a vytvořit aplikaci Chat.

Požadavky:

- Visual Studio 2010 SP1 nebo 2012. Pokud nemáte Visual Studio, přečtěte si článek [ASP.NET downloads](https://www.asp.net/downloads) , kde získáte bezplatný vývojářský nástroj sady Visual Studio 2012 Express.
- [Microsoft ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=279941). V případě sady Visual Studio 2012 tento instalační program přidá do sady Visual Studio nové funkce ASP.NET včetně šablon signálů. V případě sady Visual Studio 2010 SP1 není instalační služba k dispozici, ale tento kurz můžete dokončit instalací balíčku NuGet pro signalizaci, jak je popsáno v krocích pro instalaci.

Následující kroky používají Visual Studio 2012 k vytvoření prázdné webové aplikace ASP.NET a přidání knihovny signalizace:

1. V aplikaci Visual Studio vytvořte prázdnou webovou aplikaci v ASP.NET.

    ![Vytvořit prázdný web](tutorial-getting-started-with-signalr/_static/image2.png)
2. Otevřete **konzolu Správce balíčků** tak, že vyberete **nástroje | Správce balíčků NuGet | Konzola správce balíčků**. Do okna konzoly zadejte následující příkaz:

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    Tento příkaz nainstaluje nejnovější verzi signalizace 1. x.
3. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt, vyberte **Přidat | Třída**. Pojmenujte novou třídu **ChatHub**.
4. V **Průzkumník řešení** rozbalte uzel skripty. Knihovny skriptů pro jQuery a Signal jsou viditelné v projektu.

    ![Odkazy knihovny](tutorial-getting-started-with-signalr/_static/image3.png)
5. Nahraďte kód ve třídě **ChatHub** následujícím kódem.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a pak klikněte na **Přidat | Nová položka**. V dialogovém okně **Přidat novou položku** vyberte možnost **globální třída aplikace** a klikněte na tlačítko **Přidat**.

    ![Přidat globální](tutorial-getting-started-with-signalr/_static/image4.png)
7. Po poskytnuté příkazy `using` ve třídě Global.asax.cs přidejte následující příkazy `using`.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. Přidejte následující řádek kódu do metody `Application_Start` globální třídy k registraci výchozí trasy pro centra signálu.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a pak klikněte na **Přidat | Nová položka**. V dialogovém okně **Přidat novou položku** vyberte možnost stránka HTML a klikněte na tlačítko **Přidat**.
10. V **Průzkumník řešení**klikněte pravým tlačítkem na právě vytvořenou stránku HTML a pak klikněte na **nastavit jako úvodní stránku**.
11. Nahraďte výchozí kód na stránce HTML následujícím kódem.

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. **Uložit vše** pro projekt.

<a id="run"></a>

## <a name="run-the-sample"></a>Spuštění ukázky

1. Stisknutím klávesy F5 spusťte projekt v režimu ladění. Stránka HTML se načte do instance prohlížeče a zobrazí výzvu k zadání uživatelského jména.

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr/_static/image5.png)
2. Zadejte jméno uživatele.
3. Zkopírujte adresu URL z adresního řádku prohlížeče a použijte ji k otevření dvou dalších instancí prohlížeče. V každé instanci prohlížeče zadejte jedinečné uživatelské jméno.
4. V každé instanci prohlížeče přidejte komentář a klikněte na **Odeslat**. Komentáře by se měly zobrazit ve všech instancích prohlížeče.

    > [!NOTE]
    > Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru. Centrum vysílá komentáře všem aktuálním uživatelům. Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.

    Následující snímek obrazovky ukazuje aplikaci Chat spuštěnou ve třech instancích prohlížeče, všechny, které jsou aktualizovány, když jedna instance pošle zprávu:

    ![Prohlížeče chatu](tutorial-getting-started-with-signalr/_static/image6.png)
5. V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci. Existuje soubor skriptu **s názvem hub** , který knihovna signálů dynamicky generuje za běhu. Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru.

    ![Generovaný skript centra](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a>Kontrola kódu

Chatovací aplikace pro signály znázorňuje dva základní úlohy vývoje signálu: vytváření rozbočovače jako hlavního objektu koordinace na serveru a použití knihovny jQuery nástroje Signal k posílání a přijímání zpráv.

### <a name="signalr-hubs"></a>Rozbočovače signálu

V ukázce kódu je třída **ChatHub** odvozena od třídy **Microsoft. ASPNET. signaler. hub** . Odvození od třídy **centra** je užitečný způsob, jak vytvořit aplikaci signalizace. Veřejné metody můžete vytvořit na třídě centra a potom k těmto metodám přistupovat voláním ze skriptů jQuery na webové stránce.

V kódu chatu klienti volají metodu **ChatHub. Send** k odeslání nové zprávy. Centrum pak pošle zprávu všem klientům voláním **clients. All. broadcastMessage**.

Metoda **Send** ukazuje několik konceptů centra:

- Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.
- K přístupu ke všem klientům připojeným k tomuto centru použijte dynamickou vlastnost **Microsoft. ASPNET. signaler. hub. clients** .
- Chcete-li aktualizovat klienty, zavolejte na klienta funkci jQuery (například funkci `broadcastMessage`).

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>Signál a jQuery

Stránka HTML v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace. Základní úlohy v kódu deklaruje proxy server pro odkazování na centrum a deklaraci funkce, kterou může server volat, aby zavolal obsah do klientů a spouštěl připojení pro odesílání zpráv do centra.

Následující kód deklaruje proxy server pro rozbočovač.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> V jQuery je odkaz na třídu serveru a jeho členy v případě ve stylu CamelCase. Ukázka kódu odkazuje na C# třídu **ChatHub** ve jQuery jako **ChatHub**.

Následující kód je způsob, jak ve skriptu vytvořit funkci zpětného volání. Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi. Dva řádky, které obsah HTML zakóduje před jeho zobrazením, jsou volitelné a zobrazují jednoduchý způsob, jak zabránit vkládání skriptu.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

Následující kód ukazuje, jak otevřít připojení pomocí centra. Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce HTML.

> [!NOTE]
> Tento přístup si zajistěte, aby bylo připojení navázáno, než se spustí obslužná rutina události.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>Další kroky

Naučili jste se, že Signal je architektura pro vytváření webových aplikací v reálném čase. Zjistili jste také několik úloh vývoje signálů: Přidání signálu do aplikace ASP.NET, vytvoření třídy centra a odeslání a přijetí zpráv z centra.

Ukázkovou aplikaci můžete vytvořit v tomto kurzu nebo v jiných aplikacích, které jsou k dispozici prostřednictvím Internetu, jejich nasazením pro poskytovatele hostingu. Microsoft nabízí bezplatné webové hostování až pro 10 webů na bezplatném [zkušebním účtu Windows Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604). Návod, jak nasadit ukázkovou aplikaci pro signalizaci, najdete v tématu [publikování ukázky Začínáme jako webu Windows Azure](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx). Podrobné informace o tom, jak nasadit webový projekt aplikace Visual Studio na web Windows Azure, najdete v tématu [nasazení aplikace ASP.NET na web Windows Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet). (Poznámka: přenos pomocí protokolu WebSocket není v současné době pro weby Windows Azure podporován. Pokud není přenos pomocí protokolu WebSocket k dispozici, používá signál další dostupné přenosy, jak je popsáno v části přenosy v [tématu Úvod do signalizace](index.md).)

Další informace o pokročilých konceptech pro vývoj signalizace najdete na následujících webech, na kterých se nachází zdrojový kód a zdroje signálů:

- [Projekt signálu](http://signalr.net)
- [GitHub a ukázky signálů](https://github.com/SignalR/SignalR)
- [Wiki signálu](https://github.com/SignalR/SignalR/wiki)
