---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Použití čítačů výkonu signalizace ve webové roli Azure | Microsoft Docs
author: guardrex
description: Jak nainstalovat a používat čítače výkonu signálů ve webové roli Azure
keywords: ASP. NET, signaler, čítač výkonu, Webová role Azure
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 969a2ce43a7cb8d649555daf282f900401c0c914
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578979"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>Použití čítačů výkonu signalizace ve webové roli Azure

Od [Luke Latham](https://github.com/guardrex)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Čítače výkonu signálu se používají ke sledování výkonu vaší aplikace ve webové roli Azure. Čítače jsou zachyceny Diagnostika Microsoft Azure. Čítače výkonu signálu do Azure nainstalujete pomocí nástroje *Signal. exe*, který se používá pro samostatné i místní aplikace. Vzhledem k tomu, že role Azure jsou přechodné, nakonfigurujete aplikaci, která bude instalovat a registrovat čítače výkonu signálu při spuštění.

## <a name="prerequisites"></a>Předpoklady

* Visual Studio 2015 nebo [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* Poznámka [k sadě Microsoft Azure SDK pro Visual Studio](https://azure.microsoft.com/downloads/) **: po instalaci sady SDK restartujte počítač.**
* Předplatné Microsoft Azure: Pokud si chcete zaregistrovat bezplatný zkušební účet Azure, podívejte se na [bezplatnou zkušební verzi Azure](https://azure.microsoft.com/free/).

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>Vytvoření aplikace webové role Azure, která zpřístupňuje čítače výkonu signálů

1. Otevřete sadu Visual Studio.

2. V aplikaci Visual Studio vyberte **soubor** > **Nový** > **projekt**.

3. V dialogovém okně **Nový projekt** vyberte na levé straně kategorii **cloudu**  **C# Visual** > a pak vyberte šablonu **cloudové služby Azure** . Pojmenujte aplikaci **SignalRPerfCounters** a vyberte **OK**.

   ![Nová cloudová aplikace](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > Pokud nevidíte kategorii **cloudové** šablony nebo šablonu **cloudové služby Azure** , musíte nainstalovat **vývojovou úlohu Azure** pro Visual Studio 2017. Kliknutím na odkaz **otevřít instalační program pro Visual Studio** v levé dolní části dialogového okna **nový projekt** otevřete instalační program pro Visual Studio. Vyberte úlohu **vývoje Azure** a pak kliknutím na tlačítko **změnit** spusťte instalaci úlohy.
   >
   > ![Úlohy vývoje Azure v Instalační program pro Visual Studio](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. V dialogovém okně **nová Microsoft Azure cloudová služba** vyberte **Webová role ASP.NET** a kliknutím na tlačítko > přidejte do projektu roli. Vyberte **OK**.

   ![Přidat webovou roli ASP.NET](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. V dialogovém okně **Nová webová aplikace v ASP.NET – WebRole1** vyberte šablonu **MVC** a pak vyberte **OK**.

   ![Přidat MVC a webové rozhraní API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. V **Průzkumník řešení**otevřete soubor *Diagnostics. wadcfgx* pod **WebRole1**.

   ![Průzkumník řešení Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. Nahraďte obsah souboru následující konfigurací a uložte soubor:

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. Otevřete **konzolu Správce balíčků** z **nástrojů** > **Správce balíčků NuGet**. Zadáním následujících příkazů nainstalujte nejnovější verzi nástroje Signaler a balíček nástrojů pro signalizaci:

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. Nakonfigurujte aplikaci tak, aby při spuštění nebo recyklaci do instance role instalovala čítače výkonu signálu. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **WebRole1** a vyberte **Přidat** > **Nová složka**. Pojmenujte nové *spuštění*složky.

   ![Přidat složku po spuštění](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. Zkopírujte soubor *Signal. exe* (přidaný do balíčku **Microsoft. ASPNET. signaler. util** ) z \<složky projektu >/SignalRPerfCounters/Packages/Microsoft.ASPNET.SignalR.utils.\<verze >/Tools do složky *po spuštění* , kterou jste vytvořili v předchozím kroku.

11. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku *po spuštění* a vyberte **Přidat** > **existující položku**. V dialogovém okně, které se zobrazí, vyberte možnost *signaler. exe* a vyberte **Přidat**.

    ![Přidat Signal. exe do projektu](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. Pravým tlačítkem myši klikněte na složku *po spuštění* , kterou jste vytvořili. Vyberte **přidat** > **novou položku**. Vyberte uzel **Obecné** , vyberte **textový soubor**a pojmenujte novou položku *SignalRPerfCounterInstall. cmd*. Tento soubor příkazů nainstaluje do webové role čítače výkonu signálu.

    ![Vytvořit instalační dávkový soubor čítače výkonu signál](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. Když Visual Studio vytvoří soubor *SignalRPerfCounterInstall. cmd* , automaticky se otevře v hlavním okně. Obsah souboru nahraďte následujícím skriptem a pak soubor uložte a zavřete. Tento skript provede *signál. exe*, který přidá čítače výkonu signalizace do instance role.

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. V **Průzkumník řešení**vyberte soubor *signaler. exe* . Ve **vlastnostech**souboru nastavte **Kopírovat do výstupního adresáře** na **Kopírovat vždy**.

    ![Nastavit kopírovat do výstupního adresáře na vždycky kopírovat](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. Opakujte předchozí krok pro soubor *SignalRPerfCounterInstall. cmd* .

16. Klikněte pravým tlačítkem myši na soubor *SignalRPerfCounterInstall. cmd* a vyberte možnost **otevřít v programu**. V dialogovém okně, které se zobrazí, vyberte **binární editor** a vyberte **OK**.

    ![Otevřít v binárním editoru](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. V binárním editoru vyberte v souboru všechny úvodní bajty a odstraňte je. Uložte soubor a zavřete ho.

    ![Odstranit úvodní bajty](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. Otevřete *ServiceDefinition. csdef* a přidejte úlohu po spuštění, která při spuštění služby spustí soubor *SignalrPerfCounterInstall. cmd* :

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. Otevřete `Views/Shared/_Layout.cshtml` a z konce souboru odeberte skript sady jQuery.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. Přidejte klienta JavaScriptu, který nepřetržitě zavolá metodu `increment` na serveru. Otevřete `Views/Home/Index.cshtml` a nahraďte obsah následujícím kódem:

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. Vytvořte novou složku v projektu **WebRole1** s názvem *Centers*. Klikněte pravým tlačítkem na složku *Centers* v **Průzkumník řešení** a vyberte **Přidat** > **Nová položka**. V dialogovém okně **Přidat novou položku** vyberte kategorii **signalizace** **webového** > a pak vyberte šablonu položky **třídy centra (v2) pro rozbočovače signálu** . Zadejte název nového centra *MyHub.cs* a vyberte **Přidat**.

    ![Přidání třídy centra signalizace do složky Center v dialogovém okně Přidat novou položku](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs* se automaticky otevře v hlavním okně. Nahraďte obsah následujícím kódem a pak soubor uložte a zavřete:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank. exe](signalr-connection-density-testing-with-crank.md)* je nástroj pro testování hustoty připojení, který je k dispozici v základu signálu. Vzhledem k tomu, že Crank vyžaduje trvalé připojení, přidejte ho do svého webu pro použití při testování. Přidejte novou složku do projektu **WebRole1** s názvem *PersistentConnections*. Klikněte pravým tlačítkem na tuto složku a vyberte **přidat** > **třídy**. Pojmenujte nový soubor třídy *MyPersistentConnections.cs* a vyberte **Přidat**.

24. Visual Studio otevře soubor *MyPersistentConnections.cs* v hlavním okně. Nahraďte obsah následujícím kódem a pak soubor uložte a zavřete:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. Pomocí třídy `Startup` se objekty signalizace spouštějí při spuštění OWIN. Otevřete nebo vytvořte *Startup.cs* a nahraďte obsah následujícím kódem:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    V kódu výše atribut `OwinStartup` označuje tuto třídu jako počáteční OWIN. Metoda `Configuration` spustí signál.

26. Otestujte aplikaci v Microsoft Azure Emulator stisknutím klávesy **F5**.

    > [!NOTE]
    > Pokud narazíte na **FileLoadException** na **MapSignalR**, změňte přesměrování vazby v *souboru Web. config* na následující:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. Počkejte asi jednu minutu. V aplikaci Visual Studio otevřete okno nástroje Průzkumník cloudu (**zobrazit** > **Průzkumník cloudu**) a rozbalte cestu `(Local)/Storage Accounts/(Development)/Tables`. Dvakrát klikněte na **WADPerformanceCountersTable**. V datech tabulky by se měly zobrazit čítače signalizace. Pokud tabulku nevidíte, možná budete muset znovu zadat přihlašovací údaje Azure Storage. Možná budete muset vybrat tlačítko **aktualizovat** , aby se zobrazila tabulka v **Průzkumníku cloudu** , nebo kliknutím na tlačítko **aktualizovat** v okně Otevřít tabulku zobrazit data v tabulce.

    ![Výběr tabulky čítače výkonu WAD v Průzkumníkovi cloudu sady Visual Studio](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![Zobrazuje se počítadla shromážděná v tabulce čítače výkonu WAD.](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. Pokud chcete otestovat aplikaci v cloudu, aktualizujte soubor **ServiceConfiguration. Cloud. cscfg** a nastavte `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` na platný připojovací řetězec Azure Storage účtu.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. Nasaďte aplikaci do svého předplatného Azure. Podrobnosti o tom, jak nasadit aplikaci do Azure, najdete v tématu [jak vytvořit a nasadit cloudovou službu](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).

30. Počkejte několik minut. V **Průzkumníku cloudu**vyhledejte účet úložiště, který jste nakonfigurovali výše, a vyhledejte v něm tabulku `WADPerformanceCountersTable`. V datech tabulky by se měly zobrazit čítače signalizace. Pokud tabulku nevidíte, možná budete muset znovu zadat přihlašovací údaje Azure Storage. Možná budete muset vybrat tlačítko **aktualizovat** , aby se zobrazila tabulka v **Průzkumníku cloudu** , nebo kliknutím na tlačítko **aktualizovat** v okně Otevřít tabulku zobrazit data v tabulce.

Pro původní obsah použitý v tomto kurzu se speciálním obsahem myslíme na [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) .
