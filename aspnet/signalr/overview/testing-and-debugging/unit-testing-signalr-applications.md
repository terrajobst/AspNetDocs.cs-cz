---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: Aplikace Signal test jednotek | Microsoft Docs
author: bradygaster
description: Tento článek popisuje, jak používat funkce testování částí nástroje Signaler 2,0.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578671"
---
# <a name="unit-testing-signalr-applications"></a>Testování jednotek aplikace knihovnou SignalR

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek popisuje použití funkcí testování částí v Signaler 2.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Signal – verze 2
>
>
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>Aplikace signalizace testování částí

Pomocí funkcí testování částí ve službě Signaler 2 můžete vytvořit testy jednotek pro vaši aplikaci signalizace. Signal 2 obsahuje rozhraní [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) , které se dá použít k vytvoření objektu pro simulaci vašich metod rozbočovače pro účely testování.

V této části přidáte testy jednotek pro aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) pomocí [XUnit.NET](https://github.com/xunit/xunit) a [MOQ](https://github.com/Moq/moq4).

XUnit.net se bude používat k řízení testu. MOQ se použije k vytvoření objektu [makety](http://en.wikipedia.org/wiki/Mock_object) pro testování. V případě potřeby lze použít jiné rozhraní pro návrhy. [NSubstitute](http://nsubstitute.github.io/) je také dobrou volbou. V tomto kurzu se dozvíte, jak nastavit objekt kresby dvěma způsoby: nejprve pomocí objektu `dynamic` (představený v .NET Framework 4) a s použitím rozhraní.

### <a name="contents"></a>Obsah

Tento kurz obsahuje následující oddíly.

- [Testování částí s dynamickým](#dynamic)
- [Testování částí podle typu](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>Testování částí s dynamickým

V této části přidáte test jednotek pro aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) pomocí dynamického objektu.

1. Nainstalujte [rozšíření XUnit Runner](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) pro Visual Studio 2013.
2. Buď dokončete [kurz Začínáme](../getting-started/tutorial-getting-started-with-signalr.md), nebo si stáhněte dokončenou aplikaci z [Galerie kódu na webu MSDN](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).
3. Pokud používáte aplikaci Začínáme ke stažení, otevřete **konzolu Správce balíčků** a kliknutím na **obnovit** přidejte do projektu balíček signalizace.

    ![Obnovit balíčky](unit-testing-signalr-applications/_static/image1.png)
4. Přidejte projekt do řešení pro testování částí. Klikněte pravým tlačítkem na své řešení v **Průzkumník řešení** a vyberte **Přidat**, **Nový projekt...** . V **C#** uzlu vyberte uzel **Windows** . Vyberte možnost **Knihovna tříd**. Pojmenujte nový projekt **TestLibrary** a klikněte na **OK**.

    ![Vytvořit knihovnu testů](unit-testing-signalr-applications/_static/image2.png)
5. Přidejte odkaz do projektu knihovny testů do projektu SignalRChat. Klikněte pravým tlačítkem na projekt **TestLibrary** a vyberte **Přidat**, **odkaz.** ... V uzlu **řešení** vyberte uzel **projekty** a zaškrtněte **SignalRChat**. Klikněte na tlačítko **OK**.

    ![Přidat odkaz na projekt](unit-testing-signalr-applications/_static/image3.png)
6. Přidejte do projektu **TestLibrary** balíčky signálu, MOQ a XUnit. V **konzole správce balíčků**nastavte výchozí rozevírací seznam **projektu** na **TestLibrary**. V okně konzoly spusťte následující příkazy:

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![Nainstalovat balíčky](unit-testing-signalr-applications/_static/image4.png)
7. Vytvořte testovací soubor. Klikněte pravým tlačítkem na projekt **TestLibrary** a klikněte na **Přidat...** , **Třída**. Pojmenujte novou třídu **Tests.cs**.
8. Obsah Tests.cs nahraďte následujícím kódem.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    Ve výše uvedeném kódu je testovací klient vytvořen pomocí objektu `Mock` z knihovny [MOQ](https://github.com/Moq/moq4) , typu [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in signal 2,1, přiřazení `dynamic` pro parametr typu.) Rozhraní `IHubCallerConnectionContext` je objekt proxy, pomocí kterého jste na klientovi vyvolali metody. Funkce `broadcastMessage` je pak definována pro maketa klienta, aby ji bylo možné volat pomocí `ChatHub` třídy. Testovací modul pak zavolá metodu `Send` třídy `ChatHub`, která zase volá napodobnou `broadcastMessage` funkci.
9. Sestavte řešení stisknutím klávesy **F6**.
10. Spusťte Jednotkový test. V aplikaci Visual Studio vyberte **test**, **Windows**, **Průzkumník testů**. V okně Průzkumník testů klikněte pravým tlačítkem na **HubsAreMockableViaDynamic** a vyberte **Spustit vybrané testy**.

    ![Průzkumník testů](unit-testing-signalr-applications/_static/image5.png)
11. Ověřte, zda byl test úspěšný, kontrolou dolního podokna v okně Průzkumníka testů. V okně se zobrazí, že test proběhl úspěšně.

    ![Test byl úspěšný](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>Testování částí podle typu

V této části přidáte test pro aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) pomocí rozhraní, které obsahuje metodu, která má být testována.

1. Proveďte kroky 1-7 v části [testování částí pomocí dynamického](#dynamic) kurzu výše.
2. Obsah Tests.cs nahraďte následujícím kódem.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    Ve výše uvedeném kódu se vytvoří rozhraní definující signaturu `broadcastMessage` metody, pro kterou testovací modul vytvoří strojového klienta. Napodobný klient je pak vytvořen pomocí objektu `Mock` typu [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in Signal 2,1, přiřazení `dynamic` parametru typu.) Rozhraní `IHubCallerConnectionContext` je objekt proxy, pomocí kterého jste na klientovi vyvolali metody.

    Test poté vytvoří instanci `ChatHub`a poté vytvoří maketnou verzi metody `broadcastMessage`, která je zase vyvolána voláním metody `Send` na rozbočovači.
3. Sestavte řešení stisknutím klávesy **F6**.
4. Spusťte Jednotkový test. V aplikaci Visual Studio vyberte **test**, **Windows**, **Průzkumník testů**. V okně Průzkumník testů klikněte pravým tlačítkem na **HubsAreMockableViaDynamic** a vyberte **Spustit vybrané testy**.

    ![Průzkumník testů](unit-testing-signalr-applications/_static/image7.png)
5. Ověřte, zda byl test úspěšný, kontrolou dolního podokna v okně Průzkumníka testů. V okně se zobrazí, že test proběhl úspěšně.

    ![Test byl úspěšný](unit-testing-signalr-applications/_static/image8.png)
