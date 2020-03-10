---
uid: whitepapers/aspnet-and-iis6
title: Spuštění ASP.NET 1,1 se službou IIS 6,0 | Microsoft Docs
author: rick-anderson
description: Systém Windows Server 2003 zahrnuje službu IIS 6,0 i ASP.NET 1,1. tyto komponenty jsou ve výchozím nastavení zakázány. Tento dokument white paper popisuje, jak povolit IIS 6,0...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523308"
---
# <a name="running-aspnet-11-with-iis-60"></a>Spuštění ASP.NET 1.1 se službou IIS 6.0

> Systém Windows Server 2003 zahrnuje službu IIS 6,0 i ASP.NET 1,1. tyto komponenty jsou ve výchozím nastavení zakázány. Tento dokument white paper popisuje, jak povolit IIS 6,0 a ASP.NET 1,1 a doporučuje několik nastavení konfigurace, aby se dosáhlo optimálního výkonu služeb IIS a ASP.NET.
> 
> Platí pro ASP.NET 1,1 a IIS 6,0.

ASP.NET 1,1 dodává se systémem Windows Server 2003, který obsahuje také nejnovější verzi serveru Internet Information Server (IIS) 6,0. Služba IIS 6,0 a ASP.NET 1,1 jsou navržené tak, aby se hladce integrují a ASP.NET teď ve výchozím nastavení nový model pracovních procesů služby IIS 6,0.

## <a name="aspnet-11-is-not-installed-by-default"></a>ASP.NET 1,1 není ve výchozím nastavení nainstalovaná.

Na rozdíl od předchozích verzí operačních systémů serveru společnosti Microsoft není služba Internet Information Server (IIS) standardně povolena. ani ASP.NET 1,1. Existují dvě možnosti, jak povolit službu IIS:

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>Povolení služby IIS, možnosti #1 – Průvodce konfigurací serveru

Windows Server 2003 dodává nový průvodce konfigurací serveru, který vám umožní správně nakonfigurovat server v požadovaném režimu.

Chcete-li spustit Průvodce – Poznámka: Chcete-li spustit průvodce, je nutné, abyste byli přihlášeni jako správce – přejít na: Start | Programy | Nástroje pro správu a vyberte Konfigurovat Server.

Po výběru byste měli vidět úvodní obrazovku průvodce konfigurací serveru:

![](aspnet-and-iis6/_static/image1.jpg)

Klikněte na další &gt;:

![](aspnet-and-iis6/_static/image2.jpg)

Klikněte na další &gt;.

![](aspnet-and-iis6/_static/image3.jpg)

Na této obrazovce budete muset jako možnosti konfigurace vybrat aplikační server (IIS, ASP.NET).

Klikněte na tlačítko Další &gt;.

![](aspnet-and-iis6/_static/image4.jpg)

Po výběru konfigurace serveru jako aplikačního serveru se zobrazí tato obrazovka s výzvou k tomu, jaké další možnosti by se měly nainstalovat. Ve výchozím nastavení není vybraná žádná možnost. Pokud chcete ASP.NET povolit automaticky, musíte vybrat Povolit ASP. NET.

Klikněte na tlačítko Další &gt;.

![](aspnet-and-iis6/_static/image5.jpg)

Tato obrazovka zobrazuje, jaké možnosti se mají nainstalovat.

Klikněte na tlačítko Další &gt;.

![](aspnet-and-iis6/_static/image6.jpg)

Tato obrazovka se zobrazí při instalaci možností, které jste vybrali. V normálním případě se zobrazí další dialogová okna, která se instalují jako služby. Může se zobrazit také výzva k zadání umístění instalačního disku CD systému Windows 2003 Server.

Po dokončení klikněte na tlačítko ' další &gt;'.

![](aspnet-and-iis6/_static/image7.jpg)

Klikněte na Dokončit – Windows Server 2003 je teď nakonfigurovaný tak, aby podporoval IIS 6,0 a ASP.NET 1,1.

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>Povolení služby IIS, možnost #2 – Ruční konfigurace služby IIS a ASP.NET

Pokud nechcete používat Průvodce konfigurací serveru, můžete volitelně nainstalovat IIS 6,0 a ASP.NET 1,1 pomocí příkazu Přidat nebo odebrat programy v Ovládacích panelech.

Nejprve otevřete ovládací panely:

![](aspnet-and-iis6/_static/image8.jpg)

Potom klikněte na tlačítko Přidat nebo odebrat součásti systému Windows. otevře se Průvodce součástmi systému Windows:

![](aspnet-and-iis6/_static/image9.jpg)

Zvýrazněte a zkontrolujte aplikační server a pak klikněte na podrobnosti. tlačítko

![](aspnet-and-iis6/_static/image10.jpg)

Pokud chcete nainstalovat ASP.NET, podívejte se na ASP. NET.

Kliknutím na tlačítko OK se vraťte do Průvodce součástmi systému Windows. Spusťte instalaci kliknutím na tlačítko Další &gt;v Průvodci součástmi systému Windows:

![](aspnet-and-iis6/_static/image11.jpg)

V normálním případě se zobrazí další dialogová okna, která se instalují jako služby. Může se zobrazit také výzva k zadání umístění instalačního disku CD systému Windows 2003 Server.

Po dokončení instalace se zobrazí poslední obrazovka Průvodce součástmi systému Windows:

![](aspnet-and-iis6/_static/image12.jpg)

Služba IIS 6,0 a ASP.NET 1,1 jsou teď nakonfigurované a dostupné.

## <a name="recommended-settings"></a>Doporučené nastavení

Při spuštění ASP.NET 1,1 se službou IIS 6,0 je k dispozici několik nastavení konfigurace, která jsou doporučena k dosažení optimálního výkonu z ASP.NET:

- Konfigurace omezení paměti pracovních procesů
- Konfigurace recyklace pracovních procesů

### <a name="configuring-worker-process-memory-limits"></a>Konfigurace omezení paměti pracovních procesů

Ve výchozím nastavení služba IIS 6,0 nenastavuje omezení velikosti paměti, kterou může služba IIS používat. Formátu. Funkce mezipaměti netto spoléhá na omezení paměti, takže mezipaměť může proaktivně odebrat nepoužívané položky z paměti.

Doporučuje se nakonfigurovat funkci Recyklace paměti služby IIS 6,0. Konfigurace tohoto programu Open Internetová informační služba Manager (Start | Programy | Nástroje pro správu | Internetová informační služba). Po otevření rozbalte složku fondy aplikací:

Pro každý fond aplikací:

![](aspnet-and-iis6/_static/image13.jpg)

1. Klikněte pravým tlačítkem na fond aplikací, třeba DefaultAppPool, a vyberte vlastnosti:

![](aspnet-and-iis6/_static/image14.jpg)

2. Potom kliknutím na možnost maximální velikost využité paměti (v megabajtech) Povolte recyklaci paměti:. Hodnota by neměla být větší než velikost fyzické (ne virtuální) paměti na serveru, dobrý odhad je 60% fyzické paměti, tj. pro server s 512 MB fyzické paměti vyberte 310. Doporučuje se také, aby při použití 2 GB adresního prostoru nepřekročila maximální počet 800MB. Pokud je adresní prostor paměti serveru povolenou, maximální limit paměti pro pracovní proces může být vysoký jako 1, 800MB:

![](aspnet-and-iis6/_static/image15.jpg)

Kliknutím na Apply (použít) a kliknutím na OK zavřete dialogové okno Vlastnosti. Tento postup opakujte pro všechny dostupné fondy aplikací.

### <a name="configuring-worker-recycling"></a>Konfigurace recyklace pracovních procesů

Ve výchozím nastavení je služba IIS 6,0 nakonfigurovaná k recyklaci pracovního procesu každých 29 hodin. Toto je trochu agresivní aplikace běžící na ASP.NET a doporučuje se, aby se automatické recyklace pracovních procesů zakázala.

Chcete-li zakázat automatickou recyklaci pracovních procesů, otevřete nejprve správce Internetová informační služba (Start | Programy | Nástroje pro správu | Internetová informační služba). Po otevření rozbalte složku fondy aplikací:

![](aspnet-and-iis6/_static/image16.jpg)

Pro každý fond aplikací:

1. Klikněte pravým tlačítkem na fond aplikací, třeba DefaultAppPool, a vyberte vlastnosti:

![](aspnet-and-iis6/_static/image17.jpg)

2. Zrušit kontrolu pracovního procesu recyklace (v minutách): ':

![](aspnet-and-iis6/_static/image18.jpg)

Kliknutím na Apply (použít) a kliknutím na OK zavřete dialogové okno Vlastnosti. Tento postup opakujte pro všechny dostupné fondy aplikací.

## <a name="granting-write-access-to-the-file-system"></a>Udělení přístupu pro zápis do systému souborů

Pokud vaše aplikace vyžaduje oprávnění k zápisu do systému souborů a používáte systém souborů NTFS, budete muset upravit seznam Access Control (ACL) pro složku nebo soubor a udělit tak přístup k ASP.NET.

Pokud například chcete udělit přístup pro zápis ASP.NET do složky c:\Inetpub\Wwwroot, otevřete Průzkumníka a přejděte do adresáře:

![](aspnet-and-iis6/_static/image19.jpg)

Potom klikněte pravým tlačítkem na adresář, třeba na "wwwroot" a vyberte vlastnosti. Po otevření dialogového okna Vlastnosti vyberte kartu zabezpečení:

![](aspnet-and-iis6/_static/image20.jpg)

Adresář c:\InetPub\Wwwroot\ je speciální adresář v tom, že speciální skupina služby IIS 6,0, kterou služba IIS\_WPG, už má udělenou možnost číst &amp; spouštění, zobrazovat obsah složky a číst. Pokud ale chcete udělit oprávnění k zápisu, musíte kliknout na zaškrtávací políčko Povolit pro zápis:

![](aspnet-and-iis6/_static/image21.jpg)

Služba IIS 6,0 má teď oprávnění k zápisu do této složky. Pokud chcete udělit oprávnění k zápisu na jiné složky, postupujte podle těchto kroků – Poznámka: Pokud ještě neexistuje, možná budete muset přidat skupinu IIS\_WPG.

> [!CAUTION]
> Udělení oprávnění k zápisu do služby IIS\_WPG umožní zapisovat do tohoto adresáře všechny aplikace v ASP.NET.

## <a name="supporting-integrated-authentication-with-sql-server"></a>Podpora integrovaného ověřování pomocí SQL Server

Integrované ověřování umožňuje SQL Server využívat ověřování systému Windows NT k ověření účtů přihlášení SQL Server. Uživatel tak může obejít standardní SQL Server procesu přihlášení. Pomocí tohoto přístupu může uživatel sítě získat přístup k databázi SQL Server bez zadání samostatného přihlašovacího ID nebo hesla, protože SQL Server získá informace o uživateli a heslech z procesu zabezpečení sítě systému Windows NT.

Volba integrovaného ověřování pro aplikace ASP.NET je dobrá volba, protože v připojovacím řetězci nejsou někdy uloženy žádné přihlašovací údaje pro vaši aplikaci. Místo toho se připojovací řetězec použitý k připojení k SQL bude podobat následujícímu:

`"server=localhost; database=Northwind;Trusted_Connection=true"`

Tento připojovací řetězec oznamuje SQL Server, aby používal přihlašovací údaje Windows pro aplikaci, která se pokouší získat přístup k SQL Server. V případě ASP.NET/IIS 6 by to byl účet ve skupině služby IIS\_WPG.

Pokud chcete povolit integrované ověřování mezi SQL Server a ASP.NET, musíte nejdřív zkontrolovat, jestli je SQL Server nakonfigurované pro integrované ověřování nebo ověřování ve smíšeném režimu – Pokud ho chcete zjistit, kontaktujte správce databáze. Pokud je SQL Server v jednom z těchto dvou režimů, můžete použít integrované ověřování.

Otevřete správce SQL Server Enterprise (Start | Programy | Microsoft SQL Server | Enterprise Manager) vyberte příslušný server a rozbalte složku zabezpečení:

![](aspnet-and-iis6/_static/image22.jpg)

Pokud není uvedená skupina BUILTINT\IIS\_WPG, klikněte pravým tlačítkem na přihlašovací údaje a vyberte New Login:

![](aspnet-and-iis6/_static/image23.jpg)

Do textového pole název: zadejte [Server/název domény] \IIS\_WPG nebo klikněte na tlačítko se třemi tečkami a otevřete výběr uživatele nebo skupiny Windows NT:

![](aspnet-and-iis6/_static/image24.jpg)

Vyberte skupinu IIS\_aktuální počítač a kliknutím na tlačítko Přidat a OK zavřete výběr.

Pak je nutné nastavit také výchozí databázi a oprávnění pro přístup k databázi. Výchozí databázi nastavíte tak, že vyberete možnost z rozevíracího seznamu, např.:

![](aspnet-and-iis6/_static/image25.jpg)

Potom klikněte na kartu přístup k databázi:

![](aspnet-and-iis6/_static/image26.jpg)

Pro každou databázi, ke které chcete povolit přístup, klikněte na zaškrtávací políčko Povolit. Budete také muset vybrat databázové role, zkontrolovat\_DB, že vaše přihlášení bude mít všechna potřebná oprávnění ke správě a používání vybrané databáze.

Kliknutím na tlačítko OK zavřete dialogové okno Vlastnosti. Vaše aplikace ASP.NET je teď nakonfigurovaná tak, aby podporovala integrované ověřování SQL Server.

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>Nespouštějte ASP.NET 1,0 v nativním režimu IIS 6,0

ASP.NET 1,0 ve službě IIS 6,0 je podporováno pouze v režimu kompatibility služby IIS 5.

Pokud chcete nakonfigurovat ASP.NET 1,0 v režimu kompatibility IIS 5,0, otevřete Správce služeb internetu a klikněte pravým tlačítkem na weby a vyberte vlastnosti:

![](aspnet-and-iis6/_static/image27.jpg)

Chcete přejít na kartu služby a ověřit? Spustit webovou službu v izolovaném režimu služby IIS 5,0?:

![](aspnet-and-iis6/_static/image28.jpg)
