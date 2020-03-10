---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Škálování signálu pomocí Azure Service Bus | Microsoft Docs
author: bradygaster
description: Verze softwaru používané v tomto tématu Visual Studio 2013 v předchozích verzích tohoto tématu v části Signaler 4,5 verze 2 tohoto tématu, pro verzi Signaler 1. x tohoto tématu,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579175"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a>Škálování aplikace SignalR službou Azure Service Bus

[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

V tomto kurzu nasadíte aplikaci signalizace do webové role Windows Azure pomocí Service Busho opětovného plánování pro distribuci zpráv do každé instance role. (Můžete také použít Service Bus pro naplánování pomocí [Web Apps v Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

Požadavky:

- Účet služby Windows Azure.
- [Sada Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).
- Visual Studio 2012 nebo 2013.

[Pro Service Bus systému Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)verze 1,1 je služba replánování Service Bus taky kompatibilní. Není ale kompatibilní s verzí 1,0 Service Bus pro Windows Server.

## <a name="pricing"></a>Ceny

Service Bus pro nové plánování používá témata k posílání zpráv. Nejnovější informace o cenách najdete v tématu [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/). V době psaní tohoto textu můžete odesílat 1 000 000 zpráv za měsíc za méně než $1. Metoda replánování pošle zprávu služby Service Bus pro každé vyvolání metody centra signalizace. K dispozici jsou také některé řídicí zprávy pro připojení, odpojení, spojování nebo opouštíní skupin a tak dále. Ve většině aplikací se většina přenosů zpráv bude vyvoláním metody rozbočovače.

## <a name="overview"></a>Přehled

Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.

1. K vytvoření nového oboru názvů Service Bus použijte Azure Portal Windows.
2. Přidejte tyto balíčky NuGet do vaší aplikace: 

    - [Microsoft. AspNet. Signaler](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. ASPNET. Signal. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) nebo [Microsoft. ASPNET. Signal. ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)
3. Vytvořte aplikaci signalizace.
4. Přidáním následujícího kódu do Startup.cs nakonfigurujte schéma pro replánování: 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

Tento kód nakonfiguruje pro replánování výchozí hodnoty pro [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) a [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx). Informace o změně těchto hodnot najdete v tématu [výkon signalizace: metriky škálování](signalr-performance.md#scaleout_metrics).

Pro každou aplikaci vyberte jinou hodnotu "soubor YourAppName". Nepoužívejte stejnou hodnotu napříč více aplikacemi.

## <a name="create-the-azure-services"></a>Vytvoření služeb Azure

Vytvořte cloudovou službu, jak je popsáno v tématu [jak vytvořit a nasadit cloudovou službu](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy). Postupujte podle kroků v části Postup: vytvoření cloudové služby pomocí příkazu rychle vytvořit. Pro tento kurz nemusíte nahrávat certifikát.

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

Vytvořte nový obor názvů Service Bus, jak je popsáno v [tématu Jak používat Service Bus témata/předplatná](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions). Postupujte podle kroků v části "Vytvoření oboru názvů služby".

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> Ujistěte se, že jste vybrali stejnou oblast pro cloudovou službu a obor názvů Service Bus.

## <a name="create-the-visual-studio-project"></a>Vytvoření projektu sady Visual Studio

Spusťte Visual Studio. V nabídce **Soubor** klikněte na **Nový projekt**.

V dialogovém okně **Nový projekt** rozbalte položku **vizuál C#** . V části **Nainstalované šablony**vyberte **Cloud** a potom vyberte **cloudová služba Windows Azure**. Ponechte výchozí .NET Framework 4,5. Pojmenujte aplikaci ChatService a klikněte na **OK**.

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

V dialogovém okně **Nová cloudová služba Microsoft Azure** vyberte ASP.NET webová role. Kliknutím na tlačítko se šipkou doprava ( **&gt;** ) přidáte roli do svého řešení.

Najeďte myší na novou roli, aby se ikona tužky zobrazila. Kliknutím na tuto ikonu přejmenujete roli. Pojmenujte roli "SignalRChat" a klikněte na tlačítko **OK**.

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

V dialogovém okně **Nový projekt ASP.NET** vyberte **MVC**a klikněte na OK.

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

Průvodce projektem vytvoří dva projekty:

- ChatService: Tento projekt je aplikace systému Windows Azure. Definuje role Azure a další možnosti konfigurace.
- SignalRChat: Tento projekt je váš projekt ASP.NET MVC 5.

## <a name="create-the-signalr-chat-application"></a>Vytvoření aplikace pro chat signálu

Chcete-li vytvořit aplikaci Chat, postupujte podle kroků v kurzu [Začínáme s nástrojem signaler a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

K instalaci požadovaných knihoven použijte NuGet. V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně **konzoly Správce balíčků** zadejte následující příkazy:

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

Použijte možnost `-ProjectName` k instalaci balíčků do projektu ASP.NET MVC místo do projektu Windows Azure.

## <a name="configure-the-backplane"></a>Konfigurovat plán

Do souboru Startup.cs vaší aplikace přidejte následující kód:

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

Nyní potřebujete získat připojovací řetězec služby Service Bus. V Azure Portal vyberte obor názvů služby Service Bus, který jste vytvořili, a klikněte na ikonu přístupového klíče.

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

Zkopírujte připojovací řetězec do schránky a vložte ho do proměnné *ConnectionString* .

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Nasazení do Azure

V Průzkumník řešení rozbalte složku **role** v projektu ChatService.

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

Klikněte pravým tlačítkem na roli SignalRChat a vyberte **vlastnosti**. Vyberte kartu **Konfigurace** . V části **instance** vyberte 2. Velikost virtuálního počítače taky můžete nastavit na **velmi malou**.

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

Uložte změny.

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt ChatService. Vyberte **Publikovat**.

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

Pokud publikujete do Windows Azure poprvé, musíte si stáhnout svoje přihlašovací údaje. V průvodci **publikování** klikněte na Přihlásit se a stáhněte přihlašovací údaje. Zobrazí se výzva, abyste se přihlásili k Windows Azure Portal a stáhli soubor nastavení publikování.

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

Klikněte na **importovat** a vyberte soubor nastavení publikování, který jste stáhli.

Klikněte na **Další**. V dialogovém okně **publikovat nastavení** v části **cloudová služba**Vyberte cloudovou službu, kterou jste vytvořili dříve.

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

Klikněte na **Publikovat**. Nasazení aplikace a spuštění virtuálních počítačů může trvat několik minut.

Nyní když spouštíte aplikaci Chat, instance rolí komunikují prostřednictvím Azure Service Bus pomocí Service Busho tématu. Téma je fronta zpráv, která umožňuje více odběratelů.

Znovu naplánování automaticky vytvoří téma a odběry. Chcete-li zobrazit odběry a aktivity zprávy, otevřete Azure Portal, vyberte obor názvů Service Bus a klikněte na tlačítko "témata".

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

Zobrazení aktivity zprávy na řídicím panelu může trvat několik minut.

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

Návěstí řídí dobu života tématu. Pokud je vaše aplikace nasazena, nepokoušejte se ručně odstranit témata nebo změnit nastavení v tématu.

## <a name="troubleshooting"></a>Řešení potíží

**System. InvalidOperationException "jedinou podporovanou IsolationLevel je" IsolationLevel. serializovatelný ".**

K této chybě může dojít, pokud je úroveň transakce pro operaci nastavena na jinou hodnotu než `Serializable`. Ověřte, že se neprovádí žádné operace s jinými úrovněmi transakce.
