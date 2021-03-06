---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: Konfigurace webového serveru pro publikování Nasazení webu (obslužná rutina Nasazení webu) | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak nakonfigurovat webový server Internetová informační služba (IIS) tak, aby podporoval publikování a nasazení webu pomocí služby IIS Nasazení webu Han...
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: baaebd32f08d3c6b861572c5c5a16ec0fb70aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568563"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a>Konfigurace webového serveru pro publikování nasazeného webu (obslužná rutina nasazení webu)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak nakonfigurovat webový server Internetová informační služba (IIS) tak, aby podporoval publikování a nasazení webu pomocí Nasazení webu obslužné rutiny služby IIS.
> 
> Když pracujete s Nasazení webu 2,0 nebo novějším, existují tři hlavní přístupy, pomocí kterých můžete své aplikace nebo weby získat na webový server. Můžete:
> 
> - Použijte *službu nasazení webu Remote Agent*. Tento přístup vyžaduje méně konfigurace webového serveru, ale musíte zadat přihlašovací údaje správce místního serveru, aby bylo možné na server nasadit cokoli.
> - Použijte *obslužnou rutinu nasazení webu*. Tento přístup je mnohem složitější a vyžaduje při nastavování webového serveru více počátečních úsilí. Pokud však použijete tento přístup, můžete nakonfigurovat službu IIS tak, aby umožňovala uživatelům bez oprávnění správce provádět nasazení. Obslužná rutina Nasazení webu je k dispozici pouze ve službě IIS verze 7 nebo novější.
> - Použijte *Offline nasazení*. Tento přístup vyžaduje nejmenší konfiguraci webového serveru, ale správce serveru musí ručně zkopírovat webový balíček na server a importovat ho pomocí Správce služby IIS.
> 
> Další informace o klíčových funkcích, výhodách a nevýhodách těchto přístupů najdete v tématu [Volba správného přístupu k nasazení webu](choosing-the-right-approach-to-web-deployment.md).

Ano, pokud chcete, aby uživatelé bez oprávnění správce mohli nasadit obsah na konkrétní weby IIS. Tento přístup je často žádoucí v těchto typech scénářů:

- Pracovní nebo produkční prostředí, kde osoba nebo účet služby, který aktivuje vzdálené nasazení, nemá pravděpodobně přístup k přihlašovacím údajům správce serveru.
- Hostovaná prostředí, kde chcete, aby vzdálení uživatelé mohli aktualizovat své weby, aniž by jim poskytovali plnou kontrolu nad webovými servery (nebo přístup k webům ostatních uživatelů).

Ve scénářích vývoje nebo testování nebo v menších organizacích je nasazení obsahu pomocí přihlašovacích údajů správce serveru často méně contentious. V těchto scénářích můžete nakonfigurovat webové servery tak, aby podporovaly nasazení pomocí [nasazení webu služba vzdáleného agenta](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) nabízí složitější přístup.

## <a name="task-overview"></a>Přehled úlohy

Chcete-li nakonfigurovat webový server tak, aby přijímal a nasadil webové balíčky ze vzdáleného počítače pomocí přístupu k obslužné rutině Nasazení webu, budete potřebovat:

- Vytvořte nebo vyberte účet uživatele domény ("uživatel bez oprávnění správce"), jehož přihlašovací údaje budete používat k provádění nasazení.
- Nainstalujte službu IIS 7,5, včetně služby webové správy a modulu základní ověřování.
- Nainstalujte Nasazení webu 2,1 nebo novější.
- Nakonfigurujte službu Web Management tak, aby povolovala vzdálená připojení, a spusťte službu.
- Vytvořte web IIS pro hostování nasazeného obsahu.
- Udělte svým webům oprávnění uživatele bez oprávnění správce ve Správci služby IIS.
- Ujistěte se, že pravidla delegování služby webové správy umožňují, aby služba přidala a změnila obsah webu pomocí uživatelského účtu bez oprávnění správce.
- Nakonfigurujte všechny brány firewall tak, aby povolovaly příchozí připojení na portu 8172.

Pro konkrétní hostování ukázkového řešení ContactManager budete také potřebovat:

- Nainstalujte .NET Framework 4,0.
- Nainstalujte ASP.NET MVC 3.

V tomto tématu se dozvíte, jak provádět jednotlivé postupy. V úlohách a návodech v tomto tématu se předpokládá, že začínáte s čistým sestavením serveru se spuštěným systémem Windows Server 2016. Než budete pokračovat, ujistěte se, že:

- Windows Server 2016
- Server je připojený k doméně.
- Server má statickou IP adresu.

> [!NOTE]
> Další informace o připojení počítačů k doméně najdete v tématu [připojení počítačů k doméně a přihlášení](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Další informace o konfiguraci statických IP adres najdete v tématu [Konfigurace statické IP adresy](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).

## <a name="install-products-and-components"></a>Nainstalovat produkty a součásti

Tato část vás provede instalací požadovaných produktů a součástí na webovém serveru. Než začnete, je vhodné spustit web Windows Update, abyste se ujistili, že je váš server plně v aktuálním stavu.

V takovém případě je potřeba nainstalovat tyto věci:

- **Doporučená konfigurace služby IIS 7**. Tím povolíte roli **webový server (IIS)** na webovém serveru a nainstalujete sadu modulů a součástí IIS, které potřebujete k hostování aplikace v ASP.NET.
- Služba **IIS: Služba správy**. Tím se do služby IIS nainstaluje služba webové správy (WMSvc). Tato služba umožňuje vzdálenou správu webů IIS a zpřístupňuje koncový bod obslužné rutiny Nasazení webu klientům.
- **Služba IIS: základní ověřování**. Tím se nainstaluje modul pro základní ověřování služby IIS. To umožňuje službě webové správy (WMSvc) ověřit přihlašovací údaje, které zadáte.
- **Nástroj pro nasazení webu 2,1 nebo novější**. Tím se na váš server nainstaluje Nasazení webu (a jeho základní spustitelný soubor MSDeploy. exe). V rámci tohoto procesu nainstaluje obslužnou rutinu Nasazení webu a integruje ji do služby webové správy.
- **.NET Framework 4,0**. To je nutné ke spuštění aplikací, které byly vytvořeny v této verzi .NET Framework.
- **ASP.NET MVC 3**. Tím se nainstaluje sestavení, která potřebujete ke spouštění aplikací MVC 3.

> [!NOTE]
> Tento návod popisuje použití instalačního programu webové platformy k instalaci a konfiguraci různých součástí. I když nemusíte používat instalační program webové platformy, zjednodušuje proces instalace tím, že automaticky detekuje závislosti a zajistil, že vždy získáte nejnovější verze produktu. Další informace najdete v tématu [Instalace webové platformy Microsoft](https://go.microsoft.com/?linkid=9805118).

**Instalace požadovaných produktů a součástí**

1. Stáhněte a nainstalujte [instalační program webové platformy](https://go.microsoft.com/?linkid=9805118).
2. Po dokončení instalace se instalační program webové platformy spustí automaticky.

    > [!NOTE]
    > V nabídce **Start** teď můžete kdykoli spustit instalační program webové platformy. Provedete to tak, že v nabídce **Start** kliknete na **všechny programy**a pak na **Instalace webové platformy Microsoft**.
3. V horní části okna **Instalace webové platformy** klikněte na **Produkty**.
4. Na levé straně okna klikněte v navigačním podokně na možnost **architektury**.
5. Pokud .NET Framework ještě není nainstalovaná, na řádku **Microsoft .NET Framework 4** klikněte na **Přidat**.

    > [!NOTE]
    > Je možné, že jste už nainstalovali .NET Framework 4,0 prostřednictvím web Windows Update. Pokud je produkt nebo součást již nainstalována, instalační program webové platformy tuto skutečnost indikuje tak, že nahrazuje tlačítko **Přidat** s textem, který je **nainstalován**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. V řádku **ASP.NET MVC 3 (Visual Studio 2010)** klikněte na **Přidat**.
7. V navigačním podokně klikněte na možnost **Server**.
8. V řádku **Konfigurace doporučeného pro IIS 7** klikněte na **Přidat**.
9. V řádku **Nástroje pro nasazení webu 2,1** klikněte na **Přidat**.
10. V řádku **Služba IIS: základní ověřování** klikněte na **Přidat**.
11. V řádku **IIS: Management Service** klikněte na **Přidat**.
12. Klikněte na **Nainstalovat**. Instalační program webové platformy zobrazí seznam produktů&#x2014;spolu s případnými přidruženými závislostmi&#x2014;, které se mají nainstalovat, a zobrazí výzvu k přijetí těchto licenčních podmínek.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. Přečtěte si licenční podmínky a pokud souhlasíte s podmínkami **, klikněte na Souhlasím.**
14. Po dokončení instalace klikněte na **Dokončit**a potom zavřete okno **Instalace webové platformy** .

Pokud jste nainstalovali .NET Framework 4,0 před instalací služby IIS, budete muset spustit [registrační nástroj služby ASP.NET IIS](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (ASPNET\_regiis. exe) a zaregistrovat nejnovější verzi ASP.NET se službou IIS. Pokud to neuděláte, zjistíte, že služba IIS bude sloužit jako statický obsah (například soubory HTML) bez jakýchkoli problémů, ale při pokusu o procházení obsahu ASP.NET se nenajde **Chyba HTTP 404,0 – nebude Nalezeno** . K zajištění registrace ASP.NET 4,0 můžete použít další postup.

**Registrace ASP.NET 4,0 se službou IIS**

1. Klikněte na tlačítko **Start**a zadejte **příkaz Command Prompt**.
2. Ve výsledcích hledání klikněte pravým tlačítkem myši na **příkazový řádek**a pak klikněte na **Spustit jako správce**.
3. V okně příkazového řádku přejděte do adresáře **%windir%\Microsoft.NET\Framework\v4.0.30319** .
4. Zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. Pokud máte v úmyslu hostovat 64 webové aplikace v jakémkoli bodě, měli byste také zaregistrovat 64 verzi ASP.NET se službou IIS. To provedete tak, že v okně příkazového řádku přejdete do adresáře **%windir%\Microsoft.NET\Framework64\v4.0.30319** .
6. Zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

Vhodným postupem je znovu použít web Windows Update v tuto chvíli ke stažení a instalaci všech dostupných aktualizací pro nové produkty a komponenty, které jste nainstalovali.

## <a name="configure-the-web-management-service"></a>Konfigurace služby webové správy

Teď, když jste nainstalovali všechno, co potřebujete, je dalším krokem konfigurace služby webové správy ve službě IIS. Na vysoké úrovni budete muset dokončit tyto úlohy:

- Povolí základní ověřování na úrovni serveru.
- Nakonfigurujte službu webové správy tak, aby přijímala vzdálená připojení.
- Spusťte službu webové správy.
- Ověřte, zda jsou zavedena požadovaná pravidla delegování služby webové správy.

**Konfigurace služby webové správy**

1. V nabídce **Start** přejděte na **Nástroje pro správu**a potom klikněte na **Správce služby Internetová informační služba (IIS)** .
2. Ve Správci služby IIS klikněte v podokně **připojení** na uzel serveru (například **STAGEWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. V prostředním podokně v části **IIS**poklikejte na **ověřování**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. Klikněte pravým tlačítkem na **základní ověřování**a pak klikněte na **Povolit**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. V podokně **připojení** znovu klikněte na uzel serveru a vraťte se k nastavení nejvyšší úrovně.
6. V prostředním podokně v části **Správa**poklikejte na **Služba pro správu**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. V prostředním podokně vyberte možnost **Povolit vzdálená připojení**.

    > [!NOTE]
    > Pokud je služba webové správy již spuštěna, je nutné ji nejprve zastavit.
8. V podokně **Akce** klikněte na možnost **Spustit** a spusťte službu webové správy.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. Pokud budete vyzváni k uložení nastavení, klikněte na **Ano**.

    > [!NOTE]
    > Je také možné, že budete chtít službu nakonfigurovat tak, aby se spouštěla automaticky. Provedete to tak, že otevřete konzolu služby, kliknete pravým tlačítkem na možnost **Služba webové správy**a potom kliknete na **vlastnosti**. V rozevíracím seznamu **Typ spouštění** vyberte možnost **automaticky**a pak klikněte na tlačítko **OK**.
10. V podokně **připojení** znovu klikněte na uzel serveru a vraťte se k nastavení nejvyšší úrovně.
11. V prostředním podokně v části **Správa**poklikejte na **delegování služby správy**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. Ověřte, že se v prostředním podokně nachází sada pravidel.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    Tato pravidla umožňují autorizovaným uživatelům služby webové správy používat různé poskytovatele Nasazení webu. Pokud například chcete nasadit webové aplikace a obsah do služby IIS prostřednictvím obslužné rutiny Nasazení webu, musí existovat pravidlo delegování, které umožňuje všem ověřeným uživatelům služby webové správy používat poskytovatele **contentPath** a **iisapp** (poslední pravidlo, které vidíte na snímku obrazovky).

    Pokud jste nainstalovali produkty a komponenty v pořadí popsaném v tomto tématu, nejnovější verze Nasazení webu by měla do služby webové správy automaticky přidat všechna požadovaná pravidla delegování. Pokud stránka pro delegování služby správy nezobrazuje žádná pravidla, budete ji muset vytvořit sami. Pokyny k tomu, jak to provést, najdete v tématu [Konfigurace obslužné rutiny nasazení webu](https://go.microsoft.com/?linkid=9805124).
13. V podokně **připojení** znovu klikněte na uzel serveru a vraťte se k nastavení nejvyšší úrovně.

## <a name="create-and-configure-an-iis-website"></a>Vytvoření a konfigurace webu služby IIS

Předtím, než budete moci nasadit webový obsah na server, je nutné vytvořit a nakonfigurovat web služby IIS pro hostování obsahu. Nasazení webu můžou nasadit jenom webové balíčky na existující web IIS; pro vás nemůže web vytvořit. Je taky potřeba udělat trochu dodatečnou konfiguraci, aby účet bez správce mohl vzdáleně nasazovat obsah. Na vysoké úrovni budete muset dokončit tyto úlohy:

- Vytvořte v systému souborů složku pro hostování vašeho obsahu.
- Vytvořte web IIS pro poskytování obsahu a přidružte ho k místní složce.
- Udělte oprávnění ke čtení identitě fondu aplikací v místní složce.
- Udělte potřebná oprávnění služby IIS účtu domény, který bude nasazovat vaši webovou aplikaci.

I když se vám nic nezastaví od nasazení obsahu na výchozí web ve službě IIS, tento přístup se nedoporučuje pro žádnou jinou než testovací nebo demonstrační scénář. Chcete-li simulovat produkční prostředí, měli byste vytvořit nový web služby IIS s nastavením, které je specifické pro požadavky vaší aplikace.

**Vytvoření webu služby IIS**

1. V místním systému souborů vytvořte složku pro uložení vašeho obsahu (například **C:\DemoSite**).
2. V nabídce **Start** přejděte na **Nástroje pro správu**a potom klikněte na **Správce služby Internetová informační služba (IIS)** .
3. Ve Správci služby IIS rozbalte v podokně **připojení** uzel serveru (například **STAGEWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. Klikněte pravým tlačítkem myši na uzel **lokality** a pak klikněte na možnost **Přidat web**.
5. Do pole **název lokality** zadejte název webu služby IIS (například **DemoSite**).
6. Do pole **fyzická cesta** zadejte (nebo vyhledejte) cestu k místní složce (například **C:\DemoSite**).
7. Do pole **port** zadejte číslo portu, na kterém chcete web hostovat (například **85**).

    > [!NOTE]
    > Standardní čísla portů jsou 80 pro protokol HTTP a 443 pro protokol HTTPS. Pokud však tento web Hostujte na portu 80, budete muset před přístupem k webu zastavit výchozí web.
8. Pole **název hostitele** nechte prázdné, pokud nechcete pro web nakonfigurovat záznam DNS (Domain Name System), a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > V produkčním prostředí pravděpodobně budete chtít web hostovat na portu 80 a nakonfigurovat hlavičku hostitele spolu se shodnými záznamy DNS. Další informace o konfiguraci hlaviček hostitele ve službě IIS 7 najdete v tématu [Konfigurace hlavičky hostitele webu (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx). Další informace o roli serveru DNS v systému Windows Server najdete v tématu [Přehled serveru DNS](https://technet.microsoft.com/library/cc770392.aspx) a [Server DNS](https://technet.microsoft.com/windowsserver/dd448607).
9. V podokně **Akce** klikněte v části **Upravit web**na možnost **vazby**.
10. V dialogu **Vazby webu** klikněte na **Přidat**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. V dialogovém okně **Přidat vazbu webu** nastavte **IP adresu** a **port** tak, aby odpovídaly vaší stávající konfiguraci lokality.
12. Do pole **název hostitele** zadejte název vašeho webového serveru (například **STAGEWEB1**) a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > První vazba webu umožňuje přístup k webu místně pomocí IP adresy a portu nebo `http://localhost:85`. Druhá vazba webu umožňuje přístup k webu z jiných počítačů v doméně pomocí názvu počítače (například http://stageweb1:85).
13. V dialogu **Vazby webu** klikněte na **Zavřít**.
14. V podokně **připojení** klikněte na **fondy aplikací**.
15. V podokně **fondy aplikací** klikněte pravým tlačítkem myši na název vašeho fondu aplikací a potom klikněte na **základní nastavení**. Ve výchozím nastavení bude název vašeho fondu aplikací odpovídat názvu vašeho webu (například **DemoSite**).
16. V seznamu **verze CLR .NET** vyberte **.NET CLR v 4.0.30319**a pak klikněte na **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

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

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. V dialogovém okně **Vybrat uživatele nebo skupiny** zadejte **IIS\_IUSRS**, klikněte na **kontrolovat jména**a pak klikněte na **OK**.
6. V dialogovém okně <strong>oprávnění pro</strong><em>[název složky]</em> si všimněte, že je ve výchozím nastavení přiřazená k nové skupině oprávnění <strong>číst &amp; spustit</strong>, <strong>Zobrazit obsah složky</strong>a <strong>číst</strong> . Nechejte to beze změny a klikněte na <strong>OK</strong>.
7. Kliknutím na tlačítko <strong>OK</strong> zavřete dialogové okno<strong>vlastnosti</strong> <em>[název složky]</em>.

Jako poslední úkol musíte udělit příslušná oprávnění uživateli bez oprávnění správce, jehož přihlašovací údaje použijete k nasazení obsahu. Tento uživatel vyžaduje oprávnění k nasazování obsahu vzdáleně na váš web.

**Konfigurace oprávnění webu IIS pro uživatele domény bez oprávnění správce**

1. Ve Správci služby IIS klikněte v podokně **připojení** pravým tlačítkem myši na uzel webu (například **DemoSite**), přejděte na **nasadit**a potom klikněte na **Konfigurovat nasazení webu publikování**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. V dialogovém okně **Konfigurace publikování nasazení webu** napravo od seznamu **oprávnění vybrat uživatele, který má poskytnout oprávnění k publikování** klikněte na tlačítko se třemi tečkami.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. V dialogovém okně **povolení uživatele** zadejte doménu a uživatelské jméno účtu, který chcete použít k nasazení obsahu, a poté klikněte na tlačítko **OK**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. V dialogovém okně **Konfigurace publikování nasazení webu** klikněte na **Nastavení**.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > Tato operace provádí dvě klíčové funkce v jednom kroku. Nejprve udělí uživateli oprávnění ke změně webu prostřednictvím služby webové správy podle pravidel delegování, které jste prozkoumali v předchozí části. Za druhé udělí uživateli úplnou kontrolu nad zdrojovou složkou webu, která umožňuje uživateli přidávat, upravovat a nastavovat oprávnění k obsahu webu.
5. V dialogovém okně **Konfigurace publikování nasazení webu** klikněte na **Zavřít**.

## <a name="configure-firewall-exceptions"></a>Konfigurace výjimek brány firewall

Ve výchozím nastavení služba správy webu služby IIS naslouchá na portu TCP 8172. Pokud je na vašem webovém serveru povolená brána Windows Firewall, budete muset vytvořit nové příchozí pravidlo povolující přenosy TCP na portu 8172 (v bráně Windows Firewall je povolený veškerý odchozí provoz). Pokud používáte bránu firewall jiného výrobce, budete muset vytvořit pravidla, která budou umožňovat provoz.

| Směr | Z portu | Na port | Typ portu |
| --- | --- | --- | --- |
| Příchozí | Všechny | 8172 | TCP |
| Odchozí | 8172 | Všechny | TCP |

Další informace o konfiguraci pravidel v bráně Windows Firewall najdete v tématu [Konfigurace pravidel brány firewall](https://technet.microsoft.com/library/dd448559(WS.10).aspx). Pro brány firewall třetích stran si prosím přečtěte dokumentaci k produktu.

## <a name="conclusion"></a>Závěr

Váš webový server by teď měl být připravený přijmout vzdálená nasazení do Nasazení webu obslužné rutiny prostřednictvím služby webové správy. Předtím, než se pokusíte nasadit webovou aplikaci na server, je vhodné tyto klíčové body ověřit:

- Povolili jste základní ověřování na úrovni serveru ve službě IIS?
- Povolili jste vzdálená připojení ke službě webové správy?
- Začali jste službu webové správy?
- Jsou zavedena pravidla delegování služby správy?
- Má identita fondu aplikací oprávnění ke čtení pro zdrojovou složku vašeho webu?
- Má účet uživatele bez oprávnění správce oprávnění na úrovni webu ve službě IIS?
- Povoluje brána firewall příchozí připojení k serveru na portu TCP 8172?

## <a name="further-reading"></a>Další čtení

Pokyny ke konfiguraci vlastních souborů projektu Microsoft Build Engine (MSBuild) pro nasazení webových balíčků do obslužné rutiny Nasazení webu najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](configuring-deployment-properties-for-a-target-environment.md).

> [!div class="step-by-step"]
> [Předchozí](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [Další](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
