---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 'Kurz: Začínáme se signálem 1. x a MVC 4 | Microsoft Docs'
author: bradygaster
description: Pomocí ASP.NET signalizace a ASP.NET MVC 4 sestavte aplikaci Chat v reálném čase.
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579567"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a>Kurz: Začínáme s knihovnou SignalR 1.x a MVC 4

autor – [Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> V tomto kurzu se dozvíte, jak pomocí ASP.NET signalizace vytvořit aplikaci Chat v reálném čase. Přidáte signál do aplikace MVC 4 a vytvoříte zobrazení chatu pro odesílání a zobrazování zpráv.

## <a name="overview"></a>Přehled

V tomto kurzu se seznámíte s vývojem webových aplikací v reálném čase pomocí ASP.NET signalizace a ASP.NET MVC 4. Kurz používá stejný kód aplikace chatu jako [Začínáme kurz pro signalizaci](tutorial-getting-started-with-signalr.md), ale ukazuje, jak ho přidat do aplikace MVC 4 založené na šabloně Internet.

V tomto tématu se seznámíte s následujícími vývojovými úkoly signalizace:

- Přidání knihovny signalizace do aplikace MVC 4.
- Vytvoření třídy centra pro nabízení obsahu klientům.
- Posílání zpráv a zobrazování aktualizací z centra pomocí knihovny jQuery v nástroji Signald na webové stránce

Následující snímek obrazovky ukazuje dokončenou aplikaci Chat spuštěnou v prohlížeči.

![Instance chatu](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

Řezů

- [Nastavení projektu](#setup)
- [Spuštění ukázky](#run)
- [Kontrola kódu](#code)
- [Další kroky](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>Nastavení projektu

Požadavky:

- Visual Studio 2010 SP1, Visual Studio 2012 nebo Visual Studio 2012 Express. Pokud nemáte Visual Studio, přečtěte si článek [ASP.NET downloads](https://www.asp.net/downloads) , kde získáte bezplatný vývojářský nástroj sady Visual Studio 2012 Express.
- V případě sady Visual Studio 2010 nainstalujte [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).

V této části se dozvíte, jak vytvořit aplikaci ASP.NET MVC 4, přidat knihovnu signálů a vytvořit aplikaci Chat.

1. 1. V aplikaci Visual Studio vytvořte aplikaci ASP.NET MVC 4, pojmenujte ji SignalRChat a klikněte na tlačítko OK.

        > [!NOTE]
        > V VS 2010 vyberte v ovládacím prvku rozevíracího seznamu verze rozhraní **.NET Framework 4** . Kód signalizace běží na .NET Framework verzích 4 a 4,5.

        ![Vytvořit web MVC](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. Vyberte šablonu internetové aplikace, zrušte zaškrtnutí políčka pro **Vytvoření projektu testu jednotek**a klikněte na OK.

         ![Vytvořit internetový web MVC](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. Otevřete **nástroje > správce balíčků NuGet > konzole správce balíčků** a spusťte následující příkaz. Tento krok přidá do projektu sadu souborů skriptu a odkazy na sestavení, které umožňují funkci signalizace.

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. V **Průzkumník řešení** rozbalte složku skripty. Všimněte si, že knihovny skriptů pro signalizaci byly přidány do projektu.

         ![Odkazy knihovny](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt, vyberte **Přidat | Novou složku**a přidejte novou složku s názvem **centra**.
      6. Klikněte pravým tlačítkem na složku **Centers** , klikněte na **Přidat | Třídu**a vytvořte novou C# třídu s názvem **ChatHub.cs**. Tuto třídu použijete jako rozbočovač serveru signalizace, který odesílá zprávy všem klientům.

> [!NOTE]
> Pokud používáte Visual Studio 2012 a máte nainstalovanou [aktualizaci ASP.NET and Web Tools 2012,2](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), můžete k vytvoření třídy centra použít novou šablonu položky signaler. Provedete to tak, že kliknete pravým tlačítkem na složku **Centers** , kliknete na **Přidat | Nová položka**, vyberte **Třída centra signalizace (V1)** a pojmenujte třídu **ChatHub.cs**.

1. Nahraďte kód ve třídě **ChatHub** následujícím kódem.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. Otevřete soubor **Global. asax** pro projekt a přidejte volání metody `RouteTable.Routes.MapHubs();` jako první řádek kódu v metodě `Application_Start`. Tento kód zaregistruje výchozí trasu pro centra signálů a musí se volat před registrací jakýchkoli jiných tras. Metoda Completed `Application_Start` vypadá jako v následujícím příkladu.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. Upravte třídu `HomeController` nalezenou v **Controllers/HomeController. cs** a přidejte následující metodu do třídy. Tato metoda vrátí zobrazení **chatu** , které budete vytvářet v pozdějším kroku.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. Klikněte pravým tlačítkem na právě vytvořenou metodu `Chat` a kliknutím na tlačítko **Přidat zobrazení** vytvořte nový soubor zobrazení.
5. V dialogovém okně **Přidat zobrazení** zaškrtněte políčko pro **použití rozložení nebo stránky předlohy** (zrušte zaškrtnutí těchto políček) a pak klikněte na tlačítko **Přidat**.

    ![Přidání zobrazení](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. Upravte nový soubor zobrazení s názvem **chat. cshtml**. Po značce &lt;H2&gt; vložte následující oddíl &lt;div&gt; a `@section scripts` blok kódu na stránku. Tento skript umožňuje stránce odesílat zprávy chatu a zobrazovat zprávy ze serveru. V následujícím bloku kódu se zobrazí úplný kód pro zobrazení chatu.

    > [!IMPORTANT]
    > Když přidáte do projektu sady Visual Studio signál a další knihovny skriptu, správce balíčků může nainstalovat verze skriptů, které jsou novější než verze uvedené v tomto tématu. Ujistěte se, že odkazy skriptu v kódu odpovídají verzím knihoven skriptů nainstalovaných ve vašem projektu.

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. **Uložit vše** pro projekt.

<a id="run"></a>

## <a name="run-the-sample"></a>Spuštění ukázky

1. Stisknutím klávesy F5 spusťte projekt v režimu ladění.
2. Na řádku Adresa prohlížeče přidejte **/Home/chat** k adrese URL výchozí stránky projektu. Stránka konverzace se načte do instance prohlížeče a zobrazí výzvu k zadání uživatelského jména.

    ![Zadat uživatelské jméno](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. Zadejte jméno uživatele.
4. Zkopírujte adresu URL z adresního řádku prohlížeče a použijte ji k otevření dvou dalších instancí prohlížeče. V každé instanci prohlížeče zadejte jedinečné uživatelské jméno.
5. V každé instanci prohlížeče přidejte komentář a klikněte na **Odeslat**. Komentáře by se měly zobrazit ve všech instancích prohlížeče.

    > [!NOTE]
    > Tato jednoduchá aplikace chatu neudržuje kontext diskuze na serveru. Centrum vysílá komentáře všem aktuálním uživatelům. Uživatelům, kteří se k chatu připojí později, se zobrazí zprávy přidané od okamžiku, kdy se připojí.
6. Následující snímek obrazovky ukazuje aplikaci Chat spuštěnou v prohlížeči.

    ![Prohlížeče chatu](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. V **Průzkumník řešení**zkontrolujte uzel **dokumenty skriptu** pro spuštěnou aplikaci. Tento uzel je viditelný v režimu ladění, pokud používáte Internet Explorer jako prohlížeč. Existuje soubor skriptu **s názvem hub** , který knihovna signálů dynamicky generuje za běhu. Tento soubor spravuje komunikaci mezi skriptem jQuery a kódem na straně serveru. Pokud používáte jiný prohlížeč než Internet Explorer, můžete k souboru dynamického **centra** přistupovat také tak, že na něj přejdete přímo, například http://mywebsite/signalr/hubs.

    ![Generovaný skript centra](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a>Kontrola kódu

Chatovací aplikace pro signály znázorňuje dva základní úlohy vývoje signálu: vytváření rozbočovače jako hlavního objektu koordinace na serveru a použití knihovny jQuery nástroje Signal k posílání a přijímání zpráv.

### <a name="signalr-hubs"></a>Rozbočovače signálu

V ukázce kódu je třída **ChatHub** odvozena od třídy **Microsoft. ASPNET. signaler. hub** . Odvození od třídy **centra** je užitečný způsob, jak vytvořit aplikaci signalizace. Veřejné metody můžete vytvořit na třídě centra a potom k těmto metodám přistupovat voláním ze skriptů jQuery na webové stránce.

V kódu chatu klienti volají metodu **ChatHub. Send** k odeslání nové zprávy. Centrum pak pošle zprávu všem klientům voláním **clients. All. addNewMessageToPage**.

Metoda **Send** ukazuje několik konceptů centra:

- Deklarovat veřejné metody na rozbočovači, aby je klienti mohli volat.
- Pro přístup ke všem klientům připojeným k tomuto centru použijte vlastnost **Microsoft. ASPNET. signaler. hub. clients** .
- Chcete-li aktualizovat klienty, zavolejte na klienta funkci jQuery (například funkci `addNewMessageToPage`).

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>Signál a jQuery

Soubor zobrazení **chat. cshtml** v ukázce kódu ukazuje, jak použít knihovnu jQuery signalizace ke komunikaci s centrem signalizace. Zásadní úlohy v kódu vytvářejí odkaz na automaticky generovaný proxy server pro centrum a deklaruje funkci, kterou může server volat, aby zavolal obsah do klientů, a spustí připojení pro posílání zpráv do centra.

Následující kód deklaruje proxy server pro rozbočovač.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> V jQuery je odkaz na třídu serveru a jeho členy v případě ve stylu CamelCase. Ukázka kódu odkazuje na C# třídu **ChatHub** ve jQuery jako **ChatHub**. Pokud chcete odkazovat na třídu `ChatHub` v jQuery pomocí konvenčních malých písmen Pascal, jako byste měli C#v, upravte soubor třídy ChatHub.cs. Přidejte příkaz `using`, který odkazuje na obor názvů `Microsoft.AspNet.SignalR.Hubs`. Pak přidejte atribut `HubName` do třídy `ChatHub`, například `[HubName("ChatHub")]`. Nakonec aktualizujte svůj odkaz jQuery na třídu `ChatHub`.

Následující kód ukazuje, jak vytvořit funkci zpětného volání ve skriptu. Třída centra na serveru volá tuto funkci, aby nanabízela aktualizace obsahu každému klientovi. Volitelné volání funkce `htmlEncode` ukazuje způsob, jak HTML kódovat obsah zprávy před jeho zobrazením na stránce, jako způsob, jak zabránit vkládání skriptu.

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

Následující kód ukazuje, jak otevřít připojení pomocí centra. Kód spustí připojení a poté předá funkci pro zpracování události Click v tlačítku **Odeslat** na stránce konverzace.

> [!NOTE]
> Tento přístup zajišťuje, aby bylo připojení vytvořeno před spuštěním obslužné rutiny události.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>Další kroky

Naučili jste se, že Signal je architektura pro vytváření webových aplikací v reálném čase. Zjistili jste také několik úloh vývoje signálů: Přidání signálu do aplikace ASP.NET, vytvoření třídy centra a odeslání a přijetí zpráv z centra.

Další informace o pokročilých konceptech pro vývoj signalizace najdete na následujících webech, na kterých se nachází zdrojový kód a zdroje signálů:

- [Projekt signálu](http://signalr.net)
- [GitHub a ukázky signálů](https://github.com/SignalR/SignalR)
- [Wiki signálu](https://github.com/SignalR/SignalR/wiki)
