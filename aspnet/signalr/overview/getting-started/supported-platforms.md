---
uid: signalr/overview/getting-started/supported-platforms
title: Podporované platformy | Microsoft Docs
author: bradygaster
description: Tento článek popisuje, které klienty a servery podporuje Signal.
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558630"
---
# <a name="supported-platforms"></a>Podporované platformy

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek popisuje, které klienty a servery podporuje Signal. 
> 
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
> 
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

Signalizace se podporuje v rámci nejrůznějších konfigurací serverů a klientů. Kromě toho každá možnost přenosu má sadu vlastních požadavků. Pokud požadavky na systém pro přenos nejsou k dispozici, je signál k řádnému převzetí služeb při selhání na jiné přenosy. Další informace o přenosech, které signalizace podporuje, najdete v tématu [přenosy a záložní](introduction-to-signalr.md#transports)služby.

## <a name="server-system-requirements"></a>Požadavky na systém serveru

Komponentu serveru signalizace lze hostovat na nejrůznějších konfiguracích serveru. Tato část popisuje podporované verze operačních systémů, rozhraní .NET Framework, serveru Internet Information Server a další součásti.

### <a name="supported-server-operating-systems"></a>Podporované serverové operační systémy

Součást serveru signalizace může být hostována v následujících serverech nebo klientských operačních systémech. Všimněte si, že pro signalizaci, že se vyžaduje použití WebSockets, Windows Server 2012, Windows Server 2016 nebo Windows 8 (WebSocket se dá použít na webech Windows Azure, pokud je verze rozhraní .NET Framework lokality nastavená na 4,5 a v lokalitě je povolená možnost webové sokety Konfigurační stránka).

- Windows Server 2016
- Windows Server 2012
- Windows Server 2008 r2
- Windows 10
- Windows 8
- Windows 7
- Windows Azure

### <a name="supported-server-net-framework-version"></a>Podporovaná verze serveru .NET Framework

Signál 2 je podporován pouze v .NET Framework 4,5. V části [Doporučené aktualizace](#updates) najdete informace o aktualizacích, které zlepšují spolehlivost, kompatibilitu, stabilitu a výkon.

### <a name="supported-server-iis-versions"></a>Podporované verze serveru IIS

V případě, že je signál hostovaný ve službě IIS, jsou podporovány následující verze. Počítejte s tím, že pokud se používá klientský operační systém, například pro vývoj (Windows 8 nebo Windows 7), neměli byste používat úplné verze služby IIS nebo Cassini, protože by to znamenalo omezení 10 současných připojení, které se dosáhne velmi rychle od připojení. jsou přechodný a často znovu navázány a nejsou okamžitě uvolněny, pokud už nebudete používat. V klientských operačních systémech by se měla použít IIS Express.

Všimněte si také, že pro signál k použití WebSocket, IIS 8 nebo IIS 8 Express se musí použít server se systémem Windows 8, Windows Server 2012 nebo novějším a v IIS musí být povolený protokol WebSocket. Informace o tom, jak povolit WebSocket ve službě IIS, najdete v tématu [Podpora protokolu WebSocket v iis 8,0](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).

- Služba IIS 8 nebo IIS 8 Express.
- IIS 7 a 7,5. Vyžaduje se podpora [rozšiřujících adres URL](https://support.microsoft.com/kb/980368) .
- Služba IIS musí běžet v integrovaném režimu. Klasický režim není podporován. V případě, že je služba IIS spuštěna v klasickém režimu pomocí přenosu událostí odeslaných serverem, může dojít ke zpoždění zpráv po dobu až 30 sekund.
- Hostující aplikace musí běžet v režimu úplného vztahu důvěryhodnosti.

## <a name="client-system-requirements"></a>Požadavky na systém klienta

Signalizaci lze použít na nejrůznějších klientských platformách. Tato část popisuje systémové požadavky na používání nástroje Signal ve webových prohlížečích, desktopových aplikacích pro Windows, aplikacích Silverlight a mobilních zařízeních.

### <a name="web-browsers"></a>Webové prohlížeče

Signalizace se dá použít v nejrůznějších webových prohlížečích, ale obvykle se podporují jenom nejnovější dvě verze.

Aplikace, které používají signál v prohlížečích, musí používat jQuery verze 1.6.4 nebo hlavní pozdější verze (například 1.7.2, 1.8.2 nebo 1.9.1).

Signalizaci lze použít v následujících prohlížečích:

- Microsoft Internet Explorer verze 8, 9, 10 a 11. Podporují se moderní, desktopové a mobilní verze.
- Mozilla Firefox: aktuální verze-1, verze Windows i Mac.
- Google Chrome: aktuální verze-1, verze Windows i Mac.
- Safari: aktuální verze-1, verze Mac a iOS.
- Opera: aktuální verze-1, jenom Windows.
- Prohlížeč Android

Kromě vyžadování určitých prohlížečů mají různé přenosy, které signalizace používá, své vlastní požadavky. Následující přenosy jsou podporovány v následujících konfiguracích:

<a id="browser"></a>

**Požadavky na přenos ve webovém prohlížeči**

| Přenos | Internet Explorer | Chrome (Windows nebo iOS) | Firefox | Safari (OSX nebo iOS) | Android |
| --- | --- | --- | --- | --- | --- |
| WebSockets | 10+ | aktuální – 1 | aktuální – 1 | aktuální – 1 | neuvedeno |
| Události odeslané serverem | neuvedeno | aktuální – 1 | aktuální – 1 | aktuální – 1 | neuvedeno |
| ForeverFrame | 8+ | neuvedeno | neuvedeno | neuvedeno | 4.1 |
| Dlouhé cyklické dotazování | 8+ | aktuální – 1 | aktuální – 1 | aktuální – 1 | 4.1 |

\*: 6 + vyžaduje se pro plnou funkčnost.

#### <a name="unsupported-browsers"></a>Nepodporované prohlížeče

I když *může* být signál vyzkoušený bez závažných problémů ve starších verzích prohlížeče, nemusíme aktivně testovat signál v nich a obecně neopravují chyby, které se v nich můžou objevit.

### <a name="windows-desktop-and-silverlight-applications"></a>Aplikace Windows Desktop a Silverlight

Kromě spuštění ve webovém prohlížeči je možné přidat signál jako hostitele samostatného klienta systému Windows nebo aplikací Silverlight. Aplikace signalizace desktopu a Silverlightu pro Windows mají následující požadavky na systém.

- Aplikace používající rozhraní .NET 4 jsou podporovány v systému Windows XP SP3 nebo novějším.
- Aplikace používající .NET Framework 4,5 jsou podporovány v systému Windows Vista nebo novějším.

Kromě požadavků na operační systém a rozhraní .NET Framework mají přenosy dostupné i pro signál. Následující přenosy jsou podporovány v následujících konfiguracích:

**Požadavky na systém Windows Desktop a Silverlight pro přenos**

| Přenos | Aplikace v .NET | Silverlight |
| --- | --- | --- |
| Webové sokety | Windows 8 + a .NET 4.5 + | neuvedeno |
| Snímek navždy | neuvedeno | neuvedeno |
| Události odeslané serverem | .NET 4+ | 5+ |
| Dlouhé cyklické dotazování | .NET 4+ | 5+ |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Aplikace pro Windows Store a Windows Phone

Signalizaci lze použít v aplikacích pro Windows Store a Windows Phone 8. Následující přenosy jsou podporovány v následujících konfiguracích:

**Požadavky na přenos pro Windows Store a Windows Phone**

| Přenos | Windows Store/.NET | Windows Store/JavaScript | Windows Phone/IE | Windows Phone/.NET |
| --- | --- | --- | --- | --- |
| WebSockets | neuvedeno | Win8 + | 8+ | neuvedeno |
| Snímek navždy | neuvedeno | Win8 + | 7.5+ | neuvedeno |
| Události odeslané serverem | Win8 + | neuvedeno | neuvedeno | 8+ |
| Dlouhé cyklické dotazování | Win8 + | Win8 + | 7.5+ | 8+ |

<a id="updates"></a>

## <a name="recommended-updates"></a>Doporučené aktualizace

Pro servery signalizace se doporučují tyto aktualizace:

- Aktualizace pro .NET Framework 4,5 je k dispozici [zde](https://support.microsoft.com/kb/2750149).
- Microsoft bude pravidelně vydávat opravy QFE pro ASP.NET. Ty by se měly použít jako dostupné.
