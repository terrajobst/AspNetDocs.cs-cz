---
uid: signalr/overview/performance/scaleout-with-redis
title: Škálování signálu pomocí Redis | Microsoft Docs
author: bradygaster
description: Verze softwaru používané v tomto tématu Visual Studio 2013 k předchozím verzím tohoto tématu v předchozích verzích rozhraní .NET 4,5 Signaler verze 2, kde najdete informace o dřívějších verzích...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579224"
---
# <a name="signalr-scaleout-with-redis"></a>Šklálování aplikace SignalR službou Redis

o [Jan Wasson](https://github.com/MikeWasson)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Signaler verze 2,4
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

V tomto kurzu použijete [Redis](http://redis.io/) k distribuci zpráv v aplikaci signalizace, která je nasazená ve dvou samostatných INSTANCÍCH služby IIS.

Redis je úložiště hodnot klíč-hodnota v paměti. Podporuje také systém zasílání zpráv s modelem publikování/odběru. Redis pro vyřízení signálu používá funkci Pub/sub k posílání zpráv na jiné servery.

![](scaleout-with-redis/_static/image1.png)

Pro tento kurz budete používat tři servery:

- Dva servery se systémem Windows, které použijete k nasazení aplikace Signal.
- Jeden server se systémem Linux, který použijete ke spuštění Redis. Pro snímky obrazovky v tomto kurzu jsem používal Ubuntu 12,04 TLS.

Pokud nemáte tři fyzické servery k použití, můžete vytvořit virtuální počítače v prostředí Hyper-V. Další možností je vytvořit virtuální počítače v Azure.

I když tento kurz používá oficiální implementaci Redis, existuje taky [Port Windows Redis](https://github.com/MSOpenTech/redis) z MSOpenTech. Nastavení a konfigurace se liší, ale v opačném případě se jedná o stejné kroky.

> [!NOTE]
>
> Škálování signálu pomocí Redis nepodporuje clustery Redis.

## <a name="overview"></a>Přehled

Než se dostanete k podrobnému kurzu, tady je rychlý přehled toho, co budete dělat.

1. Nainstalujte Redis a spusťte server Redis.
2. Přidejte tyto balíčky NuGet do vaší aplikace:

    - [Microsoft. AspNet. Signaler](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. AspNet. Signaler. StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. Vytvořte aplikaci signalizace.
4. Přidáním následujícího kódu do Startup.cs nakonfigurujte schéma pro replánování:

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Ubuntu na Hyper-V

Pomocí technologie Windows Hyper-V můžete snadno vytvořit virtuální počítač s Ubuntu na Windows serveru.

Stáhněte si Ubuntu ISO z [http://www.ubuntu.com](http://www.ubuntu.com/).

V Hyper-V přidejte nový virtuální počítač. V kroku **připojit virtuální pevný disk** vyberte možnost **vytvořit virtuální pevný disk**.

![](scaleout-with-redis/_static/image2.png)

V kroku **Možnosti instalace** vyberte **soubor obrázku (. ISO)** , klikněte na tlačítko **Procházet**a přejděte do Ubuntu instalace ISO.

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>Nainstalovat Redis

Podle pokynů v části [http://redis.io/download](http://redis.io/download) Stáhněte a sestavte Redis.

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

Tím se vytvoří binární soubory Redis v adresáři `src`.

Ve výchozím nastavení Redis nevyžaduje heslo. Chcete-li nastavit heslo, upravte soubor `redis.conf`, který je umístěn v kořenovém adresáři zdrojového kódu. (Před úpravou! vytvořte záložní kopii souboru) Přidejte následující direktivu pro `redis.conf`:

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

Nyní spusťte server Redis:

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

Otevřete port 6379, což je výchozí port, na kterém Redis naslouchá. (V konfiguračním souboru můžete změnit číslo portu.)

## <a name="create-the-signalr-application"></a>Vytvoření aplikace Signal

Pomocí některého z těchto kurzů vytvořte aplikaci signalizace:

- [Začínáme se signálem 2,0](../getting-started/tutorial-getting-started-with-signalr.md)
- [Začínáme s nástrojem Signal 2,0 a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

V dalším kroku změníme aplikaci Chat, aby podporovala horizontální navýšení kapacity pomocí Redis. Nejprve do svého projektu přidejte balíček NuGet `Microsoft.AspNet.SignalR.StackExchangeRedis`. V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

Pak otevřete soubor Startup.cs. Do metody **Konfigurace** přidejte následující kód:

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "Server" je název serveru, na kterém běží Redis.
- *port* je číslo portu.
- heslo je heslo, které jste definovali v souboru Redis. conf.
- "AppName" je libovolný řetězec. Signal vytvoří Redis kanál pro publikování a podkanál s tímto názvem.

Příklad:

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>Nasazení a spuštění aplikace

Připraví instance Windows serveru pro nasazení aplikace Signal.

Přidejte roli IIS. Zahrňte funkce pro vývoj aplikací, včetně protokolu WebSocket.

![](scaleout-with-redis/_static/image5.png)

Zahrňte také službu správy (v seznamu "nástroje pro správu").

![](scaleout-with-redis/_static/image6.png)

**Nainstalujte Nasazení webu 3,0.** Spustíte-li správce služby IIS, zobrazí se výzva k instalaci webové platformy společnosti Microsoft nebo můžete [instalační program stáhnout](https://go.microsoft.com/fwlink/?LinkId=255386). V instalačním programu platformy vyhledejte Nasazení webu a nainstalujte Nasazení webu 3,0

![](scaleout-with-redis/_static/image7.png)

Ověřte, zda je spuštěna služba webové správy. V takovém případě službu spusťte. (Pokud se služba webové správy nezobrazuje v seznamu služeb systému Windows, ujistěte se, že jste nainstalovali službu správy při přidání role služby IIS.)

Ve výchozím nastavení služba webové správy naslouchá na portu TCP 8172. V bráně Windows Firewall vytvořte nové příchozí pravidlo povolující přenosy TCP na portu 8172. Další informace najdete v tématu [Konfigurace pravidel brány firewall](https://technet.microsoft.com/library/dd448559(WS.10).aspx). (Pokud virtuální počítače hostují v Azure, můžete to provést přímo v Azure Portal. Přečtěte si téma [nastavení koncových bodů na virtuální počítač](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)

Nyní jste připraveni nasadit projekt sady Visual Studio z vývojového počítače na server. V Průzkumník řešení klikněte pravým tlačítkem na řešení a pak klikněte na **publikovat**.

Podrobnější dokumentaci k nasazení webu najdete v tématu [Mapa obsahu nasazení webu pro Visual Studio a ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).

Pokud nasadíte aplikaci na dva servery, můžete každou instanci otevřít v samostatném okně prohlížeče a podívat se, že každý z nich obdrží zprávy signálu. (Samozřejmě v produkčním prostředí budou dva servery za nástroj pro vyrovnávání zatížení.)

![](scaleout-with-redis/_static/image8.png)

Pokud jste zajímá zprávy, které se odesílají do Redis, můžete použít klienta **Redis-CLI** , který se instaluje s Redis.

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
