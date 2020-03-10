---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: Testování hustoty připojení signálem pomocí Crank | Microsoft Docs
author: bradygaster
description: Testování hustoty připojení nástrojem Crank
ms.author: bradyg
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 901e039fbb81651ed18d560c99745b7e7f716e01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558336"
---
# <a name="signalr-connection-density-testing-with-crank"></a>Testování hustoty připojení nástrojem Crank

tím, že [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek popisuje, jak používat nástroj Crank k otestování aplikace s více simulovanými klienty.

Jakmile vaše aplikace běží ve svém hostitelském prostředí (buď webová role Azure, IIS, nebo v místním prostředí s využitím Owin), můžete otestovat reakci aplikace na vysokou úroveň hustoty připojení pomocí nástroje Crank. Hostující prostředí může být server Internetová informační služba (IIS), hostitel Owin nebo webová role Azure. (Poznámka: čítače výkonu nejsou k dispozici v Azure App Service Web Apps, takže nebudete moci získat údaje o výkonu z testu hustoty připojení.)

Hustota připojení odkazuje na počet souběžných připojení TCP, která lze na serveru vytvořit. Každé připojení TCP má za následek svoji vlastní režii a otevření velkého počtu nečinných připojení nakonec vytvoří kritické místo pro paměť.

[Základ signálu](https://github.com/signalr/signalr) obsahuje nástroj pro testování zatížení nazvaný **Crank**. Nejnovější verzi Crank najdete ve [vývojářské větvi](https://github.com/SignalR/signalr/tree/dev) na GitHubu. Archiv zip větve pro vývojovou větev si můžete stáhnout [tady](https://github.com/SignalR/SignalR/archive/dev.zip).

Crank se dá použít k plnému sytosti paměti serveru, aby se mohl vypočítat celkový počet nečinných připojení na hardwaru serveru. Alternativně můžete také použít Crank k zátěži testu serveru s určitou velikostí paměti tím, že provedete navýšení připojení, dokud není dosaženo konkrétního počtu nebo určité prahové hodnoty paměti.

Při testování je důležité používat vzdálené klienty, abyste se vyhnuli jakékoli konkurenci pro prostředky (tj. připojení TCP a paměť). Monitorujte klienty, abyste se ujistili, že nedošlo k žádným kritickým bodům, které by mohly zabránit serveru v dosažení plné kapacity (paměti nebo procesoru). Možná budete muset zvýšit počet klientů, aby bylo možné plně načíst Server.

### <a name="running-a-connection-density-test"></a>Spuštění testu hustoty připojení

Tato část popisuje kroky potřebné ke spuštění testu hustoty připojení v aplikaci signalizace.

1. Stáhněte a sestavte [vývojovou větev základu signálu](https://github.com/SignalR/SignalR/archive/dev.zip). Na příkazovém řádku přejděte do složky &lt;Project Directory&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug.
2. Nasaďte aplikaci do svého zamýšleného hostitelského prostředí. Poznamenejte si koncový bod, který vaše aplikace používá; například v aplikaci vytvořené v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md)je koncový bod `http://<yourhost>:8080/signalr`.
3. Nainstalujte [čítače výkonu signálu](signalr-performance.md#perfcounters) na server. Pokud je vaše aplikace spuštěná v Azure, přečtěte si téma [použití čítačů výkonu signálů ve webové roli Azure](using-signalr-performance-counters-in-an-azure-web-role.md).

Po stažení a sestavení základu kódu a nainstalování čítačů výkonu na hostitele lze nástroj příkazového řádku Crank najít ve složce `src\Microsoft.AspNet.SignalR.Crank\bin\Debug`.

K dispozici jsou možnosti pro nástroj Crank:

- **/?** : Zobrazuje obrazovku help. Dostupné možnosti se zobrazí také v případě, že je parametr **adresy URL** vynechán.
- **/URL**: adresa URL pro připojení k signalizaci. Tento parametr je povinný. Pro aplikaci signalizace, která používá výchozí mapování, bude cesta končit "/SignalR".
- **/Transport**: název použitého přenosu. Výchozí hodnota je `auto`, ve kterém se vybere nejlepší dostupný protokol. Mezi možnosti patří `WebSockets`, `ServerSentEvents`a `LongPolling` (`ForeverFrame` není možnost pro Crank, protože se používá klient .NET namísto použití aplikace Internet Explorer). Další informace o tom, jak signál vybírá přenosy, najdete v tématu [přenosy a záložní](../getting-started/introduction-to-signalr.md#transports)služby.
- **/BatchSize**: počet klientů přidaných do každé dávky. Výchozí hodnota je 50.
- **/ConnectInterval**: interval v milisekundách mezi přidáváním připojení. Výchozí hodnota je 500.
- **/Connections**: počet připojení použitých k načtení a otestování aplikace. Výchozí hodnota je 100 000.
- **/ConnectTimeout**: časový limit v sekundách před přerušením testu. Výchozí hodnota je 300.
- **MinServerMBytes**: minimální dostupný server megabajtů. Výchozí hodnota je 500.
- **SendBytes**: velikost datové části odeslané na server v bajtech. Výchozí hodnota je 0.
- **SendInterval**: zpoždění v milisekundách mezi zprávami na server. Výchozí hodnota je 500.
- **SendTimeout**: časový limit v milisekundách pro zprávy na server. Výchozí hodnota je 300.
- **ControllerUrl**: adresa URL, kam bude jeden klient hostovat centrum kontrolérů. Výchozí hodnota je null (žádné centrum řadičů). Centrum kontrolérů se spustí při spuštění relace Crank; mezi centrem kontrolérů a Crank se neprovádí žádný další kontakt.
- **NumClients**: počet simulovaných klientů, které se mají připojit k aplikaci. Výchozí hodnota je jedna.
- **Logfile**: název souboru protokolu pro testovací běh. Výchozí formát je `crank.csv`.
- **SampleInterval**: čas v milisekundách mezi ukázkami čítače výkonu. Výchozí hodnota je 1000.
- **SignalRInstance**: název instance pro čítače výkonu na serveru. Ve výchozím nastavení se použije stav připojení klienta.

### <a name="example"></a>Příklad

Následující příkaz otestuje web s názvem `pfsignalr` v Azure, který hostuje aplikaci na portu 8080 s centrem s názvem "ControllerHub" s použitím připojení 100.

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
