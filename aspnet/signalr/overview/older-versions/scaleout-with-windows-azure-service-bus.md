---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: Horizontální navýšení signálu pomocí Azure Service Bus (Signal 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558413"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a>Škálování aplikace SignalR službou Azure Service Bus (SignalR 1.x)

[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

V tomto kurzu nasadíte aplikaci signalizace do webové role Windows Azure pomocí Service Busho opětovného plánování pro distribuci zpráv do každé instance role.

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

Požadavky:

- Účet služby Windows Azure.
- [Sada Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).
- Visual Studio 2012.

[Pro Service Bus systému Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)verze 1,1 je služba replánování Service Bus taky kompatibilní. Není ale kompatibilní s verzí 1,0 Service Bus pro Windows Server.

## <a name="pricing"></a>Ceny

Service Bus pro nové plánování používá témata k posílání zpráv. Nejnovější informace o cenách najdete v tématu [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/). V době psaní tohoto textu můžete odesílat 1 000 000 zpráv za měsíc za méně než $1. Metoda replánování pošle zprávu služby Service Bus pro každé vyvolání metody centra signalizace. K dispozici jsou také některé řídicí zprávy pro připojení, odpojení, spojování nebo opouštíní skupin a tak dále. Ve většině aplikací se většina přenosů zpráv bude vyvoláním metody rozbočovače.

## <a name="overview"></a>Přehled

Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.

1. K vytvoření nového oboru názvů Service Bus použijte Azure Portal Windows.
2. Přidejte tyto balíčky NuGet do vaší aplikace: 

    - [Microsoft. AspNet. Signaler](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. AspNet. Signaler. ServiceBus](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. Vytvořte aplikaci signalizace.
4. Přidejte následující kód do Global. asax ke konfiguraci rozhraní pro naplánování: 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

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

V dialogovém okně **Nová cloudová služba Microsoft Azure** vyberte webová role ASP.NET MVC 4. Kliknutím na tlačítko se šipkou doprava ( **&gt;** ) přidáte roli do svého řešení.

Najeďte myší na novou roli, aby se ikona tužky zobrazila. Kliknutím na tuto ikonu přejmenujete roli. Pojmenujte roli "SignalRChat" a klikněte na tlačítko **OK**.

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

V průvodci **vytvořením nového projektu ASP.NET MVC 4** vyberte **internetovou aplikaci**. Klikněte na tlačítko **OK**. Průvodce projektem vytvoří dva projekty:

- ChatService: Tento projekt je aplikace systému Windows Azure. Definuje role Azure a další možnosti konfigurace.
- SignalRChat: Tento projekt je váš projekt ASP.NET MVC 4.

## <a name="create-the-signalr-chat-application"></a>Vytvoření aplikace pro chat signálu

Chcete-li vytvořit aplikaci Chat, postupujte podle kroků v kurzu [Začínáme s nástrojem Signal and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).

K instalaci požadovaných knihoven použijte NuGet. V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně **konzoly Správce balíčků** zadejte následující příkazy:

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

Použijte možnost `-ProjectName` k instalaci balíčků do projektu ASP.NET MVC místo do projektu Windows Azure.

## <a name="configure-the-backplane"></a>Konfigurovat plán

Do souboru Global. asax vaší aplikace přidejte následující kód:

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

Nyní potřebujete získat připojovací řetězec služby Service Bus. V Azure Portal vyberte obor názvů služby Service Bus, který jste vytvořili, a klikněte na ikonu přístupového klíče.

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

Zkopírujte připojovací řetězec do schránky a vložte ho do proměnné *ConnectionString* .

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Nasazení do Azure

V Průzkumník řešení rozbalte složku **role** v projektu ChatService.

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

Klikněte pravým tlačítkem na roli SignalRChat a vyberte **vlastnosti**. Vyberte kartu **Konfigurace** . V části **instance** vyberte 2. Velikost virtuálního počítače taky můžete nastavit na **velmi malou**.

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

Uložte změny.

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt ChatService. Vyberte **Publikovat**.

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

Pokud publikujete do Windows Azure poprvé, musíte si stáhnout svoje přihlašovací údaje. V průvodci **publikování** klikněte na Přihlásit se a stáhněte přihlašovací údaje. Zobrazí se výzva, abyste se přihlásili k Windows Azure Portal a stáhli soubor nastavení publikování.

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

Klikněte na **importovat** a vyberte soubor nastavení publikování, který jste stáhli.

Klikněte na **Další**. V dialogovém okně **publikovat nastavení** v části **cloudová služba**Vyberte cloudovou službu, kterou jste vytvořili dříve.

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

Klikněte na **Publikovat**. Nasazení aplikace a spuštění virtuálních počítačů může trvat několik minut.

Nyní když spouštíte aplikaci Chat, instance rolí komunikují prostřednictvím Azure Service Bus pomocí Service Busho tématu. Téma je fronta zpráv, která umožňuje více odběratelů.

Znovu naplánování automaticky vytvoří téma a odběry. Chcete-li zobrazit odběry a aktivity zprávy, otevřete Azure Portal, vyberte obor názvů Service Bus a klikněte na tlačítko "témata".

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

Zobrazení aktivity zprávy na řídicím panelu může trvat několik minut.

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

Návěstí řídí dobu života tématu. Pokud je vaše aplikace nasazena, nepokoušejte se ručně odstranit témata nebo změnit nastavení v tématu.
