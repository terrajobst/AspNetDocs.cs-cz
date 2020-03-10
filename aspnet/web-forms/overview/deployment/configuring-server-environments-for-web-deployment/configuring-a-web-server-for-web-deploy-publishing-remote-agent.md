---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: Konfigurace webového serveru pro publikování Nasazení webu (vzdálený Agent) | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak nakonfigurovat webový server Internetová informační služba (IIS) tak, aby podporoval publikování a nasazení webu pomocí webového nasazení služby IIS...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: ce0d246afdfb65c2ea15a287064511e7d1d58622
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567471"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>Konfigurace webového serveru pro publikování nasazeného webu (vzdálený agent)

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak nakonfigurovat webový server Internetová informační služba (IIS) tak, aby podporoval publikování a nasazení webu pomocí služby vzdáleného agenta nástroje pro nasazení webu služby IIS (Nasazení webu).
> 
> Když pracujete s Nasazení webu 2,0 nebo novějším, existují tři hlavní přístupy, pomocí kterých můžete své aplikace nebo weby získat na webový server. Můžete:
> 
> - Použijte *službu nasazení webu Remote Agent*. Tento přístup vyžaduje méně konfigurace webového serveru, ale musíte zadat přihlašovací údaje správce místního serveru, aby bylo možné na server nasadit cokoli.
> - Použijte *obslužnou rutinu nasazení webu*. Tento přístup je mnohem složitější a vyžaduje při nastavování webového serveru více počátečních úsilí. Pokud však použijete tento přístup, můžete nakonfigurovat službu IIS tak, aby umožňovala uživatelům bez oprávnění správce provádět nasazení. Obslužná rutina Nasazení webu je k dispozici pouze ve službě IIS verze 7 nebo novější.
> - Použijte *Offline nasazení*. Tento přístup vyžaduje nejmenší konfiguraci webového serveru, ale správce serveru musí ručně zkopírovat webový balíček na server a importovat ho pomocí Správce služby IIS.
> 
> Další informace o klíčových funkcích, výhodách a nevýhodách těchto přístupů najdete v tématu [Volba správného přístupu k nasazení webu](choosing-the-right-approach-to-web-deployment.md).

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>Je Nasazení webu Vzdálený agent pro vás správný přístup?

Ano, pokud uživatel, který bude obsah nasazovat, může zadat přihlašovací údaje správce na cílovém serveru. Tento přístup je často žádoucí v těchto typech scénářů:

- Vývojové nebo testovací prostředí, kde vývojář má plnou kontrolu nad cílovým webovým serverem a databázovým serverem.
- Menší organizace, ve kterých má jeden uživatel nebo malá skupina uživatelů kontrolu nad celým životním cyklem aplikace.

V mnoha větších organizacích, a to hlavně pro pracovní nebo produkční prostředí, není často reálné, aby uživatelům poskytoval práva správce na webových serverech. V případě hostovaných webových serverů to je obzvláště pravděpodobné, že se nejedná o případ. Kromě toho, pokud plánujete automatizovat nasazení ze serveru sestavení, nebudete chtít pro proces nasazení použít přihlašovací údaje správce. V těchto scénářích je možné nakonfigurovat webové servery tak, aby podporovaly nasazení pomocí [obslužné rutiny nasazení webu](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) může poskytovat přesněji vyhovující možnosti.

## <a name="task-overview"></a>Přehled úlohy

V tomto tématu se dozvíte, jak nakonfigurovat webový server Internetová informační služba (IIS) 7,5 pro přijímání a nasazování webových balíčků ze vzdáleného počítače pomocí přístupu ke vzdálenému agentu Nasazení webu. Budete potřebovat:

- Nainstalujte službu IIS 7,5 a doporučenou konfiguraci IIS 7.
- Nainstalujte Nasazení webu 2,1 nebo novější.
- Vytvořte web IIS pro hostování nasazeného obsahu.
- Ujistěte se, že je spuštěná služba Web Deployment Agent.

K hostování ukázkového řešení také budete potřebovat:

- Nainstalujte .NET Framework 4,0.
- Nainstalujte ASP.NET MVC 3.

V tomto tématu se dozvíte, jak provádět jednotlivé postupy. V úlohách a návodech v tomto tématu se předpokládá, že začínáte s čistým sestavením serveru, na kterém běží Windows Server 2008 R2. Než budete pokračovat, ujistěte se, že:

- Nainstaluje se Windows Server 2008 R2 Service Pack 1 a nainstalují se všechny dostupné aktualizace.
- Server je připojený k doméně.
- Server má statickou IP adresu.

> [!NOTE]
> Další informace o připojení počítačů k doméně najdete v tématu [připojení počítačů k doméně a přihlášení](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Další informace o konfiguraci statických IP adres najdete v tématu [Konfigurace statické IP adresy](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx). Služba vzdáleného agenta je podporována službou IIS 6 a vyšší a nevyžaduje, abyste se připojili k doméně. Postup v tomto kurzu byl ale vyvinutý a testovaný ve službě IIS 7,5 a postupy pro jiné verze se můžou lišit.

## <a name="install-products-and-components"></a>Nainstalovat produkty a součásti

Tato část vás provede instalací požadovaných produktů a součástí na webovém serveru. Než začnete, je vhodné spustit web Windows Update, abyste se ujistili, že je váš server plně v aktuálním stavu.

V takovém případě je potřeba nainstalovat tyto věci:

- **Doporučená konfigurace služby IIS 7**. Tím povolíte roli **webový server (IIS)** na webovém serveru a nainstalujete sadu modulů a součástí IIS, které potřebujete k hostování aplikace v ASP.NET.
- **.NET Framework 4,0**. To je nutné ke spuštění aplikací, které byly vytvořeny v této verzi .NET Framework.
- **Nástroj pro nasazení webu 2,1 nebo novější**. Tím se na váš server nainstaluje Nasazení webu (a jeho základní spustitelný soubor MSDeploy. exe). V rámci tohoto procesu nainstaluje a spustí službu Web Deployment Agent. Tato služba umožňuje nasadit webové balíčky ze vzdáleného počítače.
- **ASP.NET MVC 3**. Tím se nainstaluje sestavení, která potřebujete ke spouštění aplikací MVC 3.

> [!NOTE]
> Tento návod popisuje použití instalačního programu webové platformy k instalaci a konfiguraci požadovaných součástí. I když nemusíte používat instalační program webové platformy, zjednodušuje proces instalace tím, že automaticky detekuje závislosti a zajistil, že vždy získáte nejnovější verze produktu. Další informace najdete v tématu [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/?linkid=9805118).

**Instalace požadovaných produktů a součástí**

1. Stáhněte a nainstalujte [instalační program webové platformy](https://go.microsoft.com/?linkid=9805118).
2. Po dokončení instalace se instalační program webové platformy spustí automaticky.

    > [!NOTE]
    > V nabídce **Start** teď můžete kdykoli spustit instalační program webové platformy. Provedete to tak, že v nabídce **Start** kliknete na **všechny programy**a pak na **Instalace webové platformy Microsoft**.
3. V horní části okna **Instalace webové platformy 3,0** klikněte na **produkty**.
4. Na levé straně okna klikněte v navigačním podokně na možnost **architektury**.
5. Pokud .NET Framework ještě není nainstalovaná, na řádku **Microsoft .NET Framework 4** klikněte na **Přidat**.

    > [!NOTE]
    > Je možné, že jste už nainstalovali .NET Framework 4,0 prostřednictvím web Windows Update. Pokud je produkt nebo součást již nainstalována, instalační program webové platformy tuto skutečnost indikuje tak, že nahrazuje tlačítko **Přidat** s textem, který je **nainstalován**.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. V řádku **ASP.NET MVC 3 (Visual Studio 2010)** klikněte na **Přidat**.
7. V navigačním podokně klikněte na možnost **Server**.
8. V řádku **Konfigurace doporučeného pro IIS 7** klikněte na **Přidat**.
9. V řádku **Nástroje pro nasazení webu 2,1** klikněte na **Přidat**.
10. Klikněte na **Nainstalovat**. Instalační program webové platformy zobrazí seznam produktů&#x2014;spolu s případnými přidruženými závislostmi&#x2014;, které se mají nainstalovat, a zobrazí výzvu k přijetí těchto licenčních podmínek.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. Přečtěte si licenční podmínky a pokud souhlasíte s podmínkami **, klikněte na Souhlasím.**
12. Po dokončení instalace klikněte na **Dokončit**a potom zavřete okno **instalace webové platformy 3,0** .

Pokud jste nainstalovali .NET Framework 4,0 před instalací služby IIS, budete muset spustit [registrační nástroj služby ASP.NET IIS](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (ASPNET\_regiis. exe) a zaregistrovat nejnovější verzi ASP.NET se službou IIS. Pokud to neuděláte, zjistíte, že služba IIS bude sloužit jako statický obsah (například soubory HTML) bez jakýchkoli problémů, ale při pokusu o procházení obsahu ASP.NET se nenajde **Chyba HTTP 404,0 – nebude Nalezeno** . Pomocí tohoto postupu můžete zajistit, aby byl zaregistrován ASP.NET 4,0.

**Registrace ASP.NET 4,0 se službou IIS**

1. Klikněte na tlačítko **Start**a zadejte **příkaz Command Prompt**.
2. Ve výsledcích hledání klikněte pravým tlačítkem myši na **příkazový řádek**a pak klikněte na **Spustit jako správce**.
3. V okně příkazového řádku přejděte do adresáře **%windir%\Microsoft.NET\Framework\v4.0.30319** .
4. Zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. Pokud máte v úmyslu hostovat 64 webové aplikace v jakémkoli bodě, měli byste také zaregistrovat 64 verzi ASP.NET se službou IIS. To provedete tak, že v okně příkazového řádku přejdete do adresáře **%windir%\Microsoft.NET\Framework64\v4.0.30319** .
6. Zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

Vhodným postupem je znovu použít web Windows Update v tuto chvíli ke stažení a instalaci všech dostupných aktualizací pro nové produkty a komponenty, které jste nainstalovali.

## <a name="configure-the-iis-website"></a>Konfigurace webu služby IIS

Předtím, než budete moci nasadit webový obsah na server, je nutné vytvořit a nakonfigurovat web služby IIS pro hostování obsahu. Nasazení webu můžou nasadit jenom webové balíčky na existující web IIS; pro vás nemůže web vytvořit. Na vysoké úrovni budete muset dokončit tyto úlohy:

- Vytvořte v systému souborů složku pro hostování vašeho obsahu.
- Vytvořte web IIS pro poskytování obsahu a přidružte ho k místní složce.
- Udělte oprávnění ke čtení identitě fondu aplikací v místní složce.

I když se vám nic nezastaví od nasazení obsahu na výchozí web ve službě IIS, tento přístup se nedoporučuje pro žádnou jinou než testovací nebo demonstrační scénář. Chcete-li simulovat produkční prostředí, měli byste vytvořit nový web služby IIS s nastavením, které je specifické pro požadavky vaší aplikace.

**Vytvoření a konfigurace webu služby IIS**

1. V místním systému souborů vytvořte složku pro uložení vašeho obsahu (například **C:\DemoSite**).
2. V nabídce **Start** přejděte na **Nástroje pro správu**a potom klikněte na **Správce služby Internetová informační služba (IIS)** .
3. Ve Správci služby IIS rozbalte v podokně **připojení** uzel serveru (například **TESTWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. Klikněte pravým tlačítkem myši na uzel **lokality** a pak klikněte na možnost **Přidat web**.
5. Do pole **název lokality** zadejte název webu služby IIS (například **DemoSite**).
6. Do pole **fyzická cesta** zadejte (nebo vyhledejte) cestu k místní složce (například **C:\DemoSite**).
7. Do pole **port** zadejte číslo portu, na kterém chcete web hostovat (například **85**).

    > [!NOTE]
    > Standardní čísla portů jsou 80 pro protokol HTTP a 443 pro protokol HTTPS. Pokud však tento web Hostujte na portu 80, budete muset před přístupem k webu zastavit výchozí web.
8. Pole **název hostitele** nechte prázdné, pokud nechcete pro web nakonfigurovat záznam DNS (Domain Name System), a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > V produkčním prostředí pravděpodobně budete chtít web hostovat na portu 80 a nakonfigurovat hlavičku hostitele spolu se shodnými záznamy DNS. Další informace o konfiguraci hlaviček hostitele ve službě IIS 7 najdete v tématu [Konfigurace hlavičky hostitele webu (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx). Další informace o roli serveru DNS v systému Windows Server 2008 R2 najdete v tématu [Přehled serveru DNS](https://technet.microsoft.com/library/cc770392.aspx) a [Server DNS](https://technet.microsoft.com/windowsserver/dd448607).
9. V podokně **Akce** klikněte v části **Upravit web**na možnost **vazby**.
10. V dialogu **Vazby webu** klikněte na **Přidat**.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. V dialogovém okně **Přidat vazbu webu** nastavte **IP adresu** a **port** tak, aby odpovídaly vaší stávající konfiguraci lokality.
12. Do pole **název hostitele** zadejte název vašeho webového serveru (například **TESTWEB1**) a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > První vazba webu umožňuje přístup k webu místně pomocí IP adresy a portu nebo `http://localhost:85`. Druhá vazba webu umožňuje přístup k webu z jiných počítačů v doméně pomocí názvu počítače (například http://testweb1:85).
13. V dialogu **Vazby webu** klikněte na **Zavřít**.
14. V podokně **připojení** klikněte na **fondy aplikací**.
15. V podokně **fondy aplikací** klikněte pravým tlačítkem myši na název vašeho fondu aplikací a potom klikněte na **základní nastavení**. Ve výchozím nastavení bude název vašeho fondu aplikací odpovídat názvu vašeho webu (například **DemoSite**).
16. V seznamu **.NET Framework verze** vyberte **.NET Framework v 4.0.30319**a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > Ukázkové řešení vyžaduje .NET Framework 4,0. Nejedná se o požadavek Nasazení webu obecně.

Aby váš web mohl poskytovat obsah, musí mít identita fondu aplikací oprávnění ke čtení v místní složce, ve které je uložený obsah. Ve službě IIS 7,5 se fondy aplikací ve výchozím nastavení spouštějí s jedinečnou identitou fondu aplikací (na rozdíl od předchozích verzí služby IIS, kde by fondy aplikací obvykle běžely pomocí účtu síťové služby). Identita fondu aplikací není reálného uživatelského účtu a nezobrazuje se v žádných seznamech uživatelů nebo skupin&#x2014;, ale je vytvořená dynamicky při spuštění fondu aplikací. Každá identita fondu aplikací se přidá do místní skupiny zabezpečení **služby IIS\_IUSRS** jako skrytá položka.

Chcete-li udělit oprávnění k identitě fondu aplikací pro soubor nebo složku, máte dvě možnosti:

- Přiřaďte oprávnění k identitě fondu aplikací přímo pomocí formátu <strong>IIS AppPool\</strong ><em>[název fondu aplikací]</em>(například <strong>IIS AppPool\DemoSite</strong>).
- Přiřaďte oprávnění skupině **IUSRS služby IIS\_** .

Nejběžnějším přístupem je přiřazení oprávnění místní skupině **služby IIS\_IUSRS** , protože tento přístup umožňuje změnit fondy aplikací bez nutnosti opětovné konfigurace oprávnění systému souborů. Další postup používá tento přístup založený na skupině.

> [!NOTE]
> Další informace o identitách fondu aplikací ve službě IIS 7,5 najdete v tématu [identity fondů aplikací](https://go.microsoft.com/?linkid=9805123).

**Konfigurace oprávnění složky pro web služby IIS**

1. V Průzkumníku Windows přejděte do umístění místní složky.
2. Klikněte pravým tlačítkem na složku a pak klikněte na **vlastnosti**.
3. Na kartě **zabezpečení** klikněte na **Upravit**a pak klikněte na **Přidat**.
4. Klikněte na **umístění**. V dialogovém okně **umístění** vyberte místní server a klikněte na tlačítko **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. V dialogovém okně **Vybrat uživatele nebo skupiny** zadejte **IIS\_IUSRS**, klikněte na **kontrolovat jména**a pak klikněte na **OK**.
6. V dialogovém okně <strong>oprávnění pro</strong><em>[název složky]</em>si všimněte, že je ve výchozím nastavení přiřazená k nové skupině oprávnění <strong>číst &amp; spustit</strong>, <strong>Zobrazit obsah složky</strong>a <strong>číst</strong> . Nechejte to beze změny a klikněte na <strong>OK</strong>.
7. Kliknutím na tlačítko <strong>OK</strong> zavřete dialogové okno<strong>vlastnosti</strong> <em>[název složky]</em>.

Jako poslední úkol před tím, než se pokusíte nasadit jakékoli webové balíčky na server, je nutné zajistit, aby služba Web Deployment Agent běžela. Když nasadíte balíček ze vzdáleného počítače, služba Web Deployment Agent zodpovídá za extrakci a instalaci obsahu balíčku. Služba se ve výchozím nastavení spouští při instalaci nástroje pro nasazení webu a spouští se v rámci identity síťové služby.

Pomocí různých nástrojů příkazového řádku nebo rutin prostředí Windows PowerShell můžete zjistit, jestli je služba spuštěná několika různými způsoby. Tento postup popisuje přímočarý přístup založený na uživatelském rozhraní.

**Chcete-li ověřit, zda je spuštěna služba Web Deployment Agent**

1. V nabídce **Start** přejděte na **Nástroje pro správu**a potom klikněte na **služby**.
2. Vyhledejte řádek **Web Deployment Agent Service** a ověřte, zda je **stav** nastaven na **spuštěno**.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. Pokud služba ještě není spuštěná, klikněte na **Spustit**.

## <a name="configure-firewall-exceptions"></a>Konfigurace výjimek brány firewall

Ve výchozím nastavení služba vzdáleného agenta naslouchá na portu TCP 80 na této adrese URL:

<http://servername.com/MSDEPLOYAGENTSERVICE>

Ve většině případů nebudete muset konfigurovat další pravidla brány firewall pro službu Remote Agent, protože webové servery obvykle naslouchají požadavkům HTTP na portu 80. Pokud jste přizpůsobili instalaci, aby naslouchala na nestandardním portu, bude nutné nakonfigurovat výjimky brány firewall podle potřeby.

## <a name="conclusion"></a>Závěr

V tuto chvíli je váš webový server připravený přijímat a instalovat webové balíčky ze vzdáleného počítače. Předtím, než se pokusíte nasadit webovou aplikaci na server, je vhodné tyto klíčové body ověřit:

- Zaregistrovali jste ASP.NET 4,0 se službou IIS?
- Má identita fondu aplikací oprávnění ke čtení pro zdrojovou složku vašeho webu?
- Běží služba Web Deployment Agent?

## <a name="further-reading"></a>Další čtení

Informace o tom, jak nakonfigurovat vlastní soubory projektu Microsoft Build Engine (MSBuild) k nasazení webových balíčků do služby Remote Agent, najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](configuring-deployment-properties-for-a-target-environment.md).

> [!div class="step-by-step"]
> [Předchozí](scenario-configuring-a-production-environment-for-web-deployment.md)
> [Další](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
