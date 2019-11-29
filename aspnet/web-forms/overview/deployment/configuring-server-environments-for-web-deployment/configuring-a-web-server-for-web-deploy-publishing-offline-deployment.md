---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: Konfigurace webového serveru pro publikování Nasazení webu (offline nasazení) | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak nakonfigurovat webový server služby IIS tak, aby podporoval publikování a nasazení webu v režimu offline. Při práci s Internetová informační služba (I...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: f93cf11085fb19afb97b71aca8f638bd88fe658b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621102"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a>Konfigurace webového serveru pro publikování nasazeného webu (offline nasazení)

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak nakonfigurovat webový server služby IIS tak, aby podporoval publikování a nasazení webu v režimu offline.
> 
> Když pracujete s nástrojem Internetová informační služba (IIS) web pro nasazení webu (Nasazení webu) 2,0 nebo novější, existují tři hlavní přístupy, pomocí kterých můžete své aplikace nebo weby získat na webový server. Můžeš:
> 
> - Použijte *službu nasazení webu Remote Agent*. Tento přístup vyžaduje méně konfigurace webového serveru, ale musíte zadat přihlašovací údaje správce místního serveru, aby bylo možné na server nasadit cokoli.
> - Použijte *obslužnou rutinu nasazení webu*. Tento přístup je mnohem složitější a vyžaduje při nastavování webového serveru více počátečních úsilí. Pokud však použijete tento přístup, můžete nakonfigurovat službu IIS tak, aby umožňovala uživatelům bez oprávnění správce provádět nasazení. Obslužná rutina Nasazení webu je k dispozici pouze ve službě IIS verze 7 nebo novější.
> - Použijte *Offline nasazení*. Tento přístup vyžaduje nejmenší konfiguraci webového serveru, ale správce serveru musí ručně zkopírovat webový balíček na server a importovat ho pomocí Správce služby IIS.
> 
> Další informace o klíčových funkcích, výhodách a nevýhodách těchto přístupů najdete v tématu [Volba správného přístupu k nasazení webu](choosing-the-right-approach-to-web-deployment.md).

Ano, pokud vaše síťová infrastruktura nebo omezení zabezpečení brání vzdálenému nasazení. Nejpravděpodobnější příčinou je to, že se jedná o v produkčním prostředí s přístupem k Internetu, kde jsou&#x2014;webové servery izolované buď fyzicky, nebo pomocí bran&#x2014;firewall a podsítí ze zbytku serverové infrastruktury.

Tento přístup je zjevnější i v případě, že se webové aplikace aktualizují pravidelně. Pokud to vaše infrastruktura umožňuje, můžete zvážit povolení vzdáleného nasazení pomocí obslužné rutiny Nasazení webu nebo služby Nasazení webu vzdáleného agenta.

## <a name="task-overview"></a>Přehled úlohy

Pokud chcete nakonfigurovat webový server tak, aby podporoval offline import a nasazení webových balíčků, budete potřebovat:

- Nainstalujte službu IIS 7,5 a doporučenou konfiguraci IIS 7.
- Nainstalujte Nasazení webu 2,1 nebo novější.
- Vytvořte web IIS pro hostování nasazeného obsahu.
- Zakažte službu Web Deployment Agent.

K hostování ukázkového řešení také budete potřebovat:

- Nainstalujte .NET Framework 4,0.
- Nainstalujte ASP.NET MVC 3.

V tomto tématu se dozvíte, jak provádět jednotlivé postupy. V úlohách a návodech v tomto tématu se předpokládá, že začínáte s čistým sestavením serveru, na kterém běží Windows Server 2008 R2. Než budete pokračovat, ujistěte se, že:

- Nainstaluje se Windows Server 2008 R2 Service Pack 1 a nainstalují se všechny dostupné aktualizace.
- Server je připojený k doméně.
- Server má statickou IP adresu.

> [!NOTE]
> Další informace o připojení počítačů k doméně najdete v tématu [připojení počítačů k doméně a přihlášení](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Další informace o konfiguraci statických IP adres najdete v tématu [Konfigurace statické IP adresy](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).

## <a name="install-products-and-components"></a>Nainstalovat produkty a součásti

Tato část vás provede instalací požadovaných produktů a součástí na webovém serveru. Než začnete, je vhodné spustit web Windows Update, abyste se ujistili, že je váš server plně v aktuálním stavu.

V takovém případě je potřeba nainstalovat tyto věci:

- **Doporučená konfigurace služby IIS 7**. Tím povolíte roli **webový server (IIS)** na webovém serveru a nainstalujete sadu modulů a součástí IIS, které potřebujete k hostování aplikace v ASP.NET.
- **.NET Framework 4,0**. To je nutné ke spuštění aplikací, které byly vytvořeny v této verzi .NET Framework.
- **Nástroj pro nasazení webu 2,1 nebo novější**. Tím se na váš server nainstaluje Nasazení webu (a jeho základní spustitelný soubor MSDeploy. exe). Nasazení webu se integruje se službou IIS a umožňuje importovat a exportovat webové balíčky.
- **ASP.NET MVC 3**. Tím se nainstaluje sestavení, která potřebujete ke spouštění aplikací MVC 3.

> [!NOTE]
> Tento návod popisuje použití instalačního programu webové platformy k instalaci a konfiguraci různých součástí. I když nemusíte používat instalační program webové platformy, zjednodušuje proces instalace tím, že automaticky detekuje závislosti a zajistil, že vždy získáte nejnovější verze produktu. Další informace najdete v tématu [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/?linkid=9805118).

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

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. V řádku **ASP.NET MVC 3 (Visual Studio 2010)** klikněte na **Přidat**.
7. V navigačním podokně klikněte na možnost **Server**.
8. V řádku **Konfigurace doporučeného pro IIS 7** klikněte na **Přidat**.
9. V řádku **Nástroje pro nasazení webu 2,1** klikněte na **Přidat**.
10. Klikněte na **nainstalovat**. Instalační program webové platformy zobrazí seznam produktů&#x2014;spolu s případnými přidruženými závislostmi&#x2014;, které se mají nainstalovat, a zobrazí výzvu k přijetí těchto licenčních podmínek.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. Přečtěte si licenční podmínky a pokud souhlasíte s podmínkami **, klikněte na Souhlasím.**
12. Po dokončení instalace klikněte na **Dokončit**a potom zavřete okno **instalace webové platformy 3,0** .

Pokud jste nainstalovali .NET Framework 4,0 před instalací služby IIS, budete muset spustit [registrační nástroj služby ASP.NET IIS](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (ASPNET\_regiis. exe) a zaregistrovat nejnovější verzi ASP.NET se službou IIS. Pokud to neuděláte, zjistíte, že služba IIS bude sloužit jako statický obsah (například soubory HTML) bez jakýchkoli problémů, ale při pokusu o procházení obsahu ASP.NET se nenajde **Chyba HTTP 404,0 – nebude Nalezeno** . K zajištění registrace ASP.NET 4,0 můžete použít další postup.

**Registrace ASP.NET 4,0 se službou IIS**

1. Klikněte na tlačítko **Start**a zadejte **příkaz Command Prompt**.
2. Ve výsledcích hledání klikněte pravým tlačítkem myši na **příkazový řádek**a pak klikněte na **Spustit jako správce**.
3. V okně příkazového řádku přejděte do adresáře **%windir%\Microsoft.NET\Framework\v4.0.30319** .
4. Zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. Pokud máte v úmyslu hostovat 64 webové aplikace v jakémkoli bodě, měli byste také zaregistrovat 64 verzi ASP.NET se službou IIS. To provedete tak, že v okně příkazového řádku přejdete do adresáře **%windir%\Microsoft.NET\Framework64\v4.0.30319** .
6. Zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

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
3. Ve Správci služby IIS rozbalte v podokně **připojení** uzel serveru (například **PROWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. Klikněte pravým tlačítkem myši na uzel **lokality** a pak klikněte na možnost **Přidat web**.
5. Do pole **název lokality** zadejte název webu služby IIS (například **DemoSite**).
6. Do pole **fyzická cesta** zadejte (nebo vyhledejte) cestu k místní složce (například **C:\DemoSite**).
7. Do pole **port** zadejte číslo portu, na kterém chcete web hostovat (například **85**).

    > [!NOTE]
    > Standardní čísla portů jsou 80 pro protokol HTTP a 443 pro protokol HTTPS. Pokud však tento web Hostujte na portu 80, budete muset před přístupem k webu zastavit výchozí web.
8. Pole **název hostitele** nechte prázdné, pokud nechcete pro web nakonfigurovat záznam DNS (Domain Name System), a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > V produkčním prostředí pravděpodobně budete chtít web hostovat na portu 80 a nakonfigurovat hlavičku hostitele spolu se shodnými záznamy DNS. Další informace o konfiguraci hlaviček hostitele ve službě IIS 7 najdete v tématu [Konfigurace hlavičky hostitele webu (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx). Další informace o roli serveru DNS v systému Windows Server 2008 R2 najdete v tématu [Přehled serveru DNS](https://technet.microsoft.com/library/cc770392.aspx) a [Server DNS](https://technet.microsoft.com/windowsserver/dd448607).
9. V podokně **Akce** klikněte v části **Upravit web**na možnost **vazby**.
10. V dialogovém okně **vazby webu** klikněte na **Přidat**.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. V dialogovém okně **Přidat vazbu webu** nastavte **IP adresu** a **port** tak, aby odpovídaly vaší stávající konfiguraci lokality.
12. Do pole **název hostitele** zadejte název vašeho webového serveru (například **PROWEB1**) a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > První vazba webu umožňuje přístup k webu místně pomocí IP adresy a portu nebo `http://localhost:85`. Druhá vazba webu umožňuje přístup k webu z jiných počítačů v doméně pomocí názvu počítače (například http://proweb1:85).
13. V dialogovém okně **vazby webu** klikněte na **Zavřít**.
14. V podokně **připojení** klikněte na **fondy aplikací**.
15. V podokně **fondy aplikací** klikněte pravým tlačítkem myši na název vašeho fondu aplikací a potom klikněte na **základní nastavení**. Ve výchozím nastavení bude název vašeho fondu aplikací odpovídat názvu vašeho webu (například **DemoSite**).
16. V seznamu **.NET Framework verze** vyberte **.NET Framework v 4.0.30319**a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > Ukázkové řešení vyžaduje .NET Framework 4,0. Nejedná se o požadavek Nasazení webu obecně.

Aby váš web mohl poskytovat obsah, musí mít identita fondu aplikací oprávnění ke čtení v místní složce, ve které je uložený obsah. Ve službě IIS 7,5 se fondy aplikací ve výchozím nastavení spouštějí s jedinečnou identitou fondu aplikací (na rozdíl od předchozích verzí služby IIS, kde by fondy aplikací obvykle běžely pomocí účtu síťové služby). Identita fondu aplikací není reálného uživatelského účtu a nezobrazuje se v žádných seznamech uživatelů nebo skupin&#x2014;, ale je vytvořená dynamicky při spuštění fondu aplikací. Každá identita fondu aplikací se přidá do místní skupiny zabezpečení **služby IIS\_IUSRS** jako skrytá položka.

Chcete-li udělit oprávnění k identitě fondu aplikací pro soubor nebo složku, máte dvě možnosti:

- Přiřaďte oprávnění k identitě fondu aplikací přímo pomocí formátu <strong>IIS AppPool\</strong ><em>[název fondu aplikací]</em>(například <strong>IIS AppPool\DemoSite</strong>).
- Přiřaďte oprávnění skupině **IUSRS služby IIS\_** .

Nejběžnějším přístupem je přiřazení oprávnění k místní skupině **služby IIS\_IUSRS** , protože tento přístup umožňuje změnit fondy aplikací bez nutnosti znovu nakonfigurovat oprávnění systému souborů. Další postup používá tento přístup založený na skupině.

> [!NOTE]
> Další informace o identitách fondu aplikací ve službě IIS 7,5 najdete v tématu [identity fondů aplikací](https://go.microsoft.com/?linkid=9805123).

**Konfigurace oprávnění složky pro web služby IIS**

1. V Průzkumníku Windows přejděte do umístění místní složky.
2. Klikněte pravým tlačítkem na složku a pak klikněte na **vlastnosti**.
3. Na kartě **zabezpečení** klikněte na **Upravit**a pak klikněte na **Přidat**.
4. Klikněte na **umístění**. V dialogovém okně **umístění** vyberte místní server a klikněte na tlačítko **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. V dialogovém okně **Vybrat uživatele nebo skupiny** zadejte **IIS\_IUSRS**, klikněte na **kontrolovat jména**a pak klikněte na **OK**.
6. V dialogovém okně <strong>oprávnění pro</strong><em>[název složky]</em> si všimněte, že je ve výchozím nastavení přiřazená k nové skupině oprávnění <strong>číst &amp; spustit</strong>, <strong>Zobrazit obsah složky</strong>a <strong>číst</strong> . Nechejte to beze změny a klikněte na <strong>OK</strong>.
7. Kliknutím na tlačítko <strong>OK</strong> zavřete dialogové okno<strong>vlastnosti</strong> <em>[název složky]</em>.

## <a name="disable-the-remote-agent-service"></a>Zakázat službu vzdáleného agenta

Při instalaci Nasazení webu je služba Web Deployment Agent nainstalována a spuštěna automaticky. Tato služba umožňuje nasadit a publikovat webové balíčky ze vzdáleného umístění. V tomto scénáři nebudete používat schopnost vzdáleného nasazení, proto byste měli službu zastavit a zakázat.

> [!NOTE]
> Nemusíte zastavovat službu vzdáleného agenta, aby bylo možné ručně naimportovat a nasazovat webový balíček. Nicméně je dobrým zvykem zastavit a zakázat službu, pokud ji neplánujete použít.

Službu můžete zastavit a zakázat několika způsoby pomocí různých nástrojů příkazového řádku nebo rutin prostředí Windows PowerShell. Tento postup popisuje přímočarý přístup založený na uživatelském rozhraní.

**Zastavení a zakázání služby vzdáleného agenta**

1. V nabídce **Start** přejděte na **Nástroje pro správu**a potom klikněte na **služby**.
2. V konzole služby vyhledejte řádek **Web Deployment Agent Service** .

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. Klikněte pravým tlačítkem na **službu Web Deployment Agent**a pak klikněte na **vlastnosti**.
4. V dialogovém okně **Vlastnosti služby webové Deployment Agent** klikněte na tlačítko **zastavit**.
5. V seznamu **Typ spouštění** vyberte možnost **zakázáno**a pak klikněte na tlačítko **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a>Závěr

V tuto chvíli je váš webový server připravený na offline nasazení webového balíčku. Předtím, než se pokusíte importovat webové balíčky na web služby IIS, je vhodné tyto klíčové body kontrolovat:

- Zaregistrovali jste ASP.NET 4,0 se službou IIS?
- Má identita fondu aplikací oprávnění ke čtení pro zdrojovou složku vašeho webu?
- Zastavili jste službu Web Deployment Agent?

> [!div class="step-by-step"]
> [Předchozí](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [Další](configuring-a-database-server-for-web-deploy-publishing.md)
